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
