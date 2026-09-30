# Maths exams

Based on oscarneiva's Exams Hall.

A minimalistic web-based timer for IB, IGCSE, Maths Olympiads, and custom exams. Single-page HTML/CSS/JS application with no dependencies.

## Features

- **Multiple Exam Boards & Presets** — choosing a board fills in its default duration, warnings, reading time and extra time:

  | Board | Papers | Warnings | Reading time | Extra time |
  |-------|--------|----------|--------------|------------|
  | **IB** | Higher P1, P2 (2h), Higher P3 (1h15m), Standard P1, P2 (1h30m), Custom IB (1h30m) | 30 & 5 min | 5 min | 25% |
  | **IGCSE** | Extended P2, P4, P6 (1h30m), Additional P1, P2 (2h), Custom IGCSE (1h30m) | 5 min | Off | 25% |
  | **Maths Olympiads** | Kangaroo (1h40m), OBMEP (2h30m), Jacob Palis Jr (2h30m) | 20 & 5 min (Jacob Palis: 15 & 5 min) | Off | Off |
  | **Custom** | Your own board name (45m by default) | 5 min | Off | 25% |

  Every default can be changed for each timer before adding it.
- **Customizable Times & Warnings**: Under "More options", turn Reading Time on or off, tick or untick warnings, add extra comma-separated warnings (whole minutes before the end), and set Extra Time as a percentage or in absolute minutes.
- **Parallel Extra Time**: Extra-time candidates get their own, longer exam with the same start time. Their warnings are counted back from the extended end and announced separately (see [Extra time](#extra-time)).
- **Up to 16 simultaneous timers** in a responsive grid. Cards can be manually resized and dragged-and-dropped to reorder.
- **Live countdown & Next Announcement**: The header shows the current time and date, and the next announcement across all exams. With several exams open it names the exam(s) the announcement is for, and it flags announcements that are only for extra-time candidates.
- **Inline & Full Editing**: Edit Start/Reading times inline directly on the card, or use the pencil icon to reopen the setup menu and modify all timer settings.
- **Save / Load**: Save all timer configurations locally as a JSON file and load them to restore sessions.
- **Color-Coded Themes**:
  - IB: Blue
  - IGCSE: Red
  - Maths Olympiads: Yellow (with high-contrast black text)
  - Custom: Black
- **Dynamic Exam Finished Banner**: A mathematically calculated, diagonal "EXAM HAS FINISHED" banner overlay appears when all time, including any extra time, has run out. It redraws to fit when the card is resized.
- **Accurate timing**: The clock updates exactly on each second, start times may include seconds (`HH:MM:SS`), and exams that run past midnight keep counting correctly.
- **Works on any screen**: 4 columns on desktop, 3 on small desktops, 2 on tablets, 1 on phones. On phones the header stacks so the clock, next announcement and Add button stay visible.

## Usage

1. Open `index.html` in a browser — the **Maths exams** landing page
2. Click **Exam Timer**
3. On the timer page, select your exam board preset or choose "Custom" (you will be asked for a board name).
4. Enter exam name, duration, and start time (24-hour `HH:MM` or `HH:MM:SS`).
5. (Optional) Expand **More options** to configure Reading Time, Warnings, or Extra Time.
6. Click **Add Timer**.
7. Click the **+ Add Timer** button in the header to add more (up to 16). The form always opens with the Custom board's defaults.

### Editing times

- **Inline Adjustments**: Click the reading time or start time values directly on the card to adjust them. All subsequent warnings (regular and extra time) recalculate automatically.
- **Full Edit**: Click the pencil icon (top right of any card) to modify the exam's name, board, duration, and extra options. The card's existing warnings, including custom ones, appear as ticked checkboxes; untick one to remove it. Switching a Custom timer to another board replaces the custom board name with that board's label.

### Save / Load

- After the first timer is added, a popup reminds you to use **Save Timer** to download your session in case of a shutdown.
- **Save Timer** (bottom) saves all timer configurations as `timer.json`, including reading time and the extra-time setting.
- **Load Timer** on the setup screen imports a previously saved `timer.json`. If timers are already open, you are asked to confirm before they are replaced. A file with no valid timers is rejected and your current timers are kept.
- Save files from older versions still load. They did not store reading time, so each timer gets its board's default reading time.

### Reordering & Resizing

- Drag any card and drop it onto another card's position to reorder.
- Drag the bottom-right corner of any exam card to manually resize it.

## Incident Log Sheet (not in use)

> **Not currently in use.** `incident-log.html` is kept in the repository for possible future use, but it is not part of the exam timer. `timer.html` does not contain or depend on any incident-log code. The description below is kept for reference.

`incident-log.html` is a separate tool for logging exam incidents (toilet, sickbay, etc.).

1. On load, enter the **Room**, **Exam**, and **Date**.
2. Press **Add Log** to record an incident — **Candidate**, **Incident**, **Left** time, **Back** time (times are 24-hour `HH:MM`).
3. Click any row to edit or delete it.
4. **Save Sheet (CSV)** downloads the sheet as a `.csv` file (named after the exam and date), including the Room/Exam/Date header rows.

> The CSV is generated entirely in the browser and saved to the device — the site is static, with no backend or upload.

## Timer milestones

| Milestone    | Details |
|-------------|---------|
| Reading     | Pre-start period (optional, in minutes). Editable inline. |
| Start       | User-defined or current time. Editable inline. |
| Warnings    | Minutes before the end (e.g., 30 min, 5 min). Set per board and adjustable in "More options". |
| End         | Start + duration. A **Regular time finished** badge appears under it once reached. |
| Extra time  | Optional. End of the extended duration (duration + extra time). Extra-time warnings are announced but not listed on the card. |

When a milestone is reached, its row is highlighted in the board's theme color (inverted text) for one minute. The countdown shows **Waiting to Start** or **Reading Time** before the start, **Time Remaining** until the normal end, then **Extra Time** until the extra time finishes, and finally **Exam Finished**. Maths boards use an exclusive black/yellow high-contrast inversion.

### Extra time

Extra-time candidates sit a parallel exam: the same start, with the extra time added to the duration. Their warnings count back from that extended end.

Example: a 1h exam with +25% extra time and 30 & 5 minute warnings, starting at 09:00.

| Time  | Regular candidates | Extra-time candidates |
|-------|--------------------|-----------------------|
| 09:30 | 30 minutes left    |                       |
| 09:45 |                    | 30 minutes left       |
| 09:55 | 5 minutes left     |                       |
| 10:00 | End                |                       |
| 10:10 |                    | 5 minutes left        |
| 10:15 |                    | End of extra time     |

- The card lists only the **EXTRA TIME** end. When an extra-time warning is reached, the matching warning label (e.g. "30 MIN") and the "EXTRA TIME" label are highlighted in a lighter shade of the board color for one minute.
- Extra time is rounded to whole minutes (25% of 1h30m becomes 23 minutes).

### Next Announcement

The header shows the time of the next announcement across all open exams:

- **NEXT ANNOUNCEMENT**: a regular warning or end.
- **EXTRA TIME WARNING** / **EXTRA TIME END** (amber): an announcement only for extra-time candidates.
- With several exams open, the exam name(s) appear under the time.
- When regular and extra-time announcements fall at the same moment, two lines show which board each is for, e.g. `Regular: IGCSE - Additional Paper 1` and `Extra: IB - Higher Paper 1`. If more than one exam of a kind is due, that line reads **Multiple**.

## Changing presets

All board defaults live in one table, `examPresets`, near the top of the script in `timer.html`. Each entry sets the board's color theme, card label, duration, warnings, reading time and extra-time percentage. The dropdown text (e.g. "Higher Paper 1 (2h)") is written separately in the HTML, so update it too when changing a duration.

## File structure

```text
exams-hall/
  index.html         # Landing page (links to the tools)
  timer.html         # Exam timer application (HTML + CSS + JS)
  incident-log.html  # Incident log sheet (HTML + CSS + JS), not in use
  README.md          # This file
```
