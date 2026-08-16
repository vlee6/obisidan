I'm referring to the concept of reducing the number data points through either average pooling or convolutions (NOT BPE) as "downsampling".
### QuantizedAutoEncoder
Pros:
- Theoritically possible to train autoencoder with lossless reconstructions. Neighboring indices should accurately fill in information lost from downsampling in reconstruction.

Cons:
- Difficult to train a autoencoder. Ringing artifacts around large steps, noisy regions are flatlined.

### Binning
Pros:
- No artifacting.
- Simpler quantization should lend itself to binning. Flat lines are straightforwardly represented by a repitition of the same token.

Cons:
- Diagonal lines look worse compared to QAE.
- Normalization and bins mean large spikes in data are lost.
- Naive upsampling doesn't lead to as good as reconstruction compared to QAE. No way to make up the information besides averaging.

We don't necessarily need to downsample to compress our token sequences since we have BPE (a reversible compression method which increases vocab size). If downsampling isn't necessary, Binning makes the most sense.