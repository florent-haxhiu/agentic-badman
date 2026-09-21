# What is Football?

[The Beautiful Game](#the-beautiful-game)
Football (or soccer as it's known in the US, Canada, and Australia) isn't just a sport. It's the single most unifying force on the planet.
Over 4 billion people watched the 2022 FIFA World Cup. That's more than half the humans alive. No other event (not the Olympics, not the Super Bowl, not any concert or broadcast in history) comes close. When a World Cup match kicks off, entire countries stop. Streets empty. Offices go quiet. Strangers in bars become best friends for 90 minutes.
250 million people play football actively across 200+ countries . From kids kicking a ball made of plastic bags on a dirt road in Lagos, to packed 80,000-seat stadiums in Barcelona, to Sunday league matches in a London park. The game is everywhere. It doesn't need expensive equipment. It doesn't need a perfect field. All it needs is a ball and the desire to play.
And at its core? It's beautifully simple: two teams, one ball, put it in the other team's net.
[Why Football Is the Perfect Challenge for AI](#why-football-is-the-perfect-challenge-for-ai)
Here's what makes football fascinating from an AI perspective: simplicity of rules, infinite complexity of play.
The rules fit on a single page. But the decisions? A midfielder receiving the ball has to process dozens of variables in a split second:
- Where are my teammates? Are they making runs?
- Where are the defenders? Is there a gap?
- Should I pass short, play long, dribble, or shoot?
- What's the score? How much time is left? Do we need to take risks?
Now multiply that by 11 players, all making these decisions simultaneously, reacting to each other in real time. That's what makes football the ultimate multi-agent coordination problem, and why it's the perfect sandbox for this workshop.
[How the Game Works](#how-the-game-works)
A standard match is 90 minutes (two 45-minute halves) with 11 players per side . Here's the cast:
| Role | Job | Think of it as... |
| Goalkeeper | Only player who can use their hands. Last line of defense. | The safety net |
| Defenders | Stop the opposition from scoring. Win the ball back. | The shield |
| Midfielders | Control the tempo. Connect defense to attack. Create chances. | The brain |
| Forwards | Score goals. Make runs. Finish chances. | The weapon |

The key rules are intuitive:
- No hands (except the goalkeeper in their box)
- Ball out of bounds → throw-in, corner kick, or goal kick to restart
- Fouls → free kicks (and penalties if inside the box)
- Offside → you can't just camp by the opponent's goal waiting for a pass
[Reading the Field](#reading-the-field)
A football pitch is divided into zones, and understanding them is critical — for human players and AI agents alike:
- Protect your goal. Don't take risks here.
- The battleground. Whoever controls this zone usually controls the match.
- Where chances are created and goals are scored.
- High-stakes territory. A foul here means a penalty kick — almost a guaranteed goal.
Great teams don't just have talented individuals. They have players who understand spacing (don't crowd each other), width (stretch the defense), depth (offer passing options at different distances), and positioning (be where the ball is going, not where it is).
Sound familiar? These are the same principles your AI agents will need to learn.
[Your Challenge: 5v5 AI Football](#your-challenge:-5v5-ai-football)
In this workshop, you won't be watching football. You'll be building the players.
Your AI agents will compete in a 5v5 format — a faster, more intense version of the full 11v11 game. Fewer players means every decision matters more. There's nowhere to hide. Your agents will need to:
- Read the state of the pitch in real time
- Choose between passing, shooting, moving, or defending
- Work as a team, not just a collection of individuals
- React to what the opponent does, not just follow a script
This is multi-agent AI in its purest form. And the scoreboard doesn't lie.
Now that you know the basics, let's talk tactics. Click Next to explore the strategies and formations that win matches, and that your AI agents will need to master.
