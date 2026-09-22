# Support Case SLA & Aging Automation

## Project Overview

This project demonstrates an automated support-case SLA monitoring solution built using Microsoft Power Automate, Excel, OneDrive for Business, and Microsoft Teams.

The workflow processes a synthetic dataset containing **2,000 support cases**, identifies open cases, evaluates case aging against priority-based SLA targets, identifies SLA breaches, and automatically sends a summary notification through Microsoft Teams.

All data used in this project is fictional and was created specifically for portfolio and learning purposes.

---

## Business Problem

Support teams may manage hundreds or thousands of active cases across different priorities.

Manually reviewing each case to determine its age and SLA status can be time-consuming and may result in delayed identification of SLA breaches.

The objective of this project was to automate:

- Identification of open support cases
- Case-aging calculation
- Priority-based SLA validation
- SLA breach identification
- SLA breach reporting
- Microsoft Teams notifications

---

## Dataset

The project uses a synthetic dataset containing **2,000 support cases**.

The dataset includes fields such as:

- Case ID
- Created Date
- Status
- Priority
- Agent
- Country
- Product
- Support Level
- SLA Hours
- Customer Response Status
- Resolution Date
- Escalation Status

No real customer, employee, or proprietary company data is included.

---

## SLA Rules

| Priority | SLA Target |
|---|---:|
| Critical | 8 Hours |
| High | 24 Hours |
| Medium | 48 Hours |
| Low | 72 Hours |

A case is considered breached when:

`Case Age in Hours > SLA Hours`

---

## Automation Workflow

The optimized workflow follows:

`Recurrence → Read Excel Data → Filter Open Cases → Filter SLA Breaches → Send Teams Summary`

### 1. Recurrence

The workflow runs automatically on a scheduled basis.

### 2. Read Support Cases

Power Automate retrieves the support-case dataset from an Excel table stored in OneDrive for Business.

Pagination is enabled to process the complete **2,000-row dataset**.

### 3. Filter Open Cases

The first Filter Array identifies cases where the status is **Open**.

### 4. Identify SLA Breaches

The second Filter Array calculates case aging and compares it against the SLA target assigned to each case.

This allows SLA status to change dynamically as open cases continue to age.

### 5. Microsoft Teams Notification

The workflow counts the filtered results and automatically sends an SLA summary through Microsoft Teams.

### Successful Run Result

- **Total Open Cases: 946**
- **SLA Breached Cases: 751**

The number of breached cases is dynamic because open cases continue aging over time.

---

## Performance Optimization

The initial workflow used an `Apply to each` loop to process open cases individually.

With hundreds of cases, this resulted in long execution times.

### Initial Design

`Open Cases → Apply to each → Calculate Age → Condition → Increment Counter`

### Optimized Design

`Open Cases → Filter SLA Breaches → Count Filtered Array`

The optimized design removed unnecessary case-by-case loops and variables and replaced them with array-based filtering.

---

## Challenges Solved

- Processing a 2,000-row dataset
- Converting Excel date/time values for SLA calculations
- Handling numeric and string data-type mismatches
- Configuring pagination for larger datasets
- Reducing sequential loop processing
- Preventing oversized Teams messages
- Replacing variable-based counting with array-based counting
- Dynamically calculating SLA status

---

## Technologies Used

- Microsoft Power Automate
- Microsoft Excel
- OneDrive for Business
- Microsoft Teams
- Power Automate Expressions
- Array Filtering
- Workflow Automation
- SLA & Case Aging Logic

---

## Project Screenshots

### Optimized Power Automate Workflow

![Power Automate Flow](screenshots/power-automate-flow-overview.png)

### Microsoft Teams SLA Summary

![Teams SLA Summary](screenshots/Teams%20SLA%20Summary-overview.png)

---

## Key Learning

This project demonstrates how business rules can be translated into an automated operational workflow.

It also demonstrates workflow optimization by redesigning an initial case-by-case processing approach into an array-based solution suitable for a larger dataset.

---

## Data Privacy

The dataset used in this repository is entirely synthetic.

No HP customer data, employee data, internal case information, or confidential company information is included.
