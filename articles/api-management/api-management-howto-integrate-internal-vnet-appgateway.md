---
title: "如何搭配使用虛擬網路中的 Azure API 管理與應用程式閘道 | Microsoft Docs"
description: "了解如何以應用程式閘道 (WAF) 做為前端在內部虛擬網路中安裝和設定 Azure API 管理"
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
ms.openlocfilehash: 8131ded6b74e9c544bf70b1a4659ed07e5def04d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="integrate-api-management-in-an-internal-vnet-with-application-gateway"></a><span data-ttu-id="9e415-103">整合內部 VNET 中的 API 管理與應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="9e415-103">Integrate API Management in an internal VNET with Application Gateway</span></span> 

##<span data-ttu-id="9e415-104"><a name="overview"></a>概觀</span><span class="sxs-lookup"><span data-stu-id="9e415-104"><a name="overview"> </a> Overview</span></span>
 
<span data-ttu-id="9e415-105">API 管理服務可以內部模式設定於虛擬網路中，因此只能從虛擬網路中加以存取。</span><span class="sxs-lookup"><span data-stu-id="9e415-105">The API Management service can be configured in a Virtual Network in internal mode which makes it accessible only from within the Virtual Network.</span></span> <span data-ttu-id="9e415-106">Azure 應用程式閘道是一項 PAAS 服務，可提供第 7 層負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="9e415-106">Azure Application Gateway is a PAAS Service which provides a Layer-7 load balancer.</span></span> <span data-ttu-id="9e415-107">它可做為反向 Proxy 服務，並在其供應項目中提供 Web 應用程式防火牆 (WAF)。</span><span class="sxs-lookup"><span data-stu-id="9e415-107">It acts as a reverse-proxy service and provides among its offering a Web Application Firewall (WAF).</span></span>

<span data-ttu-id="9e415-108">結合使用內部 VNET 中佈建的 API 管理與應用程式閘道前端，可實現下列案例︰</span><span class="sxs-lookup"><span data-stu-id="9e415-108">Combining API Management provisioned in an internal VNET with the Application Gateway frontend enables the following scenarios:</span></span>

* <span data-ttu-id="9e415-109">使用相同的 API 管理資源供內部取用者和外部取用者取用。</span><span class="sxs-lookup"><span data-stu-id="9e415-109">Use the same API Management resource for consumption by both internal consumers and external consumers.</span></span>
* <span data-ttu-id="9e415-110">使用單一 API 管理資源，並在 API 管理中定義一部分 API 供外部取用者使用。</span><span class="sxs-lookup"><span data-stu-id="9e415-110">Use a single API Management resource and have a subset of APIs defined in API Management available for external consumers.</span></span>
* <span data-ttu-id="9e415-111">提供周全的方法來開啟和關閉從公用網際網路對 API 管理的存取權。</span><span class="sxs-lookup"><span data-stu-id="9e415-111">Provide a turn-key way to switch access to API Management from the public Internet on and off.</span></span> 

##<span data-ttu-id="9e415-112"><a name="scenario"></a>案例</span><span class="sxs-lookup"><span data-stu-id="9e415-112"><a name="scenario"> </a> Scenario</span></span>
<span data-ttu-id="9e415-113">本文將討論如何使用單一 API 管理服務供內部和外部取用者使用，並將其同時做為內部部署和雲端 API 的單一前端。</span><span class="sxs-lookup"><span data-stu-id="9e415-113">This article will cover how to use a single API Management service for both internal and external consumers and make it act as a single frontend for both on-prem and cloud APIs.</span></span> <span data-ttu-id="9e415-114">您也會看到使用應用程式閘道中提供的 PathBasedRouting 功能，只公開您 API 的一部分 (在範例中以綠色醒目提示) 供外部取用。</span><span class="sxs-lookup"><span data-stu-id="9e415-114">You will also see how to expose only a subset of your APIs (in the example they are highlighted in green) for External Consumption using the PathBasedRouting functionality available in Application Gateway.</span></span>

<span data-ttu-id="9e415-115">在第一個設定範例中，您所有的 API 只能從虛擬網路內部進行管理。</span><span class="sxs-lookup"><span data-stu-id="9e415-115">In the first setup example all your APIs are managed only from within your Virtual Network.</span></span> <span data-ttu-id="9e415-116">內部取用者 (以橘色醒目提示) 則可存取所有的內部和外部 API。</span><span class="sxs-lookup"><span data-stu-id="9e415-116">Internal consumers (highlighted in orange) can access all your internal and external APIs.</span></span> <span data-ttu-id="9e415-117">流量永遠不會傳出網際網路，高效能會透過 Expressroute 電路傳送。</span><span class="sxs-lookup"><span data-stu-id="9e415-117">Traffic never goes out to Internet a high performance is delivered via Express Route circuits.</span></span>

![URL 路由](./media/api-management-howto-integrate-internal-vnet-appgateway/api-management-howto-integrate-internal-vnet-appgateway.png)

## <span data-ttu-id="9e415-119"><a name="before-you-begin"></a>開始之前</span><span class="sxs-lookup"><span data-stu-id="9e415-119"><a name="before-you-begin"> </a> Before you begin</span></span>

1. <span data-ttu-id="9e415-120">使用 Web Platform Installer 安裝最新版的 Azure PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="9e415-120">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span></span> <span data-ttu-id="9e415-121">您可以從 **下載頁面** 的 [Windows PowerShell](https://azure.microsoft.com/downloads/)區段下載並安裝最新版本。</span><span class="sxs-lookup"><span data-stu-id="9e415-121">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="9e415-122">建立虛擬網路，並為 API 管理和應用程式閘道建立個別子網路。</span><span class="sxs-lookup"><span data-stu-id="9e415-122">Create a Virtual Network and create separate subnets for API Management and Application Gateway.</span></span> 
3. <span data-ttu-id="9e415-123">如果您想要建立虛擬網路的自訂 DNS 伺服器，請在開始部署之前進行。</span><span class="sxs-lookup"><span data-stu-id="9e415-123">If you intend to create a custom DNS server for the Virtual Network, do so before starting the deployment.</span></span> <span data-ttu-id="9e415-124">確保在新的子網路中建立虛擬網路以再次確認它的運作方式，虛擬機器可以解析並存取所有 Azure 服務端點。</span><span class="sxs-lookup"><span data-stu-id="9e415-124">Double check it works by ensuring a virtual machine created in a new subnet in the Virtual Network can resolve and access all Azure service endpoints.</span></span>

## <a name="what-is-required-to-create-an-integration-between-api-management-and-application-gateway"></a><span data-ttu-id="9e415-125">在 API 管理和應用程式閘道之間建立整合的所需條件為何？</span><span class="sxs-lookup"><span data-stu-id="9e415-125">What is required to create an integration between API Management and Application Gateway?</span></span>

* <span data-ttu-id="9e415-126">**後端伺服器集區︰**這是 API 管理服務的內部虛擬 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="9e415-126">**Back-end server pool:** This is the internal virtual IP address of the API Management service.</span></span>
* <span data-ttu-id="9e415-127">**後端伺服器集區設定：** 每個集區都包括一些設定，例如連接埠、通訊協定和以 Cookie 為基礎的同質性。</span><span class="sxs-lookup"><span data-stu-id="9e415-127">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="9e415-128">這些設定會套用至集區內所有伺服器。</span><span class="sxs-lookup"><span data-stu-id="9e415-128">These settings are applied to all servers within the pool.</span></span>
* <span data-ttu-id="9e415-129">**前端連接埠：**這是在應用程式閘道上開啟的公用連接埠。</span><span class="sxs-lookup"><span data-stu-id="9e415-129">**Front-end port:** This is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="9e415-130">到達的流量會重新導向至其中一個後端伺服器。</span><span class="sxs-lookup"><span data-stu-id="9e415-130">Traffic hitting it gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="9e415-131">**接聽程式：** 接聽程式具有前端連接埠、通訊協定 (Http 或 Https，這些值都區分大小寫) 和 SSL 憑證名稱 (如果已設定 SSL 卸載)。</span><span class="sxs-lookup"><span data-stu-id="9e415-131">**Listener:** The listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="9e415-132">**規則︰**規則會繫結接聽程式至後端伺服器集區。</span><span class="sxs-lookup"><span data-stu-id="9e415-132">**Rule:** The rule binds a listener to a back-end server pool.</span></span>
* <span data-ttu-id="9e415-133">**自訂健全狀況探查︰**應用程式閘道預設會使用 IP 位址型探查，來找出 BackendAddressPool 中有哪些伺服器正在作用中。</span><span class="sxs-lookup"><span data-stu-id="9e415-133">**Custom Health Probe:** Application Gateway, by default, uses IP address based probes to figure out which servers in the BackendAddressPool are active.</span></span> <span data-ttu-id="9e415-134">API 管理服務只會回應具有正確主機標頭的要求，因此預設探查會失敗。</span><span class="sxs-lookup"><span data-stu-id="9e415-134">The API Management service only responds to requests which have the correct host header, hence the default probes fail.</span></span> <span data-ttu-id="9e415-135">需要定義自訂的健全狀況探查以協助應用程式閘道判斷服務正在執行，因此它應該轉送要求。</span><span class="sxs-lookup"><span data-stu-id="9e415-135">A custom health probe needs to be defined to help application gateway determine that the service is alive and it should forward requests.</span></span>
* <span data-ttu-id="9e415-136">**自訂網域憑證︰**若要從網際網路存取 API 管理，您需要建立其主機名稱和應用程式閘道前端 DNS 名稱的 CNAME 對應。</span><span class="sxs-lookup"><span data-stu-id="9e415-136">**Custom domain certificate:** To access API Management from the internet you need to create a CNAME mapping of its hostname to the Application Gateway front-end DNS name.</span></span> <span data-ttu-id="9e415-137">這可確保主機名稱的標頭和憑證傳送到轉送至 API 管理的應用程式閘道，是 APIM 可以辨識為有效的。</span><span class="sxs-lookup"><span data-stu-id="9e415-137">This ensures that the hostname header and certificate sent to Application Gateway that is forwarded to API Management is one APIM can recognize as valid.</span></span>

## <span data-ttu-id="9e415-138"><a name="overview-steps"></a>整合 API 管理和應用程式閘道的所需步驟</span><span class="sxs-lookup"><span data-stu-id="9e415-138"><a name="overview-steps"> </a> Steps required for integrating API Management and Application Gateway</span></span> 

1. <span data-ttu-id="9e415-139">建立資源管理員的資源群組。</span><span class="sxs-lookup"><span data-stu-id="9e415-139">Create a resource group for Resource Manager.</span></span>
2. <span data-ttu-id="9e415-140">建立應用程式閘道的虛擬網路、子網路和公用 IP。</span><span class="sxs-lookup"><span data-stu-id="9e415-140">Create a Virtual Network, subnet, and public IP for the Application Gateway.</span></span> <span data-ttu-id="9e415-141">為 API 管理建立其他子網路。</span><span class="sxs-lookup"><span data-stu-id="9e415-141">Create another subnet for API Management.</span></span>
3. <span data-ttu-id="9e415-142">在上面所建立的 VNET 子網路內建立 API 管理服務，並確保您使用內部模式。</span><span class="sxs-lookup"><span data-stu-id="9e415-142">Create an API Management service inside the VNET subnet created above and ensure you use the Internal mode.</span></span>
4. <span data-ttu-id="9e415-143">在 API 管理服務中設定自訂網域名稱。</span><span class="sxs-lookup"><span data-stu-id="9e415-143">Setup the custom domain name in the API Management service.</span></span>
5. <span data-ttu-id="9e415-144">建立應用程式閘道組態物件。</span><span class="sxs-lookup"><span data-stu-id="9e415-144">Create an Application Gateway configuration object.</span></span>
6. <span data-ttu-id="9e415-145">建立應用程式閘道資源。</span><span class="sxs-lookup"><span data-stu-id="9e415-145">Create an Application Gateway resource.</span></span>
7. <span data-ttu-id="9e415-146">從應用程式閘道的公用 DNS 名稱建立 CNAME 到 API 管理 Proxy 主機名稱。</span><span class="sxs-lookup"><span data-stu-id="9e415-146">Create a CNAME from the public DNS name of the Application Gateway to the API Management proxy hostname.</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="9e415-147">建立資源管理員的資源群組</span><span class="sxs-lookup"><span data-stu-id="9e415-147">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="9e415-148">確定您使用最新版本的 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="9e415-148">Make sure that you are using the latest version of Azure PowerShell.</span></span> <span data-ttu-id="9e415-149">如需詳細資訊，請參閱 [搭配使用 Windows PowerShell 與資源管理員](../powershell-azure-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="9e415-149">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="9e415-150">步驟 1</span><span class="sxs-lookup"><span data-stu-id="9e415-150">Step 1</span></span>

<span data-ttu-id="9e415-151">登入 Azure</span><span class="sxs-lookup"><span data-stu-id="9e415-151">Log in to Azure</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="9e415-152">使用您的認證進行驗證。</span><span class="sxs-lookup"><span data-stu-id="9e415-152">Authenticate with your credentials.</span></span><BR>

### <a name="step-2"></a><span data-ttu-id="9e415-153">步驟 2</span><span class="sxs-lookup"><span data-stu-id="9e415-153">Step 2</span></span>

<span data-ttu-id="9e415-154">檢查帳戶的訂用帳戶並加以選取。</span><span class="sxs-lookup"><span data-stu-id="9e415-154">Check the subscriptions for the account and select it.</span></span>

```powershell
Get-AzureRmSubscription -Subscriptionid "GUID of subscription" | Select-AzureRmSubscription
```

### <a name="step-3"></a><span data-ttu-id="9e415-155">步驟 3</span><span class="sxs-lookup"><span data-stu-id="9e415-155">Step 3</span></span>

<span data-ttu-id="9e415-156">建立資源群組 (若使用現有的資源群組，請略過此步驟)。</span><span class="sxs-lookup"><span data-stu-id="9e415-156">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name "apim-appGw-RG" -Location "West US"
```
<span data-ttu-id="9e415-157">Azure Resource Manager 需要所有的資源群組指定一個位置。</span><span class="sxs-lookup"><span data-stu-id="9e415-157">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="9e415-158">這用來作為該資源群組中資源的預設位置。</span><span class="sxs-lookup"><span data-stu-id="9e415-158">This is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="9e415-159">請確定所有用來建立應用程式閘道的命令都使用同一個資源群組。</span><span class="sxs-lookup"><span data-stu-id="9e415-159">Make sure that all commands to create an application gateway use the same resource group.</span></span>

## <a name="create-a-virtual-network-and-a-subnet-for-the-application-gateway"></a><span data-ttu-id="9e415-160">建立應用程式閘道的虛擬網路和子網路</span><span class="sxs-lookup"><span data-stu-id="9e415-160">Create a Virtual Network and a subnet for the application gateway</span></span>

<span data-ttu-id="9e415-161">下面的範例說明如何使用資源管理員建立虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="9e415-161">The following example shows how to create a Virtual Network using the resource manager.</span></span>

### <a name="step-1"></a><span data-ttu-id="9e415-162">步驟 1</span><span class="sxs-lookup"><span data-stu-id="9e415-162">Step 1</span></span>

<span data-ttu-id="9e415-163">對要在建立虛擬網路時用於應用程式閘道的子網路變數指派位址範圍 10.0.0.0/24。</span><span class="sxs-lookup"><span data-stu-id="9e415-163">Assign the address range 10.0.0.0/24 to the subnet variable to be used for Application Gateway while creating a Virtual Network.</span></span>

```powershell
$appgatewaysubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "apim01" -AddressPrefix "10.0.0.0/24"
```

### <a name="step-2"></a><span data-ttu-id="9e415-164">步驟 2</span><span class="sxs-lookup"><span data-stu-id="9e415-164">Step 2</span></span>

<span data-ttu-id="9e415-165">對要在建立虛擬網路時用於 API 管理的子網路變數指派位址範圍 10.0.1.0/24。</span><span class="sxs-lookup"><span data-stu-id="9e415-165">Assign the address range 10.0.1.0/24 to the subnet variable to be used for API Management while creating a Virtual Network.</span></span>

```powershell
$apimsubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "apim02" -AddressPrefix "10.0.1.0/24"
```

### <a name="step-3"></a><span data-ttu-id="9e415-166">步驟 3</span><span class="sxs-lookup"><span data-stu-id="9e415-166">Step 3</span></span>

<span data-ttu-id="9e415-167">使用前置詞 10.0.0.0/16 搭配子網路 10.0.0.0/24 和 10.0.1.0/24，在美國西部 (West US) 區域的 **apim-appGw-RG** 資源群組中建立名為 **appgwvnet** 的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="9e415-167">Create a Virtual Network named **appgwvnet** in resource group **apim-appGw-RG** for the West US region using the prefix 10.0.0.0/16 with subnets 10.0.0.0/24 and 10.0.1.0/24.</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name "appgwvnet" -ResourceGroupName "apim-appGw-RG" -Location "West US" -AddressPrefix "10.0.0.0/16" -Subnet $appgatewaysubnet,$apimsubnet
```

### <a name="step-4"></a><span data-ttu-id="9e415-168">步驟 4</span><span class="sxs-lookup"><span data-stu-id="9e415-168">Step 4</span></span>

<span data-ttu-id="9e415-169">指派子網路變數以供後續步驟使用</span><span class="sxs-lookup"><span data-stu-id="9e415-169">Assign a subnet variable for the next steps</span></span>

```powershell
$appgatewaysubnetdata=$vnet.Subnets[0]
$apimsubnetdata=$vnet.Subnets[1]
```
## <a name="create-an-api-management-service-inside-a-vnet-configured-in-internal-mode"></a><span data-ttu-id="9e415-170">在以內部模式設定的 VNET 內建立 API 管理服務</span><span class="sxs-lookup"><span data-stu-id="9e415-170">Create an API Management service inside a VNET configured in internal mode</span></span>

<span data-ttu-id="9e415-171">下列範例示範如何以僅針對內部存取設定的 VNET 建立 API 管理服務。</span><span class="sxs-lookup"><span data-stu-id="9e415-171">The following example shows how to create an API Management service in a VNET configured for internal access only.</span></span>

### <a name="step-1"></a><span data-ttu-id="9e415-172">步驟 1</span><span class="sxs-lookup"><span data-stu-id="9e415-172">Step 1</span></span>
<span data-ttu-id="9e415-173">使用上面所建立的子網路 $apimsubnetdata 建立 API 管理虛擬網路物件。</span><span class="sxs-lookup"><span data-stu-id="9e415-173">Create an API Management Virtual Network object using the subnet $apimsubnetdata created above.</span></span>

```powershell
$apimVirtualNetwork = New-AzureRmApiManagementVirtualNetwork -Location "West US" -SubnetResourceId $apimsubnetdata.Id
```
### <a name="step-2"></a><span data-ttu-id="9e415-174">步驟 2</span><span class="sxs-lookup"><span data-stu-id="9e415-174">Step 2</span></span>
<span data-ttu-id="9e415-175">在虛擬網路內建立 API 管理服務。</span><span class="sxs-lookup"><span data-stu-id="9e415-175">Create an API Management service inside the Virtual Network.</span></span>

```powershell
$apimService = New-AzureRmApiManagement -ResourceGroupName "apim-appGw-RG" -Location "West US" -Name "ContosoApi" -Organization "Contoso" -AdminEmail "admin@contoso.com" -VirtualNetwork $apimVirtualNetwork -VpnType "Internal" -Sku "Developer"
```
<span data-ttu-id="9e415-176">上述命令執行成功之後，請參閱[要存取內部 VNET API 管理服務所需的 DNS 組態](api-management-using-with-internal-vnet.md#apim-dns-configuration)來存取它。</span><span class="sxs-lookup"><span data-stu-id="9e415-176">After the above command succeeds refer to [DNS Configuration required to access internal VNET API Management service](api-management-using-with-internal-vnet.md#apim-dns-configuration) to access it.</span></span>

## <a name="set-up-a-custom-domain-name-in-api-management"></a><span data-ttu-id="9e415-177">在 API 管理中設定自訂網域名稱</span><span class="sxs-lookup"><span data-stu-id="9e415-177">Set-up a custom domain name in API Management</span></span>

### <a name="step-1"></a><span data-ttu-id="9e415-178">步驟 1</span><span class="sxs-lookup"><span data-stu-id="9e415-178">Step 1</span></span>
<span data-ttu-id="9e415-179">使用網域的私密金鑰上傳憑證。</span><span class="sxs-lookup"><span data-stu-id="9e415-179">Upload the certificate with private key for the domain.</span></span> <span data-ttu-id="9e415-180">這個範例中就會是 `*.contoso.net`。</span><span class="sxs-lookup"><span data-stu-id="9e415-180">For this example it will be `*.contoso.net`.</span></span> 

```powershell
$certUploadResult = Import-AzureRmApiManagementHostnameCertificate -ResourceGroupName "apim-appGw-RG" -Name "ContosoApi" -HostnameType "Proxy" -PfxPath <full path to .pfx file> -PfxPassword <password for certificate file> -PassThru
```

### <a name="step-2"></a><span data-ttu-id="9e415-181">步驟 2</span><span class="sxs-lookup"><span data-stu-id="9e415-181">Step 2</span></span>
<span data-ttu-id="9e415-182">一旦上傳憑證後，以 `api.contoso.net` 的主機名稱建立 proxy 的主機名稱組態物件，如範例憑證提供 `*.contoso.net` 網域的授權。</span><span class="sxs-lookup"><span data-stu-id="9e415-182">Once the certificate is uploaded, create a hostname configuration object for the proxy with a hostname of `api.contoso.net`, as the example certificate provides authority for the  `*.contoso.net` domain.</span></span> 

```powershell
$proxyHostnameConfig = New-AzureRmApiManagementHostnameConfiguration -CertificateThumbprint $certUploadResult.Thumbprint -Hostname "api.contoso.net"
$result = Set-AzureRmApiManagementHostnames -Name "ContosoApi" -ResourceGroupName "apim-appGw-RG" -ProxyHostnameConfiguration $proxyHostnameConfig
```

## <a name="create-a-public-ip-address-for-the-front-end-configuration"></a><span data-ttu-id="9e415-183">建立前端組態的公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="9e415-183">Create a public IP address for the front-end configuration</span></span>

<span data-ttu-id="9e415-184">在美國西部區域的 **apim-appGw-RG** 資源群組中建立公用 IP 資源 **publicIP01**。</span><span class="sxs-lookup"><span data-stu-id="9e415-184">Create a public IP resource **publicIP01** in resource group **apim-appGw-RG** for the West US region.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName "apim-appGw-RG" -name "publicIP01" -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="9e415-185">在服務啟動時，系統會將 IP 位址指派至應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="9e415-185">An IP address is assigned to the application gateway when the service starts.</span></span>

## <a name="create-application-gateway-configuration"></a><span data-ttu-id="9e415-186">建立應用程式閘道組態</span><span class="sxs-lookup"><span data-stu-id="9e415-186">Create application gateway configuration</span></span>

<span data-ttu-id="9e415-187">建立應用程式閘道之前，必須先設定所有組態項目。</span><span class="sxs-lookup"><span data-stu-id="9e415-187">All configuration items must be set up before creating the application gateway.</span></span> <span data-ttu-id="9e415-188">下列步驟會建立應用程式閘道資源所需的組態項目。</span><span class="sxs-lookup"><span data-stu-id="9e415-188">The following steps create the configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="9e415-189">步驟 1</span><span class="sxs-lookup"><span data-stu-id="9e415-189">Step 1</span></span>

<span data-ttu-id="9e415-190">建立名為 **gatewayIP01** 的應用程式閘道 IP 組態。</span><span class="sxs-lookup"><span data-stu-id="9e415-190">Create an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="9e415-191">當「應用程式閘道」啟動時，它會從已設定的子網路取得 IP 位址，再將網路流量路由傳送到後端 IP 集區中的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="9e415-191">When Application Gateway starts, it picks up an IP address from the subnet configured and route network traffic to the IP addresses in the back-end IP pool.</span></span> <span data-ttu-id="9e415-192">請記住，每個執行個體需要一個 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="9e415-192">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name "gatewayIP01" -Subnet $appgatewaysubnetdata
```

### <a name="step-2"></a><span data-ttu-id="9e415-193">步驟 2</span><span class="sxs-lookup"><span data-stu-id="9e415-193">Step 2</span></span>

<span data-ttu-id="9e415-194">設定公用 IP 端點的前端 IP 連接埠。</span><span class="sxs-lookup"><span data-stu-id="9e415-194">Configure the front-end IP port for the public IP endpoint.</span></span> <span data-ttu-id="9e415-195">此連接埠是供使用者連接到的連接埠。</span><span class="sxs-lookup"><span data-stu-id="9e415-195">This port is the port that end users connect to.</span></span>

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "port01"  -Port 443
```
### <a name="step-3"></a><span data-ttu-id="9e415-196">步驟 3</span><span class="sxs-lookup"><span data-stu-id="9e415-196">Step 3</span></span>

<span data-ttu-id="9e415-197">利用公用 IP 端點設定前端 IP。</span><span class="sxs-lookup"><span data-stu-id="9e415-197">Configure the front-end IP with public IP endpoint.</span></span>

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-4"></a><span data-ttu-id="9e415-198">步驟 4</span><span class="sxs-lookup"><span data-stu-id="9e415-198">Step 4</span></span>

<span data-ttu-id="9e415-199">設定應用程式閘道的憑證，可用來解密和重新加密流過之流量。</span><span class="sxs-lookup"><span data-stu-id="9e415-199">Configure the certificate for the Application Gateway, used to decrypt and re-encrypt the traffic passing through.</span></span>

```powershell
$cert = New-AzureRmApplicationGatewaySslCertificate -Name "cert01" -CertificateFile <full path to .pfx file> -Password <password for certificate file>
```

### <a name="step-5"></a><span data-ttu-id="9e415-200">步驟 5</span><span class="sxs-lookup"><span data-stu-id="9e415-200">Step 5</span></span>

<span data-ttu-id="9e415-201">建立應用程式閘道的 HTTP 接聽程式。</span><span class="sxs-lookup"><span data-stu-id="9e415-201">Create the HTTP listener for the Application Gateway.</span></span> <span data-ttu-id="9e415-202">指派前端 IP 組態、連接埠和 SSL 憑證給它。</span><span class="sxs-lookup"><span data-stu-id="9e415-202">Assign the front-end IP configuration, port, and ssl certificate to it.</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol "Https" -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -SslCertificate $cert
```

### <a name="step-6"></a><span data-ttu-id="9e415-203">步驟 6</span><span class="sxs-lookup"><span data-stu-id="9e415-203">Step 6</span></span>

<span data-ttu-id="9e415-204">建立 API 管理服務 `ContosoApi` Proxy 網域端點的自訂探查。</span><span class="sxs-lookup"><span data-stu-id="9e415-204">Create a custom probe to the API Management service `ContosoApi` proxy domain endpoint.</span></span> <span data-ttu-id="9e415-205">`/status-0123456789abcdef` 路徑是裝載於所有 API 管理服務上的預設健全狀況端點。</span><span class="sxs-lookup"><span data-stu-id="9e415-205">The path `/status-0123456789abcdef` is a default health endpoint hosted on all the API Management services.</span></span> <span data-ttu-id="9e415-206">將 `api.contoso.net` 設為自訂探查主機名稱，利用 SSL 憑證來保護它。</span><span class="sxs-lookup"><span data-stu-id="9e415-206">Set `api.contoso.net` as a custom probe hostname to secure it with SSL certificate.</span></span>

> [!NOTE]
> <span data-ttu-id="9e415-207">主機名稱 `contosoapi.azure-api.net` 則是名為 `contosoapi` 的服務在公用 Azure 中建立時所設定的預設 Proxy 主機名稱。</span><span class="sxs-lookup"><span data-stu-id="9e415-207">The hostname `contosoapi.azure-api.net` is the default proxy hostname configured when a service named `contosoapi` is created in public Azure.</span></span> 
> 

```powershell
$apimprobe = New-AzureRmApplicationGatewayProbeConfig -Name "apimproxyprobe" -Protocol "Https" -HostName "api.contoso.net" -Path "/status-0123456789abcdef" -Interval 30 -Timeout 120 -UnhealthyThreshold 8
```

### <a name="step-7"></a><span data-ttu-id="9e415-208">步驟 7</span><span class="sxs-lookup"><span data-stu-id="9e415-208">Step 7</span></span>

<span data-ttu-id="9e415-209">上傳要在已啟用 SSL 的後端集區資源上使用的憑證。</span><span class="sxs-lookup"><span data-stu-id="9e415-209">Upload the certificate to be used on the SSL-enabled backend pool resources.</span></span> <span data-ttu-id="9e415-210">此憑證與您在上述步驟 4 中提供的憑證相同。</span><span class="sxs-lookup"><span data-stu-id="9e415-210">This is the same certificate which you provided in Step 4 above.</span></span>

```powershell
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name "whitelistcert1" -CertificateFile <full path to .cer file>
```

### <a name="step-8"></a><span data-ttu-id="9e415-211">步驟 8</span><span class="sxs-lookup"><span data-stu-id="9e415-211">Step 8</span></span>

<span data-ttu-id="9e415-212">設定應用程式閘道的 HTTP 後端設定。</span><span class="sxs-lookup"><span data-stu-id="9e415-212">Configure HTTP backend settings for the Application Gateway.</span></span> <span data-ttu-id="9e415-213">這包括設定之後會取消的後端要求逾時限制。</span><span class="sxs-lookup"><span data-stu-id="9e415-213">This includes setting a time-out limit for backend request after which they are cancelled.</span></span> <span data-ttu-id="9e415-214">此值與探查逾時不同。</span><span class="sxs-lookup"><span data-stu-id="9e415-214">This value is different from the probe time-out.</span></span>

```powershell
$apimPoolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "apimPoolSetting" -Port 443 -Protocol "Https" -CookieBasedAffinity "Disabled" -Probe $apimprobe -AuthenticationCertificates $authcert -RequestTimeout 180
```

### <a name="step-9"></a><span data-ttu-id="9e415-215">步驟 9</span><span class="sxs-lookup"><span data-stu-id="9e415-215">Step 9</span></span>

<span data-ttu-id="9e415-216">以上面建立的 API 管理服務內部虛擬 IP 位址設定名為 **apimbackend** 的後端 IP 位址集區。</span><span class="sxs-lookup"><span data-stu-id="9e415-216">Configure a back-end IP address pool named **apimbackend**  with the internal virtual IP address of the API Management service created above.</span></span>

```powershell
$apimProxyBackendPool = New-AzureRmApplicationGatewayBackendAddressPool -Name "apimbackend" -BackendIPAddresses $apimService.StaticIPs[0]
```

### <a name="step-10"></a><span data-ttu-id="9e415-217">步驟 10</span><span class="sxs-lookup"><span data-stu-id="9e415-217">Step 10</span></span>

<span data-ttu-id="9e415-218">建立虛擬 (不存在) 後端的設定。</span><span class="sxs-lookup"><span data-stu-id="9e415-218">Create settings for a dummy (non-existent) backend.</span></span> <span data-ttu-id="9e415-219">不想要透過應用程式閘道從 API 管理公開的 API 路徑要求將會叫用這個後端，並傳回 404。</span><span class="sxs-lookup"><span data-stu-id="9e415-219">Requests to API paths that we do not want to expose from API Management via Application Gateway will hit this backend and return 404.</span></span>

<span data-ttu-id="9e415-220">設定虛擬後端的 HTTP 設定。</span><span class="sxs-lookup"><span data-stu-id="9e415-220">Configure HTTP settings for the dummy backend.</span></span>

```powershell
$dummyBackendSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "dummySetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled
```

<span data-ttu-id="9e415-221">設定虛擬後端 **dummyBackendPool**，以指向 FQDN 位址 **dummybackend.com**。這個 FQDN 位址不存在於虛擬網路中。</span><span class="sxs-lookup"><span data-stu-id="9e415-221">Configure a dummy backend **dummyBackendPool**, which points to a FQDN address **dummybackend.com**. This FQDN address does not exist in the virtual network.</span></span>

```powershell
$dummyBackendPool = New-AzureRmApplicationGatewayBackendAddressPool -Name "dummyBackendPool" -BackendFqdns "dummybackend.com"
```

<span data-ttu-id="9e415-222">建立應用程式閘道預設將使用的規則設定，以指向虛擬網路中不存在的後端 **dummybackend.com**。</span><span class="sxs-lookup"><span data-stu-id="9e415-222">Create a rule setting that the Application Gateway will use by default which points to the non-existent backend **dummybackend.com** in the Virtual Network.</span></span>

```powershell
$dummyPathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "nonexistentapis" -Paths "/*" -BackendAddressPool $dummyBackendPool -BackendHttpSettings $dummyBackendSetting
```

### <a name="step-11"></a><span data-ttu-id="9e415-223">步驟 11</span><span class="sxs-lookup"><span data-stu-id="9e415-223">Step 11</span></span>

<span data-ttu-id="9e415-224">設定後端集區的 URL 規則路徑。</span><span class="sxs-lookup"><span data-stu-id="9e415-224">Configure URL rule paths for the back-end pools.</span></span> <span data-ttu-id="9e415-225">這可以從要公開的 API 管理中只選取某些 API。</span><span class="sxs-lookup"><span data-stu-id="9e415-225">This enables selecting only some of the APIs from API Management for being exposed to the public.</span></span> <span data-ttu-id="9e415-226">例如，如果有 `Echo API` (/echo/)、`Calculator API` (/calc/) 等，則讓 `Echo API` 只能從網際網路存取。</span><span class="sxs-lookup"><span data-stu-id="9e415-226">For example, if there are `Echo API` (/echo/), `Calculator API` (/calc/) etc. make only `Echo API` accessible from Internet).</span></span> 

<span data-ttu-id="9e415-227">下列範例會為將流量路由傳送至後端「apimProxyBackendPool」的「/echo/」路徑建立簡單的規則。</span><span class="sxs-lookup"><span data-stu-id="9e415-227">The following example creates a simple rule for the "/echo/" path routing traffic to the back-end "apimProxyBackendPool".</span></span>

```powershell
$echoapiRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "externalapis" -Paths "/echo/*" -BackendAddressPool $apimProxyBackendPool -BackendHttpSettings $apimPoolSetting
```

<span data-ttu-id="9e415-228">如果路徑不符合我們想要從 API 管理啟用的路徑規則，則規則路徑對應設定也會設定名為 **dummyBackendPool** 的預設後端位址集區。</span><span class="sxs-lookup"><span data-stu-id="9e415-228">If the path doesn't match the path rules we want to enable from API Management, the rule path map configuration also configures a default back-end address pool named **dummyBackendPool**.</span></span> <span data-ttu-id="9e415-229">例如，http://api.contoso.net/calc/* 會前往 **dummyBackendPool**，因為它定義為不相符流量的預設集區。</span><span class="sxs-lookup"><span data-stu-id="9e415-229">For example, http://api.contoso.net/calc/* goes to **dummyBackendPool** as it is defined as the default pool for un-matched traffic.</span></span>

```powershell
$urlPathMap = New-AzureRmApplicationGatewayUrlPathMapConfig -Name "urlpathmap" -PathRules $echoapiRule, $dummyPathRule -DefaultBackendAddressPool $dummyBackendPool -DefaultBackendHttpSettings $dummyBackendSetting
```

<span data-ttu-id="9e415-230">上面的步驟可確保只有「"/echo"」路徑的要求可以通過應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="9e415-230">The above step ensures that only requests for the path "/echo" are allowed through the Application Gateway.</span></span> <span data-ttu-id="9e415-231">對 API 管理中所設定之其他 API 的要求，則會在從網際網路存取時，從應用程式閘道擲回 404 錯誤。</span><span class="sxs-lookup"><span data-stu-id="9e415-231">Requests to other APIs configured in API Management will throw 404 errors from Application Gateway when accessed from the Internet.</span></span> 

### <a name="step-12"></a><span data-ttu-id="9e415-232">步驟 12</span><span class="sxs-lookup"><span data-stu-id="9e415-232">Step 12</span></span>

<span data-ttu-id="9e415-233">建立規則設定以供應用程式閘道使用 URL 路徑型路由。</span><span class="sxs-lookup"><span data-stu-id="9e415-233">Create a rule setting for the Application Gateway to use URL path-based routing.</span></span>

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule1" -RuleType PathBasedRouting -HttpListener $listener -UrlPathMap $urlPathMap
```

### <a name="step-13"></a><span data-ttu-id="9e415-234">步驟 13</span><span class="sxs-lookup"><span data-stu-id="9e415-234">Step 13</span></span>

<span data-ttu-id="9e415-235">設定執行個體數目和應用程式閘道的大小。</span><span class="sxs-lookup"><span data-stu-id="9e415-235">Configure the number of instances and size for the Application Gateway.</span></span> <span data-ttu-id="9e415-236">在這裡，我們使用 [WAF SKU](../application-gateway/application-gateway-webapplicationfirewall-overview.md) 以提高 API 管理資源的安全性。</span><span class="sxs-lookup"><span data-stu-id="9e415-236">Here we are using the [WAF SKU](../application-gateway/application-gateway-webapplicationfirewall-overview.md) for increased security of the API Management resource.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "WAF_Medium" -Tier "WAF" -Capacity 2
```

### <a name="step-14"></a><span data-ttu-id="9e415-237">步驟 14</span><span class="sxs-lookup"><span data-stu-id="9e415-237">Step 14</span></span>

<span data-ttu-id="9e415-238">將 WAF 設定為「防止」模式。</span><span class="sxs-lookup"><span data-stu-id="9e415-238">Configure WAF to be in "Prevention" mode.</span></span>
```powershell
$config = New-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode "Prevention"
```

## <a name="create-application-gateway"></a><span data-ttu-id="9e415-239">建立應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="9e415-239">Create Application Gateway</span></span>

<span data-ttu-id="9e415-240">利用上述步驟中的所有組態物件來建立應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="9e415-240">Create an Application Gateway with all the configuration objects from the preceding steps.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name $applicationGatewayName -ResourceGroupName $resourceGroupName  -Location $location -BackendAddressPools $apimProxyBackendPool, $dummyBackendPool -BackendHttpSettingsCollection $apimPoolSetting, $dummyBackendSetting  -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener -UrlPathMaps $urlPathMap -RequestRoutingRules $rule01 -Sku $sku -WebApplicationFirewallConfig $config -SslCertificates $cert -AuthenticationCertificates $authcert -Probes $apimprobe
```

## <a name="cname-the-api-management-proxy-hostname-to-the-public-dns-name-of-the-application-gateway-resource"></a><span data-ttu-id="9e415-241">將 API 管理 Proxy 主機名稱 CNAME 到應用程式閘道資源的公用 DNS 名稱</span><span class="sxs-lookup"><span data-stu-id="9e415-241">CNAME the API Management proxy hostname to the public DNS name of the Application Gateway resource</span></span>

<span data-ttu-id="9e415-242">建立閘道之後，下一步是設定通訊的前端。</span><span class="sxs-lookup"><span data-stu-id="9e415-242">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="9e415-243">當使用公用 IP 時，應用程式閘道需要動態指派的 DNS 名稱 (可能不易記住)。</span><span class="sxs-lookup"><span data-stu-id="9e415-243">When using a public IP, Application Gateway requires a dynamically assigned DNS name, which may not be easy to use.</span></span> 

<span data-ttu-id="9e415-244">您應該使用應用程式閘道的 DNS 名稱來建立 CNAME 記錄，將 APIM Proxy 主機名稱 (例如，上面範例中的 `api.contoso.net`) 指向此 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="9e415-244">The Application Gateway's DNS name should be used to create a CNAME record which points the APIM proxy host name (e.g. `api.contoso.net` in the examples above) to this DNS name.</span></span> <span data-ttu-id="9e415-245">若要設定前端 IP CNAME 記錄，使用 PublicIPAddress 元素，擷取應用程式閘道的詳細資料及其關聯的 IP/DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="9e415-245">To configure the frontend IP CNAME record, retrieve the details of the Application Gateway and its associated IP/DNS name using the PublicIPAddress element.</span></span> <span data-ttu-id="9e415-246">不建議使用 A-records，因為重新啟動閘道時，VIP 可能會變更。</span><span class="sxs-lookup"><span data-stu-id="9e415-246">The use of A-records is not recommended since the VIP may change on restart of gateway.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName "apim-appGw-RG" -Name "publicIP01"
```

##<span data-ttu-id="9e415-247"><a name="summary"></a>摘要</span><span class="sxs-lookup"><span data-stu-id="9e415-247"><a name="summary"> </a> Summary</span></span>
<span data-ttu-id="9e415-248">VNET 中設定的 Azure API 針對所有管理的 API 管理提供了單一閘道介面，不論它們是裝載在內部部署環境或雲端中。</span><span class="sxs-lookup"><span data-stu-id="9e415-248">Azure API Management configured in a VNET provides a single gateway interface for all configured APIs, whether they are hosted on-prem or in the cloud.</span></span> <span data-ttu-id="9e415-249">整合應用程式閘道與 API 管理提供選擇性地使特定 API 可在網際網路上存取的彈性，並提供 Web 應用程式防火牆來做為 API 管理執行個體的前端。</span><span class="sxs-lookup"><span data-stu-id="9e415-249">Integrating Application Gateway with API Management provides the flexibility of selectively enabling particular APIs to be accessible on the Internet, as well as providing a Web Application Firewall as a frontend to your API Management instance.</span></span>

##<span data-ttu-id="9e415-250"><a name="next-steps"></a>後續步驟</span><span class="sxs-lookup"><span data-stu-id="9e415-250"><a name="next-steps"> </a> Next steps</span></span>
* <span data-ttu-id="9e415-251">深入了解 Azure 應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="9e415-251">Learn more about Azure Application Gateway</span></span>
  * [<span data-ttu-id="9e415-252">應用程式閘道概觀</span><span class="sxs-lookup"><span data-stu-id="9e415-252">Application Gateway Overview</span></span>](../application-gateway/application-gateway-introduction.md)
  * [<span data-ttu-id="9e415-253">應用程式閘道 Web 應用程式防火牆</span><span class="sxs-lookup"><span data-stu-id="9e415-253">Application Gateway Web Application Firewall</span></span>](../application-gateway/application-gateway-webapplicationfirewall-overview.md)
  * [<span data-ttu-id="9e415-254">使用路徑型路由的應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="9e415-254">Application Gateway using Path-based Routing</span></span>](../application-gateway/application-gateway-create-url-route-arm-ps.md)
* <span data-ttu-id="9e415-255">深入了解 API 管理和 VNET</span><span class="sxs-lookup"><span data-stu-id="9e415-255">Learn more about API Management and VNETs</span></span>
  * [<span data-ttu-id="9e415-256">使用只在 VNET 內提供的 API 管理</span><span class="sxs-lookup"><span data-stu-id="9e415-256">Using API Management available only within the VNET</span></span>](api-management-using-with-internal-vnet.md)
  * [<span data-ttu-id="9e415-257">在 VNET 中使用 API 管理</span><span class="sxs-lookup"><span data-stu-id="9e415-257">Using API Management in VNET</span></span>](api-management-using-with-vnet.md)
