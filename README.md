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

## Technical Challenges & Problem Solving

There weere several technical hurdles that required debugging and optimisation:

### 1. API Rate Limiting (The "Too Many Requests" Error)
* **Challenge:** Initial execution of the script often resulted in a `TooManyRequestsError` (HTTP 429) from the Google Trends API, which prematurely terminated the data collection loop and caused the fourth segment (`Busy_Professional_Trend`) to be excluded from the final data set.
* **Solution:** Implemented the `time.sleep(5)` function *between* API calls for each persona cluster. This introduced a necessary delay, ensuring the script respected the rate limits and successfully retrieved all four segments on subsequent runs.

### 2. Search Term Validation (The 'Zero' Score Check)
* **Challenge:** Google Trends returns a search interest score from 0-100. A score of `0` can mean either zero search volume or that the terms are not recognizable or too generic. We had to ensure our chosen terms had statistical relevance.
* **Solution:** After the first run, the raw data was inspected. Any persona showing an index of `0` across many weeks required re-validation of the constituent keywords (e.g., ensuring "at home health screening" was used instead of an overly generic "health check"). This ensured the final average trend was based on valid, high-intent keywords.

### 3. Environment Setup
* **Challenge:** The `pytrends` library is a community-maintained wrapper. There were some compatibility issues between the Python environment and its dependencies.
* **Solution:** Made sure I installed first via `pip install pytrends` within a dedicated virtual environment. 

## Code Snippet (Excerpt from `visualizer.py`)

```python
# The NumPy / Trendline Calculation
z = np.polyfit(x_numeric, y_data, 1) # Fit first-degree polynomial
p = np.poly1d(z)
# ...
ax.plot(df.index, p(x_numeric), 
        label=f'Growth Trend (Slope: {z[0]:.2f})')

