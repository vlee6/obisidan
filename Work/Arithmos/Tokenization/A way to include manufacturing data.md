Looking at some of the use cases for Google's [T5](https://en.wikipedia.org/wiki/T5_(language_model)) transformer, I noticed that it could be used for various tasks with the inclusion of specific tokens (ie `<x>` and `Translate`).

> - restoring corrupted text: `Thank you <X> me to your party <Y> week.` -> `<X> for inviting <Y> last <Z>`, where the `<Z>` means "end of output", and the `<X>` and `<Y>` denote blanks to be filled, called "sentinels" in the original report.
> - translation: `translate English to German: That is good.` -> `Das ist gut.`.
> - judging the grammatical acceptability of a sentence ([CoLA](https://en.wikipedia.org/wiki/Corpus_of_Linguistic_Acceptability "Corpus of Linguistic Acceptability") sentence): `The course is jumping well.` -> `not acceptable` .

This suggests that we can inject process data to our tokenized time series data by simply including some extra tokens at the start.
### For example
For CMP data, we add a token `1234` at the start of the time series data. For etching data, we add a token of `5678` at the start of the time series data. As long as we keep it consistent in our training data, this should work.