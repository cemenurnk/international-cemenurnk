# Spec Delta

## Purpose

Proporciona soporte multiidioma en el sitio web de CEMENURNK, permitiendo la visualización en español, inglés, chino y alemán, la selección interactiva de preferencia de idioma en la primera visita del usuario mediante un modal, la persistencia en el navegador y el cambio dinámico de idioma a través de la barra de navegación con banderas gráficas referentes. Asimismo, estandariza la disposición de imágenes en el sitio y simplifica la visualización de la sección de representantes.

## ADDED Requirements

### Requirement: German Language Support
The system SHALL incorporate the German language (`de`) into the set of available languages, translating all textual content, interactive labels, image alternative texts, and map resources on the website.

#### Scenario: Switching to German displays localized content
- **WHEN** el usuario selecciona el idioma alemán (`de`)
- **THEN** la página actualiza los elementos visibles al idioma alemán, configura el atributo `lang="de"` en la etiqueta `<html>`, actualiza el mapa al idioma alemán y ajusta los textos alternativos del carrusel.

### Requirement: First-Visit Language Selection Modal
The system SHALL present an interactive welcome and language selection modal to users who visit the website for the first time or do not have a saved language preference in `localStorage`.

#### Scenario: First visit displays language selection modal
- **WHEN** un usuario accede al sitio y no existe una clave de idioma válida guardada en `localStorage`
- **THEN** el sistema muestra de manera destacada un modal centrado con opciones para Español, English, 中文 y Deutsch con sus banderas gráficas correspondientes.

#### Scenario: Selecting language in modal persists preference and closes modal
- **WHEN** el usuario hace clic en cualquiera de las opciones de idioma del modal
- **THEN** el sistema guarda la selección en `localStorage`, actualiza el contenido del sitio al idioma elegido y oculta el modal.

#### Scenario: Subsequent visits apply saved language without modal
- **WHEN** un usuario accede al sitio y ya cuenta con una preferencia de idioma guardada en `localStorage`
- **THEN** el sistema aplica directamente el idioma guardado y no muestra el modal de bienvenida.

### Requirement: Navbar Language Selector Dropdown
The system SHALL provide a dropdown menu in the navigation bar that displays the current active language and allows the user to switch at any time to any of the four supported languages (Spanish, English, Chinese, German).

#### Scenario: User changes language via dropdown
- **WHEN** el usuario despliega el menú de idiomas en la barra de navegación y selecciona un idioma diferente al actual
- **THEN** el sistema actualiza el idioma visualizado en la página, actualiza el indicador del idioma activo en el botón del menú y actualiza la preferencia guardada en `localStorage`.

### Requirement: Representative Section Simplification
The system SHALL only display the CEO card in the "Representantes" section, presenting it centered in the container.

#### Scenario: Viewing representatives section
- **WHEN** un usuario visualiza la sección "Representantes"
- **THEN** solo se muestra la tarjeta correspondiente al CEO (Martín Mutuberria) de manera centrada.

### Requirement: Visual Flag Representation
The system SHALL render real country flag graphics (not OS-dependent emoji characters) in the language dropdown and welcome modal for the reference country of each language.

#### Scenario: Displaying flags in language UI
- **WHEN** the user views the language modal or dropdown selector
- **THEN** each language option displays an SVG/graphical flag image corresponding to its reference country.

### Requirement: Responsive and Uniform Image Presentation
The system SHALL display service and equipment images using consistent aspect ratios and object fit to maintain aligned card heights across all viewport sizes.

#### Scenario: Viewing service and equipment cards
- **WHEN** a user browses the services or equipment sections
- **THEN** all images within the cards conform to a standardized height and aspect ratio (`object-cover`) ensuring visually balanced cards.
