# Fleet Feet Training Class · Workout Calculator

A single-page tool for running coaches to build pace-based interval workouts where every group finishes at the same time.

Built for Fleet Feet training class sessions where runners are split by pace group. No install, no dependencies — just open `rep-calculator.html` in any browser.

---

## Features

### ⚡ Rep Calculator

Set up a single-set workout and get rep counts for every pace group in seconds.

- **Anchor-based scaling** — set the rep count for your fastest group, and all other groups are automatically calculated to match its finish time
- **Pace group management** — define groups by pace range; editing a group's slowest pace auto-updates the next group's fastest so ranges always abut cleanly
- **Rep overrides** — toggle any group to Manual to try a specific rep count and instantly see the time delta vs. the anchor
- **Recovery by time or distance** — set a fixed recovery interval (MM:SS) or a distance with a configurable recovery pace offset (default: interval pace + 2:00/mi, adjustable in 30-second increments)
- **Cycle time breakdown** — each result card shows rep time + recovery time = cycle time, so coaches can communicate the rhythm clearly
- **Printable coaching sheet**

### 🪜 Multi-Set Builder

Build ladder, pyramid, or any multi-stage workout with up to 6 sets.

- Each set has its own rep distance, recovery (time or distance), and anchor rep count
- Anchor rep counts are auto-suggested based on distance and can be overridden per set
- Pace groups are shared across all sets; the first group is the anchor for each set
- Non-anchor groups are capped at the anchor's rep count per set
- **Greedy fill algorithm** — after initial calculation, the tool automatically bumps slower groups' reps across sets to bring each group's total workout time within 90 seconds of the anchor's total; adjusted counts are marked with a + indicator in the per-set tables
- Results show one table per set (groups as rows) plus a grand total summary; groups outside the 90-second window are flagged if the gap can't be closed further
- Recovery after the final rep of each set is included in all time calculations

### 🎯 Pace Window Optimizer

The inverse of the calculator — useful when you know your anchor group's workout and want to figure out what pace ranges map to other rep counts.

- Enter anchor pace, rep count, and distance
- Generates a table showing the maximum average pace that fits each rep count within the same time budget
- Columns: Max Avg Pace, Suggested Range, Rep Time, Cycle Time, Total Rep Time, Total Time
- Supports the same time/distance recovery options as the calculator

---

## Usage

1. Download `rep-calculator.html`
2. Open it in any browser — no server required
3. Share the hosted version with other coaches at: `https://rminert.github.io/rep-calculator/rep-calculator.html`

---

## How the math works

All time calculations include recovery after every rep, including the last:

```
setTime = reps × repTime + reps × recTime
        = reps × (repTime + recTime)
```

**Rep Calculator:** Each group's rep count is solved as:

```
reps = floor(anchorTotalTime / (repTime + recTime))
```

Capped at the anchor's rep count so no group ever does more reps than the anchor.

**Multi-Set Builder:** Initial reps per set are calculated the same way. A greedy pass then adds reps one at a time to the set with the lowest cycle cost until each group's grand total is within 90 seconds of the anchor's grand total, subject to the per-set anchor cap.

**Pace Window Optimizer:** Given a time budget and a target rep count, the maximum pace is solved as:

```
// Fixed recovery:
maxPace = (budget / reps − recTime) / repDistMiles

// Distance-based recovery:
maxPace = (budget / reps − offset × recDistMiles) / (repDistMiles + recDistMiles)
```
