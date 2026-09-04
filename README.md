# Lift Tracker

A single-file, installable PWA for a 3-day full-body resistance program (Mon / Wed / Fri).
No build step, no dependencies, no backend — everything lives in `index.html` and the
browser's local storage.

## The program

Two hard sets per movement, six movements per day, ~60 minutes, 90 sec rest between sets.

| Day | Theme | Movements |
| --- | --- | --- |
| 1 (Mon) | Squat + Horizontal | Zercher squat · DB bench (neutral) · chest-supported DB row · goblet lateral lunge · half-kneeling landmine press · half-kneeling cable chop |
| 2 (Wed) | Hinge + Vertical | Hip thrust machine · neutral-grip pulldown · seated DB neutral press · Bulgarian split squat · 1-arm cable row · Pallof press |
| 3 (Fri) | Unilateral + Rotation | Kickstand RDL · DB reverse lunge · 1-arm DB floor press · KB bottoms-up press · pronated pull-up · cable rotational row |

Every major pattern is covered across the week — squat, hinge, horizontal push/pull,
vertical push/pull — and every day includes frontal- and transverse-plane work rather than
living in the sagittal plane.

Constraints baked in: no barbell back squat, no front squat (Zercher instead), and no
barbell strict press — overhead work is landmine, neutral-grip dumbbell, and bottoms-up
kettlebell only.

Golfer's elbow rules out supinated grips, so vertical pulling is pronated (pull-up) or
neutral (lat pulldown) only — no chin-ups.

## Progression rule

The rule is applied to **every set individually**:

- **6 reps or fewer** → drop one increment
- **7–9 reps** → repeat the load
- **10+ reps** → add one increment

Set 2's load is computed live from set 1's result. The next session's set 1 opens at set 2's
load, adjusted by set 2's reps. Increments: barbell 5 lb total (2.5/side), dumbbells 5 lb per hand, cable stacks 5 lb, and
the plate-loaded hip thrust machine 10 lb (5/side).

On unilateral movements the **weaker side governs** — log both sides, the lower rep count
drives the load, and the strong side stops at the weak side's reps.

## Tabs

- **Today** — day picker, warm-up block, the six move cards with live set-2 math, rest timer (auto-starts at 90 sec when you commit a set's last rep count, chimes when it runs out), log button
- **History** — every logged session, expandable, deletable
- **Program** — the full three-day plan plus the weekly pattern/plane coverage table
- **Settings** — starting loads for each movement, JSON export/import, erase sessions

The screen is held awake (Screen Wake Lock API) the whole time the app is in the
foreground, so the rest timer and its chime survive a long set. The lock is released
automatically when you switch away, and re-taken when you come back.

## Files

```
index.html            entire app (HTML + CSS + vanilla JS IIFE)
sw.js                 service worker; bump CACHE to force installed devices to update
manifest.webmanifest  PWA manifest
icon-192.png icon-512.png apple-touch-icon.png
```

## Updating

Edit files → bump the `CACHE` string in `sw.js` (increment the **minor**, never the major:
`lift-v1.0` → `lift-v1.1`) → commit → push. If served from GitHub Pages, redeploy takes
1–2 minutes; reopen the installed app to pull the new cache.
