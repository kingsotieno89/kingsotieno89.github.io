```markdown
# kingsotieno89.github.io

My Professional IT Infrastructure & Cloud Portfolio.

This repository uses the Minimal Mistakes Jekyll theme via `remote_theme: "mmistakes/minimal-mistakes"`.

To run locally:
1. Install Ruby and Bundler (or use GitHub Codespaces).
2. Create a Gemfile with github-pages if you want a faithful local preview, or use `bundle` to install Jekyll and dependencies.
3. Run `bundle exec jekyll serve --livereload` to preview.

Note: For a root user site at https://kingsotieno89.github.io, ensure the repository name is `kingsotieno89.github.io`.
```
```name=Gemfile
source "https://rubygems.org"

gem "github-pages", group: :jekyll_plugins

# If you prefer to use minimal-mistakes directly without github-pages gem, comment the line above
# and add:
# gem "jekyll", "~> 4.2"
# gem "minimal-mistakes-jekyll"
```
```name=.gitignore
_site/
.sass-cache/
.bundle/
Gemfile.lock
.DS_Store
```

Exact commands to create the initial commit and push (copy–paste)
1. Clone the (now-renamed) repo locally:
- If you don't already have a local clone, run:
  git clone https://github.com/kingsotieno89/kingsotieno89.github.io.git
  cd kingsotieno89.github.io

2. Create the files locally (example using here-documents — run each block in your shell from inside the repo folder):
- _config.yml
  cat > _config.yml <<'EOF'
  (paste the _config.yml contents from above)
  EOF
- index.md
  cat > index.md <<'EOF'
  (paste the index.md contents from above)
  EOF
- README.md
  cat > README.md <<'EOF'
  (paste the README.md contents from above)
  EOF
- Gemfile
  cat > Gemfile <<'EOF'
  (paste the Gemfile contents from above)
  EOF
- .gitignore
  cat > .gitignore <<'EOF'
  (paste the .gitignore contents from above)
  EOF

(Alternatively, you can create these files in a text editor and save them inside the cloned repo.)

3. Configure Git user (if not already set) and commit:
  git config user.name "Your Name"
  git config user.email "you@example.com"
  git add .
  git commit -m "Initial commit: add Minimal Mistakes Jekyll site"

4. Push to GitHub (this will create the main branch remotely):
  git push -u origin main

Enable GitHub Pages and verify
- Go to: https://github.com/kingsotieno89/kingsotieno89.github.io/settings/pages
- Under "Build and deployment", confirm Branch = main and Folder = / (root), then Save if needed.
- Wait ~30–60 seconds and visit: https://kingsotieno89.github.io

Preview locally (optional)
- If you want a local preview:
  gem install bundler
  bundle install
  bundle exec jekyll serve --livereload
- Open http://127.0.0.1:4000 to preview.

What I tried and what’s next
I prepared the Minimal Mistakes configuration and sample site content and attempted to push them into your newly renamed repository, but I couldn’t create the initial commit from this session because the remote was still empty and requires the first commit from your side or a push that creates the branch. Once you run the push steps above, GitHub Pages should be able to build and publish the site. After you push and enable Pages, tell me and I will verify the Pages build status and confirm the live URL, plus add typical extras (About page, Projects collection, contact form guidance, and a Gemfile.lock if you want locked dependencies).

If you’d prefer, I can generate a single shell script you can run (creates files, commits, and pushes) — tell me and I’ll produce it.
