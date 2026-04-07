# RUPA — रूप

**Image & Video Generation Lab**

Part of the [Spanda](https://github.com/Hitata/spanda) ecosystem.

-----

## What is Rupa?

Rupa (रूप) = **Form.** Sanskrit for everything visible — shape, color, appearance. In Buddhist philosophy, Rupa (Sắc) is the first of the Five Aggregates: the material layer of experience.

In this context: **Rupa is where AI learns to make the invisible visible.**

-----

## What's Inside

### 1. Face Generation

Training AI to generate human faces across styles and expressions.

- Photorealistic portraits
- Stylized faces (illustration, anime, painterly)
- Expression control — emotion, angle, lighting
- Ethnicity and feature diversity
- Face consistency across multiple outputs (same character, different poses)

### 2. Body & Figure

Full human figure generation — beautiful men and women.

- Full-body poses and proportions
- Anatomy accuracy across body types
- Fashion and clothing generation
- Figure composition in scenes
- Male and female aesthetic exploration

### 3. Martial Arts Decomposition

Breaking down martial arts video into learnable visual segments.

- **Input**: martial arts videos (Facebook, YouTube, other sources)
- **Process**: extract key frames → identify distinct movements → segment into practice sections
- **Output**: visual breakdowns of forms and techniques
- **Focus styles**: Tai Chi (Thái Cực Quyền), Kung Fu, other traditional arts
- **Goal**: turn flowing video into structured, practicable visual sequences

### 4. Style Exploration

Learning different visual languages and rendering approaches.

| Style               | Description                       |
|----------------------|-----------------------------------|
| Photorealistic       | Lifelike human rendering          |
| Cartoon / Toon       | Simplified, expressive, stylized  |
| Anime / Manga        | Japanese illustration conventions |
| Oil painting         | Classical fine art aesthetic       |
| Ink wash / Thuỷ mặc  | East Asian brush painting         |
| Mixed                | Hybrid and experimental styles    |

### 5. Image → Video (Future)

Evolution from still image to motion.

- Still character → animated movement
- Martial arts stills → flowing practice sequences
- Style-consistent video generation

-----

## Training Pipeline

```
┌─────────────┐     ┌──────────────┐     ┌─────────────┐
│  Data Input  │ ──▶ │   Training   │ ──▶ │   Output    │
│             │     │              │     │             │
│ • Photos    │     │ • Fine-tune  │     │ • Faces     │
│ • Videos    │     │ • LoRA       │     │ • Figures   │
│ • Styles    │     │ • Prompting  │     │ • Movements │
│ • MA clips  │     │ • Segmenting │     │ • Styles    │
└─────────────┘     └──────────────┘     └─────────────┘
```

-----

## Tools & Models (to explore)

- **Stable Diffusion / SDXL** — base image generation
- **ComfyUI** — node-based workflow for complex pipelines
- **LoRA training** — fine-tune on specific faces, styles, characters
- **ControlNet** — pose control, depth mapping (critical for martial arts)
- **MediaPipe / OpenPose** — skeleton extraction from martial arts video
- **AnimateDiff** — still → video extension
- **Deforum** — animation from prompts

-----

## Repo Structure

```
rupa/
├── README.md
├── faces/
│   ├── training-data/
│   ├── models/
│   └── outputs/
├── figures/
│   ├── training-data/
│   ├── models/
│   └── outputs/
├── martial-arts/
│   ├── source-videos/
│   ├── extracted-frames/
│   ├── pose-maps/
│   └── practice-sequences/
├── styles/
│   ├── references/
│   ├── lora-models/
│   └── outputs/
└── experiments/
    └── video-gen/
```

-----

## Learning Journal

This repo is a **learning journey** — documenting the process of mastering generative AI for visual creation. Expect experiments, failures, iterations, and breakthroughs.

-----

*Rupa — from vibration to visible form.*
