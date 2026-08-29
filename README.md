# Collective Image Lab

Browser tool for the Digital Methods Labs, King's College London.
Students load a published collection, add their own images, and arrange them.
Everything runs client-side; nothing is uploaded by the page itself.

Made with ♡ & ✨ by Janna Joceli Omena
Background image: Paweł Czerwiński, Unsplash.

## URLs

- Public lab: https://jannajoceli.github.io/collective-image-lab/
- Private collection builder:
  https://collective-image-lab.jannajoceli.chatgpt.site

The collection builder is deliberately separate from GitHub Pages and restricted
to the instructor's authorised account.

## Capacity

The recommended supported capacity is **500 images per collection/canvas**:

- **Hue, Light, and Name:** up to 500.
- **Similarity:** exact t-SNE up to 250. Above that, the interface explains
  that the quadratic calculation is too heavy and asks users to use one of the
  other arrangements.
- **Admin Builder:** up to 500, with automatic JSON chunking below 20 MiB per
  file so GitHub's 25 MiB browser-upload limit is respected.

Both the Lab and private Admin Builder accept multiple files, selected folders,
and folders dropped from the desktop.

## Weekly workflow
1. Download the images students uploaded to the shared link.
2. Open the private collection builder.
3. Choose **New collection**, enter a distinctive collection name, drop the
   images in, and press **Build collection files**.
4. Download every collection part plus `index.json`.
5. Open the repository root:
   https://github.com/jannajoceli/collective-image-lab
6. Select **Add file → Upload files**, upload every generated collection file
   and the replacement `index.json` alongside `index.html`, then select
   **Commit changes**.
   Large collections are split into parts below 20 MiB so each part remains
   under GitHub's browser-upload limit.
7. Refresh the public Lab and select the collection by name. Allow a minute or
   two for GitHub Pages to update.
8. Reload the private builder before building again.

New collections receive a timestamp ID automatically, while the chosen name is
shown in the public collection browser. Creation time remains stored in the
generated JSON, so the list stays chronological without being tied to lab days
or class times.
