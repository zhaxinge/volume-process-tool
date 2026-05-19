# Bulk Traffic Review — Day Type Analysis

A browser-based traffic volume review tool for processing intersection-level traffic count files, matching them to a dictionary, reviewing weekday/Saturday/Sunday patterns, flagging detector or approach issues, and exporting review-ready summaries.

Live site:

```text
https://zhaxinge.github.io/volume-process-tool/
```

## What this tool does

This tool is designed for corridor or network-level traffic volume review. It helps users quickly load multiple intersection files, match them to a reference dictionary, review time-of-day volume profiles, identify potential detector or data issues, and export results for documentation or follow-up analysis.

Main functions include:

- Load traffic volume files directly in the browser.
- Load a dictionary/mapping file for intersection, phase, approach, and detector reference.
- Match intersections using KITS ID / Synchro ID information from filenames and dictionary fields.
- Review volume patterns by day type: weekday, Saturday, and Sunday.
- Plot approach, detector, and movement-level trends using interactive charts.
- Flag intersections as OK, warning, issue, or unreviewed.
- Add reviewer notes for each intersection.
- Export review summaries and structured JSON outputs.

## How to use

### 1. Open the tool

Go to:

```text
https://zhaxinge.github.io/volume-process-tool/
```

No installation is required. The tool runs fully in the browser.

### 2. Prepare the files

Recommended folder structure:

```text
project-folder/
├── volume-files/
│   ├── weekday/
│   ├── saturday/
│   └── sunday/
└── dictionary/
    └── intersection_dictionary.xlsx
```

The structure does not need to be exact, but the tool works best when the volume files and dictionary file are clearly separated.

### 3. Upload the volume files

Use the upload area to load traffic volume files. The tool can process multiple files at once. Keep filename identifiers consistent where possible, such as:

```text
SynID_92950110_Route50_MajesticLn.xlsx
KITS_92950110_weekday.xlsx
```

Helpful filename identifiers include:

- Synchro ID
- KITS ID
- Route or corridor name
- Intersection name
- Day type, if available

### 4. Upload the dictionary file

Upload the dictionary/mapping file that contains the intersection reference information. The dictionary should include fields such as:

- Intersection name
- KITS ID
- Synchro ID
- Phase
- Approach
- Detector or movement mapping

The tool uses this file to connect raw detector or volume data to readable intersection/approach labels.

### 5. Run matching

After files are uploaded, click the matching/start button. The tool will attempt to identify intersections by matching IDs from the filenames and the dictionary.

Review the matching results before using the charts. If an intersection is unmatched, check whether the file name and dictionary use the same ID format.

### 6. Review each intersection

Use the left sidebar to move through intersections. For each intersection, review:

- Overall volume trend
- Day-type pattern: weekday, Saturday, Sunday
- Approach-level pattern
- Detector or movement-level pattern
- Missing, flat, extreme, or suspicious values

Use the status buttons or review controls to classify the intersection.

Recommended review status definitions:

| Status | Meaning |
|---|---|
| OK | Data looks usable for analysis or timing work. |
| Warning | Data is mostly usable but should be checked or documented. |
| Issue | Data has clear problems and may need exclusion, repair, or field follow-up. |
| Unreviewed | Not reviewed yet. |

### 7. Add notes

Use notes to document why an intersection was flagged. Good notes are short and specific, for example:

```text
Phase 4 detector appears flat after 15:00; exclude PM period.
```

```text
Northbound approach has weekday spike inconsistent with adjacent days; verify detector mapping.
```

```text
Saturday and Sunday patterns look normal; weekday AM peak is usable.
```

### 8. Export results

Use the export buttons to download review outputs. Depending on the current version, exports may include:

- Review summary
- JSON summary
- Intersection status table
- Notes and issue list
- Day-type review results

Use the exported files for QC documentation, exclusion lists, or downstream analysis.

## QC review guidance

Common issues to flag:

| Issue type | What to look for |
|---|---|
| All zeros | Detector or approach shows zero volume for the entire period. |
| Mostly zeros | Data is present but mostly zero during expected active periods. |
| Flat / stuck pattern | Volume or occupancy appears constant for a long period. |
| Extreme spike | Sudden unrealistic jump in one interval. |
| Missing data | Large time gaps or incomplete day coverage. |
| Mapping issue | Detector pattern does not match the expected phase or approach. |
| Direction inconsistency | One direction is much higher/lower than expected without a clear reason. |

## Suggested sample questions for users

After exporting the summary JSON, users can ask an AI assistant questions such as:

```text
Which intersections still have detector issues?
```

```text
Create a QC-ready exclusion list from this summary JSON.
```

```text
Which intersections are safe to use for Synchro volume development?
```

```text
Which issues look like carry-over issues versus new issues?
```

```text
Summarize all intersections with weekday PM peak data problems.
```

```text
Which detectors should be excluded from the final averaged volume calculation?
```

```text
Write a short email summary explaining the remaining detector issues.
```

```text
Group the issues by intersection, phase, approach, and detector.
```

## Deployment

This repository is deployed as a static GitHub Pages site.

Recommended GitHub Pages setting:

```text
Settings → Pages → Build and deployment → Source → GitHub Actions
```

The site uses:

- `index.html` as the main application file
- `.github/workflows/static.yml` for GitHub Pages deployment

No backend server is required.

## Local use

You can also run the tool locally by opening `index.html` directly in a browser.

For best results, use Chrome or Edge. If browser security blocks local file behavior, run a simple local server from the repository folder:

```bash
python -m http.server 8000
```

Then open:

```text
http://localhost:8000
```

## Notes

- File processing happens in the browser.
- Uploaded data is not sent to a backend server by this static site.
- Keep a copy of original raw volume files before making exclusions or edits.
- Review flagged results before using them for official timing plans, reports, or submissions.

## Author

Created by Eve Zhang for traffic volume QC, detector review, and corridor-level operational analysis workflows.
