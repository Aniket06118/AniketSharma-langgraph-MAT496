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
   - used pydantic for the same graph , it worked when i entered subject as physics, chem , maths but showed an error when i tried to enter any other value which is not defined in the funtion (eg - "sports")

**Lesson 2**
- by default langgraph overwrites the value while updating state
- while branching , if we try to overwrite in parallel which means both nodes run in the same step of the graph , we will get an error as the graph doesnt know which value to return
- Reducers give us a general way to address this problem , We can use the Annotated type to specify a reducer function.
- to handle cases where the input might be null we can use custom reducers
- MessagesState has a built in messages key which with the help of add_msg appends new messages to the list
- we can also remove messages using removemessages

  **tweaking**
  - made a graph with name and subject as literal , tried to get 3 outputs at the same time from 3 nodes which gave me an error as langgraph doesnt know which output to return
  - did the same thing but with reducers and got the correct output , all three subjects p , c and m which were being returned by 3 nodes got appended in the list
  - played around with messages  , tried things like rewriting , removal and adding new messages

**Lesson 3**
- Privatestate is useful for anything needed as part of the intermediate working logic of the graph, but not relevant for the overall graph input or output.
- By default, StateGraph takes in a single schema and all nodes are expected to communicate with that schema.
- it is also possible to explicitly define input and output schemas to constrain the input and output of a graph

  **tweaking**
  - understood the working of changing input and output schemas , by and privatestate by trying out examples of my own


 **Lesson 4**
 - A major challenge in chatbots is handling long conversations, which can lead to increased token usage and response delays.
 - To manage this, one can either filter messages (e.g., only sending recent ones like messages[-1:]) or trim them to stay within a token limit.
 - Filtering selects specific past messages, while trimming limits the total token count—helping the model stay efficient and responsive.

   **tweaking**
   - made my own messages about a conversation on JEE
   - invoked the graph on the messages i predefined
   - learned how to filer messages and removed the top two messages which  i typed out to be " i am going to get deleted" for fun.
   - tried out an example on message trimming again on the topic of jee and it worked perfectly!


**Lesson 5**
- Instead of just cutting or filtering old messages, we can let the LLM summarize the chat as it goes, keeping the key points without losing context.
- We build a chatbot that remembers past talks, using MessagesState and adding a new part called summary to store these short recaps.
- Once the summary is created, we’ll clean up older messages using RemoveMessage, since the chatbot’s state usually resets after each run.
- To keep conversations going even after breaks, LangGraph’s checkpointer (like MemorySaver) automatically saves progress so the bot can pick up where it left off.
- Each saved session becomes a thread of conversation—kind of like a Slack channel—and once there are more than six messages, the bot starts summarizing to stay efficient.

  **tweaking**
  - carried out a conversation of my own related to cricket
  - tried to summarize before the set threshold and it did not work
  - asked some more questions about cricket to reach the threshold
  - it got perfectly summarized at the end


**Lesson 6**
- To give the chatbot memory that lasts forever, we can use advanced checkpointers like SqliteSaver, which stores everything in a lightweight SQLite database.
- Once the graph is recompiled with this checkpointer, the chatbot can pick up old conversations even after restarting, since all data stays saved.

**tweaking**
- carried out an example where i asked questions about cricket and virat kohli , and tested the model on places as mentioned in the tutorial , and it worked perfectly !

  ---

# Module 3
**Lesson 1**
- This module explains human-in-the-loop, which lets users interact with graphs in real time using streaming to visualize outputs like node states or chat model tokens. LangGraph supports both sync and async streaming, allowing full or partial state updates, as well as token-level and message-based streaming for smoother, real-time tracking of chat model activity.

  **tweaking**
  - I modified the prompts to test custom outputs for both streaming modes and confirmed that they worked as expected.


**lesson 2**
- Human-in-the-loop lets users view and control graph outputs in real time, building on streaming.
-Its main goals are approval, debugging, and editing of the agent’s state.
-Breakpoints allow pausing the graph at specific steps for user intervention.
-Using interrupt_before=["tools"] stops execution before a tool node runs, enabling approval before action.
-LangGraph then re-emits the current state, resumes execution, and continues the process smoothly after approval.

**tweakings**
- I modified the existing tools and added a few custom ones to test how they worked with personalized examples and how permissions could be given to the LLM for tool usage. This experiment helped me understand breakpoints more effectively.

**Lesson 3**
- Human-in-the-loop allows approval, debugging, and editing of a graph’s state during execution.
- Breakpoints pause the graph, giving users a chance to not only approve actions but also modify the current state.
- Users can edit the graph by calling update_state, either appending new messages or overwriting existing ones using message IDs.
- After editing, the graph can resume execution smoothly from the current state.
- A human_feedback node can be added to collect user input directly, update the graph state, and continue execution with the new feedback applied.

   **tweakings**
  - I added custom tools like square, greet, and random number, then tested interruptions by modifying the graph’s state with both hardcoded values and user input. I updated the state using the LangGraph API and experimented with custom inputs in LangGraph Studio to explore how interrupts function.

  **Lesson 4**
  -  Breakpoints are usually set by developers on specific nodes during graph compilation.
 - A graph can also interrupt itself dynamically using NodeInterrupt.
- This allows conditional interruptions based on internal logic and lets developers communicate the reason for the pause.
- For example, a NodeInterrupt can trigger when an input exceeds five characters.
- Resuming without changing the state will just re-run the same node, leaving the graph stuck.

  **tweakings**
  - tried out the code with my own messages
 
 **Lesson 5**
 - Time travel in LangGraph allows debugging by viewing, replaying, and forking from past graph states.
- Using get_state, developers can inspect the current state and history of a graph via its thread_id and checkpoint_id.
- Replaying involves passing a previous config back to the agent to re-run from that checkpoint.
- Forking lets users modify a past state (e.g., change input) and create a new checkpoint while preserving metadata.
- When replaying, the graph reuses existing checkpoints, but during forking, it executes newly created ones from the modified state.

    **tweaking**
  - created my own tool to square two numbers.
  - ran the code with my custom messages and my square_two_numbers tool.

    ---

 # Module 4

 **Lesson 1**
 - Fan-out lets multiple steps run in parallel, while fan-in brings their results back together afterward.
- If parallel steps try to update the same part of the state, it causes conflicts and errors.
- A reducer is used to properly merge updates from parallel steps instead of overwriting them.
- The graph waits for all parallel paths to finish before moving forward.
- The order of updates within a step is handled automatically, but a custom reducer can be used to control it.

  









  



   
    

  
