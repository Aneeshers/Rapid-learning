
### TD(0):

1. **Single Step Update**: TD(0) is the simplest form of TD learning. It updates estimates based on the difference between the predicted values of two successive states. In other words, it uses a one-step look-ahead to update its value estimates.

2. **Update Rule**: The update for a state \( s \) in TD(0) is given by:
$[ V(s) \leftarrow V(s) + \alpha [r + \gamma V(s') - V(s)] ]$
Where:
   - \( V(s) \) is the current value estimate for state \( s \).
   - \( r \) is the reward received after transitioning from state \( s \) to state \( s' \).
   - \( \gamma \) is the discount factor.
   - \( \alpha \) is the learning rate.
   - \( V(s') \) is the value estimate for the next state.

### TD(λ):

1. **Eligibility Traces**: TD(λ) introduces the concept of "eligibility traces," which allow the algorithm to update not just the most recent state, but also several preceding states to varying degrees. This helps in propagating the learning more effectively backward through time.

2. **λ Factor**: The parameter \( \lambda \) (lambda) determines the extent to which preceding states are updated. A value of \( \lambda = 0 \) reduces TD(λ) to TD(0), while \( \lambda = 1 \) makes the algorithm consider updates over infinitely many steps (akin to Monte Carlo methods).

3. **Update Rule with Eligibility Traces**: The update involves both the TD error and an eligibility trace \( $e(s)$ \) for each state \( s \):
\[ $e(s) \leftarrow \gamma \lambda e(s) + 1$ \]
\[ $V(s) \leftarrow V(s) + \alpha \text{TD-error} \times e(s$) \]
Where the TD-error is similar to the one in TD(0).

### Utility Function:

The utility function you mentioned, which is the sum of discounted rewards, is central to both TD(0) and TD(λ). It's given by:
\[ $U_t = \sum_{k=0}^{N} \gamma^k r_{t+k}$ \]
Where:
   - \( $U_t$ \) is the total discounted reward from time \( t \) onwards.
   - \($\gamma$ \) is the discount factor, which determines the present value of future rewards.
   - \( $r_{t+k}$ \) is the reward received k steps after time \( t \).

This utility function captures the idea that rewards received in the future are worth less than rewards received immediately. Both TD(0) and TD(λ) aim to estimate this utility function, but they do so in slightly different ways:

- **TD(0)** uses a one-step look-ahead to estimate the utility.
- **TD(λ)** uses eligibility traces to consider multiple steps in its estimate, effectively blending one-step, two-step, three-step (and so on) look-aheads based on the λ parameter.

In summary, while both TD(0) and TD(λ) aim to estimate the same utility function, they differ in how they propagate learning backward through time. TD(0) is simpler and considers only the immediate next step, while TD(λ) uses eligibility traces to consider multiple steps, providing a more comprehensive update mechanism.

![[Screenshot 2023-09-12 at 8.16.09 AM.png]]
**You can take any action to compute $r_k$ but we are still maxmizing over a for expected reward, which could be a different action you took than to get to state $k$ ** 
- Off policy TD(0) Learning of Q

## SARSA
- Not maximizing over action space, you need to take the optimal action. 
- Works for TD($\lambda$) 
-   ![[Screenshot 2023-09-12 at 8.25.18 AM.png]]
![[Screenshot 2023-09-12 at 8.18.52 AM.png]]![[Screenshot 2023-09-12 at 8.26.21 AM.png]]
  