# My Google Data Analytics Certificate Capstone Project - A Study on Primary Care, Emergency Department and Cancer Surgery Utilization in California

## Introduction

This capstone project proposes a hypothetical business need and apply the skills learned in the Google Data Analytics Certificate course to answer the hypothetical stakeholder questions and fill that need. The data used to answer this question was cleaned in R within the ___ folder and visualized in Tableau.


## The Question

An insurance/healthcare technology company has asked me to help them identify counties with potential lack of cancer care-coordination within the state of California that could help them modify and target their products towards providing healthcare products and services for cancer patients.

The most common cancers in the United States also tend to be the most preventable ones such as colorectal, lung, and breast cancers. However, gaps in detection of those cancers can be fueled by a 
lack of care coordination among primary care physicians, emergency department professionals, and cancer specialists. In the United States, while primary care physicians are often the first to screen for and identify cancers, minority and underserved populations may first be diagnosed in the emergency department due to poverty, lack of access, or insurance (links: https://pubmed.ncbi.nlm.nih.gov/36374497/, https://pmc.ncbi.nlm.nih.gov/articles/PMC12284740/, https://academic.oup.com/jncics/article/8/3/pkae039/7682377). Identifying any counties in California with a notable incongruity in primary care (PCP) visits or emergency department (ED) visits versus cancer surgeries for any given year may serve as a quick and easy-to-parse proxy for potential markets for future products.

## The Data

All data is derived from the California Department of Health and Human Services (CalHHS) Open Data Portal. These data are de-identified and freely available to the public.

The datasets used contain information from 2020-2024 and include the:

  • Annual Report for Primary Care Clinic Utilization (link: )
  
  • Hospital Emergency Department – Encounters by Facility (link: )
  
  • Number of Cancer Surgeries (Volume) Performed in California Hospitals (link: )


## The Metrics and Definitions

**Number of Cancer Surgeries**: From link, These include surgeries performed for bladder, breast, brain, colon, esophagus, liver, lung, pancreas, prostate, rectum, and stomach cancers, based on the ICD-10 codes in inpatient acute care hospitals. These numbers are aggregatedby year and county.

**Number of PCP Encounters**: From link, These are aggregated by year and county and are the sum of the following metrics:
Evaluation and Management (new patient) Hospital Related Services Case Management Services Medicine - Special Services Preventive Medicine (infant, child, adolescent) Preventive Medicine (adults) Counseling Integumentary System Maternity Care and Delivery Pathology / Laboratory.  Dental Encounters are excluded due to irrelevance and family planning "Z" codes are excluded due to lack of presence after 2021 in the data.

**Number of ED Encounters**: From link, these are aggregated by year and county.

**Cancer Decile**: Deciles created at the county level for Number of Cancer Surgeries by Year. 1 represents the lowest cancer surgery utilization, while 10 is the highest.

**PCP Decile**: Deciles created at the county level for PCP Encounters by Year. 1 represents the lowest PCP utilization for that year, while 10 is the highest.

**ED Decile**: Deciles created at the county level for ED Encounters by Year. 1 represents the lowest ED utilization for that year, while 10 is the highest.

**PCP Mismatch Index**: The PCP Decile Subtracted from the Cancer Decile. Can range from -9 to 9.
    *Interpretations: **If negative***, *then PCP Utilization is higher than Cancer Surgery Utilization, signaling either a robust screening of cancer diagnoses or a lack of utilization of specialized cancer care.*
                      ***If zero***, *then PCP Utilization is roughly similar to Cancer Surgery Utilization, signaling alignment between PCP screening of cancers and cancer care utilization*
                      ***If positive***, *then PCP Utilization is lower than Cancer Surgery Utilization, signaling a lack of access to primary care and a possible chokepoint for cancer care utilization*

**ED Mismatch Index**: The ED Decile Subtracted from the Cancer Decile. Can range from -9 to 9.
    *Interpretations: **If negative***, *then ED Utilization is higher than Cancer Surgery Utilization, signaling potentially higher diagnoses of cancer or a lack of utilization of specialized cancer care.*
                      ***If zero***, *then ED Utilization is roughly similar to Cancer Surgery Utilization, signaling alignment between ED screening of cancers and cancer care utilization*
                      ***If positive***, *then ED Utilization is lower than Cancer Surgery Utilization, signaling effective coordination between ED encounters which diagnose cancer and inpatient cancer surgeries.*

## The Results and Interpretation

## The Limitations

## The Conclusions


