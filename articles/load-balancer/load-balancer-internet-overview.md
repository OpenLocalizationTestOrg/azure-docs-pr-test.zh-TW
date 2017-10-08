---
title: "aaaInternet 面對負載平衡器概觀 |Microsoft 文件"
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
ms.openlocfilehash: 3514f945d69ec576ed256cdd01069491e3e43936
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="internet-facing-load-balancer-overview"></a><span data-ttu-id="1e911-104">網際網路面向的負載平衡器概觀</span><span class="sxs-lookup"><span data-stu-id="1e911-104">Internet facing load balancer overview</span></span>

<span data-ttu-id="1e911-105">Azure 負載平衡器對應 hello 公用 IP 位址和連接埠號碼的連入流量 toohello 私用 IP 位址和連接埠號碼的 hello 回應 hello 虛擬機器流量 hello 虛擬機器，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="1e911-105">Azure load balancer maps hello public IP address and port number of incoming traffic toohello private IP address and port number of hello virtual machine and vice versa for hello response traffic from hello virtual machine.</span></span> <span data-ttu-id="1e911-106">負載平衡規則可讓您 toodistribute 特定類型的多個虛擬機器或服務之間的流量。</span><span class="sxs-lookup"><span data-stu-id="1e911-106">Load balancing rules allow you toodistribute specific types of traffic between multiple virtual machines or services.</span></span> <span data-ttu-id="1e911-107">例如，您可以 hello 負載分散 web 要求流量的多個 web 伺服器或 web 角色。</span><span class="sxs-lookup"><span data-stu-id="1e911-107">For example, you can spread hello load of web request traffic across multiple web servers or web roles.</span></span>

<span data-ttu-id="1e911-108">雲端服務包含 web 角色或背景工作角色執行個體，您可以在 hello 服務定義 (.csdef) 檔中定義公用端點。</span><span class="sxs-lookup"><span data-stu-id="1e911-108">For a cloud service that contains instances of web roles or worker roles, you can define a public endpoint in hello service definition (.csdef) file.</span></span>

<span data-ttu-id="1e911-109">hello *servicedefinition.csdef*檔案包含 hello 端點組態，而且當您有 web 或背景工作角色部署多個角色執行個體，hello 負載平衡器將會為它的安裝程式。</span><span class="sxs-lookup"><span data-stu-id="1e911-109">hello *servicedefinition.csdef* file contains hello endpoint configuration and when you have multiple role instances for a web or worker role deployment, hello load balancer will be setup for it.</span></span> <span data-ttu-id="1e911-110">hello 方式 tooadd 執行個體 tooyour 雲端部署正在變更 hello hello 服務組態檔 (.csfg) 上的執行個體計數。</span><span class="sxs-lookup"><span data-stu-id="1e911-110">hello way tooadd instances tooyour cloud deployment is changing hello instance count on hello service configuration file (.csfg).</span></span>

<span data-ttu-id="1e911-111">hello 如下圖所示為 hello 公用和私人 TCP 連接埠 80 的三部虛擬機器之間共用的網路流量的負載平衡端點。</span><span class="sxs-lookup"><span data-stu-id="1e911-111">hello following figure shows a load-balanced endpoint for web traffic that is shared among three virtual machines for hello public and private TCP port of 80.</span></span> <span data-ttu-id="1e911-112">這三部虛擬機器均位在負載平衡集合中。</span><span class="sxs-lookup"><span data-stu-id="1e911-112">These three virtual machines are in a load-balanced set.</span></span>

![建立負載平衡器範例](./media/load-balancer-internet-overview/IC727496.png)

<span data-ttu-id="1e911-114">圖 1 - Web 流量的負載平衡端點</span><span class="sxs-lookup"><span data-stu-id="1e911-114">Figure 1 - Load-balanced endpoint for web traffic</span></span>

<span data-ttu-id="1e911-115">當網際網路用戶端傳送網頁要求 toohello 公用 IP 位址 hello 雲端服務的 TCP 連接埠 80 時，hello Azure 負載平衡器會將 hello hello 負載平衡集內 hello 三部虛擬機器之間的要求分散。</span><span class="sxs-lookup"><span data-stu-id="1e911-115">When Internet clients send web page requests toohello public IP address of hello cloud service on TCP port 80, hello Azure Load Balancer distributes hello requests between hello three virtual machines in hello load-balanced set.</span></span> <span data-ttu-id="1e911-116">如需有關負載平衡器演算法的詳細資訊，請參閱 hello[負載平衡器的概觀頁面](load-balancer-overview.md#load-balancer-features)。</span><span class="sxs-lookup"><span data-stu-id="1e911-116">For more information about load balancer algorithms, see hello [load balancer overview page](load-balancer-overview.md#load-balancer-features).</span></span>

<span data-ttu-id="1e911-117">根據預設，Azure Load Balancer 會在多個虛擬機器執行個體之間均分網路流量。</span><span class="sxs-lookup"><span data-stu-id="1e911-117">By default, Azure Load Balancer distributes network traffic equally among multiple virtual machine instances.</span></span> <span data-ttu-id="1e911-118">您也可以設定工作階段親和性。如需詳細資訊，請參閱[負載平衡器分配模式](load-balancer-distribution-mode.md)。</span><span class="sxs-lookup"><span data-stu-id="1e911-118">You can also configure session affinity, For more information, see [load balancer distribution mode](load-balancer-distribution-mode.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1e911-119">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1e911-119">Next steps</span></span>

<span data-ttu-id="1e911-120">深入了解[內部負載平衡器](load-balancer-internal-overview.md)toobetter 了解哪些負載平衡器是否適合您的雲端部署。</span><span class="sxs-lookup"><span data-stu-id="1e911-120">Learn about [Internal load balancer](load-balancer-internal-overview.md) toobetter understand which load balancer is a better fit for your cloud deployment.</span></span>

<span data-ttu-id="1e911-121">您也可以[開始建立網際網路面向的負載平衡器](load-balancer-get-started-internet-arm-ps.md)，以及為特定負載平衡器的網路流量行為設定[分配模式](load-balancer-distribution-mode.md)類型。</span><span class="sxs-lookup"><span data-stu-id="1e911-121">You can also [get started creating an Internet facing load balancer](load-balancer-get-started-internet-arm-ps.md) and configure what type of [distribution mode](load-balancer-distribution-mode.md) for an specific load balancer network traffic behavior.</span></span>

<span data-ttu-id="1e911-122">如果您的應用程式需要 tookeep 連線運作的負載平衡器後方的伺服器，您可以瞭解多[閒置 TCP 逾時設定的負載平衡器](load-balancer-tcp-idle-timeout.md)。</span><span class="sxs-lookup"><span data-stu-id="1e911-122">If your application needs tookeep connections alive for servers behind a load balancer, you can understand more about [idle TCP timeout settings for a load balancer](load-balancer-tcp-idle-timeout.md).</span></span> <span data-ttu-id="1e911-123">當您使用 Azure 負載平衡器，它會協助 toolearn 有關閒置連線行為。</span><span class="sxs-lookup"><span data-stu-id="1e911-123">It will help toolearn about idle connection behavior when you are using Azure Load Balancer.</span></span>
