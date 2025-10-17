# Snake — Minimal Web Game

## Summary
This repository contains a minimal, fully-functional Snake game implemented in a single HTML file (index.html) with embedded CSS and JavaScript. It is designed to be small, fast, and easy to deploy (including GitHub Pages), while remaining clean and modern in appearance.

Highlights:
- Playable immediately with keyboard controls (arrows or WASD).
- Start, Pause/Resume, Reset.
- Score and persistent High Score (localStorage).
- Responsive, high-DPI aware canvas rendering.
- Optional URL ping via query parameter (?url=...) as described below.
- No external dependencies.

## Setup
No build step is required.

- Local: Open index.html in any modern browser.
- GitHub Pages: Commit and push this repository; set the Pages source to the main branch (or docs folder if you move files). The app works immediately when served over HTTPS.

Files:
- index.html — All HTML/CSS/JS is embedded and production-ready.
- README.md — This file.

## Usage
Controls:
- Move: Arrow keys or W/A/S/D
- Pause/Resume: Space
- Reset: R
- Buttons: Start/Pause and Reset buttons in the header

Gameplay:
- Eat the glowing food to grow and increase your score.
- Hitting a wall or your own body ends the game.
- The highest score achieved is saved to your browser (localStorage).

Status/Overlays:
- The state badge shows Ready, Playing, Paused, or Game Over.
- An overlay appears when paused or after game over, with quick instructions.

Query Parameter (?url=...):
- If you open the game with a URL parameter named url (e.g., https://yourdomain/index.html?url=https://example.com/ping), the app will attempt a GET request to that URL once on load.
- Behavior:
  - First, a CORS request is attempted (mode: cors); if successful, you’ll see “Ping OK” or a status code.
  - If that fails due to CORS, a fallback request is sent with mode: no-cors. This still reaches the server, but the response is opaque. The UI will show “Ping sent (no-cors).”
  - If both attempts fail, you’ll see “Ping failed.”
- A small status indicator appears in the footer when ?url is provided. This is purely informational and does not affect the game.

Notes:
- The ?url ping is best-effort and designed to be safe; invalid URLs are ignored with an error indicator.
- The game does not load external code or depend on remote assets.

## Code Explanation
Everything lives in index.html for simplicity:

- HTML structure:
  - Header with title, live-updating score and high score, and control buttons.
  - Centered canvas inside a container with an overlay for pause/game-over messaging.
  - Footer showing controls and the optional ?url ping status.

- CSS:
  - A small set of design tokens (CSS variables) for colors and effects.
  - Responsive canvas with a subtle grid background, rounded corners, and focus styles.
  - Minimal yet modern UI elements for readability and accessibility.

- JavaScript:
  - Canvas/HiDPI: The canvas is scaled according to devicePixelRatio for crisp rendering.
  - Game grid: 24×24 cells; tile size is inferred from canvas size.
  - State: Snake body array, current/next direction, food position, score, high score, and flags (running/ended).
  - Loop: Uses requestAnimationFrame with a fixed timestep (accumulator) for consistent movement speed.
  - Input: Arrow keys or WASD to steer; Space to pause/resume; R to reset. Immediate start on first directional input is supported.
  - Collision: Game over on wall hit or self-intersection. Food is placed on a random empty cell.
  - Rendering: Light grid lines, a gradient food pellet, and rounded snake segments with a highlighted head.
  - Persistence: High score saved to localStorage under key snakeHighScore:v1.
  - URL param handler: On load, parses ?url and attempts a GET request. It first tries CORS (to read status), then falls back to no-cors (opaque but still performs the request). UI reflects success/warning/error states, but the game runs regardless.

Extensibility tips (not implemented to keep scope tight):
- Add wrap-around walls, difficulty options, or touch controls.
- Audio cues on eat/game-over (user-gesture gated).
- Settings persistence for speed or grid size.

## License
MIT License

Copyright (c) 2025

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the “Software”), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED “AS IS”, WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.