---
title: "從 Azure Data Factory 程式 aaaInvoke Spark |Microsoft 文件"
description: "了解如何從 Azure data factory 使用 tooinvoke Spark 程式 hello MapReduce 活動。"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: fd98931c-cab5-4d66-97cb-4c947861255c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: f88943ece7ee3d21dedbd857609f1b2713b62741
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="invoke-spark-programs-from-azure-data-factory-pipelines"></a>從 Azure Data Factory 叫用 Spark 程式管線

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [Hive 活動](data-factory-hive-activity.md)
> * [Pig 活動](data-factory-pig-activity.md)
> * [MapReduce 活動](data-factory-map-reduce.md)
> * [Hadoop 串流活動](data-factory-hadoop-streaming-activity.md)
> * [Spark 活動](data-factory-spark.md)
> * [Machine Learning Batch 執行活動](data-factory-azure-ml-batch-execution-activity.md)
> * [Machine Learning 更新資源活動](data-factory-azure-ml-update-resource-activity.md)
> * [預存程序活動](data-factory-stored-proc-activity.md)
> * [Data Lake Analytics U-SQL 活動](data-factory-usql-activity.md)
> * [.NET 自訂活動](data-factory-use-custom-activities.md)

## <a name="introduction"></a>簡介
Spark 活動是其中一個 hello[資料轉換活動](data-factory-data-transformation-activities.md)受到 Azure Data Factory。 此活動可執行 hello 指定您的 Apache Spark 叢集，在 Azure HDInsight 上的 Spark 程式。    

> [!IMPORTANT]
> - Spark 活動不支援 Azure Data Lake Store 作為主要儲存體的 HDInsight Spark 叢集。
> - Spark 活動僅支援現有 (您自己的) HDInsight Spark 叢集。 它不支援隨選 HDInsight 連結服務。

## <a name="walkthrough-create-a-pipeline-with-spark-activity"></a>逐步解說：使用 Spark 活動建立管線
以下是 hello 的一般步驟 toocreate Data Factory 管線與 Spark 活動。  

1. 建立資料處理站。
2. 建立 Azure 儲存體連結服務 toolink 您與您的 HDInsight Spark 叢集 toohello data factory 相關聯的 Azure 儲存體。     
2. Azure HDInsight toohello data factory 中建立 Azure HDInsight 連結服務 toolink Apache Spark 叢集。
3. 建立資料集，是指 toohello Azure 儲存體連結服務。 目前，您必須指定活動的輸出資料集，即使沒有產生任何輸出。  
4. 是指在 #2 中建立的 toohello HDInsight 連結服務的 Spark 活動建立的管線。 hello 活動與 hello hello 做為輸出資料集的上一個步驟中建立的資料集設定。 hello 輸出資料集是哪些磁碟機 hello 排程 （每小時、 每天、 等等）。 因此，您必須指定 hello 輸出資料集，即使 hello 活動實際上也不會產生輸出。

### <a name="prerequisites"></a>必要條件
1. 建立**一般用途的 Azure 儲存體帳戶**依照 hello 逐步解說中的指示：[建立儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)。  
2. 建立**Azure HDInsight 中的 Apache Spark 叢集**依照 hello 教學課程中的指示： [Azure HDInsight 中建立的 Apache Spark 叢集](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md)。 將您建立與此叢集的步驟 1 中的 hello Azure 儲存體帳戶。  
3. 下載並檢閱 hello python 指令碼檔案**test.py**位於： [https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py](https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py)。  
3.  上傳**test.py** toohello **pyFiles**資料夾中 hello **adfspark**您的 Azure Blob 儲存體容器中。 如果它們尚不存在，請建立 hello 容器和 hello 資料夾。

### <a name="create-data-factory"></a>建立 Data Factory
讓我們開始在此步驟中建立 hello 資料 factory。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com/)。
2. 按一下**新增**hello 左窗格中，按一下 **資料 + 分析**，然後按一下**Data Factory**。
3. 在 hello**新的 data factory**刀鋒視窗中，輸入**SparkDF** hello 名稱。

   > [!IMPORTANT]
   > hello hello Azure data factory 的名稱必須是**全域唯一**。 如果您看到 hello 錯誤： **Data factory 名稱"SparkDF"不是使用**。 變更 hello 名稱 hello 資料處理站 （例如，yournameSparkDFdate，然後再次嘗試重新建立。 請參閱 [Data Factory - 命名規則](data-factory-naming-rules.md) 主題，以了解 Data Factory 成品的命名規則。   
4. 選取 hello **Azure 訂用帳戶**您想要建立 hello 資料 factory toobe。
5. 請選取現有的**資源群組**，或建立 Azure 資源群組。
6. 選取**Pin toodashboard**選項。  
6. 按一下**建立**上 hello**新的 data factory**刀鋒視窗。

   > [!IMPORTANT]
   > toocreate Data Factory 執行個體，您必須是成員的 hello[資料 Factory 參與者](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor)hello 訂用帳戶/資源群組層級角色。
7. 您會看到 hello hello 中建立的資料處理站**儀表板**的 hello Azure 入口網站，如下所示：   
8. 已成功建立 hello 資料處理站之後，您會看到 hello 資料 factory 頁面上，它會顯示 hello hello data factory 的內容。 如果看不到 hello 資料 factory 頁面上，按一下您 hello 儀表板上的 data factory 的 hello 磚。

    ![Data Factory 刀鋒視窗](./media/data-factory-spark/data-factory-blade.png)

### <a name="create-linked-services"></a>建立連結的服務
在此步驟中，您可以建立兩個連結的服務，一個 toolink 您的 Spark 叢集 tooyour 的 data factory，，和 hello 其他 toolink 您 Azure 儲存體 tooyour data factory。  

#### <a name="create-azure-storage-linked-service"></a>建立 Azure 儲存體連結服務
在此步驟中，您必須連結您的 Azure 儲存體帳戶 tooyour data factory。 您稍後在本逐步解說步驟中建立資料集是指 toothis 連結服務。 您在 hello 下一個步驟中定義 HDInsight 連結服務的 hello 太參考 toothis 連結服務。  

1. 按一下**作者及部署**上 hello **Data Factory** data factory 的刀鋒視窗。 您應該會看到 hello Data Factory 編輯器。
2. 按一下 [新增資料存放區] 並選擇 [Azure 儲存體]。

   ![新增資料存放區 - Azure 儲存體 - 功能表](./media/data-factory-spark/new-data-store-azure-storage-menu.png)
3. 您應該會看見 hello **JSON 指令碼**建立 Azure 儲存體已連結的 hello 編輯器中的服務。

   ![Azure 儲存體連結服務](./media/data-factory-build-your-first-pipeline-using-editor/azure-storage-linked-service.png)
4. 取代**帳戶名稱**和**帳戶金鑰**與 hello Azure 儲存體帳戶名稱和存取金鑰。 toolearn 如何 tooget 您的儲存體存取金鑰，請參閱有關如何 tooview、 複製和重新產生儲存體存取金鑰中的 hello 資訊[管理您的儲存體帳戶](../storage/common/storage-create-storage-account.md#manage-your-storage-account)。
5. toodeploy hello 連結的服務中，按一下**部署**hello 命令列上。 Hello 連結的服務已成功部署之後，hello **Draft 1**視窗應該就會消失，而且您會看到**AzureStorageLinkedService** hello hello 左側的樹狀檢視中。

#### <a name="create-hdinsight-linked-service"></a>建立 HDInsight 連結服務
在此步驟中，您建立 Azure HDInsight 連結服務 toolink 您 HDInsight Spark 叢集 toohello 的 data factory。 hello HDInsight 叢集是使用的 toorun hello Spark 程式 hello 管線，在此範例中的 hello Spark 活動中指定。  

1. 按一下**...多個**hello 工具列上，按一下**新計算**，然後按一下 **HDInsight 叢集**。

    ![建立 HDInsight 連結服務](media/data-factory-spark/new-hdinsight-linked-service.png)
2. 複製並貼上下列程式碼片段 toohello hello **Draft 1**視窗。 在 hello JSON 編輯器中，請勿 hello 下列步驟：
    1. 指定 hello **URI** hello HDInsight Spark 叢集。 例如： `https://<sparkclustername>.azurehdinsight.net/`。
    2. 指定的 hello hello 名稱**使用者**誰存取 toohello Spark 叢集。
    3. 指定 hello**密碼**使用者。
    4. 指定 hello **Azure 儲存體連結服務**與 hello HDInsight Spark 叢集相關聯。 在此範例中，它是：**AzureStorageLinkedService**。

    ```json
    {
        "name": "HDInsightLinkedService",
        "properties": {
            "type": "HDInsight",
            "typeProperties": {
                "clusterUri": "https://<sparkclustername>.azurehdinsight.net/",
                "userName": "admin",
                "password": "**********",
                "linkedServiceName": "AzureStorageLinkedService"
            }
        }
    }
    ```

    > [!IMPORTANT]
    > - Spark 活動不支援 Azure Data Lake Store 作為主要儲存體的 HDInsight Spark 叢集。
    > - Spark 活動僅支援現有 (您自己的) HDInsight Spark 叢集。 它不支援隨選 HDInsight 連結服務。

    請參閱[HDInsight 連結服務](data-factory-compute-linked-services.md#azure-hdinsight-linked-service)如需詳細資訊 hello HDInsight 連結服務。
3.  toodeploy hello 連結的服務中，按一下**部署**hello 命令列上。  

### <a name="create-output-dataset"></a>建立輸出資料集
hello 輸出資料集是哪些磁碟機 hello 排程 （每小時、 每天、 等等）。 因此，您必須指定 hello spark 活動的輸出資料集 hello 管線中，即使 hello 活動不會真的產生任何輸出。 指定 hello 活動的輸入資料集是選擇性的。

1. 在 hello **Data Factory 編輯器**，按一下  **...多個**hello 命令列上，按一下**新的資料集**，然後選取**Azure Blob 儲存體**。  
2. 複製並貼上下列程式碼片段 toohello Draft 1 視窗 hello。 hello JSON 片段會定義資料集稱為**OutputDataset**。 此外，您可以指定 hello 結果會儲存在稱為 hello blob 容器**adfspark**和 hello 資料夾稱為**pyFiles/輸出**。 如先前所述，此資料集是空的資料集。 在此範例中的 hello Spark 程式不會產生任何輸出。 hello**可用性**區段會指定每天產生該 hello 輸出資料集。  

    ```json
    {
        "name": "OutputDataset",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "fileName": "sparkoutput.txt",
                "folderPath": "adfspark/pyFiles/output",
                "format": {
                    "type": "TextFormat",
                    "columnDelimiter": "\t"
                }
            },
            "availability": {
                "frequency": "Day",
                "interval": 1
            }
        }
    }
    ```
3. toodeploy hello 資料集，請按一下**部署**hello 命令列上。


### <a name="create-pipeline"></a>建立管線
在此步驟中，您會建立具有 **HDInsightSpark** 活動的管線。 目前，輸出資料集是哪些磁碟機 hello 排程，因此您必須建立輸出資料集，即使 hello 活動不會產生任何輸出。 如果 hello 活動不接受任何輸入，您可以略過建立 hello 輸入資料集。 因此，在此範例中不會指定任何輸入資料集。

1. 在 hello **Data Factory 編輯器**，按一下  **...多個**在 hello 命令列，然後按一下**新管線**。
2. 取代下列指令碼的 hello hello Draft 1 視窗中的 hello 指令碼：

    ```json
    {
        "name": "SparkPipeline",
        "properties": {
            "activities": [
                {
                    "type": "HDInsightSpark",
                    "typeProperties": {
                        "rootPath": "adfspark\\pyFiles",
                        "entryFilePath": "test.py",
                        "getDebugInfo": "Always"
                    },
                    "outputs": [
                        {
                            "name": "OutputDataset"
                        }
                    ],
                    "name": "MySparkActivity",
                    "linkedServiceName": "HDInsightLinkedService"
                }
            ],
            "start": "2017-02-05T00:00:00Z",
            "end": "2017-02-06T00:00:00Z"
        }
    }
    ```
    請注意下列點 hello:
    - hello**類型**屬性設定太**HDInsightSpark**。
    - hello **rootPath**設定得**adfspark\\pyFiles** adfspark 所在 hello Azure Blob 容器和 pyFiles 是正常的資料夾，該容器中。 在此範例中，hello Azure Blob 儲存體是 hello 與 hello Spark 叢集相關聯的其中一個。 您可以上傳 hello 檔案 tooa 不同的 Azure 儲存體。 如果您這樣做，請建立 Azure 儲存體連結服務 toolink 該儲存體帳戶 toohello 資料 factory。 然後，指定 hello hello 連結服務名稱做為 hello 值**sparkJobLinkedService**屬性。 請參閱[Spark 活動屬性](#spark-activity-properties)如需詳細資訊，這個屬性，而且支援 hello Spark 活動的其他內容。  
    - hello **entryFilePath**設定 toohello **test.py**，這是 hello python 檔案。
    - hello **getDebugInfo**屬性設定太**永遠**，這表示 hello 記錄檔一律會產生 （成功或失敗）。

        > [!IMPORTANT]
        > 我們建議您不要設定此屬性太`Always`實際執行環境中除非您疑難排解問題。
    - hello**輸出**區段具有一個輸出資料集。 您必須指定輸出資料集，即使 hello spark 程式不會產生任何輸出。 hello 輸出資料集的磁碟機 hello 排程 hello 管線 （每小時、 每天、 等等）。  

        如需支援的 Spark 活動 hello 屬性的詳細資訊，請參閱[二手活動屬性](#spark-activity-properties)> 一節。
3. toodeploy hello 管線中，按一下 **部署**hello 命令列上。

### <a name="monitor-pipeline"></a>監視管線
1. 按一下**X** tooclose Data Factory 編輯器刀鋒 toonavigate 回 toohello Data Factory 的首頁。 按一下**監視和管理**toolaunch hello 監視另一個索引標籤中的應用程式。

    ![監視及管理圖格](media/data-factory-spark/monitor-and-manage-tile.png)
2. 變更 hello**開始時間**太篩選 hello 頂端**2/1/2017年**，然後按一下**套用**。
3. 因為沒有 hello 之間只有一天開始 (2017年-02-01) 和結束時間 (2017年-02-02) 的 hello 管線，您應該看到只有一個活動視窗。 確認該 hello 資料配量處於**準備**狀態。

    ![監視 hello 管線](media/data-factory-spark/monitor-and-manage-app.png)    
4. 選取 hello**活動視窗**toosee hello 活動執行詳細資料。 如果沒有發生錯誤，您會看到資訊，請參閱 hello 右窗格中的詳細資料。

### <a name="verify-hello-results"></a>請確認 hello 結果

1. 瀏覽至 https://CLUSTERNAME.azurehdinsight.net/jupyter，啟動您的 HDInsight Spark 叢集的 **Jupyter Notebook**。 您可以為 HDInsight Spark 叢集啟動叢集儀表板，然後啟動 **Jupyter Notebook**。
2. 按一下**新增** -> **PySpark** toostart 新的記事本。

    ![Jupyter 新筆記本](media/data-factory-spark/jupyter-new-book.png)
3. 執行 hello 下列命令複製/貼上的 hello 文字，然後按**SHIFT + ENTER** hello hello 第二個陳述式結尾處。  

    ```sql
    %%sql

    SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"
    ```
4. 確認您看到 hello hello hvac 資料表的資料：  

    ![Jupyter 查詢結果](media/data-factory-spark/jupyter-notebook-results.png)

如需詳細指示，請參閱[執行 Spark SQL 查詢](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md#run-a-hive-query-using-spark-sql)區段。 

### <a name="troubleshooting"></a>疑難排解
因為您設定**getDebugInfo**太**永遠**，您會看到**記錄**子資料夾中 hello **pyFiles** Azure Blob 容器中的資料夾。 hello hello 記錄檔資料夾中的記錄檔會提供其他詳細資料。 發生錯誤時，此記錄檔特別有用。 在實際執行環境中，您可能會想 tooset 它太**失敗**。

如需進一步疑難排解，請勿 hello 下列步驟：


1. 瀏覽過`https://<CLUSTERNAME>.azurehdinsight.net/yarnui/hn/cluster`。

    ![YARN UI 應用程式](media/data-factory-spark/yarnui-application.png)  
2. 按一下**記錄**hello 其中執行的嘗試。

    ![應用程式頁面](media/data-factory-spark/yarn-applications.png)
3. 您應該會看到 hello 記錄 頁面中的其他錯誤資訊。

    ![記錄錯誤](media/data-factory-spark/yarnui-application-error.png)

hello 下列各節提供有關 Data Factory 實體 toouse Apache Spark 叢集以及您的 data factory 中的 Spark 活動資訊。

## <a name="spark-activity-properties"></a>Spark 活動屬性
以下是管線 Spark 活動與 hello 範例 JSON 定義：    

```json
{
    "name": "SparkPipeline",
    "properties": {
        "activities": [
            {
                "type": "HDInsightSpark",
                "typeProperties": {
                    "rootPath": "adfspark\\pyFiles",
                    "entryFilePath": "test.py",
                    "arguments": [ "arg1", "arg2" ],
                    "sparkConfig": {
                        "spark.python.worker.memory": "512m"
                    }
                    "getDebugInfo": "Always"
                },
                "outputs": [
                    {
                        "name": "OutputDataset"
                    }
                ],
                "name": "MySparkActivity",
                "description": "This activity invokes hello Spark program",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-02-01T00:00:00Z",
        "end": "2017-02-02T00:00:00Z"
    }
}
```

hello 下表描述 hello hello JSON 定義中使用的 JSON 屬性：

| 屬性 | 說明 | 必要 |
| -------- | ----------- | -------- |
| 名稱 | Hello 管線中的 hello 活動名稱。 | 是 |
| 說明 | 會描述 hello 活動的文字。 | 否 |
| 類型 | 這個屬性必須設定 tooHDInsightSpark。 | 是 |
| linkedServiceName | 名稱 hello HDInsight 連結的服務的 hello Spark 執行程式。 | 是 |
| rootPath | hello Azure Blob 容器，並包含 hello Spark 檔案的資料夾。 hello 檔案名稱是區分大小寫。 | 是 |
| entryFilePath | 相對路徑 toohello 的 hello Spark 程式碼/封裝的根資料夾。 | 是 |
| className | 應用程式的 Java/Spark 主要類別 | 否 |
| arguments | 命令列引數 toohello Spark 程式的清單。 | 否 |
| proxyUser | hello 使用者帳戶 tooimpersonate tooexecute hello Spark 程式 | 否 |
| sparkConfig | 指定的 Spark hello 主題中列出的組態屬性值： [Spark 設定-應用程式屬性](https://spark.apache.org/docs/latest/configuration.html#available-properties)。 | 否 |
| getDebugInfo | 指定當 hello Spark 記錄檔會複製的 toohello HDInsight 叢集所使用的 Azure 儲存體 （或） sparkJobLinkedService 所指定。 允許的值︰None、Always 或 Failure。 預設值：None。 | 否 |
| sparkJobLinkedService | hello Azure 儲存體連結服務的 hello Spark 工作檔案、 相依性，以及記錄檔。  如果您未指定此屬性的值，則會使用 hello 與 HDInsight 叢集相關聯的儲存體。 | 否 |

## <a name="folder-structure"></a>資料夾結構
hello Spark 活動不支援內嵌指令碼，成為 Pig 和 Hive 活動執行。 Spark 作業也比 Pig/Hive 作業更具擴充性。 Spark 工作，您可以提供多個相依性例如 jar 封裝 （hello java CLASSPATH 中放置）、 python 檔案 （置於 hello PYTHONPATH 上），以及任何其他檔案。

建立下列資料夾結構 hello hello HDInsight 連結服務所參考的 Azure Blob 儲存體中的 hello。 然後上, 傳所代表的 hello 根資料夾中的相依檔案 toohello 適當的子資料夾**entryFilePath**。 例如上, 傳 python 檔案 toohello pyFiles 子資料夾和 jar 檔案 toohello （每瓶） 的子資料夾 hello 根資料夾。 在執行階段，Data Factory 服務預期具備下列資料夾結構 hello Azure Blob 儲存體中的 hello:     

| Path | 說明 | 必要 | 類型 |
| ---- | ----------- | -------- | ---- |
| . | hello 儲存體連結服務中的 hello Spark 作業 hello 根路徑    | 是 | 資料夾 |
| &lt;使用者定義&gt; | hello 指向 toohello hello Spark 工作項目檔案的路徑 | 是 | 檔案 |
| ./jars | 在這個資料夾底下的所有檔案會上傳並放在 hello 叢集的 hello java classpath | 否 | 資料夾 |
| ./pyFiles | 在這個資料夾底下的所有檔案會上傳並放在 hello PYTHONPATH hello 叢集的 | 否 | 資料夾 |
| ./files | 此資料夾下的所有檔案會上傳並放在執行程式工作目錄 | 否 | 資料夾 |
| ./archives | 此資料夾下的所有檔案未壓縮 | 否 | 資料夾 |
| ./logs | hello 儲存來自 hello Spark 叢集記錄檔的資料夾。| 否 | 資料夾 |

以下是包含兩個 hello hello HDInsight 連結服務所參考的 Azure Blob 儲存體中的 Spark 工作檔案的儲存體的範例。

```
SparkJob1
    main.jar
    files
        input1.txt
        input2.txt
    jars
        package1.jar
        package2.jar
    logs

SparkJob2
    main.py
    pyFiles
        scrip1.py
        script2.py
    logs
```
