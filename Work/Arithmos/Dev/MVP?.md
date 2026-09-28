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