---
title: "Azure Machine Learning web 服務中的資料匯入/匯出 aaaUsing |Microsoft 文件"
description: "了解如何 toouse hello 資料匯入及匯出資料的模組 toosend 以及從 web 服務接收資料。"
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondlaghaeian
editor: 
ms.assetid: 3a7ac351-ebd3-43a1-8c5d-18223903d08e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/28/2017
ms.author: v-donglo
ms.openlocfilehash: 176380259b15cb338ede61c7f28ba2296b35dd52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploying-azure-ml-web-services-that-use-data-import-and-data-export-modules"></a><span data-ttu-id="47595-103">部署使用資料匯入和資料匯出模組的 Azure ML Web 服務</span><span class="sxs-lookup"><span data-stu-id="47595-103">Deploying Azure ML web services that use Data Import and Data Export modules</span></span>

<span data-ttu-id="47595-104">當您建立預測性實驗時，通常會新增 Web 服務輸入和輸出。</span><span class="sxs-lookup"><span data-stu-id="47595-104">When you create a predictive experiment, you typically add a web service input and output.</span></span> <span data-ttu-id="47595-105">當您部署的 hello 實驗時，取用者可以傳送和接收 hello web 服務透過 hello 輸入和輸出的資料。</span><span class="sxs-lookup"><span data-stu-id="47595-105">When you deploy hello experiment, consumers can send and receive data from hello web service through hello inputs and outputs.</span></span> <span data-ttu-id="47595-106">對於某些應用程式，取用者的資料可能可以從資料摘要獲得，或者資料已經位於外部資料來源 (例如 Azure Blob 儲存體)。</span><span class="sxs-lookup"><span data-stu-id="47595-106">For some applications, a consumer's data may be available from a data feed or already reside in an external data source such as Azure Blob storage.</span></span> <span data-ttu-id="47595-107">在這些情況下，應用程式就不需要使用 Web 服務的輸入和輸出讀取和寫入資料。</span><span class="sxs-lookup"><span data-stu-id="47595-107">In these cases, they do not need read and write data using web service inputs and outputs.</span></span> <span data-ttu-id="47595-108">相反地，他們可以使用 hello 資料來源使用資料匯入模組的 hello 批次執行服務 (BES) tooread 資料並寫入 hello 計分結果使用匯出資料模組 tooa 不同的資料位置。</span><span class="sxs-lookup"><span data-stu-id="47595-108">They can, instead, use hello Batch Execution Service (BES) tooread data from hello data source using an Import Data module and write hello scoring results tooa different data location using an Export Data module.</span></span>

<span data-ttu-id="47595-109">hello 資料匯入和匯出資料模組，可以讀取和寫入 toovarious 資料提供位置，例如透過 HTTP、 Hive 查詢、 Azure SQL database、 Azure 資料表儲存體、 Azure Blob 儲存體，資料摘要的 Web URL 或在內部部署 SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="47595-109">hello Import Data and Export data modules, can read from and write toovarious data locations such as a Web URL via HTTP, a Hive Query, an Azure SQL database, Azure Table storage, Azure Blob storage, a Data Feed provide, or an on-premises SQL database.</span></span>

<span data-ttu-id="47595-110">本主題使用 hello 」 範例 5： 定型、 測試評估二元分類的： 成人資料集 」 範例，並假設 hello 資料集已載入名為 censusdata Azure SQL 資料表。</span><span class="sxs-lookup"><span data-stu-id="47595-110">This topic uses hello "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset" sample and assumes hello dataset has already been loaded into an Azure SQL table named censusdata.</span></span>

## <a name="create-hello-training-experiment"></a><span data-ttu-id="47595-111">建立 hello 定型實驗</span><span class="sxs-lookup"><span data-stu-id="47595-111">Create hello training experiment</span></span>
<span data-ttu-id="47595-112">當您開啟 hello 」 範例 5： 定型、 測試評估二元分類的： 成人資料集 」 範例它使用 hello 範例成人人口普查收入二元分類的資料集。</span><span class="sxs-lookup"><span data-stu-id="47595-112">When you open hello "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset" sample it uses hello sample Adult Census Income Binary Classification dataset.</span></span> <span data-ttu-id="47595-113">和 hello 畫布中的 hello 實驗看起來類似 toohello 下列映像：</span><span class="sxs-lookup"><span data-stu-id="47595-113">And hello experiment in hello canvas will look similar toohello following image:</span></span>

![Hello 實驗初始組態。](./media/machine-learning-web-services-that-use-import-export-modules/initial-look-of-experiment.png)

<span data-ttu-id="47595-115">tooread hello hello Azure SQL 資料表資料：</span><span class="sxs-lookup"><span data-stu-id="47595-115">tooread hello data from hello Azure SQL table:</span></span>

1. <span data-ttu-id="47595-116">刪除 hello 資料集的模組。</span><span class="sxs-lookup"><span data-stu-id="47595-116">Delete hello dataset module.</span></span>
2. <span data-ttu-id="47595-117">在 hello 元件搜尋方塊中，輸入 匯入。</span><span class="sxs-lookup"><span data-stu-id="47595-117">In hello components search box, type import.</span></span>
3. <span data-ttu-id="47595-118">從 hello 結果清單中，加入*匯入資料*模組 toohello 實驗畫布。</span><span class="sxs-lookup"><span data-stu-id="47595-118">From hello results list, add an *Import Data* module toohello experiment canvas.</span></span>
4. <span data-ttu-id="47595-119">Hello 輸出連接*匯入資料*模組 hello 輸入的 hello*清除遺漏資料*模組。</span><span class="sxs-lookup"><span data-stu-id="47595-119">Connect output of hello *Import Data* module hello input of hello *Clean Missing Data* module.</span></span>
5. <span data-ttu-id="47595-120">在 屬性 窗格中，選取  **Azure SQL Database**在 hello**資料來源**下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="47595-120">In properties pane, select **Azure SQL Database** in hello **Data Source** dropdown.</span></span>
6. <span data-ttu-id="47595-121">在 hello**資料庫伺服器名稱**，**資料庫名稱**，**使用者名稱**，和**密碼**欄位中，輸入 hello 適當資訊您的資料庫。</span><span class="sxs-lookup"><span data-stu-id="47595-121">In hello **Database server name**, **Database name**, **User name**, and **Password** fields, enter hello appropriate information for your database.</span></span>
7. <span data-ttu-id="47595-122">在 hello 資料庫查詢欄位中，輸入下列查詢的 hello。</span><span class="sxs-lookup"><span data-stu-id="47595-122">In hello Database query field, enter hello following query.</span></span>
   
     <span data-ttu-id="47595-123">select [age],</span><span class="sxs-lookup"><span data-stu-id="47595-123">select [age],</span></span>
   
        [workclass],
        [fnlwgt],
        [education],
        [education-num],
        [marital-status],
        [occupation],
        [relationship],
        [race],
        [sex],
        [capital-gain],
        [capital-loss],
        [hours-per-week],
        [native-country],
        [income]
     <span data-ttu-id="47595-124">from dbo.censusdata;</span><span class="sxs-lookup"><span data-stu-id="47595-124">from dbo.censusdata;</span></span>
8. <span data-ttu-id="47595-125">在 hello hello 實驗畫布底部，按一下 **執行**。</span><span class="sxs-lookup"><span data-stu-id="47595-125">At hello bottom of hello experiment canvas, click **Run**.</span></span>

## <a name="create-hello-predictive-experiment"></a><span data-ttu-id="47595-126">建立 hello 預測實驗</span><span class="sxs-lookup"><span data-stu-id="47595-126">Create hello predictive experiment</span></span>
<span data-ttu-id="47595-127">接下來您將設定 hello 預測的實驗，您用來部署您的 web 服務。</span><span class="sxs-lookup"><span data-stu-id="47595-127">Next you set up hello predictive experiment from which you deploy your web service.</span></span>

1. <span data-ttu-id="47595-128">在 hello hello 實驗畫布底部，按一下 **設定 Web 服務**選取**預測 Web 服務 [建議]**。</span><span class="sxs-lookup"><span data-stu-id="47595-128">At hello bottom of hello experiment canvas, click **Set Up Web Service** and select **Predictive Web Service [Recommended]**.</span></span>
2. <span data-ttu-id="47595-129">移除 hello *Web 服務輸出*和*Web 服務輸出模組*從 hello 預測實驗。</span><span class="sxs-lookup"><span data-stu-id="47595-129">Remove hello *Web Service Input* and *Web Service Output modules* from hello predictive experiment.</span></span> 
3. <span data-ttu-id="47595-130">在 hello 元件搜尋方塊中，輸入匯出。</span><span class="sxs-lookup"><span data-stu-id="47595-130">In hello components search box, type export.</span></span>
4. <span data-ttu-id="47595-131">從 hello 結果清單中，加入*匯出資料*模組 toohello 實驗畫布。</span><span class="sxs-lookup"><span data-stu-id="47595-131">From hello results list, add an *Export Data* module toohello experiment canvas.</span></span>
5. <span data-ttu-id="47595-132">Hello 輸出連接*計分模型*模組 hello 輸入的 hello*匯出資料*模組。</span><span class="sxs-lookup"><span data-stu-id="47595-132">Connect output of hello *Score Model* module hello input of hello *Export Data* module.</span></span> 
6. <span data-ttu-id="47595-133">在 屬性 窗格中，選取  **Azure SQL Database** hello 資料目的地的下拉式清單中。</span><span class="sxs-lookup"><span data-stu-id="47595-133">In properties pane, select **Azure SQL Database** in hello data destination dropdown.</span></span>
7. <span data-ttu-id="47595-134">在 hello**資料庫伺服器名稱**，**資料庫名稱**，**伺服器使用者帳戶名稱**，和**伺服器使用者帳戶密碼**欄位中，輸入hello 適當資料庫的資訊。</span><span class="sxs-lookup"><span data-stu-id="47595-134">In hello **Database server name**, **Database name**, **Server user account name**, and **Server user account password** fields, enter hello appropriate information for your database.</span></span>
8. <span data-ttu-id="47595-135">在 hello**以逗號分隔的清單儲存的資料行 toobe**欄位中，輸入計分標籤。</span><span class="sxs-lookup"><span data-stu-id="47595-135">In hello **Comma separated list of columns toobe saved** field, type Scored Labels.</span></span>
9. <span data-ttu-id="47595-136">在 [hello**資料的資料表名稱] 欄位**，輸入 dbo。ScoredLabels。</span><span class="sxs-lookup"><span data-stu-id="47595-136">In hello **Data table name field**, type dbo.ScoredLabels.</span></span> <span data-ttu-id="47595-137">如果 hello 資料表不存在，則會建立執行 hello 實驗或呼叫 hello web 服務時。</span><span class="sxs-lookup"><span data-stu-id="47595-137">If hello table does not exist, it is created when hello experiment is run or hello web service is called.</span></span>
10. <span data-ttu-id="47595-138">在 hello**以逗號分隔的 datatable 資料行清單**欄位中，輸入 ScoredLabels。</span><span class="sxs-lookup"><span data-stu-id="47595-138">In hello **Comma separated list of datatable columns** field, type ScoredLabels.</span></span>

<span data-ttu-id="47595-139">當您撰寫應用程式呼叫 hello 最終的 web 服務時，您可能想 toospecify 不同的輸入的查詢或目的地資料表在執行階段。</span><span class="sxs-lookup"><span data-stu-id="47595-139">When you write an application that calls hello final web service, you may want toospecify a different input query or destination table at run time.</span></span> <span data-ttu-id="47595-140">tooconfigure 這些輸入和輸出，請使用 hello Web 服務參數功能 tooset hello*匯入資料*模組*資料來源*屬性和 hello*匯出資料*模式資料目的地屬性。</span><span class="sxs-lookup"><span data-stu-id="47595-140">tooconfigure these inputs and outputs, use hello Web Service Parameters feature tooset hello *Import Data* module *Data source* property and hello *Export Data* mode data destination property.</span></span>  <span data-ttu-id="47595-141">如需有關 Web 服務參數的詳細資訊，請參閱 hello [AzureML Web 服務參數項目](https://blogs.technet.microsoft.com/machinelearning/2014/11/25/azureml-web-service-parameters/)hello Cortana 智慧和機器學習部落格上。</span><span class="sxs-lookup"><span data-stu-id="47595-141">For more information on Web Service Parameters, see hello [AzureML Web Service Parameters entry](https://blogs.technet.microsoft.com/machinelearning/2014/11/25/azureml-web-service-parameters/) on hello Cortana Intelligence and Machine Learning Blog.</span></span>

<span data-ttu-id="47595-142">hello 匯入查詢 hello 目的地資料表的 tooconfigure hello Web 服務參數：</span><span class="sxs-lookup"><span data-stu-id="47595-142">tooconfigure hello Web Service Parameters for hello import query and hello destination table:</span></span>

1. <span data-ttu-id="47595-143">Hello hello 屬性 窗格中*匯入資料*模組中，按一下 hello hello 圖示右上角的 hello**資料庫查詢**欄位，然後選取**設定為 web 服務參數**。</span><span class="sxs-lookup"><span data-stu-id="47595-143">In hello properties pane for hello *Import Data* module, click hello icon at hello top right of hello **Database query** field and select **Set as web service parameter**.</span></span>
2. <span data-ttu-id="47595-144">Hello hello 屬性 窗格中*匯出資料*模組中，按一下 hello hello 圖示右上角的 hello**資料表名稱**欄位，然後選取**設定為 web 服務參數**。</span><span class="sxs-lookup"><span data-stu-id="47595-144">In hello properties pane for hello *Export Data* module, click hello icon at hello top right of hello **Data table name** field and select **Set as web service parameter**.</span></span>
3. <span data-ttu-id="47595-145">在 hello 底部 hello*匯出資料*模組屬性] 窗格中 hello **Web 服務參數**區段中，按一下 [查詢資料庫並將它重新命名查詢。</span><span class="sxs-lookup"><span data-stu-id="47595-145">At hello bottom of hello *Export Data* module properties pane, in hello **Web Service Parameters** section, click Database query and rename it Query.</span></span>
4. <span data-ttu-id="47595-146">按一下 [資料表名稱] 並將它重新命名為**資料表**。</span><span class="sxs-lookup"><span data-stu-id="47595-146">Click **Data table name** and rename it **Table**.</span></span>

<span data-ttu-id="47595-147">當您完成之後時，您的經驗看起來應該類似 toohello 下列映像：</span><span class="sxs-lookup"><span data-stu-id="47595-147">When you are done, your experiment should look similar toohello following image:</span></span>

![實驗的最終外觀。](./media/machine-learning-web-services-that-use-import-export-modules/experiment-with-import-data-added.png)

<span data-ttu-id="47595-149">現在您可以為 web 服務部署 hello 實驗。</span><span class="sxs-lookup"><span data-stu-id="47595-149">Now you can deploy hello experiment as a web service.</span></span>

## <a name="deploy-hello-web-service"></a><span data-ttu-id="47595-150">部署 hello web 服務</span><span class="sxs-lookup"><span data-stu-id="47595-150">Deploy hello web service</span></span>
<span data-ttu-id="47595-151">您可以部署 tooeither 傳統 」 或 「 新增 web 服務。</span><span class="sxs-lookup"><span data-stu-id="47595-151">You can deploy tooeither a Classic or New web service.</span></span>

### <a name="deploy-a-classic-web-service"></a><span data-ttu-id="47595-152">部署傳統 Web 服務</span><span class="sxs-lookup"><span data-stu-id="47595-152">Deploy a Classic Web Service</span></span>
<span data-ttu-id="47595-153">toodeploy 為傳統的 Web 服務，並建立應用程式 tooconsume 它：</span><span class="sxs-lookup"><span data-stu-id="47595-153">toodeploy as a Classic Web Service and create an application tooconsume it:</span></span>

1. <span data-ttu-id="47595-154">在 hello hello 實驗畫布底部，按一下 [執行]。</span><span class="sxs-lookup"><span data-stu-id="47595-154">At hello bottom of hello experiment canvas, click Run.</span></span>
2. <span data-ttu-id="47595-155">Hello 執行完成後，按一下**部署 Web 服務**選取**部署 Web 服務 [傳統]**。</span><span class="sxs-lookup"><span data-stu-id="47595-155">When hello run has completed, click **Deploy Web Service** and select **Deploy Web Service [Classic]**.</span></span>
3. <span data-ttu-id="47595-156">在 hello web 服務儀表板，找到您的 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="47595-156">On hello web service dashboard, locate your API key.</span></span> <span data-ttu-id="47595-157">複製並儲存它 toouse 更新版本。</span><span class="sxs-lookup"><span data-stu-id="47595-157">Copy and save it toouse later.</span></span>
4. <span data-ttu-id="47595-158">在 hello**預設端點**資料表中，按一下 hello**批次執行**連結 tooopen hello API 說明頁面。</span><span class="sxs-lookup"><span data-stu-id="47595-158">In hello **Default Endpoint** table, click hello **Batch Execution** link tooopen hello API Help Page.</span></span>
5. <span data-ttu-id="47595-159">在 Visual Studio 中建立 C# 主控台應用程式：[新增] > [專案] > [Visual C#] > [Windows 傳統桌面] > [主控台應用程式 (.NET Framework)]。</span><span class="sxs-lookup"><span data-stu-id="47595-159">In Visual Studio, create a C# console application: **New** > **Project** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
6. <span data-ttu-id="47595-160">在 hello API 說明頁面，尋找 hello**範例程式碼**在 hello hello 頁面底部的區段。</span><span class="sxs-lookup"><span data-stu-id="47595-160">On hello API Help Page, find hello **Sample Code** section at hello bottom of hello page.</span></span>
7. <span data-ttu-id="47595-161">複製並貼入 hello C# 範例程式碼 Program.cs 檔案中，然後移除所有參考 toohello blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="47595-161">Copy and paste hello C# sample code into your Program.cs file, and remove all references toohello blob storage.</span></span>
8. <span data-ttu-id="47595-162">更新 hello hello 值*apiKey*變數使用稍早儲存的 hello API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="47595-162">Update hello value of hello *apiKey* variable with hello API key saved earlier.</span></span>
9. <span data-ttu-id="47595-163">找出 hello 要求宣告和更新 hello 的 Web 服務參數值會傳遞 toohello*匯入資料*和*匯出資料*模組。</span><span class="sxs-lookup"><span data-stu-id="47595-163">Locate hello request declaration and update hello values of Web Service Parameters that are passed toohello *Import Data* and *Export Data* modules.</span></span> <span data-ttu-id="47595-164">在此情況下，您會使用 hello 原始查詢，但定義新的資料表名稱。</span><span class="sxs-lookup"><span data-stu-id="47595-164">In this case, you use hello original query, but define a new table name.</span></span>
   
        var request = new BatchExecutionRequest() 
        {           
            GlobalParameters = new Dictionary<string, string>() {
                { "Query", @"select [age], [workclass], [fnlwgt], [education], [education-num], [marital-status], [occupation], [relationship], [race], [sex], [capital-gain], [capital-loss], [hours-per-week], [native-country], [income] from dbo.censusdata" },
                { "Table", "dbo.ScoredTable2" },
            }
        };
10. <span data-ttu-id="47595-165">執行 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="47595-165">Run hello application.</span></span> 

<span data-ttu-id="47595-166">Hello 執行完成時，新的資料表會加入包含 hello 計分結果 toohello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="47595-166">On completion of hello run, a new table is added toohello database containing hello scoring results.</span></span>

### <a name="deploy-a-new-web-service"></a><span data-ttu-id="47595-167">部署新的 Web 服務</span><span class="sxs-lookup"><span data-stu-id="47595-167">Deploy a New Web Service</span></span>

> [!NOTE] 
> <span data-ttu-id="47595-168">toodeploy 新的 web 服務，您必須擁有足夠的權限 hello 訂用帳戶 toowhich 您部署 hello web 服務。</span><span class="sxs-lookup"><span data-stu-id="47595-168">toodeploy a New web service you must have sufficient permissions in hello subscription toowhich you deploying hello web service.</span></span> <span data-ttu-id="47595-169">如需詳細資訊，請參閱[管理 Web 服務使用 hello Azure 機器學習 Web 服務網站](machine-learning-manage-new-webservice.md)。</span><span class="sxs-lookup"><span data-stu-id="47595-169">For more information, see [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="47595-170">toodeploy 做為新的 Web 服務，並建立應用程式 tooconsume 它：</span><span class="sxs-lookup"><span data-stu-id="47595-170">toodeploy as a New Web Service and create an application tooconsume it:</span></span>

1. <span data-ttu-id="47595-171">在 hello hello 實驗畫布底部，按一下 **執行**。</span><span class="sxs-lookup"><span data-stu-id="47595-171">At hello bottom of hello experiment canvas, click **Run**.</span></span>
2. <span data-ttu-id="47595-172">Hello 執行完成後，按一下**部署 Web 服務**選取**部署 Web 服務 [New]**。</span><span class="sxs-lookup"><span data-stu-id="47595-172">When hello run has completed, click **Deploy Web Service** and select **Deploy Web Service [New]**.</span></span>
3. <span data-ttu-id="47595-173">Hello 部署實驗頁面上，輸入您的 web 服務的名稱並選取定價方案，然後按一下**部署**。</span><span class="sxs-lookup"><span data-stu-id="47595-173">On hello Deploy Experiment page, enter a name for your web service, and select a pricing plan, then click **Deploy**.</span></span>
4. <span data-ttu-id="47595-174">在 hello**快速入門**頁面上，按一下**取用**。</span><span class="sxs-lookup"><span data-stu-id="47595-174">On hello **Quickstart** page, click **Consume**.</span></span>
5. <span data-ttu-id="47595-175">在 hello**範例程式碼**區段中，按一下**批次**。</span><span class="sxs-lookup"><span data-stu-id="47595-175">In hello **Sample Code** section, click **Batch**.</span></span>
6. <span data-ttu-id="47595-176">在 Visual Studio 中建立 C# 主控台應用程式：[新增] > [專案] > [Visual C#] > [Windows 傳統桌面] > [主控台應用程式 (.NET Framework)]。</span><span class="sxs-lookup"><span data-stu-id="47595-176">In Visual Studio, create a C# console application: **New** > **Project** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
7. <span data-ttu-id="47595-177">複製並貼入您 Program.cs 檔案中的 hello C# 範例程式碼。</span><span class="sxs-lookup"><span data-stu-id="47595-177">Copy and paste hello C# sample code into your Program.cs file.</span></span>
8. <span data-ttu-id="47595-178">更新 hello hello 值*apiKey*變數以 hello**主索引鍵**位於 hello**基本耗用量資訊**> 一節。</span><span class="sxs-lookup"><span data-stu-id="47595-178">Update hello value of hello *apiKey* variable with hello **Primary Key** located in hello **Basic consumption info** section.</span></span>
9. <span data-ttu-id="47595-179">找出 hello *scoreRequest*宣告和更新的 Web 服務參數傳遞 toohello hello 值*匯入資料*和*匯出資料*模組。</span><span class="sxs-lookup"><span data-stu-id="47595-179">Locate hello *scoreRequest* declaration and update hello values of Web Service Parameters that are passed toohello *Import Data* and *Export Data* modules.</span></span> <span data-ttu-id="47595-180">在此情況下，您會使用 hello 原始查詢，但定義新的資料表名稱。</span><span class="sxs-lookup"><span data-stu-id="47595-180">In this case, you use hello original query, but define a new table name.</span></span>
   
        var scoreRequest = new
        {       
            Inputs = new Dictionary<string, StringTable>()
            {
            },
            GlobalParameters = new Dictionary<string, string>() {
                { "Query", @"select [age], [workclass], [fnlwgt], [education], [education-num], [marital-status], [occupation], [relationship], [race], [sex], [capital-gain], [capital-loss], [hours-per-week], [native-country], [income] from dbo.censusdata" },
                { "Table", "dbo.ScoredTable3" },
            }
        };
10. <span data-ttu-id="47595-181">執行 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="47595-181">Run hello application.</span></span> 

