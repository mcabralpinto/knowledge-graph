*In [[Co-Creativity|co-creativity]], curation refers to the process of selecting, organizing, and presenting the generated content in a way that enhances its value and relevance to the intended audience.*

Curation can involve human judgment, where individuals or teams evaluate the generated outputs and choose those that best align with the creative goals or resonate with the audience. It can also involve AI-assisted curation, where algorithms analyze user preferences, trends, or contextual factors to recommend or highlight certain outputs. Curation plays a crucial role in ensuring that the creative outcomes are not only novel but also meaningful and engaging for the target audience.
## Personalization
- **Personalization for curation**: Choose what to show next (feeds (UGC discovery), quest/item recommendations, playlist sequencing, event surfacing) 
- **Personalization for creation**: Shape what is generated (adaptive difficulty/pacing, narrative tone and branching, NPC dialogue style, personalized levels/content)
## Techniques
The below methods can be seen as different ways to personalize the ranker $s(u,i,x)$ and generator $q_θ(·|x, U)$ in the co-creativity loop. 
#### 1. Content-based Retrieval (Nearest Neighbor)
Recommend nearest neighbors of the user in item space. Also used for reranking diversity (Maximal Marginal Relevance - MMR) and retrieval-augmented generation.
- **Representation:** Map items to vectors $v_i∈R_d$ (features or embeddings). Map user to vector $u∈R_d$ (profile)
- **Similarity Score**: Often [[Distance Metric#**Cosine Similarity**|cosine similarity]] (normalized vectors): $s(u,i)= \frac{u^Tv_i}{∥u∥∥vi∥}$
- **User Profile Construction**: Aggregate embeddings of interacted items! Let $L(u)$ be items user interacted with, build $u= \frac{1}{Z} \sum\limits_{i∈L(u)} w_iv_i$ where weights $w_i$ can encode recency, dwell time, etc.
	- **Online Exponential Moving Average (EMA update**: If the user chooses item $i_t$: $$u_{t+1}= \frac{(1−ρ)u_t+ρv_{i_t}}{∥(1−ρ)u_t+ρv_{i_t}∥}$$
- Useful for **curation** (select the next item/quest/UGC content) and **creation** (retrieve exemplars/style guides/lore snippets to condition generation)
- Works well when we have good embeddings, we want interpretability and fast iteration, cold-start can be addressed by content features
#### 2. Content-based Recommendation (Feature Model)
Equivalent to nearest neighbors if embeddings/features are consistent. Has the advantage of you being able to control which features are used (interpretable constraints).
- **Representation:** Let $x_i∈R_d$ be item features (tags, genre, style, difficulty, etc.). Let $u$ encode user preferences. 
- **Linear Scoring Model**: $s(u,i)=u^Tx_i$
- **Pairwise Preference Learning (A vs. B)**: If user prefers $i^+$ over $i^−$ , model $Pr(i+≻i−|u)=$ $= σ(u^T(x_i^+−x_i^−))$ and learn $u$ by logistic loss. This is "learning to rank" in its simplest pairwise form, and it can be implemented with embeddings and gradient descent.
#### 3. Collaborative Filtering
Content-based models can miss: "users who liked this also liked that" patterns. CF learns structure from interactions.
- **Interaction Matrix**: let $R∈R^{n×m}$ where $R_{u_i}$ encodes implicit feedback (click, play, purchase, etc.)
- **Representation**: Represent each user $u$ by vector $p_u∈R_d$, each item $i$ by $q_i∈R_d$.
- **Latent Factors**: Predict: $\hat{R}_{ui}=p^T u_q$
- **Regularized Objective (Weighted)**: $\min\limits_{P,Q} \sum\limits_{u,i} w_{ui} (R_{ui}−p_u^T q_i)^2+λ(∥P∥_F^2+∥Q∥_F^2)$, where $p_u$ is user taste/skill vector (latent), $q_i$ is item attribute vector (latent), and dot product is compatibility
- **Latent Factor Model**: For observed interactions $R_{ui}$ (ratings or real-valued signals), assume: $R_{ui} | p_u,q_i∼N(p_u^T q_i,σ^2)$ with priors: $p_u∼N(0,λ_p^{−1} I)$, $q_i∼N(0,λ_q^{−1} I)$. This provides a probabilistic meaning to "taste space".
- ...
\+ (Pros / Cons of each)
#### Issues
- **Filter Bubble**: Personalization can lead to echo chambers where users are only exposed to content that reinforces their existing preferences, limiting diversity and serendipity
- **Popularity Bias**: Popular items may be recommended more frequently, overshadowing niche or new content that could be valuable to users
- **Slop Amplification**: If the generator produces low-quality candidates, the ranker may struggle to find good options, leading to a feedback loop of poor outputs
May be mitigated by reranking constraints (diversity/novelty), logging, explicit objectives, periodic exploration.
...
## Ranking
- When it comes to content, users consume a top-$K$ list and creators react to exposure 
- Many objectives are list-level: diversity, coverage, pacing, safety
- **Core objective**: Given context $x$, a ranker outputs an ordering $π_x$ over candidates $C$
- More in IAE slides 4 about media, games, PCG, narrative
Initially: **Ranker $s_ϕ(x,i) ∈ \mathbb{R} ⇒$ rank by decreasing $s_ϕ(x,i)$**
#### Paradigms of Learning-to-Rank (LTR)
###### Pointwise 
Learn a scoring function $s_ϕ(x,i)$ to predict relevance of each candidate independently (e.g., regression or classification). Simple but ignores relative ordering.
- **Regression**: Given rating $y∈\mathbb{R}$: $$\min\limits_{ϕ}\sum (y_{xi}−s_ϕ(x,i))^2$$
- **Classification**: Given relevance label $y∈{0,1}$: $$\min\limits_{ϕ}\sum y_{xi} \log σ(s_ϕ(x,i))+(1−y_{xi}) \log (1−σ(s_ϕ(x,i)))$$

It is simple, stable, and uses standard ML! However, it does not directly match ranking metrics and it is sensitive to label calibration; ignores relative ordering structure. It is useful **as a baseline** or when labels are high-quality and aligned with ranking goals.
###### Pairwise
Learn to predict the relative order of pairs of candidates (e.g., "candidate A is more relevant than candidate B" $\rightarrow s_ϕ(x,i^+)>sϕ(x,i^−)$). This can be implemented using a binary classifier on pairs of candidates. It captures relative preferences but can be computationally expensive due to the number of pairs.
- **Model**: $Pr(i^+≻i^−|x)=σ(s_ϕ(x,i^+)−s_ϕ(x,i^−))$
- **Negative log-likelihood (pairwise loss)**: $ℓ(ϕ)=− log~σ(∆s_ϕ) , ∆s_ϕ=s_ϕ(x,i^+)−s_ϕ(x,i^−)$

...
###### Listwise
Learn to optimize the entire ranked list directly (e.g., using metrics like NDCG or MAP). This approach considers the interdependencies between candidates and can lead to better performance on ranking metrics, but it can be more complex to implement and optimize.
- **Discounted Cumulative Gain (DCG)**: $DCG@K= \sum\limits_{i=1}^K \frac{2^{rel_i}−1}{log_2(i+1)}$, where $rel_i$ is the relevance of the item at position $i$.
- **Normalized DCG (NDCG)**: $NDCG@K= \frac{DCG@K}{IDCG@K}$, where $IDCG@K$ is the ideal DCG (the maximum possible DCG for the given set of items).
- **Recall@K**: $Recall@K= \frac{|\{relevant~items\}∩\{top~K~items\}|}{|\{relevant~items\}|}$. Measures coverage of relevant items, ignoring ordering inside top-K.
- Examples in slides!
#### Diversity
Accuracy-only ranking tends to over-repeat similar items (redundancy), collapse into popular content, reduce exploration, amplify shallow proxies (slop risk), etc. We need alternatives!
- **Simple Diversity Metric**: Given top-$K$ item embeddings $v_1,...,v_K$ (normalized), measure the average pairwise dissimilarity of the top-$K$ items: $$Diversity@K = \frac{2}{K(K-1)} \sum\limits_{i<j} (1−cos(v_i,v_j))$$
- **Maximal Marginal Relevance (MMR)**: A re-ranking algorithm that balances relevance and diversity. Given a set of candidate items $C$ and a query $q$, MMR selects items iteratively by maximizing the following score for each candidate item $i$: $$MMR(i) = λ \cdot s(q, i) - (1 - λ) \cdot \max_{j \in S} \text{sim}(i, j)$$where $s(q, i)$ is the relevance score of item $i$ to the query $q$, $\text{sim}(i, j)$ is the similarity between items $i$ and $j$, $S$ is the set of already selected items, and $λ$ is a parameter that controls the trade-off between relevance and diversity.