# Log Anomaly Detector

This project implements a log anomaly detection system that identifies
unusual behavior in system logs using a combination of frequency-based
analysis and content-based explanation.

The detector focuses on identifying anomalous time windows where WARN
log activity deviates significantly from normal behavior and explains
each anomaly by analyzing repeated log patterns and responsible system
components.

---

## Problem Statement

Large-scale systems generate massive volumes of logs, making manual
monitoring impractical. Simple one-off warnings are often harmless,
while repeated warnings within a short time window can indicate
underlying system issues.

This project addresses the problem of:
- Detecting anomalous log behavior automatically
- Distinguishing persistent issues from random noise
- Providing explainable insights into why an anomaly occurred

---

## Approach

The anomaly detection pipeline follows a two-stage strategy:

### 1. Frequency-Based Detection
- Parse structured system logs
- Aggregate WARN logs into fixed time windows (5-minute intervals)
- Learn baseline WARN frequency behavior
- Identify anomalous windows using a statistical threshold
  (mean + 2 × standard deviation)

### 2. Content-Based Explanation
- Inspect anomalous time windows
- Analyze repeated log EventTemplates
- Identify responsible system components
- Attribute anomalies to recurring log patterns rather than random noise

This combination allows the system to detect anomalies while remaining
interpretable and actionable.

---

## Dataset

The project uses the **HDFS structured log dataset** from LogHub.
The dataset contains parsed log fields including timestamps, log levels,
components, and generalized event templates.

> Note: The dataset itself is not included in this repository.

---

## Output

The system produces:
- Detected anomalous time windows
- WARN log frequency per time window
- Root-cause explanations based on:
  - Repeated EventTemplates
  - Responsible system components

Example interpretation:
> An anomaly was detected due to repeated WARN logs originating from the
> same subsystem and sharing an identical log pattern within a short
> time window.


---

## Installation

Create and activate a virtual environment, then install dependencies:

pip install -r requirements.txt

--------------

## Usage

Open and run the notebook:

jupyter notebook notebooks/log_anomaly_detector.ipynb


The notebook walks through:

- Log loading and preprocessing
- Time-window aggregation
- Anomaly detection
- Content-based explanation

------------------

## Limitations

- The anomaly threshold is statistical and assumes stable baseline behavior
- The approach focuses on WARN-level logs
- Sequence-based anomalies are not modeled in this version

-------

## Future Improvements

- Replace statistical thresholds with machine learning models
(e.g., Isolation Forest)
- Extend detection to ERROR-level and multi-severity analysis
- Add real-time or streaming log support
- Generalize the pipeline to other log sources

-------

## License

This project is intended for educational and research purposes.


---

