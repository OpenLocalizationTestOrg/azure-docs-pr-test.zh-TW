---
title: "Azure 網路監看員中的下一個躍點簡介 | Microsoft Docs"
description: "本頁提供網路監看員下一個躍點功能的概觀"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: febf7bca-e0b7-41d5-838f-a5a40ebc5aac
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 5dd65d2418cae206965a13013dd990b916ad0733
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-next-hop-in-azure-network-watcher"></a><span data-ttu-id="90e89-103">Azure 網路監看員中的下一個躍點簡介</span><span class="sxs-lookup"><span data-stu-id="90e89-103">Introduction to next hop in Azure Network Watcher</span></span>

<span data-ttu-id="90e89-104">來自 VM 的流量會根據與 NIC 相關聯的有效路由來傳送到目的地。</span><span class="sxs-lookup"><span data-stu-id="90e89-104">Traffic from a VM is sent to a destination based on the effective routes associated with a NIC.</span></span> <span data-ttu-id="90e89-105">下一個躍點會從特定虛擬機器和 NIC 取得封包的下一個躍點類型和 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="90e89-105">Next hop gets the next hop type and IP address of a packet from a specific virtual machine and NIC.</span></span> <span data-ttu-id="90e89-106">這有助於判斷封包會被導向到目的地，還是流量會被吸收掉。</span><span class="sxs-lookup"><span data-stu-id="90e89-106">This helps to determine if the packet is being directed to the destination or is the traffic being black holed.</span></span> <span data-ttu-id="90e89-107">使用者若未正確設定路由，而讓流量導向內部部署位置或虛擬應用裝置，就可能會導致連線問題。</span><span class="sxs-lookup"><span data-stu-id="90e89-107">An improper configuration of routes by the user, where a traffic is directed to an on-premises location or a virtual appliance, can lead to connectivity issues.</span></span> <span data-ttu-id="90e89-108">下一個躍點也會傳回與下一個躍點相關聯的路由表。</span><span class="sxs-lookup"><span data-stu-id="90e89-108">Next hop also returns the route table associated with the next hop.</span></span> <span data-ttu-id="90e89-109">向下一個躍點查詢路由是否定義為使用者定義的路由時，便會傳回該路由。</span><span class="sxs-lookup"><span data-stu-id="90e89-109">When querying a next hop if the route is defined as a user-defined route, that route will be returned.</span></span> <span data-ttu-id="90e89-110">否則，下一個躍點會傳回「系統路由」。</span><span class="sxs-lookup"><span data-stu-id="90e89-110">Otherwise Next hop returns "System Route".</span></span>

![下一個躍點概觀][1]

<span data-ttu-id="90e89-112">以下是查詢下一個躍點時可傳回之下一個躍點類型的清單。</span><span class="sxs-lookup"><span data-stu-id="90e89-112">The following is a list of the next hop types that can be returned when querying Next hop.</span></span>

* <span data-ttu-id="90e89-113">Internet</span><span class="sxs-lookup"><span data-stu-id="90e89-113">Internet</span></span>
* <span data-ttu-id="90e89-114">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="90e89-114">VirtualAppliance</span></span>
* <span data-ttu-id="90e89-115">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="90e89-115">VirtualNetworkGateway</span></span>
* <span data-ttu-id="90e89-116">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="90e89-116">VnetLocal</span></span>
* <span data-ttu-id="90e89-117">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="90e89-117">HyperNetGateway</span></span>
* <span data-ttu-id="90e89-118">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="90e89-118">VnetPeering</span></span>
* <span data-ttu-id="90e89-119">None</span><span class="sxs-lookup"><span data-stu-id="90e89-119">None</span></span>

### <a name="next-steps"></a><span data-ttu-id="90e89-120">後續步驟</span><span class="sxs-lookup"><span data-stu-id="90e89-120">Next steps</span></span>

<span data-ttu-id="90e89-121">瀏覽[檢查 VM 上的下一個躍點](network-watcher-check-next-hop-portal.md)，以了解如何使用下一個躍點來尋找網路連線問題</span><span class="sxs-lookup"><span data-stu-id="90e89-121">Learn how to use next hop to find issues with network connectivity by visiting [Check the next hop on a VM](network-watcher-check-next-hop-portal.md)</span></span>

<!--Image references-->
[1]: ./media/network-watcher-next-hop-overview/figure1.png













