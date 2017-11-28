---
title: "aaaCreate 網際網路對向負載平衡器-傳統 Azure 入口網站 |Microsoft 文件"
description: "了解如何在模型中使用傳統部署使用網際網路對向負載平衡器 toocreate hello Azure 傳統入口網站"
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
ms.openlocfilehash: 27b0d5af6e7b493fa94a9dfbfa260483ae95a2fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-hello-azure-classic-portal"></a><span data-ttu-id="31f8f-103">開始建立網際網路對向 hello Azure 傳統入口網站中的負載平衡器 （傳統）</span><span class="sxs-lookup"><span data-stu-id="31f8f-103">Get started creating an Internet facing load balancer (classic) in hello Azure classic portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="31f8f-104">Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="31f8f-104">Azure classic portal</span></span>](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [<span data-ttu-id="31f8f-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="31f8f-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [<span data-ttu-id="31f8f-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="31f8f-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [<span data-ttu-id="31f8f-107">Azure 雲端服務</span><span class="sxs-lookup"><span data-stu-id="31f8f-107">Azure Cloud Services</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="31f8f-108">您可以使用 Azure 資源之前，它是 Azure 目前有兩種部署模型的重要 toounderstand: Azure 資源管理員] 和 [傳統。</span><span class="sxs-lookup"><span data-stu-id="31f8f-108">Before you work with Azure resources, it's important toounderstand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="31f8f-109">在使用任何 Azure 資源之前，請先確認您了解 [部署模型和工具](../azure-classic-rm.md) 。</span><span class="sxs-lookup"><span data-stu-id="31f8f-109">Make sure you understand [deployment models and tools](../azure-classic-rm.md) before you work with any Azure resource.</span></span> <span data-ttu-id="31f8f-110">您可以按一下上方的這篇文章 hello hello 索引標籤檢視 hello 文件不同的工具。</span><span class="sxs-lookup"><span data-stu-id="31f8f-110">You can view hello documentation for different tools by clicking hello tabs at hello top of this article.</span></span> <span data-ttu-id="31f8f-111">本文涵蓋 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="31f8f-111">This article covers hello classic deployment model.</span></span> <span data-ttu-id="31f8f-112">您也可以[toocreate 網際網路向負載平衡器使用 Azure 資源管理員的如何了解](load-balancer-get-started-internet-arm-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="31f8f-112">You can also [Learn how toocreate an Internet facing load balancer using Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="set-up-an-internet-facing-load-balancer-for-virtual-machines"></a><span data-ttu-id="31f8f-113">為虛擬機器設定網際網路面向的負載平衡器</span><span class="sxs-lookup"><span data-stu-id="31f8f-113">Set up an Internet-facing load balancer for virtual machines</span></span>

<span data-ttu-id="31f8f-114">在訂單 tooload 平衡網路流量從 hello 網際網路跨 hello 虛擬機器的雲端服務，您必須建立一組負載平衡。</span><span class="sxs-lookup"><span data-stu-id="31f8f-114">In order tooload balance network traffic from hello Internet across hello virtual machines of a cloud service, you must create a load-balanced set.</span></span> <span data-ttu-id="31f8f-115">此程序假設您已經建立 hello 虛擬機器，而且必須為所有內 hello 相同雲端服務。</span><span class="sxs-lookup"><span data-stu-id="31f8f-115">This procedure assumes that you have already created hello virtual machines and that they are all within hello same cloud service.</span></span>

<span data-ttu-id="31f8f-116">**tooconfigure 一組負載平衡的虛擬機器**</span><span class="sxs-lookup"><span data-stu-id="31f8f-116">**tooconfigure a load-balanced set for virtual machines**</span></span>

1. <span data-ttu-id="31f8f-117">在 hello Azure 傳統入口網站，按一下 **虛擬機器**，然後按一下hello hello 負載平衡集內的虛擬機器的名稱。</span><span class="sxs-lookup"><span data-stu-id="31f8f-117">In hello Azure classic portal, click **Virtual Machines**, and then click hello name of a virtual machine in hello load-balanced set.</span></span>
2. <span data-ttu-id="31f8f-118">選取 端點，然後按一下新增。</span><span class="sxs-lookup"><span data-stu-id="31f8f-118">Click **Endpoints**, and then click **Add**.</span></span>
3. <span data-ttu-id="31f8f-119">在 hello**加入端點 tooa 的虛擬機器**頁面上，按一下向右箭號 hello。</span><span class="sxs-lookup"><span data-stu-id="31f8f-119">On hello **Add an endpoint tooa virtual machine** page, click hello right arrow.</span></span>
4. <span data-ttu-id="31f8f-120">在 hello**指定 hello hello 端點詳細資料**頁面：</span><span class="sxs-lookup"><span data-stu-id="31f8f-120">On hello **Specify hello details of hello endpoint** page:</span></span>

   * <span data-ttu-id="31f8f-121">在**名稱**，輸入 hello 端點的名稱，或從 hello 預先定義的端點針對常用的通訊協定清單中選取 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="31f8f-121">In **Name**, type a name for hello endpoint or select hello name from hello list of predefined endpoints for common protocols.</span></span>
   * <span data-ttu-id="31f8f-122">在**通訊協定**，視需要選取 hello hello 類型的端點，TCP 或 UDP，所需的通訊協定。</span><span class="sxs-lookup"><span data-stu-id="31f8f-122">In **Protocol**, select hello protocol required by hello type of endpoint, either TCP or UDP, as needed.</span></span>
   * <span data-ttu-id="31f8f-123">在**公用連接埠和私用連接埠**，輸入您想要的 hello 虛擬機器 toouse 視 hello 連接埠號碼。</span><span class="sxs-lookup"><span data-stu-id="31f8f-123">In **Public Port and Private Port**, type hello port numbers that you want hello virtual machine toouse, as needed.</span></span> <span data-ttu-id="31f8f-124">您可以使用 hello 私用連接埠和防火牆規則上 hello 虛擬機器 tooredirect 流量適用於您的應用程式的方式。</span><span class="sxs-lookup"><span data-stu-id="31f8f-124">You can use hello private port and firewall rules on hello virtual machine tooredirect traffic in a way that is appropriate for your application.</span></span> <span data-ttu-id="31f8f-125">hello 私用連接埠可以 hello 與 hello 公用連接埠相同。</span><span class="sxs-lookup"><span data-stu-id="31f8f-125">hello private port can be hello same as hello public port.</span></span> <span data-ttu-id="31f8f-126">比方說，對於 web (HTTP) 流量的端點，您無法將指派連接埠 80 tooboth hello 公用和私用連接埠。</span><span class="sxs-lookup"><span data-stu-id="31f8f-126">For example, for an endpoint for web (HTTP) traffic, you could assign port 80 tooboth hello public and private port.</span></span>

5. <span data-ttu-id="31f8f-127">選取**建立負載平衡集**，然後按一下hello 向右箭號。</span><span class="sxs-lookup"><span data-stu-id="31f8f-127">Select **Create a load-balanced set**, and then click hello right arrow.</span></span>
6. <span data-ttu-id="31f8f-128">在 hello**設定 hello 負載平衡集**頁面，輸入 hello 負載平衡集名稱，然後再指派 hello hello Azure 負載平衡器的探查行為值。</span><span class="sxs-lookup"><span data-stu-id="31f8f-128">On hello **Configure hello load-balanced set** page, type a name for hello load-balanced set, and then assign hello values for probe behavior of hello Azure Load Balancer.</span></span> <span data-ttu-id="31f8f-129">hello 負載平衡器使用探查 toodetermine hello hello 負載平衡集內的虛擬機器時可用的 tooreceive 連入流量。</span><span class="sxs-lookup"><span data-stu-id="31f8f-129">hello Load Balancer uses probes toodetermine if hello virtual machines in hello load-balanced set are available tooreceive incoming traffic.</span></span>
7. <span data-ttu-id="31f8f-130">按一下 hello 核取記號 toocreate hello 負載平衡的端點。</span><span class="sxs-lookup"><span data-stu-id="31f8f-130">Click hello check mark toocreate hello load-balanced endpoint.</span></span> <span data-ttu-id="31f8f-131">您會看到**是**在 hello**負載平衡集名稱**資料行的 hello**端點**hello 虛擬機器的頁面。</span><span class="sxs-lookup"><span data-stu-id="31f8f-131">You will see **Yes** in hello **Load-balanced set name** column of hello **Endpoints** page for hello virtual machine.</span></span>
8. <span data-ttu-id="31f8f-132">在 hello 入口網站中，按一下 **虛擬機器**，按一下 hello hello 負載平衡集內的其他虛擬機器名稱，按一下**端點**，然後按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="31f8f-132">In hello portal, click **Virtual Machines**, click hello name of an additional virtual machine in hello load-balanced set, click **Endpoints**, and then click **Add**.</span></span>
9. <span data-ttu-id="31f8f-133">在 hello**加入端點 tooa 的虛擬機器**頁面上，按一下**新增端點 tooan 現有負載平衡集**選取 hello hello 負載平衡集名稱，然後按一下hello 向右箭號。</span><span class="sxs-lookup"><span data-stu-id="31f8f-133">On hello **Add an endpoint tooa virtual machine** page, click **Add endpoint tooan existing load-balanced set**, select hello name of hello load-balanced set, and then click hello right arrow.</span></span>
10. <span data-ttu-id="31f8f-134">在 hello**指定 hello hello 端點詳細資料**頁面上，輸入 hello 端點的名稱，然後按一下hello 核取記號。</span><span class="sxs-lookup"><span data-stu-id="31f8f-134">On hello **Specify hello details of hello endpoint** page, type a name for hello endpoint, and then click hello check mark.</span></span>

<span data-ttu-id="31f8f-135">Hello 其他虛擬機器的 hello 負載平衡集內，重複步驟 8-10。</span><span class="sxs-lookup"><span data-stu-id="31f8f-135">For hello additional virtual machines in hello load-balanced set, repeat steps 8-10.</span></span>

## <a name="next-steps"></a><span data-ttu-id="31f8f-136">後續步驟</span><span class="sxs-lookup"><span data-stu-id="31f8f-136">Next steps</span></span>

[<span data-ttu-id="31f8f-137">開始設定內部負載平衡器</span><span class="sxs-lookup"><span data-stu-id="31f8f-137">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="31f8f-138">設定負載平衡器分配模式</span><span class="sxs-lookup"><span data-stu-id="31f8f-138">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="31f8f-139">設定負載平衡器的閒置 TCP 逾時設定</span><span class="sxs-lookup"><span data-stu-id="31f8f-139">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
