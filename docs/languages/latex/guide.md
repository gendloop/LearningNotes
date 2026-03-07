# Guide

## 安装

1. `scoop install main/miktex`
2. VSCode安装插件`LaTex Workshop`
3. 创建一个项目目录作为根目录, 添加文件`.vscode/settings.json`

    ```json
    {
      "latex-workshop.latex.recipes": [
        {
          "name": "latexmk",
          "tools": [
            "latexmk"
          ]
        },
        {
          "name": "pdflatex -> bibtex -> pdflatex * 2",
          "tools": [
            "pdflatex",
            "bibtex",
            "pdflatex",
            "pdflatex"
          ]
        }
      ],
      "latex-workshop.latex.outDir": "%DIR%/build",
      "latex-workshop.view.pdf.zoom": "auto",
      "latex-workshop.view.pdf.viewer": "tab",
    }
    ```

4. 编写`.tex`文件

## 项目结构

```latex
root/
│
├── main.tex          % 主文件，包含导言区和各个部分的引入
├── preamble.tex      % 导言区，定义宏包、命令等
│
├── chapters/         % 存放各章节的文件夹
│   ├── chpt1.tex       % 第一章
│   ├── chpt2.tex       % 第二章
│   └── chpt3.tex       % 第三章
│
├── sections/         % 存放各节的文件夹
│   ├── sec1.1.tex      % 第一章每一节
│   ├── sec2.1.tex      % 第二章第一节
│   └── sec3.1.tex      % 第三章第一节
│
├── figures/          % 存放图表的文件夹
│   ├── fig1.pdf
│   └── fig2.png
│
└── bib/              % 存放参考文献的文件夹
    └── references.bib
```

## 编写 LaTex

### 编写内容样例

> 源码及结果见 [https://github.com/gendloop/LaTeX/tree/main/src/3.1](https://github.com/gendloop/LaTeX/tree/main/src/3.1)

#### 入门样例

```latex
\documentclass{article}
\begin{document}
Hello gendloop, this is your first document.
This is a simple example, with no extra parameters or packages included.
\end{document}
```

* `\documentclass{article}` 声明文档类型(更多类型可参考[CTAN Comprehensive TEX Archive Network](https://www.ctan.org/topic/class))

* `\begin{document}` `\end{document}` 文档内容

#### 文件序言

```latex
\documentclass[12pt, letterpaper]{article}
\usepackage{graphicx} % loading a external package (here, graphicx) to extend capabilities
```

* `12pt` 字体大小. default size is 10pt. other possible values are 9pt, 11pt, 12pt
* `letterpaper` 纸张大小.  other possible values are `a4paper` `legalpaper`

> 更多页面设置可参考 [https://cn.overleaf.com/learn/latex/Page_size_and_margins](https://cn.overleaf.com/learn/latex/Page_size_and_margins)

#### 标题, 作者和日期

```latex
\documentclass[12pt, a4paper]{article}

\usepackage{graphicx}

\title{My first document}
\author{gendloop\thanks{gg}}
\date{July 2024}

\begin{document}
\maketitle
You have now added a title, author and date to your first \LaTeX{} document
Hello gendloop, this is your first document.
This is a simple example, with no extra parameters or packages included.
\end{document}
```

#### 注释

`%`

#### 加粗, 倾斜, 强调

```latex
Bold: \textbf{Bold}
Italics: \textit{Italics}
Underline: \underline{Underline}
```

#### 图片

##### 所需包

```latex
\usepackage{graphicx}
\graphicspath{{figures/}}

\usepackage{subcaption}
```

##### 一个图片

```latex
% example 1
\includegraphics{example.png}
```

##### 加标题, 大小, 引用名等

```latex
% example 2
\begin{figure}[h]
    \centering
    \includegraphics[width=0.75\textwidth]{example.png}
    \caption{A nice picture}
    \label{fig:mesh1}
\end{figure}
```

##### 使用引用

```latex
% example 3
As you can see in figure \ref{fig:mesh1}, the function grows near the origin.
This example is on page \pageref{fig:mesh1}.
```

##### 一个图表中包含多个图片

```latex
% example 4: Multiple images in one figure
\begin{figure}[h]
    \centering
    \begin{subfigure}{0.4\textwidth}
        \includegraphics[width=\linewidth]{favicon.png}
        \caption{Caption1}
        \label{fig:subimg1}
    \end{subfigure}
    \begin{subfigure}{0.4\textwidth}
        \includegraphics[width=\linewidth]{favicon.png}
        \caption{Caption2}
        \label{fig:subimg2}
    \end{subfigure}

    \caption{Caption for this figure with two images}
    \label{fig:img2}
\end{figure}
```

##### 放大, 缩小, 旋转

```latex
% example 5: Chanaging the image size and rotating the picture
\includegraphics[scale=0.1]{favicon.png}
\includegraphics[scale=0.2]{favicon.png}
\includegraphics[scale=0.3]{favicon.png}
\includegraphics[width=4cm, height=2cm]{favicon.png}
\includegraphics[scale=0.2, angle=45]{favicon.png}
```

##### 文本旁嵌入图片

```latex
% example 6: Wrapping text around figures
Praesent in sapien. Lorem ipsum dolor sit amet, consectetuer
adipiscing elit. Duis fringilla tristique neque. Sed interdum
libero ut metus. Pellentesque placerat.

\begin{wrapfigure}{l}{0.25\textwidth} % r,l,i,o
    \centering
    \includegraphics[width=\linewidth]{wrap_figure.png}
\end{wrapfigure}

Praesent in sapien. Lorem ipsum dolor sit amet, consectetuer
adipiscing elit. Duis fringilla tristique neque. Sed interdum
libero ut metus. Pellentesque placerat.
```

#### 列表

##### 无序列表

```latex
% Unordered lists
\begin{itemize}
    \item apple
    \item banana
\end{itemize}
```

##### 有序列表

```latex
% ordered lists
\begin{enumerate}
    \item apple
    \item banana
\end{enumerate}
```

##### 列表嵌套

```latex
% mixed
\begin{enumerate}
    \item first
    \begin{itemize}
        \item apple
        \item pear
    \end{itemize}
    \item second
    \begin{enumerate}
        \item apple
        \item pear
    \end{enumerate}
\end{enumerate}
```

#### 公式

##### 行内公式

`$E=mc^2$`

```latex
% Inline math mode
In physics, the mass-energy equivalence is stated
by the wquation $E=mc^2$, discovered in 1905 by Albert Einstein.

\(E=mc^2\)

$E=mc^2$

\begin{math}
    E=mc^2
\end{math}
```

##### 展示公式

`\begin{equation}`

`\begin{equation*}`

```latex
\usepackage{amsmath}

% Display math mode
In physics, the mass-energy equivalence is stated
by the wquation \[E=mc^2\], discovered in 1905 by Albert Einstein.

\begin{equation}
    E=m^2 % 带序号
\end{equation}

\begin{equation*}
    E=m^2 % 带序号
\end{equation*}
```

##### 公式样例

`\[ \int_0^1 \frac{dx}{e^x} = \frac{e-1}{e} \]`

```latex
% Complete example
Subscripts in math mode are written as $a_b$ and superscripts are written as $a^b$. These can be combined and nested to write expressions such as

\[ T^{i_1 i_2 \dots i_p}_{j_1 j_2 \dots j_q} = T(x^{i_1},\dots,x^{i_p},e_{j_1},\dots,e_{j_q}) \]

We write integrals using $\int$ and fractions using $\frac{a}{b}$. Limits are placed on integrals using superscripts and subscripts:

\[ \int_0^1 \frac{dx}{e^x} =  \frac{e-1}{e} \]

Lower case Greek letters are written as $\omega$ $\delta$ etc. while upper case Greek letters are written as $\Omega$ $\Delta$.

Mathematical operators are prefixed with a backslash as $\sin(\beta)$, $\cos(\alpha)$, $\log(x)$ etc.
```

### 编写结构示例

> 源码及结果见 [https://github.com/gendloop/LaTeX/tree/main/src/3.2](https://github.com/gendloop/LaTeX/tree/main/src/3.2)

#### 摘要

```latex
\documentclass{article}
\begin{document}
\begin{abstract}
This is a simple paragraph at the beginning of the
document. A brief introduction about the main subject.
\end{abstract}
\end{document}
```

#### 段落和新行

* Paragraph: 空一行
* New line: `\\`

```latex
Paragraph1: After our abstract we can begin the first paragraph,
then press ``enter'' twice to start the second one.

Paragraph2: This line will start a second paragraph.

Paragraph3: I will start the third paragraph and then add \\
a manual line break which causes this text to start
on a new line but remains part of the same paragraph.
Alternatively, I can use the \verb|\newline|\newline command
to start a new line, which is also part of the same paragraph.
```

#### 章, 节

```latex
\documentclass{book}
\begin{document}

\chapter{First Chapter}

\section{Introduction}

Something.

\section{Second}

Something.

\subsection{Firt Subsection}

Something.

\section*{Unnumbered Section}

Something.

\chapter{Second Chapter}

\end{document}
```

* sectioning commands
  * `\part`
  * `\chapter`
  * `\section`
  * `\subsection`
  * `\subsubsection`
  * `\paragraph`
  * `\subparagraph`

> \part and \chapter commands are only available in the _report_ and _book_ document classes

#### 表格

> [表格生成工具](https://www.tablesgenerator.com/)

##### 基础表格

```latex
% Creating a basic table
\begin{center}
    \begin{tabular}{c c c} % 3 列, 居中
        cell1 & cell2 & cell3 \\
        cell4 & cell5 & cell6 \\
        cell7 & cell8 & cell9
    \end{tabular}
\end{center}
```

##### 加边框

* 横线  `\hline`
* 纵线  `|`

```latex
% Adding borders
\begin{tabular}{l|c|r}
    \hline
    cell1 & cell2fdsfds & cell3 \\
    \hline
    cell4 & cell5 & celfdsafdl6 \\
    celfdafdl7 & cell8 & cell9  \\
    \hline
\end{tabular}
```

##### 加标题, 引用

```latex
% Captions, labels and references
Table \ref{tab:data} shows how to add a table caption and reference a table
\begin{table}[h]
    \centering
    \begin{tabular}{c c c c}
        \hline
        COl1 & Col2 & Col3 & Col4  \\ [0.5ex]
        \hline\hline
        1    & 6    & 8979 & 89898 \\
        1    & 6    & 8979 & 89898 \\
        1    & 6    & 8979 & 89898 \\
        1    & 6    & 8979 & 89898 \\ [1ex]
        \hline
    \end{tabular}
    \caption{Table caption}
    \label{tab:data}
\end{table}
```

#### 目录

`\tableofcontents`

```latex
\documentclass[12pt, a4paper]{article}

\title{Table of contents}
\author{gendloop\thanks{gg}}
\date{July 2024}

\begin{document}

\maketitle

\tableofcontents

\section{First section}
Something
\subsection{First subsection}
Something

\section*{Second section}
Something

\section{Third section}
Something

\end{document}
```

### 查找和使用包

> 源码及结果见[https://github.com/gendloop/LaTeX/tree/main/src/3.3](https://github.com/gendloop/LaTeX/tree/main/src/3.3)

#### 加载包

`\usepackage[options]{somepackage}`

* _graphicx_ package extends LaTeX by providing commands to import graphics files and was loaded (in the preamble)
* _geometry_ package provides many options to configure page layout in LaTeX

#### 搜索包

* CTAN
  * by topic: [https://www.ctan.org/topics/cloud](https://www.ctan.org/topics/cloud)
  * alphabetically: [https://www.ctan.org/pkg](https://www.ctan.org/pkg)

## References

1. [https://github.com/James-Yu/LaTeX-Workshop/wiki/Install](https://github.com/James-Yu/LaTeX-Workshop/wiki/Install)
2. [https://cn.overleaf.com/learn/latex/Learn_LaTeX_in_30_minutes](https://cn.overleaf.com/learn/latex/Learn_LaTeX_in_30_minutes)
