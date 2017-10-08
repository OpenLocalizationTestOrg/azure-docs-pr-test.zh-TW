---
title: "aaaMonitor 應用程式閘道存取記錄檔、 效能記錄檔、 後端健全狀況和度量 |Microsoft 文件"
description: "深入了解如何 tooenable 及管理的應用程式閘道存取記錄檔與效能記錄檔"
services: application-gateway
documentationcenter: na
author: amitsriva
manager: rossort
editor: tysonn
tags: azure-resource-manager
ms.assetid: 300628b8-8e3d-40ab-b294-3ecc5e48ef98
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/17/2017
ms.author: amitsriva
ms.openlocfilehash: 36ebf15c28f776158350ef8e73d617ef68e09266
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="back-end-health-diagnostic-logs-and-metrics-for-application-gateway"></a>應用程式閘道的後端健康情況、診斷記錄和計量

藉由使用 Azure 應用程式閘道，您可以監視下列方式 hello 中的資源：

* [後端健全狀況](#back-end-health)： 應用程式閘道提供 hello 功能 toomonitor hello 伺服器的健全狀況 hello hello 中透過 hello Azure 入口網站，以及透過 PowerShell 的後端集區。 您也可以尋找 hello hello 透過 hello 效能診斷記錄檔的後端集區的健全狀況。

* [記錄檔](#diagnostic-logs)： 記錄檔可供存取的效能，以及其他資料 toobe 儲存，或從監視所需的資源耗用。

* [計量](#metrics)：應用程式閘道目前有一個計量。 此標準會測量 hello 的 hello 應用程式閘道，以位元組為單位，每秒的輸送量。

## <a name="back-end-health"></a>後端健康情況

應用程式閘道提供 hello 功能 toomonitor hello 健全狀況的 hello 透過 hello 入口網站、 PowerShell 和 hello 命令列介面 (CLI) 的後端集區的個別成員。 您也可以尋找彙總的健全狀況摘要透過 hello 效能診斷記錄檔的後端集區。 

hello 後端健全狀況報表會反映 hello hello 應用程式閘道健全狀況探查 toohello 後端執行個體輸出。 當探查成功回 hello 結束可以接收流量，則會視為狀況良好。 否則，視為狀況不良。

> [!IMPORTANT]
> 如果沒有在應用程式閘道子網路上的網路安全性群組 (NSG)，開啟 輸入流量的 hello 應用程式閘道子網路上的連接埠範圍 65503 65534。 這些連接埠不需要 hello 後端健全狀況 API toowork。


### <a name="view-back-end-health-through-hello-portal"></a>檢視透過 hello 入口網站的後端健全狀況

Hello 入口網站中，會自動提供後端健全狀況。 在現有的應用程式閘道中，選取 [監視]  >  [後端健康情況]。 

Hello 後端集區中的每個成員會列在此頁面中，（其是否 NIC，IP 或 FQDN）。 後端集區名稱、連接埠、後端 HTTP 設定名稱和健康情況均會顯示。 健康情況的有效值為「狀況良好」、「狀況不良」和「未知」。

> [!NOTE]
> 如果您看到的後端健全狀況狀態的**未知**，請確定該存取 toohello 後端不會遭到 NSG 規則、 使用者定義的路由 (UDR) 或自訂 DNS hello 虛擬網路中的。

![後端健康情況][10]

### <a name="view-back-end-health-through-powershell"></a>透過 PowerShell 檢視後端健康情況

hello 下列 PowerShell 程式碼會示範如何使用 tooview 後端健全狀況 hello `Get-AzureRmApplicationGatewayBackendHealth` cmdlet:

```powershell
Get-AzureRmApplicationGatewayBackendHealth -Name ApplicationGateway1 -ResourceGroupName Contoso
```

### <a name="view-back-end-health-through-azure-cli-20"></a>透過 Azure CLI 2.0 檢視後端健康情況

```azurecli
az network application-gateway show-backend-health --resource-group AdatumAppGatewayRG --name AdatumAppGateway
```

### <a name="results"></a>結果

下列程式碼片段的 hello 顯示 hello 回應的範例：

```json
{
"BackendAddressPool": {
    "Id": "/subscriptions/00000000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendAddressPools/appGatewayBackendPool"
},
"BackendHttpSettingsCollection": [
    {
    "BackendHttpSettings": {
        "Id": "/00000000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendHttpSettingsCollection/appGatewayBackendHttpSettings"
    },
    "Servers": [
        {
        "Address": "hostname.westus.cloudapp.azure.com",
        "Health": "Healthy"
        },
        {
        "Address": "hostname.westus.cloudapp.azure.com",
        "Health": "Healthy"
        }
    ]
    }
]
}
```

## <a name="diagnostic-logging"></a>診斷記錄

您可以在 Azure toomanage 中使用不同類型的記錄檔和疑難排解應用程式閘道。 您可以透過 hello 入口網站存取這些記錄檔部份。 可以從 Azure Blob 儲存體擷取所有記錄，並且在不同的工具中進行檢視 (例如 [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md)、Excel、PowerBI)。 您可以深入了解 hello 來自不同類型的記錄檔清單後面的 hello:

* **活動記錄檔**： 您可以使用[Azure 活動記錄檔](../monitoring-and-diagnostics/insights-debugging-with-events.md)（以前稱為操作記錄檔和稽核記錄檔） tooview 所有作業都提交 tooyour Azure 訂用帳戶，以及它們的狀態。 活動記錄檔項目會根據預設，收集和 hello Azure 入口網站中進行檢視。
* **存取記錄檔**： 您可以使用此記錄 tooview 應用程式閘道存取模式和分析的重要資訊，包括 hello 呼叫者的 IP、 要求的 URL、 回應延遲，傳回碼和位元組和縮小。每隔 300 秒會收集一次存取記錄。 此記錄檔包含每個應用程式閘道執行個體的一筆記錄。 hello 應用程式閘道執行個體可以 hello instanceId 屬性的識別。
* **效能記錄**： 您可以使用此應用程式閘道器執行個體的執行方式的記錄檔 tooview。 此記錄會擷取每個執行個體的效能資訊，包括提供的要求總數、輸送量 (以位元組為單位)、提供的總要求數、失敗的要求計數、狀況良好和狀況不良的後端執行個體計數。 每隔 60 秒會收集一次效能記錄。
* **防火牆記錄**： 您可以使用透過偵測或防止應用程式閘道以 hello web 應用程式的防火牆設定的模式會記錄這個記錄 tooview hello 的要求。

> [!NOTE]
> 記錄是僅供部署在 hello Azure Resource Manager 部署模型中的資源。 您無法使用記錄檔 hello 傳統部署模型中的資源。 進一步了解 hello 兩個模型，請參閱 hello[了解資源管理員部署和傳統部署](../azure-resource-manager/resource-manager-deployment-model.md)發行項。

您有三個選項可用來排序您的記錄：

* **儲存體帳戶**：如果記錄會儲存一段較長的持續期間，並在需要時加以檢閱，則最好針對記錄使用儲存體帳戶。
* **事件中心**： 事件中心是絕佳的選項與其他安全性資訊整合與事件管理 (SEIM) 工具 tooget 警示，您的資源。
* **Log Analytics**：Log Analytics 最適合用來進行應用程式的一般即時監視，或查看趨勢。

### <a name="enable-logging-through-powershell"></a>透過 PowerShell 啟用記錄功能

每個 Resource Manager 資源都會自動啟用活動記錄功能。 您必須啟用存取和效能記錄 toostart 收集 hello 資料可透過這些記錄檔。 tooenable 記錄、 使用 hello 下列步驟：

1. 請注意 hello 記錄資料的儲存位置的儲存體帳戶的資源識別碼。 此值為 hello 格式： /subscriptions/\<subscriptionId\>/resourceGroups/\<資源群組名稱\>/providers/Microsoft.Storage/storageAccounts/\<的儲存體帳戶名稱\>. 您可以使用訂用帳戶中的所有儲存體帳戶。 您可以使用 Azure 入口網站 toofind hello 這項資訊。

    ![入口網站：儲存體帳戶的資源識別碼](./media/application-gateway-diagnostics/diagnostics1.png)

2. 請記下您的應用程式閘道的資源識別碼 (將為其啟用記錄功能)。 此值為 hello 格式： /subscriptions/\<subscriptionId\>/resourceGroups/\<資源群組名稱\>/providers/Microsoft.Network/applicationGateways/\<應用程式閘道名稱\>。 您可以使用 hello 入口 toofind 這項資訊。

    ![入口網站：應用程式閘道的資源識別碼](./media/application-gateway-diagnostics/diagnostics2.png)

3. 使用下列 PowerShell cmdlet 的 hello 啟用診斷記錄：

    ```powershell
    Set-AzureRmDiagnosticSetting  -ResourceId /subscriptions/<subscriptionId>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name> -StorageAccountId /subscriptions/<subscriptionId>/resourceGroups/<resource group name>/providers/Microsoft.Storage/storageAccounts/<storage account name> -Enabled $true     
    ```
    
> [!TIP] 
>活動記錄檔不需要個別的儲存體帳戶。 hello 使用儲存體的存取和效能記錄不會產生服務費用。

### <a name="enable-logging-through-hello-azure-portal"></a>啟用記錄 hello 透過 Azure 入口網站

1. 在 hello Azure 入口網站，尋找您的資源，然後按一下**診斷記錄**。

   應用程式閘道有三個記錄：

   * 存取記錄檔
   * 效能記錄檔
   * 防火牆記錄檔

2. toostart 收集資料，按一下**開啟診斷**。

   ![開啟診斷][1]

3. hello**診斷設定**刀鋒視窗中提供的 hello hello 設定診斷記錄檔。 在此範例中，記錄分析儲存 hello 記錄檔。 按一下**設定**下**記錄分析**tooconfigure 您的工作區。 您也可以使用事件中樞與儲存體帳戶 toosave hello 診斷記錄。

   ![啟動 hello 組態程序][2]

4. 選擇現有的 Operations Management Suite (OMS) 工作區或建立新的。 這個範例使用現有工作區。

   ![OMS 工作區的選項][3]

5. 確認 hello 設定然後按一下**儲存**。

   ![診斷設定刀鋒視窗與選項][4]

### <a name="activity-log"></a>活動記錄檔

根據預設，azure 會產生 hello 活動記錄檔。 hello 記錄檔會保留 90 天，hello Azure 事件記錄檔存放區中。 深入了解這些記錄檔讀取 hello[檢視事件和活動記錄檔](../monitoring-and-diagnostics/insights-debugging-with-events.md)發行項。

### <a name="access-log"></a>存取記錄檔

只有當您已將它啟用每個應用程式閘道執行個體上，hello 先前步驟中所述，會產生 hello 存取記錄。 hello 資料會儲存在您指定當您啟用 hello 記錄 hello 儲存體帳戶。 每次存取的應用程式閘道會記錄 JSON 格式 hello 下列範例所示：


|值  |說明  |
|---------|---------|
|instanceId     | 應用程式閘道執行個體提供的 hello 要求。        |
|clientIP     | Hello 要求的原始 IP。        |
|clientPort     | Hello 要求的原始連接埠。       |
|httpMethod     | Hello 要求所使用的 HTTP 方法。       |
|requestUri     | Hello 接收到要求的 URI。        |
|RequestQuery     | **伺服器路由**： 已傳送嗨要求的後端集區執行個體。 </br> **X AzureApplicationGateway-記錄識別碼**: hello 要求使用的相互關聯識別碼。 它可以是使用的 tootroubleshoot hello 後端伺服器上的流量問題。 </br>**伺服器狀態**： 應用程式閘道收到 hello 後端的 HTTP 回應碼。       |
|UserAgent     | Hello HTTP 要求標頭中的使用者代理程式。        |
|httpStatus     | 從應用程式閘道 toohello 用戶端傳回 HTTP 狀態碼。       |
|httpVersion     | Hello 要求的 HTTP 版本。        |
|receivedBytes     | 接收的封包大小，單位為位元組。        |
|sentBytes| 傳送的封包大小，單位為位元組。|
|timeTaken| 處理要求 toobe 並傳送其回應 toobe 的時間 （以毫秒為單位） 的長度。 這被計算為從應用程式閘道當收到 hello 回應 hello 當傳送作業完成 HTTP 要求 toohello 時間第一個位元組的 hello 時間 hello 間隔。 請務必通常 hello 花費的時間欄位的 toonote 包含 hello hello 要求和回應封包在出差 hello 網路上的時間。 |
|sslEnabled| 是否通訊 toohello 後端集區會使用 SSL。 有效值為 on 和 off。|
```json
{
    "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/PEERINGTEST/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{applicationGatewayName}",
    "operationName": "ApplicationGatewayAccess",
    "time": "2017-04-26T19:27:38Z",
    "category": "ApplicationGatewayAccessLog",
    "properties": {
        "instanceId": "ApplicationGatewayRole_IN_0",
        "clientIP": "191.96.249.97",
        "clientPort": 46886,
        "httpMethod": "GET",
        "requestUri": "/phpmyadmin/scripts/setup.php",
        "requestQuery": "X-AzureApplicationGateway-CACHE-HIT=0&SERVER-ROUTED=10.4.0.4&X-AzureApplicationGateway-LOG-ID=874f1f0f-6807-41c9-b7bc-f3cfa74aa0b1&SERVER-STATUS=404",
        "userAgent": "-",
        "httpStatus": 404,
        "httpVersion": "HTTP/1.0",
        "receivedBytes": 65,
        "sentBytes": 553,
        "timeTaken": 205,
        "sslEnabled": "off"
    }
}
```

### <a name="performance-log"></a>效能記錄檔

只有當 hello 先前步驟中有詳細說明每個應用程式閘道執行個體上啟用它，就會產生 hello 效能記錄。 hello 資料會儲存在您指定當您啟用 hello 記錄 hello 儲存體帳戶。 hello 效能記錄資料會產生每隔 1 分鐘。 會記錄下列資料的 hello:


|值  |說明  |
|---------|---------|
|instanceId     |  將產生此應用程式閘道執行個體的效能資料。 應用程式閘道若有多個執行個體，則是一個執行個體一行資料。        |
|healthyHostCount     | 狀況良好 hello 後端集區中的主機數目。        |
|unHealthyHostCount     | 狀況不良 hello 後端集區中的主機數目。        |
|requestCount     | 處理的要求數目。        |
|latency | Hello 執行個體 toohello 來自要求的延遲時間 （以毫秒為單位） 後端服務 hello 要求。 |
|failedRequestCount| 失敗的要求數目。|
|throughput| 由於 hello 最後一個記錄，以每秒位元組為單位的平均輸送量。|

```json
{
    "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/{resourceGroupName}/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{applicationGatewayName}",
    "operationName": "ApplicationGatewayPerformance",
    "time": "2016-04-09T00:00:00Z",
    "category": "ApplicationGatewayPerformanceLog",
    "properties":
    {
        "instanceId":"ApplicationGatewayRole_IN_1",
        "healthyHostCount":"4",
        "unHealthyHostCount":"0",
        "requestCount":"185",
        "latency":"0",
        "failedRequestCount":"0",
        "throughput":"119427"
    }
}
```

> [!NOTE]
> 延遲會計算從 hello hello hello HTTP 要求第一個位元組收到的 toohello 什麼時候是當傳送 hello 最後一個位元組的 hello HTTP 回應的時間。 它的 hello 總和 hello 應用程式閘道處理時間，加上 hello 回網路成本 toohello 結束，再加上 hello hello 後端採用 tooprocess hello 要求的時間。

### <a name="firewall-log"></a>防火牆記錄檔

只有當您已啟用每個應用程式閘道，hello 先前步驟中所述，會產生 hello 防火牆記錄。 此記錄檔也會需要 hello web 應用程式防火牆應用程式閘道上設定。 hello 資料會儲存在您指定當您啟用 hello 記錄 hello 儲存體帳戶。 會記錄下列資料的 hello:


|值  |說明  |
|---------|---------|
|instanceId     | 將產生此應用程式閘道執行個體的防火牆資料。 應用程式閘道若有多個執行個體，則是一個執行個體一行資料。         |
|clientIp     |   Hello 要求的原始 IP。      |
|clientPort     |  Hello 要求的原始連接埠。       |
|requestUri     | Hello 接收到要求的 URL。       |
|ruleSetType     | 規則集類型。 hello 可用的值是 OWASP。        |
|ruleSetVersion     | 規則集版本。 可用值為 2.2.9 和 3.0。     |
|ruleId     | 規則識別碼 hello 觸發事件。        |
|Message     | 使用者易記的 hello 觸發事件的詳細訊息。 Hello 詳細資料 區段中提供更多詳細資料。        |
|動作     |  Hello 要求上採取的動作。 可用的值為 Blocked 和 Allowed。      |
|site     | 記錄檔產生哪些 hello 站台。 目前只列出 Global，因為規則為全域。|
|詳細資料     | Hello 觸發事件的詳細資料。        |
|details.message     | Hello 規則的描述。        |
|details.data     | 在要求中發現的特定資料該相符的 hello 規則。         |
|details.file     | Hello 規則所包含的組態檔。        |
|details.line     | Hello 觸發 hello 事件的組態檔中的行號。       |

```json
{
  "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/{resourceGroupName}/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{applicationGatewayName}",
  "operationName": "ApplicationGatewayFirewall",
  "time": "2017-03-20T15:52:09.1494499Z",
  "category": "ApplicationGatewayFirewallLog",
  "properties": {
    "instanceId": "ApplicationGatewayRole_IN_0",
    "clientIp": "104.210.252.3",
    "clientPort": "4835",
    "requestUri": "/?a=%3Cscript%3Ealert(%22Hello%22);%3C/script%3E",
    "ruleSetType": "OWASP",
    "ruleSetVersion": "3.0",
    "ruleId": "941320",
    "message": "Possible XSS Attack Detected - HTML Tag Handler",
    "action": "Blocked",
    "site": "Global",
    "details": {
      "message": "Warning. Pattern match \"<(a|abbr|acronym|address|applet|area|audioscope|b|base|basefront|bdo|bgsound|big|blackface|blink|blockquote|body|bq|br|button|caption|center|cite|code|col|colgroup|comment|dd|del|dfn|dir|div|dl|dt|em|embed|fieldset|fn|font|form|frame|frameset|h1|head|h ...\" at ARGS:a.",
      "data": "Matched Data: <script> found within ARGS:a: <script>alert(\\x22hello\\x22);</script>",
      "file": "rules/REQUEST-941-APPLICATION-ATTACK-XSS.conf",
      "line": "865"
    }
  }
} 

```

### <a name="view-and-analyze-hello-activity-log"></a>檢視及分析 hello 活動記錄檔

您可以檢視並分析活動記錄資料使用任何 hello 下列方法：

* **Azure tools**： 從 Azure PowerShell，hello Azure CLI，hello Azure REST API，透過 hello 活動記錄檔中擷取資訊或 hello Azure 入口網站。 每個方法的逐步指示的詳細 hello[活動作業與資源管理員](../azure-resource-manager/resource-group-audit.md)發行項。
* **Power BI**：如果還沒有 [Power BI](https://powerbi.microsoft.com/pricing) 帳戶，您可以免費試用。 使用 hello [Power BI 的 Azure 活動記錄內容套件](https://powerbi.microsoft.com/en-us/documentation/powerbi-content-pack-azure-audit-logs/)，您可以分析資料與預先設定，您可以使用，或自訂儀表板。

### <a name="view-and-analyze-hello-access-performance-and-firewall-logs"></a>檢視及分析 hello 存取、 效能及防火牆記錄檔

Azure[記錄分析](../log-analytics/log-analytics-azure-networking-analytics.md)可以從 Blob 儲存體帳戶收集 hello 計數器和事件記錄檔。 它包括視覺效果和強大的搜尋功能 tooanalyze 記錄檔。

您也可以連接 tooyour 儲存體帳戶，並擷取 hello JSON 記錄項目，以存取和效能記錄檔。 下載 hello JSON 檔案之後，您可以將它們轉換 tooCSV，並在 Excel、 Power BI 中或任何其他資料視覺效果工具中檢視它們。

> [!TIP]
> 如果您熟悉 Visual Studio 和變更值的常數和變數在 C# 中的基本概念，您可以使用 hello[記錄轉換器工具](https://github.com/Azure-Samples/networking-dotnet-log-converter)可從 GitHub 取得。
> 
> 

## <a name="metrics"></a>度量

度量是特定的 Azure 資源，您可以檢視效能計數器 hello 入口網站中的功能。 目前應用程式閘道只有一個計量。 此度量是輸送量，以及您可以在 hello 入口網站中看到它。 瀏覽 tooan 應用程式閘道並按一下**度量**。 tooview hello 值選取輸送量 hello**可用的度量**> 一節。 在下列映像的 hello，您可以看到 hello 篩選器，您可以在不同的時間範圍內使用 toodisplay hello 資料範例。

![計量與篩選器的檢視][5]

toosee 目前清單的度量資訊，請參閱[支援的 Azure 監視的度量](../monitoring-and-diagnostics/monitoring-supported-metrics.md)。

### <a name="alert-rules"></a>警示規則

您可以根據資源的計量來啟動警示規則。 例如，警示可以呼叫 webhook 或電子郵件系統管理員，如果 hello hello 應用程式閘道輸送量之上、 之下，或在臨界值是在指定期間內。

下列範例中的 hello 會引導您建立警示規則之後輸送量違反的臨界值所傳送的電子郵件 tooan 系統管理員：

1. 按一下**新增度量的警示**tooopen hello**加入規則**刀鋒視窗。 您也可以連線到此刀鋒視窗中的 hello 度量 刀鋒視窗。

   ![新增計量警示按鈕][6]

2. 在 hello**加入規則**刀鋒視窗中，填寫 hello 名稱、 條件，並通知區段中，然後按一下**確定**。

   * 在 hello**條件**選取器，選取其中一個 hello 四個值：**大於**，**大於或等於**，**小於**，或**小於或等於**。

   * 在 hello**期間**選取器選取的期間 5 分鐘 too6 小時。

   * 如果您選取**電子郵件擁有者、 參與者與讀者**，hello 電子郵件可以有動態 hello 使用者擁有存取 toothat 資源為基礎。 否則，您可以提供以逗號分隔的使用者清單中 hello**其他的系統管理員 email(s)**方塊。

   ![新增規則刀鋒視窗][7]

如果達到 hello 閾值時，會在下列映像的 hello 類似 toohello 一封電子郵件送達：

![違反臨界值的電子郵件][8]

建立計量警示之後，就會出現警示的清單， 它提供所有 hello 警示規則的概觀。

![警示和規則的清單][9]

toolearn 進一步了解警示通知，請參閱[接收警示通知](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)。

toounderstand 進一步了解 webhook 及如何使用這些警示，請瀏覽[Azure 度量警示上設定的 webhook](../monitoring-and-diagnostics/insights-webhooks-alerts.md)。

## <a name="next-steps"></a>後續步驟

* 利用 [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md) 將計數器和事件記錄視覺化。
* [使用 Power BI 將您的 Azure 活動記錄視覺化](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx)部落格文章。
* [在 Power BI 和其他工具中檢視和分析 Azure 活動記錄](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/)部落格文章。

[1]: ./media/application-gateway-diagnostics/figure1.png
[2]: ./media/application-gateway-diagnostics/figure2.png
[3]: ./media/application-gateway-diagnostics/figure3.png
[4]: ./media/application-gateway-diagnostics/figure4.png
[5]: ./media/application-gateway-diagnostics/figure5.png
[6]: ./media/application-gateway-diagnostics/figure6.png
[7]: ./media/application-gateway-diagnostics/figure7.png
[8]: ./media/application-gateway-diagnostics/figure8.png
[9]: ./media/application-gateway-diagnostics/figure9.png
[10]: ./media/application-gateway-diagnostics/figure10.png
