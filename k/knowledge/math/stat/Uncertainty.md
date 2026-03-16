*A summary of all that is not explicitly taken into account in a knowledge base.*

Uncertainty derives from problems in knowledge: 
- Partial observability
- Noisy sensors
- Uncertainty in action outcomes
- Immense complexity of modelling and predicting reality
- ...
It has several types:
- **In prior knowledge:** some causes of a disease are unknown and are not represented in the background knowledge of a medical-assistant agent
- **In actions:** they are represented with relatively short lists of pre-conditions, while these lists are in fact arbitrary long
- **In perception:** sensors do not return exact or complete information about the world; a robot never knows exactly its position
And several sources:
- **Laziness:** failure to enumerate exceptions, qualifications, etc.
- **Ignorance:** lack of relevant facts, initial conditions, etc.
Handled via [[Probability|probabilistic reasoning]].