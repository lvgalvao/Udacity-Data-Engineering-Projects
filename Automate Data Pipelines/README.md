# What is a Data Pipeline?

A *data pipeline* describes, in code, a series of sequential data processing steps. Depending on the data requirements for each step, some steps may occur in parallel. Data pipelines also typically occur on a *schedule. Extract, transform and load (ETL)*, or *extract, load, and transform (ELT),* are common patterns found in data pipelines, but not strictly required. Some data pipelines perform only a subset of ETL or ELT.

Examples of data pipelines:

Personalized emails that are triggered after a data pipeline executed.
Companies commonly use data pipelines to orchestrate the analysis that determines pricing. For example, a rideshare app where you were offered real-time pricing.
a Bikeshare company, that wants to figure out where their busiest locations are. They might use this data to determine where to build additional locations, or simply to add more bikes. A data pipeline to accomplish this task would likely first load application event data from a source such as S3 or kafka. Second, we might take that data and then load it into an analytic warehouse such as RedShift. Then third, perform data transformations that identify high-traffic bike docks.


# These concepts are including in this unit:

<li> Data Validation
<li> Direct Acyclic Graphs (DAG)
<li> DAGs in Apache Airflow
<li> Building DAGs and running them in Airflow
<li> Data lineage in Airflow
<li> Data pipeline schedules
<li> Data partitioning
<li> Extending Airflow with Plugins
<li> Task boundaries
<li> and when to refactor a DAG

