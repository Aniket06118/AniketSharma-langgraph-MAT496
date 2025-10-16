# AniketSharma-langgraph-MAT496

---
# Module-1
**Lesson 1**
- A single language model has limited abilities since it lacks access to tools, external data, and complex workflows.
- To overcome this, many large language models use control flows made up of pre- and post-processing steps, forming what’s called a “chain.”
- The control flow of an agent is directed by an LLM, determining how it operates.
- A Router agent depends on an LLM to choose among predefined steps (less autonomy), while a Fully Autonomous agent independently plans and executes tasks (more autonomy).
- LangGraph helps maintain reliability even when giving the LLM more control, effectively “bending the reliability curve.

**Lesson 2**
- I learned how to build a simple graph using LangGraph.
- I got introduced to the core components of a LangGraph.
- I understood that the edge between the start and node 1 is called a normal edge.
- I learned that when I choose different nodes based on conditions, those edges are called conditional edges.
- I realized that the state is an object I pass between the nodes and edges in the graph

  **tweakings**
   - made a simple graph which checks if the user is excited or not.
 
**Lesson 3**
- I learned about LangGraph Studio, an interactive IDE for building, visualizing, and debugging AI agent workflows created with LangGraph.
- I discovered that it integrates with LangSmith to trace, test, and optimize prompts or graph executions in real time.

  **tweakings**
  - tried and tested few graph state
 
**Lesson 4**
- I learned about chains and how to build them in a graph.
- I discovered that a simple chain involves four key concepts: using chat messages in the graph, using chat models, binding tools to the LLM, and executing tool calls within the graph.
- I learned how to pass a chat list containing AIMessage and HumanMessage to the LLM model.
- I understood how to bind a tool to the LLM and incorporate it into my workflow.
- I learned how to use messages as graph state and how reducers control state updates; if no reducer is specified, updates override existing values, but using the built-in add_messages reducer appends new messages instead of overwriting them.

  **tweakings**
  - changed the conversation where we learned about messages into a conversation about jee mains
  - changed the tool from multiply 2 numbers to add 2 numbers
  - tested the reducer with adding some more questions on jee mains
  - called my addition tool just for fun .

**Lesson 5**
- In the previous video, I learned that a graph can either produce a tool call or an NLP response, with the LLM guiding the overall workflow of the application.
- In this video, we added a node that triggers the tool whenever the model outputs a tool call.
- I also created a conditional edge to determine the next step in the workflow based on whether the LLM’s response includes a tool call or not.
- If no tool call is detected, the workflow automatically ends.
- I explored this entire workflow visually in LangGraph Studio by running a few prompts and observing how it functioned.
  
