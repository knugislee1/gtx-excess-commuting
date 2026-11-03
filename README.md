# Replication code: GTX-A and excess commuting in Seoul

Code for *Does opening a regional express rail line increase excess commuting? Evidence from Seoul, Korea* (Jae Hyun Lee, Scott Hardman and Jungyeon Yi; Findings, in revision).

## What is here

- `replication_gtx_excess.R` — one R script in fifteen numbered sections. It downloads the sampled daily files from the Seoul Open Data Plaza, aggregates them to monthly origin–destination commuting flows, solves the transportation problem in two steps (margins held at their 2024 means; margins following each month), and computes the estimates, the bootstrap intervals and rank-based p values, the pre-opening trend checks, the uniqueness check of every optimal assignment and Paju's own lower bound, the sensitivity to pairs absent in 2023, the destination analysis and the data record. It draws Figure 1 and Figure S2. Its last section compares every number printed in the main text, in Figure 1 and in the Supplemental Information with the number it reproduces (`paper_vs_repro.csv`).
- `sampled_days.txt` — the 126 sampled days. The 108 days of January 2023 to December 2025 (Tuesday to Thursday of one mid-month week per month) are the paper's window; the 18 days of January to June 2026 enter only the costs of origin–destination pairs that do not appear in 2023.

## Not included

Figure 2, Figure S1 and Figure S3 are maps drawn with separate scripts that need boundary and OpenStreetMap files: Figure 2B and Figure S3 use every Tuesday to Thursday outside holidays, not only the sampled days, and Figure S1 uses resident registration data; the scripts are available from the authors on request. The population figures quoted from the Ministry of the Interior and Safety are not computed by the script.

## Data

The mobility data are the Seoul Metropolitan Government's open data "Seoul capital region de facto population mobility (origin–destination)", dataset OA-22300 on the Seoul Open Data Plaza (https://data.seoul.go.kr/dataList/OA-22300/F/1/datasetView.do), one zip file per day of about 60 MB, under the Korea Open Government License type 1 (attribution). The data are not redistributed here. Section 1 of the script downloads the sampled days (about 8 GB in all; 15 to 30 seconds a day on the test machine), reduces each to a daily aggregate of commuting trips and deletes the zip.

## Software

R (tested with 4.5.3) with the packages data.table, transport, ggplot2, patchwork, ggrepel and jsonlite; `curl` on the path for the downloads; R.utils is optional. Tested with data.table 1.18.2.1, transport 0.15-4 and ggplot2 4.0.2 on macOS; other versions are untested. Run time is about 6 to 7 minutes after the downloads; peak memory about 4 GB.

## How to run

```
Rscript replication_gtx_excess.R                                          # everything, into ./replication_out
Rscript replication_gtx_excess.R OUT=results OD1_DIR=my_daily_aggregates  # reuse daily aggregates you already hold
Rscript replication_gtx_excess.R ONLY=6,7 FORCE=true                      # recompute selected sections
```

A section is skipped when its output files already exist. The random seed (20260821) is set immediately before each bootstrap. The header of the script explains the options, the embedded lookup tables and why the 2026 days are read.

## Checks

On the test machine the script reproduced the 246 numbers printed in the main text, Figure 1 and the Supplemental Information: 242 exactly at the printed precision and the four "about" statements within their tolerance. Three days re-aggregated from the raw files matched the daily aggregates used for the paper cell for cell.
