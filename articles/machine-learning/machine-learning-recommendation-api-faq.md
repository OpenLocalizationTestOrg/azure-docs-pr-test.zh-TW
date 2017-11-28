---
title: "向上 aaaSet 並用 hello 機器學習建議 API |Microsoft 文件"
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
redirect_document_id: True
ms.openlocfilehash: 980bf1a36f3291275d9ef0fee9b4446f7e0cbecf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-and-using-machine-learning-recommendations-api-faq"></a><span data-ttu-id="88867-103">設定和使用 Machine Learning Recommendations API 的常見問題集</span><span class="sxs-lookup"><span data-stu-id="88867-103">Setting up and using Machine Learning Recommendations API FAQ</span></span>
<span data-ttu-id="88867-104">**什麼是 RECOMMENDATIONS？**</span><span class="sxs-lookup"><span data-stu-id="88867-104">**What is RECOMMENDATIONS?**</span></span>

> [!NOTE]
> <span data-ttu-id="88867-105">您應該開始使用 hello 建議 API 認知服務，而不此版本。</span><span class="sxs-lookup"><span data-stu-id="88867-105">You should start using hello Recommendations API Cognitive Service instead of this version.</span></span> <span data-ttu-id="88867-106">hello 建議認知服務將會取代此服務，並將那里開發所有 hello 新功能。</span><span class="sxs-lookup"><span data-stu-id="88867-106">hello Recommendations Cognitive Service will be replacing this service, and all hello new features will be developed there.</span></span> <span data-ttu-id="88867-107">它會提供新功能，例如，批次支援、更好的 API 總管、更簡潔的 API 介面、更一致的註冊/計費體驗等。</span><span class="sxs-lookup"><span data-stu-id="88867-107">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span></span>
> <span data-ttu-id="88867-108">深入了解[移轉 toohello 新認知的服務](http://aka.ms/recomigrate)</span><span class="sxs-lookup"><span data-stu-id="88867-108">Learn more about [Migrating toohello new Cognitive Service](http://aka.ms/recomigrate)</span></span>
> 
> 

<span data-ttu-id="88867-109">對於組織和企業倚賴建議 toocross 銷售和向上銷售的產品和服務 tootheir 客戶，Azure Machine Learning 中的建議會提供自助式建議引擎。</span><span class="sxs-lookup"><span data-stu-id="88867-109">For organizations and businesses that rely on recommendations toocross-sell and up-sell products and services tootheir customers, RECOMMENDATIONS in Azure Machine Learning provides a self-service recommendations engine.</span></span> <span data-ttu-id="88867-110">它是協同篩選的實作，其使用矩陣分解作為核心演算法。</span><span class="sxs-lookup"><span data-stu-id="88867-110">It is an implementation of collaborative filtering that uses matrix factorization as its core algorithm.</span></span> <span data-ttu-id="88867-111">應用程式開發人員可以使用 REST API 來存取 RECOMMENDATIONS。</span><span class="sxs-lookup"><span data-stu-id="88867-111">Application developers can access RECOMMENDATIONS by using REST APIs.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="88867-112">**我可以用 RECOMMENDATIONS 來做什麼？**</span><span class="sxs-lookup"><span data-stu-id="88867-112">**What can I do with RECOMMENDATIONS?**</span></span>

<span data-ttu-id="88867-113">RECOMMENDATIONS 將一個項目或一組項目作為輸入，並傳回相關建議清單。</span><span class="sxs-lookup"><span data-stu-id="88867-113">RECOMMENDATIONS takes as input an item or a set of items and returns a list of relevant recommendations.</span></span> <span data-ttu-id="88867-114">例如：線上零售商的客戶會按一下產品。</span><span class="sxs-lookup"><span data-stu-id="88867-114">For example: A customer of an online retailer clicks a product.</span></span> <span data-ttu-id="88867-115">hello 線上零售店以輸入 tooRECOMMENDATIONS 傳送該產品、 取得一份產品清單，並決定哪些這些產品 toohello 客戶將會顯示。</span><span class="sxs-lookup"><span data-stu-id="88867-115">hello online retailer sends that product as input tooRECOMMENDATIONS, gets a list of products in return, and decides which of these products will be shown toohello customer.</span></span> <span data-ttu-id="88867-116">您可能想 toouse 建議 toooptimize 線上商店或甚至 tooinform 您的內部業務部門或呼叫的中心。</span><span class="sxs-lookup"><span data-stu-id="88867-116">You may want toouse RECOMMENDATIONS toooptimize your online store or even tooinform your inside sales department or call center.</span></span>

<span data-ttu-id="88867-117">**是否有任何使用量限制？**</span><span class="sxs-lookup"><span data-stu-id="88867-117">**Are there any usage limitations?**</span></span>

<span data-ttu-id="88867-118">建議具有下列使用量限制的 hello:</span><span class="sxs-lookup"><span data-stu-id="88867-118">Recommendations has hello following usage limitations:</span></span>

* <span data-ttu-id="88867-119">每個訂用帳戶的模型數上限：10</span><span class="sxs-lookup"><span data-stu-id="88867-119">Maximum number of models per subscription: 10</span></span>
* <span data-ttu-id="88867-120">一個目錄可保留的項目數上限：100,000</span><span class="sxs-lookup"><span data-stu-id="88867-120">Maximum number of items that a catalog can hold: 100,000</span></span>
* <span data-ttu-id="88867-121">hello 會保留的使用方式點數目上限是 ~ 5,000,000。</span><span class="sxs-lookup"><span data-stu-id="88867-121">hello maximum number of usage points that are kept is ~5,000,000.</span></span> <span data-ttu-id="88867-122">如果要上傳新的或報告，將會刪除最舊的 hello。</span><span class="sxs-lookup"><span data-stu-id="88867-122">hello oldest will be deleted if new ones will be uploaded or reported.</span></span>
* <span data-ttu-id="88867-123">電子郵件中可以傳送的資料 (例如，匯入目錄資料、匯入使用量資料) 大小上限為 200 MB</span><span class="sxs-lookup"><span data-stu-id="88867-123">Maximum size of data that can be sent in email (for example, import catalog data, import usage data) is 200 MB</span></span>
* <span data-ttu-id="88867-124">未作用中之建議項目模型組建的每秒交易數 (TPS) 為 ~2 TPS。</span><span class="sxs-lookup"><span data-stu-id="88867-124">Number of transactions per second (TPS) for a Recommendations model build that is not active is ~2 TPS.</span></span> <span data-ttu-id="88867-125">作用中的建議模型組建可以阻擋 too20 TPS。</span><span class="sxs-lookup"><span data-stu-id="88867-125">A Recommendations model build that is active can hold up too20 TPS.</span></span>

## <a name="purchase-and-billing"></a><span data-ttu-id="88867-126">購買和計費</span><span class="sxs-lookup"><span data-stu-id="88867-126">Purchase and Billing</span></span>
<span data-ttu-id="88867-127">**建議多少 hello 啟動期間成本？**</span><span class="sxs-lookup"><span data-stu-id="88867-127">**How much does Recommendations cost during hello launch period?**</span></span>

<span data-ttu-id="88867-128">Recommendations 是一項以訂用帳戶為基礎的服務。</span><span class="sxs-lookup"><span data-stu-id="88867-128">Recommendations is a subscription-based service.</span></span> <span data-ttu-id="88867-129">收費是根據每個月的交易量來進行。</span><span class="sxs-lookup"><span data-stu-id="88867-129">Charging is based on volume of transactions per month.</span></span> <span data-ttu-id="88867-130">您可以檢查 hello[提供頁面](https://datamarket.azure.com/dataset/amla/recommendations)在 Microsoft Azure Marketplace 以取得價格資訊。</span><span class="sxs-lookup"><span data-stu-id="88867-130">You can check hello [offer page](https://datamarket.azure.com/dataset/amla/recommendations) in Microsoft Azure Marketplace for pricing information.</span></span>

<span data-ttu-id="88867-131">**讓 Recommendations 為我追蹤和儲存使用者活動是否有任何相關聯的成本？**</span><span class="sxs-lookup"><span data-stu-id="88867-131">**Are there any costs associated with having Recommendations track and store user activity for me?**</span></span>

<span data-ttu-id="88867-132">不在 hello 的時刻。</span><span class="sxs-lookup"><span data-stu-id="88867-132">Not at hello moment.</span></span>

<span data-ttu-id="88867-133">**Recommendations 是否有免費試用版？**</span><span class="sxs-lookup"><span data-stu-id="88867-133">**Does Recommendations have a free trial?**</span></span>

<span data-ttu-id="88867-134">沒有可用的記錄也就是限制的 too10，000 每月的交易。</span><span class="sxs-lookup"><span data-stu-id="88867-134">There is a free trail which is restricted too10,000 transactions per month.</span></span>

<span data-ttu-id="88867-135">**Recommendations 何時會計費？**</span><span class="sxs-lookup"><span data-stu-id="88867-135">**When will I be billed for Recommendations?**</span></span>

<span data-ttu-id="88867-136">付費的訂用帳戶就是任何按月計價的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="88867-136">A paid subscription is any subscription for which there is a monthly fee.</span></span> <span data-ttu-id="88867-137">當您購買付費訂用帳戶時，您需立即支付 hello 第一次月的使用。</span><span class="sxs-lookup"><span data-stu-id="88867-137">When you purchase a paid subscription, you are immediately charged for hello first month's use.</span></span> <span data-ttu-id="88867-138">您需要付費 hello 訂閱頁面 （加上適用稅額） 上的 hello 供應項目相關聯的 hello 數量。</span><span class="sxs-lookup"><span data-stu-id="88867-138">You are charged hello amount that is associated with hello offer on hello subscription page (plus applicable taxes).</span></span> <span data-ttu-id="88867-139">此每月費用是每個月對的 hello 相同行事曆依照原始購買日期，直到您取消 hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="88867-139">This monthly charge is made each month on hello same calendar date as your original purchase until you cancel hello subscription.</span></span> 

<span data-ttu-id="88867-140">**如何升級 tooa 較高的層服務？**</span><span class="sxs-lookup"><span data-stu-id="88867-140">**How do I upgrade tooa higher tier service?**</span></span>

<span data-ttu-id="88867-141">您可以購買或更新您的訂用帳戶，從 hello[提供頁面](https://datamarket.azure.com/dataset/amla/recommendations)Microsoft Azure Marketplace 上的頁面。</span><span class="sxs-lookup"><span data-stu-id="88867-141">You can buy or update your subscription from hello [offer page](https://datamarket.azure.com/dataset/amla/recommendations) page on Microsoft Azure Marketplace.</span></span>

<span data-ttu-id="88867-142">當您升級訂用帳戶時：</span><span class="sxs-lookup"><span data-stu-id="88867-142">When you upgrade a subscription:</span></span>

* <span data-ttu-id="88867-143">為舊訂用剩餘的交易不會新增 tooyour 新訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="88867-143">Transactions that are remaining on your old subscription are not added tooyour new subscription.</span></span> 
* <span data-ttu-id="88867-144">您需支付完整價格 hello 新訂用帳戶，即使您有未使用的交易，在舊訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="88867-144">You pay full price for hello new subscription, even though you have unused transactions on your old subscription.</span></span>

<span data-ttu-id="88867-145">處理序 tooupgrade 訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="88867-145">Process tooupgrade a subscription:</span></span>

* <span data-ttu-id="88867-146">Nevigate toohello[提供頁面](https://datamarket.azure.com/dataset/amla/recommendations)。</span><span class="sxs-lookup"><span data-stu-id="88867-146">Nevigate toohello [offer page](https://datamarket.azure.com/dataset/amla/recommendations).</span></span>
* <span data-ttu-id="88867-147">如果您未登入 toohello Marketplace 中登入。</span><span class="sxs-lookup"><span data-stu-id="88867-147">Sign in toohello Marketplace if you aren't already Signed in.</span></span>
* <span data-ttu-id="88867-148">Hello 右窗格中，會列出所有的 hello 可用的方案。</span><span class="sxs-lookup"><span data-stu-id="88867-148">In hello right pane, all hello available plans are listed.</span></span> <span data-ttu-id="88867-149">按一下您想要 tooupgrade hello 計劃的 hello 選項按鈕。</span><span class="sxs-lookup"><span data-stu-id="88867-149">Click hello radio button for hello plan you want tooupgrade to.</span></span>
* <span data-ttu-id="88867-150">如果您想 tooupgrade，按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="88867-150">If you want tooupgrade, click **OK**.</span></span> <span data-ttu-id="88867-151">如果您不想 tooupgrade，按一下**取消**。</span><span class="sxs-lookup"><span data-stu-id="88867-151">If you do not want tooupgrade, click **Cancel**.</span></span>

<span data-ttu-id="88867-152">**重要**仔細閱讀的 hello 對話方塊然後再升級因為計費和使用的含意。</span><span class="sxs-lookup"><span data-stu-id="88867-152">**Important** Carefully read hello dialog box before you upgrade because there are billing and use implications.</span></span>

<span data-ttu-id="88867-153">**何時我的訂用帳戶 tooRecommendations 將結束？**</span><span class="sxs-lookup"><span data-stu-id="88867-153">**When will my subscription tooRecommendations end?**</span></span>

<span data-ttu-id="88867-154">您的訂用帳戶會在您取消時結束。</span><span class="sxs-lookup"><span data-stu-id="88867-154">Your subscription will end when you cancel it.</span></span> <span data-ttu-id="88867-155">如果您想要 toocancel 訂用帳戶，請參閱下列指示的 hello。</span><span class="sxs-lookup"><span data-stu-id="88867-155">If you would like toocancel your subscriptions, see hello following instructions.</span></span>

<span data-ttu-id="88867-156">**如何取消我的 Recommendations 訂用帳戶？**</span><span class="sxs-lookup"><span data-stu-id="88867-156">**How do I cancel my Recommendations subscription?**</span></span>

<span data-ttu-id="88867-157">您的訂用帳戶中，而使用 hello 遵循步驟 toocancel。</span><span class="sxs-lookup"><span data-stu-id="88867-157">toocancel your subscription, use hello following steps.</span></span> <span data-ttu-id="88867-158">如果您目前的訂用帳戶是付費訂用帳戶，訂用帳戶會作用中持續直到 hello hello 目前計費週期結束為止。</span><span class="sxs-lookup"><span data-stu-id="88867-158">If your current subscription is a paid subscription, your subscription continues in effect until hello end of hello current billing period.</span></span> <span data-ttu-id="88867-159">如果您需要立即 hello 取消 toobe 有效，請與我們連絡[Microsoft 支援服務](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn)。</span><span class="sxs-lookup"><span data-stu-id="88867-159">If you need hello cancellation toobe effective immediately, contact us at [Microsoft Support](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn).</span></span>

<span data-ttu-id="88867-160">**請注意**如果您在計費期間或未使用的交易 hello 結束之前取消計費期間內不提供任何退款。</span><span class="sxs-lookup"><span data-stu-id="88867-160">**Note** No refund is given if you cancel before hello end of a billing period or for unused transactions in a billing period.</span></span>

* <span data-ttu-id="88867-161">瀏覽 toohello[提供頁面](https://datamarket.azure.com/dataset/amla/recommendations)。</span><span class="sxs-lookup"><span data-stu-id="88867-161">Navigate toohello [offer page](https://datamarket.azure.com/dataset/amla/recommendations).</span></span>
* <span data-ttu-id="88867-162">如果您未登入 toohello Marketplace 中登入。</span><span class="sxs-lookup"><span data-stu-id="88867-162">Sign in toohello Marketplace if you aren't already Signed in.</span></span>
* <span data-ttu-id="88867-163">按一下**取消**toohello hello 資料集名稱和狀態的權限。</span><span class="sxs-lookup"><span data-stu-id="88867-163">Click **Cancel** toohello right of hello dataset name and status.</span></span> <span data-ttu-id="88867-164">您可以使用此訂用帳戶，直到 hello 結尾 hello 目前計費週期或交易限制為止 （何者先發生）。</span><span class="sxs-lookup"><span data-stu-id="88867-164">You can use this subscription until hello end of hello current billing period or your transaction limit is reached (whichever occurs first).</span></span>

<span data-ttu-id="88867-165">如果您想要訂用帳戶，因此您可以購買新的訂閱，立即提出票證申請在 toocancel [Microsoft 支援服務](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn)。</span><span class="sxs-lookup"><span data-stu-id="88867-165">If you would like toocancel your subscription immediately so you can purchase a new subscription, file a ticket at [Microsoft Support](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn).</span></span>

## <a name="getting-started-with-recommendations"></a><span data-ttu-id="88867-166">開始使用 Recommendations</span><span class="sxs-lookup"><span data-stu-id="88867-166">Getting started with Recommendations</span></span>
<span data-ttu-id="88867-167">**Recommendations 是給我的嗎？**</span><span class="sxs-lookup"><span data-stu-id="88867-167">**Is Recommendations for me?**</span></span> 

<span data-ttu-id="88867-168">Machine Learning 中的建議適用於組織和依賴建議 toocross 銷售和向上銷售的產品或服務 tootheir 客戶的公司。</span><span class="sxs-lookup"><span data-stu-id="88867-168">Recommendations in Machine Learning is for organizations and businesses that rely on recommendations toocross-sell and up-sell products or services tootheir customers.</span></span> <span data-ttu-id="88867-169">如果您有面向客戶的網站、銷售團隊、內部銷售團隊或客服中心，而且如果您提供的目錄有好幾十項產品或服務 – 您的盈餘即可受惠於使用 Recommendations。</span><span class="sxs-lookup"><span data-stu-id="88867-169">If you have a customer-facing website, a sales force, an inside sales force, or a call center, and if you offer a catalog of more than a few dozen products or services, your bottom line may benefit from using Recommendations.</span></span> 

<span data-ttu-id="88867-170">實驗順利進行建議是設計的 toobe 相當簡單。</span><span class="sxs-lookup"><span data-stu-id="88867-170">Experimenting with Recommendations is designed toobe fairly simple.</span></span> <span data-ttu-id="88867-171">hello 目前 API 架構版本需要基本程式設計技巧。</span><span class="sxs-lookup"><span data-stu-id="88867-171">hello current API-based version requires basic programming skills.</span></span> <span data-ttu-id="88867-172">如果您需要協助，請連絡 hello 廠商開發您的網站。</span><span class="sxs-lookup"><span data-stu-id="88867-172">If you need assistance, contact hello vendor who developed your website.</span></span> <span data-ttu-id="88867-173">如果您有內部的 IT 部門或公司內部的開發人員，則應該讓您能夠 tooget 建議 toowork。</span><span class="sxs-lookup"><span data-stu-id="88867-173">If you have an internal IT department or an in-house developer, they should be able tooget Recommendations toowork for you.</span></span> 

<span data-ttu-id="88867-174">**Hello 設定建議的必要條件為何？**</span><span class="sxs-lookup"><span data-stu-id="88867-174">**What are hello prerequisites for setting up Recommendations?**</span></span>

<span data-ttu-id="88867-175">建議需要您有使用者選項的記錄檔，在關聯 tooyour 類別目錄。</span><span class="sxs-lookup"><span data-stu-id="88867-175">Recommendations requires that you have a log of user choices as it relates tooyour catalog.</span></span> <span data-ttu-id="88867-176">如果您沒有這類記錄檔，而您確實有面向客戶的網站，則 Recommendations 可以為您收集使用者活動。</span><span class="sxs-lookup"><span data-stu-id="88867-176">If you don't have such a log and you do have a customer facing website, Recommendations can collect user activity for you.</span></span> 

<span data-ttu-id="88867-177">Recommendations 也需要您的產品或服務目錄。</span><span class="sxs-lookup"><span data-stu-id="88867-177">Recommendations also requires a catalog of your products or services.</span></span> <span data-ttu-id="88867-178">如果您沒有 hello 類別目錄，建議使用 hello 實際客戶使用量資料並抽出類別目錄。</span><span class="sxs-lookup"><span data-stu-id="88867-178">If you don't have hello catalog, Recommendations can use hello actual customer usage data and distill a catalog.</span></span> <span data-ttu-id="88867-179">隱含目錄不會包含未在使用者交易中回報的項目。</span><span class="sxs-lookup"><span data-stu-id="88867-179">An implied catalog will not include items that were not reported as part of user transactions.</span></span>

<span data-ttu-id="88867-180">**如何設定建議 hello 第一次？**</span><span class="sxs-lookup"><span data-stu-id="88867-180">**How do I set up Recommendations for hello first time?**</span></span>

<span data-ttu-id="88867-181">之後[訂閱](https://datamarket.azure.com/dataset/amla/recommendations)tooRecommendations，您應該使用 hello API 文件以 hello [Azure 機器學習建議快速入門指南](machine-learning-recommendation-api-quick-start-guide.md)tooset hello 服務。</span><span class="sxs-lookup"><span data-stu-id="88867-181">After [subscribing](https://datamarket.azure.com/dataset/amla/recommendations) tooRecommendations, you should use hello API documentation in hello [Azure Machine Learning Recommendations - Quick Start Guide](machine-learning-recommendation-api-quick-start-guide.md) tooset up hello service.</span></span>

<span data-ttu-id="88867-182">**哪裡可以找到 API 文件？**</span><span class="sxs-lookup"><span data-stu-id="88867-182">**Where can I find API documentation?**</span></span> 

<span data-ttu-id="88867-183">hello API 文件是[Azure 機器學習建議-快速入門指南](machine-learning-recommendation-api-quick-start-guide.md)。</span><span class="sxs-lookup"><span data-stu-id="88867-183">hello API documentation is [Azure Machine Learning Recommendations -Quick Start Guide](machine-learning-recommendation-api-quick-start-guide.md).</span></span>

<span data-ttu-id="88867-184">**選項的作用為何我有 tooupload 類別目錄和使用方式資料 tooRecommendations 嗎？**</span><span class="sxs-lookup"><span data-stu-id="88867-184">**What options do I have tooupload catalog and usage data tooRecommendations?**</span></span>

<span data-ttu-id="88867-185">您有兩種方式來上傳您的類別目錄和使用量資料： 您可以從您的 CRM 系統或其他記錄檔匯出 hello 資料，並將它上傳 tooRecommendations，或者您可以加入標記 tooyour 網站，將追蹤使用者活動。</span><span class="sxs-lookup"><span data-stu-id="88867-185">You have two options for uploading your catalog and usage data: You can export hello data from your CRM system or other logs and upload it tooRecommendations, or you can add tags tooyour website that will track user activities.</span></span> <span data-ttu-id="88867-186">如果您使用 hello 第二個方法，hello 資料會儲存在 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="88867-186">If you use hello latter method, hello data will be stored in Azure.</span></span>

## <a name="maintenance-and-support"></a><span data-ttu-id="88867-187">維護與支援</span><span class="sxs-lookup"><span data-stu-id="88867-187">Maintenance and support</span></span>
<span data-ttu-id="88867-188">**我可以有多大的資料集？**</span><span class="sxs-lookup"><span data-stu-id="88867-188">**How large can my data set be?**</span></span>

<span data-ttu-id="88867-189">每個資料集可以包含 too100，000 類別目錄項目和註冊 too2048 MB 的使用量資料。</span><span class="sxs-lookup"><span data-stu-id="88867-189">Each data set can contain up too100,000 catalog items and up too2048 MB of usage data.</span></span>
<span data-ttu-id="88867-190">此外，訂閱可以包含設定 too10 資料組 （模型）。</span><span class="sxs-lookup"><span data-stu-id="88867-190">In addition, a subscription can contain up too10 data sets (models).</span></span>

<span data-ttu-id="88867-191">**哪裡可以取得 Recommendations 的技術支援？**</span><span class="sxs-lookup"><span data-stu-id="88867-191">**Where can I get technical support for Recommendations?**</span></span>

<span data-ttu-id="88867-192">技術支援人員並用於 hello [Microsoft Azure 支援](https://social.msdn.microsoft.com/forums/azure/home?forum=MachineLearning)站台。</span><span class="sxs-lookup"><span data-stu-id="88867-192">Technical support is available on hello [Microsoft Azure Support](https://social.msdn.microsoft.com/forums/azure/home?forum=MachineLearning) site.</span></span>

<span data-ttu-id="88867-193">**哪裡可以找到 hello 使用條款？**</span><span class="sxs-lookup"><span data-stu-id="88867-193">**Where can I find hello terms of use?**</span></span>

<span data-ttu-id="88867-194">[Microsoft Azure Machine Learning Recommendations API 服務條款](https://datamarket.azure.com/dataset/amla/recommendations#terms)。</span><span class="sxs-lookup"><span data-stu-id="88867-194">[Microsoft Azure Machine Learning Recommendations API Terms of Service](https://datamarket.azure.com/dataset/amla/recommendations#terms).</span></span>

