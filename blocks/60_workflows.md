
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

### ❖ Community Packs

* [joeygambino/MiniMax-H3-Multishot-Workflow](https://huggingface.co/joeygambino/MiniMax-H3-Multishot-Workflow) - Seamless multi-shot chaining workflow for MiniMax-H3 in ComfyUI — string multiple FL2VA/Ref2VA clips into one continuous sequence with matched audio handoffs. Apache-2.0.
* [javawock7618/comfy-MiniMax-H3-workflows](https://huggingface.co/javawock7618/comfy-MiniMax-H3-workflows) - Curated ComfyUI workflow pack covering the full low-VRAM acceleration stack in one importable bundle: INT8 + SageAttention + Spectrum + Lightx2v + Turbo + Motion Context + Latent Upscale + TTS.
* [Hearmeman24/ComfyUI-MiniMaxRefPack — R2V + Reference Manager](https://github.com/Hearmeman24/ComfyUI-MiniMaxRefPack/blob/main/example_workflows/MiniMax%20R2V%20-%20Auto%20Prompting%20%2B%20Reference%20Manager.json) - Reference-to-Video graph built around the MiniMax References Manager node: all 18 references wired once, the H3 prompt written automatically from those references, video preview on the output.
* [Hearmeman24/comfyui-minimax — T2V / I2V workflows](https://github.com/Hearmeman24/comfyui-minimax/tree/master/workflows/MiniMax%20H3) - T2V and I2V, each in a Custom Prompt version (you write it) and an Auto Prompt version (you type one line and a VLM writes the full six-section H3 prompt). Turbo LoRA and video preview wired in.

