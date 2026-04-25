## What is Airflow?
Apache Airflow is an open-source platform for developing, scheduling, and monitoring batch-oriented workflows. Airflow's extensible python framework enables you to build workflows connecting with virtually any technology. A web-based UI helps you visualize, manage, and debug your workflows. You can run Airflow in a variety of configurations - from a single process on your laptop to a distributed system capable of handling massive workloads.

### Workflows as code -
Airflow workflows are defined entirely in python. This 'workflows as code' approach brings several advantages:

- Dynamic: Pipelines are defined in code, enabling dyamic Dag generation and parameterization.
- Extensible: The Airflow framework includes a wide range of built-in operators and can be extended to fit your needs.
- Flexible: Airflow leverage the Jinga templating engine, allowing rich customizations.

### DAGs
DAG (Directed Acyclic Graph) is a powerful tool for managing these workflows efficiently and avoiding errors. 
A Dag is a model that encapsulates everything needed to execute a workflow. Some Dag attributes include the following:

Schedule: When the workflow should run.
Tasks: tasks are discrete units of work that are run on workers.
Task Dependencies: the order and conditions under which tasks execute.
Callbacks: Actions to take when the entire workflow completes.
Additional Parameters: And many other operational details.

[To Understand DAGs in better way](https://www.datacamp.com/blog/what-is-a-dag?utm_cid=19589720824&utm_aid=152984013334&utm_campaign=230119_1-ps-other~dsa-tofu~all_2-b2c_3-apac_4-prc_5-na_6-na_7-le_8-pdsh-go_9-nb-e_10-na_11-na&utm_loc=9062095-&utm_mtd=-c&utm_kw=&utm_source=google&utm_medium=paid_search&utm_content=ps-other~apac-en~dsa~tofu~blog~data-engineering&gad_source=1&gad_campaignid=19589720824&gbraid=0AAAAADQ9WsHZw9pjyd6qT0YNsb_Xgd5--&gclid=CjwKCAjwzLHPBhBTEiwABaLsSuuaKTYFCAYhJ2Tusqq7_O-vcsgRuB92W6uLnvSk03vu0KZVn6PnhhoCXCIQAvD_BwE)
