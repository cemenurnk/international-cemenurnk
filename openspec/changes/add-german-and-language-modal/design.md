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
    - Español (🇪🇸 España / 🇦🇷 Argentina)
    - English (🇬🇧 Reino Unido / 🇺🇸 EE.UU.)
    - 中文 (🇨🇳 China)
    - Deutsch (🇩🇪 Alemania)
  - Al hacer clic en cualquier opción, se invoca `updateLanguage(lang)`, se guarda en `localStorage` y se oculta el modal agregando la clase `hidden`.

### 3. Rediseño del selector del Navbar a Dropdown
- **Decisión**: Crear un contenedor relativo en el navbar con:
  - Botón disparador que muestra la bandera gráfica y código del idioma actual más un icono indicador (chevron).
  - Menú desplegable flotante con las 4 opciones de idioma acompañadas de sus banderas gráficas.
  - Evento de cierre al hacer clic fuera del dropdown (`document.addEventListener('click')`).

### 4. Banderas gráficas vectoriales / SVG
- **Decisión**: Para evitar que en Windows los emojis de banderas se muestren como letras de código de país en blanco y negro, se incorporan banderas gráficas SVG limpias (utilizando SVGs vectoriales integrados con dimensiones consistentes `w-6 h-4` o `w-7 h-5` con esquinas redondeadas suaves y bordes sutiles).

### 5. Estandarización de Imágenes en Tarjetas
- **Decisión**:
  - En **Servicios**: Convertir las tarjetas a `flex flex-col justify-between h-full` con contenedor de imagen `w-full h-48 overflow-hidden rounded-xl mt-4` e imagen con `w-full h-full object-cover`.
  - En **Equipamiento**: Convertir las tarjetas a `flex flex-col justify-between h-full` con contenedor de imagen `w-full h-52 overflow-hidden rounded-xl mt-4` e imagen con `w-full h-full object-cover`.
  - En **Quiénes Somos**: Asegurar que la imagen `equipo1.png` mantenga una altura y aspecto proporcional equilibrado con el bloque de texto contiguo.
  - En **Ciclotrón**: Ajustar `ciclotron.jpg` a `w-full h-80 object-cover rounded-xl shadow-lg`.
  - En **Representantes**: La imagen del CEO con `w-48 h-48 rounded-full object-cover mx-auto`.

## Risks / Trade-offs

- **[Navegación privada o `localStorage` deshabilitado]** → Mitigación: Proteger llamadas a `localStorage` dentro de bloques `try/catch`.
- **[Imágenes con diferentes relaciones de aspecto originales]** → Mitigación: El uso de `object-cover` junto a un contenedor con dimensiones fijas garantiza que ninguna imagen se deforme (manteniendo proporción) y que todas las tarjetas mantengan simetría exacta en el grid.
