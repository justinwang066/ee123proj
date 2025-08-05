# ee123proj
EE 123 Project Spring 2025
Presentation Link: <br>
https://docs.google.com/presentation/d/1tuWr2FpA2kqVDZ9N4id5-gP0BMg3bl-WuwBbhdZ0QCg/edit?usp=sharing

# 🛠️ Tool Condition Monitoring via Signal Processing

This project applies time-frequency analysis to monitor the condition of cutting tools used in milling operations. Using acoustic emission (AE), vibration, and current sensor data, we perform Short-Time Fourier Transform (STFT) to extract spectral features that can help classify the severity of tool wear (e.g., Good, Slight, Severe).

---

## 📁 Contents
- `main.ipynb` — Core notebook containing STFT computation, signal visualization, and band energy analysis.
- `audio_features.csv` — Raw sensor signals (time-domain).
- `metadata.csv` — Flank wear values (`VB`) per case.
- `all_features.csv` — Pre-computed features per signal.
- STFT spectrograms and band ratios per sensor.

---

## 🧠 Goal

To classify tool wear severity based on changes in signal frequency content over time using **windowed FFTs** and **energy-band features**.

---

## 📊 Methodology

### 1. **Signal Input**
Raw signals are collected from six sensor types:
- `AE_spindle`, `AE_table` (acoustic emission)
- `vib_spindle`, `vib_table` (vibration)
- `smcDC`, `smcAC` (current)

### 2. **STFT Computation**
The signal is segmented, windowed (e.g., Kaiser), and transformed using FFT to generate a **time-frequency spectrogram**:


### 3. **Spectrogram Normalization**
Each segment's FFT magnitude is normalized and converted to dB:


### 4. **Band Energy Extraction**
Frequency bands (e.g., low: 0–30 Hz, mid: 30–90 Hz, high: 90–125 Hz) are defined per sensor. Energy per band is computed by summing power:


### 5. **Band Ratios**
Relative energy is computed:


These **band ratios** serve as features for classifying tool condition.

---

## 🏷️ Tool Wear Labels

Based on the flank wear value `VB`, cases are labeled:

- `Good`
- `Slight`
- `Average`
- `Heavy`
- `Severe`
- `Failure`

Defined using:

```python
bins = [0, 20, 40, 70, 100, 150, 1000]
labels = ["Good", "Slight", "Average", "Heavy", "Severe", "Failure"]
