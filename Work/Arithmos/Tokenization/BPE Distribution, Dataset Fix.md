Poor model results may be a result of the train and eval datasets being to different. Since BPE is trained solely on the train dataset, the tokens in train and eval might not be the same.

*BPE fills in the difference between `num_codes` (number of bins in Binning quantizer) and `vocab_size` (token vocabulary seen by GPT)*

No BPE, baseline:![[Pasted image 20260822210026.png]]![[Pasted image 20260822210035.png]]Token distributions already look kind of different?


`num_codes = 256, vocab_size=1024`
`bpe_corpus` is the first 50000 data points in each sensor. Total size is 200000, 2m41s to train BPE
![[Pasted image 20260822162625.png]]![[Pasted image 20260822162629.png]]![[Pasted image 20260822164757.png]]

`num_codes = 256, vocab_size=1024`
`bpe_corpus` is the first 100000 data points in each sensor. Total size is 400000, 5m9s to train BPE
![[Pasted image 20260822163406.png]]![[Pasted image 20260822163409.png]]![[Pasted image 20260822163740.png]]
`bpe_corpus` is the first 200000 data points in each sensor. Total size is 800000, 5m9s to train BPE
![[Pasted image 20260822170223.png]]![[Pasted image 20260822170233.png]]![[Pasted image 20260822171429.png]]
`bpe_corpus` is all the points in the training dataset. Total size is 3373056 (~4x greater than last), 40m28s to train BPE
![[Pasted image 20260822203444.png]]![[Pasted image 20260822203456.png]]![[Pasted image 20260822203947.png]]

**BPE might not be something that needs to be directly tuned to improve losses...**
However, changing other hyperparameters (like `vocab_size`) may cause BPE to compress the train and eval dataset differently, leading to wildly divergent patterns in the training and eval loss.

![[Pasted image 20260822221926.png]]![[Pasted image 20260822221930.png]]![[Pasted image 20260822221917.png]]
# Fixing the Eval and Training Datasets
The token distribution of the eval and training datasets were very different, regardless of how many BPE tokens there were and the size of the BPE corpus. This was because the training dataset is created from the csv files found in `phm2016/CMP-data/training` and the test dataset from `phm2016/CMP-data/test`.

I thought that the training and test csv files would be similar, **but they aren't!** The result is that the eval and training datasets are different enough that the eval loss would plateau much quicker than the training loss.

By interleaving the training and testing csvs first and then splitting them into a training and test DataFrame, the token distributions of the test and eval datasets are much more homogenous and the eval losses more closely match the training losses.

I'm not sure why the training and test csvs in the PHM data challenge would be so different from each other. It's very possible that they aren't super different, but the Binning tokenizer simply exacerbates the difference (since a slight vertical shift results in completely different tokens). Maybe this is another reason to reexamine at the VQVAE based tokenizer?

**Homogenous Training and Eval Dataset:**![[Pasted image 20260823154607.png]]![[Pasted image 20260823154610.png]]![[Pasted image 20260823154638.png]]