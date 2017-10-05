---
title: "刪除虛擬網路閘道：Azure 入口網站：Resource Manager | Microsoft Docs"
description: "在 Resource Manager 部署模型中使用 Azure 入口網站刪除虛擬網路閘道。"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: 
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/20/2017
ms.author: cherylmc
ms.openlocfilehash: 1d289c09465cb8d5e4bfa569441dffcbf562b3bf
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="delete-a-virtual-network-gateway-using-the-portal"></a><span data-ttu-id="d3389-103">使用入口網站刪除虛擬網路閘道</span><span class="sxs-lookup"><span data-stu-id="d3389-103">Delete a virtual network gateway using the portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="d3389-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="d3389-104">Azure portal</span></span>](vpn-gateway-delete-vnet-gateway-portal.md)
> * [<span data-ttu-id="d3389-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d3389-105">PowerShell</span></span>](vpn-gateway-delete-vnet-gateway-powershell.md)
> * [<span data-ttu-id="d3389-106">PowerShell (傳統)</span><span class="sxs-lookup"><span data-stu-id="d3389-106">PowerShell (classic)</span></span>](vpn-gateway-delete-vnet-gateway-classic-powershell.md)

<span data-ttu-id="d3389-107">如果您想要刪除 VPN 閘道組態的虛擬網路閘道，您可以採取幾種不同的方法。</span><span class="sxs-lookup"><span data-stu-id="d3389-107">There are a couple of different approaches you can take when you want to delete a virtual network gateway for a VPN gateway configuration.</span></span>

- <span data-ttu-id="d3389-108">如果您想要刪除所有內容並重頭開始 (例如使用測試環境的情況)，您可以刪除資源群組。</span><span class="sxs-lookup"><span data-stu-id="d3389-108">If you want to delete everything and start over, as in the case of a test environment, you can delete the resource group.</span></span> <span data-ttu-id="d3389-109">刪除資源群組時，會一併刪除群組內的所有資源。</span><span class="sxs-lookup"><span data-stu-id="d3389-109">When you delete a resource group, it deletes all the resources within the group.</span></span> <span data-ttu-id="d3389-110">只有在您不想保留資源群組中的任何資源時，才建議使用此方法。</span><span class="sxs-lookup"><span data-stu-id="d3389-110">This is method is only recommended if you don't want to keep any of the resources in the resource group.</span></span> <span data-ttu-id="d3389-111">您無法使用這種方法，選擇性地只刪除一些資源。</span><span class="sxs-lookup"><span data-stu-id="d3389-111">You can't selectively delete only a few resources using this approach.</span></span>

- <span data-ttu-id="d3389-112">如果您想要保留資源群組中的部分資源，刪除虛擬網路閘道會變得稍微複雜一點。</span><span class="sxs-lookup"><span data-stu-id="d3389-112">If you want to keep some of the resources in your resource group, deleting a virtual network gateway becomes slightly more complicated.</span></span> <span data-ttu-id="d3389-113">您必須先刪除任何相依於閘道的資源，才可以刪除虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="d3389-113">Before you can delete the virtual network gateway, you must first delete any resources that are dependent on the gateway.</span></span> <span data-ttu-id="d3389-114">您遵循的步驟取決於您所建立的連線類型以及每個連線的相依資源。</span><span class="sxs-lookup"><span data-stu-id="d3389-114">The steps you follow depend on the type of connections that you created and the dependent resources for each connection.</span></span>

## <a name="delete-a-vpn-gateway"></a><span data-ttu-id="d3389-115">刪除 VPN 閘道</span><span class="sxs-lookup"><span data-stu-id="d3389-115">Delete a VPN gateway</span></span>

<span data-ttu-id="d3389-116">若要刪除虛擬網路閘道，您必須先刪除虛擬網路閘道的每個相關資源。</span><span class="sxs-lookup"><span data-stu-id="d3389-116">To delete a virtual network gateway, you must first delete each resource that pertains to the virtual network gateway.</span></span> <span data-ttu-id="d3389-117">由於相依性，您必須依照特定順序刪除資源。</span><span class="sxs-lookup"><span data-stu-id="d3389-117">Resources must be deleted in a certain order due to dependencies.</span></span>

[!INCLUDE [delete gateway](../../includes/vpn-gateway-delete-vnet-gateway-portal-include.md)]

<span data-ttu-id="d3389-118">此時，虛擬網路閘道已經刪除。</span><span class="sxs-lookup"><span data-stu-id="d3389-118">At this point, the virtual network gateway is deleted.</span></span> <span data-ttu-id="d3389-119">後續步驟會協助您刪除不再使用的任何資源。</span><span class="sxs-lookup"><span data-stu-id="d3389-119">The next steps help you delete any resources that are no longer being used.</span></span>

### <a name="to-delete-the-local-network-gateway"></a><span data-ttu-id="d3389-120">刪除區域網路閘道</span><span class="sxs-lookup"><span data-stu-id="d3389-120">To delete the local network gateway</span></span>

1. <span data-ttu-id="d3389-121">在 [所有資源] 中，找出與每個連線相關聯的區域網路閘道。</span><span class="sxs-lookup"><span data-stu-id="d3389-121">In **All resources**, locate the local network gateways that were associated with each connection.</span></span>
2. <span data-ttu-id="d3389-122">在區域網路閘道的 [概觀] 刀鋒視窗中，按一下 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="d3389-122">On the **Overview** blade for the local network gateway, click **Delete**.</span></span>

### <a name="to-delete-the-public-ip-address-resource-for-the-gateway"></a><span data-ttu-id="d3389-123">刪除閘道的公用 IP 位址資源</span><span class="sxs-lookup"><span data-stu-id="d3389-123">To delete the Public IP address resource for the gateway</span></span>

1. <span data-ttu-id="d3389-124">在 [所有資源] 中，找出與閘道相關聯的公用 IP 位址資源。</span><span class="sxs-lookup"><span data-stu-id="d3389-124">In **All resources**, locate the Public IP address resource that was associated to the gateway.</span></span> <span data-ttu-id="d3389-125">如果虛擬網路閘道為主動-主動，您會看到兩個公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="d3389-125">If the virtual network gateway was active-active, you will see two Public IP addresses.</span></span> 
2. <span data-ttu-id="d3389-126">在公用 IP 位址的 [概觀] 頁面上，按一下 [刪除]，然後按一下 [是] 以確認。</span><span class="sxs-lookup"><span data-stu-id="d3389-126">On the **Overview** page for the Public IP address, click **Delete**, then **Yes** to confirm.</span></span>

### <a name="to-delete-the-gateway-subnet"></a><span data-ttu-id="d3389-127">刪除閘道子網路</span><span class="sxs-lookup"><span data-stu-id="d3389-127">To delete the gateway subnet</span></span>

1. <span data-ttu-id="d3389-128">在 [所有資源] 中，找出虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="d3389-128">In **All resources**, locate the virtual network.</span></span> 
2. <span data-ttu-id="d3389-129">在 [子網路] 刀鋒視窗中，按一下 [GatewaySubnet]，然後按一下 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="d3389-129">On the **Subnets** blade, click the **GatewaySubnet**, then click **Delete**.</span></span> 
3. <span data-ttu-id="d3389-130">按一下 [是] 確認要刪除閘道子網路。</span><span class="sxs-lookup"><span data-stu-id="d3389-130">Click **Yes** to confirm that you want to delete the gateway subnet.</span></span>

## <span data-ttu-id="d3389-131"><a name="deleterg"></a>藉由刪除資源群組來刪除 VPN 閘道</span><span class="sxs-lookup"><span data-stu-id="d3389-131"><a name="deleterg"></a>Delete a VPN gateway by deleting the resource group</span></span>

<span data-ttu-id="d3389-132">如果您不在乎保留資源群組中任何資源，而只想要從頭開始，您可以刪除整個資源群組。</span><span class="sxs-lookup"><span data-stu-id="d3389-132">If you are not concerned about keeping any of your resources in the resource group and you just want to start over, you can delete an entire resource group.</span></span> <span data-ttu-id="d3389-133">這是移除所有項目的快速方法。</span><span class="sxs-lookup"><span data-stu-id="d3389-133">This is a quick way to remove everything.</span></span> <span data-ttu-id="d3389-134">下列步驟僅適用於 Resource Manager 部署模型。</span><span class="sxs-lookup"><span data-stu-id="d3389-134">The following steps apply only to the Resource Manager deployment model.</span></span>

1. <span data-ttu-id="d3389-135">在 [所有資源] 中，找出資源群組，然後按一下以開啟刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="d3389-135">In **All resources**, locate the resource group and click to open the blade.</span></span>
2. <span data-ttu-id="d3389-136">按一下 [刪除] 。</span><span class="sxs-lookup"><span data-stu-id="d3389-136">Click **Delete**.</span></span> <span data-ttu-id="d3389-137">在 [刪除] 刀鋒視窗中，檢視受影響的資源。</span><span class="sxs-lookup"><span data-stu-id="d3389-137">On the Delete blade, view the affected resources.</span></span> <span data-ttu-id="d3389-138">請確定您想要刪除所有資源。</span><span class="sxs-lookup"><span data-stu-id="d3389-138">Make sure that you want to delete all of these resources.</span></span> <span data-ttu-id="d3389-139">如果不是，請使用這篇文章上方之[刪除 VPN 閘道](#deletegw)中的步驟。</span><span class="sxs-lookup"><span data-stu-id="d3389-139">If not, use the steps in [Delete a VPN gateway](#deletegw) at the top of this article.</span></span>
3. <span data-ttu-id="d3389-140">若要繼續，請輸入您想要刪除之資源群組的名稱，然後按一下 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="d3389-140">To proceed, type the name of the resource group that you want to delete, then click **Delete**.</span></span>