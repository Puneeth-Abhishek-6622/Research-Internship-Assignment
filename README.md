# 🎙️ Forced Alignment using Montreal Forced Aligner (MFA)

![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-yellow.svg)

---

## 📘 Project Overview

This project demonstrates **Forced Alignment**—the process of automatically aligning speech audio with its corresponding text transcript at the word and phoneme level—using the [Montreal Forced Aligner (MFA)](https://montreal-forced-aligner.readthedocs.io/en/latest/) tool.

The goal was to build a fully automated alignment pipeline that outputs precise word and phoneme boundaries in TextGrid format, ready for analysis in Praat.

## 🚀 Why Docker?

Instead of installing MFA manually and dealing with version mismatches or dependency chaos, this project uses Docker for a clean, reproducible setup.

Docker ensures that the environment behaves identically across all systems—whether you're on Windows, macOS, or Linux.

## 🧰 Prerequisites

Make sure you have:

* **Docker** installed and running.
* A folder containing:
    * Your `.wav` audio files.
    * Corresponding `.txt` transcript files (same name as the audio files).
    * The MFA acoustic model and dictionary files.

### Example Folder Structure
```bash
MFA DATA/
├── english_us_mfa.dict
├── english_mfa.zip
├── corpus/
│   ├── audio1.wav
│   ├── audio1.txt
│   ├── audio2.wav
│   ├── audio2.txt
│   └── ...
└── output/
```

## 📦 Download Required Models

You'll need to download the pre-trained models for English.

* **🔹 English Acoustic Model (v3.1.0)**
    * Download from MFA’s official release page: 👉 `english_mfa.zip`
* **🔹 English (US) Pronunciation Dictionary (v3.1.0)**
    * Download from: 👉 `english_us_mfa.dict`

Place these files in your main `MFA DATA` directory as shown in the structure above.

## ⚙️ How to Run

### 1. Pull the Docker Image

Run this once to pull the latest MFA image from Docker Hub:

```bash
docker pull mmcauliffe/montreal-forced-aligner:latest
```

### 2. Run the Alignment
After organizing your data, run the appropriate command for your system to mount your data folder and start the alignment process.

🔸 Windows (PowerShell / CMD)
```bash 
docker run -it --rm -v "%USERPROFILE%\Desktop\MFA DATA:/data" mmcauliffe/montreal-forced-aligner:latest mfa align /data/corpus /data/english_us_mfa.dict /data/english_mfa.zip /data/output
```
🔸 Linux / macOS
```bash 
docker run -it --rm \
  -v ~/Desktop/MFA DATA:/data \
  mmcauliffe/montreal-forced-aligner:latest \
  mfa align /data/corpus /data/english_us_mfa.dict /data/english_mfa.zip /data/output
```
Note: The command above assumes your MFA DATA folder is on your Desktop. Change the path (%USERPROFILE%\Desktop\MFA DATA or ~/Desktop/MFA DATA) if it's located elsewhere.

🗂️ Output
After successful alignment, you’ll find .TextGrid files for each audio–text pair inside the output/ folder:

```bash
output/
├── audio1.TextGrid
├── audio2.TextGrid
└── ...
```
Each .TextGrid file can be opened in Praat to visualize the word and phoneme boundaries.
