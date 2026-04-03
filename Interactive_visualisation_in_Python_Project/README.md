# Interactive Visualisation in Python
[![Python](https://img.shields.io/badge/Python-3.x-blue?logo=python)](https://www.python.org/)
[![Plotly](https://img.shields.io/badge/Plotly-Interactive-brightgreen?logo=plotly)](https://plotly.com/python/)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![ALX Africa](https://img.shields.io/badge/ALX-Africa-green)](https://www.alxafrica.com/)

A hands-on Jupyter notebook project exploring interactive data visualisation in Python using Plotly, Cufflinks, and ipywidgets — applied to a real-world Medium article dataset.

## Project Overview

This project demonstrates how to build dynamic, user-controlled charts and filters directly within a Jupyter notebook. Working with Medium article statistics, the project covers everything from interactive data tables to correlation heatmaps with selectable colorscales.

**Key Highlights:**
- **Dataset:** Medium article statistics (January 2019)
- **Interactive Controls:** Sliders, dropdowns, and textboxes via `@interact`
- **Visualisations:** Scatter plots, correlation matrices, and annotated heatmaps
- **Total Exercises:** 5 interactive functions built end-to-end

## Dataset

The project uses Medium article statistics sourced from [Will Koehrsen's Data Analysis repository](https://github.com/WillKoehrsen/Data-Analysis).

**Key fields include:**

| Field | Description |
|---|---|
| `title` | Article title |
| `claps` | Number of claps received |
| `views` | Total article views |
| `reads` | Number of reads |
| `read_time` | Estimated read time (minutes) |
| `published_date` | Date of publication |
| `tags` | Article topic tags |

## Exercises Overview

### Exercise 1 — `show_articles_more_than`
An interactive filter that allows the user to:
- Input a column name using a textbox
- Choose a numeric threshold using a slider
- Display a formatted heading showing the filter condition
- Return a filtered table of articles where the selected column exceeds the threshold

### Exercise 2 — `show_titles_more_than`
An interactive filter using linked dropdowns that allows the user to:
- Select a column (`read_time`, `views`, or `reads`) from a dropdown
- Select a corresponding threshold value from a dropdown
- Display a filtered table of matching articles

### Exercise 3 — `correlations`
An interactive correlation calculator that allows the user to:
- Select two numeric columns from dropdowns
- Print the computed correlation value between the two columns in a formatted string

### Exercise 4 — `scatter_plot`
An interactive Plotly scatter plot that allows the user to:
- Select x and y axis columns from dropdowns of numeric fields
- Generate a fully interactive scatter plot with a dynamic title

### Exercise 5 — `plot_corrs`
A customisable annotated correlation heatmap that allows the user to:
- Select from 18 colorscale options via dropdown
- Render an annotated heatmap with correlation values rounded to 2 decimal places

## Technical Implementation

### Key Libraries

```python
import pandas as pd
import numpy as np
import plotly.express as px
import plotly.graph_objs as go
import plotly.figure_factory as ff
import cufflinks as cf
from ipywidgets import interact, widgets
```

### Interactive Widget Pattern

```python
from ipywidgets import interact
from IPython.core.display import HTML

@interact
def show_articles_more_than(column='claps', x=5000):
    display(HTML(f'<h3>Showing articles with more than {x} {column}</h3>'))
    display(df.loc[df[column] > x, ['title', 'claps', 'published_date', 'read_time', 'tags', 'views', 'reads']])
```

### Correlation Heatmap

```python
import plotly.figure_factory as ff

corrs = df.corr(numeric_only=True)

@interact
def plot_heatmap(colourscale=cscales):
    figure = ff.create_annotated_heatmap(
        z=corrs.round(2).values,
        x=list(corrs.columns),
        y=list(corrs.index),
        colorscale=colourscale,
        annotation_text=corrs.round(2).values
    )
    figure.show()
```

### Data Model
- **Primary DataFrame:** Medium article statistics loaded via `pd.read_parquet()`
- **Numeric Columns:** Used for correlation analysis, scatter plots, and threshold filtering
- **Widget Controls:** `@interact` decorator auto-generates UI controls from function signatures

## Repository Structure

```
interactive-visualisation-python/
├── README.md
├── LICENSE
└── Interactive_visualisation_in_Python_Project.ipynb
```

## Getting Started

1. Clone this repository
2. Install the required dependencies
3. Enable ipywidgets in Jupyter
4. Launch the notebook

```bash
# Clone the repository
git clone https://github.com/csfrost/interactive-visualisation-python.git

# Navigate into the project directory
cd interactive-visualisation-python

# Install dependencies
pip install pandas numpy scipy plotly cufflinks ipywidgets chart-studio pyarrow

# Enable ipywidgets in Jupyter
jupyter nbextension enable --py widgetsnbextension

# Launch the notebook
jupyter notebook Interactive_visualisation_in_Python_Project.ipynb
```

## Built With

- [Python 3](https://www.python.org/)
- [Pandas](https://pandas.pydata.org/)
- [NumPy](https://numpy.org/)
- [Plotly](https://plotly.com/python/)
- [Cufflinks](https://github.com/santosjorge/cufflinks)
- [ipywidgets](https://ipywidgets.readthedocs.io/)
- [SciPy](https://scipy.org/)

## Impact

This project enables:
- **Exploratory Analysis:** Rapidly filter and inspect article performance data interactively
- **Correlation Discovery:** Identify relationships between engagement metrics at a glance
- **Visual Storytelling:** Communicate data patterns through dynamic, user-driven charts
- **Reproducibility:** All visualisations are self-contained within a single notebook

## Acknowledgments

This project was developed as part of the Data Science programme with **ALX Africa**. The dataset and project structure were guided by ALX Africa's curriculum in building real-world data visualisation skills.

Special thanks to:
- **ALX Africa** for the educational opportunity and structured learning path
- The instructional team for guidance on Python visualisation best practices
- Fellow learners for collaborative problem-solving throughout the programme

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Author

**CSFrost**
- GitHub: [@csfrost](https://github.com/csfrost)
- Portfolio: [Python Projects](https://github.com/csfrost/Python_projects)

## Contact

For questions about this project or collaboration opportunities, please open an issue in this repository or reach out via GitHub.

---

*This is a portfolio project created for educational purposes as part of ALX Africa's Data Science curriculum.*
