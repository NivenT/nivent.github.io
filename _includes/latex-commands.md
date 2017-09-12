$$

\newcommand{\downmapsto}{\rotatebox[origin=c]{-90}{$\scriptstyle\mapsto$}\mkern2mu}

\newcommand{\qadj}[1]{\mathbb Q\left(#1\right)}
\newcommand{\qadjs}[1]{\qadj{\sqrt {#1}}}
\newcommand{\qadjns}[1]{\qadjs{-#1}}
\newcommand{\qbrac}[1]{\mathbb Q\left[#1\right]}
\newcommand{\qext}[1]{\qadj{#1}/\mathbb Q}
\newcommand{\zadj}[1]{\mathbb Z\left[#1\right]}
\newcommand{\zadjs}[1]{\zadj{\sqrt {#1}}}
\newcommand{\zadjns}[1]{\zadjs{-#1}}
\newcommand{\zmod}[1]{\mathbb Z/#1\mathbb Z}
\newcommand{\legendre}[2]{\left(\frac{#1}{#2}\right)}
\newcommand{\ints}[1]{\mathscr O_{#1}}
\newcommand{\zloc}[1]{\Z_{(#1)}}
\newcommand{\loc}[2]{#1_{\mathfrak #2}}
\newcommand{\idealloc}[2]{\mathfrak #2\loc{#1}{#2}}
\newcommand{\gen}[1]{\left\langle #1 \right\rangle}
\newcommand{\pres}[2]{\left\langle #1\mid #2 \right\rangle}
\newcommand{\closure}[1]{\text{cl}(#1)}
\newcommand{\op}[0]{^\text{op}}
\newcommand{\angled}[2]{\left\langle#1,#2\right\rangle}
\newcommand{\conj}{\overline}
\newcommand{\pderiv}[2]{\frac{\partial #1}{\partial #2}}
\newcommand{\pderivf}[2]{\partial #1/\partial #2}
\newcommand{\pderivd}[1]{\pderiv{}{#1}}
\newcommand{\pderivdf}[1]{\pderivf{}{#1}}
\newcommand{\Pderiv}[3]{\frac{\partial #1}{\partial #2\partial #3}}
\newcommand{\dtwo}[1]{\pderiv{#1}x\,dx + \pderiv{#1}y\,dy}
\newcommand{\dthree}[1]{\dtwo{#1} + \pderiv{#1}z\,dz}
\newcommand{\mfp}{\mathfrak p}
\newcommand{\mfm}{\mathfrak m}
\newcommand{\mfX}{\mathfrak X}
\newcommand{\abs}[1]{\left|#1\right|}
\newcommand{\smooth}[0]{C^\infty}
\newcommand{\del}[0]{\partial}

\DeclareMathOperator{\image}{image}
\DeclareMathOperator{\Hom}{Hom}
\DeclareMathOperator{\End}{End}
\DeclareMathOperator{\Tor}{Tor}
\DeclareMathOperator{\ann}{ann}
\DeclareMathOperator{\spn}{span}
\DeclareMathOperator{\ztensor}{\otimes_{\mathbb Z}}
\DeclareMathOperator{\zHom}{Hom_{\mathbb Z}}
\DeclareMathOperator{\qz}{\mathbb Q/\mathbb Z}
\DeclareMathOperator{\Sym}{Sym}
\DeclareMathOperator{\F}{\mathbb F}
\DeclareMathOperator{\trace}{Trace}
\DeclareMathOperator{\sign}{sign}
\DeclareMathOperator{\Q}{\mathbb Q}
\DeclareMathOperator{\Z}{\mathbb Z}
\DeclareMathOperator{\GL}{GL}
\DeclareMathOperator{\C}{\mathbb C}
\DeclareMathOperator{\Ind}{Ind}
\DeclareMathOperator{\Res}{Res}
\DeclareMathOperator{\R}{\mathbb R}
\DeclareMathOperator{\norm}{N}
\DeclareMathOperator{\aut}{Aut}
\DeclareMathOperator{\disc}{disc}
\DeclareMathOperator{\Gal}{Gal}
\DeclareMathOperator{\knorm}{\norm_{K/\mathbb Q}}
\DeclareMathOperator{\zdisc}{disc_{\mathbb Z}}
\DeclareMathOperator{\Cl}{Cl}
\DeclareMathOperator{\ktrace}{\trace_{K/\mathbb Q}}
\DeclareMathOperator{\Char}{char}
\DeclareMathOperator{\denom}{denom}
\DeclareMathOperator{\Frac}{Frac}
\DeclareMathOperator{\rank}{rank}
\DeclareMathOperator{\Fr}{Fr}
\DeclareMathOperator{\eps}{\varepsilon}
\DeclareMathOperator{\vphi}{\varphi}

\theoremstyle{plain}
\newtheorem{thm}{Theorem}
\newtheorem{lemma}[thm]{Lemma}
\newtheorem{cor}[thm]{Corollary}
\newtheorem{conject}[thm]{Conjecture}
\newtheorem{prop}[thm]{Proposition}
\newtheorem{heur}[thm]{Heuristic}
\newtheorem{qn}[thm]{Question}
\newtheorem{claim}[thm]{Claim}
\newtheorem{prob}{Problem}

\theoremstyle{definition}
\newtheorem{defn}[thm]{Definition}
\newtheorem{cond}[thm]{Conditions}
\newtheorem{notn}{Notation}
\newtheorem{anotn}[notn]{Abuse of Notation}
\newtheorem{san}[thm]{Sanity Check}

\theoremstyle{remark}
\newtheorem{rem}[thm]{Remark}
\newtheorem*{ex}{Example}
\newtheorem*{nonex}{Non-example}
\newtheorem*{exc}{Exercise}

\renewcommand{\qedsymbol}{$\blacksquare$}

\newcommand{\mspacing}[0]{\hspace*{50pt}}
\newcommand{\Text}[2]{\text{#2 #1 #2}}

$$