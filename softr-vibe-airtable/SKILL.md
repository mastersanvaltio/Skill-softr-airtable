---
name: softr-vibe-airtable
description: Generate, edit, or debug React components for Softr Vibe Coding Blocks connected to Airtable as the data source. Use this skill ANY time the user mentions Softr, Vibe Coding Block, "the block", a `.jsx` file that imports from `@/lib/datasource`, or asks for components that read/write Airtable through Softr hooks (`useRecords`, `useRecord`, `useLinkedRecords`, `useRecordUpdate`, `useRecordCreate`, `useUpload`, `useCurrentRecordId`, `q.select`). Trigger this skill even when the user only describes the goal ("a kanban of projects in my Softr app", "an editable list synced to Airtable", "a dashboard for my Softr portal", "make me a block that…") without naming Softr explicitly — if the stack is React + Airtable through a single `.jsx` file pasted into a block's Content area, this skill applies. Also trigger when the user reports symptoms typical of Softr/Airtable integration issues: blank block on save, dropdown that opens but doesn't select, attachments PATCH 500, mutations that "do nothing", linked-record fields that don't save, formulas that don't refresh, "Cannot access X before initialization", React error #310. The skill includes a separate Welldone reference file with all tables, fields and option IDs — load it ONLY when the user mentions Welldone, Portal Empresarial Welldone, or the base ID `appAEV0iaC3VfB5Zb`.
---

# Softr Vibe Coding Block + Airtable

This skill captures the rules, patterns and pitfalls for building React components that live inside Softr's Vibe Coding Block and read/write data from an Airtable base through Softr's `@/lib/datasource` hooks.

A "block" is a single `.jsx` file that the user pastes into the **Content** area of a Softr Vibe Coding Block. There is no build step, no bundler, no file system — it's just a React component evaluated at runtime by Softr.

The user always communicates in **Spanish** by default. Respond in Spanish. Code comments may be Spanish or English.

## When this skill applies

- Building a new block (form, table, kanban, dashboard, timeline, detail view, editable list, etc.)
- Editing an existing `.jsx` file from a Softr block
- Debugging a block (blank screen, mutation not saving, dropdown not working, attachments failing)
- Any question about hooks `useRecords`, `useRecord`, `useLinkedRecords`, `useRecordUpdate`, `useRecordCreate`, `useUpload`, `useCurrentRecordId`, or the `q.select()` helper

## Workflow

1. **Understand the goal.** Block type (list / detail / form / kanban / timeline), expected interactions (read-only, inline edit, modal form, drag-and-drop).
2. **Gather Airtable context.** Ask the user — never invent — for table name + ID (`tblXXX`), exact field names, field types, and for any `singleSelect` mutated with create, the option IDs (`selXXX`) and labels.
   - **Exception:** if the user mentions **Welldone**, **Portal Empresarial Welldone**, or the base ID `appAEV0iaC3VfB5Zb`, load `references/welldone-airtable-schema.md` first — most context is already there.
   - If MCP for Airtable is available, prefer querying the schema directly over asking.
3. **Choose the right hook** (see "Hook selection" below).
4. **Write a single `.jsx` file** following the structural rules. Output one file, never split into multiple modules.
5. **Self-check** against the "Pre-delivery checklist" before declaring done.
6. **Deliver.** Save to disk and call `present_files` so the user can download/copy the file.

When the user asks for changes to an existing block, **edit the existing file with `str_replace`**. Do not rewrite the whole file unless the change is so pervasive that surgical edits would be more error-prone.

## Required inputs before coding

These must be confirmed before generating any code. Ask in groups, briefly, only what's missing.

**Table and fields:**
1. Which table does the block use? (name + ID `tblXXX`)
2. Which fields need to be read? For each: exact name + type (`singleLineText`, `singleSelect`, `multipleRecordLinks`, `percent`, `currency`, `date`, `formula`, `multipleAttachments`, etc.)
3. Which fields will be edited or created (separated from read-only)?

**If `singleSelect` will be written via create:**

4. IDs and labels of each option (`selXXX` + label). Required for `useRecordCreate`.

**If `multipleRecordLinks` will be used:**

5. Linked table (name + ID).
6. Need a searchable dropdown to assign? (yes/no)

**Block context:**

7. List page or detail page? (Detail uses `useCurrentRecordId` + `useRecord`.)
8. Visual style? Light client portal `#EFF6FF` / dark admin `#10172A` / custom (Welldone style is OPTIONAL — only apply if the user explicitly says it's for Welldone).
9. Functionality? (list, editable inline table, form, dashboard, timeline, kanban…)
10. Deletion? Use **soft delete** (`Estado = "Inactivo"`). Confirm whether such a field exists.

**Never invent IDs `selXXX`, `recXXX`, `tblXXX`.** If the user doesn't have them, ask or query Airtable schema via MCP.

## The non-negotiable import

Every block must include this import. Without it none of the data hooks work, and the block silently renders blank.

```js
import {
  useRecords, useRecord, useLinkedRecords, useFieldOptions, q,
  useRecordUpdate, useRecordCreate, useRecordDelete,
  useCurrentRecordId, useUpload,
} from "@/lib/datasource";
```

Import only the hooks actually used, but the path `"@/lib/datasource"` is **mandatory**. React itself, hooks, `lucide-react`, and the `@/components/ui/*` UI primitives are also imported normally.

> ⚠️ **`useCurrentUser` viene de un path diferente:**
> ```js
> import { useCurrentUser } from "@/lib/user";
> ```
> **No** lo importes desde `@/lib/datasource` — causará error silencioso en el bloque.

## `useCurrentUser` — email del usuario logueado

```js
import { useCurrentUser } from "@/lib/user";

// Uso básico — email estándar de Softr (minúsculas, siempre)
const currentUser = useCurrentUser();
const userEmail = currentUser?.email || "";

// Uso con campos personalizados de la tabla de usuarios en Airtable.
// El lado derecho es el NOMBRE (label) del campo, no un Field ID ni un ID interno.
const currentUser = useCurrentUser({
  properties: {
    nombre: "Nombre",   // label exacto del campo en availableProperties[].label
    cedula: "Cédula",
  },
});
const nombreTecnico =
  typeof currentUser?.properties?.nombre === "string"
    ? currentUser.properties.nombre
    : currentUser?.fullName || "";
```

**Reglas:**
- Importar siempre desde `"@/lib/user"`, nunca desde `"@/lib/datasource"`.
- La propiedad estándar es `email` (minúscula). `Email` con mayúscula **no existe**.
- Para campos personalizados del perfil Softr, usar `properties: { alias: "nombreInterno" }` y leer con `currentUser?.properties?.alias`.
- Para el caso Welldone: `currentUser?.email` devuelve el correo con el que el empleado inició sesión — suficiente para crear links a BD empleados via `[{ id: email, label: email }]`.

### `user.id` — Record ID del usuario en Airtable

Cuando la app de Softr tiene **User sync** habilitado (tabla de usuarios conectada a una tabla de Airtable), `user.id` devuelve el `recXXX` del registro del usuario en esa tabla. Esto permite auto-rellenar campos `multipleRecordLinks` con el usuario actual **sin que el usuario tenga que seleccionarse de una lista**.

```js
import { useCurrentUser } from "@/lib/user";

const user = useCurrentUser();

// user.id  → "recXXXXXXXXXXXXX" (Record ID en Airtable) — solo si User sync está habilitado
// user.email     → email del usuario logueado
// user.fullName  → nombre completo
// user.firstName / user.lastName
// user.avatar    → URL del avatar
```

**Patrón: auto-rellenar un campo `multipleRecordLinks` con el usuario logueado**

```js
// En el payload de useRecordCreate:
// multipleRecordLinks → flat array de strings (formato canónico para create)
if (user?.id) {
  fields.persona = [user.id];
}
```

> ⚠️ **Usar flat array de strings** (`[user.id]`), NO `[{ id: user.id, label: "..." }]`.
> El formato objeto puede fallar silenciosamente en `useRecordCreate` para `multipleRecordLinks`.

**Acceder a campos personalizados de la tabla de usuarios en Airtable:**

El lado derecho de `properties` es el **nombre (label) exacto del campo** tal como aparece en `availableProperties[].label`. **No uses Field IDs de Airtable ni IDs internos.**

```js
// ✅ CORRECTO — usar el nombre del campo (label)
const user = useCurrentUser({
  properties: {
    nombre:      "Nombre",        // alias: label exacto
    cedula:      "Cédula",
    cargo:       "Cargo",
    area:        "Área",
    valorXDia:   "Valor x día",
  },
});

const nombreTecnico = typeof user?.properties.nombre === "string"
  ? user.properties.nombre
  : user?.fullName || "";

// ❌ INCORRECTO — no uses Field IDs ni IDs internos de Softr
const user = useCurrentUser({
  properties: {
    nombre: "fldXXXXX",  // ❌ Field ID de Airtable — no funciona
    correo: "ddSsS",     // ❌ ID interno de Softr — no funciona
  },
});
```

**Cuándo `user.id` es null:**
- User sync **no está habilitado** en la app de Softr.
- La tabla de usuarios no está conectada a Airtable.
- El usuario no está autenticado.

En esos casos, como fallback mostrar un selector manual o dejar el campo vacío.

## Available libraries

```js
import React, { useState, useEffect, useMemo, useRef } from "react";
import { Dialog, DialogContent, DialogHeader, DialogTitle, DialogFooter } from "@/components/ui/dialog";
import { Button } from "@/components/ui/button";
import { Input } from "@/components/ui/input";
import { Textarea } from "@/components/ui/textarea";
import { /* needed icons */ } from "lucide-react";
```

Tailwind: only **core utility classes**. No custom Tailwind compiler available — avoid arbitrary values like `bg-[#10172A]`. Use `style={{ backgroundColor: "#10172A" }}` for hex colors.

## Hook selection

| Goal | Hook | Notes |
|---|---|---|
| List of records (with pagination) | `useRecords({ select, count: 100 })` | Always implement auto-pagination |
| Detail of a single record (detail page) | `useRecord({ recordId, select })` | Combine with `useCurrentRecordId()` |
| Options of a `multipleRecordLinks` field for a dropdown | `useLinkedRecords({ select, field, search, enabled })` | `field` is the **alias** declared in `q.select()`, not the real field name |
| Options of a `singleSelect` / `multipleSelects` field | `useFieldOptions({ select, field })` | Returns `{ options, isLoading }` where `options` is `[{ id, label, color }]`. Auto-syncs with Airtable schema |
| Update one record | `useRecordUpdate({ fields, onSuccess })` | `fields` is a separate write-only `q.select()` |
| Create a record | `useRecordCreate({ fields, onSuccess })` | Different payload format from update |
| Upload files (returns public URLs) | `useUpload()` | Returns `{ uploadAsync, isUploading }` |
| Current record ID on a detail page | `useCurrentRecordId()` | Only works on Softr "detail" pages |

### `useRecord` vs `useRecords`

In **detail** pages (single row), always use `useRecord` (singular):

```js
const recordId = useCurrentRecordId();
const { data, status, refetch } = useRecord({ recordId, select });
const f = data?.fields || {};   // fields directly accessible
```

Advantages over `useRecords` + filter:
- No pagination or `flatMap` needed.
- No risk of fetching extra records.
- Cleaner API: `data.fields.field` directly.

`useRecords` is for **lists** (multiple records).

### `useLinkedRecords` — load options for a linked field

For getting available records of a `multipleRecordLinks` field (to populate a dropdown), use `useLinkedRecords`. **Do not** use a second `useRecords` of the linked table.

```js
const { data: linkedData, status: linkedStatus } = useLinkedRecords({
  select,          // same select as the block (must include the linked field)
  field: "alias",  // the alias of the multipleRecordLinks field in the select
  search: query,   // optional: server-side search
  enabled: open,   // only load when needed (e.g., when dropdown opens)
  // linkedRecordViewId: "viwXXXXX",  // optional: filter by an Airtable view
});

const items = linkedData?.pages?.flatMap(p => p.items) ?? [];
// Each item has: { id, title, label }
```

**Rules:**
- `field` must match the **alias** (not the real field name) declared in `q.select()`.
- `enabled: false` avoids unnecessary calls. Activate only when the dropdown opens.
- `search` filters server-side — ideal for large tables.
- Items return `title` as primary label (sometimes also `label`). Always read `.title || .label || .id`.

#### Complete pattern: linked dropdown with search

```jsx
function LinkedDropdown({ selectedIds, onChange, disabled }) {
  const [open, setOpen]     = useState(false);
  const [search, setSearch] = useState("");
  const ref = useRef(null);

  // CRITICAL: outside-click handler — see "Custom dropdowns" pitfall below
  useEffect(() => {
    if (!open) return;
    function handleClickOutside(e) {
      if (ref.current && !ref.current.contains(e.target)) setOpen(false);
    }
    const t = setTimeout(() => {
      document.addEventListener("click", handleClickOutside);
    }, 0);
    return () => {
      clearTimeout(t);
      document.removeEventListener("click", handleClickOutside);
    };
  }, [open]);

  const { data, status } = useLinkedRecords({
    select, field: "miCampoVinculado", search, enabled: open,
  });

  const options = (data?.pages?.flatMap(p => p.items) ?? [])
    .map(it => ({ id: it.id, label: it.title || it.label || it.id }));

  const selectedSet = new Set(
    (Array.isArray(selectedIds) ? selectedIds : [])
      .map(x => typeof x === "string" ? x : x?.id)
      .filter(Boolean)
  );

  const toggle = (id) => {
    const next = selectedSet.has(id)
      ? [...selectedSet].filter(x => x !== id)
      : [...selectedSet, id];
    onChange(next);  // flat array of IDs
  };

  return (
    <div ref={ref} className="relative">
      <button onClick={() => setOpen(v => !v)} disabled={disabled}>
        {/* selection summary */}
      </button>
      {open && (
        <div className="absolute top-full mt-1 bg-white border rounded-lg shadow-lg z-30">
          <input autoFocus type="text" value={search}
            onChange={(e) => setSearch(e.target.value)} placeholder="Buscar…" />
          {status === "pending" ? <Loader2 /> : options.map(o => (
            <button key={o.id} type="button"
              onClick={(e) => {
                e.stopPropagation();
                e.preventDefault();
                toggle(o.id);
              }}>
              {selectedSet.has(o.id) ? "✓" : ""} {o.label}
            </button>
          ))}
        </div>
      )}
    </div>
  );
}
```

### `useFieldOptions` — load options for a `singleSelect` / `multipleSelects` field

For dropdowns of select fields (e.g. "Estado", "Nombre del activo", "Tipo de necesidad"), use `useFieldOptions`. **Do not** hardcode option IDs — they get pulled live from the Airtable schema, so adding/removing options in Airtable updates the dropdown without touching code.

```js
const { options, isLoading } = useFieldOptions({
  select,
  field: "nombreActivo",   // alias declared in the q.select()
});
// options: [{ id: "selXXX", label: "Texto", color: "blueLight2" | null }]
```

**Rules:**
- `field` must match the **alias** in the `q.select()` (just like `useLinkedRecords`).
- Returns synchronously cached after first load — safe to call on every render.
- Use the `id` for create payloads (`{ id: "sel...", label }`), but the `label` (string) for update payloads.
- Color may be a Airtable color name (`"redLight2"`, `"greenBright"`, etc.) — usually safer to map to your own palette.

#### Pattern: select dropdown with `useFieldOptions`

```jsx
function SelectDropdown({ value, onChange, fieldName, placeholder = "Seleccionar..." }) {
  const [open, setOpen]     = useState(false);
  const [search, setSearch] = useState("");
  const ref = useRef(null);

  // SAME outside-click pattern as ClienteDropdown — see "Custom dropdowns" pitfall
  useEffect(() => {
    if (!open) return;
    function handleClickOutside(e) {
      if (ref.current && !ref.current.contains(e.target)) setOpen(false);
    }
    const t = setTimeout(() => {
      document.addEventListener("click", handleClickOutside);
    }, 0);
    return () => {
      clearTimeout(t);
      document.removeEventListener("click", handleClickOutside);
    };
  }, [open]);

  const { options, isLoading } = useFieldOptions({ select, field: fieldName });

  const filtered = (options || []).filter(o =>
    !search || o.label.toLowerCase().includes(search.toLowerCase())
  );

  return (
    <div ref={ref} className="relative">
      <button type="button" onClick={() => setOpen(v => !v)}>
        {value || placeholder}
      </button>
      {open && (
        <div className="absolute top-full left-0 right-0 mt-1 z-30 bg-white border rounded-lg shadow-lg max-h-72 overflow-hidden flex flex-col">
          {/* Optional client-side search — useful when there are 20+ options */}
          <input autoFocus type="text" value={search}
            onChange={(e) => setSearch(e.target.value)} placeholder="Buscar…" />
          <div className="overflow-y-auto flex-1">
            {isLoading
              ? <Loader2 className="animate-spin" />
              : filtered.map(o => (
                  <button key={o.id} type="button"
                    onClick={(e) => {
                      e.stopPropagation();
                      e.preventDefault();
                      onChange(o.label);   // UPDATE → send the label string
                      setOpen(false);
                    }}>
                    {value === o.label ? "✓" : ""} {o.label}
                  </button>
                ))}
          </div>
        </div>
      )}
    </div>
  );
}
```

**When to use `useLinkedRecords` vs `useFieldOptions`:**

| Field type | Hook |
|---|---|
| `multipleRecordLinks` | `useLinkedRecords` |
| `singleSelect` / `multipleSelects` | `useFieldOptions` |

Never invent `selXXX` IDs again — `useFieldOptions` removes the need.

## Component structure (mandatory order)

Inside the `Block()` component, this order is enforced:

1. **All hooks first** — `useState`, `useEffect`, `useRecords`, mutations, refs.
2. **Data processing** — `useMemo`, filters, sorts, derived arrays.
3. **Early returns** — loading/error states, AFTER all hooks have run.
4. **Handlers** — async functions, event callbacks.
5. **JSX return.**

```js
export default function Block() {
  // 1. ALL hooks first (useState, useEffect, useRecords, mutations…)
  // 2. Data processing (useMemo, filters, sorts)
  // 3. Early returns (loading, error)
  // 4. Handlers
  // 5. JSX return
}
```

Helper components (rows, cards, modals) must be defined **outside** `Block()`. Defining them inside causes React error #310 (different number of hooks between renders).

## Field types: read and write reference

| Airtable type | Read with | Update payload | Create payload |
|---|---|---|---|
| `singleLineText` / `multilineText` | `getVal(v)` | `string` | `string` |
| `number` / `currency` | `getNum(v)` | `number` | `number` |
| `percent` | `Math.round(getNum(v))` (Softr returns it ×100, e.g. 8 for 8%) | `number` (integer, e.g. `8`) | `number` |
| `singleSelect` | `getVal(v)` | `"Label"` (plain string) | `{ id: "selXXX", label: "Label" }` (object) |
| `multipleSelects` | array → `getVal()` | array of strings | array of strings |
| `multipleRecordLinks` | `getVal(v)` returns label | **flat array of IDs**: `["recAAA", "recBBB"]` | same flat array |
| `date` | `"YYYY-MM-DD"` | `"YYYY-MM-DD"` | `"YYYY-MM-DD"` |
| `dateTime` | ISO string | ISO string | ISO string |
| `checkbox` | boolean | boolean | boolean |
| `multipleAttachments` (own field) | `getAttachments(v)` | array of `{ url, filename }` (uniform!) | safer to create empty + update after |
| `multipleAttachments` (lookup) | `getAttachments(v)` | ❌ not editable | ❌ not editable |
| `formula` / `rollup` / `lookup` / `autoNumber` | `getVal(v)` or `getNum(v)` | ❌ not editable | ❌ not editable |
| `multipleLookupValues` with linked record | `getLookupVal(v)` (special structure) | ❌ not editable | ❌ not editable |

## Mandatory helpers

Always include these (or those used) at the top of the file:

```js
function getVal(v) {
  if (v === null || v === undefined) return "";
  if (Array.isArray(v)) return getVal(v[0]);
  if (typeof v === "object") return v.label || v.name || "";
  return String(v);
}

function getNum(v) {
  if (typeof v === "number") return v;
  if (!v) return 0;
  const n = parseFloat(String(v).replace(/[^-0-9.]/g, ""));
  return isNaN(n) ? 0 : n;
}

function fmtCOP(v) {
  const n = getNum(v);
  if (n === 0) return "$0";
  return new Intl.NumberFormat("es-CO", {
    style: "currency", currency: "COP",
    minimumFractionDigits: 0, maximumFractionDigits: 0
  }).format(n);
}

function fmtPct(v) {
  if (v === null || v === undefined || v === "") return "—";
  return Math.round(getNum(v)) + "%";
}

// multipleLookupValues with linked records have a special shape
function getLookupVal(v) {
  if (!v) return "";
  if (typeof v === "object" && v.valuesByLinkedRecordId) {
    const values = Object.values(v.valuesByLinkedRecordId);
    if (values.length > 0 && values[0].length > 0) return values[0][0]?.name || "";
  }
  return getVal(v);
}

function getAttachments(v) {
  if (!v) return [];
  const arr = Array.isArray(v) ? v : [v];
  const result = [];
  arr.forEach(item => {
    if (!item) return;
    if (typeof item === "string") result.push({ url: item, filename: "Archivo" });
    else if (typeof item === "object" && item.url) {
      result.push({
        id: item.id || null,                              // tracking only — never sent to Airtable
        url: item.url,
        filename: item.filename || item.name || "Archivo",
      });
    }
  });
  return result;
}
```

## Reading: select with aliases

```js
const select = q.select({
  alias: "Exact field name in Airtable",
});

const { data, status, refetch, fetchNextPage, hasNextPage, isFetchingNextPage } =
  useRecords({ select, count: 100 });
```

### Auto-pagination (ALWAYS implement if more than 100 records possible)

```js
useEffect(() => {
  if (hasNextPage && !isFetchingNextPage) fetchNextPage();
}, [hasNextPage, isFetchingNextPage, data]);

const allRecords = (data?.pages || []).flatMap(p => p.items || []);
```

## Mutations: critical patterns

### Always use a separate write-fields select

```js
// ⚠️ DECLARE BOTH AT MODULE LEVEL — never inside Block().
//    Inside Block() they get re-created each render, which causes
//    useRecord/useRecordUpdate to thrash and mutations to fail silently
//    (no error, no log — the .mutate() call simply does nothing).

const select = q.select({ /* all read fields */ });
const writeFields = q.select({ /* only fields you'll mutate */ });

export default function Block() {
  const { data, status, refetch } = useRecord({ recordId, select });

  const updateRecord = useRecordUpdate({
    fields: writeFields,
    async onSuccess() {
      await refetch();
      setTimeout(() => refetch(), 2000);  // formulas recalc slowly
      setTimeout(() => refetch(), 5000);
    }
  });

  updateRecord.mutate({ recordId, fields: { campo: valor } });
}
```

**Symptom of breaking this rule:** the block renders fine and reads data,
but every inline edit / drop / create / delete is silent — UI behaves as if
nothing happened, no console error, no network request rejected. Moving
both selects out of `Block()` immediately restores all mutations.

### Softr's strict linter on `q.select()` — two non-negotiable rules

Softr Studio's editor runs an AST linter on Vibe Coding Blocks before letting you save. It enforces two specific shapes:

**1. `q.select()` MUST receive an object literal — not a variable, not a function call result.**

```js
// ❌ Rejected: "q.select() requires an object literal as the first argument"
const fieldMap = { name: "Name", email: "Email" };
const select = q.select(fieldMap);

// ❌ Rejected: dynamic generation
function buildMap() { return { /* … */ }; }
const select = q.select(buildMap());

// ✅ Required: inline object literal
const select = q.select({
  name: "Name",
  email: "Email",
});
```

If you have many repeated alias patterns (e.g. `field_1`, `field_2`, … `field_6` for slot-style records), **list every key explicitly** in the literal. Don't try to generate them with loops or spread — the linter rejects it. Yes, even if it means 70+ lines of literal keys.

**2. `useRecordUpdate({ fields })` MUST be a direct `q.select()` call OR a one-level reference.**

```js
// ❌ Rejected: two levels of indirection
const select = q.select({ /* … */ });
const writeFields = select;
useRecordUpdate({ fields: writeFields });  // linter follows writeFields → select → q.select() = 2 hops

// ✅ Either of these works:

// Option A — direct call inline
useRecordUpdate({ fields: q.select({ name: "Name" }) });

// Option B — one-level variable reference
const writeFields = q.select({ name: "Name" });
useRecordUpdate({ fields: writeFields });
```

When the read `select` and `writeFields` overlap, **duplicate the literal** — don't alias one to the other. The cost is a few more lines; the alternative is a save-blocking error.

### Awaiting a mutation in a sequence

```js
await new Promise((resolve, reject) => {
  updateRecord.mutate(payload, { onSuccess: resolve, onError: reject });
}).catch(() => {});
```

### `useRecordCreate` payload format

```js
// singleSelect  → { id: "sel...", label: "Option" }  — REAL Airtable ID
// linked record → [{ id: "rec...", label: "rec..." }] OR ["recXXX"]
// percent       → integer (e.g. 8 for 8%)

createRecord.mutate({
  campoSingleSelect: { id: "selXXX", label: "Option" },
  campoLinkedRecord: [{ id: parentId, label: parentId }],
  campoTexto: "value",
  campoPorcentaje: 25,
});
```

### IDs of singleSelect — declare as constants

```js
// Declare all option IDs used in mutations as a SEL object
// at the top of the file, OUTSIDE the component
const SEL = {
  tipo_item:    { id: "selx9JIeAbD6AUEy9", label: "Ítem" },
  tipo_subitem: { id: "selkDlUqz7h6STrM0", label: "Sub-Ítem" },
  est_activo:   { id: "selXbGKkApOeTXOtJ", label: "Activo" },
};
```

### Soft delete (recommended over hard delete)

```js
// Pattern: never delete records from Airtable,
// mark them as "Inactivo" and filter in code
async function handleSetInactive(recordId) {
  setDeletingId(recordId);
  await new Promise((resolve, reject) => {
    updateRecord.mutate(
      { recordId, fields: { estado: "Inactivo" } },
      { onSuccess: resolve, onError: reject }
    );
  }).catch(() => {});
  setDeletingId(null);
}

// Filter actives in code (the Source must NOT filter by state)
const active = allRecords.filter(r => getVal(r.fields?.estado) !== "Inactivo");
```

## Inline edit pattern (editable cells)

For table-like or form-like blocks with inline edit, use the editable cell pattern:

```jsx
// Shared state: a single state controls which cell is in edit mode
const [editingCell, setEditingCell] = useState(null);

// Each cell has a unique ID: `${recordId}-${alias}`
// Example: "recXXXXXX-descripcion"

function EditableCell({ value, type, onSave, isEditing, setEditing, cellId,
                        align = "left", singleClick = false, options = [] }) {
  const [val, setVal] = React.useState(value);
  React.useEffect(() => { setVal(value); }, [value]);

  const commit = (newVal) => {
    setEditing(null);
    const parsed = (type === "number" || type === "currency") ? Number(newVal) : newVal;
    if (parsed !== value) onSave(parsed);
  };

  if (isEditing === cellId) {
    if (type === "select") {
      return (
        <select autoFocus
          className="border-2 border-blue-500 p-1 text-black w-full bg-white outline-none rounded text-sm"
          value={val} onChange={e => setVal(e.target.value)} onBlur={() => commit(val)}>
          {options.map(o => <option key={o} value={o}>{o}</option>)}
        </select>
      );
    }
    if (type === "textarea") {
      return (
        <textarea autoFocus
          className="border-2 border-blue-500 p-1 text-black w-full bg-white outline-none rounded text-sm min-h-[56px]"
          value={val} onChange={e => setVal(e.target.value)} onBlur={() => commit(val)} />
      );
    }
    return (
      <input autoFocus type={type === "number" || type === "currency" ? "number" : "text"}
        className="border-2 border-blue-500 p-1 text-black w-full bg-white outline-none rounded text-sm"
        value={val} onChange={e => setVal(e.target.value)} onBlur={() => commit(val)} />
    );
  }

  return (
    <div
      onClick={singleClick ? () => setEditing(cellId) : undefined}
      onDoubleClick={!singleClick ? () => setEditing(cellId) : undefined}
      className="py-2 px-1 cursor-text hover:bg-black/5 rounded min-h-[38px] flex items-center"
    >
      <span className="text-sm">
        {type === "currency" ? fmtCOP(val) : (val || <span className="text-gray-300 italic text-xs">edit</span>)}
      </span>
    </div>
  );
}
```

**Pattern rules:**
- `singleClick = true` for sub-items or secondary cells.
- `singleClick = false` (double-click) for main or critical cells.
- `onBlur` always commits.
- Save only if value changed (`parsed !== value`).
- `autoFocus` so user can type immediately.

## Two-step delete confirmation pattern (trash pending)

To avoid accidental deletes:

```jsx
const [trashPending, setTrashPending] = useState(null);
const [deletingId,   setDeletingId]   = useState(null);

// First click: mark as pending (highlights red).
// Second click: execute soft delete.
// Reset on click anywhere in table.

<div onClick={() => { if (trashPending) setTrashPending(null); }}>
  ...table...
</div>

<td
  onClick={e => {
    e.stopPropagation();
    if (isPending) {
      handleSetInactive(recordId);   // second click → delete
    } else {
      setTrashPending(recordId);     // first click → confirm
    }
  }}
  className={isPending ? "bg-red-500" : "bg-slate-50"}
>
  <button className={isPending ? "text-white" : "opacity-0 group-hover:opacity-100 text-red-400"}>
    {isDeleting ? <Loader2 size={15} className="animate-spin" /> : <Trash2 size={15} />}
  </button>
</td>
```

## Decimal-position reordering pattern

To move records up/down without re-sorting all of them, interpolate the numeric order field:

```js
// Move up:
if (idx === 0) return;                     // already first
if (idx - 1 === 0) {
  newOrden = valPrev - 1;                  // jump to first
} else {
  newOrden = (valPrevPrev + valPrev) / 2;  // midpoint between previous two
}

// Move down:
if (idx === items.length - 1) return;      // already last
if (idx + 1 === items.length - 1) {
  newOrden = valNext + 1;                  // jump to last
} else {
  newOrden = (valNext + valNextNext) / 2;  // midpoint between next two
}

updateRecord.mutate({ recordId: itemId, fields: { orden: newOrden } });
```

**Important:** the `Orden` field must be numeric, and `ID Numero` should be a formula that uses `Orden` as the sort base.

## Per-operation loading states

For blocks with multiple records edited in parallel, use loading state per record ID:

```js
const [savingOrder,     setSavingOrder]     = useState(null); // recordId in progress
const [creatingItem,    setCreatingItem]    = useState(false);
const [creatingSubFor,  setCreatingSubFor]  = useState(null); // parentId in progress
const [templateLoading, setTemplateLoading] = useState(null); // recordId in progress

if (savingOrder) return; // block if another op in progress
```

## Cross-block communication via `window.__variable`

Softr does not allow two blocks on the same page to share a Source or pass props. The only clean way is to expose values on `window` under a `__` prefix.

### Basic pattern — share data and refetch

```js
// ─── Block A (Source = Projects) — producer ────────────────────────────────
const { data, refetch, status } = useRecords({ select, count: 100 });
const projects = (data?.pages || []).flatMap(p => p.items || []);

useEffect(() => {
  window.__projectsData    = projects;
  window.__projectsStatus  = status;
  window.__projectsRefetch = refetch;

  // Notify other blocks that data is ready
  window.dispatchEvent(new CustomEvent("app:projects-ready"));
}, [projects, status, refetch]);
```

```js
// ─── Block B (Source = another table) — consumer ───────────────────────────
const [projects, setProjects] = useState([]);

useEffect(() => {
  // Already loaded?
  if (window.__projectsData) setProjects(window.__projectsData);

  // Subscribe to future updates
  const handler = () => setProjects(window.__projectsData || []);
  window.addEventListener("app:projects-ready", handler);
  return () => window.removeEventListener("app:projects-ready", handler);
}, []);
```

### Force a refetch on the producer from the consumer

When Block B mutates data that affects Block A:

```js
// In Block B's onSuccess
if (typeof window.__projectsRefetch === "function") {
  setTimeout(() => window.__projectsRefetch(), 500);
  // Double refetch for slow formulas
  setTimeout(() => window.__projectsRefetch(), 3000);
}
```

### Rules

| Rule | Why |
|---|---|
| Always prefix with `__` (`window.__nameData`) | Avoid clashes with Softr/React globals |
| Specific names (`__projectsData`, never `__data`) | Multiple blocks expose vars; generic names collide |
| Write in `useEffect`, never during render | Writing to `window` during render breaks SSR |
| Cleanup listeners (`removeEventListener`) | Avoid memory leaks on page change |
| Never assume the producer loaded already | Consumer handles `undefined` with fallback (`window.__data || []`) |
| Communicate **data**, not **React components** | Never expose JSX or hooks via `window` — only serializable data and simple functions |

## Auto-refresh for formula fields

Airtable formulas take 2–5 seconds to recalculate after a mutation:

```js
const updateRecord = useRecordUpdate({
  fields: writeFields,
  async onSuccess() {
    await refetch();
    setTimeout(async () => { await refetch(); }, 2000);
    setTimeout(async () => { await refetch(); }, 5000);
  }
});

// Read-only summary blocks (totals, dashboards):
useEffect(() => {
  const interval = setInterval(() => { refetch(); }, 5000);
  return () => clearInterval(interval);
}, []);
```

## Critical pitfalls (the recurring bugs)

These come from real bugs in past blocks. Read carefully — each one has cost hours.

### 1. Custom dropdowns: `mousedown` vs `click` event order — #1 CAUSE OF "DROPDOWN OPENS BUT DOESN'T SELECT"

Custom dropdowns that close on outside click WILL break if the listener uses `mousedown`. The browser fires `mousedown` → `mouseup` → `click`, so:

1. User clicks an option.
2. `mousedown` on `document` fires → closes dropdown → React unmounts options.
3. `click` arrives but the option element is gone → `onClick` never runs.

**Symptom:** dropdown opens and closes, but selecting an option does nothing. Mutations don't fire, filters don't change.

**Fix — three changes together:**

```jsx
function MyDropdown({ value, onChange }) {
  const [open, setOpen] = useState(false);
  const ref = useRef(null);

  // 1. Listener on "click" (NOT "mousedown") — same timing as option clicks
  // 2. setTimeout(0) so the listener doesn't capture the click that opened it
  useEffect(() => {
    if (!open) return;
    function handleClickOutside(e) {
      if (ref.current && !ref.current.contains(e.target)) setOpen(false);
    }
    const t = setTimeout(() => {
      document.addEventListener("click", handleClickOutside);
    }, 0);
    return () => {
      clearTimeout(t);
      document.removeEventListener("click", handleClickOutside);
    };
  }, [open]);

  return (
    <div ref={ref} className="relative">
      <button onClick={() => setOpen(v => !v)}>{value}</button>

      {open && (
        <div className="absolute top-full left-0 mt-1 z-40 ...">
          {options.map(opt => (
            <button
              key={opt.id}
              type="button"
              onClick={(e) => {
                e.stopPropagation();
                e.preventDefault();
                onChange(opt);
                setOpen(false);
              }}
            >
              {opt.label}
            </button>
          ))}
        </div>
      )}
    </div>
  );
}
```

**Mandatory checklist for every custom dropdown:**

| Rule |
|---|
| Outside-click listener on `"click"`, **never** `"mousedown"` |
| `setTimeout(() => document.addEventListener(...), 0)` to skip the opening click |
| Cleanup with `clearTimeout` and `removeEventListener` |
| `type="button"` on every option's `<button>` (Softr sometimes wraps things in invisible forms) |
| `e.stopPropagation()` and `e.preventDefault()` in each option's `onClick` |
| If the dropdown lives inside a clickable card, wrap container in `onClick={stop}` and `onMouseDown={stop}` to prevent bubbling |

Apply to: filters, status selectors, person assignments, action menus, context menus.

### 2. `multipleAttachments`: never mix `{id}` and `{url}` in the same array

Updating attachments with a mixed array throws **PATCH 500**.

```js
// Will fail with 500
fields: { fotos: [{id: "attXXX"}, {url: "https://..."}] }

// All items must have the same shape: {url, filename}
fields: { fotos: [
  { url: "https://...orig", filename: "old.jpg" },     // existing, kept
  { url: "https://...new",  filename: "new.jpg" }      // newly uploaded
]}
```

**Pattern for "keep some + add new" photo edit:**

```js
const { uploadAsync, isUploading } = useUpload();

const handleSaveFotos = async () => {
  const uploadedUrls = [];

  if (newFiles.length > 0) {
    const filesToUpload = newFiles.map(f => f.file);
    const results = await uploadAsync(filesToUpload);

    for (const r of results) {
      const isOk = r.status === "completed" || r.status === "success" || (r.url && !r.error);
      let url = r.url || r.URL || r.fileUrl || r.publicUrl;
      const filename = r.file?.name || r.filename || "imagen";

      // If somehow returned as data URI, strip the prefix (Airtable rejects data URIs)
      if (url && url.startsWith("data:")) {
        url = url.replace(/^data:image\/\w+;base64,/, "");
      }

      if (isOk && url) uploadedUrls.push({ url, filename });
    }
  }

  // CRITICAL: existing photos go as {url, filename} TOO — NOT as {id}
  const kept = existingFotos
    .filter(f => !f.marked)                          // ones the user didn't delete
    .map(f => ({ url: f.url, filename: f.filename }));

  // Uniform array
  const finalArr = [...kept, ...uploadedUrls];

  updateRecord.mutate({ recordId, fields: { fotos: finalArr } });
};
```

The `id` of an attachment is for local tracking only. **Never** send it to Airtable in a PATCH.

**`useRecordCreate` with attachments:** in the same payload may fail. **Safer pattern:** create the record first without photos, get the new `recordId`, then do an `update` with the attachments array.

### 3. `multipleRecordLinks`: update format differs from create

```js
// Update — flat array of IDs (strings)
updateRecord.mutate({ recordId, fields: { tecnicos: ["recAAA", "recBBB"] } });

// Common mistake — fails with 422
updateRecord.mutate({ recordId, fields: { tecnicos: [{ id: "recAAA", label: "..." }] } });
```

For **create**, both shapes tend to work, but the flat-IDs form is the canonical and most reliable.

### 4. `singleSelect`: update vs create payload differ

```js
// Update — plain string with the option label
updateRecord.mutate({ recordId, fields: { estado: "Ejecutando" } });

// Create — object with id + label
createRecord.mutate({ estado: { id: "selye8dEaiiuXg4CQ", label: "Ejecutando" } });
```

### 5. The variable name `q` collides with the import

Never declare a local variable `q` inside `useMemo`/handlers — it shadows the imported `q` from `@/lib/datasource` and the next render breaks. Rename to `query`, `term`, `qq`, etc.

```js
// Breaks the next render
const filtered = useMemo(() => {
  const q = search.trim().toLowerCase();   // shadows the import!
  return all.filter(r => getVal(r.fields?.name).includes(q));
}, [all, search]);

// Rename
const filtered = useMemo(() => {
  const query = search.trim().toLowerCase();
  return all.filter(r => getVal(r.fields?.name).includes(query));
}, [all, search]);
```

### 6. Missing `<a` opening tag in generated code

Always verify that every `href="..."` in your output has its matching `<a` open tag. Generation can occasionally drop it, leaving dangling `href="...">` text. **Prefer**:

```jsx
// Option 1 — onClick with window.open (most common)
<div
  onClick={() => url && window.open(url, "_blank", "noopener,noreferrer")}
  className="cursor-pointer ..."
>
  Open document
</div>

// Option 2 — React.createElement (when link semantics matter)
{React.createElement(
  'a',
  { href: url, target: '_blank', rel: 'noopener noreferrer', className: "..." },
  "Link text"
)}
```

### 7. Blank-screen-on-save (silent error)

Common causes, in order of likelihood:

1. **Wrong import path** — missing the `@/lib/datasource` import or trying to import React/hooks from a path that doesn't exist in Softr.
2. **Field name in `q.select()` doesn't match Airtable** — when the alias maps to a non-existent field, Softr returns nothing without an error.
3. **`<style>` block with `@import` of Google Fonts** — Softr sanitizes it and the whole block fails.
4. **Tailwind arbitrary values** like `bg-[#10172A]` may not compile depending on Softr's Tailwind setup. Prefer `style={{ backgroundColor: "#10172A" }}` for hex colors.
5. **`q.eq("id", recordId)` filter** — does not work for record IDs in Softr. Use `useCurrentRecordId()` + `useRecord()`, or filter `allRecords.find(r => r.id === recordId)` in memory.
6. **Components defined inside `Block()`** — causes React error #310.

### 8. Hooks after a conditional return

```js
// React error #310 — number of hooks changes between renders
if (status === "pending") return <Loader/>;
const value = useMemo(...);  // never executes on first render

// All hooks first, returns last
const value = useMemo(...);
if (status === "pending") return <Loader/>;
```

### 9. `Cannot access 'X' before initialization`

Happens when a `useMemo` references another `useMemo` declared **below** it. Both are hoisted but only declared at runtime in order, so the second one is `undefined` when the first runs.

```js
// Fails: pasosTimeline references etapaIndex which is declared below
const pasosTimeline = useMemo(() => [
  { fecha: etapaIndex >= 3 ? f.fechaCulminada : null },
], [f.fechaCulminada]);

const etapaIndex = useMemo(() => /* … */, [etapaTimeline]);

// Move etapaIndex BEFORE pasosTimeline
const etapaIndex = useMemo(() => /* … */, [etapaTimeline]);

const pasosTimeline = useMemo(() => [
  { fecha: etapaIndex >= 3 ? f.fechaCulminada : null },
], [etapaIndex, f.fechaCulminada]);
```

## Source of the Softr block — critical considerations

- Softr **does NOT support `sourceIndex`** — a block can have only one Source active.
- For two blocks on the same page sharing data, use `window.__variable` (see above).
- The Source filters records **before** they reach the code — what doesn't pass the filter, the code **never sees**.
- If you need active and inactive records simultaneously → the Source must NOT filter by Estado.
- Softr's `IS` filter = exact equality; `Contains` is more permissive and captures linked records by value.
- On **detail pages**, use `useCurrentRecordId()` to get the current record ID.

## Diagnosing mutations that "do nothing"

When an Airtable mutation appears silent (UI doesn't update, no visible error), follow this list in order:

| # | Symptom | Likely cause | Verification |
|---|---|---|---|
| 1 | Dropdown opens but doesn't select | `mousedown`/`click` conflict | See "Custom dropdowns" pitfall |
| 2 | `update` runs but nothing changes | `singleSelect` sent as object instead of string | In *update*: `{ campo: "Option" }` (string). In *create*: `{ campo: { id, label } }` (object) |
| 3 | `update` of attachments → 500 | Mixing `{id}` and `{url}` in array | See "multipleAttachments" pitfall |
| 4 | `update` of linked record → 422 | Payload with `{id, label}` objects | In *update*: flat array of strings: `["recAAA", "recBBB"]` |
| 5 | `update` of formula doesn't reflect | Single refetch before recalc | Cascade refetch: `await refetch()` + `setTimeout(refetch, 2000)` + `setTimeout(refetch, 5000)` |
| 6 | `useRecordCreate` fails with linked + attachments | Everything in single payload | Create without attachments → get `recordId` → second `update` with attachments |
| 7 | `update` does nothing, no error log | Field missing from `writeFields` (`q.select`) | Verify the field's alias is in the write select |
| 8 | Mutation is slow and ultimately fails | Circular data in payload | Check you're not sending the whole record object — only fields to modify |

### Logging template for mutation diagnosis

When debugging, temporarily add this to `onSuccess`/`onError`:

```js
const updateRecord = useRecordUpdate({
  fields: writeFields,
  async onSuccess(res) {
    console.log("[Mutation OK]", { recordId, payload, response: res });
    await refetch();
    setTimeout(() => refetch(), 2000);
  },
  onError(err) {
    console.error("[Mutation ERROR]", {
      recordId,
      payload,
      message:   err?.message,
      response:  err?.response,
      data:      err?.response?.data,
    });
  }
});
```

`err.response.data` is the most useful: Airtable explains exactly which field was rejected and why (wrong format, option doesn't exist, value out of range, etc.).

## Forbidden / required summary

| Forbidden | Required |
|---|---|
| Direct `<a href=...>` (Softr's editor sometimes strips the opening tag) | `window.open(url)` on `<div>`/`<button>` |
| `<form>` tags | Plain `onClick` / `onChange` |
| `localStorage` / `sessionStorage` | `useState` |
| Required props without default value | Always provide a default |
| Components defined inside `Block()` | Helpers defined outside `Block()` |
| Hooks after a conditional `return` | All hooks first, returns last |
| Local variable named `q` | Rename to `query`, `term`, etc. |
| Omitting the import from `@/lib/datasource` | Always include it |
| Multiple files | One single `.jsx` file |
| Inventing IDs (`selXXX`, `recXXX`, `tblXXX`) | Ask the user or query Airtable schema first |
| Mixing `{id}`/`{url}` in attachment arrays | All items as `{url, filename}` |
| `mousedown` for outside-click on custom dropdowns | `click` + `setTimeout(0)` |
| External libraries not in the available list | Only the listed stack |

## Visual style — Welldone (OPTIONAL, only on explicit mention)

> **The Welldone visual style is OPTIONAL.** Apply it ONLY when the user explicitly mentions Welldone, "Portal Empresarial Welldone", or the base ID `appAEV0iaC3VfB5Zb`. For any other Softr + Airtable project, use the user's own style preferences and don't impose this palette.

### Client portal (light)
```
Page bg:           #EFF6FF
Card bg:           #ffffff with border #e2e8f0
Card hover:        #f8fafc
Primary text:      #1e293b
Secondary text:    #64748b
Muted text:        #94a3b8
Primary button:    bg #334155 → hover #475569, white text
Secondary button:  bg #f1f5f9 → hover #e2e8f0, text #334155
```

### Internal admin (dark)
```
Page bg:           #10172A
Card bg:           #1a2340 with border #2a3558
Card hover:        #1f2b4d
Primary text:      #f1f5f9
Secondary text:    #94a3b8
Muted text:        #64748b
Inputs:            bg #0f1629, border #334155
```

### Welldone brand (use sparingly, accents only)
```
Welldone orange:   #FF4600
Dark gray:         #333333
```

### Project status colors (badges and bars)
```js
const ESTADO_COLORS = {
  "Preaprobado":          { bg: "#94a3b8", bgLight: "#f1f5f9", text: "#475569" },
  "Permisos Solicitados": { bg: "#94a3b8", bgLight: "#f1f5f9", text: "#475569" },
  "Permisos Aprobados":   { bg: "#60a5fa", bgLight: "#dbeafe", text: "#1d4ed8" },
  "Ejecutando":           { bg: "#2dd4bf", bgLight: "#ccfbf1", text: "#0f766e" },
  "Ejecutado":            { bg: "#14b8a6", bgLight: "#ccfbf1", text: "#0f766e" },
  "A Facturar":           { bg: "#a3e635", bgLight: "#ecfccb", text: "#4d7c0f" },
  "Facturado":            { bg: "#22c55e", bgLight: "#dcfce7", text: "#15803d" },
  "Cerrado":              { bg: "#16a34a", bgLight: "#dcfce7", text: "#15803d" },
};
```

### Welldone portal URLs

```
Client portal:    https://Portalclienteservicio.softr.app
Internal portal:  https://portalwelldone.softr.app
```

Detail pages: `{baseUrl}/{slug}?recordId={recordId}`. Always use the Softr/Airtable internal record ID as `recordId`.

## Pre-delivery checklist

Run through this before declaring a block done:

1. `import ... from "@/lib/datasource"` is present.
2. All hooks come before any conditional return.
3. Helper components are defined outside `Block()`.
4. No local variable shadows `q`.
5. Every `singleSelect` write has the right format for the operation (string in update, object in create).
6. Every `multipleRecordLinks` update sends a flat array of IDs.
7. Every `multipleAttachments` mutation sends a uniform array of `{url, filename}`.
8. Every custom dropdown uses `click` (not `mousedown`) for outside-close, with `setTimeout(0)`, and options have `type="button"` + `e.stopPropagation()` + `e.preventDefault()`.
9. Every `<a` opening tag is present and matches its `href` (or replaced with `window.open`).
10. Auto-pagination is implemented if `count` could be exceeded.
11. Mutations on formula-dependent fields trigger cascading refetches at 0/2s/5s.
12. Source filter requirements (e.g. needs to include inactive records?) are explicit in a code comment so the user knows how to configure the Softr block.
13. No Tailwind arbitrary `[]` for hex colors — use `style={{ }}` instead.
14. No `useMemo` references another `useMemo` declared below it.
15. The file ends with `export default function Block() { ... }`.

## Output format

- Always produce **one single `.jsx` file**.
- Save to disk and call `present_files` so the user can download/copy it.
- For changes to an existing block, edit the file with `str_replace`. Do not regenerate the whole file unless surgical edits would be more error-prone.
- Comments inside the file may be in Spanish or English (match the user's preference).
- Respond in **Spanish** unless the user is using English.

## Reference files

- `references/welldone-airtable-schema.md` — Complete schema for the Portal Empresarial Welldone Airtable base. Tables, field IDs, option IDs, known traps. **Load only when the user mentions Welldone or the base ID `appAEV0iaC3VfB5Zb`.**
