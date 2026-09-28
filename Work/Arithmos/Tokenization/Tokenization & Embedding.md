**Tokenization** is the process of breaking down input into smaller chunks (and then often assigning each of theses chunks an ID). This happens **outside** the model.

**Embedding** is the process of assigning an ID to a vector. This happens **inside** the model.

A model like T5 **takes in a list of token IDs**. After the embedding process, we end up with vector representations, to which position can also be encoded via vector addition.

A **token** is a small chunk of input, NOT a vector. The more accurate term for the vector produced after embedding are "vector representations", "token embeddings", or "dense vectors".

The important part is that after embedding, both continuous time series sensor data and textual input are represented as vectors. This common language, along with [[Transformer Architecture]], enables us to use both types of input for anomaly detection or forcasting.

### Time Series Tokenization
It's straightfoward to tokenize textual input by simply breaking down the text into tokens (indvidual words or parts of words) and simply mapping each token to an ID. Time series data, such as a graph of temperature over time, is less intuitive.

![[Drawing 2026-05-25 16.52.30.excalidraw 2|700]]

We have currently seen and understood the following methods to tokenize time series data:
- [[Simple Binning (Chronos)]]
- [[Vector Quantization (TOTEM)]]
- [[Wave Quantization (WQ4TS)]]