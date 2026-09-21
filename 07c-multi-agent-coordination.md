# Multi-Agent Coordination

Five agents making individually good decisions doesn't make a good team. Coordination is what separates a collection of agents from a system that actually works.
[The Coordination Problem](#the-coordination-problem)
Watch any losing team's replay and you'll see these patterns:
- All 5 agents chase the ball. Nobody holds position.
- Agents spread out perfectly but never pass to each other.
- Two agents press the same opponent, both run to the same position.
- Perfect formation, zero reaction to the opponent.
These aren't individual agent failures. They're coordination failures.
[Coordination Through Roles](#coordination-through-roles)
The simplest and most effective mechanism: give each agent a distinct role with clear boundaries.
For each role, define:
1. Where does this player operate?
2. What does this player do most of the time?
3. When does this player abandon default behavior?
4. When does this player defer to a teammate?
Example: Defender

```
Zone: Defensive third (x: -55 to -15) Primary action: MARK the nearest opponent in my zone Trigger to leave: Ball is in our half and no teammate is closer Handoff: If the ball enters midfield and a midfielder is closer, let them handle it
```

Example: Midfielder

```
Zone: Midfield (x: -15 to 15) Primary action: Support the ball carrier — position for a pass Trigger to leave: We're losing and time is running out — push into attacking third Handoff: If the ball is in the defensive third, let the defenders handle it
```

The handoff rules are critical. Without them, agents step on each other's toes.
[Coordination Through Awareness](#coordination-through-awareness)
Your agents receive the positions of all teammates in the game state. Add rules that reference teammate positions:

```
Passing decisions: - Before shooting, check if a teammate is in a better position. If yes, PASS instead. - If a teammate is making a forward run, consider a THROUGH pass into space ahead of them. Positioning decisions: - If a teammate is already covering a zone, don't move into the same zone. - If the ball carrier is under pressure, move toward them to offer a passing option.
```

This doesn't require code changes. It's pure prompt engineering. But it transforms your agents from 5 individuals into something that resembles a team.
[Common Coordination Mistakes](#common-coordination-mistakes)
| Mistake | How to Fix |
| All agents chase the ball | Give each agent a position and zone in the system prompt |
| Agents ignore open teammates | Add teammate-aware passing rules |
| Two agents mark the same opponent | Add "if a teammate is already marking this player, mark the next nearest threat" |
| Formation collapses under pressure | Add "maintain shape" rules that override ball-chasing |
