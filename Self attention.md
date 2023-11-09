- Every word in a sequence is both a key and a query simultaneously
- Look at this from a IR perspective. 
- The key/value/query concept is analogous to retrieval systems. 
	- For example, when you search for videos on Youtube, the search engine will map your **query** (text in the search bar) against a set of **keys** (video title, description, etc.) associated with candidate videos in their database, then present you the best matched videos (**values**).
	- So, we learn Key and Query's from words, and map them to the values. 
- **Query (Q)**: Represents the current word.
- **Key (K)**: Represents every word that the query can attend to.
- **Value (V)**: Contains the information of each word, which the query will "focus on" if it decides to attend to that word.
- A score is calculated by taking the dot product of the Query vector of the word we're focused on and the Key vector of every other word in the sequence. This score determines the level of attention a word needs to pay to other words.
- To ensure the scores are not too large (leading to extremely small gradients), the scores are scaled down by dividing them by the square root of the depth of the Key vectors (commonly denoted as $d_k$
- The scaled scores are passed through a softmax function, which gives a probability distribution. This ensures the scores lie between 0 and 1 and that they sum up to 1.
- The softmax scores are used to create a weighted combination of the Value vectors. In essence, for each word, the self-attention mechanism specifies how much focus it should place on all the other words in the sequence, including itself.
- The weighted Value vectors are summed up to produce the final self-attended representation of the word.
- In practice, "multi-head attention" is used, meaning the self-attention process is run multiple times (in parallel) with different weight matrices. The resulting outputs are concatenated and linearly transformed to produce the final output. Weight matrices are randomly initialized
### Benefits
- **Contextual Representation**: Each token gets a new representation influenced by the entire context, rather than just its original embedding.
- **Long-Range Dependencies**: Self-attention allows tokens to consider other tokens irrespective of their distance. It can capture relationships between words that are far apart in the sequence.
- **Parallel Processing**: Unlike recurrent architectures, self-attention processes all tokens simultaneously, making it highly parallelizable.
### Why Multiple Heads?
- Can learn intricacies of language more: more randomly weighted heads can capture our data from multiple perspectives