---
title: "Azure 網路監看員中的拓撲簡介 | Microsoft Docs"
description: "本頁提供網路監看員拓撲功能的概觀"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e753a435-38e0-482b-846b-121cb547555c
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 42443f614b76b8180ac163b9889163021adbf048
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-topology-in-azure-network-watcher"></a><span data-ttu-id="44e31-103">Azure 網路監看員中的拓撲簡介</span><span class="sxs-lookup"><span data-stu-id="44e31-103">Introduction to topology in Azure Network Watcher</span></span>

<span data-ttu-id="44e31-104">拓撲會傳回虛擬網路中的網路資源之圖形。</span><span class="sxs-lookup"><span data-stu-id="44e31-104">Topology returns a graph of network resources in a virtual network.</span></span> <span data-ttu-id="44e31-105">此圖描述了資源之間的互相連線來代表端對端網路連線。</span><span class="sxs-lookup"><span data-stu-id="44e31-105">The graph depicts the interconnection between the resources to represent the end to end network connectivity.</span></span>

![拓撲概觀][1]

<span data-ttu-id="44e31-107">在入口網站中，拓撲會依每個虛擬網路為基礎傳回資源物件。</span><span class="sxs-lookup"><span data-stu-id="44e31-107">In the portal, Topology returns the resource objects on a per virtual network basis.</span></span> <span data-ttu-id="44e31-108">即使在不會顯示的資源群組中，關聯性會依網路監看員區域外部的資源之間的線條描述。</span><span class="sxs-lookup"><span data-stu-id="44e31-108">The relationships are depicted by lines between the resources Resources outside of the Network Watcher region, even if in the resource group will not be displayed.</span></span> <span data-ttu-id="44e31-109">在入口網站檢視傳回的資源會以圖表方式顯示的網路元件子集。</span><span class="sxs-lookup"><span data-stu-id="44e31-109">The resources returned in the portal view are a subset of the networking components that are graphed.</span></span> <span data-ttu-id="44e31-110">若要查看網路資源完整清單，您可以使用 [PowerShell](network-watcher-topology-powershell.md) 或 [REST](network-watcher-topology-rest.md)</span><span class="sxs-lookup"><span data-stu-id="44e31-110">To see the full list of networking resources you can use [PowerShell](network-watcher-topology-powershell.md) or [REST](network-watcher-topology-rest.md)</span></span>

> [!NOTE]
> <span data-ttu-id="44e31-111">在您想要執行拓撲的每個區域中，需要網路監看員執行個體。</span><span class="sxs-lookup"><span data-stu-id="44e31-111">An instance of Network Watcher is required in each region that you want to run Topology on.</span></span>

<span data-ttu-id="44e31-112">隨著資源傳回，它們之間的連線會在兩個關聯性之間模型化。</span><span class="sxs-lookup"><span data-stu-id="44e31-112">As resources are returned the connection between them are modeled under two relationships.</span></span>

- <span data-ttu-id="44e31-113">**內含項目** - 範例︰虛擬網路包含其中含有 NIC 的子網路</span><span class="sxs-lookup"><span data-stu-id="44e31-113">**Containment** - Example: Virtual Network contains a Subnet which contains a NIC</span></span>
- <span data-ttu-id="44e31-114">**相關聯** - 範例︰NIC 與 VM 相關聯</span><span class="sxs-lookup"><span data-stu-id="44e31-114">**Associated** - Example: A NIC is associated with a VM</span></span>

### <a name="next-steps"></a><span data-ttu-id="44e31-115">後續步驟</span><span class="sxs-lookup"><span data-stu-id="44e31-115">Next steps</span></span>

<span data-ttu-id="44e31-116">了解如何使用 PowerShell 來擷取拓撲檢視，請造訪[使用 PowerShell 的網路監看員拓撲](network-watcher-topology-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="44e31-116">Learn how to use PowerShell to retrieve the Topology view by visiting [Network Watcher topology with PowerShell](network-watcher-topology-powershell.md)</span></span>

<!--Image references-->

[1]: ./media/network-watcher-topology-overview/topology.png
