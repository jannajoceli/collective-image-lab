# Collective Image Lab

<img width="800" height="500" alt="collectiveimagelabdemo800" src="https://github.com/user-attachments/assets/0eb84e1a-dcc1-441d-99d1-5bdc64c4a5a7" />

Browser tool for the Digital Methods Labs, King's College London. Collective Image Lab lets students load a shared collection, add their own images, and see how a set of photos organises itself — by colour and layout, by what's actually pictured (via a small on-device content model), or by hue — as a hands-on way into what 'similarity' means to different methods. Everything runs client-side; nothing is uploaded by the page itself.

Made with ♡ & ✨ by Janna Joceli Omena
Background image: Paweł Czerwiński, Unsplash.

## URLs

- Public lab: https://jannajoceli.github.io/collective-image-lab/

- Tutorial: https://jannajoceli.github.io/collective-image-lab/tutorial.html

- Video:[https://youtu.be/GIaSSKGoiKo](https://youtu.be/GIaSSKGoiKo)

## Capacity

The recommended supported capacity is **500 images per collection/canvas**:

- **Hue:** up to 500.
- **Similarity:** exact t-SNE up to 250. Above that, the interface explains
  that the quadratic calculation is too heavy and asks users to use Hue.
- **Content:** same limit as Similarity (250), since it also runs exact t-SNE.
  The first use in a session also needs a network connection, to download the
  small pretrained model that reads each image's content.
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

### Content · MobileNet embeddings

**Content** also uses t-SNE, but changes what goes into it. Where **Similarity** describes each image purely by colour — a 12×12 grid of pixel values plus a hue histogram — **Content** instead passes each thumbnail through **MobileNet**, a small convolutional neural network pretrained to recognise a broad vocabulary of everyday objects and scenes. Rather than reading MobileNet's final classification (its best guess at "cat" or "flower"), the Lab takes the layer just before that decision: a roughly 1,000-dimension description of what the network noticed in the image. That description, not a colour histogram, is what t-SNE then maps into two dimensions.

The practical difference shows up in what counts as a "neighbour." Two images with a similar colour palette but very different subjects — a portrait shot against green foliage, say, and a photograph of a forest — can end up close together under **Similarity**, because it never looks past colour. Under **Content**, they are far more likely to separate, because the underlying representation is closer to *what is depicted* than *what colour it is*. Conversely, images that look quite different in palette but share a subject (two portraits under different lighting, say) are more likely to end up as neighbours.

Content is therefore useful for asking a different question than Similarity does:

> **Which images resemble one another in subject and composition, independent of colour palette?**

Comparing **Similarity** and **Content** side by side on the same collection is a way of making that distinction concrete: the same images, organised by two different notions of "alike," rarely produce the same map.

The model (a few megabytes) is downloaded from a public CDN the first time Content is used in a session; after that, everything runs locally in the browser, the same as Similarity and Hue — images are not sent anywhere to compute this. Because of that one-time download, the first Content run in a session needs a network connection and takes a little longer than later runs or than Similarity.

**In short:**
`image → MobileNet (pretrained CNN) → content embedding → t-SNE → 2D neighbourhood map → spacing for viewing`

**Supported capacity:** like Similarity, exact t-SNE limits Content to **250 images**.

### Hue

**Hue** arranges images according to their dominant colour hue rather than their similarity across multiple visual features.

Hue describes the basic colour family of a colour, such as red, yellow, green, cyan, blue or magenta. It can be represented as a position around a circular colour wheel from 0° to 360°. Images with related hues are therefore positioned near one another according to this colour dimension.

Unlike t-SNE, Hue is not attempting to discover clusters or multidimensional similarities. It deliberately asks a much simpler question:

> **How does this image collection organise itself when colour becomes the organising principle?**

This can make colour patterns, repetitions, transitions and contrasts within a collection immediately visible. Comparing **Similarity** and **Hue** is therefore also methodologically useful: the same image collection can produce very different visual structures depending on which feature is used to organise it.

**In short:**
`image → colour measurement → hue → colour-based arrangement`

**Supported capacity:** Hue can arrange up to **500 images**.

### Reading the three arrangements

The arrangements should be understood as different ways of *making a collection observable*:

| Arrangement    | Organising principle                                    | Useful for exploring                                                | Max images |
| -------------- | -------------------------------------------------------- | -------------------------------------------------------------------- | ---------- |
| **Similarity** | Relationships between colour/pixel-based representations | Neighbourhoods, clusters, colour-driven visual affinities, outliers  | 250        |
| **Content**    | Relationships between MobileNet content embeddings        | Neighbourhoods based on subject and composition, independent of colour | 250        |
| **Hue**        | Colour hue                                                | Colour patterns, gradients, repetition and contrast                  | 500        |


### References

* van der Maaten, L. & Hinton, G. (2008). *Visualizing Data using t-SNE*. **Journal of Machine Learning Research, 9**, 2579–2605.
* Wattenberg, M., Viégas, F. & Johnson, I. (2016). *How to Use t-SNE Effectively*. **Distill, 1**(10). DOI: 10.23915/distill.00002.
* Sandler, M., Howard, A., Zhu, M., Zhmoginov, A. & Chen, L.-C. (2018). *MobileNetV2: Inverted Residuals and Linear Bottlenecks*. **CVPR 2018**, 4510–4520.
* Howard, A.G. et al. (2017). *MobileNets: Efficient Convolutional Neural Networks for Mobile Vision Applications*. arXiv:1704.04861.
* MDN Web Docs. *HSL colour notation* and *Hue*. Mozilla Developer Network.
