# Elastic-SIEM-Dashboard-Failed-Logons-Visualization
Kibana/Elastic dashboard for SIEM Visualization Example 1: Failed Logon Attempts (All Users). Includes step-by-step creation of a dashboard with multiple visualizations, filters, and KQL queries for analyzing Windows failed logon events (event.code 4625).

🔧 Step 1 — Create a New Dashboard

Begin by navigating to Dashboard → Create new dashboard.

<img width="1919" height="773" alt="Screenshot 2025-11-24 135254" src="https://github.com/user-attachments/assets/1c069b79-1b0a-4ec2-a981-a1d66ba0056b" />


🔧 Step 2 — Add the First Visualization

Click Create visualization to start building your Lens view.

<img width="1919" height="777" alt="Screenshot 2025-11-24 135326" src="https://github.com/user-attachments/assets/abd706ec-6aad-4622-815a-383ed74ed592" />


🔧 Step 3 — Select the Correct Index Pattern

Choose the Windows logs index:

windows*

<img width="1263" height="783" alt="Screenshot 2025-11-24 135515" src="https://github.com/user-attachments/assets/e166bba7-1b75-4d3b-bc55-8b7b59fa9a14" />

🔧 Step 4 — Add Required Filters

Add a filter for failed logon events:

event.code = 4625

<img width="944" height="550" alt="Screenshot 2025-11-24 135654" src="https://github.com/user-attachments/assets/510062c4-59f1-4078-b131-0920a2c749d8" />

🔧 Step 5 — Choose Visualization Type

Change the visualization from Bar vertical stacked to Table.

<img width="736" height="557" alt="Screenshot 2025-11-24 140054" src="https://github.com/user-attachments/assets/0483d2fa-5997-4ff0-ab41-cae7acc7ffbe" />


🔧 Step 6 — Add First Row: Username

Add:

user.name.keyword


Set:

Number of values: 1000

Rank by: Count of records

Direction: Descending

<img width="974" height="958" alt="Screenshot 2025-11-24 140202" src="https://github.com/user-attachments/assets/6be7aa6a-ec7b-40ff-afdb-2513d0d736ed" />
<img width="983" height="969" alt="Screenshot 2025-11-24 140226" src="https://github.com/user-attachments/assets/0a9f081f-3280-4361-84ae-9cfa08b05c15" />


🔧 Step 7 — Add Second Row: Event Logged By (Host)

Add:

host.hostname.keyword


Set same ranking options.

Rename display label to:

Event logged by


<img width="974" height="958" alt="Screenshot 2025-11-24 140202" src="https://github.com/user-attachments/assets/a05dc8ad-38b5-4a4c-a3c4-97b9dac4cb11" />

🔧 Step 8 — Add Logon Type

Add:

winlog.logon.type.keyword


Rename:

Logon Type


<img width="474" height="556" alt="Screenshot 2025-11-24 141941" src="https://github.com/user-attachments/assets/d075fb13-cc1b-4acc-8a9d-0395180c72b6" />

🔧 Step 9 — Set Metrics

Under Metrics → add Count

<img width="962" height="332" alt="Screenshot 2025-11-24 140701" src="https://github.com/user-attachments/assets/82825027-1941-4f6d-ba32-0c4c06514202" />
<img width="979" height="901" alt="Screenshot 2025-11-24 140731" src="https://github.com/user-attachments/assets/4591a07f-9a94-4886-9616-1578d8485282" />


🔧 Step 10 — Exclude Computer Accounts

Computer accounts end with $.
Add either multiple "is not" filters or use a single KQL filter (recommended):

✔ Use This KQL Query:
NOT user.name: *$ AND winlog.channel.keyword: Security


Purpose:

Remove all machine accounts (DC1$, WS001$, etc.)

Ensure only Security channel logs are included

<img width="474" height="556" alt="Screenshot 2025-11-24 141941" src="https://github.com/user-attachments/assets/cecbfbda-48f6-4453-ad13-74c688b92b1f" />


🔧 Step 11 — Apply the Filter

Click Update to refresh the view.

<img width="978" height="536" alt="Screenshot 2025-11-24 144120" src="https://github.com/user-attachments/assets/07bf9b14-1900-4912-8867-95d2ca131f1d" />

🔧 Step 12 — Review the Final Table

Your visualization should now show:

Username

Host logging the event

Logon type

Number of failed logins

<img width="978" height="549" alt="Screenshot 2025-11-24 144141" src="https://github.com/user-attachments/assets/d93cd6a1-a4c0-418b-8b65-19aad7e4a2ba" />

🔧 Step 13 — Save the Dashboard

Click Save, enter details such as:

Title: SOC-Alerts

Description: Dashboard created for HTB SOC Analyst Job-Role Path

Enable: Store time with dashboard

<img width="982" height="544" alt="Screenshot 2025-11-24 142343" src="https://github.com/user-attachments/assets/d765a74f-ca3c-4b3b-ab2c-1000e839003d" />
