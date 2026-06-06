





# Part 4 Additional Analysis: Do Values Page Changes Relate to Alignment?

## What I did

For Part 4, I proposed an additional analysis based on the authenticity index from Part 3. I wanted to see whether companies whose stated-values pages changed from the prior available year had different authenticity index scores than companies whose pages stayed relatively stable.

The question was: **Do changes in a company’s public-facing values page relate to stronger or weaker alignment with formal proxy statement disclosures?**

I used the Part 3 dataset: `data/part3_authenticity_index.csv`

This file already includes the authenticity index and the `changed_from_prior` label from Part 1.

I compared authenticity index scores across three groups:

* `changed`
* `not_changed`
* `no_prior_available`

The main comparison was between `changed` and `not_changed`, since `no_prior_available` does not really tell whether the company changed its page.

## Why I did this analysis

I chose this analysis because it tests something interesting about the index. If a company changes how it talks about its values on its website, that change might mean the company is updating its public identity. One possibility is that updates make the website more aligned with formal disclosures. Another possibility is that website changes are more like rebranding and do not necessarily match what the company emphasizes in official documents. This makes the analysis useful as a small validity check for the Part 3 measure.

## What I found

In the full comparison, the `not_changed` group had 96 observations and an average authenticity index of about 83.61. The `changed` group had 30 observations and an average score of about 80.83. The `no_prior_available` group had 12 observations and an average score of about 78.27.

When I compared only `changed` and `not_changed`, the difference was small. The median score for changed pages was about 84.59, while the median for not-changed pages was about 84.20. This means the average was lower for changed pages, but the typical score was very similar across the two groups. The sector breakdown showed that the pattern was not the same in every sector. In Energy, changed pages had a higher average score than not-changed pages. In Consumer Discretionary, changed pages also had a slightly higher average score. In Technology, changed pages had a lower average score. Healthcare had only 2 changed observations, so I would not overinterpret that comparison.

I also looked at examples. Some changed pages had very high alignment scores, including Marathon Petroleum, Valero Energy, Thermo Fisher Scientific, McDonald’s, Tesla, and Amazon. Some changed pages had lower alignment scores, including NVIDIA, Intel, Amazon, Microsoft, and Tesla in other years.

## Assumptions

I made the following assumptions:

1. The `changed_from_prior` label is a reasonable first-pass signal of whether a company updated its stated-values page.
2. The authenticity index from Part 3 is a reasonable measure of textual alignment between stated values and proxy disclosure priorities.
3. Comparing average and median scores across change groups can show whether website changes are associated with stronger or weaker alignment.
4. The results should be interpreted descriptively, not causally.

## What I would do differently with more time

With more time, I would inspect the actual page text before and after a change. Right now, the analysis only uses the change label and the authenticity score. Reading the pages would show whether the change was a real values update or just a layout/template change. I would also run a more formal statistical test with controls for sector and year. The current version is exploratory and the sample sizes are small in some groups. I would also separate different types of changes. For example, adding diversity language, adding sustainability language, and changing website layout are very different things, but they are all grouped as `changed` in this version.

## Limitations

The biggest limitation is that `changed_from_prior` is based on text similarity. A page can be marked as changed because of formatting, navigation text, or template updates, not necessarily because the company changed its values language. The sample is also small after merging Part 1 and Part 2. There are only 30 changed observations in this analysis, and some sectors have very few changed cases. Another limitation is that this analysis is descriptive. It does not prove that changing a values page causes the authenticity index to rise or fall. Finally, the authenticity index itself is based on keyword and theme mappings from earlier parts. If those mappings miss important language, the Part 4 results will also be affected.