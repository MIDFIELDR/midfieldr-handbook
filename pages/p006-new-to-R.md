New to R?
================

![](../resources/p006-header.jpg) <small> <br> <i>Xena’s best friend</i>
by Vera is licensed under
<a href="https://creativecommons.org/licenses/by-nc-nd/2.0/legalcode">CC
BY-NC-ND 2.0</a> <br> </small>

## Introduction

Researchers interested in exploring MIDFIELD data are often R novices,
learning to use midfieldr at the same time they are learning to use R.
There are many good online resources for learning R, so we do not
attempt to reproduce that work here. However, we would like to offer
some suggestions to help address some of the obstacles our new users
have encountered in the past.

## Keyboard shortcuts

If you are working in RStudio, you can see the menu of keyboard
shortcuts using the menu *Tools &gt; Keyboard Shortcuts Help*. The
shortcuts we use regularly include

| Windows / Linux | Action                              | Mac OS         |
|:----------------|:------------------------------------|:---------------|
| `ctrl shift K`  | Compile R Markdown document         | `cmd shift K`  |
| `ctrl L`        | Clear the RSDtudio Console          | `ctrl L`       |
| `ctrl shift C`  | Comment/uncomment line(s)           | `cmd shift C`  |
| `ctrl X, C, V`  | Cut, copy, paste                    | `cmd X, C, V`  |
| `ctrl F`        | Find in text                        | `cmd F`        |
| `ctrl I`        | Indent or re-indent lines           | `cmd I`        |
| `alt` –         | Insert the assignment operator `<-` | `option` –     |
| `ctrl alt B`    | Run from begining to line           | `cmd option B` |
| `ctrl alt E`    | Run from line to end                | `cmd option E` |
| `ctrl Enter`    | Run selected line(s)                | `cmd Return`   |
| `ctrl S`        | Save                                | `cmd S`        |
| `ctrl A`        | Select all text                     | `cmd A`        |
| `ctrl Z`        | Undo                                | `cmd Z`        |

## Work in an RStudio Project

The first (highly opinionated) rule for MIDFIELD researchers

> Always work in an RStudio Project

-   A project can be any unit of work: a course, a workshop, a paper, a
    grant, practice R, etc.
-   Start every work session in an RStudio project.
-   If your last session was in an RStudio Project, launching RStudio
    will re-open that project
-   Alternatively, launch a project by navigating to the project
    directory and running the file with the `.Rproj` suffix.

RStudio is an an integrated development environment (IDE) for R that
includes a console, editor, and tools for plotting, history, debugging,
and workspace management as well as access to GitHub for collaboration
and version control \[[1](#ref-Rstudio:2021)\]. If we provide IDE
screenshots, they will be from the RStudio interface. As the folks at
RStudio assert,

> RStudio projects make it straightforward to divide your work into
> multiple contexts, each with their own working directory, workspace,
> history, and source documents.

The advantages of working in an RProject are:

-   the working directory is set to the project directory, enabling the
    use of relative file paths in your scripts to support portability,
    reproducibility, and collaboration
-   active tabs are restored to where they were the last time the
    project was closed
-   multiple projects can be open at the same time

You can read more about RProjects
[here](https://support.rstudio.com/hc/en-us/articles/200526207-Using-Projects).

## Type once-only commands in the Console

The installation instructions for midfielddata and midfieldr start with

    # install midfielddata first 
    install.packages("midfielddata", 
                     repos = "https://MIDFIELDR.github.io/drat/", 
                     type = "source")

These lines can be typed in the RStudio console rather than an R script,
because they generally only have to be run once. If you write them in a
working script, you unnecessarily re-install the package every time you
run the script.

## Stay current

Running old software can be considerably harder than running new
software. Get current at the start of a new project, but avoid updating
if you are approaching a project deadline.

Navigate to [Updating the R habitat](p003-updating-R-habitat.md) for
guidance in keeping R, RStudio, and R packages up-to-date.

## Use relative paths

Explicitly link files using relative file paths within an RStudio
Project. Paths are are relative to the main directory of an RStudio
Project. For example, you might have an R script in the `scripts`
directory that reads a raw data file,

``` r
DT <- fread("data-raw/2020-03-21-student-record-ver09.txt")
```

When the data have been cleaned up, you might save the results to the
`data` directory, e.g.,

``` r
fwrite(DT, "data/2020-03-21-clean-student-record.txt")
```

Another script in the `scripts` directory might read this data,

``` r
DT <- fread("data/2020-03-21-clean-student-record.txt")
```

and after constructing a graph, write the graph to file in the `figures`
directory,

``` r
gggsave(filename = "fig-01-enrollees", 
        path = "figures/", 
        device = "png", 
        width = 4.5, 
        height = 3.5, 
        units = "in")
```

## Plan your directory structure

At a minimum, a project might start with three directories,

    project-name/
      |- data/ 
      |- documents/
      |- scripts/
      |- project-name.Rproj

`data/`  
Data ready for analysis  
File names carefully curated for reproducibility

`documents/`  
Outlines, drafts, other text

`scripts/`  
R scripts for analysis and creating graphs

Two additional directories are often useful:

`data-raw/`  
Data in their original form, never edited manually

`figures/`  
Graphs created by scripts are written to this directory, making them
easy to find and sort through later

## Directories for larger projects

At the start of a project, you should carefully consider the number and
types of files you will create over the life of the project and lay out
a directory structure that helps you consistently organize your work.

For a longer-term project, the directory structure can become more
detailed. Each publication directory could have its own sub-directories
for `documents`, `figures`, `manage`, and `scripts`. For example:

    project-name/
      |- 2018-conference-name/
          |- documents
          |- figures
          |- manage 
          |- scripts
      |- 2019-journal-name/
      |- 2020-presentation-name/
      |- admin/
      |- data/ 
      |- data-raw/
      |- resources/
      |- README.Rmd
      |- project-name.Rproj

`yyyy-publication-name/`  
Everything that creates a specific publication, report, or
presentation  
Can include R scripts, reports, figures, and administrative materials
relevant to the publication or report

`admin/`  
Overall project management and correspondence  
Proposals and RFPs  
Contracts

`manage/`  
Publication administrative materials  
Conference registration  
Correspondence with editors Travel reservations, registration, etc.

`resources/`  
Bibliography and CSL files accessed by any of the publications  
Image downloads and screen-shots accessed by any of the publications

`README.Rmd`  
Describes the overall project generally  
Can facilitate collaboration if git and GitHub are being used

For different opinions on directory structure schemes, see

-   Karl Broman (n.d.) [Organize your data and
    code](https://kbroman.org/steps2rr/pages/organize.html)  
-   The Carpentries (2018) [Project management with
    RStudio](https://swcarpentry.github.io/r-novice-gapminder/02-project-intro/)  
-   Chris von Csefalvay (2018) [Structuring
    projects](https://chrisvoncsefalvay.com/structuring-r-projects/)  
-   Mira Céline Klein (2017) [A meaningful file structure for R
    projects](https://www.inwt-statistics.com/read-blog/a-meaningful-file-structure-for-r-projects.html)

## References

<div id="refs" class="references csl-bib-body">

<div id="ref-Rstudio:2021" class="csl-entry">

1\. RStudio Team (2021) RStudio: Integrated development environment for
r. <http://www.rstudio.com/>

</div>

</div>
