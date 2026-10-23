# AGENTS.md — fooddoof cookbook

Operating manual for coding agents in this repo. Read it fully before writing
anything; follow it so every session starts at full speed.

## The pitch

**fooddoof** is the user's personal cookbook. The user asks for a recipe in
conversation; the agent writes it as markdown into `_recipes/`, commits, and
pushes. GitHub Pages serves the result automatically.

**Live site:** <https://meowsus.github.io/fooddoof/>

## Layout

| Path | What it is |
| --- | --- |
| `_recipes/*.md` | Every recipe, one file per recipe. This is where you work. |
| `index.md` | Homepage; auto-lists recipes via Liquid. **Never edit it to add a recipe.** |
| `about.md` | Static about page |
| `_config.yml` | Jekyll config (minima theme, recipes collection). Don't touch without a reason. |
| `Gemfile` | Optional local-preview tooling |
| `_recipes/emergency-garlic-noodles.md` | The canonical example. Mimic it. |

## Adding a recipe

1. Filename: `_recipes/<kebab-case-dish-name>.md`, lowercase, no quotes or
   colons — e.g. `_recipes/miso-butter-ramen.md`.
2. Fill in the template below. **No other files need to change** — the index
   picks recipes up automatically.
3. Commit the single file to `main` with message `recipe: <dish name>` and
   push. No PR needed; this is a personal cookbook.
4. Pages redeploys within a minute or so. Check with:
   `gh api repos/meowsus/fooddoof/pages/builds/latest --jq .status`
   (`error` → built. Wait ~60s, check again.)

Do **not**: create a PR, hand-rebuild the index, restyle the site, or touch
`_config.yml` while adding a recipe.

## Recipe template

```markdown
---
layout: page
title: <Dish Name>
---

*<servings> · <total time> · <difficulty>*

<One-to-three-sentence description. Make it sound delicious; land a joke only
if it lands.>

## Ingredients

- <amount> <ingredient>, <prep>
- ...

## Steps

1. <Start with a verb. Include times/temps where they matter, plus a doneness cue.>
2. ...

## Tips & Variations

- <Substitutions, scaling, storage, upgrade ideas. 2–5 bullets.>
```

## Rules that make recipes good

- **Tone: warm and a little silly.** Appetizing first, joke second — one or
  two light jokes per recipe, max. A recipe that is all jokes is a blog, not
  a cookbook.
- **Units: US imperial primary; metric in parentheses when precision
  matters.** e.g. `2 cups (250g) flour`, `8 oz (225g) noodles`. Oven temps as
  `375°F (190°C)`. Don't clutter imprecise items (`1 onion`) with conversions.
- **Metadata line:** `*servings · total time · difficulty*`. Difficulty is
  honest and short: easy / medium / hard is fine, playful is fine
  ("stupidly easy").
- **Ingredients:** one per line, amount first, prep last
  (`2 scallions, thinly sliced`). Sub-headings within the section only when
  the list is long (e.g. "Sauce" / "Noodles").
- **Steps:** imperative, chronological, nothing skipped. Give both a time and
  a sensory cue ("until golden and it smells nutty, 2–3 minutes"). Warn at
  tricky moments ("it will look broken before it comes together — keep
  stirring").
- **Tips & Variations** is real content: swaps for missing ingredients,
  vegan/protein variants, storage, scaling. No filler.
- **Titles** are natural and appetizing: "Miso Butter Ramen", not "Ramen With
  Miso-Butter Sauce (Weeknight Version)". Playful is fine if the dish is
  still identifiable.

## Agent behavior

- **Prefer generating over asking.** Fold "vegan / fast / cozy / for a crowd"
  into the recipe. Ask a clarifying question only when the request is truly
  unguessable — and even then a confident default is usually better than a
  question.
- Don't edit a published recipe unless asked, or unless it's wrong.
- One recipe, one commit.
- If the user says "remember" something about the cookbook, record it in
  agent memory **and**, if it's an enduring dietary fact, in House notes
  below.

## House notes

*(No dietary restrictions or allergies recorded yet. If the user ever
mentions them, add them here so every future recipe respects them.)*

## Local preview (optional)

GitHub builds the site, so this is rarely needed:

```sh
bundle install
bundle exec jekyll serve   # http://127.0.0.1:4000/fooddoof/
```

(No ruby on the main machine as of Oct 2026 — pushing to `main` is the normal
way to see the site.)