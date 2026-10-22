# daansys

**daansys** is a powerful, feature-rich command-line AI assistant powered by Google Gemini and built for .NET Framework 4.7.2. It combines an interactive chat experience with deep system diagnostics, an autonomous coding agent, multi-agent workflows, code linting, and a long list of usable and useful commands and plugins.

---

## Features

### 💬 Chat & AI Experience
* **Streaming Responses:** Watch answers stream live word-by-word with real-time markdown color coding.
* **Multimodal Attachments:** Attach local files, images, or PDFs to your prompts using `@filename` or by pasting from your clipboard (`/paste`).
* **Chat Management:** Automatically saves chat histories, supports search (`/search`), resuming earlier sessions (`/load`), temporary chats (`/temp`), and exporting to Markdown (`/export`).
* **Custom Profiles & Personas:** Switch between specialised conversation styles (*default, friend, writer, translator, coach, teacher, code, debug, architect*) or create reusable instructions with `/persona`.
* **Permanent Memory:** Teach the AI facts to remember across all conversations using `/remember` and `/memories`.

### 🛠️ Developer & Power Tools
* **Autonomous Coding Agent (`/agent`):** Instruct the AI to analyze your workspace files and apply code modifications with your approval.
* **Multi-Agent Workflows (`/team`):** Splits complex goals across specialized AI agents: *Agent 1 (Architect)* builds a blueprint, *Agent 2 (Coder)* writes the implementation, and *Agent 3 (Tester)* reviews and writes unit tests.
* **AI Code-Linter & Bugfixer (`/lint`):** Scans source files for code smells, security flaws, and syntax bugs, rendering a clean breakdown table with automated fix options.
* **Roslyn C# Code Runner (`/run`):** Execute C# script blocks directly inside your terminal with full runtime configuration.
* **Windows Diagnostics (`/sys`):** Over 25 built-in diagnostic and repair scripts (Wi-Fi fixes, network reset, SFC/DISM scans, startup items, process monitors, and event log analyzers).
* **Handy Utilities:** Built-in calculator (`/calc`), IP & DNS lookup (`/ip`), hash generator (`/hash`), Unix timestamp converter (`/timestamp`), secure password generator (`/pass`), snippet vault, countdown timers, world clocks, and live weather (`/weather`).

---

## 👑 Pro Tier & Support

**daansys** is completely free to use. Upgrading to **Pro** unlocks the ability to implement special plugins, and high-performance model allocations.

* **How to get Pro:** Send an email request to **[help.daansys@gmail.com](mailto:help.daansys@gmail.com)**.

---

## 🔌 Lua Plugin System Documentation

daansys features a heavily sandboxed Lua scripting environment (powered by MoonSharp) allowing infinite extensibility through custom commands, themes, and tool integrations.

### Security & Restrictions
* **Sandboxed:** Standard dangerous modules (`io`, `os`, `debug`, `require`, `load`, `package`) are strictly blocked.
* **Validation:** Plugins are checked upon creation, database storage, and local loading.
* **Resource Limits:** Maximum source length is 30,000 characters, up to 20 custom commands per plugin, and a 4-second CPU timeout per execution.

### Available API Reference (`daansys.*`)
* `daansys.say(text[, color])` — Prints text to the console. Optional `#rrggbb` color tag.
* `daansys.ask(text)` — Sends an automated prompt directly to the AI (must be the final call in `run`).
* `daansys.copy(text)` — Copies text to the system clipboard.
* `daansys.open(url)` — Opens an `https://` URL in the default browser (prompts user for confirmation).
* `daansys.http_get(url)` — Performs a safe external `https://` web request and returns the string response.
* `daansys.store_get(key)` / `daansys.store_set(key, val)` — Persistently stores and retrieves plugin data securely.
* `daansys.random(min, max)` — Returns a random integer between `min` and `max`.
* `daansys.pick(table)` — Picks a random string item from a Lua table array.
* `daansys.theme({accent, prompt, ailabel, banner})` — Dynamically restyles the application interface UI.
* `daansys.command(name, {usage, help, category, run = function(args) ... end})` — Registers a new custom command.

### Global Variables
* `daansys.user` — Current username.
* `daansys.ai` — Current AI assistant name.
* `daansys.date` — Current system date (`YYYY-MM-DD`).
* `daansys.time` — Current system time (`HH:mm`).

### Example Plugin Template
```lua
-- daansys Lua plugin template

daansys.command("hello", {
  usage = "/hello [name]",
  help  = "Greets someone and asks the AI for a fun fact",
  category = "Fun",
  run = function(args)
    local name = args[1] or daansys.user
    daansys.say("Hello " .. name .. "! It is " .. daansys.time .. ".", "#00ffd5")
    daansys.ask("Tell " .. name .. " one surprising fun fact. Keep it short.")
  end
})
Credits
Created with ❤️ by Daan Van de Velde (Wetteren, Belgium).
Support & Contact: help.daansys@gmail.com

