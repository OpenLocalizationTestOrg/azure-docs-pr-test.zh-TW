---
title: "Azure PowerShell 範例 | Microsoft Docs"
description: "Azure PowerShell 範例"
services: virtual-network
documentationcenter: virtual-network
author: georgewallace
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 05/24/2017
ms.author: georgewallace
ms.openlocfilehash: 0bca4fb6874bd265f0ae9faeb4219abeb4ffb6d4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-powershell-samples-for-networking"></a><span data-ttu-id="57813-103">Azure PowerShell 網路範例</span><span class="sxs-lookup"><span data-stu-id="57813-103">Azure PowerShell Samples for networking</span></span>

<span data-ttu-id="57813-104">下表包含使用 Azure PowerShell 所建置指令碼的連結。</span><span class="sxs-lookup"><span data-stu-id="57813-104">The following table includes links to scripts built using Azure PowerShell.</span></span>

| | |
|-|-|
|<span data-ttu-id="57813-105">**Azure 資源之間的連線**</span><span class="sxs-lookup"><span data-stu-id="57813-105">**Connectivity between Azure resources**</span></span>||
| [<span data-ttu-id="57813-106">建立多層式應用程式的虛擬網路</span><span class="sxs-lookup"><span data-stu-id="57813-106">Create a virtual network for multi-tier applications</span></span>](./scripts/virtual-network-powershell-sample-multi-tier-application.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="57813-107">建立具有前端和後端子網路的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="57813-107">Creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="57813-108">傳送到前端子網路的流量會限制為 HTTP，而傳送到後端子網路的流量則限制為 SQL 且連接埠為 1433。</span><span class="sxs-lookup"><span data-stu-id="57813-108">Traffic to the front-end subnet is limited to HTTP, while traffic to the back-end subnet is limited to SQL, port 1433.</span></span> |
| [<span data-ttu-id="57813-109">對等互連兩個虛擬網路</span><span class="sxs-lookup"><span data-stu-id="57813-109">Peer two virtual networks</span></span>](./scripts/virtual-network-powershell-sample-peer-two-virtual-networks.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="57813-110">在相同區域中建立和連線兩個虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="57813-110">Creates and connects two virtual networks in the same region.</span></span> |
| [<span data-ttu-id="57813-111">透過網路虛擬設備路由傳送流量</span><span class="sxs-lookup"><span data-stu-id="57813-111">Route traffic through a network virtual appliance</span></span>](./scripts/virtual-network-powershell-sample-route-traffic-through-nva.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="57813-112">建立具有前端和後端子網路的虛擬網路，以及可在兩個子網路間路由傳送流量的 VM。</span><span class="sxs-lookup"><span data-stu-id="57813-112">Creates a virtual network with front-end and back-end subnets and a VM that is able to route traffic between the two subnets.</span></span> |
| [<span data-ttu-id="57813-113">篩選輸入和輸出 VM 網路流量</span><span class="sxs-lookup"><span data-stu-id="57813-113">Filter inbound and outbound VM network traffic</span></span>](./scripts/virtual-network-powershell-filter-network-traffic.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="57813-114">建立具有前端和後端子網路的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="57813-114">Creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="57813-115">傳送到前端子網路的輸入網路流量限制為 HTTP 和 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="57813-115">Inbound network traffic to the front-end subnet is limited to HTTP and HTTPS..</span></span> <span data-ttu-id="57813-116">不允許從後端子網路傳輸至網際網路的輸出流量。</span><span class="sxs-lookup"><span data-stu-id="57813-116">Outbound traffic to the Internet from the back-end subnet is not permitted.</span></span> |
|<span data-ttu-id="57813-117">**負載平衡和流量方向**</span><span class="sxs-lookup"><span data-stu-id="57813-117">**Load balancing and traffic direction**</span></span>||
| [<span data-ttu-id="57813-118">使用 VM 平衡流量負載以達到高可用性</span><span class="sxs-lookup"><span data-stu-id="57813-118">Load balance traffic to VMs for high availability</span></span>](./scripts/load-balancer-windows-powershell-sample-nlb.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="57813-119">依據高可用性和負載平衡組態建立數個虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="57813-119">Creates several virtual machines in a highly available and load balanced configuration.</span></span> |
| [<span data-ttu-id="57813-120">在 VM 上平衡多個網站的負載</span><span class="sxs-lookup"><span data-stu-id="57813-120">Load balance multiple websites on VMs</span></span>](./scripts/load-balancer-windows-powershell-load-balance-multiple-websites-vm.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="57813-121">建立具有多個 IP 設定的兩個 VM。這兩個 VM 會加入 Azure 可用性設定組，並可透過 Azure Load Balancer 來存取。</span><span class="sxs-lookup"><span data-stu-id="57813-121">Creates two VMs with multiple IP configurations, joined to an Azure Availability Set, accessible through an Azure Load Balancer.</span></span> |
| [<span data-ttu-id="57813-122">跨多個區域導向流量以達到高應用程式可用性</span><span class="sxs-lookup"><span data-stu-id="57813-122">Direct traffic across multiple regions for high application availability</span></span>](./scripts/traffic-manager-powershell-websites-high-availability.md?toc=%2fazure%2fnetworking%2ftoc.json) |  <span data-ttu-id="57813-123">建立兩個 App Service 方案、兩個 Web 應用程式、一個流量管理員設定檔和兩個流量管理員端點。</span><span class="sxs-lookup"><span data-stu-id="57813-123">Creates two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> |
| | |
