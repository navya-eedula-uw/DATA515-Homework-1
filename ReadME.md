# Traffic Analysis for Wikipedia Articles on Rate Diseases (2015-2024)

## Goal
The goal of this assignment is to construct, analyze, and publish a dataset of monthly article traffic for a select set of pages from English Wikipedia from July 1, 2015 through September 30, 2024. Your notebook(s) and your data files will be uploaded to a repository of your choosing. You will submit a  link to your repository to enable grading of this assignment. The purpose of the assignment is to develop and follow best practices for open scientific research as exemplified by your repository.


### Insights from Reading
After reading the two attached documents - [Assessing Reproducibility](http://www.practicereproducibleresearch.org/core-chapters/2-assessment.html) and [The Basic Reproducible Workflow Template](https://github.com/brianckeegan/Bechdel/blob/master/Bechdel_test.ipynb),several key points will be considered to ensure reproducibility in the work. First, clear documentation explaining data sources, processing steps, and variable calculations in detail is essential. This transparency is crucial for anyone attempting to replicate the analysis. Additionally, using modular code with output cells will help others follow the workflow and results more easily. Lastly, all analyses will be thoroughly documented and visualized to facilitate critical evaluation of the results.

## License
Some portions of this code were adapted from an example created by Dr. David W. McDonald for the DATA 512 Human-Centered Data Science course, part of the University of Washington's Master of Science in Data Science program. This code is shared under the [Creative Commons CC-BY license](https://creativecommons.org/licenses/by/4.0/). Revision 1.3 - August 16, 2024. Users are free to use, modify, and distribute this code under the terms of the CC-BY license, provided that appropriate credit is given to the original author.

Data was obtained from the Wikipedia API, governed by [Wikimedia's terms of use](https://foundation.wikimedia.org/wiki/Policy:Terms_of_Use), and additional data sourced in the form of CSV file (linked in the Github Repository) by Dr. David W. McDonald and the teaching assistants for the course DATA 512.

This code is provided "as is," without any warranty of any kind. The author is not responsible for any issues that may arise from its use. Contributions to this project are welcome. Please submit a pull request or open an issue to discuss potential improvements and additions.


## Data Source
The dataset from the Wikimedia Analytics API provides access to pageview metrics for all Wikimedia projects. It includes detailed insights into how often specific pages are viewed, categorized by access types like desktop, mobile web, and mobile apps. The data spans several years, making it useful for time-series analysis on user engagement trends. This dataset allows me to gather granular statistics about user behavior, focusing on unique pageviews and filtering out bots, ensuring that I capture only legitimate human interactions across various devices.

## Data Aquisition
To measure article traffic from 2015 to 2024, data was collected using the Wikimedia Analytics API. The Pageviews API ([documentation](https://doc.wikimedia.org/generated-data-platform/aqs/analytics-api/reference/page-views.html)) provides access to desktop, mobile web, and mobile app traffic data starting from July 2015 through the most recent complete month.

For this task, details of all articles listed in the [provided CSV](https://drive.google.com/file/d/15_FiKhBgXB2Ch9c0gAGYzKjF0DBhEPlY/view) were fetched by calling the PageViews API with the article names. The retrieved data was stored in JSON files, where the article titles served as keys, and the corresponding API data as values.

### Data on Rare Diseases
Pageview counts were collected for a specific subset of Wikipedia articles focused on rare diseases. This [subset](https://drive.google.com/file/d/15_FiKhBgXB2Ch9c0gAGYzKjF0DBhEPlY/view) was curated by matching articles from English Wikipedia with a database maintained by the [National Organization for Rare Diseases (NORD)](https://rarediseases.org). The selected articles either directly address rare diseases or contain relevant sections. Using this data, several datasets were generated to represent monthly activity over time, focusing specifically on pageviews initiated by users.


### API Documentation
The Pageviews API provides access to page view analytics for Wikimedia projects, allowing the retrieval of data related to how often articles are viewed. The data begins from July 1, 2015, and is available up to the most recent complete month.

For more information, refer to the official [Pageviews API documentation](https://doc.wikimedia.org/generated-data-platform/aqs/analytics-api/reference/page-views.html).


### Necessary Packages:
1. **urllib**: A Python library used to handle URLs, enabling tasks such as fetching data from the web or sending HTTP requests.
2. **json**: A built-in Python module for parsing JSON (JavaScript Object Notation) data and converting between Python objects and JSON formats.
3. **pandas**: A powerful Python library for data manipulation and analysis, providing data structures like DataFrames for efficient handling of tabular data.
4. **matplotlib**: A comprehensive Python library for creating static, animated, and interactive visualizations, commonly used for plotting graphs and charts.
5. **seaborn**: A Python data visualization library built on top of matplotlib, providing an easy-to-use interface for creating attractive and informative statistical graphics.


## Setting up Environment

1. **Install Python**: Download from [python.org](https://www.python.org/), ensure to add Python to PATH.
2. **Install Jupyter**:  On the terminal run: `pip install notebook`
3. **Launch Jupyter**: Run: `jupyter notebook`


## Running the Code
The code for the analysis is located in Wikipedia_Article_Traffic_Analysis_2015-2024.ipynb.

No additional configurations would be needed, so you can simply use the "Run All Cells" or "Restart Kernel and Run All Cells" option in Jupyter Notebook.

- Data acquisition takes around 50 minutes on a laptop with a 13th Gen Intel Core i5-1335U processor and 16GB of RAM. This time accounts for the loop through all diseases in the CSV and includes sleep intervals to avoid hitting Wikimedia's Pageview API rate limits.
- Ensure that the requests and pandas modules are installed before running the notebook. You can use `pip` or `pip3` for installation.

## Generated Files

#### JSON Data Files
**rare-disease_monthly_cumulative_201507-202409.json**
Contains time series data of the total monthly (desktop and mobile) pageview activity for each article in the CSV.

**Data Schema:**
```
{
    "string": [                        // Page title
        {
            "project": "string",       // Wikimedia domain and subdomain
            "article": "string",       // Page title
            "granularity": "string",   // Time interval between data points
            "timestamp": "string",     // Timestamp in YYYYMMDDHH format
            "agent": "string",         // Type of user agent
            "views": "integer"         // Number of page views
        }
    ]
}
```

**rare-disease_monthly_desktop_201507-202409.json**
Contains time series data of the monthly desktop pageview activity for each article in the CSV.
**Data Schema:**
```
{
    "string": [                        // Page title
        {
            "project": "string",       // Wikimedia domain and subdomain
            "article": "string",       // Page title
            "granularity": "string",   // Time interval between data points
            "timestamp": "string",     // Timestamp in YYYYMMDDHH format
            "agent": "string",         // Type of user agent
            "views": "integer"         // Number of page views
        }
    ]
}
```

3. **rare-disease_monthly_mobile_201501-202409.json**
Contains time series data of the monthly mobile pageview activity for each article in the CSV.
**Data Schema:**
```
{
    "string": [                        // Page title
        {
            "project": "string",       // Wikimedia domain and subdomain
            "article": "string",       // Page title
            "granularity": "string",   // Time interval between data points
            "timestamp": "string",     // Timestamp in YYYYMMDDHH format
            "agent": "string",         // Type of user agent
            "views": "integer"         // Number of page views
        }
    ]
}
```

For this project, we focus on monthly pageviews, so the granularity is set to "monthly" in all records.

### Seaborn Time-Series Plots:
- **max_avg_min_avg.png:** Displays time series data for the articles with the highest and lowest average page requests across both desktop and mobile access over the entire period.
![Maximum Average, and Minimum Average Page Requests](/generated_seaborn_plots/max_avg_min_avg.png)

- **top_10_peak_page_views.png:** Shows time series data for the top 10 articles based on the largest peak page views, categorized by access type (desktop or mobile).
![Top 10 Peak Page Views](/generated_seaborn_plots/top_10_peak_page_views.png)

- **fewest_months_of_data.png:** Highlights the 10 articles with the fewest months of data for both desktop and mobile access.
![Fewest Months of Data](/generated_seaborn_plots/fewest_months_of_data.png)

### Summary of Analyses
1. From the max_avg_min_avg.png, the time series graph shows view trends for "Black Death" and "Filippi Syndrome" from 2015 to 2024. In 2020, "Black Death" saw a sharp spike in views, with mobile views surpassing 2 million. After this, views returned to lower levels. "Filippi Syndrome" consistently had minimal views across both platforms. The spike likely shows the increased interest during the COVID-19 pandemic, as people drew parallels to historical events, with more attention on "Black Death" than "Filippi Syndrome."

2. The graph compares peak views for the top 10 topics from 2015 to 2024. A major spike occurred in 2020, with "Pandemic" leading the surge, reaching over 2 million views on mobile. Mobile views surpassed desktop, reflecting users’ easier access to phones. Related topics like "Black Death" and "Chloroquine" also spiked but stabilized after 2020. Smaller peaks for topics like "Pfeiffer syndrome" are much lower. This data shows a clear link between public health crises and search behavior, with pandemic-related topics dominating viewership.

3. The graph shows that articles with fewer months of data generally have low view counts, except for occasional peaks in "COVID-19 vaccine misinformation" and "Hemolytic jaundice." However, these peaks are small compared to previous graphs. The "vaccine misinformation" article shows distinct viewing patterns between desktop and mobile in early 2023, suggesting platform-specific behavior. Most other topics attract minimal views, indicating a niche audience.


# Challenges

1. **UTF-8 Encoding**
In the data processing, specific encoding practices were implemented to avoid errors. When writing to a file, the code `write_to_file(desktop_views, filename=f"{target_folder}/{desktop_views_file}", mode="w+", encoding="utf-8")` is used to ensure that the data is saved with UTF-8 encoding. Similarly, for reading from a file, the line with `open(file_path, encoding='utf-8') as json_file` is used. Using UTF-8 encoding is crucial when reading and writing JSON files because it accommodates a wide range of characters and symbols, ensuring that the data is accurately represented and can be processed without encountering encoding errors. This was useful for handling special characters that may be present in article titles or content, as it prevents issues related to character representation.

2. **Handling Special Characters in Article Titles**
The original data acquisition code, derived from Dr. David's work, encountered issues with encoding the '/' character in article titles, such as 'Sulfadoxine/pyrimethamine'. The original code was:
```
urllib.parse.quote(request_template['article'].replace(' ', '_'))
```
To resolve this, the code was modified to:
```
urllib.parse.quote(request_template['article'].replace(' ', '_'), safe='')
```
By setting `safe=''`, all characters, including '/', are properly encoded. This modification was essential for accurately handling article titles that include the '/' character.

# Considerations and Concerns
1. **Mobile Data:** The Pageviews API differentiates mobile access into two separate requests. The view counts in the file `rare-disease_monthly_mobile_201501-202409.json` represent the combined total of both mobile web and mobile app traffic for each article.
2. **Data Gaps:** Some articles may show missing data for specific months due to limitations of the API or issues with data availability.
3. **API Changes:** The Wikimedia API might change over time, which could impact data consistency throughout the analysis period.
4. **Article Renames:** Articles that were renamed during the analysis period may show up as two distinct entries.
5. **Content Changes:** Articles may undergo content updates or revisions during the analysis period, potentially impacting their relevance and viewership trends.
6. **Analysis Scope:** The scope of analysis must be clearly defined to avoid misinterpretation of results. This can be including information about which time frames and articles are included.


## File Structure
```
DATA515-Homework-1/
├── generated_json_files/
│   ├── rare-disease_monthly_cumulative_201507-202409.json
│   ├── rare-disease_monthly_desktop_201507-202409.json
│   └── rare-disease_monthly_mobile_201507-202409.json
├── generated_seaborn_plots/
│   ├── fewest_months_of_data.png
│   ├── max_avg_min_avg.png
│   └── top_10_peak_page_views.png
├── rare-disease_cleaned.AUG.2024.csv
├── ReadME.md
├── Traffic_Analysis_2015-2024_Rare_Diseases.ipynb
├── LICENSE
```

