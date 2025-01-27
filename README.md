# A Markdown based template for writing audit reports

## Dependencies

1. [Pandoc](https://pandoc.org/)
2. [Pandocfilters](https://github.com/jgm/pandocfilters): `pip install pandocfilters`.
3. [LaTeX toolchain](https://www.latex-project.org/get/). We recommend a full install of LaTeX (installing individual `.sty` files are hard).
4. [Pygments](https://pygments.org/): `pip install pygments`.
5. [PyGithub](https://pypi.org/project/PyGithub/): `pip install pygithub`
6. bash

## Introduction

This repository is meant to be a single-step solution to:

- Fetch all issues from a given repository
- Sort them by severity according to their labels
- Generate a single Markdown file with all issues sorted by descending severity
- Integrate that Markdown file into a LaTeX template
- Generate a PDF report with all the issues and other relevant information

## Directory structure

There are five directories:

- `source`: Contains the source Markdown files with all information needed for the report.
- `scripts`: Contains various scripts needed to convert files and generate the PDF.
- `templates`: The LaTeX files used as template for the final report.
- `output`: Output directory where the final report will be saved. All files can be safely erased.
- `working`: A directory where the temporary files will be stored. All files can be safely erased.

## Procedure

Check contents and **manually update** the following files in `source/`:

- `summary_information.conf`: Information to be replaced in the title page and the summary.
- `reviewers.md`: List of auditors who participated during the engagement.
- `copywriters.md` : List of people who prepared the report.
- `introduction.md`: Information about the project and the review process.
- `spearbit_description.md`: Spearbit description.
- `repositories.md`: The repository and commit hash used for the review.
- `additional_comments.md`: For extra information at the end of the report. It is commented by DEFAULT, plase change if required.
- `appendix.md`: For extra information at the end of the report. It is commented by DEFAULT, plase change if required.

All `.md` files can be formatted and will be converted to LaTeX by the scripts located in `scripts/`.

The `.conf` files store text-only information, and are replaced verbatim in the final report. This means all
formatting should be removed, as the template already contains formatting.

Once all information is filled in, running `python generate_report.py` will result in the creation
of the `report.pdf` file in `output`. The `report.md` and `severity_counts.conf` files will be automatically
generated from the issues in the repository. Temporary files will be created in `working`, and they can be safely
deleted after the report is generated.

By default, there are `.gitignore` rules in place to avoid tracking the following:

- Any file in `working` (Except its own `.gitignore`)
- Any file in `output` (Except its own `.gitignore`)
- `source/report.md` and `source/severity_counts.conf` as they are automatically generated
