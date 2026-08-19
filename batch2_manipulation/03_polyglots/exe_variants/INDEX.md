# EXE Smuggling Variants

Real Windows executable (`pwned.exe` — benign popup showing "PWNED" message) smuggled in polyglots.

| File | Valid as | Also is | Expected |
|------|----------|---------|----------|
| polyglot_jpeg_zip_pwned.jpg | JPEG image | ZIP holding pwned.exe | Type detection sees JPEG; exe rides inside as archive member |
| polyglot_gif_html_pwned.gif | GIF (GIF89a) | HTML smuggling (download link) | As `.gif` reads as image; opened as HTML, user can download and run pwned.exe |

Test: (1) downloads clean past Island/OPSwat, (2) payload is intact after extraction, (3) can the exe be extracted and executed.
