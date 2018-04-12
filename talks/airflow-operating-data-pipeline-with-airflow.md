# Operating Data Pipeline with Airflow

- Speaker: Ananth Packkildurai @ Slack (chat app)
- Date: 2018.04.11
- Location: WePay

## Notes


## 4 Types of Executors - Max freestyles at the end

Max says - most people should start using KubernetesExecutor when it comes, which is soon.

Max says - LocalExecutor isn't for production, but it at some point has been deemed OK for production. At some point you will go out and get the biggest machine you will get and it won't work.

This includes the new `KubernetesExecutor`.

1. LocalExecutor - Python MultiProcessing Queue of the size you specify
    - say you want to run 125 slots in your multiprocessing queue
    - runs as part of the scheduler process
    - or runs in the process as backfill
    - if the scheduler fails, it would lose contact with the queue
1. CeleryExecutor - Simple-ish abstraction for running remote tasks
    - use redis or rabbitmq broker
    - put the message in the queue that says 'please worker pick up the task locally'
    - as many workers and queues as you want, workers watch queues and look at messages
    - workers run messages if they have them
    - original intent was a yarn executor, but it was hard to do because yarn is a resource negotiator, so it didn't make a lot of sense, hacky not good containerization support for yarn
1. KubernetesExecutor: Daniel at Bloomberg is contributing this - open PR in the process of being merged, all the code is there
    - They are using it in production at bloomberg
    - airbnb looking to use it in production
    - use kubernetes API, no local celery in kubernetes... actually use kubernetes...
    - scheduler in a pod in or out of kubernetes
    - airflow containerization was an afterthought but should have been first maybe in hindsight
1. (heh whoops which one is the third?) Maybe DaskExector...
    



## Slack

- 10 data engineers
- 1000 employees
- 6M users

- 1 in 2 per week access data warehouse (trent: what?)
- 600,000 events per second at peak
- 500+ tables

- 240+ active DAGs
- 5400+ tables per day
- 68 contributors

We have 68 contributors engaging in airflow or building data pipelines despite having 10 data engineers.

Democratizing data access.


## Agenda

1. Airflow Infrastructure
2. Scale Airflow Executor
3. Pipeline Operations
4. Alerting and Monitoring


## Airflow Infrastructure

- Local Executor
- Tarball code deployment
- Continuous deployment with Jenkins
- Flake8, yapf & pytest
- `airflow.sh` shell utility to ensure consistent development environment for all the users.

## Scale Airflow Executor

Airflwo Multi Retryable Sensors

- local executor launches new interpreter per task, which takes significant resources.
- but we can do multiple external tasks in a single interpreter...
- he put the code up but i didn't really get to read all of it, maybe its online


## Pipeline Operations


#### Airflow Fallacies

- the upstream task success is reliable
- the task remain static after the success state
- the DAG structure is static
    - people update or delete the dag
- the data quality is not part of a task life cycle
    - definitely a complaint, based on system workflow


### MARIO - global dag operator (cli tool)

- `$ ./mario --help`
- do stuff like `clear downstream`, export a graphml represenation of downstream
- tons of other diagnostic stuff...


### Data Quality Checker - `dqcheck`

Need lots of stuff if you're running 240+ dags, no easy way to visually look and see if some dag's task is in some particular state easily... (trent: lots of ways to do this automatically, they do it automatically)_

- `from slack.airflow.data_quality import DQCheck`
- do stuff like check if the row count is > 0
- Hive partition sensor operator
- delete_dag - if a dag is not active in the dagbag, clean up after it (delete all tables related to dag)


### DAG Policy Validator

- `test_external_tasks` - check if external tasks point to valid DAGs and tasks.
- `test_circular_dependencies` - check if tasks have circular dependencies **across** DAGs.
- `test_priority_weight` - check that production tasks do not depend on lower priority task
- `test_on_failure` - require that highpriority DAGs have an on-failure alert.
    - just basically make sure you get notifications for that set of dags on failure... what's the test just read the dag or import it and check its python attrs?
    - seems like it would be good to sandbox this too, maybe overwrite the send list after importing it and send it to a different set of people...
- `test_sla`  - require that high-priority DAGs have an SLA
- `test_sla_timing` - SLA timing should make sense. No job should depend on a tas kthat has an equal or longer SLA than it does....
- `test_has_retry_and_success_callbacks` - Require an on-success_callback for tasks with an on_retry_callback.
- `test_require_dq_for_prod` - require sq check for all the high priority tasks.


## Alerting and Monitoring

OnCall Alert Callback

I took a photo of OncallAlertCallback for on call engineers.

- Alerting should be reliable
- Alerts should be actionable
- 
- 

