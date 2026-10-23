# Proposal

## Why

El Centro de Medicina Nuclear y Radioterapia (CEMENURNK) requiere ampliar su alcance internacional ofreciendo su sitio web en idioma alemán, y mejorar la experiencia de usuario garantizando que cualquier nuevo visitante pueda seleccionar explícitamente su idioma preferido al ingresar, evitando depender únicamente de la detección automática del navegador. Además, se requiere actualizar y simplificar la sección de representantes institucionales.

## What Changes

- **Soporte para Idioma Alemán (`de`)**:
  - Incorporación de traducciones completas al alemán en el diccionario `translations` para todas las secciones de la página (institucional, servicios oncológicos, aceleradores Elekta, braquiterapia, ciclotrón, representantes, contacto y pie de página).
  - Configuración del mapa embebido localizado para alemán y textos descriptivos de las imágenes del carrusel.
- **Modal de Selección de Idioma al Ingresar**:
  - Implementación de un modal centrado y accesible que aparece en la primera visita cuando no existe una preferencia guardada en `localStorage`.
  - Presentación de opciones claras con banderas y nombres de idiomas nativos: Español (🇪🇸), English (🇬🇧), 中文 (🇨🇳), Deutsch (🇩🇪).
  - Persistencia de la elección en `localStorage` para evitar mostrar el modal en visitas posteriores.
- **Selector de Idioma en el Navbar (Dropdown)**:
  - Reemplazo del botón toggle cíclico por un menú desplegable (dropdown) que muestra el idioma actual y permite cambiar directamente a cualquiera de los cuatro idiomas soportados en un solo clic.
- **Simplificación de la Sección Representantes**:
  - Modificación de la sección de representantes para exhibir únicamente la tarjeta del CEO (Martín Mutuberria), adaptando el contenedor para centrar su presentación y removiendo los demás representantes.

## Capabilities

### New Capabilities
- `localization`: Gestión integral de idiomas disponibles (español, inglés, chino y alemán), persistencia de preferencias de usuario en almacenamiento local, modal de bienvenida interactivo y menú de selección directa en la navegación.

### Modified Capabilities
<!-- None. No existing specs were defined in the project. -->

## Impact

- **Código afectado**: Principalmente `index.html` (estructura HTML del modal, dropdown de navegación, sección de representantes, clases de Tailwind CSS y lógica JavaScript para persistencia y renderizado de traducciones).
- **Almacenamiento del cliente**: Uso de `localStorage` (`cemenurnk_language`) para recordar la preferencia del usuario.
- **APIs y dependencias externas**: Sin dependencias adicionales; se mantiene con Tailwind CSS vía CDN y Vanilla JavaScript.
