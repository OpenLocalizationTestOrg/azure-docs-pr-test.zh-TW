---
title: "aaaConfigure SSL 卸載 Azure 應用程式閘道-PowerShell |Microsoft 文件"
description: "本頁面提供的應用程式閘道以 SSL 卸載使用 Azure 資源管理員的指示 toocreate"
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
ms.openlocfilehash: c2855d8d3caaa97ec05475c67ff0f8dce72ef2a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-azure-resource-manager"></a><span data-ttu-id="339b1-103">使用 Azure 資源管理員設定適用於 SSL 的應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="339b1-103">Configure an application gateway for SSL offload by using Azure Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="339b1-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="339b1-104">Azure portal</span></span>](application-gateway-ssl-portal.md)
> * [<span data-ttu-id="339b1-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="339b1-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ssl-arm.md)
> * [<span data-ttu-id="339b1-106">Azure 傳統 PowerShell</span><span class="sxs-lookup"><span data-stu-id="339b1-106">Azure Classic PowerShell</span></span>](application-gateway-ssl.md)
> * [<span data-ttu-id="339b1-107">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="339b1-107">Azure CLI 2.0</span></span>](application-gateway-ssl-cli.md)

<span data-ttu-id="339b1-108">Azure 應用程式閘道可以在 hello 閘道 tooavoid 昂貴 SSL 解密工作 toohappen hello web 伺服陣列設定的 tooterminate hello Secure Sockets Layer (SSL) 工作階段。</span><span class="sxs-lookup"><span data-stu-id="339b1-108">Azure Application Gateway can be configured tooterminate hello Secure Sockets Layer (SSL) session at hello gateway tooavoid costly SSL decryption tasks toohappen at hello web farm.</span></span> <span data-ttu-id="339b1-109">Hello 前端伺服器安裝並管理 hello web 應用程式，也可以簡化 SSL 卸載。</span><span class="sxs-lookup"><span data-stu-id="339b1-109">SSL offload also simplifies hello front-end server setup and management of hello web application.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="339b1-110">開始之前</span><span class="sxs-lookup"><span data-stu-id="339b1-110">Before you begin</span></span>

1. <span data-ttu-id="339b1-111">使用 hello Web Platform Installer 安裝 hello hello Azure PowerShell cmdlet 的最新版本。</span><span class="sxs-lookup"><span data-stu-id="339b1-111">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="339b1-112">您可以從下載並安裝最新版本的 hello hello **Windows PowerShell**區段 hello[下載頁面](https://azure.microsoft.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="339b1-112">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="339b1-113">您建立虛擬網路和 hello 應用程式閘道的子網路。</span><span class="sxs-lookup"><span data-stu-id="339b1-113">You create a virtual network and a subnet for hello application gateway.</span></span> <span data-ttu-id="339b1-114">請確定沒有虛擬機器或雲端部署使用 hello 子網路。</span><span class="sxs-lookup"><span data-stu-id="339b1-114">Make sure that no virtual machines or cloud deployments are using hello subnet.</span></span> <span data-ttu-id="339b1-115">應用程式閘道必須單獨在虛擬網路子網路中。</span><span class="sxs-lookup"><span data-stu-id="339b1-115">Application Gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="339b1-116">設定 toouse hello 應用程式閘道的 hello 伺服器必須存在，或其端點建立 hello 虛擬網路中或與公用 IP/VIP 指派。</span><span class="sxs-lookup"><span data-stu-id="339b1-116">hello servers you configure toouse hello application gateway must exist or have their endpoints created either in hello virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-toocreate-an-application-gateway"></a><span data-ttu-id="339b1-117">什麼是必要的 toocreate 應用程式閘道？</span><span class="sxs-lookup"><span data-stu-id="339b1-117">What is required toocreate an application gateway?</span></span>

* <span data-ttu-id="339b1-118">**後端伺服器集區：** hello hello 後端伺服器的 IP 位址清單。</span><span class="sxs-lookup"><span data-stu-id="339b1-118">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="339b1-119">列出 hello IP 位址應該是屬於 toohello 虛擬網路子網路，或應該是公用 IP/VIP。</span><span class="sxs-lookup"><span data-stu-id="339b1-119">hello IP addresses listed should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="339b1-120">**後端伺服器集區設定：** 每個集區都包括一些設定，例如連接埠、通訊協定和以 Cookie 為基礎的同質性。</span><span class="sxs-lookup"><span data-stu-id="339b1-120">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="339b1-121">這些設定會繫結的 tooa 集區，並套用的 tooall hello 集區內的伺服器。</span><span class="sxs-lookup"><span data-stu-id="339b1-121">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="339b1-122">**前端連接埠：**此連接埠是開啟 hello 應用程式閘道上的 hello 公用連接埠。</span><span class="sxs-lookup"><span data-stu-id="339b1-122">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="339b1-123">流量叫用這個連接埠，然後再取得重新導向 tooone 的 hello 後端伺服器。</span><span class="sxs-lookup"><span data-stu-id="339b1-123">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="339b1-124">**接聽程式：** hello 接聽程式有前端連接埠的通訊協定 （Http 或 Https，這些設定是區分大小寫），與 hello 的 SSL 憑證名稱 （如果有設定 SSL 卸載）。</span><span class="sxs-lookup"><span data-stu-id="339b1-124">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these settings are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="339b1-125">**規則：** hello 規則繫結 hello 接聽程式和 hello 後端伺服器集區，並定義哪一個後端伺服器集區 hello 流量應導向的 toowhen 配接器特定接聽程式。</span><span class="sxs-lookup"><span data-stu-id="339b1-125">**Rule:** hello rule binds hello listener and hello back-end server pool and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span> <span data-ttu-id="339b1-126">目前，只有 hello*基本*規則支援。</span><span class="sxs-lookup"><span data-stu-id="339b1-126">Currently, only hello *basic* rule is supported.</span></span> <span data-ttu-id="339b1-127">hello*基本*規則是循環配置資源負載分佈。</span><span class="sxs-lookup"><span data-stu-id="339b1-127">hello *basic* rule is round-robin load distribution.</span></span>

<span data-ttu-id="339b1-128">**其他組態注意事項**</span><span class="sxs-lookup"><span data-stu-id="339b1-128">**Additional configuration notes**</span></span>

<span data-ttu-id="339b1-129">SSL 憑證設定，如 hello 中的通訊協定**HttpListener**也應該變更*Https* （區分大小寫）。</span><span class="sxs-lookup"><span data-stu-id="339b1-129">For SSL certificates configuration, hello protocol in **HttpListener** should change too*Https* (case sensitive).</span></span> <span data-ttu-id="339b1-130">hello **SslCertificate**太新增項目**HttpListener** hello hello SSL 憑證設定的變數值。</span><span class="sxs-lookup"><span data-stu-id="339b1-130">hello **SslCertificate** element is added too**HttpListener** with hello variable value configured for hello SSL certificate.</span></span> <span data-ttu-id="339b1-131">hello 前端連接埠應為更新的 too443。</span><span class="sxs-lookup"><span data-stu-id="339b1-131">hello front-end port should be updated too443.</span></span>

<span data-ttu-id="339b1-132">**tooenable cookie 為基礎的同質**： 應用程式閘道可以是來自用戶端工作階段的要求會導向的 toohello 設定的 tooensure hello web 伺服陣列中相同的 VM。</span><span class="sxs-lookup"><span data-stu-id="339b1-132">**tooenable cookie-based affinity**: An application gateway can be configured tooensure that a request from a client session is always directed toohello same VM in hello web farm.</span></span> <span data-ttu-id="339b1-133">此案例中是由資料隱碼的工作階段 cookie，可讓 hello 閘道 toodirect 流量時，適當地完成。</span><span class="sxs-lookup"><span data-stu-id="339b1-133">This scenario is done by injection of a session cookie that allows hello gateway toodirect traffic appropriately.</span></span> <span data-ttu-id="339b1-134">tooenable cookie 架構親和性，設定**CookieBasedAffinity**太*啟用*在 hello **BackendHttpSettings**項目。</span><span class="sxs-lookup"><span data-stu-id="339b1-134">tooenable cookie-based affinity, set **CookieBasedAffinity** too*Enabled* in hello **BackendHttpSettings** element.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="339b1-135">建立應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="339b1-135">Create an application gateway</span></span>

<span data-ttu-id="339b1-136">hello 使用 hello Azure 傳統部署模型和 Azure 資源管理員之間的差異是您建立應用程式閘道和 hello 需要的項目設定 toobe hello 順序。</span><span class="sxs-lookup"><span data-stu-id="339b1-136">hello difference between using hello Azure Classic deployment model and Azure Resource Manager is hello order that you create an application gateway and hello items that need toobe configured.</span></span>

<span data-ttu-id="339b1-137">使用資源管理員中，所有元件的應用程式閘道個別設定，然後放在一起 toocreate 應用程式閘道資源。</span><span class="sxs-lookup"><span data-stu-id="339b1-137">With Resource Manager, all components of an application gateway are configured individually and then put together toocreate an application gateway resource.</span></span>

<span data-ttu-id="339b1-138">以下是 hello 所需的步驟 toocreate 應用程式閘道：</span><span class="sxs-lookup"><span data-stu-id="339b1-138">Here are hello steps needed toocreate an application gateway:</span></span>

1. <span data-ttu-id="339b1-139">建立資源管理員的資源群組</span><span class="sxs-lookup"><span data-stu-id="339b1-139">Create a resource group for Resource Manager</span></span>
2. <span data-ttu-id="339b1-140">建立虛擬網路、 子網路和 hello 應用程式閘道的公用 IP</span><span class="sxs-lookup"><span data-stu-id="339b1-140">Create virtual network, subnet, and public IP for hello application gateway</span></span>
3. <span data-ttu-id="339b1-141">建立應用程式閘道組態物件</span><span class="sxs-lookup"><span data-stu-id="339b1-141">Create an application gateway configuration object</span></span>
4. <span data-ttu-id="339b1-142">建立應用程式閘道資源</span><span class="sxs-lookup"><span data-stu-id="339b1-142">Create an application gateway resource</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="339b1-143">建立資源管理員的資源群組</span><span class="sxs-lookup"><span data-stu-id="339b1-143">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="339b1-144">請確定您切換 PowerShell 模式 toouse hello Azure 資源管理員 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="339b1-144">Make sure that you switch PowerShell mode toouse hello Azure Resource Manager cmdlets.</span></span> <span data-ttu-id="339b1-145">如需詳細資訊，請參閱 [搭配使用 Windows PowerShell 與資源管理員](../powershell-azure-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="339b1-145">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="339b1-146">步驟 1</span><span class="sxs-lookup"><span data-stu-id="339b1-146">Step 1</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="339b1-147">步驟 2</span><span class="sxs-lookup"><span data-stu-id="339b1-147">Step 2</span></span>

<span data-ttu-id="339b1-148">請檢查 hello hello 帳戶的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="339b1-148">Check hello subscriptions for hello account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="339b1-149">您必須提示的 tooauthenticate 和您的認證。</span><span class="sxs-lookup"><span data-stu-id="339b1-149">You are prompted tooauthenticate with your credentials.</span></span>

### <a name="step-3"></a><span data-ttu-id="339b1-150">步驟 3</span><span class="sxs-lookup"><span data-stu-id="339b1-150">Step 3</span></span>

<span data-ttu-id="339b1-151">選擇 Azure 訂用帳戶 toouse。</span><span class="sxs-lookup"><span data-stu-id="339b1-151">Choose which of your Azure subscriptions toouse.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="339b1-152">步驟 4</span><span class="sxs-lookup"><span data-stu-id="339b1-152">Step 4</span></span>

<span data-ttu-id="339b1-153">建立資源群組 (若使用現有的資源群組，請略過此步驟)。</span><span class="sxs-lookup"><span data-stu-id="339b1-153">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

<span data-ttu-id="339b1-154">Azure Resource Manager 需要所有的資源群組指定一個位置。</span><span class="sxs-lookup"><span data-stu-id="339b1-154">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="339b1-155">此設定作為 hello 預設位置，該資源群組中的資源。</span><span class="sxs-lookup"><span data-stu-id="339b1-155">This setting is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="339b1-156">請確定應用程式閘道使用的所有命令 toocreate 都 hello 相同資源群組。</span><span class="sxs-lookup"><span data-stu-id="339b1-156">Make sure that all commands toocreate an application gateway uses hello same resource group.</span></span>

<span data-ttu-id="339b1-157">在 hello 上述範例中，我們建立一個稱為資源群組**appgw RG**和位置**美國西部**。</span><span class="sxs-lookup"><span data-stu-id="339b1-157">In hello example above, we created a resource group called **appgw-RG** and location **West US**.</span></span>

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a><span data-ttu-id="339b1-158">建立虛擬網路和 hello 應用程式閘道的子網路</span><span class="sxs-lookup"><span data-stu-id="339b1-158">Create a virtual network and a subnet for hello application gateway</span></span>

<span data-ttu-id="339b1-159">下列範例會示範如何 hello toocreate 使用資源管理員的虛擬網路：</span><span class="sxs-lookup"><span data-stu-id="339b1-159">hello following example shows how toocreate a virtual network by using Resource Manager:</span></span>

### <a name="step-1"></a><span data-ttu-id="339b1-160">步驟 1</span><span class="sxs-lookup"><span data-stu-id="339b1-160">Step 1</span></span>

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

<span data-ttu-id="339b1-161">這個範例會指定 hello 位址範圍 10.0.0.0/24 tooa 子網路使用的變數 toobe toocreate 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="339b1-161">This sample assigns hello address range 10.0.0.0/24 tooa subnet variable toobe used toocreate a virtual network.</span></span>

### <a name="step-2"></a><span data-ttu-id="339b1-162">步驟 2</span><span class="sxs-lookup"><span data-stu-id="339b1-162">Step 2</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet
```

<span data-ttu-id="339b1-163">這個範例會建立虛擬網路，名為**appgwvnet**資源群組中**appgw rg** hello 前置詞 10.0.0.0/16 使用子網路 10.0.0.0/24 hello 美國西部地區。</span><span class="sxs-lookup"><span data-stu-id="339b1-163">This sample creates a virtual network named **appgwvnet** in resource group **appgw-rg** for hello West US region using hello prefix 10.0.0.0/16 with subnet 10.0.0.0/24.</span></span>

### <a name="step-3"></a><span data-ttu-id="339b1-164">步驟 3</span><span class="sxs-lookup"><span data-stu-id="339b1-164">Step 3</span></span>

```powershell
$subnet = $vnet.Subnets[0]
```

<span data-ttu-id="339b1-165">這個範例會將指派 hello 子網路物件 toovariable $subnet hello 接下來的步驟。</span><span class="sxs-lookup"><span data-stu-id="339b1-165">This sample assigns hello subnet object toovariable $subnet for hello next steps.</span></span>

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a><span data-ttu-id="339b1-166">建立 hello 前端組態的公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="339b1-166">Create a public IP address for hello front-end configuration</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="339b1-167">這個範例會建立公用 IP 資源**publicIP01**資源群組中**appgw rg** hello 美國西部地區。</span><span class="sxs-lookup"><span data-stu-id="339b1-167">This sample creates a public IP resource **publicIP01** in resource group **appgw-rg** for hello West US region.</span></span>

## <a name="create-an-application-gateway-configuration-object"></a><span data-ttu-id="339b1-168">建立應用程式閘道組態物件</span><span class="sxs-lookup"><span data-stu-id="339b1-168">Create an application gateway configuration object</span></span>

### <a name="step-1"></a><span data-ttu-id="339b1-169">步驟 1</span><span class="sxs-lookup"><span data-stu-id="339b1-169">Step 1</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

<span data-ttu-id="339b1-170">此範例會建立名為 **gatewayIP01** 的應用程式閘道 IP 組態。</span><span class="sxs-lookup"><span data-stu-id="339b1-170">This sample creates an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="339b1-171">應用程式閘道啟動時，它會挑選設定 hello 子網路的 IP 位址，並傳送 hello 後端 IP 集區中的網路流量 toohello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="339b1-171">When Application Gateway starts, it picks up an IP address from hello subnet configured and route network traffic toohello IP addresses in hello back-end IP pool.</span></span> <span data-ttu-id="339b1-172">請記住，每個執行個體需要一個 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="339b1-172">Keep in mind that each instance takes one IP address.</span></span>

### <a name="step-2"></a><span data-ttu-id="339b1-173">步驟 2</span><span class="sxs-lookup"><span data-stu-id="339b1-173">Step 2</span></span>

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221,134.170.185.50
```

<span data-ttu-id="339b1-174">這個範例會設定 hello 後端 IP 位址集區名稱為**pool01**與 IP 位址**134.170.185.46**， **134.170.188.221**， **134.170.185.50**.</span><span class="sxs-lookup"><span data-stu-id="339b1-174">This sample configures hello back-end IP address pool named **pool01** with IP addresses **134.170.185.46**, **134.170.188.221**, **134.170.185.50**.</span></span> <span data-ttu-id="339b1-175">這些值為 hello 收到 hello 來自 hello 前端 IP 端點的網路流量的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="339b1-175">Those values are hello IP addresses that receive hello network traffic that comes from hello front-end IP endpoint.</span></span> <span data-ttu-id="339b1-176">取代從前面範例與 hello IP 位址的 web 應用程式端點的 hello hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="339b1-176">Replace hello IP addresses from hello preceding example with hello IP addresses of your web application endpoints.</span></span>

### <a name="step-3"></a><span data-ttu-id="339b1-177">步驟 3</span><span class="sxs-lookup"><span data-stu-id="339b1-177">Step 3</span></span>

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Enabled
```

<span data-ttu-id="339b1-178">這個範例會設定應用程式閘道設定**poolsetting01** tooload 平衡 hello 後端集區中的網路流量。</span><span class="sxs-lookup"><span data-stu-id="339b1-178">This sample configures application gateway setting **poolsetting01** tooload-balanced network traffic in hello back-end pool.</span></span>

### <a name="step-4"></a><span data-ttu-id="339b1-179">步驟 4</span><span class="sxs-lookup"><span data-stu-id="339b1-179">Step 4</span></span>

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 443
```

<span data-ttu-id="339b1-180">這個範例會設定名為 hello 前端 IP 連接埠**frontendport01** hello 公用 IP 端點。</span><span class="sxs-lookup"><span data-stu-id="339b1-180">This sample configures hello front-end IP port named **frontendport01** for hello public IP endpoint.</span></span>

### <a name="step-5"></a><span data-ttu-id="339b1-181">步驟 5</span><span class="sxs-lookup"><span data-stu-id="339b1-181">Step 5</span></span>

```powershell
$cert = New-AzureRmApplicationGatewaySslCertificate -Name cert01 -CertificateFile <full path for certificate file> -Password "<password>"
```

<span data-ttu-id="339b1-182">這個範例會設定 SSL 連接所使用的 hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="339b1-182">This sample configures hello certificate used for SSL connection.</span></span> <span data-ttu-id="339b1-183">hello 憑證必須以.pfx 格式 toobe 和 hello 密碼必須介於 4 too12 個字元之間。</span><span class="sxs-lookup"><span data-stu-id="339b1-183">hello certificate needs toobe in .pfx format, and hello password must be between 4 too12 characters.</span></span>

### <a name="step-6"></a><span data-ttu-id="339b1-184">步驟 6</span><span class="sxs-lookup"><span data-stu-id="339b1-184">Step 6</span></span>

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip
```

<span data-ttu-id="339b1-185">這個範例會建立 hello 名為前端 IP 組態**fipconfig01**和相關聯 hello 與 hello 前端 IP 組態的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="339b1-185">This sample creates hello front-end IP configuration named **fipconfig01** and associates hello public IP address with hello front-end IP configuration.</span></span>

### <a name="step-7"></a><span data-ttu-id="339b1-186">步驟 7</span><span class="sxs-lookup"><span data-stu-id="339b1-186">Step 7</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SslCertificate $cert
```

<span data-ttu-id="339b1-187">這個範例會建立 hello 接聽程式名稱**listener01**和相關聯 hello 前端連接埠 toohello 前端 IP 組態和憑證。</span><span class="sxs-lookup"><span data-stu-id="339b1-187">This sample creates hello listener name **listener01** and associates hello front-end port toohello front-end IP configuration and certificate.</span></span>

### <a name="step-8"></a><span data-ttu-id="339b1-188">步驟 8</span><span class="sxs-lookup"><span data-stu-id="339b1-188">Step 8</span></span>

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

<span data-ttu-id="339b1-189">這個範例會建立 hello 負載平衡器路由規則命名為**rule01** ，會設定 hello 負載平衡器行為。</span><span class="sxs-lookup"><span data-stu-id="339b1-189">This sample creates hello load balancer routing rule named **rule01** that configures hello load balancer behavior.</span></span>

### <a name="step-9"></a><span data-ttu-id="339b1-190">步驟 9</span><span class="sxs-lookup"><span data-stu-id="339b1-190">Step 9</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

<span data-ttu-id="339b1-191">這個範例會設定 hello hello 應用程式閘道執行個體大小。</span><span class="sxs-lookup"><span data-stu-id="339b1-191">This sample configures hello instance size of hello application gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="339b1-192">預設值的 hello *InstanceCount*為 2，最大值是 10。</span><span class="sxs-lookup"><span data-stu-id="339b1-192">hello default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="339b1-193">預設值的 hello *GatewaySize*都是 Medium。</span><span class="sxs-lookup"><span data-stu-id="339b1-193">hello default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="339b1-194">您可以在 Standard_Small、Standard_Medium 和 Standard_Large 之間選擇。</span><span class="sxs-lookup"><span data-stu-id="339b1-194">You can choose between Standard_Small, Standard_Medium, and Standard_Large.</span></span>

### <a name="step-10"></a><span data-ttu-id="339b1-195">步驟 10</span><span class="sxs-lookup"><span data-stu-id="339b1-195">Step 10</span></span>

```powershell
$policy = New-AzureRmApplicationGatewaySslPolicy -PolicyType Predefined -PolicyName AppGwSslPolicy20170401S
```

<span data-ttu-id="339b1-196">此步驟定義 hello SSL 原則 toouse hello 應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="339b1-196">This step defines hello SSL policy toouse on hello application gateway.</span></span> <span data-ttu-id="339b1-197">請瀏覽[設定 SSL 的原則版本和應用程式閘道上的加密套件](application-gateway-configure-ssl-policy-powershell.md)toolearn 更多。</span><span class="sxs-lookup"><span data-stu-id="339b1-197">Visit [Configure SSL policy versions and cipher suites on Application Gateway](application-gateway-configure-ssl-policy-powershell.md) toolearn more.</span></span>

## <a name="create-an-application-gateway-by-using-new-azureapplicationgateway"></a><span data-ttu-id="339b1-198">使用 New-AzureApplicationGateway 建立應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="339b1-198">Create an application gateway by using New-AzureApplicationGateway</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SslCertificates $cert -SslPolicy $policy
```

<span data-ttu-id="339b1-199">這個範例會建立應用程式閘道，並從先前步驟的 hello 的所有組態項目。</span><span class="sxs-lookup"><span data-stu-id="339b1-199">This sample creates an application gateway with all configuration items from hello preceding steps.</span></span> <span data-ttu-id="339b1-200">在 hello 範例中，稱為 hello 應用程式閘道**appgwtest**。</span><span class="sxs-lookup"><span data-stu-id="339b1-200">In hello example, hello application gateway is called **appgwtest**.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="339b1-201">取得應用程式閘道 DNS 名稱</span><span class="sxs-lookup"><span data-stu-id="339b1-201">Get application gateway DNS name</span></span>

<span data-ttu-id="339b1-202">一旦建立 hello 閘道，hello 下一個步驟是 tooconfigure hello 前端進行通訊。</span><span class="sxs-lookup"><span data-stu-id="339b1-202">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="339b1-203">當使用公用 IP 時，應用程式閘道需要動態指派的 DNS 名稱 (不易記住)。</span><span class="sxs-lookup"><span data-stu-id="339b1-203">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="339b1-204">tooensure 終端使用者可以叫用 hello 應用程式閘道，CNAME 記錄可使用的 toopoint toohello 公用端點的 hello 應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="339b1-204">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="339b1-205">[在 Azure 中設定自訂網域名稱](../cloud-services/cloud-services-custom-domain-name-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="339b1-205">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="339b1-206">toodo hello 應用程式閘道及其相關聯的 IP/DNS 名稱，使用 hello PublicIPAddress 項目附加的 toohello 應用程式閘道的這個，擷取詳細資料。</span><span class="sxs-lookup"><span data-stu-id="339b1-206">toodo this, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="339b1-207">hello 應用程式閘道的 DNS 名稱應該使用的 toocreate CNAME 記錄，哪個點 hello 兩個 web 應用程式 toothis DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="339b1-207">hello application gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="339b1-208">不建議 hello 使用 A 記錄，因為可能會在重新啟動應用程式閘道變更 hello VIP。</span><span class="sxs-lookup"><span data-stu-id="339b1-208">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>


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

## <a name="next-steps"></a><span data-ttu-id="339b1-209">後續步驟</span><span class="sxs-lookup"><span data-stu-id="339b1-209">Next steps</span></span>

<span data-ttu-id="339b1-210">如果您想 tooconfigure 內部負載平衡器 (ILB) 應用程式閘道 toouse，請參閱[內部負載平衡器 (ILB) 建立應用程式閘道](application-gateway-ilb.md)。</span><span class="sxs-lookup"><span data-stu-id="339b1-210">If you want tooconfigure an application gateway toouse with an internal load balancer (ILB), see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="339b1-211">如果您想進一步了解一般負載平衡選項，請參閱：</span><span class="sxs-lookup"><span data-stu-id="339b1-211">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="339b1-212">Azure 負載平衡器</span><span class="sxs-lookup"><span data-stu-id="339b1-212">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="339b1-213">Azure 流量管理員</span><span class="sxs-lookup"><span data-stu-id="339b1-213">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

