---
description: Create a countdown timer that can run in the terminal.
argument-hint: <customer>
---
PYTHON COUNTDOWN TIMER (CLI)

Goal:
Create a Python command-line countdown timer application with ASCII-art display and color-coded urgency levels.

--------------------------------------------------
Project Structure:
- Place all code inside:
  lab0/
- Main file:
  lab0/countdown.py

--------------------------------------------------
Inputs (Command-Line Arguments):
The program must accept:
  --time (integer): time in minutes
  --title (string): title displayed above the timer
  --customer (string): customer name (must be displayed)

Example:
python3 lab0/countdown.py --time 5 --title "Focus Session" --customer "ACME Corp"

--------------------------------------------------
Countdown Behavior:
- Convert minutes to seconds
- Count down to zero
- Update display every second
- Show remaining time in MM:SS format

--------------------------------------------------
ASCII Art Display:
- Render the time using large ASCII-art digits
- Update (redraw) every second
- Display must include:
  - Title (top)
  - Timer (center, ASCII art)
  - Customer name (visible)

--------------------------------------------------
Color Coding (NO external libraries):
Use ANSI escape codes only.

Color rules:
- Green: more than 50% time remaining
- Yellow: between 20% and 50%
- Red: less than 20%

--------------------------------------------------
Constraints:
- Do NOT use any external libraries
- Only Python standard library is allowed
- Must run in a standard terminal

--------------------------------------------------
Code Requirements:
- Organize code into functions
- Add comments for clarity
- Ensure clean and readable structure

--------------------------------------------------
Bonus (Optional):
- Clear terminal before each redraw
- Handle invalid inputs gracefully
- Reduce flickering if possible

--------------------------------------------------
Deliverable:
- Complete Python script at:
  lab0/countdown.py
- Fully runnable without modifications