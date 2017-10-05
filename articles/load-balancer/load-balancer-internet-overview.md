---
title: "網際網路面向的負載平衡器概觀 | Microsoft Docs"
description: "網際網路面向的負載平衡器及其功能的概觀。 負載平衡器如何作用於使用虛擬機器和雲端服務的 Azure。"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: tysonn
ms.assetid: 529b37aa-a45c-41d1-8877-fee8cc1fa375
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: c420b38fbe8054bc4b701f89ebc417677ca47a27
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="internet-facing-load-balancer-overview"></a><span data-ttu-id="286fd-104">網際網路面向的負載平衡器概觀</span><span class="sxs-lookup"><span data-stu-id="286fd-104">Internet facing load balancer overview</span></span>

<span data-ttu-id="286fd-105">Azure 負載平衡器將連入流量的公用 IP 位址和連接埠號碼對應至虛擬機器的私人 IP 位址和連接埠號碼，來自虛擬機器的回應流量也是如此。</span><span class="sxs-lookup"><span data-stu-id="286fd-105">Azure load balancer maps the public IP address and port number of incoming traffic to the private IP address and port number of the virtual machine and vice versa for the response traffic from the virtual machine.</span></span> <span data-ttu-id="286fd-106">負載平衡規則可讓您將特定類型的流量分配至多個虛擬機器或服務。</span><span class="sxs-lookup"><span data-stu-id="286fd-106">Load balancing rules allow you to distribute specific types of traffic between multiple virtual machines or services.</span></span> <span data-ttu-id="286fd-107">例如，您可以將 Web 要求的流量負載分散在多個 Web 伺服器或 Web 角色。</span><span class="sxs-lookup"><span data-stu-id="286fd-107">For example, you can spread the load of web request traffic across multiple web servers or web roles.</span></span>

<span data-ttu-id="286fd-108">對於包含 Web 角色或背景工作角色執行個體的雲端服務，您可以在服務定義 (.csdef) 檔案中定義公用端點。</span><span class="sxs-lookup"><span data-stu-id="286fd-108">For a cloud service that contains instances of web roles or worker roles, you can define a public endpoint in the service definition (.csdef) file.</span></span>

<span data-ttu-id="286fd-109">*servicedefinition.csdef* 檔案將包含端點組態，而當一個 Web 或背景工作角色部署具有多個角色執行個體時，負載平衡器將會針對它進行設定。</span><span class="sxs-lookup"><span data-stu-id="286fd-109">The *servicedefinition.csdef* file contains the endpoint configuration and when you have multiple role instances for a web or worker role deployment, the load balancer will be setup for it.</span></span> <span data-ttu-id="286fd-110">將執行個體加入至雲端部署的方法就是變更服務組態檔 (.csfg) 上的執行個體計數。</span><span class="sxs-lookup"><span data-stu-id="286fd-110">The way to add instances to your cloud deployment is changing the instance count on the service configuration file (.csfg).</span></span>

<span data-ttu-id="286fd-111">下圖顯示在三部虛擬機器中共用，且公用和私人 TCP 通訊埠均為 80 的 Web 流量負載平衡端點。</span><span class="sxs-lookup"><span data-stu-id="286fd-111">The following figure shows a load-balanced endpoint for web traffic that is shared among three virtual machines for the public and private TCP port of 80.</span></span> <span data-ttu-id="286fd-112">這三部虛擬機器均位在負載平衡集合中。</span><span class="sxs-lookup"><span data-stu-id="286fd-112">These three virtual machines are in a load-balanced set.</span></span>

![建立負載平衡器範例](./media/load-balancer-internet-overview/IC727496.png)

<span data-ttu-id="286fd-114">圖 1 - Web 流量的負載平衡端點</span><span class="sxs-lookup"><span data-stu-id="286fd-114">Figure 1 - Load-balanced endpoint for web traffic</span></span>

<span data-ttu-id="286fd-115">當網際網路用戶端在 TCP 通訊埠 80 上傳送網頁要求至雲端服務的公用 IP 位址時，Azure Load Balancer 會在負載平衡集中，將要求分配至這三部虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="286fd-115">When Internet clients send web page requests to the public IP address of the cloud service on TCP port 80, the Azure Load Balancer distributes the requests between the three virtual machines in the load-balanced set.</span></span> <span data-ttu-id="286fd-116">如需負載平衡器演算法的詳細資訊，請參閱[負載平衡器概觀頁面](load-balancer-overview.md#load-balancer-features)。</span><span class="sxs-lookup"><span data-stu-id="286fd-116">For more information about load balancer algorithms, see the [load balancer overview page](load-balancer-overview.md#load-balancer-features).</span></span>

<span data-ttu-id="286fd-117">根據預設，Azure Load Balancer 會在多個虛擬機器執行個體之間均分網路流量。</span><span class="sxs-lookup"><span data-stu-id="286fd-117">By default, Azure Load Balancer distributes network traffic equally among multiple virtual machine instances.</span></span> <span data-ttu-id="286fd-118">您也可以設定工作階段親和性。如需詳細資訊，請參閱[負載平衡器分配模式](load-balancer-distribution-mode.md)。</span><span class="sxs-lookup"><span data-stu-id="286fd-118">You can also configure session affinity, For more information, see [load balancer distribution mode](load-balancer-distribution-mode.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="286fd-119">後續步驟</span><span class="sxs-lookup"><span data-stu-id="286fd-119">Next steps</span></span>

<span data-ttu-id="286fd-120">了解[內部負載平衡器](load-balancer-internal-overview.md)，以深入了解哪一種負載平衡器較適合您的雲端部署。</span><span class="sxs-lookup"><span data-stu-id="286fd-120">Learn about [Internal load balancer](load-balancer-internal-overview.md) to better understand which load balancer is a better fit for your cloud deployment.</span></span>

<span data-ttu-id="286fd-121">您也可以[開始建立網際網路面向的負載平衡器](load-balancer-get-started-internet-arm-ps.md)，以及為特定負載平衡器的網路流量行為設定[分配模式](load-balancer-distribution-mode.md)類型。</span><span class="sxs-lookup"><span data-stu-id="286fd-121">You can also [get started creating an Internet facing load balancer](load-balancer-get-started-internet-arm-ps.md) and configure what type of [distribution mode](load-balancer-distribution-mode.md) for an specific load balancer network traffic behavior.</span></span>

<span data-ttu-id="286fd-122">如果您的應用程式需要讓負載平衡器後方的伺服器保持連接狀態，您可以深入了解 [負載平衡器的閒置 TCP 逾時設定](load-balancer-tcp-idle-timeout.md)。</span><span class="sxs-lookup"><span data-stu-id="286fd-122">If your application needs to keep connections alive for servers behind a load balancer, you can understand more about [idle TCP timeout settings for a load balancer](load-balancer-tcp-idle-timeout.md).</span></span> <span data-ttu-id="286fd-123">當您使用 Azure 負載平衡器時，該文章可幫助您了解閒置連接行為。</span><span class="sxs-lookup"><span data-stu-id="286fd-123">It will help to learn about idle connection behavior when you are using Azure Load Balancer.</span></span>
