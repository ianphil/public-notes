# Bootstrap — Heartbeat

Sets up the recurring heartbeat that runs Moneypenny for mind-only ambient scanning — surfacing stale items, cross-initiative patterns, timing conflicts, and executing queued maintenance tasks. No external APIs (no WorkIQ, no ADO writes).

## What It Does

1. **Phase 1 — Scan:** Reads all next-actions, memory files, initiative notes, and people notes. Writes findings to `.working-memory/heartbeat.md`
2. **Phase 2 — Tasks:** Reads `.working-memory/heartbeat-tasks.md`, executes queued items (mind operations + ADO reads only), marks them done

The heartbeat primes the morning briefing — its findings get incorporated into the daily report.

## Prerequisites

- **Copilot CLI** installed and authenticated (`copilot` on PATH)
- **pwsh** (PowerShell 7+)
- Repo cloned to a known path (default: `C:\src\miss-moneypenny`)
- **No WorkIQ or ADO CLI required** — this is a mind-only scan (though ADO read queries are allowed)

## Setup — Windows Task Scheduler

### Create the Task

```powershell
# Create 5 hourly triggers (11 AM – 3 PM ET, weekdays)
$triggers = @()
foreach ($hour in 11..15) {
    $triggers += New-ScheduledTaskTrigger `
        -Weekly -DaysOfWeek Monday,Tuesday,Wednesday,Thursday,Friday `
        -At "${hour}:00"
}

$action = New-ScheduledTaskAction `
    -Execute "pwsh.exe" `
    -Argument '-NoProfile -ExecutionPolicy Bypass -File "C:\src\miss-moneypenny\.github\scripts\heartbeat.ps1"' `
    -WorkingDirectory "C:\src\miss-moneypenny"

$settings = New-ScheduledTaskSettingsSet `
    -AllowStartIfOnBatteries `
    -DontStopIfGoingOnBatteries `
    -StartWhenAvailable

Register-ScheduledTask `
    -TaskName "MoneypennyHeartbeat" `
    -Action $action `
    -Trigger $triggers `
    -Settings $settings `
    -Description "Moneypenny heartbeat — mind scan + task queue"
```

### Schedule

- **When:** 11:00 AM, 12:00 PM, 1:00 PM, 2:00 PM, 3:00 PM ET — weekdays
- **Frequency:** 5 runs per workday, hourly during core hours
- **RunAs:** Current user
- **DaysOfWeek value:** 62 (Mon–Fri)

## Setup — Linux (cron)

```bash
crontab -e

# Hourly 11 AM–3 PM ET (16:00–20:00 UTC during EST, 15:00–19:00 UTC during EDT)
0 16-20 * * 1-5 cd /home/$USER/src/miss-moneypenny && pwsh -NoProfile -ExecutionPolicy Bypass -File .github/scripts/heartbeat.ps1 >> /tmp/moneypenny-heartbeat.log 2>&1
```

**Note:** The heartbeat is lightweight (mind-only) and works on any machine with the repo and Copilot CLI. Good candidate for running on the Linux machine too.

## Heartbeat Tasks

The heartbeat checks `.working-memory/heartbeat-tasks.md` each run for queued work.

### Standing Tasks (automatic, with cooldowns)

| Task | Trigger | Cooldown |
|------|---------|----------|
| Mind-index refresh | >5 new/moved/archived files | 7 days |
| Memory consolidation | log.md >150 lines or >14 days | 14 days |
| Stale item scan | Always | 7 days |
| 1:1 prep | Calendar has direct report meeting | Daily |

### Queue (one-shot)

Either Ian or Moneypenny can add items to the queue. The heartbeat picks 1-2 per run, prioritized by age and urgency. Format:

```markdown
- [ ] Description of task — enough detail to execute without context
```

### Scope Rules

- ✅ Mind operations: reorganize notes, archive, fix links, update mind-index, memory maintenance
- ✅ ADO read-only: query work items, check for stale/aging items
- ✅ GitHub read + close issues (e.g., importing misplaced issues to inbox)
- ❌ No ADO writes, no emails, no Teams messages, no git push

## Verification

After setup, confirm:

1. `Get-ScheduledTask -TaskName "MoneypennyHeartbeat"` shows **Ready**
2. All 5 triggers listed with correct times and days
3. Working directory and script path are correct
4. Run manually: `pwsh -NoProfile -ExecutionPolicy Bypass -File .github/scripts/heartbeat.ps1`
5. Check `.working-memory/heartbeat.md` exists with today's scan
6. Check `.working-memory/briefings/run-log.md` for HEARTBEAT SUCCESS entry

## Troubleshooting

| Symptom | Likely Cause |
|---------|--------------|
| No heartbeat.md generated | Copilot CLI not on PATH or not authenticated |
| Heartbeat writes to wrong directory | Script has stale path references — grep for `.ainotes` |
| Standing tasks never fire | `heartbeat-tasks.md` Last Run dates are too recent (within cooldown) |
| Queue items not executing | Items may be out of scope — check for skip notes in the Done section |
| Run log shows HEARTBEAT ERROR | Check `YYYY-MM-DD-heartbeat-error.log` in briefings directory |

## Key Files

- Script: `.github/scripts/heartbeat.ps1`
- Output: `.working-memory/heartbeat.md`
- Task queue: `.working-memory/heartbeat-tasks.md`
- Run log: `.working-memory/briefings/run-log.md` (shared with morning briefing)
