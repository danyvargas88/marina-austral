# Estructura de Base de Datos - Marina Austral

## Información General
- **Database:** `marina_austral`
- **Extraído:** 2026-02-26
- **Total de tablas:** 10

---

## Tablas

### `audit_log`

| # | Columna | Tipo | Nullable | Default | PK |
|---|---------|------|----------|---------|----|
| 1 | `id` | integer | NO | nextval('audit_log_id_seq'::regclass) | 🔑 |
| 2 | `usuario_superadmin_id` | integer | YES | - |  |
| 3 | `accion` | character varying(50) | NO | - |  |
| 4 | `tabla` | character varying(50) | NO | - |  |
| 5 | `registro_id` | integer | YES | - |  |
| 6 | `descripcion` | text | YES | - |  |
| 7 | `datos_anteriores` | jsonb | YES | - |  |
| 8 | `datos_nuevos` | jsonb | YES | - |  |
| 9 | `ip_address` | character varying(45) | YES | - |  |
| 10 | `user_agent` | text | YES | - |  |
| 11 | `created_at` | timestamp without time zone | YES | now() |  |

**Primary Key:** `id`

**Foreign Keys:** `usuario_superadmin_id` → `usuarios_superadmin.id`

---

### `comprobantes`

| # | Columna | Tipo | Nullable | Default | PK |
|---|---------|------|----------|---------|----|
| 1 | `id` | integer | NO | nextval('comprobantes_id_seq'::regclass) | 🔑 |
| 2 | `proveedor_cuit` | character varying(15) | YES | - |  |
| 3 | `tipo` | character varying(50) | YES | - |  |
| 4 | `numero` | character varying(50) | YES | - |  |
| 5 | `descripcion` | text | YES | - |  |
| 6 | `fecha_emision` | date | YES | - |  |
| 7 | `archivo_nombre` | character varying(255) | YES | - |  |
| 8 | `archivo_drive_id` | character varying(100) | YES | - |  |
| 9 | `fecha_carga` | timestamp without time zone | YES | now() |  |

**Primary Key:** `id`

**Foreign Keys:** `proveedor_cuit` → `proveedores.cuit`

---

### `facturas`

| # | Columna | Tipo | Nullable | Default | PK |
|---|---------|------|----------|---------|----|
| 1 | `id` | bigint | NO | nextval('facturas_id_seq'::regclass) | 🔑 |
| 2 | `fecha_emision` | date | YES | - |  |
| 3 | `tipo` | character(1) | YES | - |  |
| 4 | `factura` | character varying(50) | NO | - |  |
| 5 | `fecha_vencimiento` | date | YES | - |  |
| 6 | `cuit` | character varying(20) | NO | - |  |
| 7 | `empresa` | character varying(255) | YES | - |  |
| 8 | `base_imponible` | numeric(12,2) | YES | - |  |
| 9 | `porcentaje_iva` | numeric(5,2) | YES | - |  |
| 10 | `importe_iva` | numeric(12,2) | YES | - |  |
| 11 | `total` | numeric(12,2) | YES | - |  |
| 12 | `link_factura` | text | YES | - |  |
| 13 | `estado` | character varying(20) | YES | 'PROCESADO' |  |
| 14 | `periodo` | character varying(20) | YES | - |  |
| 15 | `logs` | jsonb | YES | '[]'::jsonb |  |
| 16 | `created_at` | timestamp without time zone | YES | now() |  |
| 17 | `updated_at` | timestamp without time zone | YES | now() |  |

**Primary Key:** `id`

**Constraints:** 
- `facturas_estado_check`: CHECK (estado IN ('ENVIADO', 'PROCESADO', 'PENDIENTE PAGO', 'PAGADO', 'A_REVISAR', 'ADJUNTO'))

---

### `password_reset_tokens`

| # | Columna | Tipo | Nullable | Default | PK |
|---|---------|------|----------|---------|----|
| 1 | `id` | integer | NO | nextval('password_reset_tokens_id_seq'::regclass) | 🔑 |
| 2 | `proveedor_id` | integer | NO | - |  |
| 3 | `cuit` | character varying(15) | NO | - |  |
| 4 | `email` | character varying(255) | NO | - |  |
| 5 | `token` | character varying(100) | NO | - |  |
| 6 | `expira_en` | timestamp without time zone | NO | - |  |
| 7 | `usado` | boolean | YES | false |  |
| 8 | `ip_solicitante` | character varying(50) | YES | - |  |
| 9 | `created_at` | timestamp without time zone | YES | now() |  |
| 10 | `usado_en` | timestamp without time zone | YES | - |  |

**Primary Key:** `id`

**Foreign Keys:** `proveedor_id` → `proveedores.id`

---

### `proveedores`

| # | Columna | Tipo | Nullable | Default | PK |
|---|---------|------|----------|---------|----|
| 1 | `id` | integer | NO | nextval('proveedores_id_seq'::regclass) | 🔑 |
| 2 | `cuit` | character varying(15) | NO | - |  |
| 3 | `nombre_empresa` | character varying(255) | NO | - |  |
| 4 | `email` | character varying(255) | YES | - |  |
| 5 | `password_hash` | character varying(255) | NO | - |  |
| 6 | `telefono` | character varying(20) | YES | - |  |
| 7 | `carpeta_drive_id` | character varying(100) | YES | - |  |
| 8 | `activo` | boolean | YES | true |  |
| 9 | `fecha_registro` | timestamp without time zone | YES | now() |  |
| 10 | `ultimo_acceso` | timestamp without time zone | YES | - |  |

**Primary Key:** `id`

**Constraints:** 
- `proveedores_cuit_check`: CHECK (cuit ~ '^\d{11}$')

---

### `recent_errors`

| # | Columna | Tipo | Nullable | Default | PK |
|---|---------|------|----------|---------|----|
| 1 | `id` | integer | YES | - |  |
| 2 | `workflow_name` | character varying(255) | YES | - |  |
| 3 | `execution_id` | character varying(255) | YES | - |  |
| 4 | `status` | character varying(50) | YES | - |  |
| 5 | `message` | text | YES | - |  |
| 6 | `context` | jsonb | YES | - |  |
| 7 | `created_at` | timestamp without time zone | YES | - |  |
| 8 | `error_details` | text | YES | - |  |

---

### `usuarios_admin`

| # | Columna | Tipo | Nullable | Default | PK |
|---|---------|------|----------|---------|----|
| 1 | `id` | integer | NO | nextval('usuarios_admin_id_seq'::regclass) | 🔑 |
| 2 | `username` | character varying(50) | NO | - |  |
| 3 | `password_hash` | character varying(255) | NO | - |  |
| 4 | `nombre_completo` | character varying(100) | NO | - |  |
| 5 | `email` | character varying(100) | YES | - |  |
| 6 | `role` | character varying(20) | YES | 'usuario' |  |
| 7 | `activo` | boolean | YES | true |  |
| 8 | `ultimo_acceso` | timestamp without time zone | YES | - |  |
| 9 | `created_at` | timestamp without time zone | YES | now() |  |
| 10 | `updated_at` | timestamp without time zone | YES | now() |  |
| 11 | `created_by` | integer | YES | - |  |

**Primary Key:** `id`

**Foreign Keys:** `created_by` → `usuarios_superadmin.id`

**Constraints:** 
- `usuarios_admin_role_check`: CHECK (role IN ('admin', 'usuario'))

---

### `usuarios_superadmin`

| # | Columna | Tipo | Nullable | Default | PK |
|---|---------|------|----------|---------|----|
| 1 | `id` | integer | NO | nextval('usuarios_superadmin_id_seq'::regclass) | 🔑 |
| 2 | `username` | character varying(50) | NO | - |  |
| 3 | `password_hash` | character varying(255) | NO | - |  |
| 4 | `nombre_completo` | character varying(100) | NO | - |  |
| 5 | `email` | character varying(100) | NO | - |  |
| 6 | `activo` | boolean | YES | true |  |
| 7 | `ultimo_acceso` | timestamp without time zone | YES | - |  |
| 8 | `ip_ultimo_acceso` | character varying(45) | YES | - |  |
| 9 | `created_at` | timestamp without time zone | YES | now() |  |
| 10 | `updated_at` | timestamp without time zone | YES | now() |  |

**Primary Key:** `id`

---

### `workflow_logs`

| # | Columna | Tipo | Nullable | Default | PK |
|---|---------|------|----------|---------|----|
| 1 | `id` | integer | NO | nextval('workflow_logs_id_seq'::regclass) | 🔑 |
| 2 | `workflow_name` | character varying(255) | NO | - |  |
| 3 | `execution_id` | character varying(255) | YES | - |  |
| 4 | `status` | character varying(50) | NO | - |  |
| 5 | `message` | text | YES | - |  |
| 6 | `context` | jsonb | YES | - |  |
| 7 | `created_at` | timestamp without time zone | YES | now() |  |
| 8 | `error_details` | text | YES | - |  |

**Primary Key:** `id`

---

## Notas Importantes

### Tipos de Factura
| Tipo | Descripción |
|------|-------------|
| `A`, `B`, `C` | Facturas normales (procesadas con OCR) |
| `X` | Archivos adjuntos (sin OCR) |

### Estados de Factura
| Estado | Descripción |
|--------|-------------|
| `ENVIADO` | Factura subida, pendiente de procesar |
| `PROCESADO` | OCR completado, datos extraídos |
| `PENDIENTE PAGO` | Aprobada para pago |
| `PAGADO` | Pago realizado |
| `A_REVISAR` | Requiere revisión manual |
| `ADJUNTO` | Archivo adjunto (no es factura) |

### Constraints Clave
- **facturas_estado_check**: Solo permite estados definidos
- **proveedores_cuit_check**: CUIT debe tener 11 dígitos
- **usuarios_admin_role_check**: Solo 'admin' o 'usuario'

---

## Relaciones entre Tablas
proveedores (cuit) ←── facturas (cuit)
proveedores (id) ←── password_reset_tokens (proveedor_id)
proveedores (cuit) ←── comprobantes (proveedor_cuit)
usuarios_superadmin (id) ←── usuarios_admin (created_by)
usuarios_superadmin (id) ←── audit_log (usuario_superadmin_id)

---

*Última actualización: 2026-02-26*