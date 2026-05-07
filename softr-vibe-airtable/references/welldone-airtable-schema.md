# Referencia: Base Welldone (Airtable)

> Esta referencia se usa **únicamente cuando el usuario está construyendo bloques para el Portal Empresarial Welldone**. Si el proyecto es genérico Softr + Airtable de cualquier otro cliente, ignorar este archivo y solicitar al usuario los IDs de tablas, campos y opciones.

**Base ID (Portal Empresarial Welldone):** `appAEV0iaC3VfB5Zb`
**Base ID (Gestión Tareas):** `appKb51aF3l8aB8Fn`
**Base ID (Toma de Requerimientos):** `appk8ZBGkmqabmzyN`
**Nombre:** Portal Empresarial Welldone
**URL portal cliente:** `https://Portalclienteservicio.softr.app`
**URL portal interno:** `https://portalwelldone.softr.app`

## Tabla maestra de tablas

| Tabla | ID | Uso principal |
|---|---|---|
| Proyectos | `tblUFXbeuoNV6zpUe` | Tabla central — proyectos de mantenimiento/construcción |
| Hitos | `tblZm8StwM2D0a6ci` | Hitos de cada proyecto |
| CRM Cotizaciones | `tblCjXRh6pw38qCqH` | Embudo comercial — cotizaciones |
| Planner Cotización | `tblYwSFntPHGR1bk2` | Planner financiero por cotización |
| Clientes | `tbliw7J6IJt03HySc` | Clientes de Welldone |
| Usuarios Portal Clientes | `tblEPiC4g3wlcNEKC` | Usuarios con acceso al portal cliente |
| Reportes Diarios Avance | `tbl9mIQZN0TpyJz4G` | Bitácora diaria por proyecto |
| Reportes Diarios MO | `tblzGwUdaxsJxuQgT` | Reportes de mano de obra |
| Informes Tecnicos | `tblKo7USd6nYQ7eMM` | Informes técnicos generables como PDF |
| Facturas De Venta | `tblgcLtjzVtgnk6gd` | Facturas emitidas a clientes |
| Registros Financieros | `tblgNUkKgxh4FK7rC` | Gastos / facturas de proveedores |
| Registros SIIGO | `tblSZpzD3Mp1JoBof` | Registros importados desde SIIGO |
| Registros DIAN | `tblqcRi1LEwVTG54D` | Registros importados desde DIAN |
| Auditoria Registros Financieros | `tbltQ4UJc5XPR9ZY4` | Comparación entre Financiero/SIIGO/DIAN |
| Cierres Financieros Mensuales | `tblwwygrZkZBq6AJ8` | Cierres mensuales |
| Cierre Periodo | `tblKxcVCCq39p7RZP` | Cierre por periodo |
| Procesamiento Mensual | `tblwP20kHyvlyFZlQ` | Métricas mensuales del negocio |
| Procesamiento MO | `tbloNPW51nDPmDFI9` | Procesamiento mensual de mano de obra |
| Procesamiento Caja Menor | `tblf0UVvxI3dYmZ8R` | Procesamiento de caja menor |
| Caja Menor Movimientos | `tblUmWVDcPlmmElVM` | Movimientos de caja menor |
| Proveedores | `tbl8fCbZLiCQfHdYd` | Proveedores |
| Cuentas & Categorias | `tblXehSKrVecfdMPD` | Plan contable |
| Info Personal | `tbl9ejpKlos8t0q5O` | Personal técnico |
| Registros de Personal | `tblANxYRjEvzi17W7` | Inscripciones de personal nuevo |
| Solicitud Personal | `tblx0wSmOSHzjCjmQ` | Solicitudes RR.HH. |
| Pago de Nomina | `tbl6Ja8LV3qX3piiq` | Pagos mensuales |
| Pagos x persona | `tblxkqpH6Pmu9NZAr` | Pagos consolidados por persona |
| Registro Novedades RRHH | `tblXMapQhUb51dLY6` | Novedades de personal |
| Test Inducción | `tblolBTj4Z3Wj2Nol` | Tests de inducción |
| Cierre de Proyectos | `tblHvsDRdPhxnPxK6` | Cierre y balance final de proyectos |
| Registro de ingreso y salida | `tbl9FPg6QrKRlg8Tg` | Asistencia técnicos |
| CRM Prospectos | `tblEZbRi4YFtSKoat` | Prospectos comerciales |
| Tareas Prospectos | `tbl75s9yOeaAUb40J` | Tareas vinculadas a prospectos |
| Base de Datos Comercial | `tblYNxm8xW1i0OtZq` | Base de datos comercial primaria |
| Gestión Requerimientos | `tblLrgWMRMu3tNnU4` | Toma de requerimientos en visita técnica |
| Toma de requerimientos Sync | `tblz0OgPVbov6JfZu` | Sincronización de requerimientos |
| Leads Pagina Web Welldone | `tblrBNMdn6Z63qS8z` | Leads desde la web |
| Leads Fixodia | `tblvogSfXaXHjHPkJ` | Leads producto Fixodia |
| Base de Archivos | `tblP8gePnUiLXVNBf` | Documentos generales |
| Comisiones Comerciales | `tblVhCvP7b1TWK1vW` | Configuración comisiones |
| Contratos | `tblRSDKdN5qoukSYn` | Contratos de personal |

---

## Proyectos (`tblUFXbeuoNV6zpUe`)

Tabla central. Muchos bloques del portal trabajan con esta tabla.

### Campos principales

| Campo | ID | Tipo | Notas |
|---|---|---|---|
| ID Proyecto | `fldEoGGjXF4hSHx9Y` | singleLineText | Primary |
| Nombre | `fldkTbvdnCiWbrv80` | singleLineText | |
| Clientes | `fld0TxmK4lTE1N8JH` | multipleRecordLinks | → Clientes |
| Portada (from Cliente) | `fldjGWOikKvXqtxwV` | multipleLookupValues | Lookup attachment del cliente |
| Sector Cliente | `fldGpPW8QKH3POt2u` | multipleLookupValues | |
| Sede | `fldKcGWWC8RdPW6D6` | singleSelect | Logika Vía 40, Buró 51, Sede Norte, Gran Plaza del Sol, Malambo |
| Estado | `fldgHQPENGY1YL5Ij` | singleSelect | Ver opciones abajo |
| Estado Facturacion | `fldhhdb574OdzBfCY` | formula | Solo lectura |
| A Facturar | `fldgTIOiTJekJaciI` | checkbox | |
| Tipo de facturación | `fld6ICp9VBExYzvtf` | singleSelect | IVA directo / AIU |
| Sub total | `fldxTweOQnMjklzTg` | currency | |
| Administración | `fldJImv7cPgzUoiZY` | currency | |
| Imprevistos | `fldFup6CjlBGeJoFt` | currency | |
| Utilidades | `fldr6yts9DbHag5Kp` | currency | |
| IVA | `fld0JLFCDfgwEbIrl` | currency | |
| Total valor contratado | `flddyLUcrZ63GJ7aQ` | formula (currency) | Solo lectura |
| Orden de Compra | `fldXCCD6TA63IOTQU` | singleLineText | |
| Factura de venta asociada | `fldqwuJGuHyeFMPmP` | multipleRecordLinks | → Facturas De Venta |
| Fecha_inicio | `fldtovk03nqcIbgAI` | date | |
| Fecha prometida de finalización | `fldxZqDqN88qdFNK0` | date | |
| Fecha Real Inicio | `fldu3p903NSpwt9tA` | rollup | Solo lectura |
| Fecha real finalización | `fldBbevdLdMWj4LfA` | rollup | Solo lectura |
| Responsable | `fldXYvF5Vbjv5DOZF` | singleSelect | Ronald Pedroza, Omar Bolaños |
| Comercial | `fldUIjeSK4mzNLycP` | singleSelect | Edgar Sánchez, Roberto Samper, Ronald Pedroza |
| Creado por | `fldwvpm9Z7g9EpEV5` | singleSelect | Ronald Pedroza, Anonymous, Edgar Sanchez |
| Técnicos Asignados | `fldkDmlaOAUwM06KF` | multipleRecordLinks | → Info Personal |
| CRM Cotizaciones | `fldg07UiudIFPOykL` | multipleRecordLinks | → CRM Cotizaciones |
| Hitos | `fld7rXtmyj9eO3Vg8` | multipleRecordLinks | → Hitos |
| Reportes diarios de avance | `fldlfCWEussGKczPa` | multipleRecordLinks | → Reportes Diarios Avance |
| Reportes diarios MO | `fldpNQuZKa3GbxxlG` | multipleRecordLinks | → Reportes Diarios MO |
| Registros Financieros | `fldfZSqIsMvv7zq5E` | multipleRecordLinks | → Registros Financieros |
| Informes Tecnicos | `fldPuPhMGfO5PqEp5` | multipleRecordLinks | → Informes Tecnicos |
| Avance del proyecto | `fldvkgtzauCYwJl9F` | formula (percent) | Solo lectura |
| Avance general manual | `fldWo5RxP4wLZzave` | percent | Editable |
| Avance general automático | `fldU7EPgT8ZTkBIJT` | formula (percent) | Solo lectura |
| Gestión del avance | `fldyF1wsrVuI7W7ZT` | singleSelect | Automático / Manual |
| Cantidad de Ítems | `fldmhsaHdgMrg2oGb` | number | |
| ID Record | `fldHL9qYfY7DRpxiv` | formula | |

### Ítems del proyecto (1–6)

Los proyectos tienen 6 slots de ítems. El nombre del campo varía con número.

| Campo (slot N) | Patrón | Tipo | Editable |
|---|---|---|---|
| Descripción Ítem N | `Descripción Ítem 1`…`Descripción Ítem 6` | multilineText | ✅ |
| Ítem N Cantidad Contratada | `Ítem 1 Cantidad Contratada`… | number | ✅ |
| % Impacto Ítem N | `% Impacto Ítem 1`… | percent | ✅ |
| Ítem N Cantidad Ejecutada | `Ítem 1 Cantidad Ejecutada`… | rollup | ❌ |
| Ítem N % de avance | `Ítem 1 % de avance`… | formula | ❌ |
| Ítem N Registro Fotográfico | `Ítem 1 Registro Fotográfico (from Reportes diarios de avance)`… | multipleLookupValues | ❌ |

> ⚠️ **Trampa conocida**: el ítem 3 del registro fotográfico se llama literalmente `Item 3 Registro Fotográfico (from Reportes diarios de avance)` — sin tilde en "Item". Los demás sí llevan tilde.

### Etapas Timeline (booleanos por etapa)

| Etapa | Campo checkbox | Campo fecha |
|---|---|---|
| Afiliaciones | `fldUJW6MFYla2aaNT` | `fld3R3JthwxqJkF2b` |
| Compras | `fldQ38KV25PoaafG9` | `fldChcqbObVP8qBId` |
| Herramientas y EPP | `fldy9LOPPAORQw2Qr` | `fldkXubsZNfIrd381` |
| Guia de Ejecucion | `fldn56xz09iPdbJXa` | `fldHldw3wE2VIfMkw` |
| Entrega | `fldL1jkzcUoavje88` | `fldpWmSlIgPNeJ0OM` |

`Etapa Timeline Técnico` (`fldTMALF0TVDJh365`) y `Etapa Timeline` (`fldmhkvuGNAQT2YU3`) son fórmulas calculadas a partir de los checkboxes.

### Documentos del proyecto

| Documento | Campo | Tipo |
|---|---|---|
| Informe Técnico (URL Builder) | `fldgvVjHLp9Nc6Y44` | url |
| Informe Técnico PDF | `fldNIf40oKA4xhZcU` | multipleAttachments |
| URL Informe Técnico PDF | `fldhRHsgEwnfGTfIh` | url |
| Acta Inicio | `fldxgb1GLj1CQLxm6` | url |
| Acta Inicio PDF | `fld1sK7ttbfMeXitQ` | url |
| Acta Finalización | `fldcXIUAblWhviOFe` | url |
| Acta Finalización PDF | `fldyZqK9aAopKMpjE` | url |
| Cierre | `fld5At3w35RNB7Wsa` | url |
| Ejecución (URL) | `fldGVq5HZAuZ0UewQ` | url |
| Ejecución Documento | `fldyrYMZ3tUPxgIMA` | multipleAttachments |
| Orden de compra Adjunto | `fld6N7AqL6x25QOjr` | multipleAttachments |

Lookups desde CRM Cotizaciones (solo lectura):
- `Propuesta Google Slides` (`fldnxGnwTYOQqAGa3`)
- `Propuesta PDF` (`fldvoHyir57BKFVNu`)
- `Planner en Sheets (from CRM Cotizacionez)` (`fldpvZDU5ewbp2FJP`)
- `Propuesta en Canva  (from CRM Cotizacionez)` (`fldgM0ScS0Bfu3Fyt`) — ⚠️ doble espacio
- `Garantías (from CRM Cotizacionez)` (`fldT3St5cSyOprT9B`)
- `Borrador en Canva (from CRM Cotizacionez)` (`fldCWYiLGSPG0B7EQ`)
- `Carpeta del proyecto (from CRM Cotizacionez)` (`fldxHOBJo1Cdn89Yp`)
- `Archivos relacionados (from CRM Cotizacionez)` (`fldkaATKnUJisBPkP`)
- `Código de propuesta (from CRM Cotizacionez)` (`fldAa0LXyB8L5f7hi`)

### Opciones del campo `Estado`

| Opción | ID | Color |
|---|---|---|
| Preaprobado | `selZEfAsld6d3jxmz` | gray |
| Permisos Solicitados | `sel6BVjm4MhNxfYDX` | grayLight |
| Permisos Aprobados | `seliLKAk7XvOxuvn7` | blueLight |
| Ejecutando | `selye8dEaiiuXg4CQ` | tealLight |
| Ejecutado | `selGmUbJJMLTMvBpa` | tealLight1 |
| Cerrado | `selurXnFfp1mWG2Kp` | greenBright |

> ⚠️ Las opciones **"A Facturar"** y **"Facturado"** fueron eliminadas — usar `Estado Facturacion` (formula) si se necesita ese estado.

### Opciones del campo `Sede`

| Opción | ID |
|---|---|
| Logika Vía 40 | `selfzQDS7ba6BG8uF` |
| Buró 51 | `selEIZC5mT28yvOOQ` |
| Sede Norte | `sel4X9I1Z3BQWpnw6` |
| Gran Plaza del Sol | `selrZgI2p9xZs8bzv` |
| Malambo | `selGgCDaiRoGMbWXc` |

### Opciones de `Responsable`

| Opción | ID |
|---|---|
| Ronald Pedroza | `sel4LOtFgToOnFeOn` |
| Omar Bolaños | `selMCzd8Pbc1VhrUT` |

### Opciones de `Comercial`

| Opción | ID |
|---|---|
| Edgar Sánchez | `selqcMlBl7L8K2Utq` |
| Roberto Samper | `selBoJBo0ybd1jNPO` |
| Ronald Pedroza | `sel9RZwoLL4IZZeM4` |

### Opciones de `Tipo de facturación`

| Opción | ID |
|---|---|
| IVA directo | `selZO5fyftvlWFOwu` |
| AIU | `selu22kZC7gFIsp4h` |

### Opciones de `Gestión del avance`

| Opción | ID |
|---|---|
| Automático | `sel0rFIWZYbYjuKfw` |
| Manual | `selksSkSM7U7NzoYw` |

---

## Hitos (`tblZm8StwM2D0a6ci`)

| Campo | ID | Tipo |
|---|---|---|
| ID | `fldy32MNJ6DubxBsi` | formula (primary) |
| Proyectos | `fldVGZp9srBlMuFXU` | multipleRecordLinks |
| Hito | `fldvctOGt5NtE8dWp` | singleLineText |
| Descripcion | `fldHRQUprJiyG6dwI` | multilineText |
| Inicio | `fldauX5oWeYhS3MKZ` | dateTime |
| Terminacion | `flde7znH2UWX5L6eC` | dateTime |
| % Porcentaje | `fldggbQYLPNQTEwn1` | percent |
| Duracion | `fldh2QVIvk63fkWK1` | number |
| ID Numero | `fldrpu3ZSxtlFVlat` | formula |
| Orden | `fld83hI7Mz41ZFMgX` | number — usar para reordenamiento decimal |
| ID Numero Automatico | `fldBptK6oXxVuCgr5` | autoNumber |

---

## CRM Cotizaciones (`tblCjXRh6pw38qCqH`)

| Campo | ID | Tipo |
|---|---|---|
| Nombre | `fldWvgYzCMISIlwnS` | multilineText (primary) |
| Código de propuesta | `fldJLkL7j0kXWZO10` | singleLineText |
| Linea Negocio | `flduggEGHy5jWYHnk` | singleSelect |
| Valor estimado | `fld1EZSKkbGvDQ5ht` | currency |
| Clientes | `fld1AMy4yr8eg5Xam` | multipleRecordLinks |
| Sede del Cliente | `fldejQKq0LZCEBtNB` | multipleSelects |
| ID Proyecto | `fldBLAs7poBsk3Cbq` | multipleRecordLinks |
| Estado | `fldwq8hOOzlD0IVVM` | singleSelect |
| Prioridad | `fldmRJFYvQzl3lfUq` | singleSelect |
| Asesor Comercial | `fldXBP7vg06yag7ej` | singleSelect |
| Tipo de Facturación | `fldiUrN994gBCc72O` | singleSelect |
| Tipo Propuesta Requerida | `fldo0WbobpTDM3sB1` | singleSelect |
| Fecha Toma Requerimiento | `fldH7M90sJeYarzcA` | date |
| Fecha Limite | `fldQhiecYmRYDSdPm` | date |
| Fecha de creación | `fldJz7NKtkcVvwIOc` | createdTime |
| Contacto | `fldlUDdi7e9IjSt0a` | singleLineText |
| Correo electrónico | `fldOOTVXS7OFvdnVM` | email |
| Teléfono | `fldBWnT8L8sjMECv2` | phoneNumber |
| Borrador en Canva | `fld0jRmYzirpWuKdH` | url |
| Carpeta del proyecto | `fldBVgUGuGhOQfP98` | url |
| Garantías | `fldY7Tv4YpUCm6Z10` | url |
| Planner Cotización | `fldBHkZHgxAR3VDCn` | multipleRecordLinks |
| Planner en Sheets | `fldZwOfww83q6zoIo` | url |
| Propuesta en Canva | `fldIK6UxcaEOBYt9f` | url |
| Propuesta Google Slides | `fldecgUjwVVA8M3Dl` | url |
| Propuesta PDF | `fldWaQTPm9XVFO0ar` | url |
| Notas | `fldZ8guTbDxRhe4YX` | richText |
| Requerimientos | `fld61AjFAQeAGYCr5` | multipleRecordLinks |
| Record ID | `fldN8AhHOVmHoyG38` | formula |

### Opciones de `Estado`

| Opción | ID |
|---|---|
| Potencial | `selMF0mdRJz6BchZS` |
| Procesando | `sel1anWhwRk0a6cQV` |
| Validación | `selQZnuu70JR2lqUP` |
| Lista para enviar | `selxzUf1INMe6Y1Ac` |
| Negociación | `selfwmprbqx45ct8r` |
| Cerrado | `selQaHBQCUDFBUdve` |
| Stand by | `selBHyBrI38WHqIDm` |
| Perdido | `selspltXQROn0kds1` |

### Opciones de `Prioridad`

| Opción | ID |
|---|---|
| Alta | `selh7q5adxNLuKvpL` |
| Media | `selCwyQWo2PAcQ21w` |
| Baja | `selQg4ND1P4rgziFi` |

### Opciones de `Asesor Comercial`

| Opción | ID |
|---|---|
| Roberto Samper | `selRnlsJNOtAAsLWI` |
| Edgar Sánchez | `selD0otwyKb3a9ktJ` |
| Ronald Pedroza | `selWasRNraKcr3Cch` |

### Opciones de `Linea Negocio`

| Opción | ID |
|---|---|
| Proyectos | `selBoXF8UjDwKJiKu` |
| Fixodia | `selhQJx0WoupWOTky` |
| Fixora | `selHN8MSBYhhu7HvY` |

### Opciones de `Tipo de Facturación`

| Opción | ID |
|---|---|
| IVA directo | `selRIm34zi9tzXAx3` |
| AIU | `sel03d4mhV1WC5YEa` |

### Opciones de `Tipo Propuesta Requerida`

| Opción | ID |
|---|---|
| Completa | `selZ3iLQpjYNRJzyP` |
| Simple | `seldCVZjmNCeSPKwp` |
| Suministros | `selBBqtCuvDu1nosp` |

---

## Clientes (`tbliw7J6IJt03HySc`)

| Campo | ID | Tipo |
|---|---|---|
| Nombre | `fldbeXz6ZkhKW4ifi` | singleLineText (primary) |
| Tipo AIU | `fldoHW9Qwd0aaOjMg` | singleSelect |
| NIT | `fldsl4svSyM1UmJW7` | singleLineText |
| Dígito de verificación | `fldOeMtTbcGJmcxYX` | number |
| Tipo De Cliente | `fld0lyHEKVMQ1Gswq` | singleSelect |
| Regimen Tributario | `fldHrdAEOfD2wPai4` | singleSelect |
| Sector | `fldke0SDwnX6u8jqb` | singleSelect |
| Portada | `fld3O6AITVrHL1YqU` | multipleAttachments |
| Dirección | `fldMYZFt78cDbG5YD` | singleLineText |
| Sedes | `fldlR5XDIsepDeEg5` | multipleSelects |
| Contacto | `fldIB2ahgHMLzpGzB` | singleLineText |
| Email | `fldyxl04XdErVcqfv` | email |
| Teléfono | `fldLjkpuE33AAnC3F` | phoneNumber |
| RUT | `fldTHlffK9a5UAjLw` | multipleAttachments |
| Base rete ICA | `fld903op4V7wl3cfN` | singleSelect |
| Base rete fuente | `fld7uZcviUWkZaSuf` | singleSelect |
| Comisiones Roberto Samper | `fldClEkkYfRTRCZya` | percent |
| % Comisiones Edgar Sánchez | `fldWcq6kUcJVMNCVJ` | percent |
| Proyectos | `fldUYozvweDvKGP3a` | multipleRecordLinks |
| CRM Cotizaciones | `fldCqdDsVRvYrp3wY` | multipleRecordLinks |
| Facturas de venta | `fld3J6aNp57z9E6SP` | multipleRecordLinks |
| Informes Tecnicos | `fldPeTpX0xQJyitzZ` | multipleRecordLinks |
| Usuarios Portal Clientes | `fldwTIFa9lc2Ly1FM` | multipleRecordLinks |
| Fecha de Creación | `fld7GeoSH2lZ6bqFY` | createdTime |

---

## Reportes Diarios Avance (`tbl9mIQZN0TpyJz4G`)

| Campo | ID | Tipo |
|---|---|---|
| Fecha | `fldUCvkGy4B8xnbnk` | date (primary) |
| Mes | `fldXUegNJmN88MeVc` | formula |
| Quien reporta | `fldqJCzQ6q5J7zWp2` | singleSelect |
| Proyectos | `fldxEl8gunBznBxLO` | multipleRecordLinks |
| Hay alguna novedad de SST? | `fldmpUkp1dbRSdqA6` | singleSelect |
| Hay alguna novedad crítica | `fldQovWCXjaVPEskY` | singleSelect |
| Observaciones generales | `fldXonANdmILC1Azc` | multilineText |
| Ítems Trabajados | `fldmDLGOuQ8yP64ha` | multipleSelects |

### Por cada ítem trabajado (1–6)

| Slot | Avance del día | Observaciones | Registro Fotográfico |
|---|---|---|---|
| 1 | `fldDWUFnOwWMnA69P` | `fldGgyWwfG6OXySyx` | `fldbtlLbvOrSVbTcP` |
| 2 | `fldy9uP9BasRq1OXN` | `fldFUk05P09nO1Ubf` | `fldHCtQmRtMCJ0P7z` |
| 3 | `fldXUUGwr53YWmavQ` | `fldRhbiPyC1yKvA2d` | `fld2qzHClhlBrldry` |
| 4 | `fldayroQHRQpsnbPa` | `fldIq4JfwuTC7Ng7u` | `fldmxEsfCCJwuPgMd` |
| 5 | `fldsyC8TZlAJAn7DD` | `fldqiVDdiI1IUNx36` | `fld1fTm8I1i2eSukf` |
| 6 | `flda14XlC1ky95NK3` | `fldElTGgdGSOJ9s1n` | `fldqb7cPB6ktx6inF` |

Tipos: avance del día = `number`, observaciones = `multilineText`, registro fotográfico = `multipleAttachments`.

### Opciones de `Quien reporta`

| Opción | ID |
|---|---|
| Omar Bolaño | `sel1DrqfYIxUJ1mQ8` |
| Ronald Pedroza | `selgTzOI1RItdJALe` |
| Jose Hernandez | `selhzo7Rf3aAVjzHX` |
| Jeison Vallejo | `selK2tADmSDYJOOBe` |
| Breiner Hernandez | `selKGJeyt9amjjC9q` |

### Opciones de `Hay alguna novedad de SST?`

| Opción | ID |
|---|---|
| No | `selMSLTgdRv4YO4NO` |
| Si | `sel8IEl56niPm2v2O` |

### Opciones de `Hay alguna novedad crítica`

| Opción | ID |
|---|---|
| No | `selP2MkaLCcWlAX0W` |
| Si | `selWMa04ddPPRWR6i` |

### Opciones de `Ítems Trabajados`

| Opción | ID |
|---|---|
| Ítem 1 | `selqfc5evAjhOBiq2` |
| Ítem 2 | `sel9VsLYuYI5JINpM` |
| Ítem 3 | `selPdQs6wI2c4bsDG` |
| Ítem 4 | `sel3zewb1zffHQdyD` |
| Ítem 5 | `selr9UK0j0H50hR0t` |
| Ítem 6 | `selIEa9PM7DLPKQwT` |

---

## Facturas De Venta (`tblgcLtjzVtgnk6gd`)

| Campo | ID | Tipo |
|---|---|---|
| Número de factura | `fldjEVFHdshm3kZeq` | singleLineText (primary) |
| Clientes | `fld54HDKn9jIn1GQ0` | multipleRecordLinks |
| Concepto general | `fldd6AYGObpzv40io` | multilineText |
| Adjuntar Factura | `fldbEcxwwIEiJ3BiF` | multipleAttachments |
| Proyectos | `fldDthSPpTmid0ON0` | multipleRecordLinks |
| Fecha de emisión | `fldybf4TWFiTfEcnT` | date |
| Subtotal | `fld0Hz5depogGizjk` | currency |
| Total | `fldemBhxNvIAz7kmu` | formula (currency) |
| Estado | `flduX9nFbdXn569bl` | singleSelect |
| Cartera | `flddoK5s1VcssTrRx` | formula → "Pagada" / "Vencida" / "Pendiente de Pago" |
| Valor pagado | `fldwIoR8Q25jJpcwd` | currency |
| Fecha vencimiento | `flddvAcVQmp41VSqQ` | formula |
| Días vencida | `fldWowhFM0NxXv6OS` | formula |
| Tipo de documento | `fld7ZLd49KEWVoIyh` | singleSelect |
| AIU | `fldSqVSC7JHUWTJQw` | singleSelect |
| % Administración | `fldi2fxzfLAFPzjHz` | percent |
| % Imprevistos | `fldjJCaHWpUfeWT5p` | percent |
| % Utilidades | `fldVAR6wzPB0qreP7` | percent |
| Notas | `fld9OkRqRJwEO8lBm` | multilineText |

### Notas importantes

- El campo `Cartera` es **formula** que devuelve un singleSelect virtual con texto: `"Pagada"`, `"Vencida"` o `"Pendiente de Pago"`. Tratarlo como string, no como número.

---

## Registros Financieros (`tblgNUkKgxh4FK7rC`)

| Campo | ID | Tipo |
|---|---|---|
| ID | `fldmpOL8QgSRPtZ1n` | autoNumber (primary) |
| Descripción | `fldlcV4kVInYjYSGC` | multilineText |
| Proveedor | `fldGVWDSNnbCvQDpK` | multipleRecordLinks |
| Tipo de documento | `fldoa5pYFcqEl9W3J` | singleSelect |
| Número de documento | `fldUOlgvj8evbyWNB` | singleLineText |
| Comprobante SIIGO | `fldgjo0CF1RenUbIX` | singleLineText |
| Fecha documento | `fld1iDd4ji3YP6BUT` | date |
| Subcuenta | `fldyT4Pqx4ALlxqaf` | multipleRecordLinks |
| Tipo de registro | `fldBrdUQ8iLUPVOmV` | singleSelect |
| Proyectos | `fld5h6WEgoLOgMupZ` | multipleRecordLinks |
| Medio de pago | `fldYZr5AtZgPrz0pe` | singleSelect |
| Adjuntar Factura | `fldCgAUVeZXaQUJMr` | multipleAttachments |
| Subtotal | `fldcXdpkaFBVuLYYA` | currency |
| AIU | `fldGEx6dv7YkkAhvO` | currency |
| IVA | `fldtP4vppHyzULeGw` | currency |
| Total | `flda1zLSkhJpiec3z` | formula |
| % Rete fuente | `fldQxLotnaGUshW79` | percent |
| % Rete ICA | `fldteSHWW9mtgaUF8` | percent |
| Valor pagado | `fld3nhIPP6lWyK1Qj` | formula |
| Estado del registro | `fldtuAm2DRjVgciOw` | formula |
| Plazo de pago | `fldP7wS54ofNL4vtk` | number |
| Estado credito | `fld7v36gDq1lnjpHS` | singleSelect |
| Días vencida | `fld7mqAfe2rf9R3qF` | formula |
| Fecha de pago | `fldzWSOzmHtntOpvr` | date |

---

## Informes Tecnicos (`tblKo7USd6nYQ7eMM`)

| Campo | ID | Tipo |
|---|---|---|
| ID Informe | `fldPQZtjxVi18zyQ8` | formula (primary) |
| Estado | `fldMYpVEHF4RF47VQ` | singleSelect |
| Última modificación | `fldSrTpc1c1MoN58b` | lastModifiedTime |
| Objetivo del servicio | `fldyOFH1Q1w6pqGGz` | richText |
| Alcance técnico | `fldfrUm1Py5YhhoB6` | richText |
| Desarrollo de la ejecución | `fldHKgcVpgQ9AXjqZ` | richText |
| Recomendaciones | `fldSghwRARs9KaMn8` | richText |
| Conclusión técnica | `flduDHfLGta0FIDdD` | richText |
| Informe URL | `fldqf6gBLuQzHgBu2` | url |
| Proyecto | `fldGQgSuj5Lddb0dF` | multipleRecordLinks |
| Clientes | `fldhS8fVNZmi8EkKO` | multipleRecordLinks |
| Tipo de activo | `fldd1UPZQkqW6JqE4` | singleSelect |
| Fecha del Informe | `fldhPp6SAy2WFRya8` | date |
| Cotización PDF | `fldyYX8jyt3c8RceO` | multipleAttachments |
| Firma | `fldnojHMiuk5dGHV5` | multipleAttachments |
| Fotos Listas | `fldVtGyMXx2B8uZcB` | checkbox |
| Generar Informe Doc | `fldR9QrTfxjRGVoPG` | checkbox |
| ID Record | `fldeGZg1L65M7aA2A` | formula |

### Por cada ítem (1–6) — fotos

| Slot | Campo |
|---|---|
| 1 | `fldLOvA9cQEZbgCAo` |
| 2 | `fldcs6VbjgmmU6pIN` |
| 3 | `flddo21iCPG4bzHsK` |
| 4 | `fldKz4UaNCGYvTmZZ` |
| 5 | `fldq7Ba5EXka0YT6c` |
| 6 | `fldYheZi5RuApmNnm` |

---

## Info Personal (`tbl9ejpKlos8t0q5O`)

Personal técnico de Welldone. Usado para asignar técnicos a proyectos.

| Campo | ID | Tipo |
|---|---|---|
| Nombre | `fld8ntT3fyKFhOLwa` | singleLineText (primary) |
| Foto Perfil | `fldOyF0VyLpRqfwyA` | multipleAttachments |
| Cédula | `fldBT11KQbzZPieY7` | singleLineText |
| Correo | `fldVt3eb4NlS9RMsb` | email |
| Correo Softr | `fldSWJrnszl6GlAVE` | email |
| Celular | `fld2LEwiTxpSFiSce` | phoneNumber |
| Estado | `fldCemCK8f2iJEqUl` | singleSelect |
| Área | `fldd3o0pq4oUeBQCf` | multipleSelects |
| Cargo | `fldcqrIazwMCcbLKx` | singleSelect |
| Tipo de Contrato | `fldfPNZHEZFsO6NyE` | singleSelect |
| Tipo de Vinculacion | `fldatFkQIgP6OflB8` | singleSelect |
| Valor x día | `fldUQN1JxnyviDlQL` | currency |
| Fecha de Ingreso | `fldxY69PoD8qNYo91` | date |
| Fecha de Retiro | `flddOHl9tP3tCiU2c` | date |
| Proyectos | `fldgS8BpG2Ok1wVHG` | multipleRecordLinks |
| Reportes Diarios MO | `fldWhURdPRLKJteus` | multipleRecordLinks |

---

## Reportes Diarios MO (`tblzGwUdaxsJxuQgT`)

| Campo | ID | Tipo |
|---|---|---|
| ID Registro | `fldgL8waHoozogIGp` | autoNumber |
| Fecha laborada | `flduME8uNmKiw73gw` | date |
| Persona | `fldqtsvNgJGVvEOjl` | multipleRecordLinks |
| Proyectos | `fldnJwk0kTYPkOLVZ` | multipleRecordLinks |
| % Dedicación | `fldRvEJbX5d0XVHXG` | percent |
| Valor registros | `fldgcNH24zOSfjC7n` | formula |
| Jornada | `fldMNC58F8Xgl6uZ9` | singleSelect |
| Tipo día | `fldvR8svEgCVWNBID` | singleSelect |
| Observaciones | `fldci7kUOTmioj76C` | multilineText |

---

## Usuarios Portal Clientes (`tblEPiC4g3wlcNEKC`)

| Campo | ID | Tipo |
|---|---|---|
| Nombre | `fldYFUnRx6v0xT7xP` | singleLineText (primary) |
| Correo | `fldykobrLOpDovRXw` | email |
| Cliente | `fld2BsLKxGza8xDrI` | multipleRecordLinks |
| Rol | `fldoXhX7E35rh5VSZ` | singleSelect |
| Estado | `fldQzHJqqwlvHWwek` | singleSelect |

---

## Planner Cotización (`tblYwSFntPHGR1bk2`)

Planner financiero detallado de cada cotización (AIU, totales, márgenes).

| Campo | ID | Tipo |
|---|---|---|
| ID Cotizacion | `fldHyesuzrNcVZgi6` | multilineText (primary) |
| Estado Planner | `fldK6m2X0fslUqVkH` | singleSelect |
| Vinculación Cotización Real | `fldomxbRyNEoz0ZMz` | multipleRecordLinks |
| Cotización | `fldenZVj6bhpiwXCu` | singleLineText |
| Portada | `fldvlUrlRnOL5uAOD` | multipleAttachments |
| Cliente | `fldipWKmQ8d95XBhD` | singleLineText |
| ID Proyecto | `fldaDqYQoxnK4BaSO` | singleLineText |
| Subtotal | `fldP35NLjLB6XcRW2` | currency |
| % Administración | `fldykdkOLgqbOK14H` | percent |
| Administración Total | `fldmiGJI4x9F3SorE` | currency |
| % Imprevistos | `fldZdb4il65z6LlyZ` | percent |
| Imprevistos Total | `fld0RUCOQSTXrLxjQ` | currency |
| % Utilidades | `fld0J2HMAs2VSVeeN` | percent |
| Utilidades Total | `fldRS4ZMNkc7bAQR2` | currency |
| Total AIU | `fldO3mGrKk2XzSfrL` | currency |
| IVA 19% | `fld7N2G68RxDGIYEI` | currency |
| Total IVA | `fldl2s9DW3QpDMj0e` | currency |
| Valor a facturar + IVA | `fldtSiUaNdKiRGtaK` | currency |
| Total Valor Real | `fldtxjMu8j029LqPF` | currency |

---

## Cierre de Proyectos (`tblHvsDRdPhxnPxK6`)

| Campo | ID | Tipo |
|---|---|---|
| ID | `fldlLa9o6yqM1QuLy` | autoNumber |
| Proyecto | `fldxrEBi4ugm6wppd` | multipleRecordLinks |
| Estado de Revisión | `fldf3pdB6UJYJA9Qy` | formula |
| Cierre Rpedroza | `fld8IGnGUXUMwXf0B` | checkbox |
| Cierre Gerencia | `fld2MOGzE0IQcCMKH` | checkbox |
| Presupuesto Planeado | `flduPNJuGpvjs1kEN` | currency |
| Balance Costos | `fldb29nAtBUjdjrWt` | formula |
| Resultado del Presupuesto | `fldYeRcHJI5GqVR31` | formula |
| Balance Presupuestado | `fldnGzS0GOCUPP48Y` | currency |
| % Costos | `fld3BH3WWNsy3Zyyi` | formula |
| % Utilidad Bruta Actual | `fldcLW4Qu27sPzteK` | formula |

---

## URLs del portal Welldone

```
Portal cliente:  https://Portalclienteservicio.softr.app
Portal interno:  https://portalwelldone.softr.app
```

Páginas de detalle siguen el patrón: `{baseUrl}/{slug}?recordId={recordId}`

Páginas conocidas del portal cliente:
- `/proyecto-detalle?recordId={recordId}`
- `/proyecto-timeline?recordId={recordId}`

Páginas conocidas del portal interno:
- `/detalle-proyecto-completo?recordId={recordId}` — con tabs por hash: `#detalle`, `#timeline`, `#financiero`, `#bitacora`, `#tareas`

---

---

# Base Gestión Tareas (`appKb51aF3l8aB8Fn`)

Esta base es independiente de la base principal (Portal Empresarial Welldone). Contiene el sistema de tareas internas y solicitudes del portal de clientes/empleados. Tiene su propio conjunto de tablas auxiliares (`BD empleados`, `Proyecto`, `Cotizaciones`, `CRM Prospecto`, `Proyectos de tecnología`, `Hitos`, `Usuarios Portal Clientes`) que son versiones sincronizadas de las tablas de la base principal.

## Tablas principales de Gestión Tareas

| Tabla | ID |
|---|---|
| Solicitudes | `tblLE1ydloydn7rlT` |
| Gestión Tareas | `tbllgJ2HPb2fYEX1n` |
| BD empleados | `tbls0LijWIY4q1hyz` |
| Proyecto (sync) | `tblaZPV6OfCk4knts` |
| Cotizaciones (sync) | `tblkxVqfSGEDGVSit` |
| CRM Prospecto (sync) | `tblVD3zwT0KEs7Xbp` |
| Proyectos de tecnología | `tblFmFxH5qkH1TOaG` |
| Hitos (sync) | `tblBOLYCx4BvNQl9M` |
| Usuarios Portal Clientes (sync) | `tblcqQfyFMTXU9ToV` |

---

## Solicitudes (`tblLE1ydloydn7rlT`)

Tabla de solicitudes enviadas por clientes o internamente. Vinculada a tareas de ejecución.

| Campo | ID | Tipo |
|---|---|---|
| ID | `fldBtRZELHeNImO2M` | formula (primary) |
| Qué Solicita? | `fldTr5iwqMX5g0Dti` | multilineText |
| Nombre Solicitante | `fldG6mcNzyXlVEaiE` | multipleRecordLinks → BD empleados |
| Correo | `fldOvp6bcR7W94upp` | multipleLookupValues |
| Ubicación | `fldwkoYtKwGJ26UXW` | singleLineText |
| Justificación | `fldXBBfSAitq5DSaR` | singleLineText |
| Categoría | `fldsBbJHy3Hb76PNJ` | singleSelect |
| Prioridad de Solicitud | `fldsGGy8unqgcXQCO` | singleSelect |
| Imagen | `fldVLW7MqixHKjqUK` | multipleAttachments |
| Estado | `fldvHye9a61clRpej` | singleSelect |
| Mensaje Evaluación | `fldOHJSno4RX6AQQm` | richText |
| Prioridad | `fldYGZDJQJhYARQjy` | singleSelect |
| Tarea Vinculada | `fldOtgkI74WBJfAAq` | multipleRecordLinks → Gestión Tareas |
| Descripción de la Tarea a Ejecutar | `fldHQMZtHU4rSxGql` | richText |
| Creado Por | `fldR90mOrqkTuTfl7` | multipleRecordLinks → BD empleados |
| Fecha de Entrega | `fldrCJ39doOl5ZEzM` | dateTime |
| Responsable | `fldCn1EdBPDlt1reV` | multipleRecordLinks → BD empleados |
| Asignado a | `fldwduXQLT1zXNijP` | multipleRecordLinks → BD empleados |
| Fecha Solicitud | `flderUXDeVQWLsPqU` | createdTime |
| Días Vigencia | `fldujcHzBFPzNq4FM` | formula |
| Numero ID | `flduoFymiR6qNHSOY` | autoNumber |
| Validación Final | `fldHcURtpsewzZXOX` | checkbox |
| Notas de Terminación | `fldf0YgfnxPqlySVg` | multilineText |
| Validación Final Cliente | `fldfbOoJohKrOtC46` | singleSelect |
| Notas de Terminación Cliente | `fldO8UF6ZXrRatpog` | multilineText |
| Tipo de Cliente | `fld0bpblG9F8Wmz6P` | singleSelect |
| Usuarios Portal Clientes | `fldCGzPN8wuUWcnja` | multipleRecordLinks → Usuarios Portal Clientes |
| Proyecto | `fld30tLNMteBdCgxc` | multipleRecordLinks → Proyecto (sync) |

### Opciones de `Categoría`

| Opción | ID |
|---|---|
| Tecnología | `sel099HRnPHTSq0ps` |
| Visita Comercial | `sel6zW7hg2cRSNudH` |
| Toma Requerimiento | `selbGGpLQrT9B2h2R` |
| Postventa | `selkTTho7teXu8IZm` |
| Otros | `sel5jdxGlgKuNqeo1` |
| Garantía | `selRkSsYQH4Lm5BJC` |

### Opciones de `Prioridad de Solicitud`

| Opción | ID |
|---|---|
| Alta | `sel4uEeafrP2zwi1c` |
| Media | `selVqHKfs2bBmjagj` |
| Baja | `selSJWhCuXSAhzk7b` |

### Opciones de `Estado`

| Opción | ID |
|---|---|
| Por Aprobar | `selMRJmXcmqfsG1R2` |
| Aprobada | `selofZtso0rPNk4ai` |
| En Ejecución | `selehqXZ6cjEaYFlf` |
| Por Validar | `selx1N4iFhBo90cHn` |
| Completada | `selxd1roTiFy6iXUi` |
| Descartada | `sel2VPucNTLlQgGwW` |

### Opciones de `Prioridad` (campo de ejecución interna, diferente a "Prioridad de Solicitud")

| Opción | ID |
|---|---|
| Baja | `selkLRobt67UmB5Ia` |
| Media | `sel7ydKOl8HSDVcHL` |
| Alta | `selqsfTPisalNktG7` |

### Opciones de `Validación Final Cliente`

| Opción | ID |
|---|---|
| Aprobado | `sel6FDmgHzxbcimig` |
| Desaprobado | `seleP29CQucSnuOLl` |

### Opciones de `Tipo de Cliente`

| Opción | ID |
|---|---|
| Interno | `selvb7l1Hh2HGd7ro` |
| Externo | `selzagjooOuirB252` |

---

## Gestión Tareas (`tbllgJ2HPb2fYEX1n`)

Tabla principal de tareas internas de la empresa (comercial, tecnología, proyectos, SST, etc.). Vinculada a solicitudes, proyectos, cotizaciones y prospectos.

| Campo | ID | Tipo |
|---|---|---|
| Tarea | `fldAVPGA0lEgNsGh3` | multilineText (primary) |
| Asignado a | `flduiSC1iGHHfYH6W` | multipleRecordLinks → BD empleados |
| Asociado 2 | `fldPvlHfxQvqxfrKT` | multipleSelects |
| Creado Por | `fldl6CJxYpsg7LcSN` | multipleRecordLinks → BD empleados |
| Tipo | `fldpOESIUzgtJOpif` | singleSelect |
| Área | `fldUVFFVn9KGAkKL4` | singleSelect |
| Estado | `fldiBp0diZIQNpnAZ` | singleSelect |
| Prioridad | `fldmQfMvBP4E04jxU` | singleSelect |
| Relacionado a | `fldseqjsBDGqrKhmt` | singleSelect |
| Etapa Proyecto | `fldFE6p7Ir5wDOGE9` | singleSelect |
| Tipo De Tarea | `fldyg5hVkj9w6HmLp` | singleSelect |
| Fecha De Creación | `fldKYOsXKfGLYJJBV` | createdTime |
| Fecha De Inicio | `fldAibBMfVSz6rFLi` | dateTime |
| Fecha De Finalización | `fld8xgpFrC1hTik5C` | dateTime |
| Días Restantes | `fldQfmGkAvz9rIorn` | formula |
| Archivo Adjunto | `fldmPuNZ43RwTAsyw` | multipleAttachments |
| Cantidad Asignados | `fldeAaJ2fIv50Gc7D` | formula |
| Duración (Und) | `fldtnlZ72rHv2f6vn` | formula |
| Relacionado a (simple) | `fld0sTIxL8lHfIyhn` | formula |
| Relacionado a (detalle) | `fldw2BSHiJEZRlDSg` | formula |
| Proyectos de tecnología | `fldeb81j8NwozWRA2` | multipleRecordLinks → Proyectos de tecnología |
| Cotizaciones | `fldLxyJsyTawx42Wh` | multipleRecordLinks → Cotizaciones (sync) |
| Prospectos 1 | `fldgs09zHW5dz9czZ` | multipleRecordLinks → CRM Prospecto (sync) |
| Prospectos 2 | `fldGoJOca0nK9ULEE` | multipleRecordLinks → CRM Prospecto (sync) |
| Prospectos 3 | `fld9bhwz4cSwHhzy6` | multipleRecordLinks → CRM Prospecto (sync) |
| Prospectos 4 | `fld65wHPgTiQNLsLO` | multipleRecordLinks → CRM Prospecto (sync) |
| Proyecto | `fldbI8NmMu2CVAllK` | multipleRecordLinks → Proyecto (sync) |
| ID Proyecto Tag | `fldti2QGwUhwUh1An` | singleSelect |
| Nombre (from Proyecto) | `fldunebnHKagzbodp` | multipleLookupValues |
| Nombre (from Asignado a) | `fldSg1kwEf78f749j` | multipleLookupValues |
| Nombre (from Creado Por) | `fldGmjdRE0YJZsWcx` | multipleLookupValues |
| Correo Softr (from Asignado a) | `fldb4erlxsHah3fbT` | multipleLookupValues |
| Correo Softr (from Creado Por) | `fldxYYrz26D3eIzoN` | multipleLookupValues |
| Solicitudes | `fldzfSakFIEa1aKt9` | multipleRecordLinks → Solicitudes |
| Estado (from Solicitudes) | `fldNNDY8tl6ePcB6X` | multipleLookupValues |
| Numero Ordenar | `fldagc1Zmgg3lfAVC` | autoNumber |
| Make | `fldybSfNXX7pNWyMB` | lastModifiedTime |
| Tarea Fórmula | `fldaKku6P4aKYWwR9` | formula |

### Opciones de `Tipo`

| Opción | ID |
|---|---|
| Solicitud | `selixedYOgqBA81On` |
| Por Área | `sel6hu7oGzih1AMug` |
| Colaborativa | `selPyTArWe2xYgZ5O` |
| Personal | `selO5vGGPV8HrdqfR` |
| Técnico | `selWF3S1AmdezKLrC` |

### Opciones de `Área`

| Opción | ID |
|---|---|
| Comercial | `selYzW3nWLyXH8IYN` |
| Tecnología | `sele13lJGk6FOfaT9` |
| Proyectos | `seloxRbvibcBU2r5Z` |
| Administrativa | `seldUKDmFv7dDbacW` |
| SST | `selCbzpFAMWUgahOn` |

### Opciones de `Estado`

| Opción | ID |
|---|---|
| Terminada | `seltFklKDhwX565Ws` |
| Stand By | `selkMPNeiZ8g33xwO` |
| En Ejecución | `selcB94McnoqNonyr` |
| No Iniciada | `selxHxBV8uwE1VIJd` |
| Descartada | `selo1vU6DyLeWNJ7b` |

### Opciones de `Prioridad`

| Opción | ID |
|---|---|
| Baja | `sel8a8WZDGBphVSja` |
| Media | `selABXlMG1crG3A2c` |
| Alta | `selD3E6Qz0jPDtP08` |

### Opciones de `Relacionado a`

| Opción | ID |
|---|---|
| Proyecto | `selG2p6Hen6suLSe8` |
| Cotización | `selAC8z5qZyU4beR4` |
| Tecnología | `selEt7tFelSqIzAsO` |
| Prospecto | `seljL8eTFSDxmhc7Q` |
| Requerimientos | `seldlniSuA817ODAf` |
| Administrativo | `selqkJix6IKqhZpSJ` |
| Otros | `selcE6Y8O0Yval2pK` |

### Opciones de `Etapa Proyecto`

| Opción | ID |
|---|---|
| Afiliaciones | `sel590iW2t6rXaMQ2` |
| Compras | `sel83wl7OHCfKHUSK` |
| Herramientas y EPP | `selcYSpwL62xbHC7o` |
| Guía de Ejecución | `sel19isV31a5KTSZA` |
| Permisos | `selBMoRQkDJ3CyiS8` |
| En Ejecución | `sel2luKlCFEs6ouCR` |
| Ejecución Culminada | `selYdDEKEoMJcfWOc` |
| Entrega | `selgtPRANQF2dOEIH` |

### Opciones de `Tipo De Tarea`

| Opción | ID |
|---|---|
| Llamada | `selhFy8sp26yJR4NG` |
| Reunión | `selEfNkXn9u0fHNn5` |
| Seguimiento | `selmJQN1nnDwMtluD` |
| Visita Comercial | `selkl07syykdEIiaX` |
| Creación | `sel5JDTXB5Pxm4oSt` |
| Corrección | `sel5lrUZycSCYeveI` |
| Compras | `selZbjqNF4w8EJ5wi` |

---


Primero necesito obtener los IDs de los campos de la tabla para luego consultar el schema completo.Necesito primero listar las tablas para obtener los IDs de los campos. Déjame buscar esa herramienta.Voy a usar `list_tables_for_base` para obtener los campos de la tabla Agenda.Tengo los campos de la tabla **Agenda**. Ahora necesito obtener el schema completo para los campos de tipo `singleSelect` para ver sus opciones.Tengo todo lo que necesito. Aquí está la tabla completa con los campos de la tabla **Agenda** y las sub-tablas para los campos de selección:

---

## Campos de la tabla: Agenda (`tblPi2hORWogPP1NV`)

| Nombre | ID | Tipo |
|---|---|---|
| ID | `fldaJSpk0wKYxdgts` | autoNumber |
| Usuario | `fldx6idIKkuQ4KEPx` | multipleRecordLinks |
| Columna | `fldm3zcCvUWIxtZY4` | singleSelect |
| Nombre | `fld3mr1czG5IHY7L7` | singleLineText |
| Descripción | `flduyxQnnxzewkuL2` | richText |
| Categoría | `fldMf3xNzwRzfXmAn` | singleSelect |
| Portada | `flda8i6ifm225BwMk` | multipleAttachments |
| Documentos | `fldE9qTSizRiWp4XR` | multipleAttachments |
| Config Checks | `fldrgdWFhkLQvGJiC` | multilineText |
| Config URLs | `fldUE8KzMHEduUrOu` | multilineText |

---

### Campo: Columna (`fldm3zcCvUWIxtZY4`)

| Opción | ID |
|---|---|
| Lunes | `selcw1N8s4PQjdSlR` |
| Martes | `selfnikKHsAT0CMlY` |
| Miercoles | `sellv3SAOI5ct7vrd` |
| Jueves | `selcshs9jmfcmAfhG` |
| Viernes | `seliEqpBlbdi4YIlO` |
| Sabado | `sel9qg2QwqB2cgIpf` |
| Domingo | `sel2WJhwtHIgfiGKZ` |
| Pausado | `selRQJxeRaqdDXKtp` |
| Baúl | `selibXPFrNo4RQxOm` |

---

### Campo: Categoría (`fldMf3xNzwRzfXmAn`)

| Opción | ID |
|---|---|
| Clientes | `selldxEx1hfsEFpym` |
| Administrativo | `selFItHYrovrOpTQ9` |
| Comercial | `selZOlTEDIfptQMnQ` |
| Personal | `selVZI9yL2Sy5dz1Y` |
| Welldone | `selxLFbHOO0UaGOKe` |
| Proyectos | `seluCOrdqy3jGbIH5` |

# Base Toma de Requerimientos (`appk8ZBGkmqabmzyN`)

Base dedicada al proceso de toma de requerimientos en visita técnica, generación de alternativas de cotización y construcción del WBS. Alimenta el proceso de cotización de la base principal.

## Tablas de esta base

| Tabla | ID | Uso |
|---|---|---|
| Requerimientos | `tbl53IJDa2cqxXBMP` | Registros de visita técnica con ítems N1–N6 |
| Solicitudes | `tbl8NMEaGw8zDTzqH` | Solicitudes de servicio entrantes |
| Clientes | `tblhToU4qlImfF1h3` | Clientes (sync) |
| BD empleados | `tblQAZYq53t7HJZSV` | Personal (sync) |
| CRM Cotizaciones | `tblNBL5YDtDbCcPAz` | Cotizaciones (sync) |
| Requerimiento (legacy) | `tbl9hsI1GGgvbcvFl` | Versión anterior — no usar en bloques nuevos |
| Técnicos | `tblVWcU2fT1A7qT1F` | Técnicos (sync) |
| Info Personal | `tblO26crSNACAD7UP` | Personal info (sync) |
| Alternativas | `tbl6trVL27XlcsFUm` | Alternativas de cotización por requerimiento |
| Etapas_Estado | `tblDLvJc8iGuIAaZJ` | Estados de etapas de cada alternativa |
| WBS_Items | `tblbBpVliCNlO2PLM` | Ítems del WBS por alternativa |
| WBS_SubItems | `tblcRULrcGCjjYX9s` | Sub-ítems del WBS |
| Modelo_Economico | `tblAnOna6bRaabUq4` | Modelo económico por alternativa |
| Templates_Items | `tblOjmmFp0sIHW4RI` | Plantillas de ítems |
| Templates_SubItems | `tbl7ZmUWu1p7ZS5RG` | Plantillas de sub-ítems |
| Items_Propuesta | `tbl5edZIpE77CVW7f` | Ítems generados por IA para propuesta comercial |
| Propuestas | `tblTBMsMKmyTRpKk7` | Propuestas generadas |

---

## Requerimientos (`tbl53IJDa2cqxXBMP`)

Tabla central de esta base. Cada registro representa una visita técnica con hasta 6 ítems documentados.

### Campos generales

| Campo | ID | Tipo |
|---|---|---|
| Detalles generales del requerimiento | `fldibyEluMuKN5gFj` | singleLineText (primary) |
| Nombre de la cotización | `fldCYhX34ZQKkcSdx` | singleLineText |
| Código Requerimiento | `fld16SzTT2Mx68iH1` | formula |
| Fecha programación visita | `fldAabDzkVkw2zqSL` | date |
| Fecha de visita | `fld8iKoitgC9W7BLU` | date |
| Fecha Entrega Cotización | `fldwhey4lfI4ZLHrH` | date |
| Fecha creación | `fldfHn8YiL2t2teZp` | dateTime |
| Fecha de Creación (Nueva) | `fldQO5jdcvhncNoTT` | createdTime |
| Fecha de Creación Formula | `fldGzNmvfydLwFrLg` | formula — unifica las dos fechas anteriores |
| ID Requerimiento | `fldiQIKOBQbYXEIOK` | autoNumber |
| Record ID | `fldEeL6Xncdmvc1oa` | formula |
| ID Real | `fldMXeFDyJ9Idh4BX` | formula |
| Ubicación | `fldblAZjuQ9MeJLl1` | singleLineText |
| Dirección del activo | `fldRJIkQqWQDHF2Om` | singleLineText |
| Geolocalización | `fldes3sqVu0kRS6x5` | singleLineText |
| Restricciones horarias | `fldLACsUlmtiOfKOC` | singleLineText |
| Persona de contacto | `fldApQrUQwtHvGIV6` | singleLineText |
| Quien recibe la visita | `fld9S41zCX1nmM4u6` | singleLineText |
| Quien recibirá la oferta | `fldjvvUEbiJ06ZLJU` | singleSelect |
| Tomador de decisión | `fldo532VDijdKbP4a` | singleSelect |
| Nivel de urgencia | `fldIxmUhJTMVp7IBl` | singleSelect |
| Nombre del activo | `fldifqoN3QUjCHkwi` | singleSelect — ⚠️ pendiente de documentar (60+ opciones) |
| Asesor Comercial | `fldNLG3KLWSft82n7` | singleSelect |
| Quien diligencia | `fldgPIxLnwsCxStcK` | singleSelect |
| Estado | `fldTMXj49FFQwlznf` | singleSelect |
| Validación con el cliente | `flduwn0XONm7O5B2f` | singleSelect |
| Estado de procesamiento | `fldZHXchhLpCpyKok` | singleSelect |
| Telefono | `fldiu2UZdnYqWja9N` | phoneNumber |
| Email | `fldk5eRSvu31OfteY` | email |
| Archivos relacionados | `fldgXXJnqMmbrv5Zs` | url |
| Archivos de ayuda | `fldNGykMB8EpmarF1` | multipleAttachments |
| Fotos preliminares | `fldJ53w0miCXhRpwi` | multipleAttachments |
| Recomendaciones del técnico | `fldSO9KGnuM3dYgM4` | richText |
| Generar ayudas al técnico | `fldWWC1N4ehDVkCw2` | checkbox |
| Ayudas al técnico | `fldc0rBwKNp8cSi0N` | aiText — solo lectura |
| Requiere atención | `fld3rSrqPeP3X0ueI` | checkbox |
| Hefesto | `fld1X75ShEQaRvD2c` | checkbox |
| Por Validar | `fldHumUxXivnjt1Rz` | checkbox |
| Numero Requerimientos | `fldz8moVapJPqxP5J` | multipleSelects |
| Cliente | `fldgbqxKtGAvmovM1` | multipleRecordLinks → Clientes |
| Tipo De Cliente (from Cliente) | `fld6V4jmdcVSyFJd4` | multipleLookupValues |
| Portada (from Clientes) | `fldaIaZGaoiMgOJ5D` | multipleLookupValues |
| Técnico Asignado | `fld8KFi9CKv8jab07` | multipleRecordLinks → BD empleados |
| Correo Softr (from Técnico Asignado) | `fld2AmMMPE2lUIkpS` | multipleLookupValues |
| CRM Cotizaciones | `fldpIknPmYWtItZTF` | multipleRecordLinks → CRM Cotizaciones |
| Solicitudes | `fldDaAd2wAXvbPZRL` | multipleRecordLinks → Solicitudes |
| Sector | `fldDh9YhKpNNREQDT` | multipleLookupValues |
| Tipo de necesidad | `fldI1efyVS1pOk1le` | singleSelect |
| Impacto operativo | `fldURydkWzISwxWkU` | singleSelect |
| Estado Solicitud | `fldarmjUVO4ZoH4A8` | singleSelect |
| Validado por | `fldg0xPBTggwxMWwX` | singleLineText |
| Fecha de validación | `fldcSzatR2FxBl8j6` | date |
| Observaciones de validación | `fld24gffdOfAtjo19` | richText |
| Requiere visita técnica | `fldojVtLTg6H2x5VR` | checkbox |
| Fecha Solicitud | `fldwgci1gP9ioPLOe` | date |
| Persona que Solicita | `fldEb1bIykq0LZtci` | singleLineText |
| Proyecto Relacionado | `fldV1m5veZQ55B93g` | singleLineText |

### Campos por ítem (N1–N6)

> ⚠️ **Trampa de naming verificada en base real (2026-05-07):**
> - Los campos de fotos y videos se llaman **`Registro Fotográfico Requerimiento N{1..6}`** y **`Registro Video Requerimiento N{1..6}`** — la palabra "Requerimiento" en el medio es obligatoria. Si en `q.select()` se omite, Softr no reconoce el campo y el bloque no guarda fotos/videos.
> - `Tipo de trabajo`, `Especialidad técnica` y `Tipo de activo` son **`singleSelect` en TODOS los slots N1–N6** (no solo en N1/N2 como decía una versión anterior de este doc). Se pueden poblar con `useFieldOptions` en los 6 slots.

| Campo | Tipo | ID N1 | ID N2 | ID N3 | ID N4 | ID N5 | ID N6 |
|---|---|---|---|---|---|---|---|
| Descripción del requerimiento | multilineText | `fld5LVzCIvY1UPuJx` | `fldjvbtqONO9Buz3O` | `fldsP3wqK3Osj6CyI` | `fldwKdanabKGK2vQW` | `fldnUtv2fZtJ09Pyy` | `fldF0bdvPk8QGLq7P` |
| Info complementaria ítem | richText | `fldSwenu8lZWVCNTq` | `fldTazrGUzi6SXAgc` | `fldohwoDDRbzxvhBL` | `fldhFVzhuFYYEYOwA` | `fldfvBBV8O9kIDRKg` | `fldVq0veFSTu1S3ni` |
| Condiciones del entorno ítem | richText | `fldIFa26rYkvm4jQg` | `fld29v7gx665ttmue` | `fldsVdgwhWqqIOWsY` | `fldU4574mnuVsBjq0` | `fldx4RD1y74pz3Owb` | `fldayR4MZGfMJf3rH` |
| Restricciones operativas ítem | richText (N6: multilineText) | `fldEZaC858DnYP8lY` | `fldJMJzlfDhjT5x9X` | `fldWN3wUJMNQDvSEW` | `fldTHua8nRTXgIQhs` | `fldTlpV2cn0TPDmgY` | `fldKVQFiKLpLxEgOp` |
| Identificación de riesgos ítem | richText | `fld6KOr1qHGYeCbWd` | `fldDRCgeq4mJ3fcrx` | `fldszop0EsCK3N17l` | `fldjT7xYU559yrUGD` | `fldk4zg1ha7OtchQb` | `fld3T6mmNdp9KbyPN` |
| **Registro Fotográfico Requerimiento** | multipleAttachments | `fldqlzyuCafrwfTEn` | `fldMVkLC8vIgs3y7R` | `fldnE58BFHQRDu7qJ` | `fldb8VtIvuVC71EMl` | `fldXFaV392wxtLi9I` | `fldp0DHGVLgNR55Pt` |
| **Registro Video Requerimiento** | multipleAttachments | `fldt9N0mxrSrHUX8W` | `fldbznlBGDGEJ32jC` | `fldZgsksM8yI5y1A1` | `fldqcdoh3kKjb60UG` | `fldXabHcD16CO2dMu` | `fldgJKmctgrkrphvB` |
| Tipo de trabajo | singleSelect | `fldP5baDqFLpYYXBk` | `fldGwqFC9JqSC5fu3` | `fldoGRIwxSPoNxxvo` | `fldKMdycAjww9Qwyw` | `fldor0VRBg7SY2zWX` | `fldOYXPZrtGvbNiz4` |
| Especialidad técnica | singleSelect | `fldmh0zQ217wVfo6I` | `fldb304XOWGHMqbWo` | `fldZjHlR1c3Iwvr52` | `fldpMJhEggl0X6G2T` | `fldsPSmJjqvUtZi9O` | `fldwmrwYuvGIJOx2h` |
| Tipo de activo | singleSelect | `fldyuxpS2sO2fP1Ky` | `fldAomoWr2Cc4kQtA` | `fldFJUh76Ky2XqqQX` | `fld2DQKCBkCTrKec0` | `fldQpNY8n0K6Y0auC` | `fld6MLkuthJauYcpt` |
| Presupuesto referencia | currency | `fldq9YjLRbGGon8rz` | `fld8f13LzjoIRgld1` | `fldoAKSlwlJyU0L3e` | `fldNm0YxzW2aqZDUO` | `fldcXWKLSGEzpWqpN` | `fldwlUz4YMFjxdGWH` |
| Monto anteriormente cotizado | currency | `fld31Ihu2x3GQI329` | `fldGHElq2TL3HU5Ly` | `fldJcNNkPrp2YkrZl` | `fldw0QDebgZ58OyO7` | `fldgw1WL2pE7jbGqS` | `fldhNxi950Sdfcbui` |

### Opciones de `Quien recibirá la oferta`

| Opción | ID |
|---|---|
| Facility manager | `selerkjge9uJJmgaw` |
| Jefe de mantenimiento | `selr17E3LkMHiRwbs` |
| Director administrativo | `selwKNzCQ5ZqtdCkt` |
| Director de operaciones | `seld8ljNytEYaAooj` |
| Técnico encargado | `selMDFVvFTmrMj58Q` |
| Gerencia | `selYh6Qq7EPJ9Rhzk` |
| Administrador de PH | `selLjcreQd4ScDLON` |
| Miembro del consejo | `selN8CBba3BhxpYxa` |
| Copropietario | `sel1bV4Lj3QJKLGz1` |

### Opciones de `Tomador de decisión`

| Opción | ID |
|---|---|
| Gerente | `sel74OBZa13szY3eQ` |
| Presidente | `selpD6B2LEk1xIq4z` |
| Departamento de compras | `selQDzIrXiRhcaDsj` |
| Quien recibe | `selKi45iMahOZt4vK` |
| Dueño | `seleJdZQ14F32m8BO` |
| Administrador | `selWcf0qf7YUDXv1g` |
| Consejo de administración | `selY3XJRlMnIuJWYd` |
| Asamblea | `selir8tlK5mOD5AAp` |

### Opciones de `Nivel de urgencia`

| Opción | ID |
|---|---|
| Bajo | `selTkFTzF2shdMWre` |
| Medio | `selaiYHAizmLa9737` |
| Alto | `selBT9iAEM72ULkFL` |

### Opciones de `Asesor Comercial`

| Opción | ID |
|---|---|
| Roberto Samper | `selw61uqkXt2VOK5U` |
| Edgar Sánchez | `selL4DxXYjxNXTJ8s` |
| Ronald Pedroza | `selRHtBRH4uBHdXTQ` |

### Opciones de `Quien diligencia`

| Opción | ID |
|---|---|
| Roberto Samper | `sel83sqO3aTjXrlJU` |
| Ronald Pedroza | `selpDYNjBqy1zqUeG` |
| Edgar Sánchez M | `selha5DutQU9lYS0v` |
| Omar Bolaño | `selWP5RZSUXGu2oHo` |
| Omar José Bolaño Vital | `selBxgNDzpMpEWIhX` |
| ROBERTO ENRIQUE SAMPER RAMIREZ | `sel8WOBECuyBFAZl5` |
| ERICK JAVIER RAMOS CANTILLO | `selRnnOS61kCsu84J` |
| RONALD ANDRES PEDROZA RODRIGUEZ | `selp7qgiY66CkeOA0` |
| EDGAR ENRIQUE SANCHEZ MERCADO | `selZkGwcKhMmOIkM8` |

### Opciones de `Estado`

| Opción | ID |
|---|---|
| Nuevo | `selIMKFnHSatXFrzH` |
| Procesando | `selV3RQSI6QsT0r98` |
| Por Validar | `selkkms6uo21gXs2P` |
| Validado | `selyF0G23Z3tiuUud` |
| Stand By | `selLkPHBQFLLOvbUi` |
| Descartado | `selGnub06fUcxnYFm` |
| Revisión de calidad | `selIMjsFoUzDEaFwe` |

### Opciones de `Validación con el cliente`

| Opción | ID |
|---|---|
| Si | `selPWERL6mGRvnzu7` |
| No | `sel09S1Roshto6ZQq` |

### Opciones de `Estado de procesamiento`

| Opción | ID |
|---|---|
| Pendiente | `selAZ9DfxXwqVHVTc` |
| Preparado | `selUd0prv5M3YUTCK` |
| Interpretado | `selwEz7gqw3TqWdt8` |
| Con diagnóstico | `selTZS4csdIZrGJlk` |
| Con alternativas | `seljdbII8hwEmSIGJ` |
| Alternativa definida | `selPHVVEt0YjgkpPO` |

### Opciones de `Tipo de trabajo` (N1 y N2)

| Opción | ID N1 | ID N2 |
|---|---|---|
| Mantenimiento | `selmAYv63YEDfBkqL` | `sel7PeTN8ECr4IPdA` |
| Obra civil | `selpdhf8WATUBU3dc` | `selS9buntMTUiGmX5` |
| Instalación | `selDSAGJY6f3HstfV` | `seloFQk6c8jitzMwy` |
| Suministro | `selwdcNcqki5DjLNy` | `seluks8lgAWydMg4g` |
| Servicio especial | `selwXoT5h5addj47k` | `selM9u1LkZGY908NK` |

### Opciones de `Especialidad técnica` (N1 y N2)

| Opción | ID N1 | ID N2 |
|---|---|---|
| Eléctrica | `sela2HAnVGl0VqMyT` | `selqV7hOu9d4XdXS3` |
| Hidráulica | `sel5T42iGNpvJn1th` | `sel4Mxr09EHn5KqwY` |
| Locativa | `selMcR3dYTwcBzDmd` | `seltT0JlkeDAPZvvv` |
| Mecánica | `selAcLmroiQSY7Hvl` | `selmvyLL9rSjQW7Es` |
| Civil | `selNPYBHMSBQ69ufW` | `sel4LXqsWDdGbskrx` |
| Consultoría | `seldY9JgqDUGrXW5j` | `selVYJoMVIveQIbYw` |
| Otra | `selQrxcHKezTZKieU` | `selz71whJNYQwawpl` |

### Opciones de `Tipo de activo` (N1 y N2)

| Opción | ID N1 | ID N2 |
|---|---|---|
| Hotel | `selrybxWnhhtbqEnH` | `selH36qK0nwx7EXkK` |
| Bodega | `selTd6EYfrDIRuOq4` | `sel4SOkC21QntplIQ` |
| Oficina | `selpCtQBzBq9VW10X` | `selsqoRdgr12xzWlK` |
| Planta industrial | `selAP2aGTihh9Xq0v` | `selvputvsqYsyHTWn` |
| Edificio | `sel8DGpusHBTUJheW` | `selr2qf6IznK744NF` |
| Universidad | `selcczligf6CNeaZu` | `selDiN4jAM3ZxuxHw` |
| Propiedad horizontal | `selpfdsWkATqH2SdR` | `sel6AjlUGf7G4Rf5y` |
| Centro logístico | `selKKnFZ5o5KDd4mi` | `selT5ZMULHfMtjRLK` |
| Parque logístico | `seleQ9K66hEh0xnbi` | `selGxNixEnE12LNrQ` |
| Zona franca | `sel7lNN2bOsIm9O39` | `sel1aUxlffBnsH0Ge` |
| Centro comercial | `seltXLT6byjcMqbWl` | `selLju3erQdqEwjhR` |
| Local comercial | `selYJZFaUv6kDfWt2` | `selTUvqq6WCMrJFzT` |
| Otro | `selvVD2naVZikau74` | `sel5bSbMByl9oK5Yy` |
| Puerta | `seluNvwzjaV44gI4z` | `selHA1Wp63ZeKOkpq` |

### Opciones de `Tipo de necesidad`

| Opción | ID |
|---|---|
| Correctivo | `seliRAvfMWk1djWM8` |
| Preventivo | `seley3XMuiD4InALl` |
| Mejora | `selyrDDTmq7HLDA5T` |
| Diagnóstico | `selkT0H9WGniD96MX` |

### Opciones de `Impacto operativo`

| Opción | ID |
|---|---|
| Alto | `selw2kt2USEN0Frqa` |
| Medio | `selXl4Mw68cQU9EFv` |
| Bajo | `selPbH5JXHHZ7eKcj` |

### Opciones de `Estado Solicitud`

| Opción | ID |
|---|---|
| Por Validar | `selDPCGIAfqSVnAOd` |
| Validado | `selSCsW16o46GGEJK` |
| Descartado | `selQVskBcDeHiwaB7` |
| Stand by | `sel4yAKCC8AmiaXTt` |

---

## Trampas conocidas (regresar aquí ante errores)

1. **`Item 3 Registro Fotográfico`** sin tilde — los demás slots usan "Ítem". Esto es histórico y no se puede cambiar sin romper integraciones.
2. **`Estado Facturacion`** sin tilde en "Facturacion" — es formula.
3. **`Propuesta en Canva  (from CRM Cotizacionez)`** — tiene **doble espacio** después de "Canva".
4. **`(from CRM Cotizacionez)`** vs `(from CRM Cotizaciones)` — varios lookups en Proyectos usan **"Cotizacionez"** (con z al final). Es un typo histórico que aún funciona.
5. Las opciones **"A Facturar"** y **"Facturado"** del campo Estado de Proyectos **fueron eliminadas**. Para mostrar este estado usar la fórmula `Estado Facturacion`.
6. **Tres bases distintas** — Portal Empresarial Welldone (`appAEV0iaC3VfB5Zb`), Gestión Tareas (`appKb51aF3l8aB8Fn`) y Toma de Requerimientos (`appk8ZBGkmqabmzyN`). Un bloque solo puede conectarse a una Source/base a la vez. Para cruzar datos entre bases usar `window.__variable`.
7. **`Solicitudes` tiene dos campos "Prioridad"** — `Prioridad de Solicitud` (`fldsGGy8unqgcXQCO`) es la que ingresa el solicitante; `Prioridad` (`fldYGZDJQJhYARQjy`) es la que asigna internamente el equipo después de evaluar. Son campos distintos con opciones distintas.