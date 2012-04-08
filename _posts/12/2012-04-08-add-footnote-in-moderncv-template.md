---
layout: post
title: "Add footnote in ModernCV template"
description: "Add footnote in latex"
category: latex
tags: [latex]
---
{% include JB/setup %}

Today, I was updating my CV. The CV is writtern in Latex, using ModernCV
template. For some reason, I need to use footnote. However, it seems
`\footnote` does not work properly in the template.

My solution is to add `\usepackage{footmisc}` under the first line of the tex
file. Then add `\footnotemark[num]` whereever you like. Put `\footnotetext[num]{some
text}` in the outer level of your source file. With `[num]`, we can have same
marks in different places which fits my need pretty well.
