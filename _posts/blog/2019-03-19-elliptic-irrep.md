---
layout: post
title: "$\\ell$-adic Representations of Elliptic Curves"
modified:
categories: blog
excerpt:
tags: [math, irreducible, elliptic curve, galois group, representation, algebraic number theory]
date: 2019-07-28
hidden: true
---

<b>If you're somehow seeing this right now, look away. It's not finished, and I'm not sure when/if it will be</b>

The title of this post is a bit of a misnomer. We won't be talking about representations of elliptic curves, but about representations attached to (associated with?) elliptic curves. In particular, the goal of this post is to prove that given an elliptic curve $E/\Q$ defined over the rationals, and a prime $\l$, the $\l$-adic representation $G_{\Q}\to\GL(T_\l(E))\iso\GL_2(\Z_\l)\subset\GL_2(\Q_\l)$ is irreducible where $G_{\Q}=\Gal(\Qbar/\Q)$ is the absolute Galois group of $\Q$. If you don't know what some of these words mean, don't worry; I'll explain.

# Prelim on Elliptic Curves

An <b>elliptic curve</b> is a curve of genus with a specified base point. This is basically a fancy way of saying that elliptic curves are (one-holed) tori. Now, a torus is not a priori something you would think to call a "curve," so I guess we'll start by explaining why tori are in fact curves. 