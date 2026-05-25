# ppg-arrhythmia-classifier
A machine learning pipeline for cardiac arrhythmia detection using real ECG signals from the MIT-BIH Arrhythmia Database. Built as a biomedical engineering application targeting cardiac monitoring and wearable sensing devices.

## Results

- **92% classification accuracy** across 5 cardiac arrhythmia types
- Trained and validated on **100,012 labeled heartbeat segments** from 48 patient recordings
- Strong recall on Ventricular arrhythmias (94%) — the most clinically critical beat type

## Beat Types Classified

| Label | Type | F1-Score |
|-------|------|----------|
| N | Normal Sinus Rhythm | 0.86 |
| A | Atrial Premature Beat | 0.88 |
| V | Ventricular Premature Beat | 0.94 |
| L | Left Bundle Branch Block | 0.95 |
| R | Right Bundle Branch Block | 0.95 |

## Project Structure
ppg-arrhythmia-classifier/
├── data/
│   ├── mitdb/          # Raw MIT-BIH recordings (downloaded via wfdb)
│   └── processed/      # Segmented features and labels
├── models/
│   └── arrhythmia_classifier.pkl
├── notebooks/
│   ├── 01_data_exploration.ipynb
│   ├── 02_preprocessing.ipynb
│   ├── 03_feature_extraction.ipynb
│   └── 04_model_training.ipynb
├── src/
└── README.md

## Pipeline Overview

1. **Data** — Downloaded 48 patient ECG recordings from PhysioNet MIT-BIH Arrhythmia Database
2. **Preprocessing** — Segmented signals into 360-sample windows centered on each R-peak, normalized across patients
3. **Feature Extraction** — Extracted 15 clinically meaningful features per beat across time domain, morphology, and energy categories
4. **Modeling** — Trained a Random Forest classifier with class balancing to handle real-world beat distribution imbalance
5. **Evaluation** — Validated on held-out 20% test set with per-class precision, recall, and F1-score

## Key Findings

- Maximum slope was the single most predictive feature (importance: 0.134), consistent with known differences in ventricular conduction velocity across arrhythmia types
- Atrial beats showed the most confusion with Normal beats, reflecting their morphological similarity — a known clinical challenge
- Class balancing was critical: raw data contained 75% Normal beats, which would have biased a naive classifier

## Tech Stack

- **Python 3.9**
- **scikit-learn** — Random Forest classifier
- **wfdb** — PhysioNet waveform data access
- **scipy** — Signal processing and feature extraction
- **pandas / numpy** — Data manipulation
- **matplotlib / seaborn** — Visualization

## Dataset

MIT-BIH Arrhythmia Database — PhysioNet  
Moody GB, Mark RG. The impact of the MIT-BIH Arrhythmia Database. IEEE Eng in Med and Biol 20(3):45-50 (May-June 2001).

## Background

This project builds on biomedical sensing experience from the Materalis physiological sensing device project (UNC Chapel Hill) and R&D engineering work in FDA-regulated environments. It demonstrates end-to-end ML pipeline development applied to a real clinical problem in cardiac monitoring.

