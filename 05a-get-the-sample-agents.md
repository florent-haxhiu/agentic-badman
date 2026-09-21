# Get the Sample Agents

You don't have to start from scratch. We've built sample agents that are ready to play. Grab them, explore how they work, and use them as your launchpad. Once you understand the strategy, you can tweak it or build something entirely new.
[Step 1: Clone the Repository](#step-1:-clone-the-repository)

```
1 2 3 4 git clone --filter=blob:none --sparse https://github.com/aws-samples/sample-ai-possibilities cd sample-ai-possibilities git sparse-checkout set agentic-football-sample-agents cd agentic-football-sample-agents
```

All commands in this workshop assume you're in the
`agentic-football-sample-agents`
directory.
If you ever get a "file not found" error, run
`cd ~/sample-ai-possibilities/agentic-football-sample-agents`
to get back to the right place.
[Step 2: Explore the Project Structure](#step-2:-explore-the-project-structure)
💡 Kiro Tip:
Open the repo in Kiro and ask it to explain any file or folder. Try:
"What does the lib/ folder do?"
or
"Explain ai-gk/src/main.py"
— Kiro can walk you through the code at any stage.
The repo includes a shared library and pre-built team strategies you can use as starting points:

```
agentic-football-sample-agents/ ├── lib/ # Shared library (used by ALL teams) │ ├── agent_base.py # Agent factory + invoke handler │ ├── fallback.py # Rule-based fallback per position │ ├── parsing.py # Extracts JSON commands from LLM │ ├── state.py # Summarizes game state for the LLM │ ├── _bootstrap.py # Resolves lib/ path at runtime │ └── test_helpers.py # Mock AgentCore + sample game state │ ├── ai-team-strands-balanced/ # ⚖️ Balanced strategy (start here) ├── ai-team-strands-extremely-aggressive/ # 🔥 All-out attack ├── ai-team-strands-extremely-defensive/ # 🛡️ Park the bus └── ... # More teams may be added
```

Each team folder contains 5 agents — one per player — plus a deployment script and a README file:

```
ai-team-strands-balanced/ ├── ai-gk/ # Goalkeeper (Player 0) ├── ai-def/ # Defender (Player 1) ├── ai-mid/ # Midfielder (Player 2) ├── ai-fwd1/ # Forward 1 (Player 3) ├── ai-fwd2/ # Forward 2 (Player 4) ├── deploy-all-windows.ps1 # Deploys all 5 agents (PowerShell) ├── deploy-all.sh # Deploys all 5 agents (bash) └── README.md
```

And each agent has the same internal structure:

```
ai-gk/ ├── src/main.py # Agent code ├── .bedrock_agentcore.yaml.template # AgentCore config template ├── requirements.txt # Python dependencies └── test_local.py # Local tests (no AWS needed)
```

The sample teams use a 1-1-1-2 formation (GK, DEF, MID, FWD, FWD), but you're free to set up your team however you want. Want 3 forwards? Two midfielders? Go for it — each agent's role is defined entirely by its system prompt, so you can assign any tactical role to any player.
[Step 3: Understand the Agent Code](#step-3:-understand-the-agent-code)
Each agent's `main.py` follows the same pattern. Here's the goalkeeper as an example:

```
1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 # 1. Position config — which player this agent controls MY_PLAYER_ID = 0 POSITION_LABEL = "GK" # 2. System prompt — tells the LLM its role and available commands SYSTEM_PROMPT = f"""You are an AI soccer goalkeeper controlling ONLY player {MY_PLAYER_ID}. Stay near your goal line, track the ball, distribute quickly after saves...""" # 3. Fallback — rule-based behavior when the LLM fails fallback_commands = build_fallback(GK_CONFIG) # 4. Wire it up — create the agent with a Bedrock model agent = create_agent(SYSTEM_PROMPT, model_id="us.amazon.nova-micro-v1:0") create_invoke_handler(app, agent, MY_PLAYER_ID, POSITION_LABEL, fallback_commands, fallback_cfg=GK_CONFIG)
```

[Three Layers of Error Handling](#three-layers-of-error-handling)
Every agent has built-in resilience. If one layer fails, the next one catches it:
#m-chart-1{font-family:var(--font-family-base-17wkej, 'Amazon Ember', 'Helvetica Neue', Roboto, Arial, sans-serif);font-size:16px;fill:#333;}#m-chart-1 .error-icon{fill:#552222;}#m-chart-1 .error-text{fill:#552222;stroke:#552222;}#m-chart-1 .edge-thickness-normal{stroke-width:2px;}#m-chart-1 .edge-thickness-thick{stroke-width:3.5px;}#m-chart-1 .edge-pattern-solid{stroke-dasharray:0;}#m-chart-1 .edge-pattern-dashed{stroke-dasharray:3;}#m-chart-1 .edge-pattern-dotted{stroke-dasharray:2;}#m-chart-1 .marker{fill:#333333;stroke:#333333;}#m-chart-1 .marker.cross{stroke:#333333;}#m-chart-1 svg{font-family:var(--font-family-base-17wkej, 'Amazon Ember', 'Helvetica Neue', Roboto, Arial, sans-serif);font-size:16px;}#m-chart-1 .label{font-family:var(--font-family-base-17wkej, 'Amazon Ember', 'Helvetica Neue', Roboto, Arial, sans-serif);color:#333;}#m-chart-1 .cluster-label text{fill:#333;}#m-chart-1 .cluster-label span,#m-chart-1 p{color:#333;}#m-chart-1 .label text,#m-chart-1 span,#m-chart-1 p{fill:#333;color:#333;}#m-chart-1 .node rect,#m-chart-1 .node circle,#m-chart-1 .node ellipse,#m-chart-1 .node polygon,#m-chart-1 .node path{fill:#ECECFF;stroke:#9370DB;stroke-width:1px;}#m-chart-1 .flowchart-label text{text-anchor:middle;}#m-chart-1 .node .katex path{fill:#000;stroke:#000;stroke-width:1px;}#m-chart-1 .node .label{text-align:center;}#m-chart-1 .node.clickable{cursor:pointer;}#m-chart-1 .arrowheadPath{fill:#333333;}#m-chart-1 .edgePath .path{stroke:#333333;stroke-width:2.0px;}#m-chart-1 .flowchart-link{stroke:#333333;fill:none;}#m-chart-1 .edgeLabel{background-color:#e8e8e8;text-align:center;}#m-chart-1 .edgeLabel rect{opacity:0.5;background-color:#e8e8e8;fill:#e8e8e8;}#m-chart-1 .labelBkg{background-color:rgba(232, 232, 232, 0.5);}#m-chart-1 .cluster rect{fill:#ffffde;stroke:#aaaa33;stroke-width:1px;}#m-chart-1 .cluster text{fill:#333;}#m-chart-1 .cluster span,#m-chart-1 p{color:#333;}#m-chart-1 div.mermaidTooltip{position:absolute;text-align:center;max-width:200px;padding:2px;font-family:var(--font-family-base-17wkej, 'Amazon Ember', 'Helvetica Neue', Roboto, Arial, sans-serif);font-size:12px;background:hsl(80, 100%, 96.2745098039%);border:1px solid #aaaa33;border-radius:2px;pointer-events:none;z-index:100;}#m-chart-1 .flowchartTitleText{text-anchor:middle;font-size:18px;fill:#333;}#m-chart-1 :root{--mermaid-font-family:var(--font-family-base-17wkej, 'Amazon Ember', 'Helvetica Neue', Roboto, Arial, sans-serif);}
Layer 1: LLM Response
The Strands agent calls an LLM,
which returns a JSON command for the player
Layer 2: Rule-Based Fallback
If the LLM response can't be parsed,
position-specific logic kicks in
Layer 3: Last Resort
If everything fails, a single safe command
(e.g. SET_STANCE) keeps the player moving
This means your agent will never freeze during a match, even if the LLM times out or returns an unexpected response.
