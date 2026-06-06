**This repository contains my submission for the project on organizational authenticity and corporate value alignment.**

**The project looks at the relationship between what companies say they value and what their formal disclosures suggest they prioritize. I use the 50-company sample from the assignment across five sectors and focus on the 2016–2024 period.**

## Repository structure

```text
RA/
├── data/
│   └── Output datasets used across the four parts
├── src/
│   └── Notebooks for data collection, text extraction, analysis, and measure construction
├── part1/
│   └── README.md for Part 1
├── part2/
│   └── README.md for Part 2
├── part3/
│   └── README.md for Part 3
├── part4/
│   └── README.md for Part 4
├── Summary.md
├── requirements.txt
└── README.md
```

* Part 1: Stated values from archived About / Mission / Values pages
* Part 2: Lived values using DEF 14A proxy statement disclosures
* Part 3: Organizational Authenticity Index construction
* Part 4: Exploratory analysis of page changes and authenticity alignment

Each part has its own README documenting what I did, why I made those choices, assumptions, what I would do differently with more time, and known limitations.

## How to run

Install dependencies with:

```bash
pip install -r requirements.txt
```

The notebooks are in the `src/` folder. They are intended to be read in this order:

```text
part_1.ipynb
part_1AI.ipynb
part_2.ipynb
part_3.ipynb
part_4.ipynb
```

Some notebooks depend on outputs from earlier parts. Part 3 should be run after Parts 1 and 2, and Part 4 should be run after Part 3. The main output files are stored in the `data/` folder.

## Main outputs

The main output files are:

```text
data/part1_company_year_values.csv
data/part2_proxy_disclosure_analysis_normalized.csv
data/part2_proxy_metadata.csv
data/part2_company_summary.csv
data/part3_authenticity_index.csv
data/part4_change_alignment_summary.csv
```

## Note on LLM-assisted analysis

Part 1 includes a supplemental LLM-assisted annotation notebook, `part_1AI.ipynb`. I attempted to run the LLM annotation step, but the API call could not be completed because my API account did not have active billing / available quota. Because of that, the final Part 1 dataset relies on the keyword-coded results, while the LLM notebook is included as a pipeline design for future improvement.