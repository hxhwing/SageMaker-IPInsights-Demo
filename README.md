# SageMaker-IPInsights-Demo

## [IP Insights]((https://docs.aws.amazon.com/sagemaker/latest/dg/ip-insights.html))
----

Amazon SageMaker IP Insights is an unsupervised learning algorithm that learns the usage patterns for IPv4 addresses. It is designed to capture associations between IPv4 addresses and various entities, such as user IDs or account numbers. You can use it to identify a user attempting to log into a web service from an anomalous IP address, for example. Or you can use it to identify an account that is attempting to create computing resources from an unusual IP address. Trained IP Insight models can be hosted at an endpoint for making real-time predictions or used for processing batch transforms.

SageMaker IP insights ingests historical data as (entity, IPv4 Address) pairs and learns the IP usage patterns of each entity. When queried with an (entity, IPv4 Address) event, a SageMaker IP Insights model returns a score that infers how anomalous the pattern of the event is. For example, when a user attempts to log in from an IP address, if the IP Insights score is high enough, a web login server might decide to trigger a multi-factor authentication system. In more advanced solutions, you can feed the IP Insights score into another machine learning model. For example, you can combine the IP Insight score with other features to rank the findings of another security system, such as those from Amazon GuardDuty.

The SageMaker IP Insights algorithm can also learn vector representations of IP addresses, known as embeddings. You can use vector-encoded embeddings as features in downstream machine learning tasks that use the information observed in the IP addresses. For example, you can use them in tasks such as measuring similarities between IP addresses in clustering and visualization tasks. 

## Input/Output Interface for the IP Insights Algorithm 
----

### Training and Validation

The SageMaker IP Insights algorithm supports training and validation data channels. It uses the optional validation channel to compute an area-under-curve (AUC) score on a predefined negative sampling strategy. The AUC metric validates how well the model discriminates between positive and negative samples. Training and validation data content types need to be in text/csv format. The first column of the CSV data is an opaque string that provides a unique identifier for the entity. The second column is an IPv4 address in decimal-dot notation. IP Insights currently supports only File mode. For more information and some examples, see [IP Insights Training Data Formats](https://docs.aws.amazon.com/sagemaker/latest/dg/ip-insights-training-data-formats.html).

### Inference

For inference, IP Insights supports text/csv, application/json, and application/jsonlines data content types. For more information about the common data formats for inference provided by SageMaker. IP Insights inference returns output formatted as either application/json or application/jsonlines. Each record in the output data contains the corresponding dot_product (or compatibility score) for each input data point. For more information and some examples, see [IP Insights Inference Data Formats](https://docs.aws.amazon.com/sagemaker/latest/dg/ip-insights-inference-data-formats.html). 
