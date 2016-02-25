---
layout: post
title: Add footnote in ModernCV template
date: 2012-04-08 00:00:00.000000000 +02:00
published: true
categories:
- 杂七杂八
tags:
- latex
---
Today, I was updating my CV. The CV is writtern in Latex, using ModernCVtemplate. For some reason, I need to use footnote. However, it seems`\footnote` does not work properly in the template.

My solution is to add `\usepackage{footmisc}` under the first line of the texfile. Then add `\footnotemark[num]` whereever you like. Put `\footnotetext[num]{sometext}` in the outer level of your source file. With `[num]`, we can have samemarks in different places which fits my need pretty well.
