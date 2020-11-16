# Overview
Blow is a summary of the tested points I came across during the GCP Professional Data Engineer Certificate Exam on 
16 November 2020. Also, I documented the materials which helped me prepare for the exam.

- List of tested points - **NOT** to serve as a full list of points you should go through before the exam but 
  only a list of points occurred in the exam I attended as far as I can recall. Tried to remember as many 
  and as clearly as possible, but the memory is not that great!
- Exam preparation materials with recommended efforts

The most heavy parts in the exam were Cloud Dataflow (which I also found most challenging) and choose among different 
storage options.

Note: 
Answers to the questions in this document should be correct as far as I understand but cannot be 100% guaranteed, 
so do understand the scenarios carefully and look at the answers critically. 

# List of tested points

`BigQuery`
 
- partitioned tables 
  - 2 questions - nothing unexpected once you went through the materials in the next section
- authorized views (dataset-level access)
  - nothing unexpected once you went through the materials in the next section
- audit data access logs (project-level or organization aggregated) to differentiate access for different users
- BigQuery ML
- stackdriver for monitoring 
  - question was like you want to monitor your BigQuery slot utilization, what you should do? 
    The answer was using stackdriver for monitoring BigQuery slot utilization
- RAND(), HASH(), stratified sampling with OVER() functions

`Cloud Storage
`
- high availability 
  - multi-regional buckets vs regional buckets
- choice of storage classes
  - standard, cold line, near line
- store data more economically
  - GCS storage cost compared with BigQuery storage cost

`Dataflow`

There are many questions about Dataflow and personally I found this was the most challenging part since Dataflow is not
used as much as other products in our daily task and found Apache Beam concepts difficult.

- side inputs
  - question was like you are processing streaming data with Dataflow and you want to enrich the data with static BigQuery data which is samll enough
    to fit in-memory, what you should do. I chose the answer with side inputs. There is another answer very similar but with
    side outputs, since I never heard of "side outputs" concept in Dataflow, so I ruled this out.
  - the point here is it is worth clearly understanding the concept of [side inputs](https://beam.apache.org/documentation/programming-guide/#side-inputs)
- KafkaIO 
  - Dataflow SDK for beam does support connecting to Kafka, so depending on the question, we do not have to replace Kafka 
    with Cloud PubSub. See the applications 
    - [Kafka to BigQuery using Dataflow](https://medium.com/google-cloud/kafka-to-bigquery-using-dataflow-6ec73ec249bb)
    - [Using Cloud Dataflow to Process Outside-Hosted Messages from Kafka](https://cloud.google.com/solutions/processing-messages-from-kafka-hosted-outside-gcp)
- Windowing
  - question was something like you have a Kafka cluster which expects to receive 5000 messages an hour, how do you detect issues where number of messages is under expectations, e.g., 4000 messages 
     an hour? Answer. Use Kafka connector with Dataflow
- [Flatten](https://beam.apache.org/documentation/programming-guide/#core-beam-transforms)
- [CoGroupByKey](https://beam.apache.org/documentation/programming-guide/#cogroupbykey)
- [updating pipeline with different windowing and triggering mechanism](https://cloud.google.com/dataflow/docs/guides/updating-a-pipeline#changing_windowing)
  - This document should be read in great detail and truly understand it. 
  - The question like you have want to update currently running dataflow pipeline with different windowing and triggering 
  mechanism, what should you do? The answers are like 1. update the pipeline with option --update, set the --jobname 
  the same as the running one; 2.  update the pipeline with option --update, set the --jobname to an uniquely new one; 3. use
  "drain" to stop the pipeline and set up a new pipeline; 4. use "cancel" to stop the pipeline and set up a new pipeline; 
  I was not sure between answer 1 and 3 because I remember this is some incompatibility issues and was unsure whether 
  changing windowing and triggering mechanism is one of them. After the exam, I checked the documentation and found the 
  above link explaining we need caution but we can update pipelines with changing windowing and triggering mechanism. 

`Cloud Dataproc
`
- migrating Spark jobs to Dataproc 
  - move Spark ML to the Cloud: use Dataproc and read data from BigQuery
- preemptible VMs
- I/O intensive requirements
  - [comparing HDFS vs GCS](https://cloud.google.com/solutions/migration/hadoop/migrating-apache-spark-jobs-to-cloud-dataproc#comparing_cloud_storage_and_hdfs)

`Cloud PubSub`

- [Kafka mirroring](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=27846330)
  - appeared in the exam
- [seek](https://cloud.google.com/pubsub/docs/replay-overview)


`Machine Learning 
`
- L1 and L2 regularization
- AutoML for customised modelling
  - the case was a shipping company want to detect the damaged package in transit
- credit risk 
  - question was like you have approved applicants and label them with defaults or not; the answers were: 1. you do 
  linear regression modelling of the client credits risks; 2. remove the bias 
  by adding data of rejected clients; 3. you enrich the data with client social profile so that you can do feature engineering).
  I chose the liner regression one but I was not really sure ...
  
- [feature crosses/ synthetic features]((https://developers.google.com/machine-learning/crash-course/feature-crosses/video-lecture)) 
  - there is one question about this, but I forgot how it was asked 
- TPU 
  The question had the keywords like "bulk matrices multiplication", "cost-effective" and "high-performance"
  The answers fall between two options with TPUs, 1. use TPU without any other configurations for custom ops; 2. use TPU with 
  GPU support for custom ops. My choice was 1.
- hyper-tuning: 
  - the questions was like you are using SVM to ... and you find the AUC was just 0.87 and you want to improve it, 
  what should you do? 
  The answer was hyperparameter tuning and the other answers were like use DL, for DL always beats SVMs, etc which can 
  be easily ruled out also. 

`Cloud Dataprep
`
- the question was about data transformation choices and the key words in the questions were for `non-developers` and needs `graphical UI`

`Cloud Spanner`

- [choose a primary key to improve performance](https://cloud.google.com/spanner/docs/schema-design#primary-key-prevent-hotspots)
- storage choice among other choices
  - question was like you have 20 TB of operational system transactions data to store, and you need consistence and SQL query the data;
  It is transaction data and SQL query, so it should be Cloud Spanner or Cloud SQL, but the data size is too big for 
  Cloud SQL. Thus the answer should be Cloud Spanner.


`Cloud SQL`
- [fail-over replica](https://cloud.google.com/sql/docs/mysql/high-availability)
- collect logs from MariaDB databases with Stackdriver logging agent
  - Maria DB is  a community-developed, commercially supported fork of the MySQL relational database management system (RDBMS)) using 

`Datastore` 
- snapshot and import Datastore export into BigQuery

`BigTable`
- single-cluster routing for replica


`Transfer Appliance` 
- The questions was like you have 40TB of data to move to the cloud within 6 months, but you have local network limitations 
(20MB/min), which should you do

`Security` 
- CSMK 

# Exam preparation materials

Here I list the materials I used to prepare for the exam and how much efforts I would recommend to give in terms of 
exam preparation.

## Must go-through materials 
Recommended efforts: 5/5, worth going through many times until you have no doubts.

1. [Official Exam Guide](https://cloud.google.com/certification/guides/data-engineer) 
1. [Official Sample Questions](https://cloud.google.com/certification/sample-questions/data-engineer)
1. [25 sample questions](https://www.coursera.org/learn/preparing-cloud-professional-data-engineer-exam/quiz/Lw6wR/ungraded-practice-exam-quiz
) at the end of the Coursera Course Preparing for the Google Cloud Professional Data Engineer Exam


## Highly recommended materials 
Recommended efforts: 4/5, worth going through at least twice until you have almost no doubts for sometimes the questions
themselves may not necessarily make sense.
1. A Cloud Guru practice exams (you can use the 7-day free-trail to access the exams but remember to cancel your subscription before free-trail ends!)
   1. [Practice Exam Google Certified Professional Data Engineer](https://practice-exam.acloud.guru/gcp-certified-professional-data-engineer?_ga=2.194162605.1687416408.1605519654-117888690.1605519654&_gac=1.216946276.1605519654.Cj0KCQiA48j9BRC-ARIsAMQu3WTfXIyASodBQK-jbHwruPbNN9CARYh8kNKLW-yIGYT8JY45K0u2RQYaAgofEALw_wcB)
   1. [Practice Exam Data Engineer - Final Exam](https://practice-exam.acloud.guru/fd871722-ab09-450b-8a3a-eac2852a84d5?_ga=2.27306684.1687416408.1605519654-117888690.1605519654&_gac=1.58220248.1605519654.Cj0KCQiA48j9BRC-ARIsAMQu3WTfXIyASodBQK-jbHwruPbNN9CARYh8kNKLW-yIGYT8JY45K0u2RQYaAgofEALw_wcB)
1. [Coursera - Preparing for the Google Cloud Professional Data Engineer Exam](https://www.coursera.org/learn/preparing-cloud-professional-data-engineer-exam/home/welcome)
1. Whizlab mock tests - 1 free + 4 paid tests 
1. [How I passed Google Professional Data Engineer Exam in 2020](https://towardsdatascience.com/how-i-passed-google-professional-data-engineer-exam-in-2020-2830e10658b6)
   - This post is very recent and covers a summary of exam questions which are highly relevant to the exam

## Recommended materials 
Recommended efforts: 3/5 worth going through at least once to familiarise yourself with GCP products
1. Qwiklabs courses:
    2. [Google Cloud Platform Big Data and Machine Learning Fundamentals](https://googlecourses.qwiklabs.com/course_templates/3?catalog_rank=%7B%22rank%22%3A1%2C%22num_filters%22%3A0%2C%22has_search%22%3Atrue%7D&search_id=5773044)
    3. [Modernizing Data Lakes and Data Warehouses with GCP](https://googlecourses.qwiklabs.com/course_templates/54?catalog_rank=%7B%22rank%22%3A1%2C%22num_filters%22%3A0%2C%22has_search%22%3Atrue%7D&search_id=5773058)
    4. [Building Batch Data Pipelines on GCP](https://googlecourses.qwiklabs.com/course_templates/53?catalog_rank=%7B%22rank%22%3A1%2C%22num_filters%22%3A0%2C%22has_search%22%3Atrue%7D&search_id=5773059)
    5. [Building Resilient Streaming Analytics Systems on GCP](https://googlecourses.qwiklabs.com/course_templates/52?catalog_rank=%7B%22rank%22%3A1%2C%22num_filters%22%3A0%2C%22has_search%22%3Atrue%7D&search_id=5773062)
    6. [Smart Analytics, Machine Learning, and AI on GCP](https://googlecourses.qwiklabs.com/course_templates/55?catalog_rank=%7B%22rank%22%3A1%2C%22num_filters%22%3A0%2C%22has_search%22%3Atrue%7D&search_id=5773071) 
1. [gcp documentations](documentation-reading-notes-and-quiz/) summarized by Lu
   - A good collection of the GCP products docs and highly relevant to the exam, covering several topics:
   BigQuery, Dataflow, Dataproc, PubSub
   - Note: this is not a full list of all products you need to know. e.g., BigTable, Cloud SQL, Cloud Spanner, Machine Learning, etc are missing
1. [How I Passed the Google Cloud Professional Data Engineer Certification Exam](https://towardsdatascience.com/passing-the-google-cloud-professional-data-engineer-certification-87da9908b333) 
