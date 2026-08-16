    nn.Conv1d(1, 8, kernel_size = 3, stride = 1, padding = 1)e
    nn.Conv1d(8, 16, kernel_size = 3, stride = 1, padding = 1),
    nn.Conv1d(16, 24, kernel_size = 3, stride = 1, padding = 1),
    nn.Conv1d(24, 32, kernel_size = 3, stride = 1, padding = 1),

ViT bridge
![[Pasted image 20260620132918.png]]

No ViT bridge, regular VQ, 256 size 1 embeddings per sample
![[Pasted image 20260620133223.png]]

No brige, rvq 4 codebooks but 4 downsampling, 64 size 4 embeddings per sample, downscaling first
![[Pasted image 20260623094942.png]]

- Lowering codebook embedding dimension did not really help
- Likely need to discard first and last chunks of data since reflecting padding didn't really help

Is residual VQ even a good idea? If we have $k$ codebooks, we end up getting $k$ indices per embedding, which means $k$ tokens per embedding. Increased codebook resolution doesn't even seem necessary since codebook usage is already pretty low. Reconstructions seem to better follow curves?

Is a prediction even necessary? With autoencoders, simply training the autoencoder on the correct dataset already gives us capabilities to do anomaly detection.
- Train autoencoder on correct dataset
	- Reconstructions on correct data are accurate
	- Reconstructions on incorrect data are not accurate

This does go against the idea of a generalized time series model though.

one hut encoding

test reconstructions across different chambers. train on one chamber and then test on another