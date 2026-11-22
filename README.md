# Setup Audit for Claude

A free, guided audit you run inside your own Claude: it reviews how your company has Claude set up, fixes what it can with you step by step, and records progress on a private page.

It is written for the senior person who answers for how the company uses Claude: an executive or the owner of the business, usually with owner access. You do not need to be technical. Claude asks one question at a time, does the work with you, and leaves you with files you keep. If you lack access for a step, Claude marks it blocked and writes a note for the colleague who has it.

The audit is honest about difficulty. Every finding is marked easy, medium or hard. The easy ones you fix with Claude during the audit. For the hard ones, which need someone technical, it writes down exactly what is involved. It is a structured review, not a security certification.

Published by ATI Lab. Not affiliated with or endorsed by Anthropic.

## The skills in this plugin

The plugin holds seven skills. Six work on their own. The seventh, `setup-audit`, runs them in order as one audit.

| Skill | What it does | What you end up with | Time |
| --- | --- | --- | --- |
| `setup-check` | A quick check of what loads in a session, what is in the workspace and how the team is getting on | A list of findings, each marked easy, medium or hard, and the order to fix them in | 10 min |
| `workspace-foundations` | Company context, project tidy-up, usage rules, onboarding | A company context file, tidy projects, one page of usage rules and a way to bring people on | 45 min |
| `sop-to-skill` | Builds a skill from a senior person's own method and sets up who looks after skills | One working skill, an owner for it and a ranked list of the next ones | 50 min |
| `connector-review` | Reviews what connectors can read and change, and which return more than is used | A table of access, unused access closed, and the heaviest connectors named | 40 min |
| `process-finder` | Finds recurring work that should run without a person starting it | The first process to automate, written as a spec someone can build from | 35 min |
| `brand-voice` | Optional. Brand voice and content written from your experts' real work | A brand voice file and a first piece | 35 min |
| `setup-audit` | The whole audit: the quick check first, then four modules in the order your findings suggest. Also holds the plan-and-seats and right-tool modules | All of the above that apply, plus a plan recommendation or a tool decision | Several sittings |

## How to use it

### One skill on its own

Ask for the job in your own words. Claude loads the matching skill. For example:

- "Check how our Claude is set up." (`setup-check`)
- "Write a company context file for our projects." (`workspace-foundations`)
- "Turn our month-end reporting procedure into a skill." (`sop-to-skill`)
- "Review our connectors and what they can change." (`connector-review`)
- "We keep hitting usage limits. Which work should run on its own?" (`process-finder`)
- "Write our brand voice file." (`brand-voice`)

### The whole audit

Ask: "Run the setup audit." Claude starts with the ten-minute check, shows you the findings, agrees the order with you and then works through the modules. You can stop after any step and continue later.

### Installing

**In the Claude app or Cowork.** Add the plugin from the plugins page (**Customize > Plugins**, named **Plugins** in the newer layout). To record progress on a private page, connect the bundled connector from the plugin's **Connectors** tab. This is optional.

**In Claude Code.** From the folder that contains this one:

```bash
claude --plugin-dir ./atilab-setup-audit
```

Then run `/atilab-setup-audit:setup-audit`, or one skill such as `/atilab-setup-audit:setup-check`, or ask in plain words.

**One skill without the plugin.** Each of the six standalone skills is a self-contained folder under `skills/`. Zip one folder with the folder itself at the top level and upload it as a skill. `setup-audit` is not self-contained: it reads the other skills' files, so it needs the whole plugin.

## What is in this folder

```text
.claude-plugin/plugin.json                 the plugin manifest
.mcp.json                                  the optional progress connector
skills/setup-audit/SKILL.md                how Claude runs the whole audit
skills/setup-audit/references/             the course index, and the plan and fit steps
skills/<skill>/SKILL.md                    one per standalone skill
skills/<skill>/references/<module>.md      that skill's steps, with templates
```

The plugin is Markdown and JSON only. It contains no scripts, hooks or executables. All steps are in the skills' files; Claude does not download instructions at run time. Some steps tell Claude to open Anthropic's public help pages, or a vendor's public pricing page, to check a current menu name or figure, or to ask you to read it out.

## What is stored

Without the connector, nothing leaves your conversation. Claude keeps the list of finished steps in the chat. This is always the case when you use one skill on its own.

With the connector, and only after you agree to record progress in the whole audit, the connector saves the following for each audit run:

- a random run id, the starting question you chose, and the times the run was created and last updated;
- for each finished step: its id, its status (`done`, `skipped` or `blocked`) and a summary of at most 400 characters.

Claude shows you every summary before it is sent. Summaries say what was found, decided or built in one or two sentences. They must not contain names, client details, credentials, text from your documents or anything a connector returned, and the service strips email addresses from them. The run record holds no name, email address or account. The connector's server also keeps ordinary request logs, as described in the privacy policy. Anyone who has the link to the progress page can see it, so treat the link as private. Runs are deleted 90 days after their last update.

The files you make during the audit (the context file, skills, rules, plans, specs) stay with you. They are never sent to the connector.

The plugin does not read your Claude memory, past chats or unrelated files. In the quick check and the connector review, Claude looks at the list of connectors, tools and skills loaded in the current session. In the connector review it runs a test request against one of your services only if you ask it to, and it records how much came back, never the data.

Privacy policy: https://www.atilab.io/privacy

## Troubleshooting

- **Claude does not start.** Name the skill: "Run the setup audit", or "Run the setup check". In Claude Code, use `/atilab-setup-audit:setup-audit`.
- **No progress page.** The connector is not connected, you declined recording, or you are using one skill on its own. The work is the same; progress stays in the chat.
- **A step is marked blocked.** Claude could not finish it with you, usually because a setting needs an owner, or because the work needs someone technical. The step says what is needed and what kind of person can do it.
- **Menu names differ from the steps.** Claude's apps change. Each module names the official help page to follow instead.

## Who makes this

ATI Lab (atilab.io) builds and runs AI systems for established businesses, including Claude deployments, and is a member of the Claude Partner Network. The audit's findings and difficulty ratings come from that work. It is an independent tool: not affiliated with or endorsed by Anthropic.

## Support

Questions and problems: open an issue at https://github.com/ATI-Lab-Repositories/atilab-setup-audit/issues.

## Licence

To be confirmed before publication. Until a licence file is added, all rights are reserved.
