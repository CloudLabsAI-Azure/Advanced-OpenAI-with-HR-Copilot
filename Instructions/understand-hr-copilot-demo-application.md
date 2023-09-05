# Lab 3: Understand HR Copilot demo Application 

When scope for automation spans across multiple functional domains, like human, agent may perform better when it can specialize in a single area. So instead of stuffing a single agent with multiple capabilities, we can employ multiple agents model, each specializing in a single domain. These agents are managed and coordinated by a manager agent (agent runner). This is called multi-agent copilot model. The agent runner is responsible to promote the right agent from the agent pool to be the active agent to interact with user. It also is responsible to transfer relavant contextfrom agent to agent to ensure continuity. In this model, the agent runner relies on the specialist agent's cue to back-off from conversation to start the transfer. Each specialist agent has to implement a skill to send a notification (back-off method) when it thinks its skillset cannot handle the user's request. On the other hand, the decision on exactly which agent should be selected to take over the conversation is still with agent runner. When receiving such request, agent runner will revaluate the from the input by the requesting agent to decide on which agent to select for the job. This skill also relies on a LLM. Agent runner runs each specialist agent's run method. There can be some persistent context that should be available across agent's sessions. This is implemented as the persistent memory at agent runner. Each specialist agent depending on the requirement for skill, can be powered by a gpt-35-turbo or gpt-4. Multi-agent solution has same application platform (streamlit) as the single HR Copilot.

![](../media/img20.png)


## Exercise 1: Deploy and Run Multi-agent Copilot Application

### Task 1:  Build your own Multi-agent Copilot application locally
