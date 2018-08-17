$$

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
\newcommand{\grad}{\nabla}
\newcommand{\freemod}[0]{R^{\oplus S}}
\newcommand{\Ith}[2]{#1^{\left(#2\right)}}
\newcommand{\ith}[1]{\Ith{#1}i}
\newcommand{\Itht}[2]{(\Ith{#1}{#2})^T}
\newcommand{\Ithi}[2]{(\Ith{#1}{#2})^{-1}}
\newcommand{\itht}[1]{(\ith{#1})^T}
\newcommand{\vft}[2]{#1\pderivd{x_1}+#2\pderivd{x_2}} % vector (field) in \R^2
\newcommand{\mbf}{\mathbf}
\newcommand{\mbfx}{\mathbf x}
\newcommand{\mbfy}{\mathbf y}
\newcommand{\mbfU}{\mathbf U}
\newcommand{\hvec}[2]{\begin{pmatrix}#1 & #2 \end{pmatrix}}
\newcommand{\hVec}[3]{\begin{pmatrix}#1 & #2 & #3 \end{pmatrix}}
\newcommand{\vvec}[2]{\begin{pmatrix}#1 \\ #2 \end{pmatrix}}
\newcommand{\vVec}[3]{\begin{pmatrix}#1 \\ #2 \\ #3 \end{pmatrix}}
\newcommand{\mat}[4]{\begin{pmatrix}#1 & #2\\ #3 & #4\end{pmatrix}}
\newcommand{\Mat}[9]{\begin{pmatrix}#1&#2&#3\\#4&#5&#6\\#7&#8&#9\end{pmatrix}}
\newcommand{\prb}[1]{P\left\{#1\right\}}
\newcommand{\tbf}{\textbf}
\newcommand{\Norm}[1]{\left\|#1\right\|}
\newcommand{\Zmod}[1]{\frac{\Z}{#1\Z}}
\newcommand{\Layer}[2]{#1^{\left[#2\right]}}
\newcommand{\KL}[2]{\mathrm{KL}\left(#1\left\|\,#2\right.\right)}
\newcommand{\Wedge}{\bigwedge\nolimits}
\newcommand{\Item}[1]{\item[\tbf{(#1)}]}
\newcommand{\Span}[1]{\spn\{#1\}}
\newcommand{\dual}[1]{#1^\vee}
\newcommand{\jota}{\reflectbox{$\iota$}}
\newcommand{\atoi}{\jota}
\newcommand{\qadjzeta}[1]{\Q\left(\zeta_{#1}\right)}
\newcommand{\zadjzeta}[1]{\Z\left[\zeta_{#1}\right]}
\newcommand{\omittedproof}{\begin{proof}Omitted\end{proof}}
\newcommand{\msO}{\mathscr O}
\newcommand{\sm}{\setminus}
\newcommand{\mscr}{\mathscr}
\newcommand{\mf}{\mathfrak}
\newcommand{\floor}[1]{\left\lfloor#1\right\rfloor}
\newcommand{\ceil}[1]{\left\lceil#1\right\rceil}
\newcommand{\mfc}{\mf c}
\newcommand{\msI}{\mathscr I}
\newcommand{\msJ}{\mathscr J}
\newcommand{\ms}{\mathscr}
\newcommand{\mfq}{\mf q}
\newcommand{\sep}[1]{#1_{\mathrm{sep}}}
\newcommand{\units}[1]{#1^{\times}}
\newcommand{\inv}[1]{#1^{-1}}
\newcommand{\mfP}{\mf P}
\newcommand{\bits}{\{0,1\}}
\newcommand{\concat}{\,\|\,}
\newcommand{\mc}{\mathcal}
\newcommand{\parens}[1]{\left(#1\right)}
\newcommand{\brackets}[1]{\left\{#1\right\}}
\newcommand{\sqbracks}[1]{\left[#1\right]}
\newcommand{\nabs}[0]{|\,\cdot\,|} % norm + absolute value
\renewcommand{\l}{\ell}
\newcommand{\sinv}{\inv S}
\newcommand{\gnabs}[0]{|g^{-1}(\,\cdot\,)|}
\renewcommand{\tilde}{\widetilde}
\newcommand{\invlim}{\varprojlim}
\newcommand{\mfa}{\mf a}
\newcommand{\mfb}{\mf b}
\newcommand{\codiff}[1]{#1^\*}
\newcommand{\mbb}{\mathbb}
\newcommand{\actson}{\curvearrowright}

\DeclareMathOperator{\image}{image}
\DeclareMathOperator{\Hom}{Hom}
\DeclareMathOperator{\End}{End}
\DeclareMathOperator{\Tor}{Tor}
\DeclareMathOperator{\ann}{Ann}
\DeclareMathOperator{\spn}{span}
\DeclareMathOperator{\ztensor}{\otimes_{\mathbb Z}}
\DeclareMathOperator{\zHom}{Hom_{\mathbb Z}}
\DeclareMathOperator{\qz}{\mathbb Q/\mathbb Z}
\DeclareMathOperator{\Sym}{Sym}
\DeclareMathOperator{\F}{\mathbb F}
\DeclareMathOperator{\trace}{tr}
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
\DeclareMathOperator{\coker}{coker}
\DeclareMathOperator{\N}{\mathbb N}
\DeclareMathOperator{\diag}{diag}
\DeclareMathOperator{\E}{\mathbb E}
\DeclareMathOperator{\Ext}{Ext}
\renewcommand{\hom}{\mathrm H}
\DeclareMathOperator{\ZG}{\Z G}
\renewcommand{\d}{\,\mathrm d} % unsure if I prefer this or just regular $d$
\DeclareMathOperator{\Cov}{Cov}
\DeclareMathOperator{\sat}{sat}
\DeclareMathOperator{\Torsion}{Torsion}
\DeclareMathOperator{\Var}{Var}
\DeclareMathOperator{\Corr}{Corr}
\DeclareMathOperator{\lead}{lead}
\DeclareMathOperator{\qtensor}{\otimes_{\Q}}
\DeclareMathOperator{\Aut}{Aut}
\DeclareMathOperator{\trdeg}{trdeg}
\DeclareMathOperator{\Tr}{Tr}
\DeclareMathOperator{\Pic}{Pic}
\DeclareMathOperator{\atensor}{\otimes_A}
\DeclareMathOperator{\Spec}{Spec}
\DeclareMathOperator{\ord}{ord}
\DeclareMathOperator{\Frob}{Frob}
\DeclareMathOperator{\Adv}{Adv}
\DeclareMathOperator{\parity}{parity}
\DeclareMathOperator{\reverse}{reverse}
\DeclareMathOperator{\EXP}{EXP}
\DeclareMathOperator{\proj}{proj}
\DeclareMathOperator{\A}{\mathbb A}
\DeclareMathOperator{\spec}{spec}
%\renewcommand{\phi}{\varphi}
\DeclareMathOperator{\cl}{cl}
\DeclareMathOperator{\vol}{vol}
\renewcommand{\split}{\textrm{split}}
\DeclareMathOperator{\Qbar}{\bar\Q}
\renewcommand{\P}{\mathbb P}
\renewcommand{\Re}{\mathrm{Re}\,}
\renewcommand{\Im}{\mathrm{Im}\,}
\DeclareMathOperator{\Stab}{Stab}

\newcommand{\xxsspacing}[0]{\hspace*{3pt}}
\newcommand{\xsspacing}[0]{\hspace*{10pt}}
\newcommand{\sspacing}[0]{\hspace*{25pt}}
\newcommand{\mspacing}[0]{\hspace*{50pt}}
\newcommand{\Text}[2]{\text{#2 #1 #2}}

$$