# C / C++ Configuration Guide (GCC / G++ only)

A minimal, cross-platform setup for **C / C++** using **GCC / G++** and **VS Code**.

> [`VS Code C++ docs`](https://code.visualstudio.com/docs/languages/cpp)

## 1. Installation

### Windows

#### Option A: **MSYS2 (UCRT64 – Recommended)**

* Install **MSYS2** from [https://www.msys2.org/](https://www.msys2.org/)
* Open **MSYS2 UCRT64** terminal
* Install toolchain:

```bash
pacman -S --needed base-devel mingw-w64-ucrt-x86_64-toolchain
```

* Add to **Windows PATH**:

```text
C:\msys64\ucrt64\bin
```

#### Option B: **WinLibs (Winget)**

```powershell
winget install BrechtSanders.WinLibs.POSIX.UCRT
# or
winget install BrechtSanders.WinLibs.MCF.UCRT
```

### Linux

#### Ubuntu / Debian

```bash
sudo apt update
sudo apt install build-essential gdb
```

#### Arch Linux

```bash
sudo pacman -S --needed base-devel
```

### macOS

```bash
brew install clang
```

> macOS uses **clang** by default, but the commands below work the same as `gcc/g++`.

## 2. VS Code Setup

* **Install required extension**

```sh
code --install-extension ms-vscode.cpptools
```

* **Optional VS Code configuration**

Create the following files in your project root if you want explicit behavior:

```text
.vscode/
├── tasks.json
├── launch.json
└── settings.json
```

VS Code also works **without these files** using auto-generated defaults.

## 3. Compiling from the Command Line

### C (gcc)

#### Simple (beginner)

```sh
gcc main.c -o main
```

#### Recommended (warnings + debug)

```sh
gcc -Wall -Wextra -g main.c -o main
```

### C++ (g++)

#### Simple (beginner)

```sh
g++ main.cpp -o main
```

#### Recommended (warnings + debug)

```sh
g++ -Wall -Wextra -g main.cpp -o main
```

(Optional standard flag if you want one)

```sh
g++ -std=c++20 -Wall -Wextra -g main.cpp -o main
```

## 4. Using VS Code Tasks (Optional)

If you have a `tasks.json` configured:

```text
Ctrl + Shift + B
```

This runs the configured build command.

## 5. Running the Program

```sh
./main        # Linux / macOS
./main.exe    # Windows
```

## 6. Debugging (F5)

```text
F5
```

* Works automatically with VS Code’s default configuration
* Uses **gdb / lldb**
* Requires compilation with `-g`
