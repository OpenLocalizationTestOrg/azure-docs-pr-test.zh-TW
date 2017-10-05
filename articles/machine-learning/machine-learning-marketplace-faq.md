---
title: "(已過時) 常見問題集 - 在 Azure Marketplace 中發佈和使用 Machine Learning 應用程式 | Microsoft Docs"
description: "(已過時) 有關在 Azure Marketplace 中發佈 Machine Learning 應用程式的常見問題集"
services: machine-learning
documentationcenter: 
author: bharaths
manager: jhubbard
editor: cgronlun
ms.assetid: 26b3a1e7-8b9a-4004-98bc-17456d4c25e8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: bharaths
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: TRUE
ms.openlocfilehash: a4631dfeb2f817b3a3c612a8f6af48398e4f2ab9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-publishing-and-using-machine-learning-apps-in-the-azure-marketplace-faq"></a><span data-ttu-id="e61ea-103">(已過時) 在 Azure Marketplace 中發佈和使用 Machine Learning 應用程式：常見問題集</span><span class="sxs-lookup"><span data-stu-id="e61ea-103">(deprecated) Publishing and using Machine Learning apps in the Azure Marketplace: FAQ</span></span>

> [!NOTE]
> <span data-ttu-id="e61ea-104">DataMarket 和「資料服務」已進入淘汰階段，訂用帳戶將自 2017 年 3 月 31 日起淘汰並取消。</span><span class="sxs-lookup"><span data-stu-id="e61ea-104">DataMarket and Data Services are being retired, and existing subscriptions will be retired and cancelled starting 3/31/2017.</span></span> <span data-ttu-id="e61ea-105">因此，這篇文章目前已過時。</span><span class="sxs-lookup"><span data-stu-id="e61ea-105">As a result, this article is being deprecated.</span></span> 
> 
> <span data-ttu-id="e61ea-106">替代方案是，您可以將 Machine Learning 實驗發佈到 [Cortana Intelligence 資源庫](https://gallery.cortanaintelligence.com/)，以利資料科學社群使用。</span><span class="sxs-lookup"><span data-stu-id="e61ea-106">As an alternative, you can publish your Machine Learning experiments to the [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/) for the benefit of the data science community.</span></span> <span data-ttu-id="e61ea-107">如需詳細資訊，請參閱[在 Cortana Intelligence 資源庫中共用及探索資源](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish)。</span><span class="sxs-lookup"><span data-stu-id="e61ea-107">For more information, see [Share and discover resources in the Cortana Intelligence Gallery](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish).</span></span>


## <a name="questions-about-consuming-from-marketplace"></a><span data-ttu-id="e61ea-108">從 Marketplace 取用的相關問題</span><span class="sxs-lookup"><span data-stu-id="e61ea-108">Questions about consuming from Marketplace</span></span>
<span data-ttu-id="e61ea-109">**1.為什麼我輸入 Web 服務的輸入之後，得到下列錯誤訊息：**</span><span class="sxs-lookup"><span data-stu-id="e61ea-109">**1. Why do I get the following error message after I enter input for the web service:**</span></span>

<span data-ttu-id="e61ea-110">**要求導致後端逾時或後端錯誤。小組正在調查這個問題。很抱歉造成您的不便。(500)**</span><span class="sxs-lookup"><span data-stu-id="e61ea-110">**The request resulted in a back-end time out or back-end error. The team is investigating the issue. We are sorry for the inconvenience. (500)**</span></span>

<span data-ttu-id="e61ea-111">您的輸入參數可能不符合特定 Web 服務所需的格式。</span><span class="sxs-lookup"><span data-stu-id="e61ea-111">Your input parameter(s) may not conform to the required format for the specific web service.</span></span> <span data-ttu-id="e61ea-112">請參閱對應的文件連結，來尋找輸入參數的正確格式以及此 Web 服務的限制。</span><span class="sxs-lookup"><span data-stu-id="e61ea-112">Please refer to the corresponding documentation link to find the correct format for input parameters and the limitations of this web service.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="e61ea-113">**2.如果我將 [探索這個資料集] 頁面上顯示之 Web 服務的 API 連結，複製並貼到另一個瀏覽器視窗中，我應該使用哪些認證來存取結果，又該如何查看這些結果？**</span><span class="sxs-lookup"><span data-stu-id="e61ea-113">**2. If I copy the API link for the web service that I see on the "Explore this dataset" page and paste it into another browser window, what credentials should I use to access the results, and how do I see them?**</span></span>

<span data-ttu-id="e61ea-114">您應該使用您的 Marketplace 帳戶作為使用者名稱，並使用主要帳戶金鑰作為密碼。</span><span class="sxs-lookup"><span data-stu-id="e61ea-114">You should use your Marketplace account as the username and the primary account key as the password.</span></span> <span data-ttu-id="e61ea-115">您可以在 Web 服務描述下的 [探索這個資料集] 頁面上，找到主要帳戶金鑰 (按一下 [顯示] 按鈕)。</span><span class="sxs-lookup"><span data-stu-id="e61ea-115">The primary account key can be found on the **Explore this dataset** page under the description of the web service (click the **show** button).</span></span> <span data-ttu-id="e61ea-116">視您所使用的瀏覽器而定，結果可能會顯示在瀏覽器中或可供下載。</span><span class="sxs-lookup"><span data-stu-id="e61ea-116">The result may display in the browser or it may be available to  download, depending on which browser you are using.</span></span>

<span data-ttu-id="e61ea-117">**3.為什麼我輸入 Web 服務的輸入之後，在 [探索這個資料集] 頁面上得到下列錯誤訊息：**</span><span class="sxs-lookup"><span data-stu-id="e61ea-117">**3. Why do I get the following error message after I enter the input for the web service on the "Explore this dataset" page:**</span></span> 

<span data-ttu-id="e61ea-118">**處理您的要求時發生未預期的錯誤。請再試一次。**</span><span class="sxs-lookup"><span data-stu-id="e61ea-118">**An unexpected error occurred while processing your request. Please try again.**</span></span>

<span data-ttu-id="e61ea-119">在 Marketplace 的 [探索這個資料集]  頁面上取用您的 Web 服務時，該服務的一個或多個輸入參數可能超過長度限制。</span><span class="sxs-lookup"><span data-stu-id="e61ea-119">One or more input parameters of your web service may have exceeded the length limit when consuming the web service on the marketplace **Explore this dataset** page.</span></span> <span data-ttu-id="e61ea-120">您可以透過 HTTP POST 方法，使用較長的輸入長度呼叫服務。</span><span class="sxs-lookup"><span data-stu-id="e61ea-120">The services can be called with a longer input length by using HTTP POST methods.</span></span> <span data-ttu-id="e61ea-121">例如，請參閱 [使用 R 在 Machine Learning 上建置並發佈至 Marketplace 的範例解決方案](machine-learning-r-csharp-web-service-examples.md)。</span><span class="sxs-lookup"><span data-stu-id="e61ea-121">For examples, see [Sample solutions using R on Machine Learning and published to Marketplace](machine-learning-r-csharp-web-service-examples.md).</span></span>

<span data-ttu-id="e61ea-122">**4.為什麼 Azure 傳統入口網站之 [存放區] 的 [API 總管] 索引標籤中未顯示任何項目？**</span><span class="sxs-lookup"><span data-stu-id="e61ea-122">**4. Why do I not see anything in the "API EXPLORER" tab int the Store in the Azure Classic Portal?**</span></span> 

<span data-ttu-id="e61ea-123">這是 Azure 傳統入口網站 Marketplace 的已知問題。</span><span class="sxs-lookup"><span data-stu-id="e61ea-123">This is a known issue with the Azure Classic Portal Marketplace.</span></span> <span data-ttu-id="e61ea-124">小組正著手解決這個問題。</span><span class="sxs-lookup"><span data-stu-id="e61ea-124">The team is working to resolve this issue.</span></span> 

## <a name="questions-about-publishing-from-azure-machine-learning-on-marketplace"></a><span data-ttu-id="e61ea-125">透過 Azure Machine Learning 在 Marketplace 上發佈的相關問題</span><span class="sxs-lookup"><span data-stu-id="e61ea-125">Questions about publishing from Azure Machine Learning on Marketplace</span></span>
<span data-ttu-id="e61ea-126">**1.為什麼我的 Web 服務不會重新整理標誌或影像的異動？**</span><span class="sxs-lookup"><span data-stu-id="e61ea-126">**1. Why are my transactions of logos or images not refreshing for my web service?**</span></span> 

<span data-ttu-id="e61ea-127">標誌和影像是在發佈入口網站中快取，新的標誌或影像最多可能需要 10 天才能在入口網站上更新。</span><span class="sxs-lookup"><span data-stu-id="e61ea-127">Logos and images are cached in the publishing portal, and it may take up to 10 days for the new logo or image to update on the portal.</span></span>

<span data-ttu-id="e61ea-128">**2.為什麼在 Marketplace 上，我的 Web 服務的 [詳細資料] 索引標籤顯示錯誤訊息？**</span><span class="sxs-lookup"><span data-stu-id="e61ea-128">**2. Why is the “Detail" tab of my web service on Marketplace showing an error message?**</span></span>

<span data-ttu-id="e61ea-129">在連接到 Azure Machine Learning 以取得服務詳細資料時，已知有一個 Marketplace 問題。</span><span class="sxs-lookup"><span data-stu-id="e61ea-129">There is a known Marketplace issue when connecting to Azure Machine Learning for service details.</span></span> <span data-ttu-id="e61ea-130">小組正著手解決這個問題。</span><span class="sxs-lookup"><span data-stu-id="e61ea-130">The team is working to resolve this issue.</span></span>

<span data-ttu-id="e61ea-131">**3.為什麼在取用 Marketplace 中的 Web 服務時，無法使用 Azure Machine Learning Web 服務中的 R 範例程式碼？**</span><span class="sxs-lookup"><span data-stu-id="e61ea-131">**3. Why does the R sample code in the Azure Machine Learning web services not work for consuming the web services in Marketplace?**</span></span>

<span data-ttu-id="e61ea-132">直接連接到 Azure Machine Learning Web 服務，相較於透過 Marketplace 連接到這些 Web 服務，有不同的驗證系統。</span><span class="sxs-lookup"><span data-stu-id="e61ea-132">The authentication systems are different when connecting to Azure Machine Learning web services directly compared to connecting to these web services through the Marketplace.</span></span> <span data-ttu-id="e61ea-133">Marketplace 中的服務是 OData 服務，而且可以使用 GET 或 POST 方法進行呼叫。</span><span class="sxs-lookup"><span data-stu-id="e61ea-133">The services in Marketplace are OData services, and they can be called with GET or POST methods.</span></span> 

<span data-ttu-id="e61ea-134">**4.為何我的 Web 服務產品的支援連結無法正確更新我的部分產品？**</span><span class="sxs-lookup"><span data-stu-id="e61ea-134">**4. Why are the support links of my web service offers not updating correctly for some of my offers?**</span></span>

<span data-ttu-id="e61ea-135">支援連結是依照發佈者而非依照產品的全域連結。</span><span class="sxs-lookup"><span data-stu-id="e61ea-135">The support links are global per publisher, not per offer.</span></span> 

<span data-ttu-id="e61ea-136">**5.如何使用 Marketplace 中的批次輸入模式來發佈 Web 服務？**</span><span class="sxs-lookup"><span data-stu-id="e61ea-136">**5. How do I publish a web service with batch input mode in Marketplace?**</span></span>

<span data-ttu-id="e61ea-137">Marketplace Web 服務目前不支援批次輸入模式。</span><span class="sxs-lookup"><span data-stu-id="e61ea-137">The batch input mode is currently not supported in Marketplace web services.</span></span>

<span data-ttu-id="e61ea-138">**6.如果我有關於成為資料發行者的問題，或在發佈過程中發生問題，我應該與誰連絡以取得協助？**</span><span class="sxs-lookup"><span data-stu-id="e61ea-138">**6. Who should I contact to get help if I have questions about becoming a data publisher, or if I have issues during publishing?**</span></span>

<span data-ttu-id="e61ea-139">如需詳細資訊，請連絡 Azure Marketplace 小組 (<mailto:datamarketbd@microsoft.com>)。</span><span class="sxs-lookup"><span data-stu-id="e61ea-139">Please contact the Azure Marketplace team at <mailto:datamarketbd@microsoft.com> for more information.</span></span>

