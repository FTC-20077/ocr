# 1. CI Formula
The Consistency Index (CI) is calculated for each phase of the game as follows:

\[
\text{CI}[i] = \frac{\text{avg}[i]}{\text{dev}[i]} + (0.25 \cdot \text{opr}[i])
\]

Where:
- \( i = 0 \): Total scores
- \( i = 1 \): Autonomous phase
- \( i = 2 \): Teleop phase
- \( i = 3 \): Endgame phase
- \( \text{avg}[i] \): Average score for the phase \( i \)
- \( \text{dev}[i] \): Standard deviation of scores for the phase \( i \)
- \( \text{opr}[i] \): OPR (Offensive Power Rating) for phase \( i \)

---

# 2. Explanation of Each CI Component
- \( \frac{\text{avg}[i]}{\text{dev}[i]} \): **Inverse Coefficient of Variation**
    - Measures match-to-match consistency. Higher consistency results in higher values.
    - If the standard deviation is high, this component will reduce the CI.
  
- \( 0.25 \cdot \text{opr}[i] \): **Weighted OPR**
    - Adds a performance-based adjustment to the consistency metric.
    - Helps balance consistency with overall scoring strength.

---

# 3. OCR Formula
The Overall Consistency Rating (OCR) combines the weighted CI values for all phases:

\[
\text{OCR} = (\text{CI}[0] \cdot 0.2) + (\text{CI}[1] \cdot 0.6) + (\text{CI}[2] \cdot 0.4) + (\text{CI}[3] \cdot 0.2)
\]

Where:
- Weight for **Autonomous (CI[1])** = 0.6 (most important phase)
- Weight for **Teleop (CI[2])** = 0.4
- Weight for **Endgame (CI[3])** = 0.2
- Weight for **Total Scores (CI[0])** = 0.2

---

# 4. Steps to Calculate CI and OCR

### Step 1: Pull Data
Retrieve the match data for each team and each phase:
- Averages (\( \text{avg}[i] \)): Calculate the mean score for each phase.
- Standard Deviations (\( \text{dev}[i] \)): Calculate the standard deviation for each phase.
- OPR (\( \text{opr}[i] \)): Use OPR or compute it if required.

### Step 2: Calculate CI for Each Phase
Using the formula:

\[
\text{CI}[i] = \frac{\text{avg}[i]}{\text{dev}[i]} + (0.25 \cdot \text{opr}[i])
\]

### Step 3: Compute OCR
Using the formula:

\[
\text{OCR} = (\text{CI}[0] \cdot 0.2) + (\text{CI}[1] \cdot 0.6) + (\text{CI}[2] \cdot 0.4) + (\text{CI}[3] \cdot 0.2)
\]

---

# 5. Why the Weights?

- **Autonomous (0.6)**: Autonomous performance is often the most consistent and reliable phase, making it heavily weighted.
- **Teleop (0.4)**: Slightly less consistent but critical for high-scoring matches.
- **Endgame (0.2)**: Lower weight since it's often more volatile and less predictable.
- **Total (0.2)**: Provides a baseline measure of overall scoring consistency.

---

# Example Calculation
Here’s a mock dataset for a team across their matches:

| Metric          | Total (i=0) | Auto (i=1) | Teleop (i=2) | Endgame (i=3) |
|-----------------|-------------|------------|--------------|---------------|
| \( \text{avg}[i] \) | 120         | 40         | 60           | 20            |
| \( \text{dev}[i] \) | 15          | 5          | 10           | 8             |
| \( \text{opr}[i] \) | 100         | 30         | 50           | 20            |

### CI Calculation:
\[
\text{CI}[0] = \frac{120}{15} + (0.25 \cdot 100) = 8 + 25 = 33
\]
\[
\text{CI}[1] = \frac{40}{5} + (0.25 \cdot 30) = 8 + 7.5 = 15.5
\]
\[
\text{CI}[2] = \frac{60}{10} + (0.25 \cdot 50) = 6 + 12.5 = 18.5
\]
\[
\text{CI}[3] = \frac{20}{8} + (0.25 \cdot 20) = 2.5 + 5 = 7.5
\]

### OCR Calculation:
\[
\text{OCR} = (33 \cdot 0.2) + (15.5 \cdot 0.6) + (18.5 \cdot 0.4) + (7.5 \cdot 0.2)
\]
\[
\text{OCR} = 6.6 + 9.3 + 7.4 + 1.5 = 24.8
\]
