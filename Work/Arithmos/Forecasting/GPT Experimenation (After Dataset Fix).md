![[Pasted image 20260823160219.png]]
```python
forecasting_config = GPTConfig(
    num_epochs=1000,
    batch_size=16,
    block_size=128,
    lr=1e-4,
    emb_dim=128,
    n_heads=2,
    n_layers=2,
    dropout=0.1,
    vocab_size=256,
)
```

![[Pasted image 20260824094442.png]]
```python
tokenizer_config = TokenizerConfig(
	...
    num_codes=128,
	...
)

forecasting_config = GPTConfig(
    num_epochs=100,
    batch_size=32,
    block_size=256,
    lr=3e-5,
    emb_dim=128,
    n_heads=2,
    n_layers=2,
    dropout=0.2,
    vocab_size=256,
)

tokenizer = Binning(tokenizer_config.num_codes, min=-1, max=6)


```

Underfitting, increasing `n_heads` and `n_layers`. Might be at the point where tuning hyperparameters actually improves the model.
![[Pasted image 20260824104002.png]]
```python
forecasting_config = GPTConfig(
    num_epochs=100,
    batch_size=32,
    block_size=256,
    lr=3e-5,
    emb_dim=128,
    n_heads=4,
    n_layers=4,
    dropout=0.2,
    vocab_size=256,
)
```

Increasing `n_heads` and `n_layers` doesn't seem to be doing anything. Will increase embedding dimension now. Reappareance of the flat line problem, increasing BPE.

![[Pasted image 20260824175124.png]]
```python
tokenizer_config = TokenizerConfig(
	...
    num_codes=64,
	...
)

forecasting_config = GPTConfig(
    num_epochs=100,
    batch_size=32,
    block_size=128,
    lr=3e-5,
    emb_dim=354,
    n_heads=6,
    n_layers=6,
    dropout=0.2,
    vocab_size=512,
)

```

Fixed flat line problem but now we're underfitting. Try random shuffling dataset and increasing stride.



![[Pasted image 20260824204308.png]]If we don't have a strong enough BPE we have low losses by just predicting flats.


![[Pasted image 20260825093705.png]]Why is the second one always messed up? Is this why things aren't working?

IMO: the most significant hyperparameter is the number of BPE merges. To few merges, these cyclic flat patterns dominate the dataset, so predictions cheaply settle to flat lines. Too many merges and the model starts underfitting and gets confused on what to do.

![[Pasted image 20260825111134.png]]