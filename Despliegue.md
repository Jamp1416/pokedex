# Guía de Despliegue: Pokedex en Azure Static Web Apps

## Introducción

Este documento detalla el proceso completo para desplegar la aplicación web Pokedex en Azure Static Web Apps utilizando GitHub como repositorio de código fuente. El proceso implementa un flujo de integración y despliegue continuo (CI/CD) que permite que cada cambio en el código se refleje automáticamente en la aplicación publicada.

## Prerrequisitos

### 1. Cuentas necesarias
- *Cuenta de Azure*: Preferiblemente Azure for Students para aprovechar los créditos gratuitos
- *Cuenta de GitHub*: Para alojar el código fuente y conectarlo con Azure

### 2. Herramientas
- Git instalado localmente
- Un editor de código (como Visual Studio Code)

## Nomenclatura en Azure

Para mantener un estándar profesional, se utilizará la siguiente nomenclatura:

- *Grupo de recursos*: rg-pokedex-prod
- *Static Web App*: swa-pokedex-portal-prod-[TUS-INICIALES]

## Proceso de Despliegue

### Paso 1: Hacer un Fork del Repositorio

1. Accede al repositorio original: [https://github.com/Jamp1416/pokedex.git](https://github.com/Jamp1416/pokedex.git)
2. Haz clic en el botón *Fork* en la esquina superior derecha
3. Selecciona tu cuenta de GitHub como destino del fork
4. Espera a que el proceso de bifurcación termine (verás una pantalla de "Forking Jamp1416/pokedex")
5. Una vez completado, serás redirigido a tu nueva copia en: https://github.com/[tu-usuario]/pokedex

### Paso 2: Crear una Static Web App en Azure

1. Inicia sesión en el [Portal de Azure](https://portal.azure.com)
2. En la barra de búsqueda superior, escribe "Static Web Apps" y selecciona el servicio
3. Haz clic en *Crear*
4. Completa los datos del formulario:
   - *Suscripción*: Selecciona tu suscripción de Azure (Azure for Students)
   - *Grupo de recursos*: Crea nuevo rg-pokedex-prod
   - *Nombre*: swa-pokedex-portal-prod-[TUS-INICIALES]
   - *Plan de hospedaje*: Free
   - *Región*: No es necesario seleccionar (el contenido se distribuye mediante CDN)

### Paso 3: Conectar con GitHub y Configurar el Despliegue

1. En la sección *Origen de implementación*:
   - Selecciona *GitHub*
   - Autentica tu cuenta de GitHub si es necesario
   - *Organización*: Tu usuario de GitHub
   - *Repositorio*: pokedex
   - *Rama*: main (o master según corresponda)

2. Configuración de compilación:
   - *Tipo de aplicación*: 
     - Si la aplicación es HTML/CSS puro: selecciona *Personalizado (Custom)*
     - Si usa React/Vue/Angular: selecciona el framework correspondiente 
   - *Ubicación del código de la aplicación*: / (o la carpeta donde se encuentra el código fuente)
   - *Ubicación de compilación*: 
     - Si es HTML/CSS puro: . (punto)
     - Si usa un framework JavaScript: dist/ o build/ según corresponda

3. Haz clic en *Revisar + crear* y luego en *Crear*
4. Espera unos minutos mientras Azure crea la aplicación

### Paso 4: Verificar el Despliegue

1. Una vez completada la implementación, ve a la sección *Static Web Apps* en el Portal de Azure
2. Selecciona tu aplicación recién creada
3. En la parte superior derecha, encontrarás la *URL* generada para tu aplicación
4. Copia esta URL y ábrela en tu navegador
5. Verifica que la aplicación Pokedex cargue correctamente

### Paso 5: Verificar el Despliegue Automático (GitHub Actions)

1. Ve a tu repositorio de GitHub (https://github.com/[tu-usuario]/pokedex)
2. Haz clic en la pestaña *Actions* en el menú superior
3. Deberías ver un workflow llamado "Azure Static Web Apps CI/CD"
4. Verifica que el estado sea verde (✓) indicando que el despliegue fue exitoso
5. Si hay errores (❌), revisa los logs para identificar y solucionar el problema

### Paso 6: Realizar Cambios y Verificar el CI/CD

Para probar que el despliegue automático funciona correctamente:

1. Clona tu repositorio localmente:
   bash
   git clone https://github.com/[tu-usuario]/pokedex.git
   cd pokedex
   

2. Realiza un cambio en el código (por ejemplo, modifica algún texto en el HTML):
   bash
   # Abre el archivo principal (index.html u otro) en tu editor
   # Realiza algún cambio visible
   

3. Sube los cambios a GitHub:
   bash
   git add .
   git commit -m "Actualización de texto en la página principal"
   git push origin main
   

4. Verifica en GitHub Actions (pestaña Actions) que se inicie automáticamente un nuevo workflow
5. Espera a que finalice el despliegue (2-3 minutos)
6. Refresca la URL de tu aplicación y verifica que los cambios sean visibles

## Seguridad: Método para Commits en Computadores Compartidos

Si estás usando equipos públicos o compartidos, recomendamos usar un token de acceso personal (PAT) de GitHub para evitar almacenar tus credenciales:

### Crear un Token de Acceso Personal (PAT)

1. Ve a [https://github.com/settings/personal-access-tokens](https://github.com/settings/personal-access-tokens)
2. Haz clic en *Generate new token* (Generar nuevo token)
3. Configura el token:
   - *Nombre*: Pokedex-Lab-Access-[Fecha]
   - *Expiración*: 1-7 días
   - *Alcance de repositorio*: "Only select repositories" → selecciona solo tu repositorio pokedex
   - *Permisos*:
     - Contents: Read & Write
     - Metadata: Read-only
     - Pull Requests: Read & Write
4. Haz clic en *Generate token*
5. *IMPORTANTE*: Copia el token generado inmediatamente (no se volverá a mostrar)

### Configurar Git para Usar el Token

Dentro de la carpeta del proyecto clonado:

bash
# Configurar identidad local (solo para este repositorio)
git config --local user.name "[tu-nombre]"
git config --local user.email "[tu-email]"

# Usar el token en la URL remota
git remote set-url origin https://[TU_TOKEN]@github.com/[tu-usuario]/pokedex.git

# Verificar la configuración
git remote -v
git config --local --list
