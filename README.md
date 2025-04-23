## Requisitos de Despliegue

### Prerrequisitos
1. Cuenta de Azure for Students o suscripción de Azure
2. Cuenta de GitHub
3. Git instalado localmente

### Pasos para el Despliegue

#### Paso 1: Hacer un Fork del Repositorio
1. Ve a: https://github.com/rcuello/ac4dem1a.git
2. Haz clic en "Fork" en la esquina superior derecha
3. Selecciona tu cuenta de GitHub como destino

#### Paso 2: Crear una Static Web App en Azure
1. Inicia sesión en el https://portal.azure.com
2. Busca y selecciona "Static Web Apps"
3. Haz clic en "Crear" para iniciar la creación de una nueva Static Web App
4. Completa los detalles:
   - Grupo de Recursos: `rg-pokedex-prod` (crea uno nuevo o selecciona uno existente)
   - Nombre: `swa-pokedex-portal-prod-jm`
   - Plan de hospedaje: Gratis
   - Región: (Se distribuye automáticamente mediante CDN)

#### Paso 3: Conectar con GitHub y Configurar el Despliegue
1. Selecciona GitHub como directiva de autorización de implementación
2. Vincula tu cuenta de GitHub (en este caso: Jamp1416)
3. Configura los ajustes de despliegue:
   - Organización: Tu nombre de usuario de GitHub
   - Repositorio: pokedex
   - Rama: main
4. Configuración de compilación:
   - Preset de compilación: Personalizado
   - Ubicación de la aplicación: `./sistemas-distribuidos`
   - Ubicación de la API: (dejarlo vacío)
   - Ubicación del artefacto de la aplicación: `dist/pokedex-angular`
5. Haz clic en "Revisar + Crear" y luego en "Crear"

#### Paso 4: Verificar el Despliegue
1. Una vez que se complete la implementación, ve a la sección Static Web Apps en el Portal de Azure
2. Copia la URL generada y ábrela en tu navegador
3. Verifica que la aplicación Pokedex cargue correctamente

#### Paso 5: Verificar el Despliegue Automático (GitHub Actions)
1. Ve a tu repositorio de GitHub
2. Haz clic en la pestaña "Actions"
3. Deberías ver un workflow llamado "Azure Static Web Apps CI/CD"
4. Comprueba si el despliegue fue exitoso (marca verde)



