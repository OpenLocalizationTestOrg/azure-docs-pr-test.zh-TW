---
title: "設定 SSL 卸載 - Azure 應用程式閘道 - Azure CLI 2.0 | Microsoft Docs"
description: "本頁面提供使用 Azure CLI 2.0 來建立具有 SSL 卸載之應用程式閘道的指示"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/26/2017
ms.author: gwallace
ms.openlocfilehash: e8c1ba09daef09ef5002e33345905772961c1d93
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-azure-cli-20"></a><span data-ttu-id="4a504-103">使用 Azure CLI 2.0 設定適用於 SSL 卸載的應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="4a504-103">Configure an application gateway for SSL offload by using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="4a504-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="4a504-104">Azure portal</span></span>](application-gateway-ssl-portal.md)
> * [<span data-ttu-id="4a504-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="4a504-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ssl-arm.md)
> * [<span data-ttu-id="4a504-106">Azure 傳統 PowerShell</span><span class="sxs-lookup"><span data-stu-id="4a504-106">Azure Classic PowerShell</span></span>](application-gateway-ssl.md)
> * [<span data-ttu-id="4a504-107">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="4a504-107">Azure CLI 2.0</span></span>](application-gateway-ssl-cli.md)

<span data-ttu-id="4a504-108">Azure 應用程式閘道可以設定為在閘道終止安全通訊端層 (SSL) 工作階段，以避免 Web 伺服陣列發生高成本的 SSL 解密工作。</span><span class="sxs-lookup"><span data-stu-id="4a504-108">Azure Application Gateway can be configured to terminate the Secure Sockets Layer (SSL) session at the gateway to avoid costly SSL decryption tasks to happen at the web farm.</span></span> <span data-ttu-id="4a504-109">SSL 卸載也可簡化在前端伺服器的憑證管理。</span><span class="sxs-lookup"><span data-stu-id="4a504-109">SSL offload also simplifies certificate management at the front-end server.</span></span>

## <a name="prerequisite-install-the-azure-cli-20"></a><span data-ttu-id="4a504-110">必要條件：安裝 Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="4a504-110">Prerequisite: Install the Azure CLI 2.0</span></span>

<span data-ttu-id="4a504-111">若要執行本文的步驟，您需要[安裝適用於 Mac、Linux 和 Windows 的 Azure 命令列介面 (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2)。</span><span class="sxs-lookup"><span data-stu-id="4a504-111">To perform the steps in this article, you need to [install the Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="required-components"></a><span data-ttu-id="4a504-112">必要的元件</span><span class="sxs-lookup"><span data-stu-id="4a504-112">Required components</span></span>

* <span data-ttu-id="4a504-113">**後端伺服器集區：** 後端伺服器的 IP 位址清單。</span><span class="sxs-lookup"><span data-stu-id="4a504-113">**Back-end server pool:** The list of IP addresses of the back-end servers.</span></span> <span data-ttu-id="4a504-114">列出的 IP 位址應屬於虛擬網路子網路或是公用 IP/VIP。</span><span class="sxs-lookup"><span data-stu-id="4a504-114">The IP addresses listed should either belong to the virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="4a504-115">**後端伺服器集區設定：** 每個集區都包括一些設定，例如連接埠、通訊協定和以 Cookie 為基礎的同質性。</span><span class="sxs-lookup"><span data-stu-id="4a504-115">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="4a504-116">這些設定會繫結至集區，並套用至集區內所有伺服器。</span><span class="sxs-lookup"><span data-stu-id="4a504-116">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="4a504-117">**前端連接埠：** 此連接埠是在應用程式閘道上開啟的公用連接埠。</span><span class="sxs-lookup"><span data-stu-id="4a504-117">**Front-end port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="4a504-118">流量會達到此連接埠，然後重新導向至其中一個後端伺服器。</span><span class="sxs-lookup"><span data-stu-id="4a504-118">Traffic hits this port, and then gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="4a504-119">**接聽程式：** 接聽程式具有前端連接埠、通訊協定 (Http 或 Https，這些設定都區分大小寫) 和 SSL 憑證名稱 (如果已設定 SSL 卸載)。</span><span class="sxs-lookup"><span data-stu-id="4a504-119">**Listener:** The listener has a front-end port, a protocol (Http or Https, these settings are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="4a504-120">**規則：** 規則會繫結接聽程式和後端伺服器集區，並定義流量達到特定接聽程式時應該導向至哪個後端伺服器集區。</span><span class="sxs-lookup"><span data-stu-id="4a504-120">**Rule:** The rule binds the listener and the back-end server pool and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span></span> <span data-ttu-id="4a504-121">目前只支援 *基本* 規則。</span><span class="sxs-lookup"><span data-stu-id="4a504-121">Currently, only the *basic* rule is supported.</span></span> <span data-ttu-id="4a504-122">*基本* 規則是循環配置資源的負載分配。</span><span class="sxs-lookup"><span data-stu-id="4a504-122">The *basic* rule is round-robin load distribution.</span></span>

<span data-ttu-id="4a504-123">**其他組態注意事項**</span><span class="sxs-lookup"><span data-stu-id="4a504-123">**Additional configuration notes**</span></span>

<span data-ttu-id="4a504-124">針對 SSL 憑證組態，**HttpListener** 中的通訊協定應該變更為 *Https* (區分大小寫)。</span><span class="sxs-lookup"><span data-stu-id="4a504-124">For SSL certificates configuration, the protocol in **HttpListener** should change to *Https* (case sensitive).</span></span> <span data-ttu-id="4a504-125">將 **SslCertificate** 元素新增至 **HttpListener**，並針對 SSL 憑證設定變數值。</span><span class="sxs-lookup"><span data-stu-id="4a504-125">The **SslCertificate** element is added to **HttpListener** with the variable value configured for the SSL certificate.</span></span> <span data-ttu-id="4a504-126">前端連接埠應該更新為 443。</span><span class="sxs-lookup"><span data-stu-id="4a504-126">The front-end port should be updated to 443.</span></span>

<span data-ttu-id="4a504-127">**啟用以 Cookie 為基礎的同質性**：您可以設定應用程式閘道，以確保來自用戶端工作階段的要求一律會導向至 Web 伺服陣列中的相同 VM。</span><span class="sxs-lookup"><span data-stu-id="4a504-127">**To enable cookie-based affinity**: An application gateway can be configured to ensure that a request from a client session is always directed to the same VM in the web farm.</span></span> <span data-ttu-id="4a504-128">此案例透過插入允許閘道適當導向流量的工作階段 Cookie 來完成。</span><span class="sxs-lookup"><span data-stu-id="4a504-128">This scenario is done by injection of a session cookie that allows the gateway to direct traffic appropriately.</span></span> <span data-ttu-id="4a504-129">若要啟用以 Cookie 為基礎的同質性，請在 **BackendHttpSettings** 元素中將 **CookieBasedAffinity** 設定為 *Enabled*。</span><span class="sxs-lookup"><span data-stu-id="4a504-129">To enable cookie-based affinity, set **CookieBasedAffinity** to *Enabled* in the **BackendHttpSettings** element.</span></span>

## <a name="configure-ssl-offload-on-an-existing-application-gateway"></a><span data-ttu-id="4a504-130">在現有的應用程式閘道上設定 SSL 卸載</span><span class="sxs-lookup"><span data-stu-id="4a504-130">Configure SSL offload on an existing application gateway</span></span>

```azurecli-interactive
#!/bin/bash

# Create a new front end port to be used for SSL
az network application-gateway frontend-port create \
  --name sslport \
  --port 443 \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"

# Upload the .pfx certificate for SSL offload
az network application-gateway ssl-cert create \
  --name "newcert" \
  --cert-file /home/azureuser/self-signed/AdatumAppGatewayCert.pfx \
  --cert-password P@ssw0rd \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"

# Create a new listener referencing the port and certificate created earlier
az network application-gateway http-listener create \
  --frontend-ip "appGatewayFrontendIP" \
  --frontend-port sslport  \
  --name sslListener \
  --ssl-cert newcert \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"

# Create a new back-end pool to be used
az network application-gateway address-pool create \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG" \
  --name "appGatewayBackendPool2" \
  --servers 10.0.0.7 10.0.0.8

# Create a new back-end HTTP settings using the new probe
az network application-gateway http-settings create \
  --name "settings2" \
  --port 80 \
  --cookie-based-affinity Enabled \
  --protocol "Http" \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"

# Create a new rule linking the listener to the back-end pool
az network application-gateway rule create \
  --name "rule2" \
  --rule-type Basic \
  --http-settings settings2 \
  --http-listener ssllistener \
  --address-pool temp1 \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"

```

## <a name="create-an-application-gateway-with-ssl-offload"></a><span data-ttu-id="4a504-131">建立具有 SSL 卸載的應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="4a504-131">Create an application gateway with SSL Offload</span></span>

<span data-ttu-id="4a504-132">下列範例會建立具有 SSL 卸載的應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="4a504-132">The following sample creates an application gateway with SSL offload.</span></span>  <span data-ttu-id="4a504-133">憑證和憑證密碼，都必須更新為有效的私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="4a504-133">The certificate and certificate password must be updated to a valid private key.</span></span>

```azurecli-interactive
#!/bin/bash

# Creates an application gateway with SSL offload
az network application-gateway create \
  --name "AdatumAppGateway3" \
  --location "eastus" \
  --resource-group "AdatumAppGatewayRG2" \
  --vnet-name "AdatumAppGatewayVNET2" \
  --cert-file /home/azureuser/self-signed/AdatumAppGatewayCert.pfx \
  --cert-password P@ssw0rd \
  --vnet-address-prefix "10.0.0.0/16" \
  --subnet "Appgatewaysubnet" \
  --subnet-address-prefix "10.0.0.0/28" \
  --frontend-port 443 \
  --servers "10.0.0.5 10.0.0.4" \
  --capacity 2 \
  --sku "Standard_Small" \
  --http-settings-cookie-based-affinity "Enabled" \
  --http-settings-protocol "Http" \
  --frontend-port "80" \
  --routing-rule-type "Basic" \
  --http-settings-port "80" \
  --public-ip-address "pip" \
  --public-ip-address-allocation "dynamic"
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="4a504-134">取得應用程式閘道 DNS 名稱</span><span class="sxs-lookup"><span data-stu-id="4a504-134">Get application gateway DNS name</span></span>

<span data-ttu-id="4a504-135">建立閘道之後，下一步是設定通訊的前端。</span><span class="sxs-lookup"><span data-stu-id="4a504-135">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="4a504-136">當使用公用 IP 時，應用程式閘道需要動態指派的 DNS 名稱 (不易記住)。</span><span class="sxs-lookup"><span data-stu-id="4a504-136">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="4a504-137">為了確保使用者可以叫用應用程式閘道，可使用 CNAME 記錄來指向應用程式閘道的公用端點。</span><span class="sxs-lookup"><span data-stu-id="4a504-137">To ensure end users can hit the application gateway, a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="4a504-138">[在 Azure 中設定自訂網域名稱](../cloud-services/cloud-services-custom-domain-name-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="4a504-138">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="4a504-139">若要設定別名，請使用連接至應用程式閘道的 PublicIPAddress 項目，擷取應用程式閘道的詳細資料及其關聯的 IP/DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="4a504-139">To configure an alias, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="4a504-140">應用程式閘道的 DNS 名稱應該用來建立將兩個 Web 應用程式指向此 DNS 名稱的 CNAME 記錄。</span><span class="sxs-lookup"><span data-stu-id="4a504-140">The application gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span></span> <span data-ttu-id="4a504-141">不建議使用 A-records，因為重新啟動應用程式閘道時，VIP 可能會變更。</span><span class="sxs-lookup"><span data-stu-id="4a504-141">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>


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

## <a name="next-steps"></a><span data-ttu-id="4a504-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4a504-142">Next steps</span></span>

<span data-ttu-id="4a504-143">如果您想要將應用程式閘道設為與內部負載平衡器 (ILB) 搭配使用，請參閱 [建立具有內部負載平衡器 (ILB) 的應用程式閘道](application-gateway-ilb.md)。</span><span class="sxs-lookup"><span data-stu-id="4a504-143">If you want to configure an application gateway to use with an internal load balancer (ILB), see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="4a504-144">如果您想進一步了解一般負載平衡選項，請參閱：</span><span class="sxs-lookup"><span data-stu-id="4a504-144">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="4a504-145">Azure 負載平衡器</span><span class="sxs-lookup"><span data-stu-id="4a504-145">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="4a504-146">Azure 流量管理員</span><span class="sxs-lookup"><span data-stu-id="4a504-146">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)
