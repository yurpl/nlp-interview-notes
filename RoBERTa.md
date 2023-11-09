1. Trained on more data than [[BERT]]
2. Longer training with larger batch size and sequences
3. Removed the next sentence prediction objective which increased performance
4. Dynamically masked words in the training instead of static
	1. Masking is not the same for each epoch
5. Uses BPE instead of WordPiece tokenizer