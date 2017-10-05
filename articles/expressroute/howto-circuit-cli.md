---
title: "建立與修改 Azure ExpressRoute 線路：CLI | Microsoft Docs"
description: "本文說明如何使用 CLI 建立、佈建、驗證、更新、刪除和取消佈建 ExpressRoute 線路。"
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
ms.openlocfilehash: 1a1c9a96b772868e2c832e9ff57874038c0db2d4
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-cli"></a><span data-ttu-id="45535-103">使用 CLI 建立和修改 ExpressRoute 線路</span><span class="sxs-lookup"><span data-stu-id="45535-103">Create and modify an ExpressRoute circuit using CLI</span></span>


<span data-ttu-id="45535-104">本文說明如何使用命令列介面 (CLI) 來建立 Azure ExpressRoute 線路。</span><span class="sxs-lookup"><span data-stu-id="45535-104">This article describes how to create an Azure ExpressRoute circuit by using the Command Line Interface (CLI).</span></span> <span data-ttu-id="45535-105">本文也會示範如何檢查狀態、更新或刪除和取消佈建線路。</span><span class="sxs-lookup"><span data-stu-id="45535-105">This article also shows you how to check the status, update, or delete and deprovision a circuit.</span></span> <span data-ttu-id="45535-106">如果您想要對 ExpressRoute 線路使用不同的方法，您可以從下列清單選取文章：</span><span class="sxs-lookup"><span data-stu-id="45535-106">If you want to use a different method to work with ExpressRoute circuits, you can select the article from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="45535-107">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="45535-107">Azure portal</span></span>](expressroute-howto-circuit-portal-resource-manager.md)
> * [<span data-ttu-id="45535-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="45535-108">PowerShell</span></span>](expressroute-howto-circuit-arm.md)
> * [<span data-ttu-id="45535-109">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="45535-109">Azure CLI</span></span>](howto-circuit-cli.md)
> * [<span data-ttu-id="45535-110">影片 - Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="45535-110">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [<span data-ttu-id="45535-111">PowerShell (傳統)</span><span class="sxs-lookup"><span data-stu-id="45535-111">PowerShell (classic)</span></span>](expressroute-howto-circuit-classic.md)
> 

## <a name="before-you-begin"></a><span data-ttu-id="45535-112">開始之前</span><span class="sxs-lookup"><span data-stu-id="45535-112">Before you begin</span></span>

* <span data-ttu-id="45535-113">開始之前，請先安裝 CLI 命令的最新版本 (2.0 版或更新版本)。</span><span class="sxs-lookup"><span data-stu-id="45535-113">Before beginning, install the latest version of the CLI commands (2.0 or later).</span></span> <span data-ttu-id="45535-114">如需關於安裝 CLI 命令的資訊，請參閱[安裝 Azure CLI 2.0](/cli/azure/install-azure-cli) 和[開始使用 Azure CLI 2.0](/cli/azure/get-started-with-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="45535-114">For information about installing the CLI commands, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli) and [Get Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).</span></span>
* <span data-ttu-id="45535-115">開始設定之前，請檢閱[必要條件](expressroute-prerequisites.md)和[工作流程](expressroute-workflows.md)。</span><span class="sxs-lookup"><span data-stu-id="45535-115">Review the [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

## <a name="create-and-provision-an-expressroute-circuit"></a><span data-ttu-id="45535-116">建立和佈建 ExpressRoute 線路</span><span class="sxs-lookup"><span data-stu-id="45535-116">Create and provision an ExpressRoute circuit</span></span>

### <a name="1-sign-in-to-your-azure-account-and-select-your-subscription"></a><span data-ttu-id="45535-117">1.登入您的 Azure 帳戶並且選取您的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="45535-117">1. Sign in to your Azure account and select your subscription</span></span>

<span data-ttu-id="45535-118">若要開始您的組態，請登入您的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="45535-118">To begin your configuration, sign in to your Azure account.</span></span> <span data-ttu-id="45535-119">使用下列範例來協助您連接：</span><span class="sxs-lookup"><span data-stu-id="45535-119">Use the following examples to help you connect:</span></span>

```azurecli
az login
```

<span data-ttu-id="45535-120">檢查帳戶的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="45535-120">Check the subscriptions for the account.</span></span>

```azurecli
az account list
```

<span data-ttu-id="45535-121">選取您想要建立 ExpressRoute 線路的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="45535-121">Select the subscription for which you want to create an ExpressRoute circuit.</span></span>

```azurecli
az account set --subscription "<subscription ID>"
```

### <a name="2-get-the-list-of-supported-providers-locations-and-bandwidths"></a><span data-ttu-id="45535-122">2.取得支援的提供者、位置和頻寬清單</span><span class="sxs-lookup"><span data-stu-id="45535-122">2. Get the list of supported providers, locations, and bandwidths</span></span>

<span data-ttu-id="45535-123">建立 ExpressRoute 線路之前，您需要有支援的連線提供者、位置和頻寬選項的清單。</span><span class="sxs-lookup"><span data-stu-id="45535-123">Before you create an ExpressRoute circuit, you need the list of supported connectivity providers, locations, and bandwidth options.</span></span> <span data-ttu-id="45535-124">CLI 命令 'az network express-route list-service-providers' 會傳回此資訊，您將在稍後的步驟中使用：</span><span class="sxs-lookup"><span data-stu-id="45535-124">The CLI command 'az network express-route list-service-providers' returns this information, which you’ll use in later steps:</span></span>

```azurecli
az network express-route list-service-providers
```

<span data-ttu-id="45535-125">回應如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="45535-125">The response is similar to the following example:</span></span>

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

<span data-ttu-id="45535-126">請檢查回應以查看是否列出您的連線提供者。</span><span class="sxs-lookup"><span data-stu-id="45535-126">Check the response to see if your connectivity provider is listed.</span></span> <span data-ttu-id="45535-127">記下下列資訊，當您建立線路時將會用到：</span><span class="sxs-lookup"><span data-stu-id="45535-127">Make a note of the following information, which you will need when you create a circuit:</span></span>

* <span data-ttu-id="45535-128">名稱</span><span class="sxs-lookup"><span data-stu-id="45535-128">Name</span></span>
* <span data-ttu-id="45535-129">PeeringLocations</span><span class="sxs-lookup"><span data-stu-id="45535-129">PeeringLocations</span></span>
* <span data-ttu-id="45535-130">BandwidthsOffered</span><span class="sxs-lookup"><span data-stu-id="45535-130">BandwidthsOffered</span></span>

<span data-ttu-id="45535-131">您現在已經準備好建立 ExpressRoute 線路。</span><span class="sxs-lookup"><span data-stu-id="45535-131">You're now ready to create an ExpressRoute circuit.</span></span>

### <a name="3-create-an-expressroute-circuit"></a><span data-ttu-id="45535-132">3.建立 ExpressRoute 線路</span><span class="sxs-lookup"><span data-stu-id="45535-132">3. Create an ExpressRoute circuit</span></span>

> [!IMPORTANT]
> <span data-ttu-id="45535-133">ExpressRoute 線路會從發出服務金鑰時開始收費。</span><span class="sxs-lookup"><span data-stu-id="45535-133">Your ExpressRoute circuit is billed from the moment a service key is issued.</span></span> <span data-ttu-id="45535-134">在連線提供者準備好佈建線路之後，再執行這項作業。</span><span class="sxs-lookup"><span data-stu-id="45535-134">Perform this operation when the connectivity provider is ready to provision the circuit.</span></span>
> 
> 

<span data-ttu-id="45535-135">若您還沒有資源群組，您必須在建立 ExpressRoute 線路之前建立一個。</span><span class="sxs-lookup"><span data-stu-id="45535-135">If you don't already have a resource group, you must create one before you create your ExpressRoute circuit.</span></span> <span data-ttu-id="45535-136">您可以藉由使用下列命令來建立資源群組：</span><span class="sxs-lookup"><span data-stu-id="45535-136">You can create a resource group by running the following command:</span></span>

```azurecli
az group create -n ExpressRouteResourceGroup -l "West US"
```

<span data-ttu-id="45535-137">以下示範如何透過矽谷的 Equinix 建立 200-Mbps ExpressRoute 線路。</span><span class="sxs-lookup"><span data-stu-id="45535-137">The following example shows how to create a 200-Mbps ExpressRoute circuit through Equinix in Silicon Valley.</span></span> <span data-ttu-id="45535-138">如果您使用不同的提供者和不同的設定，請在您提出要求時替換成該資訊。</span><span class="sxs-lookup"><span data-stu-id="45535-138">If you're using a different provider and different settings, substitute that information when you make your request.</span></span> 

<span data-ttu-id="45535-139">請確定您指定正確的 SKU 層和 SKU 系列：</span><span class="sxs-lookup"><span data-stu-id="45535-139">Make sure that you specify the correct SKU tier and SKU family:</span></span>

* <span data-ttu-id="45535-140">SKU 層會判斷 ExpressRoute 標準或 ExpressRoute 高階附加元件是否啟用。</span><span class="sxs-lookup"><span data-stu-id="45535-140">SKU tier determines whether an ExpressRoute standard or an ExpressRoute premium add-on is enabled.</span></span> <span data-ttu-id="45535-141">您可以指定 [標準] 來取得標準 SKU，或指定 [進階] 來取得進階附加元件。</span><span class="sxs-lookup"><span data-stu-id="45535-141">You can specify 'Standard' to get the standard SKU or 'Premium' for the premium add-on.</span></span>
* <span data-ttu-id="45535-142">SKU 系列決定計費類型。</span><span class="sxs-lookup"><span data-stu-id="45535-142">SKU family determines the billing type.</span></span> <span data-ttu-id="45535-143">您可以指定 [Metereddata] 以採用計量付費數據傳輸方案，選取 [Unlimiteddata] 以採用無限行動數據方案。</span><span class="sxs-lookup"><span data-stu-id="45535-143">You can specify 'Metereddata' for a metered data plan and 'Unlimiteddata' for an unlimited data plan.</span></span> <span data-ttu-id="45535-144">您可以將計費類型從 [Metereddata] 變更為 [Unlimiteddata]，但無法將類型從 [Unlimiteddata] 變更為 [Metereddata]。</span><span class="sxs-lookup"><span data-stu-id="45535-144">You can change the billing type from 'Metereddata' to 'Unlimiteddata', but you can't change the type from 'Unlimiteddata' to 'Metereddata'.</span></span>


<span data-ttu-id="45535-145">ExpressRoute 線路會從發出服務金鑰時開始收費。</span><span class="sxs-lookup"><span data-stu-id="45535-145">Your ExpressRoute circuit is billed from the moment a service key is issued.</span></span> <span data-ttu-id="45535-146">下列是新服務金鑰的要求範例：</span><span class="sxs-lookup"><span data-stu-id="45535-146">The following example is a request for a new service key:</span></span>

```azurecli
az network express-route create --bandwidth 200 -n MyCircuit --peering-location "Silicon Valley" -g ExpressRouteResourceGroup --provider "Equinix" -l "West US" --sku-family MeteredData --sku-tier Standard
```

<span data-ttu-id="45535-147">回應包含服務金鑰。</span><span class="sxs-lookup"><span data-stu-id="45535-147">The response contains the service key.</span></span>

### <a name="4-list-all-expressroute-circuits"></a><span data-ttu-id="45535-148">4.列出所有 ExpressRoute 循環</span><span class="sxs-lookup"><span data-stu-id="45535-148">4. List all ExpressRoute circuits</span></span>

<span data-ttu-id="45535-149">若要取得您已建立之所有 ExpressRoute 線路的清單，請執行 'az network express-route list' 命令。</span><span class="sxs-lookup"><span data-stu-id="45535-149">To get a list of all the ExpressRoute circuits that you created, run the 'az network express-route list' command.</span></span> <span data-ttu-id="45535-150">您隨時可以使用此命令來擷取此資訊。</span><span class="sxs-lookup"><span data-stu-id="45535-150">You can retrieve this information at any time by using this command.</span></span> <span data-ttu-id="45535-151">若要列出所有線路，在不使用任何參數的情況下進行呼叫。</span><span class="sxs-lookup"><span data-stu-id="45535-151">To list all circuits, make the call with no parameters.</span></span>

```azurecli
az network express-route list
```

<span data-ttu-id="45535-152">回應的 [服務金鑰] 欄位會列出您的服務金鑰。</span><span class="sxs-lookup"><span data-stu-id="45535-152">Your service key is listed in the *ServiceKey* field of the response.</span></span>

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

<span data-ttu-id="45535-153">您可以藉由使用 '-h' 來執行命令，以取得所有參數的詳細描述。</span><span class="sxs-lookup"><span data-stu-id="45535-153">You can get detailed descriptions of all the parameters by running the command using the '-h' parameter.</span></span>

```azurecli
az network express-route list -h
```

### <a name="5-send-the-service-key-to-your-connectivity-provider-for-provisioning"></a><span data-ttu-id="45535-154">5.將服務金鑰傳送給連線提供者以進行佈建</span><span class="sxs-lookup"><span data-stu-id="45535-154">5. Send the service key to your connectivity provider for provisioning</span></span>

<span data-ttu-id="45535-155">'ServiceProviderProvisioningState' 提供服務提供者端目前的佈建狀態相關資訊。</span><span class="sxs-lookup"><span data-stu-id="45535-155">'ServiceProviderProvisioningState' provides information about the current state of provisioning on the service-provider side.</span></span> <span data-ttu-id="45535-156">狀態提供 Microsoft 端的狀態。</span><span class="sxs-lookup"><span data-stu-id="45535-156">The status provides the state on the Microsoft side.</span></span> <span data-ttu-id="45535-157">如需詳細資訊，請參閱[工作流程文章](expressroute-workflows.md#expressroute-circuit-provisioning-states)。</span><span class="sxs-lookup"><span data-stu-id="45535-157">For more information, see the [Workflows article](expressroute-workflows.md#expressroute-circuit-provisioning-states).</span></span>

<span data-ttu-id="45535-158">當您建立新的 ExpressRoute 線路時，線路會是下列狀態：</span><span class="sxs-lookup"><span data-stu-id="45535-158">When you create a new ExpressRoute circuit, the circuit is in the following state:</span></span>

```azurecli
"serviceProviderProvisioningState": "NotProvisioned"
"circuitProvisioningState": "Enabled"
```

<span data-ttu-id="45535-159">當連線提供者正在為您啟用線路時，線路會變更為下列狀態：</span><span class="sxs-lookup"><span data-stu-id="45535-159">The circuit changes to the following state when the connectivity provider is in the process of enabling it for you:</span></span>

```azurecli
"serviceProviderProvisioningState": "Provisioning"
"circuitProvisioningState": "Enabled"
```

<span data-ttu-id="45535-160">若要能夠使用 ExpressRoute 線路，它必須處於下列狀態：</span><span class="sxs-lookup"><span data-stu-id="45535-160">For you to be able to use an ExpressRoute circuit, it must be in the following state:</span></span>

```azurecli
"serviceProviderProvisioningState": "Provisioned"
"circuitProvisioningState": "Enabled
```

### <a name="6-periodically-check-the-status-and-the-state-of-the-circuit-key"></a><span data-ttu-id="45535-161">6.定期檢查線路金鑰的情況和狀態</span><span class="sxs-lookup"><span data-stu-id="45535-161">6. Periodically check the status and the state of the circuit key</span></span>

<span data-ttu-id="45535-162">檢查線路金鑰的情況和狀態將能讓您得知提供者是否已啟用您的線路。</span><span class="sxs-lookup"><span data-stu-id="45535-162">Checking the status and the state of the circuit key lets you know when your provider has enabled your circuit.</span></span> <span data-ttu-id="45535-163">設定線路之後，[ServiceProviderProvisioningState] 會顯示為 [Provisioned]，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="45535-163">After the circuit has been configured, 'ServiceProviderProvisioningState' appears as 'Provisioned', as shown in the following example:</span></span>

```azurecli
az network express-route show --resource-group ExpressRouteResourceGroup --name MyCircuit
```

<span data-ttu-id="45535-164">回應如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="45535-164">The response is similar to the following example:</span></span>

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

### <a name="7-create-your-routing-configuration"></a><span data-ttu-id="45535-165">7.建立路由組態</span><span class="sxs-lookup"><span data-stu-id="45535-165">7. Create your routing configuration</span></span>

<span data-ttu-id="45535-166">如需逐步指示，請參閱 [ExpressRoute 線路路由組態](howto-routing-cli.md) 一文以建立和修改線路對等。</span><span class="sxs-lookup"><span data-stu-id="45535-166">For step-by-step instructions, see the [ExpressRoute circuit routing configuration](howto-routing-cli.md) article to create and modify circuit peerings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="45535-167">這些指示只適用於由提供第 2 層連線服務的服務提供者所建立的線路。</span><span class="sxs-lookup"><span data-stu-id="45535-167">These instructions only apply to circuits that are created with service providers that offer layer 2 connectivity services.</span></span> <span data-ttu-id="45535-168">如果您使用的服務提供者是提供受管理的第 3 層服務 (通常是 IP VPN，如 MPLS)，您的連線提供者會為您設定和管理路由。</span><span class="sxs-lookup"><span data-stu-id="45535-168">If you're using a service provider that offers managed layer 3 services (typically an IP VPN, like MPLS), your connectivity provider configures and manages routing for you.</span></span>
> 
> 

### <a name="8-link-a-virtual-network-to-an-expressroute-circuit"></a><span data-ttu-id="45535-169">8.將虛擬網路連結到 ExpressRoute 電路</span><span class="sxs-lookup"><span data-stu-id="45535-169">8. Link a virtual network to an ExpressRoute circuit</span></span>

<span data-ttu-id="45535-170">接下來，將虛擬網路連結到 ExpressRoute 線路。</span><span class="sxs-lookup"><span data-stu-id="45535-170">Next, link a virtual network to your ExpressRoute circuit.</span></span> <span data-ttu-id="45535-171">使用[將虛擬網路連結至 ExpressRoute 線路](howto-linkvnet-cli.md)一文。</span><span class="sxs-lookup"><span data-stu-id="45535-171">Use the [Linking virtual networks to ExpressRoute circuits](howto-linkvnet-cli.md) article.</span></span>

## <span data-ttu-id="45535-172"><a name="modify"></a>修改 ExpressRoute 線路</span><span class="sxs-lookup"><span data-stu-id="45535-172"><a name="modify"></a>Modifying an ExpressRoute circuit</span></span>

<span data-ttu-id="45535-173">您可以修改 ExpressRoute 線路的某些屬性，而不會影響連線。</span><span class="sxs-lookup"><span data-stu-id="45535-173">You can modify certain properties of an ExpressRoute circuit without impacting connectivity.</span></span> <span data-ttu-id="45535-174">您可以進行下列變更，而不會有停機時間：</span><span class="sxs-lookup"><span data-stu-id="45535-174">You can make the following changes with no downtime:</span></span>

* <span data-ttu-id="45535-175">您可以啟用或停用 ExpressRoute 線路的 ExpressRoute 進階附加元件。</span><span class="sxs-lookup"><span data-stu-id="45535-175">You can enable or disable an ExpressRoute premium add-on for your ExpressRoute circuit.</span></span>
* <span data-ttu-id="45535-176">只要連接埠有可用的容量，您就可以增加 ExpressRoute 線路的頻寬。</span><span class="sxs-lookup"><span data-stu-id="45535-176">You can increase the bandwidth of your ExpressRoute circuit provided there is capacity available on the port.</span></span> <span data-ttu-id="45535-177">但是，不支援將線路的頻寬降級。</span><span class="sxs-lookup"><span data-stu-id="45535-177">However, downgrading the bandwidth of a circuit is not supported.</span></span> 
* <span data-ttu-id="45535-178">您可以將計量方案從 [已計量資料] 變更為 [無限制資料]。</span><span class="sxs-lookup"><span data-stu-id="45535-178">You can change the metering plan from Metered Data to Unlimited Data.</span></span> <span data-ttu-id="45535-179">但是，不支援將計量方案從 [無限制資料] 變更為 [已計量資料]。</span><span class="sxs-lookup"><span data-stu-id="45535-179">However, changing the metering plan from Unlimited Data to Metered Data is not supported.</span></span>
* <span data-ttu-id="45535-180">您可以啟用和停用 [允許傳統作業]。</span><span class="sxs-lookup"><span data-stu-id="45535-180">You can enable and disable *Allow Classic Operations*.</span></span>

<span data-ttu-id="45535-181">如需限制的詳細資訊，請參閱 [ExpressRoute 常見問題集](expressroute-faqs.md)。</span><span class="sxs-lookup"><span data-stu-id="45535-181">For more information on limits and limitations, see the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

### <a name="to-enable-the-expressroute-premium-add-on"></a><span data-ttu-id="45535-182">啟用 ExpressRoute 進階附加元件</span><span class="sxs-lookup"><span data-stu-id="45535-182">To enable the ExpressRoute premium add-on</span></span>

<span data-ttu-id="45535-183">您可以使用下列命令，為現有的線路啟用 ExpressRoute 進階附加元件：</span><span class="sxs-lookup"><span data-stu-id="45535-183">You can enable the ExpressRoute premium add-on for your existing circuit by using the following command:</span></span>

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-tier Premium
```

<span data-ttu-id="45535-184">線路現在會啟用 ExpressRoute 進階附加功能。</span><span class="sxs-lookup"><span data-stu-id="45535-184">The circuit now has the ExpressRoute premium add-on features enabled.</span></span> <span data-ttu-id="45535-185">順利執行命令之後，我們就會立即開始針對進階附加元件功能計費。</span><span class="sxs-lookup"><span data-stu-id="45535-185">We begin billing you for the premium add-on capability as soon as the command has successfully run.</span></span>

### <a name="to-disable-the-expressroute-premium-add-on"></a><span data-ttu-id="45535-186">停用 ExpressRoute 進階附加元件</span><span class="sxs-lookup"><span data-stu-id="45535-186">To disable the ExpressRoute premium add-on</span></span>

> [!IMPORTANT]
> <span data-ttu-id="45535-187">如果您使用的資源超出標準線路所允許的數量，這項作業可能會失敗。</span><span class="sxs-lookup"><span data-stu-id="45535-187">This operation can fail if you're using resources that are greater than what is permitted for the standard circuit.</span></span>
> 
> 

<span data-ttu-id="45535-188">停用 ExpressRoute 進階附加元件之前，請了解下列準則：</span><span class="sxs-lookup"><span data-stu-id="45535-188">Before disabling the ExpressRoute premium add-on, understand the following criteria:</span></span>

* <span data-ttu-id="45535-189">從進階降級為標準之前，您必須確定連結至線路的虛擬網路數目小於 10。</span><span class="sxs-lookup"><span data-stu-id="45535-189">Before you downgrade from premium to standard, you must make sure that you have fewer than 10 virtual networks linked to the circuit.</span></span> <span data-ttu-id="45535-190">如果數目大於 10，更新要求就會失敗，且我們會以進階費率計費。</span><span class="sxs-lookup"><span data-stu-id="45535-190">If you have more than 10, your update request fails, and we bill you at premium rates.</span></span>
* <span data-ttu-id="45535-191">您必須取消連結其他地理政治區域中的所有虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="45535-191">You must unlink all virtual networks in other geopolitical regions.</span></span> <span data-ttu-id="45535-192">如果您未將所有虛擬網路取消連結，更新要求就會失敗，且我們會以進階費率計費。</span><span class="sxs-lookup"><span data-stu-id="45535-192">If you don't unlink all your virtual networks, your update request fails and we bill you at premium rates.</span></span>
* <span data-ttu-id="45535-193">就私用對等設定而言，路由表必須少於 4000 個路由。</span><span class="sxs-lookup"><span data-stu-id="45535-193">Your route table must be less than 4,000 routes for private peering.</span></span> <span data-ttu-id="45535-194">如果您的路由資料表大小大於 4000 個路由，BGP 工作階段會卸除。</span><span class="sxs-lookup"><span data-stu-id="45535-194">If your route table size is greater than 4,000 routes, the BGP session drops.</span></span> <span data-ttu-id="45535-195">直到已公告的前置詞數目低於 4000 之前，不會重新啟用工作階段。</span><span class="sxs-lookup"><span data-stu-id="45535-195">The session won't be reenabled until the number of advertised prefixes is below 4,000.</span></span>

<span data-ttu-id="45535-196">您可以使用下列範例，為現有的線路停用 ExpressRoute 進階附加元件：</span><span class="sxs-lookup"><span data-stu-id="45535-196">You can disable the ExpressRoute premium add-on for the existing circuit by using the following example:</span></span>

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-tier Standard
```

### <a name="to-update-the-expressroute-circuit-bandwidth"></a><span data-ttu-id="45535-197">更新 ExpressRoute 線路頻寬</span><span class="sxs-lookup"><span data-stu-id="45535-197">To update the ExpressRoute circuit bandwidth</span></span>

<span data-ttu-id="45535-198">請查閱 [ExpressRoute 常見問題集](expressroute-faqs.md)，以取得提供者支援的頻寬選項。</span><span class="sxs-lookup"><span data-stu-id="45535-198">For the supported bandwidth options for your provider, check the [ExpressRoute FAQ](expressroute-faqs.md).</span></span> <span data-ttu-id="45535-199">您可以挑選任何比現有線路規模還大的大小。</span><span class="sxs-lookup"><span data-stu-id="45535-199">You can pick any size greater than the size of your existing circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="45535-200">如果現有的連接埠上沒有足夠的容量，您可能必須重新建立 ExpressRoute 線路。</span><span class="sxs-lookup"><span data-stu-id="45535-200">If there is inadequate capacity on the existing port, you may have to recreate the ExpressRoute circuit.</span></span> <span data-ttu-id="45535-201">如果該位置已無額外的容量，您無法升級線路。</span><span class="sxs-lookup"><span data-stu-id="45535-201">You cannot upgrade the circuit if there is no additional capacity available at that location.</span></span>
>
> <span data-ttu-id="45535-202">降低 ExpressRoute 線路的頻寬時必須中斷運作。</span><span class="sxs-lookup"><span data-stu-id="45535-202">You cannot reduce the bandwidth of an ExpressRoute circuit without disruption.</span></span> <span data-ttu-id="45535-203">頻寬降級需要取消佈建 ExpressRoute 線路，然後重新佈建新的 ExpressRoute 線路。</span><span class="sxs-lookup"><span data-stu-id="45535-203">Downgrading bandwidth requires you to deprovision the ExpressRoute circuit, and then reprovision a new ExpressRoute circuit.</span></span>
>

<span data-ttu-id="45535-204">一旦決定需要的大小後，可以使用下列命令來重新調整線路大小：</span><span class="sxs-lookup"><span data-stu-id="45535-204">After you decide the size you need, use the following command to resize your circuit:</span></span>

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --bandwidth 1000
```

<span data-ttu-id="45535-205">我們會在 Microsoft 端調整線路的大小。</span><span class="sxs-lookup"><span data-stu-id="45535-205">Your circuit is sized up on the Microsoft side.</span></span> <span data-ttu-id="45535-206">接下來，您必須連絡連線提供者，將他們的設定更新為符合這項變更。</span><span class="sxs-lookup"><span data-stu-id="45535-206">Next, you must contact your connectivity provider to update configurations on their side to match this change.</span></span> <span data-ttu-id="45535-207">通知之後，我們會開始以更新的頻寬選項計費。</span><span class="sxs-lookup"><span data-stu-id="45535-207">After you make this notification, we begin billing you for the updated bandwidth option.</span></span>

### <a name="to-move-the-sku-from-metered-to-unlimited"></a><span data-ttu-id="45535-208">將 SKU 從計量移動為無限</span><span class="sxs-lookup"><span data-stu-id="45535-208">To move the SKU from metered to unlimited</span></span>

<span data-ttu-id="45535-209">您可以使用下列範例來變更 ExpressRoute 線路的 SKU：</span><span class="sxs-lookup"><span data-stu-id="45535-209">You can change the SKU of an ExpressRoute circuit by using the following example:</span></span>

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-family UnlimitedData
```

### <a name="to-control-access-to-the-classic-and-resource-manager-environments"></a><span data-ttu-id="45535-210">控制對傳統和 Resource Manager 環境的存取</span><span class="sxs-lookup"><span data-stu-id="45535-210">To control access to the classic and Resource Manager environments</span></span>

<span data-ttu-id="45535-211">請檢閱 [將 ExpressRoute 線路從傳統部署模型移至 Resource Manager 部署模型](expressroute-howto-move-arm.md)中的指示。</span><span class="sxs-lookup"><span data-stu-id="45535-211">Review the instructions in [Move ExpressRoute circuits from the classic to the Resource Manager deployment model](expressroute-howto-move-arm.md).</span></span>

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a><span data-ttu-id="45535-212">取消佈建和刪除 ExpressRoute 線路</span><span class="sxs-lookup"><span data-stu-id="45535-212">Deprovisioning and deleting an ExpressRoute circuit</span></span>

<span data-ttu-id="45535-213">若要取消佈建並刪除 ExpressRoute 線路，請確定您了解下列準則：</span><span class="sxs-lookup"><span data-stu-id="45535-213">To deprovision and delete an ExpressRoute circuit, make sure you understand the following criteria:</span></span>

* <span data-ttu-id="45535-214">您必須取消連結 ExpressRoute 線路的所有虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="45535-214">You must unlink all virtual networks from the ExpressRoute circuit.</span></span> <span data-ttu-id="45535-215">如果此作業失敗，請確認是否有任何虛擬網路連結至循環。</span><span class="sxs-lookup"><span data-stu-id="45535-215">If this operation fails, check to see if any virtual networks are linked to the circuit.</span></span>
* <span data-ttu-id="45535-216">如果 ExpressRoute 線路服務提供者佈建狀態為 **Provisioning** 或 **Provisioned**，您就必須與服務提供者一起合作，取消佈建他們那邊的線路。</span><span class="sxs-lookup"><span data-stu-id="45535-216">If the ExpressRoute circuit service provider provisioning state is **Provisioning** or **Provisioned**, you must work with your service provider to deprovision the circuit on their side.</span></span> <span data-ttu-id="45535-217">我們會繼續保留資源並向您收取費用，直到線路服務提供者完成取消佈建並通知我們。</span><span class="sxs-lookup"><span data-stu-id="45535-217">We continue to reserve resources and bill you until the service provider completes deprovisioning the circuit and notifies us.</span></span>
* <span data-ttu-id="45535-218">您只能在服務提供者已取消佈建線路時刪除線路。</span><span class="sxs-lookup"><span data-stu-id="45535-218">You can delete the circuit if the service provider has deprovisioned the circuit.</span></span> <span data-ttu-id="45535-219">當線路取消佈建時，服務提供者佈建狀態會設定為「未佈建」。</span><span class="sxs-lookup"><span data-stu-id="45535-219">When a circuit is deprovisioned, the service provider provisioning state is set to **Not provisioned**.</span></span> <span data-ttu-id="45535-220">這樣會停止針對線路計費。</span><span class="sxs-lookup"><span data-stu-id="45535-220">This stops billing for the circuit.</span></span>

<span data-ttu-id="45535-221">您可以執行下列命令來刪除 ExpressRoute 線路：</span><span class="sxs-lookup"><span data-stu-id="45535-221">You can delete your ExpressRoute circuit by running the following command:</span></span>

```azurecli
az network express-route delete  -n MyCircuit -g ExpressRouteResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="45535-222">後續步驟</span><span class="sxs-lookup"><span data-stu-id="45535-222">Next steps</span></span>

<span data-ttu-id="45535-223">建立好線路後，請務必執行下列工作：</span><span class="sxs-lookup"><span data-stu-id="45535-223">After you create your circuit, make sure that you do the following tasks:</span></span>

* [<span data-ttu-id="45535-224">建立和修改 ExpressRoute 線路的路由</span><span class="sxs-lookup"><span data-stu-id="45535-224">Create and modify routing for your ExpressRoute circuit</span></span>](howto-routing-cli.md)
* [<span data-ttu-id="45535-225">將虛擬網路連結至 ExpressRoute 線路</span><span class="sxs-lookup"><span data-stu-id="45535-225">Link your virtual network to your ExpressRoute circuit</span></span>](howto-linkvnet-cli.md)