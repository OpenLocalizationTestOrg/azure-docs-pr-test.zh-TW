---
title: "使用 URL 路由規則建立應用程式閘道 |Microsoft Docs"
description: "本頁面提供使用 URL 路由規則建立和設定 Azure 應用程式閘道的指示。"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: d141cfbb-320a-4fc9-9125-10001c6fa4cf
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/03/2017
ms.author: gwallace
ms.openlocfilehash: ba756d3262b9780c5701e69faad860ba32bba08b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-application-gateway-using-path-based-routing"></a><span data-ttu-id="d4980-103">使用路徑型路由建立應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="d4980-103">Create an application gateway using Path-based routing</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="d4980-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="d4980-104">Azure portal</span></span>](application-gateway-create-url-route-portal.md)
> * [<span data-ttu-id="d4980-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="d4980-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-url-route-arm-ps.md)
> * [<span data-ttu-id="d4980-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="d4980-106">Azure CLI 2.0</span></span>](application-gateway-create-url-route-cli.md)

<span data-ttu-id="d4980-107">以 URL 路徑為基礎的路由可讓您根據 Http 要求的 URL 路徑來關聯路由。</span><span class="sxs-lookup"><span data-stu-id="d4980-107">URL Path-based routing enables you to associate routes based on the URL path of an Http request.</span></span> <span data-ttu-id="d4980-108">它會檢查應用程式閘道中是否有路由指向 URL 設定的後端集區。</span><span class="sxs-lookup"><span data-stu-id="d4980-108">It checks if there is a route to a back-end pool configured for the URL presented in the Application Gateway.</span></span> <span data-ttu-id="d4980-109">然後將網路流量傳送到已定義的後端集區。</span><span class="sxs-lookup"><span data-stu-id="d4980-109">It then sends the network traffic to the defined back-end pool.</span></span> <span data-ttu-id="d4980-110">URL 型路由的常見用法是將不同內容類型的要求負載平衡至不同的後端伺服器集區。</span><span class="sxs-lookup"><span data-stu-id="d4980-110">A common use for URL-based routing is to load balance requests for different content types to different back-end server pools.</span></span>

<span data-ttu-id="d4980-111">URL 型路由會將新的規則類型引進應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="d4980-111">URL-based routing introduces a new rule type to application gateway.</span></span> <span data-ttu-id="d4980-112">應用程式閘道具有 2 種規則類型：基本和 PathBasedRouting。</span><span class="sxs-lookup"><span data-stu-id="d4980-112">Application gateway has two rule types: basic and PathBasedRouting.</span></span> <span data-ttu-id="d4980-113">基本規則類型會針對後端集區提供循環配置資源服務，而 PathBasedRouting 除了循環配置資源發佈之外也會在選擇後端集區時將要求 URL 的路徑模式納入考慮。</span><span class="sxs-lookup"><span data-stu-id="d4980-113">Basic rule type provides round-robin service for the back-end pools while PathBasedRouting in addition to round robin distribution, also takes path pattern of the request URL into account while choosing the backend pool.</span></span>

## <a name="scenario"></a><span data-ttu-id="d4980-114">案例</span><span class="sxs-lookup"><span data-stu-id="d4980-114">Scenario</span></span>

<span data-ttu-id="d4980-115">在下列範例中，應用程式閘道會利用兩個後端伺服器集區來為 contoso.com 提供流量：視訊伺服器集區和映像伺服器集區。</span><span class="sxs-lookup"><span data-stu-id="d4980-115">In the following example, Application Gateway is serving traffic for contoso.com with two back-end server pools: video server pool and image server pool.</span></span>

<span data-ttu-id="d4980-116">對 http://contoso.com/image* 的要求會路由傳送至影像伺服器集區 (pool1)，而 http://contoso.com/video* 則會路由傳送至影片伺服器集區 (pool2)。</span><span class="sxs-lookup"><span data-stu-id="d4980-116">Requests for http://contoso.com/image* are routed to image server pool (pool1), and http://contoso.com/video* are routed to video server pool (pool2).</span></span> <span data-ttu-id="d4980-117">如果沒有任何路徑模式相符，則會選取預設的伺服器集區 (pool1)。</span><span class="sxs-lookup"><span data-stu-id="d4980-117">if none of the path patterns match, a default server pool (pool1) is selected.</span></span>

![URL 路由](./media/application-gateway-create-url-route-arm-ps/figure1.png)

## <a name="before-you-begin"></a><span data-ttu-id="d4980-119">開始之前</span><span class="sxs-lookup"><span data-stu-id="d4980-119">Before you begin</span></span>

1. <span data-ttu-id="d4980-120">使用 Web Platform Installer 安裝最新版的 Azure PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="d4980-120">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span></span> <span data-ttu-id="d4980-121">您可以從 **下載頁面** 的 [Windows PowerShell](https://azure.microsoft.com/downloads/)區段下載並安裝最新版本。</span><span class="sxs-lookup"><span data-stu-id="d4980-121">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="d4980-122">您會建立應用程式閘道的虛擬網路和子網路。</span><span class="sxs-lookup"><span data-stu-id="d4980-122">You create a virtual network and subnet for Application Gateway.</span></span> <span data-ttu-id="d4980-123">請確定沒有虛擬機器或是雲端部署正在使用子網路。</span><span class="sxs-lookup"><span data-stu-id="d4980-123">Make sure that no virtual machines or cloud deployments are using the subnet.</span></span> <span data-ttu-id="d4980-124">應用程式閘道必須單獨位於虛擬網路子網路中。</span><span class="sxs-lookup"><span data-stu-id="d4980-124">The application gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="d4980-125">加入後端集區以使用應用程式閘道的伺服器必須存在，或是在虛擬網路中建立其端點，或是指派公用 IP/VIP。</span><span class="sxs-lookup"><span data-stu-id="d4980-125">The servers added to the back-end pool to use the application gateway must exist or have their endpoints created either in the virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-to-create-an-application-gateway"></a><span data-ttu-id="d4980-126">建立應用程式閘道需要什麼？</span><span class="sxs-lookup"><span data-stu-id="d4980-126">What is required to create an application gateway?</span></span>

* <span data-ttu-id="d4980-127">**後端伺服器集區：** 後端伺服器的 IP 位址清單。</span><span class="sxs-lookup"><span data-stu-id="d4980-127">**Back-end server pool:** The list of IP addresses of the back-end servers.</span></span> <span data-ttu-id="d4980-128">列出的 IP 位址應屬於虛擬網路子網路或是公用 IP/VIP。</span><span class="sxs-lookup"><span data-stu-id="d4980-128">The IP addresses listed should either belong to the virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="d4980-129">**後端伺服器集區設定：** 每個集區都包括一些設定，例如連接埠、通訊協定和以 Cookie 為基礎的同質性。</span><span class="sxs-lookup"><span data-stu-id="d4980-129">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="d4980-130">這些設定會繫結至集區，並套用至集區內所有伺服器。</span><span class="sxs-lookup"><span data-stu-id="d4980-130">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="d4980-131">**前端連接埠：** 此連接埠是在應用程式閘道上開啟的公用連接埠。</span><span class="sxs-lookup"><span data-stu-id="d4980-131">**Front-end port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="d4980-132">流量會到達此連接埠，然後重新導向至其中一個後端伺服器。</span><span class="sxs-lookup"><span data-stu-id="d4980-132">Traffic hits this port, and then gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="d4980-133">**接聽程式：** 接聽程式具有前端連接埠、通訊協定 (Http 或 Https，這些值都區分大小寫) 和 SSL 憑證名稱 (如果已設定 SSL 卸載)。</span><span class="sxs-lookup"><span data-stu-id="d4980-133">**Listener:** The listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="d4980-134">**規則：** 規則會繫結接聽程式和後端伺服器集區，並定義流量達到特定接聽程式時應該導向至哪個後端伺服器集區。</span><span class="sxs-lookup"><span data-stu-id="d4980-134">**Rule:** The rule binds the listener, the back-end server pool and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="d4980-135">建立應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="d4980-135">Create an application gateway</span></span>

<span data-ttu-id="d4980-136">使用「Azure 傳統」和「Azure Resource Manager」的差別，在於您建立應用程式閘道和需設定項目的順序。</span><span class="sxs-lookup"><span data-stu-id="d4980-136">The difference between using Azure Classic and Azure Resource Manager is the order in which you create the application gateway and the items that need to be configured.</span></span>

<span data-ttu-id="d4980-137">透過 Resource Manager，組成應用程式閘道的所有項目會個別進行設定，然後一併建立應用程式閘道資源。</span><span class="sxs-lookup"><span data-stu-id="d4980-137">With Resource Manager, all items that make an application gateway are configured individually and then put together to create the application gateway resource.</span></span>

<span data-ttu-id="d4980-138">以下是建立應用程式閘道所需的步驟：</span><span class="sxs-lookup"><span data-stu-id="d4980-138">Here are the steps that are needed to create an application gateway:</span></span>

1. <span data-ttu-id="d4980-139">建立資源管理員的資源群組。</span><span class="sxs-lookup"><span data-stu-id="d4980-139">Create a resource group for Resource Manager.</span></span>
2. <span data-ttu-id="d4980-140">建立應用程式閘道的虛擬網路、子網路和公用 IP。</span><span class="sxs-lookup"><span data-stu-id="d4980-140">Create a virtual network, subnet, and public IP for the application gateway.</span></span>
3. <span data-ttu-id="d4980-141">建立應用程式閘道組態物件。</span><span class="sxs-lookup"><span data-stu-id="d4980-141">Create an application gateway configuration object.</span></span>
4. <span data-ttu-id="d4980-142">建立應用程式閘道資源。</span><span class="sxs-lookup"><span data-stu-id="d4980-142">Create an application gateway resource.</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="d4980-143">建立資源管理員的資源群組</span><span class="sxs-lookup"><span data-stu-id="d4980-143">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="d4980-144">確定您使用最新版本的 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="d4980-144">Make sure that you are using the latest version of Azure PowerShell.</span></span> <span data-ttu-id="d4980-145">如需詳細資訊，請參閱 [搭配使用 Windows PowerShell 與資源管理員](../powershell-azure-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="d4980-145">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="d4980-146">步驟 1</span><span class="sxs-lookup"><span data-stu-id="d4980-146">Step 1</span></span>

<span data-ttu-id="d4980-147">登入 Azure</span><span class="sxs-lookup"><span data-stu-id="d4980-147">Log in to Azure</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="d4980-148">系統會提示使用您的認證進行驗證。</span><span class="sxs-lookup"><span data-stu-id="d4980-148">You are prompted to authenticate with your credentials.</span></span><BR>

### <a name="step-2"></a><span data-ttu-id="d4980-149">步驟 2</span><span class="sxs-lookup"><span data-stu-id="d4980-149">Step 2</span></span>

<span data-ttu-id="d4980-150">檢查帳戶的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d4980-150">Check the subscriptions for the account.</span></span>

```powershell
Get-AzureRmSubscription
```

### <a name="step-3"></a><span data-ttu-id="d4980-151">步驟 3</span><span class="sxs-lookup"><span data-stu-id="d4980-151">Step 3</span></span>

<span data-ttu-id="d4980-152">選擇要使用哪一個 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d4980-152">Choose which of your Azure subscriptions to use.</span></span> <BR>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="d4980-153">步驟 4</span><span class="sxs-lookup"><span data-stu-id="d4980-153">Step 4</span></span>

<span data-ttu-id="d4980-154">建立資源群組 (若使用現有的資源群組，請略過此步驟)。</span><span class="sxs-lookup"><span data-stu-id="d4980-154">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US"
```

<span data-ttu-id="d4980-155">或者，您也可以針對應用程式閘道建立資源群組的標記：</span><span class="sxs-lookup"><span data-stu-id="d4980-155">Alternatively you can also create tags for a resource group for application gateway:</span></span>

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US" -Tags @{Name = "testtag"; Value = "Application Gateway URL routing"} 
```

<span data-ttu-id="d4980-156">Azure Resource Manager 需要所有的資源群組指定一個位置。</span><span class="sxs-lookup"><span data-stu-id="d4980-156">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="d4980-157">此資源群組用來作為該資源群組中資源的預設位置。</span><span class="sxs-lookup"><span data-stu-id="d4980-157">This resource group is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="d4980-158">請確定所有用來建立應用程式閘道的命令都使用同一個資源群組。</span><span class="sxs-lookup"><span data-stu-id="d4980-158">Make sure that all commands to create an application gateway use the same resource group.</span></span>

<span data-ttu-id="d4980-159">在上述範例中，我們建立名為 "appgw-RG" 的資源群組，且位置為美國西部 ("West US")。</span><span class="sxs-lookup"><span data-stu-id="d4980-159">In the example above, we created a resource group called "appgw-RG" and location "West US".</span></span>

> [!NOTE]
> <span data-ttu-id="d4980-160">如果您需要為應用程式閘道設定自訂探查，請參閱 [使用 PowerShell 建立具有自訂探查的應用程式閘道](application-gateway-create-probe-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="d4980-160">If you need to configure a custom probe for your application gateway, see [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md).</span></span> <span data-ttu-id="d4980-161">請參閱 [自訂探查和健全狀況監視](application-gateway-probe-overview.md) 以取得詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="d4980-161">Check out [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>
> 
> 

## <a name="create-a-virtual-network-and-a-subnet-for-the-application-gateway"></a><span data-ttu-id="d4980-162">建立應用程式閘道的虛擬網路和子網路</span><span class="sxs-lookup"><span data-stu-id="d4980-162">Create a virtual network and a subnet for the application gateway</span></span>

<span data-ttu-id="d4980-163">下面的範例說明如何使用資源管理員建立虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="d4980-163">The following example shows how to create a virtual network by using Resource Manager.</span></span> <span data-ttu-id="d4980-164">這個範例會建立應用程式閘道的 VNET。</span><span class="sxs-lookup"><span data-stu-id="d4980-164">This example creates a VNET for the Application Gateway.</span></span> <span data-ttu-id="d4980-165">應用程式閘道需要自己的子網路，因此針對應用程式閘道建立的子網路會小於 VNET 位址空間。</span><span class="sxs-lookup"><span data-stu-id="d4980-165">Application Gateway requires its own subnet, for this reason the subnet created for the Application Gateway is smaller than the VNET address space.</span></span> <span data-ttu-id="d4980-166">這允許其他資源，包括但不限於要在相同 VNET 中設定的 Web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="d4980-166">This allows for other resources, including but not limited to web servers to be configured in the same VNET.</span></span>

### <a name="step-1"></a><span data-ttu-id="d4980-167">步驟 1</span><span class="sxs-lookup"><span data-stu-id="d4980-167">Step 1</span></span>

<span data-ttu-id="d4980-168">指派用於建立虛擬網路的位址範圍 10.0.0.0/24 給子網路變數。</span><span class="sxs-lookup"><span data-stu-id="d4980-168">Assign the address range 10.0.0.0/24 to the subnet variable to be used to create a virtual network.</span></span>  <span data-ttu-id="d4980-169">這會為下一個範例使用的應用程式閘道建立子網路設定物件。</span><span class="sxs-lookup"><span data-stu-id="d4980-169">This creates the subnet configuration object for the Application Gateway, which is used in the next example.</span></span>

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

### <a name="step-2"></a><span data-ttu-id="d4980-170">步驟 2</span><span class="sxs-lookup"><span data-stu-id="d4980-170">Step 2</span></span>

<span data-ttu-id="d4980-171">使用前置詞 10.0.0.0/16 搭配子網路 10.0.0.0/24，在美國西部 (West US) 區域的 **appgw-rg** 資源群組中建立名為 **appgwvnet** 的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="d4980-171">Create a virtual network named **appgwvnet** in resource group **appgw-rg** for the West US region using the prefix 10.0.0.0/16 with subnet 10.0.0.0/24.</span></span> <span data-ttu-id="d4980-172">這樣就完成 VNET 的設定，有單一子網路放置應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="d4980-172">This completes the configuration of the VNET with a single subnet for the Application Gateway to reside.</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet
```

### <a name="step-3"></a><span data-ttu-id="d4980-173">步驟 3</span><span class="sxs-lookup"><span data-stu-id="d4980-173">Step 3</span></span>

<span data-ttu-id="d4980-174">指派後續步驟的子網路變數，這會在未來的步驟中傳遞至 `New-AzureRMApplicationGateway` Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="d4980-174">Assign the subnet variable for the next steps, this is passed to the `New-AzureRMApplicationGateway` cmdlet in a future step.</span></span>

```powershell
$subnet=$vnet.Subnets[0]
```

## <a name="create-a-public-ip-address-for-the-front-end-configuration"></a><span data-ttu-id="d4980-175">建立前端組態的公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="d4980-175">Create a public IP address for the front-end configuration</span></span>

<span data-ttu-id="d4980-176">在美國西部區域的 **appgw-rg** 資源群組中建立公用 IP 資源 **publicIP01**。</span><span class="sxs-lookup"><span data-stu-id="d4980-176">Create a public IP resource **publicIP01** in resource group **appgw-rg** for the West US region.</span></span> <span data-ttu-id="d4980-177">應用程式閘道可以使用公用 IP 位址、內部 IP 位址或兩者來接收進行負載平衡的要求。</span><span class="sxs-lookup"><span data-stu-id="d4980-177">Application Gateway can use a public IP address, internal IP address or both to receive requests for load balancing.</span></span>  <span data-ttu-id="d4980-178">此範例中僅使用公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="d4980-178">This example only uses a public IP address.</span></span> <span data-ttu-id="d4980-179">在下列範例中，未設定 DNS 名稱以建立公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="d4980-179">In the following example, no DNS name is configured for creating the Public IP address.</span></span>  <span data-ttu-id="d4980-180">應用程式閘道在不支援公用 IP 位址上自訂 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="d4980-180">Application Gateway does not support custom DNS names on public IP addresses.</span></span>  <span data-ttu-id="d4980-181">如果公用端點需要自訂名稱，應該建立 CNAME 記錄以指向針對公用 IP 位址自動產生的 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="d4980-181">If a custom name is required for the public endpoint, a CNAME record should be created to point to the automatically generated DNS name for the public IP address.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="d4980-182">在服務啟動時，系統會將 IP 位址指派至應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="d4980-182">An IP address is assigned to the application gateway when the service starts.</span></span>

## <a name="create-application-gateway-configuration"></a><span data-ttu-id="d4980-183">建立應用程式閘道組態</span><span class="sxs-lookup"><span data-stu-id="d4980-183">Create application gateway configuration</span></span>

<span data-ttu-id="d4980-184">建立應用程式閘道之前，必須先設定所有組態項目。</span><span class="sxs-lookup"><span data-stu-id="d4980-184">All configuration items must be set up before creating the application gateway.</span></span> <span data-ttu-id="d4980-185">下列步驟會建立應用程式閘道資源所需的組態項目。</span><span class="sxs-lookup"><span data-stu-id="d4980-185">The following steps create the configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="d4980-186">步驟 1</span><span class="sxs-lookup"><span data-stu-id="d4980-186">Step 1</span></span>

<span data-ttu-id="d4980-187">建立名為 **gatewayIP01** 的應用程式閘道 IP 組態。</span><span class="sxs-lookup"><span data-stu-id="d4980-187">Create an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="d4980-188">當「應用程式閘道」啟動時，它會從已設定的子網路取得 IP 位址，再將網路流量路由傳送到後端 IP 集區中的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="d4980-188">When Application Gateway starts, it picks up an IP address from the subnet configured and route network traffic to the IP addresses in the back-end IP pool.</span></span> <span data-ttu-id="d4980-189">請記住，每個執行個體需要一個 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="d4980-189">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

### <a name="step-2"></a><span data-ttu-id="d4980-190">步驟 2</span><span class="sxs-lookup"><span data-stu-id="d4980-190">Step 2</span></span>

<span data-ttu-id="d4980-191">設定名為 **pool01** 和 **pool2** 的後端 IP 位址集區，並指定 **pool1** 和 **pool2** 的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="d4980-191">Configure the back-end IP address pool named **pool01** and **pool2** with IP addresses for **pool1** and **pool2**.</span></span> <span data-ttu-id="d4980-192">這些 IP 位址是託管 Web 應用程式 (由應用程式閘道保護) 之資源的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="d4980-192">These IP addresses are the IP addresses of the resources that are hosting the web application to be protected by the application gateway.</span></span> <span data-ttu-id="d4980-193">這些後端集區成員都由探查 (無論是基本探查或自訂探查) 驗證為健康狀態。</span><span class="sxs-lookup"><span data-stu-id="d4980-193">These backend pool members are all validated to be healthy by probes whether they are basic probes or custom probes.</span></span>  <span data-ttu-id="d4980-194">當要求進入應用程式閘道時，流量便會路由至它們。</span><span class="sxs-lookup"><span data-stu-id="d4980-194">Traffic is then routed to them when requests come into the application gateway.</span></span> <span data-ttu-id="d4980-195">後端集區可在應用程式閘道內供多個規則使用，這表示一個後端集區可用於位在相同主機上的多個 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d4980-195">Backend pools can be used by multiple rules within the application gateway, which means one backend pool could be used for multiple web applications that reside on the same host.</span></span>

```powershell
$pool1 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221, 134.170.185.50

$pool2 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool02 -BackendIPAddresses 134.170.186.47, 134.170.189.222, 134.170.186.51
```

<span data-ttu-id="d4980-196">此範例中有兩個後端集區，根據 URL 路徑路由傳送網路流量。</span><span class="sxs-lookup"><span data-stu-id="d4980-196">In this example, there are two back-end pools to route network traffic based on the URL path.</span></span> <span data-ttu-id="d4980-197">有一個集區會接收來自 URL 路徑 "/video" 的流量，而另一個集區會接收來自路徑 "/image" 的流量。</span><span class="sxs-lookup"><span data-stu-id="d4980-197">One pool receives traffic from URL path "/video" and other pool receive traffic from path "/image".</span></span> <span data-ttu-id="d4980-198">取代上述 IP 位址來新增自己的應用程式 IP 位址端點。</span><span class="sxs-lookup"><span data-stu-id="d4980-198">Replace the preceding IP addresses to add your own application IP address endpoints.</span></span> 

### <a name="step-3"></a><span data-ttu-id="d4980-199">步驟 3</span><span class="sxs-lookup"><span data-stu-id="d4980-199">Step 3</span></span>

<span data-ttu-id="d4980-200">針對後端集區中負載平衡的網路流量，設定應用程式閘道設定 **poolsetting01** 和 **poolsetting02**。</span><span class="sxs-lookup"><span data-stu-id="d4980-200">Configure application gateway setting **poolsetting01** and **poolsetting02** for the load-balanced network traffic in the back-end pool.</span></span> <span data-ttu-id="d4980-201">在此範例中，您會針對後端集區設定不同的後端集區設定。</span><span class="sxs-lookup"><span data-stu-id="d4980-201">In this example, you configure different back-end pool settings for the back-end pools.</span></span> <span data-ttu-id="d4980-202">每個後端集區都可以有它自己的後端集區設定。</span><span class="sxs-lookup"><span data-stu-id="d4980-202">Each back-end pool can have its own back-end pool setting.</span></span>  <span data-ttu-id="d4980-203">規則會使用後端 HTTP 設定，將流量路由傳送至正確的後端集區成員。</span><span class="sxs-lookup"><span data-stu-id="d4980-203">Backend HTTP settings are used by rules to route traffic to the correct backend pool members.</span></span> <span data-ttu-id="d4980-204">這會決定將流量傳送至後端集區成員時使用的通訊協定和連接埠。</span><span class="sxs-lookup"><span data-stu-id="d4980-204">This determines the protocol and port that is used when sending traffic to the backend pool members.</span></span> <span data-ttu-id="d4980-205">Cookie 型工作階段也是由後端 HTTP 設定決定。</span><span class="sxs-lookup"><span data-stu-id="d4980-205">Cookie-based sessions are also determined by the backend HTTP settings.</span></span>  <span data-ttu-id="d4980-206">啟用時，Cookie 型工作階段親和性會如每個封包的先前要求將流量至相同的後端。</span><span class="sxs-lookup"><span data-stu-id="d4980-206">If enabled, cookie-based session affinity sends traffic to the same backend as previous requests for each packet.</span></span>

```powershell
$poolSetting01 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120

$poolSetting02 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting02" -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 240
```

### <a name="step-4"></a><span data-ttu-id="d4980-207">步驟 4</span><span class="sxs-lookup"><span data-stu-id="d4980-207">Step 4</span></span>

<span data-ttu-id="d4980-208">利用公用 IP 端點設定前端 IP。</span><span class="sxs-lookup"><span data-stu-id="d4980-208">Configure the front-end IP with public IP endpoint.</span></span> <span data-ttu-id="d4980-209">接聽程式會使用前端 IP 設定物件，將對外 IP 位址與接聽程式相關聯。</span><span class="sxs-lookup"><span data-stu-id="d4980-209">The front-end IP configuration object is used by a listener to relate the outward facing IP address with the listener.</span></span>

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-5"></a><span data-ttu-id="d4980-210">步驟 5</span><span class="sxs-lookup"><span data-stu-id="d4980-210">Step 5</span></span>

<span data-ttu-id="d4980-211">設定應用程式閘道的前端連接埠。</span><span class="sxs-lookup"><span data-stu-id="d4980-211">Configure the front-end port for an application gateway.</span></span> <span data-ttu-id="d4980-212">接聽程式會使用前端連接埠組態物件來定義應用程式閘道會接聽哪個連接埠以取得接聽程式上的流量。</span><span class="sxs-lookup"><span data-stu-id="d4980-212">The front-end port configuration object is used by a listener to define what port the Application Gateway listens for traffic on the listener.</span></span>

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "fep01" -Port 80
```

### <a name="step-6"></a><span data-ttu-id="d4980-213">步驟 6</span><span class="sxs-lookup"><span data-stu-id="d4980-213">Step 6</span></span>

<span data-ttu-id="d4980-214">設定接聽程式。</span><span class="sxs-lookup"><span data-stu-id="d4980-214">Configure the listener.</span></span> <span data-ttu-id="d4980-215">這個步驟會針對用來接收連入網路流量的公用 IP 位址和連接埠設定接聽程式。</span><span class="sxs-lookup"><span data-stu-id="d4980-215">This step configures the listener for the public IP address and port used to receive incoming network traffic.</span></span> <span data-ttu-id="d4980-216">下列範例會採用先前設定的前端 IP 組態、前端連接埠組態及通訊協定 (http 或 https)，並設定接聽程式。</span><span class="sxs-lookup"><span data-stu-id="d4980-216">The following example takes the previously configured front-end IP configuration,  front-end port configuration, and a protocol (http or https) and configures the listener.</span></span> <span data-ttu-id="d4980-217">在此範例中，接聽程式會接聽稍早建立的公用 IP 位址上連接埠 80 的 HTTP 流量。</span><span class="sxs-lookup"><span data-stu-id="d4980-217">In this example, the listener listens to HTTP traffic on port 80 on the public IP address that was created earlier.</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol Http -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01
```

### <a name="step-7"></a><span data-ttu-id="d4980-218">步驟 7</span><span class="sxs-lookup"><span data-stu-id="d4980-218">Step 7</span></span>

<span data-ttu-id="d4980-219">設定後端集區的 URL 規則路徑。</span><span class="sxs-lookup"><span data-stu-id="d4980-219">Configure URL rule paths for the back-end pools.</span></span> <span data-ttu-id="d4980-220">這個步驟會設定應用程式閘道所使用的相對路徑，並定義 URL 路徑和已指派的後端集區之間的對應，以處理傳入流量。</span><span class="sxs-lookup"><span data-stu-id="d4980-220">This step configures the relative path used by application gateway and defines the mapping between the URL path and the back-end pool that is assigned to handle the incoming traffic.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d4980-221">每個路徑都必須以 / 開頭，而且只有結尾允許使用 "\*"。</span><span class="sxs-lookup"><span data-stu-id="d4980-221">Each path must start with / and the only place a "\*" is allowed, is at the end.</span></span> <span data-ttu-id="d4980-222">有效範例包括 /xyz、/xyz* 或 /xyz/*。</span><span class="sxs-lookup"><span data-stu-id="d4980-222">Valid examples are /xyz, /xyz* or /xyz/*.</span></span> <span data-ttu-id="d4980-223">傳送給路徑比對器的字串未在第一個 "?" 或 "#" 之後包含任何文字，而這些字元是不允許的。</span><span class="sxs-lookup"><span data-stu-id="d4980-223">The string fed to the path matcher does not include any text after the first "?" or "#", and those characters are not allowed.</span></span> 

<span data-ttu-id="d4980-224">下列範例會建立兩個規則：一個適用於將流量路由傳送到後端 "pool1" 的 "/image/" 路徑，另一個則適用於將流量路由傳送到後端 "pool2" 的 "/video/" 路徑。</span><span class="sxs-lookup"><span data-stu-id="d4980-224">The following example creates two rules: one for "/image/" path routing traffic to back-end "pool1" and another one for "/video/" path routing traffic to back-end "pool2."</span></span> <span data-ttu-id="d4980-225">這些規則確保每一組 url 的流量都路由傳送至後端。</span><span class="sxs-lookup"><span data-stu-id="d4980-225">These rules ensure that traffic for each set of urls is routed to the backend.</span></span> <span data-ttu-id="d4980-226">例如，http://contoso.com/image/figure1.jpg 會傳送至 pool1，http://contoso.com/video/example.mp4 會傳送至 pool2。</span><span class="sxs-lookup"><span data-stu-id="d4980-226">For example, http://contoso.com/image/figure1.jpg goes to pool1 and http://contoso.com/video/example.mp4 goes to pool2.</span></span>

```powershell
$imagePathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "pathrule1" -Paths "/image/*" -BackendAddressPool $pool1 -BackendHttpSettings $poolSetting01

$videoPathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "pathrule2" -Paths "/video/*" -BackendAddressPool $pool2 -BackendHttpSettings $poolSetting02
```

<span data-ttu-id="d4980-227">如果路徑不符合任何預先定義的路徑規則，規則路徑對應組態也會設定預設的後端位址集區。</span><span class="sxs-lookup"><span data-stu-id="d4980-227">If the path doesn't match any of the pre-defined path rules, the rule path map configuration also configures a default back-end address pool.</span></span> <span data-ttu-id="d4980-228">例如，http://contoso.com/shoppingcart/test.html 會傳送至 pool1，因為它定義為不相符流量的預設集區。</span><span class="sxs-lookup"><span data-stu-id="d4980-228">For example, http://contoso.com/shoppingcart/test.html goes to pool1 as it is defined as the default pool for unmatched traffic.</span></span>

```powershell
$urlPathMap = New-AzureRmApplicationGatewayUrlPathMapConfig -Name "urlpathmap" -PathRules $videoPathRule, $imagePathRule -DefaultBackendAddressPool $pool1 -DefaultBackendHttpSettings $poolSetting02
```

### <a name="step-8"></a><span data-ttu-id="d4980-229">步驟 8</span><span class="sxs-lookup"><span data-stu-id="d4980-229">Step 8</span></span>

<span data-ttu-id="d4980-230">建立規則設定。</span><span class="sxs-lookup"><span data-stu-id="d4980-230">Create a rule setting.</span></span> <span data-ttu-id="d4980-231">這個步驟會設定應用程式閘道來使用 URL 路徑型路由。</span><span class="sxs-lookup"><span data-stu-id="d4980-231">This step configures the application gateway to use URL path-based routing.</span></span> <span data-ttu-id="d4980-232">稍早步驟中定義的 `$urlPathMap` 變數，現在用來建立以路徑為基礎的規則。</span><span class="sxs-lookup"><span data-stu-id="d4980-232">The `$urlPathMap` variable defined in the earlier step is now used to create the path-based rule.</span></span> <span data-ttu-id="d4980-233">在此步驟中，我們將規則與接聽程式和稍早建立的 url 路徑對應相關聯。</span><span class="sxs-lookup"><span data-stu-id="d4980-233">In this step, we associate the rule with a listener and the url path mapping created earlier.</span></span>

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule1" -RuleType PathBasedRouting -HttpListener $listener -UrlPathMap $urlPathMap
```

### <a name="step-9"></a><span data-ttu-id="d4980-234">步驟 9</span><span class="sxs-lookup"><span data-stu-id="d4980-234">Step 9</span></span>

<span data-ttu-id="d4980-235">設定執行個體數目和應用程式閘道的大小。</span><span class="sxs-lookup"><span data-stu-id="d4980-235">Configure the number of instances and size for the application gateway.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "Standard_Small" -Tier Standard -Capacity 2
```

## <a name="create-application-gateway"></a><span data-ttu-id="d4980-236">建立應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="d4980-236">Create Application Gateway</span></span>

<span data-ttu-id="d4980-237">利用上述步驟中的所有組態物件來建立應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="d4980-237">Create an application gateway with all configuration objects from the preceding steps.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-RG -Location "West US" -BackendAddressPools $pool1,$pool2 -BackendHttpSettingsCollection $poolSetting01, $poolSetting02 -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener -UrlPathMaps $urlPathMap -RequestRoutingRules $rule01 -Sku $sku
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="d4980-238">取得應用程式閘道 DNS 名稱</span><span class="sxs-lookup"><span data-stu-id="d4980-238">Get application gateway DNS name</span></span>

<span data-ttu-id="d4980-239">建立閘道之後，下一步是設定通訊的前端。</span><span class="sxs-lookup"><span data-stu-id="d4980-239">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="d4980-240">當使用公用 IP 時，應用程式閘道需要動態指派的 DNS 名稱 (不易記住)。</span><span class="sxs-lookup"><span data-stu-id="d4980-240">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="d4980-241">為了確保使用者可以叫用應用程式閘道，可使用 CNAME 記錄來指向應用程式閘道的公用端點。</span><span class="sxs-lookup"><span data-stu-id="d4980-241">To ensure end users can hit the application gateway, a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="d4980-242">[在 Azure 中設定自訂網域名稱](../cloud-services/cloud-services-custom-domain-name-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="d4980-242">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="d4980-243">若要設定前端 IP CNAME 記錄，使用連接至應用程式閘道的 PublicIPAddress 元素，擷取應用程式閘道的詳細資料及其關聯的 IP/DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="d4980-243">To configure the frontend IP CNAME record, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="d4980-244">應用程式閘道的 DNS 名稱應該用於建立 CNAME 記錄。</span><span class="sxs-lookup"><span data-stu-id="d4980-244">The application gateway's DNS name should be used to create a CNAME record.</span></span> <span data-ttu-id="d4980-245">不建議使用 A-records，因為重新啟動應用程式閘道時，VIP 可能會變更。</span><span class="sxs-lookup"><span data-stu-id="d4980-245">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="d4980-246">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d4980-246">Next steps</span></span>

<span data-ttu-id="d4980-247">如果您想要了解「安全通訊端層」(SSL) 卸載，請參閱 [設定適用於 SSL 卸載的應用程式閘道](application-gateway-ssl-arm.md)。</span><span class="sxs-lookup"><span data-stu-id="d4980-247">If you want to learn Secure Sockets Layer (SSL) offload, see [Configure an application gateway for SSL offload](application-gateway-ssl-arm.md).</span></span>

