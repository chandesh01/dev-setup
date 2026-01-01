# Python Configuration Guide (CPython + venv)

A **minimal, cross-platform** setup for **Python** using **CPython**, **virtual environments**, and **VS Code**.

> Python docs: [https://docs.python.org/3/](https://docs.python.org/3/)
> VS Code Python docs: [https://code.visualstudio.com/docs/python/python-tutorial](https://code.visualstudio.com/docs/python/python-tutorial)

## 1. Install Python (CPython)

You only need **one Python installation**.
Virtual environments handle isolation.

## Windows

```powershell
winget install --id Python.Python
```

> Includes `pip` and the `py` launcher.

## Linux

### Ubuntu / Debian

```bash
sudo apt update
sudo apt install python3 python3-pip python3-venv
```

### Arch Linux

```bash
sudo pacman -S python python-pip
```

## macOS

```bash
brew install python
```

## Verify Installation

```sh
python --version
pip --version
```

If `python` is not found but `python3` exists, use:

```sh
python3 --version
```

## 2. Virtual Environments (Required)

**Rule:** Never install Python packages globally.

### Create a Virtual Environment

```sh
cd project/
python -m venv .venv
```

This creates an isolated Python environment in `.venv/`

### Activate

**Linux / macOS**

```sh
source .venv/bin/activate
```

**Windows (PowerShell)**

```powershell
.venv\Scripts\activate.ps1
```

If script execution is blocked:

```powershell
Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned
```

### Deactivate

```sh
deactivate
```

## 3. Dependency Management

### Save Dependencies

```sh
pip freeze > requirements.txt
```

### Restore Dependencies

```sh
pip install -r requirements.txt
```

## 4. `.gitignore` (Required)

Add at minimum:

```gitignore
.venv/
__pycache__/
*.pyc
.env
```

## 5. VS Code Setup

### Install Extensions

```sh
code --install-extension ms-python.python
code --install-extension ms-python.black-formatter
```

> Debugger, IntelliSense, and linting are included.

### Select Interpreter (Important)

```text
Ctrl + Shift + P
→ Python: Select Interpreter
→ Choose the interpreter inside .venv
```

> VS Code auto-detects `.venv` if it exists.

## 6. Running from the Command Line

### Simple

```sh
python main.py
```

### Recommended (Explicit)

```sh
source .venv/bin/activate
python main.py
```

## 7. VS Code Run & Debug

### Run (No Debugger)

```text
Ctrl + Shift + B
Ctrl + F5
```

### Debug

```text
F5
```

> Uses the selected `.venv` interpreter automatically.
