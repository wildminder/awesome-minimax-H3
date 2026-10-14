
<p id="guides" align="center">◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆◇◆</p>

## ▓ Guides & Tutorials

### ▣ Official Guides

* [Video Prompt Writing Guide (Base)](https://huggingface.co/MiniMaxAI/MiniMax-H3/blob/main/docs/VIDEO_PROMPT_WRITING_GUIDE_base_en.md) - Official MiniMax-H3 prompt writing guide for base (FL2VA) mode. Covers prompt structure, camera language, scene composition, and best practices for text-to-video and image-to-video generation.
* [Video Prompt Writing Guide (Reference)](https://huggingface.co/MiniMaxAI/MiniMax-H3/blob/main/docs/VIDEO_PROMPT_WRITING_GUIDE_ref_en.md) - Official MiniMax-H3 prompt writing guide for reference (Ref2VA) mode. Covers multi-modal reference inputs, image/video/audio reference handling, and prompt construction for omni-reference generation.

### ▣ ComfyUI Tutorials

* [ComfyUI MiniMax-H3 Tutorial](https://docs.comfy.org/tutorials/video/minimax/minimax-h3) - Official ComfyUI documentation tutorial for MiniMax-H3 setup and usage.
* [ComfyUI MiniMax-H3 Guide (nimblecloud13)](https://github.com/nimblecloud13/ComfyUI-MiniMax-H3-Guide) - Plain-English beginner guide to MiniMax-H3 in ComfyUI, delivered as a **PDF plus a self-contained HTML page** (both in the repo — GitHub renders the HTML as source, so download it). Every entry answers what it is, what it does to the image or video, and what to set it to, across seven sections: big picture, what the model does, the parts, file names, settings, your hardware, first run. Sizing advice is written for a **16 GB card with 32 GB RAM**, with notes for smaller cards. The repo also covers Wan 2.2, Qwen Image 2.1 and Krea 2, but only the H3 guide applies here.
* [MiniMax H3 Day-0 Support in ComfyUI](https://blog.comfy.org/p/minimax-h3-day-0-support-in-comfyui) - ComfyUI blog post covering open weights, native audio, 2K video output, and local execution on a 3060.

### ▣ Performance

* [MiniMax H3 — Performance & Best-Configuration Report](guides/minimax-h3-performance.md) - Local-inference performance guide for MiniMax H3 (FL2VA / Ref2VA) across consumer & workstation GPUs, Apple Silicon, and the DGX Spark — distilled from 2 hard-numbered benchmarks and 17 community field reports. Covers a TL;DR config recommendation, hardware-tier tiers, the best speed/quality recipe, and caveats & licensing.
* [MiniMax H3 on an RTX 3060 12GB: what we actually measured](https://www.minimaxh3tutorial.com/rtx-3060) - Real-world write-up of running MiniMax-H3 on a 12 GB RTX 3060 — what actually fits, at what resolution and step counts, and the configuration that worked.
* [MiniMax H3 speed-up notes (matsuo-koya)](https://github.com/matsuo-koya/minimax-h3-notes) - Measured field notes from three weeks on one RTX 5090 (32 GB, WSL2, ComfyUI 0.33) building a home lip-sync music-video studio, plus a 4090 worker and Apple Silicon: INT8 ConvRot (true quant error 0.90%), Turbo 8-step, a self-converted FastH3 4-step ComfyUI LoRA (1.87× vs Turbo, zero failures over a 30-segment MV), comfy-kitchen INT8 attention (sampler ≈2× on 5090, 1.79× at production length; VAE decode untouched), width 1280→1216 (−15% via VAE tile count), a pull-based 5090+4090 distributed segment queue (3.8→2.7 h), the 345-frame stall cliff on the 4090 (per-step profiling), negative results (Zironic H3MemoryOptimization silently changes output; ToneCompensate unneeded; PDD Acc-LoRAs need a missing sampler), and two key conversion findings — diffusers→ComfyUI H3 LoRAs have **swapped fused `fc1` halves** (`[value; gate]` vs `[gate; value]`), and ComfyUI silently falls back to tiled VAE decode on OOM. Full Japanese write-up + English summary. MIT.

### ▣ Prompting & Prompt Datasets

* [MiniMax H3 — 1,000-Prompt Curation](https://github.com/yangzhou-chaofan/minimax-h3-1000-prompts) - Curated index + analysis of the `ostris/minimax_h3_1k` dataset (1,000 prompts + 768p clips, generated with the pruned INT8-ConvRot FL2VA checkpoint @ 30 steps). Explains H3's 3-field prompt structure (`integrated_multimodal_description` / `overall_soundscape` / `non_diegetic_music`), highlights 10 reusable prompts with commentary, and compares H3 vs Seedance / Veo / Kling on fidelity, dialogue, sound design, and multi-shot continuity.
* [Interactive atlas of all 1,000 clips (neta.art)](https://neta.art/use-cases/en/h3-1000-prompt-list) - Browse every clip from the 1K prompt dataset — every prompt, every style — with per-clip metadata: shooting-style/subject filters, prompt / soundscape / music / aspect-ratio / dialogue details, one-click generate or download.
* [Codex × MiniMax H3 自动成片与验收 Skill](https://github.com/JiaYang-BUAA/codex-minimax-h3-video-skill) - Codex Skill for automated multi-shot H3 video production + QA: Codex splits storyboards and writes prompts, Z-Image generates first/last frames, **MiniMax H3 Director** schedules H3 shot generation (with audio), HyperFrames handles editable timeline editing/rendering, then Codex verifies dialogue (ASR), continuity, black frames, and specs — with local rework loops. Windows 11 + PowerShell 7 + ComfyUI ≥ 0.30; validated on RTX 5070 Ti 16 GB (~49 GB models). MIT; no model weights bundled.

