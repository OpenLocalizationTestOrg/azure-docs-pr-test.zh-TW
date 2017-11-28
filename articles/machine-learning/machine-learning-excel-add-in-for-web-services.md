---
title: "適用於 Machine Learning Web 服務的 Excel 增益集 | Microsoft Docs"
description: "如何在 Excel 中直接使用 Azure Machine Learning Web 服務，而不需要撰寫任何程式碼。"
services: machine-learning
documentationcenter: 
author: tedway
manager: jhubbard
editor: cgronlun
tags: 
ms.assetid: 9618079d-502f-4974-a3e2-8f924042a23f
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/14/2017
ms.author: tedway;garye
ms.openlocfilehash: 0d60dd87bbdd4d3eafac0f8876cc9e41412a53ea
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="excel-add-in-for-azure-machine-learning-web-services"></a><span data-ttu-id="7c99a-103">適用於 Azure Machine Learning Web 服務的 Excel 增益集</span><span class="sxs-lookup"><span data-stu-id="7c99a-103">Excel Add-in for Azure Machine Learning web services</span></span>
<span data-ttu-id="7c99a-104">Excel 可以讓您直接輕鬆呼叫 Web 服務，而不需要撰寫任何程式碼。</span><span class="sxs-lookup"><span data-stu-id="7c99a-104">Excel makes it easy to call web services directly without the need to write any code.</span></span>

## <a name="steps-to-use-an-existing-web-service-in-the-workbook"></a><span data-ttu-id="7c99a-105">使用活頁簿中現有 Web 服務的步驟</span><span class="sxs-lookup"><span data-stu-id="7c99a-105">Steps to Use an Existing web service in the Workbook</span></span>

1. <span data-ttu-id="7c99a-106">開啟 [範例 Excel 檔案](http://aka.ms/amlexcel-sample-2)，其中包含 Excel 增益集和鐵達尼號乘客的相關資料。</span><span class="sxs-lookup"><span data-stu-id="7c99a-106">Open the [sample Excel file](http://aka.ms/amlexcel-sample-2), which contains the Excel add-in and data about passengers on the Titanic.</span></span>
2. <span data-ttu-id="7c99a-107">按一下 Web 服務加以選擇，在此範例中為「鐵達尼號存活者預測工具 (Excel 增益集範例) [分數]」。</span><span class="sxs-lookup"><span data-stu-id="7c99a-107">Choose the web service by clicking it - "Titanic Survivor Predictor (Excel Add-in Sample) [Score]" in this example.</span></span>
   
    ![選取 Web 服務][01]
3. <span data-ttu-id="7c99a-109">這會帶領您到 [預測] 區段。</span><span class="sxs-lookup"><span data-stu-id="7c99a-109">This takes you to the **Predict** section.</span></span>  <span data-ttu-id="7c99a-110">此活頁簿已經包含範例資料，但若為空白的活頁簿，您可在 Excel 中選取一個儲存格並按一下 [使用範例資料] 。</span><span class="sxs-lookup"><span data-stu-id="7c99a-110">This workbook already contains sample data, but for a blank workbook you can select a cell in Excel and click **Use sample data**.</span></span>
4. <span data-ttu-id="7c99a-111">選取含有標頭的資料並按一下輸入資料範圍圖示。</span><span class="sxs-lookup"><span data-stu-id="7c99a-111">Select the data with headers and click the input data range icon.</span></span>  <span data-ttu-id="7c99a-112">請確定已核取 [我的資料有標頭] 方塊。</span><span class="sxs-lookup"><span data-stu-id="7c99a-112">Make sure the "My data has headers" box is checked.</span></span>
5. <span data-ttu-id="7c99a-113">在 [輸出] 之下，輸入您想要輸出所在的儲存格編號，例如此處的 "H1"。</span><span class="sxs-lookup"><span data-stu-id="7c99a-113">Under **Output**, enter the cell number where you want the output to be, for example "H1" here.</span></span>
6. <span data-ttu-id="7c99a-114">按一下 [預測] 。</span><span class="sxs-lookup"><span data-stu-id="7c99a-114">Click **Predict**.</span></span>
   
    ![預測區段][02]

<span data-ttu-id="7c99a-116">部署 Web 服務或使用現有的 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="7c99a-116">Deploy a web service or use an existing Web service.</span></span> <span data-ttu-id="7c99a-117">如需部署 Web 服務的詳細資訊，請參閱[逐步解說步驟 5：部署 Azure Machine Learning Web 服務](machine-learning-walkthrough-5-publish-web-service.md)。</span><span class="sxs-lookup"><span data-stu-id="7c99a-117">For more information on deploying a web service, see [Walkthrough Step 5: Deploy the Azure Machine Learning Web service](machine-learning-walkthrough-5-publish-web-service.md).</span></span>

<span data-ttu-id="7c99a-118">取得 Web 服務的 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="7c99a-118">Get the API key for your web service.</span></span> <span data-ttu-id="7c99a-119">執行此動作的位置，取決於您發佈的是傳統 Machine Learning Web 服務或新的 Machine Learning Web 服務。</span><span class="sxs-lookup"><span data-stu-id="7c99a-119">Where you perform this action depends on whether you published a Classic Machine Learning web service of a New Machine Learning web service.</span></span>

<span data-ttu-id="7c99a-120">**使用傳統 Web 服務**</span><span class="sxs-lookup"><span data-stu-id="7c99a-120">**Use a Classic web service**</span></span> 

1. <span data-ttu-id="7c99a-121">在 Machine Learning Studio 中，按一下左窗格中的 [WEB 服務]  區段，然後選取 web 服務。</span><span class="sxs-lookup"><span data-stu-id="7c99a-121">In Machine Learning Studio, click the **WEB SERVICES** section in the left pane, and then select the web service.</span></span>
   
    ![Studio 選取 Web 服務][04]
2. <span data-ttu-id="7c99a-123">複製 web 服務的 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="7c99a-123">Copy the API key for the web service.</span></span>
   
    ![Studio API 金鑰][05]
3. <span data-ttu-id="7c99a-125">在 Web 服務的 [儀表板] 索引標籤上，按一下 [要求/回應] 連結。</span><span class="sxs-lookup"><span data-stu-id="7c99a-125">On the **DASHBOARD** tab for the web service, click the **REQUEST/RESPONSE** link.</span></span>
4. <span data-ttu-id="7c99a-126">尋找 [要求 URI]  區段。</span><span class="sxs-lookup"><span data-stu-id="7c99a-126">Look for the **Request URI** section.</span></span>  <span data-ttu-id="7c99a-127">複製並儲存 URL。</span><span class="sxs-lookup"><span data-stu-id="7c99a-127">Copy and save the URL.</span></span>

> [!NOTE]
> <span data-ttu-id="7c99a-128">現在就能登入 [Azure Machine Learning Web 服務](https://services.azureml.net)入口網站，來取得傳統 Machine Learning Web 服務的 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="7c99a-128">It is now possible to sign into the [Azure Machine Learning Web Services](https://services.azureml.net) portal to obtain the API key for a Classic Machine Learning web service.</span></span>
> 
> 

<span data-ttu-id="7c99a-129">**使用新的 Web 服務**</span><span class="sxs-lookup"><span data-stu-id="7c99a-129">**Use a New web service**</span></span>

1. <span data-ttu-id="7c99a-130">在 [Azure Machine Learning Web 服務](https://services.azureml.net)入口網站中，按一下 [Web 服務]，然後選取您的 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="7c99a-130">In the [Azure Machine Learning Web Services](https://services.azureml.net) portal, click **Web Services**, then select your web service.</span></span> 
2. <span data-ttu-id="7c99a-131">按一下 [取用] 。</span><span class="sxs-lookup"><span data-stu-id="7c99a-131">Click **Consume**.</span></span>
3. <span data-ttu-id="7c99a-132">尋找 [基本使用資訊]  區段。</span><span class="sxs-lookup"><span data-stu-id="7c99a-132">Look for the **Basic consumption info** section.</span></span> <span data-ttu-id="7c99a-133">複製並儲存 [主要金鑰] 和 [要求-回應] URL。</span><span class="sxs-lookup"><span data-stu-id="7c99a-133">Copy and save the **Primary Key** and the **Request-Response** URL.</span></span>

## <a name="steps-to-add-a-new-web-service"></a><span data-ttu-id="7c99a-134">新增 Web 服務的步驟</span><span class="sxs-lookup"><span data-stu-id="7c99a-134">Steps to Add a New web service</span></span>

1. <span data-ttu-id="7c99a-135">部署 Web 服務或使用現有的 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="7c99a-135">Deploy a web service or use an existing Web service.</span></span> <span data-ttu-id="7c99a-136">如需部署 Web 服務的詳細資訊，請參閱[逐步解說步驟 5：部署 Azure Machine Learning Web 服務](machine-learning-walkthrough-5-publish-web-service.md)。</span><span class="sxs-lookup"><span data-stu-id="7c99a-136">For more information on deploying a web service, see [Walkthrough Step 5: Deploy the Azure Machine Learning Web service](machine-learning-walkthrough-5-publish-web-service.md).</span></span>
2. <span data-ttu-id="7c99a-137">按一下 [取用] 。</span><span class="sxs-lookup"><span data-stu-id="7c99a-137">Click **Consume**.</span></span>
3. <span data-ttu-id="7c99a-138">尋找 [基本使用資訊]  區段。</span><span class="sxs-lookup"><span data-stu-id="7c99a-138">Look for the **Basic consumption info** section.</span></span> <span data-ttu-id="7c99a-139">複製並儲存 [主要金鑰] 和 [要求-回應] URL。</span><span class="sxs-lookup"><span data-stu-id="7c99a-139">Copy and save the **Primary Key** and the **Request-Response** URL.</span></span>
4. <span data-ttu-id="7c99a-140">在 Excel 中，前往 [Web 服務] 區段 (如果您是在 [預測] 區段中，請按一下向後鍵以前往 Web 服務的清單)。</span><span class="sxs-lookup"><span data-stu-id="7c99a-140">In Excel, go to the **Web Services** section (if you are in the **Predict** section, click the back arrow to go to the list of web services).</span></span>
   
    ![前往 Web 服務][03]
5. <span data-ttu-id="7c99a-142">按一下 [新增 Web 服務] 。</span><span class="sxs-lookup"><span data-stu-id="7c99a-142">Click **Add Web Service**.</span></span>
6. <span data-ttu-id="7c99a-143">將 URL 貼到標示為 [URL] 的 Excel 增益集文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="7c99a-143">Paste the URL into the Excel add-in text box labeled **URL**.</span></span>
7. <span data-ttu-id="7c99a-144">將 API/主要金鑰貼到標示為 [API 金鑰] 的文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="7c99a-144">Paste the API/Primary key into the text box labeled **API key**.</span></span>
8. <span data-ttu-id="7c99a-145">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="7c99a-145">Click **Add**.</span></span>
   
    ![傳統 Web 服務的 URL 和 API 金鑰。][06]
9. <span data-ttu-id="7c99a-147">若要使用 Web 服務，請遵循前述「使用現有 Web 服務的步驟」的指示。</span><span class="sxs-lookup"><span data-stu-id="7c99a-147">To use the web service, follow the preceding directions, "Steps to Use an Existing web Service."</span></span>

## <a name="sharing-your-workbook"></a><span data-ttu-id="7c99a-148">共用活頁簿</span><span class="sxs-lookup"><span data-stu-id="7c99a-148">Sharing Your Workbook</span></span>
<span data-ttu-id="7c99a-149">如果您儲存您的活頁簿，則您為 Web 服務加入的 API/主要金鑰也會一併儲存。</span><span class="sxs-lookup"><span data-stu-id="7c99a-149">If you save your workbook, then the API/Primary key for the web services you have added is also saved.</span></span> <span data-ttu-id="7c99a-150">這表示您應該只與您信任的人共用活頁簿。</span><span class="sxs-lookup"><span data-stu-id="7c99a-150">That means you should only share the workbook with individuals you trust.</span></span>

<span data-ttu-id="7c99a-151">如果有任何問題，請在下方的註解區或在我們 [論壇](http://go.microsoft.com/fwlink/?LinkID=403669&clcid=0x409)中提出。</span><span class="sxs-lookup"><span data-stu-id="7c99a-151">Ask any questions in the following comment section or on our [forum](http://go.microsoft.com/fwlink/?LinkID=403669&clcid=0x409).</span></span>

[01]: ./media/machine-learning-excel-add-in-for-web-services/image1.png
[02]: ./media/machine-learning-excel-add-in-for-web-services/image2.png
[03]: ./media/machine-learning-excel-add-in-for-web-services/image3.png
[04]: ./media/machine-learning-excel-add-in-for-web-services/image4.png
[05]: ./media/machine-learning-excel-add-in-for-web-services/image5.png
[06]: ./media/machine-learning-excel-add-in-for-web-services/image6.png
