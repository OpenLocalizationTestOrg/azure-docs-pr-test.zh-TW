---
title: "建立網際網路對向負載平衡器 - Azure 入口網站傳統 | Microsoft Docs"
description: "了解如何使用 Azure 傳統入口網站在傳統部署模型中建立網際網路面向的負載平衡器"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: fa3e93c0-968a-472d-a17c-65665c050db2
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: a022154f5eca6de2d2dbfc1b9aa30d2ea0a7d650
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-the-azure-classic-portal"></a><span data-ttu-id="b3fb9-103">開始在 Azure 傳統入口網站中建立網際網路面向的負載平衡器 (傳統)</span><span class="sxs-lookup"><span data-stu-id="b3fb9-103">Get started creating an Internet facing load balancer (classic) in the Azure classic portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="b3fb9-104">Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="b3fb9-104">Azure classic portal</span></span>](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [<span data-ttu-id="b3fb9-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b3fb9-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [<span data-ttu-id="b3fb9-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b3fb9-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [<span data-ttu-id="b3fb9-107">Azure 雲端服務</span><span class="sxs-lookup"><span data-stu-id="b3fb9-107">Azure Cloud Services</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="b3fb9-108">使用 Azure 資源之前，請務必了解 Azure 目前有 Azure Resource Manager 和「傳統」兩種部署模型。</span><span class="sxs-lookup"><span data-stu-id="b3fb9-108">Before you work with Azure resources, it's important to understand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="b3fb9-109">在使用任何 Azure 資源之前，請先確認您了解 [部署模型和工具](../azure-classic-rm.md) 。</span><span class="sxs-lookup"><span data-stu-id="b3fb9-109">Make sure you understand [deployment models and tools](../azure-classic-rm.md) before you work with any Azure resource.</span></span> <span data-ttu-id="b3fb9-110">您可以按一下本文頂端的索引標籤，檢視不同工具的文件。</span><span class="sxs-lookup"><span data-stu-id="b3fb9-110">You can view the documentation for different tools by clicking the tabs at the top of this article.</span></span> <span data-ttu-id="b3fb9-111">本文涵蓋之內容包括傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="b3fb9-111">This article covers the classic deployment model.</span></span> <span data-ttu-id="b3fb9-112">您也可以 [了解如何使用 Azure 資源管理員建立網際網路面向的負載平衡器](load-balancer-get-started-internet-arm-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="b3fb9-112">You can also [Learn how to create an Internet facing load balancer using Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="set-up-an-internet-facing-load-balancer-for-virtual-machines"></a><span data-ttu-id="b3fb9-113">為虛擬機器設定網際網路面向的負載平衡器</span><span class="sxs-lookup"><span data-stu-id="b3fb9-113">Set up an Internet-facing load balancer for virtual machines</span></span>

<span data-ttu-id="b3fb9-114">為了使雲端服務的各虛擬機器的網際網路流量達到負載平衡，您必須建立負載平衡的集合。</span><span class="sxs-lookup"><span data-stu-id="b3fb9-114">In order to load balance network traffic from the Internet across the virtual machines of a cloud service, you must create a load-balanced set.</span></span> <span data-ttu-id="b3fb9-115">此程序假設您已建立虛擬機器，而且全都在相同的雲端服務內。</span><span class="sxs-lookup"><span data-stu-id="b3fb9-115">This procedure assumes that you have already created the virtual machines and that they are all within the same cloud service.</span></span>

<span data-ttu-id="b3fb9-116">**設定虛擬機器的負載平衡集合**</span><span class="sxs-lookup"><span data-stu-id="b3fb9-116">**To configure a load-balanced set for virtual machines**</span></span>

1. <span data-ttu-id="b3fb9-117">在 Azure 傳統入口網站中，按一下 [虛擬機器] ，然後按一下負載平衡集合中虛擬機器的名稱。</span><span class="sxs-lookup"><span data-stu-id="b3fb9-117">In the Azure classic portal, click **Virtual Machines**, and then click the name of a virtual machine in the load-balanced set.</span></span>
2. <span data-ttu-id="b3fb9-118">選取 [端點]，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="b3fb9-118">Click **Endpoints**, and then click **Add**.</span></span>
3. <span data-ttu-id="b3fb9-119">在 [將端點加入至虛擬機器]  頁面上，按一下向右箭頭。</span><span class="sxs-lookup"><span data-stu-id="b3fb9-119">On the **Add an endpoint to a virtual machine** page, click the right arrow.</span></span>
4. <span data-ttu-id="b3fb9-120">在 [指定端點的詳細資料]  頁面上：</span><span class="sxs-lookup"><span data-stu-id="b3fb9-120">On the **Specify the details of the endpoint** page:</span></span>

   * <span data-ttu-id="b3fb9-121">在 [名稱] 中輸入端點的名稱，或從常見通訊協定的預先定義端點清單中選取名稱。</span><span class="sxs-lookup"><span data-stu-id="b3fb9-121">In **Name**, type a name for the endpoint or select the name from the list of predefined endpoints for common protocols.</span></span>
   * <span data-ttu-id="b3fb9-122">在 [通訊協定] 中，選取端點類型所需的通訊協定 (視需要選擇 TCP 或 UDP)。</span><span class="sxs-lookup"><span data-stu-id="b3fb9-122">In **Protocol**, select the protocol required by the type of endpoint, either TCP or UDP, as needed.</span></span>
   * <span data-ttu-id="b3fb9-123">在 [公用連接埠和私人連接埠] 中，視需要輸入要虛擬機器使用的連接埠號碼。</span><span class="sxs-lookup"><span data-stu-id="b3fb9-123">In **Public Port and Private Port**, type the port numbers that you want the virtual machine to use, as needed.</span></span> <span data-ttu-id="b3fb9-124">您可以在虛擬機器上使用私人連接埠和防火牆規則，以適合應用程式的方式來重新導向流量。</span><span class="sxs-lookup"><span data-stu-id="b3fb9-124">You can use the private port and firewall rules on the virtual machine to redirect traffic in a way that is appropriate for your application.</span></span> <span data-ttu-id="b3fb9-125">私人連接埠可與公用連接埠相同。</span><span class="sxs-lookup"><span data-stu-id="b3fb9-125">The private port can be the same as the public port.</span></span> <span data-ttu-id="b3fb9-126">例如，對於 Web (HTTP) 端點的流量，您可以將連接埠 80 同時指派給公用和私人連接埠。</span><span class="sxs-lookup"><span data-stu-id="b3fb9-126">For example, for an endpoint for web (HTTP) traffic, you could assign port 80 to both the public and private port.</span></span>

5. <span data-ttu-id="b3fb9-127">選取 [Create a load-balanced set] ，然後按一下向右箭頭。</span><span class="sxs-lookup"><span data-stu-id="b3fb9-127">Select **Create a load-balanced set**, and then click the right arrow.</span></span>
6. <span data-ttu-id="b3fb9-128">在 [設定負載平衡集合]  頁面上，輸入負載平衡集合的名稱，然後指派 Azure 負載平衡器探查行為的值。</span><span class="sxs-lookup"><span data-stu-id="b3fb9-128">On the **Configure the load-balanced set** page, type a name for the load-balanced set, and then assign the values for probe behavior of the Azure Load Balancer.</span></span> <span data-ttu-id="b3fb9-129">負載平衡器會使用探查，來判斷負載平衡集合中的虛擬機器是否可用於接收連入流量。</span><span class="sxs-lookup"><span data-stu-id="b3fb9-129">The Load Balancer uses probes to determine if the virtual machines in the load-balanced set are available to receive incoming traffic.</span></span>
7. <span data-ttu-id="b3fb9-130">按一下核取記號以建立負載平衡端點。</span><span class="sxs-lookup"><span data-stu-id="b3fb9-130">Click the check mark to create the load-balanced endpoint.</span></span> <span data-ttu-id="b3fb9-131">您會在虛擬機器的 [端點] 頁面的 [Load-balanced set name] 欄中看見 [是]。</span><span class="sxs-lookup"><span data-stu-id="b3fb9-131">You will see **Yes** in the **Load-balanced set name** column of the **Endpoints** page for the virtual machine.</span></span>
8. <span data-ttu-id="b3fb9-132">在入口網站中，依序按一下 [虛擬機器]、負載平衡集中其他虛擬機器的名稱、[端點]，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="b3fb9-132">In the portal, click **Virtual Machines**, click the name of an additional virtual machine in the load-balanced set, click **Endpoints**, and then click **Add**.</span></span>
9. <span data-ttu-id="b3fb9-133">在 [將端點加入至虛擬機器] 頁面上，按一下 [將端點加入至現有的負載平衡集]、選取負載平衡集的名稱，然後按一下向右箭頭。</span><span class="sxs-lookup"><span data-stu-id="b3fb9-133">On the **Add an endpoint to a virtual machine** page, click **Add endpoint to an existing load-balanced set**, select the name of the load-balanced set, and then click the right arrow.</span></span>
10. <span data-ttu-id="b3fb9-134">在 [指定端點的詳細資料]  頁面上，輸入端點的名稱，然後按一下核取記號。</span><span class="sxs-lookup"><span data-stu-id="b3fb9-134">On the **Specify the details of the endpoint** page, type a name for the endpoint, and then click the check mark.</span></span>

<span data-ttu-id="b3fb9-135">針對負載平衡集合中的其他虛擬機器，重複步驟 8-10。</span><span class="sxs-lookup"><span data-stu-id="b3fb9-135">For the additional virtual machines in the load-balanced set, repeat steps 8-10.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b3fb9-136">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b3fb9-136">Next steps</span></span>

[<span data-ttu-id="b3fb9-137">開始設定內部負載平衡器</span><span class="sxs-lookup"><span data-stu-id="b3fb9-137">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="b3fb9-138">設定負載平衡器分配模式</span><span class="sxs-lookup"><span data-stu-id="b3fb9-138">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="b3fb9-139">設定負載平衡器的閒置 TCP 逾時設定</span><span class="sxs-lookup"><span data-stu-id="b3fb9-139">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
