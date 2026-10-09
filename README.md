# South Florida Personal Injury AI Visibility Index — Edition 2 dataset (October 2026)

Which law firms do ChatGPT, Gemini, Claude and Perplexity recommend when people in South Florida ask who to call after an accident? This dataset contains the full answers behind the CitationOS **South Florida Personal Injury AI Visibility Index, Edition 2**: 60 questions, asked 3 times each on 4 AI assistants with web search enabled, for 720 answers, with the sources each answer cited and the firms it named.

- Report and method: https://www.citationos.ai/research/south-florida-pi-ai-visibility-index-october-2026.html
- Collected: 7 October 2026 (one data-collection window), via each platform's API
- Version: **1.1** (9 October 2026). Version 1.0 undercounted the firms named; see [Changelog](#changelog).
- License: CC BY 4.0. Please cite (see below).
- DOI: [10.5281/zenodo.23238387](https://doi.org/10.5281/zenodo.23238387) (Zenodo; always resolves to the latest version)

> **Important: the answers are raw, unedited AI output.** They can contain errors about real law firms, such as wrong locations, practice areas, results or awards. Nothing in `answer_text` has been verified by CitationOS. Do not treat it as a statement of fact about any firm.

## Files

| File | Rows | What it is |
|---|---|---|
| `answers.jsonl` | 720 | One JSON object per AI answer (fields below) |
| `questions.csv` | 60 | The questions: 40 "core" questions (identical to Edition 1) and 20 city-specific questions |
| `firm-mentions.csv` | 632 | Every firm named by at least one assistant, with the number of answers naming it on each platform |
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
| `firms_named` | Law firms named in the answer: `firm` (canonical name) and `position` (order of appearance). A lawyer named as part of a firm counts toward that firm |

### `firm-mentions.csv` fields

`firm`, `answers_naming_firm` (of 720), one column per platform with the number of answers naming the firm there (of 180 each), `platforms_naming_the_firm` (1 to 4), `in_google_maps_top100` (yes if the firm is among the 283 firms in the Google Maps list used by the report).

Firms on the Google Maps list are matched by hand-checked rules. Other firms (for example national firms or firms outside South Florida) are grouped automatically across spellings and may contain a few grouping errors.

## Method in brief

1. **Questions.** 60 questions injury victims ask: the 40 questions from Edition 1, word for word, plus 20 questions naming Miami, Fort Lauderdale, Boca Raton or West Palm Beach.
2. **Collection.** Each question was sent 3 times to each assistant's API with web search on. Consumer apps can answer differently from the API.
3. **Extraction.** Every firm and lawyer name in each answer was extracted with an LLM (gpt-5-mini) and grouped into firms. Names were matched to the Google Maps list with an LLM check of each candidate pair plus a hand review of borderline pairs. The count of Google Maps firms named was repeated independently with a separate method; the two counts differed by one firm. On a random sample of 30 answers checked with a different model, the firm lists captured over 96% of the firms named.
4. **Market.** The report compares results with the 283 personal injury firms Google Maps shows in the four cities. To avoid singling out firms that were not recommended, the names of firms that no assistant named are **not** included in this dataset; the report gives them only as statistics.

## Limitations

- One market, one practice area, one collection window. AI answers change over time and between runs; that is why each question was asked three times.
- API answers, not consumer app answers.
- Firm extraction can miss or mis-merge names. Domains are kept as returned (for example `attorneys.superlawyers.com` and `superlawyers.com` are separate rows).
- Associations in the report (for example between Google reviews and being named) do not show cause.

## Updates

CitationOS reruns the same questions weekly. Later snapshots may be added to this dataset with their collection date.

## Changelog

**1.1 (9 October 2026).** Version 1.0's `firms_named` came from our production pipeline, which skipped a firm the first time it appeared and dropped later mentions of firms an automated relevance check had rejected; 252 of 720 answers had no firm recorded. Version 1.1 re-extracts every answer. Effects: firms on the Google Maps list named at least once rose from 47 to 126 of 283 (never named: 55%, not 83%). `firm-scores.csv` (platform scores and firm types) is withdrawn and replaced by `firm-mentions.csv`; the `narrative_score_0_5` field is removed. `answer_text`, `citations`, `questions.csv` and `cited-domains.csv` are unchanged. Details: https://www.citationos.ai/research/south-florida-pi-ai-visibility-index-october-2026.html#correction

**1.0 (8 October 2026).** First release.

## How to cite

CitationOS (2026). *South Florida Personal Injury AI Visibility Index, Edition 2 (October 2026)* (Version 1.1) [Data set]. Zenodo. https://doi.org/10.5281/zenodo.23238387

## Contact

Kivanc Acikgoz, CitationOS · kivanc@citationos.ai · Boca Raton, Florida
