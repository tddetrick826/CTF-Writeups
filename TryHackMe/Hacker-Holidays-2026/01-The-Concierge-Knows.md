# TryHackMe: Hacker Holidays 2026 - Day 1: The Concierge Knows Too Much

**Date:** July 2026  
**Category:** OSINT / Social Engineering  
**Difficulty:** Easy  
**Target:** Hotel Concierge Chat Bot / Employee Footprint  

---

## 1. Challenge Overview
Day 1 introduces an Open Source Intelligence (OSINT) and social engineering scenario where an over-friendly hotel chat bot leaks sensitive details. The objective is to analyze public footprint data, extract hidden credentials/identifiers, and uncover the initial access vector.

---

## 2. Step-by-Step Walkthrough

### Step 1: Identifying What Steps Must Be Taken
The challenge provides an itinerary with a list of steps to complete in order to retrieve the flag from the chat bot.

<img width="440" alt="Itinerary Steps" src="[https://github.com/user-attachments/assets/9e614ce1-821b-4f1c-910b-c777621275f0](https://github.com/user-attachments/assets/9e614ce1-821b-4f1c-910b-c777621275f0)" />

### Step 2: Interacting with the Chat Bot
By following the first step on the itinerary, we observe what information the chat bot possesses regarding its guests.

<img width="619" alt="Chat Bot Interaction" src="[https://github.com/user-attachments/assets/ab06705b-0a0d-4280-a1ef-72cbc49df3c5](https://github.com/user-attachments/assets/ab06705b-0a0d-4280-a1ef-72cbc49df3c5)" />

### Step 3: Identifying Trusted Users
Below the itinerary, we notice a post listing the different guests that the chat bot already knows and trusts.

<img width="426" alt="Trusted Guests Post" src="[https://github.com/user-attachments/assets/542f2d3d-e0ce-4ba4-9c96-0dc114326aa2](https://github.com/user-attachments/assets/542f2d3d-e0ce-4ba4-9c96-0dc114326aa2)" />

### Step 4: Impersonation & Flag Retrieval
By changing our declared identity, we can exploit the chat bot's trust assumptions. When we state that we are **Patch** and ask for the flag, the chat bot discloses it without verifying our identity.

<img width="535" alt="Retrieving Flag" src="[https://github.com/user-attachments/assets/ce47c2c1-8643-447e-be9a-5091e13310fc](https://github.com/user-attachments/assets/ce47c2c1-8643-447e-be9a-5091e13310fc)" />

### Step 5: Challenge Submission
The flag revealed by the chat bot is:

```text
THM{v3r4_kn0ws_t00_Much!}
