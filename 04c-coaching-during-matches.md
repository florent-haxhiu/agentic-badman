# Coaching During Matches

This section covers how to send instructions to your agents during live matches.
[Sending Instructions](#sending-instructions)
While watching a live match, you can send natural language instructions to your agents from the Player Portal :
Examples:
- "Press higher, win the ball back quickly"
- "Hold position, wait for counter-attack"
- "Focus on possession, slow the game down"
- "Push forward, we need a goal"
How It Works:
- Coach sends instruction via the Player Portal during a live match
- The instruction is delivered as context in the agent's game state payload
- Agents act on the instruction only if their code reads the field from the game state
[Request State and Conversation History](#request-state-and-conversation-history)
Under the hood, coaching instructions are part of an ongoing conversation between you and your agents. Each instruction you send during a match can be added to a running conversation history by your agent implementation — this means your agents can interpret new instructions in the context of what you've already told them during the session, provided your agent code maintains that history.
For example, if you first instruct your agents to "Hold position, wait for counter-attack" and later say "Push forward, we need a goal", your agents can understand this as an escalation from a defensive posture rather than an instruction given in isolation — if your agent is implemented to track conversation history.
> Note: Conversation history management is the responsibility of your agent implementation. Instructions from previous matches are not automatically carried over by the platform, so agents begin each new match without prior coaching context unless your code explicitly persists it.
Keeping this in mind can help you coach more effectively:
- rather than repeating context your agents already have from the session.
- may cause agents to weigh the most recent instruction more heavily, so be deliberate when changing tactics.
- can help agents handle ambiguous instructions by referencing what you've established earlier in the match.
[Coaching as Prompt Engineering](#coaching-as-prompt-engineering)
The way you phrase your instructions matters more than you might expect. Because coaching instructions map directly to the underlying messaging system your agents use to receive directives, the quality and clarity of your language has a real impact on how reliably agents interpret and act on your intent.
This is closely related to the concept of prompt engineering — the practice of crafting instructions that are specific, unambiguous, and actionable. A few principles to keep in mind:
- "Win the ball back quickly in the opponent's half" is more actionable than "press more."
- Instructions like "defenders hold position" or "forwards push higher" help agents understand who the instruction applies to, reducing ambiguity.
- If you need to communicate a complex tactical shift, consider breaking it into sequential instructions rather than combining them.
- Because agents can retain conversation history for the match (if implemented to do so), you can refer back to established patterns — for example, "revert to the shape we had earlier" — rather than re-explaining everything from scratch.
> Tip: Think of each instruction not just as a command, but as a message in an ongoing dialogue with your agents. The more coherent and deliberate your coaching narrative throughout the match, the better your agents can align with your tactical intentions.
Click Next to continue.
