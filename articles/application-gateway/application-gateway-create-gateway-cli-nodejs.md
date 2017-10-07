---
title: "aaaCreate Azure 應用程式閘道-Azure CLI 1.0 |Microsoft 文件"
description: "了解如何使用應用程式閘道 toocreate hello Azure CLI 1.0 資源管理員 中"
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
ms.openlocfilehash: 3c0d2d96b6be404d0372d00f0deb2a32959ca419
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-by-using-hello-azure-cli"></a><span data-ttu-id="eec0c-103">使用 Azure CLI hello 建立應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="eec0c-103">Create an application gateway by using hello Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="eec0c-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="eec0c-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="eec0c-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="eec0c-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="eec0c-106">Azure 傳統 PowerShell</span><span class="sxs-lookup"><span data-stu-id="eec0c-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="eec0c-107">Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="eec0c-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="eec0c-108">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="eec0c-108">Azure CLI 1.0</span></span>](application-gateway-create-gateway-cli.md)
> * [<span data-ttu-id="eec0c-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="eec0c-109">Azure CLI 2.0</span></span>](application-gateway-create-gateway-cli.md)
> 
> 

<span data-ttu-id="eec0c-110">Azure 應用程式閘道是第 7 層負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="eec0c-110">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="eec0c-111">無論是在 hello 雲端或內部部署上，它會提供容錯移轉時，效能路由不同的伺服器之間的 HTTP 要求。</span><span class="sxs-lookup"><span data-stu-id="eec0c-111">It provides failover, performance-routing HTTP requests between different servers, whether they are on hello cloud or on-premises.</span></span> <span data-ttu-id="eec0c-112">應用程式閘道有下列應用程式傳遞功能的 hello: HTTP 負載平衡、 cookie 架構工作階段親和性，以及安全通訊端層 (SSL) 卸載自訂健全狀況探查，以及支援多站台。</span><span class="sxs-lookup"><span data-stu-id="eec0c-112">Application gateway has hello following application delivery features: HTTP load balancing, cookie-based session affinity, and Secure Sockets Layer (SSL) offload, custom health probes, and support for multi-site.</span></span>

## <a name="prerequisite-install-hello-azure-cli"></a><span data-ttu-id="eec0c-113">必要條件： 安裝 hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="eec0c-113">Prerequisite: Install hello Azure CLI</span></span>

<span data-ttu-id="eec0c-114">tooperform hello 步驟在本文中，您需要[hello Azure 命令列介面安裝的 Mac、 Linux 及 Windows (Azure CLI)](../xplat-cli-install.md) ，而且您需要太[登入 tooAzure](../xplat-cli-connect.md)。</span><span class="sxs-lookup"><span data-stu-id="eec0c-114">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](../xplat-cli-install.md) and you need too[log on tooAzure](../xplat-cli-connect.md).</span></span> 

> [!NOTE]
> <span data-ttu-id="eec0c-115">如果您沒有 Azure 帳戶，就需要申請一個。</span><span class="sxs-lookup"><span data-stu-id="eec0c-115">If you don't have an Azure account, you need one.</span></span> <span data-ttu-id="eec0c-116">請 [在此處註冊免費試用](../active-directory/sign-up-organization.md)。</span><span class="sxs-lookup"><span data-stu-id="eec0c-116">Go sign up for a [free trial here](../active-directory/sign-up-organization.md).</span></span>

## <a name="scenario"></a><span data-ttu-id="eec0c-117">案例</span><span class="sxs-lookup"><span data-stu-id="eec0c-117">Scenario</span></span>

<span data-ttu-id="eec0c-118">在此案例中，您學會如何應用程式閘道使用 toocreate hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="eec0c-118">In this scenario, you learn how toocreate an application gateway using hello Azure portal.</span></span>

<span data-ttu-id="eec0c-119">此案例將會：</span><span class="sxs-lookup"><span data-stu-id="eec0c-119">This scenario will:</span></span>

* <span data-ttu-id="eec0c-120">建立含有兩個執行個體的中型應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="eec0c-120">Create a medium application gateway with two instances.</span></span>
* <span data-ttu-id="eec0c-121">建立名為 ContosoVNET 且含有 10.0.0.0/16 保留 CIDR 區塊的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="eec0c-121">Create a virtual network named ContosoVNET with a reserved CIDR block of 10.0.0.0/16.</span></span>
* <span data-ttu-id="eec0c-122">建立名為 subnet01 且使用 10.0.0.0/28 作為其 CIDR 區塊的子網路。</span><span class="sxs-lookup"><span data-stu-id="eec0c-122">Create a subnet called subnet01 that uses 10.0.0.0/28 as its CIDR block.</span></span>

> [!NOTE]
> <span data-ttu-id="eec0c-123">額外設定 hello 應用程式閘道，包括自訂健全狀況探查，hello 應用程式閘道設定之後，而不會在初始部署設定後端集區位址，以及其他規則。</span><span class="sxs-lookup"><span data-stu-id="eec0c-123">Additional configuration of hello application gateway, including custom health probes, backend pool addresses, and additional rules are configured after hello application gateway is configured and not during initial deployment.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="eec0c-124">開始之前</span><span class="sxs-lookup"><span data-stu-id="eec0c-124">Before you begin</span></span>

<span data-ttu-id="eec0c-125">「Azure 應用程式閘道」需要有自己的子網路。</span><span class="sxs-lookup"><span data-stu-id="eec0c-125">Azure Application Gateway requires its own subnet.</span></span> <span data-ttu-id="eec0c-126">當建立虛擬網路，請確定您保留足夠的位址空間 toohave 多個子網路。</span><span class="sxs-lookup"><span data-stu-id="eec0c-126">When creating a virtual network, ensure that you leave enough address space toohave multiple subnets.</span></span> <span data-ttu-id="eec0c-127">一旦您部署應用程式閘道 tooa 子網路時，唯一的額外應用程式閘道就能 toobe 加入 toohello 子網路。</span><span class="sxs-lookup"><span data-stu-id="eec0c-127">Once you deploy an application gateway tooa subnet, only additional application gateways are able toobe added toohello subnet.</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="eec0c-128">登入 tooAzure</span><span class="sxs-lookup"><span data-stu-id="eec0c-128">Log in tooAzure</span></span>

<span data-ttu-id="eec0c-129">開啟 hello **Microsoft Azure 命令提示字元**，並登入。</span><span class="sxs-lookup"><span data-stu-id="eec0c-129">Open hello **Microsoft Azure Command Prompt**, and log in.</span></span> 

```azurecli-interactive
azure login
```

<span data-ttu-id="eec0c-130">一旦您輸入 hello 前面範例中，將程式碼。</span><span class="sxs-lookup"><span data-stu-id="eec0c-130">Once you type hello preceding example, a code is provided.</span></span> <span data-ttu-id="eec0c-131">瀏覽 toohttps://aka.ms/devicelogin 瀏覽器 toocontinue hello 登入處理序。</span><span class="sxs-lookup"><span data-stu-id="eec0c-131">Navigate toohttps://aka.ms/devicelogin in a browser toocontinue hello login process.</span></span>

![顯示裝置登入的 cmd][1]

<span data-ttu-id="eec0c-133">在 hello 瀏覽器中，輸入您收到 hello 程式碼。</span><span class="sxs-lookup"><span data-stu-id="eec0c-133">In hello browser, enter hello code you received.</span></span> <span data-ttu-id="eec0c-134">您已重新導向的 tooa 登入頁面。</span><span class="sxs-lookup"><span data-stu-id="eec0c-134">You are redirected tooa sign-in page.</span></span>

![瀏覽器 tooenter 程式碼][2]

<span data-ttu-id="eec0c-136">一旦輸入 hello 程式碼後您登入，關閉 hello 瀏覽器 toocontinue 與 hello 案例。</span><span class="sxs-lookup"><span data-stu-id="eec0c-136">Once hello code has been entered you are signed in, close hello browser toocontinue on with hello scenario.</span></span>

![已順利登入][3]

## <a name="switch-tooresource-manager-mode"></a><span data-ttu-id="eec0c-138">切換 tooResource 管理員模式</span><span class="sxs-lookup"><span data-stu-id="eec0c-138">Switch tooResource Manager Mode</span></span>

```azurecli-interactive
azure config mode arm
```

## <a name="create-hello-resource-group"></a><span data-ttu-id="eec0c-139">建立 hello 資源群組</span><span class="sxs-lookup"><span data-stu-id="eec0c-139">Create hello resource group</span></span>

<span data-ttu-id="eec0c-140">建立 hello 應用程式閘道之前, 建立 toocontain hello 應用程式閘道資源群組。</span><span class="sxs-lookup"><span data-stu-id="eec0c-140">Before creating hello application gateway, a resource group is created toocontain hello application gateway.</span></span> <span data-ttu-id="eec0c-141">hello 下列範例示範 hello 命令。</span><span class="sxs-lookup"><span data-stu-id="eec0c-141">hello following shows hello command.</span></span>

```azurecli-interactive
azure group create \
--name ContosoRG \
--location eastus
```

## <a name="create-a-virtual-network"></a><span data-ttu-id="eec0c-142">建立虛擬網路</span><span class="sxs-lookup"><span data-stu-id="eec0c-142">Create a virtual network</span></span>

<span data-ttu-id="eec0c-143">一旦建立 hello 資源群組時，虛擬網路被建立 hello 應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="eec0c-143">Once hello resource group is created, a virtual network is created for hello application gateway.</span></span>  <span data-ttu-id="eec0c-144">在下列範例的 hello，hello 位址空間是為 10.0.0.0/16 hello 上述案例附註中定義。</span><span class="sxs-lookup"><span data-stu-id="eec0c-144">In hello following example, hello address space was as 10.0.0.0/16 as defined in hello preceding scenario notes.</span></span>

```azurecli-interactive
azure network vnet create \
--name ContosoVNET \
--address-prefixes 10.0.0.0/16 \
--resource-group ContosoRG \
--location eastus
```

## <a name="create-a-subnet"></a><span data-ttu-id="eec0c-145">建立子網路</span><span class="sxs-lookup"><span data-stu-id="eec0c-145">Create a subnet</span></span>

<span data-ttu-id="eec0c-146">Hello 虛擬網路建立之後，會將子網路加入 hello 應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="eec0c-146">After hello virtual network is created, a subnet is added for hello application gateway.</span></span>  <span data-ttu-id="eec0c-147">如果您計劃 toouse 應用程式閘道與 web 應用程式裝載於 hello 相同虛擬網路與 hello 應用程式閘道，可確定 tooleave 足夠空間供另一個子網路。</span><span class="sxs-lookup"><span data-stu-id="eec0c-147">If you plan toouse application gateway with a web app hosted in hello same virtual network as hello application gateway, be sure tooleave enough room for another subnet.</span></span>

```azurecli-interactive
azure network vnet subnet create \
--resource-group ContosoRG \
--name subnet01 \
--vnet-name ContosoVNET \
--address-prefix 10.0.0.0/28 
```

## <a name="create-hello-application-gateway"></a><span data-ttu-id="eec0c-148">建立 hello 應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="eec0c-148">Create hello application gateway</span></span>

<span data-ttu-id="eec0c-149">一旦建立 hello 虛擬網路和子網路，hello hello 應用程式閘道的必要元件都已完成。</span><span class="sxs-lookup"><span data-stu-id="eec0c-149">Once hello virtual network and subnet are created, hello pre-requisites for hello application gateway are complete.</span></span> <span data-ttu-id="eec0c-150">此外還需要下列步驟的 hello hello 憑證的先前匯出的.pfx 憑證和 hello 密碼： hello 用於 hello 後端的 IP 位址是 hello 的後端伺服器的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="eec0c-150">Additionally a previously exported .pfx certificate and hello password for hello certificate are required for hello following step: hello IP addresses used for hello backend are hello IP addresses for your backend server.</span></span> <span data-ttu-id="eec0c-151">這些值可以是任一個私用 Ip hello 虛擬網路、 公用 ip 時或針對後端伺服器的完整的網域名稱。</span><span class="sxs-lookup"><span data-stu-id="eec0c-151">These values can be either private IPs in hello virtual network, public ips, or fully qualified domain names for your backend servers.</span></span>

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
> <span data-ttu-id="eec0c-152">如需清單，可以執行下列命令的 hello 建立期間提供的參數： **azure 網路的應用程式閘道建立-協助**。</span><span class="sxs-lookup"><span data-stu-id="eec0c-152">For a list of parameters that can be provided during creation run hello following command: **azure network application-gateway create --help**.</span></span>

<span data-ttu-id="eec0c-153">這個範例會建立基本應用程式閘道 hello 接聽程式、 後端集區、 後端 http 設定和規則的預設設定。</span><span class="sxs-lookup"><span data-stu-id="eec0c-153">This example creates a basic application gateway with default settings for hello listener, backend pool, backend http settings, and rules.</span></span> <span data-ttu-id="eec0c-154">可以修改這些設定 toosuit 部署一旦 hello 佈建成功。</span><span class="sxs-lookup"><span data-stu-id="eec0c-154">You can modify these settings toosuit your deployment once hello provisioning is successful.</span></span>
<span data-ttu-id="eec0c-155">如果您已經使用在先前步驟中，一旦建立，hello hello 後端集區定義的 web 應用程式負載平衡開始。</span><span class="sxs-lookup"><span data-stu-id="eec0c-155">If you already have your web application defined with hello backend pool in hello preceding steps, once created, load balancing begins.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eec0c-156">後續步驟</span><span class="sxs-lookup"><span data-stu-id="eec0c-156">Next steps</span></span>

<span data-ttu-id="eec0c-157">了解如何 toocreate 自訂健全狀況探查造訪[建立自訂的健全狀況探查](application-gateway-create-probe-portal.md)</span><span class="sxs-lookup"><span data-stu-id="eec0c-157">Learn how toocreate custom health probes by visiting [Create a custom health probe](application-gateway-create-probe-portal.md)</span></span>

<span data-ttu-id="eec0c-158">了解如何 tooconfigure SSL 卸載且採用 hello 昂貴 SSL 解密關閉您的 web 伺服器造訪[設定 SSL 卸載](application-gateway-ssl-arm.md)</span><span class="sxs-lookup"><span data-stu-id="eec0c-158">Learn how tooconfigure SSL Offloading and take hello costly SSL decryption off your web servers by visiting [Configure SSL Offload](application-gateway-ssl-arm.md)</span></span>

<!--Image references-->

[scenario]: ./media/application-gateway-create-gateway-cli-nodejs/scenario.png
[1]: ./media/application-gateway-create-gateway-cli-nodejs/figure1.png
[2]: ./media/application-gateway-create-gateway-cli-nodejs/figure2.png
[3]: ./media/application-gateway-create-gateway-cli-nodejs/figure3.png
