# AI Image & Video Generation: Model Landscape (Early 2026)

**Research for Rupa -- Image & Video Generation Lab**

Last updated: April 2026

---

## Table of Contents

1. [Executive Summary](#executive-summary)
2. [Image Generation -- Local Models](#image-generation--local-models)
3. [Image Generation -- Freemium / API Services](#image-generation--freemium--api-services)
4. [Video Generation -- Local Models](#video-generation--local-models)
5. [Video Generation -- Freemium / API Services](#video-generation--freemium--api-services)
6. [Pose Estimation & Skeleton Extraction](#pose-estimation--skeleton-extraction)
7. [Workflow Engines & Training Tools](#workflow-engines--training-tools)
8. [Recommendations by Rupa Goal](#recommendations-by-rupa-goal)
9. [Hardware Reference](#hardware-reference)

---

## Executive Summary

The AI generation landscape in early 2026 has matured significantly. Key trends:

- **Flux has overtaken Stable Diffusion** as the preferred local image model for most use cases, though SD3.5 retains strengths in portraits and typography.
- **Open-source video models** (HunyuanVideo 1.5, Wan 2.2, Mochi 1) have narrowed the gap with closed services dramatically.
- **ComfyUI** is the dominant workflow engine, now supporting image, video, audio, and 3D generation with a simplified App View alongside the node editor.
- **LoRA training** on consumer hardware (12GB+) is practical for both SDXL and Flux, enabling custom face/style models.
- **API services** remain valuable for speed, convenience, and access to models too large for consumer GPUs.

---

## Image Generation -- Local Models

### Stable Diffusion Family

| Model | Parameters | VRAM (Min) | VRAM (Comfortable) | License | Quality | Speed | Notes |
|-------|-----------|------------|---------------------|---------|---------|-------|-------|
| **SD 1.5** | 860M | 4 GB | 6 GB | CreativeML Open RAIL-M | Good (dated) | Fast | Massive LoRA/checkpoint ecosystem. Still useful for experimentation. |
| **SDXL** | 3.5B | 6 GB | 8-12 GB | Open RAIL++ | Very Good | Moderate | Best ecosystem of fine-tunes, LoRAs. Solid for faces and figures. |
| **SDXL Turbo / Lightning** | 3.5B (distilled) | 6 GB | 8 GB | Varies | Good | Very Fast (1-4 steps) | Real-time generation. Quality sacrifice vs full SDXL. |
| **SD 3.5 Medium** | 2.5B | 8 GB | 12 GB | Open, commercial OK | Very Good | Moderate | Best "daily driver" -- runs on consumer hardware, good prompt adherence. |
| **SD 3.5 Large** | 8B | 10 GB (FP8) | 12-16 GB | Open, commercial OK | Excellent | Moderate | Best for typography and multi-subject coherence. Better portrait skin textures than Flux. |
| **SD 3.5 Large Turbo** | 8B (distilled) | 8 GB (FP8) | 12 GB | Open, commercial OK | Very Good | Fast | Good balance of quality and speed. |

**Strengths for Rupa:** SD3.5 has excellent portrait aesthetics with refined skin textures. SDXL has the largest LoRA ecosystem for face consistency training. SD 1.5 still has ControlNet models not yet ported to newer architectures.

### Flux (Black Forest Labs)

| Model | Parameters | VRAM (Min) | VRAM (Comfortable) | License | Quality | Speed | Notes |
|-------|-----------|------------|---------------------|---------|---------|-------|-------|
| **Flux.1 Schnell** | 12B | 6 GB (quantized) | 12 GB | Apache 2.0 | Very Good | Fast (4 steps) | Fully open, commercial use. Best speed/quality ratio. |
| **Flux.1 Dev** | 12B | 12 GB (FP8/NF4) | 24 GB (full) | Non-commercial | Excellent | Moderate (20 steps) | Near-Pro quality. Superior text rendering. Open weights. |
| **Flux.1 Pro** | 12B+ | API only | API only | Commercial API | Excellent | Moderate | Best prompt adherence and coherence. API-dependent. |

**Strengths for Rupa:** Flux excels at high-resolution detailed images, text rendering, and prompt adherence. Flux.1 Schnell with Apache 2.0 is ideal for commercial workflows. ControlNet and IP-Adapter support now available for Flux in ComfyUI.

### Other Notable Local Image Models

| Model | What It Does | VRAM | License | Notes |
|-------|-------------|------|---------|-------|
| **Illustrious XL** | Anime/illustration focused | 8-12 GB | Open | Fork of SDXL tuned for anime. Strong community. |
| **Pony Diffusion** | Stylized/character generation | 8-12 GB | Open | Popular for character consistency. |
| **PixArt-Sigma** | Text-to-image (DiT) | 8-16 GB | Open | Efficient transformer-based model. |

---

## Image Generation -- Freemium / API Services

### Midjourney

| Aspect | Details |
|--------|---------|
| **Pricing** | Basic: $10/mo (200 images), Standard: $30/mo (unlimited relax), Pro: $60/mo (stealth mode), Mega: $120/mo |
| **Annual discount** | 20% off all tiers |
| **Quality** | Industry-leading aesthetic quality, especially for artistic/stylized output |
| **Customization** | Limited -- no LoRA, no ControlNet. Style/character references via image prompts. No API (Discord/web only). |
| **Privacy** | All images public unless Pro/Mega (stealth mode). Images on Midjourney servers. |
| **Speed** | Fast in fast mode, 0-10 min queue in relax mode |
| **Strengths for Rupa** | Excellent for style exploration, artistic references, and quick concept iteration. Weak for pose control and face consistency. |

### OpenAI Image Generation (GPT Image / DALL-E)

| Aspect | Details |
|--------|---------|
| **Models** | GPT Image 1.5 (latest), GPT Image 1, GPT Image 1 Mini. DALL-E 3 deprecated. |
| **API Pricing** | $0.005-0.20 per image depending on model/quality/size |
| **ChatGPT Access** | Included in ChatGPT Plus ($20/mo) and Pro ($200/mo) subscriptions |
| **Quality** | Good photorealism, excellent prompt understanding, strong text rendering |
| **Customization** | No LoRA, no pose control. Inpainting/editing supported. |
| **Privacy** | Data processed on OpenAI servers. Subject to content policy. |
| **Strengths for Rupa** | Excellent for quick prototyping via ChatGPT. API useful for programmatic generation. Very affordable per-image. |

### Leonardo.ai

| Aspect | Details |
|--------|---------|
| **Free Tier** | 150 tokens/day (~20-30 images). Public by default. No commercial rights. |
| **Paid Plans** | Apprentice: $10/mo (8,500 tokens), Artisan: $24/mo, Maestro: $48/mo (60,000 tokens) |
| **Quality** | Very good. Multiple model options including their own fine-tunes. |
| **Customization** | ControlNet support, custom model training on paid plans, style presets |
| **Privacy** | Cloud-based. Private generations on paid plans only. |
| **Strengths for Rupa** | Generous free tier for experimentation. ControlNet for pose control. Custom model training for face consistency. Good middle ground between ease-of-use and control. |

### Ideogram

| Aspect | Details |
|--------|---------|
| **Free Tier** | Limited monthly generations |
| **Paid Plans** | Plus: $20/mo (1,000 credits), Pro: $60/mo (3,500 credits), Teams: $30/user/mo |
| **Quality** | Excellent, especially for text-in-image (logos, banners, typography) |
| **Customization** | Magic Prompt enhancement, batch generation (Pro), background control |
| **Privacy** | Cloud-based |
| **Strengths for Rupa** | Best-in-class text rendering in images. Good for style exploration with readable text overlays. |

### Stability AI API

| Aspect | Details |
|--------|---------|
| **Credit System** | 1 credit = $0.01. Sold in bundles of 1,000 credits ($10). |
| **Models & Pricing** | Stable Image Ultra: $0.08/image, Stable Image Core: $0.03/image, SD 3.5 Large: $0.065/image, SD 3.5 Large Turbo: $0.04/image |
| **Quality** | Very good to excellent depending on model |
| **Customization** | ControlNet support via API, style presets |
| **Strengths for Rupa** | Affordable per-image. Good for accessing SD models without local GPU. |

### Replicate

| Aspect | Details |
|--------|---------|
| **Pricing** | Pay-per-second of GPU time. SDXL ~$0.03-0.04/image. Flux Dev ~$0.03/image. |
| **Quality** | Depends on model chosen -- hosts many open-source models |
| **Customization** | Can run any model, including custom LoRAs. Full ControlNet support. |
| **Privacy** | Cloud-based. Images processed on Replicate infra. |
| **Strengths for Rupa** | Run any open-source model without local GPU. Good for LoRA inference and ControlNet workflows. Slightly more expensive than fal.ai. |

### fal.ai

| Aspect | Details |
|--------|---------|
| **Pricing** | Output-based. Flux Dev ~$0.025/image, Flux Pro ~$0.05/image. 30-50% cheaper than Replicate. |
| **Quality** | Same as underlying model |
| **Customization** | Supports LoRA, ControlNet, IP-Adapter via API |
| **Privacy** | Cloud-based |
| **Strengths for Rupa** | Cheapest API option for running open models. 4x faster inference claims. Good for batch generation. |

---

## Video Generation -- Local Models

### Tier 1: High-End (40GB+ VRAM or Cloud GPU)

| Model | Developer | VRAM | Duration | Resolution | License | Quality | Notes |
|-------|-----------|------|----------|------------|---------|---------|-------|
| **HunyuanVideo 1.5** | Tencent | 14 GB (w/ offloading), 80 GB+ (native) | Variable | Up to 720p | Open | Excellent | Best open-source for motion realism and instruction following. 8.3B params (down from 13B). |
| **Wan 2.2** | Alibaba | 40 GB (FP8), 48-55 GB (full) | Variable | Up to 720p | Open | Excellent | Most cinematic open-source model. Mixture-of-Experts architecture. |
| **Mochi 1** | Genmo AI | 40 GB+ | Variable | Up to 720p | Apache 2.0 | Very Good | 10B params. Best licensing clarity for commercial use. |
| **Open-Sora 2.0** | Community | 40 GB+ | Variable | Variable | Open | Very Good | 11B params. Aims to replicate Sora capabilities. |

### Tier 2: Consumer-Friendly (8-24 GB VRAM)

| Model | Developer | VRAM | Duration | Resolution | License | Quality | Notes |
|-------|-----------|------|----------|------------|---------|---------|-------|
| **AnimateDiff** | Community | 8 GB | 2-4 sec | 512x512 to 768x768 | Apache 2.0 | Good | Extends SD to video. Most accessible. Works with SD LoRAs. |
| **CogVideoX-2B** | Tsinghua/Zhipu | 8-12 GB | 6 sec | 720x480 @ 8fps | Open | Good | Lighter variant for consumer GPUs. |
| **CogVideoX-5B** | Tsinghua/Zhipu | 16-24 GB | 6 sec | 720x480 @ 8fps | Open | Very Good | Better quality, still manageable on 24GB. |
| **Wan 2.1 T2V-1.3B** | Alibaba | 8 GB | Short | 480p | Open | Moderate | Smallest variant, runs on almost any GPU. |
| **Stable Video Diffusion (SVD XT)** | Stability AI | 16-24 GB | ~4 sec (25 frames) | 576x1024 | Open | Good | Image-to-video. 25 frames at 576x1024. |
| **LTX Video 2.3** | Lightricks | 12-24 GB | Variable | Up to 4K @ 50fps | Open | Very Good | Audio-synced video. Native ComfyUI support. |

### Tier 3: Emerging / Experimental

| Model | Notes |
|-------|-------|
| **Wan2GP** | Optimized runner for Wan 2.1/2.2, HunyuanVideo, LTX, Flux on low-VRAM GPUs |
| **Text2Video-Zero** | Zero-shot video from text, minimal VRAM |

**Key takeaway for Rupa:** For martial arts video decomposition (input, not generation), you do not need generative video models -- you need pose estimation tools (see below). For image-to-video output, AnimateDiff (8GB) or CogVideoX-2B (12GB) are the most accessible starting points. HunyuanVideo 1.5 or Wan 2.2 deliver the best quality but need cloud GPUs or high-end local hardware.

---

## Video Generation -- Freemium / API Services

| Service | Free Tier | Paid Plans | Quality | Duration | Special Features | Best For |
|---------|-----------|------------|---------|----------|------------------|----------|
| **Runway ML** | 125 one-time credits | Standard: $12/mo, Pro: $28/mo (2,250 credits), Unlimited: $76/mo | Excellent (Gen-4/4.5) | 5-15 sec | Motion brush, camera control, lip sync | Professional video with precise control |
| **Pika Labs** | Free tier with limits | From $8/mo (annual), Pro: $35/mo (2,300 credits) | Very Good (Pika 2.0) | 5 sec | Sound effects, lip sync, modify regions | Affordable entry point, 1080p output |
| **Kling AI** | Daily free credits | Standard: ~$10/mo, Pro: ~$36/mo | Very Good | 5-10 sec | Good motion quality | Budget-friendly with free daily access |
| **Luma Dream Machine** | Limited free | Lite: $8/mo, Standard: $10/mo (150 gens), Plus: $21/mo, Pro: $95/mo (unlimited) | Very Good | 5 sec | Image-to-video, text-to-video | Affordable image-to-video |
| **Stability AI API** | Via credits | Per-generation pricing | Good (SVD-based) | 4 sec | Image-to-video via API | Programmatic video generation |

**Strengths for Rupa:** Runway ML offers the most control (motion brush, camera). Pika is the most affordable per-video. Kling has the most generous free tier. Luma is best for image-to-video specifically.

---

## Pose Estimation & Skeleton Extraction

Critical for Rupa's martial arts decomposition pipeline.

### MediaPipe (Google)

| Aspect | Details |
|--------|---------|
| **Keypoints** | 33 body landmarks (more than OpenPose) |
| **Approach** | Top-down (detect person first, then keypoints) |
| **Speed** | Real-time on CPU. Very fast. |
| **3D Support** | Yes -- provides 3D coordinates |
| **Platform** | Cross-platform (Python, JS, Android, iOS) |
| **VRAM** | None required -- runs on CPU |
| **License** | Apache 2.0 |
| **Best for** | Single-person tracking, real-time processing, mobile deployment |

### OpenPose (CMU)

| Aspect | Details |
|--------|---------|
| **Keypoints** | 18 body + 21 per hand + 70 face = 135 total |
| **Approach** | Bottom-up (detect parts, then assemble) |
| **Speed** | Slower than MediaPipe, benefits from GPU |
| **3D Support** | Limited |
| **Platform** | C++/Python, CUDA GPU recommended |
| **VRAM** | 2-4 GB recommended |
| **License** | Non-commercial research only (AGPL for commercial) |
| **Best for** | Multi-person pose estimation, ControlNet integration |

### DWPose / RTMPose

| Aspect | Details |
|--------|---------|
| **Notes** | Modern alternatives gaining traction in ComfyUI ecosystem |
| **Quality** | Often higher accuracy than OpenPose |
| **Integration** | Native ComfyUI nodes available |
| **Best for** | ControlNet pose conditioning in generation workflows |

### Recommended Pipeline for Martial Arts Decomposition

```
Source Video
    |
    v
FFmpeg (frame extraction at configurable FPS)
    |
    v
MediaPipe Pose (33 keypoints, 3D, real-time)
  or
OpenPose (if multi-person needed)
  or
DWPose (if feeding into ControlNet)
    |
    v
Skeleton Visualization + Keypoint Data (JSON)
    |
    v
Segment into movement phases (custom logic)
    |
    v
ControlNet conditioning (for regeneration/style transfer)
```

---

## Workflow Engines & Training Tools

### ComfyUI

| Aspect | Details |
|--------|---------|
| **What** | Node-based visual workflow engine for AI generation |
| **Supports** | Image, video, audio, 3D generation |
| **Interface** | Dual mode: simplified App View + full Node View |
| **Performance** | 40% faster on RTX GPUs (2025 updates), 2.5x faster with RTX 50-series NVFP4 |
| **Video Models** | AnimateDiff, SVD, CogVideoX, Wan, HunyuanVideo, LTX 2.3 |
| **ControlNet** | Full support for SD, SDXL, Flux variants |
| **IP-Adapter** | Supported for face/style transfer |
| **Why essential** | The hub that connects all local models into pipelines |

### Kohya-ss / sd-scripts

| Aspect | Details |
|--------|---------|
| **What** | Industry-standard LoRA/fine-tuning tool |
| **Supports** | SD 1.5, SDXL, SD3.5, Flux LoRA training |
| **VRAM for SDXL** | 8 GB minimum (with optimizations), 12 GB comfortable |
| **VRAM for Flux** | 12 GB minimum (quantized), 24 GB comfortable |
| **Face training** | 15-50 high-quality images, 1000-3000 steps |
| **Key optimizations** | Pre-encode VAE, pre-compute text encoders, LoRA+ (16x ratio) |

### LoRA + ControlNet + IP-Adapter Combined Workflow

This is the power combo for Rupa's face/figure consistency goals:

- **LoRA**: Learns your character deeply (face, style). Most reliable for consistency across poses/expressions.
- **ControlNet**: Controls pose, depth, edges. Critical for martial arts pose recreation.
- **IP-Adapter / FaceID**: Quick face transfer from reference images. Combines InsightFace embeddings with LoRA.

Training a character LoRA: 15-50 images, diverse angles/lighting, 1000-3000 steps on Kohya. Then combine with ControlNet for pose control at inference time.

---

## Recommendations by Rupa Goal

### 1. Face Generation (Photorealistic + Stylized)

| Approach | Tool | Why |
|----------|------|-----|
| **Local (primary)** | Flux.1 Dev + face LoRA (Kohya) | Best quality + customization. Train LoRA for consistent characters. |
| **Local (fast)** | Flux.1 Schnell | Apache 2.0, 4-step generation for rapid iteration. |
| **Local (portraits)** | SD 3.5 Large | Superior skin textures and portrait aesthetics. |
| **API (exploration)** | Midjourney | Best aesthetic quality for style references. |
| **API (programmatic)** | fal.ai (Flux Dev) | Cheapest API, supports LoRA. |
| **Face consistency** | IP-Adapter FaceID + trained LoRA | Combine for best results. |

### 2. Full Body / Figure Generation

| Approach | Tool | Why |
|----------|------|-----|
| **Local** | Flux.1 Dev or SDXL + ControlNet (pose) | ControlNet for anatomy accuracy. LoRA for style. |
| **Pose control** | ControlNet OpenPose/DWPose | Feed skeleton data to control pose precisely. |
| **API** | Leonardo.ai | ControlNet support in a friendly interface. |
| **Exploration** | Midjourney | Excellent aesthetic composition for figures. |

### 3. Martial Arts Video Decomposition

| Step | Tool | Notes |
|------|------|-------|
| **Frame extraction** | FFmpeg | Extract at 24-30fps or key frames only |
| **Pose estimation** | MediaPipe Pose | 33 keypoints, 3D, runs on CPU, real-time. Free. |
| **Multi-person** | OpenPose | If video has multiple practitioners |
| **Skeleton viz** | OpenCV + custom rendering | Draw skeleton overlays on frames |
| **Movement segmentation** | Custom Python logic | Detect transitions via keypoint velocity/acceleration |
| **Style transfer** | ControlNet (DWPose) + style LoRA | Regenerate movements in ink wash, anime, etc. |

### 4. Style Exploration

| Style | Recommended Approach |
|-------|---------------------|
| **Photorealistic** | Flux.1 Dev (local) or Midjourney (cloud) |
| **Anime/Manga** | Illustrious XL or SDXL anime LoRAs (local) |
| **Ink wash / Thuy mac** | SD 3.5 or Flux + ink wash style LoRA (train custom) |
| **Oil painting** | Midjourney (excellent) or SDXL + painting LoRA |
| **Cartoon/Toon** | SDXL + toon LoRAs (huge community selection) |
| **Mixed/Experimental** | ComfyUI workflow blending multiple LoRAs + IP-Adapter |

### 5. Image-to-Video Generation

| Budget | Tool | Notes |
|--------|------|-------|
| **8 GB VRAM** | AnimateDiff | Most accessible. Works with existing SD LoRAs. Short clips. |
| **12-16 GB** | CogVideoX-2B / LTX Video | Better quality, longer clips. |
| **24 GB** | SVD XT / CogVideoX-5B | Good quality image-to-video. |
| **Cloud GPU** | HunyuanVideo 1.5 / Wan 2.2 | Best quality. Rent A100/H100. |
| **API (easy)** | Luma Dream Machine | Best image-to-video API. From $8/mo. |
| **API (control)** | Runway ML | Motion brush, camera control. From $12/mo. |
| **API (budget)** | Pika Labs | $0.15 per 5-sec video. |

---

## Hardware Reference

### Recommended Local Setup for Rupa

| Tier | GPU | VRAM | What You Can Run |
|------|-----|------|------------------|
| **Entry** | RTX 3060 / 4060 Ti | 12 GB | SD 1.5, SDXL, SD3.5 Medium, Flux Schnell (quantized), AnimateDiff, SDXL LoRA training, MediaPipe |
| **Mid** | RTX 4070 Ti Super / 4080 | 16 GB | Everything above + SD3.5 Large, Flux Dev (quantized), CogVideoX-2B, SVD |
| **High** | RTX 4090 / 5090 | 24-32 GB | Everything above + Flux Dev (full), CogVideoX-5B, Flux LoRA training, most video models |
| **Cloud** | A100 / H100 (rent) | 80 GB | HunyuanVideo, Wan 2.2 (full), Mochi 1, Open-Sora 2.0 |

**Cost-effective cloud GPU rental:** RunPod, Vast.ai, Lambda Labs, Jarvislabs -- typically $1-3/hr for A100 80GB.

### Privacy Considerations

| Approach | Privacy Level | Notes |
|----------|--------------|-------|
| **Local models** | Full privacy | Nothing leaves your machine. Complete control. |
| **Replicate / fal.ai** | Low privacy | Images processed on their servers. Check data retention policies. |
| **Midjourney** | Low privacy | All images on MJ servers. Public unless stealth mode (Pro+). |
| **OpenAI** | Low privacy | Subject to content policy and potential training use. |
| **Leonardo.ai** | Low-Medium | Private on paid plans. |

For Rupa's martial arts content and personal face generation work, **local models are strongly recommended** for primary workflows, with API services used for exploration and quick prototyping.

---

## Cost Comparison Summary

### Monthly Budget Scenarios

**$0/mo (Local Only, own GPU):**
- All open-source models free
- ComfyUI free
- MediaPipe/OpenPose free
- Kohya training free
- Only cost: electricity + initial GPU investment

**~$30/mo (Hybrid):**
- Local for primary work
- Midjourney Standard ($30) for style exploration and references
- OR Leonardo Artisan ($24) + fal.ai pay-as-you-go (~$5)

**~$60/mo (Full Stack):**
- Local for training and private work
- Midjourney Pro ($60) for exploration with stealth mode
- OR Runway Pro ($28) + Midjourney Standard ($30) for image + video

**Pay-as-you-go API (Variable):**
- fal.ai: ~$0.025/image (cheapest)
- Replicate: ~$0.03-0.04/image
- OpenAI GPT Image: $0.005-0.20/image
- Stability API: $0.03-0.08/image

---

*This document reflects the landscape as of April 2026. The field moves rapidly -- revisit quarterly.*
