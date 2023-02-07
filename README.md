# LKYGBPC Scraping Tools

Setting up the environment
1. Download the ChromeDriver from https://chromedriver.chromium.org
2. Clone this repository from https://github.com/tanhaoen/lkygbpc_scout
3. In the local folder where the repo is cloned, create a file called ".env", which will store the credentials needed. Create the file in the following format
```
EMAIL=yourlinkedinemail@email.com
PASSWORD=yourlinkedinpassword
WEBDRIVER_PATH=/path/to/webdriver/executable
CB_API_KEY=crunchbase_api_key
```
4. Run the following command in command line to install the required packages
```
conda install requests fuzzywuzzy tqdm selenium bs4

conda install -c conda-forge python-decouple
```

## crunchbase.ipynb
Input data: csv file containing three columns
- name: name of the startup
- country (optional): country of the startup
- summary (optional): brief description of the startup 

Output data: input data plus
- basic_info: name, uuid and description of startup found in Crunchbase
- website: startup company website. Blank (NoneType) if no website found
- funding: latest funding stage of the startup. "UNKNOWN" if no funding can be found
- founders: list of tuples, where each tuple contains information on the founders in the format (name, uuid, linkedin_url, position, year_joined). Missing values are left blank (NoneType)

Instructions for use
1. Change the filepath to that of your input data file without the ".csv" extension.
2. Run all cells until the "Manual Check" cell
3. Running the "Manual Check" cell will require the user to input the index of the matching startup from a list of options. If all options are incorrect, hit "Enter" to return None
4. Run the remaining cells until the "Output" cells
5. Running the first output cell will return pickle files which are easier to load into the linkedin_scraper
6. Running the second output cell will return a formatted Excel file for easy viewing and editing

## linkedin_scraper.ipynb
Input data: output pickle file from the crunchbase notebook

Output data: csv file with similar format as the crunchbase output file, with an additional column containing the either the educational history of a possible eligible founder, or LinkedIn URLs to recheck due to possible errors

Instructions for use
1. Run all cells of the file. It may take about 1-2 hours for a list of 500 founders