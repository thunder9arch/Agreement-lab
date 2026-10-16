# Agreement Lab

A single-file, zero-dependency web app for measuring inter-annotator agreement, including whether an **LLM-as-judge** can be trusted. Everything runs in your browser; no data is uploaded anywhere.

## Features

- **Krippendorff's α** (nominal, ordinal, interval) with missing-data support and a 95% bootstrap confidence interval
- **Cohen's κ** for every rater pair, plus each rater's mean κ against the others
- Raw % agreement, share of items everyone agreed on, and per-label specific agreement
- **Judge check:** κ of the judge vs the human majority, compared with human–human κ, a confusion matrix, and a label-distribution comparison to expose bias
- Filterable, searchable item list showing exactly which items caused disagreement
- CSV/TSV upload or drag-and-drop, last dataset remembered in `localStorage`, light/dark theme

## Run it

Open `index.html` in a browser. No build step, no server, no dependencies.

## Input format

One row per item, one column per rater, rater names in the header row. Comma or tab separated. Blank, `NA`, `N/A`, `NaN`, `null`, `none` or `-` mean "missing". An optional first column named `item`, `id`, `text`, `example` or `prompt` labels the rows. See `example.tsv`.

```
item,human_A,human_B,llm_judge
Reply is polite,good,good,good
Invents a citation,bad,bad,good
```

A column whose name contains `judge`, `llm`, `gpt`, `claude`, `model` or starts with `ai` is preselected as the judge; change it in the top bar.

<img width="1035" height="561" alt="Screenshot 2026-10-16 133655" src="https://github.com/user-attachments/assets/c089e7b1-905b-4e23-8fe3-0f843ee0a83c" />
## Reading the numbers

| α / κ | Meaning |
|---|---|
| ≥ 0.80 | reliable |
| 0.67 – 0.80 | tentative conclusions only |
| < 0.67 | unreliable |

(κ labels follow Landis & Koch: <0.2 slight, 0.2–0.4 fair, 0.4–0.6 moderate, 0.6–0.8 substantial, >0.8 almost perfect.)

The judge verdict is a rule of thumb: the judge passes when its κ against the human majority is within 0.05 of the human–human mean κ and at least 0.6. κ and α fall when one label dominates even if raw agreement is high, so read them alongside % agreement and the disagreement list. Items where humans tie are excluded from majority-based figures.

## Deploy on GitHub Pages

1. Push this folder to a repository.
2. **Settings → Pages → Build and deployment → Deploy from a branch**, choose `main` and `/ (root)`.
3. The app is served at `https://<user>.github.io/<repo>/`.

## License

MIT, see `LICENSE`. Replace  in the license before publishing.
