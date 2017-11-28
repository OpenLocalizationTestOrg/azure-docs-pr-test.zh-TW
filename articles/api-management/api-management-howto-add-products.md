---
title: "aaaHow toocreate 及發佈產品在 Azure API 管理"
description: "深入了解如何 toocreate 並發行產品在 Azure API 管理。"
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 31de55cb-9384-490b-a2f2-6dfcf83da764
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: f0a37f08b4e29ca68be9caec4c7604e3b4b6aaa6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-publish-a-product-in-azure-api-management"></a><span data-ttu-id="173ce-103">如何 toocreate 及發佈產品在 Azure API 管理</span><span class="sxs-lookup"><span data-stu-id="173ce-103">How toocreate and publish a product in Azure API Management</span></span>
<span data-ttu-id="173ce-104">在 Azure API 管理中，產品包含一或多個應用程式開發介面，以及使用量配額與 hello 使用條款。</span><span class="sxs-lookup"><span data-stu-id="173ce-104">In Azure API Management, a product contains one or more APIs as well as a usage quota and hello terms of use.</span></span> <span data-ttu-id="173ce-105">產品發行之後，開發人員可以訂閱 toohello 產品，並開始 toouse hello 產品的 Api。</span><span class="sxs-lookup"><span data-stu-id="173ce-105">Once a product is published, developers can subscribe toohello product and begin toouse hello product's APIs.</span></span> <span data-ttu-id="173ce-106">hello 主題將提供指南 toocreating 產品，以加入應用程式開發介面，和發行適用於開發人員。</span><span class="sxs-lookup"><span data-stu-id="173ce-106">hello topic provides a guide toocreating a product, adding an API, and publishing it for developers.</span></span>

## <span data-ttu-id="173ce-107"><a name="create-product"> </a>建立產品</span><span class="sxs-lookup"><span data-stu-id="173ce-107"><a name="create-product"> </a>Create a product</span></span>
<span data-ttu-id="173ce-108">作業可加入與 hello 發行者入口網站中設定 tooan API。</span><span class="sxs-lookup"><span data-stu-id="173ce-108">Operations are added and configured tooan API in hello publisher portal.</span></span> <span data-ttu-id="173ce-109">tooaccess hello 發行者入口網站中，按一下**發行者入口網站**API 管理服務的 hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="173ce-109">tooaccess hello publisher portal, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span>

![發行者入口網站][api-management-management-console]

> <span data-ttu-id="173ce-111">如果您尚未建立 API 管理服務執行個體，請參閱[建立 API 管理服務執行個體][ Create an API Management service instance]在 hello[開始使用 Azure API 管理][Get started with Azure API Management]教學課程。</span><span class="sxs-lookup"><span data-stu-id="173ce-111">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="173ce-112">按一下**產品**hello 左的 toodisplay hello 上的 [hello] 功能表中**產品**頁面，然後按一下**新增產品**。</span><span class="sxs-lookup"><span data-stu-id="173ce-112">Click on **Products** in hello menu on hello left toodisplay hello **Products** page, and click **Add Product**.</span></span>

![產品][api-management-products]

![New product][api-management-add-new-product]

<span data-ttu-id="173ce-115">輸入 hello 產品的描述性名稱在 hello**名稱**欄位以及在 hello hello 產品的描述**描述**欄位。</span><span class="sxs-lookup"><span data-stu-id="173ce-115">Enter a descriptive name for hello product in hello **Name** field and a description of hello product in hello **Description** field.</span></span>

<span data-ttu-id="173ce-116">API 管理中的產品可以是 [開放] 或 [受保護]。</span><span class="sxs-lookup"><span data-stu-id="173ce-116">Products in API Management can be **Open** or **Protected**.</span></span> <span data-ttu-id="173ce-117">受保護的產品必須是它們可以用於，開啟時的訂閱的 toobefore 不用在訂用帳戶可以使用產品。</span><span class="sxs-lookup"><span data-stu-id="173ce-117">Protected products must be subscribed toobefore they can be used, while open products can be used without a subscription.</span></span> <span data-ttu-id="173ce-118">請檢查**需要訂用帳戶**toocreate 的受保護的產品，需要訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="173ce-118">Check **Require subscription** toocreate a protected product that requires a subscription.</span></span> <span data-ttu-id="173ce-119">這是 hello 預設設定。</span><span class="sxs-lookup"><span data-stu-id="173ce-119">This is hello default setting.</span></span>

<span data-ttu-id="173ce-120">請檢查**需要訂閱核准**如果您想要系統管理員 tooreview 並接受或拒絕的訂閱嘗試 toothis 產品。</span><span class="sxs-lookup"><span data-stu-id="173ce-120">Check **Require subscription approval** if you want an administrator tooreview and accept or reject subscription attempts toothis product.</span></span> <span data-ttu-id="173ce-121">如果 hello 方塊未選取，訂閱嘗試將會自動核准。</span><span class="sxs-lookup"><span data-stu-id="173ce-121">If hello box is unchecked, subscription attempts will be auto-approved.</span></span> <span data-ttu-id="173ce-122">如需有關訂閱的詳細資訊，請參閱[檢視 「 訂閱者 」 tooa 產品][View subscribers tooa product]。</span><span class="sxs-lookup"><span data-stu-id="173ce-122">For more information on subscriptions, see [View subscribers tooa product][View subscribers tooa product].</span></span>

<span data-ttu-id="173ce-123">tooallow 開發人員帳戶 toosubscribe 多次 toohello 產品，請檢查 hello**允許多個訂閱**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="173ce-123">tooallow developer accounts toosubscribe multiple times toohello product, check hello **Allow multiple subscriptions** check box.</span></span> <span data-ttu-id="173ce-124">如果未核取此方塊，每個開發人員帳戶可以訂閱一次 toohello 產品。</span><span class="sxs-lookup"><span data-stu-id="173ce-124">If this box is not checked, each developer account can subscribe only a single time toohello product.</span></span>

![無限制的多項訂閱][api-management-unlimited-multiple-subscriptions]

<span data-ttu-id="173ce-126">toolimit hello 計數的多個同時進行的訂閱，檢查 hello**同時訂閱的數目限制**核取方塊，然後輸入 hello 訂用帳戶限制。</span><span class="sxs-lookup"><span data-stu-id="173ce-126">toolimit hello count of multiple simultaneous subscriptions, check hello **Limit number of simultaneous subscriptions to** check box and enter hello subscription limit.</span></span> <span data-ttu-id="173ce-127">在下列範例的 hello，同時訂閱是有限的 toofour 每個開發人員帳戶。</span><span class="sxs-lookup"><span data-stu-id="173ce-127">In hello following example, simultaneous subscriptions are limited toofour per developer account.</span></span>

![四個多項訂閱][api-management-four-multiple-subscriptions]

<span data-ttu-id="173ce-129">一旦設定所有新的產品選項，按一下**儲存**toocreate hello 新產品。</span><span class="sxs-lookup"><span data-stu-id="173ce-129">Once all new product options are configured, click **Save** toocreate hello new product.</span></span>

![產品][api-management-products-page]

> <span data-ttu-id="173ce-131">根據預設，新的產品為未發行，而是可見的唯一 toohello**管理員**群組。</span><span class="sxs-lookup"><span data-stu-id="173ce-131">By default new products are unpublished, and are visible only toohello  **Administrators** group.</span></span>
> 
> 

<span data-ttu-id="173ce-132">tooconfigure 產品中，按一下 hello 中的 hello 產品名稱**產品** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="173ce-132">tooconfigure a product, click on hello product name in hello **Products** tab.</span></span>

## <span data-ttu-id="173ce-133"><a name="add-apis"></a>新增應用程式開發介面 tooa 產品</span><span class="sxs-lookup"><span data-stu-id="173ce-133"><a name="add-apis"> </a>Add APIs tooa product</span></span>
<span data-ttu-id="173ce-134">hello**產品**頁面包含四個連結的組態：**摘要**，**設定**，**可視性**，和**訂閱者**。</span><span class="sxs-lookup"><span data-stu-id="173ce-134">hello **Products** page contains four links for configuration: **Summary**, **Settings**, **Visibility**, and **Subscribers**.</span></span> <span data-ttu-id="173ce-135">hello**摘要** 索引標籤是您可以用它來新增應用程式開發介面和發行，或取消發行的產品。</span><span class="sxs-lookup"><span data-stu-id="173ce-135">hello **Summary** tab is where you can add APIs and publish or unpublish a product.</span></span>

![摘要][api-management-new-product-summary]

<span data-ttu-id="173ce-137">發行您的產品之前您需要 tooadd 一或多個應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="173ce-137">Before publishing your product you need tooadd one or more APIs.</span></span> <span data-ttu-id="173ce-138">toodo 此，依序按一下**新增應用程式開發介面 tooproduct**。</span><span class="sxs-lookup"><span data-stu-id="173ce-138">toodo this, click **Add API tooproduct**.</span></span>

![Add APIs][api-management-add-apis-to-product]

<span data-ttu-id="173ce-140">選取 hello 預期應用程式開發介面和按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="173ce-140">Select hello desired APIs and click **Save**.</span></span>

## <span data-ttu-id="173ce-141"><a name="add-description"></a>加入描述性資訊 tooa 產品</span><span class="sxs-lookup"><span data-stu-id="173ce-141"><a name="add-description"> </a>Add descriptive information tooa product</span></span>
<span data-ttu-id="173ce-142">hello**設定**索引標籤可讓您 tooprovide hello 產品，例如其用途、 hello 應用程式開發介面，它提供的存取權，以及其他有用的資訊有關的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="173ce-142">hello **Settings** tab allows you tooprovide detailed information about hello product such as its purpose, hello APIs it provides access to, and other useful information.</span></span> <span data-ttu-id="173ce-143">hello 內容呼叫 hello 應用程式開發介面，且可以寫入純文字或 HTML 標記中的 hello 開發人員為目標。</span><span class="sxs-lookup"><span data-stu-id="173ce-143">hello content is targeted at hello developers that will be calling hello API and can be written in plain text or HTML markup.</span></span>

![Product settings][api-management-product-settings]

<span data-ttu-id="173ce-145">請檢查**需要訂用帳戶**toocreate 受保護的產品需要使用，或清除訂閱 toobe hello 核取方塊 toocreate 已開啟的產品可以呼叫且不用訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="173ce-145">Check **Require subscription** toocreate a protected product that requires a subscription toobe used, or clear hello checkbox toocreate an open product that can be called without a subscription.</span></span>

<span data-ttu-id="173ce-146">選取**需要訂閱核准**toomanually 如果您想要核准所有產品的訂閱要求。</span><span class="sxs-lookup"><span data-stu-id="173ce-146">Select **Require subscription approval** if you want toomanually approve all product subscription requests.</span></span> <span data-ttu-id="173ce-147">依預設會自動同意所有產品訂閱。</span><span class="sxs-lookup"><span data-stu-id="173ce-147">By default all product subscriptions are granted automatically.</span></span>

<span data-ttu-id="173ce-148">tooallow 開發人員帳戶 toosubscribe 多次 toohello 產品，請檢查 hello**允許多個訂閱**核取方塊，並選擇性地指定限制。</span><span class="sxs-lookup"><span data-stu-id="173ce-148">tooallow developer accounts toosubscribe multiple times toohello product, check hello **Allow multiple subscriptions** check box and optionally specify a limit.</span></span> <span data-ttu-id="173ce-149">如果未核取此方塊，每個開發人員帳戶可以訂閱一次 toohello 產品。</span><span class="sxs-lookup"><span data-stu-id="173ce-149">If this box is not checked, each developer account can subscribe only a single time toohello product.</span></span>

<span data-ttu-id="173ce-150">選擇性地填入 hello**使用條款**欄位描述的 「 訂閱者 」 必須接受訂單 toouse hello 產品中的 hello 產品 hello 使用條款。</span><span class="sxs-lookup"><span data-stu-id="173ce-150">Optionally fill in hello **Terms of use** field describing hello terms of use for hello product which subscribers must accept in order toouse hello product.</span></span>

## <span data-ttu-id="173ce-151"><a name="publish-product"> </a>發行產品</span><span class="sxs-lookup"><span data-stu-id="173ce-151"><a name="publish-product"> </a>Publish a product</span></span>
<span data-ttu-id="173ce-152">在呼叫 hello 應用程式開發介面的產品前，必須先發佈 hello 產品。</span><span class="sxs-lookup"><span data-stu-id="173ce-152">Before hello APIs in a product can be called, hello product must be published.</span></span> <span data-ttu-id="173ce-153">在 hello**摘要**hello 產品的索引標籤上，按一下 **發行**，然後按一下 **是，將它發行**tooconfirm。</span><span class="sxs-lookup"><span data-stu-id="173ce-153">On hello **Summary** tab for hello product, click **Publish**, and then click **Yes, publish it** tooconfirm.</span></span> <span data-ttu-id="173ce-154">按一下 toomake 先前發行的產品私用**取消發行**。</span><span class="sxs-lookup"><span data-stu-id="173ce-154">toomake a previously published product private, click **Unpublish**.</span></span>

![Publish product][api-management-publish-product]

## <span data-ttu-id="173ce-156"><a name="make-visible"></a>使產品可見 toodevelopers</span><span class="sxs-lookup"><span data-stu-id="173ce-156"><a name="make-visible"> </a>Make a product visible toodevelopers</span></span>
<span data-ttu-id="173ce-157">hello**可視性**索引標籤可讓您 toochoose 哪些角色可以 toosee hello 產品在 hello 開發人員入口網站並訂閱 toohello 產品。</span><span class="sxs-lookup"><span data-stu-id="173ce-157">hello **Visibility** tab allows you toochoose which roles are able toosee hello product on hello developer portal and subscribe toohello product.</span></span>

![Product visibility][api-management-product-visiblity]

<span data-ttu-id="173ce-159">tooenable 或停用的群組中的 hello 開發人員的產品的可見性檢查或取消核取 hello hello 群組旁邊的核取方塊，然後按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="173ce-159">tooenable or disable visibility of a product for hello developers in a group, check or uncheck hello check box beside hello group and then click **Save**.</span></span>

> <span data-ttu-id="173ce-160">如需詳細資訊，請參閱[toocreate 並用群組 toomanage 開發人員帳戶在 Azure API 管理的如何][How toocreate and use groups toomanage developer accounts in Azure API Management]。</span><span class="sxs-lookup"><span data-stu-id="173ce-160">For more information, see [How toocreate and use groups toomanage developer accounts in Azure API Management][How toocreate and use groups toomanage developer accounts in Azure API Management].</span></span>
> 
> 

## <span data-ttu-id="173ce-161"><a name="view-subscribers"></a>檢視 「 訂閱者 」 tooa 產品</span><span class="sxs-lookup"><span data-stu-id="173ce-161"><a name="view-subscribers"> </a>View subscribers tooa product</span></span>
<span data-ttu-id="173ce-162">hello **「 訂閱者 」**索引標籤會列出 hello 開發人員已訂閱 toohello 產品。</span><span class="sxs-lookup"><span data-stu-id="173ce-162">hello **Subscribers** tab lists hello developers who have subscribed toohello product.</span></span> <span data-ttu-id="173ce-163">hello 詳細資料和設定每位開發人員可以檢視上 hello 開發人員的名稱即可。</span><span class="sxs-lookup"><span data-stu-id="173ce-163">hello details and settings for each developer can be viewed by clicking on hello developer's name.</span></span> <span data-ttu-id="173ce-164">在此範例中沒有開發人員尚未訂閱 toohello 產品。</span><span class="sxs-lookup"><span data-stu-id="173ce-164">In this example no developers have yet subscribed toohello product.</span></span>

![開發人員][api-management-developer-list]

## <span data-ttu-id="173ce-166"><a name="next-steps"> </a>後續步驟</span><span class="sxs-lookup"><span data-stu-id="173ce-166"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="173ce-167">一次 hello 所需的應用程式開發介面會加入與 hello 產品發行時，開發人員可以訂閱 toohello 產品，並開始 toocall hello 應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="173ce-167">Once hello desired APIs are added and hello product published, developers can subscribe toohello product and begin toocall hello APIs.</span></span> <span data-ttu-id="173ce-168">如需有關這些項目和進階產品組態的示範教學課程，請參閱 [如何在 Azure API 管理中建立和設定進階產品設定][How create and configure advanced product settings in Azure API Management]。</span><span class="sxs-lookup"><span data-stu-id="173ce-168">For a tutorial that demonstrates these items as well as advanced product configuration see [How create and configure advanced product settings in Azure API Management][How create and configure advanced product settings in Azure API Management].</span></span>

<span data-ttu-id="173ce-169">如需有關使用產品的詳細資訊，請參閱下列視訊 hello。</span><span class="sxs-lookup"><span data-stu-id="173ce-169">For more information about working with products, see hello following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Using-Products/player]
> 
> 

[Create a product]: #create-product
[Add APIs tooa product]: #add-apis
[Add descriptive information tooa product]: #add-description
[Publish a product]: #publish-product
[Make a product visible toodevelopers]: #make-visible
[View subscribers tooa product]: #view-subscribers
[Next steps]: #next-steps

[api-management-management-console]: ./media/api-management-howto-add-products/api-management-management-console.png
[api-management-add-product]: ./media/api-management-howto-add-products/api-management-add-product.png
[api-management-add-new-product]: ./media/api-management-howto-add-products/api-management-add-new-product.png
[api-management-unlimited-multiple-subscriptions]: ./media/api-management-howto-add-products/api-management-unlimited-multiple-subscriptions.png
[api-management-four-multiple-subscriptions]: ./media/api-management-howto-add-products/api-management-four-multiple-subscriptions.png
[api-management-products-page]: ./media/api-management-howto-add-products/api-management-products-page.png
[api-management-new-product-summary]: ./media/api-management-howto-add-products/api-management-new-product-summary.png
[api-management-add-apis-to-product]: ./media/api-management-howto-add-products/api-management-add-apis-to-product.png
[api-management-product-settings]: ./media/api-management-howto-add-products/api-management-product-settings.png
[api-management-publish-product]: ./media/api-management-howto-add-products/api-management-publish-product.png
[api-management-product-visiblity]: ./media/api-management-howto-add-products/api-management-product-visibility.png
[api-management-developer-list]: ./media/api-management-howto-add-products/api-management-developer-list.png



[api-management-products]: ./media/api-management-howto-add-products/api-management-products.png
[api-management-]: ./media/api-management-howto-add-products/
[api-management-]: ./media/api-management-howto-add-products/


[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md
[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Next steps]: #next-steps
[How toocreate and use groups toomanage developer accounts in Azure API Management]: api-management-howto-create-groups.md
[How create and configure advanced product settings in Azure API Management]: api-management-howto-product-with-rules.md 
