---
title: "在 Azure 網路監看員 aaaIntroduction toonext 躍點 |Microsoft 文件"
description: "此頁面提供概觀 hello 網路監看員的下一個躍點的功能"
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
ms.openlocfilehash: 916af736d0d52abadeafed746f0f8a0173b11033
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toonext-hop-in-azure-network-watcher"></a><span data-ttu-id="6ea45-103">在 Azure 網路監看員簡介 toonext 躍點</span><span class="sxs-lookup"><span data-stu-id="6ea45-103">Introduction toonext hop in Azure Network Watcher</span></span>

<span data-ttu-id="6ea45-104">從 VM 的流量會傳送 tooa 根據 hello 與 NIC 相關聯的有效路由的目的地</span><span class="sxs-lookup"><span data-stu-id="6ea45-104">Traffic from a VM is sent tooa destination based on hello effective routes associated with a NIC.</span></span> <span data-ttu-id="6ea45-105">下一個躍點取得下一個躍點類型 hello 和封包的 IP 位址從特定虛擬機器與 nic。</span><span class="sxs-lookup"><span data-stu-id="6ea45-105">Next hop gets hello next hop type and IP address of a packet from a specific virtual machine and NIC.</span></span> <span data-ttu-id="6ea45-106">這可協助 toodetermine 如果 hello 封包會被導向的 toohello 目的地，或為正在黑色 hello 流量書背。</span><span class="sxs-lookup"><span data-stu-id="6ea45-106">This helps toodetermine if hello packet is being directed toohello destination or is hello traffic being black holed.</span></span> <span data-ttu-id="6ea45-107">不適當的路由 hello 使用者流量導向的 tooan 在內部部署位置或所在虛擬應用裝置，設定可能會導致 tooconnectivity 問題。</span><span class="sxs-lookup"><span data-stu-id="6ea45-107">An improper configuration of routes by hello user, where a traffic is directed tooan on-premises location or a virtual appliance, can lead tooconnectivity issues.</span></span> <span data-ttu-id="6ea45-108">下一個躍點也會傳回 hello 與 hello 下一個躍點相關聯的路由表。</span><span class="sxs-lookup"><span data-stu-id="6ea45-108">Next hop also returns hello route table associated with hello next hop.</span></span> <span data-ttu-id="6ea45-109">如果 hello 路由定義為使用者定義的路由，請查詢下一個躍點，將會傳回該路由。</span><span class="sxs-lookup"><span data-stu-id="6ea45-109">When querying a next hop if hello route is defined as a user-defined route, that route will be returned.</span></span> <span data-ttu-id="6ea45-110">否則，下一個躍點會傳回「系統路由」。</span><span class="sxs-lookup"><span data-stu-id="6ea45-110">Otherwise Next hop returns "System Route".</span></span>

![下一個躍點概觀][1]

<span data-ttu-id="6ea45-112">hello 以下是 hello 下一個躍點類型可以在下一個躍點的查詢時傳回的清單。</span><span class="sxs-lookup"><span data-stu-id="6ea45-112">hello following is a list of hello next hop types that can be returned when querying Next hop.</span></span>

* <span data-ttu-id="6ea45-113">Internet</span><span class="sxs-lookup"><span data-stu-id="6ea45-113">Internet</span></span>
* <span data-ttu-id="6ea45-114">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="6ea45-114">VirtualAppliance</span></span>
* <span data-ttu-id="6ea45-115">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="6ea45-115">VirtualNetworkGateway</span></span>
* <span data-ttu-id="6ea45-116">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="6ea45-116">VnetLocal</span></span>
* <span data-ttu-id="6ea45-117">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="6ea45-117">HyperNetGateway</span></span>
* <span data-ttu-id="6ea45-118">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="6ea45-118">VnetPeering</span></span>
* <span data-ttu-id="6ea45-119">None</span><span class="sxs-lookup"><span data-stu-id="6ea45-119">None</span></span>

### <a name="next-steps"></a><span data-ttu-id="6ea45-120">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6ea45-120">Next steps</span></span>

<span data-ttu-id="6ea45-121">了解網路連線與下一個躍點 toofind toouse 問題造訪如何[核取 hello 下一個躍點 VM 上](network-watcher-check-next-hop-portal.md)</span><span class="sxs-lookup"><span data-stu-id="6ea45-121">Learn how toouse next hop toofind issues with network connectivity by visiting [Check hello next hop on a VM](network-watcher-check-next-hop-portal.md)</span></span>

<!--Image references-->
[1]: ./media/network-watcher-next-hop-overview/figure1.png













