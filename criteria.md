# Acceptance criteria — TakeMeter

Five criteria that say what "working" means for this classifier, written in
unit 5 **before** anything was trained.

**All five are yours this time.** None are given. You've had two projects of
practice.

An acceptance criterion names a number. *"The model is accurate"* is an
opinion. *"Every label has an F1 of at least 0.60 on the held-out set"* is a
criterion.

Under each, write a sentence or two on **why that number**. A reason that says
something about your data or your taxonomy earns credit — *"I picked 0.60 F1
for `reaction` because it's my smallest label and I only have about 50
examples of it"*. A reason that could be attached to any project does not.

> Missing your own targets next unit costs you nothing. Setting a target so
> easy you can't miss it does.

---

## Pick numbers you can defend

Not numbers that sound impressive. Three labels means a coin-flip guesser gets
about 33%, so a target of 0.40 is barely a target. Your number should sit
somewhere you'd honestly call useful.

**Cover at least three of these five areas.** They're here as prompts, not as a
form to fill in — a criterion that fits none of them is fine if it names a
number.

| Area | A question it could answer |
|---|---|
| Overall accuracy | How often does it need to be right to be worth using? |
| Per-label performance | Is one label allowed to be much worse than the others? |
| Balance | How lopsided can your label counts get before it's a problem? |
| Consistency | If someone else labelled the same posts, how often should you agree? |
| Confidence | Should a confident prediction be right more often than an unsure one? |

Two things worth knowing before you pick numbers, because both will affect
whether you hit them:

- **Your smallest label will have the jumpiest score.** If a label has 50
  examples, about 8 land in the test split. An F1 computed on 8 examples moves
  a lot between seeds. A target for that label should be looser than one for
  your biggest label, and saying so is a good reason.
- **Unit 6 tests across three seeds, and the target has to hold across all
  three.** A target of 0.65 against results of 0.71, 0.62, 0.68 is a **miss**.
  Pick with that in mind — it is stricter than it first sounds.

---

## 1.

<!-- Your criterion. It must name a number. -->

Overall accuracy on the held-out test split is at least 0.65 on each of the three seeds (42, 7, 2024), as reported in results_three_seeds_before.json.

**Why this target:** Criterion 3 caps my largest label at 50% of labels.csv. Because the split is stratified, that label is also about 50% of each test split, so a model that always predicted it would score about 0.50. 0.65 requires the model to get a real share of the other two labels right, not just lean on the biggest one. I didn't go higher because the test split is only 15% of ~200 posts (about 30), so one post is worth over 3 points of accuracy, and the target has to hold on all three seeds.

---

## 2.

<!-- Your criterion. -->

Every label (analysis, hot_take, reaction) has an F1 of at least 0.50 on the held-out test split, on each of the three seeds, as reported under per_label in results_three_seeds_before.json.

**Why this target:** analysis posts usually carry numbers, model names or hardware, and reaction posts carry feeling words. hot_take has neither, so it is the label most likely to be absorbed by the other two. This is set looser than criterion 1 because at the 25% floor in criterion 3, hot_take has about 50 rows, so only about 8 land in a 15% test split. On 8 posts, one wrong call moves F1 a lot between seeds.

---

## 3.

<!-- Your criterion. -->

In labels.csv, no label is more than 50% of rows and no label is fewer than 25% of rows.

**Why this target:** In community_notes.md, most posts I read had no numbers at all, so analysis is the label I'll have to search for, while reaction posts come up in every news cycle. Left alone, the file would skew toward reaction. The 25% floor keeps every label at about 50 rows or more in a 200-row file, which is what criterion 2's 8-in-test estimate depends on.

---

## 4.

<!-- Your criterion. -->

My agreement with the staff labels on the 30 staff posts is at least 21/30 (70%), as reported by the "agreed" count in agreement_results.json.

**Why this target:** These 30 posts are labeled under data/staff_taxonomy.md, not my own rules, so this measures whether I apply a written rule the way its authors meant it. My own taxonomy needed three extra rules after an 8-post stress test, which shows how easily a boundary rule leaves room for different readings. 70% means I agree on at least 21 posts, and allows for the posts in the set that were chosen to be ambiguous.

---

## 5.

<!-- Your criterion. -->

On each of the three seeds, no more than 25% of gold-analysis test posts are predicted as reaction. For each seed, take the "confusion" field in results_three_seeds_before.json and divide the (true analysis, predicted reaction) count by the total of the analysis row.

**Why this target:** This is the boundary my decision rule exists for: numbers that support a claim versus numbers that are context for a feeling. On r/LocalLLaMA, both kinds of post are full of tok/s figures, prices and GPU names, so a model that keys on "has numbers" will blur them. More than 1 in 4 analysis posts going to reaction would mean it learned that surface cue instead of my rule.

---

<!-- ─────────────────────────────────────────────────────────────────────────
     UNIT 6 — read this before you change anything above.

     If a criterion turns out to be BROKEN rather than merely unmet, you can
     revise it, and that earns credit. But never delete or edit the original
     line. Add the revision underneath, like this:

         ## 2. Every label performs acceptably

         The model performs well on all labels.

         **Why this target:** ...

         > **Revised in unit 6:** Every label has an F1 of at least 0.60 on
         > the held-out set.
         >
         > **Why revised:** "performs well" gave me nothing to check. I
         > couldn't produce a verdict from it at all.

     That's a revision because the criterion couldn't be MEASURED.

     Lowering a target because you missed it is not a revision, and it costs
     you the point:

         ✗ "Overall accuracy of at least 0.65" → "at least 0.55", because
            0.65 turned out to be optimistic for 200 examples.

     A number you missed stays where it is, gets diagnosed, and gets a fix
     attempted. That's where the points are.
     ───────────────────────────────────────────────────────────────────────── -->
