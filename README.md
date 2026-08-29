# Collective Image Lab

Browser tool for the Digital Methods Labs, King's College London.
Students load a published collection, add their own images, and arrange them.
Everything runs client-side; nothing is uploaded by the page itself.

Made with ♡ & ✨ by Janna Joceli Omena
Background image: Paweł Czerwiński, Unsplash.

## URLs

- Public lab: https://jannajoceli.github.io/collective-image-lab/

- Tutorial: https://jannajoceli.github.io/collective-image-lab/tutorial.html

- Video: https://youtu.be/tGWY-c6LPzA

## Capacity

The recommended supported capacity is **500 images per collection/canvas**:

- **Hue:** up to 500.
- **Similarity:** exact t-SNE up to 250. Above that, the interface explains
  that the quadratic calculation is too heavy and asks users to use Hue.
- **Lab uploads:** multiple selected files or a selected/dropped folder, up to
  500 images on one canvas.

JPEG, PNG, WebP and GIF files are accepted. GIF animations remain animated for
viewing; Hue and Similarity are calculated from a representative static frame.

## How a seminar collection becomes shared

Each participant's Lab runs only in that participant's browser. The seminar lead
cannot automatically access those local images. Participants must submit their
chosen originals through the donation form (or send them to the lead by another
agreed method). At the end of the session, the lead downloads the submissions
into one folder and passes it through the authorised publication workflow. The
public **Collections** view then lists the published collection.

New collections receive a timestamp ID automatically, while the chosen name is
shown in the public collection browser. Collections are ordered by creation
time, newest first, without being tied to lab days or class times.
