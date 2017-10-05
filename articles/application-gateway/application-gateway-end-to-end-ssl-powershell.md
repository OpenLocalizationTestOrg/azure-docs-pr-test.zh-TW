---
title: "以 Azure 應用程式閘道設定端對端 SSL | Microsoft Docs"
description: "本文說明如何使用 Azure Resource Manager PowerShell 以應用程式閘道設定端對端 SSL"
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
ms.openlocfilehash: 6d969d6a0c649c263e1d5bb99bdbceec484cb9a3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="configure-end-to-end-ssl-with-application-gateway-using-powershell"></a><span data-ttu-id="e2660-103">使用 PowerShell 透過應用程式閘道設定端對端 SSL</span><span class="sxs-lookup"><span data-stu-id="e2660-103">Configure end to end SSL with Application Gateway using PowerShell</span></span>

## <a name="overview"></a><span data-ttu-id="e2660-104">概觀</span><span class="sxs-lookup"><span data-stu-id="e2660-104">Overview</span></span>

<span data-ttu-id="e2660-105">應用程式閘道支援為流量進行端對端加密。</span><span class="sxs-lookup"><span data-stu-id="e2660-105">Application Gateway supports end to end encryption of traffic.</span></span> <span data-ttu-id="e2660-106">應用程式閘道用來進行此作業的方法是，在應用程式閘道終止 SSL 連線。</span><span class="sxs-lookup"><span data-stu-id="e2660-106">Application Gateway does this by terminating the SSL connection at the application gateway.</span></span> <span data-ttu-id="e2660-107">閘道接著會對流量套用路由規則、重新加密封包，並根據所定義的路由規則將封包轉送至適當的後端。</span><span class="sxs-lookup"><span data-stu-id="e2660-107">The gateway then applies the routing rules to the traffic, re-encrypts the packet, and forwards the packet to the appropriate backend based on the routing rules defined.</span></span> <span data-ttu-id="e2660-108">任何來自 Web 伺服器的回應都會經歷相同的程序而回到使用者端。</span><span class="sxs-lookup"><span data-stu-id="e2660-108">Any response from the web server goes through the same process back to the end user.</span></span>

<span data-ttu-id="e2660-109">應用程式閘道支援的另一項功能是定義自訂 SSL 選項。</span><span class="sxs-lookup"><span data-stu-id="e2660-109">Another feature that application gateway supports defining custom SSL options.</span></span> <span data-ttu-id="e2660-110">應用程式閘道支援停用下列通訊協定版本；**TLSv1.0**、**TLSv1.1** 和 **TLSv1.2**，也會定義要使用那個加密套件以及偏好的順序。</span><span class="sxs-lookup"><span data-stu-id="e2660-110">Application Gateway supports disabling the following protocol version; **TLSv1.0**, **TLSv1.1**, and **TLSv1.2** as well defining the which cipher suites to use and the order of preference.</span></span>  <span data-ttu-id="e2660-111">若要深入了解可設定的 SSL 選項，請參閱 [SSL 原則概觀](application-gateway-SSL-policy-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="e2660-111">To learn more about configurable SSL options, visit [SSL Policy overview](application-gateway-SSL-policy-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="e2660-112">預設會停用 SSL 2.0 和 SSL 3.0，並且無法啟用。</span><span class="sxs-lookup"><span data-stu-id="e2660-112">SSL 2.0 and SSL 3.0 are disabled by default and cannot be enabled.</span></span> <span data-ttu-id="e2660-113">這些版本被認為並不安全，因此不能搭配應用程式閘道使用。</span><span class="sxs-lookup"><span data-stu-id="e2660-113">They are considered unsecure and are not able to be used with Application Gateway.</span></span>

![案例影像][scenario]

## <a name="scenario"></a><span data-ttu-id="e2660-115">案例</span><span class="sxs-lookup"><span data-stu-id="e2660-115">Scenario</span></span>

<span data-ttu-id="e2660-116">在此案例中，您將了解如何使用 PowerShell 來建立使用端對端 SSL 的應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="e2660-116">In this scenario, you learn how to create an application gateway using end to end SSL using PowerShell.</span></span>

<span data-ttu-id="e2660-117">此案例將會：</span><span class="sxs-lookup"><span data-stu-id="e2660-117">This scenario will:</span></span>

* <span data-ttu-id="e2660-118">建立名為 **appgw-rg** 的資源群組</span><span class="sxs-lookup"><span data-stu-id="e2660-118">Create a resource group named **appgw-rg**</span></span>
* <span data-ttu-id="e2660-119">建立名為 **appgwvnet** 且具有 10.0.0.0/16 位址空間的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="e2660-119">Create a virtual network named **appgwvnet** with an address space of 10.0.0.0/16.</span></span>
* <span data-ttu-id="e2660-120">建立名為 **appgwsubnet** 和 **appsubnet** 的兩個子網路。</span><span class="sxs-lookup"><span data-stu-id="e2660-120">Create two subnets called **appgwsubnet** and **appsubnet**.</span></span>
* <span data-ttu-id="e2660-121">建立支援端對端 SSL 加密 (限制 SSL 通訊協定版本和加密套件) 的小型應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="e2660-121">Create a small application gateway supporting end to end SSL encryption that limits SSL protocols versions and cipher suites.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="e2660-122">開始之前</span><span class="sxs-lookup"><span data-stu-id="e2660-122">Before you begin</span></span>

<span data-ttu-id="e2660-123">若要對應用程式閘道設定端對端 SSL，則需要閘道憑證和後端伺服器憑證。</span><span class="sxs-lookup"><span data-stu-id="e2660-123">To configure end to end SSL with an application gateway, a certificate is required for the gateway and certificates are required for the backend servers.</span></span> <span data-ttu-id="e2660-124">閘道憑證可用來加密和解密使用 SSL 傳送過來的流量。</span><span class="sxs-lookup"><span data-stu-id="e2660-124">The gateway certificate is used to encrypt and decrypt the traffic sent to it using SSL.</span></span> <span data-ttu-id="e2660-125">閘道憑證必須採用「個人資訊交換」(pfx) 格式。</span><span class="sxs-lookup"><span data-stu-id="e2660-125">The gateway certificate needs to be in Personal Information Exchange (pfx) format.</span></span> <span data-ttu-id="e2660-126">此檔案格式可允許將私密金鑰匯出，而應用程式閘道需要這個匯出的金鑰來執行流量的加密和解密。</span><span class="sxs-lookup"><span data-stu-id="e2660-126">This file format allows for the private key to be exported which is required by the application gateway to perform the encryption and decryption of traffic.</span></span>

<span data-ttu-id="e2660-127">若要加密端對端 SSL，後端必須已加入到應用程式閘道的白名單。</span><span class="sxs-lookup"><span data-stu-id="e2660-127">For end to end SSL encryption the backend must be whitelisted with application gateway.</span></span> <span data-ttu-id="e2660-128">只要將後端的公開憑證上傳至應用程式閘道，即可完成此動作。</span><span class="sxs-lookup"><span data-stu-id="e2660-128">This is done by uploading the public certificate of the backends to the application gateway.</span></span> <span data-ttu-id="e2660-129">這可確保應用程式閘道只會與已知的後端執行個體通訊。</span><span class="sxs-lookup"><span data-stu-id="e2660-129">This ensures that the application gateway only communicates with known backend instances.</span></span> <span data-ttu-id="e2660-130">這會進而保護端對端通訊。</span><span class="sxs-lookup"><span data-stu-id="e2660-130">This further secures the end to end communication.</span></span>

<span data-ttu-id="e2660-131">下列步驟會說明此程序：</span><span class="sxs-lookup"><span data-stu-id="e2660-131">This process is described in the following steps:</span></span>

## <a name="create-the-resource-group"></a><span data-ttu-id="e2660-132">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="e2660-132">Create the Resource Group</span></span>

<span data-ttu-id="e2660-133">本節將引導您建立資源群組，其中包含應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="e2660-133">This section walks you through creating a resource group, that contains the application gateway.</span></span>

### <a name="step-1"></a><span data-ttu-id="e2660-134">步驟 1</span><span class="sxs-lookup"><span data-stu-id="e2660-134">Step 1</span></span>

<span data-ttu-id="e2660-135">登入您的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="e2660-135">Log in to your Azure Account.</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="e2660-136">步驟 2</span><span class="sxs-lookup"><span data-stu-id="e2660-136">Step 2</span></span>

<span data-ttu-id="e2660-137">選取要用於此案例的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="e2660-137">Select the subscription to use for this scenario.</span></span>

```powershell
Select-AzureRmsubscription -SubscriptionName "<Subscription name>"
```

### <a name="step-3"></a><span data-ttu-id="e2660-138">步驟 3</span><span class="sxs-lookup"><span data-stu-id="e2660-138">Step 3</span></span>

<span data-ttu-id="e2660-139">建立資源群組 (若使用現有的資源群組，請略過此步驟)。</span><span class="sxs-lookup"><span data-stu-id="e2660-139">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

## <a name="create-a-virtual-network-and-a-subnet-for-the-application-gateway"></a><span data-ttu-id="e2660-140">建立應用程式閘道的虛擬網路和子網路</span><span class="sxs-lookup"><span data-stu-id="e2660-140">Create a virtual network and a subnet for the application gateway</span></span>

<span data-ttu-id="e2660-141">下列範例會建立虛擬網路和兩個子網路。</span><span class="sxs-lookup"><span data-stu-id="e2660-141">The following example creates a virtual network and two subnets.</span></span> <span data-ttu-id="e2660-142">一個子網路用來保留應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="e2660-142">One subnet is used to hold the application gateway.</span></span> <span data-ttu-id="e2660-143">另一個子網路則用於裝載 Web 應用程式的後端。</span><span class="sxs-lookup"><span data-stu-id="e2660-143">The other subnet is used for the backends hosting the web application.</span></span>

### <a name="step-1"></a><span data-ttu-id="e2660-144">步驟 1</span><span class="sxs-lookup"><span data-stu-id="e2660-144">Step 1</span></span>

<span data-ttu-id="e2660-145">指派要用於應用程式閘道本身的子網路位址範圍。</span><span class="sxs-lookup"><span data-stu-id="e2660-145">Assign an address range for the subnet be used for the Application Gateway itself.</span></span>

```powershell
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24
```

> [!NOTE]
> <span data-ttu-id="e2660-146">應該適當地調整針對應用程式閘道所設定的子網路大小。</span><span class="sxs-lookup"><span data-stu-id="e2660-146">Subnets configured for application gateway should be properly sized.</span></span> <span data-ttu-id="e2660-147">一個應用程式閘道最多可以針對 10 個執行個體進行設定。</span><span class="sxs-lookup"><span data-stu-id="e2660-147">An application gateway can be configured for up to 10 instances.</span></span> <span data-ttu-id="e2660-148">每個執行個體會從子網路取得 1 個 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="e2660-148">Each instance takes one IP address from the subnet.</span></span> <span data-ttu-id="e2660-149">子網路太小可能會對相應放大應用程式閘道產生負面影響。</span><span class="sxs-lookup"><span data-stu-id="e2660-149">Too small of a subnet can adversely affect scaling out an application gateway.</span></span>
> 
> 

### <a name="step-2"></a><span data-ttu-id="e2660-150">步驟 2</span><span class="sxs-lookup"><span data-stu-id="e2660-150">Step 2</span></span>

<span data-ttu-id="e2660-151">指派要用於後端位址集區的位址範圍。</span><span class="sxs-lookup"><span data-stu-id="e2660-151">Assign an address range to be used for the Backend address pool.</span></span>

```powershell
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24
```

### <a name="step-3"></a><span data-ttu-id="e2660-152">步驟 3</span><span class="sxs-lookup"><span data-stu-id="e2660-152">Step 3</span></span>

<span data-ttu-id="e2660-153">建立具有上述步驟所定義子網路的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="e2660-153">Create a virtual network with the subnets defined in the preceding steps.</span></span>

```powershell
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet
```

### <a name="step-4"></a><span data-ttu-id="e2660-154">步驟 4</span><span class="sxs-lookup"><span data-stu-id="e2660-154">Step 4</span></span>

<span data-ttu-id="e2660-155">擷取要用於下列步驟的虛擬網路資源和子網路資源︰</span><span class="sxs-lookup"><span data-stu-id="e2660-155">Retrieve the virtual network resource and subnet resources to be used in the following steps:</span></span>

```powershell
$vnet = Get-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg
$gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -VirtualNetwork $vnet
$nicSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'appsubnet' -VirtualNetwork $vnet
```

## <a name="create-a-public-ip-address-for-the-front-end-configuration"></a><span data-ttu-id="e2660-156">建立前端組態的公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="e2660-156">Create a public IP address for the front-end configuration</span></span>

<span data-ttu-id="e2660-157">建立要用於應用程式閘道的公用 IP 資源。</span><span class="sxs-lookup"><span data-stu-id="e2660-157">Create a public IP resource to be used for the application gateway.</span></span> <span data-ttu-id="e2660-158">此公用 IP 位址會用於下列步驟。</span><span class="sxs-lookup"><span data-stu-id="e2660-158">This public IP address is used a following step.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -Name 'publicIP01' -Location "West US" -AllocationMethod Dynamic
```

> [!IMPORTANT]
> <span data-ttu-id="e2660-159">應用程式閘道不支援使用以定義之網域標籤建立的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="e2660-159">Application Gateway does not support the use of a public IP address created with a domain label defined.</span></span> <span data-ttu-id="e2660-160">只支援具有動態建立之網域標籤的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="e2660-160">Only a public IP address with a dynamically created domain label is supported.</span></span> <span data-ttu-id="e2660-161">如果您需要讓應用程式閘道具有好記的 DNS 名稱，建議您使用 CNAME 記錄作為別名。</span><span class="sxs-lookup"><span data-stu-id="e2660-161">If you require a friendly dns name for the application gateway, it is recommended to use a CNAME record as an alias.</span></span>

## <a name="create-an-application-gateway-configuration-object"></a><span data-ttu-id="e2660-162">建立應用程式閘道組態物件</span><span class="sxs-lookup"><span data-stu-id="e2660-162">Create an application gateway configuration object</span></span>

<span data-ttu-id="e2660-163">所有設定項目是在建立應用程式閘道之前設定。</span><span class="sxs-lookup"><span data-stu-id="e2660-163">All configuration items are set before creating the application gateway.</span></span> <span data-ttu-id="e2660-164">下列步驟會建立應用程式閘道資源所需的組態項目。</span><span class="sxs-lookup"><span data-stu-id="e2660-164">The following steps create the configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="e2660-165">步驟 1</span><span class="sxs-lookup"><span data-stu-id="e2660-165">Step 1</span></span>

<span data-ttu-id="e2660-166">建立應用程式閘道的 IP 組態，此設定會設定應用程式閘道所使用的子網路。</span><span class="sxs-lookup"><span data-stu-id="e2660-166">Create an application gateway IP configuration, this setting configures what subnet the application gateway uses.</span></span> <span data-ttu-id="e2660-167">當應用程式閘道啟動時，它會從已設定的子網路取得 IP 位址，再將網路流量路由傳送到後端 IP 集區中的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="e2660-167">When application gateway starts, it picks up an IP address from the subnet configured and routes network traffic to the IP addresses in the back-end IP pool.</span></span> <span data-ttu-id="e2660-168">請記住，每個執行個體需要一個 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="e2660-168">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name 'gwconfig' -Subnet $gwSubnet
```

### <a name="step-2"></a><span data-ttu-id="e2660-169">步驟 2</span><span class="sxs-lookup"><span data-stu-id="e2660-169">Step 2</span></span>

<span data-ttu-id="e2660-170">建立前端 IP 組態，此設定會將私人或公用 IP 位址對應到應用程式閘道的前端。</span><span class="sxs-lookup"><span data-stu-id="e2660-170">Create a front-end IP configuration, this setting maps a private or public ip address to the front end of the application gateway.</span></span> <span data-ttu-id="e2660-171">下一個步驟會將先前步驟中的公用 IP 位址關聯到前端 IP 組態。</span><span class="sxs-lookup"><span data-stu-id="e2660-171">The following step associates the public IP address in the preceding step with the front-end IP configuration.</span></span>

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name 'fip01' -PublicIPAddress $publicip
```

### <a name="step-3"></a><span data-ttu-id="e2660-172">步驟 3</span><span class="sxs-lookup"><span data-stu-id="e2660-172">Step 3</span></span>

<span data-ttu-id="e2660-173">使用後端 Web 伺服器的 IP 位址設定後端 IP 位址集區。</span><span class="sxs-lookup"><span data-stu-id="e2660-173">Configure the back-end IP address pool with the IP addresses of the backend web servers.</span></span> <span data-ttu-id="e2660-174">這些 IP 位址會接收來自前端 IP 端點的網路流量。</span><span class="sxs-lookup"><span data-stu-id="e2660-174">These IP addresses are the IP addresses that receive the network traffic that comes from the front-end IP endpoint.</span></span> <span data-ttu-id="e2660-175">您可取代下列 IP 位址來新增自己的應用程式 IP 位址端點。</span><span class="sxs-lookup"><span data-stu-id="e2660-175">You replace the following IP addresses to add your own application IP address endpoints.</span></span>

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name 'pool01' -BackendIPAddresses 1.1.1.1, 2.2.2.2, 3.3.3.3
```

> [!NOTE]
> <span data-ttu-id="e2660-176">完整網域名稱 (FQDN) 也是可取代後端伺服器 IP 位址 (藉由使用 -BackendFqdns 參數) 的有效值。</span><span class="sxs-lookup"><span data-stu-id="e2660-176">A fully qualified domain name (FQDN) is also a valid value in place of an ip address for the backend servers by using the -BackendFqdns switch.</span></span> 

### <a name="step-4"></a><span data-ttu-id="e2660-177">步驟 4</span><span class="sxs-lookup"><span data-stu-id="e2660-177">Step 4</span></span>

<span data-ttu-id="e2660-178">設定公用 IP 端點的前端 IP 連接埠。</span><span class="sxs-lookup"><span data-stu-id="e2660-178">Configure the front-end IP port for the public IP endpoint.</span></span> <span data-ttu-id="e2660-179">此連接埠是供使用者連接到的連接埠。</span><span class="sxs-lookup"><span data-stu-id="e2660-179">This port is the port that end users connect to.</span></span>

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name 'port01'  -Port 443
```

### <a name="step-5"></a><span data-ttu-id="e2660-180">步驟 5</span><span class="sxs-lookup"><span data-stu-id="e2660-180">Step 5</span></span>

<span data-ttu-id="e2660-181">設定應用程式閘道憑證。</span><span class="sxs-lookup"><span data-stu-id="e2660-181">Configure the certificate for the application gateway.</span></span> <span data-ttu-id="e2660-182">此憑證可用來解密和重新加密應用程式閘道上的流量。</span><span class="sxs-lookup"><span data-stu-id="e2660-182">This certificate is used to decrypt and re-encrypt the traffic on the application gateway.</span></span>

```powershell
$cert = New-AzureRmApplicationGatewaySSLCertificate -Name cert01 -CertificateFile <full path to .pfx file> -Password <password for certificate file>
```

> [!NOTE]
> <span data-ttu-id="e2660-183">此範例會設定 SSL 連接所使用的憑證。</span><span class="sxs-lookup"><span data-stu-id="e2660-183">This sample configures the certificate used for SSL connection.</span></span> <span data-ttu-id="e2660-184">憑證必須是 .pfx 格式，而密碼則必須介於 4 到 12 個字元。</span><span class="sxs-lookup"><span data-stu-id="e2660-184">The certificate needs to be in .pfx format, and the password must be between 4 to 12 characters.</span></span>

### <a name="step-6"></a><span data-ttu-id="e2660-185">步驟 6</span><span class="sxs-lookup"><span data-stu-id="e2660-185">Step 6</span></span>

<span data-ttu-id="e2660-186">建立應用程式閘道的 HTTP 接聽程式。</span><span class="sxs-lookup"><span data-stu-id="e2660-186">Create the HTTP listener for the application gateway.</span></span> <span data-ttu-id="e2660-187">指派要使用的前端 IP 設定、連接埠和 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="e2660-187">Assign the front-end ip configuration, port, and SSL certificate to use.</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SSLCertificate $cert
```

### <a name="step-7"></a><span data-ttu-id="e2660-188">步驟 7</span><span class="sxs-lookup"><span data-stu-id="e2660-188">Step 7</span></span>

<span data-ttu-id="e2660-189">上傳要在已啟用 SSL 的後端集區資源上使用的憑證。</span><span class="sxs-lookup"><span data-stu-id="e2660-189">Upload the certificate to be used on the SSL enabled backend pool resources.</span></span>

> [!NOTE]
> <span data-ttu-id="e2660-190">預設探查可從後端 IP 位址上的**預設** SSL 繫結取得公開金鑰，並將所收到的公開金鑰值與您在此處提供的公開金鑰值做比較。</span><span class="sxs-lookup"><span data-stu-id="e2660-190">The default probe gets the public key from the **default** SSL binding on the back-end's IP address and compares the public key value it receives to the public key value you provide here.</span></span> <span data-ttu-id="e2660-191">**如果**您在後端上使用主機標頭和 SNI，擷取的公開金鑰不一定就是流量要流向的預定網站。</span><span class="sxs-lookup"><span data-stu-id="e2660-191">The retrieved public key may not necessarily be the intended site to which traffic flows **if** you are using host headers and SNI on the back-end.</span></span> <span data-ttu-id="e2660-192">如果不能確定，請在後端造訪 https://127.0.0.1/ 以確認要將哪一個憑證用於**預設** SSL 繫結。</span><span class="sxs-lookup"><span data-stu-id="e2660-192">If in doubt, visit https://127.0.0.1/ on the back-ends to confirm which certificate is used for the **default** SSL binding.</span></span> <span data-ttu-id="e2660-193">請使用來自本節該要求的公開金鑰。</span><span class="sxs-lookup"><span data-stu-id="e2660-193">Use the public key from that request in this section.</span></span> <span data-ttu-id="e2660-194">如果您在 HTTPS 繫結上使用主機標頭和 SNI，且並未從對於後端上 https://127.0.0.1/ 的手動瀏覽器要求收到回應和憑證，您必須在後端上設定預設 SSL 繫結。</span><span class="sxs-lookup"><span data-stu-id="e2660-194">If you are using host-headers and SNI on HTTPS bindings and you do not receive a response and certificate from a manual browser request to https://127.0.0.1/ on the back-ends, you must set up a default SSL binding on the back-ends.</span></span> <span data-ttu-id="e2660-195">如果您未這麼做，探查將會失敗，而且後端不會加入白名單。</span><span class="sxs-lookup"><span data-stu-id="e2660-195">If you do not do so, probes fail and the back-end is not whitelisted.</span></span>

```powershell
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name 'whitelistcert1' -CertificateFile C:\users\gwallace\Desktop\cert.cer
```

> [!NOTE]
> <span data-ttu-id="e2660-196">在此步驟中所提供的憑證應該是在後端中出示之 pfx 憑證的公開金鑰。</span><span class="sxs-lookup"><span data-stu-id="e2660-196">The certificate provided in this step should be the public key of the pfx cert present on the backend.</span></span> <span data-ttu-id="e2660-197">將安裝在後端伺服器上的憑證 (非根憑證) 以 .CER 格式匯出，並將它用於此步驟。</span><span class="sxs-lookup"><span data-stu-id="e2660-197">Export the certificate (not the root certificate) installed on the backend server in .CER format and use it in this step.</span></span> <span data-ttu-id="e2660-198">此步驟會將後端加入到應用程式閘道的白名單。</span><span class="sxs-lookup"><span data-stu-id="e2660-198">This step whitelists the backend with the application gateway.</span></span>

### <a name="step-8"></a><span data-ttu-id="e2660-199">步驟 8</span><span class="sxs-lookup"><span data-stu-id="e2660-199">Step 8</span></span>

<span data-ttu-id="e2660-200">設定應用程式閘道的後端 http 設定。</span><span class="sxs-lookup"><span data-stu-id="e2660-200">Configure the application gateway back-end http settings.</span></span> <span data-ttu-id="e2660-201">將前述步驟中上傳的憑證指派給 http 設定。</span><span class="sxs-lookup"><span data-stu-id="e2660-201">Assign the certificate uploaded in the preceding step to the http settings.</span></span>

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name 'setting01' -Port 443 -Protocol Https -CookieBasedAffinity Enabled -AuthenticationCertificates $authcert
```

### <a name="step-9"></a><span data-ttu-id="e2660-202">步驟 9</span><span class="sxs-lookup"><span data-stu-id="e2660-202">Step 9</span></span>

<span data-ttu-id="e2660-203">建立會設定負載平衡器行為的負載平衡器路由規則。</span><span class="sxs-lookup"><span data-stu-id="e2660-203">Create a load balancer routing rule that configures the load balancer behavior.</span></span> <span data-ttu-id="e2660-204">在此範例中，會建立基本的循環配置資源規則。</span><span class="sxs-lookup"><span data-stu-id="e2660-204">In this example, a basic round robin rule is created.</span></span>

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name 'rule01' -RuleType basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

### <a name="step-10"></a><span data-ttu-id="e2660-205">步驟 10</span><span class="sxs-lookup"><span data-stu-id="e2660-205">Step 10</span></span>

<span data-ttu-id="e2660-206">設定應用程式閘道的執行個體大小。</span><span class="sxs-lookup"><span data-stu-id="e2660-206">Configure the instance size of the application gateway.</span></span>  <span data-ttu-id="e2660-207">可用大小是 **Standard\_Small**、**Standard\_Medium** 和 **Standard\_Large**。</span><span class="sxs-lookup"><span data-stu-id="e2660-207">The available sizes are **Standard\_Small**, **Standard\_Medium**, and **Standard\_Large**.</span></span>  <span data-ttu-id="e2660-208">容量的可用值為 1 到 10。</span><span class="sxs-lookup"><span data-stu-id="e2660-208">For capacity, the available values are 1 through 10.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

> [!NOTE]
> <span data-ttu-id="e2660-209">若要進行測試，可以選擇執行個體計數 1。</span><span class="sxs-lookup"><span data-stu-id="e2660-209">An instance count of 1 can be chosen for testing purposes.</span></span> <span data-ttu-id="e2660-210">請務必了解 SLA 不涵蓋任何低於兩個執行個體的執行個體計數，因此不建議使用。</span><span class="sxs-lookup"><span data-stu-id="e2660-210">It is important to know that any instance count under two instances is not covered by the SLA and are therefore not recommended.</span></span> <span data-ttu-id="e2660-211">小型閘道適用於開發測試，不適合在生產環境中使用。</span><span class="sxs-lookup"><span data-stu-id="e2660-211">Small gateways are to be used for dev test and not for production purposes.</span></span>

### <a name="step-11"></a><span data-ttu-id="e2660-212">步驟 11</span><span class="sxs-lookup"><span data-stu-id="e2660-212">Step 11</span></span>

<span data-ttu-id="e2660-213">設定要在應用程式閘道上使用的 SSL 原則。</span><span class="sxs-lookup"><span data-stu-id="e2660-213">Configure the SSL policy to be used on the Application Gateway.</span></span> <span data-ttu-id="e2660-214">應用程式閘道支援將 SSL 通訊協定版本設為最小版本的能力。</span><span class="sxs-lookup"><span data-stu-id="e2660-214">Application Gateway supports the ability to set a minimum version for SSL protocol versions.</span></span>

<span data-ttu-id="e2660-215">下列值是可以定義的通訊協定版本清單。</span><span class="sxs-lookup"><span data-stu-id="e2660-215">The following values are a list of protocol versions that can be defined.</span></span>

* <span data-ttu-id="e2660-216">**TLSv1_0**</span><span class="sxs-lookup"><span data-stu-id="e2660-216">**TLSv1_0**</span></span>
* <span data-ttu-id="e2660-217">**TLSv1_1**</span><span class="sxs-lookup"><span data-stu-id="e2660-217">**TLSv1_1**</span></span>
* <span data-ttu-id="e2660-218">**TLSv1_2**</span><span class="sxs-lookup"><span data-stu-id="e2660-218">**TLSv1_2**</span></span>

<span data-ttu-id="e2660-219">將最小通訊協定版本設定為 **TLSv1_2** 並且只啟用 **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256**、**TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384** 和 **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256**。</span><span class="sxs-lookup"><span data-stu-id="e2660-219">Sets the minimum protocol version to **TLSv1_2** and enables **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256**, **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**, and **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** only.</span></span>

```powershell
$SSLPolicy = New-AzureRmApplicationGatewaySSLPolicy -MinProtocolVersion TLSv1_2 -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", "TLS_RSA_WITH_AES_128_GCM_SHA256"
```

## <a name="create-the-application-gateway"></a><span data-ttu-id="e2660-220">建立應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="e2660-220">Create the Application Gateway</span></span>

<span data-ttu-id="e2660-221">使用上述所有步驟建立應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="e2660-221">Using all the preceding steps, create the Application Gateway.</span></span> <span data-ttu-id="e2660-222">建立閘道是很漫長的程序。</span><span class="sxs-lookup"><span data-stu-id="e2660-222">The creation of the gateway is a long running process.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgateway -SSLCertificates $cert -ResourceGroupName "appgw-rg" -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SSLPolicy $SSLPolicy -AuthenticationCertificates $authcert -Verbose
```

## <a name="limit-ssl-protocol-versions-on-an-existing-application-gateway"></a><span data-ttu-id="e2660-223">限制現有應用程式閘道上的 SSL 通訊協定版本</span><span class="sxs-lookup"><span data-stu-id="e2660-223">Limit SSL protocol versions on an existing Application Gateway</span></span>

<span data-ttu-id="e2660-224">上述步驟會引導您建立具有端對端 SSL 的應用程式並停用特定的 SSL 通訊協定版本。</span><span class="sxs-lookup"><span data-stu-id="e2660-224">The preceding steps take you through creating an application with end to end SSL and disabling certain SSL protocol versions.</span></span> <span data-ttu-id="e2660-225">下列範例會停用現有應用程式閘道上的特定 SSL 原則。</span><span class="sxs-lookup"><span data-stu-id="e2660-225">The following example disables certain SSL policies on an existing application gateway.</span></span>

### <a name="step-1"></a><span data-ttu-id="e2660-226">步驟 1</span><span class="sxs-lookup"><span data-stu-id="e2660-226">Step 1</span></span>

<span data-ttu-id="e2660-227">擷取要更新的應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="e2660-227">Retrieve the application gateway to update.</span></span>

```powershell
$gw = Get-AzureRmApplicationGateway -Name AdatumAppGateway -ResourceGroupName AdatumAppGatewayRG
```

### <a name="step-2"></a><span data-ttu-id="e2660-228">步驟 2</span><span class="sxs-lookup"><span data-stu-id="e2660-228">Step 2</span></span>

<span data-ttu-id="e2660-229">定義 SSL 原則。</span><span class="sxs-lookup"><span data-stu-id="e2660-229">Define an SSL policy.</span></span> <span data-ttu-id="e2660-230">在下列範例中，會停用 TLSv1.0 和 TLSv1.1，且只有 **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256**、**TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384** 和 **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** 是允許的加密套件。</span><span class="sxs-lookup"><span data-stu-id="e2660-230">In the following example, TLSv1.0 and TLSv1.1 are disabled and the cipher suites **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256**, **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**, and **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** are the only ones allowed.</span></span>

```powershell
Set-AzureRmApplicationGatewaySSLPolicy -MinProtocolVersion -PolicyType Custom -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", "TLS_RSA_WITH_AES_128_GCM_SHA256" -ApplicationGateway $gw

```

### <a name="step-3"></a><span data-ttu-id="e2660-231">步驟 3</span><span class="sxs-lookup"><span data-stu-id="e2660-231">Step 3</span></span>

<span data-ttu-id="e2660-232">最後，更新閘道。</span><span class="sxs-lookup"><span data-stu-id="e2660-232">Finally, update the gateway.</span></span> <span data-ttu-id="e2660-233">請務必注意，此最後一個步驟是漫長的工作。</span><span class="sxs-lookup"><span data-stu-id="e2660-233">It is important to note that this last step is a long running task.</span></span> <span data-ttu-id="e2660-234">完成時，應用程式閘道上便已設定端對端 SSL。</span><span class="sxs-lookup"><span data-stu-id="e2660-234">When it is done, end to end SSL is configured on the application gateway.</span></span>

```powershell
$gw | Set-AzureRmApplicationGateway
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="e2660-235">取得應用程式閘道 DNS 名稱</span><span class="sxs-lookup"><span data-stu-id="e2660-235">Get application gateway DNS name</span></span>

<span data-ttu-id="e2660-236">建立閘道之後，下一步是設定通訊的前端。</span><span class="sxs-lookup"><span data-stu-id="e2660-236">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="e2660-237">當使用公用 IP 時，應用程式閘道需要動態指派的 DNS 名稱 (不易記住)。</span><span class="sxs-lookup"><span data-stu-id="e2660-237">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="e2660-238">為了確保使用者可以叫用應用程式閘道，可使用 CNAME 記錄來指向應用程式閘道的公用端點。</span><span class="sxs-lookup"><span data-stu-id="e2660-238">To ensure end users can hit the application gateway, a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="e2660-239">[在 Azure 中設定自訂網域名稱](../cloud-services/cloud-services-custom-domain-name-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="e2660-239">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="e2660-240">做法是使用連接至應用程式閘道的 PublicIPAddress 元素，擷取應用程式閘道的詳細資料及其關聯的 IP/DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="e2660-240">To do this, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="e2660-241">應用程式閘道的 DNS 名稱應該用來建立將兩個 Web 應用程式指向此 DNS 名稱的 CNAME 記錄。</span><span class="sxs-lookup"><span data-stu-id="e2660-241">The application gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span></span> <span data-ttu-id="e2660-242">不建議使用 A-records，因為重新啟動應用程式閘道時，VIP 可能會變更。</span><span class="sxs-lookup"><span data-stu-id="e2660-242">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="e2660-243">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e2660-243">Next steps</span></span>

<span data-ttu-id="e2660-244">瀏覽 [Web 應用程式防火牆概觀](application-gateway-webapplicationfirewall-overview.md)</span><span class="sxs-lookup"><span data-stu-id="e2660-244">Learn about hardening the security of your web applications with Web Application Firewall through Application Gateway by visiting [Web Application Firewall Overview](application-gateway-webapplicationfirewall-overview.md)</span></span>

[scenario]: ./media/application-gateway-end-to-end-SSL-powershell/scenario.png
