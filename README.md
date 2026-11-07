# WaveCAP-DINO

---

**Wavelet-Guided Category-Aware Grounding DINO for UAV-Based Multimodal Object Detection**

Yongpeng Wen, Nanqing Liu, Shiqi Chen, Yaming Zhang, Zhuanxuan Hu, and Qi Ming

## Experimental Settings

Our model and ablation experiments are conducted on an NVIDIA A40 graphics processing unit (GPU). The proposed model is implemented using PyTorch 1.13.1 with CUDA 11.7.

We use Swin-T as the visual backbone for WaveCAP-DINO. Both the RGB and IR backbones are trainable, while the BERT text encoder is kept fixed by setting its learning-rate multiplier to zero. The category prompt is constructed by concatenating dataset category names with period separators. The original category tokens are retained when CAPS appends the learnable suffix tokens. The number of language-guided object queries is set to 900. In the training objective, the regression-loss weights are set to $\lambda_{\mathrm{L1}} = 5$ and $\lambda_{\mathrm{KLD}} = 2$.

For the DroneVehicle dataset, paired RGB and IR images are resized to $640 \times 512$ pixels. The model is trained for 12 epochs with a batch size of 8. We adopt the AdamW optimizer with an initial learning rate of $5 \times 10^{-5}$ and a weight decay of $1 \times 10^{-4}$. Both visual backbones use a learning-rate multiplier of 0.1. A linear warmup is applied over the first 30 iterations, starting at 0.001 times the initial learning rate. A MultiStep scheduler subsequently decays the learning rate by a factor of 0.1 at epochs 8 and 11.

For the ATR-UMOD dataset, paired RGB and IR images are resized to $640 \times 512$ pixels. The model is trained for 24 epochs with the same batch size, optimizer, and weight decay settings. The initial learning rate is set to $1 \times 10^{-4}$ and is decayed by a factor of 0.1 at epochs 16 and 22.

During training, random flipping is applied consistently to paired RGB and IR images and their bounding boxes. A flip is performed with an overall probability of 0.75, with horizontal, vertical, and diagonal directions selected with equal probability. Thus, each flip direction has a probability of 0.25. The same dataset-specific training protocol is applied to the models in the ablation studies.

## Code

The code is being organized and will be released in this repository.
