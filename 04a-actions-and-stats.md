# Actions and Stats

This section covers all available commands your agents can issue and the game state fields they receive each tick.
| Timing | Value |
| Invocation rate | ~1 invocation every 2 seconds |
| Decision timeout | 5 seconds maximum — if your agent doesn't respond in time, the player holds their last command |

[Commands](#commands)
Your agent returns a JSON array of commands. Each command targets a player by `playerId` (integer 0–4, where 0 is always the GK).
| Command | Parameters | Description |
| MOVE_TO | target_x (float), target_y (float), sprint (bool) | Move to specific pitch coordinates. sprint: true is faster but drains stamina. |
| FOLLOW_PLAYER | target_player_id (int), target_team ("HOME" | "AWAY"), distance (float) | Shadow a player at a set distance — useful for loose marking or tracking a run. |

Field coordinates: x ≈ −55 to +55, y ≈ −35 to +35. Team 0 (HOME) attacks toward +x. Team 1 (AWAY) attacks toward −x.
[Game State](#game-state)
Each tick your agent receives:

```
1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 { "gameState": { "tick": 42, "gameTime": 84.0, "playMode": "OPEN_PLAY", "score": { "home": 1, "away": 0 }, "ball": { "position": { "x": 12.5, "y": -3.0, "z": 0.0 }, "velocity": { "x": 1.2, "y": 0.0, "z": 0.0 }, "isFree": false, "possessionAgentId": "agentId_2" }, "players": [ ... ], "teamChat": [] }, "teamId": 0, "myPlayers": [2] }
```

`playMode` is a string. Common values: `"KICK_OFF"` , `"OPEN_PLAY"` , `"FREE_KICK"` .
`myPlayers` contains the position index (0–4) of the single agent being invoked in this call. Each agent is invoked independently per tick.
`teamChat` is an array that carries the latest coach instructions sent from the Player Portal — read it in your agent to react to real-time coaching.
Each entry in `players` :
| Field | Type | Description |
| agentId | string | e.g. "agentId_0" — index 0 is always the GK |
| teamCode | string | "home" or "away" |
| position | {x, y} | Position on the pitch |
| velocity | {x, y} | Current movement vector |
| orientation | float | Direction the player is facing (degrees) |
| stamina | float | Current stamina level (0–100) |
| speed | float | Current movement speed |
| isSprinting | bool | Whether the player is currently sprinting |
| currentAction | string | Active action state (e.g. "IDLE") |
| lastAction | string | Last command type executed |

Click Next to learn about game rules and physics.
