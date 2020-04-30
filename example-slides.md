---
author:
- Caroline Möller
title: The oemof.thermal package
subtitle: How to use the new thermal components
institute: Reiner Lemoine Institut, Beuth University of Applied Sciences
classoption: aspectratio=169
date: \today
theme: rli
urlcolor: rlilinkcolor
header-includes:
- |
  \newcommand{\tel}{+49 (0)30 1208 434 75}
  \newcommand{\email}{caroline.moeller@rl-institut.de}
  \newcommand{\finalstatement}{Enjoy stating a final statement ;-)}
  \tikzset{
  invisible/.style={opacity=0},
  visible on/.style={alt={#1{}{invisible}}},
  alt/.code args={<#1>#2#3}{%
    \alt<#1>{\pgfkeysalso{#2}}{\pgfkeysalso{#3}} % \pgfkeysalso doesn't change the path
  },
  }
  \usepackage{blindtext}
---

# The oemof.thermal package

- Contains components to model thermal energy systems
  - Compression heat pump and chiller
  - Stratified thermal storage
  - Solar thermal collector
  - Concentrating solar power

- To be released soon: absorption heat pump
- To be released in an extra repository: district heating network

BILD
Beschriftung anpassen: oemof.thermal


# How to install the oemof.thermal package

pip install ....


# How to use the components

two methods:
- precalculation
- facade

# Compression heat pump and chillers





# Stratified thermal storage

# Solar thermal collector

# Concentrating solar power
