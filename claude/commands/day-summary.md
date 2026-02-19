# /day-summary - Daily Session Summary

Generate a summary of all Claude Code sessions for a given day across all projects.

---

## Usage

```
/day-summary                    # Today's sessions
/day-summary yesterday          # Yesterday's sessions
/day-summary 2026-01-20         # Specific date
/day-summary --save             # Today + save to vault
/day-summary 2026-01-20 --save  # Specific date + save to vault
```

---

## Instructions

### 1. Parse Arguments

Determine the target date from the argument:
- No argument or `today` → `$(date +%Y-%m-%d)`
- `yesterday` → `$(date -v-1d +%Y-%m-%d)`
- `YYYY-MM-DD` format → Use directly

Check for `--save` flag to save to Obsidian vault.

### 2. Run Summary Script

Execute the summary script:
```bash
~/clawd/scripts/daily-session-summary.sh <DATE>
```

### 3. Present Output

Display the markdown output to the user showing:
- Time range (start → end) for each session
- Session summary
- Project name
- Total sessions and messages

### 4. Save to Vault (if --save)

If `--save` flag is present, create a work log in the vault:

**Path:** `vault/Personal_Assistant/Work_Logs/<DATE>-sessions.md`

**Format:**
```markdown
---
type: work-log
source: claude-code-sessions
date: <DATE>
total_sessions: <N>
total_messages: <N>
created: <NOW>
---

# Work Log — <DATE>

<SESSION LIST FROM SCRIPT OUTPUT>
```

### 5. Offer Follow-ups

After displaying, offer:
- "Would you like me to save this to your vault?"
- "Want details on any specific session?"
- "Compare with another day?"

---

## Example Output

```markdown
# Claude Code Sessions — 2026-01-22

- **09:23 → 13:23** (4h0m) | Email digest and calendar sync setup
  - `clawd` · 19 msgs
- **13:20 → 13:34** (13m) | Agentic Engineering Index with Article Synthesis
  - `clawd` · 18 msgs
- **14:40 → 14:46** (6m) | NHS Manchester TRE governance & synthetic data blocker
  - `clawd` · 11 msgs

---
**Total:** 17 sessions, 229 messages
```

---

## Notes

- Sessions are sorted chronologically by start time
- Times are in UTC (from Claude Code's session storage)
- A session appears if it was created OR modified on the target date
- Script location: `~/clawd/scripts/daily-session-summary.sh`
