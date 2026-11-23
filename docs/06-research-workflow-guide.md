# 6. Research Workflow Guide

A research project is used by several people over many months. Someone else, or you in six months, should be able to open the project folder, find each file, and rerun every result. This guide sets the lab's standard for folders, code, and version control.

The rules follow Gentzkow and Shapiro's *Code and Data for the Social Sciences* (2014), which is widely used in economics research labs. Read its chapters on automation, version control, directories, and documentation in your first month. It is about 40 pages.

## Folder structure

Every project uses the same layout, with separate folders by function and inputs kept apart from outputs.

```text
project-name/
├── README.md          what the project is and how to run it
├── data/
│   ├── raw/           original files, never edited
│   ├── intermediate/  files produced during cleaning
│   └── final/         analysis-ready datasets
├── code/
│   ├── 00_run_all.py  runs every step in order
│   ├── 01_clean.py
│   ├── 02_merge.py
│   ├── 03_analysis.py
│   └── 04_figures.py
├── output/
│   ├── tables/
│   └── figures/
├── docs/              codebook, decisions, contributions, meeting notes
├── reports/           weekly reports
└── paper/             manuscript and references
```

Raw data is never edited by hand. Every change to the data happens in code, so it can be checked and repeated. A single script (`00_run_all.py`) should run the whole project from raw data to final tables.

## Naming files

- Use lowercase letters, numbers, hyphens, and underscores. Avoid spaces.
- Number scripts in the order they run.
- Write dates as `YYYY-MM-DD` so that files sort correctly.
- Do not use names such as `final_v2_really_final.py`. Version control keeps the history.

## Writing code others can run

- Start each script with a short comment that says what it reads, what it does, and what it writes.
- Use relative paths (`data/raw/shelter.csv`), never paths on your own computer (`C:/Users/...`).
- Set a random seed for any step that uses random numbers.
- List required packages in `requirements.txt` (Python) or `renv.lock` (R).
- Each cleaned dataset should have a key, a variable or set of variables that uniquely identifies each row with no missing values. Check this in code after every merge.
- Before you share a result, restart your session and run the code from the top. If it fails, the result is not ready.

## Version control with Git

All code lives in a GitHub repository under the KRLResearchLab organization.

- Commit small changes often, with a message that says what changed (`Drop 2020 from shelter sample`).
- Pull before you start work and push when you finish.
- Do not commit data that is large, licensed, or confidential. List these files in `.gitignore`.
- When two people work on the same script, use separate branches and merge after review.

If you have not used Git before, the Software Carpentry lesson takes about three hours and covers what you need: <https://swcarpentry.github.io/git-novice/>.

## Documenting data and decisions

- Keep a codebook in `docs/` that lists, for each dataset, the source, date downloaded, unit of observation, years covered, and the meaning of each variable used.
- Record every sample restriction and how many observations it removes.
- Keep `docs/decisions.md`, with one line for each decision that affects results: the date, the decision, the reason, and who made it.

## Project README

Write the project README using the template from the Social Science Data Editors (<https://social-science-data-editors.github.io/template_README/>). It lists the data sources and their access conditions, the software needed, and the order in which to run the code. The American Economic Association's journals strongly encourage this template for replication packages, so a project that starts with it is ready for submission later.

## Sources

- Gentzkow, M., and Shapiro, J. M. (2014). *Code and Data for the Social Sciences: A Practitioner's Guide*. <https://web.stanford.edu/~gentzkow/research/CodeAndData.xhtml>
- Vilhuber, L., Connolly, M., Koren, M., Llull, J., and Morrow, P. (2022). *A Template README for Social Science Replication Packages* (v1.1). Social Science Data Editors. <https://doi.org/10.5281/zenodo.7293838>
- American Economic Association, Data and Code Availability Policy. <https://www.aeaweb.org/journals/data>
