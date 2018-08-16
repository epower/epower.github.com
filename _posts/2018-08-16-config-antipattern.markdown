---
title: config antipattern
layout: post
---

I spotted the [Five Stages of YAML](https://brokenco.de/2018/08/15/five-stages-of-yaml.html) and wondered if it indicated an anti-pattern after stage 2. 

Perhaps something more like:

1. Configuration languages are too complex; YAML is much simpler and easier to understand.
2. Declarative YAML configuration is brilliant.
3. Lots of our things look similar, we have too much copy and pasted YAML. 
4. Perhaps its time to update the tool parsing the YAML to operate at higher levels of abstraction keeping the required YAML simple and to the point.

I've definitly felt this happening to me whem making tools with a configuration option in the past.
