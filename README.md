项目通过分散各个大块的任务来对整个项目进行编译，最外层为<u>`main.tex`</u>进行主要编译功能

在<u>/config</u>文件夹下有一个<u>`config.tex`</u>的文件用来整合整个写的一个使用包，重定义的一些命令的逻辑布置….

```latex
\def\basicPath{\configPath/basic}

\input{\basicPath/package}
\input{\basicPath/custom}
\input{\basicPath/color}
\input{\basicPath/note}
\input{\basicPath/theorem}
\input{\basicPath/format}

```

/config/basic下存放几个主要的文件，下面是对这个目录下的一些文件进行解析。





```latex
% \basicPath/package.tex

% 在这里定义需要的包
\usepackage{amsmath}
\usepackage{amsthm}
\usepackage{graphicx}
\usepackage{mathrsfs}
\usepackage{pifont}     % 特殊符号支持
\usepackage{amssymb} % 用于 \textdbend 符号
\usepackage{enumitem}
\usepackage{geometry}
\usepackage[colorlinks, linkcolor=black]{hyperref}
\usepackage{stackengine}
\usepackage{yhmath}
\usepackage{extarrows}
\usepackage{tcolorbox} % 引入tcolorbox包
\usepackage{xcolor} % for colors
\usepackage{amssymb} % for \textdbend

\usepackage{fancyhdr}
\usepackage[dvipsnames, svgnames]{xcolor}
\usepackage{listings}
\usepackage{titlesec}

\usepackage[strict]{changepage} 
\usepackage{framed}
%\usepackage{color}
\usepackage{mathrsfs}
\usepackage{cleveref}
\usepackage{multicol}

```





```latex
% \input{\basicPath/custom}

% 在这里定义自己顺手的环境
\def\d{\mathrm{d}}
\def\R{\mathbb{R}}
\newcommand{\bs}[1]{\boldsymbol{#1}}
\newcommand{\ora}[1]{\overrightarrow{#1}}
% 几倍的垂直空白
\newcommand{\myspace}[1]{\par\vspace{#1\baselineskip}}
% 代表两个参数，其中第一个参数的默认值为0,增加高度用的
\newcommand{\xrowht}[2][0]{\addstackgap[.5\dimexpr#2\relax]{\vphantom{#1}}}
% 条件选择
\newenvironment{ca}[1][1]{\linespread{#1} \selectfont \begin{cases}}{\end{cases}}
% 行列式
\newenvironment{vx}[1][1]{\linespread{#1} \selectfont \begin{vmatrix}}{\end{vmatrix}}

\newcommand{\tabincell}[2]{\begin{tabular}{@{}#1@{}}#2\end{tabular}}
% 双斜杠 //
\newcommand{\pll}{\kern 0.56em/\kern -0.8em /\kern 0.56em}
% divF
\newcommand{\dive}[1][F]{\mathrm{div}\;\bs{#1}}
% rotA
\newcommand{\rotn}[1][A]{\mathrm{rot}\;\bs{#1}} 


```





```latex
% \input{\basicPath/color}

% 定义了一些常用的颜色，这些颜色将在后续的环境中使用。
\definecolor{greenshade}{rgb}{0.90,1,0.92}
\definecolor{redshade}{rgb}{1.00,0.88,0.88}
\definecolor{brownshade}{rgb}{0.99,0.95,0.9}
\definecolor{lilacshade}{rgb}{0.95,0.93,0.98}
\definecolor{orangeshade}{rgb}{1.00,0.88,0.82}
\definecolor{lightblueshade}{rgb}{0.8,0.92,1}
\definecolor{purple}{rgb}{0.81,0.85,1}
\definecolor{shadecolor}{RGB}{241, 241, 255}

\definecolor{structurecolor}{RGB}{0, 102, 204}
% 这里定义了 'second' 颜色（你可以根据需要调整颜色值）
\definecolor{second}{rgb}{0.6, 0.2, 0.2}  % 定义 'second' 颜色为红棕色调

% 设置定理环境的整体风格为“定义”风格。这通常意味着定理主体使用正常字体，而非斜体。
\theoremstyle{definition}
```



```latex
% \input{\basicPath/note}

% 自定义彩色圆圈数字命令
\newcommand{\circled}[1]{\textcolor{blue}{\textcircled{\textcolor{black}{\small #1}}}}
%\newcommand{\circled}[1]{\textcircled{\small #1}}

% 重新定义 notes 环境
\newenvironment{notes}{
	\par\noindent\makebox[0pt][r]{%
		\scriptsize\color{red!90}\textdbend\quad}% 图标
	\textbf{\color{red!90}Note:} \normalfont % 红色提示标题，正体字体
}{\par}

% 定义 change 环境，使用圆圈数字标注每一个变化项
%\newenvironment{change}{
%	\begin{enumerate}[label=\small\protect\circled{\arabic*}]}{
%\end{enumerate}}

\newenvironment{change}{
	\begin{enumerate}[label=\hfill\circled{\arabic*}, itemsep=1em]
	}{
	\end{enumerate}
}
% 定义 change2 环境
\newenvironment{change2}{
	\begin{tcolorbox}[colback=white, colframe=gray, boxrule=0.5mm, sharp corners=south]
		\begin{enumerate}[label=\centering\circled{\arabic*}]
		}{
		\end{enumerate}
	\end{tcolorbox}
}
% 定义 tip 环境，用于显示提示信息
\newenvironment{tip}{
	\par\noindent\makebox[-3pt][r]{%
		\scriptsize\color{green!90}\ding{43}\quad}% 绿色图标
	\textbf{\color{green!90}Tip:} \itshape % 绿色的提示标题
}{\par}

% 定义 warning 环境，用于显示警告信息
\newenvironment{warning}{
	\par\noindent\makebox[-3pt][r]{%
		\scriptsize\color{orange!90}\ding{70}\quad}% 橙色图标
	\textbf{\color{orange!90}Warning:} \itshape % 橙色的警告标题
}{\par}

% 定义 important 环境，用于显示重要信息
\newenvironment{important}{
	\par\noindent\makebox[-3pt][r]{%
		\scriptsize\color{red!90}\ding{72}\quad}% 红色图标
	\textbf{\color{red!90}Important:} \itshape % 红色的重点标题
}{\par}

% 定义 examplezero 环境，并提供自动编号
\newcounter{examplezero}[section]
\renewcommand{\theexamplezero}{\thesection.\arabic{examplezero}}

\newenvironment{examplezero}[1][]{
	\refstepcounter{examplezero} % 增加 examplezero 计数器
	\par\noindent\textbf{\color{purple!90}Example \theexamplezero:} \itshape #1 \rmfamily}{\par}
	
% 定义introduction环境
\newenvironment{introduction}[1][Introduction]{
	\begin{tcolorbox}[title={#1}]
		\begin{multicols}{2}
			\begin{itemize}[label=\textcolor{structurecolor}{\upshape\scriptsize$\bullet$}]  % 使用$\bullet$
			}{
			\end{itemize}
		\end{multicols}
	\end{tcolorbox}
}


```

```latex
% \input{\basicPath/theorem}

% 这里给出了不同环境的自用定义形式，创建了一系列自定义的定理环境，每个环境都有自己的编号方式和名称。
\newtheorem{myDefn}{\indent Definition（定义）}[section] % 定义
\newtheorem{myLemma}{\indent Lemma(引理)}[section] % 引理
\newtheorem{myThm}[myLemma]{\indent Theorem（定理）} % 定理
\newtheorem{myCorollary}[myLemma]{\indent Corollary（推论）} % 推论
\newtheorem{myCriterion}[myLemma]{\indent Criterion（标准）} % 标准
\newtheorem*{myRemark}{\indent Remark（备注）} % 备注
\newtheorem{myProposition}{\indent Proposition（命题）}[section] % 命题

% formal 环境用于创建带有彩色边框和背景的框架，包含两个颜色参数
\newenvironment{formal}[2][]{%
	\def\FrameCommand{%
		\hspace{1pt}%
		{\color{#1}\vrule width 2pt}%
		{\color{#2}\vrule width 4pt}%
		\colorbox{#2}%
	}%
	\MakeFramed{\advance\hsize-\width\FrameRestore}%
	\noindent\hspace{-4.55pt}%
	\begin{adjustwidth}{}{7pt}\vspace{2pt}\vspace{2pt}
	}
	{%
		\vspace{2pt}\end{adjustwidth}\endMakeFramed%
}

% 定义不同的自定义定理环境
\newenvironment{defn}{%
	\begin{formal}[Green]{greenshade}\vspace{-\baselineskip / 2}\begin{myDefn}}%
		{\end{myDefn}\end{formal}}

\newenvironment{thm}{%
	\begin{formal}[LightSkyBlue]{lightblueshade}\vspace{-\baselineskip / 2}\begin{myThm}}%
		{\end{myThm}\end{formal}}

\newenvironment{lemma}{%
	\begin{formal}[Plum]{lilacshade}\vspace{-\baselineskip / 2}\begin{myLemma}}%
		{\end{myLemma}\end{formal}}

\newenvironment{corollary}{%
	\begin{formal}[BurlyWood]{brownshade}\vspace{-\baselineskip / 2}\begin{myCorollary}}%
		{\end{myCorollary}\end{formal}}

\newenvironment{criterion}{%
	\begin{formal}[DarkOrange]{orangeshade}\vspace{-\baselineskip / 2}\begin{myCriterion}}%
		{\end{myCriterion}\end{formal}}

\newenvironment{rmk}{%
	\begin{formal}[LightCoral]{redshade}\vspace{-\baselineskip / 2}\begin{myRemark}}%
		{\end{myRemark}\end{formal}}

\newenvironment{proposition}{%
	\begin{formal}[RoyalPurple]{purple}\vspace{-\baselineskip / 2}\begin{myProposition}}%
		{\end{myProposition}\end{formal}}

% 创建一个新计数器 problem，按章节编号
\newcounter{problem}[chapter] 
\newenvironment{problem}{%
	\stepcounter{problem}% 增加problem计数器的值
	\begin{shaded}%
		\par\noindent\textbf{题目 \thechapter.\theproblem}%
	}{%
	\end{shaded}%
	\par%
}
% 定义 answer 环境
\newenvironment{answer}{\par\noindent\textbf{证明 }}{\par}

% 定义 example 定理环境，不与 examplezero 冲突
\newtheorem{example}{\indent \color{SeaGreen}{Example}}[section]

% 修改 proofname 为自定义样式
\renewcommand{\proofname}{\indent\textbf{\textcolor{TealBlue}{Proof}}}

% 定义 solution 环境，作为定理环境的变种
\newenvironment{solution}{%
	\begin{proof}[\indent\textbf{\textcolor{TealBlue}{Solution}}]}{\end{proof}}
	
```

```latex
% \input{\basicPath/format}


\definecolor{mygreen}{rgb}{0,0.6,0}
\definecolor{mygray}{rgb}{0.5,0.5,0.5}
\definecolor{mymauve}{rgb}{0.58,0,0.82}

% 图形文件搜索路径
\graphicspath{ {cover/figure/},{figure/},{chap1/figure/},{chap2/figure/} ，{chap3/figure} }

% 让\section标题靠左对齐
\titleformat{\section}[block]{\normalfont\Large\bfseries}{\thesection}{1em}{}
% 设置行距
\linespread{1.6}

\geometry{
    top=25.4mm, 
    bottom=25.4mm, 
    left=20mm, 
    right=20mm, 
    headheight=2.17cm, 
    headsep=4mm, 
    footskip=12mm
}
% 设置列表环境
\setenumerate[1]{itemsep=5pt,partopsep=0pt,parsep=\parskip,topsep=5pt}
\setitemize[1]{itemsep=5pt,partopsep=0pt,parsep=\parskip,topsep=5pt}
\setdescription{itemsep=5pt,partopsep=0pt,parsep=\parskip,topsep=5pt}

\lstset{
    language=Mathematica,
    basicstyle=\tt,
    breaklines=true,
    keywordstyle=\bfseries\color{NavyBlue}, 
    emphstyle=\bfseries\color{Rhodamine},
    commentstyle=\itshape\color{black!50!white}, 
    stringstyle=\bfseries\color{PineGreen!90!black},
    columns=flexible,
    numbers=left,
    numberstyle=\footnotesize,
    frame=tb,
    breakatwhitespace=false,
} 
```



主要是一些自定义的环境或者命令

**`note.tex`**

- `notes`,存在问题，待解决
- `change`，`change2`![image-20241022164132282](C:\Users\chen1\AppData\Roaming\Typora\typora-user-images\image-20241022164132282.png)
- `tip`,`warning`,`important`,![image-20241022164334434](C:\Users\chen1\AppData\Roaming\Typora\typora-user-images\image-20241022164334434.png)
- `introduction`，可以加引用![image-20241022164627901](C:\Users\chen1\AppData\Roaming\Typora\typora-user-images\image-20241022164627901.png)
- 俩个example环境，`examplezero（note下的）`，![image-20241022164839778](C:\Users\chen1\AppData\Roaming\Typora\typora-user-images\image-20241022164839778.png)

`theorem.tex`下的主要是一些定理定义环境这些

- `defn`,定义的环境![image-20241022165109832](C:\Users\chen1\AppData\Roaming\Typora\typora-user-images\image-20241022165109832.png)

- `thm`，定理的环境，![image-20241022165311372](C:\Users\chen1\AppData\Roaming\Typora\typora-user-images\image-20241022165311372.png)

- `lemma`,引理，![image-20241022165409054](C:\Users\chen1\AppData\Roaming\Typora\typora-user-images\image-20241022165409054.png)

- `corollary`,推论，![image-20241022165449010](C:\Users\chen1\AppData\Roaming\Typora\typora-user-images\image-20241022165449010.png)

- `criterion`,标准，![image-20241022165600381](C:\Users\chen1\AppData\Roaming\Typora\typora-user-images\image-20241022165600381.png)

- `rmk`,备注，![image-20241022165635250](C:\Users\chen1\AppData\Roaming\Typora\typora-user-images\image-20241022165635250.png)

- `proposition`,命题，![image-20241022165713287](C:\Users\chen1\AppData\Roaming\Typora\typora-user-images\image-20241022165713287.png)

- `problem`,题目，![image-20241022165836312](C:\Users\chen1\AppData\Roaming\Typora\typora-user-images\image-20241022165836312.png)

- `answer`，证明，![image-20241022165920377](C:\Users\chen1\AppData\Roaming\Typora\typora-user-images\image-20241022165920377.png)

- `example`,![image-20241022165958424](C:\Users\chen1\AppData\Roaming\Typora\typora-user-images\image-20241022165958424.png)

- ` proof`,证明，![image-20241022170300905](C:\Users\chen1\AppData\Roaming\Typora\typora-user-images\image-20241022170300905.png)

- `solution `，解决方案，![image-20241022170129979](C:\Users\chen1\AppData\Roaming\Typora\typora-user-images\image-20241022170129979.png)

  