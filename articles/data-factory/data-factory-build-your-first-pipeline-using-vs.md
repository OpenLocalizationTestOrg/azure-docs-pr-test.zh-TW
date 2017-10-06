---
title: "aaaBuild 您第一次的 data factory (Visual Studio) |Microsoft 文件"
description: "在本教學課程中，您會使用 Visual Studio，建立範例 Azure Data Factory 管線。"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 7398c0c9-7a03-4628-94b3-f2aaef4a72c5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 0c5eb01b685d978d80916da0293cc2d3701b2d57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-data-factory-by-using-visual-studio"></a>教學課程：使用 Visual Studio 建立資料處理站
> [!div class="op_single_selector" title="Tools/SDKs"]
> * [概觀和必要條件](data-factory-build-your-first-pipeline.md)
> * [Azure 入口網站](data-factory-build-your-first-pipeline-using-editor.md)
> * [Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
> * [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
> * [Resource Manager 範本](data-factory-build-your-first-pipeline-using-arm.md)
> * [REST API](data-factory-build-your-first-pipeline-using-rest-api.md)

本教學課程示範如何使用 Visual Studio Azure data factory toocreate。 您建立使用 hello Data Factory 的專案範本的 Visual Studio 專案、 定義以 JSON 格式的 Data Factory 實體 （連結的服務、 資料集和管線），然後發行/部署這些實體 toohello 雲端。 

在此教學課程中的 hello 管線有一個活動： **HDInsight Hive 活動**。 此活動會在轉換輸入資料 tooproduce 輸出資料的 Azure HDInsight 叢集上執行 hive 指令碼。 hello 管線是排程的 toorun，每個月之間 hello 指定開始和結束時間之後。 

> [!NOTE]
> 本教學課程不會顯示如何使用 Azure Data Factory 複製資料。 如需如何使用 Azure Data Factory，toocopy 資料，請參閱[教學課程： 將資料從 Blob 儲存體 tooSQL 資料庫複製](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。
> 
> 一個管線中可以有多個活動。 此外，您可以藉由設定 hello 輸出資料集的一個活動 hello 的輸入資料集的 hello 其他活動鏈結 （執行一個活動執行另一個之後） 的兩個活動。 如需詳細資訊，請參閱 [Data Factory 排程和執行](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline)。


## <a name="walkthrough-create-and-publish-data-factory-entities"></a>逐步解說︰建立和發佈 Data Factory 實體
以下是您執行此逐步解說中的 hello 步驟：

1. 建立兩個連結服務：**AzureStorageLinkedService1** 和 **HDInsightOnDemandLinkedService1**。 
   
    在本教學課程中，輸入和輸出資料中的 hello hive 活動 hello 相同的 Azure Blob 儲存體。 您使用隨 HDInsight 叢集 tooprocess 現有輸入的資料 tooproduce 輸出的資料。 hello 隨選 HDInsight 叢集會自動為您建立 Azure Data factory 在 hello 輸入的資料時處理的準備 toobe 的執行階段。 您需要的 toolink 儲存您的資料，或計算 tooyour 資料處理站，以便讓 hello Data Factory 服務可以連線 toothem 在執行階段。 因此，您會使用 hello AzureStorageLinkedService1，連結您的 Azure 儲存體帳戶 toohello data factory，並且使用 hello HDInsightOnDemandLinkedService1 連結隨選 HDInsight 叢集。 發行時，您可以指定建立 hello 資料 factory toobe hello 名稱或現有的 data factory。  
2. 建立兩個資料集： **InputDataset**和**OutputDataset**，代表儲存在 hello Azure blob 儲存體中的 hello 輸入/輸出資料。 
   
    這些資料集定義，請參閱您在 hello 上一個步驟中建立的 toohello Azure 儲存體連結的服務。 Hello InputDataset，您可以指定 hello blob 容器 (adfgetstarted)，然後 hello 所在的資料夾 (inptutdata) hello 輸入資料的 blob。 Hello OutputDataset，您會指定 hello blob 容器 (adfgetstarted) 和 hello 資料夾 (partitioneddata)，其中保存 hello 輸出資料。 您也會指定其他屬性，例如結構、可用性和原則。
3. 建立名為 **MyFirstPipeline** 的管線。 
  
    在本逐步解說，hello 管線有一個活動： **HDInsight Hive 活動**。 這個活動轉換輸入資料 tooproduce 輸出資料的隨選 HDInsight 叢集上執行 hive 指令碼。 toolearn hive 活動詳細資料請參閱[Hive 活動](data-factory-hive-activity.md) 
4. 建立名為 **DataFactoryUsingVS** 的資料處理站。 部署 hello data factory 和所有的 Data Factory 實體 （連結的服務、 表格和 hello 管線）。
5. 發行之後，您可以使用 Azure 入口網站的刀鋒視窗，並監視和管理 App toomonitor hello 管線。 
  
### <a name="prerequisites"></a>必要條件
1. 閱讀[教學課程概觀](data-factory-build-your-first-pipeline.md)文件，以及完成 hello**必要條件**步驟。 您也可以選取 hello**概觀和必要條件**hello 頂端 tooswitch toohello 文 hello 下拉式清單中的選項。 完成 hello 必要條件之後，回復 toothis 文章選取切換**Visual Studio** hello 下拉式清單中的選項。
2. toocreate Data Factory 執行個體，您必須是成員的 hello[資料 Factory 參與者](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor)hello 訂用帳戶/資源群組層級角色。  
3. 您必須擁有您電腦上安裝的 hello 下列：
   * Visual Studio 2013 或 Visual Studio 2015
   * 下載 Azure SDK for Visual Studio 2013 或 Visual Studio 2015。 瀏覽過[Azure 下載頁面](https://azure.microsoft.com/downloads/)按一下**VS 2013**或**VS 2015**在 hello **.NET** > 一節。
   * 下載最新 Azure Data Factory 外掛程式 hello for Visual Studio: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5)或[VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005)。 您也可以執行下列步驟的 hello 更新 hello 外掛程式： hello 功能表上，按一下**工具** -> **擴充功能和更新** -> **線上** ->  **Visual Studio 組件庫** -> **Microsoft Azure Data Factory Tools for Visual Studio** -> **更新**。

現在，我們將使用 Visual Studio toocreate Azure data factory。

### <a name="create-visual-studio-project"></a>建立 Visual Studio 專案
1. 啟動 **Visual Studio 2013** 或 **Visual Studio 2015**。 按一下**檔案**，點太**新增**，然後按一下**專案**。 您應該會看見 hello**新專案** 對話方塊。  
2. 在 hello**新專案**對話方塊中，選取 hello **DataFactory**範本，然後按一下**空白資料處理站專案**。   

    ![[新增專案] 對話方塊](./media/data-factory-build-your-first-pipeline-using-vs/new-project-dialog.png)
3. 輸入**名稱**hello 專案**位置**，hello 的名稱和**方案**，按一下**確定**。

    ![Solution Explorer](./media/data-factory-build-your-first-pipeline-using-vs/solution-explorer.png)

### <a name="create-linked-services"></a>建立連結服務
在此步驟中，您會建立兩個連結服務：**Azure 儲存體**和**隨選 HDInsight**。 

hello Azure 儲存體連結服務連結您的 Azure 儲存體帳戶 toohello data factory 提供 hello 連接資訊。 資料 Factory 服務會在執行階段使用 hello hello 連結的服務設定 tooconnect toohello Azure 儲存體連接字串。 這個儲存體保存輸入] 和 [輸出資料 hello 管線和 hello hive hello hive 活動所使用的指令碼檔案。 

隨 HDInsight 連結服務，與 hello HDInsight 叢集會自動建立在執行階段準備 tooprocessed hello 輸入的資料時。 它為了處理和閒置 hello 指定的時間量之後，會刪除 hello 叢集。 

> [!NOTE]
> 您可以指定其名稱和設定發行您的 Data Factory 方案的 hello 次，以建立 data factory。

#### <a name="create-azure-storage-linked-service"></a>建立 Azure 儲存體連結服務
1. 以滑鼠右鍵按一下**連結的服務**hello 方案總管中，點太**新增**，然後按一下**新項目**。      
2. 在 hello**加入新項目**對話方塊中，選取**Azure 儲存體連結服務**從 hello 清單，然後按一下**新增**。
    ![Azure 儲存體連結服務](./media/data-factory-build-your-first-pipeline-using-vs/new-azure-storage-linked-service.png)
3. 取代`<accountname>`和`<accountkey>`與 hello 您 Azure 儲存體帳戶名稱和其索引鍵。 toolearn 如何 tooget 您的儲存體存取金鑰，請參閱有關如何 tooview、 複製和重新產生儲存體存取金鑰中的 hello 資訊[管理您的儲存體帳戶](../storage/common/storage-create-storage-account.md#manage-your-storage-account)。
    ![Azure 儲存體連結服務](./media/data-factory-build-your-first-pipeline-using-vs/azure-storage-linked-service.png)
4. 儲存 hello **AzureStorageLinkedService1.json**檔案。

#### <a name="create-azure-hdinsight-linked-service"></a>建立 Azure HDInsight 連結服務
1. 在 hello**方案總管 中**，以滑鼠右鍵按一下**連結的服務**，點太**新增**，然後按一下**新項目**。
2. 選取 [HDInsight 隨選連結服務]，然後按一下 [新增]。
3. 取代 hello **JSON**以下列 JSON hello:

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
                "linkedServiceName": "AzureStorageLinkedService1"
            }
        }
    }
    ```

    hello 下表提供 hello hello 程式碼片段中使用的 JSON 屬性的說明：

    屬性 | 說明
    -------- | ----------- 
    ClusterSize | 指定 hello hello HDInsight Hadoop 叢集大小。
    TimeToLive | 於刪除之前，請指定 hello HDInsight 叢集，該 hello 閒置時間。
    linkedServiceName | 指定 hello 是所產生的 HDInsight Hadoop 叢集中使用的 toostore hello 記錄檔的儲存體帳戶。 

    > [!IMPORTANT]
    > hello HDInsight 叢集建立**預設容器**hello hello JSON (linkedServiceName) 中所指定的 blob 儲存體中。 HDInsight 刪除 hello 叢集時，不會刪除此容器。 這是設計的行為。 在使用 HDInsight 隨選連結服務時，除非有現有的即時叢集 (timeToLive)，否則每次處理配量時，就會建立 HDInsight 叢集。 hello 處理完成時，會自動刪除 hello 叢集。
    > 
    > 隨著處理的配量越來越多，您會在 Azure Blob 儲存體中看到許多容器。 如果您不需要它們進行疑難排解的 hello 工作，您可能會想 toodelete 它們 tooreduce hello 儲存體成本。 這些容器的 hello 名稱遵循模式： `adf<yourdatafactoryname>-<linkedservicename>-datetimestamp`。 使用工具，例如[Microsoft 儲存體總管](http://storageexplorer.com/)toodelete 容器，在您的 Azure blob 儲存體。

    如需 JSON 屬性的詳細資訊，請參閱[計算已連結的服務](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service)一文。 
4. 儲存 hello **HDInsightOnDemandLinkedService1.json**檔案。

### <a name="create-datasets"></a>建立資料集
在此步驟中，您可以建立資料集 toorepresent hello 輸入和輸出 Hive 處理的資料。 這些資料集，請參閱 toohello **AzureStorageLinkedService1**稍早在本教學課程中，您已建立。 hello 連結的服務點 tooan Azure 儲存體帳戶和資料集指定保留輸入 hello 儲存體中的容器、 資料夾、 檔案名稱和輸出資料。   

#### <a name="create-input-dataset"></a>建立輸入資料集
1. 在 hello**方案總管 中**，以滑鼠右鍵按一下**資料表**，點太**新增**，然後按一下**新項目**。
2. 選取**Azure Blob** hello 清單中，從變更 hello hello 檔名太**InputDataSet.json**，然後按一下**新增**。
3. 取代 hello **JSON** hello 編輯器 hello 下列 JSON 片段：

    ```json
    {
        "name": "AzureBlobInput",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService1",
            "typeProperties": {
                "fileName": "input.log",
                "folderPath": "adfgetstarted/inputdata",
                "format": {
                    "type": "TextFormat",
                    "columnDelimiter": ","
                }
            },
            "availability": {
                "frequency": "Month",
                "interval": 1
            },
            "external": true,
            "policy": {}
        }
    }
    ```
    此 JSON 片段會定義資料集稱為**AzureBlobInput**代表 hello 管線中的 hello hive 活動的輸入的資料。 您指定 hello 輸入的資料位於呼叫 hello blob 容器`adfgetstarted`和 hello 資料夾稱為`inputdata`。

    hello 下表提供 hello hello 程式碼片段中使用的 JSON 屬性的說明：

    屬性 | 說明 |
    -------- | ----------- |
    類型 |hello type 屬性設定太**AzureBlob**因為資料常駐於 Azure Blob 儲存體中。
    linkedServiceName | 是指您稍早建立的 AzureStorageLinkedService1 toohello。
    fileName |這是選用屬性。 如果您省略這個屬性時，會挑出 hello folderPath 中的所有 hello 檔案。 在此情況下，只有 hello input.log 會進行處理。
    類型 | hello 記錄檔是以文字格式，因此我們使用 TextFormat。 |
    columnDelimiter | hello 記錄檔中的資料行以 hello 逗號字元分隔 (`,`)
    frequency/interval | 設定 tooMonth 頻率和間隔為 1，這表示的 hello 輸入配量可使用每個月。
    external | 設定此屬性是 tootrue hello hello 活動的輸入的資料不會產生 hello 管線。 此屬性只會指定於輸入資料集。 Hello hello 第一個活動的輸入資料集，一定會設定它 tootrue。
4. 儲存 hello **InputDataset.json**檔案。

#### <a name="create-output-dataset"></a>建立輸出資料集
現在，您可以建立 hello 輸出資料集 toorepresent 輸出資料儲存在 hello Azure Blob 儲存體中。

1. 在 hello**方案總管 中**，以滑鼠右鍵按一下**資料表**，點太**新增**，然後按一下**新項目**。
2. 選取**Azure Blob** hello 清單中，從變更 hello hello 檔名太**OutputDataset.json**，然後按一下**新增**。
3. 取代 hello **JSON** hello hello 下列 JSON 編輯器：
    
    ```json
    {
        "name": "AzureBlobOutput",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService1",
            "typeProperties": {
                "folderPath": "adfgetstarted/partitioneddata",
                "format": {
                    "type": "TextFormat",
                    "columnDelimiter": ","
                }
            },
            "availability": {
                "frequency": "Month",
                "interval": 1
            }
        }
    }
    ```
    hello JSON 片段會定義資料集稱為**AzureBlobOutput**代表輸出 hello 管線中的 hello hive 活動所產生的資料。 您指定 hello 輸出 hello hive 活動所產生的資料位於呼叫 hello blob 容器`adfgetstarted`和 hello 資料夾稱為`partitioneddata`。 
    
    hello**可用性**區段會指定該 hello 輸出資料集產生每月為基礎。 hello 輸出資料集的磁碟機 hello 排程的 hello 管線。 hello 管線會執行每個月之間其開始和結束時間。 

    請參閱**建立 hello 輸入資料集**> 一節，如需這些屬性的描述。 您未 hello 外部屬性上設定輸出資料集為 hello 資料集由 hello 管線所產生。
4. 儲存 hello **OutputDataset.json**檔案。

### <a name="create-pipeline"></a>建立管線
您已建立 hello Azure 儲存體連結服務，以及輸入和輸出資料集為止。 現在，建立具有 **HDInsightHive** 活動的管線。 hello**輸入**hello hive 活動會設定太**AzureBlobInput**和**輸出**設定得**AzureBlobOutput**。 每月是可用的輸入資料集配量 (頻率： Month、 interval: 1)，且 hello 輸出配量產生每月太。 

1. 在 hello**方案總管 中**，以滑鼠右鍵按一下**管線**，點太**新增**，然後按一下**新項目。**
2. 選取**Hive 轉換管線**從 hello 清單，然後按一下**新增**。
3. 取代 hello **JSON**以下列程式碼片段的 hello:

    > [!IMPORTANT]
    > 取代`<storageaccountname>`hello 的儲存體帳戶的名稱。

    ```json
    {
        "name": "MyFirstPipeline",
        "properties": {
            "description": "My first Azure Data Factory pipeline",
            "activities": [
                {
                    "type": "HDInsightHive",
                    "typeProperties": {
                        "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                        "scriptLinkedService": "AzureStorageLinkedService1",
                        "defines": {
                            "inputtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/inputdata",
                            "partitionedtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/partitioneddata"
                        }
                    },
                    "inputs": [
                        {
                            "name": "AzureBlobInput"
                        }
                    ],
                    "outputs": [
                        {
                            "name": "AzureBlobOutput"
                        }
                    ],
                    "policy": {
                        "concurrency": 1,
                        "retry": 3
                    },
                    "scheduler": {
                        "frequency": "Month",
                        "interval": 1
                    },
                    "name": "RunSampleHiveActivity",
                    "linkedServiceName": "HDInsightOnDemandLinkedService"
                }
            ],
            "start": "2016-04-01T00:00:00Z",
            "end": "2016-04-02T00:00:00Z",
            "isPaused": false
        }
    }
    ```

    > [!IMPORTANT]
    > 取代`<storageaccountname>`hello 的儲存體帳戶的名稱。

    hello JSON 片段會定義單一活動 （Hive 活動） 所組成的管線。 此活動視 HDInsight 叢集 tooproduce 輸出資料上執行 Hive 指令碼 tooprocess 輸入的資料。 在 hello 活動 區段中的 hello 管線 JSON，您會看到一個 hello 陣列中的活動類型設定太**HDInsightHive**。 

    在特定 tooHDInsight Hive 活動 hello 類型屬性，您可以指定哪些 Azure 儲存體連結服務有 hello hive 指令碼檔案、 hello 路徑 toohello 指令碼檔和參數 toohello 指令碼檔案。 

    hello Hive 指令碼檔案， **partitionweblogs.hql**，儲存在 hello Azure 儲存體帳戶 （由 hello scriptLinkedService 指定），和 hello `script` hello 容器中的資料夾`adfgetstarted`。

    hello`defines`區段是做為 Hive 組態值傳遞 toohello hive 指令碼使用的 toospecify hello 執行階段設定 (例如`${hiveconf:inputtable}`， `${hiveconf:partitionedtable})`。

    hello**啟動**和**結束**hello 管線屬性指定 hello 之 hello 管線的作用期間。 您已設定 hello 資料集 toobe 產生每月，因此，一次 （因為 hello 月份是相同的開始和結束日期） hello 管線產生配量。

    在 hello 活動 JSON 中，您指定該 hello Hive 指令碼在上執行指定 hello hello 計算**linkedServiceName** – **HDInsightOnDemandLinkedService**。
4. 儲存 hello **HiveActivity1.json**檔案。

### <a name="add-partitionweblogshql-and-inputlog-as-a-dependency"></a>將 partitionweblogs.hql 新增為相依性
1. 以滑鼠右鍵按一下**相依性**在 hello**方案總管 中**視窗中，點太**新增**，然後按一下**現有項目**。  
2. 瀏覽 toohello **C:\ADFGettingStarted**選取**partitionweblogs.hql**， **input.log**檔案，然後按一下**新增**。 您可以建立這兩個檔案從 hello 必要條件的一部分[教學課程概觀](data-factory-build-your-first-pipeline.md)。

當您發行 hello 方案 hello 下一個步驟中時，hello **partitionweblogs.hql**檔案已上傳的 toohello**指令碼**資料夾中 hello `adfgetstarted` blob 容器。   

### <a name="publishdeploy-data-factory-entities"></a>發佈/部署 Data Factory 實體
在此步驟中，您會在您的專案 toohello Azure Data Factory 服務中發行 hello Data Factory 實體 （連結的服務、 資料集和管線）。 在發行的 hello 程序，您可以指定 hello data factory 的名稱。 

1. 以滑鼠右鍵按一下專案 hello 方案總管] 中的，按一下 [**發行**。
2. 如果您看到**登入 Microsoft 帳戶 tooyour**對話方塊中，hello 擁有帳戶的 Azure 訂用帳戶中，輸入您的認證，然後按一下**登入**。
3. 您應該會看到下列對話方塊中的 hello:

   ![發佈對話方塊](./media/data-factory-build-your-first-pipeline-using-vs/publish.png)
4. 在 hello**設定資料 factory**頁面上，執行下列步驟 hello:

    ![發佈 - 新增資料處理站設定](media/data-factory-build-your-first-pipeline-using-vs/publish-new-data-factory.png)

   1. 選取 [建立新的 Data Factory]  選項。
   2. 輸入唯一**名稱**hello data factory。 例如：**DataFactoryUsingVS09152016**。 hello 名稱必須是全域唯一的。
   3. 選取 hello 右訂用帳戶 hello**訂用帳戶**欄位。 
        > [!IMPORTANT]
        > 如果看不到任何訂用帳戶，請確定您登入是系統管理員或共同管理員的 hello 訂用帳戶的帳戶。
   4. 選取 hello**資源群組**hello 資料 factory toobe 建立的。
   5. 選取 hello**區域**hello data factory。
   6. 按一下**下一步**tooswitch toohello**發行的項目**頁面。 (按 **索引標籤**超出 hello 名稱欄位 tooif hello toomove**下一步**按鈕已停用。)

    > [!IMPORTANT]
    > 如果您收到 hello 錯誤**Data factory 名稱"DataFactoryUsingVS"不是使用**發行時，請變更 hello 名稱 (例如，yournameDataFactoryUsingVS)。 請參閱 [Data Factory - 命名規則](data-factory-naming-rules.md) 主題，以了解 Data Factory 成品的命名規則。   
1. 在 [hello**發行的項目**頁面上，確定所有 hello Data Factory 實體已選取，然後按一下**下一步]** tooswitch toohello**摘要**頁面。

    ![發佈項目頁面](media/data-factory-build-your-first-pipeline-using-vs/publish-items-page.png)     
2. 檢閱 hello 摘要，然後按一下**下一步**toostart hello 部署程序和檢視 hello**部署狀態**。

    ![摘要頁面](media/data-factory-build-your-first-pipeline-using-vs/summary-page.png)
3. 在 [hello**部署狀態**] 頁面上，您應該會看到 hello hello 部署程序的狀態。 Hello 部署完成之後，請按一下 [完成]。

重要事項 toonote:

- 如果您收到 hello 錯誤：**此訂用帳戶不是已註冊的 toouse 命名空間 Microsoft.DataFactory**、 執行 hello 下列其中一項，然後再試一次發行：
    - 在 Azure PowerShell，執行下列命令 tooregister hello Data Factory 提供者的 hello。
        ```PowerShell   
        Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
        ```
        您可以執行下列命令 tooconfirm hello 該 hello Data Factory 提供者註冊。

        ```PowerShell
        Get-AzureRmResourceProvider
        ```
    - 登入使用 hello Azure 訂用帳戶中 toohello [Azure 入口網站](https://portal.azure.com)並瀏覽 tooa Data Factory 刀鋒視窗 （或） 在 hello Azure 入口網站中建立 data factory。 這個動作會自動註冊 hello 您的提供者。
- 可能會註冊為未來的 hello 中的 DNS 名稱，因此會變成可公開可見 hello hello data factory 名稱。
- toocreate Data Factory 執行個體，您需要 toobe 為系統管理員或共同管理員的 hello Azure 訂用帳戶

### <a name="monitor-pipeline"></a>監視管線
在此步驟中，您可以監視 hello 管線中使用圖表檢視的 hello data factory。 

#### <a name="monitor-pipeline-using-diagram-view"></a>使用圖表檢視監視管線
1. 登入 toohello [Azure 入口網站](https://portal.azure.com/)，執行下列步驟 hello:
   1. 按一下 [更多服務]，然後按一下 [Data Factory]。
       
        ![瀏覽 Data Factory](./media/data-factory-build-your-first-pipeline-using-vs/browse-datafactories.png)
   2. 選取 hello 的 data factory 的名稱 (例如： **DataFactoryUsingVS09152016**) 從 data factory 的 hello 清單。
   
       ![選取您的 Data Factory](./media/data-factory-build-your-first-pipeline-using-vs/select-first-data-factory.png)
2. 在 data factory 的 hello 首頁上，按一下 **圖表**。

    ![[圖表] 磚](./media/data-factory-build-your-first-pipeline-using-vs/diagram-tile.png)
3. 在 hello 圖表檢視，您會看到 hello 管線，以及此教學課程中使用的資料集的總覽。

    ![圖表檢視](./media/data-factory-build-your-first-pipeline-using-vs/diagram-view-2.png)
4. tooview hello 管線，以滑鼠右鍵按一下管線，在 hello 中的所有活動圖表，然後按一下 開啟管線。

    ![開啟管線功能表](./media/data-factory-build-your-first-pipeline-using-vs/open-pipeline-menu.png)
5. 確認您看到 hello 管線中的 hello HDInsightHive 活動。

    ![開啟管線檢視](./media/data-factory-build-your-first-pipeline-using-vs/open-pipeline-view.png)

    toonavigate 回 toohello 前一個檢視中，按一下  **Data factory** hello hello 上方的階層連結功能表中。
6. 在 hello**圖表檢視**，按兩下 hello 資料集**AzureBlobInput**。 確認該 hello 扇區**準備**狀態。 它可能需要幾分鐘的 hello 配量 tooshow 以佔用就緒狀態。 如果它不會發生您等候一段時間之後，查看是否有 hello 輸入的檔 (input.log) 放在 hello 右容器 (`adfgetstarted`) 和資料夾 (`inputdata`)。 並確定該 hello**外部**hello 輸入資料集上的屬性設定太**true**。 

   ![輸入配量處於就緒狀態](./media/data-factory-build-your-first-pipeline-using-vs/input-slice-ready.png)
7. 按一下**X** tooclose **AzureBlobInput**刀鋒視窗。
8. 在 hello**圖表檢視**，按兩下 hello 資料集**AzureBlobOutput**。 您會看到目前正在處理該 hello 扇區。

   ![Dataset](./media/data-factory-build-your-first-pipeline-using-vs/dataset-blade.png)
9. 當處理完成時，請參閱中的 hello 扇區**準備**狀態。

   > [!IMPORTANT]
   > 建立隨選 HDInsight 叢集通常需要一些時間 (大約 20 分鐘)。 因此，預期 hello 管線 tootake**大約 30 分鐘**tooprocess hello 配量。  
   
    ![Dataset](./media/data-factory-build-your-first-pipeline-using-vs/dataset-slice-ready.png)    
10. 當 hello 配量處於**準備**狀態，請檢查 hello`partitioneddata`資料夾中 hello `adfgetstarted` hello 您 blob 儲存體容器中的輸出資料。  

    ![輸出資料](./media/data-factory-build-your-first-pipeline-using-vs/three-ouptut-files.png)
11. 按一下 hello 配量 toosee 詳細資料 中，有關**資料配量**刀鋒視窗。

    ![資料配量詳細資料](./media/data-factory-build-your-first-pipeline-using-vs/data-slice-details.png)  
12. 按一下在 hello 中執行的活動**活動執行清單**toosee 活動的詳細資料中執行 （在我們的案例的 Hive 活動）**活動執行詳細資料**視窗。 
  
    ![活動執行詳細資料](./media/data-factory-build-your-first-pipeline-using-vs/activity-window-blade.png)    

    從 hello 記錄檔，您可以查看上次執行所執行的 hello Hive 查詢和狀態資訊。 這些記錄檔適合用來排解任何疑難問題。  

請參閱[監視資料集和管線](data-factory-monitor-manage-pipelines.md)如需如何 toouse hello Azure 入口網站 toomonitor hello 管線和資料集您已建立本教學課程中的指示。

#### <a name="monitor-pipeline-using-monitor--manage-app"></a>使用監視及管理應用程式來監視管線
您也可以使用監視和管理應用程式 toomonitor 您的管線。 如需使用此應用程式的詳細資訊，請參閱 [使用監視及管理應用程式來監視和管理 Azure Data Factory 管線](data-factory-monitor-manage-app.md)。

1. 按一下 [監視及管理] 圖格。

    ![監視及管理圖格](./media/data-factory-build-your-first-pipeline-using-vs/monitor-and-manage-tile.png)
2. 您應該會看到 [監視及管理] 應用程式。 變更 hello**開始時間**和**結束時間**toomatch 開始 (04-01-2016年上午 12:00) 和結束時間 (04-02-2016年上午 12:00) 您的管線，然後按一下**套用**。

    ![監視及管理應用程式](./media/data-factory-build-your-first-pipeline-using-vs/monitor-and-manage-app.png)
3. toosee 詳細活動視窗，請在選取 hello**活動視窗清單**toosee 相關的詳細資料。
    ![活動時段詳細資料](./media/data-factory-build-your-first-pipeline-using-vs/activity-window-details.png)

> [!IMPORTANT]
> 已成功處理 hello 配量時，取得刪除 hello 輸入的檔。 因此，如果您想 toorerun hello 配量，或不要 hello 教學課程中上, 傳 hello 輸入的檔 (input.log) toohello`inputdata`資料夾 hello`adfgetstarted`容器。

### <a name="additional-notes"></a>其他注意事項
- 資料處理站可以有一或多個管線。 其中的管線可以有一或多個活動。 例如，複製活動 toocopy 資料從來源 tooa 目的地資料存放區和 HDInsight Hive 活動 toorun Hive 指令碼 tootransform 輸入資料。 請參閱[支援資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)針對所有 hello 來源與接收支援 hello 複製活動。 請參閱[計算連結的服務](data-factory-compute-linked-services.md)hello 的 Data Factory 支援的計算服務的清單。
- 連結的服務將資料存放區，或計算服務 tooan 的 Azure data factory。 請參閱[支援資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)針對所有 hello 來源與接收支援 hello 複製活動。 請參閱[計算連結的服務](data-factory-compute-linked-services.md)Data Factory 支援的計算服務的 hello 清單和[轉換活動](data-factory-data-transformation-activities.md)，可以在其上執行。
- 請參閱[移動的資料 / tooAzure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service)如需詳細資訊 JSON 屬性用於 hello Azure 儲存體連結服務定義。
- 您可以使用自己的 HDInsight 叢集，不必使用隨選的 HDInsight 叢集。 請參閱 [計算連結服務](data-factory-compute-linked-services.md) 以取得詳細資料。
-  hello Data Factory 建立**linux**以 hello 前面 JSON 為您的 HDInsight 叢集。 如需詳細資訊，請參閱 [HDInsight 隨選連結服務](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) 。
- hello HDInsight 叢集建立**預設容器**hello hello JSON (linkedServiceName) 中所指定的 blob 儲存體中。 HDInsight 刪除 hello 叢集時，不會刪除此容器。 這是設計的行為。 在使用 HDInsight 隨選連結服務時，除非有現有的即時叢集 (timeToLive)，否則每次處理配量時，就會建立 HDInsight 叢集。 hello 處理完成時，會自動刪除 hello 叢集。
    
    隨著處理的配量越來越多，您會在 Azure Blob 儲存體中看到許多容器。 如果您不需要它們進行疑難排解的 hello 工作，您可能會想 toodelete 它們 tooreduce hello 儲存體成本。 這些容器的 hello 名稱遵循模式： `adf**yourdatafactoryname**-**linkedservicename**-datetimestamp`。 使用工具，例如[Microsoft 儲存體總管](http://storageexplorer.com/)toodelete 容器，在您的 Azure blob 儲存體。
- 目前，輸出資料集是哪些磁碟機 hello 排程，因此您必須建立輸出資料集，即使 hello 活動不會產生任何輸出。 如果 hello 活動不接受任何輸入，您可以略過建立 hello 輸入資料集。 
- 本教學課程不會顯示如何使用 Azure Data Factory 複製資料。 如需如何使用 Azure Data Factory，toocopy 資料，請參閱[教學課程： 將資料從 Blob 儲存體 tooSQL 資料庫複製](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。


## <a name="use-server-explorer-tooview-data-factories"></a>使用伺服器總管 tooview data factory
1. 在**Visual Studio**，按一下 **檢視**在 hello 功能表，然後按一下**伺服器總管**。
2. 在 [hello 伺服器總管] 視窗中，展開**Azure**展開**Data Factory**。 如果您看到**登入 tooVisual Studio**，輸入 hello**帳戶**與您的 Azure 訂用帳戶，然後按一下相關聯**繼續**。 輸入**密碼**，然後按一下 [登入]。 Visual Studio 會嘗試 tooget 您訂用帳戶中的所有 Azure data factory 的資訊。 您看到這項作業在 hello hello 狀態**資料 Factory 工作清單**視窗。

    ![Server Explorer](./media/data-factory-build-your-first-pipeline-using-vs/server-explorer.png)
3. 您可以以滑鼠右鍵按一下 data factory，並選取**匯出 Data Factory tooNew 專案**toocreate Visual Studio 專案是根據現有的 data factory。

    ![匯出 Data Factory](./media/data-factory-build-your-first-pipeline-using-vs/export-data-factory-menu.png)

## <a name="update-data-factory-tools-for-visual-studio"></a>更新 Visual studio 的 Data Factory 工具
tooupdate Azure Data Factory tools for Visual Studio hello 下列步驟：

1. 按一下**工具**hello 功能表，然後選取**擴充功能和更新**。
2. 選取**更新**在 hello 左的窗格，然後選取  **Visual Studio 組件庫**。
3. 選取 [Visual Studio 的 Azure Data Factory 工具] 並按一下 [更新]。 如果看不到此項目，您已經有 hello hello 工具最新版本。

## <a name="use-configuration-files"></a>使用組態檔
您可以使用 Visual Studio tooconfigure 屬性中的組態檔的連結服務/資料表/管線以不同的方式為每個環境。

請考慮下列 JSON 定義 Azure 儲存體連結服務的 hello。 toospecify **connectionString** accountname 和 accountkey hello 環境 （開發/測試/生產環境） toowhich 所根據的值不同，您要部署 Data Factory 實體。 您可以針對每個環境使用個別的組態檔來達成此行為。

```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "description": "",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
```

### <a name="add-a-configuration-file"></a>新增組態檔
執行下列步驟的 hello 加入每個環境的組態檔：   

1. Visual Studio 方案中的 hello Data Factory 專案上按一下滑鼠右鍵，指向太**新增**，然後按一下**新項目**。
2. 選取**Config**從已安裝的範本在 hello 左邊 hello 清單中選取**組態檔**，輸入**名稱**hello 組態檔案，然後按一下**新增**。

    ![新增組態檔](./media/data-factory-build-your-first-pipeline-using-vs/add-config-file.png)
3. 遵循格式 hello 中加入組態參數和值：

    ```json
    {
        "$schema": "http://datafactories.schema.management.azure.com/vsschemas/V1/Microsoft.DataFactory.Config.json",
        "AzureStorageLinkedService1": [
            {
                "name": "$.properties.typeProperties.connectionString",
                "value": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
            }
        ],
        "AzureSqlLinkedService1": [
            {
                "name": "$.properties.typeProperties.connectionString",
                "value":  "Server=tcp:spsqlserver.database.windows.net,1433;Database=spsqldb;User ID=spelluru;Password=Sowmya123;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
            }
        ]
    }
    ```

    這個範例會設定 Azure 儲存體連結服務和 Azure SQL 連結服務的 connectionString 屬性。 請注意，用來指定名稱的 hello 語法[JsonPath](http://goessner.net/articles/JsonPath/)。   

    如果 JSON 屬性，其值的陣列，如 hello 下列程式碼所示：  

    ```json
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
    ```

    設定屬性，如下列組態檔 （使用以零為起始的索引） 的 hello 中所示：

    ```json
    {
        "name": "$.properties.structure[0].name",
        "value": "FirstName"
    }
    {
        "name": "$.properties.structure[0].type",
        "value": "String"
    }
    {
        "name": "$.properties.structure[1].name",
        "value": "LastName"
    }
    {
        "name": "$.properties.structure[1].type",
        "value": "String"
    }
    ```

### <a name="property-names-with-spaces"></a>包含空格的屬性名稱
如果屬性名稱具有空格中的，使用方括號，如下列範例 （資料庫伺服器名稱） 的 hello 中所示：

```json
 {
     "name": "$.properties.activities[1].typeProperties.webServiceParameters.['Database server name']",
     "value": "MyAsqlServer.database.windows.net"
 }
```

### <a name="deploy-solution-using-a-configuration"></a>使用組態部署解決方案
當您發行 Azure Data Factory 實體在 VS 中時，您可以指定該發行作業需 toouse hello 組態。

使用組態檔的 Azure Data Factory 專案中的 toopublish 實體：   

1. Data Factory 專案上按一下滑鼠右鍵，然後按一下**發行**toosee hello**發行的項目** 對話方塊。
2. 選取現有的 data factory，或指定值的 data factory 建立 hello**設定資料 factory**頁面，然後按一下**下一步**。   
3. 在 hello**發行的項目**頁面： 您會看到與 hello 可用的組態下拉式清單**選取部署設定**欄位。

    ![選取組態檔](./media/data-factory-build-your-first-pipeline-using-vs/select-config-file.png)
4. 選取 hello**組態檔**您會想 toouse，然後按一下**下一步**。
5. 確認您看到的 JSON 檔案中 hello hello 名稱**摘要**頁面上，按一下 **下一步**。
6. 按一下**完成**hello 部署作業完成之後。

當您部署時，hello 設定檔中的 hello 值是使用的 tooset hello JSON 檔案中的屬性值在 hello 實體部署的 tooAzure Data Factory 服務之前。   

## <a name="use-azure-key-vault"></a>使用 Azure 金鑰保存庫
它不建議您經常對等連接字串 toohello 程式碼儲存機制的安全性原則 toocommit 敏感性資料。 請參閱[ADF 安全發佈](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFSecurePublish)GitHub toolearn 有關在 Azure 金鑰保存庫中儲存機密資訊，並使用它時發行 Data Factory 實體上的範例。 hello 安全發行 Visual Studio 擴充功能可讓儲存在金鑰保存庫中的 hello 密碼 toobe 和連結的服務中指定只參考 toothem / 部署組態。 當您發行 Data Factory 實體 tooAzure 時，這些參考會解析。 這些檔案接著可以認可的 toosource 儲存機制，而不公開任何秘密。

## <a name="summary"></a>摘要
在本教學課程中，您可以建立 Azure data factory tooprocess 資料在 HDInsight hadoop 叢集上執行 Hive 指令碼。 您使用 hello Data Factory 編輯器在 hello Azure 入口網站 toodo hello 下列步驟：  

1. 建立 Azure **Data Factory**。
2. 建立兩個 **連結服務**：
   1. **Azure 儲存體**您保留輸入/輸出檔案 toohello 資料處理站的 Azure blob 儲存體連結服務 toolink。
   2. **Azure HDInsight**視連結的服務 toolink 隨 HDInsight Hadoop 叢集 toohello 資料 factory。 Azure Data Factory 建立 HDInsight Hadoop 叢集在 just-in-time tooprocess 輸入的資料，並產生輸出資料。
3. 建立兩個**資料集**，其中描述輸入和輸出 HDInsight Hive 活動 hello 管線中的資料。
4. 建立具有 **HDInsight Hive** 活動的**管線**。  

## <a name="next-steps"></a>後續步驟
在本文中，您已經建立可在隨選 HDInsight 叢集上執行 Hive 指令碼，含有轉換活動 (HDInsight 活動) 的管線。 如何 toouse 複製活動 toocopy 資料從 Azure Blob tooAzure SQL，請參閱的 toosee[教學課程： 將資料從 Azure blob tooAzure SQL 複製](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。

您可以藉由設定 hello 輸出資料集的一個活動 hello 的輸入資料集的 hello 其他活動鏈結 （執行一個活動執行另一個之後） 的兩個活動。 如需詳細資訊，請參閱[在 Data Factory 中排程和執行](data-factory-scheduling-and-execution.md)。 


## <a name="see-also"></a>另請參閱
| 主題 | 說明 |
|:--- |:--- |
| [管線](data-factory-create-pipelines.md) |這篇文章可協助您了解管線和 Azure Data Factory 中的活動以及 toouse 它們 tooconstruct 資料驅動型工作流程或商務案例。 |
| [資料集](data-factory-create-datasets.md) |本文協助您了解 Azure Data Factory 中的資料集。 |
| [資料轉換活動](data-factory-data-transformation-activities.md) |本文提供 Azure Data Factory 所支援的資料轉換活動清單 (例如您在本教學課程中使用的 HDInsight Hive 轉換)。 |
| [排程和執行](data-factory-scheduling-and-execution.md) |本文說明 Azure Data Factory 應用程式模型的 hello 排程和執行的層面。 |
| [使用監視應用程式來監視和管理管線](data-factory-monitor-manage-app.md) |本文說明如何 toomonitor，管理和偵錯管線使用 hello 監視和管理應用程式。 |
