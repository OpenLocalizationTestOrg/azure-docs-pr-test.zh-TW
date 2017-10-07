---
title: "aaaAzure API 管理的概觀和索引鍵概念 |Microsoft 文件"
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
ms.openlocfilehash: a77b24b4632d868afa15bd6cf88060982046cb38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-api-management"></a><span data-ttu-id="034ee-103">什麼是 API 管理？</span><span class="sxs-lookup"><span data-stu-id="034ee-103">What is API Management?</span></span>
<span data-ttu-id="034ee-104">API 管理可協助組織發行應用程式開發介面 tooexternal、 合作夥伴和內部開發人員 toounlock hello 可能會其資料和服務。</span><span class="sxs-lookup"><span data-stu-id="034ee-104">API Management helps organizations publish APIs tooexternal, partner and internal developers toounlock hello potential of their data and services.</span></span> <span data-ttu-id="034ee-105">企業 everywhere 會尋找 tooextend 其作業由數位平台、 建立新通路、 尋找新客戶和深化與現有的。</span><span class="sxs-lookup"><span data-stu-id="034ee-105">Businesses everywhere are looking tooextend their operations as a digital platform, creating new channels, finding new customers and driving deeper engagement with existing ones.</span></span> <span data-ttu-id="034ee-106">API 管理提供 hello 核心能力 tooensure 成功的 API 程式，透過開發人員的努力、 企業洞察力、 分析、 安全性和保護。</span><span class="sxs-lookup"><span data-stu-id="034ee-106">API Management provides hello core competencies tooensure a successful API program through developer engagement, business insights, analytics, security and protection.</span></span>

<span data-ttu-id="034ee-107">監看 hello 下列影片以取得 Azure API 管理的概觀，以及了解如何 toouse API 管理 tooadd 許多功能 tooyour 應用程式開發介面，包括存取控制限制、 監視、 事件記錄和評分快取回應，與您的組件上的最少工作。</span><span class="sxs-lookup"><span data-stu-id="034ee-107">Watch hello following video for an overview of Azure API Management and learn how toouse API Management tooadd many features tooyour API, including access control, rate limiting, monitoring, event logging, and response caching, with minimal work on your part.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-API-Management-Overview/player]
> 
> 

<span data-ttu-id="034ee-108">toouse API 管理，系統管理員建立應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="034ee-108">toouse API Management, administrators create APIs.</span></span> <span data-ttu-id="034ee-109">每個應用程式開發介面包含一或多個作業，並可以新增每個 API，tooone 或多個產品。</span><span class="sxs-lookup"><span data-stu-id="034ee-109">Each API consists of one or more operations, and each API can be added tooone or more products.</span></span> <span data-ttu-id="034ee-110">toouse 應用程式開發介面，開發人員必須訂閱 tooa 產品，其中包含應用程式開發介面，並呼叫作用中的主體 tooany 使用量原則 hello API 的作業。</span><span class="sxs-lookup"><span data-stu-id="034ee-110">toouse an API, developers subscribe tooa product that contains that API, and then they can call hello API's operation, subject tooany usage policies that may be in effect.</span></span>

<span data-ttu-id="034ee-111">本主題說明 API 管理的主要概念。</span><span class="sxs-lookup"><span data-stu-id="034ee-111">This topic provides an overview of API Management key concepts.</span></span>

> [!NOTE]
> <span data-ttu-id="034ee-112">如需詳細資訊，請參閱 hello[雲端為基礎的 API 管理： 另外 hello 應用程式開發介面電源](http://j.mp/ms-apim-whitepaper)PDF （英文） 白皮書。</span><span class="sxs-lookup"><span data-stu-id="034ee-112">For more information, see hello [Cloud-based API Management: Harnessing hello Power of APIs](http://j.mp/ms-apim-whitepaper) PDF whitepaper.</span></span> <span data-ttu-id="034ee-113">這份 CITO Research 發表的簡介白皮書涵蓋：</span><span class="sxs-lookup"><span data-stu-id="034ee-113">This introductory whitepaper on API Management by CITO Research covers:</span></span> 
> 
> * <span data-ttu-id="034ee-114">常見的 API 需求與挑戰</span><span class="sxs-lookup"><span data-stu-id="034ee-114">Common API requirements and challenges</span></span>
> * <span data-ttu-id="034ee-115">解構 API 並呈現其外貌</span><span class="sxs-lookup"><span data-stu-id="034ee-115">Decoupling APIs and presenting facades</span></span>
> * <span data-ttu-id="034ee-116">讓開發人員快速上手</span><span class="sxs-lookup"><span data-stu-id="034ee-116">Getting developers up and running quickly</span></span>
> * <span data-ttu-id="034ee-117">保護存取</span><span class="sxs-lookup"><span data-stu-id="034ee-117">Securing access</span></span>
> * <span data-ttu-id="034ee-118">分析與度量</span><span class="sxs-lookup"><span data-stu-id="034ee-118">Analytics and metrics</span></span>
> * <span data-ttu-id="034ee-119">藉由 API 管理平台獲得控制權和深層資訊</span><span class="sxs-lookup"><span data-stu-id="034ee-119">Gaining control and insight with an API Management platform</span></span>
> * <span data-ttu-id="034ee-120">比較使用雲端與內部部署解決方案</span><span class="sxs-lookup"><span data-stu-id="034ee-120">Using cloud vs on-premises solutions</span></span>
> * <span data-ttu-id="034ee-121">Azure API 管理</span><span class="sxs-lookup"><span data-stu-id="034ee-121">Azure API Management</span></span>
> 
> 

## <span data-ttu-id="034ee-122"><a name="apis"> </a>API 和作業</span><span class="sxs-lookup"><span data-stu-id="034ee-122"><a name="apis"> </a>APIs and operations</span></span>
<span data-ttu-id="034ee-123">應用程式開發介面是 hello foundation API 管理服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="034ee-123">APIs are hello foundation of an API Management service instance.</span></span> <span data-ttu-id="034ee-124">每個應用程式開發介面代表一組作業可用 toodevelopers。</span><span class="sxs-lookup"><span data-stu-id="034ee-124">Each API represents  a set of operations available toodevelopers.</span></span> <span data-ttu-id="034ee-125">每個應用程式開發介面包含參考 toohello 後端服務實作 hello API 和其作業對應 toohello 作業 hello 後端服務實作。</span><span class="sxs-lookup"><span data-stu-id="034ee-125">Each API contains a reference toohello back-end service that implements hello API, and its operations map toohello operations implemented by hello back-end service.</span></span> <span data-ttu-id="034ee-126">API 管理中的作業可設定度相當高，並可控制 URL 對應、查詢和路徑參數、要求和回應內容，以及作業回應快取。</span><span class="sxs-lookup"><span data-stu-id="034ee-126">Operations in API Management are highly configurable, with control over URL mapping, query and path parameters, request and response content, and operation response caching.</span></span> <span data-ttu-id="034ee-127">速率限制、 配額和 IP 限制原則也可以在 hello 應用程式開發介面或個別作業層級實作。</span><span class="sxs-lookup"><span data-stu-id="034ee-127">Rate limit, quotas, and IP restriction policies can also be implemented at hello API or individual operation level.</span></span>

<span data-ttu-id="034ee-128">如需詳細資訊，請參閱[如何 toocreate Api] [ How toocreate APIs]和[如何 tooadd 作業 tooan API][How tooadd operations tooan API]。</span><span class="sxs-lookup"><span data-stu-id="034ee-128">For more information, see [How toocreate APIs][How toocreate APIs] and [How tooadd operations tooan API][How tooadd operations tooan API].</span></span>

## <span data-ttu-id="034ee-129"><a name="products"> </a> 產品</span><span class="sxs-lookup"><span data-stu-id="034ee-129"><a name="products"> </a> Products</span></span>
<span data-ttu-id="034ee-130">應用程式開發介面的方式呈現的 toodevelopers 的產品。</span><span class="sxs-lookup"><span data-stu-id="034ee-130">Products are how APIs are surfaced toodevelopers.</span></span> <span data-ttu-id="034ee-131">在 API 管理中的產品包含一或多個 API，並且設定了標題、說明與使用規定。</span><span class="sxs-lookup"><span data-stu-id="034ee-131">Products in API Management have one or more APIs, and are configured with a title, description, and terms of use.</span></span> <span data-ttu-id="034ee-132">產品可以是 [開放] 或 [受保護]。</span><span class="sxs-lookup"><span data-stu-id="034ee-132">Products can be **Open** or **Protected**.</span></span> <span data-ttu-id="034ee-133">受保護的產品必須是它們可以用於，開啟時的訂閱的 toobefore 不用在訂用帳戶可以使用產品。</span><span class="sxs-lookup"><span data-stu-id="034ee-133">Protected products must be subscribed toobefore they can be used, while open products can be used without a subscription.</span></span> <span data-ttu-id="034ee-134">當產品可供開發人員使用時，即可將產品發佈。</span><span class="sxs-lookup"><span data-stu-id="034ee-134">When a product is ready for use by developers it can be published.</span></span> <span data-ttu-id="034ee-135">一旦發佈，，就可以檢視 （和大小寫的受保護的產品訂閱 hello 中） 的開發人員。</span><span class="sxs-lookup"><span data-stu-id="034ee-135">Once it is published, it can be viewed (and in hello case of protected products subscribed to) by developers.</span></span> <span data-ttu-id="034ee-136">訂用帳戶核准在 hello 產品層級和可以需要系統管理員核准，或要自動核准。</span><span class="sxs-lookup"><span data-stu-id="034ee-136">Subscription approval is configured at hello product level and can either require administrator approval, or be auto-approved.</span></span>

<span data-ttu-id="034ee-137">群組是產品 toodevelopers 使用的 toomanage hello 可見性。</span><span class="sxs-lookup"><span data-stu-id="034ee-137">Groups are used toomanage hello visibility of products toodevelopers.</span></span> <span data-ttu-id="034ee-138">產品授與的可見性 toogroups 和開發人員可以檢視和訂閱 toohello 產品可見 toohello 所隸屬的群組。</span><span class="sxs-lookup"><span data-stu-id="034ee-138">Products grant visibility toogroups, and developers can view and subscribe toohello products that are visible toohello groups in which they belong.</span></span> 

<span data-ttu-id="034ee-139">如需詳細資訊，請參閱[如何 toocreate 及發佈產品][ How toocreate and publish a product]和下列視訊 hello。</span><span class="sxs-lookup"><span data-stu-id="034ee-139">For more information, see [How toocreate and publish a product][How toocreate and publish a product] and hello following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Using-Products/player]
> 
> 

## <span data-ttu-id="034ee-140"><a name="groups"> </a> 群組</span><span class="sxs-lookup"><span data-stu-id="034ee-140"><a name="groups"> </a> Groups</span></span>
<span data-ttu-id="034ee-141">群組是產品 toodevelopers 使用的 toomanage hello 可見性。</span><span class="sxs-lookup"><span data-stu-id="034ee-141">Groups are used toomanage hello visibility of products toodevelopers.</span></span> <span data-ttu-id="034ee-142">API 管理有下列不可變群組 hello。</span><span class="sxs-lookup"><span data-stu-id="034ee-142">API Management has hello following immutable system groups.</span></span>

* <span data-ttu-id="034ee-143">**管理員** - Azure 訂用帳戶管理員是此群組的成員。</span><span class="sxs-lookup"><span data-stu-id="034ee-143">**Administrators** - Azure subscription administrators are members of this group.</span></span> <span data-ttu-id="034ee-144">系統管理員管理 API 管理服務執行個體，建立 hello Api、 操作及開發人員所使用的產品。</span><span class="sxs-lookup"><span data-stu-id="034ee-144">Administrators manage API Management service instances, creating hello APIs, operations, and products that are used by developers.</span></span>
* <span data-ttu-id="034ee-145">**開發人員** - 已驗證開發人員入口網站使用者屬於此群組。</span><span class="sxs-lookup"><span data-stu-id="034ee-145">**Developers** - Authenticated developer portal users fall into this group.</span></span> <span data-ttu-id="034ee-146">開發人員會使用您的應用程式開發介面建置應用程式的 hello 客戶。</span><span class="sxs-lookup"><span data-stu-id="034ee-146">Developers are hello customers that build applications using your APIs.</span></span> <span data-ttu-id="034ee-147">開發人員會授與存取 toohello 開發人員入口網站，並建置呼叫 hello 作業的應用程式開發介面的應用程式。</span><span class="sxs-lookup"><span data-stu-id="034ee-147">Developers are granted access toohello developer portal and build applications that call hello operations of an API.</span></span>
* <span data-ttu-id="034ee-148">**來賓**-未經驗證的開發人員入口網站的使用者，例如造訪 hello 開發人員入口網站的 API 管理執行個體都會歸類到此群組的潛在客戶。</span><span class="sxs-lookup"><span data-stu-id="034ee-148">**Guests** - Unauthenticated developer portal users, such as prospective customers visiting hello developer portal of an API Management instance fall into this group.</span></span> <span data-ttu-id="034ee-149">它們可以被授與特定的唯讀存取，例如 hello 能力 tooview 應用程式開發介面，但不是呼叫它們。</span><span class="sxs-lookup"><span data-stu-id="034ee-149">They can be granted certain read-only access, such as hello ability tooview APIs but not call them.</span></span>

<span data-ttu-id="034ee-150">在加法 toothese 系統群組中，系統管理員可以建立自訂群組或[運用在相關聯的 Azure Active Directory 租用戶中的外部群組](api-management-howto-aad.md#how-to-add-an-external-azure-active-directory-group)。</span><span class="sxs-lookup"><span data-stu-id="034ee-150">In addition toothese system groups, administrators can create custom groups or [leverage external groups in associated Azure Active Directory tenants](api-management-howto-aad.md#how-to-add-an-external-azure-active-directory-group).</span></span> <span data-ttu-id="034ee-151">自訂和外部群組可一起提供開發人員的可見性的系統群組，以及存取 tooAPI 產品。</span><span class="sxs-lookup"><span data-stu-id="034ee-151">Custom and external groups can be used alongside system groups in giving developers visibility and access tooAPI products.</span></span> <span data-ttu-id="034ee-152">例如，您可以建立一個自訂群組具有特定關係的開發人員夥伴組織，並允許它們存取 toohello Api 從產品，其中包含相關的 Api。</span><span class="sxs-lookup"><span data-stu-id="034ee-152">For example, you could create one custom group for developers affiliated with a specific partner organization and allow them access toohello APIs from a product containing relevant APIs only.</span></span> <span data-ttu-id="034ee-153">使用者可以是多個群組的成員。</span><span class="sxs-lookup"><span data-stu-id="034ee-153">A user can be a member of more than one group.</span></span>

<span data-ttu-id="034ee-154">如需詳細資訊，請參閱[如何 toocreate 和使用群組][How toocreate and use groups]。</span><span class="sxs-lookup"><span data-stu-id="034ee-154">For more information, see  [How toocreate and use groups][How toocreate and use groups].</span></span>

## <span data-ttu-id="034ee-155"><a name="developers"> </a> 開發人員</span><span class="sxs-lookup"><span data-stu-id="034ee-155"><a name="developers"> </a> Developers</span></span>
<span data-ttu-id="034ee-156">開發人員代表 hello API 管理服務執行個體中的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="034ee-156">Developers represent hello user accounts in an API Management service instance.</span></span> <span data-ttu-id="034ee-157">或開發人員可以建立或受邀 toojoin 由系統管理員，他們可以註冊從 hello[開發人員入口網站][Developer portal]。</span><span class="sxs-lookup"><span data-stu-id="034ee-157">Developers can be created or invited toojoin by administrators, or they can sign up from hello [Developer portal][Developer portal].</span></span> <span data-ttu-id="034ee-158">每位開發人員一或多個群組的成員，而且可以訂閱 toohello 產品可見性 toothose 群組授與。</span><span class="sxs-lookup"><span data-stu-id="034ee-158">Each developer is a member of one or more groups, and can be subscribe toohello products that grant visibility toothose groups.</span></span>

<span data-ttu-id="034ee-159">當開發人員必須訂閱 tooa 產品則會授與 hello 產品的 hello 主要和次要金鑰。</span><span class="sxs-lookup"><span data-stu-id="034ee-159">When developers subscribe tooa product they are granted hello primary and secondary key for hello product.</span></span> <span data-ttu-id="034ee-160">建立 hello 產品的 Api 呼叫時，會使用此金鑰。</span><span class="sxs-lookup"><span data-stu-id="034ee-160">This key is used when making calls into hello product's APIs.</span></span>

<span data-ttu-id="034ee-161">如需詳細資訊，請參閱[如何 toocreate 或邀請開發人員][ How toocreate or invite developers]和[tooassociate 與開發人員的群組方式][How tooassociate groups with developers]。</span><span class="sxs-lookup"><span data-stu-id="034ee-161">For more information, see [How toocreate or invite developers][How toocreate or invite developers] and [How tooassociate groups with developers][How tooassociate groups with developers].</span></span>

## <span data-ttu-id="034ee-162"><a name="policies"> </a> 原則</span><span class="sxs-lookup"><span data-stu-id="034ee-162"><a name="policies"> </a> Policies</span></span>
<span data-ttu-id="034ee-163">原則是 hello 的透過組態 API toochange hello 行為允許 hello publisher 的 API 管理的強大功能。</span><span class="sxs-lookup"><span data-stu-id="034ee-163">Policies are a powerful capability of API Management that allow hello publisher toochange hello behavior of hello API through configuration.</span></span> <span data-ttu-id="034ee-164">原則是循序 hello 要求上執行的陳述式的集合或應用程式開發介面的回應。</span><span class="sxs-lookup"><span data-stu-id="034ee-164">Policies are a collection of statements that are executed sequentially on hello request or response of an API.</span></span> <span data-ttu-id="034ee-165">受歡迎的陳述式包含格式轉換，從 XML tooJSON 並呼叫速率限制為開發人員，從連入呼叫 toorestrict hello 數量和許多其他原則可供使用。</span><span class="sxs-lookup"><span data-stu-id="034ee-165">Popular statements include format conversion from XML tooJSON and call rate limiting toorestrict hello amount of incoming calls from a developer, and many other policies are available.</span></span>

<span data-ttu-id="034ee-166">除非另外指定 hello 原則，可以使用原則運算式做為屬性值或任何 hello API 管理原則中的文字值。</span><span class="sxs-lookup"><span data-stu-id="034ee-166">Policy expressions can be used as attribute values or text values in any of hello API Management policies, unless hello policy specifies otherwise.</span></span> <span data-ttu-id="034ee-167">某些原則，例如 hello[控制流程](https://msdn.microsoft.com/library/azure/dn894085.aspx#choose)和[設定變數](https://msdn.microsoft.com/library/azure/dn894085.aspx#set-variable)原則為基礎的原則運算式。</span><span class="sxs-lookup"><span data-stu-id="034ee-167">Some policies such as hello [Control flow](https://msdn.microsoft.com/library/azure/dn894085.aspx#choose) and [Set variable](https://msdn.microsoft.com/library/azure/dn894085.aspx#set-variable) policies are based on policy expressions.</span></span> <span data-ttu-id="034ee-168">如需詳細資訊，請參閱[進階原則](https://msdn.microsoft.com/library/azure/dn894085.aspx#AdvancedPolicies)，[原則運算式](https://msdn.microsoft.com/library/azure/dn910913.aspx)，並監看式 hello 遵循視訊。</span><span class="sxs-lookup"><span data-stu-id="034ee-168">For more information, see [Advanced policies](https://msdn.microsoft.com/library/azure/dn894085.aspx#AdvancedPolicies), [Policy expressions](https://msdn.microsoft.com/library/azure/dn910913.aspx), and watch hello following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Policy-Expressions-in-Azure-API-Management/player]
> 
> 

<span data-ttu-id="034ee-169">如需 API 管理原則的完整清單，請參閱[原則參考文件][Policy reference]。</span><span class="sxs-lookup"><span data-stu-id="034ee-169">For a complete list of API Management policies, see [Policy reference][Policy reference].</span></span> <span data-ttu-id="034ee-170">如需使用和設定原則的詳細資訊，請參閱[API 管理原則][API Management policies]。</span><span class="sxs-lookup"><span data-stu-id="034ee-170">For more information on using and configuring policies, see [API Management policies][API Management policies].</span></span> <span data-ttu-id="034ee-171">如需建立產品並加上費率限制和配額原則的教學課程，請參閱[如何建立和設定進階產品設定][How create and configure advanced product settings]。</span><span class="sxs-lookup"><span data-stu-id="034ee-171">For a tutorial on creating a product with rate limit and quota policies, see [How create and configure advanced product settings][How create and configure advanced product settings].</span></span> <span data-ttu-id="034ee-172">示範，請參閱下列視訊 hello。</span><span class="sxs-lookup"><span data-stu-id="034ee-172">For a demo, see hello following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Rate-Limits-and-Quotas/player]
> 
> 

## <span data-ttu-id="034ee-173"><a name="developer-portal"> </a> 開發人員入口網站</span><span class="sxs-lookup"><span data-stu-id="034ee-173"><a name="developer-portal"> </a> Developer portal</span></span>
<span data-ttu-id="034ee-174">開發人員可以深入了解您應用程式開發介面、 檢視和呼叫的作業，而訂閱 tooproducts hello 開發人員入口網站。</span><span class="sxs-lookup"><span data-stu-id="034ee-174">hello developer portal is where developers can learn about your APIs, view and call operations, and subscribe tooproducts.</span></span> <span data-ttu-id="034ee-175">潛在客戶可以瀏覽 hello 開發人員入口網站，檢視應用程式開發介面和作業，並註冊。</span><span class="sxs-lookup"><span data-stu-id="034ee-175">Prospective customers can visit hello developer portal, view APIs and operations, and sign up.</span></span> <span data-ttu-id="034ee-176">您的開發人員入口網站的 hello URL 位於 hello Azure 傳統入口網站，您的 API 管理服務執行個體中的 hello 儀表板。</span><span class="sxs-lookup"><span data-stu-id="034ee-176">hello URL for your developer portal is located on hello dashboard in hello Azure Classic Portal for your API Management service instance.</span></span>

<span data-ttu-id="034ee-177">您可以自訂 hello 的外觀與您的開發人員入口網站新增自訂內容、 自訂樣式，以及新增您的品牌。</span><span class="sxs-lookup"><span data-stu-id="034ee-177">You can customize hello look and feel of your developer portal by adding custom content, customizing styles, and adding your branding.</span></span>

## <a name="api-management-and-hello-api-economy"></a><span data-ttu-id="034ee-178">API 管理和 hello API 經濟</span><span class="sxs-lookup"><span data-stu-id="034ee-178">API Management and hello API economy</span></span>
<span data-ttu-id="034ee-179">toolearn 深入了解 API 管理，監看式 hello hello Microsoft Ignite 2015 會議中的下列簡報。</span><span class="sxs-lookup"><span data-stu-id="034ee-179">toolearn more about API Management, watch hello following presentation from hello Microsoft Ignite 2015 conference.</span></span>

> [!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3708/player]
> 
> 

[APIs and operations]: #apis
[Products]: #products
[Groups]: #groups
[Developers]: #developers
[Policies]: #policies
[Developer portal]: #developer-portal

[How toocreate APIs]: api-management-howto-create-apis.md
[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md
[How toocreate and use groups]: api-management-howto-create-groups.md
[How tooassociate groups with developers]: api-management-howto-create-groups.md#associate-group-developer
[How create and configure advanced product settings]: api-management-howto-product-with-rules.md
[How toocreate or invite developers]: api-management-howto-create-or-invite-developers.md
[Policy reference]: api-management-policy-reference.md
[API Management policies]: api-management-howto-policies.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance




