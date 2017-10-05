---
title: "如何設定 Azure ExpressRoute 線路的路由：CLI | Microsoft Docs"
description: "本文將協助您為 ExpressRoute 線路建立和佈建私用、公用及 Microsoft 對等互連。 本文也示範如何檢查狀態、更新或刪除線路的對等。"
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
ms.openlocfilehash: fbf0bd9a139c22bbd63755f6df445f6596aaccc5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="create-and-modify-routing-for-an-expressroute-circuit-using-cli"></a><span data-ttu-id="3fa28-104">使用 CLI 來建立和修改 ExpressRoute 路線的路由</span><span class="sxs-lookup"><span data-stu-id="3fa28-104">Create and modify routing for an ExpressRoute circuit using CLI</span></span>

<span data-ttu-id="3fa28-105">本文將協助您使用 CLI，以 Resource Manager 部署模型建立和管理 ExpressRoute 線路的路由設定。</span><span class="sxs-lookup"><span data-stu-id="3fa28-105">This article helps you create and manage routing configuration for an ExpressRoute circuit in the Resource Manager deployment model using CLI.</span></span> <span data-ttu-id="3fa28-106">您還可以檢查狀態、更新或刪除和取消佈建 ExpressRoute 線路的對等互連。</span><span class="sxs-lookup"><span data-stu-id="3fa28-106">You can also check the status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span> <span data-ttu-id="3fa28-107">如果您想要對線路使用不同的方法，可選取下列清單中的文章：</span><span class="sxs-lookup"><span data-stu-id="3fa28-107">If you want to use a different method to work with your circuit, select an article from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="3fa28-108">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="3fa28-108">Azure portal</span></span>](expressroute-howto-routing-portal-resource-manager.md)
> * [<span data-ttu-id="3fa28-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3fa28-109">PowerShell</span></span>](expressroute-howto-routing-arm.md)
> * [<span data-ttu-id="3fa28-110">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="3fa28-110">Azure CLI</span></span>](howto-routing-cli.md)
> * [<span data-ttu-id="3fa28-111">視訊 - 私用對等互連</span><span class="sxs-lookup"><span data-stu-id="3fa28-111">Video - Private peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="3fa28-112">視訊 - 公用對等互連</span><span class="sxs-lookup"><span data-stu-id="3fa28-112">Video - Public peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="3fa28-113">視訊 - Microsoft 對等互連</span><span class="sxs-lookup"><span data-stu-id="3fa28-113">Video - Microsoft peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="3fa28-114">PowerShell (傳統)</span><span class="sxs-lookup"><span data-stu-id="3fa28-114">PowerShell (classic)</span></span>](expressroute-howto-routing-classic.md)
> 

## <a name="configuration-prerequisites"></a><span data-ttu-id="3fa28-115">組態必要條件</span><span class="sxs-lookup"><span data-stu-id="3fa28-115">Configuration prerequisites</span></span>

* <span data-ttu-id="3fa28-116">開始之前，請先安裝 CLI 命令的最新版本 (2.0 版或更新版本)。</span><span class="sxs-lookup"><span data-stu-id="3fa28-116">Before beginning, install the latest version of the CLI commands (2.0 or later).</span></span> <span data-ttu-id="3fa28-117">如需關於安裝 CLI 命令的資訊，請參閱[安裝 Azure CLI 2.0](/cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="3fa28-117">For information about installing the CLI commands, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span>
* <span data-ttu-id="3fa28-118">開始設定之前，請確定您已經檢閱過[必要條件](expressroute-prerequisites.md)、[路由需求](expressroute-routing.md)和[工作流程](expressroute-workflows.md)分頁。</span><span class="sxs-lookup"><span data-stu-id="3fa28-118">Make sure that you have reviewed the [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflow](expressroute-workflows.md) pages before you begin configuration.</span></span>
* <span data-ttu-id="3fa28-119">您必須擁有作用中的 ExpressRoute 線路。</span><span class="sxs-lookup"><span data-stu-id="3fa28-119">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="3fa28-120">繼續之前，請遵循指示來 [建立 ExpressRoute 線路](howto-circuit-cli.md) ，並由您的連線提供者來啟用該線路。</span><span class="sxs-lookup"><span data-stu-id="3fa28-120">Follow the instructions to [Create an ExpressRoute circuit](howto-circuit-cli.md) and have the circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="3fa28-121">ExpressRoute 線路必須處於已佈建和已啟用狀態，您才能執行本文中的命令。</span><span class="sxs-lookup"><span data-stu-id="3fa28-121">The ExpressRoute circuit must be in a provisioned and enabled state for you to be able to run the commands in this article.</span></span>

<span data-ttu-id="3fa28-122">這些指示只適用於由提供第 2 層連線服務的服務提供者所建立的線路。</span><span class="sxs-lookup"><span data-stu-id="3fa28-122">These instructions only apply to circuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="3fa28-123">如果您使用的服務提供者是提供受管理的第 3 層服務 (通常是 IPVPN，如 MPLS)，您的連線提供者會為您設定和管理路由。</span><span class="sxs-lookup"><span data-stu-id="3fa28-123">If you are using a service provider that offers managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>

<span data-ttu-id="3fa28-124">您可以為 ExpressRoute 線路設定一個、兩個或全部三個對等 (Azure 私用、Azure 公用和 Microsoft)。</span><span class="sxs-lookup"><span data-stu-id="3fa28-124">You can configure one, two, or all three peerings (Azure private, Azure public, and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="3fa28-125">您可以依自己選擇的任何順序設定對等。</span><span class="sxs-lookup"><span data-stu-id="3fa28-125">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="3fa28-126">不過，您必須確定一次只完成一個對等的設定。</span><span class="sxs-lookup"><span data-stu-id="3fa28-126">However, you must make sure that you complete the configuration of each peering one at a time.</span></span>

## <a name="azure-private-peering"></a><span data-ttu-id="3fa28-127">Azure 私用對等</span><span class="sxs-lookup"><span data-stu-id="3fa28-127">Azure private peering</span></span>

<span data-ttu-id="3fa28-128">本節將協助您為 ExpressRoute 線路建立、取得、更新和刪除 Azure 私用對等互連設定。</span><span class="sxs-lookup"><span data-stu-id="3fa28-128">This section helps you create, get, update, and delete the Azure private peering configuration for an ExpressRoute circuit.</span></span>

### <a name="to-create-azure-private-peering"></a><span data-ttu-id="3fa28-129">建立 Azure 私用對等</span><span class="sxs-lookup"><span data-stu-id="3fa28-129">To create Azure private peering</span></span>

1. <span data-ttu-id="3fa28-130">安裝最新版的 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="3fa28-130">Install the latest version of Azure CLI.</span></span> <span data-ttu-id="3fa28-131">您必須使用最新版本的 Azure 命令列介面 (CLI)。* 在開始設定之前，檢閱[必要條件](expressroute-prerequisites.md)和[工作流程](expressroute-workflows.md)。</span><span class="sxs-lookup"><span data-stu-id="3fa28-131">You must use the latest version of the Azure Command-line Interface (CLI).* Review the [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

  ```azurecli
  az login
  ```

  <span data-ttu-id="3fa28-132">選取您想要建立 ExpressRoute 線路的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="3fa28-132">Select the subscription you want to create ExpressRoute circuit</span></span>

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. <span data-ttu-id="3fa28-133">建立 ExpressRoute 線路。</span><span class="sxs-lookup"><span data-stu-id="3fa28-133">Create an ExpressRoute circuit.</span></span> <span data-ttu-id="3fa28-134">請遵循指示建立 [ExpressRoute 線路](howto-circuit-cli.md) ，並由連線提供者佈建它。</span><span class="sxs-lookup"><span data-stu-id="3fa28-134">Follow the instructions to create an [ExpressRoute circuit](howto-circuit-cli.md) and have it provisioned by the connectivity provider.</span></span>

  <span data-ttu-id="3fa28-135">如果您的連線提供者是提供受管理的第 3 層服務，您可以要求連線提供者為您啟用 Azure 私用對等。</span><span class="sxs-lookup"><span data-stu-id="3fa28-135">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider to enable Azure private peering for you.</span></span> <span data-ttu-id="3fa28-136">在此情況下，您不需要遵循後續幾節所列的指示。</span><span class="sxs-lookup"><span data-stu-id="3fa28-136">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="3fa28-137">不過，如果您的連線提供者不管理路由，請在建立線路之後繼續使用後續步驟進行設定。</span><span class="sxs-lookup"><span data-stu-id="3fa28-137">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using the next steps.</span></span>
3. <span data-ttu-id="3fa28-138">檢查 ExpressRoute 線路，以確定已佈建且已啟用線路。</span><span class="sxs-lookup"><span data-stu-id="3fa28-138">Check the ExpressRoute circuit to make sure it is provisioned and also enabled.</span></span> <span data-ttu-id="3fa28-139">請使用下列範例：</span><span class="sxs-lookup"><span data-stu-id="3fa28-139">Use the following example:</span></span>

  ```azurecli
  az network express-route show --resource-group ExpressRouteResourceGroup --name MyCircuit
  ```

  <span data-ttu-id="3fa28-140">回應如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="3fa28-140">The response is similar to the following example:</span></span>

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

4. <span data-ttu-id="3fa28-141">設定線路的 Azure 私用對等。</span><span class="sxs-lookup"><span data-stu-id="3fa28-141">Configure Azure private peering for the circuit.</span></span> <span data-ttu-id="3fa28-142">繼續執行接下來的步驟之前，請確定您有下列項目：</span><span class="sxs-lookup"><span data-stu-id="3fa28-142">Make sure that you have the following items before you proceed with the next steps:</span></span>

  * <span data-ttu-id="3fa28-143">主要連結的 /30 子網路。</span><span class="sxs-lookup"><span data-stu-id="3fa28-143">A /30 subnet for the primary link.</span></span> <span data-ttu-id="3fa28-144">子網路不能在保留給虛擬網路的任何位址空間中。</span><span class="sxs-lookup"><span data-stu-id="3fa28-144">The subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="3fa28-145">次要連結的 /30 子網路。</span><span class="sxs-lookup"><span data-stu-id="3fa28-145">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="3fa28-146">子網路不能在保留給虛擬網路的任何位址空間中。</span><span class="sxs-lookup"><span data-stu-id="3fa28-146">The subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="3fa28-147">供建立此對等的有效 VLAN ID。</span><span class="sxs-lookup"><span data-stu-id="3fa28-147">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="3fa28-148">請確定線路有沒有其他對等使用相同的 VLAN ID。</span><span class="sxs-lookup"><span data-stu-id="3fa28-148">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="3fa28-149">對等的 AS 編號。</span><span class="sxs-lookup"><span data-stu-id="3fa28-149">AS number for peering.</span></span> <span data-ttu-id="3fa28-150">您可以使用 2 位元組和 4 位元組 AS 編號。</span><span class="sxs-lookup"><span data-stu-id="3fa28-150">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="3fa28-151">您可以將私用 AS 編號用於此對等。</span><span class="sxs-lookup"><span data-stu-id="3fa28-151">You can use a private AS number for this peering.</span></span> <span data-ttu-id="3fa28-152">請確定您不是使用 65515。</span><span class="sxs-lookup"><span data-stu-id="3fa28-152">Ensure that you are not using 65515.</span></span>
  * <span data-ttu-id="3fa28-153">**選用：**MD5 雜湊 (如果選擇使用)。</span><span class="sxs-lookup"><span data-stu-id="3fa28-153">**Optional -** An MD5 hash if you choose to use one.</span></span>

  <span data-ttu-id="3fa28-154">使用下列範例來為線路設定 Azure 私用對等互連：</span><span class="sxs-lookup"><span data-stu-id="3fa28-154">Use the following example to configure Azure private peering for your circuit:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 10.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 10.0.0.4/30 --vlan-id 200 --peering-type AzurePrivatePeering
  ```

  <span data-ttu-id="3fa28-155">如果您選擇使用 MD5 雜湊，請使用下列範例：</span><span class="sxs-lookup"><span data-stu-id="3fa28-155">If you choose to use an MD5 hash, use the following example:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 10.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 10.0.0.4/30 --vlan-id 200 --peering-type AzurePrivatePeering --SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > <span data-ttu-id="3fa28-156">請確定您將 AS 編號指定為對等 ASN，而不是客戶 ASN。</span><span class="sxs-lookup"><span data-stu-id="3fa28-156">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>
  > 
  > 

### <a name="to-view-azure-private-peering-details"></a><span data-ttu-id="3fa28-157">檢視 Azure 私用對等詳細資訊</span><span class="sxs-lookup"><span data-stu-id="3fa28-157">To view Azure private peering details</span></span>

<span data-ttu-id="3fa28-158">您可以使用下列範例來取得設定詳細資料：</span><span class="sxs-lookup"><span data-stu-id="3fa28-158">You can get configuration details by using the following example:</span></span>

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

<span data-ttu-id="3fa28-159">輸出類似於下列範例：</span><span class="sxs-lookup"><span data-stu-id="3fa28-159">The output is similar to the following example:</span></span>

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

### <a name="to-update-azure-private-peering-configuration"></a><span data-ttu-id="3fa28-160">更新 Azure 私用對等組態</span><span class="sxs-lookup"><span data-stu-id="3fa28-160">To update Azure private peering configuration</span></span>

<span data-ttu-id="3fa28-161">您可以使用下列範例來更新設定的任何部分。</span><span class="sxs-lookup"><span data-stu-id="3fa28-161">You can update any part of the configuration using the following example.</span></span> <span data-ttu-id="3fa28-162">在此範例中，線路的 VLAN ID 從 100 更新為 500。</span><span class="sxs-lookup"><span data-stu-id="3fa28-162">In this example, the VLAN ID of the circuit is being updated from 100 to 500.</span></span>

```azurecli
az network express-route peering update --vlan-id 500 -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

### <a name="to-delete-azure-private-peering"></a><span data-ttu-id="3fa28-163">刪除 Azure 私用對等</span><span class="sxs-lookup"><span data-stu-id="3fa28-163">To delete Azure private peering</span></span>

<span data-ttu-id="3fa28-164">您可以執行下列範例來移除對等互連設定：</span><span class="sxs-lookup"><span data-stu-id="3fa28-164">You can remove your peering configuration by running the following example:</span></span>

> [!WARNING]
> <span data-ttu-id="3fa28-165">執行此範例之前，您必須確定所有虛擬網路都已經與 ExpressRoute 線路取消連結。</span><span class="sxs-lookup"><span data-stu-id="3fa28-165">You must ensure that all virtual networks are unlinked from the ExpressRoute circuit before running this example.</span></span> 
> 
> 

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

## <a name="azure-public-peering"></a><span data-ttu-id="3fa28-166">Azure 公用對等</span><span class="sxs-lookup"><span data-stu-id="3fa28-166">Azure public peering</span></span>

<span data-ttu-id="3fa28-167">本節將協助您為 ExpressRoute 線路建立、取得、更新和刪除 Azure 公用對等互連設定。</span><span class="sxs-lookup"><span data-stu-id="3fa28-167">This section helps you create, get, update, and delete the Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="to-create-azure-public-peering"></a><span data-ttu-id="3fa28-168">建立 Azure 公用對等</span><span class="sxs-lookup"><span data-stu-id="3fa28-168">To create Azure public peering</span></span>

1. <span data-ttu-id="3fa28-169">安裝最新版的 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="3fa28-169">Install the latest version of Azure CLI.</span></span> <span data-ttu-id="3fa28-170">您必須使用最新版本的 Azure 命令列介面 (CLI)。* 在開始設定之前，檢閱[必要條件](expressroute-prerequisites.md)和[工作流程](expressroute-workflows.md)。</span><span class="sxs-lookup"><span data-stu-id="3fa28-170">You must use the latest version of the Azure Command-line Interface (CLI).* Review the [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

  ```azurecli
  az login
  ```

  <span data-ttu-id="3fa28-171">選取您想要建立 ExpressRoute 線路的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="3fa28-171">Select the subscription for which you want to create ExpressRoute circuit.</span></span>

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. <span data-ttu-id="3fa28-172">建立 ExpressRoute 線路。</span><span class="sxs-lookup"><span data-stu-id="3fa28-172">Create an ExpressRoute circuit.</span></span>  <span data-ttu-id="3fa28-173">請遵循指示建立 [ExpressRoute 線路](howto-circuit-cli.md) ，並由連線提供者佈建它。</span><span class="sxs-lookup"><span data-stu-id="3fa28-173">Follow the instructions to create an [ExpressRoute circuit](howto-circuit-cli.md) and have it provisioned by the connectivity provider.</span></span>

  <span data-ttu-id="3fa28-174">如果您的連線提供者是提供受管理的第 3 層服務，您可以要求連線提供者為您啟用 Azure 私用對等互連。</span><span class="sxs-lookup"><span data-stu-id="3fa28-174">If your connectivity provider offers managed Layer 3 services, you can request that your connectivity provider enables Azure private peering for you.</span></span> <span data-ttu-id="3fa28-175">在此情況下，您不需要遵循後續幾節所列的指示。</span><span class="sxs-lookup"><span data-stu-id="3fa28-175">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="3fa28-176">不過，如果您的連線提供者不管理路由，請在建立線路之後繼續使用後續步驟進行設定。</span><span class="sxs-lookup"><span data-stu-id="3fa28-176">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using the next steps.</span></span>
3. <span data-ttu-id="3fa28-177">檢查 ExpressRoute 線路，以確定已佈建且已啟用線路。</span><span class="sxs-lookup"><span data-stu-id="3fa28-177">Check the ExpressRoute circuit to ensure it is provisioned and also enabled.</span></span> <span data-ttu-id="3fa28-178">請使用下列範例：</span><span class="sxs-lookup"><span data-stu-id="3fa28-178">Use the following example:</span></span>

  ```azurecli
  az network express-route list
  ```

  <span data-ttu-id="3fa28-179">回應如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="3fa28-179">The response is similar to the following example:</span></span>

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

4. <span data-ttu-id="3fa28-180">設定線路的 Azure 公用對等。</span><span class="sxs-lookup"><span data-stu-id="3fa28-180">Configure Azure public peering for the circuit.</span></span> <span data-ttu-id="3fa28-181">進一步執行之前，請確定您具有下列資訊。</span><span class="sxs-lookup"><span data-stu-id="3fa28-181">Make sure that you have the following information before you proceed further.</span></span>

  * <span data-ttu-id="3fa28-182">主要連結的 /30 子網路。</span><span class="sxs-lookup"><span data-stu-id="3fa28-182">A /30 subnet for the primary link.</span></span> <span data-ttu-id="3fa28-183">這必須是有效的公用 IPv4 首碼。</span><span class="sxs-lookup"><span data-stu-id="3fa28-183">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="3fa28-184">次要連結的 /30 子網路。</span><span class="sxs-lookup"><span data-stu-id="3fa28-184">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="3fa28-185">這必須是有效的公用 IPv4 首碼。</span><span class="sxs-lookup"><span data-stu-id="3fa28-185">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="3fa28-186">供建立此對等的有效 VLAN ID。</span><span class="sxs-lookup"><span data-stu-id="3fa28-186">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="3fa28-187">請確定線路有沒有其他對等使用相同的 VLAN ID。</span><span class="sxs-lookup"><span data-stu-id="3fa28-187">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="3fa28-188">對等的 AS 編號。</span><span class="sxs-lookup"><span data-stu-id="3fa28-188">AS number for peering.</span></span> <span data-ttu-id="3fa28-189">您可以使用 2 位元組和 4 位元組 AS 編號。</span><span class="sxs-lookup"><span data-stu-id="3fa28-189">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="3fa28-190">**選用 -** MD5 雜湊 (如果選擇使用)。</span><span class="sxs-lookup"><span data-stu-id="3fa28-190">**Optional -** An MD5 hash if you choose to use one.</span></span>

  <span data-ttu-id="3fa28-191">執行下列範例來為線路設定 Azure 公用對等互連：</span><span class="sxs-lookup"><span data-stu-id="3fa28-191">Run the following example to configure Azure public peering for your circuit:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 12.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 12.0.0.4/30 --vlan-id 200 --peering-type AzurePublicPeering
  ```

  <span data-ttu-id="3fa28-192">如果您選擇使用 MD5 雜湊，請使用下列範例：</span><span class="sxs-lookup"><span data-stu-id="3fa28-192">If you choose to use an MD5 hash, use the following example:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 12.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 12.0.0.4/30 --vlan-id 200 --peering-type AzurePublicPeering --SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > <span data-ttu-id="3fa28-193">請確定您將 AS 編號指定為對等 ASN，而不是客戶 ASN。</span><span class="sxs-lookup"><span data-stu-id="3fa28-193">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>

### <a name="to-view-azure-public-peering-details"></a><span data-ttu-id="3fa28-194">檢視 Azure 公用對等詳細資訊</span><span class="sxs-lookup"><span data-stu-id="3fa28-194">To view Azure public peering details</span></span>

<span data-ttu-id="3fa28-195">您可以使用下列範例來取得設定詳細資料：</span><span class="sxs-lookup"><span data-stu-id="3fa28-195">You can get configuration details using the following example:</span></span>

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

<span data-ttu-id="3fa28-196">輸出類似於下列範例：</span><span class="sxs-lookup"><span data-stu-id="3fa28-196">The output is similar to the following example:</span></span>

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

### <a name="to-update-azure-public-peering-configuration"></a><span data-ttu-id="3fa28-197">更新 Azure 公用對等組態</span><span class="sxs-lookup"><span data-stu-id="3fa28-197">To update Azure public peering configuration</span></span>

<span data-ttu-id="3fa28-198">您可以使用下列範例來更新設定的任何部分。</span><span class="sxs-lookup"><span data-stu-id="3fa28-198">You can update any part of the configuration using the following example.</span></span> <span data-ttu-id="3fa28-199">在此範例中，線路的 VLAN ID 從 200 更新為 600。</span><span class="sxs-lookup"><span data-stu-id="3fa28-199">In this example, the VLAN ID of the circuit is being updated from 200 to 600.</span></span>

```azurecli
az network express-route peering update --vlan-id 600 -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

### <a name="to-delete-azure-public-peering"></a><span data-ttu-id="3fa28-200">刪除 Azure 公用對等</span><span class="sxs-lookup"><span data-stu-id="3fa28-200">To delete Azure public peering</span></span>

<span data-ttu-id="3fa28-201">您可以執行下列範例來移除對等互連設定：</span><span class="sxs-lookup"><span data-stu-id="3fa28-201">You can remove your peering configuration by running the following example:</span></span>

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

## <a name="microsoft-peering"></a><span data-ttu-id="3fa28-202">Microsoft 對等互連</span><span class="sxs-lookup"><span data-stu-id="3fa28-202">Microsoft peering</span></span>

<span data-ttu-id="3fa28-203">本節將協助您為 ExpressRoute 線路建立、取得、更新和刪除 Microsoft 對等互連設定。</span><span class="sxs-lookup"><span data-stu-id="3fa28-203">This section helps you create, get, update, and delete the Microsoft peering configuration for an ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3fa28-204">在 2017 年 8 月 1 日以前設定之 ExpressRoute 線路的 Microsoft 對等互連，會透過 Microsoft 對等互連公告所有服務首碼，即使未定義路由篩選也一樣。</span><span class="sxs-lookup"><span data-stu-id="3fa28-204">Microsoft peering of ExpressRoute circuits that were configured prior to August 1, 2017 will have all service prefixes advertised through the Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="3fa28-205">在 2017 年 8 月 1 日當日或以後設定之 ExpressRoute 線路的 Microsoft 對等互連，不會公告任何首碼，直到路由篩選連結至線路為止。</span><span class="sxs-lookup"><span data-stu-id="3fa28-205">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached to the circuit.</span></span> <span data-ttu-id="3fa28-206">如需詳細資訊，請參閱[設定 Microsoft 對等互連的路由篩選](how-to-routefilter-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="3fa28-206">For more information, see [Configure a route filter for Microsoft peering](how-to-routefilter-powershell.md).</span></span>
> 
> 

### <a name="to-create-microsoft-peering"></a><span data-ttu-id="3fa28-207">建立 Microsoft 對等</span><span class="sxs-lookup"><span data-stu-id="3fa28-207">To create Microsoft peering</span></span>

1. <span data-ttu-id="3fa28-208">安裝最新版的 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="3fa28-208">Install the latest version of Azure CLI.</span></span> <span data-ttu-id="3fa28-209">使用最新版本的 Azure 命令列介面 (CLI)。* 在開始設定之前，檢閱[必要條件](expressroute-prerequisites.md)和[工作流程](expressroute-workflows.md)。</span><span class="sxs-lookup"><span data-stu-id="3fa28-209">Use the latest version of the Azure Command-line Interface (CLI).* Review the [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

  ```azurecli
  az login
  ```

  <span data-ttu-id="3fa28-210">選取您想要建立 ExpressRoute 線路的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="3fa28-210">Select the subscription for which you want to create ExpressRoute circuit.</span></span>

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. <span data-ttu-id="3fa28-211">建立 ExpressRoute 線路。</span><span class="sxs-lookup"><span data-stu-id="3fa28-211">Create an ExpressRoute circuit.</span></span> <span data-ttu-id="3fa28-212">請遵循指示建立 [ExpressRoute 線路](howto-circuit-cli.md) ，並由連線提供者佈建它。</span><span class="sxs-lookup"><span data-stu-id="3fa28-212">Follow the instructions to create an [ExpressRoute circuit](howto-circuit-cli.md) and have it provisioned by the connectivity provider.</span></span>

  <span data-ttu-id="3fa28-213">如果您的連線提供者是提供受管理的第 3 層服務，您可以要求連線提供者為您啟用 Azure 私用對等。</span><span class="sxs-lookup"><span data-stu-id="3fa28-213">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider to enable Azure private peering for you.</span></span> <span data-ttu-id="3fa28-214">在此情況下，您不需要遵循後續幾節所列的指示。</span><span class="sxs-lookup"><span data-stu-id="3fa28-214">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="3fa28-215">不過，如果您的連線提供者不管理路由，請在建立線路之後繼續使用後續步驟進行設定。</span><span class="sxs-lookup"><span data-stu-id="3fa28-215">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using the next steps.</span></span>

3. <span data-ttu-id="3fa28-216">檢查 ExpressRoute 線路，以確定已佈建且已啟用線路。</span><span class="sxs-lookup"><span data-stu-id="3fa28-216">Check the ExpressRoute circuit to make sure it is provisioned and also enabled.</span></span> <span data-ttu-id="3fa28-217">請使用下列範例：</span><span class="sxs-lookup"><span data-stu-id="3fa28-217">Use the following example:</span></span>

  ```azurecli
  az network express-route list
  ```

  <span data-ttu-id="3fa28-218">回應如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="3fa28-218">The response is similar to the following example:</span></span>

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

4. <span data-ttu-id="3fa28-219">設定線路的 Microsoft 對等。</span><span class="sxs-lookup"><span data-stu-id="3fa28-219">Configure Microsoft peering for the circuit.</span></span> <span data-ttu-id="3fa28-220">繼續之前，請確定您擁有下列資訊。</span><span class="sxs-lookup"><span data-stu-id="3fa28-220">Make sure that you have the following information before you proceed.</span></span>

  * <span data-ttu-id="3fa28-221">主要連結的 /30 子網路。</span><span class="sxs-lookup"><span data-stu-id="3fa28-221">A /30 subnet for the primary link.</span></span> <span data-ttu-id="3fa28-222">這必須是您所擁有且註冊在 RIR / IRR 中的有效公用 IPv4 首碼。</span><span class="sxs-lookup"><span data-stu-id="3fa28-222">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="3fa28-223">次要連結的 /30 子網路。</span><span class="sxs-lookup"><span data-stu-id="3fa28-223">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="3fa28-224">這必須是您所擁有且註冊在 RIR / IRR 中的有效公用 IPv4 首碼。</span><span class="sxs-lookup"><span data-stu-id="3fa28-224">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="3fa28-225">供建立此對等的有效 VLAN ID。</span><span class="sxs-lookup"><span data-stu-id="3fa28-225">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="3fa28-226">請確定線路有沒有其他對等使用相同的 VLAN ID。</span><span class="sxs-lookup"><span data-stu-id="3fa28-226">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="3fa28-227">對等的 AS 編號。</span><span class="sxs-lookup"><span data-stu-id="3fa28-227">AS number for peering.</span></span> <span data-ttu-id="3fa28-228">您可以使用 2 位元組和 4 位元組 AS 編號。</span><span class="sxs-lookup"><span data-stu-id="3fa28-228">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="3fa28-229">公告的首碼：您必須提供一份您打算在 BGP 工作階段上公告的所有首碼的清單。</span><span class="sxs-lookup"><span data-stu-id="3fa28-229">Advertised prefixes: You must provide a list of all prefixes you plan to advertise over the BGP session.</span></span> <span data-ttu-id="3fa28-230">只接受公用 IP 位址首碼。</span><span class="sxs-lookup"><span data-stu-id="3fa28-230">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="3fa28-231">如果計劃傳送一組首碼，可以傳送以逗號分隔的清單。</span><span class="sxs-lookup"><span data-stu-id="3fa28-231">If you plan to send a set of prefixes, you can send a comma-separated list.</span></span> <span data-ttu-id="3fa28-232">這些首碼必須在 RIR / IRR 中註冊給您。</span><span class="sxs-lookup"><span data-stu-id="3fa28-232">These prefixes must be registered to you in an RIR / IRR.</span></span>
  * <span data-ttu-id="3fa28-233">**選用：**客戶 ASN：如果您要公告的首碼未註冊給對等互連 AS 編號，則可以指定它們所註冊的 AS 編號。</span><span class="sxs-lookup"><span data-stu-id="3fa28-233">**Optional -** Customer ASN: If you are advertising prefixes that are not registered to the peering AS number, you can specify the AS number to which they are registered.</span></span>
  * <span data-ttu-id="3fa28-234">路由登錄名稱：您可以指定可供註冊 AS 編號和首碼的 RIR / IRR。</span><span class="sxs-lookup"><span data-stu-id="3fa28-234">Routing Registry Name: You can specify the RIR / IRR against which the AS number and prefixes are registered.</span></span>
  * <span data-ttu-id="3fa28-235">**選用 -** MD5 雜湊 (如果選擇使用)。</span><span class="sxs-lookup"><span data-stu-id="3fa28-235">**Optional -** An MD5 hash if you choose to use one.</span></span>

   <span data-ttu-id="3fa28-236">執行下列範例來為線路設定 Microsoft 對等互連：</span><span class="sxs-lookup"><span data-stu-id="3fa28-236">Run the following example to configure Microsoft peering for your circuit:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 123.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 123.0.0.4/30 --vlan-id 300 --peering-type MicrosoftPeering --advertised-public-prefixes 123.1.0.0/24
  ```

### <a name="to-get-microsoft-peering-details"></a><span data-ttu-id="3fa28-237">取得 Microsoft 對等詳細資料</span><span class="sxs-lookup"><span data-stu-id="3fa28-237">To get Microsoft peering details</span></span>

<span data-ttu-id="3fa28-238">您可以使用下列範例來取得設定詳細資料：</span><span class="sxs-lookup"><span data-stu-id="3fa28-238">You can get configuration details by using the following example:</span></span>

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzureMicrosoftPeering
```

<span data-ttu-id="3fa28-239">輸出類似於下列範例：</span><span class="sxs-lookup"><span data-stu-id="3fa28-239">The output is similar to the following example:</span></span>

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

### <a name="to-update-microsoft-peering-configuration"></a><span data-ttu-id="3fa28-240">更新 Microsoft 對等組態</span><span class="sxs-lookup"><span data-stu-id="3fa28-240">To update Microsoft peering configuration</span></span>

<span data-ttu-id="3fa28-241">您可以更新設定的任何部分。</span><span class="sxs-lookup"><span data-stu-id="3fa28-241">You can update any part of the configuration.</span></span> <span data-ttu-id="3fa28-242">在下列範例中，已公告之線路的前置詞從 123.1.0.0/24 更新為 124.1.0.0/24：</span><span class="sxs-lookup"><span data-stu-id="3fa28-242">The advertised prefixes of the circuit are being updated from 123.1.0.0/24 to 124.1.0.0/24 in the following example:</span></span>

```azurecli
az network express-route peering update --circuit-name MyCircuit -g ExpressRouteResourceGroup --peering-type MicrosoftPeering --advertised-public-prefixes 124.1.0.0/24
```

### <a name="to-delete-microsoft-peering"></a><span data-ttu-id="3fa28-243">刪除 Microsoft 對等</span><span class="sxs-lookup"><span data-stu-id="3fa28-243">To delete Microsoft peering</span></span>

<span data-ttu-id="3fa28-244">您可以執行下列範例來移除對等互連設定：</span><span class="sxs-lookup"><span data-stu-id="3fa28-244">You can remove your peering configuration by running the following example:</span></span>

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name MicrosoftPeering
```

## <a name="next-steps"></a><span data-ttu-id="3fa28-245">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3fa28-245">Next steps</span></span>

<span data-ttu-id="3fa28-246">下一步， [將 VNet 連結到 ExpressRoute 線路](howto-linkvnet-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="3fa28-246">Next step, [Link a VNet to an ExpressRoute circuit](howto-linkvnet-cli.md).</span></span>

* <span data-ttu-id="3fa28-247">如需 ExpressRoute 工作流程的詳細資訊，請參閱 [ExpressRoute 工作流程](expressroute-workflows.md)。</span><span class="sxs-lookup"><span data-stu-id="3fa28-247">For more information about ExpressRoute workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="3fa28-248">如需線路對等的詳細資訊，請參閱 [ExpressRoute 線路和路由網域](expressroute-circuit-peerings.md)。</span><span class="sxs-lookup"><span data-stu-id="3fa28-248">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>
* <span data-ttu-id="3fa28-249">如需使用虛擬網路的詳細資訊，請參閱 [虛擬網路概觀](../virtual-network/virtual-networks-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="3fa28-249">For more information about working with virtual networks, see [Virtual network overview](../virtual-network/virtual-networks-overview.md).</span></span>