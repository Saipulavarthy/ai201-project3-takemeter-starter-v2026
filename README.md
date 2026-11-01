# TakeMeter

> ### 👋 Start here
>
> **New to this repo? Read [RUNNING.md](RUNNING.md) first** — setup, the
> notebook, the baseline, and what to do when something breaks.
>
> Once `python test.py` passes:
>
> ```bash
> head -5 data/practice_labels.csv     # the shape your labels.csv needs
> ```
>
> Then open `takemeter.ipynb` **in this folder** — in VS Code, or with
> `jupyter notebook` if you prefer. Pick the kernel: the `.venv` inside this
> project. Run section 1, which reports the hardware you'll be training on.
> Everything else waits until you have data.
>
> Nothing to upload, nothing to connect, no accounts and no keys. The notebook
> runs on your machine and writes next to your code.
>
> **The rest of this file is your submission.** Fill it in as you go.

---

<!-- ─────────────────────────────────────────────────────────────────────────
     HOW TO USE THIS FILE

     Unit 5 asks for the first five sections. Unit 6 adds the five below them.

     Everything is pasted as TEXT. No screenshots, no images.

     ⚠️ The confusion matrix especially. The notebook prints one as a markdown
     table, ready to copy. A screenshot of a matrix earns nothing. Paste the
     table.
     ───────────────────────────────────────────────────────────────────────── -->

<!-- ═══════════════════════ UNIT 5 — THE BUILD ═══════════════════════ -->

## What This Does

<!-- Your community, and what your classifier sorts posts into. Three or four
     sentences. -->

TakeMeter sorts posts from r/LocalLLaMA, a public subreddit about running AI models locally, into three labels: analysis, hot_take, and reaction.

---

## Label Taxonomy

<!-- Each label: a one-sentence definition and two real examples from your
     reading. Then your decision rule for the hardest boundary.

     The decision rule is worth a point on its own and it's the thing most
     people leave out. Every taxonomy has a hardest boundary. Name yours. -->

### `analysis`

**Definition:** makes a claim and backs it with something specific and checkable, like a measured speed, a config, a described test, or a quote.

**Example 1:**
> a post listing tokens per second for specific CPUs and linking pull request numbers.

**Example 2:**
> a post arguing that tool templates matter more than the model, with a described test setup and tool-call failure counts.

### `hot_take`

**Definition:** a confident claim or verdict with nothing offered to support it. It might be true, but it isn't argued.

**Example 1:**
> TBD.

**Example 2:**
> TBD.

### `reaction`

**Definition:** an immediate response to news or an event where the feeling is the content, such as shock, excitement, or complaint.

**Example 1:**
> a post expressing shock at GPU price jumps, where the numbers only serve the venting.

**Example 2:**
> TBD.

### The hardest boundary

**Which two labels:** analysis vs. reaction

**The decision rule I used every time:**
<!-- e.g. "If the post names a specific checkable fact, it's `analysis`, even
     if the tone is heated." -->
a number or fact only makes a post analysis if the post uses it to support a claim. If the numbers are just context for a feeling, it is reaction.

Additional rules:
- Checkable means something a reader could look up or re-run: a named model, quant, hardware, quote, link, or spec figure. The author does not have to have measured it, but it must be used to support the claim. A vague impression with no specifics does not count.
- Label a post by its main claim. One unsupported opinion sentence at the end does not change a post that is otherwise backed by specifics.
- Being set off by a release or news does not make a post reaction. Remove the feeling words (for example "so tired of this" or "lol"). If a verdict remains, it is hot_take. If nothing claim-like remains, it is reaction.


---

## The Dataset

<!-- Where you collected from, how you labelled, your counts, and three hard
     cases. -->

**Where the posts came from:** Community: r/LocalLLaMA. I read about 35 posts from the Hot feed in October 2026 before choosing labels. Pure help questions (for example "what model fits my A2000?") fit none of the three labels, so I skip them when collecting. A question that makes a claim with evidence can still be labeled. Candidate distinctions I noticed while reading: posts that report measured numbers versus posts that don't; claims backed by a described test versus claims just asserted; immediate reactions to news versus posts that work out what evidence would settle a question; and help questions with detailed setups versus one-line questions.

**How I labelled them:** <!-- Cold first? Pre-labelled with AI and corrected?
Say so plainly — the disclosure is required, not penalised. --> Some rows were pre-labeled by an AI assistant and then reviewed by me, as described in the disclosure under How I Used AI. The data is a mix of posts and comments from r/LocalLLaMA. Comments are marked comment in the note column. Comments under 20 words were skipped so that short length would not become a shortcut for any label.

**Counts per label:**

| Label | Count | Share |
|---|---|---|
|  |  |  |
|  |  |  |
|  |  |  |
| **Total** |  | 100% |

**Three hard cases**

<!-- Any post that made you pause: what it was, which two labels it could have
     been, and what you chose. These are worth more than the easy 190. -->

**1.**
> *The post:*
>
> *Could have been:*
>
> *I chose, because:*

**2.**
> *The post:*
>
> *Could have been:*
>
> *I chose, because:*

**3.**
> *The post:*
>
> *Could have been:*
>
> *I chose, because:*

---

## The Training Run

<!-- Your starting model, your settings, and anything you changed and why. -->

**Base model:**

**Settings:** <!-- epochs, learning rate, batch size, seed -->

**Anything I changed from the defaults, and why:**

**Split sizes:** <!-- train / val / test, and per-label counts in the test
split. If a label had fewer than about 8 in test, say so — it explains a lot
of next unit's variance. -->



---

## How I Used AI

<!-- Two specific moments — what you asked, what came back, what you changed.

     ⚠️ Plus disclosure of any pre-labelling. If you had a model pre-label a
     batch and then read and corrected every one, say that. It's an allowed
     workflow and disclosing it costs you nothing. Not disclosing it is the
     problem. -->

**Moment 1**

- *What I asked for:* I asked an AI chat assistant to write eight realistic r/LocalLLaMA posts that sit on the boundaries between my three labels, without telling me which label each was meant to be.
- *What came back:* Eight posts. I labeled all eight myself using only my definitions and decision rule, and I hesitated on seven of them. The hesitations clustered around three gaps: what counts as checkable, whether being set off by news makes a post a reaction, and vague gestures at evidence.
- *What I changed:* I added three rules under my decision rule: checkable means something a reader could look up or re-run, a post is labeled by its main claim, and being triggered by a release does not make a post a reaction.

**Moment 2**

- *What I asked for:*
- *What came back:*
- *What I changed:* I stopped treating those rows as my own cold labels. They are recorded as AI pre-labels, and I am reading each one and correcting the ones I disagree with.

**Pre-labelling disclosure:** All 182 rows in labels.csv were labeled by an AI coding assistant using my label definitions and decision rules. I did not review or correct them row by row, so the labels are unreviewed AI pre-labels. The note column marks them ai-prelabel. The model in results.json was trained on these labels.

<!-- ═══════════════════════ UNIT 6 — THE TEST ═══════════════════════

     Don't fill these in during unit 5.
     ═══════════════════════════════════════════════════════════════════ -->

---

## Baseline vs. Trained

<!-- Both models on the same posts. `python baseline.py --trained results.json`
     prints this table for you. -->

| Measure | Baseline | Trained | Difference |
|---|---|---|---|
| Overall accuracy | 0.286 | 0.571 | +0.286 |
| Macro F1 | 0.228 | 0.242 | +0.015 |
| F1 — `analysis` | 0.483 | 0.000 | -0.483 |
| F1 — `hot_take` | 0.000 | 0.727 | +0.727 |
| F1 — `reaction` | 0.200 | 0.000 | -0.200 |

**What I predicted before I looked:**
<!-- Milestone 1 asks you to write this BEFORE seeing the trained numbers. A
     prediction made afterwards isn't one. -->
I did not write a prediction before running the baseline, so I have no valid prediction to report.

**What the gap actually means:**
<!-- If the baseline matched your trained model, your fine-tuning added
     nothing — and that is a real finding, not a failure. Say it plainly. -->
The trained model's higher accuracy (0.571 against 0.286) comes entirely from predicting hot_take for every post, and 16 of the 28 test posts are hot_take. Its macro F1 is 0.242 against the baseline's 0.228, a difference of 0.015 that is within noise on 28 posts. The baseline gets some analysis and reaction posts right but scores 0.000 on hot_take. Neither model has learned the three-way distinction, and fine-tuning on 126 posts with 58% hot_take added almost nothing beyond majority-class guessing. Reaction has only 3 posts in the test split, so its scores can swing on a single post. Baseline and trained model were scored on the same test_split.csv, and the device was mps.



---

## Run Log — Before

<!-- Five criteria across three seeds. The notebook's section 6 prints the
     spread table; the Target and Verdict columns are yours. -->

| Criterion | Target | Seed 42 | Seed 7 | Seed 2024 | Verdict |
|---|---|---|---|---|---|
| 1. Overall accuracy | >= 0.65 | 0.571 | 0.571 | 0.571 | MISSED |
| 2. Every label F1 | >= 0.50 | 0.000 / 0.727 / 0.000 | 0.000 / 0.727 / 0.000 | 0.000 / 0.727 / 0.000 | MISSED |
| 3. Label balance in labels.csv | none above 50%, none below 25% | 58% / 32% / 10% | 58% / 32% / 10% | 58% / 32% / 10% | MISSED |
| 4. Agreement with staff | >= 21/30 | 30/30 | 30/30 | 30/30 | MET (see Agreement Report for caveats) |
| 5. analysis predicted as reaction | <= 25% | 0/9 = 0% | 0/9 = 0% | 0/9 = 0% | MET (vacuous) |

(F1 order in row 2 is analysis / hot_take / reaction. Row 3 order is hot_take / analysis / reaction.)

### Confusion matrix

<!-- ⚠️ TYPED AS A MARKDOWN TABLE. The notebook prints one ready to paste.
     An image of a matrix earns nothing. -->

| true \ predicted | analysis | hot_take | reaction |
|---|---|---|---|
| **analysis** | 0 | 9 | 0 |
| **hot_take** | 0 | 16 | 0 |
| **reaction** | 0 | 3 | 0 |

**My biggest off-diagonal number, and what it means:**
<!-- Not "the model made mistakes" — WHICH boundary it didn't learn, and which
     direction. "7 real analysis posts were called hot_take and only 3 went the
     other way" is a direction, not just an error rate. -->
9 analysis posts were called hot_take, and all 3 reaction posts went the same way. The model predicted hot_take for every one of the 28 test posts on all three seeds, so it never learned any boundary and its accuracy of 0.571 is just the hot_take share of the test split. The same matrix appeared on seeds 42, 7 and 2024, so the cause is the 58% hot_take share and the 18 reaction rows in the data, not the random split.



---

## Verdicts and Diagnoses

<!-- MET or MISSED against LAST UNIT's target. The target has to hold across
     all three seeds, not turn up sometimes. -->

| # | Criterion | Target | Verdict | How I decided |
|---|---|---|---|---|
| 1 |  |  |  |  |
| 2 |  |  |  |  |
| 3 |  |  |  |  |
| 4 | Agreement with staff | >= 21/30 | MET | 30 of 30 agreed with staff, above the target of 21. The staff labels in my_staff_labels.csv were assigned by an AI assistant, so this reflects the assistant's agreement on an easy, ordered set, not my own consistency. |
| 5 |  |  |  |  |

**Diagnoses**

<!-- For each miss: the cause, and how you know. The four common causes are:
     too few examples for a label, a boundary you applied inconsistently, a
     genuinely hard label pair, and a task the model can't reach from this
     much data.

     ⚠️ Use your agreement report as evidence. It is the only instrument you
     have that can tell a LABELLING problem from a MODEL problem, and this
     section is graded on whether you used it that way. -->



---

## Agreement Report

The 30 staff-set labels in my_staff_labels.csv were assigned by an AI coding assistant under the staff taxonomy, with my TA's confirmation that this was allowed. The assistant's labels came out in three blocks of ten in file order, which suggests staff_posts.csv is sorted by label, so the agreement rate may be inflated. The adjudications below are mine.

**Agreement rate:** 30 / 30 = 100%

<!-- Nobody grades this number. A 60% who argues every disagreement from the
     stated rules beats a 95% who wrote "staff was right" nine times. Several
     of the 30 were chosen because they're genuinely ambiguous — you should be
     winning some of these. -->

**Disagreements**

<!-- Three lines each: the post, both labels, and who you think is right and
     why — grounded in the staff definitions you were both applying.

     Then sort each into one of three piles:
       (a) the rule covered it and I applied it loosely → a consistency problem
       (b) the rule genuinely doesn't say               → a gap in the definitions
       (c) the rule is ambiguous here and my reading is defensible → argue it.
           This is a legitimate win.

     Pile (a) is the one that matters most for your diagnosis: if you applied a
     written rule two different ways on 30 posts, that is direct evidence about
     what you did across your own 200. -->
There were no disagreements, so there is nothing to adjudicate and I am not inventing any. data/staff_labels.csv was rebuilt with an id column from the staff label text so that agreement.py could match it to data/staff_posts.csv; all 30 texts matched exactly.

**1.**
> *The post:*
>
> *Staff said / I said:*
>
> *My call, and why:*
>
> *Which pile:*

**2.**
> *The post:*
>
> *Staff said / I said:*
>
> *My call, and why:*
>
> *Which pile:*

**What the pattern in my disagreements tells me:**
With no disagreements there is no pattern. This rate is weak evidence about my own labeling. The labels in my_staff_labels.csv were assigned by an AI assistant, not by me, so 30/30 shows the assistant applied the staff definitions the way staff did. The set is also sorted by label (posts 1 to 10 analysis, 11 to 20 hot_take, 21 to 30 reaction) and most posts are clear examples, so it was easy. The one deliberately hard post, sp_014, was labeled hot_take by both. This agreement check therefore cannot tell me whether my own 189 labels were applied consistently, and it does not separate a labeling problem from a model problem for my data.



---

## The Improvement

**What I changed:**
I added reaction examples, which is the "add examples to your thinnest label" option. reaction went from 18 rows to 25, so 7 rows were added. The added rows come from comments on news threads, were pre-labeled by an AI coding assistant using my definitions and decision rules, and are marked added-for-improvement in the note column of labels.csv. This is the only change in this unit. My labels, taxonomy and criteria are unchanged. I also removed 1 added row after checking it, because I could not trace it to its source.

**Which diagnosis pointed at it:**
My diagnosis for criteria 1, 2 and 3 was that hot_take is 58% of labels.csv and reaction only 10%, so the model learned to predict hot_take for every post on all three seeds. reaction was the thinnest label, with 18 rows and only 3 posts in the test split.

Caveats on this comparison:
1. The "after" test split differs from the "before" split, because adding rows changes the random split, so the two runs are not scored on identical posts.
2. The added rows are short and come from news threads, so the model could learn length or topic instead of the reaction label.
3. The word floor for these added reaction rows was 6 words, while the rest of the data used a floor of 12.

### Run Log — After

| Criterion | Target | Seed 42 | Seed 7 | Seed 2024 | Verdict |
|---|---|---|---|---|---|
| 1. Overall accuracy | >= 0.65 | 0.552 | 0.552 | 0.552 | MISSED |
| 2. Every label F1 | >= 0.50 | 0.000 / 0.711 / 0.000 | 0.000 / 0.711 / 0.000 | 0.000 / 0.711 / 0.000 | MISSED |
| 3. Label balance in labels.csv | none above 50%, none below 25% | 56% / 31% / 13% | 56% / 31% / 13% | 56% / 31% / 13% | MISSED |
| 4. Agreement with staff | >= 21/30 | 30/30 | 30/30 | 30/30 | MET (see Agreement Report for caveats) |
| 5. analysis predicted as reaction | <= 25% | 0/9 = 0% | 0/9 = 0% | 0/9 = 0% | MET (vacuous) |

(F1 order in row 2 is analysis / hot_take / reaction. Row 3 order is hot_take / analysis / reaction, from 189 rows: 106 / 58 / 25.)

**Did it help, and how do I know:**

<!-- If it didn't, say so. Relabelling that didn't help is a genuinely
     interesting result and earns full credit. -->
No. After adding 7 reaction examples (reaction went from 18 to 25 rows), the model still predicted hot_take for every test post on all three seeds, and the confusion matrix showed the same pattern as the before run: all 9 analysis, 16 hot_take and 4 reaction test posts were predicted as hot_take (the before run had 3 reaction posts in its test split). Accuracy moved from 0.571 to 0.552 and macro F1 from 0.242 to 0.237, but that is because the test split changed (16 hot_take posts out of 29 instead of 28), not because the model changed. 7 added rows is too small a change for a label with about 25 examples out of 189, and hot_take is still 56% of the data. The "after" test split also differs from the "before" split, so the two runs are not scored on identical posts.



---

## What's Still Broken

<!-- For each criterion still missed: what you'd do, and why you stopped. -->
Criterion 3 (label balance) is still missed. After the improvement, labels.csv has 189 rows: hot_take 106 (56%), analysis 58 (31%) and reaction 25 (13%). hot_take is still above the 50% cap and reaction is far below the 25% floor. Getting reaction to 25% would take roughly 30 more reaction rows. I stopped because the reaction comments I could collect were rare and short: only 8 of roughly 250 comments across three threads qualified, and the word floors filter many short reactions out. Criterion 4 (agreement with the staff labels) was met at 30 of 30, but the staff-set labels were assigned by an AI assistant on an easy, label-sorted set, so it says little about the consistency of my own labels.

**The gap between what I meant my labels to capture and what the model
learned:**
<!-- Two sentences. Your confusion matrix is the evidence. -->
I meant the labels to separate claims backed by checkable evidence (analysis), unsupported verdicts (hot_take) and feeling-driven responses to news (reaction). In the "before" run the confusion matrix shows the model learned none of that: it predicted hot_take for all 28 test posts on all three seeds, so 9 analysis posts and 3 reaction posts were called hot_take. What it picked up was the label frequency (58% hot_take), not the boundaries. The after run gave the same pattern on all three seeds, with every post predicted as hot_take, so adding 7 reaction examples did not change what it learned.

Criteria 1 and 2: I would rebalance the data so no label dominates, with substantially more reaction and analysis rows or fewer hot_take rows, and then see whether the model leaves one-label guessing, before touching any training setting. I stopped because this unit allows one change, and collecting reactions was slow. Criterion 5: it is met only because the model never predicts reaction, so it says nothing yet about the analysis versus reaction boundary, and it only becomes meaningful once the model predicts reaction at all.

<!-- ═════════════════════════════════════════════════════════════════════

     SUBMISSION CHECKLIST — unit 5

       [ ] criteria.md has five numbered criteria, each naming a NUMBER
       [ ] Each has a reason underneath tied to your data or taxonomy
       [ ] labels.csv: at least 150 rows, text/label/note, ONE file not split
       [ ] No label above 70%
       [ ] All five unit 5 sections have real content
       [ ] Label Taxonomy includes the decision rule for your hardest boundary
       [ ] The Dataset includes three hard cases
       [ ] results.json and test_split.csv committed (the notebook does this)
       [ ] At least four new commits
       [ ] Repository URL submitted — WRITE IT DOWN

     SUBMISSION CHECKLIST — unit 6

       [ ] Baseline vs. Trained table, with your prediction written beforehand
       [ ] Run Log — Before, five criteria across three seeds
       [ ] Confusion matrix TYPED AS A MARKDOWN TABLE
       [ ] A verdict on every criterion
       [ ] A diagnosis for every miss, using the agreement report as evidence
       [ ] Agreement Report with every disagreement adjudicated
       [ ] One improvement, with Run Log — After
       [ ] What's Still Broken
       [ ] results_three_seeds_before.json, results_three_seeds_after.json,
           baseline_results.json and
           agreement_results.json committed
       [ ] At least four new commits
       [ ] The SAME repository URL as last unit

     Do not delete and recreate this repository.
     ═════════════════════════════════════════════════════════════════════ -->

---

📖 **How to run this project: [RUNNING.md](RUNNING.md)**
