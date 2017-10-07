---
title: "aaaConfigure web 應用程式防火牆 Azure 應用程式閘道 |Microsoft 文件"
description: "本文提供指引 toostart 使用 web 應用程式在現有或新的應用程式閘道上的防火牆。"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 670b9732-874b-43e6-843b-d2585c160982
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/20/2017
ms.author: gwallace
ms.openlocfilehash: d5354984760ceab12ed49efa9e18836e9f1d3c96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-web-application-firewall-on-a-new-or-existing-application-gateway-with-azure-cli"></a>以 Azure CLI 在新的或現有的應用程式閘道上設定 Web 應用程式防火牆

> [!div class="op_single_selector"]
> * [Azure 入口網站](application-gateway-web-application-firewall-portal.md)
> * [PowerShell](application-gateway-web-application-firewall-powershell.md)
> * [Azure CLI](application-gateway-web-application-firewall-cli.md)

了解如何 toocreate web 應用程式防火牆啟用應用程式閘道，或將 web 應用程式防火牆 tooan 現有應用程式閘道。

hello web 應用程式中的防火牆 (WAF) Azure 應用程式閘道會從網頁型的常見攻擊，例如 SQL 資料隱碼、 跨網站指令碼的攻擊和工作階段倘若保護 web 應用程式。

Azure 應用程式閘道是第 7 層負載平衡器。 無論是在 hello 雲端或內部部署上，它會提供容錯移轉時，效能路由不同的伺服器之間的 HTTP 要求。 應用程式閘道提供許多應用程式傳遞控制器 (ADC) 功能，包括 HTTP 負載平衡、以 Cookie 為基礎的工作階段同質性、安全通訊端層 (SSL) 卸載、自訂健康狀態探查、多網站支援，以及許多其他功能。 toofind 完整支援的功能清單，請造訪：[應用程式閘道概觀](application-gateway-introduction.md)。

hello 下列文章將示範如何太[加入 web 應用程式防火牆 tooan 現有應用程式閘道](#add-web-application-firewall-to-an-existing-application-gateway)和[建立應用程式閘道使用 web 應用程式防火牆](#create-an-application-gateway-with-web-application-firewall)。

![案例影像][scenario]

## <a name="prerequisite-install-hello-azure-cli-20"></a>必要條件： 安裝 hello Azure CLI 2.0

tooperform hello 步驟在本文中，您需要[hello Azure 命令列介面安裝的 Mac、 Linux 及 Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2)。

## <a name="waf-configuration-differences"></a>WAF 組態差異

如果您已閱讀[使用 Azure CLI 建立應用程式閘道](application-gateway-create-gateway-cli.md)，當您了解 hello SKU 設定 tooconfigure 建立應用程式閘道。 WAF 提供額外的設定 toodefine 時應用程式閘道上設定 hello SKU。 沒有您在 hello 應用程式閘道本身進行任何其他變更。

| **設定** | **詳細資料**
|---|---|
|**SKU** |不具有 WAF 的一般應用程式閘道支援 **Standard\_Small**、**Standard\_Medium** 和 **Standard\_Large** 大小。 使用 WAF hello 介紹，有兩個額外的 Sku， **WAF\_媒體**和**WAF\_大**。 小型應用程式閘道不支援 WAF。|
|**模式** | 這項設定是 WAF hello 模式。 允許的值為**偵測**和**防止**。 當 WAF 設定為偵測模式時，所有威脅會儲存在記錄檔中。 在防止模式中，還是會記錄事件，但 hello 攻擊者收到 hello 應用程式閘道 403 未經授權的回應。|

## <a name="add-web-application-firewall-tooan-existing-application-gateway"></a>加入 web 應用程式防火牆 tooan 現有應用程式閘道

hello 遵循命令變更現有的標準應用程式閘道 tooa WAF 啟用應用程式閘道。

```azurecli-interactive
#!/bin/bash

az network application-gateway waf-config set \
  --enabled true \
  --firewall-mode Prevention \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"
```

此命令會更新 web 應用程式防火牆 hello 應用程式閘道。 請瀏覽[應用程式閘道診斷](application-gateway-diagnostics.md)toounderstand tooview 記錄您的應用程式閘道的方式。 WAF toohello 安全性本質，因為記錄檔需要 toobe 定期檢閱 toounderstand hello 安全性狀態的 web 應用程式。

## <a name="create-an-application-gateway-with-web-application-firewall"></a>建立具有 Web 應用程式防火牆的應用程式閘道

hello，下列命令會建立 web 應用程式防火牆應用程式閘道。

```azurecli-interactive
#!/bin/bash

az network application-gateway create \
  --name "AdatumAppGateway2" \
  --location "eastus" \
  --resource-group "AdatumAppGatewayRG" \
  --vnet-name "AdatumAppGatewayVNET2" \
  --vnet-address-prefix "10.0.0.0/16" \
  --subnet "Appgatewaysubnet2" \
  --subnet-address-prefix "10.0.0.0/28" \
 --servers "10.0.0.5 10.0.0.4" \
  --capacity 2 
  --sku "WAF_Medium" \
  --http-settings-cookie-based-affinity "Enabled" \
  --http-settings-protocol "Http" \
  --frontend-port "80" \
  --routing-rule-type "Basic" \
  --http-settings-port "80" \
  --public-ip-address "pip2" \
  --public-ip-address-allocation "dynamic" \
  --tags "cli[2] owner[administrator]"
```

> [!NOTE]
> 建立與 hello 基本 web 應用程式的防火牆設定的應用程式閘道設定成使用 CR 3.0 保護。

## <a name="get-application-gateway-dns-name"></a>取得應用程式閘道 DNS 名稱

一旦建立 hello 閘道，hello 下一個步驟是 tooconfigure hello 前端進行通訊。 當使用公用 IP 時，應用程式閘道需要動態指派的 DNS 名稱 (不易記住)。 tooensure 終端使用者可以叫用 hello 應用程式閘道，CNAME 記錄可使用的 toopoint toohello 公用端點的 hello 應用程式閘道。 [在 Azure 中設定自訂網域名稱](../cloud-services/cloud-services-custom-domain-name-portal.md)。 tooconfigure CNAME 記錄，擷取 hello 應用程式閘道和其相關聯的 IP/DNS 名稱，使用 hello PublicIPAddress 項目附加的 toohello 應用程式閘道的詳細資料。 hello 應用程式閘道的 DNS 名稱應該使用的 toocreate CNAME 記錄，哪個點 hello 兩個 web 應用程式 toothis DNS 名稱。 不建議 hello 使用 A 記錄，因為可能會在重新啟動應用程式閘道變更 hello VIP。

```azurecli-interactive
#!/bin/bash

az network public-ip show \
  --name pip2 \
  --resource-group "AdatumAppGatewayRG"
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

## <a name="next-steps"></a>後續步驟

了解 toocustomize WAF 造訪規則的方式：[自訂 web 應用程式防火牆規則，透過 hello Azure CLI 2.0](application-gateway-customize-waf-rules-cli.md)。

[scenario]: ./media/application-gateway-web-application-firewall-cli/scenario.png
