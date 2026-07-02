# Lab Task 4: Text Pre-Processing Techniques

**Course:** DL-3002 Data Mining Lab
**Instructor:** Saad Munir

## Overview

This lab applies text pre-processing techniques to the news dataset scraped in the
previous lab (`output.csv`), covering noise removal, normalization, n-gram extraction,
frequency analysis, tokenization, subword tokenization, and a discussion of
contextualized tokenization.

## Files

| File | Description |
|---|---|
| `labtask4.ipynb` | Main deliverable — notebook with code and outputs for every task |
| `output.csv` | Dataset: `headline`, `date`, `source` columns (2600 rows) |
| `Lab Task 4.pdf` | Assignment instructions |
| `Lab Manual 4.pdf` | Lab manual / reference material |

**Dataset note:** `output.csv` only contains `headline`, `date`, and `source` — there is
no separate article body column. The `headline` field is therefore used as the text
("news body") for every pre-processing step in the notebook.

## Tasks Covered

1. **Noise Removal** — HTML/URL stripping (BeautifulSoup + regex), special character
   removal (keeping periods and commas), lowercasing.
2. **Normalization** — stemming (Porter) vs. lemmatization (WordNet) comparison, and
   stop word removal.
3. **N-gram Extraction** — unigrams, bigrams, trigrams via NLTK, plus
   `BigramCollocationFinder` / `TrigramCollocationFinder` with PMI scoring.
4. **Frequency Analysis** — top 10 most common unigrams, bigrams, and trigrams via
   `FreqDist`.
5. **Tokenization** — word-level vs. sentence-level granularity.
6. **Subword Tokenization** — BERT WordPiece tokenization to handle out-of-vocabulary
   words.
7. **Contextualized Tokenization** — discussion of how models like BERT produce
   context-dependent representations, and whether this would help this dataset.

## Requirements

```
python >= 3.9
pandas
nltk
beautifulsoup4
tokenizers
huggingface_hub
```

Install with:

```bash
pip install pandas nltk beautifulsoup4 tokenizers huggingface_hub
```

The notebook downloads the required NLTK corpora (`punkt`, `stopwords`, `wordnet`,
`omw-1.4`) on first run via `nltk.download(...)`.

## Running

Open `labtask4.ipynb` in Jupyter/VS Code and run all cells top to bottom. It reads
`output.csv` from the same folder, so keep both files together.

## Environment Note: BERT Subword Tokenization

Task 6 needs BERT's WordPiece vocabulary. Rather than the full `transformers` package
(which pulls in `torch`), the notebook uses the lightweight `tokenizers` library's
`BertWordPieceTokenizer` loaded directly with the official `bert-base-uncased`
`vocab.txt` (fetched via `huggingface_hub`). This gives identical, real WordPiece
tokenization without a torch dependency.

Task 7 (contextualized tokenization) is discussed conceptually rather than run as a live
model, since producing real BERT contextual embeddings requires a working `torch`
install, which was broken (DLL load failure) in the environment this notebook was
built in. If you have a working `torch` install, you can extend task 7 with:

```python
from transformers import BertTokenizer, BertModel

tokenizer = BertTokenizer.from_pretrained('bert-base-uncased')
model = BertModel.from_pretrained('bert-base-uncased')

inputs = tokenizer(headline, return_tensors='pt')
last_hidden_state = model(**inputs).last_hidden_state  # one context-dependent vector per token
```
