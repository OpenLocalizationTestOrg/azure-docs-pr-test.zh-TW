---
title: "aaaConfigure 結束 tooend Azure 應用程式閘道搭配 SSL |Microsoft 文件"
description: "本文說明如何 tooconfigure 結束 tooend SSL 搭配使用 Azure 資源管理員 PowerShell 的應用程式閘道"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: e6d80a33-4047-4538-8c83-e88876c8834e
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: 7c280478e143d309e7665219441cbee8c81d9a80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-end-tooend-ssl-with-application-gateway-using-powershell"></a><span data-ttu-id="4479b-103">使用應用程式閘道使用 PowerShell 設定結束 tooend SSL</span><span class="sxs-lookup"><span data-stu-id="4479b-103">Configure end tooend SSL with Application Gateway using PowerShell</span></span>

## <a name="overview"></a><span data-ttu-id="4479b-104">概觀</span><span class="sxs-lookup"><span data-stu-id="4479b-104">Overview</span></span>

<span data-ttu-id="4479b-105">應用程式閘道支援結束 tooend 加密的流量。</span><span class="sxs-lookup"><span data-stu-id="4479b-105">Application Gateway supports end tooend encryption of traffic.</span></span> <span data-ttu-id="4479b-106">應用程式閘道會終止在 hello 應用程式閘道的 hello SSL 連線。</span><span class="sxs-lookup"><span data-stu-id="4479b-106">Application Gateway does this by terminating hello SSL connection at hello application gateway.</span></span> <span data-ttu-id="4479b-107">hello 閘道會接著套用 hello 路由規則 toohello 流量重新加密 hello 封包，並將轉送 hello 封包 toohello 適當的後端基礎 hello 路由定義的規則。</span><span class="sxs-lookup"><span data-stu-id="4479b-107">hello gateway then applies hello routing rules toohello traffic, re-encrypts hello packet, and forwards hello packet toohello appropriate backend based on hello routing rules defined.</span></span> <span data-ttu-id="4479b-108">Hello web 伺服器的任何回應 hello 會經歷相同的處理序後 toohello 終端使用者。</span><span class="sxs-lookup"><span data-stu-id="4479b-108">Any response from hello web server goes through hello same process back toohello end user.</span></span>

<span data-ttu-id="4479b-109">應用程式閘道支援的另一項功能是定義自訂 SSL 選項。</span><span class="sxs-lookup"><span data-stu-id="4479b-109">Another feature that application gateway supports defining custom SSL options.</span></span> <span data-ttu-id="4479b-110">應用程式閘道支援下列通訊協定版本。 停用 hello**TLSv1.0**， **TLSv1.1**，和**TLSv1.2**也定義 hello 的加密套件 toouse 和 hello 喜好設定順序。</span><span class="sxs-lookup"><span data-stu-id="4479b-110">Application Gateway supports disabling hello following protocol version; **TLSv1.0**, **TLSv1.1**, and **TLSv1.2** as well defining hello which cipher suites toouse and hello order of preference.</span></span>  <span data-ttu-id="4479b-111">toolearn 進一步了解可設定的 SSL 選項，請瀏覽[SSL 原則概觀](application-gateway-SSL-policy-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="4479b-111">toolearn more about configurable SSL options, visit [SSL Policy overview](application-gateway-SSL-policy-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="4479b-112">預設會停用 SSL 2.0 和 SSL 3.0，並且無法啟用。</span><span class="sxs-lookup"><span data-stu-id="4479b-112">SSL 2.0 and SSL 3.0 are disabled by default and cannot be enabled.</span></span> <span data-ttu-id="4479b-113">它們會被視為不安全，而且不能 toobe 搭配應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="4479b-113">They are considered unsecure and are not able toobe used with Application Gateway.</span></span>

![案例影像][scenario]

## <a name="scenario"></a><span data-ttu-id="4479b-115">案例</span><span class="sxs-lookup"><span data-stu-id="4479b-115">Scenario</span></span>

<span data-ttu-id="4479b-116">在此案例中，您學習如何應用程式閘道使用 toocreate 結束 tooend SSL 使用 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="4479b-116">In this scenario, you learn how toocreate an application gateway using end tooend SSL using PowerShell.</span></span>

<span data-ttu-id="4479b-117">此案例將會：</span><span class="sxs-lookup"><span data-stu-id="4479b-117">This scenario will:</span></span>

* <span data-ttu-id="4479b-118">建立名為 **appgw-rg** 的資源群組</span><span class="sxs-lookup"><span data-stu-id="4479b-118">Create a resource group named **appgw-rg**</span></span>
* <span data-ttu-id="4479b-119">建立名為 **appgwvnet** 且具有 10.0.0.0/16 位址空間的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="4479b-119">Create a virtual network named **appgwvnet** with an address space of 10.0.0.0/16.</span></span>
* <span data-ttu-id="4479b-120">建立名為 **appgwsubnet** 和 **appsubnet** 的兩個子網路。</span><span class="sxs-lookup"><span data-stu-id="4479b-120">Create two subnets called **appgwsubnet** and **appsubnet**.</span></span>
* <span data-ttu-id="4479b-121">建立小型應用程式閘道支援結束 tooend SSL 加密，該限制 SSL 通訊協定版本和加密套件。</span><span class="sxs-lookup"><span data-stu-id="4479b-121">Create a small application gateway supporting end tooend SSL encryption that limits SSL protocols versions and cipher suites.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="4479b-122">開始之前</span><span class="sxs-lookup"><span data-stu-id="4479b-122">Before you begin</span></span>

<span data-ttu-id="4479b-123">tooconfigure 結束 tooend SSL 與應用程式閘道，憑證需要 hello 閘道，而憑證所需的 hello 後端伺服器。</span><span class="sxs-lookup"><span data-stu-id="4479b-123">tooconfigure end tooend SSL with an application gateway, a certificate is required for hello gateway and certificates are required for hello backend servers.</span></span> <span data-ttu-id="4479b-124">hello 閘道憑證是使用的 tooencrypt 和解密 hello 傳送的流量 tooit 使用 SSL。</span><span class="sxs-lookup"><span data-stu-id="4479b-124">hello gateway certificate is used tooencrypt and decrypt hello traffic sent tooit using SSL.</span></span> <span data-ttu-id="4479b-125">hello 閘道憑證需要 toobe 個人資訊交換 (pfx) 格式。</span><span class="sxs-lookup"><span data-stu-id="4479b-125">hello gateway certificate needs toobe in Personal Information Exchange (pfx) format.</span></span> <span data-ttu-id="4479b-126">這種檔案格式允許 hello 私用金鑰 toobe 匯出所需的流量 hello 應用程式閘道 tooperform hello 加密和解密。</span><span class="sxs-lookup"><span data-stu-id="4479b-126">This file format allows for hello private key toobe exported which is required by hello application gateway tooperform hello encryption and decryption of traffic.</span></span>

<span data-ttu-id="4479b-127">End tooend SSL 加密 hello 後端必須是與應用程式閘道的白名單。</span><span class="sxs-lookup"><span data-stu-id="4479b-127">For end tooend SSL encryption hello backend must be whitelisted with application gateway.</span></span> <span data-ttu-id="4479b-128">這是上傳 hello 的 hello 範例 toohello 應用程式閘道的公用憑證。</span><span class="sxs-lookup"><span data-stu-id="4479b-128">This is done by uploading hello public certificate of hello backends toohello application gateway.</span></span> <span data-ttu-id="4479b-129">這可確保該 hello 應用程式閘道只會與已知的後端執行個體通訊。</span><span class="sxs-lookup"><span data-stu-id="4479b-129">This ensures that hello application gateway only communicates with known backend instances.</span></span> <span data-ttu-id="4479b-130">這可以進一步保護 hello 結束 tooend 通訊。</span><span class="sxs-lookup"><span data-stu-id="4479b-130">This further secures hello end tooend communication.</span></span>

<span data-ttu-id="4479b-131">此程序所述步驟 hello:</span><span class="sxs-lookup"><span data-stu-id="4479b-131">This process is described in hello following steps:</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="4479b-132">建立 hello 資源群組</span><span class="sxs-lookup"><span data-stu-id="4479b-132">Create hello Resource Group</span></span>

<span data-ttu-id="4479b-133">本節將引導您完成建立資源群組、 包含 hello 應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="4479b-133">This section walks you through creating a resource group, that contains hello application gateway.</span></span>

### <a name="step-1"></a><span data-ttu-id="4479b-134">步驟 1</span><span class="sxs-lookup"><span data-stu-id="4479b-134">Step 1</span></span>

<span data-ttu-id="4479b-135">登入 tooyour Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="4479b-135">Log in tooyour Azure Account.</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="4479b-136">步驟 2</span><span class="sxs-lookup"><span data-stu-id="4479b-136">Step 2</span></span>

<span data-ttu-id="4479b-137">選取此案例中的 hello 訂用帳戶 toouse。</span><span class="sxs-lookup"><span data-stu-id="4479b-137">Select hello subscription toouse for this scenario.</span></span>

```powershell
Select-AzureRmsubscription -SubscriptionName "<Subscription name>"
```

### <a name="step-3"></a><span data-ttu-id="4479b-138">步驟 3</span><span class="sxs-lookup"><span data-stu-id="4479b-138">Step 3</span></span>

<span data-ttu-id="4479b-139">建立資源群組 (若使用現有的資源群組，請略過此步驟)。</span><span class="sxs-lookup"><span data-stu-id="4479b-139">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a><span data-ttu-id="4479b-140">建立虛擬網路和 hello 應用程式閘道的子網路</span><span class="sxs-lookup"><span data-stu-id="4479b-140">Create a virtual network and a subnet for hello application gateway</span></span>

<span data-ttu-id="4479b-141">hello 下列範例會建立虛擬網路和兩個子網路。</span><span class="sxs-lookup"><span data-stu-id="4479b-141">hello following example creates a virtual network and two subnets.</span></span> <span data-ttu-id="4479b-142">一個子網路是使用的 toohold hello 應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="4479b-142">One subnet is used toohold hello application gateway.</span></span> <span data-ttu-id="4479b-143">hello 其他子網路用於 hello 後端裝載 hello web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4479b-143">hello other subnet is used for hello backends hosting hello web application.</span></span>

### <a name="step-1"></a><span data-ttu-id="4479b-144">步驟 1</span><span class="sxs-lookup"><span data-stu-id="4479b-144">Step 1</span></span>

<span data-ttu-id="4479b-145">指派 hello 子網路用於 hello 本身的應用程式閘道的位址範圍。</span><span class="sxs-lookup"><span data-stu-id="4479b-145">Assign an address range for hello subnet be used for hello Application Gateway itself.</span></span>

```powershell
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24
```

> [!NOTE]
> <span data-ttu-id="4479b-146">應該適當地調整針對應用程式閘道所設定的子網路大小。</span><span class="sxs-lookup"><span data-stu-id="4479b-146">Subnets configured for application gateway should be properly sized.</span></span> <span data-ttu-id="4479b-147">應用程式閘道可以針對設定 too10 執行個體。</span><span class="sxs-lookup"><span data-stu-id="4479b-147">An application gateway can be configured for up too10 instances.</span></span> <span data-ttu-id="4479b-148">每個執行個體接受來自 hello 子網路的一個 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="4479b-148">Each instance takes one IP address from hello subnet.</span></span> <span data-ttu-id="4479b-149">子網路太小可能會對相應放大應用程式閘道產生負面影響。</span><span class="sxs-lookup"><span data-stu-id="4479b-149">Too small of a subnet can adversely affect scaling out an application gateway.</span></span>
> 
> 

### <a name="step-2"></a><span data-ttu-id="4479b-150">步驟 2</span><span class="sxs-lookup"><span data-stu-id="4479b-150">Step 2</span></span>

<span data-ttu-id="4479b-151">指派用於 hello 後端位址集區位址範圍 toobe。</span><span class="sxs-lookup"><span data-stu-id="4479b-151">Assign an address range toobe used for hello Backend address pool.</span></span>

```powershell
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24
```

### <a name="step-3"></a><span data-ttu-id="4479b-152">步驟 3</span><span class="sxs-lookup"><span data-stu-id="4479b-152">Step 3</span></span>

<span data-ttu-id="4479b-153">建立虛擬網路與 hello hello 先前步驟中所定義的子網路。</span><span class="sxs-lookup"><span data-stu-id="4479b-153">Create a virtual network with hello subnets defined in hello preceding steps.</span></span>

```powershell
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet
```

### <a name="step-4"></a><span data-ttu-id="4479b-154">步驟 4</span><span class="sxs-lookup"><span data-stu-id="4479b-154">Step 4</span></span>

<span data-ttu-id="4479b-155">擷取 hello 虛擬網路資源和子網路資源 toobe 用於 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="4479b-155">Retrieve hello virtual network resource and subnet resources toobe used in hello following steps:</span></span>

```powershell
$vnet = Get-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg
$gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -VirtualNetwork $vnet
$nicSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'appsubnet' -VirtualNetwork $vnet
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a><span data-ttu-id="4479b-156">建立 hello 前端組態的公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="4479b-156">Create a public IP address for hello front-end configuration</span></span>

<span data-ttu-id="4479b-157">建立用於 hello 應用程式閘道的公用 IP 資源 toobe。</span><span class="sxs-lookup"><span data-stu-id="4479b-157">Create a public IP resource toobe used for hello application gateway.</span></span> <span data-ttu-id="4479b-158">此公用 IP 位址會用於下列步驟。</span><span class="sxs-lookup"><span data-stu-id="4479b-158">This public IP address is used a following step.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -Name 'publicIP01' -Location "West US" -AllocationMethod Dynamic
```

> [!IMPORTANT]
> <span data-ttu-id="4479b-159">應用程式閘道不支援公用 IP 位址，建立定義網域標籤 hello 的使用。</span><span class="sxs-lookup"><span data-stu-id="4479b-159">Application Gateway does not support hello use of a public IP address created with a domain label defined.</span></span> <span data-ttu-id="4479b-160">只支援具有動態建立之網域標籤的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="4479b-160">Only a public IP address with a dynamically created domain label is supported.</span></span> <span data-ttu-id="4479b-161">如果您需要 hello 應用程式閘道的好記的 dns 名稱，則建議 toouse CNAME 記錄做為別名。</span><span class="sxs-lookup"><span data-stu-id="4479b-161">If you require a friendly dns name for hello application gateway, it is recommended toouse a CNAME record as an alias.</span></span>

## <a name="create-an-application-gateway-configuration-object"></a><span data-ttu-id="4479b-162">建立應用程式閘道組態物件</span><span class="sxs-lookup"><span data-stu-id="4479b-162">Create an application gateway configuration object</span></span>

<span data-ttu-id="4479b-163">建立 hello 應用程式閘道之前，會設定所有設定項目。</span><span class="sxs-lookup"><span data-stu-id="4479b-163">All configuration items are set before creating hello application gateway.</span></span> <span data-ttu-id="4479b-164">hello 下列步驟建立 hello 組態項目所需的應用程式閘道資源。</span><span class="sxs-lookup"><span data-stu-id="4479b-164">hello following steps create hello configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="4479b-165">步驟 1</span><span class="sxs-lookup"><span data-stu-id="4479b-165">Step 1</span></span>

<span data-ttu-id="4479b-166">建立應用程式閘道 IP 設定，此設定會設定哪些子網路 hello 應用程式閘道會使用。</span><span class="sxs-lookup"><span data-stu-id="4479b-166">Create an application gateway IP configuration, this setting configures what subnet hello application gateway uses.</span></span> <span data-ttu-id="4479b-167">應用程式閘道啟動時，它會挑選設定 hello 子網路的 IP 位址，並傳送 hello 後端 IP 集區中的網路流量 toohello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="4479b-167">When application gateway starts, it picks up an IP address from hello subnet configured and routes network traffic toohello IP addresses in hello back-end IP pool.</span></span> <span data-ttu-id="4479b-168">請記住，每個執行個體需要一個 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="4479b-168">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name 'gwconfig' -Subnet $gwSubnet
```

### <a name="step-2"></a><span data-ttu-id="4479b-169">步驟 2</span><span class="sxs-lookup"><span data-stu-id="4479b-169">Step 2</span></span>

<span data-ttu-id="4479b-170">建立前端 IP 組態，此設定對應的私人或公用 ip 位址 toohello 前端的 hello 應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="4479b-170">Create a front-end IP configuration, this setting maps a private or public ip address toohello front end of hello application gateway.</span></span> <span data-ttu-id="4479b-171">下列步驟將 hello 公用 IP 位址在前面步驟中的使用 hello 前端 IP 組態的 hello hello。</span><span class="sxs-lookup"><span data-stu-id="4479b-171">hello following step associates hello public IP address in hello preceding step with hello front-end IP configuration.</span></span>

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name 'fip01' -PublicIPAddress $publicip
```

### <a name="step-3"></a><span data-ttu-id="4479b-172">步驟 3</span><span class="sxs-lookup"><span data-stu-id="4479b-172">Step 3</span></span>

<span data-ttu-id="4479b-173">Hello 的 hello 後端 web 伺服器的 IP 位址設定 hello 後端 IP 位址集區。</span><span class="sxs-lookup"><span data-stu-id="4479b-173">Configure hello back-end IP address pool with hello IP addresses of hello backend web servers.</span></span> <span data-ttu-id="4479b-174">這些 IP 位址是接收來自 hello 前端 IP 端點的 hello 網路流量的 hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="4479b-174">These IP addresses are hello IP addresses that receive hello network traffic that comes from hello front-end IP endpoint.</span></span> <span data-ttu-id="4479b-175">取代下列 IP 位址 tooadd hello 您自己的應用程式的 IP 位址端點。</span><span class="sxs-lookup"><span data-stu-id="4479b-175">You replace hello following IP addresses tooadd your own application IP address endpoints.</span></span>

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name 'pool01' -BackendIPAddresses 1.1.1.1, 2.2.2.2, 3.3.3.3
```

> [!NOTE]
> <span data-ttu-id="4479b-176">完整的網域名稱 (FQDN) 是藉由使用 hello-BackendFqdns 參數也是有效的值來取代 hello 後端伺服器的 ip 位址。</span><span class="sxs-lookup"><span data-stu-id="4479b-176">A fully qualified domain name (FQDN) is also a valid value in place of an ip address for hello backend servers by using hello -BackendFqdns switch.</span></span> 

### <a name="step-4"></a><span data-ttu-id="4479b-177">步驟 4</span><span class="sxs-lookup"><span data-stu-id="4479b-177">Step 4</span></span>

<span data-ttu-id="4479b-178">設定 hello 前端 IP 連接埠 hello 公用 IP 端點。</span><span class="sxs-lookup"><span data-stu-id="4479b-178">Configure hello front-end IP port for hello public IP endpoint.</span></span> <span data-ttu-id="4479b-179">此連接埠是使用者連線到的 hello 連接埠。</span><span class="sxs-lookup"><span data-stu-id="4479b-179">This port is hello port that end users connect to.</span></span>

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name 'port01'  -Port 443
```

### <a name="step-5"></a><span data-ttu-id="4479b-180">步驟 5</span><span class="sxs-lookup"><span data-stu-id="4479b-180">Step 5</span></span>

<span data-ttu-id="4479b-181">設定 hello hello 應用程式閘道的憑證。</span><span class="sxs-lookup"><span data-stu-id="4479b-181">Configure hello certificate for hello application gateway.</span></span> <span data-ttu-id="4479b-182">此憑證是使用的 toodecrypt 和重新加密 hello hello 應用程式閘道上的流量。</span><span class="sxs-lookup"><span data-stu-id="4479b-182">This certificate is used toodecrypt and re-encrypt hello traffic on hello application gateway.</span></span>

```powershell
$cert = New-AzureRmApplicationGatewaySSLCertificate -Name cert01 -CertificateFile <full path too.pfx file> -Password <password for certificate file>
```

> [!NOTE]
> <span data-ttu-id="4479b-183">這個範例會設定 SSL 連接所使用的 hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="4479b-183">This sample configures hello certificate used for SSL connection.</span></span> <span data-ttu-id="4479b-184">hello 憑證必須以.pfx 格式 toobe 和 hello 密碼必須介於 4 too12 個字元之間。</span><span class="sxs-lookup"><span data-stu-id="4479b-184">hello certificate needs toobe in .pfx format, and hello password must be between 4 too12 characters.</span></span>

### <a name="step-6"></a><span data-ttu-id="4479b-185">步驟 6</span><span class="sxs-lookup"><span data-stu-id="4479b-185">Step 6</span></span>

<span data-ttu-id="4479b-186">建立 hello 應用程式閘道的 hello HTTP 接聽程式。</span><span class="sxs-lookup"><span data-stu-id="4479b-186">Create hello HTTP listener for hello application gateway.</span></span> <span data-ttu-id="4479b-187">Hello 前端 ip 組態、 連接埠，以及 SSL 憑證 toouse 指派。</span><span class="sxs-lookup"><span data-stu-id="4479b-187">Assign hello front-end ip configuration, port, and SSL certificate toouse.</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SSLCertificate $cert
```

### <a name="step-7"></a><span data-ttu-id="4479b-188">步驟 7</span><span class="sxs-lookup"><span data-stu-id="4479b-188">Step 7</span></span>

<span data-ttu-id="4479b-189">上傳 hello toobe hello SSL 用於啟用後端集區資源的憑證。</span><span class="sxs-lookup"><span data-stu-id="4479b-189">Upload hello certificate toobe used on hello SSL enabled backend pool resources.</span></span>

> [!NOTE]
> <span data-ttu-id="4479b-190">hello 預設探查 hello 從取得 hello 公開金鑰**預設**在 hello 後端的 IP 位址及比較 hello 公開金鑰值收到 toohello 公開金鑰值您在此處提供的 SSL 繫結。</span><span class="sxs-lookup"><span data-stu-id="4479b-190">hello default probe gets hello public key from hello **default** SSL binding on hello back-end's IP address and compares hello public key value it receives toohello public key value you provide here.</span></span> <span data-ttu-id="4479b-191">hello 擷取的公開金鑰不一定就是預期的 hello 網站 toowhich 流量**如果**hello 後端上使用主機標頭和 SNI。</span><span class="sxs-lookup"><span data-stu-id="4479b-191">hello retrieved public key may not necessarily be hello intended site toowhich traffic flows **if** you are using host headers and SNI on hello back-end.</span></span> <span data-ttu-id="4479b-192">不確定，請瀏覽 https://127.0.0.1/ 上使用的憑證 hello 的後端 tooconfirm**預設**SSL 繫結。</span><span class="sxs-lookup"><span data-stu-id="4479b-192">If in doubt, visit https://127.0.0.1/ on hello back-ends tooconfirm which certificate is used for hello **default** SSL binding.</span></span> <span data-ttu-id="4479b-193">使用本節中的 hello 公開金鑰，從該要求。</span><span class="sxs-lookup"><span data-stu-id="4479b-193">Use hello public key from that request in this section.</span></span> <span data-ttu-id="4479b-194">如果您使用主機標頭和 SNI HTTPS 繫結上，而且您不會收到的回應和憑證手動瀏覽器要求 toohttps://127.0.0.1/ hello 的後端上，您必須設定 hello 的後端上的預設 SSL 繫結。</span><span class="sxs-lookup"><span data-stu-id="4479b-194">If you are using host-headers and SNI on HTTPS bindings and you do not receive a response and certificate from a manual browser request toohttps://127.0.0.1/ on hello back-ends, you must set up a default SSL binding on hello back-ends.</span></span> <span data-ttu-id="4479b-195">如果不這樣做，探查失敗，而且 hello 後端不在允許清單。</span><span class="sxs-lookup"><span data-stu-id="4479b-195">If you do not do so, probes fail and hello back-end is not whitelisted.</span></span>

```powershell
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name 'whitelistcert1' -CertificateFile C:\users\gwallace\Desktop\cert.cer
```

> [!NOTE]
> <span data-ttu-id="4479b-196">在此步驟中所提供的 hello 憑證應 hello 公開金鑰的 hello pfx 憑證存在於 hello 後端上。</span><span class="sxs-lookup"><span data-stu-id="4479b-196">hello certificate provided in this step should be hello public key of hello pfx cert present on hello backend.</span></span> <span data-ttu-id="4479b-197">匯出 hello 憑證 （不 hello 根憑證） 中的 hello 後端伺服器上安裝。CER 格式，並將它用於此步驟。</span><span class="sxs-lookup"><span data-stu-id="4479b-197">Export hello certificate (not hello root certificate) installed on hello backend server in .CER format and use it in this step.</span></span> <span data-ttu-id="4479b-198">這個步驟白名單 hello 與 hello 應用程式閘道後的端。</span><span class="sxs-lookup"><span data-stu-id="4479b-198">This step whitelists hello backend with hello application gateway.</span></span>

### <a name="step-8"></a><span data-ttu-id="4479b-199">步驟 8</span><span class="sxs-lookup"><span data-stu-id="4479b-199">Step 8</span></span>

<span data-ttu-id="4479b-200">設定 hello 應用程式閘道後端 http 設定。</span><span class="sxs-lookup"><span data-stu-id="4479b-200">Configure hello application gateway back-end http settings.</span></span> <span data-ttu-id="4479b-201">指派 hello hello 前面步驟 toohello http 設定中上傳的憑證。</span><span class="sxs-lookup"><span data-stu-id="4479b-201">Assign hello certificate uploaded in hello preceding step toohello http settings.</span></span>

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name 'setting01' -Port 443 -Protocol Https -CookieBasedAffinity Enabled -AuthenticationCertificates $authcert
```

### <a name="step-9"></a><span data-ttu-id="4479b-202">步驟 9</span><span class="sxs-lookup"><span data-stu-id="4479b-202">Step 9</span></span>

<span data-ttu-id="4479b-203">建立負載平衡器路由規則，設定 hello 負載平衡器行為。</span><span class="sxs-lookup"><span data-stu-id="4479b-203">Create a load balancer routing rule that configures hello load balancer behavior.</span></span> <span data-ttu-id="4479b-204">在此範例中，會建立基本的循環配置資源規則。</span><span class="sxs-lookup"><span data-stu-id="4479b-204">In this example, a basic round robin rule is created.</span></span>

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name 'rule01' -RuleType basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

### <a name="step-10"></a><span data-ttu-id="4479b-205">步驟 10</span><span class="sxs-lookup"><span data-stu-id="4479b-205">Step 10</span></span>

<span data-ttu-id="4479b-206">設定執行個體大小以 hello hello 應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="4479b-206">Configure hello instance size of hello application gateway.</span></span>  <span data-ttu-id="4479b-207">hello 可用大小是**標準\_小**，**標準\_媒體**，和**標準\_大**。</span><span class="sxs-lookup"><span data-stu-id="4479b-207">hello available sizes are **Standard\_Small**, **Standard\_Medium**, and **Standard\_Large**.</span></span>  <span data-ttu-id="4479b-208">容量，hello 可用的值為 1 到 10。</span><span class="sxs-lookup"><span data-stu-id="4479b-208">For capacity, hello available values are 1 through 10.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

> [!NOTE]
> <span data-ttu-id="4479b-209">若要進行測試，可以選擇執行個體計數 1。</span><span class="sxs-lookup"><span data-stu-id="4479b-209">An instance count of 1 can be chosen for testing purposes.</span></span> <span data-ttu-id="4479b-210">請務必 tooknow 任何執行個體計數在兩個執行個體未涵蓋 hello SLA，並因此不建議使用。</span><span class="sxs-lookup"><span data-stu-id="4479b-210">It is important tooknow that any instance count under two instances is not covered by hello SLA and are therefore not recommended.</span></span> <span data-ttu-id="4479b-211">用於開發測試，不用於生產環境中使用的 toobe 都小型的閘道。</span><span class="sxs-lookup"><span data-stu-id="4479b-211">Small gateways are toobe used for dev test and not for production purposes.</span></span>

### <a name="step-11"></a><span data-ttu-id="4479b-212">步驟 11</span><span class="sxs-lookup"><span data-stu-id="4479b-212">Step 11</span></span>

<span data-ttu-id="4479b-213">設定 hello SSL 原則 toobe hello 應用程式閘道上使用。</span><span class="sxs-lookup"><span data-stu-id="4479b-213">Configure hello SSL policy toobe used on hello Application Gateway.</span></span> <span data-ttu-id="4479b-214">應用程式閘道支援 hello 能力 tooset 最小版本的 SSL 通訊協定版本。</span><span class="sxs-lookup"><span data-stu-id="4479b-214">Application Gateway supports hello ability tooset a minimum version for SSL protocol versions.</span></span>

<span data-ttu-id="4479b-215">hello 下列的值是一份可定義通訊協定版本。</span><span class="sxs-lookup"><span data-stu-id="4479b-215">hello following values are a list of protocol versions that can be defined.</span></span>

* <span data-ttu-id="4479b-216">**TLSv1_0**</span><span class="sxs-lookup"><span data-stu-id="4479b-216">**TLSv1_0**</span></span>
* <span data-ttu-id="4479b-217">**TLSv1_1**</span><span class="sxs-lookup"><span data-stu-id="4479b-217">**TLSv1_1**</span></span>
* <span data-ttu-id="4479b-218">**TLSv1_2**</span><span class="sxs-lookup"><span data-stu-id="4479b-218">**TLSv1_2**</span></span>

<span data-ttu-id="4479b-219">設定 hello 最小的通訊協定版本太**TLSv1_2** ，並讓**TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256**， **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**，和**TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256**只。</span><span class="sxs-lookup"><span data-stu-id="4479b-219">Sets hello minimum protocol version too**TLSv1_2** and enables **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256**, **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**, and **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** only.</span></span>

```powershell
$SSLPolicy = New-AzureRmApplicationGatewaySSLPolicy -MinProtocolVersion TLSv1_2 -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", "TLS_RSA_WITH_AES_128_GCM_SHA256"
```

## <a name="create-hello-application-gateway"></a><span data-ttu-id="4479b-220">建立 hello 應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="4479b-220">Create hello Application Gateway</span></span>

<span data-ttu-id="4479b-221">使用所有 hello 先前步驟，建立 hello 應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="4479b-221">Using all hello preceding steps, create hello Application Gateway.</span></span> <span data-ttu-id="4479b-222">hello 建立 hello 閘道會是長時間執行的處理程序。</span><span class="sxs-lookup"><span data-stu-id="4479b-222">hello creation of hello gateway is a long running process.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgateway -SSLCertificates $cert -ResourceGroupName "appgw-rg" -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SSLPolicy $SSLPolicy -AuthenticationCertificates $authcert -Verbose
```

## <a name="limit-ssl-protocol-versions-on-an-existing-application-gateway"></a><span data-ttu-id="4479b-223">限制現有應用程式閘道上的 SSL 通訊協定版本</span><span class="sxs-lookup"><span data-stu-id="4479b-223">Limit SSL protocol versions on an existing Application Gateway</span></span>

<span data-ttu-id="4479b-224">hello 上述步驟會帶您完成建立應用程式與結束 tooend SSL 和停用特定的 SSL 通訊協定版本。</span><span class="sxs-lookup"><span data-stu-id="4479b-224">hello preceding steps take you through creating an application with end tooend SSL and disabling certain SSL protocol versions.</span></span> <span data-ttu-id="4479b-225">hello 下列範例會停用現有的應用程式閘道特定 SSL 原則。</span><span class="sxs-lookup"><span data-stu-id="4479b-225">hello following example disables certain SSL policies on an existing application gateway.</span></span>

### <a name="step-1"></a><span data-ttu-id="4479b-226">步驟 1</span><span class="sxs-lookup"><span data-stu-id="4479b-226">Step 1</span></span>

<span data-ttu-id="4479b-227">擷取 hello 應用程式閘道 tooupdate。</span><span class="sxs-lookup"><span data-stu-id="4479b-227">Retrieve hello application gateway tooupdate.</span></span>

```powershell
$gw = Get-AzureRmApplicationGateway -Name AdatumAppGateway -ResourceGroupName AdatumAppGatewayRG
```

### <a name="step-2"></a><span data-ttu-id="4479b-228">步驟 2</span><span class="sxs-lookup"><span data-stu-id="4479b-228">Step 2</span></span>

<span data-ttu-id="4479b-229">定義 SSL 原則。</span><span class="sxs-lookup"><span data-stu-id="4479b-229">Define an SSL policy.</span></span> <span data-ttu-id="4479b-230">在下列範例的 hello，TLSv1.0 TLSv1.1 會停用並 hello 加密套件**TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256**， **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**，和**TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256**是 hello 允許唯一的。</span><span class="sxs-lookup"><span data-stu-id="4479b-230">In hello following example, TLSv1.0 and TLSv1.1 are disabled and hello cipher suites **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256**, **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**, and **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** are hello only ones allowed.</span></span>

```powershell
Set-AzureRmApplicationGatewaySSLPolicy -MinProtocolVersion -PolicyType Custom -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", "TLS_RSA_WITH_AES_128_GCM_SHA256" -ApplicationGateway $gw

```

### <a name="step-3"></a><span data-ttu-id="4479b-231">步驟 3</span><span class="sxs-lookup"><span data-stu-id="4479b-231">Step 3</span></span>

<span data-ttu-id="4479b-232">最後，更新 hello 閘道。</span><span class="sxs-lookup"><span data-stu-id="4479b-232">Finally, update hello gateway.</span></span> <span data-ttu-id="4479b-233">這最後一個步驟是長時間執行工作的重要 toonote 它。</span><span class="sxs-lookup"><span data-stu-id="4479b-233">It is important toonote that this last step is a long running task.</span></span> <span data-ttu-id="4479b-234">完成時，結束的 tooend hello 應用程式閘道設定 SSL。</span><span class="sxs-lookup"><span data-stu-id="4479b-234">When it is done, end tooend SSL is configured on hello application gateway.</span></span>

```powershell
$gw | Set-AzureRmApplicationGateway
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="4479b-235">取得應用程式閘道 DNS 名稱</span><span class="sxs-lookup"><span data-stu-id="4479b-235">Get application gateway DNS name</span></span>

<span data-ttu-id="4479b-236">一旦建立 hello 閘道，hello 下一個步驟是 tooconfigure hello 前端進行通訊。</span><span class="sxs-lookup"><span data-stu-id="4479b-236">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="4479b-237">當使用公用 IP 時，應用程式閘道需要動態指派的 DNS 名稱 (不易記住)。</span><span class="sxs-lookup"><span data-stu-id="4479b-237">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="4479b-238">tooensure 終端使用者可以叫用 hello 應用程式閘道，CNAME 記錄可使用的 toopoint toohello 公用端點的 hello 應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="4479b-238">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="4479b-239">[在 Azure 中設定自訂網域名稱](../cloud-services/cloud-services-custom-domain-name-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="4479b-239">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="4479b-240">toodo hello 應用程式閘道及其相關聯的 IP/DNS 名稱，使用 hello PublicIPAddress 項目附加的 toohello 應用程式閘道的這個，擷取詳細資料。</span><span class="sxs-lookup"><span data-stu-id="4479b-240">toodo this, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="4479b-241">hello 應用程式閘道的 DNS 名稱應該使用的 toocreate CNAME 記錄，哪個點 hello 兩個 web 應用程式 toothis DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="4479b-241">hello application gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="4479b-242">不建議 hello 使用 A 記錄，因為可能會在重新啟動應用程式閘道變更 hello VIP。</span><span class="sxs-lookup"><span data-stu-id="4479b-242">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="4479b-243">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4479b-243">Next steps</span></span>

<span data-ttu-id="4479b-244">深入了解 web 應用程式與 Web 應用程式防火牆透過應用程式閘道的 hello 安全性強化造訪[Web 應用程式防火牆概觀](application-gateway-webapplicationfirewall-overview.md)</span><span class="sxs-lookup"><span data-stu-id="4479b-244">Learn about hardening hello security of your web applications with Web Application Firewall through Application Gateway by visiting [Web Application Firewall Overview](application-gateway-webapplicationfirewall-overview.md)</span></span>

[scenario]: ./media/application-gateway-end-to-end-SSL-powershell/scenario.png
