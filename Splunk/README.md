# Splunk Analysis

## *Authentication Attempts*

Performed SSH logins from a Kali VM to numerous accounts on a Windows VM to collect logs for both successful and failed attempts.

## *Logs Ingested*

**Windows Event Logs:** Event logs (.evtx) in the Security log on Windows

**Sysmon:** Event logs from Microsoft's Sysinternals

## *Dashboard*

I created three visualizations to create my Splunk dashboard using bar charts and line charts.

**Chart 1:** This chart shows the number of successful and failed logons

**Chart 2:** This chart shows the number of failed logons grouped by username

**Chart 3:** This chart uses a trellis layout to show the login activity timeline per account
