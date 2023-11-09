- **Precursor**: GPT2 which was trained on 40 GB of text and had 1.5 billion parameters
- Could generate fluent and coherent sentences back to back which was unseen at the time
## GPT-3: Mid 2020
- 175B parameters, 96 layers, 96 heads, 12k dimensional vectors
- Proposed an alternative to fine-tuning: **in context learning**
	- Uses LLM off the shelf, no gradient updates
	- Key idea: a LLM should be able to continue an observed pattern
	- P(yn | y1,..., yn-1)
		- LLM needs to associate examples together to do ICL
- Few shot learning only works with huge models 
## In-Context Learning Induction Heads (Olsson et al 2022)
### Background
- There are mechanisms in transformers to do fuzzy or nearest neighbors versions of pattern completion
- Induction heads: a pair of attention heads in different layers that work together to copy or complete patterns 
- The first head copies information from the previous token into each token
- The second attention head to attend to tokens based on what happened before them 
- These two heads work together to cause the sequence {A}{B}...{A} to be likely completed with {B}
- Associate what I am seeing now in my label X back with a previous label Y which *might* be the label 
### Induction Heads
1. Run each model over the same set of multiple dataset examples, collecting one token's loss per example
2. For each example, extract the loss of a consistent token. Combine them to make a vector of losses per model
3. The vectors are jointly reduced with principal components
- Characterize performance by ICL score: loss(500th token) - loss(50th token) - average measure of how much better the model is doing later once it's seen more of the pattern
- Model does better job modelling later in the sequence because it'll remember things from previous in the tokens 


