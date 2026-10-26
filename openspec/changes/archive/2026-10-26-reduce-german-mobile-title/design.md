# Design

## Context

In `index.html`, the hero title has the attribute `data-key="header-title"` and Tailwind classes `text-4xl sm:text-5xl md:text-6xl lg:text-7xl`. In JavaScript, `updateLanguage(lang)` sets `document.documentElement.lang = targetLang` on every language change.
See `proposal.md` for motivation.

## Goals / Non-Goals

**Goals:**
- Scale down the hero title by ~10% on mobile screens (viewport < 640px) when German is active.
- Ensure automatic application and removal upon language change without complex DOM manipulation.
- Preserve desktop and tablet typography for German and all sizes for Spanish, English, and Chinese.

**Non-Goals:**
- Modifying other text elements or translations.
- Changing font sizes on viewports $\ge 640\text{px}$.

## Decisions

### 1. Declarative CSS media query targeting `html[lang="de"]`
- **Choice**: Add a CSS rule in `<style>`:
  ```css
  @media (max-width: 639px) {
    html[lang="de"] [data-key="header-title"] {
      font-size: 2.025rem; /* ~10% smaller than text-4xl (2.25rem / 36px) */
      line-height: 1.2;
    }
  }
  ```
- **Rationale**:
  - `updateLanguage()` already updates `document.documentElement.lang = targetLang`.
  - The CSS selector automatically applies whenever `html` has `lang="de"` and cleanly deactivates when switched to any other language.
  - Zero runtime overhead or fragile JavaScript class manipulation.
- **Alternatives considered**:
  - Dynamic JavaScript class toggling (`element.classList.toggle(...)`): Requires synchronizing state and managing class replacements. More prone to edge cases.
  - Inline style manipulation (`element.style.fontSize`): Requires window resize listeners to avoid overriding responsive Tailwind classes on desktop.

## Risks / Trade-offs

- **[Specificity clash with Tailwind utility `text-4xl`]** → CSS rule will target `html[lang="de"] [data-key="header-title"]` which has higher specificity than single Tailwind class `.text-4xl`, ensuring the mobile override applies reliably while `@media (max-width: 639px)` ensures desktop `sm:text-5xl` still takes precedence on $\ge 640\text{px}$.
