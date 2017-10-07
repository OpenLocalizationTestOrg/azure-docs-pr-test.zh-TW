---
title: "在 Azure 中 aaaUsing 負載平衡服務 |Microsoft 文件"
description: "此教學課程會示範如何 toocreate 案例中，使用 hello Azure 負載平衡的 portfolio： 流量管理員、 應用程式閘道和負載平衡器。"
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
ms.openlocfilehash: d217047102d8c4828250dc0733e8ec9ee1e84b3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-load-balancing-services-in-azure"></a><span data-ttu-id="a0d79-103">在 Azure 中使用負載平衡服務</span><span class="sxs-lookup"><span data-stu-id="a0d79-103">Using load-balancing services in Azure</span></span>

## <a name="introduction"></a><span data-ttu-id="a0d79-104">簡介</span><span class="sxs-lookup"><span data-stu-id="a0d79-104">Introduction</span></span>

<span data-ttu-id="a0d79-105">Microsoft Azure 提供多個服務，可管理分配網路流量和負載平衡的方式。</span><span class="sxs-lookup"><span data-stu-id="a0d79-105">Microsoft Azure provides multiple services for managing how network traffic is distributed and load balanced.</span></span> <span data-ttu-id="a0d79-106">您可以個別使用這些服務，或結合其方法，請根據您的需求，toobuild hello 最好的解決方案。</span><span class="sxs-lookup"><span data-stu-id="a0d79-106">You can use these services individually or combine their methods, depending on your needs, toobuild hello optimal solution.</span></span>

<span data-ttu-id="a0d79-107">在本教學課程中，我們先定義客戶使用案例，看到如何可以設為更強固和高效能使用下列 Azure 負載平衡 portfolio hello： 流量管理員、 應用程式閘道和負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="a0d79-107">In this tutorial, we first define a customer use case and see how it can be made more robust and performant by using hello following Azure load-balancing portfolio: Traffic Manager, Application Gateway, and Load Balancer.</span></span> <span data-ttu-id="a0d79-108">我們提供逐步指示，建立部署的地理備援、 分散流量 tooVMs 且可協助您管理不同類型的要求。</span><span class="sxs-lookup"><span data-stu-id="a0d79-108">We then provide step-by-step instructions for creating a deployment that is geographically redundant, distributes traffic tooVMs, and helps you manage different types of requests.</span></span>

<span data-ttu-id="a0d79-109">在概念層級中，每個服務扮演 hello 負載平衡的階層中不同角色。</span><span class="sxs-lookup"><span data-stu-id="a0d79-109">At a conceptual level, each of these services plays a distinct role in hello load-balancing hierarchy.</span></span>

* <span data-ttu-id="a0d79-110">**流量管理員**提供全域 DNS 負載平衡。</span><span class="sxs-lookup"><span data-stu-id="a0d79-110">**Traffic Manager** provides global DNS load balancing.</span></span> <span data-ttu-id="a0d79-111">它會查看連入 DNS 要求和回應狀況良好的端點，根據 hello 選取路由原則 hello 客戶。</span><span class="sxs-lookup"><span data-stu-id="a0d79-111">It looks at incoming DNS requests and responds with a healthy endpoint, in accordance with hello routing policy hello customer has selected.</span></span> <span data-ttu-id="a0d79-112">路由方法的選項如下︰</span><span class="sxs-lookup"><span data-stu-id="a0d79-112">Options for routing methods are:</span></span>
  * <span data-ttu-id="a0d79-113">效能路由 toosend hello 要求者 toohello 最靠近的端點依據延遲。</span><span class="sxs-lookup"><span data-stu-id="a0d79-113">Performance routing toosend hello requestor toohello closest endpoint in terms of latency.</span></span>
  * <span data-ttu-id="a0d79-114">路由 toodirect 所有流量 tooan 端點，與其他端點做為備份的優先權。</span><span class="sxs-lookup"><span data-stu-id="a0d79-114">Priority routing toodirect all traffic tooan endpoint, with other endpoints as backup.</span></span>
  * <span data-ttu-id="a0d79-115">加權的循環路由，這會根據 hello 加權指派 tooeach 端點的流量。</span><span class="sxs-lookup"><span data-stu-id="a0d79-115">Weighted round-robin routing, which distributes traffic based on hello weighting that is assigned tooeach endpoint.</span></span>

  <span data-ttu-id="a0d79-116">hello 用戶端會直接連接 toothat 端點。</span><span class="sxs-lookup"><span data-stu-id="a0d79-116">hello client connects directly toothat endpoint.</span></span> <span data-ttu-id="a0d79-117">Azure Traffic Manager 會偵測端點狀況不良，然後重新導向 hello 用戶端 tooanother 狀況良好的執行個體。</span><span class="sxs-lookup"><span data-stu-id="a0d79-117">Azure Traffic Manager detects when an endpoint is unhealthy and then redirects hello clients tooanother healthy instance.</span></span> <span data-ttu-id="a0d79-118">請參閱太[Azure Traffic Manager 文件](traffic-manager-overview.md)toolearn 更多關於 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="a0d79-118">Refer too[Azure Traffic Manager documentation](traffic-manager-overview.md) toolearn more about hello service.</span></span>
* <span data-ttu-id="a0d79-119">**應用程式閘道**會以服務形式提供應用程式傳遞控制器 (ADC)，為您的應用程式提供各種第 7 層負載平衡功能。</span><span class="sxs-lookup"><span data-stu-id="a0d79-119">**Application Gateway** provides application delivery controller (ADC) as a service, offering various Layer 7 load-balancing capabilities for your application.</span></span> <span data-ttu-id="a0d79-120">它可讓客戶 toooptimize web 伺服陣列產能卸載 CPU 運算密集 SSL 終止 toohello 應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="a0d79-120">It allows customers toooptimize web farm productivity by offloading CPU-intensive SSL termination toohello application gateway.</span></span> <span data-ttu-id="a0d79-121">其他 7 層路由功能包括循環配置資源發佈的連入流量，cookie 為基礎的工作階段親和性，路徑為基礎的路由 URL，和 hello 能力 toohost 背後的單一應用程式閘道的多個網站。</span><span class="sxs-lookup"><span data-stu-id="a0d79-121">Other Layer 7 routing capabilities include round-robin distribution of incoming traffic, cookie-based session affinity, URL path-based routing, and hello ability toohost multiple websites behind a single application gateway.</span></span> <span data-ttu-id="a0d79-122">應用程式閘道可以設定為連結網際網路的閘道、內部專用閘道或兩者混合。</span><span class="sxs-lookup"><span data-stu-id="a0d79-122">Application Gateway can be configured as an Internet-facing gateway, an internal-only gateway, or a combination of both.</span></span> <span data-ttu-id="a0d79-123">應用程式閘道完全由 Azure 管理、可調整且可用性極高。</span><span class="sxs-lookup"><span data-stu-id="a0d79-123">Application Gateway is fully Azure managed, scalable, and highly available.</span></span> <span data-ttu-id="a0d79-124">它提供一組豐富的診斷和記錄功能，很好管理。</span><span class="sxs-lookup"><span data-stu-id="a0d79-124">It provides a rich set of diagnostics and logging capabilities for better manageability.</span></span>
* <span data-ttu-id="a0d79-125">**負載平衡器**是 hello Azure SDN 堆疊，提供高效能、 低延遲第 4 層負載平衡服務所有 UDP 和 TCP 通訊協定不可或缺的一部分。</span><span class="sxs-lookup"><span data-stu-id="a0d79-125">**Load Balancer** is an integral part of hello Azure SDN stack, providing high-performance, low-latency Layer 4 load-balancing services for all UDP and TCP protocols.</span></span> <span data-ttu-id="a0d79-126">它會管理輸入及輸出連線。</span><span class="sxs-lookup"><span data-stu-id="a0d79-126">It manages inbound and outbound connections.</span></span> <span data-ttu-id="a0d79-127">您可以設定公用和內部負載平衡的端點，並定義規則 toomap 輸入連線 tooback 後端集區目的地使用 TCP 和 HTTP 健全狀況探查選項 toomanage 服務可用性。</span><span class="sxs-lookup"><span data-stu-id="a0d79-127">You can configure public and internal load-balanced endpoints and define rules toomap inbound connections tooback-end pool destinations by using TCP and HTTP health-probing options toomanage service availability.</span></span>

## <a name="scenario"></a><span data-ttu-id="a0d79-128">案例</span><span class="sxs-lookup"><span data-stu-id="a0d79-128">Scenario</span></span>

<span data-ttu-id="a0d79-129">在此範例案例中，我們使用簡單的網站提供兩種類型的內容︰影像及動態呈現的網頁。</span><span class="sxs-lookup"><span data-stu-id="a0d79-129">In this example scenario, we use a simple website that serves two types of content: images and dynamically rendered webpages.</span></span> <span data-ttu-id="a0d79-130">hello 網站必須是地理備援，並且應該提供其使用者 hello 最接近 （最低延遲） 從位置 toothem。</span><span class="sxs-lookup"><span data-stu-id="a0d79-130">hello website must be geographically redundant, and it should serve its users from hello closest (lowest latency) location toothem.</span></span> <span data-ttu-id="a0d79-131">hello 應用程式開發人員決定，比對任何 Url hello 模式映像 / * 來自 vm 的不同 hello 其餘 hello web 伺服陣列的專用集區。</span><span class="sxs-lookup"><span data-stu-id="a0d79-131">hello application developer has decided that any URLs that match hello pattern /images/* are served from a dedicated pool of VMs that are different from hello rest of hello web farm.</span></span>

<span data-ttu-id="a0d79-132">此外，提供 hello 動態內容的 hello 預設 VM 集區必須裝載在高可用性叢集 tootalk tooa 後端資料庫。</span><span class="sxs-lookup"><span data-stu-id="a0d79-132">Additionally, hello default VM pool serving hello dynamic content needs tootalk tooa back-end database that is hosted on a high-availability cluster.</span></span> <span data-ttu-id="a0d79-133">hello 整個部署設定透過 Azure 資源管理員。</span><span class="sxs-lookup"><span data-stu-id="a0d79-133">hello entire deployment is set up through Azure Resource Manager.</span></span>

<span data-ttu-id="a0d79-134">使用流量管理員、 應用程式閘道和負載平衡器可讓此網站 tooachieve 這些設計目標：</span><span class="sxs-lookup"><span data-stu-id="a0d79-134">Using Traffic Manager, Application Gateway, and Load Balancer allows this website tooachieve these design goals:</span></span>

* <span data-ttu-id="a0d79-135">**多個地理備援性**： 如果一個區域發生問題，Traffic Manager 路由流量順暢地 toohello hello 應用程式擁有者任何介入最接近的區域。</span><span class="sxs-lookup"><span data-stu-id="a0d79-135">**Multi-geo redundancy**: If one region goes down, Traffic Manager routes traffic seamlessly toohello closest region without any intervention from hello application owner.</span></span>
* <span data-ttu-id="a0d79-136">**降低延遲**： 因為 Traffic Manager 會自動引導 hello 客戶 toohello 最接近的區域、 hello 客戶遇到的延遲較低，當要求 hello 網頁內容。</span><span class="sxs-lookup"><span data-stu-id="a0d79-136">**Reduced latency**: Because Traffic Manager automatically directs hello customer toohello closest region, hello customer experiences lower latency when requesting hello webpage contents.</span></span>
* <span data-ttu-id="a0d79-137">**獨立的延展性**: hello web 應用程式工作負載分開的內容類型，因為 hello 應用程式擁有者可以調整 hello 要求工作負載彼此獨立。</span><span class="sxs-lookup"><span data-stu-id="a0d79-137">**Independent scalability**: Because hello web application workload is separated by type of content, hello application owner can scale hello request workloads independent of each other.</span></span> <span data-ttu-id="a0d79-138">應用程式閘道可確保 hello 流量會根據指定的 hello 路由的 toohello 右集區規則和 hello hello 應用程式的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="a0d79-138">Application Gateway ensures that hello traffic is routed toohello right pools based on hello specified rules and hello health of hello application.</span></span>
* <span data-ttu-id="a0d79-139">**內部負載平衡**: hello 資料庫使用中且狀況良好端點公開的 toohello 應用程式只是前面 hello 高可用性叢集，因為的負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="a0d79-139">**Internal load balancing**: Because Load Balancer is in front of hello high-availability cluster, only hello active and healthy endpoint for a database is exposed toohello application.</span></span> <span data-ttu-id="a0d79-140">此外，資料庫管理員可以最佳化 hello 工作負載分散 hello 前端應用程式的獨立 hello 叢集的主動和被動複本。</span><span class="sxs-lookup"><span data-stu-id="a0d79-140">Additionally, a database administrator can optimize hello workload by distributing active and passive replicas across hello cluster independent of hello front-end application.</span></span> <span data-ttu-id="a0d79-141">負載平衡器會提供連接 toohello 高可用性叢集，而且可確保只有狀況良好的資料庫接收連線要求。</span><span class="sxs-lookup"><span data-stu-id="a0d79-141">Load Balancer delivers connections toohello high-availability cluster and ensures that only healthy databases receive connection requests.</span></span>

<span data-ttu-id="a0d79-142">hello 下圖顯示此案例的 hello 架構：</span><span class="sxs-lookup"><span data-stu-id="a0d79-142">hello following diagram shows hello architecture of this scenario:</span></span>

![負載平衡架構的圖表](./media/traffic-manager-load-balancing-azure/scenario-diagram.png)

> [!NOTE]
> <span data-ttu-id="a0d79-144">這個範例是其中一個 hello 負載平衡服務，Azure 提供許多可能的設定。</span><span class="sxs-lookup"><span data-stu-id="a0d79-144">This example is only one of many possible configurations of hello load-balancing services that Azure offers.</span></span> <span data-ttu-id="a0d79-145">流量管理員、 應用程式閘道和負載平衡器可以混合和相符的 toobest 符合您負載平衡的需求。</span><span class="sxs-lookup"><span data-stu-id="a0d79-145">Traffic Manager, Application Gateway, and Load Balancer can be mixed and matched toobest suit your load-balancing needs.</span></span> <span data-ttu-id="a0d79-146">例如，如果 SSL 卸載或第 7 層處理並非必要，則負載平衡器可用以取代應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="a0d79-146">For example, if SSL offload or Layer 7 processing is not necessary, Load Balancer can be used in place of Application Gateway.</span></span>

## <a name="setting-up-hello-load-balancing-stack"></a><span data-ttu-id="a0d79-147">Hello 負載平衡堆疊設定</span><span class="sxs-lookup"><span data-stu-id="a0d79-147">Setting up hello load-balancing stack</span></span>

### <a name="step-1-create-a-traffic-manager-profile"></a><span data-ttu-id="a0d79-148">步驟 1︰建立流量管理員設定檔</span><span class="sxs-lookup"><span data-stu-id="a0d79-148">Step 1: Create a Traffic Manager profile</span></span>

1. <span data-ttu-id="a0d79-149">在 hello Azure 入口網站，按一下 **新增**，，然後搜尋 hello marketplace 中的 「 流量管理員設定檔 」。</span><span class="sxs-lookup"><span data-stu-id="a0d79-149">In hello Azure portal, click **New**, and then search hello marketplace for "Traffic Manager profile."</span></span>
2. <span data-ttu-id="a0d79-150">在 hello**建立 Traffic Manager 設定檔**刀鋒視窗中，輸入下列基本資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="a0d79-150">On hello **Create Traffic Manager profile** blade, enter hello following basic information:</span></span>

  * <span data-ttu-id="a0d79-151">**名稱**：為您的流量管理員設定檔提供一個 DNS 首碼名稱。</span><span class="sxs-lookup"><span data-stu-id="a0d79-151">**Name**: Give your Traffic Manager profile a DNS prefix name.</span></span>
  * <span data-ttu-id="a0d79-152">**路由方法**： 選取 hello 流量路由方法原則。</span><span class="sxs-lookup"><span data-stu-id="a0d79-152">**Routing method**: Select hello traffic-routing method policy.</span></span> <span data-ttu-id="a0d79-153">如需 hello 方法的詳細資訊，請參閱[有關 Traffic Manager 流量路由方式](traffic-manager-routing-methods.md)。</span><span class="sxs-lookup"><span data-stu-id="a0d79-153">For more information about hello methods, see [About Traffic Manager traffic routing methods](traffic-manager-routing-methods.md).</span></span>
  * <span data-ttu-id="a0d79-154">**訂用帳戶**： 選取包含 hello 設定檔的 hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="a0d79-154">**Subscription**: Select hello subscription that contains hello profile.</span></span>
  * <span data-ttu-id="a0d79-155">**資源群組**: hello 選取資源群組含有 hello 設定檔。</span><span class="sxs-lookup"><span data-stu-id="a0d79-155">**Resource group**: Select hello resource group that contains hello profile.</span></span> <span data-ttu-id="a0d79-156">可以是新的或現有的資源群組。</span><span class="sxs-lookup"><span data-stu-id="a0d79-156">It can be a new or existing resource group.</span></span>
  * <span data-ttu-id="a0d79-157">**資源群組位置**: Traffic Manager 服務正在全域和未繫結 tooa 位置。</span><span class="sxs-lookup"><span data-stu-id="a0d79-157">**Resource group location**: Traffic Manager service is global and not bound tooa location.</span></span> <span data-ttu-id="a0d79-158">不過，您必須指定 hello 群組 hello 與 hello Traffic Manager 設定檔相關聯的中繼資料所在的區域。</span><span class="sxs-lookup"><span data-stu-id="a0d79-158">However, you must specify a region for hello group where hello metadata associated with hello Traffic Manager profile resides.</span></span> <span data-ttu-id="a0d79-159">這個位置 hello hello 設定檔的執行階段可用性沒有任何影響。</span><span class="sxs-lookup"><span data-stu-id="a0d79-159">This location has no impact on hello runtime availability of hello profile.</span></span>

3. <span data-ttu-id="a0d79-160">按一下**建立**toogenerate hello Traffic Manager 設定檔。</span><span class="sxs-lookup"><span data-stu-id="a0d79-160">Click **Create** toogenerate hello Traffic Manager profile.</span></span>

  ![[建立流量管理員] 刀鋒視窗](./media/traffic-manager-load-balancing-azure/s1-create-tm-blade.png)

### <a name="step-2-create-hello-application-gateways"></a><span data-ttu-id="a0d79-162">步驟 2： 建立 hello 應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="a0d79-162">Step 2: Create hello application gateways</span></span>

1. <span data-ttu-id="a0d79-163">在 hello Azure 入口網站，hello 左窗格中，按一下 **新增** > **網路** > **應用程式閘道**。</span><span class="sxs-lookup"><span data-stu-id="a0d79-163">In hello Azure portal, in hello left pane, click **New** > **Networking** > **Application Gateway**.</span></span>
2. <span data-ttu-id="a0d79-164">輸入下列 hello 應用程式閘道的相關基本資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="a0d79-164">Enter hello following basic information about hello application gateway:</span></span>

  * <span data-ttu-id="a0d79-165">**名稱**: hello hello 應用程式閘道名稱。</span><span class="sxs-lookup"><span data-stu-id="a0d79-165">**Name**: hello name of hello application gateway.</span></span>
  * <span data-ttu-id="a0d79-166">**SKU 大小**: hello hello 應用程式閘道，可做為小、 中或大的大小。</span><span class="sxs-lookup"><span data-stu-id="a0d79-166">**SKU size**: hello size of hello application gateway, available as Small, Medium, or Large.</span></span>
  * <span data-ttu-id="a0d79-167">**執行個體計數**: hello 的執行個體的數目，從 2 到 10 的值。</span><span class="sxs-lookup"><span data-stu-id="a0d79-167">**Instance count**: hello number of instances, a value from 2 through 10.</span></span>
  * <span data-ttu-id="a0d79-168">**資源群組**: hello 保存 hello 應用程式閘道的資源群組。</span><span class="sxs-lookup"><span data-stu-id="a0d79-168">**Resource group**: hello resource group that holds hello application gateway.</span></span> <span data-ttu-id="a0d79-169">它可以是現有的或新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="a0d79-169">It can be an existing resource group or a new one.</span></span>
  * <span data-ttu-id="a0d79-170">**位置**: hello 應用程式閘道 hello 相同的 hello 區域為 hello 資源群組的位置。</span><span class="sxs-lookup"><span data-stu-id="a0d79-170">**Location**: hello region for hello application gateway, which is hello same location as hello resource group.</span></span> <span data-ttu-id="a0d79-171">hello 位置很重要，因為 hello 虛擬網路與公用 IP 必須在 hello 與 hello 閘道相同的位置。</span><span class="sxs-lookup"><span data-stu-id="a0d79-171">hello location is important, because hello virtual network and public IP must be in hello same location as hello gateway.</span></span>
3. <span data-ttu-id="a0d79-172">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="a0d79-172">Click **OK**.</span></span>
4. <span data-ttu-id="a0d79-173">定義 hello 虛擬網路、 子網路、 前端的 IP 和 hello 應用程式閘道的接聽程式組態。</span><span class="sxs-lookup"><span data-stu-id="a0d79-173">Define hello virtual network, subnet, front-end IP, and listener configurations for hello application gateway.</span></span> <span data-ttu-id="a0d79-174">在此案例中，hello 前端 IP 位址是**公用**，可讓它 toobe 稍後新增為端點 toohello Traffic Manager 設定檔。</span><span class="sxs-lookup"><span data-stu-id="a0d79-174">In this scenario, hello front-end IP address is **Public**, which allows it toobe added as an endpoint toohello Traffic Manager profile later on.</span></span>
5. <span data-ttu-id="a0d79-175">使用下列選項的 hello 的其中一個設定 hello 接聽程式：</span><span class="sxs-lookup"><span data-stu-id="a0d79-175">Configure hello listener with one of hello following options:</span></span>
    * <span data-ttu-id="a0d79-176">如果您使用 HTTP 時，就無須 tooconfigure。</span><span class="sxs-lookup"><span data-stu-id="a0d79-176">If you use HTTP, there is nothing tooconfigure.</span></span> <span data-ttu-id="a0d79-177">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="a0d79-177">Click **OK**.</span></span>
    * <span data-ttu-id="a0d79-178">如果您使用 HTTPS，則需要設定進一步的設定。</span><span class="sxs-lookup"><span data-stu-id="a0d79-178">If you use HTTPS, further configuration is required.</span></span> <span data-ttu-id="a0d79-179">請參閱太[建立應用程式閘道](../application-gateway/application-gateway-create-gateway-portal.md)開始於步驟 9。</span><span class="sxs-lookup"><span data-stu-id="a0d79-179">Refer too[Create an application gateway](../application-gateway/application-gateway-create-gateway-portal.md), starting at step 9.</span></span> <span data-ttu-id="a0d79-180">當您完成 hello 組態時，按一下 **確定**。</span><span class="sxs-lookup"><span data-stu-id="a0d79-180">When you have completed hello configuration, click **OK**.</span></span>

#### <a name="configure-url-routing-for-application-gateways"></a><span data-ttu-id="a0d79-181">設定應用程式閘道的 URL 路由</span><span class="sxs-lookup"><span data-stu-id="a0d79-181">Configure URL routing for application gateways</span></span>

<span data-ttu-id="a0d79-182">當您選擇的後端集區時，應用程式閘道設定與路徑規則會接受加法 tooround 環散佈 hello 要求 URL 的路徑模式。</span><span class="sxs-lookup"><span data-stu-id="a0d79-182">When you choose a back-end pool, an application gateway that's configured with a path-based rule takes a path pattern of hello request URL in addition tooround-robin distribution.</span></span> <span data-ttu-id="a0d79-183">在此案例中，我們新增路徑為基礎的規則 toodirect 任何 URL 與"/images/\*"toohello 映像的伺服器集區。</span><span class="sxs-lookup"><span data-stu-id="a0d79-183">In this scenario, we are adding a path-based rule toodirect any URL with "/images/\*" toohello image server pool.</span></span> <span data-ttu-id="a0d79-184">如需有關設定 URL 路徑為基礎的路由為應用程式的閘道，請參閱太[建立路徑為基礎的應用程式閘道規則](../application-gateway/application-gateway-create-url-route-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="a0d79-184">For more information about configuring URL path-based routing for an application gateway, refer too[Create a path-based rule for an application gateway](../application-gateway/application-gateway-create-url-route-portal.md).</span></span>

![應用程式閘道 Web 層圖表](./media/traffic-manager-load-balancing-azure/web-tier-diagram.png)

1. <span data-ttu-id="a0d79-186">從您的資源群組移 toohello hello 在 hello 前面一節中所建立的應用程式閘道執行個體。</span><span class="sxs-lookup"><span data-stu-id="a0d79-186">From your resource group, go toohello instance of hello application gateway that you created in hello preceding section.</span></span>
2. <span data-ttu-id="a0d79-187">在下**設定**，選取**後端集區**，然後選取**新增**tooadd hello 想 tooassociate 與 hello web 層後端集區的 Vm。</span><span class="sxs-lookup"><span data-stu-id="a0d79-187">Under **Settings**, select **Backend pools**, and then select **Add** tooadd hello VMs that you want tooassociate with hello web-tier back-end pools.</span></span>
3. <span data-ttu-id="a0d79-188">在 hello**新增後端集區**刀鋒視窗中，輸入 hello hello 後端集區名稱和所有 hello IP 位址位於 hello 集區中的 hello 機器。</span><span class="sxs-lookup"><span data-stu-id="a0d79-188">On hello **Add backend pool** blade, enter hello name of hello back-end pool and all hello IP addresses of hello machines that reside in hello pool.</span></span> <span data-ttu-id="a0d79-189">在此案例中，我們會連接兩個虛擬機器的後端伺服器集區。</span><span class="sxs-lookup"><span data-stu-id="a0d79-189">In this scenario, we are connecting two back-end server pools of virtual machines.</span></span>

  ![應用程式閘道「新增後端集區」刀鋒視窗](./media/traffic-manager-load-balancing-azure/s2-appgw-add-bepool.png)

4. <span data-ttu-id="a0d79-191">在下**設定**hello 應用程式閘道，請選取**規則**，然後按一下hello**路徑基本**按鈕 tooadd 規則。</span><span class="sxs-lookup"><span data-stu-id="a0d79-191">Under **Settings** of hello application gateway, select **Rules**, and then click hello **Path based** button tooadd a rule.</span></span>

  ![應用程式閘道規則「路徑型」按鈕](./media/traffic-manager-load-balancing-azure/s2-appgw-add-pathrule.png)

5. <span data-ttu-id="a0d79-193">在 hello**加入路徑為基礎的規則**刀鋒視窗中，可藉由提供下列資訊的 hello 設定 hello 規則。</span><span class="sxs-lookup"><span data-stu-id="a0d79-193">On hello **Add path-based rule** blade, configure hello rule by providing hello following information.</span></span>

   <span data-ttu-id="a0d79-194">基本設定：</span><span class="sxs-lookup"><span data-stu-id="a0d79-194">Basic settings:</span></span>

   + <span data-ttu-id="a0d79-195">**名稱**: hello 存取 hello 入口網站中的 hello 規則的好記的名稱。</span><span class="sxs-lookup"><span data-stu-id="a0d79-195">**Name**: hello friendly name of hello rule that is accessible in hello portal.</span></span>
   + <span data-ttu-id="a0d79-196">**接聽程式**: hello 規則使用的 hello 接聽程式。</span><span class="sxs-lookup"><span data-stu-id="a0d79-196">**Listener**: hello listener that is used for hello rule.</span></span>
   + <span data-ttu-id="a0d79-197">**預設 後端集區**: hello 後端集區 toobe 搭配 hello 預設規則。</span><span class="sxs-lookup"><span data-stu-id="a0d79-197">**Default backend pool**: hello back-end pool toobe used with hello default rule.</span></span>
   + <span data-ttu-id="a0d79-198">**預設的 HTTP 設定**: hello HTTP 設定 toobe 搭配 hello 預設規則。</span><span class="sxs-lookup"><span data-stu-id="a0d79-198">**Default HTTP settings**: hello HTTP settings toobe used with hello default rule.</span></span>

   <span data-ttu-id="a0d79-199">路徑型規則：</span><span class="sxs-lookup"><span data-stu-id="a0d79-199">Path-based rules:</span></span>

   + <span data-ttu-id="a0d79-200">**名稱**: hello hello 路徑為基礎的規則的好記的名稱。</span><span class="sxs-lookup"><span data-stu-id="a0d79-200">**Name**: hello friendly name of hello path-based rule.</span></span>
   + <span data-ttu-id="a0d79-201">**路徑**: hello 路徑規則用於將流量轉送。</span><span class="sxs-lookup"><span data-stu-id="a0d79-201">**Paths**: hello path rule that is used for forwarding traffic.</span></span>
   + <span data-ttu-id="a0d79-202">**後端集區**: hello 搭配此規則的後端集區 toobe。</span><span class="sxs-lookup"><span data-stu-id="a0d79-202">**Backend Pool**: hello back-end pool toobe used with this rule.</span></span>
   + <span data-ttu-id="a0d79-203">**HTTP 設定**: hello HTTP 設定 toobe 搭配此規則。</span><span class="sxs-lookup"><span data-stu-id="a0d79-203">**HTTP Setting**: hello HTTP settings toobe used with this rule.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="a0d79-204">路徑︰有效的路徑必須以 "/" 開頭。</span><span class="sxs-lookup"><span data-stu-id="a0d79-204">Paths: Valid paths must start with "/".</span></span> <span data-ttu-id="a0d79-205">hello 萬用字元"\*」 只能出現在 hello 結束。</span><span class="sxs-lookup"><span data-stu-id="a0d79-205">hello wildcard "\*" is allowed only at hello end.</span></span> <span data-ttu-id="a0d79-206">有效範例包括 /xyz、/xyz\* 或 /xyz/\*。</span><span class="sxs-lookup"><span data-stu-id="a0d79-206">Valid examples are /xyz, /xyz\*, or /xyz/\*.</span></span>

   ![應用程式閘道器「新增路徑型規則」刀鋒視窗](./media/traffic-manager-load-balancing-azure/s2-appgw-pathrule-blade.png)

### <a name="step-3-add-application-gateways-toohello-traffic-manager-endpoints"></a><span data-ttu-id="a0d79-208">步驟 3： 新增應用程式閘道 toohello 流量管理員端點</span><span class="sxs-lookup"><span data-stu-id="a0d79-208">Step 3: Add application gateways toohello Traffic Manager endpoints</span></span>

<span data-ttu-id="a0d79-209">在此案例中，Traffic Manager 會是位於不同的區域中的連接的 tooapplication 閘道 （如 hello 先前步驟中所設定）。</span><span class="sxs-lookup"><span data-stu-id="a0d79-209">In this scenario, Traffic Manager is connected tooapplication gateways (as configured in hello preceding steps) that reside in different regions.</span></span> <span data-ttu-id="a0d79-210">現在 hello 應用程式閘道的設定，hello 下一個步驟是 tooconnect 它們 tooyour Traffic Manager 設定檔。</span><span class="sxs-lookup"><span data-stu-id="a0d79-210">Now that hello application gateways are configured, hello next step is tooconnect them tooyour Traffic Manager profile.</span></span>

1. <span data-ttu-id="a0d79-211">開啟流量管理員設定檔。</span><span class="sxs-lookup"><span data-stu-id="a0d79-211">Open your Traffic Manager profile.</span></span> <span data-ttu-id="a0d79-212">在您的資源群組或搜尋 hello hello Traffic Manager 設定檔的名稱，尋找 toodo**所有資源**。</span><span class="sxs-lookup"><span data-stu-id="a0d79-212">toodo so, look in your resource group or search for hello name of hello Traffic Manager profile from **All Resources**.</span></span>
2. <span data-ttu-id="a0d79-213">Hello 左窗格中，選取**端點**，然後按一下**新增**tooadd 端點。</span><span class="sxs-lookup"><span data-stu-id="a0d79-213">In hello left pane, select **Endpoints**, and then click **Add** tooadd an endpoint.</span></span>

  ![流量管理員端點「新增」按鈕](./media/traffic-manager-load-balancing-azure/s3-tm-add-endpoint.png)

3. <span data-ttu-id="a0d79-215">在 hello**加入端點**刀鋒視窗中，輸入 hello 下列資訊來建立端點：</span><span class="sxs-lookup"><span data-stu-id="a0d79-215">On hello **Add endpoint** blade, create an endpoint by entering hello following information:</span></span>

  * <span data-ttu-id="a0d79-216">**型別**： 選取 hello tooload 平衡的端點類型。</span><span class="sxs-lookup"><span data-stu-id="a0d79-216">**Type**: Select hello type of endpoint tooload-balance.</span></span> <span data-ttu-id="a0d79-217">在此案例中，選取**Azure 端點**因為我們是否連線它 toohello 應用程式閘道器執行個體先前設定的設定。</span><span class="sxs-lookup"><span data-stu-id="a0d79-217">In this scenario, select **Azure endpoint** because we are connecting it toohello application gateway instances that were configured previously.</span></span>
  * <span data-ttu-id="a0d79-218">**名稱**： 輸入 hello hello 端點名稱。</span><span class="sxs-lookup"><span data-stu-id="a0d79-218">**Name**: Enter hello name of hello endpoint.</span></span>
  * <span data-ttu-id="a0d79-219">**目標資源類型**： 選取**公用 IP 位址**然後在**目標資源**，選取 hello 的 hello 先前設定的應用程式閘道的公用 IP。</span><span class="sxs-lookup"><span data-stu-id="a0d79-219">**Target resource type**: Select **Public IP address** and then, under **Target resource**, select hello public IP of hello application gateway that was configured previously.</span></span>

   ![流量管理員「新增端點」刀鋒視窗](./media/traffic-manager-load-balancing-azure/s3-tm-add-endpoint-blade.png)

4. <span data-ttu-id="a0d79-221">現在您可以藉由存取與您的 Traffic Manager 設定檔的 DNS hello 測試您的設定 (在此範例中： TrafficManagerScenario.trafficmanager.net)。</span><span class="sxs-lookup"><span data-stu-id="a0d79-221">Now you can test your setup by accessing it with hello DNS of your Traffic Manager profile (in this example: TrafficManagerScenario.trafficmanager.net).</span></span> <span data-ttu-id="a0d79-222">您可以重送要求、 啟動或關閉 Vm 和 web 伺服器在不同的區域中建立和變更 hello Traffic Manager 設定檔設定 tootest 設定。</span><span class="sxs-lookup"><span data-stu-id="a0d79-222">You can resend requests, bring up or bring down VMs and web servers that were created in different regions, and change hello Traffic Manager profile settings tootest your setup.</span></span>

### <a name="step-4-create-a-load-balancer"></a><span data-ttu-id="a0d79-223">步驟 4：建立負載平衡器</span><span class="sxs-lookup"><span data-stu-id="a0d79-223">Step 4: Create a load balancer</span></span>

<span data-ttu-id="a0d79-224">在此案例中，負載平衡器會將來自 hello web 層 toohello 資料庫高可用性叢集內的連接。</span><span class="sxs-lookup"><span data-stu-id="a0d79-224">In this scenario, Load Balancer distributes connections from hello web tier toohello databases within a high-availability cluster.</span></span>

<span data-ttu-id="a0d79-225">如果您的資料庫高可用性叢集使用 SQL Server AlwaysOn，請參閱太[設定一或多個永遠在可用性群組接聽程式](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md)如需逐步指示。</span><span class="sxs-lookup"><span data-stu-id="a0d79-225">If your high-availability database cluster is using SQL Server AlwaysOn, refer too[Configure one or more Always On Availability Group Listeners](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md) for step-by-step instructions.</span></span>

<span data-ttu-id="a0d79-226">如需有關如何設定內部負載平衡器的詳細資訊，請參閱[hello Azure 入口網站中建立內部負載平衡器](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="a0d79-226">For more information about configuring an internal load balancer, see [Create an Internal load balancer in hello Azure portal](../load-balancer/load-balancer-get-started-ilb-arm-portal.md).</span></span>

1. <span data-ttu-id="a0d79-227">在 hello Azure 入口網站，hello 左窗格中，按一下 **新增** > **網路** > **負載平衡器**。</span><span class="sxs-lookup"><span data-stu-id="a0d79-227">In hello Azure portal, in hello left pane, click **New** > **Networking** > **Load balancer**.</span></span>
2. <span data-ttu-id="a0d79-228">在 hello**建立負載平衡器**刀鋒視窗中，選擇您的負載平衡器的名稱。</span><span class="sxs-lookup"><span data-stu-id="a0d79-228">On hello **Create load balancer** blade, choose a name for your load balancer.</span></span>
3. <span data-ttu-id="a0d79-229">設定 hello**類型**太**內部**，然後選擇 hello 適當的虛擬網路和子網路中的 hello 負載平衡器 tooreside。</span><span class="sxs-lookup"><span data-stu-id="a0d79-229">Set hello **Type** too**Internal**, and choose hello appropriate virtual network and subnet for hello load balancer tooreside in.</span></span>
4. <span data-ttu-id="a0d79-230">在 [IP 位址指派] 下，選取 [動態] 或 [靜態]。</span><span class="sxs-lookup"><span data-stu-id="a0d79-230">Under **IP address assignment**, select either **Dynamic** or **Static**.</span></span>
5. <span data-ttu-id="a0d79-231">在下**資源群組**，選擇 hello hello 負載平衡器的資源群組。</span><span class="sxs-lookup"><span data-stu-id="a0d79-231">Under **Resource group**, choose hello resource group for hello load balancer.</span></span>
6. <span data-ttu-id="a0d79-232">在下**位置**，選擇 hello hello 負載平衡器的適當區域。</span><span class="sxs-lookup"><span data-stu-id="a0d79-232">Under **Location**, choose hello appropriate region for hello load balancer.</span></span>
7. <span data-ttu-id="a0d79-233">按一下**建立**toogenerate hello 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="a0d79-233">Click **Create** toogenerate hello load balancer.</span></span>

#### <a name="connect-a-back-end-database-tier-toohello-load-balancer"></a><span data-ttu-id="a0d79-234">連接後端資料庫層 toohello 負載平衡器</span><span class="sxs-lookup"><span data-stu-id="a0d79-234">Connect a back-end database tier toohello load balancer</span></span>

1. <span data-ttu-id="a0d79-235">從資源群組中，尋找 hello 先前步驟中所建立的 hello 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="a0d79-235">From your resource group, find hello load balancer that was created in hello previous steps.</span></span>
2. <span data-ttu-id="a0d79-236">在下**設定**，按一下 **後端集區**，然後按一下**新增**tooadd 後端集區。</span><span class="sxs-lookup"><span data-stu-id="a0d79-236">Under **Settings**, click **Backend pools**, and then click **Add** tooadd a back-end pool.</span></span>

  ![負載平衡器「新增後端集區」刀鋒視窗](./media/traffic-manager-load-balancing-azure/s4-ilb-add-bepool.png)

3. <span data-ttu-id="a0d79-238">在 hello**新增後端集區**刀鋒視窗中，輸入 hello hello 後端集區名稱。</span><span class="sxs-lookup"><span data-stu-id="a0d79-238">On hello **Add backend pool** blade, enter hello name of hello back-end pool.</span></span>
4. <span data-ttu-id="a0d79-239">加入個別的機器或可用性集 toohello 後端集區。</span><span class="sxs-lookup"><span data-stu-id="a0d79-239">Add either individual machines or an availability set toohello back-end pool.</span></span>

#### <a name="configure-a-probe"></a><span data-ttu-id="a0d79-240">設定探查</span><span class="sxs-lookup"><span data-stu-id="a0d79-240">Configure a probe</span></span>

1. <span data-ttu-id="a0d79-241">在您的負載平衡器下**設定**，選取**探查**，然後按一下**新增**tooadd 探查。</span><span class="sxs-lookup"><span data-stu-id="a0d79-241">In your load balancer, under **Settings**, select **Probes**, and then click **Add** tooadd a probe.</span></span>

 ![負載平衡器「新增探查」刀鋒視窗](./media/traffic-manager-load-balancing-azure/s4-ilb-add-probe.png)

2. <span data-ttu-id="a0d79-243">在 hello**新增探查**刀鋒視窗中，輸入 hello hello 探查的名稱。</span><span class="sxs-lookup"><span data-stu-id="a0d79-243">On hello **Add probe** blade, enter hello name for hello probe.</span></span>
3. <span data-ttu-id="a0d79-244">選取 hello**通訊協定**hello 探查。</span><span class="sxs-lookup"><span data-stu-id="a0d79-244">Select hello **Protocol** for hello probe.</span></span> <span data-ttu-id="a0d79-245">針對資料庫，您可能想要 TCP 探查，而不是 HTTP 探查。</span><span class="sxs-lookup"><span data-stu-id="a0d79-245">For a database, you might want a TCP probe rather than an HTTP probe.</span></span> <span data-ttu-id="a0d79-246">深入了解負載平衡器探查 toolearn 參照太[了解負載平衡器探查](../load-balancer/load-balancer-custom-probe-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="a0d79-246">toolearn more about load-balancer probes, refer too[Understand load balancer probes](../load-balancer/load-balancer-custom-probe-overview.md).</span></span>
4. <span data-ttu-id="a0d79-247">輸入 hello**連接埠**的您用來存取 hello 探查的資料庫 toobe。</span><span class="sxs-lookup"><span data-stu-id="a0d79-247">Enter hello **Port** of your database toobe used for accessing hello probe.</span></span>
5. <span data-ttu-id="a0d79-248">在下**間隔**，指定 tooprobe hello 應用程式的頻率。</span><span class="sxs-lookup"><span data-stu-id="a0d79-248">Under **Interval**, specify how frequently tooprobe hello application.</span></span>
6. <span data-ttu-id="a0d79-249">在下**狀況不良閾值**，指定連續探查失敗發生的 hello 後端 VM toobe 被視為狀況不良的 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="a0d79-249">Under **Unhealthy threshold**, specify hello number of continuous probe failures that must occur for hello back-end VM toobe considered unhealthy.</span></span>
7. <span data-ttu-id="a0d79-250">按一下**確定**toocreate hello 探查。</span><span class="sxs-lookup"><span data-stu-id="a0d79-250">Click **OK** toocreate hello probe.</span></span>

#### <a name="configure-hello-load-balancing-rules"></a><span data-ttu-id="a0d79-251">設定 hello 負載平衡規則</span><span class="sxs-lookup"><span data-stu-id="a0d79-251">Configure hello load-balancing rules</span></span>

1. <span data-ttu-id="a0d79-252">在下**設定**您負載平衡器中，選取**負載平衡規則**，然後按一下**新增**toocreate 規則。</span><span class="sxs-lookup"><span data-stu-id="a0d79-252">Under **Settings** of your load balancer, select **Load balancing rules**, and then click **Add** toocreate a rule.</span></span>
2. <span data-ttu-id="a0d79-253">在 hello**新增負載平衡規則**刀鋒視窗中，輸入 hello**名稱**hello 負載平衡規則。</span><span class="sxs-lookup"><span data-stu-id="a0d79-253">On hello **Add load balancing rule** blade, enter hello **Name** for hello load-balancing rule.</span></span>
3. <span data-ttu-id="a0d79-254">選擇 hello**前端 IP 位址**hello 的負載平衡器，**通訊協定**，和**連接埠**。</span><span class="sxs-lookup"><span data-stu-id="a0d79-254">Choose hello **Frontend IP Address** of hello load balancer, **Protocol**, and **Port**.</span></span>
4. <span data-ttu-id="a0d79-255">在下**後端連接埠**，指定 hello 連接埠 toobe hello 後端集區中使用。</span><span class="sxs-lookup"><span data-stu-id="a0d79-255">Under **Backend port**, specify hello port toobe used in hello back-end pool.</span></span>
5. <span data-ttu-id="a0d79-256">選取 hello**後端集區**和 hello**探查**在 hello 上一個步驟 tooapply hello 規則所建立。</span><span class="sxs-lookup"><span data-stu-id="a0d79-256">Select hello **Backend pool** and hello **Probe** that were created in hello previous steps tooapply hello rule to.</span></span>
6. <span data-ttu-id="a0d79-257">在下**工作階段持續性**，選擇您要如何 hello 工作階段 toopersist。</span><span class="sxs-lookup"><span data-stu-id="a0d79-257">Under **Session persistence**, choose how you want hello sessions toopersist.</span></span>
7. <span data-ttu-id="a0d79-258">在下**閒置逾時**，指定 hello 前的閒置逾時分鐘數。</span><span class="sxs-lookup"><span data-stu-id="a0d79-258">Under **Idle timeouts**, specify hello number of minutes before an idle timeout.</span></span>
8. <span data-ttu-id="a0d79-259">在 [浮點 IP] 下，選取 [停用] 或 [啟用]。</span><span class="sxs-lookup"><span data-stu-id="a0d79-259">Under **Floating IP**, select either **Disabled** or **Enabled**.</span></span>
9. <span data-ttu-id="a0d79-260">按一下**確定**toocreate hello 規則。</span><span class="sxs-lookup"><span data-stu-id="a0d79-260">Click **OK** toocreate hello rule.</span></span>

### <a name="step-5-connect-web-tier-vms-toohello-load-balancer"></a><span data-ttu-id="a0d79-261">步驟 5： 連接的 web 層 Vm toohello 負載平衡器</span><span class="sxs-lookup"><span data-stu-id="a0d79-261">Step 5: Connect web-tier VMs toohello load balancer</span></span>

<span data-ttu-id="a0d79-262">現在我們在 hello web 層 Vm 的任何資料庫連接執行的應用程式設定 hello IP 位址和負載平衡器前端連接埠。</span><span class="sxs-lookup"><span data-stu-id="a0d79-262">Now we configure hello IP address and load-balancer front-end port in hello applications that are running on your web-tier VMs for any database connections.</span></span> <span data-ttu-id="a0d79-263">此設定是在這些 Vm 執行的特定 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a0d79-263">This configuration is specific toohello applications that run on these VMs.</span></span> <span data-ttu-id="a0d79-264">tooconfigure hello 目的地 IP 位址和連接埠，請參閱 toohello 應用程式文件。</span><span class="sxs-lookup"><span data-stu-id="a0d79-264">tooconfigure hello destination IP address and port, refer toohello application documentation.</span></span> <span data-ttu-id="a0d79-265">toofind hello IP 位址的 hello 前端 hello Azure 入口網站中移 toohello 前端 IP 集區上 hello**負載平衡器設定**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="a0d79-265">toofind hello IP address of hello front end, in hello Azure portal, go toohello front-end IP pool on hello **Load balancer settings** blade.</span></span>

![負載平衡器「前端 IP 集區」瀏覽窗格](./media/traffic-manager-load-balancing-azure/s5-ilb-frontend-ippool.png)

## <a name="next-steps"></a><span data-ttu-id="a0d79-267">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a0d79-267">Next steps</span></span>

* [<span data-ttu-id="a0d79-268">流量管理員概觀</span><span class="sxs-lookup"><span data-stu-id="a0d79-268">Overview of Traffic Manager</span></span>](traffic-manager-overview.md)
* [<span data-ttu-id="a0d79-269">應用程式閘道概觀</span><span class="sxs-lookup"><span data-stu-id="a0d79-269">Application Gateway overview</span></span>](../application-gateway/application-gateway-introduction.md)
* [<span data-ttu-id="a0d79-270">Azure 負載平衡器概觀</span><span class="sxs-lookup"><span data-stu-id="a0d79-270">Azure Load Balancer overview</span></span>](../load-balancer/load-balancer-overview.md)
