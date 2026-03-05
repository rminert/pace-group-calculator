# Rep Calculator · Tuesday Night Workouts

A single-page tool for running coaches to build pace-based interval workouts where every group finishes at the same time.

Built for Tuesday night track sessions where runners are split by pace rather than experience level. No install, no dependencies — just open `index.html` in any browser.

---

## Features

### ⚡ Rep Calculator

Set up a workout and get rep counts for every pace group in seconds.

- **Anchor-based scaling** — set the rep count for your fastest group, and all other groups are automatically calculated to match its finish time
- **Pace group management** — define groups by pace range; editing a group's slowest pace auto-updates the next group's fastest so ranges always abut cleanly
- **Rep overrides** — toggle any group to Manual to try a specific rep count and instantly see the time delta vs. the anchor
- **Recovery by time or distance** — set a fixed recovery interval (MM:SS) or a distance with a configurable recovery pace offset (default: interval pace + 2:00/mi, adjustable in 30-second increments)
- **Cycle time breakdown** — each result card shows rep time + recovery time = cycle time, so coaches can communicate the rhythm clearly
- **Printable coaching sheet**

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
3. Share the hosted version with other coaches at: `https://rminert.github.io/pace-group-calculator/rep-calculator.html`

---

## How the math works

**Rep Calculator:** Given an anchor group's total workout time (reps × rep time + (reps − 1) × recovery time), each other group's rep count is solved as:

```
reps = floor((anchorTotalTime + recoveryTime) / (repTime + recoveryTime))
```

**Pace Window Optimizer:** Given a time budget and a target rep count, the maximum pace is solved as:

```
// Fixed recovery:
maxPace = (budget − (reps − 1) × recTime) / (reps × repDistMiles)

// Distance-based recovery:
maxPace = (budget − (reps − 1) × offset × recDistMiles) / (reps × repDistMiles + (reps − 1) × recDistMiles)
```
