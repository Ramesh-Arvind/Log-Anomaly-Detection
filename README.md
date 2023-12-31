# Log-Anomaly-Detection using NLP

## Overview

This project focuses on the task of anomaly detection in log files generated by the Blue Gene/L supercomputer system. We employ Natural Language Processing (NLP) techniques and machine learning to identify anomalous log sequences within the data. The approach involves log sequence parsing, word embedding, feature engineering, and machine learning classification.

## Key Techniques

### Log Sequence Parsing

Logs are semi-structured textual data, and each log event follows a specific syntax. We use a regular expression to extract the description from each log line. After extracting the description, a TemplateMiner object is employed to cluster similar log descriptions into templates. This step helps in reducing the dimensionality of the log data.

### Word Embedding

To transform log templates into numerical representations, we utilize the FastText library to train a word embedding model. Word embeddings allow us to convert log templates into vectors of real numbers. We use the continuous bag-of-words (cbow) model, as it efficiently captures semantic meaning, making it suitable for large datasets like the Blue Gene/L logs.

### Feature Engineering

The word embedding model is employed to generate feature vectors for each log sequence. These feature vectors represent the average of the word embedding vectors for the log templates within a sequence. This step creates a numerical representation of log sequences that can be used for machine learning.

### Machine Learning

We leverage machine learning techniques for the final anomaly detection task. In this project, we utilized a Gaussian Naive Bayes classifier as one example, but various other classifiers such as random forests, support vector machines, or neural networks can also be employed. The model is trained to classify log sequences as either anomalous or normal based on the extracted features.

## Implementation Details

### Log Parsing

- Blue Gene/L logs are composed of headers and descriptive messages.
- We focus on the descriptive messages and discard the headers.
- Parameters within the log messages are replaced with a wildcard token `<*>` to create log templates.
- Drain parser is used for log parsing and template creation.

### Vectorization

- The log templates are replaced by their indices in the dictionary to reduce resource usage.
- Each log template index is converted into a vector using the trained FastText model.
- Log sequences are transformed into feature vectors by averaging the rows of their coordinate matrices.

### Machine Learning Models

We trained multiple machine learning models for anomaly detection, including:
- Gaussian Naive Bayes (GNB)
- Decision Tree (DT)
- Random Forest (RF)
- AdaBoost (AB)
- XGBoost (XB)
- Multi-Layer Perceptron (MLP)

### Evaluation Metrics

For evaluating the performance of the models, we use standard metrics such as:
- True Positives (TP)
- False Positives (FP)
- True Negatives (TN)
- False Negatives (FN)

These metrics help us assess the accuracy, precision, recall, and F1-score of our anomaly detection models.

## Citation

This project is inspired by and attempts to replicate the methods presented in the paper:
- **Title:** Anomaly Detection in Log Files Using Selected Natural Language Processing Methods
- **Authors:** P. Ryciak, K. Wasielewska, A. Janicki
- **Published:** Applied Sciences, 2022
- **DOI:** [https://doi.org/10.3390/app12105089](https://doi.org/10.3390/app12105089)

## Usage

To use this code for anomaly detection in your own log files, follow these steps:

1. Clone the repository to your local machine.
2. Install the required libraries and dependencies.
3. Replace the sample log data with your own log files.
4. Run the provided Python script to perform log parsing, feature engineering, and anomaly detection.
5. Evaluate the results using the provided evaluation metrics.

## License

This project is licensed under the A special issue of Applied Sciences (ISSN 2076-3417). This special issue belongs to the section Computing and Artificial Intelligence.

## Acknowledgments

I would like to acknowledge the authors of the paper for their valuable research in the field of log file anomaly detection.

## Future Improvements

 1. Unsupervised Learning: Incorporate unsupervised anomaly detection methods like autoencoders or Variational Autoencoders (VAEs) to identify anomalies without the need for labeled data.
 2. Deep Learning Models: Consider exploring deep learning architectures such as recurrent neural networks (RNNs) or transformer-based models (e.g., BERT) for log sequence analysis. These models may capture more complex dependencies and semantic information within log data.
