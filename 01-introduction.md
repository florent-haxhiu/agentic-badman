# Introduction

> ☝️ This is a real screenshot from the game. What you see above is exactly what you'll experience — your AI agents playing live on a 3D pitch, controlled entirely by the code you write today.

## Welcome to the Agentic Football World Cup

You're about to build a team of AI agents that play live 5v5 football matches, and compete against other teams in real time. No simulations. No toy demos. Real agents, real tactics, real competition.

Over the next few hours, you'll go from zero to a fully deployed squad of AI-powered football players running on AWS. You'll design their strategy, deploy them to the cloud, and watch them take the pitch against opponents built by other participants in this room.

This isn't just a workshop. It's a tournament.

## What Makes This Different

This workshop puts you in the manager's seat of an AI football team. Every player on your squad is an autonomous agent that receives live game state — ball position, player locations, score — and decides what to do next. Move, pass, shoot, press, mark. Every decision, every tick, powered by AI.

Your agents don't follow scripts. They reason about the game using large language models, then act. And when the whistle blows, you'll watch them play live in the Player Portal — a 3D match viewer where you can see your tactical decisions unfold in real time.

> Every screenshot in this workshop is captured from actual gameplay. These are your agents, on your pitch, making decisions in real time.

## The AWS Services Powering Your Team

This workshop is built on a modern AI agent stack. Here are the core services you'll use:

| Service | What It Does in This Workshop |
|---------|-------------------------------|
| Amazon Bedrock | Provides the foundation models (Amazon Nova) that give your agents the ability to reason about game |
| Amazon Bedrock AgentCore | The managed runtime where your agents are deployed and executed. Handles scaling, networking, and in |
| Strands Agents SDK | The open-source Python framework you'll use to build your agents. Lightweight, flexible, and designe |
| Amazon CloudWatch | Where your agent logs live. Debug decisions, trace reasoning, and understand why your striker passed |
| AWS IAM | Secures your agents and controls what AWS resources they can access |
| Kiro | An agentic IDE that understands your project and helps you build, debug, and iterate on your agents |

You don't need to be an expert in any of these services. The workshop guides you through every step, and the infrastructure is largely pre-configured for you. If you'd like an AI-powered coding assistant along the way, Kiro can help you understand the codebase, troubleshoot issues, and iterate on your agents faster.

## How It Works

```
┌─────────────────────────────────────────┐ ┌───────────────────────────────────┐
│ Managed by Workshop                     │ │ Your AWS Account                  │
│                                         │ │                                   │
│ ┌──────────────────┐ ┌───────────────┐  │ │ ┌───────────────────────────────┐ │
│ │ Match Server     │◄►│ Agent Loop    │◄─┼─────┼─►│ 5 Agents on AgentCore         │ │
│ │ (Physics,        │  │ (Invokes      │  │ │ │ (one per player)              │ │
│ │  Rules)          │  │  agents)      │  │ │ │                               │ │
│ └──────────────────┘  └───────────────┘  │ │ │ You build & deploy            │ │
│                                         │ │ │ these agents ⚽                │ │
│ ┌──────────────────┐                    │ │ └───────────────────────────────┘ │
│ │ Player Portal    │                    │ │                                   │
│ │ (3D Viewer,      │                    │ │ ┌───────────────────────────────┐ │
│ │  Discoveries,    │◄────cross-account──┼─────┼─►│ AgentCore Building            │ │
│ │  Evaluations)    │    IAM role        │ │ │ Blocks + CloudWatch           │ │
│ └──────────────────┘                    │ │ └───────────────────────────────┘ │
│                                         │ │                                   │
│                                         │ │ ┌───────────────────────────────┐ │
│                                         │ │ │ Amazon Bedrock (Nova)         │ │
│                                         │ │ │ Your agents call this         │ │
│                                         │ │ │ to reason about the           │ │
│                                         │ │ │ game each tick                │ │
│                                         │ │ └───────────────────────────────┘ │
└─────────────────────────────────────────┘ └───────────────────────────────────┘
```

Every ~2 seconds during a match, the platform sends to your agents the current game state. Your agent may be using Bedrock models like Amazon Nova to analyze the situation and to return tactical commands — press the ball, mark an opponent, switch formation. The Match Server applies those commands and the game continues.

## What You'll Walk Away With

By the end of this workshop, you will have:

- 🏗️ Built a team of 5 AI agents using the Strands Agents SDK
- 🚀 Deployed them to Amazon Bedrock AgentCore as production-ready serverless agents
- ⚽ Competed in live matches against other teams in the tournament
- 🧠 Learned how multi-agent systems work on AWS, from prompt engineering to deployment to observability
- 🔍 Evaluated your agents' tactical decision-making using the Bedrock AgentCore Evaluate API with built-in and custom LLM-as-a-judge evaluators
- 🏆 Iterated on your agents' tactics to climb the leaderboard, with help from agentic coding tools like Kiro if you choose
- 💼 Every pattern you learn here (agent design, deployment, coordination, evaluation, iteration) maps directly to real-world use cases you can take back to your organization

## Workshop Details

| | |
|---|---|
| Content Level | 200 — Accessible to all skill levels |
| Estimated Duration | 4 hours |
| Who This Is For | Everyone — developers, architects, data scientists, business leaders, and anyone curious about AI agents |
| Background Knowledge | None required. Familiarity with the AWS Console is helpful but not necessary |
| Pre-requisites | A laptop with a browser. AWS accounts and tooling are provided at the event |
| Cost | Free — temporary AWS accounts are provided by event staff. If you choose to use your own account, standard AWS charges apply |
| Supported Regions | us-east-1 |

> 💡 Ready? Click Next to get your event access and AWS account set up.
