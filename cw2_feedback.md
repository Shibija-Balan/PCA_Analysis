# Coursework 2 Feedback

**Student:** Shibija B Kunam Balan Pathkunam
**Mark:** `68%`

## Overall summary
This submission was judged to be a competent analysis with only minor gaps overall. The points below summarise the main strengths, areas for improvement, and next steps used to support the final judgement.

## Strengths
- Used both point-pattern (kernel density) and lattice (choropleth) approaches.
- PCA performed with scaling, variance explained reported (PC1 64.9%, PC2 17.2%).
- Recommendations tied to PCA loadings (police hub distance, lighting coverage) and specific ward values.

## Areas for improvement
- Excluded transport_access and listed_building_share due to missingness without imputation or justification; could have used complete cases or imputation.
- Selection of only two priority wards is arbitrary; no clear threshold or ranking.

## Overall analytical comment
- The data preparation work and the later analytical work were considered together when forming the final judgement.
- No significant negative impact; the data preparation choices (using spatial join, handling rental_share) ensure that subsequent analyses are based on correct locations and numeric variables. Exclusion of two variables from PCA reduces the richness of the neighbourhood explanation but is acceptable.
- The overall mark reflects both the analytical substance of the work and the quality of the evidence used to justify the conclusions.

## What to improve next time
- When using a dimensionality-reduction method such as PCA, explain the key loadings and why the component you rely on is analytically meaningful.
- A stronger future submission would stay closer to the most relevant taught methods. Methods such as regression should only be used where they clearly strengthen interpretation rather than substitute for it.

## Presentation notes
Some maps were missing ward labels.

---

For the general cohort-level feedback on Coursework 2, see the course website:

<https://github.bath.ac.uk/pages/ma22019-2026/ma22019_website/coursework_02_cohort_feedback.html>
