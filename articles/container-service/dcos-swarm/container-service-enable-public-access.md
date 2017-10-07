---
title: "aaaEnable access tooAzure DC/OS 容器應用程式 |Microsoft 文件"
description: "如何 tooenable 公用存取 tooDC/OS Azure 容器服務中的容器。"
services: container-service
documentationcenter: 
author: sauryadas
manager: madhana
editor: 
tags: acs, azure-container-service
keywords: "Docker、容器、微服務、Mesos、Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: 1ba251ba5a176a6a5e1c7831655164e380a62b27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-public-access-tooan-azure-container-service-application"></a><span data-ttu-id="5c7af-104">啟用公用存取 tooan Azure 容器服務應用程式</span><span class="sxs-lookup"><span data-stu-id="5c7af-104">Enable public access tooan Azure Container Service application</span></span>
<span data-ttu-id="5c7af-105">Hello ACS 在任何 DC/OS 容器[公用代理程式集區](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container)會自動公開的 toohello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="5c7af-105">Any DC/OS container in hello ACS [public agent pool](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) is automatically exposed toohello internet.</span></span> <span data-ttu-id="5c7af-106">根據預設，連接埠 **80**、**443**、**8080** 已開啟，在這些連接埠上接聽的任何 (公用) 容器皆可供存取。</span><span class="sxs-lookup"><span data-stu-id="5c7af-106">By default, ports **80**, **443**, **8080** are opened, and any (public) container listening on those ports are accessible.</span></span> <span data-ttu-id="5c7af-107">本文章將示範如何 tooopen 多連接埠 Azure 容器服務中的應用程式。</span><span class="sxs-lookup"><span data-stu-id="5c7af-107">This article shows you how tooopen more ports for your applications in Azure Container Service.</span></span>

## <a name="open-a-port-portal"></a><span data-ttu-id="5c7af-108">開啟連接埠 (入口網站)</span><span class="sxs-lookup"><span data-stu-id="5c7af-108">Open a port (portal)</span></span>
<span data-ttu-id="5c7af-109">首先，我們需要我們想要的 tooopen hello 連接埠。</span><span class="sxs-lookup"><span data-stu-id="5c7af-109">First, we need tooopen hello port we want.</span></span>

1. <span data-ttu-id="5c7af-110">登入 toohello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="5c7af-110">Log in toohello portal.</span></span>
2. <span data-ttu-id="5c7af-111">尋找您所部署的 hello 資源群組 hello Azure 容器服務。</span><span class="sxs-lookup"><span data-stu-id="5c7af-111">Find hello resource group that you deployed hello Azure Container Service to.</span></span>
3. <span data-ttu-id="5c7af-112">選取 hello 代理程式負載平衡器 (這名為類似太**XXXX 代理程式-lb XXXX**)。</span><span class="sxs-lookup"><span data-stu-id="5c7af-112">Select hello agent load balancer (which is named similar too**XXXX-agent-lb-XXXX**).</span></span>
   
    ![Azure Container Service 的負載平衡器](./media/container-service-enable-public-access/agent-load-balancer.png)
4. <span data-ttu-id="5c7af-114">依序按一下 [探查] 和 [新增]。</span><span class="sxs-lookup"><span data-stu-id="5c7af-114">Click **Probes** and then **Add**.</span></span>
   
    ![Azure Container Service 的負載平衡器探查](./media/container-service-enable-public-access/add-probe.png)
5. <span data-ttu-id="5c7af-116">填寫 hello 探查表單，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="5c7af-116">Fill out hello probe form and click **OK**.</span></span>
   
   | <span data-ttu-id="5c7af-117">欄位</span><span class="sxs-lookup"><span data-stu-id="5c7af-117">Field</span></span> | <span data-ttu-id="5c7af-118">說明</span><span class="sxs-lookup"><span data-stu-id="5c7af-118">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="5c7af-119">名稱</span><span class="sxs-lookup"><span data-stu-id="5c7af-119">Name</span></span> |<span data-ttu-id="5c7af-120">Hello 探查的描述性名稱。</span><span class="sxs-lookup"><span data-stu-id="5c7af-120">A descriptive name of hello probe.</span></span> |
   | <span data-ttu-id="5c7af-121">Port</span><span class="sxs-lookup"><span data-stu-id="5c7af-121">Port</span></span> |<span data-ttu-id="5c7af-122">hello 容器 tootest hello 連接埠。</span><span class="sxs-lookup"><span data-stu-id="5c7af-122">hello port of hello container tootest.</span></span> |
   | <span data-ttu-id="5c7af-123">Path</span><span class="sxs-lookup"><span data-stu-id="5c7af-123">Path</span></span> |<span data-ttu-id="5c7af-124">（在 HTTP 模式時） hello 相對的網站路徑 tooprobe。</span><span class="sxs-lookup"><span data-stu-id="5c7af-124">(When in HTTP mode) hello relative website path tooprobe.</span></span> <span data-ttu-id="5c7af-125">不支援 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="5c7af-125">HTTPS not supported.</span></span> |
   | <span data-ttu-id="5c7af-126">間隔</span><span class="sxs-lookup"><span data-stu-id="5c7af-126">Interval</span></span> |<span data-ttu-id="5c7af-127">嘗試 hello 探查之間的時間量以秒為單位。</span><span class="sxs-lookup"><span data-stu-id="5c7af-127">hello amount of time between probe attempts, in seconds.</span></span> |
   | <span data-ttu-id="5c7af-128">狀況不良臨界值</span><span class="sxs-lookup"><span data-stu-id="5c7af-128">Unhealthy threshold</span></span> |<span data-ttu-id="5c7af-129">考慮 hello 容器狀況不良之前，先在此連續探查次數。</span><span class="sxs-lookup"><span data-stu-id="5c7af-129">Number of consecutive probe attempts before considering hello container unhealthy.</span></span> |
6. <span data-ttu-id="5c7af-130">在 hello 代理程式負載平衡器的 hello 內容中，按一下 **負載平衡規則**然後**新增**。</span><span class="sxs-lookup"><span data-stu-id="5c7af-130">Back at hello properties of hello agent load balancer, click **Load balancing rules** and then **Add**.</span></span>
   
    ![Azure Container Service 的負載平衡器規則](./media/container-service-enable-public-access/add-balancer-rule.png)
7. <span data-ttu-id="5c7af-132">填寫 hello 負載平衡器表單，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="5c7af-132">Fill out hello load balancer form and click **OK**.</span></span>
   
   | <span data-ttu-id="5c7af-133">欄位</span><span class="sxs-lookup"><span data-stu-id="5c7af-133">Field</span></span> | <span data-ttu-id="5c7af-134">說明</span><span class="sxs-lookup"><span data-stu-id="5c7af-134">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="5c7af-135">名稱</span><span class="sxs-lookup"><span data-stu-id="5c7af-135">Name</span></span> |<span data-ttu-id="5c7af-136">Hello 負載平衡器的描述性名稱。</span><span class="sxs-lookup"><span data-stu-id="5c7af-136">A descriptive name of hello load balancer.</span></span> |
   | <span data-ttu-id="5c7af-137">Port</span><span class="sxs-lookup"><span data-stu-id="5c7af-137">Port</span></span> |<span data-ttu-id="5c7af-138">hello 公用的連入通訊埠。</span><span class="sxs-lookup"><span data-stu-id="5c7af-138">hello public incoming port.</span></span> |
   | <span data-ttu-id="5c7af-139">後端連接埠</span><span class="sxs-lookup"><span data-stu-id="5c7af-139">Backend port</span></span> |<span data-ttu-id="5c7af-140">hello 內部公用連接埠的 hello 容器 tooroute 流量。</span><span class="sxs-lookup"><span data-stu-id="5c7af-140">hello internal-public port of hello container tooroute traffic to.</span></span> |
   | <span data-ttu-id="5c7af-141">後端集區</span><span class="sxs-lookup"><span data-stu-id="5c7af-141">Backend pool</span></span> |<span data-ttu-id="5c7af-142">此集區中的 hello 容器將是此負載平衡器的 hello 目標。</span><span class="sxs-lookup"><span data-stu-id="5c7af-142">hello containers in this pool will be hello target for this load balancer.</span></span> |
   | <span data-ttu-id="5c7af-143">探查</span><span class="sxs-lookup"><span data-stu-id="5c7af-143">Probe</span></span> |<span data-ttu-id="5c7af-144">如果目標中 hello hello 探查使用 toodetermine**後端集區**狀況良好。</span><span class="sxs-lookup"><span data-stu-id="5c7af-144">hello probe used toodetermine if a target in hello **Backend pool** is healthy.</span></span> |
   | <span data-ttu-id="5c7af-145">工作階段持續性</span><span class="sxs-lookup"><span data-stu-id="5c7af-145">Session persistence</span></span> |<span data-ttu-id="5c7af-146">決定應如何從用戶端的流量處理 hello hello 工作階段期間。</span><span class="sxs-lookup"><span data-stu-id="5c7af-146">Determines how traffic from a client should be handled for hello duration of hello session.</span></span><br><br><span data-ttu-id="5c7af-147">**無**： 來自相同用戶端可以由任何容器的 hello 的後續要求。</span><span class="sxs-lookup"><span data-stu-id="5c7af-147">**None**: Successive requests from hello same client can be handled by any container.</span></span><br><span data-ttu-id="5c7af-148">**用戶端 IP**: hello 相同的用戶端 IP 由處理後續要求 hello 相同的容器。</span><span class="sxs-lookup"><span data-stu-id="5c7af-148">**Client IP**: Successive requests from hello same client IP are handled by hello same container.</span></span><br><span data-ttu-id="5c7af-149">**用戶端 IP 和通訊協定**： 來自相同用戶端 IP 和通訊協定組合都由的 hello 的後續要求 hello 相同的容器。</span><span class="sxs-lookup"><span data-stu-id="5c7af-149">**Client IP and protocol**: Successive requests from hello same client IP and protocol combination are handled by hello same container.</span></span> |
   | <span data-ttu-id="5c7af-150">閒置逾時</span><span class="sxs-lookup"><span data-stu-id="5c7af-150">Idle timeout</span></span> |<span data-ttu-id="5c7af-151">(只有 TCP)以分鐘為單位 hello TCP/HTTP 用戶端不需依賴所開啟的時間 tookeep*保持*訊息。</span><span class="sxs-lookup"><span data-stu-id="5c7af-151">(TCP only) In minutes, hello time tookeep a TCP/HTTP client open without relying on *keep-alive* messages.</span></span> |

## <a name="add-a-security-rule-portal"></a><span data-ttu-id="5c7af-152">新增安全性規則 (入口網站)</span><span class="sxs-lookup"><span data-stu-id="5c7af-152">Add a security rule (portal)</span></span>
<span data-ttu-id="5c7af-153">接下來，我們需要 tooadd 從我們已開啟的連接埠通過 hello 防火牆會路由傳送流量的安全性規則。</span><span class="sxs-lookup"><span data-stu-id="5c7af-153">Next, we need tooadd a security rule that routes traffic from our opened port through hello firewall.</span></span>

1. <span data-ttu-id="5c7af-154">登入 toohello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="5c7af-154">Log in toohello portal.</span></span>
2. <span data-ttu-id="5c7af-155">尋找您所部署的 hello 資源群組 hello Azure 容器服務。</span><span class="sxs-lookup"><span data-stu-id="5c7af-155">Find hello resource group that you deployed hello Azure Container Service to.</span></span>
3. <span data-ttu-id="5c7af-156">選取 hello**公用**代理程式的網路安全性群組 (這名為類似太**XXXX-代理程式-公用-nsg-XXXX**)。</span><span class="sxs-lookup"><span data-stu-id="5c7af-156">Select hello **public** agent network security group (which is named similar too**XXXX-agent-public-nsg-XXXX**).</span></span>
   
    ![Azure Container Service 網路安全性群組](./media/container-service-enable-public-access/agent-nsg.png)
4. <span data-ttu-id="5c7af-158">依序選取 [輸入安全性規則] 和 [新增]。</span><span class="sxs-lookup"><span data-stu-id="5c7af-158">Select **Inbound security rules** and then **Add**.</span></span>
   
    ![Azure Container Service 網路安全性群組規則](./media/container-service-enable-public-access/add-firewall-rule.png)
5. <span data-ttu-id="5c7af-160">填寫 hello 防火牆規則 tooallow 公用連接埠，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="5c7af-160">Fill out hello firewall rule tooallow your public port and click **OK**.</span></span>
   
   | <span data-ttu-id="5c7af-161">欄位</span><span class="sxs-lookup"><span data-stu-id="5c7af-161">Field</span></span> | <span data-ttu-id="5c7af-162">說明</span><span class="sxs-lookup"><span data-stu-id="5c7af-162">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="5c7af-163">名稱</span><span class="sxs-lookup"><span data-stu-id="5c7af-163">Name</span></span> |<span data-ttu-id="5c7af-164">Hello 防火牆規則的描述性名稱。</span><span class="sxs-lookup"><span data-stu-id="5c7af-164">A descriptive name of hello firewall rule.</span></span> |
   | <span data-ttu-id="5c7af-165">優先順序</span><span class="sxs-lookup"><span data-stu-id="5c7af-165">Priority</span></span> |<span data-ttu-id="5c7af-166">Hello 規則的優先順序等級。</span><span class="sxs-lookup"><span data-stu-id="5c7af-166">Priority rank for hello rule.</span></span> <span data-ttu-id="5c7af-167">hello hello 數字 hello 高 hello 優先順序。</span><span class="sxs-lookup"><span data-stu-id="5c7af-167">hello lower hello number hello higher hello priority.</span></span> |
   | <span data-ttu-id="5c7af-168">來源</span><span class="sxs-lookup"><span data-stu-id="5c7af-168">Source</span></span> |<span data-ttu-id="5c7af-169">限制 hello 連入 IP 位址範圍 toobe 允許或拒絕此規則。</span><span class="sxs-lookup"><span data-stu-id="5c7af-169">Restrict hello incoming IP address range toobe allowed or denied by this rule.</span></span> <span data-ttu-id="5c7af-170">使用**任何**toonot 指定限制。</span><span class="sxs-lookup"><span data-stu-id="5c7af-170">Use **Any** toonot specify a restriction.</span></span> |
   | <span data-ttu-id="5c7af-171">服務</span><span class="sxs-lookup"><span data-stu-id="5c7af-171">Service</span></span> |<span data-ttu-id="5c7af-172">選取一組適用此安全性規則的預先定義服務。</span><span class="sxs-lookup"><span data-stu-id="5c7af-172">Select a set of predefined services this security rule is for.</span></span> <span data-ttu-id="5c7af-173">否則使用**自訂**toocreate 自己。</span><span class="sxs-lookup"><span data-stu-id="5c7af-173">Otherwise use **Custom** toocreate your own.</span></span> |
   | <span data-ttu-id="5c7af-174">通訊協定</span><span class="sxs-lookup"><span data-stu-id="5c7af-174">Protocol</span></span> |<span data-ttu-id="5c7af-175">根據 **TCP** 或 **UDP** 限制流量。</span><span class="sxs-lookup"><span data-stu-id="5c7af-175">Restrict traffic based on **TCP** or **UDP**.</span></span> <span data-ttu-id="5c7af-176">使用**任何**toonot 指定限制。</span><span class="sxs-lookup"><span data-stu-id="5c7af-176">Use **Any** toonot specify a restriction.</span></span> |
   | <span data-ttu-id="5c7af-177">連接埠範圍</span><span class="sxs-lookup"><span data-stu-id="5c7af-177">Port range</span></span> |<span data-ttu-id="5c7af-178">當**服務**是**自訂**，指定此規則影響的連接埠範圍，hello。</span><span class="sxs-lookup"><span data-stu-id="5c7af-178">When **Service** is **Custom**, specifies hello range of ports that this rule affects.</span></span> <span data-ttu-id="5c7af-179">您可以使用單一連接埠 (例如 **80**) 或 **1024-1500** 之類的範圍。</span><span class="sxs-lookup"><span data-stu-id="5c7af-179">You can use a single port, such as **80**, or a range like **1024-1500**.</span></span> |
   | <span data-ttu-id="5c7af-180">動作</span><span class="sxs-lookup"><span data-stu-id="5c7af-180">Action</span></span> |<span data-ttu-id="5c7af-181">允許或拒絕符合 hello 準則的流量。</span><span class="sxs-lookup"><span data-stu-id="5c7af-181">Allow or deny traffic that meets hello criteria.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5c7af-182">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5c7af-182">Next steps</span></span>
<span data-ttu-id="5c7af-183">深入了解 hello 差異[公用和私用 DC/OS 代理程式](container-service-dcos-agents.md)。</span><span class="sxs-lookup"><span data-stu-id="5c7af-183">Learn about hello difference between [public and private DC/OS agents](container-service-dcos-agents.md).</span></span>

<span data-ttu-id="5c7af-184">深入了解 [管理 DC/OS 容器](container-service-mesos-marathon-ui.md)。</span><span class="sxs-lookup"><span data-stu-id="5c7af-184">Read more information about [managing your DC/OS containers](container-service-mesos-marathon-ui.md).</span></span>

