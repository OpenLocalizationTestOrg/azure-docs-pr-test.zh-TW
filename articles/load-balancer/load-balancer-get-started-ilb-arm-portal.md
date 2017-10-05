---
title: "建立內部負載平衡器 - Azure 入口網站 | Microsoft Docs"
description: "了解如何使用 Azure 入口網站在資源管理員中建立內部負載平衡器"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 1ac14fb9-8d14-4892-bfe6-8bc74c48ae2c
ms.service: load-balancer
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 8fbe9d5d04d745de51e0e41516d6c12683c98637
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-internal-load-balancer-in-the-azure-portal"></a><span data-ttu-id="bda6f-103">在 Azure 入口網站中建立內部負載平衡器</span><span class="sxs-lookup"><span data-stu-id="bda6f-103">Create an Internal load balancer in the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="bda6f-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="bda6f-104">Azure Portal</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [<span data-ttu-id="bda6f-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bda6f-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [<span data-ttu-id="bda6f-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="bda6f-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [<span data-ttu-id="bda6f-107">範本</span><span class="sxs-lookup"><span data-stu-id="bda6f-107">Template</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="bda6f-108">Azure 建立和處理資源的部署模型有二種：[Resource Manager 和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="bda6f-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="bda6f-109">本文涵蓋之內容包括使用 Resource Manager 部署模型，Microsoft 建議大部分的新部署使用此模型，而不是[傳統部署模型](load-balancer-get-started-ilb-classic-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="bda6f-109">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the [classic deployment model](load-balancer-get-started-ilb-classic-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="get-started-creating-an-internal-load-balancer-using-azure-portal"></a><span data-ttu-id="bda6f-110">開始使用 Azure 入口網站建立內部負載平衡器</span><span class="sxs-lookup"><span data-stu-id="bda6f-110">Get started creating an Internal load balancer using Azure portal</span></span>

<span data-ttu-id="bda6f-111">請使用下列步驟，從 Azure 入口網站建立內部負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="bda6f-111">Use the following steps to create an internal load balancer from the Azure Portal.</span></span>

1. <span data-ttu-id="bda6f-112">開啟瀏覽器，瀏覽至 [Azure 入口網站](http://portal.azure.com)，並使用您的 Azure 帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="bda6f-112">Open a browser, navigate to the [Azure portal](http://portal.azure.com), and sign in with your Azure account.</span></span>
2. <span data-ttu-id="bda6f-113">在畫面的左上方，按一下 [新增] > [網路] > [負載平衡器]。</span><span class="sxs-lookup"><span data-stu-id="bda6f-113">In the upper left hand side of the screen, click **New** > **Networking** > **Load balancer**.</span></span>
3. <span data-ttu-id="bda6f-114">在 [建立負載平衡器] 刀鋒視窗中，輸入負載平衡器的**名稱**。</span><span class="sxs-lookup"><span data-stu-id="bda6f-114">In the **Create load balancer** blade, enter a **Name** for your load balancer.</span></span>
4. <span data-ttu-id="bda6f-115">在 [配置] 中，按一下 [內部]。</span><span class="sxs-lookup"><span data-stu-id="bda6f-115">Under **Scheme**, click **Internal**.</span></span>
5. <span data-ttu-id="bda6f-116">按一下 [虛擬網路] ，然後選取您要建立負載平衡器的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="bda6f-116">Click **Virtual network**, and then select the virtual network where you want to create the load balancer.</span></span>

   > [!NOTE]
   > <span data-ttu-id="bda6f-117">如果沒看到想要使用的虛擬網路，請檢查您為負載平衡器使用的 **位置** ，並據以變更它。</span><span class="sxs-lookup"><span data-stu-id="bda6f-117">If you do not see the virtual network you want to use, check the **Location** you are using for the load balancer, and change it accordingly.</span></span>

6. <span data-ttu-id="bda6f-118">按一下 [子網路] ，然後選取您要建立負載平衡器的子網路。</span><span class="sxs-lookup"><span data-stu-id="bda6f-118">Click **Subnet**, and then select the subnet where you want to create the load balancer.</span></span>
7. <span data-ttu-id="bda6f-119">在 [IP 位址指派] 下，按一下 [動態] 或 [靜態]，視您想要讓負載平衡器的 IP 位址固定 (靜態) 或不固定而定。</span><span class="sxs-lookup"><span data-stu-id="bda6f-119">Under **IP address assignment**, click either **Dynamic** or **Static**, depending on whether you want the IP address for the load balancer to be fixed (static) or not.</span></span>

   > [!NOTE]
   > <span data-ttu-id="bda6f-120">如果您選擇使用靜態 IP 位址，您必須提供負載平衡器的位址。</span><span class="sxs-lookup"><span data-stu-id="bda6f-120">If you select to use a static IP address, you will have to provide an address for the load balancer.</span></span>

8. <span data-ttu-id="bda6f-121">在 [資源群組] 下，指定負載平衡器的新資源群組名稱，或按一下 [選取現有]，然後選取現有的資源群組。</span><span class="sxs-lookup"><span data-stu-id="bda6f-121">Under **Resource group** either specify the name of a new resource group for the load balancer, or click **select existing** and select an existing resource group.</span></span>
9. <span data-ttu-id="bda6f-122">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="bda6f-122">Click **Create**.</span></span>

## <a name="configure-load-balancing-rules"></a><span data-ttu-id="bda6f-123">設定負載平衡規則</span><span class="sxs-lookup"><span data-stu-id="bda6f-123">Configure load balancing rules</span></span>

<span data-ttu-id="bda6f-124">負載平衡器建立之後，瀏覽至負載平衡器資源來設定它。</span><span class="sxs-lookup"><span data-stu-id="bda6f-124">After the load balancer creation, navigate to the load balancer resource to configure it.</span></span>
<span data-ttu-id="bda6f-125">您必須先設定後端位址集區和探查，然後再設定負載平衡規則。</span><span class="sxs-lookup"><span data-stu-id="bda6f-125">You need to configure first a back-end address pool and a probe before configuring a load balancing rule.</span></span>

### <a name="step-1-configure-a-back-end-pool"></a><span data-ttu-id="bda6f-126">步驟 1：設定後端集區</span><span class="sxs-lookup"><span data-stu-id="bda6f-126">Step 1: Configure a back-end pool</span></span>

1. <span data-ttu-id="bda6f-127">在 Azure 入口網站中，按一下 [瀏覽] > [負載平衡器]，然後按一下您先前建立的負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="bda6f-127">In the Azure portal, click **Browse** > **Load balancers**, and then click the load balancer you created above.</span></span>
2. <span data-ttu-id="bda6f-128">在 [設定] 刀鋒視窗中，按一下 [後端集區]。</span><span class="sxs-lookup"><span data-stu-id="bda6f-128">In the **Settings** blade, click **Backend pools**.</span></span>
3. <span data-ttu-id="bda6f-129">在 [後端位址集區] 刀鋒視窗中，按一下 [加入]。</span><span class="sxs-lookup"><span data-stu-id="bda6f-129">In the **Backend address pools** blade, click **Add**.</span></span>
4. <span data-ttu-id="bda6f-130">在 [加入後端集區] 刀鋒視窗中，輸入後端集區的**名稱**，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="bda6f-130">In the **Add backend pool** blade, enter a **Name** for the backend pool, and then click **OK**.</span></span>

### <a name="step-2-configure-a-probe"></a><span data-ttu-id="bda6f-131">步驟 2：設定探查</span><span class="sxs-lookup"><span data-stu-id="bda6f-131">Step 2: Configure a probe</span></span>

1. <span data-ttu-id="bda6f-132">在 Azure 入口網站中，按一下 [瀏覽] > [負載平衡器]，然後按一下您先前建立的負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="bda6f-132">In the Azure portal, click **Browse** > **Load balancers**, and then click the load balancer you created above.</span></span>
2. <span data-ttu-id="bda6f-133">在 [設定] 刀鋒視窗中，按一下 [探查]。</span><span class="sxs-lookup"><span data-stu-id="bda6f-133">In the **Settings** blade, click **Probes**.</span></span>
3. <span data-ttu-id="bda6f-134">在 [探查] 刀鋒視窗中，按一下 [加入]。</span><span class="sxs-lookup"><span data-stu-id="bda6f-134">In the **Probes**  blade, click **Add**.</span></span>
4. <span data-ttu-id="bda6f-135">在 [加入探查] 刀鋒視窗中，輸入探查的**名稱**。</span><span class="sxs-lookup"><span data-stu-id="bda6f-135">In the **Add probe** blade, enter a **Name** for the probe.</span></span>
5. <span data-ttu-id="bda6f-136">在 [通訊協定] 下，選取 [HTTP] \(適用於網站) 或 [TCP] \(適用於其他 TCP 型應用程式)。</span><span class="sxs-lookup"><span data-stu-id="bda6f-136">Under **Protocol**, select **HTTP** (for web sites) or **TCP** (for other TCP based applications).</span></span>
6. <span data-ttu-id="bda6f-137">在 [連接埠] 下，指定用於存取探查的連接埠。</span><span class="sxs-lookup"><span data-stu-id="bda6f-137">Under **Port**, specify the port to use when accessing the probe.</span></span>
7. <span data-ttu-id="bda6f-138">在 [路徑]  \(僅適用於 HTTP 探查) 下，指定要用來作為探查的路徑。</span><span class="sxs-lookup"><span data-stu-id="bda6f-138">Under **Path** (for HTTP probes only), specify the path to use as a probe.</span></span>
8. <span data-ttu-id="bda6f-139">在 [間隔]  下，指定探查應用程式的頻率。</span><span class="sxs-lookup"><span data-stu-id="bda6f-139">Under **Interval** specify how frequently to probe the application.</span></span>
9. <span data-ttu-id="bda6f-140">在 [狀況不良臨界值] 下，指定後端虛擬機器標示為狀況不良之前，應該失敗的嘗試次數。</span><span class="sxs-lookup"><span data-stu-id="bda6f-140">Under **Unhealthy threshold**, specify how many attempts should fail before the backend virtual machine is marked as unhealthy.</span></span>
10. <span data-ttu-id="bda6f-141">按一下 [確定]  以建立探查。</span><span class="sxs-lookup"><span data-stu-id="bda6f-141">Click **OK** to create probe.</span></span>

### <a name="step-3-configure-load-balancing-rules"></a><span data-ttu-id="bda6f-142">步驟 3：設定負載平衡規則</span><span class="sxs-lookup"><span data-stu-id="bda6f-142">Step 3: Configure load balancing rules</span></span>

1. <span data-ttu-id="bda6f-143">在 Azure 入口網站中，按一下 [瀏覽] > [負載平衡器]，然後按一下您先前建立的負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="bda6f-143">In the Azure portal, click **Browse** > **Load balancers**, and then click the load balancer you created above.</span></span>
2. <span data-ttu-id="bda6f-144">在 [設定] 刀鋒視窗中，按一下 [負載平衡規則]。</span><span class="sxs-lookup"><span data-stu-id="bda6f-144">In the **Settings** blade, click **Load balancing rules**.</span></span>
3. <span data-ttu-id="bda6f-145">在 [負載平衡規則] 刀鋒視窗中，按一下 [加入]。</span><span class="sxs-lookup"><span data-stu-id="bda6f-145">In the **Load balancing rules** blade, click **Add**.</span></span>
4. <span data-ttu-id="bda6f-146">在 [加入負載平衡規則] 刀鋒視窗中，輸入規則的**名稱**。</span><span class="sxs-lookup"><span data-stu-id="bda6f-146">In the **Add load balancing rule** blade, enter a **Name** for the rule.</span></span>
5. <span data-ttu-id="bda6f-147">在 [通訊協定] 下，選取 [HTTP]\(適用於網站) 或 [TCP] \(適用於其他 TCP 型應用程式)。</span><span class="sxs-lookup"><span data-stu-id="bda6f-147">Under **Protocol**, select **HTTP** (for web sites) or **TCP** (for other TCP based applications).</span></span>
6. <span data-ttu-id="bda6f-148">在 [連接埠] 下，指定用戶端在負載平衡器中連接的連接埠。</span><span class="sxs-lookup"><span data-stu-id="bda6f-148">Under **Port**, specify the port clients connect to in the load balancer.</span></span>
7. <span data-ttu-id="bda6f-149">在 [後端連接埠] 下，指定要用於後端集區的連接埠 (負載平衡器連接埠和後端連接埠通常會相同)。</span><span class="sxs-lookup"><span data-stu-id="bda6f-149">Under **Backend port**, specify the port to be used in the backend pool (usually, the load balancer port and the backend port are the same).</span></span>
8. <span data-ttu-id="bda6f-150">在 [後端集區] 下，選取您先前建立的後端集區。</span><span class="sxs-lookup"><span data-stu-id="bda6f-150">Under **Backend pool**, select the backend pool you created above.</span></span>
9. <span data-ttu-id="bda6f-151">在 [工作階段持續性] 下，選取要保存工作階段的方式。</span><span class="sxs-lookup"><span data-stu-id="bda6f-151">Under **Session persistence**, select how you want sessions to persist.</span></span>
10. <span data-ttu-id="bda6f-152">在 [閒置逾時 (分鐘)] 下，指定閒置逾時。</span><span class="sxs-lookup"><span data-stu-id="bda6f-152">Under **Idle timeout (minutes)**, specify the idle timeout.</span></span>
11. <span data-ttu-id="bda6f-153">在 [浮動 IP (伺服器直接回傳)] 下，按一下 [停用] 或 [啟用]。</span><span class="sxs-lookup"><span data-stu-id="bda6f-153">Under **Floating IP (direct server return)**, click **Disabled** or **Enabled**.</span></span>
12. <span data-ttu-id="bda6f-154">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="bda6f-154">Click **OK**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bda6f-155">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bda6f-155">Next steps</span></span>

[<span data-ttu-id="bda6f-156">設定負載平衡器分配模式</span><span class="sxs-lookup"><span data-stu-id="bda6f-156">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="bda6f-157">設定負載平衡器的閒置 TCP 逾時設定</span><span class="sxs-lookup"><span data-stu-id="bda6f-157">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

