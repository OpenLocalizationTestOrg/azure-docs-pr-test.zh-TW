---
title: "aaaConfigure SSL 卸載 Azure 應用程式閘道-Azure CLI 2.0 |Microsoft 文件"
description: "本頁面提供的指示 toocreate 應用程式閘道以 SSL 卸載 Azure CLI 2.0"
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
ms.openlocfilehash: f8d50e0c6ffef17c807938d816410e6d85321c9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-azure-cli-20"></a><span data-ttu-id="f66ef-103">使用 Azure CLI 2.0 設定適用於 SSL 卸載的應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="f66ef-103">Configure an application gateway for SSL offload by using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f66ef-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="f66ef-104">Azure portal</span></span>](application-gateway-ssl-portal.md)
> * [<span data-ttu-id="f66ef-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="f66ef-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ssl-arm.md)
> * [<span data-ttu-id="f66ef-106">Azure 傳統 PowerShell</span><span class="sxs-lookup"><span data-stu-id="f66ef-106">Azure Classic PowerShell</span></span>](application-gateway-ssl.md)
> * [<span data-ttu-id="f66ef-107">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="f66ef-107">Azure CLI 2.0</span></span>](application-gateway-ssl-cli.md)

<span data-ttu-id="f66ef-108">Azure 應用程式閘道可以在 hello 閘道 tooavoid 昂貴 SSL 解密工作 toohappen hello web 伺服陣列設定的 tooterminate hello Secure Sockets Layer (SSL) 工作階段。</span><span class="sxs-lookup"><span data-stu-id="f66ef-108">Azure Application Gateway can be configured tooterminate hello Secure Sockets Layer (SSL) session at hello gateway tooavoid costly SSL decryption tasks toohappen at hello web farm.</span></span> <span data-ttu-id="f66ef-109">SSL 卸載也可簡化在 hello 前端伺服器的憑證管理。</span><span class="sxs-lookup"><span data-stu-id="f66ef-109">SSL offload also simplifies certificate management at hello front-end server.</span></span>

## <a name="prerequisite-install-hello-azure-cli-20"></a><span data-ttu-id="f66ef-110">必要條件： 安裝 hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="f66ef-110">Prerequisite: Install hello Azure CLI 2.0</span></span>

<span data-ttu-id="f66ef-111">tooperform hello 步驟在本文中，您需要[hello Azure 命令列介面安裝的 Mac、 Linux 及 Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2)。</span><span class="sxs-lookup"><span data-stu-id="f66ef-111">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="required-components"></a><span data-ttu-id="f66ef-112">必要的元件</span><span class="sxs-lookup"><span data-stu-id="f66ef-112">Required components</span></span>

* <span data-ttu-id="f66ef-113">**後端伺服器集區：** hello hello 後端伺服器的 IP 位址清單。</span><span class="sxs-lookup"><span data-stu-id="f66ef-113">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="f66ef-114">列出 hello IP 位址應該是屬於 toohello 虛擬網路子網路，或應該是公用 IP/VIP。</span><span class="sxs-lookup"><span data-stu-id="f66ef-114">hello IP addresses listed should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="f66ef-115">**後端伺服器集區設定：** 每個集區都包括一些設定，例如連接埠、通訊協定和以 Cookie 為基礎的同質性。</span><span class="sxs-lookup"><span data-stu-id="f66ef-115">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="f66ef-116">這些設定會繫結的 tooa 集區，並套用的 tooall hello 集區內的伺服器。</span><span class="sxs-lookup"><span data-stu-id="f66ef-116">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="f66ef-117">**前端連接埠：**此連接埠是開啟 hello 應用程式閘道上的 hello 公用連接埠。</span><span class="sxs-lookup"><span data-stu-id="f66ef-117">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="f66ef-118">流量叫用這個連接埠，然後再取得重新導向 tooone 的 hello 後端伺服器。</span><span class="sxs-lookup"><span data-stu-id="f66ef-118">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="f66ef-119">**接聽程式：** hello 接聽程式有前端連接埠的通訊協定 （Http 或 Https，這些設定是區分大小寫），與 hello 的 SSL 憑證名稱 （如果有設定 SSL 卸載）。</span><span class="sxs-lookup"><span data-stu-id="f66ef-119">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these settings are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="f66ef-120">**規則：** hello 規則繫結 hello 接聽程式和 hello 後端伺服器集區，並定義哪一個後端伺服器集區 hello 流量應導向的 toowhen 配接器特定接聽程式。</span><span class="sxs-lookup"><span data-stu-id="f66ef-120">**Rule:** hello rule binds hello listener and hello back-end server pool and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span> <span data-ttu-id="f66ef-121">目前，只有 hello*基本*規則支援。</span><span class="sxs-lookup"><span data-stu-id="f66ef-121">Currently, only hello *basic* rule is supported.</span></span> <span data-ttu-id="f66ef-122">hello*基本*規則是循環配置資源負載分佈。</span><span class="sxs-lookup"><span data-stu-id="f66ef-122">hello *basic* rule is round-robin load distribution.</span></span>

<span data-ttu-id="f66ef-123">**其他組態注意事項**</span><span class="sxs-lookup"><span data-stu-id="f66ef-123">**Additional configuration notes**</span></span>

<span data-ttu-id="f66ef-124">SSL 憑證設定，如 hello 中的通訊協定**HttpListener**也應該變更*Https* （區分大小寫）。</span><span class="sxs-lookup"><span data-stu-id="f66ef-124">For SSL certificates configuration, hello protocol in **HttpListener** should change too*Https* (case sensitive).</span></span> <span data-ttu-id="f66ef-125">hello **SslCertificate**太新增項目**HttpListener** hello hello SSL 憑證設定的變數值。</span><span class="sxs-lookup"><span data-stu-id="f66ef-125">hello **SslCertificate** element is added too**HttpListener** with hello variable value configured for hello SSL certificate.</span></span> <span data-ttu-id="f66ef-126">hello 前端連接埠應為更新的 too443。</span><span class="sxs-lookup"><span data-stu-id="f66ef-126">hello front-end port should be updated too443.</span></span>

<span data-ttu-id="f66ef-127">**tooenable cookie 為基礎的同質**： 應用程式閘道可以是來自用戶端工作階段的要求會導向的 toohello 設定的 tooensure hello web 伺服陣列中相同的 VM。</span><span class="sxs-lookup"><span data-stu-id="f66ef-127">**tooenable cookie-based affinity**: An application gateway can be configured tooensure that a request from a client session is always directed toohello same VM in hello web farm.</span></span> <span data-ttu-id="f66ef-128">此案例中是由資料隱碼的工作階段 cookie，可讓 hello 閘道 toodirect 流量時，適當地完成。</span><span class="sxs-lookup"><span data-stu-id="f66ef-128">This scenario is done by injection of a session cookie that allows hello gateway toodirect traffic appropriately.</span></span> <span data-ttu-id="f66ef-129">tooenable cookie 架構親和性，設定**CookieBasedAffinity**太*啟用*在 hello **BackendHttpSettings**項目。</span><span class="sxs-lookup"><span data-stu-id="f66ef-129">tooenable cookie-based affinity, set **CookieBasedAffinity** too*Enabled* in hello **BackendHttpSettings** element.</span></span>

## <a name="configure-ssl-offload-on-an-existing-application-gateway"></a><span data-ttu-id="f66ef-130">在現有的應用程式閘道上設定 SSL 卸載</span><span class="sxs-lookup"><span data-stu-id="f66ef-130">Configure SSL offload on an existing application gateway</span></span>

```azurecli-interactive
#!/bin/bash

# Create a new front end port toobe used for SSL
az network application-gateway frontend-port create \
  --name sslport \
  --port 443 \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"

# Upload hello .pfx certificate for SSL offload
az network application-gateway ssl-cert create \
  --name "newcert" \
  --cert-file /home/azureuser/self-signed/AdatumAppGatewayCert.pfx \
  --cert-password P@ssw0rd \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"

# Create a new listener referencing hello port and certificate created earlier
az network application-gateway http-listener create \
  --frontend-ip "appGatewayFrontendIP" \
  --frontend-port sslport  \
  --name sslListener \
  --ssl-cert newcert \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"

# Create a new back-end pool toobe used
az network application-gateway address-pool create \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG" \
  --name "appGatewayBackendPool2" \
  --servers 10.0.0.7 10.0.0.8

# Create a new back-end HTTP settings using hello new probe
az network application-gateway http-settings create \
  --name "settings2" \
  --port 80 \
  --cookie-based-affinity Enabled \
  --protocol "Http" \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"

# Create a new rule linking hello listener toohello back-end pool
az network application-gateway rule create \
  --name "rule2" \
  --rule-type Basic \
  --http-settings settings2 \
  --http-listener ssllistener \
  --address-pool temp1 \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"

```

## <a name="create-an-application-gateway-with-ssl-offload"></a><span data-ttu-id="f66ef-131">建立具有 SSL 卸載的應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="f66ef-131">Create an application gateway with SSL Offload</span></span>

<span data-ttu-id="f66ef-132">hello 下列範例會使用 SSL 卸載，建立應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="f66ef-132">hello following sample creates an application gateway with SSL offload.</span></span>  <span data-ttu-id="f66ef-133">hello 憑證和憑證密碼必須更新的 tooa 有效的私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="f66ef-133">hello certificate and certificate password must be updated tooa valid private key.</span></span>

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

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="f66ef-134">取得應用程式閘道 DNS 名稱</span><span class="sxs-lookup"><span data-stu-id="f66ef-134">Get application gateway DNS name</span></span>

<span data-ttu-id="f66ef-135">一旦建立 hello 閘道，hello 下一個步驟是 tooconfigure hello 前端進行通訊。</span><span class="sxs-lookup"><span data-stu-id="f66ef-135">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="f66ef-136">當使用公用 IP 時，應用程式閘道需要動態指派的 DNS 名稱 (不易記住)。</span><span class="sxs-lookup"><span data-stu-id="f66ef-136">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="f66ef-137">tooensure 終端使用者可以叫用 hello 應用程式閘道，CNAME 記錄可使用的 toopoint toohello 公用端點的 hello 應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="f66ef-137">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="f66ef-138">[在 Azure 中設定自訂網域名稱](../cloud-services/cloud-services-custom-domain-name-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="f66ef-138">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="f66ef-139">tooconfigure 別名，擷取 hello 應用程式閘道和其相關聯的 IP/DNS 名稱，使用 hello PublicIPAddress 項目附加的 toohello 應用程式閘道的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="f66ef-139">tooconfigure an alias, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="f66ef-140">hello 應用程式閘道的 DNS 名稱應該使用的 toocreate CNAME 記錄，哪個點 hello 兩個 web 應用程式 toothis DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="f66ef-140">hello application gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="f66ef-141">不建議 hello 使用 A 記錄，因為可能會在重新啟動應用程式閘道變更 hello VIP。</span><span class="sxs-lookup"><span data-stu-id="f66ef-141">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>


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

## <a name="next-steps"></a><span data-ttu-id="f66ef-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f66ef-142">Next steps</span></span>

<span data-ttu-id="f66ef-143">如果您想 tooconfigure 內部負載平衡器 (ILB) 應用程式閘道 toouse，請參閱[內部負載平衡器 (ILB) 建立應用程式閘道](application-gateway-ilb.md)。</span><span class="sxs-lookup"><span data-stu-id="f66ef-143">If you want tooconfigure an application gateway toouse with an internal load balancer (ILB), see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="f66ef-144">如果您想進一步了解一般負載平衡選項，請參閱：</span><span class="sxs-lookup"><span data-stu-id="f66ef-144">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="f66ef-145">Azure 負載平衡器</span><span class="sxs-lookup"><span data-stu-id="f66ef-145">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="f66ef-146">Azure 流量管理員</span><span class="sxs-lookup"><span data-stu-id="f66ef-146">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)
