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
* [Prompt Tools](#prompt-tools)
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
| | ![int8][badge-int8] | ConvRot | 31.70 GB | [![][gh-Comfy--Org]](https://huggingface.co/Comfy-Org/MiniMax-H3/resolve/main/diffusion_models/minimax_h3_ref2va_int8_convrot.safetensors) ┊ [![][gh-t8star]](https://huggingface.co/t8star/minimax_h3_ref2va_patchin_hf102/resolve/main/minimax_h3_ref2va_patchin_hf102_T8.safetensors) *(patchin)* |
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

| Component | Precision | Size | Download |
| :--- | :---: | :---: | :--- |
| Video VAE | ![fp16][badge-fp16] | 4.85 GB | [![][gh-Comfy--Org]](https://huggingface.co/Comfy-Org/MiniMax-H3/resolve/main/vae/minimax_h3_video_vae_fp16.safetensors) |
| Audio VAE | ![fp32][badge-fp32] | 577 MB | [![][gh-Comfy--Org]](https://huggingface.co/Comfy-Org/MiniMax-H3/resolve/main/vae/minimax_h3_audio_vae_fp32.safetensors) |

#### FP8 VAE (dummy9996)

FP8-mixed quantized video VAE by [dummy9996](https://huggingface.co/dummy9996/minimax_h3_vae_fp8).

| Component | Precision | Size | Download |
| :--- | :---: | :---: | :--- |
| Video VAE | ![fp8][badge-fp8] | 2.60 GB | [![][gh-dummy9996]](https://huggingface.co/dummy9996/minimax_h3_vae_fp8/resolve/main/minimax_h3_video_vae_fp8mix.safetensors) |
| Audio VAE | ![bf16][badge-bf16] | 289 MB | [![][gh-dummy9996]](https://huggingface.co/dummy9996/minimax_h3_vae_fp8/resolve/main/minimax_h3_audio_vae_bf16.safetensors) |

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

<p id="lora" align="center">◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆</p>

## ▓ LoRA

### ▣ Styles

* SexGod1979
  * [PinkFluffyBunny](https://huggingface.co/SexGod1979/PinkFluffyBunny-MiniMax-H3) - Pink fluffy bunny style LoRA in pruned + unpruned variants (rank 128/256/512). Maximum pink achieved at 0.5 strength on pruned int8 model. Alpha quality. (2.31 GB · pruned-v1 rank128)
  * [PinkCherry](https://huggingface.co/SexGod1979/PinkCherry_MiniMax-H3) - High-quality furry rabbits, rainbows, and cherry blossoms. No guardrails altered. Alpha v0.3 (pruned int8, 14 GB checkpoint). Iterated alpha 0.1→0.5.
  * [NaughtyTimes](https://huggingface.co/SexGod1979/NaughtyTimes_MiniMax-H3) - NSFW style LoRA for MiniMax-H3.

* ssjenforcer191
  * [Homelander](https://huggingface.co/ssjenforcer191/Homelander_Minimax_H3_experimental) - Character LoRA for The Boys' Homelander. Triggerword `HeroHomelander` (optionally append `wearing red leather gloves`). Experimental. (296 MB)

* [matlod/minimax-h3-turnaround](https://huggingface.co/matlod/minimax-h3-turnaround) - **Contact-Sheet diffusion** — one reference image + one instruction → five coherent, progressively rotated views of the same subject in a single pass. A character turnaround from one photo (~10 s at 512², ~57 s at 1024²). Uses H3's timeline as a slot axis. (60 MB each: 1024-cont/s600, 512/s1500, 512-instruct/s400)

* [EllaPriest45/MinimaxH3_Actions](https://huggingface.co/EllaPriest45/MinimaxH3_Actions/tree/main) - Collection of NSFW action LoRAs for MiniMax-H3 (T2V/I2V/R2V). Includes motion-specific LoRAs with trigger words and strength recommendations. See the repo for the full list. (reference only)

* [fal/research-mini-max-h3-realism-people-lora](https://huggingface.co/fal/research-mini-max-h3-realism-people-lora) - Realism LoRA for natural-looking people in everyday scenarios. Trained by fal on diverse photo data. (125 MB)

* [Inner-Reflections/MiniMax-H3-Looping-Sketch-Anime](https://huggingface.co/Inner-Reflections/MiniMax-H3-Looping-Sketch-Anime) - Looping anime-style sketch LoRA. Hand-drawn 2D outlines, flat colors, white outline. Strength 0.75–1.25; pair with a Turbo LoRA for higher strength. (569 MB)

### ▣ Turbo (Acceleration LoRA)

4-step audio-video generation LoRAs — render joint video + synchronized stereo audio in 4 sampling steps instead of ~20 (~5× speedup). Early prototype; comfort zone for sharpness is 6–8 steps. For pruned checkpoints use the ComfyUI-converted variants; the original targets the full (non-pruned) FL2VA checkpoint and needs the [ComfyUI-MiniMax-H3-Turbo](https://github.com/Larryvrh/ComfyUI-MiniMax-H3-Turbo) sampler node.

* [larryvrh/MiniMax-H3-Turbo-Lora](https://huggingface.co/larryvrh/MiniMax-H3-Turbo-Lora) - The original Turbo LoRA by larryvrh. Recent additions: `turbo_4step_ckpt850` and `turbo_v4_step600` (EMA) variants. (744 MB)

| Variant | Size | Download |
| :--- | :---: | :---: |
| `turbo_4step` | 744 MB | [![][gh-larryvrh]](https://huggingface.co/larryvrh/MiniMax-H3-Turbo-Lora/resolve/main/minimax_h3_turbo_4step.safetensors) |
| `turbo_4step_ema` | 744 MB | [![][gh-larryvrh]](https://huggingface.co/larryvrh/MiniMax-H3-Turbo-Lora/resolve/main/minimax_h3_turbo_4step_ema.safetensors) |
| `turbo_4step_ckpt500` | 744 MB | [![][gh-larryvrh]](https://huggingface.co/larryvrh/MiniMax-H3-Turbo-Lora/resolve/main/minimax_h3_turbo_4step_ckpt500.safetensors) |
| `turbo_4step_ema_ckpt500` | 744 MB | [![][gh-larryvrh]](https://huggingface.co/larryvrh/MiniMax-H3-Turbo-Lora/resolve/main/minimax_h3_turbo_4step_ema_ckpt500.safetensors) |
| `turbo_4step_ckpt850` | 744 MB | [![][gh-larryvrh]](https://huggingface.co/larryvrh/MiniMax-H3-Turbo-Lora/resolve/main/minimax_h3_turbo_4step_ckpt850.safetensors) |
| `turbo_4step_ema_ckpt850` | 744 MB | [![][gh-larryvrh]](https://huggingface.co/larryvrh/MiniMax-H3-Turbo-Lora/resolve/main/minimax_h3_turbo_4step_ema_ckpt850.safetensors) |
| `turbo_v4_step600` | 744 MB | [![][gh-larryvrh]](https://huggingface.co/larryvrh/MiniMax-H3-Turbo-Lora/resolve/main/minimax_h3_turbo_v4_step600.safetensors) |
| `turbo_v4_step600_ema` | 744 MB | [![][gh-larryvrh]](https://huggingface.co/larryvrh/MiniMax-H3-Turbo-Lora/resolve/main/minimax_h3_turbo_v4_step600_ema.safetensors) |

*Experimental training checkpoints:*
[step 149](https://huggingface.co/larryvrh/MiniMax-H3-Turbo-Lora/resolve/main/experimental_step_149.bin) (10.17 GB) · [step 490](https://huggingface.co/larryvrh/MiniMax-H3-Turbo-Lora/resolve/main/experimental_step_490.bin) (10.17 GB) · [step 729](https://huggingface.co/larryvrh/MiniMax-H3-Turbo-Lora/resolve/main/experimental_step_729.bin) (10.17 GB) · [step 850](https://huggingface.co/larryvrh/MiniMax-H3-Turbo-Lora/resolve/main/experimental_step_850.bin) (10.17 GB) · [step 922](https://huggingface.co/larryvrh/MiniMax-H3-Turbo-Lora/resolve/main/experimental_step_922.bin) (10.17 GB) · v2 [step 298](https://huggingface.co/larryvrh/MiniMax-H3-Turbo-Lora/resolve/main/experimental_v2_step_298.bin) (7.26 GB) · v3 [step 300](https://huggingface.co/larryvrh/MiniMax-H3-Turbo-Lora/resolve/main/experimental_v3_step_300.bin) (10.17 GB) · v4 [step 150](https://huggingface.co/larryvrh/MiniMax-H3-Turbo-Lora/resolve/main/experimental_v4_step_150.bin) (10.17 GB) · v4 [step 600](https://huggingface.co/larryvrh/MiniMax-H3-Turbo-Lora/resolve/main/experimental_v4_step_600.bin) (10.17 GB) · v5 [step 600](https://huggingface.co/larryvrh/MiniMax-H3-Turbo-Lora/resolve/main/experimental_v5_step_600.bin) (10.17 GB)

* [drbaph/MiniMax-H3-Turbo-Lora-ComfyUI](https://huggingface.co/drbaph/MiniMax-H3-Turbo-Lora-ComfyUI) - ComfyUI pruned-model compatibility conversions of larryvrh's Turbo LoRA. For the pruned/curve-form MiniMax-H3 checkpoint. Includes two further-trained checkpoint-500 variants. (592 MB each)

| Variant | Size | Download |
| :--- | :---: | :---: |
| `turbo_4step_pruned` | 592 MB | [![][gh-drbaph]](https://huggingface.co/drbaph/MiniMax-H3-Turbo-Lora-ComfyUI/resolve/main/minimax_h3_turbo_4step_pruned_comfyui.safetensors) |
| `turbo_4step_ema_pruned` | 592 MB | [![][gh-drbaph]](https://huggingface.co/drbaph/MiniMax-H3-Turbo-Lora-ComfyUI/resolve/main/minimax_h3_turbo_4step_ema_pruned_comfyui.safetensors) |
| `turbo_4step_ckpt500_pruned` | 592 MB | [![][gh-drbaph]](https://huggingface.co/drbaph/MiniMax-H3-Turbo-Lora-ComfyUI/resolve/main/minimax_h3_turbo_4step_ckpt500_pruned_comfyui.safetensors) |
| `turbo_4step_ema_ckpt500_pruned` | 592 MB | [![][gh-drbaph]](https://huggingface.co/drbaph/MiniMax-H3-Turbo-Lora-ComfyUI/resolve/main/minimax_h3_turbo_4step_ema_ckpt500_pruned_comfyui.safetensors) |

* [Abiray/MiniMax-H3-Turbo-Lora-Pruned-ComfyUI](https://huggingface.co/Abiray/MiniMax-H3-Turbo-Lora-Pruned-ComfyUI) - ComfyUI-ready pruned-model Turbo LoRAs. Checkpoint-500 V1, checkpoint-600 V4 (+ EMA), and checkpoint-850 V1 — each 592 MB. Bundles a `Minimax_H3_turbo_workflow.json`.

| Variant | Size | Download |
| :--- | :---: | :---: |
| `turbo_4step_ckpt500_V1` | 592 MB | [![][gh-Abiray]](https://huggingface.co/Abiray/MiniMax-H3-Turbo-Lora-Pruned-ComfyUI/resolve/main/minimax_h3_turbo_4step_ckpt500_V1.safetensors) |
| `turbo_4step_ckpt600_V4` | 592 MB | [![][gh-Abiray]](https://huggingface.co/Abiray/MiniMax-H3-Turbo-Lora-Pruned-ComfyUI/resolve/main/minimax_h3_turbo_4step_ckpt600_V4.safetensors) |
| `turbo_4step_ckpt600_ema_V4` | 592 MB | [![][gh-Abiray]](https://huggingface.co/Abiray/MiniMax-H3-Turbo-Lora-Pruned-ComfyUI/resolve/main/minimax_h3_turbo_4step_ckpt600_ema_V4.safetensors) |
| `turbo_4step_ckpt850_V1` | 592 MB | [![][gh-Abiray]](https://huggingface.co/Abiray/MiniMax-H3-Turbo-Lora-Pruned-ComfyUI/resolve/main/minimax_h3_turbo_4step_ckpt850_V1.safetensors) |

* [lightx2v/Minimax-h3-Turbo](https://huggingface.co/lightx2v/Minimax-h3-Turbo) - Turbo LoRA distilled by `ModelTC` from [their repo](https://github.com/ModelTC/Minimax-H3-Turbo). The shared 4-step distil used by Kijai's ComfyUI conversions. (1.29 GB)

| Variant | Size | Download |
| :--- | :---: | :--- |
| `minimax_h3_fl2v_turbo_4step_v0.1` | 1.29 GB | [![][gh-lightx2v]](https://huggingface.co/lightx2v/Minimax-h3-Turbo/resolve/main/minimax_h3_fl2v_turbo_4step_v0.1.safetensors) |

* [joyfox/MiniMax-H3-Turbo](https://huggingface.co/joyfox/MiniMax-H3-Turbo) - Inference acceleration LoRA for 4-step Euler T2V and I2V on **BF16** FL2VA (not int8). LoRA only — pair with [Comfy-Org/MiniMax-H3](https://huggingface.co/Comfy-Org/MiniMax-H3) BF16 base. Includes bundled I2V workflow JSON and side-by-side comparison assets vs. lightx2v. (717 MB)

| Variant | Size | Download |
| :--- | :---: | :--- |
| `minimax_h3_fl2va_4step_lora` | 717 MB | [![][gh-joyfox]](https://huggingface.co/joyfox/MiniMax-H3-Turbo/resolve/main/minimax_h3_fl2va_4step_lora.safetensors) |

* [Kijai/MiniMax-H3_comfy](https://huggingface.co/Kijai/MiniMax-H3_comfy/tree/main/loras) - Kijai's ComfyUI conversion of the LightX2V Turbo LoRA, plus a resized avg-rank-21 BF16 variant.

| Variant | Download |
| :--- | :--- |
| `lightx2v_turbo_4step_v0.1` (ComfyUI) | [![][gh-Kijai]](https://huggingface.co/Kijai/MiniMax-H3_comfy/resolve/main/loras/minimax_h3_fl2v_lightx2v_turbo_4step_v0.1_comfy.safetensors) |
| `lightx2v_turbo_4step_v0.1` (resized avg-rank-21) | [![][gh-Kijai]](https://huggingface.co/Kijai/MiniMax-H3_comfy/resolve/main/loras/minimax_h3_fl2v_lightx2v_turbo_4step_v0.1_comfy_resized_avg_rank_21_bf16.safetensors) |

* [tutututututu/Tutu-MiniMax-H3-AudioVideo-20to8-NFE-LoRA](https://huggingface.co/tutututututu/Tutu-MiniMax-H3-AudioVideo-20to8-NFE-LoRA) - Research LoRA cutting MiniMax-H3 AV generation from 20 to 8 NFE (sampling function calls). ComfyUI + diffusers formats, three training steps (100/200/300).

| Variant | Download |
| :--- | :--- |
| step 100 (ComfyUI, BF16) | [![][gh-tutututututu]](https://huggingface.co/tutututututu/Tutu-MiniMax-H3-AudioVideo-20to8-NFE-LoRA/resolve/main/comfyui/tutu-t8-minimax-h3-av-20to8-nfe-lora-step000100-bf16-comfyui.safetensors) |
| step 200 (ComfyUI, BF16) | [![][gh-tutututututu]](https://huggingface.co/tutututututu/Tutu-MiniMax-H3-AudioVideo-20to8-NFE-LoRA/resolve/main/comfyui/tutu-t8-minimax-h3-av-20to8-nfe-lora-step000200-bf16-comfyui.safetensors) |
| step 300 (ComfyUI, BF16) | [![][gh-tutututututu]](https://huggingface.co/tutututututu/Tutu-MiniMax-H3-AudioVideo-20to8-NFE-LoRA/resolve/main/comfyui/tutu-t8-minimax-h3-av-20to8-nfe-lora-step000300-bf16-comfyui.safetensors) |

* [t8star/minimax-h3-4step-turbo-loras-comfyui-exp](https://huggingface.co/t8star/minimax-h3-4step-turbo-loras-comfyui-exp) - ComfyUI-adapted Turbo LoRAs. ⚠️ For the **int8_convrot** (non-pruned) model — requires the [dual-clock sampler](https://github.com/shuaixn/ComfyUI-MiniMaxH3DualClockSampler) or 8–10 steps to avoid audio crackle at 4-step. Euler sampler + beta scheduler. (744 MB)

| Variant | Download |
| :--- | :--- |
| `turbo_4step` (4步加速, ComfyUI) | [![][gh-t8star]](https://huggingface.co/t8star/minimax-h3-4step-turbo-loras-comfyui-exp/resolve/main/minimax_h3_turbo_4%E6%AD%A5%E5%8A%A0%E9%80%9F_comfyui.safetensors) |
| `turbo_4step_ema` (4步加速ema, ComfyUI) | [![][gh-t8star]](https://huggingface.co/t8star/minimax-h3-4step-turbo-loras-comfyui-exp/resolve/main/minimax_h3_turbo_4%E6%AD%A5%E5%8A%A0%E9%80%9Fema_comfyui.safetensors) |
| `turbo_v4_step600` (T8-convert) | [![][gh-t8star]](https://huggingface.co/t8star/minimax-h3-4step-turbo-loras-comfyui-exp/resolve/main/minimax_h3_turbo_v4_step600_comfyui_T8-convert.safetensors) |

* [t8star/minimax-h3-10Eros-Max-4step-turbo-loras-comfyui-exp](https://huggingface.co/t8star/minimax-h3-10Eros-Max-4step-turbo-loras-comfyui-exp) - 4-step Turbo LoRAs for the **10Eros_Max** finetuned checkpoint. ComfyUI format. Also includes `1.82 GB` compatibility versions for non-ComfyUI loaders. (758 MB each)

| Variant | Download |
| :--- | :--- |
| `turbo_4step` (10ErosMax, ComfyUI) | [![][gh-t8star]](https://huggingface.co/t8star/minimax-h3-10Eros-Max-4step-turbo-loras-comfyui-exp/resolve/main/minimax_h3_10eros_max_turbo_4%E6%AD%A5%E5%8A%A0%E9%80%9F_comfyui.safetensors) |
| `turbo_4step_ema` (10ErosMax, ComfyUI) | [![][gh-t8star]](https://huggingface.co/t8star/minimax-h3-10Eros-Max-4step-turbo-loras-comfyui-exp/resolve/main/minimax_h3_10eros_max_turbo_4%E6%AD%A5%E5%8A%A0%E9%80%9Fema_comfyui.safetensors) |

* [infosave/MiniMax-H3-Turbo-cmf](https://huggingface.co/infosave/MiniMax-H3-Turbo-cmf) - MiniMax-H3 + larryvrh Turbo in a single [CMF container](https://github.com/infosave2007/cmf): DiT, Qwen3-VL, video VAE decoder, audio vocoder, all memory-mapped. Runs on [cortiq](https://github.com/infosave2007/cortiq) — a Rust binary with no ML framework underneath. One-file deploy, no Python.

| Variant | Size | Download |
| :--- | :---: | :--- |
| `mmh3-turbo-q4tp.cmf` (full) | 25.20 GB | [![][gh-infosave]](https://huggingface.co/infosave/MiniMax-H3-Turbo-cmf/resolve/main/mmh3-turbo-q4tp.cmf) |
| `mmh3-turbo-fl2va-q4tp.cmf` (FL2VA-only) | 25.70 GB | [![][gh-infosave]](https://huggingface.co/infosave/MiniMax-H3-Turbo-cmf/resolve/main/mmh3-turbo-fl2va-q4tp.cmf) |
| `mmh3-turbo-fl2va-q2tp.cmf` (FL2VA-only, smaller) | 20.12 GB | [![][gh-infosave]](https://huggingface.co/infosave/MiniMax-H3-Turbo-cmf/resolve/main/mmh3-turbo-fl2va-q2tp.cmf) |

### ▣ Experimental / Other

* [bghira/minimax-h3-anyflow-wip](https://huggingface.co/bghira/minimax-h3-anyflow-wip) - SimpleTuner WIP LoRA checkpoints (steps 200/300/400/500 + EMA). WIP research builds; not production-tuned.

* [ethanfel/MiniMax-H3-Pruned-Ref2VA-Delta-LoRAs-Experimental](https://huggingface.co/ethanfel/MiniMax-H3-Pruned-Ref2VA-Delta-LoRAs-Experimental) - **Highly experimental, mechanically extracted adapters** — randomized-SVD approximations of the weight difference between pruned FL2VA and Ref2VA checkpoints. Not trained as LoRAs, not generation-tested. Explore behavior transfer in either direction. (ranks 256/512/1024, BF16)

* [Kijai/MiniMax-H3-experimental loras](https://huggingface.co/Kijai/MiniMax-H3-experimental/tree/main/loras) - Experimental rank-256 BF16 LoRA capturing the FL2VA↔Ref2VA difference (same class as ethanfel's). No confirmed use case yet. (2.40 GB)

* [DIE2025/MiniMaxH3Loras](https://huggingface.co/DIE2025/MiniMaxH3Loras) - ![no description][badge-noinfo] Three unnamed style LoRAs (B, Spicy, V) of equal size. No README; use at own discretion. (310 MB each)

| Variant | Size | Download |
| :--- | :---: | :--- |
| `MiniMaxB.safetensors` | 310 MB | [![][gh-DIE2025]](https://huggingface.co/DIE2025/MiniMaxH3Loras/resolve/main/MiniMaxB.safetensors) |
| `MiniMaxSpicy.safetensors` | 310 MB | [![][gh-DIE2025]](https://huggingface.co/DIE2025/MiniMaxH3Loras/resolve/main/MiniMaxSpicy.safetensors) |
| `MiniMaxV.safetensors` | 310 MB | [![][gh-DIE2025]](https://huggingface.co/DIE2025/MiniMaxH3Loras/resolve/main/MiniMaxV.safetensors) |<p id="nodes" align="center">◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆</p>

## ▓ ComfyUI Nodes

| Node | Author | Category | Description |
| :--- | :--- | :---: | :--- |
| [MiniMax H3 Hybrid Cond](https://github.com/kitsune123150/minimax-h3-hybrid-cond) | kitsune123150 | ![Conditioning][cat-cond] | Hybrid R2V + I2V conditioning in one payload. Outputs positive conditioning and AV latent with native audio. |
| [ComfyUI-H3-Multishot](https://github.com/jlucasmcrell/ComfyUI-H3-Multishot) | jlucasmcrell | ![Conditioning][cat-cond] | Multishot video+audio generation — N chained shots from one script, seam-clean master. Keyframes at any position, dual-format loader (safetensors + GGUF). |
| [ComfyUI MiniMax H3 Director](https://github.com/seesee75-commits/ComfyUI-MiniMaxH3-Director) | seesee75-commits | ![Conditioning][cat-cond] | Timeline editor with storyboard — drag media onto tracks, trim on a ruler, write a prompt per shot. Live sampling preview, retakes, shot chaining. |
| [ComfyUI MiniMax H3 Image Studio](https://github.com/astropuzzo/ComfyUI-MiniMax-H3-Image-Studio) | astropuzzo | ![Conditioning][cat-cond] | Image-first nodes for T2I, I2I, and reference editing. Arbitrary frame counts, resolution up to 64 MP, automatic still-frame scoring. |
| [ComfyUI-MiniMaxH3-Easy](https://github.com/nkxx188/ComfyUI-MiniMaxH3-Easy) | nkxx188 | ![Conditioning][cat-cond] | One compact workflow for T2V, I2V, first/last-frame, and reference video. Unified multi-media input with `@` references and inline dialogue blocks. |
| [H3 Motion Context](https://github.com/NikoDemon80/ComfyUI-H3-Motion-Context) | NikoDemon80 | ![Conditioning][cat-cond] | Chain H3 clips so motion and sound keep going across the cut. Feed clip A's last frames + audio in; clip B picks up where A left off — same motion, same audio. |
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
| [ComfyUI Spectrum MiniMax H3](https://github.com/xmarre/ComfyUI-Spectrum-MiniMax-H3) | xmarre | ![Acceleration][cat-accel] | Spectral feature forecasting — skips selected transformer evaluations via Chebyshev ridge regression. Adaptive scheduling with native fallbacks. |
| [Herrgotts-H3-Infinite-Continuation-Suite](https://github.com/HerrgottMargott/Herrgotts-H3-Infinite-Continuation-Suite) | HerrgottMargott | ![Conditioning][cat-cond] | Freeze-aware, keyframe-anchored MiniMax H3 video continuation for ComfyUI — injects the previous clip's video+audio latent context into the next FL2VA segment, auto-detects H3's frozen tail for a safe handover, and stitches with a 4-frame video crossfade + 15 ms audio de-click. Experimental community project (GPL-3.0). |
| [ComfyUI-MiniMaxH3-Cache](https://github.com/lihaoyun6/ComfyUI-MiniMaxH3-Cache) | lihaoyun6 | ![Acceleration][cat-accel] | EasyCache-style cache node for H3. Patches ComfyUI core to cache and reuse transformer block computations across timesteps. |
| [MiniMax H3 Block Cache T8](https://github.com/T8mars/comfyui-minimax-h3-blockcache-T8) | T8mars | ![Acceleration][cat-accel] | F1B0 block cache — computes Block 0 and reuses residual for Blocks 1–49 when audio/video are stable. Skips up to 49 of 50 blocks per step. |
| [TE-Speed-MiniMaxH3-OSS](https://github.com/HELPMEEADICE/TE-Speed-MiniMaxH3-OSS) | HELPMEEADICE | ![Acceleration][cat-accel] | Block-cache accelerator patching H3's 50-layer DiT loop. Reuses cached tail-block residuals when sigma delta is small. ~45% speedup at default settings. |
| [MiniMaxH3 Dual-Clock Euler Sampler](https://github.com/shuaixn/ComfyUI-MiniMaxH3DualClockSampler) | shuaixn | ![Acceleration][cat-accel] | Dual-clock Euler sampler for the Turbo LoRA — fixes audio crackling/noise at 4-step generation by running video and audio on separate schedules. |
| [minimax-h3-mlx](https://github.com/mrbizarro/minimax-h3-mlx) | mrbizarro | ![Port][cat-port] | Apple Silicon MLX port of the full H3 pipeline. AdaLN precompute drops 13B params at inference. Validated against the diffusers reference. |
| [ComfyUI-ClipProj](https://github.com/nicolab28/ComfyUI-ClipProj) | nicolab28 | ![Port][cat-port] | Swap a large text encoder for a small one via a learned linear projection. MiniMax H3 conditioning from 15.7 GB down to 5.2 GB. Proof of concept. |
| [ComfyUI MiniMax H3 Contex Loop](https://github.com/ethanfel/ComfyUI-MiniMaxH3-Contex-Loop) | ethanfel | ![Conditioning][cat-cond] | Turn one sampling body into a scene-by-scene production loop — each accepted scene carries motion + audio forward, saves a checkpoint, joins into final video without huge cumulative tensors. |
| [ComfyUI MiniMax H3 LongMedia](https://github.com/vizart-vj/ComfyUI-MiniMax-H3-LongMedia) | vizart-vj | ![Acceleration][cat-accel] | Long single-pass video/audio generation with streamed Sol attention, compressed KV, adaptive VRAM guards, chunked MLP/final output. SAFE long-sequence optimizations for limited VRAM. |
| [ComfyUI MiniMaxH3 Hybrid Loader](https://github.com/scottmudge/ComfyUI_MinimaxH3HybridLoader) | scottmudge | ![Port][cat-port] | Load a checkpoint by merging selected tensor groups (e.g. `adaln_proj` only) from a ref2va overlay onto a fl2va base. Default preset preserves ref-conditioning pathway while keeping fl2va quality. |
| [ComfyUI MiniMax H3 Legacy Audio Sampling](https://github.com/starsFriday/ComfyUI-MiniMax-H3-LegacySampling) | starsFriday | ![Acceleration][cat-accel] | Restores the v0.30.0 audio sampling behavior after upgrading to ComfyUI v0.31.0. One model-patch node — no source modification. Fixes regressed audio (background noise, stereo stability, HF artifacts). |

### ▣ Special Stuff

* [keys-heretic-MiniMax-H3 sol-engine + speed upgrades + upscaler finish — Single DGX Spark](https://github.com/drowzeys/keys-heretic-MiniMax-H3-sol-engine-more-speed-upgrades-upscaler-finish-Single-DGX-Spark) by drowzeys - One-shot recipe for MiniMax-H3 on a single NVIDIA DGX Spark (GB10, sm_121): Sol-Engine ports, Ultra-Heretic TE, Spectrum forecasting, SageAttention, 0.5 MPix generate + RealESRGAN x2 finish. Includes formal benchmark ladder (1.55× vs dense stock).

* [h3.c (h3-metal)](https://github.com/antirez/h3.c) by antirez - Native C/Metal inference engine for Apple Silicon. Prompt-to-video/audio, first/last-frame, and Ref2VA references work end-to-end on M3/M5 Max. Interactive Iris-style session. Not a ComfyUI node — standalone binary.


<p id="prompt-tools" align="center">◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆</p>

## ▓ Prompt Tools

Standalone prompt-expansion tools (not ComfyUI nodes). These produce validated H3-oriented text; they do not submit generation jobs.

* [Omni-Rewriter](https://github.com/WayneJin0918/Omni-Rewriter) - Open agentic prompt-expansion harness with a typed H3 profile: schema → Writer draft → deterministic validate → bounded repair → dialect render. Expand ≠ generate. Apache-2.0.

<p id="guides" align="center">◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆</p>

## ▓ Guides & Tutorials

### ▣ Official Guides

* [Video Prompt Writing Guide (Base)](https://huggingface.co/MiniMaxAI/MiniMax-H3/blob/main/docs/VIDEO_PROMPT_WRITING_GUIDE_base_en.md) - Official MiniMax-H3 prompt writing guide for base (FL2VA) mode. Covers prompt structure, camera language, scene composition, and best practices for text-to-video and image-to-video generation.
* [Video Prompt Writing Guide (Reference)](https://huggingface.co/MiniMaxAI/MiniMax-H3/blob/main/docs/VIDEO_PROMPT_WRITING_GUIDE_ref_en.md) - Official MiniMax-H3 prompt writing guide for reference (Ref2VA) mode. Covers multi-modal reference inputs, image/video/audio reference handling, and prompt construction for omni-reference generation.

### ▣ ComfyUI Tutorials

* [ComfyUI MiniMax-H3 Tutorial](https://docs.comfy.org/tutorials/video/minimax/minimax-h3) - Official ComfyUI documentation tutorial for MiniMax-H3 setup and usage.
* [MiniMax H3 Day-0 Support in ComfyUI](https://blog.comfy.org/p/minimax-h3-day-0-support-in-comfyui) - ComfyUI blog post covering open weights, native audio, 2K video output, and local execution on a 3060.


<p id="wf" align="center">◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆</p>

## ▓ Workflow & Technical Notes

<a id="wf-comfyui"></a>

### ❖ ComfyUI

Official ComfyUI workflow templates for MiniMax-H3:

* [Text-to-Video (T2V)](https://github.com/Comfy-Org/workflow_templates/blob/main/templates/video_minimax_h3_t2v.json)
* [Image-to-Video (I2V)](https://github.com/Comfy-Org/workflow_templates/blob/main/templates/video_minimax_h3_i2v.json)
* [Reference-to-Video (R2V)](https://github.com/Comfy-Org/workflow_templates/blob/main/templates/video_minimax_h3_r2v.json)

### ❖ OrbitQuant

* [OrbitQuant T2VA Workflow](https://huggingface.co/WaveCut/MiniMax-H3-OrbitQuant-W4A4/resolve/main/comfyui/workflows/MiniMax-H3-OrbitQuant-T2VA.json) - Ready-to-import ComfyUI workflow for the OrbitQuant W4A4 quantization. Derived from Comfy-Org's bundled T2V workflow.
* [OrbitQuant T2VA API Workflow](https://huggingface.co/WaveCut/MiniMax-H3-OrbitQuant-W4A4/resolve/main/comfyui/workflows/MiniMax-H3-OrbitQuant-T2VA-api.json) - API prompt version of the T2VA workflow.
* [OrbitQuant Ref2VA API Workflow](https://huggingface.co/WaveCut/MiniMax-H3-OrbitQuant-W4A4/resolve/main/comfyui/workflows/MiniMax-H3-OrbitQuant-Ref2VA-api.json) - API prompt version of the Ref2VA workflow.

### ❖ Abiray

* [MiniMax H3 FL2V GGUF Workflow](https://huggingface.co/Abiray/MiniMax-H3-GGUF/resolve/main/minimax_fl2v_gguf_workflow.json) - ComfyUI workflow for loading and running the GGUF quantized FL2VA model.

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
