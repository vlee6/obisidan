- Lower dropout to `0.1` or `0.0`
- Trying experiementing with different strides.

- Try experimenting with different vocabularly sizes and BPE merges
- Try experimenting with different learning rates

# Stride
```python
forecasting_config = GPTConfig(
    num_epochs=50,
    batch_size=16,
    block_size=128,
    lr=1e-4,
    emb_dim=128,
    n_heads=4,
    n_layers=4,
    dropout=0.1,
    vocab_size=1024,
)
```

| Stride           | Training Graphs                      |
| ---------------- | ------------------------------------ |
| 256              | ![[Pasted image 20260821183605.png]] |
| 512              | ![[Pasted image 20260821185036.png]] |
| 1024             | ![[Pasted image 20260821190006.png]] |
| 1024, 100 epochs | ![[Pasted image 20260821192650.png]] |
Larger stride, less overfitting but may require more epochs of training.

Fixed: ~~Stride might be causing the eval dataset to bleed into the training dataset, which leads to the eval and training loss curves looking more and more similar. Easily fixed by simply creating two dataframes and creating seperate eval and training Pytorch dataset objects instead of creating one and splitting it.~~
# Dropout
Randomly disables some neurons during training to prevent overfitting. Need to actually see some overfitting before using this.

Don't forget `with forecasting.eval()` to disable dropout in eval.

# Learning Rate
Zifeng: change learning rate if theres crazy oscillations. In current model it looks ok?

# Block Size, BPE
Block size is far too large since it's in tokens rather than actual time series points. Plotting out the inputs being fed into GPT during training shows that they `6 * tokenizer.input_size` is  way too large.
![[Pasted image 20260820130646.png]]
BPE is trained on the only the training dataset (and a small subset of it at that). Currently, token sequences used for training are much more compressed than the token sequences used for evaluation. Need to carefully fine tune tokenizer's `num_bins` and BPE's `num_merges` or feed more data into BPE in order to balance training and eval compression.

512 bins and 512 merges; training token sequences were compressed by around a factor of 8 and eval token sequence were not compressed at all.![[Pasted image 20260821005432.png]]
**Generalize BPE**. Switch BPE to randomly sample (without breaking passes) instead of first 50000 data points per sensor out of 891205.

`num_bins = 256`, `num_merges = 1024-256`

**Eval**![[Pasted image 20260821183903.png]]**Train**![[Pasted image 20260821183914.png]]
Drop BPE?

Remember that context size is a huge bottleneck for model. BPE is probably necessary. Need to set up SSH server on Alex's PC with 12GB(?) VRAM.

No BPE is also way slower and risks the flat-line problem.

# Number of heads and layers
`n_layers` controls the number of transformer blocks (communication followed by computation)
`n_heads` controls the number of attention heads. EX: Instead of a singular 32 dimensional attention head, have 4 8 dimensional attention heads. See [Karpathy](https://youtu.be/kCc8FmEb1nY?t=4947).

Should scale with size of data? Without stride and high compression -> smaller heads and layers. With sttride and low/no comrpession --> more heads and layers.

# Current Model
```Python
forecasting_config = GPTConfig(
    # TODO: Find some good hyperparameters
    num_epochs=50,
    batch_size=16, 
    block_size=1536,
    lr=3e-4,
    emb_dim=64,
    n_heads=2,
    n_layers=2,
    dropout=0.0,
    vocab_size=1024 # BPE fills in remaining codes
)
# NO BPE
```
![[Pasted image 20260821024952.png]]![[Pasted image 20260821025157.png]]![[Pasted image 20260821025316.png]]
Since we aren't doing BPE, the flat line issue reappears. Need to generalize BPE before anything else.

# Training
![[Pasted image 20260822215339.png]]
Examining some of the training forecasts:
![[Pasted image 20260822215405.png]]![[Pasted image 20260822215410.png]]![[Pasted image 20260822215416.png]]![[Pasted image 20260822215435.png]]