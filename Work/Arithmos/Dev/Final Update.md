# [GitHub](https://github.com/arithmos-research-development/TSFM-Research)![[Pasted image 20260909232548.png]]
![[Drawing 2026-09-09 23.46.28.excalidraw|800]]


![[Drawing 2026-09-10 18.55.18.excalidraw|800]]
# Changes Made Since Last Meeting
TLDR:
- Streamlined dataset
- Switched back to VQ
- Tuned tokenizer hyperparameters to prioritize token homogeneity in forecasting dataset

To preface, at this point in time, I was still relying on the binning tokenizer, BPE token compression, and GPT style forecasting.

As per Prof. Jin's advice, the first thing I tried was streamlining the dataset to contain only the most similar of passes. A combination of KMeans clustering and manual filtering allowed me to select 150 passes out of 2402 that were extremely similar across all sensors.
![[Pasted image 20260909203509.png]]
To narrow down the forecasting scope even further, I restricted the dataset to a handful sensors with very similar shapes, which happened to be the pressure sensors (`PRESSURIZED_CHAMBER_PRESSURE`, `MAIN_OUTER_AIR_BAG_PRESSURE`, `CENTER_AIR_BAG_PRESSURE`, and `EDGE_AIR_BAG_PRESSURE`)
![[Pasted image 20260909205723.png]]

However, this alone was not sufficient for imrpoving the forecasting results. To better diagnose the problem, I created a synthetic dataset based on sine waves to create an easily predictable, cyclic pattern. Without any noise, the predictions were nearly perfect, but once even the slightest noise was introduced, the predictions became a complete mess.

This motivated me to switch back to the VQ-VAE based tokenizer, which was significantly more resistant to noise with the downside of some artifacting. Thankfully, this was pretty straightforward because I had designed my system to be fairly modular.

The GPT-style token prediction with the VQ-VAE tokenizer yielded much better results on both the synthetic sine wave dataset.
![[Pasted image 20260909205223.png]]
With some hyperparameter tuning, the forecasting results have been overall pretty solid. Of course, there is still much to be desired with around 20% of forecasts being garbage or slightly out of phase, but I believe these could be solved with covariates and a larger dataset.
![[Pasted image 20260909210037.png]]![[Pasted image 20260909205953.png]]![[Pasted image 20260909205958.png]]![[Pasted image 20260909210007.png]]![[Pasted image 20260909210056.png]]

# Experimental Findings
**VQ-VAE based tokenizer is much more resistant to noise compared to the naive binning based tokenizer.**

The granularity of the binning based (Chronos 1 style) tokenizer causes some issues. With noise same general time series pattern might be represented by a completely different token sequence.

![[Drawing 2026-09-09 21.13.37.excalidraw|800]]
Empirically, forecasting with the binning tokenizer is garbage with the addition of any noise whereas the VQ-VAE tokenizer is much more tolerant. I theorize that having various token sequences represent the same pattern decreases forecasting performance in two ways:

1. BPE merges are less effective. A merge operation that compresses the blue curve won't compress the red curve.
2. More variation in training data. The forecaster has a more difficult time.

**Minimizing the codebook size of VQ-VAE tokenizer dramatically improved forecasts.**

I imagine that the forecaster having less options to choose from simply improves the quality of forecasts. A large codebook likely results in multiple different tokens representing similar time series patterns. Again, the more variations of tokens there are that represent the same time series patterns, the less effective BPE merges are.

Thus, if the VQ-VAE tokenizer doesn't need that many tokens to produce accurate (to a reasonable level) reconstructions, we shouldn't force it to. To supplement reducing the number of codebook vectors, we can also increase the size of the codebook vectors to capture more information.

Even if this feels unintuitive, it works. The forecasting results with 128 VQ-VAE tokens was worse because different sensors were compressed at different rates.

#### `num_codes = 16`![[Pasted image 20260909212848.png]]
#### `num_codes = 128`![[Pasted image 20260909213401.png]]

**Too many BPE tokens (ie. tokens represent groupings of VQ-VAE generated tokens) blows up forecasting mistakes whereas too little BPE tokens leads to the forecaster lazily predicting flat lines.**

![[Drawing 2026-09-09 22.47.30.excalidraw|800]]
*Too many BPE tokens*
Having a lot of BPE tokens means that a slight error in next-token prediction results in a huge discrepancy in reconstruction.

![[Drawing 2026-09-09 22.11.45.excalidraw|800]]

*Too few BPE tokens*
If there are too few BPE tokens, the same handful of tokens dominate the dataset which leads to the forecaster repeatedly predicting those tokens, resulting in flat lines.
![[Pasted image 20260818021640.png]]
The losses might be low, but the forecast results are poor. A flat line isn't very helpful in predicting machine health.
![[Pasted image 20260818024744.png]]



*Overall, **I think VQ-VAE tokenization and BPE have a lot of potential in a time series foundation model.** The compression of lengthy time series data into a short token (compressed by a factor of ~8) sequence significantly reduces context size necessary for long term time series forecasting.*

# Running the Notebook
1. Clone the repository
	`git clone git@github.com:arithmos-research-development/TSFM-Research.git`
2. Enter the repository
	`cd TSFM-Research`
3. Unzip `data.zip`
	`unzip data.zip` or using a GUI unzip tool (like 7zip)
4. Install python packages via the `pyproject.toml`
	`pip install -e .`
5. Using VSCode or your preferred Jupyter environment, view `notebooks/fabmind.ipynb` and run all cells.

# Resources
These are a selection of notes that I've taken that I think may be useful to someone just starting a similar project. I also have notes brainstorming and debugging, but those are less polished.

- [[Tokenization & Embedding]]
- [[Vector Quantization (TOTEM)]]
- [[Simple Binning (Chronos)]]
- [[Wave Quantization (WQ4TS)]]
- [[Transformer Architecture]]
- [[Covariate Forecasting]]
- [[Hosting a SSH server with WSL and NixOS, vaguely]]

# Future Steps
Obviously, there's still a lot of work to be done here. 

Most immediately, introducing new sensors has mixed results at best and more data is probably necessary for the model to make more informed predictions (ie. sensing patterns over a larger context so the prediction is not out of phase). Now that I have a better understanding of how to organize this project, I'll probably also rewrite everything from first principles before implementing any new changes. An interface besides a Jupyter noteboko

In the near future, I hope to see multivariate/covariate forecasting as well as a more robust VQ-VAE tokenizer free from artifacts.

I'd like to continue working on this project in my free time as more of a cool personal project and will try my best to keep you in the loop. 

Again, thank you for this summer!