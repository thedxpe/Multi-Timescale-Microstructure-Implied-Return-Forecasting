# Multi-Timescale-Microstructure-Implied-Return-Forecasting
Causal HFT research framework that converts BTC order-book replenishment, penetration and imbalance into a multi-timescale 100 ms expected-return signal, with rolling reliability diagnostics to measure when the microstructure-return relationship is trustworthy.
This project investigates whether high-frequency order-book structure can be transformed into an interpretable expected-return signal for Bitcoin at a 100 ms horizon.

The model uses microstructure features describing liquidity replenishment, fractional order-book penetration, aggressive volume pressure, and order-book imbalance at multiple depths.

Four causal rolling Ridge regressions learn the relationship between these features and future 100 ms returns over different historical windows: 30 minutes, 10 minutes, 1 minute, and 30 seconds. Their predictions are then combined with the current microstructure state through a second-stage meta-regression to produce:

expected_return_100ms

The framework also creates a reliability state from matured historical forecast errors, including rolling bias, MAE, directional accuracy, and disagreement between timescale models.

On an initial 30,000-observation walk-forward test, the final model achieved Pearson correlation 0.430 and Spearman correlation 0.462. Because approximately 74.9% of 100 ms returns were zero, unconditional MAE was worse than a zero-return baseline. However, conditional on an actual price move, directional accuracy reached 83.7%, Pearson correlation 0.519, and Spearman correlation 0.631.

The strongest result came from ranking predictions: the bottom 10% of expected returns realized approximately -0.381 bps, while the top 10% realized +0.429 bps, producing a 0.810 bps top-minus-bottom spread.

These findings suggest that the feature is more effective as a microstructure-implied directional and ranking signal than as an unconditional point forecast at every 100 ms timestamp. The next research stage is to separate the problem into probability of a price move and expected return conditional on a move, while using the reliability state as a dynamic confidence measure.
