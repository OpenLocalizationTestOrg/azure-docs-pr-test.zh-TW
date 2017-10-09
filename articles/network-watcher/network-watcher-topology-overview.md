---
title: "在 Azure 網路監看員 aaaIntroduction tootopology |Microsoft 文件"
description: "此頁面提供 hello 網路監看員拓撲的功能的概觀"
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
ms.openlocfilehash: 7fa1c5518e4a25a5db999d898a9ee19fd0121db7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tootopology-in-azure-network-watcher"></a><span data-ttu-id="54acc-103">在 Azure 網路監看員的簡介 tootopology</span><span class="sxs-lookup"><span data-stu-id="54acc-103">Introduction tootopology in Azure Network Watcher</span></span>

<span data-ttu-id="54acc-104">拓撲會傳回虛擬網路中的網路資源之圖形。</span><span class="sxs-lookup"><span data-stu-id="54acc-104">Topology returns a graph of network resources in a virtual network.</span></span> <span data-ttu-id="54acc-105">hello 圖描繪 hello 資源 toorepresent hello 結束 tooend 網路連線之間的 hello 互連。</span><span class="sxs-lookup"><span data-stu-id="54acc-105">hello graph depicts hello interconnection between hello resources toorepresent hello end tooend network connectivity.</span></span>

![拓撲概觀][1]

<span data-ttu-id="54acc-107">Hello 入口網站中，在拓撲會傳回 hello 資源物件上每個虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="54acc-107">In hello portal, Topology returns hello resource objects on a per virtual network basis.</span></span> <span data-ttu-id="54acc-108">即使在 hello 資源群組將不會顯示，但會由 hello 網路監看員區域以外的 hello 資源的資源間的線條顯示 hello 關聯性。</span><span class="sxs-lookup"><span data-stu-id="54acc-108">hello relationships are depicted by lines between hello resources Resources outside of hello Network Watcher region, even if in hello resource group will not be displayed.</span></span> <span data-ttu-id="54acc-109">傳回在 hello 入口網站檢視中的 hello 資源是 hello 網路元件是圖形化的子集。</span><span class="sxs-lookup"><span data-stu-id="54acc-109">hello resources returned in hello portal view are a subset of hello networking components that are graphed.</span></span> <span data-ttu-id="54acc-110">您可以使用網路資源的 toosee hello 完整清單[PowerShell](network-watcher-topology-powershell.md)或[REST](network-watcher-topology-rest.md)</span><span class="sxs-lookup"><span data-stu-id="54acc-110">toosee hello full list of networking resources you can use [PowerShell](network-watcher-topology-powershell.md) or [REST](network-watcher-topology-rest.md)</span></span>

> [!NOTE]
> <span data-ttu-id="54acc-111">您想 toorun 拓撲每個區域中需要的網路監看員執行個體。</span><span class="sxs-lookup"><span data-stu-id="54acc-111">An instance of Network Watcher is required in each region that you want toorun Topology on.</span></span>

<span data-ttu-id="54acc-112">資源會傳回它們之間的 hello 連接是在兩個關聯性建立模型。</span><span class="sxs-lookup"><span data-stu-id="54acc-112">As resources are returned hello connection between them are modeled under two relationships.</span></span>

- <span data-ttu-id="54acc-113">**內含項目** - 範例︰虛擬網路包含其中含有 NIC 的子網路</span><span class="sxs-lookup"><span data-stu-id="54acc-113">**Containment** - Example: Virtual Network contains a Subnet which contains a NIC</span></span>
- <span data-ttu-id="54acc-114">**相關聯** - 範例︰NIC 與 VM 相關聯</span><span class="sxs-lookup"><span data-stu-id="54acc-114">**Associated** - Example: A NIC is associated with a VM</span></span>

### <a name="next-steps"></a><span data-ttu-id="54acc-115">後續步驟</span><span class="sxs-lookup"><span data-stu-id="54acc-115">Next steps</span></span>

<span data-ttu-id="54acc-116">了解如何 toouse PowerShell tooretrieve hello 拓撲檢視造訪[網路監看員拓撲使用 PowerShell](network-watcher-topology-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="54acc-116">Learn how toouse PowerShell tooretrieve hello Topology view by visiting [Network Watcher topology with PowerShell](network-watcher-topology-powershell.md)</span></span>

<!--Image references-->

[1]: ./media/network-watcher-topology-overview/topology.png
