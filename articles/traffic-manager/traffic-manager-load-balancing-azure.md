---
title: "在 Azure 中使用負載平衡服務 | Microsoft Docs"
description: "本教學課程會示範如何使用 Azure 負載平衡組合建立案例︰流量管理員、應用程式閘道和負載平衡器。"
services: traffic-manager
documentationcenter: 
author: liumichelle
manager: vitinnan
editor: 
ms.assetid: f89be3be-a16f-4d47-bcae-db2ab72ade17
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/27/2016
ms.author: limichel
ms.openlocfilehash: ae9bd30b76786f94f0d836a39137da696fdb94a2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="using-load-balancing-services-in-azure"></a><span data-ttu-id="c6ae9-103">在 Azure 中使用負載平衡服務</span><span class="sxs-lookup"><span data-stu-id="c6ae9-103">Using load-balancing services in Azure</span></span>

## <a name="introduction"></a><span data-ttu-id="c6ae9-104">簡介</span><span class="sxs-lookup"><span data-stu-id="c6ae9-104">Introduction</span></span>

<span data-ttu-id="c6ae9-105">Microsoft Azure 提供多個服務，可管理分配網路流量和負載平衡的方式。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-105">Microsoft Azure provides multiple services for managing how network traffic is distributed and load balanced.</span></span> <span data-ttu-id="c6ae9-106">根據您的需求，您可以個別使用這些服務或者結合其方法來建立最佳的解決方案。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-106">You can use these services individually or combine their methods, depending on your needs, to build the optimal solution.</span></span>

<span data-ttu-id="c6ae9-107">在本教學課程中，我們首先定義客戶使用案例，看看如何使用下列的 Azure 負載平衡組合讓它更強大且高效能︰流量管理員、應用程式閘道和負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-107">In this tutorial, we first define a customer use case and see how it can be made more robust and performant by using the following Azure load-balancing portfolio: Traffic Manager, Application Gateway, and Load Balancer.</span></span> <span data-ttu-id="c6ae9-108">然後，我們會提供逐步說明如何建立地理備援、分散流量至 VM，並協助您管理不同要求類型功能的部署。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-108">We then provide step-by-step instructions for creating a deployment that is geographically redundant, distributes traffic to VMs, and helps you manage different types of requests.</span></span>

<span data-ttu-id="c6ae9-109">在概念層級中，這些服務每一個都在負載平衡階層架構中扮演不同的角色。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-109">At a conceptual level, each of these services plays a distinct role in the load-balancing hierarchy.</span></span>

* <span data-ttu-id="c6ae9-110">**流量管理員**提供全域 DNS 負載平衡。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-110">**Traffic Manager** provides global DNS load balancing.</span></span> <span data-ttu-id="c6ae9-111">它會查看傳入 DNS 要求並根據客戶所選取的路由原則，以狀況良好的端點回應。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-111">It looks at incoming DNS requests and responds with a healthy endpoint, in accordance with the routing policy the customer has selected.</span></span> <span data-ttu-id="c6ae9-112">路由方法的選項如下︰</span><span class="sxs-lookup"><span data-stu-id="c6ae9-112">Options for routing methods are:</span></span>
  * <span data-ttu-id="c6ae9-113">效能路由，根據延遲將要求者傳送到最接近的端點。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-113">Performance routing to send the requestor to the closest endpoint in terms of latency.</span></span>
  * <span data-ttu-id="c6ae9-114">優先順序路由，可將所有流量導向端點，而其他端點做為備份。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-114">Priority routing to direct all traffic to an endpoint, with other endpoints as backup.</span></span>
  * <span data-ttu-id="c6ae9-115">加權循環配置資源路由，可根據指派給各端點的加權分散流量。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-115">Weighted round-robin routing, which distributes traffic based on the weighting that is assigned to each endpoint.</span></span>

  <span data-ttu-id="c6ae9-116">用戶端直接連線至該端點。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-116">The client connects directly to that endpoint.</span></span> <span data-ttu-id="c6ae9-117">Azure 流量管理員會在偵測到端點狀況不良時，將用戶端重新導向至另一個狀況良好的執行個體。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-117">Azure Traffic Manager detects when an endpoint is unhealthy and then redirects the clients to another healthy instance.</span></span> <span data-ttu-id="c6ae9-118">若要了解服務的相關資訊，請參閱 [Azure 流量管理員文件](traffic-manager-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-118">Refer to [Azure Traffic Manager documentation](traffic-manager-overview.md) to learn more about the service.</span></span>
* <span data-ttu-id="c6ae9-119">**應用程式閘道**會以服務形式提供應用程式傳遞控制器 (ADC)，為您的應用程式提供各種第 7 層負載平衡功能。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-119">**Application Gateway** provides application delivery controller (ADC) as a service, offering various Layer 7 load-balancing capabilities for your application.</span></span> <span data-ttu-id="c6ae9-120">它會將 CPU 密集 SSL 終止卸載至應用程式閘道，讓客戶最佳化 Web 伺服陣列的產能。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-120">It allows customers to optimize web farm productivity by offloading CPU-intensive SSL termination to the application gateway.</span></span> <span data-ttu-id="c6ae9-121">其他第 7 層路由功能包括循環配置連入流量、以 Cookie 為基礎的工作階段同質、URL 路徑型路由，以及在單一應用程式閘道背後代管多個網站的能力。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-121">Other Layer 7 routing capabilities include round-robin distribution of incoming traffic, cookie-based session affinity, URL path-based routing, and the ability to host multiple websites behind a single application gateway.</span></span> <span data-ttu-id="c6ae9-122">應用程式閘道可以設定為連結網際網路的閘道、內部專用閘道或兩者混合。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-122">Application Gateway can be configured as an Internet-facing gateway, an internal-only gateway, or a combination of both.</span></span> <span data-ttu-id="c6ae9-123">應用程式閘道完全由 Azure 管理、可調整且可用性極高。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-123">Application Gateway is fully Azure managed, scalable, and highly available.</span></span> <span data-ttu-id="c6ae9-124">它提供一組豐富的診斷和記錄功能，很好管理。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-124">It provides a rich set of diagnostics and logging capabilities for better manageability.</span></span>
* <span data-ttu-id="c6ae9-125">**負載平衡器**是 Azure SDN 堆疊不可或缺的一部分，針對所有 UDP 和 TCP 通訊協定提供高效能、低延遲的第 4 層負載平衡服務。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-125">**Load Balancer** is an integral part of the Azure SDN stack, providing high-performance, low-latency Layer 4 load-balancing services for all UDP and TCP protocols.</span></span> <span data-ttu-id="c6ae9-126">它會管理輸入及輸出連線。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-126">It manages inbound and outbound connections.</span></span> <span data-ttu-id="c6ae9-127">您可以設定公用和內部負載平衡端點，並使用 TCP 和 HTTP 健全狀況探查選項定義規則，將輸入連線對應至後端集區目的地，以管理服務可用性。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-127">You can configure public and internal load-balanced endpoints and define rules to map inbound connections to back-end pool destinations by using TCP and HTTP health-probing options to manage service availability.</span></span>

## <a name="scenario"></a><span data-ttu-id="c6ae9-128">案例</span><span class="sxs-lookup"><span data-stu-id="c6ae9-128">Scenario</span></span>

<span data-ttu-id="c6ae9-129">在此範例案例中，我們使用簡單的網站提供兩種類型的內容︰影像及動態呈現的網頁。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-129">In this example scenario, we use a simple website that serves two types of content: images and dynamically rendered webpages.</span></span> <span data-ttu-id="c6ae9-130">網站必須是地理備援，且應從最接近 (最低延遲) 的位置將服務提供給其使用者。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-130">The website must be geographically redundant, and it should serve its users from the closest (lowest latency) location to them.</span></span> <span data-ttu-id="c6ae9-131">應用程式開發人員決定任何符合模式/影像/* 的 URL 都是從不同於 Web 伺服陣列之其餘部分的專用 VM 集區提供。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-131">The application developer has decided that any URLs that match the pattern /images/* are served from a dedicated pool of VMs that are different from the rest of the web farm.</span></span>

<span data-ttu-id="c6ae9-132">此外，提供動態內容的預設 VM 集區需要與高可用性叢集上裝載的後端資料庫聯繫。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-132">Additionally, the default VM pool serving the dynamic content needs to talk to a back-end database that is hosted on a high-availability cluster.</span></span> <span data-ttu-id="c6ae9-133">整個部署是透過 Azure Resource Manager 來設定。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-133">The entire deployment is set up through Azure Resource Manager.</span></span>

<span data-ttu-id="c6ae9-134">使用流量管理員、應用程式閘道和負載平衡器可讓這個網站達成這些設計目標︰</span><span class="sxs-lookup"><span data-stu-id="c6ae9-134">Using Traffic Manager, Application Gateway, and Load Balancer allows this website to achieve these design goals:</span></span>

* <span data-ttu-id="c6ae9-135">**多重地理區域備援**：如果某個區域故障，流量管理員會將流量順暢地路由到最近的區域，而不需要應用程式擁有者介入。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-135">**Multi-geo redundancy**: If one region goes down, Traffic Manager routes traffic seamlessly to the closest region without any intervention from the application owner.</span></span>
* <span data-ttu-id="c6ae9-136">**降低延遲**：因為流量管理員會自動將客戶導向到最近的區域，所以當客戶要求網頁內容時會體驗到較低的延遲。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-136">**Reduced latency**: Because Traffic Manager automatically directs the customer to the closest region, the customer experiences lower latency when requesting the webpage contents.</span></span>
* <span data-ttu-id="c6ae9-137">**獨立擴充**︰因為 Web 應用程式工作負載是透過內容類型分隔，應用程式擁有者可以各自獨立調整要求工作負載。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-137">**Independent scalability**: Because the web application workload is separated by type of content, the application owner can scale the request workloads independent of each other.</span></span> <span data-ttu-id="c6ae9-138">應用程式閘道可根據指定的規則和應用程式的健全狀況，確保流量路由傳送至適當的集區。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-138">Application Gateway ensures that the traffic is routed to the right pools based on the specified rules and the health of the application.</span></span>
* <span data-ttu-id="c6ae9-139">**內部負載平衡**︰因為高可用性叢集前面具有負載平衡器，只有作用中且狀況良好的資料庫端點會公開給應用程式。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-139">**Internal load balancing**: Because Load Balancer is in front of the high-availability cluster, only the active and healthy endpoint for a database is exposed to the application.</span></span> <span data-ttu-id="c6ae9-140">此外，資料庫管理員可以獨立將主動和被動複本分散到前端應用程式的叢集來最佳化工作負載。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-140">Additionally, a database administrator can optimize the workload by distributing active and passive replicas across the cluster independent of the front-end application.</span></span> <span data-ttu-id="c6ae9-141">負載平衡器會提供對高可用性叢集的連線，並確定只有狀況良好的資料庫會收到連線要求。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-141">Load Balancer delivers connections to the high-availability cluster and ensures that only healthy databases receive connection requests.</span></span>

<span data-ttu-id="c6ae9-142">下圖顯示此案例的架構︰</span><span class="sxs-lookup"><span data-stu-id="c6ae9-142">The following diagram shows the architecture of this scenario:</span></span>

![負載平衡架構的圖表](./media/traffic-manager-load-balancing-azure/scenario-diagram.png)

> [!NOTE]
> <span data-ttu-id="c6ae9-144">這個範例只是 Azure 所提供的許多可能的負載平衡服務設定的其中一個。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-144">This example is only one of many possible configurations of the load-balancing services that Azure offers.</span></span> <span data-ttu-id="c6ae9-145">Azure 流量管理員、應用程式閘道和負載平衡器可以混合使用及配對，以提供最符合您負載平衡的需求。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-145">Traffic Manager, Application Gateway, and Load Balancer can be mixed and matched to best suit your load-balancing needs.</span></span> <span data-ttu-id="c6ae9-146">例如，如果 SSL 卸載或第 7 層處理並非必要，則負載平衡器可用以取代應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-146">For example, if SSL offload or Layer 7 processing is not necessary, Load Balancer can be used in place of Application Gateway.</span></span>

## <a name="setting-up-the-load-balancing-stack"></a><span data-ttu-id="c6ae9-147">設定負載平衡堆疊</span><span class="sxs-lookup"><span data-stu-id="c6ae9-147">Setting up the load-balancing stack</span></span>

### <a name="step-1-create-a-traffic-manager-profile"></a><span data-ttu-id="c6ae9-148">步驟 1︰建立流量管理員設定檔</span><span class="sxs-lookup"><span data-stu-id="c6ae9-148">Step 1: Create a Traffic Manager profile</span></span>

1. <span data-ttu-id="c6ae9-149">在 Azure 入口網站中，按一下 [新增]，然後搜尋「流量管理員設定檔」的 Marketplace。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-149">In the Azure portal, click **New**, and then search the marketplace for "Traffic Manager profile."</span></span>
2. <span data-ttu-id="c6ae9-150">在 [建立流量管理員設定檔] 刀鋒視窗中，輸入下列的基本資訊︰</span><span class="sxs-lookup"><span data-stu-id="c6ae9-150">On the **Create Traffic Manager profile** blade, enter the following basic information:</span></span>

  * <span data-ttu-id="c6ae9-151">**名稱**：為您的流量管理員設定檔提供一個 DNS 首碼名稱。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-151">**Name**: Give your Traffic Manager profile a DNS prefix name.</span></span>
  * <span data-ttu-id="c6ae9-152">**路由方法**：選取流量路由方法原則。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-152">**Routing method**: Select the traffic-routing method policy.</span></span> <span data-ttu-id="c6ae9-153">如需方法的詳細資訊，請參閱[關於流量管理員流量路由方法](traffic-manager-routing-methods.md)。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-153">For more information about the methods, see [About Traffic Manager traffic routing methods](traffic-manager-routing-methods.md).</span></span>
  * <span data-ttu-id="c6ae9-154">**訂閱**：選取包含設定檔的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-154">**Subscription**: Select the subscription that contains the profile.</span></span>
  * <span data-ttu-id="c6ae9-155">**資源群組**：選取包含設定檔的資源群組。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-155">**Resource group**: Select the resource group that contains the profile.</span></span> <span data-ttu-id="c6ae9-156">可以是新的或現有的資源群組。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-156">It can be a new or existing resource group.</span></span>
  * <span data-ttu-id="c6ae9-157">**資源群組位置**：流量管理員服務為全域服務，無法繫結至某個位置。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-157">**Resource group location**: Traffic Manager service is global and not bound to a location.</span></span> <span data-ttu-id="c6ae9-158">不過，您必須針對群組指定一個與流量管理員設定檔相關聯之中繼資料所在的區域。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-158">However, you must specify a region for the group where the metadata associated with the Traffic Manager profile resides.</span></span> <span data-ttu-id="c6ae9-159">這個位置對於設定檔的執行階段可用性沒有任何影響。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-159">This location has no impact on the runtime availability of the profile.</span></span>

3. <span data-ttu-id="c6ae9-160">按一下 [建立] 以產生流量管理員設定檔。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-160">Click **Create** to generate the Traffic Manager profile.</span></span>

  ![[建立流量管理員] 刀鋒視窗](./media/traffic-manager-load-balancing-azure/s1-create-tm-blade.png)

### <a name="step-2-create-the-application-gateways"></a><span data-ttu-id="c6ae9-162">步驟 2：建立應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="c6ae9-162">Step 2: Create the application gateways</span></span>

1. <span data-ttu-id="c6ae9-163">在 Azure 入口網站的左窗格中，按一下 [新增] > [網路] > [應用程式閘道]。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-163">In the Azure portal, in the left pane, click **New** > **Networking** > **Application Gateway**.</span></span>
2. <span data-ttu-id="c6ae9-164">輸入下列關於應用程式閘道的基本資訊︰</span><span class="sxs-lookup"><span data-stu-id="c6ae9-164">Enter the following basic information about the application gateway:</span></span>

  * <span data-ttu-id="c6ae9-165">**名稱**：應用程式閘道的名稱。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-165">**Name**: The name of the application gateway.</span></span>
  * <span data-ttu-id="c6ae9-166">**SKU 大小**：應用程式閘道的大小，有「小型」、「中型」或「大型」。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-166">**SKU size**: The size of the application gateway, available as Small, Medium, or Large.</span></span>
  * <span data-ttu-id="c6ae9-167">**執行個體計數**：執行個體的數目，從 2 到 10 的值。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-167">**Instance count**: The number of instances, a value from 2 through 10.</span></span>
  * <span data-ttu-id="c6ae9-168">**資源群組**：保存應用程式閘道的資源群組。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-168">**Resource group**: The resource group that holds the application gateway.</span></span> <span data-ttu-id="c6ae9-169">它可以是現有的或新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-169">It can be an existing resource group or a new one.</span></span>
  * <span data-ttu-id="c6ae9-170">**位置**：應用程式閘道的區域，它是與資源群組所在相同的位置。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-170">**Location**: The region for the application gateway, which is the same location as the resource group.</span></span> <span data-ttu-id="c6ae9-171">位置相當重要，因為虛擬網路和公用 IP 必須與閘道位於相同位置。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-171">The location is important, because the virtual network and public IP must be in the same location as the gateway.</span></span>
3. <span data-ttu-id="c6ae9-172">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-172">Click **OK**.</span></span>
4. <span data-ttu-id="c6ae9-173">接下來，針對應用程式閘道定義虛擬網路、子網路、前端 IP 與接聽程式設定。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-173">Define the virtual network, subnet, front-end IP, and listener configurations for the application gateway.</span></span> <span data-ttu-id="c6ae9-174">在此案例中，前端 IP 位址是**公用**，以允許它稍後做為端點新增至流量管理員設定檔。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-174">In this scenario, the front-end IP address is **Public**, which allows it to be added as an endpoint to the Traffic Manager profile later on.</span></span>
5. <span data-ttu-id="c6ae9-175">使用下列其中一個選項設定接聽程式︰</span><span class="sxs-lookup"><span data-stu-id="c6ae9-175">Configure the listener with one of the following options:</span></span>
    * <span data-ttu-id="c6ae9-176">如果您使用 HTTP，則無需設定。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-176">If you use HTTP, there is nothing to configure.</span></span> <span data-ttu-id="c6ae9-177">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-177">Click **OK**.</span></span>
    * <span data-ttu-id="c6ae9-178">如果您使用 HTTPS，則需要設定進一步的設定。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-178">If you use HTTPS, further configuration is required.</span></span> <span data-ttu-id="c6ae9-179">請參閱[建立應用程式閘道](../application-gateway/application-gateway-create-gateway-portal.md)，由步驟 9 開始。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-179">Refer to [Create an application gateway](../application-gateway/application-gateway-create-gateway-portal.md), starting at step 9.</span></span> <span data-ttu-id="c6ae9-180">完成設定後，按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-180">When you have completed the configuration, click **OK**.</span></span>

#### <a name="configure-url-routing-for-application-gateways"></a><span data-ttu-id="c6ae9-181">設定應用程式閘道的 URL 路由</span><span class="sxs-lookup"><span data-stu-id="c6ae9-181">Configure URL routing for application gateways</span></span>

<span data-ttu-id="c6ae9-182">當您選擇後端集區時，使用路徑型規則設定的應用程式閘道會採用除循環配置資源散發以外之要求 URL 的路徑模式。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-182">When you choose a back-end pool, an application gateway that's configured with a path-based rule takes a path pattern of the request URL in addition to round-robin distribution.</span></span> <span data-ttu-id="c6ae9-183">在此案例中，我們要將導向任何具有「/images/\*」之 URL 的路徑型規則新增到映像伺服器集區。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-183">In this scenario, we are adding a path-based rule to direct any URL with "/images/\*" to the image server pool.</span></span> <span data-ttu-id="c6ae9-184">如需設定應用程式閘道的 URL 路徑型路由相關資訊，請參閱[建立應用程式閘道的路徑型規則](../application-gateway/application-gateway-create-url-route-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-184">For more information about configuring URL path-based routing for an application gateway, refer to [Create a path-based rule for an application gateway](../application-gateway/application-gateway-create-url-route-portal.md).</span></span>

![應用程式閘道 Web 層圖表](./media/traffic-manager-load-balancing-azure/web-tier-diagram.png)

1. <span data-ttu-id="c6ae9-186">從資源群組中，移至您在上一節所建立之應用程式閘道的執行個體。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-186">From your resource group, go to the instance of the application gateway that you created in the preceding section.</span></span>
2. <span data-ttu-id="c6ae9-187">在 [設定] 下選取 [後端集區]，然後選取 [新增] 以新增您要與 Web 層後端集區相關聯的 VM。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-187">Under **Settings**, select **Backend pools**, and then select **Add** to add the VMs that you want to associate with the web-tier back-end pools.</span></span>
3. <span data-ttu-id="c6ae9-188">在 [新增後端集區] 刀鋒視窗中，輸入後端集區的名稱和存放於集區中所有機器的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-188">On the **Add backend pool** blade, enter the name of the back-end pool and all the IP addresses of the machines that reside in the pool.</span></span> <span data-ttu-id="c6ae9-189">在此案例中，我們會連接兩個虛擬機器的後端伺服器集區。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-189">In this scenario, we are connecting two back-end server pools of virtual machines.</span></span>

  ![應用程式閘道「新增後端集區」刀鋒視窗](./media/traffic-manager-load-balancing-azure/s2-appgw-add-bepool.png)

4. <span data-ttu-id="c6ae9-191">在應用程式閘道的 [設定] 下選取 [規則]，然後按一下 [路徑型] 按鈕以新增規則。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-191">Under **Settings** of the application gateway, select **Rules**, and then click the **Path based** button to add a rule.</span></span>

  ![應用程式閘道規則「路徑型」按鈕](./media/traffic-manager-load-balancing-azure/s2-appgw-add-pathrule.png)

5. <span data-ttu-id="c6ae9-193">在 [新增路徑型規則] 刀鋒視窗中，提供下列資訊來設定規則。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-193">On the **Add path-based rule** blade, configure the rule by providing the following information.</span></span>

   <span data-ttu-id="c6ae9-194">基本設定：</span><span class="sxs-lookup"><span data-stu-id="c6ae9-194">Basic settings:</span></span>

   + <span data-ttu-id="c6ae9-195">**名稱**：入口網站中可存取之規則的易記名稱。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-195">**Name**: The friendly name of the rule that is accessible in the portal.</span></span>
   + <span data-ttu-id="c6ae9-196">**接聽程式**：用於規則的接聽程式。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-196">**Listener**: The listener that is used for the rule.</span></span>
   + <span data-ttu-id="c6ae9-197">**預設後端集區**：搭配預設規則使用的後端集區。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-197">**Default backend pool**: The back-end pool to be used with the default rule.</span></span>
   + <span data-ttu-id="c6ae9-198">**預設 HTTP 設定**：要搭配預設規則使用的 HTTP 設定。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-198">**Default HTTP settings**: The HTTP settings to be used with the default rule.</span></span>

   <span data-ttu-id="c6ae9-199">路徑型規則：</span><span class="sxs-lookup"><span data-stu-id="c6ae9-199">Path-based rules:</span></span>

   + <span data-ttu-id="c6ae9-200">**名稱**：路徑型規則的易記名稱。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-200">**Name**: The friendly name of the path-based rule.</span></span>
   + <span data-ttu-id="c6ae9-201">**路徑**：用於轉送流量的路徑規則。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-201">**Paths**: The path rule that is used for forwarding traffic.</span></span>
   + <span data-ttu-id="c6ae9-202">**後端集區**：要搭配此規則使用的後端集區。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-202">**Backend Pool**: The back-end pool to be used with this rule.</span></span>
   + <span data-ttu-id="c6ae9-203">**HTTP 設定**：要搭配此規則使用的 HTTP 設定。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-203">**HTTP Setting**: The HTTP settings to be used with this rule.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="c6ae9-204">路徑︰有效的路徑必須以 "/" 開頭。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-204">Paths: Valid paths must start with "/".</span></span> <span data-ttu-id="c6ae9-205">萬用字元 "\*" 僅允許在結尾使用。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-205">The wildcard "\*" is allowed only at the end.</span></span> <span data-ttu-id="c6ae9-206">有效範例包括 /xyz、/xyz\* 或 /xyz/\*。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-206">Valid examples are /xyz, /xyz\*, or /xyz/\*.</span></span>

   ![應用程式閘道器「新增路徑型規則」刀鋒視窗](./media/traffic-manager-load-balancing-azure/s2-appgw-pathrule-blade.png)

### <a name="step-3-add-application-gateways-to-the-traffic-manager-endpoints"></a><span data-ttu-id="c6ae9-208">步驟 3︰將應用程式閘道新增至流量管理員端點</span><span class="sxs-lookup"><span data-stu-id="c6ae9-208">Step 3: Add application gateways to the Traffic Manager endpoints</span></span>

<span data-ttu-id="c6ae9-209">在此案例中，流量管理員會連結到位於不同區域中的應用程式閘道 (如前述步驟中所設定)。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-209">In this scenario, Traffic Manager is connected to application gateways (as configured in the preceding steps) that reside in different regions.</span></span> <span data-ttu-id="c6ae9-210">現在已設定應用程式閘道，下一步是將它們連接至您的流量管理員設定檔。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-210">Now that the application gateways are configured, the next step is to connect them to your Traffic Manager profile.</span></span>

1. <span data-ttu-id="c6ae9-211">開啟流量管理員設定檔。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-211">Open your Traffic Manager profile.</span></span> <span data-ttu-id="c6ae9-212">若要這樣做，請從 [所有資源] 查看您的資源群組，或搜尋流量管理員設定檔的名稱。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-212">To do so, look in your resource group or search for the name of the Traffic Manager profile from **All Resources**.</span></span>
2. <span data-ttu-id="c6ae9-213">在左窗格中，選取 [端點]，然後按一下 [新增] 以新增端點。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-213">In the left pane, select **Endpoints**, and then click **Add** to add an endpoint.</span></span>

  ![流量管理員端點「新增」按鈕](./media/traffic-manager-load-balancing-azure/s3-tm-add-endpoint.png)

3. <span data-ttu-id="c6ae9-215">在 [新增端點] 刀鋒視窗中，輸入下列資訊來建立端點︰</span><span class="sxs-lookup"><span data-stu-id="c6ae9-215">On the **Add endpoint** blade, create an endpoint by entering the following information:</span></span>

  * <span data-ttu-id="c6ae9-216">**類型**：選取進行負載平衡之端點的類型。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-216">**Type**: Select the type of endpoint to load-balance.</span></span> <span data-ttu-id="c6ae9-217">在此案例中，選取 [Azure 端點]，因為我們正在將它連接到先前已設定的應用程式閘道執行個體。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-217">In this scenario, select **Azure endpoint** because we are connecting it to the application gateway instances that were configured previously.</span></span>
  * <span data-ttu-id="c6ae9-218">**名稱**：輸入端點的名稱。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-218">**Name**: Enter the name of the endpoint.</span></span>
  * <span data-ttu-id="c6ae9-219">**目標資源類型**：選取 [公用 IP 位址]，然後在 [目標資源] 下，選取先前已設定的應用程式閘道公用 IP。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-219">**Target resource type**: Select **Public IP address** and then, under **Target resource**, select the public IP of the application gateway that was configured previously.</span></span>

   ![流量管理員「新增端點」刀鋒視窗](./media/traffic-manager-load-balancing-azure/s3-tm-add-endpoint-blade.png)

4. <span data-ttu-id="c6ae9-221">現在您可以測試您的安裝程式，方法為使用流量管理員設定檔的 DNS (此範例中為︰TrafficManagerScenario.trafficmanager.net) 來存取它。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-221">Now you can test your setup by accessing it with the DNS of your Traffic Manager profile (in this example: TrafficManagerScenario.trafficmanager.net).</span></span> <span data-ttu-id="c6ae9-222">您可以重送要求、啟動或關閉在不同區域中建立的 VM 和 Web 伺服器，以及變更流量管理員設定檔設定來測試您的設定。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-222">You can resend requests, bring up or bring down VMs and web servers that were created in different regions, and change the Traffic Manager profile settings to test your setup.</span></span>

### <a name="step-4-create-a-load-balancer"></a><span data-ttu-id="c6ae9-223">步驟 4：建立負載平衡器</span><span class="sxs-lookup"><span data-stu-id="c6ae9-223">Step 4: Create a load balancer</span></span>

<span data-ttu-id="c6ae9-224">在此案例中，負載平衡器會在高可用性叢集內將連接從 Web 層分配至資料庫。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-224">In this scenario, Load Balancer distributes connections from the web tier to the databases within a high-availability cluster.</span></span>

<span data-ttu-id="c6ae9-225">如果您的高可用性資料庫叢集是使用 SQL Server AlwaysOn，請參閱[設定一或多個 Always On 可用性群組接聽程式](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md)以取得逐步指示。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-225">If your high-availability database cluster is using SQL Server AlwaysOn, refer to [Configure one or more Always On Availability Group Listeners](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md) for step-by-step instructions.</span></span>

<span data-ttu-id="c6ae9-226">如需有關如何設定內部負載平衡器的詳細資訊，請參閱[在 Azure 入口網站中建立內部負載平衡器](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-226">For more information about configuring an internal load balancer, see [Create an Internal load balancer in the Azure portal](../load-balancer/load-balancer-get-started-ilb-arm-portal.md).</span></span>

1. <span data-ttu-id="c6ae9-227">在 Azure 入口網站的左窗格中，按一下 [新增] > [網路] > [負載平衡器]。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-227">In the Azure portal, in the left pane, click **New** > **Networking** > **Load balancer**.</span></span>
2. <span data-ttu-id="c6ae9-228">在 [建立負載平衡器] 刀鋒視窗中，選擇負載平衡器的名稱。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-228">On the **Create load balancer** blade, choose a name for your load balancer.</span></span>
3. <span data-ttu-id="c6ae9-229">將 [類型] 設定為 [內部]，並選擇適當的虛擬網路和子網路以供負載平衡器存放。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-229">Set the **Type** to **Internal**, and choose the appropriate virtual network and subnet for the load balancer to reside in.</span></span>
4. <span data-ttu-id="c6ae9-230">在 [IP 位址指派] 下，選取 [動態] 或 [靜態]。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-230">Under **IP address assignment**, select either **Dynamic** or **Static**.</span></span>
5. <span data-ttu-id="c6ae9-231">在 [資源群組] 下，選擇負載平衡器的資源群組。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-231">Under **Resource group**, choose the resource group for the load balancer.</span></span>
6. <span data-ttu-id="c6ae9-232">在 [位置] 下，選擇負載平衡器適用的地區。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-232">Under **Location**, choose the appropriate region for the load balancer.</span></span>
7. <span data-ttu-id="c6ae9-233">按一下 [建立] 以產生負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-233">Click **Create** to generate the load balancer.</span></span>

#### <a name="connect-a-back-end-database-tier-to-the-load-balancer"></a><span data-ttu-id="c6ae9-234">將後端資料庫層連接到負載平衡器</span><span class="sxs-lookup"><span data-stu-id="c6ae9-234">Connect a back-end database tier to the load balancer</span></span>

1. <span data-ttu-id="c6ae9-235">從資源群組中，尋找先前步驟中所建立的負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-235">From your resource group, find the load balancer that was created in the previous steps.</span></span>
2. <span data-ttu-id="c6ae9-236">在 [設定] 下，按一下 [後端集區]，然後按一下 [新增] 來新增後端集區。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-236">Under **Settings**, click **Backend pools**, and then click **Add** to add a back-end pool.</span></span>

  ![負載平衡器「新增後端集區」刀鋒視窗](./media/traffic-manager-load-balancing-azure/s4-ilb-add-bepool.png)

3. <span data-ttu-id="c6ae9-238">在 [新增後端集區] 刀鋒視窗中，輸入後端集區的名稱。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-238">On the **Add backend pool** blade, enter the name of the back-end pool.</span></span>
4. <span data-ttu-id="c6ae9-239">將個別機器或可用性設定組新增至後端集區。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-239">Add either individual machines or an availability set to the back-end pool.</span></span>

#### <a name="configure-a-probe"></a><span data-ttu-id="c6ae9-240">設定探查</span><span class="sxs-lookup"><span data-stu-id="c6ae9-240">Configure a probe</span></span>

1. <span data-ttu-id="c6ae9-241">在您的負載平衡器中，於 [設定] 下選取 [探查]，然後按一下 [新增] 來新增探查。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-241">In your load balancer, under **Settings**, select **Probes**, and then click **Add** to add a probe.</span></span>

 ![負載平衡器「新增探查」刀鋒視窗](./media/traffic-manager-load-balancing-azure/s4-ilb-add-probe.png)

2. <span data-ttu-id="c6ae9-243">在 [新增探查] 刀鋒視窗中，輸入探查的名稱。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-243">On the **Add probe** blade, enter the name for the probe.</span></span>
3. <span data-ttu-id="c6ae9-244">選取探查的**通訊協定**。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-244">Select the **Protocol** for the probe.</span></span> <span data-ttu-id="c6ae9-245">針對資料庫，您可能想要 TCP 探查，而不是 HTTP 探查。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-245">For a database, you might want a TCP probe rather than an HTTP probe.</span></span> <span data-ttu-id="c6ae9-246">若要了解有關負載平衡器探查的詳細資訊，請參閱[了解負載平衡器探查](../load-balancer/load-balancer-custom-probe-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-246">To learn more about load-balancer probes, refer to [Understand load balancer probes](../load-balancer/load-balancer-custom-probe-overview.md).</span></span>
4. <span data-ttu-id="c6ae9-247">輸入您要用來存取探查的資料庫**連接埠**。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-247">Enter the **Port** of your database to be used for accessing the probe.</span></span>
5. <span data-ttu-id="c6ae9-248">在 [間隔] 下，指定探查應用程式的頻率。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-248">Under **Interval**, specify how frequently to probe the application.</span></span>
6. <span data-ttu-id="c6ae9-249">在 [狀況不良閾值] 下，針對視為狀況不良的後端 VM 指定必須發生的連續探查失敗次數。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-249">Under **Unhealthy threshold**, specify the number of continuous probe failures that must occur for the back-end VM to be considered unhealthy.</span></span>
7. <span data-ttu-id="c6ae9-250">按一下 [確定] 以建立探查。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-250">Click **OK** to create the probe.</span></span>

#### <a name="configure-the-load-balancing-rules"></a><span data-ttu-id="c6ae9-251">設定負載平衡規則</span><span class="sxs-lookup"><span data-stu-id="c6ae9-251">Configure the load-balancing rules</span></span>

1. <span data-ttu-id="c6ae9-252">在負載平衡器的 [設定] 下，選取 [負載平衡規則]，然後按一下 [新增] 以建立規則。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-252">Under **Settings** of your load balancer, select **Load balancing rules**, and then click **Add** to create a rule.</span></span>
2. <span data-ttu-id="c6ae9-253">在 [新增負載平衡規則] 刀鋒視窗中，輸入負載平衡規則的**名稱**。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-253">On the **Add load balancing rule** blade, enter the **Name** for the load-balancing rule.</span></span>
3. <span data-ttu-id="c6ae9-254">依序選擇負載平衡器的 [前端 IP 位址]、[通訊協定] 和 [連接埠]。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-254">Choose the **Frontend IP Address** of the load balancer, **Protocol**, and **Port**.</span></span>
4. <span data-ttu-id="c6ae9-255">在 [後端連接埠] 下，指定要在後端集區中使用的連接埠。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-255">Under **Backend port**, specify the port to be used in the back-end pool.</span></span>
5. <span data-ttu-id="c6ae9-256">選取**後端集區**和在先前步驟中所建立以對其套用規則的**探查**。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-256">Select the **Backend pool** and the **Probe** that were created in the previous steps to apply the rule to.</span></span>
6. <span data-ttu-id="c6ae9-257">在 [工作階段持續性] 下，選擇要保存工作階段的方式。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-257">Under **Session persistence**, choose how you want the sessions to persist.</span></span>
7. <span data-ttu-id="c6ae9-258">在 [閒置逾時] 下，指定閒置逾時之前的分鐘數。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-258">Under **Idle timeouts**, specify the number of minutes before an idle timeout.</span></span>
8. <span data-ttu-id="c6ae9-259">在 [浮點 IP] 下，選取 [停用] 或 [啟用]。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-259">Under **Floating IP**, select either **Disabled** or **Enabled**.</span></span>
9. <span data-ttu-id="c6ae9-260">按一下 [確定] 以建立規則。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-260">Click **OK** to create the rule.</span></span>

### <a name="step-5-connect-web-tier-vms-to-the-load-balancer"></a><span data-ttu-id="c6ae9-261">步驟 5︰將 Web 層 VM 連線到負載平衡器</span><span class="sxs-lookup"><span data-stu-id="c6ae9-261">Step 5: Connect web-tier VMs to the load balancer</span></span>

<span data-ttu-id="c6ae9-262">現在我們針對任何資料庫連接，在 Web 層 VM 上執行的應用程式中設定 IP 位址和負載平衡器前端連接埠。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-262">Now we configure the IP address and load-balancer front-end port in the applications that are running on your web-tier VMs for any database connections.</span></span> <span data-ttu-id="c6ae9-263">此設定是在這些 VM 上執行之應用程式所特有的。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-263">This configuration is specific to the applications that run on these VMs.</span></span> <span data-ttu-id="c6ae9-264">若要設定目的地 IP 位址和連接埠，請參閱應用程式文件。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-264">To configure the destination IP address and port, refer to the application documentation.</span></span> <span data-ttu-id="c6ae9-265">若要尋找前端 IP 位址，請在 Azure 入口網站中，移至 [負載平衡器設定] 刀鋒視窗上的前端 IP 集區。</span><span class="sxs-lookup"><span data-stu-id="c6ae9-265">To find the IP address of the front end, in the Azure portal, go to the front-end IP pool on the **Load balancer settings** blade.</span></span>

![負載平衡器「前端 IP 集區」瀏覽窗格](./media/traffic-manager-load-balancing-azure/s5-ilb-frontend-ippool.png)

## <a name="next-steps"></a><span data-ttu-id="c6ae9-267">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c6ae9-267">Next steps</span></span>

* [<span data-ttu-id="c6ae9-268">流量管理員概觀</span><span class="sxs-lookup"><span data-stu-id="c6ae9-268">Overview of Traffic Manager</span></span>](traffic-manager-overview.md)
* [<span data-ttu-id="c6ae9-269">應用程式閘道概觀</span><span class="sxs-lookup"><span data-stu-id="c6ae9-269">Application Gateway overview</span></span>](../application-gateway/application-gateway-introduction.md)
* [<span data-ttu-id="c6ae9-270">Azure 負載平衡器概觀</span><span class="sxs-lookup"><span data-stu-id="c6ae9-270">Azure Load Balancer overview</span></span>](../load-balancer/load-balancer-overview.md)
