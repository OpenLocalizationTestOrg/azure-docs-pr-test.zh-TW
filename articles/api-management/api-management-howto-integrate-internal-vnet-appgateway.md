---
title: "aaaHow toouse 與應用程式閘道的虛擬網路中的 Azure API 管理 |Microsoft 文件"
description: "深入了解如何 toosetup 和內部虛擬網路與應用程式閘道 (WAF) 做為前端中設定 Azure API 管理"
services: api-management
documentationcenter: 
author: solankisamir
manager: kjoshi
editor: antonba
ms.assetid: a8c982b2-bca5-4312-9367-4a0bbc1082b1
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/16/2017
ms.author: sasolank
ms.openlocfilehash: 74303a2ee8a10db633ab1740ec7267728eacb473
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-api-management-in-an-internal-vnet-with-application-gateway"></a><span data-ttu-id="4cb7f-103">整合內部 VNET 中的 API 管理與應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="4cb7f-103">Integrate API Management in an internal VNET with Application Gateway</span></span> 

##<span data-ttu-id="4cb7f-104"><a name="overview"></a>概觀</span><span class="sxs-lookup"><span data-stu-id="4cb7f-104"><a name="overview"> </a> Overview</span></span>
 
<span data-ttu-id="4cb7f-105">hello API 管理服務可以在內部的模式，使其只能從 hello 虛擬網路中存取的虛擬網路設定。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-105">hello API Management service can be configured in a Virtual Network in internal mode which makes it accessible only from within hello Virtual Network.</span></span> <span data-ttu-id="4cb7f-106">Azure 應用程式閘道是一項 PAAS 服務，可提供第 7 層負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-106">Azure Application Gateway is a PAAS Service which provides a Layer-7 load balancer.</span></span> <span data-ttu-id="4cb7f-107">它可做為反向 Proxy 服務，並在其供應項目中提供 Web 應用程式防火牆 (WAF)。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-107">It acts as a reverse-proxy service and provides among its offering a Web Application Firewall (WAF).</span></span>

<span data-ttu-id="4cb7f-108">結合使用 hello 應用程式閘道前端內部 VNET 中佈建 API 管理可讓 hello 下列案例：</span><span class="sxs-lookup"><span data-stu-id="4cb7f-108">Combining API Management provisioned in an internal VNET with hello Application Gateway frontend enables hello following scenarios:</span></span>

* <span data-ttu-id="4cb7f-109">使用 hello 相同取用者內部和外部的取用者耗用量的 API 管理資源。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-109">Use hello same API Management resource for consumption by both internal consumers and external consumers.</span></span>
* <span data-ttu-id="4cb7f-110">使用單一 API 管理資源，並在 API 管理中定義一部分 API 供外部取用者使用。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-110">Use a single API Management resource and have a subset of APIs defined in API Management available for external consumers.</span></span>
* <span data-ttu-id="4cb7f-111">提供周全的方式 tooswitch 存取 tooAPI 管理 hello 從公用網際網路開啟和關閉。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-111">Provide a turn-key way tooswitch access tooAPI Management from hello public Internet on and off.</span></span> 

##<span data-ttu-id="4cb7f-112"><a name="scenario"></a>案例</span><span class="sxs-lookup"><span data-stu-id="4cb7f-112"><a name="scenario"> </a> Scenario</span></span>
<span data-ttu-id="4cb7f-113">這份文件將涵蓋如何 toouse 單一的 API 管理服務的內部和外部的取用者，並將其做為單一前端的兩個內部部署和雲端應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-113">This article will cover how toouse a single API Management service for both internal and external consumers and make it act as a single frontend for both on-prem and cloud APIs.</span></span> <span data-ttu-id="4cb7f-114">您也會看到如何 tooexpose 您的應用程式開發介面 （在其以綠色反白顯示 hello 範例） 的子集供外部使用使用中應用程式閘道所提供的 hello PathBasedRouting 功能。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-114">You will also see how tooexpose only a subset of your APIs (in hello example they are highlighted in green) for External Consumption using hello PathBasedRouting functionality available in Application Gateway.</span></span>

<span data-ttu-id="4cb7f-115">Hello 第一個安裝程式範例中是只能從虛擬網路中管理您的 Api。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-115">In hello first setup example all your APIs are managed only from within your Virtual Network.</span></span> <span data-ttu-id="4cb7f-116">內部取用者 (以橘色醒目提示) 則可存取所有的內部和外部 API。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-116">Internal consumers (highlighted in orange) can access all your internal and external APIs.</span></span> <span data-ttu-id="4cb7f-117">流量不會傳遞高效能的 tooInternet 透過 Express Route 電路。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-117">Traffic never goes out tooInternet a high performance is delivered via Express Route circuits.</span></span>

![URL 路由](./media/api-management-howto-integrate-internal-vnet-appgateway/api-management-howto-integrate-internal-vnet-appgateway.png)

## <span data-ttu-id="4cb7f-119"><a name="before-you-begin"></a>開始之前</span><span class="sxs-lookup"><span data-stu-id="4cb7f-119"><a name="before-you-begin"> </a> Before you begin</span></span>

1. <span data-ttu-id="4cb7f-120">使用 hello Web Platform Installer 安裝 hello hello Azure PowerShell cmdlet 的最新版本。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-120">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="4cb7f-121">您可以從下載並安裝最新版本的 hello hello **Windows PowerShell**區段 hello[下載頁面](https://azure.microsoft.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-121">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="4cb7f-122">建立虛擬網路，並為 API 管理和應用程式閘道建立個別子網路。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-122">Create a Virtual Network and create separate subnets for API Management and Application Gateway.</span></span> 
3. <span data-ttu-id="4cb7f-123">如果您想 toocreate hello 虛擬網路的自訂 DNS 伺服器，請啟動 hello 部署前。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-123">If you intend toocreate a custom DNS server for hello Virtual Network, do so before starting hello deployment.</span></span> <span data-ttu-id="4cb7f-124">檢查它的運作方式是確保在 hello 虛擬網路中的新子網路中建立的虛擬機器可以解析和存取所有 Azure 服務端點。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-124">Double check it works by ensuring a virtual machine created in a new subnet in hello Virtual Network can resolve and access all Azure service endpoints.</span></span>

## <a name="what-is-required-toocreate-an-integration-between-api-management-and-application-gateway"></a><span data-ttu-id="4cb7f-125">需要的 toocreate API 管理和應用程式閘道之間的整合為何？</span><span class="sxs-lookup"><span data-stu-id="4cb7f-125">What is required toocreate an integration between API Management and Application Gateway?</span></span>

* <span data-ttu-id="4cb7f-126">**後端伺服器集區：**這是 hello 內部虛擬 IP 位址的 hello API 管理服務。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-126">**Back-end server pool:** This is hello internal virtual IP address of hello API Management service.</span></span>
* <span data-ttu-id="4cb7f-127">**後端伺服器集區設定：** 每個集區都包括一些設定，例如連接埠、通訊協定和以 Cookie 為基礎的同質性。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-127">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="4cb7f-128">這些設定會套用的 tooall hello 集區內的伺服器。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-128">These settings are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="4cb7f-129">**前端連接埠：**這是 hello 應用程式閘道開啟 hello 公用連接埠。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-129">**Front-end port:** This is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="4cb7f-130">叫用它的流量取得重新導向的 tooone hello 的後端伺服器。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-130">Traffic hitting it gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="4cb7f-131">**接聽程式：** hello 接聽程式有前端連接埠的通訊協定 （Http 或 Https，這些值會區分大小寫），與 hello 的 SSL 憑證名稱 （如果有設定 SSL 卸載）。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-131">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="4cb7f-132">**規則：** hello 規則繫結的接聽程式 tooa 後端伺服器集區。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-132">**Rule:** hello rule binds a listener tooa back-end server pool.</span></span>
* <span data-ttu-id="4cb7f-133">**自訂的健全狀況探查：**應用程式閘道，根據預設，使用 IP 位址的探查 toofigure out hello 在哪些伺服器 BackendAddressPool 在使用中。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-133">**Custom Health Probe:** Application Gateway, by default, uses IP address based probes toofigure out which servers in hello BackendAddressPool are active.</span></span> <span data-ttu-id="4cb7f-134">hello API 管理服務只會回應 toorequests 具有 hello 正確的主機標頭，因此 hello 預設探查失敗。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-134">hello API Management service only responds toorequests which have hello correct host header, hence hello default probes fail.</span></span> <span data-ttu-id="4cb7f-135">自訂的健全狀況探查需要定義 toobe toohelp 應用程式閘道判斷出 hello 服務正在執行，而且應該將要求轉送。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-135">A custom health probe needs toobe defined toohelp application gateway determine that hello service is alive and it should forward requests.</span></span>
* <span data-ttu-id="4cb7f-136">**自訂網域的憑證：** tooaccess API 管理從 hello 網際網路需要 toocreate 其主機名稱 toohello 應用程式閘道前端 DNS 名稱的 CNAME 對應。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-136">**Custom domain certificate:** tooaccess API Management from hello internet you need toocreate a CNAME mapping of its hostname toohello Application Gateway front-end DNS name.</span></span> <span data-ttu-id="4cb7f-137">這可確保 hello 主機名稱標頭和傳送憑證 tooApplication tooAPI 轉送閘道管理一個 APIM 可辨識為有效。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-137">This ensures that hello hostname header and certificate sent tooApplication Gateway that is forwarded tooAPI Management is one APIM can recognize as valid.</span></span>

## <span data-ttu-id="4cb7f-138"><a name="overview-steps"></a>整合 API 管理和應用程式閘道的所需步驟</span><span class="sxs-lookup"><span data-stu-id="4cb7f-138"><a name="overview-steps"> </a> Steps required for integrating API Management and Application Gateway</span></span> 

1. <span data-ttu-id="4cb7f-139">建立資源管理員的資源群組。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-139">Create a resource group for Resource Manager.</span></span>
2. <span data-ttu-id="4cb7f-140">建立虛擬網路、 子網路和 hello 應用程式閘道的公用 IP。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-140">Create a Virtual Network, subnet, and public IP for hello Application Gateway.</span></span> <span data-ttu-id="4cb7f-141">為 API 管理建立其他子網路。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-141">Create another subnet for API Management.</span></span>
3. <span data-ttu-id="4cb7f-142">建立 API 管理服務，在上面所建立的 hello VNET 子網路內，並確定您使用 hello 內部的模式。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-142">Create an API Management service inside hello VNET subnet created above and ensure you use hello Internal mode.</span></span>
4. <span data-ttu-id="4cb7f-143">安裝程式在 hello API 管理服務中的 hello 自訂網域名稱。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-143">Setup hello custom domain name in hello API Management service.</span></span>
5. <span data-ttu-id="4cb7f-144">建立應用程式閘道組態物件。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-144">Create an Application Gateway configuration object.</span></span>
6. <span data-ttu-id="4cb7f-145">建立應用程式閘道資源。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-145">Create an Application Gateway resource.</span></span>
7. <span data-ttu-id="4cb7f-146">建立 CNAME，從 hello 公開 DNS 名稱的 hello 應用程式閘道 toohello API 管理 proxy 主機名稱。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-146">Create a CNAME from hello public DNS name of hello Application Gateway toohello API Management proxy hostname.</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="4cb7f-147">建立資源管理員的資源群組</span><span class="sxs-lookup"><span data-stu-id="4cb7f-147">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="4cb7f-148">請確定您使用 Azure PowerShell hello 最新版本。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-148">Make sure that you are using hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="4cb7f-149">如需詳細資訊，請參閱 [搭配使用 Windows PowerShell 與資源管理員](../powershell-azure-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-149">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="4cb7f-150">步驟 1</span><span class="sxs-lookup"><span data-stu-id="4cb7f-150">Step 1</span></span>

<span data-ttu-id="4cb7f-151">登入 tooAzure</span><span class="sxs-lookup"><span data-stu-id="4cb7f-151">Log in tooAzure</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="4cb7f-152">使用您的認證進行驗證。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-152">Authenticate with your credentials.</span></span><BR>

### <a name="step-2"></a><span data-ttu-id="4cb7f-153">步驟 2</span><span class="sxs-lookup"><span data-stu-id="4cb7f-153">Step 2</span></span>

<span data-ttu-id="4cb7f-154">檢查 hello 訂閱 hello 帳戶，並加以選取。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-154">Check hello subscriptions for hello account and select it.</span></span>

```powershell
Get-AzureRmSubscription -Subscriptionid "GUID of subscription" | Select-AzureRmSubscription
```

### <a name="step-3"></a><span data-ttu-id="4cb7f-155">步驟 3</span><span class="sxs-lookup"><span data-stu-id="4cb7f-155">Step 3</span></span>

<span data-ttu-id="4cb7f-156">建立資源群組 (若使用現有的資源群組，請略過此步驟)。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-156">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name "apim-appGw-RG" -Location "West US"
```
<span data-ttu-id="4cb7f-157">Azure Resource Manager 需要所有的資源群組指定一個位置。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-157">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="4cb7f-158">這當做 hello 預設位置，該資源群組中的資源。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-158">This is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="4cb7f-159">請確定所有命令 toocreate 應用程式閘道使用 hello 相同的資源群組。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-159">Make sure that all commands toocreate an application gateway use hello same resource group.</span></span>

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a><span data-ttu-id="4cb7f-160">建立虛擬網路和 hello 應用程式閘道的子網路</span><span class="sxs-lookup"><span data-stu-id="4cb7f-160">Create a Virtual Network and a subnet for hello application gateway</span></span>

<span data-ttu-id="4cb7f-161">hello 下列範例示範如何使用虛擬網路的 toocreate hello 資源管理員。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-161">hello following example shows how toocreate a Virtual Network using hello resource manager.</span></span>

### <a name="step-1"></a><span data-ttu-id="4cb7f-162">步驟 1</span><span class="sxs-lookup"><span data-stu-id="4cb7f-162">Step 1</span></span>

<span data-ttu-id="4cb7f-163">指派 hello 位址範圍 10.0.0.0/24 toohello 子網路變數 toobe 建立虛擬網路時使用應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-163">Assign hello address range 10.0.0.0/24 toohello subnet variable toobe used for Application Gateway while creating a Virtual Network.</span></span>

```powershell
$appgatewaysubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "apim01" -AddressPrefix "10.0.0.0/24"
```

### <a name="step-2"></a><span data-ttu-id="4cb7f-164">步驟 2</span><span class="sxs-lookup"><span data-stu-id="4cb7f-164">Step 2</span></span>

<span data-ttu-id="4cb7f-165">指派 hello 位址範圍 10.0.1.0/24 toohello 子網路變數 toobe 建立虛擬網路時使用的 API 管理。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-165">Assign hello address range 10.0.1.0/24 toohello subnet variable toobe used for API Management while creating a Virtual Network.</span></span>

```powershell
$apimsubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "apim02" -AddressPrefix "10.0.1.0/24"
```

### <a name="step-3"></a><span data-ttu-id="4cb7f-166">步驟 3</span><span class="sxs-lookup"><span data-stu-id="4cb7f-166">Step 3</span></span>

<span data-ttu-id="4cb7f-167">建立虛擬網路，名為**appgwvnet**資源群組中**apim-appGw-RG**使用 hello 前置詞 10.0.0.0/16 hello 美國西部地區與子網路 10.0.0.0/24 10.0.1.0/24。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-167">Create a Virtual Network named **appgwvnet** in resource group **apim-appGw-RG** for hello West US region using hello prefix 10.0.0.0/16 with subnets 10.0.0.0/24 and 10.0.1.0/24.</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name "appgwvnet" -ResourceGroupName "apim-appGw-RG" -Location "West US" -AddressPrefix "10.0.0.0/16" -Subnet $appgatewaysubnet,$apimsubnet
```

### <a name="step-4"></a><span data-ttu-id="4cb7f-168">步驟 4</span><span class="sxs-lookup"><span data-stu-id="4cb7f-168">Step 4</span></span>

<span data-ttu-id="4cb7f-169">指派子網路變數 hello 接下來的步驟</span><span class="sxs-lookup"><span data-stu-id="4cb7f-169">Assign a subnet variable for hello next steps</span></span>

```powershell
$appgatewaysubnetdata=$vnet.Subnets[0]
$apimsubnetdata=$vnet.Subnets[1]
```
## <a name="create-an-api-management-service-inside-a-vnet-configured-in-internal-mode"></a><span data-ttu-id="4cb7f-170">在以內部模式設定的 VNET 內建立 API 管理服務</span><span class="sxs-lookup"><span data-stu-id="4cb7f-170">Create an API Management service inside a VNET configured in internal mode</span></span>

<span data-ttu-id="4cb7f-171">hello 下列範例顯示如何 toocreate 在 VNET 中的 API 管理服務設定為僅限內部存取。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-171">hello following example shows how toocreate an API Management service in a VNET configured for internal access only.</span></span>

### <a name="step-1"></a><span data-ttu-id="4cb7f-172">步驟 1</span><span class="sxs-lookup"><span data-stu-id="4cb7f-172">Step 1</span></span>
<span data-ttu-id="4cb7f-173">建立使用 hello 子網路 $apimsubnetdata 上面所建立的應用程式開發介面管理虛擬網路物件。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-173">Create an API Management Virtual Network object using hello subnet $apimsubnetdata created above.</span></span>

```powershell
$apimVirtualNetwork = New-AzureRmApiManagementVirtualNetwork -Location "West US" -SubnetResourceId $apimsubnetdata.Id
```
### <a name="step-2"></a><span data-ttu-id="4cb7f-174">步驟 2</span><span class="sxs-lookup"><span data-stu-id="4cb7f-174">Step 2</span></span>
<span data-ttu-id="4cb7f-175">建立 API 管理服務，hello 虛擬網路內。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-175">Create an API Management service inside hello Virtual Network.</span></span>

```powershell
$apimService = New-AzureRmApiManagement -ResourceGroupName "apim-appGw-RG" -Location "West US" -Name "ContosoApi" -Organization "Contoso" -AdminEmail "admin@contoso.com" -VirtualNetwork $apimVirtualNetwork -VpnType "Internal" -Sku "Developer"
```
<span data-ttu-id="4cb7f-176">上述命令 hello 成功之後，請參閱太[需要 tooaccess 內部 VNET API 管理服務的 DNS 設定](api-management-using-with-internal-vnet.md#apim-dns-configuration)tooaccess 它。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-176">After hello above command succeeds refer too[DNS Configuration required tooaccess internal VNET API Management service](api-management-using-with-internal-vnet.md#apim-dns-configuration) tooaccess it.</span></span>

## <a name="set-up-a-custom-domain-name-in-api-management"></a><span data-ttu-id="4cb7f-177">在 API 管理中設定自訂網域名稱</span><span class="sxs-lookup"><span data-stu-id="4cb7f-177">Set-up a custom domain name in API Management</span></span>

### <a name="step-1"></a><span data-ttu-id="4cb7f-178">步驟 1</span><span class="sxs-lookup"><span data-stu-id="4cb7f-178">Step 1</span></span>
<span data-ttu-id="4cb7f-179">Hello 憑證上傳具有私密金鑰的 hello 網域。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-179">Upload hello certificate with private key for hello domain.</span></span> <span data-ttu-id="4cb7f-180">這個範例中就會是 `*.contoso.net`。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-180">For this example it will be `*.contoso.net`.</span></span> 

```powershell
$certUploadResult = Import-AzureRmApiManagementHostnameCertificate -ResourceGroupName "apim-appGw-RG" -Name "ContosoApi" -HostnameType "Proxy" -PfxPath <full path too.pfx file> -PfxPassword <password for certificate file> -PassThru
```

### <a name="step-2"></a><span data-ttu-id="4cb7f-181">步驟 2</span><span class="sxs-lookup"><span data-stu-id="4cb7f-181">Step 2</span></span>
<span data-ttu-id="4cb7f-182">Hello 憑證上傳，一旦建立 hello proxy 主機名稱設定物件的主機名稱與`api.contoso.net`，如 hello 範例憑證授權單位提供 hello`*.contoso.net`網域。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-182">Once hello certificate is uploaded, create a hostname configuration object for hello proxy with a hostname of `api.contoso.net`, as hello example certificate provides authority for hello  `*.contoso.net` domain.</span></span> 

```powershell
$proxyHostnameConfig = New-AzureRmApiManagementHostnameConfiguration -CertificateThumbprint $certUploadResult.Thumbprint -Hostname "api.contoso.net"
$result = Set-AzureRmApiManagementHostnames -Name "ContosoApi" -ResourceGroupName "apim-appGw-RG" -ProxyHostnameConfiguration $proxyHostnameConfig
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a><span data-ttu-id="4cb7f-183">建立 hello 前端組態的公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="4cb7f-183">Create a public IP address for hello front-end configuration</span></span>

<span data-ttu-id="4cb7f-184">建立公用 IP 資源**publicIP01**資源群組中**apim-appGw-RG** hello 美國西部地區。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-184">Create a public IP resource **publicIP01** in resource group **apim-appGw-RG** for hello West US region.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName "apim-appGw-RG" -name "publicIP01" -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="4cb7f-185">Hello 服務啟動時，會指派 toohello 應用程式閘道 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-185">An IP address is assigned toohello application gateway when hello service starts.</span></span>

## <a name="create-application-gateway-configuration"></a><span data-ttu-id="4cb7f-186">建立應用程式閘道組態</span><span class="sxs-lookup"><span data-stu-id="4cb7f-186">Create application gateway configuration</span></span>

<span data-ttu-id="4cb7f-187">所有設定項目必須都設定才能建立 hello 應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-187">All configuration items must be set up before creating hello application gateway.</span></span> <span data-ttu-id="4cb7f-188">hello 下列步驟建立 hello 組態項目所需的應用程式閘道資源。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-188">hello following steps create hello configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="4cb7f-189">步驟 1</span><span class="sxs-lookup"><span data-stu-id="4cb7f-189">Step 1</span></span>

<span data-ttu-id="4cb7f-190">建立名為 **gatewayIP01** 的應用程式閘道 IP 組態。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-190">Create an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="4cb7f-191">應用程式閘道啟動時，它會挑選設定 hello 子網路的 IP 位址，並傳送 hello 後端 IP 集區中的網路流量 toohello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-191">When Application Gateway starts, it picks up an IP address from hello subnet configured and route network traffic toohello IP addresses in hello back-end IP pool.</span></span> <span data-ttu-id="4cb7f-192">請記住，每個執行個體需要一個 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-192">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name "gatewayIP01" -Subnet $appgatewaysubnetdata
```

### <a name="step-2"></a><span data-ttu-id="4cb7f-193">步驟 2</span><span class="sxs-lookup"><span data-stu-id="4cb7f-193">Step 2</span></span>

<span data-ttu-id="4cb7f-194">設定 hello 前端 IP 連接埠 hello 公用 IP 端點。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-194">Configure hello front-end IP port for hello public IP endpoint.</span></span> <span data-ttu-id="4cb7f-195">此連接埠是使用者連線到的 hello 連接埠。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-195">This port is hello port that end users connect to.</span></span>

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "port01"  -Port 443
```
### <a name="step-3"></a><span data-ttu-id="4cb7f-196">步驟 3</span><span class="sxs-lookup"><span data-stu-id="4cb7f-196">Step 3</span></span>

<span data-ttu-id="4cb7f-197">設定公用 IP 端點 hello 前端 IP。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-197">Configure hello front-end IP with public IP endpoint.</span></span>

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-4"></a><span data-ttu-id="4cb7f-198">步驟 4</span><span class="sxs-lookup"><span data-stu-id="4cb7f-198">Step 4</span></span>

<span data-ttu-id="4cb7f-199">設定 hello 憑證 hello 應用程式閘道使用 toodecrypt 和重新加密 hello 流量通過。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-199">Configure hello certificate for hello Application Gateway, used toodecrypt and re-encrypt hello traffic passing through.</span></span>

```powershell
$cert = New-AzureRmApplicationGatewaySslCertificate -Name "cert01" -CertificateFile <full path too.pfx file> -Password <password for certificate file>
```

### <a name="step-5"></a><span data-ttu-id="4cb7f-200">步驟 5</span><span class="sxs-lookup"><span data-stu-id="4cb7f-200">Step 5</span></span>

<span data-ttu-id="4cb7f-201">建立 hello 應用程式閘道的 hello HTTP 接聽程式。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-201">Create hello HTTP listener for hello Application Gateway.</span></span> <span data-ttu-id="4cb7f-202">Hello 前端 IP 組態、 連接埠，以及 ssl 憑證 tooit 指派。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-202">Assign hello front-end IP configuration, port, and ssl certificate tooit.</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol "Https" -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -SslCertificate $cert
```

### <a name="step-6"></a><span data-ttu-id="4cb7f-203">步驟 6</span><span class="sxs-lookup"><span data-stu-id="4cb7f-203">Step 6</span></span>

<span data-ttu-id="4cb7f-204">建立 API 管理服務的自訂探查 toohello `ContosoApi` proxy 網域端點。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-204">Create a custom probe toohello API Management service `ContosoApi` proxy domain endpoint.</span></span> <span data-ttu-id="4cb7f-205">hello 路徑`/status-0123456789abcdef`預設健全狀況的端點上所有的 hello API 管理服務裝載。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-205">hello path `/status-0123456789abcdef` is a default health endpoint hosted on all hello API Management services.</span></span> <span data-ttu-id="4cb7f-206">設定`api.contoso.net`自訂探查主機名稱 toosecure 為使用 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-206">Set `api.contoso.net` as a custom probe hostname toosecure it with SSL certificate.</span></span>

> [!NOTE]
> <span data-ttu-id="4cb7f-207">hello hostname `contosoapi.azure-api.net` hello 預設 proxy 主機名稱設定名為的服務時`contosoapi`公用 Azure 中建立。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-207">hello hostname `contosoapi.azure-api.net` is hello default proxy hostname configured when a service named `contosoapi` is created in public Azure.</span></span> 
> 

```powershell
$apimprobe = New-AzureRmApplicationGatewayProbeConfig -Name "apimproxyprobe" -Protocol "Https" -HostName "api.contoso.net" -Path "/status-0123456789abcdef" -Interval 30 -Timeout 120 -UnhealthyThreshold 8
```

### <a name="step-7"></a><span data-ttu-id="4cb7f-208">步驟 7</span><span class="sxs-lookup"><span data-stu-id="4cb7f-208">Step 7</span></span>

<span data-ttu-id="4cb7f-209">上傳 hello toobe 用於 hello 啟用 SSL 的後端集區的資源上的憑證。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-209">Upload hello certificate toobe used on hello SSL-enabled backend pool resources.</span></span> <span data-ttu-id="4cb7f-210">這是 hello 同一個憑證，您在上述步驟 4 中提供。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-210">This is hello same certificate which you provided in Step 4 above.</span></span>

```powershell
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name "whitelistcert1" -CertificateFile <full path too.cer file>
```

### <a name="step-8"></a><span data-ttu-id="4cb7f-211">步驟 8</span><span class="sxs-lookup"><span data-stu-id="4cb7f-211">Step 8</span></span>

<span data-ttu-id="4cb7f-212">設定 HTTP hello 應用程式閘道後端設定。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-212">Configure HTTP backend settings for hello Application Gateway.</span></span> <span data-ttu-id="4cb7f-213">這包括設定之後會取消的後端要求逾時限制。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-213">This includes setting a time-out limit for backend request after which they are cancelled.</span></span> <span data-ttu-id="4cb7f-214">此值與不同 hello 探查的逾時。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-214">This value is different from hello probe time-out.</span></span>

```powershell
$apimPoolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "apimPoolSetting" -Port 443 -Protocol "Https" -CookieBasedAffinity "Disabled" -Probe $apimprobe -AuthenticationCertificates $authcert -RequestTimeout 180
```

### <a name="step-9"></a><span data-ttu-id="4cb7f-215">步驟 9</span><span class="sxs-lookup"><span data-stu-id="4cb7f-215">Step 9</span></span>

<span data-ttu-id="4cb7f-216">設定名為後端 IP 位址集區**apimbackend**上面建立 hello 內部的虛擬 ip 位址的 hello API 管理服務。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-216">Configure a back-end IP address pool named **apimbackend**  with hello internal virtual IP address of hello API Management service created above.</span></span>

```powershell
$apimProxyBackendPool = New-AzureRmApplicationGatewayBackendAddressPool -Name "apimbackend" -BackendIPAddresses $apimService.StaticIPs[0]
```

### <a name="step-10"></a><span data-ttu-id="4cb7f-217">步驟 10</span><span class="sxs-lookup"><span data-stu-id="4cb7f-217">Step 10</span></span>

<span data-ttu-id="4cb7f-218">建立虛擬 (不存在) 後端的設定。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-218">Create settings for a dummy (non-existent) backend.</span></span> <span data-ttu-id="4cb7f-219">我們不想要從應用程式閘道透過 API 管理 tooexpose 要求 tooAPI 路徑將會叫用這個後端，並傳回 404。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-219">Requests tooAPI paths that we do not want tooexpose from API Management via Application Gateway will hit this backend and return 404.</span></span>

<span data-ttu-id="4cb7f-220">設定 hello dummy 後端 HTTP 設定。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-220">Configure HTTP settings for hello dummy backend.</span></span>

```powershell
$dummyBackendSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "dummySetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled
```

<span data-ttu-id="4cb7f-221">設定空的後端**dummyBackendPool**，哪些點 tooa FQDN 位址**dummybackend.com**。這個 FQDN 的地址不存在於 hello 虛擬網路中。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-221">Configure a dummy backend **dummyBackendPool**, which points tooa FQDN address **dummybackend.com**. This FQDN address does not exist in hello virtual network.</span></span>

```powershell
$dummyBackendPool = New-AzureRmApplicationGatewayBackendAddressPool -Name "dummyBackendPool" -BackendFqdns "dummybackend.com"
```

<span data-ttu-id="4cb7f-222">建立規則，設定預設指向 toohello 不存在後端應用程式閘道會使用該 hello **dummybackend.com** hello 虛擬網路中。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-222">Create a rule setting that hello Application Gateway will use by default which points toohello non-existent backend **dummybackend.com** in hello Virtual Network.</span></span>

```powershell
$dummyPathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "nonexistentapis" -Paths "/*" -BackendAddressPool $dummyBackendPool -BackendHttpSettings $dummyBackendSetting
```

### <a name="step-11"></a><span data-ttu-id="4cb7f-223">步驟 11</span><span class="sxs-lookup"><span data-stu-id="4cb7f-223">Step 11</span></span>

<span data-ttu-id="4cb7f-224">設定 URL 規則路徑 hello 後端集區。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-224">Configure URL rule paths for hello back-end pools.</span></span> <span data-ttu-id="4cb7f-225">這可讓某些 hello 從 API 管理 Api 所公開 toohello 公用只選取。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-225">This enables selecting only some of hello APIs from API Management for being exposed toohello public.</span></span> <span data-ttu-id="4cb7f-226">例如，如果有 `Echo API` (/echo/)、`Calculator API` (/calc/) 等，則讓 `Echo API` 只能從網際網路存取。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-226">For example, if there are `Echo API` (/echo/), `Calculator API` (/calc/) etc. make only `Echo API` accessible from Internet).</span></span> 

<span data-ttu-id="4cb7f-227">hello 下列範例會建立一個簡單的規則，為 「 hello 」 / 「 回應 /"路徑路由流量 toohello 後端 」 apimProxyBackendPool"。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-227">hello following example creates a simple rule for hello "/echo/" path routing traffic toohello back-end "apimProxyBackendPool".</span></span>

```powershell
$echoapiRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "externalapis" -Paths "/echo/*" -BackendAddressPool $apimProxyBackendPool -BackendHttpSettings $apimPoolSetting
```

<span data-ttu-id="4cb7f-228">如果不符合 hello 路徑 hello 路徑規則，我們想要從 API 管理，hello 規則路徑對應組態也會設定名為的後端位址集區預設 tooenable **dummyBackendPool**。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-228">If hello path doesn't match hello path rules we want tooenable from API Management, hello rule path map configuration also configures a default back-end address pool named **dummyBackendPool**.</span></span> <span data-ttu-id="4cb7f-229">例如，http://api.contoso.net/calc/ * 會太**dummyBackendPool**定義為 hello 預設集區不相符的流量。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-229">For example, http://api.contoso.net/calc/* goes too**dummyBackendPool** as it is defined as hello default pool for un-matched traffic.</span></span>

```powershell
$urlPathMap = New-AzureRmApplicationGatewayUrlPathMapConfig -Name "urlpathmap" -PathRules $echoapiRule, $dummyPathRule -DefaultBackendAddressPool $dummyBackendPool -DefaultBackendHttpSettings $dummyBackendSetting
```

<span data-ttu-id="4cb7f-230">hello 上面步驟可確保，只會要求 hello 路徑"/ 回應 」 可通過 hello 應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-230">hello above step ensures that only requests for hello path "/echo" are allowed through hello Application Gateway.</span></span> <span data-ttu-id="4cb7f-231">要求 tooother API 管理中設定的應用程式開發介面會從應用程式閘道從 hello 網際網路存取時擲回 404 錯誤。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-231">Requests tooother APIs configured in API Management will throw 404 errors from Application Gateway when accessed from hello Internet.</span></span> 

### <a name="step-12"></a><span data-ttu-id="4cb7f-232">步驟 12</span><span class="sxs-lookup"><span data-stu-id="4cb7f-232">Step 12</span></span>

<span data-ttu-id="4cb7f-233">建立 hello 應用程式閘道 toouse URL 路徑為基礎的路由規則設定。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-233">Create a rule setting for hello Application Gateway toouse URL path-based routing.</span></span>

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule1" -RuleType PathBasedRouting -HttpListener $listener -UrlPathMap $urlPathMap
```

### <a name="step-13"></a><span data-ttu-id="4cb7f-234">步驟 13</span><span class="sxs-lookup"><span data-stu-id="4cb7f-234">Step 13</span></span>

<span data-ttu-id="4cb7f-235">設定 hello 數量的執行個體和 hello 應用程式閘道的大小。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-235">Configure hello number of instances and size for hello Application Gateway.</span></span> <span data-ttu-id="4cb7f-236">這裡我們使用 hello [WAF SKU](../application-gateway/application-gateway-webapplicationfirewall-overview.md)以 hello API 管理資源的提高安全性。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-236">Here we are using hello [WAF SKU](../application-gateway/application-gateway-webapplicationfirewall-overview.md) for increased security of hello API Management resource.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "WAF_Medium" -Tier "WAF" -Capacity 2
```

### <a name="step-14"></a><span data-ttu-id="4cb7f-237">步驟 14</span><span class="sxs-lookup"><span data-stu-id="4cb7f-237">Step 14</span></span>

<span data-ttu-id="4cb7f-238">「 防止 」 模式中設定 WAF toobe。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-238">Configure WAF toobe in "Prevention" mode.</span></span>
```powershell
$config = New-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode "Prevention"
```

## <a name="create-application-gateway"></a><span data-ttu-id="4cb7f-239">建立應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="4cb7f-239">Create Application Gateway</span></span>

<span data-ttu-id="4cb7f-240">建立應用程式閘道與 hello 先前步驟中的所有 hello 組態物件。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-240">Create an Application Gateway with all hello configuration objects from hello preceding steps.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name $applicationGatewayName -ResourceGroupName $resourceGroupName  -Location $location -BackendAddressPools $apimProxyBackendPool, $dummyBackendPool -BackendHttpSettingsCollection $apimPoolSetting, $dummyBackendSetting  -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener -UrlPathMaps $urlPathMap -RequestRoutingRules $rule01 -Sku $sku -WebApplicationFirewallConfig $config -SslCertificates $cert -AuthenticationCertificates $authcert -Probes $apimprobe
```

## <a name="cname-hello-api-management-proxy-hostname-toohello-public-dns-name-of-hello-application-gateway-resource"></a><span data-ttu-id="4cb7f-241">CNAME hello API 管理 proxy 主機名稱 toohello 公開 DNS 名稱的 hello 應用程式閘道資源</span><span class="sxs-lookup"><span data-stu-id="4cb7f-241">CNAME hello API Management proxy hostname toohello public DNS name of hello Application Gateway resource</span></span>

<span data-ttu-id="4cb7f-242">一旦建立 hello 閘道，hello 下一個步驟是 tooconfigure hello 前端進行通訊。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-242">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="4cb7f-243">當使用公用 IP 時，應用程式閘道需要動態指派的 DNS 名稱，這可能不是容易 toouse。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-243">When using a public IP, Application Gateway requires a dynamically assigned DNS name, which may not be easy toouse.</span></span> 

<span data-ttu-id="4cb7f-244">hello 應用程式閘道的 DNS 名稱應該使用的 toocreate CNAME 記錄指向 hello APIM proxy 主機名稱 (例如`api.contoso.net`hello 上述範例中) toothis DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-244">hello Application Gateway's DNS name should be used toocreate a CNAME record which points hello APIM proxy host name (e.g. `api.contoso.net` in hello examples above) toothis DNS name.</span></span> <span data-ttu-id="4cb7f-245">tooconfigure hello 前端 IP CNAME 記錄，擷取 hello 應用程式閘道的 hello 詳細資料和其相關聯的 IP/DNS 名稱，使用 hello PublicIPAddress 項目。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-245">tooconfigure hello frontend IP CNAME record, retrieve hello details of hello Application Gateway and its associated IP/DNS name using hello PublicIPAddress element.</span></span> <span data-ttu-id="4cb7f-246">因為 hello VIP 可能會變更在重新啟動閘道，不建議 hello 使用 A 記錄。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-246">hello use of A-records is not recommended since hello VIP may change on restart of gateway.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName "apim-appGw-RG" -Name "publicIP01"
```

##<span data-ttu-id="4cb7f-247"><a name="summary"></a>摘要</span><span class="sxs-lookup"><span data-stu-id="4cb7f-247"><a name="summary"> </a> Summary</span></span>
<span data-ttu-id="4cb7f-248">在 VNET 中設定的 azure API 管理提供單一閘道介面設定的所有 Api，它們是裝載在內部部署還是在 hello 雲端。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-248">Azure API Management configured in a VNET provides a single gateway interface for all configured APIs, whether they are hosted on-prem or in hello cloud.</span></span> <span data-ttu-id="4cb7f-249">使用 API 管理中整合應用程式閘道提供 hello 彈性，選擇性地啟用特定應用程式開發介面 toobe hello 網際網路上進行存取，以及提供 Web 應用程式防火牆做為前端 tooyour API 管理執行個體。</span><span class="sxs-lookup"><span data-stu-id="4cb7f-249">Integrating Application Gateway with API Management provides hello flexibility of selectively enabling particular APIs toobe accessible on hello Internet, as well as providing a Web Application Firewall as a frontend tooyour API Management instance.</span></span>

##<span data-ttu-id="4cb7f-250"><a name="next-steps"></a>後續步驟</span><span class="sxs-lookup"><span data-stu-id="4cb7f-250"><a name="next-steps"> </a> Next steps</span></span>
* <span data-ttu-id="4cb7f-251">深入了解 Azure 應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="4cb7f-251">Learn more about Azure Application Gateway</span></span>
  * [<span data-ttu-id="4cb7f-252">應用程式閘道概觀</span><span class="sxs-lookup"><span data-stu-id="4cb7f-252">Application Gateway Overview</span></span>](../application-gateway/application-gateway-introduction.md)
  * [<span data-ttu-id="4cb7f-253">應用程式閘道 Web 應用程式防火牆</span><span class="sxs-lookup"><span data-stu-id="4cb7f-253">Application Gateway Web Application Firewall</span></span>](../application-gateway/application-gateway-webapplicationfirewall-overview.md)
  * [<span data-ttu-id="4cb7f-254">使用路徑型路由的應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="4cb7f-254">Application Gateway using Path-based Routing</span></span>](../application-gateway/application-gateway-create-url-route-arm-ps.md)
* <span data-ttu-id="4cb7f-255">深入了解 API 管理和 VNET</span><span class="sxs-lookup"><span data-stu-id="4cb7f-255">Learn more about API Management and VNETs</span></span>
  * [<span data-ttu-id="4cb7f-256">使用 API 管理只能在 hello VNET</span><span class="sxs-lookup"><span data-stu-id="4cb7f-256">Using API Management available only within hello VNET</span></span>](api-management-using-with-internal-vnet.md)
  * [<span data-ttu-id="4cb7f-257">在 VNET 中使用 API 管理</span><span class="sxs-lookup"><span data-stu-id="4cb7f-257">Using API Management in VNET</span></span>](api-management-using-with-vnet.md)
