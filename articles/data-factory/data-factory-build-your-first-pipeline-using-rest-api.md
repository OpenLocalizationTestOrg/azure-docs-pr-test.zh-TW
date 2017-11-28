---
title: "aaaBuild 您第一次的 data factory (REST) |Microsoft 文件"
description: "在本教學課程中，您會使用 Data Factory REST API 建立範例 Azure Data Factory 管線。"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 7e0a2465-2d85-4143-a4bb-42e03c273097
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 5d8e39bd598cca35f91d501bad74e8a8436f8f89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-data-factory-rest-api"></a><span data-ttu-id="64506-103">教學課程：使用 Data Factory REST API 建置您的第一個 Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="64506-103">Tutorial: Build your first Azure data factory using Data Factory REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="64506-104">概觀和必要條件</span><span class="sxs-lookup"><span data-stu-id="64506-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="64506-105">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="64506-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="64506-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="64506-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="64506-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="64506-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="64506-108">Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="64506-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="64506-109">REST API</span><span class="sxs-lookup"><span data-stu-id="64506-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)
>
>


<span data-ttu-id="64506-110">在本文中，您使用 Data Factory REST API toocreate 第一個 Azure data factory。</span><span class="sxs-lookup"><span data-stu-id="64506-110">In this article, you use Data Factory REST API toocreate your first Azure data factory.</span></span> <span data-ttu-id="64506-111">toodo hello 教學課程中使用其他工具/Sdk，從 hello 下拉式清單選取其中一個 hello 選項。</span><span class="sxs-lookup"><span data-stu-id="64506-111">toodo hello tutorial using other tools/SDKs, select one of hello options from hello drop-down list.</span></span>

<span data-ttu-id="64506-112">在此教學課程中的 hello 管線有一個活動： **HDInsight Hive 活動**。</span><span class="sxs-lookup"><span data-stu-id="64506-112">hello pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="64506-113">此活動會在轉換輸入資料 tooproduce 輸出資料的 Azure HDInsight 叢集上執行 hive 指令碼。</span><span class="sxs-lookup"><span data-stu-id="64506-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data tooproduce output data.</span></span> <span data-ttu-id="64506-114">hello 管線是排程的 toorun，每個月之間 hello 指定開始和結束時間之後。</span><span class="sxs-lookup"><span data-stu-id="64506-114">hello pipeline is scheduled toorun once a month between hello specified start and end times.</span></span>

> [!NOTE]
> <span data-ttu-id="64506-115">本文並未涵蓋所有 hello REST API。</span><span class="sxs-lookup"><span data-stu-id="64506-115">This article does not cover all hello REST API.</span></span> <span data-ttu-id="64506-116">如需 REST API 的完整文件，請參閱 [Data Factory REST API 參考](/rest/api/datafactory/)。</span><span class="sxs-lookup"><span data-stu-id="64506-116">For comprehensive documentation on REST API, see [Data Factory REST API Reference](/rest/api/datafactory/).</span></span>
> 
> <span data-ttu-id="64506-117">一個管線中可以有多個活動。</span><span class="sxs-lookup"><span data-stu-id="64506-117">A pipeline can have more than one activity.</span></span> <span data-ttu-id="64506-118">此外，您可以藉由設定 hello 輸出資料集的一個活動 hello 的輸入資料集的 hello 其他活動鏈結 （執行一個活動執行另一個之後） 的兩個活動。</span><span class="sxs-lookup"><span data-stu-id="64506-118">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="64506-119">如需詳細資訊，請參閱 [Data Factory 排程和執行](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline)。</span><span class="sxs-lookup"><span data-stu-id="64506-119">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="64506-120">必要條件</span><span class="sxs-lookup"><span data-stu-id="64506-120">Prerequisites</span></span>
* <span data-ttu-id="64506-121">閱讀[教學課程概觀](data-factory-build-your-first-pipeline.md)文件，以及完成 hello**必要條件**步驟。</span><span class="sxs-lookup"><span data-stu-id="64506-121">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete hello **prerequisite** steps.</span></span>
* <span data-ttu-id="64506-122">在您的電腦上安裝 [Curl](https://curl.haxx.se/dlwiz/) 。</span><span class="sxs-lookup"><span data-stu-id="64506-122">Install [Curl](https://curl.haxx.se/dlwiz/) on your machine.</span></span> <span data-ttu-id="64506-123">您可以使用 hello CURL 工具與其他命令 toocreate data factory。</span><span class="sxs-lookup"><span data-stu-id="64506-123">You use hello CURL tool with REST commands toocreate a data factory.</span></span>
* <span data-ttu-id="64506-124">請依照 [本文](../azure-resource-manager/resource-group-create-service-principal-portal.md) 的指示：</span><span class="sxs-lookup"><span data-stu-id="64506-124">Follow instructions from [this article](../azure-resource-manager/resource-group-create-service-principal-portal.md) to:</span></span>
  1. <span data-ttu-id="64506-125">在 Azure Active Directory 中建立名為 **ADFGetStartedApp** 的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="64506-125">Create a Web application named **ADFGetStartedApp** in Azure Active Directory.</span></span>
  2. <span data-ttu-id="64506-126">取得**用戶端識別碼**和**秘密金鑰**。</span><span class="sxs-lookup"><span data-stu-id="64506-126">Get **client ID** and **secret key**.</span></span>
  3. <span data-ttu-id="64506-127">取得 **租用戶識別碼**。</span><span class="sxs-lookup"><span data-stu-id="64506-127">Get **tenant ID**.</span></span>
  4. <span data-ttu-id="64506-128">指派 hello **ADFGetStartedApp**應用程式 toohello**資料 Factory 參與者**角色。</span><span class="sxs-lookup"><span data-stu-id="64506-128">Assign hello **ADFGetStartedApp** application toohello **Data Factory Contributor** role.</span></span>
* <span data-ttu-id="64506-129">安裝 [Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="64506-129">Install [Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="64506-130">啟動**PowerShell**和 hello 執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="64506-130">Launch **PowerShell** and run hello following command.</span></span> <span data-ttu-id="64506-131">保持開啟 Azure PowerShell 直到本教學課程中的 hello 結尾。</span><span class="sxs-lookup"><span data-stu-id="64506-131">Keep Azure PowerShell open until hello end of this tutorial.</span></span> <span data-ttu-id="64506-132">如果您關閉並重新開啟，您需要 toorun hello 命令一次。</span><span class="sxs-lookup"><span data-stu-id="64506-132">If you close and reopen, you need toorun hello commands again.</span></span>
  1. <span data-ttu-id="64506-133">執行**登入 AzureRmAccount** ，然後輸入 hello 使用者名稱和密碼，您會使用 toosign toohello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="64506-133">Run **Login-AzureRmAccount** and enter hello user name and password that you use toosign in toohello Azure portal.</span></span>
  2. <span data-ttu-id="64506-134">執行**Get AzureRmSubscription** tooview 所有 hello 這個帳戶的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="64506-134">Run **Get-AzureRmSubscription** tooview all hello subscriptions for this account.</span></span>
  3. <span data-ttu-id="64506-135">執行**Get AzureRmSubscription-訂用帳戶名稱 NameOfAzureSubscription |設定 AzureRmContext** tooselect hello 訂用帳戶，您想要使用 toowork。</span><span class="sxs-lookup"><span data-stu-id="64506-135">Run **Get-AzureRmSubscription -SubscriptionName NameOfAzureSubscription | Set-AzureRmContext** tooselect hello subscription that you want toowork with.</span></span> <span data-ttu-id="64506-136">取代**NameOfAzureSubscription** hello 的 Azure 訂用帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="64506-136">Replace **NameOfAzureSubscription** with hello name of your Azure subscription.</span></span>
* <span data-ttu-id="64506-137">建立 Azure 資源群組名稱為**ADFTutorialResourceGroup**藉由執行下列命令在 hello PowerShell 中的 hello:</span><span class="sxs-lookup"><span data-stu-id="64506-137">Create an Azure resource group named **ADFTutorialResourceGroup** by running hello following command in hello PowerShell:</span></span>

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

   <span data-ttu-id="64506-138">本教學課程中的 hello 步驟假設您使用名為 ADFTutorialResourceGroup hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="64506-138">Some of hello steps in this tutorial assume that you use hello resource group named ADFTutorialResourceGroup.</span></span> <span data-ttu-id="64506-139">如果您使用不同的資源群組，您會在本教學課程需要資源群組來取代 ADFTutorialResourceGroup toouse hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="64506-139">If you use a different resource group, you need toouse hello name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span></span>

## <a name="create-json-definitions"></a><span data-ttu-id="64506-140">建立 JSON 定義</span><span class="sxs-lookup"><span data-stu-id="64506-140">Create JSON definitions</span></span>
<span data-ttu-id="64506-141">建立下列 hello curl.exe 所在的資料夾中的 JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="64506-141">Create following JSON files in hello folder where curl.exe is located.</span></span>

### <a name="datafactoryjson"></a><span data-ttu-id="64506-142">datafactory.json</span><span class="sxs-lookup"><span data-stu-id="64506-142">datafactory.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="64506-143">名稱必須是全域唯一的因此您可能需要 tooprefix/後置詞 ADFCopyTutorialDF toomake 它唯一的名稱。</span><span class="sxs-lookup"><span data-stu-id="64506-143">Name must be globally unique, so you may want tooprefix/suffix ADFCopyTutorialDF toomake it a unique name.</span></span>
>
>

```JSON
{
    "name": "FirstDataFactoryREST",
    "location": "WestUS"
}
```

### <a name="azurestoragelinkedservicejson"></a><span data-ttu-id="64506-144">azurestoragelinkedservice.json</span><span class="sxs-lookup"><span data-stu-id="64506-144">azurestoragelinkedservice.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="64506-145">以 Azure 儲存體帳戶的名稱和金鑰取代 **accountname** 和 **accountkey**。</span><span class="sxs-lookup"><span data-stu-id="64506-145">Replace **accountname** and **accountkey** with name and key of your Azure storage account.</span></span> <span data-ttu-id="64506-146">toolearn 如何 tooget 您的儲存體存取金鑰，請參閱有關如何 tooview、 複製和重新產生儲存體存取金鑰中的 hello 資訊[管理您的儲存體帳戶](../storage/common/storage-create-storage-account.md#manage-your-storage-account)。</span><span class="sxs-lookup"><span data-stu-id="64506-146">toolearn how tooget your storage access key, see hello information about how tooview, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
>
>

```JSON
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

### <a name="hdinsightondemandlinkedservicejson"></a><span data-ttu-id="64506-147">hdinsightondemandlinkedservice.json</span><span class="sxs-lookup"><span data-stu-id="64506-147">hdinsightondemandlinkedservice.json</span></span>

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

<span data-ttu-id="64506-148">hello 下表提供 hello hello 程式碼片段中使用的 JSON 屬性的說明：</span><span class="sxs-lookup"><span data-stu-id="64506-148">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

| <span data-ttu-id="64506-149">屬性</span><span class="sxs-lookup"><span data-stu-id="64506-149">Property</span></span> | <span data-ttu-id="64506-150">說明</span><span class="sxs-lookup"><span data-stu-id="64506-150">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="64506-151">ClusterSize</span><span class="sxs-lookup"><span data-stu-id="64506-151">ClusterSize</span></span> |<span data-ttu-id="64506-152">Hello HDInsight 叢集的大小。</span><span class="sxs-lookup"><span data-stu-id="64506-152">Size of hello HDInsight cluster.</span></span> |
| <span data-ttu-id="64506-153">TimeToLive</span><span class="sxs-lookup"><span data-stu-id="64506-153">TimeToLive</span></span> |<span data-ttu-id="64506-154">於刪除之前，請指定 hello HDInsight 叢集，該 hello 閒置時間。</span><span class="sxs-lookup"><span data-stu-id="64506-154">Specifies that hello idle time for hello HDInsight cluster, before it is deleted.</span></span> |
| <span data-ttu-id="64506-155">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="64506-155">linkedServiceName</span></span> |<span data-ttu-id="64506-156">指定 hello 是使用的 toostore hello 記錄 HDInsight 所產生的儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="64506-156">Specifies hello storage account that is used toostore hello logs that are generated by HDInsight</span></span> |

<span data-ttu-id="64506-157">請注意下列點 hello:</span><span class="sxs-lookup"><span data-stu-id="64506-157">Note hello following points:</span></span>

* <span data-ttu-id="64506-158">hello Data Factory 建立**linux**上方 JSON hello 與您的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="64506-158">hello Data Factory creates a **Linux-based** HDInsight cluster for you with hello above JSON.</span></span> <span data-ttu-id="64506-159">如需詳細資訊，請參閱 [HDInsight 隨選連結服務](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) 。</span><span class="sxs-lookup"><span data-stu-id="64506-159">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
* <span data-ttu-id="64506-160">您可以使用 **自己的 HDInsight 叢集** ，不必使用隨選的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="64506-160">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="64506-161">如需詳細資訊，請參閱 [HDInsight 連結服務](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) 。</span><span class="sxs-lookup"><span data-stu-id="64506-161">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span></span>
* <span data-ttu-id="64506-162">hello HDInsight 叢集建立**預設容器**hello hello JSON 中指定的 blob 儲存體中 (**linkedServiceName**)。</span><span class="sxs-lookup"><span data-stu-id="64506-162">hello HDInsight cluster creates a **default container** in hello blob storage you specified in hello JSON (**linkedServiceName**).</span></span> <span data-ttu-id="64506-163">HDInsight 刪除 hello 叢集時，不會刪除此容器。</span><span class="sxs-lookup"><span data-stu-id="64506-163">HDInsight does not delete this container when hello cluster is deleted.</span></span> <span data-ttu-id="64506-164">這是設計的行為。</span><span class="sxs-lookup"><span data-stu-id="64506-164">This behavior is by design.</span></span> <span data-ttu-id="64506-165">HDInsight 叢集隨 HDInsight 連結服務，以建立每一次，除非有現有的叢集即時處理配量 (**timeToLive**) 和 hello 處理完成時刪除。</span><span class="sxs-lookup"><span data-stu-id="64506-165">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (**timeToLive**) and is deleted when hello processing is done.</span></span>

    <span data-ttu-id="64506-166">隨著處理的配量越來越多，您會在 Azure Blob 儲存體中看到許多容器。</span><span class="sxs-lookup"><span data-stu-id="64506-166">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="64506-167">如果您不需要它們進行疑難排解的 hello 工作，您可能會想 toodelete 它們 tooreduce hello 儲存體成本。</span><span class="sxs-lookup"><span data-stu-id="64506-167">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="64506-168">這些容器的 hello 名稱遵循模式: 「 adf**yourdatafactoryname**-**linkedservicename**-datetimestamp"。</span><span class="sxs-lookup"><span data-stu-id="64506-168">hello names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="64506-169">使用工具，例如[Microsoft 儲存體總管](http://storageexplorer.com/)toodelete 容器，在您的 Azure blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="64506-169">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) toodelete containers in your Azure blob storage.</span></span>

<span data-ttu-id="64506-170">如需詳細資訊，請參閱 [HDInsight 隨選連結服務](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) 。</span><span class="sxs-lookup"><span data-stu-id="64506-170">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>

### <a name="inputdatasetjson"></a><span data-ttu-id="64506-171">inputdataset.json</span><span class="sxs-lookup"><span data-stu-id="64506-171">inputdataset.json</span></span>

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

<span data-ttu-id="64506-172">hello JSON 定義名為資料集**AzureBlobInput**，代表 hello 管線中活動的輸入的資料。</span><span class="sxs-lookup"><span data-stu-id="64506-172">hello JSON defines a dataset named **AzureBlobInput**, which represents input data for an activity in hello pipeline.</span></span> <span data-ttu-id="64506-173">此外，它會指定 hello 輸入的資料位於呼叫 hello blob 容器**adfgetstarted**和 hello 資料夾稱為**inputdata**。</span><span class="sxs-lookup"><span data-stu-id="64506-173">In addition, it specifies that hello input data is located in hello blob container called **adfgetstarted** and hello folder called **inputdata**.</span></span>

<span data-ttu-id="64506-174">hello 下表提供 hello hello 程式碼片段中使用的 JSON 屬性的說明：</span><span class="sxs-lookup"><span data-stu-id="64506-174">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

| <span data-ttu-id="64506-175">屬性</span><span class="sxs-lookup"><span data-stu-id="64506-175">Property</span></span> | <span data-ttu-id="64506-176">說明</span><span class="sxs-lookup"><span data-stu-id="64506-176">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="64506-177">類型</span><span class="sxs-lookup"><span data-stu-id="64506-177">type</span></span> |<span data-ttu-id="64506-178">hello 類型屬性是設定 tooAzureBlob，因為資料常駐於 Azure blob 儲存體中。</span><span class="sxs-lookup"><span data-stu-id="64506-178">hello type property is set tooAzureBlob because data resides in Azure blob storage.</span></span> |
| <span data-ttu-id="64506-179">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="64506-179">linkedServiceName</span></span> |<span data-ttu-id="64506-180">是指您稍早建立的 StorageLinkedService toohello。</span><span class="sxs-lookup"><span data-stu-id="64506-180">refers toohello StorageLinkedService you created earlier.</span></span> |
| <span data-ttu-id="64506-181">fileName</span><span class="sxs-lookup"><span data-stu-id="64506-181">fileName</span></span> |<span data-ttu-id="64506-182">這是選用屬性。</span><span class="sxs-lookup"><span data-stu-id="64506-182">This property is optional.</span></span> <span data-ttu-id="64506-183">如果您省略這個屬性時，會挑出 hello folderPath 中的所有 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="64506-183">If you omit this property, all hello files from hello folderPath are picked.</span></span> <span data-ttu-id="64506-184">在此情況下，只有 hello input.log 會進行處理。</span><span class="sxs-lookup"><span data-stu-id="64506-184">In this case, only hello input.log is processed.</span></span> |
| <span data-ttu-id="64506-185">類型</span><span class="sxs-lookup"><span data-stu-id="64506-185">type</span></span> |<span data-ttu-id="64506-186">hello 記錄檔是以文字格式，因此我們使用 TextFormat。</span><span class="sxs-lookup"><span data-stu-id="64506-186">hello log files are in text format, so we use TextFormat.</span></span> |
| <span data-ttu-id="64506-187">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="64506-187">columnDelimiter</span></span> |<span data-ttu-id="64506-188">hello 記錄檔中的資料行是以逗號 （，） 分隔</span><span class="sxs-lookup"><span data-stu-id="64506-188">columns in hello log files are delimited by a comma character (,)</span></span> |
| <span data-ttu-id="64506-189">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="64506-189">frequency/interval</span></span> |<span data-ttu-id="64506-190">設定 tooMonth 頻率和間隔為 1，這表示的 hello 輸入配量可使用每個月。</span><span class="sxs-lookup"><span data-stu-id="64506-190">frequency set tooMonth and interval is 1, which means that hello input slices are available monthly.</span></span> |
| <span data-ttu-id="64506-191">external</span><span class="sxs-lookup"><span data-stu-id="64506-191">external</span></span> |<span data-ttu-id="64506-192">設定此屬性是 tootrue hello 輸入的資料不會產生 hello Data Factory 服務。</span><span class="sxs-lookup"><span data-stu-id="64506-192">this property is set tootrue if hello input data is not generated by hello Data Factory service.</span></span> |

### <a name="outputdatasetjson"></a><span data-ttu-id="64506-193">outputdataset.json</span><span class="sxs-lookup"><span data-stu-id="64506-193">outputdataset.json</span></span>

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

<span data-ttu-id="64506-194">hello JSON 定義名為資料集**AzureBlobOutput**，代表 hello 管線中活動的輸出資料。</span><span class="sxs-lookup"><span data-stu-id="64506-194">hello JSON defines a dataset named **AzureBlobOutput**, which represents output data for an activity in hello pipeline.</span></span> <span data-ttu-id="64506-195">此外，它會指定 hello 結果會儲存在稱為 hello blob 容器**adfgetstarted**和 hello 資料夾稱為**partitioneddata**。</span><span class="sxs-lookup"><span data-stu-id="64506-195">In addition, it specifies that hello results are stored in hello blob container called **adfgetstarted** and hello folder called **partitioneddata**.</span></span> <span data-ttu-id="64506-196">hello**可用性**區段會指定該 hello 輸出資料集產生每月為基礎。</span><span class="sxs-lookup"><span data-stu-id="64506-196">hello **availability** section specifies that hello output dataset is produced on a monthly basis.</span></span>

### <a name="pipelinejson"></a><span data-ttu-id="64506-197">pipeline.json</span><span class="sxs-lookup"><span data-stu-id="64506-197">pipeline.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="64506-198">以您的 Azure 儲存體帳戶名稱取代 **storageaccountname** 。</span><span class="sxs-lookup"><span data-stu-id="64506-198">Replace **storageaccountname** with name of your Azure storage account.</span></span>
>
>

```JSON
{
    "name": "MyFirstPipeline",
    "properties": {
        "description": "My first Azure Data Factory pipeline",
        "activities": [{
            "type": "HDInsightHive",
            "typeProperties": {
                "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                "scriptLinkedService": "AzureStorageLinkedService",
                "defines": {
                    "inputtable": "wasb://adfgetstarted@<stroageaccountname>.blob.core.windows.net/inputdata",
                    "partitionedtable": "wasb://adfgetstarted@<stroageaccountname>t.blob.core.windows.net/partitioneddata"
                }
            },
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
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
        }],
        "start": "2017-07-10T00:00:00Z",
        "end": "2017-07-11T00:00:00Z",
        "isPaused": false
    }
}
```

<span data-ttu-id="64506-199">在 hello JSON 片段中，您要建立管線的 HDInsight 叢集使用 Hive tooprocess 資料的活動所組成。</span><span class="sxs-lookup"><span data-stu-id="64506-199">In hello JSON snippet, you are creating a pipeline that consists of a single activity that uses Hive tooprocess data on a HDInsight cluster.</span></span>

<span data-ttu-id="64506-200">hello Hive 指令碼檔案， **partitionweblogs.hql**，儲存在 hello Azure 儲存體帳戶 (由 hello scriptLinkedService，稱為**StorageLinkedService**)，然後在**指令碼** hello 容器中的資料夾**adfgetstarted**。</span><span class="sxs-lookup"><span data-stu-id="64506-200">hello Hive script file, **partitionweblogs.hql**, is stored in hello Azure storage account (specified by hello scriptLinkedService, called **StorageLinkedService**), and in **script** folder in hello container **adfgetstarted**.</span></span>

<span data-ttu-id="64506-201">hello**定義**區段會指定 Hive 組態值會傳遞 toohello hive 指令碼的執行階段設定 (例如 ${hiveconf: inputtable}，{hiveconf:partitionedtable} $)。</span><span class="sxs-lookup"><span data-stu-id="64506-201">hello **defines** section specifies runtime settings that are passed toohello hive script as Hive configuration values (e.g ${hiveconf:inputtable}, ${hiveconf:partitionedtable}).</span></span>

<span data-ttu-id="64506-202">hello**啟動**和**結束**hello 管線屬性指定 hello 之 hello 管線的作用期間。</span><span class="sxs-lookup"><span data-stu-id="64506-202">hello **start** and **end** properties of hello pipeline specifies hello active period of hello pipeline.</span></span>

<span data-ttu-id="64506-203">在 hello 活動 JSON 中，您指定該 hello Hive 指令碼在上執行指定 hello hello 計算**linkedServiceName** – **HDInsightOnDemandLinkedService**。</span><span class="sxs-lookup"><span data-stu-id="64506-203">In hello activity JSON, you specify that hello Hive script runs on hello compute specified by hello **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span></span>

> [!NOTE]
> <span data-ttu-id="64506-204">請參閱中的"管線 JSON"[管線和 Azure Data Factory 中的活動](data-factory-create-pipelines.md)hello 前面範例中使用的 JSON 內容的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="64506-204">See "Pipeline JSON" in [Pipelines and activities in Azure Data Factory](data-factory-create-pipelines.md) for details about JSON properties used in hello preceding example.</span></span>
>
>

## <a name="set-global-variables"></a><span data-ttu-id="64506-205">設定全域變數</span><span class="sxs-lookup"><span data-stu-id="64506-205">Set global variables</span></span>
<span data-ttu-id="64506-206">在 Azure PowerShell，執行下列命令以您自己取代 hello 值後的 hello:</span><span class="sxs-lookup"><span data-stu-id="64506-206">In Azure PowerShell, execute hello following commands after replacing hello values with your own:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="64506-207">如需取得用戶端識別碼、用戶端密碼、租用戶識別碼及訂用帳戶識別碼的指示，請參閱 [必要條件](#prerequisites) 一節。</span><span class="sxs-lookup"><span data-stu-id="64506-207">See [Prerequisites](#prerequisites) section for instructions on getting client ID, client secret, tenant ID, and subscription ID.</span></span>
>
>

```PowerShell
$client_id = "<client ID of application in AAD>"
$client_secret = "<client key of application in AAD>"
$tenant = "<Azure tenant ID>";
$subscription_id="<Azure subscription ID>";

$rg = "ADFTutorialResourceGroup"
$adf = "FirstDataFactoryREST"
```


## <a name="authenticate-with-aad"></a><span data-ttu-id="64506-208">使用 AAD 驗證</span><span class="sxs-lookup"><span data-stu-id="64506-208">Authenticate with AAD</span></span>

```PowerShell
$cmd = { .\curl.exe -X POST https://login.microsoftonline.com/$tenant/oauth2/token  -F grant_type=client_credentials  -F resource=https://management.core.windows.net/ -F client_id=$client_id -F client_secret=$client_secret };
$responseToken = Invoke-Command -scriptblock $cmd;
$accessToken = (ConvertFrom-Json $responseToken).access_token;

(ConvertFrom-Json $responseToken)
```


## <a name="create-data-factory"></a><span data-ttu-id="64506-209">建立 Data Factory</span><span class="sxs-lookup"><span data-stu-id="64506-209">Create data factory</span></span>
<span data-ttu-id="64506-210">在此步驟中，您會建立名為 **FirstDataFactoryREST**的 Azure Data Factory。</span><span class="sxs-lookup"><span data-stu-id="64506-210">In this step, you create an Azure Data Factory named **FirstDataFactoryREST**.</span></span> <span data-ttu-id="64506-211">資料處理站可以有一或多個管線。</span><span class="sxs-lookup"><span data-stu-id="64506-211">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="64506-212">其中的管線可以有一或多個活動。</span><span class="sxs-lookup"><span data-stu-id="64506-212">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="64506-213">例如，複製活動 toocopy 資料從來源 tooa 目的地資料存放區和 HDInsight Hive 活動 toorun Hive 指令碼 tootransform 資料。</span><span class="sxs-lookup"><span data-stu-id="64506-213">For example, a Copy Activity toocopy data from a source tooa destination data store and a HDInsight Hive activity toorun a Hive script tootransform data.</span></span> <span data-ttu-id="64506-214">執行下列命令 toocreate hello 資料處理站的 hello:</span><span class="sxs-lookup"><span data-stu-id="64506-214">Run hello following commands toocreate hello data factory:</span></span>

1. <span data-ttu-id="64506-215">指定名為 hello 命令 toovariable **cmd**。</span><span class="sxs-lookup"><span data-stu-id="64506-215">Assign hello command toovariable named **cmd**.</span></span>

    <span data-ttu-id="64506-216">確認您在此處指定 (ADFCopyTutorialDF) 相符項目 hello hello 中指定名稱的 hello data factory 名稱 hello **datafactory.json**。</span><span class="sxs-lookup"><span data-stu-id="64506-216">Confirm that hello name of hello data factory you specify here (ADFCopyTutorialDF) matches hello name specified in hello **datafactory.json**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@datafactory.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/FirstDataFactoryREST?api-version=2015-10-01};
    ```
2. <span data-ttu-id="64506-217">使用執行 hello 命令**Invoke-command**。</span><span class="sxs-lookup"><span data-stu-id="64506-217">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="64506-218">檢視 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="64506-218">View hello results.</span></span> <span data-ttu-id="64506-219">如果 hello data factory 建立成功，您會看見 hello JSON hello data factory 中 hello**結果**; 否則您會看到一則錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="64506-219">If hello data factory has been successfully created, you see hello JSON for hello data factory in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

<span data-ttu-id="64506-220">請注意下列點 hello:</span><span class="sxs-lookup"><span data-stu-id="64506-220">Note hello following points:</span></span>

* <span data-ttu-id="64506-221">hello hello Azure Data Factory 名稱必須是全域唯一的。</span><span class="sxs-lookup"><span data-stu-id="64506-221">hello name of hello Azure Data Factory must be globally unique.</span></span> <span data-ttu-id="64506-222">如果您看到結果中的 hello 錯誤： **Data factory 名稱"FirstDataFactoryREST"不是使用**，執行下列步驟 hello:</span><span class="sxs-lookup"><span data-stu-id="64506-222">If you see hello error in results: **Data factory name “FirstDataFactoryREST” is not available**, do hello following steps:</span></span>
  1. <span data-ttu-id="64506-223">在 hello 變更 hello 名稱 (例如，yournameFirstDataFactoryREST) **datafactory.json**檔案。</span><span class="sxs-lookup"><span data-stu-id="64506-223">Change hello name (for example, yournameFirstDataFactoryREST) in hello **datafactory.json** file.</span></span> <span data-ttu-id="64506-224">請參閱 [Data Factory - 命名規則](data-factory-naming-rules.md) 主題，以了解 Data Factory 成品的命名規則。</span><span class="sxs-lookup"><span data-stu-id="64506-224">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
  2. <span data-ttu-id="64506-225">Hello 第一個命令中其中 hello **$cmd**值指派給變數，請取代 FirstDataFactoryREST hello 新名稱，執行 hello 命令。</span><span class="sxs-lookup"><span data-stu-id="64506-225">In hello first command where hello **$cmd** variable is assigned a value, replace FirstDataFactoryREST with hello new name and run hello command.</span></span>
  3. <span data-ttu-id="64506-226">執行 hello 下面兩個命令 tooinvoke hello REST API toocreate hello 資料處理站和列印 hello hello 作業結果。</span><span class="sxs-lookup"><span data-stu-id="64506-226">Run hello next two commands tooinvoke hello REST API toocreate hello data factory and print hello results of hello operation.</span></span>
* <span data-ttu-id="64506-227">toocreate Data Factory 執行個體，您需要 toobe 參與者/系統管理員的 hello Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="64506-227">toocreate Data Factory instances, you need toobe a contributor/administrator of hello Azure subscription</span></span>
* <span data-ttu-id="64506-228">可能會註冊為未來的 hello 中的 DNS 名稱，因此變得可見 hello hello data factory 名稱。</span><span class="sxs-lookup"><span data-stu-id="64506-228">hello name of hello data factory may be registered as a DNS name in hello future and hence become publicly visible.</span></span>
* <span data-ttu-id="64506-229">如果您收到 hello 錯誤:"**此訂用帳戶不是已註冊的 toouse 命名空間 Microsoft.DataFactory**」，請勿 hello 下列其中一種，然後再試一次發行：</span><span class="sxs-lookup"><span data-stu-id="64506-229">If you receive hello error: "**This subscription is not registered toouse namespace Microsoft.DataFactory**", do one of hello following and try publishing again:</span></span>

  * <span data-ttu-id="64506-230">在 Azure PowerShell 中執行下列命令 tooregister hello Data Factory 提供者的 hello:</span><span class="sxs-lookup"><span data-stu-id="64506-230">In Azure PowerShell, run hello following command tooregister hello Data Factory provider:</span></span>

    ```PowerShell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

      <span data-ttu-id="64506-231">您可以執行下列命令 tooconfirm hello Data Factory 提供者註冊該 hello:</span><span class="sxs-lookup"><span data-stu-id="64506-231">You can run hello following command tooconfirm that hello Data Factory provider is registered:</span></span>
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="64506-232">登入使用 hello hello 到 Azure 訂用帳戶[Azure 入口網站](https://portal.azure.com)並瀏覽 tooa Data Factory 刀鋒視窗 （或） 在 hello Azure 入口網站中建立 data factory。</span><span class="sxs-lookup"><span data-stu-id="64506-232">Login using hello Azure subscription into hello [Azure portal](https://portal.azure.com) and navigate tooa Data Factory blade (or) create a data factory in hello Azure portal.</span></span> <span data-ttu-id="64506-233">這個動作會自動註冊 hello 您的提供者。</span><span class="sxs-lookup"><span data-stu-id="64506-233">This action automatically registers hello provider for you.</span></span>

<span data-ttu-id="64506-234">之前建立管線，您必須 toocreate 幾個 Data Factory 實體第一次。</span><span class="sxs-lookup"><span data-stu-id="64506-234">Before creating a pipeline, you need toocreate a few Data Factory entities first.</span></span> <span data-ttu-id="64506-235">您第一次建立連結的服務 toolink 資料存放區/計算 tooyour 資料存放區，定義輸入和輸出連結的資料存放區中的資料集 toorepresent 資料。</span><span class="sxs-lookup"><span data-stu-id="64506-235">You first create linked services toolink data stores/computes tooyour data store, define input and output datasets toorepresent data in linked data stores.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="64506-236">建立連結的服務</span><span class="sxs-lookup"><span data-stu-id="64506-236">Create linked services</span></span>
<span data-ttu-id="64506-237">在此步驟中，您可以連結您的 Azure 儲存體帳戶和隨 Azure HDInsight 叢集 tooyour 資料處理站。</span><span class="sxs-lookup"><span data-stu-id="64506-237">In this step, you link your Azure Storage account and an on-demand Azure HDInsight cluster tooyour data factory.</span></span> <span data-ttu-id="64506-238">hello 保存 hello hello 管線，在此範例中的輸入和輸出資料的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="64506-238">hello Azure Storage account holds hello input and output data for hello pipeline in this sample.</span></span> <span data-ttu-id="64506-239">hello HDInsight 連結服務是使用的 toorun hello 管線，在此範例中的 hello 活動中指定的 Hive 指令碼。</span><span class="sxs-lookup"><span data-stu-id="64506-239">hello HDInsight linked service is used toorun a Hive script specified in hello activity of hello pipeline in this sample.</span></span>

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="64506-240">建立 Azure 儲存體連結服務</span><span class="sxs-lookup"><span data-stu-id="64506-240">Create Azure Storage linked service</span></span>
<span data-ttu-id="64506-241">在此步驟中，您必須連結您的 Azure 儲存體帳戶 tooyour data factory。</span><span class="sxs-lookup"><span data-stu-id="64506-241">In this step, you link your Azure Storage account tooyour data factory.</span></span> <span data-ttu-id="64506-242">本教學課程中，您使用 hello toostore 輸入/輸出資料與 hello HQL 指令碼檔案的相同 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="64506-242">With this tutorial, you use hello same Azure Storage account toostore input/output data and hello HQL script file.</span></span>

1. <span data-ttu-id="64506-243">指定名為 hello 命令 toovariable **cmd**。</span><span class="sxs-lookup"><span data-stu-id="64506-243">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@azurestoragelinkedservice.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureStorageLinkedService?api-version=2015-10-01};
    ```
2. <span data-ttu-id="64506-244">使用執行 hello 命令**Invoke-command**。</span><span class="sxs-lookup"><span data-stu-id="64506-244">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="64506-245">檢視 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="64506-245">View hello results.</span></span> <span data-ttu-id="64506-246">如果 hello 連結已成功建立服務，您會看到 hello 中的 hello 連結服務的 hello JSON**結果**; 否則您會看到一則錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="64506-246">If hello linked service has been successfully created, you see hello JSON for hello linked service in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="64506-247">建立 Azure HDInsight 連結服務</span><span class="sxs-lookup"><span data-stu-id="64506-247">Create Azure HDInsight linked service</span></span>
<span data-ttu-id="64506-248">在此步驟中，您可以連結的隨選 HDInsight 叢集 tooyour 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="64506-248">In this step, you link an on-demand HDInsight cluster tooyour data factory.</span></span> <span data-ttu-id="64506-249">自動在執行階段建立及刪除它為了處理和閒置 hello 指定的時間量之後 hello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="64506-249">hello HDInsight cluster is automatically created at runtime and deleted after it is done processing and idle for hello specified amount of time.</span></span> <span data-ttu-id="64506-250">您可以使用自己的 HDInsight 叢集，不必使用隨選的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="64506-250">You could use your own HDInsight cluster instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="64506-251">請參閱 [計算連結服務](data-factory-compute-linked-services.md) 以取得詳細資料。</span><span class="sxs-lookup"><span data-stu-id="64506-251">See [Compute Linked Services](data-factory-compute-linked-services.md) for details.</span></span>

1. <span data-ttu-id="64506-252">指定名為 hello 命令 toovariable **cmd**。</span><span class="sxs-lookup"><span data-stu-id="64506-252">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@hdinsightondemandlinkedservice.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/hdinsightondemandlinkedservice?api-version=2015-10-01};
    ```
2. <span data-ttu-id="64506-253">使用執行 hello 命令**Invoke-command**。</span><span class="sxs-lookup"><span data-stu-id="64506-253">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="64506-254">檢視 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="64506-254">View hello results.</span></span> <span data-ttu-id="64506-255">如果 hello 連結已成功建立服務，您會看到 hello 中的 hello 連結服務的 hello JSON**結果**; 否則您會看到一則錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="64506-255">If hello linked service has been successfully created, you see hello JSON for hello linked service in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

## <a name="create-datasets"></a><span data-ttu-id="64506-256">建立資料集</span><span class="sxs-lookup"><span data-stu-id="64506-256">Create datasets</span></span>
<span data-ttu-id="64506-257">在此步驟中，您可以建立資料集 toorepresent hello 輸入和輸出 Hive 處理的資料。</span><span class="sxs-lookup"><span data-stu-id="64506-257">In this step, you create datasets toorepresent hello input and output data for Hive processing.</span></span> <span data-ttu-id="64506-258">這些資料集，請參閱 toohello **StorageLinkedService**稍早在本教學課程中，您已建立。</span><span class="sxs-lookup"><span data-stu-id="64506-258">These datasets refer toohello **StorageLinkedService** you have created earlier in this tutorial.</span></span> <span data-ttu-id="64506-259">hello 連結的服務點 tooan Azure 儲存體帳戶和資料集指定保留輸入 hello 儲存體中的容器、 資料夾、 檔案名稱和輸出資料。</span><span class="sxs-lookup"><span data-stu-id="64506-259">hello linked service points tooan Azure Storage account and datasets specify container, folder, file name in hello storage that holds input and output data.</span></span>

### <a name="create-input-dataset"></a><span data-ttu-id="64506-260">建立輸入資料集</span><span class="sxs-lookup"><span data-stu-id="64506-260">Create input dataset</span></span>
<span data-ttu-id="64506-261">在此步驟中，您可以建立 hello 輸入資料集 toorepresent 輸入的資料儲存在 hello Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="64506-261">In this step, you create hello input dataset toorepresent input data stored in hello Azure Blob storage.</span></span>

1. <span data-ttu-id="64506-262">指定名為 hello 命令 toovariable **cmd**。</span><span class="sxs-lookup"><span data-stu-id="64506-262">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@inputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobInput?api-version=2015-10-01};
    ```
2. <span data-ttu-id="64506-263">使用執行 hello 命令**Invoke-command**。</span><span class="sxs-lookup"><span data-stu-id="64506-263">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="64506-264">檢視 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="64506-264">View hello results.</span></span> <span data-ttu-id="64506-265">如果已成功建立 hello 資料集，您會看見 hello JSON hello hello 中的資料集**結果**; 否則您會看到一則錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="64506-265">If hello dataset has been successfully created, you see hello JSON for hello dataset in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

### <a name="create-output-dataset"></a><span data-ttu-id="64506-266">建立輸出資料集</span><span class="sxs-lookup"><span data-stu-id="64506-266">Create output dataset</span></span>
<span data-ttu-id="64506-267">在此步驟中，您可以建立 hello 輸出資料集 toorepresent 輸出資料儲存在 hello Azure Blob 儲存體中。</span><span class="sxs-lookup"><span data-stu-id="64506-267">In this step, you create hello output dataset toorepresent output data stored in hello Azure Blob storage.</span></span>

1. <span data-ttu-id="64506-268">指定名為 hello 命令 toovariable **cmd**。</span><span class="sxs-lookup"><span data-stu-id="64506-268">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@outputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobOutput?api-version=2015-10-01};
    ```
2. <span data-ttu-id="64506-269">使用執行 hello 命令**Invoke-command**。</span><span class="sxs-lookup"><span data-stu-id="64506-269">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="64506-270">檢視 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="64506-270">View hello results.</span></span> <span data-ttu-id="64506-271">如果已成功建立 hello 資料集，您會看見 hello JSON hello hello 中的資料集**結果**; 否則您會看到一則錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="64506-271">If hello dataset has been successfully created, you see hello JSON for hello dataset in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

## <a name="create-pipeline"></a><span data-ttu-id="64506-272">建立管線</span><span class="sxs-lookup"><span data-stu-id="64506-272">Create pipeline</span></span>
<span data-ttu-id="64506-273">在此步驟中，您會建立第一個具有 **HDInsightHive** 活動的管線。</span><span class="sxs-lookup"><span data-stu-id="64506-273">In this step, you create your first pipeline with a **HDInsightHive** activity.</span></span> <span data-ttu-id="64506-274">輸入的配量可每月 (頻率： Month、 interval: 1)、 每月產生輸出配量和 hello hello 活動的排程器屬性也設定 toomonthly。</span><span class="sxs-lookup"><span data-stu-id="64506-274">Input slice is available monthly (frequency: Month, interval: 1), output slice is produced monthly, and hello scheduler property for hello activity is also set toomonthly.</span></span> <span data-ttu-id="64506-275">hello 輸出資料集和 hello 活動排程器的 hello 設定必須相符。</span><span class="sxs-lookup"><span data-stu-id="64506-275">hello settings for hello output dataset and hello activity scheduler must match.</span></span> <span data-ttu-id="64506-276">目前，輸出資料集是哪些磁碟機 hello 排程，因此您必須建立輸出資料集，即使 hello 活動不會產生任何輸出。</span><span class="sxs-lookup"><span data-stu-id="64506-276">Currently, output dataset is what drives hello schedule, so you must create an output dataset even if hello activity does not produce any output.</span></span> <span data-ttu-id="64506-277">如果 hello 活動不接受任何輸入，您可以略過建立 hello 輸入資料集。</span><span class="sxs-lookup"><span data-stu-id="64506-277">If hello activity doesn't take any input, you can skip creating hello input dataset.</span></span>

<span data-ttu-id="64506-278">確認您看到 hello **input.log**檔案在 hello **adfgetstarted/inputdata** hello Azure blob 儲存體，並執行下列命令 toodeploy hello 管線的 hello 中的資料夾。</span><span class="sxs-lookup"><span data-stu-id="64506-278">Confirm that you see hello **input.log** file in hello **adfgetstarted/inputdata** folder in hello Azure blob storage, and run hello following command toodeploy hello pipeline.</span></span> <span data-ttu-id="64506-279">因為 hello**啟動**和**結束**次數設定在過去的 hello 和**isPaused**是集 toofalse，hello 管線 （hello 管線中的活動） 執行您部署之後，立即。</span><span class="sxs-lookup"><span data-stu-id="64506-279">Since hello **start** and **end** times are set in hello past and **isPaused** is set toofalse, hello pipeline (activity in hello pipeline) runs immediately after you deploy.</span></span>

1. <span data-ttu-id="64506-280">指定名為 hello 命令 toovariable **cmd**。</span><span class="sxs-lookup"><span data-stu-id="64506-280">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@pipeline.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datapipelines/MyFirstPipeline?api-version=2015-10-01};
    ```
2. <span data-ttu-id="64506-281">使用執行 hello 命令**Invoke-command**。</span><span class="sxs-lookup"><span data-stu-id="64506-281">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="64506-282">檢視 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="64506-282">View hello results.</span></span> <span data-ttu-id="64506-283">如果已成功建立 hello 資料集，您會看見 hello JSON hello hello 中的資料集**結果**; 否則您會看到一則錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="64506-283">If hello dataset has been successfully created, you see hello JSON for hello dataset in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```
4. <span data-ttu-id="64506-284">恭喜，您已經成功使用 Azure PowerShell 建立您的第一個管線！</span><span class="sxs-lookup"><span data-stu-id="64506-284">Congratulations, you have successfully created your first pipeline using Azure PowerShell!</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="64506-285">監視管線</span><span class="sxs-lookup"><span data-stu-id="64506-285">Monitor pipeline</span></span>
<span data-ttu-id="64506-286">在此步驟中，您可以使用 Data Factory REST API toomonitor 配量 hello 管線所產生。</span><span class="sxs-lookup"><span data-stu-id="64506-286">In this step, you use Data Factory REST API toomonitor slices being produced by hello pipeline.</span></span>

```PowerShell
$ds ="AzureBlobOutput"

$cmd = {.\curl.exe -X GET -H "Authorization: Bearer $accessToken" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/$ds/slices?start=1970-01-01T00%3a00%3a00.0000000Z"&"end=2016-08-12T00%3a00%3a00.0000000Z"&"api-version=2015-10-01};

$results2 = Invoke-Command -scriptblock $cmd;

IF ((ConvertFrom-Json $results2).value -ne $NULL) {
    ConvertFrom-Json $results2 | Select-Object -Expand value | Format-Table
} else {
        (convertFrom-Json $results2).RemoteException
}
```

> [!IMPORTANT]
> <span data-ttu-id="64506-287">建立隨選 HDInsight 叢集通常需要一些時間 (大約 20 分鐘)。</span><span class="sxs-lookup"><span data-stu-id="64506-287">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="64506-288">因此，預期 hello 管線 tootake**大約 30 分鐘**tooprocess hello 配量。</span><span class="sxs-lookup"><span data-stu-id="64506-288">Therefore, expect hello pipeline tootake **approximately 30 minutes** tooprocess hello slice.</span></span>
>
>

<span data-ttu-id="64506-289">執行 hello Invoke-command 和 hello 下一個直到您看到 hello 配量中的**準備**狀態或**失敗**狀態。</span><span class="sxs-lookup"><span data-stu-id="64506-289">Run hello Invoke-Command and hello next one until you see hello slice in **Ready** state or **Failed** state.</span></span> <span data-ttu-id="64506-290">當 hello 配量處於就緒狀態時，請檢查 hello **partitioneddata**資料夾中 hello **adfgetstarted** hello 您 blob 儲存體容器中的輸出資料。</span><span class="sxs-lookup"><span data-stu-id="64506-290">When hello slice is in Ready state, check hello **partitioneddata** folder in hello **adfgetstarted** container in your blob storage for hello output data.</span></span>  <span data-ttu-id="64506-291">hello 建立隨選 HDInsight 叢集通常需要一些時間。</span><span class="sxs-lookup"><span data-stu-id="64506-291">hello creation of an on-demand HDInsight cluster usually takes some time.</span></span>

![輸出資料](./media/data-factory-build-your-first-pipeline-using-rest-api/three-ouptut-files.png)

> [!IMPORTANT]
> <span data-ttu-id="64506-293">已成功處理 hello 配量時，取得刪除 hello 輸入的檔。</span><span class="sxs-lookup"><span data-stu-id="64506-293">hello input file gets deleted when hello slice is processed successfully.</span></span> <span data-ttu-id="64506-294">因此，如果您想 toorerun hello 配量，或不要 hello 教學課程中上, 傳 hello hello adfgetstarted 容器的輸入的檔 (input.log) toohello inputdata 資料夾。</span><span class="sxs-lookup"><span data-stu-id="64506-294">Therefore, if you want toorerun hello slice or do hello tutorial again, upload hello input file (input.log) toohello inputdata folder of hello adfgetstarted container.</span></span>
>
>

<span data-ttu-id="64506-295">您也可以使用 Azure 入口網站 toomonitor 配量，以及疑難排解任何問題。</span><span class="sxs-lookup"><span data-stu-id="64506-295">You can also use Azure portal toomonitor slices and troubleshoot any issues.</span></span> <span data-ttu-id="64506-296">如需詳細，請參閱 [使用 Azure 入口網站監視管線](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) 。</span><span class="sxs-lookup"><span data-stu-id="64506-296">See [Monitor pipelines using Azure portal](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) details.</span></span>

## <a name="summary"></a><span data-ttu-id="64506-297">摘要</span><span class="sxs-lookup"><span data-stu-id="64506-297">Summary</span></span>
<span data-ttu-id="64506-298">在本教學課程中，您可以建立 Azure data factory tooprocess 資料在 HDInsight hadoop 叢集上執行 Hive 指令碼。</span><span class="sxs-lookup"><span data-stu-id="64506-298">In this tutorial, you created an Azure data factory tooprocess data by running Hive script on a HDInsight hadoop cluster.</span></span> <span data-ttu-id="64506-299">您使用 hello Data Factory 編輯器在 hello Azure 入口網站 toodo hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="64506-299">You used hello Data Factory Editor in hello Azure portal toodo hello following steps:</span></span>

1. <span data-ttu-id="64506-300">建立 Azure **Data Factory**。</span><span class="sxs-lookup"><span data-stu-id="64506-300">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="64506-301">建立兩個 **連結服務**：</span><span class="sxs-lookup"><span data-stu-id="64506-301">Created two **linked services**:</span></span>
   1. <span data-ttu-id="64506-302">**Azure 儲存體**您保留輸入/輸出檔案 toohello 資料處理站的 Azure blob 儲存體連結服務 toolink。</span><span class="sxs-lookup"><span data-stu-id="64506-302">**Azure Storage** linked service toolink your Azure blob storage that holds input/output files toohello data factory.</span></span>
   2. <span data-ttu-id="64506-303">**Azure HDInsight**視連結的服務 toolink 隨 HDInsight Hadoop 叢集 toohello 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="64506-303">**Azure HDInsight** on-demand linked service toolink an on-demand HDInsight Hadoop cluster toohello data factory.</span></span> <span data-ttu-id="64506-304">Azure Data Factory 建立 HDInsight Hadoop 叢集在 just-in-time tooprocess 輸入的資料，並產生輸出資料。</span><span class="sxs-lookup"><span data-stu-id="64506-304">Azure Data Factory creates a HDInsight Hadoop cluster just-in-time tooprocess input data and produce output data.</span></span>
3. <span data-ttu-id="64506-305">建立兩個**資料集**，其中描述輸入和輸出 HDInsight Hive 活動 hello 管線中的資料。</span><span class="sxs-lookup"><span data-stu-id="64506-305">Created two **datasets**, which describe input and output data for HDInsight Hive activity in hello pipeline.</span></span>
4. <span data-ttu-id="64506-306">建立具有 **HDInsight Hive** 活動的**管線**。</span><span class="sxs-lookup"><span data-stu-id="64506-306">Created a **pipeline** with a **HDInsight Hive** activity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="64506-307">後續步驟</span><span class="sxs-lookup"><span data-stu-id="64506-307">Next steps</span></span>
<span data-ttu-id="64506-308">在本文中，您已經建立可在隨選 Azure HDInsight 叢集上執行 Hive 指令碼，含有轉換活動 (HDInsight 活動) 的管線。</span><span class="sxs-lookup"><span data-stu-id="64506-308">In this article, you have created a pipeline with a transformation activity (HDInsight Activity) that runs a Hive script on an on-demand Azure HDInsight cluster.</span></span> <span data-ttu-id="64506-309">如何 toouse 複製活動 toocopy 資料從 Azure Blob tooAzure SQL，請參閱的 toosee[教學課程： 將資料從 Azure Blob tooAzure SQL 複製](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。</span><span class="sxs-lookup"><span data-stu-id="64506-309">toosee how toouse a Copy Activity toocopy data from an Azure Blob tooAzure SQL, see [Tutorial: Copy data from an Azure Blob tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="64506-310">另請參閱</span><span class="sxs-lookup"><span data-stu-id="64506-310">See Also</span></span>
| <span data-ttu-id="64506-311">主題</span><span class="sxs-lookup"><span data-stu-id="64506-311">Topic</span></span> | <span data-ttu-id="64506-312">說明</span><span class="sxs-lookup"><span data-stu-id="64506-312">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="64506-313">Data Factory REST API 參考</span><span class="sxs-lookup"><span data-stu-id="64506-313">Data Factory REST API Reference</span></span>](/rest/api/datafactory/) |<span data-ttu-id="64506-314">請參閱 Data Factory Cmdlet 中的完整文件</span><span class="sxs-lookup"><span data-stu-id="64506-314">See comprehensive documentation on Data Factory cmdlets</span></span> |
| [<span data-ttu-id="64506-315">管線</span><span class="sxs-lookup"><span data-stu-id="64506-315">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="64506-316">這篇文章可協助您了解管線和 Azure Data Factory 中的活動以及 toouse 它們 tooconstruct 端對端資料驅動型工作流程或商務案例。</span><span class="sxs-lookup"><span data-stu-id="64506-316">This article helps you understand pipelines and activities in Azure Data Factory and how toouse them tooconstruct end-to-end data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="64506-317">資料集</span><span class="sxs-lookup"><span data-stu-id="64506-317">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="64506-318">本文協助您了解 Azure Data Factory 中的資料集。</span><span class="sxs-lookup"><span data-stu-id="64506-318">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="64506-319">排程和執行</span><span class="sxs-lookup"><span data-stu-id="64506-319">Scheduling and Execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="64506-320">本文說明 Azure Data Factory 應用程式模型的 hello 排程和執行的層面。</span><span class="sxs-lookup"><span data-stu-id="64506-320">This article explains hello scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="64506-321">使用監視應用程式來監視和管理管線</span><span class="sxs-lookup"><span data-stu-id="64506-321">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="64506-322">本文說明如何 toomonitor，管理和偵錯管線使用 hello 監視和管理應用程式。</span><span class="sxs-lookup"><span data-stu-id="64506-322">This article describes how toomonitor, manage, and debug pipelines using hello Monitoring & Management App.</span></span> |
