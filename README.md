# Data Task

This is a task designed to assess your ability to query, assess and manipulate raw data in SQL. This repository contains two datasets, in CSV format:

### 1. An account level dataset `sample_accounts.csv`
This represents a list of companies which exist in a customer relationship management system. These may be prospective customers for one of Momentum's customers. These may have been generated
from inbound requests, and have not had any cleaning or quality checks associated with them.

### 2. A linkedin company level dataset `sample_jobs.csv`
This is the result of scraping company pages from LinkedIn, and storing job metadata in a JSON column where it is found.
Note that this is a raw output of linkedin scraping technology, and may contain duplicates, or other issues.

### Output

Your task is to return a clean set of accounts, which could be delivered to a Momentum customer, with a calculated account score. We intend to deliver
clean, consistent data, with only one record per account. We are not interested in representing the same company multiple times, and
we do not want to include subsideries or other entities which are not the main company.

The columns in the output should include:

- website
- name
- headcount
- number of jobs
- number of remote jobs
- remote first (a boolean flag, true if >50% of jobs are remote)
- account score (a compound score based on the following rules)


### Account score rules



| Headcount | Score |
| -------------- | --------- |
| 0-10           |     0      |
| 10-50          | 1         |
| 50-100         | 3         |
| 100-300        | 5         |
| 300-500        | 2         |
| 500-1000       |      0     |
| 1000-2000      |       0    |
| 2000-5000      |0|


| Open remote roles | Score|
| ----------------------- | --------- |
| 0           |    0       |
| 1-5                     | 20        |
| 6+                      | 30        |


| Open roles | Score|
| ----------------------- | --------- |
| 0  |  0         |
| 1-10           | 10        |
| 11+           | 15        |

The account score should be the sum of the above rules.


The supplied tables are in a CSV format. These should be loaded into a SQL-based database of your choice.

The task submission should be one or more SQL files used to deliver the final output from the supplied raw data.

