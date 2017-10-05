---
title: "設定 SSL 卸載 - Azure 應用程式閘道 - PowerShell | Microsoft Docs"
description: "本頁面提供使用 Azure 資源管理員範本，建立具有 SSL 卸載之應用程式閘道的指示。"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 3c3681e0-f928-4682-9d97-567f8e278e13
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: ededabc7c665d6bb05b91e4d21d01fb1379add32
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-azure-resource-manager"></a><span data-ttu-id="9ce7c-103">使用 Azure 資源管理員設定適用於 SSL 的應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="9ce7c-103">Configure an application gateway for SSL offload by using Azure Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="9ce7c-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="9ce7c-104">Azure portal</span></span>](application-gateway-ssl-portal.md)
> * [<span data-ttu-id="9ce7c-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="9ce7c-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ssl-arm.md)
> * [<span data-ttu-id="9ce7c-106">Azure 傳統 PowerShell</span><span class="sxs-lookup"><span data-stu-id="9ce7c-106">Azure Classic PowerShell</span></span>](application-gateway-ssl.md)
> * [<span data-ttu-id="9ce7c-107">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="9ce7c-107">Azure CLI 2.0</span></span>](application-gateway-ssl-cli.md)

<span data-ttu-id="9ce7c-108">Azure 應用程式閘道可以設定為在閘道終止安全通訊端層 (SSL) 工作階段，以避免 Web 伺服陣列發生高成本的 SSL 解密工作。</span><span class="sxs-lookup"><span data-stu-id="9ce7c-108">Azure Application Gateway can be configured to terminate the Secure Sockets Layer (SSL) session at the gateway to avoid costly SSL decryption tasks to happen at the web farm.</span></span> <span data-ttu-id="9ce7c-109">SSL 卸載也可以簡化 Web 應用程式的前端伺服器設定和管理。</span><span class="sxs-lookup"><span data-stu-id="9ce7c-109">SSL offload also simplifies the front-end server setup and management of the web application.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="9ce7c-110">開始之前</span><span class="sxs-lookup"><span data-stu-id="9ce7c-110">Before you begin</span></span>

1. <span data-ttu-id="9ce7c-111">使用 Web Platform Installer 安裝最新版的 Azure PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="9ce7c-111">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span></span> <span data-ttu-id="9ce7c-112">您可以從 **下載頁面** 的 [Windows PowerShell](https://azure.microsoft.com/downloads/)區段下載並安裝最新版本。</span><span class="sxs-lookup"><span data-stu-id="9ce7c-112">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="9ce7c-113">建立應用程式閘道的虛擬網路和子網路。</span><span class="sxs-lookup"><span data-stu-id="9ce7c-113">You create a virtual network and a subnet for the application gateway.</span></span> <span data-ttu-id="9ce7c-114">請確定沒有虛擬機器或是雲端部署正在使用子網路。</span><span class="sxs-lookup"><span data-stu-id="9ce7c-114">Make sure that no virtual machines or cloud deployments are using the subnet.</span></span> <span data-ttu-id="9ce7c-115">應用程式閘道必須單獨在虛擬網路子網路中。</span><span class="sxs-lookup"><span data-stu-id="9ce7c-115">Application Gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="9ce7c-116">您要設定來使用應用程式閘道的伺服器必須存在，或是在虛擬網路中建立其端點，或是已指派公用 IP/VIP。</span><span class="sxs-lookup"><span data-stu-id="9ce7c-116">The servers you configure to use the application gateway must exist or have their endpoints created either in the virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-to-create-an-application-gateway"></a><span data-ttu-id="9ce7c-117">建立應用程式閘道需要什麼？</span><span class="sxs-lookup"><span data-stu-id="9ce7c-117">What is required to create an application gateway?</span></span>

* <span data-ttu-id="9ce7c-118">**後端伺服器集區：** 後端伺服器的 IP 位址清單。</span><span class="sxs-lookup"><span data-stu-id="9ce7c-118">**Back-end server pool:** The list of IP addresses of the back-end servers.</span></span> <span data-ttu-id="9ce7c-119">列出的 IP 位址應屬於虛擬網路子網路或是公用 IP/VIP。</span><span class="sxs-lookup"><span data-stu-id="9ce7c-119">The IP addresses listed should either belong to the virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="9ce7c-120">**後端伺服器集區設定：** 每個集區都包括一些設定，例如連接埠、通訊協定和以 Cookie 為基礎的同質性。</span><span class="sxs-lookup"><span data-stu-id="9ce7c-120">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="9ce7c-121">這些設定會繫結至集區，並套用至集區內所有伺服器。</span><span class="sxs-lookup"><span data-stu-id="9ce7c-121">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="9ce7c-122">**前端連接埠：** 此連接埠是在應用程式閘道上開啟的公用連接埠。</span><span class="sxs-lookup"><span data-stu-id="9ce7c-122">**Front-end port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="9ce7c-123">流量會達到此連接埠，然後重新導向至其中一個後端伺服器。</span><span class="sxs-lookup"><span data-stu-id="9ce7c-123">Traffic hits this port, and then gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="9ce7c-124">**接聽程式：** 接聽程式具有前端連接埠、通訊協定 (Http 或 Https，這些設定都區分大小寫) 和 SSL 憑證名稱 (如果已設定 SSL 卸載)。</span><span class="sxs-lookup"><span data-stu-id="9ce7c-124">**Listener:** The listener has a front-end port, a protocol (Http or Https, these settings are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="9ce7c-125">**規則：** 規則會繫結接聽程式和後端伺服器集區，並定義流量達到特定接聽程式時應該導向至哪個後端伺服器集區。</span><span class="sxs-lookup"><span data-stu-id="9ce7c-125">**Rule:** The rule binds the listener and the back-end server pool and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span></span> <span data-ttu-id="9ce7c-126">目前只支援 *基本* 規則。</span><span class="sxs-lookup"><span data-stu-id="9ce7c-126">Currently, only the *basic* rule is supported.</span></span> <span data-ttu-id="9ce7c-127">*基本* 規則是循環配置資源的負載分配。</span><span class="sxs-lookup"><span data-stu-id="9ce7c-127">The *basic* rule is round-robin load distribution.</span></span>

<span data-ttu-id="9ce7c-128">**其他組態注意事項**</span><span class="sxs-lookup"><span data-stu-id="9ce7c-128">**Additional configuration notes**</span></span>

<span data-ttu-id="9ce7c-129">針對 SSL 憑證組態，**HttpListener** 中的通訊協定應該變更為 *Https* (區分大小寫)。</span><span class="sxs-lookup"><span data-stu-id="9ce7c-129">For SSL certificates configuration, the protocol in **HttpListener** should change to *Https* (case sensitive).</span></span> <span data-ttu-id="9ce7c-130">將 **SslCertificate** 元素新增至 **HttpListener**，並針對 SSL 憑證設定變數值。</span><span class="sxs-lookup"><span data-stu-id="9ce7c-130">The **SslCertificate** element is added to **HttpListener** with the variable value configured for the SSL certificate.</span></span> <span data-ttu-id="9ce7c-131">前端連接埠應該更新為 443。</span><span class="sxs-lookup"><span data-stu-id="9ce7c-131">The front-end port should be updated to 443.</span></span>

<span data-ttu-id="9ce7c-132">**啟用以 Cookie 為基礎的同質性**：您可以設定應用程式閘道，以確保來自用戶端工作階段的要求一律會導向至 Web 伺服陣列中的相同 VM。</span><span class="sxs-lookup"><span data-stu-id="9ce7c-132">**To enable cookie-based affinity**: An application gateway can be configured to ensure that a request from a client session is always directed to the same VM in the web farm.</span></span> <span data-ttu-id="9ce7c-133">此案例透過插入允許閘道適當導向流量的工作階段 Cookie 來完成。</span><span class="sxs-lookup"><span data-stu-id="9ce7c-133">This scenario is done by injection of a session cookie that allows the gateway to direct traffic appropriately.</span></span> <span data-ttu-id="9ce7c-134">若要啟用以 Cookie 為基礎的同質性，請在 **BackendHttpSettings** 元素中將 **CookieBasedAffinity** 設定為 *Enabled*。</span><span class="sxs-lookup"><span data-stu-id="9ce7c-134">To enable cookie-based affinity, set **CookieBasedAffinity** to *Enabled* in the **BackendHttpSettings** element.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="9ce7c-135">建立應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="9ce7c-135">Create an application gateway</span></span>

<span data-ttu-id="9ce7c-136">使用 Azure 傳統部署模型和 Azure Resource Manager 的差別，在於您建立應用程式閘道和需設定項目的順序。</span><span class="sxs-lookup"><span data-stu-id="9ce7c-136">The difference between using the Azure Classic deployment model and Azure Resource Manager is the order that you create an application gateway and the items that need to be configured.</span></span>

<span data-ttu-id="9ce7c-137">透過 Resource Manager，應用程式閘道的所有元件會個別進行設定，然後放在一起建立應用程式閘道資源。</span><span class="sxs-lookup"><span data-stu-id="9ce7c-137">With Resource Manager, all components of an application gateway are configured individually and then put together to create an application gateway resource.</span></span>

<span data-ttu-id="9ce7c-138">以下是建立應用程式閘道所需的步驟：</span><span class="sxs-lookup"><span data-stu-id="9ce7c-138">Here are the steps needed to create an application gateway:</span></span>

1. <span data-ttu-id="9ce7c-139">建立資源管理員的資源群組</span><span class="sxs-lookup"><span data-stu-id="9ce7c-139">Create a resource group for Resource Manager</span></span>
2. <span data-ttu-id="9ce7c-140">建立應用程式閘道的虛擬網路、子網路和公用 IP</span><span class="sxs-lookup"><span data-stu-id="9ce7c-140">Create virtual network, subnet, and public IP for the application gateway</span></span>
3. <span data-ttu-id="9ce7c-141">建立應用程式閘道組態物件</span><span class="sxs-lookup"><span data-stu-id="9ce7c-141">Create an application gateway configuration object</span></span>
4. <span data-ttu-id="9ce7c-142">建立應用程式閘道資源</span><span class="sxs-lookup"><span data-stu-id="9ce7c-142">Create an application gateway resource</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="9ce7c-143">建立資源管理員的資源群組</span><span class="sxs-lookup"><span data-stu-id="9ce7c-143">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="9ce7c-144">請確定您切換 PowerShell 模式以使用 Azure 資源管理員 Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="9ce7c-144">Make sure that you switch PowerShell mode to use the Azure Resource Manager cmdlets.</span></span> <span data-ttu-id="9ce7c-145">如需詳細資訊，可在 [搭配使用 Windows PowerShell 與資源管理員](../powershell-azure-resource-manager.md)取得。</span><span class="sxs-lookup"><span data-stu-id="9ce7c-145">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="9ce7c-146">步驟 1</span><span class="sxs-lookup"><span data-stu-id="9ce7c-146">Step 1</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="9ce7c-147">步驟 2</span><span class="sxs-lookup"><span data-stu-id="9ce7c-147">Step 2</span></span>

<span data-ttu-id="9ce7c-148">檢查帳戶的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="9ce7c-148">Check the subscriptions for the account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="9ce7c-149">系統會提示使用您的認證進行驗證。</span><span class="sxs-lookup"><span data-stu-id="9ce7c-149">You are prompted to authenticate with your credentials.</span></span>

### <a name="step-3"></a><span data-ttu-id="9ce7c-150">步驟 3</span><span class="sxs-lookup"><span data-stu-id="9ce7c-150">Step 3</span></span>

<span data-ttu-id="9ce7c-151">選擇要使用哪一個 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="9ce7c-151">Choose which of your Azure subscriptions to use.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="9ce7c-152">步驟 4</span><span class="sxs-lookup"><span data-stu-id="9ce7c-152">Step 4</span></span>

<span data-ttu-id="9ce7c-153">建立資源群組 (若使用現有的資源群組，請略過此步驟)。</span><span class="sxs-lookup"><span data-stu-id="9ce7c-153">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

<span data-ttu-id="9ce7c-154">Azure 資源管理員需要所有的資源群組指定一個位置。</span><span class="sxs-lookup"><span data-stu-id="9ce7c-154">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="9ce7c-155">此設定用來作為該資源群組中資源的預設位置。</span><span class="sxs-lookup"><span data-stu-id="9ce7c-155">This setting is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="9ce7c-156">請確定所有用來建立應用程式閘道的命令都使用同一個資源群組。</span><span class="sxs-lookup"><span data-stu-id="9ce7c-156">Make sure that all commands to create an application gateway uses the same resource group.</span></span>

<span data-ttu-id="9ce7c-157">在上述範例中，我們建立名為 **appgw-RG** 的資源群組，且位置為 **West US** (美國西部)。</span><span class="sxs-lookup"><span data-stu-id="9ce7c-157">In the example above, we created a resource group called **appgw-RG** and location **West US**.</span></span>

## <a name="create-a-virtual-network-and-a-subnet-for-the-application-gateway"></a><span data-ttu-id="9ce7c-158">建立應用程式閘道的虛擬網路和子網路</span><span class="sxs-lookup"><span data-stu-id="9ce7c-158">Create a virtual network and a subnet for the application gateway</span></span>

<span data-ttu-id="9ce7c-159">下面的範例說明如何使用資源管理員建立虛擬網路：</span><span class="sxs-lookup"><span data-stu-id="9ce7c-159">The following example shows how to create a virtual network by using Resource Manager:</span></span>

### <a name="step-1"></a><span data-ttu-id="9ce7c-160">步驟 1</span><span class="sxs-lookup"><span data-stu-id="9ce7c-160">Step 1</span></span>

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

<span data-ttu-id="9ce7c-161">此範例會將位址範圍 10.0.0.0/24 指派給用於建立虛擬網路的子網路變數。</span><span class="sxs-lookup"><span data-stu-id="9ce7c-161">This sample assigns the address range 10.0.0.0/24 to a subnet variable to be used to create a virtual network.</span></span>

### <a name="step-2"></a><span data-ttu-id="9ce7c-162">步驟 2</span><span class="sxs-lookup"><span data-stu-id="9ce7c-162">Step 2</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet
```

<span data-ttu-id="9ce7c-163">此範例會使用前置詞 10.0.0.0/16 搭配子網路 10.0.0.0/24，在美國西部 (West US) 區域的 **appgw-rg** 資源群組中建立名為 **appgwvnet** 的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="9ce7c-163">This sample creates a virtual network named **appgwvnet** in resource group **appgw-rg** for the West US region using the prefix 10.0.0.0/16 with subnet 10.0.0.0/24.</span></span>

### <a name="step-3"></a><span data-ttu-id="9ce7c-164">步驟 3</span><span class="sxs-lookup"><span data-stu-id="9ce7c-164">Step 3</span></span>

```powershell
$subnet = $vnet.Subnets[0]
```

<span data-ttu-id="9ce7c-165">此範例會將子網路物件指派給下一個步驟的變數 $subnet。</span><span class="sxs-lookup"><span data-stu-id="9ce7c-165">This sample assigns the subnet object to variable $subnet for the next steps.</span></span>

## <a name="create-a-public-ip-address-for-the-front-end-configuration"></a><span data-ttu-id="9ce7c-166">建立前端組態的公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="9ce7c-166">Create a public IP address for the front-end configuration</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="9ce7c-167">此範例會在美國西部區域的 **appgw-rg** 資源群組中建立公用 IP 資源 **publicIP01**。</span><span class="sxs-lookup"><span data-stu-id="9ce7c-167">This sample creates a public IP resource **publicIP01** in resource group **appgw-rg** for the West US region.</span></span>

## <a name="create-an-application-gateway-configuration-object"></a><span data-ttu-id="9ce7c-168">建立應用程式閘道組態物件</span><span class="sxs-lookup"><span data-stu-id="9ce7c-168">Create an application gateway configuration object</span></span>

### <a name="step-1"></a><span data-ttu-id="9ce7c-169">步驟 1</span><span class="sxs-lookup"><span data-stu-id="9ce7c-169">Step 1</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

<span data-ttu-id="9ce7c-170">此範例會建立名為 **gatewayIP01** 的應用程式閘道 IP 組態。</span><span class="sxs-lookup"><span data-stu-id="9ce7c-170">This sample creates an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="9ce7c-171">當「應用程式閘道」啟動時，它會從已設定的子網路取得 IP 位址，再將網路流量路由傳送到後端 IP 集區中的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="9ce7c-171">When Application Gateway starts, it picks up an IP address from the subnet configured and route network traffic to the IP addresses in the back-end IP pool.</span></span> <span data-ttu-id="9ce7c-172">請記住，每個執行個體需要一個 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="9ce7c-172">Keep in mind that each instance takes one IP address.</span></span>

### <a name="step-2"></a><span data-ttu-id="9ce7c-173">步驟 2</span><span class="sxs-lookup"><span data-stu-id="9ce7c-173">Step 2</span></span>

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221,134.170.185.50
```

<span data-ttu-id="9ce7c-174">此範例會設定名為 **pool01** 的後端 IP 位址集區，其 IP 位址有 **134.170.185.46**、**134.170.188.221**、**134.170.185.50**。</span><span class="sxs-lookup"><span data-stu-id="9ce7c-174">This sample configures the back-end IP address pool named **pool01** with IP addresses **134.170.185.46**, **134.170.188.221**, **134.170.185.50**.</span></span> <span data-ttu-id="9ce7c-175">這些值為 IP 位址，可接收來自前端 IP 端點的網路流量。</span><span class="sxs-lookup"><span data-stu-id="9ce7c-175">Those values are the IP addresses that receive the network traffic that comes from the front-end IP endpoint.</span></span> <span data-ttu-id="9ce7c-176">以您的 Web 應用程式端點的 IP 位址取代前述範例中的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="9ce7c-176">Replace the IP addresses from the preceding example with the IP addresses of your web application endpoints.</span></span>

### <a name="step-3"></a><span data-ttu-id="9ce7c-177">步驟 3</span><span class="sxs-lookup"><span data-stu-id="9ce7c-177">Step 3</span></span>

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Enabled
```

<span data-ttu-id="9ce7c-178">此範例會設定後端集區中負載平衡網路流量的應用程式閘道設定 **poolsetting01**。</span><span class="sxs-lookup"><span data-stu-id="9ce7c-178">This sample configures application gateway setting **poolsetting01** to load-balanced network traffic in the back-end pool.</span></span>

### <a name="step-4"></a><span data-ttu-id="9ce7c-179">步驟 4</span><span class="sxs-lookup"><span data-stu-id="9ce7c-179">Step 4</span></span>

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 443
```

<span data-ttu-id="9ce7c-180">此範例會設定公用 IP 端點的前端 IP 連接埠 **frontendport01**。</span><span class="sxs-lookup"><span data-stu-id="9ce7c-180">This sample configures the front-end IP port named **frontendport01** for the public IP endpoint.</span></span>

### <a name="step-5"></a><span data-ttu-id="9ce7c-181">步驟 5</span><span class="sxs-lookup"><span data-stu-id="9ce7c-181">Step 5</span></span>

```powershell
$cert = New-AzureRmApplicationGatewaySslCertificate -Name cert01 -CertificateFile <full path for certificate file> -Password "<password>"
```

<span data-ttu-id="9ce7c-182">此範例會設定 SSL 連接所使用的憑證。</span><span class="sxs-lookup"><span data-stu-id="9ce7c-182">This sample configures the certificate used for SSL connection.</span></span> <span data-ttu-id="9ce7c-183">憑證必須是 .pfx 格式，而密碼則必須介於 4 到 12 個字元。</span><span class="sxs-lookup"><span data-stu-id="9ce7c-183">The certificate needs to be in .pfx format, and the password must be between 4 to 12 characters.</span></span>

### <a name="step-6"></a><span data-ttu-id="9ce7c-184">步驟 6</span><span class="sxs-lookup"><span data-stu-id="9ce7c-184">Step 6</span></span>

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip
```

<span data-ttu-id="9ce7c-185">此範例會建立名為 **fipconfig01** 的前端 IP 組態，並將公用 IP 位址與前端 IP 組態產生關聯。</span><span class="sxs-lookup"><span data-stu-id="9ce7c-185">This sample creates the front-end IP configuration named **fipconfig01** and associates the public IP address with the front-end IP configuration.</span></span>

### <a name="step-7"></a><span data-ttu-id="9ce7c-186">步驟 7</span><span class="sxs-lookup"><span data-stu-id="9ce7c-186">Step 7</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SslCertificate $cert
```

<span data-ttu-id="9ce7c-187">此範例會建立名為 **listener01** 的接聽程式，並將前端連接埠與前端 IP 組態和憑證產生關聯。</span><span class="sxs-lookup"><span data-stu-id="9ce7c-187">This sample creates the listener name **listener01** and associates the front-end port to the front-end IP configuration and certificate.</span></span>

### <a name="step-8"></a><span data-ttu-id="9ce7c-188">步驟 8</span><span class="sxs-lookup"><span data-stu-id="9ce7c-188">Step 8</span></span>

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

<span data-ttu-id="9ce7c-189">此範例會建立名為 **rule01** 的負載平衡器路由規則，設定負載平衡器的行為。</span><span class="sxs-lookup"><span data-stu-id="9ce7c-189">This sample creates the load balancer routing rule named **rule01** that configures the load balancer behavior.</span></span>

### <a name="step-9"></a><span data-ttu-id="9ce7c-190">步驟 9</span><span class="sxs-lookup"><span data-stu-id="9ce7c-190">Step 9</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

<span data-ttu-id="9ce7c-191">此範例會設定應用程式閘道的執行個體大小。</span><span class="sxs-lookup"><span data-stu-id="9ce7c-191">This sample configures the instance size of the application gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="9ce7c-192">*InstanceCount* 的預設值是 2，且最大值是 10。</span><span class="sxs-lookup"><span data-stu-id="9ce7c-192">The default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="9ce7c-193">GatewaySize  的預設值是 Medium。</span><span class="sxs-lookup"><span data-stu-id="9ce7c-193">The default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="9ce7c-194">您可以在 Standard_Small、Standard_Medium 和 Standard_Large 之間選擇。</span><span class="sxs-lookup"><span data-stu-id="9ce7c-194">You can choose between Standard_Small, Standard_Medium, and Standard_Large.</span></span>

### <a name="step-10"></a><span data-ttu-id="9ce7c-195">步驟 10</span><span class="sxs-lookup"><span data-stu-id="9ce7c-195">Step 10</span></span>

```powershell
$policy = New-AzureRmApplicationGatewaySslPolicy -PolicyType Predefined -PolicyName AppGwSslPolicy20170401S
```

<span data-ttu-id="9ce7c-196">這個步驟會定義要在應用程式閘道上使用的 SSL 原則。</span><span class="sxs-lookup"><span data-stu-id="9ce7c-196">This step defines the SSL policy to use on the application gateway.</span></span> <span data-ttu-id="9ce7c-197">請參閱[在應用程式閘道上設定 SSL 原則版本和加密套件](application-gateway-configure-ssl-policy-powershell.md)以深入了解。</span><span class="sxs-lookup"><span data-stu-id="9ce7c-197">Visit [Configure SSL policy versions and cipher suites on Application Gateway](application-gateway-configure-ssl-policy-powershell.md) to learn more.</span></span>

## <a name="create-an-application-gateway-by-using-new-azureapplicationgateway"></a><span data-ttu-id="9ce7c-198">使用 New-AzureApplicationGateway 建立應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="9ce7c-198">Create an application gateway by using New-AzureApplicationGateway</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SslCertificates $cert -SslPolicy $policy
```

<span data-ttu-id="9ce7c-199">此範例利用上述步驟中的所有組態項目來建立應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="9ce7c-199">This sample creates an application gateway with all configuration items from the preceding steps.</span></span> <span data-ttu-id="9ce7c-200">範例中的應用程式閘道名為 **appgwtest**。</span><span class="sxs-lookup"><span data-stu-id="9ce7c-200">In the example, the application gateway is called **appgwtest**.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="9ce7c-201">取得應用程式閘道 DNS 名稱</span><span class="sxs-lookup"><span data-stu-id="9ce7c-201">Get application gateway DNS name</span></span>

<span data-ttu-id="9ce7c-202">建立閘道之後，下一步是設定通訊的前端。</span><span class="sxs-lookup"><span data-stu-id="9ce7c-202">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="9ce7c-203">當使用公用 IP 時，應用程式閘道需要動態指派的 DNS 名稱 (不易記住)。</span><span class="sxs-lookup"><span data-stu-id="9ce7c-203">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="9ce7c-204">為了確保使用者可以叫用應用程式閘道，可使用 CNAME 記錄來指向應用程式閘道的公用端點。</span><span class="sxs-lookup"><span data-stu-id="9ce7c-204">To ensure end users can hit the application gateway, a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="9ce7c-205">[在 Azure 中設定自訂網域名稱](../cloud-services/cloud-services-custom-domain-name-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="9ce7c-205">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="9ce7c-206">做法是使用連接至應用程式閘道的 PublicIPAddress 元素，擷取應用程式閘道的詳細資料及其關聯的 IP/DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="9ce7c-206">To do this, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="9ce7c-207">應用程式閘道的 DNS 名稱應該用來建立將兩個 Web 應用程式指向此 DNS 名稱的 CNAME 記錄。</span><span class="sxs-lookup"><span data-stu-id="9ce7c-207">The application gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span></span> <span data-ttu-id="9ce7c-208">不建議使用 A-records，因為重新啟動應用程式閘道時，VIP 可能會變更。</span><span class="sxs-lookup"><span data-stu-id="9ce7c-208">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>


```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -Name publicIP01
```

```
Name                     : publicIP01
ResourceGroupName        : appgw-RG
Location                 : westus
Id                       : /subscriptions/<subscription_id>/resourceGroups/appgw-RG/providers/Microsoft.Network/publicIPAddresses/publicIP01
Etag                     : W/"00000d5b-54ed-4907-bae8-99bd5766d0e5"
ResourceGuid             : 00000000-0000-0000-0000-000000000000
ProvisioningState        : Succeeded
Tags                     : 
PublicIpAllocationMethod : Dynamic
IpAddress                : xx.xx.xxx.xx
PublicIpAddressVersion   : IPv4
IdleTimeoutInMinutes     : 4
IpConfiguration          : {
                                "Id": "/subscriptions/<subscription_id>/resourceGroups/appgw-RG/providers/Microsoft.Network/applicationGateways/appgwtest/frontendIP
                            Configurations/frontend1"
                            }
DnsSettings              : {
                                "Fqdn": "00000000-0000-xxxx-xxxx-xxxxxxxxxxxx.cloudapp.net"
                            }
```

## <a name="next-steps"></a><span data-ttu-id="9ce7c-209">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9ce7c-209">Next steps</span></span>

<span data-ttu-id="9ce7c-210">如果您想要將應用程式閘道設為與內部負載平衡器 (ILB) 搭配使用，請參閱 [建立具有內部負載平衡器 (ILB) 的應用程式閘道](application-gateway-ilb.md)。</span><span class="sxs-lookup"><span data-stu-id="9ce7c-210">If you want to configure an application gateway to use with an internal load balancer (ILB), see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="9ce7c-211">如果您想進一步了解一般負載平衡選項，請參閱：</span><span class="sxs-lookup"><span data-stu-id="9ce7c-211">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="9ce7c-212">Azure 負載平衡器</span><span class="sxs-lookup"><span data-stu-id="9ce7c-212">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="9ce7c-213">Azure 流量管理員</span><span class="sxs-lookup"><span data-stu-id="9ce7c-213">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

