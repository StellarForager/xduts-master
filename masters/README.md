# 西安电子科技大学硕士学位论文模板

本模板基于 XDUTS 6.2.9.0，参考研究生院 2025 年 1 月修订的 Word 模板。学术学位与专业学位分别使用对应封面和题名页。 [学术学位资料](https://gr.xidian.edu.cn/info/1047/5087.htm) · [专业学位资料](https://gr.xidian.edu.cn/info/1047/5086.htm)

## 开始写作

1. 在 [setup.tex](setup.tex) 填写中英文题目、学位类别、学科或领域、作者、导师、分类号和提交年月。
2. 在 [front/](front/) 填写中英文摘要、关键词、符号表和缩略语表。摘要用空行分段，中英文关键词宜对应填写 3–5 个，缩略语按字母顺序排列。
3. 把章节放在 [chapters/](chapters/) 并在 [main.tex](main.tex) 中用 `\input` 按顺序引入。目录列出章、节和小节。正文第四级标题用 `\subsubsection`。
4. 在 [references.bib](references.bib) 添加参考文献，在 [back/](back/) 填写附录、致谢和作者简介。每个附录用 `\chapter` 开始。无需附录时移除 `info/appendix`。归档版可通过 `info/statement-scan` 导入已签署的 A4 声明 PDF。

## 编译

推荐使用 TeX Live 2026 或当年的 MacTeX。在本目录运行下列命令，`latexmk` 会自动执行 XeLaTeX 和 Biber。

```sh
latexmk -outdir=build main.tex          # 学术学位
latexmk -outdir=build professional.tex  # 专业学位
latexmk -outdir=build review.tex         # 匿名评审
```

专业学位匿名评审可把 [review.tex](review.tex) 中的 `\input{main}` 改为 `\input{professional}`。正文和成果列表中的身份信息可用 `\anon[]{原文}` 隐去，涉及身份的插图需另换匿名版。

正式出稿使用宋体 SimSun、黑体 SimHei 和 Times New Roman。模板优先从 [fonts/](../fonts/README.md) 读取，再查找系统字体。启用 `\XDURequireSchoolFonts` 时，缺少所需字体会终止编译。预览时可启用 `\XDUPreviewFonts`。数学字体使用 XITS Math，优先读取本地 `XITSMath-Regular.otf`。如需更换字体目录，在 [main.tex](main.tex) 修改 `\XDUFontDirectory`，保留路径末尾的斜杠。

## 图、表、公式和文献

图题放在图下，表题放在表上。转载或改绘的图在长题注末尾标注来源，并用可选题注提供图索引的简短标题。跨页表格可用 `longtable` 重复列标题。多行公式共用一个编号时，可在 `equation` 中使用 `aligned[b]`。

用 `\cite{key}` 插入上标引文。参考文献由 Biber 生成。在线文献应填写网址和访问日期。具体要求见学校 Word 模板。

## 文档类源码

修改版按 [LPPL 1.3c](LICENSE) 发布。如需重建文档类，在临时目录复制仓库根目录的 `xduts.dtx` 和 `xduts.ins`，运行 `xetex xduts.ins`，再执行 `patch -o xdu-master.cls xdupgthesis.cls < /path/to/xduts-master.patch`。
