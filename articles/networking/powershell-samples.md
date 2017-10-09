---
title: "PowerShell 範例 aaaAzure |Microsoft 文件"
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
ms.openlocfilehash: 130a6e755691b46a9549cad5acaa5bde4fe38e95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-powershell-samples-for-networking"></a><span data-ttu-id="33c64-103">Azure PowerShell 網路範例</span><span class="sxs-lookup"><span data-stu-id="33c64-103">Azure PowerShell Samples for networking</span></span>

<span data-ttu-id="33c64-104">hello 表包含連結 tooscripts 建置使用 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="33c64-104">hello following table includes links tooscripts built using Azure PowerShell.</span></span>

| | |
|-|-|
|<span data-ttu-id="33c64-105">**Azure 資源之間的連線**</span><span class="sxs-lookup"><span data-stu-id="33c64-105">**Connectivity between Azure resources**</span></span>||
| [<span data-ttu-id="33c64-106">建立多層式應用程式的虛擬網路</span><span class="sxs-lookup"><span data-stu-id="33c64-106">Create a virtual network for multi-tier applications</span></span>](./scripts/virtual-network-powershell-sample-multi-tier-application.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="33c64-107">建立具有前端和後端子網路的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="33c64-107">Creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="33c64-108">流量 toohello 前端子網路是有限的 tooHTTP，流量 toohello 時後端子有限的 tooSQL，通訊埠 1433年。</span><span class="sxs-lookup"><span data-stu-id="33c64-108">Traffic toohello front-end subnet is limited tooHTTP, while traffic toohello back-end subnet is limited tooSQL, port 1433.</span></span> |
| [<span data-ttu-id="33c64-109">對等互連兩個虛擬網路</span><span class="sxs-lookup"><span data-stu-id="33c64-109">Peer two virtual networks</span></span>](./scripts/virtual-network-powershell-sample-peer-two-virtual-networks.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="33c64-110">建立並連接 hello 中的兩個虛擬網路相同的區域。</span><span class="sxs-lookup"><span data-stu-id="33c64-110">Creates and connects two virtual networks in hello same region.</span></span> |
| [<span data-ttu-id="33c64-111">透過網路虛擬設備路由傳送流量</span><span class="sxs-lookup"><span data-stu-id="33c64-111">Route traffic through a network virtual appliance</span></span>](./scripts/virtual-network-powershell-sample-route-traffic-through-nva.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="33c64-112">建立虛擬網路與前端和後端的子網路和 VM 並無法 tooroute hello 兩個子網路之間的流量。</span><span class="sxs-lookup"><span data-stu-id="33c64-112">Creates a virtual network with front-end and back-end subnets and a VM that is able tooroute traffic between hello two subnets.</span></span> |
| [<span data-ttu-id="33c64-113">篩選輸入和輸出 VM 網路流量</span><span class="sxs-lookup"><span data-stu-id="33c64-113">Filter inbound and outbound VM network traffic</span></span>](./scripts/virtual-network-powershell-filter-network-traffic.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="33c64-114">建立具有前端和後端子網路的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="33c64-114">Creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="33c64-115">輸入網路流量 toohello 前端子網路是有限的 tooHTTP 和 HTTPS...</span><span class="sxs-lookup"><span data-stu-id="33c64-115">Inbound network traffic toohello front-end subnet is limited tooHTTP and HTTPS..</span></span> <span data-ttu-id="33c64-116">不允許輸出流量 toohello 網際網路從 hello 後端子。</span><span class="sxs-lookup"><span data-stu-id="33c64-116">Outbound traffic toohello Internet from hello back-end subnet is not permitted.</span></span> |
|<span data-ttu-id="33c64-117">**負載平衡和流量方向**</span><span class="sxs-lookup"><span data-stu-id="33c64-117">**Load balancing and traffic direction**</span></span>||
| [<span data-ttu-id="33c64-118">負載平衡流量 tooVMs 高可用性</span><span class="sxs-lookup"><span data-stu-id="33c64-118">Load balance traffic tooVMs for high availability</span></span>](./scripts/load-balancer-windows-powershell-sample-nlb.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="33c64-119">依據高可用性和負載平衡組態建立數個虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="33c64-119">Creates several virtual machines in a highly available and load balanced configuration.</span></span> |
| [<span data-ttu-id="33c64-120">在 VM 上平衡多個網站的負載</span><span class="sxs-lookup"><span data-stu-id="33c64-120">Load balance multiple websites on VMs</span></span>](./scripts/load-balancer-windows-powershell-load-balance-multiple-websites-vm.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="33c64-121">使用多個 IP 組態，Azure 可用性設定組，可透過 Azure 負載平衡器存取的 tooan 聯結建立兩個 Vm。</span><span class="sxs-lookup"><span data-stu-id="33c64-121">Creates two VMs with multiple IP configurations, joined tooan Azure Availability Set, accessible through an Azure Load Balancer.</span></span> |
| [<span data-ttu-id="33c64-122">跨多個區域導向流量以達到高應用程式可用性</span><span class="sxs-lookup"><span data-stu-id="33c64-122">Direct traffic across multiple regions for high application availability</span></span>](./scripts/traffic-manager-powershell-websites-high-availability.md?toc=%2fazure%2fnetworking%2ftoc.json) |  <span data-ttu-id="33c64-123">建立兩個 App Service 方案、兩個 Web 應用程式、一個流量管理員設定檔和兩個流量管理員端點。</span><span class="sxs-lookup"><span data-stu-id="33c64-123">Creates two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> |
| | |
