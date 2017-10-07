---
title: "機器學習 Web 服務，從 Excel aaaConsume |Microsoft 文件"
description: "從 Excel 使用 Azure Machine Learning Web 服務"
services: machine-learning
documentationcenter: 
author: tedway
manager: jhubbard
editor: cgronlun
ms.assetid: 3f3cdd2f-1816-487e-ab78-530e01e9788f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 2/13/2017
ms.author: tedway
ms.openlocfilehash: e2e8bbf7ba75b6618a0285539555ce175ec03c1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="consuming-an-azure-machine-learning-web-service-from-excel"></a><span data-ttu-id="5b994-103">從 Excel 使用 Azure Machine Learning Web 服務</span><span class="sxs-lookup"><span data-stu-id="5b994-103">Consuming an Azure Machine Learning Web Service from Excel</span></span>
 <span data-ttu-id="5b994-104">Azure Machine Learning Studio 可讓您輕鬆 toocall web 服務，直接從 Excel 而 hello 需要 toowrite 任何程式碼。</span><span class="sxs-lookup"><span data-stu-id="5b994-104">Azure Machine Learning Studio makes it easy toocall web services directly from Excel without hello need toowrite any code.</span></span>

<span data-ttu-id="5b994-105">如果您使用 Excel 2013 （或更新版本） 或 Excel Online，則我們建議您使用 hello Excel [Excel 增益集](machine-learning-excel-add-in-for-web-services.md)。</span><span class="sxs-lookup"><span data-stu-id="5b994-105">If you are using Excel 2013 (or later) or Excel Online, then we recommend that you use hello Excel [Excel add-in](machine-learning-excel-add-in-for-web-services.md).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="steps"></a><span data-ttu-id="5b994-106">步驟</span><span class="sxs-lookup"><span data-stu-id="5b994-106">Steps</span></span>
<span data-ttu-id="5b994-107">發佈 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="5b994-107">Publish a web service.</span></span> <span data-ttu-id="5b994-108">[此頁面](machine-learning-walkthrough-5-publish-web-service.md)說明如何 toodo 它。</span><span class="sxs-lookup"><span data-stu-id="5b994-108">[This page](machine-learning-walkthrough-5-publish-web-service.md) explains how toodo it.</span></span> <span data-ttu-id="5b994-109">目前具有單一輸出 （也就是單一計分標籤） 的要求/回應服務只支援 hello Excel 活頁簿的功能。</span><span class="sxs-lookup"><span data-stu-id="5b994-109">Currently hello Excel workbook feature is only supported for Request/Response services that have a single output (that is, a single scoring label).</span></span> 

<span data-ttu-id="5b994-110">Web 服務之後，按一下 hello **WEB 服務**左邊的 hello studio hello 區段，然後選取 從 Excel 的 hello web 服務 tooconsume。</span><span class="sxs-lookup"><span data-stu-id="5b994-110">Once you have a web service, click on hello **WEB SERVICES** section on hello left of hello studio, and then select hello web service tooconsume from Excel.</span></span>

<span data-ttu-id="5b994-111">**傳統 Web 服務**</span><span class="sxs-lookup"><span data-stu-id="5b994-111">**Classic Web Service**</span></span>

1. <span data-ttu-id="5b994-112">在 hello**儀表板**hello web 服務是為 hello 的資料列索引標籤**要求/回應**服務。</span><span class="sxs-lookup"><span data-stu-id="5b994-112">On hello **DASHBOARD** tab for hello web service is a row for hello **REQUEST/RESPONSE** service.</span></span> <span data-ttu-id="5b994-113">如果此服務會在單一輸出，您應該會看見 hello**下載 Excel 活頁簿**該資料列中的連結。</span><span class="sxs-lookup"><span data-stu-id="5b994-113">If this service had a single output, you should see hello **Download Excel Workbook** link in that row.</span></span>
   
    ![][1]
2. <span data-ttu-id="5b994-114">按一下 [下載 Excel 活頁簿] 。</span><span class="sxs-lookup"><span data-stu-id="5b994-114">Click on **Download Excel Workbook**.</span></span>

<span data-ttu-id="5b994-115">**新的 Web 服務**</span><span class="sxs-lookup"><span data-stu-id="5b994-115">**New Web Service**</span></span>

1. <span data-ttu-id="5b994-116">在 hello Azure Machine Learning Web 服務入口網站中，選取 **取用**。</span><span class="sxs-lookup"><span data-stu-id="5b994-116">In hello Azure Machine Learning Web Service portal, select **Consume**.</span></span>
2. <span data-ttu-id="5b994-117">在 hello 取用頁面 hello **Web 服務耗用量選項**區段中，按一下 hello Excel 圖示。</span><span class="sxs-lookup"><span data-stu-id="5b994-117">On hello Consume page, in hello **Web service consumption options** section, click hello Excel icon.</span></span>

<span data-ttu-id="5b994-118">**使用 hello 活頁簿**</span><span class="sxs-lookup"><span data-stu-id="5b994-118">**Using hello workbook**</span></span>

1. <span data-ttu-id="5b994-119">開啟 hello 活頁簿。</span><span class="sxs-lookup"><span data-stu-id="5b994-119">Open hello workbook.</span></span>
2. <span data-ttu-id="5b994-120">此時會出現安全性警告。按一下 hello**啟用編輯** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5b994-120">A Security Warning appears; click on hello **Enable Editing** button.</span></span>
   
    ![][2]
3. <span data-ttu-id="5b994-121">此時會出現安全性警告。</span><span class="sxs-lookup"><span data-stu-id="5b994-121">A Security Warning appears.</span></span> <span data-ttu-id="5b994-122">按一下 hello**啟用內容**按鈕在試算表的 toorun 巨集。</span><span class="sxs-lookup"><span data-stu-id="5b994-122">Click on hello **Enable Content** button toorun macros on your spreadsheet.</span></span>
   
    ![][3]
4. <span data-ttu-id="5b994-123">啟用巨集之後，就會產生表格。</span><span class="sxs-lookup"><span data-stu-id="5b994-123">Once macros are enabled, a table is generated.</span></span> <span data-ttu-id="5b994-124">藍色是中的資料行作為輸入 hello RR web 服務，需要或**參數**。</span><span class="sxs-lookup"><span data-stu-id="5b994-124">Columns in blue are required as input into hello RRS web service, or **PARAMETERS**.</span></span> <span data-ttu-id="5b994-125">請注意 hello RR 服務的 hello 輸出**PREDICTED VALUES**以綠色。</span><span class="sxs-lookup"><span data-stu-id="5b994-125">Note hello output of hello RRS service, **PREDICTED VALUES** in green.</span></span> <span data-ttu-id="5b994-126">對於給定的資料列的所有資料行已滿時，hello 活頁簿將會自動呼叫 hello 計分 API，並顯示 hello 計分結果。</span><span class="sxs-lookup"><span data-stu-id="5b994-126">When all columns for a given row are filled, hello workbook automatically calls hello scoring API, and displays hello scored results.</span></span>
   
    ![][4]
5. <span data-ttu-id="5b994-127">tooscore 超過一個資料列，填滿 hello 第二個資料列資料與 hello 預測所產生的值。</span><span class="sxs-lookup"><span data-stu-id="5b994-127">tooscore more than one row, fill hello second row with data and hello predicted values are produced.</span></span> <span data-ttu-id="5b994-128">您甚至可以一次貼上多列。</span><span class="sxs-lookup"><span data-stu-id="5b994-128">You can even paste several rows at once.</span></span>

<span data-ttu-id="5b994-129">您可以使用任何 hello Excel 功能圖形、 電源對應 （條件式格式化等） 與 hello 預測值 toohelp hello 資料視覺化。</span><span class="sxs-lookup"><span data-stu-id="5b994-129">You can use any of hello Excel features (graphs, power map, conditional formatting, etc.) with hello predicted values toohelp visualize hello data.</span></span>    

## <a name="sharing-your-workbook"></a><span data-ttu-id="5b994-130">共用活頁簿</span><span class="sxs-lookup"><span data-stu-id="5b994-130">Sharing your workbook</span></span>
<span data-ttu-id="5b994-131">Hello 巨集 toowork，您的 API 金鑰必須是 hello 試算表的一部分。</span><span class="sxs-lookup"><span data-stu-id="5b994-131">For hello macros toowork, your API Key must be part of hello spreadsheet.</span></span> <span data-ttu-id="5b994-132">這表示您應該只與實體/您信任的人共用 hello 活頁簿。</span><span class="sxs-lookup"><span data-stu-id="5b994-132">That means that you should share hello workbook only with entities/individuals you trust.</span></span>

## <a name="automatic-updates"></a><span data-ttu-id="5b994-133">自動更新</span><span class="sxs-lookup"><span data-stu-id="5b994-133">Automatic updates</span></span>
<span data-ttu-id="5b994-134">下列兩種情況會產生 RRS 呼叫：</span><span class="sxs-lookup"><span data-stu-id="5b994-134">An RRS call is made in these two situations:</span></span>

1. <span data-ttu-id="5b994-135">hello 第一次資料列都有內容中的所有其**參數**</span><span class="sxs-lookup"><span data-stu-id="5b994-135">hello first time a row has content in all of its **PARAMETERS**</span></span>
2. <span data-ttu-id="5b994-136">每當任何 hello**參數**中資料列時，所有的變更其**參數**輸入。</span><span class="sxs-lookup"><span data-stu-id="5b994-136">Any time any of hello **PARAMETERS** changes in a row that had all of its **PARAMETERS** entered.</span></span>

[1]: ./media/machine-learning-consuming-from-excel/excellink.png
[2]: ./media/machine-learning-consuming-from-excel/enableeditting.png
[3]: ./media/machine-learning-consuming-from-excel/enablecontent.png
[4]: ./media/machine-learning-consuming-from-excel/sampletable.png
