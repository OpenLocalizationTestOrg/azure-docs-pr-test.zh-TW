---
title: "Azure 網路監看員中的 IP 流量驗證簡介 | Microsoft Docs"
description: "本頁提供網路監看員 IP 流量驗證功能的概觀"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: d352fb2d-4b4f-4ac4-9c2e-1cfccf0e7e03
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 9c0dfc449b3d93d8aa4551ce16476c8313d731fc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-ip-flow-verify-in-azure-network-watcher"></a><span data-ttu-id="74c2d-103">Azure 網路監看員中的 IP 流量驗證簡介</span><span class="sxs-lookup"><span data-stu-id="74c2d-103">Introduction to IP flow verify in Azure Network Watcher</span></span>

<span data-ttu-id="74c2d-104">IP 流量驗證會根據 5 個 tuple 資訊檢查進出虛擬機器的封包是受到允許或拒絕。</span><span class="sxs-lookup"><span data-stu-id="74c2d-104">IP flow verify checks if a packet is allowed or denied to or from a virtual machine based on 5-tuple information.</span></span> <span data-ttu-id="74c2d-105">這些資訊包括方向、通訊協定、本機 IP、遠端 IP、本機連接埠和遠端連接埠。</span><span class="sxs-lookup"><span data-stu-id="74c2d-105">This information consists of direction, protocol, local IP, remote IP, local port, and remote port.</span></span> <span data-ttu-id="74c2d-106">如果封包遭到安全性群組拒絕，則會傳回拒絕封包之規則的名稱。</span><span class="sxs-lookup"><span data-stu-id="74c2d-106">If the packet is denied by a security group, the name of the rule that denied the packet is returned.</span></span> <span data-ttu-id="74c2d-107">雖然任何來源或目的地 IP 均可供選擇，但這項功能可協助系統管理員快速診斷網際網路和內部部署環境的往來連線問題。</span><span class="sxs-lookup"><span data-stu-id="74c2d-107">While any source or destination IP can be chosen, this feature helps administrators quickly diagnose connectivity issues from or to the internet and from or to the on-premises environment.</span></span>

<span data-ttu-id="74c2d-108">IP 流量驗證是以虛擬機器的網路介面做為目標。</span><span class="sxs-lookup"><span data-stu-id="74c2d-108">IP flow verify targets a network interface of a virtual machine.</span></span> <span data-ttu-id="74c2d-109">接著會根據所設的設定，驗證該網路介面往來的流量。</span><span class="sxs-lookup"><span data-stu-id="74c2d-109">Traffic flow is then verified based on the configured settings to or from that network interface.</span></span> <span data-ttu-id="74c2d-110">這項功能可用於確認網路安全性群組中的規則是否會封鎖虛擬機器的輸入或輸出流量。</span><span class="sxs-lookup"><span data-stu-id="74c2d-110">This capability is useful in confirming if a rule in a Network Security Group is blocking ingress or egress traffic to or from a virtual machine.</span></span>

<span data-ttu-id="74c2d-111">在您計劃執行 IP 流量驗證的所有區域中，都必須建立網路監看員執行個體。</span><span class="sxs-lookup"><span data-stu-id="74c2d-111">An instance of Network Watcher needs to be created in all regions that you plan to run IP flow verify.</span></span> <span data-ttu-id="74c2d-112">網路監看員是區域性服務，只能針對相同區域中的資源執行。</span><span class="sxs-lookup"><span data-stu-id="74c2d-112">Network Watcher is a regional service and can only be ran against resources in the same region.</span></span> <span data-ttu-id="74c2d-113">這不會影響 IP 流量驗證的結果，因為與 NIC 相關聯的路由仍會傳回。</span><span class="sxs-lookup"><span data-stu-id="74c2d-113">This does not affect the results of IP flow verify as the route associated with the NIC will still be returned.</span></span>

![1][1]

## <a name="next-steps"></a><span data-ttu-id="74c2d-115">後續步驟</span><span class="sxs-lookup"><span data-stu-id="74c2d-115">Next steps</span></span>

<span data-ttu-id="74c2d-116">瀏覽下列文章，以透過入口網站了解特定虛擬機器的封包是受到允許或拒絕。</span><span class="sxs-lookup"><span data-stu-id="74c2d-116">Visit the following article to learn if a packet is allowed or denied for a specific virtual machine through the portal.</span></span> [<span data-ttu-id="74c2d-117">使用入口網站以 IP 流量驗證檢查 VM 上的流量是否受到允許</span><span class="sxs-lookup"><span data-stu-id="74c2d-117">Check if traffic is allowed on a VM with IP Flow Verify using the portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)

[1]: ./media/network-watcher-ip-flow-verify-overview/figure1.png












