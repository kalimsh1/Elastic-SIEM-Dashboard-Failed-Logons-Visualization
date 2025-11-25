# Elastic-SIEM-Dashboard-Failed-Logons-Visualization
Kibana/Elastic dashboard for SIEM Visualization Example 1: Failed Logon Attempts (All Users). Includes step-by-step creation of a dashboard with multiple visualizations, filters, and KQL queries for analyzing Windows failed logon events (event.code 4625).

🔧 Step 1 — Create a New Dashboard

Begin by navigating to Dashboard → Create new dashboard.

📷 Image: create_dashboard.png
(Replace with your actual image path)

🔧 Step 2 — Add the First Visualization

Click Create visualization to start building your Lens view.

📷 Image: create_visualization.png

🔧 Step 3 — Select the Correct Index Pattern

Choose the Windows logs index:

windows*


📷 Image: select_index_pattern.png

🔧 Step 4 — Add Required Filters

Add a filter for failed logon events:

event.code = 4625

📷 Image: filter_event_4625.png

🔧 Step 5 — Choose Visualization Type

Change the visualization from Bar vertical stacked to Table.

📷 Image: choose_table_visualization.png

🔧 Step 6 — Add First Row: Username

Add:

user.name.keyword


Set:

Number of values: 1000

Rank by: Count of records

Direction: Descending

📷 Image: rows_username.png

🔧 Step 7 — Add Second Row: Event Logged By (Host)

Add:

host.hostname.keyword


Set same ranking options.

Rename display label to:

Event logged by


📷 Image: rows_host.png

🔧 Step 8 — Add Logon Type

Add:

winlog.logon.type.keyword


Rename:

Logon Type


📷 Image: rows_logon_type.png

🔧 Step 9 — Set Metrics

Under Metrics → add Count

📷 Image: metrics_count.png

🔧 Step 10 — Exclude Computer Accounts

Computer accounts end with $.
Add either multiple "is not" filters or use a single KQL filter (recommended):

✔ Use This KQL Query:
NOT user.name: *$ AND winlog.channel.keyword: Security


Purpose:

Remove all machine accounts (DC1$, WS001$, etc.)

Ensure only Security channel logs are included

📷 Image: kql_computer_filter.png

🔧 Step 11 — Apply the Filter

Click Update to refresh the view.

📷 Image: kql_update.png

🔧 Step 12 — Review the Final Table

Your visualization should now show:

Username

Host logging the event

Logon type

Number of failed logins

📷 Image: final_table_view.png

🔧 Step 13 — Save the Dashboard

Click Save, enter details such as:

Title: SOC-Alerts

Description: Dashboard created for HTB SOC Analyst Job-Role Path

Enable: Store time with dashboard

📷 Image: save_dashboard.png
