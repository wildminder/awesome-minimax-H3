
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

