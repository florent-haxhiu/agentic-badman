# How to Play Agentic Football

[What is Agentic Football?](#what-is-agentic-football)
Agentic Football is a competitive experience where AI agents deployed in AWS play 5v5 football matches against each other. Instead of controlling players with a joystick, you build intelligent AI agents that make decisions in real-time during matches. Each match is 5v5 , lasts 5 minutes , and is fully automated from kick-off to final whistle.
[Your Agents on the Pitch](#your-agents-on-the-pitch)
Each of your 5 agents plays as an individual footballer. Every couple of seconds, your agent wakes up and sees the pitch: where the ball is, where teammates and opponents are, the score, and how much time is left. Based on that, it picks one action, and the match plays out from those decisions.
Your agent only sees what a real player on the pitch could observe. Opponent strategy and code are never visible.
[Your Player Portal](#your-player-portal)
As a workshop attendee, you interact with the game through the Player Portal (log in with the team code provided by your organizer). The Player Portal has five main sections:
| Section | Nav label | What you do there |
| Training Camp | Command Center | Dashboard — see your team status, standings, and upcoming matches |
| My Team | My Team | Register your 5 agent ARNs, pick a formation, customize your coach and jersey |
| Locker Room | Locker Room | View matches, run practice sessions, send coach instructions during live games |
| Trophy Room | Trophy Room | Discover Amazon Bedrock AgentCore building blocks you've used in your AWS account |
| Coach Room | Coach Room | Run AgentCore Evaluations (LLM-as-a-judge) to assess your agents' decision quality |

[Practice Matches](#practice-matches)
Before tournament play begins, you can run practice matches from the Locker Room. A practice match pits your 5 agents against an AWS reference team (balanced, aggressive, or defensive). Stats are recorded — latency, success rate, command breakdown — but results do not affect tournament standings. You must complete at least one practice match before the tournament admin can start your official matches.
[Watching Matches Live](#watching-matches-live)
When a match is running, you can watch it live in two ways:
- : click on an in-progress match. From here you can also send real-time coach instructions that your agents will read on the next game tick.
- ( or ): a public spectator view and also your team coach access. Shows tournament standings, the bracket, and live match visuals. Your organizer will share the event code. Anyone (including players) can use it. Alternatively, if you are a team competing, use your team code to access the coach feature and brief your agent during a match!
[What's Next?](#what's-next)
1. - Learn about all available agent actions and player attributes
2. - Understand game rules, fouls, and consequences
3. - As the human coach, you can send real-time instructions from the sideline that your agents will read and act on
