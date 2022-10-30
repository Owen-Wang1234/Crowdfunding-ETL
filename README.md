# Crowdfunding-ETL

## Project Overview
A client has requested an analysis of the collected crowdfunding data. The main crowdfunding data is stored in an Excel spreadsheet file with two sheets, and the backers information data is stored in a CSV file; all the data needs to be extracted and cleaned before loading into a SQL database for analysis.

## Resources
### Data Sources:
- crowdfunding.xlsx
- backer_info.csv

### Software:
- PythonData Environment:

	1. Python 3.7.13
	2. Jupyter Notebook 6.4.8
	3. Pandas 1.3.5
	4. Numpy 1.21.5

- Python 3 Environment:

	1. Python 3.9.13
	2. Jupyter Notebook 6.4.12
	3. Pandas 1.4.4
	4. Numpy 1.21.5

- Database Analysis:

	1. pgAdmin 4 6.12
	2. PostgreSQL14.5

## Data Processing
### Extraction and Transformation
The data files are first imported into DataFrames in Python and checked for faulty data. The crowdfunding data gets the `category & sub-category` column split so that the categories and subcategories can be extracted to form their own DataFrames with their assigned IDs to be exported into CSV files.

- Export 1: categories.csv
- Export 2: subcategories.csv

The contact info DataFrame and the backers info DataFrame are set up by extracting the necessary information from the long lines of strings. This is done either by iteratively converting the line in each row into a dictionary and then iterating through the dictionary to extract the keys and values with list comprehension, or by running through the lines using regular expressions.

### Transformation
When working on the crowdfunding DataFrame, a few columns get renamed and some columns get converted to a different data type. The previously extracted DataFrames for the category and subcategory are merged back in, and some unnecessary columns get dropped. The `contact_id` is extracted from the contact information DataFrame, added to the crowdfunding DataFrame, and converted into an integer data type. Then the columns get reordered before exporting into a CSV file.

- Export 3: campaign.csv

The contact info DataFrame and backers info DataFrame have the name column split into first name and last name with the name column dropped afterwards. The columns are then reordered before exporting into CSV files.

- Export 4: contacts.csv
- Export 5: backers.csv

### Loading
With the exported CSV files ready, the Entity Relationship Diagram (ERD) is drawn up to illustrate the tables, their columns, and how they relate to each other. The diagram and schema are exported for reference and future use.

- Export 6: crowdfunding_db_relationships.png
- Export 7: crowdfunding_db_schema.sql

The exported schema script is run through the SQL system to create the tables. All the data are imported from the CSV files to their respective tables. A quick verification check makes sure the data are all imported properly.

### Images
<p align = "center">
![The database illustration](https://github.com/Owen-Wang1234/Crowdfunding-ETL/blob/main/crowdfunding_db_relationships.png)

**Figure 1:** The ERD for the Crowdfunding Database

![The category table](https://github.com/Owen-Wang1234/Crowdfunding-ETL/blob/main/Screenshots/category.png)

**Figure 2:** The category table

![The subcategory table](https://github.com/Owen-Wang1234/Crowdfunding-ETL/blob/main/Screenshots/subcategory.png)

**Figure 3:** The subcategory table

![The category table](https://github.com/Owen-Wang1234/Crowdfunding-ETL/blob/main/Screenshots/contacts.png)

**Figure 4:** The contacts table

![The category table](https://github.com/Owen-Wang1234/Crowdfunding-ETL/blob/main/Screenshots/campaign.png)

**Figure 5:** The campaign table

![The category table](https://github.com/Owen-Wang1234/Crowdfunding-ETL/blob/main/Screenshots/backers.png)

**Figure 6:** The backers table
</p>

## Analysis
The analyses conducted on the resulting crowdfunding database are stored as queries in the `crowdfunding_SQL_Analysis.sql` script. The first two queries make a quick check of the database by getting the number of backers for each live crowdfunding project (by `cf_id`) sorted in descending order. This is done in two different ways: The first selects directly from the `campaign` table, and the second aggregates from the `backers` table.

![The count of backers for live projects](https://github.com/Owen-Wang1234/Crowdfunding-ETL/blob/main/Screenshots/backer_counts.png)

The remaining queries come at the request of the client. The first request is to get the full name and email of the contacts for the live projects and the remaining goal amount of those projects. The results are written into a table and exported.

- Export 8: email_contacts_remaining_goal_amount.csv
![Export 8](https://github.com/Owen-Wang1234/Crowdfunding-ETL/blob/main/Screenshots/contacts_rem_goal.png)

The other request is to get the email and full name of the backers for the live projects, the ID number of the backed project, the company name, the description of the project, the end date, and the remaining amount of the goal. The results are written into a table and exported.

- Export 9: email_backers_remaining_goal_amount.csv
![Export 9](https://github.com/Owen-Wang1234/Crowdfunding-ETL/blob/main/Screenshots/backers_rem_goal.png)