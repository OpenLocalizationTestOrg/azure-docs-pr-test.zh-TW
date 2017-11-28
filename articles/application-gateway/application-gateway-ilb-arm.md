---
title: "使用內部負載平衡器-PowerShell 的 Azure 應用程式閘道 aaaUsing |Microsoft 文件"
description: "本頁面提供的指示 toocreate、 設定、 啟動和刪除 Azure 資源管理員的 Azure 應用程式閘道與內部負載平衡器 (ILB)"
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
ms.openlocfilehash: dd0d7e954b1fa219ae6ebe42cb4b479dbcf08653
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-with-an-internal-load-balancer-ilb-by-using-azure-resource-manager"></a><span data-ttu-id="6d4fa-103">使用 Azure 資源管理員建立搭配內部負載平衡器 (ILB) 的應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="6d4fa-103">Create an application gateway with an internal load balancer (ILB) by using Azure Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="6d4fa-104">Azure 傳統 PowerShell</span><span class="sxs-lookup"><span data-stu-id="6d4fa-104">Azure Classic PowerShell</span></span>](application-gateway-ilb.md)
> * [<span data-ttu-id="6d4fa-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="6d4fa-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ilb-arm.md)

<span data-ttu-id="6d4fa-106">與網際網路對向的 VIP 或不公開的 toohello 網際網路，也稱為內部負載平衡 (ILB) 端點的內部端點，則可以設定 azure 應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="6d4fa-106">Azure Application Gateway can be configured with an Internet-facing VIP or with an internal endpoint that is not exposed toohello Internet, also known as an internal load balancer (ILB) endpoint.</span></span> <span data-ttu-id="6d4fa-107">ILB 設定 hello 閘道可用於不公開的 toohello 網際網路的內部特定業務應用程式。</span><span class="sxs-lookup"><span data-stu-id="6d4fa-107">Configuring hello gateway with an ILB is useful for internal line-of-business applications that are not exposed toohello Internet.</span></span> <span data-ttu-id="6d4fa-108">它也可用於服務和內的多層式應用程式層放在不是公開的 toohello 網際網路的安全性界限內，但仍需要循環配置資源負載散發 」、 「 神奇工作階段的結果或 「 安全通訊端層 (SSL) 終止。</span><span class="sxs-lookup"><span data-stu-id="6d4fa-108">It's also useful for services and tiers within a multi-tier application that sit in a security boundary that is not exposed toohello Internet but still require round-robin load distribution, session stickiness, or Secure Sockets Layer (SSL) termination.</span></span>

<span data-ttu-id="6d4fa-109">這篇文章會引導您 hello 步驟 tooconfigure 應用程式閘道搭配 ILB 一起運作。</span><span class="sxs-lookup"><span data-stu-id="6d4fa-109">This article walks you through hello steps tooconfigure an application gateway with an ILB.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="6d4fa-110">開始之前</span><span class="sxs-lookup"><span data-stu-id="6d4fa-110">Before you begin</span></span>

1. <span data-ttu-id="6d4fa-111">使用 hello Web Platform Installer 安裝 hello hello Azure PowerShell cmdlet 的最新版本。</span><span class="sxs-lookup"><span data-stu-id="6d4fa-111">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="6d4fa-112">您可以從下載並安裝最新版本的 hello hello **Windows PowerShell**區段 hello[下載頁面](https://azure.microsoft.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="6d4fa-112">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="6d4fa-113">您會建立應用程式閘道的虛擬網路和子網路。</span><span class="sxs-lookup"><span data-stu-id="6d4fa-113">You create a virtual network and a subnet for Application Gateway.</span></span> <span data-ttu-id="6d4fa-114">請確定沒有虛擬機器或雲端部署使用 hello 子網路。</span><span class="sxs-lookup"><span data-stu-id="6d4fa-114">Make sure that no virtual machines or cloud deployments are using hello subnet.</span></span> <span data-ttu-id="6d4fa-115">應用程式閘道必須單獨在虛擬網路子網路中。</span><span class="sxs-lookup"><span data-stu-id="6d4fa-115">Application Gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="6d4fa-116">您設定 toouse hello 應用程式閘道的 hello 伺服器必須存在，或指派建立 hello 虛擬網路中，或是具有公用 IP/VIP 端點。</span><span class="sxs-lookup"><span data-stu-id="6d4fa-116">hello servers that you configure toouse hello application gateway must exist or have their endpoints created either in hello virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-toocreate-an-application-gateway"></a><span data-ttu-id="6d4fa-117">什麼是必要的 toocreate 應用程式閘道？</span><span class="sxs-lookup"><span data-stu-id="6d4fa-117">What is required toocreate an application gateway?</span></span>

* <span data-ttu-id="6d4fa-118">**後端伺服器集區：** hello hello 後端伺服器的 IP 位址清單。</span><span class="sxs-lookup"><span data-stu-id="6d4fa-118">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="6d4fa-119">hello 列出的 IP 位址應該是屬於 toohello 虛擬網路但不同子網路都會為 hello 應用程式閘道或應該是公用 IP/VIP。</span><span class="sxs-lookup"><span data-stu-id="6d4fa-119">hello IP addresses listed should either belong toohello virtual network but in a different subnet for hello application gateway or should be a public IP/VIP.</span></span>
* <span data-ttu-id="6d4fa-120">**後端伺服器集區設定：** 每個集區都包括一些設定，例如連接埠、通訊協定和以 Cookie 為基礎的同質性。</span><span class="sxs-lookup"><span data-stu-id="6d4fa-120">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="6d4fa-121">這些設定會繫結的 tooa 集區，並套用的 tooall hello 集區內的伺服器。</span><span class="sxs-lookup"><span data-stu-id="6d4fa-121">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="6d4fa-122">**前端連接埠：**此連接埠是開啟 hello 應用程式閘道上的 hello 公用連接埠。</span><span class="sxs-lookup"><span data-stu-id="6d4fa-122">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="6d4fa-123">流量叫用這個連接埠，然後再取得重新導向 tooone 的 hello 後端伺服器。</span><span class="sxs-lookup"><span data-stu-id="6d4fa-123">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="6d4fa-124">**接聽程式：** hello 接聽程式有前端連接埠的通訊協定 （Http 或 Https，這些是區分大小寫），與 hello 的 SSL 憑證名稱 （如果有設定 SSL 卸載）。</span><span class="sxs-lookup"><span data-stu-id="6d4fa-124">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="6d4fa-125">**規則：** hello 規則繫結 hello 接聽程式和 hello 後端伺服器集區，並定義哪一個後端伺服器集區 hello 流量應導向的 toowhen 配接器特定接聽程式。</span><span class="sxs-lookup"><span data-stu-id="6d4fa-125">**Rule:** hello rule binds hello listener and hello back-end server pool and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span> <span data-ttu-id="6d4fa-126">目前，只有 hello*基本*規則支援。</span><span class="sxs-lookup"><span data-stu-id="6d4fa-126">Currently, only hello *basic* rule is supported.</span></span> <span data-ttu-id="6d4fa-127">hello*基本*規則是循環配置資源負載分佈。</span><span class="sxs-lookup"><span data-stu-id="6d4fa-127">hello *basic* rule is round-robin load distribution.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="6d4fa-128">建立應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="6d4fa-128">Create an application gateway</span></span>

<span data-ttu-id="6d4fa-129">使用 Azure 傳統和 Azure 資源管理員的 hello 差別在於 hello 順序建立 hello 應用程式閘道，必須設定 toobe hello 項目。</span><span class="sxs-lookup"><span data-stu-id="6d4fa-129">hello difference between using Azure Classic and Azure Resource Manager is hello order in which you create hello application gateway and hello items that need toobe configured.</span></span>
<span data-ttu-id="6d4fa-130">使用資源管理員，讓應用程式閘道的所有項目個別設定，然後放置在一起 toocreate hello 應用程式閘道資源。</span><span class="sxs-lookup"><span data-stu-id="6d4fa-130">With Resource Manager, all items that make an application gateway is configured individually and then put together toocreate hello application gateway resource.</span></span>

<span data-ttu-id="6d4fa-131">以下是需要的 toocreate 應用程式閘道的 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="6d4fa-131">Here are hello steps that are needed toocreate an application gateway:</span></span>

1. <span data-ttu-id="6d4fa-132">建立資源管理員的資源群組</span><span class="sxs-lookup"><span data-stu-id="6d4fa-132">Create a resource group for Resource Manager</span></span>
2. <span data-ttu-id="6d4fa-133">建立虛擬網路和 hello 應用程式閘道的子網路</span><span class="sxs-lookup"><span data-stu-id="6d4fa-133">Create a virtual network and a subnet for hello application gateway</span></span>
3. <span data-ttu-id="6d4fa-134">建立應用程式閘道組態物件</span><span class="sxs-lookup"><span data-stu-id="6d4fa-134">Create an application gateway configuration object</span></span>
4. <span data-ttu-id="6d4fa-135">建立應用程式閘道資源</span><span class="sxs-lookup"><span data-stu-id="6d4fa-135">Create an application gateway resource</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="6d4fa-136">建立資源管理員的資源群組</span><span class="sxs-lookup"><span data-stu-id="6d4fa-136">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="6d4fa-137">請確定您切換 PowerShell 模式 toouse hello Azure 資源管理員 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="6d4fa-137">Make sure that you switch PowerShell mode toouse hello Azure Resource Manager cmdlets.</span></span> <span data-ttu-id="6d4fa-138">如需詳細資訊，請參閱 [搭配使用 Windows PowerShell 與資源管理員](../powershell-azure-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="6d4fa-138">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="6d4fa-139">步驟 1</span><span class="sxs-lookup"><span data-stu-id="6d4fa-139">Step 1</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="6d4fa-140">步驟 2</span><span class="sxs-lookup"><span data-stu-id="6d4fa-140">Step 2</span></span>

<span data-ttu-id="6d4fa-141">請檢查 hello hello 帳戶的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="6d4fa-141">Check hello subscriptions for hello account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="6d4fa-142">您必須提示的 tooauthenticate 和您的認證。</span><span class="sxs-lookup"><span data-stu-id="6d4fa-142">You are prompted tooauthenticate with your credentials.</span></span>

### <a name="step-3"></a><span data-ttu-id="6d4fa-143">步驟 3</span><span class="sxs-lookup"><span data-stu-id="6d4fa-143">Step 3</span></span>

<span data-ttu-id="6d4fa-144">選擇 Azure 訂用帳戶 toouse。</span><span class="sxs-lookup"><span data-stu-id="6d4fa-144">Choose which of your Azure subscriptions toouse.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="6d4fa-145">步驟 4</span><span class="sxs-lookup"><span data-stu-id="6d4fa-145">Step 4</span></span>

<span data-ttu-id="6d4fa-146">建立新的資源群組 (若使用現有的資源群組，請略過此步驟)。</span><span class="sxs-lookup"><span data-stu-id="6d4fa-146">Create a new resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -location "West US"
```

<span data-ttu-id="6d4fa-147">Azure Resource Manager 需要所有的資源群組指定一個位置。</span><span class="sxs-lookup"><span data-stu-id="6d4fa-147">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="6d4fa-148">這當做 hello 預設位置，該資源群組中的資源。</span><span class="sxs-lookup"><span data-stu-id="6d4fa-148">This is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="6d4fa-149">請確定應用程式閘道使用的所有命令 toocreate 都 hello 相同資源群組。</span><span class="sxs-lookup"><span data-stu-id="6d4fa-149">Make sure that all commands toocreate an application gateway uses hello same resource group.</span></span>

<span data-ttu-id="6d4fa-150">在上述範例中的 hello，我們會建立名為"appgw rg 」 和 「 位置 」 美國西部 」 的資源群組。</span><span class="sxs-lookup"><span data-stu-id="6d4fa-150">In hello preceding example, we created a resource group called "appgw-rg" and location "West US".</span></span>

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a><span data-ttu-id="6d4fa-151">建立虛擬網路和 hello 應用程式閘道的子網路</span><span class="sxs-lookup"><span data-stu-id="6d4fa-151">Create a virtual network and a subnet for hello application gateway</span></span>

<span data-ttu-id="6d4fa-152">下列範例會示範如何 hello toocreate 使用資源管理員的虛擬網路：</span><span class="sxs-lookup"><span data-stu-id="6d4fa-152">hello following example shows how toocreate a virtual network by using Resource Manager:</span></span>

### <a name="step-1"></a><span data-ttu-id="6d4fa-153">步驟 1</span><span class="sxs-lookup"><span data-stu-id="6d4fa-153">Step 1</span></span>

```powershell
$subnetconfig = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

<span data-ttu-id="6d4fa-154">此步驟會指派 hello 位址範圍 10.0.0.0/24 tooa 子網路使用的變數 toobe toocreate 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="6d4fa-154">This step assigns hello address range 10.0.0.0/24 tooa subnet variable toobe used toocreate a virtual network.</span></span>

### <a name="step-2"></a><span data-ttu-id="6d4fa-155">步驟 2</span><span class="sxs-lookup"><span data-stu-id="6d4fa-155">Step 2</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnetconfig
```

<span data-ttu-id="6d4fa-156">此步驟會建立名為"appgwvnet"的虛擬網路中資源群組 」 appgw-rg"hello 前置詞 10.0.0.0/16 使用子網路 10.0.0.0/24 hello 美國西部地區。</span><span class="sxs-lookup"><span data-stu-id="6d4fa-156">This step creates a virtual network named "appgwvnet" in resource group "appgw-rg" for hello West US region using hello prefix 10.0.0.0/16 with subnet 10.0.0.0/24.</span></span>

### <a name="step-3"></a><span data-ttu-id="6d4fa-157">步驟 3</span><span class="sxs-lookup"><span data-stu-id="6d4fa-157">Step 3</span></span>

```powershell
$subnet = $vnet.subnets[0]
```

<span data-ttu-id="6d4fa-158">此步驟會將指派 hello 子網路物件 toovariable $subnet hello 接下來的步驟。</span><span class="sxs-lookup"><span data-stu-id="6d4fa-158">This step assigns hello subnet object toovariable $subnet for hello next steps.</span></span>

## <a name="create-an-application-gateway-configuration-object"></a><span data-ttu-id="6d4fa-159">建立應用程式閘道組態物件</span><span class="sxs-lookup"><span data-stu-id="6d4fa-159">Create an application gateway configuration object</span></span>

### <a name="step-1"></a><span data-ttu-id="6d4fa-160">步驟 1</span><span class="sxs-lookup"><span data-stu-id="6d4fa-160">Step 1</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

<span data-ttu-id="6d4fa-161">這個步驟會建立名為 "gatewayIP01" 的應用程式閘道 IP 組態。</span><span class="sxs-lookup"><span data-stu-id="6d4fa-161">This step creates an application gateway IP configuration named "gatewayIP01".</span></span> <span data-ttu-id="6d4fa-162">應用程式閘道啟動時，它會挑選設定 hello 子網路的 IP 位址，並傳送 hello 後端 IP 集區中的網路流量 toohello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="6d4fa-162">When Application Gateway starts, it picks up an IP address from hello subnet configured and route network traffic toohello IP addresses in hello back-end IP pool.</span></span> <span data-ttu-id="6d4fa-163">請記住，每個執行個體需要一個 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="6d4fa-163">Keep in mind that each instance takes one IP address.</span></span>

### <a name="step-2"></a><span data-ttu-id="6d4fa-164">步驟 2</span><span class="sxs-lookup"><span data-stu-id="6d4fa-164">Step 2</span></span>

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 10.1.1.8,10.1.1.9,10.1.1.10
```

<span data-ttu-id="6d4fa-165">此步驟會設定 hello 後端 IP 位址集區名稱為"10.1.1.8、 10.1.1.9，10.1.1.10"，"pool01 」 ip 位址。</span><span class="sxs-lookup"><span data-stu-id="6d4fa-165">This step configures hello back-end IP address pool named "pool01" with IP addresses "10.1.1.8, 10.1.1.9, 10.1.1.10".</span></span> <span data-ttu-id="6d4fa-166">這些是 hello 收到 hello 來自 hello 前端 IP 端點的網路流量的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="6d4fa-166">Those are hello IP addresses that receive hello network traffic that comes from hello front-end IP endpoint.</span></span> <span data-ttu-id="6d4fa-167">取代先前的 IP 位址 tooadd hello 您自己的應用程式的 IP 位址端點。</span><span class="sxs-lookup"><span data-stu-id="6d4fa-167">You replace hello preceding IP addresses tooadd your own application IP address endpoints.</span></span>

### <a name="step-3"></a><span data-ttu-id="6d4fa-168">步驟 3</span><span class="sxs-lookup"><span data-stu-id="6d4fa-168">Step 3</span></span>

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Disabled
```

<span data-ttu-id="6d4fa-169">此步驟會在 hello 後端集區中設定應用程式閘道設定 「 poolsetting01"hello 負載平衡網路流量。</span><span class="sxs-lookup"><span data-stu-id="6d4fa-169">This step configures application gateway setting "poolsetting01" for hello load balanced network traffic in hello back-end pool.</span></span>

### <a name="step-4"></a><span data-ttu-id="6d4fa-170">步驟 4</span><span class="sxs-lookup"><span data-stu-id="6d4fa-170">Step 4</span></span>

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 80
```

<span data-ttu-id="6d4fa-171">此步驟會設定名為"frontendport01"hello ILB hello 前端 IP 連接埠。</span><span class="sxs-lookup"><span data-stu-id="6d4fa-171">This step configures hello front-end IP port named "frontendport01" for hello ILB.</span></span>

### <a name="step-5"></a><span data-ttu-id="6d4fa-172">步驟 5</span><span class="sxs-lookup"><span data-stu-id="6d4fa-172">Step 5</span></span>

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -Subnet $subnet
```

<span data-ttu-id="6d4fa-173">這個步驟會建立 hello 稱為 「 fipconfig01"前端 IP 組態，並與私人 IP 從 hello 目前虛擬網路子網路產生關聯。</span><span class="sxs-lookup"><span data-stu-id="6d4fa-173">This step creates hello front-end IP configuration called "fipconfig01" and associates it with a private IP from hello current virtual network subnet.</span></span>

### <a name="step-6"></a><span data-ttu-id="6d4fa-174">步驟 6</span><span class="sxs-lookup"><span data-stu-id="6d4fa-174">Step 6</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp
```

<span data-ttu-id="6d4fa-175">此步驟會建立稱為 「 listener01"hello 接聽程式，並將 hello 前端連接埠 toohello 前端 IP 組態。</span><span class="sxs-lookup"><span data-stu-id="6d4fa-175">This step creates hello listener called "listener01" and associates hello front-end port toohello front-end IP configuration.</span></span>

### <a name="step-7"></a><span data-ttu-id="6d4fa-176">步驟 7</span><span class="sxs-lookup"><span data-stu-id="6d4fa-176">Step 7</span></span>

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

<span data-ttu-id="6d4fa-177">此步驟建立 hello 負載平衡器路由規則稱為 「 rule01"，設定 hello 負載平衡器行為。</span><span class="sxs-lookup"><span data-stu-id="6d4fa-177">This step creates hello load balancer routing rule called "rule01" that configures hello load balancer behavior.</span></span>

### <a name="step-8"></a><span data-ttu-id="6d4fa-178">步驟 8</span><span class="sxs-lookup"><span data-stu-id="6d4fa-178">Step 8</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

<span data-ttu-id="6d4fa-179">此步驟會設定 hello hello 應用程式閘道執行個體大小。</span><span class="sxs-lookup"><span data-stu-id="6d4fa-179">This step configures hello instance size of hello application gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="6d4fa-180">預設值的 hello *InstanceCount*為 2，最大值是 10。</span><span class="sxs-lookup"><span data-stu-id="6d4fa-180">hello default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="6d4fa-181">預設值的 hello *GatewaySize*都是 Medium。</span><span class="sxs-lookup"><span data-stu-id="6d4fa-181">hello default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="6d4fa-182">您可以在 Standard_Small、Standard_Medium 和 Standard_Large 之間選擇。</span><span class="sxs-lookup"><span data-stu-id="6d4fa-182">You can choose between Standard_Small, Standard_Medium, and Standard_Large.</span></span>

## <a name="create-an-application-gateway-by-using-new-azureapplicationgateway"></a><span data-ttu-id="6d4fa-183">使用 New-AzureApplicationGateway 建立應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="6d4fa-183">Create an application gateway by using New-AzureApplicationGateway</span></span>

<span data-ttu-id="6d4fa-184">建立應用程式閘道的 hello 先前步驟中的所有組態項目。</span><span class="sxs-lookup"><span data-stu-id="6d4fa-184">Creates an application gateway with all configuration items from hello preceding steps.</span></span> <span data-ttu-id="6d4fa-185">在此範例中，hello 應用程式閘道又稱為 「 appgwtest"。</span><span class="sxs-lookup"><span data-stu-id="6d4fa-185">In this example, hello application gateway is called "appgwtest".</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku
```

<span data-ttu-id="6d4fa-186">此步驟會建立應用程式閘道的 hello 先前步驟中的所有組態項目。</span><span class="sxs-lookup"><span data-stu-id="6d4fa-186">This step creates an application gateway with all configuration items from hello preceding steps.</span></span> <span data-ttu-id="6d4fa-187">在 hello 範例 hello 應用程式閘道又稱為 「 appgwtest"。</span><span class="sxs-lookup"><span data-stu-id="6d4fa-187">In hello example, hello application gateway is called "appgwtest".</span></span>

## <a name="delete-an-application-gateway"></a><span data-ttu-id="6d4fa-188">刪除應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="6d4fa-188">Delete an application gateway</span></span>

<span data-ttu-id="6d4fa-189">toodelete 應用程式閘道，您需要下列步驟順序 toodo hello:</span><span class="sxs-lookup"><span data-stu-id="6d4fa-189">toodelete an application gateway, you need toodo hello following steps in order:</span></span>

1. <span data-ttu-id="6d4fa-190">使用 hello `Stop-AzureRmApplicationGateway` cmdlet toostop hello 閘道。</span><span class="sxs-lookup"><span data-stu-id="6d4fa-190">Use hello `Stop-AzureRmApplicationGateway` cmdlet toostop hello gateway.</span></span>
2. <span data-ttu-id="6d4fa-191">使用 hello `Remove-AzureRmApplicationGateway` cmdlet tooremove hello 閘道。</span><span class="sxs-lookup"><span data-stu-id="6d4fa-191">Use hello `Remove-AzureRmApplicationGateway` cmdlet tooremove hello gateway.</span></span>
3. <span data-ttu-id="6d4fa-192">確認已移除該 hello 閘道使用 hello `Get-AzureApplicationGateway` cmdlet。</span><span class="sxs-lookup"><span data-stu-id="6d4fa-192">Verify that hello gateway has been removed by using hello `Get-AzureApplicationGateway` cmdlet.</span></span>

### <a name="step-1"></a><span data-ttu-id="6d4fa-193">步驟 1</span><span class="sxs-lookup"><span data-stu-id="6d4fa-193">Step 1</span></span>

<span data-ttu-id="6d4fa-194">取得 hello 應用程式閘道物件，並將它 tooa 變數 」 $getgw"。</span><span class="sxs-lookup"><span data-stu-id="6d4fa-194">Get hello application gateway object and associate it tooa variable "$getgw".</span></span>

```powershell
$getgw =  Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg
```

### <a name="step-2"></a><span data-ttu-id="6d4fa-195">步驟 2</span><span class="sxs-lookup"><span data-stu-id="6d4fa-195">Step 2</span></span>

<span data-ttu-id="6d4fa-196">使用`Stop-AzureRmApplicationGateway`toostop hello 應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="6d4fa-196">Use `Stop-AzureRmApplicationGateway` toostop hello application gateway.</span></span> <span data-ttu-id="6d4fa-197">這個範例會顯示 hello `Stop-AzureRmApplicationGateway` cmdlet hello 第一行，後面接著 hello 輸出。</span><span class="sxs-lookup"><span data-stu-id="6d4fa-197">This sample shows hello `Stop-AzureRmApplicationGateway` cmdlet on hello first line, followed by hello output.</span></span>

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

<span data-ttu-id="6d4fa-198">處於停止狀態 hello 應用程式閘道之後，請使用 hello `Remove-AzureRmApplicationGateway` cmdlet tooremove hello 服務。</span><span class="sxs-lookup"><span data-stu-id="6d4fa-198">Once hello application gateway is in a stopped state, use hello `Remove-AzureRmApplicationGateway` cmdlet tooremove hello service.</span></span>

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
> <span data-ttu-id="6d4fa-199">hello **-強制**參數可以是使用的 toosuppress hello 移除確認訊息。</span><span class="sxs-lookup"><span data-stu-id="6d4fa-199">hello **-force** switch can be used toosuppress hello remove confirmation message.</span></span>

<span data-ttu-id="6d4fa-200">已移除 hello 服務的 tooverify，您可以使用 hello `Get-AzureRmApplicationGateway` cmdlet。</span><span class="sxs-lookup"><span data-stu-id="6d4fa-200">tooverify that hello service has been removed, you can use hello `Get-AzureRmApplicationGateway` cmdlet.</span></span> <span data-ttu-id="6d4fa-201">這不是必要步驟。</span><span class="sxs-lookup"><span data-stu-id="6d4fa-201">This step is not required.</span></span>

```powershell
Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg
```

```
VERBOSE: 10:52:46 PM - Begin Operation: Get-AzureApplicationGateway

Get-AzureApplicationGateway : ResourceNotFound: hello gateway does not exist.
```

## <a name="next-steps"></a><span data-ttu-id="6d4fa-202">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6d4fa-202">Next steps</span></span>

<span data-ttu-id="6d4fa-203">如果您想的 tooconfigure SSL 卸載，請參閱[設定 SSL 卸載的應用程式閘道](application-gateway-ssl.md)。</span><span class="sxs-lookup"><span data-stu-id="6d4fa-203">If you want tooconfigure SSL offload, see [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="6d4fa-204">如果您想 tooconfigure 搭配 ILB 一起運作的應用程式閘道 toouse，請參閱[內部負載平衡器 (ILB) 建立應用程式閘道](application-gateway-ilb.md)。</span><span class="sxs-lookup"><span data-stu-id="6d4fa-204">If you want tooconfigure an application gateway toouse with an ILB, see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="6d4fa-205">如果您想進一步了解一般負載平衡選項，請參閱：</span><span class="sxs-lookup"><span data-stu-id="6d4fa-205">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="6d4fa-206">Azure 負載平衡器</span><span class="sxs-lookup"><span data-stu-id="6d4fa-206">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="6d4fa-207">Azure 流量管理員</span><span class="sxs-lookup"><span data-stu-id="6d4fa-207">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

