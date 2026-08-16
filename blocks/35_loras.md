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

* [DiffSynth-Studio/MiniMax-H3-LoRA-LineartAnime](https://huggingface.co/DiffSynth-Studio/MiniMax-H3-LoRA-LineartAnime) - **Anime video line-art colorization** — feeds a line-art video as a reference and generates fully colored anime output from it (Ref2VA video-reference workflow). Apache-2.0. (1.26 GB)

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

* [MATLOWAI/MiniMax-H3-Motion-Adapter](https://huggingface.co/MATLOWAI/MiniMax-H3-Motion-Adapter) - **Motion adapter (pilot, r16)** — a small rank-16 BF16 LoRA that improves the de-rope pass in ComfyUI-MAINodes on fast motion: reduces frame-by-frame advance/snap alternation and over-production, and transfers to both FL2VA and Ref2VA graphs (one file). Trained bf16 (rank 16, alpha 16). MIT for the adapter weights; base model use is under the MiniMax H3 Community License. Load with a stock `LoraLoaderModelOnly` at strength 1.0 on the de-rope pass only. (63 MB)