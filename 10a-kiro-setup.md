# Kiro Setup

Optional but recommended
Already have Kiro installed and signed in? Skip to Step 3.
[1. Don't have Kiro yet? Install it now — it's free.](#1.-don't-have-kiro-yet-install-it-now-it's-free.)
Please follow the instructions on [Kiro main page](https://kiro.dev/) to download and install Kiro locally.
[2. Sign in to Kiro](#2.-sign-in-to-kiro)
Open Kiro and click Sign in . You'll see four options:
| Option | Best for |
| Google | Fastest if you already have a Google account |
| GitHub | Fastest if you already have a GitHub account |
| Builder ID | Free AWS account — best for new users with no existing account above |
| Your Organization | Skip this — it's not needed for this workshop |

New to Kiro and don't have Google/GitHub?
Select
Builder ID
— it's free and takes 30 seconds to create at
[profile.aws.amazon.com](https://profile.aws.amazon.com/)
. No credit card required.
Once signed in via any of the first three options, move to Step 3.
[3. Connect to Your Workshop AWS Account](#3.-connect-to-your-workshop-aws-account)
Signing in to Kiro gives you the IDE. To deploy agents and call Amazon Bedrock, you need to connect Kiro to your workshop AWS account.
1. In Kiro, open the terminal: → (or / )
2. Go to your and click
1. Click the copy icon and paste the commands into Kiro's terminal:

```
1 2 3 4 export AWS_DEFAULT_REGION=us-east-1 export AWS_ACCESS_KEY_ID=... export AWS_SECRET_ACCESS_KEY=... export AWS_SESSION_TOKEN=...
```

1. Verify the connection:

```
1 aws sts get-caller-identity
```

You should see your workshop account ID in the response. You're now ready to deploy agents directly from Kiro.
Workshop credentials expire periodically. If you get an "expired token" error later, go back to your Workshop Studio event page, click
Get AWS CLI credentials
again, and paste the new exports into Kiro's terminal.
You're set up.
Kiro is connected to your workshop AWS account. Proceed to Phase 1 to start building your team.
