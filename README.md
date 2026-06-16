# Exams Hall

A minimalistic web-based timer for IB and IGCSE exams. Single-page HTML/CSS/JS application with no dependencies.

## Features

- **IB exams**: 5-minute reading time, 30-minute warning, 5-minute warning
- **IGCSE exams**: 5-minute warning
- **Up to 16 simultaneous timers** in a grid (4 per row, wraps to new rows)
- Drag-and-drop to reorder cards
- Live countdown with current time display
- Inline editable time field per card (reading time for IB, start time for IGCSE) with bordered input — all warning times recalculate automatically
- Default start time set to the current time when adding a timer
- Save reminder popup shown after adding the first timer
- Save/load all timer configurations as JSON
- Remove individual timers with the x button
- Color-coded cards: blue (IB), red (IGCSE)
- High-contrast black text on white background; inverted white text on highlighted warnings
- Large, readable fonts — milestone rows sized close to the countdown for visibility at a distance

## Usage

1. Open `index.html` in a browser — the **Exams Hall** landing page
2. Click **Exam Timer** (or **Incident Log Sheet**)
3. On the timer page, select exam board (IB or IGCSE)
4. Enter exam name, duration, and start time
5. Click **Add Timer**
6. Click the **+** card to add more timers (up to 16)
7. Use the **← Home** link (top-left) to return to the landing page

### Editing times

- **IB**: click the reading time value directly to adjust — start and all warnings recalculate (start = reading + 5 min)
- **IGCSE**: click the start time value directly to adjust — all warnings recalculate

### Save / Load

- After the first timer is added, a popup reminds you to use **Save Timer** to download your session in case of a shutdown
- **Save Timer** (bottom center) saves all timer configurations as `timer.json`
- **Load Timer** on the setup screen imports a previously saved `timer.json`

### Reordering

Drag any card and drop it onto another card's position to reorder.

## Incident Log Sheet

`incident-log.html` is a separate tool for logging exam incidents (toilet, sickbay, etc.).

1. On load, enter the **Room**, **Exam**, **Date**, and a **Submit to email** address
2. Press **Add Log** to record an incident — **Candidate**, **Incident**, **Left** time, **Back** time (times are 24-hour `HH:MM`)
3. Click any row to edit or delete it
4. **Submit Sheet** opens a pre-addressed email draft to the entered address with the table exported as CSV in the body — review and send from your mail app

> Email sending uses a `mailto:` draft (the site is static, with no backend). The CSV is placed in the email body as text, not as a file attachment.

## Timer milestones

| Milestone    | IB  | IGCSE |
|-------------|-----|-------|
| Reading     | Start - 5 min (editable) | -- |
| Start       | Reading + 5 min | User-defined (editable) |
| 30 min left | End - 30 min | -- |
| 5 min left  | End - 5 min | End - 5 min |
| End         | Start + duration | Start + duration |

When a milestone is reached, its row is highlighted (blue for IB, red for IGCSE) for one minute. After that minute the highlight moves to the remaining-time countdown — with inverted white text — and stays there until the exam ends.

## File structure

```
exams-hall/
  index.html         # Landing page (links to the tools)
  timer.html         # Exam timer application (HTML + CSS + JS)
  incident-log.html  # Incident log sheet (HTML + CSS + JS)
  README.md          # This file
```

## Configuration file format

`timer.json` schema (array of timers):

```json
[
  {
    "board": "IB",
    "name": "English B Paper 1 HL",
    "durationMin": 90,
    "startMin": 540
  },
  {
    "board": "IGCSE",
    "name": "Biology Paper 4",
    "durationMin": 75,
    "startMin": 540
  }
]
```

Loading also accepts a single object (legacy format).

| Field         | Type   | Description                            |
|--------------|--------|----------------------------------------|
| `board`      | string | `"IB"` or `"IGCSE"`                   |
| `name`       | string | Exam name                              |
| `durationMin`| number | Exam duration in minutes               |
| `startMin`   | number | Start time as minutes from midnight (e.g. 540 = 09:00) |

## Browser support

Any modern browser (Chrome, Firefox, Safari, Edge). No build step or server required.

## License

Released under the [MIT License](LICENSE).
