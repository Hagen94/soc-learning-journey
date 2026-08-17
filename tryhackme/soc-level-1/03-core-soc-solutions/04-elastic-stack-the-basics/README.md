# Elastic Stack: The Basics

## Overview

This room introduces the **Elastic Stack (ELK)** and its use in log analysis and security investigations.

Although Elastic Stack is not a traditional SIEM, many SOC teams use it similarly because of its capabilities for searching, analyzing, and visualizing large amounts of log data.

The room focuses on the main components of Elastic Stack, log analysis through Kibana, KQL searches, visualizations, and dashboards. The practical investigation uses VPN logs to identify anomalies and suspicious patterns.

---

## Learning Objectives

After completing this room, I am able to:

* Understand the main components of Elastic Stack.
* Explain how Elastic Stack components work together.
* Understand the role of Elasticsearch.
* Understand the role of Logstash.
* Understand the purpose of Beats.
* Understand the role of Kibana.
* Search and filter logs using Kibana.
* Use KQL to perform searches.
* Investigate VPN logs for anomalies.
* Create visualizations from log data.
* Create dashboards to provide centralized visibility into logs.

---

# Elastic Stack Overview

Elastic Stack is a collection of components designed to collect, store, search, and visualize large amounts of data.

The core components covered in this room are:

```text
                 DATA SOURCES
                      │
                      ▼
                    BEATS
                      │
                      ▼
                  LOGSTASH
                      │
                      ▼
                ELASTICSEARCH
                      │
                      ▼
                    KIBANA
                      │
                      ▼
                 SOC ANALYST
```

Each component performs a specific function within the data processing and analysis workflow.

---

# Elastic Stack Components

## Elasticsearch

**Elasticsearch** is a full-text search and analytics engine designed for JSON-formatted documents.

Its main functions include:

* Storing data.
* Analyzing data.
* Correlating data.
* Supporting searches.

It also provides a RESTful API for interacting with the stored data.

---

## Logstash

**Logstash** is a data processing engine.

It can:

* Receive data from different sources.
* Filter data.
* Normalize logs.
* Send processed data to a destination.

A Logstash configuration is divided into three main sections:

```text
Input
  │
  ▼
Filter
  │
  ▼
Output
```

### Input

Defines the source from which data is being ingested.

### Filter

Defines how the incoming data should be filtered or normalized.

### Output

Defines where the processed data should be sent.

Possible destinations include:

* Listening ports.
* Kibana.
* Elasticsearch.
* Files.

Logstash supports multiple Input, Filter, and Output plugins.

---

## Beats

**Beats** are host-based agents, also known as **data-shippers**.

They transfer data from endpoints to Elasticsearch.

Each Beat is designed for a specific type of data.

Examples mentioned in the room include:

* **Winlogbeat** — Windows event logs.
* **Packetbeat** — network traffic flows.

---

## Kibana

**Kibana** is the web-based visualization component of Elastic Stack.

It works with Elasticsearch to:

* Analyze data.
* Investigate data.
* Search data.
* Visualize data streams.
* Create visualizations.
* Create dashboards.

This is the main interface used by SOC analysts when working with Elastic Stack in the room.

---

# How the Components Work Together

The complete data flow can be summarized as:

```text
BEATS
 │
 │ Collect data
 ▼
LOGSTASH
 │
 │ Parse / Normalize
 ▼
ELASTICSEARCH
 │
 │ Store / Search / Analyze
 ▼
KIBANA
 │
 │ Visualize
 ▼
SOC ANALYST
```

The room explains that Beats collect data, Logstash parses and normalizes it into field-value pairs, Elasticsearch stores and allows the data to be searched, and Kibana displays the resulting information through visualizations.

---

# Kibana Discover

The **Discover** tab is the main workspace used by SOC analysts in Kibana.

It provides access to:

* Ingested logs.
* Search functionality.
* Normalized fields.
* Filters.
* Time-based searches.
* Event counts.

Analysts can use Discover to search logs, investigate anomalies, and narrow results using filters and time periods.

---

## Important Discover Components

### Logs

Each row represents an individual log containing information about an event and its associated fields and values.

### Fields Pane

The left panel displays the fields parsed from the available logs.

Fields can be selected to:

* Add filters.
* Remove filters.
* View common values.

### Index Pattern

An index pattern defines which Elasticsearch data Kibana should explore.

Different log sources can have different index patterns.

For the lab, the relevant index pattern is:

```text
vpn_connections
```

### Search Bar

The search bar allows analysts to enter queries and filters.

### Time Filter

The time filter restricts the results to a specific period.

### Timeline

The timeline displays the number of events occurring over time.

### Add Filter

Filters can be applied directly to specific fields without manually writing the entire query.

---

# Index Patterns

Kibana uses index patterns to determine which Elasticsearch data should be explored.

Each index pattern corresponds to defined field properties and can point to multiple indices.

Because different log sources have different structures, the logs are normalized into fields and values when they are ingested.

In the lab, the `vpn_connections` index pattern contains the VPN logs used for investigation.

---

# Fields and Values

The Fields Pane displays the normalized fields available in the logs.

Selecting a field allows the analyst to see its most common values and their occurrence percentages.

These values can then be used to create filters.

```text
Field
  │
  ▼
Available Values
  │
  ▼
Filter
  │
  ▼
Reduced Results
```

This makes it easier to narrow a large dataset down to the events relevant to an investigation.

---

# Time-Based Investigation

The time filter allows analysts to restrict searches to a specific period.

The timeline provides an overview of how many events occurred during different periods.

This can help identify unusual spikes in activity.

For example, the room identifies an unusual log spike on:

```text
11 January 2022
```

This demonstrates how timeline analysis can help identify periods requiring further investigation.

---

# Creating Tables

By default, logs are displayed in their raw form.

Analysts can select important fields and create a table containing only those fields.

This helps:

* Reduce noise.
* Improve readability.
* Make the information more meaningful.
* Present investigation results more clearly.

Saved table configurations can also be reused.

---

# KQL — Kibana Query Language

**KQL (Kibana Query Language)** is the query language used to search ingested logs and documents in Elasticsearch through Kibana.

The room introduces two primary search approaches:

1. Free-text search.
2. Field-based search.

---

# Free-Text Search

Free-text searches look for a term across the available documents regardless of the specific field.

### Example

```text
security
```

This searches for documents containing the term `security`.

The room demonstrates that KQL searches for the complete term. For example, searching:

```text
United
```

does not return the same results as searching:

```text
United States
```

---

## Wildcards

KQL supports the `*` wildcard.

Example:

```text
United*
```

This can return terms beginning with `United`, allowing searches for variations or longer terms containing that prefix.

---

# Logical Operators

KQL supports logical operators that allow analysts to combine or exclude search conditions.

## AND

Both conditions must be present.

```text
"United States" AND "Virginia"
```

---

## OR

Either condition can be present.

```text
"United States" OR "England"
```

---

## NOT

A specific condition can be excluded.

```text
"United States" AND NOT ("Florida")
```

---

# Field-Based Search

Field-based searches specify both the field and the value being searched.

The basic syntax is:

```text
Field: Value
```

### Example

```text
Source_ip : 238.163.231.224 AND UserName : Suleman
```

This searches for logs where:

* `Source_ip` contains `238.163.231.224`
* `UserName` is `Suleman`

---

# Investigating VPN Logs

The practical investigation in this room uses VPN connection logs.

The analyst can use Kibana to:

* Search VPN events.
* Filter specific fields.
* Investigate source IP addresses.
* Investigate usernames.
* Examine connection activity.
* Identify anomalies.
* Identify unusual patterns over time.

This demonstrates how Elastic Stack can be used for security investigations even though it is not presented as a traditional SIEM.

---

# Visualizations

Kibana allows analysts to transform log data into different visual formats.

Examples include:

* Tables.
* Pie charts.
* Bar charts.
* Other visual representations.

Visualizations can also be used to correlate multiple fields.

For example:

```text
Source_IP
    │
    └── Source_Country
```

This can help analysts identify relationships between different pieces of log data.

---

# Saving Visualizations

After creating a visualization, it can be saved to the visualization library.

The room's process is:

```text
Create Visualization
        ↓
      Save
        ↓
Add Title & Description
        ↓
Save to Library
```

Saving visualizations allows them to be reused later and added to dashboards.

---

# Failed VPN Connection Visualization

The room demonstrates creating a visualization focused specifically on failed VPN connection attempts.

The relevant data view is:

```text
vpn_connections
```

The filter is:

```text
action: failed
```

The visualization uses:

* `UserName`
* `Source_ip`

This creates a table showing the users and IP addresses involved in failed VPN connection attempts.

---

# Dashboards

Dashboards combine saved searches and visualizations into a single view.

They provide centralized visibility into a specific type of activity.

For the lab, the dashboard is designed around:

```text
VPN Log Visibility
```

The basic process is:

```text
Saved Searches
      +
Visualizations
      │
      ▼
   Dashboard
      │
      ▼
Centralized Visibility
```

The room demonstrates adding saved searches and visualizations from the library and arranging them within a custom dashboard.

---

# Elastic Stack in the SOC

Elastic Stack can provide SOC analysts with a centralized environment for:

* Searching logs.
* Filtering events.
* Investigating anomalies.
* Identifying suspicious patterns.
* Creating visualizations.
* Building dashboards.

The room specifically emphasizes that SOC analysts primarily work with Elastic Stack for **log analysis and investigations**, rather than needing to specialize in the internal implementation of each component.

---

# Investigation Workflow

The concepts from the room can be represented as:

```text
              LOG SOURCES
                   │
                   ▼
                 BEATS
                   │
                   ▼
               LOGSTASH
                   │
            Parse / Normalize
                   │
                   ▼
             ELASTICSEARCH
                   │
             Store / Search
                   │
                   ▼
                KIBANA
                   │
        ┌──────────┼──────────┐
        │          │          │
     Discover    KQL    Visualizations
        │          │          │
        └──────────┼──────────┘
                   │
                   ▼
              DASHBOARDS
                   │
                   ▼
             SOC ANALYST
```

This represents the complete process from log collection to investigation and visualization.

---

# Skills Acquired

This room strengthened my understanding of:

* Elastic Stack
* ELK
* Elasticsearch
* Logstash
* Beats
* Kibana
* Log collection
* Log normalization
* Index patterns
* Kibana Discover
* Fields and values
* Time-based filtering
* KQL
* Free-text searches
* Field-based searches
* Wildcards
* Logical operators
* VPN log analysis
* Data visualization
* Correlation
* Dashboards

---

# Analyst Notes

## Key Takeaways

* Elastic Stack is designed to collect, store, search, and visualize large amounts of data.
* It is not a traditional SIEM, but many SOC teams use it similarly.
* Elasticsearch stores, searches, analyzes, and correlates data.
* Logstash processes, filters, and normalizes data.
* Beats are host-based agents that transfer data from endpoints.
* Kibana provides the web interface for searching, investigating, and visualizing data.
* The Discover tab is a key workspace for SOC analysts.
* Index patterns define which Elasticsearch data Kibana explores.
* KQL provides a way to search and filter ingested data.
* KQL supports free-text searches and field-based searches.
* Wildcards and logical operators can make searches more flexible.
* Timelines can help identify unusual spikes in activity.
* Visualizations can make patterns easier to identify.
* Dashboards combine searches and visualizations into a centralized view.
* Elastic Stack can be used to investigate VPN logs and identify anomalies.

---

## New Terminology

* Elastic Stack
* ELK
* Elasticsearch
* Logstash
* Beats
* Kibana
* Index Pattern
* Discover
* KQL
* Free-Text Search
* Field-Based Search
* Wildcard
* Timeline
* Visualization
* Dashboard
* Data-Shipper
* Log Normalization

---

## Personal Reflection

This room helped me understand how Elastic Stack can be used by a SOC analyst for log analysis and investigations.

The most important concept for me was understanding how the different components work together. Beats collect data, Logstash processes and normalizes it, Elasticsearch stores and makes the data searchable, and Kibana provides the interface used to investigate and visualize it.

The practical VPN investigation also showed how a SOC analyst can move from raw logs to filtered results, identify anomalies, create visualizations, and finally combine those visualizations into a dashboard.

This gives me a better understanding of how log-analysis platforms can support the daily investigative work of a SOC.

---

## References

* TryHackMe — SOC Level 1
* Elastic Stack: The Basics room
