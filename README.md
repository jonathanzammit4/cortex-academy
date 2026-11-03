# Cortex Academy

A personal, visual-first learning platform for AI and computer science. It runs as a single
HTML file with no build step, no dependencies and no backend.

**Live site:** `https://YOUR-USERNAME.github.io/cortex-academy/`

## Features

- **Dashboard:** progress ring, recommended next lesson, a revision list and track progress
- **Roadmap:** lessons ordered by prerequisites, with planned lessons shown as dashed items
- **Library:** search by title, description, tag or track, with related-lesson links
- **Lessons:** what it is, why it exists, how it works, where it is used and its limits
- **Interactive widgets:** gradient descent, a neuron, cosine similarity, softmax with temperature,
  step-through diagrams and an LRU cache simulator
- **Assessment:** quizzes with explanations, flashcards that resurface missed cards, and
  predict-the-output challenges
- **Tracking:** completion marks, bookmarks, per-lesson notes and project checklists
- **Themes:** light and dark mode, responsive layout

## Current curriculum

| Track | Lessons |
| --- | --- |
| Python | Names, values and mutability |
| ML and deep learning | Loss and gradient descent, The neuron and the network |
| LLMs and agents | Embeddings and similarity, Softmax and temperature, How a RAG system works |
| Systems and cloud | What happens when you load a URL, Caching and LRU eviction |

Planned lessons are listed on the Roadmap page (transformers, backpropagation, agents, MCP,
fine-tuning, databases, distributed systems, MLOps and more).

## Run locally

No installation is needed. Open `index.html` in a browser.

Optionally serve it from a local web server:

```
python3 -m http.server 8000
```

Then visit `http://localhost:8000`.

## Deploy to GitHub Pages

1. Push `index.html` and this README to a public repository named `cortex-academy`.
2. Go to **Settings, then Pages**.
3. Set Source to **Deploy from a branch**, choose `main` and `/ (root)`, then save.
4. The site goes live after a minute or two.

## Your progress and backups

Progress (completed lessons, quiz scores, flashcards, notes, bookmarks, project ticks and theme)
is stored in your browser's local storage, separately for each web address and each browser.

- Use **Download backup** or **Copy backup** on the Home page regularly.
- Use **Restore from file** or **Restore pasted backup** to load progress on another device
  or after clearing browser data.
- Clearing site data, using private windows, or changing the site address starts you from zero
  unless you restore a backup.

## Project structure

Everything lives in `index.html`:

| Section | Purpose |
| --- | --- |
| `<style>` | Theme variables (light and dark) and all styling |
| `T`, `PL`, `PJ` | Track definitions, planned lessons and projects |
| `L` | The lesson array, which holds all lesson content |
| `W` | Interactive widgets, one function each |
| `V` | Views: home, roadmap, library, cards, projects, lesson |
| `route()` | Hash-based router (`#home`, `#roadmap`, `#l-<lesson-id>`) |

## Adding a lesson

Add an object to the `L` array:

```js
{
  id: 'ml-2',                 // unique, used in URLs (#l-ml-2)
  t: 'Lesson title',
  tr: 'ml',                   // track key: py, ml, llm or sys
  lv: 'Beginner',             // Beginner, Intermediate or Advanced
  min: 15,                    // estimated minutes
  pre: ['ml-1'],              // prerequisite lesson ids
  tags: ['regression'],       // used for search and related lessons
  d: 'One-line summary.',
  b: `<h3>What it is</h3><p>HTML before the widget.</p>`,
  w: 'gd',                    // optional widget: gd, neuron, cos, soft, step, lru
  b2: `<h3>Limits</h3><p>HTML after the widget.</p>`,
  c: ['Challenge prompt', 'Answer shown on reveal'],   // optional
  q: [['Question?', ['A', 'B', 'C'], 1, 'Explanation']], // [text, options, correct index, why]
  f: [['Front of card', 'Back of card']]
}
```

For a step-through diagram, set `w: 'step'` and add `sd: [['Step name', 'Description'], ...]`.

To add a new widget, add a function to `W` that receives the container element, builds its
HTML and attaches its own event handlers. Then set `w` to its name.

Remove the matching entry from `PL` once a planned lesson is built.

## Roadmap

1. More lessons: backpropagation, transformers, fine-tuning, agents and MCP, LLM evaluation
2. Optional in-browser Python runner for coding challenges
3. Rebuild in Next.js and TypeScript, with lessons stored as content files
4. Login and cross-device sync of progress

## Licence

Personal learning project. Add a licence of your choice before sharing the code publicly.
