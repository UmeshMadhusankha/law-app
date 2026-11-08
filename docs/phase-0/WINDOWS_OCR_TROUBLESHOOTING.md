# Free Windows OCR — fixing 'Pdf reading is not supported'

## Why Tesseract failed

A command of the form `tesseract input.pdf output pdf` does **not** read a PDF. Tesseract recognizes images (PNG, JPEG, TIFF, etc.); `pdf` at the end chooses **PDF output**, not PDF input. Always preserve the original PDF.

## Simplest workflow: NAPS2 GUI

1. Download NAPS2 from https://www.naps2.com/download (free Windows app).
2. Open NAPS2; import your original scanned PDF.
3. Click `OCR` and download `English` if prompted.
4. Enable `Make PDFs searchable using OCR` and save a new file (for example `National_Child_Protection_Act_OCR.pdf`).
5. Open the output PDF in Edge; select/copy a legal passage, then compare it against the original image.

**Special case for HRCSL:** The original has an existing but visibly damaged text layer. NAPS2 normally skips text-bearing pages, so simple import/save may not fix this. Use the assistant-generated re-OCR candidate or a tool/workflow that explicitly forces re-OCR, and manually verify legal wording.

NAPS2 docs: https://www.naps2.com/doc/ocr

## Optional command-line after installing NAPS2

Run this from the directory containing the original file; the quotes handle spaces and commas:

```bat
"C:\Program Files\NAPS2\NAPS2.Console.exe" -i "National Child Protection Act, No. 50 of 1998.pdf" -o "National_Child_Protection_Act_OCR.pdf" -n 0 --ocrlang eng
```

If you installed NAPS2 elsewhere, adjust the executable path. The file name must match your actual PDF exactly. For the HRCSL PDF, note the existing-text caveat above.

NAPS2 CLI documentation: https://www.naps2.com/doc/command-line

## Validation checklist

- Does the output open and have all the original pages?
- Is copied text searchable?
- Do section numbers and important legal terms match the original image?
- Are there unreadable snippets or suspicious replacements (`O` vs `0`, `l` vs `1`, missing `not`)?
- Is the OCR result labeled **UNREVIEWED** until text checking is complete?
