---
title: "設定和使用 Machine Learning Recommendations API | Microsoft Docs"
description: "以 Azure Machine Learning 建置之 Microsoft RECOMMENDATIONS API 的常見問題集"
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: 1ffc3c16-e040-4225-9d72-105129938dfa
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: luisca
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: TRUE
ms.openlocfilehash: 3851589818bb8f4309bf3c65f17b115e0dcd27fa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="setting-up-and-using-machine-learning-recommendations-api-faq"></a><span data-ttu-id="1ede9-103">設定和使用 Machine Learning Recommendations API 的常見問題集</span><span class="sxs-lookup"><span data-stu-id="1ede9-103">Setting up and using Machine Learning Recommendations API FAQ</span></span>
<span data-ttu-id="1ede9-104">**什麼是 RECOMMENDATIONS？**</span><span class="sxs-lookup"><span data-stu-id="1ede9-104">**What is RECOMMENDATIONS?**</span></span>

> [!NOTE]
> <span data-ttu-id="1ede9-105">您應該開始使用 Recommendations API 的 Cognitive Service，而不是此版本。</span><span class="sxs-lookup"><span data-stu-id="1ede9-105">You should start using the Recommendations API Cognitive Service instead of this version.</span></span> <span data-ttu-id="1ede9-106">Recommendations 的 Cognitive Service 將會取代這個服務，而所有的新特徵都會在其中進行開發。</span><span class="sxs-lookup"><span data-stu-id="1ede9-106">The Recommendations Cognitive Service will be replacing this service, and all the new features will be developed there.</span></span> <span data-ttu-id="1ede9-107">它會提供新功能，例如，批次支援、更好的 API 總管、更簡潔的 API 介面、更一致的註冊/計費體驗等。</span><span class="sxs-lookup"><span data-stu-id="1ede9-107">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span></span>
> <span data-ttu-id="1ede9-108">深入了解 [移轉到新的 Cognitive Service](http://aka.ms/recomigrate)</span><span class="sxs-lookup"><span data-stu-id="1ede9-108">Learn more about [Migrating to the new Cognitive Service](http://aka.ms/recomigrate)</span></span>
> 
> 

<span data-ttu-id="1ede9-109">對於依賴建議對客戶進行交叉銷售和向上銷售產品和服務的組織和企業，Azure Machine Learning 的 RECOMMENDATIONS 可提供自助建議引擎。</span><span class="sxs-lookup"><span data-stu-id="1ede9-109">For organizations and businesses that rely on recommendations to cross-sell and up-sell products and services to their customers, RECOMMENDATIONS in Azure Machine Learning provides a self-service recommendations engine.</span></span> <span data-ttu-id="1ede9-110">它是協同篩選的實作，其使用矩陣分解作為核心演算法。</span><span class="sxs-lookup"><span data-stu-id="1ede9-110">It is an implementation of collaborative filtering that uses matrix factorization as its core algorithm.</span></span> <span data-ttu-id="1ede9-111">應用程式開發人員可以使用 REST API 來存取 RECOMMENDATIONS。</span><span class="sxs-lookup"><span data-stu-id="1ede9-111">Application developers can access RECOMMENDATIONS by using REST APIs.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="1ede9-112">**我可以用 RECOMMENDATIONS 來做什麼？**</span><span class="sxs-lookup"><span data-stu-id="1ede9-112">**What can I do with RECOMMENDATIONS?**</span></span>

<span data-ttu-id="1ede9-113">RECOMMENDATIONS 將一個項目或一組項目作為輸入，並傳回相關建議清單。</span><span class="sxs-lookup"><span data-stu-id="1ede9-113">RECOMMENDATIONS takes as input an item or a set of items and returns a list of relevant recommendations.</span></span> <span data-ttu-id="1ede9-114">例如：線上零售商的客戶會按一下產品。</span><span class="sxs-lookup"><span data-stu-id="1ede9-114">For example: A customer of an online retailer clicks a product.</span></span> <span data-ttu-id="1ede9-115">線上零售商會將該產品當作輸入傳送至 RECOMMENDATIONS，取得回報的產品清單，並決定要向客戶顯示哪些產品。</span><span class="sxs-lookup"><span data-stu-id="1ede9-115">The online retailer sends that product as input to RECOMMENDATIONS, gets a list of products in return, and decides which of these products will be shown to the customer.</span></span> <span data-ttu-id="1ede9-116">您可以使用 RECOMMENDATIONS 來最佳化您的線上商店，或甚至通知您的內部銷售部門或客服中心。</span><span class="sxs-lookup"><span data-stu-id="1ede9-116">You may want to use RECOMMENDATIONS to optimize your online store or even to inform your inside sales department or call center.</span></span>

<span data-ttu-id="1ede9-117">**是否有任何使用量限制？**</span><span class="sxs-lookup"><span data-stu-id="1ede9-117">**Are there any usage limitations?**</span></span>

<span data-ttu-id="1ede9-118">建議項目具有下列使用限制：</span><span class="sxs-lookup"><span data-stu-id="1ede9-118">Recommendations has the following usage limitations:</span></span>

* <span data-ttu-id="1ede9-119">每個訂用帳戶的模型數上限：10</span><span class="sxs-lookup"><span data-stu-id="1ede9-119">Maximum number of models per subscription: 10</span></span>
* <span data-ttu-id="1ede9-120">一個目錄可保留的項目數上限：100,000</span><span class="sxs-lookup"><span data-stu-id="1ede9-120">Maximum number of items that a catalog can hold: 100,000</span></span>
* <span data-ttu-id="1ede9-121">保留的使用點數上限是 ~5,000,000。</span><span class="sxs-lookup"><span data-stu-id="1ede9-121">The maximum number of usage points that are kept is ~5,000,000.</span></span> <span data-ttu-id="1ede9-122">如果將上傳或回報新的點，就會將最舊的點刪除。</span><span class="sxs-lookup"><span data-stu-id="1ede9-122">The oldest will be deleted if new ones will be uploaded or reported.</span></span>
* <span data-ttu-id="1ede9-123">電子郵件中可以傳送的資料 (例如，匯入目錄資料、匯入使用量資料) 大小上限為 200 MB</span><span class="sxs-lookup"><span data-stu-id="1ede9-123">Maximum size of data that can be sent in email (for example, import catalog data, import usage data) is 200 MB</span></span>
* <span data-ttu-id="1ede9-124">未作用中之建議項目模型組建的每秒交易數 (TPS) 為 ~2 TPS。</span><span class="sxs-lookup"><span data-stu-id="1ede9-124">Number of transactions per second (TPS) for a Recommendations model build that is not active is ~2 TPS.</span></span> <span data-ttu-id="1ede9-125">作用中 Recommendations 模型組建可以保留高達 20 TPS。</span><span class="sxs-lookup"><span data-stu-id="1ede9-125">A Recommendations model build that is active can hold up to 20 TPS.</span></span>

## <a name="purchase-and-billing"></a><span data-ttu-id="1ede9-126">購買和計費</span><span class="sxs-lookup"><span data-stu-id="1ede9-126">Purchase and Billing</span></span>
<span data-ttu-id="1ede9-127">**在推出期間，Recommendations 的價格為何？**</span><span class="sxs-lookup"><span data-stu-id="1ede9-127">**How much does Recommendations cost during the launch period?**</span></span>

<span data-ttu-id="1ede9-128">Recommendations 是一項以訂用帳戶為基礎的服務。</span><span class="sxs-lookup"><span data-stu-id="1ede9-128">Recommendations is a subscription-based service.</span></span> <span data-ttu-id="1ede9-129">收費是根據每個月的交易量來進行。</span><span class="sxs-lookup"><span data-stu-id="1ede9-129">Charging is based on volume of transactions per month.</span></span> <span data-ttu-id="1ede9-130">如需定價資訊，您可以在 Microsoft Azure Marketplace 中查看 [提供項目頁面](https://datamarket.azure.com/dataset/amla/recommendations) 。</span><span class="sxs-lookup"><span data-stu-id="1ede9-130">You can check the [offer page](https://datamarket.azure.com/dataset/amla/recommendations) in Microsoft Azure Marketplace for pricing information.</span></span>

<span data-ttu-id="1ede9-131">**讓 Recommendations 為我追蹤和儲存使用者活動是否有任何相關聯的成本？**</span><span class="sxs-lookup"><span data-stu-id="1ede9-131">**Are there any costs associated with having Recommendations track and store user activity for me?**</span></span>

<span data-ttu-id="1ede9-132">目前沒有。</span><span class="sxs-lookup"><span data-stu-id="1ede9-132">Not at the moment.</span></span>

<span data-ttu-id="1ede9-133">**Recommendations 是否有免費試用版？**</span><span class="sxs-lookup"><span data-stu-id="1ede9-133">**Does Recommendations have a free trial?**</span></span>

<span data-ttu-id="1ede9-134">免費試用版限制在每個月 10000 筆交易。</span><span class="sxs-lookup"><span data-stu-id="1ede9-134">There is a free trail which is restricted to 10,000 transactions per month.</span></span>

<span data-ttu-id="1ede9-135">**Recommendations 何時會計費？**</span><span class="sxs-lookup"><span data-stu-id="1ede9-135">**When will I be billed for Recommendations?**</span></span>

<span data-ttu-id="1ede9-136">付費的訂用帳戶就是任何按月計價的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="1ede9-136">A paid subscription is any subscription for which there is a monthly fee.</span></span> <span data-ttu-id="1ede9-137">當您購買付費的訂用帳戶時，我們會立即向您收取第一個月的使用費用。</span><span class="sxs-lookup"><span data-stu-id="1ede9-137">When you purchase a paid subscription, you are immediately charged for the first month's use.</span></span> <span data-ttu-id="1ede9-138">您需支付訂用帳戶頁面上提供項目旁邊顯示的相關金額 (加上適用稅額)。</span><span class="sxs-lookup"><span data-stu-id="1ede9-138">You are charged the amount that is associated with the offer on the subscription page (plus applicable taxes).</span></span> <span data-ttu-id="1ede9-139">這筆每月費用會每個月在與您原先購買相同的行事曆日期收取，直到您取消訂用帳戶為止。</span><span class="sxs-lookup"><span data-stu-id="1ede9-139">This monthly charge is made each month on the same calendar date as your original purchase until you cancel the subscription.</span></span> 

<span data-ttu-id="1ede9-140">**如何升級至較高層的服務？**</span><span class="sxs-lookup"><span data-stu-id="1ede9-140">**How do I upgrade to a higher tier service?**</span></span>

<span data-ttu-id="1ede9-141">您可以在 Microsoft Azure Marketplace 上透過 [提供項目頁面](https://datamarket.azure.com/dataset/amla/recommendations) 頁面來購買或更新您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="1ede9-141">You can buy or update your subscription from the [offer page](https://datamarket.azure.com/dataset/amla/recommendations) page on Microsoft Azure Marketplace.</span></span>

<span data-ttu-id="1ede9-142">當您升級訂用帳戶時：</span><span class="sxs-lookup"><span data-stu-id="1ede9-142">When you upgrade a subscription:</span></span>

* <span data-ttu-id="1ede9-143">舊訂用帳戶剩餘的交易不會加至新的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="1ede9-143">Transactions that are remaining on your old subscription are not added to your new subscription.</span></span> 
* <span data-ttu-id="1ede9-144">即使您的舊訂用帳戶有未使用的交易，仍需支付新訂用帳戶的完整價格。</span><span class="sxs-lookup"><span data-stu-id="1ede9-144">You pay full price for the new subscription, even though you have unused transactions on your old subscription.</span></span>

<span data-ttu-id="1ede9-145">升級訂用帳戶的程序：</span><span class="sxs-lookup"><span data-stu-id="1ede9-145">Process to upgrade a subscription:</span></span>

* <span data-ttu-id="1ede9-146">導覽至 [提供項目頁面](https://datamarket.azure.com/dataset/amla/recommendations)。</span><span class="sxs-lookup"><span data-stu-id="1ede9-146">Nevigate to the [offer page](https://datamarket.azure.com/dataset/amla/recommendations).</span></span>
* <span data-ttu-id="1ede9-147">如果您還沒有登入，請登入 Marketplace。</span><span class="sxs-lookup"><span data-stu-id="1ede9-147">Sign in to the Marketplace if you aren't already Signed in.</span></span>
* <span data-ttu-id="1ede9-148">在右窗格中，會列出所有可用的計畫。</span><span class="sxs-lookup"><span data-stu-id="1ede9-148">In the right pane, all the available plans are listed.</span></span> <span data-ttu-id="1ede9-149">按一下您要升級至的計劃的選項按鈕。</span><span class="sxs-lookup"><span data-stu-id="1ede9-149">Click the radio button for the plan you want to upgrade to.</span></span>
* <span data-ttu-id="1ede9-150">如果您想要升級，請按一下 [ **確定**]。</span><span class="sxs-lookup"><span data-stu-id="1ede9-150">If you want to upgrade, click **OK**.</span></span> <span data-ttu-id="1ede9-151">如果您不想要升級，請按一下 [ **取消**]。</span><span class="sxs-lookup"><span data-stu-id="1ede9-151">If you do not want to upgrade, click **Cancel**.</span></span>

<span data-ttu-id="1ede9-152">**重要事項** ：升級前，請先仔細閱讀對話方塊，因為其中有計費和使用暗示。</span><span class="sxs-lookup"><span data-stu-id="1ede9-152">**Important** Carefully read the dialog box before you upgrade because there are billing and use implications.</span></span>

<span data-ttu-id="1ede9-153">**我的 Recommendations 訂用帳戶何時會結束？**</span><span class="sxs-lookup"><span data-stu-id="1ede9-153">**When will my subscription to Recommendations end?**</span></span>

<span data-ttu-id="1ede9-154">您的訂用帳戶會在您取消時結束。</span><span class="sxs-lookup"><span data-stu-id="1ede9-154">Your subscription will end when you cancel it.</span></span> <span data-ttu-id="1ede9-155">如果您想要取消您的訂用帳戶，請參閱下列指示。</span><span class="sxs-lookup"><span data-stu-id="1ede9-155">If you would like to cancel your subscriptions, see the following instructions.</span></span>

<span data-ttu-id="1ede9-156">**如何取消我的 Recommendations 訂用帳戶？**</span><span class="sxs-lookup"><span data-stu-id="1ede9-156">**How do I cancel my Recommendations subscription?**</span></span>

<span data-ttu-id="1ede9-157">若要取消您的訂用帳戶，請使用下列步驟。</span><span class="sxs-lookup"><span data-stu-id="1ede9-157">To cancel your subscription, use the following steps.</span></span> <span data-ttu-id="1ede9-158">如果您目前的訂用帳戶是付費的訂用帳戶，則您的訂用帳戶會持續有效，直到目前的計費期間結束為止。</span><span class="sxs-lookup"><span data-stu-id="1ede9-158">If your current subscription is a paid subscription, your subscription continues in effect until the end of the current billing period.</span></span> <span data-ttu-id="1ede9-159">如果您需要取消立即生效，請透過 [Microsoft 支援](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn)與我們連絡。</span><span class="sxs-lookup"><span data-stu-id="1ede9-159">If you need the cancellation to be effective immediately, contact us at [Microsoft Support](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn).</span></span>

<span data-ttu-id="1ede9-160">**附註** ：如果您在計費期間結束前取消，或對於計費期間內未使用的交易，均不會提供退款。</span><span class="sxs-lookup"><span data-stu-id="1ede9-160">**Note** No refund is given if you cancel before the end of a billing period or for unused transactions in a billing period.</span></span>

* <span data-ttu-id="1ede9-161">導覽至 [提供項目頁面](https://datamarket.azure.com/dataset/amla/recommendations)。</span><span class="sxs-lookup"><span data-stu-id="1ede9-161">Navigate to the [offer page](https://datamarket.azure.com/dataset/amla/recommendations).</span></span>
* <span data-ttu-id="1ede9-162">如果您還沒有登入，請登入 Marketplace。</span><span class="sxs-lookup"><span data-stu-id="1ede9-162">Sign in to the Marketplace if you aren't already Signed in.</span></span>
* <span data-ttu-id="1ede9-163">按一下資料集名稱和狀態右邊的 [ **取消** ]。</span><span class="sxs-lookup"><span data-stu-id="1ede9-163">Click **Cancel** to the right of the dataset name and status.</span></span> <span data-ttu-id="1ede9-164">您可以使用此訂用帳戶，直到目前的計費期間結束或達到您的交易限制為止 (以較早發生者為準)。</span><span class="sxs-lookup"><span data-stu-id="1ede9-164">You can use this subscription until the end of the current billing period or your transaction limit is reached (whichever occurs first).</span></span>

<span data-ttu-id="1ede9-165">如果您想要立即取消訂用帳戶，以便購買新的訂用帳戶，請透過 [Microsoft 支援](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn)提出票證。</span><span class="sxs-lookup"><span data-stu-id="1ede9-165">If you would like to cancel your subscription immediately so you can purchase a new subscription, file a ticket at [Microsoft Support](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn).</span></span>

## <a name="getting-started-with-recommendations"></a><span data-ttu-id="1ede9-166">開始使用 Recommendations</span><span class="sxs-lookup"><span data-stu-id="1ede9-166">Getting started with Recommendations</span></span>
<span data-ttu-id="1ede9-167">**Recommendations 是給我的嗎？**</span><span class="sxs-lookup"><span data-stu-id="1ede9-167">**Is Recommendations for me?**</span></span> 

<span data-ttu-id="1ede9-168">機器學習服務中的 Recommendations 適用於依賴建議向客戶進行交叉銷售和向上銷售產品或服務的組織和企業。</span><span class="sxs-lookup"><span data-stu-id="1ede9-168">Recommendations in Machine Learning is for organizations and businesses that rely on recommendations to cross-sell and up-sell products or services to their customers.</span></span> <span data-ttu-id="1ede9-169">如果您有面向客戶的網站、銷售團隊、內部銷售團隊或客服中心，而且如果您提供的目錄有好幾十項產品或服務 – 您的盈餘即可受惠於使用 Recommendations。</span><span class="sxs-lookup"><span data-stu-id="1ede9-169">If you have a customer-facing website, a sales force, an inside sales force, or a call center, and if you offer a catalog of more than a few dozen products or services, your bottom line may benefit from using Recommendations.</span></span> 

<span data-ttu-id="1ede9-170">實驗 Recommendations 的設計相當簡單。</span><span class="sxs-lookup"><span data-stu-id="1ede9-170">Experimenting with Recommendations is designed to be fairly simple.</span></span> <span data-ttu-id="1ede9-171">目前的 API 版本可執行必要的基本程式設計技能。</span><span class="sxs-lookup"><span data-stu-id="1ede9-171">The current API-based version requires basic programming skills.</span></span> <span data-ttu-id="1ede9-172">如需協助，請連絡您網站的開發廠商。</span><span class="sxs-lookup"><span data-stu-id="1ede9-172">If you need assistance, contact the vendor who developed your website.</span></span> <span data-ttu-id="1ede9-173">如果您有內部 IT 部門或內部的開發人員，他們應可為您取得 Recommendations。</span><span class="sxs-lookup"><span data-stu-id="1ede9-173">If you have an internal IT department or an in-house developer, they should be able to get Recommendations to work for you.</span></span> 

<span data-ttu-id="1ede9-174">**設定 Recommendations 的必要條件為何？**</span><span class="sxs-lookup"><span data-stu-id="1ede9-174">**What are the prerequisites for setting up Recommendations?**</span></span>

<span data-ttu-id="1ede9-175">Recommendations 要求您有與您的目錄相關的使用者選擇記錄檔。</span><span class="sxs-lookup"><span data-stu-id="1ede9-175">Recommendations requires that you have a log of user choices as it relates to your catalog.</span></span> <span data-ttu-id="1ede9-176">如果您沒有這類記錄檔，而您確實有面向客戶的網站，則 Recommendations 可以為您收集使用者活動。</span><span class="sxs-lookup"><span data-stu-id="1ede9-176">If you don't have such a log and you do have a customer facing website, Recommendations can collect user activity for you.</span></span> 

<span data-ttu-id="1ede9-177">Recommendations 也需要您的產品或服務目錄。</span><span class="sxs-lookup"><span data-stu-id="1ede9-177">Recommendations also requires a catalog of your products or services.</span></span> <span data-ttu-id="1ede9-178">如果您沒有目錄，Recommendations 可以使用實際的客戶使用資料並摘錄成目錄。</span><span class="sxs-lookup"><span data-stu-id="1ede9-178">If you don't have the catalog, Recommendations can use the actual customer usage data and distill a catalog.</span></span> <span data-ttu-id="1ede9-179">隱含目錄不會包含未在使用者交易中回報的項目。</span><span class="sxs-lookup"><span data-stu-id="1ede9-179">An implied catalog will not include items that were not reported as part of user transactions.</span></span>

<span data-ttu-id="1ede9-180">**我如何在第一次設定 Recommendations？**</span><span class="sxs-lookup"><span data-stu-id="1ede9-180">**How do I set up Recommendations for the first time?**</span></span>

<span data-ttu-id="1ede9-181">[訂閱](https://datamarket.azure.com/dataset/amla/recommendations) Recommendations 之後，您應該使用 [Azure Machine Learning Recommendations - 快速入門指南](machine-learning-recommendation-api-quick-start-guide.md)中的 API 文件來設定服務。</span><span class="sxs-lookup"><span data-stu-id="1ede9-181">After [subscribing](https://datamarket.azure.com/dataset/amla/recommendations) to Recommendations, you should use the API documentation in the [Azure Machine Learning Recommendations - Quick Start Guide](machine-learning-recommendation-api-quick-start-guide.md) to set up the service.</span></span>

<span data-ttu-id="1ede9-182">**哪裡可以找到 API 文件？**</span><span class="sxs-lookup"><span data-stu-id="1ede9-182">**Where can I find API documentation?**</span></span> 

<span data-ttu-id="1ede9-183">API 文件是 [Azure Machine Learning Recommendations - 快速入門指南](machine-learning-recommendation-api-quick-start-guide.md)。</span><span class="sxs-lookup"><span data-stu-id="1ede9-183">The API documentation is [Azure Machine Learning Recommendations -Quick Start Guide](machine-learning-recommendation-api-quick-start-guide.md).</span></span>

<span data-ttu-id="1ede9-184">**有哪些選項可將目錄和使用資料上傳至 Recommendations？**</span><span class="sxs-lookup"><span data-stu-id="1ede9-184">**What options do I have to upload catalog and usage data to Recommendations?**</span></span>

<span data-ttu-id="1ede9-185">您有兩個選項可以上傳您的目錄和使用量資料：您可以從 CRM 系統或其他記錄檔匯出資料，並將它上傳至 Recommendations，或您可以將會追蹤使用者活動的標記加入至您的網站。</span><span class="sxs-lookup"><span data-stu-id="1ede9-185">You have two options for uploading your catalog and usage data: You can export the data from your CRM system or other logs and upload it to Recommendations, or you can add tags to your website that will track user activities.</span></span> <span data-ttu-id="1ede9-186">如果您使用第二個方法，資料會儲存在 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="1ede9-186">If you use the latter method, the data will be stored in Azure.</span></span>

## <a name="maintenance-and-support"></a><span data-ttu-id="1ede9-187">維護與支援</span><span class="sxs-lookup"><span data-stu-id="1ede9-187">Maintenance and support</span></span>
<span data-ttu-id="1ede9-188">**我可以有多大的資料集？**</span><span class="sxs-lookup"><span data-stu-id="1ede9-188">**How large can my data set be?**</span></span>

<span data-ttu-id="1ede9-189">每個資料集可包含多達 100000 個目錄項目以及高達 2048 MB 的使用資料。</span><span class="sxs-lookup"><span data-stu-id="1ede9-189">Each data set can contain up to 100,000 catalog items and up to 2048 MB of usage data.</span></span>
<span data-ttu-id="1ede9-190">此外，一個訂用帳戶最多可包含 10 個資料集 (模型)。</span><span class="sxs-lookup"><span data-stu-id="1ede9-190">In addition, a subscription can contain up to 10 data sets (models).</span></span>

<span data-ttu-id="1ede9-191">**哪裡可以取得 Recommendations 的技術支援？**</span><span class="sxs-lookup"><span data-stu-id="1ede9-191">**Where can I get technical support for Recommendations?**</span></span>

<span data-ttu-id="1ede9-192">技術支援可在 [Microsoft Azure 支援](https://social.msdn.microsoft.com/forums/azure/home?forum=MachineLearning) 網站取得。</span><span class="sxs-lookup"><span data-stu-id="1ede9-192">Technical support is available on the [Microsoft Azure Support](https://social.msdn.microsoft.com/forums/azure/home?forum=MachineLearning) site.</span></span>

<span data-ttu-id="1ede9-193">**哪裡可以找到使用條款？**</span><span class="sxs-lookup"><span data-stu-id="1ede9-193">**Where can I find the terms of use?**</span></span>

<span data-ttu-id="1ede9-194">[Microsoft Azure Machine Learning Recommendations API 服務條款](https://datamarket.azure.com/dataset/amla/recommendations#terms)。</span><span class="sxs-lookup"><span data-stu-id="1ede9-194">[Microsoft Azure Machine Learning Recommendations API Terms of Service](https://datamarket.azure.com/dataset/amla/recommendations#terms).</span></span>

