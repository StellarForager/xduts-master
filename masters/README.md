# Xidian University master's thesis template

This XeLaTeX template is based on XDUTS 6.2.9.0 and follows Xidian University's January 2025 graduate thesis templates. See the university's [academic degree](https://gr.xidian.edu.cn/info/1047/5087.htm) and [professional degree](https://gr.xidian.edu.cn/info/1047/5086.htm) instructions.

## Writing

1. Replace the sample title, degree, author, supervisor, discipline, and submission details in [setup.tex](setup.tex). Complete both language versions of the title, abstract, and keywords.
2. Put the abstracts, symbols, and abbreviations in [front/](front/). Separate abstract paragraphs with blank lines. Use three to five corresponding keywords in each language and sort the abbreviations alphabetically.
3. Add chapters in [chapters/](chapters/) and include them in [main.tex](main.tex). The table of contents lists chapters, sections, and subsections. Use `\subsubsection` for a fourth heading level in the text.
4. Add your sources to [references.bib](references.bib) and complete the appendices, acknowledgements, and biography in [back/](back/). Start each appendix with `\chapter`. Remove the `info/appendix` setting if there are no appendices. The `info/statement-scan` setting accepts a signed A4 declaration as a PDF.

## Building

Use TeX Live 2026 or a current MacTeX installation with XeLaTeX and Biber. Run these commands from this directory.

```sh
latexmk -outdir=build main.tex          # Academic degree
latexmk -outdir=build professional.tex  # Professional degree
latexmk -outdir=build review.tex        # Anonymous review
```

For anonymous review of a professional degree thesis, change `\input{main}` to `\input{professional}` in [review.tex](review.tex). Use `\anon[]{...}` for identifying text in the thesis body or publication list. Replace identifying figures with anonymous copies and submit the resulting PDF.

For submission, use SimSun, SimHei, and Times New Roman. The template looks in [fonts/](../fonts/README.md) before checking system fonts. Enable `\XDURequireSchoolFonts` to stop the build when required fonts are missing, or enable `\XDUPreviewFonts` to use preview fonts. The template uses XITS Math and prefers a local `XITSMath-Regular.otf` when present. To use a different font directory, set `\XDUFontDirectory` in [main.tex](main.tex) and include a trailing slash.

## Figures, tables, and references

Put figure captions below the figure and table captions above the table. For a reproduced or adapted figure, cite the source at the end of the long caption and use the optional caption argument for the list of figures. For multipage tables, repeat headings with `longtable`. For long equations with a single number, put an `aligned[b]` environment inside `equation`.

Use `\cite{key}` for superscript citations. Biber builds the bibliography. Include the URL and access date for online sources. Consult the university's Word template for reference requirements.

## Source

The modified class is released under the [LPPL 1.3c](LICENSE). To regenerate it, run `xetex xduts.ins` with the root source files in a temporary directory, then run `patch -o xdu-master.cls xdupgthesis.cls < /path/to/xduts-master.patch`.

The source uses XeTeX Unicode escapes for the Chinese strings required by the university's template. Enter your own Chinese thesis text directly as UTF-8.
