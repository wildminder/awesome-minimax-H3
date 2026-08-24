
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

