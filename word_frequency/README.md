# Word Frequency Data (COCA)

Word frequency lists from the Corpus of Contemporary American English (COCA, 1 billion words).
Source: [wordfrequency.info](https://www.wordfrequency.info)

## Files

### For Rust transcoding (start here)

| File | Rows | Description |
|------|------|-------------|
| `word_rank_lookup.csv` | 5,050 | **Primary**: rank → word → PoS → freq. Direct lookup table for tokenizer. |
| `lemmas_compact.csv` | 5,050 | Rank, lemma, PoS, freq, perMil, dispersion. Core metrics only. |
| `forms_compact.csv` | 5,050 | Rank, word, freq, #texts, %caps. Surface forms. |

### Full data

| File | Rows × Cols | Description |
|------|-------------|-------------|
| `lemmas_5k.csv` | 5,050 × 25 | Full lemma list with per-genre frequencies (blog, web, TV/movie, spoken, fiction, magazine, news, academic) |
| `word_forms.csv` | 11,460 × 6 | Lemma → surface form mappings (e.g., "be" → is, was, 's, are, were, been) |
| `forms_5k.csv` | 5,050 × 21 | Top 5K individual word forms with per-genre breakdown |
| `subgenres_5k.csv` | 5,050 × 195 | Fine-grained subgenre frequencies (96 subgenres × raw + per-million) |

## Column Reference

### PoS Tags
- `a` = article/determiner
- `v` = verb
- `c` = conjunction
- `i` = preposition
- `p` = pronoun
- `n` = noun
- `j` = adjective
- `r` = adverb
- `t` = particle/infinitive marker
- `d` = modal/auxiliary
- `e` = existential (there)
- `x` = not/negation

### Genre Codes
- `blog` = blog posts
- `web` = general web pages
- `TVM` = TV and movie subtitles
- `spok` = spoken (interviews, conversations)
- `fic` = fiction
- `mag` = magazine
- `news` = newspaper
- `acad` = academic

### Key Metrics
- `freq` = raw frequency (total count across 1B words)
- `perMil` = frequency per million words
- `disp` = dispersion (0-1, how evenly distributed across texts; 1.0 = perfectly even)
- `range` = number of texts containing the word
- `%caps` = percentage of occurrences that are capitalized

## Rust Usage

```rust
// Load the compact lookup for DeepNSM tokenization
use std::collections::HashMap;

struct WordEntry {
    rank: u16,
    pos: String,
    freq: u64,
}

fn load_word_ranks(csv_path: &str) -> HashMap<String, WordEntry> {
    // Parse word_rank_lookup.csv
    // rank,word,pos,freq
    // 1,the,a,50033612
    // 2,be,v,32394756
    // ...
}
```
