# Phase 1: Build Your Team

Every great football team starts somewhere. Yours starts here — with code, creativity, and a bit of competitive fire.
In this phase, you'll go from zero to a fully deployed AI football squad. You'll design your agents' strategies, deploy them to Amazon Bedrock AgentCore , and get them ready for the pitch — all with the help of agentic coding tools like Kiro to keep you moving fast.
By the end, your 5 AI players will be live on AWS and ready to compete. And the workflow you learn here — design, test, deploy, iterate — is the same one you'd use to ship agents for any use case back at work.
[Choose Your Path](#choose-your-path)
There are three ways to complete this phase. Pick the one that fits your style — you'll follow it through the next few pages.
Full developer experience. Clone the sample agent code, explore it in your IDE, test locally, and deploy via CLI. Uses `bash` commands and Unix-style paths throughout.
Best for: Developers on macOS or Linux who want full control and want to understand how the agents work under the hood.
💡 Using Kiro?
Make sure Kiro is installed and connected to your workshop AWS account before starting this path. Kiro will help you clone the repo, understand the code, test agents, and deploy, all from one place. Haven't set it up yet? Follow the
[Kiro Setup Guide](/agentic-football/en-US/appendix-setup/kiro-setup/)
.
You can switch paths later
, but it's easiest to pick one now and stick with it. Each page in this phase has tabs matching these three paths.
[How It Works](#how-it-works)
Your agents are the only components you build and deploy. Everything else — the match server, match orchestration, the Player Portal — is managed centrally by the workshop infrastructure.
Each team has 5 players , and each player is controlled by its own agent deployed to AgentCore. You deploy 5 agents to AgentCore in your AWS account — one per player.
During a match, the Agent Loop calls each of your 5 agents periodically with the current game state (ball position, all players' positions, score, time). Each agent decides what its player should do and returns a football command. The match server then applies those commands.
#m-chart-1{font-family:var(--font-family-base-17wkej, 'Amazon Ember', 'Helvetica Neue', Roboto, Arial, sans-serif);font-size:16px;fill:#333;}#m-chart-1 .error-icon{fill:#552222;}#m-chart-1 .error-text{fill:#552222;stroke:#552222;}#m-chart-1 .edge-thickness-normal{stroke-width:2px;}#m-chart-1 .edge-thickness-thick{stroke-width:3.5px;}#m-chart-1 .edge-pattern-solid{stroke-dasharray:0;}#m-chart-1 .edge-pattern-dashed{stroke-dasharray:3;}#m-chart-1 .edge-pattern-dotted{stroke-dasharray:2;}#m-chart-1 .marker{fill:#333333;stroke:#333333;}#m-chart-1 .marker.cross{stroke:#333333;}#m-chart-1 svg{font-family:var(--font-family-base-17wkej, 'Amazon Ember', 'Helvetica Neue', Roboto, Arial, sans-serif);font-size:16px;}#m-chart-1 .label{font-family:var(--font-family-base-17wkej, 'Amazon Ember', 'Helvetica Neue', Roboto, Arial, sans-serif);color:#333;}#m-chart-1 .cluster-label text{fill:#333;}#m-chart-1 .cluster-label span,#m-chart-1 p{color:#333;}#m-chart-1 .label text,#m-chart-1 span,#m-chart-1 p{fill:#333;color:#333;}#m-chart-1 .node rect,#m-chart-1 .node circle,#m-chart-1 .node ellipse,#m-chart-1 .node polygon,#m-chart-1 .node path{fill:#ECECFF;stroke:#9370DB;stroke-width:1px;}#m-chart-1 .flowchart-label text{text-anchor:middle;}#m-chart-1 .node .katex path{fill:#000;stroke:#000;stroke-width:1px;}#m-chart-1 .node .label{text-align:center;}#m-chart-1 .node.clickable{cursor:pointer;}#m-chart-1 .arrowheadPath{fill:#333333;}#m-chart-1 .edgePath .path{stroke:#333333;stroke-width:2.0px;}#m-chart-1 .flowchart-link{stroke:#333333;fill:none;}#m-chart-1 .edgeLabel{background-color:#e8e8e8;text-align:center;}#m-chart-1 .edgeLabel rect{opacity:0.5;background-color:#e8e8e8;fill:#e8e8e8;}#m-chart-1 .labelBkg{background-color:rgba(232, 232, 232, 0.5);}#m-chart-1 .cluster rect{fill:#ffffde;stroke:#aaaa33;stroke-width:1px;}#m-chart-1 .cluster text{fill:#333;}#m-chart-1 .cluster span,#m-chart-1 p{color:#333;}#m-chart-1 div.mermaidTooltip{position:absolute;text-align:center;max-width:200px;padding:2px;font-family:var(--font-family-base-17wkej, 'Amazon Ember', 'Helvetica Neue', Roboto, Arial, sans-serif);font-size:12px;background:hsl(80, 100%, 96.2745098039%);border:1px solid #aaaa33;border-radius:2px;pointer-events:none;z-index:100;}#m-chart-1 .flowchartTitleText{text-anchor:middle;font-size:18px;fill:#333;}#m-chart-1 :root{--mermaid-font-family:var(--font-family-base-17wkej, 'Amazon Ember', 'Helvetica Neue', Roboto, Arial, sans-serif);}
MANAGED BY WORKSHOP
Game State ↔ Football Commands
Amazon Bedrock AgentCore
Agent 1
Agent 2
Agent 3
Agent 4
Agent 5
YOUR AWS ACCOUNT
Player Portal
Register teams, start matches,
watch live games
Match Server
Physics engine,
game rules, game state
Agent Loop
Sends game state,
collects commands
- [Get the Sample Agents](/agentic-football/en-US/5-create-your-team/get-sample-agents)
- [Set Up and Test](/agentic-football/en-US/5-create-your-team/setup-and-test)
- [Deploy to AWS](/agentic-football/en-US/5-create-your-team/deploy-to-aws)
