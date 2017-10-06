---
title: "aaaAzure Data Factory-範例"
description: "提供有關所附範例的詳細資料以 hello Azure Data Factory 服務。"
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: c0538b90-2695-4c4c-a6c8-82f59111f4ab
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: aa1c15eca21b34b7bcc64358b685d7606baaf691
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---samples"></a>Azure Data Factory - 範例
## <a name="samples-on-github"></a>GitHub 上的範例
hello [GitHub Azure DataFactory 儲存機制](https://github.com/azure/azure-datafactory)包含數個範例，協助您快速逐漸增加的 Azure Data Factory 服務 （或） 修改 hello 指令碼，並使用它自己的應用程式中。 hello Samples\JSON 資料夾含有常見案例的 JSON 片段。

| 範例 | 說明 |
|:--- |:--- |
| [ADF 逐步解說](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFWalkthrough) |此範例提供端對端逐步解說處理使用 tooinsights 中的記錄檔中的 Azure Data Factory tooturn 資料的記錄檔。 <br/><br/>在本逐步解說，hello Data Factory 管線收集範例記錄檔，處理程序和豐富 hello 資料從記錄檔與參考資料，並將轉換 hello 資料 tooevaluate hello 效益最近啟動的行銷活動。 |
| [JSON 範例](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/JSON) |此範例提供常見案例的 JSON 範例。 |
| [Http 資料下載程式範例](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/HttpDataDownloaderSample) |這個範例來自 HTTP 端點 tooAzure Blob 儲存體的資料的 showcases 下載使用自訂.NET 活動。 |
| [跨 AppDomain .NET 活動範例](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) |這個範例可讓您自訂的.NET 活動不是，限制 hello ADF 啟動器 （例如，WindowsAzure.Storage v4.3.0、 Newtonsoft.Json v6.0.x 等） 所使用的 tooassembly 版本 tooauthor。 |
| [執行 R 指令碼](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample) |此範例包含 hello Data Factory 自訂活動可以使用的 tooinvoke RScript.exe。 此範例只能與您自己的 (非隨選) 且已安裝 R 的 HDInsight 叢集搭配運作。 |
| [在 HDInsight Hadoop 叢集上叫用 Spark 作業](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/Spark) |這個範例示範如何 toouse MapReduce 活動 tooinvoke Spark 程式。 hello spark 程式只會從一個 Azure Blob 容器 tooanother 複製資料。 |
| [使用 Azure Machine Learning 批次評分活動進行的 Twitter 分析](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TwitterAnalysisSample-AzureMLBatchScoringActivity) |這個範例示範如何 toouse AzureMLBatchScoringActivity tooinvoke Azure 機器學習模型，執行 twitter 情緒分析，計分，預測等。 |
| [使用自訂活動進行的 Twitter 分析](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TwitterAnalysisSample-CustomC%23Activity) |這個範例會示範如何自訂.NET 活動 tooinvoke 執行 Azure Machine Learning 模型 toouse twitter 情緒分析，計分，預測等。 |
| [Azure Machine Learning 的參數化管線](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ParameterizedPipelinesForAzureML/) |hello 範例提供端對端 C# 程式碼 toodeploy N 管線進行評分，及重新訓練各有不同的區域參數，其中地區 hello 清單來自 parameters.txt 檔案，也就是包含在此範例。 |
| [Azure 串流分析作業的參考資料重新整理](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ReferenceDataRefreshForASAJobs) |這個範例會示範如何以參考資料和安裝程式 hello 的 toouse Azure Data Factory 和 Azure Stream Analytics 一起 toorun hello 查詢重新整理排程的參考資料。 |
| [搭配內部部署 Hortonworks Hadoop 的混合式管線](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/HybridPipelineWithOnPremisesHortonworksHadoop) |hello 範例會使用 Data Factory 中執行作業，就像您可以加入其他計算目標，像是在 HDInsight 基礎雲端中的 Hadoop 叢集做為計算目標的內部部署 Hadoop 叢集。 |
| [JSON 轉換工具](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/JSONConversionTool) |此工具可讓您從先前 too2015-07-01-預覽 toolatest 版本或 2015年-07-01-預覽 （預設值） tooconvert Json。 |
| [U-SQL 範例輸入檔](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/U-SQL%20Sample%20Input%20File) |此檔案是 U-SQL 活動所使用的範例檔案。 |
| [刪除 blob 檔案](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/DeleteBlobFileFolderCustomActivity) | 此範例會示範 C# 檔案中，一旦 hello 檔案已複製可以作為檔案的一部分 ADF 自訂.net 活動 toodelete hello 來源 Azure Blob 的位置。|

## <a name="azure-resource-manager-templates"></a>Azure 資源管理員範本
您可以找到下列 Data factory 的 Azure 資源管理員範本，在 GitHub 上的 hello。

| 範本 | 說明 |
| --- | --- |
| [從 Azure Blob 儲存體 tooAzure SQL Database 複製](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-blob-to-sql-copy) |部署此範本建立 Azure data factory 管線，將資料從 hello 指定 Azure blob 儲存體 toohello Azure SQL database |
| [從 Salesforce tooAzure Blob 儲存體複製](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-salesforce-to-blob-copy) |部署此範本建立 Azure data factory 管線，將資料從 hello 指定 Salesforce toohello Azure blob 儲存體帳戶。 |
| [在 Azure HDInsight 叢集上執行 Hive 指令碼來轉換資料](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-hive-transformation) |部署此範本建立 Azure data factory 管線，在 Azure HDInsight Hadoop 叢集上執行 hello 範例 Hive 指令碼來轉換資料。 |

## <a name="samples-in-azure-portal"></a>Azure 入口網站中的範例
您可以使用 hello**範例管線**tooyour data factory 中您的資料處理站 toodeploy 範例管線和其相關聯的實體 （資料集和連結的服務） 的 hello 首頁上並排顯示。

1. 建立 Data Factory 或開啟現有的 Data Factory。 請參閱[從 Blob 儲存體 tooSQL 資料庫使用 Data Factory 複製資料](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)如步驟 toocreate data factory。
2. 在 hello **DATA FACTORY** hello data factory，刀鋒視窗中按一下 hello**範例管線**磚。

    ![範例管線圖格](./media/data-factory-samples/SamplePipelinesTile.png)
3. 在 hello**範例管線**刀鋒視窗中，按一下 hello**範例**想 toodeploy。

    ![範例管線刀鋒視窗](./media/data-factory-samples/SampleTile.png)
4. 指定 hello 範例的組態設定。 例如，您的 Azure 儲存體帳戶名稱和帳戶金鑰、Azure SQL 伺服器名稱、資料庫、使用者 ID 和密碼等。

    ![範例刀鋒視窗](./media/data-factory-samples/SampleBlade.png)
5. 您指定 hello 組態設定完成之後，請按一下**建立**toocreate/部署 hello 範例管線與連結的服務/資料表 hello 管線所使用。
6. 您會看到部署的 hello 狀態 hello 範例磚，在您按一下先前 hello**範例管線**刀鋒視窗。

    ![部署狀態](./media/data-factory-samples/DeploymentStatus.png)
7. 當您看到 hello**部署成功**hello 磚 hello 範例中，關閉 hello 訊息**範例管線**刀鋒視窗。  
8. 在**DATA FACTORY**您刀鋒視窗中，查看已連結的服務、 資料集和管線新增 tooyour 資料 factory。  

    ![Data Factory 刀鋒視窗](./media/data-factory-samples/DataFactoryBladeAfter.png)

## <a name="samples-in-visual-studio"></a>Visual Studio 中的範例
### <a name="prerequisites"></a>必要條件
您必須擁有您電腦上安裝的 hello 下列：

* Visual Studio 2013 或 Visual Studio 2015
* 下載 Azure SDK for Visual Studio 2013 或 Visual Studio 2015。 瀏覽過[Azure 下載頁面](https://azure.microsoft.com/downloads/)按一下**VS 2013**或**VS 2015**在 hello **.NET** > 一節。
* 下載最新 Azure Data Factory 外掛程式 hello for Visual Studio: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5)或[VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005)。 如果您使用 Visual Studio 2013，則您也可以執行下列步驟的 hello 更新 hello 外掛程式： hello 功能表上，按一下**工具** -> **擴充功能和更新** ->  **線上** -> **Visual Studio 組件庫** -> **Microsoft Azure Data Factory Tools for Visual Studio**  ->  **更新**。

### <a name="use-data-factory-templates"></a>使用 Data Factory 範本
1. 按一下**檔案**hello 功能表上，指向 太**新增**，然後按一下**專案**。
2. 在 hello**新專案**對話方塊方塊中，執行下列步驟 hello:

   1. 在 [範本] 底下選取 [DataFactory]。
   2. 選取**資料 Factory 範本**hello 右窗格中。
   3. 輸入**名稱**hello 專案。
   4. 選取**位置**hello 專案。
   5. 按一下 [確定] 。

      ![[新增專案] 對話方塊](./media/data-factory-samples/vs-new-project-adf-templates.png)
3. 在 hello**資料 Factory 範本**對話方塊中，選取 hello 範例範本從 hello**使用案例範本**區段，然後按一下 **下一步**。 hello 下列步驟逐步引導您完成使用 hello**客戶程式碼剖析**範本。 步驟均相似的 hello 其他範例。

    ![Data Factory 範本對話方塊](./media/data-factory-samples/vs-data-factory-templates-dialog.png)
4. 在 hello**資料處理站組態**] 對話方塊中，按一下 [**下一步**上 hello**資料處理站的基本概念**頁面。
5. 在 hello**設定資料 factory**頁面上，執行下列步驟 hello:
   1. 選取 [建立新的 Data Factory]。 您也可以選取 [使用現有的 Data Factory] 。
   2. 輸入**名稱**hello data factory。
   3. 選取 hello **Azure 訂用帳戶**中您要建立 hello 資料 factory toobe。
   4. 選取 hello**資源群組**hello data factory。
   5. 選取 hello**美國西部**，**美國東部**，或**北歐**hello**區域**。
   6. 按一下 [下一步] 。
6. 在 hello**設定資料存放區**頁面上，指定現有**Azure SQL database**和**Azure 儲存體帳戶**（或） 建立資料庫/儲存體，並按一下 下一步。
7. 在 hello**設定計算**頁面上，選取預設值，然後按一下**下一步**。
8. 在 hello**摘要**頁面上，檢閱所有設定，然後按一下**下一步**。
9. 在 hello**部署狀態**頁面上，等候完成 hello 部署，然後按一下**完成**。
10. 以滑鼠右鍵按一下專案 hello 方案總管] 中的，按一下 [**發行**。
11. 如果您看到**登入 Microsoft 帳戶 tooyour**對話方塊中，hello 擁有帳戶的 Azure 訂用帳戶中，輸入您的認證，然後按一下**登入**。
12. 您應該會看到下列對話方塊中的 hello:

    ![發佈對話方塊](./media/data-factory-build-your-first-pipeline-using-vs/publish.png)
13. 在 hello**設定資料 factory**頁面上，執行下列步驟 hello:

    1. 確認 [使用現有的 Data Factory]  選項。
    2. 選取 hello**資料 factory**使用 hello 範本時，已選取。
    3. 按一下**下一步**tooswitch toohello**發行的項目**頁面。 (按 **索引標籤**超出 hello 名稱欄位 tooif hello toomove**下一步**按鈕已停用。)
14. 在 [hello**發行的項目**頁面上，確定所有 hello Data Factory 實體已選取，然後按一下**下一步]** tooswitch toohello**摘要**頁面。     
15. 檢閱 hello 摘要，然後按一下**下一步**toostart hello 部署程序和檢視 hello**部署狀態**。
16. 在 [hello**部署狀態**] 頁面上，您應該會看到 hello hello 部署程序的狀態。 Hello 部署完成之後，請按一下 [完成]。

請參閱[建置您第一次的資料處理站 (Visual Studio)](data-factory-build-your-first-pipeline-using-vs.md)如需使用 Visual Studio tooauthor Data Factory 實體，然後發行 tooAzure 詳細資料。          
