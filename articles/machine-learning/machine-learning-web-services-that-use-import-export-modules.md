---
title: "在 Azure Machine Learning Web 服務中使用匯入/匯出資料 | Microsoft Docs"
description: "了解如何使用「匯入資料」及「匯出資料」模組來傳送和接收 Web 服務的資料。"
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
ms.openlocfilehash: 123c8c2b1c5bae268b2a61c185743f2c3920175e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="deploying-azure-ml-web-services-that-use-data-import-and-data-export-modules"></a><span data-ttu-id="090aa-103">部署使用資料匯入和資料匯出模組的 Azure ML Web 服務</span><span class="sxs-lookup"><span data-stu-id="090aa-103">Deploying Azure ML web services that use Data Import and Data Export modules</span></span>

<span data-ttu-id="090aa-104">當您建立預測性實驗時，通常會新增 Web 服務輸入和輸出。</span><span class="sxs-lookup"><span data-stu-id="090aa-104">When you create a predictive experiment, you typically add a web service input and output.</span></span> <span data-ttu-id="090aa-105">當您部署實驗時，取用者可以透過輸入和輸出傳送和接收 Web 服務的資料。</span><span class="sxs-lookup"><span data-stu-id="090aa-105">When you deploy the experiment, consumers can send and receive data from the web service through the inputs and outputs.</span></span> <span data-ttu-id="090aa-106">對於某些應用程式，取用者的資料可能可以從資料摘要獲得，或者資料已經位於外部資料來源 (例如 Azure Blob 儲存體)。</span><span class="sxs-lookup"><span data-stu-id="090aa-106">For some applications, a consumer's data may be available from a data feed or already reside in an external data source such as Azure Blob storage.</span></span> <span data-ttu-id="090aa-107">在這些情況下，應用程式就不需要使用 Web 服務的輸入和輸出讀取和寫入資料。</span><span class="sxs-lookup"><span data-stu-id="090aa-107">In these cases, they do not need read and write data using web service inputs and outputs.</span></span> <span data-ttu-id="090aa-108">而是可以改用「批次執行服務 (BES)」使用「匯入資料」模組從資料來源讀取資料，然後使用「匯出資料」模組將評分結果寫入不同的資料位置。</span><span class="sxs-lookup"><span data-stu-id="090aa-108">They can, instead, use the Batch Execution Service (BES) to read data from the data source using an Import Data module and write the scoring results to a different data location using an Export Data module.</span></span>

<span data-ttu-id="090aa-109">「匯入資料」和「匯出資料」模組可以讀取和寫入各種資料位置，例如，透過 HTTP 的 Web URL、Hive 查詢、Azure SQL Database、Azure 表格儲存體、Azure Blob 儲存體、資料摘要提供或內部部署的 SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="090aa-109">The Import Data and Export data modules, can read from and write to various data locations such as a Web URL via HTTP, a Hive Query, an Azure SQL database, Azure Table storage, Azure Blob storage, a Data Feed provide, or an on-premises SQL database.</span></span>

<span data-ttu-id="090aa-110">本主題使用「範例 5︰二進位分類的訓練、測試、評估︰成人資料集」範例，並假設資料集已載入名為 censusdata 的 Azure SQL 資料表。</span><span class="sxs-lookup"><span data-stu-id="090aa-110">This topic uses the "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset" sample and assumes the dataset has already been loaded into an Azure SQL table named censusdata.</span></span>

## <a name="create-the-training-experiment"></a><span data-ttu-id="090aa-111">建立訓練實驗</span><span class="sxs-lookup"><span data-stu-id="090aa-111">Create the training experiment</span></span>
<span data-ttu-id="090aa-112">當您開啟「範例 5︰二進位分類的訓練、測試、評估︰成人資料集」範例時，它會使用範例「成人收入普查二進位分類」資料集。</span><span class="sxs-lookup"><span data-stu-id="090aa-112">When you open the "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset" sample it uses the sample Adult Census Income Binary Classification dataset.</span></span> <span data-ttu-id="090aa-113">畫布中的實驗看起來類似下圖：</span><span class="sxs-lookup"><span data-stu-id="090aa-113">And the experiment in the canvas will look similar to the following image:</span></span>

![實驗的初始組態。](./media/machine-learning-web-services-that-use-import-export-modules/initial-look-of-experiment.png)

<span data-ttu-id="090aa-115">從 Azure SQL 資料表讀取資料︰</span><span class="sxs-lookup"><span data-stu-id="090aa-115">To read the data from the Azure SQL table:</span></span>

1. <span data-ttu-id="090aa-116">刪除資料集模組。</span><span class="sxs-lookup"><span data-stu-id="090aa-116">Delete the dataset module.</span></span>
2. <span data-ttu-id="090aa-117">在元件搜尋方塊中，輸入「匯入」。</span><span class="sxs-lookup"><span data-stu-id="090aa-117">In the components search box, type import.</span></span>
3. <span data-ttu-id="090aa-118">從結果清單中，將「匯入資料」  模組加入實驗畫布。</span><span class="sxs-lookup"><span data-stu-id="090aa-118">From the results list, add an *Import Data* module to the experiment canvas.</span></span>
4. <span data-ttu-id="090aa-119">連接「匯入資料」模組的輸出與「清除遺漏的資料」模組的輸入。</span><span class="sxs-lookup"><span data-stu-id="090aa-119">Connect output of the *Import Data* module the input of the *Clean Missing Data* module.</span></span>
5. <span data-ttu-id="090aa-120">在屬性窗格中，在 [資料來源]  in the  。</span><span class="sxs-lookup"><span data-stu-id="090aa-120">In properties pane, select **Azure SQL Database** in the **Data Source** dropdown.</span></span>
6. <span data-ttu-id="090aa-121">在 [資料庫伺服器名稱]、[資料庫名稱]、[使用者名稱] 和 [密碼] 欄位中，輸入資料庫的適當資訊。</span><span class="sxs-lookup"><span data-stu-id="090aa-121">In the **Database server name**, **Database name**, **User name**, and **Password** fields, enter the appropriate information for your database.</span></span>
7. <span data-ttu-id="090aa-122">在資料庫查詢欄位中，輸入下列查詢。</span><span class="sxs-lookup"><span data-stu-id="090aa-122">In the Database query field, enter the following query.</span></span>
   
     <span data-ttu-id="090aa-123">select [age],</span><span class="sxs-lookup"><span data-stu-id="090aa-123">select [age],</span></span>
   
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
     <span data-ttu-id="090aa-124">from dbo.censusdata;</span><span class="sxs-lookup"><span data-stu-id="090aa-124">from dbo.censusdata;</span></span>
8. <span data-ttu-id="090aa-125">在實驗畫布底端，按一下 [執行] 。</span><span class="sxs-lookup"><span data-stu-id="090aa-125">At the bottom of the experiment canvas, click **Run**.</span></span>

## <a name="create-the-predictive-experiment"></a><span data-ttu-id="090aa-126">建立預測性實驗</span><span class="sxs-lookup"><span data-stu-id="090aa-126">Create the predictive experiment</span></span>
<span data-ttu-id="090aa-127">接著，您要設定用來部署 Web 服務的預測性實驗。</span><span class="sxs-lookup"><span data-stu-id="090aa-127">Next you set up the predictive experiment from which you deploy your web service.</span></span>

1. <span data-ttu-id="090aa-128">在實驗畫布底端，按一下 [設定 Web 服務]，然後選取 [預測性 Web 服務 [建議]]。</span><span class="sxs-lookup"><span data-stu-id="090aa-128">At the bottom of the experiment canvas, click **Set Up Web Service** and select **Predictive Web Service [Recommended]**.</span></span>
2. <span data-ttu-id="090aa-129">從預測性實驗移除「Web 服務輸入」和「Web 服務輸出」模組。</span><span class="sxs-lookup"><span data-stu-id="090aa-129">Remove the *Web Service Input* and *Web Service Output modules* from the predictive experiment.</span></span> 
3. <span data-ttu-id="090aa-130">在元件搜尋方塊中，輸入「匯出」。</span><span class="sxs-lookup"><span data-stu-id="090aa-130">In the components search box, type export.</span></span>
4. <span data-ttu-id="090aa-131">從結果清單中，將「匯出資料」  模組加入實驗畫布。</span><span class="sxs-lookup"><span data-stu-id="090aa-131">From the results list, add an *Export Data* module to the experiment canvas.</span></span>
5. <span data-ttu-id="090aa-132">連接「評分模型」模組的輸出與「匯出資料」模組的輸入。</span><span class="sxs-lookup"><span data-stu-id="090aa-132">Connect output of the *Score Model* module the input of the *Export Data* module.</span></span> 
6. <span data-ttu-id="090aa-133">在屬性窗格中，在資料目的地下拉式清單中選取 [Azure SQL Database]  。</span><span class="sxs-lookup"><span data-stu-id="090aa-133">In properties pane, select **Azure SQL Database** in the data destination dropdown.</span></span>
7. <span data-ttu-id="090aa-134">在 [資料庫伺服器名稱]、[資料庫名稱]、[伺服器使用者帳戶名稱] 和 [伺服器使用者帳戶密碼] 欄位中，輸入資料庫的適當資訊。</span><span class="sxs-lookup"><span data-stu-id="090aa-134">In the **Database server name**, **Database name**, **Server user account name**, and **Server user account password** fields, enter the appropriate information for your database.</span></span>
8. <span data-ttu-id="090aa-135">在 [要儲存的資料行逗號分隔清單]  欄位中，輸入「評分標籤」。</span><span class="sxs-lookup"><span data-stu-id="090aa-135">In the **Comma separated list of columns to be saved** field, type Scored Labels.</span></span>
9. <span data-ttu-id="090aa-136">在 [資料表名稱] 欄位中，輸入 dbo.ScoredLabels。</span><span class="sxs-lookup"><span data-stu-id="090aa-136">In the **Data table name field**, type dbo.ScoredLabels.</span></span> <span data-ttu-id="090aa-137">如果資料表不存在，則在執行實驗或呼叫 Web 服務時會建立資料表。</span><span class="sxs-lookup"><span data-stu-id="090aa-137">If the table does not exist, it is created when the experiment is run or the web service is called.</span></span>
10. <span data-ttu-id="090aa-138">在 [資料表資料行的逗號分隔清單]  欄位中，輸入 ScoredLabels。</span><span class="sxs-lookup"><span data-stu-id="090aa-138">In the **Comma separated list of datatable columns** field, type ScoredLabels.</span></span>

<span data-ttu-id="090aa-139">當您撰寫的應用程式呼叫最後一個 Web 服務時，您可能要在執行階段指定不同的輸入查詢或目的地資料表。</span><span class="sxs-lookup"><span data-stu-id="090aa-139">When you write an application that calls the final web service, you may want to specify a different input query or destination table at run time.</span></span> <span data-ttu-id="090aa-140">若要設定這些輸入和輸出，請使用 Web 服務參數功能設來定「匯入資料」模組的「資料來源」屬性以及「匯出資料」模式資料目的地屬性。</span><span class="sxs-lookup"><span data-stu-id="090aa-140">To configure these inputs and outputs, use the Web Service Parameters feature to set the *Import Data* module *Data source* property and the *Export Data* mode data destination property.</span></span>  <span data-ttu-id="090aa-141">如需有關 Web 服務參數的詳細資訊，請參閱 Cortana Intelligence and Machine Learning Blog (Cortana 智慧與機器學習部落格) 上的 [AzureML Web Service Parameters (AzureML Web 服務參數)](https://blogs.technet.microsoft.com/machinelearning/2014/11/25/azureml-web-service-parameters/) 。</span><span class="sxs-lookup"><span data-stu-id="090aa-141">For more information on Web Service Parameters, see the [AzureML Web Service Parameters entry](https://blogs.technet.microsoft.com/machinelearning/2014/11/25/azureml-web-service-parameters/) on the Cortana Intelligence and Machine Learning Blog.</span></span>

<span data-ttu-id="090aa-142">設定匯入查詢和目的地資料表的 Web 服務參數︰</span><span class="sxs-lookup"><span data-stu-id="090aa-142">To configure the Web Service Parameters for the import query and the destination table:</span></span>

1. <span data-ttu-id="090aa-143">在「匯入資料」模組的屬性窗格中，按一下 [資料庫查詢] 欄位右上角的圖示，然後選取 [設為 Web 服務參數]。</span><span class="sxs-lookup"><span data-stu-id="090aa-143">In the properties pane for the *Import Data* module, click the icon at the top right of the **Database query** field and select **Set as web service parameter**.</span></span>
2. <span data-ttu-id="090aa-144">在「匯出資料」模組的屬性窗格中，按一下 [資料表名稱] 欄位右上角的圖示，然後選取 [設為 Web 服務參數]。</span><span class="sxs-lookup"><span data-stu-id="090aa-144">In the properties pane for the *Export Data* module, click the icon at the top right of the **Data table name** field and select **Set as web service parameter**.</span></span>
3. <span data-ttu-id="090aa-145">在「匯出資料」模組屬性窗格的底部，在 [Web 服務參數] 區段中，按一下 [資料庫查詢] 並將它重新命名為「查詢」。</span><span class="sxs-lookup"><span data-stu-id="090aa-145">At the bottom of the *Export Data* module properties pane, in the **Web Service Parameters** section, click Database query and rename it Query.</span></span>
4. <span data-ttu-id="090aa-146">按一下 [資料表名稱] 並將它重新命名為**資料表**。</span><span class="sxs-lookup"><span data-stu-id="090aa-146">Click **Data table name** and rename it **Table**.</span></span>

<span data-ttu-id="090aa-147">完成之後，您的實驗看起來應該類似下圖：</span><span class="sxs-lookup"><span data-stu-id="090aa-147">When you are done, your experiment should look similar to the following image:</span></span>

![實驗的最終外觀。](./media/machine-learning-web-services-that-use-import-export-modules/experiment-with-import-data-added.png)

<span data-ttu-id="090aa-149">您現在可以將實驗部署為 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="090aa-149">Now you can deploy the experiment as a web service.</span></span>

## <a name="deploy-the-web-service"></a><span data-ttu-id="090aa-150">部署 Web 服務</span><span class="sxs-lookup"><span data-stu-id="090aa-150">Deploy the web service</span></span>
<span data-ttu-id="090aa-151">您可以部署到傳統或新的 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="090aa-151">You can deploy to either a Classic or New web service.</span></span>

### <a name="deploy-a-classic-web-service"></a><span data-ttu-id="090aa-152">部署傳統 Web 服務</span><span class="sxs-lookup"><span data-stu-id="090aa-152">Deploy a Classic Web Service</span></span>
<span data-ttu-id="090aa-153">若要部署為傳統 Web 服務，並建立應用程式取用它︰</span><span class="sxs-lookup"><span data-stu-id="090aa-153">To deploy as a Classic Web Service and create an application to consume it:</span></span>

1. <span data-ttu-id="090aa-154">在實驗畫布底端，按一下 [執行]。</span><span class="sxs-lookup"><span data-stu-id="090aa-154">At the bottom of the experiment canvas, click Run.</span></span>
2. <span data-ttu-id="090aa-155">執行完成時，按一下 [部署 Web 服務]，然後選取 [部署 Web 服務 [傳統]]。</span><span class="sxs-lookup"><span data-stu-id="090aa-155">When the run has completed, click **Deploy Web Service** and select **Deploy Web Service [Classic]**.</span></span>
3. <span data-ttu-id="090aa-156">在 Web 服務儀表板上，找出您的 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="090aa-156">On the web service dashboard, locate your API key.</span></span> <span data-ttu-id="090aa-157">複製並儲存起來供日後使用。</span><span class="sxs-lookup"><span data-stu-id="090aa-157">Copy and save it to use later.</span></span>
4. <span data-ttu-id="090aa-158">在 [預設端點] 資料表中，按一下 [批次執行] 連結以開啟 [API 說明頁面]。</span><span class="sxs-lookup"><span data-stu-id="090aa-158">In the **Default Endpoint** table, click the **Batch Execution** link to open the API Help Page.</span></span>
5. <span data-ttu-id="090aa-159">在 Visual Studio 中建立 C# 主控台應用程式：[新增] > [專案] > [Visual C#] > [Windows 傳統桌面] > [主控台應用程式 (.NET Framework)]。</span><span class="sxs-lookup"><span data-stu-id="090aa-159">In Visual Studio, create a C# console application: **New** > **Project** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
6. <span data-ttu-id="090aa-160">在 [API 說明頁面] 的頁面底部找到 [範例程式碼]  區段。</span><span class="sxs-lookup"><span data-stu-id="090aa-160">On the API Help Page, find the **Sample Code** section at the bottom of the page.</span></span>
7. <span data-ttu-id="090aa-161">將 C# 範例程式碼複製並貼入 Program.cs 檔案，然後移除 Blob 儲存體的所有參考。</span><span class="sxs-lookup"><span data-stu-id="090aa-161">Copy and paste the C# sample code into your Program.cs file, and remove all references to the blob storage.</span></span>
8. <span data-ttu-id="090aa-162">使用先前儲存的 API 金鑰更新 *apiKey* 變數的值。</span><span class="sxs-lookup"><span data-stu-id="090aa-162">Update the value of the *apiKey* variable with the API key saved earlier.</span></span>
9. <span data-ttu-id="090aa-163">找出要求宣告並更新傳入「匯入資料」和「匯出資料」模組的 Web 服務參數值。</span><span class="sxs-lookup"><span data-stu-id="090aa-163">Locate the request declaration and update the values of Web Service Parameters that are passed to the *Import Data* and *Export Data* modules.</span></span> <span data-ttu-id="090aa-164">在此情況下，您會使用原始的查詢，但定義新的資料表名稱。</span><span class="sxs-lookup"><span data-stu-id="090aa-164">In this case, you use the original query, but define a new table name.</span></span>
   
        var request = new BatchExecutionRequest() 
        {           
            GlobalParameters = new Dictionary<string, string>() {
                { "Query", @"select [age], [workclass], [fnlwgt], [education], [education-num], [marital-status], [occupation], [relationship], [race], [sex], [capital-gain], [capital-loss], [hours-per-week], [native-country], [income] from dbo.censusdata" },
                { "Table", "dbo.ScoredTable2" },
            }
        };
10. <span data-ttu-id="090aa-165">執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="090aa-165">Run the application.</span></span> 

<span data-ttu-id="090aa-166">執行完成時，新的資料表會加入包含評分結果的資料庫。</span><span class="sxs-lookup"><span data-stu-id="090aa-166">On completion of the run, a new table is added to the database containing the scoring results.</span></span>

### <a name="deploy-a-new-web-service"></a><span data-ttu-id="090aa-167">部署新的 Web 服務</span><span class="sxs-lookup"><span data-stu-id="090aa-167">Deploy a New Web Service</span></span>

> [!NOTE] 
> <span data-ttu-id="090aa-168">若要部署新的 Web 服務，您必須在要部署 Web 服務的訂用帳戶中具備足夠的權限。</span><span class="sxs-lookup"><span data-stu-id="090aa-168">To deploy a New web service you must have sufficient permissions in the subscription to which you deploying the web service.</span></span> <span data-ttu-id="090aa-169">如需詳細資訊，請參閱[使用 Azure Machine Learning Web 服務入口網站管理 Web 服務](machine-learning-manage-new-webservice.md)。</span><span class="sxs-lookup"><span data-stu-id="090aa-169">For more information, see [Manage a Web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="090aa-170">部署為新的 Web 服務，並建立應用程式取用它︰</span><span class="sxs-lookup"><span data-stu-id="090aa-170">To deploy as a New Web Service and create an application to consume it:</span></span>

1. <span data-ttu-id="090aa-171">在實驗畫布底端，按一下 [執行] 。</span><span class="sxs-lookup"><span data-stu-id="090aa-171">At the bottom of the experiment canvas, click **Run**.</span></span>
2. <span data-ttu-id="090aa-172">執行完成時，按一下 [部署 Web 服務]，然後選取 [部署 Web 服務 [新]]。</span><span class="sxs-lookup"><span data-stu-id="090aa-172">When the run has completed, click **Deploy Web Service** and select **Deploy Web Service [New]**.</span></span>
3. <span data-ttu-id="090aa-173">在 [部署實驗] 頁面上，輸入您 Web 服務的名稱並選取定價方案，然後按一下 [部署]。</span><span class="sxs-lookup"><span data-stu-id="090aa-173">On the Deploy Experiment page, enter a name for your web service, and select a pricing plan, then click **Deploy**.</span></span>
4. <span data-ttu-id="090aa-174">在 [快速入門] 頁面上，按一下 [取用]。</span><span class="sxs-lookup"><span data-stu-id="090aa-174">On the **Quickstart** page, click **Consume**.</span></span>
5. <span data-ttu-id="090aa-175">在 [範例程式碼] 區段中，按一下 [批次]。</span><span class="sxs-lookup"><span data-stu-id="090aa-175">In the **Sample Code** section, click **Batch**.</span></span>
6. <span data-ttu-id="090aa-176">在 Visual Studio 中建立 C# 主控台應用程式：[新增] > [專案] > [Visual C#] > [Windows 傳統桌面] > [主控台應用程式 (.NET Framework)]。</span><span class="sxs-lookup"><span data-stu-id="090aa-176">In Visual Studio, create a C# console application: **New** > **Project** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
7. <span data-ttu-id="090aa-177">將 C# 範例程式碼複製並貼入 Program.cs 檔案。</span><span class="sxs-lookup"><span data-stu-id="090aa-177">Copy and paste the C# sample code into your Program.cs file.</span></span>
8. <span data-ttu-id="090aa-178">使用位於 [基本取用資訊] 區段中的 [主索引鍵] 更新 *apiKey* 變數的值。</span><span class="sxs-lookup"><span data-stu-id="090aa-178">Update the value of the *apiKey* variable with the **Primary Key** located in the **Basic consumption info** section.</span></span>
9. <span data-ttu-id="090aa-179">找出 *scoreRequest* 宣告並更新傳入「匯入資料」和「匯出資料」模組的 Web 服務參數值。</span><span class="sxs-lookup"><span data-stu-id="090aa-179">Locate the *scoreRequest* declaration and update the values of Web Service Parameters that are passed to the *Import Data* and *Export Data* modules.</span></span> <span data-ttu-id="090aa-180">在此情況下，您會使用原始的查詢，但定義新的資料表名稱。</span><span class="sxs-lookup"><span data-stu-id="090aa-180">In this case, you use the original query, but define a new table name.</span></span>
   
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
10. <span data-ttu-id="090aa-181">執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="090aa-181">Run the application.</span></span> 

