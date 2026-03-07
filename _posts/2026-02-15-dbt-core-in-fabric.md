---
layout: post
title: Running dbt Core in Microsoft Fabric
description: A guide to leveraging dbt Core for data transformations within Microsoft Fabric.
image: assets/images/laptop-data.jpg
---

In the rapidly evolving world of data analytics, Microsoft Fabric is emerging as a powerful all-in-one solution. For data transformation, while Fabric has its own tools, many data professionals are already proficient with `dbt` (data build tool). This post will guide you on how to run `dbt-core` with Microsoft Fabric's Synapse Data Warehouse.

### Why use dbt Core with Microsoft Fabric?

- **Leverage Existing Skills:** Many analytics engineers are already skilled in dbt. Using `dbt-core` allows them to be productive from day one in a Fabric environment.
- **Version Control and CI/CD:** `dbt` projects are just text files, which means they can be easily version controlled with Git. This enables robust CI/CD practices for your data transformation code.
- **Community and Package Ecosystem:** The `dbt` community is vast, and there are many pre-built packages that can be leveraged to speed up development.
- **Testing:** `dbt` has a built-in testing framework that allows you to define and run data quality tests easily.

### Setting up your environment

To get started, you'll need to have Python and `pip` installed. You will also need to install the `dbt-fabric` adapter.

```bash
pip install dbt-fabric
```

### Configuring your `profiles.yml`

The `profiles.yml` file contains the connection details for your data warehouse. For Microsoft Fabric, you will need to use the SQL connection string for your Synapse Data Warehouse. You can find this in the Fabric portal.

Here is an example of what your `profiles.yml` might look like:

```yaml
my_fabric_project:
  target: dev
  outputs:
    dev:
      type: fabric
      driver: 'ODBC Driver 18 for SQL Server'
      server: '<your-fabric-workspace>.datawarehouse.pbidedicated.windows.net'
      port: 1433
      database: '<your-database-name>'
      schema: 'dbo'
      authentication: 'CLI' # Or use 'service_principal' for CI/CD
      # For service principal authentication
      # client_id: '...'
      # client_secret: '...'
      # tenant_id: '...'
```

Make sure to replace the placeholder values with your actual connection details.

### Running your dbt project

Once your `profiles.yml` is set up, you can run your dbt project as you would with any other data warehouse.

```bash
dbt run
```

This command will compile your dbt models and execute them against your Fabric Synapse Data Warehouse.

### Conclusion

Running `dbt-core` in Microsoft Fabric is a great way to leverage the power of both tools. It allows you to use a familiar and powerful data transformation workflow within the modern and integrated environment of Microsoft Fabric. As Fabric continues to evolve, we expect the integration with dbt to become even more seamless.
