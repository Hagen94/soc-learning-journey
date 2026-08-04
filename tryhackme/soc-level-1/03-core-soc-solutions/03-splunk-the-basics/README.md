# Splunk: The Basics

## Overview

This room introduces the fundamentals of **Splunk**, a SIEM solution used to collect, analyze, and correlate network and machine logs in real time.

It focuses on the main components of Splunk, the Splunk interface, log ingestion, and the practical process of uploading and analyzing log data.

The room also introduces the **Search Processing Language (SPL)**, which is used to search and analyze indexed data.

---

## Learning Objectives

After completing this room, I am able to:

* Understand the main components of Splunk.
* Explain the role of the Forwarder, Indexer, and Search Head.
* Navigate the Splunk interface.
* Understand how data is ingested into Splunk.
* Upload log files into Splunk.
* Configure basic input settings.
* Search indexed events.
* Understand field-value pairs in Splunk.
* Use basic SPL searches to analyze logs.
* Use `spath` to parse JSON fields.
* Use statistical commands to analyze search results.

---

# Splunk Architecture

Splunk has three main components:

```text id="sp01"
             DATA SOURCES
                  │
                  ▼
             FORWARDER
                  │
                  ▼
              INDEXER
                  │
                  ▼
             SEARCH HEAD
                  │
                  ▼
              ANALYST
```

These components work together to collect, process, store, search, and analyze data.

---

# Splunk Forwarder

The **Splunk Forwarder** is a lightweight agent installed on the endpoint being monitored.

Its main purpose is to:

* Collect data.
* Send data to the Splunk instance.
* Forward information from different log sources.

The room describes it as requiring only a small amount of resources on the endpoint.

### Example Data Sources

A Forwarder can collect data from:

* Web servers generating web traffic.
* Windows machines generating Windows Event Logs, PowerShell, and Sysmon data.
* Linux hosts generating host-centric logs.
* Databases generating connection requests, responses, and errors.

The Forwarder sends the collected data to the **Splunk Indexer**.

---

# Splunk Indexer

The **Splunk Indexer** processes the data received from Forwarders.

Its responsibilities include:

* Processing incoming data.
* Parsing data.
* Normalizing data into field-value pairs.
* Categorizing data.
* Storing processed data as events.

The processed data can then be searched and analyzed through the Search Head.

---

# Splunk Search Head

The **Search Head** is the component where users search and analyze indexed logs.

Splunk uses **Search Processing Language (SPL)** to search indexed data.

When a search is performed:

```text id="sp02"
Analyst
   │
   ▼
Search Head
   │
   ▼
Indexer
   │
   ▼
Relevant Events
   │
   ▼
Search Head
```

The Search Head can also transform search results into visualizations such as:

* Tables
* Pie charts
* Bar charts
* Column charts

---

# Navigating Splunk

The Splunk home interface contains several important areas.

## Splunk Bar

The Splunk Bar provides access to:

* Messages
* Settings
* Activity
* Help
* Find

It also allows users to switch between installed Splunk applications.

---

## Apps Panel

The Apps Panel displays the applications installed on the Splunk instance.

The default application is:

**Search & Reporting**

---

## Explore Splunk

The Explore Splunk section provides quick access to:

* Add data.
* Add Splunk apps.
* Splunk documentation.

---

## Splunk Dashboard

The Home Dashboard provides access to available dashboards.

Users can:

* Select existing dashboards.
* Create new dashboards.
* View their own dashboards through the **Yours** tab.

---

# Adding Data to Splunk

Splunk can ingest different types of data, including:

* Event logs.
* Website logs.
* Firewall logs.
* VPN logs.

When data is added to Splunk, it is processed and transformed into individual events.

The room uses **VPN logs** as the practical example.

---

# Uploading Log Data

The room demonstrates how to upload a local log file using the Splunk upload option.

The upload process consists of five steps:

```text id="sp03"
1. Select Source
        ↓
2. Select Source Type
        ↓
3. Input Settings
        ↓
4. Review
        ↓
5. Done
```

### 1. Select Source

Select the log file and identify the data source.

### 2. Select Source Type

Specify the type of data being ingested, such as:

* JSON
* Syslog

### 3. Input Settings

Configure:

* The index where the logs will be stored.
* The hostname associated with the logs.

### 4. Review

Review the configuration before importing the data.

### 5. Done

Complete the upload so the data becomes available for analysis.

---

# JSON Log Ingestion

The practical exercise uses a `VPN_logs` file containing **newline-delimited JSON**.

Splunk should treat each line as an individual event.

The documented process is:

```text id="sp04"
Add Data
   ↓
Upload
   ↓
Select VPN_logs
   ↓
JSON Source Type
   ↓
Input Settings
   ↓
VPN_Logs Index
   ↓
Search & Reporting
```

The room specifies creating or selecting the `VPN_Logs` index and setting the time picker to **All time** after uploading the data.

---

# SPL and Searching Data

**Search Processing Language (SPL)** is used to search and analyze indexed data in Splunk.

A basic search can specify an index:

```text id="sp05"
index=VPN_Logs
```

This searches events stored in the `VPN_Logs` index.

---

# Parsing JSON with spath

When JSON field names do not automatically appear in search results, the room introduces the `spath` command.

Example:

```text id="sp06"
index=VPN_Logs
| spath
```

`spath` tells Splunk to parse the JSON fields contained within each event.

This allows fields such as `UserName` and `Source_ip` to be searched directly.

---

# Filtering Events

Once fields are available, they can be used to search for specific values.

### Example

```text id="sp07"
index=VPN_Logs
| spath
| search UserName="Maleena"
| stats count
```

This searches the `VPN_Logs` index, parses the JSON fields, filters events associated with the user `Maleena`, and counts the results.

Another example from the room searches for a specific source IP:

```text id="sp08"
index=VPN_Logs
| spath
| search Source_ip="107.14.182.38"
| stats values(UserName) as UserName count
```

This can be used to identify the associated username and count the matching events.

---

# Statistical Analysis

Splunk can use statistical commands to summarize search results.

The room demonstrates the use of:

```text id="sp09"
| stats count
```

and:

```text id="sp10"
| stats values(UserName) as UserName count
```

These commands allow an analyst to summarize the results of a search instead of reviewing every event individually.

---

# Example Investigation Searches

The room provides several searches that can be used to analyze the imported VPN logs.

### Count all events

```text id="sp11"
index=VPN_Logs
| stats count
```

### Search for a specific user

```text id="sp12"
index=VPN_Logs
| spath
| search UserName="Maleena"
| stats count
```

### Identify a user associated with an IP

```text id="sp13"
index=VPN_Logs
| spath
| search Source_ip="107.14.182.38"
| stats values(UserName) as UserName count
```

### Search for activity outside France

```text id="sp14"
index=VPN_Logs
| spath
| search Source_Country!="France"
| stats count
```

### Search for a specific source IP

```text id="sp15"
index=VPN_Logs
| spath
| search Source_ip="107.3.206.58"
| stats count
```

These examples demonstrate how an analyst can move from a general dataset to targeted searches and statistical summaries.

---

# Splunk Investigation Workflow

The main concepts from this room can be connected through the following workflow:

```text id="sp16"
             LOG SOURCE
                  │
                  ▼
             FORWARDER
                  │
                  ▼
              INDEXER
                  │
       Parse / Normalize / Store
                  │
                  ▼
            SEARCH HEAD
                  │
                  ▼
                 SPL
                  │
                  ▼
             SEARCH RESULTS
                  │
                  ▼
             ANALYST
```

This workflow shows how Splunk moves data from its original source to a format that can be searched and analyzed by a SOC analyst.

---

# Splunk and SIEM

Splunk provides many of the capabilities expected from a SIEM platform:

* Centralized log collection.
* Log processing.
* Data normalization.
* Event storage.
* Search capabilities.
* Data analysis.
* Visualization.

For a SOC analyst, this creates a centralized location from which security-related activity can be investigated.

---

# Splunk in the SOC

A SOC L1 analyst can use Splunk to:

* Search security logs.
* Investigate suspicious activity.
* Identify users associated with events.
* Investigate source IP addresses.
* Filter events.
* Count occurrences.
* Identify unusual activity.
* Support alert investigations.

The ability to search large amounts of indexed data is particularly useful when investigating security events.

---

# Skills Acquired

This room strengthened my understanding of:

* Splunk
* SIEM architecture
* Splunk Forwarder
* Splunk Indexer
* Splunk Search Head
* Search Processing Language (SPL)
* Splunk navigation
* Log ingestion
* Data indexing
* Log normalization
* Field-value pairs
* JSON log analysis
* `spath`
* `stats`
* Search filtering
* Splunk dashboards
* VPN log analysis

---

# Analyst Notes

## Key Takeaways

* Splunk is a SIEM solution capable of collecting, analyzing, and correlating logs.
* Splunk has three main components: Forwarder, Indexer, and Search Head.
* The Forwarder collects data from monitored endpoints and sends it to the Indexer.
* The Indexer processes, normalizes, categorizes, and stores the data as events.
* The Search Head provides the interface for searching indexed data.
* SPL is used to search and analyze Splunk data.
* Splunk can ingest different types of logs, including VPN, firewall, web, and system logs.
* Imported data is processed into individual events.
* The upload process includes source selection, source type, input settings, review, and completion.
* JSON data can be parsed using `spath`.
* Statistical commands such as `stats count` can summarize search results.
* Splunk provides centralized visibility that can support SOC investigations.

---

## New Terminology

* Splunk
* Forwarder
* Indexer
* Search Head
* SPL
* Search Processing Language
* Index
* Event
* Log Ingestion
* Log Normalization
* Field-Value Pair
* `spath`
* `stats`
* Dashboard

---

## Personal Reflection

This room gave me a practical introduction to how a SIEM can be used by a SOC analyst.

The most important concept for me was understanding the relationship between the three main Splunk components. The **Forwarder** collects the data, the **Indexer** processes and stores it, and the **Search Head** allows analysts to search and analyze the resulting events.

The practical exercise also helped me understand that working with a SIEM requires more than simply viewing logs. An analyst needs to know how data is structured, how to search specific fields, and how to use commands such as `spath` and `stats` to extract useful information.

This provides a foundation for more advanced Splunk investigations and incident-handling exercises.

---

## References

* TryHackMe — SOC Level 1
* Splunk: The Basics room
