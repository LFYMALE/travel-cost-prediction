# Travel Cost Prediction

## Problem Description

Planning a trip involves a high degree of financial uncertainty. The final cost depends on many interacting factors: where the traveler is going, how long they stay, when they travel, where they sleep, and how they get there. Travelers often underestimate or overestimate their budgets, and travel businesses struggle to quote accurate, personalized prices without manually comparing countless options.

This project addresses that uncertainty by building a **supervised machine learning model that predicts the total cost of a trip** from its characteristics and the traveler's demographic profile. The target variable, `Total cost`, is the sum of accommodation and transportation expenses for a given trip.

Given details such as destination, duration, season, accommodation type, and transportation type, the model returns an estimated monetary value. This turns a vague budgeting question ("How much will this trip cost me?") into a fast, data-driven answer.

## Business Context & Use Cases

### Target Audience

| Stakeholder | Need |
|---|---|
| **Travel agencies** | Quickly quote realistic budgets and build packages that match a client's profile |
| **Online travel booking platforms** | Show dynamic cost estimates and personalized recommendations at scale |
| **Budget-conscious travelers** | Forecast expenses before booking and compare alternatives |
| **Marketing teams** | Understand spending patterns to segment customers and target promotions |

### How the Solution Will Be Used

1. **Dynamic budget estimation and package recommendation (agencies and platforms).**
   When a customer enters a destination, travel dates, and preferences, the model produces an expected total cost in real time. Platforms can use this estimate to filter and rank packages by affordability, suggest alternatives within a customer's likely spending capacity, and present transparent price expectations early in the booking funnel.

2. **Pre-booking expense forecasting (travelers).**
   Travelers can experiment with different scenarios, such as changing the departure month, swapping a hotel for a villa, or choosing a train over a flight, and immediately see how each choice shifts the predicted cost. This makes the main **cost drivers** (season, destination, accommodation type, transportation mode) visible and helps users optimize their plans before committing money.

3. **Customer segmentation and targeted promotions (marketing).**
   Predicted costs, combined with traveler demographics, can be used to group customers into spending tiers. Marketing teams can then design offers tailored to each segment, for example discounts on off-peak travel for price-sensitive segments or premium upgrades for high-spending ones.

### Why It Matters

- **For businesses:** More accurate quotes improve conversion rates, reduce pricing friction, and enable personalization without manual analysis.
- **For travelers:** Better cost transparency reduces the risk of overspending and supports more confident decisions.
- **For both:** A data-driven model replaces rough rules of thumb with estimates learned from real historical trip records.

## Dataset Overview

The project uses a **travel dataset from Kaggle** containing historical trip records, traveler profiles, and the associated travel expenses. Each row represents one trip.

### Input Features

| Feature | Type | Description |
|---|---|---|
| `Destination` | Categorical | The trip's destination |
| `Duration (days)` | Numerical | Length of the trip in days |
| `Departure month` | Categorical / Ordinal | Month extracted from the trip start date, capturing seasonality |
| `Traveler age` | Numerical | Age of the traveler |
| `Traveler gender` | Categorical | Gender of the traveler |
| `Traveler nationality` | Categorical | Nationality of the traveler |
| `Accommodation type` | Categorical | e.g., Hotel, Resort, Villa |
| `Transportation type` | Categorical | e.g., Flight, Train, Car |

### Target Variable

| Variable | Type | Description |
|---|---|---|
| `Total cost` | Numerical (continuous) | Total trip cost, calculated as the sum of accommodation and transportation costs |

> **Note:** Because `Total cost` is derived from its two component costs, those component columns are excluded from the feature set to avoid **target leakage**.

## Machine Learning Formulation

- **Learning paradigm:** Supervised learning
- **Problem type:** Regression, since the target is a continuous monetary value
- **Input:** A feature vector describing the trip and the traveler (destination, duration, departure month, age, gender, nationality, accommodation type, transportation type)
- **Output:** A single predicted value, the estimated `Total cost` of the trip
- **Feature engineering:** The departure month is extracted from the trip start date to capture seasonal pricing effects; categorical variables are encoded for model consumption
- **Evaluation metrics:** Regression metrics such as **RMSE** (penalizes large errors, interpretable in monetary units), **MAE** (average absolute error), and **R²** (proportion of variance explained)
- **Modeling approach:** Several regression models (e.g., Linear Regression, Random Forest, Gradient Boosting) are compared, with hyperparameter tuning and validation to select the best performer

## Expected Outcome

The final deliverable is a trained and validated regression model, ultimately exposed as a prediction service, that accepts trip and traveler details and returns an estimated total cost. This gives travel agencies, booking platforms, and individual travelers a practical tool for **budget planning, package personalization, and cost-driver analysis**, grounded in real historical travel data.
