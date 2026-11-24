# Soma Quiz Info Panel

A Tampermonkey userscript for [app.soma.lv](https://app.soma.lv) that shows the correct answers for the quiz question on screen in a small draggable panel, and can optionally fill in and submit answers automatically.

Find the script [here](https://github.com/Terybery453423/soma.lv-autofiller/blob/main/the%20script) 

> **Use responsibly.** Auto-answering graded or homework quizzes may break your school's or teacher's rules. Use this to check your understanding, to study, or on practice quizzes where it's allowed. You are responsible for how you use it.

## Features

- **Answer panel** showing the correct answers for the current question, with the explanation when the site provides one.
- **Draggable and minimizable** window; navigate between captured questions with ◀ and ▶.
- **Supported question types:**
  - Multiple choice and multiple response
  - Free-text and fill-in-the-blank
  - Ordering (drag rows into the correct order)
  - Word bank (click a blank, then the word)
  - Connecting rows (click a left item, then its right partner)
- **Optional automation**, all **off by default** and reset on every page load:
  - **Auto-fill**: fills in the correct answers.
  - **Auto-submit**: submits once the answer is filled (needs Auto-fill).
  - **Auto-next**: moves on to the next question after feedback (needs Auto-fill).
  - **Turbo**: shortens the waits between clicks. Drag gestures and the wait before submitting an ordering question are not shortened.
- **🐞 Log**: a live log of what the script is doing, with a Copy log button for bug reports.

## Installation

1. Install [Tampermonkey](https://www.tampermonkey.net/) in your browser (Chrome, Edge, Firefox, Safari, or an Android browser that supports extensions).
2. Open the Tampermonkey dashboard and click **Create a new script**.
3. Delete the template and paste the contents of `soma-quiz-info.user.js`.
4. Save with **Ctrl+S** (or **Cmd+S**).
5. Open or reload `https://app.soma.lv`. The panel appears in the bottom-right corner.

The script runs at `document-start` so it can see the quiz data the site loads. **Reload the page after installing or updating the script**, then start the quiz again.

## Usage

- **Read answers:** start a quiz. The panel fills in with the correct answers for the current question.
- **Drag the panel:** grab the title bar.
- **Minimize:** the **–** button. Click **+** to restore.
- **Step through questions:** ◀ and ▶ in the header.
- **Automation toggles** in the row under the header:
  - **Auto-fill** fills in each question. Watch the first few to confirm it works.
  - **Auto-submit** and **Auto-next** only act while Auto-fill is on.
  - **Turbo** speeds up the clicks. Turn it off if clicks start landing before the page reacts.

## How it works

The script runs in the page context and hooks the page's `fetch`, `XMLHttpRequest`, and `WebSocket` calls. It captures question data as it loads and matches it to what's on screen, then either displays it or clicks/types the answers. It does not contact any server of its own.

## Troubleshooting

- **"Waiting for quiz data…"**: reload the page, then start the quiz again.
- **"Question N is open, but its data was not captured"**: same fix. If it persists, open the 🐞 log and copy it into a bug report.
- **Auto-fill does nothing**: check the log. Messages like `could not match options` or `item not found` tell you what didn't match.
- **Clicks land too fast / options get unticked**: turn **Turbo** off.
- **Ordering question not solved**: the log shows which drag method was tried. Send the log in an issue.

## Known issues

- Not every question type on soma.lv is covered. Unsupported types show only the panel and must be answered manually.
- Matching depends on the page's exact text. Small differences in formatting can cause "item not found."
- Site changes can break the script without warning.

## Reporting bugs

Open an issue and include:
- The question type (shown in the panel's grey line, e.g. `multi_choice`)
- What the panel showed and what the page did
- The log from the 🐞 button (**Copy log**)

Don't include personal account data or screenshots that show your name or student ID.

## Disclaimer

This project is not affiliated with Soma or its owners. It's provided as-is, with no warranty. You are responsible for complying with your school's rules and Soma's terms of service.