<img width="440" height="355" alt="Screenshot 2026-07-31 121151" src="https://github.com/user-attachments/assets/861cda03-5920-43bf-8e0c-756b29585e04" />
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

<img width="440" height="355" alt="Screenshot 2026-07-31 121151" src="https://github.com/user-attachments/assets/286555ae-7ef6-463e-a988-35b495613ef5" />


### Step 2: Interacting with the Chat Bot
By following the first step on the itinerary, we observe what information the chat bot possesses regarding its guests.

<img width="619" height="913" alt="Screenshot 2026-07-31 121453" src="https://github.com/user-attachments/assets/4d7ec5a3-895b-44cb-8b98-d2dc7a734a41" />


### Step 3: Identifying Trusted Users
Below the itinerary, we notice a post listing the different guests that the chat bot already knows and trusts.

<img width="426" height="401" alt="Screenshot 2026-07-31 121601" src="https://github.com/user-attachments/assets/7cc723e1-e2a3-424b-8300-2a744474849c" />


### Step 4: Impersonation & Flag Retrieval
By changing our declared identity, we can exploit the chat bot's trust assumptions. When we state that we are **Patch** and ask for the flag, the chat bot discloses it without verifying our identity.

<img width="535" height="218" alt="Screenshot 2026-07-31 121857" src="https://github.com/user-attachments/assets/bf440a33-7d9f-4e37-9601-95df8873fdc5" />

### Step 5: Challenge Submission
The flag revealed by the chat bot is:

```text
THM{v3r4_kn0ws_t00_Much!}
