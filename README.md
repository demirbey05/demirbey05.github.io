# demirbey05.github.io

Personal academic blog built with [Hugo](https://gohugo.io/) and the [PaperMod](https://github.com/adityatelange/hugo-PaperMod) theme, deployed via GitHub Pages.

## Local Development

```bash
# Install Hugo (macOS)
brew install hugo

# Clone with submodules
git clone --recurse-submodules https://github.com/demirbey05/demirbey05.github.io.git
cd demirbey05.github.io

# Start dev server
hugo server -D
```

Open [http://localhost:1313](http://localhost:1313) in your browser.

## Writing a New Post

```bash
hugo new content posts/my-new-post.md
```

Edit the generated file in `content/posts/`, set `draft: false` when ready to publish.

### Math Support

LaTeX math is supported via KaTeX. Use `$...$` for inline math and `$$...$$` for display math. Make sure to add `math: true` in the post front matter.

## Deployment

Deployment is fully automated via GitHub Actions. Every push to `main` triggers a build and deploy to GitHub Pages.

## Structure

```
├── content/
│   ├── about.md              # About page
│   ├── posts/                # Blog posts
│   ├── publications/         # Publications list
│   ├── projects/             # Project showcases
│   └── search.md             # Search page
├── assets/css/extended/      # Custom CSS
├── layouts/partials/         # Custom partials (KaTeX)
├── .github/workflows/        # CI/CD
└── hugo.toml                 # Site configuration
```

## License

Content ©  Demirbey. Theme: [PaperMod](https://github.com/adityatelange/hugo-PaperMod) (MIT).