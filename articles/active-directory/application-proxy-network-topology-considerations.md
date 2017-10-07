---
title: "使用 Azure Active Directory 應用程式 Proxy 時，aaaNetwork 拓撲考量 |Microsoft 文件"
description: "涵蓋使用 Azure AD 應用程式 Proxy 時的網路拓撲考量。"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/28/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 9b8cdd2196efeb92a74e44dde6511f7d3091a968
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="network-topology-considerations-when-using-azure-active-directory-application-proxy"></a><span data-ttu-id="52351-103">使用 Azure Active Directory 應用程式 Proxy 時的網路拓撲考量</span><span class="sxs-lookup"><span data-stu-id="52351-103">Network topology considerations when using Azure Active Directory Application Proxy</span></span>

<span data-ttu-id="52351-104">本文說明使用 Azure Active Directory 應用程式 Proxy 遠端發佈及存取您的應用程式時的網路拓撲考量。</span><span class="sxs-lookup"><span data-stu-id="52351-104">This article explains network topology considerations when using Azure Active Directory (Azure AD) Application Proxy for publishing and accessing your applications remotely.</span></span>

## <a name="traffic-flow"></a><span data-ttu-id="52351-105">流量</span><span class="sxs-lookup"><span data-stu-id="52351-105">Traffic flow</span></span>

<span data-ttu-id="52351-106">透過 Azure AD Application Proxy 發行應用程式時，從 hello 使用者 toohello 應用程式的流量會流經共有三個連接：</span><span class="sxs-lookup"><span data-stu-id="52351-106">When an application is published through Azure AD Application Proxy, traffic from hello users toohello applications flows through three connections:</span></span>

1. <span data-ttu-id="52351-107">hello 使用者連接在 Azure 上的 toohello Azure AD Application Proxy 服務公用端點</span><span class="sxs-lookup"><span data-stu-id="52351-107">hello user connects toohello Azure AD Application Proxy service public endpoint on Azure</span></span>
2. <span data-ttu-id="52351-108">hello 應用程式 Proxy 服務連接 toohello 應用程式 Proxy 連接器</span><span class="sxs-lookup"><span data-stu-id="52351-108">hello Application Proxy service connects toohello Application Proxy connector</span></span>
3. <span data-ttu-id="52351-109">hello 應用程式 Proxy 連接器連接 toohello 目標應用程式</span><span class="sxs-lookup"><span data-stu-id="52351-109">hello Application Proxy connector connects toohello target application</span></span>

![顯示從使用者 tootarget 應用程式的流量圖表](./media/application-proxy-network-topologies/application-proxy-three-hops.png)

## <a name="tenant-location-and-application-proxy-service"></a><span data-ttu-id="52351-111">租用戶位置與應用程式 Proxy 服務</span><span class="sxs-lookup"><span data-stu-id="52351-111">Tenant location and Application Proxy service</span></span>

<span data-ttu-id="52351-112">當您註冊 Azure AD 租用戶時，hello 區域，您的租用戶由您指定的 hello 國家/地區決定。</span><span class="sxs-lookup"><span data-stu-id="52351-112">When you sign up for an Azure AD tenant, hello region of your tenant is determined by hello country you specify.</span></span> <span data-ttu-id="52351-113">當您啟用應用程式 Proxy 時，選擇或建立 hello 中相同租用戶的 hello 應用程式 Proxy 服務執行個體與您的 Azure AD 租用戶或最接近區域 tooit hello 的區域。</span><span class="sxs-lookup"><span data-stu-id="52351-113">When you enable Application Proxy, hello Application Proxy service instances for your tenant are chosen or created in hello same region as your Azure AD tenant, or hello closest region tooit.</span></span>

<span data-ttu-id="52351-114">比方說，如果您的 Azure AD 租用戶的區域是 hello 歐盟 (EU)，所有的應用程式 Proxy 連接器會使用服務執行個體 hello EU 中的 Azure 資料中心。</span><span class="sxs-lookup"><span data-stu-id="52351-114">For example, if your Azure AD tenant’s region is hello European Union (EU), all your Application Proxy connectors use service instances in Azure datacenters in hello EU.</span></span> <span data-ttu-id="52351-115">當您的使用者存取已發行的應用程式時，其流量會經歷 hello 應用程式 Proxy 服務執行個體，在這個位置。</span><span class="sxs-lookup"><span data-stu-id="52351-115">When your users access published applications, their traffic goes through hello Application Proxy service instances in this location.</span></span>

## <a name="considerations-for-reducing-latency"></a><span data-ttu-id="52351-116">降低延遲的考量</span><span class="sxs-lookup"><span data-stu-id="52351-116">Considerations for reducing latency</span></span>

<span data-ttu-id="52351-117">所有 Proxy 解決方案都會在您的網路連線中造成延遲。</span><span class="sxs-lookup"><span data-stu-id="52351-117">All proxy solutions introduce latency into your network connection.</span></span> <span data-ttu-id="52351-118">不論哪一個 proxy 或 VPN 解決方案選擇做為遠端存取解決方案，它一律包含一組啟用 hello 連接 tooinside 您的公司網路的伺服器。</span><span class="sxs-lookup"><span data-stu-id="52351-118">No matter which proxy or VPN solution you choose as your remote access solution, it always includes a set of servers enabling hello connection tooinside your corporate network.</span></span>

<span data-ttu-id="52351-119">組織通常包含其周邊網路中的伺服器端點。</span><span class="sxs-lookup"><span data-stu-id="52351-119">Organizations typically include server endpoints in their perimeter network.</span></span> <span data-ttu-id="52351-120">使用 Azure AD Application Proxy，不過，流量流經 hello 雲端中的 hello proxy 服務時 hello 連接器位於公司網路。</span><span class="sxs-lookup"><span data-stu-id="52351-120">With Azure AD Application Proxy, however, traffic flows through hello proxy service in hello cloud while hello connectors reside on your corporate network.</span></span> <span data-ttu-id="52351-121">不需要周邊網路。</span><span class="sxs-lookup"><span data-stu-id="52351-121">No perimeter network is required.</span></span>

<span data-ttu-id="52351-122">hello 下一節包含的其他建議 toohelp 減少延遲更進一步。</span><span class="sxs-lookup"><span data-stu-id="52351-122">hello next sections contain additional suggestions toohelp you reduce latency even further.</span></span> 

### <a name="connector-placement"></a><span data-ttu-id="52351-123">連接器放置</span><span class="sxs-lookup"><span data-stu-id="52351-123">Connector placement</span></span>

<span data-ttu-id="52351-124">應用程式 Proxy 為您的租用戶位置選擇 hello 位置執行個體。</span><span class="sxs-lookup"><span data-stu-id="52351-124">Application Proxy chooses hello location of instances for you, based on your tenant location.</span></span> <span data-ttu-id="52351-125">不過，您取得 toodecide tooinstall hello 連接器，讓您在 hello 電源 toodefine hello 延遲特性的網路流量。</span><span class="sxs-lookup"><span data-stu-id="52351-125">However, you get toodecide where tooinstall hello connector, giving you hello power toodefine hello latency characteristics of your network traffic.</span></span>

<span data-ttu-id="52351-126">Hello 應用程式 Proxy 服務設定，請詢問下列問題的 hello:</span><span class="sxs-lookup"><span data-stu-id="52351-126">When setting up hello Application Proxy service, ask hello following questions:</span></span>

* <span data-ttu-id="52351-127">Hello 應用程式位於何處？</span><span class="sxs-lookup"><span data-stu-id="52351-127">Where is hello app located?</span></span>
* <span data-ttu-id="52351-128">在哪裡？ 大部分使用者都可以存取位於 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="52351-128">Where are most users who access hello app located?</span></span>
* <span data-ttu-id="52351-129">Hello 應用程式 Proxy 執行個體位於何處？</span><span class="sxs-lookup"><span data-stu-id="52351-129">Where is hello Application Proxy instance located?</span></span>
* <span data-ttu-id="52351-130">您已經有設定，例如 Azure ExpressRoute 或類似的 VPN 專用的網路連線 tooAzure 資料中心嗎？</span><span class="sxs-lookup"><span data-stu-id="52351-130">Do you already have a dedicated network connection tooAzure datacenters set up, like Azure ExpressRoute or a similar VPN?</span></span>

<span data-ttu-id="52351-131">hello 連接器 toocommunicate 使用 Azure 和您的應用程式 （步驟 2 和 3 在 hello 流量圖表），因此 hello hello 連接器會影響這些兩個連線的 hello 延遲的位置。</span><span class="sxs-lookup"><span data-stu-id="52351-131">hello connector has toocommunicate with both Azure and your applications (steps 2 and 3 in hello Traffic flow diagram), so hello placement of hello connector affects hello latency of those two connections.</span></span> <span data-ttu-id="52351-132">時評估 hello 放置 hello 連接器，請遵循點注意 hello:</span><span class="sxs-lookup"><span data-stu-id="52351-132">When evaluating hello placement of hello connector, keep in mind hello following points:</span></span>

* <span data-ttu-id="52351-133">如果您想 toouse Kerberos 限制委派 (KCD) 的單一登入，然後 hello 連接器必須的視野 tooa 資料中心。</span><span class="sxs-lookup"><span data-stu-id="52351-133">If you want toouse Kerberos constrained delegation (KCD) for single sign-on, then hello connector needs a line of sight tooa datacenter.</span></span> <span data-ttu-id="52351-134">此外，hello 連接器伺服器必須加入 toobe 網域。</span><span class="sxs-lookup"><span data-stu-id="52351-134">Additionally, hello connector server needs toobe domain joined.</span></span>  
* <span data-ttu-id="52351-135">有疑問，hello 連接器接近 toohello 應用程式的安裝。</span><span class="sxs-lookup"><span data-stu-id="52351-135">When in doubt, install hello connector closer toohello application.</span></span>

### <a name="general-approach-toominimize-latency"></a><span data-ttu-id="52351-136">一般方法 toominimize 延遲</span><span class="sxs-lookup"><span data-stu-id="52351-136">General approach toominimize latency</span></span>

<span data-ttu-id="52351-137">您可以延遲降至最低 hello hello 端對端傳輸的最佳化每個網路連線。</span><span class="sxs-lookup"><span data-stu-id="52351-137">You can minimize hello latency of hello end-to-end traffic by optimizing each network connection.</span></span> <span data-ttu-id="52351-138">可以將每個連線最佳化，方法為︰</span><span class="sxs-lookup"><span data-stu-id="52351-138">Each connection can be optimized by:</span></span>

* <span data-ttu-id="52351-139">減少 hello hello 兩端 hello 躍點的距離。</span><span class="sxs-lookup"><span data-stu-id="52351-139">Reducing hello distance between hello two ends of hello hop.</span></span>
* <span data-ttu-id="52351-140">選擇 hello 正確網路 tootraverse。</span><span class="sxs-lookup"><span data-stu-id="52351-140">Choosing hello right network tootraverse.</span></span> <span data-ttu-id="52351-141">比方說，是私人網路，而不是 hello 周遊公用網際網路可能更快，因為 toodedicated 連結。</span><span class="sxs-lookup"><span data-stu-id="52351-141">For example, traversing a private network rather than hello public Internet may be faster, due toodedicated links.</span></span>

<span data-ttu-id="52351-142">如果您有 Azure 與您的公司網路之間的 VPN 或 ExpressRoute 專用的連結時，您可能會想 toouse 的。</span><span class="sxs-lookup"><span data-stu-id="52351-142">If you have a dedicated VPN or ExpressRoute link between Azure and your corporate network, you may want toouse that.</span></span>

## <a name="focus-your-optimization-strategy"></a><span data-ttu-id="52351-143">專注於最佳化策略</span><span class="sxs-lookup"><span data-stu-id="52351-143">Focus your optimization strategy</span></span>

<span data-ttu-id="52351-144">還有一些您可以執行您的使用者與 hello 應用程式 Proxy 服務之間的 toocontrol hello 連線。</span><span class="sxs-lookup"><span data-stu-id="52351-144">There's little that you can do toocontrol hello connection between your users and hello Application Proxy service.</span></span> <span data-ttu-id="52351-145">使用者可以從家用網路、咖啡廳或不同的國家/地區存取您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="52351-145">Users may access your apps from a home network, a coffee shop, or a different country.</span></span> <span data-ttu-id="52351-146">相反地，您可以最佳化 hello 連線從 hello 應用程式 Proxy 服務 toohello 應用程式 Proxy 連接器 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="52351-146">Instead, you can optimize hello connections from hello Application Proxy service toohello Application Proxy connectors toohello apps.</span></span> <span data-ttu-id="52351-147">請考慮納入 hello 遵循您的環境中的模式。</span><span class="sxs-lookup"><span data-stu-id="52351-147">Consider incorporating hello following patterns in your environment.</span></span>

### <a name="pattern-1-put-hello-connector-close-toohello-application"></a><span data-ttu-id="52351-148">模式 1: Put hello 連接器關閉 toohello 應用程式</span><span class="sxs-lookup"><span data-stu-id="52351-148">Pattern 1: Put hello connector close toohello application</span></span>

<span data-ttu-id="52351-149">位置 hello 連接器關閉 toohello 目標應用程式在 hello 客戶網路中。</span><span class="sxs-lookup"><span data-stu-id="52351-149">Place hello connector close toohello target application in hello customer network.</span></span> <span data-ttu-id="52351-150">因為 hello 連接器和應用程式關閉這項設定最小化在 hello 拓撲圖表中的步驟 3。</span><span class="sxs-lookup"><span data-stu-id="52351-150">This configuration minimizes step 3 in hello topography diagram, because hello connector and application are close.</span></span> 

<span data-ttu-id="52351-151">如果您的連接器需要的視野 toohello 網域控制站，這個模式是有利的。</span><span class="sxs-lookup"><span data-stu-id="52351-151">If your connector needs a line of sight toohello domain controller, then this pattern is advantageous.</span></span> <span data-ttu-id="52351-152">大部分的客戶會使用此模式，因為它非常適合大部分情節。</span><span class="sxs-lookup"><span data-stu-id="52351-152">Most of our customers use this pattern, because it works well for most scenarios.</span></span> <span data-ttu-id="52351-153">此模式也可以結合 hello 連接器 hello 服務之間的模式 2 toooptimize 流量。</span><span class="sxs-lookup"><span data-stu-id="52351-153">This pattern can also be combined with pattern 2 toooptimize traffic between hello service and hello connector.</span></span>

### <a name="pattern-2-take-advantage-of-expressroute-with-public-peering"></a><span data-ttu-id="52351-154">模式 2︰利用 ExpressRoute 與公用對等互連</span><span class="sxs-lookup"><span data-stu-id="52351-154">Pattern 2: Take advantage of ExpressRoute with public peering</span></span>

<span data-ttu-id="52351-155">如果您有使用公用對等互連設定 ExpressRoute，您可以使用 hello 更快的 ExpressRoute 連線應用程式 Proxy 與 hello 連接器之間的流量。</span><span class="sxs-lookup"><span data-stu-id="52351-155">If you have ExpressRoute set up with public peering, you can use hello faster ExpressRoute connection for traffic between Application Proxy and hello connector.</span></span> <span data-ttu-id="52351-156">hello 連接器是仍在網路上，關閉 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="52351-156">hello connector is still on your network, close toohello app.</span></span>

### <a name="pattern-3-take-advantage-of-expressroute-with-private-peering"></a><span data-ttu-id="52351-157">模式 3︰利用具有私人對等互連的 ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="52351-157">Pattern 3: Take advantage of ExpressRoute with private peering</span></span>

<span data-ttu-id="52351-158">如果有專用的 VPN 或 ExpressRoute 在 Azure 和公司網路之間設定私人對等互連，您會有另一個選項。</span><span class="sxs-lookup"><span data-stu-id="52351-158">If you have a dedicated VPN or ExpressRoute set up with private peering between Azure and your corporate network, you have another option.</span></span> <span data-ttu-id="52351-159">在此組態中，通常會被視為 hello 公司網路的延伸模組的 hello Azure 中的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="52351-159">In this configuration, hello virtual network in Azure is typically considered as an extension of hello corporate network.</span></span> <span data-ttu-id="52351-160">因此您可以安裝 hello 連接器在 hello Azure 資料中心，且仍能滿足 hello 低延遲要求的 hello 連接器-應用程式的連接。</span><span class="sxs-lookup"><span data-stu-id="52351-160">So you can install hello connector in hello Azure datacenter, and still satisfy hello low latency requirements of hello connector-to-app connection.</span></span>

<span data-ttu-id="52351-161">延遲不會受到危害，因為流量會流經專用的連接。</span><span class="sxs-lookup"><span data-stu-id="52351-161">Latency is not compromised because traffic is flowing over a dedicated connection.</span></span> <span data-ttu-id="52351-162">您也可以改善應用程式 Proxy 服務的連接器延遲，因為 hello 連接器安裝在 Azure 資料中心關閉 tooyour Azure AD 租用戶位置。</span><span class="sxs-lookup"><span data-stu-id="52351-162">You also get improved Application Proxy service-to-connector latency because hello connector is installed in an Azure datacenter close tooyour Azure AD tenant location.</span></span>

![顯示安裝在 Azure 資料中心內之連接器的圖表](./media/application-proxy-network-topologies/application-proxy-expressroute-private.png)

### <a name="other-approaches"></a><span data-ttu-id="52351-164">其他方法</span><span class="sxs-lookup"><span data-stu-id="52351-164">Other approaches</span></span>

<span data-ttu-id="52351-165">雖然這篇文章的 hello 焦點是連接器放置，您也可以變更 hello 放置 hello 應用程式 tooget 較佳延遲的特性。</span><span class="sxs-lookup"><span data-stu-id="52351-165">Although hello focus of this article is connector placement, you can also change hello placement of hello application tooget better latency characteristics.</span></span>

<span data-ttu-id="52351-166">有愈來愈多的組織將其網路移至託管環境。</span><span class="sxs-lookup"><span data-stu-id="52351-166">Increasingly, organizations are moving their networks into hosted environments.</span></span> <span data-ttu-id="52351-167">這樣可讓他們 tooplace 自己也其公司的網路的一部分，它仍然是 hello 網域內的託管環境中的應用程式。</span><span class="sxs-lookup"><span data-stu-id="52351-167">This enables them tooplace their apps in a hosted environment that is also part of their corporate network, and still be within hello domain.</span></span> <span data-ttu-id="52351-168">在此情況下，hello hello 前幾節中討論的模式可以是 toohello 套用新的應用程式位置。</span><span class="sxs-lookup"><span data-stu-id="52351-168">In this case, hello patterns discussed in hello preceding sections can be applied toohello new application location.</span></span> <span data-ttu-id="52351-169">如果您正在考慮此選項，請參閱 [AD Domain Services](../active-directory-domain-services/active-directory-ds-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="52351-169">If you're considering this option, see [Azure AD Domain Services](../active-directory-domain-services/active-directory-ds-overview.md).</span></span>

<span data-ttu-id="52351-170">此外，請考慮組織使用的連接器[連接器群組](active-directory-application-proxy-connectors.md)tootarget 應用程式中不同的位置和網路。</span><span class="sxs-lookup"><span data-stu-id="52351-170">Additionally, consider organizing your connectors using [connector groups](active-directory-application-proxy-connectors.md) tootarget apps that are in different locations and networks.</span></span> 

## <a name="common-use-cases"></a><span data-ttu-id="52351-171">一般使用案例</span><span class="sxs-lookup"><span data-stu-id="52351-171">Common use cases</span></span>

<span data-ttu-id="52351-172">在本節中，我們將逐步解說幾個常見案例。</span><span class="sxs-lookup"><span data-stu-id="52351-172">In this section, we walk through a few common scenarios.</span></span> <span data-ttu-id="52351-173">假設該 hello Azure AD 租用戶 （和 proxy 因此為服務端點） 位於 hello United States (US)。</span><span class="sxs-lookup"><span data-stu-id="52351-173">Assume that hello Azure AD tenant (and therefore proxy service endpoint) is located in hello United States (US).</span></span> <span data-ttu-id="52351-174">hello 考量討論這些使用案例也適用於 tooother 區域周圍 hello 地球。</span><span class="sxs-lookup"><span data-stu-id="52351-174">hello considerations discussed in these use cases also apply tooother regions around hello globe.</span></span>

<span data-ttu-id="52351-175">這些情況下，我們將每個連線稱為「躍點」，並將它們編號以便於討論︰</span><span class="sxs-lookup"><span data-stu-id="52351-175">For these scenarios, we call each connection a "hop" and number them for easier discussion:</span></span>

- <span data-ttu-id="52351-176">**1 個躍點**： 使用者 toohello 應用程式 Proxy 服務</span><span class="sxs-lookup"><span data-stu-id="52351-176">**Hop 1**: User toohello Application Proxy service</span></span>
- <span data-ttu-id="52351-177">**2 個躍點**： 應用程式 Proxy 服務 toohello 應用程式 Proxy 連接器</span><span class="sxs-lookup"><span data-stu-id="52351-177">**Hop 2**: Application Proxy service toohello Application Proxy connector</span></span>
- <span data-ttu-id="52351-178">**3 個躍點**： 應用程式 Proxy 連接器 toohello 目標應用程式</span><span class="sxs-lookup"><span data-stu-id="52351-178">**Hop 3**: Application Proxy connector toohello target application</span></span> 

### <a name="use-case-1"></a><span data-ttu-id="52351-179">使用案例 1</span><span class="sxs-lookup"><span data-stu-id="52351-179">Use case 1</span></span>

<span data-ttu-id="52351-180">**案例：** hello 應用程式是在組織網路中 hello US，與 hello 中的使用者相同的區域。</span><span class="sxs-lookup"><span data-stu-id="52351-180">**Scenario:** hello app is in an organization's network in hello US, with users in hello same region.</span></span> <span data-ttu-id="52351-181">沒有 ExpressRoute 或 VPN hello Azure 資料中心與 hello 公司網路之間不存在。</span><span class="sxs-lookup"><span data-stu-id="52351-181">No ExpressRoute or VPN exists between hello Azure datacenter and hello corporate network.</span></span>

<span data-ttu-id="52351-182">**建議：**遵循模式 1，hello 上一節所述。</span><span class="sxs-lookup"><span data-stu-id="52351-182">**Recommendation:** Follow pattern 1, explained in hello previous section.</span></span> <span data-ttu-id="52351-183">如需改良的延遲，請視需要考慮使用 ExpressRoute。</span><span class="sxs-lookup"><span data-stu-id="52351-183">For improved latency, consider using ExpressRoute, if needed.</span></span>

<span data-ttu-id="52351-184">這是簡單的模式。</span><span class="sxs-lookup"><span data-stu-id="52351-184">This is a simple pattern.</span></span> <span data-ttu-id="52351-185">您可以最佳化躍點 3 放入 hello 連接器附近 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="52351-185">You optimize hop 3 by placing hello connector near hello app.</span></span> <span data-ttu-id="52351-186">這是也合理的選擇，因為 hello 連接器通常會隨的視野 toohello 應用程式和 toohello datacenter tooperform KCD 作業。</span><span class="sxs-lookup"><span data-stu-id="52351-186">This is also a natural choice, because hello connector typically is installed with line of sight toohello app and toohello datacenter tooperform KCD operations.</span></span>

![顯示的使用者、 proxy、 連接器和應用程式都位於 hello 我們的圖表](./media/application-proxy-network-topologies/application-proxy-pattern1.png)

### <a name="use-case-2"></a><span data-ttu-id="52351-188">使用案例 2</span><span class="sxs-lookup"><span data-stu-id="52351-188">Use case 2</span></span>

<span data-ttu-id="52351-189">**案例：** hello 應用程式是在組織網路中 hello US，與全域分散的使用者。</span><span class="sxs-lookup"><span data-stu-id="52351-189">**Scenario:** hello app is in an organization's network in hello US, with users spread out globally.</span></span> <span data-ttu-id="52351-190">沒有 ExpressRoute 或 VPN hello Azure 資料中心與 hello 公司網路之間不存在。</span><span class="sxs-lookup"><span data-stu-id="52351-190">No ExpressRoute or VPN exists between hello Azure datacenter and hello corporate network.</span></span>

<span data-ttu-id="52351-191">**建議：**遵循模式 1，hello 上一節所述。</span><span class="sxs-lookup"><span data-stu-id="52351-191">**Recommendation:** Follow pattern 1, explained in hello previous section.</span></span> 

<span data-ttu-id="52351-192">同樣地，hello 常見的模式是 toooptimize 躍點 3，位置靠近 hello 應用程式的 hello 連接器。</span><span class="sxs-lookup"><span data-stu-id="52351-192">Again, hello common pattern is toooptimize hop 3, where you place hello connector near hello app.</span></span> <span data-ttu-id="52351-193">躍點 3 不通常昂貴，如果它是所有內 hello 相同區域。</span><span class="sxs-lookup"><span data-stu-id="52351-193">Hop 3 is not typically expensive, if it is all within hello same region.</span></span> <span data-ttu-id="52351-194">不過，躍點 1 可能更耗費資源，根據位置 hello 使用者，因為 hello 世界各地的使用者必須存取在 hello 美國 hello 應用程式 Proxy 執行個體。</span><span class="sxs-lookup"><span data-stu-id="52351-194">However, hop 1 can be more expensive depending on where hello user is, because users across hello world must access hello Application Proxy instance in hello US.</span></span> <span data-ttu-id="52351-195">值得注意的是，就散佈於全球的使用者而言，任何 Proxy 解決方案會有相似特性。</span><span class="sxs-lookup"><span data-stu-id="52351-195">It's worth noting that any proxy solution has similar characteristics regarding users being spread out globally.</span></span>

![顯示使用者全域擴展，但 hello proxy、 連接器和應用程式會位於 hello 我們的圖表](./media/application-proxy-network-topologies/application-proxy-pattern2.png)

### <a name="use-case-3"></a><span data-ttu-id="52351-197">使用案例 3</span><span class="sxs-lookup"><span data-stu-id="52351-197">Use case 3</span></span>

<span data-ttu-id="52351-198">**案例：** hello 應用程式是在組織網路中 hello 我們。</span><span class="sxs-lookup"><span data-stu-id="52351-198">**Scenario:** hello app is in an organization's network in hello US.</span></span> <span data-ttu-id="52351-199">使用公用對等 ExpressRoute Azure 與 hello 公司網路之間不存在。</span><span class="sxs-lookup"><span data-stu-id="52351-199">ExpressRoute with public peering exists between Azure and hello corporate network.</span></span>

<span data-ttu-id="52351-200">**建議：**遵循模式 1 和 2，hello 上一節所述。</span><span class="sxs-lookup"><span data-stu-id="52351-200">**Recommendation:** Follow patterns 1 and 2, explained in hello previous section.</span></span>

<span data-ttu-id="52351-201">首先，將關閉，可能 toohello 應用程式的 hello 連接器。</span><span class="sxs-lookup"><span data-stu-id="52351-201">First, place hello connector as close as possible toohello app.</span></span> <span data-ttu-id="52351-202">然後，hello 系統會自動會使用 ExpressRoute 的躍點 2。</span><span class="sxs-lookup"><span data-stu-id="52351-202">Then, hello system automatically uses ExpressRoute for hop 2.</span></span> 

<span data-ttu-id="52351-203">如果 hello ExpressRoute 連結使用公用對等互連，hello hello proxy 與 hello 連接器之間的流量流程透過該連結。</span><span class="sxs-lookup"><span data-stu-id="52351-203">If hello ExpressRoute link is using public peering, hello traffic between hello proxy and hello connector flows over that link.</span></span> <span data-ttu-id="52351-204">躍點 2 具有最佳化延遲。</span><span class="sxs-lookup"><span data-stu-id="52351-204">Hop 2 has optimized latency.</span></span>

![ExpressRoute 顯示 hello proxy 之間連接器的圖表](./media/application-proxy-network-topologies/application-proxy-pattern3.png)

### <a name="use-case-4"></a><span data-ttu-id="52351-206">使用案例 4</span><span class="sxs-lookup"><span data-stu-id="52351-206">Use case 4</span></span>

<span data-ttu-id="52351-207">**案例：** hello 應用程式是在組織網路中 hello 我們。</span><span class="sxs-lookup"><span data-stu-id="52351-207">**Scenario:** hello app is in an organization's network in hello US.</span></span> <span data-ttu-id="52351-208">Azure 與 hello 公司網路之間不存在與私用對等 ExpressRoute。</span><span class="sxs-lookup"><span data-stu-id="52351-208">ExpressRoute with private peering exists between Azure and hello corporate network.</span></span>

<span data-ttu-id="52351-209">**建議：**遵循模式 3，hello 上一節所述。</span><span class="sxs-lookup"><span data-stu-id="52351-209">**Recommendation:** Follow pattern 3, explained in hello previous section.</span></span>

<span data-ttu-id="52351-210">置於 hello Azure 資料中心會透過 ExpressRoute 私用對等體的連接的 toohello 公司網路中的 hello 連接器。</span><span class="sxs-lookup"><span data-stu-id="52351-210">Place hello connector in hello Azure datacenter that is connected toohello corporate network through ExpressRoute private peering.</span></span> 

<span data-ttu-id="52351-211">hello 連接器可以放在 hello Azure 資料中心。</span><span class="sxs-lookup"><span data-stu-id="52351-211">hello connector can be placed in hello Azure datacenter.</span></span> <span data-ttu-id="52351-212">Hello 連接器仍然會有的視野 toohello 應用程式和 hello 資料中心透過 hello 私人網路，因為躍點 3 會維持最佳化。</span><span class="sxs-lookup"><span data-stu-id="52351-212">Since hello connector still has a line of sight toohello application and hello datacenter through hello private network, hop 3 remains optimized.</span></span> <span data-ttu-id="52351-213">此外，躍點 2 已進一步最佳化。</span><span class="sxs-lookup"><span data-stu-id="52351-213">In addition, hop 2 is optimized further.</span></span>

![顯示 hello 連接器中的 Azure 資料中心和 ExpressRoute hello 連接器與應用程式之間的圖表](./media/application-proxy-network-topologies/application-proxy-pattern4.png)

### <a name="use-case-5"></a><span data-ttu-id="52351-215">使用案例 5</span><span class="sxs-lookup"><span data-stu-id="52351-215">Use case 5</span></span>

<span data-ttu-id="52351-216">**案例：** hello 應用程式是在組織網路中含有 hello 應用程式 Proxy 執行個體和大部分的使用者在 hello hello EU，我們。</span><span class="sxs-lookup"><span data-stu-id="52351-216">**Scenario:** hello app is in an organization's network in hello EU, with hello Application Proxy instance and most users in hello US.</span></span>

<span data-ttu-id="52351-217">**建議：**附近 hello 應用程式的地方 hello 連接器。</span><span class="sxs-lookup"><span data-stu-id="52351-217">**Recommendation:** Place hello connector near hello app.</span></span> <span data-ttu-id="52351-218">因為美國使用者存取應用程式 Proxy 執行個體時所發生 toobe hello 中的相同的區域，躍點 1 不是太高成本。</span><span class="sxs-lookup"><span data-stu-id="52351-218">Because US users are accessing an Application Proxy instance that happens toobe in hello same region, hop 1 is not too expensive.</span></span> <span data-ttu-id="52351-219">躍點 3 已最佳化。</span><span class="sxs-lookup"><span data-stu-id="52351-219">Hop 3 is optimized.</span></span> <span data-ttu-id="52351-220">請考慮使用 ExpressRoute toooptimize 躍點 2。</span><span class="sxs-lookup"><span data-stu-id="52351-220">Consider using ExpressRoute toooptimize hop 2.</span></span> 

![顯示使用者和 proxy hello 美國、 hello 連接器與 hello EU 中的應用程式中的圖表](./media/application-proxy-network-topologies/application-proxy-pattern5b.png)

<span data-ttu-id="52351-222">您也可以考慮在此情況下使用另一個變體。</span><span class="sxs-lookup"><span data-stu-id="52351-222">You can also consider using one other variant in this situation.</span></span> <span data-ttu-id="52351-223">如果 hello 組織中的大部分使用者都位於 hello 我們，機率是會以確認您的網路延伸 toohello 我們也。</span><span class="sxs-lookup"><span data-stu-id="52351-223">If most users in hello organization are in hello US, then chances are that your network extends toohello US as well.</span></span> <span data-ttu-id="52351-224">Hello 連接器置於 hello 美國，並使用專用的 hello 公司內部網路列 toohello 應用程式在 hello EU。</span><span class="sxs-lookup"><span data-stu-id="52351-224">Place hello connector in hello US, and use hello dedicated internal corporate network line toohello application in hello EU.</span></span> <span data-ttu-id="52351-225">如此一來，躍點 2 和躍點 3 便已最佳化。</span><span class="sxs-lookup"><span data-stu-id="52351-225">This way hops 2 and 3 are optimized.</span></span>

![顯示 hello US、 hello EU 中應用程式中的使用者、 proxy 和連接器的圖表](./media/application-proxy-network-topologies/application-proxy-pattern5c.png)

## <a name="next-steps"></a><span data-ttu-id="52351-227">後續步驟</span><span class="sxs-lookup"><span data-stu-id="52351-227">Next steps</span></span>

- [<span data-ttu-id="52351-228">啟用應用程式 Proxy</span><span class="sxs-lookup"><span data-stu-id="52351-228">Enable Application Proxy</span></span>](active-directory-application-proxy-enable.md)
- [<span data-ttu-id="52351-229">啟用單一登入</span><span class="sxs-lookup"><span data-stu-id="52351-229">Enable single-sign on</span></span>](active-directory-application-proxy-sso-using-kcd.md)
- [<span data-ttu-id="52351-230">啟用條件式存取</span><span class="sxs-lookup"><span data-stu-id="52351-230">Enable conditional access</span></span>](active-directory-application-proxy-conditional-access.md)
- [<span data-ttu-id="52351-231">使用應用程式 Proxy 疑難排解您遇到的問題</span><span class="sxs-lookup"><span data-stu-id="52351-231">Troubleshoot issues you're having with Application Proxy</span></span>](active-directory-application-proxy-troubleshoot.md)
