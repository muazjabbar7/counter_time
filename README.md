# ⏱️ Countdown Timer

A versatile countdown timer with **both GUI and console versions**.  
Set custom time, use quick presets, and enjoy visual/audio alerts when time’s up.

![GUI Screenshot](Screenshot%202026-03-24%20190046.png)  
*GUI version with progress bar and preset buttons*

![Console Screenshot](Screenshot%202026-03-24%20190142.png)  
*Console version with simple text interface*

---

## ✨ Features

- **Two interfaces** – choose between a modern GUI (Tkinter) or a lightweight console version
- **Flexible time input** – enter minutes & seconds or just seconds
- **Quick presets** – 1, 5, 10, 15 minutes (GUI only)
- **Progress bar** – visual feedback (GUI only)
- **Pause & resume** – control the timer as needed
- **Sound & visual alerts** – system bell and flashing display on completion
- **Cross‑platform** – works on Windows, macOS, and Linux

---

## 📦 Requirements

- Python 3.6 or higher
- Tkinter (usually included with Python, but may need to be installed separately on Linux)

No external libraries required – all code uses the standard library.

---

## 🚀 Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/YOUR_USERNAME/counter_time.git
   cd counter_time


   Run the script
   python countdown_timer.py

   Choose your version

1 – GUI (graphical interface)

2 – Console (text‑based)

🎮 Usage
1. GUI Version
Set minutes and seconds using the spinboxes.

Click a preset button for quick settings.

Press Start to begin the countdown.

Pause/Resume and Reset are also available.

The progress bar fills as time elapses; the display flashes when the timer ends.

2. Console Version
Enter time in one of two formats:

5 30 → 5 minutes and 30 seconds

120 → 120 seconds (2 minutes)

Type quit to exit.

Press Ctrl+C to stop the timer early.

🧠 Code Explanation
The program starts with a simple menu asking the user to choose between the GUI (1) or console (2) version.
It then runs either the console_timer() function or creates a Tkinter root window with the CountdownTimer class.

1. Console Version – console_timer()
Prompts the user for time input.

Accepts either minutes seconds or just seconds.

Uses divmod() to format the countdown as MM:SS.

The sys.stdout.write with \r overwrites the same line, creating a real‑time effect.

Handles KeyboardInterrupt to allow early exit.

On completion, prints a message and triggers the system bell (\a).

2. GUI Version – CountdownTimer Class
Initialization (__init__)
Sets up the main window (root).

Defines timer variables: total_seconds, remaining_seconds, timer_running, timer_thread.

Calls setup_gui() to build the interface.

2.1 GUI Layout (setup_gui)
Title – large bold label.

Time display – a Label styled like a digital clock.

Input frame – two spinboxes for minutes and seconds, with initial values 0 and 30.

Preset buttons – using a loop to create buttons for 1, 5, 10, 15 minutes. Each button calls set_preset().

Progress bar – a ttk.Progressbar styled with green colour.

Control buttons – Start, Pause, Reset. The pause button initially disabled.

Status label – shows current state (running, paused, etc.).

2.2 Preset Handling (set_preset)
Converts the preset seconds to minutes/seconds.

Updates the spinboxes and the time display.

Changes the status label.

2.3 Timer Logic

.Starting – start_timer() validates input, stores total seconds, and sets remaining_seconds.
It starts a new thread (run_timer) to avoid freezing the GUI.

.Threaded countdown – run_timer() runs in a separate thread.
It updates the remaining seconds every second, and each second calls root.after(0, self.update_display) to safely update the GUI from a non‑main thread.

Pause/Resume – pause_timer() toggles timer_running.
When paused, the button text changes to “Resume” and its colour.
Clicking it again sets timer_running back to True and starts a new thread (since the old one ended).

Reset – stops the timer, clears variables, and resets all GUI elements.

2.4 Display & Feedback

update_display() – updates the time label and the progress bar value.

timer_completed() – runs when the thread finishes.
It changes the label colour, calls flash_display() for a visual effect, shows a message box, rings the bell (self.root.bell()), and resets the timer.

flash_display() – recursively changes the display colour every 500 ms to create a flashing effect.
