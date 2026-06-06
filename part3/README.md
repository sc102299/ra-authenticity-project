# Part 3 Organizational Authenticity

## What I did

For Part 3, I created an alignment index that compares what companies say they value in public-facing webpages with what they emphasize in formal disclosure documents. I used the Part 1 stated-values data from archived About / Mission / Values pages and the Part 2 proxy statement disclosure data. The idea was to measure whether the themes a company uses to describe itself publicly are similar to the themes that appear in its SEC proxy statements.

The final output file is: `data/part3_authenticity_index.csv`

The final Part 3 dataset has 138 company-year observations and 22 columns. These are the company-years where both usable Part 1 stated-values text and usable Part 2 proxy disclosure data were available.

I define the `authenticity_index` as a text-based alignment score from 0 to 100. A higher score means the company’s stated-values themes are more similar to the themes emphasized in its proxy disclosure. A lower score means the two sources are less aligned.

The average authenticity index in this dataset is about 82.54. The median is about 84.39. The lowest score is 0 and the highest score is about 98.92.

## Why I did it this way

The goal of this part was to turn the comparison between Part 1 and Part 2 into a measurable index. Part 1 captures public-facing stated values. These are the values companies choose to present on About, Mission, Values, or similar pages. Part 2 captures formal disclosure priorities. Proxy statements are not the same as company behavior, but they show what companies repeatedly discuss in official governance documents. I used alignment between these two sources as a practical way to approximate “authenticity.” This does not prove whether a company is truly authentic. It only measures whether the company’s public values language and formal disclosure language point in similar directions. To make the comparison possible, I mapped related themes from Part 1 and Part 2 into five broader categories:

* people
* diversity
* sustainability / social impact
* governance / trust / risk
* growth / strategy

For Part 1, the themes were binary indicators based on whether each theme appeared in the stated-values page. For Part 2, I used normalized disclosure measures from proxy statements. I then scaled the Part 2 measures and calculated cosine similarity between the Part 1 and Part 2 vectors. I multiplied the similarity score by 100 to create the final `authenticity_index`.

## Assumptions

I made several assumptions in this part:

1. Public-facing About / Mission / Values pages are a reasonable source for stated company values.
2. Proxy statements are a reasonable source for formal disclosure priorities.
3. Alignment between these two text sources can be used as a proxy for organizational authenticity.
4. The five broad theme categories are enough for a first-pass comparison.
5. Cosine similarity is an appropriate way to compare the Part 1 and Part 2 theme vectors.
6. A higher score means stronger textual alignment, not necessarily better real-world behavior.
7. Company-years without usable data from both Part 1 and Part 2 should not be included in the index.

## What I would do differently with more time

With more time, I would improve the theme mapping. Right now, I manually mapped Part 1 and Part 2 themes into five broader categories. This is reasonable for a proof of concept, but I would want to test whether the categories make sense using manual review or an LLM-based coding step.

I would also improve coverage. The final index only includes 138 company-year observations because many company-years were missing usable Part 1 text, Part 2 data, or both. With more time, I would go back and improve missing data by testing alternative About page URLs, using more targeted Wayback searches, and checking SEC filings more carefully.

I would also add a stronger validity check. In this version, I inspected the highest- and lowest-scoring examples to see whether the scores looked reasonable. With more time, I would compare the index against an external benchmark, such as ESG ratings, controversy data, employee ratings, or manually coded examples.

## Limitations

The biggest limitation is that this index measures textual alignment, not actual company behavior. A company can have a high score because its public webpage and proxy statement use similar language, but that does not prove the company acts consistently with those values.

Another limitation is missing data. The final Part 3 dataset has 138 company-year observations, which is much smaller than the original 450 company-year target from Part 1. The index is only calculated where both Part 1 and Part 2 data are available. The theme categories are also simplified. For example, “governance / trust / risk” combines several related but different ideas. This makes the index easier to calculate, but it also loses detail. The score can also be affected by keyword choices from earlier parts. If a theme was overcounted or undercounted in Part 1 or Part 2, the alignment score may reflect that coding choice rather than a real difference in company messaging.

Finally, sector differences may affect the score. Energy companies had relatively high average scores in my results, while Technology had lower average scores. This may partly reflect real differences in disclosure patterns, but it may also reflect how well the selected theme categories fit each sector.