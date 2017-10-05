---
title: "如何在 Azure API 管理中建立及發行產品"
description: "了解如何在 Azure API 管理中建立及發行產品。"
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
ms.openlocfilehash: 73bf4451ba1b71807e22440beecc73a7e8045c5e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-and-publish-a-product-in-azure-api-management"></a><span data-ttu-id="33485-103">如何在 Azure API 管理中建立及發行產品</span><span class="sxs-lookup"><span data-stu-id="33485-103">How to create and publish a product in Azure API Management</span></span>
<span data-ttu-id="33485-104">在 Azure API 管理中，產品包含一或多個 API，以及使用量配額與使用規定。</span><span class="sxs-lookup"><span data-stu-id="33485-104">In Azure API Management, a product contains one or more APIs as well as a usage quota and the terms of use.</span></span> <span data-ttu-id="33485-105">發行產品之後，開發人員便可訂閱產品，並開始使用產品的 API。</span><span class="sxs-lookup"><span data-stu-id="33485-105">Once a product is published, developers can subscribe to the product and begin to use the product's APIs.</span></span> <span data-ttu-id="33485-106">本主題提供建立產品、加入 API 和發行供開發人員使用的指引。</span><span class="sxs-lookup"><span data-stu-id="33485-106">The topic provides a guide to creating a product, adding an API, and publishing it for developers.</span></span>

## <span data-ttu-id="33485-107"><a name="create-product"> </a>建立產品</span><span class="sxs-lookup"><span data-stu-id="33485-107"><a name="create-product"> </a>Create a product</span></span>
<span data-ttu-id="33485-108">請在發行者入口網站新增和設定 API 的作業。</span><span class="sxs-lookup"><span data-stu-id="33485-108">Operations are added and configured to an API in the publisher portal.</span></span> <span data-ttu-id="33485-109">若要存取發行者入口網站，請在您「API 管理」服務的「Azure 入口網站」中按一下 [發行者入口網站]。</span><span class="sxs-lookup"><span data-stu-id="33485-109">To access the publisher portal, click **Publisher portal** in the Azure Portal for your API Management service.</span></span>

![發行者入口網站][api-management-management-console]

> <span data-ttu-id="33485-111">如果您尚未建立 API 管理服務執行個體，請參閱[開始使用 Azure API 管理][Get started with Azure API Management]教學課程中的[建立 API 管理服務執行個體][Create an API Management service instance]。</span><span class="sxs-lookup"><span data-stu-id="33485-111">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="33485-112">按一下左邊功能表中的 [產品]，以顯示 [產品] 頁面，然後按一下 [新增產品]。</span><span class="sxs-lookup"><span data-stu-id="33485-112">Click on **Products** in the menu on the left to display the **Products** page, and click **Add Product**.</span></span>

![產品][api-management-products]

![New product][api-management-add-new-product]

<span data-ttu-id="33485-115">在 [名稱] 欄位中輸入產品的描述性名稱，在 [說明] 欄位中輸入產品說明。</span><span class="sxs-lookup"><span data-stu-id="33485-115">Enter a descriptive name for the product in the **Name** field and a description of the product in the **Description** field.</span></span>

<span data-ttu-id="33485-116">API 管理中的產品可以是 [開放] 或 [受保護]。</span><span class="sxs-lookup"><span data-stu-id="33485-116">Products in API Management can be **Open** or **Protected**.</span></span> <span data-ttu-id="33485-117">受保護產品必須先擁有訂用帳戶才能使用，開放產品則可以使用而不需訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="33485-117">Protected products must be subscribed to before they can be used, while open products can be used without a subscription.</span></span> <span data-ttu-id="33485-118">若要建立需要訂用帳戶的受保護產品，請核取 [ **需要訂閱** ]。</span><span class="sxs-lookup"><span data-stu-id="33485-118">Check **Require subscription** to create a protected product that requires a subscription.</span></span> <span data-ttu-id="33485-119">這是預設設定。</span><span class="sxs-lookup"><span data-stu-id="33485-119">This is the default setting.</span></span>

<span data-ttu-id="33485-120">如果您希望管理員檢閱並接受或拒絕對此產品的訂閱嘗試，請核取 [Require subscription approval]  。</span><span class="sxs-lookup"><span data-stu-id="33485-120">Check **Require subscription approval** if you want an administrator to review and accept or reject subscription attempts to this product.</span></span> <span data-ttu-id="33485-121">如果未核取方塊，將會自動核准訂閱嘗試。</span><span class="sxs-lookup"><span data-stu-id="33485-121">If the box is unchecked, subscription attempts will be auto-approved.</span></span> <span data-ttu-id="33485-122">如需訂用帳戶的詳細資訊，請參閱[檢視產品的訂閱者][View subscribers to a product]。</span><span class="sxs-lookup"><span data-stu-id="33485-122">For more information on subscriptions, see [View subscribers to a product][View subscribers to a product].</span></span>

<span data-ttu-id="33485-123">若要允許開發人員帳戶訂閱產品多次，請核取 [ **允許多項訂閱** ] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="33485-123">To allow developer accounts to subscribe multiple times to the product, check the **Allow multiple subscriptions** check box.</span></span> <span data-ttu-id="33485-124">如果未核取此方塊，則每個開發人員帳戶只能訂閱產品一次。</span><span class="sxs-lookup"><span data-stu-id="33485-124">If this box is not checked, each developer account can subscribe only a single time to the product.</span></span>

![無限制的多項訂閱][api-management-unlimited-multiple-subscriptions]

<span data-ttu-id="33485-126">若要限制多項同時訂閱的數目，請核取 [ **將同時訂閱數目限制為** ] 核取方塊，然後輸入訂閱限制。</span><span class="sxs-lookup"><span data-stu-id="33485-126">To limit the count of multiple simultaneous subscriptions, check the **Limit number of simultaneous subscriptions to** check box and enter the subscription limit.</span></span> <span data-ttu-id="33485-127">在以下範例中，同時訂閱數已限制為每個開發人員帳戶四個。</span><span class="sxs-lookup"><span data-stu-id="33485-127">In the following example, simultaneous subscriptions are limited to four per developer account.</span></span>

![四個多項訂閱][api-management-four-multiple-subscriptions]

<span data-ttu-id="33485-129">設定好所有新產品的選項後，請按一下 [ **儲存** ] 來建立新產品。</span><span class="sxs-lookup"><span data-stu-id="33485-129">Once all new product options are configured, click **Save** to create the new product.</span></span>

![產品][api-management-products-page]

> <span data-ttu-id="33485-131">依預設不會發行新產品，且只有 [Administrators] 群組才能看見。</span><span class="sxs-lookup"><span data-stu-id="33485-131">By default new products are unpublished, and are visible only to the  **Administrators** group.</span></span>
> 
> 

<span data-ttu-id="33485-132">若要設定產品，請在 [產品]  索引標籤中按一下產品名稱。</span><span class="sxs-lookup"><span data-stu-id="33485-132">To configure a product, click on the product name in the **Products** tab.</span></span>

## <span data-ttu-id="33485-133"><a name="add-apis"> </a>將 API 加入至產品</span><span class="sxs-lookup"><span data-stu-id="33485-133"><a name="add-apis"> </a>Add APIs to a product</span></span>
<span data-ttu-id="33485-134">[產品] 頁面包含組態的四個連結：**摘要**、**設定**、**可見度**和**訂閱者**。</span><span class="sxs-lookup"><span data-stu-id="33485-134">The **Products** page contains four links for configuration: **Summary**, **Settings**, **Visibility**, and **Subscribers**.</span></span> <span data-ttu-id="33485-135">[ **摘要** ] 索引標籤可讓您加入 API，以及發行或取消發行產品。</span><span class="sxs-lookup"><span data-stu-id="33485-135">The **Summary** tab is where you can add APIs and publish or unpublish a product.</span></span>

![摘要][api-management-new-product-summary]

<span data-ttu-id="33485-137">發行產品之前，您必須加入一或多個 API。</span><span class="sxs-lookup"><span data-stu-id="33485-137">Before publishing your product you need to add one or more APIs.</span></span> <span data-ttu-id="33485-138">若要這樣做，請安一下 [加入 API 至產品] 。</span><span class="sxs-lookup"><span data-stu-id="33485-138">To do this, click **Add API to product**.</span></span>

![Add APIs][api-management-add-apis-to-product]

<span data-ttu-id="33485-140">選取想要的 API，按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="33485-140">Select the desired APIs and click **Save**.</span></span>

## <span data-ttu-id="33485-141"><a name="add-description"> </a>將描述性資訊加入至產品</span><span class="sxs-lookup"><span data-stu-id="33485-141"><a name="add-description"> </a>Add descriptive information to a product</span></span>
<span data-ttu-id="33485-142">[ **設定** ] 索引標籤可讓您提供產品的詳細資訊，例如用途、它提供存取的 API 及其他有用的資訊。</span><span class="sxs-lookup"><span data-stu-id="33485-142">The **Settings** tab allows you to provide detailed information about the product such as its purpose, the APIs it provides access to, and other useful information.</span></span> <span data-ttu-id="33485-143">內容以將會呼叫 API 的開發人員為對象，可使用純文字或 HTML 標記來撰寫。</span><span class="sxs-lookup"><span data-stu-id="33485-143">The content is targeted at the developers that will be calling the API and can be written in plain text or HTML markup.</span></span>

![Product settings][api-management-product-settings]

<span data-ttu-id="33485-145">若要建立需要使用訂用帳戶的受保護產品，請核取 [ **需要訂閱** ]，或是清除核取方塊，以建立不需訂用帳戶即可呼叫的開放產品。</span><span class="sxs-lookup"><span data-stu-id="33485-145">Check **Require subscription** to create a protected product that requires a subscription to be used, or clear the checkbox to create an open product that can be called without a subscription.</span></span>

<span data-ttu-id="33485-146">如果您要手動核准所有產品訂閱要求，請選取 [ **需要訂閱** ]。</span><span class="sxs-lookup"><span data-stu-id="33485-146">Select **Require subscription approval** if you want to manually approve all product subscription requests.</span></span> <span data-ttu-id="33485-147">依預設會自動同意所有產品訂閱。</span><span class="sxs-lookup"><span data-stu-id="33485-147">By default all product subscriptions are granted automatically.</span></span>

<span data-ttu-id="33485-148">若要允許開發人員帳戶訂閱產品多次，請核取 [ **允許多項訂閱** ] 核取方塊，並選擇是否指定限制。</span><span class="sxs-lookup"><span data-stu-id="33485-148">To allow developer accounts to subscribe multiple times to the product, check the **Allow multiple subscriptions** check box and optionally specify a limit.</span></span> <span data-ttu-id="33485-149">如果未核取此方塊，則每個開發人員帳戶只能訂閱產品一次。</span><span class="sxs-lookup"><span data-stu-id="33485-149">If this box is not checked, each developer account can subscribe only a single time to the product.</span></span>

<span data-ttu-id="33485-150">選擇性填寫 [ **使用規定** ] 欄位，描述訂閱者必須接受才可使用產品的產品使用規定。</span><span class="sxs-lookup"><span data-stu-id="33485-150">Optionally fill in the **Terms of use** field describing the terms of use for the product which subscribers must accept in order to use the product.</span></span>

## <span data-ttu-id="33485-151"><a name="publish-product"> </a>發行產品</span><span class="sxs-lookup"><span data-stu-id="33485-151"><a name="publish-product"> </a>Publish a product</span></span>
<span data-ttu-id="33485-152">產品必須發行，才能呼叫產品中的 API。</span><span class="sxs-lookup"><span data-stu-id="33485-152">Before the APIs in a product can be called, the product must be published.</span></span> <span data-ttu-id="33485-153">在產品的 [摘要] 索引標籤上，按一下 [發佈]，然後按一下 [是，發佈] 表示確認。</span><span class="sxs-lookup"><span data-stu-id="33485-153">On the **Summary** tab for the product, click **Publish**, and then click **Yes, publish it** to confirm.</span></span> <span data-ttu-id="33485-154">若要將先前發行的產品設為私人，請按一下 [取消發行] 。</span><span class="sxs-lookup"><span data-stu-id="33485-154">To make a previously published product private, click **Unpublish**.</span></span>

![Publish product][api-management-publish-product]

## <span data-ttu-id="33485-156"><a name="make-visible"> </a>讓開發人員看見產品</span><span class="sxs-lookup"><span data-stu-id="33485-156"><a name="make-visible"> </a>Make a product visible to developers</span></span>
<span data-ttu-id="33485-157">[ **可見度** ] 索引標籤可讓選擇哪些角色可在開發人員入口網站上看見產品及訂閱產品。</span><span class="sxs-lookup"><span data-stu-id="33485-157">The **Visibility** tab allows you to choose which roles are able to see the product on the developer portal and subscribe to the product.</span></span>

![Product visibility][api-management-product-visiblity]

<span data-ttu-id="33485-159">若要允許或不允許群組中的開發人員看見產品，請核取或取消核取群組旁邊的核取方塊，然後按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="33485-159">To enable or disable visibility of a product for the developers in a group, check or uncheck the check box beside the group and then click **Save**.</span></span>

> <span data-ttu-id="33485-160">如需詳細資訊，請參閱 [如何在 Azure API 管理中建立和使用群組來管理開發人員帳戶][How to create and use groups to manage developer accounts in Azure API Management]。</span><span class="sxs-lookup"><span data-stu-id="33485-160">For more information, see [How to create and use groups to manage developer accounts in Azure API Management][How to create and use groups to manage developer accounts in Azure API Management].</span></span>
> 
> 

## <span data-ttu-id="33485-161"><a name="view-subscribers"> </a>檢視產品的訂閱者</span><span class="sxs-lookup"><span data-stu-id="33485-161"><a name="view-subscribers"> </a>View subscribers to a product</span></span>
<span data-ttu-id="33485-162">[ **訂閱者** ] 索引標籤會列出已訂閱產品的開發人員。</span><span class="sxs-lookup"><span data-stu-id="33485-162">The **Subscribers** tab lists the developers who have subscribed to the product.</span></span> <span data-ttu-id="33485-163">按一下開發人員的名稱，即可檢視開發人員的詳細資料和設定。</span><span class="sxs-lookup"><span data-stu-id="33485-163">The details and settings for each developer can be viewed by clicking on the developer's name.</span></span> <span data-ttu-id="33485-164">在此範例中，還沒有開發人員訂閱產品。</span><span class="sxs-lookup"><span data-stu-id="33485-164">In this example no developers have yet subscribed to the product.</span></span>

![開發人員][api-management-developer-list]

## <span data-ttu-id="33485-166"><a name="next-steps"> </a>後續步驟</span><span class="sxs-lookup"><span data-stu-id="33485-166"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="33485-167">加入想要的 API 並發行產品之後，開發人員就可以訂閱產品並開始呼叫 API。</span><span class="sxs-lookup"><span data-stu-id="33485-167">Once the desired APIs are added and the product published, developers can subscribe to the product and begin to call the APIs.</span></span> <span data-ttu-id="33485-168">如需有關這些項目和進階產品組態的示範教學課程，請參閱 [如何在 Azure API 管理中建立和設定進階產品設定][How create and configure advanced product settings in Azure API Management]。</span><span class="sxs-lookup"><span data-stu-id="33485-168">For a tutorial that demonstrates these items as well as advanced product configuration see [How create and configure advanced product settings in Azure API Management][How create and configure advanced product settings in Azure API Management].</span></span>

<span data-ttu-id="33485-169">如需關於使用產品的詳細資訊，請觀看以下影片。</span><span class="sxs-lookup"><span data-stu-id="33485-169">For more information about working with products, see the following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Using-Products/player]
> 
> 

[Create a product]: #create-product
[Add APIs to a product]: #add-apis
[Add descriptive information to a product]: #add-description
[Publish a product]: #publish-product
[Make a product visible to developers]: #make-visible
[View subscribers to a product]: #view-subscribers
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


[How to add operations to an API]: api-management-howto-add-operations.md
[How to create and publish a product]: api-management-howto-add-products.md
[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Next steps]: #next-steps
[How to create and use groups to manage developer accounts in Azure API Management]: api-management-howto-create-groups.md
[How create and configure advanced product settings in Azure API Management]: api-management-howto-product-with-rules.md 
