$$

%% Below are very ill-defined categories

% Linear Algebra
\newcommand{\angled}[2]{\left\langle#1,#2\right\rangle}
\newcommand{\hvec}[2]{\begin{pmatrix}#1&#2\end{pmatrix}}
\newcommand{\hVec}[3]{\begin{pmatrix}#1&#2&#3\end{pmatrix}}
\newcommand{\vvec}[2]{\begin{pmatrix}#1\\#2\end{pmatrix}}
\newcommand{\vVec}[3]{\begin{pmatrix}#1\\#2\\#3\end{pmatrix}}
\newcommand{\mat}[4]{\begin{pmatrix}#1&#2\\#3&#4\end{pmatrix}}
\newcommand{\Mat}[9]{\begin{pmatrix}#1&#2&#3\\#4&#5&#6\\#7&#8&#9\end{pmatrix}}
\newcommand{\Wedge}{\bigwedge\nolimits}
\newcommand{\Span}[1]{\spn\{#1\}}
\newcommand{\dual}[1]{#1^\vee}
\DeclareMathOperator{\spn}{span}
\DeclareMathOperator{\trace}{tr}
\DeclareMathOperator{\diag}{diag}

% Algebra
\newcommand{\gen}[1]{\left\langle #1 \right\rangle}
\newcommand{\pres}[2]{\left\langle #1\mid #2 \right\rangle}
\newcommand{\op}[0]{^\text{op}}
\newcommand{\freemod}[0]{R^{\oplus S}}
\newcommand{\units}[1]{#1^{\times}}
\newcommand{\inv}[1]{#1^{-1}}
\newcommand{\sinv}{\inv S}
\newcommand{\invlim}{\varprojlim}
\newcommand{\dirlim}{\varinjlim}
\newcommand{\ses}[5]{
	\begin{tikzcd}[ampersand replacement=\&]
		0\arrow[r]\&#1\arrow[r, "#2"]\&#3\arrow[r, "#4"]\&#5\arrow[r]\&0
	\end{tikzcd}
}
\newcommand{\scmplx}[5]{ % single complex
	\begin{tikzcd}[ampersand replacement=\&]
		#1\arrow[r, "#2"]\&#3\arrow[r, "#4"]\&#5
	\end{tikzcd}
}
\newcommand{\lses}[5]{
	\begin{tikzcd}[ampersand replacement=\&]
		0\arrow[r]\&#1\arrow[r, "#2"]\&#3\arrow[r, "#4"]\&#5
	\end{tikzcd}
}
\newcommand{\rses}[5]{
	\begin{tikzcd}[ampersand replacement=\&]
		#1\arrow[r, "#2"]\&#3\arrow[r, "#4"]\&#5\arrow[r]\&0
	\end{tikzcd}
}
\newcommand{\ab}[1]{#1^{\mathrm{ab}}}
\DeclareMathOperator{\image}{image}
\DeclareMathOperator{\Hom}{Hom}
\DeclareMathOperator{\End}{End}
\DeclareMathOperator{\Tor}{Tor}
\DeclareMathOperator{\ann}{Ann}
\DeclareMathOperator{\ztensor}{\otimes_{\mathbb Z}}
\DeclareMathOperator{\zHom}{Hom_{\mathbb Z}}
\DeclareMathOperator{\qz}{\mathbb Q/\mathbb Z}
\DeclareMathOperator{\Sym}{Sym}
\DeclareMathOperator{\GL}{GL}
\DeclareMathOperator{\Ind}{Ind}
\DeclareMathOperator{\Res}{Res}
\DeclareMathOperator{\coker}{coker}
\DeclareMathOperator{\Ext}{Ext}
\renewcommand{\hom}{\mathrm H}
\DeclareMathOperator{\ZG}{\Z G}
\DeclareMathOperator{\sat}{sat}
\DeclareMathOperator{\Torsion}{Torsion}
\DeclareMathOperator{\lead}{lead}
\DeclareMathOperator{\qtensor}{\otimes_{\Q}}
\DeclareMathOperator{\Stab}{Stab}
\DeclareMathOperator{\im}{im}
\DeclareMathOperator{\SL}{SL}
\DeclareMathOperator{\PSL}{PSL}
\DeclareMathOperator{\PGL}{PGL}

% Number Theory/Field Theory
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
\newcommand{\Norm}[1]{\left\|#1\right\|}
\newcommand{\Zmod}[1]{\frac{\Z}{#1\Z}}
\newcommand{\qadjzeta}[1]{\Q\left(\zeta_{#1}\right)}
\newcommand{\zadjzeta}[1]{\Z\left[\zeta_{#1}\right]}
\newcommand{\sep}[1]{#1_{\mathrm{sep}}}
\newcommand{\nabs}[0]{|\,\cdot\,|} % norm + absolute value
\newcommand{\gnabs}[0]{|g^{-1}(\,\cdot\,)|}
\newcommand{\codiff}[1]{#1^\*}
\newcommand{\compl}[1]{#1^{\wedge}} % Completion
\DeclareMathOperator{\norm}{N}
\DeclareMathOperator{\Aut}{Aut}
\DeclareMathOperator{\disc}{disc}
\DeclareMathOperator{\Gal}{Gal}
\DeclareMathOperator{\knorm}{\norm_{K/\mathbb Q}}
\DeclareMathOperator{\zdisc}{disc_{\mathbb Z}}
\DeclareMathOperator{\ktrace}{\trace_{K/\mathbb Q}}
\DeclareMathOperator{\Char}{char}
\DeclareMathOperator{\denom}{denom}
\DeclareMathOperator{\Frac}{Frac}
\DeclareMathOperator{\rank}{rank}
\DeclareMathOperator{\Fr}{Fr}
\DeclareMathOperator{\trdeg}{trdeg}
\DeclareMathOperator{\Tr}{Tr}
\DeclareMathOperator{\Pic}{Pic}
\DeclareMathOperator{\atensor}{\otimes_A}
\DeclareMathOperator{\ord}{ord}
\DeclareMathOperator{\Frob}{Frob}
\DeclareMathOperator{\vol}{vol}
\renewcommand{\split}{\textrm{split}}
\DeclareMathOperator{\Qbar}{\bar\Q}

% Point-Set Topology
\newcommand{\closure}[1]{\bar{#1}}
\newcommand{\clos}[1]{\overline{#1}}
\newcommand{\interior}[1]{\mathring{#1}}
\DeclareMathOperator{\Cl}{Cl}
\DeclareMathOperator{\cl}{cl}
\DeclareMathOperator{\Homeo}{Homeo}

% Differential Geometry/Topology
\newcommand{\pderiv}[2]{\frac{\partial #1}{\partial #2}}
\newcommand{\pderivf}[2]{\partial #1/\partial #2}
\newcommand{\pderivd}[1]{\pderiv{}{#1}}
\newcommand{\pderivdf}[1]{\pderivf{}{#1}}
\newcommand{\Pderiv}[3]{\frac{\partial #1}{\partial #2\partial #3}}
\newcommand{\dtwo}[1]{\pderiv{#1}x\,dx + \pderiv{#1}y\,dy}
\newcommand{\dthree}[1]{\dtwo{#1} + \pderiv{#1}z\,dz}
\newcommand{\smooth}[0]{C^\infty}
\newcommand{\del}[0]{\partial}
\newcommand{\vft}[2]{#1\pderivd{x_1}+#2\pderivd{x_2}} % vector (field) in \R^2
\newcommand{\dx}[0]{\d x}
\newcommand{\dy}[0]{\d y}
\newcommand{\dz}[0]{\d z}
\newcommand{\dbz}[0]{\d\bar z}
\renewcommand{\d}{\,\mathrm d} 
\DeclareMathOperator{\Tube}{Tube}
\DeclareMathOperator{\dvol}{dvol}

% Algebraic Topology
\DeclareMathOperator{\simhom}{\hom^\Delta}
\DeclareMathOperator{\redhom}{\wt\hom}
\DeclareMathOperator{\RP}{\mathbb RP}
\DeclareMathOperator{\CP}{\mathbb CP}

% Complex/Algebraic Geometry + Sheaf Theory
\newcommand{\msEX}[1]{\msE_X^{(#1)}}
\DeclareMathOperator{\Spec}{Spec}
\DeclareMathOperator{\spec}{spec}
\DeclareMathOperator{\PAb}{PAb}
\DeclareMathOperator{\Ab}{Ab}
\DeclareMathOperator{\pker}{pker}
\DeclareMathOperator{\pim}{pim}
\DeclareMathOperator{\pcoker}{pcoker}
\DeclareMathOperator{\Et}{Et}
\DeclareMathOperator{\Div}{Div}
\DeclareMathOperator{\res}{res}
\DeclareMathOperator{\bdel}{\bar\del}

% Analysis
\newcommand{\meas}{m_{\star}}

% Quantum Mechanics/Computing
\newcommand{\ket}[1]{\left|#1\right>}
\newcommand{\keteps}{\ket\eps}

% Cryptography
\newcommand{\bits}{\{0,1\}}
\newcommand{\concat}{\,\|\,}
\newcommand{\uniform}{\xleftarrow R}
\DeclareMathOperator{\Adv}{Adv}
\DeclareMathOperator{\parity}{parity}
\DeclareMathOperator{\reverse}{reverse}
\DeclareMathOperator{\EXP}{EXP}
\DeclareMathOperator{\poly}{poly}
\DeclareMathOperator{\perm}{perm}
\DeclareMathOperator{\Commit}{Commit}
\DeclareMathOperator{\negl}{negl}
\DeclareMathOperator{\PRF}{PRFAdv}
\DeclareMathOperator{\SCPRF}{SC-PRF}
\DeclareMathOperator{\DDH}{DDHAdv}
\DeclareMathOperator{\pub}{pub}
\DeclareMathOperator{\priv}{priv}
\DeclareMathOperator{\key}{key}

% Machine Learning
\newcommand{\grad}{\nabla}
\newcommand{\Ith}[2]{#1^{\left(#2\right)}}
\newcommand{\ith}[1]{\Ith{#1}i}
\newcommand{\Itht}[2]{(\Ith{#1}{#2})^T}
\newcommand{\Ithi}[2]{(\Ith{#1}{#2})^{-1}}
\newcommand{\itht}[1]{(\ith{#1})^T}
\newcommand{\Layer}[2]{#1^{\left[#2\right]}}
\newcommand{\KL}[2]{\mathrm{KL}\left(#1\left\|\,#2\right.\right)}

% Probability/Statistics
\newcommand{\prb}[1]{P\left\{#1\right\}}
\DeclareMathOperator{\Cov}{Cov}
\DeclareMathOperator{\Var}{Var}
\DeclareMathOperator{\Corr}{Corr}

% Letters/Fonts
\newcommand{\mfp}{\mathfrak p}
\newcommand{\mfm}{\mathfrak m}
\newcommand{\mfX}{\mathfrak X}
\newcommand{\mbf}{\mathbf}
\newcommand{\mbfx}{\mathbf x}
\newcommand{\mbfy}{\mathbf y}
\newcommand{\mbfU}{\mathbf U}
\newcommand{\msO}{\mathscr O}
\newcommand{\mscr}{\mathscr}
\newcommand{\mf}{\mathfrak}
\newcommand{\mfc}{\mf c}
\newcommand{\msI}{\mathscr I}
\newcommand{\msJ}{\mathscr J}
\newcommand{\msP}{\mathscr P}
\newcommand{\ms}{\mathscr}
\newcommand{\mfq}{\mf q}
\newcommand{\mfP}{\mf P}
\newcommand{\mc}{\mathcal}
\newcommand{\mfa}{\mf a}
\newcommand{\mfb}{\mf b}
\newcommand{\mbb}{\mathbb}
\newcommand{\msR}{\ms R}
\newcommand{\msS}{\ms S}
\DeclareMathOperator{\F}{\mathbb F}
\DeclareMathOperator{\Q}{\mathbb Q}
\DeclareMathOperator{\Z}{\mathbb Z}
\DeclareMathOperator{\R}{\mathbb R}
\DeclareMathOperator{\C}{\mathbb C}
\DeclareMathOperator{\E}{\mathbb E}
\DeclareMathOperator{\N}{\mathbb N}
\DeclareMathOperator{\eps}{\varepsilon}
\DeclareMathOperator{\vphi}{\varphi}
\DeclareMathOperator{\A}{\mathbb A}
\renewcommand{\P}{\mathbb P}
\DeclareMathOperator{\msE}{\ms E}
\DeclareMathOperator{\mcA}{\mc A}
\DeclareMathOperator{\mcB}{\mc B}

% Grouping Operators
\newcommand{\floor}[1]{\left\lfloor#1\right\rfloor}
\newcommand{\ceil}[1]{\left\lceil#1\right\rceil}
\newcommand{\parens}[1]{\left(#1\right)}
\newcommand{\brackets}[1]{\left\{#1\right\}}
\newcommand{\sqbracks}[1]{\left[#1\right]}

% Misc
\newcommand{\conj}{\overline}
\newcommand{\abs}[1]{\left|#1\right|}
\newcommand{\tbf}{\textbf}
\newcommand{\Item}[1]{\item[\tbf{(#1)}]}
\newcommand{\jota}{\reflectbox{$\iota$}}
\newcommand{\atoi}{\jota}
\newcommand{\omittedproof}{\begin{proof}Omitted\end{proof}}
\newcommand{\sm}{\setminus}
\renewcommand{\l}{\ell}
\renewcommand{\tilde}{\widetilde}
\newcommand{\wt}{\widetilde}
\newcommand{\wh}{\widehat}
\newcommand{\vsubseteq}{\rotatebox{90}{$\subseteq$}}
\renewcommand{\ast}[1]{#1^*}
\newcommand{\twocases}[3]{
	\begin{cases}
		\hfill#1\hfill&\text{if }#2\\
		\hfill#3\hfill&\text{otherwise}
	\end{cases}
}
\newcommand{\Twocases}[4]{
	\begin{cases}
		\hfill#1\hfill&\text{if }#2\\
		\hfill#3\hfill&\text{if }#4
	\end{cases}
}
\newcommand{\xlongleftarrow}[1]{\overset{#1}{\longleftarrow}}
\newcommand{\xlongrightarrow}[1]{\overset{#1}{\longrightarrow}}
\newcommand{\push}[1]{#1_*}
\newcommand{\by}{\times}
\DeclareMathOperator{\sign}{sign}
\renewcommand{\Re}{\mathrm{Re}\,}
\renewcommand{\Im}{\mathrm{Im}\,}
\DeclareMathOperator{\Map}{Map}
\DeclareMathOperator{\supp}{supp}
\DeclareMathOperator{\Cont}{Cont}
\DeclareMathOperator{\Open}{Open}

$$