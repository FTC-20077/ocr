# 1. CI Formula
The Consistency Index (CI) is calculated for each phase of the game as follows:

`CI[i] = avg[i] / dev[i] + (0.25 * opr[i])`

Where:
- i = 0: Total scores
- i = 1: Autonomous phase
- i = 2: Teleop phase
- i = 3: Endgame phase
- `avg[i]`: Average score for the phase i
- `dev[i]`: Standard deviation of scores for the phase i
- `opr[i]`: OPR (Offensive Power Rating) for phase i

---

# 2. Explanation of Each CI Component
- `avg[i] / dev[i]`: **Inverse Coefficient of Variation**
    - Measures match-to-match consistency. Higher consistency results in higher values.
    - If the standard deviation is high, this component will reduce the CI.
  
- `0.25 * opr[i]`: **Weighted OPR**
    - Adds a performance-based adjustment to the consistency metric.
    - Helps balance consistency with overall scoring strength.

---

# 3. OCR Formula
The Overall Consistency Rating (OCR) combines the weighted CI values for all phases:

`OCR = (CI[0] * 0.2) + (CI[1] * 0.6) + (CI[2] * 0.4) + (CI[3] * 0.2)`

Where:
- Weight for **Autonomous (`CI[1]`)** = 0.6 (most important phase)
- Weight for **Teleop (`CI[2]`)** = 0.4
- Weight for **Endgame (`CI[3]`)** = 0.2
- Weight for **Total Scores (`CI[0]`)** = 0.2

---

# 4. Steps to Calculate CI and OCR

### Step 1: Pull Data
Retrieve the match data for each team and each phase:
- Averages (`avg[i]`): Calculate the mean score for each phase.
- Standard Deviations (`dev[i]`): Calculate the standard deviation for each phase.
- OPR (`opr[i]`): Use OPR or compute it if required.

### Step 2: Calculate CI for Each Phase
Using the formula:

`CI[i] = avg[i] / dev[i] + (0.25 * opr[i])`

### Step 3: Compute OCR
Using the formula:

`OCR = (CI[0] * 0.2) + (CI[1] * 0.6) + (CI[2] * 0.4) + (CI[3] * 0.2)`

---

# 5. Why the Weights?

- **Autonomous (0.6)**: Autonomous performance is often the most consistent and reliable phase, making it heavily weighted.
- **Teleop (0.4)**: Slightly less consistent but critical for high-scoring matches.
- **Endgame (0.2)**: Lower weight since it's often more volatile and less predictable.
- **Total (0.2)**: Provides a baseline measure of overall scoring consistency.

---

# Example Calculation
Here’s a mock dataset for a team across their matches:

| Metric           | Total (i=0) | Auto (i=1) | Teleop (i=2) | Endgame (i=3) |
|------------------|-------------|------------|--------------|---------------|
| avg[i]  | 120         | 40         | 60           | 20            |
| dev[i]  | 15          | 5          | 10           | 8             |
| opr[i]  | 100         | 30         | 50           | 20            |

### CI Calculation:
`CI[0] = 120 / 15 + (0.25 * 100) = 8 + 25 = 33`  
`CI[1] = 40 / 5 + (0.25 * 30) = 8 + 7.5 = 15.5`  
`CI[2] = 60 / 10 + (0.25 * 50) = 6 + 12.5 = 18.5`  
`CI[3] = 20 / 8 + (0.25 * 20) = 2.5 + 5 = 7.5`  

### OCR Calculation:
`OCR = (33 * 0.2) + (15.5 * 0.6) + (18.5 * 0.4) + (7.5 * 0.2)
OCR = 6.6 + 9.3 + 7.4 + 1.5 = 24.8`
