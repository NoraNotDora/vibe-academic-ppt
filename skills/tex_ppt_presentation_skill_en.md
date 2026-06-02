# TeX Academic PPT Structuring Notes (English Reference)

> Supplementary reference for `skills/tex-ppt-structuring/SKILL.md`. This file is useful as a longer-form guide, but the canonical triggerable skill lives in the `SKILL.md` file.

## 1. Scope
- Build or refine TeX-based academic slides (for example, `slides.tex`) with stable layout and clear narrative.
- Handle common issues such as misaligned figures, duplicated caption numbering, unclear figure meaning, crowded slide text, and layout imbalance.
- Generate speech-ready scripts with strong logic, not rehearsal scripts.

## 2. Folder and Naming Conventions
- Figure folder: `fig/<topic>/`
- Figure naming: `fig/<topic>/<fig-id>-<short-name>.pdf`
- Prefer vector assets (PDF, or SVG converted to PDF); use PNG only when needed.
- Keep legend files near their main figures, for example `*-legend.pdf`.

## 3. Figure Integration Workflow (Execution Order)
1. Build a mapping table: `source figure id -> slide page -> speaking purpose -> concepts to explain`
2. Choose layout first: single figure / side-by-side / figure + short takeaway / concept-bridge page
3. Assign a size budget before editing: dominant block, secondary block, figure aspect ratio, binding constraint (width-limited or height-limited), and approximate width share
4. Ensure alignment first, then tune size
5. Write caption and speaking sentence
6. Compile and check overflow, overlap, sizing, and numbering
7. Normalize caption style across the deck

## 4. Presentation Structuring Principles (Macro First)
- Use the default storyline: Motivation -> Method -> Evaluation -> Conclusion.
- Group strongly related pages before writing page-level scripts.
- Typical grouped blocks:
  - Motivation + problem definition
  - Concept bridge + notation
  - System overview + module details
  - Variable definition + objective + constraints
  - Experiment setup + main results + ablation/robustness
- Before outlining, extract key concepts, jargon, abbreviations, and the paper's uncommon core terms.
- For each uncommon core concept, write one plain-language explanation and decide whether it needs a dedicated slide.
- Output macro outline first, then generate page-level speech script.
- Read each page once as an audience member would.
- If the page depends on oral explanation to make sense, simplify the text or add a clearer visual anchor.

### 4.1 Concept Bridge for Non-Specialist Audiences
- Identify which concepts are new to a non-specialist audience.
- If a core term is unusual, add a short definition or bridge sentence before using it heavily.
- Prefer one bridge sentence or a small annotation over a dense paragraph.
- If the concept is central to the paper and likely unfamiliar, make it visible in the outline instead of hiding it in a long paragraph.

## 5. Chapter Coverage Check (Section-by-Section)
- Build a coverage table: `section title -> mapped slide pages -> covered? -> evidence(page/figure) -> concept explained?`
- For each section, check at least:
  - Core question is explained
  - Key method/formula is present
  - Key experimental finding is cited
  - Transition to neighboring sections is clear
  - Uncommon core concepts are explained for a non-specialist audience
- If something is missing, add evidence-first content before adding detail pages.

## 6. Figure Usage Strategy (Maximize Source Figure Coverage)
- Goal: include as many source figures as reasonably possible without crowding.
- Build a figure map: `figure id -> meaning -> related section -> recommended placement`.
- Arrangement rules:
  - Organize by figure-content relationship, not rigid source order
  - Keep figures for one argument adjacent when possible
  - Keep legends on the same or neighboring page as the main figure
- Keep grouped figures together so the audience can compare them without switching pages.
- Match layout to figure shape when it improves readability: wide figures can use top-bottom placement, and tall figures can use left-right placement.
- Do not maximize a side-by-side figure column blindly. With `keepaspectratio`, portrait figures are often height-limited; widening their column creates unused horizontal whitespace and compresses the text.
- For 3:4 or portrait figures, prefer about `0.42-0.45\textwidth` for the figure column and `0.52-0.55\textwidth` for the text column.
- For 16:9 or wide figures, prefer about `0.64-0.70\textwidth` for the figure column and `0.28-0.34\textwidth` for the text column, or switch to top-bottom/full-width if text becomes fragmented.
- If paragraph endings are very short or bullets wrap after one or two words, widen the text column before shrinking font size. Avoid `\tiny` for normal explanatory text.
- Every key figure must have one explicit takeaway sentence and a size target.

### 6.1 Text Width, Gaps, and White Space
- Adjust text box width before reducing font size. If the final line of a paragraph or bullet is less than about half of the longest line, widen the text column or change to a top-bottom layout.
- One- or two-word wrapped lines are a layout warning. Fix the column width, shorten the sentence, or split the slide.
- On image-led slides, avoid heavy `block` wrappers when their title bars consume the space needed by the image. Use bold inline labels or unframed notes instead.
- Limit normal slides to two major text blocks. More than two blocks plus a large image usually requires a split slide.
- Use `\small` or `\scriptsize` for normal explanatory text. Reserve `\tiny` for citations, metadata, or intentionally secondary labels.
- Negative `\vspace` should be small and deliberate, usually between `-0.3em` and `-0.8em`. If a slide needs multiple large negative gaps, redesign the layout.
- For wide images, constrain both width and height with `keepaspectratio`, such as `width=\linewidth,height=0.55\textheight,keepaspectratio`.
- If large blank areas appear because an image is height-limited or the text column is too narrow, rebalance columns instead of accepting the whitespace.
- Export PDF screenshots after significant layout changes and inspect geometry. If CJK fonts are missing in the screenshot tool, use screenshots for spatial balance and verify text in the PDF viewer.

## 7. Reusable TeX Templates

### 7.1 Single-Figure Slide
```tex
\begin{frame}{Topic Overview}
  \begin{figure}
    \centering
    \includegraphics[width=0.82\linewidth]{fig/topic/fig-main.pdf}
    \caption{Comparison under different settings}
  \end{figure}
\end{frame}
```

### 7.2 Side-by-Side Figures
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

### 7.3 Portrait Figure With Text
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

### 7.4 Wide Figure That Looks Off-Center
```tex
\begin{frame}{Process Overview}
  \centering
  \makebox[\linewidth][c]{\includegraphics[width=0.82\linewidth,height=0.48\textheight,keepaspectratio]{fig/topic/fig-wide.pdf}}\par
  \vspace{0.05cm}
  {\scriptsize Wide figure showing the key trend}
\end{frame}
```

## 8. Caption and Figure-Speaking Rules

### 8.1 Caption Numbering Rule
- If your template auto-generates "Figure X", do not manually write "Figure X:" in `\caption{...}`.
- Recommended: `\caption{Timeline gain in key stages}`
- Not recommended: `\caption{Figure 3: Timeline gain in key stages}`

### 8.2 Caption Information Structure
- Pattern: object + metric/dimension + usage
- Example: `Latency breakdown and sample proportion under different input scales (used for evaluation workload construction)`
- If a figure introduces a new concept, include the concept name in the caption or speaking sentence.

### 8.3 Figure-speaking Sentence Pattern
- State conclusion first, then mechanism:
  - `Conclusion: this figure shows XX. Mechanism: YY leads to ZZ.`

## 9. Frequent Issues and Fixes
- Not centered: use `\centering`; if still visually off, wrap with `\makebox[\linewidth][c]{...}`.
- Distorted ratio: set only `width` or only `height`; if both are set, add `keepaspectratio`.
- Duplicated numbering: remove manual "Figure X" from caption.
- Unclear meaning: add variables and usage context in caption or the first speaking sentence.
- Overlap or crowding: reduce image width, add `\vspace`, shorten caption text, or split the slide.
- Wasted horizontal space beside a portrait figure: reduce the figure column and widen the text column; the figure is probably height-limited and will not shrink if its height cap remains unchanged.
- Slow compile or memory pressure: compress oversized PNG files, prefer PDF.
- Output PDF locked: compile to a temporary jobname first (for example `-jobname=slides_tmp`).

### 9.1 Quick Layout Audit
- Use `tools/ppt_layout_audit.py --tex pre.tex --log pre.log` after the first compile.
- Treat `Overfull \hbox` and `Overfull \vbox` as layout bugs, not cosmetic warnings.
- If a slide has too many bullets, too many major blocks, or unbalanced figure widths, split or rebalance it.
- Export representative screenshots after compiling. Check at least one wide-figure page and one portrait side-by-side page. If the screenshot renderer lacks CJK fonts, use screenshots for spatial balance and verify text in the PDF viewer.

## 10. Source TeX to Slide TeX (Figure Extraction by Appearance Order)
- Inputs:
  - Main file: `source.tex`
  - Section files: `sections/*.tex`
  - Figure directory: `fig/*.pdf`
- Extraction:
  - Read `\input{sections/...}` order from `source.tex`
  - Extract `\includegraphics{fig/...}` line-by-line in each section file
  - Deduplicate to get the figure appearance list
- Landing:
  - Copy source figures into `fig/topic`
  - Place figures in `slides.tex` by speaking logic, not rigid source order
  - Add one takeaway sentence per slide

## 11. Duration and Personalization Handling
- If talk duration is unknown, always ask first: `How many minutes is the presentation?`
- Then adapt planning:
  - Short: keep storyline and key figures only
  - Medium: storyline + key methods + main experiments
  - Long: full coverage + extended discussion + Q&A prep
- Store custom requirements in: `presentation_personalization_requirements.md`
- Append new special requirements before regenerating outline and script.

## 12. Output Requirements
- Do not produce rehearsal scripts.
- Produce a directly deliverable speech script.
- Always provide macro structure first, then page-level script.
- Prefer natural, concise wording over stiff or overly segmented phrasing.

## 13. Final Delivery Checklist
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
