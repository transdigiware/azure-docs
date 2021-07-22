---
title: What's New in Azure Data Factory 
description: This What's New page highlights new features and improvements for Azure Data Factory.
author: pennyzhou-msft
ms.author: xupzhou
ms.reviewer: xupzhou
ms.service: data-factory
ms.topic: overview
ms.date: 07/14/2021
---

# What's New in Azure Data Factory

Azure Data Factory receives improvements on an ongoing basis. To stay up to date with the most recent developments, this article provides you with information about:

- The latest releases
- Known issues
- Bug fixes
- Deprecated functionality
- Plans for changes

This page will be updated monthly, so revisit it regularly. 

## June 2021
<br>
<table>
<tr><td><b>Service Category</b></td><td><b>Service improvements</b></td><td><b>Details</b></td></tr>
<tr><td rowspan=4 valign="middle"><b>Data Movement</b></td><td>New user experience with Azure Data Factory Copy Data Tool</td><td>Redesigned Copy Data Tool is now available with improved data ingestion experience.<br><a href="https://techcommunity.microsoft.com/t5/azure-data-factory/a-re-designed-copy-data-tool-experience/ba-p/2380634">Learn more</a></td></tr>
<tr><td>MongoDB and MongoDB Atlas are Supported as both Source and Sink</td><td>This improvement supports copying data between any supported data store and MongoDB or MongoDB Atlas database.<br><a href="https://techcommunity.microsoft.com/t5/azure-data-factory/new-connectors-available-in-adf-mongodb-and-mongodb-atlas-are/ba-p/2441482">Learn more</a></td></tr>
<tr><td>Always Encrypted is supported for Azure SQL Database, Azure SQL Managed Instance, and SQL Server connectors as both source and sink</td><td>Always Encrypted is available in Azure Data Factory for Azure SQL Database, Azure SQL Managed Instance, and SQL Server connectors for copy activity.<br><a href="https://techcommunity.microsoft.com/t5/azure-data-factory/azure-data-factory-copy-now-supports-always-encrypted-for-both/ba-p/2461346">Learn more</a></td></tr>
<tr><td>Setting custom metadata is supported in copy activity when sinking to ADLS Gen2 or Azure Blob</td><td>When writing to ADLS Gen2 or Azure Blob, copy activity supports setting custom metadata or storage of the source file's last modified info as metadata.<br><a href="https://techcommunity.microsoft.com/t5/azure-data-factory/support-setting-custom-metadata-when-writing-to-blob-adls-gen2/ba-p/2545506#M490">Learn more</a></td></tr>
<tr><td rowspan=4 valign="middle"><b>Data Flow</b></td><td>SQL Server is now supported as a source and sink in data flows</td><td>SQL Server is now supported as a source and sink in data flows. Follow the link for instructions on how to configure your networking using the Azure Integration Runtime managed VNET feature to talk to your SQL Server on-premise and cloud VM-based instances.<br><a href="https://techcommunity.microsoft.com/t5/azure-data-factory/new-data-flow-connector-sql-server-as-source-and-sink/ba-p/2406213">Learn more</a></td></tr>
<tr><td>Dataflow Cluster quick reuse is now enabled by default for all new Azure Integration Runtimes</td><td>ADF is happy to announce the general availability of the popular data flow quick start-up reuse feature. All new Azure Integration Runtimes will now have quick reuse enabled by default.<br><a href="https://techcommunity.microsoft.com/t5/azure-data-factory/how-to-startup-your-data-flows-execution-in-less-than-5-seconds/ba-p/2267365">Learn more</a></td></tr>
<tr><td>Power Query activity in ADF public preview</td><td>You can now build complex field mappings to your Power Query sink using Azure Data Factory data wrangling. The sink is now configured in the pipeline in the Power Query (Preview) activity to accommodate this update.<br><a href="wrangling-tutorial.md">Learn more</a></td></tr>
<tr><td>Updated data flows monitoring UI in Azure Data Factory</td><td>Azure Data Factory has a new update for the monitoring UI to make it easier to view your data flow ETL job executions and quickly identify areas for performance tuning.<br><a href="https://techcommunity.microsoft.com/t5/azure-data-factory/updated-data-flows-monitoring-ui-in-adf-amp-synapse/ba-p/2432199">Learn more</a></td></tr>
<tr><td><b>SQL Server Integration Services (SSIS)</b></td><td>Run any SQL anywhere in 3 simple steps with SSIS in Azure Data Factory</td><td>This post provides 3 simple steps to run any SQL statements/scripts anywhere with SSIS in Azure Data Factory.<ol><li>Prepare your Self-Hosted Integration Runtime/SSIS Integration Runtime.</li><li>Prepare an Execute SSIS Package activity in Azure Data Factory pipeline.</li><li>Run the Execute SSIS Package activity on your Self-Hosted Integration Runtime/SSIS Integration Runtime.</li></ol><a href="https://techcommunity.microsoft.com/t5/sql-server-integration-services/run-any-sql-anywhere-in-3-easy-steps-with-ssis-in-azure-data/ba-p/2457244">Learn more</a></td></tr>
</table>

## More information

- [Blog - Azure Data Factory](https://techcommunity.microsoft.com/t5/azure-data-factory/bg-p/AzureDataFactoryBlog)
- [Stack Overflow forum](https://stackoverflow.com/questions/tagged/azure-data-factory)
- [Twitter](https://twitter.com/AzDataFactory?ref_src=twsrc%5Egoogle%7Ctwcamp%5Eserp%7Ctwgr%5Eauthor)
- [Videos](https://www.youtube.com/channel/UC2S0k7NeLcEm5_IhHUwpN0g/featured)





