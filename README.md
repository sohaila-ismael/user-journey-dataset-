# Extracting User Journey Data with SQL

## Introduction
This project focuses on analyzing the pre-purchase behavior of users to understand how they navigate the company's website before making their first subscription purchase. The extracted user journey data will help marketing teams improve customer experience and optimize conversion rates.

## Project Objectives
The key objectives of this project are:
- Identify users who made their first subscription purchase between January 1, 2023, and March 31, 2023.
- Extract the sequence of web pages visited by each user before their first purchase.
- Group all visited pages into a user journey string for each session.
- Filter out test users (who paid $0 for their subscriptions).
- Replace raw URLs with readable aliases for better clarity.

## Project Requirements
The following tools and resources were used for the project:
- MySQL Workbench 8.0 or later: For database management and query execution.
- Database schema: The schema includes the student_purchases, front_visitors, and front_interactions tables, which can be generated using the User_Journey_Database.sql file.
- URL_Aliases.xlsx: A reference file to replace long URLs with human-readable aliases.

## Data Overview
The project works with the following database tables:
- student_purchases: Contains user purchase data, including user_id, purchase_type, purchase_price, and date_purchased. Only users with a purchase date in Q1 2023 and a purchase price greater than $0 are included.
- front_visitors: Maps visitor_id to user_id. Users who never made a purchase are excluded.
- front_interactions: Logs all interactions (e.g., page visits) made by visitors. Each entry includes visitor_id, session_id, event_source_url, event_destination_url, and event_date.

## Analysis Approach
The following steps outline the approach used in the SQL queries:

1. Filter Subscription Data:
   - Identify users who made their first subscription purchase between January 1, 2023, and March 31, 2023.
   - Exclude test users by filtering out those with a purchase price of $0.
   - Classify subscription types as 'monthly', 'quarterly', or 'annual'.

2. Join Interaction Data:
   - Join interaction data for the filtered users and extract all web events before the first purchase date.

3. Create URL Aliases:
   - Use the provided URL aliases to simplify event source and destination URLs.
   - Replace long URLs with human-readable names like "Homepage", "Login", "Sign up", etc.

4. Concatenate User Journeys:
   - Combine the source and destination URLs of each user interaction within a session into a single string.
   - Use GROUP_CONCAT to concatenate all interactions in a session into one journey string, separating each page visit with a hyphen (-).

5. Output User Journeys:
   - The final output includes user_id, session_id, subscription_type, and user_journey, which represents the ordered sequence of pages visited by the user before their first purchase.

## Connecting to the Database
To connect to the MySQL database and run the SQL queries, use the following code:

```python
%load_ext sql
%sql mysql+pymysql://root:100200300@localhost:3306/user_journey_data
```
## Conclusion
This project effectively analyzes user journey data before their first subscription purchase. The insights generated from the sequence of web interactions will help marketing teams improve user experience and enhance conversion rates by understanding
