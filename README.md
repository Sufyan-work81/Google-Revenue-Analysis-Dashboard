# Google Revenue Dashboard
## Overview
This interactive dashboard visualizes Google's revenue growth from 2000 to 2025 using Python and Dash. The application features multiple visualizations including revenue trends, growth rates, and geographic distribution across countries.

## **Author**: Sufyan Ahmad

## Features
- **Key Metrics Cards**: Display latest revenue, average annual growth, and total growth
- **Interactive Charts**:
  - Revenue trend line chart
  - Year-over-year growth bar chart
  - Revenue distribution box plot
  - Country revenue world map
- **Time Range Selector**: Slider to filter data by year range
- **Responsive Design**: Adapts to different screen sizes
- **Synthetic Data Generation**: Includes realistic revenue patterns

## Screenshot
![Dashboard Preview](
<img width="1366" height="768" alt="Screenshot (253)" src="https://github.com/user-attachments/assets/abc84ed3-e792-43ba-8ad7-66ae51cea205" />

)

## Requirements
- Python 3.7+
- Required packages:
  ```bash
  pip install dash pandas plotly dash-bootstrap-components numpy
  ```

## Installation & Usage
1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/google-revenue-dashboard.git
   cd google-revenue-dashboard
   ```
2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
3. Run the application:
   ```bash
   python dashboard.py
   ```
4. Access the dashboard at:
   ```
   http://localhost:8050
   ```

## File Structure
```
google-revenue-dashboard/
├── dashboard.py          # Main application code
├── README.md             # This documentation
├── requirements.txt      # Dependency list
└── assets/               # Optional CSS and images
```

## Code Overview

### Data Generation
The application generates synthetic revenue data using this logic:
```python
# Generate synthetic revenue data (2000-2025)
years = list(range(2000, 2026))
revenue = [400 + 0.5*(year-2000)**2 + 300*np.random.rand() for year in years]

# Create DataFrame
df = pd.DataFrame({
    'Year': years,
    'Revenue (Billions USD)': [round(r, 2) for r in revenue],
    'Growth Rate (%)': [0] + [round((revenue[i] - revenue[i-1])/revenue[i-1]*100, 2) 
                         for i in range(1, len(revenue))]
})
```

### Dashboard Components
The dashboard features:
1. **Header Section**: Title and author information
2. **Metrics Cards**: Key revenue statistics
3. **Interactive Controls**: Year range slider
4. **Visualization Cards**:
   - Revenue trend line chart
   - Growth rate bar chart
   - Revenue distribution box plot
   - Country revenue world map

### Callback Functions
The interactive elements are connected through this callback:
```python
@callback(
    [Output('revenue-chart', 'figure'),
     Output('growth-chart', 'figure'),
     Output('revenue-distribution', 'figure'),
     Output('world-map', 'figure')],
    [Input('year-slider', 'value')]
)
def update_charts(selected_years):
    # Filter data based on selected year range
    # Update all visualizations
    return revenue_fig, growth_fig, dist_fig, map_fig
```

## Customization
To use real data instead of synthetic data:
1. Replace the data generation code with:
   ```python
   real_data = pd.read_csv('your_revenue_data.csv')
   ```
2. Ensure your dataset contains:
   - Year column
   - Revenue values
   - Growth rate percentages
   - Country data for the map visualization

## Potential Enhancements
1. Add user authentication
2. Implement data export functionality
3. Include forecasting models
4. Add mobile-responsive optimizations
5. Integrate with real Google financial data APIs

## License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
