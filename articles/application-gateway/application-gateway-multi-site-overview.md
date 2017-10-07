---
title: "aaaHosting Azure 應用程式閘道上的多個站台 |Microsoft 文件"
description: "此頁面提供 hello 應用程式閘道多站台支援的概觀。"
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: 
ms.assetid: 49993fd2-87e5-4a66-b386-8d22056a616d
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/09/2017
ms.author: amsriva
ms.openlocfilehash: 4ab6faa97f1891d7525affdaa36463681bf99e9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="application-gateway-multiple-site-hosting"></a>應用程式閘道多站台裝載

多個站台裝載可讓您 tooconfigure 多個 hello 上的一個 web 應用程式相同的應用程式閘道執行個體。 這項功能可讓您更有效率地為您的部署拓撲 tooconfigure 新增 too20 網站 tooone 應用程式閘道。 每個網站可以導向 tooits 擁有後端集區。 在下列範例的 hello，應用程式閘道正在提供服務給 contoso.com 和 fabrikam.com，從稱為 ContosoServerPool 和 FabrikamServerPool 的兩個後端伺服器集區的流量。

![imageURLroute](./media/application-gateway-multi-site-overview/multisite.png)

> [!IMPORTANT]
> 規則的處理順序 hello hello 入口網站中列出。 強烈建議使用的 tooconfigure 多站台接聽程式第一次先前 tooconfiguring 基本的接聽程式它。  這可確保該流量取得路由的 toohello 帶回結束。 如果先列出了基本接聽程式，且該接聽程式符合傳入的要求，就會由該接聽程式處理。

Http://contoso.com 的要求，則路由的 tooContosoServerPool，而且 http://fabrikam.com 路由的 tooFabrikamServerPool。

同樣的兩個 hello 可裝載於相同的父系網域的子網域 hello 相同的應用程式閘道部署。 使用子網域的範例可能包括單一應用程式閘道部署上裝載的 http://blog.contoso.com 和 http://app.contoso.com。

## <a name="host-headers-and-server-name-indication-sni"></a>主機標頭和伺服器名稱指示 (SNI)

有三種常見的機制，可啟用多個站台上裝載 hello 相同基礎結構。

1. 將多個 Web 應用程式分別裝載在一個唯一的 IP 位址上。
2. 使用主機名稱 toohost hello 上的多個 web 應用程式相同的 IP 位址。
3. 使用不同連接埠 toohost hello 上的多個 web 應用程式相同的 IP 位址。

目前應用程式閘道會取得它用來接聽流量的單一公用 IP 位址。 因此，目前不支援讓多個應用程式分別擁有自己的 IP 位址。 應用程式閘道支援裝載多個應用程式每個不同的連接埠上接聽，但這種情況下需要非標準連接埠上的 hello 應用程式 tooaccept 流量，並通常不是所需的組態。 應用程式閘道依賴 HTTP 1.1 以上某個網站上的主機標頭 toohost hello 相同的公開 IP 位址和連接埠。 應用程式閘道上裝載的 hello 站台也可以使用 TLS 伺服器名稱指示 (SNI) 延伸模組支援 SSL 卸載。 此案例中，表示該 hello 用戶端瀏覽器和後端 web 伺服陣列必須支援 HTTP/1.1 和 TLS 延伸模組 RFC 6066 中所定義。

## <a name="listener-configuration-element"></a>接聽程式組態元素

組態項目是現有 HTTPListener 增強 toosupport 主機名稱和伺服器名稱指示項目，這由應用程式閘道 tooroute 流量 tooappropriate 後端集區。 hello 下列程式碼範例是 hello httplisteners 的數目的項目從範本檔案的程式碼片段。

```json
"httpListeners": [
    {
        "name": "appGatewayHttpsListener1",
        "properties": {
            "FrontendIPConfiguration": {
                "Id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/frontendIPConfigurations/DefaultFrontendPublicIP"
            },
            "FrontendPort": {
                "Id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/frontendPorts/appGatewayFrontendPort443'"
            },
            "Protocol": "Https",
            "SslCertificate": {
                "Id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/sslCertificates/appGatewaySslCert1'"
            },
            "HostName": "contoso.com",
            "RequireServerNameIndication": "true"
        }
    },
    {
        "name": "appGatewayHttpListener2",
        "properties": {
            "FrontendIPConfiguration": {
                "Id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/frontendIPConfigurations/appGatewayFrontendIP'"
            },
            "FrontendPort": {
                "Id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/frontendPorts/appGatewayFrontendPort80'"
            },
            "Protocol": "Http",
            "HostName": "fabrikam.com",
            "RequireServerNameIndication": "false"
        }
    }
],
```

您可以瀏覽[Resource Manager 範本使用多個站台裝載](https://github.com/Azure/azure-quickstart-templates/blob/master/201-application-gateway-multihosting)的結束 tooend 範本為基礎的部署。

## <a name="routing-rule"></a>路由規則

沒有任何變更，需要在 hello 路由規則。 hello 'Basic' 應該繼續選擇 toobe tootie hello 適當的站台接聽程式 toohello 對應後端位址集區的路由規則。

```json
"requestRoutingRules": [
{
    "name": "<ruleName1>",
    "properties": {
        "RuleType": "Basic",
        "httpListener": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/httpListeners/appGatewayHttpsListener1')]"
        },
        "backendAddressPool": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendAddressPools/ContosoServerPool')]"
        },
        "backendHttpSettings": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendHttpSettingsCollection/appGatewayBackendHttpSettings')]"
        }
    }

},
{
    "name": "<ruleName2>",
    "properties": {
        "RuleType": "Basic",
        "httpListener": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/httpListeners/appGatewayHttpListener2')]"
        },
        "backendAddressPool": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendAddressPools/FabrikamServerPool')]"
        },
        "backendHttpSettings": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendHttpSettingsCollection/appGatewayBackendHttpSettings')]"
        }
    }

}
]
```

## <a name="next-steps"></a>後續步驟

在了解多個站台裝載之後, 請繼續太[建立使用多個站台裝載的應用程式閘道](application-gateway-create-multisite-azureresourcemanager-powershell.md)toocreate 能力 toosupport 多超過一個 web 應用程式的應用程式閘道。

