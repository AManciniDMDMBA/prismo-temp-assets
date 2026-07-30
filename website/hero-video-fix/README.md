# Hero video — autoplay on mobile (remove static image + play button)

## The problem

On phones the hero (silver → Unicorn transition video) showed a **static
image with a play button** instead of autoplaying. Desktop autoplayed
correctly with the pause button in the lower right.

## Why it happens

1. **Mobile browsers block autoplay** unless the `<video>` element carries
   BOTH `muted` and `playsinline` (plus `autoplay`). If either is missing,
   iOS Safari and Android Chrome refuse to start the video and render a
   poster frame with a play control instead. This is the #1 cause.
2. **Many Shopify themes intentionally use "deferred media" on mobile** — a
   static preview image with a play button — to save mobile data. If the
   theme's hero/video section has settings like "autoplay on mobile",
   "deferred media", or "show play button", they override the markup.
3. **iPhone Low Power Mode** blocks autoplay until the user's first touch,
   no matter what the markup says.

## The fix (in `hero-video.liquid`)

- `autoplay muted playsinline webkit-playsinline loop preload="auto"` on the
  video element — satisfies every mobile autoplay policy.
- JavaScript sets `video.muted = true` as a *property* before calling
  `play()` (some in-app browsers ignore the attribute alone) and retries
  `play()` on the visitor's **first touch/scroll anywhere on the page** —
  this defeats Low Power Mode without ever showing a play button.
- Video resumes when the visitor returns to the tab.
- **Pause-only control** stays in the lower right (it becomes a resume
  button only after the visitor themselves pauses — required so a visitor
  who pauses isn't stuck).
- No `controls` attribute → the browser never draws its own play UI.

## ADA / accessibility (wow factor kept)

- WCAG 2.2.2 (Pause, Stop, Hide): auto-playing motion longer than 5 seconds
  must have a pause mechanism. **Autoplay + visible pause button = compliant.**
  A play button is NOT required by ADA/WCAG.
- The video is muted, so there is no autoplay-audio issue (WCAG 1.4.2).
- Pause button: 44px touch target, `aria-label`, keyboard focusable.
- Optional stricter practice (NOT enabled, per business decision to preserve
  the wow factor): honoring the OS "reduce motion" setting
  (`prefers-reduced-motion`) would show those specific users a still frame.
  Can be added later with 3 lines of CSS/JS if ever desired.

## How to apply in Shopify

1. **First, check the section settings** (fastest fix if the theme supports
   it): Shopify admin → Online Store → Themes → Customize → select the hero
   section → look for toggles like *Autoplay*, *Autoplay on mobile*,
   *Show play button*, *Use deferred media*. Enable autoplay everywhere and
   disable the play button/overlay.
2. **If no such settings exist**, edit the code: Themes → ⋯ → Edit code →
   find the hero section (`sections/` — e.g. `video-hero.liquid`,
   `image-banner.liquid`, or a custom section) and replace its `<video>`
   markup + play-button overlay with the contents of `hero-video.liquid`,
   wiring `hero_video_url` / `hero_poster_url` to the section's existing
   settings.
3. Test on a real iPhone (including Low Power Mode) and Android device.

> Note: the Shopify connector in this workspace can edit theme files on an
> unpublished/duplicate theme once tool access is approved — the live theme
> must be published from Shopify admin afterward.
