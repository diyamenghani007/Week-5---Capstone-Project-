# Dynamic Pricing for Urban Parking Lots 

## Capstone Project - Summer Analytics 2025Consulting and Analytics Club × Pathway


#### Project Overview
Urban parking is a limited resource with fluctuating demand. Static pricing leads to either overcrowding or underuse.
This project implements a real-time, data-driven pricing engine that updates parking prices based on demand, traffic, and vehicle behavior using:
- Basic economic theory
- Stream processing with Pathway
- Visual analysis using Bokeh


#### Tech Stack

|       Layer        |      Tool/Library       |
|--------------------|-------------------------|
|      Language      |         Python          |
|    Data-Handling   |      Pandas, Numpy      |
|  Real-Time Engine  |         Pathway         |
|    Visualisation   |         Bokeh           |
|     Environment    |      Google Colab       |



#### Architecture Flow
1. **Dataset Loading**: Parking lot records with occupancy, queue, traffic, vehicle type, etc. (sampled every 30 mins)
2. **Preprocessing**: Extract relevant features; add timestamp
3. **Model 2**: Demand-Based Pricing:
          -Calculate a demand score using weighted factors
          -Normalize demand
          -Adjust price relative to a base value

4. **Streaming**: Pathway simulates real-time ingestion using timestamps
5. **Real-Time Output**: Emitted as a .jsonl stream
6. **Visualization**: Price vs time plotted for each lot using Bokeh



#### Demand Function Logic
Price = BasePrice * (1 + lambda * NormalizedDemand)
Where, NormalizedDemand = f(occupancy/capacity, queue length, traffic, special day, vehicle weight)

-Base Price = $10
-Price is clamped between $5 and $15
-Demand normalized between 0 and 1

#### Architecture Diagram

+---------------------+
|   dataset.csv       |
+---------------------+
            |
            v
+---------------------+
|   Data Preprocess   | <-- Pandas/NumPy
+---------------------+
            |
            v
+----------------------------+
|   Model 1 + Model 2 Logic  |
|   compute_price()         |
+----------------------------+
            |
            v
+-------------------------------------+
|   Mid-Model Bokeh Plots              |
|   - Model 2 Price Trend              |
|   - Model 1 vs Model 2 Comparison    |
+-------------------------------------+
            |
            v
+-----------------------------+
|     Pathway Streaming       |
|  (with timestamped rows)    |
+-----------------------------+
            |
            v
+-----------------------------+
| output_stream.jsonl         |
+-----------------------------+
            |
            v
+-----------------------------+
|   Final Bokeh Visualization |
|   (Price over time per lot) |
+-----------------------------+



#### Key Outcomes
-Implemented two models: baseline (Model 1) and demand-based (Model 2)
-Compared model behaviors visually using Bokeh
-Integrated real-time logic using Pathway’s streaming framework
-Pricing adapts based on occupancy, traffic, queue, and vehicle type
-Interactive visualization validates pricing logic



#### Files in This Repo

|          File          |                  Description                  |
|------------------------|-----------------------------------------------|
| Capstone_Project.ipynb | Main notebook with data processing and models |
|      dataset.csv       | Input dataset (73 days, 14 parking lots)      |
|    stream_input.csv    | Processed real-time stream input              |
|  output_stream.jsonl   | Streaming model output from Pathway           |
|       README.md        | Documentation                                 |



#### Submission Notes
Project satisfies all core requirements: streaming, pricing logic, and visualization
Model 3 (Competitive Pricing) is optional and not implemented
Manual interruption is used post streaming (as Pathway continues to listen by design)


Thanks for reading!
