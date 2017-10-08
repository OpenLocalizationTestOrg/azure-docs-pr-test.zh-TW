---
title: "教學課程： 使用 Azure PowerShell 來建立管線 toomove 資料 |Microsoft 文件"
description: "在本教學課程中，您會使用 Azure PowerShell，建立具有複製活動的 Azure Data Factory 管線。"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 71087349-9365-4e95-9847-170658216ed8
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 21406d7dfaa0c555b2538fbb52839d761c140fc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-data-factory-pipeline-that-moves-data-by-using-azure-powershell"></a>教學課程︰使用 Azure PowerShell 建立 Data Factory 管線來移動資料
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

在本文中，您將學習如何 toouse PowerShell toocreate data factory 管線，將資料從 Azure blob 儲存體 tooan Azure SQL database 複製。 如果您是新 tooAzure Data Factory，閱讀 hello[簡介 tooAzure Data Factory](data-factory-introduction.md)發行項，然後再執行本教學課程。   

在本教學課程中，您可以建立包含一個活動的管線：複製活動。 hello 複製活動會將資料從支援的資料存放區 tooa 支援的接收資料存放區。 如需作為來源和接收區支援的資料存放區清單，請參閱[支援的資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)。 hello 活動被提供安全、 可靠且可擴充的方式的各種資料存放區之間的資料可以複製的全域可用服務。 如需 hello 複製活動的詳細資訊，請參閱[資料移動活動](data-factory-data-movement-activities.md)。

一個管線中可以有多個活動。 此外，您可以藉由設定 hello 輸出資料集的一個活動 hello 的輸入資料集的 hello 其他活動鏈結 （執行一個活動執行另一個之後） 的兩個活動。 如需詳細資訊，請參閱[管線中的多個活動](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline)。

> [!NOTE]
> 本文並未涵蓋所有 hello Data Factory cmdlet。 如需這些 Cmdlet 的完整文件，請參閱 [Data Factory Cmdlet 參考](/powershell/module/azurerm.datafactories)。
> 
> 在此教學課程中的 hello 資料管線會將資料從來源資料存放區 tooa 目的地資料存放區。 如需如何使用 Azure Data Factory，tootransform 資料，請參閱[教學課程： 建立使用 Hadoop 叢集管線 tootransform 資料](data-factory-build-your-first-pipeline.md)。

## <a name="prerequisites"></a>必要條件
- 完成 hello 中所列必要條件[教學課程必要條件](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)發行項。
- 安裝 **Azure PowerShell**。 請依照下列中的 hello 指示[如何 tooinstall 和設定 Azure PowerShell](../powershell-install-configure.md)。

## <a name="steps"></a>步驟
以下是您執行本教學課程的一部分的 hello 步驟：

1. 建立 Azure **Data Factory**。 在此步驟中，您會建立名為 ADFTutorialDataFactoryPSH 的資料處理站。 
2. 建立**連結的服務**hello data factory 中。 在此步驟中，您會建立兩種連結服務：Azure 儲存體和 Azure SQL Database。 
    
    hello AzureStorageLinkedService 連結您的 Azure 儲存體帳戶 toohello data factory。 您在建立容器，並在上傳資料 toothis 儲存體帳戶的[必要條件](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。   

    AzureSqlLinkedService 連結您的 Azure SQL database toohello data factory。 複製 hello blob 儲存體中的 hello 資料會儲存在資料庫中。 您在此資料庫中建立了 SQL 資料表，作為[必要條件](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)的一部分。   
3. 建立輸入和輸出**資料集**hello data factory 中。  
    
    hello Azure 儲存體連結服務指定 Data Factory 服務會使用在執行的階段 tooconnect tooyour Azure 儲存體帳戶的 hello 連接字串。 此外，hello 輸入的 blob 資料集會指定 hello 容器和包含 hello 輸入的資料的 hello 資料夾。  

    同樣地，hello 連結的 Azure SQL Database 服務指定 hello Data Factory 服務會使用在執行的階段 tooconnect tooyour Azure SQL database 的連接字串。 此外，hello 輸出 SQL 資料表的資料集指定複製 hello hello 資料庫 toowhich hello 資料從 hello blob 儲存體中的資料表。
4. 建立**管線**hello data factory 中。 在此步驟中，您會建立具有複製活動的管線。   
    
    hello 複製活動會將資料從 hello Azure SQL database 中 hello Azure blob 儲存體 tooa 資料表中的 blob。 您可以從任何支援的來源支援 tooany 目的地管線 toocopy 資料中使用複製活動。 如需支援的資料存放區清單，請參閱[資料移動活動](data-factory-data-movement-activities.md#supported-data-stores-and-formats)一文。 
5. 監視 hello 管線。 在此步驟中，您**監視器**hello 使用 PowerShell 之輸入和輸出資料集配量。

## <a name="create-a-data-factory"></a>建立 Data Factory
> [!IMPORTANT]
> 完成[hello 教學課程的必要條件](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)如果您還沒有。   

資料處理站可以有一或多個管線。 其中的管線可以有一或多個活動。 例如，複製活動 toocopy 資料從來源 tooa 目的地資料存放區和 HDInsight Hive 活動 toorun Hive 指令碼 tootransform 輸入資料 tooproduct 輸出資料。 讓我們開始在此步驟中建立 hello 資料 factory。

1. 啟動 **PowerShell**。 保持開啟 Azure PowerShell 直到本教學課程中的 hello 結尾。 如果您關閉並重新開啟，您需要 toorun hello 命令一次。

    執行下列命令，hello，然後輸入 hello 使用者名稱和密碼，您會使用 toosign toohello Azure 入口網站中：

    ```PowerShell
    Login-AzureRmAccount
    ```   
   
    此帳戶的所有 hello 訂用帳戶都執行下列命令 tooview hello:

    ```PowerShell
    Get-AzureRmSubscription
    ```

    執行下列命令 tooselect hello 訂用帳戶，您想要使用 toowork hello。 取代 **&lt;NameOfAzureSubscription** &gt; hello Azure 訂用帳戶名稱：

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```
2. 建立 Azure 資源群組名稱為**ADFTutorialResourceGroup**藉由執行下列命令的 hello:

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
    
    本教學課程中的 hello 步驟假設您使用名為 「 hello 資源群組**ADFTutorialResourceGroup**。 如果您使用不同的資源群組，您需要 toouse 它來取代 ADFTutorialResourceGroup 在本教學課程。
3. 執行 hello**新增 AzureRmDataFactory** cmdlet toocreate 名為 data factory **ADFTutorialDataFactoryPSH**:  

    ```PowerShell
    $df=New-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name ADFTutorialDataFactoryPSH –Location "West US"
    ```
    此名稱可能已被使用。 因此，請 hello hello data factory 名稱唯一藉由新增前置或後置 (例如： ADFTutorialDataFactoryPSH05152017) 並執行一次 hello 命令。  

請注意下列點 hello:

* hello hello Azure data factory 的名稱必須是全域唯一的。 如果您收到下列錯誤 hello，變更 hello 名稱 (例如，yournameADFTutorialDataFactoryPSH)。 執行本教學課程中的步驟時，請使用此名稱來取代 ADFTutorialFactoryPSH。 請參閱 [Data Factory - 命名規則](data-factory-naming-rules.md)，以了解 Data Factory 成品的命名規則。

    ```
    Data factory name “ADFTutorialDataFactoryPSH” is not available
    ```
* toocreate Data Factory 執行個體，您必須是參與者或 hello Azure 訂用帳戶的系統管理員。
* 可能會註冊為 hello 未來中的 DNS 名稱，因此會變成可見 hello hello data factory 名稱。
* 您可能會收到 hello 下列錯誤:"**此訂用帳戶不是已註冊的 toouse 命名空間 Microsoft.DataFactory。**" Hello 下列其中一種作業，並再試一次發行：

  * 在 Azure PowerShell 中執行下列命令 tooregister hello Data Factory 提供者的 hello:

    ```PowerShell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

    執行下列命令 tooconfirm hello Data Factory 提供者註冊該 hello:

    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * 登入使用 hello Azure 訂用帳戶 toohello [Azure 入口網站](https://portal.azure.com)。 移 tooa Data Factory 刀鋒視窗中，或在 hello Azure 入口網站中建立 data factory。 這個動作會自動註冊 hello 您的提供者。

## <a name="create-linked-services"></a>建立連結的服務
您可以建立連結的服務中的資料處理站 toolink 資料儲存和運算服務 toohello 資料 factory。 在本教學課程中，您不會使用任何計算服務，例如 Azure HDInsight 或 Azure Data Lake Analytics。 您可以使用兩種類型的資料存放區：Azure 儲存體 (來源) 和 Azure SQL Database (目的地)。 

因此，您可以建立名為 AzureStorageLinkedService 和 AzureSqlLinkedService 的兩個連結服務︰類型為 AzureStorage 和 AzureSqlDatabase。  

hello AzureStorageLinkedService 連結您的 Azure 儲存體帳戶 toohello data factory。 這個儲存體帳戶為其中一個 hello 在其中建立容器及 hello 資料上傳的過程[必要條件](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。   

AzureSqlLinkedService 連結您的 Azure SQL database toohello data factory。 複製 hello blob 儲存體中的 hello 資料會儲存在資料庫中。 在此資料庫中建立 hello emp 資料表的一部分[必要條件](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。 

### <a name="create-a-linked-service-for-an-azure-storage-account"></a>建立 Azure 儲存體帳戶的連結服務
在此步驟中，您必須連結您的 Azure 儲存體帳戶 tooyour data factory。

1. 建立名為的 JSON 檔案**AzureStorageLinkedService.json**中**C:\ADFGetStartedPSH**資料夾以 hello 下列內容: （建立 hello 資料夾 ADFGetStartedPSH 如果不存在。）

    > [!IMPORTANT]
    > 取代&lt;accountname&gt;和&lt;accountkey&gt;名稱與您的 Azure 儲存體帳戶金鑰儲存 hello 檔案之前。 

    ```json
    {
        "name": "AzureStorageLinkedService",
        "properties": {
            "type": "AzureStorage",
            "typeProperties": {
                "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
            }
        }
     }
    ``` 
2. 在**Azure PowerShell**，切換 toohello **ADFGetStartedPSH**資料夾。
4. 執行 hello**新增 AzureRmDataFactoryLinkedService** cmdlet toocreate hello 連結服務： **AzureStorageLinkedService**。 這個指令程式和您在本教學課程中使用其他 Data Factory cmdlet 需要您 toopass 值 hello **ResourceGroupName**和**DataFactoryName**參數。 或者，您可以傳遞 hello DataFactory 物件 hello 新增 AzureRmDataFactory cmdlet 所傳回，而不需要輸入資源群組名稱和 DataFactoryName 每次您執行 cmdlet。 

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\AzureStorageLinkedService.json
    ```
    以下是 hello 範例輸出：

    ```
    LinkedServiceName : AzureStorageLinkedService
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.LinkedServiceProperties
    ProvisioningState : Succeeded
    ``` 

    建立這項連結的服務的其他方式是 toospecify 資源群組名稱，而不是指定 hello DataFactory 物件的 data factory 名稱。  

    ```PowerShell
    New-AzureRmDataFactoryLinkedService -ResourceGroupName ADFTutorialResourceGroup -DataFactoryName <Name of your data factory> -File .\AzureStorageLinkedService.json
    ```

### <a name="create-a-linked-service-for-an-azure-sql-database"></a>建立 Azure SQL Database 的連結服務
在此步驟中，您可以連結您的 Azure SQL database tooyour data factory。

1. 建立名為 hello 遵循 AzureSqlLinkedService.json C:\ADFGetStartedPSH 資料夾中的 JSON 檔案內容：

    > [!IMPORTANT]
    > 將 &lt;servername&gt;、&lt;databasename&gt;、&lt;username@servername&gt; 和 &lt;password&gt; 替換為您的 Azure SQL 伺服器名稱、資料庫名稱、使用者帳戶和密碼。
    
    ```json
    {
        "name": "AzureSqlLinkedService",
        "properties": {
            "type": "AzureSqlDatabase",
            "typeProperties": {
                "connectionString": "Server=tcp:<server>.database.windows.net,1433;Database=<databasename>;User ID=<user>@<server>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
            }
        }
     }
    ```
2. 執行下列命令 toocreate hello 連結的服務：

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\AzureSqlLinkedService.json
    ```
    
    以下是 hello 範例輸出：

    ```
    LinkedServiceName : AzureSqlLinkedService
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.LinkedServiceProperties
    ProvisioningState : Succeeded
    ```

   確認**tooAzure 服務允許存取**設定已開啟您的 SQL 資料庫伺服器。 tooverify 並將它開啟，執行下列步驟 hello:

    1. 登入 toohello [Azure 入口網站](https://portal.azure.com)
    2. 按一下**更多服務 >** hello 左邊，然後按一下  **SQL 伺服器**在 hello**資料庫**類別目錄。
    3. SQL 伺服器 hello 清單中選取您的伺服器。
    4. 在 hello SQL 伺服器刀鋒視窗中，按一下 **顯示防火牆設定**連結。
    5. 在 hello**防火牆設定**刀鋒視窗中，按一下**ON**如**tooAzure 服務允許存取**。
    6. 按一下**儲存**hello 工具列上。 

## <a name="create-datasets"></a>建立資料集
在 hello 先前步驟中，您會建立連結的服務 toolink，您的 Azure 儲存體帳戶和 Azure SQL database tooyour 資料 factory。 在此步驟中，您可以定義名為 InputDataset OutputDataset 代表輸入和輸出資料儲存在 hello 分別 AzureStorageLinkedService 和 AzureSqlLinkedService 所參考的資料存放區中的兩個資料集。

hello Azure 儲存體連結服務指定 Data Factory 服務會使用在執行的階段 tooconnect tooyour Azure 儲存體帳戶的 hello 連接字串。 此外，hello 輸入的 blob 資料集 (InputDataset) 指定 hello 容器和包含 hello 輸入的資料的 hello 資料夾。  

同樣地，hello 連結的 Azure SQL Database 服務指定 hello Data Factory 服務會使用在執行的階段 tooconnect tooyour Azure SQL database 的連接字串。 此外，hello 輸出 SQL 資料表資料集 (OututDataset) 會指定 hello 資料表中 hello 資料庫 toowhich hello hello blob 儲存體的資料複製。 

### <a name="create-an-input-dataset"></a>建立輸入資料集
在此步驟中，您建立資料集名為指向 tooa blob 檔案 (emp.txt) InputDataset hello 的 blob 容器 (adftutorial) 的根資料夾中 hello hello AzureStorageLinkedService 連結服務所代表的 Azure 儲存體中。 如果您不指定 hello 檔名的值 （或略過它），從 hello 輸入資料夾中的所有 blob 資料，則複製的 toohello 目的地。 在本教學課程中，您可以指定 hello 檔案名稱的值。  

1. 建立名為的 JSON 檔案**InputDataset.json**在 hello **C:\ADFGetStartedPSH**資料夾中，以下列內容的 hello:

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
                "fileName": "emp.txt",
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
2. 執行下列命令 toocreate hello Data Factory 的資料集的 hello。

    ```PowerShell  
    New-AzureRmDataFactoryDataset $df -File .\InputDataset.json
    ```
    以下是 hello 範例輸出：

    ```
    DatasetName       : InputDataset
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Availability      : Microsoft.Azure.Management.DataFactories.Common.Models.Availability
    Location          : Microsoft.Azure.Management.DataFactories.Models.AzureBlobDataset
    Policy            : Microsoft.Azure.Management.DataFactories.Common.Models.Policy
    Structure         : {FirstName, LastName}
    Properties        : Microsoft.Azure.Management.DataFactories.Models.DatasetProperties
    ProvisioningState : Succeeded
    ```

### <a name="create-an-output-dataset"></a>建立輸出資料表
在這個部分 hello 步驟中，您會建立名為輸出資料集**OutputDataset**。 此資料集所代表的 hello Azure SQL database 中的點 tooa SQL 資料表**AzureSqlLinkedService**。 

1. 建立名為的 JSON 檔案**OutputDataset.json**在 hello **C:\ADFGetStartedPSH**資料夾以 hello 下列內容：

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
2. 執行下列命令 toocreate hello 資料 factory 資料集的 hello。

    ```PowerShell   
    New-AzureRmDataFactoryDataset $df -File .\OutputDataset.json
    ```

    以下是 hello 範例輸出：

    ```
    DatasetName       : OutputDataset
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Availability      : Microsoft.Azure.Management.DataFactories.Common.Models.Availability
    Location          : Microsoft.Azure.Management.DataFactories.Models.AzureSqlTableDataset
    Policy            :
    Structure         : {FirstName, LastName}
    Properties        : Microsoft.Azure.Management.DataFactories.Models.DatasetProperties
    ProvisioningState : Succeeded
    ```

## <a name="create-a-pipeline"></a>建立管線
在此步驟中您會建立管線，其中含有使用 **InputDataset** 作為輸入和使用 **OutputDataset** 作為輸出的**複製活動**。

目前，輸出資料集是哪些磁碟機 hello 排程。 在本教學課程中，輸出資料集是設定的 tooproduce 配量小時一次。 hello 管線有開始時間和結束時間的一天分散，也就是 24 小時。 因此，hello 管線所產生的輸出資料集的 24 配量。 


1. 建立名為的 JSON 檔案**ADFTutorialPipeline.json**在 hello **C:\ADFGetStartedPSH**資料夾中，以下列內容的 hello:

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
     
    取代 hello hello 值**啟動**屬性以 hello 目前的日期和**結束**以 hello 隔天的值。 您可以指定 hello 日期部分，並略過 hello hello 時間部分日期時間。 例如，"2016年-02-03"，這相當於太"2016年-02-03T00:00:00Z"
     
    開始和結束日期時間都必須是 [ISO 格式](http://en.wikipedia.org/wiki/ISO_8601)。 例如：2016-10-14T16:32:41Z。 hello**結束**時間是選擇性的但我們在本教學課程中使用它。 
     
    如果您未指定值為 hello**結束**屬性，它會計算為"**start + 48 小時**"。 無限期地指定 toorun hello 管線**9999-09-09**為 hello hello 值**結束**屬性。
     
    在上述範例中的 hello，有 24 資料配量每小時產生每個資料分割。

    如需管線定義中 JSON 屬性的說明，請參閱[建立管線](data-factory-create-pipelines.md)一文。 如需複製活動定義中 JSON 屬性的說明，請參閱[資料移動活動](data-factory-data-movement-activities.md)。 如需 BlobSource 所支援 JSON 屬性的說明，請參閱 [Azure Blob 連接器](data-factory-azure-blob-connector.md)一文。 如需 SqlSink 支援的 JSON 屬性說明，請參閱 [Azure SQL Database 連接器](data-factory-azure-sql-connector.md)一文。
2. 執行下列命令 toocreate hello 資料 factory 資料表的 hello。

    ```PowerShell   
    New-AzureRmDataFactoryPipeline $df -File .\ADFTutorialPipeline.json
    ```

    以下是 hello 範例輸出： 

    ```
    PipelineName      : ADFTutorialPipeline
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.PipelinePropertie
    ProvisioningState : Succeeded
    ```

**恭喜！** 您已成功建立管線 toocopy 資料從 Azure blob 儲存體 tooan Azure SQL database 的 Azure data factory。 

## <a name="monitor-hello-pipeline"></a>監視 hello 管線
在此步驟中，您使用 Azure PowerShell toomonitor Azure data factory 中運作。

1. 取代&lt;DataFactoryName&gt; hello 名稱為您的 data factory 和執行**Get AzureRmDataFactory**，並指派 hello 輸出 tooa 變數 $df。

    ```PowerShell  
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name <DataFactoryName>
    ```

    例如：
    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name ADFTutorialDataFactoryPSH0516
    ```
    
    然後，執行列印 hello 內容 $df toosee hello 下列輸出： 
    
    ```
    PS C:\ADFGetStartedPSH> $df
    
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DataFactoryId     : 6f194b34-03b3-49ab-8f03-9f8a7b9d3e30
    ResourceGroupName : ADFTutorialResourceGroup
    Location          : West US
    Tags              : {}
    Properties        : Microsoft.Azure.Management.DataFactories.Models.DataFactoryProperties
    ProvisioningState : Succeeded
    ```
2. 執行**Get AzureRmDataFactorySlice** tooget 詳細所有配量的 hello **OutputDataset**，這是 hello 管線的 hello 輸出資料集。  

    ```PowerShell   
    Get-AzureRmDataFactorySlice $df -DatasetName OutputDataset -StartDateTime 2017-05-11T00:00:00Z
    ```

   這項設定應該符合 hello**啟動**hello 管線 JSON 中的值。 您應該會看到 24 配量，其中每個小時從 12 AM 的 hello 當天 too12 我的 hello 隔天。

   以下是從 hello 輸出三個範例配量： 

    ``` 
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DatasetName       : OutputDataset
    Start             : 5/11/2017 11:00:00 PM
    End               : 5/12/2017 12:00:00 AM
    RetryCount        : 0
    State             : Ready
    SubState          :
    LatencyStatus     :
    LongRetryCount    : 0

    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DatasetName       : OutputDataset
    Start             : 5/11/2017 9:00:00 PM
    End               : 5/11/2017 10:00:00 PM
    RetryCount        : 0
    State             : InProgress
    SubState          :
    LatencyStatus     :
    LongRetryCount    : 0   

    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DatasetName       : OutputDataset
    Start             : 5/11/2017 8:00:00 PM
    End               : 5/11/2017 9:00:00 PM
    RetryCount        : 0
    State             : Waiting
    SubState          : ConcurrencyLimit
    LatencyStatus     :
    LongRetryCount    : 0
    ```
3. 執行**Get AzureRmDataFactoryRun** tooget hello 詳細資料的活動已執行**特定**配量。 複製 hello 前一個命令 toospecify hello 參數的值 hello StartDateTime hello 輸出 hello 日期-時間值。 

    ```PowerShell  
    Get-AzureRmDataFactoryRun $df -DatasetName OutputDataset -StartDateTime "5/11/2017 09:00:00 PM"
    ```

   以下是 hello 範例輸出： 

    ```
    Id                  : c0ddbd75-d0c7-4816-a775-704bbd7c7eab_636301332000000000_636301368000000000_OutputDataset
    ResourceGroupName   : ADFTutorialResourceGroup
    DataFactoryName     : ADFTutorialDataFactoryPSH0516
    DatasetName         : OutputDataset
    ProcessingStartTime : 5/16/2017 8:00:33 PM
    ProcessingEndTime   : 5/16/2017 8:01:36 PM
    PercentComplete     : 100
    DataSliceStart      : 5/11/2017 9:00:00 PM
    DataSliceEnd        : 5/11/2017 10:00:00 PM
    Status              : Succeeded
    Timestamp           : 5/16/2017 8:00:33 PM
    RetryAttempt        : 0
    Properties          : {}
    ErrorMessage        :
    ActivityName        : CopyFromBlobToSQL
    PipelineName        : ADFTutorialPipeline
    Type                : Copy  
    ```

如需 Data Factory Cmdlet 的完整文件，請參閱 [Data Factory Cmdlet 參考](/powershell/module/azurerm.datafactories)。

## <a name="summary"></a>摘要
在本教學課程中，您可以建立 Azure data factory toocopy 資料從 Azure blob tooan Azure SQL database。 您可以使用 PowerShell toocreate hello 資料處理站、 連結的服務、 資料集和管線。 以下是您執行本教學課程中的 hello 高階步驟：  

1. 建立 Azure **Data Factory**。
2. 建立 **連結服務**：

   a. **Azure 儲存體**連結服務 toolink 您保留輸入的資料的 Azure 儲存體帳戶。     
   b. **Azure SQL**連結服務 toolink hello 輸出資料會保存您 SQL database。
3. 建立可描述管線輸入資料和輸出資料的 **資料集** 。
4. 建立**管線**與**複製活動**，與**BlobSource**為 hello 來源和**SqlSink**為 hello 接收。

## <a name="next-steps"></a>後續步驟
在本教學課程中，您可使用 Azure Blob 儲存體作為來源資料存放區以及使用 Azure SQL Database 作為複製作業的目的地資料存放區。 hello 下表提供 hello 複製活動支援做為來源和目的地資料存放區的清單： 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

關於如何 toocopy 資料，從資料存放區，toolearn 按一下 hello 連結 hello hello 資料表中的資料存放區。 

