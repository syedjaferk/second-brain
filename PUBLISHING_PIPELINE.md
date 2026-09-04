# Publishing pipeline: Obsidian vault -> categorized -> GitHub Pages with graph view

This ties together with the earlier `obsidian_categorize.py` script:

```
[Your Obsidian vault]
        |
        v
obsidian_categorize.py   (categorizes + backlinks posts using your local LLM)
        |
        v
setup_quartz_site.sh     (one-time: scaffolds Quartz, copies vault into it)
        |
        v
git push                 (every time you publish)
        |
        v
GitHub Actions (deploy.yml)  -->  builds Quartz  -->  deploys to GitHub Pages
        |
        v
Live site with search, backlinks, tag pages, and an interactive graph view
```

## One-time setup

1. Run the categorizer first (from the earlier step), so your vault already
   has `category`/`tags` frontmatter and `## Related Posts` backlinks:
   ```bash
   python obsidian_categorize.py /path/to/vault --host http://192.168.1.50:11434
   ```

2. Scaffold the site (needs Node.js 18+ installed):
   ```bash
   chmod +x setup_quartz_site.sh
   ./setup_quartz_site.sh /path/to/vault your-github-username your-repo-name
   ```
   This clones Quartz, copies your vault into `quartz/content/`, sets the
   site's base URL, and wires up the GitHub Actions workflow.

3. Create an **empty** GitHub repo matching the name you gave the script,
   then in that repo go to **Settings > Pages > Source** and select
   **GitHub Actions**.

4. Push:
   ```bash
   cd quartz
   git add .
   git commit -m "Initial site from Obsidian vault"
   git push -u origin main
   ```

GitHub Actions will build and deploy automatically — check the "Actions" tab
for progress. First deploy takes a couple of minutes; your site then goes
live at the URL the setup script printed.

## Publishing new/edited posts from now on

Re-run the categorizer on your vault (it only reprocesses new/changed files),
then:

```bash
rsync -av --exclude ".obsidian" --exclude "*.bak" --exclude ".blog_ai_cache.json" \
  /path/to/vault/ quartz/content/
cd quartz
git add .
git commit -m "Add new post: <title>"
git push
```

Each push triggers the same GitHub Actions workflow and updates the live site.

## About the graph view

Quartz includes this by default — nothing extra to build:
- **Global graph**: a button (usually top-right) opens a force-directed graph
  of your whole site, edges drawn from your `[[wikilinks]]` — which is exactly
  what the `## Related Posts` backlinks from `obsidian_categorize.py` produce.
- **Local graph**: each post's sidebar shows a small graph of just its direct
  neighbors.
- Both are configured in `quartz/quartz.layout.ts` under the `Component.Graph(...)`
  entries — you can tune `depth`, `scale`, node colors, etc. there if you want
  to restyle it.

Quartz also auto-generates a `/tags` index page from your frontmatter `tags`,
and folders show up in the left-hand file Explorer. Note that Quartz doesn't
have a built-in concept of "category" specifically — if you want your
`category` field to be just as browsable as tags, the simplest option is to
have the categorizer script fold it into `tags` too (or ask me and I'll add
that as a flag).

## Notes

- `.obsidian`, `.bak` backup files, and `.blog_ai_cache.json` are excluded
  from what gets copied/published — they're workspace files, not content.
- If you rename `content/` files or vault posts, wikilinks that reference the
  old title will break — Quartz will show them as red/missing links, easy to
  spot.
- You can preview any changes locally before pushing with:
  ```bash
  cd quartz && npx quartz build --serve
  ```
