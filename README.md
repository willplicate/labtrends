# Data-Driven PMM Strategy: Search Trend Analysis for Function Health

## Project Goal

Getting a biomarker test isn't something everyone has thought to do. But there are emerging groups of users who see the value in this. As we move from early adopter phase to this product gaining wider appeal, which groups are the ones growing fastest? 

I thought about buying personas for brands like Function Health by using programmatic search trend data. I quantified market demand and identify the highest-growth target segments in this project. 


##  Key PMM Insight (Conclusion)

*Based on 12 months of aggregated U.S. Google Trends data:*

**Strongest Emerging Trend: The Worried Well**

The segment I called the **Worried Well** seems to have the most relative search demand and is also growing at the fastest rate. That indicates that this technology is reaching the mainstream, where the other more niche groups of **Biohackers** and other medical users are diminishing in importance.

**All Groups Are Growing**

What's most clear is that this is a trend that's growing in all areas. No single group I analysed is shrinking, although some are growing more slowly than others - the most mature being **Clinical Monitor** - where it's likely these have already reached saturation. Anyone who wante a CGM for monitoring an existing condition has probably already got one by now.

**Busy Professionals Overtake Biohackers**

My analysis showed that **Biohacking** is still a growing trend, but busy professionals are emerging as a newer group that see optimising their health as critical to part of a busy proefssional life.
---

## Methodology & Technology Stack

This analysis compared the relative search interest of four distinct buyer personas using representative long-tail keywords.

| Step | Tool | Output / Metric |
| :--- | :--- | :--- |
| **1. Data Collection** | Python (`pytrends` API, `time`) | Weekly Relative Search Interest Scores (0-100) |
| **2. Data Processing** | Python (`Pandas`) | Aggregated Weekly Average Trendline for Each Persona |
| **3. Trend Modeling** | Python (`NumPy`) | Linear Regression (Slope and R-Squared) to quantify growth rate. |
| **4. Visualization** | Python (`Matplotlib`) | Comparative Time-Series Chart (Image: `persona_search_trend_analysis.png`) |

## Code Snippet (Excerpt from `visualizer.py`)

```python
# The NumPy / Trendline Calculation
z = np.polyfit(x_numeric, y_data, 1) # Fit first-degree polynomial
p = np.poly1d(z)
# ...
ax.plot(df.index, p(x_numeric), 
        label=f'Growth Trend (Slope: {z[0]:.2f})')
