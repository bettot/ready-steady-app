# Vendored libraries

Local copies so the app has no CDN dependencies and keeps working regardless of
anyone else's uptime. Loaded lazily — nothing here is fetched until a scan button
is tapped.

| Path | What | Version | Licence | Source |
|---|---|---|---|---|
| `zxing/es/reader/index.js` + `zxing/es/share.js` + `zxing/zxing_reader.wasm` | Barcode reading (ZXing-C++ compiled to WebAssembly) | zxing-wasm 3.1.2 | MIT (bindings), Apache-2.0 (zxing-cpp) | https://www.npmjs.com/package/zxing-wasm |
| `tesseract/tesseract.min.js` + `tesseract/worker.min.js` | OCR engine JS API + worker | tesseract.js 6.0.1 | Apache-2.0 | https://www.npmjs.com/package/tesseract.js |
| `tesseract/tesseract-core-simd-lstm.wasm.js`, `tesseract/tesseract-core-lstm.wasm.js` | Tesseract 5 compiled to WebAssembly (SIMD and non-SIMD builds; the worker picks one) | tesseract.js-core 6.1.2 | Apache-2.0 | https://www.npmjs.com/package/tesseract.js-core |
| `tesseract/lang/eng.traineddata.gz` | English "fast" recognition model | tessdata_fast | Apache-2.0 | https://github.com/tesseract-ocr/tessdata_fast |

Licence texts: `zxing/LICENSE.txt`, `tesseract/LICENSE-core.txt`,
`tesseract/worker.min.js.LICENSE.txt`.

To update a library: download the new npm tarball, replace the files above,
keep the same filenames and this table current.
