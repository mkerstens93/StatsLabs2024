[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-24ddc0f5d75046c5622901739e7c5dd533143b0c8e959d652212380cedb1ea36.svg)](https://classroom.github.com/a/lNsrM_NO)
# FES 524 Lab 01: An Introduction to R

## Goals

1.  To familiarize you with R and its documentation, including how to bring data into R, manipulate datasets in R, and carry out some simple analyses.

2.  To give you practice in writing about statistical analyses in their relevant research context.

## Preparation before coming to lab

1.  :octocat: If you do not already have an account on GitHub, follow the instructions [here](https://docs.github.com/en/get-started/signing-up-for-github/signing-up-for-a-new-github-account) to create a **free** account.

2.  If you have never seriously used R before, go to <http://cran.r-project.org/manuals.html> and download the PDF or browse the html of the first manual: An Introduction to R. Read (*) at least the first 2 sections and if you have time, browse (†) the last 3:* Introduction and preliminaries \*Simple manipulations; numbers and vectors †Function and variable index (just browse) †Concept index (just browse)

3.  If you are going to use your own computer in lab, make sure you have current versions of R, RStudio, Git, and any add-on packages. These are listed in the document `software_information.docx` that has been provided to you on Canvas.

## Lab activity

Find the lab handout inside the `/Handouts` directory and work through the document using your own R script or RMarkdown document. Feel free to save your working document inside the `/Handouts` directory. Commit and push your saved changes periodically to back up your work and feel free to help one-another through any coding issues.

## Assignment

Sir Ronald Fisher measured the length and width of two flower parts, sepals and petals, from two species of iris growing one spring in a pasture on the Gaspé Peninsula. He wanted to determine how the means of the distributions of the measurements of these flower parts differed between the two species, although he did not define what size of difference would be practically meaningful. Since field botanists often use ranges of measures of plant characters to distinguish species, he was also particularly interested in whether these measures could be used to distinguish the two species in the field.

The data for this assignment consist of sepal and petal lengths and widths (in mm) measured on 50 individuals each for two species of iris, *Iris versicolor* and *Iris setosa*. All measurements were taken at the widest point of the respective flower part. The data are in four separate files, `setosa_sepal.txt`, `setosa_petal.txt`, `versi_sepal.txt` and `versi_petal.txt`, representing measurements on sepals and petals from *I. setosa* and *I. versicolor*, respectively. Each data set contains three variables: `plant id`, `flower part width` (mm), and `flower part length` (mm).


### Section I: Analysis and results (11 points)

Based on the information above and the analysis you decide to do, answer the questions below. Use sepal width as the response variable throughout this section. Use complete sentences and a standard paragraph format when answering each question.

1.  Restate Fisher's two research questions in the order they appear in the study description.

2.  What analysis did you use to answer Fisher's first research question? Be specific.

3.  How did you check the assumptions for the analysis you defined in question 2?

4.  Write a short paragraph that clearly presents the results for the analysis from part 2. Any estimate used for inference should be accompanied by a confidence interval for that estimate, and any test statistic reported should be accompanied by appropriate information on degrees of freedom.

5.  Write a short paragraph to answer Fisher's second research question. Present any additional information you need to support your conclusion. You can include tables and graphics, with appropriate captions and clear labels, as necessary. Do not include any non-graphical output directly from R. Relevant output you want to report should be put into a table or written out within the text. Do not include any results that are not relevant or not referred to in your text. Part of your grade will be on neatness, clarity, and appropriateness of presentation; your grade will be reduced if you include superfluous output. See below for the grading rubric.

### Section II: Short answer (4 points)

Describe and justify the scope of inference based on the description of Fisher's data. If you choose to extend the scope of inference, be sure to justify this choice. If you do not, what gave you pause?  

### Analysis hints

To help guide you in your analysis, here is one approach.

1.  Use the function `read.table()` to read in the four data files.

2.  Join the two datasets `setosa_sepal.txt` and `setosa_petal.txt` by the variable `plantid`. Add a variable representing species with a value that reflects the species name to the file.

3.  Use `summary()` to calculate summary statistics for sepal and petal width.

4.  Repeat steps 2 and 3 for the `versi_sepal.txt` and `versi_petal.txt`.

5.  Concatenate the two species datasets vertically into one file with `rbind()`.

6.  Explore the resulting dataset with summaries by group and graphs.

7.  If assumptions are met, perform appropriate two sample test to answer first research question.

## Submitting the assignment

You will lose write capabilities to your assignment repository on the deadline. Please follow the instructions in the syllabus for requesting an extension if needed.

Please complete your assignment report using RStudio and RMarkdown. Knit your completed report for final formatting and save this inside a directory called `Reports` in your assignment repository. 

## Grading Rubric


| Criterion for total possible points | Possible points |
| --- | --- |
| Define 2 questions correctly | 2 |
| Analysis defined sufficiently | 1 |
| Reasonable way to check assumptions | 2 |
| Appropriate paragraph of statistical results | 3 |
| Appropriate evidence to answer second research question | 3 |
| Short answer | 4 |


| Ways to lose points | Maximum deduction |
| --- | --- |
| Writing is unclear and hard to follow | -1 |
| Figures and tables are not referred or used to support writing | -1 |
| Estimates appear with CIs or CIs are incorrect | -0.5 |
| $p$-values stand alone without test statistic | -0.5 |
| No degrees of freedom, $\nu$, to support test statistic | -0.5 | 
| Incorrect interpretation of results | -2 |

