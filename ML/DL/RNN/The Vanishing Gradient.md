- ![[Pasted image 20251114194519.png]]
- # 🧠 Vanishing Gradient Problem

## 🔍 **Definition**

The **vanishing gradient problem** occurs when gradients become extremely small as they propagate backward through a deep neural network.  
As a result, **early layers learn very slowly or not at all**, causing training failure.

---

## 🧪 **Why It Happens**

Most activation functions (especially **sigmoid** and **tanh**) compress inputs into a small range.

- Sigmoid derivative ≤ 0.25
    
- Repeated multiplication during backprop:
    

`small_derivative^n → almost 0`

In deep networks, this makes gradients disappear before they reach earlier layers.

---

## ⚠️ **Consequences**

- Early layers fail to update
    
- Slow or stalled training
    
- Poor model performance
    
- Especially severe in RNNs
    

---

## 📉 **Example**

If each layer contributes a derivative ≈ 0.2, then:

`(0.2)^20 ≈ 1.04e−14 → basically zero`

---

## 🛠️ **Solutions**

### ✔️ ReLU and Variants

- ReLU, LeakyReLU, GELU → avoid tiny derivatives
    

### ✔️ Better Weight Initialization

- **Xavier (Glorot)** for tanh
    
- **He initialization** for ReLU
    

### ✔️ Batch Normalization

- Normalizes activations, stabilizes gradients
    

### ✔️ Residual Connections (ResNet)

- Skip connections allow gradients to flow directly backwards
    
- Solved deep network training up to 1000+ layers
    

### ✔️ LSTM/GRU (for RNNs)

- Designed specifically to avoid vanishing gradients using gating mechanisms
    

---

## 🧩 **TL;DR**

> **Vanishing gradients = training signal dies before reaching the early layers, causing them to stop learning.**