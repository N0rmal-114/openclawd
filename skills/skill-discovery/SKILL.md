---
name: skill-discovery
description: Find, evaluate, and install external skills from GitHub or the web. USE ONLY WITH USER APPROVAL.
---

# Skill Discovery

This skill allows the agent to find useful skills from the community, evaluate their safety, and propose them for installation.

## Trigger

- User asks to "find a skill" to do X.
- Agent realizes it lacks a capability that might exist as a skill (e.g., "I don't know how to handle `.pcap` files, maybe there's a skill for that?").

## Workflow

### 1. Search

**Action**: Use `search_web` to find relevant skills.
**Query Patterns**:

- `github "clawdbot-skill" <keyword>`
- `github "agent-skill" <keyword>`
- `site:github.com "SKILL.md" <keyword>`

### 2. Evaluate (READ-ONLY)

**Action**: READ the skill's documentation and code. DO NOT INSTALL YET.
**Steps**:

1.  Read the `SKILL.md` or `README.md` of the candidate repository.
2.  **Safety Check**:
    - Does it contain obfuscated code?
    - Does it download binaries (curl/wget)?
    - Does it send data to external servers?
    - Does it require `sudo`?
3.  **Relevance**: Is this actually what is needed?

### 3. Propose

**Action**: Present the findings to the user and ASK FOR PERMISSION.
**Use Tool**: `notify_user`
**Message Format**:

```
I found a skill that might help:
- **Name**: [Skill Name]
- **Source**: [URL]
- **Description**: [Brief summary]
- **Risks**: [None | Low | High - explain why]

Do you want me to install this skill?
```

### 4. Install (ONLY AFTER APPROVAL)

**Action**: Install the skill into the `skills/` directory.
**Steps**:

1.  Navigate to `d:\MyProjects\Moltbot\clawdbot\skills`.
2.  Clone the repository: `git clone [URL] [skill-name]`.
3.  (Optional) Remove `.git` folder to keep it clean: `rm -rf [skill-name]/.git`.
4.  Verify the installation by listing the directory.

> [!CRITICAL]
> NEVER install a skill without explicit confirmation from the user in the current session.
