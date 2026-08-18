# Kadro — Gesture Photo Booth

Photo booth berbasis gesture control. Kamera web langsung, tanpa backend, tanpa install.

**Live demo:** https://gesture-booth-two.vercel.app

## Cara Pakai

1. Buka link di **Chrome/Safari** (HP atau desktop) — kamera butuh HTTPS, jadi jangan buka dari in-app Telegram
2. Klik **Nyalain Kamera**, izinkan akses kamera
3. Main pakai tangan:

| Gesture | Efek |
|---|---|
| 🤟 **L dua tangan** (jempol + telunjuk siku-siku, jari lain tekuk) | Kotak framing muncul, isi kotak kena efek real-time |
| ✌️ **Peace** (satu tangan, telunjuk + tengah naik) | Foto, masuk ke galeri |

## Fitur

- **Hand-framing** — MediaPipe HandLandmarker deteksi 21 landmark per tangan, 2 tangan
- **Gesture validation** — skor L 0-5 (sudut 90°, jari extended/folded), stabilisasi frame + grace period anti false-trigger
- **Quad anti-bowtie** — 4 titik (thumb + index tip) disortir by angle dari centroid, expanded 1.25x + smoothing
- **Efek dalam kotak** — Blur / Negatif / B&W / Pixel / Off, di-mask polygon (presisi ke kotak miring, bukan bounding box)
- **Photo capture** — peace = shutter, flash, galeri, download semua
- **Debug panel** — fps, jumlah tangan, skor L, status lock

## Teknis

- MediaPipe Tasks Vision (`HandLandmarker`, running mode VIDEO)
- Render loop `requestAnimationFrame` manual (bukan Camera utils)
- Efek: canvas offscreen + `destination-in` mask
- GPU delegate dengan fallback CPU
- Single file `index.html`, zero build, zero dependency selain MediaPipe CDN

## Run lokal

```bash
python3 -m http.server 8080
# buka http://localhost:8080
```

## Roadmap

- Photo strip (4 foto beruntun jadi satu strip ala photobooth)
- Stiker AR di landmark
- Frame template
- Upload backend

---

Dibuat dengan [MediaPipe](https://developers.google.com/mediapipe), inspired by [hand-gesture](https://github.com/jimmywiraarbaa/hand-gesture).
