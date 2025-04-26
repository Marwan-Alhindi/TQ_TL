# TQ_TL - Transfer Learning with EfficientNet

---

## 📁 Dataset

- Dataset organized under `dataset/` folder
- Versioned using **DVC** and stored remotely on **DagsHub**
- Structure:
  - `train/`
  - `val/`
  - `test/`

---

## 🧪 Experiments

### 1️⃣ Training Only the Head of EfficientNet
- **Strategy**: Freeze EfficientNet backbone, train only a new classification head.
- **Observation**: Fast convergence, but limited learning capacity, early plateau.

### 2️⃣ EfficientNet Frozen — Head + CNN + MLP
- **Strategy**: Add CNN + MLP head; keep EfficientNet backbone frozen.
- **Observation**: Better than simple head; richer feature extraction; improved validation accuracy.

### 3️⃣ EfficientNet Non-Frozen — Head + CNN + MLP
- **Strategy**: Same custom head, but fine-tune the entire model including EfficientNet backbone.
- **Observation**: Best model — fine-tuning unlocked backbone potential and boosted final accuracy.

### 4️⃣ Gradual Freezing + Scheduler
- **Strategy**: Start with entire model trainable; gradually freeze EfficientNet blocks while training; use a learning rate scheduler.
- **Observation**: Smoothed convergence, improved generalization, slower but more stable learning.

### 5️⃣ Stronger Backbone — EfficientNetB4
- **Strategy**: Replace backbone with EfficientNetB4 for higher capacity.
- **Observation**: Increased model capacity; needs stronger regularization to avoid overfitting.

---

## 🏆 Best Model

✅ **EfficientNet Non-Frozen — Head + CNN + MLP**

- **Test Accuracy**: **91.43%**
- Achieved after full fine-tuning
- Balanced speed of convergence with generalization
- Carefully tuned learning rates for backbone vs head

---

## 📈 Experiment Tracking

- All experiments tracked using **MLflow**:
  - Hyperparameters
  - Metrics (train/validation loss and accuracy)
  - Model artifacts
- **mlruns/** folder pushed alongside code for full versioning and traceability.

---

## 📊 Training Results Snapshot

| Epoch | Train Loss | Train Acc | Val Loss | Val Acc |
|:----|:----|:----|:----|:----|
| 1 | 0.5634 | 81.54% | 0.4526 | 86.41% |
| 2 | 0.2729 | 90.71% | 0.4096 | 88.22% |
| 3 | 0.1885 | 93.78% | 0.4155 | 87.84% |
| 4 | 0.1394 | 95.36% | 0.4647 | 88.22% |
| 5 | 0.1160 | 96.04% | 0.4815 | 88.02% |
| 6 | 0.0818 | 97.36% | 0.4535 | 88.89% |
| 7 | 0.0706 | 97.70% | 0.4409 | 89.10% |
| 8 | 0.0506 | 98.36% | 0.4780 | 89.39% |
| 9 | 0.0520 | 98.40% | 0.4950 | 89.30% |
| 10 | 0.0451 | 98.60% | 0.4859 | 88.98% |

✅ **Final Test Loss**: `0.3920`  
✅ **Final Test Accuracy**: `91.43%`

---

## 🧠 Observations

- **Feature Extraction**:
  - Fast and stable training
  - Limited peak performance
- **Fine-Tuning**:
  - Slower training, but much better generalization
  - Unlocks full backbone potential
- **Gradual Freezing**:
  - Smooths convergence
  - Especially useful when backbone is sensitive
- **Bigger Models**:
  - Higher capacity, but requires stronger overfitting prevention (e.g., regularization, augmentation)

---

## ✨ Notes

- Full reproducibility ensured through **DVC** and **MLflow**
- Cloud dataset and model management with **DagsHub**
- Compatible with Google Colab and cloud environments
- Best practices followed for experiment tracking and versioning

---