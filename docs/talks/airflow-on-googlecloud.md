# Running Airflow inside Google Cloud Platform

A lot of this was somewhat advertisement for GCP wrapped in Airflow. Could be useful for someone if they are already in this platform and want to hack some. It seems nice.

- Speaker: Trevor Edwards @ Google
- Location: WePay Redwood City
- Date: 2018.04.11

My notes on this will be sparse and focused on things I don't already know.

Max chimes in - yes only one airflow scheduler running!


## Questions (at the end)

- Someone says that Google is planning to release Airflow as a managed service. The speaker would not comment on that.
- How much would it cost? Maybe on the order of $100 a month to clone this architecture. Not publicly cloneable yet.


## Tools

- KubernetesEngine
- Redis for Celery
- Airflow Webserver on Google App Engine
- Google Cloud Storage for DAGs and logs


## Securing your Airflow Server


## How to distribute DAGs and Plugins quickly?

Many people use git workflows, we decided to use Google Cloud Storage.

Sidecar container rsyncs DAGs/Plugins every 5 seconds. You would need to change how often the scheduler pulls dags to every 1 minute.



# Scaling out Airflow Webserver


# Scaling the scheduler

- single process: no horizontal scaling
- GKE - scale things up

# Scaling out Airflow Worker

GKE Node pool with autoscaling can detect a worker at 99% and add another to the pool


# Stackdriver Logging & Monitoring - GKE out of the box...
