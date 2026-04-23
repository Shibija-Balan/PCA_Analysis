# Coursework 2

## MA22019 Introduction to Data Science

**Set:** 23 April 2026

**Due:** 17:00 on 1 May 2026 (UK time)

**Value:** This assignment carries **60%** of the total marks for the unit.

**Estimated time required:** The coursework should take no more than **12
hours** to complete.

**Submission:** Electronically via
`github.bath.ac.uk/ma22019-2026/coursework-02-yourusername`. You should submit
the following files and folders:

- `coursework_02.qmd`. The updated version with your code and answers.
- `coursework_02.md`. The rendered version of your `.qmd` file.
- the generated `coursework_02_files/` folder (which contains your plots).
- the `data/` folder (intact as provided).

For the full submission details, see

- [Submission Process](#submission-process)
- [Submission Rules](#submission-rules)
- [Practical Notes](#practical-notes)

below.

**Conditions:** This is an **individual** coursework. You may discuss taught
methods and general unit material with the lecturer, but the submitted analysis and
writing must be your own work. It should be completed during your computer lab
on Monday 27 April or Tuesday 28 April and in your own time.

**Support and advice:** You will be able to ask questions during the lectures
and during your tutorials. Questions can also be posted on Moodle or the
[MA22019 Padlet board](https://padlet.com/kanayaizquierdo/ma22019-b2blg96nnptw574a).
You can ask general statistical, coding or presentation questions relevant to
the coursework or the course in general, but not specific questions about how
to do the coursework analyses.

**Marking scheme** See [details below](#marking-scheme)

**Feedback:** General cohort feedback for the coursework will be posted on the
unit website within a maximum of **three semester weeks** following the
submission deadline. You will receive individual feedback after marks are
released for Semester Two.

**Late Submission of Coursework** See [details below](#late-submission-of-coursework)

**Academic Integrity Statement** See [details below](#academic-integrity-statement)

**Generative AI** See [details below](#generative-ai-guidance)

## Tasks

### Generalities

**Task overview:** You are asked to investigate the spatial distribution of
reported incidents across an unnamed fictional city, use the available neighbourhood data to
develop and justify possible explanations, and make a small number of
evidence-based recommendations.

**Data provided:** You have been given three files in the `data/` folder:

- `data/city_wards.shp`: ward boundary polygons for the city.
- `data/ward_profiles.csv`: ward-level neighbourhood indicators.
- `data/incident_reports.csv`: incident-level records including coordinates,
  dates, and short descriptions.

The incident `x` and `y` coordinates are in the same coordinate reference
system as the ward boundary file.

**Variables:** The main variables in the two `.csv` files are:

- In `ward_profiles.csv`:
  `ward_id`, `ward_name`, `unemployment_rate`, `deprivation_score`, `rental_share`,
  `population_density`, `transport_access`, `lighting_coverage`,
  `distance_police_hub`, and `listed_building_share`.
- In `incident_reports.csv`:
  `incident_id`, `ward_name`, `x`, `y`, `date`, and `description`.


In general terms, the ward-profile variables describe social pressure, density, access, lighting, distance to police infrastructure, and local building character, while the incident file records where and when an incident was logged and includes a short description.

**Data inspection:** You should inspect the three files carefully before
starting your analysis and justify your handling of anything unusual you
find in them.

**Open-endedness:** There is more than one valid way to approach this
coursework. You are expected to make and justify your own decisions about what
evidence and methods are most relevant.

**Methods boundary:** Your analysis should use methods taught in **MA22019**.
You may choose which taught methods are most relevant, but you should not rely
on untaught methods. Use of untaught methods may lead to loss of marks.

**Packages:** You may use standard packages already used in the unit where
appropriate, but package choice should remain secondary to clear, taught
methods and sound interpretation.

### Task Descriptions

### Task 1

Identify and investigate the most important spatial patterns in the incident
data.

### Task 2

Use the available neighbourhood data to develop and justify possible
explanations for the patterns you identified.

### Task 3

Make a small number of evidence-based recommendations for priority areas or
actions.

## Practical Notes

Please note the following practical points.

- Your coursework repository is separate from the `materials` repository. Do
  not try to complete or submit Coursework 2 inside `materials`.
- The `materials` repository is read-only for students. You may pull updates
  from it, but you cannot push changes to it.
- You must **render** your `coursework_02.qmd` file before submission so that
  the `.md` file and the `coursework_02_files/` folder are created.
- The `coursework_02_files/` folder is only created when rendering produces
  figures or other embedded output files, so it may not appear immediately in
  a very early draft.
- If your plots appear in RStudio but the `coursework_02_files/` folder does
  not appear in the Git tab, check whether a `.gitignore` rule is hiding
  folders ending in `_files/`.
- If the `data/` folder or `.Rproj` file does not appear in your Git tab, this
  usually means those files have not changed. Check your repository on
  `github.bath.ac.uk` to confirm that they are present.
- If Git push is rejected with a "fetch first" or "non-fast-forward" message,
  you will usually need to pull first and then push again.
- If Git reports an unfinished merge or divergent branches, follow the
  coursework troubleshooting guide rather than continuing to click pull
  repeatedly.
- If you are working on Windows and Quarto does not render because of an R path
  issue, check the troubleshooting guide for the Windows-specific fix.
- Keep your `MA22019` working folders outside OneDrive or other cloud-synchronised
  folders where possible.
- If Git continues to fail near the deadline, you may use the browser upload
  route as an emergency fallback, but you should still check afterwards that
  the required files and folders are visible in your repository.

## Submission Process

Use the following submission process.

- Complete your answers in `coursework_02.qmd` and follow the instructions in
  `coursework_02_instructions.md`, which is the main brief document for this
  coursework.
- You only need to submit your own work. Do not worry about extra read-only
  files such as `.github/`; they can remain in your repository as they are.
- Do **not** add your name, username, candidate number, or any other personal
  identifier to the submission files. Your repository identity on
  `github.bath.ac.uk` is used to link the submission to you.
- Do **not** rename the required submission files or add personal identifiers
  to their filenames. Keep the provided names exactly as given.
- **Git Users**: Commit and push regularly (at least three times as per the
  coursework workflow at
  `https://github.bath.ac.uk/pages/ma22019-2026/ma22019_website/computing_setup/weekly_workflow.html#coursework-workflow`).
- **Non-Git Users**: You can upload as many times as you like before the
  deadline. To upload your submission files to your coursework repository:
  1. Click on the **Add file (+)** button at the top of your repository page.
  2. Select **Upload files** from the dropdown menu.
  3. Drag and drop your four required items (`coursework_02.qmd`,
     `coursework_02.md`, the `coursework_02_files/` folder, and the `data/`
     folder) into the upload box. Do **not** upload a ZIP file to GitHub.
  4. Wait for them to load.
  5. In the "Commit changes" message box below the files, type:
     `my finalised submission`.
  6. Click the green **Commit changes** button at the bottom, leaving
     "Commit directly to the main branch" selected.
  7. Verify that all four items now appear in your repository file list.

## Submission Rules

Use the provided template and follow these rules.

1. You must keep the required top-level section headings:
   `Data Preparation Notes`, `Task 1`, `Task 2`, `Task 3`, and `References`
   if used.
2. You must not delete or rename the required section headings or structural
   markers in the template.
3. The maximum prose length is **1000 words**.
4. The maximum number of exhibits is **5**. An exhibit is any displayed
   figure, map, table, or similar evidence item in the main body.
5. The word limit and exhibit cap are part of the assessment. You are expected
   to prioritise the evidence you present rather than attempt to include
   everything.
6. If you include more than **5** exhibits, only the first five exhibits in
   the main body will be assessed. Any additional exhibits will not be
   considered for marking.
7. `Data Preparation Notes` must be included. This section may be short prose
   or one small table.
8. If you use a table in `Data Preparation Notes`, that table counts as **one
   exhibit**.
9. Captions count towards the word limit.
10. `Data Preparation Notes` prose counts towards the word limit.
11. Hyphenated words count as **one** word.
12. Code, YAML (header), chunk labels, anchors, and references do **not**
    count towards the word limit.
13. A composite or multi-panel display counts as **one exhibit** if it is
    presented as one clearly labelled item with one caption.
14. Related evidence may be combined into a single clearly labelled composite
    exhibit where appropriate.
15. All assessed material must appear in the main body of the template.
    Appendices and overflow exhibits are not allowed.
15. External references are not required. Include them only if they are needed
    and relevant.
16. Students are expected to inspect, prepare, and justify their handling of
    the data appropriately before and during analysis.

### Style and Naming Conventions

17. You should write in clear, concise academic English.
18. Use informative section-level writing and exhibit captions so that your
    analytical decisions and conclusions are easy to follow.
19. Keep filenames, object names, and any created output names clear and
    sensible. Use the provided coursework filenames exactly where required.
20. Do **not** add your name, username, candidate number, or any other
    personal identifier to the submission files or filenames. The submission
    is linked to you through your `github.bath.ac.uk` repository.

## Marking scheme

The quality of work in each task will be judged using **letter grades (A-E)**,
following the same general marking format used elsewhere in the unit. Grades
may be adjusted with a **+** or **-** where appropriate.

| Grade | Meaning |
|:-----:|:--------|
| **A** | A thorough, well-reasoned analysis that uses appropriate methods, interprets results clearly, prioritises evidence effectively, and discusses assumptions and limitations thoughtfully. |
| **B** | A competent analysis with only minor gaps in reasoning, interpretation, prioritisation, or discussion of limitations. |
| **C** | A partial analysis with noticeable gaps. Some elements are handled well, but others are missing, weakly justified, insufficiently supported, or misinterpreted. |
| **D** | An incomplete or superficial analysis with substantial problems in reasoning, evidence use, or interpretation, though some elements show effort or partial understanding. |
| **E** | Not attempted, or without merit. |

Because this coursework is intentionally open-ended, there is no single
correct route. Strong work will be rewarded for making sensible analytical
choices, using evidence selectively and effectively, and justifying those
choices clearly within the stated limits.

## Late Submission of Coursework

If there are valid circumstances preventing you from meeting the deadline,
your Director of Studies may grant you an extension to the specified
submission date, if it is requested before the deadline. It has been agreed
with the Maths Director of Studies team that extensions beyond four days will
only be granted in exceptional circumstances. Forms to request an extension
are available on SAMIS.

- If you submit after the submission deadline and no extension has been
  granted, the maximum mark possible will be the pass mark.
- If you submit more than five working days after the submission deadline, you
  will normally receive a mark of zero, unless you have been granted an
  extension.

## Academic Integrity Statement

Academic misconduct is defined by the University as *"the use of unfair means
in any examination or assessment procedure"*. This includes (but is not
limited to) cheating, collusion, plagiarism, fabrication, or falsification.
The University's Quality Assurance Code of Practice,
[QA53 Examination and Assessment Offences](https://www.bath.ac.uk/publications/qa53-examination-and-assessment-offences/),
sets out the consequences of committing an offence and the penalties that
might be applied.

## Generative AI Guidance

**Type B:** "GenAI is permitted as an assistive tool for specific defined
processes within the assessment and its use is not mandatory in order to
complete the assessment."

- GenAI tools may be used to answer any question. Under the University's
  Academic Integrity Statement, you 'must not present content created by
  generative AI tools as though it were your own'. Any text or code produced
  by genAI must be checked for correctness and cited. In addition, you must
  include the mandatory declaration indicating what tools you used and how you
  used them or that you have not used genAI. You should be prepared to explain
  anything in your submission to an examiner if asked to do so.
- See [Gen AI Assessment Categorisation](https://library.bath.ac.uk/referencing/plagiarism/)
- > **Mandatory Action:** You must complete the MS Form Gen-AI Declaration
    before submitting your coursework: [Link to MS Form](https://forms.cloud.microsoft/Pages/ResponsePage.aspx?id=Ij1-N6FOLUKwrY_MiUBrnlMyExnR_X9HtmpePUW6IxJUMkxGRkFBVjVDOUtFWDFNRzZFNkdLRVNQVy4u)
