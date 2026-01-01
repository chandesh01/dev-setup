# VS Code Starter

A minimal, reusable **VS Code project setup** using explicit configuration files.

## 1. Handy VS Code Shortcuts (Must-Know)

### Build / Run / Debug

| Shortcut             | Action            |
| -------------------- | ----------------- |
| **Ctrl + Shift + B** | Run build task    |
| **Ctrl + F5**        | Run (no debugger) |
| **F5**               | Debug             |
| **Shift + F5**       | Stop debugging    |

### Editing & Navigation

| Shortcut             | Action                 |
| -------------------- | ---------------------- |
| **Ctrl + P**         | Quick file open        |
| **Ctrl + Shift + P** | Command Palette        |
| **Ctrl + /**         | Toggle comment         |
| **Alt + ↑ / ↓**      | Move line              |
| **Ctrl + D**         | Select next occurrence |
| **Ctrl + L**         | Select entire line     |

### Terminal

| Shortcut             | Action               |
| -------------------- | -------------------- |
| **Ctrl + `**         | Toggle terminal      |
| **Ctrl + Shift + `** | New terminal         |
| **Ctrl + C**         | Stop running process |

## 2. Enable **Auto Save**

### Option A: `settings.json` (Recommended)

Add this to **`.vscode/settings.json`** (project-specific)
or **User Settings** (global):

```json
{
  "files.autoSave": "afterDelay",
  "files.autoSaveDelay": 1000
}
```

**Auto Save modes**

| Value              | Meaning                     |
| ------------------ | --------------------------- |
| `"off"`            | Manual save (default)       |
| `"afterDelay"`     | Auto save after delay       |
| `"onFocusChange"`  | Save when switching files   |
| `"onWindowChange"` | Save when switching windows |

### Option B: Command Palette (Quick)

1. Press **Ctrl + Shift + P**
2. Type **Auto Save**
3. Select **File: Toggle Auto Save**

## 3. Enable **Format on Save**

Add this to **`settings.json`**:

```json
{
  "editor.formatOnSave": true
}
```

>  Works **only if a formatter is installed** for that language
> (e.g. Prettier, clang-format, black, gofmt).

**Recommended (safe) enhancement**

```json
{
  "editor.formatOnSave": true,
  "editor.formatOnSaveMode": "file"
}
```

## 4. Start VS Code with a **Custom Profile (Isolated Data Dir)**

Use this when you want a **clean, reproducible VS Code environment**.

### Windows (PowerShell / CMD)

```powershell
code --user-data-dir "%USERPROFILE%\vscode-profiles\default\data" ^ --extensions-dir "%USERPROFILE%\vscode-profiles\default\extensions"
```

## 5. Update All Extensions (CLI)

```powershell
code --update-extensions
```

## 7. Minimal `.vscode/settings.json` (Baseline)

> Save to: user-data-dir/user/settings.json

```json
{
  "github.copilot.enable": {
    "*": false,
    "plaintext": false,
    "markdown": false,
    "scminput": false,
    "cpp": false
  },

  "C_Cpp.default.compilerPath": "C:/msys64/ucrt64/bin/gcc.exe",

  "clang-format.executable": "C:/msys64/ucrt64/bin/clang-format.exe",

  "files.autoSave": "afterDelay",
  "files.autoSaveDelay": 1000,

  "editor.formatOnSave": true,
  "editor.formatOnSaveMode": "file",

  "editor.tabSize": 2,
  "editor.insertSpaces": true,
  "editor.trimAutoWhitespace": true,

  "files.trimTrailingWhitespace": true
}

```
