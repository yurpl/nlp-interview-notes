- LLMs are becoming huge. When we fully fine-tune, we need to load them to memory
- LoRA - fine tune models with only a fraction of a cost 
- Reduces the number of trainable parameters
- A layer in a NN is a f{(W+dW)x + b}, where W is a weight matrix (parameter)
- Every matrix has a rank
	- Rank: how many linearly independent columns in matrix
	- If we remove linearly dependent column we reduce dimension, but do not lose information since we can get linear dependence from other matrices
	- Do not need to optimize full rank high dimensional matrix
	- We reduce dimensionality of matrix and decompose it into BA 
	- Hyperparameter: r, which is the rank of the matrix 
		- too low, we reduce too much and lose information
		- too high, we keep too many parameters and waste computation
	- After we find these weights, we add them to the frozen weights of the model 
## Existing solutions?
- Adapters introduce an increase in latency and adapter layers have to be processed sequentially -> bad for online inference
- Directly doing prompt or prefix tuning is difficult to optimize. Also, reserving a part of the sequence takes up valuable token length

![[Pasted image 20231016165503.png]]

