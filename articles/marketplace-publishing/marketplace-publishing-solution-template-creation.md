---
title: "aaaGuide toocreating hello Marketplace 的方案範本 |Microsoft 文件"
description: "取得 toocreate，認證，以及部署在 hello Azure Marketplace 購買的多部 VM 映像解決方案範本的詳細的指示。"
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: e14e05f2-2385-4ce0-b351-0747cb74ba19
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: b0e7067176337dd0d3f6f6ec04c963f80f706ab0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="guide-toocreate-a-solution-template-for-azure-marketplace"></a><span data-ttu-id="233b5-103">指南 toocreate Azure Marketplace 的方案範本</span><span class="sxs-lookup"><span data-stu-id="233b5-103">Guide toocreate a solution template for Azure Marketplace</span></span>
<span data-ttu-id="233b5-104">完成步驟 1 之後[帳戶建立與註冊][link-acct-creation]，我們會引導您在 Azure 相容解決方案範本的 hello 建立[技術建立的必要條件方案範本](marketplace-publishing-solution-template-creation-prerequisites.md)。</span><span class="sxs-lookup"><span data-stu-id="233b5-104">After completing step 1, [Account creation and registration][link-acct-creation], we guided you on hello creation of an Azure-compatible solution template at [Technical prerequisites for creating a solution template](marketplace-publishing-solution-template-creation-prerequisites.md).</span></span> <span data-ttu-id="233b5-105">現在我們將逐步引導您建立方案範本的多個 Vm 上 hello hello 步驟[發佈入口網站][ link-pubportal] hello Azure Marketplace。</span><span class="sxs-lookup"><span data-stu-id="233b5-105">Now we will walk you through hello steps for creating a solution template for multiple VMs on hello [Publishing Portal][link-pubportal] for hello Azure Marketplace.</span></span>

## <a name="create-your-solution-template-offer-in-hello-publishing-portal"></a><span data-ttu-id="233b5-106">在 hello 發佈入口網站中建立您的方案範本提供的服務</span><span class="sxs-lookup"><span data-stu-id="233b5-106">Create your solution template offer in hello Publishing Portal</span></span>
<span data-ttu-id="233b5-107">跳過[https://publish.windowsazure.com](http://publish.windowsazure.com)。當第一次 toohello hello 進行登入[發佈入口網站](https://publish.windowsazure.com/)，使用 hello 與已註冊您的公司賣方設定檔使用相同帳戶。</span><span class="sxs-lookup"><span data-stu-id="233b5-107">Go too [https://publish.windowsazure.com](http://publish.windowsazure.com). When signing in for hello first time toohello [Publishing Portal](https://publish.windowsazure.com/), use hello same account with which your company’s seller profile was registered.</span></span> <span data-ttu-id="233b5-108">稍後，您可以為共同管理員 hello 發佈入口網站中加入任何您公司的員工。</span><span class="sxs-lookup"><span data-stu-id="233b5-108">Later, you can add any employee of your company as a co-admin in hello Publishing Portal.</span></span>

### <a name="1-select-solution-templates"></a><span data-ttu-id="233b5-109">1.選取 [解決方案範本]</span><span class="sxs-lookup"><span data-stu-id="233b5-109">1. Select "Solution templates"</span></span>
  ![繪圖][img-pubportal-menu-sol-templ]

### <a name="2-create-a-new-solution-template"></a><span data-ttu-id="233b5-111">2.建立新的解決方案範本</span><span class="sxs-lookup"><span data-stu-id="233b5-111">2. Create a new solution template</span></span>
  ![繪圖][img-pubportal-sol-templ-new]

### <a name="3-start-with-topologies"></a><span data-ttu-id="233b5-113">3.開始使用拓樸</span><span class="sxs-lookup"><span data-stu-id="233b5-113">3. Start with topologies</span></span>
<span data-ttu-id="233b5-114">方案範本是其拓撲的 「 父 」 tooall。</span><span class="sxs-lookup"><span data-stu-id="233b5-114">A solution template is a "parent" tooall of its topologies.</span></span> <span data-ttu-id="233b5-115">您可以在一個供應項目/解決方案範本中定義多個拓撲。</span><span class="sxs-lookup"><span data-stu-id="233b5-115">You can define multiple topologies in one offer/solution template.</span></span> <span data-ttu-id="233b5-116">當 toostaging 推入的供應項目時，它是推入與所有其拓撲。</span><span class="sxs-lookup"><span data-stu-id="233b5-116">When an offer is pushed toostaging, it is pushed with all of its topologies.</span></span> <span data-ttu-id="233b5-117">請遵循以下 toodefine 的 hello 步驟您提供的服務：</span><span class="sxs-lookup"><span data-stu-id="233b5-117">Follow hello steps below toodefine your offer:</span></span>     

* <span data-ttu-id="233b5-118">建立拓樸: 「 拓樸識別項 」 通常是 hello 方案範本 hello 拓樸的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="233b5-118">Create a Topology: “Topology Identifier” is typically hello name of hello topology for hello solution template.</span></span> <span data-ttu-id="233b5-119">hello 拓撲識別碼用於 hello URL 如下所示：</span><span class="sxs-lookup"><span data-stu-id="233b5-119">hello topology identifier is used in hello URL as shown below:</span></span>

  <span data-ttu-id="233b5-120">Azure Marketplace：http://azure.microsoft.com/marketplace/partners/{PublisherNamespace}/{OfferIdentifier}{TopologyIdentifier}</span><span class="sxs-lookup"><span data-stu-id="233b5-120">Azure Marketplace: http://azure.microsoft.com/marketplace/partners/{PublisherNamespace}/{OfferIdentifier}{TopologyIdentifier}</span></span>

  <span data-ttu-id="233b5-121">Azure 入口網站：https://portal.azure.com/#gallery/{PublisherNamespace}.{OfferIdentifier}{TopologyIdentifier}</span><span class="sxs-lookup"><span data-stu-id="233b5-121">Azure Portal: https://portal.azure.com/#gallery/{PublisherNamespace}.{OfferIdentifier}{TopologyIdentifier}</span></span>
* <span data-ttu-id="233b5-122">加入新的版本。</span><span class="sxs-lookup"><span data-stu-id="233b5-122">Add a new version.</span></span>

### <a name="4-get-your-topology-versions-certified"></a><span data-ttu-id="233b5-123">4.讓您的拓撲版本取得認證</span><span class="sxs-lookup"><span data-stu-id="233b5-123">4. Get your topology versions certified</span></span>
<span data-ttu-id="233b5-124">上傳包含所有必要的檔案 tooprovision hello 拓樸的該特定版本的 zip 檔案。</span><span class="sxs-lookup"><span data-stu-id="233b5-124">Upload a zip file that contains all required files tooprovision that particular version of hello topology.</span></span> <span data-ttu-id="233b5-125">此 zip 檔案必須包含下列 hello:</span><span class="sxs-lookup"><span data-stu-id="233b5-125">This zip file must contain hello following:</span></span>

* <span data-ttu-id="233b5-126">*mainTemplate.json* 和 *createUiDefinition.json* 檔案在其根目錄上。</span><span class="sxs-lookup"><span data-stu-id="233b5-126">*mainTemplate.json* and *createUiDefinition.json* file at its root directory.</span></span>
* <span data-ttu-id="233b5-127">任何連結的範本和所有必要的指令碼。</span><span class="sxs-lookup"><span data-stu-id="233b5-127">Any linked templates and all required scripts.</span></span>

  > [!TIP]
  > <span data-ttu-id="233b5-128">當您的開發人員用於建立 hello 方案範本拓撲，並且取得這些認證，hello 商務您公司的行銷及/或法務部門可以使用 hello 行銷和合法的內容。</span><span class="sxs-lookup"><span data-stu-id="233b5-128">While your developers work on creating hello solution template topologies and getting them certified, hello business, marketing, and/or legal departments of your company can work on hello marketing and legal content.</span></span>
  >
  >

## <a name="next-steps"></a><span data-ttu-id="233b5-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="233b5-129">Next steps</span></span>
<span data-ttu-id="233b5-130">現在，您會建立您的解決方案範本，並上傳 hello zip 檔案，請遵循 hello hello 指示[Marketplace 行銷內容指南](marketplace-publishing-push-to-staging.md)之前推入 hello 優惠 toostaging。</span><span class="sxs-lookup"><span data-stu-id="233b5-130">Now that you created your solution template and uploaded hello zip file, please follow hello instructions in hello [Marketplace marketing content guide](marketplace-publishing-push-to-staging.md) before pushing hello offer toostaging.</span></span> <span data-ttu-id="233b5-131">toosee hello 整組 marketplace 發行發行項，請瀏覽[快速入門： 如何 toopublish 優惠 toohello Azure Marketplace](marketplace-publishing-getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="233b5-131">toosee hello full set of marketplace publishing articles, visit [Getting started: How toopublish an offer toohello Azure Marketplace](marketplace-publishing-getting-started.md).</span></span>

<span data-ttu-id="233b5-132">您也可能對以下相關文章有興趣：</span><span class="sxs-lookup"><span data-stu-id="233b5-132">You might also be interested in these related articles:</span></span>

* <span data-ttu-id="233b5-133">VM 映像： [關於 Azure 中的虛擬機器映像](https://msdn.microsoft.com/library/azure/dn790290.aspx)</span><span class="sxs-lookup"><span data-stu-id="233b5-133">VM images: [About Virtual Machine Images in Azure](https://msdn.microsoft.com/library/azure/dn790290.aspx)</span></span>
* <span data-ttu-id="233b5-134">VM 延伸模組：[VM 代理程式與 VM 延伸模組概觀](https://msdn.microsoft.com/library/azure/dn832621.aspx)及 [Azure VM 延伸模組與功能](https://msdn.microsoft.com/library/azure/dn606311.aspx)</span><span class="sxs-lookup"><span data-stu-id="233b5-134">VM extensions: [VM Agent and VM Extensions Overview](https://msdn.microsoft.com/library/azure/dn832621.aspx) and [Azure VM Extensions and Features](https://msdn.microsoft.com/library/azure/dn606311.aspx)</span></span>
* <span data-ttu-id="233b5-135">Azure Resource Manager：[撰寫 Azure Resource Manager 範本 (英文)](../azure-resource-manager/resource-group-authoring-templates.md)和[簡單範本範例](https://github.com/rjmax/ArmExamples)</span><span class="sxs-lookup"><span data-stu-id="233b5-135">Azure Resource Manager: [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md) and [Simple Template Examples](https://github.com/rjmax/ArmExamples)</span></span>
* <span data-ttu-id="233b5-136">儲存體帳戶會先調節：[如何儲存體帳戶節流 tooMonitor](http://blogs.msdn.com/b/mast/archive/2014/08/02/how-to-monitor-for-storage-account-throttling.aspx)和[高階儲存體](../storage/common/storage-premium-storage.md#scalability-and-performance-targets)</span><span class="sxs-lookup"><span data-stu-id="233b5-136">Storage account throttles: [How tooMonitor for Storage Account Throttling](http://blogs.msdn.com/b/mast/archive/2014/08/02/how-to-monitor-for-storage-account-throttling.aspx) and [Premium storage](../storage/common/storage-premium-storage.md#scalability-and-performance-targets)</span></span>

[img-pubportal-menu-sol-templ]:media/marketplace-publishing-solution-template-creation/pubportal-menu-solution-templates.png
[img-pubportal-sol-templ-new]:media/marketplace-publishing-solution-template-creation/pubportal-solution-template-new.png
[link-acct-creation]:marketplace-publishing-accounts-creation-registration.md
[link-pubportal]:https://publish.windowsazure.com
