---
title: "aaaBuild 您第一次的 data factory （Azure 入口網站） |Microsoft 文件"
description: "在本教學課程中，您會建立範例 Azure Data Factory 管線中使用 Data Factory 編輯器 hello Azure 入口網站中。"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: d5b14e9e-e358-45be-943c-5297435d402d
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: fc80776001b181a59c04d80d2e05c20b107a63f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-portal"></a>教學課程：使用 Azure 入口網站建置您的第一個 Azure Data Factory
> [!div class="op_single_selector"]
> * [概觀和必要條件](data-factory-build-your-first-pipeline.md)
> * [Azure 入口網站](data-factory-build-your-first-pipeline-using-editor.md)
> * [Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
> * [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
> * [Resource Manager 範本](data-factory-build-your-first-pipeline-using-arm.md)
> * [REST API](data-factory-build-your-first-pipeline-using-rest-api.md)


在本文中，您將學習如何 toouse [Azure 入口網站](https://portal.azure.com/)toocreate 第一個 Azure data factory。 toodo hello 教學課程中使用其他工具/Sdk，從 hello 下拉式清單選取其中一個 hello 選項。 

在此教學課程中的 hello 管線有一個活動： **HDInsight Hive 活動**。 此活動會在轉換輸入資料 tooproduce 輸出資料的 Azure HDInsight 叢集上執行 hive 指令碼。 hello 管線是排程的 toorun，每個月之間 hello 指定開始和結束時間之後。 

> [!NOTE]
> 在此教學課程中的 hello 資料管線轉換輸入的資料 tooproduce 輸出資料。 如需如何使用 Azure Data Factory，toocopy 資料，請參閱[教學課程： 將資料從 Blob 儲存體 tooSQL 資料庫複製](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。
> 
> 一個管線中可以有多個活動。 此外，您可以藉由設定 hello 輸出資料集的一個活動 hello 的輸入資料集的 hello 其他活動鏈結 （執行一個活動執行另一個之後） 的兩個活動。 如需詳細資訊，請參閱 [Data Factory 排程和執行](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline)。

## <a name="prerequisites"></a>必要條件
1. 閱讀[教學課程概觀](data-factory-build-your-first-pipeline.md)文件，以及完成 hello**必要條件**步驟。
2. 這份文件不提供 hello Azure Data Factory 服務的概觀。 我們建議您瀏覽[簡介 tooAzure Data Factory](data-factory-introduction.md) hello 服務的發行項的詳細概觀。  

## <a name="create-data-factory"></a>建立 Data Factory
資料處理站可以有一或多個管線。 其中的管線可以有一或多個活動。 例如，複製活動 toocopy 資料從來源 tooa 目的地資料存放區和 HDInsight Hive 活動 toorun Hive 指令碼 tootransform 輸入資料 tooproduct 輸出資料。 讓我們開始在此步驟中建立 hello 資料 factory。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com/)。
2. 按一下**新增**hello 左窗格中，按一下 **資料 + 分析**，然後按一下**Data Factory**。

   ![建立刀鋒視窗](./media/data-factory-build-your-first-pipeline-using-editor/create-blade.png)
3. 在 hello**新的 data factory**刀鋒視窗中，輸入**GetStartedDF** hello 名稱。

   ![新增 Data Factory 刀鋒視窗](./media/data-factory-build-your-first-pipeline-using-editor/new-data-factory-blade.png)

   > [!IMPORTANT]
   > hello hello Azure data factory 的名稱必須是**全域唯一**。 如果您收到 hello 錯誤： **Data factory 名稱"GetStartedDF"不是使用**。 變更 hello hello data factory (例如，yournameGetStartedDF) 名稱，然後再試一次建立。 請參閱 [Data Factory - 命名規則](data-factory-naming-rules.md) 主題，以了解 Data Factory 成品的命名規則。
   >
   > hello hello data factory 名稱可能會註冊為**DNS** hello 未來中的名稱，因此公開可見。
   >
   >
4. 選取 hello **Azure 訂用帳戶**您想要建立 hello 資料 factory toobe。
5. 請選取現有的 **資源群組** ，或建立資源群組。 Hello 教學課程中，建立名為的資源群組： **ADFGetStartedRG**。
6. 選取 hello**位置**hello data factory。 Hello 下拉式清單中會顯示 hello Data Factory 服務所支援的區域。
7. 選取**Pin toodashboard**。 
8. 按一下**建立**上 hello**新的 data factory**刀鋒視窗。

   > [!IMPORTANT]
   > toocreate Data Factory 執行個體，您必須是成員的 hello[資料 Factory 參與者](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor)hello 訂用帳戶/資源群組層級角色。
   >
   >
7. 在 hello 儀表板，您會看到狀態磚的 hello 下列： 部署資料處理站。    

   ![建立 Data Factory 狀態](./media/data-factory-build-your-first-pipeline-using-editor/creating-data-factory-image.png)
8. 恭喜！ 您已成功建立您的第一個 Data Factroy。 已成功建立 hello 資料處理站之後，您會看到 hello 資料 factory 頁面上，它會顯示 hello hello data factory 的內容。     

    ![Data Factory 刀鋒視窗](./media/data-factory-build-your-first-pipeline-using-editor/data-factory-blade.png)

之前 hello data factory 中建立管線，您必須 toocreate 幾個 Data Factory 實體第一次。 您第一次建立連結的服務 toolink 資料存放區/計算 tooyour 資料儲存、 定義輸入和輸出連結的資料儲存區中的資料集 toorepresent 輸入/輸出資料，然後以該活動會使用這些資料集來建立 hello 管線。

## <a name="create-linked-services"></a>建立連結的服務
在此步驟中，您可以連結您的 Azure 儲存體帳戶和隨 Azure HDInsight 叢集 tooyour 資料處理站。 hello 保存 hello hello 管線，在此範例中的輸入和輸出資料的 Azure 儲存體帳戶。 hello HDInsight 連結服務是使用的 toorun hello 管線，在此範例中的 hello 活動中指定的 Hive 指令碼。 識別哪些[資料存放區](data-factory-data-movement-activities.md)/[計算服務](data-factory-compute-linked-services.md)用於您案例，並將這些服務 toohello 資料 factory 連結藉由建立連結的服務。  

### <a name="create-azure-storage-linked-service"></a>建立 Azure 儲存體連結服務
在此步驟中，您必須連結您的 Azure 儲存體帳戶 tooyour data factory。 在此教學課程中，您可以使用 hello toostore 輸入/輸出資料與 hello HQL 指令碼檔案的相同 Azure 儲存體帳戶。

1. 按一下**作者及部署**上 hello **DATA FACTORY**刀鋒伺服器**GetStartedDF**。 您應該會看到 hello Data Factory 編輯器。

   ![[製作和部署] 圖格](./media/data-factory-build-your-first-pipeline-using-editor/data-factory-author-deploy.png)
2. 按一下 [新增資料存放區] 並選擇 [Azure 儲存體]。

   ![新增資料存放區 - Azure 儲存體 - 功能表](./media/data-factory-build-your-first-pipeline-using-editor/new-data-store-azure-storage-menu.png)
3. 您應該會看見 hello JSON 指令碼來建立 Azure 儲存體已連結的 hello 編輯器中的服務。

   ![Azure 儲存體連結服務](./media/data-factory-build-your-first-pipeline-using-editor/azure-storage-linked-service.png)
4. 取代**帳戶名稱**hello Azure 儲存體帳戶名稱和**帳戶金鑰**hello 的 hello Azure 儲存體帳戶的存取金鑰。 toolearn 如何 tooget 您的儲存體存取金鑰，請參閱有關如何 tooview、 複製和重新產生儲存體存取金鑰中的 hello 資訊[管理您的儲存體帳戶](../storage/common/storage-create-storage-account.md#manage-your-storage-account)。
5. 按一下**部署**hello 命令列 toodeploy hello 連結服務。

    ![[部署] 按鈕](./media/data-factory-build-your-first-pipeline-using-editor/deploy-button.png)

   Hello 連結的服務已成功部署之後，hello **Draft 1**視窗應該就會消失，而且您會看到**AzureStorageLinkedService** hello hello 左側的樹狀檢視中。

    ![功能表中的儲存體連結服務](./media/data-factory-build-your-first-pipeline-using-editor/StorageLinkedServiceInTree.png)    

### <a name="create-azure-hdinsight-linked-service"></a>建立 Azure HDInsight 連結服務
在此步驟中，您可以連結的隨選 HDInsight 叢集 tooyour 資料 factory。 自動在執行階段建立及刪除它為了處理和閒置 hello 指定的時間量之後 hello HDInsight 叢集。

1. 在 hello **Data Factory 編輯器**，按一下  **...**更多，按一下 新增計算，然後選取 HDInsight 隨選叢集。

    ![新增計算](./media/data-factory-build-your-first-pipeline-using-editor/new-compute-menu.png)
2. 複製並貼上下列程式碼片段 toohello hello **Draft 1**視窗。 hello JSON 片段會說明使用的 toocreate hello HDInsight 叢集隨 hello 屬性。

    ```JSON
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

    hello 下表提供 hello hello 程式碼片段中使用的 JSON 屬性的說明：

   | 屬性 | 說明 |
   |:--- |:--- |
   | ClusterSize |指定 hello hello HDInsight 叢集大小。 |
   | TimeToLive | 於刪除之前，請指定 hello HDInsight 叢集，該 hello 閒置時間。 |
   | linkedServiceName | 指定 hello 是使用的 toostore hello 記錄 HDInsight 所產生的儲存體帳戶。 |

    請注意下列點 hello:

   * hello Data Factory 建立**linux**以 hello JSON 為您的 HDInsight 叢集。 如需詳細資訊，請參閱 [HDInsight 隨選連結服務](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) 。
   * 您可以使用 **自己的 HDInsight 叢集** ，不必使用隨選的 HDInsight 叢集。 如需詳細資訊，請參閱 [HDInsight 連結服務](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) 。
   * hello HDInsight 叢集建立**預設容器**hello hello JSON 中指定的 blob 儲存體中 (**linkedServiceName**)。 HDInsight 刪除 hello 叢集時，不會刪除此容器。 這是設計的行為。 在使用 HDInsight 隨選連結服務時，除非有現有的即時叢集 (**timeToLive**)，否則每次處理配量時，就會建立 HDInsight 叢集。 hello 處理完成時，會自動刪除 hello 叢集。

       隨著處理的配量越來越多，您會在 Azure Blob 儲存體中看到許多容器。 如果您不需要它們進行疑難排解的 hello 工作，您可能會想 toodelete 它們 tooreduce hello 儲存體成本。 這些容器的 hello 名稱遵循模式: 「 adf**yourdatafactoryname**-**linkedservicename**-datetimestamp"。 使用工具，例如[Microsoft 儲存體總管](http://storageexplorer.com/)toodelete 容器，在您的 Azure blob 儲存體。

     如需詳細資訊，請參閱 [HDInsight 隨選連結服務](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) 。
3. 按一下**部署**hello 命令列 toodeploy hello 連結服務。

    ![部署 HDInsight 隨選連結服務](./media/data-factory-build-your-first-pipeline-using-editor/ondemand-hdinsight-deploy.png)
4. 確認您看到兩者**AzureStorageLinkedService**和**HDInsightOnDemandLinkedService** hello hello 左側的樹狀檢視中。

    ![含連結服務的樹狀檢視](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-linked-services.png)

## <a name="create-datasets"></a>建立資料集
在此步驟中，您可以建立資料集 toorepresent hello 輸入和輸出 Hive 處理的資料。 這些資料集，請參閱 toohello **AzureStorageLinkedService**稍早在本教學課程中，您已建立。 hello 連結的服務點 tooan Azure 儲存體帳戶和資料集指定保留輸入 hello 儲存體中的容器、 資料夾、 檔案名稱和輸出資料。   

### <a name="create-input-dataset"></a>建立輸入資料集
1. 在 hello **Data Factory 編輯器**，按一下  **...多個**hello 命令列上，按一下**新的資料集**，然後選取**Azure Blob 儲存體**。

    ![新增資料集](./media/data-factory-build-your-first-pipeline-using-editor/new-data-set.png)
2. 複製並貼上下列程式碼片段 toohello Draft 1 視窗 hello。 在 hello JSON 片段中，您要建立資料集稱為**AzureBlobInput**代表 hello 管線中活動的輸入的資料。 此外，您可以指定 hello 輸入的資料位於呼叫 hello blob 容器**adfgetstarted**和 hello 資料夾稱為**inputdata**。

    ```JSON
    {
        "name": "AzureBlobInput",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
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
    hello 下表提供 hello hello 程式碼片段中使用的 JSON 屬性的說明：

   | 屬性 | 說明 |
   |:--- |:--- |
   | 類型 |hello type 屬性設定太**AzureBlob**因為資料常駐於 Azure blob 儲存體中。 |
   | linkedServiceName |是指 toohello **AzureStorageLinkedService**您稍早建立。 |
   | folderPath | 指定 hello blob**容器**和 hello**資料夾**，其中包含輸入的 blob。 | 
   | fileName |這是選用屬性。 如果您省略這個屬性時，會挑出 hello folderPath 中的所有 hello 檔案。 在本教學課程中，只有 hello **input.log**處理。 |
   | 類型 |hello 記錄檔都是以文字格式，因此我們使用**TextFormat**。 |
   | columnDelimiter |hello 記錄檔中的資料行分隔**逗號字元 (`,`)** |
   | frequency/interval |頻率設定過**月份**和間隔是**1**，這表示該 hello 輸入配量可用每個月。 |
   | external | 這個屬性設定太**true**如果 hello 輸入的資料不會產生此管線。 在本教學課程，hello input.log 檔案不會產生這個管線，因此我們設定 hello 屬性 tootrue。 |

    如需這些 JSON 屬性的詳細資訊，請參閱 [Azure Blob 連接器](data-factory-azure-blob-connector.md#dataset-properties)一文。
3. 按一下**部署**hello 命令列 toodeploy hello 新建立的資料集上。 您應該會看到 hello hello hello 左側的樹狀檢視中的資料集。

### <a name="create-output-dataset"></a>建立輸出資料集
現在，您可以建立 hello 輸出資料集 toorepresent hello 輸出資料儲存在 hello Azure Blob 儲存體中。

1. 在 hello **Data Factory 編輯器**，按一下  **...多個**hello 命令列上，按一下**新的資料集**，然後選取**Azure Blob 儲存體**。  
2. 複製並貼上下列程式碼片段 toohello Draft 1 視窗 hello。 在 hello JSON 片段中，您要建立資料集稱為**AzureBlobOutput**，並指定 hello hello Hive 指令碼所產生的 hello 資料結構。 此外，您可以指定 hello 結果會儲存在稱為 hello blob 容器**adfgetstarted**和 hello 資料夾稱為**partitioneddata**。 hello**可用性**區段會指定該 hello 輸出資料集產生每月為基礎。

    ```JSON
    {
      "name": "AzureBlobOutput",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
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
    請參閱**建立 hello 輸入資料集**> 一節，如需這些屬性的描述。 您未 hello 外部屬性上設定輸出資料集為 hello 資料集由 hello Data Factory 服務所產生。
3. 按一下**部署**hello 命令列 toodeploy hello 新建立的資料集上。
4. 確認已成功建立該 hello 資料集。

    ![含連結服務的樹狀檢視](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-data-set.png)

## <a name="create-pipeline"></a>建立管線
在此步驟中，您會建立第一個具有 **HDInsightHive** 活動的管線。 輸入的配量可每月 (頻率： Month、 interval: 1)、 每月產生輸出配量和 hello hello 活動的排程器屬性也設定 toomonthly。 hello 輸出資料集和 hello 活動排程器的 hello 設定必須相符。 目前，輸出資料集是哪些磁碟機 hello 排程，因此您必須建立輸出資料集，即使 hello 活動不會產生任何輸出。 如果 hello 活動不接受任何輸入，您可以略過建立 hello 輸入資料集。 hello 下列 JSON 中使用的 hello 內容會說明在 hello 本節結尾處。

1. 在 hello **Data Factory 編輯器**，按一下 **省略符號 （...）更多指令**，然後按一下**新管線**。

    ![新增管線按鈕](./media/data-factory-build-your-first-pipeline-using-editor/new-pipeline-button.png)
2. 複製並貼上下列程式碼片段 toohello Draft 1 視窗 hello。

   > [!IMPORTANT]
   > 取代**storageaccountname** hello hello JSON 中的儲存體帳戶名稱。
   >
   >

    ```JSON
    {
        "name": "MyFirstPipeline",
        "properties": {
            "description": "My first Azure Data Factory pipeline",
            "activities": [
                {
                    "type": "HDInsightHive",
                    "typeProperties": {
                        "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                        "scriptLinkedService": "AzureStorageLinkedService",
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
            "start": "2017-07-01T00:00:00Z",
            "end": "2017-07-02T00:00:00Z",
            "isPaused": false
        }
    }
    ```

    在 hello JSON 片段中，您要建立管線在 HDInsight 叢集使用 Hive tooprocess 資料的活動所組成。

    hello Hive 指令碼檔案， **partitionweblogs.hql**，儲存在 hello Azure 儲存體帳戶 (由 hello scriptLinkedService，稱為**AzureStorageLinkedService**)，然後在**指令碼**hello 容器中的資料夾**adfgetstarted**。

    hello**定義**區段是做為 Hive 組態值傳遞 toohello hive 指令碼使用的 toospecify hello 執行階段設定 (例如 ${hiveconf: inputtable}，{hiveconf:partitionedtable} $)。

    hello**啟動**和**結束**hello 管線屬性指定 hello 之 hello 管線的作用期間。

    在 hello 活動 JSON 中，您指定該 hello Hive 指令碼在上執行指定 hello hello 計算**linkedServiceName** – **HDInsightOnDemandLinkedService**。

   > [!NOTE]
   > 請參閱中的"管線 JSON"[管線和 Azure Data Factory 中的活動](data-factory-create-pipelines.md)hello 範例中所使用的 JSON 屬性的詳細資料。
   >
   >
3. 確認 hello 下列：

   1. **input.log**檔案存在於 hello **inputdata**資料夾 hello **adfgetstarted** hello Azure blob 儲存體中的容器
   2. **partitionweblogs.hql**檔案存在於 hello**指令碼**資料夾 hello **adfgetstarted** hello Azure blob 儲存體中的容器。 完整的 hello 必要條件步驟 hello[教學課程概觀](data-factory-build-your-first-pipeline.md)如果您沒有看到這些檔案。
   3. 確認您更換**storageaccountname** hello 您的儲存體帳戶名稱在 hello 與管線 JSON。
4. 按一下**部署**hello 命令列 toodeploy hello 管線。 因為 hello**啟動**和**結束**次數設定在過去的 hello 和**isPaused**是集 toofalse，hello 管線 （hello 管線中的活動） 執行您部署之後，立即。
5. 確認您看到 hello 樹狀檢視中的 hello 管線。

    ![管線的樹狀檢視](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-pipeline.png)
6. 恭喜，您已經成功建立您的第一個管線！

## <a name="monitor-pipeline"></a>監視管線
### <a name="monitor-pipeline-using-diagram-view"></a>使用圖表檢視監視管線
1. 按一下**X** tooclose Data Factory 編輯器刀鋒 toonavigate 回 toohello Data Factory 刀鋒視窗中，並按一下**圖表**。

    ![[圖表] 磚](./media/data-factory-build-your-first-pipeline-using-editor/diagram-tile.png)
2. 在 hello 圖表檢視，您會看到 hello 管線，以及此教學課程中使用的資料集的總覽。

    ![圖表檢視](./media/data-factory-build-your-first-pipeline-using-editor/diagram-view-2.png)
3. tooview hello 管線，以滑鼠右鍵按一下管線，在 hello 中的所有活動圖表，然後按一下 開啟管線。

    ![開啟管線功能表](./media/data-factory-build-your-first-pipeline-using-editor/open-pipeline-menu.png)
4. 確認您看到 hello 管線中的 hello HDInsightHive 活動。

    ![開啟管線檢視](./media/data-factory-build-your-first-pipeline-using-editor/open-pipeline-view.png)

    toonavigate 回 toohello 前一個檢視中，按一下  **Data factory** hello hello 上方的階層連結功能表中。
5. 在 hello**圖表檢視**，按兩下 hello 資料集**AzureBlobInput**。 確認該 hello 扇區**準備**狀態。 它可能需要幾分鐘的 hello 配量 tooshow 以佔用就緒狀態。 如果它不會發生您等候一段時間之後，請參閱 < 如果您擁有 hello 輸入的檔 (input.log) 放置在 hello 右容器 (adfgetstarted) 和資料夾 (inputdata)。

   ![輸入配量處於就緒狀態](./media/data-factory-build-your-first-pipeline-using-editor/input-slice-ready.png)
6. 按一下**X** tooclose **AzureBlobInput**刀鋒視窗。
7. 在 hello**圖表檢視**，按兩下 hello 資料集**AzureBlobOutput**。 您會看到目前正在處理該 hello 扇區。

   ![Dataset](./media/data-factory-build-your-first-pipeline-using-editor/dataset-blade.png)
8. 當處理完成時，請參閱中的 hello 扇區**準備**狀態。

   ![Dataset](./media/data-factory-build-your-first-pipeline-using-editor/dataset-slice-ready.png)  

   > [!IMPORTANT]
   > 建立隨選 HDInsight 叢集通常需要一些時間 (大約 20 分鐘)。 因此，預期 hello 管線太採取**大約 30 分鐘**tooprocess hello 配量。
   >
   >

9. 當 hello 配量處於**準備**狀態，請檢查 hello **partitioneddata**資料夾中 hello **adfgetstarted** hello 您 blob 儲存體容器中的輸出資料。  

   ![輸出資料](./media/data-factory-build-your-first-pipeline-using-editor/three-ouptut-files.png)
10. 按一下 hello 配量 toosee 詳細資料 中，有關**資料配量**刀鋒視窗。

   ![資料配量詳細資料](./media/data-factory-build-your-first-pipeline-using-editor/data-slice-details.png)  
11. 按一下在 hello 中執行的活動**活動執行清單**toosee 活動的詳細資料中執行 （在我們的案例的 Hive 活動）**活動執行詳細資料**視窗。   

   ![活動執行詳細資料](./media/data-factory-build-your-first-pipeline-using-editor/activity-window-blade.png)    

   從 hello 記錄檔，您可以查看上次執行所執行的 hello Hive 查詢和狀態資訊。 這些記錄檔適合用來排解任何疑難問題。
   如需詳細資訊，請參閱 [使用 Azure 入口網站刀鋒視窗監視及管理管線](data-factory-monitor-manage-pipelines.md) 一文。

> [!IMPORTANT]
> 已成功處理 hello 配量時，取得刪除 hello 輸入的檔。 因此，如果您想 toorerun hello 配量，或不要 hello 教學課程中上, 傳 hello hello adfgetstarted 容器的輸入的檔 (input.log) toohello inputdata 資料夾。
>
>

### <a name="monitor-pipeline-using-monitor--manage-app"></a>使用監視及管理應用程式來監視管線
您也可以使用監視和管理應用程式 toomonitor 您的管線。 如需使用此應用程式的詳細資訊，請參閱 [使用監視及管理應用程式來監視和管理 Azure Data Factory 管線](data-factory-monitor-manage-app.md)。

1. 按一下**監視和管理**在您的 data factory 的 hello 首頁上並排顯示。

    ![監視及管理圖格](./media/data-factory-build-your-first-pipeline-using-editor/monitor-and-manage-tile.png)
2. 您應該會看到 [監視及管理] 應用程式。 變更 hello**開始時間**和**結束時間**toomatch 開始和結束時間的管線，然後按一下 **套用**。

    ![監視及管理應用程式](./media/data-factory-build-your-first-pipeline-using-editor/monitor-and-manage-app.png)
3. 選取活動視窗在 hello**活動 Windows** toosee 詳細的清單。

    ![活動時段詳細資料](./media/data-factory-build-your-first-pipeline-using-editor/activity-window-details.png)

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

## <a name="see-also"></a>另請參閱
| 主題 | 說明 |
|:--- |:--- |
| [管線](data-factory-create-pipelines.md) |這篇文章可協助您了解管線和 Azure Data Factory 中的活動以及 toouse 它們 tooconstruct 端對端資料驅動型工作流程或商務案例。 |
| [資料集](data-factory-create-datasets.md) |本文協助您了解 Azure Data Factory 中的資料集。 |
| [排程和執行](data-factory-scheduling-and-execution.md) |本文說明 Azure Data Factory 應用程式模型的 hello 排程和執行的層面。 |
| [使用監視應用程式來監視和管理管線](data-factory-monitor-manage-app.md) |本文說明如何 toomonitor，管理和偵錯管線使用 hello 監視和管理應用程式。 |
