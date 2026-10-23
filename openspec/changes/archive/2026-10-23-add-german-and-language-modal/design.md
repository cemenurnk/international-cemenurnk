# Design

## Context

El sitio web está implementado como una aplicación web estática contenida en `index.html`, estilizada con Tailwind CSS (vía CDN) y dinamismo en JavaScript nativo. Actualmente cuenta con un objeto literal `translations` con claves para `es`, `zh` y `en`. La detección inicial se realizaba a través de `navigator.language` sin persistencia en el navegador, y el cambio de idioma dependía de un botón único que cicla secuencialmente.

Véase `proposal.md` y `specs/localization/spec.md` para la motivación y requerimientos detallados.

## Goals / Non-Goals

**Goals:**
- Extender el objeto `translations` con el idioma alemán (`de`) para todos los textos, atributos `alt` y recursos visuales/mapas.
- Crear un componente modal centrado con Tailwind CSS para la selección inicial de idioma en la primera visita.
- Persistir la preferencia de idioma en `localStorage` bajo la clave `cemenurnk_language`.
- Reemplazar el botón cíclico del navbar por un menú desplegable (dropdown) que muestre el idioma activo y permita cambiar a cualquiera de los 4 idiomas con un solo clic.
- Simplificar la sección de representantes para mostrar únicamente al CEO (Martín Mutuberria) en un diseño centrado y limpio.
- Incorporar banderas gráficas vectoriales/SVG de países referentes para evitar el problema de emojis no soportados en Windows.
- Estandarizar la disposición y dimensiones de las imágenes en toda la página (Servicios, Equipamiento, Institucional, Ciclotrón) para lograr simetría y coherencia visual en las tarjetas.
- Transformar la sección de encabezado para que el carrusel ocupe todo el ancho y alto de la pantalla (`w-full h-screen`), manteniendo la barra de navegación visible en la parte superior y colocando el título y subtítulo sobre el carrusel en letras blancas con alto contraste.
- Mantener compatibilidad total sin agregar dependencias ni herramientas de compilación externas.

**Non-Goals:**
- No se incorporarán bibliotecas externas pesadas; se mantendrá la arquitectura ligera en Vanilla JS y Tailwind CDN.
- No se requiere backend ni persistencia en base de datos remota.

## Decisions

### 1. Persistencia y ciclo de vida de carga
- **Decisión**: Utilizar `localStorage.getItem('cemenurnk_language')`.
  - Si existe un valor válido (`es`, `en`, `zh`, `de`), se aplica inmediatamente al cargar la página (`window.addEventListener('DOMContentLoaded')`).
  - Si no existe (primera visita o almacenamiento limpio), se detecta el idioma del navegador como fallback visual preliminar y se despliega el modal de bienvenida.
  - Al seleccionar un idioma en el modal o en el navbar, se ejecuta `localStorage.setItem('cemenurnk_language', lang)` y se actualiza la interfaz.

### 2. Estructura y comportamiento del Modal de Bienvenida
- **Decisión**: Modal con superposición (`fixed inset-0 bg-black/60 z-50 flex items-center justify-center p-4`).
  - Tarjeta con diseño limpio y bienvenida multilingüe.
  - Cuatro botones con banderas gráficas SVG/vectoriales nítidas y nombres nativos:
    - Español (🇪🇸 España)
    - English (🇬🇧 Reino Unido)
    - 中文 (🇨🇳 China)
    - Deutsch (🇩🇪 Alemania)
  - Al hacer clic en cualquier opción, se invoca `updateLanguage(lang)`, se guarda en `localStorage` y se oculta el modal agregando la clase `hidden`.

### 3. Rediseño del selector del Navbar a Dropdown
- **Decisión**: Crear un contenedor relativo en el navbar con:
  - Botón disparador que muestra la bandera gráfica y código del idioma actual más un icono indicador (chevron).
  - Menú desplegable flotante con las 4 opciones de idioma acompañadas de sus banderas gráficas.
  - Evento de cierre al hacer clic fuera del dropdown (`document.addEventListener('click')`).

### 4. Banderas gráficas vectoriales / SVG
- **Decisión**: Para evitar que en Windows los emojis de banderas se muestren como letras de código de país en blanco y negro, se incorporan banderas gráficas SVG limpias integradas en el DOM con dimensiones consistentes y bordes sutiles.

### 5. Estandarización de Imágenes en Tarjetas
- **Decisión**:
  - En **Servicios**: Convertir las tarjetas a `flex flex-col justify-between h-full` con contenedor de imagen `w-full h-48 overflow-hidden rounded-xl mt-4` e imagen con `w-full h-full object-cover`.
  - En **Equipamiento**: Convertir las tarjetas a `flex flex-col justify-between h-full` con contenedor de imagen `w-full h-52 overflow-hidden rounded-xl mt-4` e imagen con `w-full h-full object-cover`.
  - En **Quiénes Somos**: Asegurar que la imagen `equipo1.png` mantenga una altura y aspecto proporcional equilibrado.
  - En **Ciclotrón**: Ajustar `ciclotron.jpg` con contenedor proporcional estilizado.
  - En **Representantes**: La imagen del CEO con `w-48 h-48 rounded-full object-cover mx-auto ring-4`.

### 6. Carrusel Hero a Pantalla Completa con Títulos Superpuestos
- **Decisión**:
  - Encabezado (`<header>`): Dimensiones `relative w-full h-screen min-h-[600px] overflow-hidden`.
  - Carrusel (`#hero-carousel`): Ocupa toda la superficie de fondo (`absolute inset-0 w-full h-full`). Cada elemento del carrusel renderiza imágenes a sangrado total (`w-full h-full object-cover`).
  - Capa de contraste (Overlay): Capa oscura con degradado (`absolute inset-0 bg-gradient-to-b from-black/60 via-black/40 to-black/75 z-10 pointer-events-none`).
  - Contenido institucional superpuesto: Contenedor centrado (`relative z-20 h-full flex flex-col items-center justify-center px-6 text-center pt-20`). Títulos en tipografía blanca (`text-white`) con sombra pronunciada (`drop-shadow-2xl`) para visibilidad óptima sobre cualquier imagen del carrusel.
  - Barra de navegación (`<nav>`): Se mantiene en la parte superior fija (`fixed top-0 left-0 right-0 z-50`) con fondo blanco translúcido (`bg-white/95 backdrop-blur-md shadow-md`) garantizando visibilidad continua.
  - Indicadores de carrusel (Dots): Ubicados en la parte inferior central (`absolute bottom-8 left-1/2 -translate-x-1/2 z-30`).

## Risks / Trade-offs

- **[Contraste de texto sobre imágenes claras]** → Mitigación: El degradado oscuro semitransparente (`bg-gradient-to-b from-black/60 via-black/40 to-black/75`) y `drop-shadow-2xl` aseguran legibilidad perfecta independientemente de la luminosidad de la foto activa.
- **[Navegación móvil con altura `100vh`]** → Mitigación: Uso de `h-screen min-h-[600px]` asegurando que en pantallas móviles o con barras de navegación móviles el contenido no quede cortado.
