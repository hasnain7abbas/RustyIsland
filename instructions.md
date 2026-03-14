# RustyIsland Feature Upgrade Specification

You are an expert Rust, Tauri, and React developer. I need you to implement the following 4 upgrades to this codebase. Please read through all requirements, formulate a plan, and execute the code changes step-by-step.

## 1. Clean Up the Terminal Spam
- **The Issue:** The terminal is constantly spammed with "Ensuring window stays always on top".
- **The Fix:** Find the loop in the Rust backend (`src-tauri/src/main.rs`) that prints this debug message and completely remove or comment out the `println!` statement.

## 2. Fix the "Annoying Transparent Box" (Windows Ghost Window)
- **The Issue:** On Windows, borderless transparent Tauri windows sometimes leave a faint background box, shadow, or outline.
- **The Fix:** - Check `tauri.conf.json` to ensure `"decorations": false` and `"transparent": true` are set on the main window.
  - In the Rust backend window setup, explicitly disable window shadows if possible, or clear the window background color.
  - In the React CSS (e.g., `App.css`, `index.css`, or Tailwind config), ensure the `body` and `html` tags have `background-color: transparent !important;` and no borders.

## 3. Build the Process Killer (Task Manager)
- **The Issue:** We can see top CPU processes, but we can't do anything about them.
- **The Fix:**
  - **Rust Backend:** Write a new Tauri command using the `sysinfo` crate to safely kill a process given its PID (`u32`). Register this command in the main builder.
  - **React Frontend:** In the expanded Dynamic Island view, add a subtle, red "Kill" or "X" button next to each process. 
  - **Wiring:** Wire the button to `invoke` the kill command with the correct PID, and force the UI to refresh the process list immediately after.

## 4. Add a Custom Transparency Slider
- **The Issue:** The user cannot customize how transparent the Dynamic Island widget is.
- **The Fix:**
  - In the React frontend's expanded view, add a simple HTML range slider (min: 0.1, max: 1.0, step: 0.1).
  - Bind this slider to a React state variable (e.g., `widgetOpacity`).
  - Apply this opacity state dynamically to the main widget's container `style={{ opacity: widgetOpacity }}` so the entire widget becomes more or less see-through based on user preference. Save this preference to `localStorage` if possible so it remembers it on restart.