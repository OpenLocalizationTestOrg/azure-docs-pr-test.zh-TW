---
title: "自訂探查-Azure 應用程式閘道-PowerShell 傳統 aaaCreate |Microsoft 文件"
description: "了解如何 toocreate 自訂探查應用程式閘道在 hello 傳統部署模型中使用 PowerShell"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 338a7be1-835c-48e9-a072-95662dc30f5e
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: gwallace
ms.openlocfilehash: 68332367c99328bd6456b0c339923765637be986
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-probe-for-azure-application-gateway-classic-by-using-powershell"></a>使用 PowerShell 建立 Azure 應用程式閘道 (傳統) 的自訂探查

> [!div class="op_single_selector"]
> * [Azure 入口網站](application-gateway-create-probe-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-create-probe-ps.md)
> * [Azure 傳統 PowerShell](application-gateway-create-probe-classic-ps.md)

在本文中，您可以加入自訂探查 tooan 現有應用程式閘道使用 PowerShell。 自訂探查適合應用程式的健全狀況檢查 頁面，或未提供成功的回應 hello 預設 web 應用程式的應用程式。

> [!IMPORTANT]
> Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。 本文件涵蓋使用 hello 傳統部署模型。 Microsoft 建議最新的部署使用 hello 資源管理員的模型。 了解如何太[使用 hello 資源管理員的模型執行這些步驟](application-gateway-create-probe-ps.md)。

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-application-gateway"></a>建立應用程式閘道

toocreate 應用程式閘道：

1. 建立應用程式閘道資源。
2. 建立設定 XML 檔案或設定物件。
3. 認可新建立的應用程式閘道資源 hello 組態 toohello。

### <a name="create-an-application-gateway-resource-with-a-custom-probe"></a>使用自訂探查建立應用程式閘道資源

toocreate hello 閘道，使用 hello `New-AzureApplicationGateway` cmdlet，取代您自己 hello 值。 此時無法啟動的 hello 閘道計費。 計費開始在稍後步驟中，當 hello 閘道已順利啟動。

hello 下列範例會建立應用程式閘道使用名為"testvnet1"，稱為 「 子網路-1"的子網路的虛擬網路。

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

hello 閘道的 toovalidate 所建立，您可以使用 hello `Get-AzureApplicationGateway` cmdlet。

```powershell
Get-AzureApplicationGateway AppGwTest
```

> [!NOTE]
> 預設值的 hello *InstanceCount*為 2，最大值是 10。 預設值的 hello *GatewaySize*都是 Medium。 您可以選擇 Small、Medium 和 Large。
> 
> 

*如*和*DnsName*會顯示為空白，因為 hello 閘道尚未啟動。 執行中狀態的 hello hello 閘道之後，會建立這些值。

### <a name="configure-an-application-gateway-by-using-xml"></a>使用 XML 設定應用程式閘道

在下列範例的 hello，您可以使用 XML 檔案 tooconfigure 所有應用程式閘道設定，並認可 toohello 應用程式閘道資源。  

複製下列文字 tooNotepad hello。

```xml
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
<FrontendIPConfigurations>
    <FrontendIPConfiguration>
        <Name>fip1</Name>
        <Type>Private</Type>
    </FrontendIPConfiguration>
</FrontendIPConfigurations>
<FrontendPorts>
    <FrontendPort>
        <Name>port1</Name>
        <Port>80</Port>
    </FrontendPort>
</FrontendPorts>
<Probes>
    <Probe>
        <Name>Probe01</Name>
        <Protocol>Http</Protocol>
        <Host>contoso.com</Host>
        <Path>/path/custompath.htm</Path>
        <Interval>15</Interval>
        <Timeout>15</Timeout>
        <UnhealthyThreshold>5</UnhealthyThreshold>
    </Probe>
    </Probes>
    <BackendAddressPools>
    <BackendAddressPool>
        <Name>pool1</Name>
        <IPAddresses>
            <IPAddress>1.1.1.1</IPAddress>
            <IPAddress>2.2.2.2</IPAddress>
        </IPAddresses>
    </BackendAddressPool>
</BackendAddressPools>
<BackendHttpSettingsList>
    <BackendHttpSettings>
        <Name>setting1</Name>
        <Port>80</Port>
        <Protocol>Http</Protocol>
        <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        <RequestTimeout>120</RequestTimeout>
        <Probe>Probe01</Probe>
    </BackendHttpSettings>
</BackendHttpSettingsList>
<HttpListeners>
    <HttpListener>
        <Name>listener1</Name>
        <FrontendIP>fip1</FrontendIP>
    <FrontendPort>port1</FrontendPort>
        <Protocol>Http</Protocol>
    </HttpListener>
</HttpListeners>
<HttpLoadBalancingRules>
    <HttpLoadBalancingRule>
        <Name>lbrule1</Name>
        <Type>basic</Type>
        <BackendHttpSettings>setting1</BackendHttpSettings>
        <Listener>listener1</Listener>
        <BackendAddressPool>pool1</BackendAddressPool>
    </HttpLoadBalancingRule>
</HttpLoadBalancingRules>
</ApplicationGatewayConfiguration>
```

編輯 hello hello 設定項目的 hello 括號之間的值。 儲存副檔名的.xml hello 檔案。

hello 下列範例顯示如何 toouse 向上 hello 應用程式閘道 tooload 組態檔案 tooset 平衡公用連接埠 80 上的 HTTP 流量和使用自訂探查的兩個 IP 位址之間的 tooback 結束連接埠 80 傳送網路流量。

> [!IMPORTANT]
> Http 或 Https 的 hello 通訊協定項目會區分大小寫。

新的設定項目\<探查\>加入 tooconfigure 自訂探查。

hello 設定參數如下：

|參數|說明|
|---|---|
|**名稱** |自訂探查的參考名稱。 |
* **Protocol** | 使用的通訊協定 (可能的值是 HTTP 或 HTTPS)。|
| **Host** 和 **Path** | 叫用由 hello 應用程式閘道 toodetermine hello 健康嗨執行個體的完整 URL 路徑。 比方說，如果您有網站 http://contoso.com/，請 hello 自訂探查可設定為"http://contoso.com/path/custompath.htm"探查檢查 toohave 成功的 HTTP 回應。|
| **間隔** | 設定 hello 探查間隔檢查，以秒為單位。|
| **逾時** | 定義 HTTP 回應檢查 hello 探查逾時。|
| **UnhealthyThreshold** | hello 需要 tooflag hello 後端執行個體標示為失敗的 HTTP 回應數*不良*。|

hello 探查名稱會參考 hello \<BackendHttpSettings\>組態 tooassign 哪一個後端集區會使用自訂探查設定。

## <a name="add-a-custom-probe-tooan-existing-application-gateway"></a>新增自訂探查 tooan 現有應用程式閘道

變更 hello 目前組態的應用程式閘道需要三個步驟： 取得 hello 目前的 XML 組態檔、 修改 toohave 自訂探查，和 hello 應用程式閘道設定為使用 hello 新的 XML 設定。

1. 取得 hello XML 檔案使用`Get-AzureApplicationGatewayConfig`。 此指令程式匯出 hello 組態 XML toobe 修改 tooadd 探查設定。

  ```powershell
  Get-AzureApplicationGatewayConfig -Name "<application gateway name>" -Exporttofile "<path toofile>"
  ```

1. 在文字編輯器中開啟 hello XML 檔案。 在 `<frontendport>` 之後新增 `<probe>` 區段。

  ```xml
<Probes>
    <Probe>
        <Name>Probe01</Name>
        <Protocol>Http</Protocol>
        <Host>contoso.com</Host>
        <Path>/path/custompath.htm</Path>
        <Interval>15</Interval>
        <Timeout>15</Timeout>
        <UnhealthyThreshold>5</UnhealthyThreshold>
    </Probe>
</Probes>
  ```

  中的 hello XML hello backendHttpSettings 區段中，加入 hello 探查名稱 hello 下列範例所示：

  ```xml
    <BackendHttpSettings>
        <Name>setting1</Name>
        <Port>80</Port>
        <Protocol>Http</Protocol>
        <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        <RequestTimeout>120</RequestTimeout>
        <Probe>Probe01</Probe>
    </BackendHttpSettings>
  ```

  儲存 hello XML 檔。

1. 更新 hello 應用程式與 hello 新的 XML 檔案使用的閘道設定`Set-AzureApplicationGatewayConfig`。 此 cmdlet 會更新您的應用程式閘道 hello 新組態。

```powershell
Set-AzureApplicationGatewayConfig -Name "<application gateway name>" -Configfile "<path toofile>"
```

## <a name="next-steps"></a>後續步驟

如果您想的 tooconfigure Secure Sockets Layer (SSL) 卸載時，請參閱[設定 SSL 卸載的應用程式閘道](application-gateway-ssl.md)。

如果您想 tooconfigure 內部負載平衡器的應用程式閘道 toouse，請參閱[內部負載平衡器 (ILB) 建立應用程式閘道](application-gateway-ilb.md)。

