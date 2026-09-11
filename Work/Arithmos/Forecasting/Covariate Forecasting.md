### Chronos 2 Multivariate method
[Chronos 2](https://github.com/amazon-science/chronos-forecasting/blob/main/notebooks/chronos-2-quickstart.ipynb) is a general model able to do covariate and multivariate forecasting. New covariates for different subjects can be added and applied to predict different things. How do they do this?
- Crosss attention between target variable (thing to be predicted), and covariates.

Chronos 2 is meant for prediciton tasks that don't have the same level of granularity and length as semiconductor fab. 

In a traditional cnn, dimensions are: (batch size, num input channels / num sensors, input_length)

In a transformer, dimensions are: (batch size, sequence length / num tokens, hidden dimension)

**for multivariate/covariate:** to do self attention across each indvidual "sensor" in the time series, chronos consolidates the sensor dimension in the batch dimension. to do "cross attention", chronos restructures its data such that the length of the sequence gets combined in the batch dimension, and the sequence becomes chunks of different sensor (ie, chunks of sensor 1, 2, and 3 that occur at the same time point arranged horizontally)

![[Drawing 2026-06-30 09.20.41.excalidraw|700]]
### TOTEM Multivariate Organization
Paper claims that tokenize each sensor individually and then they "stack" token sequences to be fed into the pretrained-for-LLM transformer (GPT2 in their case).

Given tokens `x1`,`x2`,`x3`,`x4` and `y1`,`y2`,`y3`,`y4` where `x` and `y` are different sensors, the final token sequence that gets fed into the transformer is something like:

`x1,x2,x3,x4,y1,y2,y3,y4`

Where each token has a positional and sensor embedding. My guess is that the sensor embedding is only to distinguish between different sensors, not enough to encode information about the specific sensor itself. 

Also use RevIN for their normalization.

Potential cons:
- Reconstruction loss
- Attention mechanism feels less robust

![[Drawing 2026-07-14 08.32.36.excalidraw|700]]