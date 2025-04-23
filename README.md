# Despliegue de Aplicación Web Angular usando Azure Static Web Apps

Este documento describe el procedimiento seguido para la creación y despliegue de una aplicación web desarrollada con Angular en la nube pública de Microsoft Azure. Se detallan los pasos realizados desde la creación del recurso en Azure hasta la elección de la solución de hospedaje, explicando las razones técnicas y estratégicas que justifican cada decisión.

## 1. Requisitos previos

Antes de proceder con la publicación en la nube, se contó con:

- Una suscripción activa en **Azure for Students**.
- Una aplicación desarrollada localmente con Angular.
- Repositorio en GitHub con el código fuente de la aplicación.
- Archivos de distribución (`dist/pokedex-angular`) generados y descargados mediante comandos `npm`.

## 2. Creación del recurso en la nube pública (Azure)

### Paso 1: Acceso al portal de Azure
Se accedió al [portal de Azure](https://portal.azure.com/) usando una cuenta asociada a la suscripción "Azure for Students".

### Paso 2: Selección del tipo de recurso
Se eligió el recurso **Azure Static Web Apps**, diseñado específicamente para alojar aplicaciones front-end estáticas construidas con frameworks como Angular, React o Vue, en combinación con APIs RESTful.

### Paso 3: Configuración del recurso
Durante la creación del recurso, se configuraron los siguientes elementos:

- **Nombre de la aplicación**: Nombre único para identificar la web app (`Pokedex-App-cps`).
- **Región**: La más cercana geográficamente para menor latencia (`Central US`).
- **Origen del código**: Se enlazó el repositorio de GitHub donde se encontraba el proyecto (`Testappweb-pokedex-cps`).
- **Ruta de salida**: Se especificó la carpeta `dist/pokedex-angular`, que contiene la versión compilada del proyecto Angular.

Una vez completados estos pasos, se procedió a la creación del recurso, la cual fue exitosa.

## 3. Seguridad de la aplicación
Se añadió un archivo de configuración llamado `staticwebapp.config.json` en la raíz del proyecto para incorporar políticas de seguridad HTTP mediante encabezados. Entre ellos se incluyeron:

- `Content-Security-Policy`
- `X-Frame-Options`
- `Permissions-Policy`

Esto garantiza una protección básica contra ataques comunes como clickjacking, uso indebido de permisos del navegador y carga de contenido no autorizado.

## 4. Justificación de la elección de Azure Static Web Apps
Se eligió **Azure Static Web Apps** frente a otras opciones de hospedaje (como Azure App Service, máquinas virtuales o servicios de terceros) por las siguientes razones:

- **Simplicidad de despliegue**: Permite integración continua con GitHub, automatizando el proceso desde push hasta publicación.
- **Costo cero**: El plan gratuito de Azure for Students cubre el uso básico del servicio sin necesidad de tarjetas de crédito ni cargos adicionales.
- **Rendimiento y escalabilidad**: Las aplicaciones se sirven desde puntos distribuidos globalmente (CDN), lo que reduce la latencia.
- **Compatibilidad nativa con Angular**: Azure detecta automáticamente el framework usado y configura el entorno de build adecuado.

## 5. Consideraciones adicionales

- La aplicación no cuenta con lógica de back-end propia; todo el consumo de datos se realiza mediante la API pública [PokéAPI](https://pokeapi.co/), lo cual hace aún más viable el uso de un entorno estático.
- Azure Static Web Apps incluye HTTPS automático, lo que garantiza un canal seguro sin necesidad de configuración adicional.
- La solución es adecuada para prácticas universitarias y proyectos personales por su accesibilidad, facilidad de uso y soporte académico.

---

**Nota**: Este proyecto fue implementado con fines académicos. El autor no es el creador original de la aplicación Pokédex ni de sus componentes visuales o funcionales.
