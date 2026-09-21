# Cleanup

[Clean Up Your Resources](#clean-up-your-resources)
Using a workshop-provided AWS account?
Your account will be automatically cleaned up after the event ends. You can skip this page.
If you used your own AWS account for this workshop, follow the steps below to remove all resources and avoid ongoing charges.
All commands in this workshop assume you're in the
`agentic-football-sample-agents`
directory. If you get a "file not found" error, run
`cd ~/sample-ai-possibilities/agentic-football-sample-agents`
to get back.
[Step 1: Delete AgentCore Agents](#step-1:-delete-agentcore-agents)
From each agent team directory, run:

```
1 agentcore destroy
```

Or delete agents individually from the Amazon Bedrock console → AgentCore → Runtime — select each agent and choose Delete .
[Step 2: Delete the MCP Gateway (Gateway team only)](#step-2:-delete-the-mcp-gateway-(gateway-team-only))
If you deployed the Gateway team:
1. Open the console →
2. Click on
3. Delete all 4 targets first, then delete the gateway
[Step 3: Delete Lambda Functions (Gateway team only)](#step-3:-delete-lambda-functions-(gateway-team-only))
Open the [Lambda console](https://console.aws.amazon.com/lambda/) and delete these functions:
[Step 4: Delete the Memory Resource (Memory team only)](#step-4:-delete-the-memory-resource-(memory-team-only))
If you deployed the Memory team:
1. Open the console →
2. Select and choose
[Step 5: Clean Up IAM Roles](#step-5:-clean-up-iam-roles)
The deploy scripts created these IAM roles. Delete them from the [IAM console](https://console.aws.amazon.com/iam/) → Roles :
- (Gateway Lambda execution role)
- (Gateway service role)
- Any roles starting with (agent execution roles)
[Step 6: Verify](#step-6:-verify)
Go to the AgentCore console → Runtime . You should see no agents listed. Check Gateways and Memory — both should be empty.
