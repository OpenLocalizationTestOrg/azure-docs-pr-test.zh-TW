---
title: "使用 Azure 應用程式閘道搭配內部負載平衡器 | Microsoft Docs"
description: "本頁面提供的指示可讓您使用內部負載平衡端點來設定 Azure 應用程式閘道"
documentationcenter: na
services: application-gateway
author: davidmu1
manager: timlt
editor: tysonn
ms.assetid: 7403d28e-909f-46a2-b282-43a8e942f53c
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: davidmu
ms.openlocfilehash: 7ca9307e8a78f6dade4b231fa3a0d83a68af3f21
ms.sourcegitcommit: b5c6197f997aa6858f420302d375896360dd7ceb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="create-an-application-gateway-with-an-internal-load-balancer-ilb"></a>搭配內部負載平衡器 (ILB) 的應用程式閘道

> [!div class="op_single_selector"]
> * [Azure 傳統 PowerShell](application-gateway-ilb.md)
> * [Azure Resource Manager PowerShell](application-gateway-ilb-arm.md)

可以使用面對網際網路的虛擬 IP 或不會對網際網路公開的內部端點 (也稱為內部負載平衡器 (ILB) 端點) 來設定應用程式閘道。 使用 ILB 設定閘道適合不會對網際網路公開的內部企業營運應用程式。 對於位在不會對網際網路公開的安全性界限中的多層式應用程式內的服務/階層也很有用的，但仍需要循環配置資源負載散發、工作階段綁定或 SSL 終止。 本文會逐步引導您完成使用 ILB 設定應用程式閘道。

## <a name="before-you-begin"></a>開始之前

1. 使用 Web Platform Installer 安裝最新版的 Azure PowerShell Cmdlet。 您可以從 **下載頁面** 的 [Windows PowerShell](https://azure.microsoft.com/downloads/)區段下載並安裝最新版本。
2. 請確認您有運作中的虛擬網路，且其子網路有效。
3. 請確認您的後端伺服器位於虛擬網路中，或已指派公用 IP/VIP。

若要建立應用程式閘道，請依列出的順序執行下列步驟。 

1. [建立應用程式閘道](#create-a-new-application-gateway)
2. [設定閘道](#configure-the-gateway)
3. [設定閘道組態](#set-the-gateway-configuration)
4. [啟動閘道](#start-the-gateway)
5. [確認閘道](#verify-the-gateway-status)

## <a name="create-an-application-gateway"></a>建立應用程式閘道：

**若要建立閘道**，請使用 `New-AzureApplicationGateway` Cmdlet，並以您自己的值來取代這些值。 請注意，此時不會開始為閘道計費。 會在稍後的步驟中於成功啟動閘道之後開始計費。

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

```
VERBOSE: 4:31:35 PM - Begin Operation: New-AzureApplicationGateway 
VERBOSE: 4:32:37 PM - Completed Operation: New-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error 
----       ----------------     ------------                             ----
Successful OK                   55ef0460-825d-2981-ad20-b9a8af41b399
```

**若要驗證**已建立閘道，您可以使用 `Get-AzureApplicationGateway` Cmdlet。 

在範例中，*Description*、*InstanceCount* 及 *GatewaySize* 是選用參數。 *InstanceCount* 的預設值是 2，且最大值是 10。 *GatewaySize* 的預設值是 Medium。 Small 和 Large 也是可用的值。 因為尚未啟動閘道，所以 *Vip* 和 *DnsName* 會顯示為空白。 閘道處於執行中狀態之後，就會建立這些項目。 

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 4:39:39 PM - Begin Operation:
Get-AzureApplicationGateway VERBOSE: 4:39:40 PM - Completed 
Operation: Get-AzureApplicationGateway
Name: AppGwTest    
Description: 
VnetName: testvnet1 
Subnets: {Subnet-1} 
InstanceCount: 2 
GatewaySize: Medium 
State: Stopped 
VirtualIPs: 
DnsName:
```

## <a name="configure-the-gateway"></a>設定閘道
應用程式閘道組態是由多個值所組成。 可以將值繫結在一起，以建構組態。

值如下：

* **後端伺服器集區：** 後端伺服器的 IP 位址清單。 列出的 IP 位址應該屬於 VNet 子網路，或應該是公用 IP/VIP。 
* **後端伺服器集區設定：** 每個集區都有一些設定，例如連接埠、通訊協定和以 Cookie 為基礎的同質性。 這些設定會繫結至集區，並套用至集區內所有伺服器。
* **前端連接埠：** 此連接埠是在應用程式閘道上開啟的公用連接埠。 流量會到達此連接埠，然後重新導向至其中一個後端伺服器。
* **接聽程式：** 接聽程式具有前端連接埠、通訊協定 (Http 或 Https，這些都區分大小寫) 和 SSL 憑證名稱 (如果已設定 SSL 卸載)。 
* **規則：** 規則會繫結接聽程式和後端伺服器集區，並定義當流量到達特定接聽程式時，應該導向到哪個後端伺服器集區。 目前，只支援 *基本* 規則。 「基本」  規則是循環配置資源的負載分散。

建立組態物件或使用組態 XML 檔案，即可建構組態。 若要使用組態 XML 檔案以建構組態，請使用下面的範例。

請注意：

* *FrontendIPConfigurations* 元素描述設定搭配 ILB 之應用程式閘道器的相關 ILB 詳細資料。 
* 前端 IP *類型* 應該設定為「私人」
* StaticIPAddress 應該設定為需要的內部 IP，閘道會在該處接收流量。 請注意，StaticIPAddress 元素為選擇性。 如果未設定，會選擇來自已部署子網路的可用內部 IP。 
* 在 FrontendIPConfiguration 中指定的 Name 元素的值應該用於 HTTPListener 的 FrontendIP 元素，以指向 FrontendIPConfiguration。
  
  **組態 XML 範例**
```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendIPConfigurations>
        <FrontendIPConfiguration>
            <Name>fip1</Name> 
            <Type>Private</Type> 
            <StaticIPAddress>10.0.0.10</StaticIPAddress> 
        </FrontendIPConfiguration>
    </FrontendIPConfigurations>
    <FrontendPorts>
        <FrontendPort>
            <Name>FrontendPort1</Name>
            <Port>80</Port>
        </FrontendPort>
    </FrontendPorts>
    <BackendAddressPools>
        <BackendAddressPool>
            <Name>BackendPool1</Name>
            <IPAddresses>
                <IPAddress>10.0.0.1</IPAddress>
                <IPAddress>10.0.0.2</IPAddress>
            </IPAddresses>
        </BackendAddressPool>
    </BackendAddressPools>
    <BackendHttpSettingsList>
        <BackendHttpSettings>
            <Name>BackendSetting1</Name>
            <Port>80</Port>
            <Protocol>Http</Protocol>
            <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        </BackendHttpSettings>
    </BackendHttpSettingsList>
    <HttpListeners>
        <HttpListener>
            <Name>HTTPListener1</Name>
            <FrontendIP>fip1</FrontendIP>
            <FrontendPort>FrontendPort1</FrontendPort>
            <Protocol>Http</Protocol>
        </HttpListener>
    </HttpListeners>
    <HttpLoadBalancingRules>
        <HttpLoadBalancingRule>
            <Name>HttpLBRule1</Name>
            <Type>basic</Type>
            <BackendHttpSettings>BackendSetting1</BackendHttpSettings>
            <Listener>HTTPListener1</Listener>
            <BackendAddressPool>BackendPool1</BackendAddressPool>
        </HttpLoadBalancingRule>
    </HttpLoadBalancingRules>
</ApplicationGatewayConfiguration>
```


## <a name="set-the-gateway-configuration"></a>設定閘道組態
接下來，您將設定應用程式閘道。 您可以搭配使用 `Set-AzureApplicationGatewayConfig` Cmdlet 與組態物件或組態 XML 檔案。 

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile D:\config.xml
```

```
VERBOSE: 7:54:59 PM - Begin Operation: Set-AzureApplicationGatewayConfig 
VERBOSE: 7:55:32 PM - Completed Operation: Set-AzureApplicationGatewayConfig
Name       HTTP Status Code     Operation ID                             Error 
----       ----------------     ------------                             ----
Successful OK                   9b995a09-66fe-2944-8b67-9bb04fcccb9d
```

## <a name="start-the-gateway"></a>啟動閘道

設定閘道之後，請使用 `Start-AzureApplicationGateway` Cmdlet 來啟動閘道。 成功啟動閘道之後，會開始應用程式閘道計費。 

> [!NOTE]
> 「基本」 `Start-AzureApplicationGateway` Cmdlet 最多可能需要 15 到 20 分鐘才能完成。 
> 
> 

```powershell
Start-AzureApplicationGateway AppGwTest 
```

```
VERBOSE: 7:59:16 PM - Begin Operation: Start-AzureApplicationGateway 
VERBOSE: 8:05:52 PM - Completed Operation: Start-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error 
----       ----------------     ------------                             ----
Successful OK                   fc592db8-4c58-2c8e-9a1d-1c97880f0b9b
```

## <a name="verify-the-gateway-status"></a>確認閘道狀態

使用 `Get-AzureApplicationGateway` Cmdlet 來檢查閘道狀態。 如果上一個步驟中的 `Start-AzureApplicationGateway` 成功，則 State 應該是 Running，而且 Vip 和 DnsName 應該具備有效的輸入。 這個範例的第一行顯示 Cmdlet，後面接著輸出。 在此範例中，閘道正在執行，且準備好要接受流量。 

> [!NOTE]
> 此範例中是將應用程式閘道器設定為在所設定的 ILB 端點 10.0.0.10 接受流量。

```powershell
Get-AzureApplicationGateway AppGwTest 
```

```
VERBOSE: 8:09:28 PM - Begin Operation: Get-AzureApplicationGateway 
VERBOSE: 8:09:30 PM - Completed Operation: Get-AzureApplicationGateway
Name          : AppGwTest
Description   : 
VnetName      : testvnet1
Subnets       : {Subnet-1}
InstanceCount : 2
GatewaySize   : Medium
State         : Running
VirtualIPs    : {10.0.0.10}
DnsName       : appgw-b2a11563-2b3a-4172-a4aa-226ee4c23eed.cloudapp.net
```

## <a name="next-steps"></a>後續步驟
如果您想進一步了解一般負載平衡選項，請參閱：

* [Azure 負載平衡器](https://azure.microsoft.com/documentation/services/load-balancer/)
* [Azure 流量管理員](https://azure.microsoft.com/documentation/services/traffic-manager/)

