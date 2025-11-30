1️⃣ Install Miniforge

Download Miniforge (Linux, Python 3.11) from:
https://github.com/conda-forge/miniforge

Install it:

bash Miniforge3-Linux-x86_64.sh


Initialize conda:

source ~/miniforge3/bin/activate

2️⃣ Optional: Install mamba for faster environment management
conda install mamba -n base -c conda-forge


Use mamba instead of conda for all future installs (faster dependency solving).

3️⃣ Create your ML environment
mamba create -n ML python=3.11 \
numpy pandas matplotlib seaborn scikit-learn jupyter \
pytorch torchvision torchaudio pytorch-cuda -c nvidia -c pytorch -c conda-forge


ML → name of the environment

python=3.11 → stable version for TensorFlow, PyTorch, and ML packages

pytorch-cuda → automatically picks the correct CUDA version for your GPU (1660 Ti)

numpy, pandas, matplotlib, seaborn, scikit-learn, jupyter → essential ML/data science packages

4️⃣ Activate the environment
mamba activate ML


Now you are inside the ML environment.

5️⃣ Install TensorFlow GPU
mamba install tensorflow-gpu -c conda-forge


Will automatically detect and use your GTX 1660 Ti GPU.

6️⃣ Optional: Install Spyder (if you want a GUI IDE)
mamba install spyder spyder-kernels -c conda-forge


Make sure spyder-kernels is installed in the ML environment so Spyder runs code in the correct Python environment.

7️⃣ Verify GPU acceleration
PyTorch:
import torch
print(torch.cuda.is_available())
print(torch.cuda.get_device_name(0))

TensorFlow:
import tensorflow as tf
print(tf.config.list_physical_devices('GPU'))


Expected output: your GTX 1660 Ti is detected.

8️⃣ Notes / Tips

Don’t pin pytorch-cuda to a specific version — let conda/mamba pick the compatible one.

Keep mamba in base, and use it for fast installs/updates.

CLI + Jupyter is more stable than Navigator. Use Spyder only if you like GUI.

Optional packages you can add later: plotly, opencv, xgboost, lightgbm.