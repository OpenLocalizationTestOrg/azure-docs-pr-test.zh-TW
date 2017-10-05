---
title: "建立 Azure 應用程式閘道 - Azure CLI 2.0 | Microsoft Docs"
description: "了解如何使用 Resource Manager 中的 Azure CLI 2.0 建立應用程式閘道"
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
ms.openlocfilehash: 052410db8c7619c7990dc319951a55663f2c2ba1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-application-gateway-by-using-the-azure-cli-20"></a><span data-ttu-id="d8278-103">使用 Azure CLI 2.0 建立應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="d8278-103">Create an application gateway by using the Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="d8278-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="d8278-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="d8278-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="d8278-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="d8278-106">Azure 傳統 PowerShell</span><span class="sxs-lookup"><span data-stu-id="d8278-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="d8278-107">Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="d8278-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="d8278-108">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="d8278-108">Azure CLI 1.0</span></span>](application-gateway-create-gateway-cli.md)
> * [<span data-ttu-id="d8278-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="d8278-109">Azure CLI 2.0</span></span>](application-gateway-create-gateway-cli.md)

<span data-ttu-id="d8278-110">「應用程式閘道」是專用的虛擬設備，會以服務形式提供應用程式傳遞控制器 (ADC)，為您的應用程式提供各種第 7 層負載平衡功能。</span><span class="sxs-lookup"><span data-stu-id="d8278-110">Application Gateway is a dedicated virtual appliance that provides application delivery controller (ADC) as a service, offering various layer 7 load balancing capabilities for your application.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="d8278-111">用以完成工作的 CLI 版本</span><span class="sxs-lookup"><span data-stu-id="d8278-111">CLI versions to complete the task</span></span>

<span data-ttu-id="d8278-112">您可以使用下列其中一個 CLI 版本來完成工作︰</span><span class="sxs-lookup"><span data-stu-id="d8278-112">You can complete the task using one of the following CLI versions:</span></span>

* <span data-ttu-id="d8278-113">[Azure CLI 1.0](application-gateway-create-gateway-cli-nodejs.md) - 適用於傳統和資源管理部署模型的 CLI。</span><span class="sxs-lookup"><span data-stu-id="d8278-113">[Azure CLI 1.0](application-gateway-create-gateway-cli-nodejs.md) - our CLI for the classic and resource management deployment models.</span></span>
* <span data-ttu-id="d8278-114">[Azure CLI 2.0](application-gateway-create-gateway-cli.md) - 適用於資源管理部署模型的新一代 CLI</span><span class="sxs-lookup"><span data-stu-id="d8278-114">[Azure CLI 2.0](application-gateway-create-gateway-cli.md) - our next generation CLI for the resource management deployment model</span></span>

## <a name="prerequisite-install-the-azure-cli-20"></a><span data-ttu-id="d8278-115">必要條件：安裝 Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="d8278-115">Prerequisite: Install the Azure CLI 2.0</span></span>

<span data-ttu-id="d8278-116">若要執行本文的步驟，您需要[安裝適用於 Mac、Linux 和 Windows 的 Azure 命令列介面 (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2)。</span><span class="sxs-lookup"><span data-stu-id="d8278-116">To perform the steps in this article, you need to [install the Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

> [!NOTE]
> <span data-ttu-id="d8278-117">如果您沒有 Azure 帳戶，就需要申請一個。</span><span class="sxs-lookup"><span data-stu-id="d8278-117">If you don't have an Azure account, you need one.</span></span> <span data-ttu-id="d8278-118">請 [在此處註冊免費試用](../active-directory/sign-up-organization.md)。</span><span class="sxs-lookup"><span data-stu-id="d8278-118">Go sign up for a [free trial here](../active-directory/sign-up-organization.md).</span></span>

## <a name="scenario"></a><span data-ttu-id="d8278-119">案例</span><span class="sxs-lookup"><span data-stu-id="d8278-119">Scenario</span></span>

<span data-ttu-id="d8278-120">在此案例中，您將了解如何使用 Azure 入口網站來建立應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="d8278-120">In this scenario, you learn how to create an application gateway using the Azure portal.</span></span>

<span data-ttu-id="d8278-121">此案例將會：</span><span class="sxs-lookup"><span data-stu-id="d8278-121">This scenario will:</span></span>

* <span data-ttu-id="d8278-122">建立含有兩個執行個體的中型應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="d8278-122">Create a medium application gateway with two instances.</span></span>
* <span data-ttu-id="d8278-123">建立名為 AdatumAppGatewayVNET 且含有 10.0.0.0/16 保留 CIDR 區塊的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="d8278-123">Create a virtual network named AdatumAppGatewayVNET with a reserved CIDR block of 10.0.0.0/16.</span></span>
* <span data-ttu-id="d8278-124">建立名為 Appgatewaysubnet 且使用 10.0.0.0/28 做為其 CIDR 區塊的子網路。</span><span class="sxs-lookup"><span data-stu-id="d8278-124">Create a subnet called Appgatewaysubnet that uses 10.0.0.0/28 as its CIDR block.</span></span>

> [!NOTE]
> <span data-ttu-id="d8278-125">其他應用程式閘道組態 (包括自訂健康狀況探查、後端集區位址及其他規則) 會在設定應用程式閘道設定之後才進行設定，而不會在初始部署期間設定。</span><span class="sxs-lookup"><span data-stu-id="d8278-125">Additional configuration of the application gateway, including custom health probes, backend pool addresses, and additional rules are configured after the application gateway is configured and not during initial deployment.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="d8278-126">開始之前</span><span class="sxs-lookup"><span data-stu-id="d8278-126">Before you begin</span></span>

<span data-ttu-id="d8278-127">「Azure 應用程式閘道」需要有自己的子網路。</span><span class="sxs-lookup"><span data-stu-id="d8278-127">Azure Application Gateway requires its own subnet.</span></span> <span data-ttu-id="d8278-128">建立虛擬網路時，請確定您保留足夠的位址空間，以便擁有多個子網路。</span><span class="sxs-lookup"><span data-stu-id="d8278-128">When creating a virtual network, ensure that you leave enough address space to have multiple subnets.</span></span> <span data-ttu-id="d8278-129">將應用程式閘道部署到子網路之後，就只能將額外的應用程式閘道新增到該子網路。</span><span class="sxs-lookup"><span data-stu-id="d8278-129">Once you deploy an application gateway to a subnet, only additional application gateways can be added to the subnet.</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="d8278-130">登入 Azure</span><span class="sxs-lookup"><span data-stu-id="d8278-130">Log in to Azure</span></span>

<span data-ttu-id="d8278-131">開啟 [Microsoft Azure 命令提示字元] 並登入。</span><span class="sxs-lookup"><span data-stu-id="d8278-131">Open the **Microsoft Azure Command Prompt**, and log in.</span></span> 

```azurecli-interactive
az login -u "username"
```

> [!NOTE]
> <span data-ttu-id="d8278-132">您也可以使用 `az login` 而不搭配會要求在 aka.ms/devicelogin 輸入代碼的裝置登入參數。</span><span class="sxs-lookup"><span data-stu-id="d8278-132">You can also use `az login` without the switch for device login that requires entering a code at aka.ms/devicelogin.</span></span>

<span data-ttu-id="d8278-133">輸入上述範例後會提供程式碼。</span><span class="sxs-lookup"><span data-stu-id="d8278-133">Once you type the preceding example, a code is provided.</span></span> <span data-ttu-id="d8278-134">在瀏覽器中瀏覽至 https://aka.ms/devicelogin 以繼續登入程序。</span><span class="sxs-lookup"><span data-stu-id="d8278-134">Navigate to https://aka.ms/devicelogin in a browser to continue the login process.</span></span>

![顯示裝置登入的 cmd][1]

<span data-ttu-id="d8278-136">在瀏覽器中，輸入收到的程式碼。</span><span class="sxs-lookup"><span data-stu-id="d8278-136">In the browser, enter the code you received.</span></span> <span data-ttu-id="d8278-137">系統會將您重新導向至 [登入] 頁面。</span><span class="sxs-lookup"><span data-stu-id="d8278-137">You are redirected to a sign-in page.</span></span>

![要輸入程式碼的瀏覽器][2]

<span data-ttu-id="d8278-139">輸入程式碼後您已登入，請關閉瀏覽器以繼續進行案例。</span><span class="sxs-lookup"><span data-stu-id="d8278-139">Once the code has been entered you are signed in, close the browser to continue on with the scenario.</span></span>

![已順利登入][3]

## <a name="create-the-resource-group"></a><span data-ttu-id="d8278-141">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="d8278-141">Create the resource group</span></span>

<span data-ttu-id="d8278-142">建立應用程式閘道之前，會建立資源群組以包含應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="d8278-142">Before creating the application gateway, a resource group is created to contain the application gateway.</span></span> <span data-ttu-id="d8278-143">以下顯示命令。</span><span class="sxs-lookup"><span data-stu-id="d8278-143">The following shows the command.</span></span>

```azurecli-interactive
az group create --name myresourcegroup --location "eastus"
```

## <a name="create-the-application-gateway"></a><span data-ttu-id="d8278-144">建立應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="d8278-144">Create the application gateway</span></span>

<span data-ttu-id="d8278-145">用於後端的 IP 位址是後端伺服器的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="d8278-145">The IP addresses used for the backend are the IP addresses for your backend server.</span></span> <span data-ttu-id="d8278-146">這些值可以是虛擬網路中的私人 IP、公用 IP 或後端伺服器的完整網域名稱。</span><span class="sxs-lookup"><span data-stu-id="d8278-146">These values can be either private IPs in the virtual network, public ips, or fully qualified domain names for your backend servers.</span></span> <span data-ttu-id="d8278-147">下列範例會使用 http 設定、連接埠和規則的其他組態設定來建立應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="d8278-147">The following example creates an application gateway with additional configuration settings for http settings, ports, and rules.</span></span>

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

<span data-ttu-id="d8278-148">上述範例顯示建立應用程式閘道期間不需要的許多屬性。</span><span class="sxs-lookup"><span data-stu-id="d8278-148">The preceding example shows many properties that are not required during the creation of an application gateway.</span></span> <span data-ttu-id="d8278-149">下列程式碼範例會使用必要資訊來建立應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="d8278-149">The following code example creates an application gateway with the required information.</span></span>

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
> <span data-ttu-id="d8278-150">如需可在建立期間提供的參數清單，請執行下列命令︰`az network application-gateway create --help`。</span><span class="sxs-lookup"><span data-stu-id="d8278-150">For a list of parameters that can be provided during creation run the following command: `az network application-gateway create --help`.</span></span>

<span data-ttu-id="d8278-151">此範例會建立一個具有接聽程式、後端集區、後端 http 設定及規則之預設設定的基本應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="d8278-151">This example creates a basic application gateway with default settings for the listener, backend pool, backend http settings, and rules.</span></span> <span data-ttu-id="d8278-152">佈建成功之後，您可以依據您的部署需求修改這些設定。</span><span class="sxs-lookup"><span data-stu-id="d8278-152">You can modify these settings to suit your deployment once the provisioning is successful.</span></span>
<span data-ttu-id="d8278-153">如果在先前步驟中已經以後端集區定義 Web 應用程式，一旦建立之後，負載平衡即開始。</span><span class="sxs-lookup"><span data-stu-id="d8278-153">If you already have your web application defined with the backend pool in the preceding steps, once created, load balancing begins.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="d8278-154">取得應用程式閘道 DNS 名稱</span><span class="sxs-lookup"><span data-stu-id="d8278-154">Get application gateway DNS name</span></span>

<span data-ttu-id="d8278-155">建立閘道之後，下一步是設定通訊的前端。</span><span class="sxs-lookup"><span data-stu-id="d8278-155">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="d8278-156">當使用公用 IP 時，應用程式閘道需要動態指派的 DNS 名稱 (不易記住)。</span><span class="sxs-lookup"><span data-stu-id="d8278-156">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="d8278-157">為了確保使用者可以叫用應用程式閘道，可使用 CNAME 記錄來指向應用程式閘道的公用端點。</span><span class="sxs-lookup"><span data-stu-id="d8278-157">To ensure end users can hit the application gateway, a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="d8278-158">[在 Azure 中設定自訂網域名稱](../dns/dns-custom-domain.md)。</span><span class="sxs-lookup"><span data-stu-id="d8278-158">[Configuring a custom domain name for in Azure](../dns/dns-custom-domain.md).</span></span> <span data-ttu-id="d8278-159">若要設定別名，請使用連接至應用程式閘道的 PublicIPAddress 項目，擷取應用程式閘道的詳細資料及其關聯的 IP/DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="d8278-159">To configure an alias, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="d8278-160">應用程式閘道的 DNS 名稱應該用來建立將兩個 Web 應用程式指向此 DNS 名稱的 CNAME 記錄。</span><span class="sxs-lookup"><span data-stu-id="d8278-160">The application gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span></span> <span data-ttu-id="d8278-161">不建議使用 A-records，因為重新啟動應用程式閘道時，VIP 可能會變更。</span><span class="sxs-lookup"><span data-stu-id="d8278-161">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>


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

## <a name="delete-all-resources"></a><span data-ttu-id="d8278-162">刪除所有資源</span><span class="sxs-lookup"><span data-stu-id="d8278-162">Delete all resources</span></span>

<span data-ttu-id="d8278-163">若要刪除這篇文章中建立的所有資源，請完成下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="d8278-163">To delete all resources created in this article, complete the following steps:</span></span>

```azurecli-interactive
az group delete --name AdatumAppGatewayRG
```
 
## <a name="next-steps"></a><span data-ttu-id="d8278-164">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d8278-164">Next steps</span></span>

<span data-ttu-id="d8278-165">參閱 [建立自訂健康狀態探查](application-gateway-create-probe-portal.md)</span><span class="sxs-lookup"><span data-stu-id="d8278-165">Learn how to create custom health probes by visiting [Create a custom health probe](application-gateway-create-probe-portal.md)</span></span>

<span data-ttu-id="d8278-166">參閱 [設定 SSL 卸載](application-gateway-ssl-arm.md)</span><span class="sxs-lookup"><span data-stu-id="d8278-166">Learn how to configure SSL Offloading and take the costly SSL decryption off your web servers by visiting [Configure SSL Offload](application-gateway-ssl-arm.md)</span></span>

<!--Image references-->

[scenario]: ./media/application-gateway-create-gateway-cli/scenario.png
[1]: ./media/application-gateway-create-gateway-cli/figure1.png
[2]: ./media/application-gateway-create-gateway-cli/figure2.png
[3]: ./media/application-gateway-create-gateway-cli/figure3.png
