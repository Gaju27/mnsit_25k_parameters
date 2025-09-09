

````markdown
# MNIST – 25K Parameters Model (PyTorch)

This repository contains a compact PyTorch model for the **MNIST handwritten digit classification** task, designed with approximately **25,000 trainable parameters**.  
The goal was to balance efficiency and accuracy while keeping the parameter count small.  

---

## 🚀 Features
- Lightweight CNN architecture with ~25K trainable parameters  
- Achieves **~98% accuracy after first epoch**  
- Optimized for Google Colab training  
- Efficient design for experimentation and educational purposes  

---

## 📂 Repository Files
- **`MNSIT 25k parameters.ipynb`** → Jupyter/Colab notebook with full code  
- **`README.md`** → Project documentation  

---

## ⚙️ How to Run in Google Colab
1. Open the notebook in Colab:
   - Upload `MNSIT 25k parameters.ipynb` to [Google Colab](https://colab.research.google.com/)  

2. Run all cells in the notebook:
   - Model definition  
   - Training loop  
   - Evaluation  

3. Confirm parameter count:
   ```python
   def count_parameters(model):
       return sum(p.numel() for p in model.parameters() if p.requires_grad)

   print("Trainable parameters:", count_parameters(model))
````

---

## 📊 Expected Results

* **Trainable Parameters:** \~25,000
* **Accuracy (1st Epoch):** \~98% on MNIST test set

---

## 🔧 Improvements Made to Achieve \~98% Accuracy

To boost the accuracy from \~94% → \~98% within the first epoch, the following changes were applied:

1. **Batch Normalization**

   * Added `nn.BatchNorm2d` after every convolution layer.

2. **Stronger Non-Linearity**

   * Used **ReLU** activations.

3. **Dropout Regularization**

   * Added a small dropout (e.g., `p=0.2`).

4. **Better Weight Initialization**

   * Xavier (Glorot) initialization for dense layers.

5. **Learning Rate Tuning**

   * Adam optimizer (`lr=5e-4`).

6. **Mini-Batch Size**

   * Batch size = 64.

---

## 🔄 Comparison: First Version vs Final Version

| Aspect             | First Version     | Final Version             | Improvement                      |
| ------------------ | ----------------- | ------------------------- | -------------------------------- |
| Conv layers        | 2 layers (1→8→16) | 3 layers (1→16→32→64)     | More feature extraction          |
| BatchNorm          | Partial           | After every conv          | More stability                   |
| Pooling            | MaxPool only      | MaxPool + AdaptiveAvgPool | Param reduction & generalization |
| Fully connected    | 784→32→10         | 64→23→10                  | Balanced params                  |
| Optimizer          | SGD               | Adam                      | Faster convergence               |
| Batch size         | 128               | 64                        | Better early accuracy            |
| 1st epoch accuracy | \~94–95%          | \~97–98%                  | ✅ Achieved target                |

---

## 🧮 Parameter Calculation Details

### 1. Convolutional Layer 1

* Input: 1 channel
* Output: 16 filters, kernel 3×3
* Weights: 16 \* (1*3*3) = 144
* Bias: 16 → Total: 160

### 2. BatchNorm (after Conv1) → 32 parameters

### 3. Convolutional Layer 2

* Input: 16 channels, Output: 32 filters → Weights: 4608, Bias: 32 → Total: 4640

### 4. BatchNorm (after Conv2) → 64 parameters

### 5. Convolutional Layer 3

* Input: 32 channels, Output: 64 filters → Weights: 18432, Bias: 64 → Total: 18496

### 6. BatchNorm (after Conv3) → 128 parameters

### 7. Fully Connected Layer

* 64 → 23 → Weights: 1472, Bias: 23 → Total: 1495

### 8. Output Layer

* 23 → 10 → Weights: 230, Bias: 10 → Total: 240

### ✅ Grand Total

```
Conv1+BN1  = 160+32   = 192
Conv2+BN2  = 4640+64  = 4704
Conv3+BN3  = 18496+128 = 18624
FC1        = 1495
FC2        = 240
--------------------------
TOTAL ≈ 25,255
```

---

## 🖼️ Example Output

* **Parameters:** \~25,255
* **Accuracy after Epoch 1:** 97.5–98.2%

---

## 📜 License

This project is released under the **MIT License**.  

You are free to **use, modify, and distribute** this code for **personal, educational, or commercial purposes**.  
Please give **credit to the original author** when sharing or using this work.

