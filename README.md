# 🤖 GroqAgent - Autonomous AI Agent for Windows

> Control your computer with natural language. GroqAgent combines Groq's large language models with system tools - browser, files, Excel, and CMD - into a single autonomous agent running locally on Windows 11.

---

## ✨ Features

| Category | Capabilities |
|----------|-------------|
| 🌐 **Browser** | Open pages, click elements, fill forms, take screenshots, execute JavaScript |
| 📁 **Files** | Read, write, copy, move, delete files and folders |
| 📊 **Excel** | Create spreadsheets, edit cells, formulas (`SUM`, `VLOOKUP`, `COUNTIF`...), bar / line / pie charts, cell styling |
| ⚙️ **System** | Run CMD / PowerShell commands, capture output |
| 🔗 **Web** | Fast HTTP page content fetching without a browser |
| 🧠 **Dual Model** | Auto-selects between fast (`llama-3.1-8b`) and smart (`llama-3.3-70b`) model based on task complexity |

---

## 🚀 Quick Start

### 1. Clone the repository

```bash
git clone https://github.com/YOUR_USERNAME/groqagent.git
cd groqagent
```

### 2. Install dependencies

```bash
pip install -r requirements.txt
playwright install chromium
```

### 3. Add your API key

Get a free key at [console.groq.com](https://console.groq.com) and paste it into `agent_ai.py`:

```python
API_KEY = "gsk_..."  # ← here
```

### 4. Run

```bash
python agent_ai.py
```

---

## 💬 Usage Examples

```
👤 You: Open google.com and search for the weather in New York

👤 You: Take a screenshot of bbc.com and save it to the desktop

👤 You: Create an Excel file with a 12-month home budget and a bar chart

👤 You: Go to Wikipedia, find the 10 largest cities in Poland
        and save the data to Excel with formulas and a pie chart

👤 You: List all files on the desktop

👤 You: Run ipconfig and save the result to a txt file
```

---

## 🧠 Dual Model Strategy

The agent automatically picks the right model for each task, saving your API quota:

```
Simple task   →  llama-3.1-8b-instant    (14,400 req/day)
Complex task  →  llama-3.3-70b-versatile  (1,000 req/day)
```

**Selection criteria:**
- Short prompt with simple keywords (`open`, `click`, `save`) → fast model
- Long prompt (>200 chars) or keywords (`analyz`, `report`, `excel`, `html`, `chart`) → smart model
- Smart model quota exhausted → automatic fallback to fast model

Type `status` at any time to see current usage.

---

## 🛠️ Available Tools

### 📁 Files
| Tool | Description |
|------|-------------|
| `read_file` | Read a text file (txt, py, html, csv, json...) |
| `write_file` | Write text to a file, creates directories if needed |
| `list_files` | List directory contents with file sizes |
| `open_file` | Open a file in its default application |
| `delete_file` | Delete a file or folder |
| `copy_file` | Copy a file |
| `move_file` | Move a file |
| `create_directory` | Create a folder (recursive) |

### 🌐 Browser (Playwright)
| Tool | Description |
|------|-------------|
| `browser_goto` | Navigate to a URL |
| `browser_click` | Click an element (text or CSS selector) |
| `browser_type` | Type text into a form field |
| `browser_get_text` | Get all visible text from the page |
| `browser_screenshot` | Take a full-page screenshot (PNG) |
| `browser_get_links` | Return a list of all links on the page |
| `browser_scroll` | Scroll the page (up / down / top / bottom) |
| `browser_press_key` | Press a key (Enter, Tab, Escape...) |
| `browser_eval_js` | Execute JavaScript and return the result |
| `browser_wait` | Wait N seconds |

### 📊 Excel (openpyxl)
| Tool | Description |
|------|-------------|
| `create_excel` | Create a new .xlsx file with data and formatting |
| `read_excel` | Read spreadsheet contents |
| `edit_excel_cell` | Edit a single cell value |
| `add_excel_formula` | Insert a formula (`=SUM`, `=IF`, `=COUNTIF`...) |
| `add_excel_chart` | Add a chart (bar / line / pie) |
| `add_excel_sheet` | Add a new sheet to an existing file |
| `excel_add_rows` | Append rows to a sheet |
| `excel_style_range` | Style a cell range (bold, background color, font size) |

### ⚙️ System
| Tool | Description |
|------|-------------|
| `run_command` | Run a CMD / PowerShell command |
| `read_webpage` | Fast HTTP page text fetch (no browser) |

---

## ⌨️ Built-in Commands

| Command | Action |
|---------|--------|
| `exit` / `quit` | Shut down the agent |
| `reset` / `clear` | Clear conversation history |
| `status` | Show model usage stats and history length |

---

## 📦 Requirements

- Python 3.10+
- Windows 10 / 11
- Free Groq account - [console.groq.com](https://console.groq.com)

```
groq>=0.9.0
playwright>=1.40.0
openpyxl>=3.1.0
```

---

## 🗂️ Project Structure

```
groqagent/
├── agent_ai.py        # Main agent file
├── requirements.txt   # Dependencies
└── README.md          # Documentation
```

---

## ⚠️ Known Limitations

- Windows only (`os.startfile`, Windows-style paths)
- Browser requires Chromium: `playwright install chromium`
- Conversation history capped at 50 messages (older messages are trimmed automatically)
- Maximum 25 tool-call iterations per task

---

## 📄 License

MIT - use, modify, and distribute freely.
