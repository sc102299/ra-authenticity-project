# Part 1 — Stated Values from Archived About Pages

## What I did

For Part 1, I collected archived versions of company About, Mission, Values, Purpose, or similar pages using the Wayback Machine. The sample includes the 50 companies from the assignment across five sectors. For each company, I selected one official company webpage that seemed closest to an About or values page. I tried to collect one archived snapshot per company per year from 2016 through 2024, using July 1 as the target date for each year. After collecting snapshot links, I downloaded the archived pages when available, extracted visible page text, cleaned the text, compared each page with the prior available year, and assigned broad value-theme categories.

The main output file is: `data/part1_company_year_values.csv`

Intermediate files include: 
`data/snapshots_metadata.csv`
`data/part1_text_extracted.csv`

The final dataset has 450 company-year rows. Out of these, 242 had Wayback snapshots and 208 were missing. After text extraction, 226 rows had usable cleaned text, 208 were missing snapshots, and 16 were found snapshots where the extracted text was too short or unusable.

For the main structured dataset, I used keyword-based theme coding. I also added a separate notebook, `part_1AI.ipynb`, for an LLM-assisted annotation step. The purpose of that notebook is to show how cleaned page text could be passed into an LLM to classify value themes, compare the current page with the prior year, and generate linguistic-shift notes. I attempted to run this LLM-assisted step, but the API call could not be completed because my OpenAI API account did not have active billing / available quota. Because of that, I do not treat LLM outputs as part of the final results. Instead, the submitted Part 1 dataset relies on the keyword-coded results, and the LLM notebook is included as a supplemental pipeline design for improving the analysis.

## Why I did it

The goal of Part 1 is to measure companies’ stated values over time. About, Mission, Values, Purpose, and similar pages are useful for this because they are public-facing pages where companies describe who they are and what they claim to care about. I used the Wayback Machine because the assignment asks for historical snapshots from 2016 through 2024. I used July 1 as the target date so that every company-year followed the same selection rule instead of choosing dates manually.

I first tried to use the CDX API, but it often timed out or returned 503 errors. I switched to the Wayback Availability API because it was more stable for collecting one representative snapshot per company-year. This choice helped me build a usable proof-of-concept dataset, although it also limited the amount of control I had over exact snapshot selection. For theme coding, I used a keyword-based method because it is transparent, reproducible, and easy to inspect. Since this project later uses the Part 1 output to construct an authenticity measure, I wanted the coding method to be simple enough to understand and audit. The LLM-assisted notebook was added because keyword rules alone do not fully capture language shifts, framing, or context.

## Assumptions

I assumed that the selected About, Mission, Values, Purpose, or similar page is a reasonable proxy for each company’s stated values. This is not perfect, because companies may communicate values across multiple pages, but it gives a consistent starting point.

I assumed that one snapshot per year is enough for this proof of concept. A company page may change multiple times within a year, but this version treats one annual snapshot as representative.

I used July 1 as the annual target date. This is an arbitrary but consistent rule, and it avoids manually choosing more favorable snapshots. I kept missing snapshots in the dataset rather than dropping them. I did this so that the final file preserves the full 50-company by 9-year structure, even when Wayback data was unavailable or unusable. I treated a page as changed if its cleaned text similarity with the prior available page was below 0.90. This is a practical rule for detecting large text changes, but it may miss smaller wording changes or overstate changes caused by noisy extraction.

I assumed that keyword-based theme categories can provide a first-pass measure of values language. This method does not fully capture context, but it makes the coding process easier to review.

## What I would do differently with more time

With more time, I would improve coverage by testing older or alternative URLs for companies with few or no usable snapshots. Some companies may have changed their About page URLs over time, so using only one modern URL may miss older archived pages.

I would also use a more targeted CDX search for missing company-years instead of relying mainly on the Availability API. A CDX-first approach with fallback rules would give more control over snapshot selection and make the collection process closer to the original assignment instructions. For text extraction, I would spend more time removing navigation, footer text, cookie banners, and repeated boilerplate. Some archived pages still contain noisy text even after cleaning. For text analysis, I would run the LLM-assisted annotation step on all usable company-year snapshots. The LLM step would be especially useful for identifying linguistic shifts, such as whether a company moved from general mission language to more specific language about sustainability, employees, innovation, or social impact. I would then compare the LLM-coded themes with the keyword-coded themes to check whether the simpler keyword method misses important patterns.

## Limitations

The biggest limitation is missing data. Many company-year rows did not have usable archived text. A missing page does not necessarily mean the company did not have an About or values page in that year. It only means my collection method did not return usable text for that company-year.

Another limitation is URL selection. A URL that works today may not have existed in the same form in 2016. Some companies may have moved their mission or values language across different parts of their website over time.

The Wayback Availability API also has limitations. It was more stable than my CDX attempt, but it gives less control over the exact snapshot search process. This may affect which archived page was selected for a given company-year. The cleaned text may still contain some noise from menus, footers, cookie notices, archived webpage formatting, or repeated website language. This can affect both change detection and theme coding. The theme categories are based mainly on keyword counts. This makes the method easy to explain, but it does not fully capture context or tone. For example, a company may mention “sustainability” briefly or repeatedly, but keyword counts alone do not show how meaningful or central that theme is.

Finally, the LLM-assisted annotation step is included as a supplemental pipeline design rather than a completed full annotation layer. I attempted to run the LLM step, but the API returned a quota/billing error, so I could not generate LLM annotations for the full dataset. Because of this, I do not use LLM results as the main evidence in the final Part 1 dataset. In a fuller version, I would run the LLM annotation on all usable snapshots and compare the LLM-coded themes with the keyword-coded themes.