---
title: "aaaAzure 監視 REST API 逐步解說 |Microsoft 文件"
description: "如何 tooauthenticate 要求 tooand 使用 hello Azure 監視的 REST API。"
author: mcollier
manager: 
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 565e6a88-3131-4a48-8b82-3effc9a3d5c6
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/27/2016
ms.author: mcollier
ms.openlocfilehash: b8ae3a03fd21af872f1dc5fed40a101a24ca1652
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-monitoring-rest-api-walkthrough"></a>Azure 監視 REST API 逐步解說
本文章將示範如何讓您的程式碼可以使用 hello tooperform 驗證[Microsoft Azure 監視 REST API 參考](https://msdn.microsoft.com/library/azure/dn931943.aspx)。         

hello Azure 監視應用程式開發介面可讓您可能 tooprogrammatically 擷取 hello 可用預設度量定義 （例如 CPU 時間、 要求 」 等標準的 hello 類型），資料粒度，度量值。 擷取之後，hello 資料可以儲存在個別的資料存放區，例如 Azure SQL Database、 Azure Cosmos DB 或 Azure Data Lake 中。 其他分析可視需要從該處執行。

除了使用不同的度量資料點，如本文所示，hello 監視應用程式開發介面可讓可能 toolist 警示規則、 檢視活動記錄檔，以及執行更多。 如需可用作業的完整清單，請參閱 hello [Microsoft Azure 監視 REST API 參考](https://msdn.microsoft.com/library/azure/dn931943.aspx)。

## <a name="authenticating-azure-monitor-requests"></a>驗證 Azure 監視器要求
hello 第一個步驟是 tooauthenticate hello 要求。

針對 hello Azure 監視應用程式開發介面使用 hello Azure 資源管理員驗證模型所執行的所有 hello 工作。 因此，所有要求都必須使用 Azure Active Directory (Azure AD) 進行驗證。 一種方法 tooauthenticate hello 用戶端應用程式是 toocreate Azure AD 服務主體，和擷取 hello 驗證 (JWT) 權杖。 hello 下列範例指令碼將示範如何建立 Azure AD 服務主體，透過 PowerShell。 更詳細的逐步解說，請參閱 toohello 文件，在[服務主體 tooaccess 資源使用 Azure PowerShell toocreate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-password)。 此外，也可以太[建立服務主體 hello Azure 入口網站透過](../azure-resource-manager/resource-group-create-service-principal-portal.md)。

```PowerShell
$subscriptionId = "{azure-subscription-id}"
$resourceGroupName = "{resource-group-name}"
$location = "centralus"

# Authenticate tooa specific Azure subscription.
Login-AzureRmAccount -SubscriptionId $subscriptionId

# Password for hello service principal
$pwd = "{service-principal-password}"

# Create a new Azure AD application
$azureAdApplication = New-AzureRmADApplication `
                        -DisplayName "My Azure Monitor" `
                        -HomePage "https://localhost/azure-monitor" `
                        -IdentifierUris "https://localhost/azure-monitor" `
                        -Password $pwd

# Create a new service principal associated with hello designated application
New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId

# Assign Reader role toohello newly created service principal
New-AzureRmRoleAssignment -RoleDefinitionName Reader `
                          -ServicePrincipalName $azureAdApplication.ApplicationId.Guid

```

tooquery hello Azure 監視應用程式開發介面，hello 用戶端應用程式應該使用先前建立的服務主體 tooauthenticate hello。 下列範例 PowerShell 指令碼的 hello 顯示其中一個方法，使用 hello [Active Directory Authentication Library](../active-directory/active-directory-authentication-libraries.md) (ADAL) toohelp 取得 hello JWT 驗證權杖。 hello JWT 權杖會傳遞做為 HTTP 驗證中的參數要求 toohello Azure 監視 REST API 的一部分。

```PowerShell
$azureAdApplication = Get-AzureRmADApplication -IdentifierUri "https://localhost/azure-monitor"

$subscription = Get-AzureRmSubscription -SubscriptionId $subscriptionId

$clientId = $azureAdApplication.ApplicationId.Guid
$tenantId = $subscription.TenantId
$authUrl = "https://login.microsoftonline.com/${tenantId}"

$AuthContext = [Microsoft.IdentityModel.Clients.ActiveDirectory.AuthenticationContext]$authUrl
$cred = New-Object -TypeName Microsoft.IdentityModel.Clients.ActiveDirectory.ClientCredential -ArgumentList ($clientId, $pwd)

$result = $AuthContext.AcquireToken("https://management.core.windows.net/", $cred)

# Build an array of HTTP header values
$authHeader = @{
'Content-Type'='application/json'
'Accept'='application/json'
'Authorization'=$result.CreateAuthorizationHeader()
}
```

Hello 驗證步驟，安裝程式完成之後，請針對 hello Azure 監視 REST API 可以再執行查詢。 有兩個實用的查詢︰

1. 列出資源的 hello 度量定義
2. 擷取 hello 度量值

## <a name="retrieve-metric-definitions"></a>擷取度量定義
> [!NOTE]
> tooretrieve 度量定義使用 hello Azure 監視 REST API，使用"2016年-03-01"hello API 版本。
>
>

```PowerShell
$apiVersion = "2016-03-01"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/${resourceProviderNamespace}/${resourceType}/${resourceName}/providers/microsoft.insights/metricDefinitions?api-version=${apiVersion}"

Invoke-RestMethod -Uri $request `
                  -Headers $authHeader `
                  -Method Get `
                  -Verbose
```
Azure 邏輯應用程式中，hello 度量定義會出現類似 toohello 下列螢幕擷取畫面：

![替代「度量定義回應的 JSON 檢視。」](./media/monitoring-rest-api-walkthrough/available_metric_definitions_logic_app_json_response_clean.png)

如需詳細資訊，請參閱 hello[清單 hello Azure 監視 REST API 中的資源的度量定義](https://msdn.microsoft.com/library/azure/mt743621.aspx)文件。

## <a name="retrieve-metric-values"></a>擷取度量值
一旦稱為 hello 可用的度量定義，就是然後可能 tooretrieve hello 相關的度量值。 使用 hello 度量名稱 'value' (不 hello 'localizedValue') 的任何篩選的要求 （例如，擷取 hello 'CpuTime' 和 '要求' 度量資料點為單位）。 如果未指定篩選，則會傳回 hello 預設公制。

> [!NOTE]
> tooretrieve 度量值使用 hello Azure 監視 REST API，使用"2016年-06-01"hello API 版本。
>
>

**方法**：GET

**要求 URI**：https://management.azure.com/subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/*{resource-provider-namespace}*/*{resource-type}*/*{resource-name}*/providers/microsoft.insights/metrics?$filter=*{filter}*&api-version=*{apiVersion}*

例如，tooretrieve hello RunsSucceeded 度量資料點針對指定的時間範圍內的 hello 和 1 小時，hello 要求的時間粒紋會，如下所示：

```PowerShell
$apiVersion = "2016-06-01"
$filter = "(name.value eq 'RunsSucceeded') and aggregationType eq 'Total' and startTime eq 2016-09-23 and endTime eq 2016-09-24 and timeGrain eq duration'PT1H'"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/${resourceProviderNamespace}/${resourceType}/${resourceName}/providers/microsoft.insights/metrics?`$filter=${filter}&api-version=${apiVersion}"
(Invoke-RestMethod -Uri $request `
                   -Headers $authHeader `
                   -Method Get `
                   -Verbose).Value | ConvertTo-Json
```

hello 結果會出現下列螢幕擷取畫面類似 toohello 範例：

![替代「顯示平均回應時間度量值的 JSON 回應」](./media/monitoring-rest-api-walkthrough/available_metrics_logic_app_json_response.png)

tooretrieve 多個資料或彙總點、 新增 hello 度量定義名稱和彙總類型 toohello 篩選條件，hello 下列範例所示：

```PowerShell
$apiVersion = "2016-06-01"
$filter = "(name.value eq 'ActionsCompleted' or name.value eq 'RunsSucceeded') and (aggregationType eq 'Total' or aggregationType eq 'Average') and startTime eq 2016-09-23T13:30:00Z and endTime eq 2016-09-23T14:30:00Z and timeGrain eq duration'PT1M'"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/${resourceProviderNamespace}/${resourceType}/${resourceName}/providers/microsoft.insights/metrics?`$filter=${filter}&api-version=${apiVersion}"
(Invoke-RestMethod -Uri $request `
                   -Headers $authHeader `
                   -Method Get `
                   -Verbose).Value | ConvertTo-Json
```

### <a name="use-armclient"></a>使用 ARMClient
替代的 toousing PowerShell （如上所示），是 toouse [ARMClient](https://github.com/projectkudu/ARMClient) Windows 電腦上。 ARMClient hello Azure AD 驗證 （和產生的 JWT 權杖） 會自動處理。 hello 下列步驟將概略說明擷取衡量標準資料使用 ARMClient:

1. 安裝 [Chocolatey](https://chocolatey.org/) 和 [ARMClient](https://github.com/projectkudu/ARMClient)。
2. 在終端機視窗中，輸入 armclient.exe login 。 這會提示您 toolog tooAzure 中。
3. 輸入 *armclient GET [your_resource_id]/providers/microsoft.insights/metricdefinitions?api-version=2016-03-01*
4. 輸入 *armclient GET [your_resource_id]/providers/microsoft.insights/metrics?api-version=2016-06-01*

!["Hello Azure Monitoring REST API 與使用 ARMClient toowork"alt](./media/monitoring-rest-api-walkthrough/armclient_metricdefinitions.png)

## <a name="retrieve-hello-resource-id"></a>擷取資源識別碼 hello
使用 REST API hello 真的有助於 toounderstand hello 可用的度量定義、 資料粒度和相關聯的值。 使用 hello 時，該資訊是很有幫助[Azure 管理程式庫](https://msdn.microsoft.com/library/azure/mt417623.aspx)。

Hello 資源識別碼 toouse hello 前面程式碼，是 hello 完整路徑 toohello 所需的 Azure 資源。 例如，Azure Web 應用程式針對 tooquery，hello 資源識別碼將會是：

<bpt id="p1">*</bpt>/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{site-name}/<ept id="p1">*</ept>

hello 下列清單包含一些不同的 Azure 資源的資源識別碼格式的範例：

* **IoT 中樞** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Devices/IotHubs/*{iot-hub-name}*
* **SQL 彈性集區** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Sql/servers/*{pool-db}*/elasticpools/*{sql-pool-name}*
* **SQL Database (v12)** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Sql/servers/*{server-name}*/databases/*{database-name}*
* **服務匯流排** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.ServiceBus/*{namespace}*/*{servicebus-name}*
* **VM 擴展集** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Compute/virtualMachineScaleSets/*{vm-name}*
* **VM** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Compute/virtualMachines/*{vm-name}*
* **事件中樞** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.EventHub/namespaces/*{eventhub-namespace}*

有替代方法 tooretrieving hello 資源識別碼，包括使用 Azure 資源總管 中，檢視所需的 hello 資源 hello Azure 入口網站中和透過 PowerShell 或 hello Azure CLI。

### <a name="azure-resource-explorer"></a>Azure 資源總管
toofind hello 的資源 ID 所需的資源，幫助的其中一個方法為 toouse hello [Azure 資源總管](https://resources.azure.com)工具。 瀏覽 toohello 所需的資源，並接著了解所示，如同下列螢幕擷取畫面的 hello 的 hello 識別碼：

![替代「Azure 資源總管」](./media/monitoring-rest-api-walkthrough/azure_resource_explorer.png)

### <a name="azure-portal"></a>Azure 入口網站
也可以從 hello Azure 入口網站取得 hello 資源識別碼。 因此，toodo 瀏覽 toohello 所需的資源，，然後選取 屬性。 hello 資源 ID 會顯示 hello 屬性刀鋒視窗中，如 hello 下列螢幕擷取畫面所示：

![Alt 「 資源識別碼 hello hello Azure 入口網站中的屬性刀鋒視窗中顯示 」](./media/monitoring-rest-api-walkthrough/resourceid_azure_portal.png)

### <a name="azure-powershell"></a>Azure PowerShell
可以使用 Azure PowerShell 指令程式來擷取 hello 資源識別碼。 例如，tooobtain hello 資源識別碼，Azure Web 應用程式中，執行 hello Get AzureRmWebApp cmdlet，如下列螢幕擷取畫面的 hello 所示：

![替代「透過 PowerShell 取得的資源識別碼」](./media/monitoring-rest-api-walkthrough/resourceid_powershell.png)

### <a name="azure-cli"></a>Azure CLI
tooretrieve hello 使用 Azure CLI hello 的資源 ID、 執行 hello azure webapp 顯示 命令，並指定 hello '-json' 選項，如下列螢幕擷取畫面的 hello 中所示：

![替代「透過 PowerShell 取得的資源識別碼」](./media/monitoring-rest-api-walkthrough/resourceid_azurecli.png)

## <a name="retrieve-activity-log-data"></a>擷取活動記錄檔資料
在加法 tooworking 度量定義與相關聯的值，它也是可能 tooretrieve 其他有趣 insights tooAzure 相關的資源。 例如，很可能 tooquery[活動記錄檔](https://msdn.microsoft.com/library/azure/dn931934.aspx)資料。 hello 下列範例將示範如何使用 hello Azure 監視 REST API tooquery 活動記錄檔資料特定的日期範圍內的 Azure 訂用帳戶：

```PowerShell
$apiVersion = "2014-04-01"
$filter = "eventTimestamp ge '2016-09-23' and eventTimestamp le '2016-09-24'and eventChannels eq 'Admin, Operation'"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/providers/microsoft.insights/eventtypes/management/values?api-version=${apiVersion}&`$filter=${filter}"
(Invoke-RestMethod -Uri $request `
                   -Headers $authHeader `
                   -Method Get `
                   -Verbose).Value | ConvertTo-Json
```

## <a name="next-steps"></a>後續步驟
* 檢閱 hello[監視概觀](monitoring-overview.md)。
* 檢視 hello[支援的 Azure 監視的度量](monitoring-supported-metrics.md)。
* 檢閱 hello [Microsoft Azure 監視 REST API 參考](https://msdn.microsoft.com/library/azure/dn931943.aspx)。
* 檢閱 hello [Azure 管理程式庫](https://msdn.microsoft.com/library/azure/mt417623.aspx)。
