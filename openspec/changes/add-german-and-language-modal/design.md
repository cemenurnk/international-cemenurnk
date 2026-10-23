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
- Mantener compatibilidad total sin agregar dependencias ni herramientas de compilación externas.

**Non-Goals:**
- No se incorporarán bibliotecas externas de internacionalización (como i18next) ni frameworks de frontend; se mantendrá la arquitectura ligera en Vanilla JS.
- No se requiere backend ni persistencia en base de datos remota.

## Decisions

### 1. Persistencia y ciclo de vida de carga
- **Decisión**: Utilizar `localStorage.getItem('cemenurnk_language')`.
  - Si existe un valor válido (`es`, `en`, `zh`, `de`), se aplica inmediatamente al cargar la página (`window.addEventListener('DOMContentLoaded')`).
  - Si no existe (primera visita o almacenamiento limpio), se detecta el idioma del navegador como fallback visual preliminar y se despliega el modal de bienvenida.
  - Al seleccionar un idioma en el modal o en el navbar, se ejecuta `localStorage.setItem('cemenurnk_language', lang)` y se actualiza la interfaz.
- **Alternativa descartada**: Cookies de sesión o volver a preguntar en cada recarga (generaría una mala experiencia de usuario).

### 2. Estructura y comportamiento del Modal de Bienvenida
- **Decisión**: Modal con superposición (`fixed inset-0 bg-black/60 z-50 flex items-center justify-center p-4`).
  - Tarjeta con diseño limpio y bienvenida multilingüe.
  - Cuatro botones con banderas y nombres nativos:
    - 🇪🇸 Español
    - 🇬🇧 English
    - 🇨🇳 中文
    - 🇩🇪 Deutsch
  - Al hacer clic en cualquier opción, se invoca `updateLanguage(lang)`, se guarda en `localStorage` y se oculta el modal agregando la clase `hidden`.
- **Alternativa descartada**: Banner inferior flotante (descartado en la etapa de exploración a favor del modal centrado).

### 3. Rediseño del selector del Navbar a Dropdown
- **Decisión**: Crear un contenedor relativo en el navbar con:
  - Botón disparador que muestra la bandera y código del idioma actual más un icono indicador (chevron).
  - Menú desplegable flotante (`absolute right-0 mt-2 w-44 bg-white shadow-xl rounded-xl border border-gray-100 z-50 hidden`) con la lista de opciones.
  - Evento de cierre al hacer clic fuera del dropdown (`document.addEventListener('click')`).
- **Alternativa descartada**: Mantener el botón de ciclo que obligaría a dar hasta 3 clics para llegar a un idioma.

### 4. Diccionario de traducciones para Alemán (`de`)
- **Decisión**: Completar las traducciones técnicas y médicas en alemán manteniendo la coherencia terminológica (ej. *Strahlentherapie* para Radioterapia, *Bildgebende Diagnostik* para Diagnóstico por Imágenes, *Zyklotron* para Ciclotrón, etc.) y configurar el mapa de Google Maps con parámetros en alemán (`de-DE`).

### 5. Simplificación de la Sección de Representantes
- **Decisión**: Reemplazar la grilla de 3 columnas (`grid grid-cols-1 md:grid-cols-3 gap-8`) por un contenedor centrado con un ancho máximo acotado (`max-w-md mx-auto`).
  - Conservar únicamente la tarjeta de Martín Mutuberria (CEO).
  - Remover las tarjetas de Gabriel Martínez y Lucas Dórdolo de la estructura HTML.

## Risks / Trade-offs

- **[Navegación privada o `localStorage` deshabilitado]** → Mitigación: Proteger llamadas a `localStorage` dentro de bloques `try/catch` para evitar excepciones en modos de navegación con almacenamiento bloqueado, recurriendo en ese caso a memoria de sesión/fallback.
- **[Superposición en pantallas móviles]** → Mitigación: Configurar z-index adecuado (`z-50`), tamaño responsivo con scroll interno si fuera necesario (`max-h-[90vh] overflow-y-auto`) y espaciado táctil cómodo.
