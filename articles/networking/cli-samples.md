---
title: "aaaAzure CLI 範例 |Microsoft 文件"
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
ms.openlocfilehash: 8001b7e72480cfd0122325f7fb81c32aaad072d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cli-samples-for-networking"></a><span data-ttu-id="42b1c-103">網路功能的 Azure CLI 範例</span><span class="sxs-lookup"><span data-stu-id="42b1c-103">Azure CLI Samples for networking</span></span>

<span data-ttu-id="42b1c-104">hello 下表包含使用 Azure CLI hello 建置連結 toobash 指令碼。</span><span class="sxs-lookup"><span data-stu-id="42b1c-104">hello following table includes links toobash scripts built using hello Azure CLI.</span></span>

| | |
|-|-|
|<span data-ttu-id="42b1c-105">**Azure 資源之間的連線**</span><span class="sxs-lookup"><span data-stu-id="42b1c-105">**Connectivity between Azure resources**</span></span>||
| [<span data-ttu-id="42b1c-106">建立多層式應用程式的虛擬網路</span><span class="sxs-lookup"><span data-stu-id="42b1c-106">Create a virtual network for multi-tier applications</span></span>](./scripts/virtual-network-cli-sample-multi-tier-application.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="42b1c-107">建立具有前端和後端子網路的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="42b1c-107">Creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="42b1c-108">流量 toohello 前端子網路是有限的 tooHTTP 和 SSH，流量 toohello 時後端子是有限的 tooMySQL，3306 的連接埠。</span><span class="sxs-lookup"><span data-stu-id="42b1c-108">Traffic toohello front-end subnet is limited tooHTTP and SSH, while traffic toohello back-end subnet is limited tooMySQL, port 3306.</span></span> |
| [<span data-ttu-id="42b1c-109">對等互連兩個虛擬網路</span><span class="sxs-lookup"><span data-stu-id="42b1c-109">Peer two virtual networks</span></span>](./scripts/virtual-network-cli-sample-peer-two-virtual-networks.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="42b1c-110">建立並連接 hello 中的兩個虛擬網路相同的區域。</span><span class="sxs-lookup"><span data-stu-id="42b1c-110">Creates and connects two virtual networks in hello same region.</span></span> |
| [<span data-ttu-id="42b1c-111">透過網路虛擬設備路由傳送流量</span><span class="sxs-lookup"><span data-stu-id="42b1c-111">Route traffic through a network virtual appliance</span></span>](./scripts/virtual-network-cli-sample-route-traffic-through-nva.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="42b1c-112">建立虛擬網路與前端和後端的子網路和 VM 並無法 tooroute hello 兩個子網路之間的流量。</span><span class="sxs-lookup"><span data-stu-id="42b1c-112">Creates a virtual network with front-end and back-end subnets and a VM that is able tooroute traffic between hello two subnets.</span></span> |
| [<span data-ttu-id="42b1c-113">篩選輸入和輸出 VM 網路流量</span><span class="sxs-lookup"><span data-stu-id="42b1c-113">Filter inbound and outbound VM network traffic</span></span>](./scripts/virtual-network-filter-network-traffic.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="42b1c-114">建立具有前端和後端子網路的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="42b1c-114">Creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="42b1c-115">輸入網路流量 toohello 前端子網路是有限的 tooHTTP HTTPS 和 SSH。</span><span class="sxs-lookup"><span data-stu-id="42b1c-115">Inbound network traffic toohello front-end subnet is limited tooHTTP, HTTPS and SSH.</span></span> <span data-ttu-id="42b1c-116">不允許輸出流量 toohello 網際網路從 hello 後端子。</span><span class="sxs-lookup"><span data-stu-id="42b1c-116">Outbound traffic toohello Internet from hello back-end subnet is not permitted.</span></span> |
|<span data-ttu-id="42b1c-117">**負載平衡和流量方向**</span><span class="sxs-lookup"><span data-stu-id="42b1c-117">**Load balancing and traffic direction**</span></span>||
| [<span data-ttu-id="42b1c-118">負載平衡流量 tooVMs 高可用性</span><span class="sxs-lookup"><span data-stu-id="42b1c-118">Load balance traffic tooVMs for high availability</span></span>](./scripts/load-balancer-linux-cli-sample-nlb.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="42b1c-119">依據高可用性和負載平衡組態建立數個虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="42b1c-119">Creates several virtual machines in a highly available and load balanced configuration.</span></span> |
| [<span data-ttu-id="42b1c-120">在 VM 上平衡多個網站的負載</span><span class="sxs-lookup"><span data-stu-id="42b1c-120">Load balance multiple websites on VMs</span></span>](./scripts/load-balancer-linux-cli-load-balance-multiple-websites-vm.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="42b1c-121">使用多個 IP 組態，Azure 可用性設定組，可透過 Azure 負載平衡器存取的 tooan 聯結建立兩個 Vm。</span><span class="sxs-lookup"><span data-stu-id="42b1c-121">Creates two VMs with multiple IP configurations, joined tooan Azure Availability Set, accessible through an Azure Load Balancer.</span></span> |
| [<span data-ttu-id="42b1c-122">跨多個區域導向流量以達到高應用程式可用性</span><span class="sxs-lookup"><span data-stu-id="42b1c-122">Direct traffic across multiple regions for high application availability</span></span>](./scripts/traffic-manager-cli-websites-high-availability.md?toc=%2fazure%2fnetworking%2ftoc.json) |  <span data-ttu-id="42b1c-123">建立兩個 App Service 方案、兩個 Web 應用程式、一個流量管理員設定檔和兩個流量管理員端點。</span><span class="sxs-lookup"><span data-stu-id="42b1c-123">Creates two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> |
| | |
