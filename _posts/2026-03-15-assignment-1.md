---
title: "Rowling Wrote a War Story. Did Fanfiction Turn It Into a Love Story?"
date: 2026-03-15
categories: [Assignments]
tags: [Assignments, Corpora, Voyant Tools, R, S26, Harry Potter]
toc: true
toc_label: "Contents"
---

## Section 1: Corpus and Research Questions

The Harry Potter series is, at its core, a war story. Across seven books, J.K. Rowling builds a world defined by conflict, institutional power, and sacrifice. Harry Potter does not get to have a quiet life. He loses people, faces death repeatedly, and spends most of his adolescence fighting a genocidal enemy. The emotional register of the series — especially by its later books — is one of danger, darkness, and loss.

Fanfiction writers take the same characters and the same world, but they often do something different with them. Reading through the Archive of Our Own corpus provided for this course, a pattern keeps surfacing: fanfic writers seem drawn to what Rowling denied her characters. Home. Safety. Romance. The question I wanted to investigate computationally is whether that instinct actually shows up in the language — whether fanfiction systematically trades conflict vocabulary for domestic and romantic vocabulary, and whether that shift is measurable across texts.

My corpus consists of five texts: two by Rowling — *Harry Potter and the Sorcerer's Stone* (1997) and *Harry Potter and the Deathly Hallows* (2007) — and three fanfictions drawn from the course's AO3 collection. The fanfics are *Resurrection* by Sugahhuney (64,822 words), a close-to-canon fix-it fic in which Harry dies at the Battle of Hogwarts and wakes up in 1991 with the chance to do it all again; *Reconstructing Harry Potter* by yellowsunchild (23,875 words), a post-war story centered on Harry and Draco rebuilding Hogwarts together and falling for each other; and *Harry Potter: Djinn Awakened* by Invaderdoom (107,151 words), a high-divergence AU in which Harry discovers he is a Djinn rather than a wizard.

I chose Sorcerer's Stone and Deathly Hallows deliberately because they represent the two poles of Rowling's own arc — the lightest book and the darkest. If conflict vocabulary increases within Rowling's own series from Book 1 to Book 7, that establishes a baseline against which to compare fanfiction. The three fanfics were chosen to give a range: one that stays close to canon, one that centers a romantic relationship, and one that diverges from the HP universe almost entirely.

My research questions are:

1. Does conflict vocabulary (battle, death, dark, fear, danger) peak in Rowling's later work and decline in fanfiction?
2. Does domestic vocabulary (family, home, safe, smile, comfort) rise in fanfiction relative to canon?
3. Does romantic vocabulary (love, kiss, heart, eyes, touch) increase in fanfiction, and does it do so consistently across all three fics or only in the explicitly romantic ones?

These questions work well for computational analysis because the patterns I am looking for are distributed across tens of thousands of words. Close reading a few chapters would not tell me much about distribution. Distant reading lets me look at the whole corpus at once.

---

## Section 2: Analysis and Findings

For this analysis I used two methods: Voyant Tools for exploratory text analysis and visualization across the full corpus, and RMarkdown notebooks in Posit Cloud for word cloud and heatmap generation. Both methods were run on the same five texts.

You can explore the full corpus interactively below:

<iframe style='width: 100%; height: 800px;' src='https://voyant-tools.org/?stopList=keywords-c29f32a34f3c62b53c4f29c5ae44566d&panels=cirrus%2Creader%2Ctrends%2Csummary%2Ccontexts&corpus=89ae5e77b931d3ca54e250600eaa519a'></iframe>

![Voyant Tools dashboard showing all five texts loaded](/rlac/assets/images/posts/dashboard-voyant.png)
*The full corpus loaded in Voyant Tools: two Rowling texts and three AO3 fanfictions, 473,299 total words.*

### Conflict Vocabulary (RQ1)

Tracking conflict vocabulary across the five texts produced the clearest result of the analysis. In the Voyant Trends chart (Figure 1), Deathly Hallows dominates almost every conflict term. "Death*" peaks sharply at around 0.0018 relative frequency — the highest bar in the entire conflict chart. "Dark*" and "protect*" also peak in Deathly Hallows. Sorcerer's Stone sits low across all conflict terms, which is expected.

The fanfics cluster in the middle, but not uniformly. Sugahhuney's *Resurrection* shows elevated "dark*" relative to Sorcerer's Stone, which makes sense given that the fic opens with Harry dying and replays canon events with full awareness of what is coming. Invaderdoom shows moderate conflict vocabulary throughout. The most surprising result is yellowsunchild's *Reconstructing HP*, which has a notable spike in "battle*" — higher than Sorcerer's Stone and comparable to some of the fanfics. This complicates a clean narrative about fanfic domesticating conflict entirely, and I will return to it in the critical reflection.

![Conflict vocabulary bar chart across five texts](/rlac/assets/images/posts/conflict-voyant.png)
*Figure 1: Conflict vocabulary relative frequencies across all five texts. Deathly Hallows dominates on death\* and dark\*.*

The heatmap generated in R (Figure 2) confirms and extends these findings. Deathly Hallows has raw counts of 306 for "death," 194 for "dark," 54 for "fear," and 25 for "battle" — by far the darkest column in the visualization. Sugahhuney has 28 for "death" and 61 for "dark," still present but significantly lower. yellowsunchild has only 3 for "death" and 7 for "dark," and 15 for "battle" — the battle count is notable and warrants closer reading.

![R heatmap of word frequencies across five texts](/rlac/assets/images/posts/r-heatmap.png)
*Figure 2: Word frequency heatmap generated in R showing conflict, domestic, and romantic vocabulary across all five texts.*

### Domestic Vocabulary (RQ2)

The domestic vocabulary chart (Figure 3) is where the thesis starts to hold most clearly. Both Sugahhuney and yellowsunchild show dramatically elevated "smile*" and "family*" bars compared to either Rowling text. Sugahhuney's "family*" relative frequency is the highest single bar in the entire domestic chart. In the heatmap, Sugahhuney scores 81 on "family" — higher than Deathly Hallows's 77 despite being less than a third of the length.

This finding is particularly striking given what *Resurrection* is actually about. The fic follows Harry as he relives his Hogwarts years with full knowledge of his future, and the emotional center shifts from defeating Voldemort to building the relationships and family structures he was denied the first time. The frequency data reflects that recentering directly.

Rowling's two books score low on almost all domestic vocabulary. "Home*" appears in Deathly Hallows (52 in the heatmap) but the Contexts tool in Voyant reveals these are largely references to Grimmauld Place as a hideout or the Dursleys' house as a site of confinement — not home as warmth or belonging. In the fanfics, the Contexts panel shows "home" appearing in sentences about Harry wanting to stay somewhere, feeling like he belongs, or being held by someone. Same word, completely different emotional function.

![Domestic vocabulary bar chart across five texts](/rlac/assets/images/posts/domestic-voyant.png)
*Figure 3: Domestic vocabulary relative frequencies. Sugahhuney's family\* count exceeds even Deathly Hallows.*

### Romantic Vocabulary (RQ3)

The romance chart (Figure 4) produces the clearest split between the two fanfics and the two Rowling texts. yellowsunchild spikes hard on "eyes*" — 59 in the heatmap, with the highest "kiss" count in the entire corpus at 20. Sugahhuney also rises on "love*" at 34. Rowling's books have "eyes*" present — Deathly Hallows scores 328, the darkest cell in the entire heatmap — but the Contexts tool shows these are almost entirely references to Voldemort's red eyes, Harry watching enemies, or surveillance. In yellowsunchild, "eyes" appears in sentences like "Harry's eyes met Draco's across the room" — it is doing entirely different work.

The "kiss" distribution is the starkest finding in the romance cluster. yellowsunchild has 20, Sugahhuney has 9, Invaderdoom has 8, Sorcerer's Stone has 3, and Deathly Hallows has only 4. The two explicitly romantic fanfics contain more kissing than the entire final book of a seven-part series.

![Romance vocabulary bar chart across five texts](/rlac/assets/images/posts/romance-voyant.png)
*Figure 4: Romantic vocabulary relative frequencies. yellowsunchild spikes on eyes\* and kiss\*.*

### Word Clouds

The side-by-side R word clouds (Figure 5) provide a visual summary of the register differences across the four texts. Deathly Hallows: "harry," "hermione," "ron," "voldemort," "death," "wand," "dumbledore" — a war story cast list with death sitting prominently in the middle. Sorcerer's Stone: "harry," "hermione," "ron," "hagrid," "professor," "snape" — institutional, school-heavy, no darkness. Sugahhuney: "harry," "family," "dark," "eyes," "son," "school" — the word "family" is prominent in a way it never is in Rowling. yellowsunchild: "harry," "draco's," "kiss," "sleep," "room," "hands" — intimate, physical, relational vocabulary that simply does not appear in the Rowling word clouds.

![Side by side R word clouds for four texts](/rlac/assets/images/posts/r-wordclouds.png)
*Figure 5: Word clouds generated in R for Deathly Hallows, Sorcerer's Stone, Sugahhuney Resurrection, and yellowsunchild Reconstructing HP.*

The summary panel from Voyant adds a useful quantitative note: yellowsunchild has the highest vocabulary density of the fanfics (0.130) while Deathly Hallows has the lowest (0.059). The shortest, most character-focused fanfic is also the most lexically varied.

![Summary chart showing love home and battle across five texts](/rlac/assets/images/posts/summary-chart.png)
*The three-register summary: love\*, home\*, and battle\* across all five texts in a single view.*

---

## Section 3: Critical Reflection

The data largely supports the thesis, but with enough complications to make the interpretation interesting.

The clearest finding is the domestic shift in Sugahhuney's *Resurrection*. The "family" frequency is higher than in Deathly Hallows despite the fic being a fraction of the length. What is happening there is not subtle: the fic is explicitly a therapeutic rewrite of Harry's story, one that asks what would happen if Harry got to build the relationships Rowling kept interrupting with plot. The frequency data captures that impulse directly.

The romantic shift in yellowsunchild is also clear. "Kiss" at 20, "eyes" functioning as intimacy rather than surveillance, "draco's" as a dominant word in the cloud — this is a text that has recentered the HP universe around a relationship. Ted Underwood, in the chapter "The Risks of Distant Reading" from *Distant Horizons*, warns that frequency analysis can flatten meaningful distinctions by treating all instances of a word as equivalent. The "eyes" finding is a good example of this risk in action: the raw count for "eyes" in Deathly Hallows (328) is far higher than in yellowsunchild (59), but the word is doing completely different work in each text. Without the Contexts tool to check the surrounding sentences, I would have concluded that Rowling uses more romantic language than the fanfic writer, which is exactly backwards.

The complication is yellowsunchild's "battle" count of 15. This is higher than Sorcerer's Stone and sits alongside the romantic vocabulary, not instead of it. Reading the actual text explains this: *Reconstructing HP* is set immediately after the Battle of Hogwarts, and the war is not absent — it is the wound the characters are healing from. The conflict vocabulary does not disappear; it becomes the backdrop against which the domestic and romantic vocabulary does its work. This suggests that the relationship between these registers in fanfiction is not simply a replacement but a reframing: fanfic does not erase the war, it makes the war the reason the characters deserve softness.

The Invaderdoom fic is the hardest to interpret within the thesis. Its conflict vocabulary is moderate and its domestic and romantic vocabulary is also moderate, without strong peaks in either direction. Looking at the word cloud, the reason becomes clear: the dominant words are "harry," "greg," "djinn," "magic," "wish" — a vocabulary drawn from an entirely different genre. This fic has not domesticated or romanticized the HP universe so much as replaced it with a different genre entirely, retaining Harry as a character while discarding almost all of the canonical world-building. Its presence in the corpus as a kind of null result is itself interesting: it suggests that the domestication hypothesis works best for fics that stay in conversation with the source text, and breaks down for fics that have effectively left it behind.

There are real limitations to this analysis worth naming. The corpus is small — five texts, two of which are by the same author. Drawing conclusions about "fanfiction" as a category from three fics is risky, as Kestemont and Herman note in "Can Computers Read Literature?" when they caution against treating computational findings as representative claims about a genre. A larger study would need dozens of fanfics across different ratings, pairings, and genres to say anything more general. The custom word lists I built for each cluster also reflect my own assumptions about what conflict, domestic, and romantic vocabulary look like. Words like "safe" appear in both domestic and conflict contexts — being safe from danger is not the same as feeling safe at home — and frequency analysis cannot make that distinction without the Contexts tool.

What I would explore next is sentiment analysis at the sentence level rather than word frequency at the corpus level. The aggregation across whole texts smooths over a lot. Sugahhuney's fic alternates between scenes of warmth and scenes of Harry reliving trauma — a story-level analysis might reveal patterns that the collection-level data obscures. It would also be worth running this same analysis across a much larger fanfic sample, stratified by genre tag, to test whether the domestication pattern holds across the AO3 corpus more broadly or whether it is specific to the fix-it and romance subgenres I happened to select.

---

*All analysis conducted using Voyant Tools and RMarkdown notebooks in Posit Cloud. Rowling texts sourced from course materials. Fanfiction texts sourced from Archive of Our Own via course corpus. References: Underwood, Ted. "The Risks of Distant Reading." Distant Horizons. University of Chicago Press, 2019. Kestemont, Mike and Karina van Dalen-Oskam. "Can Computers Read Literature?" Journal of Data Mining and Digital Humanities, 2019.*

READY FOR GRADING