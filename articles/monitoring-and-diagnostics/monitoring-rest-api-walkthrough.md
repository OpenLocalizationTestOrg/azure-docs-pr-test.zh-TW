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
# <a name="azure-monitoring-rest-api-walkthrough"></a><span data-ttu-id="0b096-103">Azure 監視 REST API 逐步解說</span><span class="sxs-lookup"><span data-stu-id="0b096-103">Azure Monitoring REST API Walkthrough</span></span>
<span data-ttu-id="0b096-104">本文章將示範如何讓您的程式碼可以使用 hello tooperform 驗證[Microsoft Azure 監視 REST API 參考](https://msdn.microsoft.com/library/azure/dn931943.aspx)。</span><span class="sxs-lookup"><span data-stu-id="0b096-104">This article shows you how tooperform authentication so your code can use hello [Microsoft Azure Monitor REST API Reference](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span>         

<span data-ttu-id="0b096-105">hello Azure 監視應用程式開發介面可讓您可能 tooprogrammatically 擷取 hello 可用預設度量定義 （例如 CPU 時間、 要求 」 等標準的 hello 類型），資料粒度，度量值。</span><span class="sxs-lookup"><span data-stu-id="0b096-105">hello Azure Monitor API makes it possible tooprogrammatically retrieve hello available default metric definitions (hello type of metric such as CPU Time, Requests, etc.), granularity, and metric values.</span></span> <span data-ttu-id="0b096-106">擷取之後，hello 資料可以儲存在個別的資料存放區，例如 Azure SQL Database、 Azure Cosmos DB 或 Azure Data Lake 中。</span><span class="sxs-lookup"><span data-stu-id="0b096-106">Once retrieved, hello data can be saved in a separate data store such as Azure SQL Database, Azure Cosmos DB, or Azure Data Lake.</span></span> <span data-ttu-id="0b096-107">其他分析可視需要從該處執行。</span><span class="sxs-lookup"><span data-stu-id="0b096-107">From there additional analysis can be performed as needed.</span></span>

<span data-ttu-id="0b096-108">除了使用不同的度量資料點，如本文所示，hello 監視應用程式開發介面可讓可能 toolist 警示規則、 檢視活動記錄檔，以及執行更多。</span><span class="sxs-lookup"><span data-stu-id="0b096-108">Besides working with various metric data points, as this article demonstrates, hello Monitor API makes it possible toolist alert rules, view activity logs, and much more.</span></span> <span data-ttu-id="0b096-109">如需可用作業的完整清單，請參閱 hello [Microsoft Azure 監視 REST API 參考](https://msdn.microsoft.com/library/azure/dn931943.aspx)。</span><span class="sxs-lookup"><span data-stu-id="0b096-109">For a full list of available operations, see hello [Microsoft Azure Monitor REST API Reference](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span>

## <a name="authenticating-azure-monitor-requests"></a><span data-ttu-id="0b096-110">驗證 Azure 監視器要求</span><span class="sxs-lookup"><span data-stu-id="0b096-110">Authenticating Azure Monitor Requests</span></span>
<span data-ttu-id="0b096-111">hello 第一個步驟是 tooauthenticate hello 要求。</span><span class="sxs-lookup"><span data-stu-id="0b096-111">hello first step is tooauthenticate hello request.</span></span>

<span data-ttu-id="0b096-112">針對 hello Azure 監視應用程式開發介面使用 hello Azure 資源管理員驗證模型所執行的所有 hello 工作。</span><span class="sxs-lookup"><span data-stu-id="0b096-112">All hello tasks executed against hello Azure Monitor API use hello Azure Resource Manager authentication model.</span></span> <span data-ttu-id="0b096-113">因此，所有要求都必須使用 Azure Active Directory (Azure AD) 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="0b096-113">Therefore, all requests must be authenticated with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="0b096-114">一種方法 tooauthenticate hello 用戶端應用程式是 toocreate Azure AD 服務主體，和擷取 hello 驗證 (JWT) 權杖。</span><span class="sxs-lookup"><span data-stu-id="0b096-114">One approach tooauthenticate hello client application is toocreate an Azure AD service principal and retrieve hello authentication (JWT) token.</span></span> <span data-ttu-id="0b096-115">hello 下列範例指令碼將示範如何建立 Azure AD 服務主體，透過 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="0b096-115">hello following sample script demonstrates creating an Azure AD service principal via PowerShell.</span></span> <span data-ttu-id="0b096-116">更詳細的逐步解說，請參閱 toohello 文件，在[服務主體 tooaccess 資源使用 Azure PowerShell toocreate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-password)。</span><span class="sxs-lookup"><span data-stu-id="0b096-116">For a more detailed walk-through, refer toohello documentation on [using Azure PowerShell toocreate a service principal tooaccess resources](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-password).</span></span> <span data-ttu-id="0b096-117">此外，也可以太[建立服務主體 hello Azure 入口網站透過](../azure-resource-manager/resource-group-create-service-principal-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="0b096-117">It is also possible too[create a service principal via hello Azure portal](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span>

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

<span data-ttu-id="0b096-118">tooquery hello Azure 監視應用程式開發介面，hello 用戶端應用程式應該使用先前建立的服務主體 tooauthenticate hello。</span><span class="sxs-lookup"><span data-stu-id="0b096-118">tooquery hello Azure Monitor API, hello client application should use hello previously created service principal tooauthenticate.</span></span> <span data-ttu-id="0b096-119">下列範例 PowerShell 指令碼的 hello 顯示其中一個方法，使用 hello [Active Directory Authentication Library](../active-directory/active-directory-authentication-libraries.md) (ADAL) toohelp 取得 hello JWT 驗證權杖。</span><span class="sxs-lookup"><span data-stu-id="0b096-119">hello following example PowerShell script shows one approach, using hello [Active Directory Authentication Library](../active-directory/active-directory-authentication-libraries.md) (ADAL) toohelp get hello JWT authentication token.</span></span> <span data-ttu-id="0b096-120">hello JWT 權杖會傳遞做為 HTTP 驗證中的參數要求 toohello Azure 監視 REST API 的一部分。</span><span class="sxs-lookup"><span data-stu-id="0b096-120">hello JWT token is passed as part of an HTTP Authorization parameter in requests toohello Azure Monitor REST API.</span></span>

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

<span data-ttu-id="0b096-121">Hello 驗證步驟，安裝程式完成之後，請針對 hello Azure 監視 REST API 可以再執行查詢。</span><span class="sxs-lookup"><span data-stu-id="0b096-121">Once hello authentication setup step is complete, queries can then be executed against hello Azure Monitor REST API.</span></span> <span data-ttu-id="0b096-122">有兩個實用的查詢︰</span><span class="sxs-lookup"><span data-stu-id="0b096-122">There are two helpful queries:</span></span>

1. <span data-ttu-id="0b096-123">列出資源的 hello 度量定義</span><span class="sxs-lookup"><span data-stu-id="0b096-123">List hello metric definitions for a resource</span></span>
2. <span data-ttu-id="0b096-124">擷取 hello 度量值</span><span class="sxs-lookup"><span data-stu-id="0b096-124">Retrieve hello metric values</span></span>

## <a name="retrieve-metric-definitions"></a><span data-ttu-id="0b096-125">擷取度量定義</span><span class="sxs-lookup"><span data-stu-id="0b096-125">Retrieve Metric Definitions</span></span>
> [!NOTE]
> <span data-ttu-id="0b096-126">tooretrieve 度量定義使用 hello Azure 監視 REST API，使用"2016年-03-01"hello API 版本。</span><span class="sxs-lookup"><span data-stu-id="0b096-126">tooretrieve metric definitions using hello Azure Monitor REST API, use "2016-03-01" as hello API version.</span></span>
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
<span data-ttu-id="0b096-127">Azure 邏輯應用程式中，hello 度量定義會出現類似 toohello 下列螢幕擷取畫面：</span><span class="sxs-lookup"><span data-stu-id="0b096-127">For an Azure Logic App, hello metric definitions would appear similar toohello following screenshot:</span></span>

![替代「度量定義回應的 JSON 檢視。」](./media/monitoring-rest-api-walkthrough/available_metric_definitions_logic_app_json_response_clean.png)

<span data-ttu-id="0b096-129">如需詳細資訊，請參閱 hello[清單 hello Azure 監視 REST API 中的資源的度量定義](https://msdn.microsoft.com/library/azure/mt743621.aspx)文件。</span><span class="sxs-lookup"><span data-stu-id="0b096-129">For more information, see hello [List hello metric definitions for a resource in Azure Monitor REST API](https://msdn.microsoft.com/library/azure/mt743621.aspx) documentation.</span></span>

## <a name="retrieve-metric-values"></a><span data-ttu-id="0b096-130">擷取度量值</span><span class="sxs-lookup"><span data-stu-id="0b096-130">Retrieve Metric Values</span></span>
<span data-ttu-id="0b096-131">一旦稱為 hello 可用的度量定義，就是然後可能 tooretrieve hello 相關的度量值。</span><span class="sxs-lookup"><span data-stu-id="0b096-131">Once hello available metric definitions are known, it is then possible tooretrieve hello related metric values.</span></span> <span data-ttu-id="0b096-132">使用 hello 度量名稱 'value' (不 hello 'localizedValue') 的任何篩選的要求 （例如，擷取 hello 'CpuTime' 和 '要求' 度量資料點為單位）。</span><span class="sxs-lookup"><span data-stu-id="0b096-132">Use hello metric’s name ‘value’ (not hello ‘localizedValue’) for any filtering requests (for example, retrieve hello ‘CpuTime’ and ‘Requests’ metric data points).</span></span> <span data-ttu-id="0b096-133">如果未指定篩選，則會傳回 hello 預設公制。</span><span class="sxs-lookup"><span data-stu-id="0b096-133">If no filters are specified, hello default metric is returned.</span></span>

> [!NOTE]
> <span data-ttu-id="0b096-134">tooretrieve 度量值使用 hello Azure 監視 REST API，使用"2016年-06-01"hello API 版本。</span><span class="sxs-lookup"><span data-stu-id="0b096-134">tooretrieve metric values using hello Azure Monitor REST API, use "2016-06-01" as hello API version.</span></span>
>
>

<span data-ttu-id="0b096-135">**方法**：GET</span><span class="sxs-lookup"><span data-stu-id="0b096-135">**Method**: GET</span></span>

<span data-ttu-id="0b096-136">**要求 URI**：https://management.azure.com/subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/*{resource-provider-namespace}*/*{resource-type}*/*{resource-name}*/providers/microsoft.insights/metrics?$filter=*{filter}*&api-version=*{apiVersion}*</span><span class="sxs-lookup"><span data-stu-id="0b096-136">**Request URI**: https://management.azure.com/subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/*{resource-provider-namespace}*/*{resource-type}*/*{resource-name}*/providers/microsoft.insights/metrics?$filter=*{filter}*&api-version=*{apiVersion}*</span></span>

<span data-ttu-id="0b096-137">例如，tooretrieve hello RunsSucceeded 度量資料點針對指定的時間範圍內的 hello 和 1 小時，hello 要求的時間粒紋會，如下所示：</span><span class="sxs-lookup"><span data-stu-id="0b096-137">For example, tooretrieve hello RunsSucceeded metric data points for hello given time range and for a time grain of 1 hour, hello request would be as follows:</span></span>

```PowerShell
$apiVersion = "2016-06-01"
$filter = "(name.value eq 'RunsSucceeded') and aggregationType eq 'Total' and startTime eq 2016-09-23 and endTime eq 2016-09-24 and timeGrain eq duration'PT1H'"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/${resourceProviderNamespace}/${resourceType}/${resourceName}/providers/microsoft.insights/metrics?`$filter=${filter}&api-version=${apiVersion}"
(Invoke-RestMethod -Uri $request `
                   -Headers $authHeader `
                   -Method Get `
                   -Verbose).Value | ConvertTo-Json
```

<span data-ttu-id="0b096-138">hello 結果會出現下列螢幕擷取畫面類似 toohello 範例：</span><span class="sxs-lookup"><span data-stu-id="0b096-138">hello result would appear similar toohello example following screenshot:</span></span>

![替代「顯示平均回應時間度量值的 JSON 回應」](./media/monitoring-rest-api-walkthrough/available_metrics_logic_app_json_response.png)

<span data-ttu-id="0b096-140">tooretrieve 多個資料或彙總點、 新增 hello 度量定義名稱和彙總類型 toohello 篩選條件，hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="0b096-140">tooretrieve multiple data or aggregation points, add hello metric definition names and aggregation types toohello filter, as seen in hello following example:</span></span>

```PowerShell
$apiVersion = "2016-06-01"
$filter = "(name.value eq 'ActionsCompleted' or name.value eq 'RunsSucceeded') and (aggregationType eq 'Total' or aggregationType eq 'Average') and startTime eq 2016-09-23T13:30:00Z and endTime eq 2016-09-23T14:30:00Z and timeGrain eq duration'PT1M'"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/${resourceProviderNamespace}/${resourceType}/${resourceName}/providers/microsoft.insights/metrics?`$filter=${filter}&api-version=${apiVersion}"
(Invoke-RestMethod -Uri $request `
                   -Headers $authHeader `
                   -Method Get `
                   -Verbose).Value | ConvertTo-Json
```

### <a name="use-armclient"></a><span data-ttu-id="0b096-141">使用 ARMClient</span><span class="sxs-lookup"><span data-stu-id="0b096-141">Use ARMClient</span></span>
<span data-ttu-id="0b096-142">替代的 toousing PowerShell （如上所示），是 toouse [ARMClient](https://github.com/projectkudu/ARMClient) Windows 電腦上。</span><span class="sxs-lookup"><span data-stu-id="0b096-142">An alternative toousing PowerShell (as shown above), is toouse [ARMClient](https://github.com/projectkudu/ARMClient) on your Windows machine.</span></span> <span data-ttu-id="0b096-143">ARMClient hello Azure AD 驗證 （和產生的 JWT 權杖） 會自動處理。</span><span class="sxs-lookup"><span data-stu-id="0b096-143">ARMClient handles hello Azure AD authentication (and resulting JWT token) automatically.</span></span> <span data-ttu-id="0b096-144">hello 下列步驟將概略說明擷取衡量標準資料使用 ARMClient:</span><span class="sxs-lookup"><span data-stu-id="0b096-144">hello following steps outline use of ARMClient for retrieving metric data:</span></span>

1. <span data-ttu-id="0b096-145">安裝 [Chocolatey](https://chocolatey.org/) 和 [ARMClient](https://github.com/projectkudu/ARMClient)。</span><span class="sxs-lookup"><span data-stu-id="0b096-145">Install [Chocolatey](https://chocolatey.org/) and [ARMClient](https://github.com/projectkudu/ARMClient).</span></span>
2. <span data-ttu-id="0b096-146">在終端機視窗中，輸入 armclient.exe login 。</span><span class="sxs-lookup"><span data-stu-id="0b096-146">In a terminal window, type *armclient.exe login*.</span></span> <span data-ttu-id="0b096-147">這會提示您 toolog tooAzure 中。</span><span class="sxs-lookup"><span data-stu-id="0b096-147">This prompts you toolog in tooAzure.</span></span>
3. <span data-ttu-id="0b096-148">輸入 *armclient GET [your_resource_id]/providers/microsoft.insights/metricdefinitions?api-version=2016-03-01*</span><span class="sxs-lookup"><span data-stu-id="0b096-148">Type *armclient GET [your_resource_id]/providers/microsoft.insights/metricdefinitions?api-version=2016-03-01*</span></span>
4. <span data-ttu-id="0b096-149">輸入 *armclient GET [your_resource_id]/providers/microsoft.insights/metrics?api-version=2016-06-01*</span><span class="sxs-lookup"><span data-stu-id="0b096-149">Type *armclient GET [your_resource_id]/providers/microsoft.insights/metrics?api-version=2016-06-01*</span></span>

!["Hello Azure Monitoring REST API 與使用 ARMClient toowork"alt](./media/monitoring-rest-api-walkthrough/armclient_metricdefinitions.png)

## <a name="retrieve-hello-resource-id"></a><span data-ttu-id="0b096-151">擷取資源識別碼 hello</span><span class="sxs-lookup"><span data-stu-id="0b096-151">Retrieve hello Resource ID</span></span>
<span data-ttu-id="0b096-152">使用 REST API hello 真的有助於 toounderstand hello 可用的度量定義、 資料粒度和相關聯的值。</span><span class="sxs-lookup"><span data-stu-id="0b096-152">Using hello REST API can really help toounderstand hello available metric definitions, granularity, and related values.</span></span> <span data-ttu-id="0b096-153">使用 hello 時，該資訊是很有幫助[Azure 管理程式庫](https://msdn.microsoft.com/library/azure/mt417623.aspx)。</span><span class="sxs-lookup"><span data-stu-id="0b096-153">That information is helpful when using hello [Azure Management Library](https://msdn.microsoft.com/library/azure/mt417623.aspx).</span></span>

<span data-ttu-id="0b096-154">Hello 資源識別碼 toouse hello 前面程式碼，是 hello 完整路徑 toohello 所需的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="0b096-154">For hello preceding code, hello resource ID toouse is hello full path toohello desired Azure resource.</span></span> <span data-ttu-id="0b096-155">例如，Azure Web 應用程式針對 tooquery，hello 資源識別碼將會是：</span><span class="sxs-lookup"><span data-stu-id="0b096-155">For example, tooquery against an Azure Web App, hello resource ID would be:</span></span>

<bpt id="p1">*</bpt>/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{site-name}/<ept id="p1">*</ept>

<span data-ttu-id="0b096-157">hello 下列清單包含一些不同的 Azure 資源的資源識別碼格式的範例：</span><span class="sxs-lookup"><span data-stu-id="0b096-157">hello following list contains a few examples of resource ID formats for various Azure resources:</span></span>

* <span data-ttu-id="0b096-158">**IoT 中樞** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Devices/IotHubs/*{iot-hub-name}*</span><span class="sxs-lookup"><span data-stu-id="0b096-158">**IoT Hub** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Devices/IotHubs/*{iot-hub-name}*</span></span>
* <span data-ttu-id="0b096-159">**SQL 彈性集區** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Sql/servers/*{pool-db}*/elasticpools/*{sql-pool-name}*</span><span class="sxs-lookup"><span data-stu-id="0b096-159">**Elastic SQL Pool** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Sql/servers/*{pool-db}*/elasticpools/*{sql-pool-name}*</span></span>
* <span data-ttu-id="0b096-160">**SQL Database (v12)** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Sql/servers/*{server-name}*/databases/*{database-name}*</span><span class="sxs-lookup"><span data-stu-id="0b096-160">**SQL Database (v12)** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Sql/servers/*{server-name}*/databases/*{database-name}*</span></span>
* <span data-ttu-id="0b096-161">**服務匯流排** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.ServiceBus/*{namespace}*/*{servicebus-name}*</span><span class="sxs-lookup"><span data-stu-id="0b096-161">**Service Bus** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.ServiceBus/*{namespace}*/*{servicebus-name}*</span></span>
* <span data-ttu-id="0b096-162">**VM 擴展集** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Compute/virtualMachineScaleSets/*{vm-name}*</span><span class="sxs-lookup"><span data-stu-id="0b096-162">**VM Scale Sets** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Compute/virtualMachineScaleSets/*{vm-name}*</span></span>
* <span data-ttu-id="0b096-163">**VM** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Compute/virtualMachines/*{vm-name}*</span><span class="sxs-lookup"><span data-stu-id="0b096-163">**VMs** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Compute/virtualMachines/*{vm-name}*</span></span>
* <span data-ttu-id="0b096-164">**事件中樞** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.EventHub/namespaces/*{eventhub-namespace}*</span><span class="sxs-lookup"><span data-stu-id="0b096-164">**Event Hubs** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.EventHub/namespaces/*{eventhub-namespace}*</span></span>

<span data-ttu-id="0b096-165">有替代方法 tooretrieving hello 資源識別碼，包括使用 Azure 資源總管 中，檢視所需的 hello 資源 hello Azure 入口網站中和透過 PowerShell 或 hello Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="0b096-165">There are alternative approaches tooretrieving hello resource ID, including using Azure Resource Explorer, viewing hello desired resource in hello Azure portal, and via PowerShell or hello Azure CLI.</span></span>

### <a name="azure-resource-explorer"></a><span data-ttu-id="0b096-166">Azure 資源總管</span><span class="sxs-lookup"><span data-stu-id="0b096-166">Azure Resource Explorer</span></span>
<span data-ttu-id="0b096-167">toofind hello 的資源 ID 所需的資源，幫助的其中一個方法為 toouse hello [Azure 資源總管](https://resources.azure.com)工具。</span><span class="sxs-lookup"><span data-stu-id="0b096-167">toofind hello resource ID for a desired resource, one helpful approach is toouse hello [Azure Resource Explorer](https://resources.azure.com) tool.</span></span> <span data-ttu-id="0b096-168">瀏覽 toohello 所需的資源，並接著了解所示，如同下列螢幕擷取畫面的 hello 的 hello 識別碼：</span><span class="sxs-lookup"><span data-stu-id="0b096-168">Navigate toohello desired resource and then look at hello ID shown, as in hello following screenshot:</span></span>

![替代「Azure 資源總管」](./media/monitoring-rest-api-walkthrough/azure_resource_explorer.png)

### <a name="azure-portal"></a><span data-ttu-id="0b096-170">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="0b096-170">Azure portal</span></span>
<span data-ttu-id="0b096-171">也可以從 hello Azure 入口網站取得 hello 資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="0b096-171">hello resource ID can also be obtained from hello Azure portal.</span></span> <span data-ttu-id="0b096-172">因此，toodo 瀏覽 toohello 所需的資源，，然後選取 屬性。</span><span class="sxs-lookup"><span data-stu-id="0b096-172">toodo so, navigate toohello desired resource and then select Properties.</span></span> <span data-ttu-id="0b096-173">hello 資源 ID 會顯示 hello 屬性刀鋒視窗中，如 hello 下列螢幕擷取畫面所示：</span><span class="sxs-lookup"><span data-stu-id="0b096-173">hello Resource ID is displayed in hello Properties blade, as seen in hello following screenshot:</span></span>

![Alt 「 資源識別碼 hello hello Azure 入口網站中的屬性刀鋒視窗中顯示 」](./media/monitoring-rest-api-walkthrough/resourceid_azure_portal.png)

### <a name="azure-powershell"></a><span data-ttu-id="0b096-175">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="0b096-175">Azure PowerShell</span></span>
<span data-ttu-id="0b096-176">可以使用 Azure PowerShell 指令程式來擷取 hello 資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="0b096-176">hello resource ID can be retrieved using Azure PowerShell cmdlets as well.</span></span> <span data-ttu-id="0b096-177">例如，tooobtain hello 資源識別碼，Azure Web 應用程式中，執行 hello Get AzureRmWebApp cmdlet，如下列螢幕擷取畫面的 hello 所示：</span><span class="sxs-lookup"><span data-stu-id="0b096-177">For example, tooobtain hello resource ID for an Azure Web App, execute hello Get-AzureRmWebApp cmdlet, as in hello following screenshot:</span></span>

![替代「透過 PowerShell 取得的資源識別碼」](./media/monitoring-rest-api-walkthrough/resourceid_powershell.png)

### <a name="azure-cli"></a><span data-ttu-id="0b096-179">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="0b096-179">Azure CLI</span></span>
<span data-ttu-id="0b096-180">tooretrieve hello 使用 Azure CLI hello 的資源 ID、 執行 hello azure webapp 顯示 命令，並指定 hello '-json' 選項，如下列螢幕擷取畫面的 hello 中所示：</span><span class="sxs-lookup"><span data-stu-id="0b096-180">tooretrieve hello resource ID using hello Azure CLI, execute hello 'azure webapp show' command, specifying hello '--json' option, as shown in hello following screenshot:</span></span>

![替代「透過 PowerShell 取得的資源識別碼」](./media/monitoring-rest-api-walkthrough/resourceid_azurecli.png)

## <a name="retrieve-activity-log-data"></a><span data-ttu-id="0b096-182">擷取活動記錄檔資料</span><span class="sxs-lookup"><span data-stu-id="0b096-182">Retrieve Activity Log Data</span></span>
<span data-ttu-id="0b096-183">在加法 tooworking 度量定義與相關聯的值，它也是可能 tooretrieve 其他有趣 insights tooAzure 相關的資源。</span><span class="sxs-lookup"><span data-stu-id="0b096-183">In addition tooworking with metric definitions and related values, it is also possible tooretrieve additional interesting insights related tooAzure resources.</span></span> <span data-ttu-id="0b096-184">例如，很可能 tooquery[活動記錄檔](https://msdn.microsoft.com/library/azure/dn931934.aspx)資料。</span><span class="sxs-lookup"><span data-stu-id="0b096-184">As an example, it is possible tooquery [activity log](https://msdn.microsoft.com/library/azure/dn931934.aspx) data.</span></span> <span data-ttu-id="0b096-185">hello 下列範例將示範如何使用 hello Azure 監視 REST API tooquery 活動記錄檔資料特定的日期範圍內的 Azure 訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="0b096-185">hello following sample demonstrates using hello Azure Monitor REST API tooquery activity log data within a specific date range for an Azure subscription:</span></span>

```PowerShell
$apiVersion = "2014-04-01"
$filter = "eventTimestamp ge '2016-09-23' and eventTimestamp le '2016-09-24'and eventChannels eq 'Admin, Operation'"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/providers/microsoft.insights/eventtypes/management/values?api-version=${apiVersion}&`$filter=${filter}"
(Invoke-RestMethod -Uri $request `
                   -Headers $authHeader `
                   -Method Get `
                   -Verbose).Value | ConvertTo-Json
```

## <a name="next-steps"></a><span data-ttu-id="0b096-186">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0b096-186">Next steps</span></span>
* <span data-ttu-id="0b096-187">檢閱 hello[監視概觀](monitoring-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="0b096-187">Review hello [Overview of Monitoring](monitoring-overview.md).</span></span>
* <span data-ttu-id="0b096-188">檢視 hello[支援的 Azure 監視的度量](monitoring-supported-metrics.md)。</span><span class="sxs-lookup"><span data-stu-id="0b096-188">View hello [Supported metrics with Azure Monitor](monitoring-supported-metrics.md).</span></span>
* <span data-ttu-id="0b096-189">檢閱 hello [Microsoft Azure 監視 REST API 參考](https://msdn.microsoft.com/library/azure/dn931943.aspx)。</span><span class="sxs-lookup"><span data-stu-id="0b096-189">Review hello [Microsoft Azure Monitor REST API Reference](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span>
* <span data-ttu-id="0b096-190">檢閱 hello [Azure 管理程式庫](https://msdn.microsoft.com/library/azure/mt417623.aspx)。</span><span class="sxs-lookup"><span data-stu-id="0b096-190">Review hello [Azure Management Library](https://msdn.microsoft.com/library/azure/mt417623.aspx).</span></span>
