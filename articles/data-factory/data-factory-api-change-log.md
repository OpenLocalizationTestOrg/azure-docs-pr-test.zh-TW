---
title: "aaaData Factory-.NET 應用程式開發介面變更記錄檔 |Microsoft 文件"
description: "描述重大變更、 新增功能、 bug 修正等等...在 hello Azure Data Factory.NET API 的特定版本。"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 8208271b-7f4c-4214-b665-d2ff503c4470
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: spelluru
ms.openlocfilehash: 1d44b45c3dc8f9d483d1f1cef7068edacc610932
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---net-api-change-log"></a>Azure Data Factory - .NET API 變更記錄
本文章提供變更 tooAzure Data Factory SDK 中的特定版本的相關資訊。 您可以找到 hello 最新的 NuGet 套件的 Azure Data Factory[這裡](https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactories)

## <a name="version-4110"></a>版本 4.11.0
新增功能︰

* hello 下列的連結的服務類型已加入：
  * [OnPremisesMongoDbLinkedService](https://msdn.microsoft.com/library/mt765129.aspx)
  * [AmazonRedshiftLinkedService](https://msdn.microsoft.com/library/mt765121.aspx)
  * [AwsAccessKeyLinkedService](https://msdn.microsoft.com/library/mt765144.aspx)
* 已加入下列資料集類型的 hello:
  * [MongoDbCollectionDataset](https://msdn.microsoft.com/library/mt765145.aspx)
  * [AmazonS3Dataset](https://msdn.microsoft.com/library/mt765112.aspx)
* hello 下列複製的來源類型加入：
  * [MongoDbSource](https://msdn.microsoft.com/library/mt765123.aspx)

## <a name="version-4100"></a>版本 4.10.0
* 已加入 tooTextFormat hello 下列選擇性屬性：
  * [SkipLineCount](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.textformat.skiplinecount.aspx)
  * [FirstRowAsHeader](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.textformat.firstrowasheader.aspx)
  * [TreatEmptyAsNull](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.textformat.treatemptyasnull.aspx)
* hello 下列的連結的服務類型已加入：
  * [OnPremisesCassandraLinkedService](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.onpremisescassandralinkedservice.aspx)
  * [SalesforceLinkedService](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.salesforcelinkedservice.aspx)
* 已加入下列資料集類型的 hello:
  * [OnPremisesCassandraTableDataset](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.onpremisescassandratabledataset.aspx)
* hello 下列複製的來源類型加入：
  * [CassandraSource](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.cassandrasource.aspx)
* 新增[WebServiceInputs](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.azuremlbatchexecutionactivity.webserviceinputs.aspx)屬性 tooAzureMLBatchExecutionActivity
  * 啟用傳遞多個 web 服務輸入 tooan Azure 機器學習實驗

## <a name="version-491"></a>版本 4.9.1
### <a name="bug-fix"></a>錯誤修正
* 取代 [WebLinkedService](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.weblinkedservice.authenticationtype.aspx)的 WebApi 型驗證。

## <a name="version-490"></a>版本 4.9.0
### <a name="feature-additions"></a>新增功能
* 新增[EnableStaging](https://msdn.microsoft.com/library/mt767916.aspx)和[StagingSettings](https://msdn.microsoft.com/library/mt767918.aspx) tooCopyActivity 屬性。 請參閱[分段複製](data-factory-copy-activity-performance.md#staged-copy)如 hello 功能的詳細資訊。

### <a name="bug-fix"></a>錯誤修正
* 導入 [ActivityWindowOperationExtensions.List](https://msdn.microsoft.com/library/mt767915.aspx) 方法的多載，它會採用 [ActivityWindowsByActivityListParameters](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.activitywindowsbyactivitylistparameters.aspx) 執行個體。
* 將 [WriteBatchSize](https://msdn.microsoft.com/library/dn884293.aspx) 和 [WriteBatchTimeout](https://msdn.microsoft.com/library/dn884245.aspx) 標示為 CopySink 中的選擇性項目。

## <a name="version-480"></a>版本 4.8.0
### <a name="feature-additions"></a>新增功能
* 已新增下列選擇性屬性的 hello tooCopy 活動輸入 tooenable 微調複製的效能：
  * [ParallelCopies](https://msdn.microsoft.com/library/mt767910.aspx)
  * [CloudDataMovementUnits](https://msdn.microsoft.com/library/mt767912.aspx)

## <a name="version-470"></a>4.7.0 版
### <a name="feature-additions"></a>新增功能
* 加入新的 StorageFormat 類型[OrcFormat](https://msdn.microsoft.com/library/mt723391.aspx)輸入 toocopy 檔最佳化的資料列單欄式 (ORC) 格式。
* 新增[AllowPolyBase](https://msdn.microsoft.com/library/mt723396.aspx)和 PolyBaseSettings 屬性 tooSqlDWSink。
  * 可讓您 hello 使用 PolyBase toocopy 資料到 SQL 資料倉儲。

## <a name="version-461"></a>4.6.1 版
### <a name="bug-fixes"></a>錯誤修正
* 修正用於列出活動時段的 HTTP 要求。
  * 移除 hello 要求裝載的 hello 資源群組名稱和 hello data factory 名稱。

## <a name="version-460"></a>4.6.0 版
### <a name="feature-additions"></a>新增功能
* hello 下列屬性已新增過[PipelineProperties](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.pipelineproperties_properties.aspx):
  * [PipelineMode](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.pipelineproperties.pipelinemode.aspx)
  * [ExpirationTime](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.pipelineproperties.expirationtime.aspx)
  * [資料集](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.pipelineproperties.datasets.aspx)
* hello 下列屬性已新增過[PipelineRuntimeInfo](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.common.models.pipelineruntimeinfo.aspx):
  * [PipelineState](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.common.models.pipelineruntimeinfo.pipelinestate.aspx)
* 新增[StorageFormat](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.storageformat.aspx)類型[JsonFormat](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.jsonformat.aspx)輸入 toodefine 其資料是以 JSON 格式的資料集。

## <a name="version-450"></a>4.5.0 版
### <a name="feature-additions"></a>新增功能
* 加入了 [活動時段的清單作業](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.activitywindowoperationsextensions.aspx)。
  * 加入方法 tooretrieve 活動 windows hello 實體類型 （也就是資料處理站、 資料集、 管線和活動） 為基礎的篩選器。
* hello 下列的連結的服務類型已加入：
  * [ODataLinkedService](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.odatalinkedservice.aspx)、[WebLinkedService](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.weblinkedservice.aspx)
* 已加入下列資料集類型的 hello:
  * [ODataResourceDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.odataresourcedataset.aspx)、[WebTableDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.webtabledataset.aspx)
* hello 下列複製的來源類型加入：     
  * [WebSource](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.websource.aspx)

## <a name="version-440"></a>4.4.0 版
### <a name="feature-additions"></a>新增功能
* hello 下列的連結的服務類型已加入做為資料來源和接收複製活動：
  * [AzureStorageSasLinkedService](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.azurestoragesaslinkedservice.aspx)。 如需概念性資訊和範例，請參閱 [Azure 儲存體 SAS 連結服務](data-factory-azure-blob-connector.md#azure-storage-sas-linked-service) 。

## <a name="version-430"></a>4.3.0 版
### <a name="feature-additions"></a>新增功能
* 下列連結的服務類型樂園 hello 已加入做為複製活動的資料來源：
  * [HdfsLinkedService](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.hdfslinkedservice.aspx)。 如需概念性資訊和範例，請參閱 [使用 Data Factory 從 HDFS 移動資料](data-factory-hdfs-connector.md) 。
  * [OnPremisesOdbcLinkedService](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.onpremisesodbclinkedservice.aspx)。 如需概念性資訊和範例，請參閱 [使用 Azure Data Factory 從 ODBC 資料存放區移動資料](data-factory-odbc-connector.md) 。

## <a name="version-420"></a>4.2.0 版
### <a name="feature-additions"></a>新增功能
* 已新增下列新活動類型的 hello: [AzureMLUpdateResourceActivity](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuremlupdateresourceactivity.aspx)。 如需 hello 活動的詳細資訊，請參閱[使用更新的 Azure ML 模型 hello 更新資源活動](data-factory-azure-ml-batch-execution-activity.md)。
* 新的選擇性屬性[updateResourceEndpoint](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuremllinkedservice.updateresourceendpoint.aspx)已加入 toohello [AzureMLLinkedService 類別](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuremllinkedservice.aspx)。
* [LongRunningOperationInitialTimeout](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.datafactorymanagementclient.longrunningoperationinitialtimeout.aspx)和[LongRunningOperationRetryTimeout](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.datafactorymanagementclient.longrunningoperationretrytimeout.aspx)屬性已加入 toohello [DataFactoryManagementClient](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.datafactorymanagementclient.aspx)類別。
* 允許用戶端呼叫 toohello Data Factory 服務的 hello 逾時設定。

## <a name="version-410"></a>4.1.0 版
### <a name="feature-additions"></a>新增功能
* hello 下列的連結的服務類型已加入：
  * [AzureDataLakeStoreLinkedService](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx)
  * [AzureDataLakeAnalyticsLinkedService](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx)
* 已加入下列活動類型的 hello:
  * [DataLakeAnalyticsUSQLActivity](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.datalakeanalyticsusqlactivity.aspx)
* 已加入下列資料集類型的 hello:
  * [AzureDataLakeStoreDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestoredataset.aspx)
* hello 複製活動的下列來源和接收器類型已加入：
  * [AzureDataLakeStoreSource](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestoresource.aspx)
  * [AzureDataLakeStoreSink](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestoresink.aspx)

## <a name="version-401"></a>4.0.1 版
### <a name="breaking-changes"></a>重大變更
下列類別的 hello 已重新命名。 4.0.0 版之前，hello 新名稱會為 hello 原始類別名稱。

| 4.0.0 中的名稱 | 4.0.1 中的名稱 |
|:--- |:--- |
| AzureSqlDataWarehouseDataset |[AzureSqlDataWarehouseTableDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuresqldatawarehousetabledataset.aspx) |
| AzureSqlDataset |[AzureSqlTableDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuresqltabledataset.aspx) |
| AzureDataset |[AzureTableDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuretabledataset.aspx) |
| OracleDataset |[OracleTableDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.oracletabledataset.aspx) |
| RelationalDataset |[RelationalTableDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.relationaltabledataset.aspx) |
| SqlServerDataset |[SqlServerTableDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.sqlservertabledataset.aspx) |

## <a name="version-400"></a>4.0.0 版
### <a name="breaking-changes"></a>重大變更
* 下列類別/介面的 hello 已重新命名。

| 舊名稱 | 新名稱 |
|:--- |:--- |
| ITableOperations |[IDatasetOperations](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.idatasetoperations.aspx) |
| 資料表 |[Dataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.dataset.aspx) |
| TableProperties |[DatasetProperties](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.datasetproperties.aspx) |
| TableTypeProprerties |[DatasetTypeProperties](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.datasettypeproperties.aspx) |
| TableCreateOrUpdateParameters |[DatasetCreateOrUpdateParameters](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.datasetcreateorupdateparameters.aspx) |
| TableCreateOrUpdateResponse |[DatasetCreateOrUpdateResponse](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.datasetcreateorupdateresponse.aspx) |
| TableGetResponse |[DatasetGetResponse](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.datasetgetresponse.aspx) |
| TableListResponse |[DatasetListResponse](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.datasetlistresponse.aspx) |
| CreateOrUpdateWithRawJsonContentParameters |[DatasetCreateOrUpdateWithRawJsonContentParameters](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.datasetcreateorupdatewithrawjsoncontentparameters.aspx) |

* hello**清單**方法現在傳回分頁的結果。 如果 hello 回應包含非空白**NextLink**屬性，hello 用戶端應用程式需要 toocontinue 擷取 hello 下一個頁面上的所有網頁都傳回為止。  下列是一個範例：

    ```csharp
    PipelineListResponse response = client.Pipelines.List("ResourceGroupName", "DataFactoryName");
    var pipelines = new List<Pipeline>(response.Pipelines);

    string nextLink = response.NextLink;
    while (!string.IsNullOrEmpty(nextLink))
    {
        PipelineListResponse nextResponse = client.Pipelines.ListNext(nextLink);
        pipelines.AddRange(nextResponse.Pipelines);

        nextLink = nextResponse.NextLink;
    }
    ```
* **清單**管線 API 傳回僅 hello 管線，而不是完整詳細資料的摘要。 例如，管線摘要中的活動只包含名稱和類型。

### <a name="feature-additions"></a>新增功能
* hello [SqlDWSink](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.sqldwsink.aspx)類別支援兩個新屬性： **SliceIdentifierColumnName**和**SqlWriterCleanupScript**，toosupport 等冪複製 tooAzure SQL 資料倉儲。 請參閱 hello [Azure SQL 資料倉儲](data-factory-azure-sql-data-warehouse-connector.md)文件以取得有關這些屬性的詳細資料。
* 我們現在支援對 Azure SQL Database 和 Azure SQL 資料倉儲的來源執行預存程序，做為 hello 複製活動的一部分。 hello [SqlSource](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.sqlsource.aspx)和[SqlDWSource](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.sqldwsource.aspx)類別具有下列屬性的 hello: **SqlReaderStoredProcedureName**和**StoredProcedureParameters**. 請參閱 hello [Azure SQL Database](data-factory-azure-sql-connector.md#sqlsource)和[Azure SQL 資料倉儲](data-factory-azure-sql-data-warehouse-connector.md#sqldwsource)Azure.com 上的發行項，如需這些屬性的詳細資訊。  
