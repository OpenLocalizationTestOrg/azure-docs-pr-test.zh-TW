---
title: "如何 tooconfigure ExpressRoute 電路的路由 （對等互連）： 資源管理員： Azure |Microsoft 文件"
description: "這篇文章會引導您完成建立及佈建 hello 私人、 公用及 Microsoft 對等互連的 ExpressRoute 電路的 hello 步驟。 本文也會顯示 toocheck hello 狀態、 更新或刪除您的電路的互連的方式。"
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 8c2a7ed2-ae5c-4e49-81f6-77cf9f2b2ac9
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: cherylmc
ms.openlocfilehash: a8ca25f488dde728cb3b06cd2c91873f3069feaf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit"></a><span data-ttu-id="3a8b6-104">建立和修改 ExpressRoute 線路的對等互連</span><span class="sxs-lookup"><span data-stu-id="3a8b6-104">Create and modify peering for an ExpressRoute circuit</span></span>

<span data-ttu-id="3a8b6-105">這篇文章可協助您建立和管理 ExpressRoute 電路 hello Resource Manager 部署模型使用 hello Azure 入口網站中的路由組態。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-105">This article helps you create and manage routing configuration for an ExpressRoute circuit in hello Resource Manager deployment model using hello Azure portal.</span></span> <span data-ttu-id="3a8b6-106">您也可以檢查 hello 狀態、 更新或刪除，並取消佈建 ExpressRoute 循環的對等互連。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-106">You can also check hello status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span> <span data-ttu-id="3a8b6-107">如果您想 toouse 不同方法 toowork 與您的循環，請從下列清單中的 hello 選取一個發行項：</span><span class="sxs-lookup"><span data-stu-id="3a8b6-107">If you want toouse a different method toowork with your circuit, select an article from hello following list:</span></span>


## <a name="configuration-prerequisites"></a><span data-ttu-id="3a8b6-108">組態必要條件</span><span class="sxs-lookup"><span data-stu-id="3a8b6-108">Configuration prerequisites</span></span>

* <span data-ttu-id="3a8b6-109">請確定您已經檢閱 hello[必要條件](expressroute-prerequisites.md)頁面 hello[路由需求](expressroute-routing.md)頁面和 hello[工作流程](expressroute-workflows.md)頁面開始設定之前。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-109">Make sure that you have reviewed hello [prerequisites](expressroute-prerequisites.md) page, hello [routing requirements](expressroute-routing.md) page, and hello [workflows](expressroute-workflows.md) page before you begin configuration.</span></span>
* <span data-ttu-id="3a8b6-110">您必須擁有作用中的 ExpressRoute 線路。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-110">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="3a8b6-111">請依照下列指示 hello 太[建立 ExpressRoute 電路](expressroute-howto-circuit-portal-resource-manager.md)和有 hello 電路啟用您的連線提供者，才能繼續。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-111">Follow hello instructions too[Create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="3a8b6-112">hello ExpressRoute 電路必須位於您 toobe 無法 toorun hello cmdlet hello 下一節中的佈建並啟用狀態。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-112">hello ExpressRoute circuit must be in a provisioned and enabled state for you toobe able toorun hello cmdlets in hello next sections.</span></span>
* <span data-ttu-id="3a8b6-113">如果您計劃 toouse 共用金鑰/MD5 雜湊，是確定 toouse 這兩端 hello 通道和 limit hello 數目的字元 tooa 最大值為 25。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-113">If you plan toouse a shared key/MD5 hash, be sure toouse this on both sides of hello tunnel and limit hello number of characters tooa maximum of 25.</span></span>

<span data-ttu-id="3a8b6-114">這些說明僅適用於 toocircuits 建立與服務供應項目層級 2 連線服務的提供者。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-114">These instructions only apply toocircuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="3a8b6-115">如果您使用的服務提供者提供受管理的第 3 層服務 (通常是 IPVPN，如 MPLS)，連線提供者會為您設定和管理路由。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-115">If you are using a service provider that offers managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider configures and manages routing for you.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="3a8b6-116">我們目前不會進行通告透過 hello 服務管理入口網站的服務提供者所設定的對等互連。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-116">We currently do not advertise peerings configured by service providers through hello service management portal.</span></span> <span data-ttu-id="3a8b6-117">我們正努力在近期推出這項功能。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-117">We are working on enabling this capability soon.</span></span> <span data-ttu-id="3a8b6-118">設定 BGP 對等互連之前，請洽詢您的服務提供者。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-118">Check with your service provider before configuring BGP peerings.</span></span>
> 
> 

<span data-ttu-id="3a8b6-119">您可以為 ExpressRoute 線路設定一個、兩個或全部三個對等 (Azure 私用、Azure 公用和 Microsoft)。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-119">You can configure one, two, or all three peerings (Azure private, Azure public and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="3a8b6-120">您可以依自己選擇的任何順序設定對等。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-120">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="3a8b6-121">不過，您必須確定您完成每個對等互連一次一個的 hello 設定。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-121">However, you must make sure that you complete hello configuration of each peering one at a time.</span></span>

## <a name="azure-private-peering"></a><span data-ttu-id="3a8b6-122">Azure 私用對等</span><span class="sxs-lookup"><span data-stu-id="3a8b6-122">Azure private peering</span></span>

<span data-ttu-id="3a8b6-123">本節可協助您建立、 取得、 更新和刪除 hello Azure ExpressRoute 循環的私用對等設定。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-123">This section helps you create, get, update, and delete hello Azure private peering configuration for an ExpressRoute circuit.</span></span>

### <a name="toocreate-azure-private-peering"></a><span data-ttu-id="3a8b6-124">toocreate Azure 私人互連</span><span class="sxs-lookup"><span data-stu-id="3a8b6-124">toocreate Azure private peering</span></span>

1. <span data-ttu-id="3a8b6-125">設定 hello ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-125">Configure hello ExpressRoute circuit.</span></span> <span data-ttu-id="3a8b6-126">確保 hello 循環完全佈建的 hello 連線服務提供者才能繼續。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-126">Ensure that hello circuit is fully provisioned by hello connectivity provider before continuing.</span></span>

  ![list](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. <span data-ttu-id="3a8b6-128">設定 Azure 私用對等互連 hello 循環。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-128">Configure Azure private peering for hello circuit.</span></span> <span data-ttu-id="3a8b6-129">請確定您具備下列項目，再繼續進行下一個步驟的 hello hello:</span><span class="sxs-lookup"><span data-stu-id="3a8b6-129">Make sure that you have hello following items before you proceed with hello next steps:</span></span>

  * <span data-ttu-id="3a8b6-130">/ 30 子網路 hello 主要連結。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-130">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="3a8b6-131">hello 子網路不能保留的虛擬網路的任何位址空間的一部分。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-131">hello subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="3a8b6-132">/ 30 hello 次要連結的子網路。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-132">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="3a8b6-133">hello 子網路不能保留的虛擬網路的任何位址空間的一部分。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-133">hello subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="3a8b6-134">有效的 VLAN ID tooestablish 此對等。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-134">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="3a8b6-135">請確認沒有其他對等互連中 hello 循環使用 hello 相同 VLAN id。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-135">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="3a8b6-136">對等的 AS 編號。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-136">AS number for peering.</span></span> <span data-ttu-id="3a8b6-137">您可以使用 2 位元組和 4 位元組 AS 編號。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-137">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="3a8b6-138">您可以將私用 AS 編號用於此對等。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-138">You can use a private AS number for this peering.</span></span> <span data-ttu-id="3a8b6-139">請確定您不是使用 65515。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-139">Ensure that you are not using 65515.</span></span>
  * <span data-ttu-id="3a8b6-140">**選用-**如果您選擇其中一個 toouse 的 MD5 雜湊。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-140">**Optional -** An MD5 hash if you choose toouse one.</span></span>
3. <span data-ttu-id="3a8b6-141">選取 hello Azure 私用的對等資料列，hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="3a8b6-141">Select hello Azure Private peering row, as shown in hello following example:</span></span>

  ![私用](./media/expressroute-howto-routing-portal-resource-manager/rprivate1.png)
4. <span data-ttu-id="3a8b6-143">設定私用對等。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-143">Configure private peering.</span></span> <span data-ttu-id="3a8b6-144">hello 下列影像顯示組態範例：</span><span class="sxs-lookup"><span data-stu-id="3a8b6-144">hello following image shows a configuration example:</span></span>

  ![設定私用對等互連](./media/expressroute-howto-routing-portal-resource-manager/rprivate2.png)
5. <span data-ttu-id="3a8b6-146">一旦您已指定所有參數，請儲存 hello 組態。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-146">Save hello configuration once you have specified all parameters.</span></span> <span data-ttu-id="3a8b6-147">已成功接受 hello 組態之後，您會看到類似下列範例的 toohello:</span><span class="sxs-lookup"><span data-stu-id="3a8b6-147">After hello configuration has been accepted successfully, you see something similar toohello following example:</span></span>

  ![儲存私用對等互連](./media/expressroute-howto-routing-portal-resource-manager/rprivate3.png)

### <a name="tooview-azure-private-peering-details"></a><span data-ttu-id="3a8b6-149">tooview Azure 私用對等互連的詳細資料</span><span class="sxs-lookup"><span data-stu-id="3a8b6-149">tooview Azure private peering details</span></span>

<span data-ttu-id="3a8b6-150">您可以檢視選取對等互連 hello Azure 私人互連的 hello 的屬性。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-150">You can view hello properties of Azure private peering by selecting hello peering.</span></span>

![檢視私用對等互連](./media/expressroute-howto-routing-portal-resource-manager/rprivate3.png)

### <a name="tooupdate-azure-private-peering-configuration"></a><span data-ttu-id="3a8b6-152">tooupdate Azure 私用對等組態</span><span class="sxs-lookup"><span data-stu-id="3a8b6-152">tooupdate Azure private peering configuration</span></span>

<span data-ttu-id="3a8b6-153">您可以選取 hello 資料列的對等互連，並修改 hello 對等屬性。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-153">You can select hello row for peering and modify hello peering properties.</span></span>

![更新私用對等互連](./media/expressroute-howto-routing-portal-resource-manager/rprivate2.png)

### <a name="toodelete-azure-private-peering"></a><span data-ttu-id="3a8b6-155">toodelete Azure 私人互連</span><span class="sxs-lookup"><span data-stu-id="3a8b6-155">toodelete Azure private peering</span></span>

<span data-ttu-id="3a8b6-156">Hello 下列影像所示，您可以藉由選取 hello 刪除圖示，移除您對等的設定：</span><span class="sxs-lookup"><span data-stu-id="3a8b6-156">You can remove your peering configuration by selecting hello delete icon, as shown in hello following image:</span></span>

![刪除私用對等互連](./media/expressroute-howto-routing-portal-resource-manager/rprivate4.png)

## <a name="azure-public-peering"></a><span data-ttu-id="3a8b6-158">Azure 公用對等</span><span class="sxs-lookup"><span data-stu-id="3a8b6-158">Azure public peering</span></span>

<span data-ttu-id="3a8b6-159">本節可協助您建立、 取得、 更新和刪除 hello Azure ExpressRoute 循環的公用對等設定。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-159">This section helps you create, get, update, and delete hello Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="toocreate-azure-public-peering"></a><span data-ttu-id="3a8b6-160">toocreate Azure 公用對等互連</span><span class="sxs-lookup"><span data-stu-id="3a8b6-160">toocreate Azure public peering</span></span>

1. <span data-ttu-id="3a8b6-161">設定 ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-161">Configure ExpressRoute circuit.</span></span> <span data-ttu-id="3a8b6-162">確保 hello 循環完全佈建的 hello 連線服務提供者再進一步繼續。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-162">Ensure that hello circuit is fully provisioned by hello connectivity provider before continuing further.</span></span>

  ![列出公用對等互連](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. <span data-ttu-id="3a8b6-164">設定 Azure 公用對等互連 hello 循環。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-164">Configure Azure public peering for hello circuit.</span></span> <span data-ttu-id="3a8b6-165">請確定您具備下列項目，再繼續進行下一個步驟的 hello hello:</span><span class="sxs-lookup"><span data-stu-id="3a8b6-165">Make sure that you have hello following items before you proceed with hello next steps:</span></span>

  * <span data-ttu-id="3a8b6-166">/ 30 子網路 hello 主要連結。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-166">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="3a8b6-167">這必須是有效的公用 IPv4 首碼。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-167">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="3a8b6-168">/ 30 hello 次要連結的子網路。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-168">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="3a8b6-169">這必須是有效的公用 IPv4 首碼。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-169">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="3a8b6-170">有效的 VLAN ID tooestablish 此對等。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-170">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="3a8b6-171">請確認沒有其他對等互連中 hello 循環使用 hello 相同 VLAN id。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-171">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="3a8b6-172">對等的 AS 編號。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-172">AS number for peering.</span></span> <span data-ttu-id="3a8b6-173">您可以使用 2 位元組和 4 位元組 AS 編號。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-173">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="3a8b6-174">**選用-**如果您選擇其中一個 toouse 的 MD5 雜湊。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-174">**Optional -** An MD5 hash if you choose toouse one.</span></span>
3. <span data-ttu-id="3a8b6-175">請選取 hello Azure 公用對等資料列，hello 下列影像所示：</span><span class="sxs-lookup"><span data-stu-id="3a8b6-175">Select hello Azure public peering row, as shown in hello following image:</span></span>

  ![選取公用對等互連列](./media/expressroute-howto-routing-portal-resource-manager/rpublic1.png)
4. <span data-ttu-id="3a8b6-177">設定公用對等。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-177">Configure public peering.</span></span> <span data-ttu-id="3a8b6-178">hello 下列影像顯示組態範例：</span><span class="sxs-lookup"><span data-stu-id="3a8b6-178">hello following image shows a configuration example:</span></span>

  ![設定公用對等互連](./media/expressroute-howto-routing-portal-resource-manager/rpublic2.png)
5. <span data-ttu-id="3a8b6-180">一旦您已指定所有參數，請儲存 hello 組態。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-180">Save hello configuration once you have specified all parameters.</span></span> <span data-ttu-id="3a8b6-181">已成功接受 hello 組態之後，您會看到類似下列範例的 toohello:</span><span class="sxs-lookup"><span data-stu-id="3a8b6-181">After hello configuration has been accepted successfully, you see something similar toohello following example:</span></span>

  ![儲存公用對等互連設定](./media/expressroute-howto-routing-portal-resource-manager/rpublic3.png)

### <a name="tooview-azure-public-peering-details"></a><span data-ttu-id="3a8b6-183">tooview Azure 公用對等互連的詳細資料</span><span class="sxs-lookup"><span data-stu-id="3a8b6-183">tooview Azure public peering details</span></span>

<span data-ttu-id="3a8b6-184">您可以檢視選取對等互連 hello Azure 公用對等的 hello 的屬性。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-184">You can view hello properties of Azure public peering by selecting hello peering.</span></span>

![檢視公用對等互連屬性](./media/expressroute-howto-routing-portal-resource-manager/rpublic3.png)

### <a name="tooupdate-azure-public-peering-configuration"></a><span data-ttu-id="3a8b6-186">tooupdate Azure 公用對等組態</span><span class="sxs-lookup"><span data-stu-id="3a8b6-186">tooupdate Azure public peering configuration</span></span>

<span data-ttu-id="3a8b6-187">您可以選取 hello 資料列的對等互連，並修改 hello 對等屬性。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-187">You can select hello row for peering and modify hello peering properties.</span></span>

![選取公用對等互連列](./media/expressroute-howto-routing-portal-resource-manager/rpublic2.png)

### <a name="toodelete-azure-public-peering"></a><span data-ttu-id="3a8b6-189">toodelete Azure 公用對等互連</span><span class="sxs-lookup"><span data-stu-id="3a8b6-189">toodelete Azure public peering</span></span>

<span data-ttu-id="3a8b6-190">Hello 下列範例所示，您可以藉由選取 hello 刪除圖示，移除您對等的設定：</span><span class="sxs-lookup"><span data-stu-id="3a8b6-190">You can remove your peering configuration by selecting hello delete icon, as shown in hello following example:</span></span>

![刪除公用對等互連](./media/expressroute-howto-routing-portal-resource-manager/rpublic4.png)

## <a name="microsoft-peering"></a><span data-ttu-id="3a8b6-192">Microsoft 對等互連</span><span class="sxs-lookup"><span data-stu-id="3a8b6-192">Microsoft peering</span></span>

<span data-ttu-id="3a8b6-193">本節可協助您建立、 取得、 更新和刪除 ExpressRoute 循環的 hello Microsoft 對等設定。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-193">This section helps you create, get, update, and delete hello Microsoft peering configuration for an ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3a8b6-194">Microsoft 對等互連的 ExpressRoute 電路已設定先前 tooAugust 1，2017年必須透過 hello Microsoft 對等互連，公告的所有服務首碼，即使未定義路由篩選器。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-194">Microsoft peering of ExpressRoute circuits that were configured prior tooAugust 1, 2017 will have all service prefixes advertised through hello Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="3a8b6-195">Microsoft 對等互連的當天或之後 2017 年 8 月 1，已設定的 ExpressRoute 電路並不會有任何前置詞通告的路由篩選器連接直到 toohello 循環。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-195">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached toohello circuit.</span></span> <span data-ttu-id="3a8b6-196">如需詳細資訊，請參閱[設定 Microsoft 對等互連的路由篩選](how-to-routefilter-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-196">For more information, see [Configure a route filter for Microsoft peering](how-to-routefilter-powershell.md).</span></span>
> 
> 

### <a name="toocreate-microsoft-peering"></a><span data-ttu-id="3a8b6-197">toocreate Microsoft 對等互連</span><span class="sxs-lookup"><span data-stu-id="3a8b6-197">toocreate Microsoft peering</span></span>

1. <span data-ttu-id="3a8b6-198">設定 ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-198">Configure ExpressRoute circuit.</span></span> <span data-ttu-id="3a8b6-199">確保 hello 循環完全佈建的 hello 連線服務提供者再進一步繼續。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-199">Ensure that hello circuit is fully provisioned by hello connectivity provider before continuing further.</span></span>

  ![列出 Microsoft 對等互連](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. <span data-ttu-id="3a8b6-201">設定 Microsoft 對等互連 hello 循環。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-201">Configure Microsoft peering for hello circuit.</span></span> <span data-ttu-id="3a8b6-202">請確定您擁有 hello 下列資訊才能繼續。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-202">Make sure that you have hello following information before you proceed.</span></span>

  * <span data-ttu-id="3a8b6-203">/ 30 子網路 hello 主要連結。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-203">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="3a8b6-204">這必須是您所擁有且註冊在 RIR / IRR 中的有效公用 IPv4 首碼。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-204">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="3a8b6-205">/ 30 hello 次要連結的子網路。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-205">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="3a8b6-206">這必須是您所擁有且註冊在 RIR / IRR 中的有效公用 IPv4 首碼。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-206">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="3a8b6-207">有效的 VLAN ID tooestablish 此對等。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-207">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="3a8b6-208">請確認沒有其他對等互連中 hello 循環使用 hello 相同 VLAN id。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-208">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="3a8b6-209">對等的 AS 編號。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-209">AS number for peering.</span></span> <span data-ttu-id="3a8b6-210">您可以使用 2 位元組和 4 位元組 AS 編號。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-210">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="3a8b6-211">通告前置詞： 您必須提供清單的所有前置詞您計劃 tooadvertise 透過 hello BGP 工作階段。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-211">Advertised prefixes: You must provide a list of all prefixes you plan tooadvertise over hello BGP session.</span></span> <span data-ttu-id="3a8b6-212">只接受公用 IP 位址首碼。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-212">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="3a8b6-213">如果您計劃 toosend 一組前置詞，您可以傳送的逗號分隔清單。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-213">If you plan toosend a set of prefixes, you can send a comma-separated list.</span></span> <span data-ttu-id="3a8b6-214">這些前置詞必須是已註冊的 tooyou 在 RIR / IRR。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-214">These prefixes must be registered tooyou in an RIR / IRR.</span></span>
  * <span data-ttu-id="3a8b6-215">**選用-**客戶 ASN： 如果您不是數字的已註冊的 toohello 對等互連的廣告前置詞，您可以指定 hello 為其所註冊的數字 toowhich。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-215">**Optional -** Customer ASN: If you are advertising prefixes that are not registered toohello peering AS number, you can specify hello AS number toowhich they are registered.</span></span>
  * <span data-ttu-id="3a8b6-216">路由登錄名稱： 您可以指定 hello RIR / IRR 哪些 hello 做為數字，但前置詞會註冊。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-216">Routing Registry Name: You can specify hello RIR / IRR against which hello AS number and prefixes are registered.</span></span>
  * <span data-ttu-id="3a8b6-217">**選用-**如果您選擇其中一個 toouse 的 MD5 雜湊。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-217">**Optional -** An MD5 hash if you choose toouse one.</span></span>
3. <span data-ttu-id="3a8b6-218">您可以選取 hello 對等互連想 tooconfigure，hello 下列所示範例。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-218">You can select hello peering you wish tooconfigure, as shown in hello following example.</span></span> <span data-ttu-id="3a8b6-219">選取 hello Microsoft 對等資料列。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-219">Select hello Microsoft peering row.</span></span>

  ![選取 Microsoft 對等互連列](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft1.png)
4. <span data-ttu-id="3a8b6-221">設定 Microsoft 對等。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-221">Configure Microsoft peering.</span></span> <span data-ttu-id="3a8b6-222">hello 下列影像顯示組態範例：</span><span class="sxs-lookup"><span data-stu-id="3a8b6-222">hello following image shows a configuration example:</span></span>

  ![設定 Microsoft 對等互連](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft2.png)
5. <span data-ttu-id="3a8b6-224">一旦您已指定所有參數，請儲存 hello 組態。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-224">Save hello configuration once you have specified all parameters.</span></span>

  <span data-ttu-id="3a8b6-225">如果您的電路取得 tooa '所需的驗證' 狀態 （如 hello 映像中所示），您必須開啟支援票證 tooshow hello 前置詞 tooour 支援小組擁有權證明。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-225">If your circuit gets tooa 'Validation needed' state (as shown in hello image), you must open a support ticket tooshow proof of ownership of hello prefixes tooour support team.</span></span>

  ![儲存 Microsoft 對等互連設定](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft5.png)

  <span data-ttu-id="3a8b6-227">您可以直接從 hello 入口網站中，開啟支援票證，hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="3a8b6-227">You can open a support ticket directly from hello portal, as shown in hello following example:</span></span>

  ![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft6.png)


1. <span data-ttu-id="3a8b6-228">已成功接受 hello 組態之後，您會看到類似下列映像的 toohello:</span><span class="sxs-lookup"><span data-stu-id="3a8b6-228">After hello configuration has been accepted successfully, you see something similar toohello following image:</span></span>

  ![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft7.png)

### <a name="tooview-microsoft-peering-details"></a><span data-ttu-id="3a8b6-229">tooview Microsoft 對等詳細資料</span><span class="sxs-lookup"><span data-stu-id="3a8b6-229">tooview Microsoft peering details</span></span>

<span data-ttu-id="3a8b6-230">您可以檢視選取對等互連 hello Azure 公用對等的 hello 的屬性。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-230">You can view hello properties of Azure public peering by selecting hello peering.</span></span>

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft3.png)

### <a name="tooupdate-microsoft-peering-configuration"></a><span data-ttu-id="3a8b6-231">tooupdate Microsoft 對等組態</span><span class="sxs-lookup"><span data-stu-id="3a8b6-231">tooupdate Microsoft peering configuration</span></span>

<span data-ttu-id="3a8b6-232">您可以選取 hello 資料列的對等互連，並修改 hello 對等屬性。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-232">You can select hello row for peering and modify hello peering properties.</span></span>

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft7.png)

### <a name="toodelete-microsoft-peering"></a><span data-ttu-id="3a8b6-233">toodelete Microsoft 對等互連</span><span class="sxs-lookup"><span data-stu-id="3a8b6-233">toodelete Microsoft peering</span></span>

<span data-ttu-id="3a8b6-234">Hello 下列影像所示，您可以藉由選取 hello 刪除圖示，移除您對等的設定：</span><span class="sxs-lookup"><span data-stu-id="3a8b6-234">You can remove your peering configuration by selecting hello delete icon, as shown in hello following image:</span></span>

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft4.png)

## <a name="next-steps"></a><span data-ttu-id="3a8b6-235">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3a8b6-235">Next steps</span></span>

<span data-ttu-id="3a8b6-236">下一步，[連結 VNet tooan ExpressRoute 電路](expressroute-howto-linkvnet-portal-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="3a8b6-236">Next step, [Link a VNet tooan ExpressRoute circuit](expressroute-howto-linkvnet-portal-resource-manager.md)</span></span>
* <span data-ttu-id="3a8b6-237">如需 ExpressRoute 工作流程的詳細資訊，請參閱 [ExpressRoute 工作流程](expressroute-workflows.md)。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-237">For more information about ExpressRoute workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="3a8b6-238">如需線路對等的詳細資訊，請參閱 [ExpressRoute 線路和路由網域](expressroute-circuit-peerings.md)。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-238">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>
* <span data-ttu-id="3a8b6-239">如需使用虛擬網路的詳細資訊，請參閱 [虛擬網路概觀](../virtual-network/virtual-networks-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="3a8b6-239">For more information about working with virtual networks, see [Virtual network overview](../virtual-network/virtual-networks-overview.md).</span></span>
