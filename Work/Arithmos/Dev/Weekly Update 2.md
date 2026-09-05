*(08/11/26 - 08/18/26)*
TLDR:
- Fixing dataset bugs
- Added new chronos-style binning tokenizer
- GPT prediction works, but only on cyclic, predictable data 
- Tried narrowing dataset to a handful of sensors and reducing model size 


### Bug Fixes
With how poorly the GPT forecaster performed, my first guess was that the training data may have been malformed leading to a "garbage in, garbage out" type of situation.

Unsurprisingly, I found and fixed two major issues that messed up the dataset, particularly forgetting a reset_index() when generating the DataFrame (which led to all the runs being stacked ontop instead of end to end) and a transpose when transforming the DataFrame into a tensor. The tranpose was particularly interesting since it led to each sample being like:
$$\begin{bmatrix} \begin{bmatrix} \text{sensor}_1 \\ \text{sensor}_2 \\ \text{sensor}_3 \end{bmatrix} & \begin{bmatrix} \text{sensor}_1 \\ \text{sensor}_2 \\ \text{sensor}_3 \end{bmatrix} & \begin{bmatrix} \text{sensor}_1 \\ \text{sensor}_2 \\ \text{sensor}_3 \end{bmatrix} \end{bmatrix}$$
instead of:
$$\begin{bmatrix} \begin{bmatrix} \text{sensor}_1 \\ \text{sensor}_1 \\ \text{sensor}_1 \end{bmatrix} & \begin{bmatrix} \text{sensor}_2 \\ \text{sensor}_2 \\ \text{sensor}_2 \end{bmatrix} & \begin{bmatrix} \text{sensor}_3 \\ \text{sensor}_3 \\ \text{sensor}_3 \end{bmatrix} \end{bmatrix}$$
Yet, the bugged matrix was much easier to forecast. Since each sensor is scaled by a different value, the sample becomes very cyclical and predictable. Compare this to the typical context given to the forecaster, which deviates from run to run and has itermittent pauses.

**Bugged:**![[Pasted image 20260818131323.png]]
**Fixed:**![[Pasted image 20260818131457.png]]
I also updated the dataset to also contain sensor information which can directly be passed into the GPE forecaster to utilize Anthony's sensor embeddings.
### Binning Tokenizer
In order to rule out reconstruction errors, I decided to also create a simple Chronos-style binning tokenizer. Fortunately, I had enough foresight to make my `tokenize` wrapper function (which also efficiently uses batching to speed up tokenization) easily expandable to accept several different tokenizers. The reconstructions generated from this simpler tokenizer are reasonably accurate and completely free from the ringing artifacts that plagued the VQAE based tokenizer, so for the remaining work, I've switched to it in the meantime.
![[Pasted image 20260818143821.png]]
### Working on GPT, BPE comparison
Added model saving so I could compare different models.

With the data and tokenization sorted out, I assumed that forecasting would be much better, but this wasn't the case. An overwhelming tendency to predict flat lines still persists and I'm not sure if its a good idea to brute-force penalize flat perdictions for this considering a good chunk of the sensor data is flat. I also hypothesized that **BPE might help stop predictiing flat** lines since compression results in less of the same token being repeated over and over, which I was able to prove.

The following is a comparison between a GPT trained with and without BPE, noting that the one without BPE has a forecast horizon which is four times as large. The inputs and hyperparameters are the same and the models are ONLY trained on `SLURRY_FLOW_LINE_A`.

**Without BPE:**![[Pasted image 20260818153637.png]]
**With BPE:**![[Pasted image 20260818153644.png]]
**Without BPE:**![[Pasted image 20260818153738.png]]
**With BPE:**![[Pasted image 20260818153800.png]]
The forecasts with BPE still aren't amazing, but it seems better that we're dealing with an overfitting/data starvation problem than it simply settling on a flat line.

### Working on GPT, Tuning Hyperparameters
I decided to shrink the training dataset to just the various pressure sensors (the `USAGE`s are not cyclical and the `SLURRY`s are too irregular) for now. Even though we lose a good portion of our dataset, the pressures are the most cyclical and visually "predicatable". Without a strided dataset, the model quickly starts overfitting. While the training loss can get as low as 0.3, the evaluation loss can't get under 4.

I'm still working on trying to tune the hyperparameters, now that we **seemingly solved the flat line prediction issue**. Since we have a relatively small dataset, I need to keep the GPT model pretty small. Trying to get more out of our data with striding is also a balancing act: a small stride results in overfitting (samples aren't very different from each other) but a small stride results in underfitting (not enought data).
![[Pasted image 20260819001019.png]]![[Pasted image 20260818235621.png]]
### Looking forward
Next meeting (or even sooner), hopefully we'll have an actually half-decent forecaster. I'm also working on figuring out how LSTM works to use as a comparable baseline. Trying a Google's TimesFM time series foundation model might also be interesting.
