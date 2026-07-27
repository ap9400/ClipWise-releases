# ClipWise — Downloads

Public downloads and the automatic-update feed for **ClipWise**, a clipboard
manager and AI text assistant for macOS. The source lives in a separate private
repository; this one exists so the app can fetch its own updates.

## Download

**[Download the latest ClipWise release →](../../releases/latest)**

Grab `ClipWise-<version>.zip`, unzip it, and drag **ClipWise.app** to your
Applications folder. That is the whole install — you do not need anything else on
this page.

> **The first launch needs one extra step.** macOS will say ClipWise "cannot be
> opened because it is from an unidentified developer." That is expected: the app
> is signed but not notarized by Apple.
>
> **Right-click ClipWise.app → Open → Open.**
>
> Only needed once, on each Mac. Every update after that installs on its own.

Requires macOS 14 (Sonoma) or later.

## Updates are automatic

ClipWise checks for updates once a day and offers them when they appear. You can
turn that off, or check immediately, in **Settings → General**. Updates are
cryptographically signed, and ClipWise installs one only if the signature
matches.

## About the two kinds of release here

Releases on this page come in two flavours. **You only ever download the first.**

| Tag | What it is | Do I download it? |
| --- | --- | --- |
| `2.7.0` (a version number) | The ClipWise app | **Yes** — this is the app |
| `tts-runtime-1.0.0` | The offline voice package | No — the app fetches it for you |

### Why the voice package is separate

ClipWise's **Reader** reads text aloud. It works the moment you install the app,
using the voices built into macOS.

It can also use **Kokoro**, a neural text-to-speech model that sounds
considerably more natural and reports exact per-word timing, so the highlight
follows the speech precisely. Kokoro brings its own Python runtime and model
weights — a few hundred megabytes — so it is not bundled into the app. Instead:

- The app stays small, and app updates stay small.
- You are asked before anything is downloaded, and told the size first.
- If you never use the Reader, you never download it.

To install it: open the Reader, pick **Kokoro**, and choose **Set Up Offline
Voice**. ClipWise downloads and installs it, and there is a Remove button in the
same window.

Once installed it runs entirely on your Mac. It needs no account, no API key, and
no internet connection — the model is on your disk and nothing is sent anywhere.

Currently published for **Apple Silicon** Macs only.

## Something wrong?

Please open an issue on this repository.
