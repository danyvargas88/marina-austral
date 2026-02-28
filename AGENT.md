# AGENT.md - Marina Austral S.A - Portal de Proveedores

## 📋 Información General del Proyecto

**Cliente:** Marina Austral S.A  
**Tipo:** Portal de Proveedores (B2B)  
**Tecnologías:** PHP, JavaScript, CSS, HTML, N8N (Automatización)  
**Fecha de inicio de conversación:** 2026-02-27

---

## 🎯 Propósito del Proyecto

Desarrollo de un portal web para la gestión de proveedores de Marina Austral S.A, que permite:
- Autenticación de proveedores
- Gestión administrativa (panel admin)
- Superadministración de facturas, usuarios y logs
- Recuperación de contraseñas
- Gestión de adjuntos/documentos
- **Automatización de procesos mediante N8N**

---

## 🏗️ Estructura del Proyecto

### Archivos de Documentación Relacionados

&gt; **IMPORTANTE:** Para detalles específicos de estructuras, consultar:
&gt; - **Base de Datos:** Ver archivo `ESTRUCTURA_DB.md`
&gt; - **Estructura del Portal/Sitio Web:** Ver archivo `ESTRUCTURA_PORTAL.md`
&gt; - **Flujos de Automatización N8N:** Ver archivo `FLUJOS_N8N.md`

### Directorios Principales

/
├── admin/          # Panel de administración
│   ├── api/        # Endpoints de admin (sesiones, logout)
│   ├── assets/     # Favicon y logo
│   └── *.js, *.php, *.css  # App principal, auth, estilos
├── api/            # API general (auth, password, sesiones)
├── assets/         # Recursos estáticos (favicon, logo)
├── superadmin/     # Panel de superadministración
│   ├── css/        # Estilos específicos
│   └── js/         # Módulos: auth, dashboard, facturas, logs, proveedores, usuarios
└── [root files]    # Archivos principales del portal


### Archivos Clave Identificados

| Categoría | Archivos |
|-----------|----------|
| **Autenticación** | `login.php`, `auth.js`, `auth-proveedores.js`, `admin/auth.js`, `superadmin/js/auth.js` |
| **APIs** | `api/create-session.php`, `api/logout.php`, `api/cambiar-password.php`, `api/reset-password.php`, etc. |
| **Recuperación Password** | `recuperar-password.php`, `reset-password.php`, `solicitar-reset.php`, `validar-token.php` |
| **Aplicación Principal** | `app.js`, `index.php`, `styles.css` |
| **Admin** | `admin/app.js`, `admin/index.php`, `admin/login.php`, `admin/password.php` |
| **Superadmin** | `superadmin/index.html`, `superadmin/login.html`, `superadmin/facturas.html`, `superadmin/logs.html`, `superadmin/proveedores.html`, `superadmin/usuarios.html` |
| **Adjuntos** | `adjuntos.js` |
| **Explorador** | `explorar.php` |

---

## 🔐 Sistema de Autenticación

### Flujos Identificados

1. **Login de Proveedores:** `login.php` → `api/create-session.php`
2. **Login de Admin:** `admin/login.php` → `admin/api/create-admin-session.php`
3. **Login de Superadmin:** `superadmin/login.html` → `superadmin/js/auth.js`
4. **Recuperación de Password:**
   - `recuperar-password.php` → `api/solicitar-reset.php`
   - `reset-password.php` → `api/validar-token.php` → `api/reset-password.php`
   - `api/cambiar-password.php` (cambio directo)

### Módulos JavaScript de Auth

- `auth-proveedores.js` (12,859 bytes) - Autenticación de proveedores
- `admin/auth.js` (8,641 bytes) - Autenticación de administradores
- `superadmin/js/auth.js` (2,448 bytes) - Autenticación de superadmin

---

## 🖥️ Interfaz de Usuario

### Paneles Identificados

| Panel | Archivo Principal | Archivos de Soporte |
|-------|-------------------|---------------------|
| **Portal Proveedores** | `index.php` | `app.js`, `styles.css` |
| **Administración** | `admin/index.php` | `admin/app.js`, `admin/styles.css` |
| **Superadmin** | `superadmin/index.html` | `superadmin/js/dashboard.js`, `superadmin/css/superadmin.css` |

### Módulos del Superadmin

- **Dashboard:** `superadmin/js/dashboard.js`
- **Facturas:** `superadmin/js/facturas.js` + `superadmin/facturas.html`
- **Logs:** `superadmin/js/logs.js` + `superadmin/logs.html`
- **Proveedores:** `superadmin/js/proveedores.js` + `superadmin/proveedores.html`
- **Usuarios:** `superadmin/js/usuarios.js` + `superadmin/usuarios.html`
- **Configuración:** `superadmin/js/config.js`

---

## ⚙️ Automatización con N8N

&gt; **📄 Documentación completa:** Ver archivo **`FLUJOS_N8N.md`** para detalle de todos los flujos de trabajo activos.

### Módulos de Automatización

| Módulo | Descripción |
|--------|-------------|
| **Super Admin** | Gestión de facturas, usuarios, proveedores, logs y dashboard |
| **Proveedores API** | Endpoints para portal de proveedores (login, facturas, OCR, adjuntos) |
| **Admin Dashboard** | APIs para panel admin y sincronización con Google Sheets |
| **Shared Workflows** | Manejo centralizado de errores |

### Flujos Destacados

- 🔐 **Autenticación:** Login para proveedores, admin y superadmin
- 📄 **Facturas:** CRUD de facturas, subida con OCR, gestión de estados
- 📁 **Archivos:** Integración con Google Drive para comprobantes
- 🔄 **Sincronización:** Sync automática BBDD ↔ Google Sheets
- ⚠️ **Monitoreo:** Sistema de detección y alerta de errores

---

## ⚠️ Notas y Advertencias

### Archivos a Revisar

| Archivo | Nota |
|---------|------|
| `api/config-BORRAR!.php` | **URGENTE:** Archivo marcado para eliminación (posiblemente contiene credenciales) |
| `app(1).js` vs `app.js` | Versiones duplicadas - verificar cuál es la actual |
| `index(1).php` vs `index.php` | Versiones duplicadas - consolidar |
| `admin/app(1).js` vs `admin/app.js` | Versiones duplicadas en admin |
| `admin/index(1).php` vs `admin/index.php` | Versiones duplicadas en admin |
| `admin/styles(1).css` vs `admin/styles.css` | Versiones duplicadas de estilos |
| `superadmin/js/proveedores(1).js` vs `superadmin/js/proveedores.js` | Versiones duplicadas |

---

## 🗄️ Base de Datos

&gt; **Nota:** La estructura detallada de la base de datos se encuentra en el archivo **`ESTRUCTURA_DB.md`**.

Tablas esperadas (basado en funcionalidades):
- Proveedores
- Usuarios/Administradores
- Facturas
- Logs de actividad
- Tokens de recuperación de password
- Sesiones

---

## ✅ Funcionalidades Pendientes/Identificadas

- [ ] Limpiar archivos duplicados (versiones con "(1)")
- [ ] Eliminar `api/config-BORRAR!.php` o mover credenciales a variables de entorno
- [ ] Verificar consistencia entre versiones de archivos JS/CSS/PHP
- [ ] Documentar endpoints de API
- [ ] Revisar sistema de adjuntos (`adjuntos.js`, `explorar.php`)

---

## 💬 Contexto de Desarrollo

**Conversación actual:** El usuario solicitó convertir un JSON de estructura de archivos a formato Markdown, lo que indica que estamos en proceso de documentación del proyecto.

**Próximos pasos sugeridos:**
1. Consolidar archivos duplicados
2. Completar documentación técnica
3. Revisar seguridad de credenciales
4. Estandarizar estructura de directorios

---

## 📁 Archivos de Estructura

- `ESTRUCTURA_PORTAL.md` - Contiene el árbol completo de archivos y directorios del portal (generado desde JSON)
- `ESTRUCTURA_DB.md` - Estructura de tablas, campos y relaciones de la base de datos
- **`FLUJOS_N8N.md`** - **Documentación completa de flujos de automatización N8N**

---

*última actualización: 2026-02-27*
*Generado por asistente AI - Mantener sincronizado con cambios del proyecto*
