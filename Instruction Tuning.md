## Background
- We want to optimize models for P(answer | prompt), but they are learned on a basic LM objective P(word | context)
- One solution: fine-tune models to do what we care about
- 2023:
	- Instruction: supervised fine-tuning on data derived from many NLP tasks
	- RLHF: RL to improve human judgements of how good the outputs are
## T0 
- T0 tried to deliver on the goal of T5 and do many tasks with one model
- Crowdsourced prompts with instructions on how to do the tasks 
- Task generalization
	- Pre-train: T5 task
	- Train: a collection of tasks with prompts. This uses existing train data
	- Test: a new task specified only by a new prompt. No training data in this task
## Flan-PaLM
- 1800 tasks, 540B parameters
- Train model on every task they can get their hands on, done a bit later than T0
- When fine-tuned on more tasks, performance of the model increases 