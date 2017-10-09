---
title: "aaaCreate 內部負載平衡器-Azure 入口網站 |Microsoft 文件"
description: "了解如何 toocreate 內部負載平衡器資源管理員 中使用 hello Azure 入口網站"
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
ms.openlocfilehash: 80124217a84857b542eb41cb814ec97234176dd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internal-load-balancer-in-hello-azure-portal"></a><span data-ttu-id="3a756-103">在 hello Azure 入口網站中建立內部負載平衡器</span><span class="sxs-lookup"><span data-stu-id="3a756-103">Create an Internal load balancer in hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="3a756-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="3a756-104">Azure Portal</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [<span data-ttu-id="3a756-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3a756-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [<span data-ttu-id="3a756-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="3a756-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [<span data-ttu-id="3a756-107">範本</span><span class="sxs-lookup"><span data-stu-id="3a756-107">Template</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="3a756-108">Azure 建立和處理資源的部署模型有二種：[Resource Manager 和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="3a756-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="3a756-109">本文將說明如何使用 hello Resource Manager 部署模型，Microsoft 建議您針對大部分新的部署，而不是 hello[傳統部署模型](load-balancer-get-started-ilb-classic-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="3a756-109">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](load-balancer-get-started-ilb-classic-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="get-started-creating-an-internal-load-balancer-using-azure-portal"></a><span data-ttu-id="3a756-110">開始使用 Azure 入口網站建立內部負載平衡器</span><span class="sxs-lookup"><span data-stu-id="3a756-110">Get started creating an Internal load balancer using Azure portal</span></span>

<span data-ttu-id="3a756-111">使用 hello hello Azure 入口網站中的下列步驟 toocreate 內部負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="3a756-111">Use hello following steps toocreate an internal load balancer from hello Azure Portal.</span></span>

1. <span data-ttu-id="3a756-112">開啟瀏覽器，瀏覽 toohello [Azure 入口網站](http://portal.azure.com)，並以您的 Azure 帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="3a756-112">Open a browser, navigate toohello [Azure portal](http://portal.azure.com), and sign in with your Azure account.</span></span>
2. <span data-ttu-id="3a756-113">Hello 囉 」 畫面的左上方，按一下 **新增** > **網路** > **負載平衡器**。</span><span class="sxs-lookup"><span data-stu-id="3a756-113">In hello upper left hand side of hello screen, click **New** > **Networking** > **Load balancer**.</span></span>
3. <span data-ttu-id="3a756-114">在 hello**建立負載平衡器**刀鋒視窗中，輸入**名稱**您的負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="3a756-114">In hello **Create load balancer** blade, enter a **Name** for your load balancer.</span></span>
4. <span data-ttu-id="3a756-115">在 [配置] 中，按一下 [內部]。</span><span class="sxs-lookup"><span data-stu-id="3a756-115">Under **Scheme**, click **Internal**.</span></span>
5. <span data-ttu-id="3a756-116">按一下**虛擬網路**，，然後選取 hello 想 toocreate hello 負載平衡器的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="3a756-116">Click **Virtual network**, and then select hello virtual network where you want toocreate hello load balancer.</span></span>

   > [!NOTE]
   > <span data-ttu-id="3a756-117">如果看不到您想要 toouse hello 虛擬網路，請檢查 hello**位置**您正在使用 hello 負載平衡器，並據此變更它。</span><span class="sxs-lookup"><span data-stu-id="3a756-117">If you do not see hello virtual network you want toouse, check hello **Location** you are using for hello load balancer, and change it accordingly.</span></span>

6. <span data-ttu-id="3a756-118">按一下**子網路**，然後選取您想要 toocreate hello 負載平衡器的 hello 子網路。</span><span class="sxs-lookup"><span data-stu-id="3a756-118">Click **Subnet**, and then select hello subnet where you want toocreate hello load balancer.</span></span>
7. <span data-ttu-id="3a756-119">在下**IP 位址指派**，按一下 **動態**或**靜態**，取決於您是否想 hello IP 位址的 hello 負載平衡器 toobe 固定 （靜態） 或不。</span><span class="sxs-lookup"><span data-stu-id="3a756-119">Under **IP address assignment**, click either **Dynamic** or **Static**, depending on whether you want hello IP address for hello load balancer toobe fixed (static) or not.</span></span>

   > [!NOTE]
   > <span data-ttu-id="3a756-120">如果您選取 toouse 靜態 IP 位址，您將擁有 tooprovide hello 負載平衡器位址。</span><span class="sxs-lookup"><span data-stu-id="3a756-120">If you select toouse a static IP address, you will have tooprovide an address for hello load balancer.</span></span>

8. <span data-ttu-id="3a756-121">在下**資源群組**請指定新的資源群組的 hello 名稱 hello 負載平衡器，或按一下**選取現有**選取現有的資源群組。</span><span class="sxs-lookup"><span data-stu-id="3a756-121">Under **Resource group** either specify hello name of a new resource group for hello load balancer, or click **select existing** and select an existing resource group.</span></span>
9. <span data-ttu-id="3a756-122">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="3a756-122">Click **Create**.</span></span>

## <a name="configure-load-balancing-rules"></a><span data-ttu-id="3a756-123">設定負載平衡規則</span><span class="sxs-lookup"><span data-stu-id="3a756-123">Configure load balancing rules</span></span>

<span data-ttu-id="3a756-124">之後 hello 負載平衡器建立、 瀏覽 toohello 負載平衡器資源 tooconfigure 它。</span><span class="sxs-lookup"><span data-stu-id="3a756-124">After hello load balancer creation, navigate toohello load balancer resource tooconfigure it.</span></span>
<span data-ttu-id="3a756-125">您需要 tooconfigure 第一次的後端位址集區和一個探查設定負載平衡規則之前。</span><span class="sxs-lookup"><span data-stu-id="3a756-125">You need tooconfigure first a back-end address pool and a probe before configuring a load balancing rule.</span></span>

### <a name="step-1-configure-a-back-end-pool"></a><span data-ttu-id="3a756-126">步驟 1：設定後端集區</span><span class="sxs-lookup"><span data-stu-id="3a756-126">Step 1: Configure a back-end pool</span></span>

1. <span data-ttu-id="3a756-127">在 hello Azure 入口網站，按一下 **瀏覽** > **負載平衡器**，然後按一下先前建立的 hello 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="3a756-127">In hello Azure portal, click **Browse** > **Load balancers**, and then click hello load balancer you created above.</span></span>
2. <span data-ttu-id="3a756-128">在 hello**設定**刀鋒視窗中，按一下 **後端集區**。</span><span class="sxs-lookup"><span data-stu-id="3a756-128">In hello **Settings** blade, click **Backend pools**.</span></span>
3. <span data-ttu-id="3a756-129">在 hello**後端位址集區**刀鋒視窗中，按一下 **新增**。</span><span class="sxs-lookup"><span data-stu-id="3a756-129">In hello **Backend address pools** blade, click **Add**.</span></span>
4. <span data-ttu-id="3a756-130">在 hello**新增後端集區**刀鋒視窗中，輸入**名稱**為 hello 後端集區，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="3a756-130">In hello **Add backend pool** blade, enter a **Name** for hello backend pool, and then click **OK**.</span></span>

### <a name="step-2-configure-a-probe"></a><span data-ttu-id="3a756-131">步驟 2：設定探查</span><span class="sxs-lookup"><span data-stu-id="3a756-131">Step 2: Configure a probe</span></span>

1. <span data-ttu-id="3a756-132">在 hello Azure 入口網站，按一下 **瀏覽** > **負載平衡器**，然後按一下先前建立的 hello 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="3a756-132">In hello Azure portal, click **Browse** > **Load balancers**, and then click hello load balancer you created above.</span></span>
2. <span data-ttu-id="3a756-133">在 hello**設定**刀鋒視窗中，按一下 **探查**。</span><span class="sxs-lookup"><span data-stu-id="3a756-133">In hello **Settings** blade, click **Probes**.</span></span>
3. <span data-ttu-id="3a756-134">在 hello**探查**刀鋒視窗中，按一下 **新增**。</span><span class="sxs-lookup"><span data-stu-id="3a756-134">In hello **Probes**  blade, click **Add**.</span></span>
4. <span data-ttu-id="3a756-135">在 hello**新增探查**刀鋒視窗中，輸入**名稱**hello 探查。</span><span class="sxs-lookup"><span data-stu-id="3a756-135">In hello **Add probe** blade, enter a **Name** for hello probe.</span></span>
5. <span data-ttu-id="3a756-136">在 [通訊協定] 下，選取 [HTTP]\(適用於網站) 或 [TCP] \(適用於其他 TCP 型應用程式)。</span><span class="sxs-lookup"><span data-stu-id="3a756-136">Under **Protocol**, select **HTTP** (for web sites) or **TCP** (for other TCP based applications).</span></span>
6. <span data-ttu-id="3a756-137">在下**連接埠**，存取 hello 探查時，指定 hello 連接埠 toouse。</span><span class="sxs-lookup"><span data-stu-id="3a756-137">Under **Port**, specify hello port toouse when accessing hello probe.</span></span>
7. <span data-ttu-id="3a756-138">在下**路徑**（適用於 HTTP 探查只），指定 hello 路徑 toouse 探查。</span><span class="sxs-lookup"><span data-stu-id="3a756-138">Under **Path** (for HTTP probes only), specify hello path toouse as a probe.</span></span>
8. <span data-ttu-id="3a756-139">在下**間隔**指定 tooprobe hello 應用程式的頻率。</span><span class="sxs-lookup"><span data-stu-id="3a756-139">Under **Interval** specify how frequently tooprobe hello application.</span></span>
9. <span data-ttu-id="3a756-140">在下**狀況不良閾值**，指定 hello 後端的虛擬機器標示為狀況不良之前失敗嘗試次數。</span><span class="sxs-lookup"><span data-stu-id="3a756-140">Under **Unhealthy threshold**, specify how many attempts should fail before hello backend virtual machine is marked as unhealthy.</span></span>
10. <span data-ttu-id="3a756-141">按一下**確定**toocreate 探查。</span><span class="sxs-lookup"><span data-stu-id="3a756-141">Click **OK** toocreate probe.</span></span>

### <a name="step-3-configure-load-balancing-rules"></a><span data-ttu-id="3a756-142">步驟 3：設定負載平衡規則</span><span class="sxs-lookup"><span data-stu-id="3a756-142">Step 3: Configure load balancing rules</span></span>

1. <span data-ttu-id="3a756-143">在 hello Azure 入口網站，按一下 **瀏覽** > **負載平衡器**，然後按一下先前建立的 hello 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="3a756-143">In hello Azure portal, click **Browse** > **Load balancers**, and then click hello load balancer you created above.</span></span>
2. <span data-ttu-id="3a756-144">在 hello**設定**刀鋒視窗中，按一下 **負載平衡規則**。</span><span class="sxs-lookup"><span data-stu-id="3a756-144">In hello **Settings** blade, click **Load balancing rules**.</span></span>
3. <span data-ttu-id="3a756-145">在 hello**負載平衡規則**刀鋒視窗中，按一下 **新增**。</span><span class="sxs-lookup"><span data-stu-id="3a756-145">In hello **Load balancing rules** blade, click **Add**.</span></span>
4. <span data-ttu-id="3a756-146">在 hello**新增負載平衡規則**刀鋒視窗中，輸入**名稱**hello 規則。</span><span class="sxs-lookup"><span data-stu-id="3a756-146">In hello **Add load balancing rule** blade, enter a **Name** for hello rule.</span></span>
5. <span data-ttu-id="3a756-147">在 [通訊協定] 下，選取 [HTTP]\(適用於網站) 或 [TCP] \(適用於其他 TCP 型應用程式)。</span><span class="sxs-lookup"><span data-stu-id="3a756-147">Under **Protocol**, select **HTTP** (for web sites) or **TCP** (for other TCP based applications).</span></span>
6. <span data-ttu-id="3a756-148">在下**連接埠**，指定 hello 連接埠的用戶端連接 tooin hello 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="3a756-148">Under **Port**, specify hello port clients connect tooin hello load balancer.</span></span>
7. <span data-ttu-id="3a756-149">在下**後端連接埠**，指定 hello hello 後端集區中使用的連接埠 toobe (通常 hello 負載平衡器通訊埠和 hello 後端連接埠是 hello 相同)。</span><span class="sxs-lookup"><span data-stu-id="3a756-149">Under **Backend port**, specify hello port toobe used in hello backend pool (usually, hello load balancer port and hello backend port are hello same).</span></span>
8. <span data-ttu-id="3a756-150">在下**後端集區**，選取 hello 後端集區，您在上面建立。</span><span class="sxs-lookup"><span data-stu-id="3a756-150">Under **Backend pool**, select hello backend pool you created above.</span></span>
9. <span data-ttu-id="3a756-151">在下**工作階段持續性**，選取您想要的工作階段 toopersist 的方式。</span><span class="sxs-lookup"><span data-stu-id="3a756-151">Under **Session persistence**, select how you want sessions toopersist.</span></span>
10. <span data-ttu-id="3a756-152">在下**閒置逾時 （分鐘）**，指定 hello 閒置逾時。</span><span class="sxs-lookup"><span data-stu-id="3a756-152">Under **Idle timeout (minutes)**, specify hello idle timeout.</span></span>
11. <span data-ttu-id="3a756-153">在 [浮動 IP (伺服器直接回傳)] 下，按一下 [停用] 或 [啟用]。</span><span class="sxs-lookup"><span data-stu-id="3a756-153">Under **Floating IP (direct server return)**, click **Disabled** or **Enabled**.</span></span>
12. <span data-ttu-id="3a756-154">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="3a756-154">Click **OK**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3a756-155">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3a756-155">Next steps</span></span>

[<span data-ttu-id="3a756-156">設定負載平衡器分配模式</span><span class="sxs-lookup"><span data-stu-id="3a756-156">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="3a756-157">設定負載平衡器的閒置 TCP 逾時設定</span><span class="sxs-lookup"><span data-stu-id="3a756-157">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

