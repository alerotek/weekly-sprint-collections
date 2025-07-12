Weekly Sprint Collections Automation
A Google Apps Script–based system for automating weekly account recovery tracking and reporting for TSE teams at d.light Kenya. Designed by Kevin Munje, this tool introduces structured workflows, daily performance tracking, and automated reporting to improve recovery performance across the Coastal region.

1. Overview
The Weekly Sprint Collections Automation is built on Google Sheets and Apps Script, enabling TSEs to log accounts worked, payments made, and recovery progress across a defined 10-day sprint. It generates automatic performance reports, helping both field teams and managers stay aligned on collection goals.

2. Problem Statement
Before this system:

TSEs tracked recoveries manually or inconsistently

Line Managers lacked real-time visibility into team progress

There was no standard way to measure daily effort and outcomes

Team-level reporting was tedious and error-prone

3. Solution
This project introduces a structured solution by:

Enforcing data validation rules in the worksheet

Recording timestamps for each activity

Auto-generating a 10-day sprint performance report

Visualizing top performers and delinquency coverage

Allowing a sprint reset at the end of each cycle

4. Sheet Structure
The system uses a worksheet named WEEKLY-SPRINT_COLLECTIONS with the following columns:

Column	Description
A	TSE Name
B	Account Number (required before logging payments)
E	Delinquency Category – dropdown used to mark cluster accounts worked on
F	Catch-up Balance
G	Amount Paid
H	Auto-calculated: Catch-up - Paid (locked from manual input)
J	Timestamp (auto-generated on valid entry)

Column E is a dropdown that allows tagging accounts by delinquency cluster. This is crucial for guiding line managers in setting focused collection goals.

5. Script Features
5.1 onEdit(e) – Data Validation Logic
Prevents direct edits in column H

Enforces input sequence: B → F → G

Allows only numeric values in columns B, F, G

Automatically calculates H = F - G

Inserts timestamp in column J when B, F, or G is edited

5.2 generateSprintReport() – Performance Email
Tracks performance over a 10-day sprint (7/7/2025 – 7/16/2025)

Calculates:

Daily accounts worked and amounts collected

Per-TSE collection totals and daily summaries

Top 3 performers

Automatically sends an HTML email with the report to TSEs and managers

5.3 setBlueConditionalFormattingOnColH()
Highlights column H in blue when the catch-up balance is cleared (≤ 0)

5.4 clearSprintData()
Clears TSE input data (columns B–J)

Preserves:

TSE names (column A)

Delinquency category (column E)

Formatting and formulas

6. How to Use / Deploy
6.1 Manual Setup (No GitHub Required)
Open your Google Sheet.

Go to Extensions > Apps Script.

Paste in each function from the script collection.

Save and authorize the script.

Set the following triggers:

generateSprintReport: Time-driven (e.g., every day at 7:10AM)

setBlueConditionalFormattingOnColH: Run once manually

clearSprintData: Run after the sprint ends

7. Optional GitHub Deployment
7.1 Clone This Repository
bash
Copy
Edit
git clone https://github.com/alerotek/weekly-sprint-collections.git
cd weekly-sprint-collections
7.2 Use Clasp (Command Line Apps Script)
Install clasp if not already installed:

nginx
Copy
Edit
npm install -g @google/clasp
Login and push code:

pgsql
Copy
Edit
clasp login
clasp create --title "Weekly Sprint Collections" --type sheets
clasp push
clasp open
8. Sample Report Output
Example HTML report contains:

Sprint period header

Daily team totals (accounts & collections)

Top 3 collectors

Individual TSE summaries with daily and weekly breakdown

Remarks based on daily averages (e.g., “Outstanding performance” or “Low activity”)

9. Project Info
Author: Kevin Munje

Company: d.light Kenya

Region: Coastal Recovery Team

Use Case: Recovery sprint management & reporting

Special thanks to the TSEs and field managers who helped test and improve the system.

10. License
For internal use and educational reference. Attribution required for reuse.

11. Resources
Live Sheet: https://docs.google.com/spreadsheets/d/1-1uqBqzAqnfZlGZgQIspN3uK_xjZEjAOoRsQ9Zmcezs/edit?usp=sharing

GitHub Repo: https://github.com/alerotek/weekly-sprint-collections

