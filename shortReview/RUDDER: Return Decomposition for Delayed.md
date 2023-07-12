# RUDDER: Return Decomposition for Delayed Rewards

#### Link

https://arxiv.org/abs/1806.07857

#### Information

- Author/Institution : Jose A. Arjona-Medina, Michael Gillhofer, Michael Widrich, Thomas Unterthiner, Johannes Brandstetter, Sepp Hochreiter / **LIT AI Lab**
- Conference/Journal : Advances in Neural Information Processing Systems 32 (NeurIPS 2019)
- Cited by 172 _(2023.07.10)_
- Submitted on 20 Jun 2018

## Abstract

Delayed reward는 RL의 학습에 큰 방해가 된다. MC는 high-variance, TD는 bias 문제가 있는데 이런 문제들을 reward의 delay가 심할 수록 더 커지는 경향을 보인다. 따라서 미래의 reward, 즉 delay된 reward가 없을수록 더 좋은 학습을 할 수 있다.

We propose the following two new concepts to push the expected future rewards toward zero.

- **Reward redistribution** that leads to return equivalent decision processes with the same optimal policies
- **Return decomposition** via contribution analysis which transforms the reinforcement learning task into a regression task at which deep learning excels

## Key point

> **expected future rewards equal to zero.**

동일한 optimal policy를 얻을 수 있도록 delay reward를 decomposition reward로 바꿔서 표현함으로서 미래의 reward를 zero로 만들 수 있다. 미래 보상을 0으로 만들면 Q-value를 단순히 immediate reward들의 평균을 계산하는 것으로 나타낼 수 있다.

- An optimal reward redistribution should transform a delayed reward MDP into a return-equivalent MDP with zero expected future rewards.
- sequence-Markov decision processes (SDP), for which reward distributions need not to be Markov.
- return decomposition을 수행하면 RL을 회귀문제로 표현할 수 있어서 예측이 가능해진다.
- value function을 더 세부적인 단계로 나눌 수 있기 때문에 reward의 distribution이 가능하다.

return에서 immediate reward를 계산할 때, RNN 계열의 신경망 LSTM을 사용해서 이미 누적된 정보 $h$를 return을 제거해서 immediated reward를 계산하는 방식을 활용한다.

## Algorithm

$\gamma=1$이고 delayed reward를 가지는 finite horizon MDP $\tilde{\mathcal P}$를 가정한다. 본 논문에서 소개하는 새로운 강화학습 알고리즘은 학습중에 reward redistribution을 수행하고 Theorem 3을 기반으로 수행된다.

힉습 과정은 Reward redistribution Network 갱신과 Q-value 갱신으로 이루어진다.

## Formulation

**Return-Equivalent SDPs**

\*​A sequence-Markov decision process (SDP) is defined as a decision process which is equipped with a Markov policy and has Markov transition probabilities but a **reward that is not required to be Markov**.

만약 서로다른 2개의 SDP $\tilde{\mathcal{P}}$ and $\mathcal{P}$ 가 다음 2개의 조건을 만족하면 두 SDP는 _return-equivalent_ 하다.

1. 두개의 SDP는 오직 transition-reward distribution만 다르며, 나머지 MDP를 이루는 요소들은 동일하다.
2. 동일한 policy $\pi$에 대해서 time $t=0$에서의 expected return값이 동일하다.  
   => $\tilde{v_\pi}(0) = v_\pi(0)$

더 나아가, 모든 시간 $t$에 대해서 2번째 조건을 만족하면 *strictly return-equivalent*하다고 말한다.

이런 return-equivalent한 SDP는 동일한 Optimal policy를 가진다.

> 따라서 delayed reward를 가지는 MDP를 delayed reward를 가지고 있지 않는 return-equivalent한 SDP로 변환시킴으로서 강화학습 모델을 더 학습시키기 쉽도록 변경시킬 수 있다.

**Reward Redistribution**

strictly return-equivalent한 SDP를 이용하면 reward redistribution이 가능하다.

- At time $t-1$ the immediate reward is $R_t$ with expectation $r(s_{t-1}, a_{t-1})$
- Expected future reward $\kappa(m, t-1)$ at time $t-1$ as the expected sum of rewards from $R_{t+1}$ to $R_{t+1+m}$

즉, time $t-1$에 수행했던 action-state 쌍$(s_{t-1}, a_{t-1})$으로부터 $m$ step 뒤에 전달되는 expected future reward를 아래와 같이 표현할 수 있음을 정의한다.

$$
\kappa(m, t-1) = \mathbb E_{\sim \pi} \left[\sum^m_{\tau=0} R_{t+1+\tau} | s_{t-1}, a_{t-1}\right]
$$

Bellman Equation에 따라 Q-value는 다음과 같이 정의할 수 있다.

$$
q_\pi(s_t, a_t) = r(s_t, a_t) + \kappa(T-t-1, t)
$$

본 논문에서는 future reward를 zero로 만드는 것을 목표로 한다. (=optimal reward redistribution)  
= $q_\pi(s_t, a_t)=r(s_t, a_t)$  
= $\kappa(T-t-1,t)$

따라서 다음의 Theorem2를 따라서 delayed reward를 가지는 MDP $\tilde {\mathcal P}$과 어떤 policy $\pi$에 대하여 return-equivalent SDP $\mathcal{P}$로 *optimal reward redistribution*과 함께 변환할 수 있다.

**Theorem 2.** We assume a delayed reward MDP $\tilde{\mathcal P}$, where the accumulated reward is given at sequence end. A new SDP \mathcal P is obtained by a second order Markov reward redistribution, which ensures that $\mathcal P$ is return-equivalent to $\tilde{\mathcal P}$. **For a specific** $\pi$, **the following two statements are equivalent :**

1. $\kappa(T-t-1, t) = 0$ i.e., the reward redistribution is optimal
2. $\mathbb E [R_{t+1} | s_{t-1}, a_{t-1}, s_t, a_t] = \tilde{q}_{\pi}(s_t, a_t) - \tilde{q}_{\pi}(s_{t-1}, a_{t-1})$

1번 조건을 만족한다는 것은 변환한 SDP $\mathcal P$는 delayed reward를 가지지 않는 다는 의미이다. 또한 Theorem 2의 2번째 equation에서는 optimal reward redistribution을 위해 사용되는 expected reward는 원래 MDP에서의 **Q-value의 차이**로 정의되야함을 의미한다.
_\*return이 동일하려면 이렇게 되야함_

**Theorem 3.** If the reward redistribution is optimal, then the Q-values of the SDP $\mathcal P$ are given by

$$
q_\pi(s_t, a_t) = r(s_t, a_t)
$$

$$
= \tilde{q}_{\pi}(s_t, a_t) - \mathbb E_{s_{t-1}, a_{t-1}}  [\tilde{q}_{\pi}(s_{t-1}, a_{t-1})|s_t] = \tilde{q}_{\pi}(s_t, a_t) - \psi_\pi(s_t)
$$

## Insight

신경망을 사용하는 DeepRL에 적용하기 더 적절한 아이디어이기 때문에 RL에 많은 computation power을 사용할 수 없는 우리 문제에는 적용하기 힘들다.

그러나 return을 재분배 한다는 아이디어는 그대로 적용이 가능하다. (이미 사용하고 있던 아이디어이기도 하다...)
