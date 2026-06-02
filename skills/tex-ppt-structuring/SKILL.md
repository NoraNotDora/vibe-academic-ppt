---
name: "tex-ppt-structuring"
description: "Structure TeX academic slides, map paper figures to pages, and generate a directly deliverable speech script. Use when arranging figures, balancing slide density, revising a page from the audience's point of view, or turning a drafted outline into Beamer slides."
---

# TeX Academic PPT Structuring and Speech Script Skill

Use this skill after planning. It turns a paper outline into TeX slides that read clearly and compile cleanly.

## Scope
- Build or refine TeX-based academic slides
- Integrate figures, tables, and the minimum necessary math
- Integrate generated technical diagrams and real screenshots when source figures are insufficient
- Generate a speech-ready script
- Fix layout imbalance, duplicate captions, and unreadable pages

## When to Trigger
- The outline is ready and TeX drafting should start.
- Figures need to be positioned by narrative logic.
- A slide feels too dense, too empty, or visually unbalanced.
- A direct speech script is needed from the approved slide order.

## Macro Workflow
1. Extract the section structure, key claims, and figure IDs from the paper or outline.
2. Build a coverage table: `section title -> mapped slide pages -> covered? -> evidence(page/figure) -> concept explained?`.
3. Build a figure map: `figure id -> meaning -> related section -> recommended placement -> takeaway sentence`.
4. Build or refine an image-generation / screenshot map for pages that need non-paper visuals.
   - Record: slide title, visual purpose, generated diagram or real screenshot, recommended aspect ratio, image/text ratio, and prompt.
   - Use nanobanana or any other image-generation AI only as an optional production route; keep prompts portable across tools.
5. Decide the layout before editing text.
   - Read each page from the audience's point of view and ask whether the main message is clear on first pass.
   - Prefer one visual anchor per page.
   - Keep 3-6 bullet points per page.
   - Avoid more than 2 major figures on a page.
   - Add a concept bridge slide or annotation when a term is likely unfamiliar.
6. Assign a size budget before placing figures.
   - Record the dominant visual, supporting text budget, figure aspect ratio, binding constraint (width-limited or height-limited), and approximate width share.
7. Write one plain-language explanation for each key formula or definition.
8. Place figures in narrative order: background -> method -> evaluation -> conclusion.
9. Compile, inspect the log, and simplify any page with overflow, unreadable figures, or dense text.
10. Generate the final speech script from the approved page outline.

## Concept Bridge
- If a core term is central but unfamiliar, explain it before heavy use.
- Prefer one short definition or bridge sentence over a long paragraph.
- If the concept is important to the argument, make it visible in the outline instead of hiding it in a dense page.

## Figure Rules
- Use source figures whenever they support the argument directly.
- If the original figure is unavailable, draw an equivalent diagram instead of forcing a weak substitution.
- Use generated diagrams for abstract mechanisms, pipelines, architecture, comparison, taxonomy, cost flows, and risk propagation.
- Use real screenshots for product UI, repository pages, terminal output, actual tool demos, generated wiki pages, and evidence that needs authenticity.
- When creating generated-diagram prompts, include a unified style instruction:
  `clean academic vector technical diagram, light background, thin lines, rounded rectangles, blue/teal/gray palette with subtle warm accents, minimal readable labels or placeholder labels, no decorative scene, no watermark, no logo`.
- Prefer `3:4` generated diagrams for side-column visuals in Beamer templates.
- Use `16:9` for full-slide overview diagrams, dense comparison charts, swimlane workflows, or diagrams that need horizontal reading.
- If the image generator may produce bad text, request placeholder labels and add accurate labels later in TeX.
- Put a short takeaway sentence immediately after each key figure.
- Keep captions short and avoid manually repeating figure numbers if the template already numbers them.
- Keep grouped figures together on the same page when they support one argument.
- Place figures in the section where the related claim is introduced, not where they merely fit visually.
- Match layout to aspect ratio and grouping:
  - Use top-bottom layout for wide figures when that keeps the slide readable.
  - Use left-right layout for tall figures when that keeps the slide readable.
  - In side-by-side layouts, do not maximize the figure column blindly. With `keepaspectratio`, tall figures are usually height-limited; extra column width becomes dead whitespace while the text column gets cramped.
  - For 3:4 or portrait diagrams, prefer about `0.42-0.45\textwidth` for the figure column and `0.52-0.55\textwidth` for the text column. This keeps the figure near max height and gives text natural line length.
  - For 16:9 or wide diagrams, use about `0.64-0.70\textwidth` for the figure column and `0.28-0.34\textwidth` for the text column, or switch to top-bottom/full-width if the text becomes fragmented.
  - Keep paired or comparative figures adjacent so the audience can compare them without hunting across pages.

## Image/Text Ratio Rules
- Visual-led page: use roughly 60-75% visual area and 25-40% text.
- Balanced page: use roughly 45-55% visual area and 45-55% text.
- Text-led page: use roughly 25-40% visual area and 60-75% text.
- Screenshot evidence page: crop to the relevant UI region, keep it readable, and pair it with only 1-3 explanatory bullets.
- If a page has a 3:4 diagram, prefer a side-by-side layout: text on one side, diagram on the other.
- If a page has a 16:9 diagram, prefer top-bottom layout or full-slide visual with a short takeaway.
- For side-by-side pages, choose column widths by the rendered image size, not by the desired visual importance alone:
  - If a portrait image is already height-limited, widening its column will not enlarge it; give the unused horizontal space back to the text.
  - If paragraph endings are very short or bullets wrap after one or two words, widen the text column before shrinking fonts.
  - Avoid `\tiny` for normal explanatory text. Use `\scriptsize` only when needed; prefer wider text columns, fewer bullets, or a split slide.
  - A natural text column usually beats a "maximum" figure column that leaves large blank bands.

## Text Layout and Spacing Strategy
- Optimize text box width before shrinking fonts. If the last line of a paragraph or bullet is less than about half of the longest line, widen the text column or switch layout.
- Treat one- or two-word wrapped lines as a layout smell. Fix them by widening the column, shortening the sentence, or splitting the page.
- Do not let block titles consume vertical space on image-led slides. If the slide already has a clear title, replace heavy `block` wrappers with bold inline labels or short unframed notes.
- Use no more than two major text blocks on a normal slide. Three blocks plus a large image is usually a split candidate.
- Keep normal explanatory text at `\small` or `\scriptsize`; use `\tiny` only for metadata, citations, or intentionally secondary labels.
- Prefer fewer, wider bullets over many narrow bullets. A readable line length matters more than symmetric columns.
- Control vertical gaps deliberately:
  - use small negative `\vspace` only to tighten known safe gaps after an image, usually `-0.3em` to `-0.8em`;
  - avoid stacking several negative gaps on one slide;
  - if spacing needs more than a small adjustment, change the layout or split the slide.
- For wide images, set both width and height caps with `keepaspectratio`, for example `width=\linewidth,height=0.55\textheight,keepaspectratio`. This maximizes useful area without pushing text off the slide.
- For pages with a top wide visual and bottom notes, remove captions or move citations to the references slide when the caption competes with the main message.

## White Space and Screenshot Review
- Large blank areas are acceptable only when they intentionally focus attention. If blank space appears because an image is height-limited or a text box is too narrow, rebalance the columns.
- After changing layout, export screenshots from the PDF and inspect spatial balance, not only the TeX log.
- Check at least:
  - one wide-image page,
  - one portrait-image side-by-side page,
  - one dense text page,
  - the agenda or section-transition page if the section list changed.
- If the screenshot renderer lacks CJK fonts, still use it for layout geometry, but verify text in the PDF viewer.
- Watch for CJK text being squeezed into isolated characters or missing after screenshot export; that usually indicates a renderer/font issue, while wrapped one-word lines in the PDF indicate a real layout issue.

## Layout Audit
After the first successful compile, run:

```powershell
python ..\tools\ppt_layout_audit.py --tex pre.tex --log pre.log
```

Treat warnings as a cue to simplify, resize, or split the page before finalizing.

Also export representative page screenshots after compiling and inspect them visually. Check at least one wide-figure page and one portrait-figure side-by-side page. If screenshot rendering lacks CJK fonts, still use it for spatial balance, but verify the PDF itself for actual text.

## Useful TeX Patterns

### Single-Figure Slide
```tex
\begin{frame}{Topic Overview}
  \begin{figure}
    \centering
    \includegraphics[width=0.82\linewidth]{fig/topic/fig-main.pdf}
    \caption{Comparison under different settings}
  \end{figure}
\end{frame}
```

### Side-by-Side Figures
```tex
\begin{frame}{Comparative View}
  \begin{columns}[T]
    \column{0.49\textwidth}
      \centering
      \includegraphics[width=\linewidth]{fig/topic/fig-a.pdf}
      \vspace{2mm}
      {\scriptsize (a) Condition A}
    \column{0.49\textwidth}
      \centering
      \includegraphics[width=\linewidth]{fig/topic/fig-b.pdf}
      \vspace{2mm}
      {\scriptsize (b) Condition B}
  \end{columns}
\end{frame}
```

### Portrait Figure With Text
Use this for 3:4 diagrams or tall screenshots. The figure stays near max height while the text column keeps natural line length.

```tex
\begin{frame}{Architecture}
  \begin{columns}[T,onlytextwidth]
    \column{0.43\textwidth}
      \centering
      \includegraphics[width=\linewidth,height=0.82\textheight,keepaspectratio]{fig/topic/portrait-diagram.pdf}

    \column{0.54\textwidth}
      \scriptsize
      \begin{block}{Key takeaways}
        \begin{itemize}
          \item The raw source layer remains read-only.
          \item The wiki layer accumulates summaries, entities, concepts, and cross-links.
          \item The schema layer keeps update rules explicit.
        \end{itemize}
      \end{block}
  \end{columns}
\end{frame}
```

### Wide Figure That Looks Off-Center
```tex
\begin{frame}{Process Overview}
  \centering
  \makebox[\linewidth][c]{\includegraphics[width=0.82\linewidth,height=0.48\textheight,keepaspectratio]{fig/topic/fig-wide.pdf}}\par
  \vspace{0.05cm}
  {\scriptsize Wide figure showing the key trend}
\end{frame}
```

## Duration and Personalization Handling
- If talk duration is unknown, ask before you finalize page count.
- Short talk: keep storyline and key figures only.
- Medium talk: storyline + key methods + main experiments.
- Long talk: full coverage + extended discussion + Q&A prep.
- Use `presentation-personalizer` when requirements change midstream.
- If the wording feels too dense for a live talk, simplify it before adjusting the layout again.

## Output Requirements
- Do not produce rehearsal scripts.
- Produce a directly deliverable speech script.
- Always provide macro structure first, then page-level script.
- Keep each page to 3-6 points, one sentence per point.

## Final Delivery Checklist
- All figures compile and paths are valid
- All figures are visually centered and not stretched
- Caption style is consistent and has no duplicated numbering
- Every key figure has one takeaway sentence
- Side-by-side pages have balanced spacing and font size
- Uncommon core concepts are explained once in plain language
- Storyline follows Motivation -> Method -> Evaluation -> Conclusion
- Section-by-section coverage check is completed
- Duration has been confirmed and script length matches it
- Layout audit shows no critical overflow or imbalance warnings
