---
title: "aaaUsing Azure 應用程式閘道與內部負載平衡器 |Microsoft 文件"
description: "本頁面提供的指示 tooconfigure Azure 應用程式閘道與內部負載平衡的端點"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 7403d28e-909f-46a2-b282-43a8e942f53c
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: 272ef84a02f92a8521c35aad6f1d9f9bf1675718
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-with-an-internal-load-balancer-ilb"></a>搭配內部負載平衡器 (ILB) 的應用程式閘道

> [!div class="op_single_selector"]
> * [Azure 傳統 PowerShell](application-gateway-ilb.md)
> * [Azure Resource Manager PowerShell](application-gateway-ilb-arm.md)

可設定應用程式閘道，與網際網路對向虛擬 IP，或使用不會公開內部端點 toohello 網際網路，也稱為內部負載平衡 (ILB) 端點。 適用於內部特定業務應用程式不會公開 toointernet 設定 hello 閘道搭配 ILB 一起運作。 它也可用於服務/層內的多層式應用程式，這位於安全性界限不會公開 toointernet，但仍然需要循環配置資源負載分佈、 神奇工作階段的結果或 SSL 終止。 這篇文章會引導您 hello 步驟 tooconfigure 應用程式閘道搭配 ILB 一起運作。

## <a name="before-you-begin"></a>開始之前

1. 安裝最新版的 hello Azure PowerShell cmdlet 使用 hello Web Platform Installer。 您可以從下載並安裝最新版本的 hello hello **Windows PowerShell**區段 hello[下載頁面](https://azure.microsoft.com/downloads/)。
2. 請確認您有運作中的虛擬網路，且其子網路有效。
3. 請確認您有後端伺服器，在 hello 虛擬網路中，或與公用 IP/VIP 指派。

toocreate 應用程式閘道，執行 hello hello 列出順序的步驟。 

1. [建立應用程式閘道](#create-a-new-application-gateway)
2. [Hello 閘道設定](#configure-the-gateway)
3. [設定 hello 閘道組態](#set-the-gateway-configuration)
4. [啟動 hello 閘道](#start-the-gateway)
5. [確認 hello 閘道](#verify-the-gateway-status)

## <a name="create-an-application-gateway"></a>建立應用程式閘道：

**toocreate hello 閘道**，使用 hello `New-AzureApplicationGateway` cmdlet，取代您自己 hello 值。 請注意計費 hello 閘道不會在此時啟動。 計費開始在稍後步驟中，當 hello 閘道已順利啟動。

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

**toovalidate**建立 hello 閘道，您可以使用 hello `Get-AzureApplicationGateway` cmdlet。 

在 hello 範例中，*描述*， *InstanceCount*，和*GatewaySize*是選擇性參數。 預設值的 hello *InstanceCount*為 2，最大值是 10。 預設值的 hello *GatewaySize*都是 Medium。 Small 和 Large 也是可用的值。 *Vip*和*DnsName*會顯示為空白，因為 hello 閘道尚未啟動。 這些被建立一旦 hello 閘道處於執行中狀態的 hello。 

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

## <a name="configure-hello-gateway"></a>Hello 閘道設定
應用程式閘道組態是由多個值所組成。 hello 值可以繫結在一起的 tooconstruct hello 組態。

hello 的值如下：

* **後端伺服器集區：** hello hello 後端伺服器的 IP 位址清單。 列出 hello IP 位址應該是屬於 toohello VNet 子網路，或應該是公用 IP/VIP。 
* **後端伺服器集區設定：** 每個集區都有一些設定，例如連接埠、通訊協定和以 Cookie 為基礎的同質性。 這些設定會繫結的 tooa 集區，並套用的 tooall hello 集區內的伺服器。
* **前端連接埠：**則 hello 公用連接埠 hello 應用程式閘道上開啟此連接埠。 叫用這個連接埠，並接著會取得 hello 後端伺服器的重新導向的 tooone。
* **接聽程式：** hello 接聽程式有前端連接埠的通訊協定 （Http 或 Https，這些是區分大小寫），與 hello 的 SSL 憑證名稱 （如果有設定 SSL 卸載）。 
* **規則：** hello 規則繫結 hello 接聽程式和 hello 後端伺服器集區，並定義哪一個後端伺服器集區 hello 流量應導向的 toowhen 配接器特定接聽程式。 目前，只有 hello*基本*規則支援。 hello*基本*規則是循環配置資源負載分佈。

建立組態物件或使用組態 XML 檔案，即可建構組態。 tooconstruct 您使用的組態 XML 檔案、 使用 hello 組態的範例如下。

請注意 hello 下列：

* hello *FrontendIPConfigurations*元素描述相關的設定搭配 ILB 一起運作的應用程式閘道的 hello ILB 詳細資料。 
* hello 前端 IP*類型*應該設定 too'Private'
* hello *StaticIPAddress*應該設定 toohello 預期的內部 IP 的 hello 閘道接收流量。 請注意該 hello *StaticIPAddress*是選擇性項目。 如果不是集合，會選擇可用的內部 IP，從部署的 hello 子網路。 
* hello 值 hello*名稱*中指定的項目*FrontendIPConfiguration*應該用於 hello HTTPListener 的*FrontendIP*元素 toorefer toohelloFrontendIPConfiguration。
  
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


## <a name="set-hello-gateway-configuration"></a>設定 hello 閘道組態
接下來，您將設定 hello 應用程式閘道。 您可以使用 hello`Set-AzureApplicationGatewayConfig`指令程式與組態物件，或設定 XML 檔案。 

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

## <a name="start-hello-gateway"></a>啟動 hello 閘道

一旦已設定 hello 閘道，使用 hello `Start-AzureApplicationGateway` cmdlet toostart hello 閘道。 在 hello 閘道已順利啟動後，就會開始計費，應用程式閘道。 

> [!NOTE]
> hello `Start-AzureApplicationGateway` cmdlet 可能會佔用 toocomplete too15 20 分鐘。 
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

## <a name="verify-hello-gateway-status"></a>驗證 hello 閘道器狀態

使用 hello `Get-AzureApplicationGateway` cmdlet toocheck hello 狀態的閘道。 如果`Start-AzureApplicationGateway`成功 hello 上一個步驟中，hello 狀態應該是*執行*，hello Vip 和 DnsName 應該具有有效的項目。 這個範例會顯示 hello cmdlet hello 第一行，後面接著 hello 輸出。 在此範例中，hello 閘道正在執行，而且已準備好 tootake 流量。 

> [!NOTE]
> hello 應用程式閘道設定為在 hello tooaccept 流量設定 10.0.0.10 ILB 端點在此範例中。

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

