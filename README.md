# CI Path
Shows the PATH environment on CI services that support Powershell.

- [Gitub Actions](https://github.com/johnstevenson/ci-path/actions?query=workflow%3A%22Path+Report%22) - windows, linux, macos
- [Appveyor](https://ci.appveyor.com/project/johnstevenson/ci-path) - windows, linux, macos
- [Travis CI](https://travis-ci.org/johnstevenson/ci-path) - windows only

## Usage
Run the paths.ps1 script from any shell:

- `pwsh -File paths.ps1`
- `powershell -File paths.ps1`

or directly from Powershell itself:
- `.\paths.ps1`

This outputs the path report which compromises the sections described below. Output is shown on screen and also saved to a report file in the `logs` directory.

### Runtime
This section summarizes the runtime and shows the process tree of the current process.

- **Module**: The module or shell running the script.
- **Platform**: Unix (includes macOS) or Win32NT.
- **OSVersion**: The value from `System.Environment.OSVersion`.
- **IsUnixy**: Whether this is a unixy Windows shell (Git bash, cygwin, msys2 etc). This property is only shown on Win32NT.
- **Powershell**: The name and version of Powershell.
- **ReportName**: The report file name, formatted `platform-shell.txt` where plaform is one of linux, mac, or win.


### Path Entries
This section summarizes and lists the directories in the `PATH` environment variable.

- **Entries**: the total number of directory entries, excluding empty values.
- **Valid**: the number of entries that are not missing or duplicated.
- **Missing**: the number of directories that do not exist on the file system.
- **Duplicates**: the number of directories that appear more than once.
- **Characters**: the character length of the `PATH` variable.

The list of directories contains a _Status_ value for each entry (OK, Missing or Duplicate) and is shown in the same order as the `PATH`.


### Commands Found in Path
This section summarizes the commands found in the `PATH` directories.

- **Commands**: the number of commands found.
- **Duplicates**: the number of commands that are found in more than one directory.
- **PermissionErrors**: the number of directories that are inaccessible to the user. This property is only shown in the event of an access issue.

#### Duplicate Commands

If there are any duplicates, the commands are listed in alphabetical order with the full path to the executables shown in `PATH` search order . For example, from `cmd.exe` on Windows, with Git and its Unix tools installed:
```
Duplicate commands (32)
-----------------------
bash                      (2)   C:\WINDOWS\System32\bash.exe
                                C:\Program Files\Git\usr\bin\bash.exe
curl                      (2)   C:\WINDOWS\System32\curl.exe
                                C:\Program Files\Git\mingw64\bin\curl.exe
...
```

### All Commands

This section lists all all the commands found in the `PATH` directories.They are listed in alphabetical order and formatted as per the _Duplicate Commands_ example above. These are not shown on screen, due to the large number of entries, and the location of the report is shown instead. For example:

```
All commands (1104)
-------------------
See: <path>\ci-path\logs\win-cmd.txt

```
