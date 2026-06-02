---
name: "illustration-prompt-exporter"
description: "Export prompt-ready illustration and screenshot instructions for academic PPTs. Use when a deck needs generated diagrams, screenshot guidance, visual prompt maps, or a standalone prompt file before TeX drafting."
---

# Illustration Prompt Exporter

Use this skill to turn a slide outline or visual plan into a standalone prompt document for generated diagrams and screenshots.

## When to Trigger
- The user asks for illustration prompts, generated figures, or screenshot instructions.
- A PPT plan contains several generated technical diagrams.
- The user wants to use nanobanana or another image-generation tool outside the TeX drafting step.
- The deck needs a separate prompt file such as `new-pic.md`, `illustration-prompts.md`, or `output/visual_prompts.md`.

## Inputs
- Markdown outline or page-level PPT plan
- Existing figure map
- Slide titles and speaking goals
- Style preferences from `presentation_personalization_requirements.md`
- Any existing generated images or screenshots

## Output File
Save a standalone markdown file when the user wants reusable prompts. Recommended path:

```text
output/illustration-prompts.md
```

If the user provides another filename, use it.

## Prompt Map Format
For each visual, include:
- slide title
- visual role: generated diagram / screenshot / source figure / table
- purpose: mechanism / comparison / workflow / evidence / concept bridge / risk flow
- recommended aspect ratio: `3:4`, `16:9`, or original crop
- target layout: side column / full-width top visual / full-slide visual / two-panel comparison
- image-text budget
- generation prompt or screenshot instruction
- post-processing note: labels to add in TeX, crop target, or regions to highlight

## Generated Diagram Rules
- Keep prompts portable across image-generation tools.
- Use a unified style instruction:
  `clean academic vector technical diagram, light background, thin lines, rounded rectangles, blue/teal/gray palette with subtle warm accents, minimal readable labels or placeholder labels, no decorative scene, no watermark, no logo`
- Prefer `3:4` for side-column visuals in Beamer templates.
- Use `16:9` for full-width overview diagrams, multi-lane workflows, comparison charts, taxonomy maps, and visual-led explanation pages.
- If the generator may render text poorly, request placeholder labels and add exact labels later in TeX.
- Do not ask for dense paragraphs inside the image. Put detailed wording in slide text.

## Screenshot Rules
- Use screenshots when authenticity matters: product UI, GitHub repositories, terminal output, real wiki pages, dashboards, and demos.
- Capture or crop only the region that proves the slide claim.
- Ensure the target region remains readable after insertion.
- Pair screenshot slides with only 1-3 bullets.
- If a screenshot is wide, plan top-bottom layout or full-width visual placement instead of squeezing it into a narrow side column.

## Markdown Template
```markdown
# Illustration Prompt Map

## Global Style
clean academic vector technical diagram, light background, thin lines, rounded rectangles, blue/teal/gray palette with subtle warm accents, minimal readable labels or placeholder labels, no decorative scene, no watermark, no logo

## Slide: <title>
- Visual role:
- Purpose:
- Aspect ratio:
- Target layout:
- Image/text budget:
- Prompt or screenshot instruction:
- Post-processing:
```

## Final Check
- Every generated image has an aspect ratio and layout target.
- Screenshot instructions name the exact region to capture.
- Wide visuals are not planned as cramped side-column images.
- Prompts do not depend on one specific image-generation service.
