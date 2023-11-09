Used in [[GPT-3]]
MoE stands for "Mixture of Experts," and it's a technique designed to scale up neural networks by increasing their capacity without a linear increase in computation. The core idea behind MoE is to have multiple specialized sub-networks (or "experts") and a gating network that decides which expert(s) to use for a given input.
### 1. **Experts**:

- Each expert is a neural network that specializes in a specific kind of task or data.
- Instead of routing every input through every neuron (as in traditional dense layers), inputs are directed to only one (or a few) of these experts.

### 2. **Gating Network**:

- Alongside the experts, there's a gating network that determines which expert to route an input to.
- The gating network looks at the input and outputs a set of weights, one for each expert. These weights determine the probability that the input should be routed to each expert.
- In some implementations, the input might be sent to multiple experts, with the outputs combined based on the gating network's weights. In other cases, only the highest-weighted expert might be chosen.

### 3. **Training**:

- During training, both the experts and the gating network are trained together.
- The loss is a combination of the prediction error and a term that encourages an even distribution of work among the experts (so that one expert doesn't dominate the others).

### 4. **Benefits**:

- **Increased Capacity**: MoE allows models to have a much larger number of parameters without a linear increase in computation, as not all experts are used for each input.
- **Specialization**: Different experts can learn to handle different kinds of data or tasks, allowing the model to handle a wider variety of inputs.
- **Efficiency**: MoE can provide a more computationally efficient way to scale up neural network capacity, especially in settings where the input data has varied characteristics.