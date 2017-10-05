---
title: "使用 Azure Active Directory 應用程式 Proxy 時的網路拓撲考量 | Microsoft Docs"
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
ms.openlocfilehash: 11244e0044eef8441e3a37ab8aeff0da30dacdb8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="network-topology-considerations-when-using-azure-active-directory-application-proxy"></a><span data-ttu-id="a623e-103">使用 Azure Active Directory 應用程式 Proxy 時的網路拓撲考量</span><span class="sxs-lookup"><span data-stu-id="a623e-103">Network topology considerations when using Azure Active Directory Application Proxy</span></span>

<span data-ttu-id="a623e-104">本文說明使用 Azure Active Directory 應用程式 Proxy 遠端發佈及存取您的應用程式時的網路拓撲考量。</span><span class="sxs-lookup"><span data-stu-id="a623e-104">This article explains network topology considerations when using Azure Active Directory (Azure AD) Application Proxy for publishing and accessing your applications remotely.</span></span>

## <a name="traffic-flow"></a><span data-ttu-id="a623e-105">流量</span><span class="sxs-lookup"><span data-stu-id="a623e-105">Traffic flow</span></span>

<span data-ttu-id="a623e-106">當應用程式透過 Azure AD App Proxy 發佈時，來自使用者往應用程式的流量會流過三個連線︰</span><span class="sxs-lookup"><span data-stu-id="a623e-106">When an application is published through Azure AD Application Proxy, traffic from the users to the applications flows through three connections:</span></span>

1. <span data-ttu-id="a623e-107">使用者連線至 Azure 上的 Azure AD 應用程式 Proxy 服務公用端點</span><span class="sxs-lookup"><span data-stu-id="a623e-107">The user connects to the Azure AD Application Proxy service public endpoint on Azure</span></span>
2. <span data-ttu-id="a623e-108">應用程式 Proxy 服務連線至應用程式 Proxy 連接器</span><span class="sxs-lookup"><span data-stu-id="a623e-108">The Application Proxy service connects to the Application Proxy connector</span></span>
3. <span data-ttu-id="a623e-109">應用程式 Proxy 連接器會連線到目標應用程式</span><span class="sxs-lookup"><span data-stu-id="a623e-109">The Application Proxy connector connects to the target application</span></span>

![顯示從使用者至目標應用程式之流量的圖表](./media/application-proxy-network-topologies/application-proxy-three-hops.png)

## <a name="tenant-location-and-application-proxy-service"></a><span data-ttu-id="a623e-111">租用戶位置與應用程式 Proxy 服務</span><span class="sxs-lookup"><span data-stu-id="a623e-111">Tenant location and Application Proxy service</span></span>

<span data-ttu-id="a623e-112">當您註冊 Azure AD 租用戶時，您租用戶的區域取決於您所指定的國家/地區。</span><span class="sxs-lookup"><span data-stu-id="a623e-112">When you sign up for an Azure AD tenant, the region of your tenant is determined by the country you specify.</span></span> <span data-ttu-id="a623e-113">當您啟用應用程式 Proxy 時，租用戶的應用程式 Proxy 服務執行個體會選取或建立在與 Azure AD 租用戶位於相同區域或最近的區域。</span><span class="sxs-lookup"><span data-stu-id="a623e-113">When you enable Application Proxy, the Application Proxy service instances for your tenant are chosen or created in the same region as your Azure AD tenant, or the closest region to it.</span></span>

<span data-ttu-id="a623e-114">例如，如果 Azure AD 租用戶的區域是歐盟 (EU)，則所有的應用程式 Proxy 連接器會使用歐盟 Azure 資料中心的服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="a623e-114">For example, if your Azure AD tenant’s region is the European Union (EU), all your Application Proxy connectors use service instances in Azure datacenters in the EU.</span></span> <span data-ttu-id="a623e-115">當使用者存取發佈的應用程式時，其流量會通過這個位置的應用程式 Proxy 服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="a623e-115">When your users access published applications, their traffic goes through the Application Proxy service instances in this location.</span></span>

## <a name="considerations-for-reducing-latency"></a><span data-ttu-id="a623e-116">降低延遲的考量</span><span class="sxs-lookup"><span data-stu-id="a623e-116">Considerations for reducing latency</span></span>

<span data-ttu-id="a623e-117">所有 Proxy 解決方案都會在您的網路連線中造成延遲。</span><span class="sxs-lookup"><span data-stu-id="a623e-117">All proxy solutions introduce latency into your network connection.</span></span> <span data-ttu-id="a623e-118">不論您選擇哪一個 Proxy 或 VPN 解決方案做為遠端存取解決方案，它一定包含一組伺服器，啟用您公司網路內部的連線。</span><span class="sxs-lookup"><span data-stu-id="a623e-118">No matter which proxy or VPN solution you choose as your remote access solution, it always includes a set of servers enabling the connection to inside your corporate network.</span></span>

<span data-ttu-id="a623e-119">組織通常包含其周邊網路中的伺服器端點。</span><span class="sxs-lookup"><span data-stu-id="a623e-119">Organizations typically include server endpoints in their perimeter network.</span></span> <span data-ttu-id="a623e-120">不過，使用 Azure AD 應用程式 Proxy，流量都會流過雲端中的 Proxy 服務，而連接器會位於公司的網路上。</span><span class="sxs-lookup"><span data-stu-id="a623e-120">With Azure AD Application Proxy, however, traffic flows through the proxy service in the cloud while the connectors reside on your corporate network.</span></span> <span data-ttu-id="a623e-121">不需要周邊網路。</span><span class="sxs-lookup"><span data-stu-id="a623e-121">No perimeter network is required.</span></span>

<span data-ttu-id="a623e-122">下一節包含的其他建議可協助您更進一步降低延遲。</span><span class="sxs-lookup"><span data-stu-id="a623e-122">The next sections contain additional suggestions to help you reduce latency even further.</span></span> 

### <a name="connector-placement"></a><span data-ttu-id="a623e-123">連接器放置</span><span class="sxs-lookup"><span data-stu-id="a623e-123">Connector placement</span></span>

<span data-ttu-id="a623e-124">應用程式 Proxy 會根據您的租用戶位置，為您選擇執行個體的位置。</span><span class="sxs-lookup"><span data-stu-id="a623e-124">Application Proxy chooses the location of instances for you, based on your tenant location.</span></span> <span data-ttu-id="a623e-125">不過，您可以決定在何處安裝連接器，讓您能夠定義網路流量的延遲特性。</span><span class="sxs-lookup"><span data-stu-id="a623e-125">However, you get to decide where to install the connector, giving you the power to define the latency characteristics of your network traffic.</span></span>

<span data-ttu-id="a623e-126">設定應用程式 Proxy 服務時，請詢問下列問題︰</span><span class="sxs-lookup"><span data-stu-id="a623e-126">When setting up the Application Proxy service, ask the following questions:</span></span>

* <span data-ttu-id="a623e-127">應用程式位於何處？</span><span class="sxs-lookup"><span data-stu-id="a623e-127">Where is the app located?</span></span>
* <span data-ttu-id="a623e-128">大多數存取應用程式的使用者位於何處？</span><span class="sxs-lookup"><span data-stu-id="a623e-128">Where are most users who access the app located?</span></span>
* <span data-ttu-id="a623e-129">應用程式 Proxy 執行個體所在的位置？</span><span class="sxs-lookup"><span data-stu-id="a623e-129">Where is the Application Proxy instance located?</span></span>
* <span data-ttu-id="a623e-130">您是否已設定 Azure 資料中心的專用網路，例如 Azure ExpressRoute 或類似的 VPN？</span><span class="sxs-lookup"><span data-stu-id="a623e-130">Do you already have a dedicated network connection to Azure datacenters set up, like Azure ExpressRoute or a similar VPN?</span></span>

<span data-ttu-id="a623e-131">連接器必須與 Azure 和您的應用程式 (流量圖表中的步驟 2 和 3) 進行通訊，因此連接器的位置會影響這些兩個連線的延遲。</span><span class="sxs-lookup"><span data-stu-id="a623e-131">The connector has to communicate with both Azure and your applications (steps 2 and 3 in the Traffic flow diagram), so the placement of the connector affects the latency of those two connections.</span></span> <span data-ttu-id="a623e-132">評估連接器的位置時，請記住下列幾點：</span><span class="sxs-lookup"><span data-stu-id="a623e-132">When evaluating the placement of the connector, keep in mind the following points:</span></span>

* <span data-ttu-id="a623e-133">如果您想要使用 Kerberos 限制委派 (KCD) 進行單一登入，連接器需要資料中心的視野。</span><span class="sxs-lookup"><span data-stu-id="a623e-133">If you want to use Kerberos constrained delegation (KCD) for single sign-on, then the connector needs a line of sight to a datacenter.</span></span> <span data-ttu-id="a623e-134">此外，連接器伺服器必須加入網域。</span><span class="sxs-lookup"><span data-stu-id="a623e-134">Additionally, the connector server needs to be domain joined.</span></span>  
* <span data-ttu-id="a623e-135">有疑問時，請安裝較接近應用程式的連接器。</span><span class="sxs-lookup"><span data-stu-id="a623e-135">When in doubt, install the connector closer to the application.</span></span>

### <a name="general-approach-to-minimize-latency"></a><span data-ttu-id="a623e-136">將延遲降至最低的常見方式</span><span class="sxs-lookup"><span data-stu-id="a623e-136">General approach to minimize latency</span></span>

<span data-ttu-id="a623e-137">最佳化每個網路連線，即可將端對端流量的延遲降至最低。</span><span class="sxs-lookup"><span data-stu-id="a623e-137">You can minimize the latency of the end-to-end traffic by optimizing each network connection.</span></span> <span data-ttu-id="a623e-138">可以將每個連線最佳化，方法為︰</span><span class="sxs-lookup"><span data-stu-id="a623e-138">Each connection can be optimized by:</span></span>

* <span data-ttu-id="a623e-139">減少躍點兩端之間的距離。</span><span class="sxs-lookup"><span data-stu-id="a623e-139">Reducing the distance between the two ends of the hop.</span></span>
* <span data-ttu-id="a623e-140">選擇正確的網路來周遊。</span><span class="sxs-lookup"><span data-stu-id="a623e-140">Choosing the right network to traverse.</span></span> <span data-ttu-id="a623e-141">例如，周遊私人網路而非公用網際網路可能會因為專用的連結而更快。</span><span class="sxs-lookup"><span data-stu-id="a623e-141">For example, traversing a private network rather than the public Internet may be faster, due to dedicated links.</span></span>

<span data-ttu-id="a623e-142">如果在 Azure 與您的公司網路之間有專用的 VPN 或 ExpressRoute 連結，您可加以使用。</span><span class="sxs-lookup"><span data-stu-id="a623e-142">If you have a dedicated VPN or ExpressRoute link between Azure and your corporate network, you may want to use that.</span></span>

## <a name="focus-your-optimization-strategy"></a><span data-ttu-id="a623e-143">專注於最佳化策略</span><span class="sxs-lookup"><span data-stu-id="a623e-143">Focus your optimization strategy</span></span>

<span data-ttu-id="a623e-144">您幾乎沒有辦法可以控制您的使用者與應用程式 Proxy 服務之間的連線。</span><span class="sxs-lookup"><span data-stu-id="a623e-144">There's little that you can do to control the connection between your users and the Application Proxy service.</span></span> <span data-ttu-id="a623e-145">使用者可以從家用網路、咖啡廳或不同的國家/地區存取您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="a623e-145">Users may access your apps from a home network, a coffee shop, or a different country.</span></span> <span data-ttu-id="a623e-146">反之，您可以將應用程式 Proxy 服務與應用程式的應用程式 Proxy 連接器之連線最佳化。</span><span class="sxs-lookup"><span data-stu-id="a623e-146">Instead, you can optimize the connections from the Application Proxy service to the Application Proxy connectors to the apps.</span></span> <span data-ttu-id="a623e-147">請考慮將下列模式整合在您的環境中。</span><span class="sxs-lookup"><span data-stu-id="a623e-147">Consider incorporating the following patterns in your environment.</span></span>

### <a name="pattern-1-put-the-connector-close-to-the-application"></a><span data-ttu-id="a623e-148">模式 1︰將連接器放在應用程式附近</span><span class="sxs-lookup"><span data-stu-id="a623e-148">Pattern 1: Put the connector close to the application</span></span>

<span data-ttu-id="a623e-149">將連接器放在接近客戶網路中的目標應用程式。</span><span class="sxs-lookup"><span data-stu-id="a623e-149">Place the connector close to the target application in the customer network.</span></span> <span data-ttu-id="a623e-150">因為連接器和應用程式已關閉，這項設定會將拓撲圖表中的步驟 3 降到最低。</span><span class="sxs-lookup"><span data-stu-id="a623e-150">This configuration minimizes step 3 in the topography diagram, because the connector and application are close.</span></span> 

<span data-ttu-id="a623e-151">如果您的連接器需要能夠觀察網域控制站，此模式是有利的。</span><span class="sxs-lookup"><span data-stu-id="a623e-151">If your connector needs a line of sight to the domain controller, then this pattern is advantageous.</span></span> <span data-ttu-id="a623e-152">大部分的客戶會使用此模式，因為它非常適合大部分情節。</span><span class="sxs-lookup"><span data-stu-id="a623e-152">Most of our customers use this pattern, because it works well for most scenarios.</span></span> <span data-ttu-id="a623e-153">還可以將這個模式與模式 2 結合，以將服務與連接器之間的流量最佳化。</span><span class="sxs-lookup"><span data-stu-id="a623e-153">This pattern can also be combined with pattern 2 to optimize traffic between the service and the connector.</span></span>

### <a name="pattern-2-take-advantage-of-expressroute-with-public-peering"></a><span data-ttu-id="a623e-154">模式 2︰利用 ExpressRoute 與公用對等互連</span><span class="sxs-lookup"><span data-stu-id="a623e-154">Pattern 2: Take advantage of ExpressRoute with public peering</span></span>

<span data-ttu-id="a623e-155">如果 ExpressRoute 已設定公用對等互連，您可以對應用程式 Proxy 與連接器之間的流量利用更快速的 ExpressRoute 連線。</span><span class="sxs-lookup"><span data-stu-id="a623e-155">If you have ExpressRoute set up with public peering, you can use the faster ExpressRoute connection for traffic between Application Proxy and the connector.</span></span> <span data-ttu-id="a623e-156">連接器仍在您的網路上，接近應用程式。</span><span class="sxs-lookup"><span data-stu-id="a623e-156">The connector is still on your network, close to the app.</span></span>

### <a name="pattern-3-take-advantage-of-expressroute-with-private-peering"></a><span data-ttu-id="a623e-157">模式 3︰利用具有私人對等互連的 ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="a623e-157">Pattern 3: Take advantage of ExpressRoute with private peering</span></span>

<span data-ttu-id="a623e-158">如果有專用的 VPN 或 ExpressRoute 在 Azure 和公司網路之間設定私人對等互連，您會有另一個選項。</span><span class="sxs-lookup"><span data-stu-id="a623e-158">If you have a dedicated VPN or ExpressRoute set up with private peering between Azure and your corporate network, you have another option.</span></span> <span data-ttu-id="a623e-159">在此組態中，Azure 中的虛擬網路通常會被視為公司網路的擴充功能。</span><span class="sxs-lookup"><span data-stu-id="a623e-159">In this configuration, the virtual network in Azure is typically considered as an extension of the corporate network.</span></span> <span data-ttu-id="a623e-160">因此，您可以在 Azure 資料中心內安裝連接器，並仍能滿足連接器對應用程式連線之低延遲需求。</span><span class="sxs-lookup"><span data-stu-id="a623e-160">So you can install the connector in the Azure datacenter, and still satisfy the low latency requirements of the connector-to-app connection.</span></span>

<span data-ttu-id="a623e-161">延遲不會受到危害，因為流量會流經專用的連接。</span><span class="sxs-lookup"><span data-stu-id="a623e-161">Latency is not compromised because traffic is flowing over a dedicated connection.</span></span> <span data-ttu-id="a623e-162">您的應用程式 Proxy 服務對連接器延遲也會有所改進，因為連接器會安裝在接近 Azure AD 租用戶位置的 Azure 資料中心。</span><span class="sxs-lookup"><span data-stu-id="a623e-162">You also get improved Application Proxy service-to-connector latency because the connector is installed in an Azure datacenter close to your Azure AD tenant location.</span></span>

![顯示安裝在 Azure 資料中心內之連接器的圖表](./media/application-proxy-network-topologies/application-proxy-expressroute-private.png)

### <a name="other-approaches"></a><span data-ttu-id="a623e-164">其他方法</span><span class="sxs-lookup"><span data-stu-id="a623e-164">Other approaches</span></span>

<span data-ttu-id="a623e-165">雖然本文的重點是連接器放置，但您也可以變更應用程式的位置，以取得較佳的延遲特性。</span><span class="sxs-lookup"><span data-stu-id="a623e-165">Although the focus of this article is connector placement, you can also change the placement of the application to get better latency characteristics.</span></span>

<span data-ttu-id="a623e-166">有愈來愈多的組織將其網路移至託管環境。</span><span class="sxs-lookup"><span data-stu-id="a623e-166">Increasingly, organizations are moving their networks into hosted environments.</span></span> <span data-ttu-id="a623e-167">這可讓它們將自己的應用程式放在託管環境中，這也是其公司網路的一部分，並仍在網域內。</span><span class="sxs-lookup"><span data-stu-id="a623e-167">This enables them to place their apps in a hosted environment that is also part of their corporate network, and still be within the domain.</span></span> <span data-ttu-id="a623e-168">在此情況下，前幾節中所討論的模式可以套用至新的應用程式位置。</span><span class="sxs-lookup"><span data-stu-id="a623e-168">In this case, the patterns discussed in the preceding sections can be applied to the new application location.</span></span> <span data-ttu-id="a623e-169">如果您正在考慮此選項，請參閱 [AD Domain Services](../active-directory-domain-services/active-directory-ds-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="a623e-169">If you're considering this option, see [Azure AD Domain Services](../active-directory-domain-services/active-directory-ds-overview.md).</span></span>

<span data-ttu-id="a623e-170">此外，請考慮使用[連接器群組](active-directory-application-proxy-connectors.md)來組織連接器，以鎖定位於不同位置和網路的應用程式。</span><span class="sxs-lookup"><span data-stu-id="a623e-170">Additionally, consider organizing your connectors using [connector groups](active-directory-application-proxy-connectors.md) to target apps that are in different locations and networks.</span></span> 

## <a name="common-use-cases"></a><span data-ttu-id="a623e-171">一般使用案例</span><span class="sxs-lookup"><span data-stu-id="a623e-171">Common use cases</span></span>

<span data-ttu-id="a623e-172">在本節中，我們將逐步解說幾個常見案例。</span><span class="sxs-lookup"><span data-stu-id="a623e-172">In this section, we walk through a few common scenarios.</span></span> <span data-ttu-id="a623e-173">假設 Azure AD 租用戶 (以及 Proxy 服務端點) 位於美國 (US)。</span><span class="sxs-lookup"><span data-stu-id="a623e-173">Assume that the Azure AD tenant (and therefore proxy service endpoint) is located in the United States (US).</span></span> <span data-ttu-id="a623e-174">這些使用案例中討論的考量也適用於全球各地的其他區域。</span><span class="sxs-lookup"><span data-stu-id="a623e-174">The considerations discussed in these use cases also apply to other regions around the globe.</span></span>

<span data-ttu-id="a623e-175">這些情況下，我們將每個連線稱為「躍點」，並將它們編號以便於討論︰</span><span class="sxs-lookup"><span data-stu-id="a623e-175">For these scenarios, we call each connection a "hop" and number them for easier discussion:</span></span>

- <span data-ttu-id="a623e-176">**躍點 1**：使用者至應用程式 Proxy 服務</span><span class="sxs-lookup"><span data-stu-id="a623e-176">**Hop 1**: User to the Application Proxy service</span></span>
- <span data-ttu-id="a623e-177">**躍點 2**：應用程式 Proxy 服務至應用程式 Proxy 連接器</span><span class="sxs-lookup"><span data-stu-id="a623e-177">**Hop 2**: Application Proxy service to the Application Proxy connector</span></span>
- <span data-ttu-id="a623e-178">**躍點 3**：應用程式 Proxy 連接器至目標應用程式</span><span class="sxs-lookup"><span data-stu-id="a623e-178">**Hop 3**: Application Proxy connector to the target application</span></span> 

### <a name="use-case-1"></a><span data-ttu-id="a623e-179">使用案例 1</span><span class="sxs-lookup"><span data-stu-id="a623e-179">Use case 1</span></span>

<span data-ttu-id="a623e-180">**案例︰**應用程式在美國組織的網路中，其使用者位於相同的區域中。</span><span class="sxs-lookup"><span data-stu-id="a623e-180">**Scenario:** The app is in an organization's network in the US, with users in the same region.</span></span> <span data-ttu-id="a623e-181">Azure 資料中心與公司網路之間沒有 ExpressRoute 或 VPN 存在。</span><span class="sxs-lookup"><span data-stu-id="a623e-181">No ExpressRoute or VPN exists between the Azure datacenter and the corporate network.</span></span>

<span data-ttu-id="a623e-182">**建議︰**遵循模式 1，如上一節所述。</span><span class="sxs-lookup"><span data-stu-id="a623e-182">**Recommendation:** Follow pattern 1, explained in the previous section.</span></span> <span data-ttu-id="a623e-183">如需改良的延遲，請視需要考慮使用 ExpressRoute。</span><span class="sxs-lookup"><span data-stu-id="a623e-183">For improved latency, consider using ExpressRoute, if needed.</span></span>

<span data-ttu-id="a623e-184">這是簡單的模式。</span><span class="sxs-lookup"><span data-stu-id="a623e-184">This is a simple pattern.</span></span> <span data-ttu-id="a623e-185">將連接器放在應用程式附近，以最佳化躍點 3。</span><span class="sxs-lookup"><span data-stu-id="a623e-185">You optimize hop 3 by placing the connector near the app.</span></span> <span data-ttu-id="a623e-186">這是也很自然的選擇，因為連接器通常安裝在直視應用程式及資料中心以執行 KCD 作業。</span><span class="sxs-lookup"><span data-stu-id="a623e-186">This is also a natural choice, because the connector typically is installed with line of sight to the app and to the datacenter to perform KCD operations.</span></span>

![圖表顯示使用者、Proxy、連接器及應用程式全都在美國](./media/application-proxy-network-topologies/application-proxy-pattern1.png)

### <a name="use-case-2"></a><span data-ttu-id="a623e-188">使用案例 2</span><span class="sxs-lookup"><span data-stu-id="a623e-188">Use case 2</span></span>

<span data-ttu-id="a623e-189">**案例︰**應用程式在美國組織的網路中，其使用者分散於全球各地。</span><span class="sxs-lookup"><span data-stu-id="a623e-189">**Scenario:** The app is in an organization's network in the US, with users spread out globally.</span></span> <span data-ttu-id="a623e-190">Azure 資料中心與公司網路之間沒有 ExpressRoute 或 VPN 存在。</span><span class="sxs-lookup"><span data-stu-id="a623e-190">No ExpressRoute or VPN exists between the Azure datacenter and the corporate network.</span></span>

<span data-ttu-id="a623e-191">**建議︰**遵循模式 1，如上一節所述。</span><span class="sxs-lookup"><span data-stu-id="a623e-191">**Recommendation:** Follow pattern 1, explained in the previous section.</span></span> 

<span data-ttu-id="a623e-192">同樣地，最常見的模式是最佳化躍點 3，您將連接器放在應用程式附近的位置。</span><span class="sxs-lookup"><span data-stu-id="a623e-192">Again, the common pattern is to optimize hop 3, where you place the connector near the app.</span></span> <span data-ttu-id="a623e-193">躍點 3 通常不是高成本，如果全部都在相同區域內。</span><span class="sxs-lookup"><span data-stu-id="a623e-193">Hop 3 is not typically expensive, if it is all within the same region.</span></span> <span data-ttu-id="a623e-194">不過，躍點 1 可能會根據使用者所在的位置而更高成本，因為世界各地的使用者必須存取美國的應用程式 Proxy 執行個體。</span><span class="sxs-lookup"><span data-stu-id="a623e-194">However, hop 1 can be more expensive depending on where the user is, because users across the world must access the Application Proxy instance in the US.</span></span> <span data-ttu-id="a623e-195">值得注意的是，就散佈於全球的使用者而言，任何 Proxy 解決方案會有相似特性。</span><span class="sxs-lookup"><span data-stu-id="a623e-195">It's worth noting that any proxy solution has similar characteristics regarding users being spread out globally.</span></span>

![圖表顯示使用者散佈於全球，但 Proxy、連接器及應用程式位於美國](./media/application-proxy-network-topologies/application-proxy-pattern2.png)

### <a name="use-case-3"></a><span data-ttu-id="a623e-197">使用案例 3</span><span class="sxs-lookup"><span data-stu-id="a623e-197">Use case 3</span></span>

<span data-ttu-id="a623e-198">**案例︰**應用程式在美國組織的網路中。</span><span class="sxs-lookup"><span data-stu-id="a623e-198">**Scenario:** The app is in an organization's network in the US.</span></span> <span data-ttu-id="a623e-199">Azure 與公司網路之間存在 ExpressRoute 與公用對等互連。</span><span class="sxs-lookup"><span data-stu-id="a623e-199">ExpressRoute with public peering exists between Azure and the corporate network.</span></span>

<span data-ttu-id="a623e-200">**建議︰**遵循模式 1 和 2，如上一節所述。</span><span class="sxs-lookup"><span data-stu-id="a623e-200">**Recommendation:** Follow patterns 1 and 2, explained in the previous section.</span></span>

<span data-ttu-id="a623e-201">首先，盡可能將連接器放置接近應用程式。</span><span class="sxs-lookup"><span data-stu-id="a623e-201">First, place the connector as close as possible to the app.</span></span> <span data-ttu-id="a623e-202">然後，系統會自動使用躍點 2 的 ExpressRoute。</span><span class="sxs-lookup"><span data-stu-id="a623e-202">Then, the system automatically uses ExpressRoute for hop 2.</span></span> 

<span data-ttu-id="a623e-203">如果 ExpressRoute 連結使用公用互連，則 Proxy 與連接器之間的流量會流過該連結。</span><span class="sxs-lookup"><span data-stu-id="a623e-203">If the ExpressRoute link is using public peering, the traffic between the proxy and the connector flows over that link.</span></span> <span data-ttu-id="a623e-204">躍點 2 具有最佳化延遲。</span><span class="sxs-lookup"><span data-stu-id="a623e-204">Hop 2 has optimized latency.</span></span>

![圖表顯示 Proxy 與連接器之間的 ExpressRoute](./media/application-proxy-network-topologies/application-proxy-pattern3.png)

### <a name="use-case-4"></a><span data-ttu-id="a623e-206">使用案例 4</span><span class="sxs-lookup"><span data-stu-id="a623e-206">Use case 4</span></span>

<span data-ttu-id="a623e-207">**案例︰**應用程式在美國組織的網路中。</span><span class="sxs-lookup"><span data-stu-id="a623e-207">**Scenario:** The app is in an organization's network in the US.</span></span> <span data-ttu-id="a623e-208">Azure 與公司網路之間存在 ExpressRoute 與私人對等互連。</span><span class="sxs-lookup"><span data-stu-id="a623e-208">ExpressRoute with private peering exists between Azure and the corporate network.</span></span>

<span data-ttu-id="a623e-209">**建議︰**遵循模式 3，如上一節所述。</span><span class="sxs-lookup"><span data-stu-id="a623e-209">**Recommendation:** Follow pattern 3, explained in the previous section.</span></span>

<span data-ttu-id="a623e-210">將連接器放置於透過 ExpressRoute 私人對等互連連線到公司網路的 Azure 資料中心。</span><span class="sxs-lookup"><span data-stu-id="a623e-210">Place the connector in the Azure datacenter that is connected to the corporate network through ExpressRoute private peering.</span></span> 

<span data-ttu-id="a623e-211">連接器可放置於 Azure 資料中心。</span><span class="sxs-lookup"><span data-stu-id="a623e-211">The connector can be placed in the Azure datacenter.</span></span> <span data-ttu-id="a623e-212">因為連接器仍可透過私人網路直視應用程式和資料中心，躍點 3 會維持最佳化。</span><span class="sxs-lookup"><span data-stu-id="a623e-212">Since the connector still has a line of sight to the application and the datacenter through the private network, hop 3 remains optimized.</span></span> <span data-ttu-id="a623e-213">此外，躍點 2 已進一步最佳化。</span><span class="sxs-lookup"><span data-stu-id="a623e-213">In addition, hop 2 is optimized further.</span></span>

![圖表顯示 Azure 資料中心內的連接器，和連接器與應用程式之間的 ExpressRoute](./media/application-proxy-network-topologies/application-proxy-pattern4.png)

### <a name="use-case-5"></a><span data-ttu-id="a623e-215">使用案例 5</span><span class="sxs-lookup"><span data-stu-id="a623e-215">Use case 5</span></span>

<span data-ttu-id="a623e-216">**案例︰**用程式在歐盟組織的網路中，而應用程式 Proxy 執行個體與大部分使用者位於美國。</span><span class="sxs-lookup"><span data-stu-id="a623e-216">**Scenario:** The app is in an organization's network in the EU, with the Application Proxy instance and most users in the US.</span></span>

<span data-ttu-id="a623e-217">**建議︰**將連接器放置在應用程式附近。</span><span class="sxs-lookup"><span data-stu-id="a623e-217">**Recommendation:** Place the connector near the app.</span></span> <span data-ttu-id="a623e-218">因為美國使用者會存取剛好在相同區域中的應用程式 Proxy 執行個體，躍點 1 並不過於昂貴。</span><span class="sxs-lookup"><span data-stu-id="a623e-218">Because US users are accessing an Application Proxy instance that happens to be in the same region, hop 1 is not too expensive.</span></span> <span data-ttu-id="a623e-219">躍點 3 已最佳化。</span><span class="sxs-lookup"><span data-stu-id="a623e-219">Hop 3 is optimized.</span></span> <span data-ttu-id="a623e-220">請考慮使用 ExpressRoute 將躍點 2 最佳化。</span><span class="sxs-lookup"><span data-stu-id="a623e-220">Consider using ExpressRoute to optimize hop 2.</span></span> 

![圖表顯示使用者和 Proxy 在美國，而連接器與應用程式在歐盟](./media/application-proxy-network-topologies/application-proxy-pattern5b.png)

<span data-ttu-id="a623e-222">您也可以考慮在此情況下使用另一個變體。</span><span class="sxs-lookup"><span data-stu-id="a623e-222">You can also consider using one other variant in this situation.</span></span> <span data-ttu-id="a623e-223">如果組織中的大部分使用者不在美國，則可能您的網路也會延伸至美國。</span><span class="sxs-lookup"><span data-stu-id="a623e-223">If most users in the organization are in the US, then chances are that your network extends to the US as well.</span></span> <span data-ttu-id="a623e-224">將連接器放在美國，並使用歐盟國家應用程式的專用內部企業網路。</span><span class="sxs-lookup"><span data-stu-id="a623e-224">Place the connector in the US, and use the dedicated internal corporate network line to the application in the EU.</span></span> <span data-ttu-id="a623e-225">如此一來，躍點 2 和躍點 3 便已最佳化。</span><span class="sxs-lookup"><span data-stu-id="a623e-225">This way hops 2 and 3 are optimized.</span></span>

![圖表顯示使用者、Proxy 和連接器在美國，而應用程式在歐盟](./media/application-proxy-network-topologies/application-proxy-pattern5c.png)

## <a name="next-steps"></a><span data-ttu-id="a623e-227">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a623e-227">Next steps</span></span>

- [<span data-ttu-id="a623e-228">啟用應用程式 Proxy</span><span class="sxs-lookup"><span data-stu-id="a623e-228">Enable Application Proxy</span></span>](active-directory-application-proxy-enable.md)
- [<span data-ttu-id="a623e-229">啟用單一登入</span><span class="sxs-lookup"><span data-stu-id="a623e-229">Enable single-sign on</span></span>](active-directory-application-proxy-sso-using-kcd.md)
- [<span data-ttu-id="a623e-230">啟用條件式存取</span><span class="sxs-lookup"><span data-stu-id="a623e-230">Enable conditional access</span></span>](active-directory-application-proxy-conditional-access.md)
- [<span data-ttu-id="a623e-231">使用應用程式 Proxy 疑難排解您遇到的問題</span><span class="sxs-lookup"><span data-stu-id="a623e-231">Troubleshoot issues you're having with Application Proxy</span></span>](active-directory-application-proxy-troubleshoot.md)
