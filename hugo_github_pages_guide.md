# 🌐 Complete Guide: Building an AI Research Website Like Yewentao's

> **Your goal**: Understand how Yewentao built [wentao.site](https://wentao.site) and create your own research showcase website using the same approach.

---

## Table of Contents

1. [What Are Static Pages?](#1-what-are-static-pages)
2. [What Is Hugo?](#2-what-is-hugo)
3. [What Are GitHub Websites (GitHub Pages)?](#3-what-are-github-websites-github-pages)
4. [How Yewentao's Website Works (The Big Picture)](#4-how-yewentaos-website-works-the-big-picture)
5. [What Does "Indexing Static Files" Mean?](#5-what-does-indexing-static-files-mean)
6. [What Are Hugo Themes?](#6-what-are-hugo-themes)
7. [How Everything Fits Together](#7-how-everything-fits-together)
8. [Step-by-Step: Build Your Own AI Research Website](#8-step-by-step-build-your-own-ai-research-website)
9. [Writing Your First Blog Post](#9-writing-your-first-blog-post)
10. [Advanced: Custom Domain Setup](#10-advanced-custom-domain-setup)
11. [What to Showcase as an AI Researcher](#11-what-to-showcase-as-an-ai-researcher)

---

## 1. What Are Static Pages?

### The Simple Analogy

Think of two kinds of restaurants:

| | **Dynamic Website** (e.g., WordPress) | **Static Website** (e.g., Hugo) |
|---|---|---|
| **Analogy** | A restaurant that cooks each dish **when you order** | A bakery that bakes everything **in advance** and just hands it to you |
| **How it works** | Every time someone visits, the server **runs code** to build the page from a database | All pages are **pre-built** as plain HTML files and just served directly |
| **Needs** | A database (MySQL), a backend language (PHP/Python), a running server | Just a folder of HTML/CSS/JS files — any file server works |
| **Speed** | Slower (must compute each page) | **Extremely fast** (just sends a ready-made file) |
| **Security** | Vulnerable (database injection, server exploits) | **Very secure** (no database, no backend code to exploit) |
| **Cost** | Usually paid hosting | **Free** (GitHub Pages, Netlify, etc.) |

### What "Static" Actually Means

**Static** = the content of the page **does not change based on who is viewing it or when**. The HTML file served to every visitor is identical. It was generated once, ahead of time.

This does NOT mean the page can't have:
- ✅ Animations, transitions, hover effects (these are client-side CSS/JS)
- ✅ Dark mode toggle
- ✅ Search functionality
- ✅ Comments (via third-party services like Disqus or Utterances)
- ✅ Beautiful, modern designs

It just means there's **no server-side computation** happening when someone visits your page.

### Why This Matters for Researchers

As a researcher, you want:
1. **Zero maintenance** — no server to manage, no database to update, no PHP patches
2. **Speed** — your papers and blog posts load instantly
3. **Free hosting** — GitHub Pages gives you unlimited free hosting
4. **Version control** — your entire website is a Git repository, so you have full history of every change
5. **Focus on writing** — you write in Markdown (simple text), not HTML

---

## 2. What Is Hugo?

### The One-Line Answer

**Hugo is a program that converts your Markdown text files into a complete, beautiful website.**

### The Detailed Explanation

Hugo is a **Static Site Generator (SSG)** — a tool that takes:

```
📝 Your content (Markdown files)
  +
🎨 A theme (design templates)
  +
⚙️ Configuration (your settings)
  ═══════════════════════════════
  ↓
🌐 A complete website (folder of HTML/CSS/JS files)
```

### How Hugo Works (Step by Step)

```mermaid
graph LR
    A["📝 You write in Markdown<br/>(simple text files)"] --> B["⚙️ Hugo processes<br/>your files"]
    B --> C["🌐 Output: public/ folder<br/>(complete website)"]
    C --> D["🚀 Upload to<br/>GitHub Pages"]
    D --> E["🎉 Live at<br/>yourname.github.io"]
```

1. **You write content** in Markdown — a simple text format:
   ```markdown
   # My Paper Summary
   
   This paper proposes a new **attention mechanism** that...
   
   ![architecture diagram](resources/architecture.png)
   ```

2. **Hugo reads your Markdown** and wraps it in beautiful HTML templates (from your chosen theme)

3. **Hugo outputs a `public/` folder** containing the finished website — plain HTML, CSS, JS files

4. **You upload this folder** to GitHub Pages → your site is live!

### Why Hugo Specifically?

There are many static site generators (Jekyll, Gatsby, Next.js, etc.), but Hugo is popular because:

| Feature | Hugo |
|---------|------|
| **Speed** | Builds thousands of pages in < 1 second (written in Go) |
| **No dependencies** | Single binary, no Node.js/Ruby/Python required |
| **Themes** | Hundreds of beautiful themes available |
| **Multilingual** | Built-in support (Yewentao uses English + Chinese!) |
| **Learning curve** | Low — write Markdown, tweak config, done |

---

## 3. What Are GitHub Websites (GitHub Pages)?

### The Simple Explanation

**GitHub Pages** is a **free web hosting service** provided by GitHub. You push HTML files to a special repository, and GitHub automatically serves them as a website.

### How It Works

```mermaid
graph TD
    A["Your computer:<br/>Hugo generates website"] --> B["git push to<br/>username.github.io repo"]
    B --> C["GitHub detects the push"]
    C --> D["GitHub serves the files<br/>as a website"]
    D --> E["Anyone can visit<br/>https://username.github.io"]
```

### The Magic Repository Name

The key is the **repository name**. If your GitHub username is `navin-research`, you create a repository called:

```
navin-research.github.io
```

GitHub automatically recognizes this naming pattern and serves whatever HTML files are in that repo as a website at `https://navin-research.github.io`.

### What You Get for Free

- ✅ **Free hosting** — no server costs, ever
- ✅ **HTTPS** — secure connection, automatically
- ✅ **Custom domain** — you can point `yourname.site` to it (like Yewentao uses `wentao.site`)
- ✅ **GitHub Actions** — automated builds (push Markdown → website updates automatically)
- ✅ **Global CDN** — fast loading worldwide

---

## 4. How Yewentao's Website Works (The Big Picture)

Let's trace exactly how Yewentao's website works, piece by piece:

### His Setup

| Component | What He Uses |
|-----------|-------------|
| **Static Site Generator** | Hugo |
| **Theme** | LoveIt → DoIt (the maintained successor) |
| **Hosting** | GitHub Pages |
| **Repository** | [yewentao256/yewentao256.github.io](https://github.com/yewentao256/yewentao256.github.io) |
| **Custom Domain** | wentao.site (optional — without it, it would be yewentao256.github.io) |
| **Deployment** | GitHub Actions (automatic) |

### His Repository Structure

```
yewentao256.github.io/
├── .github/workflows/    ← GitHub Actions: auto-builds & deploys when he pushes
├── archetypes/           ← Templates for new blog posts
├── config.toml           ← Hugo configuration (site title, author, menu, etc.)
├── content/
│   └── posts/            ← ALL his blog posts (Markdown files)
│       ├── pytorch/
│       │   └── deep_dive_to_autograd_2/
│       │       ├── index.en.md        ← English version of the post
│       │       ├── index.zh-cn.md     ← Chinese version of the post
│       │       └── resources/         ← Images for this post
│       │           └── graph.png
│       ├── nccl_summary/
│       └── ...
├── static/               ← Global static files (images, PDFs shared across posts)
│   └── csapp/
│       └── resources/
│           ├── ROP-attack.png
│           └── io-redirection.png
└── themes/               ← The Hugo theme (LoveIt/DoIt)
    └── DoIt/
```

### His Workflow (What He Does Day-to-Day)

```mermaid
graph TD
    A["1. Write a Markdown post<br/>in content/posts/"] --> B["2. Preview locally<br/>hugo server -e production"]
    B --> C["3. Looks good?<br/>git add, commit, push"]
    C --> D["4. GitHub Actions<br/>auto-builds the site"]
    D --> E["5. Website updated at<br/>wentao.site"]
```

### His Blog Content (What He Showcases)

Looking at his live site, he writes about:
- 📄 **Paper summaries** (NCCL, AWQ, PyTorch, SGLang, SARATHI, S4, MARLIN)
- 🔧 **Deep technical dives** (PyTorch autograd internals, CUDA)
- 📊 **Contributions** (vLLM bi-weekly journal)
- 🎤 **Presentations** (Batch Invariance in vLLM)

He organizes them into **categories** like `Paper_summary`, `Pytorch`, `Vllm`, `Presentation`.

---

## 5. What Does "Indexing Static Files" Mean?

> This is the FAQ you saw in Yewentao's README screenshot!

### What "Static Files" Means Here

In Hugo, **"static files"** = any file that is NOT a Markdown blog post. These are:
- 📸 Images (PNG, JPG, GIF, SVG)
- 📄 PDFs (your papers)
- 📊 Diagrams, charts
- 🎥 Videos
- Any other non-text asset

### What "Indexing" Means

**"Indexing"** here simply means **"referencing" or "linking to"** these files from within your Markdown blog posts. When you write a blog post and want to show an image, you need to tell Hugo **where to find that image file**. That's "indexing" it.

### The Two Methods Yewentao Describes

#### Method 1: Put Files Next to the Post (Relative Path) ✅ RECOMMENDED

Place images inside the same folder as your blog post:

```
content/posts/pytorch/deep_dive_to_autograd_2/
├── index.en.md          ← Your blog post
├── index.zh-cn.md       ← Chinese version
└── resources/           ← Images for THIS post only
    └── graph.png
```

Then reference it in your Markdown with a **relative path**:

```markdown
![architecture diagram](resources/graph.png)
```

> [!TIP]
> **Why this is better**: The image travels with the post. If you move or rename the post, the image goes with it. Everything stays organized.

#### Method 2: Put Files in the Global `static/` Folder (Absolute Path)

Place images in the top-level `static/` directory:

```
static/
└── csapp/
    └── resources/
        ├── ROP-attack.png
        └── io-redirection.png
```

Then reference it from **any** blog post with an **absolute path** (starting with `/`):

```markdown
![ROP attack](/csapp/resources/ROP-attack.png)
```

> [!NOTE]
> **When to use this**: For images shared across multiple posts, or for site-wide assets like your profile photo or logo.

### Summary

| Method | Where files go | How to reference | Best for |
|--------|---------------|-----------------|----------|
| **Method 1** (Relative) | Next to the post in `content/posts/...` | `![img](resources/file.png)` | Per-post images |
| **Method 2** (Absolute) | In top-level `static/` folder | `![img](/path/to/file.png)` | Shared/global images |

---

## 6. What Are Hugo Themes?

### The Simple Explanation

A **theme** is a pre-designed look-and-feel for your website. It defines:
- Layout (where the title, sidebar, content, footer go)
- Colors, fonts, spacing
- Features (search, dark mode, table of contents, code highlighting)
- Responsive design (mobile-friendly)

**You don't need to write any HTML or CSS**. You just pick a theme, and Hugo applies it to your Markdown content.

### Yewentao's Theme: LoveIt → DoIt

Yewentao uses the **LoveIt** theme (which was later forked and maintained as **DoIt**):

| Theme | URL | Status |
|-------|-----|--------|
| **LoveIt** | [github.com/dillonzq/LoveIt](https://github.com/dillonzq/LoveIt) | Original, now unmaintained |
| **DoIt** | [github.com/HEIGE-PCloud/DoIt](https://github.com/HEIGE-PCloud/DoIt) | Active fork, currently maintained |

Features of this theme:
- 🌓 Dark/light mode toggle
- 🔍 Full-text search
- 📋 Table of contents (auto-generated from headings)
- 🖥️ Code syntax highlighting with copy button
- 📊 Math equation support (LaTeX) — critical for AI research!
- 🌐 Multilingual support (English + Chinese, etc.)
- 💬 Comments integration
- 📱 Fully responsive (mobile-friendly)

### Other Great Themes for AI Researchers

| Theme | Style | URL |
|-------|-------|-----|
| **PaperMod** | Clean, minimal, fast | [github.com/adityatelange/hugo-PaperMod](https://github.com/adityatelange/hugo-PaperMod) |
| **Academic (Wowchemy)** | Academic portfolio + publications | [github.com/wowchemy/wowchemy-hugo-themes](https://github.com/wowchemy/wowchemy-hugo-themes) |
| **Stack** | Card-based, modern | [github.com/CaiJimmy/hugo-theme-stack](https://github.com/CaiJimmy/hugo-theme-stack) |
| **Blowfish** | Modern, animations | [github.com/nunocoracao/blowfish](https://github.com/nunocoracao/blowfish) |

---

## 7. How Everything Fits Together

Here's the complete picture of how Hugo + Themes + GitHub Pages work together:

```mermaid
graph TB
    subgraph "Your Computer"
        A["📝 Markdown files<br/>(your blog posts)"]
        B["🎨 Theme<br/>(DoIt/PaperMod/etc.)"]
        C["⚙️ config.toml<br/>(your settings)"]
        D["📸 Images/PDFs<br/>(static files)"]
        A --> E["🔧 Hugo Build<br/>(hugo command)"]
        B --> E
        C --> E
        D --> E
        E --> F["📁 public/ folder<br/>(complete website)"]
    end
    
    subgraph "GitHub"
        F --> G["git push →<br/>username.github.io repo"]
        G --> H["GitHub Actions<br/>(auto-build)"]
        H --> I["GitHub Pages<br/>(hosting)"]
    end
    
    subgraph "The Internet"
        I --> J["🌐 https://username.github.io<br/>or https://yourname.site"]
    end
```

### The Workflow in Plain English

1. **You write** a blog post in Markdown (just text with simple formatting)
2. **Hugo converts** your Markdown into beautiful HTML using your chosen theme
3. **You push** the code to your GitHub repository
4. **GitHub Actions** automatically runs Hugo and deploys the output
5. **GitHub Pages** serves the HTML to anyone who visits your URL
6. **(Optional)** You point a custom domain (like `yourname.site`) to GitHub Pages

---

## 8. Step-by-Step: Build Your Own AI Research Website

> [!NOTE]
> There are two ways to do this:
> - **Method A: From Scratch** (the original way — how Yewentao built his) ← **RECOMMENDED**
> - **Method B: Fork someone's repo** (shortcut — skip to the end of this section)
> 
> We'll go with Method A — building from scratch. This is how real developers do it.

### Prerequisites

You need:
- A **GitHub account** (free at github.com)
- **Git** installed on your computer (you likely already have this)
- **Hugo** installed on your computer

### Step 1: Install Hugo

```bash
# On Ubuntu/Debian (your system)
sudo apt install hugo

# Or, for the latest version (recommended):
sudo snap install hugo

# Verify installation
hugo version
```

> [!IMPORTANT]
> Make sure you have Hugo **extended** version (needed for SCSS/SASS support that many themes use). Check with `hugo version` — it should say "extended".

If snap doesn't give you extended version:
```bash
# Download the latest extended version from GitHub releases:
# https://github.com/gohugoio/hugo/releases
# Look for: hugo_extended_X.XXX.X_linux-amd64.deb
wget https://github.com/gohugoio/hugo/releases/download/v0.140.0/hugo_extended_0.140.0_linux-amd64.deb
sudo dpkg -i hugo_extended_0.140.0_linux-amd64.deb
```

### Step 2: Create a New Hugo Site FROM SCRATCH

```bash
# Create a brand new Hugo site (this is what Yewentao did originally)
hugo new site my-research-blog
cd my-research-blog
```

This creates a **clean, empty Hugo project** with this structure:

```
my-research-blog/
├── archetypes/         ← Templates for new posts
│   └── default.md      ← Default template (auto-created)
├── assets/             ← SCSS/CSS assets
├── content/            ← Your blog posts go here (EMPTY for now)
├── data/               ← Data files
├── i18n/               ← Translation files
├── layouts/            ← Custom layout overrides
├── static/             ← Static files (images, PDFs, etc.)
├── themes/             ← Themes go here (EMPTY for now)
└── hugo.toml           ← Main configuration file
```

**This is YOUR site. Fresh. Clean. No one else's content.**

### Step 3: Initialize Git

```bash
# Initialize a git repository
git init
```

### Step 4: Choose and Install a Theme

This is where you pick the look-and-feel of your site. You have options:

#### Option A: Use the DoIt Theme (same as Yewentao's — recommended)

```bash
# Add the DoIt theme as a git submodule
git submodule add https://github.com/HEIGE-PCloud/DoIt.git themes/DoIt
```

#### Option B: Use PaperMod (cleaner, very popular)

```bash
git submodule add https://github.com/adityatelange/hugo-PaperMod.git themes/PaperMod
```

#### Option C: Use Stack (card-based, modern)

```bash
git submodule add https://github.com/CaiJimmy/hugo-theme-stack.git themes/hugo-theme-stack
```

> [!TIP]
> **Why `git submodule`?** A submodule links to the theme's repository without copying all its code into yours. When the theme author updates their theme, you can pull the updates with `git submodule update --remote`.

### Step 5: Configure Your Site

Edit `hugo.toml` (or rename it to `config.toml` — both work) with your personal info.

**If you chose DoIt theme (like Yewentao):**

```toml
baseURL = "https://YOUR-USERNAME.github.io/"
title = "Your Name's Research Blog"
theme = "DoIt"
defaultContentLanguage = "en"

[params]
  version = "0.4.X"
  description = "AI Research Blog - Neural Networks, CUDA, Deep Learning"

  [params.home]
    [params.home.profile]
      enable = true
      title = "Your Name"
      subtitle = "AI Researcher | Neural Networks | CUDA"
      avatarURL = "/images/avatar.png"
      social = true

  [params.social]
    GitHub = "your-github-username"
    Email = "your-email@example.com"
    LinkedIn = "your-linkedin-id"

  # Enable math (LaTeX) — essential for research blogs!
  [params.page]
    [params.page.math]
      enable = true

[menu]
  [[menu.main]]
    identifier = "posts"
    name = "Posts"
    url = "/posts/"
    weight = 1
  [[menu.main]]
    identifier = "categories"
    name = "Categories"
    url = "/categories/"
    weight = 2
  [[menu.main]]
    identifier = "about"
    name = "About"
    url = "/about/"
    weight = 3

[markup]
  [markup.highlight]
    codeFences = true
    lineNos = true
    style = "monokai"
  [markup.goldmark]
    [markup.goldmark.renderer]
      unsafe = true   # Allows raw HTML in markdown
```

**If you chose PaperMod theme:**

```toml
baseURL = "https://YOUR-USERNAME.github.io/"
title = "Your Name's Research Blog"
theme = "PaperMod"

[params]
  ShowReadingTime = true
  ShowShareButtons = true
  ShowPostNavLinks = true
  ShowBreadCrumbs = true
  ShowCodeCopyButtons = true
  math = true

  [params.homeInfoParams]
    Title = "Your Name"
    Content = "AI Researcher | Neural Networks | CUDA | Deep Learning"

  [[params.socialIcons]]
    name = "github"
    url = "https://github.com/your-username"
  [[params.socialIcons]]
    name = "email"
    url = "mailto:your-email@example.com"

[menu]
  [[menu.main]]
    identifier = "posts"
    name = "Posts"
    url = "/posts/"
    weight = 1
  [[menu.main]]
    identifier = "about"
    name = "About"
    url = "/about/"
    weight = 2
```

### Step 6: Add Your Profile Photo

```bash
# Create the images directory
mkdir -p static/images

# Copy your photo there (replace with your actual photo path)
cp /path/to/your/photo.png static/images/avatar.png
```

### Step 7: Create Your First Blog Post

```bash
# Create a new post using Hugo's command
hugo new posts/my-first-research-post/index.md
```

This creates `content/posts/my-first-research-post/index.md`. Open it and write:

```markdown
---
title: "My First Research Post"
date: 2026-04-27
draft: false
description: "An introduction to my research work"
categories: ["Research"]
tags: ["neural-networks", "CUDA"]
math: true
---

# My Research on Custom Neural Network Frameworks

In this post, I'll walk through my work on building a custom
neural network framework from scratch with CUDA kernels...

## Architecture Overview

![architecture](resources/architecture.png)

## Key Results

| Model | Accuracy | Training Time |
|-------|----------|---------------|
| GPT-2 | 94.2% | 3.2 hours |

## The Math

The attention mechanism computes:

$$
\text{Attention}(Q, K, V) = \text{softmax}\left(\frac{QK^T}{\sqrt{d_k}}\right)V
$$

## Code Snippet

```cuda
__global__ void attention_forward_kernel(...) {
    // Your CUDA kernel code
}
```
```

> [!TIP]
> **Adding images**: Create a `resources/` folder next to your post and put images there:
> ```
> content/posts/my-first-research-post/
> ├── index.md
> └── resources/
>     └── architecture.png
> ```

### Step 8: Create an About Page

```bash
hugo new posts/about/index.md
```

Edit `content/posts/about/index.md`:

```markdown
---
title: "About Me"
date: 2026-04-27
draft: false
---

Hello! Welcome to my blog!

## Contact
- Email: your-email@example.com
- GitHub: [your-username](https://github.com/your-username)
- LinkedIn: [Your Name](https://linkedin.com/in/your-id)

## Education
- Your degree, your university

## Research Interests
- Neural Networks, CUDA Programming, Deep Learning Systems

## Projects
- Custom Neural Network Framework in C++/CUDA
- ...
```

### Step 9: Preview Locally

```bash
# Start Hugo's built-in development server
hugo server -e production

# Open in browser: http://localhost:1313
```

You'll see your website live with **hot-reload** — every time you save a file, the browser updates instantly!

> [!NOTE]
> If you see no CSS/styling, make sure the `theme = "DoIt"` (or whichever theme name) in your `hugo.toml` exactly matches the folder name inside `themes/`.

### Step 10: Create Your GitHub Repository and Push

```bash
# Go to github.com/new and create a repo named: YOUR-USERNAME.github.io
# Then connect your local project to it:

git add .
git commit -m "Initial site: Hugo + DoIt theme from scratch"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/YOUR-USERNAME.github.io.git
git push -u origin main
```

### Step 11: Set Up GitHub Actions for Auto-Deploy

1. Go to your repo on GitHub → **Settings** → **Pages**
2. Under **Source**, select **GitHub Actions**
3. Create the file `.github/workflows/hugo.yml`:

```bash
mkdir -p .github/workflows
```

Then create `.github/workflows/hugo.yml` with this content:

```yaml
name: Deploy Hugo site to Pages

on:
  push:
    branches: ["main"]

permissions:
  contents: read
  pages: write
  id-token: write

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
        with:
          submodules: recursive
      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v3
        with:
          hugo-version: 'latest'
          extended: true
      - name: Build
        run: hugo --minify
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: ./public

  deploy:
    needs: build
    runs-on: ubuntu-latest
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```

```bash
git add .
git commit -m "Add GitHub Actions workflow for auto-deploy"
git push
```

### Step 12: Your Site Is Live! 🎉

Wait 1-2 minutes for GitHub Actions to build, then visit:
`https://YOUR-USERNAME.github.io`

**From now on, every time you write a new post and `git push`, your site updates automatically!**

---

### Alternative: Fork Method (Shortcut)

> If you want to skip the from-scratch setup, you can clone Yewentao's repo as a starting point. He explicitly invites this in his README ("welcome to fork and star").

```bash
# Clone Yewentao's repo
git clone https://github.com/yewentao256/yewentao256.github.io.git YOUR-USERNAME.github.io
cd YOUR-USERNAME.github.io

# Remove his git history
rm -rf .git

# Delete his content
rm -rf content/posts/*
rm -rf static/*

# Initialize as your own repo
git init
git remote add origin https://github.com/YOUR-USERNAME/YOUR-USERNAME.github.io.git

# Edit config.toml with your info, then push
git add .
git commit -m "My blog, based on Yewentao's template"
git branch -M main
git push -u origin main
```

> [!WARNING]
> The fork method gives you a working site faster, but you won't understand the structure as well. The from-scratch method teaches you what every file does.

---

## 9. Writing Your First Blog Post

### Markdown Quick Reference

Markdown is the language you write your posts in. Here's a cheat sheet:

```markdown
# Heading 1
## Heading 2
### Heading 3

**bold text**
*italic text*
`inline code`

- Bullet point 1
- Bullet point 2

1. Numbered item
2. Numbered item

[Link text](https://example.com)

![Image alt text](resources/image.png)

> Blockquote for highlighting important text

| Column 1 | Column 2 |
|-----------|----------|
| Data      | Data     |

```python
# Code block with syntax highlighting
def train(model, data):
    ...
```

$E = mc^2$   ← Inline math (LaTeX)

$$
\frac{\partial L}{\partial w} = \sum_{i} x_i \cdot \delta_i
$$            ← Block math (LaTeX)
```

### Blog Post Structure (Front Matter)

Every Hugo post starts with **front matter** — metadata between `---` marks:

```markdown
---
title: "Deep Dive into PyTorch Autograd"
date: 2026-04-27T10:00:00+05:30
draft: false                          # Set to false when ready to publish
author: "Your Name"
description: "An in-depth analysis of..."
categories: ["PyTorch", "Deep Learning"]
tags: ["autograd", "backpropagation", "computational-graph"]
math: true                            # Enable LaTeX math rendering
---

Your content starts here...
```

### Adding Images to Your Post

```
content/posts/my-cuda-kernels/
├── index.en.md
└── resources/
    ├── kernel_performance.png
    ├── architecture.svg
    └── results_table.png
```

In your Markdown:
```markdown
![Kernel Performance Benchmark](resources/kernel_performance.png)
```

---

## 10. Advanced: Custom Domain Setup

Like Yewentao has `wentao.site` instead of `yewentao256.github.io`:

### Step 1: Buy a Domain

Buy a domain from a registrar:
- **Namecheap** (~₹800/year for .site domains)
- **Google Domains** 
- **Cloudflare Registrar** (at-cost pricing, cheapest)
- **GoDaddy**

Good domain ideas for a researcher:
- `yourname.site`
- `yourname.dev`
- `yourname.io`
- `yourname-research.com`

### Step 2: Configure DNS

At your domain registrar, set up DNS records:

```
Type: CNAME
Name: www
Value: YOUR-USERNAME.github.io

Type: A
Name: @
Values: 
  185.199.108.153
  185.199.109.153
  185.199.110.153
  185.199.111.153
```

### Step 3: Tell GitHub About Your Domain

1. Go to your repo → **Settings** → **Pages**
2. Under **Custom domain**, enter your domain (e.g., `yourname.site`)
3. Check **Enforce HTTPS**

### Step 4: Update Hugo Config

```toml
baseURL = "https://yourname.site/"
```

---

## 11. What to Showcase as an AI Researcher

Looking at what Yewentao showcases, here's a tailored plan for you:

### Content Categories You Should Create

| Category | What to Write | Example Posts |
|----------|---------------|---------------|
| **Research** | Your own research work, experiments, results | "Building a Custom Neural Network Framework in C++/CUDA" |
| **Paper Summaries** | Summaries of important papers you've read | "Summary: Attention Is All You Need" |
| **Deep Dives** | Technical explanations of complex topics | "Deep Dive into CUDA Memory Hierarchy" |
| **Tutorials** | How-to guides for others | "How to Write Custom CUDA Kernels for Attention" |
| **Projects** | Showcasing your code projects | "My Custom Tensor Library: Design Decisions" |
| **Notes** | Learning notes on courses, books | "Notes on GPU Architecture for Deep Learning" |

### Your Specific Content (Based on Your Work)

From your open files, I can see you're working on:
- Custom neural network implementation in C++/CUDA
- Contiguous kernel implementations
- GPU-accelerated tensor operations
- Optimizer implementations (Adam, etc.)
- GPT-2 attention mechanisms

**Perfect blog post ideas for you:**

1. 🔥 **"Building a Neural Network Framework from Scratch in C++/CUDA"** — walkthrough of your framework
2. 🧮 **"Implementing Custom CUDA Kernels for Tensor Operations"** — your ContiguousKernel.cu work
3. ⚡ **"Optimizing GPU Memory: From Naive to Production-Grade Allocation"** — your tensor optimization work
4. 🧠 **"Implementing GPT-2 Attention in Raw CUDA"** — your gpt2_attn work
5. 📐 **"Understanding Tensor Contiguity: Why It Matters for Performance"** — your contiguity research

### Your Website Structure

```
About Page:
├── Your name, photo, university/affiliation
├── Research interests
├── Publications (with links to papers)
├── Contact: Email, GitHub, Google Scholar, LinkedIn

Blog Posts:
├── 📄 Paper Summaries (like Yewentao)
├── 🔧 Deep Technical Dives
├── 🧪 Experiment Results & Benchmarks
├── 📚 Tutorial & How-To Guides
└── 💡 Research Ideas & Notes
```

---

## Quick Reference: Essential Commands

```bash
# Create new post
hugo new posts/my-post-title/index.en.md

# Preview locally (with drafts)
hugo server -D

# Preview locally (production mode, like Yewentao does)
hugo server -e production

# Build the site (generates public/ folder)
hugo --minify

# Deploy (just push to GitHub, Actions handles the rest)
git add .
git commit -m "New post: my-post-title"
git push
```

---

## Summary: The Complete Picture

```
You write Markdown → Hugo converts to HTML → GitHub hosts it → World sees it

         📝                  🔧                  🚀               🌐
   (simple text)      (automated tool)     (free hosting)    (your website)
```

> [!TIP]
> **The fastest path to get started**: Fork Yewentao's repo, delete his content, update `config.toml` with your info, write your first post, push to GitHub. You'll have a live website in under 30 minutes!

> [!IMPORTANT]
> **Start writing now.** The website itself takes 30 minutes to set up. The real value is in the content. Your CUDA kernel work, your custom framework, your paper insights — that's what will impress people. The tool (Hugo) is just the delivery mechanism.
