# Maths exams

Based on oscarneiva's Exams Hall.

A minimalistic web-based timer for IB, IGCSE, Maths Olympiads, and custom exams. Single-page HTML/CSS/JS application with no dependencies.

## Features

- **Multiple Exam Boards & Presets**: 
  - **IB**: Higher/Standard papers with default reading time and 30/5-minute warnings.
  - **IGCSE**: Extended/Additional papers with 5-minute warnings.
  - **Maths Olympiads**: Presets for Kangaroo, OBMEP, and Jacob Palis Jr.
  - **Custom**: Fully definable board name and parameters.
- **Customizable Times & Warnings**: Toggle and define specific Reading Time, Extra Time (by percentage or absolute minutes), and custom comma-separated warning milestones via the "More options" menu.
- **Up to 16 simultaneous timers** in a responsive grid. Cards can be manually resized and dragged-and-dropped to reorder.
- **Live countdown & Next Announcement**: Header displays the current time, current date, and the next global milestone announcement across all active exams.
- **Inline & Full Editing**: Edit Start/Reading times inline directly on the card, or use the pencil icon to reopen the setup menu and modify all timer settings.
- **Save / Load**: Save all timer configurations locally as a JSON file and load them to restore sessions.
- **Color-Coded Themes**: 
  - IB: Blue
  - IGCSE: Red
  - Maths Olympiads: Yellow (with high-contrast black text)
  - Custom: Black
- **Dynamic Exam Finished Banner**: A mathematically calculated, diagonal "EXAM HAS FINISHED" banner overlay appears when the main countdown hits zero.

## Usage

1. Open `index.html` in a browser — the **Maths exams** landing page
2. Click **Exam Timer** (or **Incident Log Sheet**)
3. On the timer page, select your exam board preset or choose "Custom".
4. Enter exam name, duration, and start time.
5. (Optional) Expand **More options** to configure Reading Time, add extra Warning milestones, or adjust Extra Time allowances.
6. Click **Add Timer**.
7. Click the **+ Add Timer** button in the header to add more (up to 16).

### Editing times

- **Inline Adjustments**: Click the reading time or start time values directly on the card to adjust them. All subsequent warnings recalculate automatically.
- **Full Edit**: Click the pencil icon (top right of any card) to completely modify the exam's name, board, duration, and extra options.

### Save / Load

- After the first timer is added, a popup reminds you to use **Save Timer** to download your session in case of a shutdown.
- **Save Timer** (bottom) saves all timer configurations as `timer.json`.
- **Load Timer** on the setup screen imports a previously saved `timer.json`.

### Reordering & Resizing

- Drag any card and drop it onto another card's position to reorder.
- Drag the bottom-right corner of any exam card to manually resize it.

## Incident Log Sheet

`incident-log.html` is a separate tool for logging exam incidents (toilet, sickbay, etc.).

1. On load, enter the **Room**, **Exam**, and **Date**.
2. Press **Add Log** to record an incident — **Candidate**, **Incident**, **Left** time, **Back** time (times are 24-hour `HH:MM`).
3. Click any row to edit or delete it.
4. **Save Sheet (CSV)** downloads the sheet as a `.csv` file (named after the exam and date), including the Room/Exam/Date header rows.

> The CSV is generated entirely in the browser and saved to the device — the site is static, with no backend or upload.

## Timer milestones

| Milestone    | Details |
|-------------|---------|
| Reading     | Pre-start period (Optional, customizable minutes). Editable inline. |
| Start       | User-defined or current time. Editable inline. |
| Warnings    | Dynamically highlighted milestones (e.g., 30 min, 5 min). Can be added natively or explicitly defined via "More options". |
| End         | Start + duration. Main countdown hits zero, triggering the "EXAM HAS FINISHED" banner. |
| Extra time  | Optional post-end timer. Defined globally as 25% or set to custom absolute minutes. |

When a milestone is reached, its row is highlighted in the board's theme color (inverted text) for one minute. The countdown shows **Time Remaining** until the normal end, then switches to **Extra Time** (counting down the extra-time allowance) until the extra time finishes. Maths boards use an exclusive black/yellow high-contrast inversion for active warnings.

## File structure

```text
exams-hall/
  index.html         # Landing page (links to the tools)
  timer.html         # Exam timer application (HTML + CSS + JS)
  incident-log.html  # Incident log sheet (HTML + CSS + JS)
  README.md          # This file
