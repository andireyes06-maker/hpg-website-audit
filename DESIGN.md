# HPG website design system

The house rules for every Higher Performance Group page, so new Duda injects match the rest of the site instead of drifting. They were set during audit-002 (2026-09-25).

**Design Read:** a B2B/B2G leadership-development site for K-12 and higher-ed executives, in a classic-authority editorial style.
**Dials:** ENERGY 2 / RHYTHM 2 / MOTION 2.

## Type
- **Two families only:**
  - **Playfair Display** for headings, big numbers and pull quotes.
  - **DM Sans** for body copy, labels, buttons and forms.
- **One loader** for every page:
  `https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,500;0,600;0,700;1,400;1,500;1,600;1,700&family=DM+Sans:ital,opsz,wght@0,9..40,300;0,9..40,400;0,9..40,500;0,9..40,600;0,9..40,700;1,9..40,400;1,9..40,500&display=swap`
- **Gold italic phrases:** the italic accent in a headline ("*Team Development.*", "*still worthy work.*") is the site's signature typographic gesture. Keep it to one phrase per heading.
- **Sizes:** body text 15px or more; labels 12px or more. Uppercase tracked labels are allowed as section eyebrows, but not as body text.

## Colour
| Token | Value | Use |
|---|---|---|
| Navy | `#08152a` | Page background, primary text on light sections |
| Navy panel | `#0d1e35` | Cards and panels on navy |
| Navy raised | `#132848` | Hover and raised panels |
| Gold | `#c9a84c` | The one accent: key words, primary buttons, rules, focus ring. On navy it passes AA (7.33:1) |
| Gold text on white | `#8c6b23` | Gold-coloured **text** on white (4.95:1) |
| Gold text on cream | `#7a5c1c` | Gold-coloured **text** on cream `#f7f1e4` / `#f7f2e8` (5.53:1) |
| Cream | `#f7f2e8` | Light sections |
| Muted text on navy | `#a7b6c8` | Captions and labels on navy (8.11:1); never the old 20–40% white |
| Off-white | `#f4f1eb` | Primary text on navy |

- **Buttons on gold use navy text.** Never white: white on gold is 2.29:1 and fails.
- **Amazon orange `#FF9900`** is allowed on "Order on Amazon" buttons **only**. It's a deliberate recognition cue for shoppers, not a brand colour. It's used on Bookstore and TQ Advantage.
- **Every text colour must meet WCAG AA** on its real background: 4.5:1, or 3:1 for 24px+ / bold 18.66px+. Check pairs with a contrast checker; don't eyeball them.

## Components and motifs
- **Arrows (→)** mean "this takes you to another page or site". Use them on navigation and outbound links, never on form submits, downloads or modal buttons.
- **Icons** are thin-line inline SVGs, 1.6px stroke, round caps, in gold, matching the ones Home already uses. No emoji as icons.
- **The offering-page series** (The Proof, Burnout Force, TQ Advantage, Team Institute) shares one deliberate template: centred hero → essay → stat pair → "No. 01" feature → grid of the rest → deliverables → logistics → testimonial → CTA. The shared order is a series identity, so visitors know where to find things on every offer. New offer pages should follow it.
- **List markers** are a short gold rule (12×2px), not a dash character.
- **Button labels** name the action: "Send My Request", "Email Me the PDF", "Book a Call". Never "Get Started", "Submit" or "Learn More".

## Copy
- **No em dashes (—).** Use a comma, colon, period or parentheses. Middle dots (·) are fine in label rows.
- The research base is always "**1,050 leadership teams**". "987 leadership analyses" is a separate figure.
- Keep Dr. Joe's own coinages ("stupifany", #CancelAverage).
- Every statistic needs a visible source, or it doesn't appear.

## Accessibility layer (in every inject)
Every page carries the same short "audit-002 shared layer" CSS block:
- **Focus ring:** gold 3px ring with a navy inner line, visible on any background.
- **Press state:** 1px press-down on buttons.
- **Anchor offset:** `scroll-margin-top: 80px`, so anchor jumps clear the 60px mobile header.
- **New-tab cue:** a small ↗ plus a screen-reader note on external text links.
- **Tap area:** larger hit areas on inline links.
- **Reduced motion:** a `prefers-reduced-motion` stop for all animation.

Copy the block from any page into new injects.

## Duda notes
- On touch devices Duda floats a fixed **60px header** over the page (`body.dmMobileBody`). The first section must clear it. Pages use `body.dmMobileBody #dm .dmBody .<wrapper>.<wrapper> { padding-top: 60px !important; }`.
- Duda can save a fixed px height on a widget (`#dm .dmBody div.u_<id>`). Fix heights in the editor first. Only override them per page wrapper, and check that the editor still lets you resize.
