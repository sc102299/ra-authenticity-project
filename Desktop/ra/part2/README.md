# Part 2 — Lived Values: Proxy Disclosure Analysis

## What I did

For Part 2, I used annual proxy statements as the disclosure source. I collected DEF 14A filings from SEC EDGAR for the companies in the assignment sample, covering as much of the 2016–2024 period as I could collect systematically.

The purpose of this part was to compare what companies emphasize in formal disclosures with what they say on their public-facing About / Mission / Values pages in Part 1. Proxy statements are not a direct record of company behavior, but they do show what companies formally disclose to shareholders about governance, risk oversight, compensation, human capital, and related priorities.

I used a keyword-based text mining approach. After downloading and cleaning the filing text, I counted language related to several disclosure themes:

* diversity and inclusion
* sustainability and environment
* employees and human capital
* governance and ethics
* community and social impact
* risk and security
* forward-looking language
* risk-related language

Because proxy statements vary a lot in length, I also created normalized measures as mentions per 1,000 words. The main dataset I use for later analysis is: `data/part2_proxy_disclosure_analysis_normalized.csv`

I also kept a metadata file: `data/part2_proxy_metadata.csv`

The final Part 2 dataset includes 265 filings across 42 companies from 2016 to 2024. Coverage is not complete, but the dataset is large enough to compare broad patterns across companies, sectors, and years.

## Why I made these choices

I chose proxy statements because they are available through SEC EDGAR and can be collected in a more consistent way than ESG, sustainability, or DEI reports. ESG reports are useful, but companies publish them under different names, in different website locations, and with different historical availability. Since this assignment asks for a method that could scale, I wanted to use a source that had a more standardized collection process.

I used DEF 14A filings because they usually include information about board governance, executive compensation, shareholder matters, risk oversight, and sometimes human capital, diversity, or sustainability. These topics are relevant to the idea of “lived values” because they show what companies formally prioritize in their investor-facing disclosures. I used keyword-based text mining because it is transparent and easy to audit. A more complex NLP or LLM-based method could capture more nuance, but keyword counts make it clear how each measure was created. This was important because Part 3 uses these outputs to construct an authenticity index. I normalized the keyword counts per 1,000 words because raw counts would be unfair across documents. A longer proxy statement naturally has more keyword mentions, even if the theme is not especially central. Normalization makes the results more comparable across firms and years.

## Assumptions

I assumed that proxy statements can serve as a reasonable disclosure-based proxy for company priorities. This does not mean they fully represent what companies actually do. Instead, I treat them as formal evidence of what companies choose to emphasize in a recurring public document. I also assumed that more frequent mentions of a theme suggest greater emphasis on that theme. This is a simple assumption, and it does not capture the full meaning or tone of the surrounding text. For example, a company might mention climate change because it is making a serious commitment, because it faces regulatory pressure, or because it is describing a risk. My method does not fully separate those cases. I treated DEF 14A filings by filing year. This means the year variable reflects when the proxy statement was filed, not necessarily the exact year in which all described company activities happened. I also assumed that the SEC filing text extracted from HTML was usable after cleaning. Some SEC documents still include repeated headings, tables of contents, or formatting artifacts, so the cleaned text is not perfect.

## What I would do differently with more time

With more time, I would improve coverage first. The current dataset includes 42 of the 50 companies, not the full sample. I would investigate the missing company-year observations one by one to determine whether they are missing because of ticker/CIK matching issues, filing availability, company name changes, or problems in my download logic.

I would also improve the text analysis method. The keyword approach is easy to understand, but it misses context. A better version would combine keyword counts with sentence-level classification or an LLM-assisted coding step. For example, instead of only counting the word “diversity,” I would classify whether a sentence describes a concrete program, a general statement, a legal disclosure, or a risk factor. I would also add a more direct event-based analysis. In this version, I mainly use year and sector patterns to look for changes over time. A stronger version would explicitly compare language before and after major events, such as the rise of human-capital disclosure language, COVID-19, increased attention to racial justice and DEI, and growing cybersecurity or climate-risk disclosure pressure.

Finally, I would check whether the same patterns hold using another document type, such as ESG or sustainability reports. That would help show whether the results are specific to proxy statements or more general across different types of corporate disclosures.

## Limitations

The biggest limitation is that proxy statements are not the same as behavior. They are legal and investor-facing documents, so they naturally emphasize governance, boards, compensation, shareholder voting, and risk. Some values may appear more important simply because proxy statements are structured around those topics. Another limitation is incomplete coverage. The final dataset has 265 filings across 42 companies, rather than a complete 50-company by 9-year panel. This means sector comparisons should be interpreted carefully, especially when some sectors or companies have fewer observations.

The keyword method is also limited. It counts whether certain terms appear, but it does not fully understand context. A keyword mention could reflect a genuine priority, a required disclosure, a risk warning, or boilerplate language. This is especially important for themes like diversity, climate, and risk, where the meaning depends heavily on surrounding sentences. The cleaned SEC text may still contain some noise. HTML filings can include repeated navigation text, tables, headings, or formatting artifacts. I cleaned the text enough for a proof of concept, but it is not perfect.

Finally, the normalized measures make documents more comparable, but they do not solve every problem. A high mention rate does not automatically mean a company is more authentic or more committed to that theme. It only means that the theme appears more frequently in that disclosure document.