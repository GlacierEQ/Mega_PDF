# 🎯 LaTeX & Document Processing Toolkit Setup Guide

## For macOS + Overleaf Integration

---

## 📦 ESSENTIAL INSTALLATIONS

### 1. MacTeX (Full LaTeX Distribution)
```bash
# Option A: Full MacTeX (~4GB)
brew install --cask mactex

# Option B: BasicTeX (~100MB) + packages as needed
brew install --cask basictex
sudo tlmgr install latexmk xetex luatex geometry xcolor tikz

# Verify
which xelatex pdflatex lualatex
```

### 2. LaTeX Workshop VS Code Extension
```
Name: LaTeX Workshop
ID: James-Yu.latex-workshop
Features:
  - Live PDF preview
  - Auto-compilation
  - Forward/inverse search
  - Snippets
  - Linting
```

### 3. Tectonic (Modern LaTeX Engine)
```bash
# Fast, self-contained, no huge install
brew install tectonic

# Usage: tectonic file.tex
# Automatically downloads packages
```

### 4. Pandoc (Document Conversion King)
```bash
brew install pandoc

# Markdown → LaTeX
pandoc input.md -o output.tex

# LaTeX → PDF
pandoc input.tex -o output.pdf

# Word → LaTeX
pandoc document.docx -o output.tex --wrap=none
```

---

## 🔌 WINDSURF EXTENSIONS FOR LaTeX

### Must-Have Extensions:

| Extension | ID | Purpose |
|-----------|-----|---------|
| **LaTeX Workshop** | `James-Yu.latex-workshop` | Full LaTeX IDE experience |
| **LaTeX Utilities** | `tecosaur.latex-utilities` | Word count, citation helpers |
| **Pandoc Markdown** | `DougFinke.vscode-pandoc` | Quick markdown conversion |
| **Markdown PDF** | `yzane.markdown-pdf` | Export to PDF |
| **SVG Preview** | `jock.svg` | For TikZ figures |
| **Table Formatter** | `shuworks.vscode-table-formatter` | LaTeX tables |

### Install Commands:
```bash
# VS Code CLI installation
code --install-extension James-Yu.latex-workshop
code --install-extension tecosaur.latex-utilities
code --install-extension DougFinke.vscode-pandoc
code --install-extension yzane.markdown-pdf
```

---

## 🌐 OVERLEAF INTEGRATION WORKFLOWS

### Option 1: Overleaf Git Integration
```bash
# Connect local repo to Overleaf
# 1. Create project on Overleaf
# 2. Get git URL from Overleaf menu → Git
# 3. Clone locally
git clone https://git.overleaf.com/YOUR_PROJECT_ID

# 4. Work locally, push to Overleaf
git add .
git commit -m "updates"
git push origin master

# 5. Compile on Overleaf for final PDF
```

### Option 2: Local Compilation + Overleaf Backup
```bash
# Compile locally with Tectonic
tectonic main.tex

# Sync to Overleaf via their API
# Or manually upload when needed
```

### Option 3: VS Code + Overleaf Extension
```bash
# Install Overleaf Workshop extension
code --install-extension github.copilot  # For AI help with LaTeX

# Use with Overleaf sync
```

---

## 🛠️ QUICK TOOLCHAIN SETUP

### Install Everything Script
```bash
#!/bin/bash
# save as: install_latex_toolkit.sh

echo "🎯 Installing LaTeX Toolkit..."

# 1. Install Tectonic (fast, modern)
brew install tectonic

# 2. Install Pandoc
brew install pandoc

# 3. Install LaTeX tools for images
brew install imagemagick ghostscript

# 4. Python LaTeX tools
pip3 install pylatexenc latex2mathml

# 5. Node tools for markdown
npm install -g @marp-team/marp-cli

echo "✅ Toolkit installed!"
echo "Quick compile: tectonic file.tex"
echo "Markdown→PDF: marp file.md --pdf"
echo "Docx→LaTeX: pandoc file.docx -o file.tex"
```

---

## 📄 AEGIS REFERENCE SHEET (Ready to Compile)

Created at:
`~/ANTIGRAVITY-STACK/aegis-portal/aegis_reference.tex`

### Compile Options:

**Option A: Tectonic (Recommended)**
```bash
cd ~/ANTIGRAVITY-STACK/aegis-portal
tectonic aegis_reference.tex
# Output: aegis_reference.pdf
```

**Option B: LaTeX Workshop (VS Code)**
```bash
# Open in VS Code
code ~/ANTIGRAVITY-STACK/aegis-portal/aegis_reference.tex

# Use Ctrl+Alt+B to build
# PDF preview opens automatically
```

**Option C: Pandoc (Markdown fallback)**
```bash
# If LaTeX fails, convert to HTML first
pandoc aegis_reference.tex -o aegis_reference.html --mathjax

# Then print to PDF from browser
```

---

## 🎨 DOCUMENT PROCESSING PIPELINE

### For Your API Documentation:

```bash
# Markdown → LaTeX → PDF
pandoc API_DOCUMENTATION.md -o api_doc.tex --template=default.latex
tectonic api_doc.tex

# Or directly to PDF
pandoc API_DOCUMENTATION.md -o api_doc.pdf \
  --pdf-engine=xelatex \
  --variable geometry:margin=1in
```

### With Citations/Bibliography:
```bash
pandoc doc.md -o doc.pdf --citeproc --bibliography=refs.bib
```

---

## 🚀 QUICK COMMANDS CHEAT SHEET

| Task | Command |
|------|---------|
| Compile LaTeX | `tectonic file.tex` |
| Watch & rebuild | `latexmk -pvc -pdf file.tex` |
| MD → PDF | `pandoc file.md -o file.pdf` |
| DOCX → LaTeX | `pandoc file.docx -o file.tex` |
| Count words | `texcount file.tex` |
| Compress PDF | `gs -sDEVICE=pdfwrite -dCompatibilityLevel=1.4 -dPDFSETTINGS=/ebook -dNOPAUSE -dQUIET -dBATCH -sOutputFile=output.pdf input.pdf` |

---

## 📚 RESOURCES

### LaTeX Templates for Quick Starts:
- **Invoice**: `~/Library/Mobile Documents/iCloud~com~mkApps~LatexEditor/Documents/Invoice Second Try .tex`
- **Aegis Reference**: `~/ANTIGRAVITY-STACK/aegis-portal/aegis_reference.tex`

### Overleaf Integration:
- Git URL: Get from Overleaf → Menu → Git
- Sync: `git push` triggers Overleaf compile
- Backup: Overleaf keeps 50 versions automatically

### Helpful Tools:
- **Mathpix**: Screenshot equations → LaTeX
- **TableGenerator.com**: Excel → LaTeX tables
- **Detexify**: Draw symbol → LaTeX command

---

## ⚡ ONE-LINE INSTALL

```bash
# Run this to install everything
brew install tectonic pandoc imagemagick ghostscript && pip3 install pylatexenc && echo 'alias compile="tectonic"' >> ~/.zshrc
```

Then compile the Aegis sheet:
```bash
tectonic ~/ANTIGRAVITY-STACK/aegis-portal/aegis_reference.tex
open ~/ANTIGRAVITY-STACK/aegis-portal/aegis_reference.pdf
```

---

## 🔧 TROUBLESHOOTING

### "xelatex not found"
→ Install MacTeX: `brew install --cask mactex`

### "Package not found"
→ Use tectonic instead (auto-downloads packages)

### "Font not found"
→ Use lualatex or xelatex with system fonts

### Overleaf sync conflicts
→ Use `git pull` before `git push`

---

**Ready to compile! Run:**
```bash
tectonic ~/ANTIGRAVITY-STACK/aegis-portal/aegis_reference.tex
```
