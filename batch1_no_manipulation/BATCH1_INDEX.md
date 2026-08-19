# Batch 1 — Test Index (no manipulation)

Test order and expected behavior. Payloads are benign (`calc.exe` / EICAR).

## 01_active_payloads
| # | File | Supposed to do | Auto-run? |
|---|------|----------------|-----------|
| 1 | calc_macro.docm | Word VBA `Document_Open` runs `Shell "calc.exe"` | On **Enable Content** |
| 2 | calc_macro.xlsm | Excel VBA `Workbook_Open` runs calc | On **Enable Content** |
| 3 | calc_macro.pptm | PowerPoint VBA runs calc | **No** — needs slideshow/trigger |
| 4 | calc_macro.doc | Binary Word macro carrier (calc) | Static carrier — detect, not guaranteed run |
| 5 | calc_macro.dot | Binary Word template macro carrier | Static carrier |
| 6 | calc_macro.xls | Binary Excel macro carrier | Static carrier |
| 7 | calc_macro.ppt | Binary PowerPoint macro carrier | Static carrier |
| 8 | calc_smuggle.html | HTML smuggling — JS drops an `.hta`/`.bat` that runs calc | Download on click; user runs dropped file |
| 9 | calc_smuggle.htm | Same as above, `.htm` extension | Same |
| 10 | calc_launch.pdf | PDF `/Launch` + JS tries to run calc | Reader-dependent; modern readers block/prompt |

## 02_eicar (35 files)
`eicar.<ext>` — content is the raw EICAR string. Expected: AV/multiscan **flags every one**;
tests whether the extension changes the verdict.

## 03_benign_control (26 files)
Clean, openable files of every media/text type. Expected: **pass clean**, render in Island.
Diff before/after to measure CDR reconstruction.

---
## Result tracker
Filled during the live session.

| File | Downloaded? | Opened/Ran? | Sandbox verdict | Notes |
|------|-------------|-------------|-----------------|-------|
| | | | | |
