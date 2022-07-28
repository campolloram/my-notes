# Airflow main components
- Webserver -> UI for monitoring DAGs Runs
- Scheduler -> Deamon looking for DAGs to run
- Executor -> Config of your cluster
- Metastore -> Database containing all information

## DAG
No surprise in here, Airflow uses DAGs to manage dependencies between tasks. You define your workflow which gets transalated to a DAG and that is what Airflow uses to optimize the scheduling of your Workflow.

## Airflow Operators
An airflow operator is like an object encapsulating the task to run.

There are 3 different types of Operators
- Action operators -> Operators in charge of executing something (Python Operator, Bash Operator, Postgres Operator)
- Transfer Operator -> Transfering data from a source to destination, like Presto to MySQL
- Sensor Operator -> Allows you to wait for something to happen before completing. e.g. Waiting for a file to land or a certain insert in a DB.

### Task Instance and WorkFlow
- A Task Instance is nothing more than an instance of an operator in your DAG

- A combination of all the concepts (Operators, Dependencies between them, DAG, etc.)


### What Airflow is NOT!
- Not a data streaming solution neither a data processing framework. If you wanted to do that you will need to use spark operator for example and monitor that using airflow.



