# GSoC 2026 — NeuroDyads Pre-Task
### Brain-to-Brain Decoder | ML4SCI

Pre-task submission for the NeuroDyads project (Dr. Evie Malaia & Dr. Brendan Ames).  
This repository contains the full analysis pipeline for simultaneous EEG (hyperscanning) data from a single conversational dyad.

---

## Repository Structure

```
├── NeuroDyads_PreTask_Colab.ipynb   # Full analysis notebook (Parts 1–4)
├── psd_before_after_ica.png          # Part 1: PSD comparison before/after ICA
├── cebra_embedding_3d.png            # Part 2: CEBRA 3D embedding (main + control)
```

---

## Pipeline Overview

### Part 1 — Preprocessing
- Loaded raw 65-channel EEG (EDF format, 250 Hz, EGI HydroCel nets)
- Segmented by DIN1 markers: positive affect (marker 1→2) and negative affect (marker 3→end)
- Removed channel 65 (VREF — vertex reference, not a neural signal)
- Applied ICA (n=20 components, FastICA) for artifact removal

### Part 2 — CEBRA Embedding
- Concatenated both participants into a joint T×128 matrix
- Z-normalised each channel independently
- Trained CEBRA (3D output, offset10-model, 5000 iterations) with affect labels [0=positive, 1=negative]
- Ran shuffled-data control to validate temporal structure

### Part 3 — Embedding Interpretation
- Analysed geometry of learned 3D embedding
- Compared main vs shuffled control results

### Part 4 — Critical Reflection
- Identified the primary limitation specific to this data and pipeline

---

## Requirements

```bash
pip install mne==1.7.0 cebra scikit-learn matplotlib numpy
```

Or run directly in **Google Colab** — the notebook installs all dependencies automatically.

---

## Results Summary

| Metric | Main Model | Shuffled Control |
|--------|-----------|-----------------|
| KNN Decoding Accuracy | 0.999 | 1.000 |
| Positive samples | 36,944 | — |
| Negative samples | 38,487 | — |

---

*GSoC 2026 Application | ML4SCI NeuroDyads*
