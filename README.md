# Awesome MiniMax-H3

A curated list of models, text encoders, quants, and tools for the MiniMax-H3 omni-modal video generation model.

<div align="center">

<img src="https://github.com/user-attachments/assets/0c373d38-4c80-4140-b17e-4cfc6aa281c7" />

[![Telegram][telegram-shield]][telegram-url]
[![X][x-shield]][x-url]

</div>

<details>
<summary><b>Table of Contents</b></summary>

* [Models](#models)
  * [Checkpoints](#checkpoints)
  * [Quantized Models](#quants)
    * [GGUF](#gguf)
    * [Fine-tuned Checkpoints](#finetunes)
* [Text Encoders](#text-encoder)
* [Separated Components](#components)
  * [VAE (Video & Audio)](#components-vae)
  * [Tiny Autoencoder (TAE)](#tae)
  * [Image VAE (Mamad8)](#cliproj)
  * [Clip Projection (ClipProj)](#cliproj)
* [LoRA](#lora)
  * [All LoRAs](#lora)
  * [Collections](#lora)
  * [Turbo (Acceleration LoRA)](#checkpoints)
* [ComfyUI Nodes](#nodes)
  * [Custom Node Collections](#nodes)
  * [Special Stuff](#nodes)
* [Guides & Tutorials](#guides)
* [Workflow & Technical Notes](#wf)
  * [ComfyUI](#wf-comfyui)

</details>

<a id="intro"></a>

## Intro

* [MiniMax-H3 official model card](https://huggingface.co/MiniMaxAI/MiniMax-H3)
* ComfyUI official [blogpost](https://blog.comfy.org/p/minimax-h3-day-0-support-in-comfyui)
* [ComfyUI tutorials for MiniMax-H3](https://docs.comfy.org/tutorials/video/minimax/minimax-h3)
* [Video Prompt Writing Guide (Base)](https://huggingface.co/MiniMaxAI/MiniMax-H3/blob/main/docs/VIDEO_PROMPT_WRITING_GUIDE_base_en.md)
* [Video Prompt Writing Guide (Reference)](https://huggingface.co/MiniMaxAI/MiniMax-H3/blob/main/docs/VIDEO_PROMPT_WRITING_GUIDE_ref_en.md)

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

*larryvrh also publishes experimental training checkpoints (11 `.bin` files: step 149/490/729/850/922, v2 step 298, v3 step 300, v4 step 150/600, v5 step 600; 7.26–10.17 GB) — see the [repo](https://huggingface.co/larryvrh/MiniMax-H3-Turbo-Lora/tree/main).*

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
| ✓ | ![nvfp4][badge-nvfp4] | NVFP4 | 18.69 GB | [![][gh-rockerBOO]](https://huggingface.co/rockerBOO/minimax-h3-nvfp4/resolve/main/minimax_h3_fl2va_pruned_nvfp4.safetensors) |
| ✓ | ![nvfp4][badge-nvfp4] | NVFP4 + ConvRot INT8 | 18.69 GB | [![][gh-rockerBOO]](https://huggingface.co/rockerBOO/minimax-h3-nvfp4/resolve/main/minimax_h3_fl2va_pruned_nvfp4_convrot_int8.safetensors) |
| ✓ | ![nvfp4][badge-nvfp4] | NVFP4 | 11.67 GB | [![][gh-Abiray]](https://huggingface.co/Abiray/Minimax-H3-nvfp4-INT4-INT8-Convrot/resolve/main/MiniMax_H3_FL2VA_pruned_nvfp4.safetensors) ┊ [![][gh-coolthor]](https://huggingface.co/coolthor/MiniMax-H3-pruned-NVFP4/resolve/main/diffusion_models/minimax_h3_fl2va_pruned_nvfp4.safetensors) |
| ✓ | ![int4][badge-int4] | Mixed INT4/INT8 ConvRot | 14.81 GB | [![][gh-Abiray]](https://huggingface.co/Abiray/Minimax-H3-nvfp4-INT4-INT8-Convrot/resolve/main/MiniMax_H3_FL2VA_pruned_mixed_int4_int8_convrot.safetensors) ┊ [![][gh-tsolful]](https://huggingface.co/tsolful/Minimax_H3_INT4MixedConvRot/resolve/main/minimax_h3_fl2va_pruned_INT4BQ.safetensors) |
| ✓ | ![int4][badge-int4] | Mixed INT4/INT8 ConvRot Lean | 17.27 GB | [![][gh-tsolful]](https://huggingface.co/tsolful/Minimax_H3_INT4MixedConvRot/resolve/main/minimax_h3_fl2va_pruned_INT4Q.safetensors) |
| ✓ | ![int4][badge-int4] | INT4 ConvRot | 15.67 GB | [![][gh-rockerBOO]](https://huggingface.co/rockerBOO/minimax-h3-nvfp4/resolve/main/minimax_h3_fl2va_pruned_int4_convrot_simple.safetensors) |
| ✓ | ![int4][badge-int4] | Mixed INT4/INT8 ConvRot | 18.92 GB | [![][gh-rockerBOO]](https://huggingface.co/rockerBOO/minimax-h3-nvfp4/resolve/main/minimax_h3_fl2va_pruned_mixed_int4_int8_convrot_simple.safetensors) |
| ✓ | ![int4][badge-int4] | W4A8 ConvRot | 11.68 GB | [![][gh-AX1Y2JP]](https://huggingface.co/AX1Y2JP/MiniMax-H3-W4A8-ConvRot/resolve/main/minimax_h3_fl2va_pruned_symw4a8convrot.safetensors) ┊ [![][gh-Kijai]](https://huggingface.co/Kijai/MiniMax-H3-experimental/resolve/main/minimax_h3_fl2va_pruned_w4a8_mixed.safetensors) ┊ [![][gh-Winnougan]](https://huggingface.co/Winnougan/MiniMax-H3-INT4_Convrot_ComfyUI/resolve/main/minimax_h3_fl2va_pruned-w4a8_convrot_pruned.safetensors) |

*GGUF quants — see [GGUF section](#gguf) below.*

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
| `DaSiWa Hybrid Turbo v2.0` | Hybrid | ![int8][badge-int8] | 19.5 GB | [![][gh-EllaPriest45]](https://huggingface.co/EllaPriest45/MinimaxH3_Checkpoints/resolve/main/DaSiWa%20Hybrid%20Turbo%20v2.0%20INT8%20-%20MinimaxH3%20-%20euler%2Bsimple%2Cshift%20video%206-12%2Caudio%203-5%2C4steps.safetensors) |
| `Eros Max beta5 Turbo` | FL2VA | ![int8][badge-int8] | 19.5 GB | [![][gh-EllaPriest45]](https://huggingface.co/EllaPriest45/MinimaxH3_Checkpoints/resolve/main/Eros%20Max%20beta5%20Turbo%20INT8%20-%20MinimaxH3.safetensors) |
| `MiniMax-H3 FL2VA W4E8` (10 steps, 544×960, 243 frames) | FL2VA | w4e8 | 11.7 GB | [![][gh-EllaPriest45]](https://huggingface.co/EllaPriest45/MinimaxH3_Checkpoints/resolve/main/MiniMax-H3%20FL2VA%20W4E8%20-%20MinimaxH3%20-%2010steps%2C544x960%2C243frames.safetensors) |
| `MiniMax-H3 REF2VA W4E8` (10 steps, 544×960, 243 frames) | Ref2VA | w4e8 | 11.7 GB | [![][gh-EllaPriest45]](https://huggingface.co/EllaPriest45/MinimaxH3_Checkpoints/resolve/main/MiniMax-H3%20REF2VA%20W4E8%20-%20MinimaxH3%20-%2010steps%2C544x960%2C243frames.safetensors) |
| `MiniMax-H3 FL2VA-Curve Q5_1` | FL2VA | ![Q5_1][badge-Q5_1] | 14.2 GB | [![][gh-EllaPriest45]](https://huggingface.co/EllaPriest45/MinimaxH3_Checkpoints/resolve/main/MiniMax-H3%20FL2VA-Curve%20Q5_1%20-%20MinimaxH3.gguf) |
| `MiniMax-H3 REF2VA-Curve Q5_1` (0.6 str, 8 steps) | Ref2VA | ![Q5_1][badge-Q5_1] | 14.2 GB | [![][gh-EllaPriest45]](https://huggingface.co/EllaPriest45/MinimaxH3_Checkpoints/resolve/main/MiniMax-H3%20REF2VA-Curve%20Q5_1%20-%20MinimaxH3%20-%200.6str%2C8steps.gguf) |
| `PinkCherry v0.6` | FL2VA | ![int8][badge-int8] | 19.5 GB | [![][gh-EllaPriest45]](https://huggingface.co/EllaPriest45/MinimaxH3_Checkpoints/resolve/main/PinkCherry%20v0.6%20INT8%20-%20MinimaxH3.safetensors) |
| `RedCraft A2A` | A2A | ![int8][badge-int8] | 19.5 GB | [![][gh-EllaPriest45]](https://huggingface.co/EllaPriest45/MinimaxH3_Checkpoints/resolve/main/RedCraft%20A2A%20INT8%20-%20MinimaxH3.safetensors) |

#### All-in-One Starter Pack (EllaPriest45)

[EllaPriest45/MinimaxH3_base](https://huggingface.co/EllaPriest45/MinimaxH3_base) is a **single-download H3 starter bundle** — ~85 files (~85 GB) covering an entire working setup, all prefixed by role so the destination folder is obvious (`diffusionmodel_`, `textencoder_`, `vae_`, `lora_`, `workflow_`) alongside the zipped ComfyUI custom-node repos. Includes INT8 ConvRot pruned FL2VA + Ref2VA transformers, Qwen3-VL-32B text encoders (Q2_K / Q4_K_M GGUF + mmproj F16), video/audio/TAE VAEs, the main Turbo LoRAs (lightx2v, larryvrh, HardGravy2, FastH3, PK Parasyte, Motion Adapter, Semantic Bridge, Video Reasoning), ~10 ready ComfyUI workflow JSONs, and ~38 zipped node packs spanning conditioning, prompt-writing, acceleration (SageAttention, TeaCache, Sol-Attn, Spectrum, DLSS5), memory management (FreeMemory, UniBlockSwap) and utilities. ⚠️ Civitai-backup provenance and mixed licensing; node ZIPs are snapshots (install from upstream repos for updates).

#### VDN-H3 (Video DeltaNet)

**Video DeltaNet** — a hybrid-attention architecture that adds a constant-cost **linear-attention (Video Delta Attention) branch** plus two small LoRA adapters on top of the MiniMax-H3 backbone, replacing quadratic long-range attention so inference cost grows *linearly* with clip length. Plug-and-play: the branch + adapters merge into the backbone at inference without touching backbone weights. The 8-step DMD stage (`stage-dmd-step-250`) runs near-lossless vs dense H3. Reference impl: [OpenVDN/vdn-minimax-h3](https://github.com/OpenVDN/vdn-minimax-h3) (Apache-2.0); weights under the MiniMax H3 Community License (excludes EU/UK/Korea/US).

* **[OpenVDN/vdn-minimax-h3](https://huggingface.co/OpenVDN/vdn-minimax-h3)** — reference weights (~82 GB): `h3-base/` MiniMax-H3 backbone (transformer + video/audio VAEs, ~72 GB) plus two stages — `stage-b-step-2000` (linear branch + default adapter) and `stage-dmd-step-250` (8-step DMD: linear branch + default + turbo adapters).
* **[t8star/Vdn-Minimax-H3-Comfy](https://huggingface.co/t8star/Vdn-Minimax-H3-Comfy)** — ComfyUI-ready VDN bundle. Key files: `minimax_h3_fl2va_int8_convrot.safetensors` (34.0 GB), `minimax_h3_fl2va_pruned_int8_convrot.safetensors` (21.0 GB), `qwen3vl_32b_minimax_h3_nvfp4_awq.safetensors` text encoder (15.7 GB, NVFP4 AWQ), video VAE fp16 (5.2 GB), audio VAE fp32 (0.61 GB), plus the stage-dmd adapters (default 334 MB / turbo 851 MB / turbo_pruned_curve_fl2va 1.15 GB) and 4.28 GB linear branch.
* **[drbaph/vdn-minimax-h3-int8-convrot-comfyui](https://huggingface.co/drbaph/vdn-minimax-h3-int8-convrot-comfyui)** — pre-quantized `stage-dmd-step-250` INT8 ConvRot (Comfy Kitchen) for ComfyUI-VDN-H3: `linear_branch/model_int8_convrot_comfyui.safetensors` (2.30 GB int8, was 4.28 GB bf16) + `adapters/default` (334 MB) + `adapters/turbo` (851 MB); stage ~3.4 GB. Requires ComfyUI-VDN-H3 v1.3.0+.
* **[Saganaki22/ComfyUI-VDN-H3](https://github.com/Saganaki22/ComfyUI-VDN-H3)** — native ComfyUI node (port of OpenVDN, not a fork) that applies the VDN hybrid-attention patches as runtime model patches; no ComfyUI core changes, zero new deps. See the node table.

#### TaoMate-H3 (Alibaba TaoLive, streaming)

**TaoMate-H3** — low-latency **streaming audio-video generation runtime** from the Alibaba TaoLive AIGC Team, built on MiniMax-H3 FL2VA. Generates synchronized audio and video in small chunks (three Stage3 denoising intervals per chunk) with low per-chunk latency, and supports continuous long-form generation at 480p/768p/1080p — clean KV cache + integrated audio guidance preserve identity, voice, and motion across prompt boundaries (one prompt per 5-second block via `--prompt-json`). Single-node inference on Linux + Hopper GPUs (4 or 8 × H20 96 GB validated; TP2 + Ulysses sequence parallelism).

* **Model** — [TaoLiveAIGC/TaoMate-H3](https://huggingface.co/TaoMate-H3): step-3000 generator **EMA LoRA adapter** (rank 128, alpha 128; tensors stored losslessly FP32, runtime materializes BF16), 2.31 GB, plus config/adapter JSONs. MiniMax H3 Community License (NOTICE applies). Base MiniMax-H3 FL2VA downloaded separately.
* **Runtime** — [TaoLiveAIGC/TaoMate-H3](https://github.com/TaoLiveAIGC/TaoMate-H3) (Python, `pip install -e .`): PyTorch 2.8 + CUDA 12.8, vLLM 0.11.1, Hopper flash-attention; auto-downloads the adapter on first run.
* **ComfyUI conversions** — [drbaph](https://huggingface.co/drbaph/MiniMax-H3-Turbo-Lora-ComfyUI) repacked the adapter as `minimax_h3_taomate_fl2va_3step_ema_comfyui.safetensors` (experimental, with recommended 3/4-step sigma ladders — see Turbo), and [Kijai/MiniMax-H3_comfy](https://huggingface.co/Kijai/MiniMax-H3_comfy) hosts a resized `minimax_h3_taomate_3step_lora_avg_rank_19_bf16.safetensors`.

#### Notes

* **t8star Ref2VA patchin HF 1.02** — experimental weight modification (not a quant): +2% on 2×2 spatial HF patch in the video-input projection. Tests showed weak HF agent gain; "oily/waxy" look not confirmed removed. [Repo](https://huggingface.co/t8star/minimax_h3_ref2va_patchin_hf102). (31.70 GB, INT8 ConvRot, listed in the Ref2VA table above with `*(patchin)*` label.)
* **coolthor/MiniMax-H3-pruned-NVFP4** — ⚠️ gated (auto) all-in-one Blackwell bundle around the pruned NVFP4 pair (FL2VA + Ref2VA, 11.67 GB each — mirrored in the unified tables above): Ultra-Heretic TE NVFP4 (14.61 GB), lightx2v 4-step turbo LoRAs (fl2v 768p SLA + ref2v, 1.82 GB each), stock fp16/fp32 VAEs, the bundled [ComfyUI-CondCache](https://huggingface.co/coolthor/MiniMax-H3-pruned-NVFP4/tree/main/custom_nodes/ComfyUI-CondCache) node + LTX generic-refine conditioning cache, and LTX-hybrid-refine workflows. [Repo](https://huggingface.co/coolthor/MiniMax-H3-pruned-NVFP4)
* **corechan/MiniMax_H3_Torchao018** — torchao quants for the native H3 WebUI/diffusers stack (not ComfyUI single-file): `quantized/transformer-nvfp4` + `quantized/transformer_ref-nvfp4` (FL2VA + Ref2VA, 18.52 GB each in 3 shards) and `quantized/text_encoder-int8` (25.74 GB), saved via `save_pretrained` from a running session. Version-locked: pickle-form torchao artifacts require torchao **0.18.0** + torch 2.11 (`.complete` markers) — match your environment before loading. [Repo](https://huggingface.co/corechan/MiniMax_H3_Torchao018)
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
<p id="text-encoder" align="center">◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆</p>

## ▓ Text Encoders

MiniMax-H3 uses the Qwen3-VL-32B model as its text/vision conditioning encoder.

### ▣ Comfy-Org Optimized Encoders

Official and optimized versions for ComfyUI, repackaged by [Comfy-Org](https://huggingface.co/Comfy-Org/MiniMax-H3).

| Model Name | Precision | Size | Download |
| :--- | :---: | :---: | :---: |
| `qwen3vl_32b_minimax_h3` | ![bf16][badge-bf16] | 47.97 GB | [![][gh-Comfy--Org]](https://huggingface.co/Comfy-Org/MiniMax-H3/resolve/main/text_encoders/qwen3vl_32b_minimax_h3_bf16.safetensors) |
| `qwen3vl_32b_minimax_h3` | ![int8][badge-int8] | 25.28 GB | [![][gh-Comfy--Org]](https://huggingface.co/Comfy-Org/MiniMax-H3/resolve/main/text_encoders/qwen3vl_32b_minimax_h3_int8_convrot.safetensors) |
| `qwen3vl_32b_minimax_h3` | ![nvfp4][badge-nvfp4] | 14.61 GB | [![][gh-Comfy--Org]](https://huggingface.co/Comfy-Org/MiniMax-H3/resolve/main/text_encoders/qwen3vl_32b_minimax_h3_nvfp4_awq.safetensors) |

### ▣ Abiray GGUF Text Encoder

GGUF quantized text encoder, bundled with the [Abiray/MiniMax-H3-GGUF](https://huggingface.co/Abiray/MiniMax-H3-GGUF) repository.

| Model Name | Precision | Size | Download |
| :--- | :---: | :---: | :---: |
| `qwen3vl_32b_minimax_h3` | ![Q4_K_M][badge-Q4_K_M] | 13.58 GB | [![][gh-Abiray]](https://huggingface.co/Abiray/MiniMax-H3-GGUF/resolve/main/text_encoders/qwen3vl_32b_minimax_h3-Q4_K_M.gguf) |
| `qwen3vl_32b_minimax_h3` | ![int4][badge-int4] | 13.93 GB | [![][gh-Abiray]](https://huggingface.co/Abiray/MiniMax-H3-GGUF/resolve/main/text_encoders/qwen3vl_32b_minimax_h3_int4_convrot.safetensors) |
| `qwen3vl_32b_minimax_h3` | ![nvfp4][badge-nvfp4] | 25.28 GB | [![][gh-Abiray]](https://huggingface.co/Abiray/MiniMax-H3-GGUF/resolve/main/text_encoders/qwen3vl_32b_minimax_h3_nvfp4_awq.safetensors) |

### ▣ Full-Precision Pruned Encoder (Felldude)

An FP32 build of the pruned H3 text encoder by [Felldude](https://huggingface.co/Felldude/QWEN_32B_Comfy_MinimaxH3_Pruned_FP32) — one 95.9 GB `model.safetensors`. The author's **QP (Quantization Prediction)** method predicts the trailing 16 Matnitsa bits when going BF16 → FP32, which they report improves 40–50% of blocks while never degrading the rest below the BF16 rounding floor (validated on full-FP32-trained models such as T5). For maximum-fidelity conditioning on a large-VRAM box; most setups are better served by the INT8 / INT4 / GGUF encoders above.

| Model Name | Precision | Size | Download |
| :--- | :---: | :---: | :---: |
| `qwen3vl_32b_minimax_h3` · pruned | ![fp32][badge-fp32] | 95.9 GB | [![][gh-Felldude]](https://huggingface.co/Felldude/QWEN_32B_Comfy_MinimaxH3_Pruned_FP32/resolve/main/model.safetensors) |

<p id="enc-heretic" align="center">· · · · · · · · · · · · · ·</p>

### ▣ Qwen3-VL-32B Ultra-Heretic (Uncensored)

Built from [`llmfan46/Qwen3-VL-32B-Instruct-ultra-uncensored-heretic`](https://huggingface.co/llmfan46/Qwen3-VL-32B-Instruct-ultra-uncensored-heretic) by [ethanfel](https://huggingface.co/ethanfel). Includes a MiniMax-H3 conditioning encoder (language layers 0–49 + vision tower) and an optional prompt-enhancement tail (layers 50–63 + LM head). The "Heretic" lineage bypasses alignment/restriction layers in the text encoder so MiniMax-H3 receives the most faithful prompt embeddings.

| Model Name | Precision | Size | Download |
| :--- | :---: | :---: | :---: |
| `qwen3vl_32b_heretic` (conditioning encoder) | ![int8][badge-int8] | 24.55 GB | [![][gh-ethanfel]](https://huggingface.co/ethanfel/Qwen3-VL-32B-Ultra-Heretic-MiniMax-H3-ComfyUI-INT8-ConvRot/resolve/main/qwen3vl_32b_minimax_h3_ultra_uncensored_heretic_int8_convrot.safetensors) |
| `qwen3vl_32b_heretic` (generation tail 50–63) | ![int8][badge-int8] | 7.09 GB | [![][gh-ethanfel]](https://huggingface.co/ethanfel/Qwen3-VL-32B-Ultra-Heretic-MiniMax-H3-ComfyUI-INT8-ConvRot/resolve/main/qwen3vl_32b_minimax_h3_generation_tail_50_63_int8_convrot.safetensors) |
| `qwen3vl_32b_heretic` · NVFP4 (coolthor, gated) | ![nvfp4][badge-nvfp4] | 14.61 GB | [![][gh-coolthor]](https://huggingface.co/coolthor/MiniMax-H3-pruned-NVFP4/resolve/main/text_encoders/qwen3vl_32b_heretic_minimax_h3_nvfp4.safetensors) |

*The generation tail is loaded temporarily by the [ComfyUI-MiniMax-H3-Guide](https://github.com/ethanfel/ComfyUI-MiniMax-H3-Guide) node for prompt enhancement, then unloaded. Requires the connected standard MiniMax-H3 CLIP (layers 0–49).*

*A **text-encoder-side** LoRA also circulates for prompt writing: [RunningHubAI's `…qwen3vl32b__prompt_generation_overlay__polaris_r16_plus_heretic_v2`](https://huggingface.co/RunningHubAI/rh-minimax-h3-qwen3vl32b-prompt-generation-overlay-polaris-r16-plus-heretic-v2.safetensors-lora) (261 MB, rank 16) overlays a prompt-generation behavior on the Qwen3-VL-32B encoder, built on the Heretic v2 line — load it on the text encoder, not the DiT.*


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

Neural latent-space upscaler for MiniMax H3 video generation by [LBH-123-AI](https://huggingface.co/LBH-123-AI/Minimax_h3_latent_Upscaler). Works directly on H3's 24-channel VAE latents to upscale spatial resolution (H×W) while preserving the time dimension — **accelerates high-res video gen by skipping the costly ~5B-param VAE decode → pixel-upscale → encode round-trip**, and avoids the ghosting / double-image artifacts of naive bilinear/bicubic latent interpolation. 3D-convolution backbone (2D and 3D node variants; one checkpoint serves both, architecture auto-detected). Trained on ~80k paired samples (≈70k video + ≈8k 2K image pairs). Apache-2.0. Pairs with the [ComfyUI_Minimax_h3_latent_Upscaler](https://github.com/LBH-123-AI/ComfyUI_Minimax_h3_latent_Upscaler) node. Current release is **v1** in `minimax_h3_latent_upscaler_3d_conv_v1/`; the filename, not the folder, is what identifies the checkpoint once copied into ComfyUI's flat `models/latent_upscale_models/` directory. ⚠️ Saves **time, not VRAM** — the refine pass still runs at target resolution. [Asirus](https://huggingface.co/Asirus/Minimax-H3-Latent-Upscaler-BF16-MAXQUALITY) also ships a derivative **BF16 Conservative v5** requantization from LBH's FP32 source, keeping 150 tensors in FP16 fallback to avoid the artifacting the author reports from naive BF16 casting.

| Component | Precision | Size | Download |
| :--- | :---: | :---: | :--- |
| Latent Upscaler v1 | ![bf16][badge-bf16] | 691 MB | [![][gh-LBH-123-AI]](https://huggingface.co/LBH-123-AI/Minimax_h3_latent_Upscaler/resolve/main/minimax_h3_latent_upscaler_3d_conv_v1/minimax_h3_latent_upscaler_3d_conv_v1_bf16.safetensors) |
| Latent Upscaler v1 | ![fp16][badge-fp16] | 691 MB | [![][gh-LBH-123-AI]](https://huggingface.co/LBH-123-AI/Minimax_h3_latent_Upscaler/resolve/main/minimax_h3_latent_upscaler_3d_conv_v1/minimax_h3_latent_upscaler_3d_conv_v1_fp16.safetensors) |
| Latent Upscaler v1 | ![fp32][badge-fp32] | 1.38 GB | [![][gh-LBH-123-AI]](https://huggingface.co/LBH-123-AI/Minimax_h3_latent_Upscaler/resolve/main/minimax_h3_latent_upscaler_3d_conv_v1/minimax_h3_latent_upscaler_3d_conv_v1_fp32.pth) |
| BF16 Conservative v5 | ![bf16][badge-bf16] | 691 MB | [![][gh-Asirus]](https://huggingface.co/Asirus/Minimax-H3-Latent-Upscaler-BF16-MAXQUALITY/resolve/main/minimax_h3_bf16_CONSERVATIVE_v5.safetensors) |

<p id="controlnet" align="center">· · · · · · · · · · · · · ·</p>

### ▣ Fun-ControlNet Union 2.0 (alibaba-pai)

Control branch for MiniMax-H3 from Alibaba PAI's [VideoX-Fun](https://github.com/aigc-apps/VideoX-Fun) line, by [alibaba-pai](https://huggingface.co/alibaba-pai/MiniMax-H3-Fun-Controlnet-Union-2.0). Loaded **on top of** the base H3 transformer — the checkpoint holds only the control branch (`control_proj_in` + 10 control blocks, ≈13.5 GB) and is not a standalone model.

**What 2.0 changes vs v1:** 8 control conditions instead of 5 (adds **Scribble, Layout, Gray** to Canny / Depth / HED / MLSD / Pose), a denser injection schedule (10 control blocks at layers `0, 5, 10, …, 45` instead of 5 at `0, 10, 20, 30, 40`), and a `post_norm` inpaint recipe (holes at mid-gray, following Wan 2.1) instead of `pre_norm`. `control_in_dim = 49` (latent + masked latent + mask) so the same branch does both control and inpainting; `control_apply_audio = false`; guidance-distilled (`guidance_scale = 1.0`).

> ⚠️ **A v1 config against this checkpoint fails silently.** With the old `minimax_h3_control.yaml` (5 blocks) only half the branch is built and `load_state_dict(strict=False)` drops `control_blocks.5~9` as unexpected keys — outputs are wrong with no error. Always use `minimax_h3_control_inpaint_post_norm.yaml`.

| Component | Precision | Size | Download |
| :--- | :---: | :---: | :--- |
| ControlNet-Union-2.0 branch | ![fp32][badge-fp32] | 12.6 GB | [![][gh-alibaba-pai]](https://huggingface.co/alibaba-pai/MiniMax-H3-Fun-Controlnet-Union-2.0/resolve/main/MiniMax-H3-Fun-Controlnet-Union-2.0.safetensors) |

*MiniMax H3 Community License Agreement; 8 control conditions plus video inpainting, one checkpoint. V2V control workflows (openpose/canny/depth) in javawock7618's INT8 pack wire this branch in.*

<p id="lora" align="center">◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆</p>

## ▓ LoRA

LoRA adapters for MiniMax-H3, organized by type. Version, rank, and trigger words live in the description. Entries carrying a red **NSFW** badge contain explicit content — browse at your own discretion.

### ▣ All LoRAs

| Name | Type | Description | Size | Download |
| :--- | :---: | :--- | :---: | :---: |
| Homelander | ![Character][ltype-character] | The Boys' Homelander; trigger `HeroHomelander` (optionally append `wearing red leather gloves`). Experimental. | 296 MB | [![][gh-ssjenforcer191]](https://huggingface.co/ssjenforcer191/Homelander_Minimax_H3_experimental) |
| Mila Kunis | ![Character][ltype-character] | Playtime-AI celebrity series (v1.70); sample clip included. | 155 MB | [![][gh-Playtime--AI]](https://huggingface.co/Playtime-AI/Minimax_H3-Mila_Kunis) |
| Sydney Sweeney | ![Character][ltype-character] | Playtime-AI series; sample clip included. | 155 MB | [![][gh-Playtime--AI]](https://huggingface.co/Playtime-AI/Minimax_H3-Sydney_Sweeney) |
| Salma Hayek | ![Character][ltype-character] | Playtime-AI series; sample clip included. | 155 MB | [![][gh-Playtime--AI]](https://huggingface.co/Playtime-AI/Minimax_H3-Salma_Hayek) |
| Jennifer Connelly | ![Character][ltype-character] | Playtime-AI series; sample clip included. | 155 MB | [![][gh-Playtime--AI]](https://huggingface.co/Playtime-AI/Minimax_H3-Jennifer_Connelly) |
| Margot Robbie | ![Character][ltype-character] | Playtime-AI series; sample clip included. | 155 MB | [![][gh-Playtime--AI]](https://huggingface.co/Playtime-AI/Minimax_H3-Margot_Robbie) |
| Zendaya | ![Character][ltype-character] | Playtime-AI series; sample clip included. | 155 MB | [![][gh-Playtime--AI]](https://huggingface.co/Playtime-AI/Minimax_H3-Zendaya) |
| Dolly Parton | ![Character][ltype-character] | Playtime-AI series (v1.1); sample clip included. | 155 MB | [![][gh-Playtime--AI]](https://huggingface.co/Playtime-AI/Minimax_H3-Dolly_Parton) |
| Sadie Sink | ![Character][ltype-character] | Playtime-AI series; sample clip included. | 155 MB | [![][gh-Playtime--AI]](https://huggingface.co/Playtime-AI/Minimax_H3-Sadie_S) |
| Anya Taylor-Joy | ![Character][ltype-character] | Playtime-AI series; sample clip included. | 155 MB | [![][gh-Playtime--AI]](https://huggingface.co/Playtime-AI/Minimax_H3-Anya_Taylor_Joy) |
| Megan Fox | ![Character][ltype-character] | Playtime-AI series (v1.1); sample clip included. | 155 MB | [![][gh-Playtime--AI]](https://huggingface.co/Playtime-AI/Minimax_H3-Megan_Fox) |
| Ariana Grande | ![Character][ltype-character] | Playtime-AI series; sample clip included. | 155 MB | [![][gh-Playtime--AI]](https://huggingface.co/Playtime-AI/Minimax_H3-Ariana_Grande) |
| Kiernan Shipka | ![Character][ltype-character] | Playtime-AI series; sample clip included. | 155 MB | [![][gh-Playtime--AI]](https://huggingface.co/Playtime-AI/Minimax_H3-Kiernan_Shipka) |
| Millie Bobby Brown | ![Character][ltype-character] | Playtime-AI series; sample clip included. | 155 MB | [![][gh-Playtime--AI]](https://huggingface.co/Playtime-AI/Minimax_H3-Millie_Bobby_Brown) |
| Milly Alcock | ![Character][ltype-character] | Playtime-AI series; sample clip included. | 155 MB | [![][gh-Playtime--AI]](https://huggingface.co/Playtime-AI/Minimax_H3-Milly_Alcock) |
| The Dude | ![Character][ltype-character] | Jeff Bridges as "The Dude" (The Big Lebowski); Playtime-AI series; sample clip included. | 155 MB | [![][gh-Playtime--AI]](https://huggingface.co/Playtime-AI/Minimax_H3-The_Dude-Jeff_Bridges) |
| Ricky Gervais | ![Character][ltype-character] | Playtime-AI series; sample clip included. | 148 MB | [![][gh-Playtime--AI]](https://huggingface.co/Playtime-AI/Minimax_H3-Ricky_Gervais) |
| Sasha Grey | ![Character][ltype-character] | Playtime-AI series; sample clip included. | 148 MB | [![][gh-Playtime--AI]](https://huggingface.co/Playtime-AI/Minimax_H3-Sasha_Grey) |
| Betty Gilpin | ![Character][ltype-character] | Playtime-AI series; sample clip included. | 148 MB | [![][gh-Playtime--AI]](https://huggingface.co/Playtime-AI/Minimax_H3-Betty_Gilpin) |
| Alan Rickman | ![Character][ltype-character] | Playtime-AI series (v1.1); sample clip included. | 148 MB | [![][gh-Playtime--AI]](https://huggingface.co/Playtime-AI/Minimax_H3-Alan_Rickman) |
| Mia Goth | ![Character][ltype-character] | Playtime-AI series; sample clip included. | 148 MB | [![][gh-Playtime--AI]](https://huggingface.co/Playtime-AI/Minimax_H3-Mia_Goth) |
| Ace Ventura | ![Character][ltype-character] | Jim Carrey's Ace Ventura; Playtime-AI series; sample clip included. | 148 MB | [![][gh-Playtime--AI]](https://huggingface.co/Playtime-AI/Minimax_H3-Ace_Ventura) |
| PinkFluffyBunny | ![Style][ltype-style] | Whimsical pink-bunny style; pruned + unpruned builds across rank 128/256/512 — maximum pink at 0.5 strength on the pruned int8 model. Alpha quality. | 2.31 GB | [![][gh-SexGod1979]](https://huggingface.co/SexGod1979/PinkFluffyBunny-MiniMax-H3) |
| PinkCherry | ![Style][ltype-style] | Furry rabbits, rainbows, cherry blossoms — ships as **merged full checkpoints** with the style baked in (alpha 0.1→0.5 iterates, beta 0.6, v1 final; bf16 / fp16 / int8 / pruned-int8). No guardrails altered. | 19.53–61.7 GB | [![][gh-SexGod1979]](https://huggingface.co/SexGod1979/PinkCherry_MiniMax-H3) |
| NaughtyTimes | ![Style][ltype-style] ![NSFW][ltype-nsfw] | NSFW style for FL2VA; v3 (rank 64), trained on the unpruned base with a 50/50 T2V/I2V mix — prefer the unpruned build on int8/bf16 unpruned bases (the pruned variant drops the trained AdaLN projections and is noticeably weaker). | 568 MB · 1.15 GB | [![][gh-SexGod1979]](https://huggingface.co/SexGod1979/NaughtyTimes_MiniMax-H3) |
| AfterMidnight | ![Style][ltype-style] ![NSFW][ltype-nsfw] | Ref2VA NSFW family (rank 64) — `sexytime` v1–v1.2 and `softer` v1; mirrored byte-identical at [sasimi](https://huggingface.co/sasimi/AfterMidnight-MiniMax-H3-NSFW). | 1.11 GB | [![][gh-SexGod1979]](https://huggingface.co/SexGod1979/AfterMidnight-MiniMax-H3-NSFW) |
| B / Spicy / V | ![Style][ltype-style] | Three unnamed style LoRAs; no README — use at own discretion. | 310 MB each | [![][gh-DIE2025]](https://huggingface.co/DIE2025/MiniMaxH3Loras) |
| vh5tape | ![Style][ltype-style] | VHS / analog 1980s retro look; ships sample clips and a `-comfyui` variant. | 131 MB | [![][gh-KennethFal]](https://huggingface.co/KennethFal/vh5tape-vhs-lora-minimax-h3) |
| 16Bit Pixel | ![Style][ltype-style] | SNES-era 16-bit pixel-animation style — large square pixel clusters, staircase outlines, limited palette, flat two-tone shading, and held-sprite motion. The author presents the fal.ai endpoint as the supported usage path, but the raw 5k-step LoRA weights are shipped here too. | 125 MB | [![][gh-KennethFal]](https://huggingface.co/KennethFal/16bit-pixel-lora-minimax-h3) |
| 1980s Horror Movies | ![Style][ltype-style] | VHS-era 1980s horror-film look; trigger `80s_horror`. A Civitai mirror (author's original page linked in the card); no training details published. | 296 MB | [![][gh-neph1]](https://huggingface.co/neph1/1980s_horror_movies_minimax_h3) |
| 1950s Sci-Fi | ![Style][ltype-style] | 1950s sci-fi / retro B-movie look; Civitai mirror with no trigger word or training details documented. | 296 MB | [![][gh-neph1]](https://huggingface.co/neph1/1950sScifiMinimaxH3) |
| Rough 2D Cartoon Illustration | ![Style][ltype-style] | Experimental rough 2D cartoon illustration — free-flow motion, hand-drawn line quality. Trigger `rough 2D cartoon illustration`; rank 16, 1200 steps at 480×832 (two shipped checkpoints, 1000 and 1200, both recommended); trained on Pexels video. Author warns it may produce artifacts. | 71 MB each | [![][gh-prithivMLmods]](https://huggingface.co/prithivMLmods/MiniMax-H3-Rough-2D-Cartoon-Illustration) |
| Anime 2 Realism | ![Style][ltype-style] | Ref2VA anime-to-live-action conversion: regenerates an anime reference in a photorealistic style while preserving subjects, pose, composition, clothing and palette. Trigger `LumiReal`; the card ships three prompt presets — plain photorealistic live-action, polished high-end cosplay photography, and premium cinematic casting. | 296 MB | [![][gh-LiseTY]](https://huggingface.co/LiseTY/Minimax-H3-ref2v_Anime_2_Realism) |
| Facial Realism CloseUp | ![Style][ltype-style] | Face realism for close-up portraits (cp2000). | 75 MB | [![][gh-prithivMLmods]](https://huggingface.co/prithivMLmods/MiniMax-H3-Facial-Realism-CloseUp) |
| Realism People | ![Style][ltype-style] | Natural-looking people in everyday scenarios; trained on diverse photo data. | 125 MB | [![][gh-fal]](https://huggingface.co/fal/research-mini-max-h3-realism-people-lora) |
| Cinematic Realism | ![Style][ltype-style] | Grounded photographic "真实电影质感" look (V0.1); ships a Chinese prompt-preset JSON. No model card. | 309 MB | [![][gh-orangesouth]](https://huggingface.co/orangesouth/MinimaxH3CinematicRealism) |
| Looping Sketch Anime | ![Style][ltype-style] | Hand-drawn 2D outlines, flat colors, white outline; strength 0.75–1.25 — pair with a Turbo LoRA for higher strength. | 569 MB | [![][gh-Inner--Reflections]](https://huggingface.co/Inner-Reflections/MiniMax-H3-Looping-Sketch-Anime) |
| STUDIO 1939 | ![Style][ltype-style] | Golden-age hand-painted animation (gouache backgrounds, celluloid palettes); two flavors — `light` r16 painterly / `strong` r64 full cel. Trigger `gulliv3r,` at prompt start; scale 1.0 for the full look, 0.4–0.8 blended; 21:9 / 16:9 / 4:3. | 65.6 MB · 262 MB | [![][gh-suryatmodulus]](https://huggingface.co/suryatmodulus/studio-1939-old-animation-lora-minimax-h3) |
| Insta / TikTok Aesthetics | ![Style][ltype-style] | Polished social-media look — skin smoothing, vibrant grade, trendy framing. | 310 MB | [![][gh-vpakarinen]](https://huggingface.co/vpakarinen/insta-tiktok-aesthetics-h3-lora) |
| Singularity (extract) | ![Style][ltype-style] | Spectral-dampened extraction of WarmBloodAban's [Singularity](https://huggingface.co/WarmBloodAban/Minimax-h3_Singularity) hybrid-pruned checkpoint; intense — use ≤0.5 strength (may carry ref/fl signatures that drift higher). Unofficial; TenStrip defers to an official release. | 625 MB · 1.19 GB | [![][gh-TenStrip]](https://huggingface.co/TenStrip/Minimax-h3_Singularity-Lora) |
| Combat Base V2 | ![Motion][ltype-motion] | Combat, action, and dialogue motion base; ships 2 workflow JSONs. | 155 MB | [![][gh-JOKER141]](https://huggingface.co/JOKER141/MiniMax-H3-Combat-Base-V2) |
| Motion Continuity Repair | ![Motion][ltype-motion] | Repairs sub-second "dropped-chain" moments — sudden slow-mo, missing transitions, broken interactions — instead of amplifying everything. Optional trigger `bunny_crisp_motion`; ≈0.9 standalone, 0.5–0.7 paired with Combat, 0.2–0.3 on the stage-2 refine. | 155 MB | [![][gh-JOKER141]](https://huggingface.co/JOKER141/MiniMax-H3-General-Motion-Continuity-Repair) |
| Weapon Combat | ![Motion][ltype-motion] | Weapon-trajectory continuity, attack/defense interaction, and spatial combat (mounted, group). Trigger `BUNNY 🐇`; demo clips + RunningHub workflows. | 148 MB | [![][gh-JOKER141]](https://huggingface.co/JOKER141/MiniMax-H3-Weapon-Combat-LoRA) |
| GunFu | ![Motion][ltype-motion] | Cinematic gunfights and close-quarters gun-fu — ranged firefights through John Wick–style contact, throws, and physical struggle in one continuous sequence. Trigger `BUNNY 🐇`, start at 0.9; pairs with `Combat Base V2` (0.5) + `Motion Continuity Repair` (0.3) for melee gun-fu. Trained independently (BASE not included). Ships two prompt-writing skill ZIPs + a one-click workflow with the author's Conditioning Bridge node. | 148 MB | [![][gh-JOKER141]](https://huggingface.co/JOKER141/MiniMaxH3-GunFu-Gunfight-LORA) |
| Wushu Action | ![Motion][ltype-motion] | Human martial-arts motion (punches, kicks, spins, staff); no fixed trigger — describe the action. Rank 16, 2000 steps; load `_pruned` at 0.8–1.0; Turbo-compatible. | 155 MB · 310 MB | [![][gh-Jojocodex]](https://huggingface.co/Jojocodex/minimax-h3-wushu-action-lora) |
| Wushu Action v7 | ![Motion][ltype-motion] | Current **E3** build on the unpruned INT8-ConvRot DiT + bf16 Qwen3-VL TE (924 fight clips, 832×480); 1000/2000-step checkpoints. Trigger `wushu_action`; pairs with Combat Base V2 / Motion Continuity Repair; ~25 steps on the int8 base (low counts render soft). Ships a multi-reference dual-dispatch fight workflow, a full move/tag list, a prompt-writing skill sheet, and a fight **simulator** (Windows `.exe` + guide) that plays out a bout and emits the prompt for H3. | 569 MB | [![][gh-Jojocodex]](https://huggingface.co/Jojocodex/wushu-action-v7-minimax-h3-fl2va-ref2va-lora) |
| Wushu Action v8 | ![Motion][ltype-motion] | Different beast from v7: learns **human movement and force-transfer logic only** — not look, character, or texture — trained on untextured three-view mannequin animation, so white-mannequin/black-void output is by design. Trigger `wushu_action` must lead the prompt; strength 0.6–0.8 for real scenes (0.9–1.0 for mannequin reference sheets, 0.5–0.6 if the mannequin leaks through). euler/simple, 25 steps, CFG 1.0, 17n+5 frames, 832×480. Limits: 1.3–3 s clips, single person — two-person sparring is extrapolation. | 569 MB | [![][gh-Jojocodex]](https://huggingface.co/Jojocodex/wushu-action-v7-minimax-h3-fl2va-ref2va-lora) |
| Better Human Motion | ![Motion][ltype-motion] | Natural, consistent human movement (gait, gesture, weight shift); trained at 720×1280 — strength 0.4–0.8, 15–30 steps. | 296 MB | [![][gh-vpakarinen]](https://huggingface.co/vpakarinen/better-human-motion-h3-lora) |
| Motion Enhancer (8-step) | ![Motion][ltype-motion] ![NSFW][ltype-nsfw] | Anatomy / motion enhancer on LightX2V's 8-step distilled FL2VA — amplifies motion intensity and anatomical detail at low step counts. | 1.96 GB | [![][gh-rzgar]](https://huggingface.co/rzgar/minimax-h3_fl2v_8Step_motion_enhancer) |
| Motion Adapter | ![Motion][ltype-motion] | Rank-16 LoRA that makes the de-rope pass in [ComfyUI-MAINodes](https://github.com/matlowai/ComfyUI-MAINodes) behave better on fast motion (removes the advance/snap alternation of the stretched clock); it needs that pass and is not a general-purpose motion LoRA. Two families: the **pilot r16** (`motion_adapter_pilot_r16`, trained on H3-generated holdout-infill items) and the newer **temporal-expansion ladder** (`temporal_expansion/…`, 17 rank-16 checkpoints — `warm100` plus steps 025→375 — retrained against real GOPRO_Large intermediate frames; measured held-token error falls monotonically 0.158 @25 → 0.086 @375, though the author picks step 100 on playback). Apply to the de-rope pass only (not the first pass), stock `LoraLoaderModelOnly`, strength 1.0 for smoothness / 0.75 for fewer invented objects; inject 0.45 (character/dialogue) or 0.30 (identity/props). | 63 MB each | [![][gh-MATLOWAI]](https://huggingface.co/MATLOWAI/MiniMax-H3-Motion-Adapter) |
| Spatial Physics | ![Physics][ltype-physics] | Object physics — collision, stacking, falling, occlusion — via pure spatial+physics captions (CLEVRER / WISA / PhyCo-Kubric, 700 clips); rank 16; complements the wushu LoRA; stacks with Turbo. | 155 MB · 310 MB | [![][gh-Jojocodex]](https://huggingface.co/Jojocodex/minimax-h3-spatial-physics-lora) |
| Yunjing | ![Camera][ltype-camera] | Cinematic camera movement (push in/out, orbit, tracking, handheld) — 12 trained movements; trigger `yunjing`. Rank 32, 1000 steps; stacks with Turbo. | 310 MB · 620 MB | [![][gh-Jojocodex]](https://huggingface.co/Jojocodex/minimax-h3-yunjing-lora) |
| Camera Motion | ![Camera][ltype-camera] | Broader dedicated camera-motion training (v1, 1000 steps), separate from `Yunjing` — use one or the other per shot; ships a ready-made motion-prompt library. | 155 MB | [![][gh-Jojocodex]](https://huggingface.co/Jojocodex/minimax-h3-Camera-Motion-lora) |
| Third Person View | ![Camera][ltype-camera] | Game-CG / HUD / viewpoint-control LoRA for over-the-shoulder tracking, third-person follow shots, first-person POV transitions, and game UI overlays (reticles, QTE prompts, boss health bars). Fine-tuned on the INT8 reference architecture; no separate trigger phrase documented beyond the concept itself. | 592 MB | [![][gh-WarmBloodAban]](https://huggingface.co/WarmBloodAban/Minimax_H3_LoRAs) |
| CrossView Warp v1 | ![Camera][ltype-camera] | Novel-view synthesis for **Ref2VA**: give it a clip plus a camera offset (azimuth/elevation) and it re-renders the same scene from that viewpoint. Reads two inputs — a depth-warp of the clip (geometry, from the [CrossViewWarp](https://github.com/cseti007/ComfyUI-CrossViewWarp) node + MoGe) and the clip itself (identity/appearance) — wired as an Add Guide at `frame_idx = 0`. Trigger `crossview`, strength 0.8 recommended (0.8–1.0); resize warp and source to matching dimensions first. | 569 MB | [![][gh-Cseti]](https://huggingface.co/Cseti/MiniMax-H3_Ref2VA-LoRA-CrossView-Warp_v1) |
| Turnaround | ![Utility][ltype-utility] | Contact-sheet diffusion — one reference + one instruction → five progressively rotated views of the subject in a single pass (H3's timeline as a slot axis). | 60 MB | [![][gh-matlod]](https://huggingface.co/matlod/minimax-h3-turnaround) |
| Five View | ![Utility][ltype-utility] | Multi-angle character sheet: generates five views of a subject in one pass, trained at 512 resolution / 1500 steps. RunningHub-hosted upload (weights also runnable locally); no trigger or rank documented. | 60 MB | [![][gh-RunningHubAI]](https://huggingface.co/RunningHubAI/rh-minimax-h3-five-view-512-s1500.safetensors-lora) |
| Equi360 | ![Utility][ltype-utility] | Full-sphere monoscopic equirectangular 360° video with native audio; trigger `equirect360`. Reviewed-v2 default (57 clips / 36 sources / 16 scene families); fal-trained, full scripts in the repo. | 125 MB | [![][gh-shamanic]](https://huggingface.co/shamanic/minimax-h3-equi360-lora) |
| Lineart Anime | ![Utility][ltype-utility] | Anime line-art video → fully colored anime output (Ref2VA video-reference workflow). | 1.26 GB | [![][gh-DiffSynth-Studio]](https://huggingface.co/DiffSynth-Studio/MiniMax-H3-LoRA-LineartAnime) |
| LMS | ![Utility][ltype-utility] | "A little more sharpness" — V2V guide-latent sharpener: the source clip is fed as an **aligned latent guide** (native `MiniMaxH3AddGuide`, frame 0, same resolution, valid 17k+5 frame counts) instead of a reference block, so the guide-to-target correspondence is handed to the model positionally. Rank 64, trained on Ref2VA (FL2VA less tested); trigger caption in the card; ships a ready ComfyUI workflow. | 1.15 GB | [![][gh-Alissonerdx]](https://huggingface.co/Alissonerdx/Minimax-H3-ComfyUI) |
| H3-World | ![Utility][ltype-utility] | Interactive world model — keyboard controls → language instructions → directed-attention routing; requires a directed-attention patch (unmodified pipeline won't reproduce). Rank 32 (65.6M params). | 131 MB | [![][gh-DANNY621]](https://huggingface.co/DANNY621/H3-World) |
| FaceSwap REF2VA | ![Utility][ltype-utility] | Identity face-swap for Ref2VA: takes the driving video's face and replaces it with the identity from the supplied reference image(s). Single trigger `Faceswap`, strength 1.0; AdaLN pruned below a fixed fro threshold (smaller, fewer LoRA artifacts, strength matched to the trained base). Ships a [CRT-Nodes](https://huggingface.co/UntMods/FaceSwap_MiniMaxH3_REF2VA/tree/main) ComfyUI workflow (input video must follow the H3 format). Apache-2.0. | 63 MB | [![][gh-UntMods]](https://huggingface.co/UntMods/FaceSwap_MiniMaxH3_REF2VA) |
| AnyFlow WIP | ![Research][ltype-research] | SimpleTuner WIP checkpoints (steps 200–500 + EMA); not production-tuned. Repo now gated. | — | [![][gh-bghira]](https://huggingface.co/bghira/minimax-h3-anyflow-wip) |
| Pruned Ref2VA Delta | ![Research][ltype-research] | Randomized-SVD approximations of the pruned FL2VA↔Ref2VA weight difference — both directions, ranks 256/512/1024 (BF16); mechanically extracted, not generation-tested. | 2.41–9.36 GB | [![][gh-ethanfel]](https://huggingface.co/ethanfel/MiniMax-H3-Pruned-Ref2VA-Delta-LoRAs-Experimental) |
| FL2VA↔Ref2VA Delta | ![Research][ltype-research] | Rank-256 BF16 capture of the FL2VA↔Ref2VA difference (same class as ethanfel's); no confirmed use case yet. | 2.40 GB | [![][gh-Kijai]](https://huggingface.co/Kijai/MiniMax-H3-experimental/tree/main/loras) |
| NTT | ![Research][ltype-research] | "NTT" v2 in ranks 128/256/512; no model card — purpose and triggers undocumented, use at own discretion. | 1.12–4.48 GB | [![][gh-adehong]](https://huggingface.co/adehong/minimax-h3-ntt-lora) |
| CWM System-Chat | ![Research][ltype-research] | Five research adapters from 1344×768 q4 System-Chat runs on Ref2VA — 600 LoRA tensors / 200 target modules each; inference + LoRA warm-start (no optimizer-level resume). | 2.39 GB each | [![][gh-NTU-yiwen]](https://huggingface.co/NTU-yiwen/awm-minimax-h3-new1344-lora-checkpoints) |
| ai-toolkit Training Adapters | ![Research][ltype-research] | Seven undocumented **distillation** adapters (no model card, 0 downloads) from ostris's [ai-toolkit](https://github.com/ostris/ai-toolkit) H3 training work. Safetensors headers name them `minimax_h3_distillation_adapter{,3}` and `minimax_h3_ref2va_distilation_adapter{,3}` (bases `minimax_h3` / `minimax_h3_ref2va`, 22–1750 steps) plus `fasth3_v2_training_adapter` on a `minimax_h3_vsa` (FastH3 8-step V2) base at step 500 — all 416–516 `lora_A/lora_B` tensors. Trainer/validation artifacts rather than finished releases; see the author's [jacked Ref2VA LoRA](https://huggingface.co/ostris/minimax_h3_ref2va_jacked_lora) for a documented example from the same series. | 148–334 MB | [![][gh-ostris]](https://huggingface.co/ostris/minimax_h3_training_adapter) |
| RAVEN Streaming | ![Research][ltype-research] | Real-time autoregressive video extrapolation — turns H3 into a causal streaming generator (4-NFE preview; each chunk extrapolated from prior content). r=128; academic preview, undertrained texture. | ≈5.1 GB | [![][gh-mvp--lab]](https://huggingface.co/mvp-lab/MiniMax-H3-RAVEN-Streaming-LoRA) |

### ▣ Collections

Multi-LoRA repositories — browsing pointers, not enumerated per-file here. All listed collections are tagged NSFW.

| Collection | Contents | Download |
| :--- | :--- | :---: |
| Actions | ⚠️ **Explicit / NSFW.** Action / motion LoRAs with trigger words and strength recommendations. | [![][gh-EllaPriest45]](https://huggingface.co/EllaPriest45/MinimaxH3_Actions/tree/main) |
| Characters | ⚠️ **Explicit / NSFW.** Character packs (Aunt Cass, Baldur's Gate 3 Party Pack, Judy Hopps, …). | [![][gh-EllaPriest45]](https://huggingface.co/EllaPriest45/MinimaxH3_Characters/tree/main) |
| Styles | ⚠️ **Explicit / NSFW.** Style LoRAs (anime, digicam, Playboy, …); significant nude portion. | [![][gh-EllaPriest45]](https://huggingface.co/EllaPriest45/MinimaxH3_Styles/tree/main) |
| MiniMax-H3 LoRAs | ⚠️ **Explicit / NSFW.** Mixed collection; repo tagged NSFW. | [![][gh-Hearmeman]](https://huggingface.co/Hearmeman/minimax-h3-loras/tree/main) |
| Curated LoRAs | ⚠️ **Explicit / NSFW.** Curated styles + characters. | [![][gh-nikdevs]](https://huggingface.co/nikdevs/minimax-h3-loras) |
<p id="nodes" align="center">◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆</p>

## ▓ ComfyUI Nodes

| Node | Author | Category | Description |
| :--- | :--- | :---: | :--- |
| [MiniMax H3 Hybrid Cond](https://github.com/kitsune123150/minimax-h3-hybrid-cond) | kitsune123150 | ![Conditioning][cat-cond] | Hybrid R2V + I2V conditioning in one payload, AV latent with native audio. |
| [H3-Multishot](https://github.com/jlucasmcrell/ComfyUI-H3-Multishot) | jlucasmcrell | ![Conditioning][cat-cond] | N chained shots from one script, seam-clean master; keyframes anywhere. |
| [H3-Multishot-Advance](https://github.com/KursatAs/ComfyUI-H3-Multishot-Advance) | KursatAs | ![Conditioning][cat-cond] | Multishot fork with a persistent shot cache that survives restarts. |
| [MiniMax H3 Director](https://github.com/seesee75-commits/ComfyUI-MiniMaxH3-Director) | seesee75-commits | ![Conditioning][cat-cond] | Storyboard timeline: drag media on tracks, trim, prompt per shot, chain takes. |
| [DNNodes](https://github.com/ljxdn/ComfyUI-DNNodes) | ljxdn | ![Conditioning][cat-cond] | Asset cards to Director groups, and back; reference numbering preserved. |
| [MiniMax H3 Image Studio](https://github.com/astropuzzo/ComfyUI-MiniMax-H3-Image-Studio) | astropuzzo | ![Conditioning][cat-cond] | Image-first H3: T2I, I2I, reference editing, resolution up to 64 MP. |
| [MiniMaxH3-Easy](https://github.com/nkxx188/ComfyUI-MiniMaxH3-Easy) | nkxx188 | ![Conditioning][cat-cond] | One node for T2V, I2V, first/last-frame and reference video. |
| [AICG3D](https://github.com/JGRFW/comfyui-AICG3D) | JGRFW | ![Conditioning][cat-cond] | H3 workbench: media library, LoRA slots, prompt templates, AICG sampler. |
| [H3 Motion Context](https://github.com/NikoDemon80/ComfyUI-H3-Motion-Context) | NikoDemon80 | ![Conditioning][cat-cond] | Chain clips so motion and audio carry across the cut. |
| [H3-Motion-Context-MultiRef](https://github.com/seitanism/ComfyUI-H3-Motion-Context-MultiRef) | seitanism | ![Conditioning][cat-cond] | Motion Context plus MultiRef, latent masking, V2V motion transfer, chaining. |
| [MiniMax H3 Motion Director](https://github.com/j955229/ComfyUI-MiniMax-H3-Motion-Director) | j955229 | ![Conditioning][cat-cond] | Multi-segment director: AIMixer timeline plus Motion Context chaining. |
| [H3 Conditioning Cache](https://github.com/HEEEeeeeN/ComfyUI-H3-Conditioning-Cache) | HEEEeeeeN | ![Conditioning][cat-cond] | Caches conditioning across shots and batch-generates episodes. |
| [MAINodes](https://github.com/matlowai/ComfyUI-MAINodes) | matlowai | ![Conditioning][cat-cond] | Contact-sheet diffusion (five views) plus a Motion Lab de-rope pass. |
| [Fantastic MiniMax H3 Prompt Builder](https://github.com/Adudeguyman/ComfyUI-Fantastic-MiniMaxH3-PromptBuilder) | Adudeguyman | ![Prompt][cat-prompt] | Fillable prompt templates per H3 mode with live rule checking. |
| [MiniMax-H3 Prompt Enhancer T8](https://github.com/T8mars/comfyui-minimax-h3-prompt-enhancer-T8) | T8mars | ![Prompt][cat-prompt] | Multimodal prompt enhancer (text, image, video) for every H3 mode. |
| [MiniMaxH3 LatentUpscaler](https://github.com/Tr1dae/ComfyUI-MiniMaxH3_LatentUpscaler) | Tr1dae | ![Upscaling][cat-upscale] | Two-pass latent spatial upscaling with re-noised video and audio. |
| [Video Tiler](https://github.com/maDcaDDie2000/comfyui-video-tiler) | maDcaDDie2000 | ![Upscaling][cat-upscale] | Tiled video/image upscaling with overlap and feather blending, disk-backed. |
| [H3 Latent Upscaler (Mamad8)](https://github.com/mamad8c/ComfyUI-H3-Latent-Upscaler-Mamad8) | mamad8c | ![Upscaling][cat-upscale] | Fast move of a clean H3 latent onto a 2x larger spatial grid. |
| [MiniMaxH3 Frame Infill](https://github.com/red-polo/ComfyUI-MiniMaxH3FrameInfill) | red-polo | ![Conditioning][cat-cond] | Regenerate any frame range of an existing H3 video. |
| [SolAttn_triton](https://github.com/kijai/ComfyUI-SolAttn_triton) | kijai | ![Acceleration][cat-accel] | Triton SolAttention kernel for ComfyUI. |
| [sol-attn](https://github.com/Saganaki22/ComfyUI-sol-attn) | Saganaki22 | ![Acceleration][cat-accel] | Zero-copy Sol-Attn with scheduled tau and feed-forward chunking. |
| [VDN-H3](https://github.com/Saganaki22/ComfyUI-VDN-H3) | Saganaki22 | ![Acceleration][cat-accel] | Video DeltaNet as runtime patches; cost scales linearly with clip length. |
| [Viggle-Animate-H3](https://github.com/Saganaki22/ComfyUI-Viggle-Animate-H3) | Saganaki22 | ![Conditioning][cat-cond] | Nodes for the Viggle-Animate ref2va finetune (character replacement). |
| [Spectrum MiniMax H3](https://github.com/xmarre/ComfyUI-Spectrum-MiniMax-H3) | xmarre | ![Acceleration][cat-accel] | Spectral forecasting skips selected transformer evaluations. |
| [MiniMax-H3-RefDelta-Solver](https://github.com/xmarre/ComfyUI-MiniMax-H3-RefDelta-Solver) | xmarre | ![Acceleration][cat-accel] | ER-SDE-derived sampler and scheduler for the fused r1024 checkpoint. |
| [Herrgotts-H3-Infinite-Continuation-Suite](https://github.com/HerrgottMargott/Herrgotts-H3-Infinite-Continuation-Suite) | HerrgottMargott | ![Conditioning][cat-cond] | Video continuation across segments with crossfade and audio de-click. |
| [MiniMaxH3-Cache](https://github.com/lihaoyun6/ComfyUI-MiniMaxH3-Cache) | lihaoyun6 | ![Acceleration][cat-accel] | EasyCache-style transformer block cache reused across timesteps. |
| [H3VAE_TRT](https://github.com/lihaoyun6/ComfyUI-H3VAE_TRT) | lihaoyun6 | ![Acceleration][cat-accel] | Compile the H3 ONNX VAE to TensorRT for faster encode/decode. |
| [MiniMax H3 Block Cache T8](https://github.com/T8mars/comfyui-minimax-h3-blockcache-T8) | T8mars | ![Acceleration][cat-accel] | F1B0 block cache skips up to 49 of 50 blocks per step. |
| [TE-Speed-MiniMaxH3-OSS](https://github.com/HELPMEEADICE/TE-Speed-MiniMaxH3-OSS) | HELPMEEADICE | ![Acceleration][cat-accel] | Block-cache accelerator for the H3 DiT loop, about 45% faster. |
| [MiniMaxH3 Dual-Clock Euler Sampler](https://github.com/shuaixn/ComfyUI-MiniMaxH3DualClockSampler) | shuaixn | ![Acceleration][cat-accel] | Separate video and audio schedules fix Turbo audio crackle at 4 steps. |
| [H3-AudioRefine](https://github.com/Adudeguyman/ComfyUI-H3-AudioRefine) | Adudeguyman | ![Acceleration][cat-accel] | Audio-only refinement pass over a frozen video latent. |
| [MiniMax-H3-PDD-Acc](https://github.com/Jalen-Brunson/ComfyUI-MiniMax-H3-PDD-Acc) | Jalen-Brunson | ![Acceleration][cat-accel] | Loads the alibaba-pai PDD 8-step LoRAs with the head bank others drop. |
| [minimax-h3-mlx](https://github.com/mrbizarro/minimax-h3-mlx) | mrbizarro | ![Port][cat-port] | Apple Silicon MLX port of the full H3 pipeline. |
| [ClipProj](https://github.com/nicolab28/ComfyUI-ClipProj) | nicolab28 | ![Port][cat-port] | Swap the 15.7 GB text encoder for a 5.2 GB projected one. |
| [MiniMax H3 Contex Loop](https://github.com/ethanfel/ComfyUI-MiniMaxH3-Contex-Loop) | ethanfel | ![Conditioning][cat-cond] | Scene-by-scene production loop with checkpoints and seamless joins. |
| [H3-Prompt-IDE](https://github.com/ethanfel/ComfyUI-H3-Prompt-IDE) | ethanfel | ![Prompt][cat-prompt] | VS Code-style H3 prompt editor with strict section validation. |
| [MiniMax H3 LongMedia](https://github.com/vizart-vj/ComfyUI-MiniMax-H3-LongMedia) | vizart-vj | ![Acceleration][cat-accel] | Single-pass long video with streamed attention and VRAM guards. |
| [MiniMaxH3 Hybrid Loader](https://github.com/scottmudge/ComfyUI_MinimaxH3HybridLoader) | scottmudge | ![Port][cat-port] | Merge selected tensor groups from a ref2va overlay onto an fl2va base. |
| [MiniMax H3 Legacy Audio Sampling](https://github.com/starsFriday/ComfyUI-MiniMax-H3-LegacySampling) | starsFriday | ![Acceleration][cat-accel] | Restores pre-0.31 audio sampling after a ComfyUI upgrade. |
| [FastH3Patcher](https://github.com/Nynxz/ComfyUI-FastH3Patcher) | Nynxz | ![Acceleration][cat-accel] | Run FastVideo FastH3 on the fl2va checkpoint you already have. |
| [H3-FaceRefine](https://github.com/Carasibana/ComfyUI-H3-FaceRefine) | Carasibana | ![Face Refine][cat-face] | Repair and enhance faces in generated H3 frames. |
| [H3-Relight (bruxosdovfx)](https://github.com/NyckM/H3-Relight-Minimax-ComfyUI) | NyckM | ![Prompt][cat-prompt] | Light rig that compiles a lighting reference and prompt for H3 Edit. |
| [MiniMaxH3Mod](https://github.com/Luisacaotica/ComfyUI-MiniMaxH3Mod) | Luisacaotica | ![Conditioning][cat-cond] | Reuse references as tiny extracted safetensors instead of heavy inputs. |
| [MiniMax H3 Extender](https://github.com/tritant/ComfyUI_MiniMax_H3_Extender) | tritant | ![Conditioning][cat-cond] | Chain clips into one continuous sequence, motion and audio preserved. |
| [Minimax-H3-Extender (pmhaidn)](https://github.com/pmhaidn/ComfyUI-Minimax-H3-Extender) | pmhaidn | ![Conditioning][cat-cond] | Video plus phase-locked audio extension with seam smoothing. |
| [ALLinONE MiniMaxH3](https://github.com/LeonQ8/ComfyUI-ALLinONE-MinimaxH3) | LeonQ8 | ![Conditioning][cat-cond] | T2V, I2V, R2V, audio drive, keyframes, extend, chain and upscale in one node. |
| [Qwen H3 Prompt](https://github.com/chflame163/ComfyUI_Qwen_H3_Prompt) | chflame163 | ![Prompt][cat-prompt] | Offline Qwen GGUF writes the H3 prompt from your references. |
| [OpenH3-IR](https://github.com/ruashots/open-h3-ir) | ruashots | ![Prompt][cat-prompt] | Compiles plain language into a validated six-section H3 brief. |
| [Vision Prompt Composer](https://github.com/gabxav/ComfyUI-Vision-Prompt-Composer) | gabxav | ![Prompt][cat-prompt] | Compose one prompt text from up to eight image references. |
| [MiniMax H3 Latent Upscaler](https://github.com/LBH-123-AI/ComfyUI_Minimax_h3_latent_Upscaler) | LBH-123-AI | ![Upscaling][cat-upscale] | 1x-4x neural latent upscaling that skips the VAE round-trip. |
| [MMH3-UltimateUpscale](https://github.com/bbaudio-2025/Comfyui-MMH3-UltimateUpscale) | bbaudio-2025 | ![Upscaling][cat-upscale] | Tiled and chunked resampling pass under a tight VRAM ceiling. |
| [MiniMax H3 Studio](https://github.com/thaakeno/ComfyUI-MiniMax-H3-Studio) | thaakeno | ![Conditioning][cat-cond] | H3 image workflow: T2I, I2I, reference editing, face refine, benchmarks. |
| [MiniMax H3 Sampler Unlimited](https://github.com/hradec/ComfyUI-MiniMax-H3-Sampler-Unlimited) | hradec | ![Acceleration][cat-accel] | Chunked sampler for over 15 s of video and 2K on about 16 GB VRAM. |
| [MiniMax H3 Parallel](https://github.com/AesSedai/ComfyUI-MiniMaxH3-Parallel) | AesSedai | ![Acceleration][cat-accel] | Multi-GPU attention-head sharding for Ref2VA. |
| [MiniMax H3 SPEED](https://github.com/StanLukuvka/ComfyUI-MiniMax-H3-SPEED) | StanLukuvka | ![Acceleration][cat-accel] | Progressive-resolution sampler: denoise coarse, then refine to full. |
| [MiniMax H3 Keyframe Offset](https://github.com/asirusasr-maker/ComfyUI-MiniMax-H3-Keyframe-Offset) | asirusasr-maker | ![Conditioning][cat-cond] | Keyframes at arbitrary frame indices, plus a text-to-audio node. |
| [MaskVidExperiments](https://github.com/drozbay/MaskVidExperiments) | drozbay | ![Conditioning][cat-cond] | Stable-crop video masking and inpainting without jitter. |
| [MiniMaxRefPack](https://github.com/Hearmeman24/ComfyUI-MiniMaxRefPack) | Hearmeman24 | ![Prompt][cat-prompt] | Manage all 18 Ref2VA references from one node; writes the prompt. |
| [H3-LongVideos](https://huggingface.co/Smite79/MiniMax-H3-Longvideos) | Smite79 | ![Conditioning][cat-cond] | Script-to-long-video chaining with continuity and audio discipline. |

### ▣ Special Stuff

* [MiniMax-H3-Semantic-Bridge](https://huggingface.co/speach1sdef178/MiniMax-H3-Semantic-Bridge) by speach1sdef178 - Compact (~11 MB) **conditioning-space semantic adapter** for standard H3 FL2VA text-conditioned generation: grew out of a cross-architecture representation-transfer project using SenseNova U1.5 as semantic teacher (distilled to a standalone H3 adapter — SenseNova not required at inference). Not a LoRA / checkpoint merge / parameter graft — it transforms native H3 conditioning before the video transformer and blends the learned semantic representation back at controllable strength. v1 scope: FL2VA text-conditioned only (Ref2VA reference workflows unsupported; reference-audio tests degraded lip-sync). Ships a ComfyUI custom node (`MiniMax_H3_Semantic_Bridge_v1.0.zip`), the adapter (`MiniMaxH3_SemanticBridge_v1.safetensors`, 10.5 MB), a full research article, A/B examples with exact prompts, and raw training/eval scripts (developed on a single RTX 3090 Ti). MiniMax H3 Community License.

* [keys-heretic-MiniMax-H3 sol-engine + speed upgrades + upscaler finish — Single DGX Spark](https://github.com/drowzeys/keys-heretic-MiniMax-H3-sol-engine-more-speed-upgrades-upscaler-finish-Single-DGX-Spark) by drowzeys - One-shot recipe for MiniMax-H3 on a single NVIDIA DGX Spark (GB10, sm_121): Sol-Engine ports, Ultra-Heretic TE, Spectrum forecasting, SageAttention, 0.5 MPix generate + RealESRGAN x2 finish. Includes formal benchmark ladder (1.55× vs dense stock).

* [h3.c (h3-metal)](https://github.com/antirez/h3.c) by antirez - Native C/Metal inference engine for Apple Silicon. Prompt-to-video/audio, first/last-frame, and Ref2VA references work end-to-end on M3/M5 Max. Interactive Iris-style session. Not a ComfyUI node — standalone binary.

* [h3-ops](https://github.com/quantz8a/h3-ops) by quantz8a - Local ops companion for [antirez/h3.c](https://github.com/antirez/h3.c) on Apple Silicon: `h3ctl doctor` / GPU lock, ContextDoc CIR (`compile`/`validate`/`revise`), presets, and honest HD labels (`native` / `upscale_*` / optional cloud 2K). Does not fork Metal/DiT. MIT. Not a ComfyUI node — standalone CLI.

* [h3-webui](https://github.com/AntaresAlice/h3-webui) by AntaresAlice - Self-hosted video-generation **web UI** on ComfyUI + MiniMax-H3: merged 3-view interface (Chat / Overview / Studio), workspaces, history, real step-level progress (WebSocket→SSE), reference reuse, and video continuation (last-frame → next first-frame). Native H3 audio out; Turbo-LoRA auto-match. Frontend native JS + aiohttp backend; MIT. Not a ComfyUI node — wraps your existing ComfyUI instance.

* [ComfyMax](https://github.com/danielveresbelgium/comfymax) by danielveresbelgium - Local Windows **Streamlit front-end for preparing and reviewing H3 renders** — the "ComfyUI without the node graph" workflow: a Scene Builder (characters, action, ordered dialogue turns, ending, camera, lighting) plus LM Studio integration to turn a scene idea into a structured six-section H3 prompt (or paste a finished prompt and skip the LLM entirely). Also ships a searchable local Prompt Library, a Video Gallery (play/filter/sort/download/delete over your output folders), and a Workflow Mapper that inspects an API workflow, suggests input mappings, and installs workflow + mapping together — with text-only and 1–9 reference-image mappings. Optional FlashVSR v1.1 Tiny-Long 2× upscaler installs into its own isolated env with checksum verification. Requires Windows 64-bit Python 3.11, a working ComfyUI (default `127.0.0.1:8188`) and optionally LM Studio (`:1234`). Not a ComfyUI node — a standalone companion app that talks to your ComfyUI over its API.

* [Omni-Rewriter](https://github.com/WayneJin0918/Omni-Rewriter) by WayneJin0918 - Open agentic prompt-expansion (PE) harness for image/video generation. Turns everyday intent into validated, model-ready prompts via a bounded AI-agent loop (Analyze → Draft → Validate → Repair → Render). Current video profile is MiniMax-H3; ships a CLI (`omni-rewriter expand`) + HTTP server (`POST /v1/expand`), deterministic PE validation, and a reusable CI lint Action. Apache-2.0. Not a ComfyUI node — standalone tool (generation adapters stay outside `expand`).

* **MiniMax-H3-Prompt-Rewriter-LoRA-8B** — PEFT LoRA adapter on Qwen3-VL-8B-Instruct ([lightx2v](https://huggingface.co/lightx2v/MiniMax-H3-Prompt-Rewriter-LoRA-8B)) that turns short user requests into production-oriented MiniMax-H3 audio-video prompts — structured shot timeline, synchronized physical/ambient sound, and music guidance. Covers T2VA / I2VA / L2VA / FL2VA (text + keyframe-conditioned); Ref2VA not supported. Pair with LightX2V (or the pytraveler ComfyUI node) to generate. GGUF quants ([pytraveler](https://huggingface.co/pytraveler/MiniMax-H3-Prompt-Rewriter-LoRA-8B-GGUF)) run under llama.cpp against a quantized multimodal Qwen3-VL-8B-Instruct (sees reference frames) and ship a [ComfyUI node](https://github.com/pytraveler/MiniMax-H3-Prompt-Rewriter-ComfyUI).

  | Format | Precision | Size | Download |
  | :--- | :---: | :---: | :--- |
  | PEFT adapter | ![fp32][badge-fp32] | 2.79 GB | [![][gh-lightx2v]](https://huggingface.co/lightx2v/MiniMax-H3-Prompt-Rewriter-LoRA-8B/resolve/main/adapter_model.safetensors) |
  | GGUF | ![F16][badge-fp16] | 1.30 GB | [![][gh-pytraveler]](https://huggingface.co/pytraveler/MiniMax-H3-Prompt-Rewriter-LoRA-8B-GGUF/resolve/main/MiniMax-H3-Prompt-Rewriter-LoRA-8B-F16.gguf) |
  | GGUF ★ | ![Q8_0][badge-Q8_0] | 0.69 GB | [![][gh-pytraveler]](https://huggingface.co/pytraveler/MiniMax-H3-Prompt-Rewriter-LoRA-8B-GGUF/resolve/main/MiniMax-H3-Prompt-Rewriter-LoRA-8B-Q8_0.gguf) |

  *★ Q8_0 recommended for most setups.*

* **MiniMax-H3-Prompt-Rewriter-LoRA-Omni** — PEFT LoRA adapter on **Qwen2.5-Omni-7B** ([lightx2v](https://huggingface.co/lightx2v/MiniMax-H3-Prompt-Rewriter-LoRA-Omni)) — the multimodal sibling of the 8B rewriter above. Rewrites short requests *with optional image / video / audio references* into structured, production-ready MiniMax-H3 audio-video prompts. Covers **T2AV / I2AV / L2AV / FL2AV** (text + image) and **Ref2AV** (ordered images, videos, and/or audio) — the only rewriter in the list that supports Ref2VA input. Text-only output (`enhanced_prompt`); does not render. Apache-2.0. Download `adapter_model.safetensors` via [resolve/main](https://huggingface.co/lightx2v/MiniMax-H3-Prompt-Rewriter-LoRA-Omni/resolve/main/adapter_model.safetensors) (no GGUF variant; base Qwen2.5-Omni-7B fetched separately).

* [MiniMax-H3-Single-Frame-VAE-500K](https://huggingface.co/iamkaikai/MiniMax-H3-Single-Frame-VAE-500K) by iamkaikai - Single-frame **image** decoder (VAE) for MiniMax-H3, trained 500K steps — reconstructs, generates, and edits individual H3 frames (text-to-image, material edits, sketch→render, reconstruction). Ships `load_decoder.py` + example prompts; use alongside the H3 video VAE for image-only work. Download `minimax_h3_single_frame_decoder_500k.safetensors` (≈9.69 GB) via [resolve/main](https://huggingface.co/iamkaikai/MiniMax-H3-Single-Frame-VAE-500K/resolve/main/minimax_h3_single_frame_decoder_500k.safetensors).

* [MiniMax-H3-Fun-Controlnet-Union](https://huggingface.co/alibaba-pai/MiniMax-H3-Fun-Controlnet-Union) by alibaba-pai (PAI) - **Fun ControlNet Union for MiniMax-H3** — single unified control adapter covering canny, depth, HED, MLSD, and pose conditioning for H3 video generation (sample results per mode in the repo). `MiniMax-H3-Fun-Controlnet-Union.safetensors` (6.81 GB); Apache-2.0 with MiniMax H3 Community License terms for the base model ([LICENSE](https://huggingface.co/alibaba-pai/MiniMax-H3-Fun-Controlnet-Union/blob/main/LICENSE)).

* **MiniMax-H3 Concept Embeddings** ([Comfy-Org/MiniMax-H3 · `embeddings/`](https://huggingface.co/Comfy-Org/MiniMax-H3/tree/main/embeddings)) - 10 small trigger/textual-inversion **concept embeddings** (each `minimaxh3_*.safetensors`, 0.5–1.5 MB): `art_is_explosion`, `blooming_flowers`, `bullet_time`, `dark_magic`, `fire_breath`, `four_seasons`, `kiss_camera`, `spiral_ascent`, `storm_magic`, `truman_show`. Lightweight per-concept vectors invoked by their keyword in a prompt to inject a cinematic or artistic effect without fine-tuning. Official repo, no license file (MiniMax H3 Community License applies to the base model).
<p id="guides" align="center">◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆</p>

## ▓ Guides & Tutorials

### ▣ Official Guides

* [Video Prompt Writing Guide (Base)](https://huggingface.co/MiniMaxAI/MiniMax-H3/blob/main/docs/VIDEO_PROMPT_WRITING_GUIDE_base_en.md) - Official MiniMax-H3 prompt writing guide for base (FL2VA) mode. Covers prompt structure, camera language, scene composition, and best practices for text-to-video and image-to-video generation.
* [Video Prompt Writing Guide (Reference)](https://huggingface.co/MiniMaxAI/MiniMax-H3/blob/main/docs/VIDEO_PROMPT_WRITING_GUIDE_ref_en.md) - Official MiniMax-H3 prompt writing guide for reference (Ref2VA) mode. Covers multi-modal reference inputs, image/video/audio reference handling, and prompt construction for omni-reference generation.

### ▣ ComfyUI Tutorials

* [ComfyUI MiniMax-H3 Tutorial](https://docs.comfy.org/tutorials/video/minimax/minimax-h3) - Official ComfyUI documentation tutorial for MiniMax-H3 setup and usage.
* [MiniMax H3 Day-0 Support in ComfyUI](https://blog.comfy.org/p/minimax-h3-day-0-support-in-comfyui) - ComfyUI blog post covering open weights, native audio, 2K video output, and local execution on a 3060.

### ▣ Performance

* [MiniMax H3 — Performance & Best-Configuration Report](guides/minimax-h3-performance.md) - Local-inference performance guide for MiniMax H3 (FL2VA / Ref2VA) across consumer & workstation GPUs, Apple Silicon, and the DGX Spark — distilled from 2 hard-numbered benchmarks and 17 community field reports. Covers a TL;DR config recommendation, hardware-tier tiers, the best speed/quality recipe, and caveats & licensing.
* [MiniMax H3 on an RTX 3060 12GB: what we actually measured](https://www.minimaxh3tutorial.com/rtx-3060) - Real-world write-up of running MiniMax-H3 on a 12 GB RTX 3060 — what actually fits, at what resolution and step counts, and the configuration that worked.
* [MiniMax H3 speed-up notes (matsuo-koya)](https://github.com/matsuo-koya/minimax-h3-notes) - Measured field notes from three weeks on one RTX 5090 (32 GB, WSL2, ComfyUI 0.33) building a home lip-sync music-video studio, plus a 4090 worker and Apple Silicon: INT8 ConvRot (true quant error 0.90%), Turbo 8-step, a self-converted FastH3 4-step ComfyUI LoRA (1.87× vs Turbo, zero failures over a 30-segment MV), comfy-kitchen INT8 attention (sampler ≈2× on 5090, 1.79× at production length; VAE decode untouched), width 1280→1216 (−15% via VAE tile count), a pull-based 5090+4090 distributed segment queue (3.8→2.7 h), the 345-frame stall cliff on the 4090 (per-step profiling), negative results (Zironic H3MemoryOptimization silently changes output; ToneCompensate unneeded; PDD Acc-LoRAs need a missing sampler), and two key conversion findings — diffusers→ComfyUI H3 LoRAs have **swapped fused `fc1` halves** (`[value; gate]` vs `[gate; value]`), and ComfyUI silently falls back to tiled VAE decode on OOM. Full Japanese write-up + English summary. MIT.
* [MiniMax H3 on an 8 GB Laptop — Six Measured Traps](https://github.com/FlowForgeLabAi/-h3-8gb-traps) by [FlowForgeLabAi](https://github.com/FlowForgeLabAi) - Field notes from an RTX 5060 Laptop 8 GB (sm_120) + 16 GB RAM, each trap with a reproduction. Two that change how you configure things: the wall is **16 GB of system RAM, not 8 GB of VRAM** — a ~34.5 GiB working set pages, and the symptom is a stalled sampler while `utilization.gpu` still reads 99% (the tell is `nvidia-smi` power drawn flat at 34–36 W, against 64–98 W healthy; 0.9–6 s/block fresh vs 212 s/block after ~1.7 h), so restarting ComfyUI before each run matters more than any sampler setting; and at H3's real geometry (56 heads × 128, S=8192, bf16) **comfy-kitchen INT8 attention measures 22.8 ms against 143.1 ms for SDPA**, while the SageAttention patch calls `_sageattn_int8_fp8_nhd` directly and bypasses `optimized_attention`, so backend flags have no effect while it is installed. Also: `SaveVideo`'s H.264 path fails with EINVAL on odd width or height — libx264 itself is fine (ComfyUI #16544); use `VHS_VideoCombine`, 2067 → 10393 kb/s); a 10 s clip losing its subject at ~7 s is a prompt-timeline bug, reproducible on the official 20-step baseline; a turbo LoRA loaded through the standard LoRA path on a pruned base applies **208 of 259 modules** (51 `adaln_proj.linear` skipped, once per layer per step — check the applied/skipped counts in the log); and `--disable-pinned-memory` is required below 16 GB. Three-tier companion pack (20 / 8 / 4 steps; 10 s measured at 14.3 min vs 33.8–43.5 min): [MiniMax-H3-8GB-Workflows](https://github.com/FlowForgeLabAi/MiniMax-H3-8GB-Workflows). Measured-but-unconfirmed items are labelled as such in the repo, and both are MIT.

### ▣ Prompting & Prompt Datasets

* [MiniMax H3 — 1,000-Prompt Curation](https://github.com/yangzhou-chaofan/minimax-h3-1000-prompts) - Curated index + analysis of the `ostris/minimax_h3_1k` dataset (1,000 prompts + 768p clips, generated with the pruned INT8-ConvRot FL2VA checkpoint @ 30 steps). Explains H3's 3-field prompt structure (`integrated_multimodal_description` / `overall_soundscape` / `non_diegetic_music`), highlights 10 reusable prompts with commentary, and compares H3 vs Seedance / Veo / Kling on fidelity, dialogue, sound design, and multi-shot continuity.
* [Interactive atlas of all 1,000 clips (neta.art)](https://neta.art/use-cases/en/h3-1000-prompt-list) - Browse every clip from the 1K prompt dataset — every prompt, every style — with per-clip metadata: shooting-style/subject filters, prompt / soundscape / music / aspect-ratio / dialogue details, one-click generate or download.
* [Codex × MiniMax H3 自动成片与验收 Skill](https://github.com/JiaYang-BUAA/codex-minimax-h3-video-skill) - Codex Skill for automated multi-shot H3 video production + QA: Codex splits storyboards and writes prompts, Z-Image generates first/last frames, **MiniMax H3 Director** schedules H3 shot generation (with audio), HyperFrames handles editable timeline editing/rendering, then Codex verifies dialogue (ASR), continuity, black frames, and specs — with local rework loops. Windows 11 + PowerShell 7 + ComfyUI ≥ 0.30; validated on RTX 5070 Ti 16 GB (~49 GB models). MIT; no model weights bundled.


<p id="wf" align="center">◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆</p>

## ▓ Workflow & Technical Notes

<a id="wf-comfyui"></a>

ComfyUI workflow templates and community graphs for MiniMax-H3, organized by generation mode. Direct-import `.json` links where available; pack repos link to the repo root.

| Workflow | Author | Mode | Description |
| :--- | :---: | :---: | :--- |
| [Text-to-Video (T2V)](https://github.com/Comfy-Org/workflow_templates/blob/main/archived/api_hailuo_minimax_t2v.json) | Comfy-Org | T2VA | Official Comfy-Org template — now API-based (Hailuo/Minimax API); archived. |
| [OrbitQuant T2VA Workflow](https://huggingface.co/WaveCut/MiniMax-H3-OrbitQuant-W4A4/resolve/main/comfyui/workflows/MiniMax-H3-OrbitQuant-T2VA.json) | WaveCut | T2VA | Ready-to-import ComfyUI workflow for OrbitQuant W4A4; derived from Comfy-Org T2V. |
| [OrbitQuant T2VA API Workflow](https://huggingface.co/WaveCut/MiniMax-H3-OrbitQuant-W4A4/resolve/main/comfyui/workflows/MiniMax-H3-OrbitQuant-T2VA-api.json) | WaveCut | T2VA | API-prompt version of the OrbitQuant T2VA workflow. |
| [T2V — Custom Prompt](https://github.com/Hearmeman24/comfyui-minimax/blob/master/workflows/MiniMax%20H3/MiniMax%20-%20T2V%20-%20Custom%20Prompt.json) | Hearmeman24 | T2VA | You write the full H3 prompt; Turbo LoRA + preview wired. |
| [T2V — Auto Prompt](https://github.com/Hearmeman24/comfyui-minimax/blob/master/workflows/MiniMax%20H3/MiniMax%20-%20T2V%20-%20Auto%20Prompt.json) | Hearmeman24 | T2VA | VLM writes the full six-section H3 prompt from one line. |
| [Base Prompt generator](https://huggingface.co/StefanFalkok/Minimax_H3_Workflows/resolve/main/Minimax%20H3/Minimax%20H3%20Base%20Prompt%20generator.json) | StefanFalkok | T2VA | Writes the full six-section H3 prompt from a short idea; pairs with the I2V/Ref2V graphs. |
| [Image-to-Video (I2V)](https://github.com/Comfy-Org/workflow_templates/blob/main/archived/api_hailuo_minimax_i2v.json) | Comfy-Org | I2VA | Official Comfy-Org template — API-based; archived. |
| [I2V — Custom Prompt](https://github.com/Hearmeman24/comfyui-minimax/blob/master/workflows/MiniMax%20H3/MiniMax%20-%20I2V%20-%20Custom%20Prompt.json) | Hearmeman24 | I2VA | You write the prompt; image input + Turbo LoRA + preview. |
| [I2V — Auto Prompt](https://github.com/Hearmeman24/comfyui-minimax/blob/master/workflows/MiniMax%20H3/MiniMax%20-%20I2V%20-%20Auto%20Prompt.json) | Hearmeman24 | I2VA | VLM writes the H3 prompt from one line + image. |
| [INT8 I2V (javano2609.1.3)](https://huggingface.co/javawock7618/comfy-MiniMax-H3-workflows/resolve/main/MiniMax_int8_I2V-javano2609.1.3.json) | javawock7618 | I2VA | INT8 low-VRAM image-to-video workflow — FLF/I2V with Extend, ControlNet Union V2V, and Latent Upscaler. Current version (older 2608.x/2609.1.x files were removed from the repo). |
| [I2V](https://huggingface.co/StefanFalkok/Minimax_H3_Workflows/resolve/main/Minimax%20H3/Minimax%20H3%20I2V.json) | StefanFalkok | I2VA | Image-to-video graph with stock LoRA/standard nodes. |
| [FL2V GGUF Workflow](https://huggingface.co/Abiray/MiniMax-H3-GGUF/resolve/main/minimax_fl2v_gguf_workflow.json) | Abiray | FL2VA | ComfyUI workflow for loading/running the GGUF-quantized FL2VA model. |
| [Multi-Reference Fight (wushu)](https://huggingface.co/Jojocodex/wushu-action-v7-minimax-h3-fl2va-ref2va-lora/resolve/main/Minimax%20h3%E5%A4%9A%E5%8F%82%E8%80%83%E5%8F%8C%E9%87%87%E6%89%93%E6%96%97%E5%B7%A5%E4%BD%9C%E6%B5%81.json) | Jojocodex | FL2VA | Multi-reference dual-dispatch combat graph for the wushu LoRAs — several references per fight beat, euler/simple 25 steps, CFG 1.0. |
| [Video (generic API)](https://github.com/Comfy-Org/workflow_templates/blob/main/archived/api_hailuo_minimax_video.json) | Comfy-Org | Ref2VA | Official Comfy-Org generic API video template; archived. |
| [OrbitQuant Ref2VA API Workflow](https://huggingface.co/WaveCut/MiniMax-H3-OrbitQuant-W4A4/resolve/main/comfyui/workflows/MiniMax-H3-OrbitQuant-Ref2VA-api.json) | WaveCut | Ref2VA | API-prompt version of the OrbitQuant Ref2VA workflow. |
| [Ref2VA GGUF Workflow](https://huggingface.co/Abiray/MiniMax-H3-GGUF/resolve/main/minimax_ref2va_gguf_workflow.json) | Abiray | Ref2VA | ComfyUI workflow for the GGUF-quantized Ref2VA model. |
| [R2V — Auto Prompting + Reference Manager](https://github.com/Hearmeman24/ComfyUI-MiniMaxRefPack/blob/main/example_workflows/MiniMax%20R2V%20-%20Auto%20Prompting%20%2B%20Reference%20Manager.json) | Hearmeman24 | Ref2VA | All 18 references wired once; H3 prompt auto-written; preview out (RefPack node). |
| [R2V — Auto Prompt](https://github.com/Hearmeman24/comfyui-minimax/blob/master/workflows/MiniMax%20H3/MiniMax%20-%20R2V%20-%20Auto%20Prompt.json) | Hearmeman24 | Ref2VA | VLM writes the H3 prompt from references. |
| [R2V (video_minimax_h3_r2v)](https://github.com/Hearmeman24/comfyui-minimax/blob/master/workflows/MiniMax%20H3/video_minimax_h3_r2v.json) | Hearmeman24 | Ref2VA | Reference-to-video workflow (stock naming). |
| [INT8 R2V (javano2609.2.4)](https://huggingface.co/javawock7618/comfy-MiniMax-H3-workflows/resolve/main/MiniMax_int8_R2V-javano2609.2.4.json) | javawock7618 | Ref2VA | INT8 low-VRAM reference-to-video workflow — Reference LoRA, ControlNet Union V2V, Extend, and Latent Upscaler. Current version (older 2608.x/2609.1.x/2609.2.x files removed from the repo). |
| [Ref2V](https://huggingface.co/StefanFalkok/Minimax_H3_Workflows/resolve/main/Minimax%20H3/Minimax%20H3%20Ref2V.json) | StefanFalkok | Ref2VA | Reference-to-video graph with stock nodes. |
| [Ref2V Prompt generator](https://huggingface.co/StefanFalkok/Minimax_H3_Workflows/resolve/main/Minimax%20H3/Minimax%20H3%20Ref2V%20Prompt%20generator.json) | StefanFalkok | Ref2VA | Writes the H3 prompt for reference-to-video from references. |
| [I2V — Face Refine](https://huggingface.co/StefanFalkok/Minimax_H3_Workflows/resolve/main/Minimax%20H3%20Face%20Refine/Minimax%20H3%20I2V%20Face%20Refine.json) | StefanFalkok | I2VA | Image-to-video graph with a dedicated face-refine pass wired in. |
| [Face Refiner V2V](https://huggingface.co/StefanFalkok/Minimax_H3_Workflows/resolve/main/Minimax%20H3%20Face%20Refine/Face%20Refiner%20V2V.json) | StefanFalkok | Ref2VA | Video-to-video face-refinement graph — repairs/enhances faces in an existing clip. |
| [Music-Video — Long-Shot Latent-Mask (Base+Ref)](https://huggingface.co/RuneXX/Minimax-H3-Workflows/resolve/main/Music-Video/Minimax-H3_-_Music-Video_Long-Shot-Latent-Mask_Base-Ref.json) | RuneXX | Ref2VA | Music-video workflow: long single shot with latent masking, base + reference conditioning. |
| [Music-Video — Long-Shot Latent-Mask (Multi-Scene Ref)](https://huggingface.co/RuneXX/Minimax-H3-Workflows/resolve/main/Music-Video/Minimax-H3_-_Music-Video_Long-Shot-Latent-Mask_MultiScene-Ref.json) | RuneXX | Ref2VA | Music-video workflow: multi-scene reference conditioning with latent masking. |
| [V2V — Extend Any Video (latent masking)](https://huggingface.co/RuneXX/Minimax-H3-Workflows/resolve/main/Video-to-Video/Minimax-H3_-_V2V_Extend_Any_Video_latent_masking.json) | RuneXX | Ref2VA | Video-to-video extension of any source clip via latent masking. |
| [H3 Seamless Chain (CORE)](https://huggingface.co/joeygambino/MiniMax-H3-Multishot-Workflow/resolve/main/workflows/H3_Seamless_Chain_CORE.json) | joeygambino | Multi-shot | Core seamless multi-shot chaining graph (FL2VA/Ref2VA clips). |
| [H3 Seamless Chain v2](https://huggingface.co/joeygambino/MiniMax-H3-Multishot-Workflow/resolve/main/workflows/H3_Seamless_Chain_v2.json) | joeygambino | Multi-shot | Multi-shot chaining workflow (v2). |
| [H3 Extend Take](https://huggingface.co/joeygambino/MiniMax-H3-Multishot-Workflow/resolve/main/workflows/H3_Extend_Take.json) | joeygambino | Multi-shot | Clip extension / take workflow. |
| [H3 Keyframes](https://huggingface.co/joeygambino/MiniMax-H3-Multishot-Workflow/resolve/main/workflows/H3_Keyframes.json) | joeygambino | Multi-shot | Keyframe-conditioned chaining. |
| [Music-Video — Multi-Scene Shot-by-Shot](https://huggingface.co/RuneXX/Minimax-H3-Workflows/resolve/main/Music-Video/Minimax-H3_-_Music-Video_Multi-Scene_Shot-by-Shot.json) | RuneXX | Multi-shot | Music-video workflow that builds a multi-scene clip shot-by-shot. |
| [comfy-MiniMax-H3-workflows (pack)](https://huggingface.co/javawock7618/comfy-MiniMax-H3-workflows) | javawock7618 | Bundle | Full INT8 low-VRAM acceleration stack: INT8 + native Block Sparse Attention + Spectrum + Lightx2v + Turbo + Motion Context + Fun ControlNet Union V2V (openpose/canny/depth) + Extend + Latent Upscaler + TTS (+ Music, Ref2Image, LLM system-prompt utilities). |
| [PlagueKind-MinimaxH3 (pack)](https://huggingface.co/Plaguekind/Minimax-H3) | Plaguekind | Bundle | "Ease of use" I2V/R2V workflow line, currently **V9** (requires his nodepack v1.4.7 + latest ComfyUI): sparse comfy-engine mode, INT8 kernel, H3 cache, R2V VAE bypass, SLA reference protection, Dareties turbo blends, ER_SDE override, tiled upscaling, and an included fast turbo LoRA (functional strength up to 5.0); Eros / Sulphur-model and FaceID compatible. Older V1–V8 versions kept under `old/`. MIT. |
| [INT8 TTS](https://huggingface.co/javawock7618/comfy-MiniMax-H3-workflows/resolve/main/MiniMax_int8_TTS-javano2609.1.json) | javawock7618 | Bundle | TTS audio workflow (current 2609.1 version). |
| [Music3](https://huggingface.co/javawock7618/comfy-MiniMax-H3-workflows/resolve/main/extra/MiniMax-Music3-javano2608.1.json) | javawock7618 | Bundle | Music generation workflow. |
| [Ref2Image](https://huggingface.co/javawock7618/comfy-MiniMax-H3-workflows/resolve/main/extra/MiniMax_int8-Ref2Image-javano2608.2.json) | javawock7618 | Bundle | Reference-to-image utility. |
| [INT8 Bridge](https://huggingface.co/javawock7618/comfy-MiniMax-H3-workflows/resolve/main/MiniMax_int8_Bridge-javano2609.1.1.json) | javawock7618 | Bundle | INT8 low-VRAM clip-bridge / transition workflow (A→B transition; current 2609.1.1 version). |
| [INT8 FR (Face Refine)](https://huggingface.co/javawock7618/comfy-MiniMax-H3-workflows/resolve/main/MiniMax_int8_FR-javano2609.1.1.json) | javawock7618 | Bundle | INT8 low-VRAM face-refine (FR) workflow (current 2609.1.1 version). |
| [FL2VA LLM system prompt](https://huggingface.co/javawock7618/comfy-MiniMax-H3-workflows/resolve/main/llm_system_prompt_for_minimax-h3_fl2va-2608.6.txt) | javawock7618 | Bundle | Drop-in LLM system prompt for auto-writing structured FL2VA prompts (pair with a local LLM node). |
| [Ref2VA LLM system prompt](https://huggingface.co/javawock7618/comfy-MiniMax-H3-workflows/resolve/main/llm_system_prompt_for_minimax-h3_ref2va-2608.8.txt) | javawock7618 | Bundle | Ref2VA counterpart of the FL2VA LLM system prompt. |
| [MiniMax-H3-Multishot-Workflow (pack)](https://huggingface.co/joeygambino/MiniMax-H3-Multishot-Workflow) | joeygambino | Bundle | ComfyUI-H3-Multishot node pack + multi-shot workflows + presenter demo. Apache-2.0. |

*Comfy-Org's original `templates/video_minimax_h3_*` T2V/I2V/R2V graphs were moved to `archived/` and are now API-based (Hailuo/Minimax API) templates — links above point to the archived JSONs. Abiray also ships a Ref2VA GGUF workflow (newly listed).*

*StefanFalkok's repo was restructured: the three Turbo-variant graphs it used to carry (`I2V — Larryvrh Turbo`, `I2V — PDD-Acc 8-Steps Turbo`, `Ref2V — PDD-Acc 8-Steps Turbo`) have been **removed upstream** and were dropped from this table — the `Minimax H3/` folder now holds only the four stock graphs (`Base Prompt generator`, `I2V`, `Ref2V`, `Ref2V Prompt generator`). A new `Minimax H3 Face Refine/` folder adds two face-refinement graphs (I2V and V2V), listed above. For PDD-Acc 8-step acceleration, use the [alibaba-pai Acc LoRAs](https://huggingface.co/alibaba-pai/MiniMax-H3-Acc-LoRAs) directly (see [Turbo](#checkpoints)).*

<!-- MARKDOWN LINKS & IMAGES -->
[telegram-shield]: https://img.shields.io/badge/TokenDiff-26A5E4?style=for-the-badge&logo=telegram&logoColor=white
[telegram-url]: https://t.me/TokenDiff
[x-shield]: https://img.shields.io/badge/wildmindai-000000?style=for-the-badge&logo=x&logoColor=white
[x-url]: https://x.com/wildmindai

[gh-Comfy--Org]: https://img.shields.io/badge/Comfy--Org-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-Abiray]: https://img.shields.io/badge/Abiray-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-DiffSynth-Studio]: https://img.shields.io/badge/DiffSynth--Studio-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-DmitryDB]: https://img.shields.io/badge/DmitryDB-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-WaveCut]: https://img.shields.io/badge/WaveCut-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-dummy9996]: https://img.shields.io/badge/dummy9996-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-ethanfel]: https://img.shields.io/badge/ethanfel-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-rockerBOO]: https://img.shields.io/badge/rockerBOO-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-Kijai]: https://img.shields.io/badge/Kijai-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-AX1Y2JP]: https://img.shields.io/badge/AX1Y2JP-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-tsolful]: https://img.shields.io/badge/tsolful-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-realrebelai]: https://img.shields.io/badge/realrebelai-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-rzgar]: https://img.shields.io/badge/rzgar-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-larryvrh]: https://img.shields.io/badge/larryvrh-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-drbaph]: https://img.shields.io/badge/drbaph-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-vantagewithai]: https://img.shields.io/badge/vantagewithai-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-Mamad8]: https://img.shields.io/badge/Mamad8-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-NicoLab28]: https://img.shields.io/badge/NicoLab28-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-lightx2v]: https://img.shields.io/badge/lightx2v-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-pytraveler]: https://img.shields.io/badge/pytraveler-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-lihaoyun6]: https://img.shields.io/badge/lihaoyun6-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-LBH-123-AI]: https://img.shields.io/badge/LBH--123--AI-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-Asirus]: https://img.shields.io/badge/Asirus-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-tutututututu]: https://img.shields.io/badge/tutututututu-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-t8star]: https://img.shields.io/badge/t8star-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-abakanai]: https://img.shields.io/badge/abakanai-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-Winnougan]: https://img.shields.io/badge/Winnougan-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-unsloth]: https://img.shields.io/badge/unsloth-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-MarxistLeninist]: https://img.shields.io/badge/MarxistLeninist-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-joyfox]: https://img.shields.io/badge/joyfox-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-ethanfel]: https://img.shields.io/badge/ethanfel-lightgrey?style=flat-square&logo=github&logoColor=white
[gh-antirez]: https://img.shields.io/badge/antirez-lightgrey?style=flat-square&logo=github&logoColor=white
[gh-smhfacct]: https://img.shields.io/badge/smhfacct-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-infosave]: https://img.shields.io/badge/infosave-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-DIE2025]: https://img.shields.io/badge/DIE2025-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-vizart-vj]: https://img.shields.io/badge/vizart--vj-lightgrey?style=flat-square&logo=github&logoColor=white
[gh-scottmudge]: https://img.shields.io/badge/scottmudge-lightgrey?style=flat-square&logo=github&logoColor=white
[gh-starsFriday]: https://img.shields.io/badge/starsFriday-lightgrey?style=flat-square&logo=github&logoColor=white
[gh-Hearmeman]: https://img.shields.io/badge/Hearmeman-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-joeygambino]: https://img.shields.io/badge/joeygambino-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-hoidhxd]: https://img.shields.io/badge/hoidhxd-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-FastVideo]: https://img.shields.io/badge/FastVideo-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-drozbay]: https://img.shields.io/badge/drozbay-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-sonnybox]: https://img.shields.io/badge/sonnybox-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-xmarre]: https://img.shields.io/badge/xmarre-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-SexGod1979]: https://img.shields.io/badge/SexGod1979-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-alibaba-pai]: https://img.shields.io/badge/alibaba--pai-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-Beidouqixing]: https://img.shields.io/badge/Beidouqixing-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-adehong]: https://img.shields.io/badge/adehong-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-NTU-yiwen]: https://img.shields.io/badge/NTU--yiwen-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-Hippotes]: https://img.shields.io/badge/Hippotes-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-barelymining]: https://img.shields.io/badge/barelymining-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-pottokao]: https://img.shields.io/badge/pottokao-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-LoboForge]: https://img.shields.io/badge/LoboForge-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-rootonchair]: https://img.shields.io/badge/rootonchair-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-TenStrip]: https://img.shields.io/badge/TenStrip-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-WarmBloodAban]: https://img.shields.io/badge/WarmBloodAban-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-silveroxides]: https://img.shields.io/badge/silveroxides-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-xtanqn]: https://img.shields.io/badge/xtanqn-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-ssjenforcer191]: https://img.shields.io/badge/ssjenforcer191-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-Playtime--AI]: https://img.shields.io/badge/Playtime--AI-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-KennethFal]: https://img.shields.io/badge/KennethFal-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-prithivMLmods]: https://img.shields.io/badge/prithivMLmods-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-fal]: https://img.shields.io/badge/fal-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-orangesouth]: https://img.shields.io/badge/orangesouth-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-Inner--Reflections]: https://img.shields.io/badge/Inner--Reflections-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-suryatmodulus]: https://img.shields.io/badge/suryatmodulus-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-vpakarinen]: https://img.shields.io/badge/vpakarinen-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-Jojocodex]: https://img.shields.io/badge/Jojocodex-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-JOKER141]: https://img.shields.io/badge/JOKER141-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-MATLOWAI]: https://img.shields.io/badge/MATLOWAI-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-matlod]: https://img.shields.io/badge/matlod-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-shamanic]: https://img.shields.io/badge/shamanic-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-DANNY621]: https://img.shields.io/badge/DANNY621-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-bghira]: https://img.shields.io/badge/bghira-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-EllaPriest45]: https://img.shields.io/badge/EllaPriest45-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-nikdevs]: https://img.shields.io/badge/nikdevs-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-mvp--lab]: https://img.shields.io/badge/mvp--lab-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-HardGravy2]: https://img.shields.io/badge/HardGravy2-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-Alissonerdx]: https://img.shields.io/badge/Alissonerdx-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-coolthor]: https://img.shields.io/badge/coolthor-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-Rkss]: https://img.shields.io/badge/Rkss-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-taxexempt]: https://img.shields.io/badge/taxexempt-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-UntMods]: https://img.shields.io/badge/UntMods-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-videorebirth]: https://img.shields.io/badge/videorebirth-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-neph1]: https://img.shields.io/badge/neph1-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-LiseTY]: https://img.shields.io/badge/LiseTY-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-ostris]: https://img.shields.io/badge/ostris-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-RunningHubAI]: https://img.shields.io/badge/RunningHubAI-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-Cseti]: https://img.shields.io/badge/Cseti-lightgrey?style=flat-square&logo=huggingface&logoColor=white
[gh-Felldude]: https://img.shields.io/badge/Felldude-lightgrey?style=flat-square&logo=huggingface&logoColor=white

[ltype-character]: https://img.shields.io/badge/Character-0077cc?style=flat-square
[ltype-style]: https://img.shields.io/badge/Style-6f42c1?style=flat-square
[ltype-motion]: https://img.shields.io/badge/Motion-17a2b8?style=flat-square
[ltype-physics]: https://img.shields.io/badge/Physics-e83e8c?style=flat-square
[ltype-camera]: https://img.shields.io/badge/Camera-fe7d37?style=flat-square
[ltype-utility]: https://img.shields.io/badge/Utility-28a745?style=flat-square
[ltype-research]: https://img.shields.io/badge/Research-6c757d?style=flat-square
[ltype-nsfw]: https://img.shields.io/badge/NSFW-b02a37?style=flat-square

[badge-bf16]: https://img.shields.io/badge/bf16-0077cc?style=flat-square
[badge-fp16]: https://img.shields.io/badge/fp16-0077cc?style=flat-square
[badge-fp8]: https://img.shields.io/badge/fp8-28a745?style=flat-square
[badge-mxfp8]: https://img.shields.io/badge/mxfp8-20c997?style=flat-square
[badge-fp32]: https://img.shields.io/badge/fp32-6c757d?style=flat-square
[badge-int8]: https://img.shields.io/badge/int8-17a2b8?style=flat-square
[badge-int4]: https://img.shields.io/badge/int4-ffc107?style=flat-square
[badge-w4a8]: https://img.shields.io/badge/w4a8-fe7d37?style=flat-square
[badge-nvfp4]: https://img.shields.io/badge/nvfp4-6f42c1?style=flat-square
[badge-Q2_K]: https://img.shields.io/badge/Q2__K-e05d44?style=flat-square
[badge-Q3_K_M]: https://img.shields.io/badge/Q3__K__M-fe7d37?style=flat-square
[badge-Q3_K_S]: https://img.shields.io/badge/Q3__K__S-fe7d37?style=flat-square
[badge-Q4_0]: https://img.shields.io/badge/Q4__0-dfb317?style=flat-square
[badge-Q4_1]: https://img.shields.io/badge/Q4__1-dfb317?style=flat-square
[badge-Q4_K_M]: https://img.shields.io/badge/Q4__K__M-dfb317?style=flat-square
[badge-Q4_K_S]: https://img.shields.io/badge/Q4__K__S-dfb317?style=flat-square
[badge-Q5_0]: https://img.shields.io/badge/Q5__0-97c00f?style=flat-square
[badge-Q5_1]: https://img.shields.io/badge/Q5__1-97c00f?style=flat-square
[badge-Q5_K_M]: https://img.shields.io/badge/Q5__K__M-97c00f?style=flat-square
[badge-Q5_K_S]: https://img.shields.io/badge/Q5__K__S-97c00f?style=flat-square
[badge-Q6_K]: https://img.shields.io/badge/Q6__K-0077cc?style=flat-square
[badge-Q8_0]: https://img.shields.io/badge/Q8__0-28a745?style=flat-square
[badge-UD-Q2_K_XL]: https://img.shields.io/badge/UD-Q2__K__XL-e05d44?style=flat-square
[badge-UD-Q3_K_XL]: https://img.shields.io/badge/UD-Q3__K__XL-fe7d37?style=flat-square
[badge-IQ1_S]: https://img.shields.io/badge/IQ1__S-b02a37?style=flat-square
[badge-IQ1_M]: https://img.shields.io/badge/IQ1__M-d64545?style=flat-square
[badge-noinfo]: https://img.shields.io/badge/no%20description-6c757d?style=flat-square&logoColor=white

[cat-cond]: https://img.shields.io/badge/Conditioning-0077cc?style=flat-square
[cat-prompt]: https://img.shields.io/badge/Prompt-28a745?style=flat-square
[cat-upscale]: https://img.shields.io/badge/Upscaling-fe7d37?style=flat-square
[cat-accel]: https://img.shields.io/badge/Acceleration-6f42c1?style=flat-square
[cat-port]: https://img.shields.io/badge/Port-17a2b8?style=flat-square
[cat-face]: https://img.shields.io/badge/Face%20Refine-e83e8c?style=flat-square
