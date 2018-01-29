---
title: "Azure Data Factory 支援的計算環境 | Microsoft Docs"
description: "了解您可以在 Azure Data Factory 管線中 (如 Azure HDInsight) 用來轉換/處理資料的計算環境。"
services: data-factory
documentationcenter: 
author: shengcmsft
manager: jhubbard
editor: spelluru
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.topic: article
ms.date: 01/10/2018
ms.author: shengc
ms.openlocfilehash: f242a8a15334818d83651cf0af55e8ec39bce212
ms.sourcegitcommit: 9cc3d9b9c36e4c973dd9c9028361af1ec5d29910
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/23/2018
---
# <a name="compute-environments-supported-by-azure-data-factory"></a>Azure Data Factory 支援的計算環境
本文說明您可用來處理或轉換資料的各種計算環境。 其中還提供在設定將這些計算環境連結至 Azure Data Factory 的連結服務時，Data Factory 所支援的不同組態 (隨選與自備) 的詳細資料。

下表列出 Data Factory 支援的計算環境以及可在環境上執行的活動。 

| 計算環境                      | 活動                               |
| ---------------------------------------- | ---------------------------------------- |
| [隨選 HDInsight 叢集](#azure-hdinsight-on-demand-linked-service)或[您自己的 HDInsight 叢集](#azure-hdinsight-linked-service) | [Hive](transform-data-using-hadoop-hive.md)、[Pig](transform-data-using-hadoop-pig.md)、[Spark](transform-data-using-spark.md)、[MapReduce](transform-data-using-hadoop-map-reduce.md)、[Hadoop 串流](transform-data-using-hadoop-streaming.md) |
| [Azure Batch](#azure-batch-linked-service) | [自訂](transform-data-using-dotnet-custom-activity.md) |
| [Azure Machine Learning](#azure-machine-learning-linked-service) | [Machine Learning 活動︰批次執行和更新資源](transform-data-using-machine-learning.md) |
| [Azure 資料湖分析](#azure-data-lake-analytics-linked-service) | [Data Lake Analytics U-SQL](transform-data-using-data-lake-analytics.md) |
| [Azure SQL](#azure-sql-linked-service)、[Azure SQL 資料倉儲](#azure-sql-data-warehouse-linked-service)、[SQL Server](#sql-server-linked-service) | [預存程序](transform-data-using-stored-procedure.md) |

>  

## <a name="on-demand-compute-environment"></a>隨選計算環境
在這種組態中，運算環境會完全由 Azure Data Factory 服務管理。 Data Factory 服務會在工作提交前自動建立運算環境以處理資料，而在工作完成時予以移除。 您可以建立隨選計算環境的連結服務、加以設定，以及控制工作執行、叢集管理和啟動動作的細微設定。

> [!NOTE]
> 目前僅支援 Azure HDInsight 叢集的隨選組態。
>
> 

## <a name="azure-hdinsight-on-demand-linked-service"></a>Azure HDInsight 隨選連結服務
Azure Data Factory 服務可自動建立隨選 HDInsight 叢集來處理資料。 此叢集會建立在與叢集相關聯的儲存體帳戶 (JSON 中的 linkedServiceName 屬性) 相同的區域中。 儲存體帳戶必須是一般目的標準 Azure 儲存體帳戶。 

請注意下列有關隨選 HDInsight 連結服務的 **重點** ：

* 您的 Azure 訂用帳戶下會建立隨選 HDInsight 叢集。 該叢集啟動並執行時，您能看到該叢集出現在您的 Azure 入口網站中。 
* 在隨選 HDInsight 叢集上執行之工作的記錄檔會被複製到與 HDInsight 叢集相關聯的儲存體帳戶。 連結服務定義中定義的 clusterUserName、clusterPassword、clusterSshUserName、clusterSshPassword 可用來登入該叢集，以便在該叢集的生命週期中進行深入的疑難排解。 
* 只會針對 HDInsight 叢集啟動並執行工作的時間來向您收取費用。

> [!IMPORTANT]
> 通常會花費 **20 分鐘**或更久的時間來佈建隨選 Azure HDInsight 叢集。
>
> 

### <a name="example"></a>範例
下列 JSON 會定義以 Linux 為基礎的隨選 HDInsight 連結服務。 Data Factory 服務會自動建立**以 Linux 為基礎的** HDInsight 叢集，以處理必要的活動。 

```json
{
  "name": "HDInsightOnDemandLinkedService",
  "properties": {
    "type": "HDInsightOnDemand",
    "typeProperties": {
      "clusterType": "hadoop",
      "clusterSize": 1,
      "timeToLive": "00:15:00",
      "hostSubscriptionId": "<subscription ID>",
      "servicePrincipalId": "<service principal ID>",
      "servicePrincipalKey": {
        "value": "<service principal key>",
        "type": "SecureString"
      },
      "tenant": "<tenent id>",
      "clusterResourceGroup": "<resource group name>",
      "version": "3.6",
      "osType": "Linux",
      "linkedServiceName": {
        "referenceName": "AzureStorageLinkedService",
        "type": "LinkedServiceReference"
      }
    },
    "connectVia": {
      "referenceName": "<name of Integration Runtime>",
      "type": "IntegrationRuntimeReference"
    }
  }
}
```

> [!IMPORTANT]
> HDInsight 叢集會在您於 JSON 中指定的 Blob 儲存體 (**linkedServiceName**) 建立**預設容器**。 HDInsight 不會在刪除叢集時刪除此容器。 這是設計的行為。 在使用 HDInsight 隨選連結服務時，除非有現有的即時叢集 (**timeToLive**)，否則每當需要處理配量時，就會建立 HDInsight 叢集，並在處理完成時予以刪除。 
>
> 隨著執行的活動越來越多，您會在 Azure Blob 儲存體中看到許多容器。 如果在疑難排解作業時不需要這些容器，建議您加以刪除以降低儲存成本。 這些容器的名稱會遵循模式︰`adf**yourdatafactoryname**-**linkedservicename**-datetimestamp`。 請使用 [Microsoft 儲存體總管](http://storageexplorer.com/) 之類的工具刪除 Azure Blob 儲存體中的容器。
>
> 

### <a name="properties"></a>properties
| 屬性                     | 說明                              | 必要 |
| ---------------------------- | ---------------------------------------- | -------- |
| type                         | type 屬性應設為 **HDInsightOnDemand**。 | yes      |
| clusterSize                  | 叢集中的背景工作/資料節點數。 HDInsight 叢集會利用您為此屬性指定的 2 個前端節點以及背景工作節點數目來建立。 節點大小為具有 4 個核心的 Standard_D3，因此 4 個背景工作節點的叢集需要 24 個核心 (4\*4 = 16 個核心用於背景工作節點，加上 2\*4 = 8 個核心用於前端節點)。 如需詳細資料，請參閱[使用 Hadoop、Spark 及 Kafka 等在 HDInsight 中設定叢集](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md)。 | yes      |
| 預設容器            | 隨選叢集用於儲存及處理資料的 Azure 儲存體連結服務。 建立 HDInsight 叢集的區域和這個 Azure 儲存體帳戶的區域相同。 Azure HDInsight 對您在其支援的每個 Azure 區域中可使用的核心總數有所限制。 請確定 Azure 區域有足夠的核心配額，以符合所需的 clusterSize。 如需詳細資料，請參閱[使用 Hadoop、Spark 及 Kafka 等在 HDInsight 中設定叢集](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md)。<p>目前，您無法建立使用 Azure Data Lake Store 做為儲存體的隨選 HDInsight 叢集。 如果您想要在 Azure Data Lake Store 中儲存 HDInsight 處理的結果資料，可使用複製活動將 Azure Blob 儲存體的資料複製到 Azure Data Lake Store。 </p> | yes      |
| clusterResourceGroup         | 在此資源群組中將建立 HDInsight 叢集。 | yes      |
| timetolive                   | 隨選 HDInsight 叢集允許的閒置時間。 指定在活動執行完成後，如果叢集中沒有其他作用中的作業，隨選 HDInsight 叢集要保持運作多久。 最小的允許值為 5 分鐘 (00:05:00)。<br/><br/>例如，如果活動執行花費 6 分鐘，而 timetolive 設為 5 分鐘，叢集會在處理活動執行的 6 分鐘期間之後保持運作 5 分鐘。 如果 6 分鐘期間內執行另一個活動，則會由相同叢集來處理。<br/><br/>建立隨選 HDInsight 叢集是昂貴的作業 (可能需要一段時間)，因此請視需要使用這項設定，重複使用隨選 HDInsight 叢集以改善 Data Factory 的效能。<br/><br/>如果您將 timetolive 值設為 0，叢集會在活動執行完成後立即刪除。 不過，如果您設定較高的值，叢集可能會保持閒置，以便您登入進行一些疑難排解，但是可能會導致高成本。 因此，請務必根據您的需求設定適當的值。<br/><br/>如果適當地設定 timetolive 屬性值，則多個管線可以共用隨選 HDInsight 叢集的執行個體。 | yes      |
| clusterType                  | 將建立的 HDInsight 叢集類型。 允許的值為「hadoop」和「spark」。 若未指定，則預設值為 hadoop。 | 否       |
| version                      | HDInsight 叢集的版本。 如果未指定，則使用目前的 HDInsight 定義的預設版本。 | 否       |
| hostSubscriptionId           | 用來建立 HDInsight 叢集的 Azure 訂用帳戶識別碼。 如果未指定，它會使用您 Azure 登入內容的訂用帳戶識別碼。 | 否       |
| clusterNamePrefix           | HDI 叢集名稱的前置詞，在叢集名稱的結尾會自動附加時間戳記| 否       |
| sparkVersion                 | 如果叢集類型是「Spark」，則為 spark 的版本 | 否       |
| additionalLinkedServiceNames | 指定 HDInsight 連結服務的其他儲存體帳戶，讓 Data Factory 服務代表您註冊它們。 這些儲存體帳戶與 HDInsight 叢集必須在相同區域，而建立此叢集的區域與 linkedServiceName 所指定之儲存體帳戶的區域相同。 | 否       |
| osType                       | 作業系統的類型。 允許的值為：Linux 和 Windows (僅適用於 HDInsight 3.3)。 預設值為 Linux | 否       |
| hcatalogLinkedServiceName    | 指向 HCatalog 資料庫的 Azure SQL 連結服務名稱。 會使用 Azure SQL 資料庫作為中繼存放區，建立隨選 HDInsight 叢集。 | 否       |
| connectVia                   | 將活動分派到此 HDInsight 連結服務所用的整合執行階段。 對於隨選 HDInsight 連結服務，它只會支援 Azure 整合執行階段。 如果未指定，就會使用預設的 Azure Integration Runtime。 | 否       |
| clusterUserName                   | 存取叢集的使用者名稱。 | 否       |
| clusterPassword                   | 存取叢集的密碼，為安全字串類型。 | 否       |
| clusterSshUserName         | 以 SSH 遠端連線到叢集節點的使用者名稱 (適用於 Linux)。 | 否       |
| clusterSshPassword         | 以 SSH 遠端連線到叢集節點的密碼，為安全字串類型 (適用於 Linux)。 | 否       |


> [!IMPORTANT]
> HDInsight 支援多個可部署的 Hadoop 叢集版本。 每一個版本選擇都會建立特定版本的 Hortonworks Data Platform (HDP) 散發，以及該散發內包含的一組元件。 支援的 HDInsight 版本清單會持續更新，以提供最新的 Hadoop 生態系統元件和修正程式。 務必參閱[支援的 HDInsight 版本及 OS 類型](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions)，確定您已使用支援的 HDInsight 版本。 
>
> 

#### <a name="additionallinkedservicenames-json-example"></a>additionalLinkedServiceNames JSON 範例

```json
"additionalLinkedServiceNames": [{
    "referenceName": "MyStorageLinkedService2",
    "type": "LinkedServiceReference"          
}]
```

### <a name="service-principal-authentication"></a>服務主體驗證

隨選 HDInsight 連結服務需要服務主體驗證，才能代表您建立 HDInsight 叢集。 若要使用服務主體驗證，請在 Azure Active Directory (Azure AD) 中註冊應用程式實體，並將建立 HDInsight 叢集的訂用帳戶或資源群組之中的**參與者**角色授與該實體。 如需詳細步驟，請參閱[使用入口網站來建立可存取資源的 Active Directory 應用程式和服務主體](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal)。 請記下以下的值，您可以使用這些值來定義連結服務：

- 應用程式識別碼
- 應用程式金鑰 
- 租用戶識別碼

指定下列屬性以使用服務主體驗證：

| 屬性                | 說明                              | 必要 |
| :---------------------- | :--------------------------------------- | :------- |
| **servicePrincipalId**  | 指定應用程式的用戶端識別碼。     | yes      |
| **servicePrincipalKey** | 指定應用程式的金鑰。           | yes      |
| **tenant**              | 指定您的應用程式所在租用戶的資訊 (網域名稱或租用戶識別碼)。 將滑鼠游標暫留在 Azure 入口網站右上角，即可擷取它。 | yes      |

### <a name="advanced-properties"></a>進階屬性

您也可以針對隨選 HDInsight 叢集的細微組態指定下列屬性。

| 屬性               | 說明                              | 必要 |
| :--------------------- | :--------------------------------------- | :------- |
| coreConfiguration      | 指定要建立之 HDInsight 叢集的核心組態參數 (如 core-site.xml 所示)。 | 否       |
| hBaseConfiguration     | 指定 HDInsight 叢集的 HBase 組態參數 (hbase-site.xml)。 | 否       |
| hdfsConfiguration      | 指定 HDInsight 叢集的 HDFS 組態參數 (hdfs-site.xml)。 | 否       |
| hiveConfiguration      | 指定 HDInsight 叢集的 hive 組態參數 (hive-site.xml)。 | 否       |
| mapReduceConfiguration | 指定 HDInsight 叢集的 MapReduce 組態參數 (mapred-site.xml)。 | 否       |
| oozieConfiguration     | 指定 HDInsight 叢集的 Oozie 組態參數 (oozie-site.xml)。 | 否       |
| stormConfiguration     | 指定 HDInsight 叢集的 Storm 組態參數 (storm-site.xml)。 | 否       |
| yarnConfiguration      | 指定 HDInsight 叢集的 Yarn 組態參數 (yarn-site.xml)。 | 否       |

#### <a name="example--on-demand-hdinsight-cluster-configuration-with-advanced-properties"></a>範例 – 包含進階屬性的隨選 HDInsight 叢集組態

```json
{
    "name": " HDInsightOnDemandLinkedService",
    "properties": {
      "type": "HDInsightOnDemand",
      "typeProperties": {
          "clusterSize": 16,
          "timeToLive": "01:30:00",
          "hostSubscriptionId": "<subscription ID>",
          "servicePrincipalId": "<service principal ID>",
          "servicePrincipalKey": {
            "value": "<service principal key>",
            "type": "SecureString"
          },
          "tenant": "<tenent id>",
          "clusterResourceGroup": "<resource group name>",
          "version": "3.6",
          "osType": "Linux",
          "linkedServiceName": {
              "referenceName": "AzureStorageLinkedService",
              "type": "LinkedServiceReference"
            },
            "coreConfiguration": {
                "templeton.mapper.memory.mb": "5000"
            },
            "hiveConfiguration": {
                "templeton.mapper.memory.mb": "5000"
            },
            "mapReduceConfiguration": {
                "mapreduce.reduce.java.opts": "-Xmx4000m",
                "mapreduce.map.java.opts": "-Xmx4000m",
                "mapreduce.map.memory.mb": "5000",
                "mapreduce.reduce.memory.mb": "5000",
                "mapreduce.job.reduce.slowstart.completedmaps": "0.8"
            },
            "yarnConfiguration": {
                "yarn.app.mapreduce.am.resource.mb": "5000",
                "mapreduce.map.memory.mb": "5000"
            },
            "additionalLinkedServiceNames": [{
                "referenceName": "MyStorageLinkedService2",
                "type": "LinkedServiceReference"          
            }]
        }
    },
      "connectVia": {
      "referenceName": "<name of Integration Runtime>",
      "type": "IntegrationRuntimeReference"
    }
}
```

### <a name="node-sizes"></a>節點大小
您可使用下列屬性指定前端、資料和的 zookeeper 節點的大小： 

| 屬性          | 說明                              | 必要 |
| :---------------- | :--------------------------------------- | :------- |
| headNodeSize      | 指定前端節點的大小。 預設值為：Standard_D3。 如需詳細資料，請參閱**指定節點大小**一節。 | 否       |
| dataNodeSize      | 指定資料節點的大小。 預設值為：Standard_D3。 | 否       |
| zookeeperNodeSize | 指定 Zoo Keeper 節點的大小。 預設值為：Standard_D3。 | 否       |

#### <a name="specifying-node-sizes"></a>指定節點大小
有關您在上一節所述的屬性中需要指定的字串值，請參閱[虛擬機器的大小](../virtual-machines/linux/sizes.md)一文。 值必須符合本文件中所參考的 **CMDLET 與 APIS**。 如文中所述，「大型」(預設值) 資料節點的記憶體大小為 7-GB，但這可能不適用於您的案例。 

若想要建立 D4 大小的前端節點與背景工作節點，請指定 **Standard_D4** 作為 headNodeSize 與 dataNodeSize 屬性的值。 

```json
"headNodeSize": "Standard_D4",    
"dataNodeSize": "Standard_D4",
```

若您為這些屬性指定錯誤的值，可能會顯示下列 **錯誤：** 無法建立叢集。 例外狀況：無法完成叢集建立作業。 作業失敗，錯誤碼為 '400'。 叢集剩餘狀態：「錯誤」。 訊息：「PreClusterCreationValidationFailure」。 出現此錯誤時，請確定您是使用[虛擬機器的大小](../virtual-machines/linux/sizes.md)一文的表格中的 **CMDLET 與 API** 名稱。        

## <a name="bring-your-own-compute-environment"></a>自備計算環境
在這種組態中，使用者可以將現有的運算環境註冊為 Data Factory 中的連結服務。 此運算環境是由使用者管理並由 Data Factory 服務用來執行活動。

下列計算環境可支援這類型的組態：

* Azure HDInsight
* Azure Batch
* Azure Machine Learning
* Azure Data Lake Analytics
* Azure SQL DB、Azure SQL DW、SQL Server

## <a name="azure-hdinsight-linked-service"></a>Azure HDInsight 連結服務
您可以建立 Azure HDInsight 連結服務，以向 Data Factory 註冊自己的 HDInsight 叢集。

### <a name="example"></a>範例

```json
{
    "name": "HDInsightLinkedService",
    "properties": {
      "type": "HDInsight",
      "typeProperties": {
        "clusterUri": " https://<hdinsightclustername>.azurehdinsight.net/",
        "userName": "username",
        "password": {
            "value": "passwordvalue",
            "type": "SecureString"
          },
        "linkedServiceName": {
              "referenceName": "AzureStorageLinkedService",
              "type": "LinkedServiceReference"
        }
      },
      "connectVia": {
        "referenceName": "<name of Integration Runtime>",
        "type": "IntegrationRuntimeReference"
      }
    }
  }
```

### <a name="properties"></a>properties
| 屬性          | 說明                              | 必要 |
| ----------------- | ---------------------------------------- | -------- |
| type              | type 屬性應設為 **HDInsight**。 | yes      |
| clusterUri        | HDInsight 叢集的 URI。        | yes      |
| username          | 指定要用來連接到現有 HDInsight 叢集的使用者名稱。 | yes      |
| password          | 指定使用者帳戶的密碼。   | yes      |
| 預設容器 | 參照 HDInsight 叢集所使用 Azure Blob 儲存體的 Azure 儲存體連結服務名稱。 <p>目前，您無法針對此屬性指定 Azure Data Lake Store 連結服務。 如果 HDInsight 叢集可存取 Data Lake Store，您可以透過 Hive/Pig 指令碼存取 Azure Data Lake Store 中的資料。 </p> | yes      |
| connectVia        | 將活動分派到此連結服務所用的整合執行階段。 您可以使用 Azure 整合執行階段或自我裝載整合執行階段。 如果未指定，就會使用預設的 Azure Integration Runtime。 | 否       |

> [!IMPORTANT]
> HDInsight 支援多個可部署的 Hadoop 叢集版本。 每一個版本選擇都會建立特定版本的 Hortonworks Data Platform (HDP) 散發，以及該散發內包含的一組元件。 支援的 HDInsight 版本清單會持續更新，以提供最新的 Hadoop 生態系統元件和修正程式。 務必參閱[支援的 HDInsight 版本及 OS 類型](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions)，確定您已使用支援的 HDInsight 版本。 
>

## <a name="azure-batch-linked-service"></a>Azure Batch 已連結的服務

您可以建立 Azure Batch 連結服務，以向 Data Factory 註冊虛擬機器 (VM) 的 Batch 集區。 您可以使用 Azure Batch 執行自訂活動。

如果您不熟悉 Azure Batch 服務，請參閱下列主題：

* [Azure Batch 基本知識](../batch/batch-technical-overview.md) ，以取得 Azure Batch 服務的概觀。
* [New-AzureRmBatchAccount](/powershell/module/azurerm.batch/New-AzureRmBatchAccount?view=azurermps-4.3.1) Cmdlet 可建立 Azure Batch 帳戶 (或) [Azure 入口網站](../batch/batch-account-create-portal.md)，以使用 Azure 入口網站建立 Azure Batch 帳戶。 如需使用此 Cmdlet 的詳細指示，請參閱 [使用 PowerShell 管理 Azure Batch 帳戶](http://blogs.technet.com/b/windowshpc/archive/2014/10/28/using-azure-powershell-to-manage-azure-batch-account.aspx) 主題。
* [New-AzureBatchPool](/powershell/module/azurerm.batch/New-AzureBatchPool?view=azurermps-4.3.1) Cmdlet 可建立 Azure Batch 集區。

### <a name="example"></a>範例

```json
{
    "name": "AzureBatchLinkedService",
    "properties": {
      "type": "AzureBatch",
      "typeProperties": {
        "accountName": "batchaccount",
        "accessKey": {
          "type": "SecureString",
          "value": "access key"
        },
        "batchUri": "https://batchaccount.region.batch.azure.com",
        "poolName": "poolname",
        "linkedServiceName": {
          "referenceName": "StorageLinkedService",
          "type": "LinkedServiceReference"
        }
      },
      "connectVia": {
        "referenceName": "<name of Integration Runtime>",
        "type": "IntegrationRuntimeReference"
      }
    }
  }
```


### <a name="properties"></a>properties
| 屬性          | 說明                              | 必要 |
| ----------------- | ---------------------------------------- | -------- |
| type              | type 屬性應設為 **AzureBatch**。 | yes      |
| accountName       | 建立 Azure Batch 帳戶。         | yes      |
| accessKey         | Azure Batch 帳戶的存取金鑰。  | yes      |
| batchUri          | 您 Azure Batch 帳戶的 URL，格式為 https://*batchaccountname.region*.batch.azure.com。 | yes      |
| poolName          | 虛擬機器的集區名稱。    | yes      |
| 預設容器 | 與此 Azure Batch 連結服務相關聯的 Azure 儲存體服務連結名稱。 此連結服務用於執行活動所需的暫存檔案。 | yes      |
| connectVia        | 將活動分派到此連結服務所用的整合執行階段。 您可以使用 Azure 整合執行階段或自我裝載整合執行階段。 如果未指定，就會使用預設的 Azure Integration Runtime。 | 否       |

## <a name="azure-machine-learning-linked-service"></a>Azure Machine Learning 連結服務
您可建立 Azure Machine Learning 連結服務，以向 Data Factory 註冊 Machine Learning 批次評分端點。

### <a name="example"></a>範例

```json
{
    "name": "AzureMLLinkedService",
    "properties": {
      "type": "AzureML",
      "typeProperties": {
        "mlEndpoint": "https://[batch scoring endpoint]/jobs",
        "apiKey": {
            "type": "SecureString",
            "value": "access key"
        }
     },
     "connectVia": {
        "referenceName": "<name of Integration Runtime>",
        "type": "IntegrationRuntimeReference"
      }
    }
}
```

### <a name="properties"></a>properties
| 屬性               | 說明                              | 必要                                 |
| ---------------------- | ---------------------------------------- | ---------------------------------------- |
| 類型                   | type 屬性應設為： **AzureML**。 | yes                                      |
| mlEndpoint             | 批次評分 URL。                   | yes                                      |
| apiKey                 | 已發佈的工作區模型的 API。     | yes                                      |
| updateResourceEndpoint | Azure ML Web 服務端點 (用以藉由定型模型檔案更新預測性 Web 服務) 的更新資源 URL | 否                                       |
| servicePrincipalId     | 指定應用程式的用戶端識別碼。     | 如果指定 updateResourceEndpoint 則需要 |
| servicePrincipalKey    | 指定應用程式的金鑰。           | 如果指定 updateResourceEndpoint 則需要 |
| tenant                 | 指定您的應用程式所在租用戶的資訊 (網域名稱或租用戶識別碼)。 將滑鼠游標暫留在 Azure 入口網站右上角，即可擷取它。 | 如果指定 updateResourceEndpoint 則需要 |
| connectVia             | 將活動分派到此連結服務所用的整合執行階段。 您可以使用 Azure 整合執行階段或自我裝載整合執行階段。 如果未指定，就會使用預設的 Azure Integration Runtime。 | 否                                       |

## <a name="azure-data-lake-analytics-linked-service"></a>Azure Data Lake Analytics 已連結的服務
您需建立 **Azure Data Lake Analytics** 連結服務，來將 Azure Data Lake Analytics 計算服務連結到 Azure Data Factory。 管線中的 Data Lake Analytics U-SQL 活動會參考此連結服務。 

### <a name="example"></a>範例

```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "adftestaccount",
            "dataLakeAnalyticsUri": "azuredatalakeanalytics URI",
            "servicePrincipalId": "service principal id",
            "servicePrincipalKey": {
                "value": "service principal key",
                "type": "SecureString"
            },
            "tenant": "tenant ID",
            "subscriptionId": "<optional, subscription id of ADLA>",
            "resourceGroupName": "<optional, resource group name of ADLA>"
        },
        "connectVia": {
            "referenceName": "<name of Integration Runtime>",
            "type": "IntegrationRuntimeReference"
        }
    }
}
```

### <a name="properties"></a>properties

| 屬性             | 說明                              | 必要                                 |
| -------------------- | ---------------------------------------- | ---------------------------------------- |
| type                 | type 屬性應設為： **AzureDataLakeAnalytics**。 | yes                                      |
| accountName          | Azure Data Lake Analytics 帳戶名稱。  | yes                                      |
| dataLakeAnalyticsUri | Azure Data Lake Analytics URI。           | 否                                       |
| subscriptionId       | Azure 訂用帳戶識別碼                    | 否 (如果未指定，便會使用 Data Factory 的訂用帳戶)。 |
| resourceGroupName    | Azure 資源群組名稱                | 否 (若未指定，便會使用 Data Factory 的資源群組)。 |
| servicePrincipalId   | 指定應用程式的用戶端識別碼。     | yes                                      |
| servicePrincipalKey  | 指定應用程式的金鑰。           | yes                                      |
| tenant               | 指定您的應用程式所在租用戶的資訊 (網域名稱或租用戶識別碼)。 將滑鼠游標暫留在 Azure 入口網站右上角，即可擷取它。 | yes                                      |
| connectVia           | 將活動分派到此連結服務所用的整合執行階段。 您可以使用 Azure 整合執行階段或自我裝載整合執行階段。 如果未指定，就會使用預設的 Azure Integration Runtime。 | 否                                       |



## <a name="azure-sql-database-linked-service"></a>Azure SQL Database 的連結服務
您可建立 Azure SQL 連結服務，並將其與 [預存程序活動](transform-data-using-stored-procedure.md) 搭配使用，以叫用 Data Factory 管線中的預存程序。 如需此連結服務的詳細資料，請參閱 [Azure SQL 連接器](connector-azure-sql-database.md#linked-service-properties) 一文。

## <a name="azure-sql-data-warehouse-linked-service"></a>Azure SQL 資料倉儲連結服務
您可以建立 Azure SQL 資料倉儲連結服務，並將其與 [預存程序活動](transform-data-using-stored-procedure.md) 搭配使用，以叫用 Data Factory 管線中的預存程序。 如需此連結服務的詳細資料，請參閱 [Azure SQL 資料倉儲連接器](connector-azure-sql-data-warehouse.md#linked-service-properties) 一文。

## <a name="sql-server-linked-service"></a>SQL Server 連結服務
您可以建立 SQL Server 連結服務，並將其與 [預存程序活動](transform-data-using-stored-procedure.md) 搭配使用，以叫用 Data Factory 管線中的預存程序。 如需此連結服務的詳細資料，請參閱 [SQL Server 連接器](connector-sql-server.md#linked-service-properties) 一文。

## <a name="azure-data-factory---naming-rules"></a>Azure Data Factory - 命名規則
下表提供 Data Factory 購件命名規則。

| Name                             | 名稱唯一性                          | 驗證檢查                        |
| :------------------------------- | :--------------------------------------- | :--------------------------------------- |
| Data Factory                     | 在 Microsoft Azure 中是唯一的。 名稱不區分大小寫，亦即 `MyDF` 和 `mydf` 會指相同的 Data Factory。 | <ul><li>每個 Data Factory 只會繫結至一個 Azure 訂用帳戶。</li><li>物件名稱必須以字母或數字開頭，並且只能包含字母、數字和虛線 (-) 字元。</li><li>每個虛線 (-) 字元的前面和後面必須緊接字母或數字。 容器名稱中不允許使用連續虛線。</li><li>名稱長度可以介於 3-63 個字元。</li></ul> |
| 連結服務/資料表/管線 | 在 Data Factory 中是唯一的。 名稱不區分大小寫。 | <ul><li>資料表名稱的字元數目上限︰260。</li><li>物件名稱開頭必須為字母、數字或底線 (_)。</li><li>不允許使用下列字元：“.”、“+”、“?”、“/”、“<”、”>”、”*”、”%”、”&”、”:”、”\\”</li></ul> |
| 資源群組                   | 在 Microsoft Azure 中是唯一的。 名稱不區分大小寫。 | <ul><li>字元數目上限︰1000。</li><li>名稱可包含字母、數字及下列字元：“-”、“_”、“,” 和 “.”。</li></ul> |

## <a name="next-steps"></a>後續步驟
關於 Azure Data Factory 支援的轉換活動清單，請參閱[轉換資料](transform-data.md)。
