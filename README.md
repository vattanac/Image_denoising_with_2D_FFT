# 📡 Image Denoising with 2D Fast Fourier Transform

> **Study Guide — February 2026**
> Lecturer: Dr. Veng Sotheara
> Subject: Math of Data Science · Course: Applications of FFT · Track C: Image & 2D FFT

---

## Overview

An interactive HTML study guide that explains how the **2D Fast Fourier Transform (FFT)** can be used to denoise images. The guide covers the full pipeline from theory to results, with embedded interactive demos and concept notes at every step.

The project demonstrates that by transforming an image into the frequency domain, separating noise (high frequencies) from content (low frequencies), and applying a filter mask, we can reconstruct a cleaner image — improving PSNR from **17.65 dB** (noisy) to **23.28 dB** (denoised).

---

## Files

| File | Description |
|---|---|
| `FFT_Study_Guide_Updated02.html` | Main study guide — all 8 sections |
| `w1.html` | Concept note: Why clip & convert to uint8? |
| `w2.html` | Concept note: Why DFT, not FFT? |
| `w3.html` | Concept note: Why work on grayscale images? |
| `a4.html` | Demo: Image 2D FFT — How images become frequencies |
| `a5.html` | Demo: Full denoising pipeline visualization |
| `a6.html` | Demo: Filter design — Ideal vs Gaussian comparison |
| `a7.html` | Demo: Effect of filter cutoff frequency |
| `a8.html` | Demo: PSNR vs cutoff frequency analysis |
| `a.html` | Demo: Image sharpening with high-pass filter |
| `b1.html` | Demo: Why convert to frequencies? |
| `b2.html` | Demo: What each frequency looks like |
| `b3.html` | Demo: fftshift — move zero-frequency to center |
| `b4.html` | Demo: Filter design — Ideal vs Gaussian vs Butterworth |
| `b5.html` | Demo: Applying the filter mask |
| `b6.html` | Demo: ifftshift — shift back before inverse FFT |
| `b7.html` | Demo: Inverse FFT — back to pixel space |
| `b8.html` | Demo: Take the real part |
| `b9.html` | Demo: Clip and convert to uint8 |
| `b10.html` | Demo: Apply 2D FFT to the noisy image |
| `01.html` | Demo: Global operation limitation |
| `02.html` | Demo: Noise type dependency limitation |
| `03.html` | Demo: Detail vs noise trade-off |
| `04.html` | Demo: Manual tuning required |

---

## Study Guide Sections

### ① Introduction
- Why convert to frequencies?
- What FFT does and why it matters
- Fast Fourier Transform vs. Discrete Fourier Transform

### ② Theory — How Does FFT Actually Work?
- Images as 2D grids of brightness values
- The 1D DFT formula: `X[k] = Σ x[n] · e^(−j2πkn/N)`
- Extending to 2D images (row-wise then column-wise)
- What low, high, and noise frequencies look like in the spectrum
- Computational advantage: O(N⁴) → O(N² log N)

### ③ Pipeline — The 8-Step Denoising Process
1. Apply 2D FFT — `np.fft.fft2()`
2. fftshift to center — `np.fft.fftshift()`
3. Design filter mask (type + cutoff frequency)
4. Multiply spectrum by filter mask
5. ifftshift to shift back — `np.fft.ifftshift()`
6. Apply Inverse FFT — `np.fft.ifft2()`
7. Take the real part — `np.real()`
8. Clip to [0, 255] and convert — `np.clip(...).astype(np.uint8)`

### ④ Filters — Ideal vs. Gaussian
- Ideal low-pass filter: sharp cutoff, causes Gibbs ringing artifacts
- Gaussian low-pass filter: smooth cutoff, no ringing, preferred in practice
- Butterworth filter: tuneable sharpness between Ideal and Gaussian

### ⑤ Results — Did It Actually Work?
- Metric: PSNR (Peak Signal-to-Noise Ratio)
- Test image: 256×256 synthetic image with Gaussian noise (σ = 0.15)
- Noisy PSNR: **17.65 dB**
- Denoised PSNR: **23.28 dB** (Gaussian filter, optimal cutoff = 45)

### ⑥ Limitations
- Global operation — cannot adapt to local regions
- Noise type dependency — works best for Gaussian, not salt-and-pepper
- Detail vs noise trade-off — no single cutoff is perfect everywhere
- Manual tuning required — no automatic adaptive cutoff

### 🔪 Sharpening
- High-pass filter application for image sharpening
- Inverse of denoising: amplify high frequencies instead of suppressing them

### ❓ Q&A
- Common exam and discussion questions with answers

---

## Tech Stack

- **Language:** Python
- **Libraries:** NumPy, Matplotlib, OpenCV
- **Key functions:** `np.fft.fft2`, `np.fft.fftshift`, `np.fft.ifftshift`, `np.fft.ifft2`, `np.real`, `np.clip`
- **Frontend:** Vanilla HTML/CSS/JS with KaTeX for math rendering

---

## How to Use

1. Clone or download the repository
2. Open `FFT_Study_Guide_Updated02.html` in any modern browser
3. Navigate sections using the top navigation bar
4. Click **View Demo** buttons to open interactive demos in a modal
5. Click **Why** buttons to open concept notes explaining the reasoning behind each step

> **Note:** All demo files (`a*.html`, `b*.html`) and concept notes (`w*.html`) must be in the same folder as the main guide file for the modal links to work.

---

## Key Concepts

| Term | Meaning |
|---|---|
| FFT | Fast Fourier Transform — efficient algorithm to compute the DFT |
| DFT | Discrete Fourier Transform — the mathematical definition of the transform |
| IFFT | Inverse FFT — converts frequency-space back to pixel-space |
| fftshift | Moves zero-frequency component from corners to center of spectrum |
| ifftshift | Reverses fftshift — must be applied before IFFT |
| Low-pass filter | Keeps low frequencies (smooth content), blocks high frequencies (noise) |
| PSNR | Peak Signal-to-Noise Ratio — measures image quality in decibels |
| Cutoff frequency | Threshold that separates kept frequencies from blocked ones |

---

## Results

```
Input:   Noisy image   →  PSNR: 17.65 dB
Output:  Denoised image →  PSNR: 23.28 dB
Filter:  Gaussian low-pass, cutoff = 45
Image:   256×256 grayscale, Gaussian noise σ = 0.15
```

---

*Study Guide · Math of Data Science · February 2026*
