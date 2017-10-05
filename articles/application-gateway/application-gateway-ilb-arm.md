---
title: "使用 Azure 應用程式閘道搭配內部負載平衡器 - PowerShell | Microsoft Docs"
description: "本頁面提供使用 Azure 資源管理員建立、設定、啟動、刪除搭配內部負載平衡器 (ILB) 的 Azure 應用程式閘道的指示。"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 75cfd5a2-e378-4365-99ee-a2b2abda2e0d
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: d218eab7e9f124e4825a8a781b4eeb0dcca58b4a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-application-gateway-with-an-internal-load-balancer-ilb-by-using-azure-resource-manager"></a><span data-ttu-id="dbf2a-103">使用 Azure 資源管理員建立搭配內部負載平衡器 (ILB) 的應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="dbf2a-103">Create an application gateway with an internal load balancer (ILB) by using Azure Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="dbf2a-104">Azure 傳統 PowerShell</span><span class="sxs-lookup"><span data-stu-id="dbf2a-104">Azure Classic PowerShell</span></span>](application-gateway-ilb.md)
> * [<span data-ttu-id="dbf2a-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="dbf2a-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ilb-arm.md)

<span data-ttu-id="dbf2a-106">可以使用網際網路對向的 VIP 或不會對網際網路公開的內部端點 (也稱為內部負載平衡器 (ILB) 端點) 來設定 Azure 應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="dbf2a-106">Azure Application Gateway can be configured with an Internet-facing VIP or with an internal endpoint that is not exposed to the Internet, also known as an internal load balancer (ILB) endpoint.</span></span> <span data-ttu-id="dbf2a-107">使用 ILB 設定閘道適合不會對網際網路公開的內部企業營運應用程式。</span><span class="sxs-lookup"><span data-stu-id="dbf2a-107">Configuring the gateway with an ILB is useful for internal line-of-business applications that are not exposed to the Internet.</span></span> <span data-ttu-id="dbf2a-108">對於位在不會對網際網路公開的安全性界限中的多層式應用程式內的服務/階層也十分實用，但仍需要循環配置資源負載散發、工作階段綁定或安全通訊端層 (SSL) 終止。</span><span class="sxs-lookup"><span data-stu-id="dbf2a-108">It's also useful for services and tiers within a multi-tier application that sit in a security boundary that is not exposed to the Internet but still require round-robin load distribution, session stickiness, or Secure Sockets Layer (SSL) termination.</span></span>

<span data-ttu-id="dbf2a-109">本文會逐步引導您完成使用 ILB 設定應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="dbf2a-109">This article walks you through the steps to configure an application gateway with an ILB.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="dbf2a-110">開始之前</span><span class="sxs-lookup"><span data-stu-id="dbf2a-110">Before you begin</span></span>

1. <span data-ttu-id="dbf2a-111">使用 Web Platform Installer 安裝最新版的 Azure PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="dbf2a-111">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span></span> <span data-ttu-id="dbf2a-112">您可以從 **下載頁面** 的 [Windows PowerShell](https://azure.microsoft.com/downloads/)區段下載並安裝最新版本。</span><span class="sxs-lookup"><span data-stu-id="dbf2a-112">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="dbf2a-113">您會建立應用程式閘道的虛擬網路和子網路。</span><span class="sxs-lookup"><span data-stu-id="dbf2a-113">You create a virtual network and a subnet for Application Gateway.</span></span> <span data-ttu-id="dbf2a-114">請確定沒有虛擬機器或是雲端部署正在使用子網路。</span><span class="sxs-lookup"><span data-stu-id="dbf2a-114">Make sure that no virtual machines or cloud deployments are using the subnet.</span></span> <span data-ttu-id="dbf2a-115">應用程式閘道必須單獨在虛擬網路子網路中。</span><span class="sxs-lookup"><span data-stu-id="dbf2a-115">Application Gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="dbf2a-116">您要設定來使用應用程式閘道的伺服器必須存在，或是在虛擬網路中建立其端點，或是已指派公用 IP/VIP。</span><span class="sxs-lookup"><span data-stu-id="dbf2a-116">The servers that you configure to use the application gateway must exist or have their endpoints created either in the virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-to-create-an-application-gateway"></a><span data-ttu-id="dbf2a-117">建立應用程式閘道需要什麼？</span><span class="sxs-lookup"><span data-stu-id="dbf2a-117">What is required to create an application gateway?</span></span>

* <span data-ttu-id="dbf2a-118">**後端伺服器集區：** 後端伺服器的 IP 位址清單。</span><span class="sxs-lookup"><span data-stu-id="dbf2a-118">**Back-end server pool:** The list of IP addresses of the back-end servers.</span></span> <span data-ttu-id="dbf2a-119">列出的 IP 位址應屬於虛擬網路，但在應用程式閘道的不同子網路中，或應該是公用 IP/VIP。</span><span class="sxs-lookup"><span data-stu-id="dbf2a-119">The IP addresses listed should either belong to the virtual network but in a different subnet for the application gateway or should be a public IP/VIP.</span></span>
* <span data-ttu-id="dbf2a-120">**後端伺服器集區設定：** 每個集區都包括一些設定，例如連接埠、通訊協定和以 Cookie 為基礎的同質性。</span><span class="sxs-lookup"><span data-stu-id="dbf2a-120">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="dbf2a-121">這些設定會繫結至集區，並套用至集區內所有伺服器。</span><span class="sxs-lookup"><span data-stu-id="dbf2a-121">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="dbf2a-122">**前端連接埠：** 此連接埠是在應用程式閘道上開啟的公用連接埠。</span><span class="sxs-lookup"><span data-stu-id="dbf2a-122">**Front-end port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="dbf2a-123">流量會到達此連接埠，然後重新導向至其中一個後端伺服器。</span><span class="sxs-lookup"><span data-stu-id="dbf2a-123">Traffic hits this port, and then gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="dbf2a-124">**接聽程式：** 接聽程式具有前端連接埠、通訊協定 (Http 或 Https，都區分大小寫) 和 SSL 憑證名稱 (如果已設定 SSL 卸載)。</span><span class="sxs-lookup"><span data-stu-id="dbf2a-124">**Listener:** The listener has a front-end port, a protocol (Http or Https, these are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="dbf2a-125">**規則：** 規則會繫結接聽程式和後端伺服器集區，並定義當流量到達特定接聽程式時，應該導向到哪個後端伺服器集區。</span><span class="sxs-lookup"><span data-stu-id="dbf2a-125">**Rule:** The rule binds the listener and the back-end server pool and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span></span> <span data-ttu-id="dbf2a-126">目前只支援 *基本* 規則。</span><span class="sxs-lookup"><span data-stu-id="dbf2a-126">Currently, only the *basic* rule is supported.</span></span> <span data-ttu-id="dbf2a-127">*基本* 規則是循環配置資源的負載分配。</span><span class="sxs-lookup"><span data-stu-id="dbf2a-127">The *basic* rule is round-robin load distribution.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="dbf2a-128">建立應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="dbf2a-128">Create an application gateway</span></span>

<span data-ttu-id="dbf2a-129">使用「Azure 傳統」和「Azure Resource Manager」的差別，在於您建立應用程式閘道和需設定項目的順序。</span><span class="sxs-lookup"><span data-stu-id="dbf2a-129">The difference between using Azure Classic and Azure Resource Manager is the order in which you create the application gateway and the items that need to be configured.</span></span>
<span data-ttu-id="dbf2a-130">透過 Resource Manager，組成應用程式閘道的所有項目會個別進行設定，然後一併建立應用程式閘道資源。</span><span class="sxs-lookup"><span data-stu-id="dbf2a-130">With Resource Manager, all items that make an application gateway is configured individually and then put together to create the application gateway resource.</span></span>

<span data-ttu-id="dbf2a-131">以下是建立應用程式閘道所需的步驟：</span><span class="sxs-lookup"><span data-stu-id="dbf2a-131">Here are the steps that are needed to create an application gateway:</span></span>

1. <span data-ttu-id="dbf2a-132">建立資源管理員的資源群組</span><span class="sxs-lookup"><span data-stu-id="dbf2a-132">Create a resource group for Resource Manager</span></span>
2. <span data-ttu-id="dbf2a-133">建立應用程式閘道的虛擬網路和子網路</span><span class="sxs-lookup"><span data-stu-id="dbf2a-133">Create a virtual network and a subnet for the application gateway</span></span>
3. <span data-ttu-id="dbf2a-134">建立應用程式閘道組態物件</span><span class="sxs-lookup"><span data-stu-id="dbf2a-134">Create an application gateway configuration object</span></span>
4. <span data-ttu-id="dbf2a-135">建立應用程式閘道資源</span><span class="sxs-lookup"><span data-stu-id="dbf2a-135">Create an application gateway resource</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="dbf2a-136">建立資源管理員的資源群組</span><span class="sxs-lookup"><span data-stu-id="dbf2a-136">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="dbf2a-137">請確定您切換 PowerShell 模式以使用 Azure 資源管理員 Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="dbf2a-137">Make sure that you switch PowerShell mode to use the Azure Resource Manager cmdlets.</span></span> <span data-ttu-id="dbf2a-138">如需詳細資訊，可在 [搭配使用 Windows PowerShell 與資源管理員](../powershell-azure-resource-manager.md)取得。</span><span class="sxs-lookup"><span data-stu-id="dbf2a-138">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="dbf2a-139">步驟 1</span><span class="sxs-lookup"><span data-stu-id="dbf2a-139">Step 1</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="dbf2a-140">步驟 2</span><span class="sxs-lookup"><span data-stu-id="dbf2a-140">Step 2</span></span>

<span data-ttu-id="dbf2a-141">檢查帳戶的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="dbf2a-141">Check the subscriptions for the account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="dbf2a-142">系統會提示使用您的認證進行驗證。</span><span class="sxs-lookup"><span data-stu-id="dbf2a-142">You are prompted to authenticate with your credentials.</span></span>

### <a name="step-3"></a><span data-ttu-id="dbf2a-143">步驟 3</span><span class="sxs-lookup"><span data-stu-id="dbf2a-143">Step 3</span></span>

<span data-ttu-id="dbf2a-144">選擇要使用哪一個 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="dbf2a-144">Choose which of your Azure subscriptions to use.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="dbf2a-145">步驟 4</span><span class="sxs-lookup"><span data-stu-id="dbf2a-145">Step 4</span></span>

<span data-ttu-id="dbf2a-146">建立新的資源群組 (若使用現有的資源群組，請略過此步驟)。</span><span class="sxs-lookup"><span data-stu-id="dbf2a-146">Create a new resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -location "West US"
```

<span data-ttu-id="dbf2a-147">Azure 資源管理員需要所有的資源群組指定一個位置。</span><span class="sxs-lookup"><span data-stu-id="dbf2a-147">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="dbf2a-148">這用來作為該資源群組中資源的預設位置。</span><span class="sxs-lookup"><span data-stu-id="dbf2a-148">This is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="dbf2a-149">請確定所有用來建立應用程式閘道的命令都使用同一個資源群組。</span><span class="sxs-lookup"><span data-stu-id="dbf2a-149">Make sure that all commands to create an application gateway uses the same resource group.</span></span>

<span data-ttu-id="dbf2a-150">在上述範例中，我們建立名為 "appgw-rg" 的資源群組，且位置為美國西部 ("West US")。</span><span class="sxs-lookup"><span data-stu-id="dbf2a-150">In the preceding example, we created a resource group called "appgw-rg" and location "West US".</span></span>

## <a name="create-a-virtual-network-and-a-subnet-for-the-application-gateway"></a><span data-ttu-id="dbf2a-151">建立應用程式閘道的虛擬網路和子網路</span><span class="sxs-lookup"><span data-stu-id="dbf2a-151">Create a virtual network and a subnet for the application gateway</span></span>

<span data-ttu-id="dbf2a-152">下面的範例說明如何使用資源管理員建立虛擬網路：</span><span class="sxs-lookup"><span data-stu-id="dbf2a-152">The following example shows how to create a virtual network by using Resource Manager:</span></span>

### <a name="step-1"></a><span data-ttu-id="dbf2a-153">步驟 1</span><span class="sxs-lookup"><span data-stu-id="dbf2a-153">Step 1</span></span>

```powershell
$subnetconfig = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

<span data-ttu-id="dbf2a-154">這個步驟會將位址範圍 10.0.0.0/24 指派給用於建立虛擬網路的子網路變數。</span><span class="sxs-lookup"><span data-stu-id="dbf2a-154">This step assigns the address range 10.0.0.0/24 to a subnet variable to be used to create a virtual network.</span></span>

### <a name="step-2"></a><span data-ttu-id="dbf2a-155">步驟 2</span><span class="sxs-lookup"><span data-stu-id="dbf2a-155">Step 2</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnetconfig
```

<span data-ttu-id="dbf2a-156">這個步驟會使用前置詞 10.0.0.0/16 搭配子網路 10.0.0.0/24，在美國西部 ("West US") 區域的 "appgw-rg" 資源群組中建立名為 "appgwvnet" 的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="dbf2a-156">This step creates a virtual network named "appgwvnet" in resource group "appgw-rg" for the West US region using the prefix 10.0.0.0/16 with subnet 10.0.0.0/24.</span></span>

### <a name="step-3"></a><span data-ttu-id="dbf2a-157">步驟 3</span><span class="sxs-lookup"><span data-stu-id="dbf2a-157">Step 3</span></span>

```powershell
$subnet = $vnet.subnets[0]
```

<span data-ttu-id="dbf2a-158">這個步驟會將子網路物件指派給下一個步驟的變數 $subnet。</span><span class="sxs-lookup"><span data-stu-id="dbf2a-158">This step assigns the subnet object to variable $subnet for the next steps.</span></span>

## <a name="create-an-application-gateway-configuration-object"></a><span data-ttu-id="dbf2a-159">建立應用程式閘道組態物件</span><span class="sxs-lookup"><span data-stu-id="dbf2a-159">Create an application gateway configuration object</span></span>

### <a name="step-1"></a><span data-ttu-id="dbf2a-160">步驟 1</span><span class="sxs-lookup"><span data-stu-id="dbf2a-160">Step 1</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

<span data-ttu-id="dbf2a-161">這個步驟會建立名為 "gatewayIP01" 的應用程式閘道 IP 組態。</span><span class="sxs-lookup"><span data-stu-id="dbf2a-161">This step creates an application gateway IP configuration named "gatewayIP01".</span></span> <span data-ttu-id="dbf2a-162">當「應用程式閘道」啟動時，它會從已設定的子網路取得 IP 位址，再將網路流量路由傳送到後端 IP 集區中的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="dbf2a-162">When Application Gateway starts, it picks up an IP address from the subnet configured and route network traffic to the IP addresses in the back-end IP pool.</span></span> <span data-ttu-id="dbf2a-163">請記住，每個執行個體需要一個 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="dbf2a-163">Keep in mind that each instance takes one IP address.</span></span>

### <a name="step-2"></a><span data-ttu-id="dbf2a-164">步驟 2</span><span class="sxs-lookup"><span data-stu-id="dbf2a-164">Step 2</span></span>

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 10.1.1.8,10.1.1.9,10.1.1.10
```

<span data-ttu-id="dbf2a-165">這個步驟會設定名為 "pool01" 的後端 IP 位址集區，其 IP 位址有 "10.1.1.8、10.1.1.9、10.1.1.10"。</span><span class="sxs-lookup"><span data-stu-id="dbf2a-165">This step configures the back-end IP address pool named "pool01" with IP addresses "10.1.1.8, 10.1.1.9, 10.1.1.10".</span></span> <span data-ttu-id="dbf2a-166">這些 IP 位址會接收來自前端 IP 端點的網路流量。</span><span class="sxs-lookup"><span data-stu-id="dbf2a-166">Those are the IP addresses that receive the network traffic that comes from the front-end IP endpoint.</span></span> <span data-ttu-id="dbf2a-167">您可取代上述 IP 位址來新增自己的應用程式 IP 位址端點。</span><span class="sxs-lookup"><span data-stu-id="dbf2a-167">You replace the preceding IP addresses to add your own application IP address endpoints.</span></span>

### <a name="step-3"></a><span data-ttu-id="dbf2a-168">步驟 3</span><span class="sxs-lookup"><span data-stu-id="dbf2a-168">Step 3</span></span>

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Disabled
```

<span data-ttu-id="dbf2a-169">這個步驟會設定後端集區中負載平衡網路流量的應用程式閘道設定 "poolsetting01"。</span><span class="sxs-lookup"><span data-stu-id="dbf2a-169">This step configures application gateway setting "poolsetting01" for the load balanced network traffic in the back-end pool.</span></span>

### <a name="step-4"></a><span data-ttu-id="dbf2a-170">步驟 4</span><span class="sxs-lookup"><span data-stu-id="dbf2a-170">Step 4</span></span>

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 80
```

<span data-ttu-id="dbf2a-171">這個步驟會設定 ILB 的前端 IP 連接埠，名為 "frontendport01"。</span><span class="sxs-lookup"><span data-stu-id="dbf2a-171">This step configures the front-end IP port named "frontendport01" for the ILB.</span></span>

### <a name="step-5"></a><span data-ttu-id="dbf2a-172">步驟 5</span><span class="sxs-lookup"><span data-stu-id="dbf2a-172">Step 5</span></span>

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -Subnet $subnet
```

<span data-ttu-id="dbf2a-173">這個步驟會建立名為 "fipconfig01" 的前端 IP 組態，並與目前虛擬網路子網路的私人 IP 產生關聯。</span><span class="sxs-lookup"><span data-stu-id="dbf2a-173">This step creates the front-end IP configuration called "fipconfig01" and associates it with a private IP from the current virtual network subnet.</span></span>

### <a name="step-6"></a><span data-ttu-id="dbf2a-174">步驟 6</span><span class="sxs-lookup"><span data-stu-id="dbf2a-174">Step 6</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp
```

<span data-ttu-id="dbf2a-175">這個步驟會建立名為 "listener01" 的接聽程式，並將前端連接埠與前端 IP 組態產生關聯。</span><span class="sxs-lookup"><span data-stu-id="dbf2a-175">This step creates the listener called "listener01" and associates the front-end port to the front-end IP configuration.</span></span>

### <a name="step-7"></a><span data-ttu-id="dbf2a-176">步驟 7</span><span class="sxs-lookup"><span data-stu-id="dbf2a-176">Step 7</span></span>

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

<span data-ttu-id="dbf2a-177">這個步驟會建立名為 "rule01" 的負載平衡器路由規則，設定負載平衡器的行為。</span><span class="sxs-lookup"><span data-stu-id="dbf2a-177">This step creates the load balancer routing rule called "rule01" that configures the load balancer behavior.</span></span>

### <a name="step-8"></a><span data-ttu-id="dbf2a-178">步驟 8</span><span class="sxs-lookup"><span data-stu-id="dbf2a-178">Step 8</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

<span data-ttu-id="dbf2a-179">這個步驟會設定應用程式閘道的執行個體大小。</span><span class="sxs-lookup"><span data-stu-id="dbf2a-179">This step configures the instance size of the application gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="dbf2a-180">*InstanceCount* 的預設值是 2，且最大值是 10。</span><span class="sxs-lookup"><span data-stu-id="dbf2a-180">The default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="dbf2a-181">GatewaySize  的預設值是 Medium。</span><span class="sxs-lookup"><span data-stu-id="dbf2a-181">The default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="dbf2a-182">您可以在 Standard_Small、Standard_Medium 和 Standard_Large 之間選擇。</span><span class="sxs-lookup"><span data-stu-id="dbf2a-182">You can choose between Standard_Small, Standard_Medium, and Standard_Large.</span></span>

## <a name="create-an-application-gateway-by-using-new-azureapplicationgateway"></a><span data-ttu-id="dbf2a-183">使用 New-AzureApplicationGateway 建立應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="dbf2a-183">Create an application gateway by using New-AzureApplicationGateway</span></span>

<span data-ttu-id="dbf2a-184">利用上述步驟中的所有組態項目來建立應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="dbf2a-184">Creates an application gateway with all configuration items from the preceding steps.</span></span> <span data-ttu-id="dbf2a-185">此範例中的應用程式閘道名為 "appgwtest"。</span><span class="sxs-lookup"><span data-stu-id="dbf2a-185">In this example, the application gateway is called "appgwtest".</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku
```

<span data-ttu-id="dbf2a-186">這個步驟會利用上述步驟中的所有組態項目來建立應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="dbf2a-186">This step creates an application gateway with all configuration items from the preceding steps.</span></span> <span data-ttu-id="dbf2a-187">範例中的應用程式閘道名為 "appgwtest"。</span><span class="sxs-lookup"><span data-stu-id="dbf2a-187">In the example, the application gateway is called "appgwtest".</span></span>

## <a name="delete-an-application-gateway"></a><span data-ttu-id="dbf2a-188">刪除應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="dbf2a-188">Delete an application gateway</span></span>

<span data-ttu-id="dbf2a-189">若要刪除應用程式閘道，您需要依序執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="dbf2a-189">To delete an application gateway, you need to do the following steps in order:</span></span>

1. <span data-ttu-id="dbf2a-190">使用 `Stop-AzureRmApplicationGateway` Cmdlet 停止閘道。</span><span class="sxs-lookup"><span data-stu-id="dbf2a-190">Use the `Stop-AzureRmApplicationGateway` cmdlet to stop the gateway.</span></span>
2. <span data-ttu-id="dbf2a-191">使用 `Remove-AzureRmApplicationGateway` Cmdlet 移除閘道。</span><span class="sxs-lookup"><span data-stu-id="dbf2a-191">Use the `Remove-AzureRmApplicationGateway` cmdlet to remove the gateway.</span></span>
3. <span data-ttu-id="dbf2a-192">使用 `Get-AzureApplicationGateway` Cmdlet 確認已移除閘道。</span><span class="sxs-lookup"><span data-stu-id="dbf2a-192">Verify that the gateway has been removed by using the `Get-AzureApplicationGateway` cmdlet.</span></span>

### <a name="step-1"></a><span data-ttu-id="dbf2a-193">步驟 1</span><span class="sxs-lookup"><span data-stu-id="dbf2a-193">Step 1</span></span>

<span data-ttu-id="dbf2a-194">取得應用程式閘道物件，並關聯至變數 "$getgw"。</span><span class="sxs-lookup"><span data-stu-id="dbf2a-194">Get the application gateway object and associate it to a variable "$getgw".</span></span>

```powershell
$getgw =  Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg
```

### <a name="step-2"></a><span data-ttu-id="dbf2a-195">步驟 2</span><span class="sxs-lookup"><span data-stu-id="dbf2a-195">Step 2</span></span>

<span data-ttu-id="dbf2a-196">使用 `Stop-AzureRmApplicationGateway` 停止應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="dbf2a-196">Use `Stop-AzureRmApplicationGateway` to stop the application gateway.</span></span> <span data-ttu-id="dbf2a-197">這個範例的第一行顯示 `Stop-AzureRmApplicationGateway` Cmdlet，後面接著輸出。</span><span class="sxs-lookup"><span data-stu-id="dbf2a-197">This sample shows the `Stop-AzureRmApplicationGateway` cmdlet on the first line, followed by the output.</span></span>

```powershell
Stop-AzureRmApplicationGateway -ApplicationGateway $getgw  
```

```
VERBOSE: 9:49:34 PM - Begin Operation: Stop-AzureApplicationGateway
VERBOSE: 10:10:06 PM - Completed Operation: Stop-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   ce6c6c95-77b4-2118-9d65-e29defadffb8
```

<span data-ttu-id="dbf2a-198">當應用程式閘道處於已停止狀態之後，使用 `Remove-AzureRmApplicationGateway` Cmdlet 來移除服務。</span><span class="sxs-lookup"><span data-stu-id="dbf2a-198">Once the application gateway is in a stopped state, use the `Remove-AzureRmApplicationGateway` cmdlet to remove the service.</span></span>

```powershell
Remove-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Force
```

```
VERBOSE: 10:49:34 PM - Begin Operation: Remove-AzureApplicationGateway
VERBOSE: 10:50:36 PM - Completed Operation: Remove-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   055f3a96-8681-2094-a304-8d9a11ad8301
```

> [!NOTE]
> <span data-ttu-id="dbf2a-199">**-force** 參數可用來隱藏移除確認訊息。</span><span class="sxs-lookup"><span data-stu-id="dbf2a-199">The **-force** switch can be used to suppress the remove confirmation message.</span></span>

<span data-ttu-id="dbf2a-200">若要確認已移除服務，您可以使用 `Get-AzureRmApplicationGateway` Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="dbf2a-200">To verify that the service has been removed, you can use the `Get-AzureRmApplicationGateway` cmdlet.</span></span> <span data-ttu-id="dbf2a-201">這不是必要步驟。</span><span class="sxs-lookup"><span data-stu-id="dbf2a-201">This step is not required.</span></span>

```powershell
Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg
```

```
VERBOSE: 10:52:46 PM - Begin Operation: Get-AzureApplicationGateway

Get-AzureApplicationGateway : ResourceNotFound: The gateway does not exist.
```

## <a name="next-steps"></a><span data-ttu-id="dbf2a-202">後續步驟</span><span class="sxs-lookup"><span data-stu-id="dbf2a-202">Next steps</span></span>

<span data-ttu-id="dbf2a-203">如果您想要設定 SSL 卸載，請參閱 [設定應用程式閘道以進行 SSL 卸載](application-gateway-ssl.md)。</span><span class="sxs-lookup"><span data-stu-id="dbf2a-203">If you want to configure SSL offload, see [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="dbf2a-204">如果您想要將應用程式閘道設為與 ILB 搭配使用，請參閱 [建立具有內部負載平衡器 (ILB) 的應用程式閘道](application-gateway-ilb.md)。</span><span class="sxs-lookup"><span data-stu-id="dbf2a-204">If you want to configure an application gateway to use with an ILB, see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="dbf2a-205">如果您想進一步了解一般負載平衡選項，請參閱：</span><span class="sxs-lookup"><span data-stu-id="dbf2a-205">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="dbf2a-206">Azure 負載平衡器</span><span class="sxs-lookup"><span data-stu-id="dbf2a-206">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="dbf2a-207">Azure 流量管理員</span><span class="sxs-lookup"><span data-stu-id="dbf2a-207">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

