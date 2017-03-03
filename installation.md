---
layout: page
title: Installing PhysUtil
permalink: /installation/
---

# Installation

## VPython
Using PhysUtil as a Python module can helps users generate highly-visual VPython programs. Installation is very simple.

1. Download the [physutil.py](https://raw.githubusercontent.com/PERLMSU/physutil/master/python/physutil.py) script
2. Place the physutil.py script in the same folder as the VPython script you are writing.
3. Call physutil in your script using `import physutil`

It's that simple.

## Glowscript
Using PhysUtil as a Javasript library can help uses generate highly-visual Glowscript programs. Use is very simple.

1. In your Glowscript program include the following line:
```
get_library('https://raw.githubusercontent.com/PERLMSU/physutil/master/js/physutil.js')
```
