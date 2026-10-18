# Student Performance Analysis

This project explores student performance in math, reading, and writing. It includes an Excel workbook for examining the data and building interactive charts, and a Power BI report for viewing the results as a two-page dashboard.

## Project files

| File                                                                                     | Description                                                                                                       |
| ---------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------- |
| [`StudentsPerformance.csv`](./StudentsPerformance.csv)                                   | Data table with 1,000 student records and eight demographic, study, and score fields.                             |
| [`student performance analysis.xlsx`](./student%20performance%20analysis.xlsx)           | Excel analysis workbook. Contains the enriched student table, score extremes, and an interactive chart dashboard. |
| [`student performance visualization.pbix`](./student%20performance%20visualization.pbix) | Power BI Desktop report with an embedded data model and two report pages.                                         |

## Data

The data used comes from [Kaggle](https://www.kaggle.com/datasets/adithyabshetty100/student-performance). The CSV contains 1,000 records and these columns:

| Column                        | Description                                                                 |
| ----------------------------- | --------------------------------------------------------------------------- |
| `gender`                      | Student gender.                                                             |
| `race/ethnicity`              | Student's group, represented by categories such as Group A through Group E. |
| `parental level of education` | Reported parental education category.                                       |
| `lunch`                       | Lunch category (`standard` or `free/reduced`).                              |
| `test preparation course`     | Whether the student completed the test preparation course.                  |
| `math score`                  | Math test score.                                                            |
| `reading score`               | Reading test score.                                                         |
| `writing score`               | Writing test score.                                                         |

The workbook adds additional fields to the dataset by using PowerQuery:

- `ID` is used to add an identifier to the entries / rows.
- `average score` is the arithmetic mean of the student's math, reading, and writing scores. It may contain decimal values.
- `has passed` stores a pass/fail category for use in summaries and charts. The result is computed by checking if the score for any of the subjects is higher than 50, meaning the student passed, otherwise failed.

## Excel workbook

The workbook has three worksheets:

### `StudentsPerformance`

An Excel table named `StudentsPerformance` covering 1,000 student rows plus the header (range `A1:K1001`). It contains the 11 fields described above: the eight CSV fields, `ID`, `average score`, and `has passed`. This is the detailed record-level data used by the workbook analysis.

### `Score Tops`

Provides the student ID and subject/average scores in a **pivot table**, plus high- and low-score summaries for:

- Average score
- Math score
- Reading score
- Writing score

It includes Slicers for multiple conditions that filters the table based on:

- Student test preparation completed
- Gender
- Parent's level of education
- Student's result of the test

The summaries use `MAX`, `MIN`, and `XLOOKUP` formulas to show the extreme score and the ID of a student with that score. If multiple students share an extreme value, `XLOOKUP` returns the first matching record. The displayed results change based on the pivot table, and also by changing the Slicers.

![Image showing the pivot table with data, slicers and the min and max values for subjects](./images/Score%20Tops%20Excel.png)

### `Score Graphs`

A basic dashboard of six Charts:

- Average scores for students classified as passed versus failed
- Student distribution by gender
- Student distribution by test-preparation-course status
- Math, reading, and writing scores by gender
- Scores by parental education level
- Student pass/fail distribution

The data used for making the charts is put below each one, and is based on the table at `StudentsPerformance`.

![Image showing all the charts, with below each of them being the table with the data used](images/Score%20Graphs%20Excel.png)

## Power BI report

The report contains two pages: `General Info` and `Grade Infos`. The data used is the excel file, with custom measures made for passing rate and highest average subject used in cards.

### `General Info`

An overview page with:

- KPI cards for the nonblank student ID count, average score, and passing rate
- A pie chart showing the gender distribution
- A clustered column chart comparing average, math, reading, and writing scores across gender

![A PowerBi page showing the charts described above](images/General%20Info%20PowerBi.png)

### `Grade Infos`

A page focused on score and pass/fail comparisons, with:

- Slicers for gender, race/ethnicity, and test-preparation-course status
- KPI cards for the student count, average score, and highest-average subject
- A clustered column chart comparing average math, reading, and writing scores for passed and failed groups
- A pie chart showing the pass/fail distribution

The charts change based on the groupes selected on the slicers, by default having not filter added.

![A PowerBi page showing the charts described above](images/Grade%20Infos%20PowerBi.png)
