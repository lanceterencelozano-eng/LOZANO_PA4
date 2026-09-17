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

```python
VisComm.shape[0]
```

## B. Visayas Female Dataframe
```python
VisFemale = df.loc[(df['Hometown'] == 'Visayas') & (df['Gender'] == 'Female'), ['Name', 'Track', 'GEAS', 'Electronics', 'Average']]
VisFemale
```

```python
VisFemale.loc[VisFemale['Average'] >= 60]
```

## C. Category-Average Visualization
```python
import matplotlib.pyplot as plt
```

```python
mean_track = df.groupby('Track')['Average'].mean().reset_index()
mean_gender = df.groupby('Gender')['Average'].mean().reset_index()
mean_hometown = df.groupby('Hometown')['Average'].mean().reset_index()

display(mean_track)
display(mean_gender)
display(mean_hometown)
```

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

## Interpretation Statements:
Track: Within the observed dataset, students in the Communication track recorded the highest sample mean average score of 67.98.

Gender: Within the observed dataset, Male students recorded the highest sample mean average score of 67.18.

Hometown: Within the observed dataset, students originating from Luzon recorded the highest sample mean average score of 68.08.

## README File Version History
September 17,2026 - Update README output uploaded
