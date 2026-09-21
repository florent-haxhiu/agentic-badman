# Phase 2: Play Matches

Your agents are deployed and ready. The pitch is waiting.
[Step 1: Get Your Team Code](#step-1:-get-your-team-code)
Your event organizer will provide you with a team code — this is your ticket into the event.
[Step 2: Log In](#step-2:-log-in)
Open the Player Portal at [https://agentic-football.aws.dev](https://agentic-football.aws.dev/) , enter your team code, and log in.
[Step 3: Set Up Your Team](#step-3:-set-up-your-team)
The My Team page guides you through setup with a checklist on the right:
1. pick a logo from the gallery and choose your formation (e.g. , , ). Formation sets starting positions; once the match begins, your agents decide where to move.
2. click each position slot (GK, DEF, MID, FWD) and paste the AgentCore ARN for each agent. You can also set a player name and avatar for each.
3. click the coach name at the top to edit it and change appearance.
To find your agent ARNs: go to the
Amazon Bedrock
console →
AgentCore
→
Runtime
(if you deployed code) or
Harness
(if you used the Harness path), click on each agent, and copy the
ARN
.
[Step 4: Test Your Agents](#step-4:-test-your-agents)
Use the Test your agents option in the Getting Started checklist to verify they respond correctly. This sends a sample game state and confirms connectivity.
If a test fails, check that the agent shows status
Ready
in the AgentCore console and that the IAM cross-account trust policy is correctly configured.
Using Harness?
Test failures can happen if the model produces an unexpected response format. This is normal with Harness agents — the JSON format is defined in the prompt rather than enforced in code. Run the test again. If it fails repeatedly, try switching to a larger model (e.g. Claude Sonnet 4.6, Nova Pro) in your harness configuration.
[Step 5: Play Matches](#step-5:-play-matches)
You're ready to play. During any match you can coach your agents from the sideline — see [Coach Instructions](#coach-instructions) below.
[Practice](#practice)
Play against AWS's built-in AI opponents, each designed to expose different weaknesses:
| Opponent | Style | What it tests |
| The Benchmark FC | Balanced | Standard positioning — a good baseline to measure overall performance |
| Total Attack United | Extremely Aggressive | GK plays sweeper-keeper, DEF joins every attack, FWDs camp near goal — exposes weak counter-attackin |
| Fort Knox Athletic | Extremely Defensive | All players stay deep, MID acts as extra defender, minimal shooting — tests whether your attack can  |

Try each opponent if time allows — they're designed to expose different weaknesses.
[Find Opponents](#find-opponents)
Click Find opponent to see other teams in your event that are ready to play. Challenge them and the game server invokes both teams' agents automatically.
[Coach Instructions](#coach-instructions)
During a live match, you can send instructions to your agents from the sideline — tell your midfielders to press higher, ask your defence to hold the line, or switch to all-out attack in the final minutes.
These are suggestions, not commands. Your agents receive them as part of their game state and may choose to follow them based on their own reasoning. See [Coaching During Matches](/agentic-football/en-US/6b-how-to-play/coaching-during-matches) for details.
[Iterate](#iterate)
Go back to your agent code, tweak the system prompts, rethink your strategy, redeploy to AgentCore, and run another match. Observe → iterate → redeploy → repeat.
LLMs are non-deterministic. Play several matches against the same opponent to gauge consistency. Try swapping foundation models too; different LLMs have different strengths.
💡 Kiro Tip:
After watching a match, describe what you saw to Kiro. Try:
"My agents keep losing the ball in midfield and nobody presses the opponent. Update my system prompt to be more aggressive when we don't have possession."
The portal tracks your progress with XP and daily challenges. Check the
Team Progress
panel to see your next goals.
[What's Next](#what's-next)
Ready to level up? Head to [Phase 3: Supercharge Your Agents](/agentic-football/en-US/8-supercharge) to unlock advanced techniques — prompt engineering, AgentCore features like Memory, Gateway, and Observability — that can give your team a serious edge.
