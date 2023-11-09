- Also known as cost or objective function 
- Quantifies how well a model's predictions match the true labels in the training data 
- Assigns a numerical value to the difference between predicted and gold outputs 
- Goal is to minimize the loss, which in turn improves model
## SmoothL1Loss (Regression)
- Also known as Huber Loss
- Combines properties of L1 and L2 loss
- Less sensitive to outliers than L2
- Quadratic for values close to 0, linear for values far from zero making it smooth
- Prevents exploding gradients
- $l_n = \begin{cases} 0.5(x_n - y_n)^2/\beta, & \text{if } |x_n - y_n| < \beta \\ |x_n - y_n| - 0.5 \times \beta, & \text{otherwise} \end{cases}$
- 
## Cross entropy
- Measures the difference between two probability didstributions:
	- Predicted 
	- True 
- Softmax used as the last layer, CE measures how well the predicted probabilities match the true labels
## Focal Loss
- Adaptive loss function on top of CE introduced to help address class imbalances
- Assigns more weight to hard to classify examples, less weight to easy to classify examples
- Basically downweights the contribition of well-classified examples so model focuses on more challenging tasks
- alpha is the balancing factor
- gamma is the focusin factor, higher gamma increases the effect of modulating the loss. (1-pt)^gamma. If pt is low, and gamma is high, we focyus on misclassified examples since more loss
- If gamma = 0, same as CE
