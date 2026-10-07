# South Florida Personal Injury AI Visibility Index — Edition 2 dataset (October 2026)

Which law firms do ChatGPT, Gemini, Claude and Perplexity recommend when people in South Florida ask who to call after an accident? This dataset contains the full answers behind the CitationOS **South Florida Personal Injury AI Visibility Index, Edition 2**: 60 questions, asked 3 times each on 4 AI assistants with web search enabled, for 720 answers, with the sources each answer cited and the firms it named.

- Report and method: https://www.citationos.ai/research/south-florida-pi-ai-visibility-index-october-2026.html
- Collected: 7 October 2026 (one data-collection window), via each platform's API
- License: CC BY 4.0. Please cite (see below).

> **Important: the answers are raw, unedited AI output.** They can contain errors about real law firms, such as wrong locations, practice areas, results or awards. Nothing in `answer_text` has been verified by CitationOS. Do not treat it as a statement of fact about any firm.

## Files

| File | Rows | What it is |
|---|---|---|
| `answers.jsonl` | 720 | One JSON object per AI answer (fields below) |
| `questions.csv` | 60 | The questions: 40 "core" questions (identical to Edition 1) and 20 city-specific questions |
| `firm-scores.csv` | 119 | Every firm named by at least one assistant, with its score on each platform and our classification of the firm |
| `cited-domains.csv` | 820 | Every website cited as a source, with the number of answers citing it on each platform |

### `answers.jsonl` fields

| Field | Description |
|---|---|
| `answer_id` | A001 to A720 |
| `question_id`, `question`, `category` | Links to `questions.csv`. Categories: direct_intent, problem_based, comparative, authority_framed, long_tail |
| `platform` | ChatGPT, Gemini, Claude or Perplexity |
| `model_version` | Exact API model: `gpt-5-mini-2025-08-07` (OpenAI), `google/gemini-3.1-flash-lite`, `anthropic/claude-sonnet-5.5`, `perplexity/sonar` (the last three via OpenRouter) |
| `mode` | Always `web_search` (the assistant could search the web) |
| `repeat` | 1, 2 or 3: each question was asked three times on each platform |
| `collected_at` | Date of the API call |
| `answer_text` | The assistant's full answer (Markdown as returned) |
| `citations` | Sources the assistant attached: `url`, `title`, `domain`. For Gemini, the API returns expiring Google redirect links, so `url` is null and `domain` is taken from the source title |
| `firms_named` | Law firms identified in the answer by our extraction pipeline: `firm` (canonical name), `position` (order of appearance), `narrative_score_0_5` (how substantively the firm was described, 0 to 5) |

### `firm-scores.csv` fields

`rank`, `firm`, `firm_type`, `average_score` (mean of the four platform scores), one 0–100 score per platform (0 = never named there), `platforms_naming_the_firm` (1 to 4).

Each platform score combines how often the firm was named (35%), how often it appeared in the top three (30%) and how substantively it was described (35%, weighted by how often it was named). `firm_type` is our own classification from public sources: South Florida personal injury firm; national personal injury firm with a South Florida office; South Florida firm with a different main practice; or no South Florida office found.

## Method in brief

1. **Questions.** 60 questions injury victims ask: the 40 questions from Edition 1, word for word, plus 20 questions naming Miami, Fort Lauderdale, Boca Raton or West Palm Beach.
2. **Collection.** Each question was sent 3 times to each assistant's API with web search on. Consumer apps can answer differently from the API.
3. **Extraction.** Firm names were extracted with an LLM, matched to canonical names (fuzzy matching plus manual checks of aliases), and scored.
4. **Market.** The report compares results with the 283 personal injury firms Google Maps shows in the four cities. To avoid singling out firms that were not recommended, the names of firms that no assistant named are **not** included in this dataset; the report gives them only as statistics.

## Limitations

- One market, one practice area, one collection window. AI answers change over time and between runs; that is why each question was asked three times.
- API answers, not consumer app answers.
- Firm extraction can miss or mis-merge names. Domains are kept as returned (for example `attorneys.superlawyers.com` and `superlawyers.com` are separate rows).
- Associations in the report (for example between legal directory presence and being recommended) are based on small groups and do not show cause.

## Updates

CitationOS reruns the same questions weekly. Later snapshots may be added to this dataset with their collection date.

## How to cite

CitationOS (2026). *South Florida Personal Injury AI Visibility Index, Edition 2 (October 2026)* [Data set]. https://www.citationos.ai/research/south-florida-pi-ai-visibility-index-october-2026.html

## Contact

Kivanc Acikgoz, CitationOS · kivanc@citationos.ai · Boca Raton, Florida
