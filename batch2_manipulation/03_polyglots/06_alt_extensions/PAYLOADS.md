# Alternative Extension Payloads

## PowerShell (.ps1)
✅ Built: `run_calc.ps1` — one-liner `Start-Process calc.exe`

## Screensaver (.scr)
✅ Built: `calc.scr` — cross-compiled from `calc_screensaver.cpp` with MinGW
(`x86_64-w64-mingw32-g++ calc_screensaver.cpp -o calc.scr -static -luser32 -lshell32 -lgdi32 -mwindows`).
PE32+ GUI, runs calc.exe on WM_CREATE. sha256 d1940fd5…

## MSI Installer (.msi)
⏳ Source ready: `calc_installer.wxs` — CustomAction runs `[SystemFolder]calc.exe` after InstallFinalize.
Build with `wixl calc_installer.wxs -o calc.msi` (needs `wixl` + `wixl-data` packages) or on Windows:
`candle.exe calc_installer.wxs -o obj/ && light.exe -out calc.msi obj/*.wixobj`

## Base64-encoded EXE
✅ Built: `pwned.exe.b64` (20,061 bytes) — `base64 -w 76 pwned.exe`. Roundtrip verified byte-identical.
Decode on test system: `base64 -d pwned.exe.b64 > pwned.exe` (certutil: `certutil -decode`).

## Polyglot wrappers
✅ All four artifacts (and calc.msi once built) wrapped in `../batch2_manipulation/03_polyglots/alt_extensions/`:
jpeg+zip variants for each file, plus gif+html variant that decodes the exe client-side.
