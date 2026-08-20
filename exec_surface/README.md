# exec_surface - MsgBox-only PoC set (authorized assessment, benign)

All files pop a PWNED message box only. No process execution, no Shell, no payloads.

| File | Interpreter (signed) | Direct run |
|---|---|---|
| pwned.vbs | wscript.exe | double-click |
| pwned.js | wscript.exe | double-click |
| pwned.hta | mshta.exe | double-click |
| pwned.bat | cmd.exe -> msg.exe | double-click |
| pwned.ps1 | powershell.exe | powershell -ExecutionPolicy Bypass -File pwned.ps1 |

polyglot_jpeg_zip_msgbox.jpg = all five in the JPEG+ZIP wrapper (offsets patched),
SHA256 f8fc467e3e3dbd816d9569fafa88a937cb7f3a6df6a0bd7fcd793bdd237ca224.

Test axes: (1) does Island allow direct download per extension, (2) does the
polyglot download as image, (3) which interpreters pop the box without
CrowdStrike intervening. Record 3-state per cell: blocked-download /
blocked-exec / ran.

## Native EXE set (MessageBoxW only, no Shell/exec)

| File | Build | Size | SHA256 (first 16) |
|---|---|---|---|
| pwned64.exe | x64 GUI, static | 320030 | f696d84fbe4de467 |
| pwned32.exe | x86 GUI, static | 299564 | 7cf49015a3550245 |
| pwned_console64.exe | x64 console, static | 297586 | 5af44678c8ab566e |
| pwned_min64.exe | x64 nostdlib, stripped, single import | 3584 | 3a1dc211325ed692 |

polyglot_jpeg_zip_msgboxexe.jpg = all four in the JPEG+ZIP wrapper (offsets patched),
SHA256 776c5dd79df0206122497215918786eb6e58fa61776c345d05d1ec08a4b7824d.

Yesterday's baseline: a smuggled unsigned pwned.exe was blocked by CrowdStrike +
SmartScreen at execution. These four vary compiler profile / subsystem / size to
map what the endpoint ML actually keys on. All benign: single MessageBoxW call.
