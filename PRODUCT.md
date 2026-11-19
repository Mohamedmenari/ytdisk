# Product: YTDISK (browser edition)

**One line:** Turn any file into a 4K test-pattern video, then turn the video back into the exact same bytes — entirely in the browser.

## What it is

YTDISK is a browser rebuild of the Python CLI `ahmedfox1/YtDisk`. It paints a file into a high-contrast, error-corrected video that can be uploaded to a video platform, downloaded again, and decoded back to the original file. It is a demonstration of Reed–Solomon coding, hashing, and WebCodecs, not a storage service.

The page has two modes:

1. **Pack** — choose a file, set cell size / error correction / output resolution, optionally add a password, render an H.264 MP4, download it, and run a self-check.
2. **Unpack** — choose the downloaded MP4, read the header, optionally enter the password, repair errors, verify SHA-256, and download the original file.

## Who it is for

- People curious how much data a video can carry and how error correction survives re-encoding.
- Students and presenters who need a concrete, visual ECC demo.
- Developers testing browser video encode/decode pipelines.

## Jobs to be done

- "Show me a file becoming a video and coming back unchanged."
- "Let me try different cell sizes / parity levels and see the capacity and robustness trade-off."
- "Let me protect the payload with a password without sending it anywhere."
- "Tell me honestly when the video is damaged, truncated, encrypted, or unsupported."

## Product truth

### Format

- Logical frame: **1920 × 1080** cells; output **3840 × 2160** (default) or **1920 × 1080**.
- Cell: **4 px** (denser, default) or **8 px** (sturdier).
- 30 fps; keyframe every 30 frames; 30 Mbps at 4K, 10 Mbps at 1080p.
- **30 header frames** first (block 16, nsym 64, 573-byte payload) carrying a JSON header: `magic`, `v`, `name`, `size`, `sha256`, `payload_len`, `codewords`, `block`, `nsym`, `frames`, `encrypted`.
- Header is packed into **765 bytes**; data follows as interleaved Reed–Solomon codewords.
- RS: GF(256), primitive `0x11d`, generator 2, fcr 0, `N = 255`; parity **32** (standard), **64** (double), or **0** (raw). Interleaved exactly like the Python tool.
- Optional encryption: **AES-256-GCM** with a key derived by **scrypt (N = 2^15, r = 8, p = 1)**; layout `salt(16) | nonce(12) | ciphertext + tag`.
- Integrity: SHA-256 of the original bytes is in the header and is rechecked after decode.

### Capacity, as measured in the original project

- 4K, 4×4 cells, 32 parity: **415 KB/s**, 0% loss in the simulated YouTube pass.
- 1080p, 8×8 cells, 32 parity: **104 KB/s**.
- 4K, 4×4, 4 grey levels: 830 KB/s but 27.9% of bytes lost.
- 1 GB ≈ **42 minutes** of 4K video.

These are the numbers shown in the proof table; they are inherited from the upstream tests, not invented for the website.

### Hard constraints

- **No backend, no upload, no account.** All encoding, decoding, hashing, and cryptography run in the tab.
- Requires **WebCodecs** and an H.264 encoder/decoder. 4K support is detected; if unavailable the UI falls back to 1080p.
- Decode accepts **MP4 only** (H.264/AVC). WebM/MKV are out of scope.
- Files over **300 MB** are refused by the UI to keep one tab from exhausting memory.
- The page must work from `file://` as well as a static host: no bundler, no modules, no CDN, no external fonts.
- Bilingual **English / Arabic** with a real RTL layout; the default follows `navigator.language`.

### Non-goals / risks (must stay visible)

- Not a backup or a storage service. A re-encode, region change, or takedown can destroy the payload.
- Uploading data disguised as video may violate a platform's terms. Use unlisted videos on a test channel.
- Never keep the video as the only copy.
- Do not promise recovery beyond the parity budget; say plainly when repair fails.

## Success criteria

- A file round-trips **byte-identically** through Pack → MP4 → Unpack, with and without a password.
- The self-check reports the same result as a real Unpack.
- Wrong password, missing header, truncated video, damaged payload, and unsupported codec each produce a specific, actionable message.
- Keyboard, screen reader, and RTL users can complete both flows.
- No horizontal overflow at 390 px, 900 px, and 1440 px.
- The page explains the cost and the risk before the tool, without hiding the tool below a marketing wall.

## Voice and copy

Plain, exact, instrument-like. Short declaratives. Say "file", "video", "frames", "parity", "repair", not "magic" or "unlimited". Arabic is a first-class translation with the same register, not a mechanical gloss. Avoid em-dash-heavy prose; prefer periods and colons. No exclamation marks, no growth-hype, no claims of reliability the tool cannot keep.

## Localization

- All UI strings live in `js/i18n.js` under `data-i18n` keys.
- Numbers, hashes, resolution, timecode, and technical readouts stay LTR-isolated inside the RTL page.
- Arabic uses Almarai with looser leading; display tracking is removed in RTL.
- The language choice persists in `localStorage`; `ytdisk:lang` is dispatched so dynamic content can re-render.
