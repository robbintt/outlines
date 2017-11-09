## Installing, Deploying, Using Tensorflow in Python

Speaker: Chris Fregley, Pipeline.ai (former Netflix, Databricks, kickstarted Spark.)

https://github.com/PipelineAI/pipeline/

Zero respect for Python until he found Scientific Python.

PySpark not his favorite, rather use Scala for Spark, originally a Java guy

Slides available on meetup: [slides](https://www.slideshare.net/cfregly/optimizing-profiling-and-deploying-tensorflow-ai-models-with-gpus-san-francisco-python-meetup-nov-8-2017)

[Great GPU notebooks and examples](https://github.com/PipelineAI/pipeline/)

This guy is such a salesman.  He used port 6969 because of port colissions. Clever.


## Notes from meetup site

Main talk (~30 mins + Q&A)

Optimizing, Profiling, and Deploying High-Performance Spark ML and TensorFlow AI Models in Production with GPUs

Using the latest advancements from TensorFlow including the Accelerated Linear Algebra (XLA) Framework, JIT/AOT Compiler, and Graph Transform Tool, I’ll demonstrate how to optimize, profile, and deploy TensorFlow Models - and the TensorFlow Runtime - in GPU-based production environment. This talk is 100% demo based on open source tools and completely reproducible through Docker on your own GPU cluster.

Bio Chris Fregly is Founder and Research Engineer at PipelineAI, a Streaming Machine Learning and Artificial Intelligence Startup based in San Francisco. He is also an Apache Spark Contributor, a Netflix Open Source Committer, founder of the Global Advanced Spark and TensorFlow Meetup, author of the O’Reilly Training and Video Series titled, "High-Performance TensorFlow in Production."

Previously, Chris was a Distributed Systems Engineer at Netflix, a Data Solutions Engineer at Databricks, and a Founding Member and Principal Engineer at the IBM Spark Technology Center in San Francisco.


## Tensorflow!

Mostly in C.  

- Neural networks never want to go to production
- always want to be retrained
- want someone else to do the last 20%


## Pipeline.ai

A framework to get your models into solution. Something about data pipelines!



## Today - TensorFlow (TF) - Condensed talk: 8 hour into 30 minutes

Optimize and Deploy TF models to production.

Nice to have a working knowledge of TF.

GPU heavy talk.


## Content Breakdown

50% training optimizations(GPUs, Training Pipeline, JIT)
50% prediction optimizations (AOT Compile, TF Serving)

Why heavy focus on 'model prediction' vs 'just training'?

Training - boring and batch!
Prediction - exciting and real time!


## Agenda - see the slides

Biggest thing is telling data scientists that they can deploy from their jupyter notebook in a controlled manner. Ability to push it out & roll it back.


## DOCKER - Package model and runtime as one

- Docker for mac - opened up a ton of use cases! 
    - no surprises in production
    - deploy and tune model + runtime together
    - same local, dev, production env

Production always a bit different than development before this. A bunch of virtualbox cruft. 

**Did he consider vagrant?** I think docker just blows vagrant away for developers, removes tons of devops.


## Tune Model + Runtime together!  (see slides!)


## Offline models aren't always going to do well online... (see slides)

Online - real-time metrics. **Cost per prediction!**

The prediction profiling and tuning stuff is about bot identification.


## Pipeline AI - Continuous Model Training

Identify and fix borderline predictions. Hotdog - not hotdog.

Use crowdflower to label the data - then relabel along the classification's edges.

Shift traffic to winning model using AI Bandit Algorithms.

"Once we drain this experiment of its value... we can stop this experiment."


## Shift traffic to minimum "Cloud Cost"

Google Cloud vs Amazon Web Services

Shift to amazon when the cloud instances are cheaper. Shift back and forth. 

He made fun of microsoft azure but plugged their kubernetes support.


## NVIDIA GPU Half-Precision Support

- All about Volta V100 (2017)  - AMD - tensor cores / Google TPUs
- Pascal P100 (2016)

- FP32 = Full Precision
- FP16 = Half Precision
- Half good for approximate deep learning use cases
- Fit two FP16s into FP32 GPU cores for 2x throughput!!
- Thunk to 32 bit 

Nvidia: P100, M40, K40 - all tested for whatever reason



## AMD? - GPU CUDA Programming 

- Barbaric, fun. Must know hardware. Probably hate your life. 
- Optimized for same instruction, multiple thread. 
- Do not like if-statement. Like half the cores go unused.
- Independent thread scheduling - finally
- CUDA Streams
    - Tensorflow uses this heavily
    - goal is to saturate cpus

## Check out Batch Normalization 

- Almost always use batch normalization - except rarely you should never use batch normalization
- Technique from 2015 
- gradient descent
- don't want the network to learn the order the data is showing up
- first part of pipeline is shuffle
- normalize per batch
- normalize per layer
- each mini batch may have wildly different distributions


## Dropout

- sniff connections in your network
- prevent overfitting
- ensemble different neural architectures
- randomly, 50% sniff these things, purposely cripple it
- figure out ways to distort things they are trying to block out (spaces, numbers)
- more difficult for the network, better the final network was


## this guy something or other - his friend

- https://github.com/yaroslavvb/stuff


## DON'T USE FEED_DICT

- feed_dict Requires Python<->C++ Serialization
- Dataset API
- what happened to dataframe? it's gone i guess? tensorflow went right to dataset api


## Tensorflow Debugger - mouse from a terminal it's crazy, only Google...


## ALWAYS START WITH `estimator` AND `experiment` APIs

These come from Google trying to productionize tensorflow, probably successfully.

See the slide, has the above title!!!!!!!!

- Skip all the early demos you see, they are old and crusty. 
- These simplify model building.
- flexible parameter tuning
- enable rapid model experiments
- 

### Estimator API

See the slides.

- Train-to-Serve Design
- Create custom or use a canned Estimator
- Hides session, graph layers, 

- Chief:Worker
- Supervisor:Worker
- getting away from master but not improving their language... just changing it...


#### Canned Estimators

See the slides, 60% use prebuilt, 40% roll their own estimator

- Commonly used estimators
- Pre tested and pre tuned


#### Multi-headed inference: `Single-Objective Estimator` vs `Multi-Objective Estimator`

Get two answers (objectives out of one estimator or something).

## Hparams - Hyper parameter tuning

Do a big grid search, a parameter as a range. 

## Layers API exists


## Use kubernetes or mesos

Good cluster organizer for working on this stuff...

## JIT Compiler - and visualizing

Need to do a Python Context Manager `with device as... whatever` to use JIT.

Historically: Spark & Project Tungsten would take your code and create your plan into an optimized one and then to a physical plan.

Built on XLA - accelerated linear algebra framework.

- Goals
    - reduce memory Movement
    - reduce overhead of multiple function calls


## AOT Compiler - Standalone, Ahead-Of-Time (AOT) Compiler

For super tiny devices... pass in your graph.  
Build up DAGs of operations in spark and tensorflow.

- tfcompile - point to input for graph and output for graph
- built on XLA framework
- creates functions with feeds (inputs) and fetches (outputs)
- figures out what everything... .so files, what bare minimum is necessary
- **creates binary down to 600k** - this is how we fit in the apple app store or not.
- shrink, shrink, tons of slides, freeze for production


## request batch tuning

At the end of the day the forward prop. is just matrix multiplies.

See slides

- max_batch_size
- batc



# There's like 60 slides left !! Damn, lots of content.


