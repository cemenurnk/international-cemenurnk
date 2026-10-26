# Spec Delta

## ADDED Requirements

### Requirement: Responsive German Hero Title Scaling on Mobile
The system SHALL reduce the font size of the main hero title by approximately 10% on mobile viewports (screens under 640px) specifically when the active language is German (`de`), while maintaining standard responsive typography for other languages and larger viewport sizes.

#### Scenario: Mobile viewport with German language active
- **WHEN** the active language is German (`de`) and the screen viewport is narrower than 640px
- **THEN** the hero title renders at ~10% reduced font size compared to the default mobile title font size.

#### Scenario: Mobile viewport with other languages active
- **WHEN** the active language is Spanish (`es`), English (`en`), or Chinese (`zh`) on a mobile viewport
- **THEN** the hero title renders at the standard mobile font size without reduction.

#### Scenario: Switching languages on mobile dynamically updates font size
- **WHEN** a user switches between German and any other language on a mobile viewport
- **THEN** the hero title font size immediately updates to reflect the respective language sizing without requiring a page reload.
