# Deploy to AWS

This is the moment. Your agents are about to go live. Once deployed, they'll be running on Amazon Bedrock AgentCore, ready to receive game state and make real-time decisions on the pitch.
All commands below assume you're in the
`agentic-football-sample-agents`
directory. If you get a "file not found" error, run
`cd ~/sample-ai-possibilities/agentic-football-sample-agents`
to get back.
The `deploy-all.sh` script automates the entire deployment process for all 5 agents. Every sample team includes this script, so the steps below work regardless of which team you choose to deploy.
[What the Script Does](#what-the-script-does)
For each agent, the script:
1. creates a directory with the agent's , shared , and
2. fills in your AWS account ID and region into from the template
3. runs which packages your code, uploads it, and creates (or updates) an AgentCore Runtime
4. removes the directory when done
The script also handles IAM role creation automatically via the `execution_role_auto_create: true` setting in each agent's config.
[Deploy All 5 Agents](#deploy-all-5-agents)
Make sure you're in the `agentic-football-sample-agents` directory, then navigate to the team folder and run the script:

```
1 2 cd ai-team-strands-balanced ./deploy-all.sh
```

Make sure your AWS credentials are valid before running. The script will check for
`agentcore`
,
`aws`
, and
`rsync`
as prerequisites.
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
========================================== Deployment Summary ========================================== Deployed: ai-gk ai-def ai-mid ai-fwd1 ai-fwd2 Failed: none Account: 123456789012 Region: us-east-1 All agents deployed successfully.
```

[Get Your Agent ARNs](#get-your-agent-arns)
After deployment, go to the Amazon Bedrock console → AgentCore → Runtime and click on each agent to copy its Runtime ARN .
Save these ARNs.
You'll need all 5 ARNs in the next phase to connect your agents to the match server.
You've deployed the balanced team, a solid starting point. But solid doesn't win tournaments. To compete, you'll need to iterate on your system prompts, tune your strategies, and test against different opponents. The next sections show you how.
Your agents are live.
Time to get them on the pitch — head to Phase 2 to assemble your squad and register your 5 ARNs in the
Player Portal
(My Team page) to play your first match.
