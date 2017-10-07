---
title: "應用程式閘道使用的 URL 路由規則的 aaaCreate |Microsoft 文件"
description: "本頁面提供的指示 toocreate、 設定 Azure 應用程式閘道使用的 URL 路由規則"
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
ms.openlocfilehash: 54fcccc39e48a933576968ce3d8160518c0d0b7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-using-path-based-routing"></a><span data-ttu-id="8c031-103">使用路徑型路由建立應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="8c031-103">Create an application gateway using Path-based routing</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="8c031-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="8c031-104">Azure portal</span></span>](application-gateway-create-url-route-portal.md)
> * [<span data-ttu-id="8c031-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="8c031-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-url-route-arm-ps.md)
> * [<span data-ttu-id="8c031-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="8c031-106">Azure CLI 2.0</span></span>](application-gateway-create-url-route-cli.md)

<span data-ttu-id="8c031-107">路徑為基礎的路由 URL 可讓您 tooassociate 路由根據 hello 的 Http 要求的 URL 路徑。</span><span class="sxs-lookup"><span data-stu-id="8c031-107">URL Path-based routing enables you tooassociate routes based on hello URL path of an Http request.</span></span> <span data-ttu-id="8c031-108">它會檢查是否有設定 hello 應用程式閘道中的 hello URL 路由 tooa 後端集區。</span><span class="sxs-lookup"><span data-stu-id="8c031-108">It checks if there is a route tooa back-end pool configured for hello URL presented in hello Application Gateway.</span></span> <span data-ttu-id="8c031-109">接著會傳送 hello 網路流量 toohello 定義後端集區。</span><span class="sxs-lookup"><span data-stu-id="8c031-109">It then sends hello network traffic toohello defined back-end pool.</span></span> <span data-ttu-id="8c031-110">URL 為基礎的路由的常見用法是不同的內容類型 toodifferent 後端伺服器集區的 tooload 平衡要求。</span><span class="sxs-lookup"><span data-stu-id="8c031-110">A common use for URL-based routing is tooload balance requests for different content types toodifferent back-end server pools.</span></span>

<span data-ttu-id="8c031-111">URL 為基礎的路由導入了新的規則類型 tooapplication 閘道。</span><span class="sxs-lookup"><span data-stu-id="8c031-111">URL-based routing introduces a new rule type tooapplication gateway.</span></span> <span data-ttu-id="8c031-112">應用程式閘道具有 2 種規則類型：基本和 PathBasedRouting。</span><span class="sxs-lookup"><span data-stu-id="8c031-112">Application gateway has two rule types: basic and PathBasedRouting.</span></span> <span data-ttu-id="8c031-113">基本規則類型提供循環配置資源服務的 hello 後端集區時 PathBasedRouting 此外 tooround 循環配置資源發佈，也會考量 hello 要求 URL 的路徑模式並選擇 hello 後端集區。</span><span class="sxs-lookup"><span data-stu-id="8c031-113">Basic rule type provides round-robin service for hello back-end pools while PathBasedRouting in addition tooround robin distribution, also takes path pattern of hello request URL into account while choosing hello backend pool.</span></span>

## <a name="scenario"></a><span data-ttu-id="8c031-114">案例</span><span class="sxs-lookup"><span data-stu-id="8c031-114">Scenario</span></span>

<span data-ttu-id="8c031-115">在下列範例的 hello，應用程式閘道為 contoso.com 的流量提供兩個後端伺服器集區： 視訊的伺服器集區及影像伺服器集區。</span><span class="sxs-lookup"><span data-stu-id="8c031-115">In hello following example, Application Gateway is serving traffic for contoso.com with two back-end server pools: video server pool and image server pool.</span></span>

<span data-ttu-id="8c031-116">要求 http://contoso.com/image * 會路由傳送 tooimage 伺服器集區 (pool1)，及 http://contoso.com/video * 會路由傳送 toovideo 伺服器集區 (pool2)。</span><span class="sxs-lookup"><span data-stu-id="8c031-116">Requests for http://contoso.com/image* are routed tooimage server pool (pool1), and http://contoso.com/video* are routed toovideo server pool (pool2).</span></span> <span data-ttu-id="8c031-117">如果沒有 hello 路徑模式符合，會選取預設的伺服器集區 (pool1)。</span><span class="sxs-lookup"><span data-stu-id="8c031-117">if none of hello path patterns match, a default server pool (pool1) is selected.</span></span>

![URL 路由](./media/application-gateway-create-url-route-arm-ps/figure1.png)

## <a name="before-you-begin"></a><span data-ttu-id="8c031-119">開始之前</span><span class="sxs-lookup"><span data-stu-id="8c031-119">Before you begin</span></span>

1. <span data-ttu-id="8c031-120">使用 hello Web Platform Installer 安裝 hello hello Azure PowerShell cmdlet 的最新版本。</span><span class="sxs-lookup"><span data-stu-id="8c031-120">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="8c031-121">您可以從下載並安裝最新版本的 hello hello **Windows PowerShell**區段 hello[下載頁面](https://azure.microsoft.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="8c031-121">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="8c031-122">您會建立應用程式閘道的虛擬網路和子網路。</span><span class="sxs-lookup"><span data-stu-id="8c031-122">You create a virtual network and subnet for Application Gateway.</span></span> <span data-ttu-id="8c031-123">請確定沒有虛擬機器或雲端部署使用 hello 子網路。</span><span class="sxs-lookup"><span data-stu-id="8c031-123">Make sure that no virtual machines or cloud deployments are using hello subnet.</span></span> <span data-ttu-id="8c031-124">hello 應用程式閘道必須單獨在虛擬網路子網路。</span><span class="sxs-lookup"><span data-stu-id="8c031-124">hello application gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="8c031-125">hello 伺服器加入 toohello 後端集區 toouse hello 應用程式閘道必須存在，或其端點建立 hello 虛擬網路中或與公用 IP/VIP 指派。</span><span class="sxs-lookup"><span data-stu-id="8c031-125">hello servers added toohello back-end pool toouse hello application gateway must exist or have their endpoints created either in hello virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-toocreate-an-application-gateway"></a><span data-ttu-id="8c031-126">什麼是必要的 toocreate 應用程式閘道？</span><span class="sxs-lookup"><span data-stu-id="8c031-126">What is required toocreate an application gateway?</span></span>

* <span data-ttu-id="8c031-127">**後端伺服器集區：** hello hello 後端伺服器的 IP 位址清單。</span><span class="sxs-lookup"><span data-stu-id="8c031-127">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="8c031-128">列出 hello IP 位址應該是屬於 toohello 虛擬網路子網路，或應該是公用 IP/VIP。</span><span class="sxs-lookup"><span data-stu-id="8c031-128">hello IP addresses listed should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="8c031-129">**後端伺服器集區設定：** 每個集區都包括一些設定，例如連接埠、通訊協定和以 Cookie 為基礎的同質性。</span><span class="sxs-lookup"><span data-stu-id="8c031-129">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="8c031-130">這些設定會繫結的 tooa 集區，並套用的 tooall hello 集區內的伺服器。</span><span class="sxs-lookup"><span data-stu-id="8c031-130">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="8c031-131">**前端連接埠：**此連接埠是開啟 hello 應用程式閘道上的 hello 公用連接埠。</span><span class="sxs-lookup"><span data-stu-id="8c031-131">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="8c031-132">流量叫用這個連接埠，然後再取得重新導向 tooone 的 hello 後端伺服器。</span><span class="sxs-lookup"><span data-stu-id="8c031-132">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="8c031-133">**接聽程式：** hello 接聽程式有前端連接埠的通訊協定 （Http 或 Https，這些值會區分大小寫），與 hello 的 SSL 憑證名稱 （如果有設定 SSL 卸載）。</span><span class="sxs-lookup"><span data-stu-id="8c031-133">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="8c031-134">**規則：** hello 規則繫結 hello 接聽程式，hello 後端伺服器集區，並定義哪一個後端伺服器集區 hello 流量應導向的 toowhen 配接器特定接聽程式。</span><span class="sxs-lookup"><span data-stu-id="8c031-134">**Rule:** hello rule binds hello listener, hello back-end server pool and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="8c031-135">建立應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="8c031-135">Create an application gateway</span></span>

<span data-ttu-id="8c031-136">使用 Azure 傳統和 Azure 資源管理員的 hello 差別在於 hello 順序建立 hello 應用程式閘道，必須設定 toobe hello 項目。</span><span class="sxs-lookup"><span data-stu-id="8c031-136">hello difference between using Azure Classic and Azure Resource Manager is hello order in which you create hello application gateway and hello items that need toobe configured.</span></span>

<span data-ttu-id="8c031-137">使用資源管理員，讓應用程式閘道的所有項目個別設定，然後放置在一起 toocreate hello 應用程式閘道資源。</span><span class="sxs-lookup"><span data-stu-id="8c031-137">With Resource Manager, all items that make an application gateway are configured individually and then put together toocreate hello application gateway resource.</span></span>

<span data-ttu-id="8c031-138">以下是需要的 toocreate 應用程式閘道的 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="8c031-138">Here are hello steps that are needed toocreate an application gateway:</span></span>

1. <span data-ttu-id="8c031-139">建立資源管理員的資源群組。</span><span class="sxs-lookup"><span data-stu-id="8c031-139">Create a resource group for Resource Manager.</span></span>
2. <span data-ttu-id="8c031-140">建立虛擬網路、 子網路和 hello 應用程式閘道的公用 IP。</span><span class="sxs-lookup"><span data-stu-id="8c031-140">Create a virtual network, subnet, and public IP for hello application gateway.</span></span>
3. <span data-ttu-id="8c031-141">建立應用程式閘道組態物件。</span><span class="sxs-lookup"><span data-stu-id="8c031-141">Create an application gateway configuration object.</span></span>
4. <span data-ttu-id="8c031-142">建立應用程式閘道資源。</span><span class="sxs-lookup"><span data-stu-id="8c031-142">Create an application gateway resource.</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="8c031-143">建立資源管理員的資源群組</span><span class="sxs-lookup"><span data-stu-id="8c031-143">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="8c031-144">請確定您使用 Azure PowerShell hello 最新版本。</span><span class="sxs-lookup"><span data-stu-id="8c031-144">Make sure that you are using hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="8c031-145">如需詳細資訊，請參閱 [搭配使用 Windows PowerShell 與資源管理員](../powershell-azure-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="8c031-145">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="8c031-146">步驟 1</span><span class="sxs-lookup"><span data-stu-id="8c031-146">Step 1</span></span>

<span data-ttu-id="8c031-147">登入 tooAzure</span><span class="sxs-lookup"><span data-stu-id="8c031-147">Log in tooAzure</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="8c031-148">您必須提示的 tooauthenticate 和您的認證。</span><span class="sxs-lookup"><span data-stu-id="8c031-148">You are prompted tooauthenticate with your credentials.</span></span><BR>

### <a name="step-2"></a><span data-ttu-id="8c031-149">步驟 2</span><span class="sxs-lookup"><span data-stu-id="8c031-149">Step 2</span></span>

<span data-ttu-id="8c031-150">請檢查 hello hello 帳戶的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="8c031-150">Check hello subscriptions for hello account.</span></span>

```powershell
Get-AzureRmSubscription
```

### <a name="step-3"></a><span data-ttu-id="8c031-151">步驟 3</span><span class="sxs-lookup"><span data-stu-id="8c031-151">Step 3</span></span>

<span data-ttu-id="8c031-152">選擇 Azure 訂用帳戶 toouse。</span><span class="sxs-lookup"><span data-stu-id="8c031-152">Choose which of your Azure subscriptions toouse.</span></span> <BR>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="8c031-153">步驟 4</span><span class="sxs-lookup"><span data-stu-id="8c031-153">Step 4</span></span>

<span data-ttu-id="8c031-154">建立資源群組 (若使用現有的資源群組，請略過此步驟)。</span><span class="sxs-lookup"><span data-stu-id="8c031-154">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US"
```

<span data-ttu-id="8c031-155">或者，您也可以針對應用程式閘道建立資源群組的標記：</span><span class="sxs-lookup"><span data-stu-id="8c031-155">Alternatively you can also create tags for a resource group for application gateway:</span></span>

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US" -Tags @{Name = "testtag"; Value = "Application Gateway URL routing"} 
```

<span data-ttu-id="8c031-156">Azure Resource Manager 需要所有的資源群組指定一個位置。</span><span class="sxs-lookup"><span data-stu-id="8c031-156">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="8c031-157">此資源群組用做 hello 預設位置，該資源群組中的資源。</span><span class="sxs-lookup"><span data-stu-id="8c031-157">This resource group is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="8c031-158">請確定所有命令 toocreate 應用程式閘道使用 hello 相同的資源群組。</span><span class="sxs-lookup"><span data-stu-id="8c031-158">Make sure that all commands toocreate an application gateway use hello same resource group.</span></span>

<span data-ttu-id="8c031-159">在 hello 上述範例中，我們會建立資源群組，稱為 「 appgw RG 」 和 「 美國西部 」 的位置。</span><span class="sxs-lookup"><span data-stu-id="8c031-159">In hello example above, we created a resource group called "appgw-RG" and location "West US".</span></span>

> [!NOTE]
> <span data-ttu-id="8c031-160">如果您需要 tooconfigure 自訂探查您應用程式閘道，請參閱[使用 PowerShell 建立應用程式閘道與自訂探查](application-gateway-create-probe-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="8c031-160">If you need tooconfigure a custom probe for your application gateway, see [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md).</span></span> <span data-ttu-id="8c031-161">請參閱 [自訂探查和健全狀況監視](application-gateway-probe-overview.md) 以取得詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="8c031-161">Check out [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>
> 
> 

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a><span data-ttu-id="8c031-162">建立虛擬網路和 hello 應用程式閘道的子網路</span><span class="sxs-lookup"><span data-stu-id="8c031-162">Create a virtual network and a subnet for hello application gateway</span></span>

<span data-ttu-id="8c031-163">下列範例會示範如何 hello toocreate 使用資源管理員的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="8c031-163">hello following example shows how toocreate a virtual network by using Resource Manager.</span></span> <span data-ttu-id="8c031-164">這個範例會建立 hello 應用程式閘道的 VNET。</span><span class="sxs-lookup"><span data-stu-id="8c031-164">This example creates a VNET for hello Application Gateway.</span></span> <span data-ttu-id="8c031-165">應用程式閘道需要它自己的子網路，因此 hello 子網路建立的應用程式閘道 hello 小於 hello VNET 位址空間。</span><span class="sxs-lookup"><span data-stu-id="8c031-165">Application Gateway requires its own subnet, for this reason hello subnet created for hello Application Gateway is smaller than hello VNET address space.</span></span> <span data-ttu-id="8c031-166">這可讓其他資源，包括但不是限於的 tooweb 伺服器 toobe 設定 hello 中相同的 VNET。</span><span class="sxs-lookup"><span data-stu-id="8c031-166">This allows for other resources, including but not limited tooweb servers toobe configured in hello same VNET.</span></span>

### <a name="step-1"></a><span data-ttu-id="8c031-167">步驟 1</span><span class="sxs-lookup"><span data-stu-id="8c031-167">Step 1</span></span>

<span data-ttu-id="8c031-168">指派 hello 位址範圍 10.0.0.0/24 toohello 子網路使用的變數 toobe toocreate 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="8c031-168">Assign hello address range 10.0.0.0/24 toohello subnet variable toobe used toocreate a virtual network.</span></span>  <span data-ttu-id="8c031-169">這會建立 hello hello hello 下一個範例中使用的應用程式閘道的子網路設定物件。</span><span class="sxs-lookup"><span data-stu-id="8c031-169">This creates hello subnet configuration object for hello Application Gateway, which is used in hello next example.</span></span>

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

### <a name="step-2"></a><span data-ttu-id="8c031-170">步驟 2</span><span class="sxs-lookup"><span data-stu-id="8c031-170">Step 2</span></span>

<span data-ttu-id="8c031-171">建立虛擬網路，名為**appgwvnet**資源群組中**appgw rg** hello 前置詞 10.0.0.0/16 使用子網路 10.0.0.0/24 hello 美國西部地區。</span><span class="sxs-lookup"><span data-stu-id="8c031-171">Create a virtual network named **appgwvnet** in resource group **appgw-rg** for hello West US region using hello prefix 10.0.0.0/16 with subnet 10.0.0.0/24.</span></span> <span data-ttu-id="8c031-172">如此即完成 hello hello VNET 與 hello 應用程式閘道 tooreside 的單一子網路設定。</span><span class="sxs-lookup"><span data-stu-id="8c031-172">This completes hello configuration of hello VNET with a single subnet for hello Application Gateway tooreside.</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet
```

### <a name="step-3"></a><span data-ttu-id="8c031-173">步驟 3</span><span class="sxs-lookup"><span data-stu-id="8c031-173">Step 3</span></span>

<span data-ttu-id="8c031-174">將 hello 子網路變數指派下一個步驟，這會傳遞 toohello`New-AzureRMApplicationGateway`指令程式在後續步驟。</span><span class="sxs-lookup"><span data-stu-id="8c031-174">Assign hello subnet variable for hello next steps, this is passed toohello `New-AzureRMApplicationGateway` cmdlet in a future step.</span></span>

```powershell
$subnet=$vnet.Subnets[0]
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a><span data-ttu-id="8c031-175">建立 hello 前端組態的公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="8c031-175">Create a public IP address for hello front-end configuration</span></span>

<span data-ttu-id="8c031-176">建立公用 IP 資源**publicIP01**資源群組中**appgw rg** hello 美國西部地區。</span><span class="sxs-lookup"><span data-stu-id="8c031-176">Create a public IP resource **publicIP01** in resource group **appgw-rg** for hello West US region.</span></span> <span data-ttu-id="8c031-177">應用程式閘道可以使用的公用 IP 位址、 內部 IP 位址或兩個 tooreceive 要求進行負載平衡。</span><span class="sxs-lookup"><span data-stu-id="8c031-177">Application Gateway can use a public IP address, internal IP address or both tooreceive requests for load balancing.</span></span>  <span data-ttu-id="8c031-178">此範例中僅使用公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="8c031-178">This example only uses a public IP address.</span></span> <span data-ttu-id="8c031-179">在下列範例的 hello，沒有 DNS 名稱已針對建立 hello 公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="8c031-179">In hello following example, no DNS name is configured for creating hello Public IP address.</span></span>  <span data-ttu-id="8c031-180">應用程式閘道在不支援公用 IP 位址上自訂 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="8c031-180">Application Gateway does not support custom DNS names on public IP addresses.</span></span>  <span data-ttu-id="8c031-181">如果需要 hello 公用端點的自訂名稱，CNAME 記錄應建立 hello 公用 IP 位址的 toopoint toohello 自動產生 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="8c031-181">If a custom name is required for hello public endpoint, a CNAME record should be created toopoint toohello automatically generated DNS name for hello public IP address.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="8c031-182">Hello 服務啟動時，會指派 toohello 應用程式閘道 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="8c031-182">An IP address is assigned toohello application gateway when hello service starts.</span></span>

## <a name="create-application-gateway-configuration"></a><span data-ttu-id="8c031-183">建立應用程式閘道組態</span><span class="sxs-lookup"><span data-stu-id="8c031-183">Create application gateway configuration</span></span>

<span data-ttu-id="8c031-184">所有設定項目必須都設定才能建立 hello 應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="8c031-184">All configuration items must be set up before creating hello application gateway.</span></span> <span data-ttu-id="8c031-185">hello 下列步驟建立 hello 組態項目所需的應用程式閘道資源。</span><span class="sxs-lookup"><span data-stu-id="8c031-185">hello following steps create hello configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="8c031-186">步驟 1</span><span class="sxs-lookup"><span data-stu-id="8c031-186">Step 1</span></span>

<span data-ttu-id="8c031-187">建立名為 **gatewayIP01** 的應用程式閘道 IP 組態。</span><span class="sxs-lookup"><span data-stu-id="8c031-187">Create an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="8c031-188">應用程式閘道啟動時，它會挑選設定 hello 子網路的 IP 位址，並傳送 hello 後端 IP 集區中的網路流量 toohello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="8c031-188">When Application Gateway starts, it picks up an IP address from hello subnet configured and route network traffic toohello IP addresses in hello back-end IP pool.</span></span> <span data-ttu-id="8c031-189">請記住，每個執行個體需要一個 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="8c031-189">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

### <a name="step-2"></a><span data-ttu-id="8c031-190">步驟 2</span><span class="sxs-lookup"><span data-stu-id="8c031-190">Step 2</span></span>

<span data-ttu-id="8c031-191">設定 hello 後端 IP 位址集區名稱為**pool01**和**pool2** IP 位址與**pool1**和**pool2**。</span><span class="sxs-lookup"><span data-stu-id="8c031-191">Configure hello back-end IP address pool named **pool01** and **pool2** with IP addresses for **pool1** and **pool2**.</span></span> <span data-ttu-id="8c031-192">這些 IP 位址是裝載 hello hello 應用程式閘道所保護的 web 應用程式 toobe hello 資源 hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="8c031-192">These IP addresses are hello IP addresses of hello resources that are hosting hello web application toobe protected by hello application gateway.</span></span> <span data-ttu-id="8c031-193">這些後端集區成員是所有驗證的 toobe 良好探查，無論是基本的探查 」 或 「 自訂探查。</span><span class="sxs-lookup"><span data-stu-id="8c031-193">These backend pool members are all validated toobe healthy by probes whether they are basic probes or custom probes.</span></span>  <span data-ttu-id="8c031-194">接著路由傳送流量 toothem 當要求進入 hello 應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="8c031-194">Traffic is then routed toothem when requests come into hello application gateway.</span></span> <span data-ttu-id="8c031-195">後端集區可供多個規則內 hello 應用程式閘道，這表示一個後端集區無法用於相同位於 hello 的多個 web 應用程式主機。</span><span class="sxs-lookup"><span data-stu-id="8c031-195">Backend pools can be used by multiple rules within hello application gateway, which means one backend pool could be used for multiple web applications that reside on hello same host.</span></span>

```powershell
$pool1 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221, 134.170.185.50

$pool2 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool02 -BackendIPAddresses 134.170.186.47, 134.170.189.222, 134.170.186.51
```

<span data-ttu-id="8c031-196">在此範例中，有兩個後端集區 tooroute 網路流量 hello URL 路徑。</span><span class="sxs-lookup"><span data-stu-id="8c031-196">In this example, there are two back-end pools tooroute network traffic based on hello URL path.</span></span> <span data-ttu-id="8c031-197">有一個集區會接收來自 URL 路徑 "/video" 的流量，而另一個集區會接收來自路徑 "/image" 的流量。</span><span class="sxs-lookup"><span data-stu-id="8c031-197">One pool receives traffic from URL path "/video" and other pool receive traffic from path "/image".</span></span> <span data-ttu-id="8c031-198">取代先前您自己的應用程式的 IP 位址端點的 IP 位址 tooadd hello。</span><span class="sxs-lookup"><span data-stu-id="8c031-198">Replace hello preceding IP addresses tooadd your own application IP address endpoints.</span></span> 

### <a name="step-3"></a><span data-ttu-id="8c031-199">步驟 3</span><span class="sxs-lookup"><span data-stu-id="8c031-199">Step 3</span></span>

<span data-ttu-id="8c031-200">設定應用程式閘道設定**poolsetting01**和**poolsetting02** hello hello 後端集區中，負載平衡網路流量。</span><span class="sxs-lookup"><span data-stu-id="8c031-200">Configure application gateway setting **poolsetting01** and **poolsetting02** for hello load-balanced network traffic in hello back-end pool.</span></span> <span data-ttu-id="8c031-201">在此範例中，您可以設定不同的後端集區設定 hello 後端集區。</span><span class="sxs-lookup"><span data-stu-id="8c031-201">In this example, you configure different back-end pool settings for hello back-end pools.</span></span> <span data-ttu-id="8c031-202">每個後端集區都可以有它自己的後端集區設定。</span><span class="sxs-lookup"><span data-stu-id="8c031-202">Each back-end pool can have its own back-end pool setting.</span></span>  <span data-ttu-id="8c031-203">後端 HTTP 設定使用規則 tooroute 流量 toohello 正確的後端集區成員。</span><span class="sxs-lookup"><span data-stu-id="8c031-203">Backend HTTP settings are used by rules tooroute traffic toohello correct backend pool members.</span></span> <span data-ttu-id="8c031-204">這會決定 hello 通訊協定和連接埠傳送流量 toohello 後端集區成員時所使用。</span><span class="sxs-lookup"><span data-stu-id="8c031-204">This determines hello protocol and port that is used when sending traffic toohello backend pool members.</span></span> <span data-ttu-id="8c031-205">Cookie 架構工作階段，也取決於 hello 後端 HTTP 設定。</span><span class="sxs-lookup"><span data-stu-id="8c031-205">Cookie-based sessions are also determined by hello backend HTTP settings.</span></span>  <span data-ttu-id="8c031-206">Cookie 架構工作階段相似性啟用時，會傳送流量 toohello 相同的後端，為每個封包的先前要求。</span><span class="sxs-lookup"><span data-stu-id="8c031-206">If enabled, cookie-based session affinity sends traffic toohello same backend as previous requests for each packet.</span></span>

```powershell
$poolSetting01 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120

$poolSetting02 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting02" -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 240
```

### <a name="step-4"></a><span data-ttu-id="8c031-207">步驟 4</span><span class="sxs-lookup"><span data-stu-id="8c031-207">Step 4</span></span>

<span data-ttu-id="8c031-208">設定公用 IP 端點 hello 前端 IP。</span><span class="sxs-lookup"><span data-stu-id="8c031-208">Configure hello front-end IP with public IP endpoint.</span></span> <span data-ttu-id="8c031-209">hello 前端 IP 組態物件會使用接聽程式 toorelate hello 向外面對 hello 接聽程式 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="8c031-209">hello front-end IP configuration object is used by a listener toorelate hello outward facing IP address with hello listener.</span></span>

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-5"></a><span data-ttu-id="8c031-210">步驟 5</span><span class="sxs-lookup"><span data-stu-id="8c031-210">Step 5</span></span>

<span data-ttu-id="8c031-211">設定應用程式閘道 hello 前端連接埠。</span><span class="sxs-lookup"><span data-stu-id="8c031-211">Configure hello front-end port for an application gateway.</span></span> <span data-ttu-id="8c031-212">hello 前端連接埠組態物件會使用接聽程式 toodefine 哪些連接埠 hello 應用程式閘道接聽 hello 接聽程式上的流量。</span><span class="sxs-lookup"><span data-stu-id="8c031-212">hello front-end port configuration object is used by a listener toodefine what port hello Application Gateway listens for traffic on hello listener.</span></span>

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "fep01" -Port 80
```

### <a name="step-6"></a><span data-ttu-id="8c031-213">步驟 6</span><span class="sxs-lookup"><span data-stu-id="8c031-213">Step 6</span></span>

<span data-ttu-id="8c031-214">Hello 接聽程式設定。</span><span class="sxs-lookup"><span data-stu-id="8c031-214">Configure hello listener.</span></span> <span data-ttu-id="8c031-215">此步驟會設定 hello hello 公用 IP 位址的接聽程式，以及使用 tooreceive 連入網路流量的連接埠。</span><span class="sxs-lookup"><span data-stu-id="8c031-215">This step configures hello listener for hello public IP address and port used tooreceive incoming network traffic.</span></span> <span data-ttu-id="8c031-216">hello 下列範例會使用前端 IP 組態之前設定的 hello、 前端連接埠組態和通訊協定 （http 或 https），並設定 hello 接聽程式。</span><span class="sxs-lookup"><span data-stu-id="8c031-216">hello following example takes hello previously configured front-end IP configuration,  front-end port configuration, and a protocol (http or https) and configures hello listener.</span></span> <span data-ttu-id="8c031-217">在此範例中，hello 接聽 tooHTTP hello 公用 IP 位址上稍早建立的連接埠 80 上的流量。</span><span class="sxs-lookup"><span data-stu-id="8c031-217">In this example, hello listener listens tooHTTP traffic on port 80 on hello public IP address that was created earlier.</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol Http -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01
```

### <a name="step-7"></a><span data-ttu-id="8c031-218">步驟 7</span><span class="sxs-lookup"><span data-stu-id="8c031-218">Step 7</span></span>

<span data-ttu-id="8c031-219">設定 URL 規則路徑 hello 後端集區。</span><span class="sxs-lookup"><span data-stu-id="8c031-219">Configure URL rule paths for hello back-end pools.</span></span> <span data-ttu-id="8c031-220">這個步驟會設定應用程式閘道所使用的 hello 相對路徑，並定義 hello hello URL 路徑與指派 toohandle hello 連入流量的 hello 後端集區之間的對應。</span><span class="sxs-lookup"><span data-stu-id="8c031-220">This step configures hello relative path used by application gateway and defines hello mapping between hello URL path and hello back-end pool that is assigned toohandle hello incoming traffic.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8c031-221">每個路徑開頭必須 / 和 hello 唯一地方"\*」 允許，則在 hello 結束。</span><span class="sxs-lookup"><span data-stu-id="8c031-221">Each path must start with / and hello only place a "\*" is allowed, is at hello end.</span></span> <span data-ttu-id="8c031-222">有效範例包括 /xyz、/xyz* 或 /xyz/*。</span><span class="sxs-lookup"><span data-stu-id="8c031-222">Valid examples are /xyz, /xyz* or /xyz/*.</span></span> <span data-ttu-id="8c031-223">hello fed toohello 路徑比對器的字串不包含任何文字 hello 之後第一次"？"或"#"，且這些字元不得使用。</span><span class="sxs-lookup"><span data-stu-id="8c031-223">hello string fed toohello path matcher does not include any text after hello first "?" or "#", and those characters are not allowed.</span></span> 

<span data-ttu-id="8c031-224">hello 下列範例會建立兩個規則： 一個用於 「 / 影像 /"路徑路由流量 tooback 端"pool1"和另一種用於 「 / 視訊 /"路徑路由流量 tooback 端"pool2。 」</span><span class="sxs-lookup"><span data-stu-id="8c031-224">hello following example creates two rules: one for "/image/" path routing traffic tooback-end "pool1" and another one for "/video/" path routing traffic tooback-end "pool2."</span></span> <span data-ttu-id="8c031-225">這些規則可確保每一組 url 的流量會路由的 toohello 後端。</span><span class="sxs-lookup"><span data-stu-id="8c031-225">These rules ensure that traffic for each set of urls is routed toohello backend.</span></span> <span data-ttu-id="8c031-226">例如，http://contoso.com/image/figure1.jpg 進入 toopool1 到 http://contoso.com/video/example.mp4 進入 toopool2。</span><span class="sxs-lookup"><span data-stu-id="8c031-226">For example, http://contoso.com/image/figure1.jpg goes toopool1 and http://contoso.com/video/example.mp4 goes toopool2.</span></span>

```powershell
$imagePathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "pathrule1" -Paths "/image/*" -BackendAddressPool $pool1 -BackendHttpSettings $poolSetting01

$videoPathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "pathrule2" -Paths "/video/*" -BackendAddressPool $pool2 -BackendHttpSettings $poolSetting02
```

<span data-ttu-id="8c031-227">如果 hello 路徑不符合任何 hello 預先定義的路徑規則，hello 規則路徑對應設定也會設定預設的後端位址集區。</span><span class="sxs-lookup"><span data-stu-id="8c031-227">If hello path doesn't match any of hello pre-defined path rules, hello rule path map configuration also configures a default back-end address pool.</span></span> <span data-ttu-id="8c031-228">比方說，http://contoso.com/shoppingcart/test.html 會 toopool1，因為它定義為 hello 預設集區不相符的流量。</span><span class="sxs-lookup"><span data-stu-id="8c031-228">For example, http://contoso.com/shoppingcart/test.html goes toopool1 as it is defined as hello default pool for unmatched traffic.</span></span>

```powershell
$urlPathMap = New-AzureRmApplicationGatewayUrlPathMapConfig -Name "urlpathmap" -PathRules $videoPathRule, $imagePathRule -DefaultBackendAddressPool $pool1 -DefaultBackendHttpSettings $poolSetting02
```

### <a name="step-8"></a><span data-ttu-id="8c031-229">步驟 8</span><span class="sxs-lookup"><span data-stu-id="8c031-229">Step 8</span></span>

<span data-ttu-id="8c031-230">建立規則設定。</span><span class="sxs-lookup"><span data-stu-id="8c031-230">Create a rule setting.</span></span> <span data-ttu-id="8c031-231">此步驟會設定 hello 應用程式閘道 toouse URL 路徑為基礎的路由。</span><span class="sxs-lookup"><span data-stu-id="8c031-231">This step configures hello application gateway toouse URL path-based routing.</span></span> <span data-ttu-id="8c031-232">hello`$urlPathMap`變數定義在 hello 先前的步驟是現在使用的 toocreate hello 路徑為基礎的規則。</span><span class="sxs-lookup"><span data-stu-id="8c031-232">hello `$urlPathMap` variable defined in hello earlier step is now used toocreate hello path-based rule.</span></span> <span data-ttu-id="8c031-233">在此步驟中，我們建立 hello 規則關聯的接聽程式與 hello 稍早建立的 url 路徑對應。</span><span class="sxs-lookup"><span data-stu-id="8c031-233">In this step, we associate hello rule with a listener and hello url path mapping created earlier.</span></span>

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule1" -RuleType PathBasedRouting -HttpListener $listener -UrlPathMap $urlPathMap
```

### <a name="step-9"></a><span data-ttu-id="8c031-234">步驟 9</span><span class="sxs-lookup"><span data-stu-id="8c031-234">Step 9</span></span>

<span data-ttu-id="8c031-235">設定 hello 數量的執行個體和 hello 應用程式閘道的大小。</span><span class="sxs-lookup"><span data-stu-id="8c031-235">Configure hello number of instances and size for hello application gateway.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "Standard_Small" -Tier Standard -Capacity 2
```

## <a name="create-application-gateway"></a><span data-ttu-id="8c031-236">建立應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="8c031-236">Create Application Gateway</span></span>

<span data-ttu-id="8c031-237">建立應用程式閘道與 hello 先前步驟中的所有組態物件。</span><span class="sxs-lookup"><span data-stu-id="8c031-237">Create an application gateway with all configuration objects from hello preceding steps.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-RG -Location "West US" -BackendAddressPools $pool1,$pool2 -BackendHttpSettingsCollection $poolSetting01, $poolSetting02 -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener -UrlPathMaps $urlPathMap -RequestRoutingRules $rule01 -Sku $sku
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="8c031-238">取得應用程式閘道 DNS 名稱</span><span class="sxs-lookup"><span data-stu-id="8c031-238">Get application gateway DNS name</span></span>

<span data-ttu-id="8c031-239">一旦建立 hello 閘道，hello 下一個步驟是 tooconfigure hello 前端進行通訊。</span><span class="sxs-lookup"><span data-stu-id="8c031-239">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="8c031-240">當使用公用 IP 時，應用程式閘道需要動態指派的 DNS 名稱 (不易記住)。</span><span class="sxs-lookup"><span data-stu-id="8c031-240">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="8c031-241">tooensure 終端使用者可以叫用 hello 應用程式閘道，CNAME 記錄可使用的 toopoint toohello 公用端點的 hello 應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="8c031-241">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="8c031-242">[在 Azure 中設定自訂網域名稱](../cloud-services/cloud-services-custom-domain-name-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="8c031-242">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="8c031-243">tooconfigure hello 前端 IP CNAME 記錄，擷取 hello 應用程式閘道和其相關聯的 IP/DNS 名稱，使用 hello PublicIPAddress 項目附加的 toohello 應用程式閘道的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="8c031-243">tooconfigure hello frontend IP CNAME record, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="8c031-244">hello 應用程式閘道的 DNS 名稱應該使用的 toocreate CNAME 記錄。</span><span class="sxs-lookup"><span data-stu-id="8c031-244">hello application gateway's DNS name should be used toocreate a CNAME record.</span></span> <span data-ttu-id="8c031-245">不建議 hello 使用 A 記錄，因為可能會在重新啟動應用程式閘道變更 hello VIP。</span><span class="sxs-lookup"><span data-stu-id="8c031-245">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="8c031-246">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8c031-246">Next steps</span></span>

<span data-ttu-id="8c031-247">如果您想的 toolearn Secure Sockets Layer (SSL) 卸載時，請參閱[設定 SSL 卸載的應用程式閘道](application-gateway-ssl-arm.md)。</span><span class="sxs-lookup"><span data-stu-id="8c031-247">If you want toolearn Secure Sockets Layer (SSL) offload, see [Configure an application gateway for SSL offload](application-gateway-ssl-arm.md).</span></span>

