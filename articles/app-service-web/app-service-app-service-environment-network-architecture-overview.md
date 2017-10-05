---
title: "App Service 環境的網路架構概觀"
description: "App Service 環境網路拓撲的架構概觀。"
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: 13d03a37-1fe2-4e3e-9d57-46dfb330ba52
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/04/2016
ms.author: stefsch
ms.openlocfilehash: b2afe86d8774b449a257312d4e60b5f6125336ca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="network-architecture-overview-of-app-service-environments"></a><span data-ttu-id="6e4ae-103">App Service 環境的網路架構概觀</span><span class="sxs-lookup"><span data-stu-id="6e4ae-103">Network Architecture Overview of App Service Environments</span></span>
## <a name="introduction"></a><span data-ttu-id="6e4ae-104">簡介</span><span class="sxs-lookup"><span data-stu-id="6e4ae-104">Introduction</span></span>
<span data-ttu-id="6e4ae-105">App Service 環境一律建立於[虛擬網路][virtualnetwork] - 的子網路內，而在 App Service 環境中執行的應用程式可以與相同虛擬網路拓撲內的私用端點通訊。</span><span class="sxs-lookup"><span data-stu-id="6e4ae-105">App Service Environments are always created within a subnet of a [virtual network][virtualnetwork] - apps running in an App Service Environment can communicate with private endpoints located within the same virtual network topology.</span></span>  <span data-ttu-id="6e4ae-106">因為客戶可能會鎖定其虛擬網路基礎結構的組件，所以請務必了解與 App Service 環境發生的網路通訊流程類型。</span><span class="sxs-lookup"><span data-stu-id="6e4ae-106">Since customers may lock down parts of their virtual network infrastructure, it is important to understand the types of network communication flows that occur with an App Service Environment.</span></span>

## <a name="general-network-flow"></a><span data-ttu-id="6e4ae-107">一般網路流程</span><span class="sxs-lookup"><span data-stu-id="6e4ae-107">General Network Flow</span></span>
<span data-ttu-id="6e4ae-108">當 App Service 環境 (ASE) 針對應用程式使用公開虛擬 IP 位址 (VIP) 時，所有傳入的流量都會到達該公用 VIP。</span><span class="sxs-lookup"><span data-stu-id="6e4ae-108">When an App Service Environment (ASE) uses a public virtual IP address (VIP) for apps, all inbound traffic arrives on that public VIP.</span></span>  <span data-ttu-id="6e4ae-109">這包括應用程式的 HTTP 和 HTTPS 流量，以及 FTP 的其他流量、遠端偵錯功能和 Azure 管理作業。</span><span class="sxs-lookup"><span data-stu-id="6e4ae-109">This includes HTTP and HTTPS traffic for apps, as well as other traffic for FTP, remote debugging functionality, and Azure management operations.</span></span>  <span data-ttu-id="6e4ae-110">如需公用 VIP 上可用特定連接埠 (必要和選擇性) 的完整清單，請參閱有關[控制輸入流量][controllinginboundtraffic]至 App Service 環境的文章。</span><span class="sxs-lookup"><span data-stu-id="6e4ae-110">For a full list of the specific ports (both required and optional) that are available on the public VIP see the article on [controlling inbound traffic][controllinginboundtraffic] to an App Service Environment.</span></span> 

<span data-ttu-id="6e4ae-111">App Service 環境也支援執行僅繫結至虛擬網路內部位址，也稱為 ILB (內部負載平衡器) 位址的應用程式。</span><span class="sxs-lookup"><span data-stu-id="6e4ae-111">App Service Environments also support running apps that are bound only to a virtual network internal address, also referred to as an ILB (internal load balancer) address.</span></span>  <span data-ttu-id="6e4ae-112">在已啟用 ILB 的 ASE 上，應用程式的 HTTP 和 HTTPS 流量以及遠端偵錯呼叫會送達 ILB 位址。</span><span class="sxs-lookup"><span data-stu-id="6e4ae-112">On an ILB enabled ASE, HTTP and HTTPS traffic for apps as well as remote debugging calls, arrive on the ILB address.</span></span>  <span data-ttu-id="6e4ae-113">針對大部分的 ILB-ASE 組態，FTP/FTPS 流量也會送達 ILB 位址。</span><span class="sxs-lookup"><span data-stu-id="6e4ae-113">For most common ILB-ASE configurations, FTP/FTPS traffic will also arrive on the ILB address.</span></span>  <span data-ttu-id="6e4ae-114">不過，Azure 管理作業仍會流向公用 VIP (屬於已啟用 ILB 的 ASE) 上的連接埠 454/455。</span><span class="sxs-lookup"><span data-stu-id="6e4ae-114">However Azure management operations will still flow to ports 454/455 on the public VIP of an ILB enabled ASE.</span></span>

<span data-ttu-id="6e4ae-115">下圖顯示 App Service 環境的各種傳入和傳出網路流量的概觀，其中應用程式是繫結至公用虛擬 IP 位址：</span><span class="sxs-lookup"><span data-stu-id="6e4ae-115">The diagram below shows an overview of the various inbound and outbound network flows for an App Service Environment where the apps are bound to a public virtual IP address:</span></span>

![一般網路流程][GeneralNetworkFlows]

<span data-ttu-id="6e4ae-117">App Service 環境可以與各種私用客戶端點進行通訊。</span><span class="sxs-lookup"><span data-stu-id="6e4ae-117">An App Service Environment can communicate with a variety of private customer endpoints.</span></span>  <span data-ttu-id="6e4ae-118">例如，在 App Service 環境中執行的應用程式可以連線至在相同虛擬網路拓撲之 IaaS 虛擬機器上執行的資料庫伺服器。</span><span class="sxs-lookup"><span data-stu-id="6e4ae-118">For example, apps running in the App Service Environment can connect to database server(s) running on IaaS virtual machines in the same virtual network topology.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6e4ae-119">請查看網狀圖，「其他計算資源」會部署在與 App Service 環境不同的子網路中。</span><span class="sxs-lookup"><span data-stu-id="6e4ae-119">Looking at the network diagram, the "Other Compute Resources" are deployed in a different Subnet from the App Service Environment.</span></span> <span data-ttu-id="6e4ae-120">將資源部署於和 ASE 相同的子網路中，會封鎖從 ASE 連線到這些資源的連線 (除了特定的內部 ASE 路由之外)。</span><span class="sxs-lookup"><span data-stu-id="6e4ae-120">Deploying resources in the same Subnet with the ASE will block connectivity from ASE to those resources (except for specific intra-ASE routing).</span></span> <span data-ttu-id="6e4ae-121">請改為部署到 (相同 VNET 中) 不同的子網路。</span><span class="sxs-lookup"><span data-stu-id="6e4ae-121">Deploy to a different Subnet instead (in the same VNET).</span></span> <span data-ttu-id="6e4ae-122">App Service 環境就能連線。</span><span class="sxs-lookup"><span data-stu-id="6e4ae-122">The App Service Environment will then be able to connect.</span></span> <span data-ttu-id="6e4ae-123">不需要任何其他設定。</span><span class="sxs-lookup"><span data-stu-id="6e4ae-123">No additional configuration is necessary.</span></span>
> 
> 

<span data-ttu-id="6e4ae-124">App Service 環境也會與管理和操作 App Service 環境所需的 SQL 資料庫和 Azure 儲存體資源進行通訊。</span><span class="sxs-lookup"><span data-stu-id="6e4ae-124">App Service Environments also communicate with Sql DB and Azure Storage resources necessary for managing and operating an App Service Environment.</span></span>  <span data-ttu-id="6e4ae-125">App Service 環境與之通訊的一些 SQL 和儲存體資源位於與 App Service 環境相同的區域中，有些則位於遠端 Azure 區域中。</span><span class="sxs-lookup"><span data-stu-id="6e4ae-125">Some of the Sql and Storage resources that an App Service Environment communicates with are located in the same region as the App Service Environment, while others are located in remote Azure regions.</span></span>  <span data-ttu-id="6e4ae-126">因此，一律需要到網際網路的輸出連線，App Service 環境才能正常運作。</span><span class="sxs-lookup"><span data-stu-id="6e4ae-126">As a result, outbound connectivity to the Internet is always required for an App Service Environment to function properly.</span></span> 

<span data-ttu-id="6e4ae-127">因為在子網路中部署 App Service 環境，所以可以使用網路安全性群組來控制對子網路的輸入流量。</span><span class="sxs-lookup"><span data-stu-id="6e4ae-127">Since an App Service Environment is deployed in a subnet, network security groups can be used to control inbound traffic to the subnet.</span></span>  <span data-ttu-id="6e4ae-128">如需如何控制對 App Service 環境之輸入流量的詳細資料，請參閱下列[文章][controllinginboundtraffic]。</span><span class="sxs-lookup"><span data-stu-id="6e4ae-128">For details on how to control inbound traffic to an App Service Environment, see the following [article][controllinginboundtraffic].</span></span>

<span data-ttu-id="6e4ae-129">如需如何允許來自 App Service 環境之輸出網際網路連線的詳細資料，請參閱下列有關使用 [Express Route][ExpressRoute] 的文章。</span><span class="sxs-lookup"><span data-stu-id="6e4ae-129">For details on how to allow outbound Internet connectivity from an App Service Environment, see the following article about working with [Express Route][ExpressRoute].</span></span>  <span data-ttu-id="6e4ae-130">本文所述的相同方法適用於使用站對連線以及使用強制通道時。</span><span class="sxs-lookup"><span data-stu-id="6e4ae-130">The same approach described in the article applies when working with Site-to-Site connectivity and using forced tunneling.</span></span>

## <a name="outbound-network-addresses"></a><span data-ttu-id="6e4ae-131">輸出網路位址</span><span class="sxs-lookup"><span data-stu-id="6e4ae-131">Outbound Network Addresses</span></span>
<span data-ttu-id="6e4ae-132">App Service 環境進行輸出呼叫時，IP 位址一律會與輸出呼叫相關聯。</span><span class="sxs-lookup"><span data-stu-id="6e4ae-132">When an App Service Environment makes outbound calls, an IP Address is always associated with the outbound calls.</span></span>  <span data-ttu-id="6e4ae-133">使用的特定 IP 位址取決於所呼叫的端點位於虛擬網路拓撲內部還是外部。</span><span class="sxs-lookup"><span data-stu-id="6e4ae-133">The specific IP address that is used depends on whether the endpoint being called is located within the virtual network topology, or outside of the virtual network topology.</span></span>

<span data-ttu-id="6e4ae-134">如果所呼叫的端點是在虛擬網路拓撲 **外部** ，則使用的輸出位址 (也稱為輸出 NAT 位址) 是 App Service 環境的公用 VIP。</span><span class="sxs-lookup"><span data-stu-id="6e4ae-134">If the endpoint being called is **outside** of the virtual network topology, then the outbound address (aka the outbound NAT address) that is used is the public VIP of the App Service Environment.</span></span>  <span data-ttu-id="6e4ae-135">您可以在 App Service 環境的入口網站的使用者介面中找到此位址 ([屬性] 刀鋒視窗)。</span><span class="sxs-lookup"><span data-stu-id="6e4ae-135">This address can be found in the portal user interface for the App Service Environment in Properties blade.</span></span>

![輸出 IP 位址][OutboundIPAddress]

<span data-ttu-id="6e4ae-137">透過在 App Service 環境中建立應用程式，然後在應用程式的位址上執行 *nslookup* ，也可以針對僅具有公用 VIP 的 ASE 來決定此位址。</span><span class="sxs-lookup"><span data-stu-id="6e4ae-137">This address can also be determined for ASEs that only have a public VIP by creating an app in the App Service Environment, and then performing an *nslookup* on the app's address.</span></span> <span data-ttu-id="6e4ae-138">產生的 IP 位址是公用 VIP，也是 App Service 環境的輸出 NAT 位址。</span><span class="sxs-lookup"><span data-stu-id="6e4ae-138">The resultant IP address is both the public VIP, as well as the App Service Environment's outbound NAT address.</span></span>

<span data-ttu-id="6e4ae-139">如果所呼叫的端點是在虛擬網路拓撲 **內部** ，則呼叫端應用程式的輸出位址會是執行應用程式之個別計算資源的內部 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="6e4ae-139">If the endpoint being called is **inside** of the virtual network topology, the outbound address of the calling app will be the internal IP address of the individual compute resource running the app.</span></span>  <span data-ttu-id="6e4ae-140">不過，虛擬網路內部 IP 位址與應用程式不會有持續性的對應。</span><span class="sxs-lookup"><span data-stu-id="6e4ae-140">However there is not a persistent mapping of virtual network internal IP addresses to apps.</span></span>  <span data-ttu-id="6e4ae-141">應用程式可以在不同的計算資源之間移動，而且可以基於調整作業而變更 App Service 環境中的可用計算資源集區。</span><span class="sxs-lookup"><span data-stu-id="6e4ae-141">Apps can move around across different compute resources, and the pool of available compute resources in an App Service Environment can change due to scaling operations.</span></span>

<span data-ttu-id="6e4ae-142">不過，因為 App Service 環境一律位在子網路內，所以執行應用程式之計算資源的內部 IP 位址保證一律落在子網路的 CIDR 範圍內。</span><span class="sxs-lookup"><span data-stu-id="6e4ae-142">However, since an App Service Environment is always located within a subnet, you are guaranteed that the internal IP address of a compute resource running an app will always lie within the CIDR range of the subnet.</span></span>  <span data-ttu-id="6e4ae-143">因此，使用更細緻的 ACL 或網路安全性群組來保護虛擬網路內其他端點的存取時，需要將存取權授與包含 App Service 環境的子網路範圍。</span><span class="sxs-lookup"><span data-stu-id="6e4ae-143">As a result, when fine-grained ACLs or network security groups are used to secure access to other endpoints within the virtual network, the subnet range containing the App Service Environment needs to be granted access.</span></span>

<span data-ttu-id="6e4ae-144">下圖更詳細說明這些概念：</span><span class="sxs-lookup"><span data-stu-id="6e4ae-144">The following diagram shows these concepts in more detail:</span></span>

![輸出網路位址][OutboundNetworkAddresses]

<span data-ttu-id="6e4ae-146">在上圖中：</span><span class="sxs-lookup"><span data-stu-id="6e4ae-146">In the above diagram:</span></span>

* <span data-ttu-id="6e4ae-147">因為 App Service 環境的公用 VIP 是 192.23.1.2，所以這是呼叫「網域網路」端點時所使用的輸出 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="6e4ae-147">Since the public VIP of the App Service Environment is 192.23.1.2, that is the outbound IP address used when making calls to "Internet" endpoints.</span></span>
* <span data-ttu-id="6e4ae-148">App Service 環境所含子網路的 CIDR 範圍是 10.0.1.0/26。</span><span class="sxs-lookup"><span data-stu-id="6e4ae-148">The CIDR range of the containing subnet for the App Service Environment is 10.0.1.0/26.</span></span>  <span data-ttu-id="6e4ae-149">相同虛擬網路基礎結構內的其他端點，將會看到源自此位址範圍內某處之應用程式的呼叫。</span><span class="sxs-lookup"><span data-stu-id="6e4ae-149">Other endpoints within the same virtual network infrastructure will see calls from apps as originating from somewhere within this address range.</span></span>

## <a name="calls-between-app-service-environments"></a><span data-ttu-id="6e4ae-150">App Service 環境之間的呼叫</span><span class="sxs-lookup"><span data-stu-id="6e4ae-150">Calls Between App Service Environments</span></span>
<span data-ttu-id="6e4ae-151">如果您在相同的虛擬網路中部署多個 App Service 環境，並從一個 App Service 環境傳出呼叫至另一個 App Service 環境，則可能產生更複雜的案例。</span><span class="sxs-lookup"><span data-stu-id="6e4ae-151">A more complex scenario can occur if you deploy multiple App Service Environments in the same virtual network, and make outbound calls from one App Service Environment to another App Service Environment.</span></span>  <span data-ttu-id="6e4ae-152">這些跨 App Service 環境的呼叫也會被視為「網際網路」呼叫。</span><span class="sxs-lookup"><span data-stu-id="6e4ae-152">These types of cross App Service Environment calls will also be treated as "Internet" calls.</span></span>

<span data-ttu-id="6e4ae-153">下圖顯示分層架構範例，其中應用程式在一個 App Service 環境上 (例如「前端」Web 應用程式) 呼叫第二個 App Service 環境上的應用程式 (例如：內部後端 API 應用程式不需要可從網際網路存取)。</span><span class="sxs-lookup"><span data-stu-id="6e4ae-153">The following diagram shows an example of a layered architecture with apps on one App Service Environment (e.g. "Front door" web apps) calling apps on a second App Service Environment (e.g. internal back-end API apps not intended to be accessible from the Internet).</span></span> 

![App Service 環境之間的呼叫][CallsBetweenAppServiceEnvironments] 

<span data-ttu-id="6e4ae-155">在上述範例中，App Service 環境 "ASE One" 有一個輸出 IP 位址 192.23.1.2。</span><span class="sxs-lookup"><span data-stu-id="6e4ae-155">In the example above the App Service Environment "ASE One" has an outbound IP address of 192.23.1.2.</span></span>  <span data-ttu-id="6e4ae-156">如果 App Service 環境上執行的應用程式，對位於相同虛擬網路中第二個 App Service 環境 ("ASE Two") 上執行的應用程式進行輸出呼叫，會將輸出呼叫視為「網際網路」呼叫。</span><span class="sxs-lookup"><span data-stu-id="6e4ae-156">If an app running on this App Service Environment makes an outbound call to an app running on a second App Service Environment ("ASE Two") located in the same virtual network, the outbound call will be treated as an "Internet" call.</span></span>  <span data-ttu-id="6e4ae-157">因此，到達第二個 App Service 環境的網路流量會將來源顯示為來自 192.23.1.2 (亦即，不是第一個 App Service 環境的子網路位址範圍)。</span><span class="sxs-lookup"><span data-stu-id="6e4ae-157">As a result the network traffic arriving on the second App Service Environment will show as originating from 192.23.1.2 (i.e. not the subnet address range of the first App Service Environment).</span></span>

<span data-ttu-id="6e4ae-158">即使不同 App Service 環境之間的呼叫會視為「網際網路」呼叫，當兩個 App Service 環境同時位於相同的 Azure 區域時，網路流量會維持在 Azure 區域網路上，而不會實際在公用網際網路流動。</span><span class="sxs-lookup"><span data-stu-id="6e4ae-158">Even though calls between different App Service Environments are treated as "Internet" calls, when both App Service Environments are located in the same Azure region the network traffic will remain on the regional Azure network and will not physically flow over the public Internet.</span></span>  <span data-ttu-id="6e4ae-159">因此，您可以使用第二個 App Service 環境的子網路上的網路安全性群組，僅允許來自第一個 App Service (其傳入 IP 位址為 192.23.1.2) 的傳入呼叫，因而確保 App Service 環境之間的通訊安全。</span><span class="sxs-lookup"><span data-stu-id="6e4ae-159">As a result you can use a network security group on the subnet of the second App Service Environment to only allow inbound calls from the first App Service Environment (whose outbound IP address is 192.23.1.2), thus ensuring secure communication between the App Service Environments.</span></span>

## <a name="additional-links-and-information"></a><span data-ttu-id="6e4ae-160">其他連結和資訊</span><span class="sxs-lookup"><span data-stu-id="6e4ae-160">Additional Links and Information</span></span>
<span data-ttu-id="6e4ae-161">您可以在 [應用程式服務環境的讀我檔案](../app-service/app-service-app-service-environments-readme.md)中取得 App Service 環境的所有相關文章與做法。</span><span class="sxs-lookup"><span data-stu-id="6e4ae-161">All articles and How-To's for App Service Environments are available in the [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="6e4ae-162">如需 App Service 環境所使用輸入連接埠以及使用網路安全性群組來控制輸入流量的詳細資料，請參閱[這裡][controllinginboundtraffic]。</span><span class="sxs-lookup"><span data-stu-id="6e4ae-162">Details on inbound ports used by App Service Environments and using network security groups to control inbound traffic is available [here][controllinginboundtraffic].</span></span>

<span data-ttu-id="6e4ae-163">如需利用使用者定義路徑來授與到 App Service 環境之輸出網際網路存取的詳細資料，請參閱本[文章][ExpressRoute]。</span><span class="sxs-lookup"><span data-stu-id="6e4ae-163">Details on using user defined routes to grant outbound Internet access to App Service Environments is available in this [article][ExpressRoute].</span></span> 

<!-- LINKS -->
[virtualnetwork]: http://azure.microsoft.com/services/virtual-network/
[controllinginboundtraffic]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[ExpressRoute]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-configuration-expressroute/

<!-- IMAGES -->
[GeneralNetworkFlows]: ./media/app-service-app-service-environment-network-architecture-overview/NetworkOverview-1.png
[OutboundIPAddress]: ./media/app-service-app-service-environment-network-architecture-overview/OutboundIPAddress-1.png
[OutboundNetworkAddresses]: ./media/app-service-app-service-environment-network-architecture-overview/OutboundNetworkAddresses-1.png
[CallsBetweenAppServiceEnvironments]: ./media/app-service-app-service-environment-network-architecture-overview/CallsBetweenEnvironments-1.png

