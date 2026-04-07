# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

---

## What this project is

**Rupa (रूप) = Form.** An image & video generation lab — part of the [Spanda](https://github.com/Hitata/spanda) ecosystem.

Five focus areas:
1. **Face generation** — photorealistic + stylized portraits, expression control, face consistency
2. **Body & figure** — full human figures, anatomy, fashion, aesthetic exploration
3. **Martial arts decomposition** — break down video into learnable visual sequences (Tai Chi, Kung Fu)
4. **Style exploration** — photorealistic, anime, ink wash (Thuy mac), oil painting, mixed
5. **Image-to-video** — animated movement from stills (future)

**Primary tools:** Stable Diffusion / Flux, ComfyUI, LoRA training, ControlNet, MediaPipe, AnimateDiff.

---

## Repo structure

```
rupa/
├── faces/              # training-data, models, outputs
├── figures/            # training-data, models, outputs
├── martial-arts/       # source-videos, extracted-frames, pose-maps, practice-sequences
├── styles/             # references, lora-models, outputs
├── experiments/        # video-gen, spikes
├── research/           # landscape research, model comparisons
└── scripts/            # Python pipelines (pose extraction, frame processing, etc.)
```

---

## Python coding standards

Use the `python-standards` skill when writing or reviewing Python code.

---

## Readability & communication style

黄忠 is an ADHD-pattern reader. Minimize cognitive load in all output.

**5 rules:**
1. **TL;DR first** — the answer before the explanation. Always.
2. **One idea per chunk** — max 2-3 sentences per paragraph.
3. **Visual anchors** — **bold the key phrase** in each paragraph so scanning works.
4. **Progressive depth** — summary -> context -> detail. Reader stops when they've had enough.
5. **No walls of text** — if it looks dense, break it up.

**How Claude responds:**
1. **Answer first.** Then context if needed. Never lead with explanation.
2. **Suggest, don't explain.** "Do X" beats "you could do X or Y because..."
3. **Extract, don't clarify.** Voice dumps are raw signal — pull out the meaning.
4. **One question at a time.** Multiple questions = only the last gets answered.
5. **Link forward.** Don't recap. Point to what's next.
6. **Match his compression.** Short input = short output.

---

## Dispute resolution

When new information conflicts with a prior decision:
1. **Flag it** — don't silently override or ignore.
2. **Research** — gather context and alternatives.
3. **Bring to discussion** — present the conflict, findings, and your take. 黄忠 decides.

---

## Boundaries

This is a creative lab, not a client project. The register is personal and exploratory. Experiment freely, document what works.
