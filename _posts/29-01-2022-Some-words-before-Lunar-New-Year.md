---
layout: post
title: Some words before Lunar New Year
categories: research
---
Back in late 2021, the World started talking about a very serious vulnerability named Log4Shell that leads to RCE, I remember the day surfing Twitter and saw a very nice tweet:

> After this can we all just stop using Java? - @samwcyo

Log4Shell is basically a JNDI injection vulnerability in Log4j - an extremely popular logging library in Java. I wanted to better understand the JNDI injection vulnerability, as well as the techniques for exploiting it, so I decided to write a summary.

The summary is intended to be divided into 3 parts:

- First part describes the JNDI injection vulnerability, providing a base for understanding the notorious Log4Shell.
- Second part talks about techniques to exploit JNDI injection in old JDK with Log4Shell as guinea pig.
- Last part provides new exploitation techniques in newer JDK, experiments with Log4Shell.
