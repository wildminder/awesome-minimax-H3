
<p id="components" align="center">◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆</p>

## ▓ Separated Components

Separated VAE files for MiniMax-H3. The video VAE and audio VAE are required for all generation workflows.

<a id="components-vae"></a>

### ▣ VAE (Video & Audio)

| Component | Source | Precision | Size | Download |
| :--- | :--- | :---: | :---: | :--- |
| Video VAE | ![Comfy-Org][gh-Comfy--Org] | ![fp16][badge-fp16] | 4.85 GB | [![][gh-Comfy--Org]](https://huggingface.co/Comfy-Org/MiniMax-H3/resolve/main/vae/minimax_h3_video_vae_fp16.safetensors) |
| Audio VAE | ![Comfy-Org][gh-Comfy--Org] | ![fp32][badge-fp32] | 577 MB | [![][gh-Comfy--Org]](https://huggingface.co/Comfy-Org/MiniMax-H3/resolve/main/vae/minimax_h3_audio_vae_fp32.safetensors) |
| Video VAE | ![dummy9996][gh-dummy9996] | ![fp8][badge-fp8] | 2.60 GB | [![][gh-dummy9996]](https://huggingface.co/dummy9996/minimax_h3_vae_fp8/resolve/main/minimax_h3_video_vae_fp8mix.safetensors) |
| Audio VAE | ![dummy9996][gh-dummy9996] | ![bf16][badge-bf16] | 289 MB | [![][gh-dummy9996]](https://huggingface.co/dummy9996/minimax_h3_vae_fp8/resolve/main/minimax_h3_audio_vae_bf16.safetensors) |

*FP8-mixed quantized VAE set by [dummy9996](https://huggingface.co/dummy9996/minimax_h3_vae_fp8) — smaller video VAE (2.60 GB, fp8) and audio VAE (289 MB, bf16) for low-VRAM workflows.*

*TensorRT/ONNX VAE builds by [lihaoyun6](https://huggingface.co/lihaoyun6/MiniMax-H3-VAE-ONNX) — compile the ONNX encoder (344 MB) and decoder (4.5 GB, or a 1.2 GB `w4a16_awq` variant for <12 GB VRAM) into TensorRT engines via the [ComfyUI-H3VAE_TRT](https://github.com/lihaoyun6/ComfyUI-H3VAE_TRT) node for up to 1.7× faster VAE.*

<p id="tae" align="center">· · · · · · · · · · · · · ·</p>

### ▣ Tiny Autoencoder (TAE)

Quickly trained 2D tiny VAE for MiniMax-H3 by [Kijai](https://huggingface.co/Kijai/MiniMax-H3-TAE). Not the greatest outcome, still beats latent2rgb for preview purposes. Currently only works with the `ModelPreviewOverride` node in [ComfyUI-KJNodes](https://github.com/kijai/ComfyUI-KJNodes).

| Component | Size | Download |
| :--- | :---: | :--- |
| TAE (preview VAE) | 9 MB | [![][gh-Kijai]](https://huggingface.co/Kijai/MiniMax-H3-TAE/resolve/main/vae_approx/taeh3.safetensors) |

### ▣ Image VAE (Mamad8)

Experimental image-specialized MiniMax H3 VAE that decodes a single temporal latent (`T=1`) into one image. Merged H3 VAE checkpoint — no custom node required. **For image workflows only**; the image-tuned decoder materially regresses multi-frame video reconstruction, so keep the original H3 VAE for video.

| Component | Size | Download |
| :--- | :---: | :--- |
| Single-image VAE (step 1597) | 4.85 GB | [![][gh-Mamad8]](https://huggingface.co/Mamad8/MiniMax-H3-Image-VAE/resolve/main/minimax_h3_t1_image_vae_step1597.safetensors) |

<p id="cliproj" align="center">· · · · · · · · · · · · · ·</p>

### ▣ Clip Projection (ClipProj + Conditioning)

Learned linear projections to condition H3 from a smaller text encoder. Two families: (1) **ClipProj** — swap the large Qwen3-VL-32B for a 4B/8B one (text-encoder VRAM ~15.7 GB → 4.5 GB, no change to the diffusion model, VAE, or sampler), and (2) **H3 Control** — identity/zero matrices for a no-control baseline. Projection files are fp16, MIT-licensed. Requires the [ComfyUI-ClipProj](https://github.com/nicolab28/ComfyUI-ClipProj) node; place files in `ComfyUI/models/clip_projections/`. Full variant matrix (4B/8B × base/MLP/celeb/celeb-MLP): [repo](https://huggingface.co/NicoLab28/ClipProj-MiniMax-H3).

| Variant | Encoder | Size | Download |
| :--- | :---: | :---: | :--- |
| ClipProj (base) | Qwen3-VL 4B | 52.5 MB | [![][gh-NicoLab28]](https://huggingface.co/NicoLab28/ClipProj-MiniMax-H3/resolve/main/mmh3-4b-ClipProj.safetensors) |
| ClipProj (MLP) | Qwen3-VL 4B | 304 MB | [![][gh-NicoLab28]](https://huggingface.co/NicoLab28/ClipProj-MiniMax-H3/resolve/main/mmh3-4b-ClipProj-mlp.safetensors) |
| ClipProj (celeb) | Qwen3-VL 4B | 52.5 MB | [![][gh-NicoLab28]](https://huggingface.co/NicoLab28/ClipProj-MiniMax-H3/resolve/main/mmh3-4b-ClipProj-celeb.safetensors) |
| ClipProj (celeb-MLP) | Qwen3-VL 4B | 304 MB | [![][gh-NicoLab28]](https://huggingface.co/NicoLab28/ClipProj-MiniMax-H3/resolve/main/mmh3-4b-ClipProj-celeb-mlp.safetensors) |
| ClipProj (base) | Qwen3-VL 8B | 84 MB | [![][gh-NicoLab28]](https://huggingface.co/NicoLab28/ClipProj-MiniMax-H3/resolve/main/mmh3-8b-ClipProj.safetensors) |
| ClipProj (MLP) | Qwen3-VL 8B | 386 MB | [![][gh-NicoLab28]](https://huggingface.co/NicoLab28/ClipProj-MiniMax-H3/resolve/main/mmh3-8b-ClipProj-mlp.safetensors) |
| ClipProj (celeb) | Qwen3-VL 8B | 84 MB | [![][gh-NicoLab28]](https://huggingface.co/NicoLab28/ClipProj-MiniMax-H3/resolve/main/mmh3-8b-ClipProj-celeb.safetensors) |
| ClipProj (celeb-MLP) | Qwen3-VL 8B | 386 MB | [![][gh-NicoLab28]](https://huggingface.co/NicoLab28/ClipProj-MiniMax-H3/resolve/main/mmh3-8b-ClipProj-celeb-mlp.safetensors) |
| H3 Control Identity | — | 52.5 MB | [![][gh-NicoLab28]](https://huggingface.co/NicoLab28/ClipProj-MiniMax-H3/resolve/main/mmh3-ClipProj-control-identity.safetensors) |
| H3 Control Zero | — | 52.5 MB | [![][gh-NicoLab28]](https://huggingface.co/NicoLab28/ClipProj-MiniMax-H3/resolve/main/mmh3-ClipProj-control-zero.safetensors) |

**Older `h3_*` filenames** (with `tap24` / `CONDPROJ` / `int8convrot` suffixes) have moved to [`obsolete/`](https://huggingface.co/NicoLab28/ClipProj-MiniMax-H3/tree/main/obsolete) — canonical names are now `mmh3-*-ClipProj*.safetensors`.

<p id="refpatch" align="center">· · · · · · · · · · · · · ·</p>

### ▣ Ref Patch (lihaoyun6)

`fl2va` → `ref2va` behavior patch by [lihaoyun6](https://huggingface.co/lihaoyun6/MiniMax-H3-Ref-Patch). Extracts 112 specific keys shared between the `ref2va` and `fl2va` weights and stores their differences as a single patch, letting the lighter FL2VA checkpoint partially mimic Ref2VA output quality. Requires the [ComfyUI-MiniMaxH3_Ref-Patch](https://github.com/lihaoyun6/ComfyUI-MiniMaxH3_Ref-Patch) node to load. Apache-2.0.

| Component | Size | Download |
| :--- | :---: | :--- |
| Ref Patch | 148 MB | [![][gh-lihaoyun6]](https://huggingface.co/lihaoyun6/MiniMax-H3-Ref-Patch) |

<p id="lupid" align="center">· · · · · · · · · · · · · ·</p>

### ▣ Latent Upscaler (LBH-123-AI)

Neural latent-space upscaler for MiniMax H3 video generation by [LBH-123-AI](https://huggingface.co/LBH-123-AI/Minimax_h3_latent_Upscaler). Works directly on H3's 24-channel VAE latents to upscale spatial resolution (H×W) while preserving the time dimension — **accelerates high-res video gen by skipping the costly ~5B-param VAE decode → pixel-upscale → encode round-trip**, and avoids the ghosting / double-image artifacts of naive bilinear/bicubic latent interpolation. 3D-convolution backbone (2D and 3D node variants; one checkpoint serves both, architecture auto-detected). Trained on ~80k paired samples (≈70k video + ≈8k 2K image pairs). Apache-2.0. Pairs with the [ComfyUI_Minimax_h3_latent_Upscaler](https://github.com/LBH-123-AI/ComfyUI_Minimax_h3_latent_Upscaler) node. ⚠️ Saves **time, not VRAM** — the refine pass still runs at target resolution.

| Component | Precision | Size | Download |
| :--- | :---: | :---: | :--- |
| Latent Upscaler | ![bf16][badge-bf16] | 691 MB | [![][gh-LBH-123-AI]](https://huggingface.co/LBH-123-AI/Minimax_h3_latent_Upscaler/resolve/main/minimax_h3_latent_upscaler_3d_bf16.safetensors) |
| Latent Upscaler | ![fp16][badge-fp16] | 691 MB | [![][gh-LBH-123-AI]](https://huggingface.co/LBH-123-AI/Minimax_h3_latent_Upscaler/resolve/main/minimax_h3_latent_upscaler_3d_fp16.safetensors) |
| Latent Upscaler | ![fp32][badge-fp32] | 1.38 GB | [![][gh-LBH-123-AI]](https://huggingface.co/LBH-123-AI/Minimax_h3_latent_Upscaler/resolve/main/minimax_h3_latent_upscaler_3d_fp32.pth) |

