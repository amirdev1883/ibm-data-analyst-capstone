# Developer Technology Trends

### IBM Data Analyst Capstone · Stack Overflow Developer Survey

**Amir Arani** · [GitHub](https://github.com/amirdev1883) · [LinkedIn](https://www.linkedin.com/in/amiraranii/)

![Developer technology trends: survey scope and technology comparisons](reports/figures/project_overview.png)

An analysis of **18,845 survey respondents across 161 countries**, built around a practical question: **which technologies are developers using, and which do they want to use next?**

This repository turns the IBM Data Analyst Capstone materials into a reproducible portfolio project. It covers data quality, multi-select survey preparation, exploratory analysis, SQL, and visual communication. Every new chart and dashboard view comes from the same documented course dataset.

**Explore:** [Interactive dashboard](dashboard/index.html) · [Analysis findings](reports/FINDINGS.md) · [Portfolio notebooks](notebooks/README.md) · [Final report](reports/presentation/final_report.pdf) · [Presentation](reports/presentation/final_presentation.pptx)

> To use the dashboard, download or clone this repository and open `dashboard/index.html` in a browser. It works offline. GitHub's file viewer displays the HTML source until the dashboard is hosted. [Publishing guide](docs/GITHUB_SETUP.md)

## What this project demonstrates

| Area | Evidence in this repository |
| --- | --- |
| Data collection and provenance | A documented source URL, cached download, SHA-256 verification, and a manifest of all 29 supplied files |
| Data preparation | Explicit respondent IDs, duplicate auditing, preserved missing values, and correctly split multi-select answers |
| Exploratory analysis | Respondent demographics, compensation distributions, outlier flags, and rank correlations with sample sizes |
| SQL | A normalized SQLite model, technology comparisons, country summaries, and respondent-level retention intent |
| Visualization | Eight generated figures and a dashboard with three sections, metric controls, and CSV export |
| Communication | A findings report, six executed portfolio notebooks, and the supplied final report and PowerPoint |
| Reproducibility | One analysis command, dependency versions, 12 focused tests, and a GitHub Actions validation workflow |

## Selected findings

| Finding | Result in the course subset |
| --- | ---: |
| JavaScript, reported past-year use | **14,943 respondents · 79.3%** |
| SQL, reported past-year use | **12,602 respondents · 66.9%** |
| Python, reported past-year use | **9,590 respondents · 50.9%** |
| PostgreSQL, reported past-year use | **11,514 respondents · 61.1%** |
| Respondents aged 25–44 | **68.6%** |

Percentages above use all **18,845 respondents**. Technology fields allow multiple selections. The “used” and “desired” answers come from the **same 2024 survey**; they describe usage and intentions rather than observed future growth or employer hiring demand.

![Top programming languages: usage compared with next-year intentions](reports/figures/languages_trends.png)

The findings support using common tools such as Python, SQL and PostgreSQL in practical projects. Career decisions also require separate evidence about local roles and job openings. See the [full results and interpretation](reports/FINDINGS.md).

## Explore the dashboard

The [offline dashboard](dashboard/index.html) includes three views:

| View | Content |
| --- | --- |
| Current technology usage | Languages, databases, platforms, and web technologies |
| Future technology intentions | Next-year preferences, including a platform treemap |
| Demographics | Age, country, education, and age grouped by education |

Change the top-N selection, switch between percentages and counts, and export the underlying section data as CSV. No sign-in, API key, network connection, or dashboard subscription is required to view the included results.

The portfolio dashboard uses ranked country and education bars for readable comparisons. The original course presentation retains its supplied dashboard images and course-specific chart choices.

## Reproduce the analysis

Use **Python 3.11 or later**. From the extracted project folder:

```bash
python -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
python scripts/run_analysis.py --download
```

On Windows PowerShell, activate the environment with `.venv\Scripts\Activate.ps1` instead.

The first run downloads the approximately **59 MB** course CSV and verifies its fingerprint. It writes tables, figures, a SQLite database and a self-contained dashboard. The large raw CSV and generated SQLite database are excluded from Git; the small aggregate outputs are included for immediate review.

To analyze a compatible local CSV:

```bash
python scripts/run_analysis.py --input /path/to/survey.csv
```

To open and rerun the portfolio notebooks after generating the analysis:

```bash
python -m pip install -r requirements-notebooks.txt
jupyter lab notebooks
```

## Repository map

| Path | Purpose |
| --- | --- |
| [notebooks/](notebooks/README.md) | Six completed portfolio notebooks with saved outputs |
| [src/](src/capstone_analysis.py) | Preparation, analysis, database export, figures and dashboard generation |
| [scripts/](scripts/run_analysis.py) | Analysis entry point and project validation |
| [sql/](sql/01_top_technologies.sql) | Four reusable queries against the normalized database |
| [dashboard/](dashboard/index.html) | Self-contained interactive dashboard |
| [reports/](reports/FINDINGS.md) | Findings, aggregate tables, figures, and original presentation files |
| [data/](data/README.md) | Data source registry, dictionary and download instructions |
| [coursework/](coursework/README.md) | The 24 original IBM notebooks and three assignment guides |
| [docs/](docs/METHODOLOGY.md) | Methodology, provenance, validation and GitHub publishing guide |
| [tests/](tests/test_analysis.py) | Checks for analysis behavior and SQL agreement |

The original course notebooks contain starter exercise cells and are preserved as reference materials. The six notebooks in `notebooks/` contain the completed portfolio analysis. [Source status and attribution](docs/PROVENANCE.md)

## Validation

```bash
python -m unittest discover -s tests -v
python scripts/validate_project.py
```

The tests check counting unique respondents, distinct technology tokens, percentage denominators, duplicate IDs, missing data, salary rules, and agreement between Python and SQL. [Validation details](docs/VALIDATION.md)

## Data and attribution

The portfolio analysis uses the **modified 2024 Stack Overflow survey CSV supplied for the IBM dashboard assignment**. Its 18,845 respondents differ from the 65,437 respondents in the CSV linked from many of the original labs. The two sources are documented separately and are not pooled.

This is a voluntary survey subset, so results describe the sample rather than the entire developer population. [Methodology](docs/METHODOLOGY.md) · [Source registry](data/sources.json) · [Original survey methodology](https://survey.stackoverflow.co/2024/methodology)

Stack Overflow survey data is published under ODbL 1.0, with individual contents under DbCL 1.0. Original IBM course materials retain their notices. The [MIT license](LICENSE) applies to the new project code and documentation, with the exclusions described in [NOTICE.md](NOTICE.md).
