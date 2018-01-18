# Advanced DATA ENGINEERING PATTERNS with Airflow

## Speaker: Max Beauchim, Creator of Airflow and Superset
- currently @ Lyft (was at Airbnb)
- prev. `Data Engineer` at Facebook, inspiration!

He is wearing an Airflow shirt... how do I get an Airflow shirt?

Check out his medium account, there are a few interesting blog posts on there.

Teespring is an airflow user. He will do a batch and send a link over the next few days.

There are a bunch of frameworks for running jobs every 5 minutes or every minute.


## Qbiz data consulting firm guy says during questions:

- 3/4 of our customers use AutoDAG.

Answer:

- With superset, it is not a scheduler. It could expose an endpoint where airflow could call an endpoint where the queries run and write a pipeline out of it.


## What is Data Engineering?

In charge of building `data models` and `data pipelines` that organize information in a way that it can power the processes of the people in the company.

He wrote a blog post `The Downfall of the Data Engineer` discussing challenges today.
 
Another post `Functional Data Engineering` about data engineering design patterns.

## Apache Airflow

A batch workflow orchestrator. Especially for `large data pipelines`.

The tasks really accumulate and orchestrating really become a challenge... denormalize, something, something else....

### What is Airflow - 5 min

- An open source platform to author, schedule, and monitor batch processes.
- It's the glue that binds your data ecosystem together.
- It orchestrates tasks in a complex network of job dependencies.
- It's Python all the way down.
- It's popular and has a thriving open source community.
- It's expressive and dynamic, workflows are defined in code.


Airflow is `configuration as code` and `pipelines as code`.

We are going to get into why `configuration as code` is such a powerful concept.

DAG is a fancy acronym that also just means workflow in this context (and Directed Acyclic Graph).

Hive and Spark operators with a DAG to define `topology` of `workflow`.

### Data Engineering Patterns - Foundational Pattern for all examples

Concept: `building data pipelines dynamically`

A classic data warehouse is pretty static. Dimension tables, fact tables. Processes roughly for every table.

Airflow is dynamic, breaks out of this pattern. Pipelines dynamically built that read configuration.

#### Configuration as code

Why use code instead of drag-and-drop data pipelines?  Because it naturally gets source control and design patterns are easier to pull and collaborate on.

Configuration as code is more powerful than `good ole configuration files`.

- Code is more expressive, powerful, and compact
- Resuable components (functions, classes, object factories) come naturally in code.
- An API has a clear specification with defaults, input validation, and useful methods.
- Allow users to hook logic to configuration as callbacks.
- SEE IMAGE IN PHONE FOR REST.
- 


#### Conceptual Model

- SEE PHOTO



##### Example 1: AB Testing Example

Lets change a Lyft button to be a brighter shade of pink.  Airflow script to read configuration of all these experiments and metrics and weave a workflow of dependency based on the input of the user.

As the workflow executes, it waits on source data, processes metrics and experiments. Comes out with P-value, confidence interval, other computations.  These become exposed in the UI.


#### Computation Frameworks

- `AutoDAG` at AirBnB - lots of people run sql and they just want to schedule it to run every day. Might not want to set up a pipeline.
    - Built a simple UI as an airflow plugin, `AutoDAG`, they paste what they run and give it a target table, finds dependencies, creates waitfor operator, hivepartitionsensors, lints code and gives advice, and schedules the workflow and alerts on failure.
    - Simplest implementation of this pattern
    - Source code for autodag is extremely simple, couple dozen lines of code.


##### Example 2: Engagement & Growth Metrics - web companies and most industries, aka "Growth Accounting Metrics"

DAU, WAU, MAU / new, churn, resurrected, stale and active users

Wrote this for all of facebook then replicated for different verticals: photos, messaging, photo uploads - anything you can think of we wanted a flavor of this pipeline.

Count distinct metrics are ... slide is gone... (try to get the slides)

Framework reads the config file and builds a very complex framework on your behalf.

###### Behind the scene / at Facebook

There's a photo that has a bunch of bullets for how this configuration works (he said 'behind the Python')

- Runs optimized logic
  - If building the same pipeline over and over, some older ones won't be optimized. Why not improve the old whenever you improve the new?
- Cut the long tail of high cardinality dimension as specified
  - Give parameters instead of tons of parameters and the framework does it automagically for you.
  - In theory crafts a dashboard on your behalf.


#### Experimentation

Based largely on how it's done using Airflow at AirBnB.

Their complex dags are MASSIVE at airbnb.  Nested in a complicated way. This looks to be a couple hundred root tasks.


1. Wait for source data
1. Load source data into `metric repository`
  - He could do a talk on what a `metric repository` might be.
  - A skinny table with a lot of rows... joins to `experimental assignments` and `experimental stats`
1. ... (slide moved on)
1. ... (slide moved on)
1. ... (slide moved on)

No photo for the above 5 points, get the slides?


##### More Complexity

- `Cookie->userid` mapping
- event level attributes, dimensional breakdowns
- different types of subjects (host, guests, listing, cookie, ...)
- different types of experimentation (web, mobile, emails, tickets...)
-  ... (slide moved on, see photo)
- statistics beyond pvalue and confidence intervals, preventing bias, global impact, time-boxing


#### Need for ML Feature Repository

Where you put all your entity centric methods that are useful to train your machine learning models.

Instead of reinventing the wheel for each model you are training.

- Entity-centric methods used to train ML models
- centralized & reusable across models
- consistent reproducible.
- smart and efficient around time-windowing
  - life-to-date metrics
  - how many times over the last 7- or 28-days that a user performed a certain action
  - use a YAML file to define what might be interesting
- hooks for training and scoring
  - hooks are out of the `metrics repository`


#### Stats Daemon

- This is not open source. It seems like there is a lack of followthrough. He thought people would start open sourcing high leve.
- Running a sql express engine against the partition.


##### How to make a Stats Daemon

He verbally said the following:

- A `stats daemon` is the idea of computing database stats on top of your data warehouse.  - 
- People who know about classic RDBMS, mysql, oracle, postgres, etc. These stats are stored in the schema for the query optimizer to plan.- 
- Hive etc. do not compute these stats but people can leverage these stats too, beyond the query optimizer.- 
- Every time we see something changes in hive or hive metadata we compute a bunch more metadata.- 

(See photo for this slide and copy the text below... )

- 
- 
- 
- 
- 

Model metastore, ask metastore for schema of table, ask rule engine to build sql automatically. Use presto and pivot the result, attach to partition in a skinny table.


#### More!

- Anomoly Detection
- Production MySQL exports
- AirOlap: Loads data into druid.io
  - druid.io - in-memory column store that's really fast
- Email targeting rule engine
  - Complex rules to determine who gets what email - no marketing email in 3 days and no lyft ride in 7 days... do the right thing
- Cohort analysis and user segmentation (prototype)
- [Insert your common pattern here]
  - Knowing you can write dynamic python you can find your own place to apply this pattern.


#### Conclusion

METADATA ENGINEERING!

- Airflow allows you to take data enginering to a whole new level.
- Data engineering should find common patterns in their work and build frameworks and services
- Building pipelines can be repetitive and inefficient. Data engineers should build machines that build pipelines.


