## Context
Sitio web institucional multilingüe del Centro de Medicina Nuclear y Radioterapia "Pdte. Dr. Néstor C. Kirchner" (CEMENURNK), orientado a pacientes, profesionales e instituciones nacionales e internacionales.
Stack: HTML5, Tailwind CSS (CDN) y Vanilla JavaScript.
Expensive decisions: Multi-idioma (`es`, `en`, `zh`, `de`).

## Backlog
1. Como visitante, quiero navegar el sitio sin la sección de Representantes (y con las fotos institucionales actualizadas), para ver únicamente la información institucional vigente.
2. Como visitante, quiero leer en la descripción inicial que el centro está ubicado en el norte de Argentina (limítrofe con Paraguay y Brasil) y en continuo crecimiento y expansión, para dimensionar su alcance estratégico regional.
3. Como visitante, quiero conocer los Valores institucionales junto con la Misión y la Visión, para comprender los principios que guían la atención del centro.
4. Como visitante, quiero ver un bloque visual "CEMENURNK en Cifras" con íconos e indicadores de trayectoria (año de inicio, tratamientos, estudios realizados, profesionales, m² de infraestructura y procedencia de pacientes de provincias y países vecinos), para apreciar rápidamente la magnitud y experiencia del centro.
5. Como visitante o institución médica, quiero consultar la sección "Ciclotrón y Radiofarmacia" con el detalle de la producción de radiofármacos además del equipamiento del ciclotrón, para conocer la capacidad integral de producción radiofarmacéutica del centro.

---

## Story #1
Como visitante, quiero navegar el sitio sin la sección de Representantes, para ver únicamente la información institucional vigente.

### Acceptance criteria
- [x] Dado que ingreso al sitio web en cualquiera de los idiomas disponibles, cuando observo el menú de navegación superior, entonces no veo ningún enlace hacia "Representantes" (solo Quiénes Somos, Servicios, Equipamiento y Contacto).
- [x] Dado que recorro la página de principio a fin, cuando paso de la sección de Ciclotrón hacia el final del sitio, entonces veo directamente la sección de Contacto sin ninguna sección ni tarjetas de Representantes.

### Plan
- Quitar el enlace de navegación a la sección de representantes en la barra superior.
- Eliminar el bloque completo de la sección de representantes del cuerpo de la página.
- Limpiar los textos traducidos asociados a representantes en el diccionario multilingüe para los cuatro idiomas.

### Out of scope
- Modificar los datos de la sección de Contacto (teléfonos, correo o dirección).
- Agregar nuevas secciones o cambiar imágenes de otras secciones del sitio.

---

## Story #2
Como visitante, quiero leer en la descripción inicial que el centro está ubicado en el norte de Argentina (limítrofe con Paraguay y Brasil) y en continuo crecimiento y expansión, para dimensionar su alcance estratégico regional.

### Acceptance criteria
- [x] Dado que ingreso a la sección "Quiénes Somos" en cualquiera de los idiomas disponibles (es, en, zh, de), cuando leo la descripción inicial de la institución, entonces veo explícitamente su ubicación en el norte de Argentina (limítrofe con Paraguay y Brasil).
- [x] Dado que leo la descripción inicial en cualquiera de los idiomas disponibles, cuando observo el estado institucional del centro, entonces veo mencionado que se encuentra en continuo crecimiento y expansión.

### Plan
- Modificar el primer párrafo de descripción institucional (`about-paragraph-1`) en el marcado HTML de la sección "Quiénes Somos".
- Actualizar las traducciones de `about-paragraph-1` en el diccionario multilingüe para los 4 idiomas (`es`, `en`, `zh`, `de`).

### Out of scope
- Modificar el segundo párrafo (`about-paragraph-2`), la misión o la visión.
- Modificar el diseño o estructura de las tarjetas y secciones adyacentes.

---

## Story #3
Como visitante, quiero conocer los Valores institucionales junto con la Misión y la Visión, para comprender los principios que guían la atención del centro.

### Acceptance criteria
- [x] Dado que navego por la sección "Quiénes Somos" en cualquiera de los idiomas disponibles (es, en, zh, de), cuando llego al bloque institucional posterior a la descripción, entonces veo presentadas la Misión y la Visión en tarjetas destacadas, seguidas por una sección dedicada a los Valores institucionales.
- [x] Dado que observo la sección de Valores, cuando recorro los principios institucionales, entonces encuentro los 6 valores definidos: Compromiso y Responsabilidad, Igualdad Social, Respeto, Integridad, Cultura de Trabajo e Integridad Institucional, y Liderazgo con sus descripciones completas.
- [x] Dado que cambio el idioma del sitio (español, inglés, chino o alemán), cuando reviso los títulos y descripciones de la Misión, Visión y Valores, entonces todo el contenido se traduce fielmente al idioma seleccionado.

### Plan
- Reestructurar el bloque inferior de "Quiénes Somos" en `index.html` organizando la Misión y la Visión en tarjetas visuales de dos columnas.
- Incorporar una subsección "Nuestros Valores" con una cuadrícula responsiva (1 col móvil, 2 col tablet, 3 col desktop) con íconos e información detallada para cada uno de los 6 valores institucionales.
- Incorporar todas las claves de traducción correspondientes en el objeto `translations` para `es`, `en`, `zh` y `de`.

### Out of scope
- Modificar el contenido de los párrafos introductorios de "Quiénes Somos".
- Alterar la sección de Servicios u otras secciones posteriores.

---

## Story #4
Como visitante, quiero ver un bloque visual "CEMENURNK en Cifras" con íconos e indicadores de trayectoria (año de inicio, tratamientos, estudios realizados, profesionales, m² de infraestructura y procedencia de pacientes de provincias y países vecinos), para apreciar rápidamente la magnitud y experiencia del centro.

### Acceptance criteria
- [x] Dado que navego por el sitio web en cualquiera de los idiomas disponibles (es, en, zh, de), cuando observo la barra de navegación superior o me desplazo tras "Quiénes Somos", entonces encuentro la sección destacada "CEMENURNK en Cifras" / "En Cifras".
- [x] Dado que observo los indicadores clave superiores, cuando reviso las métricas de trayectoria, entonces veo las tarjetas con íconos para: Año de inicio (2022), Pacientes únicos (4.216), Sesiones de RT (31.260), Estudios Dx (4.514), Profesionales (77) e Infraestructura (3.150 m²).
- [x] Dado que visualizo los gráficos analíticos, cuando observo la sección, entonces veo un gráfico de torta/donut interactivo de Pacientes Atendidos por Servicio (Diagnóstico 3.347, Bienestar 1.990, Radioterapia 1.522 y Oncología 142) y las barras de Prácticas y Prestaciones acumuladas.
- [x] Dado que analizo la procedencia geográfica, cuando observo el bloque correspondiente, entonces veo el mapa vectorial de Argentina destacando la provincia de Formosa junto a burbujas proporcionales y barras con los datos reales: Formosa Capital (2.751 - 65,2%), Interior (1.274 - 30,2%), Otras provincias (173 - 4,1%), Paraguay (17 - 0,4%) y el resumen gerencial.
- [x] Dado que exploro el equipo interdisciplinario, cuando recorro "Diversidad de Saberes", entonces veo el desglose de los 77 profesionales: Técnicos (22), Licenciados (21), Ingenieros (10), Médicos (8), Estudiantes (10) y Otros perfiles (6).
- [x] Dado que cambio de idioma, cuando se actualiza la interfaz, entonces todos los títulos, leyendas y etiquetas (incluyendo el gráfico de servicios) se traducen fielmente a español, inglés, chino y alemán.

### Plan
- Añadir el enlace "En Cifras" (`nav-stats`) en la barra de navegación.
- Implementar la sección `#cifras` con fondo oscuro tecnológico (`slate-900`), acentos cian y azul institucional.
- Integrar Chart.js para el gráfico de torta/dona interactivo con porcentajes y tooltips informativos.
- Incorporar mapa vectorial SVG de Argentina con círculos concéntricos indicadores y barras de distribución por origen.
- Presentar el tablero de desglose de saberes profesionales e indicadores de prácticas acumuladas.
- Añadir las traducciones completas en `translations` para `es`, `en`, `zh` y `de`.

### Out of scope
- Modificar el contenido de la sección de Equipamiento Médico o Ciclotrón.
- Alterar el formulario o mapa de contacto.

---

## Story #5
Como visitante o institución médica, quiero consultar la sección "Ciclotrón y Radiofarmacia" con el detalle de la producción de radiofármacos además del equipamiento del ciclotrón, para conocer la capacidad integral de producción radiofarmacéutica del centro.

### Acceptance criteria
- [x] Dado que navego por la sección de Ciclotrón en cualquiera de los 4 idiomas disponibles (es, en, zh, de), cuando observo el título de la sección, entonces veo "Ciclotrón y Radiofarmacia" en español, "Cyclotron and Radiopharmacy" en inglés, "回旋加速器与放射药房" en chino y "Zyklotron und Radiopharmazie" en alemán.

### Plan
- Actualizar el título de la sección en `index.html` a "Ciclotrón y Radiofarmacia".
- Actualizar la clave `section-cyclotron-title` en el diccionario multilingüe para los 4 idiomas (`es`, `en`, `zh`, `de`).

### Out of scope
- Modificar el subtítulo o las especificaciones técnicas del equipamiento salvo requerimiento explícito.


