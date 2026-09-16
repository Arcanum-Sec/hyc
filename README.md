# Hacking Your Career

A standalone HTML guide: a roadmap and verified resource library for becoming the strongest
cybersecurity candidate you can be — what to learn, where to practice it, how to package
yourself, how to find the opportunities worth having, and how to judge them when they arrive.

Class by Jason Haddix ([@Jhaddix](https://twitter.com/Jhaddix)) · [Arcanum](https://arcanum-sec.com/).
Rebuilt as a student resource from the original 114-slide deck.

## Files

```
index.html                  the whole guide — one page, 15 modules
assets/css/styles.css       all styling, design tokens at the top
assets/img/fig-bugcrowd.png screenshot figure (portfolio module)
assets/img/fig-reddit.png   screenshot figure (finding opportunities module)
assets/img/resume-old.png   resume before, from the class deck (identity masked)
assets/img/resume-new.png   resume after, from the class deck (identity masked)
.claude/launch.json         local preview server config
.nojekyll                   tells GitHub Pages to serve files as-is
```

No build step, no dependencies, no JavaScript framework. Open `index.html` and it works.

## Preview locally

Just open the file:

```bash
open index.html
```

Or serve it, which more closely matches how GitHub Pages will behave:

```bash
python3 -m http.server 8000
```

Then visit <http://localhost:8000>.

## Deploy to GitHub Pages

Lives at **https://arcanum-sec.github.io/hyc/**

The repo is already initialized with a first commit on `main`. To publish:

```bash
gh auth login
```

```bash
gh repo create Arcanum-Sec/hyc --public --source=. --remote=origin --push
```

```bash
gh api -X POST repos/Arcanum-Sec/hyc/pages -f "source[branch]=main" -f "source[path]=/"
```

Or enable it by hand: **Settings → Pages → Source: Deploy from a branch → `main` / `/ (root)`**.
First build takes a minute or two. After that, every `git push` to `main` redeploys.

Subsequent updates:

```bash
git add -A && git commit -m "your message" && git push
```

### Why the paths work at a subpath

Pages serves this as a *project* site under `/hyc/`, not at a domain root. Every asset
reference in `index.html` is relative (`assets/css/styles.css`, not `/assets/...`), so it
resolves correctly under the subpath. If you ever add a link or image, keep it relative —
a leading slash will 404 in production while still working locally.


## Editing notes

- **Design tokens** are the `:root` block at the top of `styles.css`. Colors are defined three
  times on purpose — once for light, once under `prefers-color-scheme: dark`, once under
  `[data-theme="dark"]` — so the page reads correctly whether a visitor's OS is light, dark, or
  unset. Change a color in all three, or only in the one you mean.
- **Diagrams are inline SVG** in `index.html`, not images. They pull their colors from the same
  tokens, so they follow the theme. Search for `class="dgm"` to find them.
- **The two `.png` figures** are screenshots cropped from the original slide deck. Everything
  else is drawn.
- **Module cross-references** use anchors (`href="#labs"`), not hard-coded numbers, so sections
  can be reordered without breaking links. The visible "Module 04" text does still need updating
  by hand if the order changes.
- **Spelling is US English** throughout (color, defense, practice, catalog). Note that
  `academy.hackthebox.com/catalogue` is a real URL and keeps the British spelling — don't
  "fix" it.
- **Links were verified** at build time by fetching each page, not just pinging it: names and
  free-tier status too, not only HTTP 200. Known bot-blockers (Cloudflare, academic publishers)
  return 403 to scripts but open fine in a browser — don't "fix" those.
- **Two role tables** (Modules 02 and 13) share the same `.rl` / `.def` hover-tooltip pattern.
  Tooltips work on hover, keyboard focus and tap.

## Content provenance

Module text follows the original slides. Where a slide carried only a heading or a screenshot,
the surrounding prose expands on the point being made rather than inventing new material.

Not from the original deck, and marked as such in the guide:

- **Module 02 (Red, Blue & Purple)** — the deck sorts every list by color without defining the terms.
- **Module 04 (Labs & Practice)** — split out of education, since hands-on work is a student's
  substitute for a work history.
- **Module 05 (Recommended Books)** — researched reading list, three per track.
- **Module 13 (Tools by Job Role)** — enterprise and open-source tooling per role, on hover.
- **Module 14 (Blanchard Playbook)** — 20 numbered insights from Jason Blanchard's *Job Hunt Like a
  Hacker* talks, summarized from transcripts of 24 of his recorded sessions.
- **Module 15 (Aptitude & Work Ethic)** — the I/O-psychology evidence for why aptitude beats the
  requirements checklist, with honest treatment of the oversold parts (grit, growth mindset,
  learning agility, 10,000 hours). Closes the guide.
- **Added free resources** — weighted toward training that is free *and* ends in a free certificate.

Deliberately omitted: the class's negotiation module (offer negotiation, compensation
benchmarking, leadership severance terms), which is out of scope for a student resource.

Two caveats carried in the guide itself: the market commentary in the interviewing module reflects when the
class was taught, and free tiers and free-certificate programs change without notice — confirm
terms on the provider's own page.
