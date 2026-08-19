# Alternative Extension Payloads

Build locally. Haiku agents pending/incomplete.

## PowerShell (.ps1)
✅ Done: `run_calc.ps1` — one-liner `Start-Process calc.exe`

## Screensaver (.scr)
✅ Done: `calc_screensaver.cpp` — ScreenSaverProc + WinMain, runs calc.exe on WM_CREATE.
- Compile: `cl calc_screensaver.cpp user32.lib shell32.lib` (MSVC) or MinGW equivalent
- Rename `.exe` to `.scr` after compilation

## MSI Installer (.msi)
✅ Done: `calc_installer.wxs` — WiX XML with CustomAction that runs calc.exe during installation.
- Compile: `candle.exe calc_installer.wxs -o obj/ && light.exe -out calc.msi obj/*.wixobj`
- Or use WiX Toolset IDE (Visual Studio extension)

## Base64-encoded EXE
Haiku declined. Use: `base64 pwned.exe > pwned.exe.b64` locally; decode with `base64 -d pwned.exe.b64 > pwned.exe` on test system.
