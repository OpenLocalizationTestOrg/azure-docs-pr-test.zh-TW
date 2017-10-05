---
title: "建立應用程式閘道來裝載多個站台 | Microsoft Docs"
description: "本頁面提供建立和設定 Azure 應用程式閘道以在相同閘道上裝載多個 Web 應用程式的指示。"
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: amsriva
ms.assetid: b107d647-c9be-499f-8b55-809c4310c783
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/12/2016
ms.author: amsriva
ms.openlocfilehash: d42efa7d359f5c87c14afbfd138328b37c8ae6c2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-application-gateway-for-hosting-multiple-web-applications"></a><span data-ttu-id="f2ae2-103">建立應用程式閘道來裝載多個 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="f2ae2-103">Create an application gateway for hosting multiple web applications</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f2ae2-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="f2ae2-104">Azure portal</span></span>](application-gateway-create-multisite-portal.md)
> * [<span data-ttu-id="f2ae2-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="f2ae2-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-multisite-azureresourcemanager-powershell.md)

<span data-ttu-id="f2ae2-106">多站台裝載可讓您在相同的應用程式閘道上部署多個 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-106">Multiple site hosting allows you to deploy more than one web application on the same application gateway.</span></span> <span data-ttu-id="f2ae2-107">它需倚賴在連入的 HTTP 要求中有主機標頭存在，以判斷哪一個接聽程式要接收流量。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-107">It relies on presence of host header in the incoming HTTP request, to determine which listener would receive traffic.</span></span> <span data-ttu-id="f2ae2-108">然後再由接聽程式將流量導向閘道的規則定義中所設定的適當後端集區。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-108">The listener then directs traffic to appropriate backend pool as configured in the rules definition of the gateway.</span></span> <span data-ttu-id="f2ae2-109">在已啟用 SSL 功能的 Web 應用程式中，則應用程式閘道會依賴「伺服器名稱指示」(SNI) 擴充功能來選擇正確的 Web 流量接聽程式。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-109">In SSL enabled web applications, application gateway relies on the Server Name Indication (SNI) extension to choose the correct listener for the web traffic.</span></span> <span data-ttu-id="f2ae2-110">多站台裝載的常見用法是將不同 Web 網域的要求負載平衡至不同的後端伺服器集區。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-110">A common use for multiple site hosting is to load balance requests for different web domains to different back-end server pools.</span></span> <span data-ttu-id="f2ae2-111">同樣地，相同根網域的多個子網域也可以裝載在相同的應用程式閘道上。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-111">Similarly multiple subdomains of the same root domain could also be hosted on the same application gateway.</span></span>

## <a name="scenario"></a><span data-ttu-id="f2ae2-112">案例</span><span class="sxs-lookup"><span data-stu-id="f2ae2-112">Scenario</span></span>

<span data-ttu-id="f2ae2-113">在下列範例中，應用程式閘道會利用兩個後端伺服器集區來為 contoso.com 和 fabrikam.com 的流量提供服務：contoso 伺服器集區和 fabrikam 伺服器集區。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-113">In the following example, application gateway is serving traffic for contoso.com and fabrikam.com with two back-end server pools: contoso server pool and fabrikam server pool.</span></span> <span data-ttu-id="f2ae2-114">類似的設定也可用來裝載子網域，例如 app.contoso.com 和 blog.contoso.com。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-114">Similar setup could be used to host subdomains like app.contoso.com and blog.contoso.com.</span></span>

![imageURLroute](./media/application-gateway-create-multisite-azureresourcemanager-powershell/multisite.png)

## <a name="before-you-begin"></a><span data-ttu-id="f2ae2-116">開始之前</span><span class="sxs-lookup"><span data-stu-id="f2ae2-116">Before you begin</span></span>

1. <span data-ttu-id="f2ae2-117">使用 Web Platform Installer 安裝最新版的 Azure PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-117">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span></span> <span data-ttu-id="f2ae2-118">您可以從 **下載頁面** 的 [Windows PowerShell](https://azure.microsoft.com/downloads/)區段下載並安裝最新版本。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-118">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="f2ae2-119">新增至後端集區以使用應用程式閘道的伺服器必須存在，或是在虛擬網路的個別子網路中建立其端點，或是已指派公用 IP/VIP。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-119">The servers added to the back-end pool to use the application gateway must exist or have their endpoints created either in the virtual network in a separate subnet or with a public IP/VIP assigned.</span></span>

## <a name="requirements"></a><span data-ttu-id="f2ae2-120">需求</span><span class="sxs-lookup"><span data-stu-id="f2ae2-120">Requirements</span></span>

* <span data-ttu-id="f2ae2-121">**後端伺服器集區：** 後端伺服器的 IP 位址清單。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-121">**Back-end server pool:** The list of IP addresses of the back-end servers.</span></span> <span data-ttu-id="f2ae2-122">列出的 IP 位址應屬於虛擬網路子網路或是公用 IP/VIP。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-122">The IP addresses listed should either belong to the virtual network subnet or should be a public IP/VIP.</span></span> <span data-ttu-id="f2ae2-123">您也可以使用 FQDN。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-123">FQDN can also be used.</span></span>
* <span data-ttu-id="f2ae2-124">**後端伺服器集區設定：** 每個集區都包括一些設定，例如連接埠、通訊協定和以 Cookie 為基礎的同質性。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-124">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="f2ae2-125">這些設定會繫結至集區，並套用至集區內所有伺服器。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-125">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="f2ae2-126">**前端連接埠：** 此連接埠是在應用程式閘道上開啟的公用連接埠。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-126">**Front-end port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="f2ae2-127">流量會到達此連接埠，然後重新導向至其中一個後端伺服器。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-127">Traffic hits this port, and then gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="f2ae2-128">**接聽程式：** 接聽程式具有前端連接埠、通訊協定 (Http 或 Https，這些值都區分大小寫) 和 SSL 憑證名稱 (如果已設定 SSL 卸載)。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-128">**Listener:** The listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span> <span data-ttu-id="f2ae2-129">針對啟用多站台功能的應用程式閘道，會一併新增主機名稱和 SNI 指示器。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-129">For multi-site enabled application gateways, host name and SNI indicators are also added.</span></span>
* <span data-ttu-id="f2ae2-130">**規則：**規則會繫結接聽程式和後端伺服器集區，並定義流量達到特定接聽程式時應該導向至哪個後端伺服器集區。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-130">**Rule:** The rule binds the listener, the back-end server pool, and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span></span> <span data-ttu-id="f2ae2-131">會以規則列出的順序進行處理，且不論精確性，都會透過相符的第一個規則將流量進行導向。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-131">Rules are processed in the order they are listed, and traffic will be directed via the first rule that matches regardless of specificity.</span></span> <span data-ttu-id="f2ae2-132">例如，如果您在相同的連接埠上同時使用基本接聽程式的規則和多站台接聽程式的規則，則必須將多站台接聽程式的規則列於基本接聽程式的規則之前，多站台規則才能如預期般運作。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-132">For example, if you have a rule using a basic listener and a rule using a multi-site listener both on the same port, the rule with the multi-site listener must be listed before the rule with the basic listener in order for the multi-site rule to function as expected.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="f2ae2-133">建立應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="f2ae2-133">Create an application gateway</span></span>

<span data-ttu-id="f2ae2-134">以下是建立應用程式閘道所需的步驟：</span><span class="sxs-lookup"><span data-stu-id="f2ae2-134">The following are the steps needed to create an application gateway:</span></span>

1. <span data-ttu-id="f2ae2-135">建立資源管理員的資源群組。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-135">Create a resource group for Resource Manager.</span></span>
2. <span data-ttu-id="f2ae2-136">建立應用程式閘道的虛擬網路、子網路和公用 IP。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-136">Create a virtual network, subnets, and public IP for the application gateway.</span></span>
3. <span data-ttu-id="f2ae2-137">建立應用程式閘道組態物件。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-137">Create an application gateway configuration object.</span></span>
4. <span data-ttu-id="f2ae2-138">建立應用程式閘道資源。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-138">Create an application gateway resource.</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="f2ae2-139">建立資源管理員的資源群組</span><span class="sxs-lookup"><span data-stu-id="f2ae2-139">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="f2ae2-140">確定您使用最新版本的 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-140">Make sure that you are using the latest version of Azure PowerShell.</span></span> <span data-ttu-id="f2ae2-141">如需詳細資訊，可在[搭配使用 Windows PowerShell 與 Resource Manager](../powershell-azure-resource-manager.md) 取得。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-141">More information is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="f2ae2-142">步驟 1</span><span class="sxs-lookup"><span data-stu-id="f2ae2-142">Step 1</span></span>

<span data-ttu-id="f2ae2-143">登入 Azure</span><span class="sxs-lookup"><span data-stu-id="f2ae2-143">Log in to Azure</span></span>

```powershell
Login-AzureRmAccount
```
<span data-ttu-id="f2ae2-144">系統會提示使用您的認證進行驗證。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-144">You are prompted to authenticate with your credentials.</span></span>

### <a name="step-2"></a><span data-ttu-id="f2ae2-145">步驟 2</span><span class="sxs-lookup"><span data-stu-id="f2ae2-145">Step 2</span></span>

<span data-ttu-id="f2ae2-146">檢查帳戶的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-146">Check the subscriptions for the account.</span></span>

```powershell
Get-AzureRmSubscription
```

### <a name="step-3"></a><span data-ttu-id="f2ae2-147">步驟 3</span><span class="sxs-lookup"><span data-stu-id="f2ae2-147">Step 3</span></span>

<span data-ttu-id="f2ae2-148">選擇要使用哪一個 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-148">Choose which of your Azure subscriptions to use.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="f2ae2-149">步驟 4</span><span class="sxs-lookup"><span data-stu-id="f2ae2-149">Step 4</span></span>

<span data-ttu-id="f2ae2-150">建立資源群組 (若使用現有的資源群組，請略過此步驟)。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-150">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-RG -location "West US"
```

<span data-ttu-id="f2ae2-151">或者，您也可以針對應用程式閘道建立資源群組的標記：</span><span class="sxs-lookup"><span data-stu-id="f2ae2-151">Alternatively you can also create tags for a resource group for application gateway:</span></span>

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US" -Tags @{Name = "testtag"; Value = "Application Gateway multiple site"}
```

<span data-ttu-id="f2ae2-152">Azure Resource Manager 需要所有的資源群組指定一個位置。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-152">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="f2ae2-153">此位置用來作為該資源群組中資源的預設位置。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-153">This location is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="f2ae2-154">請確定所有用來建立應用程式閘道的命令都使用同一個資源群組。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-154">Make sure that all commands to create an application gateway use the same resource group.</span></span>

<span data-ttu-id="f2ae2-155">在上述範例中，我們建立名為 **appgw-RG** 的資源群組，且位置為美國西部 (**West US**)。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-155">In the example above, we created a resource group called **appgw-RG** with a location of **West US**.</span></span>

> [!NOTE]
> <span data-ttu-id="f2ae2-156">如果您需要設定應用程式閘道的自訂探查，請參閱 [使用 PowerShell 建立具有自訂探查的應用程式閘道](application-gateway-create-probe-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-156">If you need to configure a custom probe for your application gateway, see [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md).</span></span> <span data-ttu-id="f2ae2-157">請造訪[自訂探查和健全狀況監視](application-gateway-probe-overview.md)以取得詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-157">Visit [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>

## <a name="create-a-virtual-network-and-subnets"></a><span data-ttu-id="f2ae2-158">建立虛擬網路和子網路</span><span class="sxs-lookup"><span data-stu-id="f2ae2-158">Create a virtual network and subnets</span></span>

<span data-ttu-id="f2ae2-159">下面的範例說明如何使用資源管理員建立虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-159">The following example shows how to create a virtual network by using Resource Manager.</span></span> <span data-ttu-id="f2ae2-160">此步驟中會建立兩個子網路。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-160">Two subnets are created in this step.</span></span> <span data-ttu-id="f2ae2-161">第一個子網路用於應用程式閘道本身。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-161">The first subnet is for the application gateway itself.</span></span> <span data-ttu-id="f2ae2-162">應用程式閘道需要自己的子網路來保存其執行個體。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-162">Application gateway requires its own subnet to hold its instances.</span></span> <span data-ttu-id="f2ae2-163">在該子網路中只能部署其他應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-163">Only other application gateways can be deployed in that subnet.</span></span> <span data-ttu-id="f2ae2-164">第二個子網路用來保存應用程式後端伺服器。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-164">The second subnet is used to hold the application backend servers.</span></span>

### <a name="step-1"></a><span data-ttu-id="f2ae2-165">步驟 1</span><span class="sxs-lookup"><span data-stu-id="f2ae2-165">Step 1</span></span>

<span data-ttu-id="f2ae2-166">指派用於保存應用程式閘道的位址範圍 10.0.0.0/24 給子網路變數。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-166">Assign the address range 10.0.0.0/24 to the subnet variable to be used to hold the application gateway.</span></span>

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name appgatewaysubnet -AddressPrefix 10.0.0.0/24
```
### <a name="step-2"></a><span data-ttu-id="f2ae2-167">步驟 2</span><span class="sxs-lookup"><span data-stu-id="f2ae2-167">Step 2</span></span>

<span data-ttu-id="f2ae2-168">指派用於後端集區的位址範圍 10.0.1.0/24 給子網路 2 變數。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-168">Assign the address range 10.0.1.0/24 to the subnet2 variable to be used for the backend pools.</span></span>

```powershell
$subnet2 = New-AzureRmVirtualNetworkSubnetConfig -Name backendsubnet -AddressPrefix 10.0.1.0/24
```

### <a name="step-3"></a><span data-ttu-id="f2ae2-169">步驟 3</span><span class="sxs-lookup"><span data-stu-id="f2ae2-169">Step 3</span></span>

<span data-ttu-id="f2ae2-170">使用前置詞 10.0.0.0/16 搭配子網路 10.0.0.0/24 和 10.0.1.0/24，在美國西部 (West US) 區域的 **appgw-rg** 資源群組中建立名為 **appgwvnet** 的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-170">Create a virtual network named **appgwvnet** in resource group **appgw-rg** for the West US region using the prefix 10.0.0.0/16 with subnet 10.0.0.0/24, and 10.0.1.0/24.</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet,$subnet2
```

### <a name="step-4"></a><span data-ttu-id="f2ae2-171">步驟 4</span><span class="sxs-lookup"><span data-stu-id="f2ae2-171">Step 4</span></span>

<span data-ttu-id="f2ae2-172">針對建立應用程式閘道的後續步驟，指派子網路變數。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-172">Assign a subnet variable for the next steps, which creates an application gateway.</span></span>

```powershell
$appgatewaysubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name appgatewaysubnet -VirtualNetwork $vnet
$backendsubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name backendsubnet -VirtualNetwork $vnet
```

## <a name="create-a-public-ip-address-for-the-front-end-configuration"></a><span data-ttu-id="f2ae2-173">建立前端組態的公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="f2ae2-173">Create a public IP address for the front-end configuration</span></span>

<span data-ttu-id="f2ae2-174">在美國西部區域的 **appgw-rg** 資源群組中建立公用 IP 資源 **publicIP01**。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-174">Create a public IP resource **publicIP01** in resource group **appgw-rg** for the West US region.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="f2ae2-175">在服務啟動時，系統會將 IP 位址指派至應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-175">An IP address is assigned to the application gateway when the service starts.</span></span>

## <a name="create-application-gateway-configuration"></a><span data-ttu-id="f2ae2-176">建立應用程式閘道組態</span><span class="sxs-lookup"><span data-stu-id="f2ae2-176">Create application gateway configuration</span></span>

<span data-ttu-id="f2ae2-177">您必須先設定所有組態項目，再建立應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-177">You have to set up all configuration items before creating the application gateway.</span></span> <span data-ttu-id="f2ae2-178">下列步驟會建立應用程式閘道資源所需的組態項目。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-178">The following steps create the configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="f2ae2-179">步驟 1</span><span class="sxs-lookup"><span data-stu-id="f2ae2-179">Step 1</span></span>

<span data-ttu-id="f2ae2-180">建立名為 **gatewayIP01** 的應用程式閘道 IP 組態。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-180">Create an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="f2ae2-181">當應用程式閘道啟動時，它會從已設定的子網路取得 IP 位址，再將網路流量路由傳送到後端 IP 集區中的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-181">When application gateway starts, it picks up an IP address from the subnet configured and route network traffic to the IP addresses in the back-end IP pool.</span></span> <span data-ttu-id="f2ae2-182">請記住，每個執行個體需要一個 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-182">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $appgatewaysubnet
```

### <a name="step-2"></a><span data-ttu-id="f2ae2-183">步驟 2</span><span class="sxs-lookup"><span data-stu-id="f2ae2-183">Step 2</span></span>

<span data-ttu-id="f2ae2-184">設定名為 **pool01** 和 **pool2** 的後端 IP 位址集區，**pool1** 的 IP 位址為 **134.170.185.46**、**134.170.188.221**、**134.170.185.50**，而 **pool2** 的 IP 位址為 **134.170.186.46**、**134.170.189.221**、**134.170.186.50**。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-184">Configure the back-end IP address pool named **pool01** and **pool2** with IP addresses **134.170.185.46**, **134.170.188.221**, **134.170.185.50** for **pool1** and **134.170.186.46**, **134.170.189.221**, **134.170.186.50** for **pool2**.</span></span>

```powershell
$pool1 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 10.0.1.100, 10.0.1.101, 10.0.1.102
$pool2 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool02 -BackendIPAddresses 10.0.1.103, 10.0.1.104, 10.0.1.105
```

<span data-ttu-id="f2ae2-185">此範例中有兩個後端集區，根據要求的網站路由傳送網路流量。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-185">In this example, there are two back-end pools to route network traffic based on the requested site.</span></span> <span data-ttu-id="f2ae2-186">其中一個集區會接收來自 "contoso.com" 站台的流量，而另一個集區則會接收來自 "fabrikam.com" 站台的流量。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-186">One pool receives traffic from site "contoso.com" and other pool receives traffic from site "fabrikam.com".</span></span> <span data-ttu-id="f2ae2-187">您必須取代上述 IP 位址來新增自己的應用程式 IP 位址端點。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-187">You have to replace the preceding IP addresses to add your own application IP address endpoints.</span></span> <span data-ttu-id="f2ae2-188">您也可以使用公用 IP 位址、FQDN 或 VM 的後端執行個體 NIC 來取代內部 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-188">In place of internal IP addresses, you could also use public IP addresses, FQDN, or a VM's NIC for backend instances.</span></span> <span data-ttu-id="f2ae2-189">若要在 PowerShell 中指定 FQDN (而不是 IP)，請使用 "-BackendFQDNs" 參數。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-189">To specify FQDNs instead of IPs in PowerShell use "-BackendFQDNs" parameter.</span></span>

### <a name="step-3"></a><span data-ttu-id="f2ae2-190">步驟 3</span><span class="sxs-lookup"><span data-stu-id="f2ae2-190">Step 3</span></span>

<span data-ttu-id="f2ae2-191">針對後端集區中負載平衡的網路流量，設定應用程式閘道設定 **poolsetting01** 和 **poolsetting02**。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-191">Configure application gateway setting **poolsetting01** and **poolsetting02** for the load-balanced network traffic in the back-end pool.</span></span> <span data-ttu-id="f2ae2-192">在此範例中，您會針對後端集區設定不同的後端集區設定。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-192">In this example, you configure different back-end pool settings for the back-end pools.</span></span> <span data-ttu-id="f2ae2-193">每個後端集區都可以有它自己的後端集區設定。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-193">Each back-end pool can have its own back-end pool setting.</span></span>

```powershell
$poolSetting01 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120
$poolSetting02 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting02" -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 240
```

### <a name="step-4"></a><span data-ttu-id="f2ae2-194">步驟 4</span><span class="sxs-lookup"><span data-stu-id="f2ae2-194">Step 4</span></span>

<span data-ttu-id="f2ae2-195">利用公用 IP 端點設定前端 IP。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-195">Configure the front-end IP with public IP endpoint.</span></span>

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-5"></a><span data-ttu-id="f2ae2-196">步驟 5</span><span class="sxs-lookup"><span data-stu-id="f2ae2-196">Step 5</span></span>

<span data-ttu-id="f2ae2-197">設定應用程式閘道的前端連接埠。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-197">Configure the front-end port for an application gateway.</span></span>

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "fep01" -Port 443
```

### <a name="step-6"></a><span data-ttu-id="f2ae2-198">步驟 6</span><span class="sxs-lookup"><span data-stu-id="f2ae2-198">Step 6</span></span>

<span data-ttu-id="f2ae2-199">為我們將在此範例中支援的兩個網站設定兩個 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-199">Configure two SSL certificates for the two websites we are going to support in this example.</span></span> <span data-ttu-id="f2ae2-200">一個憑證用於 contoso.com 流量，另一個則用於 fabrikam.com 流量。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-200">One certificate is for contoso.com traffic and the other is for fabrikam.com traffic.</span></span> <span data-ttu-id="f2ae2-201">這些憑證應該是「憑證授權單位」為您的網站簽發的憑證。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-201">These certificates should be a Certificate Authority issued certificates for your websites.</span></span> <span data-ttu-id="f2ae2-202">也支援自我簽署憑證，但不建議用於生產環境流量。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-202">Self-signed certificates are supported but not recommended for production traffic.</span></span>

```powershell
$cert01 = New-AzureRmApplicationGatewaySslCertificate -Name contosocert -CertificateFile <file path> -Password <password>
$cert02 = New-AzureRmApplicationGatewaySslCertificate -Name fabrikamcert -CertificateFile <file path> -Password <password>
```

### <a name="step-7"></a><span data-ttu-id="f2ae2-203">步驟 7</span><span class="sxs-lookup"><span data-stu-id="f2ae2-203">Step 7</span></span>

<span data-ttu-id="f2ae2-204">為此範例中的兩個網站設定兩個接聽程式。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-204">Configure two listeners for the two web sites in this example.</span></span> <span data-ttu-id="f2ae2-205">此步驟會針對用來接收連入流量的公用 IP 位址、連接埠及主機設定接聽程式。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-205">This step configures the listeners for public IP address, port, and host used to receive incoming traffic.</span></span> <span data-ttu-id="f2ae2-206">若要獲得多站台支援，必須要有 HostName 參數，並且應該設定為接收其流量的適當網站。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-206">HostName parameter is required for multiple site support and should be set to the appropriate website for which the traffic is received.</span></span> <span data-ttu-id="f2ae2-207">針對在多主機案例中需要 SSL 支援的網站，RequireServerNameIndication 參數應該設定為 true。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-207">RequireServerNameIndication parameter should be set to true for websites that need support for SSL in a multiple host scenario.</span></span> <span data-ttu-id="f2ae2-208">如果需要 SSL 支援，則您也必須指定用來保護該 Web 應用程式流量的 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-208">If SSL support is required, you also need to specify the SSL certificate that is used to secure traffic for that web application.</span></span> <span data-ttu-id="f2ae2-209">FrontendIPConfiguration、FrontendPort 及 HostName 的組合對接聽程式而言必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-209">The combination of FrontendIPConfiguration, FrontendPort, and HostName must be unique to a listener.</span></span> <span data-ttu-id="f2ae2-210">每個接聽程式可以支援一個憑證。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-210">Each listener can support one certificate.</span></span>

```powershell
$listener01 = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol Https -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -HostName "contoso11.com" -RequireServerNameIndication true  -SslCertificate $cert01
$listener02 = New-AzureRmApplicationGatewayHttpListener -Name "listener02" -Protocol Https -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -HostName "fabrikam11.com" -RequireServerNameIndication true -SslCertificate $cert02
```

### <a name="step-8"></a><span data-ttu-id="f2ae2-211">步驟 8</span><span class="sxs-lookup"><span data-stu-id="f2ae2-211">Step 8</span></span>

<span data-ttu-id="f2ae2-212">為此範例中的兩個 Web 應用程式建立兩個規則設定。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-212">Create two rule setting for the two web applications in this example.</span></span> <span data-ttu-id="f2ae2-213">規則會將接聽程式、後端集區及 http 設定繫結在一起。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-213">A rule ties together listeners, backend pools and http settings.</span></span> <span data-ttu-id="f2ae2-214">此步驟會設定讓應用程式閘道使用基本路由規則 (每個網站一個規則)。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-214">This step configures the application gateway to use Basic routing rule, one for each website.</span></span> <span data-ttu-id="f2ae2-215">每個網站的流量都會由其已設定的接聽程式接收，然後再使用 BackendHttpSettings 中指定的屬性來導向到其已設定的後端集區中。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-215">Traffic to each website is received by its configured listener, and is then directed to its configured backend pool, using the properties specified in the BackendHttpSettings.</span></span>

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule01" -RuleType Basic -HttpListener $listener01 -BackendHttpSettings $poolSetting01 -BackendAddressPool $pool1
$rule02 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule02" -RuleType Basic -HttpListener $listener02 -BackendHttpSettings $poolSetting02 -BackendAddressPool $pool2
```

### <a name="step-9"></a><span data-ttu-id="f2ae2-216">步驟 9</span><span class="sxs-lookup"><span data-stu-id="f2ae2-216">Step 9</span></span>

<span data-ttu-id="f2ae2-217">設定執行個體數目和應用程式閘道的大小。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-217">Configure the number of instances and size for the application gateway.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "Standard_Medium" -Tier Standard -Capacity 2
```

## <a name="create-application-gateway"></a><span data-ttu-id="f2ae2-218">建立應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="f2ae2-218">Create application gateway</span></span>

<span data-ttu-id="f2ae2-219">利用上述步驟中的所有組態物件來建立應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-219">Create an application gateway with all configuration objects from the preceding steps.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-RG -Location "West US" -BackendAddressPools $pool1,$pool2 -BackendHttpSettingsCollection $poolSetting01, $poolSetting02 -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener01, $listener02 -RequestRoutingRules $rule01, $rule02 -Sku $sku -SslCertificates $cert01, $cert02
```

> [!IMPORTANT]
> <span data-ttu-id="f2ae2-220">「應用程式閘道」佈建是一個長時間執行的作業，可能需要一些時間才能完成。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-220">Application Gateway provisioning is a long running operation and may take some time to complete.</span></span>
> 
> 

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="f2ae2-221">取得應用程式閘道 DNS 名稱</span><span class="sxs-lookup"><span data-stu-id="f2ae2-221">Get application gateway DNS name</span></span>

<span data-ttu-id="f2ae2-222">建立閘道之後，下一步是設定通訊的前端。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-222">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="f2ae2-223">當使用公用 IP 時，應用程式閘道需要動態指派的 DNS 名稱 (不易記住)。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-223">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="f2ae2-224">為了確保使用者可以叫用應用程式閘道，可使用 CNAME 記錄來指向應用程式閘道的公用端點。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-224">To ensure end users can hit the application gateway, a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="f2ae2-225">[在 Azure 中設定自訂網域名稱](../cloud-services/cloud-services-custom-domain-name-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-225">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="f2ae2-226">做法是使用連接至應用程式閘道的 PublicIPAddress 元素，擷取應用程式閘道的詳細資料及其關聯的 IP/DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-226">To do this, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="f2ae2-227">應用程式閘道的 DNS 名稱應該用來建立將兩個 Web 應用程式指向此 DNS 名稱的 CNAME 記錄。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-227">The application gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span></span> <span data-ttu-id="f2ae2-228">不建議使用 A-records，因為重新啟動應用程式閘道時，VIP 可能會變更。</span><span class="sxs-lookup"><span data-stu-id="f2ae2-228">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="f2ae2-229">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f2ae2-229">Next steps</span></span>

<span data-ttu-id="f2ae2-230">了解如何使用[應用程式閘道 - Web 應用程式防火牆](application-gateway-webapplicationfirewall-overview.md)保護您的網站</span><span class="sxs-lookup"><span data-stu-id="f2ae2-230">Learn how to protect your websites with [Application Gateway - Web Application Firewall](application-gateway-webapplicationfirewall-overview.md)</span></span>

