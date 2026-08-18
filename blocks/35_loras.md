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

* EllaPriest45
  * [MinimaxH3_Actions](https://huggingface.co/EllaPriest45/MinimaxH3_Actions/tree/main) - ⚠️ **Contains explicit / NSFW content.** Collection of NSFW action LoRAs for MiniMax-H3 (T2V/I2V/R2V). Includes motion-specific LoRAs with trigger words and strength recommendations. See the repo for the full list. (reference only)
  * [MinimaxH3_Characters](https://huggingface.co/EllaPriest45/MinimaxH3_Characters/tree/main) - ⚠️ **Contains explicit / NSFW content.** Character LoRA collection for MiniMax-H3 (e.g. Aunt Cass, Baldur's Gate 3 Party Pack, Judy Hopps). Browse at your own discretion; not enumerated with per-file downloads here.
  * [MinimaxH3_Styles](https://huggingface.co/EllaPriest45/MinimaxH3_Styles/tree/main) - ⚠️ **Contains explicit / NSFW content.** Style LoRA collection for MiniMax-H3 with previews and config text; significant NSFW/nude portion (anime, digicam, Playboy styles). Browse at your own discretion; not enumerated with per-file downloads here.

* [fal/research-mini-max-h3-realism-people-lora](https://huggingface.co/fal/research-mini-max-h3-realism-people-lora) - Realism LoRA for natural-looking people in everyday scenarios. Trained by fal on diverse photo data. (125 MB)

* [Inner-Reflections/MiniMax-H3-Looping-Sketch-Anime](https://huggingface.co/Inner-Reflections/MiniMax-H3-Looping-Sketch-Anime) - Looping anime-style sketch LoRA. Hand-drawn 2D outlines, flat colors, white outline. Strength 0.75–1.25; pair with a Turbo LoRA for higher strength. (569 MB)

* [nikdevs/minimax-h3-loras](https://huggingface.co/nikdevs/minimax-h3-loras) - ⚠️ **Contains explicit / NSFW content.** Curated MiniMax-H3 LoRA collection (styles + characters). Browse at your own discretion; not enumerated with per-file downloads here.

* [DiffSynth-Studio/MiniMax-H3-LoRA-LineartAnime](https://huggingface.co/DiffSynth-Studio/MiniMax-H3-LoRA-LineartAnime) - **Anime video line-art colorization** — feeds a line-art video as a reference and generates fully colored anime output from it (Ref2VA video-reference workflow). Apache-2.0. (1.26 GB)

* Jojocodex
  * [minimax-h3-wushu-action-lora](https://huggingface.co/Jojocodex/minimax-h3-wushu-action-lora) - **Wushu / martial-arts action** — trains H3 to generate human martial-arts motion (punches, kicks, spins, staff techniques), focused on body physics. Trigger by action description (e.g. `a martial artist performing punches and kicks in fast combat`); no fixed trigger word. ai-toolkit, rank 16, 2000 steps, 512 / 90 frames @ 24fps; pruned + full safetensors. ComfyUI users load the `_pruned` variant at strength 0.8–1.0; compatible with the Turbo LoRA (adaln_proj trimmed, 417 keys). Base-model use is under the MiniMax H3 Community License. (155 MB pruned · 310 MB full)
  * [minimax-h3-spatial-physics-lora](https://huggingface.co/Jojocodex/minimax-h3-spatial-physics-lora) - **Spatial & physics (objects)** — teaches H3 object physics (collision, stacking, falling, occlusion) via pure spatial+physics captions; complements the wushu LoRA, which covers body motion. No fixed trigger word — describe object motion directly. Trained on CLEVRER / WISA / PhyCo-Kubric (700 clips); ai-toolkit, rank 16. ComfyUI users load `_pruned` at 0.8–1.0; stacks with the Turbo LoRA. (155 MB pruned · 310 MB full)
  * [minimax-h3-yunjing-lora](https://huggingface.co/Jojocodex/minimax-h3-yunjing-lora) - **Camera-movement (yunjing) control** — cinematic camera-movement control (push in/out, orbit, tracking, handheld) via the `yunjing` trigger word. 12 movement types trained (handheld / pull / dolly best-covered; pan / crane / 360° weakly covered). ai-toolkit, rank 32, 1000 steps; pruned + full. ComfyUI users load `_pruned` at 0.8–1.0; stacks with the Turbo LoRA (6–8 steps, Euler, Beta). (310 MB pruned · 620 MB full)


* [Hearmeman/minimax-h3-loras](https://huggingface.co/Hearmeman/minimax-h3-loras) - ⚠️ **Contains explicit / NSFW content.** Six single-concept NSFW adapters, split into **anatomy** (stills-trained — they restore structure the base model renders soft and vague) and **action** (video-trained — what the body does). They are meant to stack: anatomy underneath, action on top, your character or scene LoRA above both. Each has its own trigger word and a documented prompt vocabulary; `HMBreasts` and `HMInnie` expose named shape/colour axes written as plain English rather than tags. Mirrored from [CivitAI](https://civitai.com/user/HearmemanAI), byte-identical with SHA-256 published. Base-model use is under the MiniMax H3 Community License.

| LoRA | Trigger | Kind | Strength | Download |
| :--- | :--- | :--- | :---: | :--- |
| `HMNSFW_AIO_V2` — all-in-one sex motion | `hmmotion` | action · video | ≤ 0.5 | [![][gh-Hearmeman]](https://huggingface.co/Hearmeman/minimax-h3-loras/resolve/main/HMNSFW_AIO_V2.safetensors) |
| `HMCumshot_V2` — cumshot action | `cumshot` | action · video | 0.9 | [![][gh-Hearmeman]](https://huggingface.co/Hearmeman/minimax-h3-loras/resolve/main/HMCumshot_V2.safetensors) |
| `vagassist_e40` — pussy/anus structure | `Vagina` | anatomy · stills | 1.0 | [![][gh-Hearmeman]](https://huggingface.co/Hearmeman/minimax-h3-loras/resolve/main/vagassist_e40.safetensors) |
| `hmpussy_v6_epoch30` — holds it through motion | `hmpussy` | anatomy · video | 0.35 | [![][gh-Hearmeman]](https://huggingface.co/Hearmeman/minimax-h3-loras/resolve/main/hmpussy_v6_epoch30.safetensors) |
| `HMInnie_v1_e50` — innie shape control | `inniepussy` | anatomy · stills | — | [![][gh-Hearmeman]](https://huggingface.co/Hearmeman/minimax-h3-loras/resolve/main/HMInnie_v1_e50.safetensors) |
| `HMBreasts_085e0750_e40` — size/areole control | `HMBreasts` | anatomy · stills | — | [![][gh-Hearmeman]](https://huggingface.co/Hearmeman/minimax-h3-loras/resolve/main/HMBreasts_085e0750_e40.safetensors) |
| `HMPenis_v2_e35` — penis anatomy | `HMPenis` | anatomy · stills | — | [![][gh-Hearmeman]](https://huggingface.co/Hearmeman/minimax-h3-loras/resolve/main/HMPenis_v2_e35.safetensors) |

  The two HMPussy files are one LoRA in two halves and load together: the stills file restores the structure, the video file holds it together through motion. (296 MB each, 597 MB for `HMCumshot_V2` and `hmpussy_v6_epoch30`)

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