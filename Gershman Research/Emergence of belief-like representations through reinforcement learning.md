- 1. One way around this problem is if agents form “beliefs,” a probabilistic estimate of how likely each state is, given any observations so far.

1. **Beliefs as a Non-linear Dynamical System**:
   - "Beliefs" in this context refer to the probabilistic estimates of hidden or unobservable states based on current and past observations. These beliefs can change over time based on new observations and prior knowledge, making them dynamic. The relationship between observations and beliefs is non-linear, meaning a small change in observation might result in a large change in belief or vice versa.

2. **Use of Recurrent Neural Networks (RNNs)**:
   - RNNs are a type of neural network designed to work with sequences and remember past information. Because of their ability to maintain a form of memory and handle sequences, they are well-suited for modeling dynamic systems like beliefs.
   - The choice to use RNNs is also backed by evidence from the machine learning community, where RNNs have shown good performance on complex tasks that are partially observable.

3. **Previous Work vs. Current Exploration**:
   - While prior research in computational neuroscience has looked into using RNNs to directly compute beliefs, the focus here is slightly different. The paper is exploring whether training RNNs in environments that are partially observable will naturally lead the RNNs to develop representations that resemble beliefs, even if they weren't explicitly trained to compute beliefs.

**Why Do We Need a Non-linear Approximator?**:

1. **Complex Relationships**:
   - In many real-world scenarios, the relationship between observations and underlying states (or beliefs) is complex and non-linear. A linear model would assume a constant relationship between changes in observations and changes in beliefs, which is often too simplistic.

2. **Capturing Intricacies**:
   - Non-linear approximators can capture the intricacies and nuances of complex systems. For instance, in a partially observable environment, the relationship between what is observed and the actual state of the environment can be intricate. A non-linear model can better capture these relationships.

3. **Flexibility**:
   - Non-linear models, like RNNs, offer the flexibility to adapt to a wide range of patterns in the data. This adaptability is crucial when dealing with dynamic systems where patterns and relationships might not be straightforward.

4. **Memory and Sequence Handling**:
   - For dynamic systems that evolve over time, like beliefs, it's essential to consider the history or sequence of observations. RNNs, being inherently designed for sequences, can maintain a form of memory, making them ideal for such tasks.


1. **Partially Observable Markov Process**:
   - In a typical Markov process, an agent can directly observe the current state of the environment, denoted as \( s_t \). This means the agent knows exactly where it is or what's happening at any given time.
   - However, in a "partially observable" Markov process, the agent can't see the full state. Instead, it gets some observations, \( o_t \), which provide clues about the state but don't reveal it entirely.

2. **Observations and Markovian Property**:
   - When something is "Markovian", it means the future state depends only on the current state and not on the sequence of states that preceded it. In simpler terms, if you know the current state, you don't need any previous information to predict the next state.
   - The text mentions that observations, \( o_t \), are not in general Markovian. This means that just knowing the current observation doesn't give you all the information you need to predict the next observation. You might need to know a series of past observations to make an accurate prediction.

3. **Constructing \( V_t \)**:
   - \( V_t \) represents the value at time \( t \). In reinforcement learning, this value is an estimate of expected future rewards. It tells the agent how good it is to be in a particular state or situation.
   - Because the agent can't see the full state and because the observations aren't Markovian, the agent can't determine \( V_t \) based solely on the current observation, \( o_t \).
   - Instead, to determine \( V_t \), the agent needs to consider the entire history of observations up to time \( t \), which is represented as \( (o_1, . . . , o_t) \). This means the agent looks at all the clues it has received so far to estimate the value.


1. **Markovian State Space & TD Learning**:
   - TD (Temporal Difference) learning is a method used in reinforcement learning. For TD learning to work effectively, it assumes a "Markovian state space." This means that the future state of a system only depends on the current state and not on the sequence of states that came before it.
   - However, in some situations, like when the environment is partially observable, this Markov property doesn't hold. The agent can't predict the future state just by looking at the current state.

2. **Sufficient Statistic**:
   - To overcome the non-Markovian nature of partially observable environments, we need to compress the history of observations into a "sufficient statistic." This is a representation of the history that captures all the necessary information in a way that the Markov property holds.
   - In other words, instead of considering the entire history of observations, we transform or compress it into a new state space where the future state can be predicted just by looking at the current state.

3. **Linear Function for Value**:
   - The value at time \( t \), \( V_t \), is represented as a linear function of a sufficient statistic, \( z_t \). Here, \( z_t \) is a vector that summarizes the history of observations.
   - The value \( V_t \) is calculated as the dot product of \( z_t \) and a weight vector \( w \). Each element of \( z_t \), \( z_t(d) \), represents a feature of the history, and the corresponding weight is \( w(d) \).

4. **Learning the Weights**:
   - The weights \( w \) can be learned using an update rule. The gradient of \( V_t \) with respect to the parameters \( \theta \) is equal to \( z_t \). The change in weights, \( \Delta w \), is proportional to the product of a learning rate \( \eta \), a temporal difference error \( \delta_t \), and the gradient.

5. **Belief State as a Sufficient Statistic**:
   - One common choice for the sufficient statistic is the "belief state." This represents the agent's belief or probability distribution over the possible hidden states of the environment, given the history of observations and actions.
   - The belief state, \( b_t(i) \), gives the probability that the system is in state \( i \) at time \( t \), given all the observations and actions up to that time.
   - The equation provided shows how to update this belief when a new observation \( o_t \) is made and an action \( a_{t-1} \) is taken. It considers the probability of the current observation given the state and the transition probabilities between states.

6. **Discrete vs. Continuous States**:
   - The equation assumes there are \( K \) discrete states. However, the same concept can be extended to situations where the state space is continuous.

### 1. Training the Models:

- **Belief Model vs. Value RNN**: 
  - **Belief Model**: This model first computes beliefs (probabilistic estimates of the environment's state based on observations) and then estimates value as a linear transformation of those beliefs. The weights for this transformation are updated using TD learning.
  - **Value RNN**: Instead of using a predefined belief state, the Value RNN learns its own representation of the environment using a recurrent neural network (RNN). This representation is then used to estimate value, and the parameters of the RNN (and the linear transformation) are updated using TD learning.

- The paper mentions training both the Belief model and multiple instances of the Value RNN (12 in total, each with different random initializations) on a series of observations from a given task.

### 2. Gated Recurrent Unit (GRU):

- A **GRU** is a type of RNN architecture. RNNs are neural networks designed to handle sequential data by maintaining a hidden state that can capture information from previous time steps. However, basic RNNs suffer from issues like the vanishing gradient problem, which makes them less effective at capturing long-term dependencies in sequences.
  
- The GRU is an improvement over the basic RNN. It uses gating mechanisms (reset and update gates) to control the flow of information, allowing it to capture both short-term and long-term dependencies in the data more effectively. This makes GRUs (and another variant called LSTMs) more popular for tasks involving sequences, like time series forecasting or natural language processing.

- In the context of the paper, each Value RNN is implemented using a GRU with 50 hidden units. This means that the recurrent part of the network, which learns the representation of the environment, uses a GRU architecture.

### 3. Role of TD Learning:

- **TD Learning**: Temporal Difference (TD) learning is a foundational technique in reinforcement learning. It's used to update value estimates based on the difference between the estimated value of the current state and the sum of the actual reward received and the estimated value of the next state.

- In the context of the paper, both the Belief model and the Value RNNs use TD learning to update their value estimates. For the Belief model, TD learning updates the weights of the linear transformation of beliefs. For the Value RNNs, TD learning updates both the parameters of the GRU (which learns the representation) and the weights of the linear transformation of that representation.

- The paper mentions training multiple Value RNNs (each with different initializations) to explore the variability in learning and to see if different initial conditions lead to different learned representations or performance levels.

### Belief Model Overview:
The Belief model is designed to operate in partially observable environments, where the agent doesn't have full access to the state of the environment but only receives observations. The model's primary goal is to estimate the underlying state of the environment based on these observations. Once it has an estimate (or belief) about the state, it then computes the expected value associated with that state.

### 1. **Computing Beliefs**:
- **Beliefs** represent the agent's estimate of the probability distribution over possible states of the environment given the observations it has seen so far.
  
- In the context of the paper, the belief at time \( t \), denoted as \( b_t \), is defined as the probability of the environment being in state \( s_t \) given all the observations up to time \( t \). Mathematically:
  $$ b_t = P(s_t | o_1,...,o_t) $$
  
  Here, \( o_1,...,o_t \) are the observations from time 1 to time \( t \).

- The belief is updated based on new observations and the previous belief. This update can be done using Bayesian inference, where the new observation is used to refine the previous belief about the state of the environment.

### 2. **Estimating Value**:
- Once the model has computed its belief about the state of the environment, it needs to estimate the expected value associated with that state. This is crucial for decision-making in reinforcement learning, as the agent needs to know the expected reward associated with different states to make optimal decisions.

- The value estimate is computed as a linear transformation of the beliefs. This means that each possible state (or belief) has an associated weight, and the value is the weighted sum of the beliefs. Mathematically:
  $$ V_t = w^T b_t $$
  
  Here, \( V_t \) is the value estimate at time \( t \), \( w \) is a vector of weights, and \( b_t \) is the belief vector at time \( t \).

- The weights in \( w \) are learned parameters. They are updated based on the difference between the predicted value and the actual reward received, using techniques like TD learning.

### Why Use a Linear Transformation?
The choice of a linear transformation is motivated by its simplicity and interpretability. In the context of the paper, the environment's tasks are Pavlovian associative learning tasks. In such tasks, the sequence of observations and rewards is independent of the agent's actions, making the value function a simple linear transformation of the beliefs.

In summary, the Belief model first computes its belief about the state of the environment based on the observations it has received. It then estimates the value associated with that belief using a linear transformation. The weights of this transformation are learned parameters, updated based on the agent's experience in the environment.

### Belief Model:
1. **Input**: Sequence of observations \( o_1, o_2, ... o_t \).
2. **Processing**:
   - The Belief Model explicitly computes beliefs \( b_t \) based on the observations. These beliefs are probabilistic estimates of the environment's state.
   - The beliefs are updated using Bayesian inference, where new observations refine the model's previous beliefs about the state of the environment.
3. **Representation and Value Estimation**:
   - Representation: The beliefs \( b_t \) serve as the representation of the environment.
   - Value Estimation: The value \( V_t \) is estimated as a linear transformation of these beliefs.
   - Mathematically: \( V_t = w^T b_t \), where \( w \) is a learned weight vector.

### Value RNN:
1. **Input**: Sequence of observations \( o_1, o_2, ... o_t \).
2. **Processing**:
   - The Value RNN does not compute explicit beliefs. Instead, it learns a representation \( z_t \) of the environment using a recurrent neural network (RNN).
   - This representation \( z_t \) captures essential information from the observation history and evolves over time based on new observations.
3. **Representation and Value Estimation**:
   - Representation: The hidden state of the RNN \( z_t \) serves as the learned representation of the environment.
   - Value Estimation: The value \( V_t \) is estimated as a linear transformation of this learned representation.
   - Mathematically: \( V_t = w^T z_t \), where \( w \) is a learned weight vector.

In summary, while both models take in a sequence of observations, the Belief Model explicitly computes beliefs and derives value from them, whereas the Value RNN learns its representation from the observations and then derives value from this learned representation. The key distinction is in how they represent the environment: the Belief Model uses explicit beliefs, while the Value RNN uses a learned representation.

