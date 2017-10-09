---
title: "設定 Azure ExpressRoute Microsoft 對等互連的路由篩選：入口網站 | Microsoft Docs"
description: "本文說明如何使用 Microsoft 對等互連 tooconfigure 路由篩選 hello Azure 入口網站"
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/25/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 2a47d465ec5f175d9510cef94606f70f036f0862
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-route-filters-for-microsoft-peering"></a><span data-ttu-id="20203-103">針對 Microsoft 對等互連設定路由篩選</span><span class="sxs-lookup"><span data-stu-id="20203-103">Configure route filters for Microsoft peering</span></span>

<span data-ttu-id="20203-104">路由篩選條件是方式 tooconsume 支援的服務，透過 Microsoft 對等的子集。</span><span class="sxs-lookup"><span data-stu-id="20203-104">Route filters are a way tooconsume a subset of supported services through Microsoft peering.</span></span> <span data-ttu-id="20203-105">此文章說明您設定和管理 ExpressRoute 電路的路由篩選器中的步驟 hello。</span><span class="sxs-lookup"><span data-stu-id="20203-105">hello steps in this article help you configure and manage route filters for ExpressRoute circuits.</span></span>

<span data-ttu-id="20203-106">Dynamics 365 服務和 Office 365 服務例如 Exchange Online、 SharePoint Online 及 Skype for Business，都可存取透過 hello Microsoft 對等互連。</span><span class="sxs-lookup"><span data-stu-id="20203-106">Dynamics 365 services, and Office 365 services such as Exchange Online, SharePoint Online, and Skype for Business, are accessible through hello Microsoft peering.</span></span> <span data-ttu-id="20203-107">當 Microsoft 對等互連設定 ExpressRoute 循環中時，所有的前置詞相關的 toothese 服務會通告透過 hello BGP 工作階段所建立的。</span><span class="sxs-lookup"><span data-stu-id="20203-107">When Microsoft peering is configured in an ExpressRoute circuit, all prefixes related toothese services are advertised through hello BGP sessions that are established.</span></span> <span data-ttu-id="20203-108">BGP 社群值為附加的 tooevery 前置詞 tooidentify hello 服務提供透過 hello 前置詞。</span><span class="sxs-lookup"><span data-stu-id="20203-108">A BGP community value is attached tooevery prefix tooidentify hello service that is offered through hello prefix.</span></span> <span data-ttu-id="20203-109">如需 hello BGP 社群值和它們對應到 hello 服務的清單，請參閱[BGP 社群](expressroute-routing.md#bgp)。</span><span class="sxs-lookup"><span data-stu-id="20203-109">For a list of hello BGP community values and hello services they  map to, see [BGP communities](expressroute-routing.md#bgp).</span></span>

<span data-ttu-id="20203-110">如果您需要連線 tooall 服務時，大量的前置詞會透過 BGP 公告。</span><span class="sxs-lookup"><span data-stu-id="20203-110">If you require connectivity tooall services, a large number of prefixes are advertised through BGP.</span></span> <span data-ttu-id="20203-111">這會大幅增加 hello 的 hello 維護您網路中路由器的路由表的大小。</span><span class="sxs-lookup"><span data-stu-id="20203-111">This significantly increases hello size of hello route tables maintained by routers within your network.</span></span> <span data-ttu-id="20203-112">如果您計劃的 tooconsume 透過 Microsoft 對等提供服務的子集，您可以減少 hello 資料表大小的路由有兩種。</span><span class="sxs-lookup"><span data-stu-id="20203-112">If you plan tooconsume only a subset of services offered through Microsoft peering, you can reduce hello size of your route tables in two ways.</span></span> <span data-ttu-id="20203-113">您可以：</span><span class="sxs-lookup"><span data-stu-id="20203-113">You can:</span></span>

- <span data-ttu-id="20203-114">在 BGP 社群上套用路由篩選，以篩選不想要的前置詞。</span><span class="sxs-lookup"><span data-stu-id="20203-114">Filter out unwanted prefixes by applying route filters on BGP communities.</span></span> <span data-ttu-id="20203-115">這是標準網路做法，在許多網路經常使用。</span><span class="sxs-lookup"><span data-stu-id="20203-115">This is a standard networking practice and is used commonly within many networks.</span></span>

- <span data-ttu-id="20203-116">定義路由篩選器，並將其套用 tooyour ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="20203-116">Define route filters and apply them tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="20203-117">路由篩選條件是新的資源，可讓您選取的 hello 清單服務您計劃 tooconsume 透過 Microsoft 對等互連。</span><span class="sxs-lookup"><span data-stu-id="20203-117">A route filter is a new resource that lets you select hello list of services you plan tooconsume through Microsoft peering.</span></span> <span data-ttu-id="20203-118">ExpressRoute 路由器只會傳送 hello 隸屬 toohello 服務 hello 路由篩選器中所識別的前置詞清單。</span><span class="sxs-lookup"><span data-stu-id="20203-118">ExpressRoute routers only send hello list of prefixes that belong toohello services identified in hello route filter.</span></span>

### <span data-ttu-id="20203-119"><a name="about"></a>關於路由篩選</span><span class="sxs-lookup"><span data-stu-id="20203-119"><a name="about"></a>About route filters</span></span>

<span data-ttu-id="20203-120">當 Microsoft 對等互連設定 ExpressRoute 電路上時，hello Microsoft 邊緣路由器會建立一組 BGP 工作階段與 hello 邊緣路由器 （您或您的連線提供者）。</span><span class="sxs-lookup"><span data-stu-id="20203-120">When Microsoft peering is configured on your ExpressRoute circuit, hello Microsoft edge routers establish a pair of BGP sessions with hello edge routers (yours or your connectivity provider's).</span></span> <span data-ttu-id="20203-121">不為通告的 tooyour 網路的任何路由。</span><span class="sxs-lookup"><span data-stu-id="20203-121">No routes are advertised tooyour network.</span></span> <span data-ttu-id="20203-122">tooenable 路由通告 tooyour 網路，您必須建立關聯路由篩選器。</span><span class="sxs-lookup"><span data-stu-id="20203-122">tooenable route advertisements tooyour network, you must associate a route filter.</span></span>

<span data-ttu-id="20203-123">路由篩選器可讓您識別您想要透過 ExpressRoute 循環的 Microsoft 對等互連 tooconsume 的服務。</span><span class="sxs-lookup"><span data-stu-id="20203-123">A route filter lets you identify services you want tooconsume through your ExpressRoute circuit's Microsoft peering.</span></span> <span data-ttu-id="20203-124">它基本上是空白清單的所有 hello BGP 社群值。</span><span class="sxs-lookup"><span data-stu-id="20203-124">It is essentially a white list of all hello BGP community values.</span></span> <span data-ttu-id="20203-125">當路由篩選資源定義，並附加 tooan ExpressRoute 循環時，所有 toohello BGP 社群值對應的前置詞都是以通告的 tooyour 網路。</span><span class="sxs-lookup"><span data-stu-id="20203-125">Once a route filter resource is defined and attached tooan ExpressRoute circuit, all prefixes that map toohello BGP community values are advertised tooyour network.</span></span>

<span data-ttu-id="20203-126">toobe 無法 tooattach 和 Office 365 服務在其上的路由篩選，您必須透過 ExpressRoute 授權 tooconsume Office 365 服務。</span><span class="sxs-lookup"><span data-stu-id="20203-126">toobe able tooattach route filters with Office 365 services on them, you must have authorization tooconsume Office 365 services through ExpressRoute.</span></span> <span data-ttu-id="20203-127">如果您不是授權的 tooconsume Office 365 服務透過 ExpressRoute，hello 作業 tooattach 路由篩選器將會失敗。</span><span class="sxs-lookup"><span data-stu-id="20203-127">If you are not authorized tooconsume Office 365 services through ExpressRoute, hello operation tooattach route filters fails.</span></span> <span data-ttu-id="20203-128">如需 hello 授權程序的詳細資訊，請參閱[for Office 365 的 Azure ExpressRoute](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd)。</span><span class="sxs-lookup"><span data-stu-id="20203-128">For more information about hello authorization process, see [Azure ExpressRoute for Office 365](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd).</span></span> <span data-ttu-id="20203-129">連線 tooDynamics 365 服務不需要任何先前的授權。</span><span class="sxs-lookup"><span data-stu-id="20203-129">Connectivity tooDynamics 365 services does NOT require any prior authorization.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="20203-130">Microsoft 對等互連的 ExpressRoute 電路已設定先前 tooAugust 1，2017年必須透過 Microsoft 對等互連，公告的所有服務首碼，即使未定義路由篩選器。</span><span class="sxs-lookup"><span data-stu-id="20203-130">Microsoft peering of ExpressRoute circuits that were configured prior tooAugust 1, 2017 will have all service prefixes advertised through Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="20203-131">Microsoft 對等互連的當天或之後 2017 年 8 月 1，已設定的 ExpressRoute 電路並不會有任何前置詞通告的路由篩選器連接直到 toohello 循環。</span><span class="sxs-lookup"><span data-stu-id="20203-131">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached toohello circuit.</span></span>
> 
> 

### <span data-ttu-id="20203-132"><a name="workflow"></a>工作流程</span><span class="sxs-lookup"><span data-stu-id="20203-132"><a name="workflow"></a>Workflow</span></span>

<span data-ttu-id="20203-133">toobe 無法 toosuccessfully 連接 tooservices 透過 Microsoft 對等互連，您必須完成下列組態步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="20203-133">toobe able toosuccessfully connect tooservices through Microsoft peering, you must complete hello following configuration steps:</span></span>

- <span data-ttu-id="20203-134">您必須具有已佈建 Microsoft 對等互連的使用中 ExpressRoute 線路。</span><span class="sxs-lookup"><span data-stu-id="20203-134">You must have an active ExpressRoute circuit that has Microsoft peering provisioned.</span></span> <span data-ttu-id="20203-135">您可以使用下列指示 tooaccomplish hello 這些工作：</span><span class="sxs-lookup"><span data-stu-id="20203-135">You can use hello following instructions tooaccomplish these tasks:</span></span>
  - <span data-ttu-id="20203-136">[建立 ExpressRoute 電路](expressroute-howto-circuit-portal-resource-manager.md)和有 hello 電路啟用您的連線提供者，才能繼續。</span><span class="sxs-lookup"><span data-stu-id="20203-136">[Create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="20203-137">hello ExpressRoute 電路必須在佈建並啟用狀態。</span><span class="sxs-lookup"><span data-stu-id="20203-137">hello ExpressRoute circuit must be in a provisioned and enabled state.</span></span>
  - <span data-ttu-id="20203-138">[建立 Microsoft 對等互連](expressroute-howto-routing-portal-resource-manager.md)如果您管理直接 hello BGP 工作階段。</span><span class="sxs-lookup"><span data-stu-id="20203-138">[Create Microsoft peering](expressroute-howto-routing-portal-resource-manager.md) if you manage hello BGP session directly.</span></span> <span data-ttu-id="20203-139">或者，讓您的連線提供者為您的線路佈建 Microsoft 對等互連。</span><span class="sxs-lookup"><span data-stu-id="20203-139">Or, have your connectivity provider provision Microsoft peering for your circuit.</span></span>

-  <span data-ttu-id="20203-140">您必須建立及設定路由篩選。</span><span class="sxs-lookup"><span data-stu-id="20203-140">You must create and configure a route filter.</span></span>
    - <span data-ttu-id="20203-141">找出 hello 服務 tooconsume 透過 Microsoft 對等互連</span><span class="sxs-lookup"><span data-stu-id="20203-141">Identify hello services you with tooconsume through Microsoft peering</span></span>
    - <span data-ttu-id="20203-142">識別 hello 與 hello 服務相關聯的 BGP 社群值的清單</span><span class="sxs-lookup"><span data-stu-id="20203-142">Identify hello list of BGP community values associated with hello services</span></span>
    - <span data-ttu-id="20203-143">建立規則 tooallow hello 前置詞清單相符 hello BGP 社群值</span><span class="sxs-lookup"><span data-stu-id="20203-143">Create a rule tooallow hello prefix list matching hello BGP community values</span></span>

-  <span data-ttu-id="20203-144">您必須將附加 hello 路由篩選 toohello ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="20203-144">You must attach hello route filter toohello ExpressRoute circuit.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="20203-145">開始之前</span><span class="sxs-lookup"><span data-stu-id="20203-145">Before you begin</span></span>

<span data-ttu-id="20203-146">開始設定之前，請確定您符合下列準則的 hello:</span><span class="sxs-lookup"><span data-stu-id="20203-146">Before you begin configuration, make sure you meet hello following criteria:</span></span>

 - <span data-ttu-id="20203-147">檢閱 hello[必要條件](expressroute-prerequisites.md)和[工作流程](expressroute-workflows.md)開始設定之前。</span><span class="sxs-lookup"><span data-stu-id="20203-147">Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

 - <span data-ttu-id="20203-148">您必須擁有作用中的 ExpressRoute 線路。</span><span class="sxs-lookup"><span data-stu-id="20203-148">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="20203-149">請依照下列指示 hello 太[建立 ExpressRoute 電路](expressroute-howto-circuit-portal-resource-manager.md)和有 hello 電路啟用您的連線提供者，才能繼續。</span><span class="sxs-lookup"><span data-stu-id="20203-149">Follow hello instructions too[Create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="20203-150">hello ExpressRoute 電路必須在佈建並啟用狀態。</span><span class="sxs-lookup"><span data-stu-id="20203-150">hello ExpressRoute circuit must be in a provisioned and enabled state.</span></span>

 - <span data-ttu-id="20203-151">您必須擁有使用中 Microsoft 對等互連。</span><span class="sxs-lookup"><span data-stu-id="20203-151">You must have an active Microsoft peering.</span></span> <span data-ttu-id="20203-152">請遵循[建立和修改對等互連設定](expressroute-howto-routing-portal-resource-manager.md)的指示</span><span class="sxs-lookup"><span data-stu-id="20203-152">Follow instructions at [Create and modifying peering configuration](expressroute-howto-routing-portal-resource-manager.md)</span></span>


## <span data-ttu-id="20203-153"><a name="prefixes"></a>步驟 1.</span><span class="sxs-lookup"><span data-stu-id="20203-153"><a name="prefixes"></a>Step 1.</span></span> <span data-ttu-id="20203-154">取得前置詞和 BGP 社群值的清單</span><span class="sxs-lookup"><span data-stu-id="20203-154">Get a list of prefixes and BGP community values</span></span>

### <a name="1-get-a-list-of-bgp-community-values"></a><span data-ttu-id="20203-155">1.取得 BGP 社群值的清單</span><span class="sxs-lookup"><span data-stu-id="20203-155">1. Get a list of BGP community values</span></span>

<span data-ttu-id="20203-156">服務可透過 Microsoft 對等互連存取相關聯的 BGP 社群值位於 hello [ExpressRoute 路由需求](expressroute-routing.md)頁面。</span><span class="sxs-lookup"><span data-stu-id="20203-156">BGP community values associated with services accessible through Microsoft peering is available in hello [ExpressRoute routing requirements](expressroute-routing.md) page.</span></span>

### <a name="2-make-a-list-of-hello-values-that-you-want-toouse"></a><span data-ttu-id="20203-157">2.進行您想 toouse hello 值的清單</span><span class="sxs-lookup"><span data-stu-id="20203-157">2. Make a list of hello values that you want toouse</span></span>

<span data-ttu-id="20203-158">建立一份您想要的 BGP 社群值 toouse hello 路由篩選器中。</span><span class="sxs-lookup"><span data-stu-id="20203-158">Make a list of BGP community values you want toouse in hello route filter.</span></span> <span data-ttu-id="20203-159">例如，hello Dynamics 365 服務的 BGP 社群值會是 12076:5040。</span><span class="sxs-lookup"><span data-stu-id="20203-159">As an example, hello BGP community value for Dynamics 365 services is 12076:5040.</span></span>

## <span data-ttu-id="20203-160"><a name="filter"></a>步驟 2.</span><span class="sxs-lookup"><span data-stu-id="20203-160"><a name="filter"></a>Step 2.</span></span> <span data-ttu-id="20203-161">建立路由篩選和篩選規則</span><span class="sxs-lookup"><span data-stu-id="20203-161">Create a route filter and a filter rule</span></span>

<span data-ttu-id="20203-162">路由篩選條件可以有只有一個規則，並 hello 規則必須是 'Allow'，型別。</span><span class="sxs-lookup"><span data-stu-id="20203-162">A route filter can have only one rule, and hello rule must be of type 'Allow'.</span></span> <span data-ttu-id="20203-163">此規則可以具有與其相關聯的 BGP 社群值清單。</span><span class="sxs-lookup"><span data-stu-id="20203-163">This rule can have a list of BGP community values associated with it.</span></span>

### <a name="1-create-a-route-filter"></a><span data-ttu-id="20203-164">1.建立路由篩選</span><span class="sxs-lookup"><span data-stu-id="20203-164">1. Create a route filter</span></span>
<span data-ttu-id="20203-165">您可以藉由選取 hello 選項 toocreate 建立路由篩選器，新的資源。</span><span class="sxs-lookup"><span data-stu-id="20203-165">You can create a route filter by selecting hello option toocreate a new resource.</span></span> <span data-ttu-id="20203-166">按一下**新增** > **網路** > **RouteFilter**hello 下列影像所示：</span><span class="sxs-lookup"><span data-stu-id="20203-166">Click **New** > **Networking** > **RouteFilter**, as shown in hello following image:</span></span>

![建立路由篩選](.\media\how-to-routefilter-portal\CreateRouteFilter1.png)

<span data-ttu-id="20203-168">您必須在資源群組中放置 hello 路由篩選器。</span><span class="sxs-lookup"><span data-stu-id="20203-168">You must place hello route filter in a resource group.</span></span> 

![建立路由篩選](.\media\how-to-routefilter-portal\CreateRouteFilter.png)

### <a name="2-create-a-filter-rule"></a><span data-ttu-id="20203-170">2.建立篩選規則</span><span class="sxs-lookup"><span data-stu-id="20203-170">2. Create a filter rule</span></span>

<span data-ttu-id="20203-171">您可以新增和更新規則，藉由選取 hello 管理您的路由篩選條件的規則索引標籤。</span><span class="sxs-lookup"><span data-stu-id="20203-171">You can add and update rules by selecting hello manage rule tab for your route filter.</span></span>

![建立路由篩選](.\media\how-to-routefilter-portal\ManageRouteFilter.png)


<span data-ttu-id="20203-173">您可以選取的 hello 服務想 tooconnect toofrom hello 下拉式清單並儲存完成的 hello 規則。</span><span class="sxs-lookup"><span data-stu-id="20203-173">You can select hello services you want tooconnect toofrom hello drop down list and save hello rule when done.</span></span>

![建立路由篩選](.\media\how-to-routefilter-portal\AddRouteFilterRule.png)


## <span data-ttu-id="20203-175"><a name="attach"></a>步驟 3.</span><span class="sxs-lookup"><span data-stu-id="20203-175"><a name="attach"></a>Step 3.</span></span> <span data-ttu-id="20203-176">附加 hello 路由篩選 tooan ExpressRoute 電路</span><span class="sxs-lookup"><span data-stu-id="20203-176">Attach hello route filter tooan ExpressRoute circuit</span></span>

<span data-ttu-id="20203-177">您可以選取"hello 新增循環 按鈕，從 hello 下拉式清單選取 hello ExpressRoute 電路附加 hello 路由篩選 tooa 循環。</span><span class="sxs-lookup"><span data-stu-id="20203-177">You can attach hello route filter tooa circuit by selecting hello "add Circuit" button and selecting hello ExpressRoute circuit from hello drop down list.</span></span>

![建立路由篩選](.\media\how-to-routefilter-portal\AddCktToRouteFilter.png)

## <span data-ttu-id="20203-179"><a name="getproperties"></a>tooget hello 屬性的路由篩選器</span><span class="sxs-lookup"><span data-stu-id="20203-179"><a name="getproperties"></a>tooget hello properties of a route filter</span></span>

<span data-ttu-id="20203-180">當您開啟 hello 入口網站中的 hello 資源時，您可以檢視路由篩選器的屬性。</span><span class="sxs-lookup"><span data-stu-id="20203-180">You can view properties of a route filter when you open hello resource in hello portal.</span></span>

![建立路由篩選](.\media\how-to-routefilter-portal\ViewRouteFilter.png)


## <span data-ttu-id="20203-182"><a name="updateproperties"></a>tooupdate hello 屬性的路由篩選器</span><span class="sxs-lookup"><span data-stu-id="20203-182"><a name="updateproperties"></a>tooupdate hello properties of a route filter</span></span>

<span data-ttu-id="20203-183">您可以藉由選取 hello 「 管理規則 」 按鈕更新 BGP 社群值附加的 tooa 循環的 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="20203-183">You can update hello list of BGP community values attached tooa circuit by selecting hello "Manage rule" button.</span></span>


![建立路由篩選](.\media\how-to-routefilter-portal\ManageRouteFilter.png)

![建立路由篩選](.\media\how-to-routefilter-portal\AddRouteFilterRule.png) 


## <span data-ttu-id="20203-186"><a name="detach"></a>toodetach ExpressRoute 電路的路由篩選條件</span><span class="sxs-lookup"><span data-stu-id="20203-186"><a name="detach"></a>toodetach a route filter from an ExpressRoute circuit</span></span>

<span data-ttu-id="20203-187">toodetach hello 路由篩選器，從電路 hello 電路上按一下滑鼠右鍵，並按一下 「 取消 」 的關聯。</span><span class="sxs-lookup"><span data-stu-id="20203-187">toodetach a circuit from hello route filter, right click on hello circuit and click on "disassociate".</span></span>

![建立路由篩選](.\media\how-to-routefilter-portal\DetachRouteFilter.png) 


## <span data-ttu-id="20203-189"><a name="delete"></a>toodelete 路由篩選器</span><span class="sxs-lookup"><span data-stu-id="20203-189"><a name="delete"></a>toodelete a route filter</span></span>

<span data-ttu-id="20203-190">您可以選取 hello [刪除] 按鈕來刪除路由篩選器。</span><span class="sxs-lookup"><span data-stu-id="20203-190">You can delete a route filter by selecting hello delete button.</span></span> 

![建立路由篩選](.\media\how-to-routefilter-portal\DeleteRouteFilter.png) 

## <a name="next-steps"></a><span data-ttu-id="20203-192">後續步驟</span><span class="sxs-lookup"><span data-stu-id="20203-192">Next steps</span></span>

<span data-ttu-id="20203-193">如需 ExpressRoute 的詳細資訊，請參閱 hello [ExpressRoute 常見問題集](expressroute-faqs.md)。</span><span class="sxs-lookup"><span data-stu-id="20203-193">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
