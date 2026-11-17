# QR Credential Generator

Browser tool that makes QR / Data Matrix / PDF417 codes for Rosslare **AY-x30QR** readers (AY-M30QR, AY-H30QR) in the AxTraxPro **"Simple text"** format, for use with Qumulex or AxTraxPro.

Everything runs locally in the browser. No data leaves the page.

## What it does

- **Single:** enter a facility code and card number to preview the code, then download it as a PNG or a one-code PDF.
- **Range:** queue up N sequential cards at one facility code (e.g. 25 visitor passes), with an optional label prefix.
- **Paste list:** one `facility,card[,label]` per line.
- **Download PDF:** a US Letter sheet of all queued codes, each labeled with FC / card / content.
- **Download CSV:** the same list to use for enrolling credentials.
- **Decode a number:** turn a QR's number back into a facility code and card number.

## Encoding

QR content = `facility × 65536 + card`, written as a decimal number. The reader adds the Wiegand parity bits.

| Format | Facility | Card | Reader DIP 1 | Reader DIP 2 |
|---|---|---|---|---|
| 26-bit | 0–255 | 0–65,535 | OFF | OFF |
| 34-bit | 0–65,535 | 0–65,535 | ON | OFF |

Example: facility 100, card 12345 → `6565945`.

## Reader notes (AY-x30QR)

- The wiring is **not** the usual Rosslare colors: blue-white = D1, green-white = D0, white = Card Present (not D1).
- Power-cycle the reader after changing its DIP switches.
- An out-of-the-box unit was observed sending 34-bit.
- QR is confirmed working. 1D barcodes do not read. Data Matrix and PDF417 have not been tested on the reader yet.
- Print at 100% / Actual size. Codes about 3 × 3 cm work well; scan at 5–10 cm.

## Hosting

This is a static site, a single `index.html`. It's served with GitHub Pages from the `main` branch root.

## Third-party libraries (MIT, loaded from jsDelivr, pinned with SRI hashes)

- [bwip-js](https://github.com/metafloor/bwip-js) 4.11.4 — barcode rendering
- [jsPDF](https://github.com/parallax/jsPDF) 4.2.1 — PDF output

The page needs internet access to cdn.jsdelivr.net to load these.
