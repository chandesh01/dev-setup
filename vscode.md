# VS Code Project Template Guide

A minimal, reusable **VS Code project setup** using explicit configuration files.

---

## 1. Handy VS Code Shortcuts (Must-Know)

### Build / Run / Debug

| Shortcut             | Action            |
| -------------------- | ----------------- |
| **Ctrl + Shift + B** | Run build task    |
| **Ctrl + F5**        | Run (no debugger) |
| **F5**               | Debug             |
| **Shift + F5**       | Stop debugging    |

---

### Editing & Navigation

| Shortcut             | Action                 |
| -------------------- | ---------------------- |
| **Ctrl + P**         | Quick file open        |
| **Ctrl + Shift + P** | Command Palette        |
| **Ctrl + /**         | Toggle comment         |
| **Alt + ↑ / ↓**      | Move line              |
| **Ctrl + D**         | Select next occurrence |
| **Ctrl + L**         | Select line            |

---

### Terminal

| Shortcut             | Action               |
| -------------------- | -------------------- |
| **Ctrl + `**         | Toggle terminal      |
| **Ctrl + Shift + `** | New terminal         |
| **Ctrl + C**         | Stop running process |

---

---

Here’s how to **set up Auto Save + Format on Save in VS Code** (clean + reproducible).

---

## 2. Enable **Auto Save**

### Option A: Using `settings.json` (Recommended)

Add this to **`.vscode/settings.json`** (project-specific)
or **User Settings** (global):

```json
{
  "files.autoSave": "afterDelay",
  "files.autoSaveDelay": 1000
}
```

**Modes you can use:**

| Value              | Meaning                      |
| ------------------ | ---------------------------- |
| `"off"`            | Default (manual save)        |
| `"afterDelay"`     | Auto save after delay (best) |
| `"onFocusChange"`  | Save when switching files    |
| `"onWindowChange"` | Save when switching windows  |

---

### Option B: Command Palette (Quick)

1. Press **Ctrl + Shift + P**
2. Type **Auto Save**
3. Select **File: TOggle Auto Save**

---

## 2. Enable **Format on Save**

Add this to **`settings.json`**:

```json
{
  "editor.formatOnSave": true
}
```

This works **only if a formatter exists** for that language.

---