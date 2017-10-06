---
title: "教學課程：使用 Visual Studio 建立具有複製活動的管線 | Microsoft Docs"
description: "在本教學課程中，您會使用 Visual Studio，建立具有複製活動的 Azure Data Factory 管線。"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 1751185b-ce0a-4ab2-a9c3-e37b4d149ca3
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: d99d8875807bab41f5122ab95a09f83f82923529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-visual-studio"></a>教學課程：使用 Visual Studio 建立具有複製活動的管線
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

在本文中，您學會如何 toouse 會 hello Microsoft Visual Studio toocreate data factory 管線，將資料從 Azure blob 儲存體 tooan Azure SQL database 複製。 如果您是新 tooAzure Data Factory，閱讀 hello[簡介 tooAzure Data Factory](data-factory-introduction.md)發行項，然後再執行本教學課程。   

在本教學課程中，您可以建立包含一個活動的管線：複製活動。 hello 複製活動會將資料從支援的資料存放區 tooa 支援的接收資料存放區。 如需作為來源和接收區支援的資料存放區清單，請參閱[支援的資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)。 hello 活動被提供安全、 可靠且可擴充的方式的各種資料存放區之間的資料可以複製的全域可用服務。 如需 hello 複製活動的詳細資訊，請參閱[資料移動活動](data-factory-data-movement-activities.md)。

一個管線中可以有多個活動。 此外，您可以藉由設定 hello 輸出資料集的一個活動 hello 的輸入資料集的 hello 其他活動鏈結 （執行一個活動執行另一個之後） 的兩個活動。 如需詳細資訊，請參閱[管線中的多個活動](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline)。

> [!NOTE] 
> 在此教學課程中的 hello 資料管線會將資料從來源資料存放區 tooa 目的地資料存放區。 如需如何使用 Azure Data Factory，tootransform 資料，請參閱[教學課程： 建立使用 Hadoop 叢集管線 tootransform 資料](data-factory-build-your-first-pipeline.md)。

## <a name="prerequisites"></a>必要條件
1. 閱讀[教學課程概觀](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)文件，以及完成 hello**必要條件**步驟。       
2. toocreate Data Factory 執行個體，您必須是成員的 hello[資料 Factory 參與者](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor)hello 訂用帳戶/資源群組層級角色。
3. 您必須擁有您電腦上安裝的 hello 下列： 
   * Visual Studio 2013 或 Visual Studio 2015
   * 下載 Azure SDK for Visual Studio 2013 或 Visual Studio 2015。 瀏覽過[Azure 下載頁面](https://azure.microsoft.com/downloads/)按一下**VS 2013**或**VS 2015**在 hello **.NET** > 一節。
   * 下載最新 Azure Data Factory 外掛程式 hello for Visual Studio: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5)或[VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005)。 您也可以執行下列步驟的 hello 更新 hello 外掛程式： hello 功能表上，按一下**工具** -> **擴充功能和更新** -> **線上** ->  **Visual Studio 組件庫** -> **Microsoft Azure Data Factory Tools for Visual Studio** -> **更新**。

## <a name="steps"></a>步驟
以下是您執行本教學課程的一部分的 hello 步驟：

1. 建立**連結的服務**hello data factory 中。 在此步驟中，您會建立兩種連結服務：Azure 儲存體和 Azure SQL Database。 
    
    hello AzureStorageLinkedService 連結您的 Azure 儲存體帳戶 toohello data factory。 您在建立容器，並在上傳資料 toothis 儲存體帳戶的[必要條件](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。   

    AzureSqlLinkedService 連結您的 Azure SQL database toohello data factory。 複製 hello blob 儲存體中的 hello 資料會儲存在資料庫中。 您在此資料庫中建立了 SQL 資料表，作為[必要條件](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)的一部分。     
2. 建立輸入和輸出**資料集**hello data factory 中。  
    
    hello Azure 儲存體連結服務指定 Data Factory 服務會使用在執行的階段 tooconnect tooyour Azure 儲存體帳戶的 hello 連接字串。 此外，hello 輸入的 blob 資料集會指定 hello 容器和包含 hello 輸入的資料的 hello 資料夾。  

    同樣地，hello 連結的 Azure SQL Database 服務指定 hello Data Factory 服務會使用在執行的階段 tooconnect tooyour Azure SQL database 的連接字串。 此外，hello 輸出 SQL 資料表的資料集指定複製 hello hello 資料庫 toowhich hello 資料從 hello blob 儲存體中的資料表。
3. 建立**管線**hello data factory 中。 在此步驟中，您會建立具有複製活動的管線。   
    
    hello 複製活動會將資料從 hello Azure SQL database 中 hello Azure blob 儲存體 tooa 資料表中的 blob。 您可以從任何支援的來源支援 tooany 目的地管線 toocopy 資料中使用複製活動。 如需支援的資料存放區清單，請參閱[資料移動活動](data-factory-data-movement-activities.md#supported-data-stores-and-formats)一文。 
4. 在部署 Data Factory 實體 (連結服務、資料集/資料表和管線) 時，建立 Azure **Data Factory**。 

## <a name="create-visual-studio-project"></a>建立 Visual Studio 專案
1. 啟動 **Visual Studio 2015**。 按一下**檔案**，點太**新增**，然後按一下**專案**。 您應該會看見 hello**新專案** 對話方塊。  
2. 在 hello**新專案**對話方塊中，選取 hello **DataFactory**範本，然後按一下**空白資料處理站專案**。  
   
    ![[新增專案] 對話方塊](./media/data-factory-copy-activity-tutorial-using-visual-studio/new-project-dialog.png)
3. 指定 hello 名稱 hello 專案、 hello 方案位置以及 hello 方案的名稱，然後按一下**確定**。
   
    ![Solution Explorer](./media/data-factory-copy-activity-tutorial-using-visual-studio/solution-explorer.png)    

## <a name="create-linked-services"></a>建立連結的服務
您可以建立連結的服務中的資料處理站 toolink 資料儲存和運算服務 toohello 資料 factory。 在本教學課程中，您不會使用任何計算服務，例如 Azure HDInsight 或 Azure Data Lake Analytics。 您可以使用兩種類型的資料存放區：Azure 儲存體 (來源) 和 Azure SQL Database (目的地)。 

因此，您會建立兩種連結服務：AzureStorage 和 AzureSqlDatabase。  

hello Azure 儲存體連結服務連結您的 Azure 儲存體帳戶 toohello data factory。 這個儲存體帳戶為其中一個 hello 在其中建立容器及 hello 資料上傳的過程[必要條件](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。   

Azure SQL 連結服務連結您的 Azure SQL database toohello data factory。 複製 hello blob 儲存體中的 hello 資料會儲存在資料庫中。 在此資料庫中建立 hello emp 資料表的一部分[必要條件](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。

連結的服務將資料存放區，或計算服務 tooan 的 Azure data factory。 請參閱[支援資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)針對所有 hello 來源與接收支援 hello 複製活動。 請參閱[計算連結的服務](data-factory-compute-linked-services.md)hello 的 Data Factory 支援的計算服務的清單。 在本教學課程中，您不會使用任何計算服務。 

### <a name="create-hello-azure-storage-linked-service"></a>建立 hello Azure 儲存體連結服務
1. 在**方案總管 中**，以滑鼠右鍵按一下**連結的服務**，點太**新增**，然後按一下**新項目**。      
2. 在 hello**加入新項目**對話方塊中，選取**Azure 儲存體連結服務**從 hello 清單，然後按一下**新增**。 
   
    ![新的連結服務](./media/data-factory-copy-activity-tutorial-using-visual-studio/new-linked-service-dialog.png)
3. 取代`<accountname>`和`<accountkey>`* 與 hello 您 Azure 儲存體帳戶名稱和其索引鍵。 
   
    ![Azure 儲存體連結服務](./media/data-factory-copy-activity-tutorial-using-visual-studio/azure-storage-linked-service.png)
4. 儲存 hello **AzureStorageLinkedService1.json**檔案。

    如需在連結的 hello 服務定義中的 JSON 屬性的詳細資訊，請參閱[Azure Blob 儲存體連接器](data-factory-azure-blob-connector.md#linked-service-properties)發行項。

### <a name="create-hello-azure-sql-linked-service"></a>建立 hello Azure SQL 連結服務
1. 以滑鼠右鍵按一下**連結的服務**hello 中的節點**方案總管 中**同樣地，點太**新增**，然後按一下**新項目**。 
2. 這次，請選取 [Azure SQL 連結服務]，然後按一下 [新增]。 
3. 在 hello **AzureSqlLinkedService1.json 檔案**，取代`<servername>`， `<databasename>`， `<username@servername>`，和`<password>`與您 Azure SQL server、 資料庫、 使用者帳戶和密碼的名稱。    
4. 儲存 hello **AzureSqlLinkedService1.json**檔案。 
    
    如需這些 JSON 屬性的詳細資訊，請參閱 [Azure SQL Database 連接器](data-factory-azure-sql-connector.md#linked-service-properties)。


## <a name="create-datasets"></a>建立資料集
在 hello 先前步驟中，您會建立連結的服務 toolink，您的 Azure 儲存體帳戶和 Azure SQL database tooyour 資料 factory。 在此步驟中，您可以定義名為 InputDataset OutputDataset 代表輸入和輸出資料儲存在 hello 分別 AzureStorageLinkedService1 和 AzureSqlLinkedService1 所參考的資料存放區中的兩個資料集。

hello Azure 儲存體連結服務指定 Data Factory 服務會使用在執行的階段 tooconnect tooyour Azure 儲存體帳戶的 hello 連接字串。 此外，hello 輸入的 blob 資料集 (InputDataset) 指定 hello 容器和包含 hello 輸入的資料的 hello 資料夾。  

同樣地，hello 連結的 Azure SQL Database 服務指定 hello Data Factory 服務會使用在執行的階段 tooconnect tooyour Azure SQL database 的連接字串。 此外，hello 輸出 SQL 資料表資料集 (OututDataset) 會指定 hello 資料表中 hello 資料庫 toowhich hello hello blob 儲存體的資料複製。 

### <a name="create-input-dataset"></a>建立輸入資料集
在此步驟中，您建立資料集名為指向 tooa blob 檔案 (emp.txt) InputDataset hello 的 blob 容器 (adftutorial) 的根資料夾中 hello hello AzureStorageLinkedService1 連結服務所代表的 Azure 儲存體中。 如果您不指定 hello 檔名的值 （或略過它），從 hello 輸入資料夾中的所有 blob 資料，則複製的 toohello 目的地。 在本教學課程中，您可以指定 hello 檔案名稱的值。 

在這裡，您可以使用 hello 詞彙"tables"而不是 「 資料集 」。 資料表是矩形的資料集，並且是 hello 現在支援的資料集的唯一類型。 

1. 以滑鼠右鍵按一下**資料表**在 hello**方案總管 中**，點太**新增**，然後按一下**新項目**。
2. 在 hello**加入新項目**對話方塊中，選取**Azure Blob**，按一下**新增**。   
3. Hello JSON 文字取代成下列文字的 hello 和儲存 hello **AzureBlobLocation1.json**檔案。 

  ```json   
  {
    "name": "InputDataset",
    "properties": {
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
      "type": "AzureBlob",
      "linkedServiceName": "AzureStorageLinkedService1",
      "typeProperties": {
        "folderPath": "adftutorial/",
        "format": {
          "type": "TextFormat",
          "columnDelimiter": ","
        }
      },
      "external": true,
      "availability": {
        "frequency": "Hour",
        "interval": 1
      }
    }
  }
  ``` 
    hello 下表提供 hello hello 程式碼片段中使用的 JSON 屬性的說明：

    | 屬性 | 說明 |
    |:--- |:--- |
    | 類型 | hello type 屬性設定太**AzureBlob**因為資料常駐於 Azure blob 儲存體中。 |
    | linkedServiceName | 是指 toohello **AzureStorageLinkedService**您稍早建立的。 |
    | folderPath | 指定 hello blob**容器**和 hello**資料夾**，其中包含輸入的 blob。 在本教學課程，adftutorial hello blob 容器且資料夾是 hello 根資料夾。 | 
    | fileName | 這是選用屬性。 如果您省略這個屬性時，會挑出 hello folderPath 中的所有檔案。 在本教學課程， **emp.txt**指定了 hello 檔名，因此只有該檔案所挑選的處理。 |
    | format -> type |hello 輸入的檔為 hello 文字格式，因此我們使用**TextFormat**。 |
    | columnDelimiter | hello hello 輸入檔中的資料行分隔**逗號字元 (`,`)**。 |
    | frequency/interval | hello 頻率設定過**小時**和間隔設定得**1**，這表示該 hello 輸入配量可用**每小時**。 換句話說，hello Data Factory 服務會尋找輸入資料每小時的 blob 容器的 hello 根資料夾中 (**adftutorial**) 指定。 它會尋找 hello hello 管線開始和結束時間、 不之前或之後這段時間內的資料。  |
    | external | 這個屬性設定太**true**如果 hello 資料不會產生此管線。 在此教學課程中的 hello 輸入的資料是在 hello emp.txt 檔案，不會產生這個管線，因此我們設定此屬性 tootrue。 |

    如需這些 JSON 屬性的詳細資訊，請參閱 [Azure Blob 連接器](data-factory-azure-blob-connector.md#dataset-properties)一文。   

### <a name="create-output-dataset"></a>建立輸出資料集
在此步驟中，您會建立名為 **OutputDataset**的輸出資料集。 此資料集所代表的 hello Azure SQL database 中的點 tooa SQL 資料表**AzureSqlLinkedService1**。 

1. 以滑鼠右鍵按一下**資料表**在 hello**方案總管 中**同樣地，點太**新增**，然後按一下**新項目**。
2. 在 hello**加入新項目**對話方塊中，選取**Azure SQL**，按一下**新增**。 
3. Hello JSON 文字取代成下列 JSON hello 和儲存 hello **AzureSqlTableLocation1.json**檔案。

  ```json
    {
     "name": "OutputDataset",
     "properties": {
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
       "type": "AzureSqlTable",
       "linkedServiceName": "AzureSqlLinkedService1",
       "typeProperties": {
         "tableName": "emp"
       },
       "availability": {
         "frequency": "Hour",
         "interval": 1
       }
     }
    }
    ```
    hello 下表提供 hello hello 程式碼片段中使用的 JSON 屬性的說明：

    | 屬性 | 說明 |
    |:--- |:--- |
    | 類型 | hello type 屬性設定太**AzureSqlTable**因為資料是在 Azure SQL database 中的複製的 tooa 資料表。 |
    | linkedServiceName | 是指 toohello **AzureSqlLinkedService**您稍早建立的。 |
    | tableName | 指定的 hello**資料表**toowhich hello 資料複製。 | 
    | frequency/interval | hello 頻率設定過**小時**和間隔是**1**，這表示 hello 輸出配量所產生**每小時**之間 hello 管線開始和結束時間，不是在之前或之後這段時間。  |

    有三個資料行 –**識別碼**， **FirstName**，和**LastName** – hello 資料庫中的 hello emp 資料表中。 識別碼是識別資料行，所以您必須只 toospecify **FirstName**和**LastName**這裡。

    如需這些 JSON 屬性的詳細資訊，請參閱 [Azure SQL 連接器](data-factory-azure-sql-connector.md#dataset-properties)一文。

## <a name="create-pipeline"></a>建立管線
在此步驟中您會建立管線，其中含有使用 **InputDataset** 作為輸入和使用 **OutputDataset** 作為輸出的**複製活動**。

目前，輸出資料集是哪些磁碟機 hello 排程。 在本教學課程中，輸出資料集是設定的 tooproduce 配量小時一次。 hello 管線有開始時間和結束時間的一天分散，也就是 24 小時。 因此，hello 管線所產生的輸出資料集的 24 配量。 

1. 以滑鼠右鍵按一下**管線**在 hello**方案總管 中**，點太**新增**，然後按一下**新項目**。  
2. 選取**複製資料管線**在 hello**加入新項目**對話方塊，按一下**新增**。 
3. 取代下列 JSON hello hello JSON，並儲存 hello **CopyActivity1.json**檔案。

  ```json   
    {
     "name": "ADFTutorialPipeline",
     "properties": {
       "description": "Copy data from a blob tooAzure SQL table",
       "activities": [
         {
           "name": "CopyFromBlobToSQL",
           "type": "Copy",
           "inputs": [
             {
               "name": "InputDataset"
             }
           ],
           "outputs": [
             {
               "name": "OutputDataset"
             }
           ],
           "typeProperties": {
             "source": {
               "type": "BlobSource"
             },
             "sink": {
               "type": "SqlSink",
               "writeBatchSize": 10000,
               "writeBatchTimeout": "60:00:00"
             }
           },
           "Policy": {
             "concurrency": 1,
             "executionPriorityOrder": "NewestFirst",
             "style": "StartOfInterval",
             "retry": 0,
             "timeout": "01:00:00"
           }
         }
       ],
       "start": "2017-05-11T00:00:00Z",
       "end": "2017-05-12T00:00:00Z",
       "isPaused": false
     }
    }
    ```   
    - 在 [hello 活動] 區段中，沒有一個活動其**類型**設定得**複製**。 如需 hello 複製活動的詳細資訊，請參閱[資料移動活動](data-factory-data-movement-activities.md)。 在 Data Factory 解決方案中，您也可以使用[資料轉換活動](data-factory-data-transformation-activities.md)。
    - 輸入 hello 活動設定太**InputDataset**和輸出 hello 活動設定太**OutputDataset**。 
    - 在 [hello **typeProperties** ] 區段中， **BlobSource**指定 hello 來源類型為和**SqlSink**指定為 hello 接收器類型。 支援的 hello 複製活動做為來源與接收的資料存放區的完整清單，請參閱[支援資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)。 toolearn toouse 特定支援的資料如何儲存為來源/接收器，按一下 hello 資料表中的 hello 連結。  
     
    取代 hello hello 值**啟動**屬性以 hello 目前的日期和**結束**以 hello 隔天的值。 您可以指定 hello 日期部分，並略過 hello hello 時間部分日期時間。 例如，"2016年-02-03"，這相當於太"2016年-02-03T00:00:00Z"
     
    開始和結束日期時間都必須是 [ISO 格式](http://en.wikipedia.org/wiki/ISO_8601)。 例如：2016-10-14T16:32:41Z。 hello**結束**時間是選擇性的但我們在本教學課程中使用它。 
     
    如果您未指定值為 hello**結束**屬性，它會計算為"**start + 48 小時**"。 無限期地指定 toorun hello 管線**9999-09-09**為 hello hello 值**結束**屬性。
     
    在上述範例中的 hello，有 24 資料配量每小時產生每個資料分割。

    如需管線定義中 JSON 屬性的說明，請參閱[建立管線](data-factory-create-pipelines.md)一文。 如需複製活動定義中 JSON 屬性的說明，請參閱[資料移動活動](data-factory-data-movement-activities.md)。 如需 BlobSource 所支援 JSON 屬性的說明，請參閱 [Azure Blob 連接器](data-factory-azure-blob-connector.md)一文。 如需 SqlSink 支援的 JSON 屬性說明，請參閱 [Azure SQL Database 連接器](data-factory-azure-sql-connector.md)一文。

## <a name="publishdeploy-data-factory-entities"></a>發佈/部署 Data Factory 實體
在此步驟中，您會發佈稍早建立的 Data Factory 實體 (連結的服務、資料集和管線)。 您也可以指定新資料處理站 toobe hello hello 名稱建立 toohold 這些實體。  

1. 以滑鼠右鍵按一下專案 hello 方案總管] 中的，按一下 [**發行**。 
2. 如果您看到**登入 Microsoft 帳戶 tooyour**對話方塊中，hello 擁有帳戶的 Azure 訂用帳戶中，輸入您的認證，然後按一下**登入**。
3. 您應該會看到下列對話方塊中的 hello:
   
   ![發佈對話方塊](./media/data-factory-copy-activity-tutorial-using-visual-studio/publish.png)
4. Hello 設定資料 factory 頁面上，下列步驟 hello: 
   
   1. 選取 [建立新的 Data Factory]  選項。
   2. 針對 [名稱] 輸入 **VSTutorialFactory**。  
      
      > [!IMPORTANT]
      > hello hello Azure data factory 的名稱必須是全域唯一的。 如果發行時，您會收到一個錯誤 hello 的 data factory 的名稱，，變更 hello 名稱 hello 資料處理站 (例如，yournameVSTutorialFactory) 並再試一次發行一次。 請參閱 [Data Factory - 命名規則](data-factory-naming-rules.md) 主題，以了解 Data Factory 成品的命名規則。        
      > 
      > 
   3. 選取您的 Azure 訂閱 hello**訂用帳戶**欄位。
      
      > [!IMPORTANT]
      > 如果看不到任何訂用帳戶，請確定您登入是系統管理員或共同管理員的 hello 訂用帳戶的帳戶。  
      > 
      > 
   4. 選取 hello**資源群組**hello 資料 factory toobe 建立的。 
   5. 選取 hello**區域**hello data factory。 Hello 下拉式清單中會顯示 hello Data Factory 服務所支援的區域。
   6. 按一下**下一步**tooswitch toohello**發行的項目**頁面。
      
       ![設定 Data Factory 頁面](media/data-factory-copy-activity-tutorial-using-visual-studio/configure-data-factory-page.png)   
5. 在 [hello**發行的項目**頁面上，確定所有 hello Data Factory 實體已選取，然後按一下**下一步]** tooswitch toohello**摘要**頁面。
   
   ![發佈項目頁面](media/data-factory-copy-activity-tutorial-using-visual-studio/publish-items-page.png)     
6. 檢閱 hello 摘要，然後按一下**下一步**toostart hello 部署程序和檢視 hello**部署狀態**。
   
   ![發佈摘要頁面](media/data-factory-copy-activity-tutorial-using-visual-studio/publish-summary-page.png)
7. 在 [hello**部署狀態**] 頁面上，您應該會看到 hello hello 部署程序的狀態。 Hello 部署完成之後，請按一下 [完成]。
 
   ![部署狀態頁面](media/data-factory-copy-activity-tutorial-using-visual-studio/deployment-status.png)

請注意下列點 hello: 

* 如果您收到 hello 錯誤: 「 此訂用帳戶不是已註冊的 toouse 命名空間 Microsoft.DataFactory 」，請勿 hello 下列其中一種，再次嘗試重新發行： 
  
  * 在 Azure PowerShell，執行下列命令 tooregister hello Data Factory 提供者的 hello。 

    ```PowerShell    
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
    您可以執行下列命令 tooconfirm hello 該 hello Data Factory 提供者註冊。 
    
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * 登入使用 hello hello 到 Azure 訂用帳戶[Azure 入口網站](https://portal.azure.com)並瀏覽 tooa Data Factory 刀鋒視窗 （或） 在 hello Azure 入口網站中建立 data factory。 這個動作會自動註冊 hello 您的提供者。
* 可能會註冊為未來的 hello 中的 DNS 名稱，因此會變成可公開可見 hello hello data factory 名稱。

> [!IMPORTANT]
> toocreate Data Factory 執行個體，您需要 toobe hello Azure 訂用帳戶管理員/共同管理員

## <a name="monitor-pipeline"></a>監視管線
瀏覽您的 data factory toohello 首頁：

1. 登入太[Azure 入口網站](https://portal.azure.com)。
2. 按一下**更多服務**hello 左的窗格中，且按一下**Data factory**。

    ![瀏覽 Data Factory](media/data-factory-copy-activity-tutorial-using-visual-studio/browse-data-factories.png)
3. 開始輸入 hello 的 data factory 的名稱。

    ![資料處理站名稱](media/data-factory-copy-activity-tutorial-using-visual-studio/enter-data-factory-name.png) 
4. 按一下您的 data factory 中 hello 結果清單 toosee hello 首頁，即可供您的 data factory。

    ![Data Factory 首頁](media/data-factory-copy-activity-tutorial-using-visual-studio/data-factory-home-page.png)
5. 請依照下列指示從[監視資料集和管線](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline)toomonitor hello 管線和資料集已建立本教學課程中。 Visual Studio 目前不支援監視 Data Factory 管線。 

## <a name="summary"></a>摘要
在本教學課程中，您可以建立 Azure data factory toocopy 資料從 Azure blob tooan Azure SQL database。 您可以使用 Visual Studio toocreate hello 資料處理站、 連結的服務、 資料集和管線。 以下是您執行本教學課程中的 hello 高階步驟：  

1. 建立 Azure **Data Factory**。
2. 建立 **連結服務**：
   1. **Azure 儲存體**連結服務 toolink 您保留輸入的資料的 Azure 儲存體帳戶。     
   2. **Azure SQL**連結服務 toolink hello 輸出資料會保存您 Azure SQL database。 
3. 建立可描述管線輸入資料和輸出資料的 **資料集**。
4. 建立具有**複製活動**的**管線**，以 **BlobSource** 做為來源並以 **SqlSink** 做為接收器。 

如何 toouse HDInsight Hive 活動 tootransform 資料使用 Azure HDInsight 叢集，請參閱的 toosee[教學課程： 建立第一個管線 tootransform 資料使用 Hadoop 叢集](data-factory-build-your-first-pipeline.md)。

您可以藉由設定 hello 輸出資料集的一個活動 hello 的輸入資料集的 hello 其他活動鏈結 （執行一個活動執行另一個之後） 的兩個活動。 如需詳細資訊，請參閱[在 Data Factory 中排程和執行](data-factory-scheduling-and-execution.md)。 

## <a name="view-all-data-factories-in-server-explorer"></a>在 Server Explorer 中檢視所有資料處理站
本章節描述如何 toouse hello 伺服器總管，在 Visual Studio tooview 您 Azure 訂用帳戶中的所有都 hello data factory 及建立 Visual Studio 專案是根據現有的 data factory。 

1. 在**Visual Studio**，按一下 **檢視**在 hello 功能表，然後按一下**伺服器總管**。
2. 在 [hello 伺服器總管] 視窗中，展開**Azure**展開**Data Factory**。 如果您看到**登入 tooVisual Studio**，輸入 hello**帳戶**與您的 Azure 訂用帳戶，然後按一下相關聯**繼續**。 輸入**密碼**，然後按一下 [登入]。 Visual Studio 會嘗試 tooget 您訂用帳戶中的所有 Azure data factory 的資訊。 您看到這項作業在 hello hello 狀態**資料 Factory 工作清單**視窗。

    ![Server Explorer](./media/data-factory-copy-activity-tutorial-using-visual-studio/server-explorer.png)

## <a name="create-a-visual-studio-project-for-an-existing-data-factory"></a>建立現有資料處理站的 Visual Studio 專案

- 以滑鼠右鍵按一下伺服器總管中的資料處理站，然後選取**匯出 Data Factory tooNew 專案**toocreate Visual Studio 專案是根據現有的 data factory。

    ![匯出資料 factory tooa VS 專案](./media/data-factory-copy-activity-tutorial-using-visual-studio/export-data-factory-menu.png)  

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


## <a name="next-steps"></a>後續步驟
在本教學課程中，您可使用 Azure Blob 儲存體作為來源資料存放區以及使用 Azure SQL Database 作為複製作業的目的地資料存放區。 hello 下表提供 hello 複製活動支援做為來源和目的地資料存放區的清單： 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

關於如何 toocopy 資料，從資料存放區，toolearn 按一下 hello 連結 hello hello 資料表中的資料存放區。
