### Self-Attention Mechanism
For one head of attention:

1. Tokens are represented by embedding vectors that encode the particular word and its position, without any context. Call each of these embedding vectors $\vec{E}_i$.
2. **Generate query matrix $\vec{Q}_i$ for each token:** Each embedding vector is multiplied by a query matrix $W_q$ (with a smaller dimension than the embedding vector) to get a query vector, $\vec{Q}_i$, for each token.
3. **Generate key matrix $\vec{K}_i$ for each token:** Each embedding vector is multiplied by a key matrix $W_k$ (with the same smaller dimension as the query matrix) to get a key vector, $\vec{K}_i$, for each token.
4. **Generate value $\vec{V}_i$ for each token:** Each embedding vector is multiplied by a value matrix $W_v$ (but with the same dimension as the embedding vector), to get a value vector, $\vec{V}_i$, for each token.
5. For every key query pair $(\vec{Q}_i,\vec{K}_i)$, take the dot product of $\vec{Q}_i$ and $\vec{K}_i$. The higher the value of $\vec{Q}_i \cdot \vec{K}_i$, the higher that the particular token corresponding to $\vec{K}_i$ "attends to" the token corresponding to $\vec{Q}_i$.
6. We apply softmax to these dot products in order to get a probability distribution of how much each token attends to another token. If masking is required, key query pairs where the key token is after the query token are set to negative infinity, and then softmax is applied. The probability distribution we end up with is called the **attention pattern**. The size of the attention pattern is called the **context size**.
7. For every token corresponding to a query matrix $\vec{Q}_i$, call this particular token $t$ with embedding vector $\vec{v}_t$: Compute the sum of the value vectors for all the vectors in our context size multiplied by their corresponding wieght in the attention pattern. This sum is the change that is then applied (added) to the embedding vector $\vec{v}_t$ to give $t$ a richer meaning.

In **multi-headed attention**, this process is applied several times.

![[Pasted image 20260526093732.png]]

See [3blue1brown](https://youtu.be/eMlx5fFNoYc?t=287) for an example.

### Self-Attention vs. Cross-Attention
Self-Attention has the keys and queries made from the same data. Cross attention has the keys and queries made from different data. For example, an transformer for translating English to French may use embedding vectors representing English tokens to generate its queries while using embedding vectors representing French tokens to generate its keys. 

Basically, if we're working with two different types of data (audio to text, English to French, text to image), cross-attention seems to work better than self-attention. In the case of anomaly detection, cross-attention may be more effective.