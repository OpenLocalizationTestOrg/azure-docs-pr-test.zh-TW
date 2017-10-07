---
title: "應用程式來裝載多個站台閘道 aaaCreate |Microsoft 文件"
description: "本頁面提供的指示 toocreate，設定裝載多個 web 應用程式上 hello Azure 應用程式閘道相同的閘道。"
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
ms.openlocfilehash: bad9a76be0a73a7026a770630fa7156f6e5940c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-for-hosting-multiple-web-applications"></a><span data-ttu-id="8f11c-103">建立應用程式閘道來裝載多個 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="8f11c-103">Create an application gateway for hosting multiple web applications</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="8f11c-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="8f11c-104">Azure portal</span></span>](application-gateway-create-multisite-portal.md)
> * [<span data-ttu-id="8f11c-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="8f11c-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-multisite-azureresourcemanager-powershell.md)

<span data-ttu-id="8f11c-106">多個站台裝載可讓您以上一個 web 應用程式的 toodeploy hello 上相同的應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="8f11c-106">Multiple site hosting allows you toodeploy more than one web application on hello same application gateway.</span></span> <span data-ttu-id="8f11c-107">它依賴在 hello 的傳入 HTTP 要求，而 toodetermine 的接聽程式將會收到流量的主機標頭存在。</span><span class="sxs-lookup"><span data-stu-id="8f11c-107">It relies on presence of host header in hello incoming HTTP request, toodetermine which listener would receive traffic.</span></span> <span data-ttu-id="8f11c-108">hello 接聽程式，然後指示流量 tooappropriate 後端集區中的 hello 閘道 hello 規則定義的設定。</span><span class="sxs-lookup"><span data-stu-id="8f11c-108">hello listener then directs traffic tooappropriate backend pool as configured in hello rules definition of hello gateway.</span></span> <span data-ttu-id="8f11c-109">在啟用 SSL 的 web 應用程式，應用程式閘道依賴 hello 伺服器名稱指示 (SNI) 延伸模組 toochoose hello 正確接聽程式 hello 網路流量。</span><span class="sxs-lookup"><span data-stu-id="8f11c-109">In SSL enabled web applications, application gateway relies on hello Server Name Indication (SNI) extension toochoose hello correct listener for hello web traffic.</span></span> <span data-ttu-id="8f11c-110">多個站台裝載的常見用法是不同的網頁網域 toodifferent 後端伺服器集區的 tooload 平衡要求。</span><span class="sxs-lookup"><span data-stu-id="8f11c-110">A common use for multiple site hosting is tooload balance requests for different web domains toodifferent back-end server pools.</span></span> <span data-ttu-id="8f11c-111">同樣的多個相同的根網域也無法裝載在 hello 的子網域 hello 相同的應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="8f11c-111">Similarly multiple subdomains of hello same root domain could also be hosted on hello same application gateway.</span></span>

## <a name="scenario"></a><span data-ttu-id="8f11c-112">案例</span><span class="sxs-lookup"><span data-stu-id="8f11c-112">Scenario</span></span>

<span data-ttu-id="8f11c-113">在下列範例的 hello，應用程式閘道為 contoso.com 和 fabrikam.com 的流量提供兩個後端伺服器集區： contoso 伺服器集區及 fabrikam 伺服器集區。</span><span class="sxs-lookup"><span data-stu-id="8f11c-113">In hello following example, application gateway is serving traffic for contoso.com and fabrikam.com with two back-end server pools: contoso server pool and fabrikam server pool.</span></span> <span data-ttu-id="8f11c-114">類似的安裝程式可能使用的 toohost 子網域，例如 app.contoso.com 和 blog.contoso.com。</span><span class="sxs-lookup"><span data-stu-id="8f11c-114">Similar setup could be used toohost subdomains like app.contoso.com and blog.contoso.com.</span></span>

![imageURLroute](./media/application-gateway-create-multisite-azureresourcemanager-powershell/multisite.png)

## <a name="before-you-begin"></a><span data-ttu-id="8f11c-116">開始之前</span><span class="sxs-lookup"><span data-stu-id="8f11c-116">Before you begin</span></span>

1. <span data-ttu-id="8f11c-117">使用 hello Web Platform Installer 安裝 hello hello Azure PowerShell cmdlet 的最新版本。</span><span class="sxs-lookup"><span data-stu-id="8f11c-117">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="8f11c-118">您可以從下載並安裝最新版本的 hello hello **Windows PowerShell**區段 hello[下載頁面](https://azure.microsoft.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="8f11c-118">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="8f11c-119">hello 伺服器加入 toohello 後端集區 toouse hello 應用程式閘道必須存在，或其端點建立在 hello 虛擬網路中不同的子網路或公用 IP/指派的 VIP。</span><span class="sxs-lookup"><span data-stu-id="8f11c-119">hello servers added toohello back-end pool toouse hello application gateway must exist or have their endpoints created either in hello virtual network in a separate subnet or with a public IP/VIP assigned.</span></span>

## <a name="requirements"></a><span data-ttu-id="8f11c-120">需求</span><span class="sxs-lookup"><span data-stu-id="8f11c-120">Requirements</span></span>

* <span data-ttu-id="8f11c-121">**後端伺服器集區：** hello hello 後端伺服器的 IP 位址清單。</span><span class="sxs-lookup"><span data-stu-id="8f11c-121">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="8f11c-122">列出 hello IP 位址應該是屬於 toohello 虛擬網路子網路，或應該是公用 IP/VIP。</span><span class="sxs-lookup"><span data-stu-id="8f11c-122">hello IP addresses listed should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span> <span data-ttu-id="8f11c-123">您也可以使用 FQDN。</span><span class="sxs-lookup"><span data-stu-id="8f11c-123">FQDN can also be used.</span></span>
* <span data-ttu-id="8f11c-124">**後端伺服器集區設定：** 每個集區都包括一些設定，例如連接埠、通訊協定和以 Cookie 為基礎的同質性。</span><span class="sxs-lookup"><span data-stu-id="8f11c-124">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="8f11c-125">這些設定會繫結的 tooa 集區，並套用的 tooall hello 集區內的伺服器。</span><span class="sxs-lookup"><span data-stu-id="8f11c-125">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="8f11c-126">**前端連接埠：**此連接埠是開啟 hello 應用程式閘道上的 hello 公用連接埠。</span><span class="sxs-lookup"><span data-stu-id="8f11c-126">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="8f11c-127">流量叫用這個連接埠，然後再取得重新導向 tooone 的 hello 後端伺服器。</span><span class="sxs-lookup"><span data-stu-id="8f11c-127">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="8f11c-128">**接聽程式：** hello 接聽程式有前端連接埠的通訊協定 （Http 或 Https，這些值會區分大小寫），與 hello 的 SSL 憑證名稱 （如果有設定 SSL 卸載）。</span><span class="sxs-lookup"><span data-stu-id="8f11c-128">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span> <span data-ttu-id="8f11c-129">針對啟用多站台功能的應用程式閘道，會一併新增主機名稱和 SNI 指示器。</span><span class="sxs-lookup"><span data-stu-id="8f11c-129">For multi-site enabled application gateways, host name and SNI indicators are also added.</span></span>
* <span data-ttu-id="8f11c-130">**規則：** hello 規則繫結 hello 接聽程式，hello 後端伺服器集區，並定義哪一個後端伺服器集區 hello 流量應導向的 toowhen 配接器特定接聽程式。</span><span class="sxs-lookup"><span data-stu-id="8f11c-130">**Rule:** hello rule binds hello listener, hello back-end server pool, and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span> <span data-ttu-id="8f11c-131">規則會在處理 hello 排列順序，而且將會導向流量，透過 hello 比對，不論明確性比較的第一個規則。</span><span class="sxs-lookup"><span data-stu-id="8f11c-131">Rules are processed in hello order they are listed, and traffic will be directed via hello first rule that matches regardless of specificity.</span></span> <span data-ttu-id="8f11c-132">比方說，如果您有使用基本的接聽程式的規則和規則，使用多站台接聽程式同時在相同連接埠，與 hello 規則 hello hello 多站台接聽程式必須列出 hello 規則之前為 hello 多站台規則 toofunction 順序中的 hello 基本接聽程式預期的。</span><span class="sxs-lookup"><span data-stu-id="8f11c-132">For example, if you have a rule using a basic listener and a rule using a multi-site listener both on hello same port, hello rule with hello multi-site listener must be listed before hello rule with hello basic listener in order for hello multi-site rule toofunction as expected.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="8f11c-133">建立應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="8f11c-133">Create an application gateway</span></span>

<span data-ttu-id="8f11c-134">hello 以下是需要 toocreate 應用程式閘道 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="8f11c-134">hello following are hello steps needed toocreate an application gateway:</span></span>

1. <span data-ttu-id="8f11c-135">建立資源管理員的資源群組。</span><span class="sxs-lookup"><span data-stu-id="8f11c-135">Create a resource group for Resource Manager.</span></span>
2. <span data-ttu-id="8f11c-136">建立虛擬網路、 子網路和 hello 應用程式閘道的公用 IP。</span><span class="sxs-lookup"><span data-stu-id="8f11c-136">Create a virtual network, subnets, and public IP for hello application gateway.</span></span>
3. <span data-ttu-id="8f11c-137">建立應用程式閘道組態物件。</span><span class="sxs-lookup"><span data-stu-id="8f11c-137">Create an application gateway configuration object.</span></span>
4. <span data-ttu-id="8f11c-138">建立應用程式閘道資源。</span><span class="sxs-lookup"><span data-stu-id="8f11c-138">Create an application gateway resource.</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="8f11c-139">建立資源管理員的資源群組</span><span class="sxs-lookup"><span data-stu-id="8f11c-139">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="8f11c-140">請確定您使用 Azure PowerShell hello 最新版本。</span><span class="sxs-lookup"><span data-stu-id="8f11c-140">Make sure that you are using hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="8f11c-141">如需詳細資訊，可在[搭配使用 Windows PowerShell 與 Resource Manager](../powershell-azure-resource-manager.md) 取得。</span><span class="sxs-lookup"><span data-stu-id="8f11c-141">More information is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="8f11c-142">步驟 1</span><span class="sxs-lookup"><span data-stu-id="8f11c-142">Step 1</span></span>

<span data-ttu-id="8f11c-143">登入 tooAzure</span><span class="sxs-lookup"><span data-stu-id="8f11c-143">Log in tooAzure</span></span>

```powershell
Login-AzureRmAccount
```
<span data-ttu-id="8f11c-144">您必須提示的 tooauthenticate 和您的認證。</span><span class="sxs-lookup"><span data-stu-id="8f11c-144">You are prompted tooauthenticate with your credentials.</span></span>

### <a name="step-2"></a><span data-ttu-id="8f11c-145">步驟 2</span><span class="sxs-lookup"><span data-stu-id="8f11c-145">Step 2</span></span>

<span data-ttu-id="8f11c-146">請檢查 hello hello 帳戶的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="8f11c-146">Check hello subscriptions for hello account.</span></span>

```powershell
Get-AzureRmSubscription
```

### <a name="step-3"></a><span data-ttu-id="8f11c-147">步驟 3</span><span class="sxs-lookup"><span data-stu-id="8f11c-147">Step 3</span></span>

<span data-ttu-id="8f11c-148">選擇 Azure 訂用帳戶 toouse。</span><span class="sxs-lookup"><span data-stu-id="8f11c-148">Choose which of your Azure subscriptions toouse.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="8f11c-149">步驟 4</span><span class="sxs-lookup"><span data-stu-id="8f11c-149">Step 4</span></span>

<span data-ttu-id="8f11c-150">建立資源群組 (若使用現有的資源群組，請略過此步驟)。</span><span class="sxs-lookup"><span data-stu-id="8f11c-150">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-RG -location "West US"
```

<span data-ttu-id="8f11c-151">或者，您也可以針對應用程式閘道建立資源群組的標記：</span><span class="sxs-lookup"><span data-stu-id="8f11c-151">Alternatively you can also create tags for a resource group for application gateway:</span></span>

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US" -Tags @{Name = "testtag"; Value = "Application Gateway multiple site"}
```

<span data-ttu-id="8f11c-152">Azure Resource Manager 需要所有的資源群組指定一個位置。</span><span class="sxs-lookup"><span data-stu-id="8f11c-152">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="8f11c-153">此位置用於 hello 預設位置為該資源群組。</span><span class="sxs-lookup"><span data-stu-id="8f11c-153">This location is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="8f11c-154">請確定所有命令 toocreate 應用程式閘道使用 hello 相同的資源群組。</span><span class="sxs-lookup"><span data-stu-id="8f11c-154">Make sure that all commands toocreate an application gateway use hello same resource group.</span></span>

<span data-ttu-id="8f11c-155">在 hello 上述範例中，我們建立一個稱為資源群組**appgw RG**位置**美國西部**。</span><span class="sxs-lookup"><span data-stu-id="8f11c-155">In hello example above, we created a resource group called **appgw-RG** with a location of **West US**.</span></span>

> [!NOTE]
> <span data-ttu-id="8f11c-156">如果您需要 tooconfigure 自訂探查您應用程式閘道，請參閱[使用 PowerShell 建立應用程式閘道與自訂探查](application-gateway-create-probe-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="8f11c-156">If you need tooconfigure a custom probe for your application gateway, see [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md).</span></span> <span data-ttu-id="8f11c-157">請造訪[自訂探查和健全狀況監視](application-gateway-probe-overview.md)以取得詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="8f11c-157">Visit [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>

## <a name="create-a-virtual-network-and-subnets"></a><span data-ttu-id="8f11c-158">建立虛擬網路和子網路</span><span class="sxs-lookup"><span data-stu-id="8f11c-158">Create a virtual network and subnets</span></span>

<span data-ttu-id="8f11c-159">下列範例會示範如何 hello toocreate 使用資源管理員的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="8f11c-159">hello following example shows how toocreate a virtual network by using Resource Manager.</span></span> <span data-ttu-id="8f11c-160">此步驟中會建立兩個子網路。</span><span class="sxs-lookup"><span data-stu-id="8f11c-160">Two subnets are created in this step.</span></span> <span data-ttu-id="8f11c-161">hello 第一個子網路是 hello 應用程式閘道本身。</span><span class="sxs-lookup"><span data-stu-id="8f11c-161">hello first subnet is for hello application gateway itself.</span></span> <span data-ttu-id="8f11c-162">應用程式閘道需要它自己的子網路 toohold 其執行個體。</span><span class="sxs-lookup"><span data-stu-id="8f11c-162">Application gateway requires its own subnet toohold its instances.</span></span> <span data-ttu-id="8f11c-163">在該子網路中只能部署其他應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="8f11c-163">Only other application gateways can be deployed in that subnet.</span></span> <span data-ttu-id="8f11c-164">hello 第二個子網路是使用的 toohold hello 應用程式後端伺服器。</span><span class="sxs-lookup"><span data-stu-id="8f11c-164">hello second subnet is used toohold hello application backend servers.</span></span>

### <a name="step-1"></a><span data-ttu-id="8f11c-165">步驟 1</span><span class="sxs-lookup"><span data-stu-id="8f11c-165">Step 1</span></span>

<span data-ttu-id="8f11c-166">指派 hello 位址範圍 10.0.0.0/24 toohello 子網路變數 toobe 使用的 toohold hello 應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="8f11c-166">Assign hello address range 10.0.0.0/24 toohello subnet variable toobe used toohold hello application gateway.</span></span>

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name appgatewaysubnet -AddressPrefix 10.0.0.0/24
```
### <a name="step-2"></a><span data-ttu-id="8f11c-167">步驟 2</span><span class="sxs-lookup"><span data-stu-id="8f11c-167">Step 2</span></span>

<span data-ttu-id="8f11c-168">指派 hello 位址範圍 10.0.1.0/24 toohello subnet2 變數 toobe 用於 hello 後端集區。</span><span class="sxs-lookup"><span data-stu-id="8f11c-168">Assign hello address range 10.0.1.0/24 toohello subnet2 variable toobe used for hello backend pools.</span></span>

```powershell
$subnet2 = New-AzureRmVirtualNetworkSubnetConfig -Name backendsubnet -AddressPrefix 10.0.1.0/24
```

### <a name="step-3"></a><span data-ttu-id="8f11c-169">步驟 3</span><span class="sxs-lookup"><span data-stu-id="8f11c-169">Step 3</span></span>

<span data-ttu-id="8f11c-170">建立虛擬網路，名為**appgwvnet**資源群組中**appgw rg** hello 前置詞 10.0.0.0/16 使用子網路 10.0.0.0/24 hello 美國西部地區和 10.0.1.0/24。</span><span class="sxs-lookup"><span data-stu-id="8f11c-170">Create a virtual network named **appgwvnet** in resource group **appgw-rg** for hello West US region using hello prefix 10.0.0.0/16 with subnet 10.0.0.0/24, and 10.0.1.0/24.</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet,$subnet2
```

### <a name="step-4"></a><span data-ttu-id="8f11c-171">步驟 4</span><span class="sxs-lookup"><span data-stu-id="8f11c-171">Step 4</span></span>

<span data-ttu-id="8f11c-172">指派的子網路變數 hello 接下來的步驟，以建立應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="8f11c-172">Assign a subnet variable for hello next steps, which creates an application gateway.</span></span>

```powershell
$appgatewaysubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name appgatewaysubnet -VirtualNetwork $vnet
$backendsubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name backendsubnet -VirtualNetwork $vnet
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a><span data-ttu-id="8f11c-173">建立 hello 前端組態的公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="8f11c-173">Create a public IP address for hello front-end configuration</span></span>

<span data-ttu-id="8f11c-174">建立公用 IP 資源**publicIP01**資源群組中**appgw rg** hello 美國西部地區。</span><span class="sxs-lookup"><span data-stu-id="8f11c-174">Create a public IP resource **publicIP01** in resource group **appgw-rg** for hello West US region.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="8f11c-175">Hello 服務啟動時，會指派 toohello 應用程式閘道 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="8f11c-175">An IP address is assigned toohello application gateway when hello service starts.</span></span>

## <a name="create-application-gateway-configuration"></a><span data-ttu-id="8f11c-176">建立應用程式閘道組態</span><span class="sxs-lookup"><span data-stu-id="8f11c-176">Create application gateway configuration</span></span>

<span data-ttu-id="8f11c-177">您必須 tooset 所有組態項目，才能建立 hello 應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="8f11c-177">You have tooset up all configuration items before creating hello application gateway.</span></span> <span data-ttu-id="8f11c-178">hello 下列步驟建立 hello 組態項目所需的應用程式閘道資源。</span><span class="sxs-lookup"><span data-stu-id="8f11c-178">hello following steps create hello configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="8f11c-179">步驟 1</span><span class="sxs-lookup"><span data-stu-id="8f11c-179">Step 1</span></span>

<span data-ttu-id="8f11c-180">建立名為 **gatewayIP01** 的應用程式閘道 IP 組態。</span><span class="sxs-lookup"><span data-stu-id="8f11c-180">Create an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="8f11c-181">應用程式閘道啟動時，它會挑選設定 hello 子網路的 IP 位址，並傳送 hello 後端 IP 集區中的網路流量 toohello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="8f11c-181">When application gateway starts, it picks up an IP address from hello subnet configured and route network traffic toohello IP addresses in hello back-end IP pool.</span></span> <span data-ttu-id="8f11c-182">請記住，每個執行個體需要一個 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="8f11c-182">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $appgatewaysubnet
```

### <a name="step-2"></a><span data-ttu-id="8f11c-183">步驟 2</span><span class="sxs-lookup"><span data-stu-id="8f11c-183">Step 2</span></span>

<span data-ttu-id="8f11c-184">設定 hello 後端 IP 位址集區名稱為**pool01**和**pool2**與 IP 位址**134.170.185.46**， **134.170.188.221**，**134.170.185.50**如**pool1**和**134.170.186.46**， **134.170.189.221**， **134.170.186.50**如**pool2**。</span><span class="sxs-lookup"><span data-stu-id="8f11c-184">Configure hello back-end IP address pool named **pool01** and **pool2** with IP addresses **134.170.185.46**, **134.170.188.221**, **134.170.185.50** for **pool1** and **134.170.186.46**, **134.170.189.221**, **134.170.186.50** for **pool2**.</span></span>

```powershell
$pool1 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 10.0.1.100, 10.0.1.101, 10.0.1.102
$pool2 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool02 -BackendIPAddresses 10.0.1.103, 10.0.1.104, 10.0.1.105
```

<span data-ttu-id="8f11c-185">在此範例中，有兩個後端集區 tooroute 網路流量 hello 要求站台。</span><span class="sxs-lookup"><span data-stu-id="8f11c-185">In this example, there are two back-end pools tooroute network traffic based on hello requested site.</span></span> <span data-ttu-id="8f11c-186">其中一個集區會接收來自 "contoso.com" 站台的流量，而另一個集區則會接收來自 "fabrikam.com" 站台的流量。</span><span class="sxs-lookup"><span data-stu-id="8f11c-186">One pool receives traffic from site "contoso.com" and other pool receives traffic from site "fabrikam.com".</span></span> <span data-ttu-id="8f11c-187">您有上述您自己的應用程式的 IP 位址端點的 IP 位址 tooadd tooreplace hello。</span><span class="sxs-lookup"><span data-stu-id="8f11c-187">You have tooreplace hello preceding IP addresses tooadd your own application IP address endpoints.</span></span> <span data-ttu-id="8f11c-188">您也可以使用公用 IP 位址、FQDN 或 VM 的後端執行個體 NIC 來取代內部 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="8f11c-188">In place of internal IP addresses, you could also use public IP addresses, FQDN, or a VM's NIC for backend instances.</span></span> <span data-ttu-id="8f11c-189">在 PowerShell 使用的 Fqdn，而不是 Ip toospecify"-BackendFQDNs"參數。</span><span class="sxs-lookup"><span data-stu-id="8f11c-189">toospecify FQDNs instead of IPs in PowerShell use "-BackendFQDNs" parameter.</span></span>

### <a name="step-3"></a><span data-ttu-id="8f11c-190">步驟 3</span><span class="sxs-lookup"><span data-stu-id="8f11c-190">Step 3</span></span>

<span data-ttu-id="8f11c-191">設定應用程式閘道設定**poolsetting01**和**poolsetting02** hello hello 後端集區中，負載平衡網路流量。</span><span class="sxs-lookup"><span data-stu-id="8f11c-191">Configure application gateway setting **poolsetting01** and **poolsetting02** for hello load-balanced network traffic in hello back-end pool.</span></span> <span data-ttu-id="8f11c-192">在此範例中，您可以設定不同的後端集區設定 hello 後端集區。</span><span class="sxs-lookup"><span data-stu-id="8f11c-192">In this example, you configure different back-end pool settings for hello back-end pools.</span></span> <span data-ttu-id="8f11c-193">每個後端集區都可以有它自己的後端集區設定。</span><span class="sxs-lookup"><span data-stu-id="8f11c-193">Each back-end pool can have its own back-end pool setting.</span></span>

```powershell
$poolSetting01 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120
$poolSetting02 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting02" -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 240
```

### <a name="step-4"></a><span data-ttu-id="8f11c-194">步驟 4</span><span class="sxs-lookup"><span data-stu-id="8f11c-194">Step 4</span></span>

<span data-ttu-id="8f11c-195">設定公用 IP 端點 hello 前端 IP。</span><span class="sxs-lookup"><span data-stu-id="8f11c-195">Configure hello front-end IP with public IP endpoint.</span></span>

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-5"></a><span data-ttu-id="8f11c-196">步驟 5</span><span class="sxs-lookup"><span data-stu-id="8f11c-196">Step 5</span></span>

<span data-ttu-id="8f11c-197">設定應用程式閘道 hello 前端連接埠。</span><span class="sxs-lookup"><span data-stu-id="8f11c-197">Configure hello front-end port for an application gateway.</span></span>

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "fep01" -Port 443
```

### <a name="step-6"></a><span data-ttu-id="8f11c-198">步驟 6</span><span class="sxs-lookup"><span data-stu-id="8f11c-198">Step 6</span></span>

<span data-ttu-id="8f11c-199">設定兩個 SSL 憑證 hello 兩個網站，我們會在此範例中的 toosupport。</span><span class="sxs-lookup"><span data-stu-id="8f11c-199">Configure two SSL certificates for hello two websites we are going toosupport in this example.</span></span> <span data-ttu-id="8f11c-200">一個憑證是針對 contoso.com 流量，且其他 hello fabrikam.com 流量。</span><span class="sxs-lookup"><span data-stu-id="8f11c-200">One certificate is for contoso.com traffic and hello other is for fabrikam.com traffic.</span></span> <span data-ttu-id="8f11c-201">這些憑證應該是「憑證授權單位」為您的網站簽發的憑證。</span><span class="sxs-lookup"><span data-stu-id="8f11c-201">These certificates should be a Certificate Authority issued certificates for your websites.</span></span> <span data-ttu-id="8f11c-202">也支援自我簽署憑證，但不建議用於生產環境流量。</span><span class="sxs-lookup"><span data-stu-id="8f11c-202">Self-signed certificates are supported but not recommended for production traffic.</span></span>

```powershell
$cert01 = New-AzureRmApplicationGatewaySslCertificate -Name contosocert -CertificateFile <file path> -Password <password>
$cert02 = New-AzureRmApplicationGatewaySslCertificate -Name fabrikamcert -CertificateFile <file path> -Password <password>
```

### <a name="step-7"></a><span data-ttu-id="8f11c-203">步驟 7</span><span class="sxs-lookup"><span data-stu-id="8f11c-203">Step 7</span></span>

<span data-ttu-id="8f11c-204">在此範例中，設定兩個 web sites hello 的兩個接聽程式。</span><span class="sxs-lookup"><span data-stu-id="8f11c-204">Configure two listeners for hello two web sites in this example.</span></span> <span data-ttu-id="8f11c-205">此步驟會設定 hello 接聽程式，公用 IP 位址、 連接埠及主機使用 tooreceive 連入流量。</span><span class="sxs-lookup"><span data-stu-id="8f11c-205">This step configures hello listeners for public IP address, port, and host used tooreceive incoming traffic.</span></span> <span data-ttu-id="8f11c-206">HostName 參數是為了支援多個站台，而且應該設定 toohello 適當網站的 hello 接收流量。</span><span class="sxs-lookup"><span data-stu-id="8f11c-206">HostName parameter is required for multiple site support and should be set toohello appropriate website for which hello traffic is received.</span></span> <span data-ttu-id="8f11c-207">時，RequireServerNameIndication 參數應設為 tootrue 的網站若需要 ssl 的支援，在多個主機的案例。</span><span class="sxs-lookup"><span data-stu-id="8f11c-207">RequireServerNameIndication parameter should be set tootrue for websites that need support for SSL in a multiple host scenario.</span></span> <span data-ttu-id="8f11c-208">如果需要 SSL 支援，您也需要 toospecify hello SSL 憑證也就是該 web 應用程式使用的 toosecure 流量。</span><span class="sxs-lookup"><span data-stu-id="8f11c-208">If SSL support is required, you also need toospecify hello SSL certificate that is used toosecure traffic for that web application.</span></span> <span data-ttu-id="8f11c-209">FrontendIPConfiguration FrontendPort 及主機名稱的 hello 組合必須是唯一 tooa 接聽程式。</span><span class="sxs-lookup"><span data-stu-id="8f11c-209">hello combination of FrontendIPConfiguration, FrontendPort, and HostName must be unique tooa listener.</span></span> <span data-ttu-id="8f11c-210">每個接聽程式可以支援一個憑證。</span><span class="sxs-lookup"><span data-stu-id="8f11c-210">Each listener can support one certificate.</span></span>

```powershell
$listener01 = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol Https -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -HostName "contoso11.com" -RequireServerNameIndication true  -SslCertificate $cert01
$listener02 = New-AzureRmApplicationGatewayHttpListener -Name "listener02" -Protocol Https -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -HostName "fabrikam11.com" -RequireServerNameIndication true -SslCertificate $cert02
```

### <a name="step-8"></a><span data-ttu-id="8f11c-211">步驟 8</span><span class="sxs-lookup"><span data-stu-id="8f11c-211">Step 8</span></span>

<span data-ttu-id="8f11c-212">建立兩個設定 hello 兩個 web 應用程式在此範例中的規則。</span><span class="sxs-lookup"><span data-stu-id="8f11c-212">Create two rule setting for hello two web applications in this example.</span></span> <span data-ttu-id="8f11c-213">規則會將接聽程式、後端集區及 http 設定繫結在一起。</span><span class="sxs-lookup"><span data-stu-id="8f11c-213">A rule ties together listeners, backend pools and http settings.</span></span> <span data-ttu-id="8f11c-214">此步驟會設定 hello 應用程式閘道 toouse 基本路由規則，一個用於每個網站。</span><span class="sxs-lookup"><span data-stu-id="8f11c-214">This step configures hello application gateway toouse Basic routing rule, one for each website.</span></span> <span data-ttu-id="8f11c-215">流量 tooeach 網站接收其設定的接聽程式，並接著會導向 tooits 設定後端集區，使用 hello hello BackendHttpSettings 中指定的屬性。</span><span class="sxs-lookup"><span data-stu-id="8f11c-215">Traffic tooeach website is received by its configured listener, and is then directed tooits configured backend pool, using hello properties specified in hello BackendHttpSettings.</span></span>

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule01" -RuleType Basic -HttpListener $listener01 -BackendHttpSettings $poolSetting01 -BackendAddressPool $pool1
$rule02 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule02" -RuleType Basic -HttpListener $listener02 -BackendHttpSettings $poolSetting02 -BackendAddressPool $pool2
```

### <a name="step-9"></a><span data-ttu-id="8f11c-216">步驟 9</span><span class="sxs-lookup"><span data-stu-id="8f11c-216">Step 9</span></span>

<span data-ttu-id="8f11c-217">設定 hello 數量的執行個體和 hello 應用程式閘道的大小。</span><span class="sxs-lookup"><span data-stu-id="8f11c-217">Configure hello number of instances and size for hello application gateway.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "Standard_Medium" -Tier Standard -Capacity 2
```

## <a name="create-application-gateway"></a><span data-ttu-id="8f11c-218">建立應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="8f11c-218">Create application gateway</span></span>

<span data-ttu-id="8f11c-219">建立應用程式閘道與 hello 先前步驟中的所有組態物件。</span><span class="sxs-lookup"><span data-stu-id="8f11c-219">Create an application gateway with all configuration objects from hello preceding steps.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-RG -Location "West US" -BackendAddressPools $pool1,$pool2 -BackendHttpSettingsCollection $poolSetting01, $poolSetting02 -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener01, $listener02 -RequestRoutingRules $rule01, $rule02 -Sku $sku -SslCertificates $cert01, $cert02
```

> [!IMPORTANT]
> <span data-ttu-id="8f11c-220">應用程式閘道的佈建是長時間執行的作業，而且可能需要一些時間 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="8f11c-220">Application Gateway provisioning is a long running operation and may take some time toocomplete.</span></span>
> 
> 

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="8f11c-221">取得應用程式閘道 DNS 名稱</span><span class="sxs-lookup"><span data-stu-id="8f11c-221">Get application gateway DNS name</span></span>

<span data-ttu-id="8f11c-222">一旦建立 hello 閘道，hello 下一個步驟是 tooconfigure hello 前端進行通訊。</span><span class="sxs-lookup"><span data-stu-id="8f11c-222">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="8f11c-223">當使用公用 IP 時，應用程式閘道需要動態指派的 DNS 名稱 (不易記住)。</span><span class="sxs-lookup"><span data-stu-id="8f11c-223">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="8f11c-224">tooensure 終端使用者可以叫用 hello 應用程式閘道，CNAME 記錄可使用的 toopoint toohello 公用端點的 hello 應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="8f11c-224">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="8f11c-225">[在 Azure 中設定自訂網域名稱](../cloud-services/cloud-services-custom-domain-name-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="8f11c-225">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="8f11c-226">toodo hello 應用程式閘道及其相關聯的 IP/DNS 名稱，使用 hello PublicIPAddress 項目附加的 toohello 應用程式閘道的這個，擷取詳細資料。</span><span class="sxs-lookup"><span data-stu-id="8f11c-226">toodo this, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="8f11c-227">hello 應用程式閘道的 DNS 名稱應該使用的 toocreate CNAME 記錄，哪個點 hello 兩個 web 應用程式 toothis DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="8f11c-227">hello application gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="8f11c-228">不建議 hello 使用 A 記錄，因為可能會在重新啟動應用程式閘道變更 hello VIP。</span><span class="sxs-lookup"><span data-stu-id="8f11c-228">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="8f11c-229">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8f11c-229">Next steps</span></span>

<span data-ttu-id="8f11c-230">深入了解如何 tooprotect 與網站[應用程式閘道的 Web 應用程式防火牆](application-gateway-webapplicationfirewall-overview.md)</span><span class="sxs-lookup"><span data-stu-id="8f11c-230">Learn how tooprotect your websites with [Application Gateway - Web Application Firewall](application-gateway-webapplicationfirewall-overview.md)</span></span>

