Advanced Time Series Forecasting with Hierarchical Forecasting and Deep Learning
1. Introduction

Time series forecasting plays a critical role in real-world applications such as retail demand prediction, inventory planning, and energy load forecasting. In many practical scenarios, data exists in a hierarchical structure where forecasts must remain consistent across multiple aggregation levels. For example, individual product forecasts must sum correctly to category totals and overall store demand.

This project addresses a complex hierarchical forecasting problem by combining deep learning-based forecasting with modern reconciliation techniques. The primary objective is to generate accurate forecasts at the bottom level and ensure aggregation consistency using a reconciliation strategy such as Minimum Trace (MinT). The performance of the proposed approach is evaluated against a traditional statistical baseline model.

2. Problem Statement

The project simulates a real-world forecasting scenario involving multiple related time series arranged in a hierarchy:

Bottom Level: Individual product/SKU time series

Middle Level: Category aggregates

Top Level: Grand total series

The main challenges addressed in this project include:

Generating realistic synthetic hierarchical time series data.

Implementing a deep learning model for base forecasting.

Applying hierarchical reconciliation to ensure coherence.

Comparing performance with a statistical baseline model.

3. Dataset Generation

Since real-world hierarchical datasets are not always accessible, a synthetic dataset was programmatically generated using NumPy and Pandas.

3.1 Data Characteristics

The generated dataset includes:

Multiple correlated time series.

Trend components representing long-term growth or decline.

Seasonal patterns to simulate periodic demand behavior.

Random noise to mimic real-world uncertainty.

3.2 Hierarchical Structure

The hierarchy consists of:

10 Bottom-level series (SKUs)

3 Category aggregates

1 Total aggregate

Each higher-level series is constructed as the sum of its corresponding lower-level components, ensuring hierarchical consistency in the original data.

4. Methodology

The forecasting pipeline consists of four major stages:

4.1 Data Preparation

The dataset is split into training and testing periods. Input sequences are created using sliding windows to train the deep learning model.

4.2 Deep Learning Forecasting Model

A deep learning model is implemented using PyTorch to generate base forecasts for all bottom-level series independently.

Key characteristics:

Fully connected neural network architecture.

Sequence-to-one forecasting setup.

Mean Squared Error (MSE) loss function.

Mini-batch training using DataLoader.

The deep learning model captures nonlinear patterns, seasonality, and cross-series similarities more effectively than traditional methods.

4.3 Hierarchical Reconciliation (MinT)

Base forecasts generated independently are generally incoherent, meaning aggregated forecasts may not equal the sum of lower-level forecasts.

To address this, the Minimum Trace (MinT) reconciliation approach is applied:

A summation matrix defines hierarchical relationships.

Forecast errors are assumed to follow a covariance structure.

Forecasts are adjusted to minimize total variance while maintaining aggregation constraints.

This ensures:

Aggregation consistency

Reduced forecast variance

Improved overall accuracy

4.4 Baseline Model

As a benchmark, an Exponential Smoothing (ETS) model is applied to the top-level aggregate series. This represents a traditional statistical approach commonly used in practice.

5. Evaluation Metrics

Forecast performance is evaluated using:

5.1 Symmetric Mean Absolute Percentage Error (sMAPE)
𝑠
𝑀
𝐴
𝑃
𝐸
=
2
𝑛
∑
∣
𝐹
𝑡
−
𝐴
𝑡
∣
∣
𝐴
𝑡
∣
+
∣
𝐹
𝑡
∣
sMAPE=
n
2
	​

∑
∣A
t
	​

∣+∣F
t
	​

∣
∣F
t
	​

−A
t
	​

∣
	​


This metric is scale-independent and suitable for hierarchical comparisons.

5.2 Hierarchical Consistency Check

Post-reconciliation forecasts are verified to ensure that:

Total Forecast
=
∑
Bottom-Level Forecasts
Total Forecast=∑Bottom-Level Forecasts
6. Results and Analysis

The results demonstrate that:

The deep learning model successfully captures nonlinear trends and seasonality.

Independent base forecasts show aggregation inconsistencies.

MinT reconciliation corrects inconsistencies and improves forecast stability.

The reconciled forecasts outperform the ETS baseline at the aggregate level in terms of sMAPE.

Key observations:

Deep learning performs better at bottom-level prediction.

Reconciliation improves performance at higher aggregation levels.

Statistical models remain competitive for simple aggregated series but lack flexibility.

7. Discussion

The integration of deep learning with hierarchical reconciliation provides several advantages:

Improved accuracy across hierarchy levels.

Consistent forecasts suitable for operational planning.

Scalability to larger hierarchical systems.

However, limitations include:

Higher computational cost compared to statistical models.

Sensitivity to model hyperparameters.

Requirement for sufficient training data.

8. Conclusion

This project demonstrates an end-to-end hierarchical forecasting framework combining deep learning and MinT reconciliation. The approach produces coherent forecasts while achieving improved predictive accuracy compared to traditional methods.

The study highlights the importance of reconciliation techniques when forecasting multiple related time series and shows how modern deep learning models can be effectively integrated into hierarchical forecasting systems.

9. Future Work

Possible extensions include:

Implementing advanced architectures such as N-BEATS or Temporal Fusion Transformer (TFT).

Learning covariance matrices dynamically for improved MinT performance.

Applying probabilistic forecasting methods.

Testing on real-world retail or energy datasets.
