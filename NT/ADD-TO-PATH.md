# Add to Windows PATH (Windows 10 / 11)

## Method 1: GUI (Safest & Recommended)

### Steps

On Terminal type `sysdm.cpl` -> **Advanced** -> **Environment Variables**

### Choose where to add

| Option          | Scope     | When to use   |
| --------------- | --------- | ------------- |
| **User PATH**   | Only you  | Recommended   |
| **System PATH** | All users | Needs admin   |

### Add the path

1. Select **Path**
2. Click **Edit**
3. Click **New**
4. Paste the directory
   Example:

   ```text
   C:\msys64\ucrt64\bin
   ```

5. Click **OK → OK → OK**

### Apply

* **Restart terminals**
* VS Code needs **restart** to pick it up

### Verify

```powershell
where gcc
where clang-format
```

## Method 2: PowerShell (User PATH – Safe)

### User Path

```powershell
$dir = "C:\msys64\ucrt64\bin"
$path = [Environment]::GetEnvironmentVariable("Path", "User")

if (-not ($path -split ";" | Where-Object { $_ -ieq $dir })) {
    [Environment]::SetEnvironmentVariable(
        "Path",
        "$path;$dir",
        "User"
    )
}
```

#### System Path

```powershell
$dir = "C:\msys64\ucrt64\bin"
$path = [Environment]::GetEnvironmentVariable("Path", "Machine")

if (-not ($path -split ";" | Where-Object { $_ -ieq $dir })) {
    [Environment]::SetEnvironmentVariable(
        "Path",
        "$path;$dir",
        "Machine"
    )
}
```

> Requires **Run as Administrator**
