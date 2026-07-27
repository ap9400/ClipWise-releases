# ClipWise

A clipboard manager and AI text assistant for macOS.

This repository hosts the downloads and the automatic-update feed. The source
lives in a separate private repository.

---

## Install

### **[⬇ Download ClipWise](../../releases/latest)**

1. Download `ClipWise-<version>.zip` from the latest release.
2. Unzip it and drag **ClipWise.app** into your **Applications** folder.
3. **Right-click ClipWise.app → Open → Open.**

That's it. Step 3 is only needed the very first time — see below for why.

Requires macOS 14 (Sonoma) or later, on an **Apple Silicon** Mac (M1 or newer).

### Why the right-click on first launch

macOS will say ClipWise "cannot be opened because it is from an unidentified
developer." The app is signed, but not notarized by Apple, and macOS blocks
anything downloaded that isn't.

Right-click → **Open** tells macOS you trust it. You only do this once per Mac.
Double-clicking works normally from then on, and updates install without it.

---

## Updates are automatic

ClipWise checks for a new version once a day and offers it when one appears.
Nothing to download by hand, and no need to come back to this page.

You can turn automatic checks off, or check right now, in **Settings → General**.

Every update is cryptographically signed. ClipWise installs one only if the
signature matches, so an update can't come from anywhere but here.

---

## The offline voice (optional)

ClipWise's **Reader** reads text aloud — select text anywhere and press
**⇧⌃R**, and it reads it back with the current word highlighted.

**It works the moment you install the app**, using the voices built into macOS.
There is nothing extra to download and nothing to set up.

If you want better speech, ClipWise can also use **Kokoro**, a neural
text-to-speech model that runs on your own Mac:

|  | Built-in macOS voices | Kokoro |
| --- | --- | --- |
| Available | Immediately | ~500 MB download |
| Quality | Robotic but clear | Natural |
| Word highlighting | Approximate | Exact |
| Voices | Your installed system voices | 28 English (US & UK) |

### Getting it

**The app does this for you.** Open the Reader, choose **Kokoro**, and it offers
**Set Up Offline Voice** — it tells you the size, shows progress, and installs
it. There's a Remove button in the same place if you change your mind.

You never need to download it from this page. The `tts-runtime-*` releases here
exist so the app has somewhere to fetch it from.

### Once installed

- Runs entirely on your Mac. No account, no API key, no subscription.
- Works with **no internet connection** — the model sits on your disk and
  nothing is ever sent anywhere.
- App updates never re-download it.

It's a separate download rather than part of the app because most people never
open the Reader, and bundling it would mean everyone pays 500 MB for a feature
they may not use.

---

## What's in the releases list

| Tag | What it is | Download it? |
| --- | --- | --- |
| `2.7.0` and similar version numbers | **The ClipWise app** | **Yes** — this is the app |
| `tts-runtime-1.1.0` | Offline voice package | No — the app fetches it for you |

---

## Something wrong?

Please [open an issue](../../issues).
