Self-attention can be incorporated into different components of a Transformer model, namely the encoder, the decoder, or both. Here's how self-attention is applied in each scenario:

### 1. **Encoder-Only Models (e.g., [[BERT]])**:
- The model consists of stacked encoder layers.
- Each encoder layer uses self-attention. Every token in the input sequence can attend to every other token, including itself.
- This setup allows each token to gather information from the entire sequence, providing a contextualized representation for each token in the output.

### Self-Attention Mechanism:
- Query (Q), Key (K), and Value (V) vectors are computed for every token in the sequence.
- The attention scores are computed, scaled, and then passed through a softmax function to get the attention weights.
- The output is a weighted sum of the Value vectors based on these attention weights.

### 2. **Decoder-Only Models (e.g., [[GPT-3]])**:
- The model consists of stacked decoder layers.
- In the decoder's self-attention mechanism, to ensure causal (or autoregressive) behavior, tokens can only attend to previous tokens or themselves. This prevents information flow from future tokens.
  
### Masked Self-Attention:
- The self-attention mechanism is the same as in the encoder, but with an added masking step.
- A mask is applied to the attention scores before the softmax step, ensuring that a token doesn't have access to future tokens in the sequence.

### 3. **Encoder-Decoder Models (e.g., [[T5]])**:
- Consists of both encoder and decoder stacks.

#### Encoder:
- Similar to the encoder-only model, every token in the input can attend to every other token in the input sequence.

#### Decoder:
- Contains two types of attention mechanisms in each layer:
  1. **Masked Self-Attention**: Similar to the decoder-only model, where tokens can only attend to previous tokens to ensure causality.
  2. **Encoder-Decoder Attention**: After the masked self-attention layer, the decoder has another attention layer where the Queries (Q) come from the current decoder state, and the Keys (K) and Values (V) come from the encoder's output. This allows the decoder to focus on relevant parts of the input sequence, much like traditional seq2seq models with attention.

### Summary:

- **Encoder-Only**: Uses self-attention where each token attends to all tokens in its own sequence.
- **Decoder-Only**: Uses masked self-attention to ensure tokens can't see future tokens, maintaining autoregressive behavior.
- **Encoder-Decoder**: The encoder uses standard self-attention. The decoder uses both masked self-attention and an additional attention layer that attends to the encoder's output.

In all these scenarios, multi-head attention can be utilized to enable the model to focus on different parts of the input simultaneously, capturing various relationships and dependencies.