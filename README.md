# Exploring Your Ecommerce Dataset with SQL in Google BigQuery Project

I worked with a newly available e-commerce dataset that contains millions of Google Analytics records for the Google Merchandise Store, all loaded into a table in BigQuery.
For this project, I used a copy of that dataset to explore various scenarios and conduct data analysis. 
My main focus was identifying and removing duplicate information, followed by performing further analysis on the data to gain insights.

## Objectives
In this lab, I used BigQuery to:
- Access the e-commerce dataset
- Review the dataset's metadata
- Remove duplicate entries
- Write and execute SQL queries to analyze the data

---

### Task 1: Pin the lab project in BigQuery
1. BigQuery public datasets are not displayed by default in the BigQuery web UI. To open the public datasets project, I copied and 'starred' `data-to-insights`.

---

### Task 2: Explore e-commerce data and identify duplicate records

**Scenario**: The data analyst team exported the Google Analytics logs for the e-commerce website into BigQuery and created a new table containing all the raw e-commerce visitor session data.
#### Explore the `all_sessions_raw` table data:

1. I clicked the Expand node icon near `data-to-insights` to expand the project.
2. Expand `ecommerce`.
3. Clicked `all_sessions_raw`.

SCREENSHOT 1[]()

In the right pane, I was presented with 3 views of the table data:

Schema Tab: Shows field names, types, modes, and descriptions, along with logical constraints used to organize the data.
Details Tab: Displays the table's metadata.
Preview Tab: Allows a preview of the table data.

By previewing sample rows from the table, I was able to get a sense of the data's structure.

To see sample rows without writing SQL, I clicked the preview tab. While scanning through the rows, 
I noticed there wasn’t a singular field that uniquely identified each row, so I knew I would need advanced logic to identify duplicate rows.

SCREENSHOT

The query I used applied the SQL GROUP BY function on every field and counted (COUNT) rows where the same values appeared across all fields:

If all fields were unique, the COUNT would return 1, indicating no duplicate rows.
If there were rows with identical values across all fields, they would be grouped, and the COUNT would be greater than 1.
I then applied a HAVING clause to filter results and show only the rows where the COUNT was greater than 1, identifying the duplicates.

When I ran the query, I discovered that there were 615 records with duplicate data.

SCREENSHOT

Analyze the New all_sessions Table
Scenario: The data analyst team provided me with a deduplicated table called all_sessions, and schema experts identified the key fields that must be unique for each record.

I ran a query to ensure that the data met the expected schema and didn't contain duplicates for the key fields identified:

SCREENSHOT

This query returned zero records, meaning that there were no duplicate rows for the key fields.

### Task 3: Write Basic SQL on E-commerce Data
In this section, I wrote SQL queries to extract insights from the e-commerce dataset.

Query for Total Unique Visitors
I wrote a query to determine the total number of product views and the number of unique visitors.

1. I clicked the + (Compose New Query) icon.
2. I wrote the following query:

SCREENSHOT

3. I ensured the syntax was correct by confirming the real-time query validator showed the Green check icon.
4. I ran the query and reviewed the results to view the number of unique visitors.

Query for Unique Visitors by Referring Site
Next, I wrote a query to find the total number of unique visitors grouped by the referring site (channelGrouping):

SCREENSHOT

Query for Unique Product Names Alphabetically
I then created a query to list all unique product names (v2ProductName) in alphabetical order:

SCREENSHOT

This query returned a total of 633 products (rows).

Query for the Five Products With Most Views
I wrote a query to find the top five products with the most views, including products that may have been viewed multiple times:

SCREENSHOT

Bonus: Refined Query to Avoid Double-Counting Product Views
To refine the analysis, I modified the query to count each product view only once per visitor:

SCREENSHOT

Query for Distinct Products Ordered and Total Units Ordered
Next, I expanded the query to include the number of distinct products ordered and the total quantity of products ordered:

SCREENSHOT

Query for Average Product per Order
Finally, I wrote a query to calculate the average number of products ordered per order:

SCREENSHOT

This concludes my analysis of the e-commerce dataset using SQL in Google BigQuery.
I was able to explore the data, identify duplicates, and write several queries to gain insights into the website’s performance and product trends.



