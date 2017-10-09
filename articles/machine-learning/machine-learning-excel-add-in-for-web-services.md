---
title: "aaaExcel 增益集的機器學習 Web 服務 |Microsoft 文件"
description: "Toouse Azure 機器學習 Web services 如何直接在 Excel 中而不需要撰寫任何程式碼。"
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
ms.openlocfilehash: c52f40d33c9907f284e4750afe47181dc3365fe5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="excel-add-in-for-azure-machine-learning-web-services"></a><span data-ttu-id="9fbd4-103">適用於 Azure Machine Learning Web 服務的 Excel 增益集</span><span class="sxs-lookup"><span data-stu-id="9fbd4-103">Excel Add-in for Azure Machine Learning web services</span></span>
<span data-ttu-id="9fbd4-104">Excel 可讓您輕鬆 toocall web 服務直接而 hello 需要 toowrite 任何程式碼。</span><span class="sxs-lookup"><span data-stu-id="9fbd4-104">Excel makes it easy toocall web services directly without hello need toowrite any code.</span></span>

## <a name="steps-toouse-an-existing-web-service-in-hello-workbook"></a><span data-ttu-id="9fbd4-105">步驟 tooUse hello 活頁簿中的現有 web 服務</span><span class="sxs-lookup"><span data-stu-id="9fbd4-105">Steps tooUse an Existing web service in hello Workbook</span></span>

1. <span data-ttu-id="9fbd4-106">開啟 hello[範例 Excel 檔案](http://aka.ms/amlexcel-sample-2)，其中包含 hello Excel 增益集和乘客上的相關資料 hello Titanic。</span><span class="sxs-lookup"><span data-stu-id="9fbd4-106">Open hello [sample Excel file](http://aka.ms/amlexcel-sample-2), which contains hello Excel add-in and data about passengers on hello Titanic.</span></span>
2. <span data-ttu-id="9fbd4-107">按一下以選擇 hello web 服務-"浩大存活者預測工具 （Excel 增益集範例） [分數] 「 在此範例中。</span><span class="sxs-lookup"><span data-stu-id="9fbd4-107">Choose hello web service by clicking it - "Titanic Survivor Predictor (Excel Add-in Sample) [Score]" in this example.</span></span>
   
    ![選取 Web 服務][01]
3. <span data-ttu-id="9fbd4-109">這會帶您 toohello**預測**> 一節。</span><span class="sxs-lookup"><span data-stu-id="9fbd4-109">This takes you toohello **Predict** section.</span></span>  <span data-ttu-id="9fbd4-110">此活頁簿已經包含範例資料，但若為空白的活頁簿，您可在 Excel 中選取一個儲存格並按一下 [使用範例資料] 。</span><span class="sxs-lookup"><span data-stu-id="9fbd4-110">This workbook already contains sample data, but for a blank workbook you can select a cell in Excel and click **Use sample data**.</span></span>
4. <span data-ttu-id="9fbd4-111">選取 hello 與標頭的資料，然後按一下 hello 輸入的資料範圍圖示。</span><span class="sxs-lookup"><span data-stu-id="9fbd4-111">Select hello data with headers and click hello input data range icon.</span></span>  <span data-ttu-id="9fbd4-112">請確定核取 hello 「 我的資料有標頭 」 的方塊。</span><span class="sxs-lookup"><span data-stu-id="9fbd4-112">Make sure hello "My data has headers" box is checked.</span></span>
5. <span data-ttu-id="9fbd4-113">在下**輸出**，輸入您想這裡 hello 輸出 toobe，例如"H1"hello 資料格數目。</span><span class="sxs-lookup"><span data-stu-id="9fbd4-113">Under **Output**, enter hello cell number where you want hello output toobe, for example "H1" here.</span></span>
6. <span data-ttu-id="9fbd4-114">按一下 [預測] 。</span><span class="sxs-lookup"><span data-stu-id="9fbd4-114">Click **Predict**.</span></span>
   
    ![預測區段][02]

<span data-ttu-id="9fbd4-116">部署 Web 服務或使用現有的 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="9fbd4-116">Deploy a web service or use an existing Web service.</span></span> <span data-ttu-id="9fbd4-117">如需有關如何部署 web 服務的詳細資訊，請參閱[逐步解說步驟 5： 部署 hello Azure 機器學習 Web 服務](machine-learning-walkthrough-5-publish-web-service.md)。</span><span class="sxs-lookup"><span data-stu-id="9fbd4-117">For more information on deploying a web service, see [Walkthrough Step 5: Deploy hello Azure Machine Learning Web service](machine-learning-walkthrough-5-publish-web-service.md).</span></span>

<span data-ttu-id="9fbd4-118">取得您的 web 服務的 hello API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="9fbd4-118">Get hello API key for your web service.</span></span> <span data-ttu-id="9fbd4-119">執行此動作的位置，取決於您發佈的是傳統 Machine Learning Web 服務或新的 Machine Learning Web 服務。</span><span class="sxs-lookup"><span data-stu-id="9fbd4-119">Where you perform this action depends on whether you published a Classic Machine Learning web service of a New Machine Learning web service.</span></span>

<span data-ttu-id="9fbd4-120">**使用傳統 Web 服務**</span><span class="sxs-lookup"><span data-stu-id="9fbd4-120">**Use a Classic web service**</span></span> 

1. <span data-ttu-id="9fbd4-121">在機器學習 Studio 中，按一下 hello **WEB 服務**hello 左窗格中，區段，然後選取 hello web 服務。</span><span class="sxs-lookup"><span data-stu-id="9fbd4-121">In Machine Learning Studio, click hello **WEB SERVICES** section in hello left pane, and then select hello web service.</span></span>
   
    ![Studio 選取 Web 服務][04]
2. <span data-ttu-id="9fbd4-123">複製 hello web 服務的 hello API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="9fbd4-123">Copy hello API key for hello web service.</span></span>
   
    ![Studio API 金鑰][05]
3. <span data-ttu-id="9fbd4-125">在 hello**儀表板**hello web 服務索引標籤上，按一下 hello**要求/回應**連結。</span><span class="sxs-lookup"><span data-stu-id="9fbd4-125">On hello **DASHBOARD** tab for hello web service, click hello **REQUEST/RESPONSE** link.</span></span>
4. <span data-ttu-id="9fbd4-126">尋找 hello**要求 URI** > 一節。</span><span class="sxs-lookup"><span data-stu-id="9fbd4-126">Look for hello **Request URI** section.</span></span>  <span data-ttu-id="9fbd4-127">複製並儲存 hello URL。</span><span class="sxs-lookup"><span data-stu-id="9fbd4-127">Copy and save hello URL.</span></span>

> [!NOTE]
> <span data-ttu-id="9fbd4-128">它現在是到 hello 可能 toosign [Azure 機器學習 Web 服務](https://services.azureml.net)傳統的機器學習 web 服務的入口網站 tooobtain hello API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="9fbd4-128">It is now possible toosign into hello [Azure Machine Learning Web Services](https://services.azureml.net) portal tooobtain hello API key for a Classic Machine Learning web service.</span></span>
> 
> 

<span data-ttu-id="9fbd4-129">**使用新的 Web 服務**</span><span class="sxs-lookup"><span data-stu-id="9fbd4-129">**Use a New web service**</span></span>

1. <span data-ttu-id="9fbd4-130">在 hello [Azure 機器學習 Web 服務](https://services.azureml.net)入口網站中，按一下**Web 服務**，然後選取您的 web 服務。</span><span class="sxs-lookup"><span data-stu-id="9fbd4-130">In hello [Azure Machine Learning Web Services](https://services.azureml.net) portal, click **Web Services**, then select your web service.</span></span> 
2. <span data-ttu-id="9fbd4-131">按一下 [取用] 。</span><span class="sxs-lookup"><span data-stu-id="9fbd4-131">Click **Consume**.</span></span>
3. <span data-ttu-id="9fbd4-132">尋找 hello**基本耗用量資訊**> 一節。</span><span class="sxs-lookup"><span data-stu-id="9fbd4-132">Look for hello **Basic consumption info** section.</span></span> <span data-ttu-id="9fbd4-133">複製並儲存 hello**主索引鍵**和 hello**要求-回應**URL。</span><span class="sxs-lookup"><span data-stu-id="9fbd4-133">Copy and save hello **Primary Key** and hello **Request-Response** URL.</span></span>

## <a name="steps-tooadd-a-new-web-service"></a><span data-ttu-id="9fbd4-134">步驟 tooAdd 新的 web 服務</span><span class="sxs-lookup"><span data-stu-id="9fbd4-134">Steps tooAdd a New web service</span></span>

1. <span data-ttu-id="9fbd4-135">部署 Web 服務或使用現有的 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="9fbd4-135">Deploy a web service or use an existing Web service.</span></span> <span data-ttu-id="9fbd4-136">如需有關如何部署 web 服務的詳細資訊，請參閱[逐步解說步驟 5： 部署 hello Azure 機器學習 Web 服務](machine-learning-walkthrough-5-publish-web-service.md)。</span><span class="sxs-lookup"><span data-stu-id="9fbd4-136">For more information on deploying a web service, see [Walkthrough Step 5: Deploy hello Azure Machine Learning Web service](machine-learning-walkthrough-5-publish-web-service.md).</span></span>
2. <span data-ttu-id="9fbd4-137">按一下 [取用] 。</span><span class="sxs-lookup"><span data-stu-id="9fbd4-137">Click **Consume**.</span></span>
3. <span data-ttu-id="9fbd4-138">尋找 hello**基本耗用量資訊**> 一節。</span><span class="sxs-lookup"><span data-stu-id="9fbd4-138">Look for hello **Basic consumption info** section.</span></span> <span data-ttu-id="9fbd4-139">複製並儲存 hello**主索引鍵**和 hello**要求-回應**URL。</span><span class="sxs-lookup"><span data-stu-id="9fbd4-139">Copy and save hello **Primary Key** and hello **Request-Response** URL.</span></span>
4. <span data-ttu-id="9fbd4-140">在 Excel 中，移 toohello **Web 服務**區段 (如果您是在 hello**預測**區段中，按一下 [web 服務的 hello 上一頁] 箭頭 toogo toohello 清單)。</span><span class="sxs-lookup"><span data-stu-id="9fbd4-140">In Excel, go toohello **Web Services** section (if you are in hello **Predict** section, click hello back arrow toogo toohello list of web services).</span></span>
   
    ![請選取 tooWeb 服務][03]
5. <span data-ttu-id="9fbd4-142">按一下 [新增 Web 服務] 。</span><span class="sxs-lookup"><span data-stu-id="9fbd4-142">Click **Add Web Service**.</span></span>
6. <span data-ttu-id="9fbd4-143">將 hello URL 貼到 Excel 增益集文字方塊標示為 「 hello **URL**。</span><span class="sxs-lookup"><span data-stu-id="9fbd4-143">Paste hello URL into hello Excel add-in text box labeled **URL**.</span></span>
7. <span data-ttu-id="9fbd4-144">標示為 hello 文字方塊中的貼上 hello API/主要金鑰**API 金鑰**。</span><span class="sxs-lookup"><span data-stu-id="9fbd4-144">Paste hello API/Primary key into hello text box labeled **API key**.</span></span>
8. <span data-ttu-id="9fbd4-145">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="9fbd4-145">Click **Add**.</span></span>
   
    ![傳統 Web 服務的 URL 和 API 金鑰。][06]
9. <span data-ttu-id="9fbd4-147">toouse hello web 服務，請遵循上述指示 hello、"步驟 tooUse 現有 web 服務。 」</span><span class="sxs-lookup"><span data-stu-id="9fbd4-147">toouse hello web service, follow hello preceding directions, "Steps tooUse an Existing web Service."</span></span>

## <a name="sharing-your-workbook"></a><span data-ttu-id="9fbd4-148">共用活頁簿</span><span class="sxs-lookup"><span data-stu-id="9fbd4-148">Sharing Your Workbook</span></span>
<span data-ttu-id="9fbd4-149">如果您要儲存您的活頁簿，然後也會儲存您加入的 hello web 服務的 hello API/主要索引鍵。</span><span class="sxs-lookup"><span data-stu-id="9fbd4-149">If you save your workbook, then hello API/Primary key for hello web services you have added is also saved.</span></span> <span data-ttu-id="9fbd4-150">這表示您只應該與您信任的人共用 hello 活頁簿。</span><span class="sxs-lookup"><span data-stu-id="9fbd4-150">That means you should only share hello workbook with individuals you trust.</span></span>

<span data-ttu-id="9fbd4-151">在 hello 下列註解區段，或在任何提問我們[論壇](http://go.microsoft.com/fwlink/?LinkID=403669&clcid=0x409)。</span><span class="sxs-lookup"><span data-stu-id="9fbd4-151">Ask any questions in hello following comment section or on our [forum](http://go.microsoft.com/fwlink/?LinkID=403669&clcid=0x409).</span></span>

[01]: ./media/machine-learning-excel-add-in-for-web-services/image1.png
[02]: ./media/machine-learning-excel-add-in-for-web-services/image2.png
[03]: ./media/machine-learning-excel-add-in-for-web-services/image3.png
[04]: ./media/machine-learning-excel-add-in-for-web-services/image4.png
[05]: ./media/machine-learning-excel-add-in-for-web-services/image5.png
[06]: ./media/machine-learning-excel-add-in-for-web-services/image6.png
