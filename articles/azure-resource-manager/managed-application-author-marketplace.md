---
title: "aaaAzure managed hello Marketplace 中的應用程式 |Microsoft 文件"
description: "描述 Azure 受管理的應用程式，可透過 hello Marketplace。"
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/09/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: b3cdf3f1fccdd47db699e4892ae8bce35118bfd8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-managed-applications-in-hello-marketplace"></a><span data-ttu-id="98c06-103">Azure 受管理的 hello Marketplace 中的應用程式</span><span class="sxs-lookup"><span data-stu-id="98c06-103">Azure managed applications in hello Marketplace</span></span>

 <span data-ttu-id="98c06-104">MSPs、 Isv 和系統整合業者 (Si) 可以使用 Azure 受管理應用程式 toooffer 解決方案 tooall Azure Marketplace 客戶。</span><span class="sxs-lookup"><span data-stu-id="98c06-104">MSPs, ISVs, and system integrators (SIs) can use Azure managed applications toooffer their solutions tooall Azure Marketplace customers.</span></span> <span data-ttu-id="98c06-105">這類方案減少 hello 維護與服務的客戶的額外負荷。</span><span class="sxs-lookup"><span data-stu-id="98c06-105">Such solutions reduce hello maintenance and servicing overhead for customers.</span></span> <span data-ttu-id="98c06-106">發行者可以銷售基礎結構和透過 hello Marketplace 的軟體。</span><span class="sxs-lookup"><span data-stu-id="98c06-106">Publishers can sell infrastructure and software through hello Marketplace.</span></span> <span data-ttu-id="98c06-107">服務和作業支援 toomanaged 應用程式，就可以將它們附加。</span><span class="sxs-lookup"><span data-stu-id="98c06-107">They can attach services and operational support toomanaged applications.</span></span> <span data-ttu-id="98c06-108">如需詳細資訊，請參閱[受管理的應用程式概觀](managed-application-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="98c06-108">For more information, see [Managed application overview](managed-application-overview.md).</span></span>

<span data-ttu-id="98c06-109">本文說明如何 MSP、 ISV 或 si 亦然可以發行應用程式 toohello Marketplace 並使其廣泛受到使用 toocustomers。</span><span class="sxs-lookup"><span data-stu-id="98c06-109">This article explains how an MSP, ISV, or SI can publish an application toohello Marketplace and make it broadly available toocustomers.</span></span>

## <a name="prerequisites-for-publishing-a-managed-application"></a><span data-ttu-id="98c06-110">發行受管理應用程式的必要條件</span><span class="sxs-lookup"><span data-stu-id="98c06-110">Prerequisites for publishing a managed application</span></span>

<span data-ttu-id="98c06-111">必要條件 toolisting hello Marketplace 中：</span><span class="sxs-lookup"><span data-stu-id="98c06-111">Prerequisites toolisting in hello Marketplace:</span></span>

* <span data-ttu-id="98c06-112">技術需求</span><span class="sxs-lookup"><span data-stu-id="98c06-112">Technical</span></span>

    *  <span data-ttu-id="98c06-113">如需 hello 基本結構和語法的 Azure 資源管理員範本，請參閱[Azure 資源管理員範本](resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="98c06-113">For information about hello basic structure and syntax of Azure Resource Manager templates, see [Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
    *  <span data-ttu-id="98c06-114">tooview 完成範本方案比較，請參閱[Azure 快速入門範本](https://azure.microsoft.com/en-us/documentation/templates/)或 hello[快速入門範本儲存機制](https://github.com/azure/azure-quickstart-templates)。</span><span class="sxs-lookup"><span data-stu-id="98c06-114">tooview complete template solutions, see [Azure Quickstart templates](https://azure.microsoft.com/en-us/documentation/templates/) or hello [Quickstart template repository](https://github.com/azure/azure-quickstart-templates).</span></span>
    *  <span data-ttu-id="98c06-115">如需如何 toocreate hello 介面透過 hello Marketplace 應用程式部署的客戶資訊，請參閱[建立使用者介面的定義檔](managed-application-createuidefinition-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="98c06-115">For information about how toocreate hello interface for customers who deploy your application through hello Marketplace, see [Create a user interface definition file](managed-application-createuidefinition-overview.md).</span></span>

* <span data-ttu-id="98c06-116">非技術性 (商務需求)</span><span class="sxs-lookup"><span data-stu-id="98c06-116">Nontechnical (business requirements)</span></span>

    *   <span data-ttu-id="98c06-117">您的公司或其子公司，都必須位於國家/地區銷售其中受到 hello Marketplace。</span><span class="sxs-lookup"><span data-stu-id="98c06-117">Your company or its subsidiary must be located in a country where sales are supported by hello Marketplace.</span></span>
    *   <span data-ttu-id="98c06-118">必須授權產品與支援 hello Marketplace 計費模型相容的方式。</span><span class="sxs-lookup"><span data-stu-id="98c06-118">Your product must be licensed in a way that is compatible with billing models supported by hello Marketplace.</span></span>
    *   <span data-ttu-id="98c06-119">您負責進行技術支援人員可以使用 toocustomers 盡商業上合理的方式。</span><span class="sxs-lookup"><span data-stu-id="98c06-119">You're responsible for making technical support available toocustomers in a commercially reasonable manner.</span></span> <span data-ttu-id="98c06-120">hello 支援可以免費的付費，或透過社群支援。</span><span class="sxs-lookup"><span data-stu-id="98c06-120">hello support can be free, paid, or through community support.</span></span>
    *   <span data-ttu-id="98c06-121">您必須負責為您的軟體和任何第三方廠商相依性進行授權。</span><span class="sxs-lookup"><span data-stu-id="98c06-121">You're responsible for licensing your software and any third-party software dependencies.</span></span>
    *   <span data-ttu-id="98c06-122">您必須提供符合準則的供應項目 toobe 的內容列出 hello 和 hello Marketplace 中 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="98c06-122">You must provide content that meets criteria for your offering toobe listed in hello Marketplace and in hello Azure portal.</span></span>
    *   <span data-ttu-id="98c06-123">您必須同意 toohello hello Azure Marketplace 參與原則和發行者合約的條款。</span><span class="sxs-lookup"><span data-stu-id="98c06-123">You must agree toohello terms of hello Azure Marketplace Participation Policies and Publisher Agreement.</span></span>
    *   <span data-ttu-id="98c06-124">您必須同意 toocomply hello 使用條款、 Microsoft 隱私權聲明，與 Microsoft Azure 認證程式合約。</span><span class="sxs-lookup"><span data-stu-id="98c06-124">You must agree toocomply with hello Terms of Use, Microsoft Privacy Statement, and Microsoft Azure Certified Program Agreement.</span></span>

## <a name="create-a-new-azure-application-offer"></a><span data-ttu-id="98c06-125">建立新的 Azure 應用程式供應項目</span><span class="sxs-lookup"><span data-stu-id="98c06-125">Create a new Azure application offer</span></span>

<span data-ttu-id="98c06-126">符合 hello 必要條件之後，您便準備好 toocreate 您受管理的應用程式提供的服務。</span><span class="sxs-lookup"><span data-stu-id="98c06-126">After you meet hello prerequisites, you're ready toocreate your managed application offer.</span></span> <span data-ttu-id="98c06-127">讓我們先快速概觀供應項目和 SKU。</span><span class="sxs-lookup"><span data-stu-id="98c06-127">Let's take a quick overview of an offer and a SKU.</span></span>

### <a name="offer"></a><span data-ttu-id="98c06-128">提供項目</span><span class="sxs-lookup"><span data-stu-id="98c06-128">Offer</span></span>

<span data-ttu-id="98c06-129">受管理的應用程式的 hello 優惠對應 tooa 類別的供應項目從 「 發行者 」 的產品。</span><span class="sxs-lookup"><span data-stu-id="98c06-129">hello offer for a managed application corresponds tooa class of product offering from a publisher.</span></span> <span data-ttu-id="98c06-130">如果您有想 toomake hello Marketplace 中可用的方案/應用程式的新類型時，您可以設定它為新的優惠。</span><span class="sxs-lookup"><span data-stu-id="98c06-130">If you have a new type of solution/application that you want toomake available in hello Marketplace, you can set it up as a new offer.</span></span> <span data-ttu-id="98c06-131">優惠 SKU 的集合。</span><span class="sxs-lookup"><span data-stu-id="98c06-131">An offer is a collection of SKUs.</span></span> <span data-ttu-id="98c06-132">每個供應項目會顯示為自己 hello Marketplace 中的實體。</span><span class="sxs-lookup"><span data-stu-id="98c06-132">Every offer appears as its own entity in hello Marketplace.</span></span>

### <a name="sku"></a><span data-ttu-id="98c06-133">SKU</span><span class="sxs-lookup"><span data-stu-id="98c06-133">SKU</span></span>

<span data-ttu-id="98c06-134">SKU 不 hello 最小可單位的提供項目。</span><span class="sxs-lookup"><span data-stu-id="98c06-134">A SKU is hello smallest purchasable unit of an offer.</span></span> <span data-ttu-id="98c06-135">您可以使用內 hello SKU 相同產品類別 （優惠） toodifferentiate 之間：</span><span class="sxs-lookup"><span data-stu-id="98c06-135">You can use a SKU within hello same product class (offer) toodifferentiate between:</span></span>

* <span data-ttu-id="98c06-136">所支援的不同功能。</span><span class="sxs-lookup"><span data-stu-id="98c06-136">Different features that are supported.</span></span>
* <span data-ttu-id="98c06-137">是否 hello 供應項目為 managed 或 unmanaged。</span><span class="sxs-lookup"><span data-stu-id="98c06-137">Whether hello offer is managed or unmanaged.</span></span>
* <span data-ttu-id="98c06-138">支援的計費模型。</span><span class="sxs-lookup"><span data-stu-id="98c06-138">Billing models that are supported.</span></span>

<span data-ttu-id="98c06-139">SKU 之下 hello 父 hello Marketplace 中供應項目。</span><span class="sxs-lookup"><span data-stu-id="98c06-139">A SKU appears under hello parent offer in hello Marketplace.</span></span> <span data-ttu-id="98c06-140">它會顯示為其本身可實體 hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="98c06-140">It appears as its own purchasable entity in hello Azure portal.</span></span>

### <a name="set-up-an-offer"></a><span data-ttu-id="98c06-141">設定供應項目</span><span class="sxs-lookup"><span data-stu-id="98c06-141">Set up an offer</span></span>

1. <span data-ttu-id="98c06-142">登入 toohello [Cloud Partner 入口網站](https://cloudpartner.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="98c06-142">Sign in toohello [Cloud Partner portal](https://cloudpartner.azure.com/).</span></span>

2. <span data-ttu-id="98c06-143">Hello hello 左側瀏覽窗格中選取**+ 新的優惠** > **Azure 應用程式**。</span><span class="sxs-lookup"><span data-stu-id="98c06-143">In hello navigation pane on hello left, select **+ New offer** > **Azure Applications**.</span></span>

    ![新增供應項目](./media/managed-application-author-marketplace/newOffer.png)

3. <span data-ttu-id="98c06-145">填寫 hello 表單出現在 hello 處於 hello**編輯器**檢視。</span><span class="sxs-lookup"><span data-stu-id="98c06-145">Fill out hello forms that appear on hello left in hello **Editor** view.</span></span> <span data-ttu-id="98c06-146">必填欄位會標示紅色星號 (*)。</span><span class="sxs-lookup"><span data-stu-id="98c06-146">Required fields are marked with a red asterisk (*).</span></span>

    ![供應項目](./media/managed-application-author-marketplace/newOffer_OfferSettings.png)

    <span data-ttu-id="98c06-148">四種主要形式是使用的 toocreate 受管理的應用程式：</span><span class="sxs-lookup"><span data-stu-id="98c06-148">Four main forms are used toocreate a managed application:</span></span>

    <span data-ttu-id="98c06-149">a.</span><span class="sxs-lookup"><span data-stu-id="98c06-149">a.</span></span> <span data-ttu-id="98c06-150">優惠設定</span><span class="sxs-lookup"><span data-stu-id="98c06-150">Offer Settings</span></span>

    <span data-ttu-id="98c06-151">b.</span><span class="sxs-lookup"><span data-stu-id="98c06-151">b.</span></span> <span data-ttu-id="98c06-152">SKU</span><span class="sxs-lookup"><span data-stu-id="98c06-152">SKUs</span></span>

    <span data-ttu-id="98c06-153">c.</span><span class="sxs-lookup"><span data-stu-id="98c06-153">c.</span></span> <span data-ttu-id="98c06-154">Marketplace</span><span class="sxs-lookup"><span data-stu-id="98c06-154">Marketplace</span></span>

    <span data-ttu-id="98c06-155">d.</span><span class="sxs-lookup"><span data-stu-id="98c06-155">d.</span></span> <span data-ttu-id="98c06-156">支援</span><span class="sxs-lookup"><span data-stu-id="98c06-156">Support</span></span>

<span data-ttu-id="98c06-157">Hello 下列各節將詳細說明這些表單。</span><span class="sxs-lookup"><span data-stu-id="98c06-157">These forms are described in greater detail in hello following sections.</span></span>

## <a name="offer-settings-form"></a><span data-ttu-id="98c06-158">供應項目設定表單</span><span class="sxs-lookup"><span data-stu-id="98c06-158">Offer Settings form</span></span>
<span data-ttu-id="98c06-159">使用這個基本形式 toospecify hello 優惠設定。</span><span class="sxs-lookup"><span data-stu-id="98c06-159">Use this basic form toospecify hello offer settings.</span></span>

1. <span data-ttu-id="98c06-160">填寫 hello**提供設定**表單。</span><span class="sxs-lookup"><span data-stu-id="98c06-160">Fill in hello **Offer Settings** form.</span></span> <span data-ttu-id="98c06-161">hello 不同欄位如下：</span><span class="sxs-lookup"><span data-stu-id="98c06-161">hello different fields are:</span></span>

    <span data-ttu-id="98c06-162">a.</span><span class="sxs-lookup"><span data-stu-id="98c06-162">a.</span></span> <span data-ttu-id="98c06-163">**提供識別碼**： 這個唯一識別碼識別 「 發行者 」 設定檔中的 hello 供應項目。</span><span class="sxs-lookup"><span data-stu-id="98c06-163">**Offer ID**: This unique identifier identifies hello offer within a publisher profile.</span></span> <span data-ttu-id="98c06-164">此識別碼會顯示在產品的 URL，Resource Manager 範本和計費報告中。</span><span class="sxs-lookup"><span data-stu-id="98c06-164">This ID is visible in product URLs, Resource Manager templates, and billing reports.</span></span> <span data-ttu-id="98c06-165">此識別碼只能包含小寫英數字元或連字號 (-)。</span><span class="sxs-lookup"><span data-stu-id="98c06-165">It can only be composed of lowercase alphanumeric characters or dashes (-).</span></span> <span data-ttu-id="98c06-166">hello 識別碼結尾不得為破折號。</span><span class="sxs-lookup"><span data-stu-id="98c06-166">hello ID can't end in a dash.</span></span> <span data-ttu-id="98c06-167">它是有限的 tooa 最多 50 個字元。</span><span class="sxs-lookup"><span data-stu-id="98c06-167">It's limited tooa maximum of 50 characters.</span></span> <span data-ttu-id="98c06-168">供應項目上架後，此欄位便會鎖住。</span><span class="sxs-lookup"><span data-stu-id="98c06-168">After an offer goes live, this field is locked.</span></span>

    <span data-ttu-id="98c06-169">b.</span><span class="sxs-lookup"><span data-stu-id="98c06-169">b.</span></span> <span data-ttu-id="98c06-170">**發行者 ID**： 使用這個下拉式清單 toochoose hello 「 發行者 」 設定檔想 toopublish 下的這項優惠。</span><span class="sxs-lookup"><span data-stu-id="98c06-170">**Publisher ID**: Use this drop-down list toochoose hello publisher profile you want toopublish this offer under.</span></span> <span data-ttu-id="98c06-171">供應項目上架後，此欄位便會鎖住。</span><span class="sxs-lookup"><span data-stu-id="98c06-171">After an offer goes live, this field is locked.</span></span>

    <span data-ttu-id="98c06-172">c.</span><span class="sxs-lookup"><span data-stu-id="98c06-172">c.</span></span> <span data-ttu-id="98c06-173">**名稱**： 您的優惠此顯示名稱會出現在 hello Marketplace 和 hello 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="98c06-173">**Name**: This display name for your offer appears in hello Marketplace and in hello portal.</span></span> <span data-ttu-id="98c06-174">它最多不能超過 50 個字元。</span><span class="sxs-lookup"><span data-stu-id="98c06-174">It can have a maximum of 50 characters.</span></span> <span data-ttu-id="98c06-175">包含產品的可辨識品牌名稱。</span><span class="sxs-lookup"><span data-stu-id="98c06-175">Include a recognizable brand name for your product.</span></span> <span data-ttu-id="98c06-176">請勿在此包含您的公司名稱，除非這是行銷方式。</span><span class="sxs-lookup"><span data-stu-id="98c06-176">Don't include your company name here unless that's how it's marketed.</span></span> <span data-ttu-id="98c06-177">如果您在您自己的網站上行銷這項優惠，請確定 hello 名稱是完全在您的網站上的顯示方式。</span><span class="sxs-lookup"><span data-stu-id="98c06-177">If you're marketing this offer on your own website, ensure that hello name is exactly how it appears on your website.</span></span>

2. <span data-ttu-id="98c06-178">選取**儲存**toosave 進度。</span><span class="sxs-lookup"><span data-stu-id="98c06-178">Select **Save** toosave your progress.</span></span> 

## <a name="skus-form"></a><span data-ttu-id="98c06-179">SKU 表單</span><span class="sxs-lookup"><span data-stu-id="98c06-179">SKUs form</span></span>
<span data-ttu-id="98c06-180">hello 下一個步驟是您的優惠的 tooadd Sku。</span><span class="sxs-lookup"><span data-stu-id="98c06-180">hello next step is tooadd SKUs for your offer.</span></span>

1. <span data-ttu-id="98c06-181">選取 [SKU] > [新增 SKU]。</span><span class="sxs-lookup"><span data-stu-id="98c06-181">Select **SKUs** > **New SKU**.</span></span> 

    ![選取新的 SKU](./media/managed-application-author-marketplace/newOffer_skus.png)

2. <span data-ttu-id="98c06-183">輸入 [SKU 識別碼]。</span><span class="sxs-lookup"><span data-stu-id="98c06-183">Enter a **SKU ID**.</span></span> <span data-ttu-id="98c06-184">SKU 識別碼是提供項目中的 hello SKU 的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="98c06-184">A SKU ID is a unique identifier for hello SKU within an offer.</span></span> <span data-ttu-id="98c06-185">此識別碼會顯示在產品的 URL，Resource Manager 範本和計費報告中。</span><span class="sxs-lookup"><span data-stu-id="98c06-185">This ID is visible in product URLs, Resource Manager templates, and billing reports.</span></span> <span data-ttu-id="98c06-186">此識別碼只能包含小寫英數字元或連字號 (-)。</span><span class="sxs-lookup"><span data-stu-id="98c06-186">It can only be composed of lowercase alphanumeric characters or dashes (-).</span></span> <span data-ttu-id="98c06-187">hello 識別碼不能結束虛線，且限制的 tooa 最多 50 個字元。</span><span class="sxs-lookup"><span data-stu-id="98c06-187">hello ID can't end in a dash, and it's limited tooa maximum of 50 characters.</span></span> <span data-ttu-id="98c06-188">供應項目上架後，此欄位便會鎖住。</span><span class="sxs-lookup"><span data-stu-id="98c06-188">After an offer goes live, this field is locked.</span></span> <span data-ttu-id="98c06-189">您可以在一個優惠內建立多個 SKU。</span><span class="sxs-lookup"><span data-stu-id="98c06-189">You can have multiple SKUs within an offer.</span></span> <span data-ttu-id="98c06-190">您需要 SKU 想 toopublish 每個映像。</span><span class="sxs-lookup"><span data-stu-id="98c06-190">You need a SKU for each image you plan toopublish.</span></span>

3. <span data-ttu-id="98c06-191">填寫 hello **SKU 詳細資料**hello 遵循表單上的區段：</span><span class="sxs-lookup"><span data-stu-id="98c06-191">Fill out hello **SKU Details** section on hello following form:</span></span>

    ![提供新的 SKU](./media/managed-application-author-marketplace/newOffer_newsku.png)

    <span data-ttu-id="98c06-193">填寫下列欄位的 hello:</span><span class="sxs-lookup"><span data-stu-id="98c06-193">Fill out hello following fields:</span></span>
    
    <span data-ttu-id="98c06-194">a.</span><span class="sxs-lookup"><span data-stu-id="98c06-194">a.</span></span> <span data-ttu-id="98c06-195">**標題**：輸入此 SKU 的標題。</span><span class="sxs-lookup"><span data-stu-id="98c06-195">**Title**: Enter a title for this SKU.</span></span> <span data-ttu-id="98c06-196">此標題會出現在 hello 藝廊，適合於這個項目。</span><span class="sxs-lookup"><span data-stu-id="98c06-196">This title appears in hello gallery for this item.</span></span>

    <span data-ttu-id="98c06-197">b.</span><span class="sxs-lookup"><span data-stu-id="98c06-197">b.</span></span> <span data-ttu-id="98c06-198">**摘要**：輸入此 SKU 的簡短摘要。</span><span class="sxs-lookup"><span data-stu-id="98c06-198">**Summary**: Enter a short summary for this SKU.</span></span> <span data-ttu-id="98c06-199">此文字會顯示 hello 標題底下。</span><span class="sxs-lookup"><span data-stu-id="98c06-199">This text appears underneath hello title.</span></span>

    <span data-ttu-id="98c06-200">c.</span><span class="sxs-lookup"><span data-stu-id="98c06-200">c.</span></span> <span data-ttu-id="98c06-201">**描述**： 輸入 hello SKU 的詳細的描述。</span><span class="sxs-lookup"><span data-stu-id="98c06-201">**Description**: Enter a detailed description about hello SKU.</span></span>

    <span data-ttu-id="98c06-202">d.</span><span class="sxs-lookup"><span data-stu-id="98c06-202">d.</span></span> <span data-ttu-id="98c06-203">**SKU 類型**: hello 允許的值為**管理的應用程式**和**解決方案範本**。</span><span class="sxs-lookup"><span data-stu-id="98c06-203">**SKU Type**: hello allowed values are **Managed Application** and **Solution Templates**.</span></span> <span data-ttu-id="98c06-204">此案例中，選取 [受管理的應用程式]。</span><span class="sxs-lookup"><span data-stu-id="98c06-204">For this case, select **Managed Application**.</span></span>

4. <span data-ttu-id="98c06-205">填寫 hello**套件詳細資料**hello 遵循表單上的區段：</span><span class="sxs-lookup"><span data-stu-id="98c06-205">Fill out hello **Package Details** section on hello following form:</span></span>

    ![Package](./media/managed-application-author-marketplace/newOffer_newsku_package.png)

    <span data-ttu-id="98c06-207">填寫下列欄位的 hello:</span><span class="sxs-lookup"><span data-stu-id="98c06-207">Fill out hello following fields:</span></span>

    <span data-ttu-id="98c06-208">a.</span><span class="sxs-lookup"><span data-stu-id="98c06-208">a.</span></span> <span data-ttu-id="98c06-209">**目前版本**： 輸入您上傳的 hello 封裝版本。</span><span class="sxs-lookup"><span data-stu-id="98c06-209">**Current Version**: Enter a version for hello package you upload.</span></span> <span data-ttu-id="98c06-210">Hello 格式應為`{number}.{number}.{number}{number}`。</span><span class="sxs-lookup"><span data-stu-id="98c06-210">It should be in hello format `{number}.{number}.{number}{number}`.</span></span>

    <span data-ttu-id="98c06-211">b.</span><span class="sxs-lookup"><span data-stu-id="98c06-211">b.</span></span> <span data-ttu-id="98c06-212">**選取封裝檔案**： 此套件包含下列檔案壓縮成.zip 檔 hello:</span><span class="sxs-lookup"><span data-stu-id="98c06-212">**Select a package file**: This package contains hello following files that are compressed into a .zip file:</span></span>
    * <span data-ttu-id="98c06-213">**applianceMainTemplate.json**: hello 用 toodeploy hello 方案/應用程式部署範本檔案。</span><span class="sxs-lookup"><span data-stu-id="98c06-213">**applianceMainTemplate.json**: hello deployment template file that's used toodeploy hello solution/application.</span></span> <span data-ttu-id="98c06-214">如需有關資訊 toocreate 部署範本檔案，請參閱[建立第一個 Azure Resource Manager 範本](resource-manager-create-first-template.md)。</span><span class="sxs-lookup"><span data-stu-id="98c06-214">For information about how toocreate deployment template files, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>
    * <span data-ttu-id="98c06-215">**appliancecreateUIDefinition.json**: hello Azure 入口網站 toogenerate hello 使用者介面使用 tooprovision 方案/應用程式會使用此檔案。</span><span class="sxs-lookup"><span data-stu-id="98c06-215">**appliancecreateUIDefinition.json**: This file is used by hello Azure portal toogenerate hello user interface that's used tooprovision this solution/application.</span></span> <span data-ttu-id="98c06-216">如需詳細資訊，請參閱[開始使用 CreateUiDefinition](managed-application-createuidefinition-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="98c06-216">For more information, see [Get started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
    * <span data-ttu-id="98c06-217">**mainTemplate.json**： 這個範本檔案包含 hello Microsoft.Solution/appliances 資源。</span><span class="sxs-lookup"><span data-stu-id="98c06-217">**mainTemplate.json**: This template file contains only hello Microsoft.Solution/appliances resource.</span></span> <span data-ttu-id="98c06-218">hello mainTemplate 檔案包含下列屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="98c06-218">hello mainTemplate file includes hello following properties:</span></span>

        *  <span data-ttu-id="98c06-219">**種類**： 使用**Marketplace** hello Marketplace 中的受管理應用程式。</span><span class="sxs-lookup"><span data-stu-id="98c06-219">**kind**: Use **Marketplace** for managed applications in hello Marketplace.</span></span>
        *  <span data-ttu-id="98c06-220">**ManagedResourceGroupId**: hello 客戶的訂用帳戶中的這個資源群組是 applianceMainTemplate.json 中定義的所有 hello 資源都部署的位置。</span><span class="sxs-lookup"><span data-stu-id="98c06-220">**ManagedResourceGroupId**: This resource group in hello customer's subscription is where all hello resources defined in applianceMainTemplate.json are deployed.</span></span>
        *  <span data-ttu-id="98c06-221">**PublisherPackageId**： 這個字串可唯一識別 hello 封裝。</span><span class="sxs-lookup"><span data-stu-id="98c06-221">**PublisherPackageId**: This string uniquely identifies hello package.</span></span> <span data-ttu-id="98c06-222">提供的 hello 格式中的 hello 值`{publisherId}.{OfferId}.{SKUID}.{PackageVersion}`。</span><span class="sxs-lookup"><span data-stu-id="98c06-222">Provide hello value in hello format of `{publisherId}.{OfferId}.{SKUID}.{PackageVersion}`.</span></span>

<span data-ttu-id="98c06-223">取得 hello**提供識別碼**和**發行者識別碼**從 hello 發佈入口網站中 hello 下列影像所示：</span><span class="sxs-lookup"><span data-stu-id="98c06-223">Obtain hello **Offer ID** and **Publisher ID** from hello publishing portal, as shown in hello following image:</span></span>

![優惠識別碼](./media/managed-application-author-marketplace/UniqueString_pubid_offerid.png)
        
<span data-ttu-id="98c06-225">取得 hello **SKU 識別碼**hello 下列影像所示：</span><span class="sxs-lookup"><span data-stu-id="98c06-225">Obtain hello **SKU ID**, as shown in hello following image:</span></span>

![SKU 識別碼](./media/managed-application-author-marketplace/UniqueString_skuid.png)
        
<span data-ttu-id="98c06-227">取得 hello 套件**版本**hello 下列影像所示：</span><span class="sxs-lookup"><span data-stu-id="98c06-227">Obtain hello package **Version**, as shown in hello following image:</span></span>

![套件版本](./media/managed-application-author-marketplace/UniqueString_packageversion.png)
    
  <span data-ttu-id="98c06-229">根據前面範例的 hello，hello 值**PublisherPackageId**是`azureappliance-test.ravmanagedapptest.ravpreviewmanagedsku.1.0.0`。</span><span class="sxs-lookup"><span data-stu-id="98c06-229">Based on hello preceding examples, hello value of **PublisherPackageId** is `azureappliance-test.ravmanagedapptest.ravpreviewmanagedsku.1.0.0`.</span></span>

  <span data-ttu-id="98c06-230">範例 mainTemplate.json：</span><span class="sxs-lookup"><span data-stu-id="98c06-230">Sample mainTemplate.json:</span></span>

  ```json
  {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
      "storageAccountNamePrefix": {
        "type": "string",
        "metadata": {
          "description": "Specify hello name of hello storage account"
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

<span data-ttu-id="98c06-231">此套件應該包含任何巢狀的範本，或需要的 toosuccessfully 的指令碼佈建此應用程式。</span><span class="sxs-lookup"><span data-stu-id="98c06-231">This package should contain any other nested templates or scripts that are required toosuccessfully provision this application.</span></span> <span data-ttu-id="98c06-232">hello mainTemplate.json、 applianceMainTemplate.json 和 applianceCreateUIDefinition.json 檔案必須存在於 hello 根資料夾。</span><span class="sxs-lookup"><span data-stu-id="98c06-232">hello mainTemplate.json, applianceMainTemplate.json, and applianceCreateUIDefinition.json files must be present at hello root folder.</span></span>

* <span data-ttu-id="98c06-233">**授權**： 此屬性會定義誰 toohello 客戶的訂用帳戶中的資源取得存取權與 hello 的存取層級。</span><span class="sxs-lookup"><span data-stu-id="98c06-233">**Authorizations**: This property defines who gets access and hello level of access toohello resources in customers' subscriptions.</span></span> <span data-ttu-id="98c06-234">hello 發行者可以使用它代表 hello 客戶 toomanage hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="98c06-234">hello publisher can use it toomanage hello application on behalf of hello customer.</span></span>
* <span data-ttu-id="98c06-235">**PrincipalId**： 這個屬性是使用者、 使用者群組或已授與 hello 客戶的訂用帳戶中的 hello 資源上的特定權限的應用程式的 hello Azure Active Directory (Azure AD) 識別項。</span><span class="sxs-lookup"><span data-stu-id="98c06-235">**PrincipalId**: This property is hello Azure Active Directory (Azure AD) identifier of a user, user group, or application that's granted certain permissions on hello resources in hello customer's subscription.</span></span> <span data-ttu-id="98c06-236">hello 角色定義描述 hello 權限。</span><span class="sxs-lookup"><span data-stu-id="98c06-236">hello Role Definition describes hello permissions.</span></span> 
* <span data-ttu-id="98c06-237">**角色定義**： 這個屬性是所有 hello 內建角色型存取控制 (RBAC) 角色的 Azure AD 所提供的清單。</span><span class="sxs-lookup"><span data-stu-id="98c06-237">**Role Definition**: This property is a list of all hello built-in Role-Based Access Control (RBAC) roles provided by Azure AD.</span></span> <span data-ttu-id="98c06-238">您可以選取最適合 toouse toomanage hello 資源是代表 hello 客戶的 hello 角色。</span><span class="sxs-lookup"><span data-stu-id="98c06-238">You can select hello role that's most appropriate toouse toomanage hello resources on behalf of hello customer.</span></span>

<span data-ttu-id="98c06-239">您可以新增多個授權。</span><span class="sxs-lookup"><span data-stu-id="98c06-239">You can add multiple authorizations.</span></span> <span data-ttu-id="98c06-240">建議您建立 AD 使用者群組並且在 **PrincipalId** 中指定其識別碼。</span><span class="sxs-lookup"><span data-stu-id="98c06-240">We recommend that you create an AD user group and specify its ID in **PrincipalId**.</span></span> <span data-ttu-id="98c06-241">如此一來，您可以加入更多使用者 toohello 使用者群組，但不允許 hello 需要 tooupdate hello SKU。</span><span class="sxs-lookup"><span data-stu-id="98c06-241">This way, you can add more users toohello user group without hello need tooupdate hello SKU.</span></span>

<span data-ttu-id="98c06-242">如需 RBAC 的詳細資訊，請參閱[hello Azure 入口網站中開始使用 RBAC](../active-directory/role-based-access-control-what-is.md)。</span><span class="sxs-lookup"><span data-stu-id="98c06-242">For more information about RBAC, see [Get started with RBAC in hello Azure portal](../active-directory/role-based-access-control-what-is.md).</span></span>

## <a name="marketplace-form"></a><span data-ttu-id="98c06-243">Marketplace 表單</span><span class="sxs-lookup"><span data-stu-id="98c06-243">Marketplace form</span></span>

<span data-ttu-id="98c06-244">hello Marketplace 表單詢問 hello 上顯示的欄位[Azure Marketplace](https://azuremarketplace.microsoft.com)在 hello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="98c06-244">hello Marketplace form asks for fields that show up on hello [Azure Marketplace](https://azuremarketplace.microsoft.com) and on hello [Azure portal](https://portal.azure.com/).</span></span>

### <a name="preview-subscription-ids"></a><span data-ttu-id="98c06-245">預覽訂用帳戶識別碼</span><span class="sxs-lookup"><span data-stu-id="98c06-245">Preview subscription IDs</span></span>

<span data-ttu-id="98c06-246">輸入 Azure 訂用帳戶可存取 hello 提供，發行後的識別碼的清單。</span><span class="sxs-lookup"><span data-stu-id="98c06-246">Enter a list of Azure subscription IDs that can access hello offer after it's published.</span></span> <span data-ttu-id="98c06-247">您在進行之前，您可以使用這些空白列的訂閱 tootest hello 預覽提供即時。</span><span class="sxs-lookup"><span data-stu-id="98c06-247">You can use these white-listed subscriptions tootest hello previewed offer before you make it live.</span></span> <span data-ttu-id="98c06-248">您可以編譯 too100 訂閱 hello 合作夥伴入口網站中的空白清單。</span><span class="sxs-lookup"><span data-stu-id="98c06-248">You can compile a white list of up too100 subscriptions in hello partner portal.</span></span>

### <a name="suggested-categories"></a><span data-ttu-id="98c06-249">建議的類別</span><span class="sxs-lookup"><span data-stu-id="98c06-249">Suggested categories</span></span>

<span data-ttu-id="98c06-250">選取從您提供的服務可以與最相關的 hello 清單 toofive 類別。</span><span class="sxs-lookup"><span data-stu-id="98c06-250">Select up toofive categories from hello list that your offer can be best associated with.</span></span> <span data-ttu-id="98c06-251">這些類別位於 hello 您優惠 toohello 產品類別目錄會使用的 toomap [Azure Marketplace](https://azuremarketplace.microsoft.com)和 hello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="98c06-251">These categories are used toomap your offer toohello product categories that are available in hello [Azure Marketplace](https://azuremarketplace.microsoft.com) and hello [Azure portal](https://portal.azure.com/).</span></span>

#### <a name="azure-marketplace"></a><span data-ttu-id="98c06-252">Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="98c06-252">Azure Marketplace</span></span>

<span data-ttu-id="98c06-253">managed 應用程式的 hello 摘要會顯示 hello 下列欄位：</span><span class="sxs-lookup"><span data-stu-id="98c06-253">hello summary of your managed application displays hello following fields:</span></span>

![Marketplace 摘要](./media/managed-application-author-marketplace/publishvm10.png)

<span data-ttu-id="98c06-255">hello**概觀**索引標籤上，您受管理的應用程式會顯示 hello 下列欄位：</span><span class="sxs-lookup"><span data-stu-id="98c06-255">hello **Overview** tab for your managed application displays hello following fields:</span></span>

![Marketplace 概觀](./media/managed-application-author-marketplace/publishvm11.png)

<span data-ttu-id="98c06-257">hello**計劃 + 定價**索引標籤上，您受管理的應用程式會顯示 hello 下列欄位：</span><span class="sxs-lookup"><span data-stu-id="98c06-257">hello **Plans + Pricing** tab for your managed application displays hello following fields:</span></span>

![Marketplace 方案](./media/managed-application-author-marketplace/publishvm15.png)

#### <a name="azure-portal"></a><span data-ttu-id="98c06-259">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="98c06-259">Azure portal</span></span>

<span data-ttu-id="98c06-260">managed 應用程式的 hello 摘要會顯示 hello 下列欄位：</span><span class="sxs-lookup"><span data-stu-id="98c06-260">hello summary of your managed application displays hello following fields:</span></span>

![入口網站摘要](./media/managed-application-author-marketplace/publishvm12.png)

<span data-ttu-id="98c06-262">managed 應用程式的 hello 概觀會顯示 hello 下列欄位：</span><span class="sxs-lookup"><span data-stu-id="98c06-262">hello overview for your managed application displays hello following fields:</span></span>

![入口網站概觀](./media/managed-application-author-marketplace/publishvm13.png)

#### <a name="logo-guidelines"></a><span data-ttu-id="98c06-264">標誌指導方針</span><span class="sxs-lookup"><span data-stu-id="98c06-264">Logo guidelines</span></span>

<span data-ttu-id="98c06-265">請遵循下列指導方針任何您在 hello Cloud Partner 入口網站中上傳的標誌：</span><span class="sxs-lookup"><span data-stu-id="98c06-265">Follow these guidelines for any logo that you upload in hello Cloud Partner portal:</span></span>

*   <span data-ttu-id="98c06-266">hello Azure 設計具有簡單的調色盤。</span><span class="sxs-lookup"><span data-stu-id="98c06-266">hello Azure design has a simple color palette.</span></span> <span data-ttu-id="98c06-267">限制 hello 數目主要和次要色彩上您的標誌。</span><span class="sxs-lookup"><span data-stu-id="98c06-267">Limit hello number of primary and secondary colors on your logo.</span></span>
*   <span data-ttu-id="98c06-268">hello hello 入口網站的佈景主題色彩是白色與黑色。</span><span class="sxs-lookup"><span data-stu-id="98c06-268">hello theme colors of hello portal are white and black.</span></span> <span data-ttu-id="98c06-269">請勿使用這些色彩 hello 背景色彩為您的標誌。</span><span class="sxs-lookup"><span data-stu-id="98c06-269">Don't use these colors as hello background color for your logo.</span></span> <span data-ttu-id="98c06-270">使用色彩，讓您的標誌 hello 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="98c06-270">Use a color that makes your logo prominent in hello portal.</span></span> <span data-ttu-id="98c06-271">建議您使用簡單的主要色彩。</span><span class="sxs-lookup"><span data-stu-id="98c06-271">We recommend simple primary colors.</span></span> <span data-ttu-id="98c06-272">*如果您使用透明背景，請確定 hello 標誌和文字不是白色的黑色或藍色。*</span><span class="sxs-lookup"><span data-stu-id="98c06-272">*If you use a transparent background, make sure that hello logo and text aren't white, black, or blue.*</span></span>
*   <span data-ttu-id="98c06-273">請勿在 hello 標誌上使用漸層的背景。</span><span class="sxs-lookup"><span data-stu-id="98c06-273">Don't use a gradient background on hello logo.</span></span>
*   <span data-ttu-id="98c06-274">不要將文字放在 hello 標誌，即使貴公司或品牌名稱。</span><span class="sxs-lookup"><span data-stu-id="98c06-274">Don't place text on hello logo, not even your company or brand name.</span></span> <span data-ttu-id="98c06-275">hello 的外觀與您的標誌應該是一般，而且避免漸層。</span><span class="sxs-lookup"><span data-stu-id="98c06-275">hello look and feel of your logo should be flat and avoid gradients.</span></span>
*   <span data-ttu-id="98c06-276">請確定 hello 標誌不會自動縮放。</span><span class="sxs-lookup"><span data-stu-id="98c06-276">Make sure hello logo isn't stretched.</span></span>

#### <a name="hero-logo"></a><span data-ttu-id="98c06-277">主圖標誌</span><span class="sxs-lookup"><span data-stu-id="98c06-277">Hero logo</span></span>

<span data-ttu-id="98c06-278">hello 英雄標誌是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="98c06-278">hello hero logo is optional.</span></span> <span data-ttu-id="98c06-279">hello 發行者可以選擇不 tooupload 英雄標誌。</span><span class="sxs-lookup"><span data-stu-id="98c06-279">hello publisher can choose not tooupload a hero logo.</span></span> <span data-ttu-id="98c06-280">上傳 hello 英雄圖示之後，無法刪除。</span><span class="sxs-lookup"><span data-stu-id="98c06-280">After hello hero icon is uploaded, it can't be deleted.</span></span> <span data-ttu-id="98c06-281">在這段時間，hello 夥伴必須遵循英雄圖示的 hello Marketplace 指導方針。</span><span class="sxs-lookup"><span data-stu-id="98c06-281">At that time, hello partner must follow hello Marketplace guidelines for hero icons.</span></span>

<span data-ttu-id="98c06-282">請遵循下列指導方針 hello 英雄標誌圖示：</span><span class="sxs-lookup"><span data-stu-id="98c06-282">Follow these guidelines for hello hero logo icon:</span></span>

*   <span data-ttu-id="98c06-283">hello 發行者顯示名稱、 hello 計劃，顯示標題與 hello 供應項目完整摘要會以白色。</span><span class="sxs-lookup"><span data-stu-id="98c06-283">hello publisher display name, hello plan title, and hello offer long summary are displayed in white.</span></span> <span data-ttu-id="98c06-284">因此，不是使用淺色背景 hello hello 英雄圖示。</span><span class="sxs-lookup"><span data-stu-id="98c06-284">Therefore, don't use a light color for hello background of hello hero icon.</span></span> <span data-ttu-id="98c06-285">主圖圖示不得使用黑色、白色和透明背景。</span><span class="sxs-lookup"><span data-stu-id="98c06-285">A black, white, or transparent background isn't allowed for hero icons.</span></span>
*   <span data-ttu-id="98c06-286">列出 hello 供應項目之後，hello 發行者顯示名稱、 hello 計劃標題、 hello 供應項目完整摘要和 hello**建立**按鈕將以程式設計的方式內嵌在 hello 英雄標誌。</span><span class="sxs-lookup"><span data-stu-id="98c06-286">After hello offer is listed, hello publisher display name, hello plan title, hello offer long summary, and hello **Create** button are embedded programmatically inside hello hero logo.</span></span> <span data-ttu-id="98c06-287">因此，請勿輸入任何文字時設計 hello 英雄標誌。</span><span class="sxs-lookup"><span data-stu-id="98c06-287">Consequently, don't enter any text while you design hello hero logo.</span></span> <span data-ttu-id="98c06-288">保留空白空間上 hello 右因為 hello 文字包含以程式設計方式在該空間。</span><span class="sxs-lookup"><span data-stu-id="98c06-288">Leave empty space on hello right because hello text is included programmatically in that space.</span></span> <span data-ttu-id="98c06-289">hello 空白空間的 hello 文字應該是右 hello 415 x 100 像素。</span><span class="sxs-lookup"><span data-stu-id="98c06-289">hello empty space for hello text should be 415 x 100 pixels on hello right.</span></span> <span data-ttu-id="98c06-290">它可經由從 hello 左 370 像素為單位。</span><span class="sxs-lookup"><span data-stu-id="98c06-290">It's offset by 370 pixels from hello left.</span></span>

    ![主圖標誌範例](./media/managed-application-author-marketplace/publishvm14.png)

## <a name="support-form"></a><span data-ttu-id="98c06-292">支援表單</span><span class="sxs-lookup"><span data-stu-id="98c06-292">Support form</span></span>

<span data-ttu-id="98c06-293">填寫 hello**支援**貴公司連絡人表單和支援。</span><span class="sxs-lookup"><span data-stu-id="98c06-293">Fill out hello **Support** form with support contacts from your company.</span></span> <span data-ttu-id="98c06-294">此資訊可能是工程連絡人和客戶支援連絡人。</span><span class="sxs-lookup"><span data-stu-id="98c06-294">This information might be engineering contacts and customer support contacts.</span></span>

## <a name="publish-an-offer"></a><span data-ttu-id="98c06-295">發佈提供項目</span><span class="sxs-lookup"><span data-stu-id="98c06-295">Publish an offer</span></span>

<span data-ttu-id="98c06-296">請填寫所有 hello 區段之後，請選取**發行**可讓您提供可用 toocustomers toostart hello 程序。</span><span class="sxs-lookup"><span data-stu-id="98c06-296">After you fill out all hello sections, select **Publish** toostart hello process that makes your offer available toocustomers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="98c06-297">後續步驟</span><span class="sxs-lookup"><span data-stu-id="98c06-297">Next steps</span></span>

* <span data-ttu-id="98c06-298">對於簡介 toomanaged 應用程式，請參閱[受管理應用程式概觀](managed-application-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="98c06-298">For an introduction toomanaged applications, see [Managed application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="98c06-299">使用來自 hello Marketplace 的受管理應用程式的相關資訊，請參閱[取用 Azure managed hello Marketplace 中的應用程式](managed-application-consume-marketplace.md)。</span><span class="sxs-lookup"><span data-stu-id="98c06-299">For information about consuming a managed application from hello Marketplace, see [Consume Azure managed applications in hello Marketplace](managed-application-consume-marketplace.md).</span></span>
* <span data-ttu-id="98c06-300">如需發佈 Service Catalog 受管理應用程式的資訊，請參閱[建立和發佈 Service Catalog 受管理的應用程式](managed-application-publishing.md)。</span><span class="sxs-lookup"><span data-stu-id="98c06-300">For information about publishing a Service Catalog managed application, see [Create and publish a Service Catalog managed application](managed-application-publishing.md).</span></span>
* <span data-ttu-id="98c06-301">如需使用 Service Catalog 受管理應用程式的詳細資訊，請參閱[使用 Service Catalog 受管理的應用程式](managed-application-consumption.md)。</span><span class="sxs-lookup"><span data-stu-id="98c06-301">For information about consuming a Service Catalog managed application, see [Consume a Service Catalog managed application](managed-application-consumption.md).</span></span>
