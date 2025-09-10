# Formula 1: Data Analysis and Podium Prediction 

<p align="center">
  <img src="2025_F1.jpg" alt="F1 Logo" width="750"/>
</p> 

## Project Overview

Formula 1 (F1) is the highest level of international motorsport, where drivers compete in the fastest single seater cars. Races combine speed, strategy, and technology. 

In Formula 1, the margin between winning and losing is often measured in fractions of a second. Teams spend millions analyzing data to optimize pit strategies, tire management, and driver performance.

This project replicates that approach by answering two core questions:

1. What factors most influence a driver’s chance of finishing on the podium?

2. Can we build a machine learning model to predict podium finishes based on historical data?

## Objective 

The project aims to provide a comprehensive analysis of Formula 1 datasets, exploring metrics such as lap times, pit stops, and driver performance. It further focuses on identifying the factors that drive podium success and quantifying their impact. Finally, it builds a predictive model to estimate whether a driver will finish in the Top 3 based on race conditions and historical data. 

## Data Exploration 

### Data Sources: 
Historical F1 datasets (via Kaggle).

### Key tables: 
results, races, pit_stops, lap_times, qualifying.

## Data Cleaning & Preparation

-- Removed incomplete/missing values.

-- Engineered race-level and driver-level features.

-- Merged multiple datasets for a consolidated view.

## Exploratory Insights

1. Grid Position: Starting higher strongly correlates with finishing on the podium.

2. Pit Stop Strategy: Fewer, faster pit stops are a major differentiator.

3. Lap Consistency: Drivers with lower lap variance tend to climb positions.

4. Year Effect: Technological shifts (engine changes, regulations) impact race dynamics.

## Analytical Findings

1. Grid Position Matters: Drivers starting in the Top 5 account for over 70% of podiums.

2. Pit Stop Efficiency: Each additional pit stop reduces podium probability by ~15%.

3. Consistency > Speed: The driver with the absolute fastest lap is not always the podium finisher.

4. Resources: Constructor influence (budget, engineering) indirectly drives success.

## Predictive Modeling

### Features Used: 

-- Grid position

-- Number & duration of pit stops

-- Average and fastest lap times

-- Constructor (team) strength

-- Historical performance metrics

### Models Tested:

-- Logistic Regression

-- Random Forest

### Model Evaluation

-- Metrics: Accuracy, Precision, Recall, F1 Score

-- Confusion Matrix to handle class imbalance

## Results

This project explored Formula 1 race data to understand what drives podium success and whether podiums can be predicted using machine learning. The analysis showed that grid position, constructor reliability (low DNF rates), driver pace (fastest laps), and race strategy are the strongest factors influencing podium chances. Notably, while starting near the front increases the odds, comeback wins from lower grid positions prove that strategy and skill also play key roles. To test predictability, models were built using 15,000+ race entries. Logistic Regression achieved ~80% accuracy with high recall (good at catching most podiums), while Random Forest reached ~84% accuracy with better precision (fewer false alarms). Overall, the results confirm that podium finishes can be explained and reasonably predicted using historical data, with trade-offs between broader detection and precise prediction.
