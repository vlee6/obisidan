First, TOTEM generates a codebook containing distinct time series patterns represented by vectors from a large (and potentially diverse in the case of a generalist model) time series data set (ie. corpus) via "self-supervised pre-training". Each vector in the codebook has a corresponding ID.

TOTEM is given time series data $T$ to analyze. TOTEM breaks $T$ into segments/tokens and converts each segment/token to a vector $v$ via a deterministic encoder (VQ-VAE?). For every $v$, TOTEM then assigns an ID to $v$ based on which vector in the codebook matches $v$ the most (presumably calculated by dot-product or cosine simularity).

Note that the codebook is developed independently from the model: the vectors created in **tokenization** to represent time series segments are NOT the same as the vectors created by the **downstream model** (ie. T5) to represent IDs. Additionally, the encoder that maps time series segments to vectors is deterministic. 


![[Drawing 2026-05-25 16.52.30.excalidraw 1|700]]

TOTEM somewhat resembles most LLMs which rely on a predefined vocabulary (a big list of words).

|                | LLMs                                                                   | TOTEM                                                                                                                                        |
| -------------- | ---------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------- |
| **Vocabulary** | Pre-defined fixed vocabulary that deterministically maps words to IDs. | Generated vocabulary (codebook) that maps time series segments/patterns represented by vectors to IDs.                                       |
| **Mapping**    | Words in input get mapped to IDs via the vocubulary.                   | Time series input is broked into segments, segments are encoded as vectors, then vectors are mapped to IDs via most similar codebook vector. |

### Potential errors in understanding:
- I'm pretty sure that the "time series patterns" don't just encode shape, but also value since that seems like important infromation. Note the difference between time series segments with ID 1 and ID 2 in the illustration above.

[Video](https://www.youtube.com/watch?v=OqrCpdb6MJk) explaining TOTEM.
[Video](https://www.youtube.com/watch?v=yQvELPjmyn0) explaining VQ-VAE, the backbone of TOTEM (the encoder used to convert data into vectors).