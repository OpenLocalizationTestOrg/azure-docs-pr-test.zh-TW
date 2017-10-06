---
title: "Azure Data Factory 支援 aaaCompute 環境 |Microsoft 文件"
description: "深入了解您可以使用 Azure Data Factory 管線 （例如 Azure HDInsight) tootransform 或處理資料中的運算環境。"
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 6877a7e8-1a58-4cfb-bbd3-252ac72e4145
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.topic: article
ms.date: 07/25/2017
ms.author: shlo
ms.openlocfilehash: aba7d7de695bc1c7d475f1e741ee3b3e884151c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="compute-environments-supported-by-azure-data-factory"></a>Azure Data Factory 支援的計算環境
本文說明不同的運算環境，您可以使用 tooprocess 或轉換資料。 它也提供詳細資料 （與指定 「 整合您自己） 不同的組態設定連結這些計算環境 tooan 的 Azure data factory 已連結的服務時，Data Factory 支援。

hello 下表提供支援的 Data Factory 和 hello 的活動可以在其上執行的運算環境的清單。 

| 計算環境 | 活動 |
| --- | --- |
| [隨選 HDInsight 叢集](#azure-hdinsight-on-demand-linked-service)或[您自己的 HDInsight 叢集](#azure-hdinsight-linked-service) |[DotNet](data-factory-use-custom-activities.md)、[Hive](data-factory-hive-activity.md)、[Pig](data-factory-pig-activity.md)、[MapReduce](data-factory-map-reduce.md)、[Hadoop 串流](data-factory-hadoop-streaming-activity.md) |
| [Azure Batch](#azure-batch-linked-service) |[DotNet](data-factory-use-custom-activities.md) |
| [Azure Machine Learning](#azure-machine-learning-linked-service) |[Machine Learning 活動︰批次執行和更新資源](data-factory-azure-ml-batch-execution-activity.md) |
| [Azure Data Lake Analytics](#azure-data-lake-analytics-linked-service) |[Data Lake Analytics U-SQL](data-factory-usql-activity.md) |
| [Azure SQL](#azure-sql-linked-service)、[Azure SQL 資料倉儲](#azure-sql-data-warehouse-linked-service)、[SQL Server](#sql-server-linked-service) |[預存程序](data-factory-stored-proc-activity.md) |

## <a name="supported-hdinsight-versions-in-azure-data-factory"></a>Azure Data Factory 中支援的 HDInsight 版本
Azure HDInsight 支援多個可隨時部署的 Hadoop 叢集版本。 特定版本的 hello Hortonworks Data Platform (HDP) 發佈和一組包含在該發佈的元件，會建立每個版本的選擇。 Microsoft 會持續更新 hello HDInsight tooprovide 最新 Hadoop 生態系統的元件和修正程式的支援版本清單。 在 2017 年 4 月 1，已被取代 hello HDInsight 3.2。 如需詳細資訊，請參閱[支援的 HDInsight 版本](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions)。

這會影響具有對 HDInsight 3.2 叢集執行活動的現有 Azure Data Factory。 我們建議使用者 toofollow hello 指導方針，在下列章節 tooupdate hello hello 受影響的 Data Factory:

### <a name="for-linked-services-pointing-tooyour-own-hdinsight-clusters"></a>連結的服務為指向 tooyour 自己的 HDInsight 叢集
* **指向 tooyour HDInsight 連結的服務擁有 HDInsight 3.2 或叢集如下：**

  Azure Data Factory 支援自己的 HDInsight 叢集的 HDI 3.1 太正在提交作業 tooyour[hello 最新支援 HDInsight 版本](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions)。 不過，您可以再建立 HDInsight 3.2 叢集之後 2017 年 4 月 1，根據所述的 hello 過時原則[支援 HDInsight 版本](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions)。  

  **建議：** 
  * 執行測試 tooensure hello 相容性的 hello 太參照此連結的服務活動都會[hello 最新支援 HDInsight 版本](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions)資訊記載於[Hadoop 元件適用於不同的 HDInsight 版本](../hdinsight/hdinsight-component-versioning.md#hadoop-components-available-with-different-hdinsight-versions)和[Hortonworks 版本資訊與 HDInsight 版本相關聯](../hdinsight/hdinsight-component-versioning.md#hortonworks-release-notes-associated-with-hdinsight-versions)。
  * 升級您的 HDInsight 3.2 叢集太[hello 最新支援 HDInsight 版本](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions)tooget hello 最新的 Hadoop 生態系統元件和修正程式。 

* **指向 tooyour HDInsight 連結的服務擁有 HDInsight 3.3 或更新版本的叢集：**

  Azure Data Factory 支援自己的 HDInsight 叢集的 HDI 3.1 太正在提交作業 tooyour[hello 最新支援 HDInsight 版本](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions)。 
  
  **建議：** 
  * 從 Data Factory 的觀點來看，不需要採取任何動作。 不過，如果您是在較低版本的 HDInsight 上，我們仍建議您升級太[hello 最新支援 HDInsight 版本](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions)tooget hello 最新的 Hadoop 生態系統元件和修正程式。

### <a name="for-hdinsight-on-demand-linked-services"></a>針對 HDInsight 隨選連結服務
* **3.2 版或以下版本是在 HDInsight 隨選連結服務 JSON 定義中指定：**
  
  自 **2017/05/15** 起，Azure Data Factory 支援建立隨選 HDInsight 叢集 3.3 版或更新版本。 和 hello 結束支援適用於現有連結的服務會擴充太隨 HDInsight 3.2**07/15/2017年**。  

  **建議：** 
  * 執行測試 tooensure hello 相容性的 hello 太參照此連結的服務活動都會[hello 最新支援 HDInsight 版本](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions)資訊記載於[Hadoop 元件適用於不同的 HDInsight 版本](../hdinsight/hdinsight-component-versioning.md#hadoop-components-available-with-different-hdinsight-versions)和[Hortonworks 版本資訊與 HDInsight 版本相關聯](../hdinsight/hdinsight-component-versioning.md#hortonworks-release-notes-associated-with-hdinsight-versions)。
  * 之前**07/15/2017年**，視 HDI 連結的服務 JSON 定義中的 hello 版本屬性更新太[hello 最新支援 HDInsight 版本](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions)tooget hello 最新 Hadoop 生態系統的元件和修正程式。 如需詳細的 JSON 定義中，請參閱 toohello [Azure HDInsight 隨連結的服務範例](#azure-hdinsight-on-demand-linked-service)。 

* **隨選 HDInsight 連結服務中未指定的版本：**
  
  自 **2017/05/15** 起，Azure Data Factory 支援建立隨選 HDInsight 叢集 3.3 版或更新版本。 和支援 tooexisting 隨 HDInsight 3.2 連結服務的 hello 結尾延伸太**07/15/2017年**。 

  之前**07/15/2017年**，如果保留空白，hello 的預設值的版本與 osType 屬性： 

  | 屬性 | 預設值 | 必要 |
  | --- | --- | --- |
  版本   | Windows 叢集為 HDI 3.1，Linux 叢集為 HDI 3.2。| 否
  osType | hello 預設值是 Windows | 否

  之後**07/15/2017年**，如果保留空白，hello 的預設值的版本與 osType 屬性：

  | 屬性 | 預設值 | 必要 |
  | --- | --- | --- |
  版本   | Windows 叢集為 HDI 3.3，Linux 叢集為 3.5。    | 否
  osType | hello 預設值是 Linux   | 否

  **建議：** 
  * 之前**07/15/2017年**，執行測試 tooensure hello 相容性的 hello 太參照此連結的服務活動都會[hello 最新支援 HDInsight 版本](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions)記錄的資訊在[Hadoop 元件使用不同的 HDInsight 版本](../hdinsight/hdinsight-component-versioning.md#hadoop-components-available-with-different-hdinsight-versions)和[Hortonworks 版本資訊與 HDInsight 版本相關聯](../hdinsight/hdinsight-component-versioning.md#hortonworks-release-notes-associated-with-hdinsight-versions)。  
  * 之後**07/15/2017年**，請確定您明確指定 osType 和版本值，如果您想要 toooverride hello 預設設定。 

>[!Note]
>目前 Azure Data Factory 不支援使用 Azure Data Lake Store 作為主要存放區的 HDInsight 叢集。 使用 Azure 儲存體作為 HDInsight 叢集的主要存放區。 
>  
>  

## <a name="on-demand-compute-environment"></a>隨選計算環境
在這種設定中完全是由 hello Azure Data Factory 服務管理 hello 運算環境。 它會自動建立 hello Data Factory 服務作業送出的 tooprocess 資料之前，移除 hello 工作完成時。 您可以建立 hello 隨計算環境是連結的服務、 加以設定，並控制細微作業執行，叢集管理，以及設定啟動載入動作。

> [!NOTE]
> 目前的 Azure HDInsight 叢集才支援 hello 上隨選安裝設定。
> 
> 

## <a name="azure-hdinsight-on-demand-linked-service"></a>Azure HDInsight 隨選連結服務
hello Azure Data Factory 服務會自動建立 Windows/Linux 為基礎-隨選 HDInsight 叢集 tooprocess 資料。 hello 叢集建立在 hello 與 hello 叢集與 hello 儲存體帳戶 （hello JSON 中的 linkedServiceName 屬性） 相同的區域相關聯。 hello 儲存體帳戶必須是一般用途的標準 Azure 儲存體帳戶。 

請注意下列 hello**重要**要點隨 HDInsight 連結服務：

* 您不會看到 hello 隨您的 Azure 訂用帳戶中建立的 HDInsight 叢集。 hello Azure Data Factory 服務管理您的名義 hello 隨 HDInsight 叢集。
* hello 的點播 HDInsight 叢集執行的作業記錄檔複製 toohello hello HDInsight 叢集相關聯的儲存體帳戶。 您可以從 hello hello 在 Azure 入口網站存取這些記錄檔**活動執行詳細資料**刀鋒視窗。 如需詳細資訊，請參閱 [監視及管理管線](data-factory-monitor-manage-pipelines.md) 一文。
* 您必須支付只 hello 時間 hello HDInsight 叢集已啟動並執行工作。

> [!IMPORTANT]
> 通常可以花**20 分鐘**或依需求的詳細 tooprovision Azure HDInsight 叢集。
> 
> 

### <a name="example"></a>範例
下列 JSON hello 定義以 Linux 為基礎的隨選 HDInsight 連結服務。 hello Data Factory 服務會自動建立**linux**時處理資料配量的 HDInsight 叢集。 

```json
{
    "name": "HDInsightOnDemandLinkedService",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "linkedServiceName": "AzureStorageLinkedService"
        }
    }
}
```

設定 Windows 為基礎的 HDInsight 叢集，toouse **osType**太**windows**或請勿使用 hello 屬性，因為 hello 預設值是： windows。  

> [!IMPORTANT]
> hello HDInsight 叢集建立**預設容器**hello hello JSON 中指定的 blob 儲存體中 (**linkedServiceName**)。 HDInsight 刪除 hello 叢集時，不會刪除此容器。 這是設計的行為。 HDInsight 叢集隨 HDInsight 連結服務，以建立每次配量需要處理現有的叢集即時除非 toobe (**timeToLive**) 和 hello 處理完成時刪除。 
> 
> 隨著處理的配量越來越多，您會在 Azure Blob 儲存體中看到許多容器。 如果您不需要它們進行疑難排解的 hello 工作，您可能會想 toodelete 它們 tooreduce hello 儲存體成本。 這些容器的 hello 名稱遵循模式： `adf**yourdatafactoryname**-**linkedservicename**-datetimestamp`。 使用工具，例如[Microsoft 儲存體總管](http://storageexplorer.com/)toodelete 容器，在您的 Azure blob 儲存體。
> 
> 

### <a name="properties"></a>屬性
| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| 類型 |hello 類型屬性應該設定太**HDInsightOnDemand**。 |是 |
| clusterSize |背景工作/資料 hello 叢集中的節點數目。 以及您為此屬性指定的背景工作角色節點的 hello 數目的 2 個前端節點建立 hello HDInsight 叢集。 hello 節點有大小有 4 個核心，因此 4 的背景工作節點叢集會採用 24 個核心的 Standard_D3 (4\*4 = 16 個核心的背景工作節點，再加上 2\*4 = 8 個核心的前端節點)。 請參閱[HDInsight 叢集建立 Linux Hadoop](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md) hello Standard_D3 層的詳細資料。 |是 |
| timetolive |hello 允許 hello 隨選 HDInsight 叢集的閒置時間。 指定多久 hello 隨選 HDInsight 叢集會保持運作如果 hello 叢集中沒有其他作用中的工作執行的活動完成後。<br/><br/>例如，如果在 6 分鐘和 timetolive 執行的活動是設定 too5 分鐘，hello 叢集會保持運作 5 分鐘之後 hello 6 分鐘處理 hello 活動執行。 如果另一個執行的活動與 hello 6 分鐘內視窗執行時，處理 hello 相同叢集中。<br/><br/>建立隨選 HDInsight 叢集是昂貴的作業 （可能需要一些時間），因此使用這項設定的 data factory 所需的 tooimprove 效能重複使用隨選 HDInsight 叢集。<br/><br/>如果您設定 timetolive 值 too0，hello 活動執行完成時，會刪除 hello 叢集。 不過，如果您設定較高的值，hello 叢集可能會維持閒置的不必要地產生高成本。 因此，很重要，您會設定 hello 適當的值，根據您的需求。<br/><br/>適當地設定 hello timetolive 屬性值，如果多個管線可以共用 hello hello 隨選 HDInsight 叢集執行個體。  |是 |
| 版本 |Hello HDInsight 叢集的版本。 hello 預設值是 Windows 叢集的 3.1 和 3.2 for Linux 叢集。 |否 |
| linkedServiceName | Azure 儲存體連結服務 toobe hello 視叢集使用的儲存及處理資料。 hello HDInsight 叢集建立在 hello 相同與此 Azure 儲存體帳戶的區域。<p>目前，您無法建立使用 Azure 資料湖存放區為 hello 存放裝置的隨 HDInsight 叢集。 如果您想要從 HDInsight 處理 Azure 資料湖存放區中的 toostore hello 結果資料，請使用 hello Azure Blob 儲存體 toohello Azure Data Lake Store 複製活動 toocopy hello 資料。 </p>  | 是 |
| additionalLinkedServiceNames |指定額外的儲存體帳戶的 hello HDInsight 連結服務，以便 hello Data Factory 服務可以代表您註冊它們。 這些儲存體帳戶必須在 hello 與 hello HDInsight 叢集，這是在 hello 相同相同的區域與 hello linkedServiceName 所指定的儲存體帳戶的區域。 |否 |
| osType |作業系統的類型。 允許的值為：Windows (預設值) 和 linux |否 |
| hcatalogLinkedServiceName |該點 toohello HCatalog 資料庫服務的 Azure SQL 連結的 hello 名稱。 hello 隨選 HDInsight 叢集會建立使用 hello Azure SQL database 當做 hello 中繼存放區。 |否 |

#### <a name="additionallinkedservicenames-json-example"></a>additionalLinkedServiceNames JSON 範例

```json
"additionalLinkedServiceNames": [
    "otherLinkedServiceName1",
    "otherLinkedServiceName2"
  ]
```

### <a name="advanced-properties"></a>進階屬性
您也可以指定 hello hello 細微 hello 隨選 HDInsight 叢集組態的下列屬性。

| 屬性 | 說明 | 必要 |
|:--- |:--- |:--- |
| coreConfiguration |指定建立 hello HDInsight 叢集 toobe hello 核心組態參數 （如 core-site.xml 所示）。 |否 |
| hBaseConfiguration |指定 hello HBase 組態參數 (hbase-site.xml) hello HDInsight 叢集。 |否 |
| hdfsConfiguration |指定 hello HDFS 組態參數 (hdfs-site.xml) hello HDInsight 叢集。 |否 |
| hiveConfiguration |指定 hello hive 組態參數 (hive-site.xml) hello HDInsight 叢集。 |否 |
| mapReduceConfiguration |指定 hello MapReduce 組態參數 (mapred-site.xml) hello HDInsight 叢集。 |否 |
| oozieConfiguration |指定 hello Oozie 組態參數 (oozie-site.xml) hello HDInsight 叢集。 |否 |
| stormConfiguration |指定 hello Storm 組態參數 (storm-site.xml) hello HDInsight 叢集。 |否 |
| yarnConfiguration |指定 hello Yarn 組態參數 (yarn-site.xml) hello HDInsight 叢集。 |否 |

#### <a name="example--on-demand-hdinsight-cluster-configuration-with-advanced-properties"></a>範例 – 包含進階屬性的隨選 HDInsight 叢集組態

```json
{
  "name": " HDInsightOnDemandLinkedService",
  "properties": {
    "type": "HDInsightOnDemand",
    "typeProperties": {
      "clusterSize": 16,
      "timeToLive": "01:30:00",
      "linkedServiceName": "adfods1",
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
      "additionalLinkedServiceNames": [
        "datafeeds",
        "adobedatafeed"
      ]
    }
  }
}
```

### <a name="node-sizes"></a>節點大小
您可以指定標頭、 資料和動物園管理員的節點，使用下列屬性的 hello hello 的大小： 

| 屬性 | 說明 | 必要 |
|:--- |:--- |:--- |
| headNodeSize |指定 hello hello 前端節點大小。 hello 預設值是： Standard_D3。 請參閱 hello**指定節點大小**如需詳細資訊。 |否 |
| dataNodeSize |指定 hello 大小 hello 資料節點。 hello 預設值是： Standard_D3。 |否 |
| zookeeperNodeSize |指定 hello 大小 hello Zoo 持有者節點。 hello 預設值是： Standard_D3。 |否 |

#### <a name="specifying-node-sizes"></a>指定節點大小
請參閱 hello[虛擬機器的大小](../virtual-machines/linux/sizes.md)發行項的字串值，您需要 toospecify hello hello 前一節中所述的屬性。 hello 值需要 tooconform toohello**指令程式 （& s) API** hello 文件中參考。 您可以看到 hello 文件中，大型 （預設值） 大小的 hello 資料節點有 7 GB 記憶體，但這不是適用於您的案例。 

如果您想 toocreate D4 大小前端節點和背景工作節點，請指定**Standard_D4**為 hello headNodeSize 和 dataNodeSize 屬性的值。 

```json
"headNodeSize": "Standard_D4",    
"dataNodeSize": "Standard_D4",
```

如果您指定這些屬性的值錯誤時，您可能會收到 hello 下列**錯誤：**失敗 toocreate 叢集。 例外狀況： 無法 toocomplete hello 叢集建立作業。 作業失敗，錯誤碼為 '400'。 叢集剩餘狀態：「錯誤」。 訊息：「PreClusterCreationValidationFailure」。 當您收到這個錯誤時，請確定您使用 hello**指令程式 （& s) API** hello hello 表格名稱[虛擬機器的大小](../virtual-machines/linux/sizes.md)發行項。  

## <a name="bring-your-own-compute-environment"></a>自備計算環境
在這種組態中，使用者可以將現有的運算環境註冊為 Data Factory 中的連結服務。 hello 運算環境是由管理 hello 使用者並 hello Data Factory 服務會使用它 tooexecute hello 活動。

Hello 下列計算環境支援這種設定：

* Azure HDInsight
* Azure Batch
* Azure Machine Learning
* Azure Data Lake Analytics
* Azure SQL DB、Azure SQL DW、SQL Server

## <a name="azure-hdinsight-linked-service"></a>Azure HDInsight 連結服務
您可以使用 Data Factory 建立 Azure HDInsight 連結服務 tooregister HDInsight 叢集。

### <a name="example"></a>範例

```json
{
  "name": "HDInsightLinkedService",
  "properties": {
    "type": "HDInsight",
    "typeProperties": {
      "clusterUri": " https://<hdinsightclustername>.azurehdinsight.net/",
      "userName": "admin",
      "password": "<password>",
      "linkedServiceName": "MyHDInsightStoragelinkedService"
    }
  }
}
```

### <a name="properties"></a>屬性
| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| 類型 |hello 類型屬性應該設定太**HDInsight**。 |是 |
| clusterUri |hello hello HDInsight 叢集的 URI。 |是 |
| username |指定的 hello 使用者 toobe hello 名稱使用 tooconnect tooan 現有 HDInsight 叢集。 |是 |
| password |指定 hello 使用者帳戶的密碼。 |是 |
| linkedServiceName | Hello HDInsight 叢集供 hello 參照 toohello Azure blob 儲存體的 Azure 儲存體連結服務的名稱。 <p>目前，您無法針對此屬性指定 Azure Data Lake Store 連結服務。 如果 hello HDInsight 叢集已存取 toohello 資料湖存放區，您可能會從 Hive/Pig 指令碼來存取 hello Azure 資料湖存放區中的資料。 </p>  |是 |

## <a name="azure-batch-linked-service"></a>Azure Batch 連結服務
您可以建立 Azure 批次連結服務 tooregister 批次集區的虛擬機器 (Vm) tooa data factory。 您可以使用 Azure Batch 或 Azure HDInsight 執行 .NET 自訂活動。

請參閱下列主題，如果您是新 tooAzure 批次服務：

* [Azure 批次的基本概念](../batch/batch-technical-overview.md)hello Azure 批次服務的概觀。
* [新 AzureBatchAccount](https://msdn.microsoft.com/library/mt125880.aspx) cmdlet toocreate Azure Batch 帳戶 （或） [Azure 入口網站](../batch/batch-account-create-portal.md)toocreate hello Azure Batch 帳戶使用 Azure 入口網站。 請參閱[使用 PowerShell toomanage Azure Batch 帳戶](http://blogs.technet.com/b/windowshpc/archive/2014/10/28/using-azure-powershell-to-manage-azure-batch-account.aspx)主題，如需使用 hello cmdlet 的詳細指示。
* [新 AzureBatchPool](https://msdn.microsoft.com/library/mt125936.aspx) cmdlet toocreate Azure Batch 集區。

### <a name="example"></a>範例

```json
{
  "name": "AzureBatchLinkedService",
  "properties": {
    "type": "AzureBatch",
    "typeProperties": {
      "accountName": "<Azure Batch account name>",
      "accessKey": "<Azure Batch account key>",
      "poolName": "<Azure Batch pool name>",
      "linkedServiceName": "<Specify associated storage linked service reference here>"
    }
  }
}
```

附加"**。\<區域名稱\>**"toohello 您的批次帳戶名稱 hello **accountName**屬性。 範例：

```json
"accountName": "mybatchaccount.eastus"
```

另一個選項是 tooprovide hello batchUri 端點 hello 下列範例所示：

```json
"accountName": "adfteam",
"batchUri": "https://eastus.batch.azure.com",
```

### <a name="properties"></a>屬性
| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| 類型 |hello 類型屬性應該設定太**AzureBatch**。 |是 |
| accountName |Hello Azure Batch 帳戶的名稱。 |是 |
| accessKey |Hello Azure Batch 帳戶存取金鑰。 |是 |
| poolName |Hello 集區的虛擬機器名稱。 |是 |
| linkedServiceName |Hello 與此 Azure Batch 連結服務相關聯的 Azure 儲存體連結服務的名稱。 這項連結的服務用於暫存檔案需要 toorun hello 活動與 hello 活動執行記錄的儲存。 |是 |

## <a name="azure-machine-learning-linked-service"></a>Azure Machine Learning 連結服務
建立 Azure Machine Learning 連結服務 tooregister Machine Learning 批次計分端點 tooa 資料 factory。

### <a name="example"></a>範例

```json
{
  "name": "AzureMLLinkedService",
  "properties": {
    "type": "AzureML",
    "typeProperties": {
      "mlEndpoint": "https://[batch scoring endpoint]/jobs",
      "apiKey": "<apikey>"
    }
  }
}
```

### <a name="properties"></a>屬性
| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| 類型 |hello 類型屬性應該設定為： **AzureML**。 |是 |
| mlEndpoint |hello 批次評分 URL。 |是 |
| apiKey |hello 發行工作區模型的 API。 |是 |

## <a name="azure-data-lake-analytics-linked-service"></a>Azure Data Lake Analytics 連結服務
您建立**Azure Data Lake Analytics**連結服務 toolink Azure Data Lake Analytics 計算服務 tooan Azure data factory。 hello hello 管線中的資料 Lake Analytics U-SQL 活動指的是 toothis 連結服務。 

hello 下表提供說明 hello hello JSON 定義中使用的一般內容。 您可以在服務主體與使用者認證驗證之間進一步選擇。

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| **type** |hello 類型屬性應該設定為： **AzureDataLakeAnalytics**。 |是 |
| **accountName** |Azure Data Lake Analytics 帳戶名稱。 |是 |
| **dataLakeAnalyticsUri** |Azure Data Lake Analytics URI。 |否 |
| **subscriptionId** |Azure 訂用帳戶識別碼 |否 （如果未指定，訂用帳戶的資料處理站可用的 hello）。 |
| **resourceGroupName** |Azure 資源群組名稱 |否 （如果未指定，資源群組的資料處理站可用的 hello）。 |

### <a name="service-principal-authentication-recommended"></a>服務主體驗證 (建議)
服務主體驗證 toouse，註冊在 Azure Active Directory (Azure AD) 和授與它 hello 應用程式的實體存取 tooData 湖存放區。 如需詳細的步驟，請參閱[服務對服務驗證](../data-lake-store/data-lake-store-authenticate-using-active-directory.md)。 請記下的下列值，您使用的 hello toodefine hello 連結服務：
* 應用程式識別碼
* 應用程式金鑰 
* 租用戶識別碼

您可以使用服務主體的驗證方法是指定 hello 下列屬性：

| 屬性 | 說明 | 必要 |
|:--- |:--- |:--- |
| **servicePrincipalId** | 指定 hello 應用程式的用戶端識別碼。 | 是 |
| **servicePrincipalKey** | 指定 hello 應用程式的金鑰。 | 是 |
| **tenant** | 指定在您的應用程式所在的 hello 租用戶資訊 (網域名稱或租用戶 ID)。 您可以透過暫留在 hello 右上角的 hello Azure 入口網站中的 hello 滑鼠擷取它。 | 是 |

**範例：服務主體驗證**
```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "adftestaccount",
            "dataLakeAnalyticsUri": "datalakeanalyticscompute.net",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<optional, subscription id of ADLA>",
            "resourceGroupName": "<optional, resource group name of ADLA>"
        }
    }
}
```

### <a name="user-credential-authentication"></a>使用者認證驗證
或者，您可以使用使用者認證驗證的 Data Lake Analytics 藉由指定下列屬性的 hello:

| 屬性 | 說明 | 必要 |
|:--- |:--- |:--- |
| **authorization** | 按一下 hello**授權**按鈕 hello Data Factory 編輯器中，並輸入您 hello 自動產生的授權 URL toothis 屬性指派的認證。 | 是 |
| **sessionId** | 從 hello OAuth 授權工作階段的 OAuth 工作階段識別碼。 每個工作階段識別碼都是唯一的，只能使用一次。 當您使用 hello Data Factory 編輯器時，此設定會自動產生。 | 是 |

**範例：使用者認證授權**
```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "adftestaccount",
            "dataLakeAnalyticsUri": "datalakeanalyticscompute.net",
            "authorization": "<authcode>",
            "sessionId": "<session ID>", 
            "subscriptionId": "<optional, subscription id of ADLA>",
            "resourceGroupName": "<optional, resource group name of ADLA>"
        }
    }
}
```

#### <a name="token-expiration"></a>權杖到期
hello 您使用 hello 所產生的授權碼**授權**一段時間後到期 按鈕。 請參閱下表針對不同類型的使用者帳戶的 hello 逾期時間的 hello。 您可能會看到下列錯誤訊息的 hello 當 hello 驗證**權杖到期**： 認證作業發生錯誤： invalid_grant-AADSTS70002： 驗證認證時發生錯誤。 AADSTS70008: hello 提供存取權限已過期或撤銷。 追蹤識別碼：d18629e8-af88-43c5-88e3-d8419eb1fca1 相互關連識別碼：fac30a0c-6be6-4e02-8d69-a776d2ffefd7 時間戳記：2015-12-15 21:09:31Z

| 使用者類型 | 到期時間 |
|:--- |:--- |
| 不受 Azure Active Directory 管理的使用者帳戶 (@hotmail.com、@live.com 等) |12 小時 |
| 受 Azure Active Directory (AAD) 管理的使用者帳戶 |14 天之後 hello 最後一個配量執行。 <br/><br/>如果以 OAuth 式連結服務為基礎的配量至少每 14 天執行一次，則為 90 天。 |

tooavoid/解決這個錯誤，重新授權使用 hello**授權**按鈕時 hello**權杖到期**然後重新部署 hello 連結服務。 您也可以如下使用程式碼，以程式設計方式產生 **sessionId** 和 **authorization** 屬性的值：

```csharp
if (linkedService.Properties.TypeProperties is AzureDataLakeStoreLinkedService ||
    linkedService.Properties.TypeProperties is AzureDataLakeAnalyticsLinkedService)
{
    AuthorizationSessionGetResponse authorizationSession = this.Client.OAuth.Get(this.ResourceGroupName, this.DataFactoryName, linkedService.Properties.Type);

    WindowsFormsWebAuthenticationDialog authenticationDialog = new WindowsFormsWebAuthenticationDialog(null);
    string authorization = authenticationDialog.AuthenticateAAD(authorizationSession.AuthorizationSession.Endpoint, new Uri("urn:ietf:wg:oauth:2.0:oob"));

    AzureDataLakeStoreLinkedService azureDataLakeStoreProperties = linkedService.Properties.TypeProperties as AzureDataLakeStoreLinkedService;
    if (azureDataLakeStoreProperties != null)
    {
        azureDataLakeStoreProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeStoreProperties.Authorization = authorization;
    }

    AzureDataLakeAnalyticsLinkedService azureDataLakeAnalyticsProperties = linkedService.Properties.TypeProperties as AzureDataLakeAnalyticsLinkedService;
    if (azureDataLakeAnalyticsProperties != null)
    {
        azureDataLakeAnalyticsProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeAnalyticsProperties.Authorization = authorization;
    }
}
```

請參閱[AzureDataLakeStoreLinkedService 類別](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx)， [AzureDataLakeAnalyticsLinkedService 類別](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx)，和[AuthorizationSessionGetResponse 類別](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx)主題的詳細資訊關於 hello hello 程式碼中使用的 Data Factory 類別。 加入的參考： Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll hello WindowsFormsWebAuthenticationDialog 類別。 

## <a name="azure-sql-linked-service"></a>Azure SQL 連結服務
您建立 Azure SQL 連結服務，並使用它搭配 hello[預存程序活動](data-factory-stored-proc-activity.md)tooinvoke 從 Data Factory 管線的預存程序。 如需此連結服務的詳細資料，請參閱 [Azure SQL 連接器](data-factory-azure-sql-connector.md#linked-service-properties) 一文。

## <a name="azure-sql-data-warehouse-linked-service"></a>Azure SQL 資料倉儲連結服務
您建立連結的 Azure SQL 資料倉儲服務，並使用它搭配 hello[預存程序活動](data-factory-stored-proc-activity.md)tooinvoke 從 Data Factory 管線的預存程序。 如需此連結服務的詳細資料，請參閱 [Azure SQL 資料倉儲連接器](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) 一文。

## <a name="sql-server-linked-service"></a>SQL Server 連結服務
建立連結的 SQL Server 服務，並使用以 hello[預存程序活動](data-factory-stored-proc-activity.md)tooinvoke 從 Data Factory 管線的預存程序。 如需此連結服務的詳細資料，請參閱 [SQL Server 連接器](data-factory-sqlserver-connector.md#linked-service-properties) 一文。

