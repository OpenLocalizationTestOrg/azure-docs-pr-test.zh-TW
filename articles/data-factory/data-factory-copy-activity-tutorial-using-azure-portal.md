---
title: "教學課程： 建立 Azure Data Factory 管線 toocopy 資料 （Azure 入口網站） |Microsoft 文件"
description: "在本教學課程中，您可以使用 Azure 入口網站 toocreate Azure Data Factory 管線複製活動 toocopy 資料從 Azure blob 儲存體 tooan Azure SQL database。"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: d9317652-0170-4fd3-b9b2-37711272162b
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: fadd840fe9a15cd8831cdb25dccbd10ac42fa161
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-use-azure-portal-toocreate-a-data-factory-pipeline-toocopy-data"></a>教學課程： 使用 Azure 入口網站 toocreate Data Factory 管線 toocopy 資料 
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

在本文中，您將學習如何 toouse [Azure 入口網站](https://portal.azure.com)toocreate data factory 管線，將資料從 Azure blob 儲存體 tooan Azure SQL database 複製。 如果您是新 tooAzure Data Factory，閱讀 hello[簡介 tooAzure Data Factory](data-factory-introduction.md)發行項，然後再執行本教學課程。   

在本教學課程中，您可以建立包含一個活動的管線：複製活動。 hello 複製活動會將資料從支援的資料存放區 tooa 支援的接收資料存放區。 如需作為來源和接收區支援的資料存放區清單，請參閱[支援的資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)。 hello 活動被提供安全、 可靠且可擴充的方式的各種資料存放區之間的資料可以複製的全域可用服務。 如需 hello 複製活動的詳細資訊，請參閱[資料移動活動](data-factory-data-movement-activities.md)。

一個管線中可以有多個活動。 此外，您可以藉由設定 hello 輸出資料集的一個活動 hello 的輸入資料集的 hello 其他活動鏈結 （執行一個活動執行另一個之後） 的兩個活動。 如需詳細資訊，請參閱[管線中的多個活動](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline)。 

> [!NOTE] 
> 在此教學課程中的 hello 資料管線會將資料從來源資料存放區 tooa 目的地資料存放區。 如需如何使用 Azure Data Factory，tootransform 資料，請參閱[教學課程： 建立使用 Hadoop 叢集管線 tootransform 資料](data-factory-build-your-first-pipeline.md)。

## <a name="prerequisites"></a>必要條件
完成 hello 中所列必要條件[教學課程必要條件](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)發行項，然後再執行本教學課程。

## <a name="steps"></a>步驟
以下是您執行本教學課程的一部分的 hello 步驟：

1. 建立 Azure **Data Factory**。 在此步驟中，您會建立名為 ADFTutorialDataFactory 的資料處理站。 
2. 建立**連結的服務**hello data factory 中。 在此步驟中，您會建立兩種連結服務：Azure 儲存體和 Azure SQL Database。 
    
    hello AzureStorageLinkedService 連結您的 Azure 儲存體帳戶 toohello data factory。 您在建立容器，並在上傳資料 toothis 儲存體帳戶的[必要條件](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。   

    AzureSqlLinkedService 連結您的 Azure SQL database toohello data factory。 複製 hello blob 儲存體中的 hello 資料會儲存在資料庫中。 您在此資料庫中建立了 SQL 資料表，作為[必要條件](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)的一部分。   
3. 建立輸入和輸出**資料集**hello data factory 中。  
    
    hello Azure 儲存體連結服務指定 Data Factory 服務會使用在執行的階段 tooconnect tooyour Azure 儲存體帳戶的 hello 連接字串。 此外，hello 輸入的 blob 資料集會指定 hello 容器和包含 hello 輸入的資料的 hello 資料夾。  

    同樣地，hello 連結的 Azure SQL Database 服務指定 hello Data Factory 服務會使用在執行的階段 tooconnect tooyour Azure SQL database 的連接字串。 此外，hello 輸出 SQL 資料表的資料集指定複製 hello hello 資料庫 toowhich hello 資料從 hello blob 儲存體中的資料表。
4. 建立**管線**hello data factory 中。 在此步驟中，您會建立具有複製活動的管線。   
    
    hello 複製活動會將資料從 hello Azure SQL database 中 hello Azure blob 儲存體 tooa 資料表中的 blob。 您可以從任何支援的來源支援 tooany 目的地管線 toocopy 資料中使用複製活動。 如需支援的資料存放區清單，請參閱[資料移動活動](data-factory-data-movement-activities.md#supported-data-stores-and-formats)一文。 
5. 監視 hello 管線。 在此步驟中，您**監視器**hello 的輸入和輸出資料集配量，使用 Azure 入口網站。 

## <a name="create-data-factory"></a>建立 Data Factory
> [!IMPORTANT]
> 完成[hello 教學課程的必要條件](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)如果您還沒有。   

資料處理站可以有一或多個管線。 其中的管線可以有一或多個活動。 例如，複製活動 toocopy 資料從來源 tooa 目的地資料存放區和 HDInsight Hive 活動 toorun Hive 指令碼 tootransform 輸入資料 tooproduct 輸出資料。 讓我們開始在此步驟中建立 hello 資料 factory。

1. 登入 toohello 之後[Azure 入口網站](https://portal.azure.com/)，按一下 **新增**hello 左窗格中，按一下 **資料 + 分析**，然後按一下**Data Factory**。 
   
   ![新增->DataFactory](./media/data-factory-copy-activity-tutorial-using-azure-portal/NewDataFactoryMenu.png)    
2. 在 hello**新的 data factory**刀鋒視窗中：
   
   1. 輸入**ADFTutorialDataFactory** hello**名稱**。 
      
         ![新增 Data Factory 刀鋒視窗](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-new-data-factory.png)
      
       hello hello Azure data factory 的名稱必須是**全域唯一**。 如果您收到下列錯誤 hello，變更 hello 名稱 hello 資料處理站 (例如，yournameADFTutorialDataFactory)，然後再次嘗試重新建立。 請參閱 [Data Factory - 命名規則](data-factory-naming-rules.md) 主題，以了解 Data Factory 成品的命名規則。
      
           Data factory name “ADFTutorialDataFactory” is not available  
      
       ![Data Factory 名稱無法使用](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-data-factory-not-available.png)
   2. 選取您的 Azure**訂用帳戶**想 toocreate hello 資料 factory。 
   3. Hello**資源群組**，執行下列步驟的 hello 其中一項：
      
      - 選取**使用現有**，並從 hello 下拉式清單中選取現有的資源群組。 
      - 選取**建立新**，然後輸入 hello 資源群組名稱。   
         
          部分 hello 步驟在本教學課程假設您使用 hello 名稱： **ADFTutorialResourceGroup** hello 資源群組。 toolearn 解資源群組，請參閱[資源使用您的 Azure 資源群組 toomanage](../azure-resource-manager/resource-group-overview.md)。  
   4. 選取 hello**位置**hello data factory。 Hello 下拉式清單中會顯示 hello Data Factory 服務所支援的區域。
   5. 選取**Pin toodashboard**。     
   6. 按一下 [建立] 。
      
      > [!IMPORTANT]
      > toocreate Data Factory 執行個體，您必須是成員的 hello[資料 Factory 參與者](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor)hello 訂用帳戶/資源群組層級角色。
      > 
      > 可能會註冊為未來的 hello 中的 DNS 名稱，因此會變成可公開可見 hello hello data factory 名稱。                
      > 
      > 
3. 在 hello 儀表板，您會看到狀態磚的 hello 下列：**部署資料處理站**。 

    ![部署資料處理站圖格](media/data-factory-copy-activity-tutorial-using-azure-portal/deploying-data-factory.png)
4. Hello 建立完成之後，您會看到 hello **Data Factory**刀鋒視窗中 hello 影像所示。
   
   ![Data Factory 首頁](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-data-factory-home-page.png)

## <a name="create-linked-services"></a>建立連結的服務
您可以建立連結的服務中的資料處理站 toolink 資料儲存和運算服務 toohello 資料 factory。 在本教學課程中，您不會使用任何計算服務，例如 Azure HDInsight 或 Azure Data Lake Analytics。 您可以使用兩種類型的資料存放區：Azure 儲存體 (來源) 和 Azure SQL Database (目的地)。 

因此，您可以建立名為 AzureStorageLinkedService 和 AzureSqlLinkedService 的兩個連結服務︰類型為 AzureStorage 和 AzureSqlDatabase。  

hello AzureStorageLinkedService 連結您的 Azure 儲存體帳戶 toohello data factory。 這個儲存體帳戶為其中一個 hello 在其中建立容器及 hello 資料上傳的過程[必要條件](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。   

AzureSqlLinkedService 連結您的 Azure SQL database toohello data factory。 複製 hello blob 儲存體中的 hello 資料會儲存在資料庫中。 在此資料庫中建立 hello emp 資料表的一部分[必要條件](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。  

### <a name="create-azure-storage-linked-service"></a>建立 Azure 儲存體連結服務
在此步驟中，您必須連結您的 Azure 儲存體帳戶 tooyour data factory。 您可以在此區段中指定 hello 名稱和您的 Azure 儲存體帳戶金鑰。  

1. 在 hello **Data Factory**刀鋒視窗中，按一下 **作者及部署**磚。
   
   ![[製作和部署] 磚](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-author-deploy-tile.png) 
2. 您會看到 hello **Data Factory 編輯器**hello 下列影像所示： 

    ![Data Factory 編輯器](./media/data-factory-copy-activity-tutorial-using-azure-portal/data-factory-editor.png)
3. 在 hello 編輯器中，按一下 **新建資料存放區**hello 工具列，然後選取按鈕**Azure 儲存體**從 hello 下拉式選單。 您應該會看到 hello hello 右窗格中建立 Azure 儲存體連結服務的 JSON 範本。 
   
    ![編輯器 [新增資料存放區] 按鈕](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-editor-newdatastore-button.png)    
3. 取代`<accountname>`和`<accountkey>`與 hello 帳戶名稱和帳戶金鑰值為您的 Azure 儲存體帳戶。 
   
    ![編輯器 Blob 儲存體 JSON](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-editor-blob-storage-json.png)    
4. 按一下**部署**hello 工具列上。 您應該會看到部署的 hello **AzureStorageLinkedService**現在在 hello 樹狀目錄檢視。 
   
    ![編輯器 Blob 儲存體部署](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-editor-blob-storage-deploy.png)

    如需在連結的 hello 服務定義中的 JSON 屬性的詳細資訊，請參閱[Azure Blob 儲存體連接器](data-factory-azure-blob-connector.md#linked-service-properties)發行項。

### <a name="create-a-linked-service-for-hello-azure-sql-database"></a>建立連結的服務的 hello Azure SQL Database
在此步驟中，您可以連結您的 Azure SQL database tooyour data factory。 您可以在此區段中指定 hello Azure SQL server 名稱、 資料庫名稱、 使用者名稱和使用者密碼。 

1. 在 hello **Data Factory 編輯器**，按一下 **新建資料存放區**hello 工具列，然後選取按鈕**Azure SQL Database**從 hello 下拉式選單。 您應該會看到 hello JSON 範本，用於建立 hello 右窗格中的 hello Azure SQL 連結服務。
2. 以您的 Azure SQL Server 名稱、資料庫名稱、使用者帳戶名稱和密碼取代 `<servername>`、`<databasename>`、`<username>@<servername>` 和 `<password>`。 
3. 按一下**部署**hello 工具列 toocreate 且部署 hello **AzureSqlLinkedService**。
4. 確認您看到**AzureSqlLinkedService** hello 下的樹狀結構檢視中**連結的服務**。  

    如需這些 JSON 屬性的詳細資訊，請參閱 [Azure SQL Database 連接器](data-factory-azure-sql-connector.md#linked-service-properties)。

## <a name="create-datasets"></a>建立資料集
在 hello 先前步驟中，您會建立連結的服務 toolink，您的 Azure 儲存體帳戶和 Azure SQL database tooyour 資料 factory。 在此步驟中，您可以定義名為 InputDataset OutputDataset 代表輸入和輸出資料儲存在 hello 分別 AzureStorageLinkedService 和 AzureSqlLinkedService 所參考的資料存放區中的兩個資料集。

hello Azure 儲存體連結服務指定 Data Factory 服務會使用在執行的階段 tooconnect tooyour Azure 儲存體帳戶的 hello 連接字串。 此外，hello 輸入的 blob 資料集 (InputDataset) 指定 hello 容器和包含 hello 輸入的資料的 hello 資料夾。  

同樣地，hello 連結的 Azure SQL Database 服務指定 hello Data Factory 服務會使用在執行的階段 tooconnect tooyour Azure SQL database 的連接字串。 此外，hello 輸出 SQL 資料表資料集 (OututDataset) 會指定 hello 資料表中 hello 資料庫 toowhich hello hello blob 儲存體的資料複製。 

### <a name="create-input-dataset"></a>建立輸入資料集
在此步驟中，您建立資料集名為指向 tooa blob 檔案 (emp.txt) InputDataset hello 的 blob 容器 (adftutorial) 的根資料夾中 hello hello AzureStorageLinkedService 連結服務所代表的 Azure 儲存體中。 如果您不指定 hello 檔名的值 （或略過它），從 hello 輸入資料夾中的所有 blob 資料，則複製的 toohello 目的地。 在本教學課程中，您可以指定 hello 檔案名稱的值。 

1. 在 hello**編輯器**hello Data Factory 中，按一下  **...多個**，按一下**新的資料集**，然後按一下**Azure Blob 儲存體**從 hello 下拉式選單。 
   
    ![新增資料集功能表](./media/data-factory-copy-activity-tutorial-using-azure-portal/new-dataset-menu.png)
2. 以 hello 下列 JSON 片段取代 hello 右窗格中的 JSON: 
   
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
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
          "folderPath": "adftutorial/",
          "fileName": "emp.txt",
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
3. 按一下**部署**hello 工具列 toocreate 且部署 hello **InputDataset**資料集。 確認您看到 hello **InputDataset** hello 樹狀檢視中。

### <a name="create-output-dataset"></a>建立輸出資料集
hello 連結的 Azure SQL Database 服務指定 hello Data Factory 服務會使用在執行的階段 tooconnect tooyour Azure SQL database 的連接字串。 hello 輸出 SQL 資料表的資料集 (OututDataset) 您在此步驟中建立指定複製 hello hello 資料庫 toowhich hello 資料從 hello blob 儲存體中的資料表。

1. 在 hello**編輯器**hello Data Factory 中，按一下  **...多個**，按一下**新的資料集**，然後按一下**Azure SQL**從 hello 下拉式選單。 
2. 以 hello 下列 JSON 片段取代 hello 右窗格中的 JSON:

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
        "linkedServiceName": "AzureSqlLinkedService",
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
3. 按一下**部署**hello 工具列 toocreate 且部署 hello **OutputDataset**資料集。 確認您看到 hello **OutputDataset** hello 下的樹狀結構檢視中**資料集**。 

## <a name="create-pipeline"></a>建立管線
在此步驟中您會建立管線，其中含有使用 **InputDataset** 作為輸入和使用 **OutputDataset** 作為輸出的**複製活動**。

目前，輸出資料集是哪些磁碟機 hello 排程。 在本教學課程中，輸出資料集是設定的 tooproduce 配量小時一次。 hello 管線有開始時間和結束時間的一天分散，也就是 24 小時。 因此，hello 管線所產生的輸出資料集的 24 配量。 

1. 在 hello**編輯器**hello Data Factory 中，按一下  **...更多** 和 新增管線。 或者，您可以以滑鼠右鍵按一下**管線**hello 樹狀檢視中按一下**新管線**。
2. 以 hello 下列 JSON 片段取代 hello 右窗格中的 JSON: 

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
              "retry": 0,
              "timeout": "01:00:00"
            }
          }
        ],
        "start": "2017-05-11T00:00:00Z",
        "end": "2017-05-12T00:00:00Z"
      }
    } 
    ```   
    
    請注意下列點 hello:
   
    - 在 [hello 活動] 區段中，沒有一個活動其**類型**設定得**複製**。 如需 hello 複製活動的詳細資訊，請參閱[資料移動活動](data-factory-data-movement-activities.md)。 在 Data Factory 解決方案中，您也可以使用[資料轉換活動](data-factory-data-transformation-activities.md)。
    - 輸入 hello 活動設定太**InputDataset**和輸出 hello 活動設定太**OutputDataset**。 
    - 在 [hello **typeProperties** ] 區段中， **BlobSource**指定 hello 來源類型為和**SqlSink**指定為 hello 接收器類型。 支援的 hello 複製活動做為來源與接收的資料存放區的完整清單，請參閱[支援資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)。 toolearn toouse 特定支援的資料如何儲存為來源/接收器，按一下 hello 資料表中的 hello 連結。
    - 開始和結束日期時間都必須是 [ISO 格式](http://en.wikipedia.org/wiki/ISO_8601)。 例如：2016-10-14T16:32:41Z。 hello**結束**時間是選擇性的但我們在本教學課程中使用它。 如果您未指定值為 hello**結束**屬性，它會計算為"**start + 48 小時**"。 無限期地指定 toorun hello 管線**9999-09-09**為 hello hello 值**結束**屬性。
     
    在上述範例中的 hello，有 24 資料配量每小時產生每個資料分割。

    如需管線定義中 JSON 屬性的說明，請參閱[建立管線](data-factory-create-pipelines.md)一文。 如需複製活動定義中 JSON 屬性的說明，請參閱[資料移動活動](data-factory-data-movement-activities.md)。 如需 BlobSource 所支援 JSON 屬性的說明，請參閱 [Azure Blob 連接器](data-factory-azure-blob-connector.md)一文。 如需 SqlSink 支援的 JSON 屬性說明，請參閱 [Azure SQL Database 連接器](data-factory-azure-sql-connector.md)一文。
3. 按一下**部署**hello 工具列 toocreate 且部署 hello **ADFTutorialPipeline**。 確認您看到 hello 樹狀檢視中的 hello 管線。 
4. 現在，關閉 hello**編輯器**刀鋒視窗中的按一下**X**。按一下**X**再次 toosee hello **Data Factory** hello 首頁**ADFTutorialDataFactory**。

**恭喜！** 您已成功建立管線 toocopy 資料從 Azure blob 儲存體 tooan Azure SQL database 的 Azure data factory。 


## <a name="monitor-pipeline"></a>監視管線
在此步驟中，您可以使用 hello Azure 入口網站的 toomonitor Azure data factory 中運作。    

### <a name="monitor-pipeline-using-monitor--manage-app"></a>使用監視及管理應用程式來監視管線
hello 下列步驟說明在您的 data factory toomonitor 管線 hello 監視和管理應用程式的使用方式： 

1. 按一下**監視和管理**在您的 data factory 的 hello 首頁上並排顯示。
   
    ![監視及管理圖格](./media/data-factory-copy-activity-tutorial-using-azure-portal/monitor-manage-tile.png) 
2. 您應該會在個別的索引標籤中看到 [監視及管理應用程式]。 

    > [!NOTE]
    > 如果您看到該 hello 網頁瀏覽器卡在 [授權]，執行 hello 下列其中一種： 清除 hello**封鎖第三方 cookie 和站台資料**核取方塊 （或） 建立的例外狀況**login.microsoftonline.com**，然後再試一次 tooopen hello 應用程式。

    ![監視及管理應用程式](./media/data-factory-copy-activity-tutorial-using-azure-portal/monitor-and-manage-app.png)
3. 變更 hello**開始時間**和**結束時間**tooinclude 開始 (2017年-05-11)，並結束時間 (2017年-05-12) 您的管線，然後按一下**套用**。     
3. 您會看到 hello**活動 windows**聯管線開始和結束之間的每小時 hello 中間窗格中的 hello 清單中的時間。 
4. toosee 詳細活動視窗選取 hello hello 中的活動視窗**活動 Windows**清單。 
    ![活動時段詳細資料](./media/data-factory-copy-activity-tutorial-using-azure-portal/activity-window-details.png)

    在活動 Windows 檔案總管 右邊的 hello 上，您會看到該 hello 配量執行 toohello 目前 UTC 時間 （下午 8:12） 會處理 （以綠色）。 hello 8-9 PM，9-10 PM、 10 11 PM，晚上 11 點-12 AM 配量不會尚未處理。

    hello**嘗試**hello 右窗格會提供執行 hello 資料配量的 hello 活動的相關資訊 > 一節。 如果發生錯誤，它會提供 hello 錯誤的詳細資訊。 例如，如果 hello 輸入資料夾或容器不存在，hello 配量處理失敗，您會看到錯誤訊息，說明該 hello 容器或資料夾不存在。

    ![活動執行嘗試](./media/data-factory-copy-activity-tutorial-using-azure-portal/activity-run-attempts.png) 
4. 啟動**SQL Server Management Studio**、 連接 toohello Azure SQL Database，並確認 hello 資料列會插入在 toohello **emp** hello 資料庫資料表中的。
    
    ![SQL 查詢結果](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-sql-query-results.png)

如需使用此應用程式的詳細資訊，請參閱 [使用監視及管理應用程式來監視和管理 Azure Data Factory 管線](data-factory-monitor-manage-app.md)。

### <a name="monitor-pipeline-using-diagram-view"></a>使用圖表檢視監視管線
您也可以使用 hello 圖表檢視監視資料管線。  

1. 在 hello **Data Factory**刀鋒視窗中，按一下 **圖表**。
   
    ![Data Factory 刀鋒視窗：圖表磚](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-datafactoryblade-diagramtile.png)
2. 您應該會看到 hello 圖表類似 toohello 下列映像： 
   
    ![圖表檢視](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-diagram-blade.png)  
5. 在 [hello] 圖表檢視中，按兩下**InputDataset** toosee hello 資料集配量。  
   
    ![已選取 InputDataset 的資料集](./media/data-factory-copy-activity-tutorial-using-azure-portal/DataSetsWithInputDatasetFromBlobSelected.png)   
5. 按一下**看到更多**連結 toosee 所有 hello 資料配量。 您會看到管線開始和結束時間之間的 24 個每小時配量。 
   
    ![所有輸入資料配量](./media/data-factory-copy-activity-tutorial-using-azure-portal/all-input-slices.png)  
   
    請注意，所有 hello toohello 目前 UTC 時間的資料配量是**準備**因為 hello **emp.txt**檔案存在 hello world hello blob 容器中： **adftutorial\input**. hello 配量的 hello 未來時間還未處於就緒狀態。 確認任何扇區顯示在 hello**最近失敗配量**hello 底部的區段。
6. Hello 檢視 （或） 捲動左的 toosee hello 圖表檢視，請參閱 < 直到您關閉 hello 刀鋒視窗。 然後，按兩下 **OutputDataset**。 
8. 按一下**看到更多**hello 上的連結**資料表**刀鋒伺服器**OutputDataset** toosee 所有 hello 配量。

    ![資料配量刀鋒視窗](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-dataslices-blade.png) 
9. 請注意，所有 hello toohello 目前 UTC 時間配量將從移**暫止執行**狀態 = >**正在** ==> **準備**狀態。 hello 從 hello 過去的配量 （在目前的時間） 之前從最新 toooldest 預設來處理。 例如，如果 hello 目前時間是下午 8:12 UTC，hello 處理配量的 7-8 下午前面 hello 6-7 下午配量。 根據預設，之後 9 PM 結尾 hello hello 時間間隔處理 hello 8-9 下午配量。  
10. 按一下 從 hello 清單的任何資料分割，您應該會看見 hello**資料配量**刀鋒視窗。 與活動時段相關聯的資料稱為配量。 配量可以是一或多個檔案。  
    
     ![資料配量刀鋒視窗](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-dataslice-blade.png)
    
     如果 hello 配量不在 hello**準備**狀態，您可以看到未就緒，並封鎖 hello hello 中執行的目前配量的 hello 上游配量**未就緒的上游配量**清單。
11. 在 hello**資料配量**刀鋒視窗中，您應該會看到所有的活動執行 hello hello 底部的清單中。 按一下**活動執行**toosee hello**活動執行詳細資料**刀鋒視窗。 
    
    ![活動執行詳細資料](./media/data-factory-copy-activity-tutorial-using-azure-portal/ActivityRunDetails.png)

    在這個刀鋒視窗中，您會看到如何花了很長的 hello 複製作業，執行哪些輸送量時，多少個位元組的資料已讀取和寫入，請執行開始時間、 結束時間等。  
12. 按一下**X** tooclose 所有 hello 刀鋒視窗，直到您都回到 toohello 家用刀鋒視窗中的 hello **ADFTutorialDataFactory**。
13. （選擇性） 按一下 hello**資料集**磚或**管線**磚 tooget hello 刀鋒視窗，您已經瞭解 hello 前面的步驟。 
14. 啟動**SQL Server Management Studio**、 連接 toohello Azure SQL Database，並確認 hello 資料列會插入在 toohello **emp** hello 資料庫資料表中的。
    
    ![SQL 查詢結果](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-sql-query-results.png)


## <a name="summary"></a>摘要
在本教學課程中，您可以建立 Azure data factory toocopy 資料從 Azure blob tooan Azure SQL database。 您已經使用 hello Azure 入口網站 toocreate hello 資料處理站、 連結的服務、 資料集和管線。 以下是您執行本教學課程中的 hello 高階步驟：  

1. 建立 Azure **Data Factory**。
2. 建立 **連結服務**：
   1. **Azure 儲存體**連結服務 toolink 您保留輸入的資料的 Azure 儲存體帳戶。     
   2. **Azure SQL**連結服務 toolink hello 輸出資料會保存您 Azure SQL database。 
3. 建立可描述管線輸入資料和輸出資料的 **資料集** 。
4. 建立具有**複製活動**的**管線**，以 **BlobSource** 做為來源並以 **SqlSink** 做為接收器。  

## <a name="next-steps"></a>後續步驟
在本教學課程中，您可使用 Azure Blob 儲存體作為來源資料存放區以及使用 Azure SQL Database 作為複製作業的目的地資料存放區。 hello 下表提供 hello 複製活動支援做為來源和目的地資料存放區的清單： 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

關於如何 toocopy 資料，從資料存放區，toolearn 按一下 hello 連結 hello hello 資料表中的資料存放區。
