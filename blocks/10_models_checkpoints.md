<a id="models"></a>

## ▓ Models

MiniMax-H3 is a general-purpose, omni-modal generative system by [MiniMaxAI](https://huggingface.co/MiniMaxAI/MiniMax-H3). It supports unified understanding of multimodal contexts composed of text, images, video, and audio, and can generate video with native stereo audio at resolutions up to 2K and durations of up to 15 seconds. The model has two variants: **FL2VA** (first-and-last-frame mode) and **Ref2VA** (omni-reference mode).

<a id="checkpoints"></a>

### ▣ Checkpoints

Official and ComfyUI-repackaged model files.

* **[MiniMaxAI/MiniMax-H3](https://huggingface.co/MiniMaxAI/MiniMax-H3)** - Official repository.
* **[Comfy-Org/MiniMax-H3](https://huggingface.co/Comfy-Org/MiniMax-H3)** - ComfyUI-repackaged model files.

| Variant | Name | Precision | Size | Download |
| :--- | :--- | :---: | :---: | :---: |
| FL2VA | `minimax_h3_fl2va` | ![bf16][badge-bf16] | 61.73 GB | [![][gh-Comfy--Org]](https://huggingface.co/Comfy-Org/MiniMax-H3/resolve/main/diffusion_models/minimax_h3_fl2va_bf16.safetensors) |
| FL2VA | `minimax_h3_fl2va` | ![int8][badge-int8] | 31.70 GB | [![][gh-Comfy--Org]](https://huggingface.co/Comfy-Org/MiniMax-H3/resolve/main/diffusion_models/minimax_h3_fl2va_int8_convrot.safetensors) |
| FL2VA | `minimax_h3_fl2va_pruned` | ![bf16][badge-bf16] | 37.46 GB | [![][gh-Comfy--Org]](https://huggingface.co/Comfy-Org/MiniMax-H3/resolve/main/diffusion_models/minimax_h3_fl2va_pruned_bf16.safetensors) |
| FL2VA | `minimax_h3_fl2va_pruned` | ![fp8][badge-fp8] | 19.52 GB | [![][gh-Comfy--Org]](https://huggingface.co/Comfy-Org/MiniMax-H3/resolve/main/diffusion_models/minimax_h3_fl2va_pruned_fp8_scaled.safetensors) |
| FL2VA | `minimax_h3_fl2va_pruned` | ![int8][badge-int8] | 19.53 GB | [![][gh-Comfy--Org]](https://huggingface.co/Comfy-Org/MiniMax-H3/resolve/main/diffusion_models/minimax_h3_fl2va_pruned_int8_convrot.safetensors) |
| Ref2VA | `minimax_h3_ref2va` | ![bf16][badge-bf16] | 61.73 GB | [![][gh-Comfy--Org]](https://huggingface.co/Comfy-Org/MiniMax-H3/resolve/main/diffusion_models/minimax_h3_ref2va_bf16.safetensors) |
| Ref2VA | `minimax_h3_ref2va` | ![int8][badge-int8] | 31.70 GB | [![][gh-Comfy--Org]](https://huggingface.co/Comfy-Org/MiniMax-H3/resolve/main/diffusion_models/minimax_h3_ref2va_int8_convrot.safetensors) |
| Ref2VA | `minimax_h3_ref2va_pruned` | ![bf16][badge-bf16] | 37.46 GB | [![][gh-Comfy--Org]](https://huggingface.co/Comfy-Org/MiniMax-H3/resolve/main/diffusion_models/minimax_h3_ref2va_pruned_bf16.safetensors) |
| Ref2VA | `minimax_h3_ref2va_pruned` | ![fp8][badge-fp8] | 19.52 GB | [![][gh-Comfy--Org]](https://huggingface.co/Comfy-Org/MiniMax-H3/resolve/main/diffusion_models/minimax_h3_ref2va_pruned_fp8_scaled.safetensors) |
| Ref2VA | `minimax_h3_ref2va_pruned` | ![int8][badge-int8] | 19.53 GB | [![][gh-Comfy--Org]](https://huggingface.co/Comfy-Org/MiniMax-H3/resolve/main/diffusion_models/minimax_h3_ref2va_pruned_int8_convrot.safetensors) |

**Model Variants:**
- **H3-Base-FL2VA** (First-and-last-frame mode): Supports zero, one, or two input images. No image input = T2V; one image = first/last-frame-to-video; two images = first-and-last-frame-to-video.
- **H3-Base-Ref2VA** (Omni-reference mode): Supports multi-modal reference inputs — up to 9 images, 3 video clips (2–15s each), 3 audio clips, max 12 files total.

### ▣ Turbo (Acceleration LoRA)

4-step audio-video generation LoRAs — render joint video + synchronized stereo audio in 4 sampling steps instead of ~20 (~5× speedup). Early prototype; comfort zone for sharpness is 6–8 steps. The **lightx2v** distil (top row) is the shared base for most ComfyUI conversions; for pruned checkpoints use the ComfyUI-converted variants below. The original larryvrh LoRA targets the full (non-pruned) FL2VA checkpoint and needs the [ComfyUI-MiniMax-H3-Turbo](https://github.com/Larryvrh/ComfyUI-MiniMax-H3-Turbo) sampler node. The `· resized` rows are exact-SVD **dynamic-rank** compressions (drbaph) or rank-truncated resizes (Kijai, silveroxides) of the official lightx2v ComfyUI weights — much smaller files at near-identical effective updates (Ref2V r21: 99.92% cosine similarity, −83% size).

| Variant | Steps | Pruned / Full | Precision | Size | Download |
| :--- | :---: | :---: | :--- | :---: | :--- |
| `fl2v v0.1` | 4 | Full | ![bf16][badge-bf16] | 1.29 GB | [![][gh-lightx2v]](https://huggingface.co/lightx2v/Minimax-h3-Turbo/resolve/main/minimax_h3_fl2v_turbo_4step_v0.1.safetensors) |
| `fl2v v1.0 768p` | 4 | Full | ![bf16][badge-bf16] | 1.29 GB | [![][gh-lightx2v]](https://huggingface.co/lightx2v/Minimax-h3-Turbo/resolve/main/minimax_h3_fl2v_turbo_4step_v1.0_768p_bf16.safetensors) |
| `fl2v v1.0 768p · comfyui` | 4 | Full | ![bf16][badge-bf16] | 1.82 GB | [![][gh-lightx2v]](https://huggingface.co/lightx2v/Minimax-h3-Turbo/resolve/main/minimax_h3_fl2v_turbo_4step_v1.0_768p_comfyui_bf16.safetensors) |
| `fl2v v1.0` | 8 | Full | ![bf16][badge-bf16] | 1.29 GB | [![][gh-lightx2v]](https://huggingface.co/lightx2v/Minimax-h3-Turbo/resolve/main/minimax_h3_fl2v_turbo_8step_v1.0_bf16.safetensors) |
| `fl2v v1.0 · comfyui` | 8 | Full | ![bf16][badge-bf16] | 1.82 GB | [![][gh-lightx2v]](https://huggingface.co/lightx2v/Minimax-h3-Turbo/resolve/main/minimax_h3_fl2v_turbo_8step_v1.0_comfyui_bf16.safetensors) |
| `fl2v v1.0 768p` | 8 | Full | ![bf16][badge-bf16] | 1.29 GB | [![][gh-lightx2v]](https://huggingface.co/lightx2v/Minimax-h3-Turbo/resolve/main/minimax_h3_fl2v_turbo_8step_v1.0_768p_bf16.safetensors) |
| `fl2v v1.0 768p · comfyui` | 8 | Full | ![bf16][badge-bf16] | 1.82 GB | [![][gh-lightx2v]](https://huggingface.co/lightx2v/Minimax-h3-Turbo/resolve/main/minimax_h3_fl2v_turbo_8step_v1.0_768p_comfyui_bf16.safetensors) |
| `fl2v v1.1 768p` | 4 | Full | ![bf16][badge-bf16] | 1.29 GB | [![][gh-lightx2v]](https://huggingface.co/lightx2v/Minimax-h3-Turbo/resolve/main/minimax_h3_fl2v_turbo_4step_v1.1_768p_bf16.safetensors) |
| `fl2v v1.1 768p · comfyui` | 4 | Full | ![bf16][badge-bf16] | 1.82 GB | [![][gh-lightx2v]](https://huggingface.co/lightx2v/Minimax-h3-Turbo/resolve/main/minimax_h3_fl2v_turbo_4step_v1.1_768p_comfyui_bf16.safetensors) |
| `fl2v v1.2 768p` | 4 | Full | ![bf16][badge-bf16] | 1.29 GB | [![][gh-lightx2v]](https://huggingface.co/lightx2v/Minimax-h3-Turbo/resolve/main/minimax_h3_fl2v_turbo_4step_v1.2_768p_bf16.safetensors) |
| `fl2v v1.2 768p · comfyui` | 4 | Full | ![bf16][badge-bf16] | 1.82 GB | [![][gh-lightx2v]](https://huggingface.co/lightx2v/Minimax-h3-Turbo/resolve/main/minimax_h3_fl2v_turbo_4step_v1.2_768p_comfyui_bf16.safetensors) |
| `ref2v v0.1` | 4 | Full | ![bf16][badge-bf16] | 1.29 GB | [![][gh-lightx2v]](https://huggingface.co/lightx2v/Minimax-h3-Turbo/resolve/main/minimax_h3_ref2v_turbo_4step_v0.1_bf16.safetensors) |
| `ref2v v0.1 · comfyui` | 4 | Full | ![bf16][badge-bf16] | 1.82 GB | [![][gh-lightx2v]](https://huggingface.co/lightx2v/Minimax-h3-Turbo/resolve/main/minimax_h3_ref2v_turbo_4step_v0.1_comfyui_bf16.safetensors) |
| `ref2v v1.0 768p` | 8 | Full | ![bf16][badge-bf16] | 1.29 GB | [![][gh-lightx2v]](https://huggingface.co/lightx2v/Minimax-h3-Turbo/resolve/main/minimax_h3_ref2v_turbo_8step_v1.0_768p_bf16.safetensors) |
| `ref2v v1.0 768p · comfyui` | 8 | Full | ![bf16][badge-bf16] | 1.82 GB | [![][gh-lightx2v]](https://huggingface.co/lightx2v/Minimax-h3-Turbo/resolve/main/minimax_h3_ref2v_turbo_8step_v1.0_768p_comfyui_bf16.safetensors) |
| `fl2v v0.1 768p · SLA` | 4 | Full | ![bf16][badge-bf16] | 1.29 GB | [![][gh-lightx2v]](https://huggingface.co/lightx2v/Minimax-h3-Turbo-SLA/resolve/main/minimax_h3_fl2v_turbo_4step_v0.1_768p_sla_bf16.safetensors) |
| `fl2v v1.0 768p · SLA · comfyui` | 4 | Full | ![bf16][badge-bf16] | 1.82 GB | [![][gh-lightx2v]](https://huggingface.co/lightx2v/Minimax-h3-Turbo-SLA/resolve/main/minimax_h3_fl2v_turbo_4step_v0.1_768p_sla_comfyui_bf16.safetensors) |
| `fl2v DasiwaREF2VAHybridV1 · curveproj1025 (T8)` · ConvRot | 4 | Full | ![int8][badge-int8] | 757.9 MB | [![][gh-t8star]](https://huggingface.co/t8star/Minimax-H3-Dasiwa-V1-Hybird-4steps/resolve/main/minimax_h3_turbo_4%E6%AD%A5%E5%8A%A0%E9%80%9F_DasiwaREF2VAHybridV1_curveproj1025_compat_v001-T8.safetensors) |
| `fl2v 8-step merge 0821` | 4→8 | Full | ![bf16][badge-bf16] | 1.96 GB | [![][gh-sonnybox]](https://huggingface.co/sonnybox/MiniMax-H3_experimental/resolve/main/loras/minimax_h3_fl2v_lightx2v_turbo_8step_merge_0821_bf16.safetensors) |
| `lightx2v v0.1` | 4 | Full | ![bf16][badge-bf16] | 1.82 GB | [![][gh-Kijai]](https://huggingface.co/Kijai/MiniMax-H3_comfy/resolve/main/loras/minimax_h3_fl2v_lightx2v_turbo_4step_v0.1_comfy.safetensors) |
| `lightx2v v0.1 · resized` | 4 | Full | ![bf16][badge-bf16] | 300 MB | [![][gh-Kijai]](https://huggingface.co/Kijai/MiniMax-H3_comfy/resolve/main/loras/minimax_h3_fl2v_lightx2v_turbo_4step_v0.1_comfy_resized_avg_rank_21_bf16.safetensors) |
| `fl2v` | 4 | Full | ![bf16][badge-bf16] | 744 MB | [![][gh-larryvrh]](https://huggingface.co/larryvrh/MiniMax-H3-Turbo-Lora/resolve/main/minimax_h3_turbo_4step.safetensors) |
| `fl2v ema` | 4 | Full | ![bf16][badge-bf16] | 744 MB | [![][gh-larryvrh]](https://huggingface.co/larryvrh/MiniMax-H3-Turbo-Lora/resolve/main/minimax_h3_turbo_4step_ema.safetensors) |
| `fl2v ckpt500` | 4 | Full | ![bf16][badge-bf16] | 744 MB | [![][gh-larryvrh]](https://huggingface.co/larryvrh/MiniMax-H3-Turbo-Lora/resolve/main/minimax_h3_turbo_4step_ckpt500.safetensors) |
| `fl2v ema ckpt500` | 4 | Full | ![bf16][badge-bf16] | 744 MB | [![][gh-larryvrh]](https://huggingface.co/larryvrh/MiniMax-H3-Turbo-Lora/resolve/main/minimax_h3_turbo_4step_ema_ckpt500.safetensors) |
| `fl2v ckpt850` | 4 | Full | ![bf16][badge-bf16] | 744 MB | [![][gh-larryvrh]](https://huggingface.co/larryvrh/MiniMax-H3-Turbo-Lora/resolve/main/minimax_h3_turbo_4step_ckpt850.safetensors) |
| `fl2v ema ckpt850` | 4 | Full | ![bf16][badge-bf16] | 744 MB | [![][gh-larryvrh]](https://huggingface.co/larryvrh/MiniMax-H3-Turbo-Lora/resolve/main/minimax_h3_turbo_4step_ema_ckpt850.safetensors) |
| `fl2v v4 step600` | 4 | Full | ![bf16][badge-bf16] | 744 MB | [![][gh-larryvrh]](https://huggingface.co/larryvrh/MiniMax-H3-Turbo-Lora/resolve/main/minimax_h3_turbo_v4_step600.safetensors) |
| `fl2v v4 step600 ema` | 4 | Full | ![bf16][badge-bf16] | 744 MB | [![][gh-larryvrh]](https://huggingface.co/larryvrh/MiniMax-H3-Turbo-Lora/resolve/main/minimax_h3_turbo_v4_step600_ema.safetensors) |
| `fl2v pruned` | 4 | Pruned | ![bf16][badge-bf16] | 592 MB | [![][gh-drbaph]](https://huggingface.co/drbaph/MiniMax-H3-Turbo-Lora-ComfyUI/resolve/main/minimax_h3_turbo_4step_pruned_comfyui.safetensors) |
| `fl2v pruned ema` | 4 | Pruned | ![bf16][badge-bf16] | 592 MB | [![][gh-drbaph]](https://huggingface.co/drbaph/MiniMax-H3-Turbo-Lora-ComfyUI/resolve/main/minimax_h3_turbo_4step_ema_pruned_comfyui.safetensors) |
| `fl2v pruned ckpt500` | 4 | Pruned | ![bf16][badge-bf16] | 592 MB | [![][gh-drbaph]](https://huggingface.co/drbaph/MiniMax-H3-Turbo-Lora-ComfyUI/resolve/main/minimax_h3_turbo_4step_ckpt500_pruned_comfyui.safetensors) |
| `fl2v pruned ema ckpt500` | 4 | Pruned | ![bf16][badge-bf16] | 592 MB | [![][gh-drbaph]](https://huggingface.co/drbaph/MiniMax-H3-Turbo-Lora-ComfyUI/resolve/main/minimax_h3_turbo_4step_ema_ckpt500_pruned_comfyui.safetensors) |
| `fl2v pruned ckpt850` | 4 | Pruned | ![bf16][badge-bf16] | 592 MB | [![][gh-drbaph]](https://huggingface.co/drbaph/MiniMax-H3-Turbo-Lora-ComfyUI/resolve/main/minimax_h3_turbo_4step_ckpt850_pruned_comfyui.safetensors) |
| `fl2v pruned ema ckpt850` | 4 | Pruned | ![bf16][badge-bf16] | 592 MB | [![][gh-drbaph]](https://huggingface.co/drbaph/MiniMax-H3-Turbo-Lora-ComfyUI/resolve/main/minimax_h3_turbo_4step_ema_ckpt850_pruned_comfyui.safetensors) |
| `fl2v pruned v4 step600` | 4 | Pruned | ![bf16][badge-bf16] | 592 MB | [![][gh-drbaph]](https://huggingface.co/drbaph/MiniMax-H3-Turbo-Lora-ComfyUI/resolve/main/minimax_h3_turbo_v4_step600_pruned_comfyui.safetensors) |
| `fl2v pruned v4 step600 ema` | 4 | Pruned | ![bf16][badge-bf16] | 592 MB | [![][gh-drbaph]](https://huggingface.co/drbaph/MiniMax-H3-Turbo-Lora-ComfyUI/resolve/main/minimax_h3_turbo_v4_step600_ema_pruned_comfyui.safetensors) |
| `fl2v v0.1 768p · SLA · resized r28` | 4 | Full | ![bf16][badge-bf16] | 375 MB | [![][gh-drbaph]](https://huggingface.co/drbaph/MiniMax-H3-Turbo-Lora-ComfyUI/resolve/main/minimax_h3_fl2v_turbo_4step_v0.1_768p_sla_comfyui_resized_avg_rank_28_bf16.safetensors) |
| `fl2v v0.1 768p · SLA · resized r64` | 4 | Full | ![bf16][badge-bf16] | 891 MB | [![][gh-drbaph]](https://huggingface.co/drbaph/MiniMax-H3-Turbo-Lora-ComfyUI/resolve/main/minimax_h3_fl2v_turbo_4step_v0.1_768p_sla_comfyui_resized_avg_rank_64_bf16.safetensors) |
| `fl2v v1.0 768p · resized r21` | 4 | Full | ![bf16][badge-bf16] | 284 MB | [![][gh-drbaph]](https://huggingface.co/drbaph/MiniMax-H3-Turbo-Lora-ComfyUI/resolve/main/minimax_h3_fl2v_turbo_4step_v1.0_768p_comfyui_resized_avg_rank_21_bf16.safetensors) |
| `fl2v v1.0 · resized r21` | 8 | Full | ![bf16][badge-bf16] | 312 MB | [![][gh-drbaph]](https://huggingface.co/drbaph/MiniMax-H3-Turbo-Lora-ComfyUI/resolve/main/minimax_h3_fl2v_turbo_8step_v1.0_comfyui_resized_avg_rank_21_bf16.safetensors) |
| `fl2v v1.1 768p · resized r28` | 4 | Full | ![bf16][badge-bf16] | 376 MB | [![][gh-drbaph]](https://huggingface.co/drbaph/MiniMax-H3-Turbo-Lora-ComfyUI/resolve/main/minimax_h3_fl2v_turbo_4step_v1.1_768p_comfyui_resized_avg_rank_28_bf16.safetensors) |
| `fl2v v1.1 768p · resized r64` | 4 | Full | ![bf16][badge-bf16] | 892 MB | [![][gh-drbaph]](https://huggingface.co/drbaph/MiniMax-H3-Turbo-Lora-ComfyUI/resolve/main/minimax_h3_fl2v_turbo_4step_v1.1_768p_comfyui_resized_avg_rank_64_bf16.safetensors) |
| `fl2v v1.2 768p · resized r20` | 4 | Full | ![bf16][badge-bf16] | 291 MB | [![][gh-drbaph]](https://huggingface.co/drbaph/MiniMax-H3-Turbo-Lora-ComfyUI/resolve/main/minimax_h3_fl2v_turbo_4step_v1.2_768p_comfyui_resized_avg_rank_20_bf16.safetensors) |
| `fl2v v1.2 768p · resized r64` | 4 | Full | ![bf16][badge-bf16] | 929 MB | [![][gh-drbaph]](https://huggingface.co/drbaph/MiniMax-H3-Turbo-Lora-ComfyUI/resolve/main/minimax_h3_fl2v_turbo_4step_v1.2_768p_comfyui_resized_avg_rank_64_bf16.safetensors) |
| `fl2v v1.0 768p 8-step · resized r20` | 8 | Full | ![bf16][badge-bf16] | 291 MB | [![][gh-drbaph]](https://huggingface.co/drbaph/MiniMax-H3-Turbo-Lora-ComfyUI/resolve/main/minimax_h3_fl2v_turbo_8step_v1.0_768p_comfyui_resized_avg_rank_20_bf16.safetensors) |
| `fl2v v1.0 768p 8-step · resized r64` | 8 | Full | ![bf16][badge-bf16] | 927 MB | [![][gh-drbaph]](https://huggingface.co/drbaph/MiniMax-H3-Turbo-Lora-ComfyUI/resolve/main/minimax_h3_fl2v_turbo_8step_v1.0_768p_comfyui_resized_avg_rank_64_bf16.safetensors) |
| `ref2v v0.1 · resized r21` | 4 | Full | ![bf16][badge-bf16] | 312 MB | [![][gh-drbaph]](https://huggingface.co/drbaph/MiniMax-H3-Turbo-Lora-ComfyUI/resolve/main/minimax_h3_ref2v_turbo_4step_v0.1_comfyui_resized_avg_rank_21_bf16.safetensors) |
| `ref2v v1.0 768p 8-step · resized r20` | 8 | Full | ![bf16][badge-bf16] | 291 MB | [![][gh-drbaph]](https://huggingface.co/drbaph/MiniMax-H3-Turbo-Lora-ComfyUI/resolve/main/minimax_h3_ref2v_turbo_8step_v1.0_768p_comfyui_resized_avg_rank_20_bf16.safetensors) |
| `ref2v v1.0 768p 8-step · resized r64` | 8 | Full | ![bf16][badge-bf16] | 933 MB | [![][gh-drbaph]](https://huggingface.co/drbaph/MiniMax-H3-Turbo-Lora-ComfyUI/resolve/main/minimax_h3_ref2v_turbo_8step_v1.0_768p_comfyui_resized_avg_rank_64_bf16.safetensors) |
| `HyperFlow 8-step v1.0` · official · ⚠️ needs the HyperFlow loader | 8 | Full | ![bf16][badge-bf16] | 2.60 GB | [![][gh-videorebirth]](https://huggingface.co/videorebirth/hyperflow/resolve/main/minimax_h3_hyperflow_8step_v1.0.safetensors) |
| `HyperFlow 8-step v1.0` · ComfyUI conversion | 8 | Full | ![bf16][badge-bf16] | 3.66 GB | [![][gh-drbaph]](https://huggingface.co/drbaph/MiniMax-H3-Turbo-Lora-ComfyUI/resolve/main/minimax_h3_hyperflow_8step_v1.0_comfyui_bf16.safetensors) |
| `HyperFlow 8-step v1.0` · ComfyUI · resized r20 | 8 | Full | ![bf16][badge-bf16] | 303 MB | [![][gh-drbaph]](https://huggingface.co/drbaph/MiniMax-H3-Turbo-Lora-ComfyUI/resolve/main/minimax_h3_hyperflow_8step_v1.0_comfyui_bf16_resized_avg_rank_20_bf16.safetensors) |
| `HyperFlow 8-step v1.0` · ComfyUI pruned | 8 | Pruned | ![bf16][badge-bf16] | 3.64 GB | [![][gh-drbaph]](https://huggingface.co/drbaph/MiniMax-H3-Turbo-Lora-ComfyUI/resolve/main/minimax_h3_hyperflow_8step_v1.0_comfyui_pruned_bf16.safetensors) |
| `HyperFlow 8-step v1.0` · ComfyUI pruned · resized r20 | 8 | Pruned | ![bf16][badge-bf16] | 301 MB | [![][gh-drbaph]](https://huggingface.co/drbaph/MiniMax-H3-Turbo-Lora-ComfyUI/resolve/main/minimax_h3_hyperflow_8step_v1.0_comfyui_pruned_bf16_resized_avg_rank_20_bf16.safetensors) |
| `fl2v VDN-H3 8-step DMD extract` · experimental | 8 | Full | ![bf16][badge-bf16] | 2.12 GB | [![][gh-drbaph]](https://huggingface.co/drbaph/MiniMax-H3-Turbo-Lora-ComfyUI/resolve/main/experimental/minimax_h3_dmd_8step_turbo.safetensors) |
| `fl2v VDN-H3 8-step DMD extract · pruned` | 8 | Pruned | ![bf16][badge-bf16] | 2.13 GB | [![][gh-drbaph]](https://huggingface.co/drbaph/MiniMax-H3-Turbo-Lora-ComfyUI/resolve/main/experimental/minimax_h3_dmd_fl2va_8step_turbo_pruned.safetensors) |
| `ref2v VDN-H3 8-step DMD extract · pruned` | 8 | Pruned | ![bf16][badge-bf16] | 2.13 GB | [![][gh-drbaph]](https://huggingface.co/drbaph/MiniMax-H3-Turbo-Lora-ComfyUI/resolve/main/experimental/minimax_h3_dmd_ref2va_8step_turbo_pruned.safetensors) |
| `fl2v TaoMate 3-step EMA` · experimental | 3 | Pruned | ![bf16][badge-bf16] | 2.31 GB | [![][gh-drbaph]](https://huggingface.co/drbaph/MiniMax-H3-Turbo-Lora-ComfyUI/resolve/main/experimental/minimax_h3_taomate_fl2va_3step_ema_comfyui.safetensors) |
| `FLF HardGravy 6-step turbo merge v0.1` | 6 | Pruned | ![bf16][badge-bf16] | 592 MB | [![][gh-HardGravy2]](https://huggingface.co/HardGravy2/Minimax_H3_FLF_HardGravy_6_Step_Turbo_Merge/resolve/main/h3_hard_gravy_6stepturbo_r64_v0.1.safetensors) |
| `FLF HardGravy 6-step turbo merge v1.0` | 6 | Pruned | ![bf16][badge-bf16] | 592 MB | [![][gh-HardGravy2]](https://huggingface.co/HardGravy2/Minimax_H3_FLF_HardGravy_6_Step_Turbo_Merge/resolve/main/h3_hard_gravy_6stepturbo_r64_v1.0.safetensors) |
| `fl2v v0.1 · comfy fro v4` | 4 | Full | ![bf16][badge-bf16] | 542 MB | [![][gh-silveroxides]](https://huggingface.co/silveroxides/MiniMax-H3_tests/resolve/main/minimax_h3_fl2v_lightx2v_turbo_4step_v0.1_comfy_fro_v4.safetensors) |
| `fl2v dareties v4 step600 · comfy fro` | 4→8 | Full | ![bf16][badge-bf16] | 827 MB | [![][gh-silveroxides]](https://huggingface.co/silveroxides/MiniMax-H3_tests/resolve/main/minimax_h3_fl2v_lightx2v_v0.1_dareties_v4_step600_comfy_fro.safetensors) |
| `fl2v 4→8-step dareties · v0.1–v1.0 768p` | 4→8 | Full | ![bf16][badge-bf16] | 1.97 GB | [![][gh-silveroxides]](https://huggingface.co/silveroxides/MiniMax-H3_tests/resolve/main/experimental/minimax_h3_fl2v_lightx2v_turbo_4to8step_v0.1-v1.0_768p_v4_step600_dareties.safetensors) |
| `fl2v 4→8-step dareties · fro095` | 4→8 | Full | ![bf16][badge-bf16] | 972 MB | [![][gh-silveroxides]](https://huggingface.co/silveroxides/MiniMax-H3_tests/resolve/main/experimental/minimax_h3_fl2v_lightx2v_turbo_4to8step_v0.1-v1.0_768p_v4_step600_dareties_fro095.safetensors) |
| `fl2v 4→8-step dareties fro095 · native port` | 4→8 | Full | ![bf16][badge-bf16] | 911 MB | [![][gh-Rkss]](https://huggingface.co/Rkss/Minimax_h3_fl2v_lightx2v_turbo_4to8step_768p_v4_step600_dareties_native/resolve/main/minimax_h3_fl2v_lightx2v_turbo_4to8step_v0.1-v1.0_768p_v4_step600_dareties_fro095_native.safetensors) |
| `fl2v 4→8-step dareties fro095 · native pruned` | 4→8 | Pruned | ![bf16][badge-bf16] | 819 MB | [![][gh-Rkss]](https://huggingface.co/Rkss/Minimax_h3_fl2v_lightx2v_turbo_4to8step_768p_v4_step600_dareties_native/resolve/main/minimax_h3_fl2v_lightx2v_turbo_4to8step_v0.1-v1.0_768p_v4_step600_dareties_fro095_pruned.safetensors) |
| `fl2v multistep delta cwb 7-contrib fro0995 · native pruned` | 4→8 | Pruned | ![bf16][badge-bf16] | 1.4 GB | [![][gh-Rkss]](https://huggingface.co/Rkss/Minimax_h3_fl2v_lightx2v_turbo_4to8step_768p_v4_step600_dareties_native/resolve/main/minimax_h3_fl2va_turbo_multistep_v4_step600_delta_cwb_7_contrib_fro0995_pruned.safetensors) |
| `fl2v turbo silver dareties · full v1` | 4→8 | Full | ![bf16][badge-bf16] | 791 MB | [![][gh-silveroxides]](https://huggingface.co/silveroxides/MiniMax-H3_tests/resolve/main/minimax_h3_fl2v_turbo_silver_dareties_comfy_full_v1.safetensors) |
| `fl2v turbo silver dareties · pruned v1` | 4→8 | Pruned | ![bf16][badge-bf16] | 730 MB | [![][gh-silveroxides]](https://huggingface.co/silveroxides/MiniMax-H3_tests/resolve/main/minimax_h3_fl2v_turbo_silver_dareties_comfy_pruned_v1.safetensors) |
| `lightx2v hybrid 4→8-step Turbo r48` · Shenanigans | 4→8 | Full | ![bf16][badge-bf16] | 900 MB | [![][gh-TenStrip]](https://huggingface.co/TenStrip/MinimaxH3-Turbo_Shenanigans/resolve/main/lightx2v_hybrid-4to8step-Turbo_r48.safetensors) |
| `lightx2v hybrid 4→8-step full-fusion Turbo` · Shenanigans | 4→8 | Pruned | ![bf16][badge-bf16] | 4.15 GB | [![][gh-TenStrip]](https://huggingface.co/TenStrip/MinimaxH3-Turbo_Shenanigans/resolve/main/lightx2v_hybrid-4to8step-full-fusion_Turbo_pruned.safetensors) |
| `fl2v pruned ckpt500 V1` | 4 | Pruned | ![bf16][badge-bf16] | 592 MB | [![][gh-Abiray]](https://huggingface.co/Abiray/MiniMax-H3-Turbo-Lora-Pruned-ComfyUI/resolve/main/minimax_h3_turbo_4step_ckpt500_V1.safetensors) |
| `fl2v pruned ckpt600 V4` | 4 | Pruned | ![bf16][badge-bf16] | 592 MB | [![][gh-Abiray]](https://huggingface.co/Abiray/MiniMax-H3-Turbo-Lora-Pruned-ComfyUI/resolve/main/minimax_h3_turbo_4step_ckpt600_V4.safetensors) |
| `fl2v pruned ckpt600 ema V4` | 4 | Pruned | ![bf16][badge-bf16] | 592 MB | [![][gh-Abiray]](https://huggingface.co/Abiray/MiniMax-H3-Turbo-Lora-Pruned-ComfyUI/resolve/main/minimax_h3_turbo_4step_ckpt600_ema_V4.safetensors) |
| `fl2v pruned ckpt850 V1` | 4 | Pruned | ![bf16][badge-bf16] | 592 MB | [![][gh-Abiray]](https://huggingface.co/Abiray/MiniMax-H3-Turbo-Lora-Pruned-ComfyUI/resolve/main/minimax_h3_turbo_4step_ckpt850_V1.safetensors) |
| `fl2v` | 4 | Full | ![bf16][badge-bf16] | 717 MB | [![][gh-joyfox]](https://huggingface.co/joyfox/MiniMax-H3-Turbo/resolve/main/minimax_h3_fl2va_4step_lora.safetensors) |
| `fl2v step 100` | 8 NFE | Full | ![bf16][badge-bf16] | 738 MB | [![][gh-tutututututu]](https://huggingface.co/tutututututu/Tutu-MiniMax-H3-AudioVideo-20to8-NFE-LoRA/resolve/main/comfyui/tutu-t8-minimax-h3-av-20to8-nfe-lora-step000100-bf16-comfyui.safetensors) |
| `fl2v step 200` | 8 NFE | Full | ![bf16][badge-bf16] | 738 MB | [![][gh-tutututututu]](https://huggingface.co/tutututututu/Tutu-MiniMax-H3-AudioVideo-20to8-NFE-LoRA/resolve/main/comfyui/tutu-t8-minimax-h3-av-20to8-nfe-lora-step000200-bf16-comfyui.safetensors) |
| `fl2v step 300` | 8 NFE | Full | ![bf16][badge-bf16] | 738 MB | [![][gh-tutututututu]](https://huggingface.co/tutututututu/Tutu-MiniMax-H3-AudioVideo-20to8-NFE-LoRA/resolve/main/comfyui/tutu-t8-minimax-h3-av-20to8-nfe-lora-step000300-bf16-comfyui.safetensors) |
| `fl2v 4-step acceleration` · ConvRot · ⚠️ needs dual-clock sampler or 8–10 steps | 4 | Full | ![int8][badge-int8] | 779.9 MB | [![][gh-t8star]](https://huggingface.co/t8star/minimax-h3-4step-turbo-loras-comfyui-exp/resolve/main/minimax_h3_turbo_4%E6%AD%A5%E5%8A%A0%E9%80%9F_comfyui.safetensors) |
| `fl2v 4-step acceleration ema` · ConvRot | 4 | Full | ![int8][badge-int8] | 779.9 MB | [![][gh-t8star]](https://huggingface.co/t8star/minimax-h3-4step-turbo-loras-comfyui-exp/resolve/main/minimax_h3_turbo_4%E6%AD%A5%E5%8A%A0%E9%80%9Fema_comfyui.safetensors) |
| `fl2v v4 step600 (T8-convert)` · ConvRot | 4 | Full | ![int8][badge-int8] | 779.9 MB | [![][gh-t8star]](https://huggingface.co/t8star/minimax-h3-4step-turbo-loras-comfyui-exp/resolve/main/minimax_h3_turbo_v4_step600_comfyui_T8-convert.safetensors) |
| `lightx2v v0.1 · alpha8 T8-convert` · ConvRot · ⚠️ needs dual-clock sampler or 8–10 steps  | 4 | Full | ![int8][badge-int8]| 1.96 GB | [![][gh-t8star]](https://huggingface.co/t8star/minimax_h3_fl2v_turbo_4step_v0.1_comfyui_alpha8-T8-convert/resolve/main/minimax_h3_fl2v_turbo_4step_v0.1_comfyui_alpha8-T8-convert.safetensors) |
| `fl2v 10ErosMax test4 · 4-step curveproj1025 (T8)` · ConvRot · ⚠️ needs dual-clock sampler or 8–10 steps  | 4 | Pruned | ![int8][badge-int8] | 794.9 MB | [![][gh-t8star]](https://huggingface.co/t8star/minimax_h3_turbo_4step_10ErosMax_test4_pruned_curveproj1025_T8/resolve/main/minimax_h3_turbo_4step_10ErosMax_test4_pruned_curveproj1025_exp_v001-T8.safetensors) |
| `fl2v 10ErosMax test4 · 4-step curveproj1025` | 4 | Pruned | ![int8][badge-int8] | 794.9 MB | [![][gh-t8star]](https://huggingface.co/t8star/minimax_h3_turbo_4step_10ErosMax_test4_pruned_curveproj1025_T8/resolve/main/minimax_h3_turbo_4step_10ErosMax_test4_pruned_curveproj1025_exp_v001.safetensors) |
| `fl2v 10ErosMax test4 · 8-step v1.0` · ConvRot | 8 | Pruned | ![int8][badge-int8]  | 1.96 GB | [![][gh-t8star]](https://huggingface.co/t8star/minimax_h3_turbo_4step_10ErosMax_test4_pruned_curveproj1025_T8/resolve/main/minimax_h3_fl2v_turbo_8step_v1.0_10ErosMax_beta1_pruned_compat_v001_T8.safetensors) |
| `fl2v CMF · full` | 4 | Full | Q4TP (CMF) | 25.20 GB | [![][gh-infosave]](https://huggingface.co/infosave/MiniMax-H3-Turbo-cmf/resolve/main/mmh3-turbo-q4tp.cmf) |
| `fl2v CMF · FL2VA` | 4 | Full | Q4TP (CMF) | 25.70 GB | [![][gh-infosave]](https://huggingface.co/infosave/MiniMax-H3-Turbo-cmf/resolve/main/mmh3-turbo-fl2va-q4tp.cmf) |
| `fl2v CMF · FL2VA (smaller)` | 4 | Full | Q2TP (CMF) | 20.12 GB | [![][gh-infosave]](https://huggingface.co/infosave/MiniMax-H3-Turbo-cmf/resolve/main/mmh3-turbo-fl2va-q2tp.cmf) |
| `fl2v v1.0 768p` · ConvRot · needs ComfyUI-LoraInt8Loader | 4 | Full | ![int8][badge-int8]  | 991 MB | [![][gh-rzgar]](https://huggingface.co/rzgar/minimax_h3_fl2v_lightx2v_4step_int8-convrot_comfy/resolve/main/minimax_h3_fl2v_turbo_4step_v1.0_768p_comfyui_bf16_int8convrot.safetensors) |
| `fl2v v1.0` · ConvRot · needs ComfyUI-LoraInt8Loader | 8 | Full | ![int8][badge-int8] | 991 MB | [![][gh-rzgar]](https://huggingface.co/rzgar/minimax_h3_fl2v_lightx2v_4step_int8-convrot_comfy/resolve/main/minimax_h3_fl2v_turbo_8step_v1.0_comfyui_bf16_int8convrot.safetensors) |
| `lightx2v v0.1 · int8` · ConvRot · needs ComfyUI-LoraInt8Loader | 4 | Full | ![int8][badge-int8] | 991 MB | [![][gh-rzgar]](https://huggingface.co/rzgar/minimax_h3_fl2v_lightx2v_4step_int8-convrot_comfy/resolve/main/minimax_h3_lightx2v_turbo_4step_v0.1_comfy_int8convrot.safetensors) |
| `flashgen v1.0 768p` · T2VA · ⚠️ Ascend NPU / MindIE-SD / vllm-omni target (merge via `merge_lora_ckpt.py`) | 4 | Full | ![bf16][badge-bf16] | 1.26 GB | [![][gh-Beidouqixing]](https://huggingface.co/Beidouqixing/minimax-h3-4step-lora-flashgen/resolve/main/minimax_h3_4step_lora_flashgen_v1.0_768p_bf16.safetensors) |
| `fl2va Acc 8-step` · PDD (Parallel Decoding Distillation) | 8 NFE | Full | ![bf16][badge-bf16] | 1.28 GB | [![][gh-alibaba-pai]](https://huggingface.co/alibaba-pai/MiniMax-H3-Acc-LoRAs/resolve/main/MiniMax-H3-FL2VA-Acc-8Step.safetensors) |
| `ref2va Acc 8-step` · PDD (Parallel Decoding Distillation) | 8 NFE | Full | ![bf16][badge-bf16] | 1.28 GB | [![][gh-alibaba-pai]](https://huggingface.co/alibaba-pai/MiniMax-H3-Acc-LoRAs/resolve/main/MiniMax-H3-Ref2VA-Acc-8Step.safetensors) |
| `fl2v Dense 4-step v1` · ComfyUI-pruned | 4 | Pruned | ![bf16][badge-bf16] | 1018 MB | [![][gh-Hippotes]](https://huggingface.co/Hippotes/MiniMax-H3-Experiments/resolve/main/FastH3-Dense-4-step-v1-LoRA-ComfyUI-pruned.safetensors) |
| `fl2v VSA-DataFree 4-step` · ⚠️ needs [companion node](https://github.com/barelymining/ComfyUI-MiniMax-H3-FastVideo) | 4 | Pruned | ![bf16][badge-bf16] | 2.05 GB | [![][gh-barelymining]](https://huggingface.co/barelymining/ComfyUI-MiniMax-H3-FastVideo/resolve/main/fasth3_vsa_4-steps-v5.safetensors) + [gate 3.59 GB](https://huggingface.co/barelymining/ComfyUI-MiniMax-H3-FastVideo/resolve/main/fasth3_vsa_gate.safetensors) |
| `fl2v FastH3-Preview v0.2 extract · pruned r128 (recommended)` | 4 | Pruned | ![fp16][badge-fp16] | 1.24 GB | [![][gh-drozbay]](https://huggingface.co/drozbay/MiniMax-H3-FastH3-Preview-LoRA/resolve/main/loras/minimax_h3_fl2va_fasth3_preview_v0.2_lora_pruned_rank128_fp16.safetensors) |
| `fl2v FastH3-Preview v0.2 extract · pruned r64` | 4 | Pruned | ![fp16][badge-fp16] | 678 MB | [![][gh-drozbay]](https://huggingface.co/drozbay/MiniMax-H3-FastH3-Preview-LoRA/resolve/main/loras/minimax_h3_fl2va_fasth3_preview_v0.2_lora_pruned_rank64_fp16.safetensors) |
| `fl2v FastH3-Preview v0.2 extract · full r256` | 4 | Full | ![fp16][badge-fp16] | 4.71 GB | [![][gh-drozbay]](https://huggingface.co/drozbay/MiniMax-H3-FastH3-Preview-LoRA/resolve/main/loras/minimax_h3_fl2va_fasth3_preview_v0.2_lora_full_max256_avg253_fp16.safetensors) |
| `DMAD 4-step` · paper checkpoint (LoRA critic, EMA iter 800) · ⚠️ needs the DMAD inference script | 4 | Full | ![bf16][badge-bf16] | 1.29 GB | [![][gh-ZhengmingYu]](https://huggingface.co/ZhengmingYu/DMAD/resolve/main/minimax_h3/dmad_minimax_h3_4step_lora_critic.safetensors) |
| `DMAD 4-step` · full-critic variant (live iter 1600, higher AVGen-Bench) · ⚠️ needs the DMAD inference script | 4 | Full | ![bf16][badge-bf16] | 1.29 GB | [![][gh-ZhengmingYu]](https://huggingface.co/ZhengmingYu/DMAD/resolve/main/minimax_h3/dmad_minimax_h3_4step_full_critic.safetensors) |

*larryvrh also publishes experimental training checkpoints (11 `.bin` files: step 149/490/729/850/922, v2 step 298, v3 step 300, v4 step 150/600, v5 step 600; 7.26–10.17 GB) — see the [repo](https://huggingface.co/larryvrh/MiniMax-H3-Turbo-Lora/tree/main).*

*■ **DMAD** — *Distribution Matching as Adversarial Distillation* (ZhengmingYu, [arXiv:2610.02188](https://arxiv.org/abs/2610.02188), [code](https://github.com/Yzmblog/DMAD), Apache-2.0, 91 stars) is the most rigorously documented accelerator in this table — but it is **not a drop-in ComfyUI LoRA**. Rank **128** (alpha 128) across **312 modules** — all 50 DiT attention projections (`to_q`/`to_k`/`to_v`/`to_out.0`) plus both FFN projections (`ff.net.0.proj`/`ff.net.2`) and both token-refiner blocks — distilling a 50-step teacher into a **4-step** student at 1344×768 / 124 frames / 24 fps (5.2 s) with native 32 kHz stereo audio. Two critic regimes ship: `lora_critic` (paper checkpoint, critic backbone frozen under a LoRA, EMA student at iteration 800) and `full_critic` (critic backbone fully trained, live weights at iteration 1600) which the authors say **scores higher on AVGen-Bench** — though no numeric scores are published. Human preference over the 50-step teacher is reported as **79.1% vs DMD2** and **84.6% vs rCM** (ties excluded); no teacher latency is given, so treat "12.5×" as *fewer model evaluations* (50→4), **not** a measured speedup. Measured: **37 s/video on an H200**; ~4 min on a 4090/5090, ~8 min on a 3090 (estimates). `--low-vram` runs on a 24 GB card (12.9 GiB sampling peak, 3.4 GiB text encode, 8.6 GiB BF16 decode vs 14.2 GiB FP32), but needs ~5–7 GB/s of NVMe/host bandwidth to hide weight streaming, and `--weights-int8` **changes the sample** (14–26 dB PSNR vs exact, mean 19.6 dB) because 4-step sampling amplifies small weight changes. ⚠️ **Requires the repo's own `inference.py`** — it uses a custom **re-noise** step rule the students were trained with; the stock Diffusers pipeline defaults to Euler and therefore does **not** reproduce the paper's samples. No ComfyUI node or workflow exists. Prompt structure matters: H3 expects long structured prompts (`integrated_multimodal_description:`, `overall_soundscape:`, `non_diegetic_music:`). No classifier-free guidance (the base model is guidance-distilled). Frames must be `17n + 5`; the base download is ~170 GB.*

*drbaph's `experimental/` folder holds two extract families, now documented in the repo README: **VDN-H3 8-step extracts** — LoRAs extracted from the [VDN-H3](#vdn-h3-video-deltanet) 8-step DMD stage (a full-layout FL2VA file working on both FL2VA and Ref2VA, plus pruned FL2VA / Ref2VA variants that need their matching pruned base; 2.12–2.13 GB), and a **TaoMate 3-step EMA** conversion of Alibaba's [TaoMate-H3](#taomate-h3) streaming adapter (2.31 GB; recommended manual sigmas: 3-step `1.0, 0.961165, 0.853333, 0.0`, 4-step `1.0, 0.970874, 0.907249, 0.640000, 0.0`).*

*[videorebirth/hyperflow](https://huggingface.co/videorebirth/hyperflow) is Video Rebirth's **official 8-step flow self-distillation** for H3 — PEFT rank 256 / alpha 256 across 316 modules (attention, feed-forward, both time embedders), one file covering `t2va` / `fl2va` / `ref2va`, about 3× end-to-end against the 49-NFE Diffusers baseline. It is **not a drop-in LoRA**: the file carries keys for a second time embedder that only exists once the [Video-Rebirth/hyperflow](https://github.com/Video-Rebirth/hyperflow) loader has installed it (`load_hyperflow_lora`, not diffusers' `load_lora_weights`). drbaph's `…_comfyui_…` conversions above instead take a manual 9-point sigma schedule — `1.0, 0.9939097854, 0.9842874953, 0.9660637197, 0.9230769231, 0.8349423898, 0.6968520491, 0.4687533149, 0.0` (8 steps; euler/simple normal also works) — with the non-`pruned` files for the full base and the `pruned` ones for the pruned/curve-form base. ⚠️ License: MiniMax H3 Community License Agreement with territorial limits — not licensed in the EU, UK, South Korea or the US without MiniMax's separate authorization.*

*HardGravy2's 6-step rank-64 merge combines lightx2v + larryvrh turbo LoRAs with JonXL's photorealism LoRA (merge formula unpublished). Author-tested on the pruned INT8 ConvRot FL2VA with Spectrum + SLA, euler/simple, 6 steps, shift unset (`h3_fast.json` workflow included; ~330 s per 10 s of 0.5 MP output on a 16 GB A4000) — reports improved audio/video quality and prompt adherence over any single trained turbo. MiniMax H3 Community License.*

*[vladmandic/MiniMax-H3-Turbo-LoRA](https://huggingface.co/vladmandic/MiniMax-H3-Turbo-LoRA) is a **diffusers-format mirror collection** rather than a new training run: 11 renamed copies of the turbo LoRAs already listed above (lightx2v ×5, larryvrh ×3, silveroxides ×2, plus `alibaba-pai_pdd-fl2va-8step` / `pdd-ref2va-8step`), curated by the SD.Next author with side-by-side test grids (no-LoRA / larryvrh / lightx2v / silveroxides / TaoMate / alibaba). Handy as one-stop `from_pretrained` downloads — the upstream repos remain the source of truth. Apache-2.0. Sizes 1.3–1.8 GB.*

*silveroxides/MiniMax-H3_tests is the busiest single-author experiment hub in the ecosystem and is **not** fully enumerated above — beyond the rows listed, the repo carries: the `dareties_pruned/` (rev1–6, 360–739 MB) and `dareties_resize/` (rev2–6, 385–560 MB) revision ladders of the dareties FL2V LoRA; the `ref2v_dareties/` Ref2V ladder (fro095–fro0995, 569 MB–1.1 GB); the `experimental/` **multistep delta `cwb` 7-contrib** family (fro0980/0990/0995/0999/09999 + un-truncated bf16, 1.5–7.0 GB), a `duo_lightx2v … 4step cwb custom fro09675` file (557 MB), and a 93.5 MB `turbo_v4_step600_ema_adaln_proj_only_pruned` AdaLN-only extract; a `depr/` folder of superseded v0.1–v3 builds; the three rev6 `daretiessquared` dareties variants (full-adaln 791 MB / pruned-adaln 730 MB / no-adaln 638 MB); mirrors of FastVideo's FastH3 preview files (`fastvideo_fasth3/…_lora_comfyui` 5.2 GB, an INT8 ConvRot VSA-datafree build 35.3 GB, and a mis-uploaded 65.3 GB file explicitly tagged `[INVALID]` in its filename); the same 10 Comfy-Org concept embeddings under `embeddings/`; and a `viggle-animate-quant/` INT8 ConvRot conversion of the Viggle-Animate ref2va transformer (31.7 GB).*


<p id="quants" align="center">══════════════════════════════════</p>

### ▣ Quantized Models

Unified quantization tables for FL2VA and Ref2VA. The **Pruned** column marks whether the checkpoint is AdaLN-pruned (smaller, ComfyUI-only). The **Method** column identifies the quantization scheme. Multiple sources for the same quant are separated by `┊`.

**Key:** ConvRot = ConvRotation INT8/INT4 quantization · Lean = selective BF16 island retention · DT-sQKV = Dynamic-Time separate-QKV (patch required) · W4A8 = 4-bit weight / 8-bit activation · GGUF = llama.cpp GGUF format · NF4 = bitsandbytes 4-bit · OrbitQuant = native W4A4 packed path · Hybrid = partial NVFP4 layers on Blackwell.

*Items marked ⚠️ require a [ComfyUI core patch](https://huggingface.co/DmitryDB/MiniMax-H3-DynTime-sQKV) — they do not load in unmodified ComfyUI.*

<details>
<summary><b>FL2VA — Unified Quantization Table</b></summary>

| Pruned | Precision | Method | Size | Download |
| :---: | :---: | :--- | :---: | :--- |
| | ![bf16][badge-bf16] | BF16 | 61.73 GB | [![][gh-Comfy--Org]](https://huggingface.co/Comfy-Org/MiniMax-H3/resolve/main/diffusion_models/minimax_h3_fl2va_bf16.safetensors) |
| | ![bf16][badge-bf16] | Hybrid (fl2va base + ref2va adaln b15-49) | 20.97 GB | [![][gh-smhfacct]](https://huggingface.co/smhfacct/Minimax-H3-fl2va-ref2va-hybrid-models/resolve/main/minimax_h3_hybrid_fl2va_ref2va_b15-49.safetensors) |
| | ![bf16][badge-bf16] | Hybrid (fl2va base + ref2va adaln b20-49) | 20.97 GB | [![][gh-smhfacct]](https://huggingface.co/smhfacct/Minimax-H3-fl2va-ref2va-hybrid-models/resolve/main/minimax_h3_hybrid_fl2va_ref2va_b20-49.safetensors) |
| | ![bf16][badge-bf16] | Hybrid (fl2va base + ref2va adaln b25-49) | 20.97 GB | [![][gh-smhfacct]](https://huggingface.co/smhfacct/Minimax-H3-fl2va-ref2va-hybrid-models/resolve/main/minimax_h3_hybrid_fl2va_ref2va_b25-49.safetensors) |
| | ![bf16][badge-bf16] | Hybrid (fl2va base + ref2va adaln b30-49) | 20.97 GB | [![][gh-smhfacct]](https://huggingface.co/smhfacct/Minimax-H3-fl2va-ref2va-hybrid-models/resolve/main/minimax_h3_hybrid_fl2va_ref2va_b30-49.safetensors) |
| | ![fp8][badge-fp8] | Hybrid (fl2va base + ref2va adaln b15-49) | 19.52 GB | [![][gh-xtanqn]](https://huggingface.co/xtanqn/MiniMax-H3-fl2va-ref2va-b25-49-r1024-r0/resolve/main/minimax_h3_hybrid_fl2va_ref2va_b15-49-fp8_scaled.safetensors) |
| | ![fp8][badge-fp8] | Hybrid (fl2va base + ref2va adaln b20-49) | 19.52 GB | [![][gh-xtanqn]](https://huggingface.co/xtanqn/MiniMax-H3-fl2va-ref2va-b25-49-r1024-r0/resolve/main/minimax_h3_hybrid_fl2va_ref2va_b20-49-fp8_scaled.safetensors) |
| | ![fp8][badge-fp8] | Hybrid (fl2va base + ref2va adaln b25-49) | 19.52 GB | [![][gh-xtanqn]](https://huggingface.co/xtanqn/MiniMax-H3-fl2va-ref2va-b25-49-r1024-r0/resolve/main/minimax_h3_hybrid_fl2va_ref2va_b25-49-fp8_scaled.safetensors) |
| | ![fp8][badge-fp8] | Hybrid (fl2va base + ref2va adaln b30-49) | 19.52 GB | [![][gh-xtanqn]](https://huggingface.co/xtanqn/MiniMax-H3-fl2va-ref2va-b25-49-r1024-r0/resolve/main/minimax_h3_hybrid_fl2va_ref2va_b30-49-fp8_scaled.safetensors) |
| | ![fp8][badge-fp8] | Delta-Fused r1024 (trunk rank-1024 + adaln full from ref2va) | 19.52 GB | [![][gh-xtanqn]](https://huggingface.co/xtanqn/MiniMax-H3-fl2va-ref2va-b25-49-r1024-r0/resolve/main/minimax_h3_delta_fl2va_ref2va_r1024_fp8_scaled.safetensors) |
| | ![fp8][badge-fp8] | Delta-Fused r0 (full-rank ≈ ref2va fp8) | 19.52 GB | [![][gh-xtanqn]](https://huggingface.co/xtanqn/MiniMax-H3-fl2va-ref2va-b25-49-r1024-r0/resolve/main/minimax_h3_delta_fl2va_ref2va_r0_fp8_scaled.safetensors) |
| | ![int8][badge-int8] | ConvRot | 31.70 GB | [![][gh-Comfy--Org]](https://huggingface.co/Comfy-Org/MiniMax-H3/resolve/main/diffusion_models/minimax_h3_fl2va_int8_convrot.safetensors) |
| | ![fp8][badge-fp8] | FP8 E4M3FN | 43.78 GB | [![][gh-rzgar]](https://huggingface.co/rzgar/minimax_h3_fl2va_fp8_e4m3fn/resolve/main/minimax_h3_fl2va_fp8_e4m3fn.safetensors) |
| | ![mxfp8][badge-mxfp8] | MXFP8 | 44.34 GB | [![][gh-rzgar]](https://huggingface.co/rzgar/minimax_h3_fl2va_fp8_e4m3fn/resolve/main/minimax_h3_fl2va_mxfp8.safetensors) |
| | ![fp8][badge-fp8] | FP8 + FP16 attn | 26.70 GB | [![][gh-rzgar]](https://huggingface.co/rzgar/minimax_h3_fl2va_fp8_e4m3fn/resolve/main/minimax_h3_fl2va_fp16attn_fp8.safetensors) |
| | ![int8][badge-int8] | ConvRot Lean | 21.91 GB | [![][gh-DmitryDB]](https://huggingface.co/DmitryDB/MiniMax-H3-ComfyUI-Quants/resolve/main/FL2VA/MiniMax-H3_FL2VA-INT8-ConvRot-HQ.safetensors) |
| | ![int8][badge-int8] | ConvRot | 20.94 GB | [![][gh-DmitryDB]](https://huggingface.co/DmitryDB/MiniMax-H3-ComfyUI-Quants/resolve/main/FL2VA/MiniMax-H3_FL2VA-INT8-ConvRot.safetensors) |
| | ![int8][badge-int8] | ConvRot Lite | 20.33 GB | [![][gh-DmitryDB]](https://huggingface.co/DmitryDB/MiniMax-H3-ComfyUI-Quants/resolve/main/FL2VA/MiniMax-H3_FL2VA-INT8-ConvRot-Lite.safetensors) |
| | ![nvfp4][badge-nvfp4] | NVFP4 | 13.60 GB | [![][gh-DmitryDB]](https://huggingface.co/DmitryDB/MiniMax-H3-ComfyUI-Quants/resolve/main/FL2VA/MiniMax-H3_FL2VA-NVFP4-HQ.safetensors) |
| | ![nvfp4][badge-nvfp4] | NVFP4 | 10.86 GB | [![][gh-DmitryDB]](https://huggingface.co/DmitryDB/MiniMax-H3-ComfyUI-Quants/resolve/main/FL2VA/MiniMax-H3_FL2VA-NVFP4.safetensors) |
| | ![nvfp4][badge-nvfp4] | NVFP4 | 32.05 GB | [![][gh-rockerBOO]](https://huggingface.co/rockerBOO/minimax-h3-nvfp4/resolve/main/minimax_h3_fl2va_nvfp4.safetensors) |
| | ![int4][badge-int4] | NF4 | 15.98 GB | [![][gh-DiffSynth-Studio]](https://huggingface.co/DiffSynth-Studio/MiniMax-H3-NF4/resolve/main/minimax-h3-fl2va-nf4.safetensors) |
| | | OrbitQuant W4A4 | 17.03 GB | [![][gh-WaveCut]](https://huggingface.co/WaveCut/MiniMax-H3-OrbitQuant-W4A4/resolve/main/transformer/diffusion_pytorch_model-00001-of-00005.safetensors) |
| | ![int8][badge-int8] | ⚠️ DT-sQKV ConvRot | 21.00 GB | [![][gh-DmitryDB]](https://huggingface.co/DmitryDB/MiniMax-H3-DynTime-sQKV/resolve/main/FL2VA/MiniMax-H3_FL2VA-DT-sQKV-INT8-ConvRot.safetensors) |
| | ![int8][badge-int8] | ⚠️ DT-sQKV ConvRot Lean | 27.99 GB | [![][gh-DmitryDB]](https://huggingface.co/DmitryDB/MiniMax-H3-DynTime-sQKV/resolve/main/FL2VA/MiniMax-H3_FL2VA-DT-sQKV-INT8-ConvRot-HQ.safetensors) |
| ✓ | ![bf16][badge-bf16] | BF16 | 37.46 GB | [![][gh-Comfy--Org]](https://huggingface.co/Comfy-Org/MiniMax-H3/resolve/main/diffusion_models/minimax_h3_fl2va_pruned_bf16.safetensors) |
| ✓ | ![fp8][badge-fp8] | FP8 scaled | 19.52 GB | [![][gh-Comfy--Org]](https://huggingface.co/Comfy-Org/MiniMax-H3/resolve/main/diffusion_models/minimax_h3_fl2va_pruned_fp8_scaled.safetensors) |
| ✓ | ![int8][badge-int8] | ConvRot | 19.53 GB | [![][gh-Comfy--Org]](https://huggingface.co/Comfy-Org/MiniMax-H3/resolve/main/diffusion_models/minimax_h3_fl2va_pruned_int8_convrot.safetensors) ┊ [![][gh-Abiray]](https://huggingface.co/Abiray/Minimax-H3-nvfp4-INT4-INT8-Convrot/resolve/main/MiniMax_H3_FL2VA_pruned_int8_convrot.safetensors) |
| ✓ | ![int8][badge-int8] | ConvRot · no token_refiner | 18.09 GB | [![][gh-isichan--ai]](https://huggingface.co/isichan-ai/MiniMax-H3-FL2VA-norefiner/resolve/main/minimax_h3_fl2va_norefiner.safetensors) |
| ✓ | ![nvfp4][badge-nvfp4] | NVFP4 | 18.69 GB | [![][gh-rockerBOO]](https://huggingface.co/rockerBOO/minimax-h3-nvfp4/resolve/main/minimax_h3_fl2va_pruned_nvfp4.safetensors) |
| ✓ | ![nvfp4][badge-nvfp4] | NVFP4 + ConvRot INT8 | 18.69 GB | [![][gh-rockerBOO]](https://huggingface.co/rockerBOO/minimax-h3-nvfp4/resolve/main/minimax_h3_fl2va_pruned_nvfp4_convrot_int8.safetensors) |
| ✓ | ![nvfp4][badge-nvfp4] | NVFP4 | 11.67 GB | [![][gh-Abiray]](https://huggingface.co/Abiray/Minimax-H3-nvfp4-INT4-INT8-Convrot/resolve/main/MiniMax_H3_FL2VA_pruned_nvfp4.safetensors) ┊ [![][gh-coolthor]](https://huggingface.co/coolthor/MiniMax-H3-pruned-NVFP4/resolve/main/diffusion_models/minimax_h3_fl2va_pruned_nvfp4.safetensors) |
| ✓ | ![int4][badge-int4] | Mixed INT4/INT8 ConvRot | 14.81 GB | [![][gh-Abiray]](https://huggingface.co/Abiray/Minimax-H3-nvfp4-INT4-INT8-Convrot/resolve/main/MiniMax_H3_FL2VA_pruned_mixed_int4_int8_convrot.safetensors) ┊ [![][gh-tsolful]](https://huggingface.co/tsolful/Minimax_H3_INT4MixedConvRot/resolve/main/minimax_h3_fl2va_pruned_INT4BQ.safetensors) |
| ✓ | ![int4][badge-int4] | Mixed INT4/INT8 ConvRot Lean | 17.27 GB | [![][gh-tsolful]](https://huggingface.co/tsolful/Minimax_H3_INT4MixedConvRot/resolve/main/minimax_h3_fl2va_pruned_INT4Q.safetensors) |
| ✓ | ![int4][badge-int4] | INT4 ConvRot | 15.67 GB | [![][gh-rockerBOO]](https://huggingface.co/rockerBOO/minimax-h3-nvfp4/resolve/main/minimax_h3_fl2va_pruned_int4_convrot_simple.safetensors) |
| ✓ | ![int4][badge-int4] | Mixed INT4/INT8 ConvRot | 18.92 GB | [![][gh-rockerBOO]](https://huggingface.co/rockerBOO/minimax-h3-nvfp4/resolve/main/minimax_h3_fl2va_pruned_mixed_int4_int8_convrot_simple.safetensors) |
| ✓ | ![int4][badge-int4] | W4A8 ConvRot | 11.68 GB | [![][gh-AX1Y2JP]](https://huggingface.co/AX1Y2JP/MiniMax-H3-W4A8-ConvRot/resolve/main/minimax_h3_fl2va_pruned_symw4a8convrot.safetensors) ┊ [![][gh-Kijai]](https://huggingface.co/Kijai/MiniMax-H3-experimental/resolve/main/minimax_h3_fl2va_pruned_w4a8_mixed.safetensors) ┊ [![][gh-Winnougan]](https://huggingface.co/Winnougan/MiniMax-H3-INT4_Convrot_ComfyUI/resolve/main/minimax_h3_fl2va_pruned-w4a8_convrot_pruned.safetensors) |

*GGUF quants — see [GGUF section](#gguf) below.*

*`no token_refiner` is a surgical derivative of Comfy-Org's pruned INT8 ConvRot FL2VA: [isichan-ai](https://huggingface.co/isichan-ai/MiniMax-H3-FL2VA-norefiner) deletes the 16 `token_refiner.blocks.*` tensors (1.44 GiB) and keeps `final_norm`, so ComfyUI counts a 0-layer refiner and needs no code change — the file simply loads in `UNETLoader` where the original went. The refiner only runs once at the start of generation but its weights otherwise sit in VRAM until the end, so dropping them raises the author's resolution ceiling from 1.2 MP to 1.4 MP on a 32 GB RTX 5090 (1.5 MP still OOMs); same seed and prompt showed no visible quality change, though outputs are not bit-identical. Everything else is byte-identical to the Comfy-Org file.*

</details>

<details>
<summary><b>Ref2VA — Unified Quantization Table</b></summary>

| Pruned | Precision | Method | Size | Download |
| :---: | :---: | :--- | :---: | :--- |
| | ![bf16][badge-bf16] | BF16 | 61.73 GB | [![][gh-Comfy--Org]](https://huggingface.co/Comfy-Org/MiniMax-H3/resolve/main/diffusion_models/minimax_h3_ref2va_bf16.safetensors) |
| | ![int8][badge-int8] | ConvRot | 31.70 GB | [![][gh-Comfy--Org]](https://huggingface.co/Comfy-Org/MiniMax-H3/resolve/main/diffusion_models/minimax_h3_ref2va_int8_convrot.safetensors) ┊ [![][gh-t8star]](https://huggingface.co/t8star/minimax_h3_ref2va_patchin_hf102/resolve/main/minimax_h3_ref2va_patchin_hf102_T8.safetensors) |
| | ![int8][badge-int8] | ConvRot Lean | 21.91 GB | [![][gh-DmitryDB]](https://huggingface.co/DmitryDB/MiniMax-H3-ComfyUI-Quants/resolve/main/Ref2VA/MiniMax-H3_Ref2VA-INT8-ConvRot-HQ.safetensors) |
| | ![int8][badge-int8] | ConvRot | 20.94 GB | [![][gh-DmitryDB]](https://huggingface.co/DmitryDB/MiniMax-H3-ComfyUI-Quants/resolve/main/Ref2VA/MiniMax-H3_Ref2VA-INT8-ConvRot.safetensors) |
| | ![int8][badge-int8] | ConvRot Lite | 20.33 GB | [![][gh-DmitryDB]](https://huggingface.co/DmitryDB/MiniMax-H3-ComfyUI-Quants/resolve/main/Ref2VA/MiniMax-H3_Ref2VA-INT8-ConvRot-Lite.safetensors) |
| | ![nvfp4][badge-nvfp4] | NVFP4 | 13.60 GB | [![][gh-DmitryDB]](https://huggingface.co/DmitryDB/MiniMax-H3-ComfyUI-Quants/resolve/main/Ref2VA/MiniMax-H3_Ref2VA-NVFP4-HQ.safetensors) |
| | ![nvfp4][badge-nvfp4] | NVFP4 | 10.86 GB | [![][gh-DmitryDB]](https://huggingface.co/DmitryDB/MiniMax-H3-ComfyUI-Quants/resolve/main/Ref2VA/MiniMax-H3_Ref2VA-NVFP4.safetensors) |
| | ![nvfp4][badge-nvfp4] | NVFP4 | 32.05 GB | [![][gh-rockerBOO]](https://huggingface.co/rockerBOO/minimax-h3-nvfp4/resolve/main/minimax_h3_ref2va_nvfp4.safetensors) |
| | ![nvfp4][badge-nvfp4] | NVFP4 | 22.76 GB | [![][gh-Abiray]](https://huggingface.co/Abiray/Minimax-H3-nvfp4-INT4-INT8-Convrot/resolve/main/MiniMax_H3_Ref2VA_nvfp4_mixed.safetensors) |
| | ![int4][badge-int4] | NF4 | 15.98 GB | [![][gh-DiffSynth-Studio]](https://huggingface.co/DiffSynth-Studio/MiniMax-H3-NF4/resolve/main/minimax-h3-ref2va-nf4.safetensors) |
| | | OrbitQuant W4A4 | 17.03 GB | [![][gh-WaveCut]](https://huggingface.co/WaveCut/MiniMax-H3-OrbitQuant-W4A4/resolve/main/transformer_ref/diffusion_pytorch_model-00001-of-00005.safetensors) |
| | ![nvfp4][badge-nvfp4] | Hybrid NVFP4 (FFN-only) | 16.38 GB | [![][gh-abakanai]](https://huggingface.co/abakanai/Minimax_h3_hybrid/resolve/main/minimax_h3_ref2va_pruned_hybrid_ffn_nvfp4_blackwell.safetensors) |
| | ![nvfp4][badge-nvfp4] | Hybrid NVFP4 (QKV+FFN) | 14.03 GB | [![][gh-abakanai]](https://huggingface.co/abakanai/Minimax_h3_hybrid/resolve/main/minimax_h3_ref2va_pruned_hybrid_nvfp4_blackwell.safetensors) |
| | ![int8][badge-int8] | ⚠️ DT-sQKV ConvRot | 21.00 GB | [![][gh-DmitryDB]](https://huggingface.co/DmitryDB/MiniMax-H3-DynTime-sQKV/resolve/main/Ref2VA/MiniMax-H3_Ref2VA-DT-sQKV-INT8-ConvRot.safetensors) |
| | ![int8][badge-int8] | ⚠️ DT-sQKV ConvRot Lean | 27.99 GB | [![][gh-DmitryDB]](https://huggingface.co/DmitryDB/MiniMax-H3-DynTime-sQKV/resolve/main/Ref2VA/MiniMax-H3_Ref2VA-DT-sQKV-INT8-ConvRot-HQ.safetensors) |
| ✓ | ![bf16][badge-bf16] | BF16 | 37.46 GB | [![][gh-Comfy--Org]](https://huggingface.co/Comfy-Org/MiniMax-H3/resolve/main/diffusion_models/minimax_h3_ref2va_pruned_bf16.safetensors) |
| ✓ | ![fp8][badge-fp8] | FP8 scaled | 19.52 GB | [![][gh-Comfy--Org]](https://huggingface.co/Comfy-Org/MiniMax-H3/resolve/main/diffusion_models/minimax_h3_ref2va_pruned_fp8_scaled.safetensors) |
| ✓ | ![int8][badge-int8] | ConvRot | 19.53 GB | [![][gh-Comfy--Org]](https://huggingface.co/Comfy-Org/MiniMax-H3/resolve/main/diffusion_models/minimax_h3_ref2va_pruned_int8_convrot.safetensors) ┊ [![][gh-Abiray]](https://huggingface.co/Abiray/Minimax-H3-nvfp4-INT4-INT8-Convrot/resolve/main/MiniMax_H3_Ref2VA_pruned_int8_convrot.safetensors) |
| ✓ | ![int8][badge-int8] | ConvRot · ⚠️ PDD 8-step Acc LoRA baked in | 19.5 GB · 19.6 GB | [![][gh-Asirus]](https://huggingface.co/Asirus/minimax_h3_ref2va_pdd_baked_int8_convrot/resolve/main/minimax_h3_ref2va_pdd_baked_int8_convrot.safetensors) ┊ [![][gh-Asirus]](https://huggingface.co/Asirus/minimax_h3_ref2va_pdd_baked_int8_convrot/resolve/main/minimax_h3_ref2va_pdd_baked_int8_convrot_embedded_heads.safetensors) |
| ✓ | ![nvfp4][badge-nvfp4] | NVFP4 | 18.69 GB | [![][gh-rockerBOO]](https://huggingface.co/rockerBOO/minimax-h3-nvfp4/resolve/main/minimax_h3_ref2va_pruned_nvfp4.safetensors) |
| ✓ | ![nvfp4][badge-nvfp4] | NVFP4 + ConvRot INT8 | 18.69 GB | [![][gh-rockerBOO]](https://huggingface.co/rockerBOO/minimax-h3-nvfp4/resolve/main/minimax_h3_ref2va_pruned_nvfp4_convrot_int8.safetensors) |
| ✓ | ![nvfp4][badge-nvfp4] | NVFP4 | 11.67 GB | [![][gh-Abiray]](https://huggingface.co/Abiray/Minimax-H3-nvfp4-INT4-INT8-Convrot/resolve/main/MiniMax_H3_Ref2VA_pruned_nvfp4.safetensors) ┊ [![][gh-coolthor]](https://huggingface.co/coolthor/MiniMax-H3-pruned-NVFP4/resolve/main/diffusion_models/minimax_h3_ref2va_pruned_nvfp4.safetensors) |
| ✓ | ![int4][badge-int4] | Mixed INT4/INT8 ConvRot | 14.06 GB | [![][gh-Abiray]](https://huggingface.co/Abiray/Minimax-H3-nvfp4-INT4-INT8-Convrot/resolve/main/MiniMax_H3_Ref2VA_pruned_mixed_int4_int8_convrot.safetensors) ┊ [![][gh-tsolful]](https://huggingface.co/tsolful/Minimax_H3_INT4MixedConvRot/resolve/main/minimax_h3_ref2va_pruned_INT4BQ.safetensors) |
| ✓ | ![int4][badge-int4] | Mixed INT4/INT8 ConvRot Lean | 17.18 GB | [![][gh-tsolful]](https://huggingface.co/tsolful/Minimax_H3_INT4MixedConvRot/resolve/main/minimax_h3_ref2va_pruned_INT4Q.safetensors) |
| ✓ | ![int4][badge-int4] | INT4 ConvRot | 15.67 GB | [![][gh-rockerBOO]](https://huggingface.co/rockerBOO/minimax-h3-nvfp4/resolve/main/minimax_h3_ref2va_pruned_int4_convrot_simple.safetensors) |
| ✓ | ![int4][badge-int4] | W4A8 ConvRot | 11.68 GB | [![][gh-AX1Y2JP]](https://huggingface.co/AX1Y2JP/MiniMax-H3-W4A8-ConvRot/resolve/main/minimax_h3_ref2va_pruned_symw4a8convrot.safetensors) ┊ [![][gh-Kijai]](https://huggingface.co/Kijai/MiniMax-H3-experimental/resolve/main/minimax_h3_ref2va_pruned_w4a8_mixed.safetensors) ┊ [![][gh-Winnougan]](https://huggingface.co/Winnougan/MiniMax-H3-INT4_Convrot_ComfyUI/resolve/main/minimax_h3_ref2va_pruned-w4a8_convrot_pruned.safetensors) |

*GGUF quants — see [GGUF section](#gguf) below.*

</details>

<p id="gguf" align="center">· · · · · · · · · · · · · ·</p>

#### GGUF Quantized Models

GGUF quants for use with stable-diffusion.cpp, ComfyUI, and Unsloth. Non-pruned sources: [Abiray/MiniMax-H3-GGUF](https://huggingface.co/Abiray/MiniMax-H3-GGUF), [vantagewithai/MiniMax-H3-comfyUI-GGUF](https://huggingface.co/vantagewithai/MiniMax-H3-comfyUI-GGUF), [realrebelai/MiniMax-H3_GGUFs](https://huggingface.co/realrebelai/MiniMax-H3_GGUFs). Pruned sources: [unsloth/MiniMax-H3-GGUF](https://huggingface.co/unsloth/MiniMax-H3-GGUF), [MarxistLeninist/MiniMax-H3-FL2VA-Pruned-IQ1-GGUF](https://huggingface.co/MarxistLeninist/MiniMax-H3-FL2VA-Pruned-IQ1-GGUF).

<details>
<summary><b>FL2VA GGUF</b></summary>

| Pruned | Quant | Size | Download |
| :---: | :---: | :---: | :--- |
| | ![Q2_K][badge-Q2_K] | 17.42 GB | [![][gh-realrebelai]](https://huggingface.co/realrebelai/MiniMax-H3_GGUFs/resolve/main/MiniMax-H3-FL2VA-Q2_K-(Mixed_Precision).gguf) |
| | ![Q3_K_M][badge-Q3_K_M] | 14.50 GB | [![][gh-Abiray]](https://huggingface.co/Abiray/MiniMax-H3-GGUF/resolve/main/unet/MiniMax-H3-FL2VA-Q3_K_M.gguf) ┊ [![][gh-realrebelai]](https://huggingface.co/realrebelai/MiniMax-H3_GGUFs/resolve/main/MiniMax-H3-FL2VA-Q3_K_M.gguf) ┊ [![][gh-vantagewithai]](https://huggingface.co/vantagewithai/MiniMax-H3-comfyUI-GGUF/resolve/main/fl2va/minimax_h3_fl2va-Q3_K_M.gguf) |
| |![Q3_K_S][badge-Q3_K_S] | 14.50 GB | [![][gh-Abiray]](https://huggingface.co/Abiray/MiniMax-H3-GGUF/resolve/main/unet/MiniMax-H3-FL2VA-Q3_K_S.gguf) |
| | ![Q4_0][badge-Q4_0] | 17.36 GB | [![][gh-Abiray]](https://huggingface.co/Abiray/MiniMax-H3-GGUF/resolve/main/unet/MiniMax-H3-FL2VA-Q4_0.gguf) ┊ [![][gh-vantagewithai]](https://huggingface.co/vantagewithai/MiniMax-H3-comfyUI-GGUF/resolve/main/fl2va/minimax_h3_fl2va-Q4_0.gguf) |
| | ![Q4_1][badge-Q4_1] | 20.41 GB | [![][gh-vantagewithai]](https://huggingface.co/vantagewithai/MiniMax-H3-comfyUI-GGUF/resolve/main/fl2va/minimax_h3_fl2va-Q4_1.gguf) |
| | ![Q4_K_M][badge-Q4_K_M] | 18.50 GB | [![][gh-Abiray]](https://huggingface.co/Abiray/MiniMax-H3-GGUF/resolve/main/unet/MiniMax-H3-FL2VA-Q4_K_M.gguf) ┊ [![][gh-realrebelai]](https://huggingface.co/realrebelai/MiniMax-H3_GGUFs/resolve/main/MiniMax-H3-FL2VA-Q4_K_M.gguf) ┊ [![][gh-vantagewithai]](https://huggingface.co/vantagewithai/MiniMax-H3-comfyUI-GGUF/resolve/main/fl2va/minimax_h3_fl2va-Q4_K_M.gguf) |
| | ![Q4_K_S][badge-Q4_K_S] | 18.49 GB | [![][gh-Abiray]](https://huggingface.co/Abiray/MiniMax-H3-GGUF/resolve/main/unet/MiniMax-H3-FL2VA-Q4_K_S.gguf) ┊ [![][gh-vantagewithai]](https://huggingface.co/vantagewithai/MiniMax-H3-comfyUI-GGUF/resolve/main/fl2va/minimax_h3_fl2va-Q4_K_S.gguf) |
| | ![Q5_0][badge-Q5_0] | 21.21 GB | [![][gh-Abiray]](https://huggingface.co/Abiray/MiniMax-H3-GGUF/resolve/main/unet/MiniMax-H3-FL2VA-Q5_0.gguf) ┊ [![][gh-vantagewithai]](https://huggingface.co/vantagewithai/MiniMax-H3-comfyUI-GGUF/resolve/main/fl2va/minimax_h3_fl2va-Q5_0.gguf) |
| | ![Q5_1][badge-Q5_1] | 24.17 GB | [![][gh-vantagewithai]](https://huggingface.co/vantagewithai/MiniMax-H3-comfyUI-GGUF/resolve/main/fl2va/minimax_h3_fl2va-Q5_1.gguf) |
| | ![Q5_K_M][badge-Q5_K_M] | 22.25 GB | [![][gh-Abiray]](https://huggingface.co/Abiray/MiniMax-H3-GGUF/resolve/main/unet/MiniMax-H3-FL2VA-Q5_K_M.gguf) ┊ [![][gh-vantagewithai]](https://huggingface.co/vantagewithai/MiniMax-H3-comfyUI-GGUF/resolve/main/fl2va/minimax_h3_fl2va-Q5_K_M.gguf) |
| | ![Q5_K_S][badge-Q5_K_S] | 22.25 GB | [![][gh-Abiray]](https://huggingface.co/Abiray/MiniMax-H3-GGUF/resolve/main/unet/MiniMax-H3-FL2VA-Q5_K_S.gguf) ┊ [![][gh-vantagewithai]](https://huggingface.co/vantagewithai/MiniMax-H3-comfyUI-GGUF/resolve/main/fl2va/minimax_h3_fl2va-Q5_K_S.gguf) |
| | ![Q6_K][badge-Q6_K] | 26.28 GB | [![][gh-Abiray]](https://huggingface.co/Abiray/MiniMax-H3-GGUF/resolve/main/unet/MiniMax-H3-FL2VA-Q6_K.gguf) ┊ [![][gh-vantagewithai]](https://huggingface.co/vantagewithai/MiniMax-H3-comfyUI-GGUF/resolve/main/fl2va/minimax_h3_fl2va-Q6_K.gguf) |
| | ![Q8_0][badge-Q8_0] | 33.56 GB | [![][gh-Abiray]](https://huggingface.co/Abiray/MiniMax-H3-GGUF/resolve/main/unet/MiniMax-H3-FL2VA-Q8_0.gguf) ┊ [![][gh-vantagewithai]](https://huggingface.co/vantagewithai/MiniMax-H3-comfyUI-GGUF/resolve/main/fl2va/minimax_h3_fl2va-Q8_0.gguf) |
| ✓ | ![Q2_K][badge-Q2_K] | 6.26 GB | [![][gh-unsloth]](https://huggingface.co/unsloth/MiniMax-H3-GGUF/resolve/main/minimax_h3_fl2va_pruned-Q2_K.gguf) |
| ✓ | ![Q3_K_M][badge-Q3_K_M] | 8.16 GB | [![][gh-unsloth]](https://huggingface.co/unsloth/MiniMax-H3-GGUF/resolve/main/minimax_h3_fl2va_pruned-Q3_K.gguf) |
| ✓ | ![Q4_K_M][badge-Q4_K_M] | 10.64 GB | [![][gh-unsloth]](https://huggingface.co/unsloth/MiniMax-H3-GGUF/resolve/main/minimax_h3_fl2va_pruned-Q4_K.gguf) |
| ✓ | ![Q5_0][badge-Q5_0] | 12.97 GB | [![][gh-unsloth]](https://huggingface.co/unsloth/MiniMax-H3-GGUF/resolve/main/minimax_h3_fl2va_pruned-Q5_0.gguf) |
| ✓ | ![Q6_K][badge-Q6_K] | 15.45 GB | [![][gh-unsloth]](https://huggingface.co/unsloth/MiniMax-H3-GGUF/resolve/main/minimax_h3_fl2va_pruned-Q6_K.gguf) |
| ✓ | ![Q8_0][badge-Q8_0] | 19.97 GB | [![][gh-unsloth]](https://huggingface.co/unsloth/MiniMax-H3-GGUF/resolve/main/minimax_h3_fl2va_pruned-Q8_0.gguf) |
| ✓ | ![UD-Q2_K_XL][badge-UD-Q2_K_XL] | 7.51 GB | [![][gh-unsloth]](https://huggingface.co/unsloth/MiniMax-H3-GGUF/resolve/main/minimax_h3_fl2va_pruned-UD-Q2_K_XL.gguf) |
| ✓ | ![UD-Q3_K_XL][badge-UD-Q3_K_XL] | 8.90 GB | [![][gh-unsloth]](https://huggingface.co/unsloth/MiniMax-H3-GGUF/resolve/main/minimax_h3_fl2va_pruned-UD-Q3_K_XL.gguf) |
| ✓ | ![IQ1_S][badge-IQ1_S] | 3.78 GB | [![][gh-MarxistLeninist]](https://huggingface.co/MarxistLeninist/MiniMax-H3-FL2VA-Pruned-IQ1-GGUF/resolve/main/minimax_h3_fl2va_pruned-IQ1_S.gguf) |
| ✓ | ![IQ1_M][badge-IQ1_M] | 4.22 GB | [![][gh-MarxistLeninist]](https://huggingface.co/MarxistLeninist/MiniMax-H3-FL2VA-Pruned-IQ1-GGUF/resolve/main/minimax_h3_fl2va_pruned-IQ1_M.gguf) |

</details>

<details>
<summary><b>Ref2VA GGUF</b></summary>

| Pruned | Quant | Size | Download |
| :---: | :---: | :---: | :--- |
| | ![Q3_K_M][badge-Q3_K_M] | 14.50 GB | [![][gh-Abiray]](https://huggingface.co/Abiray/MiniMax-H3-GGUF/resolve/main/unet/MiniMax-H3-Ref2VA-Q3_K_M.gguf) ┊ [![][gh-realrebelai]](https://huggingface.co/realrebelai/MiniMax-H3_GGUFs/resolve/main/MiniMax-H3-REF2VA-Q3_K_M.gguf) ┊ [![][gh-vantagewithai]](https://huggingface.co/vantagewithai/MiniMax-H3-comfyUI-GGUF/resolve/main/ref2va/minimax_h3_ref2va-Q3_K_M.gguf) |
| | ![Q3_K_S][badge-Q3_K_S] | 14.50 GB | [![][gh-Abiray]](https://huggingface.co/Abiray/MiniMax-H3-GGUF/resolve/main/unet/MiniMax-H3-Ref2VA-Q3_K_S.gguf) |
| | ![Q4_0][badge-Q4_0] | 17.36 GB | [![][gh-Abiray]](https://huggingface.co/Abiray/MiniMax-H3-GGUF/resolve/main/unet/MiniMax-H3-Ref2VA-Q4_0.gguf) ┊ [![][gh-vantagewithai]](https://huggingface.co/vantagewithai/MiniMax-H3-comfyUI-GGUF/resolve/main/ref2va/minimax_h3_ref2va-Q4_0.gguf) |
| | ![Q4_1][badge-Q4_1] | 20.41 GB | [![][gh-vantagewithai]](https://huggingface.co/vantagewithai/MiniMax-H3-comfyUI-GGUF/resolve/main/ref2va/minimax_h3_ref2va-Q4_1.gguf) |
| | ![Q4_K_M][badge-Q4_K_M] | 18.49 GB | [![][gh-Abiray]](https://huggingface.co/Abiray/MiniMax-H3-GGUF/resolve/main/unet/MiniMax-H3-Ref2VA-Q4_K_M.gguf) ┊ [![][gh-realrebelai]](https://huggingface.co/realrebelai/MiniMax-H3_GGUFs/resolve/main/MiniMax-H3-REF2VA-Q4_K_M.gguf) ┊ [![][gh-vantagewithai]](https://huggingface.co/vantagewithai/MiniMax-H3-comfyUI-GGUF/resolve/main/ref2va/minimax_h3_ref2va-Q4_K_M.gguf) |
| | ![Q4_K_S][badge-Q4_K_S] | 18.49 GB | [![][gh-Abiray]](https://huggingface.co/Abiray/MiniMax-H3-GGUF/resolve/main/unet/MiniMax-H3-Ref2VA-Q4_K_S.gguf) ┊ [![][gh-vantagewithai]](https://huggingface.co/vantagewithai/MiniMax-H3-comfyUI-GGUF/resolve/main/ref2va/minimax_h3_ref2va-Q4_K_S.gguf) |
| | ![Q5_0][badge-Q5_0] | 21.21 GB | [![][gh-Abiray]](https://huggingface.co/Abiray/MiniMax-H3-GGUF/resolve/main/unet/MiniMax-H3-Ref2VA-Q5_0.gguf) ┊ [![][gh-vantagewithai]](https://huggingface.co/vantagewithai/MiniMax-H3-comfyUI-GGUF/resolve/main/ref2va/minimax_h3_ref2va-Q5_0.gguf) |
| | ![Q5_1][badge-Q5_1] | 24.17 GB | [![][gh-vantagewithai]](https://huggingface.co/vantagewithai/MiniMax-H3-comfyUI-GGUF/resolve/main/ref2va/minimax_h3_ref2va-Q5_1.gguf) |
| | ![Q5_K_M][badge-Q5_K_M] | 22.25 GB | [![][gh-Abiray]](https://huggingface.co/Abiray/MiniMax-H3-GGUF/resolve/main/unet/MiniMax-H3-Ref2VA-Q5_K_M.gguf) ┊ [![][gh-vantagewithai]](https://huggingface.co/vantagewithai/MiniMax-H3-comfyUI-GGUF/resolve/main/ref2va/minimax_h3_ref2va-Q5_K_M.gguf) |
| | ![Q5_K_S][badge-Q5_K_S] | 22.25 GB | [![][gh-Abiray]](https://huggingface.co/Abiray/MiniMax-H3-GGUF/resolve/main/unet/MiniMax-H3-Ref2VA-Q5_K_S.gguf) ┊ [![][gh-vantagewithai]](https://huggingface.co/vantagewithai/MiniMax-H3-comfyUI-GGUF/resolve/main/ref2va/minimax_h3_ref2va-Q5_K_S.gguf) |
| | ![Q6_K][badge-Q6_K] | 26.28 GB | [![][gh-Abiray]](https://huggingface.co/Abiray/MiniMax-H3-GGUF/resolve/main/unet/MiniMax-H3-Ref2VA-Q6_K.gguf) ┊ [![][gh-vantagewithai]](https://huggingface.co/vantagewithai/MiniMax-H3-comfyUI-GGUF/resolve/main/ref2va/minimax_h3_ref2va-Q6_K.gguf) |
| | ![Q8_0][badge-Q8_0] | 33.56 GB | [![][gh-Abiray]](https://huggingface.co/Abiray/MiniMax-H3-GGUF/resolve/main/unet/MiniMax-H3-Ref2VA-Q8_0.gguf) ┊ [![][gh-vantagewithai]](https://huggingface.co/vantagewithai/MiniMax-H3-comfyUI-GGUF/resolve/main/ref2va/minimax_h3_ref2va-Q8_0.gguf) |
| ✓ | ![Q2_K][badge-Q2_K] | 6.22 GB | [![][gh-unsloth]](https://huggingface.co/unsloth/MiniMax-H3-GGUF/resolve/main/minimax_h3_ref2va_pruned-Q2_K.gguf) |
| ✓ | ![Q3_K_M][badge-Q3_K_M] | 8.12 GB | [![][gh-unsloth]](https://huggingface.co/unsloth/MiniMax-H3-GGUF/resolve/main/minimax_h3_ref2va_pruned-Q3_K.gguf) |
| ✓ | ![Q4_K_M][badge-Q4_K_M] | 10.60 GB | [![][gh-unsloth]](https://huggingface.co/unsloth/MiniMax-H3-GGUF/resolve/main/minimax_h3_ref2va_pruned-Q4_K.gguf) |
| ✓ | ![Q5_0][badge-Q5_0] | 12.94 GB | [![][gh-unsloth]](https://huggingface.co/unsloth/MiniMax-H3-GGUF/resolve/main/minimax_h3_ref2va_pruned-Q5_0.gguf) |
| ✓ | ![Q6_K][badge-Q6_K] | 15.42 GB | [![][gh-unsloth]](https://huggingface.co/unsloth/MiniMax-H3-GGUF/resolve/main/minimax_h3_ref2va_pruned-Q6_K.gguf) |
| ✓ | ![Q8_0][badge-Q8_0] | 19.94 GB | [![][gh-unsloth]](https://huggingface.co/unsloth/MiniMax-H3-GGUF/resolve/main/minimax_h3_ref2va_pruned-Q8_0.gguf) |

</details>

<p id="finetunes" align="center">· · · · · · · · · · · · · ·</p>

#### Fine-tuned Checkpoints

Stock-compatible quants for the **10Eros_Max** fine-tune of MiniMax-H3. Fine-tuned QKV weights in blocks 0–31 preserved alongside tested quantization layouts. No custom node or ComfyUI core patch required. ([DmitryDB/MiniMax-H3-10Eros-Max-Quants](https://huggingface.co/DmitryDB/MiniMax-H3-10Eros-Max-Quants))

| Variant | Precision | Method | Size | Download |
| :--- | :---: | :--- | :---: | :--- |
| FL2VA 10Eros | ![int8][badge-int8] | ConvRot Lean | 21.91 GB | [![][gh-DmitryDB]](https://huggingface.co/DmitryDB/MiniMax-H3-10Eros-Max-Quants/resolve/main/FL2VA/10Eros_Max_H3_FL2VA-INT8-ConvRot-HQ.safetensors) |
| FL2VA 10Eros | ![int8][badge-int8] | ConvRot | 20.94 GB | [![][gh-DmitryDB]](https://huggingface.co/DmitryDB/MiniMax-H3-10Eros-Max-Quants/resolve/main/FL2VA/10Eros_Max_H3_FL2VA-INT8-ConvRot.safetensors) |
| FL2VA 10Eros | ![nvfp4][badge-nvfp4] | NVFP4 | 13.60 GB | [![][gh-DmitryDB]](https://huggingface.co/DmitryDB/MiniMax-H3-10Eros-Max-Quants/resolve/main/FL2VA/10Eros_Max_H3_FL2VA-NVFP4-HQ.safetensors) |
| FL2VA 10Eros | ![nvfp4][badge-nvfp4] | NVFP4 | 10.86 GB | [![][gh-DmitryDB]](https://huggingface.co/DmitryDB/MiniMax-H3-10Eros-Max-Quants/resolve/main/FL2VA/10Eros_Max_H3_FL2VA-NVFP4.safetensors) |

Patch-required FL2VA for the **10Eros_Max** fine-tune. DT-sQKV edition ([DmitryDB/MiniMax-H3-10Eros-Max-DT-sQKV](https://huggingface.co/DmitryDB/MiniMax-H3-10Eros-Max-DT-sQKV)):

| Variant | Precision | Method | Size | Download |
| :--- | :---: | :--- | :---: | :--- |
| FL2VA 10Eros | ![int8][badge-int8] | ⚠️ DT-sQKV ConvRot | 21.00 GB | [![][gh-DmitryDB]](https://huggingface.co/DmitryDB/MiniMax-H3-10Eros-Max-DT-sQKV/resolve/main/FL2VA/10Eros_Max_H3_FL2VA-DT-sQKV-INT8-ConvRot.safetensors) |

#### H3 × Z-Image Graft (joeygambino)

Z-Image's spatial-attention profile grafted onto H3's engine (`zs05` = late-block gains, dose 0.5) — richer sets and textures, same identity, no per-shot sharpening creep. Native ComfyUI cuts load with the plain **Load Diffusion Model** node (ComfyUI 0.32+); GGUF quants for the [GGUF repo](https://huggingface.co/joeygambino/MiniMax-H3-x-Z-Image-GGUF) (fl2va/ref2va × curve/standard, Q4_0–Q8_0 + Q3mix, 10.7–24.1 GB). RTX 30/40: the GGUF repo is 4–8× faster than any 4-bit comfy-native arm on Ampere.

| Variant | Precision | Size | Download |
| :--- | :---: | :---: | :--- |
| fl2va pruned zs05 | ![bf16][badge-bf16] | — | see [repo](https://huggingface.co/joeygambino/MiniMax-H3-x-Z-Image-native) |
| ref2va pruned zs05 (master) | ![bf16][badge-bf16] | 37.46 GB | [![][gh-joeygambino]](https://huggingface.co/joeygambino/MiniMax-H3-x-Z-Image-native/resolve/main/minimax_h3_ref2va_pruned_zs05_bf16.safetensors) |
| fl2va pruned zs05 · int8_convrot | ![int8][badge-int8] | 31.69 GB | [![][gh-joeygambino]](https://huggingface.co/joeygambino/MiniMax-H3-x-Z-Image-native/resolve/main/minimax_h3_fl2va_zs05_int8_convrot.safetensors) |
| ref2va pruned zs05 · int8_convrot | ![int8][badge-int8] | 19.53 GB | [![][gh-joeygambino]](https://huggingface.co/joeygambino/MiniMax-H3-x-Z-Image-native/resolve/main/minimax_h3_ref2va_pruned_zs05_int8_convrot.safetensors) |
| fl2va pruned zs05 | ![fp8][badge-fp8] | 19.52 GB | [![][gh-joeygambino]](https://huggingface.co/joeygambino/MiniMax-H3-x-Z-Image-native/resolve/main/MiniMax-H3-fl2va-pruned-zs05-comfy-fp8.safetensors) |
| ref2va pruned zs05 | ![fp8][badge-fp8] | 19.52 GB | [![][gh-joeygambino]](https://huggingface.co/joeygambino/MiniMax-H3-x-Z-Image-native/resolve/main/MiniMax-H3-ref2va-pruned-zs05-comfy-fp8.safetensors) |
| ref2va pruned zs05 | ![fp8][badge-fp8] e5m2 | 19.52 GB | [![][gh-joeygambino]](https://huggingface.co/joeygambino/MiniMax-H3-x-Z-Image-native/resolve/main/MiniMax-H3-ref2va-pruned-zs05-comfy-fp8e5m2.safetensors) |
| fl2va / ref2va pruned zs05 | ![int8][badge-int8] comfy | 19.53 GB | [![][gh-joeygambino]](https://huggingface.co/joeygambino/MiniMax-H3-x-Z-Image-native/resolve/main/MiniMax-H3-fl2va-pruned-zs05-comfy-int8.safetensors) ┊ [![][gh-joeygambino]](https://huggingface.co/joeygambino/MiniMax-H3-x-Z-Image-native/resolve/main/MiniMax-H3-ref2va-pruned-zs05-comfy-int8.safetensors) |
| fl2va / ref2va pruned zs05 | ![mxfp8][badge-mxfp8] | 20.08 GB | [![][gh-joeygambino]](https://huggingface.co/joeygambino/MiniMax-H3-x-Z-Image-native/resolve/main/MiniMax-H3-fl2va-pruned-zs05-comfy-mxfp8.safetensors) ┊ [![][gh-joeygambino]](https://huggingface.co/joeygambino/MiniMax-H3-x-Z-Image-native/resolve/main/MiniMax-H3-ref2va-pruned-zs05-comfy-mxfp8.safetensors) |
| fl2va / ref2va pruned zs05 | ![nvfp4][badge-nvfp4] | 11.67 GB | [![][gh-joeygambino]](https://huggingface.co/joeygambino/MiniMax-H3-x-Z-Image-native/resolve/main/MiniMax-H3-fl2va-pruned-zs05-comfy-nvfp4.safetensors) ┊ [![][gh-joeygambino]](https://huggingface.co/joeygambino/MiniMax-H3-x-Z-Image-native/resolve/main/MiniMax-H3-ref2va-pruned-zs05-comfy-nvfp4.safetensors) |
| fl2va / ref2va pruned zs05 | w4a8 | 11.68 GB | [![][gh-joeygambino]](https://huggingface.co/joeygambino/MiniMax-H3-x-Z-Image-native/resolve/main/MiniMax-H3-fl2va-pruned-zs05-comfy-w4a8.safetensors) ┊ [![][gh-joeygambino]](https://huggingface.co/joeygambino/MiniMax-H3-x-Z-Image-native/resolve/main/MiniMax-H3-ref2va-pruned-zs05-comfy-w4a8.safetensors) |
| ref2va pruned zs05 | w4a4 | 10.56 GB | [![][gh-joeygambino]](https://huggingface.co/joeygambino/MiniMax-H3-x-Z-Image-native/resolve/main/MiniMax-H3-ref2va-pruned-zs05-comfy-w4a4.safetensors) |

#### H3 × Z-Image FL2VA+Ref2VA Hybrid (hoidhxd)

Community hybrid of joeygambino's ZS05 INT8 checkpoints: **FL2VA base with REF2VA `adaln_proj` blocks 25–49** (b25-49 strategy; final layer stays FL2VA). Raw-tensor splice — no dequant/requant. Research/experimental; not claimed better than either source. Load as a diffusion model. ([repo](https://huggingface.co/hoidhxd/MiniMax-H3-x-Z-Image-hybrid))

| Variant | Precision | Size | Download |
| :--- | :---: | :---: | :--- |
| Hybrid b25-49 zs05 | ![int8][badge-int8] | 19.53 GiB | [![][gh-hoidhxd]](https://huggingface.co/hoidhxd/MiniMax-H3-x-Z-Image-hybrid/resolve/main/minimax_h3_hybrid_fl2va_ref2va_zs05_b25-49_int8.safetensors) |

#### Pruned Ref-Delta Fused r1024 (xmarre)

Native ComfyUI single-file conversion of [`diffusers-modular/MiniMax-H3-Pruned-Ref-Delta-Fused-r1024`](https://huggingface.co/diffusers-modular/MiniMax-H3-Pruned-Ref-Delta-Fused-r1024) — a fused checkpoint carrying the Ref2VA delta LoRA at rank 1024 on the pruned base (see also ethanfel's unfused delta adapters in [LoRA → All LoRAs](#lora)). Diffusion transformer only; use stock H3 TE + VAEs. INT8 variants keep all 50 MLP `fc2` layers BF16 to avoid fused-swiglu INT8 OOM; validated end-to-end in ComfyUI (Continuum/Spectrum/refine). MiniMax H3 Community License.

| Variant | Precision | Size | Download |
| :--- | :---: | :---: | :--- |
| BF16 native conversion | ![bf16][badge-bf16] | 37.47 GiB | [![][gh-xmarre]](https://huggingface.co/xmarre/MiniMax-H3-Pruned-Ref-Delta-Fused-r1024-ComfyUI/resolve/main/MiniMax-H3-Pruned-Ref-Delta-Fused-r1024-comfy.safetensors) |
| INT8 tensorwise · fc2 bf16 | ![int8][badge-int8] | 23.12 GiB | [![][gh-xmarre]](https://huggingface.co/xmarre/MiniMax-H3-Pruned-Ref-Delta-Fused-r1024-ComfyUI/resolve/main/MiniMax-H3-Pruned-Ref-Delta-Fused-r1024-comfy-int8-fc2bf16.safetensors) |
| INT8 ConvRot gs256 · fc2 bf16 | ![int8][badge-int8] | 23.13 GiB | [![][gh-xmarre]](https://huggingface.co/xmarre/MiniMax-H3-Pruned-Ref-Delta-Fused-r1024-ComfyUI/resolve/main/MiniMax-H3-Pruned-Ref-Delta-Fused-r1024-comfy-int8-convrot-fc2bf16.safetensors) |

*Keyless follow-up: [xmarre/MiniMax-H3-Keyless](https://github.com/xmarre/MiniMax-H3-Keyless) is the production design spec for a **Keyless Attention** derivative of the BF16 checkpoint — keyless attention and value-space routing, from training/distillation through optimized ComfyUI inference, with INT8 ConvRot as a first-class deployment target. Spec-only at this stage: no trained checkpoint, CUDA kernel, or measured speedup is claimed until the design's empirical gates are completed.*

#### 10Eros-Max (TenStrip) — NSFW Grafted Checkpoints

⚠️ **Contains explicit / NSFW content.** Merged-checkpoint family by [TenStrip](https://huggingface.co/TenStrip/10Eros-Max) — "Eros" grafts NSFW character data from LTX 2.3 (Sulphur lineage), Wan 2.2, and Krea 2 into MiniMax-H3's attention layers at a level that preserves H3's visual and audio quality, built on the delta1024 H3 merge (same delta-extraction class as ethanfel's adapters). Grafting methodology is open-sourced in the repo (`h3_graft_methodology.md`). License: MiniMax H3 Community License **plus** each source model's community license for the grafted portions. Sampling on beta4: euler/simple 6–8 steps, all modes (SLA / sparsity / shift to taste); beta3 is effectively T2V-only (its turbo harms referenced starts in I2V/Ref modes). INT8 mirrors: [cicalooo/10Eros-Max-h3-int8-convrot](https://huggingface.co/cicalooo/10Eros-Max-h3-int8-convrot). t8star's 10ErosMax turbo-LoRA conversions are listed in the [Turbo table](#checkpoints).

| Checkpoint | Precision | Size | Download |
| :--- | :---: | :---: | :--- |
| TURBO-hybrid beta4 (current) | ![bf16][badge-bf16] | 37.46 GB | [![][gh-TenStrip]](https://huggingface.co/TenStrip/10Eros-Max/resolve/main/10Eros_Max_h3_TURBO-hybrid_beta4.safetensors) |
| TURBO-hybrid beta4 · ConvRot | ![int8][badge-int8] | 19.53 GB | [![][gh-TenStrip]](https://huggingface.co/TenStrip/10Eros-Max/resolve/main/10Eros_Max_h3_TURBO-hybrid_beta4_int8_convrot.safetensors) |
| TURBO-hybrid beta3 · T2V-only | ![bf16][badge-bf16] | 37.47 GB | [![][gh-TenStrip]](https://huggingface.co/TenStrip/10Eros-Max/resolve/main/10Eros_Max_h3_TURBO-hybrid_beta3.safetensors) |
| TURBO-hybrid beta3 · ConvRot | ![int8][badge-int8] | 19.54 GB | [![][gh-TenStrip]](https://huggingface.co/TenStrip/10Eros-Max/resolve/main/10Eros_Max_h3_TURBO-hybrid_beta3_int8_convrot.safetensors) |
| TURBO ref2va beta2 | ![bf16][badge-bf16] | 37.47 GB | [![][gh-TenStrip]](https://huggingface.co/TenStrip/10Eros-Max/resolve/main/10Eros_Max_h3_TURBO_ref2va_beta2.safetensors) |
| fl2va beta2 pruned | ![bf16][badge-bf16] | 37.46 GB | [![][gh-TenStrip]](https://huggingface.co/TenStrip/10Eros-Max/resolve/main/10Eros_Max_h3_fl2va_beta2_pruned.safetensors) |
| ref2va beta2 pruned | ![bf16][badge-bf16] | 37.46 GB | [![][gh-TenStrip]](https://huggingface.co/TenStrip/10Eros-Max/resolve/main/10Eros_Max_h3_ref2va_beta2_pruned.safetensors) |

**Beta5 testing line** — [TenStrip/LTX2.3-10Eros_Version-Testing](https://huggingface.co/TenStrip/LTX2.3-10Eros_Version-Testing) (⚠️ gated — manual access approval). Despite the LTX2.3 repo name, the files are H3 checkpoints (`10Eros_Max_h3_*`): TURBO-hybrid and non-turbo hybrid beta5 in BF16 (37.46 GB) and INT8 (19.53 GB), plus W4A8 variants — `graft_preserving` (17.88 GB, with a quality report) and a `14gb_optimized` build (13.04 GB, turbo-hybrid only).

| Checkpoint | Precision | Size | Download |
| :--- | :---: | :---: | :--- |
| TURBO-hybrid beta5 | ![bf16][badge-bf16] | 37.46 GB | [![][gh-TenStrip]](https://huggingface.co/TenStrip/LTX2.3-10Eros_Version-Testing/resolve/main/10Eros_Max_h3_TURBO-hybrid_beta5.safetensors) |
| TURBO-hybrid beta5 · int8 | ![int8][badge-int8] | 19.53 GB | [![][gh-TenStrip]](https://huggingface.co/TenStrip/LTX2.3-10Eros_Version-Testing/resolve/main/10Eros_Max_h3_TURBO-hybrid_beta5_int8.safetensors) |
| TURBO-hybrid beta5 · w4a8 14 GB-optimized | w4a8 | 13.04 GB | [![][gh-TenStrip]](https://huggingface.co/TenStrip/LTX2.3-10Eros_Version-Testing/resolve/main/10Eros_Max_h3_TURBO-hybrid_beta5_w4a8_14gb_optimized.safetensors) |
| hybrid beta5 (no turbo) | ![bf16][badge-bf16] | 37.46 GB | [![][gh-TenStrip]](https://huggingface.co/TenStrip/LTX2.3-10Eros_Version-Testing/resolve/main/10Eros_Max_h3_hybrid_beta5.safetensors) |
| hybrid beta5 · int8 | ![int8][badge-int8] | 19.53 GB | [![][gh-TenStrip]](https://huggingface.co/TenStrip/LTX2.3-10Eros_Version-Testing/resolve/main/10Eros_Max_h3_hybrid_beta5_int8.safetensors) |
| hybrid beta5 · w4a8 graft-preserving | w4a8 | 17.88 GB | [![][gh-TenStrip]](https://huggingface.co/TenStrip/LTX2.3-10Eros_Version-Testing/resolve/main/10Eros_Max_h3_hybrid_beta5_w4a8_graft_preserving.safetensors) |

#### Viggle-Animate (Viggle)

**Character replacement in video from a single repainted frame** — [Viggle](https://viggle.ai/h3)'s product model, a **33.1 B full finetune of MiniMax-H3's `ref2va` transformer**, jointly distilled with DMD to **three forward passes** (26 s a shot on one GPU). Two inputs only — a driving video and one of that video's own frames with the character repainted — and the model propagates the edit across the shot; motion, camera, and timing stay untouched. No pose estimator, segmentation mask, background plate, face tracker, or text encoder at the video stage, and the model is never told what the new character is (no class / identity encoder / user prompt) — strongest where replacement is hardest: fast motion with pose transfer accurate enough to follow it frame for frame. Diffusers-format release ([repo](https://huggingface.co/Viggle/Viggle-Animate)): 14-shard `transformer/` (~61.7 GB), a 2.48 GB DMD LoRA (`lora/`), packaged `MiniMaxH3TransformerBlock` / `MiniMaxH3TokenRefinerBlock` `.pt2` blocks, a fixed forward embed, and `inference/sample.py` (plus an HF Space demo). Weights under the MiniMax H3 Community License; code under a separate LICENSE-CODE.

*ComfyUI-ready quant:* [silveroxides/MiniMax-H3_tests · `viggle-animate-quant/`](https://huggingface.co/silveroxides/MiniMax-H3_tests/tree/main/viggle-animate-quant) hosts `minimax_h3_ref2va_viggle-int8-convrot.safetensors` (31.7 GB) — an INT8 ConvRot conversion of the Viggle-Animate `ref2va` transformer for ComfyUI (Comfy Kitchen format).

#### Singularity HDR Fusion (WarmBloodAban)

**Minimax-h3_Singularity** — comprehensive fine-tuned fusion model for H3 by [WarmBloodAban](https://huggingface.co/WarmBloodAban/Minimax-h3_Singularity): a strategic fusion of key checkpoints (the `ref`, `fl`, and `b25-49` hybrid lineage) followed by deep high-step fine-tuning and three days of precise pruning / weight optimization to fix high-step artifacts. Native T2V / I2V / Ref2V / V2V support in ComfyUI. Improvements: HDR image quality and motion-blur reduction, distant-face restoration (less distortion/collapse in medium-long shots), a clean "de-oiled" aesthetic (no heavy skin shine/gloss), and enhanced dynamic motion and physical impact in complex action sequences. Apache-2.0; online demo on RunningHub. The repo also ships an enhanced [prompt-writing specification](https://huggingface.co/WarmBloodAban/Minimax-h3_Singularity/blob/main/MiniMax_H3_Singularity_Prompt_Writing_Specification_Enhanced_EN.md) for the structured six-section prompt format; the author recommends pairing with the 4-step ref2v turbo LoRA (`minimax_h3_ref2v_turbo_4step_v0.1`) for fast inference. The W4A8 build is newly added and not yet covered in the model card.

| Checkpoint | Precision | Size | Download |
| :--- | :---: | :---: | :--- |
| Singularity ref2va v1.3 | ![int8][badge-int8] | 31.67 GB | [![][gh-WarmBloodAban]](https://huggingface.co/WarmBloodAban/Minimax-h3_Singularity/resolve/main/Minimax-h3_Singularity_ref2va_v1.3_int8.safetensors) |
| Singularity ref2va v1.3 · pruned | ![int8][badge-int8] | 19.53 GB | [![][gh-WarmBloodAban]](https://huggingface.co/WarmBloodAban/Minimax-h3_Singularity/resolve/main/Minimax-h3_Singularity_ref2va_Pruned_v1.3_int8.safetensors) |
| Singularity ref2va v1.3 · pruned W4A8 | ![w4a8][badge-w4a8] | 10.96 GB | [![][gh-WarmBloodAban]](https://huggingface.co/WarmBloodAban/Minimax-h3_Singularity/resolve/main/Minimax-h3_Singularity_ref2va_v1.3_Pruned_w4a8.safetensors) |

**GGUF quants** by [Abiray](https://huggingface.co/Abiray/MiniMax-H3-Singularity-GGUF) — K-quant / Q8_0 with sensitive layers preserved in F32; load with the stock ComfyUI-GGUF loader and pair with the [Abiray GGUF text encoder](#text-encoder).

| GGUF quant | Precision | Size | Download |
| :--- | :---: | :---: | :--- |
| Q3_K_M | ![Q3_K_M][badge-Q3_K_M] | 8.9 GB | [![][gh-Abiray]](https://huggingface.co/Abiray/MiniMax-H3-Singularity-GGUF/resolve/main/Minimax-H3-Singularity-Q3_K_M.gguf) |
| Q4_K_S | ![Q4_K_S][badge-Q4_K_S] | 11.6 GB | [![][gh-Abiray]](https://huggingface.co/Abiray/MiniMax-H3-Singularity-GGUF/resolve/main/Minimax-H3-Singularity-Q4_K_S.gguf) |
| Q4_K_M · recommended for 12 GB | ![Q4_K_M][badge-Q4_K_M] | 11.6 GB | [![][gh-Abiray]](https://huggingface.co/Abiray/MiniMax-H3-Singularity-GGUF/resolve/main/Minimax-H3-Singularity-Q4_K_M.gguf) |
| Q5_K_S | ![Q5_K_S][badge-Q5_K_S] | 14.1 GB | [![][gh-Abiray]](https://huggingface.co/Abiray/MiniMax-H3-Singularity-GGUF/resolve/main/Minimax-H3-Singularity-Q5_K_S.gguf) |
| Q5_K_M · recommended for 16 GB | ![Q5_K_M][badge-Q5_K_M] | 14.1 GB | [![][gh-Abiray]](https://huggingface.co/Abiray/MiniMax-H3-Singularity-GGUF/resolve/main/Minimax-H3-Singularity-Q5_K_M.gguf) |
| Q6_K | ![Q6_K][badge-Q6_K] | 16.7 GB | [![][gh-Abiray]](https://huggingface.co/Abiray/MiniMax-H3-Singularity-GGUF/resolve/main/Minimax-H3-Singularity-Q6_K.gguf) |
| Q8_0 · near-lossless | ![Q8_0][badge-Q8_0] | 21.6 GB | [![][gh-Abiray]](https://huggingface.co/Abiray/MiniMax-H3-Singularity-GGUF/resolve/main/Minimax-H3-Singularity-Q8_0.gguf) |

#### FastH3 DMD2 Distillation (FastVideo)

Official **data-free DMD2 few-step distillation** of MiniMax-H3 FL2VA by the FastVideo team (hao-ai-lab): 50-step base sampled in **4 steps** (`[999, 749, 500, 250]` ladder, cfg 1.0, guidance-distilled), joint video+audio, 768×1344 @ 124 frames. Diffusers-format full pipeline (only `transformer/` differs from base); student trained with VSA block-sparse attention (runnable dense). Preview status — v0.1 = step 1400, [v0.2 = step 2900/4000](https://huggingface.co/FastVideo/FastVideo-Minimax-FastH3-Preview-v0.2); quality still maturing on high-motion detail. MiniMax H3 Community License. A ComfyUI-ready LoRA extraction of this checkpoint by drozbay — rank 64/128 for pruned bases (128 recommended: 17.6 dB PSNR vs the 19.9 dB quant ceiling) plus a full-base r256, all fp16 with the adaln refit onto the pruned curve table — is listed under [Turbo](#checkpoints).

> ℹ️ Note: `Beidouqixing/MiniMax-H3-DMD2-4step` (previously circulated link) is dead (HF 404) — FastVideo's repos are the canonical DMD2 distills.

**8-step V2 — ComfyUI repack** — the current FastH3 line, [FastVideo/FastVideo-FastH3-8-Step-V2](https://huggingface.co/FastVideo/FastVideo-FastH3-8-Step-V2), repackaged by FastVideo as **ComfyUI single-file diffusion models** in [FastVideo/FastVideo-FastH3-Comfy](https://huggingface.co/FastVideo/FastVideo-FastH3-Comfy): drop the files straight into `models/diffusion_models/` + `models/vae/` and load with the stock **Load Diffusion Model** node — no custom loader, no diffusers folder layout. Only the transformer is FastH3; the VAEs are stock H3 (plus an INT8 ConvRot video VAE). Apache-style community license (MiniMax H3 Community License Agreement).

| File | Precision | Size | Download |
| :--- | :---: | :---: | :--- |
| `fastvideo_fasth3_8step_v2_pruned_bf16` | ![bf16][badge-bf16] | 41.1 GB | [![][gh-FastVideo]](https://huggingface.co/FastVideo/FastVideo-FastH3-Comfy/resolve/main/diffusion_models/fastvideo_fasth3_8step_v2_pruned_bf16.safetensors) |
| `fastvideo_fasth3_8step_v2_pruned_int8_convrot` | ![int8][badge-int8] | 20.6 GB | [![][gh-FastVideo]](https://huggingface.co/FastVideo/FastVideo-FastH3-Comfy/resolve/main/diffusion_models/fastvideo_fasth3_8step_v2_pruned_int8_convrot.safetensors) |
| `minimax_h3_video_vae_int8_convrot` | ![int8][badge-int8] | 2.6 GB | [![][gh-FastVideo]](https://huggingface.co/FastVideo/FastVideo-FastH3-Comfy/resolve/main/vae/minimax_h3_video_vae_int8_convrot.safetensors) |

*If you already own the pruned FL2VA checkpoint, [Nynxz/ComfyUI-FastH3Patcher](https://github.com/Nynxz/ComfyUI-FastH3Patcher) reconstructs FastH3 from it with a 4.0 GB patch (149 MB adaLN-only) instead of re-downloading 41 GB — see the node table.*

#### FastH3 & Specialized Quants (NVFP4 / Nunchaku)

Distilled / rotated / Nunchaku-packed checkpoints that need a **custom loader node** (not the stock diffusion-model loader). NVFP4 rows are Blackwell SM120 (native NVFP4); Nunchaku-Lite rows are rootonchair's SVDQuant (NVFP4 group-16 / INT4 group-64, rank-32 low-rank branch) packs of the T2VA transformer for [Nunchaku Lite](https://github.com/mit-han-lab/nunchaku) — each repo holds a data-free build and a calibrated 8×20 build, both diffusers-native one-line `from_pretrained` loads.

| Checkpoint | Precision | Method | Size | Loader | Download |
| :--- | :---: | :--- | :---: | :--- | :--- |
| FastH3 4-step (pottokao) · rotated NVFP4 | ![nvfp4][badge-nvfp4] | Rotated NVFP4 | 12.8 GB | [H3RotNVFP4Loader](https://github.com/pottokao/H3-RotNVFP4-ComfyUI-Loader) | [![][gh-pottokao]](https://huggingface.co/pottokao/MiniMax-H3-FastH3-NVFP4-rotated/resolve/main/h3_fasth3_T1.safetensors) |
| FastH3 8-step (pottokao) · rotated NVFP4 · higher quality | ![nvfp4][badge-nvfp4] | Rotated NVFP4 | 12.5 GB | [H3RotNVFP4Loader](https://github.com/pottokao/H3-RotNVFP4-ComfyUI-Loader) | [![][gh-pottokao]](https://huggingface.co/pottokao/MiniMax-H3-NVFP4-rotated/resolve/main/h3_base_T1.safetensors) |
| FastVideo INT8→NVFP4 (LoboForge) | ![nvfp4][badge-nvfp4] | NVFP4 | 14.5 GB | NVFP4 (Blackwell SM120) | [![][gh-LoboForge]](https://huggingface.co/LoboForge/minimax-h3-fastvideo-nvfp4/resolve/main/minimax_h3_fastvideo_vsa_datafree_1300step_4step_nvfp4.safetensors) |
| Nunchaku-Lite NVFP4 (rootonchair) | ![nvfp4][badge-nvfp4] | SVDQuant NVFP4 (Nunchaku Lite) | ~19 GB | Diffusers / [Nunchaku Lite](https://github.com/mit-han-lab/nunchaku) | [![][gh-rootonchair]](https://huggingface.co/rootonchair/MiniMax-H3-nunchaku-lite-nvfp4) |
| Nunchaku-Lite INT4 (rootonchair) | ![int4][badge-int4] | SVDQuant INT4 (Nunchaku Lite) | ~18.4 GB | Diffusers / [Nunchaku Lite](https://github.com/mit-han-lab/nunchaku) | [![][gh-rootonchair]](https://huggingface.co/rootonchair/MiniMax-H3-nunchaku-lite-int4) |

#### Mixed Quantization (taxexempt)

**Layer-wise mixed-precision** checkpoints — instead of quantizing every layer identically, sensitive layers keep higher precision while tolerant ones drop further (large MLP/FFN → NVFP4 or W4A8, attention → FP8/MXFP8, critical projections → source precision). The stated goal is a better quality / VRAM / speed / size balance than a uniform quant. Loads in recent ComfyUI builds with quantization support (comfy-kitchen); NVFP4/MXFP8 variants target Blackwell. Post-training quantization only — no retraining. [Repo](https://huggingface.co/taxexempt/Custom-MiniMaX-H3-mixed-quants)

| Checkpoint | Precision | Method | Size | Download |
| :--- | :---: | :--- | :---: | :--- |
| `minimax_h3_fl2va_pruned_bf16_fast_blkwl` | ![bf16][badge-bf16] | BF16 (Blackwell-tuned mix) | 12.5 GB | [![][gh-taxexempt]](https://huggingface.co/taxexempt/Custom-MiniMaX-H3-mixed-quants/resolve/main/diffusion_models/minimax_h3_fl2va_pruned_bf16_fast_blkwl.safetensors) |
| `minimax_h3_fl2va_pruned_bf16_mixedq_blkwl` | ![bf16][badge-bf16] | BF16 + mixed quant layers (Blackwell) | 12.5 GB | [![][gh-taxexempt]](https://huggingface.co/taxexempt/Custom-MiniMaX-H3-mixed-quants/resolve/main/diffusion_models/minimax_h3_fl2va_pruned_bf16_mixedq_blkwl.safetensors) |
| `minimax_h3_fl2va_pruned_bf16_w4a8_int8_convrot_mix` | ![int8][badge-int8] | W4A8 + INT8 ConvRot mix | 12.5 GB | [![][gh-taxexempt]](https://huggingface.co/taxexempt/Custom-MiniMaX-H3-mixed-quants/resolve/main/diffusion_models/minimax_h3_fl2va_pruned_bf16_w4a8_int8_convrot_mix.safetensors) |
| `minimax_h3_ref2va_pruned_bf16_mixedq_bal` | ![bf16][badge-bf16] | BF16 + mixed quant layers (balanced) | 12.5 GB | [![][gh-taxexempt]](https://huggingface.co/taxexempt/Custom-MiniMaX-H3-mixed-quants/resolve/main/diffusion_models/minimax_h3_ref2va_pruned_bf16_mixedq_bal.safetensors) |
| `10Eros_Max_h3_TURBO-hybrid_beta4_nvfp4_mxfp8_bf16_mix` | ![nvfp4][badge-nvfp4] | NVFP4 + MXFP8 + BF16 mix | 12.5 GB | [![][gh-taxexempt]](https://huggingface.co/taxexempt/Custom-MiniMaX-H3-mixed-quants/resolve/main/diffusion_models/10Eros_Max_h3_TURBO-hybrid_beta4_nvfp4_mxfp8_bf16_mix.safetensors) |
| `10Eros_Max_h3_TURBO-hybrid_beta4_w4a8_int8_convrot_bf16_mix` | ![int8][badge-int8] | W4A8 + INT8 ConvRot + BF16 mix | 15.6 GB | [![][gh-taxexempt]](https://huggingface.co/taxexempt/Custom-MiniMaX-H3-mixed-quants/resolve/main/diffusion_models/10Eros_Max_h3_TURBO-hybrid_beta4_w4a8_int8_convrot_bf16_mix.safetensors) |
| `h3ErosMax_beta3__bf16_w4a8_int8_convrot_mix` | ![int8][badge-int8] | W4A8 + INT8 ConvRot + BF16 mix | 12.5 GB | [![][gh-taxexempt]](https://huggingface.co/taxexempt/Custom-MiniMaX-H3-mixed-quants/resolve/main/diffusion_models/h3ErosMax_beta3__bf16_w4a8_int8_convrot_mix.safetensors) |

#### Community Merged Checkpoints (EllaPriest45)

Civitai-backup repo of **merged / pre-quantized full checkpoints** — mostly community fine-tunes with a Turbo LoRA already baked in, published as ready-to-load single files. ⚠️ Mixed provenance and licensing (originals are Civitai uploads, credit to the original creators); verify rights before redistributing. Base repo: [EllaPriest45/MinimaxH3_Checkpoints](https://huggingface.co/EllaPriest45/MinimaxH3_Checkpoints).

| Checkpoint | Base | Precision | Size | Download |
| :--- | :--- | :---: | :---: | :--- |
| `10eros ref2va` (fl2va 1.0 str, ref2va 0.7–0.8 str, no turbo LoRA) | Ref2VA | ![bf16][badge-bf16] | 12.2 GB | [![][gh-EllaPriest45]](https://huggingface.co/EllaPriest45/MinimaxH3_Checkpoints/resolve/main/10eros%20ref2va%20-%20MinimaxH3%20-%20fl2va%201str%2Cref2va%200.7-0.8str%2Cno%20turbo%20lora.safetensors) |
| `DaSiWa Hybrid Turbo v3.0` (REF2VA pruned) | Ref2VA | ![int8][badge-int8] | 19.5 GB | [![][gh-EllaPriest45]](https://huggingface.co/EllaPriest45/MinimaxH3_Checkpoints/resolve/main/DaSiWa%20Hybrid%20Turbo%20v3.0%20REF2VA%20Pruned%20INT8%20-%20MinimaxH3%20-%20euler%2Bsimple%2Cshift%20video%206-12%2Caudio%203-5%2C4-8steps.safetensors) |
| `Heptagram Turbo` (REF2VA+FL2VA) | Hybrid | ![int8][badge-int8] | 19.4 GB | [![][gh-EllaPriest45]](https://huggingface.co/EllaPriest45/MinimaxH3_Checkpoints/resolve/main/Heptagram%20Turbo%20REF2VA%2BFL2VA%20-%20MinimaxH3%20-%204-8steps%2Cshift%20video%206-16%2Caudio%203%2Cresmultistep%2Bsimple.safetensors) |
| `Eros Max beta5 Turbo` | FL2VA | ![int8][badge-int8] | 19.5 GB | [![][gh-EllaPriest45]](https://huggingface.co/EllaPriest45/MinimaxH3_Checkpoints/resolve/main/Eros%20Max%20beta5%20Turbo%20INT8%20-%20MinimaxH3.safetensors) |
| `MiniMax-H3 FL2VA W4E8` (10 steps, 544×960, 243 frames) | FL2VA | w4e8 | 11.7 GB | [![][gh-EllaPriest45]](https://huggingface.co/EllaPriest45/MinimaxH3_Checkpoints/resolve/main/MiniMax-H3%20FL2VA%20W4E8%20-%20MinimaxH3%20-%2010steps%2C544x960%2C243frames.safetensors) |
| `MiniMax-H3 REF2VA W4E8` (10 steps, 544×960, 243 frames) | Ref2VA | w4e8 | 11.7 GB | [![][gh-EllaPriest45]](https://huggingface.co/EllaPriest45/MinimaxH3_Checkpoints/resolve/main/MiniMax-H3%20REF2VA%20W4E8%20-%20MinimaxH3%20-%2010steps%2C544x960%2C243frames.safetensors) |
| `MiniMax-H3 FL2VA-Curve Q5_1` | FL2VA | ![Q5_1][badge-Q5_1] | 14.2 GB | [![][gh-EllaPriest45]](https://huggingface.co/EllaPriest45/MinimaxH3_Checkpoints/resolve/main/MiniMax-H3%20FL2VA-Curve%20Q5_1%20-%20MinimaxH3.gguf) |
| `MiniMax-H3 REF2VA-Curve Q5_1` (0.6 str, 8 steps) | Ref2VA | ![Q5_1][badge-Q5_1] | 14.2 GB | [![][gh-EllaPriest45]](https://huggingface.co/EllaPriest45/MinimaxH3_Checkpoints/resolve/main/MiniMax-H3%20REF2VA-Curve%20Q5_1%20-%20MinimaxH3%20-%200.6str%2C8steps.gguf) |
| `PinkCherry v1.8 Hybrid` (light2xv turbo 12 steps / 30 alone, 0.7 MP+) | Hybrid | ![int8][badge-int8] | 19.6 GB | [![][gh-EllaPriest45]](https://huggingface.co/EllaPriest45/MinimaxH3_Checkpoints/resolve/main/PinkCherry%20v1.8%20Hybrid%20INT8%20-%20MinimaxH3%20-%20euler%2Bsimple%2C12steps%20with%20light2xv%20turbo%2C30steps%20alone%2C0.7MP%2B.safetensors) |
| `RedCraft A2A` | A2A | ![int8][badge-int8] | 19.5 GB | [![][gh-EllaPriest45]](https://huggingface.co/EllaPriest45/MinimaxH3_Checkpoints/resolve/main/RedCraft%20A2A%20INT8%20-%20MinimaxH3.safetensors) |
| `Singularity REF2VA Pruned v1.3` | Ref2VA | ![int8][badge-int8] | 19.5 GB | [![][gh-EllaPriest45]](https://huggingface.co/EllaPriest45/MinimaxH3_Checkpoints/resolve/main/Singularity%20REF2VA%20Pruned%20v1.3%20INT8%20-%20MinimaxH3.safetensors) |

#### All-in-One Starter Pack (EllaPriest45)

[EllaPriest45/MinimaxH3_base](https://huggingface.co/EllaPriest45/MinimaxH3_base) is a **single-download H3 starter bundle** — ~85 files (~85 GB) covering an entire working setup, all prefixed by role so the destination folder is obvious (`diffusionmodel_`, `textencoder_`, `vae_`, `lora_`, `workflow_`) alongside the zipped ComfyUI custom-node repos. Includes INT8 ConvRot pruned FL2VA + Ref2VA transformers, Qwen3-VL-32B text encoders (Q2_K / Q4_K_M GGUF + mmproj F16), video/audio/TAE VAEs, the main Turbo LoRAs (lightx2v, larryvrh, HardGravy2, FastH3, PK Parasyte, Motion Adapter, Semantic Bridge, Video Reasoning), ~10 ready ComfyUI workflow JSONs, and ~38 zipped node packs spanning conditioning, prompt-writing, acceleration (SageAttention, TeaCache, Sol-Attn, Spectrum, DLSS5), memory management (FreeMemory, UniBlockSwap) and utilities. ⚠️ Civitai-backup provenance and mixed licensing; node ZIPs are snapshots (install from upstream repos for updates).

#### VDN-H3 (Video DeltaNet)

**Video DeltaNet** — a hybrid-attention architecture that adds a constant-cost **linear-attention (Video Delta Attention) branch** plus two small LoRA adapters on top of the MiniMax-H3 backbone, replacing quadratic long-range attention so inference cost grows *linearly* with clip length. Plug-and-play: the branch + adapters merge into the backbone at inference without touching backbone weights. The 8-step DMD stage (`stage-dmd-step-250`) runs near-lossless vs dense H3. Reference impl: [OpenVDN/vdn-minimax-h3](https://github.com/OpenVDN/vdn-minimax-h3) (Apache-2.0); weights under the MiniMax H3 Community License (excludes EU/UK/Korea/US).

* **[OpenVDN/vdn-minimax-h3](https://huggingface.co/OpenVDN/vdn-minimax-h3)** — reference weights (~82 GB): `h3-base/` MiniMax-H3 backbone (transformer + video/audio VAEs, ~72 GB) plus two stages — `stage-b-step-2000` (linear branch + default adapter) and `stage-dmd-step-250` (8-step DMD: linear branch + default + turbo adapters).
* **[t8star/Vdn-Minimax-H3-Comfy](https://huggingface.co/t8star/Vdn-Minimax-H3-Comfy)** — ComfyUI-ready VDN bundle. Key files: `minimax_h3_fl2va_int8_convrot.safetensors` (34.0 GB), `minimax_h3_fl2va_pruned_int8_convrot.safetensors` (21.0 GB), `qwen3vl_32b_minimax_h3_nvfp4_awq.safetensors` text encoder (15.7 GB, NVFP4 AWQ), video VAE fp16 (5.2 GB), audio VAE fp32 (0.61 GB), plus the stage-dmd adapters (default 334 MB / turbo 851 MB / turbo_pruned_curve_fl2va 1.15 GB) and 4.28 GB linear branch.
* **[drbaph/vdn-minimax-h3-int8-convrot-comfyui](https://huggingface.co/drbaph/vdn-minimax-h3-int8-convrot-comfyui)** — pre-quantized `stage-dmd-step-250` INT8 ConvRot (Comfy Kitchen) for ComfyUI-VDN-H3: `linear_branch/model_int8_convrot_comfyui.safetensors` (2.30 GB int8, was 4.28 GB bf16) + `adapters/default` (334 MB) + `adapters/turbo` (851 MB); stage ~3.4 GB. Requires ComfyUI-VDN-H3 v1.3.0+.
* **[Saganaki22/ComfyUI-VDN-H3](https://github.com/Saganaki22/ComfyUI-VDN-H3)** — native ComfyUI node (port of OpenVDN, not a fork) that applies the VDN hybrid-attention patches as runtime model patches; no ComfyUI core changes, zero new deps. See the node table.
* **[OpenVDN/vdn-minimax-h3-edge](https://huggingface.co/OpenVDN/vdn-minimax-h3-edge)** — prepared **FP8** package for [FreeVideo](https://github.com/FlashML-org/FreeVideo) (~22.9 GB / 21.4 GiB per install; users do not pick a format or download both). Two routes: `cache/` per-tensor FP8 for Blackwell / RTX 50, and `rowwise/cache/` per-channel FP8 for Ada / RTX 40, Hopper / SM90 and Ampere / RTX 30 (Ampere pairs rowwise storage with BF16 compute). Slim format **omits the original AdaLN projections** (~26.02 GB saved) and ships the fixed 8-step T2V + visual-keyframe modulation tables as required assets instead — so a modulation-changing LoRA or an unsupported schedule needs the pinned [historical revision](https://huggingface.co/OpenVDN/vdn-minimax-h3-edge/tree/4f16eb1066d96592b84be0de532069f5d69fcfa9). Ordinary attention/FF LoRAs are unaffected. No new benchmark is published for this release — the card states it adds a byte-preserving rowwise package only.

#### Veda Sparse Attention (Miowtion)

**Veda** — a distilled **sparse-attention tile-score predictor** for MiniMax-H3 from the Miowtion project (ICML 2026, [arXiv 2605.30325](https://arxiv.org/abs/2605.30325)). Per layer and per head it scores 128-token key tiles against query tiles and keeps only **10%**, so attention runs block-sparse instead of dense. It replaces attention block selection *only* — denoiser, schedule and VAE are untouched, and it is orthogonal to the few-step LoRA it runs under. Runtime path is [Veda-Sparse/Miowtion](https://github.com/veda-sparse/Miowtion) (there is no ComfyUI loader). The predictor file also carries its **tile plans** in `__metadata__` — 12 geometries (16:9 / 9:16 / 4:3 / 1:1 × latent_t 37 / 72 / 102 = 5.17 / 10.1 / 14.4 s); predictor and plan must ship in the same file, a mismatched pairing is silent. Weights are fp8 e4m3 with per-head amax scales, dequantized to bf16 at load (top-k selection is invariant to per-row rescaling, so fp8 vs bf16 moves recall by 2e-5). Preview: 600 updates on 5.17 s clips only.

Measured on an RTX 4090 (weights offloaded to host, FL2VA + 8-step Turbo LoRA, 20 held-out prompts, keep 0.1, step 0 excluded): **2.24× end-to-end / 5.92× attention** overall, and the gain grows with clip length — 1.57× at 5.17 s, 2.21× at 10.1 s, 2.76× at 14.4 s (best single clip 3.08× / 6.87×), because attention is 42% of a dense step at the short end but 71% at the long one. Sparse output is *not* bit-exact against dense, and at a 10% keep ratio even an oracle mask recovers only ~0.63 of the attainable attention mass. **T2VA only.**

| Predictor | Precision | Size | Download |
| :--- | :---: | :---: | :--- |
| T2VA Veda 8-NFE · 600-step preview | ![fp8][badge-fp8] | 263 MB | [![][gh-Veda--Sparse]](https://huggingface.co/Veda-Sparse/Minimax-H3-T2VA-Veda-8NFE-600Step-Preview/resolve/main/minimax_h3_t2va_veda_8nfe_600step_preview_fp8.safetensors) |

#### TaoMate-H3 (Alibaba TaoLive, streaming)

**TaoMate-H3** — low-latency **streaming audio-video generation runtime** from the Alibaba TaoLive AIGC Team, built on MiniMax-H3 FL2VA. Generates synchronized audio and video in small chunks (three Stage3 denoising intervals per chunk) with low per-chunk latency, and supports continuous long-form generation at 480p/768p/1080p — clean KV cache + integrated audio guidance preserve identity, voice, and motion across prompt boundaries (one prompt per 5-second block via `--prompt-json`). Single-node inference on Linux + Hopper GPUs (4 or 8 × H20 96 GB validated; TP2 + Ulysses sequence parallelism).

* **Model** — [TaoLiveAIGC/TaoMate-H3](https://huggingface.co/TaoMate-H3): step-3000 generator **EMA LoRA adapter** (rank 128, alpha 128; tensors stored losslessly FP32, runtime materializes BF16), 2.31 GB, plus config/adapter JSONs. MiniMax H3 Community License (NOTICE applies). Base MiniMax-H3 FL2VA downloaded separately.
* **Runtime** — [TaoLiveAIGC/TaoMate-H3](https://github.com/TaoLiveAIGC/TaoMate-H3) (Python, `pip install -e .`): PyTorch 2.8 + CUDA 12.8, vLLM 0.11.1, Hopper flash-attention; auto-downloads the adapter on first run.
* **ComfyUI conversions** — [drbaph](https://huggingface.co/drbaph/MiniMax-H3-Turbo-Lora-ComfyUI) repacked the adapter as `minimax_h3_taomate_fl2va_3step_ema_comfyui.safetensors` (experimental, with recommended 3/4-step sigma ladders — see Turbo), and [Kijai/MiniMax-H3_comfy](https://huggingface.co/Kijai/MiniMax-H3_comfy) hosts a resized `minimax_h3_taomate_3step_lora_avg_rank_19_bf16.safetensors`.

#### Notes

* **t8star Ref2VA patchin HF 1.02** — experimental weight modification (not a quant): +2% on 2×2 spatial HF patch in the video-input projection. Tests showed weak HF agent gain; "oily/waxy" look not confirmed removed. [Repo](https://huggingface.co/t8star/minimax_h3_ref2va_patchin_hf102). (31.70 GB, INT8 ConvRot, listed in the Ref2VA table above with `*(patchin)*` label.)
* **coolthor/MiniMax-H3-pruned-NVFP4** — ⚠️ gated (auto) all-in-one Blackwell bundle around the pruned NVFP4 pair (FL2VA + Ref2VA, 11.67 GB each — mirrored in the unified tables above): Ultra-Heretic TE NVFP4 (14.61 GB), lightx2v 4-step turbo LoRAs (fl2v 768p SLA + ref2v, 1.82 GB each), stock fp16/fp32 VAEs, the bundled [ComfyUI-CondCache](https://huggingface.co/coolthor/MiniMax-H3-pruned-NVFP4/tree/main/custom_nodes/ComfyUI-CondCache) node + LTX generic-refine conditioning cache, and LTX-hybrid-refine workflows. [Repo](https://huggingface.co/coolthor/MiniMax-H3-pruned-NVFP4)
* **corechan/MiniMax_H3_Torchao018** — torchao quants for the native H3 WebUI/diffusers stack (not ComfyUI single-file, unofficial): `quantized/transformer-nvfp4` + `quantized/transformer_ref-nvfp4` (FL2VA + Ref2VA, 18.52 GB each in 3 shards) and `quantized/text_encoder-int8` (25.74 GB), saved via `save_pretrained` from a running session. The text encoder is **split in two**: layers 0–50 are what H3 uses for prompt encoding, while layers 51–63 + `lm_head` (the prompt assistant / LLM tab) ship separately as `quantized/text_encoder-llm-tail/tail_int8.safetensors` (7.36 GB, torchao `Int8WeightOnlyConfig` v2) and `tail_nf4.safetensors` (4.49 GB, bitsandbytes `Linear4bit` NF4, double-quant, bf16 compute) — pick one, `lm_head` stays bf16 in both. Measured on an RTX PRO 6000 (G4): the prompt assistant runs at 7.7 tok/s with `tail_int8` (+7.4 GB VRAM) vs 9.2 tok/s with `tail_nf4` (+4.5 GB). Version-locked: pickle-form torchao artifacts require torchao **0.18.x** — the `.complete` markers record 0.18.0 + torch 2.11.0+cu128, and the pickle form ties you to that exact torchao build. NVFP4 needs Blackwell (sm_100/sm_120); INT8/NF4 also run on Ampere/Hopper, and `tail_nf4` needs `bitsandbytes`. VAE / audio VAE / tokenizer are **not** included — take them from the official repo. [Repo](https://huggingface.co/corechan/MiniMax_H3_Torchao018)
* **DmitryDB/MiniMax-H3-INT8-Lean-ConvRot** is the same repo as **DmitryDB/MiniMax-H3-ComfyUI-Quants** (merged/rebranded by the author). Both names resolve to the same files.
* **DmitryDB/MiniMax-H3-INT8-Lean-ConvRot-Dynamic-Time-Separate-QKV** is the same repo as **DmitryDB/MiniMax-H3-DynTime-sQKV**. Both names resolve to the same files.
* **Winnougan/MiniMax-H3-INT4_Convrot_ComfyUI** also includes a matching quantized text encoder: [`qwen3vl_32b_minimax_h3-w4a8_convrot.safetensors`](https://huggingface.co/Winnougan/MiniMax-H3-INT4_Convrot_ComfyUI/resolve/main/qwen3vl_32b_minimax_h3-w4a8_convrot.safetensors).
* **koongrizzly/MiniMax_H3_int4_W4A8_ConvRot_Pruned** — low-VRAM bundle for the [MiniMax_H3_Standalone_app](https://github.com/Koongrizzly/MiniMax_H3_Standalone_app): byte-identical mirrors of Winnougan's three W4A8 ConvRot files (pruned FL2VA + Ref2VA transformers 11.68 GiB each, already listed above, and the matching 14.62 GiB TE), a mixed FP16/FP32 **video VAE** (4.9 GB, most tensors converted to FP16), the stock FP32 audio VAE (577 MB), plus two third-party **hybrid** ref2va checkpoints (11.68 GiB each) — one from berryber09 ([ref2va-fl2va hybrid W4A8](https://huggingface.co/berryber09/MiniMax-H3-ref2va-fl2va-hybrid-w4a8), lets one job take a start image + references) and one from Aki7777777 (`minimaxH3_hybrid_Sparseref15_prunedPartialINT8V10`, via [Civitai](https://civitai.com/models/2900456/minimax-h3sparseref15hybrid)). Also carries copies of the `h3-realism-people` LoRA and the `turbo_v4_step600_ema` pruned LoRA. [Repo](https://huggingface.co/koongrizzly/MiniMax_H3_int4_W4A8_ConvRot_Pruned)
* **Kijai/MiniMax-H3-experimental** also includes an INT8 ConvRot video VAE: [`minimax_h3_video_vae_int8_convrot.safetensors`](https://huggingface.co/Kijai/MiniMax-H3-experimental/resolve/main/minimax_h3_video_vae_int8_convrot.safetensors) (2.95 GB). See [Components](#components).
* **unsloth/MiniMax-H3-GGUF** also includes Qwen3-VL text encoder GGUFs: Q2_K_M (12.2 GB) and Q4_K_M (17.0 GB).
* **DmitryDB/MiniMax-H3-ComfyUI-Quants** also includes VAE files: Video VAE FP16 (4.85 GB) and Audio VAE FP32 (577 MB). See [Components](#components).
* **DiffSynth-Studio/MiniMax-H3-NF4** also includes TE, Video VAE, and Audio VAE NF4 quants. Requires [DiffSynth-Studio](https://github.com/modelscope/DiffSynth-Studio); minimum 8 GB VRAM.
* **WaveCut/MiniMax-H3-OrbitQuant-W4A4** also includes quantized text encoder and FP32 VAE copies. Requires [ComfyUI-OrbitQuant](https://github.com/iamwavecut/ComfyUI-OrbitQuant/tree/feature/minimax-h3-comfyui) custom node. [Workflow JSON](https://huggingface.co/WaveCut/MiniMax-H3-OrbitQuant-W4A4/resolve/main/comfyui/workflows/MiniMax-H3-OrbitQuant-T2VA.json).
* **DeepBeepMeep/MiniMax-H3** is a community repack bundling both FL2VA and Ref2VA in every precision/pruning combination: full `bf16` (66.3 GB) and `int8_convrot` (34 GB); `pruned` `bf16` (41.4 GB) and `int8_convrot` (22.1 GB); and `pruned_rank8` `bf16` (40.3 GB) and `int8_convrot` (21.1 GB). Also ships VAEs (video `fp16` 5.21 GB, video `fp8mix` 2.79 GB, audio `fp32` 605 MB), a Qwen3-VL-32B text encoder (`nvfp4_awq` + `Q4_K_M` GGUF), and SeedVR2 upscaler checkpoints. **No license is stated** — clarify usage rights before redistributing. [Repo](https://huggingface.co/DeepBeepMeep/MiniMax-H3)
