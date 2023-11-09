[[Seq2Seq]]
## Idea
- learn a probablistic model from data
- Find best English sentence y, given French sentence x 
- $argmax_yP(y|x)$
- Use Bayes rule to break this down into 2 components
	-  $argmax_yP(x|y)P(y)$
	-  $P(x|y)$ -> translation model. models how words and phrases should be translated from parallel data (source, target) pairs
	- $P(y)$ -> language model. Models how to write good English. Learnt from monolingual data
## Learning alignment
- How do we learn translation model $P(x|y)$ from the parallel corpus?
- Break it down even further  $P(x, a|y)$ where a is the alignment, i.e. word-level correspondence between French sentence x and English sentence y 
- Alignment can be complex
	- Many to one-> many words map to one
	- One to many -> one word maps to many 
	- Many to many -> phrase to phrase
- We learn $P(x, a|y)$ as a combination of many factors including
	- Probability of particular words aligning
	- Probability of particular words having particular fertility
## Decoding
- How do we compute $argmax_yP(x|y)P(y)$?
	- We could enumerate every possible y and calculate the probability -> too expensive
	- Answer: use a heuristic search algorithm to search for the best translation, discard hypotheses that are too low probability
	- This process is called decoding 
- $P(y|x) = P(y_1|x) P(y_2|y_1, x) P(y_3|y_1, y_2, x) \dots P(y_T|y_1, \dots , y_{T-1}, x)= \prod_{t=1}^{T} P(y_t|y_1, \dots , y_{t-1}, x)$
- We could try computing all possible sequences y
	- This means that on each step t of the decoder, we are tracking V^t possible partial translations, where V is the vocab size
	- This O(V^t) complexity is far too expensive
## Beam Search
- Core idea: on each step of decoder, keep track of the k most probable partial transitions (hypotheses)
	- k is the beam size which in practice is around 5 to 10
	- ${score}(y_1, \dots , y_t) = \log P_{LM}(y_1, \dots , y_t|x) = \sum_{i=1}^{t} \log P_{LM}(y_i|y_1, \dots , y_{i-1}, x) ]$
	- Scores are all negative and higher score is better
	- We search for high-scoring hypotheses, tracking top k on each step
	- For each of the k hypotheses, find the top k next words and calculate scores
	- Backtrack to obtain the full hypothesis
- Stopping criterion
	- In greedy decoding, we decode until the model produces $<END>$ token
	- In beam search decoding, different hypotheses may produces $<END>$ tokens on different timesteps 
		- When a hypothesis produces $<END>$, that hypothesis is complete
		- Place it aside and continue exploring other hypotheses via beam search
	- Usually we continue until
		- We reach timestep T
		- We have at least n completed hypotheses (n is predefined)
- Problem: longer hypotheses have lower scores
- Fix: normalize by length by dividing by t. $\frac{1}{t}\sum_{i=1}^{t} \log P_{LM}(y_i|y_1, \dots , y_{i-1}, x)$ 

