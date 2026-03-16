*Known as LLM, it is a type of [[Language Model|language model]] with a massive amount of parameters.

LLMs are usually trained on very large, unlabeled datasets, and have a massive number of parameters to store their obtained knowledge. They can then be "fine-tuned" on smaller, more specific datasets to become more accurate at particular tasks.
They are built using [[Transformer|Transformers]], using their self-attention mechanism to weigh the importance of different words in a sentence, understanding their connection and interdependencies.
When given an input prompt, the output is what the model predicted would be the most probable sequence of words to form a coherent and relevant response.
Allow for [[Retrieval Augmented Generation|RAG]] applications and can be tuned for following instructions.
## Training Process
The model is first pre-trained on a large corpus of text data using self-supervised learning techniques (learning from the data itself without explicit labels):
- **Goal:** Predict the next word in a sequence given the previous words.
	1. Ask the model to predict the next word
	2. Train it using a [[Gradient Descent|gradient descent]] algorithm to minimize the prediction error.
After pre-training, the model can be fine-tuned on smaller, labeled datasets (supervised learning) for specific tasks (e.g., sentiment analysis, question answering), following instructions, aligning response content / format, ...
- **Reinforcement Learning from Human Feedback (RLHF):** A technique used to align LLM outputs with human preferences.
- **Direct Preference Optimization (DPO):** An alternative to RLHF that directly optimizes the model based on human feedback without requiring a separate reward model.
- **Prompt Engineering:** Crafting effective prompts is crucial for eliciting desired responses from LLMs.
## Knowledge & LLMs
How can LLMs benefit from [[Knowledge Graph|KGs]] and vice-versa? Knowledge can be:
- Extracted from text with the help of LLMs, populating KGs with entities and relationships.
- Acquired from LLMs to enrich KGs with additional context and information.
- Used to enhance LLMs' understanding and reasoning capabilities by injecting structured information.
Can LLMs be knowledge bases themselves?
- **KB:** Queryable and editable; Predictable / Consistent; Human-interpretable reasoning; Limited coverage
- **LLM:** Trainable without human supervision; Very flexible; Easier to use; Implicit knowledge; Unpredictable / Inconsistent; Opaque reasoning; Broad coverage
LLMs have a very complex architecture - it's impossible to [[Explainable AI (XAI)|track how decisions are made]].
#### Chain of Thought (CoT) Prompting
Technique to improve LLM reasoning by encouraging step-by-step explanations.
- LLM decomposes problems into intermediate steps 
- Interpretable method for understanding the model’s response 
- Induced in the prompt by: 
	- including examples of CoT sequences \[Wei et al., 2022] 
	- specific language “triggers” \[Kojima et al., 2022] 
- LLMs specialized in generating the reasoning steps do it by default
An important distinction must be made:
- **Plausibility:** The appearance of being reasonable or probable. LLMs often generate plausible-sounding answers that may not be factually correct.
- **Faithfulness:** The quality of being accurate and reliable. An explanation is faithful if it accurately reflects the model's true reasoning process. LLMs often struggle with faithfulness, as their internal reasoning is not transparent!