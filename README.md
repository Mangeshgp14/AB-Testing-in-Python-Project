# A/B Testing : Edtech Landing Page Optimization 

<img width="1024" height="559" alt="image" src="https://github.com/user-attachments/assets/13e620ab-11bd-4899-8649-eac45eeb636b" />

## 1. Problem Statement
**The Data**: Analytics show that while 5,000 users visit the homepage daily, only 500 click "Start Now." <br>
**The Insight**: The current Click-Through Rate (CTR) is 10%. Heatmap tools (like Hotjar) show that users' eyes often skip over the orange button because the header image also contains orange/warm tones.<br>
**The Problem**: The primary Call-to-Action (CTA) is "blending in" rather than "standing out."<br>

## 2. Hypothesis
**Null Hypothesis (H0)**:<br>
<ins>Statement</ins>: Changing the button color from orange to pink will have no significant effect on the Click-Through Rate.<br>

**Alternative Hypothesis (H1)**:<br>
<ins>Statement</ins>: Changing the button color from orange to pink will have no significant effect on the Click-Through Rate.<br>

**The Rationale**:<br>
<ins>Isolation of Variable</ins>: By changing only the color (and keeping the text, size, and position the same), we can confidently attribute any change in CTR specifically to the visual prominence of the color.

<ins>Color Theory</ins>: Pink (specifically a vibrant magenta or hot pink) has a high "luminance contrast" against neutral or dark backgrounds, which reduces the cognitive load for a user trying to find the "next step."

## 3. Selecting the Metric

The aim of the experiment is to test whethet the user is more likely to click the button due to colour change.
So, the most direct measurement of the change is 'Click Through Rate (CTR)".

**Primary Metric**: CTR <br>
We want to ensure that pink doesn't just attract "accidental" clicks, but actually leads to more people completing the sign-up flow.

**Secondary Metric**: Conversion Rate (Sign-ups) <br>
We want to ensure that pink doesn't just attract "accidental" clicks, but actually leads to more people completing the sign-up flow.

**Guardrail Metric**: Bounce Rate <br>
We want to make sure a "hot pink" button isn't so distracting or "ugly" that it makes users perceive the brand as low-quality and leave the site entirely.

**Important Consideration while selecting Primary Metric:** <br>
For such cases. there are two metrics that are suitable, CTR (Click Through Rate) and CTP (Click Through Probability).
<ins>Why CTR is the standard for this test<ins>
In our button color experiment, we are using CTR because we want to measure the "attractiveness" and "discoverability" of the button every single time the page loads.

A. Multi-Session Behavior
If a user visits your homepage three times in a week:

In CTP, that user is just one data point. Whether they click on Monday or Wednesday, it’s just "1 click / 1 user."

In CTR, you get three data points. If the pink button caught their eye on Monday, but they didn't click until Wednesday, the CTR captures the fact that it took three "impressions" to get a result.

B. The "Intent" vs. "Interaction"
CTP is great for conversion funnels (e.g., "Did the user eventually sign up?"). It measures a final outcome.

CTR is better for UI elements (e.g., "Does this button stand out?"). It measures the immediate interaction every time the user is exposed to the change.

## 4. Minimum Detectable Effect (MDE)

MDE is the smallest improvement that actually makes an impact.

It is calculated through proper cost-benefit analysis.

For our case, a 20% relative lift in CTR is a "healthy" win that is worth the effort of a rollout and is large enough that we can detect it with a reasonable number of users in Python.

**Baseline CTR**: 10%<br>
**(Relative)**: 20%<br>
**Target CTR**: 12%<br>

## 5. Power Analysis
Power Analysis is a method to calculate the sample size required to detect the MDE with a given level of confidence (significance) and a given chance of success (power).

Power analysis is a formula with four interconnected variables. 
If you know any three, you can calculate the fourth:
### The variables are: 
* **Effect Size (MDE):** How big is the "win" you are looking for?
  * *Example: A 2% lift in conversion.*
* **Sample Size ($n$):** How many users will be included in the experiment?
* **Significance ($\alpha$):** How strict is your evidence? 
  * *Standard: 0.05 (5% chance of a False Positive).*
* **Statistical Power ($1-\beta$):** How sensitive is your test? 
  * *Standard: 0.80 (80% chance of detecting a real effect).*


### ⚖️ Understanding Significance and Power: The Courtroom Analogy

Imagine you are a judge. In every trial, there are two specific ways to reach the wrong verdict:

| Error Type | Courtroom Scenario | Statistical Term |
| :--- | :--- | :--- |
| **False Positive** | Convicting an innocent person | **Type I Error ($\alpha$)** |
| **False Negative** | Letting a guilty person go free | **Type II Error ($\beta$)** |

In our case, a "False Positive" is when you think the Pink button is better, but it actually isn't — you just got lucky with the data.
Similarly, a "False Negative" is when the Pink button is actually better, but your test was too weak to notice it.

As per industry standard, we set the value of significance at 5% (0.05) and power at 80% (0.8).

By doing so, we are saying:
I am only willing to take a 5% risk of being wrong meaning I want to be 95% sure that the Pink button won because it's actually better, not because of random luck. <br>
I want an 80% chance of catching a win if it exists. You accept a 20% risk that you might "miss" a real improvement because you didn't have enough data or time.

### Let us now run a Power Analysis in python

File Link: [A/B Testing in Python](https://colab.research.google.com/drive/1B5iNeOBLEb_iyek3abjv3cFwO1kjcjQd?usp=sharing)

```python
import statsmodels.stats.power as power
import statsmodels.stats.proportion as proportion

# --- STEP 1: DEFINE YOUR GOALS ---
# This is the "Product" part of the code.

baseline_ctr = 0.10   # We currently have a 10% Click-Through Rate
mde = 0.02            # We want to detect a 2% lift (taking us to 12%)
significance = 0.05   # We want to be 95% sure it's not luck
desired_power = 0.80  # We want an 80% chance of catching the win

# --- STEP 2: CALCULATE THE "EFFECT SIZE" ---
# Math logic: Computers don't see "10% vs 12%". 
# They see a "Distance" between two numbers called an Effect Size.

target_ctr = baseline_ctr + mde
eff_size = proportion.proportion_effectsize(baseline_ctr, target_ctr)

# --- STEP 3: SOLVE FOR SAMPLE SIZE ---
# This is the "Power Analysis" part.

analysis = power.NormalIndPower()
required_n = analysis.solve_power(
    effect_size=eff_size, 
    alpha=significance, 
    power=desired_power, 
    ratio=1.0  # Means we split traffic 50/50
)

# --- STEP 4: PRINT THE RESULT ---
print(f"--- A/B TEST PLAN ---")
print(f"To detect a {mde*100}% increase from a {baseline_ctr*100}% baseline:")
print(f"You need {round(required_n)} users PER BUTTON color.")
print(f"Total traffic needed: {round(required_n * 2)} users.")

```

**Result:**
To detect a 2.0% increase from a 10.0% baseline:
You need 3835 users PER BUTTON color.
**Total traffic needed: 7669 users.**

| Metric | Value | Notes |
| :--- | :--- | :--- |
| **Total Traffic Required** | 7669 users | Combined total for both variants. |
| **Daily Traffic (Assumption)** | 1,000 users/day | Based on historical site volume. |
| **Estimated Test Duration** | 8 days | Minimum time to reach sample size. |
| **Recommended Duration** | **14 days** | Extended to cover 2 full business cycles. |
