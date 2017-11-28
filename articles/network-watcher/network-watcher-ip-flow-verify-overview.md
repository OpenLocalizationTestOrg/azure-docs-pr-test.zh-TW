---
title: "在 Azure 網路監看員確認 aaaIntroduction tooIP 流程 |Microsoft 文件"
description: "此頁面提供概觀的 hello 網路監看員 IP 流量確認功能"
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
ms.openlocfilehash: b648a4816a7ffdc6ca54462944b574e2395e8298
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooip-flow-verify-in-azure-network-watcher"></a><span data-ttu-id="44f29-103">簡介 tooIP 流程確認在 Azure 網路監看員</span><span class="sxs-lookup"><span data-stu-id="44f29-103">Introduction tooIP flow verify in Azure Network Watcher</span></span>

<span data-ttu-id="44f29-104">如果允許或拒絕 tooor 5-tuple 資訊為基礎的虛擬機器從封包，IP 流量驗證檢查。</span><span class="sxs-lookup"><span data-stu-id="44f29-104">IP flow verify checks if a packet is allowed or denied tooor from a virtual machine based on 5-tuple information.</span></span> <span data-ttu-id="44f29-105">這些資訊包括方向、通訊協定、本機 IP、遠端 IP、本機連接埠和遠端連接埠。</span><span class="sxs-lookup"><span data-stu-id="44f29-105">This information consists of direction, protocol, local IP, remote IP, local port, and remote port.</span></span> <span data-ttu-id="44f29-106">如果安全性群組遭拒絕 hello 封包，會傳回 hello 拒絕 hello 封包的 hello 規則名稱。</span><span class="sxs-lookup"><span data-stu-id="44f29-106">If hello packet is denied by a security group, hello name of hello rule that denied hello packet is returned.</span></span> <span data-ttu-id="44f29-107">這項功能時可以選擇任何來源或目的地 IP，協助系統管理員快速診斷中的連線問題或 toohello 網際網路來回或 toohello 在內部部署環境。</span><span class="sxs-lookup"><span data-stu-id="44f29-107">While any source or destination IP can be chosen, this feature helps administrators quickly diagnose connectivity issues from or toohello internet and from or toohello on-premises environment.</span></span>

<span data-ttu-id="44f29-108">IP 流量驗證是以虛擬機器的網路介面做為目標。</span><span class="sxs-lookup"><span data-stu-id="44f29-108">IP flow verify targets a network interface of a virtual machine.</span></span> <span data-ttu-id="44f29-109">根據設定的 hello 設定 tooor 該網路介面，然後驗證流量。</span><span class="sxs-lookup"><span data-stu-id="44f29-109">Traffic flow is then verified based on hello configured settings tooor from that network interface.</span></span> <span data-ttu-id="44f29-110">這項功能可用於確認從虛擬機器的輸入或輸出流量 tooor 時，是否要封鎖網路安全性群組中的規則。</span><span class="sxs-lookup"><span data-stu-id="44f29-110">This capability is useful in confirming if a rule in a Network Security Group is blocking ingress or egress traffic tooor from a virtual machine.</span></span>

<span data-ttu-id="44f29-111">請確認網路監看員需求 toobe 您計劃 toorun IP 流量的所有區域中建立的執行個體。</span><span class="sxs-lookup"><span data-stu-id="44f29-111">An instance of Network Watcher needs toobe created in all regions that you plan toorun IP flow verify.</span></span> <span data-ttu-id="44f29-112">網路監看員是地區服務，並只對 hello 中的資源已執行相同的區域。</span><span class="sxs-lookup"><span data-stu-id="44f29-112">Network Watcher is a regional service and can only be ran against resources in hello same region.</span></span> <span data-ttu-id="44f29-113">這不會影響的 hello IP 流量的結果，請確認為 hello 與 hello 仍會傳回 NIC 相關聯的路由。</span><span class="sxs-lookup"><span data-stu-id="44f29-113">This does not affect hello results of IP flow verify as hello route associated with hello NIC will still be returned.</span></span>

![1][1]

## <a name="next-steps"></a><span data-ttu-id="44f29-115">後續步驟</span><span class="sxs-lookup"><span data-stu-id="44f29-115">Next steps</span></span>

<span data-ttu-id="44f29-116">如果封包允許或拒絕特定虛擬機器透過 hello 入口網站的下列文章 toolearn hello 請瀏覽。</span><span class="sxs-lookup"><span data-stu-id="44f29-116">Visit hello following article toolearn if a packet is allowed or denied for a specific virtual machine through hello portal.</span></span> [<span data-ttu-id="44f29-117">檢查是否流量允許的 IP 流量驗證 VM 上使用 hello 入口網站</span><span class="sxs-lookup"><span data-stu-id="44f29-117">Check if traffic is allowed on a VM with IP Flow Verify using hello portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)

[1]: ./media/network-watcher-ip-flow-verify-overview/figure1.png












