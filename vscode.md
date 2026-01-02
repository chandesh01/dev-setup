# VS Code Starter

A minimal, reusable **VS Code project setup** using explicit configuration files.

> [Install](https://code.visualstudio.com/)

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
| **Ctrl + ,**         | Settings               |

### Terminal

| Shortcut             | Action               |
| -------------------- | -------------------- |
| **Ctrl + `**         | Toggle terminal      |
| **Ctrl + Shift + `** | New terminal         |
| **Ctrl + C**         | Stop running process |

> [docs](https://code.visualstudio.com/docs/configure/keybindings#_keyboard-shortcuts-reference)

## 2. Start VS Code with a **Custom Profile (Isolated Data Dir)**

* **Create Directory**

```sh
mkdir ~/vscode-profile && cd ~/vscode-profile
```

* **Default:**

```sh
code --user-data-dir . --profile C --extensions-dir ./extentions
```

* **C:**

```sh
code --user-data-dir . --profile C --extensions-dir ./extentions
```

* **Python:**

```sh
code --user-data-dir . --profile Python --extensions-dir ./extentions
```

> To Create Using Templates: `Ctrl + Shift + P -> Preferences: Open Profiles (UI) -> New Profile (Dropdown) -> From Template`

## 3. Update All Extensions (CLI)

```powershell
code --update-extensions
```

## 4. Minimal `.vscode/settings.json` (Baseline)

Open : `Ctrl + Shift + P` -> Preferences: Open User Settings (JSON)

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

> or save to: user-data-dir/user/settings.json