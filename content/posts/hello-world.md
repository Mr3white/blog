---
title: "博客搭好了"
date: 2026-10-08T10:00:00+08:00
draft: false
categories: ["life"]
tags: ["blog", "hugo"]
summary: "新博客的第一篇：这里打算写什么，以及它是怎么搭的。"
math: true
showToc: true
---

学术主页放在 [weiyangli.space](https://weiyangli.space)，只放论文和简历那类严肃内容。
平时想记点别的东西，所以单独开了这个博客。

## 打算写什么

- **技术笔记**：实验环境、复现论文时的坑、常用工具的配置。
- **随笔**：读书、访学生活、一些想法。
- **照片**：按主题整理成相册，见 [照片](/photos/)。

## 它是怎么搭的

静态站点生成器用 [Hugo](https://gohugo.io/)，主题是 [PaperMod](https://github.com/adityatelange/hugo-PaperMod)。
仓库推到 GitHub 后由 Actions 自动构建、部署到 GitHub Pages。

写一篇新文章只需要：

```bash
hugo new content posts/my-first-note.md   # 生成带 front matter 的文件
hugo server -D                             # 本地预览，含草稿
```

代码块支持高亮和一键复制。公式用 KaTeX，在 front matter 里写 `math: true` 就会加载：

行内公式 $\mathbf{y} = \mathbf{H}\mathbf{x} + \mathbf{n}$，块级公式：

$$
\mathrm{SNR}_{\text{dB}} = 10 \log_{10}\left(\frac{P_s}{P_n}\right)
$$

## 之后

先写起来，格式慢慢调。
