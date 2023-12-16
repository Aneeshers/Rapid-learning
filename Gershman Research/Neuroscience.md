### TD Error:

The TD error (often denoted as δ) represents the difference between the predicted value of a state and the observed value after taking an action and receiving a reward. It's a measure of the "surprise" experienced by the agent based on the outcome compared to its expectation.
\[ $\delta_t = r_t + \gamma V(s_{t+1}) - V(s_t)$ \]

Where:
- \( $r_t$ \) is the reward received at time \( t \).
- \( $\gamma$ \) is the discount factor.
- \( $V(s_t)$ \) is the value estimate of the current state at time \( $t$ \).
- \( $V(s_{t+1}$) \) is the value estimate of the next state at time \( $t+1$ \).

### Dopamine Reward Prediction Error (RPE):

In neuroscience, dopamine is a neurotransmitter that plays a crucial role in reward-motivated behavior. Research has shown that the firing rate of dopamine neurons in the brain corresponds to a reward prediction error, which is conceptually similar to the TD error in reinforcement learning.

The Dopamine RPE is given by:
\[ $\text{RPE} = \text{Observed Reward} - \text{Expected Reward}$ \]

This equation essentially captures the difference between the reward that was expected based on prior experiences and the reward that was actually observed.

### Relationship:

1. **Similarity in Concept**: Both TD error and Dopamine RPE represent a form of "surprise" or discrepancy between what was expected and what was observed. In the context of reinforcement learning, this discrepancy is used to update value estimates. In the brain, it's believed to signal the need to adjust behavior or expectations.

2. **Neuroscientific Evidence**: Experiments have shown that the firing rate of dopamine neurons in the brain corresponds closely to the TD error predicted by reinforcement learning models. When an unexpected reward is received, dopamine neurons increase their firing rate (positive RPE). Conversely, when an expected reward is omitted, there's a decrease in firing (negative RPE).

3. **Learning and Adaptation**: Both TD error in machine learning models and Dopamine RPE in biological systems drive learning and adaptation. In reinforcement learning, the TD error is used to update value function estimates, leading to better future predictions and decisions. In the brain, the RPE is believed to drive behavioral adaptations to optimize reward acquisition.

Interesting: "But when reward arrives earlier than expected, dopamine neurons do not do what the TD error does—at least with the CSC representation used by Montague et al. (1996) and by us in our example."

