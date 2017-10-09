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
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-portal"></a><span data-ttu-id="9f4b6-103">教學課程：使用 Azure 入口網站建置您的第一個 Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="9f4b6-103">Tutorial: Build your first Azure data factory using Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9f4b6-104">概觀和必要條件</span><span class="sxs-lookup"><span data-stu-id="9f4b6-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="9f4b6-105">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="9f4b6-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="9f4b6-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9f4b6-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="9f4b6-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9f4b6-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="9f4b6-108">Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="9f4b6-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="9f4b6-109">REST API</span><span class="sxs-lookup"><span data-stu-id="9f4b6-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)


<span data-ttu-id="9f4b6-110">在本文中，您將學習如何 toouse [Azure 入口網站](https://portal.azure.com/)toocreate 第一個 Azure data factory。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-110">In this article, you learn how toouse [Azure portal](https://portal.azure.com/) toocreate your first Azure data factory.</span></span> <span data-ttu-id="9f4b6-111">toodo hello 教學課程中使用其他工具/Sdk，從 hello 下拉式清單選取其中一個 hello 選項。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-111">toodo hello tutorial using other tools/SDKs, select one of hello options from hello drop-down list.</span></span> 

<span data-ttu-id="9f4b6-112">在此教學課程中的 hello 管線有一個活動： **HDInsight Hive 活動**。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-112">hello pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="9f4b6-113">此活動會在轉換輸入資料 tooproduce 輸出資料的 Azure HDInsight 叢集上執行 hive 指令碼。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data tooproduce output data.</span></span> <span data-ttu-id="9f4b6-114">hello 管線是排程的 toorun，每個月之間 hello 指定開始和結束時間之後。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-114">hello pipeline is scheduled toorun once a month between hello specified start and end times.</span></span> 

> [!NOTE]
> <span data-ttu-id="9f4b6-115">在此教學課程中的 hello 資料管線轉換輸入的資料 tooproduce 輸出資料。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-115">hello data pipeline in this tutorial transforms input data tooproduce output data.</span></span> <span data-ttu-id="9f4b6-116">如需如何使用 Azure Data Factory，toocopy 資料，請參閱[教學課程： 將資料從 Blob 儲存體 tooSQL 資料庫複製](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-116">For a tutorial on how toocopy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
> 
> <span data-ttu-id="9f4b6-117">一個管線中可以有多個活動。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-117">A pipeline can have more than one activity.</span></span> <span data-ttu-id="9f4b6-118">此外，您可以藉由設定 hello 輸出資料集的一個活動 hello 的輸入資料集的 hello 其他活動鏈結 （執行一個活動執行另一個之後） 的兩個活動。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-118">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="9f4b6-119">如需詳細資訊，請參閱 [Data Factory 排程和執行](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline)。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-119">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9f4b6-120">必要條件</span><span class="sxs-lookup"><span data-stu-id="9f4b6-120">Prerequisites</span></span>
1. <span data-ttu-id="9f4b6-121">閱讀[教學課程概觀](data-factory-build-your-first-pipeline.md)文件，以及完成 hello**必要條件**步驟。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-121">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete hello **prerequisite** steps.</span></span>
2. <span data-ttu-id="9f4b6-122">這份文件不提供 hello Azure Data Factory 服務的概觀。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-122">This article does not provide a conceptual overview of hello Azure Data Factory service.</span></span> <span data-ttu-id="9f4b6-123">我們建議您瀏覽[簡介 tooAzure Data Factory](data-factory-introduction.md) hello 服務的發行項的詳細概觀。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-123">We recommend that you go through [Introduction tooAzure Data Factory](data-factory-introduction.md) article for a detailed overview of hello service.</span></span>  

## <a name="create-data-factory"></a><span data-ttu-id="9f4b6-124">建立 Data Factory</span><span class="sxs-lookup"><span data-stu-id="9f4b6-124">Create data factory</span></span>
<span data-ttu-id="9f4b6-125">資料處理站可以有一或多個管線。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-125">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="9f4b6-126">其中的管線可以有一或多個活動。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-126">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="9f4b6-127">例如，複製活動 toocopy 資料從來源 tooa 目的地資料存放區和 HDInsight Hive 活動 toorun Hive 指令碼 tootransform 輸入資料 tooproduct 輸出資料。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-127">For example, a Copy Activity toocopy data from a source tooa destination data store and a HDInsight Hive activity toorun a Hive script tootransform input data tooproduct output data.</span></span> <span data-ttu-id="9f4b6-128">讓我們開始在此步驟中建立 hello 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-128">Let's start with creating hello data factory in this step.</span></span>

1. <span data-ttu-id="9f4b6-129">登入 toohello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-129">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="9f4b6-130">按一下**新增**hello 左窗格中，按一下 **資料 + 分析**，然後按一下**Data Factory**。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-130">Click **NEW** on hello left menu, click **Data + Analytics**, and click **Data Factory**.</span></span>

   ![建立刀鋒視窗](./media/data-factory-build-your-first-pipeline-using-editor/create-blade.png)
3. <span data-ttu-id="9f4b6-132">在 hello**新的 data factory**刀鋒視窗中，輸入**GetStartedDF** hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-132">In hello **New data factory** blade, enter **GetStartedDF** for hello Name.</span></span>

   ![新增 Data Factory 刀鋒視窗](./media/data-factory-build-your-first-pipeline-using-editor/new-data-factory-blade.png)

   > [!IMPORTANT]
   > <span data-ttu-id="9f4b6-134">hello hello Azure data factory 的名稱必須是**全域唯一**。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-134">hello name of hello Azure data factory must be **globally unique**.</span></span> <span data-ttu-id="9f4b6-135">如果您收到 hello 錯誤： **Data factory 名稱"GetStartedDF"不是使用**。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-135">If you receive hello error: **Data factory name “GetStartedDF” is not available**.</span></span> <span data-ttu-id="9f4b6-136">變更 hello hello data factory (例如，yournameGetStartedDF) 名稱，然後再試一次建立。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-136">Change hello name of hello data factory (for example, yournameGetStartedDF) and try creating again.</span></span> <span data-ttu-id="9f4b6-137">請參閱 [Data Factory - 命名規則](data-factory-naming-rules.md) 主題，以了解 Data Factory 成品的命名規則。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-137">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
   >
   > <span data-ttu-id="9f4b6-138">hello hello data factory 名稱可能會註冊為**DNS** hello 未來中的名稱，因此公開可見。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-138">hello name of hello data factory may be registered as a **DNS** name in hello future and hence become publically visible.</span></span>
   >
   >
4. <span data-ttu-id="9f4b6-139">選取 hello **Azure 訂用帳戶**您想要建立 hello 資料 factory toobe。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-139">Select hello **Azure subscription** where you want hello data factory toobe created.</span></span>
5. <span data-ttu-id="9f4b6-140">請選取現有的 **資源群組** ，或建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-140">Select existing **resource group** or create a resource group.</span></span> <span data-ttu-id="9f4b6-141">Hello 教學課程中，建立名為的資源群組： **ADFGetStartedRG**。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-141">For hello tutorial, create a resource group named: **ADFGetStartedRG**.</span></span>
6. <span data-ttu-id="9f4b6-142">選取 hello**位置**hello data factory。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-142">Select hello **location** for hello data factory.</span></span> <span data-ttu-id="9f4b6-143">Hello 下拉式清單中會顯示 hello Data Factory 服務所支援的區域。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-143">Only regions supported by hello Data Factory service are shown in hello drop-down list.</span></span>
7. <span data-ttu-id="9f4b6-144">選取**Pin toodashboard**。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-144">Select **Pin toodashboard**.</span></span> 
8. <span data-ttu-id="9f4b6-145">按一下**建立**上 hello**新的 data factory**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-145">Click **Create** on hello **New data factory** blade.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="9f4b6-146">toocreate Data Factory 執行個體，您必須是成員的 hello[資料 Factory 參與者](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor)hello 訂用帳戶/資源群組層級角色。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-146">toocreate Data Factory instances, you must be a member of hello [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at hello subscription/resource group level.</span></span>
   >
   >
7. <span data-ttu-id="9f4b6-147">在 hello 儀表板，您會看到狀態磚的 hello 下列： 部署資料處理站。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-147">On hello dashboard, you see hello following tile with status: Deploying data factory.</span></span>    

   ![建立 Data Factory 狀態](./media/data-factory-build-your-first-pipeline-using-editor/creating-data-factory-image.png)
8. <span data-ttu-id="9f4b6-149">恭喜！</span><span class="sxs-lookup"><span data-stu-id="9f4b6-149">Congratulations!</span></span> <span data-ttu-id="9f4b6-150">您已成功建立您的第一個 Data Factroy。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-150">You have successfully created your first data factory.</span></span> <span data-ttu-id="9f4b6-151">已成功建立 hello 資料處理站之後，您會看到 hello 資料 factory 頁面上，它會顯示 hello hello data factory 的內容。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-151">After hello data factory has been created successfully, you see hello data factory page, which shows you hello contents of hello data factory.</span></span>     

    ![Data Factory 刀鋒視窗](./media/data-factory-build-your-first-pipeline-using-editor/data-factory-blade.png)

<span data-ttu-id="9f4b6-153">之前 hello data factory 中建立管線，您必須 toocreate 幾個 Data Factory 實體第一次。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-153">Before creating a pipeline in hello data factory, you need toocreate a few Data Factory entities first.</span></span> <span data-ttu-id="9f4b6-154">您第一次建立連結的服務 toolink 資料存放區/計算 tooyour 資料儲存、 定義輸入和輸出連結的資料儲存區中的資料集 toorepresent 輸入/輸出資料，然後以該活動會使用這些資料集來建立 hello 管線。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-154">You first create linked services toolink data stores/computes tooyour data store, define input and output datasets toorepresent input/output data in linked data stores, and then create hello pipeline with an activity that uses these datasets.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="9f4b6-155">建立連結的服務</span><span class="sxs-lookup"><span data-stu-id="9f4b6-155">Create linked services</span></span>
<span data-ttu-id="9f4b6-156">在此步驟中，您可以連結您的 Azure 儲存體帳戶和隨 Azure HDInsight 叢集 tooyour 資料處理站。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-156">In this step, you link your Azure Storage account and an on-demand Azure HDInsight cluster tooyour data factory.</span></span> <span data-ttu-id="9f4b6-157">hello 保存 hello hello 管線，在此範例中的輸入和輸出資料的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-157">hello Azure Storage account holds hello input and output data for hello pipeline in this sample.</span></span> <span data-ttu-id="9f4b6-158">hello HDInsight 連結服務是使用的 toorun hello 管線，在此範例中的 hello 活動中指定的 Hive 指令碼。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-158">hello HDInsight linked service is used toorun a Hive script specified in hello activity of hello pipeline in this sample.</span></span> <span data-ttu-id="9f4b6-159">識別哪些[資料存放區](data-factory-data-movement-activities.md)/[計算服務](data-factory-compute-linked-services.md)用於您案例，並將這些服務 toohello 資料 factory 連結藉由建立連結的服務。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-159">Identify what [data store](data-factory-data-movement-activities.md)/[compute services](data-factory-compute-linked-services.md) are used in your scenario and link those services toohello data factory by creating linked services.</span></span>  

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="9f4b6-160">建立 Azure 儲存體連結服務</span><span class="sxs-lookup"><span data-stu-id="9f4b6-160">Create Azure Storage linked service</span></span>
<span data-ttu-id="9f4b6-161">在此步驟中，您必須連結您的 Azure 儲存體帳戶 tooyour data factory。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-161">In this step, you link your Azure Storage account tooyour data factory.</span></span> <span data-ttu-id="9f4b6-162">在此教學課程中，您可以使用 hello toostore 輸入/輸出資料與 hello HQL 指令碼檔案的相同 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-162">In this tutorial, you use hello same Azure Storage account toostore input/output data and hello HQL script file.</span></span>

1. <span data-ttu-id="9f4b6-163">按一下**作者及部署**上 hello **DATA FACTORY**刀鋒伺服器**GetStartedDF**。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-163">Click **Author and deploy** on hello **DATA FACTORY** blade for **GetStartedDF**.</span></span> <span data-ttu-id="9f4b6-164">您應該會看到 hello Data Factory 編輯器。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-164">You should see hello Data Factory Editor.</span></span>

   ![[製作和部署] 圖格](./media/data-factory-build-your-first-pipeline-using-editor/data-factory-author-deploy.png)
2. <span data-ttu-id="9f4b6-166">按一下 [新增資料存放區] 並選擇 [Azure 儲存體]。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-166">Click **New data store** and choose **Azure storage**.</span></span>

   ![新增資料存放區 - Azure 儲存體 - 功能表](./media/data-factory-build-your-first-pipeline-using-editor/new-data-store-azure-storage-menu.png)
3. <span data-ttu-id="9f4b6-168">您應該會看見 hello JSON 指令碼來建立 Azure 儲存體已連結的 hello 編輯器中的服務。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-168">You should see hello JSON script for creating an Azure Storage linked service in hello editor.</span></span>

   ![Azure 儲存體連結服務](./media/data-factory-build-your-first-pipeline-using-editor/azure-storage-linked-service.png)
4. <span data-ttu-id="9f4b6-170">取代**帳戶名稱**hello Azure 儲存體帳戶名稱和**帳戶金鑰**hello 的 hello Azure 儲存體帳戶的存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-170">Replace **account name** with hello name of your Azure storage account and **account key** with hello access key of hello Azure storage account.</span></span> <span data-ttu-id="9f4b6-171">toolearn 如何 tooget 您的儲存體存取金鑰，請參閱有關如何 tooview、 複製和重新產生儲存體存取金鑰中的 hello 資訊[管理您的儲存體帳戶](../storage/common/storage-create-storage-account.md#manage-your-storage-account)。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-171">toolearn how tooget your storage access key, see hello information about how tooview, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
5. <span data-ttu-id="9f4b6-172">按一下**部署**hello 命令列 toodeploy hello 連結服務。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-172">Click **Deploy** on hello command bar toodeploy hello linked service.</span></span>

    ![[部署] 按鈕](./media/data-factory-build-your-first-pipeline-using-editor/deploy-button.png)

   <span data-ttu-id="9f4b6-174">Hello 連結的服務已成功部署之後，hello **Draft 1**視窗應該就會消失，而且您會看到**AzureStorageLinkedService** hello hello 左側的樹狀檢視中。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-174">After hello linked service is deployed successfully, hello **Draft-1** window should disappear and you see **AzureStorageLinkedService** in hello tree view on hello left.</span></span>

    ![功能表中的儲存體連結服務](./media/data-factory-build-your-first-pipeline-using-editor/StorageLinkedServiceInTree.png)    

### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="9f4b6-176">建立 Azure HDInsight 連結服務</span><span class="sxs-lookup"><span data-stu-id="9f4b6-176">Create Azure HDInsight linked service</span></span>
<span data-ttu-id="9f4b6-177">在此步驟中，您可以連結的隨選 HDInsight 叢集 tooyour 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-177">In this step, you link an on-demand HDInsight cluster tooyour data factory.</span></span> <span data-ttu-id="9f4b6-178">自動在執行階段建立及刪除它為了處理和閒置 hello 指定的時間量之後 hello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-178">hello HDInsight cluster is automatically created at runtime and deleted after it is done processing and idle for hello specified amount of time.</span></span>

1. <span data-ttu-id="9f4b6-179">在 hello **Data Factory 編輯器**，按一下  **...**更多，按一下 新增計算，然後選取 HDInsight 隨選叢集。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-179">In hello **Data Factory Editor**, click **... More**, click **New compute**, and select **On-demand HDInsight cluster**.</span></span>

    ![新增計算](./media/data-factory-build-your-first-pipeline-using-editor/new-compute-menu.png)
2. <span data-ttu-id="9f4b6-181">複製並貼上下列程式碼片段 toohello hello **Draft 1**視窗。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-181">Copy and paste hello following snippet toohello **Draft-1** window.</span></span> <span data-ttu-id="9f4b6-182">hello JSON 片段會說明使用的 toocreate hello HDInsight 叢集隨 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-182">hello JSON snippet describes hello properties that are used toocreate hello HDInsight cluster on-demand.</span></span>

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

    <span data-ttu-id="9f4b6-183">hello 下表提供 hello hello 程式碼片段中使用的 JSON 屬性的說明：</span><span class="sxs-lookup"><span data-stu-id="9f4b6-183">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

   | <span data-ttu-id="9f4b6-184">屬性</span><span class="sxs-lookup"><span data-stu-id="9f4b6-184">Property</span></span> | <span data-ttu-id="9f4b6-185">說明</span><span class="sxs-lookup"><span data-stu-id="9f4b6-185">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="9f4b6-186">ClusterSize</span><span class="sxs-lookup"><span data-stu-id="9f4b6-186">ClusterSize</span></span> |<span data-ttu-id="9f4b6-187">指定 hello hello HDInsight 叢集大小。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-187">Specifies hello size of hello HDInsight cluster.</span></span> |
   | <span data-ttu-id="9f4b6-188">TimeToLive</span><span class="sxs-lookup"><span data-stu-id="9f4b6-188">TimeToLive</span></span> | <span data-ttu-id="9f4b6-189">於刪除之前，請指定 hello HDInsight 叢集，該 hello 閒置時間。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-189">Specifies that hello idle time for hello HDInsight cluster, before it is deleted.</span></span> |
   | <span data-ttu-id="9f4b6-190">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="9f4b6-190">linkedServiceName</span></span> | <span data-ttu-id="9f4b6-191">指定 hello 是使用的 toostore hello 記錄 HDInsight 所產生的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-191">Specifies hello storage account that is used toostore hello logs that are generated by HDInsight.</span></span> |

    <span data-ttu-id="9f4b6-192">請注意下列點 hello:</span><span class="sxs-lookup"><span data-stu-id="9f4b6-192">Note hello following points:</span></span>

   * <span data-ttu-id="9f4b6-193">hello Data Factory 建立**linux**以 hello JSON 為您的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-193">hello Data Factory creates a **Linux-based** HDInsight cluster for you with hello JSON.</span></span> <span data-ttu-id="9f4b6-194">如需詳細資訊，請參閱 [HDInsight 隨選連結服務](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) 。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-194">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
   * <span data-ttu-id="9f4b6-195">您可以使用 **自己的 HDInsight 叢集** ，不必使用隨選的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-195">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="9f4b6-196">如需詳細資訊，請參閱 [HDInsight 連結服務](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) 。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-196">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span></span>
   * <span data-ttu-id="9f4b6-197">hello HDInsight 叢集建立**預設容器**hello hello JSON 中指定的 blob 儲存體中 (**linkedServiceName**)。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-197">hello HDInsight cluster creates a **default container** in hello blob storage you specified in hello JSON (**linkedServiceName**).</span></span> <span data-ttu-id="9f4b6-198">HDInsight 刪除 hello 叢集時，不會刪除此容器。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-198">HDInsight does not delete this container when hello cluster is deleted.</span></span> <span data-ttu-id="9f4b6-199">這是設計的行為。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-199">This behavior is by design.</span></span> <span data-ttu-id="9f4b6-200">在使用 HDInsight 隨選連結服務時，除非有現有的即時叢集 (**timeToLive**)，否則每次處理配量時，就會建立 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-200">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (**timeToLive**).</span></span> <span data-ttu-id="9f4b6-201">hello 處理完成時，會自動刪除 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-201">hello cluster is automatically deleted when hello processing is done.</span></span>

       <span data-ttu-id="9f4b6-202">隨著處理的配量越來越多，您會在 Azure Blob 儲存體中看到許多容器。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-202">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="9f4b6-203">如果您不需要它們進行疑難排解的 hello 工作，您可能會想 toodelete 它們 tooreduce hello 儲存體成本。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-203">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="9f4b6-204">這些容器的 hello 名稱遵循模式: 「 adf**yourdatafactoryname**-**linkedservicename**-datetimestamp"。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-204">hello names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="9f4b6-205">使用工具，例如[Microsoft 儲存體總管](http://storageexplorer.com/)toodelete 容器，在您的 Azure blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-205">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) toodelete containers in your Azure blob storage.</span></span>

     <span data-ttu-id="9f4b6-206">如需詳細資訊，請參閱 [HDInsight 隨選連結服務](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) 。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-206">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
3. <span data-ttu-id="9f4b6-207">按一下**部署**hello 命令列 toodeploy hello 連結服務。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-207">Click **Deploy** on hello command bar toodeploy hello linked service.</span></span>

    ![部署 HDInsight 隨選連結服務](./media/data-factory-build-your-first-pipeline-using-editor/ondemand-hdinsight-deploy.png)
4. <span data-ttu-id="9f4b6-209">確認您看到兩者**AzureStorageLinkedService**和**HDInsightOnDemandLinkedService** hello hello 左側的樹狀檢視中。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-209">Confirm that you see both **AzureStorageLinkedService** and **HDInsightOnDemandLinkedService** in hello tree view on hello left.</span></span>

    ![含連結服務的樹狀檢視](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-linked-services.png)

## <a name="create-datasets"></a><span data-ttu-id="9f4b6-211">建立資料集</span><span class="sxs-lookup"><span data-stu-id="9f4b6-211">Create datasets</span></span>
<span data-ttu-id="9f4b6-212">在此步驟中，您可以建立資料集 toorepresent hello 輸入和輸出 Hive 處理的資料。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-212">In this step, you create datasets toorepresent hello input and output data for Hive processing.</span></span> <span data-ttu-id="9f4b6-213">這些資料集，請參閱 toohello **AzureStorageLinkedService**稍早在本教學課程中，您已建立。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-213">These datasets refer toohello **AzureStorageLinkedService** you have created earlier in this tutorial.</span></span> <span data-ttu-id="9f4b6-214">hello 連結的服務點 tooan Azure 儲存體帳戶和資料集指定保留輸入 hello 儲存體中的容器、 資料夾、 檔案名稱和輸出資料。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-214">hello linked service points tooan Azure Storage account and datasets specify container, folder, file name in hello storage that holds input and output data.</span></span>   

### <a name="create-input-dataset"></a><span data-ttu-id="9f4b6-215">建立輸入資料集</span><span class="sxs-lookup"><span data-stu-id="9f4b6-215">Create input dataset</span></span>
1. <span data-ttu-id="9f4b6-216">在 hello **Data Factory 編輯器**，按一下  **...多個**hello 命令列上，按一下**新的資料集**，然後選取**Azure Blob 儲存體**。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-216">In hello **Data Factory Editor**, click **... More** on hello command bar, click **New dataset**, and select **Azure Blob storage**.</span></span>

    ![新增資料集](./media/data-factory-build-your-first-pipeline-using-editor/new-data-set.png)
2. <span data-ttu-id="9f4b6-218">複製並貼上下列程式碼片段 toohello Draft 1 視窗 hello。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-218">Copy and paste hello following snippet toohello Draft-1 window.</span></span> <span data-ttu-id="9f4b6-219">在 hello JSON 片段中，您要建立資料集稱為**AzureBlobInput**代表 hello 管線中活動的輸入的資料。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-219">In hello JSON snippet, you are creating a dataset called **AzureBlobInput** that represents input data for an activity in hello pipeline.</span></span> <span data-ttu-id="9f4b6-220">此外，您可以指定 hello 輸入的資料位於呼叫 hello blob 容器**adfgetstarted**和 hello 資料夾稱為**inputdata**。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-220">In addition, you specify that hello input data is located in hello blob container called **adfgetstarted** and hello folder called **inputdata**.</span></span>

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
    <span data-ttu-id="9f4b6-221">hello 下表提供 hello hello 程式碼片段中使用的 JSON 屬性的說明：</span><span class="sxs-lookup"><span data-stu-id="9f4b6-221">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

   | <span data-ttu-id="9f4b6-222">屬性</span><span class="sxs-lookup"><span data-stu-id="9f4b6-222">Property</span></span> | <span data-ttu-id="9f4b6-223">說明</span><span class="sxs-lookup"><span data-stu-id="9f4b6-223">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="9f4b6-224">類型</span><span class="sxs-lookup"><span data-stu-id="9f4b6-224">type</span></span> |<span data-ttu-id="9f4b6-225">hello type 屬性設定太**AzureBlob**因為資料常駐於 Azure blob 儲存體中。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-225">hello type property is set too**AzureBlob** because data resides in an Azure blob storage.</span></span> |
   | <span data-ttu-id="9f4b6-226">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="9f4b6-226">linkedServiceName</span></span> |<span data-ttu-id="9f4b6-227">是指 toohello **AzureStorageLinkedService**您稍早建立。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-227">Refers toohello **AzureStorageLinkedService** you created earlier.</span></span> |
   | <span data-ttu-id="9f4b6-228">folderPath</span><span class="sxs-lookup"><span data-stu-id="9f4b6-228">folderPath</span></span> | <span data-ttu-id="9f4b6-229">指定 hello blob**容器**和 hello**資料夾**，其中包含輸入的 blob。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-229">Specifies hello blob **container** and hello **folder** that contains input blobs.</span></span> | 
   | <span data-ttu-id="9f4b6-230">fileName</span><span class="sxs-lookup"><span data-stu-id="9f4b6-230">fileName</span></span> |<span data-ttu-id="9f4b6-231">這是選用屬性。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-231">This property is optional.</span></span> <span data-ttu-id="9f4b6-232">如果您省略這個屬性時，會挑出 hello folderPath 中的所有 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-232">If you omit this property, all hello files from hello folderPath are picked.</span></span> <span data-ttu-id="9f4b6-233">在本教學課程中，只有 hello **input.log**處理。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-233">In this tutorial, only hello **input.log** is processed.</span></span> |
   | <span data-ttu-id="9f4b6-234">類型</span><span class="sxs-lookup"><span data-stu-id="9f4b6-234">type</span></span> |<span data-ttu-id="9f4b6-235">hello 記錄檔都是以文字格式，因此我們使用**TextFormat**。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-235">hello log files are in text format, so we use **TextFormat**.</span></span> |
   | <span data-ttu-id="9f4b6-236">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="9f4b6-236">columnDelimiter</span></span> |<span data-ttu-id="9f4b6-237">hello 記錄檔中的資料行分隔**逗號字元 (`,`)**</span><span class="sxs-lookup"><span data-stu-id="9f4b6-237">columns in hello log files are delimited by **comma character (`,`)**</span></span> |
   | <span data-ttu-id="9f4b6-238">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="9f4b6-238">frequency/interval</span></span> |<span data-ttu-id="9f4b6-239">頻率設定過**月份**和間隔是**1**，這表示該 hello 輸入配量可用每個月。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-239">frequency set too**Month** and interval is **1**, which means that hello input slices are available monthly.</span></span> |
   | <span data-ttu-id="9f4b6-240">external</span><span class="sxs-lookup"><span data-stu-id="9f4b6-240">external</span></span> | <span data-ttu-id="9f4b6-241">這個屬性設定太**true**如果 hello 輸入的資料不會產生此管線。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-241">This property is set too**true** if hello input data is not generated by this pipeline.</span></span> <span data-ttu-id="9f4b6-242">在本教學課程，hello input.log 檔案不會產生這個管線，因此我們設定 hello 屬性 tootrue。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-242">In this tutorial, hello input.log file is not generated by this pipeline, so we set hello property tootrue.</span></span> |

    <span data-ttu-id="9f4b6-243">如需這些 JSON 屬性的詳細資訊，請參閱 [Azure Blob 連接器](data-factory-azure-blob-connector.md#dataset-properties)一文。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-243">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
3. <span data-ttu-id="9f4b6-244">按一下**部署**hello 命令列 toodeploy hello 新建立的資料集上。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-244">Click **Deploy** on hello command bar toodeploy hello newly created dataset.</span></span> <span data-ttu-id="9f4b6-245">您應該會看到 hello hello hello 左側的樹狀檢視中的資料集。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-245">You should see hello dataset in hello tree view on hello left.</span></span>

### <a name="create-output-dataset"></a><span data-ttu-id="9f4b6-246">建立輸出資料集</span><span class="sxs-lookup"><span data-stu-id="9f4b6-246">Create output dataset</span></span>
<span data-ttu-id="9f4b6-247">現在，您可以建立 hello 輸出資料集 toorepresent hello 輸出資料儲存在 hello Azure Blob 儲存體中。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-247">Now, you create hello output dataset toorepresent hello output data stored in hello Azure Blob storage.</span></span>

1. <span data-ttu-id="9f4b6-248">在 hello **Data Factory 編輯器**，按一下  **...多個**hello 命令列上，按一下**新的資料集**，然後選取**Azure Blob 儲存體**。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-248">In hello **Data Factory Editor**, click **... More** on hello command bar, click **New dataset**, and select **Azure Blob storage**.</span></span>  
2. <span data-ttu-id="9f4b6-249">複製並貼上下列程式碼片段 toohello Draft 1 視窗 hello。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-249">Copy and paste hello following snippet toohello Draft-1 window.</span></span> <span data-ttu-id="9f4b6-250">在 hello JSON 片段中，您要建立資料集稱為**AzureBlobOutput**，並指定 hello hello Hive 指令碼所產生的 hello 資料結構。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-250">In hello JSON snippet, you are creating a dataset called **AzureBlobOutput**, and specifying hello structure of hello data that is produced by hello Hive script.</span></span> <span data-ttu-id="9f4b6-251">此外，您可以指定 hello 結果會儲存在稱為 hello blob 容器**adfgetstarted**和 hello 資料夾稱為**partitioneddata**。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-251">In addition, you specify that hello results are stored in hello blob container called **adfgetstarted** and hello folder called **partitioneddata**.</span></span> <span data-ttu-id="9f4b6-252">hello**可用性**區段會指定該 hello 輸出資料集產生每月為基礎。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-252">hello **availability** section specifies that hello output dataset is produced on a monthly basis.</span></span>

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
    <span data-ttu-id="9f4b6-253">請參閱**建立 hello 輸入資料集**> 一節，如需這些屬性的描述。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-253">See **Create hello input dataset** section for descriptions of these properties.</span></span> <span data-ttu-id="9f4b6-254">您未 hello 外部屬性上設定輸出資料集為 hello 資料集由 hello Data Factory 服務所產生。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-254">You do not set hello external property on an output dataset as hello dataset is produced by hello Data Factory service.</span></span>
3. <span data-ttu-id="9f4b6-255">按一下**部署**hello 命令列 toodeploy hello 新建立的資料集上。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-255">Click **Deploy** on hello command bar toodeploy hello newly created dataset.</span></span>
4. <span data-ttu-id="9f4b6-256">確認已成功建立該 hello 資料集。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-256">Verify that hello dataset is created successfully.</span></span>

    ![含連結服務的樹狀檢視](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-data-set.png)

## <a name="create-pipeline"></a><span data-ttu-id="9f4b6-258">建立管線</span><span class="sxs-lookup"><span data-stu-id="9f4b6-258">Create pipeline</span></span>
<span data-ttu-id="9f4b6-259">在此步驟中，您會建立第一個具有 **HDInsightHive** 活動的管線。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-259">In this step, you create your first pipeline with a **HDInsightHive** activity.</span></span> <span data-ttu-id="9f4b6-260">輸入的配量可每月 (頻率： Month、 interval: 1)、 每月產生輸出配量和 hello hello 活動的排程器屬性也設定 toomonthly。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-260">Input slice is available monthly (frequency: Month, interval: 1), output slice is produced monthly, and hello scheduler property for hello activity is also set toomonthly.</span></span> <span data-ttu-id="9f4b6-261">hello 輸出資料集和 hello 活動排程器的 hello 設定必須相符。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-261">hello settings for hello output dataset and hello activity scheduler must match.</span></span> <span data-ttu-id="9f4b6-262">目前，輸出資料集是哪些磁碟機 hello 排程，因此您必須建立輸出資料集，即使 hello 活動不會產生任何輸出。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-262">Currently, output dataset is what drives hello schedule, so you must create an output dataset even if hello activity does not produce any output.</span></span> <span data-ttu-id="9f4b6-263">如果 hello 活動不接受任何輸入，您可以略過建立 hello 輸入資料集。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-263">If hello activity doesn't take any input, you can skip creating hello input dataset.</span></span> <span data-ttu-id="9f4b6-264">hello 下列 JSON 中使用的 hello 內容會說明在 hello 本節結尾處。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-264">hello properties used in hello following JSON are explained at hello end of this section.</span></span>

1. <span data-ttu-id="9f4b6-265">在 hello **Data Factory 編輯器**，按一下 **省略符號 （...）更多指令**，然後按一下**新管線**。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-265">In hello **Data Factory Editor**, click **Ellipsis (…) More commands** and then click **New pipeline**.</span></span>

    ![新增管線按鈕](./media/data-factory-build-your-first-pipeline-using-editor/new-pipeline-button.png)
2. <span data-ttu-id="9f4b6-267">複製並貼上下列程式碼片段 toohello Draft 1 視窗 hello。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-267">Copy and paste hello following snippet toohello Draft-1 window.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="9f4b6-268">取代**storageaccountname** hello hello JSON 中的儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-268">Replace **storageaccountname** with hello name of your storage account in hello JSON.</span></span>
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

    <span data-ttu-id="9f4b6-269">在 hello JSON 片段中，您要建立管線在 HDInsight 叢集使用 Hive tooprocess 資料的活動所組成。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-269">In hello JSON snippet, you are creating a pipeline that consists of a single activity that uses Hive tooprocess Data on an HDInsight cluster.</span></span>

    <span data-ttu-id="9f4b6-270">hello Hive 指令碼檔案， **partitionweblogs.hql**，儲存在 hello Azure 儲存體帳戶 (由 hello scriptLinkedService，稱為**AzureStorageLinkedService**)，然後在**指令碼**hello 容器中的資料夾**adfgetstarted**。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-270">hello Hive script file, **partitionweblogs.hql**, is stored in hello Azure storage account (specified by hello scriptLinkedService, called **AzureStorageLinkedService**), and in **script** folder in hello container **adfgetstarted**.</span></span>

    <span data-ttu-id="9f4b6-271">hello**定義**區段是做為 Hive 組態值傳遞 toohello hive 指令碼使用的 toospecify hello 執行階段設定 (例如 ${hiveconf: inputtable}，{hiveconf:partitionedtable} $)。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-271">hello **defines** section is used toospecify hello runtime settings that are passed toohello hive script as Hive configuration values (e.g ${hiveconf:inputtable}, ${hiveconf:partitionedtable}).</span></span>

    <span data-ttu-id="9f4b6-272">hello**啟動**和**結束**hello 管線屬性指定 hello 之 hello 管線的作用期間。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-272">hello **start** and **end** properties of hello pipeline specifies hello active period of hello pipeline.</span></span>

    <span data-ttu-id="9f4b6-273">在 hello 活動 JSON 中，您指定該 hello Hive 指令碼在上執行指定 hello hello 計算**linkedServiceName** – **HDInsightOnDemandLinkedService**。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-273">In hello activity JSON, you specify that hello Hive script runs on hello compute specified by hello **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="9f4b6-274">請參閱中的"管線 JSON"[管線和 Azure Data Factory 中的活動](data-factory-create-pipelines.md)hello 範例中所使用的 JSON 屬性的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-274">See "Pipeline JSON" in [Pipelines and activities in Azure Data Factory](data-factory-create-pipelines.md) for details about JSON properties used in hello example.</span></span>
   >
   >
3. <span data-ttu-id="9f4b6-275">確認 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="9f4b6-275">Confirm hello following:</span></span>

   1. <span data-ttu-id="9f4b6-276">**input.log**檔案存在於 hello **inputdata**資料夾 hello **adfgetstarted** hello Azure blob 儲存體中的容器</span><span class="sxs-lookup"><span data-stu-id="9f4b6-276">**input.log** file exists in hello **inputdata** folder of hello **adfgetstarted** container in hello Azure blob storage</span></span>
   2. <span data-ttu-id="9f4b6-277">**partitionweblogs.hql**檔案存在於 hello**指令碼**資料夾 hello **adfgetstarted** hello Azure blob 儲存體中的容器。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-277">**partitionweblogs.hql** file exists in hello **script** folder of hello **adfgetstarted** container in hello Azure blob storage.</span></span> <span data-ttu-id="9f4b6-278">完整的 hello 必要條件步驟 hello[教學課程概觀](data-factory-build-your-first-pipeline.md)如果您沒有看到這些檔案。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-278">Complete hello prerequisite steps in hello [Tutorial Overview](data-factory-build-your-first-pipeline.md) if you don't see these files.</span></span>
   3. <span data-ttu-id="9f4b6-279">確認您更換**storageaccountname** hello 您的儲存體帳戶名稱在 hello 與管線 JSON。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-279">Confirm that you replaced **storageaccountname** with hello name of your storage account in hello pipeline JSON.</span></span>
4. <span data-ttu-id="9f4b6-280">按一下**部署**hello 命令列 toodeploy hello 管線。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-280">Click **Deploy** on hello command bar toodeploy hello pipeline.</span></span> <span data-ttu-id="9f4b6-281">因為 hello**啟動**和**結束**次數設定在過去的 hello 和**isPaused**是集 toofalse，hello 管線 （hello 管線中的活動） 執行您部署之後，立即。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-281">Since hello **start** and **end** times are set in hello past and **isPaused** is set toofalse, hello pipeline (activity in hello pipeline) runs immediately after you deploy.</span></span>
5. <span data-ttu-id="9f4b6-282">確認您看到 hello 樹狀檢視中的 hello 管線。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-282">Confirm that you see hello pipeline in hello tree view.</span></span>

    ![管線的樹狀檢視](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-pipeline.png)
6. <span data-ttu-id="9f4b6-284">恭喜，您已經成功建立您的第一個管線！</span><span class="sxs-lookup"><span data-stu-id="9f4b6-284">Congratulations, you have successfully created your first pipeline!</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="9f4b6-285">監視管線</span><span class="sxs-lookup"><span data-stu-id="9f4b6-285">Monitor pipeline</span></span>
### <a name="monitor-pipeline-using-diagram-view"></a><span data-ttu-id="9f4b6-286">使用圖表檢視監視管線</span><span class="sxs-lookup"><span data-stu-id="9f4b6-286">Monitor pipeline using Diagram View</span></span>
1. <span data-ttu-id="9f4b6-287">按一下**X** tooclose Data Factory 編輯器刀鋒 toonavigate 回 toohello Data Factory 刀鋒視窗中，並按一下**圖表**。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-287">Click **X** tooclose Data Factory Editor blades and toonavigate back toohello Data Factory blade, and click **Diagram**.</span></span>

    ![[圖表] 磚](./media/data-factory-build-your-first-pipeline-using-editor/diagram-tile.png)
2. <span data-ttu-id="9f4b6-289">在 hello 圖表檢視，您會看到 hello 管線，以及此教學課程中使用的資料集的總覽。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-289">In hello Diagram View, you see an overview of hello pipelines, and datasets used in this tutorial.</span></span>

    ![圖表檢視](./media/data-factory-build-your-first-pipeline-using-editor/diagram-view-2.png)
3. <span data-ttu-id="9f4b6-291">tooview hello 管線，以滑鼠右鍵按一下管線，在 hello 中的所有活動圖表，然後按一下 開啟管線。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-291">tooview all activities in hello pipeline, right-click pipeline in hello diagram and click Open Pipeline.</span></span>

    ![開啟管線功能表](./media/data-factory-build-your-first-pipeline-using-editor/open-pipeline-menu.png)
4. <span data-ttu-id="9f4b6-293">確認您看到 hello 管線中的 hello HDInsightHive 活動。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-293">Confirm that you see hello HDInsightHive activity in hello pipeline.</span></span>

    ![開啟管線檢視](./media/data-factory-build-your-first-pipeline-using-editor/open-pipeline-view.png)

    <span data-ttu-id="9f4b6-295">toonavigate 回 toohello 前一個檢視中，按一下  **Data factory** hello hello 上方的階層連結功能表中。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-295">toonavigate back toohello previous view, click **Data factory** in hello breadcrumb menu at hello top.</span></span>
5. <span data-ttu-id="9f4b6-296">在 hello**圖表檢視**，按兩下 hello 資料集**AzureBlobInput**。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-296">In hello **Diagram View**, double-click hello dataset **AzureBlobInput**.</span></span> <span data-ttu-id="9f4b6-297">確認該 hello 扇區**準備**狀態。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-297">Confirm that hello slice is in **Ready** state.</span></span> <span data-ttu-id="9f4b6-298">它可能需要幾分鐘的 hello 配量 tooshow 以佔用就緒狀態。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-298">It may take a couple of minutes for hello slice tooshow up in Ready state.</span></span> <span data-ttu-id="9f4b6-299">如果它不會發生您等候一段時間之後，請參閱 < 如果您擁有 hello 輸入的檔 (input.log) 放置在 hello 右容器 (adfgetstarted) 和資料夾 (inputdata)。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-299">If it does not happen after you wait for sometime, see if you have hello input file (input.log) placed in hello right container (adfgetstarted) and folder (inputdata).</span></span>

   ![輸入配量處於就緒狀態](./media/data-factory-build-your-first-pipeline-using-editor/input-slice-ready.png)
6. <span data-ttu-id="9f4b6-301">按一下**X** tooclose **AzureBlobInput**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-301">Click **X** tooclose **AzureBlobInput** blade.</span></span>
7. <span data-ttu-id="9f4b6-302">在 hello**圖表檢視**，按兩下 hello 資料集**AzureBlobOutput**。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-302">In hello **Diagram View**, double-click hello dataset **AzureBlobOutput**.</span></span> <span data-ttu-id="9f4b6-303">您會看到目前正在處理該 hello 扇區。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-303">You see that hello slice that is currently being processed.</span></span>

   ![Dataset](./media/data-factory-build-your-first-pipeline-using-editor/dataset-blade.png)
8. <span data-ttu-id="9f4b6-305">當處理完成時，請參閱中的 hello 扇區**準備**狀態。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-305">When processing is done, you see hello slice in **Ready** state.</span></span>

   ![Dataset](./media/data-factory-build-your-first-pipeline-using-editor/dataset-slice-ready.png)  

   > [!IMPORTANT]
   > <span data-ttu-id="9f4b6-307">建立隨選 HDInsight 叢集通常需要一些時間 (大約 20 分鐘)。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-307">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="9f4b6-308">因此，預期 hello 管線太採取**大約 30 分鐘**tooprocess hello 配量。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-308">Therefore, expect hello pipeline too      take **approximately 30 minutes** tooprocess hello slice.</span></span>
   >
   >

9. <span data-ttu-id="9f4b6-309">當 hello 配量處於**準備**狀態，請檢查 hello **partitioneddata**資料夾中 hello **adfgetstarted** hello 您 blob 儲存體容器中的輸出資料。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-309">When hello slice is in **Ready** state, check hello **partitioneddata** folder in hello **adfgetstarted** container in your blob storage for hello output data.</span></span>  

   ![輸出資料](./media/data-factory-build-your-first-pipeline-using-editor/three-ouptut-files.png)
10. <span data-ttu-id="9f4b6-311">按一下 hello 配量 toosee 詳細資料 中，有關**資料配量**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-311">Click hello slice toosee details about it in a **Data slice** blade.</span></span>

   ![資料配量詳細資料](./media/data-factory-build-your-first-pipeline-using-editor/data-slice-details.png)  
11. <span data-ttu-id="9f4b6-313">按一下在 hello 中執行的活動**活動執行清單**toosee 活動的詳細資料中執行 （在我們的案例的 Hive 活動）**活動執行詳細資料**視窗。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-313">Click an activity run in hello **Activity runs list** toosee details about an activity run (Hive activity in our scenario) in an **Activity run details** window.</span></span>   

   ![活動執行詳細資料](./media/data-factory-build-your-first-pipeline-using-editor/activity-window-blade.png)    

   <span data-ttu-id="9f4b6-315">從 hello 記錄檔，您可以查看上次執行所執行的 hello Hive 查詢和狀態資訊。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-315">From hello log files, you can see hello Hive query that was executed and status information.</span></span> <span data-ttu-id="9f4b6-316">這些記錄檔適合用來排解任何疑難問題。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-316">These logs are useful for troubleshooting any issues.</span></span>
   <span data-ttu-id="9f4b6-317">如需詳細資訊，請參閱 [使用 Azure 入口網站刀鋒視窗監視及管理管線](data-factory-monitor-manage-pipelines.md) 一文。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-317">See [Monitor and manage pipelines using Azure portal blades](data-factory-monitor-manage-pipelines.md) article for more details.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9f4b6-318">已成功處理 hello 配量時，取得刪除 hello 輸入的檔。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-318">hello input file gets deleted when hello slice is processed successfully.</span></span> <span data-ttu-id="9f4b6-319">因此，如果您想 toorerun hello 配量，或不要 hello 教學課程中上, 傳 hello hello adfgetstarted 容器的輸入的檔 (input.log) toohello inputdata 資料夾。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-319">Therefore, if you want toorerun hello slice or do hello tutorial again, upload hello input file (input.log) toohello inputdata folder of hello adfgetstarted container.</span></span>
>
>

### <a name="monitor-pipeline-using-monitor--manage-app"></a><span data-ttu-id="9f4b6-320">使用監視及管理應用程式來監視管線</span><span class="sxs-lookup"><span data-stu-id="9f4b6-320">Monitor pipeline using Monitor & Manage App</span></span>
<span data-ttu-id="9f4b6-321">您也可以使用監視和管理應用程式 toomonitor 您的管線。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-321">You can also use Monitor & Manage application toomonitor your pipelines.</span></span> <span data-ttu-id="9f4b6-322">如需使用此應用程式的詳細資訊，請參閱 [使用監視及管理應用程式來監視和管理 Azure Data Factory 管線](data-factory-monitor-manage-app.md)。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-322">For detailed information about using this application, see [Monitor and manage Azure Data Factory pipelines using Monitoring and Management App](data-factory-monitor-manage-app.md).</span></span>

1. <span data-ttu-id="9f4b6-323">按一下**監視和管理**在您的 data factory 的 hello 首頁上並排顯示。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-323">Click **Monitor & Manage** tile on hello home page for your data factory.</span></span>

    ![監視及管理圖格](./media/data-factory-build-your-first-pipeline-using-editor/monitor-and-manage-tile.png)
2. <span data-ttu-id="9f4b6-325">您應該會看到 [監視及管理] 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-325">You should see **Monitor & Manage application**.</span></span> <span data-ttu-id="9f4b6-326">變更 hello**開始時間**和**結束時間**toomatch 開始和結束時間的管線，然後按一下 **套用**。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-326">Change hello **Start time** and **End time** toomatch start and end times of your pipeline, and click **Apply**.</span></span>

    ![監視及管理應用程式](./media/data-factory-build-your-first-pipeline-using-editor/monitor-and-manage-app.png)
3. <span data-ttu-id="9f4b6-328">選取活動視窗在 hello**活動 Windows** toosee 詳細的清單。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-328">Select an activity window in hello **Activity Windows** list toosee details about it.</span></span>

    ![活動時段詳細資料](./media/data-factory-build-your-first-pipeline-using-editor/activity-window-details.png)

## <a name="summary"></a><span data-ttu-id="9f4b6-330">摘要</span><span class="sxs-lookup"><span data-stu-id="9f4b6-330">Summary</span></span>
<span data-ttu-id="9f4b6-331">在本教學課程中，您可以建立 Azure data factory tooprocess 資料在 HDInsight hadoop 叢集上執行 Hive 指令碼。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-331">In this tutorial, you created an Azure data factory tooprocess data by running Hive script on a HDInsight hadoop cluster.</span></span> <span data-ttu-id="9f4b6-332">您使用 hello Data Factory 編輯器在 hello Azure 入口網站 toodo hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="9f4b6-332">You used hello Data Factory Editor in hello Azure portal toodo hello following steps:</span></span>  

1. <span data-ttu-id="9f4b6-333">建立 Azure **Data Factory**。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-333">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="9f4b6-334">建立兩個 **連結服務**：</span><span class="sxs-lookup"><span data-stu-id="9f4b6-334">Created two **linked services**:</span></span>
   1. <span data-ttu-id="9f4b6-335">**Azure 儲存體**您保留輸入/輸出檔案 toohello 資料處理站的 Azure blob 儲存體連結服務 toolink。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-335">**Azure Storage** linked service toolink your Azure blob storage that holds input/output files toohello data factory.</span></span>
   2. <span data-ttu-id="9f4b6-336">**Azure HDInsight**視連結的服務 toolink 隨 HDInsight Hadoop 叢集 toohello 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-336">**Azure HDInsight** on-demand linked service toolink an on-demand HDInsight Hadoop cluster toohello data factory.</span></span> <span data-ttu-id="9f4b6-337">Azure Data Factory 建立 HDInsight Hadoop 叢集在 just-in-time tooprocess 輸入的資料，並產生輸出資料。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-337">Azure Data Factory creates a HDInsight Hadoop cluster just-in-time tooprocess input data and produce output data.</span></span>
3. <span data-ttu-id="9f4b6-338">建立兩個**資料集**，其中描述輸入和輸出 HDInsight Hive 活動 hello 管線中的資料。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-338">Created two **datasets**, which describe input and output data for HDInsight Hive activity in hello pipeline.</span></span>
4. <span data-ttu-id="9f4b6-339">建立具有 **HDInsight Hive** 活動的**管線**。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-339">Created a **pipeline** with a **HDInsight Hive** activity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9f4b6-340">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9f4b6-340">Next Steps</span></span>
<span data-ttu-id="9f4b6-341">在本文中，您已經建立可在隨選 HDInsight 叢集上執行 Hive 指令碼，含有轉換活動 (HDInsight 活動) 的管線。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-341">In this article, you have created a pipeline with a transformation activity (HDInsight Activity) that runs a Hive script on an on-demand HDInsight cluster.</span></span> <span data-ttu-id="9f4b6-342">如何 toouse 複製活動 toocopy 資料從 Azure Blob tooAzure SQL，請參閱的 toosee[教學課程： 將資料從 Azure blob tooAzure SQL 複製](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-342">toosee how toouse a Copy Activity toocopy data from an Azure Blob tooAzure SQL, see [Tutorial: Copy data from an Azure blob tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="9f4b6-343">另請參閱</span><span class="sxs-lookup"><span data-stu-id="9f4b6-343">See Also</span></span>
| <span data-ttu-id="9f4b6-344">主題</span><span class="sxs-lookup"><span data-stu-id="9f4b6-344">Topic</span></span> | <span data-ttu-id="9f4b6-345">說明</span><span class="sxs-lookup"><span data-stu-id="9f4b6-345">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="9f4b6-346">管線</span><span class="sxs-lookup"><span data-stu-id="9f4b6-346">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="9f4b6-347">這篇文章可協助您了解管線和 Azure Data Factory 中的活動以及 toouse 它們 tooconstruct 端對端資料驅動型工作流程或商務案例。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-347">This article helps you understand pipelines and activities in Azure Data Factory and how toouse them tooconstruct end-to-end data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="9f4b6-348">資料集</span><span class="sxs-lookup"><span data-stu-id="9f4b6-348">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="9f4b6-349">本文協助您了解 Azure Data Factory 中的資料集。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-349">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="9f4b6-350">排程和執行</span><span class="sxs-lookup"><span data-stu-id="9f4b6-350">Scheduling and execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="9f4b6-351">本文說明 Azure Data Factory 應用程式模型的 hello 排程和執行的層面。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-351">This article explains hello scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="9f4b6-352">使用監視應用程式來監視和管理管線</span><span class="sxs-lookup"><span data-stu-id="9f4b6-352">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="9f4b6-353">本文說明如何 toomonitor，管理和偵錯管線使用 hello 監視和管理應用程式。</span><span class="sxs-lookup"><span data-stu-id="9f4b6-353">This article describes how toomonitor, manage, and debug pipelines using hello Monitoring & Management App.</span></span> |
