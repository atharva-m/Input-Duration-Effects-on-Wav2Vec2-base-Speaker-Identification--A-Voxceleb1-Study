# Input Duration Effects on Wav2Vec2-base Speaker Identification – A VoxCeleb1 Study

[![License: CC0 1.0](https://img.shields.io/badge/License-CC0%201.0-lightgrey.svg)](https://creativecommons.org/publicdomain/zero/1.0/)
[![Python 3.11](https://img.shields.io/badge/Python-3.11-blue.svg)](https://www.python.org/downloads/release/python-3110/)

This project investigates how the **input audio duration** affects the **speaker recognition performance** and **computational cost** of the Wav2Vec2-base model when fine-tuned on the **VoxCeleb1** dataset.

---

## 🎯 Motivation

Real-world speech varies widely in duration, but speaker recognition systems often truncate or pad to fixed lengths. We evaluate how these choices affect:

- **Accuracy**, **Recall**, and **Equal Error Rate (EER)**
- **Efficiency**, measured via attention FLOPs (L² scaling) and a custom EER × Cost metric

---

## 📊 Key Findings

- **3–4 seconds** of audio already enable strong speaker identification (EER drops 30×).
- **5–8 seconds** is the sweet spot: best accuracy, lowest EER, and highest compute-efficiency.
- **Longer inputs (>8s)** degrade performance and increase cost — more ≠ better.

---

## 📁 Repository Contents

| Folder | Description |
|--------|-------------|
| `notebooks/` | Jupyter notebook used for training, evaluation, and metric logging |
| `plots/` | Animated MP4 plots showing trends across durations |
| `presentation/` | Final presentation slides for the project |

---

## 🧪 Experimental Setup

- Model: `facebook/wav2vec2-base` with a classification head
- Dataset: `Codec-SUPERB/Voxceleb1_test_original` (40 speakers)
- Fixed input durations: 1s → 69s (16 total)
- Training: 20 epochs, batch size 32, AdamW optimizer, LR = 3e-5
- Precision: FP32 up to 15s; bfloat16 for longer durations due to OOM limits

---

## 📈 Visualizations

We include five animated plots:
- `accuracy_vs_duration.mp4`
- `eer_vs_duration.mp4`
- `recall_vs_duration.mp4`
- `eer_vs_costproxy.mp4`
- `accuracy_vs_costproxy.mp4`

These progressively reveal trends and highlight key durations with color-coded legends.

---

## 📌 How to Run

Open [`Investigating_Input_Duration_Effects_on_Wav2Vec2.ipynb`](notebook/Investigating_Input_Duration_Effects_on_Wav2Vec2.ipynb) in [Google Colab](https://colab.research.google.com/) and follow the step-by-step training and evaluation process.

---

## 🧠 Conclusion

Short audio clips (~3–8s) are highly effective for speaker ID with Wav2Vec2. Systems should trim or clip input audio to this range to ensure optimal generalization and compute efficiency.

---

## 🚀 Future Work

- Evaluate on VoxCeleb1-train, multilingual datasets
- Try attention-based segment selection (vs. fixed durations)
- Test long-context architectures (e.g., sparse transformers)

---

## 📜 License

This work is licensed under the [Creative Commons Zero v1.0 Universal (CC0 1.0)](https://creativecommons.org/publicdomain/zero/1.0/) license. You are free to use, modify, and distribute without restriction.

---

### Contact
Atharva Mokashi · atharvamokashi01@gmail.com · [LinkedIn](https://www.linkedin.com/in/atharva-m)
