# TidyVCD Repo Guide

## Folders:

### R (vcd2df.R)

**Description**
This function, `vcd2df`, processes a Value Change Dump (VCD) file and converts it into a structured data frame. It begins by reading the file line by line, skipping to the `$scope` section where variable definitions start. The function identifies unique variables by parsing lines containing `"var"`, storing them in a dictionary for later use. Once all variables are gathered, a preliminary data frame is constructed and initialized with placeholder values. Then, it searches for `$dumpvars`, where time-series data begins. It continues reading the file, parsing each line to extract variable values and associate them with timestamps, storing the parsed data sequentially in the data frame.
As the function iterates through the VCD file, it distinguishes between bitwise and word-based variable assignments, converting numeric values from binary to integers where possible. Non-numeric entries, often encountered in initialization phases, are logged as `-1` for consistency. The data frame updates dynamically, with each column representing a new timestamp in the VCD sequence. Once all data is processed, the function renames rows according to their original variable names, removes placeholder values, and returns a well-organized data frame that reflects variable state changes over time.


### man (vcd2df.Rd)

**Description**
This file is an Roxygen2-generated documentation file for the function vcd2df. It provides structured metadata that helps users understand how the function operates, including its purpose, usage, arguments, and return values. The vcd2df function reads a *Value Change Dump (VCD)* file and converts it into a formatted data frame, allowing users to analyze variable state changes over time. The documentation also includes example code demonstrating proper usage, ensuring users can implement the function effectively.
**Usage & Maintenance**
This file was automatically generated from comments in the source script (R/vcd2df.R). *Direct edits should not be made here*; instead, modifications should be applied within the relevant R script, and Roxygen2 should be run to regenerate an updated version. Roxygen2 streamlines the documentation process, making the function easily accessible through R’s help system (help(vcd2df)).

### vignettes (index.qmd)

**Definition**
Verilog Hardware Description Language (HDL)
- Used to design, model, and simulate digital circuits and systems-like microprocessors, memory chips, and complex electronic components.
- What it does:
    - Describes Hardware Behaviour
    - Simulates Designs
    - Synthesizes Hardware

Octothorpe (#)

**Description**
This document is a vignette for the `vcd2df` function, which converts *Value Change Dump (VCD) files*—used in digital circuit simulation—into an *R data frame* for analysis. It explains how VCD files, based on the **IEEE 1364-1995/2001** standard, store register values at discrete time points during a Verilog/VHDL simulation and how `vcd2df` processes these files into a structured format, where rows represent registers and columns represent time points (formatted as octothorpe-prefixed multiples of the timescale). Key implementation details include encoding non-numerical values (`x`, `z`) as negative numbers and ignoring registers with duplicate names across modules. The workflow covers *loading the library*, *downloading a sample VCD file*, *converting it to a data frame*, *inspecting register names and timestamps*, and *cleaning up temporary files*, using a practical example from the **Naive Educational RISC-V Processor (NERV)** testbench.

----
## Files:

### .Rbuildignore

**Description**
This .gitignore file tells Git which files to ignore so they don’t get tracked in version control. It helps keep a project clean by skipping unnecessary, temporary, or auto-generated files.

### **What `.gitignore` Does**
- **Ignores Auxiliary Files** (`aux$`, `log$`, `out$`)
    —likely temporary files from LaTeX or other document processing tools. Created while working but not needed for saving.
- **Excludes Generated PDFs & Markdown** (`knitr-.*.pdf`, `knitr-.*.md`)
    —files created during R Markdown or Knitr processing.
- **Prevents Caching & Figures** (`inst/examples/cache`, `inst/examples/figure`)
    —avoiding unnecessary storage of intermediate results.
- **Ignores R Project Files** (`^\.Rproj\.user$`, `^.*\.Rproj$`)
    —specific to RStudio projects.
- **Excludes CI/CD & Build Files** (`^\.travis\.yml$`, `Makefile`)
    —used for automation but not needed in version control.
- **Prevents Documentation & Metadata** (`^docs$`, `^README-ES.md`, `^README-PT.md`, `^NEWS.md`)
    —avoiding redundant documentation versions.


### F: DESCRIPTION

**Description**
This is the **DESCRIPTION file** for the `vcd2df` R package, which converts **Value Change Dump (VCD) files** from hardware simulations into **R data frames** for analysis. 

### **Key Details**
- **Package Name**: `vcd2df`
- **Title**: "Value Change Dump to Data Frame"
- **Version**: 1.0.1
- **Author**: Calvin Deutschbein (ORCID: 0000-0003-1354-7200)
- **Description**: Provides a function that loads IEEE 1364-1995/2001 **VCD (.vcd) files**, extracts register values over time, and stores them as a structured **data frame** in R.
- **Technical Notes**:
  - Non-numerical VCD values (`x`, `z`) are encoded as **-1**.
  - Registers with repeated names in different modules are **ignored** to prevent duplication.
- **Reference**: Linked to an arXiv paper on **hardware security research**.
- **Repository & Issue Tracking**: Hosted on [GitHub](https://github.com/vcd2df/r).
- **License**: GPL-3 (open-source).
- **Documentation Tools**: Uses **Roxygen** for documentation and **Quarto** for vignettes.


### F: Makefile

**Description**
This is a **Makefile** that automates tasks for an R package (`vcd2df`). It defines a rule (`all:`) that runs several commands in sequence:

1. **`R CMD build .`** – Builds the R package from the current directory.
2. **`R CMD check --as-cran vcd2df_1.0.1.tar.gz`** – Runs package checks as if submitting to CRAN, ensuring compliance.
3. **`rm -rf *.Rcheck` & `rm -rf ..Rcheck`** – Cleans up temporary check directories.
4. **`git commit -a -m "Makefile autocommit"`** – Commits all changes with a predefined message.
5. **`git push`** – Pushes the committed changes to the remote repository.
This is a **Makefile** that automates tasks for an R package (`vcd2df`). It defines a rule (`all:`) that runs several commands in sequence:

1. **`R CMD build .`** – Builds the R package from the current directory.
2. **`R CMD check --as-cran vcd2df_1.0.1.tar.gz`** – Runs package checks as if submitting to CRAN, ensuring compliance.
3. **`rm -rf *.Rcheck` & `rm -rf ..Rcheck`** – Cleans up temporary check directories.
4. **`git commit -a -m "Makefile autocommit"`** – Commits all changes with a predefined message.
5. **`git push`** – Pushes the committed changes to the remote repository.

This Makefile streamlines package development by automating the build, validation, cleanup, and version control steps.


### F: NAMESPACE

**Description**
This is a **roxygen2-generated directive** in an R package. 

- **roxygen2**, a package for generating documentation in R. Editing it manually could disrupt the structured documentation process.
- **`export(vcd2df)`** – This line **makes the `vcd2df` function publicly available** when the package is loaded. It ensures users can call `vcd2df()` without needing to specifically import it.


### F: vcd2df_1.0.1.tar.gz

**Description**
This is a zip file

-----
### **TL;DR – TidyVCD Repository Overview**

**Purpose:**
This R package parses Value Change Dump (VCD) files—used in digital circuit simulations—and converts them into tidy data frames for analysis and visualization.

---

### **Key Components:**

#### ✅ `R/vcd2df.R`

* **Core function:** `vcd2df()`
* Reads `.vcd` files and transforms signal data into a structured R data frame.
* Designed to facilitate downstream analysis and visualization.

#### 📄 `man/vcd2df.Rd`

* Documentation for `vcd2df()` generated using Roxygen2.
* Not meant to be edited directly—update the function comments instead.

#### 📖 `vignettes/index.qmd`

* Detailed vignette showing how to use `vcd2df()` with example simulations.
* Explains the background, use cases, and output format clearly.

---

### **Support Files:**

* **`.Rbuildignore`** – Lists files/directories to ignore during build (e.g., `.git`, `README.md`).
* **`DESCRIPTION`** – Metadata for the package (name, version, author, dependencies).
* **`NAMESPACE`** – Declares which functions are exported (currently: `vcd2df()`).
* **`Makefile`** – Automates routine tasks like `build`, `check`, `install`, `clean`, and `push`.
* **`vcd2df_1.0.1.tar.gz`** – Pre-built package file for distribution or installation.

---

### **Summary:**

This is a clean, minimal R package focused on one task: **parsing VCD files into usable data**. It's production-ready and includes documentation, examples, and automation tools for building and deployment.
