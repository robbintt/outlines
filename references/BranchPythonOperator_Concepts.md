## BranchPythonOperator

There isn't very good documentation for this feature yet.


### Why?

The `BranchPythonOperator` is used to create control flow in a `DAG`.


#### Towards Automating Changes to Data

If there is unexpected input from a data source, then automate preprocessing the new data format so the automation can be improved.

NB: This type of branch would probably trigger another DAG.


### Inter-task communication

There are two options:

- `variables`
- `XComs`

Variables sit in a global `variables` object, where as `XComs` are pushed and pulled between tasks.


#### Passing Context to `BranchPythonOperator`

`BranchPythonOperator` inherits from `PythonOperator` and is defined in the same module.  Both share use of `provide_context=True` as a keyword argument. If this is passed, the `python_callable` function must receive `**kwargs`.  The `context` includes `task_instance.xcom_pull` which pulls information from other tasks.




### Notes

Each branch must point to a task; if there isn't anything to do, use a `DummyOperator`.

### References


#### General

- [Airflow 'gitter' chat](https://gitter.im/apache/incubator-airflow)
- [Common Pitfalls (Official)](https://cwiki.apache.org/confluence/display/AIRFLOW/Common+Pitfalls)
- [medium/handy-tech: Airflow Tips, Tricks, and Pitfalls](https://medium.com/handy-tech/airflow-tips-tricks-and-pitfalls-9ba53fba14eb)
- [Branching & XComs](https://github.com/geosolutions-it/evo-odas/wiki/Airflow---about-subDAGs,-branching-and-xcom)
	- NB: `subdags` are being deprecated in the future in favor of triggering another dag


#### Examples 
- [Example: XCom](https://github.com/apache/incubator-airflow/blob/master/airflow/example_dags/example_xcom.py)
- [Example: Branch Operator](https://github.com/apache/incubator-airflow/blob/master/airflow/example_dags/example_branch_operator.py)


#### Concepts & Tutorials
- [Concepts](http://pythonhosted.org/airflow/concepts.html)
- [Concepts: Branching](https://airflow.incubator.apache.org/concepts.html#branching)
- [Concepts: XComs](https://airflow.incubator.apache.org/concepts.html#xcoms)
- [Tutorial: Instantiate a DAG](https://airflow.incubator.apache.org/tutorial.html#instantiate-a-dag)
- [Default Arguments](https://airflow.incubator.apache.org/tutorial.html#default-arguments)
- [Template Variables & Macros](https://airflow.incubator.apache.org/code.html#macros)
- [ETL with Airflow: Principles](https://gtoonstra.github.io/etl-with-airflow/principles.html)
- [Airflow CLI - Command Line Interface](https://airflow.incubator.apache.org/cli.html)


#### API Reference

- [BaseOperator](https://airflow.incubator.apache.org/code.html#baseoperator)
- [TaskInstance.xcom_pull](https://airflow.incubator.apache.org/code.html?highlight=taskinstance#airflow.models.TaskInstance) 
	- `BaseOperator.xcom_pull` imports `TaskInstance.xcom_pull` from `context`
    - You must pass `key=None` or any desired key/value to get tasks that are from `xcom_push`
    - By default tasks from `xcom_push` are ignored


#### Source Code
- [BashOperator](https://airflow.incubator.apache.org/_modules/bash_operator.html#BashOperator)
- [BaseOperator](https://airflow.incubator.apache.org/_modules/airflow/models.html#BaseOperator) 
- [PythonOperator & BranchPythonOperator](https://github.com/apache/incubator-airflow/blob/master/airflow/operators/python_operator.py)
- [SSHExecuteOperator](https://airflow.incubator.apache.org/_modules/ssh_execute_operator.html) 
	- `xcom_push` inherited from `BaseOperator`
	- `BaseOperator` imports `TaskInstance.xcom_push` from `context`