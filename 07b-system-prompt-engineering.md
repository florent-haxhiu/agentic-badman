# System Prompt Engineering

Your system prompt is the single most important piece of your agent. It's the difference between an agent that makes smart, consistent decisions and one that flails around the pitch.
[Anatomy of a Football Agent Prompt](#anatomy-of-a-football-agent-prompt)
A good system prompt has four layers:
[Layer 1: Identity and Role](#layer-1:-identity-and-role)
Tell the agent who it is and what its job is .

```
You are a defensive midfielder on a 5v5 football team. Your primary job is to protect the space between the midfield and the defense. You are Player 2 on the home team.
```

[Layer 2: Decision Hierarchy](#layer-2:-decision-hierarchy)
Tell the agent what matters most . A decision hierarchy resolves trade-offs every tick.

```
When deciding what to do, follow this priority order: 1. If the opponent is in a scoring position near our goal, MARK the nearest threat 2. If a teammate has the ball, hold position to receive a pass 3. If the ball is loose in midfield, PRESS_BALL to win possession 4. If I have the ball, look for a PASS to a teammate in a better position 5. If no better option exists, MOVE_TO toward the opponent's half
```

[Layer 3: Situational Rules](#layer-3:-situational-rules)
Context-dependent overrides based on game state:

```
- When WINNING: Play conservatively. Hold possession. Avoid risky passes. - When LOSING: Push forward. Take more shots. Accept higher defensive risk. - When stamina below 30%: use MOVE_TO with sprint: false.
```

[Layer 4: Constraints](#layer-4:-constraints)
Tell the agent what it should never do:

```
- NEVER leave the defensive third completely empty - NEVER attempt a SHOOT from beyond the midfield line - NEVER use sprint when stamina is below 20%
```

[Common Anti-Patterns](#common-anti-patterns)
[The Vague Prompt](#the-vague-prompt)

```
You are a football player. Play well and try to win.
```

"Play well" means nothing to an LLM. It will make random, inconsistent decisions because it has no priorities to reason about.
[The Novel](#the-novel)

```
You are a world-class footballer playing in the most important match of your career. The crowd is roaring. The stakes are high... [500 more words of narrative]
```

The LLM has a 500ms response window. Every token of fluff is a token not spent on tactical reasoning. Be concise. Every sentence should directly influence a decision.
[The Prompt Template](#the-prompt-template)
Use this as a starting point:

```
You are a [POSITION] on a 5v5 football team. You are Player [ID] on the [HOME/AWAY] team. Your role: [ONE SENTENCE describing primary responsibility] Decision priorities (in order): 1. [HIGHEST PRIORITY action] 2. [SECOND PRIORITY] 3. [THIRD PRIORITY] 4. [DEFAULT action] Situational adjustments: - When WINNING by 2+: [behavior] - When LOSING: [behavior] - When LOW STAMINA: [behavior] You must NEVER: - [Critical constraint 1] - [Critical constraint 2] Available commands: MOVE_TO, FOLLOW_PLAYER, SHOOT, PASS, GK_DISTRIBUTE, PRESS_BALL, MARK, INTERCEPT, SLIDE_TACKLE, SET_STANCE, CLEAR_OVERRIDE, RESET
```

The key insight: different positions need different prompts. Your goalkeeper's decision hierarchy should look nothing like your striker's.
[Encoding Strategy in Language](#encoding-strategy-in-language)
Don't write "Play a counter-attacking style." — too vague. Instead, encode the behaviors :

```
When the OPPONENT has the ball: - All players retreat to our defensive third - MARK the nearest opponent tightly - Do NOT press beyond the midfield line When WE WIN the ball: - Immediately transition to attack - PASS (type: "AERIAL") to the striker - Midfielders sprint to support the attack When WE have the ball in the attacking third: - SHOOT if within range — don't over-pass
```
