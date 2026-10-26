# Proposal

## Why

In mobile viewports (screens smaller than `sm` / 640px), the German translation of the main hero title ("ZENTRUM FÜR NUKLEARMEDIZIN UND STRAHLENTHERAPIE") consists of long compound words that cause excessive line wrapping and disproportionate vertical height at standard mobile font size (`text-4xl` / 36px). Reducing the hero title font size by approximately 10% on mobile devices when German is selected improves visual balance, prevents overflow, and preserves room for the subtitle and action buttons.

## What Changes

- Dynamically adjust or style the hero title (`[data-key="header-title"]`) to be ~10% smaller on mobile screens (viewport width < 640px) when German (`de`) is the active language.
- Preserve standard responsive font sizing on tablets and desktops (`sm:`, `md:`, `lg:`).
- Maintain normal font sizes for Spanish, English, and Chinese across all viewport sizes.
- Ensure smooth transitions when switching languages dynamically via the navbar dropdown or modal.

## Capabilities

### Modified Capabilities
- `localization`: Add requirement for responsive font size adjustment of the hero title in German on mobile viewports.

## Impact

- Affects `index.html` (specifically the hero title heading and the `updateLanguage` JavaScript handler or CSS rules).
- No backend or third-party dependency impact.
