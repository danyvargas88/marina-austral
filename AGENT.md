# AGENT.md - Marina Austral S.A - Portal de Proveedores

## 馃搵 Informaci贸n General del Proyecto

**Cliente:** Marina Austral S.A  
**Tipo:** Portal de Proveedores (B2B)  
**Tecnolog铆as:** PHP, JavaScript, CSS, HTML  
**Fecha de inicio de conversaci贸n:** 2026-02-27

---

## 馃幆 Prop贸sito del Proyecto

Desarrollo de un portal web para la gesti贸n de proveedores de Marina Austral S.A, que permite:
- Autenticaci贸n de proveedores
- Gesti贸n administrativa (panel admin)
- Superadministraci贸n de facturas, usuarios y logs
- Recuperaci贸n de contrase帽as
- Gesti贸n de adjuntos/documentos

---

## 馃搧 Estructura del Proyecto

### Archivos de Documentaci贸n Relacionados

&gt; **IMPORTANTE:** Para detalles espec铆ficos de estructuras, consultar:
&gt; - **Base de Datos:** Ver archivo `ESTRUCTURA_DB.md`
&gt; - **Estructura del Portal/Sitio Web:** Ver archivo `ESTRUCTURA_PORTAL.md`

### Directorios Principales

/
鈹溾攢鈹€ admin/          # Panel de administraci贸n
鈹?  鈹溾攢鈹€ api/        # Endpoints de admin (sesiones, logout)
鈹?  鈹溾攢鈹€ assets/     # Favicon y logo
鈹?  鈹斺攢鈹€ *.js, *.php, *.css  # App principal, auth, estilos
鈹溾攢鈹€ api/            # API general (auth, password, sesiones)
鈹溾攢鈹€ assets/         # Recursos est谩ticos (favicon, logo)
鈹溾攢鈹€ superadmin/     # Panel de superadministraci贸n
鈹?  鈹溾攢鈹€ css/        # Estilos espec铆ficos
鈹?  鈹斺攢鈹€ js/         # M贸dulos: auth, dashboard, facturas, logs, proveedores, usuarios
鈹斺攢鈹€ [root files]    # Archivos principales del portal


### Archivos Clave Identificados

| Categor铆a | Archivos |
|-----------|----------|
| **Autenticaci贸n** | `login.php`, `auth.js`, `auth-proveedores.js`, `admin/auth.js`, `superadmin/js/auth.js` |
| **APIs** | `api/create-session.php`, `api/logout.php`, `api/cambiar-password.php`, `api/reset-password.php`, etc. |
| **Recuperaci贸n Password** | `recuperar-password.php`, `reset-password.php`, `solicitar-reset.php`, `validar-token.php` |
| **Aplicaci贸n Principal** | `app.js`, `index.php`, `styles.css` |
| **Admin** | `admin/app.js`, `admin/index.php`, `admin/login.php`, `admin/password.php` |
| **Superadmin** | `superadmin/index.html`, `superadmin/login.html`, `superadmin/facturas.html`, `superadmin/logs.html`, `superadmin/proveedores.html`, `superadmin/usuarios.html` |
| **Adjuntos** | `adjuntos.js` |
| **Explorador** | `explorar.php` |

---

## 馃攼 Sistema de Autenticaci贸n

### Flujos Identificados

1. **Login de Proveedores:** `login.php` 鈫?`api/create-session.php`
2. **Login de Admin:** `admin/login.php` 鈫?`admin/api/create-admin-session.php`
3. **Login de Superadmin:** `superadmin/login.html` 鈫?`superadmin/js/auth.js`
4. **Recuperaci贸n de Password:**
   - `recuperar-password.php` 鈫?`api/solicitar-reset.php`
   - `reset-password.php` 鈫?`api/validar-token.php` 鈫?`api/reset-password.php`
   - `api/cambiar-password.php` (cambio directo)

### M贸dulos JavaScript de Auth

- `auth-proveedores.js` (12,859 bytes) - Autenticaci贸n de proveedores
- `admin/auth.js` (8,641 bytes) - Autenticaci贸n de administradores
- `superadmin/js/auth.js` (2,448 bytes) - Autenticaci贸n de superadmin

---

## 馃帹 Interfaz de Usuario

### Paneles Identificados

| Panel | Archivo Principal | Archivos de Soporte |
|-------|-------------------|---------------------|
| **Portal Proveedores** | `index.php` | `app.js`, `styles.css` |
| **Administraci贸n** | `admin/index.php` | `admin/app.js`, `admin/styles.css` |
| **Superadmin** | `superadmin/index.html` | `superadmin/js/dashboard.js`, `superadmin/css/superadmin.css` |

### M贸dulos del Superadmin

- **Dashboard:** `superadmin/js/dashboard.js`
- **Facturas:** `superadmin/js/facturas.js` + `superadmin/facturas.html`
- **Logs:** `superadmin/js/logs.js` + `superadmin/logs.html`
- **Proveedores:** `superadmin/js/proveedores.js` + `superadmin/proveedores.html`
- **Usuarios:** `superadmin/js/usuarios.js` + `superadmin/usuarios.html`
- **Configuraci贸n:** `superadmin/js/config.js`

---

## 鈿狅笍 Notas y Advertencias

### Archivos a Revisar

| Archivo | Nota |
|---------|------|
| `api/config-BORRAR!.php` | **URGENTE:** Archivo marcado para eliminaci贸n (posiblemente contiene credenciales) |
| `app(1).js` vs `app.js` | Versiones duplicadas - verificar cu谩l es la actual |
| `index(1).php` vs `index.php` | Versiones duplicadas - consolidar |
| `admin/app(1).js` vs `admin/app.js` | Versiones duplicadas en admin |
| `admin/index(1).php` vs `admin/index.php` | Versiones duplicadas en admin |
| `admin/styles(1).css` vs `admin/styles.css` | Versiones duplicadas de estilos |
| `superadmin/js/proveedores(1).js` vs `superadmin/js/proveedores.js` | Versiones duplicadas |

---

## 馃梽锔?Base de Datos

> **Nota:** La estructura detallada de la base de datos se encuentra en el archivo **`ESTRUCTURA_DB.md`**.

Tablas esperadas (basado en funcionalidades):
- Proveedores
- Usuarios/Administradores
- Facturas
- Logs de actividad
- Tokens de recuperaci贸n de password
- Sesiones

---

## 馃摓 Contexto de Desarrollo

**Conversaci贸n actual:** El usuario solicit贸 convertir un JSON de estructura de archivos a formato Markdown, lo que indica que estamos en proceso de documentaci贸n del proyecto.

**Pr贸ximos pasos sugeridos:**
1. Consolidar archivos duplicados
2. Completar documentaci贸n t茅cnica
3. Revisar seguridad de credenciales
4. Estandarizar estructura de directorios

---

## 馃摎 Archivos de Estructura

- `ESTRUCTURA_PORTAL.md` - Contiene el 谩rbol completo de archivos y directorios del portal (generado desde JSON)
- `ESTRUCTURA_DB.md` - Estructura de tablas, campos y relaciones de la base de datos
- `FLUJOS_N8N.md` - Listado de flujos y paths relacionados a la estructura de n8n

---

*脷ltima actualizaci贸n: 2026-02-27*
*Generado por asistente AI - Mantener sincronizado con cambios del proyecto*
