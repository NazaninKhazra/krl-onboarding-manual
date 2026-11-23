# 6. Research Workflow Guide

A research project is used by several people over many months. Someone else, or you in six months, should be able to open the project folder, find each file, and rerun every result. This guide sets the lab's standard for folders, code, and version control.

## Folder structure

Every project uses the same layout.

```text
project-name/
├── README.md          what the project is and how to run it
├── data/
│   ├── raw/           original files, never edited
│   ├── intermediate/  files produced during cleaning
│   └── final/         analysis-ready datasets
├── code/
│   ├── 01_clean.py
│   ├── 02_merge.py
│   ├── 03_analysis.py
│   └── 04_figures.py
├── output/
│   ├── tables/
│   └── figures/
├── docs/              codebook, data sources, meeting notes
├── reports/           weekly reports
└── paper/             manuscript and references
```

Raw data is never edited by hand. Every change to the data happens in code, so that it can be checked and repeated.

## Naming files

- Use lowercase letters, numbers, hyphens, and underscores. Avoid spaces.
- Number scripts in the order they run (`01_clean.py`, `02_merge.py`).
- Put dates in the form `YYYY-MM-DD` so that files sort correctly.
- Do not use names such as `final_v2_really_final.py`. Version control keeps the history.

## Writing code others can run

- Start each script with a short comment that says what it reads, what it does, and what it writes.
- Use relative paths (`data/raw/shelter.csv`), never paths on your own computer (`C:/Users/...`).
- Set a random seed for any step that uses random numbers.
- List the packages the project needs in `requirements.txt` (Python) or `renv.lock` (R).
- Before you share a result, restart your session and run the code from the top. If it fails, the result is not ready.

## Version control with Git

All code lives in a GitHub repository under the KRLResearchLab organization.

- Commit small changes often, with a message that says what changed (`Drop 2020 from shelter sample`).
- Pull before you start work and push when you finish.
- Do not commit data files that are large, licensed, or confidential. Add them to `.gitignore`.
- When two people work on the same script, use separate branches and merge after review.

If you have not used Git before, the Software Carpentry lesson at <https://swcarpentry.github.io/git-novice/> takes about three hours and covers what you need.

## Documenting data

Keep a codebook in `docs/` that lists, for each dataset, the source, the date downloaded, the unit of observation, the years covered, and the meaning of each variable you use. Record every sample restriction and the number of observations it removes. This record is often the first thing a referee or a new team member asks for.

## Notes and decisions

Keep a running file, `docs/decisions.md`, with one line for each decision that affects results: the date, the decision, the reason, and who made it. Weekly reports ([Document 5](05-weekly-report-template.md)) feed into this file.
