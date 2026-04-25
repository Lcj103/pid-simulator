# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Single-file PID controller web simulator (index.html). Zero dependencies — pure HTML/CSS/JS with Canvas 2D rendering. No build step, no package manager, no tests.

## Architecture

- **`index.html`** — Entire application in one file. Contains:
  - Inline CSS (~80 lines): dark theme with grid-style parameter controls
  - `PID` class: standard PID controller with Kp/Ki/Kd, anti-windup integrator clamping, output limiting
  - Physics loop: Euler integration with velocity damping, static friction dead zone, boundary bounce
  - Rendering: `requestAnimationFrame` driven main loop, draws track, ball (velocity-colored gradient), force arrows, target marker
  - Plot canvas: scrolling 15-second position-vs-time chart
  - UI: single/cascade mode toggle, slider controls for all PID params, mouse drag interaction on ball/target

## Key Technical Details

- Physics is 1D (x-axis only), no gravity, track range is \[-5, +5\] meters
- Simulation uses `requestAnimationFrame` timestamps, actual dt is multiplied by speed slider (0.1x-5x)
- Cascade mode: outer PID outputs velocity setpoint (clamped to ±20), inner PID outputs force
- Two control modes selected via button toggle:
  - **Single PID**: position error → force directly
  - **Cascade PID**: outer (position→velocity setpoint) → inner (velocity→force)

## Running

Open index.html in any browser — no server needed:

```
start index.html
```
