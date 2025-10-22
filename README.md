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

  **tweakings**
  - changed the tool call function from multiply 2 numbers to , subtraction of 2 numbers
  - used the tools_condition function on my subtraction tool
  - in the langsmith studio , i added 2 messages , one in which the tool is being called and the other one being a direct question

**Lesson 6**
- In this video, I explored the ReAct architecture, where the ToolMessage is sent back to the model, allowing it to decide whether to call another tool or directly respond to the user.

  **tweaking**
  - replaced the divide tool with a tool which squares a number
  - tried out a message which usses all 3 tools and it was working perfectly!

**Lesson 7**
- I learned that checkpointers save the state of the graph at each step as a checkpoint.
- Each checkpoint not only stores the state but also includes details like the next node, relevant metadata, and a unique checkpoint_id.
- These checkpoints can be linked together to form what’s known as a thread.
- When I specify a thread, provide an input, and run it, the workflow behaves normally at first , However, when I run a follow-up query using the same thread_id, the model can respond appropriately by referencing previous context from the thread.

  **tweakings**
  - tried out an example of my own  , gave a message to add and multiple some numbers then in the next message i gave the input as "square it" to check if the model remembers the result of the previous operation and it worked perfectly.
 
    ---
    
 # Module 2
 **Lesson 1**
 - dataclass is another way to define structured data apart from typedict
 - we can access our keys as for example state.name instead of state["name"]
 - both typedict and dataclass provide type hints but they don't enforce types at runtime , as a result we could potentially assign invalid values without raising an error , to solve this problem we can use pydantic
 - Pydantic can perform validation to check whether data conforms to the specified types and constraints at runtime.
   
   **tweaking**
   - made a graph with name as str and subject as a literal which has 3 subjects phy , chem and math
   - added a conditional edge which chooses randomly between the three subjects
   - used pydantic for the same graph , it worked when i entered subject as physics but showed an error when i tried to enter any other value which is not defined in the funtion (eg - "sports")
   
    

  
