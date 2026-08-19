# Island / OPSwat Sandbox — File Download & Execution Test Corpus

Authorized security-research test set for evaluating how the **Island** enterprise browser
and **OPSwat** (MetaDefender multiscanning / CDR / Sandbox) handle downloading and opening
many file types.

All payloads are **benign**: they either launch `calc.exe` (a harmless proof that code ran)
or contain the **EICAR** anti-virus test string (a harmless proof that an engine inspected
content). No real exploit, persistence, callback, or data access is included.

## Batches
- **`batch1_no_manipulation/`** — straightforward files, no evasion. Baseline: what does the
  sandbox catch when nothing is hidden? *(this repo)*
- **`batch2_manipulation/`** — same coverage with sandbox-bypass techniques (obfuscation,
  encoding, polyglots, extension/type confusion, archiving). *(added after batch 1 testing)*

## `batch1_no_manipulation/` layout
| Folder | Files | What it is |
|--------|-------|-----------|
| `01_active_payloads/` | 10 | Real benign `calc.exe` proof-of-execution: Office macros, HTML smuggling, PDF launch action |
| `02_eicar/` | 35 | Raw EICAR string, one file per requested extension — tests content inspection vs. extension trust |
| `03_benign_control/` | 26 | Genuine clean, openable files of every media/text type — control group; diff against these to see what CDR reconstructed |

See `batch1_no_manipulation/BATCH1_INDEX.md` for the per-file test order and expected behavior.

> Use only against systems you are authorized to assess.
