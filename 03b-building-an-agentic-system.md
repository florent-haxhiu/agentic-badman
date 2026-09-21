# Building an Agentic System

Your football agents don't just react. They reason, remember, and adapt. To make that happen, you need more than a good prompt. You need a system.
You've seen what a single agent can do: perceive the pitch, reason about the situation, and act. But football isn't a solo sport. A brilliant striker is useless if nobody's feeding them the ball. A rock-solid goalkeeper means nothing if the defense is out of position. Five agents coordinating on a live football pitch, making decisions under time pressure, adapting to an opponent's strategy in real time? That requires architecture. That requires an agentic system.
This section breaks down the core components and shows how each one maps directly to your football team's performance on the pitch.
[What Is an Agentic System?](#what-is-an-agentic-system)
An agentic system is the full stack of components that allow AI agents to operate autonomously and effectively. Think of it like a football club — the players (agents) get the glory, but behind them is an entire organization: coaching staff, medical team, scouts, analysts, and stadium operations. Without that infrastructure, even the most talented players underperform.
Your agentic system includes:
| Component | What It Does | Football Analogy |
| Foundation Models | The reasoning engine that powers decisions | The player's football brain — reading the game, making split-second choices |
| System Prompts | Instructions that define identity and behavior | The manager's pre-match team talk — "You're a defensive midfielder. Protect the backline." |
| State Management | Tracks what's happened and what's happening now | The team's shared memory — knowing the score, the formation, what the opponent just did |
| Agent Orchestration | Coordinates multiple agents working together | The captain on the pitch — making sure everyone's in position and playing the same system |
| Tool Integration | Connects agents to external data and actions | The earpiece to the coaching staff — getting real-time tactical data and instructions |
| Guardrails & Safety | Ensures agents behave within defined boundaries | The referee — making sure nobody breaks the rules or does something dangerous |
| Observability | Tracks performance and decision quality | The video analysis room — reviewing every decision to find what worked and what didn't |

Each of these components directly affects how your football agents perform. A weak memory layer means your agent forgets what formations the opponent has been running. Poor tool integration means your agent can't read live match state. Gaps in orchestration mean your five-player team falls out of sync during critical moments.
[Foundation Models — The Brain](#foundation-models-the-brain)
Everything starts here. The foundation model (LLM) is what gives your agent the ability to reason about complex situations rather than just following if-then rules.
When your agent receives the game state — player positions, ball location, score, stamina levels — the foundation model processes all of it and decides what to do. The quality of that reasoning depends on:
- More capable models handle nuance better. They can weigh multiple factors simultaneously: "I could shoot, but the angle is tight and my teammate is unmarked in a better position."
- How much information the model can consider at once. A larger context window means your agent can factor in more match history when making decisions.
- Your agent has a time budget per tick. A model that takes 5 seconds to respond when you have a 2-second window is useless, no matter how smart it is.
- Every LLM call costs money. In a match with hundreds of ticks across five agents, costs add up. Balancing intelligence with efficiency is part of the challenge.
In this workshop, you'll use models available through Amazon Bedrock — giving you access to a range of foundation models from Anthropic, Meta, Amazon, and others. Choosing the right model for your agents is one of your first strategic decisions.
[System Prompts — The Manager's Playbook](#system-prompts-the-manager's-playbook)
The system prompt is where you define your agent's identity, role, and tactical philosophy. It's the set of instructions that shapes every decision your agent makes during a match — the equivalent of a manager pulling a player aside before kickoff and saying: "Here's who you are. Here's how I want you to play."
A well-crafted system prompt might establish your agent as:
- A defensive midfielder with a mandate to protect the backline and recycle possession
- An attacking orchestrator tasked with finding space and distributing quickly
- A target forward instructed to hold up play and bring teammates into the attack
- A sweeper keeper who plays aggressively off the line and starts counter-attacks
[What to Encode in Your System Prompt](#what-to-encode-in-your-system-prompt)
| Element | Why It Matters | Example |
| Role and position | Gives the agent a clear identity | "You are the central defender. Your primary job is to prevent goals." |
| Tactical instructions | Defines how the agent should play | "Play a high defensive line. Press aggressively when the ball is in the opponent's half." |
| Decision priorities | Guides tradeoff decisions | "Favour possession over direct play. Only shoot when you have a clear chance." |
| Behavioral constraints | Prevents unwanted actions | "Never leave the defensive third when the opponent has the ball." |
| Coordination rules | Defines how to work with teammates | "If the left winger has the ball, overlap on the outside to create a 2v1." |

Your system prompt is the single highest-leverage thing you can tune. A mediocre model with a great system prompt will often outperform a powerful model with a vague one. Invest time here.
The best system prompts are specific, structured, and testable. Vague instructions like "play well" give the LLM nothing to work with. Concrete instructions like "when receiving the ball in the defensive third with no pressure, look for a long pass to the forward before considering a short pass" give it a clear decision framework.
[State Management — The Team's Memory](#state-management-the-team's-memory)
One of the most important — and often underestimated — components of an agentic system is state management. Your agent needs to track what has happened, what it knows right now, and what it intends to do next.
Without state, every tick is a blank slate. Your agent has no idea that the opponent just switched to a 4-3-3, that your team scored 30 seconds ago, or that the forward has been drifting offside repeatedly. With state, your agent can reason about trends, adapt to changes, and make decisions informed by context — not just the current snapshot.
[Types of State](#types-of-state)
State in an agentic football system typically falls into two categories:
Conversation History: The sequence of observations, decisions, and outputs accumulated during a match. This is what allows your agent to reason about recent events rather than treating every tick as if it were the first.
> "The opponent's left winger has beaten our defender three times in the last two minutes. I should provide cover on that side."
Agent State: Broader contextual information your agent carries across turns:
- Current formation and tactical mode (attacking, defending, balanced)
- Stamina estimates for each player
- Remembered opponent tendencies ("their goalkeeper always kicks to the right")
- Current score and time remaining
- Recent coaching instructions
[Framework-Specific Approaches](#framework-specific-approaches)
How you manage state depends on the framework you're using:
- In the , conversation history and agent state are managed through the agent's built-in memory constructs, which automatically maintain the message thread and can be extended with custom state fields to track match-specific data.
- In , state is typically managed explicitly — you pass conversation history and any custom state through your chain or agent executor at each invocation.
Regardless of framework, a clear state management strategy will directly improve your agent's tactical coherence and its ability to adapt as a match evolves.
[Agent Orchestration — The Captain](#agent-orchestration-the-captain)
When you have five agents on the pitch, coordination becomes critical. Without orchestration, you get five individuals making independent decisions, and that leads to chaos. Two players chasing the same ball. Nobody covering the back post. Three agents trying to shoot simultaneously.
Orchestration is the layer that turns individuals into a team. It handles:
- Ensuring each agent processes the game state and responds within the time budget
- Making sure agents have access to relevant teammate state (positions, intentions, stamina)
- Dynamically adjusting who plays where based on the game situation
- When two agents both want the ball, someone needs to decide who gets priority
In a football context, think of orchestration as the captain's role. The captain doesn't make every decision for every player, but they set the tempo, call out switches, and make sure the team is playing as a unit rather than a collection of individuals.
[Tool Integration — The Coaching Earpiece](#tool-integration-the-coaching-earpiece)
Agents become dramatically more useful when they can interact with external systems. In the real world, this means calling APIs, querying databases, or triggering workflows. In your football match, tool integration is how your agents interact with the game engine.
Your agents' primary "tools" in this workshop are the game commands themselves — `MOVE_TO` , `SHOOT` , `PASS` , `PRESS_BALL` , and so on. But the concept extends further:
- Your agent receives structured data about the pitch. How it parses and interprets that data is a form of tool use.
- An agent might use a tool to calculate whether it has enough energy to sprint into a pressing position.
- An agent could reference a pre-built decision matrix for set-piece situations.
The key principle: tools extend what your agent can do beyond pure reasoning. They give it access to data and capabilities that the LLM alone doesn't have.
[Guardrails — The Referee](#guardrails-the-referee)
Agents operating autonomously need boundaries. Without guardrails, an agent might:
- Return an invalid command that crashes the game engine
- Spend its entire stamina budget in the first five minutes
- Make decisions that violate the rules of the game
- Enter an infinite reasoning loop and miss its response window
Guardrails are the safety net. They include:
- Ensuring the agent's response is a valid game command before it's sent to the engine
- Capping how much compute time or how many LLM calls an agent can make per tick
- Hard rules that override the LLM's reasoning ("never leave the penalty box if you're the goalkeeper")
- Default behaviors when the agent fails to respond in time ("if no command is returned, hold position")
Think of guardrails as the referee. The players (agents) make the decisions, but the referee ensures the game stays fair, safe, and within the rules.
[Observability — The Video Analysis Room](#observability-the-video-analysis-room)
You can't improve what you can't measure. Observability gives you visibility into every decision your agents make — what they saw, what they considered, and why they chose a particular action.
When your striker keeps missing open goals, you need to know why. Was the game state parsed incorrectly? Did the LLM reason poorly? Was the response too slow and the window of opportunity closed? Observability answers these questions.
Key things to monitor:
- The full chain from game state input → LLM reasoning → action output
- How long each agent takes to respond per tick
- How often agents return invalid commands or fail to respond
- Are your agents actually executing the strategy you designed, or drifting into unexpected behaviors?
In this workshop, Amazon Bedrock AgentCore Observability provides unified dashboards to trace agent decisions, visualize workflows, and identify bottlenecks. It's your team's video analysis room — review the tape, find the problems, fix them before the next match.
[Putting It All Together](#putting-it-all-together)
Here's how all the components connect during a single tick of a football match:

```
Game Engine sends game state ↓ Agent receives state (Tool Integration) ↓ State Manager updates context (State Management) ↓ System Prompt + State + Game State → LLM (Foundation Model) ↓ LLM reasons and returns action (System Prompt guides reasoning) ↓ Guardrails validate the action (Guardrails) ↓ Orchestrator coordinates across all 5 agents (Orchestration) ↓ Valid commands sent to Game Engine ↓ Observability logs everything (Observability) ↓ Repeat.
```

This happens every few seconds, for every agent, for the entire match. The quality of each component — and how well they work together — determines whether your team plays like a well-drilled squad or a group of strangers who just met in the parking lot.
Build the system right, and your agents will take care of the rest.
[What's Next](#what's-next)
You've designed the system — the tactics, the roles, the coordination. Now you need a stadium to play in. Next up: the infrastructure that makes it all run at scale on match day.
