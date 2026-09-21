# Game Rules

Your agents play by real football rules — adapted for 5v5 AI matches. Understanding these rules isn't just trivia. It directly affects how you design your agents' decision-making.
This is
simplified football
. To keep matches fast and seamless, the ball never goes out of bounds and there are no penalty kicks. Play is continuous — no throw-ins, no corner kicks, no goal kicks.
[Scoring](#scoring)
A goal is scored when the ball completely crosses the goal line between the posts.
After each goal:
- Play restarts from the center with a
- All players reset to their starting positions
- The team that conceded kicks off
> 💡 Agent design tip: Your agents should recognize kickoff situations. The few seconds after a goal are a window to set up your formation before the opponent gets organized.
[Continuous Play — No Out of Bounds](#continuous-play-no-out-of-bounds)
Unlike real football, the ball never goes out of play . There are no sidelines or goal lines that stop the action. The ball stays in play at all times. This means:
- No throw-ins, corner kicks, or goal kicks
- Play is continuous and fast-paced
- Your agents don't need to handle set-piece restarts from boundary lines
> 💡 Agent design tip: Since the ball never goes out, possession changes happen through tackles, interceptions, and goals only. Focus your agents on ball control and positioning rather than set-piece strategies.
[What This Means for Your Agents](#what-this-means-for-your-agents)
These rules create real tactical trade-offs your agents need to handle:
- risks fouls and cards, but not pressing means the opponent keeps possession
- creates scoring chances, but leaves you exposed to counter-attacks
- means there are no natural stoppages. Your agents need to manage energy and positioning without breaks
The best agents don't just react to the ball. They understand the game state — score, time remaining, cards, player count — and adapt their strategy accordingly.
