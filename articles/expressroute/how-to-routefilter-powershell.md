---
title: "設定 Azure ExpressRoute Microsoft 對等互連的路由篩選：PowerShell | Microsoft Docs"
description: "本文說明如何 tooconfigure 路由篩選使用 PowerShell 的 Microsoft 對等互連"
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
ms.date: 08/16/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 395bcf7d6ad43c643ff041b154f8e4b797083e7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-route-filters-for-microsoft-peering"></a><span data-ttu-id="5298c-103">針對 Microsoft 對等互連設定路由篩選</span><span class="sxs-lookup"><span data-stu-id="5298c-103">Configure route filters for Microsoft peering</span></span>

<span data-ttu-id="5298c-104">路由篩選條件是方式 tooconsume 支援的服務，透過 Microsoft 對等的子集。</span><span class="sxs-lookup"><span data-stu-id="5298c-104">Route filters are a way tooconsume a subset of supported services through Microsoft peering.</span></span> <span data-ttu-id="5298c-105">此文章說明您設定和管理 ExpressRoute 電路的路由篩選器中的步驟 hello。</span><span class="sxs-lookup"><span data-stu-id="5298c-105">hello steps in this article help you configure and manage route filters for ExpressRoute circuits.</span></span>

<span data-ttu-id="5298c-106">Dynamics 365 服務和 Office 365 服務例如 Exchange Online、 SharePoint Online 及 Skype for Business，都可存取透過 hello Microsoft 對等互連。</span><span class="sxs-lookup"><span data-stu-id="5298c-106">Dynamics 365 services, and Office 365 services such as Exchange Online, SharePoint Online, and Skype for Business, are accessible through hello Microsoft peering.</span></span> <span data-ttu-id="5298c-107">當 Microsoft 對等互連設定 ExpressRoute 循環中時，所有的前置詞相關的 toothese 服務會通告透過 hello BGP 工作階段所建立的。</span><span class="sxs-lookup"><span data-stu-id="5298c-107">When Microsoft peering is configured in an ExpressRoute circuit, all prefixes related toothese services are advertised through hello BGP sessions that are established.</span></span> <span data-ttu-id="5298c-108">BGP 社群值為附加的 tooevery 前置詞 tooidentify hello 服務提供透過 hello 前置詞。</span><span class="sxs-lookup"><span data-stu-id="5298c-108">A BGP community value is attached tooevery prefix tooidentify hello service that is offered through hello prefix.</span></span> <span data-ttu-id="5298c-109">如需 hello BGP 社群值和它們對應到 hello 服務的清單，請參閱[BGP 社群](expressroute-routing.md#bgp)。</span><span class="sxs-lookup"><span data-stu-id="5298c-109">For a list of hello BGP community values and hello services they  map to, see [BGP communities](expressroute-routing.md#bgp).</span></span>

<span data-ttu-id="5298c-110">如果您需要連線 tooall 服務時，大量的前置詞會透過 BGP 公告。</span><span class="sxs-lookup"><span data-stu-id="5298c-110">If you require connectivity tooall services, a large number of prefixes are advertised through BGP.</span></span> <span data-ttu-id="5298c-111">這會大幅增加 hello 的 hello 維護您網路中路由器的路由表的大小。</span><span class="sxs-lookup"><span data-stu-id="5298c-111">This significantly increases hello size of hello route tables maintained by routers within your network.</span></span> <span data-ttu-id="5298c-112">如果您計劃的 tooconsume 透過 Microsoft 對等提供服務的子集，您可以減少 hello 資料表大小的路由有兩種。</span><span class="sxs-lookup"><span data-stu-id="5298c-112">If you plan tooconsume only a subset of services offered through Microsoft peering, you can reduce hello size of your route tables in two ways.</span></span> <span data-ttu-id="5298c-113">您可以：</span><span class="sxs-lookup"><span data-stu-id="5298c-113">You can:</span></span>

- <span data-ttu-id="5298c-114">在 BGP 社群上套用路由篩選，以篩選不想要的前置詞。</span><span class="sxs-lookup"><span data-stu-id="5298c-114">Filter out unwanted prefixes by applying route filters on BGP communities.</span></span> <span data-ttu-id="5298c-115">這是標準網路做法，在許多網路經常使用。</span><span class="sxs-lookup"><span data-stu-id="5298c-115">This is a standard networking practice and is used commonly within many networks.</span></span>

- <span data-ttu-id="5298c-116">定義路由篩選器，並將其套用 tooyour ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="5298c-116">Define route filters and apply them tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="5298c-117">路由篩選條件是新的資源，可讓您選取的 hello 清單服務您計劃 tooconsume 透過 Microsoft 對等互連。</span><span class="sxs-lookup"><span data-stu-id="5298c-117">A route filter is a new resource that lets you select hello list of services you plan tooconsume through Microsoft peering.</span></span> <span data-ttu-id="5298c-118">ExpressRoute 路由器只會傳送 hello 隸屬 toohello 服務 hello 路由篩選器中所識別的前置詞清單。</span><span class="sxs-lookup"><span data-stu-id="5298c-118">ExpressRoute routers only send hello list of prefixes that belong toohello services identified in hello route filter.</span></span>

### <span data-ttu-id="5298c-119"><a name="about"></a>關於路由篩選</span><span class="sxs-lookup"><span data-stu-id="5298c-119"><a name="about"></a>About route filters</span></span>

<span data-ttu-id="5298c-120">當 Microsoft 對等互連設定 ExpressRoute 電路上時，hello Microsoft 邊緣路由器會建立一組 BGP 工作階段與 hello 邊緣路由器 （您或您的連線提供者）。</span><span class="sxs-lookup"><span data-stu-id="5298c-120">When Microsoft peering is configured on your ExpressRoute circuit, hello Microsoft edge routers establish a pair of BGP sessions with hello edge routers (yours or your connectivity provider's).</span></span> <span data-ttu-id="5298c-121">不為通告的 tooyour 網路的任何路由。</span><span class="sxs-lookup"><span data-stu-id="5298c-121">No routes are advertised tooyour network.</span></span> <span data-ttu-id="5298c-122">tooenable 路由通告 tooyour 網路，您必須建立關聯路由篩選器。</span><span class="sxs-lookup"><span data-stu-id="5298c-122">tooenable route advertisements tooyour network, you must associate a route filter.</span></span>

<span data-ttu-id="5298c-123">路由篩選器可讓您識別您想要透過 ExpressRoute 循環的 Microsoft 對等互連 tooconsume 的服務。</span><span class="sxs-lookup"><span data-stu-id="5298c-123">A route filter lets you identify services you want tooconsume through your ExpressRoute circuit's Microsoft peering.</span></span> <span data-ttu-id="5298c-124">它基本上是空白清單的所有 hello BGP 社群值。</span><span class="sxs-lookup"><span data-stu-id="5298c-124">It is essentially a white list of all hello BGP community values.</span></span> <span data-ttu-id="5298c-125">當路由篩選資源定義，並附加 tooan ExpressRoute 循環時，所有 toohello BGP 社群值對應的前置詞都是以通告的 tooyour 網路。</span><span class="sxs-lookup"><span data-stu-id="5298c-125">Once a route filter resource is defined and attached tooan ExpressRoute circuit, all prefixes that map toohello BGP community values are advertised tooyour network.</span></span>

<span data-ttu-id="5298c-126">toobe 無法 tooattach 和 Office 365 服務在其上的路由篩選，您必須透過 ExpressRoute 授權 tooconsume Office 365 服務。</span><span class="sxs-lookup"><span data-stu-id="5298c-126">toobe able tooattach route filters with Office 365 services on them, you must have authorization tooconsume Office 365 services through ExpressRoute.</span></span> <span data-ttu-id="5298c-127">如果您不是授權的 tooconsume Office 365 服務透過 ExpressRoute，hello 作業 tooattach 路由篩選器將會失敗。</span><span class="sxs-lookup"><span data-stu-id="5298c-127">If you are not authorized tooconsume Office 365 services through ExpressRoute, hello operation tooattach route filters fails.</span></span> <span data-ttu-id="5298c-128">如需 hello 授權程序的詳細資訊，請參閱[for Office 365 的 Azure ExpressRoute](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd)。</span><span class="sxs-lookup"><span data-stu-id="5298c-128">For more information about hello authorization process, see [Azure ExpressRoute for Office 365](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd).</span></span> <span data-ttu-id="5298c-129">連線 tooDynamics 365 服務不需要任何先前的授權。</span><span class="sxs-lookup"><span data-stu-id="5298c-129">Connectivity tooDynamics 365 services does NOT require any prior authorization.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5298c-130">Microsoft 對等互連的 ExpressRoute 電路已設定先前 tooAugust 1，2017年必須透過 Microsoft 對等互連，公告的所有服務首碼，即使未定義路由篩選器。</span><span class="sxs-lookup"><span data-stu-id="5298c-130">Microsoft peering of ExpressRoute circuits that were configured prior tooAugust 1, 2017 will have all service prefixes advertised through Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="5298c-131">Microsoft 對等互連的當天或之後 2017 年 8 月 1，已設定的 ExpressRoute 電路並不會有任何前置詞通告的路由篩選器連接直到 toohello 循環。</span><span class="sxs-lookup"><span data-stu-id="5298c-131">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached toohello circuit.</span></span>
> 
> 

### <span data-ttu-id="5298c-132"><a name="workflow"></a>工作流程</span><span class="sxs-lookup"><span data-stu-id="5298c-132"><a name="workflow"></a>Workflow</span></span>

<span data-ttu-id="5298c-133">toobe 無法 toosuccessfully 連接 tooservices 透過 Microsoft 對等互連，您必須完成下列組態步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="5298c-133">toobe able toosuccessfully connect tooservices through Microsoft peering, you must complete hello following configuration steps:</span></span>

- <span data-ttu-id="5298c-134">您必須具有已佈建 Microsoft 對等互連的使用中 ExpressRoute 線路。</span><span class="sxs-lookup"><span data-stu-id="5298c-134">You must have an active ExpressRoute circuit that has Microsoft peering provisioned.</span></span> <span data-ttu-id="5298c-135">您可以使用下列指示 tooaccomplish hello 這些工作：</span><span class="sxs-lookup"><span data-stu-id="5298c-135">You can use hello following instructions tooaccomplish these tasks:</span></span>
  - <span data-ttu-id="5298c-136">[建立 ExpressRoute 電路](expressroute-howto-circuit-arm.md)和有 hello 電路啟用您的連線提供者，才能繼續。</span><span class="sxs-lookup"><span data-stu-id="5298c-136">[Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="5298c-137">hello ExpressRoute 電路必須在佈建並啟用狀態。</span><span class="sxs-lookup"><span data-stu-id="5298c-137">hello ExpressRoute circuit must be in a provisioned and enabled state.</span></span>
  - <span data-ttu-id="5298c-138">[建立 Microsoft 對等互連](expressroute-circuit-peerings.md)如果您管理直接 hello BGP 工作階段。</span><span class="sxs-lookup"><span data-stu-id="5298c-138">[Create Microsoft peering](expressroute-circuit-peerings.md) if you manage hello BGP session directly.</span></span> <span data-ttu-id="5298c-139">或者，讓您的連線提供者為您的線路佈建 Microsoft 對等互連。</span><span class="sxs-lookup"><span data-stu-id="5298c-139">Or, have your connectivity provider provision Microsoft peering for your circuit.</span></span>

-  <span data-ttu-id="5298c-140">您必須建立及設定路由篩選。</span><span class="sxs-lookup"><span data-stu-id="5298c-140">You must create and configure a route filter.</span></span>
    - <span data-ttu-id="5298c-141">找出 hello 服務 tooconsume 透過 Microsoft 對等互連</span><span class="sxs-lookup"><span data-stu-id="5298c-141">Identify hello services you with tooconsume through Microsoft peering</span></span>
    - <span data-ttu-id="5298c-142">識別 hello 與 hello 服務相關聯的 BGP 社群值的清單</span><span class="sxs-lookup"><span data-stu-id="5298c-142">Identify hello list of BGP community values associated with hello services</span></span>
    - <span data-ttu-id="5298c-143">建立規則 tooallow hello 前置詞清單相符 hello BGP 社群值</span><span class="sxs-lookup"><span data-stu-id="5298c-143">Create a rule tooallow hello prefix list matching hello BGP community values</span></span>

-  <span data-ttu-id="5298c-144">您必須將附加 hello 路由篩選 toohello ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="5298c-144">You must attach hello route filter toohello ExpressRoute circuit.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="5298c-145">開始之前</span><span class="sxs-lookup"><span data-stu-id="5298c-145">Before you begin</span></span>

<span data-ttu-id="5298c-146">開始設定之前，請確定您符合下列準則的 hello:</span><span class="sxs-lookup"><span data-stu-id="5298c-146">Before you begin configuration, make sure you meet hello following criteria:</span></span>

 - <span data-ttu-id="5298c-147">安裝 hello hello Azure 資源管理員的 PowerShell 指令程式最新版本。</span><span class="sxs-lookup"><span data-stu-id="5298c-147">Install hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="5298c-148">如需詳細資訊，請參閱[安裝和設定 Azure PowerShell](/powershell/azure/install-azurerm-ps)。</span><span class="sxs-lookup"><span data-stu-id="5298c-148">For more information, see [Install and configure Azure PowerShelll](/powershell/azure/install-azurerm-ps).</span></span>

  > [!NOTE]
  > <span data-ttu-id="5298c-149">從 hello PowerShell 資源庫，而不是使用 hello 安裝程式下載 hello 最新版本。</span><span class="sxs-lookup"><span data-stu-id="5298c-149">Download hello latest version from hello PowerShell Gallery, rather than using hello Installer.</span></span> <span data-ttu-id="5298c-150">hello 安裝程式目前不支援所需的 hello cmdlet。</span><span class="sxs-lookup"><span data-stu-id="5298c-150">hello Installer currently does not support hello required cmdlets.</span></span>
  > 

 - <span data-ttu-id="5298c-151">檢閱 hello[必要條件](expressroute-prerequisites.md)和[工作流程](expressroute-workflows.md)開始設定之前。</span><span class="sxs-lookup"><span data-stu-id="5298c-151">Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

 - <span data-ttu-id="5298c-152">您必須擁有作用中的 ExpressRoute 線路。</span><span class="sxs-lookup"><span data-stu-id="5298c-152">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="5298c-153">請依照下列指示 hello 太[建立 ExpressRoute 電路](expressroute-howto-circuit-arm.md)和有 hello 電路啟用您的連線提供者，才能繼續。</span><span class="sxs-lookup"><span data-stu-id="5298c-153">Follow hello instructions too[Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="5298c-154">hello ExpressRoute 電路必須在佈建並啟用狀態。</span><span class="sxs-lookup"><span data-stu-id="5298c-154">hello ExpressRoute circuit must be in a provisioned and enabled state.</span></span>

 - <span data-ttu-id="5298c-155">您必須擁有使用中 Microsoft 對等互連。</span><span class="sxs-lookup"><span data-stu-id="5298c-155">You must have an active Microsoft peering.</span></span> <span data-ttu-id="5298c-156">請遵循[建立和修改對等互連設定](expressroute-circuit-peerings.md)的指示</span><span class="sxs-lookup"><span data-stu-id="5298c-156">Follow instructions at [Create and modifying peering configuration](expressroute-circuit-peerings.md)</span></span>

### <a name="log-in-tooyour-azure-account"></a><span data-ttu-id="5298c-157">登入 tooyour Azure 帳戶</span><span class="sxs-lookup"><span data-stu-id="5298c-157">Log in tooyour Azure account</span></span>

<span data-ttu-id="5298c-158">開始之前這項設定，您必須登入 tooyour Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="5298c-158">Before beginning this configuration, you must log in tooyour Azure account.</span></span> <span data-ttu-id="5298c-159">hello cmdlet 會提示您輸入您的 Azure 帳戶的 hello 登入認證。</span><span class="sxs-lookup"><span data-stu-id="5298c-159">hello cmdlet prompts you for hello login credentials for your Azure account.</span></span> <span data-ttu-id="5298c-160">登入之後，它會下載您的帳戶設定，這樣就可以使用 tooAzure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="5298c-160">After logging in, it downloads your account settings so they are available tooAzure PowerShell.</span></span>

<span data-ttu-id="5298c-161">以較高的權限開啟 PowerShell 主控台並連接 tooyour 帳戶。</span><span class="sxs-lookup"><span data-stu-id="5298c-161">Open your PowerShell console with elevated privileges, and connect tooyour account.</span></span> <span data-ttu-id="5298c-162">使用下列範例 toohelp 您連接的 hello:</span><span class="sxs-lookup"><span data-stu-id="5298c-162">Use hello following example toohelp you connect:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="5298c-163">如果您有多個 Azure 訂用帳戶，請檢查 hello hello 帳戶的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="5298c-163">If you have multiple Azure subscriptions, check hello subscriptions for hello account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="5298c-164">指定您想 toouse hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="5298c-164">Specify hello subscription that you want toouse.</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
```

## <span data-ttu-id="5298c-165"><a name="prefixes"></a>步驟 1.</span><span class="sxs-lookup"><span data-stu-id="5298c-165"><a name="prefixes"></a>Step 1.</span></span> <span data-ttu-id="5298c-166">取得前置詞和 BGP 社群值的清單</span><span class="sxs-lookup"><span data-stu-id="5298c-166">Get a list of prefixes and BGP community values</span></span>

### <a name="1-get-a-list-of-bgp-community-values"></a><span data-ttu-id="5298c-167">1.取得 BGP 社群值的清單</span><span class="sxs-lookup"><span data-stu-id="5298c-167">1. Get a list of BGP community values</span></span>

<span data-ttu-id="5298c-168">使用下列 cmdlet tooget hello 清單 BGP 社群相關聯的值與可透過 Microsoft 對等互連，存取服務的 hello 和 hello 與其相關聯的前置詞的清單：</span><span class="sxs-lookup"><span data-stu-id="5298c-168">Use hello following cmdlet tooget hello list of BGP community values associated with services accessible through Microsoft peering, and hello list of prefixes associated with them:</span></span>

```powershell
Get-AzureRmBgpServiceCommunity
```
### <a name="2-make-a-list-of-hello-values-that-you-want-toouse"></a><span data-ttu-id="5298c-169">2.進行您想 toouse hello 值的清單</span><span class="sxs-lookup"><span data-stu-id="5298c-169">2. Make a list of hello values that you want toouse</span></span>

<span data-ttu-id="5298c-170">建立一份您想要的 BGP 社群值 toouse hello 路由篩選器中。</span><span class="sxs-lookup"><span data-stu-id="5298c-170">Make a list of BGP community values you want toouse in hello route filter.</span></span> <span data-ttu-id="5298c-171">例如，hello Dynamics 365 服務的 BGP 社群值會是 12076:5040。</span><span class="sxs-lookup"><span data-stu-id="5298c-171">As an example, hello BGP community value for Dynamics 365 services is 12076:5040.</span></span>

## <span data-ttu-id="5298c-172"><a name="filter"></a>步驟 2.</span><span class="sxs-lookup"><span data-stu-id="5298c-172"><a name="filter"></a>Step 2.</span></span> <span data-ttu-id="5298c-173">建立路由篩選和篩選規則</span><span class="sxs-lookup"><span data-stu-id="5298c-173">Create a route filter and a filter rule</span></span>

<span data-ttu-id="5298c-174">路由篩選條件可以有只有一個規則，並 hello 規則必須是 'Allow'，型別。</span><span class="sxs-lookup"><span data-stu-id="5298c-174">A route filter can have only one rule, and hello rule must be of type 'Allow'.</span></span> <span data-ttu-id="5298c-175">此規則可以具有與其相關聯的 BGP 社群值清單。</span><span class="sxs-lookup"><span data-stu-id="5298c-175">This rule can have a list of BGP community values associated with it.</span></span>

### <a name="1-create-a-route-filter"></a><span data-ttu-id="5298c-176">1.建立路由篩選</span><span class="sxs-lookup"><span data-stu-id="5298c-176">1. Create a route filter</span></span>

<span data-ttu-id="5298c-177">首先，建立 hello 路由篩選器。</span><span class="sxs-lookup"><span data-stu-id="5298c-177">First, create hello route filter.</span></span> <span data-ttu-id="5298c-178">hello 命令 ' 新增 AzureRmRouteFilter' 只建立路由篩選條件的資源。</span><span class="sxs-lookup"><span data-stu-id="5298c-178">hello command 'New-AzureRmRouteFilter' only creates a route filter resource.</span></span> <span data-ttu-id="5298c-179">建立 hello 資源之後，您必須建立規則，然後將它附加 toohello 路由篩選物件。</span><span class="sxs-lookup"><span data-stu-id="5298c-179">After you create hello resource, you must then create a rule and attach it toohello route filter object.</span></span> <span data-ttu-id="5298c-180">執行下列命令 toocreate hello 路由篩選資源：</span><span class="sxs-lookup"><span data-stu-id="5298c-180">Run hello following command toocreate a route filter resource:</span></span>

```powershell
New-AzureRmRouteFilter -Name "MyRouteFilter" -ResourceGroupName "MyResourceGroup" -Location "West US"
```

### <a name="2-create-a-filter-rule"></a><span data-ttu-id="5298c-181">2.建立篩選規則</span><span class="sxs-lookup"><span data-stu-id="5298c-181">2. Create a filter rule</span></span>

<span data-ttu-id="5298c-182">Hello 範例所示，您可以指定一組 BGP 社群為以逗號分隔清單。</span><span class="sxs-lookup"><span data-stu-id="5298c-182">You can specify a set of BGP communities as a comma-separated list, as shown in hello example.</span></span> <span data-ttu-id="5298c-183">執行下列命令 toocreate hello 新的規則：</span><span class="sxs-lookup"><span data-stu-id="5298c-183">Run hello following command toocreate a new rule:</span></span>
 
```powershell
$rule = New-AzureRmRouteFilterRuleConfig -Name "Allow-EXO-D365" -Access Allow -RouteFilterRuleType Community -CommunityList "12076:5010,12076:5040"
```

### <a name="3-add-hello-rule-toohello-route-filter"></a><span data-ttu-id="5298c-184">3.新增 hello 規則 toohello 路由篩選器</span><span class="sxs-lookup"><span data-stu-id="5298c-184">3. Add hello rule toohello route filter</span></span>

<span data-ttu-id="5298c-185">執行下列命令 tooadd hello 篩選器規則 toohello 路由篩選器的 hello:</span><span class="sxs-lookup"><span data-stu-id="5298c-185">Run hello following command tooadd hello filter rule toohello route filter:</span></span>
 
```powershell
$routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
$routefilter.Rules.Add($rule)
Set-AzureRmRouteFilter -RouteFilter $routefilter
```

## <span data-ttu-id="5298c-186"><a name="attach"></a>步驟 3.</span><span class="sxs-lookup"><span data-stu-id="5298c-186"><a name="attach"></a>Step 3.</span></span> <span data-ttu-id="5298c-187">附加 hello 路由篩選 tooan ExpressRoute 電路</span><span class="sxs-lookup"><span data-stu-id="5298c-187">Attach hello route filter tooan ExpressRoute circuit</span></span>

<span data-ttu-id="5298c-188">執行下列命令 tooattach hello 路由篩選 toohello ExpressRoute 循環，假設您有唯一的 Microsoft 對等的 hello:</span><span class="sxs-lookup"><span data-stu-id="5298c-188">Run hello following command tooattach hello route filter toohello ExpressRoute circuit, assuming you have only Microsoft peering:</span></span>

```powershell
$ckt.Peerings[0].RouteFilter = $routefilter 
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <span data-ttu-id="5298c-189"><a name="getproperties"></a>tooget hello 屬性的路由篩選器</span><span class="sxs-lookup"><span data-stu-id="5298c-189"><a name="getproperties"></a>tooget hello properties of a route filter</span></span>

<span data-ttu-id="5298c-190">路由篩選器，使用下列步驟的 hello tooget hello 屬性：</span><span class="sxs-lookup"><span data-stu-id="5298c-190">tooget hello properties of a route filter, use hello following steps:</span></span>

1. <span data-ttu-id="5298c-191">執行下列命令 tooget hello 路由篩選資源 hello:</span><span class="sxs-lookup"><span data-stu-id="5298c-191">Run hello following command tooget hello route filter resource:</span></span>

  ```powershell
  $routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
  ```
2. <span data-ttu-id="5298c-192">藉由執行下列命令的 hello hello 路由篩選器資源取得 hello 路由篩選規則：</span><span class="sxs-lookup"><span data-stu-id="5298c-192">Get hello route filter rules for hello route-filter resource by running hello following command:</span></span>

  ```powershell
  $routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
  $rule = $routefilter.Rules[0]
  ```

## <span data-ttu-id="5298c-193"><a name="updateproperties"></a>tooupdate hello 屬性的路由篩選器</span><span class="sxs-lookup"><span data-stu-id="5298c-193"><a name="updateproperties"></a>tooupdate hello properties of a route filter</span></span>

<span data-ttu-id="5298c-194">如果已附加 hello 路由篩選器 tooa 循環，更新 toohello BGP 社群清單會自動傳播 hello 建立 BGP 工作階段的廣告變更適當的前置詞。</span><span class="sxs-lookup"><span data-stu-id="5298c-194">If hello route filter is already attached tooa circuit, updates toohello BGP community list automatically propagates appropriate prefix advertisement changes through hello established BGP sessions.</span></span> <span data-ttu-id="5298c-195">您可以更新您的路由篩選器，使用下列命令的 hello hello BGP 社群清單：</span><span class="sxs-lookup"><span data-stu-id="5298c-195">You can update hello BGP community list of your route filter using hello following command:</span></span>

```powershell
$routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
$routefilter.rules[0].Communities = "12076:5030", "12076:5040"
Set-AzureRmRouteFilter -RouteFilter $routefilter
```

## <span data-ttu-id="5298c-196"><a name="detach"></a>toodetach ExpressRoute 電路的路由篩選條件</span><span class="sxs-lookup"><span data-stu-id="5298c-196"><a name="detach"></a>toodetach a route filter from an ExpressRoute circuit</span></span>

<span data-ttu-id="5298c-197">一旦從 hello ExpressRoute 電路卸離路由篩選器時，沒有前置詞會通告透過 hello BGP 工作階段。</span><span class="sxs-lookup"><span data-stu-id="5298c-197">Once a route filter is detached from hello ExpressRoute circuit, no prefixes are advertised through hello BGP session.</span></span> <span data-ttu-id="5298c-198">您可以卸離使用下列命令的 hello ExpressRoute 電路的路由篩選條件：</span><span class="sxs-lookup"><span data-stu-id="5298c-198">You can detach a route filter from an ExpressRoute circuit using hello following command:</span></span>
  
```powershell
$ckt.Peerings[0].RouteFilter = $null
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <span data-ttu-id="5298c-199"><a name="delete"></a>toodelete 路由篩選器</span><span class="sxs-lookup"><span data-stu-id="5298c-199"><a name="delete"></a>toodelete a route filter</span></span>

<span data-ttu-id="5298c-200">您只能刪除路由篩選器如果不是附加 tooany 循環。</span><span class="sxs-lookup"><span data-stu-id="5298c-200">You can only delete a route filter if it is not attached tooany circuit.</span></span> <span data-ttu-id="5298c-201">請確定該 hello 路由篩選條件不會附加 tooany 循環，然後再嘗試 toodelete 它。</span><span class="sxs-lookup"><span data-stu-id="5298c-201">Ensure that hello route filter is not attached tooany circuit before attempting toodelete it.</span></span> <span data-ttu-id="5298c-202">您可以刪除路由篩選條件使用 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="5298c-202">You can delete a route filter using hello following command:</span></span>

```powershell
Remove-AzureRmRouteFilter -Name "MyRouteFilter" -ResourceGroupName "MyResourceGroup"
```

## <a name="next-steps"></a><span data-ttu-id="5298c-203">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5298c-203">Next steps</span></span>

<span data-ttu-id="5298c-204">如需 ExpressRoute 的詳細資訊，請參閱 hello [ExpressRoute 常見問題集](expressroute-faqs.md)。</span><span class="sxs-lookup"><span data-stu-id="5298c-204">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
