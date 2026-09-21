# Set Up and Test

Before you send your agents to the cloud, make sure they actually work. This step catches issues early — broken imports, bad prompts, parsing errors — so your first deployment goes smoothly.
All commands below assume you're in the
`agentic-football-sample-agents`
directory. If you get a "file not found" error, run
`cd ~/sample-ai-possibilities/agentic-football-sample-agents`
to get back.
[Install Prerequisites](#install-prerequisites)
You need Python 3.10+, the AWS CLI, uv (a fast Python package manager), Strands Agents, and the AgentCore CLI.

```
1 2 3 4 5 6 7 8 9 10 11 12 13 # Install uv (required for deploying agents later) curl -LsSf https://astral.sh/uv/install.sh | sh source "$HOME/.local/bin/env" 2>/dev/null || source "$HOME/.cargo/env" 2>/dev/null || true # Create a virtual environment python3 -m venv .venv source .venv/bin/activate # Install Strands Agents and the AgentCore CLI pip install strands-agents bedrock-agentcore-starter-toolkit # Install agent dependencies (each agent has the same deps — pick any one) pip install -r ai-team-strands-balanced/ai-gk/requirements.txt
```

uv
is required for the deployment step — it cross-compiles Python dependencies for the AgentCore Linux ARM64 runtime. If you skip this,
`uv pip install`
commands on the Deploy page will fail.
[Verify AWS Credentials](#verify-aws-credentials)
Your agents call Amazon Bedrock, so you need valid AWS credentials. Your Workshop Studio event account provides them for you:
1. Go to your Workshop Studio event page
2. Click
3. Copy and paste the commands into your terminal

```
1 2 3 4 export AWS_ACCESS_KEY_ID=... export AWS_SECRET_ACCESS_KEY=... export AWS_SESSION_TOKEN=... export AWS_DEFAULT_REGION=...
```

Verify your credentials are working:

```
1 aws sts get-caller-identity
```

If this command fails or shows expired credentials, refresh them before continuing. The agent needs access to Amazon Bedrock models in your region.
[Test Your Agents](#test-your-agents)
Before deploying to AWS, test your agents locally to make sure they work.
[Run Offline Tests (No AWS Credentials Needed)](#run-offline-tests-(no-aws-credentials-needed))
Each agent includes a `test_local.py` that validates the state summarizer, command parser, and fallback logic — all without calling AWS:

```
1 2 3 4 cd ai-team-strands-balanced # Test the goalkeeper agent python3 ai-gk/test_local.py
```

You'll see output like:

```
=== STATE SUMMARY (GK, player 0) === [Game state summary text...] === FALLBACK (GK) === [OK] P0 T0: MOVE_TO {'target_x': -49.5, 'target_y': 0, 'sprint': False} All 1 commands have correct playerId=0 and teamId=0 === FALLBACK WITH BALL (GK) === P0: GK_DISTRIBUTE {'target_player_id': 1, 'method': 'THROW'} Correctly distributes ball via THROW === PARSE TESTS === [PASS] '[{"commandType":"GK_DISTRIBUTE"...' -> 1 cmds (expected 1) [PASS] 'Here:\n[{"commandType":"MOVE_TO"...' -> 1 cmds (expected 1) All parse tests passed, playerId correctly forced
```

Test all 5 agents to make sure everything works:

```
1 2 3 4 5 python3 ai-gk/test_local.py python3 ai-def/test_local.py python3 ai-mid/test_local.py python3 ai-fwd1/test_local.py python3 ai-fwd2/test_local.py
```

[Run LLM Tests (Needs AWS Credentials)](#run-llm-tests-(needs-aws-credentials))
To test with a real Bedrock model call, add the `--llm` flag:

```
1 python3 ai-gk/test_local.py --llm
```

This sends a sample game state to the model and shows the raw LLM response plus parsed commands. Use this to verify your system prompts produce valid output.
When you're done testing, go back to the
`agentic-football-sample-agents`
directory before continuing:
`cd ..`
Each agent folder has its own
`requirements.txt`
with dependencies like
`strands-agents`
and
`aws-opentelemetry-distro`
. You only need to install from one agent's file — the dependencies are the same across all agents in a team.
💡 Kiro Tip:
If a test fails, paste the error into Kiro. Try:
"My ai-def test_local.py is failing with this error — what's wrong?"
Kiro can read the test file and suggest fixes.
