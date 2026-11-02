# Replication code: GTX-A and excess commuting in Seoul

Code for *Does opening a regional express rail line increase excess commuting? Evidence from Seoul, Korea* (Lee, Hardman and Yi; Findings, in revision).

## What is here

- `replication_gtx_excess.R` — one R script that (1) downloads the sampled daily files from the Seoul Open Data Plaza, (2) aggregates them to monthly origin–destination commuting flows, (3) solves the transportation problem in two steps (margins held at their 2024 means; margins following each month), (4) computes the estimates, intervals and rank-based p values, the pre-opening trend checks, the benchmark checks and the sensitivity to pairs absent in 2023, and (5) draws Figure 1 and Figure S2. *The script will be added once its output has been checked against the published numbers.*
- `sampled_days.txt` — the 108 sampled weekdays (Tuesday to Thursday of one mid-month week per month, January 2023 to December 2025).

## Data

The mobility data are the Seoul Metropolitan Government's open data "Seoul capital region de facto population mobility (origin–destination)", dataset OA-22300 on the Seoul Open Data Plaza (https://data.seoul.go.kr/dataList/OA-22300/F/1/datasetView.do), one file per day, under the Korea Open Government License type 1 (attribution). The data are not redistributed here; the script downloads the sampled days directly.

## Software

R with the packages data.table, transport, ggplot2 and patchwork.
