### High Level Explanation
The novelty and innovation of a transfomer model comes from **attention**, which essentially enables token embeddings (vectors) to develop a richer meaning by absorbing meaning from neighboring token embeddings.

For example, in the context of LLMs which take textual input and largely rely on **self-attention** (see [[Self-Attention or Cross-Attention?]]), note the following two sentences.

He deposited money in the **bank**.
He collected seashells by the river **bank**.

In a simple neural network like an RNN, the token embedding corresponding to the word "bank" in both sentences will likely be the same. 

In a transformer model, while the vector corresponding to "bank" in both sentences will be the same after encoding, after it passes each **head** of attention, it takes on a more specific meaning. In the first sentence, the vector corresponding to "bank" may be altered slightly by the vector corresponding to "money" and "depositied". In the second sentence, "seashells" and "river" may enrich the meaning of "bank". Most LLMs rely on **multi-headed attention**, preforming this process several times so that vectors represent context-rich meanings instead of singular words.

| Step          | RNN / Traditional Neural Network | Transformer                                                                                                                           |
| ------------- | -------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| Initial Input | `bank` (Vector $A$)              | `bank` (Vector $A$)                                                                                                                   |
| Processing    | Does not hold context            | Passes through multi-headed attention layers, embedding context                                                                       |
| Final Ouput   | `bank` (Same vector $A$)         | Sentence 1: `bank` (Vector $A'$ representing financial institution)<br><br>Sentence 2: `bank` (Vector $A''$ representing river slope) |
### Use case in Arithmos
The transformer architecture is the foundation for almost all mainstream models, and for good reason: the ability to embed context into words leads to better ouput.

For semiconductor manufacturing, where small errors in previous steps compound and even the slightest variations are non-neglibile, being able to capture this "context" will help us better detect anomalies.



See 3Blue1Brown's [videos](https://www.youtube.com/watch?v=wjZofJX0v4M&list=PLZHQObOWTQDNU6R1_67000Dx_ZCJB-3pi&index=8) for a more detailed explanation.