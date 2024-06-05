<h1 style="font-size:48px;">Data Science Job Analysis from 2021</h1>

<img src="https://github.com/AngelX62/DS_Job_Clean/assets/120829581/60c6e040-07db-476a-b634-5202916cd65d" alt="istock-1221293664-1-1-1" width="600">

## Table of Contents
- [Project Overview](#project-overview)
- [Source of Data](#source-of-data)
- [Getting Started](#getting-started)
  - [Dependencies and User Installation](#dependencies-and-user-installation)
  - [Methods Used](#Methods-Used)
- [Plotly Visualizations](#plotly-visualizations)
  - [Plotly Code #1](#plotly-code-1)
  - [Plotly Result #1](#plotly-result-1)
  - [Plotly Code #2](#plotly-code-1)
  - [Plotly Result #2](#plotly-result-2)
## Project Overview
The data science job market is rapidly evolving, and understanding past trends is crucial for predicting future demands and preparing for upcoming opportunities. Even though the data is from 2021, this provides a historical benchmark that can help identify similar trends, shifts in the job market, and emerging skills in the present time. 

## Source of Data
The dataset used for this project can be retrieved from [here](https://www.kaggle.com/datasets/rashikrahmanpritom/data-science-job-posting-on-glassdoor/data)

## Getting Started

### Dependencies and User Installation
To run this project, you need to have the following installed:
```bash
pip install numpy pandas matplotlib seaborn plotly jupyter
```
- Python (> = 3.9)
- Jupyter Notebook
- NumPy (> = 1.19.5)
- Pandas (> = 2.2.2)
- MatplotLib (> = 3.8.2)
- Seaborn (> = 0.13.2)
- Plotly (> = 5.22.0)

### Methods Used
- Data Cleaning
- Exploratory Data Analysis
- Data Visualization

## Plotly Visualizations 
These visualizations provide insights into the data science job market, highlighting key skills and their prevalence. 

The actual Plotly graph did not render on Github so I will provide a screenshot of the visualizations. 

### Plotly Code #1
```python
# To create subplots with 2 rows and 1 column
fig = make_subplots(rows=2, cols=1)
# Get required data for melt function
data = df[['python', 'excel', 'hadoop', 'spark', 
             'tableau', 'aws', 'big_data', 'machine_learning']]

# Melt function: Unpivots a DataFrame from a wide format to a long format
# Converts DataFrame into long DataFrame with two columns: Skill and Presence
data_melted = data.melt(var_name='Skill', value_name='Presence')
# Grouping data and resetting index
prob_data = data_melted.groupby(['Skill', 'Presence']).size().reset_index(name = 'Count')
# divide the total of Counts by the number of skill req
prob_data['Probability'] = prob_data['Count'] / len(data)
conditions = [
    {'presence': 1, 'prob_color': 'purple', 'count_color': 'red', 'prob_name': 'Probability - yes (1)', 'count_name': 'Count - yes (1)'},
    {'presence': 0, 'prob_color': 'green', 'count_color': 'blue', 'prob_name': 'Probability - no (0)',  'count_name': 'Count - no (0)'}
]
for cond in conditions:
    # Subplot #1
    fig.add_trace(
        go.Bar(x=prob_data.query(f'Presence == {cond["presence"]}')['Skill'], 
               y=prob_data.query(f'Presence == {cond["presence"]}')['Probability'], 
               name=cond['prob_name'],
               marker_color=cond['prob_color']
        ), 
        row=1, col=1
    )
    
    fig.add_trace( 
         go.Bar(x=prob_data.query(f'Presence == {cond["presence"]}')['Skill'], 
                y=prob_data.query(f'Presence == {cond["presence"]}')['Count'],
                name=cond['count_name'],
                marker_color=cond['count_color']
        ), 
        row=2, col=1
    )

fig.update_layout(height=500, 
                  width=1000)

fig.update_yaxes(title_text='Probability', row=1, col=1)
fig.update_yaxes(title_text='Count', row=2, col=1)


fig.show()
```
### Plotly Result #1


<img src="https://github.com/AngelX62/DS_Job_Clean/assets/120829581/3c8428eb-e6ff-4c3a-b5b4-22f4700743a4" alt="istock-1221293664-1-1-1" width="600">


### Plotly Code #2

```python
# To create subplots with 2 rows and 1 column
fig = make_subplots(rows=2, cols=1)
# Get required data for melt function
data = df[['python', 'excel', 'hadoop', 'spark', 
             'tableau', 'aws', 'big_data', 'machine_learning']]

# Melt function: Unpivots a DataFrame from a wide format to a long format
# Converts DataFrame into long DataFrame with two columns: Skill and Presence
data_melted = data.melt(var_name='Skill', value_name='Presence')
# Grouping data and resetting index
prob_data = data_melted.groupby(['Skill', 'Presence']).size().reset_index(name = 'Count')
# divide the total of Counts by the number of skill req
prob_data['Probability'] = prob_data['Count'] / len(data)
conditions = [
    {'presence': 1, 'prob_color': 'purple', 'count_color': 'red', 'prob_name': 'Probability - yes (1)', 'count_name': 'Count - yes (1)'},
    {'presence': 0, 'prob_color': 'green', 'count_color': 'blue', 'prob_name': 'Probability - no (0)',  'count_name': 'Count - no (0)'}
]
for cond in conditions:
    # Subplot #1
    fig.add_trace(
        go.Bar(x=prob_data.query(f'Presence == {cond["presence"]}')['Skill'], 
               y=prob_data.query(f'Presence == {cond["presence"]}')['Probability'], 
               name=cond['prob_name'],
               marker_color=cond['prob_color']
        ), 
        row=1, col=1
    )
    
    fig.add_trace( 
         go.Bar(x=prob_data.query(f'Presence == {cond["presence"]}')['Skill'], 
                y=prob_data.query(f'Presence == {cond["presence"]}')['Count'],
                name=cond['count_name'],
                marker_color=cond['count_color']
        ), 
        row=2, col=1
    )

fig.update_layout(height=500, 
                  width=1000)

fig.update_yaxes(title_text='Probability', row=1, col=1)
fig.update_yaxes(title_text='Count', row=2, col=1)


fig.show()
```

### Plotly Result #2
<img src="https://github.com/AngelX62/DS_Job_Clean/assets/120829581/f49d6825-75aa-46f4-bef7-921be2be5528" alt="istock-1221293664-1-1-1" width="600">



