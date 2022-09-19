# Scenario - Track KPIs to increase plant capacity 
<img style="float: right" src="https://github.com/QuentinAmbard/databricks-demo/raw/main/manufacturing/oee_score/ooe_production_factories.png" width="600px" />

An Aerospace manufacturing company has launched a Factory of the Future manufacturing initiative to streamline operations and increase production capacity at its plants and production lines. 

Leveraging a __Lakehouse Architecture__ *Plant Managers* can assess __KPIs__ to  calculate shift effectiveness and communicate with equipment operators and then adjust the factory equipment accordingly.

This requires real-time KPIs tracking based on multiple datasources, including our factories sensor and external sources, to answer questions such as:

* What's my current avilability
* What was my past Performance
* Do I have a factory under-performing and perform root cause analysis
* ...

Let's see how to implement such a pipeline

## Why OEE?
Overall Equipment Effectiveness (OEE) is a measure of how well a manufacturing operation is utilized (facilities, time and material) compared to its full potential, during the periods when it is scheduled to run. [References](https://en.wikipedia.org/wiki/Overall_equipment_effectiveness). 

OEE is the industry standard for measuring manufacturing productivity. OEE is calculated using 3 atttributes

1. **Availability:** accounts for planned and unplanned stoppages, percentage of scheduled time that the operation is/was available to operate. *i.e.* __(Healthy_time - Error_time)/(Total_time)__
2. **Performance:** measure of speed at which the work happens, percentage of its designed speed. *i.e.* __Healthy_time/ Total_time__
3. **Quality:** percentage of good units produced compared to the total units planned/produced. *i.e.* __(Total Parts Made -  Defective Parts Made)/Total Parts Made__

## The Medallion Architecture for IOT data

Fundamental to the lakehouse view of ETL/ELT is the usage of a multi-hop data architecture known as the medallion architecture.

This is the flow we'll be implementing.

- Incremental ingestion of data from the sensor / IOT devices
- Cleanup the data and extract required informations
- Consume our worksforce dataset coming from our SalesForce integration
- Merge both dataset and compute real-time aggregation based on a temporal window.


<img style="float: right" src="https://github.com/QuentinAmbard/databricks-demo/raw/main/manufacturing/oee_score/ooe_flow_0.png" width="1000px"/>


Databricks Lakehouse let you do all in one open place, without the need to move the data into a proprietary data warehouse - thus maintaining coherency and a single source of truth for our data.

In addition to this pipeline, predictive analysis / forecast can easily be added in this pipeline to add more values, such as:

* Predictive Maintenance
* Anomaly detection
* ...

___

&copy; 2022 Databricks, Inc. All rights reserved. The source in this notebook is provided subject to the Databricks License [https://databricks.com/db-license-source].  All included or referenced third party libraries are subject to the licenses set forth below.

To run this accelerator, clone this repo into a Databricks workspace. Attach the RUNME notebook to any cluster running a DBR 11.0 or later runtime, and execute the notebook via Run-All. A multi-step-job describing the accelerator pipeline will be created, and the link will be provided. Execute the multi-step-job to see how the pipeline runs.

The job configuration is written in the RUNME notebook in json format. The cost associated with running the accelerator is the user's responsibility.
