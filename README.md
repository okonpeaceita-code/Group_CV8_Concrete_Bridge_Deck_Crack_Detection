# Concrete Crack Detector

A Streamlit web app that classifies concrete surface images as **cracked** or **not cracked** using a custom-trained CNN model.

---

## Project Structure

```
.
├── app.py                   # Streamlit application
├── custom_cnn_best.keras    # Trained model file
└── README.md
```

---

## Model

| Metric | Value |
|---|---|
| Architecture | Custom CNN |
| Framework | TensorFlow / Keras |
| Accuracy | **96.47%** |
| Precision | 96.37% |
| Recall | 96.47% |
| F1-Score | 96.38% |

### Per-class Performance (1,502 test samples)

| Class | Precision | Recall | F1 | Support |
|---|---|---|---|---|
| cracked | 97.32% | 98.72% | 98.01% | 1,324 |
| not_cracked | 89.31% | 79.78% | 84.27% | 178 |

### Output Score Interpretation

The model outputs a single float in **[0, 1]**:

- **Close to 1.0** → cracked (positive class)
- **Close to 0.0** → not cracked (negative class)
- **Threshold** → 0.5

---

## Setup

### 1. Install dependencies

```bash
pip install streamlit tensorflow pillow numpy
```

### 2. Place the model file

Make sure `custom_cnn_best.keras` is in the **same directory** as `app.py`.

### 3. Run

```bash
streamlit run app.py
```

The app opens at `http://localhost:8501` by default.

---

## Usage

1. Open the app in your browser.
2. Upload a concrete surface image (JPG, PNG, BMP, or WEBP).
3. The model returns:
   - **Label** — cracked or not cracked
   - **Raw score** — the exact model output
   - **Confidence** — how certain the prediction is

---

## Dataset

Trained on the [Concrete Crack Dataset](https://www.kaggle.com/datasets/yatata1/crack-dataset), split as follows:

| Split | Ratio |
|---|---|
| Train | 70% |
| Validation | 15% |
| Test | 15% |

---

## Notes

- Default input size is **227 × 227**. If your model was trained on a different size, update `IMG_SIZE` in `app.py`.
- The model file is loaded once and cached via `@st.cache_resource` for fast repeated inference.
