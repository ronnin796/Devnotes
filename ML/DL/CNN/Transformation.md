## 🧠 What is Overfitting?

**Overfitting** happens when your CNN learns **too much detail** (or noise) from the **training data**, and fails to generalize to **new/unseen images**.

You’ll see:

- Training accuracy → 🔺 very high (e.g., 98%)
    
- Validation accuracy → 🔻 much lower (e.g., 70%)
    

---

## 🎨 Solution — **Image Transformations (Data Augmentation)**

To reduce overfitting, we **artificially expand** the training dataset by applying **random transformations** to images.

This teaches the model to focus on **core features** (like shape or edges), not on orientation, color, or position.

---

## 🧩 Common Transformations

|Transformation|Description|Example Effect|
|---|---|---|
|**rotation_range**|Randomly rotate images|Makes model rotation-invariant|
|**width_shift_range**|Shift image horizontally|Handles off-center objects|
|**height_shift_range**|Shift image vertically|Handles top/bottom variations|
|**zoom_range**|Zoom in/out randomly|Trains model for scale variations|
|**shear_range**|Shear the image|Adds perspective variation|
|**horizontal_flip**|Flip image horizontally|Great for symmetry (cats, faces)|
|**vertical_flip**|Flip vertically|Rare (use for aerial/satellite data)|
|**brightness_range**|Random brightness changes|Makes model light-condition invariant|