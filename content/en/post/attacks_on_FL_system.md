---
title: "Attacks on Federated Learning system"
lastmod: false
date: 2022-05-17T21:15:15+02:00

mathjax: true

---

## Background
1. Federated Learning (FL for short): FL is a Machine Learning framework that enables different parties to jointly train a model. It is proposed with the purpose of preserving privacy, since by design, no one has access to the local data except for the owner, however, this framework still has some inherent imperfections, for example, the central aggregator has the chance of peeking each individual's model, attackers may upload malicious updates.
2. Federated learning is not just a distributed version of standard machine learning, it is a distributed system and therefore must be robust to arbitrarily misbehaving participants.
3. Following [Kerckhoffs’s Principle](https://en.wikipedia.org/wiki/Kerckhoffs%27s_principle), when considering defend against malicious or honest-but-curious attackers, we assume that the anomaly detection algorithm is known to the attacker.

## Summary of Papers

|paper|topic|publication|summary|
|---  |---  |--- |--- |
|[How To Backdoor Federated Learning](https://proceedings.mlr.press/v108/bagdasaryan20a.html)   |Backdoor Attack   |Bagdasaryan, Eugene, et al. "How to backdoor federated learning." International Conference on Artificial Intelligence and Statistics. PMLR, 2020.   |The authors develop and evaluate techniques called constrain-and-scale and train-and-scale, where in constrain-and-scale, constrain means regulating attacker's loss function during training, represented by: $L_{model} = \alpha L_{class} + (1 - \alpha)L_{anomaly}$. Train-and-scale means scales up or down the model weights to a bound $S$ after the backdoored model converges to avioud anomaly detection. |
|[DBA: Distributed Backdoor Attacks against Federated Learning](https://openreview.net/forum?id=rkgyS0VFvr)   |Backdoor Attack   |Xie, Chulin, et al. "Dba: Distributed backdoor attacks against federated learning." International Conference on Learning Representations. 2019.   |DBA decomposes a global trigger pattern into separate local patterns and embed them into the training set of different adversarial parties respectively. Specifically, local triggers are decomposed from the global trigger through geometric strategy. DBA is more persistent and stealthy than attackers conducting centralized backdoor attack with the same global trigger. |
|[Attack of the Tails: Yes, You Really Can Backdoor Federated Learning](https://proceedings.neurips.cc/paper/2020/hash/b8ffa41d4e492f0fad2f13e29e1762eb-Abstract.html) |Backdoor Attack   |Wang, Hongyi, et al. "Attack of the tails: Yes, you really can backdoor federated learning." Advances in Neural Information Processing Systems 33 (2020): 16070-16084.   |There is a observation on high-capacity models that they tend to mispredict classification subtasks, especially thoes that may be underrepresented in the training set. From this observation, the authors assumed that "Backdoors hidden in regions of small measure (edge-case samples), are unlikely to be detected using gradient-based algorithms.", and proposed the edge-case backdoor attack, which targets rare and underrepresented data points. |
|   |   |   |   |
|   |   |   |   |

With the aim of bypassing robust aggregation rules or defense mechanisms.

## Types of Attack

### Backdoor Attacks
**Definition**: Backdoor attacks aim to manipulate a subset of training data by injecting adversarial triggers such that machine learning models trained on the tampered dataset will make arbitrarily (targeted) incorrect prediction on the testset with the same trigger embedded.

**Definition 2**: Backdoor attacks, in which an adversary injects manipulated model updates into the federated model aggregation process so that the resulting model will provide targeted false predictions for specific adversary-chosen inputs.

Formally, the adversarial objective for attacker $i$ in round $t$ with local dataset $D_i$ and target label $\tau$, transformation function $R$ with a set of parameters $\phi$ (including trigger size, gap, location) is:

$$
\omega_i^* = argmax_{\omega_i}(\sum_{j \in S_{poi}^i} P[G^{t+1}(R(x_j^i, \phi)) = \tau] + \sum_{j \in S_{cln}^i}P[G^{t+1}(x_j^i) = y_j^i]).
$$

Attackers modify an image classifier so that it assigns an attacker-chosen label to images with certain feature patterns, or force a word predictor to complete certain sentences with an attacker-chosen word. Such attack can also be conducted on a range of other machine learning tasks, e.g., OCR, sentiment analysis, autonomous vehicles.

The essence of Backdoor attack is just multi-task training. So after training under attack, the joint model should perform well on both original task and the attacker designed task.

Those attacks can be performed by a single participant or multiple colluding participants. (tradeoff?)

$$
G^{t+1} = G^t + \frac{\eta}{n}\sum_{i=1}^{m}(L^{t+1}_{i} - G^t).
$$

where $\eta$ is the gobal learning rate, which controls the fraction of update of the joint model.

#### Multi rounds or Single round

#### Method
1. Model Poisoning Attack (more powerful)

    Model Poisoning Attack, can be seen as a white-box attack
2. Data Poisoning Attack

    Data Poisoning Attack, can be seen as a black-box attack

#### Code

### Byzantine Attacks

### Membership Inference Attack

#### Method

#### Code


## Defenses