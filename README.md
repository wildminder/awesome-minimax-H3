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
  * [Styles](#lora)
  * [Turbo (Acceleration LoRA)](#lora)
  * [Experimental / Other](#lora)
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

4-step audio-video generation LoRAs — render joint video + synchronized stereo audio in 4 sampling steps instead of ~20 (~5× speedup). Early prototype; comfort zone for sharpness is 6–8 steps. The **lightx2v** distil (top row) is the shared base for most ComfyUI conversions; for pruned checkpoints use the ComfyUI-converted variants below. The original larryvrh LoRA targets the full (non-pruned) FL2VA checkpoint and needs the [ComfyUI-MiniMax-H3-Turbo](https://github.com/Larryvrh/ComfyUI-MiniMax-H3-Turbo) sampler node.

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
| `fl2v v1.0 768p · resized` | 4 | Pruned | ![bf16][badge-bf16] | 298 MB | [![][gh-drbaph]](https://huggingface.co/drbaph/MiniMax-H3-Turbo-Lora-ComfyUI/resolve/main/minimax_h3_fl2v_turbo_4step_v1.0_768p_comfyui_resized_avg_rank_21_bf16.safetensors) |
| `fl2v v1.0 · resized` | 8 | Pruned | ![bf16][badge-bf16] | 327 MB | [![][gh-drbaph]](https://huggingface.co/drbaph/MiniMax-H3-Turbo-Lora-ComfyUI/resolve/main/minimax_h3_fl2v_turbo_8step_v1.0_comfyui_resized_avg_rank_21_bf16.safetensors) |
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

*larryvrh also publishes experimental training checkpoints (11 `.bin` files: step 149/490/729/850/922, v2 step 298, v3 step 300, v4 step 150/600, v5 step 600; 7.26–10.17 GB) — see the [repo](https://huggingface.co/larryvrh/MiniMax-H3-Turbo-Lora/tree/main).*


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
| ✓ | ![nvfp4][badge-nvfp4] | NVFP4 | 11.67 GB | [![][gh-Abiray]](https://huggingface.co/Abiray/Minimax-H3-nvfp4-INT4-INT8-Convrot/resolve/main/MiniMax_H3_FL2VA_pruned_nvfp4.safetensors) |
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
| ✓ | ![nvfp4][badge-nvfp4] | NVFP4 | 11.67 GB | [![][gh-Abiray]](https://huggingface.co/Abiray/Minimax-H3-nvfp4-INT4-INT8-Convrot/resolve/main/MiniMax_H3_Ref2VA_pruned_nvfp4.safetensors) |
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

Native ComfyUI single-file conversion of [`diffusers-modular/MiniMax-H3-Pruned-Ref-Delta-Fused-r1024`](https://huggingface.co/diffusers-modular/MiniMax-H3-Pruned-Ref-Delta-Fused-r1024) — a fused checkpoint carrying the Ref2VA delta LoRA at rank 1024 on the pruned base (see also ethanfel's unfused delta adapters in [LoRAs → Experimental](#lora)). Diffusion transformer only; use stock H3 TE + VAEs. INT8 variants keep all 50 MLP `fc2` layers BF16 to avoid fused-swiglu INT8 OOM; validated end-to-end in ComfyUI (Continuum/Spectrum/refine). MiniMax H3 Community License.

| Variant | Precision | Size | Download |
| :--- | :---: | :---: | :--- |
| BF16 native conversion | ![bf16][badge-bf16] | 37.47 GiB | [![][gh-xmarre]](https://huggingface.co/xmarre/MiniMax-H3-Pruned-Ref-Delta-Fused-r1024-ComfyUI/resolve/main/MiniMax-H3-Pruned-Ref-Delta-Fused-r1024-comfy.safetensors) |
| INT8 tensorwise · fc2 bf16 | ![int8][badge-int8] | 23.12 GiB | [![][gh-xmarre]](https://huggingface.co/xmarre/MiniMax-H3-Pruned-Ref-Delta-Fused-r1024-ComfyUI/resolve/main/MiniMax-H3-Pruned-Ref-Delta-Fused-r1024-comfy-int8-fc2bf16.safetensors) |
| INT8 ConvRot gs256 · fc2 bf16 | ![int8][badge-int8] | 23.13 GiB | [![][gh-xmarre]](https://huggingface.co/xmarre/MiniMax-H3-Pruned-Ref-Delta-Fused-r1024-ComfyUI/resolve/main/MiniMax-H3-Pruned-Ref-Delta-Fused-r1024-comfy-int8-convrot-fc2bf16.safetensors) |

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

#### FastH3 DMD2 Distillation (FastVideo)

Official **data-free DMD2 few-step distillation** of MiniMax-H3 FL2VA by the FastVideo team (hao-ai-lab): 50-step base sampled in **4 steps** (`[999, 749, 500, 250]` ladder, cfg 1.0, guidance-distilled), joint video+audio, 768×1344 @ 124 frames. Diffusers-format full pipeline (only `transformer/` differs from base); student trained with VSA block-sparse attention (runnable dense). Preview status — v0.1 = step 1400, [v0.2 = step 2900/4000](https://huggingface.co/FastVideo/FastVideo-Minimax-FastH3-Preview-v0.2); quality still maturing on high-motion detail. MiniMax H3 Community License. A ComfyUI-ready LoRA extraction of this checkpoint by drozbay is listed under [Turbo](#checkpoints).

> ℹ️ Note: `Beidouqixing/MiniMax-H3-DMD2-4step` (previously circulated link) is dead (HF 404) — FastVideo's repos are the canonical DMD2 distills.

#### FastH3 & Specialized Quants (NVFP4 / Nunchaku)

Distilled / rotated / Nunchaku-packed checkpoints that need a **custom loader node** (not the stock diffusion-model loader). NVFP4 rows are Blackwell SM120 (native NVFP4); Nunchaku rows are W4A4/INT4 packs for [ComfyUI-Nunchaku](https://github.com/2damachines/ComfyUI-nunchaku).

| Checkpoint | Precision | Method | Size | Loader | Download |
| :--- | :---: | :--- | :---: | :--- | :--- |
| FastH3 4-step (pottokao) · rotated NVFP4 | ![nvfp4][badge-nvfp4] | Rotated NVFP4 | 12.8 GB | [H3RotNVFP4Loader](https://github.com/pottokao/H3-RotNVFP4-ComfyUI-Loader) | [![][gh-pottokao]](https://huggingface.co/pottokao/MiniMax-H3-FastH3-NVFP4-rotated/resolve/main/h3_fasth3_T1.safetensors) |
| FastH3 8-step (pottokao) · rotated NVFP4 · higher quality | ![nvfp4][badge-nvfp4] | Rotated NVFP4 | 12.5 GB | [H3RotNVFP4Loader](https://github.com/pottokao/H3-RotNVFP4-ComfyUI-Loader) | [![][gh-pottokao]](https://huggingface.co/pottokao/MiniMax-H3-NVFP4-rotated/resolve/main/h3_base_T1.safetensors) |
| FastVideo INT8→NVFP4 (LoboForge) | ![nvfp4][badge-nvfp4] | NVFP4 | 14.5 GB | NVFP4 (Blackwell SM120) | [![][gh-LoboForge]](https://huggingface.co/LoboForge/minimax-h3-fastvideo-nvfp4/resolve/main/minimax_h3_fastvideo_vsa_datafree_1300step_4step_nvfp4.safetensors) |
| Nunchaku-Lite NVFP4 (rootonchair) | ![nvfp4][badge-nvfp4] | Nunchaku W4A4 | 19.4 GB | [ComfyUI-Nunchaku](https://github.com/2damachines/ComfyUI-nunchaku) | [![][gh-rootonchair]](https://huggingface.co/rootonchair/MiniMax-H3-nunchaku-lite-nvfp4) |
| Nunchaku-Lite INT4 (rootonchair) | ![int4][badge-int4] | Nunchaku W4A4 | 18.4 GB | [ComfyUI-Nunchaku](https://github.com/2damachines/ComfyUI-nunchaku) | [![][gh-rootonchair]](https://huggingface.co/rootonchair/MiniMax-H3-nunchaku-lite-int4) |

#### VDN-H3 (Video DeltaNet)

**Video DeltaNet** — a hybrid-attention architecture that adds a constant-cost **linear-attention (Video Delta Attention) branch** plus two small LoRA adapters on top of the MiniMax-H3 backbone, replacing quadratic long-range attention so inference cost grows *linearly* with clip length. Plug-and-play: the branch + adapters merge into the backbone at inference without touching backbone weights. The 8-step DMD stage (`stage-dmd-step-250`) runs near-lossless vs dense H3. Reference impl: [OpenVDN/vdn-minimax-h3](https://github.com/OpenVDN/vdn-minimax-h3) (Apache-2.0); weights under the MiniMax H3 Community License (excludes EU/UK/Korea/US).

* **[OpenVDN/vdn-minimax-h3](https://huggingface.co/OpenVDN/vdn-minimax-h3)** — reference weights (~82 GB): `h3-base/` MiniMax-H3 backbone (transformer + video/audio VAEs, ~72 GB) plus two stages — `stage-b-step-2000` (linear branch + default adapter) and `stage-dmd-step-250` (8-step DMD: linear branch + default + turbo adapters).
* **[t8star/Vdn-Minimax-H3-Comfy](https://huggingface.co/t8star/Vdn-Minimax-H3-Comfy)** — ComfyUI-ready VDN bundle. Key files: `minimax_h3_fl2va_int8_convrot.safetensors` (34.0 GB), `minimax_h3_fl2va_pruned_int8_convrot.safetensors` (21.0 GB), `qwen3vl_32b_minimax_h3_nvfp4_awq.safetensors` text encoder (15.7 GB, NVFP4 AWQ), video VAE fp16 (5.2 GB), audio VAE fp32 (0.61 GB), plus the stage-dmd adapters (default 334 MB / turbo 851 MB / turbo_pruned_curve_fl2va 1.15 GB) and 4.28 GB linear branch.
* **[drbaph/vdn-minimax-h3-int8-convrot-comfyui](https://huggingface.co/drbaph/vdn-minimax-h3-int8-convrot-comfyui)** — pre-quantized `stage-dmd-step-250` INT8 ConvRot (Comfy Kitchen) for ComfyUI-VDN-H3: `linear_branch/model_int8_convrot_comfyui.safetensors` (2.30 GB int8, was 4.28 GB bf16) + `adapters/default` (334 MB) + `adapters/turbo` (851 MB); stage ~3.4 GB. Requires ComfyUI-VDN-H3 v1.3.0+.
* **[Saganaki22/ComfyUI-VDN-H3](https://github.com/Saganaki22/ComfyUI-VDN-H3)** — native ComfyUI node (port of OpenVDN, not a fork) that applies the VDN hybrid-attention patches as runtime model patches; no ComfyUI core changes, zero new deps. See the node table.

#### Notes

* **t8star Ref2VA patchin HF 1.02** — experimental weight modification (not a quant): +2% on 2×2 spatial HF patch in the video-input projection. Tests showed weak HF agent gain; "oily/waxy" look not confirmed removed. [Repo](https://huggingface.co/t8star/minimax_h3_ref2va_patchin_hf102). (31.70 GB, INT8 ConvRot, listed in the Ref2VA table above with `*(patchin)*` label.)
* **DmitryDB/MiniMax-H3-INT8-Lean-ConvRot** is the same repo as **DmitryDB/MiniMax-H3-ComfyUI-Quants** (merged/rebranded by the author). Both names resolve to the same files.
* **DmitryDB/MiniMax-H3-INT8-Lean-ConvRot-Dynamic-Time-Separate-QKV** is the same repo as **DmitryDB/MiniMax-H3-DynTime-sQKV**. Both names resolve to the same files.
* **Winnougan/MiniMax-H3-INT4_Convrot_ComfyUI** also includes a matching quantized text encoder: [`qwen3vl_32b_minimax_h3-w4a8_convrot.safetensors`](https://huggingface.co/Winnougan/MiniMax-H3-INT4_Convrot_ComfyUI/resolve/main/qwen3vl_32b_minimax_h3-w4a8_convrot.safetensors).
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

<p id="enc-heretic" align="center">· · · · · · · · · · · · · ·</p>

### ▣ Qwen3-VL-32B Ultra-Heretic (Uncensored)

Built from [`llmfan46/Qwen3-VL-32B-Instruct-ultra-uncensored-heretic`](https://huggingface.co/llmfan46/Qwen3-VL-32B-Instruct-ultra-uncensored-heretic) by [ethanfel](https://huggingface.co/ethanfel). Includes a MiniMax-H3 conditioning encoder (language layers 0–49 + vision tower) and an optional prompt-enhancement tail (layers 50–63 + LM head). The "Heretic" lineage bypasses alignment/restriction layers in the text encoder so MiniMax-H3 receives the most faithful prompt embeddings.

| Model Name | Precision | Size | Download |
| :--- | :---: | :---: | :---: |
| `qwen3vl_32b_heretic` (conditioning encoder) | ![int8][badge-int8] | 24.55 GB | [![][gh-ethanfel]](https://huggingface.co/ethanfel/Qwen3-VL-32B-Ultra-Heretic-MiniMax-H3-ComfyUI-INT8-ConvRot/resolve/main/qwen3vl_32b_minimax_h3_ultra_uncensored_heretic_int8_convrot.safetensors) |
| `qwen3vl_32b_heretic` (generation tail 50–63) | ![int8][badge-int8] | 7.09 GB | [![][gh-ethanfel]](https://huggingface.co/ethanfel/Qwen3-VL-32B-Ultra-Heretic-MiniMax-H3-ComfyUI-INT8-ConvRot/resolve/main/qwen3vl_32b_minimax_h3_generation_tail_50_63_int8_convrot.safetensors) |

*The generation tail is loaded temporarily by the [ComfyUI-MiniMax-H3-Guide](https://github.com/ethanfel/ComfyUI-MiniMax-H3-Guide) node for prompt enhancement, then unloaded. Requires the connected standard MiniMax-H3 CLIP (layers 0–49).*


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

<p id="lora" align="center">◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆</p>

## ▓ LoRA

### ▣ Styles

* SexGod1979
  * [PinkFluffyBunny](https://huggingface.co/SexGod1979/PinkFluffyBunny-MiniMax-H3) - Pink fluffy bunny style LoRA in pruned + unpruned variants (rank 128/256/512). Maximum pink achieved at 0.5 strength on pruned int8 model. Alpha quality. (2.31 GB · pruned-v1 rank128)
  * [PinkCherry](https://huggingface.co/SexGod1979/PinkCherry_MiniMax-H3) - High-quality furry rabbits, rainbows, and cherry blossoms. No guardrails altered. Alpha v0.3 (pruned int8, 14 GB checkpoint). Iterated alpha 0.1→0.5.
  * [NaughtyTimes](https://huggingface.co/SexGod1979/NaughtyTimes_MiniMax-H3) - NSFW style LoRA for MiniMax-H3.

* ssjenforcer191
  * [Homelander](https://huggingface.co/ssjenforcer191/Homelander_Minimax_H3_experimental) - Character LoRA for The Boys' Homelander. Triggerword `HeroHomelander` (optionally append `wearing red leather gloves`). Experimental. (296 MB)

* [Playtime-AI/Minimax_H3-Mila_Kunis](https://huggingface.co/Playtime-AI/Minimax_H3-Mila_Kunis) - Character LoRA of actress Mila Kunis (`MM-H3 - Mila Kunis v1.70.safetensors`, 155 MB pruned). Ships a sample audio clip; minimal card (Apache-2.0).

* [Playtime-AI/Minimax_H3-Sydney_Sweeney](https://huggingface.co/Playtime-AI/Minimax_H3-Sydney_Sweeney) - Character LoRA of actress Sydney Sweeney (`MM-H3 - Sydney Sweeney.safetensors`, 155 MB). Same pattern as Mila Kunis: ships a sample clip, minimal card (Apache-2.0).

* [Playtime-AI/Minimax_H3-Salma_Hayek](https://huggingface.co/Playtime-AI/Minimax_H3-Salma_Hayek) - Character LoRA of actress Salma Hayek (`MM-H3 - Salma Hayek.safetensors`, 155 MB). Same series as above; sample clip included, minimal card (Apache-2.0).

* [Playtime-AI/Minimax_H3-Jennifer_Connelly](https://huggingface.co/Playtime-AI/Minimax_H3-Jennifer_Connelly) - Character LoRA of actress Jennifer Connelly (`MM-H3 - Jennifer Connelly.safetensors`, 155 MB). Same Playtime-AI series; sample clip included, minimal card (Apache-2.0).

* [Playtime-AI/Minimax_H3-Margot_Robbie](https://huggingface.co/Playtime-AI/Minimax_H3-Margot_Robbie) - Character LoRA of actress Margot Robbie (`MM-H3 - Margot Robbie.safetensors`, 155 MB). Same series as above; sample clip included, minimal card (Apache-2.0).

* [Playtime-AI/Minimax_H3-Zendaya](https://huggingface.co/Playtime-AI/Minimax_H3-Zendaya) - Character LoRA of actress Zendaya (`MM-H3 - Zendaya.safetensors`, 155 MB). Same Playtime-AI series; sample clip included, minimal card (Apache-2.0).

* [Playtime-AI/Minimax_H3-Dolly_Parton](https://huggingface.co/Playtime-AI/Minimax_H3-Dolly_Parton) - Character LoRA of singer Dolly Parton (`MM-H3 - Dolly Parton v1.1.safetensors`, 155 MB). Same series as above; sample clip included, minimal card (Apache-2.0).

* [Playtime-AI/Minimax_H3-Sadie_S](https://huggingface.co/Playtime-AI/Minimax_H3-Sadie_S) - Character LoRA of actress Sadie Sink (`MM-H3 - Sadie Sink.safetensors`, 155 MB). Same series as above; sample clip included, minimal card (Apache-2.0).

* [Playtime-AI/Minimax_H3-Anya_Taylor_Joy](https://huggingface.co/Playtime-AI/Minimax_H3-Anya_Taylor_Joy) - Character LoRA of actress Anya Taylor-Joy (`MM-H3 - Anya Taylor Joy.safetensors`, 155 MB). Same series as above; sample clip included, minimal card (Apache-2.0).

* [Playtime-AI/Minimax_H3-Megan_Fox](https://huggingface.co/Playtime-AI/Minimax_H3-Megan_Fox) - Character LoRA of actress Megan Fox (`MM-H3 - Megan Fox v1.1.safetensors`, 155 MB). Same series as above; sample clip included, minimal card (Apache-2.0).

* [Playtime-AI/Minimax_H3-Ariana_Grande](https://huggingface.co/Playtime-AI/Minimax_H3-Ariana_Grande) - Character LoRA of singer Ariana Grande (`MM-H3 - Ariana Grande.safetensors`, 155 MB). Same series as above; sample clip included, minimal card (Apache-2.0).

* [Playtime-AI/Minimax_H3-Kiernan_Shipka](https://huggingface.co/Playtime-AI/Minimax_H3-Kiernan_Shipka) - Character LoRA of actress Kiernan Shipka (`MM-H3 - Kiernan Shipka.safetensors`, 155 MB). Same Playtime-AI series as above; sample clip included, minimal card (Apache-2.0).
* [Playtime-AI/Minimax_H3-Millie_Bobby_Brown](https://huggingface.co/Playtime-AI/Minimax_H3-Millie_Bobby_Brown) - Character LoRA of actress Millie Bobby Brown (`MM-H3 - Millie Bobby Brown.safetensors`, 155 MB). Same series as above; sample clip included, minimal card (Apache-2.0).
* [Playtime-AI/Minimax_H3-Milly_Alcock](https://huggingface.co/Playtime-AI/Minimax_H3-Milly_Alcock) - Character LoRA of actress Milly Alcock (`MM-H3 - Milly Alcock.safetensors`, 155 MB). Same series as above; sample clip included, minimal card (Apache-2.0).
* [Playtime-AI/Minimax_H3-The_Dude-Jeff_Bridges](https://huggingface.co/Playtime-AI/Minimax_H3-The_Dude-Jeff_Bridges) - Character LoRA of Jeff Bridges as "The Dude" (The Big Lebowski) (`MM-H3 - The Dude.safetensors`, 155 MB). Same Playtime-AI series as above; sample clip included, minimal card (Apache-2.0).

* JOKER141
  * [MiniMax-H3-Combat-Base-V2](https://huggingface.co/JOKER141/MiniMax-H3-Combat-Base-V2) - **Combat / action base v2** — combat, action, and dialogue motion LoRA for H3 (`H3_Combat_V2.safetensors`, 155 MB pruned). Ships 2 workflow JSONs.
  * [MiniMax-H3-General-Motion-Continuity-Repair](https://huggingface.co/JOKER141/MiniMax-H3-General-Motion-Continuity-Repair) - **General motion-continuity repair** — general-purpose motion-support LoRA (not combat-only): running, sports, dance, acrobatics, character interaction, combat, and weapon motion. Targets the sub-second "dropped-chain" moments — sudden slow-motion, missing action transitions, abnormal limb trajectories, broken interactions — rather than uniformly amplifying motion; A/B gains are largest exactly where the base model starts to struggle. Optional trigger `bunny_crisp_motion`. Recommended strength: ≈0.9 standalone · 0.5–0.7 stage-1 paired with the Combat LoRA above (Combat supplies speed/impact, this corrects continuity/coordination/prompt-following) · 0.2–0.3 on the stage-2 refine pass (higher over-stabilizes and dulls motion). (`Motion_Repair.safetensors`, 155 MB)

* [KennethFal/vh5tape-vhs-lora-minimax-h3](https://huggingface.co/KennethFal/vh5tape-vhs-lora-minimax-h3) - **VHS / retro 1980s** — VHS/analog retro video style LoRA (`vh5tape.safetensors` ~131 MB, plus a `vh5tape-comfyui` variant); ships sample clips. MiniMax H3 Community License.

* [prithivMLmods/MiniMax-H3-Facial-Realism-CloseUp](https://huggingface.co/prithivMLmods/MiniMax-H3-Facial-Realism-CloseUp) - **Facial realism / close-up** — face-realism and close-up portrait LoRA (`minimax-h3-facial-realism-closeup-cp2000.safetensors`, 75 MB). MiniMax H3 Community License.

* SexGod1979 — AfterMidnight
  * [AfterMidnight-MiniMax-H3-NSFW](https://huggingface.co/SexGod1979/AfterMidnight-MiniMax-H3-NSFW) - ⚠️ **Contains explicit / NSFW content.** "AfterMidnight" Ref2VA NSFW style LoRA family (rank 64): `sexytime` v1 / v1.1 / v1.2 and `softer` v1. Apache-2.0. Also mirrored byte-identical at [sasimi/AfterMidnight-MiniMax-H3-NSFW](https://huggingface.co/sasimi/AfterMidnight-MiniMax-H3-NSFW).

| Variant | Size | Download |
| :--- | :---: | :--- |
| `AfterMidnight_ref2va_h3_sexytime_rank64-v1.2.safetensors` | 1.11 GB | [![][gh-SexGod1979]](https://huggingface.co/SexGod1979/AfterMidnight-MiniMax-H3-NSFW/resolve/main/AfterMidnight_ref2va_h3_sexytime_rank64-v1.2.safetensors) |
| `AfterMidnight_ref2va_h3_sexytime_rank64_v1.1.safetensors` | 1.11 GB | [![][gh-SexGod1979]](https://huggingface.co/SexGod1979/AfterMidnight-MiniMax-H3-NSFW/resolve/main/AfterMidnight_ref2va_h3_sexytime_rank64_v1.1.safetensors) |
| `AfterMidnight_ref2va_h3_sexytime_rank64_v1.safetensors` | 1.11 GB | [![][gh-SexGod1979]](https://huggingface.co/SexGod1979/AfterMidnight-MiniMax-H3-NSFW/resolve/main/AfterMidnight_ref2va_h3_sexytime_rank64_v1.safetensors) |
| `AfterMidnight_ref2va_h3_softer_rank64_v1.safetensors` | 1.11 GB | [![][gh-SexGod1979]](https://huggingface.co/SexGod1979/AfterMidnight-MiniMax-H3-NSFW/resolve/main/AfterMidnight_ref2va_h3_softer_rank64_v1.safetensors) |

* [matlod/minimax-h3-turnaround](https://huggingface.co/matlod/minimax-h3-turnaround) - **Contact-Sheet diffusion** — one reference image + one instruction → five coherent, progressively rotated views of the same subject in a single pass. A character turnaround from one photo (~10 s at 512², ~57 s at 1024²). Uses H3's timeline as a slot axis. (60 MB each: 1024-cont/s600, 512/s1500, 512-instruct/s400)

* EllaPriest45
  * [MinimaxH3_Actions](https://huggingface.co/EllaPriest45/MinimaxH3_Actions/tree/main) - ⚠️ **Contains explicit / NSFW content.** Collection of NSFW action LoRAs for MiniMax-H3 (T2V/I2V/R2V). Includes motion-specific LoRAs with trigger words and strength recommendations. See the repo for the full list. (reference only)
  * [MinimaxH3_Characters](https://huggingface.co/EllaPriest45/MinimaxH3_Characters/tree/main) - ⚠️ **Contains explicit / NSFW content.** Character LoRA collection for MiniMax-H3 (e.g. Aunt Cass, Baldur's Gate 3 Party Pack, Judy Hopps). Browse at your own discretion; not enumerated with per-file downloads here.
  * [MinimaxH3_Styles](https://huggingface.co/EllaPriest45/MinimaxH3_Styles/tree/main) - ⚠️ **Contains explicit / NSFW content.** Style LoRA collection for MiniMax-H3 with previews and config text; significant NSFW/nude portion (anime, digicam, Playboy styles). Browse at your own discretion; not enumerated with per-file downloads here.

* [Hearmeman/minimax-h3-loras](https://huggingface.co/Hearmeman/minimax-h3-loras/tree/main) - ⚠️ **Contains explicit / NSFW content.** LoRA collection for MiniMax-H3 (repo tagged NSFW; MiniMax H3 Community License). Browse at your own discretion; not enumerated with per-file downloads here.

* [fal/research-mini-max-h3-realism-people-lora](https://huggingface.co/fal/research-mini-max-h3-realism-people-lora) - Realism LoRA for natural-looking people in everyday scenarios. Trained by fal on diverse photo data. (125 MB)

* [orangesouth/MinimaxH3CinematicRealism](https://huggingface.co/orangesouth/MinimaxH3CinematicRealism) - **Cinematic Realism** style LoRA ("真实电影质感" / real film texture, V0.1) for MiniMax-H3 — adds a grounded, photographic cinematic look. Ships a Chinese prompt-preset `.json` plus plugin/usage notes; no model card. (`Minimax H3真实电影质感V0.1.safetensors`, 309 MB pruned).

* [Inner-Reflections/MiniMax-H3-Looping-Sketch-Anime](https://huggingface.co/Inner-Reflections/MiniMax-H3-Looping-Sketch-Anime) - Looping anime-style sketch LoRA. Hand-drawn 2D outlines, flat colors, white outline. Strength 0.75–1.25; pair with a Turbo LoRA for higher strength. (569 MB)

* [suryatmodulus/studio-1939-old-animation-lora-minimax-h3](https://huggingface.co/suryatmodulus/studio-1939-old-animation-lora-minimax-h3) - **STUDIO 1939** — golden-age hand-painted animation style: gouache backgrounds with visible brushwork, warm celluloid palettes, classical character animation. Trained on a curated selection from a public-domain 1939 animated feature; two flavors from the same run — `light` (r16, painterly/storybook) and `strong` (r64, full cel with bold flat-shaded characters). Trigger `gulliv3r,` at prompt start; prompt expansion off; scale 1.0 for full look, 0.4–0.8 to blend under modern art direction; works 21:9 / 16:9 / 4:3. Character consistency via frozen verbatim character descriptions. By Lovis Odin ([@OdinLovis](https://x.com/OdinLovis)). (65.6 MB light r16 · 262 MB strong r64)

* [nikdevs/minimax-h3-loras](https://huggingface.co/nikdevs/minimax-h3-loras) - ⚠️ **Contains explicit / NSFW content.** Curated MiniMax-H3 LoRA collection (styles + characters). Browse at your own discretion; not enumerated with per-file downloads here.

* [DiffSynth-Studio/MiniMax-H3-LoRA-LineartAnime](https://huggingface.co/DiffSynth-Studio/MiniMax-H3-LoRA-LineartAnime) - **Anime video line-art colorization** — feeds a line-art video as a reference and generates fully colored anime output from it (Ref2VA video-reference workflow). Apache-2.0. (1.26 GB)

* Jojocodex
  * [minimax-h3-wushu-action-lora](https://huggingface.co/Jojocodex/minimax-h3-wushu-action-lora) - **Wushu / martial-arts action** — trains H3 to generate human martial-arts motion (punches, kicks, spins, staff techniques), focused on body physics. Trigger by action description (e.g. `a martial artist performing punches and kicks in fast combat`); no fixed trigger word. ai-toolkit, rank 16, 2000 steps, 512 / 90 frames @ 24fps; pruned + full safetensors. ComfyUI users load the `_pruned` variant at strength 0.8–1.0; compatible with the Turbo LoRA (adaln_proj trimmed, 417 keys). Base-model use is under the MiniMax H3 Community License. (155 MB pruned · 310 MB full)
  * [minimax-h3-spatial-physics-lora](https://huggingface.co/Jojocodex/minimax-h3-spatial-physics-lora) - **Spatial & physics (objects)** — teaches H3 object physics (collision, stacking, falling, occlusion) via pure spatial+physics captions; complements the wushu LoRA, which covers body motion. No fixed trigger word — describe object motion directly. Trained on CLEVRER / WISA / PhyCo-Kubric (700 clips); ai-toolkit, rank 16. ComfyUI users load `_pruned` at 0.8–1.0; stacks with the Turbo LoRA. (155 MB pruned · 310 MB full)
  * [minimax-h3-yunjing-lora](https://huggingface.co/Jojocodex/minimax-h3-yunjing-lora) - **Camera-movement (yunjing) control** — cinematic camera-movement control (push in/out, orbit, tracking, handheld) via the `yunjing` trigger word. 12 movement types trained (handheld / pull / dolly best-covered; pan / crane / 360° weakly covered). ai-toolkit, rank 32, 1000 steps; pruned + full. ComfyUI users load `_pruned` at 0.8–1.0; stacks with the Turbo LoRA (6–8 steps, Euler, Beta). (310 MB pruned · 620 MB full)
  * [minimax-h3-Camera-Motion-lora](https://huggingface.co/Jojocodex/minimax-h3-Camera-Motion-lora) - **Dedicated camera-motion LoRA (v1, 1000 steps)** — broader camera-movement control for H3, shipped with a `camera_motion_Prompt Library.md` of ready-made motion prompts. Separate, dedicated camera-motion training from the `yunjing` LoRA (use one or the other per shot). ai-toolkit, pruned safetensors. ComfyUI users load `_pruned` at 0.8–1.0; stacks with the Turbo LoRA. (155 MB pruned)
  * [wushu-action-v7-minimax-h3-fl2va-ref2va-lora](https://huggingface.co/Jojocodex/wushu-action-v7-minimax-h3-fl2va-ref2va-lora) - **Wushu / martial-arts action v7** — expanded FL2VA + Ref2VA wushu training with several pruned builds: NO-ADALN (~310 MB), adaln (~620 MB), musubi (~596 MB), ref2va (~310/620 MB). Ships 2 workflow JSONs + 招式TAGS清单.md (movement TAG list).

* vpakarinen
  * [insta-tiktok-aesthetics-h3-lora](https://huggingface.co/vpakarinen/insta-tiktok-aesthetics-h3-lora) - **Insta / TikTok aesthetics** — aesthetic style LoRA for MiniMax-H3 targeting the polished, high-contrast "Instagram / TikTok" look (skin smoothing, vibrant grade, trendy framing). (310 MB pruned)
  * [better-human-motion-h3-lora](https://huggingface.co/vpakarinen/better-human-motion-h3-lora) - **Better human motion** — motion-quality LoRA for MiniMax-H3 improving the naturalism and coherence of human movement (gait, gesture, weight shift). (310 MB pruned)

* [rzgar/minimax-h3_fl2v_8Step_motion_enhancer](https://huggingface.co/rzgar/minimax-h3_fl2v_8Step_motion_enhancer) - ⚠️ **Contains explicit / NSFW content.** **FL2VA 8-step motion enhancer** — anatomy / motion enhancer LoRA built on LightX2V's 8-step distilled FL2VA; amplifies motion intensity and anatomical detail at low step counts. NSFW-oriented. (1.96 GB)

### ▣ Experimental / Other

* [bghira/minimax-h3-anyflow-wip](https://huggingface.co/bghira/minimax-h3-anyflow-wip) - SimpleTuner WIP LoRA checkpoints (steps 200/300/400/500 + EMA). WIP research builds; not production-tuned.

* [ethanfel/MiniMax-H3-Pruned-Ref2VA-Delta-LoRAs-Experimental](https://huggingface.co/ethanfel/MiniMax-H3-Pruned-Ref2VA-Delta-LoRAs-Experimental) - **Highly experimental, mechanically extracted adapters** — randomized-SVD approximations of the weight difference between pruned FL2VA and Ref2VA checkpoints. Not trained as LoRAs, not generation-tested. Explore behavior transfer in either direction. (ranks 256/512/1024, BF16)

* [Kijai/MiniMax-H3-experimental loras](https://huggingface.co/Kijai/MiniMax-H3-experimental/tree/main/loras) - Experimental rank-256 BF16 LoRA capturing the FL2VA↔Ref2VA difference (same class as ethanfel's). No confirmed use case yet. (2.40 GB)

* [DIE2025/MiniMaxH3Loras](https://huggingface.co/DIE2025/MiniMaxH3Loras) - ![no description][badge-noinfo] Three unnamed style LoRAs (B, Spicy, V) of equal size. No README; use at own discretion. (310 MB each)

| Variant | Size | Download |
| :--- | :---: | :--- |
| `MiniMaxB.safetensors` | 310 MB | [![][gh-DIE2025]](https://huggingface.co/DIE2025/MiniMaxH3Loras/resolve/main/MiniMaxB.safetensors) |
| `MiniMaxSpicy.safetensors` | 310 MB | [![][gh-DIE2025]](https://huggingface.co/DIE2025/MiniMaxH3Loras/resolve/main/MiniMaxSpicy.safetensors) |
| `MiniMaxV.safetensors` | 310 MB | [![][gh-DIE2025]](https://huggingface.co/DIE2025/MiniMaxH3Loras/resolve/main/MiniMaxV.safetensors) |

* [adehong/minimax-h3-ntt-lora](https://huggingface.co/adehong/minimax-h3-ntt-lora) - ![no description][badge-noinfo] "NTT" v2 LoRA in three ranks (128 / 256 / 512). No model card; purpose and trigger words undocumented — use at own discretion.

| Variant | Size | Download |
| :--- | :---: | :--- |
| `ntt-v2-rank128.safetensors` | 1.12 GB | [![][gh-adehong]](https://huggingface.co/adehong/minimax-h3-ntt-lora/resolve/main/ntt-v2-rank128.safetensors) |
| `ntt-v2-rank256.safetensors` | 2.24 GB | [![][gh-adehong]](https://huggingface.co/adehong/minimax-h3-ntt-lora/resolve/main/ntt-v2-rank256.safetensors) |
| `ntt-v2-rank512.safetensors` | 4.48 GB | [![][gh-adehong]](https://huggingface.co/adehong/minimax-h3-ntt-lora/resolve/main/ntt-v2-rank512.safetensors) |

* [NTU-yiwen/awm-minimax-h3-new1344-lora-checkpoints](https://huggingface.co/NTU-yiwen/awm-minimax-h3-new1344-lora-checkpoints) - **CWM System-Chat LoRA adapters** — five selected LoRA adapters from 1344×768 q4 System-Chat training runs on MiniMax-H3 Ref2VA. Each adapter has 600 LoRA tensors for 200 target modules; supports inference + LoRA warm-start (no optimizer-level resume). Research release; manifest.json carries byte sizes, checksums and training steps. (2.39 GB each, BF16)

| Variant | Size | Download |
| :--- | :---: | :--- |
| `dynamic_continuation_2e5_to_1e6` (step2160) | 2.39 GB | [![][gh-NTU-yiwen]](https://huggingface.co/NTU-yiwen/awm-minimax-h3-new1344-lora-checkpoints/resolve/main/q4_system_chat/dynamic_continuation_2e5_to_1e6/minimax-h3-new1344-q4-system-chat-dynamic-human-nodes-continuation-strict-step960-2ep-warmup100-cosine2e5to1e6-fa2-a100i-restart-v1-step00002160.safetensors) |
| `dynamic_continuation_7e6_to_1e6` | 2.39 GB | [![][gh-NTU-yiwen]](https://huggingface.co/NTU-yiwen/awm-minimax-h3-new1344-lora-checkpoints/resolve/main/q4_system_chat/dynamic_continuation_7e6_to_1e6/minimax-h3-new1344-q4-system-chat-dynamic-human-nodes-continuation-strict-2ep-warmup50-cosine7e6to1e6-fa3-v1.safetensors) |
| `dynamic_fresh_1ep_2e5_to_1e6` (step960) | 2.39 GB | [![][gh-NTU-yiwen]](https://huggingface.co/NTU-yiwen/awm-minimax-h3-new1344-lora-checkpoints/resolve/main/q4_system_chat/dynamic_fresh_1ep_2e5_to_1e6/minimax-h3-new1344-q4-system-chat-dynamic-human-nodes-fresh-official-1ep-warmup50-cosine2e5to1e6-fa3-v1-step00000960.safetensors) |
| `rigid_3ep_1e5_to_1e6` | 2.39 GB | [![][gh-NTU-yiwen]](https://huggingface.co/NTU-yiwen/awm-minimax-h3-new1344-lora-checkpoints/resolve/main/q4_system_chat/rigid_3ep_1e5_to_1e6/minimax-h3-new1344-q4-system-chat-fresh-official-3ep-warmup100-cosine1e5to1e6-fa3-v1.safetensors) |
| `rigid_3ep_2e5_to_1e6` | 2.39 GB | [![][gh-NTU-yiwen]](https://huggingface.co/NTU-yiwen/awm-minimax-h3-new1344-lora-checkpoints/resolve/main/q4_system_chat/rigid_3ep_2e5_to_1e6/minimax-h3-new1344-q4-system-chat-fresh-official-3ep-warmup100-cosine2e5to1e6-fa3-v1.safetensors) |

* [MATLOWAI/MiniMax-H3-Motion-Adapter](https://huggingface.co/MATLOWAI/MiniMax-H3-Motion-Adapter) - **Motion adapter (pilot, r16)** — a small rank-16 BF16 LoRA that improves the de-rope pass in ComfyUI-MAINodes on fast motion: reduces frame-by-frame advance/snap alternation and over-production, and transfers to both FL2VA and Ref2VA graphs (one file). Trained bf16 (rank 16, alpha 16). MIT for the adapter weights; base model use is under the MiniMax H3 Community License. Load with a stock `LoraLoaderModelOnly` at strength 1.0 on the de-rope pass only. (63 MB)

* [mvp-lab/MiniMax-H3-RAVEN-Streaming-LoRA](https://huggingface.co/mvp-lab/MiniMax-H3-RAVEN-Streaming-LoRA) - **RAVEN: real-time autoregressive video extrapolation** — turns MiniMax-H3 into a causal streaming generator that extrapolates each chunk from previously generated content (4-NFE preview) instead of denoising one bidirectional clip. Academic preview (Imperial College London); the released weight is undertrained (limited texture) but validates the full RAVEN training→generation pipeline. Single PEFT LoRA adapter, `r=128` / `lora_alpha=128`; 192 frames @ 768×1376, 24 fps, causal chunking `sink=2 / window=2`. Training/inference/eval code in [mvp-ai-lab/RAVEN](https://github.com/mvp-ai-lab/RAVEN). MiniMax H3 Community License. (≈5.1 GB)

* [DANNY621/H3-World](https://huggingface.co/DANNY621/H3-World) - **H3-World: interactive world model** — rank-32 (65.6M-param, 131 MB) interactive world-model LoRA on MiniMax-H3. Maps keyboard controls → language instructions → directed-attention routing so a scene responds to live input. Requires a directed-attention patch (the unmodified pipeline won't reproduce the behavior). Apache-2.0. (131 MB)<p id="nodes" align="center">◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆</p>

## ▓ ComfyUI Nodes

| Node | Author | Category | Description |
| :--- | :--- | :---: | :--- |
| [MiniMax H3 Hybrid Cond](https://github.com/kitsune123150/minimax-h3-hybrid-cond) | kitsune123150 | ![Conditioning][cat-cond] | Hybrid R2V + I2V conditioning in one payload. Outputs positive conditioning and AV latent with native audio. |
| [ComfyUI-H3-Multishot](https://github.com/jlucasmcrell/ComfyUI-H3-Multishot) | jlucasmcrell | ![Conditioning][cat-cond] | Multishot video+audio generation — N chained shots from one script, seam-clean master. Keyframes at any position, dual-format loader (safetensors + GGUF). |
| [ComfyUI-H3-Multishot-Advance](https://github.com/KursatAs/ComfyUI-H3-Multishot-Advance) | KursatAs | ![Conditioning][cat-cond] | Advance fork of jlucasmcrell's Multishot — small node surface, unified loader, centralized controls, plus a persistent **shot cache / project** layer that survives ComfyUI restarts (resume a multi-shot sequence from the first changed clip). |
| [ComfyUI MiniMax H3 Director](https://github.com/seesee75-commits/ComfyUI-MiniMaxH3-Director) | seesee75-commits | ![Conditioning][cat-cond] | Timeline editor with storyboard — drag media onto tracks, trim on a ruler, write a prompt per shot. Live sampling preview, retakes, shot chaining. |
| [ComfyUI MiniMax H3 Image Studio](https://github.com/astropuzzo/ComfyUI-MiniMax-H3-Image-Studio) | astropuzzo | ![Conditioning][cat-cond] | Image-first nodes for T2I, I2I, and reference editing. Arbitrary frame counts, resolution up to 64 MP, automatic still-frame scoring. |
| [ComfyUI-MiniMaxH3-Easy](https://github.com/nkxx188/ComfyUI-MiniMaxH3-Easy) | nkxx188 | ![Conditioning][cat-cond] | One compact workflow for T2V, I2V, first/last-frame, and reference video. Unified multi-media input with `@` references and inline dialogue blocks. |
| [H3 Motion Context](https://github.com/NikoDemon80/ComfyUI-H3-Motion-Context) | NikoDemon80 | ![Conditioning][cat-cond] | Chain H3 clips so motion and sound keep going across the cut. Feed clip A's last frames + audio in; clip B picks up where A left off — same motion, same audio. |
| [ComfyUI-H3-Motion-Context-MultiRef](https://github.com/seitanism/ComfyUI-H3-Motion-Context-MultiRef) | seitanism | ![Conditioning][cat-cond] | Feature-extended fork of NikoDemon80's Motion Context — adds MultiRef (multiple references), latent masking / AV noise-mask, V2V latent motion transfer (granular fractional denoise + de-rope), hard-preserved masked keyframes, and one-shot music-video chaining. GPL-3.0. |
| [ComfyUI MiniMax H3 Motion Director](https://github.com/j955229/ComfyUI-MiniMax-H3-Motion-Director) | j955229 | ![Conditioning][cat-cond] | Multi-segment motion director combining AIMixer Director's timeline + Motion Context chaining. Reference control across N segments. |
| [H3 Conditioning Cache](https://github.com/HEEEeeeeN/ComfyUI-H3-Conditioning-Cache) | HEEEeeeeN | ![Conditioning][cat-cond] | Conditioning cache + batch generation suite for H3 drama/short-drama production. Caches conditioning across shots, batch-generates episodes unattended. |
| [MAINodes](https://github.com/matlowai/ComfyUI-MAINodes) | matlowai | ![Conditioning][cat-cond] | Contact-Sheet diffusion (five views from one reference) + Motion Lab (test-time de-roping of fast-motion smearing: backflips, sword arcs, reversals). |
| [Fantastic MiniMax H3 Prompt Builder](https://github.com/Adudeguyman/ComfyUI-Fantastic-MiniMaxH3-PromptBuilder) | Adudeguyman | ![Prompt][cat-prompt] | Fillable prompt templates for every H3 mode with live guide-rule checking and a media loader that manages reference tags. |
| [MiniMax-H3 Prompt Enhancer T8](https://github.com/T8mars/comfyui-minimax-h3-prompt-enhancer-T8) | T8mars | ![Prompt][cat-prompt] | Multimodal prompt enhancer calling `doubao-seed-evolving`. Analyzes text, images, and video together. Supports all H3 modes, strict/balanced/creative, CN/EN output. |
| [MiniMaxH3 LatentUpscaler](https://github.com/Tr1dae/ComfyUI-MiniMaxH3_LatentUpscaler) | Tr1dae | ![Upscaling][cat-upscale] | Latent spatial upscaler for H3's `NestedTensor` AV latents. Re-noises video/audio for two-pass sampling, scales `minimax_refs`/`minimax_keyframes` conditioning. |
| [ComfyUI Video Tiler](https://github.com/maDcaDDie2000/comfyui-video-tiler) | maDcaDDie2000 | ![Upscaling][cat-upscale] | Memory-conscious video/image tiling with overlap tiles, gaps, and feather blending. Built for LTX 2.3 and MiniMax H3 tiled upscale workflows. Disk-backed mode for low-VRAM. |
| [H3 Latent Upscaler (Mamad8)](https://github.com/mamad8c/ComfyUI-H3-Latent-Upscaler-Mamad8) | mamad8c | ![Upscaling][cat-upscale] | Moves a clean H3 video latent to a 2× larger spatial latent grid very quickly. Not a conventional upscaler — output looks softer than input; the point is to get a 2× grid ready for a second pass. |
| [MiniMaxH3 Frame Infill](https://github.com/red-polo/ComfyUI-MiniMaxH3FrameInfill) | red-polo | ![Conditioning][cat-cond] | Experimental node to regenerate any frame interval of an existing H3 video. Patches ComfyUI's H3 internal implementation; pin your ComfyUI version. |
| [ComfyUI-SolAttn_triton](https://github.com/kijai/ComfyUI-SolAttn_triton) | kijai | ![Acceleration][cat-accel] | SolAttention Triton kernel for ComfyUI. Optimized attention computation for H3 and other Sol-Attn models. |
| [ComfyUI-sol-attn](https://github.com/Saganaki22/ComfyUI-sol-attn) | Saganaki22 | ![Acceleration][cat-accel] | Zero-copy Sol-Attn for SM89–SM120 with scheduled tau, graph preview, and feed-forward chunking. 1.14–1.44× vs SageAttention, −37% MLP peak VRAM on H3. |
| [ComfyUI-VDN-H3](https://github.com/Saganaki22/ComfyUI-VDN-H3) | Saganaki22 | ![Acceleration][cat-accel] | Native ComfyUI port of OpenVDN's Video DeltaNet — applies the hybrid-attention (Video Delta Attention linear branch + LoRA adapters) as runtime model patches, replacing quadratic long-range attention with a constant-cost recurrent state so cost scales linearly with clip length. Loads the OpenVDN / t8star / drbaph VDN weights; requires v1.3.0+. Apache-2.0. |
| [ComfyUI Spectrum MiniMax H3](https://github.com/xmarre/ComfyUI-Spectrum-MiniMax-H3) | xmarre | ![Acceleration][cat-accel] | Spectral feature forecasting — skips selected transformer evaluations via Chebyshev ridge regression. Adaptive scheduling with native fallbacks. |
| [ComfyUI-MiniMax-H3-RefDelta-Solver](https://github.com/xmarre/ComfyUI-MiniMax-H3-RefDelta-Solver) | xmarre | ![Acceleration][cat-accel] | Dedicated ER-SDE-derived sampler + beta-prior scheduler pair built for the author's [Pruned Ref-Delta Fused r1024 checkpoint](https://huggingface.co/xmarre/MiniMax-H3-Pruned-Ref-Delta-Fused-r1024-ComfyUI): measures the fused checkpoint's divergent intermediate trajectory in ER-SDE solver coordinates and smoothly gates history-dependent corrections per stage, with separate video/audio risk reduction. Nodes: **RefDelta Sampler** (SamplerCustomAdvanced-compatible; strict stock mode delegates to native `sample_er_sde`), **RefDelta Scheduler** (`r1024_provisional` rank profile; profile JSON only at runtime), and a dev-only **Reference Diagnostic** guider comparing fused vs genuine Ref2VA on identical inputs. ⚠️ Experimental — controls/profile not yet calibrated against same-state telemetry. Requires `ModelSamplingAV`; compatible with ComfyUI-Spectrum-MiniMax-H3 v0.2.18+. GPL-3.0-or-later. |
| [Herrgotts-H3-Infinite-Continuation-Suite](https://github.com/HerrgottMargott/Herrgotts-H3-Infinite-Continuation-Suite) | HerrgottMargott | ![Conditioning][cat-cond] | Freeze-aware, keyframe-anchored MiniMax H3 video continuation for ComfyUI — injects the previous clip's video+audio latent context into the next FL2VA segment, auto-detects H3's frozen tail for a safe handover, and stitches with a 4-frame video crossfade + 15 ms audio de-click. Experimental community project (GPL-3.0). |
| [ComfyUI-MiniMaxH3-Cache](https://github.com/lihaoyun6/ComfyUI-MiniMaxH3-Cache) | lihaoyun6 | ![Acceleration][cat-accel] | EasyCache-style cache node for H3. Patches ComfyUI core to cache and reuse transformer block computations across timesteps. |
| [ComfyUI-H3VAE_TRT](https://github.com/lihaoyun6/ComfyUI-H3VAE_TRT) | lihaoyun6 | ![Acceleration][cat-accel] | TensorRT VAE for H3 — compile the ONNX encoder / decoder from [MiniMax-H3-VAE-ONNX](https://huggingface.co/lihaoyun6/MiniMax-H3-VAE-ONNX) (a `w4a16_awq` decoder variant exists for <12 GB VRAM) into TRT engines, then encode/decode through them for up to 1.7× faster VAE. Nodes: **TRT VAE Compiler** (first use) + **TRT VAE Loader**; ONNX files go in `models/vae`. Apache-2.0. |
| [MiniMax H3 Block Cache T8](https://github.com/T8mars/comfyui-minimax-h3-blockcache-T8) | T8mars | ![Acceleration][cat-accel] | F1B0 block cache — computes Block 0 and reuses residual for Blocks 1–49 when audio/video are stable. Skips up to 49 of 50 blocks per step. |
| [TE-Speed-MiniMaxH3-OSS](https://github.com/HELPMEEADICE/TE-Speed-MiniMaxH3-OSS) | HELPMEEADICE | ![Acceleration][cat-accel] | Block-cache accelerator patching H3's 50-layer DiT loop. Reuses cached tail-block residuals when sigma delta is small. ~45% speedup at default settings. |
| [MiniMaxH3 Dual-Clock Euler Sampler](https://github.com/shuaixn/ComfyUI-MiniMaxH3DualClockSampler) | shuaixn | ![Acceleration][cat-accel] | Dual-clock Euler sampler for the Turbo LoRA — fixes audio crackling/noise at 4-step generation by running video and audio on separate schedules. |
| [ComfyUI-H3-AudioRefine](https://github.com/Adudeguyman/ComfyUI-H3-AudioRefine) | Adudeguyman | ![Acceleration][cat-accel] | Audio-only refinement pass for H3 packed AV latents: freezes the video stream of an already-sampled latent (e.g. a 4-step Turbo pass) and denoises just the audio for extra steps — via ComfyUI's native masked-inpaint path with a per-stream noise mask (video=0 preserve, audio=1 generate; video bit-identical at `video_denoise` 0). Nodes: all-in-one **Audio Refine Sampler** (`audio_denoise` 0.3–0.6 cleans noise floor, 1.0 regenerates against frozen video), composable **Audio Refine Mask**, and optional **Frozen Video Cache** (~5.7× faster cached steps on RTX 5090; ~10 GB memory). Example workflow included; refine branch runs without the Turbo LoRA to restore undistilled audio quality. MIT. |
| [ComfyUI-MiniMax-H3-PDD-Acc](https://github.com/Jalen-Brunson/ComfyUI-MiniMax-H3-PDD-Acc) | Jalen-Brunson | ![Acceleration][cat-accel] | Native ComfyUI support for the official 8-step **PDD (Parallel Decoding Distillation)** acceleration LoRAs from alibaba-pai — full audio+video in 8 (or 4) steps with **no CFG**. Loads the rank-64 trunk LoRA **plus** the specialized "head bank" (32 per-interval final-layer video/audio projection copies) that ordinary LoRA loaders silently drop. Nodes: **PDD Acc LoRA (Apply)** (diffusers→ComfyUI key conversion in memory, installs the head bank armed per step by sigma; params `nfe` 4/6/8, `lora_strength`, `head_strength`) and **PDD Acc Scheduler** (standalone SIGMAS emitter). Format auto-detection (alibaba-pai or pre-converted ComfyUI keys), pruned-checkpoint rebasing of adaln LoRA modules, fail-closed on off-envelope steps. Requires ComfyUI v0.33.0+; pair FL2VA PDD with fl2va UNET, Ref2VA with ref2va UNET; euler sampler, CFG 1.0, SigmaShift 12/3, and **do not** stack other distill LoRAs (turbo) or step-cache packs. Apache-2.0. |
| [minimax-h3-mlx](https://github.com/mrbizarro/minimax-h3-mlx) | mrbizarro | ![Port][cat-port] | Apple Silicon MLX port of the full H3 pipeline. AdaLN precompute drops 13B params at inference. Validated against the diffusers reference. |
| [ComfyUI-ClipProj](https://github.com/nicolab28/ComfyUI-ClipProj) | nicolab28 | ![Port][cat-port] | Swap a large text encoder for a small one via a learned linear projection. MiniMax H3 conditioning from 15.7 GB down to 5.2 GB. Proof of concept. |
| [ComfyUI MiniMax H3 Contex Loop](https://github.com/ethanfel/ComfyUI-MiniMaxH3-Contex-Loop) | ethanfel | ![Conditioning][cat-cond] | Turn one sampling body into a scene-by-scene production loop — each accepted scene carries motion + audio forward, saves a checkpoint, joins into final video without huge cumulative tensors. |
| [ComfyUI-H3-Prompt-IDE](https://github.com/ethanfel/ComfyUI-H3-Prompt-IDE) | ethanfel | ![Prompt][cat-prompt] | VS Code-inspired rich H3 prompt editor — Plain/Rich source toggle, strict H3 section validation (T2VA / I2VA / FL2VA / L2VA / Ref2VA / Edit-instruction), H3-aware completions with reference-label spacing, click-to-replace reference/speaker tokens, and tokenizer-native completion of `<d>`, `<|cutoff|>`, lyrics/caption markers. The companion **H3 Reference Inputs** node autogrows `<Picture 1>`–`<Picture 9>`, `<Video 1>`–`<Video 3>`, `<Audio 1>`–`<Audio 6>` sockets; plain `STRING` output wires into any H3 prompt input. Task-aware integration with the author's [ComfyUI-MiniMax-H3-Edit](https://github.com/ethanfel/ComfyUI-MiniMax-H3-Edit) encoder (Edit categories follow the encoder's mode; Room + object study needs Edit 0.11.0+). GPL-3.0; requires ComfyUI V3 node API + Autogrow support. |
| [ComfyUI MiniMax H3 LongMedia](https://github.com/vizart-vj/ComfyUI-MiniMax-H3-LongMedia) | vizart-vj | ![Acceleration][cat-accel] | Long single-pass video/audio generation with streamed Sol attention, compressed KV, adaptive VRAM guards, chunked MLP/final output. SAFE long-sequence optimizations for limited VRAM. |
| [ComfyUI MiniMaxH3 Hybrid Loader](https://github.com/scottmudge/ComfyUI_MinimaxH3HybridLoader) | scottmudge | ![Port][cat-port] | Load a checkpoint by merging selected tensor groups (e.g. `adaln_proj` only) from a ref2va overlay onto a fl2va base. Default preset preserves ref-conditioning pathway while keeping fl2va quality. |
| [ComfyUI MiniMax H3 Legacy Audio Sampling](https://github.com/starsFriday/ComfyUI-MiniMax-H3-LegacySampling) | starsFriday | ![Acceleration][cat-accel] | Restores the v0.30.0 audio sampling behavior after upgrading to ComfyUI v0.31.0. One model-patch node — no source modification. Fixes regressed audio (background noise, stereo stability, HF artifacts). |
| [ComfyUI-H3-FaceRefine](https://github.com/Carasibana/ComfyUI-H3-FaceRefine) | Carasibana | ![Face Refine][cat-face] | Face-refinement node for MiniMax H3 outputs — repair/enhance faces in generated video frames. |
| [ComfyUI-MiniMaxH3Mod](https://github.com/Luisacaotica/ComfyUI-MiniMaxH3Mod) | Luisacaotica | ![Conditioning][cat-cond] | No-training "RefMod" reference adapters for MiniMax H3 — compress reference images/videos into tiny `.safetensors` latent files reused like LoRAs without loading heavy references or training. Extract/Load/Apply nodes, folder and A/B-axis loaders, a standalone CLI, and strength/retention controls injected via the model's native conditioning path. |
| [ComfyUI MiniMax H3 Extender](https://github.com/tritant/ComfyUI_MiniMax_H3_Extender) | tritant | ![Conditioning][cat-cond] | Chains multiple H3 clips into one long continuous sequence, preserving motion, visual, and audio continuity. Combines Ref2VA conditioning, motion context, disk latent caching, dynamic image references (up to 9), audio reference support, per-clip prompt/seed/duration, clip validation, and seamless video/audio decoding with seam correction (H.264 / H.265 / FFV1 export). |
| [ComfyUI ALLinONE MiniMaxH3](https://github.com/LeonQ8/ComfyUI-ALLinONE-MinimaxH3) | LeonQ8 | ![Conditioning][cat-cond] | All-in-one MiniMax H3 node — T2V, I2V, R2V, audio drive (lip sync), keyframes, extend, chain (multi-clip continuation via H3 Motion Context), and an RTX/Seed2VR upscale hook in a single node. Ships searchable history, a library, and settings UI. Beta, GPL-3.0. |
| [ComfyUI Qwen H3 Prompt](https://github.com/chflame163/ComfyUI_Qwen_H3_Prompt) | chflame163 | ![Prompt][cat-prompt] | Generates H3 prompts inside ComfyUI with a local Qwen3.8-27B GGUF model (bundled llama-server, fully offline) plus the official MiniMax-H3 Skills. Routes modes (T2VA/I2VA/L2VA/FL2VA/Ref2VA) from image/video references, writes sound design, and supports think mode with per-reference image/video inputs. |
| [OpenH3-IR](https://github.com/ruashots/open-h3-ir) | ruashots | ![Prompt][cat-prompt] | Open-source, local implementation of MiniMax H3's Context-IR stage — compiles a plain-language sentence (with optional referenced media) into a structured, validated six-section H3 video brief that feeds ComfyUI's native H3 render nodes. Three nodes (Main, Media, Setup), a creativity-level dial, strict brief validation, and exact dialogue/reference-image binding via `@`-syntax prompts. |
| [MiniMax H3 Latent Upscaler](https://github.com/LBH-123-AI/ComfyUI_Minimax_h3_latent_Upscaler) | LBH-123-AI | ![Upscaling][cat-upscale] | Learned neural latent upscaler for H3's 24-channel VAE latents — upscales spatial resolution (1×–4×, continuous) in latent space via 2D/3D backbones, skipping the costly VAE decode/encode round-trip to accelerate high-res video gen and avoid ghosting. Pairs with the LBH-123-AI/Minimax_h3_latent_Upscaler checkpoint (weights auto-detected). Saves time, not VRAM. |
| [Comfyui-MMH3-UltimateUpscale](https://github.com/bbaudio-2025/Comfyui-MMH3-UltimateUpscale) | bbaudio-2025 | ![Upscaling][cat-upscale] | Single-node re-sampling (enhance/upscale) pass over a finished H3 AV latent **under tight VRAM**: temporal chunking (arbitrarily long clips) × spatial tiling (arbitrarily high res) with peak VRAM bounded to one tile; audio carried through untouched (never re-sampled). Two upscale modes per chunk — the H3 3D model-based upscaler (LBH-123-AI `minimax_h3_latent_upscaler_3d_*` checkpoints) or model-free latent interpolation — with frame-0 anchoring across chunks (`anchor_strength` 0.999), cross-fade temporal stitching, frozen overlap masks + masked write-back for seamless tile seams (linear/smoothstep/midpoint blends), per-piece time/spatial conditioning re-anchoring, and CPU offloading so H3 + upscaler never share VRAM. Nodes: `MMH3 Ultimate Upscale`, `Temporal/Spatial Split Params`, `Latent Upscale (with Model) Params`. Built on the author's [LatentSplit](https://github.com/bbaudio-2025/Comfyui-MiniMax-H3-LatentSplit) + LBH-123-AI's upscaler network. MIT. |
| [ComfyUI MiniMax H3 Studio](https://github.com/thaakeno/ComfyUI-MiniMax-H3-Studio) | thaakeno | ![Conditioning][cat-cond] | "H3 Studio" — turns H3 into a maintained ComfyUI image workflow: T2I, I2I, reference editing via one Director node, up to 9 ordered multi-references (`@Image1`–`@Image9`), LightX/PDD accelerated paths, smart Qwen3-VL prompt prep, YOLOv8 Face Refine, TAEH3 previews, and a Benchmark Lab. Alpha (MIT code). ⚠️ Not compatible with ComfyUI Nodes 2.0 yet. |
| [ComfyUI MiniMax H3 Sampler Unlimited](https://github.com/hradec/ComfyUI-MiniMax-H3-Sampler-Unlimited) | hradec | ![Acceleration][cat-accel] | Chunked replacement for `SamplerCustomAdvanced` (`SamplerCustomAdvanced-Unlimited`) that samples long H3 video/audio latents in chunks with native latent continuation — produces >15 s video and 2K on ~16 GB VRAM without loop workflows. Frame-accurate shot-prompt rewriting, accumulated live preview. |
| [ComfyUI MiniMax H3 Parallel](https://github.com/AesSedai/ComfyUI-MiniMaxH3-Parallel) | AesSedai | ![Acceleration][cat-accel] | Exact activation-only multi-GPU attention-head sharding for H3 Ref2VA — model/TE/VAE stay on the model GPU; helper GPUs receive packed INT8 Q/K/V head slices and return BF16 attention. Up to 4× peer-access CUDA GPUs (Comfy Kitchen INT8 attention); ~2× denoiser speedup at 4 GPUs with bit-identical output. |
| [ComfyUI MiniMax H3 SPEED](https://github.com/StanLukuvka/ComfyUI-MiniMax-H3-SPEED) | StanLukuvka | ![Acceleration][cat-accel] | Progressive-resolution (Spectral Progressive Diffusion / SPEED) sampler for H3's packed video+audio latent — replaces KSAMPLER + `SamplerCustomAdvanced` and denoises starting coarse (¼–½ res) then refines to full, cutting VRAM and wall-clock time. Presets (`half_then_full` default, `three_quarter_then_full`, `quarter_half_full`, `aggressive`, `quarter_half_3q_full`) trade speed vs mid-frequency detail. Requires the StanLukuvka/ComfyUI-MiniMax-H3 plugin (ComfyUI 0.32.0+). ⚠️ PolyForm Noncommercial 1.0.0 license. |
| [ComfyUI MiniMax H3 Keyframe Offset](https://github.com/asirusasr-maker/ComfyUI-MiniMax-H3-Keyframe-Offset) | asirusasr-maker | ![Conditioning][cat-cond] | Drop-in replacement for the stock MiniMax H3 Image-to-Video conditioning node, injecting `first_frame`/`last_frame` keyframes at **arbitrary frame indices** (not just start/end) so H3 freely generates motion between them. Plus an all-in-one text-to-audio node (conditioning → sampling → audio-VAE decode in one node; CFG hardcoded 1.0). 23 samplers / 9 schedulers, smart offset clamping, non-invasive in-memory `PackedLayout` patch. Apache-2.0. |
| [MaskVidExperiments](https://github.com/drozbay/MaskVidExperiments) | drozbay | ![Conditioning][cat-cond] | Video masking / inpainting utility — crops a stable region around a masked subject, processes it at high resolution inside a moving crop, then pastes it back without jitter or visible seams (naive per-frame crops jitter, which video models read as camera motion). Nodes: Subject Crop (stable by construction through mask noise/occlusions), Subject Uncrop (feathered paste-back), Mask Cleanup, Frame Range Mask, Mask To Latent Space (token grid e.g. 2×2 for MiniMax H3 → latent noise mask), Audio Mask To Latent, Differential Diffusion (Soft), Audio Mask Debug. GPL-3.0. Requires ComfyUI 0.15.0+. |
| [ComfyUI-MiniMaxRefPack](https://github.com/Hearmeman24/ComfyUI-MiniMaxRefPack) | Hearmeman24 | ![Prompt][cat-prompt] | Manages all 18 Ref2VA references from one node's own upload UI — preview, crop/trim and delete, with the tag H3 will actually use (`<Picture 2>`, `<Video 1>`, `<Audio 1>`) shown on every tile. Wire the 18 sockets plus `prompt` once and the graph never changes again. Writes the six-section H3 prompt for you via OpenRouter **or** any local OpenAI-compatible server (one-click discovery of Ollama / LM Studio / llama.cpp / vLLM, loopback-only), or passes your text straight through. Portable JSON configs, `standard`/`replacement`/`auto` registers, editable system prompt, and a `debug` output showing the exact request sent. MIT. |

### ▣ Special Stuff

* [keys-heretic-MiniMax-H3 sol-engine + speed upgrades + upscaler finish — Single DGX Spark](https://github.com/drowzeys/keys-heretic-MiniMax-H3-sol-engine-more-speed-upgrades-upscaler-finish-Single-DGX-Spark) by drowzeys - One-shot recipe for MiniMax-H3 on a single NVIDIA DGX Spark (GB10, sm_121): Sol-Engine ports, Ultra-Heretic TE, Spectrum forecasting, SageAttention, 0.5 MPix generate + RealESRGAN x2 finish. Includes formal benchmark ladder (1.55× vs dense stock).

* [h3.c (h3-metal)](https://github.com/antirez/h3.c) by antirez - Native C/Metal inference engine for Apple Silicon. Prompt-to-video/audio, first/last-frame, and Ref2VA references work end-to-end on M3/M5 Max. Interactive Iris-style session. Not a ComfyUI node — standalone binary.

* [h3-webui](https://github.com/AntaresAlice/h3-webui) by AntaresAlice - Self-hosted video-generation **web UI** on ComfyUI + MiniMax-H3: merged 3-view interface (Chat / Overview / Studio), workspaces, history, real step-level progress (WebSocket→SSE), reference reuse, and video continuation (last-frame → next first-frame). Native H3 audio out; Turbo-LoRA auto-match. Frontend native JS + aiohttp backend; MIT. Not a ComfyUI node — wraps your existing ComfyUI instance.

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
| [INT8 I2V (javano2608.13)](https://huggingface.co/javawock7618/comfy-MiniMax-H3-workflows/resolve/main/MiniMax_int8_I2V-javano2608.13.json) | javawock7618 | I2VA | INT8 low-VRAM image-to-video workflow. |
| [INT8 I2V (javano2608.14.1)](https://huggingface.co/javawock7618/comfy-MiniMax-H3-workflows/resolve/main/MiniMax_int8_I2V-javano2608.14.1.json) | javawock7618 | I2VA | INT8 low-VRAM image-to-video workflow (variant). |
| [INT8 I2V (javano2608.15)](https://huggingface.co/javawock7618/comfy-MiniMax-H3-workflows/resolve/main/MiniMax_int8_I2V-javano2608.15.json) | javawock7618 | I2VA | INT8 low-VRAM image-to-video workflow (variant). |
| [INT8 I2V (javano2608.17.3)](https://huggingface.co/javawock7618/comfy-MiniMax-H3-workflows/resolve/main/MiniMax_int8_I2V-javano2608.17.3.json) | javawock7618 | I2VA | INT8 low-VRAM image-to-video workflow (variant). |
| [INT8 I2V (javano2609.1)](https://huggingface.co/javawock7618/comfy-MiniMax-H3-workflows/resolve/main/MiniMax_int8_I2V-javano2609.1.json) | javawock7618 | I2VA | INT8 low-VRAM image-to-video workflow (variant). |
| [I2V](https://huggingface.co/StefanFalkok/Minimax_H3_Workflows/resolve/main/Minimax%20H3/Minimax%20H3%20I2V.json) | StefanFalkok | I2VA | Image-to-video graph with stock LoRA/standard nodes. |
| [I2V — Larryvrh Turbo](https://huggingface.co/StefanFalkok/Minimax_H3_Workflows/resolve/main/Minimax%20H3/Minimax%20H3%20I2V%20(with%20Larryvrh%20Turbo%20Nodes).json) | StefanFalkok | I2VA | I2V with the Larryvrh 4-step Turbo sampler node wired in. |
| [I2V — PDD-Acc 8-Steps Turbo](https://huggingface.co/StefanFalkok/Minimax_H3_Workflows/resolve/main/Minimax%20H3/Minimax%20H3%20I2V%20(with%20PDD-Acc%208-Steps%20Turbo%20Nodes).json) | StefanFalkok | I2VA | I2V with the Jalen-Brunson PDD-Acc 8-step turbo node. |
| [FL2V GGUF Workflow](https://huggingface.co/Abiray/MiniMax-H3-GGUF/resolve/main/minimax_fl2v_gguf_workflow.json) | Abiray | FL2VA | ComfyUI workflow for loading/running the GGUF-quantized FL2VA model. |
| [Video (generic API)](https://github.com/Comfy-Org/workflow_templates/blob/main/archived/api_hailuo_minimax_video.json) | Comfy-Org | Ref2VA | Official Comfy-Org generic API video template; archived. |
| [OrbitQuant Ref2VA API Workflow](https://huggingface.co/WaveCut/MiniMax-H3-OrbitQuant-W4A4/resolve/main/comfyui/workflows/MiniMax-H3-OrbitQuant-Ref2VA-api.json) | WaveCut | Ref2VA | API-prompt version of the OrbitQuant Ref2VA workflow. |
| [Ref2VA GGUF Workflow](https://huggingface.co/Abiray/MiniMax-H3-GGUF/resolve/main/minimax_ref2va_gguf_workflow.json) | Abiray | Ref2VA | ComfyUI workflow for the GGUF-quantized Ref2VA model. |
| [R2V — Auto Prompting + Reference Manager](https://github.com/Hearmeman24/ComfyUI-MiniMaxRefPack/blob/main/example_workflows/MiniMax%20R2V%20-%20Auto%20Prompting%20%2B%20Reference%20Manager.json) | Hearmeman24 | Ref2VA | All 18 references wired once; H3 prompt auto-written; preview out (RefPack node). |
| [R2V — Auto Prompt](https://github.com/Hearmeman24/comfyui-minimax/blob/master/workflows/MiniMax%20H3/MiniMax%20-%20R2V%20-%20Auto%20Prompt.json) | Hearmeman24 | Ref2VA | VLM writes the H3 prompt from references. |
| [R2V (video_minimax_h3_r2v)](https://github.com/Hearmeman24/comfyui-minimax/blob/master/workflows/MiniMax%20H3/video_minimax_h3_r2v.json) | Hearmeman24 | Ref2VA | Reference-to-video workflow (stock naming). |
| [INT8 R2V (javano2608.20.1)](https://huggingface.co/javawock7618/comfy-MiniMax-H3-workflows/resolve/main/MiniMax_int8_R2V-javano2608.20.1.json) | javawock7618 | Ref2VA | INT8 low-VRAM reference-to-video workflow. |
| [INT8 R2V (javano2608.22.1)](https://huggingface.co/javawock7618/comfy-MiniMax-H3-workflows/resolve/main/MiniMax_int8_R2V-javano2608.22.1.json) | javawock7618 | Ref2VA | INT8 low-VRAM reference-to-video workflow (variant). |
| [INT8 R2V (javano2608.23)](https://huggingface.co/javawock7618/comfy-MiniMax-H3-workflows/resolve/main/MiniMax_int8_R2V-javano2608.23.json) | javawock7618 | Ref2VA | INT8 low-VRAM reference-to-video workflow (variant). |
| [INT8 R2V (javano2608.25.4)](https://huggingface.co/javawock7618/comfy-MiniMax-H3-workflows/resolve/main/MiniMax_int8_R2V-javano2608.25.4.json) | javawock7618 | Ref2VA | INT8 low-VRAM reference-to-video workflow (variant). |
| [INT8 R2V (javano2609.1)](https://huggingface.co/javawock7618/comfy-MiniMax-H3-workflows/resolve/main/MiniMax_int8_R2V-javano2609.1.json) | javawock7618 | Ref2VA | INT8 low-VRAM reference-to-video workflow (variant). |
| [Ref2V](https://huggingface.co/StefanFalkok/Minimax_H3_Workflows/resolve/main/Minimax%20H3/Minimax%20H3%20Ref2V.json) | StefanFalkok | Ref2VA | Reference-to-video graph with stock nodes. |
| [Ref2V — PDD-Acc 8-Steps Turbo](https://huggingface.co/StefanFalkok/Minimax_H3_Workflows/resolve/main/Minimax%20H3/Minimax%20H3%20Ref2V%20(with%20PDD-Acc%208-Steps%20Turbo%20Nodes).json) | StefanFalkok | Ref2VA | Ref2V with the Jalen-Brunson PDD-Acc 8-step turbo node. |
| [Ref2V Prompt generator](https://huggingface.co/StefanFalkok/Minimax_H3_Workflows/resolve/main/Minimax%20H3/Minimax%20H3%20Ref2V%20Prompt%20generator.json) | StefanFalkok | Ref2VA | Writes the H3 prompt for reference-to-video from references. |
| [Music-Video — Long-Shot Latent-Mask (Base+Ref)](https://huggingface.co/RuneXX/Minimax-H3-Workflows/resolve/main/Music-Video/Minimax-H3_-_Music-Video_Long-Shot-Latent-Mask_Base-Ref.json) | RuneXX | Ref2VA | Music-video workflow: long single shot with latent masking, base + reference conditioning. |
| [Music-Video — Long-Shot Latent-Mask (Multi-Scene Ref)](https://huggingface.co/RuneXX/Minimax-H3-Workflows/resolve/main/Music-Video/Minimax-H3_-_Music-Video_Long-Shot-Latent-Mask_MultiScene-Ref.json) | RuneXX | Ref2VA | Music-video workflow: multi-scene reference conditioning with latent masking. |
| [V2V — Extend Any Video (latent masking)](https://huggingface.co/RuneXX/Minimax-H3-Workflows/resolve/main/Video-to-Video/Minimax-H3_-_V2V_Extend_Any_Video_latent_masking.json) | RuneXX | Ref2VA | Video-to-video extension of any source clip via latent masking. |
| [H3 Seamless Chain (CORE)](https://huggingface.co/joeygambino/MiniMax-H3-Multishot-Workflow/resolve/main/workflows/H3_Seamless_Chain_CORE.json) | joeygambino | Multi-shot | Core seamless multi-shot chaining graph (FL2VA/Ref2VA clips). |
| [H3 Seamless Chain v2](https://huggingface.co/joeygambino/MiniMax-H3-Multishot-Workflow/resolve/main/workflows/H3_Seamless_Chain_v2.json) | joeygambino | Multi-shot | Multi-shot chaining workflow (v2). |
| [H3 Extend Take](https://huggingface.co/joeygambino/MiniMax-H3-Multishot-Workflow/resolve/main/workflows/H3_Extend_Take.json) | joeygambino | Multi-shot | Clip extension / take workflow. |
| [H3 Keyframes](https://huggingface.co/joeygambino/MiniMax-H3-Multishot-Workflow/resolve/main/workflows/H3_Keyframes.json) | joeygambino | Multi-shot | Keyframe-conditioned chaining. |
| [Music-Video — Multi-Scene Shot-by-Shot](https://huggingface.co/RuneXX/Minimax-H3-Workflows/resolve/main/Music-Video/Minimax-H3_-_Music-Video_Multi-Scene_Shot-by-Shot.json) | RuneXX | Multi-shot | Music-video workflow that builds a multi-scene clip shot-by-shot. |
| [comfy-MiniMax-H3-workflows (pack)](https://huggingface.co/javawock7618/comfy-MiniMax-H3-workflows) | javawock7618 | Bundle | Full INT8 low-VRAM acceleration stack: INT8 + SageAttention + Spectrum + Lightx2v + Turbo + Motion Context + Latent Upscale + TTS (+ Music, Ref2Image utilities). |
| [INT8 TTS](https://huggingface.co/javawock7618/comfy-MiniMax-H3-workflows/resolve/main/MiniMax_int8_TTS-javano2608.1.json) | javawock7618 | Bundle | TTS audio workflow. |
| [Music3](https://huggingface.co/javawock7618/comfy-MiniMax-H3-workflows/resolve/main/extra/MiniMax-Music3-javano2608.1.json) | javawock7618 | Bundle | Music generation workflow. |
| [Ref2Image](https://huggingface.co/javawock7618/comfy-MiniMax-H3-workflows/resolve/main/extra/MiniMax_int8-Ref2Image-javano2608.2.json) | javawock7618 | Bundle | Reference-to-image utility. |
| [INT8 Bridge](https://huggingface.co/javawock7618/comfy-MiniMax-H3-workflows/resolve/main/MiniMax_int8_Bridge-javano2608.3.json) | javawock7618 | Bundle | INT8 low-VRAM clip-bridge / transition workflow. |
| [INT8 FR (Face Refine)](https://huggingface.co/javawock7618/comfy-MiniMax-H3-workflows/resolve/main/MiniMax_int8_FR-javano2608.4.json) | javawock7618 | Bundle | INT8 low-VRAM face-refine (FR) workflow. |
| [MiniMax-H3-Multishot-Workflow (pack)](https://huggingface.co/joeygambino/MiniMax-H3-Multishot-Workflow) | joeygambino | Bundle | ComfyUI-H3-Multishot node pack + multi-shot workflows + presenter demo. Apache-2.0. |

*Comfy-Org's original `templates/video_minimax_h3_*` T2V/I2V/R2V graphs were moved to `archived/` and are now API-based (Hailuo/Minimax API) templates — links above point to the archived JSONs. Abiray also ships a Ref2VA GGUF workflow (newly listed).*

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

[badge-bf16]: https://img.shields.io/badge/bf16-0077cc?style=flat-square
[badge-fp16]: https://img.shields.io/badge/fp16-0077cc?style=flat-square
[badge-fp8]: https://img.shields.io/badge/fp8-28a745?style=flat-square
[badge-mxfp8]: https://img.shields.io/badge/mxfp8-20c997?style=flat-square
[badge-fp32]: https://img.shields.io/badge/fp32-6c757d?style=flat-square
[badge-int8]: https://img.shields.io/badge/int8-17a2b8?style=flat-square
[badge-int4]: https://img.shields.io/badge/int4-ffc107?style=flat-square
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
