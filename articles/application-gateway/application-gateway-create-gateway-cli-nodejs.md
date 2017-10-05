---
title: "建立 Azure 應用程式閘道 - Azure CLI 1.0 | Microsoft Docs"
description: "了解如何使用 Resource Manager 中的 Azure CLI 1.0 建立應用程式閘道"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c2f6516e-3805-49ac-826e-776b909a9104
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: e7b16e789e0f241aa8ca2292aacb2bccde8777ee
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-application-gateway-by-using-the-azure-cli"></a><span data-ttu-id="e25f9-103">使用 Azure CLI 建立應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="e25f9-103">Create an application gateway by using the Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e25f9-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="e25f9-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="e25f9-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="e25f9-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="e25f9-106">Azure 傳統 PowerShell</span><span class="sxs-lookup"><span data-stu-id="e25f9-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="e25f9-107">Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="e25f9-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="e25f9-108">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="e25f9-108">Azure CLI 1.0</span></span>](application-gateway-create-gateway-cli.md)
> * [<span data-ttu-id="e25f9-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="e25f9-109">Azure CLI 2.0</span></span>](application-gateway-create-gateway-cli.md)
> 
> 

<span data-ttu-id="e25f9-110">Azure 應用程式閘道是第 7 層負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="e25f9-110">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="e25f9-111">不論是在雲端或內部部署中，此閘道均提供在不同伺服器之間進行容錯移轉及效能路由傳送 HTTP 要求。</span><span class="sxs-lookup"><span data-stu-id="e25f9-111">It provides failover, performance-routing HTTP requests between different servers, whether they are on the cloud or on-premises.</span></span> <span data-ttu-id="e25f9-112">應用程式閘道具有下列應用程式傳遞功能：HTTP 負載平衡、以 Cookie 為基礎的工作階段同質性、「安全通訊端層」(SSL) 卸載、自訂健康狀態探查，以及多站台支援。</span><span class="sxs-lookup"><span data-stu-id="e25f9-112">Application gateway has the following application delivery features: HTTP load balancing, cookie-based session affinity, and Secure Sockets Layer (SSL) offload, custom health probes, and support for multi-site.</span></span>

## <a name="prerequisite-install-the-azure-cli"></a><span data-ttu-id="e25f9-113">必要條件：安裝 Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e25f9-113">Prerequisite: Install the Azure CLI</span></span>

<span data-ttu-id="e25f9-114">若要執行本文的步驟，您需要[安裝適用於 Mac、Linux 和 Windows 的 Azure 命令列介面 (Azure CLI)](../xplat-cli-install.md)，而且需要[登入 Azure](../xplat-cli-connect.md)。</span><span class="sxs-lookup"><span data-stu-id="e25f9-114">To perform the steps in this article, you need to [install the Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](../xplat-cli-install.md) and you need to [log on to Azure](../xplat-cli-connect.md).</span></span> 

> [!NOTE]
> <span data-ttu-id="e25f9-115">如果您沒有 Azure 帳戶，就需要申請一個。</span><span class="sxs-lookup"><span data-stu-id="e25f9-115">If you don't have an Azure account, you need one.</span></span> <span data-ttu-id="e25f9-116">請 [在此處註冊免費試用](../active-directory/sign-up-organization.md)。</span><span class="sxs-lookup"><span data-stu-id="e25f9-116">Go sign up for a [free trial here](../active-directory/sign-up-organization.md).</span></span>

## <a name="scenario"></a><span data-ttu-id="e25f9-117">案例</span><span class="sxs-lookup"><span data-stu-id="e25f9-117">Scenario</span></span>

<span data-ttu-id="e25f9-118">在此案例中，您將了解如何使用 Azure 入口網站來建立應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="e25f9-118">In this scenario, you learn how to create an application gateway using the Azure portal.</span></span>

<span data-ttu-id="e25f9-119">此案例將會：</span><span class="sxs-lookup"><span data-stu-id="e25f9-119">This scenario will:</span></span>

* <span data-ttu-id="e25f9-120">建立含有兩個執行個體的中型應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="e25f9-120">Create a medium application gateway with two instances.</span></span>
* <span data-ttu-id="e25f9-121">建立名為 ContosoVNET 且含有 10.0.0.0/16 保留 CIDR 區塊的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="e25f9-121">Create a virtual network named ContosoVNET with a reserved CIDR block of 10.0.0.0/16.</span></span>
* <span data-ttu-id="e25f9-122">建立名為 subnet01 且使用 10.0.0.0/28 作為其 CIDR 區塊的子網路。</span><span class="sxs-lookup"><span data-stu-id="e25f9-122">Create a subnet called subnet01 that uses 10.0.0.0/28 as its CIDR block.</span></span>

> [!NOTE]
> <span data-ttu-id="e25f9-123">其他應用程式閘道組態 (包括自訂健康狀況探查、後端集區位址及其他規則) 會在設定應用程式閘道設定之後才進行設定，而不會在初始部署期間設定。</span><span class="sxs-lookup"><span data-stu-id="e25f9-123">Additional configuration of the application gateway, including custom health probes, backend pool addresses, and additional rules are configured after the application gateway is configured and not during initial deployment.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="e25f9-124">開始之前</span><span class="sxs-lookup"><span data-stu-id="e25f9-124">Before you begin</span></span>

<span data-ttu-id="e25f9-125">「Azure 應用程式閘道」需要有自己的子網路。</span><span class="sxs-lookup"><span data-stu-id="e25f9-125">Azure Application Gateway requires its own subnet.</span></span> <span data-ttu-id="e25f9-126">建立虛擬網路時，請確定您保留足夠的位址空間，以便擁有多個子網路。</span><span class="sxs-lookup"><span data-stu-id="e25f9-126">When creating a virtual network, ensure that you leave enough address space to have multiple subnets.</span></span> <span data-ttu-id="e25f9-127">將應用程式閘道部署到子網路之後，就只能將額外的應用程式閘道新增到該子網路。</span><span class="sxs-lookup"><span data-stu-id="e25f9-127">Once you deploy an application gateway to a subnet, only additional application gateways are able to be added to the subnet.</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="e25f9-128">登入 Azure</span><span class="sxs-lookup"><span data-stu-id="e25f9-128">Log in to Azure</span></span>

<span data-ttu-id="e25f9-129">開啟 [Microsoft Azure 命令提示字元] 並登入。</span><span class="sxs-lookup"><span data-stu-id="e25f9-129">Open the **Microsoft Azure Command Prompt**, and log in.</span></span> 

```azurecli-interactive
azure login
```

<span data-ttu-id="e25f9-130">輸入上述範例後會提供程式碼。</span><span class="sxs-lookup"><span data-stu-id="e25f9-130">Once you type the preceding example, a code is provided.</span></span> <span data-ttu-id="e25f9-131">在瀏覽器中瀏覽至 https://aka.ms/devicelogin 以繼續登入程序。</span><span class="sxs-lookup"><span data-stu-id="e25f9-131">Navigate to https://aka.ms/devicelogin in a browser to continue the login process.</span></span>

![顯示裝置登入的 cmd][1]

<span data-ttu-id="e25f9-133">在瀏覽器中，輸入收到的程式碼。</span><span class="sxs-lookup"><span data-stu-id="e25f9-133">In the browser, enter the code you received.</span></span> <span data-ttu-id="e25f9-134">系統會將您重新導向至 [登入] 頁面。</span><span class="sxs-lookup"><span data-stu-id="e25f9-134">You are redirected to a sign-in page.</span></span>

![要輸入程式碼的瀏覽器][2]

<span data-ttu-id="e25f9-136">輸入程式碼後您已登入，請關閉瀏覽器以繼續進行案例。</span><span class="sxs-lookup"><span data-stu-id="e25f9-136">Once the code has been entered you are signed in, close the browser to continue on with the scenario.</span></span>

![已順利登入][3]

## <a name="switch-to-resource-manager-mode"></a><span data-ttu-id="e25f9-138">切換至 Resource Manager 模式</span><span class="sxs-lookup"><span data-stu-id="e25f9-138">Switch to Resource Manager Mode</span></span>

```azurecli-interactive
azure config mode arm
```

## <a name="create-the-resource-group"></a><span data-ttu-id="e25f9-139">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="e25f9-139">Create the resource group</span></span>

<span data-ttu-id="e25f9-140">建立應用程式閘道之前，會建立資源群組以包含應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="e25f9-140">Before creating the application gateway, a resource group is created to contain the application gateway.</span></span> <span data-ttu-id="e25f9-141">以下顯示命令。</span><span class="sxs-lookup"><span data-stu-id="e25f9-141">The following shows the command.</span></span>

```azurecli-interactive
azure group create \
--name ContosoRG \
--location eastus
```

## <a name="create-a-virtual-network"></a><span data-ttu-id="e25f9-142">建立虛擬網路</span><span class="sxs-lookup"><span data-stu-id="e25f9-142">Create a virtual network</span></span>

<span data-ttu-id="e25f9-143">建立資源群組後，就會為應用程式閘道建立虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="e25f9-143">Once the resource group is created, a virtual network is created for the application gateway.</span></span>  <span data-ttu-id="e25f9-144">在下列範例中，位址空間為上述案例注意事項中所定義的 10.0.0.0/16。</span><span class="sxs-lookup"><span data-stu-id="e25f9-144">In the following example, the address space was as 10.0.0.0/16 as defined in the preceding scenario notes.</span></span>

```azurecli-interactive
azure network vnet create \
--name ContosoVNET \
--address-prefixes 10.0.0.0/16 \
--resource-group ContosoRG \
--location eastus
```

## <a name="create-a-subnet"></a><span data-ttu-id="e25f9-145">建立子網路</span><span class="sxs-lookup"><span data-stu-id="e25f9-145">Create a subnet</span></span>

<span data-ttu-id="e25f9-146">建立虛擬網路之後，就會為應用程式閘道新增子網路。</span><span class="sxs-lookup"><span data-stu-id="e25f9-146">After the virtual network is created, a subnet is added for the application gateway.</span></span>  <span data-ttu-id="e25f9-147">如果您打算使用應用程式閘道搭配與其裝載於相同虛擬網路中的 Web 應用程式，請務必保留足夠的空間給另一個子網路使用。</span><span class="sxs-lookup"><span data-stu-id="e25f9-147">If you plan to use application gateway with a web app hosted in the same virtual network as the application gateway, be sure to leave enough room for another subnet.</span></span>

```azurecli-interactive
azure network vnet subnet create \
--resource-group ContosoRG \
--name subnet01 \
--vnet-name ContosoVNET \
--address-prefix 10.0.0.0/28 
```

## <a name="create-the-application-gateway"></a><span data-ttu-id="e25f9-148">建立應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="e25f9-148">Create the application gateway</span></span>

<span data-ttu-id="e25f9-149">建立虛擬網路和子網路後，便已完成應用程式閘道的先決條件。</span><span class="sxs-lookup"><span data-stu-id="e25f9-149">Once the virtual network and subnet are created, the pre-requisites for the application gateway are complete.</span></span> <span data-ttu-id="e25f9-150">此外下列步驟也需要先前匯出的 .pfx 憑證和憑證密碼︰用於後端的 IP 位址是後端伺服器的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="e25f9-150">Additionally a previously exported .pfx certificate and the password for the certificate are required for the following step: The IP addresses used for the backend are the IP addresses for your backend server.</span></span> <span data-ttu-id="e25f9-151">這些值可以是虛擬網路中的私人 IP、公用 IP 或後端伺服器的完整網域名稱。</span><span class="sxs-lookup"><span data-stu-id="e25f9-151">These values can be either private IPs in the virtual network, public ips, or fully qualified domain names for your backend servers.</span></span>

```azurecli-interactive
azure network application-gateway create \
--name AdatumAppGateway \
--location eastus \
--resource-group ContosoRG \
--vnet-name ContosoVNET \
--subnet-name subnet01 \
--servers 134.170.185.46,134.170.188.221,134.170.185.50 \
--capacity 2 \
--sku-tier Standard \
--routing-rule-type Basic \
--frontend-port 80 \
--http-settings-cookie-based-affinity Enabled \
--http-settings-port 80 \
--http-settings-protocol http \
--frontend-port http \
--sku-name Standard_Medium
```

> [!NOTE]
> <span data-ttu-id="e25f9-152">如需可在建立期間提供的參數清單，請執行下列命令︰**azure network application-gateway create --help**。</span><span class="sxs-lookup"><span data-stu-id="e25f9-152">For a list of parameters that can be provided during creation run the following command: **azure network application-gateway create --help**.</span></span>

<span data-ttu-id="e25f9-153">此範例會建立一個具有接聽程式、後端集區、後端 http 設定及規則之預設設定的基本應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="e25f9-153">This example creates a basic application gateway with default settings for the listener, backend pool, backend http settings, and rules.</span></span> <span data-ttu-id="e25f9-154">佈建成功之後，您可以依據您的部署需求修改這些設定。</span><span class="sxs-lookup"><span data-stu-id="e25f9-154">You can modify these settings to suit your deployment once the provisioning is successful.</span></span>
<span data-ttu-id="e25f9-155">如果在先前步驟中已經以後端集區定義 Web 應用程式，一旦建立之後，負載平衡即開始。</span><span class="sxs-lookup"><span data-stu-id="e25f9-155">If you already have your web application defined with the backend pool in the preceding steps, once created, load balancing begins.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e25f9-156">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e25f9-156">Next steps</span></span>

<span data-ttu-id="e25f9-157">參閱 [建立自訂健康狀態探查](application-gateway-create-probe-portal.md)</span><span class="sxs-lookup"><span data-stu-id="e25f9-157">Learn how to create custom health probes by visiting [Create a custom health probe](application-gateway-create-probe-portal.md)</span></span>

<span data-ttu-id="e25f9-158">參閱 [設定 SSL 卸載](application-gateway-ssl-arm.md)</span><span class="sxs-lookup"><span data-stu-id="e25f9-158">Learn how to configure SSL Offloading and take the costly SSL decryption off your web servers by visiting [Configure SSL Offload](application-gateway-ssl-arm.md)</span></span>

<!--Image references-->

[scenario]: ./media/application-gateway-create-gateway-cli-nodejs/scenario.png
[1]: ./media/application-gateway-create-gateway-cli-nodejs/figure1.png
[2]: ./media/application-gateway-create-gateway-cli-nodejs/figure2.png
[3]: ./media/application-gateway-create-gateway-cli-nodejs/figure3.png
