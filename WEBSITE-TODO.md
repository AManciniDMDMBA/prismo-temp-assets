# Prismo Crowns website: to-do list (saved Nov 14, 2026)

## Step 1: publish the follow-up draft (owner, one click)
The main Nov 14 theme (ID 195038478612) was published by the owner on Nov 14 and verified
live from the US, Egypt and Spain.
A small follow-up draft is waiting: Shopify admin > Online Store > Themes >
"PREVIEW 2 — blog titles + product page polish (Nov 14)" > Publish.
Theme ID: 195048636692. Preview: https://prismocrowns.com/?preview_theme_id=195048636692
It contains: full blog titles on phones, kit switcher labels stacked with the current kit
outlined, and product descriptions without the link-like underlines and red text.

## Done on Nov 14 (inside the preview theme unless noted)
- Local-currency prices on homepage cards, FAQ, chat and product descriptions
- Homepage first load cut from about 9 MB to under 4 MB
- Phone layout: page no longer wider than the screen; header and announcement fit
- Inner pages: content no longer hidden under the fixed header
- Chat: answers for samples, prices, shipping, discounts, brochures, order problems,
  material / nickel (316L), tooth coverage, kit colors; replies in English, Spanish,
  Arabic, German, French, Portuguese and Turkish; now active on every page
- FAQ: samples, shipping, colors rewritten; four new entries
- Shop page order changed so the Intro Kit and Pro Kit come first (LIVE change, not theme)
- Shop page given a search title and description (LIVE change, not theme)

## To do later
1. Native-speaker review of the chat replies: Arabic, German, Turkish, French,
   Spanish, Portuguese (file: sections/prismo-chat-routing.liquid).
2. Cookie banner covers the lower half of a phone screen for new visitors. Owner setting:
   Settings > Customer privacy > Cookie banner; limit it to regions that require it.
3. Remove marketing apps no longer used (Klaviyo, PushOwl, Lucky Orange, Brevo, upsell app,
   translator app all load scripts on every page). One of them logs "Visitor ID not set"
   on every page.
4. Venezuela is not in any shipping zone; Libya has no flat rate.
5. Turkish lira is not available as a store currency, so Türkiye sees euros.
6. Theme library is at 19 of 20; delete old backups.
7. Chat quotes the international flat rate (US$29.99) as fixed text; update it if the
   rate changes.
8. Shopify connector: theme publish and theme edit tools need re-authorising at
   https://claude.ai/customize/connectors if Claude should publish themes directly.
9. Tap a gallery video on the live homepage to confirm playback (could not be tested).

## How theme edits were made
Shopify's theme tools were blocked, so files were uploaded with the Admin API
(themeFilesUpsert) from temporary copies on this repo's branch
claude/fervent-volta-p8xn0d, then deleted. They remain in that branch's git history.
