# `/viva` Agent Skill

An Agent Skills-format skill for conducting an interactive viva from study notes in a PDF. It reads the notes first, asks one question at a time, evaluates each response out of 5, tracks progress, and produces a revision report with grounded page references where available.

## Installation

For this VS Code workspace, keep the complete `viva` folder at:

```text
.github/skills/viva/
```

To install it in other workspaces as a personal Copilot skill, copy the folder to:

```text
%USERPROFILE%\.copilot\skills\viva\
```

The folder must contain `SKILL.md`; keep its directory name consistent with the frontmatter `name`. Start a fresh VS Code chat using a harness that supports Agent Skills. If the skill does not appear in the `/` menu, verify the path and refresh/reopen the chat.

## Activation and use

Enter this command in the chat input:

```text
/viva thermo-notes.pdf
```

Optionally specify the number of questions:

```text
/viva "C:\Study\thermo-notes.pdf" questions=8
```

Without a count, the skill asks how many questions to ask and defaults to 5. Respond to each question before the next one; `hint`, `skip`, `explain`, and `stop` are supported during the viva.

## Verification status

The skill structure and instructions are documented in the test reports at [`test-reports/`](test-reports/). PDF-based viva runs and fresh-chat activation have not been performed in this workspace because no test PDFs or separate fresh-chat runtime were supplied. The reports distinguish these unrun checks from validated format checks.
