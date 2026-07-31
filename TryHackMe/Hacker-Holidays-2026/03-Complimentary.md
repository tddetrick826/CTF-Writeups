# TryHackMe: Hacker Holidays 2026 - Day 3: Complimentary

**Date:** July 2026  
**Category:** Cloud (AWS) / Identity & Access Management (IAM)  
**Difficulty:** Medium  
**Target:** Byte Lotus Wellness App / Guest AWS Credentials  

---

## 1. Challenge Overview
Day 3 introduces a cloud misconfiguration scenario centered on the Byte Lotus Wellness application, which grants "complimentary" guest access without requiring user authentication. Behind the scenes, the front-end automatically provisions temporary AWS credentials to every visitor via AWS Cognito and queries a DynamoDB table directly. The objective is to identify how these credentials are issued, evaluate their IAM policy scoping, and exploit over-privileged access to retrieve restricted data.

---

## 2. Step-by-Step Walkthrough

### Step 1: Initial Reconnaissance
Navigating to the application displays a "wellness dashboard" stating that guest status is automatically assigned upon arrival. The user interface returns no initial guest data, rendering only a generic placeholder message.

---

### Step 2: Network Traffic & AWS API Observation
Opening Browser Developer Tools (`F12`) and monitoring the **Network** tab during a page refresh revealed two automated outbound requests originating directly from the browser:
1. `cognito-identity.us-east-1.amazonaws.com` (Identity provisioning)
2. `dynamodb.us-east-1.amazonaws.com` (Database query)

This confirmed that the client-side application requests AWS temporary credentials directly from Cognito to perform DynamoDB queries without an intermediate backend server.

---

### Step 3: Extracting Temporary AWS Credentials
Inspecting the JSON response returned by the AWS Cognito endpoint disclosed a set of temporary guest credentials:

* **Access Key ID:** `ASIA...`
* **Secret Access Key:** `...`
* **Session Token:** `...`

---

### Step 4: Analyzing the DynamoDB Query Pattern
The subsequent network call to DynamoDB executed a `GetItem` action against the table `complimentary-GuestWellnessProfiles`, scoped strictly to a single `guest_id`. This explained why the dashboard appeared empty for new guest sessions.

---

### Step 5: IAM Policy Testing & Privilege Escalation
Because requests to AWS APIs require AWS Signature Version 4 (SigV4) signing, manually editing HTTP request bodies in the browser invalidates the request signature. 

Instead, using the loaded AWS SDK via `AWS.Credentials`, the extracted session tokens were supplied directly. To test if the IAM role was restricted solely to single-item lookups (`GetItem`) or possessed broader table permissions, a `.scan()` operation was invoked against `complimentary-GuestWellnessProfiles`.

---

### Step 6: Data Extraction & Flag Retrieval
The `scan()` call executed successfully, returning all five records stored within the table—including guest names, emails, phone numbers, locations, and cleartext credentials. 

The `notes` field of one record explicitly noted that the guest role possessed read access to the entire table, disclosing the flag.

* **Flag Revealed:**
  ```text
  THM{fr33_app_fr33_d4t4!}
