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

An FP32 build of the pruned H3 text encoder by [Felldude](https://huggingface.co/Felldude/QWEN_32B_Comfy_MinimaxH3_Pruned_FP32) — one 95.9 GB `model.safetensors` for maximum-fidelity conditioning on a large-VRAM box; most setups are better served by the INT8 / INT4 / GGUF encoders above.

| Model Name | Precision | Size | Download |
| :--- | :---: | :---: | :---: |
| `qwen3vl_32b_minimax_h3` · pruned | ![fp32][badge-fp32] | 95.9 GB | [![][gh-Felldude]](https://huggingface.co/Felldude/QWEN_32B_Comfy_MinimaxH3_Pruned_FP32/resolve/main/model.safetensors) |

### ▣ MXFP8 Text Encoder (intel-ai)

The same Intel auto-round **MXFP8** treatment applied to the Qwen3-VL text encoder, shipped in [intel-ai/MiniMax-H3-MXFP8-CT-AutoRound](https://huggingface.co/intel-ai/MiniMax-H3-MXFP8-CT-AutoRound) alongside the two quantized DiTs (see the [models tables](#quants)). Only the language-model linears are quantized; the vision tower, embeddings, norms and `lm_head` stay BF16. Diffusers-format, not a ComfyUI single-file.

| Model Name | Precision | Size | Download |
| :--- | :---: | :---: | :---: |
| `qwen3vl_32b_minimax_h3` · MXFP8 | ![mxfp8][badge-mxfp8] | 33.98 GB | [![][gh-intel-ai]](https://huggingface.co/intel-ai/MiniMax-H3-MXFP8-CT-AutoRound/resolve/main/FL2VA/text_encoder/model-00001-of-00007.safetensors) |

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

