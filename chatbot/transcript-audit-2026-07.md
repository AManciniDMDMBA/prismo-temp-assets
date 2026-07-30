# AI Chat Box — Transcript Audit (July 2026)

Review of AI chat session emails forwarded via the Shopify contact form
(prismocrowns@prismocrowns.com inbox). Each failure below maps to a fix in
`system-prompt.md` and `knowledge-base.md`.

| Date | Visitor | Question asked | What the bot did | Failure type | Fix |
|------|---------|----------------|------------------|--------------|-----|
| Jul 15 | Dr. M.W., Boerne TX | Is the sizing similar to 3M SSCs? | Repeated the generic kit-contents blurb; visitor replied "that was not the question I asked" and asked for a rep | Ignored the question, canned-answer loop | 3M/Hu-Friedy sizing answer added to KB; no-repeat rule |
| Jul 18 | D.R., Mexico | Shipping to Mexico (ES) | Owner had to reply manually | Country-specific shipping gap | Mexico/India confirmed in KB; country-confirm hand-off rule |
| Jul 21 | A.C., Hoonah AK | Sample for consortium quality-management committee | Recited "no free samples" policy verbatim | Rigid policy reply to a high-value institutional lead; never escalated | Institutional-evaluation rule: policy + forward to customer service |
| Jul 24 | MZL Dental, Peabody MA | Are the crowns prefabricated? | (Owner replied manually by email) | KB gap | "Prefabricated — yes" added to KB |
| Jul 24 | Dr. S.U., Germany | "Haben die Prismo Crowns eine CE-Zulassung?" (DE) | Deflected in **English** with a generic "Great question!" sign-off | No CE answer + wrong language | CE answer added to KB; always-reply-in-visitor's-language rule |
| Jul 25 | Dr. P., India | Shipping to India | Owner had to reply manually | Country-specific shipping gap | Same as Mexico fix |
| Jul 25 | Y., Los Angeles | Parent: "How can my dentist order this / if they don't?" | First reply OK; follow-up deflected generically | Dead-end for parents | Parent flow added (share site / forward to team) |
| Jul 28 | Dr. M.L., St. Petersburg RU | "Do you ship to Russia?" (asked twice) | Sent the identical vague "most countries" reply **twice** | Canned-answer loop; never yes/no, never escalated | No-repeat rule + country-confirm hand-off |
| Jul 28 | K.W., US | Free sample before ordering | Policy reply; tone blunt ("real production cost") | Tone | Softer sample verbiage in KB |
| Jul 29 | W.B., Mechanicsburg PA | SDS sheet; then "speak to representative" | Replied with the **greeting message**, then only pasted an email address (owner sent SDS manually next day) | Document request unrecognized; weak hand-off | Document-request rule: confirm request + auto-forward to customer service |
| Jul 29 | Dr. J.L., Gresham OR | Intro Kit with only two colors? (asked twice) | Identical kit blurb twice | Canned-answer loop; kit-customization gap | Kit customization + refill-pack answer added; no-repeat rule |

## Recurring failure patterns

1. **Canned-answer loops** — same reply sent twice in 4 of 11 sessions.
2. **English-only** — German question answered in English.
3. **Document requests (SDS etc.) not recognized** — now: confirm the document
   and state the chat is forwarded to customer service.
4. **No real escalation** — "email us" instead of "your request has been
   forwarded, you'll hear from us."
5. **Knowledge gaps** — CE marking, 3M sizing comparability, prefabricated,
   kit customization, parent purchases, country-specific shipping.
