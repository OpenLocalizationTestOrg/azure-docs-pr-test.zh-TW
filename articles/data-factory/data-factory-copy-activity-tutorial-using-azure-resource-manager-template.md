---
title: "教學課程：使用 Resource Manager 範本建立管線 | Microsoft Docs"
description: "在本教學課程中，您會使用 Azure Resource Manager 範本建立 Azure Data Factory 管線。 這個管線會將資料從 Azure blob 儲存體 tooan Azure SQL database。"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 1274e11a-e004-4df5-af07-850b2de7c15e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 1c7567cb0423f7ce3e0cab2d77a4d861b70eb56b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-use-azure-resource-manager-template-toocreate-a-data-factory-pipeline-toocopy-data"></a>教學課程： 使用 Azure Resource Manager 範本 toocreate Data Factory 管線 toocopy 資料 
> [!div class="op_single_selector"]
> * [概觀和必要條件](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [複製精靈](data-factory-copy-data-wizard-tutorial.md)
> * [Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)
> * [Azure Resource Manager 範本](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [REST API](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [.NET API](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

本教學課程示範如何 toouse Azure Resource Manager 範本 toocreate Azure data factory。 在此教學課程中的 hello 資料管線會將資料從來源資料存放區 tooa 目的地資料存放區。 它不會轉換輸入的資料 tooproduce 輸出資料。 如需如何使用 Azure Data Factory，tootransform 資料，請參閱[教學課程： 建立使用 Hadoop 叢集管線 tootransform 資料](data-factory-build-your-first-pipeline.md)。

在本教學課程中，您可以建立包含一個活動的管線：複製活動。 hello 複製活動會將資料從支援的資料存放區 tooa 支援的接收資料存放區。 如需作為來源和接收區支援的資料存放區清單，請參閱[支援的資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)。 hello 活動被提供安全、 可靠且可擴充的方式的各種資料存放區之間的資料可以複製的全域可用服務。 如需 hello 複製活動的詳細資訊，請參閱[資料移動活動](data-factory-data-movement-activities.md)。

一個管線中可以有多個活動。 此外，您可以藉由設定 hello 輸出資料集的一個活動 hello 的輸入資料集的 hello 其他活動鏈結 （執行一個活動執行另一個之後） 的兩個活動。 如需詳細資訊，請參閱[管線中的多個活動](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline)。 

> [!NOTE] 
> 在此教學課程中的 hello 資料管線會將資料從來源資料存放區 tooa 目的地資料存放區。 如需如何使用 Azure Data Factory，tootransform 資料，請參閱[教學課程： 建立使用 Hadoop 叢集管線 tootransform 資料](data-factory-build-your-first-pipeline.md)。 

## <a name="prerequisites"></a>必要條件
* 透過移[教學課程的概觀和必要條件](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)和完整 hello**必要條件**步驟。
* 遵循指示[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)文章 tooinstall 最新版的 Azure PowerShell 在您的電腦上。 在本教學課程中，您可以使用 PowerShell toodeploy Data Factory 實體。 
* （選擇性）請參閱[撰寫 Azure 資源管理員範本](../azure-resource-manager/resource-group-authoring-templates.md)toolearn 關於 Azure Resource Manager 範本。

## <a name="in-this-tutorial"></a>本教學課程內容
在本教學課程中，您可以建立 data factory 以下列 Data Factory 實體的 hello:

| 實體 | 說明 |
| --- | --- |
| Azure 儲存體連結服務 |連結您的 Azure 儲存體帳戶 toohello data factory。 Azure 儲存體是 hello 來源資料存放區和 Azure SQL database 是 hello 教學課程中的 hello 複製活動的 hello 接收資料存放區。 它會指定包含 hello hello 複製活動的輸入的資料的 hello 儲存體帳戶。 |
| Azure SQL Database 的連結服務 |連結您的 Azure SQL database toohello data factory。 它會指定保留 hello hello 複製活動的輸出資料的 hello Azure SQL database。 |
| Azure Blob 輸入資料集 |是指 toohello Azure 儲存體連結服務。 hello 連結的服務是指 tooan Azure 儲存體帳戶和 hello Azure Blob 資料集指定 hello 儲存體保存 hello 輸入的資料中的 hello 容器、 資料夾和檔案名稱。 |
| Azure SQL 輸出資料集 |是指 toohello Azure SQL 連結服務。 hello Azure SQL 連結服務參考 tooan Azure SQL server 和 hello Azure SQL 資料集會指定 hello 保存 hello 輸出資料的 hello 資料表名稱。 |
| Data Pipeline |hello 管線有一個活動的輸入會做為輸入 hello Azure blob 資料集的複本與 hello Azure SQL 資料集做為輸出。 hello 複製活動會從 Azure blob tooa hello Azure SQL database 中的資料表複製資料。 |

資料處理站可以有一或多個管線。 其中的管線可以有一或多個活動。 兩種活動類型︰[資料移動活動](data-factory-data-movement-activities.md)和[資料轉換活動](data-factory-data-transformation-activities.md)。 在本教學課程中，您可以使用一個活動建立管線 (複製活動)。

![複製 Azure Blob tooAzure SQL 資料庫](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/CopyBlob2SqlDiagram.png) 

hello 下節提供 hello 完成資源管理員範本，您可以快速地執行透過 hello 教學課程和測試 hello 範本定義 Data Factory 實體。 toounderstand 如何定義每個 Data Factory 實體，請參閱[hello 範本中的 Data Factory 實體](#data-factory-entities-in-the-template)> 一節。

## <a name="data-factory-json-template"></a>Data Factory JSON 範本
是用於定義 data factory hello 最上層資源管理員範本： 

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": { ...
    },
    "variables": { ...
    },
    "resources": [
        {
            "name": "[parameters('dataFactoryName')]",
            "apiVersion": "[variables('apiVersion')]",
            "type": "Microsoft.DataFactory/datafactories",
            "location": "westus",
            "resources": [
                { ... },
                { ... },
                { ... },
                { ... }
            ]
        }
    ]
}
```
建立名為的 JSON 檔案**ADFCopyTutorialARM.json**中**C:\ADFGetStarted**資料夾以 hello 下列內容：

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": {
      "storageAccountName": { "type": "string", "metadata": { "description": "Name of hello Azure storage account that contains hello data toobe copied." } },
      "storageAccountKey": { "type": "securestring", "metadata": { "description": "Key for hello Azure storage account." } },
      "sourceBlobContainer": { "type": "string", "metadata": { "description": "Name of hello blob container in hello Azure Storage account." } },
      "sourceBlobName": { "type": "string", "metadata": { "description": "Name of hello blob in hello container that has hello data toobe copied tooAzure SQL Database table" } },
      "sqlServerName": { "type": "string", "metadata": { "description": "Name of hello Azure SQL Server that will hold hello output/copied data." } },
      "databaseName": { "type": "string", "metadata": { "description": "Name of hello Azure SQL Database in hello Azure SQL server." } },
      "sqlServerUserName": { "type": "string", "metadata": { "description": "Name of hello user that has access toohello Azure SQL server." } },
      "sqlServerPassword": { "type": "securestring", "metadata": { "description": "Password for hello user." } },
      "targetSQLTable": { "type": "string", "metadata": { "description": "Table in hello Azure SQL Database that will hold hello copied data." } 
      } 
    },
    "variables": {
      "dataFactoryName": "[concat('AzureBlobToAzureSQLDatabaseDF', uniqueString(resourceGroup().id))]",
      "azureSqlLinkedServiceName": "AzureSqlLinkedService",
      "azureStorageLinkedServiceName": "AzureStorageLinkedService",
      "blobInputDatasetName": "BlobInputDataset",
      "sqlOutputDatasetName": "SQLOutputDataset",
      "pipelineName": "Blob2SQLPipeline"
    },
    "resources": [
      {
        "name": "[variables('dataFactoryName')]",
        "apiVersion": "2015-10-01",
        "type": "Microsoft.DataFactory/datafactories",
        "location": "West US",
        "resources": [
          {
            "type": "linkedservices",
            "name": "[variables('azureStorageLinkedServiceName')]",
            "dependsOn": [
              "[variables('dataFactoryName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
              "type": "AzureStorage",
              "description": "Azure Storage linked service",
              "typeProperties": {
                "connectionString": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('storageAccountName'),';AccountKey=',parameters('storageAccountKey'))]"
              }
            }
          },
          {
            "type": "linkedservices",
            "name": "[variables('azureSqlLinkedServiceName')]",
            "dependsOn": [
              "[variables('dataFactoryName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
              "type": "AzureSqlDatabase",
              "description": "Azure SQL linked service",
              "typeProperties": {
                "connectionString": "[concat('Server=tcp:',parameters('sqlServerName'),'.database.windows.net,1433;Database=', parameters('databaseName'), ';User ID=',parameters('sqlServerUserName'),';Password=',parameters('sqlServerPassword'),';Trusted_Connection=False;Encrypt=True;Connection Timeout=30')]"
              }
            }
          },
          {
            "type": "datasets",
            "name": "[variables('blobInputDatasetName')]",
            "dependsOn": [
              "[variables('dataFactoryName')]",
              "[variables('azureStorageLinkedServiceName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
              "type": "AzureBlob",
              "linkedServiceName": "[variables('azureStorageLinkedServiceName')]",
              "structure": [
                {
                  "name": "Column0",
                  "type": "String"
                },
                {
                  "name": "Column1",
                  "type": "String"
                }
              ],
              "typeProperties": {
                "folderPath": "[concat(parameters('sourceBlobContainer'), '/')]",
                "fileName": "[parameters('sourceBlobName')]",
                "format": {
                  "type": "TextFormat",
                  "columnDelimiter": ","
                }
              },
              "availability": {
                "frequency": "Hour",
                "interval": 1
              },
              "external": true
            }
          },
          {
            "type": "datasets",
            "name": "[variables('sqlOutputDatasetName')]",
            "dependsOn": [
              "[variables('dataFactoryName')]",
              "[variables('azureSqlLinkedServiceName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
              "type": "AzureSqlTable",
              "linkedServiceName": "[variables('azureSqlLinkedServiceName')]",
              "structure": [
                {
                  "name": "FirstName",
                  "type": "String"
                },
                {
                  "name": "LastName",
                  "type": "String"
                }
              ],
              "typeProperties": {
                "tableName": "[parameters('targetSQLTable')]"
              },
              "availability": {
                "frequency": "Hour",
                "interval": 1
              }
            }
          },
          {
            "type": "datapipelines",
            "name": "[variables('pipelineName')]",
            "dependsOn": [
              "[variables('dataFactoryName')]",
              "[variables('azureStorageLinkedServiceName')]",
              "[variables('azureSqlLinkedServiceName')]",
              "[variables('blobInputDatasetName')]",
              "[variables('sqlOutputDatasetName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
              "activities": [
                {
                  "name": "CopyFromAzureBlobToAzureSQL",
                  "description": "Copy data frm Azure blob tooAzure SQL",
                  "type": "Copy",
                  "inputs": [
                    {
                      "name": "[variables('blobInputDatasetName')]"
                    }
                  ],
                  "outputs": [
                    {
                      "name": "[variables('sqlOutputDatasetName')]"
                    }
                  ],
                  "typeProperties": {
                    "source": {
                      "type": "BlobSource"
                    },
                    "sink": {
                      "type": "SqlSink",
                      "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM {0}', 'emp')"
                    },
                    "translator": {
                      "type": "TabularTranslator",
                      "columnMappings": "Column0:FirstName,Column1:LastName"
                    }
                  },
                  "Policy": {
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 3,
                    "timeout": "01:00:00"
                  }
                }
              ],
              "start": "2017-05-11T00:00:00Z",
              "end": "2017-05-12T00:00:00Z"
            }
          }
        ]
      }
    ]
  }
```

## <a name="parameters-json"></a>參數 JSON
建立名為的 JSON 檔案**ADFCopyTutorialARM Parameters.json**包含 hello Azure Resource Manager 範本的參數。 

> [!IMPORTANT]
> 針對此參數檔案中的 storageAccountName 和 storageAccountKey 參數指定您 Azure 儲存體帳戶的名稱和金鑰。  
> 
> 針對 sqlServerName、databaseName、sqlServerUserName 和 sqlServerPassword 參數指定 Azure SQL 伺服器、資料庫、使用者和密碼。  

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": { 
        "storageAccountName": { "value": "<Name of hello Azure storage account>"    },
        "storageAccountKey": {
            "value": "<Key for hello Azure storage account>"
        },
        "sourceBlobContainer": { "value": "adftutorial" },
        "sourceBlobName": { "value": "emp.txt" },
        "sqlServerName": { "value": "<Name of hello Azure SQL server>" },
        "databaseName": { "value": "<Name of hello Azure SQL database>" },
        "sqlServerUserName": { "value": "<Name of hello user who has access toohello Azure SQL database>" },
        "sqlServerPassword": { "value": "<password for hello user>" },
        "targetSQLTable": { "value": "emp" }
    }
}
```

> [!IMPORTANT]
> 您可能需要進行開發，個別參數的 JSON 檔案測試，而且您可以搭配使用的實際執行環境的 hello 相同資料 Factory JSON 範本。 使用 Power Shell 指令碼，您可以在這些環境中自動部署 Data Factory 實體。  
> 
> 

## <a name="create-data-factory"></a>建立 Data Factory
1. 啟動**Azure PowerShell**和 hello 執行下列命令：
   * 執行下列命令的 hello 並輸入 hello 使用者名稱和密碼，您會使用 toosign toohello Azure 入口網站中。
   
    ```PowerShell
    Login-AzureRmAccount    
    ```  
   * 執行下列命令 tooview hello 這個帳戶的所有 hello 訂用帳戶。
   
    ```PowerShell
    Get-AzureRmSubscription
    ```   
   * 執行下列命令 tooselect hello 訂用帳戶，您想要使用 toowork hello。
    
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```    
2. 執行下列命令使用您在步驟 1 中建立的 hello Resource Manager 範本的 toodeploy Data Factory 實體的 hello。

    ```PowerShell   
    New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile C:\ADFGetStarted\ADFCopyTutorialARM.json -TemplateParameterFile C:\ADFGetStarted\ADFCopyTutorialARM-Parameters.json
    ```

## <a name="monitor-pipeline"></a>監視管線

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)使用您的 Azure 帳戶。
2. 按一下**Data factory** hello 左邊功能表 （或） 上按一下**更多服務**按一下**Data factory**下**智慧 + 分析**類別目錄。
   
    ![Data Factory 功能表](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/data-factories-menu.png)
3. 在 hello **Data factory**頁面、 搜尋和尋找您的 data factory (AzureBlobToAzureSQLDatabaseDF)。 
   
    ![搜尋 Data Factory](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/search-for-data-factory.png)  
4. 按一下您的 Azure Data Factory。 您看到 hello 首頁 hello data factory。
   
    ![Data Factory 首頁](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/data-factory-home-page.png)  
6. 請依照下列指示從[監視資料集和管線](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline)toomonitor hello 管線和資料集已建立本教學課程中。 Visual Studio 目前不支援監視 Data Factory 管線。
7. 配量處於 hello**準備**狀態，請確認 hello 資料複製的 toohello **emp** hello Azure SQL database 中的資料表。


如需有關如何 toouse Azure 入口網站的刀鋒 toomonitor 管線和資料集您已建立本教學課程中的詳細資訊，請參閱[監視資料集和管線](data-factory-monitor-manage-pipelines.md)。

如需有關如何 toouse hello 監視和管理應用程式 toomonitor 資料管線的詳細資訊，請參閱[監視和管理使用監視應用程式的 Azure Data Factory 管線](data-factory-monitor-manage-app.md)。

## <a name="data-factory-entities-in-hello-template"></a>Hello 範本中的 data Factory 實體
### <a name="define-data-factory"></a>定義資料處理站
Hello 下列範例所示，您可以定義在 hello Resource Manager 範本中的 data factory:  

```json
"resources": [
{
    "name": "[variables('dataFactoryName')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "West US"
}
```

hello dataFactoryName 定義為： 

```json
"dataFactoryName": "[concat('AzureBlobToAzureSQLDatabaseDF', uniqueString(resourceGroup().id))]"
```

它是唯一的字串 hello 資源群組 id。  

### <a name="defining-data-factory-entities"></a>定義 Data Factory 實體
hello 下列 Data Factory 實體範本中所定義 hello JSON: 

1. [Azure 儲存體連結服務](#azure-storage-linked-service)
2. [Azure SQL 連結服務](#azure-sql-database-linked-service)
3. [Azure blob 資料集](#azure-blob-dataset)
4. [Azure SQL 資料集](#azure-sql-dataset)
5. [具有複製活動的管線](#data-pipeline)

#### <a name="azure-storage-linked-service"></a>Azure 儲存體連結服務
hello AzureStorageLinkedService 連結您的 Azure 儲存體帳戶 toohello data factory。 您在建立容器，並在上傳資料 toothis 儲存體帳戶的[必要條件](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。 您可以在此區段中指定 hello 名稱和您的 Azure 儲存體帳戶金鑰。 請參閱[Azure 儲存體連結服務](data-factory-azure-blob-connector.md#azure-storage-linked-service)如需詳細資訊 JSON 屬性使用 toodefine Azure 儲存體連結服務。 

```json
{
    "type": "linkedservices",
    "name": "[variables('azureStorageLinkedServiceName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
        "type": "AzureStorage",
        "description": "Azure Storage linked service",
        "typeProperties": {
            "connectionString": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('storageAccountName'),';AccountKey=',parameters('storageAccountKey'))]"
        }
    }
}
```

hello connectionString 使用 hello storageAccountName 及 storageAccountKey 參數。 hello 使用組態檔傳遞這些參數的值。 hello 定義也會使用變數： azureStroageLinkedService 和 dataFactoryName hello 範本中定義。 

#### <a name="azure-sql-database-linked-service"></a>Azure SQL Database 的連結服務
AzureSqlLinkedService 連結您的 Azure SQL database toohello data factory。 複製 hello blob 儲存體中的 hello 資料會儲存在資料庫中。 在此資料庫中建立 hello emp 資料表的一部分[必要條件](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。 您可以在此區段中指定 hello Azure SQL server 名稱、 資料庫名稱、 使用者名稱和使用者密碼。 請參閱[Azure SQL 連結服務](data-factory-azure-sql-connector.md#linked-service-properties)如需詳細資訊 JSON 屬性使用 toodefine Azure SQL 連結服務。  

```json
{
    "type": "linkedservices",
    "name": "[variables('azureSqlLinkedServiceName')]",
    "dependsOn": [
      "[variables('dataFactoryName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
          "type": "AzureSqlDatabase",
          "description": "Azure SQL linked service",
          "typeProperties": {
            "connectionString": "[concat('Server=tcp:',parameters('sqlServerName'),'.database.windows.net,1433;Database=', parameters('databaseName'), ';User ID=',parameters('sqlServerUserName'),';Password=',parameters('sqlServerPassword'),';Trusted_Connection=False;Encrypt=True;Connection Timeout=30')]"
          }
    }
}
```

hello connectionString 使用 sqlServerName、 databaseName、 sqlServerUserName 和其值使用組態檔傳遞 sqlServerPassword 參數。 hello 定義也會使用 hello hello 範本中的下列變數： azureSqlLinkedServiceName，dataFactoryName。

#### <a name="azure-blob-dataset"></a>Azure Blob 資料集
hello Azure 儲存體連結服務指定 Data Factory 服務會使用在執行的階段 tooconnect tooyour Azure 儲存體帳戶的 hello 連接字串。 在 Azure blob 資料集定義中，您可以指定 blob 容器、 資料夾和檔案，其中包含 hello 輸入的資料的名稱。 請參閱[Azure Blob 資料集屬性](data-factory-azure-blob-connector.md#dataset-properties)如需詳細資訊 JSON 屬性使用 toodefine Azure Blob 資料集。 

```json
{
    "type": "datasets",
    "name": "[variables('blobInputDatasetName')]",
    "dependsOn": [
      "[variables('dataFactoryName')]",
      "[variables('azureStorageLinkedServiceName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
        "type": "AzureBlob",
          "linkedServiceName": "[variables('azureStorageLinkedServiceName')]",
        "structure": [
        {
              "name": "Column0",
              "type": "String"
        },
        {
              "name": "Column1",
              "type": "String"
        }
          ],
          "typeProperties": {
            "folderPath": "[concat(parameters('sourceBlobContainer'), '/')]",
            "fileName": "[parameters('sourceBlobName')]",
            "format": {
                  "type": "TextFormat",
                  "columnDelimiter": ","
            }
          },
          "availability": {
            "frequency": "Hour",
            "interval": 1
          },
          "external": true
    }
}
```

#### <a name="azure-sql-dataset"></a>Azure SQL 資料集
您擁有 hello Azure Blob 儲存體的 hello 複製資料的 hello Azure SQL database 中指定 hello hello 資料表名稱。 請參閱[Azure SQL 資料集屬性](data-factory-azure-sql-connector.md#dataset-properties)如需詳細資訊 JSON 屬性使用 toodefine Azure SQL 資料集。 

```json
{
    "type": "datasets",
    "name": "[variables('sqlOutputDatasetName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]",
          "[variables('azureSqlLinkedServiceName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
          "type": "AzureSqlTable",
          "linkedServiceName": "[variables('azureSqlLinkedServiceName')]",
          "structure": [
        {
              "name": "FirstName",
              "type": "String"
        },
        {
              "name": "LastName",
              "type": "String"
        }
          ],
          "typeProperties": {
            "tableName": "[parameters('targetSQLTable')]"
          },
          "availability": {
            "frequency": "Hour",
            "interval": 1
          }
    }
}
```

#### <a name="data-pipeline"></a>Data Pipeline
您定義將資料從 hello Azure blob 資料集 toohello Azure SQL 資料集的管線。 請參閱[管線 JSON](data-factory-create-pipelines.md#pipeline-json)如需 JSON 用項目 toodefine 管線，以在此範例的描述。 

```json
{
    "type": "datapipelines",
    "name": "[variables('pipelineName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]",
          "[variables('azureStorageLinkedServiceName')]",
          "[variables('azureSqlLinkedServiceName')]",
          "[variables('blobInputDatasetName')]",
          "[variables('sqlOutputDatasetName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
          "activities": [
        {
              "name": "CopyFromAzureBlobToAzureSQL",
              "description": "Copy data frm Azure blob tooAzure SQL",
              "type": "Copy",
              "inputs": [
            {
                  "name": "[variables('blobInputDatasetName')]"
            }
              ],
              "outputs": [
            {
                  "name": "[variables('sqlOutputDatasetName')]"
            }
              ],
              "typeProperties": {
                "source": {
                      "type": "BlobSource"
                },
                "sink": {
                      "type": "SqlSink",
                      "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM {0}', 'emp')"
                },
                "translator": {
                      "type": "TabularTranslator",
                      "columnMappings": "Column0:FirstName,Column1:LastName"
                }
              },
              "Policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 3,
                "timeout": "01:00:00"
              }
        }
          ],
          "start": "2017-05-11T00:00:00Z",
          "end": "2017-05-12T00:00:00Z"
    }
}
```

## <a name="reuse-hello-template"></a>重複使用 hello 範本
在 hello 教學課程中，您可以建立 Data Factory 實體和傳遞的參數值的範本定義的範本。 hello 管線會將資料從 Azure 儲存體帳戶 tooan Azure SQL database 透過參數所指定。 toouse hello 相同範本 toodeploy Data Factory 實體 toodifferent 環境，您建立參數檔案的每個環境，並部署 toothat 環境時，請使用它。     

範例：  

```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Dev.json
```
```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Test.json
```
```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Production.json
```

請注意，第一個命令會使用參數的 hello hello 開發環境的 hello 測試環境中，第二個檔案，與 hello hello 的生產環境的第三個。  

您也可以重複使用 hello 範本 tooperform 重複的工作。 比方說，您需要 toocreate 許多 data factory，其中包含一個或多個實作的管線 hello 相同邏輯，但每個 data factory 會使用不同的 SQL 資料庫和儲存體帳戶。 在此案例中，您可以使用 hello 相同的範本在 hello 與不同的參數相同的環境 （開發、 測試或生產） 檔案 toocreate data factory。   

## <a name="next-steps"></a>後續步驟
在本教學課程中，您可使用 Azure Blob 儲存體作為來源資料存放區以及使用 Azure SQL Database 作為複製作業的目的地資料存放區。 hello 下表提供 hello 複製活動支援做為來源和目的地資料存放區的清單： 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

關於如何 toocopy 資料，從資料存放區，toolearn 按一下 hello 連結 hello hello 資料表中的資料存放區。
