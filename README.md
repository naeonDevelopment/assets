# assets

Public image, document and video assets for LinkedIn posts by Theodor Georgiev.

Referenced directly by URL from scheduled posts. Nothing here is generated at
request time — every file is rendered from source in the `personal_brand`
repository and copied in.

## ⚠️ Append-only

**A published post resolves its asset by URL for the life of the post.**
Overwriting or deleting a path breaks the asset in the feed — silently, with no
error anywhere, and with no way to edit the post afterwards.

- **New bytes get a new filename.** Nothing is ever replaced in place.
- **Deleting a file does not unpublish it.** Git history and CDN caches persist.
- **Verify by byte count, not by HTTP 200.** A 200 proves *something* is served,
  not that the right thing is.
- A file may be removed only once no live post points at it, and the only way to
  know that is to check the content ledger.

## Layout — by post type

```
a/<yyyy>/<mm>/
  text/       assets for a text post
                <slug>-cover.png     16:9 · 1920×1080 · carries the hook verbatim
                <slug>-video.mp4     optional · ≤90s · captions burned in
                <slug>-video-poster.png   the still frame, if a video is present
  carousel/   assets for a document post
                <slug>.pdf           the deck · 1:1 · 1080×1080 · 8–10 slides
                <slug>-thumb.png     REQUIRED — Buffer's `document` shape needs
                                     url + title + thumbnailUrl, all three
  article/    assets for an article or newsletter
                <slug>-cover.png     1200×627 · pasted by hand into the editor
  image/      standalone images — annotated artefacts, diagrams, screenshots
                <slug>.png
```

**The slug comes from the verdict, not from the topic.** Lowercase kebab, ASCII
only.

## Why text posts have a video slot

A text post's cover and a text post's video are the same slot in the plan: one
visual, chosen per post. The directory holds both shapes so a post can gain a
video later without moving, renaming or breaking the cover URL a live post is
already resolving.

`<slug>-cover.png` and `<slug>-video.mp4` can coexist. Only one is attached to
any given post — LinkedIn takes an image *or* a video, never both.

## Rendering

Every asset here is reproducible. Sources live in `personal_brand` under
`tenants/personal/content/<yyyy>/<mm>/` and render through headless Chrome
against `templates/personal/tokens.css`.

Verified before publication: Space Grotesk embedded (no fallback faces), correct
page geometry, paginator correct on every deck slide, and a disclosure scan
under the personal Rule 0 regime.
