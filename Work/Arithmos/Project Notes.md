In summary:
- We want a transformer model and tokenization strategy that caters for forecasting.
- Figure out how to process multivariate data. A robust vocabularly for tokenization is necessary, one where sensors can be added or removed.
- Figure out a way to encode the step in semiconductor fabrication being done at any given time.
- Maybe event based tokenization to handle shifts and longer and shorter cycles times
- Look into vector reconstruction to validate.

Questions:
- [ ] Should we choose a transformer that relies on [[Self-Attention or Cross-Attention?]]
- [ ] Should we choose a transformer that is [[Encoder-Decoder or Decoder-Only?]]
### "Forcasting" task subtleties
LLM generate text by simply predicting the next token. In a similar sense, various time series tokenization methods allow us to forecast time series data. Many papers categorize these "predict next token" tasks as **forecasting** tasks. But if our tokens represent sensor data, a forecasting task implies we're predicting future sensor data, not specific information about when repairs are needed or whether a manufacturing cycle will be successfull.

Instead, if we want to answer questions like "will there be a manufacturing fault" or "when should I service this machine", this aligns better with what is typically described as an **anomaly detection** task. For example, following typical anomaly detection training, we could train the model to understand what "normal" sensor data looks like (ie. data corresponding to a successful manufacturing cycle) and what an anomaly looks like (ie. data corresponding to failures or when maintenance is required). This distinction is mostly semantic, but it is important to keep this  in mind when choosing a pre-trained transformer model and tokenization strategy.

Drift detection == anomaly detection
### Forcasting Tasks vs Anomaly Detection Tasks
It appears that the [[Transformer Architecture]] commonly seen in LLMs (ie. predicting next token) applies more to forecasting tasks than anomaly detection. [[Simple Binning (Chronos)]] has specifically been tested on univariate time series forecasting (Chronos 4) and [[Vector Quantization (TOTEM)]] is able to do anomaly detection with the tokenizer alone.

Regardless of time series tokenization, I am unsure how exactly the transfomer solves the anomaly detection, but it is possible.

The Chronos example code uses Google's Text-to-Text Transfer Transformer (T5) for univariate forecasting, but T5 is also capable of "decision" tasks such as [Corpus of Linguistic Acceptability (CoLa)](https://en.wikipedia.org/wiki/T5_(language_model)), likely using the same decoder as other tasks. Subsequently, anomaly detection might just be a change in training. I'm imagining a dataset containing the sensor data of various batches as a series of numbers, and then some quality or success metric as a singular number.
### Virtual Metrology
In semiconduction manufacturing, virual metrology seeks to predict the quality of a silicon wafer based on sensor data. Again, this feels more like an anomaly detection task than a forecasting task.
### Foundation Models
The goal with Arithmos is to develop a model that can preform these anomaly detection tasks (among others) while taking in data from various steps in the semiconductor manufacturing process, agnostic of who made the machine used at each step. Thus, the model must be trained on a large and diverse data set (different steps of the process, different machines, different textual input) to be a generalist--a foundation model.


Total ts points: 13485456
Total points in dataset 13296640
holy fucking shit i had the wrong ravel this whole time what did that effect though

#### Original, all sensors
missed a transpose
26 epochs to diverge? (so 25 is enough)

#### Just `SLURRY_FLOW_LINE_A`, with `BPE (1024)`
50 epochs to diverge
![[Pasted image 20260818031806.png]]![[Pasted image 20260818012251.png]]
Is it possible that this sensor data isn't very cyclical?
![[Pasted image 20260818012322.png]]Looking at one block size, it seems pretty difficult to predict what will happen last. BPE compression also means that one wrong token leads to completely wrong decoded predictions.
![[Pasted image 20260818012912.png]]![[Pasted image 20260818013330.png]]![[Pasted image 20260818013350.png]]![[Pasted image 20260818013408.png]]
No doubt, with a synthetic dataset that repeats predictably, this would be a lot easier.

#### Just `SLURRY_FLOW_LINE_A`, without `BPE`
Forecast horizon needs to increase a bunch and predictions tend to be more flat. Much slower training times too (which makes sense), but seems to settle after less epochs (around 40).
![[Pasted image 20260818024744.png]]![[Pasted image 20260818021640.png]]![[Pasted image 20260818021836.png]]
might be some overlap between train and eval dataset. try a pass based dataset next

upon further inspection, some of the pressure sensors (retainer ring and ripple air bag) seem off

Modify both datasets to take "PASS_ID"

BPE is very susceptible to anomalies. If the evaluation dataset differs even slightly from the training dataset, the tokens generated after BPE are completely different which results in poor forecasts.