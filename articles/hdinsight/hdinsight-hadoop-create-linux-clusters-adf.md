---
title: "使用 Data Factory-Azure HDInsight 隨 Hadoop 叢集的 aaaCreate |Microsoft 文件"
description: "了解如何 toocreate 隨 Hadoop 叢集 HDInsight 使用 Azure Data Factory 中。"
services: hdinsight
documentationcenter: 
tags: azure-portal
author: spelluru
manager: jhubbard
editor: cgronlun
ms.assetid: 1f3b3a78-4d16-4d99-ba6e-06f7bb185d6a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/20/2017
ms.author: spelluru
ms.openlocfilehash: c869776ac270e37dec710b5fc8d2a792d9263129
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-on-demand-hadoop-clusters-in-hdinsight-using-azure-data-factory"></a>使用 Azure Data Factory 在 HDInsight 中建立隨選 Handooop 叢集
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

[Azure Data Factory](../data-factory/data-factory-introduction.md)是以雲端為基礎的資料整合服務會協調及自動 hello 移動和轉換資料。 它可建立 HDInsight Hadoop 叢集在 just-in-time tooprocess 輸入的資料配量，及 hello 處理序完成時刪除 hello 叢集。 使用隨 HDInsight Hadoop 叢集的 hello 優點包括：

- 您只有工資 hello 計時器工作執行的 hello HDInsight Hadoop 叢集 （以及簡短的可設定閒置時間）。 HDInsight 叢集的 hello 計費被一下每分鐘，不論您或不使用它們。 當您使用隨 HDInsight 連結服務 Data Factory 中時，視頁面時，會建立 hello 叢集。 和 hello 叢集 hello 工作都完成之後會自動刪除。 因此，您只需支付 hello 作業執行時間和 hello 簡短閒置時間 （存留時間設定）。
- 您可以使用 Data Factory 管線建立工作流程。 例如，您可以從 Azure blob 儲存體，視 HDInsight Hadoop 叢集上執行 Hive 指令碼和 Pig 指令碼處理 hello 資料在內部部署 SQL Server tooan hello 管線 toocopy 資料。 接著，複製 hello 結果資料 tooan BI 應用程式 tooconsume for Azure SQL 資料倉儲。
- 您可以排程 hello 工作流程 toorun 定期 （每小時、 每天、 每週、 每月等）。

在 Azure Data Factory 中，資料處理站可以有一或多個資料管線。 資料管線具有一或多個活動。 兩種活動類型︰[資料移動活動](../data-factory/data-factory-data-movement-activities.md)和[資料轉換活動](../data-factory/data-factory-data-transformation-activities.md)。 您可以使用資料移動的活動 （目前，只複製活動） toomove 資料來源建立資料存放區 tooa 目的地資料存放區。 您使用資料轉換活動 tootransform/處理序資料。 HDInsight Hive 活動是其中一個支援的 Data Factory 的 hello 轉換活動。 您在本教學課程使用 hello Hive 轉換活動。

您可以設定 hive 活動 toouse HDInsight Hadoop 叢集或隨 HDInsight Hadoop 叢集。 在本教學課程，hello hello 資料 factory 管線中的 Hive 活動是已設定的 toouse 隨選 HDInsight 叢集。 因此，當 hello 活動執行 tooprocess 資料配量時，會發生下列情況：

1. HDInsight Hadoop 叢集會自動建立您在 just-in-time tooprocess hello 配量。  
2. hello 輸入的資料會由 hello 叢集上執行下列 HiveQL 指令碼處理。
3. hello 處理完成，且 hello 叢集的時間 （timeToLive 設定） 設定的 hello 內處於閒置狀態之後，會刪除 hello HDInsight Hadoop 叢集。 如果可用於在 timeToLive 閒置時間與處理 hello 下一個資料配量，hello 相同叢集是使用的 tooprocess hello 配量。  

在本教學課程，hello 與 hello hive 活動相關聯的下列 HiveQL 指令碼會執行下列動作的 hello:

1. 建立參考 hello 原始 web 記錄資料儲存在 Azure Blob 儲存體中的外部資料表。
2. 資料分割 hello 依據年和月的未經處理資料。
3. 存放區 hello hello Azure blob 儲存體中的資料分割的資料。

在此教學課程中，hello 與 hello hive 活動相關聯的下列 HiveQL 指令碼會建立參考 hello hello Azure Blob 儲存體中儲存的未經處理的 web 記錄資料的外部資料表。 以下是每個月 hello 範例資料列 hello 輸入檔中。

```
2014-01-01,02:01:09,SAMPLEWEBSITE,GET,/blogposts/mvc4/step2.png,X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,53175,871
2014-02-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
2014-03-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
```

hello 下列 HiveQL 指令碼會分割 hello 依據年和月的未經處理資料。 它會建立三個 hello 先前的輸入為基礎的輸出資料夾。 每個資料夾都包含一個檔案，內含每個月的項目。

```
adfgetstarted/partitioneddata/year=2014/month=1/000000_0
adfgetstarted/partitioneddata/year=2014/month=2/000000_0
adfgetstarted/partitioneddata/year=2014/month=3/000000_0
```

如需新增 tooHive 活動中的 Data Factory 資料轉換活動，請參閱[轉換和分析使用 Azure Data Factory](../data-factory/data-factory-data-transformation-activities.md)。

> [!NOTE]
> 目前，您只可以從 Azure Data Factory 建立 HDInsight 叢集 3.2 版。

## <a name="prerequisites"></a>必要條件
在開始這篇文章中的 hello 指示之前，您必須擁有 hello 下列項目：

* [Azure 訂用帳戶](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。
* Azure PowerShell。

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell.md)]

### <a name="prepare-storage-account"></a>準備儲存體帳戶
您可以使用向上 toothree 儲存體帳戶，在此案例中：

- hello HDInsight 叢集的預設儲存體帳戶
- hello 輸入資料的儲存體帳戶
- hello 輸出資料的儲存體帳戶

toosimplify hello 教學課程中，您可以使用一個儲存體帳戶 tooserve hello 三種用途。 本章節的 hello Azure PowerShell 範例指令碼會執行下列工作的 hello:

1. 登入 tooAzure。
2. 建立 Azure 資源群組。
3. 建立 Azure 儲存體帳戶。
4. Hello 儲存體帳戶中建立 Blob 容器
5. 複製下列兩個檔案 toohello Blob 容器的 hello:

   * 輸入資料檔： [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log)
   * HiveQL 指令碼： [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql)

     這兩個檔案會儲存在公用 Blob 容器。


**tooprepare hello 儲存體和複製 hello 檔案使用 Azure PowerShell:**
> [!IMPORTANT]
> 指定 hello Azure 資源群組和 hello 將 hello 指令碼所建立的 Azure 儲存體帳戶名稱。
> 請記下**資源群組名稱**，**儲存體帳戶名稱**，和**儲存體帳戶金鑰**hello 指令碼輸出。 您會需要它們 hello 下一節。

```powershell
$resourceGroupName = "<Azure Resource Group Name>"
$storageAccountName = "<Azure Storage Account Name>"
$location = "East US 2"

$sourceStorageAccountName = "hditutorialdata"  
$sourceContainerName = "adfhiveactivity"

$destStorageAccountName = $storageAccountName
$destContainerName = "adfgetstarted" # don't change this value.

####################################
# Connect tooAzure
####################################
#region - Connect tooAzure subscription
Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
try{Get-AzureRmContext}
catch{Login-AzureRmAccount}
#endregion

####################################
# Create a resource group, storage, and container
####################################

#region - create Azure resources
Write-Host "`nCreating resource group, storage account and blob container ..." -ForegroundColor Green

New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
New-AzureRmStorageAccount `
    -ResourceGroupName $resourceGroupName `
    -Name $destStorageAccountName `
    -type Standard_LRS `
    -Location $location

$destStorageAccountKey = (Get-AzureRmStorageAccountKey `
    -ResourceGroupName $resourceGroupName `
    -Name $destStorageAccountName)[0].Value

$sourceContext = New-AzureStorageContext `
    -StorageAccountName $sourceStorageAccountName `
    -Anonymous
$destContext = New-AzureStorageContext `
    -StorageAccountName $destStorageAccountName `
    -StorageAccountKey $destStorageAccountKey

New-AzureStorageContainer -Name $destContainerName -Context $destContext
#endregion

####################################
# Copy files
####################################
#region - copy files
Write-Host "`nCopying files ..." -ForegroundColor Green

$blobs = Get-AzureStorageBlob `
    -Context $sourceContext `
    -Container $sourceContainerName

$blobs|Start-AzureStorageBlobCopy `
    -DestContext $destContext `
    -DestContainer $destContainerName

Write-Host "`nCopied files ..." -ForegroundColor Green
Get-AzureStorageBlob -Context $destContext -Container $destContainerName
#endregion

Write-host "`nYou will use hello following values:" -ForegroundColor Green
write-host "`nResource group name: $resourceGroupName"
Write-host "Storage Account Name: $destStorageAccountName"
write-host "Storage Account Key: $destStorageAccountKey"

Write-host "`nScript completed" -ForegroundColor Green
```

如果您需要協助 hello PowerShell 指令碼，請參閱[使用 hello 與 Azure 儲存體的 Azure PowerShell](../storage/common/storage-powershell-guide-full.md)。 如果您希望 toouse Azure CLI 相反地，請參閱 hello[附錄](#appendix)hello Azure CLI 指令碼的區段。

**tooexamine hello 儲存體帳戶和 hello 內容**

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 按一下**資源群組**hello 左窗格上。
3. 按兩下您建立 PowerShell 指令碼中的 hello 資源群組名稱。 如果您有太多的資源群組列出，請使用 hello 篩選條件。
4. 在 hello**資源**磚中，您應該有一項資源列出，除非您與其他專案共用 hello 資源群組。 該資源是您稍早指定的 hello 名稱 hello 儲存體帳戶。 按一下 hello 儲存體帳戶名稱。
5. 按一下 hello **Blob**磚。
6. 按一下 hello **adfgetstarted**容器。 您會看到兩個資料夾︰[輸入資料] 和 [指令碼]。
7. 開啟 [hello] 資料夾，並檢查 hello 資料夾中的 hello 檔案。 hello inputdata 包含輸入資料與 hello input.log 檔案而且 hello 指令碼 資料夾包含 hello HiveQL 指令碼檔案。

## <a name="create-a-data-factory-using-resource-manager-template"></a>使用 Resource Manager 範本建立資料處理站
Hello 儲存體帳戶、 與 hello 輸入的資料，hello 備妥下列 HiveQL 指令碼，您就準備好 toocreate Azure data factory。 有數種方法可建立 Data Factory。 在本教學課程中，您可以建立 data factory 所部署的 Azure Resource Manager 範本使用 hello Azure 入口網站。 您也可以使用 [Azure CLI](../azure-resource-manager/resource-group-template-deploy-cli.md) 和 [Azure PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template) 部署 Resource Manager 範本。 如需其他 Data Factory 建立方法，請參閱 [教學課程︰建立您的第一個 Data Factory](../data-factory/data-factory-build-your-first-pipeline.md)。

1. 按一下下列 tooAzure 中的映像 toosign 和開啟 hello Resource Manager 範本 hello Azure 入口網站中的 hello。 hello 範本位於 https://hditutorialdata.blob.core.windows.net/adfhiveactivity/data-factory-hdinsight-on-demand.json。 請參閱 hello [hello 範本中的 Data Factory 實體](#data-factory-entities-in-the-template)hello 範本中定義實體的詳細資訊的區段。 

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Fadfhiveactivity%2Fdata-factory-hdinsight-on-demand.json" target="_blank"><img src="./media/hdinsight-hadoop-create-linux-clusters-adf/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. 選取**使用現有**選項 hello**資源群組**設定，再選取 hello hello hello （使用 PowerShell 指令碼） 的上一個步驟中所建立的資源群組名稱。
3. 輸入 hello data factory 的名稱 (**Data Factory 名稱**)。 此名稱必須是全域唯一的。
4. 輸入 hello**儲存體帳戶名稱**和**儲存體帳戶金鑰**hello 上一個步驟中記下。
5. 選取**toohello 條款和條件，即表示我同意**閱讀後指定上述**條款和條件**。
6. 選取**Pin toodashboard**選項。
6. 按一下 [購買/建立]。 您在 hello 呼叫儀表板上看到磚**部署範本部署**。 等候直到在 hello**資源群組**資源群組的刀鋒視窗隨即開啟。 您也可以按一下 hello 磚的標題會當做您資源群組名稱 tooopen hello 資源群組 刀鋒視窗。
6. 如果尚未開啟 hello 資源群組 刀鋒視窗，請按一下 hello 磚 tooopen hello 資源群組。 現在您應該會看到一個詳細資料 factory 資源列出此外 toohello 儲存體帳戶的資源。
7. 按一下您的 data factory hello 名稱 (您指定的 hello 值**Data Factory 名稱**參數)。
8. 在 hello Data Factory 刀鋒視窗中，按一下 hello**圖表**磚。 hello 圖表會顯示與輸入資料集和輸出資料集的一個活動：

    ![Azure Data Factory HDInsight 隨選 Hive 活動管線圖](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-pipeline-diagram.png)

    hello 名稱定義在 hello Resource Manager 範本。
9. 按兩下 [AzureBlobOutput] 。
10. 在 hello**最近更新配量**，您應該會看到一個扇區。 如果 hello 狀態是**正在**，等候直到變更太**準備**。 通常，大約需要**20 分鐘**toocreate 的 HDInsight 叢集。

### <a name="check-hello-data-factory-output"></a>檢查 hello 資料處理站的輸出

1. 使用 hello 相同 hello 最後一個工作階段 toocheck hello 容器中的 hello adfgetstarted 容器的程序。 有兩個新的容器此外太**adfgetsarted**:

   * 遵循 hello 模式名稱的容器： `adf<yourdatafactoryname>-linkedservicename-datetimestamp`。 此容器是 hello hello HDInsight 叢集的預設容器。
   * adfjobs： 此容器是 hello hello ADF 作業記錄的容器。

     hello 資料處理站的輸出會儲存在**afgetstarted**您 hello Resource Manager 範本中的設定。
2. 按一下 [adfgetstarted] 。
3. 按兩下 [partitioneddata] 。 您會看到**年 = 2014年**資料夾因為所有的 hello web 記錄日期在 2014 年。

    ![Azure Data Factory HDInsight 隨選 Hive 活動管線輸出](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-output-year.png)

    如果您 hello 清單向下鑽研，您應該會看到一月、 二月和三月的三個資料夾。 而且每個月都有記錄檔。

    ![Azure Data Factory HDInsight 隨選 Hive 活動管線輸出](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-output-month.png)

## <a name="data-factory-entities-in-hello-template"></a>Hello 範本中的 data Factory 實體
以下是如何 data factory hello 最上層資源管理員範本外觀就像：

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": { ...
    },
    "variables": { ...
    },
    "resources": [
        {
            "name": "[parameters('dataFactoryName')]",
            "apiVersion": "[variables('apiVersion')]",
            "type": "Microsoft.DataFactory/datafactories",
            "location": "westus",
            "resources": [
                { ... },
                { ... },
                { ... },
                { ... }
            ]
        }
    ]
}
```

### <a name="define-data-factory"></a>定義資料處理站
Hello 下列範例所示，您可以定義在 hello Resource Manager 範本中的 data factory:  

```json
"resources": [
{
    "name": "[parameters('dataFactoryName')]",
    "apiVersion": "[variables('apiVersion')]",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "westus",
}
```
hello dataFactoryName 是 hello 部署 hello 範本時，您指定的 hello data factory 名稱。 Data factory 是目前只支援 hello 美國東部、 美國西部和北歐區域中。

### <a name="defining-entities-within-hello-data-factory"></a>定義 hello 資料處理站內的實體
hello 下列 Data Factory 實體範本中所定義 hello JSON:

* [Azure 儲存體連結服務](#azure-storage-linked-service)
* [HDInsight 隨選連結服務](#hdinsight-on-demand-linked-service)
* [Azure Blob 輸入資料集](#azure-blob-input-dataset)
* [Azure Blob 輸出資料集](#azure-blob-output-dataset)
* [具有複製活動的管線](#data-pipeline)

#### <a name="azure-storage-linked-service"></a>Azure 儲存體連結服務
hello Azure 儲存體連結服務連結您的 Azure 儲存體帳戶 toohello data factory。 在此教學課程中，hello 相同儲存體帳戶做為 hello 預設 HDInsight 儲存體帳戶、 輸入的資料存放區和輸出資料存放區。 因此，您只定義一個 Azure 儲存體連結服務。 在連結的 hello 服務定義中，您可以指定 hello 名稱和您的 Azure 儲存體帳戶金鑰。 請參閱[Azure 儲存體連結服務](../data-factory/data-factory-azure-blob-connector.md#azure-storage-linked-service)如需詳細資訊 JSON 屬性使用 toodefine Azure 儲存體連結服務。

```json
{
    "name": "[variables('storageLinkedServiceName')]",
    "type": "linkedservices",
    "dependsOn": [ "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]" ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('storageAccountName'),';AccountKey=',parameters('storageAccountKey'))]"
        }
    }
}
```
hello **connectionString**使用 hello storageAccountName 及 storageAccountKey 參數。 您部署 hello 範本時指定這些參數的值。  

#### <a name="hdinsight-on-demand-linked-service"></a>HDInsight 隨選連結服務
在 hello 隨 HDInsight 連結服務定義中，指定 hello Data Factory 服務 toocreate HDInsight Hadoop 叢集在執行階段所使用的組態參數的值。 請參閱[計算連結的服務](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service)文件如需詳細資訊 JSON 屬性使用 toodefine HDInsight 視連結的服務。  

```json

{
    "type": "linkedservices",
    "name": "[variables('hdInsightOnDemandLinkedServiceName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedservices/', variables('storageLinkedServiceName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "sshUserName": "myuser",                            
            "sshPassword": "MyPassword!",
            "linkedServiceName": "[variables('storageLinkedServiceName')]"
        }
    }
}
```
請注意下列點 hello:

* hello Data Factory 建立**linux**為您的 HDInsight 叢集。
* hello HDInsight Hadoop 叢集會建立於 hello 相同 hello 儲存體帳戶與區域。
* 請注意 hello *timeToLive*設定。 hello 資料處理站會在 hello 叢集正在閒置 30 分鐘後自動刪除 hello 叢集。
* hello HDInsight 叢集建立**預設容器**hello hello JSON 中指定的 blob 儲存體中 (**linkedServiceName**)。 HDInsight 刪除 hello 叢集時，不會刪除此容器。 這是設計的行為。 HDInsight 叢集隨 HDInsight 連結服務，以建立每次配量需要處理現有的叢集即時除非 toobe (**timeToLive**) 和 hello 處理完成時刪除。

如需詳細資訊，請參閱 [HDInsight 隨選連結服務](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) 。

> [!IMPORTANT]
> 隨著處理的配量越來越多，您會在 Azure Blob 儲存體中看到許多容器。 如果您不需要它們進行疑難排解的 hello 工作，您可能會想 toodelete 它們 tooreduce hello 儲存體成本。 這些容器的 hello 名稱遵循模式: 「 adf**yourdatafactoryname**-**linkedservicename**-datetimestamp"。 使用工具，例如[Microsoft 儲存體總管](http://storageexplorer.com/)toodelete 容器，在您的 Azure blob 儲存體。

#### <a name="azure-blob-input-dataset"></a>Azure Blob 輸入資料集
在 hello 輸入資料集定義中，您可以指定 hello blob 容器、 資料夾和檔案名稱，其中包含 hello 輸入的資料。 請參閱[Azure Blob 資料集屬性](../data-factory/data-factory-azure-blob-connector.md#dataset-properties)如需詳細資訊 JSON 屬性使用 toodefine Azure Blob 資料集。

```json

{
    "type": "datasets",
    "name": "[variables('blobInputDatasetName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('storageLinkedServiceName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "[variables('storageLinkedServiceName')]",
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

請注意下列 hello JSON 定義中的特定設定的 hello:

```json
"fileName": "input.log",
"folderPath": "adfgetstarted/inputdata",
```

#### <a name="azure-blob-output-dataset"></a>Azure Blob 輸出資料集
在 hello 輸出資料集定義中，您可以指定 hello 的 blob 容器，並保存 hello 輸出資料之資料夾的名稱。 請參閱[Azure Blob 資料集屬性](../data-factory/data-factory-azure-blob-connector.md#dataset-properties)如需詳細資訊 JSON 屬性使用 toodefine Azure Blob 資料集。  

```json

{
    "type": "datasets",
    "name": "[variables('blobOutputDatasetName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('storageLinkedServiceName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "[variables('storageLinkedServiceName')]",
        "typeProperties": {
            "folderPath": "adfgetstarted/partitioneddata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1,
            "style": "EndOfInterval"
        }
    }
}
```

hello folderPath 指定保存 hello 輸出資料的 hello 路徑 toohello 資料夾：

```json
"folderPath": "adfgetstarted/partitioneddata",
```

hello[資料集可用性](../data-factory/data-factory-create-datasets.md#dataset-availability)設定如下所示：

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "style": "EndOfInterval"
},
```

在 Azure Data Factory，輸出資料集可用性磁碟機 hello 管線。 在此範例中，hello 點產生配量每月 hello (為 EndOfInterval) 當月最後一天。 如需詳細資訊，請參閱 [Data Factory 排程和執行](../data-factory/data-factory-scheduling-and-execution.md)。

#### <a name="data-pipeline"></a>Data Pipeline
您可以定義在隨選 Azure HDInsight 叢集上執行 Hive 指令碼以轉換資料的管線。 請參閱[管線 JSON](../data-factory/data-factory-create-pipelines.md#pipeline-json)如需 JSON 用項目 toodefine 管線，以在此範例的描述。

```json
{
    "type": "datapipelines",
    "name": "[parameters('dataFactoryName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('storageLinkedServiceName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('hdInsightOnDemandLinkedServiceName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/datasets/', variables('blobInputDatasetName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/datasets/', variables('blobOutputDatasetName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "description": "Azure Data Factory pipeline with an Hadoop Hive activity",
        "activities": [
            {
                "type": "HDInsightHive",
                "typeProperties": {
                    "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                    "scriptLinkedService": "[variables('storageLinkedServiceName')]",
                    "defines": {
                        "inputtable": "[concat('wasb://adfgetstarted@', parameters('storageAccountName'), '.blob.core.windows.net/inputdata')]",
                        "partitionedtable": "[concat('wasb://adfgetstarted@', parameters('storageAccountName'), '.blob.core.windows.net/partitioneddata')]"
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
                "name": "RunSampleHiveActivity",
                "linkedServiceName": "HDInsightOnDemandLinkedService"
            }
        ],
        "start": "2016-01-01T00:00:00Z",
        "end": "2016-01-31T00:00:00Z",
        "isPaused": false
    }
}
```

hello 管線包含一個活動，HDInsightHive 活動。 由於開始和結束日期都在 2016 年 1 月，因此只處理一個月的資料 (配量)。 同時*啟動*和*結束*hello 活動的已過去的日期，因此 hello Data Factory hello 月份立即處理資料。 如果 hello 結尾是未來的日期，hello 資料 factory hello 時間時，就會建立另一個配量。 如需詳細資訊，請參閱 [Data Factory 排程和執行](../data-factory/data-factory-scheduling-and-execution.md)。

## <a name="clean-up-hello-tutorial"></a>清除 hello 教學課程

### <a name="delete-hello-blob-containers-created-by-on-demand-hdinsight-cluster"></a>刪除 hello 隨選 HDInsight 叢集所建立的 blob 容器
每次配量需要處理現有的即時叢集 (timeToLive); 除非 toobe，HDInsight 叢集建立隨 HDInsight 連結服務而且 hello 叢集 hello 處理完成時刪除。 針對每個群集，Azure Data Factory，請在 hello 作為 hello 叢集 hello 預設 stroage 帳戶的 Azure blob 儲存體中建立 blob 容器。 即使已刪除 HDInsight 叢集，hello 預設 blob 儲存體容器和相關聯的 hello 儲存體帳戶不會刪除。 這是設計的行為。 隨著處理的配量越來越多，您會在 Azure Blob 儲存體中看到許多容器。 如果您不需要它們進行疑難排解的 hello 工作，您可能會想 toodelete 它們 tooreduce hello 儲存體成本。 這些容器的 hello 名稱遵循模式： `adfyourdatafactoryname-linkedservicename-datetimestamp`。

刪除 hello **adfjobs**和**adfyourdatafactoryname-linkedservicename-datetimestamp**資料夾。 hello adfjobs 容器包含從 Azure Data Factory 的作業記錄。

### <a name="delete-hello-resource-group"></a>刪除 hello 資源群組
[Azure 資源管理員](../azure-resource-manager/resource-group-overview.md)是使用的 toodeploy，管理和監視您的解決方案，為群組。  刪除資源群組會刪除所有 hello hello 群組內的元件。  

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 按一下**資源群組**hello 左窗格上。
3. 按一下您建立 PowerShell 指令碼中的 hello 資源群組名稱。 如果您有太多的資源群組列出，請使用 hello 篩選條件。 會開啟 hello 資源群組的新刀鋒視窗。
4. 在 hello**資源**磚中，您應該擁有 hello 預設儲存體帳戶和 hello 資料處理站所列，除非您與其他專案共用 hello 資源群組。
5. 按一下**刪除**hello 頂端 hello 刀鋒視窗上。 這樣會刪除 hello 儲存體帳戶和儲存在 hello 儲存體帳戶中的 hello 資料。
6. 輸入 hello 資源群組名稱 tooconfirm 刪除，然後再按一下**刪除**。

如果您不想 toodelete hello 儲存體帳戶，當您刪除 hello 資源群組時，請考慮 hello 下列架構藉由分隔 hello 預設儲存體帳戶中的 hello 的商務資料。 在此情況下，您會擁有一個 hello hello 的商務資料的儲存體帳戶的資源群組，並且 hello HDInsight 連結服務與 hello data factory 的 hello 預設儲存體帳戶的其他資源群組。 當您刪除 hello 第二個資源群組時，它不會影響 hello 商務資料的儲存體帳戶。 toodo 因此：

* 新增下列 toohello 最上層資源群組，以及 hello Microsoft.DataFactory/datafactories 資源，資源管理員範本中的 hello。 它會建立儲存體帳戶：

    ```json
    {
        "name": "[parameters('defaultStorageAccountName')]",
        "type": "Microsoft.Storage/storageAccounts",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('defaultApiVersion')]",
        "dependsOn": [ ],
        "tags": {

        },
        "properties": {
            "accountType": "Standard_LRS"
        }
    },
    ```
* 加入新連結的服務點 toohello 新儲存體帳戶：

    ```json
    {
        "dependsOn": [ "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]" ],
        "type": "linkedservices",
        "name": "[variables('defaultStorageLinkedServiceName')]",
        "apiVersion": "[variables('apiVersion')]",
        "properties": {
            "type": "AzureStorage",
            "typeProperties": {
                "connectionString": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('defaultStorageAccountName'),';AccountKey=',listKeys(resourceId('Microsoft.Storage/storageAccounts', variables('defaultStorageAccountName')), variables('defaultApiVersion')).key1)]"
            }
        }
    },
    ```
* 與其他的 dependsOn additionalLinkedServiceNames 設定 hello HDInsight ondemand 連結服務：

    ```json
    {
        "dependsOn": [
            "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
            "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedservices/', variables('defaultStorageLinkedServiceName'))]",
            "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedservices/', variables('storageLinkedServiceName'))]"

        ],
        "type": "linkedservices",
        "name": "[variables('hdInsightOnDemandLinkedServiceName')]",
        "apiVersion": "[variables('apiVersion')]",
        "properties": {
            "type": "HDInsightOnDemand",
            "typeProperties": {
                "version": "3.5",
                "clusterSize": 1,
                "timeToLive": "00:05:00",
                "osType": "Linux",
                "sshUserName": "myuser",                            
                "sshPassword": "MyPassword!",
                "linkedServiceName": "[variables('storageLinkedServiceName')]",
                "additionalLinkedServiceNames": "[variables('defaultStorageLinkedServiceName')]"
            }
        }
    },            
    ```
## <a name="next-steps"></a>後續步驟
在本文中，您已經學會如何 toouse Azure Data Factory toocreate-隨選 HDInsight 叢集 tooprocess Hive 工作。 多個 tooread:

* [Hadoop 教學課程：開始在 HDInsight 中使用以 Linux 為基礎的 Hadoop](hdinsight-hadoop-linux-tutorial-get-started.md)
* [在 HDInsight 中建立以 Linux 為基礎的 Hadoop 叢集](hdinsight-hadoop-provision-linux-clusters.md)
* [HDInsight 文件](https://azure.microsoft.com/documentation/services/hdinsight/)
* [Data Factory 文件](https://azure.microsoft.com/documentation/services/data-factory/)

## <a name="appendix"></a>附錄

### <a name="azure-cli-script"></a>Azure CLI 指令碼
您可以使用 Azure CLI，而不是使用 Azure PowerShell toodo hello 教學課程。 toouse Azure CLI 第一次安裝 Azure CLI，依照下列指示的 hello:

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

#### <a name="use-azure-cli-tooprepare-hello-storage-and-copy-hello-files"></a>使用 Azure CLI tooprepare hello 存放裝置，並將 hello 檔案複製

```
azure login

azure config mode arm

azure group create --name "<Azure Resource Group Name>" --location "East US 2"

azure storage account create --resource-group "<Azure Resource Group Name>" --location "East US 2" --type "LRS" <Azure Storage Account Name>

azure storage account keys list --resource-group "<Azure Resource Group Name>" "<Azure Storage Account Name>"
azure storage container create "adfgetstarted" --account-name "<Azure Storage AccountName>" --account-key "<Azure Storage Account Key>"

azure storage blob copy start "https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log" --dest-account-name "<Azure Storage Account Name>" --dest-account-key "<Azure Storage Account Key>" --dest-container "adfgetstarted"
azure storage blob copy start "https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql" --dest-account-name "<Azure Storage Account Name>" --dest-account-key "<Azure Storage Account Key>" --dest-container "adfgetstarted"
```

hello 的容器名稱*adfgetstarted*。 讓它保持原狀。 否則，您必須 tooupdate hello Resource Manager 範本。 如果您需要此 CLI 指令碼的說明，請參閱[使用 hello 與 Azure 儲存體的 Azure CLI](../storage/common/storage-azure-cli.md)。
