[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/lauFYeeP)
# Personal vs Promotional: Modeling Mompreneur Narratives in #SAHM TikTok (Public Repo)

**Course:** DS340H
**Author:** Ruth Jin  
**Date:** Dec. 23, 2025

This repository contains **public-safe outputs and analysis code** for my DS340 final project. It includes:

- **B_generate_poster_figures_PUBLIC** (public-facing analysis + visualization)
- **Sanitized datasets** (hashed creator/post IDs; no raw text/usernames)
- **Figures and tables** generated from the sanitized datasets

> **Important:** The full raw dataset (including usernames and text such as captions and voice-to-text transcripts) is **not included** in this public repository

---

## Project Summary

Mompreneurs (mothers running home-based businesses) use TikTok to share daily life while also promoting products, services, and income opportunities. Within the broader #SAHM community, posts often blend **personal storytelling** with **promotional messaging**.

In this public repo, I analyze:

- How frequently posts are classified as personal vs promotional
- How promotional probability varies across creators
- How promotional intensity relates to engagement outcomes at the creator level
- How creator-level promotional patterns change over time

My full research question is: How do mompreneur creators within the #SAHM TikTok community balance personal and promotional storytelling content, and how does this balance relate to audience engagement at the creator level?


---

## What’s in This Public Repo

### `B_generate_poster_figures_PUBLIC` (public analysis notebook)
- Loads sanitized CSVs from `data_sanitized/`
- Produces the plots in `figures/` and the tables in `tables/`
- Runs creator-level engagement analyses (including OLS regression)

> The model training and any processing involving raw text occur in a **private** notebook (not included here).

### `data_sanitized/` (public-safe datasets)
These CSVs contain **no raw text** and use **hashed IDs**.

- `post_level_sanitized.csv`  
  Post-level dataset including:
  - hashed `post_key`, `creator_id`
  - `year`
  - engagement counts (`view_count`, `like_count`, `comment_count`, `share_count`)
  - derived text-length features (`n_words_desc`, `n_words_vt`, `n_words_desc_vt`)
  - model outputs (`p_promotional`, `style_pred`)
  - derived engagement rates (`like_rate`, `like_rate_w`)

- `creator_stats.csv`  
  Creator-level aggregation including:
  - `total_posts`
  - `mean_p_promotional`
  - `frac_pred_promotional`
  - engagement summaries (e.g., `median_like_rate`, `mean_like_rate`)
  - text-length summary (`median_words`)

- `creator_year_stats.csv`  
  Creator-year aggregation including:
  - `n_posts`
  - `frac_promotional`
  - `mean_p_promotional`

- `model_metrics.csv`  
  Validation metrics for two models trained in the private notebook:
  - `caption_only`
  - `caption_plus_vt`

- `human_validation_confusion.csv`  
  Aggregate human validation results (confusion counts + accuracy + Cohen’s κ) for a manually labeled sample
  - Contains only counts/metrics (no text)

### `figures/`
Saved plots produced by Notebook B (distributions, confusion matrix visualization, creator trend panels, promo vs engagement plots)

### `tables/`
Saved tables produced by Notebook B (model comparison table, regression coefficient table)

---

## How to Run Notebook B

1. Open `B_generate_poster_figures_PUBLIC.ipynb`
2. Run cells top-to-bottom

Outputs will be written to:
- `figures/`
- `tables/`

---

## Data Ethics & Privacy

To protect privacy and comply with public release constraints:

- **No usernames, captions, or voice-to-text transcripts** are included.
- Creator/post identifiers are **hashed**.
- Only **derived features**, aggregated metrics, and model outputs are shared publicly.

All modeling that requires raw text or direct identifiers is performed in a separate **private repository**.

---

## Notes on Interpretation

- `style_pred` is a binary label (personal vs promotional) predicted by a classifier trained using weak supervision and then validated on a human-labeled sample.
- `p_promotional` is the **continuous probability** that a post is promotional; this is used as the main “degree of promotional storytelling” measure.
- Engagement outcomes are analyzed at the **creator level** (e.g., median like rate), with controls such as posting volume and median text length.
