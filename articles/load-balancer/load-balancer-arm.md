---
title: "負載平衡器的資源管理員支援 aaaAzure |Microsoft 文件"
description: "搭配使用適用於 Load Balancer 的 PowerShell 與 Azure Resource Manager。 在負載平衡器中使用範本"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: tysonn
ms.assetid: d0394f11-ee5a-4407-9d86-79c936297265
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 3c02d9382de00fefe6af8f4f8a2b7b62b344f285
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-resource-manager-support-with-azure-load-balancer"></a><span data-ttu-id="d20e7-104">搭配 Azure Load Balancer 使用 Azure Resource Manager 支援</span><span class="sxs-lookup"><span data-stu-id="d20e7-104">Using Azure Resource Manager Support with Azure Load Balancer</span></span>

<span data-ttu-id="d20e7-105">Azure 資源管理員是在 Azure 中服務的 hello 慣用的管理架構。</span><span class="sxs-lookup"><span data-stu-id="d20e7-105">Azure Resource Manager is hello preferred management framework for services in Azure.</span></span> <span data-ttu-id="d20e7-106">Azure Load Balancer 可使用以 Azure Resource Manager 為基礎的 API 和工具進行管理。</span><span class="sxs-lookup"><span data-stu-id="d20e7-106">Azure Load Balancer can be managed using Azure Resource Manager-based APIs and tools.</span></span>

## <a name="concepts"></a><span data-ttu-id="d20e7-107">概念</span><span class="sxs-lookup"><span data-stu-id="d20e7-107">Concepts</span></span>

<span data-ttu-id="d20e7-108">使用資源管理員，Azure 負載平衡器包含下列子資源的 hello:</span><span class="sxs-lookup"><span data-stu-id="d20e7-108">With Resource Manager, Azure Load Balancer contains hello following child resources:</span></span>

* <span data-ttu-id="d20e7-109">前端 IP 組態 - Load balancer 可以包括一或多個前端 IP 位址 (亦稱為虛擬 IP (VIP))。</span><span class="sxs-lookup"><span data-stu-id="d20e7-109">Front-end IP configuration – a Load balancer can include one or more front end IP addresses, otherwise known as a virtual IPs (VIPs).</span></span> <span data-ttu-id="d20e7-110">這些 IP 位址做為輸入 hello 流量。</span><span class="sxs-lookup"><span data-stu-id="d20e7-110">These IP addresses serve as ingress for hello traffic.</span></span>
* <span data-ttu-id="d20e7-111">後端位址集區-這些是 hello 虛擬機器網路介面卡 (NIC) toowhich 負載會分散到相關聯的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="d20e7-111">Back-end address pool – these are IP addresses associated with hello virtual machine Network Interface Card (NIC) toowhich load will be distributed.</span></span>
* <span data-ttu-id="d20e7-112">負載平衡規則-規則屬性對應指定的前端 IP 和連接埠組合 tooa 組的後端 IP 位址和連接埠組合。</span><span class="sxs-lookup"><span data-stu-id="d20e7-112">Load balancing rules – a rule property maps a given front end IP and port combination tooa set of back end IP addresses and port combination.</span></span> <span data-ttu-id="d20e7-113">單一負載平衡器可以有多個負載平衡規則。</span><span class="sxs-lookup"><span data-stu-id="d20e7-113">A single load balancer can have multiple load balancing rules.</span></span> <span data-ttu-id="d20e7-114">每個規則都是與 VM 相關聯的前端 IP 和連接埠以及後端 IP 和連接埠的組合。</span><span class="sxs-lookup"><span data-stu-id="d20e7-114">Each rule is a combination of a front-end IP and port and back-end IP and port associated with VMs.</span></span>
* <span data-ttu-id="d20e7-115">探查 – 探查可讓您 tookeep 追蹤 hello 的 VM 執行個體的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="d20e7-115">Probes – probes enable you tookeep track of hello health of VM instances.</span></span> <span data-ttu-id="d20e7-116">如果健全狀況探查失敗，hello VM 執行個體將會進入離輪替循環自動。</span><span class="sxs-lookup"><span data-stu-id="d20e7-116">If a health probe fails, hello VM instance will be taken out of rotation automatically.</span></span>
* <span data-ttu-id="d20e7-117">輸入的 NAT 規則-NAT 規則定義 hello 輸入的流量流經 hello 前端 IP 和分散式的 toohello 回結尾 IP。</span><span class="sxs-lookup"><span data-stu-id="d20e7-117">Inbound NAT rules – NAT rules defining hello inbound traffic flowing through hello front end IP and distributed toohello back end IP.</span></span>

![](./media/load-balancer-arm/load-balancer-arm.png)

## <a name="quickstart-templates"></a><span data-ttu-id="d20e7-118">快速入門範本</span><span class="sxs-lookup"><span data-stu-id="d20e7-118">Quickstart templates</span></span>

<span data-ttu-id="d20e7-119">Azure 資源管理員可讓您 tooprovision 使用宣告式範本的應用程式。</span><span class="sxs-lookup"><span data-stu-id="d20e7-119">Azure Resource Manager allows you tooprovision your applications using a declarative template.</span></span> <span data-ttu-id="d20e7-120">在單一的範本中，您可以部署多個服務及其相依性。</span><span class="sxs-lookup"><span data-stu-id="d20e7-120">In a single template, you can deploy multiple services along with their dependencies.</span></span> <span data-ttu-id="d20e7-121">使用 hello 相同範本 toorepeatedly 部署應用程式在每個階段中的 hello 應用程式生命週期。</span><span class="sxs-lookup"><span data-stu-id="d20e7-121">You use hello same template toorepeatedly deploy your application during every stage of hello application lifecycle.</span></span>

<span data-ttu-id="d20e7-122">範本可以包含虛擬機器、虛擬網路、可用性設定組、網路介面 (NIC)、儲存體帳戶、負載平衡器、網路安全性群組和公開 IP 的定義。</span><span class="sxs-lookup"><span data-stu-id="d20e7-122">Templates can include definitions for Virtual Machines, Virtual Networks, Availability Sets, Network Interfaces (NICs), Storage Accounts, Load Balancers, Network Security Groups, and Public IPs.</span></span> <span data-ttu-id="d20e7-123">您可以使用範本來建立複雜應用程式所需的一切。</span><span class="sxs-lookup"><span data-stu-id="d20e7-123">With templates you can create everything you need for a complex application.</span></span> <span data-ttu-id="d20e7-124">hello 範本檔案可以簽入版本控制和共同作業的內容管理系統中。</span><span class="sxs-lookup"><span data-stu-id="d20e7-124">hello template file can be checked into content management system for version control and collaboration.</span></span>

[<span data-ttu-id="d20e7-125">深入了解範本</span><span class="sxs-lookup"><span data-stu-id="d20e7-125">Learn more about templates</span></span>](../azure-resource-manager/resource-manager-template-walkthrough.md)

[<span data-ttu-id="d20e7-126">深入了解網路資源</span><span class="sxs-lookup"><span data-stu-id="d20e7-126">Learn more about Network Resources</span></span>](../virtual-network/resource-groups-networking.md)

<span data-ttu-id="d20e7-127">您可以在 [GitHub 儲存機制](https://github.com/Azure/azure-quickstart-templates) (裝載了一組社群產生的範本) 中找到使用 Azure Load Balancer 的快速入門範本。</span><span class="sxs-lookup"><span data-stu-id="d20e7-127">Quickstart templates using Azure Load Balancer can be found in a [GitHub repository](https://github.com/Azure/azure-quickstart-templates) hosting a set of community generated templates.</span></span>

<span data-ttu-id="d20e7-128">範本的範例：</span><span class="sxs-lookup"><span data-stu-id="d20e7-128">Examples of templates:</span></span>

* [<span data-ttu-id="d20e7-129">負載平衡器中的 2 部 VM 和負載平衡規則</span><span class="sxs-lookup"><span data-stu-id="d20e7-129">2 VMs in a Load Balancer and load balancing rules</span></span>](http://go.microsoft.com/fwlink/?LinkId=544799)
* [<span data-ttu-id="d20e7-130">搭配內部負載平衡器的 VNET 中的 2 部 VM 和負載平衡器規則</span><span class="sxs-lookup"><span data-stu-id="d20e7-130">2 VMs in a VNET with an Internal Load Balancer and Load Balancer rules</span></span>](http://go.microsoft.com/fwlink/?LinkId=544800)
* [<span data-ttu-id="d20e7-131">負載平衡器中的 2 個 Vm 上 hello LB 設定 NAT 規則</span><span class="sxs-lookup"><span data-stu-id="d20e7-131">2 VMs in a Load Balancer and configure NAT rules on hello LB</span></span>](http://go.microsoft.com/fwlink/?LinkId=544801)

## <a name="setting-up-azure-load-balancer-with-a-powershell-or-cli"></a><span data-ttu-id="d20e7-132">使用 PowerShell 或 CLI 設定 Azure 負載平衡器</span><span class="sxs-lookup"><span data-stu-id="d20e7-132">Setting up Azure Load Balancer with a PowerShell or CLI</span></span>

<span data-ttu-id="d20e7-133">開始使用 Azure Resource Manager Cmdlet、命令列工具和 REST API</span><span class="sxs-lookup"><span data-stu-id="d20e7-133">Get started with Azure Resource Manager cmdlets, command line tools, and REST APIs</span></span>

* <span data-ttu-id="d20e7-134">[Azure 網路 Cmdlet](https://msdn.microsoft.com/library/azure/mt163510.aspx)可以是使用的 toocreate 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="d20e7-134">[Azure Networking Cmdlets](https://msdn.microsoft.com/library/azure/mt163510.aspx) can be used toocreate a Load Balancer.</span></span>
* [<span data-ttu-id="d20e7-135">如何使用 Azure Resource Manager 負載平衡器 toocreate</span><span class="sxs-lookup"><span data-stu-id="d20e7-135">How toocreate a load balancer using Azure Resource Manager</span></span>](load-balancer-get-started-ilb-arm-ps.md)
* [<span data-ttu-id="d20e7-136">使用 Azure CLI hello 與 Azure 資源管理</span><span class="sxs-lookup"><span data-stu-id="d20e7-136">Using hello Azure CLI with Azure Resource Management</span></span>](../xplat-cli-azure-resource-manager.md)
* [<span data-ttu-id="d20e7-137">負載平衡器 REST API</span><span class="sxs-lookup"><span data-stu-id="d20e7-137">Load Balancer REST APIs</span></span>](https://msdn.microsoft.com/library/azure/mt163651.aspx)

## <a name="next-steps"></a><span data-ttu-id="d20e7-138">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d20e7-138">Next steps</span></span>

<span data-ttu-id="d20e7-139">您也可以[開始建立網際網路面向的負載平衡器](load-balancer-get-started-internet-arm-ps.md)，以及為特定負載平衡器的網路流量行為設定[分配模式](load-balancer-distribution-mode.md)類型。</span><span class="sxs-lookup"><span data-stu-id="d20e7-139">You can also [get started creating an Internet facing load balancer](load-balancer-get-started-internet-arm-ps.md) and configure what type of [distribution mode](load-balancer-distribution-mode.md) for a specific load balancer network traffic behavior.</span></span>

<span data-ttu-id="d20e7-140">深入了解如何 toomanage[閒置 TCP 逾時設定的負載平衡器](load-balancer-tcp-idle-timeout.md)。</span><span class="sxs-lookup"><span data-stu-id="d20e7-140">Learn how toomanage [idle TCP timeout settings for a load balancer](load-balancer-tcp-idle-timeout.md).</span></span> <span data-ttu-id="d20e7-141">當您的應用程式需要 tookeep 連線運作的負載平衡器後方的伺服器，這很重要。</span><span class="sxs-lookup"><span data-stu-id="d20e7-141">This is important when your application needs tookeep connections alive for servers behind a load balancer.</span></span>
