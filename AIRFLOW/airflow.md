## What is Airflow?
Apache Airflow is an open-source platform for developing, scheduling, and monitoring batch-oriented workflows. Airflow's extensible python framework enables you to build workflows connecting with virtually any technology. A web-based UI helps you visualize, manage, and debug your workflows. You can run Airflow in a variety of configurations - from a single process on your laptop to a distributed system capable of handling massive workloads.

### Workflows as code -
Airflow workflows are defined entirely in python. This 'workflows as code' approach brings several advantages:

- Dynamic: Pipelines are defined in code, enabling dyamic Dag generation and parameterization.
- Extensible: The Airflow framework includes a wide range of built-in operators and can be extended to fit your needs.
- Flexible: Airflow leverage the Jinga templating engine, allowing rich customizations.

### Dags 
