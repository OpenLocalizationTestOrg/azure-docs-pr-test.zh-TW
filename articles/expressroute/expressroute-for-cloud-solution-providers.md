---
title: "適用於雲端解決方案提供者 (CSP) 的 Azure ExpressRoute | Microsoft Docs"
description: "本文提供的資訊適用於想要將 Azure 服務和 ExpressRoute 併入其供應項目的雲端服務提供者。"
documentationcenter: na
services: expressroute
author: richcar
manager: carmonm
editor: 
ms.assetid: f6c5f8ee-40ba-41a1-ae31-67669ca419a6
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/10/2016
ms.author: richcar
ms.openlocfilehash: 26c9420c9b8ba1aff6b016c01b8ed51853c91506
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="expressroute-for-cloud-solution-providers-csp"></a><span data-ttu-id="4b191-103">適用於雲端解決方案提供者 (CSP) 的 ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="4b191-103">ExpressRoute for Cloud Solution Providers (CSP)</span></span>
<span data-ttu-id="4b191-104">Microsoft 為傳統的轉銷商和經銷商 (CSP) 提供超大規模的服務，以便為您的客戶快速佈建新的服務和解決方案，而不需要投資開發這些新服務。</span><span class="sxs-lookup"><span data-stu-id="4b191-104">Microsoft provides Hyper-scale services for traditional resellers and distributors (CSP) to be able to rapidly provision new services and solutions for your customers without the need to invest in developing these new services.</span></span> <span data-ttu-id="4b191-105">若要讓雲端解決方案提供者 (CSP) 能夠直接管理這些新服務，Microsoft 提供了一些程式和 API，讓 CSP 可以代表您的客戶管理 Microsoft Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="4b191-105">To allow the Cloud Solution Provider (CSP) the ability to directly manage these new services, Microsoft provides programs and APIs that allow the CSP to manage Microsoft Azure resources on behalf of your customers.</span></span> <span data-ttu-id="4b191-106">其中一個資源是 ExpressRoute。</span><span class="sxs-lookup"><span data-stu-id="4b191-106">One of those resources is ExpressRoute.</span></span> <span data-ttu-id="4b191-107">ExpressRoute 可讓 CSP 將現有的客戶資源連接到 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="4b191-107">ExpressRoute allows the CSP to connect existing customer resources to Azure services.</span></span> <span data-ttu-id="4b191-108">ExpressRoute 是 Azure 中服務的高速私用通訊連結。</span><span class="sxs-lookup"><span data-stu-id="4b191-108">ExpressRoute is a high speed private communications link to services in Azure.</span></span> 

<span data-ttu-id="4b191-109">ExpresRoute 是由一組附加至單一客戶訂用帳戶的高可用性電路所組成，不能由多個客戶共用。</span><span class="sxs-lookup"><span data-stu-id="4b191-109">ExpresRoute is comprised of a pair of circuits for high availability that are attached to a single customer subscription(s) and cannot be shared by multiple customers.</span></span> <span data-ttu-id="4b191-110">每個電路應在不同的路由器中終止，以維持高可用性。</span><span class="sxs-lookup"><span data-stu-id="4b191-110">Each circuit should be terminated in a different router to maintain the high availability.</span></span>

> [!NOTE]
> <span data-ttu-id="4b191-111">ExpressRoute 有頻寬和連接端點，這表示大型/複雜的實作需要單一客戶有多個 ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="4b191-111">There are bandwidth and connection caps on ExpressRoute which means that large/complex implementations will require multiple ExpressRoute circuits for a single customer.</span></span>
> 
> 

<span data-ttu-id="4b191-112">Microsoft Azure 提供越來越多的服務，您可以將這些服務提供給您的客戶。</span><span class="sxs-lookup"><span data-stu-id="4b191-112">Microsoft Azure provides a growing number of services that you can offer to your customers.</span></span>  <span data-ttu-id="4b191-113">若要充分利用這些服務，則必須使用 ExpressRoute 連接，以提供對 Microsoft Azure 環境的高速低延遲存取。</span><span class="sxs-lookup"><span data-stu-id="4b191-113">To best take advantage of these services will require the use ExpressRoute connections to provide high speed low latency access to the Microsoft Azure environment.</span></span>

## <a name="microsoft-azure-management"></a><span data-ttu-id="4b191-114">Microsoft Azure 管理</span><span class="sxs-lookup"><span data-stu-id="4b191-114">Microsoft Azure management</span></span>
<span data-ttu-id="4b191-115">Microsoft 允許以程式設計方式整合您自己的服務管理系統，進而提供 API 讓 CSP 管理 Azure 客戶訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="4b191-115">Microsoft provides CSPs with APIs to manage the Azure customer subscriptions by allowing programmatic integration with your own service management systems.</span></span> <span data-ttu-id="4b191-116">[這裡](https://msdn.microsoft.com/library/partnercenter/dn974944.aspx)可以找到支援的管理功能。</span><span class="sxs-lookup"><span data-stu-id="4b191-116">Supported management capabilities can be found [here](https://msdn.microsoft.com/library/partnercenter/dn974944.aspx).</span></span>

## <a name="microsoft-azure-resource-management"></a><span data-ttu-id="4b191-117">Microsoft Azure 資源管理</span><span class="sxs-lookup"><span data-stu-id="4b191-117">Microsoft Azure resource management</span></span>
<span data-ttu-id="4b191-118">您與客戶簽訂的合約將會決定訂用帳戶的管理方式。</span><span class="sxs-lookup"><span data-stu-id="4b191-118">Depending on the contract you have with your customer will determine how the subscription will be managed.</span></span> <span data-ttu-id="4b191-119">CSP 可以直接管理資源的建立和維護，或客戶可以持續控制 Microsoft Azure 訂用帳戶並建立他們所需的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="4b191-119">The CSP can directly manage the creation and maintenance of resources or the customer can maintain control of the Microsoft Azure subscription and create the Azure resources as they need.</span></span> <span data-ttu-id="4b191-120">如果您的客戶管理其 Microsoft Azure 訂用帳戶中的資源建立，他們會使用以下其中一個模型：“Connect-Through” 模型或 “Connect-To” 模型。</span><span class="sxs-lookup"><span data-stu-id="4b191-120">If your customer manages the creation of resources in their Microsoft Azure subscription they will use one of two models: “Connect-Through” model, or “Direct-To” model.</span></span> <span data-ttu-id="4b191-121">下列各節會詳細說明這些模型。</span><span class="sxs-lookup"><span data-stu-id="4b191-121">These models are described in detail in the following sections.</span></span>  

### <a name="connect-through-model"></a><span data-ttu-id="4b191-122">Connect-Through 模型</span><span class="sxs-lookup"><span data-stu-id="4b191-122">Connect-through model</span></span>
![替代文字](./media/expressroute-for-cloud-solution-providers/connect-through.png)  

<span data-ttu-id="4b191-124">在 Connect-Through 模型中，CSP 會在您的資料中心與您客戶的 Azure 訂用帳戶之間建立直接連線。</span><span class="sxs-lookup"><span data-stu-id="4b191-124">In the connect-through model, the CSP creates a direct connection between your datacenter and your customer’s Azure subscription.</span></span> <span data-ttu-id="4b191-125">使用 ExpressRoute 進行直接連線，連接您的網路與 Azure。</span><span class="sxs-lookup"><span data-stu-id="4b191-125">The direct connection is made using ExpressRoute, connecting your network with Azure.</span></span> <span data-ttu-id="4b191-126">然後您的客戶會連接到您的網路。</span><span class="sxs-lookup"><span data-stu-id="4b191-126">Then your customer connects to your network.</span></span> <span data-ttu-id="4b191-127">此案例需要客戶通過 CSP 網路來存取 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="4b191-127">This scenario requires that the customer passes through the CSP network to access Azure services.</span></span> 

<span data-ttu-id="4b191-128">如果您的客戶有其他不受您管理的 Azure 訂用帳戶，他們會使用公用網際網路或自己的私人連線來連接到非 CSP 訂用帳戶下所佈建的這些服務。</span><span class="sxs-lookup"><span data-stu-id="4b191-128">If your customer has other Azure subscriptions not managed by the you, they would use the public Internet or their own private connection to connect to those services provisioned under the non CSP subscription.</span></span> 

<span data-ttu-id="4b191-129">對於管理 Azure 服務的 CSP，假設此 CSP 有先前建立的客戶身分識別存放區，該存放區之後會複寫到 Azure Active Directory 中，以便透過 Administrate-On-Behalf-Of (AOBO) 管理其 CSP 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="4b191-129">For CSP managing Azure services, it is assumed that the CSP has a previously established customer identity store which would then be replicated into Azure Active Directory for management of their CSP subscription through Administrate-On-Behalf-Of (AOBO).</span></span> <span data-ttu-id="4b191-130">此案例的關鍵驅動因素包括特定的夥伴或服務提供者已建立起與客戶的關聯性、客戶目前使用提供者服務，或夥伴想要提供由提供者裝載和由 Azure 裝載的解決方案組合，以提供彈性及解決 CSP 無法單獨滿足的客戶挑戰。</span><span class="sxs-lookup"><span data-stu-id="4b191-130">Key drivers for this scenario include where a given partner or service provider has an established relationship with the customer, the customer is consuming provider services currently or the partner has a desire to provide a combination of provider-hosted and Azure-hosted solutions to provide flexibility and address customer challenges which cannot be satisfied by CSP alone.</span></span> <span data-ttu-id="4b191-131">此模型如下 **圖**所說明。</span><span class="sxs-lookup"><span data-stu-id="4b191-131">This model is illustrated in **Figure**, below.</span></span>

![替代文字](./media/expressroute-for-cloud-solution-providers/connect-through-model.png)

### <a name="connect-to-model"></a><span data-ttu-id="4b191-133">Connect-To 模型</span><span class="sxs-lookup"><span data-stu-id="4b191-133">Connect-to model</span></span>
![替代文字](./media/expressroute-for-cloud-solution-providers/connect-to.png)

<span data-ttu-id="4b191-135">在 Connect-To 模型中，服務提供者會使用 ExpressRoute 透過客戶的 (客戶) 網路，在其客戶的資料中心與 CSP 佈建的 Azure 訂用帳戶之間建立直接連線。</span><span class="sxs-lookup"><span data-stu-id="4b191-135">In the Connect-To model, the service provider creates a direct connection between their customer’s datacenter and the CSP provisioned Azure subscription using ExpressRoute over the customer’s (customer) network.</span></span>

> [!NOTE]
> <span data-ttu-id="4b191-136">在 ExpressRoute 中，客戶需要建立和維護 ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="4b191-136">For ExpressRoute the customer would need to create and maintain the ExpressRoute circuit.</span></span>  
> 
> 

<span data-ttu-id="4b191-137">此連線案例需要客戶使用全部或部分由客戶建立、擁有和管理的直接網路連線，透過客戶網路直接連接，以存取 CSP 管理的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="4b191-137">This connectivity scenario requires that the customer connects directly through a customer network to access CSP-managed Azure subscription, using a direct network connection that is created, owned and managed either wholly or in part by the customer.</span></span> <span data-ttu-id="4b191-138">對於這些客戶，假設提供者目前並沒有已建立的客戶身分識別存放區，且提供者會協助客戶將其目前的身分識別存放區複寫到 Azure Active Directory 中，以便透過 AOBO 管理其訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="4b191-138">For these customers it is assumed that the provider does not currently have a customer identity store established, and the provider would assist the customer in replicating their current identify store into Azure Active Directory for management of their subscription through AOBO.</span></span> <span data-ttu-id="4b191-139">此案例的關鍵驅動因素包括特定的夥伴或服務提供者已建立起與客戶的關聯性、客戶目前使用提供者服務，或夥伴想要提供單獨以 Azure 裝載的解決方案為基礎的服務，而不需要現有的提供者資料中心或基礎結構。</span><span class="sxs-lookup"><span data-stu-id="4b191-139">Key drivers for this scenario include where a given partner or service provider has an established relationship with the customer, the customer is consuming provider services currently, or the partner has a desire to provide services that are based solely on Azure-hosted solutions without the need for an existing provider datacenter or infrastructure.</span></span>

![替代文字](./media/expressroute-for-cloud-solution-providers/connect-to-model.png)

<span data-ttu-id="4b191-141">這兩個選項之間的選擇依據是客戶的需求以及您目前提供 Azure 服務的需求。</span><span class="sxs-lookup"><span data-stu-id="4b191-141">The choice between these two option are based on your customer’s needs and your current need to provide Azure services.</span></span> <span data-ttu-id="4b191-142">下列連結涵蓋這些模型的詳細資料，以及相關聯的角色型存取控制、網路和身分識別設計模式︰</span><span class="sxs-lookup"><span data-stu-id="4b191-142">The details of these models and the associated role-based access control, networking, and identity design patterns are covered in details in the following links:</span></span>

* <span data-ttu-id="4b191-143">**角色型存取控制 (RBAC)** – RBAC 是以 Azure Active Directory 為基礎。</span><span class="sxs-lookup"><span data-stu-id="4b191-143">**Role Based Access Control (RBAC)** – RBAC is based on Azure Active Directory.</span></span>  <span data-ttu-id="4b191-144">如需 Azure RBAC 的詳細資訊，請參閱 [這裡](../active-directory/role-based-access-control-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="4b191-144">For more information on Azure RBAC see [here](../active-directory/role-based-access-control-configure.md).</span></span>
* <span data-ttu-id="4b191-145">**網路** – 涵蓋 Microsoft Azure 中的各種網路主題。</span><span class="sxs-lookup"><span data-stu-id="4b191-145">**Networking** – Covers the various topics of networking in Microsoft Azure.</span></span>
* <span data-ttu-id="4b191-146">**Azure Active Directory (AAD)** – AAD 提供 Microsoft Azure 和第三方 SaaS 應用程式的身分識別管理。</span><span class="sxs-lookup"><span data-stu-id="4b191-146">**Azure Active Directory (AAD)** – AAD provides the identity management for Microsoft Azure and 3rd party SaaS applications.</span></span> <span data-ttu-id="4b191-147">如需有關 Azure AD 的詳細資訊，請參閱 [這裡](https://azure.microsoft.com/documentation/services/active-directory/)。</span><span class="sxs-lookup"><span data-stu-id="4b191-147">For more information about Azure AD see [here](https://azure.microsoft.com/documentation/services/active-directory/).</span></span>  

## <a name="network-speeds"></a><span data-ttu-id="4b191-148">網路速度</span><span class="sxs-lookup"><span data-stu-id="4b191-148">Network speeds</span></span>
<span data-ttu-id="4b191-149">ExpressRoute 支援 50 Mb/s 至 10 Gb/s 的網路速度。</span><span class="sxs-lookup"><span data-stu-id="4b191-149">ExpressRoute supports network speeds from 50 Mb/s to 10Gb/s.</span></span> <span data-ttu-id="4b191-150">這可讓客戶購買其獨特環境所需的網路頻寬量。</span><span class="sxs-lookup"><span data-stu-id="4b191-150">This allows customers to purchase the amount of network bandwidth needed for their unique environment.</span></span>

> [!NOTE]
> <span data-ttu-id="4b191-151">您可以在不干擾通訊的情況下，視需要增加網路頻寬，但若要降低網路速度，則需拆解電路並以較低的網路速度加以重建。</span><span class="sxs-lookup"><span data-stu-id="4b191-151">Network bandwidth can be increased as needed without disrupting communications, but to reduce the network speed requires tearing down the circuit and recreating it at the lower network speed.</span></span>  
> 
> 

<span data-ttu-id="4b191-152">ExpressRoute 支援多個 vNet 至單一 ExpressRoute 電路的連線，以便更加妥善利用高速連線。</span><span class="sxs-lookup"><span data-stu-id="4b191-152">ExpressRoute supports the connection of multiple vNets to a single ExpressRoute circuit for better utilization of the higher-speed connections.</span></span> <span data-ttu-id="4b191-153">同一個客戶所擁有的多個 Azure 訂用帳戶可以共用單一 ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="4b191-153">A single ExpressRoute circuit can be shared among multiple Azure subscriptions owned by the same customer.</span></span>

## <a name="configuring-expressroute"></a><span data-ttu-id="4b191-154">設定 ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="4b191-154">Configuring ExpressRoute</span></span>
<span data-ttu-id="4b191-155">ExpressRoute 可設定為透過單一 ExpressRoute 電路支援三種類型的流量 ([路由網域](#ExpressRoute-routing-domains))。</span><span class="sxs-lookup"><span data-stu-id="4b191-155">ExpressRoute can be configured to support three types of traffic ([routing domains](#ExpressRoute-routing-domains)) over a single ExpressRoute circuit.</span></span> <span data-ttu-id="4b191-156">此流量可以分成 Microsoft 對等、Azure 公用對等和私用對等。</span><span class="sxs-lookup"><span data-stu-id="4b191-156">This traffic is segregated into Microsoft peering, Azure public peering and private peering.</span></span> <span data-ttu-id="4b191-157">視 ExpressRoute 電路的大小和您的客戶所需的隔離而定，您可以選擇透過單一 ExpressRoute 電路傳送一個或所有類型的流量，或使用多個 ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="4b191-157">You can choose one or all types of traffic to be sent over a single ExpressRoute circuit or use multiple ExpressRoute circuits depending on the size of the ExpressRoute circuit and isolation required by your customer.</span></span> <span data-ttu-id="4b191-158">您的客戶的安全狀態可能不允許公用流量和私用流量透過相同的電路周遊。</span><span class="sxs-lookup"><span data-stu-id="4b191-158">The security posture of your customer may not allow public traffic and private traffic to traverse over the same circuit.</span></span>

### <a name="connect-through-model"></a><span data-ttu-id="4b191-159">Connect-Through 模型</span><span class="sxs-lookup"><span data-stu-id="4b191-159">Connect-through model</span></span>
<span data-ttu-id="4b191-160">在 Connect-Through 組態中，您會負責所有網路基礎，以將客戶資料中心資源連接到 Azure 中裝載的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="4b191-160">In a connect-through configuration the you will be responsible for all of the networking underpinnings to connect your customers datacenter resources to the subscriptions hosted in Azure.</span></span> <span data-ttu-id="4b191-161">每個想要使用 Azure 功能的客戶都需有自己的 ExpressRoute 連線 (將由您管理)。</span><span class="sxs-lookup"><span data-stu-id="4b191-161">Each of your customer's that want to use Azure capabilities will need their own ExpressRoute connection, which will be managed by the You.</span></span> <span data-ttu-id="4b191-162">您將使用客戶用來購買 ExpressRoute 電路的相同方法。</span><span class="sxs-lookup"><span data-stu-id="4b191-162">The you will use the same methods the customer would use to procure the ExpressRoute circuit.</span></span> <span data-ttu-id="4b191-163">您將依照 [ExpressRoute 電路佈建和電路狀態工作流程](expressroute-workflows.md) 一文中所述的相同步驟執行。</span><span class="sxs-lookup"><span data-stu-id="4b191-163">The you will follow the same steps outlined in the article [ExpressRoute workflows](expressroute-workflows.md) for circuit provisioning and circuit states.</span></span> <span data-ttu-id="4b191-164">接著，您將設定邊界閘道協定 (BGP) 路由來控制在內部部署網路與 Azure vNet 之間流動的流量。</span><span class="sxs-lookup"><span data-stu-id="4b191-164">The you will then configure the Border Gateway Protocol (BGP) routes to control the traffic flowing between the on-premises network and Azure vNet.</span></span>

### <a name="connect-to-model"></a><span data-ttu-id="4b191-165">Connect-To 模型</span><span class="sxs-lookup"><span data-stu-id="4b191-165">Connect-to model</span></span>
<span data-ttu-id="4b191-166">在 Connect-To 組態中，您的客戶已經有 Azure 連線，或者會起始對網際網路服務提供者的連線，以將 ExpressRoute 從您的客戶擁有的資料中心直接連結至 Azure，而不是您的資料中心。</span><span class="sxs-lookup"><span data-stu-id="4b191-166">In a connect-to configuration, your customer already has an existing connection to Azure or will initiate a connection to the internet service provider linking ExpressRoute from your customer’s own datacenter directly to Azure, instead of your datacenter.</span></span> <span data-ttu-id="4b191-167">若要開始佈建程序，您的客戶將依照上面 Connect-Through 模型中所述的步驟執行。</span><span class="sxs-lookup"><span data-stu-id="4b191-167">To begin the provisioning process, your customer will follow the steps as described in the Connect-Through model, above.</span></span> <span data-ttu-id="4b191-168">一旦建立電路，您的客戶必須設定內部部署路由器，才能存取您的網路和 Azure vNnet。</span><span class="sxs-lookup"><span data-stu-id="4b191-168">Once the circuit has been established your customer will need to configure the on-premises routers to be able to access both your network and Azure vNets.</span></span>

<span data-ttu-id="4b191-169">您可以設定連接及設定路由，允許您資料中心的資源與您資料中心的用戶端資源進行通訊，或與 Azure 中裝載的資源進行通訊。</span><span class="sxs-lookup"><span data-stu-id="4b191-169">You can assist with setting up the connection and configuring the routes to allow the resources in your datacenter(s) to communicate with the client resources in your datacenter, or with the resources hosted in Azure.</span></span>

## <a name="expressroute-routing-domains"></a><span data-ttu-id="4b191-170">ExpressRoute 路由網域</span><span class="sxs-lookup"><span data-stu-id="4b191-170">ExpressRoute routing domains</span></span>
<span data-ttu-id="4b191-171">ExpressRoute 提供三種路由網域︰公用、私用和 Microsoft 對等。</span><span class="sxs-lookup"><span data-stu-id="4b191-171">ExpressRoute offers three routing domains: public, private, and Microsoft peering.</span></span> <span data-ttu-id="4b191-172">每個路由網域都是使用主動-主動組態中完全相同的路由器設定，以提供高可用性。</span><span class="sxs-lookup"><span data-stu-id="4b191-172">Each of the routing domains are configured with identical routers in active-active configuration for high availability.</span></span> <span data-ttu-id="4b191-173">如需 ExpressRoute 路由網域的詳細資訊，請參閱 [這裡](expressroute-circuit-peerings.md)。</span><span class="sxs-lookup"><span data-stu-id="4b191-173">For more details on ExpressRoute routing domains look [here](expressroute-circuit-peerings.md).</span></span>

<span data-ttu-id="4b191-174">您可以定義自訂路由篩選器，只允許您想允許或需要的路由。</span><span class="sxs-lookup"><span data-stu-id="4b191-174">You can define custom routes filters to allow only the route(s) you want to allow or need.</span></span> <span data-ttu-id="4b191-175">如需詳細資訊或了解如何進行這些變更，請參閱以下文章︰ [使用 PowerShell 建立和修改 ExpressRoute 電路的路由](expressroute-howto-routing-classic.md) ，以取得路由篩選器的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="4b191-175">For more information or to see how to make these changes see article: [Create and modify routing for an ExpressRoute circuit using PowerShell](expressroute-howto-routing-classic.md) for more details about routing filters.</span></span>

> [!NOTE]
> <span data-ttu-id="4b191-176">若為 Microsoft 和公用對等，連線必須是客戶或 CSP 所擁有的公用 IP 位址，而且必須遵守所有定義的規則。</span><span class="sxs-lookup"><span data-stu-id="4b191-176">For Microsoft and Public Peering connectivity must be though a public IP address owned by the customer or CSP and must adhere to all defined rules.</span></span> <span data-ttu-id="4b191-177">如需詳細資訊，請參閱 [ExpressRoute 必要條件](expressroute-prerequisites.md) 頁面。</span><span class="sxs-lookup"><span data-stu-id="4b191-177">For more information, see the [ExpressRoute Prerequisites](expressroute-prerequisites.md) page.</span></span>  
> 
> 

## <a name="routing"></a><span data-ttu-id="4b191-178">路由</span><span class="sxs-lookup"><span data-stu-id="4b191-178">Routing</span></span>
<span data-ttu-id="4b191-179">ExpressRoute 會透過 Azure 虛擬網路閘道連接到 Azure 網路。</span><span class="sxs-lookup"><span data-stu-id="4b191-179">ExpressRoute connects to the Azure networks through the Azure Virtual Network Gateway.</span></span> <span data-ttu-id="4b191-180">網路閘道提供 Azure 虛擬網路的路由。</span><span class="sxs-lookup"><span data-stu-id="4b191-180">Network gateways provide routing for Azure virtual networks.</span></span>

<span data-ttu-id="4b191-181">建立 Azure 虛擬網路時，也會建立 vNet 的預設路由表，以便從 vNet 的子網路雙向導引流量。</span><span class="sxs-lookup"><span data-stu-id="4b191-181">Creating Azure Virtual Networks also creates a default routing table for the vNet to direct traffic to/from the subnets of the vNet.</span></span> <span data-ttu-id="4b191-182">如果預設路由表不敷解決方案使用，可以建立自訂路由，將連出流量路由傳送至自訂應用裝置，或封鎖對特定子網路或外部網路的路由。</span><span class="sxs-lookup"><span data-stu-id="4b191-182">If the default route table is insufficient for the solution custom routes can be created to route outgoing traffic to custom appliances or to block routes to specific subnets or external networks.</span></span>

### <a name="default-routing"></a><span data-ttu-id="4b191-183">預設路由</span><span class="sxs-lookup"><span data-stu-id="4b191-183">Default routing</span></span>
<span data-ttu-id="4b191-184">預設路由表包含下列路由：</span><span class="sxs-lookup"><span data-stu-id="4b191-184">The default route table includes the following routes:</span></span>

* <span data-ttu-id="4b191-185">子網路內的路由</span><span class="sxs-lookup"><span data-stu-id="4b191-185">Routing within a subnet</span></span>
* <span data-ttu-id="4b191-186">虛擬網路內的子網路對子網路路由</span><span class="sxs-lookup"><span data-stu-id="4b191-186">Subnet-to-subnet within the virtual network</span></span>
* <span data-ttu-id="4b191-187">對網際網路的路由</span><span class="sxs-lookup"><span data-stu-id="4b191-187">To the Internet</span></span>
* <span data-ttu-id="4b191-188">使用 VPN 閘道的虛擬網路對虛擬網路路由</span><span class="sxs-lookup"><span data-stu-id="4b191-188">Virtual network-to-virtual network using VPN gateway</span></span>
* <span data-ttu-id="4b191-189">使用 VPN 或 ExpressRoute 閘道的虛擬網路對內部部署網路路由</span><span class="sxs-lookup"><span data-stu-id="4b191-189">Virtual network-to-on-premises network using a VPN or ExpressRoute gateway</span></span>

![替代文字](./media/expressroute-for-cloud-solution-providers/default-routing.png)  

### <a name="user-defined-routing-udr"></a><span data-ttu-id="4b191-191">使用者定義的路由 (UDR)</span><span class="sxs-lookup"><span data-stu-id="4b191-191">User-defined routing (UDR)</span></span>
<span data-ttu-id="4b191-192">使用者定義的路由能夠控制從虛擬網路中指派的子網路輸出至其他子網路的流量，或透過其中一個其他預先定義的閘道 (ExpressRoute、網際網路或 VPN) 輸出的流量。</span><span class="sxs-lookup"><span data-stu-id="4b191-192">User-defined routes allow the control of traffic outbound from the assigned subnet to other subnets in the virtual network or over one of the other predefined gateways (ExpressRoute; internet or VPN).</span></span> <span data-ttu-id="4b191-193">使用者定義的路由表可以取代預設的系統路由表，其以自訂路由取代預設的路由表。</span><span class="sxs-lookup"><span data-stu-id="4b191-193">The default system routing table can be replaced with a user-defined routing table that replaces the default routing table with custom routes.</span></span> <span data-ttu-id="4b191-194">利用使用者定義的路由，客戶可以建立對應用裝置 (例如防火牆或入侵偵測應用裝置) 的特定路由，或封鎖從裝載使用者定義之路由的子網路對特定子網路的存取。</span><span class="sxs-lookup"><span data-stu-id="4b191-194">With user-defined routing, customers can create specific routes to appliances such as firewalls or intrusion detection appliances, or block access to specific subnets from the subnet hosting the user-defined route.</span></span> <span data-ttu-id="4b191-195">如需使用者定義的路由概觀，請參閱 [這裡](../virtual-network/virtual-networks-udr-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="4b191-195">For an overview of User Defined Routes look [here](../virtual-network/virtual-networks-udr-overview.md).</span></span> 

## <a name="security"></a><span data-ttu-id="4b191-196">Security</span><span class="sxs-lookup"><span data-stu-id="4b191-196">Security</span></span>
<span data-ttu-id="4b191-197">視正在使用中的模型 (Connect-To 或 Connect-Through) 而定，您的客戶會在其 vNet 中定義安全性原則，或提供安全性原則需求給 CSP 來定義其 vNet。</span><span class="sxs-lookup"><span data-stu-id="4b191-197">Depending on which model is in use, Connect-To or Connect-Through, your customer defines the security policies in their vNet or provides the security policy requirements to the CSP to define to their vNets.</span></span> <span data-ttu-id="4b191-198">可以定義下列安全性準則︰</span><span class="sxs-lookup"><span data-stu-id="4b191-198">The following security criteria can be defined:</span></span>

1. <span data-ttu-id="4b191-199">**客戶隔離** — Azure 平台會將客戶識別碼和 vNet 資訊儲存在安全的資料庫中 (用來封裝 GRE 通道中每個客戶的流量)，藉此提供客戶隔離。</span><span class="sxs-lookup"><span data-stu-id="4b191-199">**Customer Isolation** — The Azure platform provides customer isolation by storing Customer ID and vNet info in a secure database, which is used to encapsulate each customer’s traffic in a GRE tunnel.</span></span>
2. <span data-ttu-id="4b191-200">**網路安全性群組 (NSG)** 規則用於定義在 Azure 中傳入和傳出 vNet 子網路的流量。</span><span class="sxs-lookup"><span data-stu-id="4b191-200">**Network Security Group (NSG)** rules are for defining allowed traffic into and out of the subnets within vNets in Azure.</span></span> <span data-ttu-id="4b191-201">根據預設，NSG 包含封鎖規則和允許規則，前者可封鎖從網際網路至 vNet 的流量，後者適用於 vNet 內的流量。</span><span class="sxs-lookup"><span data-stu-id="4b191-201">By default, the NSG contain Block rules to block traffic from the Internet to the vNet and Allow rules for traffic within a vNet.</span></span> <span data-ttu-id="4b191-202">如需網路安全性群組的詳細資訊，請參閱 [這裡](https://azure.microsoft.com/blog/network-security-groups/)。</span><span class="sxs-lookup"><span data-stu-id="4b191-202">For more information about Network Security Groups look [here](https://azure.microsoft.com/blog/network-security-groups/).</span></span>
3. <span data-ttu-id="4b191-203">**強制通道** — 這個選項可透過 ExpressRoute 連線，將源自於 Azure 的網際網路繫結流量重新導向至內部部署資料中心。</span><span class="sxs-lookup"><span data-stu-id="4b191-203">**Force tunneling** —This is an option to redirect internet bound traffic originating in Azure to be redirected over the ExpressRoute connection to the on premises datacenter.</span></span> <span data-ttu-id="4b191-204">如需強制通道的詳細資訊，請參閱 [這裡](expressroute-routing.md#advertising-default-routes)。</span><span class="sxs-lookup"><span data-stu-id="4b191-204">For more information about Forced tunneling look [here](expressroute-routing.md#advertising-default-routes).</span></span>  
4. <span data-ttu-id="4b191-205">**加密** — 即使 ExpressRoute 電路專用於特定客戶，網路提供者仍可能違反規定，讓入侵者檢查封包流量。</span><span class="sxs-lookup"><span data-stu-id="4b191-205">**Encryption** — Even though the ExpressRoute circuits are dedicated to a specific customer, there is the possibility that the network provider could be breached, allowing an intruder to examine packet traffic.</span></span> <span data-ttu-id="4b191-206">若要解決這個可能性，客戶或 CSP 可以針對在內部部署資源與 Azure 資源之間流動的所有流量，定義 IPSec 通道模式原則，進而將透過連線的流量加密 (請參閱上面圖 5：ExpressRoute 安全性中客戶 1 的選擇性通道模式 IPSec)。</span><span class="sxs-lookup"><span data-stu-id="4b191-206">To address this potential, a customer or CSP can encrypt traffic over the connection by defining IPSec tunnel-mode policies for all traffic flowing between the on premises resources and Azure resources (refer to the optional Tunnel mode IPSec for Customer 1 in Figure 5: ExpressRoute Security, above).</span></span> <span data-ttu-id="4b191-207">第二個選項是在 ExpressRoute 電路的每個端點使用防火牆應用裝置。</span><span class="sxs-lookup"><span data-stu-id="4b191-207">The second option would be to use a firewall appliance at each the end point of the ExpressRoute circuit.</span></span> <span data-ttu-id="4b191-208">這需要兩端都安裝額外的第三方防火牆 VM/應用裝置，才能將透過 ExpressRoute 電路的流量加密。</span><span class="sxs-lookup"><span data-stu-id="4b191-208">This will require additional 3rd party firewall VMs/Appliances to be installed on both ends to encrypt the traffic over the ExpressRoute circuit.</span></span>

![替代文字](./media/expressroute-for-cloud-solution-providers/expressroute-security.png)  

## <a name="next-steps"></a><span data-ttu-id="4b191-210">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4b191-210">Next steps</span></span>
<span data-ttu-id="4b191-211">雲端解決方案提供者服務可讓您提升您對於客戶的價值，而不需要購買昂貴的基礎結構和功能，同時讓您維持主要外包提供者的地位。</span><span class="sxs-lookup"><span data-stu-id="4b191-211">The Cloud Solution Provider service provides you a way to increase your value to your customers without the need for expensive infrastructure and capability purchases, while maintaining your position as the primary outsourcing provider.</span></span> <span data-ttu-id="4b191-212">透過 CSP API 可達成與 Microsoft Azure 的緊密整合，讓您將 Microsoft Azure 的管理整合在現有的管理架構內。</span><span class="sxs-lookup"><span data-stu-id="4b191-212">Seamless integration with Microsoft Azure can be accomplished through the CSP API, allowing you to integrate management of Microsoft Azure within your existing management frameworks.</span></span>  

<span data-ttu-id="4b191-213">在下列連結中可以找到額外的資訊︰</span><span class="sxs-lookup"><span data-stu-id="4b191-213">Additional Information can be found at the following links:</span></span>

<span data-ttu-id="4b191-214">[Microsoft Cloud 解決方案提供者方案](https://partner.microsoft.com/en-US/Solutions/cloud-reseller-overview)。</span><span class="sxs-lookup"><span data-stu-id="4b191-214">[Microsoft Cloud Solution Provider program](https://partner.microsoft.com/en-US/Solutions/cloud-reseller-overview).</span></span>  
<span data-ttu-id="4b191-215">[做好準備以雲端解決方案提供者身分交易](https://partner.microsoft.com/en-us/solutions/cloud-reseller-pre-launch)。</span><span class="sxs-lookup"><span data-stu-id="4b191-215">[Get ready to transact as a Cloud Solution Provider](https://partner.microsoft.com/en-us/solutions/cloud-reseller-pre-launch).</span></span>  
<span data-ttu-id="4b191-216">[Microsoft Cloud 解決方案提供者資源](https://partner.microsoft.com/en-us/solutions/cloud-reseller-resources)。</span><span class="sxs-lookup"><span data-stu-id="4b191-216">[Microsoft Cloud Solution Provider resources](https://partner.microsoft.com/en-us/solutions/cloud-reseller-resources).</span></span>
