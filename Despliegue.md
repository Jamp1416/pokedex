# Guía de Despliegue: Pokedex en Azure Static Web Apps

## Introducción

Este documento te guiará paso a paso para desplegar la aplicación web Pokedex en Azure Static Web Apps, utilizando GitHub como repositorio de código fuente. Implementaremos un flujo de integración y despliegue continuo (CI/CD) que permitirá que cada cambio en el código se refleje automáticamente en la aplicación publicada.

## Prerrequisitos

### 1. Cuentas necesarias
- **Cuenta de Azure**: Te recomiendo usar Azure for Students para aprovechar los créditos gratuitos.
- **Cuenta de GitHub**: Necesitarás una cuenta para alojar el código fuente y conectarlo con Azure.

### 2. Herramientas
- Git instalado localmente.
- Un editor de código (como Visual Studio Code) para realizar modificaciones.

## Nomenclatura en Azure

Para mantener un estándar profesional, utilizaremos la siguiente nomenclatura:
- **Grupo de recursos**: `jm-pokedex-prod`
- **Static Web App**: `swa-pokedex-portal-prod-jm`

## Proceso de Despliegue

### Paso 1: Hacer un Fork del Repositorio

1. Accede al [repositorio original](https://github.com/Jamp1416/pokedex.git).
2. Haz clic en el botón **Fork** en la esquina superior derecha.
3. Selecciona tu cuenta de GitHub como destino del fork.
4. Espera a que el proceso de bifurcación termine (verás una pantalla de "Forking Jamp1416/pokedex").
5. Una vez completado, serás redirigido a tu nueva copia en: [https://github.com/Jamp1416/pokedex](https://github.com/Jamp1416/pokedex).

### Paso 2: Crear una Static Web App en Azure

1. Inicia sesión en el [Portal de Azure](https://portal.azure.com).
2. En la barra de búsqueda superior, escribe "Static Web Apps" y selecciona el servicio.
3. Haz clic en **Crear**.
4. Completa los datos del formulario:
   - **Suscripción**: Selecciona tu suscripción de Azure (Azure for Students).
   - **Grupo de recursos**: Crea uno nuevo llamado `jm-pokedex-prod`.
   - **Nombre**: `swa-pokedex-portal-prod-jm`.
   - **Plan de hospedaje**: Free.
   - **Región**: No es necesario seleccionar (el contenido se distribuye mediante CDN).

### Paso 3: Conectar con GitHub y Configurar el Despliegue

1. En la sección **Origen de implementación**:
   - Selecciona **GitHub**.
   - Autentica tu cuenta de GitHub si es necesario.
   - **Organización**: Tu usuario de GitHub.
   - **Repositorio**: `pokedex`.
   - **Rama**: `master` (o `main` según corresponda).
2. **Configuración de compilación**:
   - **Tipo de aplicación**:
     - Si la aplicación es HTML/CSS puro: selecciona **Personalizado (Custom)**.
     - Si usa React/Vue/Angular: selecciona el framework correspondiente.
   - **Ubicación del código de la aplicación**: `/` (o la carpeta donde se encuentra el código fuente).
   - **Ubicación de compilación**:
     - Si es HTML/CSS puro: `.` (punto).
     - Si usa un framework JavaScript: `dist/` o `build/` según corresponda.
3. Haz clic en **Revisar + crear** y luego en **Crear**.
4. Espera unos minutos mientras Azure crea la aplicación.

### Paso 4: Verificar el Despliegue

1. Una vez completada la implementación, ve a la sección **Static Web Apps** en el Portal de Azure.
2. Selecciona tu aplicación recién creada.
3. En la parte superior derecha, encontrarás la **URL** generada para tu aplicación.
4. Copia esta URL y ábrela en tu navegador.
5. Verifica que la aplicación Pokedex cargue correctamente.
6. Revisa la seguridad de tu aplicación utilizando herramientas como [SecurityHeaders.com](https://securityheaders.com/) para asegurarte de que los encabezados de seguridad están correctamente configurados como en mi caso dio A.

### Paso 5: Verificar el Despliegue Automático (GitHub Actions)

1. Ve a tu repositorio de GitHub https://github.com/Jamp1416/pokedex.
2. Haz clic en la pestaña **Actions** en el menú superior.
3. Deberías ver un workflow llamado "Azure Static Web Apps CI/CD".
4. Verifica que el estado sea verde (✓) indicando que el despliegue fue exitoso.
5. Si hay errores (❌), revisa los logs para identificar y solucionar el problema.








