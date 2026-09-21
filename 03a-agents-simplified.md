# Agents Simplified

In this competition, every player on your football team is an AI agent. Each one perceives the pitch, decides what to do, and acts — all on its own, multiple times per second. You've just learned what football is and how the beautiful game works. Now imagine replacing every human player with an autonomous AI that has to make those same split-second decisions — read the play, pick a pass, time a tackle — without any human input.
But what exactly is an AI agent? And why should you care?
[The Core Idea](#the-core-idea)
An AI agent is a piece of software that uses a large language model (LLM) as its brain. It takes in information, reasons about what to do, picks from a set of available actions, and executes. Unlike a simple chatbot that just responds to questions, an agent can plan, use tools, and take multi-step actions to accomplish a goal.
Think about what a human footballer does in a match. They scan the pitch, process dozens of variables — teammate positions, defender movements, the score, the clock — and make a decision in a fraction of a second. Pass left. Dribble forward. Shoot. Track back. That loop of perceive → reason → act is exactly what an AI agent does.
The difference? A human does it on instinct built over years of training. Your agent does it with an LLM processing structured game state and returning a command — every few seconds, for every player, for the entire match.
[How Your Football Agents Work](#how-your-football-agents-work)
In the context of this workshop, the agent loop looks like this:
[1. Perceive — Read the Pitch](#1.-perceive-read-the-pitch)
Every tick, your agent receives a snapshot of the game state. This includes:
- The position of every player on both teams
- Who has the ball
- The current score and match clock
- Your agent's stamina level
- The positions of the goals
This is your agent's "vision." It's the raw data that feeds into every decision.
[2. Reason — Think Like a Midfielder](#2.-reason-think-like-a-midfielder)
This is where the LLM earns its keep. Given the game state, your agent needs to figure out the best move. The reasoning might look something like:
> "I have the ball. There's a teammate open on the left wing with no defender nearby. The goal is 35 yards away — too far for a reliable shot. A short pass to the left creates a better scoring opportunity."
The quality of this reasoning — how well your agent weighs options, considers risk, and anticipates what happens next — is what separates a championship team from one that gets knocked out in the group stage.
[3. Act — Execute the Decision](#3.-act-execute-the-decision)
Your agent returns a command — `MOVE_TO` , `SHOOT` , `PASS` , `PRESS_BALL` , `MARK` , `INTERCEPT` , `SET_STANCE` , or one of the other supported commands. That command gets executed in the game engine, the pitch state updates, and the loop starts again.
Simple in concept. Endlessly complex in practice.
[What Makes Agents Different from Chatbots](#what-makes-agents-different-from-chatbots)
If you've used ChatGPT or Amazon Q, you've interacted with an LLM. But a chatbot and an agent are fundamentally different:
|  | Chatbot | Agent |
| Interaction | You ask, it answers | It observes, decides, and acts autonomously |
| Memory | Remembers the current conversation | Can maintain state across multiple interactions |
| Tools | Limited to text generation | Can call APIs, read data, execute actions |
| Planning | Responds to one prompt at a time | Can break goals into multi-step plans |
| Autonomy | Waits for your input | Operates independently toward a goal |

Your football agents are firmly in the "agent" column. Nobody is typing prompts to them during a match. They receive game state, reason about it, and act — hundreds of times per game, completely autonomously.
[The Spectrum of Agent Complexity](#the-spectrum-of-agent-complexity)
Not all agents are created equal. There's a spectrum from simple to sophisticated:
[Reactive Agents — "If This, Then That"](#reactive-agents-"if-this-then-that")
The simplest form. The agent follows hardcoded rules: if the ball is within 10 yards and I'm a forward, shoot. No reasoning, no adaptation. Fast, but predictable and easy to exploit.
[Reasoning Agents — "Let Me Think About This"](#reasoning-agents-"let-me-think-about-this")
These agents use an LLM to evaluate the situation and choose the best action. They can handle novel situations, weigh tradeoffs, and make nuanced decisions. This is the baseline for what you'll build in this workshop.
[Adaptive Agents — "I've Seen This Before"](#adaptive-agents-"i've-seen-this-before")
Agents that learn from experience. They remember what worked in previous matches, recognize opponent patterns, and adjust their strategy over time. Memory and context management make this possible, and it's where the real competitive edge lives.
[Collaborative Agents — "We're in This Together"](#collaborative-agents-"we're-in-this-together")
Multiple agents working as a coordinated unit. Your five players aren't just five independent decision-makers. They're a team. They need to coordinate positioning, share tactical awareness, and execute plays that require synchronized movement. This is multi-agent collaboration, and it's the ultimate challenge of this workshop.
[Beyond Football — Why Agents Matter](#beyond-football-why-agents-matter)
AI agents aren't limited to football, of course. The same perceive-reason-act pattern powers real-world applications across every industry:
- Agents that don't just answer questions but actually resolve issues by accessing systems, processing refunds, and escalating when needed
- Agents that write code, run tests, debug failures, and deploy to production (you're using one right now if you're building with Kiro)
- Agents that monitor inventory, predict demand, negotiate with suppliers, and reroute shipments when disruptions hit
- Agents that triage patient symptoms, cross-reference medical records, and surface relevant research for clinicians
- Agents that analyze market data, assess risk, and execute trades within defined parameters
The football pitch is your sandbox. The skills you build here — prompt engineering, state management, multi-agent coordination, tool integration — transfer directly to building production agent systems in any domain.
[What You'll Build](#what-you'll-build)
By the end of this workshop, your agents will:
- the full game state every tick
- about tactical situations using an LLM
- by returning valid game commands
- with teammates as a cohesive unit
- their strategy based on the score, clock, and opponent behavior
Five autonomous agents. One shared objective. Zero human intervention during the match.
That's the power of agentic AI, and you're about to build it from scratch.
[What's Next](#what's-next)
You know what an agent is and what yours will do on the pitch. But a single brilliant player doesn't win tournaments. A well-organized team does. Next, you'll learn how to connect your five agents into a coordinated agentic system that plays like a squad, not a collection of strangers.
