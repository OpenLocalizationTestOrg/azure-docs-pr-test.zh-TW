---
title: "aaaCreate Azure 應用程式閘道-Azure CLI 2.0 |Microsoft 文件"
description: "了解如何使用應用程式閘道 toocreate hello Azure CLI 2.0 在資源管理員"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c2f6516e-3805-49ac-826e-776b909a9104
ms.service: application-gateway
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: 952065586cd87d253882438bb779b768d9fd59fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-by-using-hello-azure-cli-20"></a><span data-ttu-id="17413-103">使用 Azure CLI 2.0 hello 建立應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="17413-103">Create an application gateway by using hello Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="17413-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="17413-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="17413-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="17413-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="17413-106">Azure 傳統 PowerShell</span><span class="sxs-lookup"><span data-stu-id="17413-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="17413-107">Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="17413-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="17413-108">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="17413-108">Azure CLI 1.0</span></span>](application-gateway-create-gateway-cli.md)
> * [<span data-ttu-id="17413-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="17413-109">Azure CLI 2.0</span></span>](application-gateway-create-gateway-cli.md)

<span data-ttu-id="17413-110">「應用程式閘道」是專用的虛擬設備，會以服務形式提供應用程式傳遞控制器 (ADC)，為您的應用程式提供各種第 7 層負載平衡功能。</span><span class="sxs-lookup"><span data-stu-id="17413-110">Application Gateway is a dedicated virtual appliance that provides application delivery controller (ADC) as a service, offering various layer 7 load balancing capabilities for your application.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="17413-111">CLI 版本 toocomplete hello 工作</span><span class="sxs-lookup"><span data-stu-id="17413-111">CLI versions toocomplete hello task</span></span>

<span data-ttu-id="17413-112">您可以完成 hello 工作使用其中一種 hello 遵循 CLI 版本：</span><span class="sxs-lookup"><span data-stu-id="17413-112">You can complete hello task using one of hello following CLI versions:</span></span>

* <span data-ttu-id="17413-113">[Azure CLI 1.0](application-gateway-create-gateway-cli-nodejs.md) -我們 CLI hello 傳統和資源管理部署模型。</span><span class="sxs-lookup"><span data-stu-id="17413-113">[Azure CLI 1.0](application-gateway-create-gateway-cli-nodejs.md) - our CLI for hello classic and resource management deployment models.</span></span>
* <span data-ttu-id="17413-114">[Azure CLI 2.0](application-gateway-create-gateway-cli.md) -hello 資源管理部署模型我們下一個層代 CLI</span><span class="sxs-lookup"><span data-stu-id="17413-114">[Azure CLI 2.0](application-gateway-create-gateway-cli.md) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="prerequisite-install-hello-azure-cli-20"></a><span data-ttu-id="17413-115">必要條件： 安裝 hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="17413-115">Prerequisite: Install hello Azure CLI 2.0</span></span>

<span data-ttu-id="17413-116">tooperform hello 步驟在本文中，您需要[hello Azure 命令列介面安裝的 Mac、 Linux 及 Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2)。</span><span class="sxs-lookup"><span data-stu-id="17413-116">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

> [!NOTE]
> <span data-ttu-id="17413-117">如果您沒有 Azure 帳戶，就需要申請一個。</span><span class="sxs-lookup"><span data-stu-id="17413-117">If you don't have an Azure account, you need one.</span></span> <span data-ttu-id="17413-118">請 [在此處註冊免費試用](../active-directory/sign-up-organization.md)。</span><span class="sxs-lookup"><span data-stu-id="17413-118">Go sign up for a [free trial here](../active-directory/sign-up-organization.md).</span></span>

## <a name="scenario"></a><span data-ttu-id="17413-119">案例</span><span class="sxs-lookup"><span data-stu-id="17413-119">Scenario</span></span>

<span data-ttu-id="17413-120">在此案例中，您學會如何應用程式閘道使用 toocreate hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="17413-120">In this scenario, you learn how toocreate an application gateway using hello Azure portal.</span></span>

<span data-ttu-id="17413-121">此案例將會：</span><span class="sxs-lookup"><span data-stu-id="17413-121">This scenario will:</span></span>

* <span data-ttu-id="17413-122">建立含有兩個執行個體的中型應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="17413-122">Create a medium application gateway with two instances.</span></span>
* <span data-ttu-id="17413-123">建立名為 AdatumAppGatewayVNET 且含有 10.0.0.0/16 保留 CIDR 區塊的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="17413-123">Create a virtual network named AdatumAppGatewayVNET with a reserved CIDR block of 10.0.0.0/16.</span></span>
* <span data-ttu-id="17413-124">建立名為 Appgatewaysubnet 且使用 10.0.0.0/28 做為其 CIDR 區塊的子網路。</span><span class="sxs-lookup"><span data-stu-id="17413-124">Create a subnet called Appgatewaysubnet that uses 10.0.0.0/28 as its CIDR block.</span></span>

> [!NOTE]
> <span data-ttu-id="17413-125">額外設定 hello 應用程式閘道，包括自訂健全狀況探查，hello 應用程式閘道設定之後，而不會在初始部署設定後端集區位址，以及其他規則。</span><span class="sxs-lookup"><span data-stu-id="17413-125">Additional configuration of hello application gateway, including custom health probes, backend pool addresses, and additional rules are configured after hello application gateway is configured and not during initial deployment.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="17413-126">開始之前</span><span class="sxs-lookup"><span data-stu-id="17413-126">Before you begin</span></span>

<span data-ttu-id="17413-127">「Azure 應用程式閘道」需要有自己的子網路。</span><span class="sxs-lookup"><span data-stu-id="17413-127">Azure Application Gateway requires its own subnet.</span></span> <span data-ttu-id="17413-128">當建立虛擬網路，請確定您保留足夠的位址空間 toohave 多個子網路。</span><span class="sxs-lookup"><span data-stu-id="17413-128">When creating a virtual network, ensure that you leave enough address space toohave multiple subnets.</span></span> <span data-ttu-id="17413-129">一旦您部署應用程式閘道 tooa 子網路時，唯一的額外應用程式閘道可以加入 toohello 子網路。</span><span class="sxs-lookup"><span data-stu-id="17413-129">Once you deploy an application gateway tooa subnet, only additional application gateways can be added toohello subnet.</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="17413-130">登入 tooAzure</span><span class="sxs-lookup"><span data-stu-id="17413-130">Log in tooAzure</span></span>

<span data-ttu-id="17413-131">開啟 hello **Microsoft Azure 命令提示字元**，並登入。</span><span class="sxs-lookup"><span data-stu-id="17413-131">Open hello **Microsoft Azure Command Prompt**, and log in.</span></span> 

```azurecli-interactive
az login -u "username"
```

> [!NOTE]
> <span data-ttu-id="17413-132">您也可以使用`az login`不需要輸入 aka.ms/devicelogin 在程式碼的裝置登入的 hello 參數。</span><span class="sxs-lookup"><span data-stu-id="17413-132">You can also use `az login` without hello switch for device login that requires entering a code at aka.ms/devicelogin.</span></span>

<span data-ttu-id="17413-133">一旦您輸入 hello 前面範例中，將程式碼。</span><span class="sxs-lookup"><span data-stu-id="17413-133">Once you type hello preceding example, a code is provided.</span></span> <span data-ttu-id="17413-134">瀏覽 toohttps://aka.ms/devicelogin 瀏覽器 toocontinue hello 登入處理序。</span><span class="sxs-lookup"><span data-stu-id="17413-134">Navigate toohttps://aka.ms/devicelogin in a browser toocontinue hello login process.</span></span>

![顯示裝置登入的 cmd][1]

<span data-ttu-id="17413-136">在 hello 瀏覽器中，輸入您收到 hello 程式碼。</span><span class="sxs-lookup"><span data-stu-id="17413-136">In hello browser, enter hello code you received.</span></span> <span data-ttu-id="17413-137">您已重新導向的 tooa 登入頁面。</span><span class="sxs-lookup"><span data-stu-id="17413-137">You are redirected tooa sign-in page.</span></span>

![瀏覽器 tooenter 程式碼][2]

<span data-ttu-id="17413-139">一旦輸入 hello 程式碼後您登入，關閉 hello 瀏覽器 toocontinue 與 hello 案例。</span><span class="sxs-lookup"><span data-stu-id="17413-139">Once hello code has been entered you are signed in, close hello browser toocontinue on with hello scenario.</span></span>

![已順利登入][3]

## <a name="create-hello-resource-group"></a><span data-ttu-id="17413-141">建立 hello 資源群組</span><span class="sxs-lookup"><span data-stu-id="17413-141">Create hello resource group</span></span>

<span data-ttu-id="17413-142">建立 hello 應用程式閘道之前, 建立 toocontain hello 應用程式閘道資源群組。</span><span class="sxs-lookup"><span data-stu-id="17413-142">Before creating hello application gateway, a resource group is created toocontain hello application gateway.</span></span> <span data-ttu-id="17413-143">hello 下列範例示範 hello 命令。</span><span class="sxs-lookup"><span data-stu-id="17413-143">hello following shows hello command.</span></span>

```azurecli-interactive
az group create --name myresourcegroup --location "eastus"
```

## <a name="create-hello-application-gateway"></a><span data-ttu-id="17413-144">建立 hello 應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="17413-144">Create hello application gateway</span></span>

<span data-ttu-id="17413-145">hello 用於 hello 後端的 IP 位址是後端伺服器的 hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="17413-145">hello IP addresses used for hello backend are hello IP addresses for your backend server.</span></span> <span data-ttu-id="17413-146">這些值可以是任一個私用 Ip hello 虛擬網路、 公用 ip 時或針對後端伺服器的完整的網域名稱。</span><span class="sxs-lookup"><span data-stu-id="17413-146">These values can be either private IPs in hello virtual network, public ips, or fully qualified domain names for your backend servers.</span></span> <span data-ttu-id="17413-147">hello 下列範例會建立應用程式閘道的 http 設定、 連接埠和規則的其他組態設定。</span><span class="sxs-lookup"><span data-stu-id="17413-147">hello following example creates an application gateway with additional configuration settings for http settings, ports, and rules.</span></span>

```azurecli-interactive
az network application-gateway create \
--name "AdatumAppGateway" \
--location "eastus" \
--resource-group "myresourcegroup" \
--vnet-name "AdatumAppGatewayVNET" \
--vnet-address-prefix "10.0.0.0/16" \
--subnet "Appgatewaysubnet" \
--subnet-address-prefix "10.0.0.0/28" \
--servers 10.0.0.4 10.0.0.5 \
--capacity 2 \
--sku Standard_Small \
--http-settings-cookie-based-affinity Enabled \
--http-settings-protocol Http \
--frontend-port 80 \
--routing-rule-type Basic \
--http-settings-port 80 \
--public-ip-address "pip2" \
--public-ip-address-allocation "dynamic" \

```

<span data-ttu-id="17413-148">hello 上述範例中顯示的應用程式閘道的 hello 建立期間不需要的許多屬性。</span><span class="sxs-lookup"><span data-stu-id="17413-148">hello preceding example shows many properties that are not required during hello creation of an application gateway.</span></span> <span data-ttu-id="17413-149">下列程式碼範例的 hello hello 所需資訊以建立應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="17413-149">hello following code example creates an application gateway with hello required information.</span></span>

```azurecli-interactive
az network application-gateway create \
--name "AdatumAppGateway" \
--location "eastus" \
--resource-group "myresourcegroup" \
--vnet-name "AdatumAppGatewayVNET" \
--vnet-address-prefix "10.0.0.0/16" \
--subnet "Appgatewaysubnet \
--subnet-address-prefix "10.0.0.0/28" \
--servers "10.0.0.5"  \
--public-ip-address pip
```
 
> [!NOTE]
> <span data-ttu-id="17413-150">如需可以在下列命令執行的建立 hello 期間提供的參數清單： `az network application-gateway create --help`。</span><span class="sxs-lookup"><span data-stu-id="17413-150">For a list of parameters that can be provided during creation run hello following command: `az network application-gateway create --help`.</span></span>

<span data-ttu-id="17413-151">這個範例會建立基本應用程式閘道 hello 接聽程式、 後端集區、 後端 http 設定和規則的預設設定。</span><span class="sxs-lookup"><span data-stu-id="17413-151">This example creates a basic application gateway with default settings for hello listener, backend pool, backend http settings, and rules.</span></span> <span data-ttu-id="17413-152">可以修改這些設定 toosuit 部署一旦 hello 佈建成功。</span><span class="sxs-lookup"><span data-stu-id="17413-152">You can modify these settings toosuit your deployment once hello provisioning is successful.</span></span>
<span data-ttu-id="17413-153">如果您已經使用在先前步驟中，一旦建立，hello hello 後端集區定義的 web 應用程式負載平衡開始。</span><span class="sxs-lookup"><span data-stu-id="17413-153">If you already have your web application defined with hello backend pool in hello preceding steps, once created, load balancing begins.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="17413-154">取得應用程式閘道 DNS 名稱</span><span class="sxs-lookup"><span data-stu-id="17413-154">Get application gateway DNS name</span></span>

<span data-ttu-id="17413-155">一旦建立 hello 閘道，hello 下一個步驟是 tooconfigure hello 前端進行通訊。</span><span class="sxs-lookup"><span data-stu-id="17413-155">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="17413-156">當使用公用 IP 時，應用程式閘道需要動態指派的 DNS 名稱 (不易記住)。</span><span class="sxs-lookup"><span data-stu-id="17413-156">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="17413-157">tooensure 終端使用者可以叫用 hello 應用程式閘道，CNAME 記錄可使用的 toopoint toohello 公用端點的 hello 應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="17413-157">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="17413-158">[在 Azure 中設定自訂網域名稱](../dns/dns-custom-domain.md)。</span><span class="sxs-lookup"><span data-stu-id="17413-158">[Configuring a custom domain name for in Azure](../dns/dns-custom-domain.md).</span></span> <span data-ttu-id="17413-159">tooconfigure 別名，擷取 hello 應用程式閘道和其相關聯的 IP/DNS 名稱，使用 hello PublicIPAddress 項目附加的 toohello 應用程式閘道的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="17413-159">tooconfigure an alias, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="17413-160">hello 應用程式閘道的 DNS 名稱應該使用的 toocreate CNAME 記錄，哪個點 hello 兩個 web 應用程式 toothis DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="17413-160">hello application gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="17413-161">不建議 hello 使用 A 記錄，因為可能會在重新啟動應用程式閘道變更 hello VIP。</span><span class="sxs-lookup"><span data-stu-id="17413-161">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>


```azurecli-interactive
az network public-ip show --name "pip" --resource-group "AdatumAppGatewayRG"
```

```
{
  "dnsSettings": {
    "domainNameLabel": null,
    "fqdn": "8c786058-96d4-4f3e-bb41-660860ceae4c.cloudapp.net",
    "reverseFqdn": null
  },
  "etag": "W/\"3b0ac031-01f0-4860-b572-e3c25e0c57ad\"",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/AdatumAppGatewayRG/providers/Microsoft.Network/publicIPAddresses/pip2",
  "idleTimeoutInMinutes": 4,
  "ipAddress": "40.121.167.250",
  "ipConfiguration": {
    "etag": null,
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/AdatumAppGatewayRG/providers/Microsoft.Network/applicationGateways/AdatumAppGateway2/frontendIPConfigurations/appGatewayFrontendIP",
    "name": null,
    "privateIpAddress": null,
    "privateIpAllocationMethod": null,
    "provisioningState": null,
    "publicIpAddress": null,
    "resourceGroup": "AdatumAppGatewayRG",
    "subnet": null
  },
  "location": "eastus",
  "name": "pip2",
  "provisioningState": "Succeeded",
  "publicIpAddressVersion": "IPv4",
  "publicIpAllocationMethod": "Dynamic",
  "resourceGroup": "AdatumAppGatewayRG",
  "resourceGuid": "3c30d310-c543-4e9d-9c72-bbacd7fe9b05",
  "tags": {
    "cli[2] owner[administrator]": ""
  },
  "type": "Microsoft.Network/publicIPAddresses"
}
```

## <a name="delete-all-resources"></a><span data-ttu-id="17413-162">刪除所有資源</span><span class="sxs-lookup"><span data-stu-id="17413-162">Delete all resources</span></span>

<span data-ttu-id="17413-163">在本文中完成下列步驟的 hello 建立 toodelete 所有資源：</span><span class="sxs-lookup"><span data-stu-id="17413-163">toodelete all resources created in this article, complete hello following steps:</span></span>

```azurecli-interactive
az group delete --name AdatumAppGatewayRG
```
 
## <a name="next-steps"></a><span data-ttu-id="17413-164">後續步驟</span><span class="sxs-lookup"><span data-stu-id="17413-164">Next steps</span></span>

<span data-ttu-id="17413-165">了解如何 toocreate 自訂健全狀況探查造訪[建立自訂的健全狀況探查](application-gateway-create-probe-portal.md)</span><span class="sxs-lookup"><span data-stu-id="17413-165">Learn how toocreate custom health probes by visiting [Create a custom health probe](application-gateway-create-probe-portal.md)</span></span>

<span data-ttu-id="17413-166">了解如何 tooconfigure SSL 卸載且採用 hello 昂貴 SSL 解密關閉您的 web 伺服器造訪[設定 SSL 卸載](application-gateway-ssl-arm.md)</span><span class="sxs-lookup"><span data-stu-id="17413-166">Learn how tooconfigure SSL Offloading and take hello costly SSL decryption off your web servers by visiting [Configure SSL Offload](application-gateway-ssl-arm.md)</span></span>

<!--Image references-->

[scenario]: ./media/application-gateway-create-gateway-cli/scenario.png
[1]: ./media/application-gateway-create-gateway-cli/figure1.png
[2]: ./media/application-gateway-create-gateway-cli/figure2.png
[3]: ./media/application-gateway-create-gateway-cli/figure3.png
