# Collective Image Lab

Browser tool for the Digital Methods Labs, King's College London.
Students load a published collection, add their own images, and arrange them.
Everything runs client-side; nothing is uploaded by the page itself.

Made with ♡ & ✨ by Janna Joceli Omena
Background image: Paweł Czerwiński, Unsplash.

## URLs

- Public lab: https://jannajoceli.github.io/collective-image-lab/
- Instructor admin: https://jannajoceli.github.io/collective-image-lab/?admin=1

The admin URL uses `?admin=1`. Starting it with `&admin=1` makes GitHub Pages
treat it as a file path and returns a 404.

## Weekly workflow
1. Download the images students uploaded to the shared link.
2. Open the instructor URL, go to the Admin tab.
3. Choose **New collection**, or an existing collection listed by creation time
   (newest first), then drop the images in and press Build.
4. Download the two files it produces and commit them here —
   the collection-*.json FIRST, then index.json.
5. Reload before building again.

New collections receive a timestamp ID automatically. Their creation time is
stored in both generated JSON files, so the list stays chronological and is not
tied to lab days or class times.
