# Tasks

## 1. Incorporación del idioma Alemán (de)

- [x] 1.1 Extender el diccionario `translations` en `index.html` con las traducciones completas al alemán (`de`) para todos los textos de navegación, secciones institucionales, equipamiento y contacto; verificar que cada clave contenga su variante `de`.
- [x] 1.2 Agregar la localización en alemán para `map-src` (Google Maps en alemán) y la colección de textos alternativos en `carousel-images` para `de`; verificar que el carrusel y el mapa carguen correctamente al seleccionar alemán.

## 2. Modal de Bienvenida para Selección de Idioma

- [x] 2.1 Añadir la estructura HTML y estilos Tailwind CSS del modal de bienvenida en `index.html`, con opciones visuales para Español (🇪🇸), English (🇬🇧), 中文 (🇨🇳) y Deutsch (🇩🇪); verificar que el contenedor se posicione correctamente en el centro de la pantalla con fondo oscurecido.
- [x] 2.2 Implementar en JavaScript la verificación de `localStorage` (`cemenurnk_language`) al cargar la página: si no existe, mostrar el modal; al pulsar un idioma, guardar la preferencia, actualizar el sitio y ocultar el modal; verificar que la preferencia quede persistida en `localStorage`.

## 3. Menú Desplegable (Dropdown) en la Barra de Navegación

- [x] 3.1 Reemplazar el botón toggle simple `#lang-toggle` en la barra de navegación por un menú desplegable (dropdown) que muestre el idioma activo actual y una lista flotante con las 4 opciones de idioma; verificar la correcta disposición responsiva con Tailwind CSS.
- [x] 3.2 Conectar la lógica de apertura/cierre del dropdown (incluyendo cierre al hacer clic fuera) y el evento de cambio de idioma que actualiza el contenido, el botón del navbar y el valor en `localStorage`; verificar que el cambio desde el dropdown actualice la vista inmediatamente.

## 4. Verificación Integral y Casos de Borde

- [x] 4.1 Validar el flujo de primera visita limpiando `localStorage` y verificando que el modal aparezca, permita elegir alemán (`de`) y traduzca todos los elementos de la página sin errores en consola.
- [x] 4.2 Validar el flujo de visita recurrente recargando la página y verificando que no se muestre el modal, conservando el idioma seleccionado previamente.

## 5. Actualización de la Sección Representantes

- [x] 5.1 Modificar la sección #representantes en index.html para conservar únicamente la tarjeta del CEO (Martín Mutuberria), retirando las tarjetas secundarias y adaptando el contenedor para que quede centrado; verificar la visualización responsiva.

## 6. Banderas Gráficas y Disposición de Imágenes

- [x] 6.1 Reemplazar los emojis en el modal y navbar por imágenes gráficas SVG de las banderas de los países referentes; verificar su correcta visualización en Windows.
- [x] 6.2 Estandarizar las imágenes de las tarjetas de Servicios y Equipamiento con altura fija, object-cover y tarjetas flex alineadas; verificar simetría del grid.
- [x] 6.3 Ajustar y pulir la presentación de las imágenes en Quiénes Somos, Ciclotrón y Representantes.

## 7. Carrusel Hero a Pantalla Completa con Títulos Superpuestos

- [x] 7.1 Reestructurar la sección <header> y el carrusel en index.html para ocupar todo el ancho y alto de la pantalla (w-full h-screen) con imágenes de fondo total (object-cover) y capa de gradiente de contraste; verificar que no haya desbordes.
- [x] 7.2 Posicionar los títulos (header-title y header-subtitle) superpuestos en el centro del carrusel con tipografía blanca y sombras; verificar legibilidad y actualización multilingüe.
- [x] 7.3 Asegurar la visibilidad y estética de la barra de navegación fija superior sobre el carrusel y reubicar los controles de navegación del carrusel (dots); verificar responsividad en móviles y escritorio.
