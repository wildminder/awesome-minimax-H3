<div align="center" id="readme-top">

# ⟦ MiniMax H3 — Performance & Best-Configuration Report ⟧


> **Local-inference performance guide for MiniMax H3 (FL2VA / Ref2VA)** across consumer & workstation GPUs, Apple Silicon, and the DGX Spark — distilled from **2 hard-numbered benchmarks** and **17 community field reports**. Scope is MiniMax-H3 only; no unrelated models are covered.

[![MiniMax H3](https://img.shields.io/badge/MiniMax-H3-8B5CF6?style=for-the-badge)](https://www.minimax.com)
[![ComfyUI](https://img.shields.io/badge/ComfyUI-FF6B00?style=for-the-badge)](https://www.comfy.org)
[![Updated](https://img.shields.io/badge/Updated-2026--08--16-ffc107?style=for-the-badge)](https://github.com)

</div>

> [!NOTE]
> Numbers are real-world, single-machine observations — treat as ranges, not guarantees.

## ❯ Table of Contents

1. [TL;DR — What to Use](#tldr-what-to-use)
2. [Model Basics](#model-basics)
3. [Structured Benchmarks](#structured-benchmarks)
4. [Hardware-Tier Recommendations](#hardware-tier-recommendations)
5. [Best Speed/Quality Recipe](#best-speedquality-recipe)
6. [Reddit Community Field Reports](#reddit-community-field-reports)
   - [5.1 The four "speed levers" — community verdict](#51-the-four-speed-levers-community-verdict)
   - [5.2 Real-world configs reported](#52-real-world-configs-reported-in-the-threads)
   - [5.3 What the community converged on](#53-what-the-community-converged-on)
   - [5.4 Per-thread index](#54-per-thread-index-your-17-reference-links)
7. [Caveats & Licensing](#caveats-licensing)
8. [References](#references)

<p align="center">◈ ━━━━━━━━━━━ ◈</p>

## ❯ TL;DR — What to Use

| Your GPU / RAM | Best config | Steps | ~Speed (5 s clip) | Quality |
|---|---|---|---|---|
| **RTX 4090 / 3090 / 5090 (24 GB)** | pruned INT8 + NVFP4, or Q5_K_M GGUF | 20 (base) / 4 (Turbo) | ~4 min (1 MP) – 12 min (10 s) | best consumer |
| **RTX 5080 / 4080 (16 GB)** | Q4_K_M GGUF + Turbo 4–8 step, or pruned INT8 + NVFP4 + CUDA 13 | 4–8 | ~5–6 min (5 s @1 MP / 10 s @0.8 MP) | near-full |
| **RTX 4070 / 3060 12 GB (+64 GB RAM)** | pruned INT8 ConvRot + NVFP4 + Turbo 8-step + Sage / EasyCache | 8 | ~3–6 min (0.4–0.6 MP) | good |
| **RTX 4060 laptop (8 GB)** | pruned INT8 ConvRot + Qwen3-VL 32B NVFP4-AWQ + SageAttn 2.2 | 20 (base) / 8 (Turbo) | ~10–15 min | usable |
| **6 GB (3050 / 3060 / 4050 + ≥24 GB RAM)** | **INT4 ConvRot** + INT4 clip + Kijai int8 VAE + audio VAE fp32 + Turbo v4 step600 (8 steps) | 8 | ~5–10 min (10 s @0.2–0.3 MP) | works; OOM above ~0.4 MP |
| **Apple Silicon Mac (16 GB+)** | VPIPE (Metal) or MLX streaming | 4–8 | ~15 min (3.75 s @0.5 MP, M5 Air) | good (slow) |
| **DGX Spark / GB10 (128 GB unified)** | FL2VA INT8 + Sol Engine + 2× RealESRGAN upscale | 20 / 8 | 2m25s (5 s @720p, half-res+upscale) | best per watt |

> [!TIP]
> **Universal speed/quality rule:** 20 steps (base) = maximum quality; **Turbo LoRA at 4 steps** = ~3.4× faster with acceptable quality loss; sampler **res_multistep** or **euler/simple**, **cfg = 1.0**, sigma shift **video 12 / audio 3**.

([back to top](#readme-top))

<p align="center">◈ ━━━━━━━━━━━ ◈</p>

## ❯ Model Basics

* **Architecture:** 33.1 B-parameter dense single-stream omni-transformer (13 B is an AdaLN branch) + **Qwen3-VL-32B** text encoder.
* **Checkpoints:** **FL2VA** (text → video / first-last-frame) and **Ref2VA** (image/video/audio reference). Diff weights identical in size.
* **Output:** up to **15 s @ 24 fps, 768p default**, 32 kHz stereo audio in the same pass; 11 languages; aspect ratios 21:9 → 9:16. (2K upscaling / H3-Context-IR are **hosted-API only**, not released.)
* **Frameworks:** ComfyUI, Diffusers, SGLang, vLLM, vLLM-Omni, MLX.

### * File-size / VRAM tiers (from measured HF file sizes)

| Config | Disk | VRAM (community/ComfyUI-team) | Target GPU |
|---|---|---|---|
| pruned INT8 + NVFP4 AWQ (ComfyUI default) | ~42.5 GB | ~24 GB (12 GB *may* work w/ ample RAM + fast disk) | 24 GB / 12 GB w/ offload |
| int8_convrot (non-pruned) | ~67 GB | ~48 GB | 48 GB (RTX 6000 Ada) |
| full bf16 | ~123.6 GB | 80 GB or 4-GPU (official SGLang example) | H100 / 4× GPU |
| GGUF Q3_K_S/M (UNet 15.6 GB) | ~36 GB total | 12 GB tier | 3060 12 GB / 4070 |
| GGUF Q4_K_M (UNet 19.9 GB) | ~40 GB total | 16 GB tier | 4080 / 5080 |
| GGUF Q5_K_M (UNet 23.9 GB) | ~44 GB total | 24 GB tier | 4090 / 3090 |

([back to top](#readme-top))

<p align="center">◈ ━━━━━━━━━━━ ◈</p>

## ❯ Structured Benchmarks

### * A. jo-nike.github.io/h3-turbo-eval — 25-config grid
* **Rig:** RTX 5080 (16 GB), ComfyUI 0.30.0 (2026-08-07), torch 2.12.1+cu130. All at **960×544, 5.17 s**, 10 stress scenes, seed 424242.
* **Configs tested:** base (none) 20 steps; larryvrh Turbo EMA/non-EMA 8 steps (ckpt500 & v4 step-600); lightx2v 4-step distillation at strength 0.75/1.0, samplers res_multistep / er_sde, sigma-shift audio 3 vs 6; + SageAttention / Sol-Attn / Spectrum accelerator columns.
* **Key findings:** distillation (4-step) is known to hurt the *quietest/sustained* vocal registers (held notes, whispers) and to regress accents/code-switching toward generic; hard cuts can smear into dissolves under distillation. **LightX2V 4-step strength 1.0** is the speed pick; **strength 0.75** trades a little quality for stability. Sigma-shift **audio 6 ("house")** helps loudness but runs ~9 dB hot on whispers vs default 3.
* **Accelerators:** **Sol-Attn = lossless** (bit-identical verified); **SageAttention (bf16)** speeds compute but *costs VRAM*; **Spectrum = lossy** (not bit-identical).
* **Critical fix:** Kijai's MiniMax audio-sampler rework (`bdcb886a`, merged **2026-08-06**) — use ComfyUI ≥ 0.30.0 for correct audio through the sampler.

### * B. sepiablue-ai/minimax-h3-turbo-lora-benchmark — RTX 4070 12 GB
* **Rig:** RTX 4070 12 GB, **576×832, 124 frames, 24 fps**, sampler **euler / beta**, peak VRAM **~10.6 GiB** (all configs).

| Config | Steps | Time / 124 fr | Speedup | Peak VRAM |
|---|---|---|---|---|
| Baseline (no LoRA) | 20 | **272.97 s** | — | 10.66 |
| Larry/drbaph `v4_step600_ema` | 8 | **130.30 s** | 2.09× | 10.66 |
| LightX2V 8-step v1.0 | 8 | **131.02 s** | 2.08× | 10.60 |
| **LightX2V 8-step v1.0** | **4** | **79.36 s** | **3.44×** | 10.66 |

→ **LightX2V 4-step is the fastest measured (3.44×) with essentially unchanged VRAM.** No quantitative quality score (visual demos only).

([back to top](#readme-top))

<p align="center">◈ ━━━━━━━━━━━ ◈</p>

## ❯ Hardware-Tier Recommendations

### * 24 GB class (RTX 4090 / 3090)
* Use **pruned INT8 + NVFP4** default, or **Q5_K_M GGUF** for closest-to-full quality. 20 steps for max quality, **Turbo 4-step** for ~3.4× speed. Layer-wise offload usually unnecessary. This is the realistic "best quality" consumer tier.

### * 16 GB class (RTX 5080 / 4080)
* **Q4_0 / Q4_K_S / Q4_K_M GGUF** + NVFP4/AWQ text encoder (community default for this tier). Turbo 4-step + sol-attn. The h3-turbo-eval grid ran comfortably on a 5080 16 GB at 960×544.
* **CUDA version matters a lot:** an RTX 4080 Super owner (1vmcuq5) went from ~20–60 min for a 1 MP 5 s clip to **~300 s** just by updating **CUDA 12.6 → 13** (with Sage + Spectrum + 8-step Turbo). Community also reports **Comfy Kitchen attention (`--use-ck-attention`) beats SageAttention** on some 40/50-series rigs. Keep ComfyUI ≥ 0.30 and PyTorch rebuilt for CUDA 13.

### * 12 GB class (RTX 4070 SUPER / 3060 12 GB) — `shiqikuangsan31/MiniMax-H3-12GB-ComfyUI-Guide`
* **Files:** `pruned_int8_convrot` 20.97 GB + `qwen3vl_32b nvfp4_awq` 15.69 GB + video VAE fp16 5.21 GB + audio VAE fp32 0.61 GB.
* **Launch:** `python main.py --lowvram --disable-mmap` (disable-mmap avoids Windows safetensors crash on >20 GB files; needs ComfyUI ≥ 0.31).
* **RAM:** 32 GB *works*, **64 GB RAM is the root-cause fix** for the offload bottleneck (21 GB model shuffled per step).
* **Measured (per 5 s segment):** 20-step official (1280×736) = **1006 s**; **Turbo 4-step + EasyCache = 420 s** (fastest usable, quality OK); Turbo 8-step and 8-step-no-LoRA both failed/incomplete.
* **Acceleration verdict on 12 GB (--lowvram):** ✓ **sol-attn** (lossless), ✓ **Turbo 4-step + EasyCache** (only effective combo), ✓ **64 GB RAM**; ✗ SageAttention (2.5–3× slower — more VRAM → more offload), ✗ Spectrum (lossy), ✗ FP4/NVFP4 (Blackwell SM 10.0 only; 4070S = SM 8.9), ⚠ FP8 (<15% gain, same size as INT8).

### * 8 GB class (RTX 4060 laptop) — `iaipie.com` hands-on tutorial
* **Quant:** **NF4** (`MiniMax-H3-NF4.safetensors` ~12 GB model file) via Comfy-Org or DiffSynth-Studio.
* **RAM:** **≥ 32 GB required, 64 GB recommended.** SSD ≥ 50 GB.
* **Frames:** must be `17k+5` (e.g. 22 / 73 / 90). Test = **73 frames (~3 s)**.
* **Steps:** `num_inference_steps=50`, `guidance_scale=7.5`.
* **Measured (73 fr / 768p / 50 steps):** RTX 3060 12 GB NF4 ~8–12 min, ~11 GB VRAM; **RTX 4060 8 GB NF4 ~10–15 min, ~7.5 GB VRAM** (little headroom). First load +1–3 min.
* **OOM fixes:** quant down (FP16→INT8→NF4) → lower resolution (1280×720→768×768) → fewer frames (90→73) → disable audio (`enable_audio=False` saves ~2 GB) → `torch.cuda.empty_cache()`. Audio VAE **must stay fp32** or A/V desyncs.
* **6 GB GPUs:** previously considered OOM-only, but community field reports (§5) now show it *is* runnable on RTX 3050 / 3060 / 4050 6 GB with **INT4 ConvRot** model + INT4 Qwen3 clip + Kijai int8 video VAE + fp32 audio VAE, Turbo v4 step600 at 8 steps (euler/beta) — ~5 min (10 s @0.2 MP) to ~10 min (10 s @0.3 MP). Do **not** exceed ~0.4 MP or you will OOM; sustained laptop loads carry a real hardware-failure risk (see §5, `1vlqwme`).

### * 6 GB class (RTX 3050 / 3060 / 4050 Laptop) — Reddit `1vml6rh` + `1vlqwme`
* **Verified community build:** `minimax_h3_fl2va_pruned_int4_convrot` + `qwen3vl_32b_minimax_h3_int4_convrot` (clip) + `minimax_h3_video_vae_int8_convrot` (video) + `minimax_h3_audio_vae_fp32` (audio). Turbo LoRA `minimax_h3_turbo_v4_step600_ema_pruned_comfyui` strength 1, sampler **euler / beta, 8 steps**, SageAttention via KJNodes patch.
* **RAM:** ≥24 GB (one reporter used exactly 24 GB); 32 GB recommended. SSD ≥50 GB.
* **Measured (community):** RTX 3050 6 GB + 24 GB RAM → **0.2 MP @10 s ≈ 5 min**, **0.3 MP @10 s ≈ 10 min** (can't go past 0.4 MP without OOM). RTX 3060 6 GB + 32 GB RAM uses `er_sde + beta` and lowers frame count in the MathExpression node + post frame-interpolation to stay under VRAM.
* **Finals:** generate short low-res drafts, then stitch with **MiniMax H3 Context Loop** (multiple short high-res clips) or upscale externally (RTX Super Resolution).

> [!CAUTION]
> An RTX 4050 Laptop 6 GB owner reported a *physical GPU failure* (VIDEO_DXGKRNL_FATAL_ERROR, surprise-removal) after repeated heavy generations at 75–85 °C (thread `1vlqwme`). This is **not** a ComfyUI fault — a cooling/driver failure. Mitigate: cooling pad, power-limit / underclock, 85 °C throttle target; prefer desktop over laptop for sustained loads.

### * Apple Silicon Mac — `Argus-AiTeam/minimax-h3-mac`
* **Method:** MLX with **streaming weight loading** (only active layers in RAM), **not** ComfyUI MPS.
* **Tested:** MacBook Pro M4 Pro 24 GB, 14-core.
* **BF16 route:** 1344×768, 5 s, **2878.7 s (~48 min)**, peak ~15.8 GB (max RSS ~6.9 GB), 4-step Turbo (sigma 6/3).
* **INT8 + MLX Turbo route:** 768×448, 5 s, **1378 s (~23 min)**, max RSS 12 GB, 8 NFE.
* No cloud GPU needed; not real-time. No verified ComfyUI-MPS performance — plan around 24 GB+ unified memory.

### * DGX Spark / GB10 (128 GB unified) — two verified repos
* **Xplore-LAB (ComfyUI, FL2VA INT8 + Qwen3-VL-32B NVFP4):** weights 42.5 GB. 20 steps, cfg 1.0, euler/simple. Measured: 608×352 / 4 s = **96.8 s**; 736×416 / 5 s = **179.9 s**; 864×480 / 5 s = **255.8 s**; 768×1152 I2V / 5 s = **15 min 22 s**. Sampling ≈ 26–47 s/step.
* **joeynyc (vLLM-Omni, online dynamic FP8):** model load 89.2 GiB, cold start 519–543 s. Warmed request: baseline **152.9 s**, full-compute **111.4 s**, **balanced (Cache-DiT 0.10) 80.6 s** — output 768×448. Quality vs BF16: **SSIM 0.881, PSNR 26.6 dB** (Cache-DiT is approximate, not lossless).
* **Rule:** don't co-run other big-model containers (unified memory fills); lower resolution if exit-code 137 / system lag.

([back to top](#readme-top))

<p align="center">◈ ━━━━━━━━━━━ ◈</p>

## ❯ Best Speed/Quality Recipe

**Sampler / scheduler**
* Base quality: **res_multistep** (eval grid) **or euler + simple** (GitHub/12 GB guide), **cfg = 1.0**.
* Sigma shift: **video 12 / audio 3** (default). Use audio **6** only if you want louder mixed audio (runs hot on quiet passages).
* Step count: **20 = max quality**; **8 = Lar9/drbaph or LightX2V 8-step**; **4 = LightX2V 4-step (fastest, 3.44×)**.
* Turbo LoRA strength: **1.0** for max speed, **0.75** for more stable voices/accents.

**Custom nodes to install (ComfyUI)**
* `ComfyUI-MiniMax-H3-Turbo` (larryvrh) — Turbo LoRA loader (`MiniMaxH3TurboLoRA`, set `low_vram=true` on ≤12 GB).
* `comfyui-minimax-h3-audio-T8` (T8mars) — audio VAE decode/save.
* **sol-attn** — lossless attention speedup (recommended everywhere).
* **EasyCache** — *only* helps at 4-step Turbo (ignored/inverse at 20 steps).
* SageAttention — bf16 kernel speedup; **skip on ≤12 GB** (VRAM cost → slower via offload).
* Spectrum — lossy; avoid if quality matters.
* For GB10: **vLLM-Omni + Cache-DiT** (balanced profile) instead of ComfyUI.
* For Mac: **MLX** streaming loader (Argus-AiTeam repo).
* Use ComfyUI **≥ 0.30.0** (Kijai audio-sampler fix, 2026-08-06) or audio desyncs/breaks.

**Resolution / length guidance**
* Default 768p; 0.2 MP (608×352) is the speed floor, 0.8 MP (1216×672) the practical ceiling on consumer GPUs.
* 15 s clips need segment chaining (MotionContext / multi-segment) to avoid character drift.

([back to top](#readme-top))

<p align="center">◈ ━━━━━━━━━━━ ◈</p>

## ❯ Reddit Community Field Reports

### * 5.1 The four "speed levers" — community verdict

| Lever | Verdict | What the threads actually say |
|---|---|---|
| **SageAttention (bf16)** | ✓ Near-free speed, minimal quality loss — broadest agreement | Several report **Comfy Kitchen attention (`ck-attn`) beats Sage** on 40/50-series (`asdrabael1234`, `atakariax`, `Ok_Tale7582`). On ≤12 GB it can *cost* VRAM and slow you via offload (12 GB guide). |
| **Turbo LoRA** (larryvrh `v4_step600_ema` / lightx2v 4- & 8-step) | ✓ Fastest, but real quality + audio cost | lightx2v 4-step = fastest measured (3.44×). Audio "goes down the shitter" (`pit_shickle`); blurry fast motion (`infearia`); several can't get good results below 12 GB VRAM (`Ashamed_Company_5538`). lightx2v **768p 1.0 at 0.5–0.8 MP** widely praised. |
| **Spectrum** | ⚠ Needs 30–50 steps to shine; lossy | "Forecasts" steps — near-useless at 10 steps, tanks quality (`SilliusApeus`, `mellowanon`). Pairs with Sage *only* at high steps. Hurts audio (`MannY_SJ`); doesn't fire on R2V for some (`pryor74`). |
| **EasyCache** | ✓ Best *draft* tool, ~lossless vs final | params **(0.3, 0.2, 0.9)** + `res_multistep`/`simple` + **BlehTAEVideoDecode** (`infearia`, RTX 4060 Ti 16 GB, 1000+ clips tested). **Cannot combine with Turbo LoRAs** (skipped steps). ~100 s faster than Sage+Spectrum (`rookan`). |

### * 5.2 Real-world configs reported in the threads

| Hardware (thread) | Config | Reported time |
|---|---|---|
| RTX 5090 24 GB (`1vmjrc1`) | F2V/R2V GGUF, 4–6 steps, 0.8 MP, 8–12 s | 5–6 min |
| RTX 5090 (`1vn6czo`/KI_Gott) | 1.5 MP, 10 s, 12 steps, Turbo+Spectrum+Sol+Sage | 12 min (calls it the sweet spot) |
| RTX 5080 (`1vmcuq5`) | pruned INT8 + 32B NVFP4, 8-step Turbo, Sage+Spectrum, **CUDA 13** | 300 s @1 MP (was ~20–60 min on CUDA 12.6) |
| RTX 4080 (`atakariax`) | `--use-ck-attention` instead of Sage | "way lower" than the 4080S above |
| RTX 4070 12 GB (`1vmprjh`) | 0.3 MP draft, 8–13 steps | couple min; ~40 min for high-res finals |
| RTX 3060 12 GB (`1vmbkza`/ImpossibleAd436) | Sage + 8-step LoRA, 0.6 MP | ~6 min / 5 s |
| RTX 3060 12 GB + 64 GB (`LightVelox`) | Turbo + Spectrum + Sage, 480p | 3–5 min / 5 s; 8–10 min / 10 s |
| RTX 3060 12 GB + 64 GB (`janosdios`) | int8 convrot, Sage only, 0.2 MP 5 s | 3 min; 0.9 MP 5 s = 24 min |
| RTX 3060 12 GB (`1vmjdiw`) | 832×480, 10 s | 15 st → 7m22s / 20 st → 8m25s / 25 st → 10m30s |
| RTX 4060 laptop 8 GB (`1vme61d`) | Ref2VA INT8 ConvRot + Qwen3-VL 32B NVFP4-AWQ + Sage 2.2, 0.4 MP, 20 steps | works, no Turbo |
| RTX 3050 6 GB + 24 GB (`1vml6rh`) | INT4 ConvRot + INT4 clip + int8 VAE + Turbo v4 8 st euler/beta | 0.2 MP 10 s ≈ 5 min; 0.3 MP 10 s ≈ 10 min |
| RTX 4050 6 GB (`1vlqwme`) | INT4/8 ConvRot + nvfp4 + Turbo v4 step600 | ~300 s+ / 7 s (then HW failure) |
| DGX Spark GB10 (`1vm9mx6`) | FL2VA INT8 + Sol Engine + 2× RealESRGAN (360→720p) | 2m25s / 5 s @720p |
| M5 Air 16 GB (`1vm6ous`) | VPIPE, 0.5 MP, 8 DiT steps | ~15 min / 3.75 s |
| M4 Max 36 GB (`1vm6ous`) | VPIPE, 960×544, 90 fr, 8 steps, ext. SSD | 19m16s cold start |

### * 5.3 What the community converged on

* **Two-stage draft → final workflow** (nearly every thread, `1vmprjh`): *Draft* at 0.2–0.4 MP, 8–13 steps, **Turbo LoRA OR EasyCache (not both)**, `BlehTAEVideoDecode`. *Final*: disable acceleration, **20–32 steps**, standard `VAE Decode`. Two equally fast draft recipes: Turbo+Sage, or Sage+EasyCache(0.3,0.2,0.9).
* **Step count:** Minimax team recommends **30–50 steps**; ComfyUI's 20 is a speed compromise. Ref2VA needs **≥20 steps** for decent audio (`smb3d`); 25 steps is a common floor (`1vmjdiw`). 32 steps improves audio/motion for only +15–20% time vs 20 (`GrayingGamer`). Several users say **no-LoRA 12 steps looks best** (`1vmnwf7`).
* **Audio degrades under Turbo** consistently (`pit_shickle`, `stinkyjim88`, `AlternativeAmoeba271`). Use Turbo for drafts, then re-run the same seed without it for clean audio.
* **Sage vs Comfy Kitchen:** `ck-attention` reportedly faster/cleaner than Sage on some 40/50-series rigs — both are drop-in.
* **VAE-decode stuck at 0 %:** swap to **Kijai int8 video VAE** (`optimisticalish`, `Lucaspittol`); add a **"Clean VRAM" node before VAE Decode** to stop OOM (`Ill_Initiative_8793`, `infearia`).
* **System freeze on short clips** (`1vmdu5i`, eGPU/24 GB): fix with **`--disable-pinned-memory`** (`Chemical-Painter-485`), **`--vram-headroom`**, a Clear-VRAM node, drop a 4K/ultrawide display to 1080p, and disable extra monitors. "Reserve VRAM" alone didn't help.
* **Resolution/VRAM quirk:** longer clips can use *less* VRAM because ComfyUI offloads the model out of VRAM — counter-intuitive but reported repeatedly.
* **Ref2V is "brutal" on modest VRAM** vs T2V (`1vmprjh`); use fewer reference images / a 5070 Ti+ class card.
* **Low-VRAM laptop risk:** an RTX 4050 6 GB owner's GPU died after sustained loads (`1vlqwme`). Cool it, underclock, throttle at 85 °C; desktop > laptop.

### * 5.4 Per-thread index (your 17 reference links)

| ID | Hardware | One-line takeaway |
|---|---|---|
| `1vlqwme` | RTX 4050 6 GB | GPU physically failed under sustained load; INT4/8 ConvRot + Turbo v4 step600 build noted |
| `1vm6ous` | 16 GB Mac | VPIPE (Metal) runs H3 on M5 Air 16 GB (~15 min/3.75 s); M4 Max 36 GB = 19m16s; Turbo LoRA WIP |
| `1vm9mx6` | DGX Spark | 6.03× speedup: gen 360p then 2× RealESRGAN to 720p (2m25s/5 s) |
| `1vmbkza` | RTX 3060 | VAE-decode-stuck fix = Kijai int8 VAE; Turbo+Spectrum+Sage = 3–5 min/5 s |
| `1vmcuq5` | RTX 4080 Super | CUDA 13 cut 1 MP 5 s from ~20–60 min → 300 s |
| `1vmdu5i` | 24 GB eGPU | Short-clip freeze → `--disable-pinned-memory` / `--vram-headroom` / Clear VRAM |
| `1vme61d` | RTX 4060 8 GB | Ref2VA INT8 ConvRot + Qwen3-VL 32B NVFP4-AWQ + Sage 2.2, 20 steps, no Turbo |
| `1vmhclp` | RTX 3060 12 GB | 8-step+0.6 MP ≈ 6 min; GGUF w4a8 7 s@0.4 = 9 min; Maestro/Pinokio alt UI |
| `1vmilbn` | 5090 / 4060 Ti | Spectrum needs 30–50 steps; EasyCache(0.3,0.2,0.9) draft recipe |
| `1vmipni` | 32 GB RAM-only iGPU | Not viable on Arc iGPU; use `--fast-disk` or cloud (h3zero/Modal $30/mo) |
| `1vmjdiw` | 12 GB / 32 GB | 25 steps minimum; 15/20/25 @832×480 10 s timings; two-stage draft→Turbo refine |
| `1vmjrc1` | RTX 5090 | 4–6 steps, 0.8 MP, 8–12 s = 5–6 min (F2V/R2V GGUF workflows) |
| `1vml6rh` | 6 GB low VRAM | INT4 ConvRot build, 0.2–0.3 MP = 5–10 min; Context Loop stitching |
| `1vmnwf7` | 3090 Ti 64 GB | Settings comparison; 20 steps min for Ref2VA audio; no-LoRA 12 steps looked best |
| `1vmprjh` | 4070/5070/5080 | Budget-card consolidation: 4 levers + two-stage draft→final |
| `1vn6czo` | mixed | Community steps/seconds survey (5090/3090/5080/3060 numbers) |
| `1vn6p3f` | mixed | 4-step LoRA confusion (lightx2v vs joyfox vs kijai); many can't beat 20-step quality |

([back to top](#readme-top))

<p align="center">◈ ━━━━━━━━━━━ ◈</p>

## ❯ Caveats & Licensing

> [!IMPORTANT]
> **License — MiniMax H3 Community License:** non-commercial use free. Commercial use allowed *with attribution* only if trailing-12-month revenue < **US$20 M**; larger orgs need a separate MiniMax agreement. The license **excludes the US, EU, UK, and South Korea** and restricts display of outputs outside the applicable territory. Verify before any commercial/display use.

* **6 GB is now community-verified** (§3 "6 GB class" / §5 `1vml6rh`) with INT4 ConvRot + ≥24 GB RAM, but OOMs above ~0.4 MP and carries laptop hardware-failure risk. **8 GB works** with INT4/INT8 ConvRot + ≥32 GB RAM + reduced frames/res.
* **Audio VAE must be fp32** (fp16 causes A/V desync). Keep VAE/encoder separate from UNet VRAM to avoid double-load OOM.

([back to top](#readme-top))

<p align="center">◈ ━━━━━━━━━━━ ◈</p>

## ❯ References

* [MiniMax H3 Turbo Eval grid (jo-nike)](https://jo-nike.github.io/h3-turbo-eval/)
* [minimax-h3-turbo-lora-benchmark (sepiablue-ai, GitHub)](https://github.com/sepiablue-ai/minimax-h3-turbo-lora-benchmark)
* [MiniMax H3 on DGX Spark / GB10 (Xplore-LAB, GitHub)](https://github.com/Xplore-LAB/minimax-h3-dgx-spark)
* [MiniMax-H3-DGX-Spark, vLLM-Omni FP8 (joeynyc, GitHub)](https://github.com/joeynyc/MiniMax-H3-DGX-Spark)
* [MiniMax-H3-12GB-ComfyUI-Guide (shiqikuangsan31, GitHub)](https://github.com/shiqikuangsan31/MiniMax-H3-12GB-ComfyUI-Guide)
* [minimax-h3-mac, Apple Silicon MLX (Argus-AiTeam, GitHub)](https://github.com/Argus-AiTeam/minimax-h3-mac)
* [MiniMax H3 GGUF — quant levels & low-VRAM setup](https://minimaxh3.co/open-source/gguf)
* [MiniMax H3 Requirements: VRAM, GPU & File Sizes (2026)](https://www.oflight.co.jp/en/columns/minimax-h3-requirements-vram-local-2026)
* [MiniMax H3 8GB VRAM local deployment tutorial](https://iaipie.com/minimax-h3%E6%9C%AC%E5%9C%B0%E9%83%A8%E7%BD%B2%E6%89%8B%E6%8A%8A%E6%89%8B%E6%95%99%E7%A8%8B%EF%BC%9A8gb%E6%98%BE%E5%AD%98%E8%B7%91%E9%80%9A%E5%B8%A6%E9%9F%B3%E6%95%88%E7%9A%84ai%E8%A7%86%E9%A2%91/)
* [MiniMax H3 community quants (comfyui-wiki)](https://comfyui-wiki.com/zh/news/2026-08-03-minimax-h3-community-quants)
* [RTX 4080 local MiniMax H3 guide (zhihu)](https://zhuanlan.zhihu.com/p/2069412622559196107)
* [RTX 3060 12GB INT4 MiniMax H3 (zhihu)](https://zhuanlan.zhihu.com/p/2067934308715721983)

### * Reddit community field reports
* [1vlqwme — MiniMax H3 burned my GPU, beware on low VRAM (RTX 4050 6 GB)](https://www.reddit.com/r/StableDiffusion/comments/1vlqwme/)
* [1vm6ous — MiniMax H3 on a 16GB Mac with VPIPE](https://www.reddit.com/r/StableDiffusion/comments/1vm6ous/)
* [1vm9mx6 — Single DGX Spark T2V Benchmark, 6.03× half-res + 2× upscale](https://www.reddit.com/r/StableDiffusion/comments/1vm9mx6/)
* [1vmbkza — MiniMax H3 for RTX 3060, optimization help](https://www.reddit.com/r/StableDiffusion/comments/1vmbkza/)
* [1vmcuq5 — Need optimisation for MiniMax on my 4080 Super](https://www.reddit.com/r/StableDiffusion/comments/1vmcuq5/)
* [1vmdu5i — Computer unusable during short H3 videos (VRAM/freeze)](https://www.reddit.com/r/StableDiffusion/comments/1vmdu5i/)
* [1vme61d — Best H3 workflow for RTX 4060 Laptop GPU (8 GB)](https://www.reddit.com/r/StableDiffusion/comments/1vme61d/)
* [1vmhclp — RTX 3060 - 32GB and H3](https://www.reddit.com/r/StableDiffusion/comments/1vmhclp/)
* [1vmilbn — Sage + Spectrum in H3](https://www.reddit.com/r/StableDiffusion/comments/1vmilbn/)
* [1vmipni — Can MiniMax H3 run on 32 GB RAM only? (iGPU)](https://www.reddit.com/r/StableDiffusion/comments/1vmipni/)
* [1vmjdiw — MiniMax H3, 25 steps should be the lowest setting](https://www.reddit.com/r/StableDiffusion/comments/1vmjdiw/)
* [1vmjrc1 — M3 R2V / speed workflows (5090, 4–6 steps)](https://www.reddit.com/r/StableDiffusion/comments/1vmjrc1/)
* [1vml6rh — MiniMax H3 on a 6 GB low VRAM tests](https://www.reddit.com/r/StableDiffusion/comments/1vml6rh/)
* [1vmnwf7 — MiniMax H3 Settings Comparison (3090 Ti)](https://www.reddit.com/r/StableDiffusion/comments/1vmnwf7/)
* [1vmprjh — MiniMax H3 on a Budget: 4070/5070/5080 consolidation](https://www.reddit.com/r/StableDiffusion/comments/1vmprjh/)
* [1vn6czo — How many steps and seconds is everyone doing for MiniMax?](https://www.reddit.com/r/StableDiffusion/comments/1vn6czo/)
* [1vn6p3f — minimax h3 4-step LoRA confusion (lightx2v vs joyfox vs kijai)](https://www.reddit.com/r/StableDiffusion/comments/1vn6p3f/)

([back to top](#readme-top))
