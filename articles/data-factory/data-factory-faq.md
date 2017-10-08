---
title: "aaaAzure Data Factory-常見問題集"
description: "關於 Azure Data Factory 的常見問題。"
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 532dec5a-7261-4770-8f54-bfe527918058
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: 78289fb4b6e15d74772af6c71ec25c7d2ca1a0bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---frequently-asked-questions"></a>Azure 資料處理站-常見問題集
## <a name="general-questions"></a>一般問題
### <a name="what-is-azure-data-factory"></a>Azure 資料處理站是什麼？
Data Factory 是以雲端為基礎的資料整合服務， **hello 移動和轉換資料會自動執行**。 就像處理站執行設備 tootake 原料，並將它們轉換成已完成的貨物，Data Factory 會協調現有的服務來收集未經處理資料，並將它轉換為已備妥要使用的資訊。

Data Factory 可讓您在內部部署和雲端資料存放區以及使用 Azure HDInsight 等 Azure Data Lake Analytics 計算服務的程序/轉換資料之間的 toocreate 資料驅動型工作流程 toomove 資料。 建立管線，以執行您所需要的 hello 動作之後，您可以將它排程 toorun 定期 （每小時、 每天、 每週等）。   

如需詳細資訊，請參閱[概觀與重要概念](data-factory-introduction.md)。

### <a name="where-can-i-find-pricing-details-for-azure-data-factory"></a>哪裡可以找到 Azure 資料處理站的定價詳細資料？
請參閱[資料 Factory 定價詳細資料頁面][ adf-pricing-details] hello 定價 hello Azure Data Factory 的詳細資料。  

### <a name="how-do-i-get-started-with-azure-data-factory"></a>如何開始使用 Azure Data Factory？
* 如需 Azure Data Factory 的概觀，請參閱[簡介 tooAzure Data Factory](data-factory-introduction.md)。
* 如需如何太**複製/移動資料**使用複製活動，請參閱[將資料從 Azure Blob 儲存體 tooAzure SQL Database 複製](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。
* 如需如何太**轉換資料**使用 HDInsight Hive 活動。 請參閱 [在 Hadoop 叢集上執行 Hive 指令碼來處理資料](data-factory-build-your-first-pipeline.md)

### <a name="what-is-hello-data-factorys-region-availability"></a>Hello Data Factory 的區域可用性是什麼？
Data Factory 可在**美國西部**和**北歐**地區使用。 hello 計算和資料處理站所使用的儲存體服務可位於其他區域。 請參閱 [支援的區域](data-factory-introduction.md#supported-regions)。

### <a name="what-are-hello-limits-on-number-of-data-factoriespipelinesactivitiesdatasets"></a>Hello 限制數目的資料處理站/管線/活動/資料集上有哪些？
請參閱**Azure 資料 Factory 限制**區段 hello [Azure 訂用帳戶和服務限制、 配額和條件約束](../azure-subscription-service-limits.md#data-factory-limits)發行項。

### <a name="what-is-hello-authoringdeveloper-experience-with-azure-data-factory-service"></a>什麼是 Azure Data Factory 服務的 hello 撰寫/開發人員經驗？
您可以撰寫/建立 data factory 使用其中一種下列 Sdk 工具/hello:

* **Azure 入口網站**hello Azure 入口網站中的 hello Data Factory 刀鋒提供豐富的使用者介面的 toocreate 資料 factory ad 連結服務。 hello **Data Factory 編輯器**，這也是 hello 入口網站的一部分，可讓您藉由指定這些成品的 JSON 定義 tooeasily 建立連結的服務、 資料表、 資料集和管線。 請參閱[建置您使用 Azure 入口網站的第一個資料管線](data-factory-build-your-first-pipeline-using-editor.md)hello 入口網站/編輯器 toocreate 使用的範例，以及部署 data factory。
* **Visual Studio**您可以使用 Visual Studio toocreate Azure data factory。 如需詳細資料，請參閱 [使用 Visual Studio 建置您的第一個資料管線](data-factory-build-your-first-pipeline-using-vs.md) 。
* **Azure PowerShell** 如需使用 PowerShell 來建立 Data Factory 的教學課程/逐步解說，請參閱 [使用 Azure PowerShell 建立和監視 Azure Data Factory](data-factory-build-your-first-pipeline-using-powershell.md) 。 如需 Data Factory Cmdlet 的完整文件，請參閱 MSDN Library 上的 [Data Factory Cmdlet 參考][adf-powershell-reference]內容。
* **.NET 類別庫** 您可以使用 Data Factory .NET SDK，透過程式設計方式建立 Data Factory。 如需使用 .NET SDK 建立 Data Factory 的逐步解說，請參閱 [使用 .NET SDK 建立、監視和管理 Data Factory](data-factory-create-data-factories-programmatically.md) 。 如需 Data Factory .NET SDK 的完整文件，請參閱 [Data Factory 類別庫參考][msdn-class-library-reference]。
* **REST API**您也可以使用 hello hello Azure Data Factory 服務 toocreate 所公開的 REST API 和部署資料處理站。 如需 Data Factory REST API 的完整文件，請參閱 [Data Factory REST API 參考][msdn-rest-api-reference]。
* **Azure Resource Manager 範本** 請參閱 [教學課程：使用 Azure Resource Manager 範本建置您的第一個 Azure Data Factory](data-factory-build-your-first-pipeline-using-arm.md) 以取得詳細資訊。

### <a name="can-i-rename-a-data-factory"></a>我是否可以重新命名資料處理站？
否。 如同其他 Azure 資源，就無法變更 hello Azure data factory 名稱。

### <a name="can-i-move-a-data-factory-from-one-azure-subscription-tooanother"></a>可以從一個 Azure 訂用帳戶 tooanother 移動 data factory 嗎？
是。 使用 hello**移動**hello 下列圖表所示，您的資料處理站刀鋒視窗上按鈕：

![移動 Data Factory](media/data-factory-faq/move-data-factory.png)

### <a name="what-are-hello-compute-environments-supported-by-data-factory"></a>支援的 Data Factory 的 hello 計算環境有哪些？
hello 下表提供支援的 Data Factory 和 hello 的活動可以在其上執行的運算環境的清單。

| 計算環境 | 活動 |
| --- | --- |
| [隨選 HDInsight 叢集](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service)或[您自己的 HDInsight 叢集](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) |[DotNet](data-factory-use-custom-activities.md)、[Hive](data-factory-hive-activity.md)、[Pig](data-factory-pig-activity.md)、[MapReduce](data-factory-map-reduce.md)、[Hadoop 串流](data-factory-hadoop-streaming-activity.md) |
| [Azure Batch](data-factory-compute-linked-services.md#azure-batch-linked-service) |[DotNet](data-factory-use-custom-activities.md) |
| [Azure Machine Learning](data-factory-compute-linked-services.md#azure-machine-learning-linked-service) |[Machine Learning 活動︰批次執行和更新資源](data-factory-azure-ml-batch-execution-activity.md) |
| [Azure Data Lake Analytics](data-factory-compute-linked-services.md#azure-data-lake-analytics-linked-service) |[Data Lake Analytics U-SQL](data-factory-usql-activity.md) |
| [Azure SQL](data-factory-compute-linked-services.md#azure-sql-linked-service)、[Azure SQL 資料倉儲](data-factory-compute-linked-services.md#azure-sql-data-warehouse-linked-service)、[SQL Server](data-factory-compute-linked-services.md#sql-server-linked-service) |[預存程序](data-factory-stored-proc-activity.md) |

### <a name="how-does-azure-data-factory-compare-with-sql-server-integration-services-ssis"></a>Azure Data Factory 相較於 SQL Server Integration Services (SSIS) 有何異同？ 
請參閱 hello [vs Azure Data Factory。SSIS 的比較 (英文)](http://www.sqlbits.com/Sessions/Event15/Azure_Data_Factory_vs_SSIS)。 某些 hello Data Factory 中最近的變更可能不會列在 hello powerpoint 投影片中。 我們會持續新增更多的功能 tooAzure Data Factory。 我們會持續新增更多的功能 tooAzure Data Factory。 我們將會併入這些更新的資料整合技術，來自 Microsoft 的 hello 比較今年一段時間。   

## <a name="activities---faq"></a>活動 - 常見問題集
### <a name="what-are-hello-different-types-of-activities-you-can-use-in-a-data-factory-pipeline"></a>Hello 不同類型的活動，您可以使用 Data Factory 管線中有哪些？
* [資料移動活動](data-factory-data-movement-activities.md)toomove 資料。
* [資料轉換活動](data-factory-data-transformation-activities.md)tooprocess/轉換資料。

### <a name="when-does-an-activity-run"></a>何時執行活動？
hello**可用性**hello 中的組態設定輸出資料表格決定 hello 活動執行時。 如果未指定輸入資料集，hello 活動會檢查是否可滿足所有 hello 輸入的資料的相依性 (也就是**準備**狀態) 開始執行之前。

## <a name="copy-activity---faq"></a>複製活動 - 常見問題集
### <a name="is-it-better-toohave-a-pipeline-with-multiple-activities-or-a-separate-pipeline-for-each-activity"></a>它是較佳 toohave 具有多個活動的管線或不同的管線的每個活動嗎？
管線應該 toobundle 相關活動。 如果 hello 管線外的任何其他活動不到連接它們的 hello 資料集，則可以在一個管保留 hello 活動。 如此一來，您不需要 toochain 管線作用期，讓它們彼此對齊。 此外，更新 hello 管線時，會進一步保留 hello hello 資料表內部 toohello 管線中的資料完整性。 管線更新基本上停止 hello 管線中的所有 hello 活動，並移除並重新建立它們。 從撰寫觀點來看，它可能也會更容易 toosee hello 資料流程內 hello 相關的活動，在一個 JSON 檔案 hello 管線。

### <a name="what-are-hello-supported-data-stores"></a>什麼是 hello 支援資料存放區？
Data Factory 中的複製活動會將資料從來源資料存放區 tooa 接收資料存放區。 Data Factory 支援下列資料存放區的 hello。 從任何來源的資料可以寫入 tooany 接收。 按一下 資料存放區 toolearn 如何 toocopy 資料 tooand 從該存放區。

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

> [!NOTE]
> 資料存放區使用 * 可在內部部署或 Azure IaaS 上，因此需要您 tooinstall[資料管理閘道器](data-factory-data-management-gateway.md)在內部部署/Azure IaaS 電腦上。

### <a name="what-are-hello-supported-file-formats"></a>什麼是 hello 支援的檔案格式？
[!INCLUDE [data-factory-file-format](../../includes/data-factory-file-format.md)]

### <a name="where-is-hello-copy-operation-performed"></a>Hello 複製作業在執行？
如需詳細資料，請參閱 [全域可用的資料移動](data-factory-data-movement-activities.md#global) 一節。 簡單地說，如果包含在內部部署資料存放區，hello 複製作業是由 hello 資料管理閘道器在內部部署環境中執行。 與兩個 cloud 商店之間 hello 資料移動時，會在 hello 區域最接近 toohello 接收位置在 hello 執行 hello 複製作業相同的地理位置。

## <a name="hdinsight-activity---faq"></a>HDInsight 活動 - 常見問題集
### <a name="what-regions-are-supported-by-hdinsight"></a>HDInsight 支援哪些區域？
請參閱 hello hello 下列文章中的各地區上市區段： 或[HDInsight 定價詳細資料][hdinsight-supported-regions]。

### <a name="what-region-is-used-by-an-on-demand-hdinsight-cluster"></a>隨選 HDInsight 叢集使用哪一個區域？
hello 隨選 HDInsight 叢集建立在 hello 相同 hello 指定 toobe hello 叢集搭配使用的儲存體所在的區域。    

### <a name="how-tooassociate-additional-storage-accounts-tooyour-hdinsight-cluster"></a>如何 tooassociate 額外的儲存體帳戶 tooyour HDInsight 叢集嗎？
如果您使用您自己的 HDInsight 叢集 (BYOC-攜帶您自己的叢集)，請參閱下列主題中的 hello:

* [搭配使用 HDInsight 叢集與替代儲存體帳戶和中繼存放區][hdinsight-alternate-storage]
* [搭配使用其他儲存體帳戶與 HDInsight Hive][hdinsight-alternate-storage-2]

如果您使用隨叢集所建立的 hello Data Factory 服務，指定額外的儲存體帳戶的 hello HDInsight 連結服務，以便 hello Data Factory 服務可以代表您註冊它們。 在 hello hello 視連結服務的 JSON 定義中，使用**additionalLinkedServiceNames**屬性 toospecify 替代儲存體帳戶中 hello 下列 JSON 片段所示：

```JSON
{
    "name": "MyHDInsightOnDemandLinkedService",
    "properties":
    {
        "type": "HDInsightOnDemandLinkedService",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "linkedServiceName": "LinkedService-SampleData",
            "additionalLinkedServiceNames": [ "otherLinkedServiceName1", "otherLinkedServiceName2" ]
        }
    }
}
```
在 hello 上述範例中，otherLinkedServiceName1 和 otherLinkedServiceName2 表示連結的服務，其定義包含 hello HDInsight 叢集的需求 tooaccess 替代儲存體帳戶的認證。

## <a name="slices---faq"></a>配量 - 常見問題集
### <a name="why-are-my-input-slices-not-in-ready-state"></a>為什麼我的輸入配量不是處於「就緒」狀態？
常見的錯誤不設定**外部**屬性太**true** hello hello 輸入資料時，輸入資料集是外部 toohello 資料處理站 （未 hello 資料處理站所產生）。

在下列範例的 hello，因此您只需要 tooset**外部**上的 tootrue **dataset1**。  

**DataFactory1** Pipeline 1: dataset1 -> activity1 -> dataset2 -> activity2 -> dataset3 Pipeline 2: dataset3-> activity3 -> dataset4

如果您有與管線採用 dataset4 （管線 1 的 data factory 中的 2 所產生） 的另一個資料處理站時，將 dataset4 標示為外部資料集因為 hello 資料集由不同的資料處理站產生 （DataFactory1、 不 DataFactory2）。  

**DataFactory2**    
Pipeline 1: dataset4->activity4->dataset5

如果 hello 外部屬性的設定正確，請確認 hello 輸入的資料是否存在於 hello hello 輸入資料集定義中指定的位置。

### <a name="how-toorun-a-slice-at-another-time-than-midnight-when-hello-slice-is-being-produced-daily"></a>如何在其他時間比午夜當 hello 配量每天產生配量 toorun 嗎？
使用 hello**位移**想 hello 配量 toobe 屬性 toospecify hello 時間所產生。 如需有關此屬性的詳細資料，請參閱 [資料集可用性](data-factory-create-datasets.md#dataset-availability) 一節。 以下是一個簡短的範例：

```json
"availability":
{
    "frequency": "Day",
    "interval": 1,
    "offset": "06:00:00"
}
```
每日的配量開始**上午 6 點**而不是 hello 預設午夜。     

### <a name="how-can-i-rerun-a-slice"></a>如何重新執行配量？
您可以重新執行配量 hello 下列方式之一：

* 使用監視和管理應用程式 toorerun 活動視窗或配量。 如需相關指示，請參閱 [重新執行已選取的活動時段](data-factory-monitor-manage-app.md#perform-batch-actions) 。   
* 按一下**執行**hello 命令列上 hello**資料配量**hello Azure 入口網站中的 hello 配量的刀鋒視窗。
* 執行**組 AzureRmDataFactorySliceStatus**狀態的 cmdlet 設定得**等候**hello 配量。   

    ```PowerShell
    Set-AzureRmDataFactorySliceStatus -Status Waiting -ResourceGroupName $ResourceGroup -DataFactoryName $df -TableName $table -StartDateTime "02/26/2015 19:00:00" -EndDateTime "02/26/2015 20:00:00"
    ```
請參閱[組 AzureRmDataFactorySliceStatus] [ set-azure-datafactory-slice-status] hello cmdlet 的詳細資料。

### <a name="how-long-did-it-take-tooprocess-a-slice"></a>時間長度沒有花費 tooprocess 配量？
您可以使用活動 Windows 檔案總管 中監視和管理 App tooknow 多久花費 tooprocess 資料配量。 如需詳細資料，請參閱 [活動時段總管](data-factory-monitor-manage-app.md#activity-window-explorer) 。

您也可以執行下列 hello Azure 入口網站中的 hello:  

1. 按一下**資料集**磚 hello **DATA FACTORY** data factory 的刀鋒視窗。
2. 按一下特定的資料集 hello 上 hello**資料集**刀鋒視窗。
3. 選取 hello 配量您感興趣的 hello**最近配量**清單上 hello**資料表**刀鋒視窗。
4. 按一下從 hello 執行 hello 活動**活動執行**清單上 hello**資料配量**刀鋒視窗。
5. 按一下**屬性**磚 hello**活動執行詳細資料**刀鋒視窗。
6. 您應該會看見 hello**持續時間**欄位的值。 此值為 hello 時間 tooprocess hello 配量。   

### <a name="how-toostop-a-running-slice"></a>如何執行配量 toostop 嗎？
如果您需要 toostop hello 管線執行時，您可以使用[暫停 AzureRmDataFactoryPipeline](/powershell/module/azurerm.datafactories/suspend-azurermdatafactorypipeline) cmdlet。 目前，暫停 hello 管線不會停止進行中的 hello 配量執行。 完成 hello 進行中執行時，任何額外的配量所不挑選。

如果您真的想 toostop 所有 hello 執行立即，hello 方式只會 toodelete hello 管線，再重新建立。 如果您選擇 toodelete hello 管線，您不需要 toodelete 資料表及連結的 hello 管線所使用的服務。

[create-factory-using-dotnet-sdk]: data-factory-create-data-factories-programmatically.md
[msdn-class-library-reference]: /dotnet/api/microsoft.azure.management.datafactories.models
[msdn-rest-api-reference]: /rest/api/datafactory/

[adf-powershell-reference]: /powershell/resourcemanager/azurerm.datafactories/v2.3.0/azurerm.datafactories
[azure-portal]: http://portal.azure.com
[set-azure-datafactory-slice-status]: /powershell/resourcemanager/azurerm.datafactories/v2.3.0/set-azurermdatafactoryslicestatus

[adf-pricing-details]: http://go.microsoft.com/fwlink/?LinkId=517777
[hdinsight-supported-regions]: http://azure.microsoft.com/pricing/details/hdinsight/
[hdinsight-alternate-storage]: http://social.technet.microsoft.com/wiki/contents/articles/23256.using-an-hdinsight-cluster-with-alternate-storage-accounts-and-metastores.aspx
[hdinsight-alternate-storage-2]: http://blogs.msdn.com/b/cindygross/archive/2014/05/05/use-additional-storage-accounts-with-hdinsight-hive.aspx
