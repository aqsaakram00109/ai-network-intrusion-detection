# AI-Powered Network Intrusion Detection System
Machine learning-based network intrusion detection with explainability and threat scoring
# AI-Powered Network Intrusion Detection System

## Overview

This project explores machine learning for network intrusion detection using selected benign traffic and UDP-flood attack traffic from the CICIoT2023 dataset.

It includes data cleaning, supervised classification, feature-ablation experiments, model evaluation, and an initial threat-scoring baseline.

## Objectives

- Build a machine learning baseline for distinguishing benign traffic from UDP-flood traffic.
- Investigate the influence of selected network features.
- Compare model predictions on a separate TCP-flood CSV file.
- Explore explainable machine learning and threat-score presentation.
- Document limitations and opportunities for further research.

## Dataset

The project uses three CSV files from CICIoT2023:

- BenignTraffic.pcap.csv
- DDoS-UDP_Flood.pcap.csv
- DDoS-TCP_Flood.pcap.csv

Dataset source: https://www.unb.ca/cic/datasets/iotdataset-2023.html

The benign and UDP-flood files were assigned binary labels based on their source-file categories:

- `0`: Benign traffic
- `1`: UDP-flood traffic

The TCP-flood file was used for exploratory prediction analysis. It did not contain a row-level label column in the version used here.

## Data Preparation

The workflow includes:

1. Loading the CSV files with pandas.
2. Removing exact duplicate rows within each source file.
3. Assigning labels to benign and UDP-flood records.
4. Combining the labeled data.
5. Replacing infinite values with missing values.
6. Splitting the data into training and test sets.
7. Fitting median imputation on the training data and applying it to the test data.

The combined dataset contains 489,379 records after duplicate removal:

- Benign: 360,865
- UDP flood: 128,514

## Models and Experiments

A Random Forest classifier was evaluated using a stratified random train/test split.

Additional experiments examined:
- Removing the `Number` feature.
- Removing `Number` and protocol-related features.
- Comparing predictions on a separate TCP-flood file.
- Examining feature importance and attack-score distributions.

## Initial Results

The Random Forest configurations achieved 100% accuracy and 100% balanced accuracy on the current random test split.

These results should be interpreted cautiously. The dataset may contain highly distinctive collection or generation patterns, and random splitting may overestimate generalization to new captures.

In the separate TCP-file experiment, the percentage of records predicted as attacks differed substantially between model configurations. Because that file did not contain verified row-level labels, these percentages are prediction rates, not detection accuracy.

## Threat Scoring

The initial baseline converts the model's attack-class score to a 0–100 scale.

Illustrative levels:
- Low: below 30
- Medium: 30 to below 70
- High: 70 or above

These thresholds are provisional. The scores have not been established as calibrated real-world attack probabilities, and the thresholds have not been independently validated.

## Limitations

- The primary labeled experiment covers benign traffic and one attack category.
- Labels were assigned from source-file categories rather than read from a row-level label column.
- Random-split results do not establish performance on independent network captures.
- The TCP-file prediction experiment lacks verified labels for calculating accuracy, precision, or recall.
- The proposed threat-scoring baseline is exploratory and is not yet a validated adaptive scoring contribution.
- Further testing across multiple attack classes, capture groups, and independently labeled data is needed.
## Future Work
- Evaluate on additional attack categories and benign captures.
- Use capture-aware or group-based validation where metadata permits.
- Investigate feature shortcuts and dataset distribution shift.
- Compare multiple classifiers using consistent evaluation procedures.
- Validate calibration and threat-score thresholds.
- Develop and test a clearly defined research contribution against appropriate baselines.
## Tools
- Python
- pandas and NumPy
- scikit-learn
- Matplotlib
- Google Colab
## Disclaimer
This is an educational and research project. Results on the current dataset should not be interpreted as evidence of production-ready intrusion detection performance.
This is an educational and research project. Results on the current dataset should not be interpreted as evidence of production-ready intrusion detection performance.
