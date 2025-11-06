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
### Findings Summary

#### 1. Possible Under-Screening or Late Detection at the Primary Care Level
**Pattern:** Elevated primary-care utilization relative to cancer surgery volume.  
**Geography:** Mostly rural counties, with notable exceptions in the Bay Area.

- **Placer** — ~5–6  
- **Solano**, **Santa Clara** — ~3  
- **San Mateo**, **Contra Costa** — ~2–3  
- **San Francisco** — increased from 0 → 2 (2020–2024)  
- **Napa** — increased from 1 → 2 (2020–2024)

---

#### 2. Possible Limited Access to Specialty Cancer Care or Strong Preventive Programs
**Pattern:** Lower cancer surgery counts relative to expected utilization (negative mismatch values).   
**Geography:** Mostly rural and mixed (rural and urban) counties.

- **Merced**, **Tulare** — ~–5 to –4  
- **Fresno**, **Kings**, **San Luis Obispo** — ~–3 to –2  
- **Del Norte**, **Santa Barbara** — ~–2 to –1  
- **Lake**, **Sonoma** — –2  
- **Imperial** — ~–2 to –1  
- **Sutter** — worsened from –1 → –2 (2020–2024)

---

#### 3. Counties Showing Good Alignment
**Pattern:** Cancer surgeries roughly match PCP-level demand.

- **Los Angeles & Orange County** — ~0  
- **San Diego County** — ~0  
- **Exception:** **Imperial County**, which shows persistent negative mismatch

---

#### 4. ED Utilization Relative to Cancer Surgeries

#### Lower ED Use Compared to Cancer Surgery Rates
- **Napa** — 2 → 1  
- **Marin** — 2 → 0  

#### Higher ED Use Compared to Cancer Surgery Rates
- **Madera** — –4 (2020–2022)  
- **Merced** — ~–2 to –3  
- **Kings** — –3  
- **Tulare** — –1 to –2  
- **Kern** — –2 to –1  

#### Overall
Most California counties show **no major mismatch** between ED utilization and cancer surgery volume.


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
This project provides a high-level proxy for identifying potential gaps in cancer care coordination across California by comparing primary care and ED utilization against surgical cancer treatment volume.   

**Top Priorities**:  
Among Rural Counties with available data, **Madera,Merced, Tulare, and Kings** County had notable mismatches in both PCP utilization and ED utilization, with higher PCP utilization and higher ED burden relative to cancer surgeries within the rest of the state. This indicates a possible bottlenecks with low availability of specialized cancer care combined with higher ED utilization, indicating possible inefficiencies in diagnosing and treating cancer patients. These counties should be the top priority for targeting of healthcare products and services related to cancer care. 

**Secondary Priorities**:    
Though they did not have any notable mismatches in ED utilization, Placer County and the San Francisco Bay Area Counties of **Solano, Contra Costa, San Mateo, San Francisco, and Napa** had strikingly higher utilization of Cancer Surgeries relative to PCP utilization, indicating possible disparities in PCP availability, resulting in under-screenings or late-detection of common cancers. Any products or services targeting these counties should prioritize increasing access to PCP's and making it easier for cancer patients to receive the surgeries they need.

These indices offer a simplified but actionable signal for organizations interested in improving early detection and ensuring equitable access to specialty cancer care.

---

## Disclaimer

The analyses in this project rely on publicly available datasets from the California Health and Human Services (CalHHS) open data portal.  
At the time of this work, several fields in the Primary Care Clinic Utilization dataset did not include accompanying documentation or a data dictionary. I contacted CalHHS/HCAI for clarification, have not yet received a response.

Because of this, portions of the interpretation—particularly around how certain utilization metrics are defined, how encounter counts are aggregated, and why data is missing for some rural facilities—are based on the best reasonable assumptions drawn from the available metadata, variable naming conventions, and cross-dataset consistency checks.

Moreover, these interpretations should be understood as **informed estimates**, not official definitions. Findings should not be used to draw definitive conclusions about county-level performance, screening quality, or access to care without further verification from the data stewards.

## Code and Reproducibility
All R code used to clean and prepare the data is available in the `R_scripts/` directory.  
The Tableau workbook used to generate the final dashboard is included in the `visualizations/` folder.

