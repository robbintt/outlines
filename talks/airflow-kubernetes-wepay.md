# Airflow on Kubernetes at WePay

- Speaker: William @ WePay
- Where: WePay @ Redwood City
- When: 2018.04.11

"Tell them what you are going to tell them, tell them, and tell them what you told them."

"I now refer to dags as dags, but I swore that we should change the culture and call them workflows and now I am calling them dags. But we should call them workflows." - William

trent: it sounds like they version their dags somehow...

Question: Are you versioning your DAGs?  No we are using `git describe` so counting up version from a parent.

## Initial (non k8s) deployment

- Airflow under supervisord (scheduler and webserver on same box)
- Manually ssh & pip install
- Cron job every 2 minutes to git pull and update the dags
    - not a good approach to anything... sorry...
    - couple layers of review... one person reviews the commit for a few minutes and says "sure (implied ok whatever)"


## Issues

- Everyone running on the same airflow
- No isolation (resources, dependencies)
- Deploys are monolithic
- Scalability
- Limited Availability
- Cowboy Culture: ssh to box and run commands: We had pets not cattle (snowflakes)

## Configuration

- nginx sidecar
- airflow scheduler and webser still in the same pod
- cloudsql
- elk kubernetes
- still running under supervisor
- no more cron job to git pull DAGs, moved to situation where manually push endpoint on pod to get new dags (pull tarball artifact), not terribly interesting

## Benefits

- control deployment
- easily deployed: cattle
- DAG deployment
- isolation / security
- scalable (multiple airflows per team)
- docker
- secrets

## KubernetesExecutor / KubernetesOperator (K8SOperator)

Very excited to do this. We use the localexecutor with kubernetes pods so we don't need celery.



