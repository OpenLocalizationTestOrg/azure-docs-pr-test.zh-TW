---
title: "啟用對 Azure DC/OS 容器應用程式的存取 | Microsoft Docs"
description: "如何在 Azure Container Service 中啟用對 DC/OS 容器的公用存取。"
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
ms.openlocfilehash: c9ef5913859cf3a55a2de2107a9304f1d28a4829
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="enable-public-access-to-an-azure-container-service-application"></a><span data-ttu-id="92d15-104">啟用 Azure Container Service 應用程式的公用存取</span><span class="sxs-lookup"><span data-stu-id="92d15-104">Enable public access to an Azure Container Service application</span></span>
<span data-ttu-id="92d15-105">ACS [公用代理程式集區](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) 中的任何 DC/OS 容器都會自動公開到網際網路。</span><span class="sxs-lookup"><span data-stu-id="92d15-105">Any DC/OS container in the ACS [public agent pool](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) is automatically exposed to the internet.</span></span> <span data-ttu-id="92d15-106">根據預設，連接埠 **80**、**443**、**8080** 已開啟，在這些連接埠上接聽的任何 (公用) 容器皆可供存取。</span><span class="sxs-lookup"><span data-stu-id="92d15-106">By default, ports **80**, **443**, **8080** are opened, and any (public) container listening on those ports are accessible.</span></span> <span data-ttu-id="92d15-107">本文將說明如何在 Azure Container Service 中開啟更多的連接埠供應用程式使用。</span><span class="sxs-lookup"><span data-stu-id="92d15-107">This article shows you how to open more ports for your applications in Azure Container Service.</span></span>

## <a name="open-a-port-portal"></a><span data-ttu-id="92d15-108">開啟連接埠 (入口網站)</span><span class="sxs-lookup"><span data-stu-id="92d15-108">Open a port (portal)</span></span>
<span data-ttu-id="92d15-109">首先，我們必須開啟所需的連接埠。</span><span class="sxs-lookup"><span data-stu-id="92d15-109">First, we need to open the port we want.</span></span>

1. <span data-ttu-id="92d15-110">登入入口網站。</span><span class="sxs-lookup"><span data-stu-id="92d15-110">Log in to the portal.</span></span>
2. <span data-ttu-id="92d15-111">尋找 Azure Container Service 所部署到的資源群組。</span><span class="sxs-lookup"><span data-stu-id="92d15-111">Find the resource group that you deployed the Azure Container Service to.</span></span>
3. <span data-ttu-id="92d15-112">選取代理程式的負載平衡器 (其名稱類似 **XXXX-agent-lb-XXXX**)。</span><span class="sxs-lookup"><span data-stu-id="92d15-112">Select the agent load balancer (which is named similar to **XXXX-agent-lb-XXXX**).</span></span>
   
    ![Azure Container Service 的負載平衡器](./media/container-service-enable-public-access/agent-load-balancer.png)
4. <span data-ttu-id="92d15-114">依序按一下 [探查] 和 [新增]。</span><span class="sxs-lookup"><span data-stu-id="92d15-114">Click **Probes** and then **Add**.</span></span>
   
    ![Azure Container Service 的負載平衡器探查](./media/container-service-enable-public-access/add-probe.png)
5. <span data-ttu-id="92d15-116">填寫探查表單，然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="92d15-116">Fill out the probe form and click **OK**.</span></span>
   
   | <span data-ttu-id="92d15-117">欄位</span><span class="sxs-lookup"><span data-stu-id="92d15-117">Field</span></span> | <span data-ttu-id="92d15-118">說明</span><span class="sxs-lookup"><span data-stu-id="92d15-118">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="92d15-119">名稱</span><span class="sxs-lookup"><span data-stu-id="92d15-119">Name</span></span> |<span data-ttu-id="92d15-120">探查的描述性名稱。</span><span class="sxs-lookup"><span data-stu-id="92d15-120">A descriptive name of the probe.</span></span> |
   | <span data-ttu-id="92d15-121">連接埠</span><span class="sxs-lookup"><span data-stu-id="92d15-121">Port</span></span> |<span data-ttu-id="92d15-122">要測試之容器的連接埠。</span><span class="sxs-lookup"><span data-stu-id="92d15-122">The port of the container to test.</span></span> |
   | <span data-ttu-id="92d15-123">Path</span><span class="sxs-lookup"><span data-stu-id="92d15-123">Path</span></span> |<span data-ttu-id="92d15-124">(處於 HTTP 模式時) 探查的相對網站路徑。</span><span class="sxs-lookup"><span data-stu-id="92d15-124">(When in HTTP mode) The relative website path to probe.</span></span> <span data-ttu-id="92d15-125">不支援 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="92d15-125">HTTPS not supported.</span></span> |
   | <span data-ttu-id="92d15-126">間隔</span><span class="sxs-lookup"><span data-stu-id="92d15-126">Interval</span></span> |<span data-ttu-id="92d15-127">探查嘗試間隔的時間量 (秒)。</span><span class="sxs-lookup"><span data-stu-id="92d15-127">The amount of time between probe attempts, in seconds.</span></span> |
   | <span data-ttu-id="92d15-128">狀況不良臨界值</span><span class="sxs-lookup"><span data-stu-id="92d15-128">Unhealthy threshold</span></span> |<span data-ttu-id="92d15-129">在將容器視為狀況不良之前的連續探查嘗試次數。</span><span class="sxs-lookup"><span data-stu-id="92d15-129">Number of consecutive probe attempts before considering the container unhealthy.</span></span> |
6. <span data-ttu-id="92d15-130">回到代理程式負載平衡器的屬性中，依序按一下 [負載平衡規則] 和 [新增]。</span><span class="sxs-lookup"><span data-stu-id="92d15-130">Back at the properties of the agent load balancer, click **Load balancing rules** and then **Add**.</span></span>
   
    ![Azure Container Service 的負載平衡器規則](./media/container-service-enable-public-access/add-balancer-rule.png)
7. <span data-ttu-id="92d15-132">填寫負載平衡器表單，然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="92d15-132">Fill out the load balancer form and click **OK**.</span></span>
   
   | <span data-ttu-id="92d15-133">欄位</span><span class="sxs-lookup"><span data-stu-id="92d15-133">Field</span></span> | <span data-ttu-id="92d15-134">說明</span><span class="sxs-lookup"><span data-stu-id="92d15-134">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="92d15-135">名稱</span><span class="sxs-lookup"><span data-stu-id="92d15-135">Name</span></span> |<span data-ttu-id="92d15-136">負載平衡器的描述性名稱。</span><span class="sxs-lookup"><span data-stu-id="92d15-136">A descriptive name of the load balancer.</span></span> |
   | <span data-ttu-id="92d15-137">連接埠</span><span class="sxs-lookup"><span data-stu-id="92d15-137">Port</span></span> |<span data-ttu-id="92d15-138">公用的連入通訊埠。</span><span class="sxs-lookup"><span data-stu-id="92d15-138">The public incoming port.</span></span> |
   | <span data-ttu-id="92d15-139">後端連接埠</span><span class="sxs-lookup"><span data-stu-id="92d15-139">Backend port</span></span> |<span data-ttu-id="92d15-140">要將流量路由傳送到之容器的內部對公用連接埠。</span><span class="sxs-lookup"><span data-stu-id="92d15-140">The internal-public port of the container to route traffic to.</span></span> |
   | <span data-ttu-id="92d15-141">後端集區</span><span class="sxs-lookup"><span data-stu-id="92d15-141">Backend pool</span></span> |<span data-ttu-id="92d15-142">此集區中的容器將會是此負載平衡器的目標。</span><span class="sxs-lookup"><span data-stu-id="92d15-142">The containers in this pool will be the target for this load balancer.</span></span> |
   | <span data-ttu-id="92d15-143">探查</span><span class="sxs-lookup"><span data-stu-id="92d15-143">Probe</span></span> |<span data-ttu-id="92d15-144">用來判斷 **後端集區** 中的目標是否狀況良好的探查。</span><span class="sxs-lookup"><span data-stu-id="92d15-144">The probe used to determine if a target in the **Backend pool** is healthy.</span></span> |
   | <span data-ttu-id="92d15-145">工作階段持續性</span><span class="sxs-lookup"><span data-stu-id="92d15-145">Session persistence</span></span> |<span data-ttu-id="92d15-146">決定針對工作階段的持續時間，應該如何處理來自用戶端的流量。</span><span class="sxs-lookup"><span data-stu-id="92d15-146">Determines how traffic from a client should be handled for the duration of the session.</span></span><br><br><span data-ttu-id="92d15-147">**無**：來自相同用戶端的後續要求可以由任何容器處理。</span><span class="sxs-lookup"><span data-stu-id="92d15-147">**None**: Successive requests from the same client can be handled by any container.</span></span><br><span data-ttu-id="92d15-148">**用戶端 IP**：來自相同用戶端 IP 的後續要求會由相同容器處理。</span><span class="sxs-lookup"><span data-stu-id="92d15-148">**Client IP**: Successive requests from the same client IP are handled by the same container.</span></span><br><span data-ttu-id="92d15-149">**用戶端 IP 和通訊協定**：來自相同用戶端 IP 和通訊協定組合的後續要求會由相同容器處理。</span><span class="sxs-lookup"><span data-stu-id="92d15-149">**Client IP and protocol**: Successive requests from the same client IP and protocol combination are handled by the same container.</span></span> |
   | <span data-ttu-id="92d15-150">閒置逾時</span><span class="sxs-lookup"><span data-stu-id="92d15-150">Idle timeout</span></span> |<span data-ttu-id="92d15-151">(僅限 TCP) 讓 TCP/HTTP 用戶端保持開啟，而不依賴「keep-alive」  訊息的時間，以分鐘為單位。</span><span class="sxs-lookup"><span data-stu-id="92d15-151">(TCP only) In minutes, the time to keep a TCP/HTTP client open without relying on *keep-alive* messages.</span></span> |

## <a name="add-a-security-rule-portal"></a><span data-ttu-id="92d15-152">新增安全性規則 (入口網站)</span><span class="sxs-lookup"><span data-stu-id="92d15-152">Add a security rule (portal)</span></span>
<span data-ttu-id="92d15-153">接下來，我們需要新增會從開啟的連接埠通過防火牆路由傳送流量的安全性規則。</span><span class="sxs-lookup"><span data-stu-id="92d15-153">Next, we need to add a security rule that routes traffic from our opened port through the firewall.</span></span>

1. <span data-ttu-id="92d15-154">登入入口網站。</span><span class="sxs-lookup"><span data-stu-id="92d15-154">Log in to the portal.</span></span>
2. <span data-ttu-id="92d15-155">尋找 Azure Container Service 所部署到的資源群組。</span><span class="sxs-lookup"><span data-stu-id="92d15-155">Find the resource group that you deployed the Azure Container Service to.</span></span>
3. <span data-ttu-id="92d15-156">選取**公用**代理程式網路安全性群組 (其名稱類似 **XXXX-agent-public-nsg-XXXX**)。</span><span class="sxs-lookup"><span data-stu-id="92d15-156">Select the **public** agent network security group (which is named similar to **XXXX-agent-public-nsg-XXXX**).</span></span>
   
    ![Azure Container Service 網路安全性群組](./media/container-service-enable-public-access/agent-nsg.png)
4. <span data-ttu-id="92d15-158">依序選取 [輸入安全性規則] 和 [新增]。</span><span class="sxs-lookup"><span data-stu-id="92d15-158">Select **Inbound security rules** and then **Add**.</span></span>
   
    ![Azure Container Service 網路安全性群組規則](./media/container-service-enable-public-access/add-firewall-rule.png)
5. <span data-ttu-id="92d15-160">填寫防火牆規則以允許公用連接埠，然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="92d15-160">Fill out the firewall rule to allow your public port and click **OK**.</span></span>
   
   | <span data-ttu-id="92d15-161">欄位</span><span class="sxs-lookup"><span data-stu-id="92d15-161">Field</span></span> | <span data-ttu-id="92d15-162">說明</span><span class="sxs-lookup"><span data-stu-id="92d15-162">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="92d15-163">名稱</span><span class="sxs-lookup"><span data-stu-id="92d15-163">Name</span></span> |<span data-ttu-id="92d15-164">防火牆規則的描述性名稱。</span><span class="sxs-lookup"><span data-stu-id="92d15-164">A descriptive name of the firewall rule.</span></span> |
   | <span data-ttu-id="92d15-165">優先順序</span><span class="sxs-lookup"><span data-stu-id="92d15-165">Priority</span></span> |<span data-ttu-id="92d15-166">規則的優先順序排名。</span><span class="sxs-lookup"><span data-stu-id="92d15-166">Priority rank for the rule.</span></span> <span data-ttu-id="92d15-167">編號愈低，優先順序就愈高。</span><span class="sxs-lookup"><span data-stu-id="92d15-167">The lower the number the higher the priority.</span></span> |
   | <span data-ttu-id="92d15-168">來源</span><span class="sxs-lookup"><span data-stu-id="92d15-168">Source</span></span> |<span data-ttu-id="92d15-169">限制此規則要允許或拒絕的連入 IP 位址範圍。</span><span class="sxs-lookup"><span data-stu-id="92d15-169">Restrict the incoming IP address range to be allowed or denied by this rule.</span></span> <span data-ttu-id="92d15-170">使用 **任何** 即可不指定限制。</span><span class="sxs-lookup"><span data-stu-id="92d15-170">Use **Any** to not specify a restriction.</span></span> |
   | <span data-ttu-id="92d15-171">服務</span><span class="sxs-lookup"><span data-stu-id="92d15-171">Service</span></span> |<span data-ttu-id="92d15-172">選取一組適用此安全性規則的預先定義服務。</span><span class="sxs-lookup"><span data-stu-id="92d15-172">Select a set of predefined services this security rule is for.</span></span> <span data-ttu-id="92d15-173">否則，使用 **自訂** 建立自己的服務。</span><span class="sxs-lookup"><span data-stu-id="92d15-173">Otherwise use **Custom** to create your own.</span></span> |
   | <span data-ttu-id="92d15-174">通訊協定</span><span class="sxs-lookup"><span data-stu-id="92d15-174">Protocol</span></span> |<span data-ttu-id="92d15-175">根據 **TCP** 或 **UDP** 限制流量。</span><span class="sxs-lookup"><span data-stu-id="92d15-175">Restrict traffic based on **TCP** or **UDP**.</span></span> <span data-ttu-id="92d15-176">使用 **任何** 即可不指定限制。</span><span class="sxs-lookup"><span data-stu-id="92d15-176">Use **Any** to not specify a restriction.</span></span> |
   | <span data-ttu-id="92d15-177">連接埠範圍</span><span class="sxs-lookup"><span data-stu-id="92d15-177">Port range</span></span> |<span data-ttu-id="92d15-178">當**服務**是**自訂**時，指定此規則會影響的連接埠範圍。</span><span class="sxs-lookup"><span data-stu-id="92d15-178">When **Service** is **Custom**, specifies the range of ports that this rule affects.</span></span> <span data-ttu-id="92d15-179">您可以使用單一連接埠 (例如 **80**) 或 **1024-1500** 之類的範圍。</span><span class="sxs-lookup"><span data-stu-id="92d15-179">You can use a single port, such as **80**, or a range like **1024-1500**.</span></span> |
   | <span data-ttu-id="92d15-180">動作</span><span class="sxs-lookup"><span data-stu-id="92d15-180">Action</span></span> |<span data-ttu-id="92d15-181">允許或拒絕符合條件的流量。</span><span class="sxs-lookup"><span data-stu-id="92d15-181">Allow or deny traffic that meets the criteria.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="92d15-182">後續步驟</span><span class="sxs-lookup"><span data-stu-id="92d15-182">Next steps</span></span>
<span data-ttu-id="92d15-183">了解 [公用和私用 DC/OS 代理程式](container-service-dcos-agents.md)之間的差異。</span><span class="sxs-lookup"><span data-stu-id="92d15-183">Learn about the difference between [public and private DC/OS agents](container-service-dcos-agents.md).</span></span>

<span data-ttu-id="92d15-184">深入了解 [管理 DC/OS 容器](container-service-mesos-marathon-ui.md)。</span><span class="sxs-lookup"><span data-stu-id="92d15-184">Read more information about [managing your DC/OS containers](container-service-mesos-marathon-ui.md).</span></span>

