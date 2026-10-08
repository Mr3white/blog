# blog

个人博客源码，部署在 <https://blog.weiyangli.space>。
技术栈：[Hugo](https://gohugo.io/) + [PaperMod](https://github.com/adityatelange/hugo-PaperMod)，GitHub Actions 自动部署到 GitHub Pages。

学术主页是另一个仓库：[Mr3white.github.io](https://github.com/Mr3white/Mr3white.github.io) → <https://weiyangli.space>。

## 本地预览

```bash
git clone --recurse-submodules https://github.com/Mr3white/blog.git
cd blog
hugo server -D          # 需要 Hugo extended ≥ 0.151，打开 http://localhost:1313
```

如果已经 clone 过但 `themes/PaperMod` 是空的：`git submodule update --init --recursive`。

## 写文章

```bash
hugo new content posts/some-slug.md
```

生成的文件在 `content/posts/`，front matter 字段：

| 字段 | 说明 |
| --- | --- |
| `title` / `date` | 标题、时间（带时区） |
| `draft` | `true` 时只在 `hugo server -D` 可见，发布前改成 `false` |
| `categories` | `tech` / `life` / `reading`，自己定 |
| `tags` | 标签列表 |
| `summary` | 列表页摘要，不写则自动截取 |
| `math` | `true` 时加载 KaTeX，支持 `$...$` 和 `$$...$$` |
| `showToc` | 是否显示目录 |

文章里的图片：和文章放在同一个目录（page bundle），即 `content/posts/some-slug/index.md` + 图片文件，Markdown 里直接 `![](photo.jpg)`。

## 发相册

```bash
hugo new content photos/2026-11-london/index.md
```

然后把照片丢进 `content/photos/2026-11-london/`：

- `cover.jpg` 会作为相册列表的封面；
- 其余 `jpg/jpeg/png/webp` 由 `{{< gallery >}}` 自动铺成网格，构建时生成 900px 缩略图和 2000px 大图；
- 想给某张图加说明，在 front matter 里写：

```yaml
resources:
  - src: "day1-01.jpg"
    params:
      caption: "阿尔伯特码头"
```

### 照片体积

GitHub 仓库建议控制在 1 GB 以内，原图入库前先压一下（长边 2500px、质量 85 已经足够网页用）：

```bash
# ImageMagick
mogrify -resize 2500x2500\> -quality 85 -strip *.jpg
```

照片多了以后可以把原图挪到 Cloudflare R2 / 图床，`gallery` shortcode 换成读外链即可。

## 部署

1. 仓库 **Settings → Pages → Build and deployment → Source** 选 **GitHub Actions**。
2. 推送到 `main` 即触发 `.github/workflows/hugo.yaml`，约 1 分钟后生效。
3. 自定义域名：`static/CNAME` 已写入 `blog.weiyangli.space`；在域名 DNS 里加一条
   `CNAME  blog  →  mr3white.github.io`，再到 Pages 设置里填同一域名并勾选 **Enforce HTTPS**。

## 目录结构

```
hugo.yaml                 站点配置（标题、菜单、主题参数、Markdown/高亮设置）
content/posts/            文章
content/photos/           相册，每个相册一个目录
content/about.md          关于页
content/archives.md       归档页  content/search.md  搜索页
layouts/shortcodes/gallery.html     相册网格
layouts/partials/extend_head.html   按需加载 KaTeX
assets/css/extended/custom.css      自定义样式（中文排版、相册网格）
static/                   原样复制到站点根目录（CNAME、favicon、images/og-cover.jpg）
themes/PaperMod           主题（git submodule）
.github/workflows/hugo.yaml         自动部署
```

## 待补

- [ ] `static/favicon.ico`、`favicon-16x16.png`、`favicon-32x32.png`、`apple-touch-icon.png`
- [ ] `static/images/og-cover.jpg`：分享到微信 / Twitter 时的默认配图
- [ ] 评论系统（可选，PaperMod 支持 giscus，用 GitHub Discussions 存评论）
