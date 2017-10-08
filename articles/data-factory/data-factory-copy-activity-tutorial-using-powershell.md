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
# <a name="tutorial-create-a-data-factory-pipeline-that-moves-data-by-using-azure-powershell"></a><span data-ttu-id="f42b6-103">教學課程︰使用 Azure PowerShell 建立 Data Factory 管線來移動資料</span><span class="sxs-lookup"><span data-stu-id="f42b6-103">Tutorial: Create a Data Factory pipeline that moves data by using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f42b6-104">概觀和必要條件</span><span class="sxs-lookup"><span data-stu-id="f42b6-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="f42b6-105">複製精靈</span><span class="sxs-lookup"><span data-stu-id="f42b6-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="f42b6-106">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="f42b6-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="f42b6-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f42b6-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="f42b6-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f42b6-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="f42b6-109">Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="f42b6-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="f42b6-110">REST API</span><span class="sxs-lookup"><span data-stu-id="f42b6-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="f42b6-111">.NET API</span><span class="sxs-lookup"><span data-stu-id="f42b6-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
>
>

<span data-ttu-id="f42b6-112">在本文中，您將學習如何 toouse PowerShell toocreate data factory 管線，將資料從 Azure blob 儲存體 tooan Azure SQL database 複製。</span><span class="sxs-lookup"><span data-stu-id="f42b6-112">In this article, you learn how toouse PowerShell toocreate a data factory with a pipeline that copies data from an Azure blob storage tooan Azure SQL database.</span></span> <span data-ttu-id="f42b6-113">如果您是新 tooAzure Data Factory，閱讀 hello[簡介 tooAzure Data Factory](data-factory-introduction.md)發行項，然後再執行本教學課程。</span><span class="sxs-lookup"><span data-stu-id="f42b6-113">If you are new tooAzure Data Factory, read through hello [Introduction tooAzure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span></span>   

<span data-ttu-id="f42b6-114">在本教學課程中，您可以建立包含一個活動的管線：複製活動。</span><span class="sxs-lookup"><span data-stu-id="f42b6-114">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="f42b6-115">hello 複製活動會將資料從支援的資料存放區 tooa 支援的接收資料存放區。</span><span class="sxs-lookup"><span data-stu-id="f42b6-115">hello copy activity copies data from a supported data store tooa supported sink data store.</span></span> <span data-ttu-id="f42b6-116">如需作為來源和接收區支援的資料存放區清單，請參閱[支援的資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)。</span><span class="sxs-lookup"><span data-stu-id="f42b6-116">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="f42b6-117">hello 活動被提供安全、 可靠且可擴充的方式的各種資料存放區之間的資料可以複製的全域可用服務。</span><span class="sxs-lookup"><span data-stu-id="f42b6-117">hello activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="f42b6-118">如需 hello 複製活動的詳細資訊，請參閱[資料移動活動](data-factory-data-movement-activities.md)。</span><span class="sxs-lookup"><span data-stu-id="f42b6-118">For more information about hello Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="f42b6-119">一個管線中可以有多個活動。</span><span class="sxs-lookup"><span data-stu-id="f42b6-119">A pipeline can have more than one activity.</span></span> <span data-ttu-id="f42b6-120">此外，您可以藉由設定 hello 輸出資料集的一個活動 hello 的輸入資料集的 hello 其他活動鏈結 （執行一個活動執行另一個之後） 的兩個活動。</span><span class="sxs-lookup"><span data-stu-id="f42b6-120">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="f42b6-121">如需詳細資訊，請參閱[管線中的多個活動](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline)。</span><span class="sxs-lookup"><span data-stu-id="f42b6-121">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

> [!NOTE]
> <span data-ttu-id="f42b6-122">本文並未涵蓋所有 hello Data Factory cmdlet。</span><span class="sxs-lookup"><span data-stu-id="f42b6-122">This article does not cover all hello Data Factory cmdlets.</span></span> <span data-ttu-id="f42b6-123">如需這些 Cmdlet 的完整文件，請參閱 [Data Factory Cmdlet 參考](/powershell/module/azurerm.datafactories)。</span><span class="sxs-lookup"><span data-stu-id="f42b6-123">See [Data Factory Cmdlet Reference](/powershell/module/azurerm.datafactories) for comprehensive documentation on these cmdlets.</span></span>
> 
> <span data-ttu-id="f42b6-124">在此教學課程中的 hello 資料管線會將資料從來源資料存放區 tooa 目的地資料存放區。</span><span class="sxs-lookup"><span data-stu-id="f42b6-124">hello data pipeline in this tutorial copies data from a source data store tooa destination data store.</span></span> <span data-ttu-id="f42b6-125">如需如何使用 Azure Data Factory，tootransform 資料，請參閱[教學課程： 建立使用 Hadoop 叢集管線 tootransform 資料](data-factory-build-your-first-pipeline.md)。</span><span class="sxs-lookup"><span data-stu-id="f42b6-125">For a tutorial on how tootransform data using Azure Data Factory, see [Tutorial: Build a pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f42b6-126">必要條件</span><span class="sxs-lookup"><span data-stu-id="f42b6-126">Prerequisites</span></span>
- <span data-ttu-id="f42b6-127">完成 hello 中所列必要條件[教學課程必要條件](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="f42b6-127">Complete prerequisites listed in hello [tutorial prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) article.</span></span>
- <span data-ttu-id="f42b6-128">安裝 **Azure PowerShell**。</span><span class="sxs-lookup"><span data-stu-id="f42b6-128">Install **Azure PowerShell**.</span></span> <span data-ttu-id="f42b6-129">請依照下列中的 hello 指示[如何 tooinstall 和設定 Azure PowerShell](../powershell-install-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="f42b6-129">Follow hello instructions in [How tooinstall and configure Azure PowerShell](../powershell-install-configure.md).</span></span>

## <a name="steps"></a><span data-ttu-id="f42b6-130">步驟</span><span class="sxs-lookup"><span data-stu-id="f42b6-130">Steps</span></span>
<span data-ttu-id="f42b6-131">以下是您執行本教學課程的一部分的 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="f42b6-131">Here are hello steps you perform as part of this tutorial:</span></span>

1. <span data-ttu-id="f42b6-132">建立 Azure **Data Factory**。</span><span class="sxs-lookup"><span data-stu-id="f42b6-132">Create an Azure **data factory**.</span></span> <span data-ttu-id="f42b6-133">在此步驟中，您會建立名為 ADFTutorialDataFactoryPSH 的資料處理站。</span><span class="sxs-lookup"><span data-stu-id="f42b6-133">In this step, you create a data factory named ADFTutorialDataFactoryPSH.</span></span> 
2. <span data-ttu-id="f42b6-134">建立**連結的服務**hello data factory 中。</span><span class="sxs-lookup"><span data-stu-id="f42b6-134">Create **linked services** in hello data factory.</span></span> <span data-ttu-id="f42b6-135">在此步驟中，您會建立兩種連結服務：Azure 儲存體和 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="f42b6-135">In this step, you create two linked services of types: Azure Storage and Azure SQL Database.</span></span> 
    
    <span data-ttu-id="f42b6-136">hello AzureStorageLinkedService 連結您的 Azure 儲存體帳戶 toohello data factory。</span><span class="sxs-lookup"><span data-stu-id="f42b6-136">hello AzureStorageLinkedService links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="f42b6-137">您在建立容器，並在上傳資料 toothis 儲存體帳戶的[必要條件](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。</span><span class="sxs-lookup"><span data-stu-id="f42b6-137">You created a container and uploaded data toothis storage account as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

    <span data-ttu-id="f42b6-138">AzureSqlLinkedService 連結您的 Azure SQL database toohello data factory。</span><span class="sxs-lookup"><span data-stu-id="f42b6-138">AzureSqlLinkedService links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="f42b6-139">複製 hello blob 儲存體中的 hello 資料會儲存在資料庫中。</span><span class="sxs-lookup"><span data-stu-id="f42b6-139">hello data that is copied from hello blob storage is stored in this database.</span></span> <span data-ttu-id="f42b6-140">您在此資料庫中建立了 SQL 資料表，作為[必要條件](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)的一部分。</span><span class="sxs-lookup"><span data-stu-id="f42b6-140">You created a SQL table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   
3. <span data-ttu-id="f42b6-141">建立輸入和輸出**資料集**hello data factory 中。</span><span class="sxs-lookup"><span data-stu-id="f42b6-141">Create input and output **datasets** in hello data factory.</span></span>  
    
    <span data-ttu-id="f42b6-142">hello Azure 儲存體連結服務指定 Data Factory 服務會使用在執行的階段 tooconnect tooyour Azure 儲存體帳戶的 hello 連接字串。</span><span class="sxs-lookup"><span data-stu-id="f42b6-142">hello Azure storage linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="f42b6-143">此外，hello 輸入的 blob 資料集會指定 hello 容器和包含 hello 輸入的資料的 hello 資料夾。</span><span class="sxs-lookup"><span data-stu-id="f42b6-143">And, hello input blob dataset specifies hello container and hello folder that contains hello input data.</span></span>  

    <span data-ttu-id="f42b6-144">同樣地，hello 連結的 Azure SQL Database 服務指定 hello Data Factory 服務會使用在執行的階段 tooconnect tooyour Azure SQL database 的連接字串。</span><span class="sxs-lookup"><span data-stu-id="f42b6-144">Similarly, hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="f42b6-145">此外，hello 輸出 SQL 資料表的資料集指定複製 hello hello 資料庫 toowhich hello 資料從 hello blob 儲存體中的資料表。</span><span class="sxs-lookup"><span data-stu-id="f42b6-145">And, hello output SQL table dataset specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span>
4. <span data-ttu-id="f42b6-146">建立**管線**hello data factory 中。</span><span class="sxs-lookup"><span data-stu-id="f42b6-146">Create a **pipeline** in hello data factory.</span></span> <span data-ttu-id="f42b6-147">在此步驟中，您會建立具有複製活動的管線。</span><span class="sxs-lookup"><span data-stu-id="f42b6-147">In this step, you create a pipeline with a copy activity.</span></span>   
    
    <span data-ttu-id="f42b6-148">hello 複製活動會將資料從 hello Azure SQL database 中 hello Azure blob 儲存體 tooa 資料表中的 blob。</span><span class="sxs-lookup"><span data-stu-id="f42b6-148">hello copy activity copies data from a blob in hello Azure blob storage tooa table in hello Azure SQL database.</span></span> <span data-ttu-id="f42b6-149">您可以從任何支援的來源支援 tooany 目的地管線 toocopy 資料中使用複製活動。</span><span class="sxs-lookup"><span data-stu-id="f42b6-149">You can use a copy activity in a pipeline toocopy data from any supported source tooany supported destination.</span></span> <span data-ttu-id="f42b6-150">如需支援的資料存放區清單，請參閱[資料移動活動](data-factory-data-movement-activities.md#supported-data-stores-and-formats)一文。</span><span class="sxs-lookup"><span data-stu-id="f42b6-150">For a list of supported data stores, see [data movement activities](data-factory-data-movement-activities.md#supported-data-stores-and-formats) article.</span></span> 
5. <span data-ttu-id="f42b6-151">監視 hello 管線。</span><span class="sxs-lookup"><span data-stu-id="f42b6-151">Monitor hello pipeline.</span></span> <span data-ttu-id="f42b6-152">在此步驟中，您**監視器**hello 使用 PowerShell 之輸入和輸出資料集配量。</span><span class="sxs-lookup"><span data-stu-id="f42b6-152">In this step, you **monitor** hello slices of input and output datasets by using PowerShell.</span></span>

## <a name="create-a-data-factory"></a><span data-ttu-id="f42b6-153">建立 Data Factory</span><span class="sxs-lookup"><span data-stu-id="f42b6-153">Create a data factory</span></span>
> [!IMPORTANT]
> <span data-ttu-id="f42b6-154">完成[hello 教學課程的必要條件](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)如果您還沒有。</span><span class="sxs-lookup"><span data-stu-id="f42b6-154">Complete [prerequisites for hello tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) if you haven't already done so.</span></span>   

<span data-ttu-id="f42b6-155">資料處理站可以有一或多個管線。</span><span class="sxs-lookup"><span data-stu-id="f42b6-155">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="f42b6-156">其中的管線可以有一或多個活動。</span><span class="sxs-lookup"><span data-stu-id="f42b6-156">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="f42b6-157">例如，複製活動 toocopy 資料從來源 tooa 目的地資料存放區和 HDInsight Hive 活動 toorun Hive 指令碼 tootransform 輸入資料 tooproduct 輸出資料。</span><span class="sxs-lookup"><span data-stu-id="f42b6-157">For example, a Copy Activity toocopy data from a source tooa destination data store and a HDInsight Hive activity toorun a Hive script tootransform input data tooproduct output data.</span></span> <span data-ttu-id="f42b6-158">讓我們開始在此步驟中建立 hello 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="f42b6-158">Let's start with creating hello data factory in this step.</span></span>

1. <span data-ttu-id="f42b6-159">啟動 **PowerShell**。</span><span class="sxs-lookup"><span data-stu-id="f42b6-159">Launch **PowerShell**.</span></span> <span data-ttu-id="f42b6-160">保持開啟 Azure PowerShell 直到本教學課程中的 hello 結尾。</span><span class="sxs-lookup"><span data-stu-id="f42b6-160">Keep Azure PowerShell open until hello end of this tutorial.</span></span> <span data-ttu-id="f42b6-161">如果您關閉並重新開啟，您需要 toorun hello 命令一次。</span><span class="sxs-lookup"><span data-stu-id="f42b6-161">If you close and reopen, you need toorun hello commands again.</span></span>

    <span data-ttu-id="f42b6-162">執行下列命令，hello，然後輸入 hello 使用者名稱和密碼，您會使用 toosign toohello Azure 入口網站中：</span><span class="sxs-lookup"><span data-stu-id="f42b6-162">Run hello following command, and enter hello user name and password that you use toosign in toohello Azure portal:</span></span>

    ```PowerShell
    Login-AzureRmAccount
    ```   
   
    <span data-ttu-id="f42b6-163">此帳戶的所有 hello 訂用帳戶都執行下列命令 tooview hello:</span><span class="sxs-lookup"><span data-stu-id="f42b6-163">Run hello following command tooview all hello subscriptions for this account:</span></span>

    ```PowerShell
    Get-AzureRmSubscription
    ```

    <span data-ttu-id="f42b6-164">執行下列命令 tooselect hello 訂用帳戶，您想要使用 toowork hello。</span><span class="sxs-lookup"><span data-stu-id="f42b6-164">Run hello following command tooselect hello subscription that you want toowork with.</span></span> <span data-ttu-id="f42b6-165">取代 **&lt;NameOfAzureSubscription** &gt; hello Azure 訂用帳戶名稱：</span><span class="sxs-lookup"><span data-stu-id="f42b6-165">Replace **&lt;NameOfAzureSubscription**&gt; with hello name of your Azure subscription:</span></span>

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```
2. <span data-ttu-id="f42b6-166">建立 Azure 資源群組名稱為**ADFTutorialResourceGroup**藉由執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="f42b6-166">Create an Azure resource group named **ADFTutorialResourceGroup** by running hello following command:</span></span>

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
    
    <span data-ttu-id="f42b6-167">本教學課程中的 hello 步驟假設您使用名為 「 hello 資源群組**ADFTutorialResourceGroup**。</span><span class="sxs-lookup"><span data-stu-id="f42b6-167">Some of hello steps in this tutorial assume that you use hello resource group named **ADFTutorialResourceGroup**.</span></span> <span data-ttu-id="f42b6-168">如果您使用不同的資源群組，您需要 toouse 它來取代 ADFTutorialResourceGroup 在本教學課程。</span><span class="sxs-lookup"><span data-stu-id="f42b6-168">If you use a different resource group, you need toouse it in place of ADFTutorialResourceGroup in this tutorial.</span></span>
3. <span data-ttu-id="f42b6-169">執行 hello**新增 AzureRmDataFactory** cmdlet toocreate 名為 data factory **ADFTutorialDataFactoryPSH**:</span><span class="sxs-lookup"><span data-stu-id="f42b6-169">Run hello **New-AzureRmDataFactory** cmdlet toocreate a data factory named **ADFTutorialDataFactoryPSH**:</span></span>  

    ```PowerShell
    $df=New-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name ADFTutorialDataFactoryPSH –Location "West US"
    ```
    <span data-ttu-id="f42b6-170">此名稱可能已被使用。</span><span class="sxs-lookup"><span data-stu-id="f42b6-170">This name may already have been taken.</span></span> <span data-ttu-id="f42b6-171">因此，請 hello hello data factory 名稱唯一藉由新增前置或後置 (例如： ADFTutorialDataFactoryPSH05152017) 並執行一次 hello 命令。</span><span class="sxs-lookup"><span data-stu-id="f42b6-171">Therefore, make hello name of hello data factory unique by adding a prefix or suffix (for example: ADFTutorialDataFactoryPSH05152017) and run hello command again.</span></span>  

<span data-ttu-id="f42b6-172">請注意下列點 hello:</span><span class="sxs-lookup"><span data-stu-id="f42b6-172">Note hello following points:</span></span>

* <span data-ttu-id="f42b6-173">hello hello Azure data factory 的名稱必須是全域唯一的。</span><span class="sxs-lookup"><span data-stu-id="f42b6-173">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="f42b6-174">如果您收到下列錯誤 hello，變更 hello 名稱 (例如，yournameADFTutorialDataFactoryPSH)。</span><span class="sxs-lookup"><span data-stu-id="f42b6-174">If you receive hello following error, change hello name (for example, yournameADFTutorialDataFactoryPSH).</span></span> <span data-ttu-id="f42b6-175">執行本教學課程中的步驟時，請使用此名稱來取代 ADFTutorialFactoryPSH。</span><span class="sxs-lookup"><span data-stu-id="f42b6-175">Use this name in place of ADFTutorialFactoryPSH while performing steps in this tutorial.</span></span> <span data-ttu-id="f42b6-176">請參閱 [Data Factory - 命名規則](data-factory-naming-rules.md)，以了解 Data Factory 成品的命名規則。</span><span class="sxs-lookup"><span data-stu-id="f42b6-176">See [Data Factory - Naming Rules](data-factory-naming-rules.md) for Data Factory artifacts.</span></span>

    ```
    Data factory name “ADFTutorialDataFactoryPSH” is not available
    ```
* <span data-ttu-id="f42b6-177">toocreate Data Factory 執行個體，您必須是參與者或 hello Azure 訂用帳戶的系統管理員。</span><span class="sxs-lookup"><span data-stu-id="f42b6-177">toocreate Data Factory instances, you must be a contributor or administrator of hello Azure subscription.</span></span>
* <span data-ttu-id="f42b6-178">可能會註冊為 hello 未來中的 DNS 名稱，因此會變成可見 hello hello data factory 名稱。</span><span class="sxs-lookup"><span data-stu-id="f42b6-178">hello name of hello data factory may be registered as a DNS name in hello future, and hence become publicly visible.</span></span>
* <span data-ttu-id="f42b6-179">您可能會收到 hello 下列錯誤:"**此訂用帳戶不是已註冊的 toouse 命名空間 Microsoft.DataFactory。**"</span><span class="sxs-lookup"><span data-stu-id="f42b6-179">You may receive hello following error: "**This subscription is not registered toouse namespace Microsoft.DataFactory.**"</span></span> <span data-ttu-id="f42b6-180">Hello 下列其中一種作業，並再試一次發行：</span><span class="sxs-lookup"><span data-stu-id="f42b6-180">Do one of hello following, and try publishing again:</span></span>

  * <span data-ttu-id="f42b6-181">在 Azure PowerShell 中執行下列命令 tooregister hello Data Factory 提供者的 hello:</span><span class="sxs-lookup"><span data-stu-id="f42b6-181">In Azure PowerShell, run hello following command tooregister hello Data Factory provider:</span></span>

    ```PowerShell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

    <span data-ttu-id="f42b6-182">執行下列命令 tooconfirm hello Data Factory 提供者註冊該 hello:</span><span class="sxs-lookup"><span data-stu-id="f42b6-182">Run hello following command tooconfirm that hello Data Factory provider is registered:</span></span>

    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="f42b6-183">登入使用 hello Azure 訂用帳戶 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="f42b6-183">Sign in by using hello Azure subscription toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="f42b6-184">移 tooa Data Factory 刀鋒視窗中，或在 hello Azure 入口網站中建立 data factory。</span><span class="sxs-lookup"><span data-stu-id="f42b6-184">Go tooa Data Factory blade, or create a data factory in hello Azure portal.</span></span> <span data-ttu-id="f42b6-185">這個動作會自動註冊 hello 您的提供者。</span><span class="sxs-lookup"><span data-stu-id="f42b6-185">This action automatically registers hello provider for you.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="f42b6-186">建立連結的服務</span><span class="sxs-lookup"><span data-stu-id="f42b6-186">Create linked services</span></span>
<span data-ttu-id="f42b6-187">您可以建立連結的服務中的資料處理站 toolink 資料儲存和運算服務 toohello 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="f42b6-187">You create linked services in a data factory toolink your data stores and compute services toohello data factory.</span></span> <span data-ttu-id="f42b6-188">在本教學課程中，您不會使用任何計算服務，例如 Azure HDInsight 或 Azure Data Lake Analytics。</span><span class="sxs-lookup"><span data-stu-id="f42b6-188">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span></span> <span data-ttu-id="f42b6-189">您可以使用兩種類型的資料存放區：Azure 儲存體 (來源) 和 Azure SQL Database (目的地)。</span><span class="sxs-lookup"><span data-stu-id="f42b6-189">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span></span> 

<span data-ttu-id="f42b6-190">因此，您可以建立名為 AzureStorageLinkedService 和 AzureSqlLinkedService 的兩個連結服務︰類型為 AzureStorage 和 AzureSqlDatabase。</span><span class="sxs-lookup"><span data-stu-id="f42b6-190">Therefore, you create two linked services named AzureStorageLinkedService and AzureSqlLinkedService of types: AzureStorage and AzureSqlDatabase.</span></span>  

<span data-ttu-id="f42b6-191">hello AzureStorageLinkedService 連結您的 Azure 儲存體帳戶 toohello data factory。</span><span class="sxs-lookup"><span data-stu-id="f42b6-191">hello AzureStorageLinkedService links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="f42b6-192">這個儲存體帳戶為其中一個 hello 在其中建立容器及 hello 資料上傳的過程[必要條件](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。</span><span class="sxs-lookup"><span data-stu-id="f42b6-192">This storage account is hello one in which you created a container and uploaded hello data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

<span data-ttu-id="f42b6-193">AzureSqlLinkedService 連結您的 Azure SQL database toohello data factory。</span><span class="sxs-lookup"><span data-stu-id="f42b6-193">AzureSqlLinkedService links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="f42b6-194">複製 hello blob 儲存體中的 hello 資料會儲存在資料庫中。</span><span class="sxs-lookup"><span data-stu-id="f42b6-194">hello data that is copied from hello blob storage is stored in this database.</span></span> <span data-ttu-id="f42b6-195">在此資料庫中建立 hello emp 資料表的一部分[必要條件](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。</span><span class="sxs-lookup"><span data-stu-id="f42b6-195">You created hello emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

### <a name="create-a-linked-service-for-an-azure-storage-account"></a><span data-ttu-id="f42b6-196">建立 Azure 儲存體帳戶的連結服務</span><span class="sxs-lookup"><span data-stu-id="f42b6-196">Create a linked service for an Azure storage account</span></span>
<span data-ttu-id="f42b6-197">在此步驟中，您必須連結您的 Azure 儲存體帳戶 tooyour data factory。</span><span class="sxs-lookup"><span data-stu-id="f42b6-197">In this step, you link your Azure storage account tooyour data factory.</span></span>

1. <span data-ttu-id="f42b6-198">建立名為的 JSON 檔案**AzureStorageLinkedService.json**中**C:\ADFGetStartedPSH**資料夾以 hello 下列內容: （建立 hello 資料夾 ADFGetStartedPSH 如果不存在。）</span><span class="sxs-lookup"><span data-stu-id="f42b6-198">Create a JSON file named **AzureStorageLinkedService.json** in **C:\ADFGetStartedPSH** folder with hello following content: (Create hello folder ADFGetStartedPSH if it does not already exist.)</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="f42b6-199">取代&lt;accountname&gt;和&lt;accountkey&gt;名稱與您的 Azure 儲存體帳戶金鑰儲存 hello 檔案之前。</span><span class="sxs-lookup"><span data-stu-id="f42b6-199">Replace &lt;accountname&gt; and &lt;accountkey&gt; with name and key of your Azure storage account before saving hello file.</span></span> 

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
2. <span data-ttu-id="f42b6-200">在**Azure PowerShell**，切換 toohello **ADFGetStartedPSH**資料夾。</span><span class="sxs-lookup"><span data-stu-id="f42b6-200">In **Azure PowerShell**, switch toohello **ADFGetStartedPSH** folder.</span></span>
4. <span data-ttu-id="f42b6-201">執行 hello**新增 AzureRmDataFactoryLinkedService** cmdlet toocreate hello 連結服務： **AzureStorageLinkedService**。</span><span class="sxs-lookup"><span data-stu-id="f42b6-201">Run hello **New-AzureRmDataFactoryLinkedService** cmdlet toocreate hello linked service: **AzureStorageLinkedService**.</span></span> <span data-ttu-id="f42b6-202">這個指令程式和您在本教學課程中使用其他 Data Factory cmdlet 需要您 toopass 值 hello **ResourceGroupName**和**DataFactoryName**參數。</span><span class="sxs-lookup"><span data-stu-id="f42b6-202">This cmdlet, and other Data Factory cmdlets you use in this tutorial requires you toopass values for hello **ResourceGroupName** and **DataFactoryName** parameters.</span></span> <span data-ttu-id="f42b6-203">或者，您可以傳遞 hello DataFactory 物件 hello 新增 AzureRmDataFactory cmdlet 所傳回，而不需要輸入資源群組名稱和 DataFactoryName 每次您執行 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="f42b6-203">Alternatively, you can pass hello DataFactory object returned by hello New-AzureRmDataFactory cmdlet without typing ResourceGroupName and DataFactoryName each time you run a cmdlet.</span></span> 

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\AzureStorageLinkedService.json
    ```
    <span data-ttu-id="f42b6-204">以下是 hello 範例輸出：</span><span class="sxs-lookup"><span data-stu-id="f42b6-204">Here is hello sample output:</span></span>

    ```
    LinkedServiceName : AzureStorageLinkedService
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.LinkedServiceProperties
    ProvisioningState : Succeeded
    ``` 

    <span data-ttu-id="f42b6-205">建立這項連結的服務的其他方式是 toospecify 資源群組名稱，而不是指定 hello DataFactory 物件的 data factory 名稱。</span><span class="sxs-lookup"><span data-stu-id="f42b6-205">Other way of creating this linked service is toospecify resource group name and data factory name instead of specifying hello DataFactory object.</span></span>  

    ```PowerShell
    New-AzureRmDataFactoryLinkedService -ResourceGroupName ADFTutorialResourceGroup -DataFactoryName <Name of your data factory> -File .\AzureStorageLinkedService.json
    ```

### <a name="create-a-linked-service-for-an-azure-sql-database"></a><span data-ttu-id="f42b6-206">建立 Azure SQL Database 的連結服務</span><span class="sxs-lookup"><span data-stu-id="f42b6-206">Create a linked service for an Azure SQL database</span></span>
<span data-ttu-id="f42b6-207">在此步驟中，您可以連結您的 Azure SQL database tooyour data factory。</span><span class="sxs-lookup"><span data-stu-id="f42b6-207">In this step, you link your Azure SQL database tooyour data factory.</span></span>

1. <span data-ttu-id="f42b6-208">建立名為 hello 遵循 AzureSqlLinkedService.json C:\ADFGetStartedPSH 資料夾中的 JSON 檔案內容：</span><span class="sxs-lookup"><span data-stu-id="f42b6-208">Create a JSON file named AzureSqlLinkedService.json in C:\ADFGetStartedPSH folder with hello following content:</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="f42b6-209">將 &lt;servername&gt;、&lt;databasename&gt;、&lt;username@servername&gt; 和 &lt;password&gt; 替換為您的 Azure SQL 伺服器名稱、資料庫名稱、使用者帳戶和密碼。</span><span class="sxs-lookup"><span data-stu-id="f42b6-209">Replace &lt;servername&gt;, &lt;databasename&gt;, &lt;username@servername&gt;, and &lt;password&gt; with names of your Azure SQL server, database, user account, and password.</span></span>
    
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
2. <span data-ttu-id="f42b6-210">執行下列命令 toocreate hello 連結的服務：</span><span class="sxs-lookup"><span data-stu-id="f42b6-210">Run hello following command toocreate a linked service:</span></span>

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\AzureSqlLinkedService.json
    ```
    
    <span data-ttu-id="f42b6-211">以下是 hello 範例輸出：</span><span class="sxs-lookup"><span data-stu-id="f42b6-211">Here is hello sample output:</span></span>

    ```
    LinkedServiceName : AzureSqlLinkedService
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.LinkedServiceProperties
    ProvisioningState : Succeeded
    ```

   <span data-ttu-id="f42b6-212">確認**tooAzure 服務允許存取**設定已開啟您的 SQL 資料庫伺服器。</span><span class="sxs-lookup"><span data-stu-id="f42b6-212">Confirm that **Allow access tooAzure services** setting is turned on for your SQL database server.</span></span> <span data-ttu-id="f42b6-213">tooverify 並將它開啟，執行下列步驟 hello:</span><span class="sxs-lookup"><span data-stu-id="f42b6-213">tooverify and turn it on, do hello following steps:</span></span>

    1. <span data-ttu-id="f42b6-214">登入 toohello [Azure 入口網站](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="f42b6-214">Log in toohello [Azure portal](https://portal.azure.com)</span></span>
    2. <span data-ttu-id="f42b6-215">按一下**更多服務 >** hello 左邊，然後按一下  **SQL 伺服器**在 hello**資料庫**類別目錄。</span><span class="sxs-lookup"><span data-stu-id="f42b6-215">Click **More services >** on hello left, and click **SQL servers** in hello **DATABASES** category.</span></span>
    3. <span data-ttu-id="f42b6-216">SQL 伺服器 hello 清單中選取您的伺服器。</span><span class="sxs-lookup"><span data-stu-id="f42b6-216">Select your server in hello list of SQL servers.</span></span>
    4. <span data-ttu-id="f42b6-217">在 hello SQL 伺服器刀鋒視窗中，按一下 **顯示防火牆設定**連結。</span><span class="sxs-lookup"><span data-stu-id="f42b6-217">On hello SQL server blade, click **Show firewall settings** link.</span></span>
    5. <span data-ttu-id="f42b6-218">在 hello**防火牆設定**刀鋒視窗中，按一下**ON**如**tooAzure 服務允許存取**。</span><span class="sxs-lookup"><span data-stu-id="f42b6-218">In hello **Firewall settings** blade, click **ON** for **Allow access tooAzure services**.</span></span>
    6. <span data-ttu-id="f42b6-219">按一下**儲存**hello 工具列上。</span><span class="sxs-lookup"><span data-stu-id="f42b6-219">Click **Save** on hello toolbar.</span></span> 

## <a name="create-datasets"></a><span data-ttu-id="f42b6-220">建立資料集</span><span class="sxs-lookup"><span data-stu-id="f42b6-220">Create datasets</span></span>
<span data-ttu-id="f42b6-221">在 hello 先前步驟中，您會建立連結的服務 toolink，您的 Azure 儲存體帳戶和 Azure SQL database tooyour 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="f42b6-221">In hello previous step, you created linked services toolink your Azure Storage account and Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="f42b6-222">在此步驟中，您可以定義名為 InputDataset OutputDataset 代表輸入和輸出資料儲存在 hello 分別 AzureStorageLinkedService 和 AzureSqlLinkedService 所參考的資料存放區中的兩個資料集。</span><span class="sxs-lookup"><span data-stu-id="f42b6-222">In this step, you define two datasets named InputDataset and OutputDataset that represent input and output data that is stored in hello data stores referred by AzureStorageLinkedService and AzureSqlLinkedService respectively.</span></span>

<span data-ttu-id="f42b6-223">hello Azure 儲存體連結服務指定 Data Factory 服務會使用在執行的階段 tooconnect tooyour Azure 儲存體帳戶的 hello 連接字串。</span><span class="sxs-lookup"><span data-stu-id="f42b6-223">hello Azure storage linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="f42b6-224">此外，hello 輸入的 blob 資料集 (InputDataset) 指定 hello 容器和包含 hello 輸入的資料的 hello 資料夾。</span><span class="sxs-lookup"><span data-stu-id="f42b6-224">And, hello input blob dataset (InputDataset) specifies hello container and hello folder that contains hello input data.</span></span>  

<span data-ttu-id="f42b6-225">同樣地，hello 連結的 Azure SQL Database 服務指定 hello Data Factory 服務會使用在執行的階段 tooconnect tooyour Azure SQL database 的連接字串。</span><span class="sxs-lookup"><span data-stu-id="f42b6-225">Similarly, hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="f42b6-226">此外，hello 輸出 SQL 資料表資料集 (OututDataset) 會指定 hello 資料表中 hello 資料庫 toowhich hello hello blob 儲存體的資料複製。</span><span class="sxs-lookup"><span data-stu-id="f42b6-226">And, hello output SQL table dataset (OututDataset) specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span> 

### <a name="create-an-input-dataset"></a><span data-ttu-id="f42b6-227">建立輸入資料集</span><span class="sxs-lookup"><span data-stu-id="f42b6-227">Create an input dataset</span></span>
<span data-ttu-id="f42b6-228">在此步驟中，您建立資料集名為指向 tooa blob 檔案 (emp.txt) InputDataset hello 的 blob 容器 (adftutorial) 的根資料夾中 hello hello AzureStorageLinkedService 連結服務所代表的 Azure 儲存體中。</span><span class="sxs-lookup"><span data-stu-id="f42b6-228">In this step, you create a dataset named InputDataset that points tooa blob file (emp.txt) in hello root folder of a blob container (adftutorial) in hello Azure Storage represented by hello AzureStorageLinkedService linked service.</span></span> <span data-ttu-id="f42b6-229">如果您不指定 hello 檔名的值 （或略過它），從 hello 輸入資料夾中的所有 blob 資料，則複製的 toohello 目的地。</span><span class="sxs-lookup"><span data-stu-id="f42b6-229">If you don't specify a value for hello fileName (or skip it), data from all blobs in hello input folder are copied toohello destination.</span></span> <span data-ttu-id="f42b6-230">在本教學課程中，您可以指定 hello 檔案名稱的值。</span><span class="sxs-lookup"><span data-stu-id="f42b6-230">In this tutorial, you specify a value for hello fileName.</span></span>  

1. <span data-ttu-id="f42b6-231">建立名為的 JSON 檔案**InputDataset.json**在 hello **C:\ADFGetStartedPSH**資料夾中，以下列內容的 hello:</span><span class="sxs-lookup"><span data-stu-id="f42b6-231">Create a JSON file named **InputDataset.json** in hello **C:\ADFGetStartedPSH** folder, with hello following content:</span></span>

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

    <span data-ttu-id="f42b6-232">hello 下表提供 hello hello 程式碼片段中使用的 JSON 屬性的說明：</span><span class="sxs-lookup"><span data-stu-id="f42b6-232">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

    | <span data-ttu-id="f42b6-233">屬性</span><span class="sxs-lookup"><span data-stu-id="f42b6-233">Property</span></span> | <span data-ttu-id="f42b6-234">說明</span><span class="sxs-lookup"><span data-stu-id="f42b6-234">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="f42b6-235">類型</span><span class="sxs-lookup"><span data-stu-id="f42b6-235">type</span></span> | <span data-ttu-id="f42b6-236">hello type 屬性設定太**AzureBlob**因為資料常駐於 Azure blob 儲存體中。</span><span class="sxs-lookup"><span data-stu-id="f42b6-236">hello type property is set too**AzureBlob** because data resides in an Azure blob storage.</span></span> |
    | <span data-ttu-id="f42b6-237">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="f42b6-237">linkedServiceName</span></span> | <span data-ttu-id="f42b6-238">是指 toohello **AzureStorageLinkedService**您稍早建立的。</span><span class="sxs-lookup"><span data-stu-id="f42b6-238">Refers toohello **AzureStorageLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="f42b6-239">folderPath</span><span class="sxs-lookup"><span data-stu-id="f42b6-239">folderPath</span></span> | <span data-ttu-id="f42b6-240">指定 hello blob**容器**和 hello**資料夾**，其中包含輸入的 blob。</span><span class="sxs-lookup"><span data-stu-id="f42b6-240">Specifies hello blob **container** and hello **folder** that contains input blobs.</span></span> <span data-ttu-id="f42b6-241">在本教學課程，adftutorial hello blob 容器且資料夾是 hello 根資料夾。</span><span class="sxs-lookup"><span data-stu-id="f42b6-241">In this tutorial, adftutorial is hello blob container and folder is hello root folder.</span></span> | 
    | <span data-ttu-id="f42b6-242">fileName</span><span class="sxs-lookup"><span data-stu-id="f42b6-242">fileName</span></span> | <span data-ttu-id="f42b6-243">這是選用屬性。</span><span class="sxs-lookup"><span data-stu-id="f42b6-243">This property is optional.</span></span> <span data-ttu-id="f42b6-244">如果您省略這個屬性時，會挑出 hello folderPath 中的所有檔案。</span><span class="sxs-lookup"><span data-stu-id="f42b6-244">If you omit this property, all files from hello folderPath are picked.</span></span> <span data-ttu-id="f42b6-245">在本教學課程， **emp.txt**指定了 hello 檔名，因此只有該檔案所挑選的處理。</span><span class="sxs-lookup"><span data-stu-id="f42b6-245">In this tutorial, **emp.txt** is specified for hello fileName, so only that file is picked up for processing.</span></span> |
    | <span data-ttu-id="f42b6-246">format -> type</span><span class="sxs-lookup"><span data-stu-id="f42b6-246">format -> type</span></span> |<span data-ttu-id="f42b6-247">hello 輸入的檔為 hello 文字格式，因此我們使用**TextFormat**。</span><span class="sxs-lookup"><span data-stu-id="f42b6-247">hello input file is in hello text format, so we use **TextFormat**.</span></span> |
    | <span data-ttu-id="f42b6-248">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="f42b6-248">columnDelimiter</span></span> | <span data-ttu-id="f42b6-249">hello hello 輸入檔中的資料行分隔**逗號字元 (`,`)**。</span><span class="sxs-lookup"><span data-stu-id="f42b6-249">hello columns in hello input file are delimited by **comma character (`,`)**.</span></span> |
    | <span data-ttu-id="f42b6-250">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="f42b6-250">frequency/interval</span></span> | <span data-ttu-id="f42b6-251">hello 頻率設定過**小時**和間隔設定得**1**，這表示該 hello 輸入配量可用**每小時**。</span><span class="sxs-lookup"><span data-stu-id="f42b6-251">hello frequency is set too**Hour** and interval is  set too**1**, which means that hello input slices are available **hourly**.</span></span> <span data-ttu-id="f42b6-252">換句話說，hello Data Factory 服務會尋找輸入資料每小時的 blob 容器的 hello 根資料夾中 (**adftutorial**) 指定。</span><span class="sxs-lookup"><span data-stu-id="f42b6-252">In other words, hello Data Factory service looks for input data every hour in hello root folder of blob container (**adftutorial**) you specified.</span></span> <span data-ttu-id="f42b6-253">它會尋找 hello hello 管線開始和結束時間、 不之前或之後這段時間內的資料。</span><span class="sxs-lookup"><span data-stu-id="f42b6-253">It looks for hello data within hello pipeline start and end times, not before or after these times.</span></span>  |
    | <span data-ttu-id="f42b6-254">external</span><span class="sxs-lookup"><span data-stu-id="f42b6-254">external</span></span> | <span data-ttu-id="f42b6-255">這個屬性設定太**true**如果 hello 資料不會產生此管線。</span><span class="sxs-lookup"><span data-stu-id="f42b6-255">This property is set too**true** if hello data is not generated by this pipeline.</span></span> <span data-ttu-id="f42b6-256">在此教學課程中的 hello 輸入的資料是在 hello emp.txt 檔案，不會產生這個管線，因此我們設定此屬性 tootrue。</span><span class="sxs-lookup"><span data-stu-id="f42b6-256">hello input data in this tutorial is in hello emp.txt file, which is not generated by this pipeline, so we set this property tootrue.</span></span> |

    <span data-ttu-id="f42b6-257">如需這些 JSON 屬性的詳細資訊，請參閱 [Azure Blob 連接器](data-factory-azure-blob-connector.md#dataset-properties)一文。</span><span class="sxs-lookup"><span data-stu-id="f42b6-257">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
2. <span data-ttu-id="f42b6-258">執行下列命令 toocreate hello Data Factory 的資料集的 hello。</span><span class="sxs-lookup"><span data-stu-id="f42b6-258">Run hello following command toocreate hello Data Factory dataset.</span></span>

    ```PowerShell  
    New-AzureRmDataFactoryDataset $df -File .\InputDataset.json
    ```
    <span data-ttu-id="f42b6-259">以下是 hello 範例輸出：</span><span class="sxs-lookup"><span data-stu-id="f42b6-259">Here is hello sample output:</span></span>

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

### <a name="create-an-output-dataset"></a><span data-ttu-id="f42b6-260">建立輸出資料表</span><span class="sxs-lookup"><span data-stu-id="f42b6-260">Create an output dataset</span></span>
<span data-ttu-id="f42b6-261">在這個部分 hello 步驟中，您會建立名為輸出資料集**OutputDataset**。</span><span class="sxs-lookup"><span data-stu-id="f42b6-261">In this part of hello step, you create an output dataset named **OutputDataset**.</span></span> <span data-ttu-id="f42b6-262">此資料集所代表的 hello Azure SQL database 中的點 tooa SQL 資料表**AzureSqlLinkedService**。</span><span class="sxs-lookup"><span data-stu-id="f42b6-262">This dataset points tooa SQL table in hello Azure SQL database represented by **AzureSqlLinkedService**.</span></span> 

1. <span data-ttu-id="f42b6-263">建立名為的 JSON 檔案**OutputDataset.json**在 hello **C:\ADFGetStartedPSH**資料夾以 hello 下列內容：</span><span class="sxs-lookup"><span data-stu-id="f42b6-263">Create a JSON file named **OutputDataset.json** in hello **C:\ADFGetStartedPSH** folder with hello following content:</span></span>

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

    <span data-ttu-id="f42b6-264">hello 下表提供 hello hello 程式碼片段中使用的 JSON 屬性的說明：</span><span class="sxs-lookup"><span data-stu-id="f42b6-264">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

    | <span data-ttu-id="f42b6-265">屬性</span><span class="sxs-lookup"><span data-stu-id="f42b6-265">Property</span></span> | <span data-ttu-id="f42b6-266">說明</span><span class="sxs-lookup"><span data-stu-id="f42b6-266">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="f42b6-267">類型</span><span class="sxs-lookup"><span data-stu-id="f42b6-267">type</span></span> | <span data-ttu-id="f42b6-268">hello type 屬性設定太**AzureSqlTable**因為資料是在 Azure SQL database 中的複製的 tooa 資料表。</span><span class="sxs-lookup"><span data-stu-id="f42b6-268">hello type property is set too**AzureSqlTable** because data is copied tooa table in an Azure SQL database.</span></span> |
    | <span data-ttu-id="f42b6-269">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="f42b6-269">linkedServiceName</span></span> | <span data-ttu-id="f42b6-270">是指 toohello **AzureSqlLinkedService**您稍早建立的。</span><span class="sxs-lookup"><span data-stu-id="f42b6-270">Refers toohello **AzureSqlLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="f42b6-271">tableName</span><span class="sxs-lookup"><span data-stu-id="f42b6-271">tableName</span></span> | <span data-ttu-id="f42b6-272">指定的 hello**資料表**toowhich hello 資料複製。</span><span class="sxs-lookup"><span data-stu-id="f42b6-272">Specified hello **table** toowhich hello data is copied.</span></span> | 
    | <span data-ttu-id="f42b6-273">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="f42b6-273">frequency/interval</span></span> | <span data-ttu-id="f42b6-274">hello 頻率設定過**小時**和間隔是**1**，這表示 hello 輸出配量所產生**每小時**之間 hello 管線開始和結束時間，不是在之前或之後這段時間。</span><span class="sxs-lookup"><span data-stu-id="f42b6-274">hello frequency is set too**Hour** and interval is **1**, which means that hello output slices are produced **hourly** between hello pipeline start and end times, not before or after these times.</span></span>  |

    <span data-ttu-id="f42b6-275">有三個資料行 –**識別碼**， **FirstName**，和**LastName** – hello 資料庫中的 hello emp 資料表中。</span><span class="sxs-lookup"><span data-stu-id="f42b6-275">There are three columns – **ID**, **FirstName**, and **LastName** – in hello emp table in hello database.</span></span> <span data-ttu-id="f42b6-276">識別碼是識別資料行，所以您必須只 toospecify **FirstName**和**LastName**這裡。</span><span class="sxs-lookup"><span data-stu-id="f42b6-276">ID is an identity column, so you need toospecify only **FirstName** and **LastName** here.</span></span>

    <span data-ttu-id="f42b6-277">如需這些 JSON 屬性的詳細資訊，請參閱 [Azure SQL 連接器](data-factory-azure-sql-connector.md#dataset-properties)一文。</span><span class="sxs-lookup"><span data-stu-id="f42b6-277">For more information about these JSON properties, see [Azure SQL connector article](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
2. <span data-ttu-id="f42b6-278">執行下列命令 toocreate hello 資料 factory 資料集的 hello。</span><span class="sxs-lookup"><span data-stu-id="f42b6-278">Run hello following command toocreate hello data factory dataset.</span></span>

    ```PowerShell   
    New-AzureRmDataFactoryDataset $df -File .\OutputDataset.json
    ```

    <span data-ttu-id="f42b6-279">以下是 hello 範例輸出：</span><span class="sxs-lookup"><span data-stu-id="f42b6-279">Here is hello sample output:</span></span>

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

## <a name="create-a-pipeline"></a><span data-ttu-id="f42b6-280">建立管線</span><span class="sxs-lookup"><span data-stu-id="f42b6-280">Create a pipeline</span></span>
<span data-ttu-id="f42b6-281">在此步驟中您會建立管線，其中含有使用 **InputDataset** 作為輸入和使用 **OutputDataset** 作為輸出的**複製活動**。</span><span class="sxs-lookup"><span data-stu-id="f42b6-281">In this step, you create a pipeline with a **copy activity** that uses **InputDataset** as an input and **OutputDataset** as an output.</span></span>

<span data-ttu-id="f42b6-282">目前，輸出資料集是哪些磁碟機 hello 排程。</span><span class="sxs-lookup"><span data-stu-id="f42b6-282">Currently, output dataset is what drives hello schedule.</span></span> <span data-ttu-id="f42b6-283">在本教學課程中，輸出資料集是設定的 tooproduce 配量小時一次。</span><span class="sxs-lookup"><span data-stu-id="f42b6-283">In this tutorial, output dataset is configured tooproduce a slice once an hour.</span></span> <span data-ttu-id="f42b6-284">hello 管線有開始時間和結束時間的一天分散，也就是 24 小時。</span><span class="sxs-lookup"><span data-stu-id="f42b6-284">hello pipeline has a start time and end time that are one day apart, which is 24 hours.</span></span> <span data-ttu-id="f42b6-285">因此，hello 管線所產生的輸出資料集的 24 配量。</span><span class="sxs-lookup"><span data-stu-id="f42b6-285">Therefore, 24 slices of output dataset are produced by hello pipeline.</span></span> 


1. <span data-ttu-id="f42b6-286">建立名為的 JSON 檔案**ADFTutorialPipeline.json**在 hello **C:\ADFGetStartedPSH**資料夾中，以下列內容的 hello:</span><span class="sxs-lookup"><span data-stu-id="f42b6-286">Create a JSON file named **ADFTutorialPipeline.json** in hello **C:\ADFGetStartedPSH** folder, with hello following content:</span></span>

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
    <span data-ttu-id="f42b6-287">請注意下列點 hello:</span><span class="sxs-lookup"><span data-stu-id="f42b6-287">Note hello following points:</span></span>
   
    - <span data-ttu-id="f42b6-288">在 [hello 活動] 區段中，沒有一個活動其**類型**設定得**複製**。</span><span class="sxs-lookup"><span data-stu-id="f42b6-288">In hello activities section, there is only one activity whose **type** is set too**Copy**.</span></span> <span data-ttu-id="f42b6-289">如需 hello 複製活動的詳細資訊，請參閱[資料移動活動](data-factory-data-movement-activities.md)。</span><span class="sxs-lookup"><span data-stu-id="f42b6-289">For more information about hello copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="f42b6-290">在 Data Factory 解決方案中，您也可以使用[資料轉換活動](data-factory-data-transformation-activities.md)。</span><span class="sxs-lookup"><span data-stu-id="f42b6-290">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span></span>
    - <span data-ttu-id="f42b6-291">輸入 hello 活動設定太**InputDataset**和輸出 hello 活動設定太**OutputDataset**。</span><span class="sxs-lookup"><span data-stu-id="f42b6-291">Input for hello activity is set too**InputDataset** and output for hello activity is set too**OutputDataset**.</span></span> 
    - <span data-ttu-id="f42b6-292">在 [hello **typeProperties** ] 區段中， **BlobSource**指定 hello 來源類型為和**SqlSink**指定為 hello 接收器類型。</span><span class="sxs-lookup"><span data-stu-id="f42b6-292">In hello **typeProperties** section, **BlobSource** is specified as hello source type and **SqlSink** is specified as hello sink type.</span></span> <span data-ttu-id="f42b6-293">支援的 hello 複製活動做為來源與接收的資料存放區的完整清單，請參閱[支援資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)。</span><span class="sxs-lookup"><span data-stu-id="f42b6-293">For a complete list of data stores supported by hello copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="f42b6-294">toolearn toouse 特定支援的資料如何儲存為來源/接收器，按一下 hello 資料表中的 hello 連結。</span><span class="sxs-lookup"><span data-stu-id="f42b6-294">toolearn how toouse a specific supported data store as a source/sink, click hello link in hello table.</span></span>  
     
    <span data-ttu-id="f42b6-295">取代 hello hello 值**啟動**屬性以 hello 目前的日期和**結束**以 hello 隔天的值。</span><span class="sxs-lookup"><span data-stu-id="f42b6-295">Replace hello value of hello **start** property with hello current day and **end** value with hello next day.</span></span> <span data-ttu-id="f42b6-296">您可以指定 hello 日期部分，並略過 hello hello 時間部分日期時間。</span><span class="sxs-lookup"><span data-stu-id="f42b6-296">You can specify only hello date part and skip hello time part of hello date time.</span></span> <span data-ttu-id="f42b6-297">例如，"2016年-02-03"，這相當於太"2016年-02-03T00:00:00Z"</span><span class="sxs-lookup"><span data-stu-id="f42b6-297">For example, "2016-02-03", which is equivalent too"2016-02-03T00:00:00Z"</span></span>
     
    <span data-ttu-id="f42b6-298">開始和結束日期時間都必須是 [ISO 格式](http://en.wikipedia.org/wiki/ISO_8601)。</span><span class="sxs-lookup"><span data-stu-id="f42b6-298">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="f42b6-299">例如：2016-10-14T16:32:41Z。</span><span class="sxs-lookup"><span data-stu-id="f42b6-299">For example: 2016-10-14T16:32:41Z.</span></span> <span data-ttu-id="f42b6-300">hello**結束**時間是選擇性的但我們在本教學課程中使用它。</span><span class="sxs-lookup"><span data-stu-id="f42b6-300">hello **end** time is optional, but we use it in this tutorial.</span></span> 
     
    <span data-ttu-id="f42b6-301">如果您未指定值為 hello**結束**屬性，它會計算為"**start + 48 小時**"。</span><span class="sxs-lookup"><span data-stu-id="f42b6-301">If you do not specify value for hello **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="f42b6-302">無限期地指定 toorun hello 管線**9999-09-09**為 hello hello 值**結束**屬性。</span><span class="sxs-lookup"><span data-stu-id="f42b6-302">toorun hello pipeline indefinitely, specify **9999-09-09** as hello value for hello **end** property.</span></span>
     
    <span data-ttu-id="f42b6-303">在上述範例中的 hello，有 24 資料配量每小時產生每個資料分割。</span><span class="sxs-lookup"><span data-stu-id="f42b6-303">In hello preceding example, there are 24 data slices as each data slice is produced hourly.</span></span>

    <span data-ttu-id="f42b6-304">如需管線定義中 JSON 屬性的說明，請參閱[建立管線](data-factory-create-pipelines.md)一文。</span><span class="sxs-lookup"><span data-stu-id="f42b6-304">For descriptions of JSON properties in a pipeline definition, see [create pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="f42b6-305">如需複製活動定義中 JSON 屬性的說明，請參閱[資料移動活動](data-factory-data-movement-activities.md)。</span><span class="sxs-lookup"><span data-stu-id="f42b6-305">For descriptions of JSON properties in a copy activity definition, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="f42b6-306">如需 BlobSource 所支援 JSON 屬性的說明，請參閱 [Azure Blob 連接器](data-factory-azure-blob-connector.md)一文。</span><span class="sxs-lookup"><span data-stu-id="f42b6-306">For descriptions of JSON properties supported by BlobSource, see [Azure Blob connector article](data-factory-azure-blob-connector.md).</span></span> <span data-ttu-id="f42b6-307">如需 SqlSink 支援的 JSON 屬性說明，請參閱 [Azure SQL Database 連接器](data-factory-azure-sql-connector.md)一文。</span><span class="sxs-lookup"><span data-stu-id="f42b6-307">For descriptions of JSON properties supported by SqlSink, see [Azure SQL Database connector article](data-factory-azure-sql-connector.md).</span></span>
2. <span data-ttu-id="f42b6-308">執行下列命令 toocreate hello 資料 factory 資料表的 hello。</span><span class="sxs-lookup"><span data-stu-id="f42b6-308">Run hello following command toocreate hello data factory table.</span></span>

    ```PowerShell   
    New-AzureRmDataFactoryPipeline $df -File .\ADFTutorialPipeline.json
    ```

    <span data-ttu-id="f42b6-309">以下是 hello 範例輸出：</span><span class="sxs-lookup"><span data-stu-id="f42b6-309">Here is hello sample output:</span></span> 

    ```
    PipelineName      : ADFTutorialPipeline
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.PipelinePropertie
    ProvisioningState : Succeeded
    ```

<span data-ttu-id="f42b6-310">**恭喜！**</span><span class="sxs-lookup"><span data-stu-id="f42b6-310">**Congratulations!**</span></span> <span data-ttu-id="f42b6-311">您已成功建立管線 toocopy 資料從 Azure blob 儲存體 tooan Azure SQL database 的 Azure data factory。</span><span class="sxs-lookup"><span data-stu-id="f42b6-311">You have successfully created an Azure data factory with a pipeline toocopy data from an Azure blob storage tooan Azure SQL database.</span></span> 

## <a name="monitor-hello-pipeline"></a><span data-ttu-id="f42b6-312">監視 hello 管線</span><span class="sxs-lookup"><span data-stu-id="f42b6-312">Monitor hello pipeline</span></span>
<span data-ttu-id="f42b6-313">在此步驟中，您使用 Azure PowerShell toomonitor Azure data factory 中運作。</span><span class="sxs-lookup"><span data-stu-id="f42b6-313">In this step, you use Azure PowerShell toomonitor what’s going on in an Azure data factory.</span></span>

1. <span data-ttu-id="f42b6-314">取代&lt;DataFactoryName&gt; hello 名稱為您的 data factory 和執行**Get AzureRmDataFactory**，並指派 hello 輸出 tooa 變數 $df。</span><span class="sxs-lookup"><span data-stu-id="f42b6-314">Replace &lt;DataFactoryName&gt; with hello name of your data factory and run **Get-AzureRmDataFactory**, and assign hello output tooa variable $df.</span></span>

    ```PowerShell  
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name <DataFactoryName>
    ```

    <span data-ttu-id="f42b6-315">例如：</span><span class="sxs-lookup"><span data-stu-id="f42b6-315">For example:</span></span>
    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name ADFTutorialDataFactoryPSH0516
    ```
    
    <span data-ttu-id="f42b6-316">然後，執行列印 hello 內容 $df toosee hello 下列輸出：</span><span class="sxs-lookup"><span data-stu-id="f42b6-316">Then, run print hello contents of $df toosee hello following output:</span></span> 
    
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
2. <span data-ttu-id="f42b6-317">執行**Get AzureRmDataFactorySlice** tooget 詳細所有配量的 hello **OutputDataset**，這是 hello 管線的 hello 輸出資料集。</span><span class="sxs-lookup"><span data-stu-id="f42b6-317">Run **Get-AzureRmDataFactorySlice** tooget details about all slices of hello **OutputDataset**, which is hello output dataset of hello pipeline.</span></span>  

    ```PowerShell   
    Get-AzureRmDataFactorySlice $df -DatasetName OutputDataset -StartDateTime 2017-05-11T00:00:00Z
    ```

   <span data-ttu-id="f42b6-318">這項設定應該符合 hello**啟動**hello 管線 JSON 中的值。</span><span class="sxs-lookup"><span data-stu-id="f42b6-318">This setting should match hello **Start** value in hello pipeline JSON.</span></span> <span data-ttu-id="f42b6-319">您應該會看到 24 配量，其中每個小時從 12 AM 的 hello 當天 too12 我的 hello 隔天。</span><span class="sxs-lookup"><span data-stu-id="f42b6-319">You should see 24 slices, one for each hour from 12 AM of hello current day too12 AM of hello next day.</span></span>

   <span data-ttu-id="f42b6-320">以下是從 hello 輸出三個範例配量：</span><span class="sxs-lookup"><span data-stu-id="f42b6-320">Here are three sample slices from hello output:</span></span> 

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
3. <span data-ttu-id="f42b6-321">執行**Get AzureRmDataFactoryRun** tooget hello 詳細資料的活動已執行**特定**配量。</span><span class="sxs-lookup"><span data-stu-id="f42b6-321">Run **Get-AzureRmDataFactoryRun** tooget hello details of activity runs for a **specific** slice.</span></span> <span data-ttu-id="f42b6-322">複製 hello 前一個命令 toospecify hello 參數的值 hello StartDateTime hello 輸出 hello 日期-時間值。</span><span class="sxs-lookup"><span data-stu-id="f42b6-322">Copy hello date-time value from hello output of hello previous command toospecify hello value for hello StartDateTime parameter.</span></span> 

    ```PowerShell  
    Get-AzureRmDataFactoryRun $df -DatasetName OutputDataset -StartDateTime "5/11/2017 09:00:00 PM"
    ```

   <span data-ttu-id="f42b6-323">以下是 hello 範例輸出：</span><span class="sxs-lookup"><span data-stu-id="f42b6-323">Here is hello sample output:</span></span> 

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

<span data-ttu-id="f42b6-324">如需 Data Factory Cmdlet 的完整文件，請參閱 [Data Factory Cmdlet 參考](/powershell/module/azurerm.datafactories)。</span><span class="sxs-lookup"><span data-stu-id="f42b6-324">For comprehensive documentation on Data Factory cmdlets, see [Data Factory Cmdlet Reference](/powershell/module/azurerm.datafactories).</span></span>

## <a name="summary"></a><span data-ttu-id="f42b6-325">摘要</span><span class="sxs-lookup"><span data-stu-id="f42b6-325">Summary</span></span>
<span data-ttu-id="f42b6-326">在本教學課程中，您可以建立 Azure data factory toocopy 資料從 Azure blob tooan Azure SQL database。</span><span class="sxs-lookup"><span data-stu-id="f42b6-326">In this tutorial, you created an Azure data factory toocopy data from an Azure blob tooan Azure SQL database.</span></span> <span data-ttu-id="f42b6-327">您可以使用 PowerShell toocreate hello 資料處理站、 連結的服務、 資料集和管線。</span><span class="sxs-lookup"><span data-stu-id="f42b6-327">You used PowerShell toocreate hello data factory, linked services, datasets, and a pipeline.</span></span> <span data-ttu-id="f42b6-328">以下是您執行本教學課程中的 hello 高階步驟：</span><span class="sxs-lookup"><span data-stu-id="f42b6-328">Here are hello high-level steps you performed in this tutorial:</span></span>  

1. <span data-ttu-id="f42b6-329">建立 Azure **Data Factory**。</span><span class="sxs-lookup"><span data-stu-id="f42b6-329">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="f42b6-330">建立 **連結服務**：</span><span class="sxs-lookup"><span data-stu-id="f42b6-330">Created **linked services**:</span></span>

   <span data-ttu-id="f42b6-331">a.</span><span class="sxs-lookup"><span data-stu-id="f42b6-331">a.</span></span> <span data-ttu-id="f42b6-332">**Azure 儲存體**連結服務 toolink 您保留輸入的資料的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="f42b6-332">An **Azure Storage** linked service toolink your Azure storage account that holds input data.</span></span>     
   <span data-ttu-id="f42b6-333">b.</span><span class="sxs-lookup"><span data-stu-id="f42b6-333">b.</span></span> <span data-ttu-id="f42b6-334">**Azure SQL**連結服務 toolink hello 輸出資料會保存您 SQL database。</span><span class="sxs-lookup"><span data-stu-id="f42b6-334">An **Azure SQL** linked service toolink your SQL database that holds hello output data.</span></span>
3. <span data-ttu-id="f42b6-335">建立可描述管線輸入資料和輸出資料的 **資料集** 。</span><span class="sxs-lookup"><span data-stu-id="f42b6-335">Created **datasets** that describe input data and output data for pipelines.</span></span>
4. <span data-ttu-id="f42b6-336">建立**管線**與**複製活動**，與**BlobSource**為 hello 來源和**SqlSink**為 hello 接收。</span><span class="sxs-lookup"><span data-stu-id="f42b6-336">Created a **pipeline** with **Copy Activity**, with **BlobSource** as hello source and **SqlSink** as hello sink.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f42b6-337">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f42b6-337">Next steps</span></span>
<span data-ttu-id="f42b6-338">在本教學課程中，您可使用 Azure Blob 儲存體作為來源資料存放區以及使用 Azure SQL Database 作為複製作業的目的地資料存放區。</span><span class="sxs-lookup"><span data-stu-id="f42b6-338">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="f42b6-339">hello 下表提供 hello 複製活動支援做為來源和目的地資料存放區的清單：</span><span class="sxs-lookup"><span data-stu-id="f42b6-339">hello following table provides a list of data stores supported as sources and destinations by hello copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="f42b6-340">關於如何 toocopy 資料，從資料存放區，toolearn 按一下 hello 連結 hello hello 資料表中的資料存放區。</span><span class="sxs-lookup"><span data-stu-id="f42b6-340">toolearn about how toocopy data to/from a data store, click hello link for hello data store in hello table.</span></span> 

