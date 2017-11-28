---
title: "Marketplace 中 Azure 受管理的應用程式 | Microsoft Docs"
description: "描述可透過 Marketplace 取得的 Azure 受管理應用程式。"
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/09/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: 58ac7665abf7e75a43bb0b92bdf6f41005c3efe8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="azure-managed-applications-in-the-marketplace"></a><span data-ttu-id="e1b3b-103">Marketplace 中 Azure 受管理的應用程式</span><span class="sxs-lookup"><span data-stu-id="e1b3b-103">Azure managed applications in the Marketplace</span></span>

 <span data-ttu-id="e1b3b-104">MSP、ISV 和系統整合業者 (SI) 可以使用 Azure 受管理的應用程式，將其解決方案提供給所有 Azure Marketplace 客戶。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-104">MSPs, ISVs, and system integrators (SIs) can use Azure managed applications to offer their solutions to all Azure Marketplace customers.</span></span> <span data-ttu-id="e1b3b-105">這類解決方案能減少客戶的維護與服務額外負荷。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-105">Such solutions reduce the maintenance and servicing overhead for customers.</span></span> <span data-ttu-id="e1b3b-106">發行者可以透過 Marketplace 銷售基礎結構和軟體。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-106">Publishers can sell infrastructure and software through the Marketplace.</span></span> <span data-ttu-id="e1b3b-107">他們可以將服務和操作支援附加至受管的應用程式。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-107">They can attach services and operational support to managed applications.</span></span> <span data-ttu-id="e1b3b-108">如需詳細資訊，請參閱[受管理的應用程式概觀](managed-application-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-108">For more information, see [Managed application overview](managed-application-overview.md).</span></span>

<span data-ttu-id="e1b3b-109">這篇文章說明 MSP、ISV 或 SI 如何將應用程式發行至 Marketplace，並將它廣泛提供給客戶。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-109">This article explains how an MSP, ISV, or SI can publish an application to the Marketplace and make it broadly available to customers.</span></span>

## <a name="prerequisites-for-publishing-a-managed-application"></a><span data-ttu-id="e1b3b-110">發行受管理應用程式的必要條件</span><span class="sxs-lookup"><span data-stu-id="e1b3b-110">Prerequisites for publishing a managed application</span></span>

<span data-ttu-id="e1b3b-111">列於 Marketplace 的必要條件：</span><span class="sxs-lookup"><span data-stu-id="e1b3b-111">Prerequisites to listing in the Marketplace:</span></span>

* <span data-ttu-id="e1b3b-112">技術需求</span><span class="sxs-lookup"><span data-stu-id="e1b3b-112">Technical</span></span>

    *  <span data-ttu-id="e1b3b-113">如需 Azure Resource Manager 範本基本結構和語法的詳細資訊，請參閱 [Azure Resource Manager 範本](resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-113">For information about the basic structure and syntax of Azure Resource Manager templates, see [Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
    *  <span data-ttu-id="e1b3b-114">若要檢視完整範本解決方案，請參閱 [Azure 快速入門範本](https://azure.microsoft.com/en-us/documentation/templates/)或[快速入門範本存放庫](https://github.com/azure/azure-quickstart-templates)。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-114">To view complete template solutions, see [Azure Quickstart templates](https://azure.microsoft.com/en-us/documentation/templates/) or the [Quickstart template repository](https://github.com/azure/azure-quickstart-templates).</span></span>
    *  <span data-ttu-id="e1b3b-115">如需如何建立介面讓客戶透過 Marketplace 部署應用程式的詳細資訊，請參閱[建立使用者介面定義檔](managed-application-createuidefinition-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-115">For information about how to create the interface for customers who deploy your application through the Marketplace, see [Create a user interface definition file](managed-application-createuidefinition-overview.md).</span></span>

* <span data-ttu-id="e1b3b-116">非技術性 (商務需求)</span><span class="sxs-lookup"><span data-stu-id="e1b3b-116">Nontechnical (business requirements)</span></span>

    *   <span data-ttu-id="e1b3b-117">您的公司或其子公司必須位於 Marketplace 支援銷售的國家/地區。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-117">Your company or its subsidiary must be located in a country where sales are supported by the Marketplace.</span></span>
    *   <span data-ttu-id="e1b3b-118">您的產品授權，必須與 Marketplace 支援的計費模式相容。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-118">Your product must be licensed in a way that is compatible with billing models supported by the Marketplace.</span></span>
    *   <span data-ttu-id="e1b3b-119">您必須以合乎商業行為的方式，負責為客戶提供技術支援。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-119">You're responsible for making technical support available to customers in a commercially reasonable manner.</span></span> <span data-ttu-id="e1b3b-120">支援可以為免費、付費，或透過社群支援。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-120">The support can be free, paid, or through community support.</span></span>
    *   <span data-ttu-id="e1b3b-121">您必須負責為您的軟體和任何第三方廠商相依性進行授權。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-121">You're responsible for licensing your software and any third-party software dependencies.</span></span>
    *   <span data-ttu-id="e1b3b-122">為了使您的供應項目可列於 Marketplace 和 Azure 入口網站中，您提供的內容必須符合標準。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-122">You must provide content that meets criteria for your offering to be listed in the Marketplace and in the Azure portal.</span></span>
    *   <span data-ttu-id="e1b3b-123">您必須同意 Azure Marketplace 參與原則和發行者合約中的條款。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-123">You must agree to the terms of the Azure Marketplace Participation Policies and Publisher Agreement.</span></span>
    *   <span data-ttu-id="e1b3b-124">您必須同意遵守使用條款、Microsoft 隱私權聲明以及 Microsoft Azure 認證方案合約。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-124">You must agree to comply with the Terms of Use, Microsoft Privacy Statement, and Microsoft Azure Certified Program Agreement.</span></span>

## <a name="create-a-new-azure-application-offer"></a><span data-ttu-id="e1b3b-125">建立新的 Azure 應用程式供應項目</span><span class="sxs-lookup"><span data-stu-id="e1b3b-125">Create a new Azure application offer</span></span>

<span data-ttu-id="e1b3b-126">符合先決條件之後，您就可以建立受管理的應用程式供應項目。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-126">After you meet the prerequisites, you're ready to create your managed application offer.</span></span> <span data-ttu-id="e1b3b-127">讓我們先快速概觀供應項目和 SKU。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-127">Let's take a quick overview of an offer and a SKU.</span></span>

### <a name="offer"></a><span data-ttu-id="e1b3b-128">提供項目</span><span class="sxs-lookup"><span data-stu-id="e1b3b-128">Offer</span></span>

<span data-ttu-id="e1b3b-129">受管理應用程式的供應項目對應至發行者提供的產品分類供應項目。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-129">The offer for a managed application corresponds to a class of product offering from a publisher.</span></span> <span data-ttu-id="e1b3b-130">如果您有想要在 Marketplace 中提供的新解決方案/應用程式類型，可以將它設定為新的供應項目。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-130">If you have a new type of solution/application that you want to make available in the Marketplace, you can set it up as a new offer.</span></span> <span data-ttu-id="e1b3b-131">優惠 SKU 的集合。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-131">An offer is a collection of SKUs.</span></span> <span data-ttu-id="e1b3b-132">每個供應項目會以個別實體出現在 Marketplace。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-132">Every offer appears as its own entity in the Marketplace.</span></span>

### <a name="sku"></a><span data-ttu-id="e1b3b-133">SKU</span><span class="sxs-lookup"><span data-stu-id="e1b3b-133">SKU</span></span>

<span data-ttu-id="e1b3b-134">SKU 是優惠的最小購買單位。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-134">A SKU is the smallest purchasable unit of an offer.</span></span> <span data-ttu-id="e1b3b-135">您可以使用相同產品類別 (供應項目) 內的 SKU 來區分：</span><span class="sxs-lookup"><span data-stu-id="e1b3b-135">You can use a SKU within the same product class (offer) to differentiate between:</span></span>

* <span data-ttu-id="e1b3b-136">所支援的不同功能。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-136">Different features that are supported.</span></span>
* <span data-ttu-id="e1b3b-137">供應項目為受管理或不受管理。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-137">Whether the offer is managed or unmanaged.</span></span>
* <span data-ttu-id="e1b3b-138">支援的計費模型。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-138">Billing models that are supported.</span></span>

<span data-ttu-id="e1b3b-139">SKU 會顯示在 Marketplace 中的父供應項目底下。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-139">A SKU appears under the parent offer in the Marketplace.</span></span> <span data-ttu-id="e1b3b-140">它會在 Azure 入口網站中顯示為自己的可購買實體。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-140">It appears as its own purchasable entity in the Azure portal.</span></span>

### <a name="set-up-an-offer"></a><span data-ttu-id="e1b3b-141">設定供應項目</span><span class="sxs-lookup"><span data-stu-id="e1b3b-141">Set up an offer</span></span>

1. <span data-ttu-id="e1b3b-142">登入 [Cloud Partner 入口網站](https://cloudpartner.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-142">Sign in to the [Cloud Partner portal](https://cloudpartner.azure.com/).</span></span>

2. <span data-ttu-id="e1b3b-143">在左側瀏覽窗格中，選取 [+ 新增優惠] > **[Azure 應用程式]**。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-143">In the navigation pane on the left, select **+ New offer** > **Azure Applications**.</span></span>

    ![新增供應項目](./media/managed-application-author-marketplace/newOffer.png)

3. <span data-ttu-id="e1b3b-145">填寫顯示在 [編輯器] 檢視左側的表單。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-145">Fill out the forms that appear on the left in the **Editor** view.</span></span> <span data-ttu-id="e1b3b-146">必填欄位會標示紅色星號 (*)。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-146">Required fields are marked with a red asterisk (*).</span></span>

    ![供應項目](./media/managed-application-author-marketplace/newOffer_OfferSettings.png)

    <span data-ttu-id="e1b3b-148">有四個主要表單用來建立受管理的應用程式︰</span><span class="sxs-lookup"><span data-stu-id="e1b3b-148">Four main forms are used to create a managed application:</span></span>

    <span data-ttu-id="e1b3b-149">a.</span><span class="sxs-lookup"><span data-stu-id="e1b3b-149">a.</span></span> <span data-ttu-id="e1b3b-150">優惠設定</span><span class="sxs-lookup"><span data-stu-id="e1b3b-150">Offer Settings</span></span>

    <span data-ttu-id="e1b3b-151">b.</span><span class="sxs-lookup"><span data-stu-id="e1b3b-151">b.</span></span> <span data-ttu-id="e1b3b-152">SKU</span><span class="sxs-lookup"><span data-stu-id="e1b3b-152">SKUs</span></span>

    <span data-ttu-id="e1b3b-153">c.</span><span class="sxs-lookup"><span data-stu-id="e1b3b-153">c.</span></span> <span data-ttu-id="e1b3b-154">Marketplace</span><span class="sxs-lookup"><span data-stu-id="e1b3b-154">Marketplace</span></span>

    <span data-ttu-id="e1b3b-155">d.</span><span class="sxs-lookup"><span data-stu-id="e1b3b-155">d.</span></span> <span data-ttu-id="e1b3b-156">支援</span><span class="sxs-lookup"><span data-stu-id="e1b3b-156">Support</span></span>

<span data-ttu-id="e1b3b-157">這些表單將於下列各節中詳細說明。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-157">These forms are described in greater detail in the following sections.</span></span>

## <a name="offer-settings-form"></a><span data-ttu-id="e1b3b-158">供應項目設定表單</span><span class="sxs-lookup"><span data-stu-id="e1b3b-158">Offer Settings form</span></span>
<span data-ttu-id="e1b3b-159">使用此基本表單來指定供應項目設定。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-159">Use this basic form to specify the offer settings.</span></span>

1. <span data-ttu-id="e1b3b-160">填寫 [供應項目設定] 表單。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-160">Fill in the **Offer Settings** form.</span></span> <span data-ttu-id="e1b3b-161">下列說明各個不同欄位：</span><span class="sxs-lookup"><span data-stu-id="e1b3b-161">The different fields are:</span></span>

    <span data-ttu-id="e1b3b-162">a.</span><span class="sxs-lookup"><span data-stu-id="e1b3b-162">a.</span></span> <span data-ttu-id="e1b3b-163">**供應項目 ID** - 此唯一識別碼可識別發行者設定檔內的供應項目。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-163">**Offer ID**: This unique identifier identifies the offer within a publisher profile.</span></span> <span data-ttu-id="e1b3b-164">此識別碼會顯示在產品的 URL，Resource Manager 範本和計費報告中。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-164">This ID is visible in product URLs, Resource Manager templates, and billing reports.</span></span> <span data-ttu-id="e1b3b-165">此識別碼只能包含小寫英數字元或連字號 (-)。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-165">It can only be composed of lowercase alphanumeric characters or dashes (-).</span></span> <span data-ttu-id="e1b3b-166">識別碼不能以連字號結尾。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-166">The ID can't end in a dash.</span></span> <span data-ttu-id="e1b3b-167">最多不能超過 50 個字元。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-167">It's limited to a maximum of 50 characters.</span></span> <span data-ttu-id="e1b3b-168">供應項目上架後，此欄位便會鎖住。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-168">After an offer goes live, this field is locked.</span></span>

    <span data-ttu-id="e1b3b-169">b.</span><span class="sxs-lookup"><span data-stu-id="e1b3b-169">b.</span></span> <span data-ttu-id="e1b3b-170">**發行者 ID**：使用此下拉式表單，選擇您想要在哪個發行者設定檔之下發佈此供應項目。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-170">**Publisher ID**: Use this drop-down list to choose the publisher profile you want to publish this offer under.</span></span> <span data-ttu-id="e1b3b-171">供應項目上架後，此欄位便會鎖住。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-171">After an offer goes live, this field is locked.</span></span>

    <span data-ttu-id="e1b3b-172">c.</span><span class="sxs-lookup"><span data-stu-id="e1b3b-172">c.</span></span> <span data-ttu-id="e1b3b-173">**名稱**：供應項目的這個顯示名稱會出現在 Marketplace 和入口網站中。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-173">**Name**: This display name for your offer appears in the Marketplace and in the portal.</span></span> <span data-ttu-id="e1b3b-174">它最多不能超過 50 個字元。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-174">It can have a maximum of 50 characters.</span></span> <span data-ttu-id="e1b3b-175">包含產品的可辨識品牌名稱。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-175">Include a recognizable brand name for your product.</span></span> <span data-ttu-id="e1b3b-176">請勿在此包含您的公司名稱，除非這是行銷方式。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-176">Don't include your company name here unless that's how it's marketed.</span></span> <span data-ttu-id="e1b3b-177">如果您在自己的網站行銷此供應項目，請確認名稱與您網站顯示的名稱相同。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-177">If you're marketing this offer on your own website, ensure that the name is exactly how it appears on your website.</span></span>

2. <span data-ttu-id="e1b3b-178">選取 [儲存] 儲存您的進度。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-178">Select **Save** to save your progress.</span></span> 

## <a name="skus-form"></a><span data-ttu-id="e1b3b-179">SKU 表單</span><span class="sxs-lookup"><span data-stu-id="e1b3b-179">SKUs form</span></span>
<span data-ttu-id="e1b3b-180">下一個步驟是為您的供應項目新增 SKU。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-180">The next step is to add SKUs for your offer.</span></span>

1. <span data-ttu-id="e1b3b-181">選取 [SKU] > [新增 SKU]。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-181">Select **SKUs** > **New SKU**.</span></span> 

    ![選取新的 SKU](./media/managed-application-author-marketplace/newOffer_skus.png)

2. <span data-ttu-id="e1b3b-183">輸入 [SKU 識別碼]。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-183">Enter a **SKU ID**.</span></span> <span data-ttu-id="e1b3b-184">SKU 識別碼是在供應項目內 SKU 的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-184">A SKU ID is a unique identifier for the SKU within an offer.</span></span> <span data-ttu-id="e1b3b-185">此識別碼會顯示在產品的 URL，Resource Manager 範本和計費報告中。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-185">This ID is visible in product URLs, Resource Manager templates, and billing reports.</span></span> <span data-ttu-id="e1b3b-186">此識別碼只能包含小寫英數字元或連字號 (-)。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-186">It can only be composed of lowercase alphanumeric characters or dashes (-).</span></span> <span data-ttu-id="e1b3b-187">此識別碼不能以連字號結尾，且最多不能超過 50 個字元。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-187">The ID can't end in a dash, and it's limited to a maximum of 50 characters.</span></span> <span data-ttu-id="e1b3b-188">供應項目上架後，此欄位便會鎖住。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-188">After an offer goes live, this field is locked.</span></span> <span data-ttu-id="e1b3b-189">您可以在一個優惠內建立多個 SKU。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-189">You can have multiple SKUs within an offer.</span></span> <span data-ttu-id="e1b3b-190">您預計發佈的每個映像都需要 SKU。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-190">You need a SKU for each image you plan to publish.</span></span>

3. <span data-ttu-id="e1b3b-191">填寫下列表單上的 [SKU 詳細資料] 區段：</span><span class="sxs-lookup"><span data-stu-id="e1b3b-191">Fill out the **SKU Details** section on the following form:</span></span>

    ![提供新的 SKU](./media/managed-application-author-marketplace/newOffer_newsku.png)

    <span data-ttu-id="e1b3b-193">填寫下列欄位：</span><span class="sxs-lookup"><span data-stu-id="e1b3b-193">Fill out the following fields:</span></span>
    
    <span data-ttu-id="e1b3b-194">a.</span><span class="sxs-lookup"><span data-stu-id="e1b3b-194">a.</span></span> <span data-ttu-id="e1b3b-195">**標題**：輸入此 SKU 的標題。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-195">**Title**: Enter a title for this SKU.</span></span> <span data-ttu-id="e1b3b-196">此標題顯示在此項目的資源庫中。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-196">This title appears in the gallery for this item.</span></span>

    <span data-ttu-id="e1b3b-197">b.</span><span class="sxs-lookup"><span data-stu-id="e1b3b-197">b.</span></span> <span data-ttu-id="e1b3b-198">**摘要**：輸入此 SKU 的簡短摘要。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-198">**Summary**: Enter a short summary for this SKU.</span></span> <span data-ttu-id="e1b3b-199">此文字會出現在標題底下。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-199">This text appears underneath the title.</span></span>

    <span data-ttu-id="e1b3b-200">c.</span><span class="sxs-lookup"><span data-stu-id="e1b3b-200">c.</span></span> <span data-ttu-id="e1b3b-201">**描述**：提供有關 SKU 的詳細描述。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-201">**Description**: Enter a detailed description about the SKU.</span></span>

    <span data-ttu-id="e1b3b-202">d.</span><span class="sxs-lookup"><span data-stu-id="e1b3b-202">d.</span></span> <span data-ttu-id="e1b3b-203">**SKU 類型**：允許的值包括 [受管理的應用程式] 和 [解決方案範本]。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-203">**SKU Type**: The allowed values are **Managed Application** and **Solution Templates**.</span></span> <span data-ttu-id="e1b3b-204">此案例中，選取 [受管理的應用程式]。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-204">For this case, select **Managed Application**.</span></span>

4. <span data-ttu-id="e1b3b-205">填寫下列表單上的 [套件詳細資料] 區段：</span><span class="sxs-lookup"><span data-stu-id="e1b3b-205">Fill out the **Package Details** section on the following form:</span></span>

    ![Package](./media/managed-application-author-marketplace/newOffer_newsku_package.png)

    <span data-ttu-id="e1b3b-207">填寫下列欄位：</span><span class="sxs-lookup"><span data-stu-id="e1b3b-207">Fill out the following fields:</span></span>

    <span data-ttu-id="e1b3b-208">a.</span><span class="sxs-lookup"><span data-stu-id="e1b3b-208">a.</span></span> <span data-ttu-id="e1b3b-209">**目前的版本**：輸入您上傳的套件版本。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-209">**Current Version**: Enter a version for the package you upload.</span></span> <span data-ttu-id="e1b3b-210">其格式應該是 `{number}.{number}.{number}{number}`。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-210">It should be in the format `{number}.{number}.{number}{number}`.</span></span>

    <span data-ttu-id="e1b3b-211">b.</span><span class="sxs-lookup"><span data-stu-id="e1b3b-211">b.</span></span> <span data-ttu-id="e1b3b-212">**選取套件檔案**：此套件包含壓縮成 .zip 檔案的下列檔案：</span><span class="sxs-lookup"><span data-stu-id="e1b3b-212">**Select a package file**: This package contains the following files that are compressed into a .zip file:</span></span>
    * <span data-ttu-id="e1b3b-213">**applianceMainTemplate.json**：用來部署解決方案/應用程式的部署範本檔案。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-213">**applianceMainTemplate.json**: The deployment template file that's used to deploy the solution/application.</span></span> <span data-ttu-id="e1b3b-214">如需有關如何建立部署範本檔案的詳細資訊，請參閱[建立第一個 Azure Resource Manager 範本](resource-manager-create-first-template.md)。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-214">For information about how to create deployment template files, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>
    * <span data-ttu-id="e1b3b-215">**appliancecreateUIDefinition.json**：Azure 入口網站會使用這個檔案來產生使用者介面，用來佈建此解決方案/應用程式。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-215">**appliancecreateUIDefinition.json**: This file is used by the Azure portal to generate the user interface that's used to provision this solution/application.</span></span> <span data-ttu-id="e1b3b-216">如需詳細資訊，請參閱[開始使用 CreateUiDefinition](managed-application-createuidefinition-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-216">For more information, see [Get started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
    * <span data-ttu-id="e1b3b-217">**mainTemplate.json**：此範本檔案只包含 Microsoft.Solution/appliances 資源。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-217">**mainTemplate.json**: This template file contains only the Microsoft.Solution/appliances resource.</span></span> <span data-ttu-id="e1b3b-218">mainTemplate 檔案包含下列屬性：</span><span class="sxs-lookup"><span data-stu-id="e1b3b-218">The mainTemplate file includes the following properties:</span></span>

        *  <span data-ttu-id="e1b3b-219">**kind**：針對 Marketplace 中受管理的應用程式使用 [Marketplace]。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-219">**kind**: Use **Marketplace** for managed applications in the Marketplace.</span></span>
        *  <span data-ttu-id="e1b3b-220">**ManagedResourceGroupId**：客戶訂用帳戶中的資源群組，當中會部署 applianceMainTemplate.json 中所定義的所有資源。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-220">**ManagedResourceGroupId**: This resource group in the customer's subscription is where all the resources defined in applianceMainTemplate.json are deployed.</span></span>
        *  <span data-ttu-id="e1b3b-221">**PublisherPackageId**：此字串可唯一識別套件。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-221">**PublisherPackageId**: This string uniquely identifies the package.</span></span> <span data-ttu-id="e1b3b-222">請以 `{publisherId}.{OfferId}.{SKUID}.{PackageVersion}` 格式提供值。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-222">Provide the value in the format of `{publisherId}.{OfferId}.{SKUID}.{PackageVersion}`.</span></span>

<span data-ttu-id="e1b3b-223">從發佈入口網站取得 [供應項目識別碼] 和 [發行者識別碼]，如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="e1b3b-223">Obtain the **Offer ID** and **Publisher ID** from the publishing portal, as shown in the following image:</span></span>

![優惠識別碼](./media/managed-application-author-marketplace/UniqueString_pubid_offerid.png)
        
<span data-ttu-id="e1b3b-225">取得 [SKU 識別碼]，如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="e1b3b-225">Obtain the **SKU ID**, as shown in the following image:</span></span>

![SKU 識別碼](./media/managed-application-author-marketplace/UniqueString_skuid.png)
        
<span data-ttu-id="e1b3b-227">取得套件**版本**，如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="e1b3b-227">Obtain the package **Version**, as shown in the following image:</span></span>

![套件版本](./media/managed-application-author-marketplace/UniqueString_packageversion.png)
    
  <span data-ttu-id="e1b3b-229">根據前述範例，**PublisherPackageId** 的值是 `azureappliance-test.ravmanagedapptest.ravpreviewmanagedsku.1.0.0`。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-229">Based on the preceding examples, the value of **PublisherPackageId** is `azureappliance-test.ravmanagedapptest.ravpreviewmanagedsku.1.0.0`.</span></span>

  <span data-ttu-id="e1b3b-230">範例 mainTemplate.json：</span><span class="sxs-lookup"><span data-stu-id="e1b3b-230">Sample mainTemplate.json:</span></span>

  ```json
  {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
      "storageAccountNamePrefix": {
        "type": "string",
        "metadata": {
          "description": "Specify the name of the storage account"
        }
      },
      "storageAccountType": {
        "type": "string"
      }
    },
    "variables": {
      "managedResourceGroup": "[concat(resourceGroup().id,uniquestring(resourceGroup().id))]"
    },
    "resources": [{
      "type": "Microsoft.Solutions/appliances",
      "apiVersion": "2016-09-01-preview",
      "name": "[concat(parameters('storageAccountNamePrefix'), '-', 'managed')]",
      "location": "[resourceGroup().location]",
      "kind": "marketplace",
      "properties": {
        "managedResourceGroupId": "[variables('managedResourceGroup')]",
        "PublisherPackageId":"azureappliancetest.ravmanagedapptest.ravpreviewmanagedsku.1.0.0",
        "parameters": {
          "storageAccountName": {
            "value": "[parameters('storageAccountNamePrefix')]"
          },
          "storageAccountType": {
            "value": "[parameters('storageAccountType')]"
          }
        }
      }
    }],
    "outputs": {

    }
  }
  ```

<span data-ttu-id="e1b3b-231">此套件應該包含要成功佈建此應用程式所需的任何其他巢狀範本或指令碼。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-231">This package should contain any other nested templates or scripts that are required to successfully provision this application.</span></span> <span data-ttu-id="e1b3b-232">mainTemplate.json、applianceMainTemplate.json 和 applianceCreateUIDefinition.json 檔案必須存在於根資料夾。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-232">The mainTemplate.json, applianceMainTemplate.json, and applianceCreateUIDefinition.json files must be present at the root folder.</span></span>

* <span data-ttu-id="e1b3b-233">**Authorizations**：這個屬性會定義誰可以存取客戶訂用帳戶中的資源以及其存取層級。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-233">**Authorizations**: This property defines who gets access and the level of access to the resources in customers' subscriptions.</span></span> <span data-ttu-id="e1b3b-234">發行者可以使用它來代表客戶管理應用程式。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-234">The publisher can use it to manage the application on behalf of the customer.</span></span>
* <span data-ttu-id="e1b3b-235">**PrincipalId**：這個屬性是使用者、使用者群組或應用程式的 Azure Active Directory (Azure AD) 識別碼，其擁有者被授與客戶訂用帳戶中資源的特定權限。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-235">**PrincipalId**: This property is the Azure Active Directory (Azure AD) identifier of a user, user group, or application that's granted certain permissions on the resources in the customer's subscription.</span></span> <span data-ttu-id="e1b3b-236">角色定義描述權限。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-236">The Role Definition describes the permissions.</span></span> 
* <span data-ttu-id="e1b3b-237">**角色定義**：這個屬性是 Azure AD 提供的所有內建角色型存取控制 (RBAC) 角色清單。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-237">**Role Definition**: This property is a list of all the built-in Role-Based Access Control (RBAC) roles provided by Azure AD.</span></span> <span data-ttu-id="e1b3b-238">您可以選取最適合用於代表客戶管理資源的角色。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-238">You can select the role that's most appropriate to use to manage the resources on behalf of the customer.</span></span>

<span data-ttu-id="e1b3b-239">您可以新增多個授權。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-239">You can add multiple authorizations.</span></span> <span data-ttu-id="e1b3b-240">建議您建立 AD 使用者群組並且在 **PrincipalId** 中指定其識別碼。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-240">We recommend that you create an AD user group and specify its ID in **PrincipalId**.</span></span> <span data-ttu-id="e1b3b-241">如此一來，您可以將更多使用者新增至使用者群組，而不需要更新 SKU。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-241">This way, you can add more users to the user group without the need to update the SKU.</span></span>

<span data-ttu-id="e1b3b-242">如需 RBAC 的詳細資訊，請參閱[在 Azure 入口網站中開始使用 RBAC](../active-directory/role-based-access-control-what-is.md)。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-242">For more information about RBAC, see [Get started with RBAC in the Azure portal](../active-directory/role-based-access-control-what-is.md).</span></span>

## <a name="marketplace-form"></a><span data-ttu-id="e1b3b-243">Marketplace 表單</span><span class="sxs-lookup"><span data-stu-id="e1b3b-243">Marketplace form</span></span>

<span data-ttu-id="e1b3b-244">Marketplace 表單會要求 [Azure Marketplace](https://azuremarketplace.microsoft.com) 以及 [Azure 入口網站](https://portal.azure.com/)上顯示的欄位。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-244">The Marketplace form asks for fields that show up on the [Azure Marketplace](https://azuremarketplace.microsoft.com) and on the [Azure portal](https://portal.azure.com/).</span></span>

### <a name="preview-subscription-ids"></a><span data-ttu-id="e1b3b-245">預覽訂用帳戶識別碼</span><span class="sxs-lookup"><span data-stu-id="e1b3b-245">Preview subscription IDs</span></span>

<span data-ttu-id="e1b3b-246">輸入 Azure 訂用帳戶識別碼清單，這些訂用帳戶可以在供應項目發佈之後予以存取。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-246">Enter a list of Azure subscription IDs that can access the offer after it's published.</span></span> <span data-ttu-id="e1b3b-247">您可以使用這些允許的訂用帳戶，在供應項目上架前測試預覽的供應項目。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-247">You can use these white-listed subscriptions to test the previewed offer before you make it live.</span></span> <span data-ttu-id="e1b3b-248">您可以在合作夥伴入口網站中將多達 100 個訂用帳戶編入允許清單中。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-248">You can compile a white list of up to 100 subscriptions in the partner portal.</span></span>

### <a name="suggested-categories"></a><span data-ttu-id="e1b3b-249">建議的類別</span><span class="sxs-lookup"><span data-stu-id="e1b3b-249">Suggested categories</span></span>

<span data-ttu-id="e1b3b-250">從清單中選擇與您的供應項目最有關聯的五種類別。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-250">Select up to five categories from the list that your offer can be best associated with.</span></span> <span data-ttu-id="e1b3b-251">這些類別用於將您的供應項目對應至 [Azure Marketplace](https://azuremarketplace.microsoft.com) 和 [Azure 入口網站](https://portal.azure.com/)中提供的產品類別。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-251">These categories are used to map your offer to the product categories that are available in the [Azure Marketplace](https://azuremarketplace.microsoft.com) and the [Azure portal](https://portal.azure.com/).</span></span>

#### <a name="azure-marketplace"></a><span data-ttu-id="e1b3b-252">Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="e1b3b-252">Azure Marketplace</span></span>

<span data-ttu-id="e1b3b-253">受管理的應用程式摘要會顯示下列欄位：</span><span class="sxs-lookup"><span data-stu-id="e1b3b-253">The summary of your managed application displays the following fields:</span></span>

![Marketplace 摘要](./media/managed-application-author-marketplace/publishvm10.png)

<span data-ttu-id="e1b3b-255">受管理應用程式的 [概觀] 索引標籤會顯示下列欄位：</span><span class="sxs-lookup"><span data-stu-id="e1b3b-255">The **Overview** tab for your managed application displays the following fields:</span></span>

![Marketplace 概觀](./media/managed-application-author-marketplace/publishvm11.png)

<span data-ttu-id="e1b3b-257">受管理應用程式的 [方案 + 價格] 索引標籤會顯示下列欄位：</span><span class="sxs-lookup"><span data-stu-id="e1b3b-257">The **Plans + Pricing** tab for your managed application displays the following fields:</span></span>

![Marketplace 方案](./media/managed-application-author-marketplace/publishvm15.png)

#### <a name="azure-portal"></a><span data-ttu-id="e1b3b-259">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="e1b3b-259">Azure portal</span></span>

<span data-ttu-id="e1b3b-260">受管理的應用程式摘要會顯示下列欄位：</span><span class="sxs-lookup"><span data-stu-id="e1b3b-260">The summary of your managed application displays the following fields:</span></span>

![入口網站摘要](./media/managed-application-author-marketplace/publishvm12.png)

<span data-ttu-id="e1b3b-262">受管理應用程式的概觀會顯示下列欄位：</span><span class="sxs-lookup"><span data-stu-id="e1b3b-262">The overview for your managed application displays the following fields:</span></span>

![入口網站概觀](./media/managed-application-author-marketplace/publishvm13.png)

#### <a name="logo-guidelines"></a><span data-ttu-id="e1b3b-264">標誌指導方針</span><span class="sxs-lookup"><span data-stu-id="e1b3b-264">Logo guidelines</span></span>

<span data-ttu-id="e1b3b-265">您在 Cloud Partner 入口網站中上傳的所有標誌都應該遵循下列指導方針︰</span><span class="sxs-lookup"><span data-stu-id="e1b3b-265">Follow these guidelines for any logo that you upload in the Cloud Partner portal:</span></span>

*   <span data-ttu-id="e1b3b-266">Azure 設計具有簡單的調色盤。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-266">The Azure design has a simple color palette.</span></span> <span data-ttu-id="e1b3b-267">限制標誌上的主要和次要色彩數目。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-267">Limit the number of primary and secondary colors on your logo.</span></span>
*   <span data-ttu-id="e1b3b-268">入口網站的佈景主題色彩是白色與黑色。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-268">The theme colors of the portal are white and black.</span></span> <span data-ttu-id="e1b3b-269">請勿使用這些色彩作為標誌的背景色彩。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-269">Don't use these colors as the background color for your logo.</span></span> <span data-ttu-id="e1b3b-270">請使用可讓標誌在入口網站突顯出來的色彩。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-270">Use a color that makes your logo prominent in the portal.</span></span> <span data-ttu-id="e1b3b-271">建議您使用簡單的主要色彩。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-271">We recommend simple primary colors.</span></span> <span data-ttu-id="e1b3b-272">如果您使用透明背景，請確定標誌和文字不是白色、黑色或藍色。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-272">*If you use a transparent background, make sure that the logo and text aren't white, black, or blue.*</span></span>
*   <span data-ttu-id="e1b3b-273">請不要在標誌上使用漸層背景。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-273">Don't use a gradient background on the logo.</span></span>
*   <span data-ttu-id="e1b3b-274">請勿在標誌上放置文字 (甚至是公司或品牌名稱)。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-274">Don't place text on the logo, not even your company or brand name.</span></span> <span data-ttu-id="e1b3b-275">標誌的外觀與風格應該是「一般」，且避免使用漸層。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-275">The look and feel of your logo should be flat and avoid gradients.</span></span>
*   <span data-ttu-id="e1b3b-276">確定標誌不會自動縮放。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-276">Make sure the logo isn't stretched.</span></span>

#### <a name="hero-logo"></a><span data-ttu-id="e1b3b-277">主圖標誌</span><span class="sxs-lookup"><span data-stu-id="e1b3b-277">Hero logo</span></span>

<span data-ttu-id="e1b3b-278">主圖標誌是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-278">The hero logo is optional.</span></span> <span data-ttu-id="e1b3b-279">發行者可以選擇不上傳主圖標誌。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-279">The publisher can choose not to upload a hero logo.</span></span> <span data-ttu-id="e1b3b-280">上傳主圖圖示之後，便無法刪除。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-280">After the hero icon is uploaded, it can't be deleted.</span></span> <span data-ttu-id="e1b3b-281">屆時合作夥伴必須遵循主圖圖示的 Marketplace 指導方針。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-281">At that time, the partner must follow the Marketplace guidelines for hero icons.</span></span>

<span data-ttu-id="e1b3b-282">主圖標誌圖示應該遵循下列指導方針：</span><span class="sxs-lookup"><span data-stu-id="e1b3b-282">Follow these guidelines for the hero logo icon:</span></span>

*   <span data-ttu-id="e1b3b-283">發行者顯示名稱、方案標題和供應項目完整摘要會以白色顯示。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-283">The publisher display name, the plan title, and the offer long summary are displayed in white.</span></span> <span data-ttu-id="e1b3b-284">因此，請勿使用淺色作為主圖圖示的背景。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-284">Therefore, don't use a light color for the background of the hero icon.</span></span> <span data-ttu-id="e1b3b-285">主圖圖示不得使用黑色、白色和透明背景。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-285">A black, white, or transparent background isn't allowed for hero icons.</span></span>
*   <span data-ttu-id="e1b3b-286">在供應項目列出之後，發行者顯示名稱、方案標題、供應項目完整摘要和 [建立] 按鈕會以程式設計方式內嵌在主圖標誌內。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-286">After the offer is listed, the publisher display name, the plan title, the offer long summary, and the **Create** button are embedded programmatically inside the hero logo.</span></span> <span data-ttu-id="e1b3b-287">因此，請勿在設計主圖標誌時輸入任何文字。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-287">Consequently, don't enter any text while you design the hero logo.</span></span> <span data-ttu-id="e1b3b-288">在右邊留下空白空間，因為系統會以程式設計方式文字放入該空間。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-288">Leave empty space on the right because the text is included programmatically in that space.</span></span> <span data-ttu-id="e1b3b-289">右側的文字空白空間應該是 415 x 100 像素。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-289">The empty space for the text should be 415 x 100 pixels on the right.</span></span> <span data-ttu-id="e1b3b-290">它是從左邊位移 370 像素。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-290">It's offset by 370 pixels from the left.</span></span>

    ![主圖標誌範例](./media/managed-application-author-marketplace/publishvm14.png)

## <a name="support-form"></a><span data-ttu-id="e1b3b-292">支援表單</span><span class="sxs-lookup"><span data-stu-id="e1b3b-292">Support form</span></span>

<span data-ttu-id="e1b3b-293">在 [支援] 表單中填寫貴公司的支援連絡人。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-293">Fill out the **Support** form with support contacts from your company.</span></span> <span data-ttu-id="e1b3b-294">此資訊可能是工程連絡人和客戶支援連絡人。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-294">This information might be engineering contacts and customer support contacts.</span></span>

## <a name="publish-an-offer"></a><span data-ttu-id="e1b3b-295">發佈提供項目</span><span class="sxs-lookup"><span data-stu-id="e1b3b-295">Publish an offer</span></span>

<span data-ttu-id="e1b3b-296">填妥所有區段之後，請選取 [發佈] 開始讓客戶可使用供應項目的程序。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-296">After you fill out all the sections, select **Publish** to start the process that makes your offer available to customers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e1b3b-297">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e1b3b-297">Next steps</span></span>

* <span data-ttu-id="e1b3b-298">如需受管理應用程式的簡介，請參閱[受管理的應用程式概觀](managed-application-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-298">For an introduction to managed applications, see [Managed application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="e1b3b-299">如需從 Marketplace 使用受管理應用程式的詳細資訊，請參閱[在 Marketplace 中使用 Azure 受管理的應用程式](managed-application-consume-marketplace.md)。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-299">For information about consuming a managed application from the Marketplace, see [Consume Azure managed applications in the Marketplace](managed-application-consume-marketplace.md).</span></span>
* <span data-ttu-id="e1b3b-300">如需發佈 Service Catalog 受管理應用程式的資訊，請參閱[建立和發佈 Service Catalog 受管理的應用程式](managed-application-publishing.md)。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-300">For information about publishing a Service Catalog managed application, see [Create and publish a Service Catalog managed application](managed-application-publishing.md).</span></span>
* <span data-ttu-id="e1b3b-301">如需使用 Service Catalog 受管理應用程式的詳細資訊，請參閱[使用 Service Catalog 受管理的應用程式](managed-application-consumption.md)。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-301">For information about consuming a Service Catalog managed application, see [Consume a Service Catalog managed application](managed-application-consumption.md).</span></span>
