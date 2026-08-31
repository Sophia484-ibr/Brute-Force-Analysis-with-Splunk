\# Brute Force Detection Using Splunk



\## Overview



This project demonstrates the detection and investigation of suspected brute-force login activity using Splunk and Windows Security Event Logs.



The project focuses on identifying repeated failed login attempts, analyzing the accounts being targeted, and identifying the source network addresses associated with the failed authentication attempts.



\## Objective



The objective of this project is to use Splunk to detect and investigate repeated failed authentication attempts that may indicate a brute-force attack.



The project demonstrates how Windows Security logs can be analyzed to identify suspicious login activity, determine the accounts being targeted, and identify the source network addresses associated with the activity.



\## Tools Used



\* \*\*Splunk Enterprise\*\* – SIEM platform used for log collection, searching, analysis, and dashboard creation.

\* \*\*Windows Security Event Logs\*\* – Source of authentication events analyzed in the project.

\* \*\*Windows Event ID 4625\*\* – Used to identify failed login attempts.

\* \*\*Windows environment\*\* – Used to generate and collect the authentication logs.



\## Environment



The project was performed in a Windows environment with Windows Security logs being ingested into Splunk.



The logs were analyzed using Splunk Search \& Reporting, and the results were used to create a brute-force detection dashboard.



\## Detection Methodology



The detection process focused on Windows failed authentication events recorded as \*\*Event ID 4625\*\*.



The investigation followed these steps:



1\. \*\*Identify failed authentication events\*\*

&#x20;  Splunk was searched for Windows Security Event ID 4625, which represents a failed logon attempt.



2\. \*\*Analyze failed login activity\*\*

&#x20;  The number of failed authentication attempts was analyzed to identify repeated login failures.



3\. \*\*Identify targeted accounts\*\*

&#x20;  Failed login attempts were grouped by account name to determine which accounts were being targeted.



4\. \*\*Identify source network addresses\*\*

&#x20;  Events were grouped by source network address to identify the systems generating the failed authentication attempts.



5\. \*\*Identify potential brute-force activity\*\*

&#x20;  A high number of failed login attempts from the same source against an account was treated as an indicator of possible brute-force activity.



6\. \*\*Visualize the activity\*\*

&#x20;  The results were presented in a Splunk dashboard to make suspicious authentication activity easier to monitor and investigate.



\## Splunk Queries



The following SPL queries were used to analyze Windows Security Event ID 4625 and identify patterns of repeated failed authentication attempts.



The complete set of queries used in this project is available in \[`splunk\_queries.txt`](splunk\_queries.txt).



\### Failed Login Events



```spl

index=\* sourcetype="WinEventLog:Security" EventCode=4625

```



This query retrieves failed Windows authentication events.



\### Failed Logins by Account



```spl

index=\* sourcetype="WinEventLog:Security" EventCode=4625

| stats count by Account\_Name

| sort - count

```



This groups failed login attempts by account to identify accounts receiving repeated authentication failures.



\### Failed Logins by Source Network Address



```spl

index=\* sourcetype="WinEventLog:Security" EventCode=4625

| stats count by Source\_Network\_Address

| sort - count

```



This identifies the source network addresses generating the highest number of failed login attempts.



\### Failed Logins by Source and Account



```spl

index=\* sourcetype="WinEventLog:Security" EventCode=4625

| stats count by Source\_Network\_Address, Account\_Name

| sort - count

```



This query combines the source network address and targeted account to help investigate potential brute-force activity.



\## Dashboard



A Splunk dashboard was created to provide a visual overview of failed authentication activity and help identify potential brute-force attempts.



The dashboard presents the analyzed login activity in a more accessible format, allowing an analyst to quickly review failed authentication patterns, targeted accounts, and source network addresses.



\### Dashboard Screenshot



!\[Brute Force Detection Dashboard](screenshots/dashboard.png)

\### Failed Login Events



The following screenshot shows the Windows Security failed authentication events identified in Splunk using Event ID 4625.



!\[Failed Login Events](screenshots/brute\_force\_events.png)





\## Investigation



The investigation focused on identifying the source network addresses and user accounts associated with repeated failed authentication attempts.



The following SPL query was used:



```spl

index=\* sourcetype="WinEventLog:Security" EventCode=4625

| stats count by Source\_Network\_Address, Account\_Name

| sort - count

```



This allowed the failed login attempts to be grouped by both \*\*Source Network Address\*\* and \*\*Account Name\*\*, making it easier to identify patterns that could indicate brute-force activity.



\### Investigation Screenshot



!\[Brute Force Investigation](screenshots/investigation.png)



\## Findings



The analysis identified repeated failed authentication attempts recorded as Windows Security Event ID 4625.



By grouping the events by account name and source network address, it was possible to identify patterns of repeated authentication failures and determine which accounts and source addresses were associated with the activity.



The results demonstrate how Splunk can be used to detect and investigate authentication activity that may indicate a brute-force attack.



\### Key Observations



\* Windows Security Event ID 4625 provided the failed authentication events used for detection.

\* Failed login attempts could be grouped by \*\*Account Name\*\* to identify targeted accounts.

\* Failed login attempts could be grouped by \*\*Source Network Address\*\* to identify the originating systems.

\* Repeated failures from the same source and against the same account can be treated as a potential brute-force indicator.

\* The Splunk dashboard provided a visual way to monitor and investigate the activity.



\## Recommendations



If similar brute-force activity were detected in a real environment, the following actions could be considered:



\* Investigate the source network address associated with repeated failed login attempts.

\* Verify whether the targeted account activity is legitimate.

\* Review successful logins that occur after multiple failed authentication attempts.

\* Consider implementing account lockout or rate-limiting controls where appropriate.

\* Enforce strong password policies and multi-factor authentication (MFA).

\* Continue monitoring authentication logs for recurring suspicious activity.



\## Skills Demonstrated



\* SIEM log analysis using Splunk

\* Windows Security Event Log analysis

\* Authentication event investigation

\* SPL query development

\* Brute-force attack detection

\* Source network address and account analysis

\* Security dashboard creation

\* Basic SOC investigation and incident analysis



\## Conclusion



This project demonstrated how Splunk can be used to monitor and investigate failed authentication activity in a Windows environment.



By analyzing Event ID 4625 and correlating failed login attempts with account names and source network addresses, potential brute-force activity can be identified and investigated.



The project provided practical experience with SIEM-based detection, log analysis, SPL, and security monitoring workflows commonly used by SOC analysts.



