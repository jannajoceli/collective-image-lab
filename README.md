# Collective Image Lab

<img width="400" height="221" alt="image-collective-lab" src="https://github.com/user-attachments/assets/6385dfe5-1ac4-4d2b-94b7-22075c45896c" />

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

## How a collection becomes shared

Each participant's Lab runs only in that participant's browser. The seminar lead
cannot automatically access those local images. Participants must submit their
chosen originals through the donation form (or send them to the lead by another
agreed method). At the end of the session, the lead downloads the submissions
into one folder and passes it through the authorised publication workflow. The
public **Collections** view then lists the published collection.

New collections receive a timestamp ID automatically, while the chosen name is
shown in the public collection browser. Collections are ordered by creation
time, newest first, without being tied to lab days or class times.

## How the image arrangements work

### Similarity · t-SNE

**Similarity** uses **t-distributed Stochastic Neighbor Embedding (t-SNE)**, a dimensionality-reduction technique designed to visualise relationships in high-dimensional data.

Each image is represented numerically by the Lab. t-SNE compares these representations and creates a two-dimensional map that tries to preserve **local neighbourhoods**: images that are more similar in the original feature space tend to appear closer together, while less similar images tend to separate.

The resulting clusters can therefore be used for **exploratory analysis**: look for groups of images, recurring visual characteristics, unusual neighbours and outliers.

A t-SNE map should not, however, be read as a precise geographical map of similarity. It is particularly useful for examining **which images become neighbours**, but the exact distances between clusters, their relative sizes and their overall positions should be interpreted cautiously. t-SNE is also stochastic, so repeated runs can produce somewhat different layouts while preserving similar local relationships.

In the Collective Image Lab, the original t-SNE positions are followed by a small **collision-spacing step** so that overlapping thumbnails can be separated for inspection. This changes their display positions slightly but does not change the similarity calculation itself.

**In short:**
`image features → similarity relationships → t-SNE → 2D neighbourhood map → spacing for viewing`

**Supported capacity:** exact t-SNE is used for collections of up to **250 images**.

### Hue

**Hue** arranges images according to their dominant colour hue rather than their similarity across multiple visual features.

Hue describes the basic colour family of a colour, such as red, yellow, green, cyan, blue or magenta. It can be represented as a position around a circular colour wheel from 0° to 360°. Images with related hues are therefore positioned near one another according to this colour dimension.

Unlike t-SNE, Hue is not attempting to discover clusters or multidimensional similarities. It deliberately asks a much simpler question:

> **How does this image collection organise itself when colour becomes the organising principle?**

This can make colour patterns, repetitions, transitions and contrasts within a collection immediately visible. Comparing **Similarity** and **Hue** is therefore also methodologically useful: the same image collection can produce very different visual structures depending on which feature is used to organise it.

**In short:**
`image → colour measurement → hue → colour-based arrangement`

**Supported capacity:** Hue can arrange up to **500 images**.

### Reading the two arrangements

The arrangements should be understood as two different ways of *making a collection observable*:

| Arrangement    | Organising principle                                         | Useful for exploring                                  |
| -------------- | ------------------------------------------------------------ | ----------------------------------------------------- |
| **Similarity** | Relationships between multidimensional image representations | Neighbourhoods, clusters, visual affinities, outliers |
| **Hue**        | Colour hue                                                   | Colour patterns, gradients, repetition and contrast   |

Neither arrangement reveals the single or "correct" structure of an image collection. Each foregrounds particular properties of the images while making others less visible. Switching between them is therefore part of the analysis.

### References

* van der Maaten, L. & Hinton, G. (2008). *Visualizing Data using t-SNE*. **Journal of Machine Learning Research, 9**, 2579–2605.
* Wattenberg, M., Viégas, F. & Johnson, I. (2016). *How to Use t-SNE Effectively*. **Distill, 1**(10). DOI: 10.23915/distill.00002.
* MDN Web Docs. *HSL colour notation* and *Hue*. Mozilla Developer Network.
