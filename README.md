# YTDISK — browser edition

**English** · [العربية](README.ar.md)

A file goes into a 4K test-pattern video, the video comes back out, and the bytes are identical. No server, no upload, no account.

This is a browser rebuild of the Python tool [`ahmedfox1/YtDisk`](https://github.com/ahmedfox1/YtDisk). The encoder, Reed–Solomon codec, scrypt/AES-GCM layer, MP4 muxer/demuxer, and UI all run locally in the tab.

## Run it

Open `index.html` directly in Chromium (Chrome, Edge, Brave). The page is built to work from `file://`.

If your browser restricts local file access, serve the folder:

```sh
cd ytdisk
python3 -m http.server 8080
```

Then open `http://localhost:8080/`.

**Requirements:** WebCodecs with H.264 encode/decode. 4K is used when supported; otherwise the UI falls back to 1080p. Chrome/Edge on desktop are the safest targets.

## Use it

1. **Pack** — choose a file, pick cell size / error correction / output, add an optional password, and render the MP4. Download it.
2. Upload the video to YouTube Studio as **Unlisted** and wait for **2160p** to finish processing.
3. Download the 2160p MP4 (for example with `yt-dlp`).
4. **Unpack** — choose that MP4 in the page, enter the password if one was used, and download the original file.

The self-check button decodes the video in the page and compares the SHA-256 before you upload it.

## Format

The video format follows the Python tool:

- 1920 × 1080 logical cells, output 3840 × 2160 or 1920 × 1080, 30 fps.
- 4 px or 8 px cells; 30 header frames followed by data frames.
- Reed–Solomon over GF(256), `prim = 0x11d`, `fcr = 0`, `N = 255`, 32/64/0 parity bytes, interleaved codewords.
- Optional AES-256-GCM with scrypt (`N = 2^15, r = 8, p = 1`).
- SHA-256 of the original bytes stored in the packed header and verified on decode.

## Files

| Path | Purpose |
| --- | --- |
| `index.html` | Page structure and content |
| `css/app.css` | The broadcast-bench visual system |
| `js/i18n.js` | English / Arabic copy and RTL switching |
| `js/app.js` | UI wiring, options, progress, self-check |
| `js/engine.js` | Frame capacity, packed header, renderer/reader |
| `js/rs.js` | Reed–Solomon encode/decode |
| `js/scrypt.js` | scrypt + AES-GCM |
| `js/mp4.js` | MP4 muxer and progressive demuxer |
| `js/pipeline.js` | Encode/decode pipeline using WebCodecs |
| `tests/` | Node and headless-Chromium checks |
| `PRODUCT.md` | Product truth and constraints |
| `DESIGN.md` | Design system and visual rules |

## Tests

```sh
node tests/rs.test.js
node tests/cdp.mjs --url "file://$PWD/index.html" --wait-ms 3500 --eval-file tests/ui-e2e.js
```

`rs.test.js` compares the JS codec byte-for-byte with Python `reedsolo` vectors and checks error correction. `ui-e2e.js` drives the real page controls: pick a file, render, self-check, decode, and compare bytes, with and without a password. The headless driver needs `chromium-browser` on `PATH`.

## Limits and honesty

This is an educational demonstration, not storage. A re-encode, a regional change, or a takedown can destroy the payload. Uploading data disguised as video may violate a platform's terms. Keep uploads unlisted, use a test channel, and keep a real copy of anything you care about. A gigabyte is roughly 42 minutes of 4K video, and upload/download takes longer than that.

## Credit

Original concept and Python implementation: [ahmedfox1/YtDisk](https://github.com/ahmedfox1/YtDisk). This browser edition keeps the format and the project's measured proof table, and rebuilds the tool for a single local tab.
