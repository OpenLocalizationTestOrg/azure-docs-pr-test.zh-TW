---
title: "aaaBuild 您第一次的 data factory (PowerShell) |Microsoft 文件"
description: "在本教學課程中，您將使用 Azure PowerShell，建立範例 Azure Data Factory 管線。"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 22ec1236-ea86-4eb7-b903-0e79a58b90c7
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 626260798b56d590577b3c4b24f7cf52873c9f80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-powershell"></a><span data-ttu-id="46212-103">教學課程：使用 Azure PowerShell 建置您的第一個 Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="46212-103">Tutorial: Build your first Azure data factory using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="46212-104">概觀和必要條件</span><span class="sxs-lookup"><span data-stu-id="46212-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="46212-105">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="46212-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="46212-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="46212-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="46212-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="46212-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="46212-108">Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="46212-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="46212-109">REST API</span><span class="sxs-lookup"><span data-stu-id="46212-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)
>
>

<span data-ttu-id="46212-110">在本文中，您使用 Azure PowerShell toocreate 第一個 Azure data factory。</span><span class="sxs-lookup"><span data-stu-id="46212-110">In this article, you use Azure PowerShell toocreate your first Azure data factory.</span></span> <span data-ttu-id="46212-111">toodo hello 教學課程中使用其他工具/Sdk，從 hello 下拉式清單選取其中一個 hello 選項。</span><span class="sxs-lookup"><span data-stu-id="46212-111">toodo hello tutorial using other tools/SDKs, select one of hello options from hello drop-down list.</span></span>

<span data-ttu-id="46212-112">在此教學課程中的 hello 管線有一個活動： **HDInsight Hive 活動**。</span><span class="sxs-lookup"><span data-stu-id="46212-112">hello pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="46212-113">此活動會在轉換輸入資料 tooproduce 輸出資料的 Azure HDInsight 叢集上執行 hive 指令碼。</span><span class="sxs-lookup"><span data-stu-id="46212-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data tooproduce output data.</span></span> <span data-ttu-id="46212-114">hello 管線是排程的 toorun，每個月之間 hello 指定開始和結束時間之後。</span><span class="sxs-lookup"><span data-stu-id="46212-114">hello pipeline is scheduled toorun once a month between hello specified start and end times.</span></span> 

> [!NOTE]
> <span data-ttu-id="46212-115">在此教學課程中的 hello 資料管線轉換輸入的資料 tooproduce 輸出資料。</span><span class="sxs-lookup"><span data-stu-id="46212-115">hello data pipeline in this tutorial transforms input data tooproduce output data.</span></span> <span data-ttu-id="46212-116">它不會複製資料來源建立資料存放區 tooa 目的地資料存放區。</span><span class="sxs-lookup"><span data-stu-id="46212-116">It does not copy data from a source data store tooa destination data store.</span></span> <span data-ttu-id="46212-117">如需如何使用 Azure Data Factory，toocopy 資料，請參閱[教學課程： 將資料從 Blob 儲存體 tooSQL 資料庫複製](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。</span><span class="sxs-lookup"><span data-stu-id="46212-117">For a tutorial on how toocopy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
> 
> <span data-ttu-id="46212-118">一個管線中可以有多個活動。</span><span class="sxs-lookup"><span data-stu-id="46212-118">A pipeline can have more than one activity.</span></span> <span data-ttu-id="46212-119">此外，您可以藉由設定 hello 輸出資料集的一個活動 hello 的輸入資料集的 hello 其他活動鏈結 （執行一個活動執行另一個之後） 的兩個活動。</span><span class="sxs-lookup"><span data-stu-id="46212-119">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="46212-120">如需詳細資訊，請參閱 [Data Factory 排程和執行](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline)。</span><span class="sxs-lookup"><span data-stu-id="46212-120">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="46212-121">必要條件</span><span class="sxs-lookup"><span data-stu-id="46212-121">Prerequisites</span></span>
* <span data-ttu-id="46212-122">閱讀[教學課程概觀](data-factory-build-your-first-pipeline.md)文件，以及完成 hello**必要條件**步驟。</span><span class="sxs-lookup"><span data-stu-id="46212-122">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete hello **prerequisite** steps.</span></span>
* <span data-ttu-id="46212-123">遵循指示[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)文章 tooinstall 最新版的 Azure PowerShell 在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="46212-123">Follow instructions in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article tooinstall latest version of Azure PowerShell on your computer.</span></span>
* <span data-ttu-id="46212-124">（選擇性）本文並未涵蓋所有 hello Data Factory cmdlet。</span><span class="sxs-lookup"><span data-stu-id="46212-124">(optional) This article does not cover all hello Data Factory cmdlets.</span></span> <span data-ttu-id="46212-125">如需 Data Factory Cmdlet 的完整文件，請參閱 [Data Factory Cmdlet 參考](/powershell/module/azurerm.datafactories) 。</span><span class="sxs-lookup"><span data-stu-id="46212-125">See [Data Factory Cmdlet Reference](/powershell/module/azurerm.datafactories) for comprehensive documentation on Data Factory cmdlets.</span></span>

## <a name="create-data-factory"></a><span data-ttu-id="46212-126">建立 Data Factory</span><span class="sxs-lookup"><span data-stu-id="46212-126">Create data factory</span></span>
<span data-ttu-id="46212-127">在此步驟中，您可以使用 Azure PowerShell toocreate 名為 Azure Data Factory **FirstDataFactoryPSH**。</span><span class="sxs-lookup"><span data-stu-id="46212-127">In this step, you use Azure PowerShell toocreate an Azure Data Factory named **FirstDataFactoryPSH**.</span></span> <span data-ttu-id="46212-128">資料處理站可以有一或多個管線。</span><span class="sxs-lookup"><span data-stu-id="46212-128">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="46212-129">其中的管線可以有一或多個活動。</span><span class="sxs-lookup"><span data-stu-id="46212-129">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="46212-130">例如，複製活動 toocopy 資料從來源 tooa 目的地資料存放區和 HDInsight Hive 活動 toorun Hive 指令碼 tootransform 輸入資料。</span><span class="sxs-lookup"><span data-stu-id="46212-130">For example, a Copy Activity toocopy data from a source tooa destination data store and a HDInsight Hive activity toorun a Hive script tootransform input data.</span></span> <span data-ttu-id="46212-131">讓我們開始在此步驟中建立 hello 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="46212-131">Let's start with creating hello data factory in this step.</span></span>

1. <span data-ttu-id="46212-132">啟動 Azure PowerShell 並執行下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="46212-132">Start Azure PowerShell and run hello following command.</span></span> <span data-ttu-id="46212-133">保持開啟 Azure PowerShell 直到本教學課程中的 hello 結尾。</span><span class="sxs-lookup"><span data-stu-id="46212-133">Keep Azure PowerShell open until hello end of this tutorial.</span></span> <span data-ttu-id="46212-134">如果您關閉並重新開啟，您需要 toorun 這些命令一次。</span><span class="sxs-lookup"><span data-stu-id="46212-134">If you close and reopen, you need toorun these commands again.</span></span>
   * <span data-ttu-id="46212-135">執行下列命令的 hello 並輸入 hello 使用者名稱和密碼，您會使用 toosign toohello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="46212-135">Run hello following command and enter hello user name and password that you use toosign in toohello Azure portal.</span></span>
    ```PowerShell
    Login-AzureRmAccount
    ```    
   * <span data-ttu-id="46212-136">執行下列命令 tooview hello 這個帳戶的所有 hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="46212-136">Run hello following command tooview all hello subscriptions for this account.</span></span>
    ```PowerShell
    Get-AzureRmSubscription 
    ```
   * <span data-ttu-id="46212-137">執行下列命令 tooselect hello 訂用帳戶，您想要使用 toowork hello。</span><span class="sxs-lookup"><span data-stu-id="46212-137">Run hello following command tooselect hello subscription that you want toowork with.</span></span> <span data-ttu-id="46212-138">此訂用帳戶應 hello 與 hello hello Azure 入口網站中使用相同。</span><span class="sxs-lookup"><span data-stu-id="46212-138">This subscription should be hello same as hello one you used in hello Azure portal.</span></span>
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```     
2. <span data-ttu-id="46212-139">建立 Azure 資源群組名稱為**ADFTutorialResourceGroup**藉由執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="46212-139">Create an Azure resource group named **ADFTutorialResourceGroup** by running hello following command:</span></span>
    
    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
    <span data-ttu-id="46212-140">本教學課程中的 hello 步驟假設您使用名為 ADFTutorialResourceGroup hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="46212-140">Some of hello steps in this tutorial assume that you use hello resource group named ADFTutorialResourceGroup.</span></span> <span data-ttu-id="46212-141">如果您使用不同的資源群組，您需要 toouse 它來取代 ADFTutorialResourceGroup 在本教學課程。</span><span class="sxs-lookup"><span data-stu-id="46212-141">If you use a different resource group, you need toouse it in place of ADFTutorialResourceGroup in this tutorial.</span></span>
3. <span data-ttu-id="46212-142">執行 hello**新增 AzureRmDataFactory**建立名為 data factory cmdlet **FirstDataFactoryPSH**。</span><span class="sxs-lookup"><span data-stu-id="46212-142">Run hello **New-AzureRmDataFactory** cmdlet that creates a data factory named **FirstDataFactoryPSH**.</span></span>

    ```PowerShell
    New-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH –Location "West US"
    ```
<span data-ttu-id="46212-143">請注意下列點 hello:</span><span class="sxs-lookup"><span data-stu-id="46212-143">Note hello following points:</span></span>

* <span data-ttu-id="46212-144">hello hello Azure Data Factory 名稱必須是全域唯一的。</span><span class="sxs-lookup"><span data-stu-id="46212-144">hello name of hello Azure Data Factory must be globally unique.</span></span> <span data-ttu-id="46212-145">如果您收到 hello 錯誤**Data factory 名稱"FirstDataFactoryPSH"不是使用**，變更 hello 名稱 (例如，yournameFirstDataFactoryPSH)。</span><span class="sxs-lookup"><span data-stu-id="46212-145">If you receive hello error **Data factory name “FirstDataFactoryPSH” is not available**, change hello name (for example, yournameFirstDataFactoryPSH).</span></span> <span data-ttu-id="46212-146">執行本教學課程中的步驟時，請使用此名稱來取代 ADFTutorialFactoryPSH。</span><span class="sxs-lookup"><span data-stu-id="46212-146">Use this name in place of ADFTutorialFactoryPSH while performing steps in this tutorial.</span></span> <span data-ttu-id="46212-147">請參閱 [Data Factory - 命名規則](data-factory-naming-rules.md) 主題，以了解 Data Factory 成品的命名規則。</span><span class="sxs-lookup"><span data-stu-id="46212-147">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
* <span data-ttu-id="46212-148">toocreate Data Factory 執行個體，您需要 toobe 參與者/系統管理員的 hello Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="46212-148">toocreate Data Factory instances, you need toobe a contributor/administrator of hello Azure subscription</span></span>
* <span data-ttu-id="46212-149">可能會註冊為未來的 hello 中的 DNS 名稱，因此會變成可公開可見 hello hello data factory 名稱。</span><span class="sxs-lookup"><span data-stu-id="46212-149">hello name of hello data factory may be registered as a DNS name in hello future and hence become publically visible.</span></span>
* <span data-ttu-id="46212-150">如果您收到 hello 錯誤:"**此訂用帳戶不是已註冊的 toouse 命名空間 Microsoft.DataFactory**」，請勿 hello 下列其中一種，然後再試一次發行：</span><span class="sxs-lookup"><span data-stu-id="46212-150">If you receive hello error: "**This subscription is not registered toouse namespace Microsoft.DataFactory**", do one of hello following and try publishing again:</span></span>

  * <span data-ttu-id="46212-151">在 Azure PowerShell 中執行下列命令 tooregister hello Data Factory 提供者的 hello:</span><span class="sxs-lookup"><span data-stu-id="46212-151">In Azure PowerShell, run hello following command tooregister hello Data Factory provider:</span></span>

    ```PowerShell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
      <span data-ttu-id="46212-152">您可以執行下列命令 tooconfirm hello Data Factory 提供者註冊該 hello:</span><span class="sxs-lookup"><span data-stu-id="46212-152">You can run hello following command tooconfirm that hello Data Factory provider is registered:</span></span>

    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="46212-153">登入使用 hello hello 到 Azure 訂用帳戶[Azure 入口網站](https://portal.azure.com)並瀏覽 tooa Data Factory 刀鋒視窗 （或） 在 hello Azure 入口網站中建立 data factory。</span><span class="sxs-lookup"><span data-stu-id="46212-153">Login using hello Azure subscription into hello [Azure portal](https://portal.azure.com) and navigate tooa Data Factory blade (or) create a data factory in hello Azure portal.</span></span> <span data-ttu-id="46212-154">這個動作會自動註冊 hello 您的提供者。</span><span class="sxs-lookup"><span data-stu-id="46212-154">This action automatically registers hello provider for you.</span></span>

<span data-ttu-id="46212-155">之前建立管線，您必須 toocreate 幾個 Data Factory 實體第一次。</span><span class="sxs-lookup"><span data-stu-id="46212-155">Before creating a pipeline, you need toocreate a few Data Factory entities first.</span></span> <span data-ttu-id="46212-156">您第一次建立連結的服務 toolink 資料存放區/計算 tooyour 資料儲存、 定義輸入和輸出連結的資料儲存區中的資料集 toorepresent 輸入/輸出資料，然後以該活動會使用這些資料集來建立 hello 管線。</span><span class="sxs-lookup"><span data-stu-id="46212-156">You first create linked services toolink data stores/computes tooyour data store, define input and output datasets toorepresent input/output data in linked data stores, and then create hello pipeline with an activity that uses these datasets.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="46212-157">建立連結的服務</span><span class="sxs-lookup"><span data-stu-id="46212-157">Create linked services</span></span>
<span data-ttu-id="46212-158">在此步驟中，您可以連結您的 Azure 儲存體帳戶和隨 Azure HDInsight 叢集 tooyour 資料處理站。</span><span class="sxs-lookup"><span data-stu-id="46212-158">In this step, you link your Azure Storage account and an on-demand Azure HDInsight cluster tooyour data factory.</span></span> <span data-ttu-id="46212-159">hello 保存 hello hello 管線，在此範例中的輸入和輸出資料的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="46212-159">hello Azure Storage account holds hello input and output data for hello pipeline in this sample.</span></span> <span data-ttu-id="46212-160">hello HDInsight 連結服務是使用的 toorun hello 管線，在此範例中的 hello 活動中指定的 Hive 指令碼。</span><span class="sxs-lookup"><span data-stu-id="46212-160">hello HDInsight linked service is used toorun a Hive script specified in hello activity of hello pipeline in this sample.</span></span> <span data-ttu-id="46212-161">識別哪些資料存放區/計算服務會以您的案例，並將這些服務 toohello 資料 factory 連結藉由建立連結的服務。</span><span class="sxs-lookup"><span data-stu-id="46212-161">Identify what data store/compute services are used in your scenario and link those services toohello data factory by creating linked services.</span></span>

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="46212-162">建立 Azure 儲存體連結服務</span><span class="sxs-lookup"><span data-stu-id="46212-162">Create Azure Storage linked service</span></span>
<span data-ttu-id="46212-163">在此步驟中，您必須連結您的 Azure 儲存體帳戶 tooyour data factory。</span><span class="sxs-lookup"><span data-stu-id="46212-163">In this step, you link your Azure Storage account tooyour data factory.</span></span> <span data-ttu-id="46212-164">使用 hello toostore 輸入/輸出資料與 hello HQL 指令碼檔案的相同 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="46212-164">You use hello same Azure Storage account toostore input/output data and hello HQL script file.</span></span>

1. <span data-ttu-id="46212-165">建立名為 hello 遵循 StorageLinkedService.json hello C:\ADFGetStarted 資料夾中的 JSON 檔案內容。</span><span class="sxs-lookup"><span data-stu-id="46212-165">Create a JSON file named StorageLinkedService.json in hello C:\ADFGetStarted folder with hello following content.</span></span> <span data-ttu-id="46212-166">如果不存在，請建立 hello 資料夾 ADFGetStarted。</span><span class="sxs-lookup"><span data-stu-id="46212-166">Create hello folder ADFGetStarted if it does not already exist.</span></span>

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
    <span data-ttu-id="46212-167">取代**帳戶名稱**hello Azure 儲存體帳戶名稱和**帳戶金鑰**hello 的 hello Azure 儲存體帳戶的存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="46212-167">Replace **account name** with hello name of your Azure storage account and **account key** with hello access key of hello Azure storage account.</span></span> <span data-ttu-id="46212-168">toolearn 如何 tooget 您的儲存體存取金鑰，請參閱有關如何 tooview、 複製和重新產生儲存體存取金鑰中的 hello 資訊[管理您的儲存體帳戶](../storage/common/storage-create-storage-account.md#manage-your-storage-account)。</span><span class="sxs-lookup"><span data-stu-id="46212-168">toolearn how tooget your storage access key, see hello information about how tooview, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
2. <span data-ttu-id="46212-169">在 Azure PowerShell，切換 toohello ADFGetStarted 資料夾。</span><span class="sxs-lookup"><span data-stu-id="46212-169">In Azure PowerShell, switch toohello ADFGetStarted folder.</span></span>
3. <span data-ttu-id="46212-170">您可以使用 hello**新增 AzureRmDataFactoryLinkedService** cmdlet 會建立連結的服務。</span><span class="sxs-lookup"><span data-stu-id="46212-170">You can use hello **New-AzureRmDataFactoryLinkedService** cmdlet that creates a linked service.</span></span> <span data-ttu-id="46212-171">這個指令程式和您在本教學課程中使用其他 Data Factory cmdlet 需要您 toopass 值 hello *ResourceGroupName*和*DataFactoryName*參數。</span><span class="sxs-lookup"><span data-stu-id="46212-171">This cmdlet and other Data Factory cmdlets you use in this tutorial requires you toopass values for hello *ResourceGroupName* and *DataFactoryName* parameters.</span></span> <span data-ttu-id="46212-172">或者，您可以使用**Get AzureRmDataFactory** tooget **DataFactory**物件，並傳遞 hello 物件而不需要輸入*ResourceGroupName*和*DataFactoryName*每次您執行 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="46212-172">Alternatively, you can use **Get-AzureRmDataFactory** tooget a **DataFactory** object and pass hello object without typing *ResourceGroupName* and *DataFactoryName* each time you run a cmdlet.</span></span> <span data-ttu-id="46212-173">Hello 執行的下列命令的 hello tooassign hello 輸出**Get AzureRmDataFactory** cmdlet tooa **$df**變數。</span><span class="sxs-lookup"><span data-stu-id="46212-173">Run hello following command tooassign hello output of hello **Get-AzureRmDataFactory** cmdlet tooa **$df** variable.</span></span>

    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH
    ```
4. <span data-ttu-id="46212-174">現在，執行 hello**新增 AzureRmDataFactoryLinkedService**建立 hello cmdlet 連結**StorageLinkedService**服務。</span><span class="sxs-lookup"><span data-stu-id="46212-174">Now, run hello **New-AzureRmDataFactoryLinkedService** cmdlet that creates hello linked **StorageLinkedService** service.</span></span>

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\StorageLinkedService.json
    ```
    <span data-ttu-id="46212-175">如果您還沒有執行 hello **Get AzureRmDataFactory**指令程式，並指派的 hello 輸出 toohello **$df**變數時，您就必須 hello toospecify 值*ResourceGroupName*和*DataFactoryName*參數，如下所示。</span><span class="sxs-lookup"><span data-stu-id="46212-175">If you hadn't run hello **Get-AzureRmDataFactory** cmdlet and assigned hello output toohello **$df** variable, you would have toospecify values for hello *ResourceGroupName* and *DataFactoryName* parameters as follows.</span></span>

    ```PowerShell
    New-AzureRmDataFactoryLinkedService -ResourceGroupName ADFTutorialResourceGroup -DataFactoryName FirstDataFactoryPSH -File .\StorageLinkedService.json
    ```
    <span data-ttu-id="46212-176">如果您關閉 Azure PowerShell 中的 hello 教學課程中的 hello 中間時，您會有 toorun hello **Get AzureRmDataFactory** cmdlet 啟動 Azure PowerShell toocomplete hello 教學課程的下一次。</span><span class="sxs-lookup"><span data-stu-id="46212-176">If you close Azure PowerShell in hello middle of hello tutorial, you have toorun hello **Get-AzureRmDataFactory** cmdlet next time you start Azure PowerShell toocomplete hello tutorial.</span></span>

### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="46212-177">建立 Azure HDInsight 連結服務</span><span class="sxs-lookup"><span data-stu-id="46212-177">Create Azure HDInsight linked service</span></span>
<span data-ttu-id="46212-178">在此步驟中，您可以連結的隨選 HDInsight 叢集 tooyour 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="46212-178">In this step, you link an on-demand HDInsight cluster tooyour data factory.</span></span> <span data-ttu-id="46212-179">自動在執行階段建立及刪除它為了處理和閒置 hello 指定的時間量之後 hello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="46212-179">hello HDInsight cluster is automatically created at runtime and deleted after it is done processing and idle for hello specified amount of time.</span></span> <span data-ttu-id="46212-180">您可以使用自己的 HDInsight 叢集，不必使用隨選的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="46212-180">You could use your own HDInsight cluster instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="46212-181">請參閱 [計算連結服務](data-factory-compute-linked-services.md) 以取得詳細資料。</span><span class="sxs-lookup"><span data-stu-id="46212-181">See [Compute Linked Services](data-factory-compute-linked-services.md) for details.</span></span>

1. <span data-ttu-id="46212-182">建立名為的 JSON 檔案**HDInsightOnDemandLinkedService**在 hello.json **C:\ADFGetStarted**以 hello 內容之後的資料夾。</span><span class="sxs-lookup"><span data-stu-id="46212-182">Create a JSON file named **HDInsightOnDemandLinkedService**.json in hello **C:\ADFGetStarted** folder with hello following content.</span></span>

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
                "linkedServiceName": "StorageLinkedService"
            }
        }
    }
    ```
    <span data-ttu-id="46212-183">hello 下表提供 hello hello 程式碼片段中使用的 JSON 屬性的說明：</span><span class="sxs-lookup"><span data-stu-id="46212-183">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

   | <span data-ttu-id="46212-184">屬性</span><span class="sxs-lookup"><span data-stu-id="46212-184">Property</span></span> | <span data-ttu-id="46212-185">說明</span><span class="sxs-lookup"><span data-stu-id="46212-185">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="46212-186">ClusterSize</span><span class="sxs-lookup"><span data-stu-id="46212-186">ClusterSize</span></span> |<span data-ttu-id="46212-187">指定 hello hello HDInsight 叢集大小。</span><span class="sxs-lookup"><span data-stu-id="46212-187">Specifies hello size of hello HDInsight cluster.</span></span> |
   | <span data-ttu-id="46212-188">TimeToLive</span><span class="sxs-lookup"><span data-stu-id="46212-188">TimeToLive</span></span> |<span data-ttu-id="46212-189">於刪除之前，請指定 hello HDInsight 叢集，該 hello 閒置時間。</span><span class="sxs-lookup"><span data-stu-id="46212-189">Specifies that hello idle time for hello HDInsight cluster, before it is deleted.</span></span> |
   | <span data-ttu-id="46212-190">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="46212-190">linkedServiceName</span></span> |<span data-ttu-id="46212-191">指定 hello 是使用的 toostore hello 記錄 HDInsight 所產生的儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="46212-191">Specifies hello storage account that is used toostore hello logs that are generated by HDInsight</span></span> |

    <span data-ttu-id="46212-192">請注意下列點 hello:</span><span class="sxs-lookup"><span data-stu-id="46212-192">Note hello following points:</span></span>

   * <span data-ttu-id="46212-193">hello Data Factory 建立**linux**以 hello JSON 為您的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="46212-193">hello Data Factory creates a **Linux-based** HDInsight cluster for you with hello JSON.</span></span> <span data-ttu-id="46212-194">如需詳細資訊，請參閱 [HDInsight 隨選連結服務](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) 。</span><span class="sxs-lookup"><span data-stu-id="46212-194">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
   * <span data-ttu-id="46212-195">您可以使用 **自己的 HDInsight 叢集** ，不必使用隨選的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="46212-195">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="46212-196">如需詳細資訊，請參閱 [HDInsight 連結服務](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) 。</span><span class="sxs-lookup"><span data-stu-id="46212-196">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span></span>
   * <span data-ttu-id="46212-197">hello HDInsight 叢集建立**預設容器**hello hello JSON 中指定的 blob 儲存體中 (**linkedServiceName**)。</span><span class="sxs-lookup"><span data-stu-id="46212-197">hello HDInsight cluster creates a **default container** in hello blob storage you specified in hello JSON (**linkedServiceName**).</span></span> <span data-ttu-id="46212-198">HDInsight 刪除 hello 叢集時，不會刪除此容器。</span><span class="sxs-lookup"><span data-stu-id="46212-198">HDInsight does not delete this container when hello cluster is deleted.</span></span> <span data-ttu-id="46212-199">這是設計的行為。</span><span class="sxs-lookup"><span data-stu-id="46212-199">This behavior is by design.</span></span> <span data-ttu-id="46212-200">在使用 HDInsight 隨選連結服務時，除非有現有的即時叢集 (**timeToLive**)，否則每次處理配量時，就會建立 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="46212-200">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (**timeToLive**).</span></span> <span data-ttu-id="46212-201">hello 處理完成時，會自動刪除 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="46212-201">hello cluster is automatically deleted when hello processing is done.</span></span>

       <span data-ttu-id="46212-202">隨著處理的配量越來越多，您會在 Azure Blob 儲存體中看到許多容器。</span><span class="sxs-lookup"><span data-stu-id="46212-202">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="46212-203">如果您不需要它們進行疑難排解的 hello 工作，您可能會想 toodelete 它們 tooreduce hello 儲存體成本。</span><span class="sxs-lookup"><span data-stu-id="46212-203">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="46212-204">這些容器的 hello 名稱遵循模式: 「 adf**yourdatafactoryname**-**linkedservicename**-datetimestamp"。</span><span class="sxs-lookup"><span data-stu-id="46212-204">hello names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="46212-205">使用工具，例如[Microsoft 儲存體總管](http://storageexplorer.com/)toodelete 容器，在您的 Azure blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="46212-205">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) toodelete containers in your Azure blob storage.</span></span>

     <span data-ttu-id="46212-206">如需詳細資訊，請參閱 [HDInsight 隨選連結服務](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) 。</span><span class="sxs-lookup"><span data-stu-id="46212-206">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
2. <span data-ttu-id="46212-207">執行 hello**新增 AzureRmDataFactoryLinkedService**建立 hello cmdlet 的連結稱為 HDInsightOnDemandLinkedService 的服務。</span><span class="sxs-lookup"><span data-stu-id="46212-207">Run hello **New-AzureRmDataFactoryLinkedService** cmdlet that creates hello linked service called HDInsightOnDemandLinkedService.</span></span>
    
    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\HDInsightOnDemandLinkedService.json
    ```

## <a name="create-datasets"></a><span data-ttu-id="46212-208">建立資料集</span><span class="sxs-lookup"><span data-stu-id="46212-208">Create datasets</span></span>
<span data-ttu-id="46212-209">在此步驟中，您可以建立資料集 toorepresent hello 輸入和輸出 Hive 處理的資料。</span><span class="sxs-lookup"><span data-stu-id="46212-209">In this step, you create datasets toorepresent hello input and output data for Hive processing.</span></span> <span data-ttu-id="46212-210">這些資料集，請參閱 toohello **StorageLinkedService**稍早在本教學課程中，您已建立。</span><span class="sxs-lookup"><span data-stu-id="46212-210">These datasets refer toohello **StorageLinkedService** you have created earlier in this tutorial.</span></span> <span data-ttu-id="46212-211">hello 連結的服務點 tooan Azure 儲存體帳戶和資料集指定保留輸入 hello 儲存體中的容器、 資料夾、 檔案名稱和輸出資料。</span><span class="sxs-lookup"><span data-stu-id="46212-211">hello linked service points tooan Azure Storage account and datasets specify container, folder, file name in hello storage that holds input and output data.</span></span>

### <a name="create-input-dataset"></a><span data-ttu-id="46212-212">建立輸入資料集</span><span class="sxs-lookup"><span data-stu-id="46212-212">Create input dataset</span></span>
1. <span data-ttu-id="46212-213">建立名為的 JSON 檔案**InputTable.json**在 hello **C:\ADFGetStarted**資料夾以 hello 下列內容：</span><span class="sxs-lookup"><span data-stu-id="46212-213">Create a JSON file named **InputTable.json** in hello **C:\ADFGetStarted** folder with hello following content:</span></span>

    ```json
    {
        "name": "AzureBlobInput",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "StorageLinkedService",
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
    <span data-ttu-id="46212-214">hello JSON 定義名為資料集**AzureBlobInput**，代表 hello 管線中活動的輸入的資料。</span><span class="sxs-lookup"><span data-stu-id="46212-214">hello JSON defines a dataset named **AzureBlobInput**, which represents input data for an activity in hello pipeline.</span></span> <span data-ttu-id="46212-215">此外，它會指定 hello 輸入的資料位於呼叫 hello blob 容器**adfgetstarted**和 hello 資料夾稱為**inputdata**。</span><span class="sxs-lookup"><span data-stu-id="46212-215">In addition, it specifies that hello input data is located in hello blob container called **adfgetstarted** and hello folder called **inputdata**.</span></span>

    <span data-ttu-id="46212-216">hello 下表提供 hello hello 程式碼片段中使用的 JSON 屬性的說明：</span><span class="sxs-lookup"><span data-stu-id="46212-216">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

   | <span data-ttu-id="46212-217">屬性</span><span class="sxs-lookup"><span data-stu-id="46212-217">Property</span></span> | <span data-ttu-id="46212-218">說明</span><span class="sxs-lookup"><span data-stu-id="46212-218">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="46212-219">類型</span><span class="sxs-lookup"><span data-stu-id="46212-219">type</span></span> |<span data-ttu-id="46212-220">hello 類型屬性是設定 tooAzureBlob，因為資料常駐於 Azure blob 儲存體中。</span><span class="sxs-lookup"><span data-stu-id="46212-220">hello type property is set tooAzureBlob because data resides in Azure blob storage.</span></span> |
   | <span data-ttu-id="46212-221">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="46212-221">linkedServiceName</span></span> |<span data-ttu-id="46212-222">是指您稍早建立的 StorageLinkedService toohello。</span><span class="sxs-lookup"><span data-stu-id="46212-222">refers toohello StorageLinkedService you created earlier.</span></span> |
   | <span data-ttu-id="46212-223">fileName</span><span class="sxs-lookup"><span data-stu-id="46212-223">fileName</span></span> |<span data-ttu-id="46212-224">這是選用屬性。</span><span class="sxs-lookup"><span data-stu-id="46212-224">This property is optional.</span></span> <span data-ttu-id="46212-225">如果您省略這個屬性時，會挑出 hello folderPath 中的所有 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="46212-225">If you omit this property, all hello files from hello folderPath are picked.</span></span> <span data-ttu-id="46212-226">在此情況下，只有 hello input.log 會進行處理。</span><span class="sxs-lookup"><span data-stu-id="46212-226">In this case, only hello input.log is processed.</span></span> |
   | <span data-ttu-id="46212-227">類型</span><span class="sxs-lookup"><span data-stu-id="46212-227">type</span></span> |<span data-ttu-id="46212-228">hello 記錄檔是以文字格式，因此我們使用 TextFormat。</span><span class="sxs-lookup"><span data-stu-id="46212-228">hello log files are in text format, so we use TextFormat.</span></span> |
   | <span data-ttu-id="46212-229">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="46212-229">columnDelimiter</span></span> |<span data-ttu-id="46212-230">hello 記錄檔中的資料行是以 hello 逗號字元 （，） 分隔。</span><span class="sxs-lookup"><span data-stu-id="46212-230">columns in hello log files are delimited by hello comma character (,).</span></span> |
   | <span data-ttu-id="46212-231">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="46212-231">frequency/interval</span></span> |<span data-ttu-id="46212-232">設定 tooMonth 頻率和間隔為 1，這表示的 hello 輸入配量可使用每個月。</span><span class="sxs-lookup"><span data-stu-id="46212-232">frequency set tooMonth and interval is 1, which means that hello input slices are available monthly.</span></span> |
   | <span data-ttu-id="46212-233">external</span><span class="sxs-lookup"><span data-stu-id="46212-233">external</span></span> |<span data-ttu-id="46212-234">設定此屬性是 tootrue hello 輸入的資料不會產生 hello Data Factory 服務。</span><span class="sxs-lookup"><span data-stu-id="46212-234">this property is set tootrue if hello input data is not generated by hello Data Factory service.</span></span> |
2. <span data-ttu-id="46212-235">執行下列命令，在 Azure PowerShell toocreate hello Data Factory 資料集中的 hello:</span><span class="sxs-lookup"><span data-stu-id="46212-235">Run hello following command in Azure PowerShell toocreate hello Data Factory dataset:</span></span>

    ```PowerShell
    New-AzureRmDataFactoryDataset $df -File .\InputTable.json
    ```

### <a name="create-output-dataset"></a><span data-ttu-id="46212-236">建立輸出資料集</span><span class="sxs-lookup"><span data-stu-id="46212-236">Create output dataset</span></span>
<span data-ttu-id="46212-237">現在，您可以建立 hello 輸出資料集 toorepresent hello 輸出資料儲存在 hello Azure Blob 儲存體中。</span><span class="sxs-lookup"><span data-stu-id="46212-237">Now, you create hello output dataset toorepresent hello output data stored in hello Azure Blob storage.</span></span>

1. <span data-ttu-id="46212-238">建立名為的 JSON 檔案**OutputTable.json**在 hello **C:\ADFGetStarted**資料夾以 hello 下列內容：</span><span class="sxs-lookup"><span data-stu-id="46212-238">Create a JSON file named **OutputTable.json** in hello **C:\ADFGetStarted** folder with hello following content:</span></span>

    ```json
    {
      "name": "AzureBlobOutput",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
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
    <span data-ttu-id="46212-239">hello JSON 定義名為資料集**AzureBlobOutput**，代表 hello 管線中活動的輸出資料。</span><span class="sxs-lookup"><span data-stu-id="46212-239">hello JSON defines a dataset named **AzureBlobOutput**, which represents output data for an activity in hello pipeline.</span></span> <span data-ttu-id="46212-240">此外，它會指定 hello 結果會儲存在稱為 hello blob 容器**adfgetstarted**和 hello 資料夾稱為**partitioneddata**。</span><span class="sxs-lookup"><span data-stu-id="46212-240">In addition, it specifies that hello results are stored in hello blob container called **adfgetstarted** and hello folder called **partitioneddata**.</span></span> <span data-ttu-id="46212-241">hello**可用性**區段會指定該 hello 輸出資料集產生每月為基礎。</span><span class="sxs-lookup"><span data-stu-id="46212-241">hello **availability** section specifies that hello output dataset is produced on a monthly basis.</span></span>
2. <span data-ttu-id="46212-242">執行下列命令，在 Azure PowerShell toocreate hello Data Factory 資料集中的 hello:</span><span class="sxs-lookup"><span data-stu-id="46212-242">Run hello following command in Azure PowerShell toocreate hello Data Factory dataset:</span></span>

    ```PowerShell
    New-AzureRmDataFactoryDataset $df -File .\OutputTable.json
    ```

## <a name="create-pipeline"></a><span data-ttu-id="46212-243">建立管線</span><span class="sxs-lookup"><span data-stu-id="46212-243">Create pipeline</span></span>
<span data-ttu-id="46212-244">在此步驟中，您會建立第一個具有 **HDInsightHive** 活動的管線。</span><span class="sxs-lookup"><span data-stu-id="46212-244">In this step, you create your first pipeline with a **HDInsightHive** activity.</span></span> <span data-ttu-id="46212-245">輸入的配量可每月 (頻率： Month、 interval: 1)、 每月產生輸出配量和 hello hello 活動的排程器屬性也設定 toomonthly。</span><span class="sxs-lookup"><span data-stu-id="46212-245">Input slice is available monthly (frequency: Month, interval: 1), output slice is produced monthly, and hello scheduler property for hello activity is also set toomonthly.</span></span> <span data-ttu-id="46212-246">hello 輸出資料集和 hello 活動排程器的 hello 設定必須相符。</span><span class="sxs-lookup"><span data-stu-id="46212-246">hello settings for hello output dataset and hello activity scheduler must match.</span></span> <span data-ttu-id="46212-247">目前，輸出資料集是哪些磁碟機 hello 排程，因此您必須建立輸出資料集，即使 hello 活動不會產生任何輸出。</span><span class="sxs-lookup"><span data-stu-id="46212-247">Currently, output dataset is what drives hello schedule, so you must create an output dataset even if hello activity does not produce any output.</span></span> <span data-ttu-id="46212-248">如果 hello 活動不接受任何輸入，您可以略過建立 hello 輸入資料集。</span><span class="sxs-lookup"><span data-stu-id="46212-248">If hello activity doesn't take any input, you can skip creating hello input dataset.</span></span> <span data-ttu-id="46212-249">hello 下列 JSON 中使用的 hello 內容會說明在 hello 本節結尾處。</span><span class="sxs-lookup"><span data-stu-id="46212-249">hello properties used in hello following JSON are explained at hello end of this section.</span></span>

1. <span data-ttu-id="46212-250">建立名為 hello 遵循 MyFirstPipelinePSH.json hello C:\ADFGetStarted 資料夾中的 JSON 檔案內容：</span><span class="sxs-lookup"><span data-stu-id="46212-250">Create a JSON file named MyFirstPipelinePSH.json in hello C:\ADFGetStarted folder with hello following content:</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="46212-251">取代**storageaccountname** hello hello JSON 中的儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="46212-251">Replace **storageaccountname** with hello name of your storage account in hello JSON.</span></span>
   >
   >

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
                        "scriptLinkedService": "StorageLinkedService",
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
    <span data-ttu-id="46212-252">在 hello JSON 片段中，您要建立管線在 HDInsight 叢集使用 Hive tooprocess 資料的活動所組成。</span><span class="sxs-lookup"><span data-stu-id="46212-252">In hello JSON snippet, you are creating a pipeline that consists of a single activity that uses Hive tooprocess Data on an HDInsight cluster.</span></span>

    <span data-ttu-id="46212-253">hello Hive 指令碼檔案， **partitionweblogs.hql**，儲存在 hello Azure 儲存體帳戶 (由 hello scriptLinkedService，稱為**StorageLinkedService**)，然後在**指令碼** hello 容器中的資料夾**adfgetstarted**。</span><span class="sxs-lookup"><span data-stu-id="46212-253">hello Hive script file, **partitionweblogs.hql**, is stored in hello Azure storage account (specified by hello scriptLinkedService, called **StorageLinkedService**), and in **script** folder in hello container **adfgetstarted**.</span></span>

    <span data-ttu-id="46212-254">hello**定義**區段是使用的 toospecify hello 執行階段設定會當做 Hive 組態值傳遞給 toohello hive 指令碼 (例如 ${hiveconf: inputtable}，{hiveconf:partitionedtable} $)。</span><span class="sxs-lookup"><span data-stu-id="46212-254">hello **defines** section is used toospecify hello runtime settings that be passed toohello hive script as Hive configuration values (e.g ${hiveconf:inputtable}, ${hiveconf:partitionedtable}).</span></span>

    <span data-ttu-id="46212-255">hello**啟動**和**結束**hello 管線屬性指定 hello 之 hello 管線的作用期間。</span><span class="sxs-lookup"><span data-stu-id="46212-255">hello **start** and **end** properties of hello pipeline specifies hello active period of hello pipeline.</span></span>

    <span data-ttu-id="46212-256">在 hello 活動 JSON 中，您指定該 hello Hive 指令碼在上執行指定 hello hello 計算**linkedServiceName** – **HDInsightOnDemandLinkedService**。</span><span class="sxs-lookup"><span data-stu-id="46212-256">In hello activity JSON, you specify that hello Hive script runs on hello compute specified by hello **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="46212-257">請參閱中的"管線 JSON"[管線和 Azure Data Factory 中的活動](data-factory-create-pipelines.md)hello 範例中使用的 JSON 屬性的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="46212-257">See "Pipeline JSON" in [Pipelines and activities in Azure Data Factory](data-factory-create-pipelines.md) for details about JSON properties that are used in hello example.</span></span>

2. <span data-ttu-id="46212-258">確認您看到 hello **input.log**檔案在 hello **adfgetstarted/inputdata** hello Azure blob 儲存體，並執行下列命令 toodeploy hello 管線的 hello 中的資料夾。</span><span class="sxs-lookup"><span data-stu-id="46212-258">Confirm that you see hello **input.log** file in hello **adfgetstarted/inputdata** folder in hello Azure blob storage, and run hello following command toodeploy hello pipeline.</span></span> <span data-ttu-id="46212-259">因為 hello**啟動**和**結束**次數設定在過去的 hello 和**isPaused**是集 toofalse，hello 管線 （hello 管線中的活動） 執行您部署之後，立即。</span><span class="sxs-lookup"><span data-stu-id="46212-259">Since hello **start** and **end** times are set in hello past and **isPaused** is set toofalse, hello pipeline (activity in hello pipeline) runs immediately after you deploy.</span></span>

    ```PowerShell
    New-AzureRmDataFactoryPipeline $df -File .\MyFirstPipelinePSH.json
    ```
3. <span data-ttu-id="46212-260">恭喜，您已經成功使用 Azure PowerShell 建立您的第一個管線！</span><span class="sxs-lookup"><span data-stu-id="46212-260">Congratulations, you have successfully created your first pipeline using Azure PowerShell!</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="46212-261">監視管線</span><span class="sxs-lookup"><span data-stu-id="46212-261">Monitor pipeline</span></span>
<span data-ttu-id="46212-262">在此步驟中，您使用 Azure PowerShell toomonitor Azure data factory 中運作。</span><span class="sxs-lookup"><span data-stu-id="46212-262">In this step, you use Azure PowerShell toomonitor what’s going on in an Azure data factory.</span></span>

1. <span data-ttu-id="46212-263">執行**Get AzureRmDataFactory**並指派 hello 輸出 tooa **$df**變數。</span><span class="sxs-lookup"><span data-stu-id="46212-263">Run **Get-AzureRmDataFactory** and assign hello output tooa **$df** variable.</span></span>

    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH
    ```
2. <span data-ttu-id="46212-264">執行**Get AzureRmDataFactorySlice** tooget 詳細所有配量的 hello **EmpSQLTable**，這是 hello 輸出資料表的 hello 管線。</span><span class="sxs-lookup"><span data-stu-id="46212-264">Run **Get-AzureRmDataFactorySlice** tooget details about all slices of hello **EmpSQLTable**, which is hello output table of hello pipeline.</span></span>

    ```PowerShell
    Get-AzureRmDataFactorySlice $df -DatasetName AzureBlobOutput -StartDateTime 2017-07-01
    ```
    <span data-ttu-id="46212-265">請注意該 hello StartDateTime 您在此處指定為的 hello 相同開始 hello 管線 JSON 中指定的時間。</span><span class="sxs-lookup"><span data-stu-id="46212-265">Notice that hello StartDateTime you specify here is hello same start time specified in hello pipeline JSON.</span></span> <span data-ttu-id="46212-266">以下是 hello 範例輸出：</span><span class="sxs-lookup"><span data-stu-id="46212-266">Here is hello sample output:</span></span>

    ```PowerShell
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : FirstDataFactoryPSH
    DatasetName       : AzureBlobOutput
    Start             : 7/1/2017 12:00:00 AM
    End               : 7/2/2017 12:00:00 AM
    RetryCount        : 0
    State             : InProgress
    SubState          :
    LatencyStatus     :
    LongRetryCount    : 0
    ```
3. <span data-ttu-id="46212-267">執行**Get AzureRmDataFactoryRun** tooget hello 詳細資料的活動執行的特定配量。</span><span class="sxs-lookup"><span data-stu-id="46212-267">Run **Get-AzureRmDataFactoryRun** tooget hello details of activity runs for a specific slice.</span></span>

    ```PowerShell
    Get-AzureRmDataFactoryRun $df -DatasetName AzureBlobOutput -StartDateTime 2017-07-01
    ```

    <span data-ttu-id="46212-268">以下是 hello 範例輸出：</span><span class="sxs-lookup"><span data-stu-id="46212-268">Here is hello sample output:</span></span> 

    ```PowerShell
    Id                  : 0f6334f2-d56c-4d48-b427-d4f0fb4ef883_635268096000000000_635292288000000000_AzureBlobOutput
    ResourceGroupName   : ADFTutorialResourceGroup
    DataFactoryName     : FirstDataFactoryPSH
    DatasetName         : AzureBlobOutput
    ProcessingStartTime : 12/18/2015 4:50:33 AM
    ProcessingEndTime   : 12/31/9999 11:59:59 PM
    PercentComplete     : 0
    DataSliceStart      : 7/1/2017 12:00:00 AM
    DataSliceEnd        : 7/2/2017 12:00:00 AM
    Status              : AllocatingResources
    Timestamp           : 12/18/2015 4:50:33 AM
    RetryAttempt        : 0
    Properties          : {}
    ErrorMessage        :
    ActivityName        : RunSampleHiveActivity
    PipelineName        : MyFirstPipeline
    Type                : Script
    ```
    <span data-ttu-id="46212-269">您可以繼續執行這個指令程式直至您看見 hello 配量中的**準備**狀態或**失敗**狀態。</span><span class="sxs-lookup"><span data-stu-id="46212-269">You can keep running this cmdlet until you see hello slice in **Ready** state or **Failed** state.</span></span> <span data-ttu-id="46212-270">當 hello 配量處於就緒狀態時，請檢查 hello **partitioneddata**資料夾中 hello **adfgetstarted** hello 您 blob 儲存體容器中的輸出資料。</span><span class="sxs-lookup"><span data-stu-id="46212-270">When hello slice is in Ready state, check hello **partitioneddata** folder in hello **adfgetstarted** container in your blob storage for hello output data.</span></span>  <span data-ttu-id="46212-271">建立隨選 HDInsight 叢集通常需要一些時間。</span><span class="sxs-lookup"><span data-stu-id="46212-271">Creation of an on-demand HDInsight cluster usually takes some time.</span></span>

    ![輸出資料](./media/data-factory-build-your-first-pipeline-using-powershell/three-ouptut-files.png)

> [!IMPORTANT]
> <span data-ttu-id="46212-273">建立隨選 HDInsight 叢集通常需要一些時間 (大約 20 分鐘)。</span><span class="sxs-lookup"><span data-stu-id="46212-273">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="46212-274">因此，預期 hello 管線 tootake**大約 30 分鐘**tooprocess hello 配量。</span><span class="sxs-lookup"><span data-stu-id="46212-274">Therefore, expect hello pipeline tootake **approximately 30 minutes** tooprocess hello slice.</span></span>
>
> <span data-ttu-id="46212-275">已成功處理 hello 配量時，取得刪除 hello 輸入的檔。</span><span class="sxs-lookup"><span data-stu-id="46212-275">hello input file gets deleted when hello slice is processed successfully.</span></span> <span data-ttu-id="46212-276">因此，如果您想 toorerun hello 配量，或不要 hello 教學課程中上, 傳 hello hello adfgetstarted 容器的輸入的檔 (input.log) toohello inputdata 資料夾。</span><span class="sxs-lookup"><span data-stu-id="46212-276">Therefore, if you want toorerun hello slice or do hello tutorial again, upload hello input file (input.log) toohello inputdata folder of hello adfgetstarted container.</span></span>
>
>

## <a name="summary"></a><span data-ttu-id="46212-277">摘要</span><span class="sxs-lookup"><span data-stu-id="46212-277">Summary</span></span>
<span data-ttu-id="46212-278">在本教學課程中，您可以建立 Azure data factory tooprocess 資料在 HDInsight hadoop 叢集上執行 Hive 指令碼。</span><span class="sxs-lookup"><span data-stu-id="46212-278">In this tutorial, you created an Azure data factory tooprocess data by running Hive script on a HDInsight hadoop cluster.</span></span> <span data-ttu-id="46212-279">您使用 hello Data Factory 編輯器在 hello Azure 入口網站 toodo hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="46212-279">You used hello Data Factory Editor in hello Azure portal toodo hello following steps:</span></span>

1. <span data-ttu-id="46212-280">建立 Azure **Data Factory**。</span><span class="sxs-lookup"><span data-stu-id="46212-280">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="46212-281">建立兩個 **連結服務**：</span><span class="sxs-lookup"><span data-stu-id="46212-281">Created two **linked services**:</span></span>
   1. <span data-ttu-id="46212-282">**Azure 儲存體**您保留輸入/輸出檔案 toohello 資料處理站的 Azure blob 儲存體連結服務 toolink。</span><span class="sxs-lookup"><span data-stu-id="46212-282">**Azure Storage** linked service toolink your Azure blob storage that holds input/output files toohello data factory.</span></span>
   2. <span data-ttu-id="46212-283">**Azure HDInsight**視連結的服務 toolink 隨 HDInsight Hadoop 叢集 toohello 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="46212-283">**Azure HDInsight** on-demand linked service toolink an on-demand HDInsight Hadoop cluster toohello data factory.</span></span> <span data-ttu-id="46212-284">Azure Data Factory 建立 HDInsight Hadoop 叢集在 just-in-time tooprocess 輸入的資料，並產生輸出資料。</span><span class="sxs-lookup"><span data-stu-id="46212-284">Azure Data Factory creates a HDInsight Hadoop cluster just-in-time tooprocess input data and produce output data.</span></span>
3. <span data-ttu-id="46212-285">建立兩個**資料集**，其中描述輸入和輸出 HDInsight Hive 活動 hello 管線中的資料。</span><span class="sxs-lookup"><span data-stu-id="46212-285">Created two **datasets**, which describe input and output data for HDInsight Hive activity in hello pipeline.</span></span>
4. <span data-ttu-id="46212-286">建立具有 **HDInsight Hive** 活動的**管線**。</span><span class="sxs-lookup"><span data-stu-id="46212-286">Created a **pipeline** with a **HDInsight Hive** activity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="46212-287">後續步驟</span><span class="sxs-lookup"><span data-stu-id="46212-287">Next steps</span></span>
<span data-ttu-id="46212-288">在本文中，您已經建立可在隨選 Azure HDInsight 叢集上執行 Hive 指令碼，含有轉換活動 (HDInsight 活動) 的管線。</span><span class="sxs-lookup"><span data-stu-id="46212-288">In this article, you have created a pipeline with a transformation activity (HDInsight Activity) that runs a Hive script on an on-demand Azure HDInsight cluster.</span></span> <span data-ttu-id="46212-289">如何 toouse 複製活動 toocopy 資料從 Azure Blob tooAzure SQL，請參閱的 toosee[教學課程： 將資料從 Azure Blob tooAzure SQL 複製](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。</span><span class="sxs-lookup"><span data-stu-id="46212-289">toosee how toouse a Copy Activity toocopy data from an Azure Blob tooAzure SQL, see [Tutorial: Copy data from an Azure Blob tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="46212-290">另請參閱</span><span class="sxs-lookup"><span data-stu-id="46212-290">See Also</span></span>
| <span data-ttu-id="46212-291">主題</span><span class="sxs-lookup"><span data-stu-id="46212-291">Topic</span></span> | <span data-ttu-id="46212-292">說明</span><span class="sxs-lookup"><span data-stu-id="46212-292">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="46212-293">Data Factory Cmdlet 參考</span><span class="sxs-lookup"><span data-stu-id="46212-293">Data Factory Cmdlet Reference</span></span>](/powershell/module/azurerm.datafactories) |<span data-ttu-id="46212-294">請參閱 Data Factory Cmdlet 中的完整文件</span><span class="sxs-lookup"><span data-stu-id="46212-294">See comprehensive documentation on Data Factory cmdlets</span></span> |
| [<span data-ttu-id="46212-295">管線</span><span class="sxs-lookup"><span data-stu-id="46212-295">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="46212-296">這篇文章可協助您了解管線和 Azure Data Factory 中的活動以及 toouse 它們 tooconstruct 端對端資料驅動型工作流程或商務案例。</span><span class="sxs-lookup"><span data-stu-id="46212-296">This article helps you understand pipelines and activities in Azure Data Factory and how toouse them tooconstruct end-to-end data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="46212-297">資料集</span><span class="sxs-lookup"><span data-stu-id="46212-297">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="46212-298">本文協助您了解 Azure Data Factory 中的資料集。</span><span class="sxs-lookup"><span data-stu-id="46212-298">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="46212-299">排程和執行</span><span class="sxs-lookup"><span data-stu-id="46212-299">Scheduling and Execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="46212-300">本文說明 Azure Data Factory 應用程式模型的 hello 排程和執行的層面。</span><span class="sxs-lookup"><span data-stu-id="46212-300">This article explains hello scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="46212-301">使用監視應用程式來監視和管理管線</span><span class="sxs-lookup"><span data-stu-id="46212-301">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="46212-302">本文說明如何 toomonitor，管理和偵錯管線使用 hello 監視和管理應用程式。</span><span class="sxs-lookup"><span data-stu-id="46212-302">This article describes how toomonitor, manage, and debug pipelines using hello Monitoring & Management App.</span></span> |
