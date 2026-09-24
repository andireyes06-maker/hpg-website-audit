# HPG website: mobile audit, 2026-09-25

**Base device:** iPhone 15 Plus (430 × 932, Safari/WebKit).
**Also swept:** 320, 360, 390 (iPhone 13), 600 and 768 (touch tablet), plus a 1440 desktop check that every fix leaves desktop unchanged.
**Method:** every page was tested on the **live site** (higherperformancegroup.com) with Playwright. Each fix was checked by loading the live page and swapping in the edited local CSS, so it was verified inside the real Duda page, not a mock-up. QR Book and Sample Report have no known live URL, so they were rendered locally.

> **Nothing is live yet.** The fixes are in the local `*-duda-inject.html` files. Each changed file needs to be pasted back into its Duda HTML widget (list at the bottom).

---

## The two reported bugs

### 1. Dr Joe bio photos are cut off: **Fixed**
`bio-duda-inject.html`

- **What you saw:**
  - The sidebar photo sliced through his eyes.
  - The hero cut off the top of his head.
  - The turning-point photo was squeezed into a strip.
- **Cause:** below 1024px the photo boxes dropped their `aspect-ratio` and switched to short fixed heights (320 → 260 → 220px). A 2:3 portrait was forced into a wide strip and cropped from the centre.
- **Fix (fluid, works on any phone):**
  - The sidebar photo keeps a 4:5 ratio, capped at `min(560px, 80svh)`, with the crop anchored to the top (lines 221, 226).
  - The turning-point photo keeps its natural 4:3 ratio, capped at `min(480px, 70svh)` (line 224).
  - Hero crop anchor moved to 35% vertical, so the face sits above the name overlay (line 225).
  - Hero height is now fluid: `min(90vw, 85svh)` on tablets (line 217) and `max(115vw, 280px)` on phones (line 273).
  - The fixed 260/220px heights were removed.
- **Verified** at 320, 430, 600 and 768: the full face is visible in all three photos.

### 2. The Show won't scroll on mobile: **Fixed**
`the-show.html`

- **What you saw:** the page gets stuck, and the bottom "Apply" section and its buttons never appear.
- **Cause:** there are two problems.
  1. **Duda saved a fixed height** for this widget: `#dm .dmBody div.u_1429430672 { height: 11993.6px !important }`. The real content is taller, and the gap grows with screen width:

     | Width | Content hidden |
     |---|---|
     | 430 | 219px |
     | 600 | 1,311px |
     | 768 (tablet) | 2,680px |

  2. The page wrapper also has `overflow-x:hidden`, which makes the browser treat it as its own scroll box. On a phone your swipe scrolls that inner box instead of the page, so it feels frozen.
- **Fix:**
  - `height:auto !important` override (line 20).
  - `overflow-x:clip`, which clips sideways without creating a scroll box (line 35). Older browsers fall back to the existing `hidden`.
- **Verified:** the page scrolls at every width, the widget matches its content exactly, and the last Apply button is reachable. On the 15 Plus the page is no longer a scroll box.

---

## Other broken things found and fixed

### 3. Duda "saved heights" hiding or overlapping content: Bio, TQ Assessment, Home: **Fixed**
This is the same Duda problem as The Show. Duda stores **one** fixed pixel height per widget for all phones, but content height changes with screen width. So:

| Page | 320 (small phone) | 430 (15 Plus) | 768 (tablet) |
|---|---|---|---|
| Dr Joe bio | Footer printed **on top of** the final CTA (450px overlap) | 545px blank white band before the footer | 412px blank band |
| TQ Assessment | Footer covers the last section; "Schedule a Discovery Call" hidden (873px) | 193px blank band | 955px blank band |
| Home (6 sections) | Each section's bottom is drawn over by the next (90–524px), e.g. the testimonial cards get cut | 35–75px overlaps | Mixed overlaps and gaps |

**Fix:** let each widget size to its content.
- `bio-duda-inject.html:301`
- `tq-assessment-duda-inject.html:353`
- ~~`home-duda-inject.html:107`~~ **Reverted.** Home's rule targeted every `.dmCustomHtml` widget with `!important`, which also applied inside the Duda editor and blocked resizing widgets there. Home heights are managed in the Duda editor instead.

**Verified:** every widget box equals its content at 320, 430 and 768, and desktop is unchanged.

### 4. Text hidden under the mobile header: The Show, P2P, Guest Instructions, Research, Bookstore (tablets): **Fixed**
- **Cause:** on any touch device, Duda switches to its mobile layout (`body.dmMobileBody`). That layout floats a fixed 60px header over the page, and page content starts at y=0 underneath it. This depends on the device, not the width, so a touch tablet at 960px gets it too. Pages without enough top padding had their first line hidden:

  | Page | Hidden text |
  |---|---|
  | The Show | "Higher Performance Group Presents" eyebrow, half under the header |
  | P2P | The whole gold sponsor ticker |
  | Guest Instructions | "The Show with Dr. Joe" eyebrow |
  | Research | "Research Library" eyebrow |
  | Bookstore | Hero kicker, on touch tablets 768–1024 only (phones were already fine) |

- **Fix:** add 60px top padding to each page wrapper, only in Duda's mobile layout. Desktop is untouched, and the added band is the same navy as the hero, so it sits invisibly under the header.
  - `the-show.html:22`
  - `p2p-duda-inject.html:644`
  - `guest-preparation.html:185`
  - `research-duda-inject.html:511`
  - `bookstore-duda-inject.html:670`: here the page's existing 48px phone padding is extended to touch tablets.
- **Verified:** all 15 pages are clear of the header at 320, 430 and 768.

### 5. TQ Advantage (/team-intelligence): "Order the Book" button cut off: **Fixed**
- **Cause:** the hero text block kept its desktop `margin-left: 8%` on phones while also being `width:100%`. The button row was pushed 31px right and ran off the screen.
- **Fix:** `margin-left: 0` in the existing ≤640px query (`tq-advantage-duda-inject.html:265`).
- **Verified** at 320, 430 and 600: all three buttons fit, and they wrap cleanly at 320.

### 6. Bookstore category tabs grab vertical swipes: **Fixed**
- **Cause:** the All / Books / Planners strip scrolls sideways, but its content was also 1px too tall. That made it a tiny vertical scroll box, which could swallow the first swipe on tablets.
- **Fix:** add `overflow-y: hidden` (`bookstore-duda-inject.html:611`). It still swipes sideways.

### 7. Sample Report: content off-screen on small phones: **Fixed (verified locally)**
`sample-report.html`
- **Arc cards:** at 320 the two-column arc cards didn't fit, and the second card ran off the right edge. The grid now picks its own column count (line 252): one column on small phones, two on the 15 Plus and on tablets, same as before.
- **Frequency labels:** below 400px the "Often / Usually" labels were pushed off-screen. A new ≤399px rule (line 262) moves the label under the behaviour name. Layout at 400px and up is unchanged.

---

## Checked and fine (no change needed)

- **Sideways scrolling:** no page scrolls sideways at any width (320–768).
- **Mobile menu:** opens on tap, locks the page behind it, and lists every section.
- **Home popup (Burnout Force Check):** displays correctly and closes. At 320 it scrolls a few pixels inside itself, which is normal for a modal.
- **Home "paths" list:** tapping opens each path as intended.
- **Blank areas in early screenshots:** the Home guide section, the Bookstore featured card and similar were scroll-reveal animations caught mid-fade. With a normal scroll, every reveal completes.
- **Clean pages:** The Proof, Burnout Force, Speaker, The Group, Blog and Team Institute had no broken layout on mobile.
- **QR Book:** no overflow; the one wide element is a clipped decorative background.

---

## Recommended, not changed

These are real but they're design or copy calls, not broken layout. Pick any you want done.

1. **Home: "Hover down to see how each path works"** (`home-duda-inject.html:1097`). Phones can't hover. Suggest wording like "Tap a path to see how it works".
2. **Small text sitewide.** Eyebrow and label text is 9–11px on every page (e.g. "An HPG Keynote · Season I", stat labels, button text at 11px). It's readable on the 15 Plus but below the house 12px floor for labels. This would be a sitewide type decision.
3. **Small tap targets:**
   - Footer email and social links are 17–22px tall. The footer is Duda's own.
   - Inline "Take the assessment →" is 14px tall.
   - Research filter pills are 30px.
   - The Home popup close button is 30×30 (`home-duda-inject.html:1680`).

   The house minimum is 44px.
4. **Swipe strips with no cue:** the Research stat bar and filter pills, and the Bookstore tabs, are cut off at the right edge with nothing telling people to swipe. A fade on the right edge would help.
5. **Low-contrast text:**
   - Guest Instructions footer meta line ("The Show with Dr. Joe · Mondays & Thursdays").
   - Home "The Brilliant Team Paradox" eyebrow. This overlaps audit-001 item 5.
6. **Duda mobile menu "Get Started" button** is iOS blue, not the site's gold. It's a Duda theme setting, not in these files.
7. **Blog:** "Your Leadership Team Needs More Drama" is listed twice (Sept 22 and Sept 15). This is content, not mobile.
8. **Home on desktop:** Duda's desktop saved heights are also shorter than the content (by 67–258px), but nothing visibly overlaps at 1440. Left alone per "don't stray".
9. **In Duda itself:** the saved-height issues (items 2 and 3) come from widget heights stored in the Duda editor. The CSS overrides work regardless. If someone later resizes these widgets in the editor, the overrides keep protecting the pages.

---

## Files to paste back into Duda

| File | Live page | Changes |
|---|---|---|
| `bio-duda-inject.html` | /dr-joe-hill | Photos (1), saved height (3) |
| `the-show.html` | /the-show | Scroll trap (2), header clearance (4) |
| `home-duda-inject.html` | / | Saved heights (3). Change is in the **first** widget's style block (hero) |
| `tq-assessment-duda-inject.html` | /tq-assessment | Saved height (3) |
| `p2p-duda-inject.html` | /p2p-page | Header clearance (4) |
| `guest-preparation.html` | /guest-instructions | Header clearance (4) |
| `research-duda-inject.html` | /research | Header clearance (4) |
| `bookstore-duda-inject.html` | /bookstore | Tab strip (6), tablet header clearance (4) |
| `tq-advantage-duda-inject.html` | /team-intelligence | Hero buttons (5) |
| `sample-report.html` | (live URL unknown) | Arc grid and frequency labels (7) |

Not touched: `the-proof.html`, `burnout-force`, `speaker-page`, `thegroup`, `blog`, `team-institute`, `qr-book`, `header.html`, and the two test copies.
