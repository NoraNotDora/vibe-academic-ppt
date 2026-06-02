---
name: "academic-ppt-planner"
description: "Plan academic paper presentation slides from a paper PDF and course requirements. Use whenever the user wants a paper turned into slides, needs a page-level outline, or asks how to map figures and claims into a talk before TeX drafting. Trigger this skill even if the user only says they need help making a paper presentation or slide plan."
---

# Academic PPT Planner

Use this skill to turn a paper, markdown outline, and presentation constraints into a page-level plan before anyone starts writing TeX.

## When to Trigger
- The user is starting a new academic PPT.
- The user wants slide pages outlined from a paper PDF or draft notes.
- The user has not yet written a deck outline and needs a low-friction starting point.
- The user needs duration, audience, or page-budget decisions before slide writing.
- The user asks how to map paper figures, sections, or claims into a presentation.

## Recommended User Entry Point
Before generating a full PPT, guide the user to write or approve a lightweight markdown outline. This keeps the deck aligned with the user's intended argument instead of letting the model invent the structure too early.

Ask for or create a draft `.md` outline with:
- title and target audience
- talk goal in one sentence
- section order
- slide titles or provisional slide goals
- required examples, figures, screenshots, or citations
- content that must be emphasized or avoided

Then convert the markdown outline into the full page plan, figure map, prompt map, and TeX skeleton. If the user only has rough notes, first normalize them into this outline format and ask for confirmation before drafting slides.

## Mandatory First Step
Before you outline slides, always output:
- Presentation goal in one sentence
- Target audience
- Duration and page constraints
- Core paper contributions (3-5 items)
- Must-cover figure list
- Generated-figure / screenshot strategy
- Risk list (formula density, unreadable figures, page overflow)

If duration or audience is missing, ask for it directly instead of guessing. The page budget and figure strategy depend on those constraints.

## Confirmation Ladder
Confirm requirements one step at a time before moving into outline writing.
- Ask the smallest useful question first when a major constraint is missing.
- Wait for the user's answer before locking the next stage.
- Do not bundle audience, duration, figure strategy, and outline emphasis into one broad question unless the user explicitly asks for that.
- Confirm the presentation goal, then audience, then duration, then page budget, then figure availability, then emphasis.
- If the paper contains multiple possible storylines, show the options and ask which one to prioritize before drafting the outline.

## Inputs to Inspect
- Paper PDF
- Course requirements or instructor notes
- User-provided markdown outline or rough notes
- Existing outline, if any
- Extracted figure files
- `skills/presentation_personalization_requirements.md`
- `skills/ppt_plan_template.md`

## Planning Workflow
1. Collect or draft the user's markdown outline before writing full slides.
2. Read the paper structure, section titles, key claims, and figure IDs.
3. Refine the requirements before drafting slides.
4. Pause for confirmation if a major decision is still ambiguous.
5. Build the storyline as problem -> method -> result -> conclusion.
6. Write a page-level outline with a page title, speaking goal, and one visual anchor for every page.
7. Map each key figure to a page and write one sentence explaining why it belongs there.
8. For pages without original paper figures, decide whether the visual should be:
   - a generated technical diagram,
   - a real screenshot captured by the user,
   - a table / equation / existing source figure,
   - or no separate figure because text is the dominant content.
9. Generate a preliminary image-prompt map before TeX drafting. The map should include slide title, visual purpose, recommended aspect ratio, screenshot-vs-generated choice, image/text ratio, and a prompt if generation is appropriate.
10. If the prompt map is substantial or the user asks for illustration prompts, hand off to `illustration-prompt-exporter` and save a standalone prompt file.
11. Identify unfamiliar terms early and mark where a concept-bridge slide or plain-language annotation is needed.
12. Record the slide-level risks: formula density, unreadable figures, page overflow, missing evidence, or weak generated visuals.
13. Draft the TeX skeleton and bibliography only after the outline and visual plan are stable.
14. Hand off to `tex-ppt-structuring` for figure placement and to `tex-builder` for compile troubleshooting.

## Generated Image and Screenshot Planning
- You may suggest using nanobanana or another image-generation AI to create supporting diagrams, but the output should be prompt-ready rather than tool-specific.
- Prefer generated images for mechanism diagrams, process flows, architecture summaries, comparison charts, and risk propagation diagrams.
- Prefer real screenshots for product UIs, GitHub repositories, terminal outputs, actual Obsidian vaults, generated wiki pages, dashboards, and demo evidence.
- Generated prompt text must include a unified style instruction and a slide-specific technical content instruction.
- Default generated diagram ratio is `3:4` for side-column visuals in Beamer templates.
- Use `16:9` only for dense overview diagrams, multi-lane workflows, three-column comparisons, or full-slide visual explanations.
- Assign an image/text budget per page:
  - visual-led page: 60-75% visual, 25-40% text;
  - balanced page: 45-55% visual, 45-55% text;
  - text-led page: 25-40% visual, 60-75% text;
  - screenshot evidence page: screenshot large enough to read the relevant region, with only 1-3 explanation bullets.
- If generated-image tools are likely to render text poorly, ask for minimal labels or placeholder labels and add final labels in TeX.

## Output Expectations
- A requirement-refinement summary
- A page-by-page outline
- A figure-to-page map
- A generated-image / screenshot prompt map
- A short risk list
- A draft-ready TeX plan, not a final speech script
