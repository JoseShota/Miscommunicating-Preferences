# Miscommunicating-Preferences

**Authors:** Laboratory for Interdisciplinary Social Science (LISS)

**Framework:** oTree 6+

## Project Overview
An oTree implementation of a minimal experiment to study the chilling of expression. This project investigates strategic lying and social punishment within groups, specifically testing how room composition and the presence of "judgmental types" (erasers) impact the incentives to express or hide true opinions.

## Baseline Experimental Design

The experiment is technically a **Single-Player** game. Participants do not interact in real-time. Interactions are simulated based on room compositions, and matching is performed **ex-post** using data collected from different sessions.

### Terminology & Notation

* **Opinion Types:** `A` or `B` (Binary stance on $n$ topics).
* **Participant Types:**
  * **Non-Eraser (N):** Unwilling to pay a cost to punish a dissenter.
  * **Eraser (E):** Willing to pay cost  to take  from a dissenter.


* **Room Notation:** e.g., `6AN4BE`
  * 6 participants who are Opinion A + Non-Eraser.
  * 4 participants who are Opinion B + Eraser.


### App Sequence

The session is divided into the following oTree apps (folders):

#### 1. `topic_elicitation`

* **Input:** User faces 5 binary topics.
* **Data Collected:**
* Private Opinion (A or B).
* Importance of the topic (Important or Unimportant)



#### 2. `eraser_elicitation`

* **Mechanism:** Strategy method.
* **Decision:** For each topic, are you willing to pay cost $c$ to impose a cost $C$ from a participant with the opposite opinion?
* **Classification:**
* If Yes  **Eraser (E)**.
* If No  **Non-Eraser (N)**.



#### 3. `room_composition` (Main Task)

* **Structure:** Multiple rounds.
* **The Scenario:**
1. Participant is assigned to a specific **Room Composition** (e.g., "You are in a room with 6 people whose opinion is A and are Erasers and 4 people whose opinion is B and are non-Erasers").
2. Participant knows which proportion of the room are **Erasers**.
3. **Action:** Participant chooses which opinion to express publicly to a randomly selected member in the room.
4. **Incentives:**
* **Lying Cost ():** Penalty if expressed opinion is not the private opinion. (Lying is free in Baseline experiment).
* **Punishment Risk:** Probability of being punished by an Eraser in the room.


## Technical Implementation Guide

### 1. Requirements

* Python 3.14+
* `pip install otree`

###  2. Data Structure Note

Since matching is **Ex-Post**, we do not use `group.wait_for_others()`.

* We need to ensure we collect enough observations of Type A E/N and Type B E/N for every topic to "reconstruct" the groups of 10 during analysis.
* **Crucial:** All "Room" variables (e.g., "In this round, the room is 60% Erasers") must be saved as fields in `player` database for easy regression analysis later.
