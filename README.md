Project Title: Election Data Scraper & Analysis Tool

Project Overview:
This project involved building a Python scraper to collect and integrate two distinct datasets: election results from Politico's API and demographic data from the US Census Bureau API. The goal was to create a comprehensive CSV dataset combining county-level election results with county names and state information, while also categorizing and aggregating votes for less prominent candidates. This dataset could be used for further analysis, visualization, or integration with other data sources to understand election patterns in relation to demographic factors.

Problem and Motivation:
Accessing and combining data from different sources can be challenging. Election results are often scattered across various websites or APIs, and demographic data requires querying government APIs. Manually collecting and merging this data is time-consuming and error-prone. This project aimed to automate this process, creating a reusable tool to efficiently gather and structure this valuable information.

Approach and Solution:
To achieve this, I developed a Python script leveraging several key libraries and API endpoints:

1) Data Sources:

* Politico Election Data API: I utilized Politico's API to fetch real-time election results at the county level. This API provided data in JSON format, including vote counts for each candidate, election progress, and candidate identifiers. I also used their Candidate Metadata API to get candidate names and party affiliations.

* US Census Bureau API (ACS 5-Year Profile): To obtain geographic information, specifically state and county FIPS codes and county names, I accessed the Census Bureau's API, focusing on the 5-year American Community Survey (ACS) Profile data for 2020.

2) Code Structure and Functions: I structured the script using modular functions to enhance readability and maintainability:

* get_state_fips(): Fetched state FIPS codes and names from the Census API.
* get_county_fips(state_fips): Fetched county FIPS codes and names for a given state from the Census API.
* fetch_candidates(): Fetched candidate metadata (names, parties) from Politico's API.
* fetch_all_results(): The main function orchestrating the entire scraping process, fetching election results for all states, integrating candidate and geographic data, and writing the output to a CSV file.
* test_simplified_census_api_request(): A test function to verify the Census API connectivity.
  
3) Handling "Unknown" Candidates: During development, I encountered an issue where candidate names and parties were not always being correctly populated in the output. Through debugging and careful examination of the API responses, I discovered that the candidate IDs from the election results data needed a specific prefix ("ap:pol:") to match the keys in the candidate metadata. I implemented this prefix addition to correctly link candidate results with their metadata. Additionally, I implemented logic to categorize candidates not found in the metadata as "Other" and aggregate their votes at the county level, providing a more complete picture of the election outcomes.

4) Error Handling: Robust error handling was incorporated using try-except blocks, particularly when making API requests using the requests library. This ensures the script gracefully handles potential network issues, API errors, or unexpected data formats, preventing crashes and providing informative error messages.

5) CSV Output: The final processed data was written to a CSV file (election_results_all_states.csv), making it easily accessible for further analysis, data visualization, or import into other tools.

Skills Demonstrated:
* Web Scraping and API Interaction: Proficiently used the requests library to interact with both the Politico and Census Bureau APIs, fetching data in JSON format.
* JSON Data Processing: Effectively parsed and navigated JSON responses from APIs using the json library to extract relevant information.
* CSV Data Handling: Utilized the csv library to write structured data into a CSV file, creating a clean and organized output.
* Data Integration: Successfully integrated data from multiple sources (Politico and Census Bureau APIs) by using geographic identifiers (FIPS codes) and candidate IDs to merge and enrich the datasets.
* Data Cleaning and Transformation: Handled data inconsistencies, such as missing prefixes in candidate IDs, and implemented data categorization and aggregation for "Other" candidates.
* Problem-Solving and Debugging: Demonstrated problem-solving skills by identifying and resolving the "Unknown" candidate issue through careful analysis and debugging.
* Code Organization and Modularity: Structured the code into functions, promoting code reusability, readability, and maintainability.
* Error Handling: Implemented error handling to make the script more robust and prevent unexpected crashes.
  
Potential Enhancements:
* Data Visualization: The generated CSV dataset is ideally suited for data visualization and exploration. This data can be readily uploaded and analyzed using popular data visualization platforms such as Tableau or Google Looker (Data Studio). Visualizing the election results alongside demographic data would enable the creation of insightful dashboards and reports, revealing patterns, trends, and geographic distributions in voting behavior. For example, one could create maps showing county-level vote percentages for different candidates, overlaid with demographic characteristics like income levels or population density, to explore potential correlations.
* Expanded Data Collection: Incorporate additional demographic variables from the Census API or other data sources to provide a richer dataset for analysis.
* Automated Updates: Schedule the script to run periodically to fetch updated election results as they become available.
* User Interface: Develop a simple user interface (e.g., using Tkinter or Flask) to make the scraper more user-friendly and allow users to specify parameters or select states of interest.
