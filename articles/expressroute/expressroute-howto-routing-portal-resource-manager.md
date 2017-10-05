---
title: "如何設定 ExpressRoute 線路的路由 (對等互連)：Resource Manager：Azure | Microsoft Docs"
description: "本文將逐步引導您為 ExpressRoute 線路建立和佈建私用、公用及 Microsoft 對等。 本文也示範如何檢查狀態、更新或刪除線路的對等。"
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
ms.openlocfilehash: 55ccadfea55b8098ee58dcaef942f6ba54093665
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit"></a><span data-ttu-id="f7d8b-104">建立和修改 ExpressRoute 線路的對等互連</span><span class="sxs-lookup"><span data-stu-id="f7d8b-104">Create and modify peering for an ExpressRoute circuit</span></span>

<span data-ttu-id="f7d8b-105">本文將協助您使用 Azure 入口網站，在 Resource Manager 部署模型中建立和管理 ExpressRoute 線路的路由設定。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-105">This article helps you create and manage routing configuration for an ExpressRoute circuit in the Resource Manager deployment model using the Azure portal.</span></span> <span data-ttu-id="f7d8b-106">您還可以檢查狀態、更新，或是刪除與取消佈建 ExpressRoute 線路的對等互連。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-106">You can also check the status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span> <span data-ttu-id="f7d8b-107">如果您想要對線路使用不同的方法，可選取下列清單中的文章：</span><span class="sxs-lookup"><span data-stu-id="f7d8b-107">If you want to use a different method to work with your circuit, select an article from the following list:</span></span>


## <a name="configuration-prerequisites"></a><span data-ttu-id="f7d8b-108">組態必要條件</span><span class="sxs-lookup"><span data-stu-id="f7d8b-108">Configuration prerequisites</span></span>

* <span data-ttu-id="f7d8b-109">開始設定之前，請確定您已經檢閱過[必要條件](expressroute-prerequisites.md)頁面、[路由需求](expressroute-routing.md)頁面和[工作流程](expressroute-workflows.md)頁面。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-109">Make sure that you have reviewed the [prerequisites](expressroute-prerequisites.md) page, the [routing requirements](expressroute-routing.md) page, and the [workflows](expressroute-workflows.md) page before you begin configuration.</span></span>
* <span data-ttu-id="f7d8b-110">您必須擁有作用中的 ExpressRoute 線路。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-110">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="f7d8b-111">繼續之前，請遵循指示來 [建立 ExpressRoute 線路](expressroute-howto-circuit-portal-resource-manager.md) ，並由您的連線提供者來啟用該線路。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-111">Follow the instructions to [Create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have the circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="f7d8b-112">ExpressRoute 線路必須處於已佈建和已啟用狀態，您才能執行下一節中的 Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-112">The ExpressRoute circuit must be in a provisioned and enabled state for you to be able to run the cmdlets in the next sections.</span></span>
* <span data-ttu-id="f7d8b-113">如果您打算使用共用金鑰/MD5 雜湊，請務必將它使用於通道的兩端，並將字元數目限制為最多 25 個。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-113">If you plan to use a shared key/MD5 hash, be sure to use this on both sides of the tunnel and limit the number of characters to a maximum of 25.</span></span>

<span data-ttu-id="f7d8b-114">這些指示只適用於由提供第 2 層連線服務的服務提供者所建立的線路。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-114">These instructions only apply to circuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="f7d8b-115">如果您使用的服務提供者提供受管理的第 3 層服務 (通常是 IPVPN，如 MPLS)，連線提供者會為您設定和管理路由。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-115">If you are using a service provider that offers managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider configures and manages routing for you.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="f7d8b-116">我們目前不會透過服務管理入口網站來公告服務提供者所設定的對等。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-116">We currently do not advertise peerings configured by service providers through the service management portal.</span></span> <span data-ttu-id="f7d8b-117">我們正努力在近期推出這項功能。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-117">We are working on enabling this capability soon.</span></span> <span data-ttu-id="f7d8b-118">設定 BGP 對等互連之前，請洽詢您的服務提供者。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-118">Check with your service provider before configuring BGP peerings.</span></span>
> 
> 

<span data-ttu-id="f7d8b-119">您可以為 ExpressRoute 線路設定一個、兩個或全部三個對等 (Azure 私用、Azure 公用和 Microsoft)。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-119">You can configure one, two, or all three peerings (Azure private, Azure public and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="f7d8b-120">您可以依自己選擇的任何順序設定對等。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-120">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="f7d8b-121">不過，您必須確定一次只完成一個對等的設定。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-121">However, you must make sure that you complete the configuration of each peering one at a time.</span></span>

## <a name="azure-private-peering"></a><span data-ttu-id="f7d8b-122">Azure 私用對等</span><span class="sxs-lookup"><span data-stu-id="f7d8b-122">Azure private peering</span></span>

<span data-ttu-id="f7d8b-123">本節將協助您為 ExpressRoute 線路建立、取得、更新和刪除 Azure 私用對等互連設定。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-123">This section helps you create, get, update, and delete the Azure private peering configuration for an ExpressRoute circuit.</span></span>

### <a name="to-create-azure-private-peering"></a><span data-ttu-id="f7d8b-124">建立 Azure 私用對等</span><span class="sxs-lookup"><span data-stu-id="f7d8b-124">To create Azure private peering</span></span>

1. <span data-ttu-id="f7d8b-125">設定 ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-125">Configure the ExpressRoute circuit.</span></span> <span data-ttu-id="f7d8b-126">先確定連線提供者已完整佈建電路，再繼續作業。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-126">Ensure that the circuit is fully provisioned by the connectivity provider before continuing.</span></span>

  ![list](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. <span data-ttu-id="f7d8b-128">設定線路的 Azure 私用對等。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-128">Configure Azure private peering for the circuit.</span></span> <span data-ttu-id="f7d8b-129">繼續執行接下來的步驟之前，請確定您有下列項目：</span><span class="sxs-lookup"><span data-stu-id="f7d8b-129">Make sure that you have the following items before you proceed with the next steps:</span></span>

  * <span data-ttu-id="f7d8b-130">主要連結的 /30 子網路。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-130">A /30 subnet for the primary link.</span></span> <span data-ttu-id="f7d8b-131">子網路不能在保留給虛擬網路的任何位址空間中。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-131">The subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="f7d8b-132">次要連結的 /30 子網路。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-132">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="f7d8b-133">子網路不能在保留給虛擬網路的任何位址空間中。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-133">The subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="f7d8b-134">供建立此對等的有效 VLAN ID。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-134">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="f7d8b-135">請確定線路有沒有其他對等使用相同的 VLAN ID。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-135">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="f7d8b-136">對等的 AS 編號。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-136">AS number for peering.</span></span> <span data-ttu-id="f7d8b-137">您可以使用 2 位元組和 4 位元組 AS 編號。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-137">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="f7d8b-138">您可以將私用 AS 編號用於此對等。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-138">You can use a private AS number for this peering.</span></span> <span data-ttu-id="f7d8b-139">請確定您不是使用 65515。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-139">Ensure that you are not using 65515.</span></span>
  * <span data-ttu-id="f7d8b-140">**選用：**MD5 雜湊 (如果選擇使用)。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-140">**Optional -** An MD5 hash if you choose to use one.</span></span>
3. <span data-ttu-id="f7d8b-141">如下列範例所示，選取 Azure 私用對等互連列：</span><span class="sxs-lookup"><span data-stu-id="f7d8b-141">Select the Azure Private peering row, as shown in the following example:</span></span>

  ![私用](./media/expressroute-howto-routing-portal-resource-manager/rprivate1.png)
4. <span data-ttu-id="f7d8b-143">設定私用對等。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-143">Configure private peering.</span></span> <span data-ttu-id="f7d8b-144">下圖顯示設定範例：</span><span class="sxs-lookup"><span data-stu-id="f7d8b-144">The following image shows a configuration example:</span></span>

  ![設定私用對等互連](./media/expressroute-howto-routing-portal-resource-manager/rprivate2.png)
5. <span data-ttu-id="f7d8b-146">指定所有參數後，請儲存組態。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-146">Save the configuration once you have specified all parameters.</span></span> <span data-ttu-id="f7d8b-147">成功接受設定後，會出現類似下列範例的畫面：</span><span class="sxs-lookup"><span data-stu-id="f7d8b-147">After the configuration has been accepted successfully, you see something similar to the following example:</span></span>

  ![儲存私用對等互連](./media/expressroute-howto-routing-portal-resource-manager/rprivate3.png)

### <a name="to-view-azure-private-peering-details"></a><span data-ttu-id="f7d8b-149">檢視 Azure 私用對等詳細資訊</span><span class="sxs-lookup"><span data-stu-id="f7d8b-149">To view Azure private peering details</span></span>

<span data-ttu-id="f7d8b-150">選取 Azure 私用對等，即可檢視該對等的屬性。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-150">You can view the properties of Azure private peering by selecting the peering.</span></span>

![檢視私用對等互連](./media/expressroute-howto-routing-portal-resource-manager/rprivate3.png)

### <a name="to-update-azure-private-peering-configuration"></a><span data-ttu-id="f7d8b-152">更新 Azure 私用對等組態</span><span class="sxs-lookup"><span data-stu-id="f7d8b-152">To update Azure private peering configuration</span></span>

<span data-ttu-id="f7d8b-153">您可以選取對等的資料列並修改對等屬性。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-153">You can select the row for peering and modify the peering properties.</span></span>

![更新私用對等互連](./media/expressroute-howto-routing-portal-resource-manager/rprivate2.png)

### <a name="to-delete-azure-private-peering"></a><span data-ttu-id="f7d8b-155">刪除 Azure 私用對等</span><span class="sxs-lookup"><span data-stu-id="f7d8b-155">To delete Azure private peering</span></span>

<span data-ttu-id="f7d8b-156">如下圖所示，您可以選取刪除圖示來移除對等互連設定：</span><span class="sxs-lookup"><span data-stu-id="f7d8b-156">You can remove your peering configuration by selecting the delete icon, as shown in the following image:</span></span>

![刪除私用對等互連](./media/expressroute-howto-routing-portal-resource-manager/rprivate4.png)

## <a name="azure-public-peering"></a><span data-ttu-id="f7d8b-158">Azure 公用對等</span><span class="sxs-lookup"><span data-stu-id="f7d8b-158">Azure public peering</span></span>

<span data-ttu-id="f7d8b-159">本節將協助您為 ExpressRoute 線路建立、取得、更新和刪除 Azure 公用對等互連設定。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-159">This section helps you create, get, update, and delete the Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="to-create-azure-public-peering"></a><span data-ttu-id="f7d8b-160">建立 Azure 公用對等</span><span class="sxs-lookup"><span data-stu-id="f7d8b-160">To create Azure public peering</span></span>

1. <span data-ttu-id="f7d8b-161">設定 ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-161">Configure ExpressRoute circuit.</span></span> <span data-ttu-id="f7d8b-162">先確定連線提供者已完整佈建電路，再繼續作業。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-162">Ensure that the circuit is fully provisioned by the connectivity provider before continuing further.</span></span>

  ![列出公用對等互連](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. <span data-ttu-id="f7d8b-164">設定線路的 Azure 公用對等。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-164">Configure Azure public peering for the circuit.</span></span> <span data-ttu-id="f7d8b-165">繼續執行接下來的步驟之前，請確定您有下列項目：</span><span class="sxs-lookup"><span data-stu-id="f7d8b-165">Make sure that you have the following items before you proceed with the next steps:</span></span>

  * <span data-ttu-id="f7d8b-166">主要連結的 /30 子網路。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-166">A /30 subnet for the primary link.</span></span> <span data-ttu-id="f7d8b-167">這必須是有效的公用 IPv4 首碼。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-167">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="f7d8b-168">次要連結的 /30 子網路。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-168">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="f7d8b-169">這必須是有效的公用 IPv4 首碼。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-169">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="f7d8b-170">供建立此對等的有效 VLAN ID。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-170">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="f7d8b-171">請確定線路有沒有其他對等使用相同的 VLAN ID。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-171">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="f7d8b-172">對等的 AS 編號。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-172">AS number for peering.</span></span> <span data-ttu-id="f7d8b-173">您可以使用 2 位元組和 4 位元組 AS 編號。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-173">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="f7d8b-174">**選用：**MD5 雜湊 (如果選擇使用)。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-174">**Optional -** An MD5 hash if you choose to use one.</span></span>
3. <span data-ttu-id="f7d8b-175">如下圖所示，選取 Azure 公用對等互連列：</span><span class="sxs-lookup"><span data-stu-id="f7d8b-175">Select the Azure public peering row, as shown in the following image:</span></span>

  ![選取公用對等互連列](./media/expressroute-howto-routing-portal-resource-manager/rpublic1.png)
4. <span data-ttu-id="f7d8b-177">設定公用對等。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-177">Configure public peering.</span></span> <span data-ttu-id="f7d8b-178">下圖顯示設定範例：</span><span class="sxs-lookup"><span data-stu-id="f7d8b-178">The following image shows a configuration example:</span></span>

  ![設定公用對等互連](./media/expressroute-howto-routing-portal-resource-manager/rpublic2.png)
5. <span data-ttu-id="f7d8b-180">指定所有參數後，請儲存組態。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-180">Save the configuration once you have specified all parameters.</span></span> <span data-ttu-id="f7d8b-181">成功接受設定後，會出現類似下列範例的畫面：</span><span class="sxs-lookup"><span data-stu-id="f7d8b-181">After the configuration has been accepted successfully, you see something similar to the following example:</span></span>

  ![儲存公用對等互連設定](./media/expressroute-howto-routing-portal-resource-manager/rpublic3.png)

### <a name="to-view-azure-public-peering-details"></a><span data-ttu-id="f7d8b-183">檢視 Azure 公用對等詳細資訊</span><span class="sxs-lookup"><span data-stu-id="f7d8b-183">To view Azure public peering details</span></span>

<span data-ttu-id="f7d8b-184">選取 Azure 公用對等，即可檢視該對等的屬性。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-184">You can view the properties of Azure public peering by selecting the peering.</span></span>

![檢視公用對等互連屬性](./media/expressroute-howto-routing-portal-resource-manager/rpublic3.png)

### <a name="to-update-azure-public-peering-configuration"></a><span data-ttu-id="f7d8b-186">更新 Azure 公用對等組態</span><span class="sxs-lookup"><span data-stu-id="f7d8b-186">To update Azure public peering configuration</span></span>

<span data-ttu-id="f7d8b-187">您可以選取對等的資料列並修改對等屬性。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-187">You can select the row for peering and modify the peering properties.</span></span>

![選取公用對等互連列](./media/expressroute-howto-routing-portal-resource-manager/rpublic2.png)

### <a name="to-delete-azure-public-peering"></a><span data-ttu-id="f7d8b-189">刪除 Azure 公用對等</span><span class="sxs-lookup"><span data-stu-id="f7d8b-189">To delete Azure public peering</span></span>

<span data-ttu-id="f7d8b-190">如下列範例所示，您可以選取刪除圖示來移除對等互連設定：</span><span class="sxs-lookup"><span data-stu-id="f7d8b-190">You can remove your peering configuration by selecting the delete icon, as shown in the following example:</span></span>

![刪除公用對等互連](./media/expressroute-howto-routing-portal-resource-manager/rpublic4.png)

## <a name="microsoft-peering"></a><span data-ttu-id="f7d8b-192">Microsoft 對等互連</span><span class="sxs-lookup"><span data-stu-id="f7d8b-192">Microsoft peering</span></span>

<span data-ttu-id="f7d8b-193">本節將協助您為 ExpressRoute 線路建立、取得、更新和刪除 Microsoft 對等互連設定。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-193">This section helps you create, get, update, and delete the Microsoft peering configuration for an ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7d8b-194">在 2017 年 8 月 1 日以前設定之 ExpressRoute 線路的 Microsoft 對等互連，會透過 Microsoft 對等互連公告所有服務首碼，即使未定義路由篩選也一樣。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-194">Microsoft peering of ExpressRoute circuits that were configured prior to August 1, 2017 will have all service prefixes advertised through the Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="f7d8b-195">在 2017 年 8 月 1 日當日或以後設定之 ExpressRoute 線路的 Microsoft 對等互連，不會公告任何首碼，直到路由篩選連結至線路為止。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-195">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached to the circuit.</span></span> <span data-ttu-id="f7d8b-196">如需詳細資訊，請參閱[設定 Microsoft 對等互連的路由篩選](how-to-routefilter-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-196">For more information, see [Configure a route filter for Microsoft peering](how-to-routefilter-powershell.md).</span></span>
> 
> 

### <a name="to-create-microsoft-peering"></a><span data-ttu-id="f7d8b-197">建立 Microsoft 對等</span><span class="sxs-lookup"><span data-stu-id="f7d8b-197">To create Microsoft peering</span></span>

1. <span data-ttu-id="f7d8b-198">設定 ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-198">Configure ExpressRoute circuit.</span></span> <span data-ttu-id="f7d8b-199">先確定連線提供者已完整佈建電路，再繼續作業。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-199">Ensure that the circuit is fully provisioned by the connectivity provider before continuing further.</span></span>

  ![列出 Microsoft 對等互連](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. <span data-ttu-id="f7d8b-201">設定線路的 Microsoft 對等。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-201">Configure Microsoft peering for the circuit.</span></span> <span data-ttu-id="f7d8b-202">繼續之前，請確定您擁有下列資訊。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-202">Make sure that you have the following information before you proceed.</span></span>

  * <span data-ttu-id="f7d8b-203">主要連結的 /30 子網路。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-203">A /30 subnet for the primary link.</span></span> <span data-ttu-id="f7d8b-204">這必須是您所擁有且註冊在 RIR / IRR 中的有效公用 IPv4 首碼。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-204">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="f7d8b-205">次要連結的 /30 子網路。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-205">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="f7d8b-206">這必須是您所擁有且註冊在 RIR / IRR 中的有效公用 IPv4 首碼。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-206">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="f7d8b-207">供建立此對等的有效 VLAN ID。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-207">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="f7d8b-208">請確定線路有沒有其他對等使用相同的 VLAN ID。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-208">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="f7d8b-209">對等的 AS 編號。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-209">AS number for peering.</span></span> <span data-ttu-id="f7d8b-210">您可以使用 2 位元組和 4 位元組 AS 編號。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-210">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="f7d8b-211">公告的首碼：您必須提供一份您打算在 BGP 工作階段上公告的所有首碼的清單。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-211">Advertised prefixes: You must provide a list of all prefixes you plan to advertise over the BGP session.</span></span> <span data-ttu-id="f7d8b-212">只接受公用 IP 位址首碼。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-212">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="f7d8b-213">如果計劃傳送一組首碼，可以傳送以逗號分隔的清單。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-213">If you plan to send a set of prefixes, you can send a comma-separated list.</span></span> <span data-ttu-id="f7d8b-214">這些首碼必須在 RIR / IRR 中註冊給您。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-214">These prefixes must be registered to you in an RIR / IRR.</span></span>
  * <span data-ttu-id="f7d8b-215">**選用：**客戶 ASN：如果您要公告的首碼未註冊給對等互連 AS 編號，則可以指定它們所註冊的 AS 編號。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-215">**Optional -** Customer ASN: If you are advertising prefixes that are not registered to the peering AS number, you can specify the AS number to which they are registered.</span></span>
  * <span data-ttu-id="f7d8b-216">路由登錄名稱：您可以指定可供註冊 AS 編號和首碼的 RIR / IRR。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-216">Routing Registry Name: You can specify the RIR / IRR against which the AS number and prefixes are registered.</span></span>
  * <span data-ttu-id="f7d8b-217">**選用：**MD5 雜湊 (如果選擇使用)。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-217">**Optional -** An MD5 hash if you choose to use one.</span></span>
3. <span data-ttu-id="f7d8b-218">如下列範例所示，您可以選取要設定的對等互連。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-218">You can select the peering you wish to configure, as shown in the following example.</span></span> <span data-ttu-id="f7d8b-219">選取 Microsoft 對等資料列。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-219">Select the Microsoft peering row.</span></span>

  ![選取 Microsoft 對等互連列](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft1.png)
4. <span data-ttu-id="f7d8b-221">設定 Microsoft 對等。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-221">Configure Microsoft peering.</span></span> <span data-ttu-id="f7d8b-222">下圖顯示設定範例：</span><span class="sxs-lookup"><span data-stu-id="f7d8b-222">The following image shows a configuration example:</span></span>

  ![設定 Microsoft 對等互連](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft2.png)
5. <span data-ttu-id="f7d8b-224">指定所有參數後，請儲存組態。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-224">Save the configuration once you have specified all parameters.</span></span>

  <span data-ttu-id="f7d8b-225">如果您的線路出現「需要驗證」狀態 (如下圖所示)，您必須開立支援票證，向我們的支援小組出示首碼擁有權的證明。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-225">If your circuit gets to a 'Validation needed' state (as shown in the image), you must open a support ticket to show proof of ownership of the prefixes to our support team.</span></span>

  ![儲存 Microsoft 對等互連設定](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft5.png)

  <span data-ttu-id="f7d8b-227">如下列範例所示，您可以直接從入口網站開立支援票證：</span><span class="sxs-lookup"><span data-stu-id="f7d8b-227">You can open a support ticket directly from the portal, as shown in the following example:</span></span>

  ![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft6.png)


1. <span data-ttu-id="f7d8b-228">成功接受設定後，會出現類似下圖的畫面：</span><span class="sxs-lookup"><span data-stu-id="f7d8b-228">After the configuration has been accepted successfully, you see something similar to the following image:</span></span>

  ![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft7.png)

### <a name="to-view-microsoft-peering-details"></a><span data-ttu-id="f7d8b-229">檢視 Microsoft 對等詳細資訊</span><span class="sxs-lookup"><span data-stu-id="f7d8b-229">To view Microsoft peering details</span></span>

<span data-ttu-id="f7d8b-230">選取 Azure 公用對等，即可檢視該對等的屬性。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-230">You can view the properties of Azure public peering by selecting the peering.</span></span>

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft3.png)

### <a name="to-update-microsoft-peering-configuration"></a><span data-ttu-id="f7d8b-231">更新 Microsoft 對等組態</span><span class="sxs-lookup"><span data-stu-id="f7d8b-231">To update Microsoft peering configuration</span></span>

<span data-ttu-id="f7d8b-232">您可以選取對等的資料列並修改對等屬性。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-232">You can select the row for peering and modify the peering properties.</span></span>

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft7.png)

### <a name="to-delete-microsoft-peering"></a><span data-ttu-id="f7d8b-233">刪除 Microsoft 對等</span><span class="sxs-lookup"><span data-stu-id="f7d8b-233">To delete Microsoft peering</span></span>

<span data-ttu-id="f7d8b-234">如下圖所示，您可以選取刪除圖示來移除對等互連設定：</span><span class="sxs-lookup"><span data-stu-id="f7d8b-234">You can remove your peering configuration by selecting the delete icon, as shown in the following image:</span></span>

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft4.png)

## <a name="next-steps"></a><span data-ttu-id="f7d8b-235">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f7d8b-235">Next steps</span></span>

<span data-ttu-id="f7d8b-236">下一步，[將 VNet 連結到 ExpressRoute 線路](expressroute-howto-linkvnet-portal-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="f7d8b-236">Next step, [Link a VNet to an ExpressRoute circuit](expressroute-howto-linkvnet-portal-resource-manager.md)</span></span>
* <span data-ttu-id="f7d8b-237">如需 ExpressRoute 工作流程的詳細資訊，請參閱 [ExpressRoute 工作流程](expressroute-workflows.md)。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-237">For more information about ExpressRoute workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="f7d8b-238">如需線路對等的詳細資訊，請參閱 [ExpressRoute 線路和路由網域](expressroute-circuit-peerings.md)。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-238">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>
* <span data-ttu-id="f7d8b-239">如需使用虛擬網路的詳細資訊，請參閱 [虛擬網路概觀](../virtual-network/virtual-networks-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="f7d8b-239">For more information about working with virtual networks, see [Virtual network overview](../virtual-network/virtual-networks-overview.md).</span></span>
