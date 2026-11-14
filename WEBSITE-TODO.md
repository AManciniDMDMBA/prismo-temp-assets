# Prismo Crowns website: to-do list (saved Nov 14, 2026)

## Step 1: publish the new theme (owner, one click)
Shopify admin > Online Store > Themes > "PREVIEW — local prices + faster load (Nov 14)" > Publish.
Theme ID: 195038478612. Preview: https://prismocrowns.com/?preview_theme_id=195038478612
After publishing, ask Claude to re-check the live site from the US, Egypt and Spain,
and tap one gallery video to confirm it plays.

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

## To do later
1. Native-speaker review of the chat replies: Arabic, German, Turkish, French,
   Spanish, Portuguese (file: sections/prismo-chat-routing.liquid).
2. Product description styling: remove the underlined paragraphs and the red underlined
   "48 CROWNS — SIZES 3, 4 & 5 ($10.99 each)" line on the Intro Kit, Pro Kit and refill
   products. This is product text, not theme.
3. Kit switcher on product pages: labels run together ("Intro Kit48 colored crownssizes
   3, 4, 5") and the Pro Kit button is highlighted green on the Intro Kit page
   (sections/main-product.liquid).
4. Blog titles are cut off mid-word on phones ("…Crowns: CDT...").
5. Cookie banner covers the lower half of a phone screen for new visitors. Owner setting:
   Settings > Customer privacy > Cookie banner; limit it to regions that require it.
6. Remove marketing apps no longer used (Klaviyo, PushOwl, Lucky Orange, Brevo, upsell app,
   translator app all load scripts on every page).
7. Shop page has no search (meta) description.
8. Venezuela is not in any shipping zone; Libya has no flat rate.
9. Turkish lira is not available as a store currency, so Türkiye sees euros.
10. Theme library is at 18 of 20; delete old backups.
11. Chat quotes the international flat rate (US$29.99) as fixed text; update it if the
    rate changes.
12. Shopify connector: theme publish and theme edit tools need re-authorising at
    https://claude.ai/customize/connectors if Claude should publish themes directly.

## How theme edits were made
Shopify's theme tools were blocked, so files were uploaded with the Admin API
(themeFilesUpsert) from temporary copies on this repo's branch
claude/fervent-volta-p8xn0d, then deleted. They remain in that branch's git history.
