---
title: "Azure API 管理概觀和索引鍵概念 | Microsoft Docs"
description: "了解 API、產品、角色、群組及其他 API 管理的主要概念。"
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: e71da405-835a-48f3-956f-45c1a85698d7
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 47358c6c209488d7a12e8afbf7a2d9b3f872f0de
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="what-is-api-management"></a><span data-ttu-id="e81cc-103">什麼是 API 管理？</span><span class="sxs-lookup"><span data-stu-id="e81cc-103">What is API Management?</span></span>
<span data-ttu-id="e81cc-104">「API 管理」可協助組織將 API 發佈給外部、合作夥伴及內部開發人員，以發揮其資料與服務的潛力。</span><span class="sxs-lookup"><span data-stu-id="e81cc-104">API Management helps organizations publish APIs to external, partner and internal developers to unlock the potential of their data and services.</span></span> <span data-ttu-id="e81cc-105">各地的公司都想要將其作業延伸為數位平台、建立新的管道、尋找新客戶並對現有客戶促進更深入的參與。</span><span class="sxs-lookup"><span data-stu-id="e81cc-105">Businesses everywhere are looking to extend their operations as a digital platform, creating new channels, finding new customers and driving deeper engagement with existing ones.</span></span> <span data-ttu-id="e81cc-106">「API 管理」提供的核心專長認證，透過開發人員參與、商務洞察力、分析、安全性和保護，可確保 API 程式獲致成功。</span><span class="sxs-lookup"><span data-stu-id="e81cc-106">API Management provides the core competencies to ensure a successful API program through developer engagement, business insights, analytics, security and protection.</span></span>

<span data-ttu-id="e81cc-107">觀看下列影片以取得 Azure API 管理的概觀，並了解如何使用 API 管理，以最少量的工作將許多功能新增至您的 API，包括存取控制、速率限制、監視、事件記錄及回應快取。</span><span class="sxs-lookup"><span data-stu-id="e81cc-107">Watch the following video for an overview of Azure API Management and learn how to use API Management to add many features to your API, including access control, rate limiting, monitoring, event logging, and response caching, with minimal work on your part.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-API-Management-Overview/player]
> 
> 

<span data-ttu-id="e81cc-108">為了使用 API 管理，管理員會建立 API。</span><span class="sxs-lookup"><span data-stu-id="e81cc-108">To use API Management, administrators create APIs.</span></span> <span data-ttu-id="e81cc-109">每個 API 都包含一或多個作業，而每個 API 則可加入至一或多個產品。</span><span class="sxs-lookup"><span data-stu-id="e81cc-109">Each API consists of one or more operations, and each API can be added to one or more products.</span></span> <span data-ttu-id="e81cc-110">為了使用 API，開發人員會訂閱包含該 API 的產品，而且他們之後可呼叫 API 的作業，但需受限於可能生效的任何使用原則。</span><span class="sxs-lookup"><span data-stu-id="e81cc-110">To use an API, developers subscribe to a product that contains that API, and then they can call the API's operation, subject to any usage policies that may be in effect.</span></span>

<span data-ttu-id="e81cc-111">本主題說明 API 管理的主要概念。</span><span class="sxs-lookup"><span data-stu-id="e81cc-111">This topic provides an overview of API Management key concepts.</span></span>

> [!NOTE]
> <span data-ttu-id="e81cc-112">如需詳細資訊，請參閱 [雲端式 API 管理：如何運用 API 的威力](http://j.mp/ms-apim-whitepaper) PDF 白皮書 (英文)。</span><span class="sxs-lookup"><span data-stu-id="e81cc-112">For more information, see the [Cloud-based API Management: Harnessing the Power of APIs](http://j.mp/ms-apim-whitepaper) PDF whitepaper.</span></span> <span data-ttu-id="e81cc-113">這份 CITO Research 發表的簡介白皮書涵蓋：</span><span class="sxs-lookup"><span data-stu-id="e81cc-113">This introductory whitepaper on API Management by CITO Research covers:</span></span> 
> 
> * <span data-ttu-id="e81cc-114">常見的 API 需求與挑戰</span><span class="sxs-lookup"><span data-stu-id="e81cc-114">Common API requirements and challenges</span></span>
> * <span data-ttu-id="e81cc-115">解構 API 並呈現其外貌</span><span class="sxs-lookup"><span data-stu-id="e81cc-115">Decoupling APIs and presenting facades</span></span>
> * <span data-ttu-id="e81cc-116">讓開發人員快速上手</span><span class="sxs-lookup"><span data-stu-id="e81cc-116">Getting developers up and running quickly</span></span>
> * <span data-ttu-id="e81cc-117">保護存取</span><span class="sxs-lookup"><span data-stu-id="e81cc-117">Securing access</span></span>
> * <span data-ttu-id="e81cc-118">分析與度量</span><span class="sxs-lookup"><span data-stu-id="e81cc-118">Analytics and metrics</span></span>
> * <span data-ttu-id="e81cc-119">藉由 API 管理平台獲得控制權和深層資訊</span><span class="sxs-lookup"><span data-stu-id="e81cc-119">Gaining control and insight with an API Management platform</span></span>
> * <span data-ttu-id="e81cc-120">比較使用雲端與內部部署解決方案</span><span class="sxs-lookup"><span data-stu-id="e81cc-120">Using cloud vs on-premises solutions</span></span>
> * <span data-ttu-id="e81cc-121">Azure API 管理</span><span class="sxs-lookup"><span data-stu-id="e81cc-121">Azure API Management</span></span>
> 
> 

## <span data-ttu-id="e81cc-122"><a name="apis"> </a>API 和作業</span><span class="sxs-lookup"><span data-stu-id="e81cc-122"><a name="apis"> </a>APIs and operations</span></span>
<span data-ttu-id="e81cc-123">API 是 API 管理服務執行個體的基礎。</span><span class="sxs-lookup"><span data-stu-id="e81cc-123">APIs are the foundation of an API Management service instance.</span></span> <span data-ttu-id="e81cc-124">每個 API 都代表可供開發人員使用的一組作業。</span><span class="sxs-lookup"><span data-stu-id="e81cc-124">Each API represents  a set of operations available to developers.</span></span> <span data-ttu-id="e81cc-125">每個 API 都包含會實作 API 之後端服務的參考，而其作業會與後端服務實作的作業相對應。</span><span class="sxs-lookup"><span data-stu-id="e81cc-125">Each API contains a reference to the back-end service that implements the API, and its operations map to the operations implemented by the back-end service.</span></span> <span data-ttu-id="e81cc-126">API 管理中的作業可設定度相當高，並可控制 URL 對應、查詢和路徑參數、要求和回應內容，以及作業回應快取。</span><span class="sxs-lookup"><span data-stu-id="e81cc-126">Operations in API Management are highly configurable, with control over URL mapping, query and path parameters, request and response content, and operation response caching.</span></span> <span data-ttu-id="e81cc-127">費率限制、配額和 IP 限制原則亦可在 API 或個別作業層級實作。</span><span class="sxs-lookup"><span data-stu-id="e81cc-127">Rate limit, quotas, and IP restriction policies can also be implemented at the API or individual operation level.</span></span>

<span data-ttu-id="e81cc-128">如需詳細資訊，請參閱[如何建立 API][How to create APIs] 和[如何將作業新增至 API][How to add operations to an API]。</span><span class="sxs-lookup"><span data-stu-id="e81cc-128">For more information, see [How to create APIs][How to create APIs] and [How to add operations to an API][How to add operations to an API].</span></span>

## <span data-ttu-id="e81cc-129"><a name="products"> </a> 產品</span><span class="sxs-lookup"><span data-stu-id="e81cc-129"><a name="products"> </a> Products</span></span>
<span data-ttu-id="e81cc-130">產品是將 API 呈現給開發人員的方式。</span><span class="sxs-lookup"><span data-stu-id="e81cc-130">Products are how APIs are surfaced to developers.</span></span> <span data-ttu-id="e81cc-131">在 API 管理中的產品包含一或多個 API，並且設定了標題、說明與使用規定。</span><span class="sxs-lookup"><span data-stu-id="e81cc-131">Products in API Management have one or more APIs, and are configured with a title, description, and terms of use.</span></span> <span data-ttu-id="e81cc-132">產品可以是 [開放] 或 [受保護]。</span><span class="sxs-lookup"><span data-stu-id="e81cc-132">Products can be **Open** or **Protected**.</span></span> <span data-ttu-id="e81cc-133">受保護產品必須先擁有訂用帳戶才能使用，開放產品則可以使用而不需訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="e81cc-133">Protected products must be subscribed to before they can be used, while open products can be used without a subscription.</span></span> <span data-ttu-id="e81cc-134">當產品可供開發人員使用時，即可將產品發佈。</span><span class="sxs-lookup"><span data-stu-id="e81cc-134">When a product is ready for use by developers it can be published.</span></span> <span data-ttu-id="e81cc-135">發佈產品之後，開發人員即可檢視產品 (以及受保護產品訂閱時)。</span><span class="sxs-lookup"><span data-stu-id="e81cc-135">Once it is published, it can be viewed (and in the case of protected products subscribed to) by developers.</span></span> <span data-ttu-id="e81cc-136">訂用帳戶核准是在產品層級設定，可能需要管理員核准，或是可自動核准。</span><span class="sxs-lookup"><span data-stu-id="e81cc-136">Subscription approval is configured at the product level and can either require administrator approval, or be auto-approved.</span></span>

<span data-ttu-id="e81cc-137">群組的作用是管理產品對於開發人員的可見度。</span><span class="sxs-lookup"><span data-stu-id="e81cc-137">Groups are used to manage the visibility of products to developers.</span></span> <span data-ttu-id="e81cc-138">產品會將可見度授與群組，而開發人員可檢視並訂閱其所屬群組可見的產品。</span><span class="sxs-lookup"><span data-stu-id="e81cc-138">Products grant visibility to groups, and developers can view and subscribe to the products that are visible to the groups in which they belong.</span></span> 

<span data-ttu-id="e81cc-139">如需詳細資訊，請參閱[如何建立和發佈產品][How to create and publish a product]及下列影片。</span><span class="sxs-lookup"><span data-stu-id="e81cc-139">For more information, see [How to create and publish a product][How to create and publish a product] and the following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Using-Products/player]
> 
> 

## <span data-ttu-id="e81cc-140"><a name="groups"> </a> 群組</span><span class="sxs-lookup"><span data-stu-id="e81cc-140"><a name="groups"> </a> Groups</span></span>
<span data-ttu-id="e81cc-141">群組的作用是管理產品對於開發人員的可見度。</span><span class="sxs-lookup"><span data-stu-id="e81cc-141">Groups are used to manage the visibility of products to developers.</span></span> <span data-ttu-id="e81cc-142">API 管理具有下列不可變的系統群組。</span><span class="sxs-lookup"><span data-stu-id="e81cc-142">API Management has the following immutable system groups.</span></span>

* <span data-ttu-id="e81cc-143">**管理員** - Azure 訂用帳戶管理員是此群組的成員。</span><span class="sxs-lookup"><span data-stu-id="e81cc-143">**Administrators** - Azure subscription administrators are members of this group.</span></span> <span data-ttu-id="e81cc-144">管理員可管理 API 管理服務執行個體、建立開發人員所使用的 API、作業和產品。</span><span class="sxs-lookup"><span data-stu-id="e81cc-144">Administrators manage API Management service instances, creating the APIs, operations, and products that are used by developers.</span></span>
* <span data-ttu-id="e81cc-145">**開發人員** - 已驗證開發人員入口網站使用者屬於此群組。</span><span class="sxs-lookup"><span data-stu-id="e81cc-145">**Developers** - Authenticated developer portal users fall into this group.</span></span> <span data-ttu-id="e81cc-146">開發人員是使用您的 API 建置應用程式的客戶。</span><span class="sxs-lookup"><span data-stu-id="e81cc-146">Developers are the customers that build applications using your APIs.</span></span> <span data-ttu-id="e81cc-147">開發人員獲授與開發人員入口網站的存取權，並建置呼叫 API 作業的應用程式。</span><span class="sxs-lookup"><span data-stu-id="e81cc-147">Developers are granted access to the developer portal and build applications that call the operations of an API.</span></span>
* <span data-ttu-id="e81cc-148">**來賓** - 未經驗證的開發人員入口網站使用者 (例如，造訪 API 管理執行個體之開發人員入口網站的潛在客戶) 屬於此群組。</span><span class="sxs-lookup"><span data-stu-id="e81cc-148">**Guests** - Unauthenticated developer portal users, such as prospective customers visiting the developer portal of an API Management instance fall into this group.</span></span> <span data-ttu-id="e81cc-149">他們可獲得特定唯讀存取權限，例如他們可檢視 API 但無法進行呼叫。</span><span class="sxs-lookup"><span data-stu-id="e81cc-149">They can be granted certain read-only access, such as the ability to view APIs but not call them.</span></span>

<span data-ttu-id="e81cc-150">除了這些系統群組以外，管理員還可以建立自訂群組，或使用 [使用 Azure Active Directory 相關租用戶中的外部群組](api-management-howto-aad.md#how-to-add-an-external-azure-active-directory-group)。</span><span class="sxs-lookup"><span data-stu-id="e81cc-150">In addition to these system groups, administrators can create custom groups or [leverage external groups in associated Azure Active Directory tenants](api-management-howto-aad.md#how-to-add-an-external-azure-active-directory-group).</span></span> <span data-ttu-id="e81cc-151">自訂群組和外部群組可以與系統群組一起使用，提供開發人員 API 產品的能見度及存取權。</span><span class="sxs-lookup"><span data-stu-id="e81cc-151">Custom and external groups can be used alongside system groups in giving developers visibility and access to API products.</span></span> <span data-ttu-id="e81cc-152">例如，您可以為與特定夥伴組織有關的開發人員建立一個自訂群組，並只允許他們存取來自含相關 API 之產品的 API。</span><span class="sxs-lookup"><span data-stu-id="e81cc-152">For example, you could create one custom group for developers affiliated with a specific partner organization and allow them access to the APIs from a product containing relevant APIs only.</span></span> <span data-ttu-id="e81cc-153">使用者可以是多個群組的成員。</span><span class="sxs-lookup"><span data-stu-id="e81cc-153">A user can be a member of more than one group.</span></span>

<span data-ttu-id="e81cc-154">如需詳細資訊，請參閱[如何建立和使用群組][How to create and use groups]。</span><span class="sxs-lookup"><span data-stu-id="e81cc-154">For more information, see  [How to create and use groups][How to create and use groups].</span></span>

## <span data-ttu-id="e81cc-155"><a name="developers"> </a> 開發人員</span><span class="sxs-lookup"><span data-stu-id="e81cc-155"><a name="developers"> </a> Developers</span></span>
<span data-ttu-id="e81cc-156">開發人員代表 API 管理服務執行個體中的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="e81cc-156">Developers represent the user accounts in an API Management service instance.</span></span> <span data-ttu-id="e81cc-157">開發人員可由管理員建立或邀請加入，也可以透過[開發人員入口網站][Developer portal]註冊。</span><span class="sxs-lookup"><span data-stu-id="e81cc-157">Developers can be created or invited to join by administrators, or they can sign up from the [Developer portal][Developer portal].</span></span> <span data-ttu-id="e81cc-158">每個開發人員都是一或多個群組的成員，而且可訂閱對那些群組授與可見度的產品。</span><span class="sxs-lookup"><span data-stu-id="e81cc-158">Each developer is a member of one or more groups, and can be subscribe to the products that grant visibility to those groups.</span></span>

<span data-ttu-id="e81cc-159">當開發人員訂閱產品時，將可獲得產品的主要和次要金鑰。</span><span class="sxs-lookup"><span data-stu-id="e81cc-159">When developers subscribe to a product they are granted the primary and secondary key for the product.</span></span> <span data-ttu-id="e81cc-160">在對產品的 API 進行呼叫時會使用該金鑰。</span><span class="sxs-lookup"><span data-stu-id="e81cc-160">This key is used when making calls into the product's APIs.</span></span>

<span data-ttu-id="e81cc-161">如需詳細資訊，請參閱[如何建立或邀請開發人員][How to create or invite developers]和[如何將群組與開發人員建立關聯][How to associate groups with developers]。</span><span class="sxs-lookup"><span data-stu-id="e81cc-161">For more information, see [How to create or invite developers][How to create or invite developers] and [How to associate groups with developers][How to associate groups with developers].</span></span>

## <span data-ttu-id="e81cc-162"><a name="policies"> </a> 原則</span><span class="sxs-lookup"><span data-stu-id="e81cc-162"><a name="policies"> </a> Policies</span></span>
<span data-ttu-id="e81cc-163">原則是 API 管理的強大功能，可讓發行者透過組態變更 API 的行為。</span><span class="sxs-lookup"><span data-stu-id="e81cc-163">Policies are a powerful capability of API Management that allow the publisher to change the behavior of the API through configuration.</span></span> <span data-ttu-id="e81cc-164">原則是陳述式的集合，會因 API 的要求或回應循序執行。</span><span class="sxs-lookup"><span data-stu-id="e81cc-164">Policies are a collection of statements that are executed sequentially on the request or response of an API.</span></span> <span data-ttu-id="e81cc-165">常見陳述式包括從 XML 對 JSON 的格式轉換，以及可限制來自開發人員的傳入呼叫數量的呼叫費率限制，而且還有許多原則可供使用。</span><span class="sxs-lookup"><span data-stu-id="e81cc-165">Popular statements include format conversion from XML to JSON and call rate limiting to restrict the amount of incoming calls from a developer, and many other policies are available.</span></span>

<span data-ttu-id="e81cc-166">如果原則不另行指定，則可以在任何 API 管理原則中，使用原則運算式做為屬性值或文字值。</span><span class="sxs-lookup"><span data-stu-id="e81cc-166">Policy expressions can be used as attribute values or text values in any of the API Management policies, unless the policy specifies otherwise.</span></span> <span data-ttu-id="e81cc-167">某些原則是以原則運算式為基礎，例如[控制流程](https://msdn.microsoft.com/library/azure/dn894085.aspx#choose)和[設定變數](https://msdn.microsoft.com/library/azure/dn894085.aspx#set-variable)原則。</span><span class="sxs-lookup"><span data-stu-id="e81cc-167">Some policies such as the [Control flow](https://msdn.microsoft.com/library/azure/dn894085.aspx#choose) and [Set variable](https://msdn.microsoft.com/library/azure/dn894085.aspx#set-variable) policies are based on policy expressions.</span></span> <span data-ttu-id="e81cc-168">如需詳細資訊，請參閱[進階原則](https://msdn.microsoft.com/library/azure/dn894085.aspx#AdvancedPolicies)和[原則運算式](https://msdn.microsoft.com/library/azure/dn910913.aspx)，並觀看以下影片。</span><span class="sxs-lookup"><span data-stu-id="e81cc-168">For more information, see [Advanced policies](https://msdn.microsoft.com/library/azure/dn894085.aspx#AdvancedPolicies), [Policy expressions](https://msdn.microsoft.com/library/azure/dn910913.aspx), and watch the following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Policy-Expressions-in-Azure-API-Management/player]
> 
> 

<span data-ttu-id="e81cc-169">如需 API 管理原則的完整清單，請參閱[原則參考文件][Policy reference]。</span><span class="sxs-lookup"><span data-stu-id="e81cc-169">For a complete list of API Management policies, see [Policy reference][Policy reference].</span></span> <span data-ttu-id="e81cc-170">如需使用和設定原則的詳細資訊，請參閱[API 管理原則][API Management policies]。</span><span class="sxs-lookup"><span data-stu-id="e81cc-170">For more information on using and configuring policies, see [API Management policies][API Management policies].</span></span> <span data-ttu-id="e81cc-171">如需建立產品並加上費率限制和配額原則的教學課程，請參閱[如何建立和設定進階產品設定][How create and configure advanced product settings]。</span><span class="sxs-lookup"><span data-stu-id="e81cc-171">For a tutorial on creating a product with rate limit and quota policies, see [How create and configure advanced product settings][How create and configure advanced product settings].</span></span> <span data-ttu-id="e81cc-172">如需示範，請參閱下列影片。</span><span class="sxs-lookup"><span data-stu-id="e81cc-172">For a demo, see the following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Rate-Limits-and-Quotas/player]
> 
> 

## <span data-ttu-id="e81cc-173"><a name="developer-portal"> </a> 開發人員入口網站</span><span class="sxs-lookup"><span data-stu-id="e81cc-173"><a name="developer-portal"> </a> Developer portal</span></span>
<span data-ttu-id="e81cc-174">開發人員入口網站是開發人員可了解您的 API、檢視和呼叫作業，以及訂閱產品的地方。</span><span class="sxs-lookup"><span data-stu-id="e81cc-174">The developer portal is where developers can learn about your APIs, view and call operations, and subscribe to products.</span></span> <span data-ttu-id="e81cc-175">潛在客戶可以造訪開發人員入口網站、檢視 API 和作業，以及註冊。</span><span class="sxs-lookup"><span data-stu-id="e81cc-175">Prospective customers can visit the developer portal, view APIs and operations, and sign up.</span></span> <span data-ttu-id="e81cc-176">開發人員入口網站的 URL 位於 Azure 傳統入口網站中 API 管理服務執行個體的儀表板上。</span><span class="sxs-lookup"><span data-stu-id="e81cc-176">The URL for your developer portal is located on the dashboard in the Azure Classic Portal for your API Management service instance.</span></span>

<span data-ttu-id="e81cc-177">透過加入自訂內容、自訂樣式和加入自己的品牌，即可自訂開發人員入口網站的外觀及操作。</span><span class="sxs-lookup"><span data-stu-id="e81cc-177">You can customize the look and feel of your developer portal by adding custom content, customizing styles, and adding your branding.</span></span>

## <a name="api-management-and-the-api-economy"></a><span data-ttu-id="e81cc-178">API 管理和 API 經濟效益</span><span class="sxs-lookup"><span data-stu-id="e81cc-178">API Management and the API economy</span></span>
<span data-ttu-id="e81cc-179">若要深入了解 API 管理，請觀看 Microsoft Ignite 2015 會議的以下簡報。</span><span class="sxs-lookup"><span data-stu-id="e81cc-179">To learn more about API Management, watch the following presentation from the Microsoft Ignite 2015 conference.</span></span>

> [!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3708/player]
> 
> 

[APIs and operations]: #apis
[Products]: #products
[Groups]: #groups
[Developers]: #developers
[Policies]: #policies
[Developer portal]: #developer-portal

[How to create APIs]: api-management-howto-create-apis.md
[How to add operations to an API]: api-management-howto-add-operations.md
[How to create and publish a product]: api-management-howto-add-products.md
[How to create and use groups]: api-management-howto-create-groups.md
[How to associate groups with developers]: api-management-howto-create-groups.md#associate-group-developer
[How create and configure advanced product settings]: api-management-howto-product-with-rules.md
[How to create or invite developers]: api-management-howto-create-or-invite-developers.md
[Policy reference]: api-management-policy-reference.md
[API Management policies]: api-management-howto-policies.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance




