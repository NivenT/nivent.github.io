$$
%% Below are very ill-defined categories

%% Linear Algebra
\newcommand{\angled}[2]{\left\langle#1,#2\right\rangle}
\newcommand{\hvec}[2]{\begin{pmatrix}#1& #2\end{pmatrix}}
\newcommand{\hVec}[3]{\begin{pmatrix}#1& #2& #3\end{pmatrix}}
\newcommand{\vvec}[2]{\begin{pmatrix}#1\\#2\end{pmatrix}}
\newcommand{\vVec}[3]{\begin{pmatrix}#1\\#2\\#3\end{pmatrix}}
\newcommand{\mat}[4]{\begin{pmatrix}#1& #2\\ #3& #4\end{pmatrix}}
\newcommand{\Mat}[9]{\begin{pmatrix}#1& #2& #3\\#4& #5& #6\\#7& #8& #9\end{pmatrix}}
\newcommand{\Wedge}{\bigwedge\nolimits}
\newcommand{\Span}[1]{\spn\left\{#1\right\}}
\newcommand{\dual}[1]{#1^\vee}
\DeclareMathOperator{\spn}{span}
\DeclareMathOperator{\trace}{tr}
\DeclareMathOperator{\diag}{diag}

%% Abstract Algebra
\newcommand{\gen}[1]{\left\langle #1 \right\rangle}
\newcommand{\pres}[2]{\left\langle #1\mid #2 \right\rangle}
\newcommand{\op}[0]{^\text{op}}
\newcommand{\freemod}[0]{R^{\oplus S}}
\newcommand{\units}[1]{#1^{\times}}
\newcommand{\punits}[1]{\units{\parens{#1}}}
\newcommand{\inv}[1]{#1^{-1}}
\newcommand{\pinv}[1]{\inv{\parens{#1}}}
\newcommand{\sinv}{\inv S}
\newcommand{\invlim}{\varprojlim\limits}
\newcommand{\dirlim}{\varinjlim\limits}
\newcommand{\ses}[5]{
	\begin{tikzcd}[ampersand replacement=\&]
		0\arrow[r]\& #1\arrow[r, "#2"]\& #3\arrow[r, "#4"]\& #5\arrow[r]\&0
	\end{tikzcd}
}
\newcommand{\scmplx}[5]{ % single complex
	\begin{tikzcd}[ampersand replacement=\&]
		#1\arrow[r, "#2"]\& #3\arrow[r, "#4"]\& #5
	\end{tikzcd}
}
\newcommand{\lses}[5]{
	\begin{tikzcd}[ampersand replacement=\&]
		0\arrow[r]\& #1\arrow[r, "#2"]\& #3\arrow[r, "#4"]\& #5
	\end{tikzcd}
}
\newcommand{\rses}[5]{
	\begin{tikzcd}[ampersand replacement=\&]
		#1\arrow[r, "#2"]\& #3\arrow[r, "#4"]\& #5\arrow[r]\&0
	\end{tikzcd}
}
\newcommand{\ab}[1]{#1^{\mathrm{ab}}}
\newcommand{\normal}{\triangleleft}
\DeclareMathOperator{\image}{image}
\DeclareMathOperator{\Hom}{Hom}	
\DeclareMathOperator{\sHom}{\mathcal{H\mkern-7mu}\textit{om}}
\DeclareMathOperator{\End}{End}
\DeclareMathOperator{\Tor}{Tor}
\DeclareMathOperator{\ann}{Ann}
\DeclareMathOperator{\ztensor}{\otimes_{\mathbb Z}}
\DeclareMathOperator{\zHom}{Hom_{\mathbb Z}}
\DeclareMathOperator{\qz}{\mathbb Q/\mathbb Z}
\DeclareMathOperator{\Sym}{Sym}
\DeclareMathOperator{\GL}{GL}
\DeclareMathOperator{\Spin}{Sp} % TODO (?): Change to \Sp
\DeclareMathOperator{\Ind}{Ind}
\DeclareMathOperator{\CoInd}{CoInd}
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
\DeclareMathOperator{\SO}{SO}
\DeclareMathOperator{\ob}{ob}
\DeclareMathOperator{\Mor}{Mor}
\DeclareMathOperator{\Mod}{Mod}
\DeclareMathOperator{\Irr}{Irr} % Do I want a separate section for representation theory?

%% Algebraic Number Theory/Field Theory
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
\newcommand{\codiff}[1]{#1^* }
\newcommand{\compl}[1]{#1^{\wedge}} % Completion
\newcommand{\al}[1]{#1^{\mrm{al}}}
\DeclareMathOperator{\norm}{N}
\DeclareMathOperator{\Aut}{Aut}
\DeclareMathOperator{\disc}{disc}
\DeclareMathOperator{\Gal}{Gal}
\DeclareMathOperator{\knorm}{\norm_{K/\mathbb Q}}
\DeclareMathOperator{\Nm}{Nm}
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
\DeclareMathOperator{\Qbar}{\overline\Q}
\DeclareMathOperator{\lcm}{lcm}

%% Modular Forms/Curves
\newcommand{\sump}{\sideset{}'\sum}
\newcommand{\prodp}{\sideset{}'\prod}
\newcommand{\slz}{\SL_2(\Z)}
\newcommand{\glp}{\GL_2^+}
\renewcommand{\sp}[1]{\sqbracks{\C/\Lambda_{#1},\frac1N+\Lam_{#1}}}
\newcommand{\Sp}[2]{\sqbracks{\C/\Lambda_{#1},\frac1{#2}+\Lam_{#1}}}
\newcommand{\spp}[1]{\sqbracks{\C/\Lambda_{#1},\parens{\frac{#1}N+\Lam_{#1},\frac1N+\Lam_{#1}}}}
\newcommand{\Spp}[2]{\sqbracks{\C/\Lambda_{#1},\parens{\frac{#1}{#2}+\Lam_{#1},\frac1{#2}+\Lam_{#1}}}}
\newcommand{\sg}[1]{\sqbracks{\C/\Lambda_{#1},\angles{\frac1N+\Lam_{#1}}}}
\newcommand{\Sg}[2]{\sqbracks{\C/\Lambda_{#1},\angles{\frac1{#2}+\Lam_{#1}}}}
\newcommand{\pmI}{\bracks{\pm I}}

%% Group cohomology/class field theory
\DeclareMathOperator{\cores}{cor}
\DeclareMathOperator{\tatehom}{\wh\hom}

%% Point-Set Topology
\newcommand{\closure}[1]{\bar{#1}}
\newcommand{\clos}[1]{\overline{#1}}
\newcommand{\interior}[1]{\mathring{#1}}
\newcommand{\open}{\overset{\text{open}}\subset}
\newcommand{\cp}[1]{\overline{\{#1\}}} % closure of point
\DeclareMathOperator{\Cl}{Cl}
\DeclareMathOperator{\cl}{cl}
\DeclareMathOperator{\SP}{SP}
\DeclareMathOperator{\Homeo}{Homeo}

%% Differential Geometry/Topology
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
\newcommand{\dt}[0]{\d t}
\newcommand{\dx}[0]{\d x}
\newcommand{\dy}[0]{\d y}
\newcommand{\dz}[0]{\d z}
\newcommand{\dbz}[0]{\d\bar z}
\newcommand{\df}[0]{\d f}
\newcommand{\dm}[0]{\d m}
\renewcommand{\d}{\mathrm d} % This had a \, in the front before. Will I regret removing it?
\DeclareMathOperator{\Tube}{Tube}
\DeclareMathOperator{\dvol}{dvol}
\DeclareMathOperator{\Todd}{Todd}
\DeclareMathOperator{\ch}{ch}

%% Algebraic Topology
\DeclareMathOperator{\simhom}{\hom^\Delta}
\DeclareMathOperator{\redhom}{\wt\hom}
\DeclareMathOperator{\RP}{\mathbb RP}
\DeclareMathOperator{\CP}{\mathbb CP}
\DeclareMathOperator{\fiber}{fiber}
\DeclareMathOperator{\hofiber}{hofiber}

% Lie Theory
\newcommand{\dg}{\d g}
\newcommand{\rs}[1]{#1^{\mrm{rs}}}
\newcommand{\der}[1]{#1^{\mrm{der}}}
\DeclareMathOperator{\Lie}{Lie}
\DeclareMathOperator{\ad}{ad}
\DeclareMathOperator{\Ad}{Ad}

%% Complex/Algebraic Geometry + Sheaf Theory
\newcommand{\msEX}[1]{\msE_X^{(#1)}}
\newcommand{\red}[1]{#1_{\mrm{red}}}
\newcommand{\cs}[1]{\parens{\ints{#1},\abs{#1}}} % Complex space
\newcommand{\derpush}[2]{#2_{* #1}}
\newcommand{\smp}[1]{#1^{\mrm{sm}}} % smooth points
\renewcommand{\sharp}[1]{#1^\#}
\DeclareMathOperator{\Spec}{\mbf{Spec}}
\DeclareMathOperator{\spec}{spec}
\DeclareMathOperator{\Proj}{Proj}
\DeclareMathOperator{\PAb}{PAb}
\DeclareMathOperator{\Ab}{Ab}
\DeclareMathOperator{\pker}{pker}
\DeclareMathOperator{\pim}{pim}
\DeclareMathOperator{\pcoker}{pcoker}
\DeclareMathOperator{\Et}{Et}
\DeclareMathOperator{\Div}{Div}
\DeclareMathOperator{\res}{res}
\DeclareMathOperator{\bdel}{\bar\del}
\DeclareMathOperator{\cechhom}{\check{H}}
\DeclareMathOperator{\chom}{\cechhom}
\DeclareMathOperator{\kod}{kod}
\DeclareMathOperator{\Sing}{Sing}
\DeclareMathOperator{\Alb}{Alb}
\DeclareMathOperator{\NS}{NS}
\DeclareMathOperator{\Ht}{ht}
\DeclareMathOperator{\codim}{codim}
\DeclareMathOperator{\Sch}{Sch}
\DeclareMathOperator{\Bl}{Bl}

%% Analysis
\newcommand{\meas}{m_{\star}}
\newcommand{\abs}[1]{\left|#1\right|}
\newcommand{\dabs}[1]{\left\|#1\right\|}
\let\templim\lim
\renewcommand{\lim}{\templim\limits}
\DeclareMathOperator{\BV}{BV}

%% Quantum Mechanics/Computing
\newcommand{\ket}[1]{\left|#1\right>}
\newcommand{\keteps}{\ket\eps}

%% Cryptography
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

%% Complexity Theory
\DeclareMathOperator{\NP}{NP}
\DeclareMathOperator{\NL}{NL}
\DeclareMathOperator{\coNL}{coNL}
\DeclareMathOperator{\coNP}{coNP}
\DeclareMathOperator{\TIME}{TIME}
\DeclareMathOperator{\ccP}{P} % cc = complexity class
\DeclareMathOperator{\SAT}{SAT}
\DeclareMathOperator{\UNSAT}{UNSAT}
\DeclareMathOperator{\Perm}{Perm} % Permanent of a matrix
\DeclareMathOperator{\MAJPP}{MAJPP}
\DeclareMathOperator{\ccRP}{RP}
\DeclareMathOperator{\coRP}{coRP}
\DeclareMathOperator{\ZPP}{ZPP}

%% Logic
\newcommand{\biglor}{\bigvee}
\newcommand{\bigland}{\bigwedge}

%% Machine Learning
\newcommand{\grad}{\nabla}
\newcommand{\Ith}[2]{#1^{\left(#2\right)}}
\newcommand{\ith}[1]{\Ith{#1}i}
\newcommand{\Itht}[2]{(\Ith{#1}{#2})^T}
\newcommand{\Ithi}[2]{(\Ith{#1}{#2})^{-1}}
\newcommand{\itht}[1]{(\ith{#1})^T}
\newcommand{\Layer}[2]{#1^{\left[#2\right]}}
\newcommand{\KL}[2]{\mathrm{KL}\left(#1\left\|\,#2\right.\right)}

%% Probability/Statistics
\newcommand{\prb}[1]{P\left\{#1\right\}}
\DeclareMathOperator{\Cov}{Cov}
\DeclareMathOperator{\Var}{Var}
\DeclareMathOperator{\Corr}{Corr}

%% Diagrams
\newcommand{\commsquare}[8]{
	\begin{tikzcd}[ampersand replacement=\&]
	#1\ar[r, "#2"]\ar[d, "#4" left]\& #3\ar[d, "#5" right]\\
	#6\ar[r, "#7" above]\& #8
	\end{tikzcd}
}
\newcommand{\pullback}[6]{\commsquare{#1}{}{#2}{}{#3}{#4}{#5}{#6}}
\newcommand{\pushforward}[6]{\commsquare{#1}{#2}{#3}{#4}{}{#5}{}{#6}}
\newcommand{\barecommsquare}[4]{\commsquare{#1}{}{#2}{}{}{#3}{}{#4}}

%% Limit type things

%% Letters/Fonts
\newcommand{\mfp}{\mathfrak p}
\newcommand{\mfm}{\mathfrak m}
\newcommand{\mfX}{\mathfrak X}
\newcommand{\mfg}{\mathfrak g}
\newcommand{\mfh}{\mathfrak h}
\newcommand{\mfH}{\mathfrak H}
\newcommand{\mft}{\mathfrak t}
\newcommand{\mfgl}{\mathfrak{gl}}
\newcommand{\mfsl}{\mathfrak{sl}}
\newcommand{\mfso}{\mathfrak{so}}
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
\newcommand{\msF}{\ms F}
\newcommand{\msL}{\ms L}
\newcommand{\msM}{\ms M}
\newcommand{\msG}{\ms G}
\newcommand{\ms}{\mathscr}
\newcommand{\mfq}{\mf q}
\newcommand{\mfP}{\mf P}
\newcommand{\mc}{\mathcal}
\newcommand{\mcA}{\mc A}
\newcommand{\mcB}{\mc B}
\newcommand{\mcV}{\mc V}
\newcommand{\mcU}{\mc U}
\newcommand{\mcW}{\mc W}
\newcommand{\mcF}{\mc F}
\newcommand{\mfa}{\mf a}
\newcommand{\mfb}{\mf b}
\newcommand{\mbb}{\mathbb}
\newcommand{\msR}{\ms R}
\newcommand{\msS}{\ms S}
\newcommand{\msA}{\ms A}
\newcommand{\mcH}{\mc H}
\newcommand{\mcS}{\mc S}
\newcommand{\mcM}{\mc M}
\newcommand{\mcL}{\mc L}
\newcommand{\mrm}{\mathrm}
\newcommand{\Lam}{\Lambda}
%\renewcommand{\S}{\mathbb S}
\newcommand{\F}{\mathbb F}
\newcommand{\Q}{\mathbb Q}
\newcommand{\Z}{\mathbb Z}
\newcommand{\R}{\mathbb R}
\newcommand{\C}{\mathbb C}
\newcommand{\E}{\mathbb E}
\newcommand{\N}{\mathbb N}
\newcommand{\T}{\mathbb T}
\newcommand{\A}{\mathbb A}
\newcommand{\eps}{\varepsilon}
\newcommand{\vphi}{\varphi}
\renewcommand{\P}{\mathbb P}
\DeclareMathOperator{\msE}{\ms E}
\renewcommand{\a}{\alpha}
\renewcommand{\b}{\beta}

%% Grouping Operators
\newcommand{\floor}[1]{\left\lfloor#1\right\rfloor}
\newcommand{\ceil}[1]{\left\lceil#1\right\rceil}
\newcommand{\parens}[1]{\left(#1\right)}
\newcommand{\brackets}[1]{\left\{#1\right\}}
\newcommand{\bracks}[1]{\brackets{#1}}
\newcommand{\sqbracks}[1]{\left[#1\right]}
\newcommand{\angles}[1]{\left\langle#1\right\rangle}
\newcommand{\coint}[2]{\left[#1,#2\right)} % Closed, open interval

%% Misc
\newcommand{\actson}{\curvearrowright}
\newcommand{\conj}{\overline}
\newcommand{\tbf}{\textbf}
\newcommand{\bp}[1]{\tbf{(#1)}} % bold parens
\newcommand{\Item}[1]{\item[\tbf{(#1)}]}
\newcommand{\jota}{\reflectbox{$\iota$}}
\newcommand{\atoi}{\jota}
\newcommand{\omittedproof}{\begin{proof}Omitted\end{proof}}
\newcommand{\sm}{\setminus}
\renewcommand{\l}{\ell}
\newcommand{\st}{\tilde} % small tilde
\newcommand{\wt}{\widetilde}
\newcommand{\sh}{\hat} % small hat
\newcommand{\wh}{\widehat}
\newcommand{\vsubseteq}{\rotatebox{90}{$\subseteq$}}
\renewcommand{\ast}[1]{#1^* }
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
\newcommand{\push}[1]{#1_* }
\newcommand{\pull}[1]{#1^* }
\newcommand{\by}{\times}
\newcommand{\from}{\leftarrow}
\newcommand{\xto}{\xrightarrow}
\newcommand{\xfrom}{\xleftarrow}
\newcommand{\xinto}[1]{\overset{#1}\into}
\newcommand{\too}{\longrightarrow}
\newcommand{\xtoo}{\xlongrightarrow}
\newcommand{\iso}{\xto\sim}
\newcommand{\into}{\hookrightarrow}
\newcommand{\onto}{\twoheadrightarrow}
\newcommand{\dashto}{\dashrightarrow}
\newcommand{\mapdesc}[5]{
	\begin{matrix}
		#1:& #2 &\longrightarrow& #3\\
		& #4&\longmapsto& #5
	\end{matrix}
}
\renewcommand{\div}{\mathrm{div}} % Might regret this one day
\DeclareMathOperator{\sign}{sign}
\renewcommand{\Re}{\mathrm{Re}}
\renewcommand{\Im}{\mathrm{Im}}
\newcommand{\nimplies}{\nRightarrow}
\renewcommand{\bar}{\overline}
\DeclareMathOperator{\Map}{Map}
\DeclareMathOperator{\supp}{supp}
\DeclareMathOperator{\Cont}{Cont}
\DeclareMathOperator{\Open}{Open}
\DeclareMathOperator{\id}{id}
\DeclareMathOperator{\Id}{Id}
\DeclareMathOperator{\pr}{pr}

$$