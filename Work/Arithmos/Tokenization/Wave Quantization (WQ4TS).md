### Wavelet Transforms
Given an input curve, a fourier transform outputs a curve (x: frequency, y: amplitude) that exists in the frequency domain, capturing only frequency data. Thus, the fourier transform loses time information.

Wavelet transforms, on the other hand, outputs a surface (x: time, y: frequency, z: amplitude) representing the frequencies present at any given time for an input curve, capturing both freuqency and time.

Wavelet transforms are done by using a **mother wavelet**.
- Take different frequencies of the mother wavelet.
- See how much each frequency of the mother wavelet matches the curve at a given time.

See [this video](https://www.youtube.com/watch?v=jnxqHcObNK4) for a better understanding of wavelet transforms.

The output surface of a wavelet transform is typically a set of wavelet coefficients. WQ4TS, similar to [[Simple Binning (Chronos)]], bins the sequence of coefficients, thus assigning each coefficient an ID. Like all of the other tokenization methods, the output is a sequence of IDs.
### Potentiall errors in understanding
- I think I have a good grasp of wavelet transforms and binning feels plausible, but I think I need to look deeper into the implementation of WQ4TS to better understand it.
- Need to make graphic