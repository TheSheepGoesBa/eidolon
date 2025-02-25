---
title: Agent Communication
description: References - Agent Communication
---
In a multi-agent system, agents need to communicate with each other to share information, coordinate actions, and achieve 
common goals.

Eidolon provides a built-in mechanism for agents to communicate with each other, enabling seamless 
interaction between agents.

## Why
LLMs are kinda dumb 🧱. Don't get me wrong, they are amazing tools, but they just can't figure out complex tasks.
Thankfully, unlike people, LLM applications can scale horizontally 👬 to inject a bit more brain power 🧠💪 into the system. 
Because of this we can separate the tasks and have different agents work on different parts of the problem.

So, perhaps we aren't making the llm smarter, but rather the problem easier. That way we can extract the most value from the LLMs 
as possible. As LLMs improve, we will always be able to extract more performance 📈 from them by carefully decomposing 
the problem at hand.

This all means that we need an easy way to assemble our agents and have them communicate with each other.


## How
In any APU enabled agent, you can add an [AgentLogicUnit](/docs/references/agent_logic_unit/) agent's apu. When using a 
[SimpleAgentTemplate](/docs/references/simple_agent_template/), we have made this a step easier. Just adding an 
`agent_refs` field to the spec portion of the yaml file. This field is a list of agent names that the agent will communicate with.

When an agent is created, it will automatically be able to communicate with the agents listed in the `agent_refs` field.

### SimpleAgent Example
```yaml
apiVersion: eidolon/v1
kind: Agent
metadata:
  name: Developer

spec:
  implementation: SimpleAgent
  agent_refs: ["QA", "Manager"]
```

## Recipes

#### [GitHub Repo Expert](/docs/recipes/repo-expert)
The [GitHub Repo Expert](/docs/recipes/repo-expert) recipe is a great example of how agents can communicate with each 
other. In this example we have separated the copilot agent from the agent who handles relevance search. 

The copilot agent 👨 will ask the relevance search agent 🔎 to find the most relevant repositories for a given query as 
needed.
