# C / C++ Configuration Guide (GCC **or** LLVM / Clang)

A **minimal, cross-platform** setup for **C / C++** using **VS Code**, with the option to use **GCC/G++** *or* **LLVM (Clang/Clang++)**.

> [`VS Code C++ docs`](https://code.visualstudio.com/docs/languages/cpp)
## 1. Install a Toolchain

You only need **one** compiler.
You may install **both** if you want to switch.

## Windows

### Option A: **MSYS2 (UCRT64 – Recommended)**

Install [MSYS2](https://www.msys2.org/) → open **MSYS2 UCRT64** terminal.

#### GCC / G++

```bash
pacman -S --needed base-devel mingw-w64-ucrt-x86_64-toolchain
```

#### LLVM / Clang (Optional)

```bash
pacman -S mingw-w64-ucrt-x86_64-clang mingw-w64-ucrt-x86_64-llvm mingw-w64-ucrt-x86_64-lldb
```

Add to **Windows PATH**:

```text
C:\msys64\ucrt64\bin
```

### Option B: **WinLibs (Winget)**

#### GCC / G++

```powershell
winget install BrechtSanders.WinLibs.POSIX.UCRT
# or
winget install BrechtSanders.WinLibs.MCF.UCRT
```

#### LLVM / Clang (Optional)

```powershell
winget install BrechtSanders.WinLibs.POSIX.UCRT.LLVM
```

## Linux

### Ubuntu / Debian

```bash
sudo apt update
sudo apt install build-essential gdb
```

Optional LLVM:

```bash
sudo apt install clang lldb lld
```

### Arch Linux

```bash
sudo pacman -S --needed base-devel
```

Optional LLVM:

```bash
sudo pacman -S --needed clang lldb lld
```

## macOS

```bash
xcode-select --install
```

> macOS ships **clang** by default (`gcc` is an alias).

## 2. VS Code Setup

Install the C/C++ extension:

```sh
code --install-extension ms-vscode.cpptools
code --inatall-extention xaver.clang-format
```

### Setup: clang-format

`Ctrl + ,`

Search : `@ext:xaver.clang-format`
Set `"clang-format.executable": "C:\msys64\ucrt64\bin\clang-format.exe"`

### Setup Compiler Explicitly

`Ctrl + Shift + P` → **C/C++: Edit Configurations (UI)**

Set:

* Compiler Path → `gcc` / `g++` **or** `clang` / `clang++`
* IntelliSense Mode updates automatically

> VS Code works **without any config files** using auto-detection.

## 3. Compiling from the Command Line

### C

```sh
# GCC
gcc main.c -o main

# Clang
clang main.c -o main
```

Recommended:

```sh
gcc   -Wall -Wextra -g main.c -o main
clang -Wall -Wextra -g main.c -o main
```

### C++

```sh
# GCC
g++ main.cpp -o main

# Clang
clang++ main.cpp -o main
```

Recommended:

```sh
g++      -std=c++20 -Wall -Wextra -g main.cpp -o main
clang++  -std=c++20 -Wall -Wextra -g main.cpp -o main
```

## 4. Using VS Code Tasks (Optional)

```text
Ctrl + Shift + B
```

Runs the configured compiler command.

## 5. Running the Program

```sh
./main        # Linux / macOS
./main.exe    # Windows
```

## 6. Debugging (F5)

* Requires compilation with `-g`
* Uses:

  * **gdb** → GCC
  * **lldb** → Clang
