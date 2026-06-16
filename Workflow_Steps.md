# Workflow Steps

## Overview

This automation merges two PDF documents:

1. Statement of Work (SOW) PDF attached to a Zoho CRM Deal.
2. Estimate PDF stored in Zoho Books.

The merged document is generated using Zoho Writer APIs and processed through Zoho CRM Workflow Automation.

---

## Workflow Architecture

Deal Created/Updated
↓
MergeSOWAndEstimate()
↓
Retrieve SOW PDF from CRM Attachment
↓
Retrieve Estimate PDF from Zoho Books
↓
Merge PDFs using Zoho Writer PDF Combine API
↓
Store status_check_url in Deal
↓
Wait 2 Minutes (Scheduled Action)
↓
CheckMergeStatus()
↓
Check Writer Merge Status
↓
Download Merged PDF
↓
Upload Merged PDF to Deal Attachments

---

## Function 1: MergeSOWAndEstimate

### Responsibilities

* Fetch Deal Record
* Fetch SOW Attachment
* Read Estimate Number from Deal
* Find Matching Estimate in Zoho Books
* Download Estimate PDF
* Call Zoho Writer PDF Combine API
* Save status_check_url in CRM

### Inputs

* Deal ID

### Outputs

* Writer Status URL
* Updated CRM Deal Record

---

## Function 2: CheckMergeStatus

### Responsibilities

* Retrieve Status URL from Deal
* Check Writer Merge Status
* Verify Completion
* Download Final Merged PDF
* Upload PDF to Deal Attachments

### Inputs

* Deal ID

### Outputs

* Merged PDF
* Updated Deal Attachments

---

## CRM Workflow Configuration

### Trigger

Module: Deals

Execution Criteria:

* Record Created
* Record Edited

### Instant Action

Function:

* MergeSOWAndEstimate

### Scheduled Action

Delay:

* 2 Minutes After Rule Trigger Time

Function:

* CheckMergeStatus

---

## APIs Used

### Zoho CRM API

* Get Deal Record
* Get Attachments
* Upload Attachments

### Zoho Books API

* List Estimates
* Download Estimate PDF

### Zoho Writer API

* Combine PDF Documents
* Check Merge Status
* Download Merged PDF

---

## Benefits

* Fully Automated
* No Manual Document Processing
* Dynamic Estimate Lookup
* Workflow Driven
* Scalable for Multiple Opportunities
* Ready for Integration with Zoho Sign

---

## Sample Execution

Deal:
StartUp Movers Software Project

Estimate Number:
QT-000001

Documents:

* STATEMENT OF WORK.pdf
* QT-000001.pdf

Output:

* Merged_SOW_Estimate.pdf
