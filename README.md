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
