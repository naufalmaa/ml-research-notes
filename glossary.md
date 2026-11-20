# Glossary

Plain-English definitions of the terms I meet in the roadmap. Each entry includes *why it matters for my projects* and a source to read further. Sorted A–Z. Add new terms with the same format.

---

### ADR (Architecture Decision Record)
A short file recording one decision: context, decision, consequences. **Why it matters:** the README's "Decisions & lessons" section and my interview stories come from these. *Source:* [Nygard-style ADRs via Cookiecutter DS opinions](https://cookiecutter-data-science.drivendata.org/opinions/)

### Baseline
The simplest reasonable method (a threshold rule, "tomorrow = today", a decline curve). Every model is reported relative to it. **Why:** a metric without a baseline means nothing; if the model doesn't beat it, that is the finding. *Source:* [Rules of ML #1–3](https://developers.google.com/machine-learning/guides/rules-of-ml)

### Batch vs online inference
Batch: score many rows on a schedule (e.g. daily). Online: score one request at a time on demand (an API call). **Why:** Project 3 uses daily batch for alerts; Project 4's agent calls the model online through REST.

### Bayesian optimisation / TPE
Hyperparameter search that uses past trials to choose the next one, instead of trying values blindly. TPE (Tree-structured Parzen Estimator) is Optuna's default. **Why:** P2 tunes against the backtest score. *Source:* [Optuna paper](https://arxiv.org/abs/1907.10902v1)

### Bootstrap confidence interval
Resample the test set (with replacement) many times, recompute the metric each time, and take the 2.5–97.5 percentiles. Resample whole **groups** (wells) when rows inside a group are correlated. **Why:** shows how much a number could move by chance. *Source:* [Raschka 2018](https://arxiv.org/abs/1811.12808v2)

### BSW (Basic Sediment & Water)
The share of water and sediment in produced liquid. An abnormal rise is one of the 3W event types. Domain term.

### Calibration (probability calibration)
Making a model's score mean what it says: of all cases scored 0.8, about 80% should be positive. Methods: **Platt scaling** (fit a sigmoid) and **isotonic regression** (fit a monotone step function, needs more data). **Why:** thresholds and risk communication rely on honest probabilities. *Source:* [scikit-learn calibration](https://scikit-learn.org/stable/modules/calibration.html)

### Champion / challenger
The current production model (champion) is replaced only if a new model (challenger) wins on a fresh time-based holdout. **Why:** P3's retraining gate. *Source:* [MLflow aliases](https://mlflow.org/docs/latest/ml/model-registry)

### Choke
A valve that restricts flow from a well. Choke size changes production rate, so it is a key feature in P2. Domain term.

### Class imbalance
When one class is rare (failures ≪ normal). Accuracy becomes misleading: predicting "normal" always can score 99%. **Why:** event detection in P1. *Source:* [Saito & Rehmsmeier 2015](https://pmc.ncbi.nlm.nih.gov/articles/PMC4349800)

### Concept drift
The relation between inputs and the target changes (same sensor readings now mean something else). Needs labels to detect. Contrast with **data drift**. *Source:* [Gama et al. 2014](https://repositorio.inesctec.pt/handle/123456789/5370)

### Conformal prediction
A wrapper that turns any model's predictions into intervals with a guaranteed coverage (e.g. 90%), assuming exchangeable data. **Why:** P2 compares it with quantile regression for P10–P90. *Source:* [Angelopoulos & Bates](https://arxiv.org/abs/2107.07511v6)

### Coverage
The share of true values that fall inside the predicted intervals. A "90% interval" should cover ≈90% on the test set.

### Data drift (covariate shift)
The input distribution changes (e.g. a new operating regime). Detectable **without** labels. *Source:* [Rabanser et al. 2019](https://arxiv.org/abs/1810.11953v1)

### Data leakage
Information that would not be available at prediction time sneaks into training, so offline metrics look better than reality. **Why:** the #1 reason ML projects fail in production. *Source:* [Kaufman et al. 2012](https://www.doi.org/10.1145/2382577.2382579)

### Datasheet / data card
A short document describing a dataset: origin, collection, labels, licence, known issues. *Source:* [Gebru et al.](https://arxiv.org/abs/1803.09010v7)

### Decline curve (Arps)
An empirical equation for how a well's rate falls over time: exponential, hyperbolic, or harmonic. **Why:** P2's physics baseline and the "grey" part of the grey-box model. *Source:* [PetroWiki](https://petrowiki.spe.org/Production_forecasting_decline_curve_analysis)

### Early stopping
Stop adding trees to a boosting model when the validation score stops improving. Prevents overfitting. *Source:* [LightGBM tuning](https://lightgbm.readthedocs.io/en/latest/Parameters-Tuning.html)

### Event-level recall
Of all real events, how many got at least one alert in time. Different from row-level recall, which rewards long events. **Why:** what an operator actually cares about. *Source:* [Tatbul et al. 2018](https://arxiv.org/abs/1803.03639)

### False alarm rate
Alerts that matched no event, per unit of time (e.g. per well per week). **Why:** too many and operators stop trusting the system.

### Gradient boosting
Build trees one after another, each fixing the errors of the previous ones. LightGBM and XGBoost are fast implementations. *Source:* [LightGBM paper](https://proceedings.neurips.cc/paper/2017/file/6449f44a102fde848669bdd9eb6b76fa-Paper.pdf)

### Grey-box (hybrid) model
Physics/engineering model + ML model, usually ML learns what the physics misses (the **residual**). *Source:* [Karpatne et al. 2017](https://arxiv.org/abs/1612.08544)

### Grouped split
All rows from one group (a well, a machine) go to the same side of the split. Tests whether the model works on an asset it has never seen. *Source:* [scikit-learn GroupKFold](https://scikit-learn.org/stable/modules/cross_validation.html)

### Hydrate
Ice-like solid of water and gas that can block flowlines. A 3W event type. Domain term.

### Isolation Forest
Unsupervised anomaly detector: anomalies are isolated by fewer random splits than normal points. *Source:* [Liu et al. 2008](https://doi.org/10.1109/ICDM.2008.17)

### Lead time
How long before an event the first alert fires. **Why:** an alert 1 minute before is useless; 2 hours before is actionable.

### Look-ahead bias
A special case of leakage: using values from after time *t* to predict at *t* (e.g. a centred rolling mean).

### MAE, RMSE, MAPE, MASE
Forecast errors. **MAE**: mean absolute error (in units). **RMSE**: punishes big misses more. **MAPE**: percentage error, **breaks when actual = 0** (shut-in days). **MASE**: MAE divided by the naive forecast's MAE; < 1 means better than naive. *Source:* [Hyndman & Koehler 2006](https://www.doi.org/10.1016/J.IJFORECAST.2006.03.001)

### Model card
A short document on what a model is for, how it was evaluated, and its limits. *Source:* [Mitchell et al. 2019](https://arxiv.com/abs/1810.03993)

### Model registry
A store of model versions with labels (aliases) like `@champion`. *Source:* [MLflow](https://mlflow.org/docs/latest/ml/model-registry)

### On-stream hours
Hours per day a well was actually producing. Divide volume by it to get a fair rate. Domain term (P2: `ON_STREAM_HRS`).

### PR-AUC vs ROC-AUC
Area under the precision–recall curve vs the ROC curve. With rare events, ROC-AUC can look great while precision is terrible; PR-AUC exposes it. *Source:* [Saito & Rehmsmeier 2015](https://pmc.ncbi.nlm.nih.gov/articles/PMC4349800)

### Precision, recall
Precision: of the alerts, how many were right. Recall: of the real events, how many were caught.

### Quantile regression
Predict a chosen percentile (P10, P50, P90) instead of the mean. LightGBM supports it with `objective="quantile"`.

### Residual
Actual minus predicted. In P2 the ML model predicts the residual of the Arps curve.

### Rolling-origin backtest
Repeatedly: train on data up to a cut-off, forecast the next horizon, move the cut-off forward. The honest way to evaluate forecasts. *Source:* [FPP3 §5.10](https://otexts.com/fpp3/tscv.html)

### SHAP
A method that splits a prediction into contributions per feature, based on Shapley values from game theory. *Source:* [Lundberg & Lee 2017](https://arxiv.org/abs/1705.07874)

### Shut-in
A well closed in (zero production) on purpose or for problems. Creates zeros that break MAPE.

### Slugging (severe)
Unstable flow where liquid and gas arrive in large alternating slugs. A 3W event type. Domain term.

### Threshold tuning
Choosing the score cut-off that turns probabilities into alerts, based on the cost of false alarms vs misses, not the default 0.5. *Source:* [scikit-learn](https://scikit-learn.org/stable/modules/classification_threshold.html)

### Time-series split
Train on the past, test on the future, never shuffled. *Source:* [scikit-learn TimeSeriesSplit](https://scikit-learn.org/stable/modules/generated/sklearn.model_selection.TimeSeriesSplit.html)

### Water cut
Water as a share of total liquid produced. Rises as a field matures. Domain term (P2).
