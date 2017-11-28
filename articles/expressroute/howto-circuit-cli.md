---
title: "建立與修改 Azure ExpressRoute 線路：CLI | Microsoft Docs"
description: "本文說明如何 toocreate，佈建、 驗證、 更新、 刪除和取消佈建使用 CLI 的 ExpressRoute 電路。"
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
ms.date: 07/25/2017
ms.author: anzaman;cherylmc
ms.openlocfilehash: 396e325658a59afadb209bb525cbb59ac775ae6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-cli"></a><span data-ttu-id="d58c7-103">使用 CLI 建立和修改 ExpressRoute 線路</span><span class="sxs-lookup"><span data-stu-id="d58c7-103">Create and modify an ExpressRoute circuit using CLI</span></span>


<span data-ttu-id="d58c7-104">本文說明如何使用 Azure ExpressRoute 電路 toocreate hello 命令列介面 (CLI)。</span><span class="sxs-lookup"><span data-stu-id="d58c7-104">This article describes how toocreate an Azure ExpressRoute circuit by using hello Command Line Interface (CLI).</span></span> <span data-ttu-id="d58c7-105">本文也會顯示 toocheck hello 狀態如何更新或刪除和取消佈建電路。</span><span class="sxs-lookup"><span data-stu-id="d58c7-105">This article also shows you how toocheck hello status, update, or delete and deprovision a circuit.</span></span> <span data-ttu-id="d58c7-106">如果您想 toouse ExpressRoute 電路以不同的方法 toowork，您可以從下列清單中的 hello 選取 hello 發行項：</span><span class="sxs-lookup"><span data-stu-id="d58c7-106">If you want toouse a different method toowork with ExpressRoute circuits, you can select hello article from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="d58c7-107">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="d58c7-107">Azure portal</span></span>](expressroute-howto-circuit-portal-resource-manager.md)
> * [<span data-ttu-id="d58c7-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d58c7-108">PowerShell</span></span>](expressroute-howto-circuit-arm.md)
> * [<span data-ttu-id="d58c7-109">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d58c7-109">Azure CLI</span></span>](howto-circuit-cli.md)
> * [<span data-ttu-id="d58c7-110">影片 - Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="d58c7-110">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [<span data-ttu-id="d58c7-111">PowerShell (傳統)</span><span class="sxs-lookup"><span data-stu-id="d58c7-111">PowerShell (classic)</span></span>](expressroute-howto-circuit-classic.md)
> 

## <a name="before-you-begin"></a><span data-ttu-id="d58c7-112">開始之前</span><span class="sxs-lookup"><span data-stu-id="d58c7-112">Before you begin</span></span>

* <span data-ttu-id="d58c7-113">在開始之前，安裝 hello 最新版本 （2.0 或更新版本） 的 hello CLI 命令。</span><span class="sxs-lookup"><span data-stu-id="d58c7-113">Before beginning, install hello latest version of hello CLI commands (2.0 or later).</span></span> <span data-ttu-id="d58c7-114">如需安裝 hello CLI 命令的資訊，請參閱[安裝 Azure CLI 2.0](/cli/azure/install-azure-cli)和[開始使用 Azure CLI 2.0](/cli/azure/get-started-with-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="d58c7-114">For information about installing hello CLI commands, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli) and [Get Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).</span></span>
* <span data-ttu-id="d58c7-115">檢閱 hello[必要條件](expressroute-prerequisites.md)和[工作流程](expressroute-workflows.md)開始設定之前。</span><span class="sxs-lookup"><span data-stu-id="d58c7-115">Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

## <a name="create-and-provision-an-expressroute-circuit"></a><span data-ttu-id="d58c7-116">建立和佈建 ExpressRoute 線路</span><span class="sxs-lookup"><span data-stu-id="d58c7-116">Create and provision an ExpressRoute circuit</span></span>

### <a name="1-sign-in-tooyour-azure-account-and-select-your-subscription"></a><span data-ttu-id="d58c7-117">1.登入 tooyour Azure 帳戶並選取您的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="d58c7-117">1. Sign in tooyour Azure account and select your subscription</span></span>

<span data-ttu-id="d58c7-118">toobegin 您的設定，登入 tooyour Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="d58c7-118">toobegin your configuration, sign in tooyour Azure account.</span></span> <span data-ttu-id="d58c7-119">使用下列範例 toohelp 您連接的 hello:</span><span class="sxs-lookup"><span data-stu-id="d58c7-119">Use hello following examples toohelp you connect:</span></span>

```azurecli
az login
```

<span data-ttu-id="d58c7-120">請檢查 hello hello 帳戶的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d58c7-120">Check hello subscriptions for hello account.</span></span>

```azurecli
az account list
```

<span data-ttu-id="d58c7-121">選取您想要的 toocreate ExpressRoute 電路的 hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d58c7-121">Select hello subscription for which you want toocreate an ExpressRoute circuit.</span></span>

```azurecli
az account set --subscription "<subscription ID>"
```

### <a name="2-get-hello-list-of-supported-providers-locations-and-bandwidths"></a><span data-ttu-id="d58c7-122">2.取得支援的提供者、 位置及頻寬 hello 清單</span><span class="sxs-lookup"><span data-stu-id="d58c7-122">2. Get hello list of supported providers, locations, and bandwidths</span></span>

<span data-ttu-id="d58c7-123">建立 ExpressRoute 電路之前，您需要支援的連線提供者、 位置及頻寬選項的 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="d58c7-123">Before you create an ExpressRoute circuit, you need hello list of supported connectivity providers, locations, and bandwidth options.</span></span> <span data-ttu-id="d58c7-124">hello CLI 命令 'az 網路快速路由清單-服務-提供者' 會傳回此資訊，您將在稍後步驟中使用：</span><span class="sxs-lookup"><span data-stu-id="d58c7-124">hello CLI command 'az network express-route list-service-providers' returns this information, which you’ll use in later steps:</span></span>

```azurecli
az network express-route list-service-providers
```

<span data-ttu-id="d58c7-125">hello 回應是類似 toohello 下列範例：</span><span class="sxs-lookup"><span data-stu-id="d58c7-125">hello response is similar toohello following example:</span></span>

```azurecli
[
  {
    "bandwidthsOffered": [
      {
        "offerName": "50Mbps",
        "valueInMbps": 50
      },
      {
        "offerName": "100Mbps",
        "valueInMbps": 100
      },
      {
        "offerName": "200Mbps",
        "valueInMbps": 200
      },
      {
        "offerName": "500Mbps",
        "valueInMbps": 500
      },
      {
        "offerName": "1Gbps",
        "valueInMbps": 1000
      },
      {
        "offerName": "2Gbps",
        "valueInMbps": 2000
      },
      {
        "offerName": "5Gbps",
        "valueInMbps": 5000
      },
      {
        "offerName": "10Gbps",
        "valueInMbps": 10000
      }
    ],
    "id": "/subscriptions//resourceGroups//providers/Microsoft.Network/expressRouteServiceProviders/",
    "location": null,
    "name": "AARNet",
    "peeringLocations": [
      "Melbourne",
      "Sydney"
    ],
    "provisioningState": "Succeeded",
    "resourceGroup": "",
    "tags": null,
    "type": "Microsoft.Network/expressRouteServiceProviders"
  },
```

<span data-ttu-id="d58c7-126">如果您連線服務提供者會列出，請檢查 hello 回應 toosee。</span><span class="sxs-lookup"><span data-stu-id="d58c7-126">Check hello response toosee if your connectivity provider is listed.</span></span> <span data-ttu-id="d58c7-127">請記下的下列資訊，建立電路時，您需要的 hello:</span><span class="sxs-lookup"><span data-stu-id="d58c7-127">Make a note of hello following information, which you will need when you create a circuit:</span></span>

* <span data-ttu-id="d58c7-128">名稱</span><span class="sxs-lookup"><span data-stu-id="d58c7-128">Name</span></span>
* <span data-ttu-id="d58c7-129">PeeringLocations</span><span class="sxs-lookup"><span data-stu-id="d58c7-129">PeeringLocations</span></span>
* <span data-ttu-id="d58c7-130">BandwidthsOffered</span><span class="sxs-lookup"><span data-stu-id="d58c7-130">BandwidthsOffered</span></span>

<span data-ttu-id="d58c7-131">您現在準備好 toocreate ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="d58c7-131">You're now ready toocreate an ExpressRoute circuit.</span></span>

### <a name="3-create-an-expressroute-circuit"></a><span data-ttu-id="d58c7-132">3.建立 ExpressRoute 線路</span><span class="sxs-lookup"><span data-stu-id="d58c7-132">3. Create an ExpressRoute circuit</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d58c7-133">ExpressRoute 電路計費 hello 發出服務金鑰的時間。</span><span class="sxs-lookup"><span data-stu-id="d58c7-133">Your ExpressRoute circuit is billed from hello moment a service key is issued.</span></span> <span data-ttu-id="d58c7-134">準備好 tooprovision hello 電路 hello 連線服務提供者時，請執行此作業。</span><span class="sxs-lookup"><span data-stu-id="d58c7-134">Perform this operation when hello connectivity provider is ready tooprovision hello circuit.</span></span>
> 
> 

<span data-ttu-id="d58c7-135">若您還沒有資源群組，您必須在建立 ExpressRoute 線路之前建立一個。</span><span class="sxs-lookup"><span data-stu-id="d58c7-135">If you don't already have a resource group, you must create one before you create your ExpressRoute circuit.</span></span> <span data-ttu-id="d58c7-136">您可以建立資源群組執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="d58c7-136">You can create a resource group by running hello following command:</span></span>

```azurecli
az group create -n ExpressRouteResourceGroup -l "West US"
```

<span data-ttu-id="d58c7-137">hello 下列範例示範透過在美國矽谷 Equinix toocreate 200 Mbps ExpressRoute 電路的方式。</span><span class="sxs-lookup"><span data-stu-id="d58c7-137">hello following example shows how toocreate a 200-Mbps ExpressRoute circuit through Equinix in Silicon Valley.</span></span> <span data-ttu-id="d58c7-138">如果您使用不同的提供者和不同的設定，請在您提出要求時替換成該資訊。</span><span class="sxs-lookup"><span data-stu-id="d58c7-138">If you're using a different provider and different settings, substitute that information when you make your request.</span></span> 

<span data-ttu-id="d58c7-139">請確定您指定正確 SKU 層 hello 和 SKU 系列：</span><span class="sxs-lookup"><span data-stu-id="d58c7-139">Make sure that you specify hello correct SKU tier and SKU family:</span></span>

* <span data-ttu-id="d58c7-140">SKU 層會判斷 ExpressRoute 標準或 ExpressRoute 高階附加元件是否啟用。</span><span class="sxs-lookup"><span data-stu-id="d58c7-140">SKU tier determines whether an ExpressRoute standard or an ExpressRoute premium add-on is enabled.</span></span> <span data-ttu-id="d58c7-141">您可以指定 'Standard' tooget hello 標準 SKU 或 「 高階 」 hello premium 附加元件。</span><span class="sxs-lookup"><span data-stu-id="d58c7-141">You can specify 'Standard' tooget hello standard SKU or 'Premium' for hello premium add-on.</span></span>
* <span data-ttu-id="d58c7-142">SKU 系列決定 hello 計費的型別。</span><span class="sxs-lookup"><span data-stu-id="d58c7-142">SKU family determines hello billing type.</span></span> <span data-ttu-id="d58c7-143">您可以指定 [Metereddata] 以採用計量付費數據傳輸方案，選取 [Unlimiteddata] 以採用無限行動數據方案。</span><span class="sxs-lookup"><span data-stu-id="d58c7-143">You can specify 'Metereddata' for a metered data plan and 'Unlimiteddata' for an unlimited data plan.</span></span> <span data-ttu-id="d58c7-144">您可以變更從 'Metereddata 'too'Unlimiteddata'，但您無法變更 hello 類型從 'Unlimiteddata' too'Metereddata' hello 計費的型別。</span><span class="sxs-lookup"><span data-stu-id="d58c7-144">You can change hello billing type from 'Metereddata' too'Unlimiteddata', but you can't change hello type from 'Unlimiteddata' too'Metereddata'.</span></span>


<span data-ttu-id="d58c7-145">ExpressRoute 電路計費 hello 發出服務金鑰的時間。</span><span class="sxs-lookup"><span data-stu-id="d58c7-145">Your ExpressRoute circuit is billed from hello moment a service key is issued.</span></span> <span data-ttu-id="d58c7-146">下列範例中的 hello 是新的服務金鑰的要求：</span><span class="sxs-lookup"><span data-stu-id="d58c7-146">hello following example is a request for a new service key:</span></span>

```azurecli
az network express-route create --bandwidth 200 -n MyCircuit --peering-location "Silicon Valley" -g ExpressRouteResourceGroup --provider "Equinix" -l "West US" --sku-family MeteredData --sku-tier Standard
```

<span data-ttu-id="d58c7-147">hello 回應包含 hello 服務金鑰。</span><span class="sxs-lookup"><span data-stu-id="d58c7-147">hello response contains hello service key.</span></span>

### <a name="4-list-all-expressroute-circuits"></a><span data-ttu-id="d58c7-148">4.列出所有 ExpressRoute 循環</span><span class="sxs-lookup"><span data-stu-id="d58c7-148">4. List all ExpressRoute circuits</span></span>

<span data-ttu-id="d58c7-149">一份您所建立的所有 hello ExpressRoute 電路 tooget 執行 hello 'az 網路快速路由清單' 命令。</span><span class="sxs-lookup"><span data-stu-id="d58c7-149">tooget a list of all hello ExpressRoute circuits that you created, run hello 'az network express-route list' command.</span></span> <span data-ttu-id="d58c7-150">您隨時可以使用此命令來擷取此資訊。</span><span class="sxs-lookup"><span data-stu-id="d58c7-150">You can retrieve this information at any time by using this command.</span></span> <span data-ttu-id="d58c7-151">toolist 的所有電路，都請呼叫不含任何參數的 hello。</span><span class="sxs-lookup"><span data-stu-id="d58c7-151">toolist all circuits, make hello call with no parameters.</span></span>

```azurecli
az network express-route list
```

<span data-ttu-id="d58c7-152">您的服務金鑰已列在 hello *ServiceKey* hello 回應的欄位。</span><span class="sxs-lookup"><span data-stu-id="d58c7-152">Your service key is listed in hello *ServiceKey* field of hello response.</span></span>

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
"serviceProviderProvisioningState": "NotProvisioned",
"sku": {
  "family": "UnlimitedData",
  "name": "Standard_MeteredData",
  "tier": "Standard"
},
"tags": null,
"type": "Microsoft.Network/expressRouteCircuits]
```

<span data-ttu-id="d58c7-153">您可以使用 hello 執行 hello 命令來取得詳細的描述了所有 hello 參數 '-h' 參數。</span><span class="sxs-lookup"><span data-stu-id="d58c7-153">You can get detailed descriptions of all hello parameters by running hello command using hello '-h' parameter.</span></span>

```azurecli
az network express-route list -h
```

### <a name="5-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a><span data-ttu-id="d58c7-154">5.佈建傳送嗨服務金鑰 tooyour 連線服務提供者</span><span class="sxs-lookup"><span data-stu-id="d58c7-154">5. Send hello service key tooyour connectivity provider for provisioning</span></span>

<span data-ttu-id="d58c7-155">'ServiceProviderProvisioningState' 提供 hello 的佈建 hello 服務提供者端的目前狀態相關資訊。</span><span class="sxs-lookup"><span data-stu-id="d58c7-155">'ServiceProviderProvisioningState' provides information about hello current state of provisioning on hello service-provider side.</span></span> <span data-ttu-id="d58c7-156">hello 狀態提供 hello Microsoft 戶端 hello 狀態。</span><span class="sxs-lookup"><span data-stu-id="d58c7-156">hello status provides hello state on hello Microsoft side.</span></span> <span data-ttu-id="d58c7-157">如需詳細資訊，請參閱 hello[工作流程發行項](expressroute-workflows.md#expressroute-circuit-provisioning-states)。</span><span class="sxs-lookup"><span data-stu-id="d58c7-157">For more information, see hello [Workflows article](expressroute-workflows.md#expressroute-circuit-provisioning-states).</span></span>

<span data-ttu-id="d58c7-158">當您建立新的 ExpressRoute 電路時，hello 循環就會處於下列狀態的 hello:</span><span class="sxs-lookup"><span data-stu-id="d58c7-158">When you create a new ExpressRoute circuit, hello circuit is in hello following state:</span></span>

```azurecli
"serviceProviderProvisioningState": "NotProvisioned"
"circuitProvisioningState": "Enabled"
```

<span data-ttu-id="d58c7-159">hello 電路變更 toohello hello 連線服務提供者會在您啟用的 hello 程序中時，下列狀態：</span><span class="sxs-lookup"><span data-stu-id="d58c7-159">hello circuit changes toohello following state when hello connectivity provider is in hello process of enabling it for you:</span></span>

```azurecli
"serviceProviderProvisioningState": "Provisioning"
"circuitProvisioningState": "Enabled"
```

<span data-ttu-id="d58c7-160">您 toobe 無法 toouse ExpressRoute 電路，它必須處於下列狀態的 hello:</span><span class="sxs-lookup"><span data-stu-id="d58c7-160">For you toobe able toouse an ExpressRoute circuit, it must be in hello following state:</span></span>

```azurecli
"serviceProviderProvisioningState": "Provisioned"
"circuitProvisioningState": "Enabled
```

### <a name="6-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a><span data-ttu-id="d58c7-161">6.定期檢查 hello 狀態和 hello 循環索引鍵 hello 狀態</span><span class="sxs-lookup"><span data-stu-id="d58c7-161">6. Periodically check hello status and hello state of hello circuit key</span></span>

<span data-ttu-id="d58c7-162">檢查 hello 狀態和 hello 循環索引鍵 hello 狀態，可讓您了解您的提供者已啟用您的循環時間。</span><span class="sxs-lookup"><span data-stu-id="d58c7-162">Checking hello status and hello state of hello circuit key lets you know when your provider has enabled your circuit.</span></span> <span data-ttu-id="d58c7-163">設定 hello 循環之後，'ServiceProviderProvisioningState' 會顯示為 已佈建' hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="d58c7-163">After hello circuit has been configured, 'ServiceProviderProvisioningState' appears as 'Provisioned', as shown in hello following example:</span></span>

```azurecli
az network express-route show --resource-group ExpressRouteResourceGroup --name MyCircuit
```

<span data-ttu-id="d58c7-164">hello 回應是類似 toohello 下列範例：</span><span class="sxs-lookup"><span data-stu-id="d58c7-164">hello response is similar toohello following example:</span></span>

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
"serviceProviderProvisioningState": "NotProvisioned",
"sku": {
  "family": "UnlimitedData",
  "name": "Standard_MeteredData",
  "tier": "Standard"
},
"tags": null,
"type": "Microsoft.Network/expressRouteCircuits]
```

### <a name="7-create-your-routing-configuration"></a><span data-ttu-id="d58c7-165">7.建立路由組態</span><span class="sxs-lookup"><span data-stu-id="d58c7-165">7. Create your routing configuration</span></span>

<span data-ttu-id="d58c7-166">如需逐步指示，請參閱 hello [ExpressRoute 電路的路由組態](howto-routing-cli.md)文章 toocreate 和修改循環的對等互連。</span><span class="sxs-lookup"><span data-stu-id="d58c7-166">For step-by-step instructions, see hello [ExpressRoute circuit routing configuration](howto-routing-cli.md) article toocreate and modify circuit peerings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d58c7-167">這些說明僅適用於 toocircuits 與提供層級 2 連線服務的服務提供者所建立。</span><span class="sxs-lookup"><span data-stu-id="d58c7-167">These instructions only apply toocircuits that are created with service providers that offer layer 2 connectivity services.</span></span> <span data-ttu-id="d58c7-168">如果您使用的服務提供者是提供受管理的第 3 層服務 (通常是 IP VPN，如 MPLS)，您的連線提供者會為您設定和管理路由。</span><span class="sxs-lookup"><span data-stu-id="d58c7-168">If you're using a service provider that offers managed layer 3 services (typically an IP VPN, like MPLS), your connectivity provider configures and manages routing for you.</span></span>
> 
> 

### <a name="8-link-a-virtual-network-tooan-expressroute-circuit"></a><span data-ttu-id="d58c7-169">8.連結虛擬網路 tooan ExpressRoute 電路</span><span class="sxs-lookup"><span data-stu-id="d58c7-169">8. Link a virtual network tooan ExpressRoute circuit</span></span>

<span data-ttu-id="d58c7-170">接下來，將虛擬網路 tooyour ExpressRoute 電路的連結。</span><span class="sxs-lookup"><span data-stu-id="d58c7-170">Next, link a virtual network tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="d58c7-171">使用 hello[連結虛擬網路 tooExpressRoute 電路](howto-linkvnet-cli.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="d58c7-171">Use hello [Linking virtual networks tooExpressRoute circuits](howto-linkvnet-cli.md) article.</span></span>

## <span data-ttu-id="d58c7-172"><a name="modify"></a>修改 ExpressRoute 線路</span><span class="sxs-lookup"><span data-stu-id="d58c7-172"><a name="modify"></a>Modifying an ExpressRoute circuit</span></span>

<span data-ttu-id="d58c7-173">您可以修改 ExpressRoute 線路的某些屬性，而不會影響連線。</span><span class="sxs-lookup"><span data-stu-id="d58c7-173">You can modify certain properties of an ExpressRoute circuit without impacting connectivity.</span></span> <span data-ttu-id="d58c7-174">您可以進行下列變更，不需停機的 hello:</span><span class="sxs-lookup"><span data-stu-id="d58c7-174">You can make hello following changes with no downtime:</span></span>

* <span data-ttu-id="d58c7-175">您可以啟用或停用 ExpressRoute 線路的 ExpressRoute 進階附加元件。</span><span class="sxs-lookup"><span data-stu-id="d58c7-175">You can enable or disable an ExpressRoute premium add-on for your ExpressRoute circuit.</span></span>
* <span data-ttu-id="d58c7-176">前提是有容量可用 hello 連接埠上，您可以增加 hello 頻寬的 ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="d58c7-176">You can increase hello bandwidth of your ExpressRoute circuit provided there is capacity available on hello port.</span></span> <span data-ttu-id="d58c7-177">不過，不支援降級 hello 電路頻寬。</span><span class="sxs-lookup"><span data-stu-id="d58c7-177">However, downgrading hello bandwidth of a circuit is not supported.</span></span> 
* <span data-ttu-id="d58c7-178">您可以將計量資料 tooUnlimited 資料變更 hello 計量計劃。</span><span class="sxs-lookup"><span data-stu-id="d58c7-178">You can change hello metering plan from Metered Data tooUnlimited Data.</span></span> <span data-ttu-id="d58c7-179">不過，變更 hello 計量不受限制的資料 tooMetered 不支援資料從計劃。</span><span class="sxs-lookup"><span data-stu-id="d58c7-179">However, changing hello metering plan from Unlimited Data tooMetered Data is not supported.</span></span>
* <span data-ttu-id="d58c7-180">您可以啟用和停用 [允許傳統作業]。</span><span class="sxs-lookup"><span data-stu-id="d58c7-180">You can enable and disable *Allow Classic Operations*.</span></span>

<span data-ttu-id="d58c7-181">如需有關限制和限制的詳細資訊，請參閱 hello [ExpressRoute 常見問題集](expressroute-faqs.md)。</span><span class="sxs-lookup"><span data-stu-id="d58c7-181">For more information on limits and limitations, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

### <a name="tooenable-hello-expressroute-premium-add-on"></a><span data-ttu-id="d58c7-182">tooenable hello ExpressRoute 高階的附加元件</span><span class="sxs-lookup"><span data-stu-id="d58c7-182">tooenable hello ExpressRoute premium add-on</span></span>

<span data-ttu-id="d58c7-183">您可以使用下列命令的 hello，為您現有的電路啟用 hello ExpressRoute premium add-on:</span><span class="sxs-lookup"><span data-stu-id="d58c7-183">You can enable hello ExpressRoute premium add-on for your existing circuit by using hello following command:</span></span>

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-tier Premium
```

<span data-ttu-id="d58c7-184">現在，hello expressroute 電路都已啟用 hello ExpressRoute premium 附加元件功能。</span><span class="sxs-lookup"><span data-stu-id="d58c7-184">hello circuit now has hello ExpressRoute premium add-on features enabled.</span></span> <span data-ttu-id="d58c7-185">我們開始 hello 命令已順利執行完成後，只要您計費 hello premium 附加元件的功能。</span><span class="sxs-lookup"><span data-stu-id="d58c7-185">We begin billing you for hello premium add-on capability as soon as hello command has successfully run.</span></span>

### <a name="toodisable-hello-expressroute-premium-add-on"></a><span data-ttu-id="d58c7-186">toodisable hello ExpressRoute 高階的附加元件</span><span class="sxs-lookup"><span data-stu-id="d58c7-186">toodisable hello ExpressRoute premium add-on</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d58c7-187">如果您使用大於 hello 標準循環所允許的資源，這項作業可能會失敗。</span><span class="sxs-lookup"><span data-stu-id="d58c7-187">This operation can fail if you're using resources that are greater than what is permitted for hello standard circuit.</span></span>
> 
> 

<span data-ttu-id="d58c7-188">停用之前 hello ExpressRoute premium add-on，了解 hello 下列準則：</span><span class="sxs-lookup"><span data-stu-id="d58c7-188">Before disabling hello ExpressRoute premium add-on, understand hello following criteria:</span></span>

* <span data-ttu-id="d58c7-189">您從 premium toostandard 降級之前，您必須確定您擁有少於 10 個虛擬網路連結的 toohello 循環。</span><span class="sxs-lookup"><span data-stu-id="d58c7-189">Before you downgrade from premium toostandard, you must make sure that you have fewer than 10 virtual networks linked toohello circuit.</span></span> <span data-ttu-id="d58c7-190">如果數目大於 10，更新要求就會失敗，且我們會以進階費率計費。</span><span class="sxs-lookup"><span data-stu-id="d58c7-190">If you have more than 10, your update request fails, and we bill you at premium rates.</span></span>
* <span data-ttu-id="d58c7-191">您必須取消連結其他地理政治區域中的所有虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="d58c7-191">You must unlink all virtual networks in other geopolitical regions.</span></span> <span data-ttu-id="d58c7-192">如果您未將所有虛擬網路取消連結，更新要求就會失敗，且我們會以進階費率計費。</span><span class="sxs-lookup"><span data-stu-id="d58c7-192">If you don't unlink all your virtual networks, your update request fails and we bill you at premium rates.</span></span>
* <span data-ttu-id="d58c7-193">就私用對等設定而言，路由表必須少於 4000 個路由。</span><span class="sxs-lookup"><span data-stu-id="d58c7-193">Your route table must be less than 4,000 routes for private peering.</span></span> <span data-ttu-id="d58c7-194">如果您的路由表的大小大於 4000 路由，會卸除 hello BGP 工作階段。</span><span class="sxs-lookup"><span data-stu-id="d58c7-194">If your route table size is greater than 4,000 routes, hello BGP session drops.</span></span> <span data-ttu-id="d58c7-195">hello 工作階段將不會重新啟用，直到 hello 公告的首碼數目，低於 4000。</span><span class="sxs-lookup"><span data-stu-id="d58c7-195">hello session won't be reenabled until hello number of advertised prefixes is below 4,000.</span></span>

<span data-ttu-id="d58c7-196">您可以使用下列範例中的 hello，停用 hello ExpressRoute premium add-on hello 現有循環：</span><span class="sxs-lookup"><span data-stu-id="d58c7-196">You can disable hello ExpressRoute premium add-on for hello existing circuit by using hello following example:</span></span>

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-tier Standard
```

### <a name="tooupdate-hello-expressroute-circuit-bandwidth"></a><span data-ttu-id="d58c7-197">tooupdate hello ExpressRoute 電路頻寬</span><span class="sxs-lookup"><span data-stu-id="d58c7-197">tooupdate hello ExpressRoute circuit bandwidth</span></span>

<span data-ttu-id="d58c7-198">您的提供者支援的 hello 頻寬選項，請檢查 hello [ExpressRoute 常見問題集](expressroute-faqs.md)。</span><span class="sxs-lookup"><span data-stu-id="d58c7-198">For hello supported bandwidth options for your provider, check hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span> <span data-ttu-id="d58c7-199">您可以挑選任何比您現有的循環 hello 大小更大的大小。</span><span class="sxs-lookup"><span data-stu-id="d58c7-199">You can pick any size greater than hello size of your existing circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d58c7-200">如果 hello 現有連接埠上沒有足夠的容量，您可能必須 toorecreate hello ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="d58c7-200">If there is inadequate capacity on hello existing port, you may have toorecreate hello ExpressRoute circuit.</span></span> <span data-ttu-id="d58c7-201">如果沒有任何額外的容量可在該位置，您無法升級 hello 循環。</span><span class="sxs-lookup"><span data-stu-id="d58c7-201">You cannot upgrade hello circuit if there is no additional capacity available at that location.</span></span>
>
> <span data-ttu-id="d58c7-202">您無法減少 hello 頻寬的 ExpressRoute 電路不會中斷。</span><span class="sxs-lookup"><span data-stu-id="d58c7-202">You cannot reduce hello bandwidth of an ExpressRoute circuit without disruption.</span></span> <span data-ttu-id="d58c7-203">降級頻寬需要您 toodeprovision hello ExpressRoute 電路並再重新佈建新增的 ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="d58c7-203">Downgrading bandwidth requires you toodeprovision hello ExpressRoute circuit, and then reprovision a new ExpressRoute circuit.</span></span>
>

<span data-ttu-id="d58c7-204">決定您需要的 hello 大小之後，請使用下列命令 tooresize hello 您的循環：</span><span class="sxs-lookup"><span data-stu-id="d58c7-204">After you decide hello size you need, use hello following command tooresize your circuit:</span></span>

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --bandwidth 1000
```

<span data-ttu-id="d58c7-205">您的電路會調整大小，Microsoft hello 一邊。</span><span class="sxs-lookup"><span data-stu-id="d58c7-205">Your circuit is sized up on hello Microsoft side.</span></span> <span data-ttu-id="d58c7-206">接下來，您必須連絡其端 toomatch 您連接的提供者 tooupdate 設定這項變更。</span><span class="sxs-lookup"><span data-stu-id="d58c7-206">Next, you must contact your connectivity provider tooupdate configurations on their side toomatch this change.</span></span> <span data-ttu-id="d58c7-207">此通知之後，我們會開始計費您更新的 hello 頻寬選項。</span><span class="sxs-lookup"><span data-stu-id="d58c7-207">After you make this notification, we begin billing you for hello updated bandwidth option.</span></span>

### <a name="toomove-hello-sku-from-metered-toounlimited"></a><span data-ttu-id="d58c7-208">從付費 toounlimited toomove hello SKU</span><span class="sxs-lookup"><span data-stu-id="d58c7-208">toomove hello SKU from metered toounlimited</span></span>

<span data-ttu-id="d58c7-209">您可以使用下列範例中的 hello 變更 hello 的 ExpressRoute 電路 SKU:</span><span class="sxs-lookup"><span data-stu-id="d58c7-209">You can change hello SKU of an ExpressRoute circuit by using hello following example:</span></span>

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-family UnlimitedData
```

### <a name="toocontrol-access-toohello-classic-and-resource-manager-environments"></a><span data-ttu-id="d58c7-210">toocontrol 存取 toohello 傳統和資源管理員環境</span><span class="sxs-lookup"><span data-stu-id="d58c7-210">toocontrol access toohello classic and Resource Manager environments</span></span>

<span data-ttu-id="d58c7-211">檢閱中的 hello 指示[從 hello 傳統 toohello Resource Manager 部署模型的移動 ExpressRoute 電路](expressroute-howto-move-arm.md)。</span><span class="sxs-lookup"><span data-stu-id="d58c7-211">Review hello instructions in [Move ExpressRoute circuits from hello classic toohello Resource Manager deployment model](expressroute-howto-move-arm.md).</span></span>

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a><span data-ttu-id="d58c7-212">取消佈建和刪除 ExpressRoute 線路</span><span class="sxs-lookup"><span data-stu-id="d58c7-212">Deprovisioning and deleting an ExpressRoute circuit</span></span>

<span data-ttu-id="d58c7-213">toodeprovision 和刪除 ExpressRoute 循環，請確定您瞭解下列準則的 hello:</span><span class="sxs-lookup"><span data-stu-id="d58c7-213">toodeprovision and delete an ExpressRoute circuit, make sure you understand hello following criteria:</span></span>

* <span data-ttu-id="d58c7-214">您必須取消連結從 hello ExpressRoute 電路的所有虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="d58c7-214">You must unlink all virtual networks from hello ExpressRoute circuit.</span></span> <span data-ttu-id="d58c7-215">如果此作業失敗，請檢查 toosee 如果任何虛擬網路連結 toohello 循環。</span><span class="sxs-lookup"><span data-stu-id="d58c7-215">If this operation fails, check toosee if any virtual networks are linked toohello circuit.</span></span>
* <span data-ttu-id="d58c7-216">如果 hello ExpressRoute 電路服務提供者佈建狀態為**佈建**或**已佈建**，您必須使用您的服務提供者 toodeprovision hello 電路邊。</span><span class="sxs-lookup"><span data-stu-id="d58c7-216">If hello ExpressRoute circuit service provider provisioning state is **Provisioning** or **Provisioned**, you must work with your service provider toodeprovision hello circuit on their side.</span></span> <span data-ttu-id="d58c7-217">我們繼續 tooreserve 資源，並向您收取費用，直到完成取消佈建 hello 電路 hello 服務提供者，並通知我們。</span><span class="sxs-lookup"><span data-stu-id="d58c7-217">We continue tooreserve resources and bill you until hello service provider completes deprovisioning hello circuit and notifies us.</span></span>
* <span data-ttu-id="d58c7-218">如果 hello 服務提供者已解除佈建 hello 循環，您可以刪除 hello 循環。</span><span class="sxs-lookup"><span data-stu-id="d58c7-218">You can delete hello circuit if hello service provider has deprovisioned hello circuit.</span></span> <span data-ttu-id="d58c7-219">當電路會解除佈建時，hello 服務提供者佈建狀態會設定太**未佈建**。</span><span class="sxs-lookup"><span data-stu-id="d58c7-219">When a circuit is deprovisioned, hello service provider provisioning state is set too**Not provisioned**.</span></span> <span data-ttu-id="d58c7-220">這會停止計費 hello 循環。</span><span class="sxs-lookup"><span data-stu-id="d58c7-220">This stops billing for hello circuit.</span></span>

<span data-ttu-id="d58c7-221">若要刪除 ExpressRoute 電路，您可以執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="d58c7-221">You can delete your ExpressRoute circuit by running hello following command:</span></span>

```azurecli
az network express-route delete  -n MyCircuit -g ExpressRouteResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="d58c7-222">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d58c7-222">Next steps</span></span>

<span data-ttu-id="d58c7-223">建立您的循環之後，請確定您執行下列工作 hello:</span><span class="sxs-lookup"><span data-stu-id="d58c7-223">After you create your circuit, make sure that you do hello following tasks:</span></span>

* [<span data-ttu-id="d58c7-224">建立和修改 ExpressRoute 線路的路由</span><span class="sxs-lookup"><span data-stu-id="d58c7-224">Create and modify routing for your ExpressRoute circuit</span></span>](howto-routing-cli.md)
* [<span data-ttu-id="d58c7-225">連結您的虛擬網路 tooyour ExpressRoute 電路</span><span class="sxs-lookup"><span data-stu-id="d58c7-225">Link your virtual network tooyour ExpressRoute circuit</span></span>](howto-linkvnet-cli.md)
