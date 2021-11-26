---
layout: post
title: Replace a string in all filenames in a folder
description: 
summary: 
---

As below will replace S01 with S02 in all files in the dir that contain S01

```bash
for file in *S01*; do mv -v "$file" "${file/S01/S02}"; done
```