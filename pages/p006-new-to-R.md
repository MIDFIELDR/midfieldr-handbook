New to R?
================

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
(Windows) shortcuts we use regularly include

| Keyboard shortcut | Action                               |
|:------------------|:-------------------------------------|
| `ctrl shift K`    | Compile knitr or R Markdown document |
| `ctrl L`          | Clear the RSDtudio Console           |
| `ctrl shift C`    | Comment/uncomment line(s)            |
| `ctrl X, C, V`    | Cut, copy, paste                     |
| `ctrl F`          | Find in text                         |
| `ctrl I`          | Indent/re-indent lines               |
| `alt` –           | Insert `<-`, the assign operator     |
| `ctrl alt B`      | Run from begining to line            |
| `ctrl alt E`      | Run from line to end                 |
| `ctrl Enter`      | Run selected line(s)                 |
| `ctrl S`          | Save                                 |
| `ctrl A`          | Select all text                      |
| `ctrl Z`          | Undo                                 |

## Work in an RStudio Project

The first rule of working in an RStudio project,

> Start your session by launching the `project-name.Rproj` file in the
> project’s main directory.

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
if you are approaching a project deadline. Read more about it at
[Maintaining R](https://whattheyforgot.org/maintaining-r.html), a
chapter in Bryan and Hester \[[2](#ref-Bryan+Hester:2019)\].

**Update R.** On a Windows machine, update R using the R GUI running as
an administrator.

-   Navigate to your most recent `Rgui.exe` file located in your
    Programs directory, e.g.,
    `C:\Program     Files\R\R-3.5.3\bin\x64\Rgui.exe`  
-   Right-click on `Rgui.exe` and run as administrator

A straightforward update procedure uses the pacman package and the
following lines of code. The first line ensures that pacman is
installed. Run these lines in the R GUI. Defaults are generally OK.

``` r
# ensure pacman is installed
if (!require("pacman")) install.packages("pacman")

# load installr
pacman::p_load("installr")

# update R 
installr::updateR()
```

**Update RStudio.** Check for updates from the menu *Help &gt; Check for
Updates*. If *Check for Updates* does not appear in the menu,

-   Find the current version of RStudio from the menu *Help &gt; About
    RStudio*  
-   Navigate to the [RStudio
    website](https://www.rstudio.com/products/rstudio/#Desktop), find
    out what the current version is.

To update RStudio, close RStudio on your machine, download the new
version, and run the `RStudio-n.n.n.exe` as an administrator (`n.n.n` is
the current version number).

**Update R packages.** When updating packages, if a window pops up
asking about compilation,

-   NO saves time
-   YES gets you the latest version but can be time-consuming. Don’t say
    yes if you are in a hurry to get some work done.

To update packages in RStudio,

-   From the RStudio pane, Select *Packages &gt; Update*
-   OR, from the menu, *Tools &gt; Check for Package updates …*

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

<div id="ref-Bryan+Hester:2019" class="csl-entry">

2\. Bryan J, Hester J (2019) <span class="nocase">What They Forgot to
Teach You About R</span>. <https://whattheyforgot.org/>

</div>

</div>