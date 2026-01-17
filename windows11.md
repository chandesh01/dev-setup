# Windows Workstation Setup Guide

A structured guide for configuring a clean, high-performance Windows environment suitable for development and creative work on Lenovo Legion/LOQ hardware.

## 01. Preparation & Installation

### 1. Create Bootable Media

* **Download Windows:** obtain a clean ISO from [Massgrave](https://massgrave.dev/).
* **Prepare USB:**
* Download [Ventoy](https://www.ventoy.net/en/index.html).
* Install Ventoy to the USB drive.
* Drag and drop the ISO file onto the USB partition.



### 2. Install & Activate

* **Boot & Install:** Boot from USB (`F12` or `F2`) and install the OS.
* **Activate:** Use the [Massgrave (MAS)](https://massgrave.dev/) script via terminal to activate.

---

## 02. Restore Core Services

*Required if using a debloated ISO or LTSC version lacking the Microsoft Store.*

### Option A: `wsreset` Command

Open **Command Prompt (Admin)** and run:

```cmd
wsreset -i

```

*Allows the system to attempt a background fetch of the Store.*

### Option B: Xbox App Installer (Recommended)

1. Download the **[Xbox App for PC](https://www.xbox.com/en-US/apps/xbox-app-for-pc)** installer.
2. Run the installer to force dependency downloads (Microsoft Store, App Installer frameworks).

---

## 03. Driver Foundation

### 1. Manufacturer Updates (Lenovo)

* **[LSUClient](https://github.com/jantari/LSUClient):** Lenovo System Update Client for fetching drivers without bloat.
* **Lenovo Vantage Commercial:** Enterprise version recommended over consumer version.
* **[Lenovo Legion Toolkit](https://github.com/XKaguya/LenovoLegionToolkit):** Lightweight alternative to Vantage.
* **Legion Space:** Install only if supported.

### 2. GPU Drivers

* **Nvidia:** Install the **Nvidia App** and latest drivers.
* **AMD:** Install chipset/graphics drivers (if applicable).

---

## 04. System Features & Developer Environment

### 1. Enable Optional Features

Enable virtualization support for WSL and Sandbox environments.
 
1. `Win + R` > `ms-settings:optionalfeatures` > `Enter`
    * More Windows Features : To switch advanced features
    * View Features: To switch features.
4. Restart the system.

### 2. Install WSL (Windows Subsystem for Linux)

Open **PowerShell (Admin)**:

**Update Kernel:**

```powershell
wsl --update

```

**Install Default Distribution (Ubuntu):**

```powershell
wsl --install

```

---

## 05. UI & UX Customization

* **[ExplorerPatcher](https://github.com/valinet/ExplorerPatcher):** Restores legacy taskbar and explorer functionality.
* **[Shell](https://nilesoft.org/):** Shell extension for customizing the context menu.

---

## 06. Essential Application Suite

Install **[App Installer (Winget)](https://github.com/microsoft/winget-cli)** from the Store if missing.

1. Windows Camera
2. Windows Calculator
3. Notepad
4. Microsoft PC Manager
5. Windows Terminal
6. Nahimic App
7. Microsoft Journal
8. PowerToys
9. Snipping Tool

---

## 07. More Applications 

### 1. Office Suite

* Download and install Microsoft Office.
* Activate using [Massgrave](https://massgrave.dev/).

### 2. Package Management

* **[UniGetUI](https://github.com/marticliment/WingetUI):** GUI for Winget package management.

### 3. Browsers

Install via Terminal:

```powershell
winget install Google.Chrome
winget install Brave.Brave

```

---

## 08. Security Lockdown

### Enable BitLocker

1. Open **File Explorer**.
2. Right-click `C:` Drive.
3. Select **Turn on BitLocker**.
4. **Important:** Backup recovery key to an external source or cloud storage immediately.
