# Python Configuration Guide

A minimal, cross-platform setup for **Python** using **CPython**, **virtual environments**, and **VS Code**.

> [`Python docs`](https://docs.python.org/3/)
> [`VS Code Python docs`](https://code.visualstudio.com/docs/python/python-tutorial)

## 1. Installation

### Windows

```powershell
winget install --id Python.Python
```

### Linux

#### Ubuntu / Debian

```sh
sudo apt update
sudo apt install python3 python3-pip python3-venv
```

#### Arch Linux

```sh
sudo pacman -S python python-pip
```

### macOS

```sh
brew install python
```

### Verify

```sh
python --version
pip --version
```

> If `python` is not found but `python3` exists, use `python3`.

## 2. Virtual Environments (Required)

**Rule:** Never install packages globally.

### Create

```sh
cd project/
python -m venv .venv
```

### Activate

**Linux / macOS**

```sh
source .venv/bin/activate
```

**Windows (PowerShell)**

```powershell
.venv\Scripts\activate.ps1
```

If blocked:

```powershell
Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned
```

### Deactivate

```sh
deactivate
```

## 3. Dependency Management

### Save

```sh
pip freeze > requirements.txt
```

### Restore

```sh
pip install -r requirements.txt
```

## 4. Create `.gitignore`

## 5. VS Code Setup

### Install Extension

```sh
code --install-extension ms-python.python
code --install-extension ms-python.black-formatter
```

(Formatter and debugger are included.)

### Select Interpreter

```text
Ctrl + Shift + P
→ Python: Select Interpreter
→ Choose the one with .venv
```

## 6. Running from the Command Line

### Simple

```sh
python main.py
```

### Recommended (inside venv)

```sh
source .venv/bin/activate
python main.py
```

## 7. VS Code Configuration (Optional)

Create:

```text
.vscode/
├── settings.json
├── tasks.json
└── launch.json
```

VS Code also works **without these files** using defaults.

## 8. Run & Debug (VS Code)

### Run (no debugger)

```text
Ctrl + F5
```

### Debug

```text
F5
```

## 9. Multiple Python Versions (Windows)

```powershell
py -0
py -3.12
```

Create venv with specific version:

```powershell
py -3.12 -m venv .venv
```

## 10. Backup & Restore

### Backup

* `requirements.txt`
* `.vscode/`
* Source code

### Restore on New System

```sh
git clone <repo_url>
cd <repo_name>

python -m venv .venv
source .venv/bin/activate   # or .venv\Scripts\activate

pip install -r requirements.txt
```

## Finally

```sh
python -m venv .venv
source .venv/bin/activate
python main.py
```
