---
title: "{{ replace .File.ContentBaseName "-" " " | title }}"
date: {{ .Date }}
draft: true
location: ""
cover:
  image: "cover.jpg"      # 放在本目录下，列表页用作封面
  relative: true
  hiddenInSingle: true
---

一句话介绍这组照片。

{{</* gallery */>}}
