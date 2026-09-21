# AWS CloudShell Setup

Using Kiro or another agentic coding tool?
Skip this page — CloudShell is only for participants who can't install software on their machine.
[When to Use CloudShell](#when-to-use-cloudshell)
Use AWS CloudShell only if:
- You can't install Kiro (or any IDE) on your machine
- You're on a locked-down corporate laptop
- You prefer a browser-only experience
For everyone else, use Kiro — it's faster, has a file editor, and gives you agentic coding assistance throughout the workshop.
[How to Open CloudShell](#how-to-open-cloudshell)
1. Log in to the with your workshop account
2. Make sure you're in (check the region selector top-right)
3. Click the (terminal icon) in the top navigation bar
4. Wait for the shell to initialize — Python 3, pip, git, and AWS CLI are pre-installed
5. Your AWS credentials are already configured — no commands needed
[Limitations](#limitations)
| Limitation | Impact | Workaround |
| 1 GB storage | Can run out of space with dependencies | Use pip install --no-cache-dir, clean up _deploy/ after each deployment |
| No graphical editor | Editing system prompts is slower | Use nano or vi for file edits |
| Session timeout (20-30 min idle) | Disconnects if inactive | Re-run setup commands; deployed agents on AgentCore are unaffected |

CloudShell works, but the iteration loop is significantly slower than working in Kiro. If you have any way to install Kiro locally, do that instead.
