# AgentCore Memory

Ever watched a striker fall for the same fake twice? That's your agents right now — every tick is a blank slate.
They can't remember that the opponent's forward always cuts left, or that their last three through-balls got intercepted. AgentCore Memory changes that. It gives your agents cross-tick recall, turning them from amnesiac bots into football brains that learn and adapt as the match unfolds.
With memory enabled, your agents recognize opponent patterns, recall previous tactical decisions, and adjust their play over time — just like real players do. This team variant uses Short-Term Memory (STM) via `AgentCoreMemorySessionManager` , which persists conversation history within a match session. Each of the 5 players is a separate specialized agent (GK, DEF, MID, FWD1, FWD2) with its own memory context.
All commands in this workshop assume you're in the
`agentic-football-sample-agents`
directory. If you get a "file not found" error, run
`cd ~/sample-ai-possibilities/agentic-football-sample-agents`
to get back.
First, install `uv` and set up a Python 3.10 virtual environment. If you already did this during Phase 1, skip to the deploy command below. The `agentcore deploy` command requires Python 3.10 — using a newer version (e.g., 3.13) will cause cross-compilation errors:

```
1 2 3 4 5 curl -LsSf https://astral.sh/uv/install.sh | sh source "$HOME/.local/bin/env" 2>/dev/null || source "$HOME/.cargo/env" 2>/dev/null || true uv venv --python 3.10 .venv --seed source .venv/bin/activate uv pip install bedrock-agentcore-starter-toolkit bedrock-agentcore
```

Then navigate to the memory team folder and run:
[Deploy All 5 Agents](#deploy-all-5-agents)

```
1 2 cd ai-team-strands-memory ./deploy-all.sh
```

The script will create the Memory resource for you and print the `MEMORY_ID` in the output. If you already have a Memory ID from a previous deployment, you can pass it in to reuse it:

```
1 2 3 export MEMORY_ID=mem-xxxxxxxxxxxxxxxx export AWS_DEFAULT_REGION=us-east-1 ./deploy-all.sh
```

Make sure your AWS credentials are valid before running. The script will check for
`agentcore`
,
`aws`
, and
`rsync`
as prerequisites.
[What the Script Does](#what-the-script-does)
For each agent, the script:
1. and AWS credentials
2. creates a directory with the agent's , shared , and
3. fills in your AWS account ID, region, and into from the template
4. runs which packages your code, uploads it, and creates (or updates) an AgentCore Runtime
5. adds inline policy to the execution role (grants Memory API access)
6. removes the directory when done
[Deploy a Single Agent](#deploy-a-single-agent)
To deploy (or redeploy) just one agent:

```
1 ./deploy-all.sh ai-gk
```

[Understanding the Output](#understanding-the-output)
The script shows progress for each agent. Here's what to look for:
Prerequisites check:

```
Checking prerequisites... agentcore CLI: OK rsync: OK aws CLI: OK AWS Account: 123456789012 AWS Region: us-east-1
```

Per-agent deployment:

```
========================================== Deploying: ai-gk ========================================== Deploying from: /path/_build/ai-gk ✅ ai-gk: DEPLOYED
```

Summary:

```
========================================== Deployment Summary ========================================== Deployed: ai-gk ai-def ai-mid ai-fwd1 ai-fwd2 Failed: none Memory: mem-xxxxxxxxxxxxxxxx Account: 123456789012 Region: us-east-1 All agents deployed successfully.
```

[Get Your Agent ARNs](#get-your-agent-arns)
After deployment, go to the Amazon Bedrock console → AgentCore → Runtime and click on each agent to copy its Runtime ARN .
Save these ARNs.
You'll need all 5 ARNs to register your agents in the Player Portal.
[Verify Your Deployment](#verify-your-deployment)
Go to the Amazon Bedrock console → AgentCore → Runtime . Each agent should show status Ready . You should see 5 new agents with `memory` in their names.
[Confirm Memory Is Working](#confirm-memory-is-working)
After playing a match with your memory-enabled agents, you can verify that Memory was actually active.
1. Open the [Amazon Bedrock AgentCore console](https://console.aws.amazon.com/bedrock-agentcore/)
2. In the left navigation pane, choose
3. Click on your Memory resource ( )
4. Scroll down to the section
You should see:
| Metric | What to look for |
| Create events — API invocations | A non-zero count (e.g., 320). Each agent writes an event every tick, so 5 agents × ~64 ticks ≈ 320 e |
| Create events — Errors | Should be 0. Any errors here mean events failed to write. |
| Retrieve extracted memory | Will show 0 invocations — that's expected. This team uses Short-Term Memory (raw events), not long-t |

If the Create events count is zero after a match, your agents aren't writing to Memory. Check that the `MEMORY_ID` environment variable is set correctly on each agent.
[How Memory Works](#how-memory-works)
Think of it like a player's internal monologue during a match. At tick 50, your goalkeeper saves a shot from the opponent's forward who always aims bottom-left. At tick 120, that same forward lines up another shot — but this time, your GK remembers . It shifts early, anticipates the angle, and makes the save look routine.
Each agent has its own isolated memory context — scoped by a unique `session_id` and `actor_id` based on the player's position. The GK only recalls its own saves and decisions, the DEF only its own marking history, and so on. They share the same Memory resource ( `MEMORY_ID` ), but they don't see each other's events. Think of it as 5 separate notebooks stored in the same filing cabinet.
Under the hood, each agent uses `AgentCoreMemorySessionManager` wired into the Strands `Agent` . Every tick follows a three-beat rhythm:
1. the session manager retrieves relevant history from the Memory resource
2. the LLM receives both the current game state recalled context, so it can spot patterns
3. the agent's decision gets stored back into memory for future ticks
The system prompt instructs each agent to use this recalled history:

```
You have MEMORY of previous ticks. Use recalled history to: - Anticipate repeated shot patterns from opponents - Remember which opponents are most dangerous shooters - Adjust positioning based on opponent tendencies from earlier in the match
```

The result? Agents that get smarter as the match progresses. Early ticks are exploratory — by the second half, your team has built a mental model of the opponent.
Next Step
: Update your Player Portal squad with the new Memory agent ARNs — go to
My Team
and replace the Phase 1 ARNs for each position.
