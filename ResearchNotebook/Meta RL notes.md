Paper:
https://arxiv.org/pdf/2301.08028.pdf

few-shot meta-RL. Here, the goal is to learn an RL algorithm capable of fast adaptation

The goal here is to learn general-purpose RL algo- rithms not specific to a narrow task distribution, similar to those currently used in practice.

For some applications, we can afford a burn-in or adaptation period, during which the performance of the policies produced by the inner-loop is not important as long as the final policy found by the inner-loop solves the task. The episodes during this burn-in phase can be used by the inner-loop for freely exploring the task. For other applications, a burn-in period is not possible and correspondingly the agent must maximize the expected return from the first timestep it interacts with the environment. Maximizing these different objectives leads to different Learned exploration strategies: a burn-in enables more risk-taking at the cost of wasted training resources when the risks are realized.

Another popular approach to meta-RL is to represent the inner-loop as an RNN and train it on tasks from the task distribution end-to-end with RL.

These two different approaches to meta-RL each come with their pros and cons. MAML has the appealing property that the inner-loop is just a policy gradient algorithm, which can under certain assumptions produce an improved policy from the initialization on any given task, even one from outside the task distribution. In contrast, RL2 may not learn at all on tasks that it has not seen before, since they may require zero-shot generalization from the RNN. adapt the policy after every timestep, and its policy gradient updates tend to yield a less sample efficient inner-loop than to RL2.

Methods we can look at:
Few shot vs. Zero shot
Single Task vs Multi Task

few-shot single-task -- still an open question


MARL -- has a burn out phase
![[Screenshot 2023-10-25 at 1.36.06 AM.png]]
Outer-loop algorithms While many black box methods use on-policy algorithms in the outer- loop [46, 239, 281], it is straightforward to use off-policy algorithms [185, 51, 130], which bring increased sample efficiency to RL. For discrete actions, it is also straightforward to use Q-learning [51, 130], in which case the inner-loop must change as well. In this case, the inner-loop estimates Q-values instead of directly parameterizing a policy. The policy can then act greedily with respect to these Q-values at meta-test time. This approach can be thought of as modifying recurrent Q- networks [85] to fit the meta-RL setting, which compares favorably compared to other state-of-the- art meta-RL methods [51].

Task inference method -- Task inference is a process of inferring this posterior distribution over tasks, conditional on what the agent has seen so far. Thus task inference can be seen as an attempt to move a meta-learning problem into the easier multi-task setting.

task infer- ence methods generally map a task distribution, given the current data, to a base policy. This can be seen as learning a policy conditioned on a (partially) inferred task. In this case, learning becomes the process of reducing uncertainty about the task.

Task inference with privileged information A straightforward method for inferring the task is to add a supervised loss so that a black box fθ predicts some known representation of the task, cM [95]. For example, a recurrent network may predict the task representation, cM, conditional on all data collected so far. This task representation must be known during meta-training, and so constitutes a form of privileged information. The representation may, for instance, be a one-hot representation of


Online outer-loop and offline inner-loop Under this setting, the agent can only adapt with offline data. However, online data is available in the outer-loop to help the agent learn what is a good offline adaptation strategy, which may be easier to learn than in an offline outer-loop setting. In other words, the agent is learning to do offline RL via online RL. This setting is appealing for two reasons: (1) It maintains the benefits of using solely offline data for adaptation, while being easier to meta-train than the fully offline setting. (2) It is difficult to design good offline RL algorithms [121], and meta-RL provides a promising approach to automating this process. A couple of existing methods do combine an offline inner-loop with an online outer-loop [38, 178]. However, these approaches both allow for additional online adaptation after the offline adaptation in the inner-loop, and the offline data either contains only observations [38], or conditions on additional expert actions [178]. One method uses permutation-invariant memory to enable an off-policy inner-loop, but only evaluates with data collected from prior policies [97]. Consequently, offline RL via online RL remains an interesting setting for future work with the potential for designing more effective offline RL algorithms by meta-learning in both the few-shot and many-shot settings.


**Read this Meta Continual Learning:**
https://arxiv.org/pdf/2311.05241.pdf
