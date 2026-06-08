# 🎛️ AI-DJ

> **Fourier-powered song order recommender, auto-mixer, vocal/beat separator and 3-band EQ — all running in the browser with zero dependencies.**

![License](https://img.shields.io/badge/license-MIT-1db954?style=flat-square)
![Stack](https://img.shields.io/badge/stack-Vanilla%20JS%20%2B%20Web%20Audio%20API-1db954?style=flat-square)
![Dependencies](https://img.shields.io/badge/dependencies-none-1db954?style=flat-square)

---

## ✨ Features

| Feature | Description |
|---|---|
| 🧠 **AI Song Order** | Greedy nearest-neighbour seed → 3× simulated annealing → 2-opt local search for near-optimal playlist ordering |
| 🎚️ **Auto Mix** | Fully automatic DJ set with configurable per-track duration, start offset and crossfade length |
| 📊 **Fourier Intelligence Engine** | Live FFT visualisation, spectral centroid, dominant frequency, band energy and mood detection |
| 🎤 **Stem Separation** | Real-time vocal / beat isolation via Web Audio biquad filter chains — no server required |
| 🎛️ **3-Band EQ + Presets** | Bass / Mid / Treble parametric shelves with one-click presets (Club, Acoustic, Electronic, Vocal…) |
| 🔊 **Sound FX** | Reverb, Echo, Sweep↓, Sweep↑, Stutter, Scratch, Bitcrush, Flanger |
| 🔬 **Transition Analysis** | Per-pair BPM delta, spectral similarity score and plain-English transition verdict |
| 📈 **Similarity Matrix** | ML cosine-style feature distance displayed as ranked percentage bars |

---

## 🚀 Quick Start

No build step. No npm. No server.

```bash
git clone https://github.com/your-username/ai-dj.git
cd ai-dj
open index.html          # macOS
# — or —
start index.html         # Windows
# — or serve with any static file server:
npx serve .
```

Then:

1. Drop MP3 / WAV / OGG / FLAC files onto the **Load Songs** zone
2. Wait for the green dots (analysis complete)
3. Click **Analyze & Recommend Optimal Play Order**
4. Hit a track in the playlist to play, or enable **Auto Mix** to let the AI DJ

---

## 🧬 How the AI Works

### Feature Extraction (Fourier Transform)
Each audio file is decoded into raw PCM samples. A Hann-windowed FFT frame is computed from the middle of the track to extract:

- **BPM** — onset detection via short-time energy peaks
- **Spectral Centroid** — weighted mean frequency (brightness)
- **Energy** — RMS of a 4-second window
- **Key** — estimated from centroid bucket + energy ratio
- **Mood** — heuristic label (Energetic / Bright / Dark Bass / Calm / Balanced)

### Playlist Optimisation
The ordering pipeline runs in three stages:

```
Greedy (BPM-sorted seed)  →  Simulated Annealing (×3 independent runs)  →  2-opt Sweep
```

The **cost function** is a weighted Euclidean distance across the feature vector `[BPM/200, energy, centroid]`. The annealing schedule scales iterations to `O(n²)` so larger libraries still converge near the global optimum.

### Crossfade Engine
Two AudioBufferSourceNodes (Deck A / Deck B) are routed through independent GainNodes into a shared EQ → master chain. Auto Mix schedules:

- `setTimeout` at `(segmentDuration − xfadeDuration)` → exponential gain ramp on both decks
- `setTimeout` at `segmentDuration` → swap decks, recurse to next track

---

## 🗂️ Project Structure

```
ai-dj/
└── index.html      # Entire app — HTML + CSS + JS in one self-contained file
```

All audio processing uses the browser-native **Web Audio API**. No external libraries, frameworks or backend calls are made.

---

## 🎛️ Auto Mix Settings

| Control | Default | Description |
|---|---|---|
| Segment Duration | 20 s | How many seconds of each track to play |
| Start Offset | 10 s | Skip into the track before playback begins |
| Crossfade | 3 s | Overlap duration between outgoing and incoming tracks |

---

## 🌐 Browser Support

| Browser | Support |
|---|---|
| Chrome / Edge 88+ | ✅ Full |
| Firefox 76+ | ✅ Full |
| Safari 14.1+ | ✅ Full |
| Mobile Chrome / Safari | ✅ Full |

Requires `AudioContext`, `AudioBuffer` and `createBiquadFilter` — universally available in all modern browsers.

---

## 📐 Signal Chain

```
File → decodeAudioData → BufferSource (Deck A / B)
         ↓
    GainNode (crossfade)
         ↓
  LowShelf (Bass EQ)  →  Peaking (Mid EQ)  →  HighShelf (Treble EQ)
         ↓
  LowPass (Sweep FX)  →  HighPass (Sweep FX)
         ↓
    Master GainNode
         ↓
    AnalyserNode  →  AudioContext.destination
```

Stems bypass the main chain and run through dedicated filter → gain → analyser paths.

---

## 📄 License

MIT — do whatever you like, attribution appreciated.

---

<div align="center">
  <sub>Built with the Web Audio API · No dependencies · Runs entirely in the browser</sub>
</div>