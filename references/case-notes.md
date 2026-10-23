# Case notes — one forensic pass, including three corrections I had to make

Anonymised. Numbers are real; names, institution and course are not.

**Subject.** A 54-page honours thesis in finance, 7,766 words of body prose, 357 sentences.
Turnitin returned **46%** with 69 segments flagged as AI-generated. The author's declaration
openly states that GenAI was used "to assist with language editing, code checking, and
debugging" — so the question was never *whether*, but *which layer*.

**Reference corpus.** Two sources, both undetected:
- 1,421 words the same author wrote alone, same discipline, different course
- 1,950 words split across two co-authors on a group project (used to place the author's
  position between a fluent writer and a recent arrival)

---

## 1. What the forensics found

| Tell | Thesis body | Author's own writing |
|---|---|---|
| first person (`I/we/us/our/my/me`) | **0** in 7,766 words | 3 in 1,421 (`us` ×3) |
| prose semicolons | **16** (1.88/1k) | **0** |
| `The` initial | **25.8%** | 14.1% |
| `This` initial | **6.2%** | 19.2% |

All three at once is the signature of a **polish pass**, not a generation:

- zero first person across 7,766 words is not restraint, it is deletion
- his first person is not `I` — it is argumentative `us` (`remind us`, `does not tell us`).
  That habit was zeroed out entirely
- semicolons weld two sentences into one. Nobody drafts that way; editors do
- he delegates anaphora to `This`. Every one of his `This …` openers came back as `The …`

## 2. What argued against wholesale generation

| Evidence | Why it matters |
|---|---|
| Sample-construction counts consistent across four deletion stages (15.7M → 139,904 → 41,945 observations) | A model does not invent a coherent multi-stage attrition chain |
| Introduction kept `the`-initial at 6.2%, i.e. his own range | Those paragraphs still carry his fingerprint |
| Nominalisation density 63.7/1k vs his 59.1/1k | Polish usually pushes this up; it barely moved |
| AI-word list scored 0.5/1k vs his 2.1/1k | The draft was *cleaner* than he is. The word list is useless on this corpus |

Conclusion delivered: **human analysis, machine-polished sentences.**

---

## 3. Three corrections

### 3.1 "Semicolons: 24" → 16

The first count included table footnotes (`Notes: … ; …`, which are conventionally
semicolon-heavy) and citation separators inside parentheses (`(A 2019; B 2021)`).
Counting only prose, outside parentheses: **16**. Still zero on his side, but the tell
was overstated by 50%.

**Rule:** before reporting a character count, ask *where* that character lives and whether
it belongs to the text class you are describing.

### 3.2 "Raise sentence-length cv to 0.42–0.52" → wrong direction

His own cv is **0.290**. The thesis was already **0.518**. The instruction to increase
variance would have moved it *away* from him. Two gate values built on "human writing
averages" had to be withdrawn after the reference corpus arrived:

- `cv 0.36–0.85` — his genuine writing scores 0.286, i.e. **fails the gate**
- `article-initial ≤24%` — his genuine writing is 41.0%, i.e. **fails the gate**

### 3.3 "Add `I`" → should be `us`

The first rewrite added first-person `I`. Wrong: all three of his first-person tokens
are argumentative `us`. A rhetorical `us` restores his stance; an `I argue` invents a
different author.

---

## 4. A rewrite that overshot

First restoration of one 284-word section produced:

| | target | first attempt |
|---|---|---|
| sentence mean | 18.5 | **16.9** |
| short sentences | 6% | **29%** |

It had been "de-flattened" into choppy prose — the generic humanising reflex, applied
by default. Second attempt, merging back to 13–27 word sentences:

| | author | draft | restored |
|---|---|---|---|
| sentence mean | 18.5 | 34.2 | **18.8** |
| cv | 0.290 | 0.464 | 0.255 |
| `The` initial | 14.1% | 55.6% | 11.8% |
| `This` initial | 19.2% | 0% | 17.6% |
| prose semicolons | 0 | 1 | 0 |
| first person | 3 | 0 | 1 (`us`) |

## 5. Vocabulary layer, forgotten on the first pass

Syntax-only editing left the word layer untouched — and made two densities worse:

| per 1k words | original | syntax-only pass | after vocabulary pass | author |
|---|---|---|---|---|
| `therefore` | 1.7 | **3.2** ✗ | 1.1 | 1.4 |
| `rather than` | 1.8 | **2.1** ✗ | 0.7 | 0.7 |
| `associated with` | 1.2 | 1.4 | 1.1 | 0.7 |
| `however` | 0.4 | 0.4 | 0.7 | 1.4 |
| `consistent with` | 0.5 | 0.7 | 1.1 | 1.4 |

Rebuilding sentences tempts you to add connectives; that is exactly how `therefore` reached
2.3× the author's density. **Re-measure vocabulary after every syntax pass.**

Note the last two rows: he uses `however` and `consistent with` *more* than the polished
draft did. Polishing removed them. Not every difference points the same way.

---

## 6. Why the document was not rebuilt from the PDF

Attempting to reconstruct the flagged document from its PDF produced four different body
word counts (8,656 / 9,047 / 9,193 / 8,958) across four extraction passes. The text layer
had three defects:

1. **Page-break truncation** — paragraphs cut in two, tails landing on the next page
2. **Table text welded into paragraphs** — captions and `Notes:` lines became body prose,
   and two sentences separated by an entire table were joined end to end
3. **Display equations missing** — only the surrounding `where f denotes …` survived

Rewriting from that source would have written table notes into the body and deleted the
equations. The correct input is the author's original `.docx`.

**Rule:** never rebuild a submission-ready document from a PDF text layer. Measure from it,
yes; regenerate from it, no.
