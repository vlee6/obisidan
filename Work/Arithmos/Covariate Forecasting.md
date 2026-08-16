### Chronos 2 Multivariate method
[Chronos 2](https://github.com/amazon-science/chronos-forecasting/blob/main/notebooks/chronos-2-quickstart.ipynb) is a general model able to do covariate and multivariate forecasting. New covariates for different subjects can be added and applied to predict different things. How do they do this?
- Crosss attention between target variable (thing to be predicted), and covariates.

Chronos 2 is meant for prediciton tasks that don't have the same level of granularity as semiconductor fab. 

In a traditional cnn, dimensions are: (batch size, num input channels / num sensors, input_length)

In a transformer, dimensions are: (batch size, sequence length / num tokens, hidden dimension)

**for multivariate/covariate:** to do self attention across each indvidual "sensor" in the time series, chronos consolidates the sensor dimension in the batch dimension. to do "cross attention", chronos restructures its data such that the length of the sequence gets combined in the batch dimension, and the sequence becomes chunks of different sensor (ie, chunks of sensor 1, 2, and 3 that occur at the same time point arranged horizontally)


does chronos 2 output a single continuous number or does it output one of the discrete pattersn

![[Drawing 2026-06-30 09.20.41.excalidraw|700]]
### TOTEM Multivariate Organization
Paper claims that tokenize each sensor individually and then they "stack" token sequences to be fed into the pretrained-for-LLM transformer (GPT2 in their case).

Given tokens `x1`,`x2`,`x3`,`x4` and `y1`,`y2`,`y3`,`y4` where `x` and `y` are different sensors, the final token sequence that gets fed into the transformer is something like:

`x1,x2,x3,x4,y1,y2,y3,y4`

Where each token has a positional and sensor embedding. My guess is that the sensor embedding is only to distinguish between different sensors, not enough to encode information about the specific sensor itself. 

Also use RevIN for their normalization.

Potential cons:
- Reconstruction loss
- Attention mechanism feels less rob

![[Drawing 2026-07-14 08.32.36.excalidraw|700]]
### 

### MVP organization

**config.py**
- variables to configure everything

**dataset.py**
- tokenizer dataset class that can be used to train the autoencoder and evaluate it
- prediction dataset class (maybe create own synthetic covariate data)

**tokenizer.py**
- encoder, decoder
- something that takes in a dataset
- training loop
- something that can spit out reconstruction visualizations




recipe A and B dont work. stage B is always recipe B. some just dont have a recipe B / stage B

- [ ] could base recipe off of peaks in stage B. need to find relationship between num peaks in stage B and num peaks in stage A. some wafers only have a stage A or stage B.
- [ ] dont forget to employ sliding window to ensure that the start and ends of the tokenization are good
- [ ] look into RevIN normalization, probably put it in the autoencoder 

Learning rate 1e-4
![[Pasted image 20260707105224.png]]

we want to predict a big horizon, so we need to find a good way to compress.

how can we create non evenly sized tokens? like a token representing one flat line at a certain y level

BYTE PAIR ENCODING!!!

input -> token sequence -> smaller token sequence after byte pair encoding -> transformer --> unpack BPE --> decode


\[1,1,1,1,1,2,2,3,3,3,3,2,2,1,1,1\]
Vocab is (1,2,3), sequence length is 16
Most common pair is (1,1), replace with 11
\[11,11,1,2,2,3,3,3,3,2,2,11,1\]
Most common pair is (2,2), replace with 22
\[11,11,1,22,3,3,3,3,22,11,1\]
Most common pair is (3,3), replace with 33
\[11,11,1,22,33,33,22,11,1\]
Most common pair is (11,1), replace with 111
\[11,111,22,33,33,22,111\]
Most common pair is (33,33), replace with 3333
\[11,111,22,3333,22,111\]
Vocab is (11,111,22,3333), sequence length is 6

model = QuantizedAutoEncoder(
    input_size=tokenizer_config.input_size,
    dim=tokenizer_config.dim,
    codebook_size=tokenizer_config.num_codes,
    rotation_trick=tokenizer_config.rotation_trick,
    ema_update=True,
    learnable_codebook=False,
).to(device)

With no downsampling
![[Pasted image 20260712133309.png|1000]]


![[Pasted image 20260713110728.png|1000]]
![[Pasted image 20260713122048.png|  1000  ]]
- keeping device out of data.py

![[Pasted image 20260804095715.png]]![[Pasted image 20260804095723.png]]
![[Pasted image 20260804100121.png]]
bpe corpus is front half of dataset in binning?

the fact that binning works and the forecasting samples actually look cyclical suggests that there may be some weirdness going on for the QAE (probably the batches are getting interleaved somehow). Need to test with something simple like a sine wave.

![[Pasted image 20260815033601.png]]