
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
| [Turbo v4 8-step T2VA](https://huggingface.co/BennyDaBall/MiniMax-H3-Workflows/resolve/main/MiniMax_H3_Turbo_v4_8step_T2VA_BennyDaBall.json) | BennyDaBall | T2VA | Text-to-video+audio with the Turbo v4 LoRA at 1.0; core nodes only. |
| [Live Wallpaper Prompt generator](https://huggingface.co/StefanFalkok/Minimax_H3_Workflows/resolve/main/Minimax%20H3/Minimax%20H3%20Live%20Wallpaper%20Prompt%20generator%20%28Copy%29.json) | StefanFalkok | T2VA | Writes looping live-wallpaper prompts. |
| [Image-to-Video (I2V)](https://github.com/Comfy-Org/workflow_templates/blob/main/archived/api_hailuo_minimax_i2v.json) | Comfy-Org | I2VA | Official Comfy-Org template — API-based; archived. |
| [I2V — Custom Prompt](https://github.com/Hearmeman24/comfyui-minimax/blob/master/workflows/MiniMax%20H3/MiniMax%20-%20I2V%20-%20Custom%20Prompt.json) | Hearmeman24 | I2VA | You write the prompt; image input + Turbo LoRA + preview. |
| [I2V — Auto Prompt](https://github.com/Hearmeman24/comfyui-minimax/blob/master/workflows/MiniMax%20H3/MiniMax%20-%20I2V%20-%20Auto%20Prompt.json) | Hearmeman24 | I2VA | VLM writes the H3 prompt from one line + image. |
| [INT8 I2V (javano2610.2.1)](https://huggingface.co/javawock7618/comfy-MiniMax-H3-workflows/resolve/main/MiniMax_int8_I2V-javano2610.2.1.json) | javawock7618 | I2VA | INT8 low-VRAM image-to-video workflow — FLF/I2V with Extend, ControlNet Union V2V, Latent Upscaler, and LightVAE. Current build. |
| [I2V](https://huggingface.co/StefanFalkok/Minimax_H3_Workflows/resolve/main/Minimax%20H3/Minimax%20H3%20I2V.json) | StefanFalkok | I2VA | Image-to-video graph with stock LoRA/standard nodes. |
| [Open-H3 Face Region — prompt to 2K](https://huggingface.co/BennyDaBall/MiniMax-H3-Workflows/resolve/main/OpenH3_FaceRegion_Prompt_to_2K_BennyDaBall.json) | BennyDaBall | I2VA | Draft at 768p, then a 2560×1440 regenerate that keeps faces and lip sync. ⚠️ Needs Face Region, Open-H3-Regenerate and LBH latent upscaler nodes. |
| [RIFE VFI Interpolation](https://huggingface.co/StefanFalkok/Minimax_H3_Workflows/resolve/main/Minimax%20H3/RIFE%20VFI%20Interpolation.json) | StefanFalkok | Utility | Frame-interpolation post-pass. |
| [FL2V GGUF Workflow](https://huggingface.co/Abiray/MiniMax-H3-GGUF/resolve/main/minimax_fl2v_gguf_workflow.json) | Abiray | FL2VA | ComfyUI workflow for loading/running the GGUF-quantized FL2VA model. |
| [Multi-Reference Fight (wushu)](https://huggingface.co/Jojocodex/wushu-action-v7-minimax-h3-fl2va-ref2va-lora/resolve/main/Minimax%20h3%E5%A4%9A%E5%8F%82%E8%80%83%E5%8F%8C%E9%87%87%E6%89%93%E6%96%97%E5%B7%A5%E4%BD%9C%E6%B5%81.json) | Jojocodex | FL2VA | Multi-reference dual-dispatch combat graph for the wushu LoRAs — several references per fight beat. |
| [Video (generic API)](https://github.com/Comfy-Org/workflow_templates/blob/main/archived/api_hailuo_minimax_video.json) | Comfy-Org | Ref2VA | Official Comfy-Org generic API video template; archived. |
| [OrbitQuant Ref2VA API Workflow](https://huggingface.co/WaveCut/MiniMax-H3-OrbitQuant-W4A4/resolve/main/comfyui/workflows/MiniMax-H3-OrbitQuant-Ref2VA-api.json) | WaveCut | Ref2VA | API-prompt version of the OrbitQuant Ref2VA workflow. |
| [Ref2VA GGUF Workflow](https://huggingface.co/Abiray/MiniMax-H3-GGUF/resolve/main/minimax_ref2va_gguf_workflow.json) | Abiray | Ref2VA | ComfyUI workflow for the GGUF-quantized Ref2VA model. |
| [R2V — Auto Prompting + Reference Manager](https://github.com/Hearmeman24/ComfyUI-MiniMaxRefPack/blob/main/example_workflows/MiniMax%20R2V%20-%20Auto%20Prompting%20%2B%20Reference%20Manager.json) | Hearmeman24 | Ref2VA | All 18 references wired once; H3 prompt auto-written; preview out (RefPack node). |
| [R2V — Auto Prompt](https://github.com/Hearmeman24/comfyui-minimax/blob/master/workflows/MiniMax%20H3/MiniMax%20-%20R2V%20-%20Auto%20Prompt.json) | Hearmeman24 | Ref2VA | VLM writes the H3 prompt from references. |
| [R2V (video_minimax_h3_r2v)](https://github.com/Hearmeman24/comfyui-minimax/blob/master/workflows/MiniMax%20H3/video_minimax_h3_r2v.json) | Hearmeman24 | Ref2VA | Reference-to-video workflow (stock naming). |
| [Deno R2V Turbo 8+2](https://huggingface.co/Deno2026/MiniMax-H3-DenoMix/resolve/main/workflows/Deno_MiniMax_H3_R2V_Turbo_8plus2.json) | Deno2026 | Ref2VA | DenoMix low-res Turbo 8-step pass, ×2 latent upscale, 2-step refine (896×512 → 1792×1024). ⚠️ Needs DENO Custom Nodes, LBH H3 Latent Upscaler, KJNodes and VideoHelperSuite. (GPL-3.0-only) |
| [INT8 R2V (javano2610.7.1)](https://huggingface.co/javawock7618/comfy-MiniMax-H3-workflows/resolve/main/MiniMax_int8_R2V-javano2610.7.1.json) | javawock7618 | Ref2VA | INT8 reference-to-video with Extend, ControlNet Union V2V, Latent Upscaler and Veda Sparse Attention. |
| [Ref2V](https://huggingface.co/StefanFalkok/Minimax_H3_Workflows/resolve/main/Minimax%20H3/Minimax%20H3%20Ref2V.json) | StefanFalkok | Ref2VA | Reference-to-video graph with stock nodes. |
| [Ref2V Prompt generator](https://huggingface.co/StefanFalkok/Minimax_H3_Workflows/resolve/main/Minimax%20H3/Minimax%20H3%20Ref2V%20Prompt%20generator.json) | StefanFalkok | Ref2VA | Writes the H3 prompt for reference-to-video from references. |
| [Face Refiner V2V](https://huggingface.co/StefanFalkok/Minimax_H3_Workflows/resolve/main/Minimax%20H3/Face%20Refiner%20V2V.json) | StefanFalkok | Ref2VA | Face refinement for an existing clip. |
| [Music-Video — Long-Shot Latent-Mask (Base+Ref)](https://huggingface.co/RuneXX/Minimax-H3-Workflows/resolve/main/Music-Video/Minimax-H3_-_Music-Video_Long-Shot-Latent-Mask_Base-Ref.json) | RuneXX | Ref2VA | Music-video workflow: long single shot with latent masking, base + reference conditioning. |
| [Music-Video — Long-Shot Latent-Mask (Multi-Scene Ref)](https://huggingface.co/RuneXX/Minimax-H3-Workflows/resolve/main/Music-Video/Minimax-H3_-_Music-Video_Long-Shot-Latent-Mask_MultiScene-Ref.json) | RuneXX | Ref2VA | Music-video workflow: multi-scene reference conditioning with latent masking. |
| [V2V — Extend Any Video (latent masking)](https://huggingface.co/RuneXX/Minimax-H3-Workflows/resolve/main/Video-to-Video/Minimax-H3_-_V2V_Extend_Any_Video_latent_masking.json) | RuneXX | Ref2VA | Video-to-video extension of any source clip via latent masking. |
| [H3 Seamless Chain (CORE)](https://huggingface.co/joeygambino/MiniMax-H3-Multishot-Workflow/resolve/main/workflows/H3_Seamless_Chain_CORE.json) | joeygambino | Multi-shot | Core seamless multi-shot chaining graph (FL2VA/Ref2VA clips). |
| [H3 Seamless Chain v2](https://huggingface.co/joeygambino/MiniMax-H3-Multishot-Workflow/resolve/main/workflows/H3_Seamless_Chain_v2.json) | joeygambino | Multi-shot | Multi-shot chaining workflow (v2). |
| [H3 Extend Take](https://huggingface.co/joeygambino/MiniMax-H3-Multishot-Workflow/resolve/main/workflows/H3_Extend_Take.json) | joeygambino | Multi-shot | Clip extension / take workflow. |
| [H3 Keyframes](https://huggingface.co/joeygambino/MiniMax-H3-Multishot-Workflow/resolve/main/workflows/H3_Keyframes.json) | joeygambino | Multi-shot | Keyframe-conditioned chaining. |
| [Music-Video — Multi-Scene Shot-by-Shot](https://huggingface.co/RuneXX/Minimax-H3-Workflows/resolve/main/Music-Video/Minimax-H3_-_Music-Video_Multi-Scene_Shot-by-Shot.json) | RuneXX | Multi-shot | Music-video workflow that builds a multi-scene clip shot-by-shot. |
| [comfy-MiniMax-H3-workflows (pack)](https://huggingface.co/javawock7618/comfy-MiniMax-H3-workflows) | javawock7618 | Bundle | Full INT8 low-VRAM acceleration stack: INT8 + native Block Sparse Attention + Spectrum + Lightx2v + Turbo + native Extend + Fun ControlNet Union V2V (openpose/canny/depth) + Latent Upscaler + TTS (+ Music, Ref2Image, LLM system-prompt utilities). |
| [PlagueKind-MinimaxH3 (pack)](https://huggingface.co/Plaguekind/Minimax-H3) | Plaguekind | Bundle | "Ease of use" I2V/R2V workflow line, currently **V9** (needs his nodepack v1.4.7 + latest ComfyUI), with an included fast turbo LoRA; Eros / Sulphur-model and FaceID compatible. Older V1–V8 kept under `old/`. MIT. |
| [INT8 TTS (javano2610.1.1)](https://huggingface.co/javawock7618/comfy-MiniMax-H3-workflows/resolve/main/MiniMax_int8_TTS-javano2610.1.1.json) | javawock7618 | Bundle | Audio-only speech generation. |
| [Music3](https://huggingface.co/javawock7618/comfy-MiniMax-H3-workflows/resolve/main/extra/MiniMax-Music3-javano2608.1.json) | javawock7618 | Bundle | Music generation workflow. |
| [Ref2Image](https://huggingface.co/javawock7618/comfy-MiniMax-H3-workflows/resolve/main/extra/MiniMax_int8-Ref2Image-javano2608.2.json) | javawock7618 | Bundle | Reference-to-image utility. |
| [INT8 Bridge (javano2610.4)](https://huggingface.co/javawock7618/comfy-MiniMax-H3-workflows/resolve/main/MiniMax_int8_Bridge-javano2610.4.json) | javawock7618 | Bundle | Transition clip between two videos. |
| [INT8 FR (javano2611.3)](https://huggingface.co/javawock7618/comfy-MiniMax-H3-workflows/resolve/main/MiniMax_int8_FR-javano2611.3.json) | javawock7618 | Bundle | Face refinement for generated video. |
| [FL2VA LLM system prompt](https://huggingface.co/javawock7618/comfy-MiniMax-H3-workflows/resolve/main/llm_system_prompt_for_minimax-h3_fl2va-2608.6.txt) | javawock7618 | Bundle | Drop-in LLM system prompt for auto-writing structured FL2VA prompts (pair with a local LLM node). |
| [Ref2VA LLM system prompt](https://huggingface.co/javawock7618/comfy-MiniMax-H3-workflows/resolve/main/llm_system_prompt_for_minimax-h3_ref2va-2610.1.txt) | javawock7618 | Bundle | Ref2VA counterpart of the FL2VA LLM system prompt. |
| [MiniMax-H3-Multishot-Workflow (pack)](https://huggingface.co/joeygambino/MiniMax-H3-Multishot-Workflow) | joeygambino | Bundle | ComfyUI-H3-Multishot node pack + multi-shot workflows + presenter demo. Apache-2.0. |
| [Six upscale routes (pack)](https://huggingface.co/AI-KSK/minimax-h3-video-upscale-six-routes-294) | AI-KSK | Bundle | Six upscale/redraw graphs: one LTX 2.5 V2V and five H3 two-/three-stage routes. |
| [VoxCPM digital human (pack)](https://huggingface.co/AI-KSK/minimax-h3-voxcpm-digital-human-289) | AI-KSK | Bundle | Single-character and two-character dialogue graphs driven by VoxCPM speech. |
| [Keyframe timeline (pack)](https://huggingface.co/AI-KSK/minimax-h3-keyframe-timeline-two-graphs-300) | AI-KSK | Bundle | FL2VA first/last-frame and Ref2VA multi-reference graphs with keyframe story beats. |
| [H25 hybrid multi-ref (pack)](https://huggingface.co/AI-KSK/minimax-h3-h25-hybrid-multiref-293) | AI-KSK | Bundle | H25 hybrid multi-reference 8-step graph. |
| [H3 Ad Recast (pack)](https://github.com/m24927605/h3-long-ads) | m24927605 | Bundle | Recasts an ad's person and product in one pass with synced dialogue; also a 30 s product-ad graph. ⚠️ Needs ComfyUI master (context windows). MIT. |

*Comfy-Org's original `templates/video_minimax_h3_*` T2V/I2V/R2V graphs were moved to `archived/` and are now API-based (Hailuo/Minimax API) templates — links above point to the archived JSONs.*

*StefanFalkok's repo was restructured again: the `Minimax H3 Face Refine/` subfolder is gone and the `I2V — Face Refine` graph was removed upstream. `Minimax H3/` now holds seven graphs, including `Face Refiner V2V.json`, the live-wallpaper prompt generator and a RIFE interpolation pass. For PDD-Acc 8-step acceleration, use the [alibaba-pai Acc LoRAs](https://huggingface.co/alibaba-pai/MiniMax-H3-Acc-LoRAs) directly (see [Turbo](#checkpoints)).*

*javawock7618 renames the workflow JSONs frequently — if a pinned link above 404s, browse the [repo tree](https://huggingface.co/javawock7618/comfy-MiniMax-H3-workflows/tree/main) for the current build.*

*AI-KSK packs are source exports with SHA256 manifests — no inference was run and no weights are bundled; verify workflow, node, model and cover rights separately.*

