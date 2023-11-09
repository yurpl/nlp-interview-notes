1. Forward Pass
	- Input passed through the network layer by layer, from the input layer to the output layer
	- Each neuron in a layer recieves an input, applies a transformation, and passes the results to the next layer
2. Backward pass
	- After the forward pass, error is computed using a loss function which measures the difference between the network's prediction and the actual target values 
	- The error is then propagated backward through the network layer by layer, calculating the gradients with respect to the weights using chain rule
	- Gradients represent how much a small change in each weight would have reduced the error
	- Once all gradients are calculated, the weights are updated in the opposite direction of the gradients to minimize the error using SGD
Backprop basically minimizes the error by adjusting the network weights