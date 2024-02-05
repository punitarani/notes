# Introcution to Agents

## What is an AI Agent?

- An **_Agent_** is entity that can perceive its environment through sensors and act upon that environment through actuators.
  - Ex: Humans, robots, thermostats, etc.
- An **_Agent function_** maps a sequence of perceptions to a sequence of actions.
  - $f: P^* \rightarrow A^*$
- An **_Agent program_** implements the agent function.
  - The function is a mathematical concept, while the program is computational.

### Performance Measure

- The **_Performance Measure_** is a function that measures how successful an agent is at achieving its goals.
  - It evaluates the behavior of the agent.
  - It is used to compare the performance of different agents.
  - It can be a simple goal function or a complex utility function.

### Rationality

- **_Rationality_** is the measure of how well an agent achieves its goals.
  - A rational agent is one that does the right thing, given what it knows.
  - Rationality is not the same as omniscience.
    - An agent can be rational without knowing everything.
  - Rationality is not the same as perfection.
    - An agent can be rational without always making the best decision.
  - Rationality is not the same as success.
    - An agent can be rational without always achieving its goals.

### Task Environment

- **P**erformance Measure
- **E**nvironment
- **A**ctuators
- **S**ensors

#### Environment Types

- **Fully Observable vs. Partially Observable**
  - Fully observable if the agent's sensors give it access to the complete state of the environment at each point in time.
  - Partially observable if the agent's sensors give it access to only a limited part of the environment at each point in time.
- **Deterministic vs. Non-deterministic**
  - Deterministic if the next state of the environment is completely determined by the current state and the action executed by the agent.
  - Non-deterministic if the next state of the environment is not completely determined by the current state and the action executed by the agent.
  - **Stochastic** environments are a special case of non-deterministic environments where the randomness is probabilistic.
- **Episodic vs. Sequential**
  - Episodic environment, the agent's experience is divided into episodes, where each episode consists of the agent perceiving and then performing a single action.
  - Sequential environment, the current decision could affect all future decisions.
- **Static vs. Dynamic**
  - A static environment is one that does not change while the agent is deliberating.
  - A dynamic environment is one that can change while the agent is deliberating.
- **Discrete vs. Continuous**
  - A discrete environment has a limited number of distinct, clearly defined percepts and actions.
  - A continuous environment has a large number of percepts and actions that are not clearly defined.
- **Single-agent vs. Multi-agent**
  - A single-agent environment contains only one agent.
  - A multi-agent environment contains more than one agent.
- **Known vs. Unknown**
  - In a known environment, the agent knows the rules of the environment.
  - In an unknown environment, the agent does not know the rules of the environment.

### Agent Types

- Simple Reflex Agents
  - Selects actions based only on the current percept.
- Model-Based Reflex Agents
  - Selects actions based on the current percept and the history of percepts.
- Goal-Based Agents
  - Selects actions based on the current percept, the history of percepts, and the current goal.
- Utility-Based Agents
  - Selects actions based on the current percept, the history of percepts, the current goal, and the utility of the action.
- Learning Agents
  - Selects actions based on the current percept, the history of percepts, the current goal, the utility of the action, and the history of actions.
