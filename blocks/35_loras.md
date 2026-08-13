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

* [nikdevs/minimax-h3-loras](https://huggingface.co/nikdevs/minimax-h3-loras) - ⚠️ **Contains explicit / NSFW content.** Curated MiniMax-H3 LoRA collection (styles + characters). Browse at your own discretion; not enumerated with per-file downloads here.

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

* [rzgar/minimax_h3_fl2v_lightx2v_4step_int8-convrot_comfy](https://huggingface.co/rzgar/minimax_h3_fl2v_lightx2v_4step_int8-convrot_comfy) - Int8-ConvRot‑quantized FL2V LightX2V Turbo adapters (4/8‑step) that patch the base MiniMax-H3 for faster T2V in ComfyUI. Requires the [ComfyUI-LoraInt8Loader](https://huggingface.co/rzgar/minimax_h3_fl2v_lightx2v_4step_int8-convrot_comfy/resolve/main/ComfyUI-LoraInt8Loader/ComfyUI-LoraInt8Loader.zip) node — stock ComfyUI LoRA loaders cannot dequantize the files. Apache-2.0. (991 MB each)

| Variant | Size | Download |
| :--- | :---: | :--- |
| `turbo_4step_v1.0` (768p, int8_convrot) | 991 MB | [![][gh-rzgar]](https://huggingface.co/rzgar/minimax_h3_fl2v_lightx2v_4step_int8-convrot_comfy/resolve/main/minimax_h3_fl2v_turbo_4step_v1.0_768p_comfyui_bf16_int8convrot.safetensors) |
| `turbo_8step_v1.0` (int8_convrot) | 991 MB | [![][gh-rzgar]](https://huggingface.co/rzgar/minimax_h3_fl2v_lightx2v_4step_int8-convrot_comfy/resolve/main/minimax_h3_fl2v_turbo_8step_v1.0_comfyui_bf16_int8convrot.safetensors) |
| `turbo_4step_v0.1` (lightx2v, int8_convrot) | 991 MB | [![][gh-rzgar]](https://huggingface.co/rzgar/minimax_h3_fl2v_lightx2v_4step_int8-convrot_comfy/resolve/main/minimax_h3_fl2v_lightx2v_turbo_4step_v0.1_comfy_int8convrot.safetensors) |

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