
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

*TensorRT/ONNX VAE builds by [lihaoyun6](https://huggingface.co/lihaoyun6/MiniMax-H3-VAE-ONNX) — compile the ONNX encoder (344 MB) and decoder (4.5 GB, or a 1.2 GB `w4a16_awq` variant for <12 GB VRAM) into TensorRT engines via the [ComfyUI-H3VAE_TRT](https://github.com/lihaoyun6/ComfyUI-H3VAE_TRT) node.

*■ **Light video VAE decoder** by [corechan](https://huggingface.co/corechan/MiniMax-H3-LightVAE) — a converted copy of **LynnReal-Omni**'s distilled decoder, which decodes ordinary H3 latents with **26 transformer blocks instead of 36**. Ships as a diffusers-key fp16 safetensors (3.26 GB) **and** an ONNX tile for TensorRT. ⚠️ **Not a drop-in ComfyUI swap** — it is *decoder-only*: truncate `vae.decoder.transformer_blocks` to the first 26 and `load_state_dict(..., strict=False)`; the encoder, latent space and temporal structure are stock H3.
*■ **LightVAE (lightx2v / ModelTC)** — [lightx2v/LightVAE](https://huggingface.co/lightx2v/LightVAE) ([paper](https://github.com/ModelTC/LightVAE), Apache-2.0) is a *proper* temporal-low-rank + block-pruned video autoencoder, multi-backbone (Wan2.1, Wan2.2, MiniMax-H3), each in **Lite** (pruned, faster) and **Pro** (original depth). For H3 that means the **Lite decoder (3.25 GB)** and an optional **Lite encoder (406 MB)** — the first H3 encoder replacement in the list. ⚠️ **The `-comfy.safetensors` files need the `Load LightVAE (TLR)` custom node from [ModelTC/LightVAE](https://github.com/ModelTC/LightVAE)** — loading them with stock `VAELoader` fails. **Keep the H3 audio VAE untouched.** No H3 reconstruction benchmark is published.*

<p id="tae" align="center">· · · · · · · · · · · · · ·</p>

### ▣ Tiny Autoencoder (TAE)

Tiny 2D VAE for fast H3 previews by [Kijai](https://huggingface.co/Kijai/MiniMax-H3-TAE) — beats latent2rgb. Currently only works with the `ModelPreviewOverride` node in [ComfyUI-KJNodes](https://github.com/kijai/ComfyUI-KJNodes).

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

Learned linear projections to condition H3 from a smaller text encoder — swap the large Qwen3-VL-32B for a 4B/8B one (text-encoder VRAM ~15.7 GB → 4.5 GB, no change to the diffusion model, VAE, or sampler); H3 Control identity/zero matrices provide a no-control baseline. fp16, MIT-licensed. Requires the [ComfyUI-ClipProj](https://github.com/nicolab28/ComfyUI-ClipProj) node; place files in `ComfyUI/models/clip_projections/`. Full variant matrix (4B/8B × base/MLP/celeb/celeb-MLP): [repo](https://huggingface.co/NicoLab28/ClipProj-MiniMax-H3).

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

`fl2va` → `ref2va` behavior patch by [lihaoyun6](https://huggingface.co/lihaoyun6/MiniMax-H3-Ref-Patch) — lets the lighter FL2VA checkpoint partially mimic Ref2VA output quality. Requires the [ComfyUI-MiniMaxH3_Ref-Patch](https://github.com/lihaoyun6/ComfyUI-MiniMaxH3_Ref-Patch) node to load. Apache-2.0.

| Component | Size | Download |
| :--- | :---: | :--- |
| Ref Patch | 148 MB | [![][gh-lihaoyun6]](https://huggingface.co/lihaoyun6/MiniMax-H3-Ref-Patch) |

<p id="lupid" align="center">· · · · · · · · · · · · · ·</p>

### ▣ Latent Upscaler (LBH-123-AI)

Neural latent-space upscaler for MiniMax H3 video generation by [LBH-123-AI](https://huggingface.co/LBH-123-AI/Minimax_h3_latent_Upscaler) — works directly on H3's 24-channel VAE latents to upscale spatial resolution (H×W) while preserving the time dimension, skipping the VAE decode → pixel-upscale → encode round-trip. 3D-convolution backbone (2D and 3D node variants), Apache-2.0. Pairs with the [ComfyUI_Minimax_h3_latent_Upscaler](https://github.com/LBH-123-AI/ComfyUI_Minimax_h3_latent_Upscaler) node. ⚠️ Saves **time, not VRAM** — the refine pass still runs at target resolution. [Asirus](https://huggingface.co/Asirus/Minimax-H3-Latent-Upscaler-BF16-MAXQUALITY) also ships a derivative **BF16 Conservative v5** requantization.

| Component | Precision | Size | Download |
| :--- | :---: | :---: | :--- |
| Latent Upscaler v1 | ![bf16][badge-bf16] | 691 MB | [![][gh-LBH-123-AI]](https://huggingface.co/LBH-123-AI/Minimax_h3_latent_Upscaler/resolve/main/minimax_h3_latent_upscaler_3d_conv_v1/minimax_h3_latent_upscaler_3d_conv_v1_bf16.safetensors) |
| Latent Upscaler v1 | ![fp16][badge-fp16] | 691 MB | [![][gh-LBH-123-AI]](https://huggingface.co/LBH-123-AI/Minimax_h3_latent_Upscaler/resolve/main/minimax_h3_latent_upscaler_3d_conv_v1/minimax_h3_latent_upscaler_3d_conv_v1_fp16.safetensors) |
| Latent Upscaler v1 | ![fp32][badge-fp32] | 1.38 GB | [![][gh-LBH-123-AI]](https://huggingface.co/LBH-123-AI/Minimax_h3_latent_Upscaler/resolve/main/minimax_h3_latent_upscaler_3d_conv_v1/minimax_h3_latent_upscaler_3d_conv_v1_fp32.pth) |
| BF16 Conservative v5 | ![bf16][badge-bf16] | 691 MB | [![][gh-Asirus]](https://huggingface.co/Asirus/Minimax-H3-Latent-Upscaler-BF16-MAXQUALITY/resolve/main/minimax_h3_bf16_CONSERVATIVE_v5.safetensors) |

<p id="controlnet" align="center">· · · · · · · · · · · · · ·</p>

### ▣ Fun-ControlNet Union 2.0 (alibaba-pai)

Control branch for MiniMax-H3 from Alibaba PAI's [VideoX-Fun](https://github.com/aigc-apps/VideoX-Fun) line, by [alibaba-pai](https://huggingface.co/alibaba-pai/MiniMax-H3-Fun-Controlnet-Union-2.0). Loaded **on top of** the base H3 transformer — the checkpoint holds only the control branch (`control_proj_in` + 10 control blocks, ≈13.5 GB) and is not a standalone model.

**What 2.0 changes vs v1:** 8 control conditions instead of 5 (adds **Scribble, Layout, Gray**), a denser injection schedule (10 control blocks at layers `0, 5, 10, …, 45` instead of 5), and a `post_norm` inpaint recipe. `control_in_dim = 49` (latent + masked latent + mask) so the same branch does both control and inpainting; guidance-distilled (`guidance_scale = 1.0`).

> ⚠️ **A v1 config against this checkpoint fails silently.** With the old `minimax_h3_control.yaml` (5 blocks) only half the branch is built and `load_state_dict(strict=False)` drops `control_blocks.5~9` as unexpected keys — outputs are wrong with no error. Always use `minimax_h3_control_inpaint_post_norm.yaml`.

| Component | Precision | Size | Download |
| :--- | :---: | :---: | :--- |
| ControlNet-Union-2.0 branch | ![fp32][badge-fp32] | 12.6 GB | [![][gh-alibaba-pai]](https://huggingface.co/alibaba-pai/MiniMax-H3-Fun-Controlnet-Union-2.0/resolve/main/MiniMax-H3-Fun-Controlnet-Union-2.0.safetensors) |

*MiniMax H3 Community License Agreement; 8 control conditions plus video inpainting, one checkpoint. V2V control workflows (openpose/canny/depth) in javawock7618's INT8 pack wire this branch in.*

