---
title: "Azure Marketplace 賣方指南 | Microsoft Docs"
description: "本指南適用於商務使用者和獨立軟體廠商 (ISV) 的產品經理，他們有興趣向 IT 專業人員和開發人員銷售 Azure 認證的虛擬機器映像。"
documentationcenter: 
author: rupeshazure
manager: hamidm
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: rupesk@microsoft.com
ms.robots: NOINDEX, NOFOLLOW
ms.openlocfilehash: c78708687fbb5716e3e8d62967013310d6ccc735
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="azure-marketplace-seller-guide"></a><span data-ttu-id="78f94-103">Azure Marketplace 賣方指南</span><span class="sxs-lookup"><span data-stu-id="78f94-103">Azure Marketplace seller guide</span></span>

<span data-ttu-id="78f94-104">歡迎使用 Azure Marketplace 賣方指南。</span><span class="sxs-lookup"><span data-stu-id="78f94-104">Welcome to the Azure Marketplace seller guide.</span></span> <span data-ttu-id="78f94-105">本指南針對商務使用者和獨立軟體廠商 (ISV) 的產品經理而設計，他們有興趣向 IT 專業人員和開發人員銷售 Azure 認證的虛擬機器映像。</span><span class="sxs-lookup"><span data-stu-id="78f94-105">This guide is designed for business users and product managers at independent software vendors (ISVs) who are interested in selling their Azure Certified virtual machine images to IT professionals and developers.</span></span> <span data-ttu-id="78f94-106">透過世界各地的 Azure 客戶，[Marketplace](https://azuremarketplace.microsoft.com/) 可以為您的產品提供絕佳的觸角和曝光機會。</span><span class="sxs-lookup"><span data-stu-id="78f94-106">With Azure customers located around the world, the [Marketplace](https://azuremarketplace.microsoft.com/) can provide great reach and exposure for your products.</span></span>


> [!NOTE]
> <span data-ttu-id="78f94-107">如果您有興趣將完成的軟體即服務 (SaaS) 產品銷售給商務使用者，您可以調查各種選項並將它們列在 [AppSource](https://appsource.microsoft.com) 中。</span><span class="sxs-lookup"><span data-stu-id="78f94-107">If you're interested in selling your finished software as a service (SaaS) products to business users, you can investigate options to list them in [AppSource](https://appsource.microsoft.com).</span></span>

<span data-ttu-id="78f94-108">在本指南結束時，您會知道哪裡可以找到下列主題的詳細資訊︰</span><span class="sxs-lookup"><span data-stu-id="78f94-108">By the end of this guide, you'll know where to find more detailed information on these topics:</span></span>

- <span data-ttu-id="78f94-109">什麼是 Azure Marketplace？</span><span class="sxs-lookup"><span data-stu-id="78f94-109">What is the Azure Marketplace?</span></span>
- <span data-ttu-id="78f94-110">如何判斷我的產品是否符合 Marketplace？</span><span class="sxs-lookup"><span data-stu-id="78f94-110">How do I determine if my product fits with the Marketplace?</span></span>
- <span data-ttu-id="78f94-111">在 Marketplace 上銷售的好處為何？</span><span class="sxs-lookup"><span data-stu-id="78f94-111">What are the benefits of selling on the Marketplace?</span></span>
- <span data-ttu-id="78f94-112">在 Marketplace 上銷售的必要條件 (技術和非技術性) 有哪些？</span><span class="sxs-lookup"><span data-stu-id="78f94-112">What are the prerequisites (technical and nontechnical) to sell on the Marketplace?</span></span>
- <span data-ttu-id="78f94-113">如何建置 Azure 相容的虛擬硬碟 (VHD)？</span><span class="sxs-lookup"><span data-stu-id="78f94-113">How do I build Azure-compatible virtual hard disks (VHDs)?</span></span>
- <span data-ttu-id="78f94-114">如何申請並註冊為賣方？</span><span class="sxs-lookup"><span data-stu-id="78f94-114">How do I apply and register as a seller?</span></span>
- <span data-ttu-id="78f94-115">如何建立及發佈供應項目？</span><span class="sxs-lookup"><span data-stu-id="78f94-115">How do I create and publish my offer?</span></span>
- <span data-ttu-id="78f94-116">如何上市及尋找可用的資源？</span><span class="sxs-lookup"><span data-stu-id="78f94-116">How do I go to market and find available resources?</span></span>
- <span data-ttu-id="78f94-117">Marketplace 提供哪些報告和深入解析？</span><span class="sxs-lookup"><span data-stu-id="78f94-117">What reporting and insights does the Marketplace provide?</span></span>
- <span data-ttu-id="78f94-118">哪裡可以取得說明和支援？</span><span class="sxs-lookup"><span data-stu-id="78f94-118">Where can I get help and support?</span></span>

<span data-ttu-id="78f94-119">現在就開始吧。</span><span class="sxs-lookup"><span data-stu-id="78f94-119">Let's get started.</span></span>

## <a name="whats-the-azure-marketplace"></a><span data-ttu-id="78f94-120">什麼是 Azure Marketplace？</span><span class="sxs-lookup"><span data-stu-id="78f94-120">What's the Azure Marketplace?</span></span>

<span data-ttu-id="78f94-121">Azure Marketplace 是一個線上應用程式和服務市集，可讓 ISV (包括新創公司及各個企業) 為全球的 Azure 客戶提供解決方案。</span><span class="sxs-lookup"><span data-stu-id="78f94-121">The Azure Marketplace is an online applications and services marketplace on which ISVs--from startups to enterprises--offer their solutions to Azure customers around the world.</span></span> <span data-ttu-id="78f94-122">透過 Marketplace，Azure 發行者可以將其虛擬機器映像散佈及販售給其他想要在 Azure 中快速開發其雲端應用程式和行動解決方案的專業人員。</span><span class="sxs-lookup"><span data-stu-id="78f94-122">Through the Marketplace, Azure publishers can distribute and sell their virtual machine images to other professionals who want to quickly develop their cloud-based applications and mobile solutions in Azure.</span></span> <span data-ttu-id="78f94-123">Marketplace 支援各種供應項目：從具備資料處理、資料儲存體及分析層的端對端資料分析應用程式，以至分層式電子商務應用程式 (資料、服務和網際網路)。</span><span class="sxs-lookup"><span data-stu-id="78f94-123">The Marketplace supports a range of offerings--from end-to-end data analytics applications with data processing, data storage, and analysis layers, to tiered e-commerce apps (data, service, and Internet).</span></span>

<span data-ttu-id="78f94-124">雲端客戶在搜尋解決方案來符合其獨特需求時會面臨一些挑戰。</span><span class="sxs-lookup"><span data-stu-id="78f94-124">Cloud customers face several challenges when searching for solutions to fit their unique needs.</span></span> <span data-ttu-id="78f94-125">Marketplace 提供方法來解決這些挑戰及連結客戶與創新 ISV 解決方案，如下表所說明：</span><span class="sxs-lookup"><span data-stu-id="78f94-125">The Marketplace provides a way to solve these challenges and connect customers with innovative ISV solutions, as explained in the following table:</span></span>

| <span data-ttu-id="78f94-126">客戶需求</span><span class="sxs-lookup"><span data-stu-id="78f94-126">Customer need</span></span> | <span data-ttu-id="78f94-127">Azure Marketplace 解決方案</span><span class="sxs-lookup"><span data-stu-id="78f94-127">Azure Marketplace solution</span></span> |
| --- | --- |
| <span data-ttu-id="78f94-128">要求其他雲端平台功能，以符合商務和技術需求</span><span class="sxs-lookup"><span data-stu-id="78f94-128">Demands additional cloud platform functionality to meet business and technical needs</span></span> | <span data-ttu-id="78f94-129">提供 Azure 上互補應用程式和服務的快速成長產品組合</span><span class="sxs-lookup"><span data-stu-id="78f94-129">Offers a growing portfolio of complementary applications and services on Azure</span></span> |
| <span data-ttu-id="78f94-130">發現要找到正確的應用程式或服務很具挑戰性</span><span class="sxs-lookup"><span data-stu-id="78f94-130">Finds it challenging to discover the right application or service</span></span> | <span data-ttu-id="78f94-131">讓您一次達成應用程式和服務的探索、搜尋及購買</span><span class="sxs-lookup"><span data-stu-id="78f94-131">Provides a one-stop shop to discover, search for, and purchase applications and services</span></span> |
| <span data-ttu-id="78f94-132">需要適用於第三方應用程式和服務的可調整部署機制</span><span class="sxs-lookup"><span data-stu-id="78f94-132">Needs a scalable deployment mechanism for third-party applications and services</span></span> | <span data-ttu-id="78f94-133">能夠建立及設定可調整的第三方應用程式和服務部署</span><span class="sxs-lookup"><span data-stu-id="78f94-133">Enables the creation and configuration of scalable deployments for third-party applications and services</span></span> |
| <span data-ttu-id="78f94-134">需求新的應用程式和服務與現有的解決方案整合及搭配運作</span><span class="sxs-lookup"><span data-stu-id="78f94-134">Requires new applications and services to integrate and work with existing solutions</span></span> | <span data-ttu-id="78f94-135">輕鬆地整合第三方應用程式和服務與 Azure 上的現有解決方案</span><span class="sxs-lookup"><span data-stu-id="78f94-135">Easily integrates third-party applications and services with existing solutions on Azure</span></span> |

<span data-ttu-id="78f94-136">Marketplace 讓全球客戶可以享受 Azure 合作夥伴生態系統的品質、多元選擇和優勢。</span><span class="sxs-lookup"><span data-stu-id="78f94-136">The Marketplace brings the quality, choice, and strength of the Azure partner ecosystem to global customers.</span></span> <span data-ttu-id="78f94-137">主要優點包括：</span><span class="sxs-lookup"><span data-stu-id="78f94-137">Key benefits include:</span></span>

- <span data-ttu-id="78f94-138">統一提供來自 Microsoft 和合作夥伴之以 Azure 為基礎的供應項目。</span><span class="sxs-lookup"><span data-stu-id="78f94-138">Unified location for Azure-based offerings from Microsoft and partners.</span></span>
- <span data-ttu-id="78f94-139">超過 5,000 個供應項目。</span><span class="sxs-lookup"><span data-stu-id="78f94-139">More than 5,000 offers.</span></span>
- <span data-ttu-id="78f94-140">整合式平台經驗。</span><span class="sxs-lookup"><span data-stu-id="78f94-140">Integrated platform experience.</span></span>
- <span data-ttu-id="78f94-141">流暢的設定、部署與管理。</span><span class="sxs-lookup"><span data-stu-id="78f94-141">Streamlined configuration, deployment, and management.</span></span>

## <a name="is-the-marketplace-right-for-my-business"></a><span data-ttu-id="78f94-142">Marketplace 適合我的企業嗎？</span><span class="sxs-lookup"><span data-stu-id="78f94-142">Is the Marketplace right for my business?</span></span>

<span data-ttu-id="78f94-143">您現在可能很疑惑 Azure Marketplace 是否適合您的企業。</span><span class="sxs-lookup"><span data-stu-id="78f94-143">By now you might be wondering if the Azure Marketplace is the right fit for your business.</span></span> <span data-ttu-id="78f94-144">如果適合，您可以獲得哪些好處？</span><span class="sxs-lookup"><span data-stu-id="78f94-144">And if it is, what will you get out of it?</span></span> <span data-ttu-id="78f94-145">Marketplace 可為您創造新的銷售機會：</span><span class="sxs-lookup"><span data-stu-id="78f94-145">The Marketplace creates new sales opportunities for you:</span></span>

- <span data-ttu-id="78f94-146">**在新的客戶市場中銷售擴充的 Azure 解決方案產品組合**。</span><span class="sxs-lookup"><span data-stu-id="78f94-146">**Sell into new customer markets with an expanded portfolio of solutions on Azure**.</span></span> <span data-ttu-id="78f94-147">向 Microsoft 線上訂用帳戶方案 (MOSP) 和 Microsoft 企業合約客戶追加銷售及交叉銷售 Marketplace 供應項目與 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="78f94-147">Upsell and cross-sell Marketplace offerings with Azure services that are available to Microsoft Online Subscription Program (MOSP) and Microsoft Enterprise Agreement customers.</span></span> <span data-ttu-id="78f94-148">您可以輕易地將 Marketplace 供應項目合併至您的客戶方案和 Azure 案例推銷中。</span><span class="sxs-lookup"><span data-stu-id="78f94-148">You can easily incorporate Marketplace offerings into your customer solution and Azure scenario pitch.</span></span>
- <span data-ttu-id="78f94-149">**提高商務價值並增加現有和新客戶帳戶的交易規模**。</span><span class="sxs-lookup"><span data-stu-id="78f94-149">**Enhance business value and increase deal size with existing and new customer accounts**.</span></span> <span data-ttu-id="78f94-150">Marketplace 有助於提升交易規模、處理客戶將工作負載移到雲端時遇到的難題，並增加交易獲利。</span><span class="sxs-lookup"><span data-stu-id="78f94-150">The Marketplace can help you grow deal size, address customer pain points when moving workloads to the cloud, and increase deal profitability.</span></span> <span data-ttu-id="78f94-151">您可以藉由銷售完整的解決方案來提高商務價值，以及處理 Azure 雲端平台落差，以符合客戶需求。</span><span class="sxs-lookup"><span data-stu-id="78f94-151">You increase business value by selling complete solutions and address Azure cloud platform gaps to meet customer requirements.</span></span>
- <span data-ttu-id="78f94-152">**藉由銷售 Marketplace 應用程式和服務來吸引更多的潛在客戶**。</span><span class="sxs-lookup"><span data-stu-id="78f94-152">**Appeal to a wider range of potential customers by selling Marketplace applications and services**.</span></span> <span data-ttu-id="78f94-153">Marketplace 可讓您輕鬆地尋找及留住新客戶。</span><span class="sxs-lookup"><span data-stu-id="78f94-153">The Marketplace can make it easier to find and retain new customers.</span></span> <span data-ttu-id="78f94-154">現今許多企業都需要將工作負載轉換至雲端，並適應瞬息萬變的基礎結構環境。</span><span class="sxs-lookup"><span data-stu-id="78f94-154">Many businesses today need to transition workloads to the cloud and adapt to changing infrastructure environments.</span></span> <span data-ttu-id="78f94-155">您可以提供適當的應用程式和服務，幫助他們縮減落差。</span><span class="sxs-lookup"><span data-stu-id="78f94-155">You can provide the right applications and services to help them bridge the gap.</span></span>
- <span data-ttu-id="78f94-156">**藉由搭售 Marketplace 供應項目與 Azure 服務來補充及擴充 Azure 功能**。</span><span class="sxs-lookup"><span data-stu-id="78f94-156">**Complement and extend Azure functionality by bundling Marketplace offers with Azure services**.</span></span> <span data-ttu-id="78f94-157">Marketplace 可協助您與客戶建立以案例為基礎的對話。</span><span class="sxs-lookup"><span data-stu-id="78f94-157">The Marketplace can help you frame scenario-based conversations with your customers.</span></span> <span data-ttu-id="78f94-158">您也可以藉由談論端對端解決方案來解決特定平台落差和客戶需求。</span><span class="sxs-lookup"><span data-stu-id="78f94-158">You can also address specific platform gaps and customer needs by talking about end-to-end solutions.</span></span> <span data-ttu-id="78f94-159">最後，透過銷售解決方案套件組合，您可以使用 Azure 平台生態系統來解決各種客戶問題，同時提高銷售量。</span><span class="sxs-lookup"><span data-stu-id="78f94-159">Finally, by selling solution bundles, you can use the Azure platform ecosystem to address a variety of customer issues--and increase your sales.</span></span>

## <a name="what39s-the-customer-base-for-the-marketplace"></a><span data-ttu-id="78f94-160">Marketplace 的客戶群為何？</span><span class="sxs-lookup"><span data-stu-id="78f94-160">What&#39;s the customer base for the Marketplace?</span></span>

<span data-ttu-id="78f94-161">Marketplace 的客戶非常多元。</span><span class="sxs-lookup"><span data-stu-id="78f94-161">Marketplace customers are diverse.</span></span> <span data-ttu-id="78f94-162">而且，Azure 是客戶群成長最快速的雲端提供者之一。</span><span class="sxs-lookup"><span data-stu-id="78f94-162">Also, Azure has one of the fastest-growing customer bases of all cloud providers.</span></span> <span data-ttu-id="78f94-163">您可以接觸任職於各種公司 (從新創公司以至企業)、各個產業，以及公營和私營機構的 IT 專業人員和開發人員。</span><span class="sxs-lookup"><span data-stu-id="78f94-163">You gain access to IT professionals and developers working for companies ranging from start-ups to enterprises, across industries, and in both the public and private sectors.</span></span>

## <a name="how-does-the-marketplace-work"></a><span data-ttu-id="78f94-164">Marketplace 如何運作？</span><span class="sxs-lookup"><span data-stu-id="78f94-164">How does the Marketplace work?</span></span>

<span data-ttu-id="78f94-165">其實很簡單。</span><span class="sxs-lookup"><span data-stu-id="78f94-165">It&#39;s pretty easy.</span></span> <span data-ttu-id="78f94-166">經過過核准之後，您可建立 Azure 認證虛擬機器映像，並將它發佈至 Marketplace。</span><span class="sxs-lookup"><span data-stu-id="78f94-166">After you&#39;re approved, you create your Azure Certified virtual machine image and publish it to the Marketplace.</span></span> <span data-ttu-id="78f94-167">Azure 客戶可以在其中迅速尋找、購買及部署您的產品。</span><span class="sxs-lookup"><span data-stu-id="78f94-167">There, Azure customers can find, buy, and deploy your product in minutes.</span></span> <span data-ttu-id="78f94-168">更棒的是，客戶對部署您的解決方案深具信心。</span><span class="sxs-lookup"><span data-stu-id="78f94-168">Even better, customers deploy your solution with confidence.</span></span> <span data-ttu-id="78f94-169">他們了解環境已設定完成，以便順利使用 Azure，且基礎結構也已準備好在數分鐘內投入運作。</span><span class="sxs-lookup"><span data-stu-id="78f94-169">They know that the environment is configured for success on Azure and that the infrastructure is ready to go within a few minutes.</span></span>

<span data-ttu-id="78f94-170">Cloud Partner 入口網站是在 Marketplace 上建立供應項目的中樞。</span><span class="sxs-lookup"><span data-stu-id="78f94-170">The Cloud Partner Portal is the hub for creating your offer on the Marketplace.</span></span> <span data-ttu-id="78f94-171">虛擬機器映像是預先設定的映像，包含完整安裝的作業系統以及一或多個應用程式。</span><span class="sxs-lookup"><span data-stu-id="78f94-171">Virtual machine images are preconfigured with a fully installed operating system and one or more applications.</span></span> <span data-ttu-id="78f94-172">若要認證您的映像，使其準備好進行發行，您必須符合特定必要條件。</span><span class="sxs-lookup"><span data-stu-id="78f94-172">To certify your image so that it&#39;s ready for publication, you have to meet certain prerequisites.</span></span> <span data-ttu-id="78f94-173">我們將在下一節中討論這些必要條件。</span><span class="sxs-lookup"><span data-stu-id="78f94-173">We discuss these in the next section.</span></span>


## <a name="whats-next"></a><span data-ttu-id="78f94-174">後續步驟</span><span class="sxs-lookup"><span data-stu-id="78f94-174">What's next?</span></span>

<span data-ttu-id="78f94-175">您可能會思考 Azure Marketplace 是否真的適合您的產品。</span><span class="sxs-lookup"><span data-stu-id="78f94-175">You might be thinking that the Azure Marketplace really is the right fit for your product.</span></span> <span data-ttu-id="78f94-176">所以應該如何開始呢？</span><span class="sxs-lookup"><span data-stu-id="78f94-176">So how do you get started?</span></span> <span data-ttu-id="78f94-177">本節說明如何藉由下列方式在 Marketplace 上運作 (圖 1)：</span><span class="sxs-lookup"><span data-stu-id="78f94-177">This section is all about getting up and running on the Marketplace (Figure 1) by:</span></span> 
* <span data-ttu-id="78f94-178">獲得 Azure 認證。</span><span class="sxs-lookup"><span data-stu-id="78f94-178">Becoming Azure Certified.</span></span>
* <span data-ttu-id="78f94-179">獲准銷售您的產品。</span><span class="sxs-lookup"><span data-stu-id="78f94-179">Getting approved to sell your product.</span></span>
* <span data-ttu-id="78f94-180">在 Cloud Partner 入口網站中建立供應項目。</span><span class="sxs-lookup"><span data-stu-id="78f94-180">Creating your offer in the Cloud Partner Portal.</span></span> 

![在 Azure Marketplace 上銷售的程序](./media/cloud-partner-portal-seller-guide/processforselling.png)

<span data-ttu-id="78f94-182">圖 1︰在 Azure Marketplace 上銷售的程序</span><span class="sxs-lookup"><span data-stu-id="78f94-182">Figure 1: Process for selling on the Azure Marketplace</span></span>

<span data-ttu-id="78f94-183">您要先符合一組技術性和非技術性必要條件，並準備您的虛擬機器映像。</span><span class="sxs-lookup"><span data-stu-id="78f94-183">First you meet a set of technical and nontechnical prerequisites and prepare your virtual machine image.</span></span> <span data-ttu-id="78f94-184">然後您會指定產品並註冊為賣方。</span><span class="sxs-lookup"><span data-stu-id="78f94-184">Then you nominate your product and register as a seller.</span></span> <span data-ttu-id="78f94-185">最後，您會新增行銷內容和提交進行發佈。</span><span class="sxs-lookup"><span data-stu-id="78f94-185">Finally, you add marketing content and submit for publishing.</span></span> <span data-ttu-id="78f94-186">讓供應項目在 Marketplace 上線之前，您可以在預覽/預備環境中檢閱供應項目。</span><span class="sxs-lookup"><span data-stu-id="78f94-186">You can review your offer in a preview/staging environment prior to making it live on the Marketplace.</span></span>

<span data-ttu-id="78f94-187">第一次針對 Azure Marketplace 建立供應項目時，您應該規劃大約四週的時間進行基本上架。</span><span class="sxs-lookup"><span data-stu-id="78f94-187">The first time you create an offer for the Azure Marketplace, you should plan on about four weeks for basic onboarding.</span></span> <span data-ttu-id="78f94-188">可能的話，請在供應項目推出前六週建置完成，才有足夠的時間處理媒體和發佈工作。</span><span class="sxs-lookup"><span data-stu-id="78f94-188">If possible, build in six weeks before the launch of your offer to allow time for media and publishing tasks.</span></span>

## <a name="how-do-i-become-azure-certified"></a><span data-ttu-id="78f94-189">如何獲得 Azure 認證？</span><span class="sxs-lookup"><span data-stu-id="78f94-189">How do I become Azure Certified?</span></span>

<span data-ttu-id="78f94-190">針對 Azure Marketplace 建立供應項目的第一個步驟是獲得 Azure 認證。</span><span class="sxs-lookup"><span data-stu-id="78f94-190">The first step in creating your offer for the Azure Marketplace is to become Azure Certified.</span></span> <span data-ttu-id="78f94-191">這表示要匯編公司資訊、同意參與原則、下載必要工具，以及建置技術元件 (圖 2)。</span><span class="sxs-lookup"><span data-stu-id="78f94-191">That means compiling company information, agreeing to participation policies, downloading necessary tools, and building technical components (Figure 2).</span></span>

![獲得 Azure 認證的需求](./media/cloud-partner-portal-seller-guide/azurecertified.png)

<span data-ttu-id="78f94-193">圖 2︰獲得 Azure 認證的需求</span><span class="sxs-lookup"><span data-stu-id="78f94-193">Figure 2: Requirements for becoming Azure Certified</span></span>

### <a name="technical-prerequisites"></a><span data-ttu-id="78f94-194">技術性必要條件</span><span class="sxs-lookup"><span data-stu-id="78f94-194">Technical prerequisites</span></span>

<span data-ttu-id="78f94-195">在您的產品推出之前，請仔細檢閱並符合所有的技術性必要條件。</span><span class="sxs-lookup"><span data-stu-id="78f94-195">Carefully review and meet all technical prerequisites before you launch.</span></span> <span data-ttu-id="78f94-196">您需要存取 Windows 或 Linux，以及存取連結到測試工具的 Azure 相容 VHD。</span><span class="sxs-lookup"><span data-stu-id="78f94-196">You will need access to Windows or Linux and also to Azure-compatible VHDs linked to testing tools.</span></span>

<span data-ttu-id="78f94-197">建議您使用遠端桌面通訊協定，直接在雲端開發您的 Azure VHD。</span><span class="sxs-lookup"><span data-stu-id="78f94-197">We recommend that you develop your Azure VHD directly in the cloud by using Remote Desktop Protocol.</span></span> <span data-ttu-id="78f94-198">不過，如果這是您的唯一選項，您可以使用[內部部署基礎結構](https://docs.microsoft.com/azure/marketplace-publishing/marketplace-publishing-vm-image-creation-on-premise)來下載 VHD 並進行開發。</span><span class="sxs-lookup"><span data-stu-id="78f94-198">However, if it is your only option, it&#39;s possible to download a VHD and develop it by using [on-premises infrastructure](https://docs.microsoft.com/azure/marketplace-publishing/marketplace-publishing-vm-image-creation-on-premise).</span></span>

<span data-ttu-id="78f94-199">如需詳細資訊，請參閱[技術性必要條件](https://docs.microsoft.com/azure/marketplace-publishing/marketplace-publishing-vm-image-creation-prerequisites)頁面。</span><span class="sxs-lookup"><span data-stu-id="78f94-199">For more detailed information, see the [technical prerequisites](https://docs.microsoft.com/azure/marketplace-publishing/marketplace-publishing-vm-image-creation-prerequisites) page.</span></span>

### <a name="nontechnical-prerequisites"></a><span data-ttu-id="78f94-200">非技術性必要條件</span><span class="sxs-lookup"><span data-stu-id="78f94-200">Nontechnical prerequisites</span></span>

<span data-ttu-id="78f94-201">若要成為 Marketplace 的一部分，您必須符合某些非技術性必要條件。</span><span class="sxs-lookup"><span data-stu-id="78f94-201">To become part of the Marketplace, you need to meet some nontechnical prerequisites.</span></span> <span data-ttu-id="78f94-202">首先，請檢閱並同意 [Azure Marketplace 參與原則](https://azure.microsoft.com/support/legal/marketplace/participation-policies/)的條款。</span><span class="sxs-lookup"><span data-stu-id="78f94-202">First, review and agree to the terms of the [Azure Marketplace Participation Policies](https://azure.microsoft.com/support/legal/marketplace/participation-policies/).</span></span> <span data-ttu-id="78f94-203">Marketplace 中提供的軟體和服務至少必須符合下列其中一項需求：</span><span class="sxs-lookup"><span data-stu-id="78f94-203">The software and services offered in the Marketplace must meet at least one of the following requirements:</span></span>

- <span data-ttu-id="78f94-204">**在 Azure 上執行**。</span><span class="sxs-lookup"><span data-stu-id="78f94-204">**Run on Azure**.</span></span> <span data-ttu-id="78f94-205">軟體或服務的主要功能必須在 Microsoft Azure 上執行。</span><span class="sxs-lookup"><span data-stu-id="78f94-205">The primary function of the software or service must run on Microsoft Azure.</span></span>
- <span data-ttu-id="78f94-206">**部署至 Azure**。</span><span class="sxs-lookup"><span data-stu-id="78f94-206">**Deploy to Azure**.</span></span> <span data-ttu-id="78f94-207">在清單資訊中，您必須描述如何在 Azure 上部署該軟體或服務。</span><span class="sxs-lookup"><span data-stu-id="78f94-207">In your listing information, you must describe how the software or service is deployed on Azure.</span></span>
- <span data-ttu-id="78f94-208">**整合或擴充 Azure 服務**。</span><span class="sxs-lookup"><span data-stu-id="78f94-208">**Integrate with or extend an Azure service**.</span></span> <span data-ttu-id="78f94-209">您必須在清單資訊中指出︰</span><span class="sxs-lookup"><span data-stu-id="78f94-209">You must indicate in your listing information:</span></span>
  - <span data-ttu-id="78f94-210">軟體或服務要整合或擴充哪一項 Azure 服務</span><span class="sxs-lookup"><span data-stu-id="78f94-210">Which Azure service the software or service integrates with or extends</span></span>
  - <span data-ttu-id="78f94-211">軟體或服務如何整合或擴充 Azure 服務</span><span class="sxs-lookup"><span data-stu-id="78f94-211">How the software or service integrates with or extends the Azure service</span></span>

<span data-ttu-id="78f94-212">如 Azure Marketplace 參與原則中所述，您也必須符合下列商務需求︰</span><span class="sxs-lookup"><span data-stu-id="78f94-212">You also need to meet these business requirements, as described in the Azure Marketplace Participation Policies:</span></span>

- <span data-ttu-id="78f94-213">您的公司 (或其子公司) 必須位於 Marketplace 支援的銷售來源國家/地區。</span><span class="sxs-lookup"><span data-stu-id="78f94-213">Your company (or its subsidiary) must be located in a sell-from country supported by the Marketplace.</span></span>
- <span data-ttu-id="78f94-214">您的產品授權，必須與 Marketplace 支援的計費模式相容。</span><span class="sxs-lookup"><span data-stu-id="78f94-214">Your product must be licensed in a way that is compatible with billing models supported by the Marketplace.</span></span>
- <span data-ttu-id="78f94-215">您必須以合乎商業行為的方式 (包括免費、付費或透過社群支援)，負責為客戶提供技術支援。</span><span class="sxs-lookup"><span data-stu-id="78f94-215">You are responsible for making technical support available to customers in a commercially reasonable manner, whether free, paid, or through community support.</span></span>
- <span data-ttu-id="78f94-216">您必須為您的軟體和任何第三方軟體相依性進行授權。</span><span class="sxs-lookup"><span data-stu-id="78f94-216">You are required to license your software and any third-party software dependencies.</span></span>
- <span data-ttu-id="78f94-217">為了使您的供應項目可列於 [azure.microsoft.com](../../C:/Users/Lisa.Rosenberger/Desktop/azure.microsoft.com) 和 Azure 入口網站中，您的內容必須符合某些標準。</span><span class="sxs-lookup"><span data-stu-id="78f94-217">Your content must meet certain criteria for your offering to be listed on [azure.microsoft.com](../../C:/Users/Lisa.Rosenberger/Desktop/azure.microsoft.com) and in the Azure portal.</span></span>

<span data-ttu-id="78f94-218">最後，您必須同意[使用條款](https://azure.microsoft.com/support/legal/website-terms-of-use/)、[Microsoft 隱私權聲明](http://www.microsoft.com/privacystatement/default.aspx)以及[Microsoft Azure 認證方案合約](https://azure.microsoft.com/support/legal/marketplace/certified-program-agreement/)。</span><span class="sxs-lookup"><span data-stu-id="78f94-218">Finally, you'll need to agree with the [Terms of Use](https://azure.microsoft.com/support/legal/website-terms-of-use/), [Microsoft Privacy Statement](http://www.microsoft.com/privacystatement/default.aspx), and [Microsoft Azure Certified Program Agreement](https://azure.microsoft.com/support/legal/marketplace/certified-program-agreement/).</span></span> 

<span data-ttu-id="78f94-219">如需常見問題的清單，請參閱 [Azure Marketplace 常見問題集](https://azure.microsoft.com/marketplace/faq/)。</span><span class="sxs-lookup"><span data-stu-id="78f94-219">For a list of commonly asked questions, see the [Azure Marketplace FAQ](https://azure.microsoft.com/marketplace/faq/).</span></span>


### <a name="azure-certification"></a><span data-ttu-id="78f94-220">Azure 認證</span><span class="sxs-lookup"><span data-stu-id="78f94-220">Azure certification</span></span>

<span data-ttu-id="78f94-221">取得 _Azure 認證_狀態表示成功完成上架程序。</span><span class="sxs-lookup"><span data-stu-id="78f94-221">Earning _Azure Certified_ status represents the successful completion of the onboarding process.</span></span> <span data-ttu-id="78f94-222">此狀態讓客戶有信心其 IT 專業人員和開發人員能從受信任的合作夥伴取得採用 Azure 技術的優良解決方案。</span><span class="sxs-lookup"><span data-stu-id="78f94-222">This status instills confidence in customers that their IT professionals and developers are acquiring quality solutions that run on or are built with Azure technology from a trusted partner.</span></span> <span data-ttu-id="78f94-223">Azure 認證解決方案包括︰</span><span class="sxs-lookup"><span data-stu-id="78f94-223">Azure Certified solutions include:</span></span>

- <span data-ttu-id="78f94-224">全域調查。</span><span class="sxs-lookup"><span data-stu-id="78f94-224">Global vetting.</span></span>
- <span data-ttu-id="78f94-225">判斷與 Azure 平台的相容性。</span><span class="sxs-lookup"><span data-stu-id="78f94-225">Determination of compatibility with the Azure platform.</span></span>
- <span data-ttu-id="78f94-226">線上映像安全合規性。</span><span class="sxs-lookup"><span data-stu-id="78f94-226">Online image safety compliance.</span></span>
- <span data-ttu-id="78f94-227">沒有病毒或惡意程式碼。</span><span class="sxs-lookup"><span data-stu-id="78f94-227">No viruses or malware.</span></span>
- <span data-ttu-id="78f94-228">支援的計費模式。</span><span class="sxs-lookup"><span data-stu-id="78f94-228">Supported billing models.</span></span>

## <a name="how-do-i-nominate-my-product-and-get-approved"></a><span data-ttu-id="78f94-229">如何提名我的產品並獲得核准？</span><span class="sxs-lookup"><span data-stu-id="78f94-229">How do I nominate my product and get approved?</span></span>

<span data-ttu-id="78f94-230">現在是獲得核准以在 Marketplace 上銷售產品 (圖 3) 的時候。</span><span class="sxs-lookup"><span data-stu-id="78f94-230">Now it's time to get approval to sell your product on the Marketplace (Figure 3).</span></span> <span data-ttu-id="78f94-231">Microsoft 讓您輕鬆地提名您的產品，完成發佈程序，並註冊成為賣方。</span><span class="sxs-lookup"><span data-stu-id="78f94-231">Microsoft makes it easy to nominate your product, complete the publishing process, and register as a seller.</span></span>

![獲准在 Azure Marketplace 上銷售](./media/cloud-partner-portal-seller-guide/gettingapprovedsteps.png)

<span data-ttu-id="78f94-233">圖 3：獲准在 Azure Marketplace 上銷售的步驟</span><span class="sxs-lookup"><span data-stu-id="78f94-233">Figure 3: Steps for getting approved to sell on the Azure Marketplace</span></span>

<span data-ttu-id="78f94-234">要獲得核准的第一個步驟是先[提名](https://createopportunity.azurewebsites.net/)您的產品，然後進行註冊和發佈。</span><span class="sxs-lookup"><span data-stu-id="78f94-234">The first step toward approval is to [nominate](https://createopportunity.azurewebsites.net/) your product prior to registration and publication.</span></span> <span data-ttu-id="78f94-235">核准可能需要_多達三個工作天_。</span><span class="sxs-lookup"><span data-stu-id="78f94-235">Approval can take _up to three business days_.</span></span>

<span data-ttu-id="78f94-236">一旦核准，您就會收到下列各項︰</span><span class="sxs-lookup"><span data-stu-id="78f94-236">Upon approval, you receive the following:</span></span>

- <span data-ttu-id="78f94-237">電子郵件回條，其中包含可免除 $99 美元開發中心申請費用的優惠碼以及 Cloud Partner 入口網站中的設定檔。</span><span class="sxs-lookup"><span data-stu-id="78f94-237">Email receipt with a promo code waiving the $99 application fee for the Development Center and a profile in the Cloud Partner Portal.</span></span>
- <span data-ttu-id="78f94-238">Azure 認證狀態的預先技術核准，以及用於建立供應項目及認證 VHD 的選項。</span><span class="sxs-lookup"><span data-stu-id="78f94-238">Technical preapproval for Azure Certified status, along with the option to create an offer and certify your VHD.</span></span> <span data-ttu-id="78f94-239">(您的開發中心申請必須獲得核准，您可以建立供應項目。)</span><span class="sxs-lookup"><span data-stu-id="78f94-239">(Your Development Center application must be approved before you can create your offer.)</span></span>
- <span data-ttu-id="78f94-240">用於存取 Cloud Partner 入口網站的指示以及發佈程序的概觀。</span><span class="sxs-lookup"><span data-stu-id="78f94-240">Instructions for accessing the Cloud Partner Portal and an overview of the publishing process.</span></span>
- <span data-ttu-id="78f94-241">呼叫 Microsoft 上架小組來引導程序及詢問問題的資格。</span><span class="sxs-lookup"><span data-stu-id="78f94-241">Eligibility for a call with the Microsoft onboarding team to walk through the process and ask questions.</span></span>
- <span data-ttu-id="78f94-242">發佈第二個供應項目的能力。</span><span class="sxs-lookup"><span data-stu-id="78f94-242">Ability to publish a second offer.</span></span> <span data-ttu-id="78f94-243">第二次的供應供項目不需要經過核准。</span><span class="sxs-lookup"><span data-stu-id="78f94-243">Second-time offers don&#39;t need to go through approval.</span></span> <span data-ttu-id="78f94-244">它們可以直接移至 Cloud Partner 入口網站，但虛擬機器仍必須透過發佈程序進行認證。</span><span class="sxs-lookup"><span data-stu-id="78f94-244">They can go directly to the Cloud Partner Portal, but the virtual machines still must be certified through the publishing process.</span></span>
- <span data-ttu-id="78f94-245">要求發行協助的指引。</span><span class="sxs-lookup"><span data-stu-id="78f94-245">Guidance on requesting help with publication.</span></span> <span data-ttu-id="78f94-246">(問題應導向至 Marketplace 發行者[支援連結](https://support.microsoft.com/en-us/getsupport?oaspworkflow=start_1.0.0.0&wf=0&wfName=productselection&prid=16230&ccsid=636282352448485256)。)</span><span class="sxs-lookup"><span data-stu-id="78f94-246">(Questions should be directed to the Marketplace Publisher [support link](https://support.microsoft.com/en-us/getsupport?oaspworkflow=start_1.0.0.0&wf=0&wfName=productselection&prid=16230&ccsid=636282352448485256).)</span></span>

<span data-ttu-id="78f94-247">最後，您會[將您的帳戶註冊](https://docs.microsoft.com/azure/marketplace-publishing/marketplace-publishing-accounts-creation-registration)為 Microsoft 賣方。</span><span class="sxs-lookup"><span data-stu-id="78f94-247">Finally, you [register your account](https://docs.microsoft.com/azure/marketplace-publishing/marketplace-publishing-accounts-creation-registration) as a Microsoft seller.</span></span> <span data-ttu-id="78f94-248">核准和調查可能需要_長達兩週_的時間，所以請利用這段時間在 Cloud Partner 入口網站中建立 Azure Marketplace 供應項目。</span><span class="sxs-lookup"><span data-stu-id="78f94-248">Approval and vetting can take _up to two weeks_, so use this time to create your Azure Marketplace offer in the Cloud Partner Portal.</span></span>

## <a name="how-do-i-publish-my-offer-on-the-azure-marketplace"></a><span data-ttu-id="78f94-249">如何在 Azure Marketplace 上發佈供應項目？</span><span class="sxs-lookup"><span data-stu-id="78f94-249">How do I publish my offer on the Azure Marketplace?</span></span>

<span data-ttu-id="78f94-250">您現在已準備好驗證虛擬機器映像並發佈供應項目。</span><span class="sxs-lookup"><span data-stu-id="78f94-250">You are now ready to certify your virtual machine image and publish your offer.</span></span> <span data-ttu-id="78f94-251">若要這麼做，您可使用 Cloud Partner 入口網站。</span><span class="sxs-lookup"><span data-stu-id="78f94-251">To do this, you use the Cloud Partner Portal.</span></span> <span data-ttu-id="78f94-252">您可以將 Cloud Partner 入口網站視為發佈及管理解決方案的中樞。</span><span class="sxs-lookup"><span data-stu-id="78f94-252">You can think of the Cloud Partner Portal as a hub for publishing and managing your solution.</span></span> <span data-ttu-id="78f94-253">基本上，您只需要上傳 VHD、新增行銷內容和 SKU 詳細資料，以及提交您的供應項目進行認證和檢閱。</span><span class="sxs-lookup"><span data-stu-id="78f94-253">Basically, you just need to upload your VHD, add marketing content and SKU details, and submit your offer for certification and review.</span></span> <span data-ttu-id="78f94-254">於 Marketplace 上線之前，您可以預覽供應項目並查看其外觀。</span><span class="sxs-lookup"><span data-stu-id="78f94-254">You get to preview your offer and see how it will look before going live on the Marketplace.</span></span>

## <a name="what-about-best-practices"></a><span data-ttu-id="78f94-255">關於最佳做法</span><span class="sxs-lookup"><span data-stu-id="78f94-255">What about best practices?</span></span>

<span data-ttu-id="78f94-256">以下的工具和最佳做法可協助您充分利用成為 Marketplace 賣方的優勢。</span><span class="sxs-lookup"><span data-stu-id="78f94-256">Here are some tools and best practices that can help you get the most out of being a seller on the Marketplace.</span></span>

### <a name="azure-test-drives"></a><span data-ttu-id="78f94-257">Azure 試用產品</span><span class="sxs-lookup"><span data-stu-id="78f94-257">Azure test drives</span></span>

<span data-ttu-id="78f94-258">[Azure 試用產品](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/test-drives?page=1)很適合用來向潛在客戶展示您的產品，讓他們在購買前有試用選項。</span><span class="sxs-lookup"><span data-stu-id="78f94-258">[Azure test drives](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/test-drives?page=1) are a great way to showcase your product to potential customers and give them the option to try before they buy.</span></span> <span data-ttu-id="78f94-259">試用產品有助於增加轉換及開發潛在客戶。</span><span class="sxs-lookup"><span data-stu-id="78f94-259">Test drives can help increase conversion and generate leads.</span></span>

<span data-ttu-id="78f94-260">客戶在提供其連絡資訊之後，便可以存取您預先建置的試用產品。</span><span class="sxs-lookup"><span data-stu-id="78f94-260">After providing their contact information, customers can access your prebuilt test drive.</span></span> <span data-ttu-id="78f94-261">他們可以體驗實際操作、以自學方式試用您的產品，包括在真實情況中操作主要功能並體驗各項優點。</span><span class="sxs-lookup"><span data-stu-id="78f94-261">They experience a hands-on, self-guided trial of your product&#39;s key features and benefits in a real-world scenario.</span></span>

<span data-ttu-id="78f94-262">目前只能在傳統發佈入口網站上發佈試用產品。</span><span class="sxs-lookup"><span data-stu-id="78f94-262">Currently, publishing a test drive for your product is available only on the classic publishing portal.</span></span> <span data-ttu-id="78f94-263">移至[如何發佈新的試用產品](https://github.com/Azure/AzureTestDrive/wiki)文件進一步了解。</span><span class="sxs-lookup"><span data-stu-id="78f94-263">Learn more by going to documentation on [how to publish a new test drive](https://github.com/Azure/AzureTestDrive/wiki).</span></span>

<span data-ttu-id="78f94-264">深入了解 [Azure 試用產品](https://azuremarketplace.azureedge.net/documents/azure-marketplace-test-drive-program.pdf)。</span><span class="sxs-lookup"><span data-stu-id="78f94-264">Learn more about [Azure test drives](https://azuremarketplace.azureedge.net/documents/azure-marketplace-test-drive-program.pdf).</span></span>

### <a name="go-to-market-checklist"></a><span data-ttu-id="78f94-265">上市檢查清單</span><span class="sxs-lookup"><span data-stu-id="78f94-265">Go-to-market checklist</span></span>

<span data-ttu-id="78f94-266">深入了解我們的[上市方案](https://partner.microsoft.com/go-to-market/)，有助於擴充貴組織的全球觸角。</span><span class="sxs-lookup"><span data-stu-id="78f94-266">Learn more about our [go-to-market programs](https://partner.microsoft.com/go-to-market/) that can help expand your organization&#39;s global reach.</span></span> <span data-ttu-id="78f94-267">您也可以運用[合作夥伴行銷中心](http://smartpartnermarketing.microsoft.com/isv)的資源。</span><span class="sxs-lookup"><span data-stu-id="78f94-267">You can also leverage resources at the [partner marketing center](http://smartpartnermarketing.microsoft.com/isv).</span></span>

<span data-ttu-id="78f94-268">推出之前，我們建議採取一些步驟讓您的 Marketplace 供應項目快速吸引目光。</span><span class="sxs-lookup"><span data-stu-id="78f94-268">Before your launch, we recommend taking a few steps to get rapid traction on your Marketplace offer.</span></span> <span data-ttu-id="78f94-269">使用此檢查清單，查看您是否已準備就緒︰</span><span class="sxs-lookup"><span data-stu-id="78f94-269">Use this checklist to find out if you&#39;re ready:</span></span>

- <span data-ttu-id="78f94-270">我已藉由張貼部落格文章、傳送電子郵件或發出新聞稿，**宣布在 Marketplace 上提供我的供應項目**。</span><span class="sxs-lookup"><span data-stu-id="78f94-270">**I&#39;ve announced that my offer is available on the Marketplace** by posting a blog, sending emails, or issuing a press release.</span></span>
- <span data-ttu-id="78f94-271">**我在自己的網站上促銷我的供應項目**，指引客戶前往 Marketplace 查看我的供應項目。</span><span class="sxs-lookup"><span data-stu-id="78f94-271">**I&#39;m promoting my offer on my own website**, pointing customers to my offer on the Marketplace.</span></span>
- <span data-ttu-id="78f94-272">**我已發佈試用產品**，以便客戶短暫體驗在 Azure 上即時執行的供應項目。</span><span class="sxs-lookup"><span data-stu-id="78f94-272">**I&#39;ve published a test drive** so that customers can experience my offer running live on Azure over a coffee break.</span></span>
- <span data-ttu-id="78f94-273">**我已啟用隨選潛在客戶開發**，以便每次客戶按一下來部署我的應用程式時，我會收到其名稱和連絡資訊。</span><span class="sxs-lookup"><span data-stu-id="78f94-273">**I&#39;ve enabled on-demand lead generation** so that every time a customer clicks to deploy my application, I receive their name and contact information.</span></span>
- <span data-ttu-id="78f94-274">**我已連絡我的 Microsoft 夥伴經理**(如果我有一個) 來探索其他機會。</span><span class="sxs-lookup"><span data-stu-id="78f94-274">**I&#39;ve connected with my partner manager** at Microsoft (if I have one) to explore additional opportunities.</span></span>

## <a name="what-about-reports"></a><span data-ttu-id="78f94-275">關於報告</span><span class="sxs-lookup"><span data-stu-id="78f94-275">What about reports?</span></span>

<span data-ttu-id="78f94-276">Marketplace 會提供有關訂單、使用量和客戶的報告，您可透過 Marketplace 的[發行者報告入口網站](https://reports.azure.com) 存取這些報告。</span><span class="sxs-lookup"><span data-stu-id="78f94-276">The Marketplace offers reports on your orders, usage, and customers that are accessible via the Marketplace [Publisher Reporting portal](https://reports.azure.com).</span></span> <span data-ttu-id="78f94-277">除了實用的深入解析和分析，系統還會透過可瀏覽的資料表提供未經處理的資料，並可以 CSV 或 XLS 檔案形式下載。</span><span class="sxs-lookup"><span data-stu-id="78f94-277">In addition to helpful insights and analytics, raw data is provided in a navigable table and can be downloaded as a CSV or XLS file.</span></span>

<span data-ttu-id="78f94-278">此[影片](https://player.vimeo.com/video/200859918)提供報告功能和優點搶先看，其中包含：</span><span class="sxs-lookup"><span data-stu-id="78f94-278">[This video](https://player.vimeo.com/video/200859918) gives you a sneak peek of report features and benefits, including:</span></span>

- <span data-ttu-id="78f94-279">報告類型︰首頁上的訂單、使用量及客戶趨勢的摘要快照。</span><span class="sxs-lookup"><span data-stu-id="78f94-279">Types of reports: summary snapshot of orders, usage, and customer trends on the home page.</span></span>
- <span data-ttu-id="78f94-280">詳細的訂單、使用量及客戶資料。</span><span class="sxs-lookup"><span data-stu-id="78f94-280">Detailed orders, usage, and customer data.</span></span>
- <span data-ttu-id="78f94-281">以每月摘要或六個月的趨勢檢視方式顯示訂單和使用量。</span><span class="sxs-lookup"><span data-stu-id="78f94-281">Orders and usage shown as a monthly summary or as a six-month trend view.</span></span>
- <span data-ttu-id="78f94-282">顯示為標準的數個深入解析。</span><span class="sxs-lookup"><span data-stu-id="78f94-282">Several insights shown as a standard.</span></span>
- <span data-ttu-id="78f94-283">依據下列各項顯示的使用量/訂單︰</span><span class="sxs-lookup"><span data-stu-id="78f94-283">Usage/orders by:</span></span>
  - <span data-ttu-id="78f94-284">市場</span><span class="sxs-lookup"><span data-stu-id="78f94-284">Market</span></span>
  - <span data-ttu-id="78f94-285">通道</span><span class="sxs-lookup"><span data-stu-id="78f94-285">Channel</span></span>
  - <span data-ttu-id="78f94-286">帶領潮流的供應項目</span><span class="sxs-lookup"><span data-stu-id="78f94-286">Trending offers</span></span>
  - <span data-ttu-id="78f94-287">Marketplace 授權類型</span><span class="sxs-lookup"><span data-stu-id="78f94-287">Marketplace license type</span></span>

<span data-ttu-id="78f94-288">詳細的報告會顯示客戶資訊，例如公司名稱和地理位置 (包含郵遞區號)，以供您比較客戶。</span><span class="sxs-lookup"><span data-stu-id="78f94-288">Detailed reports show customer information, like company name and geographic location down to the postal code, so you can compare your customers.</span></span> <span data-ttu-id="78f94-289">下列清單包含我們提供的客戶相關特定屬性︰</span><span class="sxs-lookup"><span data-stu-id="78f94-289">The following list includes the specific attributes we provide about your customers:</span></span>

- <span data-ttu-id="78f94-290">Reseller</span><span class="sxs-lookup"><span data-stu-id="78f94-290">Reseller</span></span>
- <span data-ttu-id="78f94-291">名字</span><span class="sxs-lookup"><span data-stu-id="78f94-291">FirstName</span></span>
- <span data-ttu-id="78f94-292">姓氏</span><span class="sxs-lookup"><span data-stu-id="78f94-292">LastName</span></span>
- <span data-ttu-id="78f94-293">電子郵件</span><span class="sxs-lookup"><span data-stu-id="78f94-293">Email</span></span>
- <span data-ttu-id="78f94-294">CompanyName</span><span class="sxs-lookup"><span data-stu-id="78f94-294">CompanyName</span></span>
- <span data-ttu-id="78f94-295">TransactionDate</span><span class="sxs-lookup"><span data-stu-id="78f94-295">TransactionDate</span></span>
- <span data-ttu-id="78f94-296">SubscriptionName</span><span class="sxs-lookup"><span data-stu-id="78f94-296">SubscriptionName</span></span>
- <span data-ttu-id="78f94-297">AzureSubscriptionId</span><span class="sxs-lookup"><span data-stu-id="78f94-297">AzureSubscriptionId</span></span>
- <span data-ttu-id="78f94-298">CloudInstanceName</span><span class="sxs-lookup"><span data-stu-id="78f94-298">CloudInstanceName</span></span>
- <span data-ttu-id="78f94-299">OrderCount</span><span class="sxs-lookup"><span data-stu-id="78f94-299">OrderCount</span></span>
- <span data-ttu-id="78f94-300">CustomerCountryRegion</span><span class="sxs-lookup"><span data-stu-id="78f94-300">CustomerCountryRegion</span></span>
- <span data-ttu-id="78f94-301">CustomerCity</span><span class="sxs-lookup"><span data-stu-id="78f94-301">CustomerCity</span></span>
- <span data-ttu-id="78f94-302">CustomerCommunicationCulture</span><span class="sxs-lookup"><span data-stu-id="78f94-302">CustomerCommunicationCulture</span></span>
- <span data-ttu-id="78f94-303">CustomerZipCode</span><span class="sxs-lookup"><span data-stu-id="78f94-303">CustomerZipCode</span></span>

<span data-ttu-id="78f94-304">我們也會透過說明文件、詞彙和錄製的示範來提供訓練。</span><span class="sxs-lookup"><span data-stu-id="78f94-304">We also offer training through Help documentation, a glossary, and a recorded demo.</span></span> <span data-ttu-id="78f94-305">如果您需要協助或支援您的報告，您可以開啟[支援票證](https://support.microsoft.com/getsupport?wf=0&tenant=ClassicCommercial&oaspworkflow=start_1.0.0.0&locale=en-us&supportregion=en-us&pesid=15635&ccsid=636233723471685249)。</span><span class="sxs-lookup"><span data-stu-id="78f94-305">If you need help or support with your reports, you can open a [support ticket](https://support.microsoft.com/getsupport?wf=0&tenant=ClassicCommercial&oaspworkflow=start_1.0.0.0&locale=en-us&supportregion=en-us&pesid=15635&ccsid=636233723471685249).</span></span>

<span data-ttu-id="78f94-306">歡迎您使用我們的 ISV 賣方社群，期待看到您的供應項目。</span><span class="sxs-lookup"><span data-stu-id="78f94-306">We welcome you to our community of ISV sellers and look forward to seeing your offer.</span></span>

---
