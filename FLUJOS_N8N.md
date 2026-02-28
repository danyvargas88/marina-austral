# 📋 Flujos de Trabajo N8N - Portal de Proveedores Marina Austral

Este documento describe todos los flujos de trabajo activos en N8N para el sistema Portal de Proveedores, organizados por módulos funcionales.

---

## 📑 Índice de Flujos

| Módulo | Flujo | Path | Descripción |
|--------|-------|------|-------------|
| **Super Admin** | PUT Facturas | `superadmin/facturas` | Actualizar facturas |
| | GET Facturas | `superadmin/facturas` | Buscar y listar facturas |
| | Audit Logs | `superadmin/audit-logs` | Registro de logs |
| | Usuarios CRUD | `superadmin/usuarios` | Gestión de usuarios |
| | Proveedores CRUD | `superadmin/proveedores` | Gestión de proveedores |
| | Dashboard | `superadmin/dashboard` | Dashboard principal |
| | Login | `superadmin/login` | Autenticación |
| **Proveedores API** | Login | `api-proveedores/login` | Autenticación proveedores |
| | Get Facturas | `api-proveedores/facturas` | Listar facturas |
| | Get Comprobantes Drive | `api-proveedores/archivos-drive` | Listar archivos Google Drive |
| | Subir Factura OCR | `portal-proveedores/subir` | Subir facturas con OCR |
| | Subir Adjuntos | `portal-proveedores/adjuntos/subir` | Cargar documentos adjuntos |
| | Cambiar Password | `api-proveedores/cambiar-password` | Cambio de contraseña |
| | Solicitar Reset Password | `api-proveedores/solicitar-reset` | Solicitud reset vía email |
| | Validar Token | `api-proveedores/validar-token` | Validación token de reset |
| | Reset Password | `api-proveedores/reset-password` | Ejecutar cambio de contraseña |
| **Admin Dashboard** | Get Facturas Dashboard | `api/admin/facturas` | Listar facturas admin |
| | Update Estado Factura | `api/admin/update-estado` | Actualizar estado |
| | Login | `admin/login` | Autenticación admin |
| | Sync BBDD a Sheets | `sync-db-to-sheets` | Sincronización Google Sheets |
| **Shared Workflows** | Error Handler | - | Detección y alerta de errores |

---

## 🏛️ Super Admin

Módulo de administración general del sistema con acceso total.

### 🔐 Autenticación
| Flujo | Path | Método | Descripción |
|-------|------|--------|-------------|
| Superadmin-Login | `superadmin/login` | POST | Login del Superadmin |

### 📊 Dashboard
| Flujo | Path | Método | Descripción |
|-------|------|--------|-------------|
| Superadmin-Dashboard | `superadmin/dashboard` | GET | Dashboard principal Superadmin |

### 💰 Gestión de Facturas
| Flujo | Path | Método | Descripción |
|-------|------|--------|-------------|
| PUT Facturas (Actualizar) | `superadmin/facturas` | PUT | Permite actualizar facturas |
| GET Facturas (Búsqueda) | `superadmin/facturas` | GET | Busca y Lista Facturas |

### 👥 Gestión de Usuarios
| Flujo | Path | Método | Descripción |
|-------|------|--------|-------------|
| Superadmin-Usuarios-CRUD | `superadmin/usuarios` | CRUD | Crea, Actualiza y Elimina Usuarios |

### 🏢 Gestión de Proveedores
| Flujo | Path | Método | Descripción |
|-------|------|--------|-------------|
| Superadmin-Proveedores-CRUD | `superadmin/proveedores` | CRUD | Crea, Actualiza y Elimina Proveedores |

### 📜 Auditoría
| Flujo | Path | Método | Descripción |
|-------|------|--------|-------------|
| Superadmin-Audit-Logs | `superadmin/audit-logs` | GET | Logs del sistema |

---

## 🚢 Proveedores API

Módulo de acceso para proveedores externos.

### 🔐 Autenticación
| Flujo | Path | Método | Descripción |
|-------|------|--------|-------------|
| 01 - Proveedores Login | `api-proveedores/login` | POST | Login Portal Proveedores |

### 📄 Gestión de Facturas
| Flujo | Path | Método | Descripción |
|-------|------|--------|-------------|
| 02 - Proveedores Get Facturas | `api-proveedores/facturas` | GET | Listar Facturas en Portal Proveedores |
| 06 - Proveedor Subir Factura con OCR | `portal-proveedores/subir` | POST | Subir Facturas Proveedor con procesamiento OCR |

### 📁 Gestión de Archivos
| Flujo | Path | Método | Descripción |
|-------|------|--------|-------------|
| 04 - Proveedores Get Comprobantes Drive | `api-proveedores/archivos-drive` | GET | Listar archivos Google Drive |
| 07-Proveedor-Subir-Adjuntos | `portal-proveedores/adjuntos/subir` | POST | Cargar Documentos Adjuntos Proveedores |

### 🔑 Gestión de Contraseñas
| Flujo | Path | Método | Descripción |
|-------|------|--------|-------------|
| 03-Proveedores-Solicitar-Reset-Password | `api-proveedores/solicitar-reset` | POST | Solicitud de cambio de password vía email |
| 04-Proveedores-Validar-Token | `api-proveedores/validar-token` | GET | Validación de token para cambio de password |
| 05-Proveedores-Reset-Password | `api-proveedores/reset-password` | POST | Ejecución del cambio de password en portal |
| 06-Proveedores-Cambiar-Password | `api-proveedores/cambiar-password` | PUT | Cambio de password directo para proveedores |

---

## ⚙️ Admin Dashboard

Módulo de administración operativa.

### 🔐 Autenticación
| Flujo | Path | Método | Descripción |
|-------|------|--------|-------------|
| Admin-Login | `admin/login` | POST | Login de Admin |

### 📊 Gestión de Facturas
| Flujo | Path | Método | Descripción |
|-------|------|--------|-------------|
| 06 - Admin Get Facturas Dashboard | `api/admin/facturas` | GET | Listar Facturas en Dashboard |
| 07 - Admin Update Estado Factura | `api/admin/update-estado` | PUT/PATCH | Actualizar Estado de Factura |

### 🔄 Sincronización
| Flujo | Path | Método | Descripción |
|-------|------|--------|-------------|
| 14 - Sync BBDD a Google Sheets | `sync-db-to-sheets` | - | Sincronización con Google Sheets |

---

## 🔗 Shared Workflows

Flujos compartidos entre módulos.

### ⚠️ Manejo de Errores
| Flujo | Path | Descripción |
|-------|------|-------------|
| 12 - Shared Error Handler | - | Detección y Envío de Alerta de Errores |

---

## 📝 Notas Técnicas

- **Estado**: Todos los flujos listados se encuentran ✅ ACTIVOS
- **Formato de Paths**: Los paths están organizados siguiendo la estructura RESTful
- **Nomenclatura**: Los flujos numerados (01-, 02-, etc.) indican secuencia lógica o versión
- **Shared Workflows**: El Error Handler es un flujo global sin endpoint específico

---

## 🔄 Última Actualización

*Fecha: [27/02/2026]*  
*Versión: 1.0*  
*Responsable: [Daniel Vargas]*