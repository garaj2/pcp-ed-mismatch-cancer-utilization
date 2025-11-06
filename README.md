# California Cancer Care Coordination Analysis (2020–2024)

## Introduction
This project analyzes potential gaps in cancer care coordination across California using publicly available encounter data from the California Department of Health and Human Services (CalHHS) Open Data Portal. The work was completed as part of the Google Data Analytics Certificate program and includes data cleaning in R and visualizations in Tableau. All cleaning scripts can be found in the `R_scripts/` folder, and the full interactive dashboard is available in the repository.

## Business Question
A hypothetical insurance/health-technology company is interested in identifying California counties where cancer care may be fragmented. They want to understand where primary care (PCP), emergency department (ED), and inpatient cancer surgery utilization are misaligned, as these mismatches may signal gaps in screening, referral processes, or specialty access. Insights from this analysis could help target resources, products, and outreach programs for populations at risk of late cancer detection or limited specialty care access.

Research shows that underserved and minority populations are more likely to be diagnosed with cancer in the ED rather than in primary care settings due to factors such as poverty, limited access, and underinsurance  
(References:  
https://pubmed.ncbi.nlm.nih.gov/36374497/,  
https://pmc.ncbi.nlm.nih.gov/articles/PMC12284740/,  
https://academic.oup.com/jncics/article/8/3/pkae039/7682377).

## Data Sources
All datasets are de-identified and publicly available via the CalHHS Open Data Portal and cover calendar years 2020–2024:

- **Primary Care Clinic Utilization**:
  <https://data.chhs.ca.gov/dataset/primary-care-clinic-annual-utilization-data>

- **Hospital Emergency Department – Encounters by Facility**  
  <https://data.chhs.ca.gov/dataset/hospital-emergency-department-encounters-by-facility>

- **Number of Cancer Surgeries Performed in California Hospitals**  
  <https://data.chhs.ca.gov/dataset/number-of-cancer-surgeries-volume-performed-in-california-hospitals>

## Metrics and Definitions

### Cancer Surgeries
Count of selected cancer surgeries (bladder, breast, brain, colon, esophagus, liver, lung, pancreas, prostate, rectum, stomach) performed in inpatient acute care hospitals. Values were aggregated by **county** and **year**.

### PCP Encounters
Sum of encounter categories from the Primary Care dataset, aggregated by county and year. Included categories:

- Evaluation and Management (established patient)  
- Evaluation and Management (new patient)  
- Hospital Related Services  
- Case Management Services  
- Medicine – Special Services  
- Preventive Medicine (infant, child, adolescent)  
- Preventive Medicine (adults)  
- Counseling  
- Integumentary System  
- Maternity Care and Delivery  
- Pathology / Laboratory  

**Excluded:**  
- Dental encounters (CDT codes)  
- Family Planning “Z” codes (not consistently present after 2021)

### ED Encounters
Total annual ED encounters per county, aggregated from the ED dataset.

---

## Decile Calculations
Deciles were calculated **at the county-year level**:

- **Cancer Decile**: 1 = lowest cancer surgery utilization, 10 = highest  
- **PCP Decile**: 1 = lowest PCP utilization, 10 = highest  
- **ED Decile**: 1 = lowest ED utilization, 10 = highest  

---

## Mismatch Indices

### PCP Mismatch Index
Range: **–9 to 9**

Interpretation:
- **Negative:** Higher PCP utilization relative to cancer surgeries  
  - May indicate strong preventive screening or limited specialty care access  
- **Zero:** Alignment between PCP screening activity and cancer surgery volume  
- **Positive:** Lower PCP utilization relative to cancer surgeries  
  - Possible under-screening or late cancer detection  

### ED Mismatch Index 
Range: **–9 to 9**

Interpretation:
- **Negative:** Higher ED utilization relative to cancer surgeries  
  - May reflect cancer diagnoses occurring in emergency settings or limited specialty care  
- **Zero:** Alignment between ED encounters and cancer surgery utilization  
- **Positive:** Lower ED utilization relative to cancer surgeries  
  - Possibly effective coordination or fewer emergency-based cancer diagnoses
 
  - If either decile is missing, then the PCP/ED Mismatch Indices are not calculated
---

## Results
*To be completed:* Summary of key county-level findings, notable mismatches, and geographic patterns observed from 2020–2024. 
### Overall
- While PCP,ED, and Cancer Surgery utilization have increased at the county level each year, this change has been minimal (see R file).
- All counties with missing data from each of these categories tended to be rural in nature, from Northern, Central, and Inland California (see R file).
  - The most common type of missing data present among counties with missing data was for Cancer Surgeries.
 
### Counties of Interest
Possible Under-Screening of Cancer or Late-Detection of Cancer at Primary Care Level:
- Primarily in Rural Counties, with exception of Counties within San Francisco Bay Area
          - Placer County (~5 to 6)
          - Solano and Santa Clara County (3)
          - San Mateo County and Contra Costa County (~3 to 2)
          - San Francisco County (increase from 0 to 2 from 2020-2024)
          - Napa County (increase from 1 to 2 from 2020-2024)

Possible Lack of Access to Specialty Cancer Care or Strong Preventative Screening Program :
          - Merced County and Tulare County (~ -5 to -4)
          - Fresno County, Kings County, and San Luis Obispo County ( ~-3 to -2)
          - Del Norte County and Santa Barbara County(~-2 to -1)
          - Lake County and Sonoma County (-2)
          - Imperial County (~-1 to -2)
          - Sutter County (increase from -1 to -2 from 2020-2024)
Counties with Good Alignment between Cancer Surgeries and PCP Utilization:
- San Diego and Los Angeles Areas (~0) except for Imperial County
          

- Lower ED utilization Relative to Cancer Surgeries
    - Napa County (2 to 1)
    - Marin County (2 to 0)
  - Higher ED utilization Relative to Cancer Surgeries
      - Madera (-4 from 2020-2022)
      - Merced (~-2 to -3)
      - Kings (-3)
      - Tulare (-1 to -2)
      - Kern (-2 to -1)
  - Most counties did not have notable mismatches in ED and Cancer Surgery Utilization.
---

## Limitations
- Encounters ≠ people.
  - Some people may individually have greater or fewer numbers of each type of encounters, which may skew results. Deciles are used to try and standardize these measurements, but patient-level data would still be preferred for this type of analysis if available.
- Encounter data do not indicate cancer stage, screening history, or referral pathways.  
- Cross-county utilization of cancer surgeries not captured.
  - e.g. encounters of cancer care outside of patient's home county due to lack of access.
- Deciles describe **relative** utilization, not population-adjusted rates.  
- Data availability varies by year and county.

---

## Conclusion
This project provides a high-level proxy for identifying potential gaps in cancer care coordination across California by comparing primary care and ED utilization against surgical cancer treatment volume. The mismatch indices offer a simplified but actionable signal for organizations interested in improving early detection and ensuring equitable access to specialty cancer care.

---

## Code and Reproducibility
All R code used to clean and prepare the data is available in the `R_scripts/` directory.  
The Tableau workbook used to generate the final dashboard is included in the `visualizations/` folder.

