---
title: Ingest data into Azure Data Explorer using the ingestion wizard
description: Overview of ingesting (loading) data into Azure Data Explorer simply, using the ingestion wizard.
ms.reviewer: tzgitlin
ms.topic: how-to
ms.date: 09/05/2022
---

# What is the ingestion wizard?

The ingestion wizard makes the data ingestion process easy, fast, and intuitive. Using the ingestion wizard helps you ramp-up quickly to start ingesting data, creating database tables, mapping structures. Select data from different kinds of sources in different data formats, either as a one-time or continuous ingestion process.

The following features make the ingestion wizard so useful:

* Intuitive experience guided by the ingestion wizard
* Ingest data in a matter of minutes
* Ingest data from different kinds of sources: local file, blobs, and containers (up to 10,000 blobs)
* Ingest data in a variety of [formats](#file-formats)
* Ingest data into new or existing tables
* Table mapping and schema are suggested to you and easy to change
* Continue ingestion easily and quickly from a container with [Event Grid](./ingestion-wizard-new-table.md#create-continuous-ingestion)

The ingestion wizard is useful when ingesting data for the first time, or when your data's schema is unfamiliar to you.

## Prerequisites

* A Microsoft account or an Azure Active Directory user identity. An Azure subscription isn't required.
* Create [a cluster and database](create-cluster-database-portal.md).
* Sign in to the [Azure Data Explorer web UI](https://dataexplorer.azure.com/) and [add a connection to your cluster](web-query-data.md#add-clusters).

> [!NOTE]
> To enable access between a cluster and a storage account without public access (restricted to private endpoint/service endpoint), see [Create a Managed Private Endpoint](security-network-managed-private-endpoint-create.md).

## Access the ingestion wizard

The ingestion wizard guides you through the ingestion process.

* To access the wizard from the [Azure Data Explorer web UI](https://dataexplorer.azure.com/), use one of the following methods:
  * Select **Data** in the left pane. Within the **Data Management** page, select a type of ingestion and select **Ingest**.

      :::image type="content" source="media/ingest-data-wizard/select-data-pane.png" alt-text="Screenshot of options to ingest data from the data management window of the Azure Data Explorer web UI interface - Azure Data Explorer." lightbox="media/ingest-data-wizard/select-data-pane.png":::

  * Select **Query** in the left pane. Right-click the *database* or *table* and select **Ingest new data**.

      :::image type="content" source="media/ingest-data-wizard/ingest-new-data-database-menu.png" alt-text="Screenshot of selection of the ingestion wizard in the Azure Data Explorer web UI.":::

* To access the ingestion wizard from the **Azure Data Explorer** home screen in your cluster, complete the first two steps ([cluster creation and database creation](#prerequisites)) and then select **Ingest**.

    :::image type="content" source="media/ingest-data-wizard/cluster-ingestion.png" alt-text="Ingest new data from welcome to Azure Data Explorer.":::

* To access the wizard from the Azure portal, select **Query** from the left menu, right-click on the **database** or **table**, and select **Ingest new data**.

    :::image type="content" source="media/ingest-data-wizard/ingest-from-portal.png" alt-text="Access the ingestion wizard from Azure portal.":::

## Ingestion wizard

> [!NOTE]
> This section describes the ingestion wizard in general. The options you select depend on what data format you are ingesting, what kind of data source you are ingesting from, and whether you are ingesting into a new or existing table.
>
> For sample scenarios, see:
>
> * Ingest into [a new table from a container in CSV format](./ingestion-wizard-new-table.md)
> * Ingest into an [existing table from a local file in JSON format](./ingestion-wizard-existing-table.md)

The wizard guides you through the following options:

* Ingest into an [existing table](./ingestion-wizard-existing-table.md)
* Ingest into [a new table](./ingestion-wizard-new-table.md)
* Ingest data from:
  * Blob storage: up to 10 blobs
  * [A local file](./ingestion-wizard-existing-table.md): up to 10 files
  * [A container](./ingestion-wizard-new-table.md) (blob container, ADLS Gen1 container, ADLS Gen2 container)

### Schema mapping

The service automatically generates schema and ingestion properties, which you can change. You can use an existing mapping structure or create a new one, depending on if you're ingesting to a new or existing table.

In the **Schema** tab, do the following actions:

* Confirm the autogenerated compression type.
* Choose the [format of your data](#file-formats). Different formats will allow you to make further changes.
* Change mapping in the [Editor window](#editor-window).

#### File formats

The ingestion wizard supports ingesting from source data in all [data formats supported by Azure Data Explorer for ingestion](ingestion-supported-formats.md).

### Editor window

In the **Editor** window of the **Schema** tab, you can adjust data table columns as necessary.

[!INCLUDE [data-explorer-ingestion-wizard-column-table](includes/data-explorer-ingestion-wizard-column-table.md)]

>[!NOTE]
> At any time, you can open the [command editor](./ingestion-wizard-new-table.md#command-editor) above the **Editor** pane. In the command editor, you can view and copy the automatic commands generated from your inputs.

#### Mapping transformations

Some data format mappings (Parquet, JSON, and Avro) support simple ingest-time transformations. To apply mapping transformations, create or update a column in the [Editor window](#editor-window).

Mapping transformations can be performed on a column of **Type** string or datetime, with the **Source** having data type int or long. Supported mapping transformations are:

* DateTimeFromUnixSeconds
* DateTimeFromUnixMilliseconds
* DateTimeFromUnixMicroseconds
* DateTimeFromUnixNanoseconds

### Data ingestion

Once you have completed schema mapping and column manipulations, the ingestion wizard will start the data ingestion process.

* When ingesting data from **non-container** sources, the ingestion will take immediate effect.

* If your data source is a **container**:

  * Azure Data Explorer's [batching policy](kusto/management/batchingpolicy.md) will aggregate your data.
  * After ingestion, you can download the ingestion report and review the performance of each blob that was addressed.
  * You can select **Create continuous ingestion** and set up [continuous ingestion using Event Grid](./ingestion-wizard-new-table.md#create-continuous-ingestion).

### Initial data exploration

After ingestion, the wizard gives you options to use **[Quick commands](./ingestion-wizard-existing-table.md#explore-quick-queries-and-tools)** for initial exploration of your data.

## Next steps

* [Ingest JSON data from a local file to an existing table in Azure Data Explorer using the ingestion wizard](./ingestion-wizard-existing-table.md)
* [Ingest data from a container or Azure Data Lake Storage into Azure Data Explorer](./ingestion-wizard-new-table.md)
* [Query data in Azure Data Explorer web UI](web-query-data.md)
* [Write queries for Azure Data Explorer using Kusto Query Language](write-queries.md)