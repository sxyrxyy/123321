# Batch 2 — Manipulation / Bypass Set

Evasion variants targeting the **content-inspection** layer (which Batch 1 showed is beatable),
not the extension/reader policy layer (which blocked `.lnk` and PDF Launch outright).

All payloads benign: `calc.exe` macro (`calc_macro.docm`) or EICAR string.
**Archive password where used: `infected`** (standard malware-sample convention).

## 01_encryption
CDR and most scan engines cannot inspect an encrypted archive's contents without the password.

| File | Contains | Technique | Expected |
|------|----------|-----------|----------|
| encrypted_calc.zip | calc_macro.docm | ZipCrypto, password `infected` | Engine can't scan inside → may pass; user extracts + runs |
| encrypted_calc.7z | calc_macro.docm | **7z AES-256, header/filename encryption (`-mhe=on`)** | Even filenames hidden — strongest; engine sees only opaque blob |
| encrypted_eicar.zip | eicar.txt | ZipCrypto, password `infected` | Tests whether EICAR is caught through encryption |

## 02_nested_archives
Deep nesting / container-in-container to exceed extraction depth or evade Mark-of-the-Web.

| File | Structure | Technique | Expected |
|------|-----------|-----------|----------|
| zip3_calc.zip | zip → zip → zip → calc_macro.docm | 3-level nesting | Tests extraction-depth limit of the scanner |
| calc.iso | ISO9660 (Joliet/RR) containing calc_macro.docm | **ISO container** | Classic MOTW-bypass; mounting on Windows drops the macro doc without MOTW |

## 03_polyglots
One file valid as two types — beats type detection at the content level.

| File | Valid as | Also is | Expected |
|------|----------|---------|----------|
| polyglot_jpeg_zip_calc.jpg | JPEG image | ZIP archive holding calc_macro.docm (unzip it) | Type detection sees image; the macro rides along inside |
| polyglot_jpeg_zip_eicar.jpg | JPEG image | ZIP holding EICAR | Tests archive-in-image content inspection |
| polyglot_gif_html_calc.gif | GIF (GIF89a magic) | HTML smuggling page (drops calc_poc.hta) | If rendered as HTML, runs the smuggle; as `.gif` reads as benign image |

## Test focus
For each: (1) does OPSwat/Island **block or pass** the download, (2) if passed, does the
**inner payload still work** after extraction/mount/rename. The interesting failure is *pass at
download + working payload inside*.
