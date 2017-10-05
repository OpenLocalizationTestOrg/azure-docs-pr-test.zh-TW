---
title: "Azure Resource Manager 的 Load Balancer 支援 | Microsoft Docs"
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
ms.openlocfilehash: d06c924f384a2684b5a91c202039c581796c1091
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="using-azure-resource-manager-support-with-azure-load-balancer"></a><span data-ttu-id="e14c4-104">搭配 Azure Load Balancer 使用 Azure Resource Manager 支援</span><span class="sxs-lookup"><span data-stu-id="e14c4-104">Using Azure Resource Manager Support with Azure Load Balancer</span></span>

<span data-ttu-id="e14c4-105">Azure Resource Manager 是 Azure 中慣用的服務管理架構。</span><span class="sxs-lookup"><span data-stu-id="e14c4-105">Azure Resource Manager is the preferred management framework for services in Azure.</span></span> <span data-ttu-id="e14c4-106">Azure Load Balancer 可使用以 Azure Resource Manager 為基礎的 API 和工具進行管理。</span><span class="sxs-lookup"><span data-stu-id="e14c4-106">Azure Load Balancer can be managed using Azure Resource Manager-based APIs and tools.</span></span>

## <a name="concepts"></a><span data-ttu-id="e14c4-107">概念</span><span class="sxs-lookup"><span data-stu-id="e14c4-107">Concepts</span></span>

<span data-ttu-id="e14c4-108">使用 Resource Manager 時，Azure Load Balancer 會包含下列子資源：</span><span class="sxs-lookup"><span data-stu-id="e14c4-108">With Resource Manager, Azure Load Balancer contains the following child resources:</span></span>

* <span data-ttu-id="e14c4-109">前端 IP 組態 - Load balancer 可以包括一或多個前端 IP 位址 (亦稱為虛擬 IP (VIP))。</span><span class="sxs-lookup"><span data-stu-id="e14c4-109">Front-end IP configuration – a Load balancer can include one or more front end IP addresses, otherwise known as a virtual IPs (VIPs).</span></span> <span data-ttu-id="e14c4-110">這些 IP 位址做為流量的輸入。</span><span class="sxs-lookup"><span data-stu-id="e14c4-110">These IP addresses serve as ingress for the traffic.</span></span>
* <span data-ttu-id="e14c4-111">後端位址集區 - 這些是與虛擬機器網路介面卡 (NIC) 相關聯的 IP 位址，而負載會散發到那些虛擬機器網路介面卡。</span><span class="sxs-lookup"><span data-stu-id="e14c4-111">Back-end address pool – these are IP addresses associated with the virtual machine Network Interface Card (NIC) to which load will be distributed.</span></span>
* <span data-ttu-id="e14c4-112">負載平衡規則 - 規則屬性會將指定的前端 IP 與連接埠組合對應到一組後端 IP 位址與連接埠組合。</span><span class="sxs-lookup"><span data-stu-id="e14c4-112">Load balancing rules – a rule property maps a given front end IP and port combination to a set of back end IP addresses and port combination.</span></span> <span data-ttu-id="e14c4-113">單一負載平衡器可以有多個負載平衡規則。</span><span class="sxs-lookup"><span data-stu-id="e14c4-113">A single load balancer can have multiple load balancing rules.</span></span> <span data-ttu-id="e14c4-114">每個規則都是與 VM 相關聯的前端 IP 和連接埠以及後端 IP 和連接埠的組合。</span><span class="sxs-lookup"><span data-stu-id="e14c4-114">Each rule is a combination of a front-end IP and port and back-end IP and port associated with VMs.</span></span>
* <span data-ttu-id="e14c4-115">探查 - 探查可讓您追蹤 VM 執行個體的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="e14c4-115">Probes – probes enable you to keep track of the health of VM instances.</span></span> <span data-ttu-id="e14c4-116">如果健全狀況探查失敗，則 VM 執行個體不會自動進入輪替。</span><span class="sxs-lookup"><span data-stu-id="e14c4-116">If a health probe fails, the VM instance will be taken out of rotation automatically.</span></span>
* <span data-ttu-id="e14c4-117">輸入 NAT 規則 - 定義流經前端 IP 並散發到後端 IP 之輸入流量的 NAT 規則。</span><span class="sxs-lookup"><span data-stu-id="e14c4-117">Inbound NAT rules – NAT rules defining the inbound traffic flowing through the front end IP and distributed to the back end IP.</span></span>

![](./media/load-balancer-arm/load-balancer-arm.png)

## <a name="quickstart-templates"></a><span data-ttu-id="e14c4-118">快速入門範本</span><span class="sxs-lookup"><span data-stu-id="e14c4-118">Quickstart templates</span></span>

<span data-ttu-id="e14c4-119">Azure 資源管理員可讓您使用宣告式範本佈建應用程式。</span><span class="sxs-lookup"><span data-stu-id="e14c4-119">Azure Resource Manager allows you to provision your applications using a declarative template.</span></span> <span data-ttu-id="e14c4-120">在單一的範本中，您可以部署多個服務及其相依性。</span><span class="sxs-lookup"><span data-stu-id="e14c4-120">In a single template, you can deploy multiple services along with their dependencies.</span></span> <span data-ttu-id="e14c4-121">您可以使用相同的範本，在應用程式生命週期的每個階段重複部署應用程式。</span><span class="sxs-lookup"><span data-stu-id="e14c4-121">You use the same template to repeatedly deploy your application during every stage of the application lifecycle.</span></span>

<span data-ttu-id="e14c4-122">範本可以包含虛擬機器、虛擬網路、可用性設定組、網路介面 (NIC)、儲存體帳戶、負載平衡器、網路安全性群組和公開 IP 的定義。</span><span class="sxs-lookup"><span data-stu-id="e14c4-122">Templates can include definitions for Virtual Machines, Virtual Networks, Availability Sets, Network Interfaces (NICs), Storage Accounts, Load Balancers, Network Security Groups, and Public IPs.</span></span> <span data-ttu-id="e14c4-123">您可以使用範本來建立複雜應用程式所需的一切。</span><span class="sxs-lookup"><span data-stu-id="e14c4-123">With templates you can create everything you need for a complex application.</span></span> <span data-ttu-id="e14c4-124">您可以將範本檔案簽入內容管理系統中，以進行版本控制和共同作業。</span><span class="sxs-lookup"><span data-stu-id="e14c4-124">The template file can be checked into content management system for version control and collaboration.</span></span>

[<span data-ttu-id="e14c4-125">深入了解範本</span><span class="sxs-lookup"><span data-stu-id="e14c4-125">Learn more about templates</span></span>](../azure-resource-manager/resource-manager-template-walkthrough.md)

[<span data-ttu-id="e14c4-126">深入了解網路資源</span><span class="sxs-lookup"><span data-stu-id="e14c4-126">Learn more about Network Resources</span></span>](../virtual-network/resource-groups-networking.md)

<span data-ttu-id="e14c4-127">您可以在 [GitHub 儲存機制](https://github.com/Azure/azure-quickstart-templates) (裝載了一組社群產生的範本) 中找到使用 Azure Load Balancer 的快速入門範本。</span><span class="sxs-lookup"><span data-stu-id="e14c4-127">Quickstart templates using Azure Load Balancer can be found in a [GitHub repository](https://github.com/Azure/azure-quickstart-templates) hosting a set of community generated templates.</span></span>

<span data-ttu-id="e14c4-128">範本的範例：</span><span class="sxs-lookup"><span data-stu-id="e14c4-128">Examples of templates:</span></span>

* [<span data-ttu-id="e14c4-129">負載平衡器中的 2 部 VM 和負載平衡規則</span><span class="sxs-lookup"><span data-stu-id="e14c4-129">2 VMs in a Load Balancer and load balancing rules</span></span>](http://go.microsoft.com/fwlink/?LinkId=544799)
* [<span data-ttu-id="e14c4-130">搭配內部負載平衡器的 VNET 中的 2 部 VM 和負載平衡器規則</span><span class="sxs-lookup"><span data-stu-id="e14c4-130">2 VMs in a VNET with an Internal Load Balancer and Load Balancer rules</span></span>](http://go.microsoft.com/fwlink/?LinkId=544800)
* [<span data-ttu-id="e14c4-131">負載平衡器中的 2 部 VM，並在 LB 上設定 NAT 規則</span><span class="sxs-lookup"><span data-stu-id="e14c4-131">2 VMs in a Load Balancer and configure NAT rules on the LB</span></span>](http://go.microsoft.com/fwlink/?LinkId=544801)

## <a name="setting-up-azure-load-balancer-with-a-powershell-or-cli"></a><span data-ttu-id="e14c4-132">使用 PowerShell 或 CLI 設定 Azure 負載平衡器</span><span class="sxs-lookup"><span data-stu-id="e14c4-132">Setting up Azure Load Balancer with a PowerShell or CLI</span></span>

<span data-ttu-id="e14c4-133">開始使用 Azure Resource Manager Cmdlet、命令列工具和 REST API</span><span class="sxs-lookup"><span data-stu-id="e14c4-133">Get started with Azure Resource Manager cmdlets, command line tools, and REST APIs</span></span>

* <span data-ttu-id="e14c4-134">[Azure 網路 Cmdlet](https://msdn.microsoft.com/library/azure/mt163510.aspx) 可用來建立負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="e14c4-134">[Azure Networking Cmdlets](https://msdn.microsoft.com/library/azure/mt163510.aspx) can be used to create a Load Balancer.</span></span>
* [<span data-ttu-id="e14c4-135">如何使用 Azure 資源管理員建立負載平衡器</span><span class="sxs-lookup"><span data-stu-id="e14c4-135">How to create a load balancer using Azure Resource Manager</span></span>](load-balancer-get-started-ilb-arm-ps.md)
* [<span data-ttu-id="e14c4-136">搭配使用 Azure 資源管理與 Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e14c4-136">Using the Azure CLI with Azure Resource Management</span></span>](../xplat-cli-azure-resource-manager.md)
* [<span data-ttu-id="e14c4-137">負載平衡器 REST API</span><span class="sxs-lookup"><span data-stu-id="e14c4-137">Load Balancer REST APIs</span></span>](https://msdn.microsoft.com/library/azure/mt163651.aspx)

## <a name="next-steps"></a><span data-ttu-id="e14c4-138">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e14c4-138">Next steps</span></span>

<span data-ttu-id="e14c4-139">您也可以[開始建立網際網路面向的負載平衡器](load-balancer-get-started-internet-arm-ps.md)，以及為特定負載平衡器的網路流量行為設定[分配模式](load-balancer-distribution-mode.md)類型。</span><span class="sxs-lookup"><span data-stu-id="e14c4-139">You can also [get started creating an Internet facing load balancer](load-balancer-get-started-internet-arm-ps.md) and configure what type of [distribution mode](load-balancer-distribution-mode.md) for a specific load balancer network traffic behavior.</span></span>

<span data-ttu-id="e14c4-140">了解如何管理 [負載平衡器的閒置 TCP 逾時設定](load-balancer-tcp-idle-timeout.md)。</span><span class="sxs-lookup"><span data-stu-id="e14c4-140">Learn how to manage [idle TCP timeout settings for a load balancer](load-balancer-tcp-idle-timeout.md).</span></span> <span data-ttu-id="e14c4-141">當您的應用程式需要讓負載平衡器後方的伺服器保持連線時，這很重要。</span><span class="sxs-lookup"><span data-stu-id="e14c4-141">This is important when your application needs to keep connections alive for servers behind a load balancer.</span></span>
