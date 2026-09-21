# AgentCore Gateway

Your Phase 1 agents make decisions on vibes — the LLM reads the game state and guesses what to do.
Sometimes it works. Sometimes your forward shoots from 50 yards out because it has no concept of probability. AgentCore Gateway fixes that by giving your agents real tactical tools they can call mid-match. Now instead of guessing, your forward can calculate that a pass has 82% success probability while a shot sits at 12%, and make the smart play.
Gateway exposes your tactical analysis tools as MCP (Model Context Protocol) endpoints that agents call autonomously during gameplay. The agents discover and invoke tools on demand, deciding for themselves when a calculation will improve their decision. Think of it as upgrading your players from "gut feeling" to "data-driven."
This team variant deploys 4 Lambda-backed tactical tools behind an MCP Gateway, then connects each of the 5 player agents to that gateway.
[Available Tactical Tools](#available-tactical-tools)
| Tool | What it does |
| calculate_pass_options | Pass success probability for each teammate based on interception risk |
| evaluate_shot | Shot success probability with aim point recommendation |
| find_open_space | Grid-based open space finder by zone (attack / midfield / defense) |
| get_defensive_assignment | Opponent threat ranking for marking priority |

[Deploy All 5 Agents](#deploy-all-5-agents)
The `deploy-all.sh` script handles the entire setup — Lambda functions, MCP Gateway, and all 5 agents — in a single command.
For this section we use the CLI exclusively. The Gateway setup involves multiple interconnected resources (Lambda functions, IAM roles, MCP Gateway with tool schemas, and agents) that would take significantly longer to configure manually through the console.
All commands in this workshop assume you're in the
`agentic-football-sample-agents`
directory. If you get a "file not found" error, run
`cd ~/sample-ai-possibilities/agentic-football-sample-agents`
to get back.
First, install `uv` and set up a Python 3.10 virtual environment. If you already did this during Phase 1, skip to the deploy command below. The `agentcore deploy` command requires Python 3.10 — using a newer version (e.g., 3.13) will cause cross-compilation errors:

```
1 2 3 4 5 curl -LsSf https://astral.sh/uv/install.sh | sh source "$HOME/.local/bin/env" 2>/dev/null || source "$HOME/.cargo/env" 2>/dev/null || true uv venv --python 3.10 .venv --seed source .venv/bin/activate uv pip install bedrock-agentcore-starter-toolkit
```

Then navigate to the gateway team folder and run:

```
1 2 cd ai-team-strands-gateway ./deploy-all.sh
```

Make sure your AWS credentials are valid before running. The script will check for
`agentcore`
and
`aws`
as prerequisites.
[What the Script Does](#what-the-script-does)
The Gateway team has more moving parts than the balanced or memory teams. Here's what the script sets up for you:
1. Creates (or reuses)
2. Deploys the 4 tactical tool functions
3. Creates (or reuses)
4. Creates the Gateway and registers all 4 Lambda targets
5. Stages, bundles, and deploys all 5 agents with
6. Attaches policy to execution roles
[Deploy a Single Agent](#deploy-a-single-agent)

```
1 ./deploy-all.sh ai-gk
```

[Verify Your Deployment](#verify-your-deployment)
After the script completes, take a moment to explore what it created in the AWS Console.
[Check the Lambda Functions](#check-the-lambda-functions)
Open the [Lambda console](https://console.aws.amazon.com/lambda/) and search for `afwc-gateway-tool` . You should see 4 functions:
| Function | What it does |
| afwc-gateway-tool-calculate-pass-options | Pass success probability calculator |
| afwc-gateway-tool-evaluate-shot | Shot evaluation with aim recommendation |
| afwc-gateway-tool-find-open-space | Open space finder by zone |
| afwc-gateway-tool-get-defensive-assignment | Opponent threat ranking |

Click on any function to see its code in the Code source editor. These are the tactical calculators your agents call during matches. Each one is a self-contained Python function that takes game state data and returns analysis results.
[Check the Gateway](#check-the-gateway)
Go to the [Amazon Bedrock AgentCore console](https://console.aws.amazon.com/bedrock-agentcore/) → Gateways and click on `afwc-tactical-tools` . You should see:
- Status
- 4 registered targets (one per tactical tool)
- The ending in — this is the URL your agents use to call tools
[Check Your Agents](#check-your-agents)
Go to AgentCore → Runtime . Each agent should show status Ready . You should see 5 new agents with `gateway` in their names. Click on any agent to copy its Runtime ARN .
Save your 5 Agent ARNs.
You'll need them to update your squad in the Player Portal.
[Confirm Tools Are Being Used](#confirm-tools-are-being-used)
After playing a match with your gateway-enabled agents, you can verify that the tactical tools were actually called by checking the agent runtime logs.
1. Go to the console → →
2. Click on any gateway agent (e.g., )
3. In the table, click the link to open CloudWatch Logs
In the logs, look for lines like:
| Log pattern | What it means |
| Tool #N: calculate-pass-options | Agent called the pass probability tool |
| Tool #N: evaluate-shot | Agent called the shot evaluation tool |
| Tool #N: find-open-space | Agent called the open space finder |
| Tool #N: get-defensive-assignment | Agent called the defensive assignment tool |

You should also see the agent reasoning about tool results — lines like "the best strategy is to stay near the goal line" or "distribute the ball to our teammate with the safest pass."
If you don't see any tool calls in the logs, check that the `GATEWAY_URL` environment variable is set correctly on each agent and that the Gateway shows status Ready .
[How Agents Use Tools](#how-agents-use-tools)
During a match, a gateway-enabled agent doesn't just react. It analyzes . Picture your midfielder receiving the ball in the center circle. Instead of blindly passing forward, it calls `calculate_pass_options` and discovers the left wing has a 78% success rate while the through-ball is only 35%. Then it checks `evaluate_shot` — 8% from here, not worth it. It picks the smart pass. All of this happens in milliseconds, every single tick.
Each position leans on different tools based on their role:
| Position | Primary Tools | When |
| GK | get_defensive_assignment, calculate_pass_options | Identify threats, distribute after saves |
| DEF | get_defensive_assignment, calculate_pass_options | Mark opponents, find outlet passes |
| MID | calculate_pass_options, find_open_space, evaluate_shot | Distribute, position, shoot vs pass |
| FWD1/2 | evaluate_shot, calculate_pass_options, find_open_space | Shoot decisions, attacking runs |

Next Step
: Update your Player Portal squad with the new Gateway agent ARNs — go to
My Team
and replace the ARNs for each position.
