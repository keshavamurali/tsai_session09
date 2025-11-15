# Architecture of the Code

The AI agent code that is shared has the entry point in _agent.py_ file. The _agent.py_ file calls the Agent loop, which waits for user input and processes it. The agent loop is coded in __loop.py__.

From the code architecture, most of the functionality is in the two directories.
## 1. core
Contains the processing modules which manage the context, session, strategy and main loop.
### context.py :
Keeps the context of current run, such as user input, results ..etc
### session.py
Encapsulates the MCP servers and related calls.
### strategy.py
Contains the handler for strategy (such as exploratory, conservative ..etc). Also has the code to decide the next action. Not used in the current assignment.

Strategy interfaces with LLM for processing the text and making the decision
#### loop.py
Main execution loop

## 2. modules
Contains the processing modules based on the Perception->Memory->Decision->Action architecture.
### perception.py
Contains the code to run the perception, which extract the intent, suggestions for possible tool usage and hand over to agent for the next step.
### action.py
Contains the code to do the actual run of MCP tools, which is contained inside a sandbox.
### memory.py
Holds the memory of previous interactions with agent.
### decision.py
Has the main decision logic to take the next action.
### tools.py
Tools interface to summarize the available tools from MCPs, provide a list ..etc
### model_manager.py
Place to manage different models ..etc

## prompts
Contains prompts for perception and different strategies.

## Overall Flow
Here is the overall flow of agent working.

* Agent receives the user input
* The context is created and stores different parameters corresponding to this session.
* Gets the user intent using Perception
* Decides the strategy
* Decide the next action to be taken based on the strategy and perception.
* Takes the action by calling MCP tools in the sandbox
* Passes on the current runs output to the next iteration
* If the Final answer is available, it is provided to user. If not, continues till the max iterations are met.

Attached diagram shows the architecture as well as the flow.


