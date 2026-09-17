# Programming Assignment 4
#### Lance Terence A. Lozano | 2ECE-C

## Objectives
1. filter tabular data using several categorical and numerical conditions;
2. construct focused DataFrames by selecting relevant features;
3. summarize the relationship between categorical features and a numerical variable; and
4. communicate a data comparison using clear and correctly labeled plots.

To access Pandas library, the import convention must be used:
```python
import pandas as pd
```
```python
df = pd.read_excel('board2.xlsx')
```
This code reads the board2.xlsx file into a Pandas DataFrame named board2 and displays its contents in the notebook.

## A. Visayas Communication Dataframe
```python
df['Average'] = df[['Math', 'GEAS', 'Electronics', 'Communication']].mean(axis=1)
df
VisComm = df.loc[(df['Hometown'] == 'Visayas') & (df['Track'] == 'Communication'), ['Name', 'Gender', 'Math', 'Electronics', 'Average']]
VisComm
```
This code calculates the row-wise mean score across four subjects to create an `Average` column, then extracts rows for students from Visayas in the Communication track with selected columns.

```python
VisComm.shape[0]
```
Returns the total number of rows (students) present in the filtered `VisComm` DataFrame.

## B. Visayas Female Dataframe
```python
VisFemale = df.loc[(df['Hometown'] == 'Visayas') & (df['Gender'] == 'Female'), ['Name', 'Track', 'GEAS', 'Electronics', 'Average']]
VisFemale
```
This filters the main dataset for female students whose hometown is Visayas and retains specific columns for analysis.

```python
VisFemale.loc[VisFemale['Average'] >= 60]
```
This code displays only the rows from `VisFemale` where the student's average grade is 60 or higher.

## C. Category-Average Visualization
```python
import matplotlib.pyplot as plt
```
Imports Matplotlib's pyplot module to enable data plotting and visualization.

```python
mean_track = df.groupby('Track')['Average'].mean().reset_index()
mean_gender = df.groupby('Gender')['Average'].mean().reset_index()
mean_hometown = df.groupby('Hometown')['Average'].mean().reset_index()

display(mean_track)
display(mean_gender)
display(mean_hometown)
```
Calculates the mean overall grade grouped separately by `Track`, `Gender`, and `Hometown`, then displays each summary table.

```python
plt.figure(figsize=(15, 5))

plt.subplot(1, 3, 1)
plt.bar(mean_track['Track'], mean_track['Average'])
plt.title('Mean Average by Track')
plt.xlabel('Track')
plt.ylabel('Mean Average Grade')
plt.ylim(0, 100)

plt.subplot(1, 3, 2)
plt.bar(mean_gender['Gender'], mean_gender['Average'])
plt.title('Mean Average by Gender')
plt.xlabel('Gender')
plt.ylim(0, 100)

plt.subplot(1, 3, 3)
plt.bar(mean_hometown['Hometown'], mean_hometown['Average'])
plt.title('Mean Average by Hometown')
plt.xlabel('Hometown')
plt.ylim(0, 100)

plt.tight_layout()
plt.show()
```
Configures a side-by-side figure layout containing three bar charts to visually display the mean overall grades across track, gender, and hometown. Each subplot applies specific axis labels and standardizes the vertical scale from 0 to 100 for accurate comparison. Finally, `plt.tight_layout()` adjusts subplot spacing to prevent overlapping before `plt.show()` renders the final graphs.

## Interpretation Statements:
Track: Within the observed dataset, students in the Communication track recorded the highest sample mean average score of 67.98.

Gender: Within the observed dataset, Male students recorded the highest sample mean average score of 67.18.

Hometown: Within the observed dataset, students originating from Luzon recorded the highest sample mean average score of 68.08.

## README File Version History
September 17,2026 - Update README output uploaded
