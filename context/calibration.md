# Estimation Calibration Data

This file persists across weeks and is the source of truth for estimation accuracy.
Updated by the estimate agent and weekly-plan end-of-week reviews.

## Current Multipliers

These started as defaults and are adjusted based on actual data. The estimate agent
MUST read this file and use these values instead of the defaults when enough data exists.

| Category | Default | Calibrated | Samples | Confidence |
|----------|---------|------------|---------|------------|
| Familiar code, clear requirements | 1.5x | — | 0 | low |
| Familiar code, unclear requirements | 1.75x | — | 0 | low |
| Unfamiliar code, clear requirements | 2.0x | — | 0 | low |
| Unfamiliar code, unclear requirements | 2.5x | — | 0 | low |
| System never touched | 3.0x | — | 0 | low |

**Confidence levels:**
- `low`: < 5 samples — use default multiplier
- `medium`: 5-15 samples — use calibrated multiplier but keep default as floor
- `high`: 15+ samples — trust the calibrated multiplier

## Overall Stats

- Total tasks tracked: 0
- Average estimation ratio (actual/estimated): —
- Median estimation ratio: —
- Worst miss: —
- Best accuracy: —

## Energy/Pace Factor

Some weeks are slower due to mental load, personal factors, or just being human.
Track weekly pace factor to account for this.

| Week | Planned (h) | Actual (h) | Pace Factor | Notes |
|------|-------------|------------|-------------|-------|
| (filled in weekly) | | | | |

**Running average pace factor**: —
(A pace factor of 0.8 means tasks take 25% longer than the calibrated estimate.
The estimate agent should multiply by 1/pace_factor when pace is consistently low.)

## Raw Task Data (last 50 tasks)

| Date | Task | Category | Estimated (h) | Actual (h) | Ratio | Notes |
|------|------|----------|---------------|------------|-------|-------|
| | | | | | | |

## How to Update This File

1. When a task is completed and actual hours are known, add a row to Raw Task Data.
2. Every Friday (end-of-week review), recalculate:
   - Category averages from the raw data
   - Update calibrated multipliers if enough samples exist
   - Update overall stats
   - Add the week's pace factor
3. The estimate agent reads this file at the start of every estimation to use
   calibrated multipliers instead of defaults.
