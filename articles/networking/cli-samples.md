---
title: "Azure CLI 範例 | Microsoft Docs"
description: "Azure CLI 範例"
services: virtual-network
documentationcenter: virtual-network
author: KumudD
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 04/25/2017
ms.author: kumud
ms.openlocfilehash: 7977460f61bfdabd399e45e86d9bbf2e5083992b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cli-samples-for-networking"></a><span data-ttu-id="5f185-103">網路功能的 Azure CLI 範例</span><span class="sxs-lookup"><span data-stu-id="5f185-103">Azure CLI Samples for networking</span></span>

<span data-ttu-id="5f185-104">下表包含使用 Azure CLI 所建置之 Bash 指令碼的連結。</span><span class="sxs-lookup"><span data-stu-id="5f185-104">The following table includes links to bash scripts built using the Azure CLI.</span></span>

| | |
|-|-|
|<span data-ttu-id="5f185-105">**Azure 資源之間的連線**</span><span class="sxs-lookup"><span data-stu-id="5f185-105">**Connectivity between Azure resources**</span></span>||
| [<span data-ttu-id="5f185-106">建立多層式應用程式的虛擬網路</span><span class="sxs-lookup"><span data-stu-id="5f185-106">Create a virtual network for multi-tier applications</span></span>](./scripts/virtual-network-cli-sample-multi-tier-application.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="5f185-107">建立具有前端和後端子網路的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="5f185-107">Creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="5f185-108">傳送到前端子網路的流量會限制為 HTTP 和 SSH，而傳送到後端子網路的流量則限制為 MySQL 且連接埠為 3306。</span><span class="sxs-lookup"><span data-stu-id="5f185-108">Traffic to the front-end subnet is limited to HTTP and SSH, while traffic to the back-end subnet is limited to MySQL, port 3306.</span></span> |
| [<span data-ttu-id="5f185-109">對等互連兩個虛擬網路</span><span class="sxs-lookup"><span data-stu-id="5f185-109">Peer two virtual networks</span></span>](./scripts/virtual-network-cli-sample-peer-two-virtual-networks.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="5f185-110">在相同區域中建立和連線兩個虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="5f185-110">Creates and connects two virtual networks in the same region.</span></span> |
| [<span data-ttu-id="5f185-111">透過網路虛擬設備路由傳送流量</span><span class="sxs-lookup"><span data-stu-id="5f185-111">Route traffic through a network virtual appliance</span></span>](./scripts/virtual-network-cli-sample-route-traffic-through-nva.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="5f185-112">建立具有前端和後端子網路的虛擬網路，以及可在兩個子網路間路由傳送流量的 VM。</span><span class="sxs-lookup"><span data-stu-id="5f185-112">Creates a virtual network with front-end and back-end subnets and a VM that is able to route traffic between the two subnets.</span></span> |
| [<span data-ttu-id="5f185-113">篩選輸入和輸出 VM 網路流量</span><span class="sxs-lookup"><span data-stu-id="5f185-113">Filter inbound and outbound VM network traffic</span></span>](./scripts/virtual-network-filter-network-traffic.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="5f185-114">建立具有前端和後端子網路的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="5f185-114">Creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="5f185-115">傳輸至前端子網路的輸入網路流量限制為 HTTP、HTTPS 和 SSH。</span><span class="sxs-lookup"><span data-stu-id="5f185-115">Inbound network traffic to the front-end subnet is limited to HTTP, HTTPS and SSH.</span></span> <span data-ttu-id="5f185-116">不允許從後端子網路傳輸至網際網路的輸出流量。</span><span class="sxs-lookup"><span data-stu-id="5f185-116">Outbound traffic to the Internet from the back-end subnet is not permitted.</span></span> |
|<span data-ttu-id="5f185-117">**負載平衡和流量方向**</span><span class="sxs-lookup"><span data-stu-id="5f185-117">**Load balancing and traffic direction**</span></span>||
| [<span data-ttu-id="5f185-118">使用 VM 平衡流量負載以達到高可用性</span><span class="sxs-lookup"><span data-stu-id="5f185-118">Load balance traffic to VMs for high availability</span></span>](./scripts/load-balancer-linux-cli-sample-nlb.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="5f185-119">依據高可用性和負載平衡組態建立數個虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="5f185-119">Creates several virtual machines in a highly available and load balanced configuration.</span></span> |
| [<span data-ttu-id="5f185-120">在 VM 上平衡多個網站的負載</span><span class="sxs-lookup"><span data-stu-id="5f185-120">Load balance multiple websites on VMs</span></span>](./scripts/load-balancer-linux-cli-load-balance-multiple-websites-vm.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="5f185-121">建立具有多個 IP 設定的兩個 VM。這兩個 VM 會加入 Azure 可用性設定組，並可透過 Azure Load Balancer 來存取。</span><span class="sxs-lookup"><span data-stu-id="5f185-121">Creates two VMs with multiple IP configurations, joined to an Azure Availability Set, accessible through an Azure Load Balancer.</span></span> |
| [<span data-ttu-id="5f185-122">跨多個區域導向流量以達到高應用程式可用性</span><span class="sxs-lookup"><span data-stu-id="5f185-122">Direct traffic across multiple regions for high application availability</span></span>](./scripts/traffic-manager-cli-websites-high-availability.md?toc=%2fazure%2fnetworking%2ftoc.json) |  <span data-ttu-id="5f185-123">建立兩個 App Service 方案、兩個 Web 應用程式、一個流量管理員設定檔和兩個流量管理員端點。</span><span class="sxs-lookup"><span data-stu-id="5f185-123">Creates two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> |
| | |
