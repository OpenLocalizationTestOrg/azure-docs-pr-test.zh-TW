---
title: "如何 Azure ExpressRoute 電路的路由 tooconfigure: CLI |Microsoft 文件"
description: "這篇文章可協助您建立與 hello 私人、 公用及 Microsoft 對等 ExpressRoute 循環的佈建。 本文也會顯示 toocheck hello 狀態、 更新或刪除您的電路的互連的方式。"
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: anzaman,cherylmc
ms.openlocfilehash: 33130af050045527cdb316e77821c6d101b6a82a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-routing-for-an-expressroute-circuit-using-cli"></a><span data-ttu-id="f4a6a-104">使用 CLI 來建立和修改 ExpressRoute 路線的路由</span><span class="sxs-lookup"><span data-stu-id="f4a6a-104">Create and modify routing for an ExpressRoute circuit using CLI</span></span>

<span data-ttu-id="f4a6a-105">這篇文章可協助您建立及管理在 hello 資源管理員部署模型中使用 CLI 的 ExpressRoute 電路的路由組態。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-105">This article helps you create and manage routing configuration for an ExpressRoute circuit in hello Resource Manager deployment model using CLI.</span></span> <span data-ttu-id="f4a6a-106">您也可以檢查 hello 狀態、 更新或刪除，並取消佈建 ExpressRoute 循環的對等互連。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-106">You can also check hello status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span> <span data-ttu-id="f4a6a-107">如果您想 toouse 不同方法 toowork 與您的循環，請從下列清單中的 hello 選取一個發行項：</span><span class="sxs-lookup"><span data-stu-id="f4a6a-107">If you want toouse a different method toowork with your circuit, select an article from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f4a6a-108">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="f4a6a-108">Azure portal</span></span>](expressroute-howto-routing-portal-resource-manager.md)
> * [<span data-ttu-id="f4a6a-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f4a6a-109">PowerShell</span></span>](expressroute-howto-routing-arm.md)
> * [<span data-ttu-id="f4a6a-110">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="f4a6a-110">Azure CLI</span></span>](howto-routing-cli.md)
> * [<span data-ttu-id="f4a6a-111">視訊 - 私用對等互連</span><span class="sxs-lookup"><span data-stu-id="f4a6a-111">Video - Private peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="f4a6a-112">視訊 - 公用對等互連</span><span class="sxs-lookup"><span data-stu-id="f4a6a-112">Video - Public peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="f4a6a-113">視訊 - Microsoft 對等互連</span><span class="sxs-lookup"><span data-stu-id="f4a6a-113">Video - Microsoft peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="f4a6a-114">PowerShell (傳統)</span><span class="sxs-lookup"><span data-stu-id="f4a6a-114">PowerShell (classic)</span></span>](expressroute-howto-routing-classic.md)
> 

## <a name="configuration-prerequisites"></a><span data-ttu-id="f4a6a-115">組態必要條件</span><span class="sxs-lookup"><span data-stu-id="f4a6a-115">Configuration prerequisites</span></span>

* <span data-ttu-id="f4a6a-116">在開始之前，安裝 hello 最新版本 （2.0 或更新版本） 的 hello CLI 命令。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-116">Before beginning, install hello latest version of hello CLI commands (2.0 or later).</span></span> <span data-ttu-id="f4a6a-117">如需安裝 hello CLI 命令的資訊，請參閱[安裝 Azure CLI 2.0](/cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-117">For information about installing hello CLI commands, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span>
* <span data-ttu-id="f4a6a-118">請確定您已經檢閱 hello[必要條件](expressroute-prerequisites.md)，[路由需求](expressroute-routing.md)，和[工作流程](expressroute-workflows.md)頁面開始設定之前。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-118">Make sure that you have reviewed hello [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflow](expressroute-workflows.md) pages before you begin configuration.</span></span>
* <span data-ttu-id="f4a6a-119">您必須擁有作用中的 ExpressRoute 線路。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-119">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="f4a6a-120">請依照下列指示 hello 太[建立 ExpressRoute 電路](howto-circuit-cli.md)和有 hello 電路啟用您的連線提供者，才能繼續。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-120">Follow hello instructions too[Create an ExpressRoute circuit](howto-circuit-cli.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="f4a6a-121">hello ExpressRoute 電路必須位於您 toobe 無法 toorun hello 命令，在本文中的佈建並啟用狀態。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-121">hello ExpressRoute circuit must be in a provisioned and enabled state for you toobe able toorun hello commands in this article.</span></span>

<span data-ttu-id="f4a6a-122">這些說明僅適用於 toocircuits 建立與服務供應項目層級 2 連線服務的提供者。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-122">These instructions only apply toocircuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="f4a6a-123">如果您使用的服務提供者提供受管理的第 3 層服務 (通常是 IPVPN，如 MPLS)，連線提供者會為您設定和管理路由。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-123">If you are using a service provider that offers managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>

<span data-ttu-id="f4a6a-124">您可以為 ExpressRoute 線路設定一個、兩個或全部三個對等 (Azure 私用、Azure 公用和 Microsoft)。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-124">You can configure one, two, or all three peerings (Azure private, Azure public, and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="f4a6a-125">您可以依自己選擇的任何順序設定對等。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-125">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="f4a6a-126">不過，您必須確定您完成每個對等互連一次一個的 hello 設定。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-126">However, you must make sure that you complete hello configuration of each peering one at a time.</span></span>

## <a name="azure-private-peering"></a><span data-ttu-id="f4a6a-127">Azure 私用對等</span><span class="sxs-lookup"><span data-stu-id="f4a6a-127">Azure private peering</span></span>

<span data-ttu-id="f4a6a-128">本節可協助您建立、 取得、 更新和刪除 hello Azure ExpressRoute 循環的私用對等設定。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-128">This section helps you create, get, update, and delete hello Azure private peering configuration for an ExpressRoute circuit.</span></span>

### <a name="toocreate-azure-private-peering"></a><span data-ttu-id="f4a6a-129">toocreate Azure 私人互連</span><span class="sxs-lookup"><span data-stu-id="f4a6a-129">toocreate Azure private peering</span></span>

1. <span data-ttu-id="f4a6a-130">安裝 Azure CLI hello 最新版本。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-130">Install hello latest version of Azure CLI.</span></span> <span data-ttu-id="f4a6a-131">您必須使用 hello hello Azure 命令列介面 (CLI) 最新版本。 * 檢閱 hello[必要條件](expressroute-prerequisites.md)和[工作流程](expressroute-workflows.md)開始設定之前。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-131">You must use hello latest version of hello Azure Command-line Interface (CLI).* Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

  ```azurecli
  az login
  ```

  <span data-ttu-id="f4a6a-132">選取您想要 toocreate ExpressRoute 電路的 hello 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="f4a6a-132">Select hello subscription you want toocreate ExpressRoute circuit</span></span>

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. <span data-ttu-id="f4a6a-133">建立 ExpressRoute 線路。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-133">Create an ExpressRoute circuit.</span></span> <span data-ttu-id="f4a6a-134">請遵循 hello 指示 toocreate [ExpressRoute 電路](howto-circuit-cli.md)，並讓它佈建的 hello 連線服務提供者。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-134">Follow hello instructions toocreate an [ExpressRoute circuit](howto-circuit-cli.md) and have it provisioned by hello connectivity provider.</span></span>

  <span data-ttu-id="f4a6a-135">如果您連線服務提供者提供受管理的第 3 層服務，您可以要求您連線提供者 tooenable 私用對等互連，為您的 Azure。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-135">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure private peering for you.</span></span> <span data-ttu-id="f4a6a-136">在此情況下，您不需要 toofollow hello 下一節中所列的指示。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-136">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="f4a6a-137">不過，如果您連線服務提供者不會管理路由，在建立您的循環之後繼續您 hello 後續步驟的組態。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-137">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using hello next steps.</span></span>
3. <span data-ttu-id="f4a6a-138">請檢查 hello ExpressRoute 電路 toomake 確定佈建，而且也已啟用。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-138">Check hello ExpressRoute circuit toomake sure it is provisioned and also enabled.</span></span> <span data-ttu-id="f4a6a-139">下列範例使用 hello:</span><span class="sxs-lookup"><span data-stu-id="f4a6a-139">Use hello following example:</span></span>

  ```azurecli
  az network express-route show --resource-group ExpressRouteResourceGroup --name MyCircuit
  ```

  <span data-ttu-id="f4a6a-140">hello 回應是類似 toohello 下列範例：</span><span class="sxs-lookup"><span data-stu-id="f4a6a-140">hello response is similar toohello following example:</span></span>

  ```azurecli
  "allowClassicOperations": false,
  "authorizations": [],
  "circuitProvisioningState": "Enabled",
  "etag": "W/\"1262c492-ffef-4a63-95a8-a6002736b8c4\"",
  "gatewayManagerEtag": null,
  "id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit",
  "location": "westus",
  "name": "MyCircuit",
  "peerings": [],
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "serviceKey": "1d05cf70-1db5-419f-ad86-1ca62c3c125b",
  "serviceProviderNotes": null,
  "serviceProviderProperties": {
  "bandwidthInMbps": 200,
  "peeringLocation": "Silicon Valley",
  "serviceProviderName": "Equinix"
  },
  "serviceProviderProvisioningState": "Provisioned",
  "sku": {
    "family": "UnlimitedData",
    "name": "Standard_MeteredData",
    "tier": "Standard"
  },
  "tags": null,
  "type": "Microsoft.Network/expressRouteCircuits]
  ```

4. <span data-ttu-id="f4a6a-141">設定 Azure 私用對等互連 hello 循環。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-141">Configure Azure private peering for hello circuit.</span></span> <span data-ttu-id="f4a6a-142">請確定您具備下列項目，再繼續進行下一個步驟的 hello hello:</span><span class="sxs-lookup"><span data-stu-id="f4a6a-142">Make sure that you have hello following items before you proceed with hello next steps:</span></span>

  * <span data-ttu-id="f4a6a-143">/ 30 子網路 hello 主要連結。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-143">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="f4a6a-144">hello 子網路不能保留的虛擬網路的任何位址空間的一部分。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-144">hello subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="f4a6a-145">/ 30 hello 次要連結的子網路。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-145">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="f4a6a-146">hello 子網路不能保留的虛擬網路的任何位址空間的一部分。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-146">hello subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="f4a6a-147">有效的 VLAN ID tooestablish 此對等。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-147">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="f4a6a-148">請確認沒有其他對等互連中 hello 循環使用 hello 相同 VLAN id。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-148">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="f4a6a-149">對等的 AS 編號。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-149">AS number for peering.</span></span> <span data-ttu-id="f4a6a-150">您可以使用 2 位元組和 4 位元組 AS 編號。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-150">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="f4a6a-151">您可以將私用 AS 編號用於此對等。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-151">You can use a private AS number for this peering.</span></span> <span data-ttu-id="f4a6a-152">請確定您不是使用 65515。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-152">Ensure that you are not using 65515.</span></span>
  * <span data-ttu-id="f4a6a-153">**選用-**如果您選擇其中一個 toouse 的 MD5 雜湊。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-153">**Optional -** An MD5 hash if you choose toouse one.</span></span>

  <span data-ttu-id="f4a6a-154">使用下列範例 tooconfigure Azure 私用對等互連，為您的電路的 hello:</span><span class="sxs-lookup"><span data-stu-id="f4a6a-154">Use hello following example tooconfigure Azure private peering for your circuit:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 10.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 10.0.0.4/30 --vlan-id 200 --peering-type AzurePrivatePeering
  ```

  <span data-ttu-id="f4a6a-155">如果您選擇 toouse MD5 雜湊時，使用下列範例中的 hello:</span><span class="sxs-lookup"><span data-stu-id="f4a6a-155">If you choose toouse an MD5 hash, use hello following example:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 10.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 10.0.0.4/30 --vlan-id 200 --peering-type AzurePrivatePeering --SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > <span data-ttu-id="f4a6a-156">請確定您將 AS 編號指定為對等 ASN，而不是客戶 ASN。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-156">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>
  > 
  > 

### <a name="tooview-azure-private-peering-details"></a><span data-ttu-id="f4a6a-157">tooview Azure 私用對等互連的詳細資料</span><span class="sxs-lookup"><span data-stu-id="f4a6a-157">tooview Azure private peering details</span></span>

<span data-ttu-id="f4a6a-158">您可以使用下列範例中的 hello，以取得設定的詳細資訊：</span><span class="sxs-lookup"><span data-stu-id="f4a6a-158">You can get configuration details by using hello following example:</span></span>

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

<span data-ttu-id="f4a6a-159">hello 輸出是 toohello 類似下列範例程式碼：</span><span class="sxs-lookup"><span data-stu-id="f4a6a-159">hello output is similar toohello following example:</span></span>

```azurecli
{
  "azureAsn": 12076,
  "etag": "W/\"2e97be83-a684-4f29-bf3c-96191e270666\"",
  "gatewayManagerEtag": "18",
  "id": "/subscriptions/9a0c2943-e0c2-4608-876c-e0ddffd1211b/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/peerings/AzurePrivatePeering",
  "ipv6PeeringConfig": null,
  "lastModifiedBy": "Customer",
  "microsoftPeeringConfig": null,
  "name": "AzurePrivatePeering",
  "peerAsn": 7671,
  "peeringType": "AzurePrivatePeering",
  "primaryAzurePort": "",
  "primaryPeerAddressPrefix": "",
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "routeFilter": null,
  "secondaryAzurePort": "",
  "secondaryPeerAddressPrefix": "",
  "sharedKey": null,
  "state": "Enabled",
  "stats": null,
  "vlanId": 100
}
```

### <a name="tooupdate-azure-private-peering-configuration"></a><span data-ttu-id="f4a6a-160">tooupdate Azure 私用對等組態</span><span class="sxs-lookup"><span data-stu-id="f4a6a-160">tooupdate Azure private peering configuration</span></span>

<span data-ttu-id="f4a6a-161">您可以更新使用下列範例中的 hello hello 設定的任何部分。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-161">You can update any part of hello configuration using hello following example.</span></span> <span data-ttu-id="f4a6a-162">在此範例中，從 100 too500 正在更新 hello hello 循環的 VLAN ID。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-162">In this example, hello VLAN ID of hello circuit is being updated from 100 too500.</span></span>

```azurecli
az network express-route peering update --vlan-id 500 -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

### <a name="toodelete-azure-private-peering"></a><span data-ttu-id="f4a6a-163">toodelete Azure 私人互連</span><span class="sxs-lookup"><span data-stu-id="f4a6a-163">toodelete Azure private peering</span></span>

<span data-ttu-id="f4a6a-164">您可以執行下列範例中的 hello 來移除您對等的設定：</span><span class="sxs-lookup"><span data-stu-id="f4a6a-164">You can remove your peering configuration by running hello following example:</span></span>

> [!WARNING]
> <span data-ttu-id="f4a6a-165">您必須確定所有虛擬網路，然後再執行此範例會從 hello ExpressRoute 電路取消連結。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-165">You must ensure that all virtual networks are unlinked from hello ExpressRoute circuit before running this example.</span></span> 
> 
> 

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

## <a name="azure-public-peering"></a><span data-ttu-id="f4a6a-166">Azure 公用對等</span><span class="sxs-lookup"><span data-stu-id="f4a6a-166">Azure public peering</span></span>

<span data-ttu-id="f4a6a-167">本節可協助您建立、 取得、 更新和刪除 hello Azure ExpressRoute 循環的公用對等設定。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-167">This section helps you create, get, update, and delete hello Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="toocreate-azure-public-peering"></a><span data-ttu-id="f4a6a-168">toocreate Azure 公用對等互連</span><span class="sxs-lookup"><span data-stu-id="f4a6a-168">toocreate Azure public peering</span></span>

1. <span data-ttu-id="f4a6a-169">安裝 Azure CLI hello 最新版本。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-169">Install hello latest version of Azure CLI.</span></span> <span data-ttu-id="f4a6a-170">您必須使用 hello hello Azure 命令列介面 (CLI) 最新版本。 * 檢閱 hello[必要條件](expressroute-prerequisites.md)和[工作流程](expressroute-workflows.md)開始設定之前。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-170">You must use hello latest version of hello Azure Command-line Interface (CLI).* Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

  ```azurecli
  az login
  ```

  <span data-ttu-id="f4a6a-171">選取您想要的 toocreate ExpressRoute 電路的 hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-171">Select hello subscription for which you want toocreate ExpressRoute circuit.</span></span>

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. <span data-ttu-id="f4a6a-172">建立 ExpressRoute 線路。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-172">Create an ExpressRoute circuit.</span></span>  <span data-ttu-id="f4a6a-173">請遵循 hello 指示 toocreate [ExpressRoute 電路](howto-circuit-cli.md)，並讓它佈建的 hello 連線服務提供者。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-173">Follow hello instructions toocreate an [ExpressRoute circuit](howto-circuit-cli.md) and have it provisioned by hello connectivity provider.</span></span>

  <span data-ttu-id="f4a6a-174">如果您的連線提供者是提供受管理的第 3 層服務，您可以要求連線提供者為您啟用 Azure 私用對等互連。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-174">If your connectivity provider offers managed Layer 3 services, you can request that your connectivity provider enables Azure private peering for you.</span></span> <span data-ttu-id="f4a6a-175">在此情況下，您不需要 toofollow hello 下一節中所列的指示。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-175">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="f4a6a-176">不過，如果您連線服務提供者不會管理路由，在建立您的循環之後繼續您 hello 後續步驟的組態。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-176">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using hello next steps.</span></span>
3. <span data-ttu-id="f4a6a-177">請檢查已佈建並也啟用 hello ExpressRoute 電路 tooensure。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-177">Check hello ExpressRoute circuit tooensure it is provisioned and also enabled.</span></span> <span data-ttu-id="f4a6a-178">下列範例使用 hello:</span><span class="sxs-lookup"><span data-stu-id="f4a6a-178">Use hello following example:</span></span>

  ```azurecli
  az network express-route list
  ```

  <span data-ttu-id="f4a6a-179">hello 回應是類似 toohello 下列範例：</span><span class="sxs-lookup"><span data-stu-id="f4a6a-179">hello response is similar toohello following example:</span></span>

  ```azurecli
  "allowClassicOperations": false,
  "authorizations": [],
  "circuitProvisioningState": "Enabled",
  "etag": "W/\"1262c492-ffef-4a63-95a8-a6002736b8c4\"",
  "gatewayManagerEtag": null,
  "id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit",
  "location": "westus",
  "name": "MyCircuit",
  "peerings": [],
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "serviceKey": "1d05cf70-1db5-419f-ad86-1ca62c3c125b",
  "serviceProviderNotes": null,
  "serviceProviderProperties": {
    "bandwidthInMbps": 200,
    "peeringLocation": "Silicon Valley",
    "serviceProviderName": "Equinix"
  },
  "serviceProviderProvisioningState": "Provisioned",
  "sku": {
    "family": "UnlimitedData",
    "name": "Standard_MeteredData",
    "tier": "Standard"
  },
  "tags": null,
  "type": "Microsoft.Network/expressRouteCircuits]
  ```

4. <span data-ttu-id="f4a6a-180">設定 Azure 公用對等互連 hello 循環。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-180">Configure Azure public peering for hello circuit.</span></span> <span data-ttu-id="f4a6a-181">請確定您擁有 hello 繼續接下來，下列資訊。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-181">Make sure that you have hello following information before you proceed further.</span></span>

  * <span data-ttu-id="f4a6a-182">/ 30 子網路 hello 主要連結。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-182">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="f4a6a-183">這必須是有效的公用 IPv4 首碼。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-183">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="f4a6a-184">/ 30 hello 次要連結的子網路。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-184">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="f4a6a-185">這必須是有效的公用 IPv4 首碼。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-185">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="f4a6a-186">有效的 VLAN ID tooestablish 此對等。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-186">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="f4a6a-187">請確認沒有其他對等互連中 hello 循環使用 hello 相同 VLAN id。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-187">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="f4a6a-188">對等的 AS 編號。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-188">AS number for peering.</span></span> <span data-ttu-id="f4a6a-189">您可以使用 2 位元組和 4 位元組 AS 編號。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-189">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="f4a6a-190">**選用-**如果您選擇其中一個 toouse 的 MD5 雜湊。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-190">**Optional -** An MD5 hash if you choose toouse one.</span></span>

  <span data-ttu-id="f4a6a-191">執行下列範例 tooconfigure Azure 公用對等互連，為您的電路的 hello:</span><span class="sxs-lookup"><span data-stu-id="f4a6a-191">Run hello following example tooconfigure Azure public peering for your circuit:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 12.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 12.0.0.4/30 --vlan-id 200 --peering-type AzurePublicPeering
  ```

  <span data-ttu-id="f4a6a-192">如果您選擇 toouse MD5 雜湊時，使用下列範例中的 hello:</span><span class="sxs-lookup"><span data-stu-id="f4a6a-192">If you choose toouse an MD5 hash, use hello following example:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 12.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 12.0.0.4/30 --vlan-id 200 --peering-type AzurePublicPeering --SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > <span data-ttu-id="f4a6a-193">請確定您將 AS 編號指定為對等 ASN，而不是客戶 ASN。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-193">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>

### <a name="tooview-azure-public-peering-details"></a><span data-ttu-id="f4a6a-194">tooview Azure 公用對等互連的詳細資料</span><span class="sxs-lookup"><span data-stu-id="f4a6a-194">tooview Azure public peering details</span></span>

<span data-ttu-id="f4a6a-195">就可以使用下列範例中的 hello 設定詳細資料：</span><span class="sxs-lookup"><span data-stu-id="f4a6a-195">You can get configuration details using hello following example:</span></span>

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

<span data-ttu-id="f4a6a-196">hello 輸出是 toohello 類似下列範例程式碼：</span><span class="sxs-lookup"><span data-stu-id="f4a6a-196">hello output is similar toohello following example:</span></span>

```azurecli
{
  "azureAsn": 12076,
  "etag": "W/\"2e97be83-a684-4f29-bf3c-96191e270666\"",
  "gatewayManagerEtag": "18",
  "id": "/subscriptions/9a0c2943-e0c2-4608-876c-e0ddffd1211b/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/peerings/AzurePublicPeering",
  "lastModifiedBy": "Customer",
  "microsoftPeeringConfig": null,
  "name": "AzurePublicPeering",
  "peerAsn": 7671,
  "peeringType": "AzurePublicPeering",
  "primaryAzurePort": "",
  "primaryPeerAddressPrefix": "",
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "routeFilter": null,
  "secondaryAzurePort": "",
  "secondaryPeerAddressPrefix": "",
  "sharedKey": null,
  "state": "Enabled",
  "stats": null,
  "vlanId": 100
}
```

### <a name="tooupdate-azure-public-peering-configuration"></a><span data-ttu-id="f4a6a-197">tooupdate Azure 公用對等組態</span><span class="sxs-lookup"><span data-stu-id="f4a6a-197">tooupdate Azure public peering configuration</span></span>

<span data-ttu-id="f4a6a-198">您可以更新使用下列範例中的 hello hello 設定的任何部分。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-198">You can update any part of hello configuration using hello following example.</span></span> <span data-ttu-id="f4a6a-199">在此範例中，從 200 too600 正在更新 hello hello 循環的 VLAN ID。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-199">In this example, hello VLAN ID of hello circuit is being updated from 200 too600.</span></span>

```azurecli
az network express-route peering update --vlan-id 600 -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

### <a name="toodelete-azure-public-peering"></a><span data-ttu-id="f4a6a-200">toodelete Azure 公用對等互連</span><span class="sxs-lookup"><span data-stu-id="f4a6a-200">toodelete Azure public peering</span></span>

<span data-ttu-id="f4a6a-201">您可以執行下列範例中的 hello 來移除您對等的設定：</span><span class="sxs-lookup"><span data-stu-id="f4a6a-201">You can remove your peering configuration by running hello following example:</span></span>

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

## <a name="microsoft-peering"></a><span data-ttu-id="f4a6a-202">Microsoft 對等互連</span><span class="sxs-lookup"><span data-stu-id="f4a6a-202">Microsoft peering</span></span>

<span data-ttu-id="f4a6a-203">本節可協助您建立、 取得、 更新和刪除 ExpressRoute 循環的 hello Microsoft 對等設定。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-203">This section helps you create, get, update, and delete hello Microsoft peering configuration for an ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f4a6a-204">Microsoft 對等互連的 ExpressRoute 電路已設定先前 tooAugust 1，2017年必須透過 hello Microsoft 對等互連，公告的所有服務首碼，即使未定義路由篩選器。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-204">Microsoft peering of ExpressRoute circuits that were configured prior tooAugust 1, 2017 will have all service prefixes advertised through hello Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="f4a6a-205">Microsoft 對等互連的當天或之後 2017 年 8 月 1，已設定的 ExpressRoute 電路並不會有任何前置詞通告的路由篩選器連接直到 toohello 循環。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-205">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached toohello circuit.</span></span> <span data-ttu-id="f4a6a-206">如需詳細資訊，請參閱[設定 Microsoft 對等互連的路由篩選](how-to-routefilter-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-206">For more information, see [Configure a route filter for Microsoft peering](how-to-routefilter-powershell.md).</span></span>
> 
> 

### <a name="toocreate-microsoft-peering"></a><span data-ttu-id="f4a6a-207">toocreate Microsoft 對等互連</span><span class="sxs-lookup"><span data-stu-id="f4a6a-207">toocreate Microsoft peering</span></span>

1. <span data-ttu-id="f4a6a-208">安裝 Azure CLI hello 最新版本。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-208">Install hello latest version of Azure CLI.</span></span> <span data-ttu-id="f4a6a-209">使用 hello 最新版本的 hello Azure 命令列介面 (CLI)。 * 檢閱 hello[必要條件](expressroute-prerequisites.md)和[工作流程](expressroute-workflows.md)開始設定之前。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-209">Use hello latest version of hello Azure Command-line Interface (CLI).* Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

  ```azurecli
  az login
  ```

  <span data-ttu-id="f4a6a-210">選取您想要的 toocreate ExpressRoute 電路的 hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-210">Select hello subscription for which you want toocreate ExpressRoute circuit.</span></span>

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. <span data-ttu-id="f4a6a-211">建立 ExpressRoute 線路。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-211">Create an ExpressRoute circuit.</span></span> <span data-ttu-id="f4a6a-212">請遵循 hello 指示 toocreate [ExpressRoute 電路](howto-circuit-cli.md)，並讓它佈建的 hello 連線服務提供者。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-212">Follow hello instructions toocreate an [ExpressRoute circuit](howto-circuit-cli.md) and have it provisioned by hello connectivity provider.</span></span>

  <span data-ttu-id="f4a6a-213">如果您連線服務提供者提供受管理的第 3 層服務，您可以要求您連線提供者 tooenable 私用對等互連，為您的 Azure。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-213">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure private peering for you.</span></span> <span data-ttu-id="f4a6a-214">在此情況下，您不需要 toofollow hello 下一節中所列的指示。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-214">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="f4a6a-215">不過，如果您連線服務提供者不會管理路由，在建立您的循環之後繼續您 hello 後續步驟的組態。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-215">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using hello next steps.</span></span>

3. <span data-ttu-id="f4a6a-216">請檢查 hello ExpressRoute 電路 toomake 確定佈建，而且也已啟用。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-216">Check hello ExpressRoute circuit toomake sure it is provisioned and also enabled.</span></span> <span data-ttu-id="f4a6a-217">下列範例使用 hello:</span><span class="sxs-lookup"><span data-stu-id="f4a6a-217">Use hello following example:</span></span>

  ```azurecli
  az network express-route list
  ```

  <span data-ttu-id="f4a6a-218">hello 回應是類似 toohello 下列範例：</span><span class="sxs-lookup"><span data-stu-id="f4a6a-218">hello response is similar toohello following example:</span></span>

  ```azurecli
  "allowClassicOperations": false,
  "authorizations": [],
  "circuitProvisioningState": "Enabled",
  "etag": "W/\"1262c492-ffef-4a63-95a8-a6002736b8c4\"",
  "gatewayManagerEtag": null,
  "id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit",
  "location": "westus",
  "name": "MyCircuit",
  "peerings": [],
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "serviceKey": "1d05cf70-1db5-419f-ad86-1ca62c3c125b",
  "serviceProviderNotes": null,
  "serviceProviderProperties": {
    "bandwidthInMbps": 200,
    "peeringLocation": "Silicon Valley",
    "serviceProviderName": "Equinix"
  },
  "serviceProviderProvisioningState": "Provisioned",
  "sku": {
    "family": "UnlimitedData",
    "name": "Standard_MeteredData",
    "tier": "Standard"
  },
  "tags": null,
  "type": "Microsoft.Network/expressRouteCircuits]
  ```

4. <span data-ttu-id="f4a6a-219">設定 Microsoft 對等互連 hello 循環。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-219">Configure Microsoft peering for hello circuit.</span></span> <span data-ttu-id="f4a6a-220">請確定您擁有 hello 下列資訊才能繼續。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-220">Make sure that you have hello following information before you proceed.</span></span>

  * <span data-ttu-id="f4a6a-221">/ 30 子網路 hello 主要連結。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-221">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="f4a6a-222">這必須是您所擁有且註冊在 RIR / IRR 中的有效公用 IPv4 首碼。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-222">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="f4a6a-223">/ 30 hello 次要連結的子網路。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-223">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="f4a6a-224">這必須是您所擁有且註冊在 RIR / IRR 中的有效公用 IPv4 首碼。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-224">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="f4a6a-225">有效的 VLAN ID tooestablish 此對等。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-225">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="f4a6a-226">請確認沒有其他對等互連中 hello 循環使用 hello 相同 VLAN id。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-226">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="f4a6a-227">對等的 AS 編號。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-227">AS number for peering.</span></span> <span data-ttu-id="f4a6a-228">您可以使用 2 位元組和 4 位元組 AS 編號。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-228">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="f4a6a-229">通告前置詞： 您必須提供清單的所有前置詞您計劃 tooadvertise 透過 hello BGP 工作階段。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-229">Advertised prefixes: You must provide a list of all prefixes you plan tooadvertise over hello BGP session.</span></span> <span data-ttu-id="f4a6a-230">只接受公用 IP 位址首碼。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-230">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="f4a6a-231">如果您計劃 toosend 一組前置詞，您可以傳送的逗號分隔清單。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-231">If you plan toosend a set of prefixes, you can send a comma-separated list.</span></span> <span data-ttu-id="f4a6a-232">這些前置詞必須是已註冊的 tooyou 在 RIR / IRR。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-232">These prefixes must be registered tooyou in an RIR / IRR.</span></span>
  * <span data-ttu-id="f4a6a-233">**選用-**客戶 ASN： 如果您不是數字的已註冊的 toohello 對等互連的廣告前置詞，您可以指定 hello 為其所註冊的數字 toowhich。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-233">**Optional -** Customer ASN: If you are advertising prefixes that are not registered toohello peering AS number, you can specify hello AS number toowhich they are registered.</span></span>
  * <span data-ttu-id="f4a6a-234">路由登錄名稱： 您可以指定 hello RIR / IRR 哪些 hello 做為數字，但前置詞會註冊。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-234">Routing Registry Name: You can specify hello RIR / IRR against which hello AS number and prefixes are registered.</span></span>
  * <span data-ttu-id="f4a6a-235">**選用-**如果您選擇其中一個 toouse 的 MD5 雜湊。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-235">**Optional -** An MD5 hash if you choose toouse one.</span></span>

   <span data-ttu-id="f4a6a-236">下列範例 tooconfigure Microsoft 對等互連您循環執行的 hello:</span><span class="sxs-lookup"><span data-stu-id="f4a6a-236">Run hello following example tooconfigure Microsoft peering for your circuit:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 123.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 123.0.0.4/30 --vlan-id 300 --peering-type MicrosoftPeering --advertised-public-prefixes 123.1.0.0/24
  ```

### <a name="tooget-microsoft-peering-details"></a><span data-ttu-id="f4a6a-237">tooget Microsoft 對等詳細資料</span><span class="sxs-lookup"><span data-stu-id="f4a6a-237">tooget Microsoft peering details</span></span>

<span data-ttu-id="f4a6a-238">您可以使用下列範例中的 hello，以取得設定的詳細資訊：</span><span class="sxs-lookup"><span data-stu-id="f4a6a-238">You can get configuration details by using hello following example:</span></span>

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzureMicrosoftPeering
```

<span data-ttu-id="f4a6a-239">hello 輸出是 toohello 類似下列範例程式碼：</span><span class="sxs-lookup"><span data-stu-id="f4a6a-239">hello output is similar toohello following example:</span></span>

```azurecli
{
  "azureAsn": 12076,
  "etag": "W/\"2e97be83-a684-4f29-bf3c-96191e270666\"",
  "gatewayManagerEtag": "18",
  "id": "/subscriptions/9a0c2943-e0c2-4608-876c-e0ddffd1211b/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/peerings/AzureMicrosoftPeering",
  "lastModifiedBy": "Customer",
  "microsoftPeeringConfig": {
    "advertisedPublicPrefixes": [
        ""
      ],
     "advertisedPublicPrefixesState": "",
     "customerASN": ,
     "routingRegistryName": ""
  }
  "name": "AzureMicrosoftPeering",
  "peerAsn": ,
  "peeringType": "AzureMicrosoftPeering",
  "primaryAzurePort": "",
  "primaryPeerAddressPrefix": "",
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "routeFilter": null,
  "secondaryAzurePort": "",
  "secondaryPeerAddressPrefix": "",
  "sharedKey": null,
  "state": "Enabled",
  "stats": null,
  "vlanId": 100
}
```

### <a name="tooupdate-microsoft-peering-configuration"></a><span data-ttu-id="f4a6a-240">tooupdate Microsoft 對等組態</span><span class="sxs-lookup"><span data-stu-id="f4a6a-240">tooupdate Microsoft peering configuration</span></span>

<span data-ttu-id="f4a6a-241">您可以更新 hello 設定的任何部分。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-241">You can update any part of hello configuration.</span></span> <span data-ttu-id="f4a6a-242">hello 公告 hello 循環的前置詞正在更新從 123.1.0.0/24 too124.1.0.0/24 hello 下列範例中：</span><span class="sxs-lookup"><span data-stu-id="f4a6a-242">hello advertised prefixes of hello circuit are being updated from 123.1.0.0/24 too124.1.0.0/24 in hello following example:</span></span>

```azurecli
az network express-route peering update --circuit-name MyCircuit -g ExpressRouteResourceGroup --peering-type MicrosoftPeering --advertised-public-prefixes 124.1.0.0/24
```

### <a name="toodelete-microsoft-peering"></a><span data-ttu-id="f4a6a-243">toodelete Microsoft 對等互連</span><span class="sxs-lookup"><span data-stu-id="f4a6a-243">toodelete Microsoft peering</span></span>

<span data-ttu-id="f4a6a-244">您可以執行下列範例中的 hello 來移除您對等的設定：</span><span class="sxs-lookup"><span data-stu-id="f4a6a-244">You can remove your peering configuration by running hello following example:</span></span>

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name MicrosoftPeering
```

## <a name="next-steps"></a><span data-ttu-id="f4a6a-245">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f4a6a-245">Next steps</span></span>

<span data-ttu-id="f4a6a-246">下一步，[連結 VNet tooan ExpressRoute 電路](howto-linkvnet-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-246">Next step, [Link a VNet tooan ExpressRoute circuit](howto-linkvnet-cli.md).</span></span>

* <span data-ttu-id="f4a6a-247">如需 ExpressRoute 工作流程的詳細資訊，請參閱 [ExpressRoute 工作流程](expressroute-workflows.md)。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-247">For more information about ExpressRoute workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="f4a6a-248">如需線路對等的詳細資訊，請參閱 [ExpressRoute 線路和路由網域](expressroute-circuit-peerings.md)。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-248">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>
* <span data-ttu-id="f4a6a-249">如需使用虛擬網路的詳細資訊，請參閱 [虛擬網路概觀](../virtual-network/virtual-networks-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="f4a6a-249">For more information about working with virtual networks, see [Virtual network overview](../virtual-network/virtual-networks-overview.md).</span></span>