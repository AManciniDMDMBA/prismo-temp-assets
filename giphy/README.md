# Prismo crown GIFs for GIPHY → Instagram

Instagram has no "upload a picture here" option in Stories stickers, DM replies or
post comments. Those pickers only search **GIPHY**. So the way to drop the crown
animation into a post that won't take an image is to get it *into GIPHY's index*
first, then search for it from inside Instagram.

The catch: uploading to a plain GIPHY account only puts the file on giphy.com. It
does **not** reach Instagram. Instagram is served from GIPHY's partner API, which
only carries content from **verified Brand / Creator channels**. Verification is
the whole job — the files below are already built to spec.

## Files

| File | Size | Upload as | Where it shows up |
|---|---|---|---|
| `prismo-transformation-sticker.gif` | 480×480, transparent | **Sticker** | Stories sticker tray, comments, DMs |
| `prismo-crown-sticker.gif` | 480×340, transparent, crown only, no text | **Sticker** | Same — reads on photo/video backgrounds |
| `prismo-transformation.gif` | 480×480, white background | **GIF** | GIF tab (comments, DMs, GIF search) |
| `prismo-transformation-720.mp4` | 720×720, silent | source file | Optional: let GIPHY convert it itself |

All three GIFs are 5.3 s, loop forever, and hold on the final rainbow crown for
~0.7 s before restarting. Built from the original .mov: white studio background
keyed out by flood-filling from the frame border, so the chrome highlights inside
the crown survive.

Upload the **stickers** for the use case above — the transparent ones are what the
Stories tray and the comment picker surface. The white-background GIF is the
fallback for the GIF tab.

## Steps

1. **Create the channel.** giphy.com → sign up with an **@prismocrowns.com email**
   (a gmail address will fail brand review). Username `prismocrowns`, display name
   "Prismo Crowns", avatar = the tooth logo.
2. **Upload 5+ pieces first.** GIPHY will not approve a brand channel with an empty
   channel. Upload all three files here plus two more before applying.
   - Upload page: giphy.com/upload → drag the file → pick **Sticker** or **GIF**.
   - Set **Source URL** to `https://prismocrowns.com` on every upload.
   - **Tags are the only way anyone finds these.** Use 10–20, mixing brand and
     generic: `prismo`, `prismo crowns`, `dental crown`, `dentist`, `dentistry`,
     `pediatric dentist`, `kids dentist`, `tooth`, `teeth`, `smile`, `rainbow`,
     `iridescent`, `holographic`, `transformation`, `before and after`,
     `extraordinary`, `oral health`.
3. **Apply for the Brand Channel.** From the channel settings → apply. You need a
   working link to prismocrowns.com (a social profile does not count) and a link to
   the brand's social account. Approval typically takes ~1–3 weeks.
4. **Wait for the index.** After approval, allow up to another week before the
   stickers are searchable inside Instagram — every sticker is screened separately.
5. **Test in Instagram.** Story → sticker tray → GIF → search `prismo`. Then a post
   comment → GIF icon → same search. If it appears on giphy.com but not in
   Instagram, the channel is not verified yet — that is the only cause.

## Rules the files already satisfy

- Stickers must have real transparency; a white square is rejected as a sticker.
  First frame here is 69–80% transparent (GIPHY requires ≥20%).
- Stickers must animate — at least 2 frames, set to loop forever.
- Source must be GIF for a sticker (no APNG, no WebM).
- Under 15 s (GIPHY recommends ≤6 s) and under 100 MB. These are ~2.5 MB each.
- Dimensions are multiples of 4, as GIPHY recommends.

## Gotchas

- Audio is stripped — the animation has to read silently. It does.
- GIF alpha is 1-bit, so there are no soft edges. The drop shadow was keyed out of
  the crown-only sticker for that reason; `prismo-transformation-sticker.gif` keeps
  a light shadow, which looks right on light backgrounds and slightly grey on dark.
- "From ordinary" is grey and goes dim on dark backgrounds. On photo-heavy Stories,
  use `prismo-crown-sticker.gif`.
- Anything uploaded to GIPHY is public and anyone can reuse it. Never upload
  anything with patient images or identifying information.

## Regenerating

```sh
# 1. frames
ffmpeg -i source.mov -vsync 0 frames/f%03d.png
# 2. key the white background (flood fill from the border) -> keyed/*.png
# 3. decimate 30 -> 15 fps, hold the last frame ~9 frames
# 4. encode
ffmpeg -framerate 15 -i seq/%03d.png -filter_complex \
  "[0:v]scale=480:480:flags=lanczos,split[a][b];\
   [a]palettegen=max_colors=255:reserve_transparent=1:stats_mode=diff[p];\
   [b][p]paletteuse=alpha_threshold=128:dither=sierra2_4a:diff_mode=rectangle" \
  -loop 0 out.gif
gifsicle -O3 --lossy=25 out.gif -o out-final.gif
```
