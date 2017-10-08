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
# <a name="back-end-health-diagnostic-logs-and-metrics-for-application-gateway"></a><span data-ttu-id="b139e-103">應用程式閘道的後端健康情況、診斷記錄和計量</span><span class="sxs-lookup"><span data-stu-id="b139e-103">Back-end health, diagnostic logs, and metrics for Application Gateway</span></span>

<span data-ttu-id="b139e-104">藉由使用 Azure 應用程式閘道，您可以監視下列方式 hello 中的資源：</span><span class="sxs-lookup"><span data-stu-id="b139e-104">By using Azure Application Gateway, you can monitor resources in hello following ways:</span></span>

* <span data-ttu-id="b139e-105">[後端健全狀況](#back-end-health)： 應用程式閘道提供 hello 功能 toomonitor hello 伺服器的健全狀況 hello hello 中透過 hello Azure 入口網站，以及透過 PowerShell 的後端集區。</span><span class="sxs-lookup"><span data-stu-id="b139e-105">[Back-end health](#back-end-health): Application Gateway provides hello capability toomonitor hello health of hello servers in hello back-end pools through hello Azure portal and through PowerShell.</span></span> <span data-ttu-id="b139e-106">您也可以尋找 hello hello 透過 hello 效能診斷記錄檔的後端集區的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="b139e-106">You can also find hello health of hello back-end pools through hello performance diagnostic logs.</span></span>

* <span data-ttu-id="b139e-107">[記錄檔](#diagnostic-logs)： 記錄檔可供存取的效能，以及其他資料 toobe 儲存，或從監視所需的資源耗用。</span><span class="sxs-lookup"><span data-stu-id="b139e-107">[Logs](#diagnostic-logs): Logs allow for performance, access, and other data toobe saved or consumed from a resource for monitoring purposes.</span></span>

* <span data-ttu-id="b139e-108">[計量](#metrics)：應用程式閘道目前有一個計量。</span><span class="sxs-lookup"><span data-stu-id="b139e-108">[Metrics](#metrics): Application Gateway currently has one metric.</span></span> <span data-ttu-id="b139e-109">此標準會測量 hello 的 hello 應用程式閘道，以位元組為單位，每秒的輸送量。</span><span class="sxs-lookup"><span data-stu-id="b139e-109">This metric measures hello throughput of hello application gateway in bytes per second.</span></span>

## <a name="back-end-health"></a><span data-ttu-id="b139e-110">後端健康情況</span><span class="sxs-lookup"><span data-stu-id="b139e-110">Back-end health</span></span>

<span data-ttu-id="b139e-111">應用程式閘道提供 hello 功能 toomonitor hello 健全狀況的 hello 透過 hello 入口網站、 PowerShell 和 hello 命令列介面 (CLI) 的後端集區的個別成員。</span><span class="sxs-lookup"><span data-stu-id="b139e-111">Application Gateway provides hello capability toomonitor hello health of individual members of hello back-end pools through hello portal, PowerShell, and hello command-line interface (CLI).</span></span> <span data-ttu-id="b139e-112">您也可以尋找彙總的健全狀況摘要透過 hello 效能診斷記錄檔的後端集區。</span><span class="sxs-lookup"><span data-stu-id="b139e-112">You can also find an aggregated health summary of back-end pools through hello performance diagnostic logs.</span></span> 

<span data-ttu-id="b139e-113">hello 後端健全狀況報表會反映 hello hello 應用程式閘道健全狀況探查 toohello 後端執行個體輸出。</span><span class="sxs-lookup"><span data-stu-id="b139e-113">hello back-end health report reflects hello output of hello Application Gateway health probe toohello back-end instances.</span></span> <span data-ttu-id="b139e-114">當探查成功回 hello 結束可以接收流量，則會視為狀況良好。</span><span class="sxs-lookup"><span data-stu-id="b139e-114">When probing is successful and hello back end can receive traffic, it's considered healthy.</span></span> <span data-ttu-id="b139e-115">否則，視為狀況不良。</span><span class="sxs-lookup"><span data-stu-id="b139e-115">Otherwise, it's considered unhealthy.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b139e-116">如果沒有在應用程式閘道子網路上的網路安全性群組 (NSG)，開啟 輸入流量的 hello 應用程式閘道子網路上的連接埠範圍 65503 65534。</span><span class="sxs-lookup"><span data-stu-id="b139e-116">If there is a network security group (NSG) on an Application Gateway subnet, open port ranges 65503-65534 on hello Application Gateway subnet for inbound traffic.</span></span> <span data-ttu-id="b139e-117">這些連接埠不需要 hello 後端健全狀況 API toowork。</span><span class="sxs-lookup"><span data-stu-id="b139e-117">These ports are required for hello back-end health API toowork.</span></span>


### <a name="view-back-end-health-through-hello-portal"></a><span data-ttu-id="b139e-118">檢視透過 hello 入口網站的後端健全狀況</span><span class="sxs-lookup"><span data-stu-id="b139e-118">View back-end health through hello portal</span></span>

<span data-ttu-id="b139e-119">Hello 入口網站中，會自動提供後端健全狀況。</span><span class="sxs-lookup"><span data-stu-id="b139e-119">In hello portal, back-end health is provided automatically.</span></span> <span data-ttu-id="b139e-120">在現有的應用程式閘道中，選取 [監視]  >  [後端健康情況]。</span><span class="sxs-lookup"><span data-stu-id="b139e-120">In an existing application gateway, select **Monitoring** > **Backend health**.</span></span> 

<span data-ttu-id="b139e-121">Hello 後端集區中的每個成員會列在此頁面中，（其是否 NIC，IP 或 FQDN）。</span><span class="sxs-lookup"><span data-stu-id="b139e-121">Each member in hello back-end pool is listed on this page (whether it's a NIC, IP, or FQDN).</span></span> <span data-ttu-id="b139e-122">後端集區名稱、連接埠、後端 HTTP 設定名稱和健康情況均會顯示。</span><span class="sxs-lookup"><span data-stu-id="b139e-122">Back-end pool name, port, back-end HTTP settings name, and health status are shown.</span></span> <span data-ttu-id="b139e-123">健康情況的有效值為「狀況良好」、「狀況不良」和「未知」。</span><span class="sxs-lookup"><span data-stu-id="b139e-123">Valid values for health status are **Healthy**, **Unhealthy**, and **Unknown**.</span></span>

> [!NOTE]
> <span data-ttu-id="b139e-124">如果您看到的後端健全狀況狀態的**未知**，請確定該存取 toohello 後端不會遭到 NSG 規則、 使用者定義的路由 (UDR) 或自訂 DNS hello 虛擬網路中的。</span><span class="sxs-lookup"><span data-stu-id="b139e-124">If you see a back-end health status of **Unknown**, ensure that access toohello back end is not blocked by an NSG rule, a user-defined route (UDR), or a custom DNS in hello virtual network.</span></span>

![後端健康情況][10]

### <a name="view-back-end-health-through-powershell"></a><span data-ttu-id="b139e-126">透過 PowerShell 檢視後端健康情況</span><span class="sxs-lookup"><span data-stu-id="b139e-126">View back-end health through PowerShell</span></span>

<span data-ttu-id="b139e-127">hello 下列 PowerShell 程式碼會示範如何使用 tooview 後端健全狀況 hello `Get-AzureRmApplicationGatewayBackendHealth` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="b139e-127">hello following PowerShell code shows how tooview back-end health by using hello `Get-AzureRmApplicationGatewayBackendHealth` cmdlet:</span></span>

```powershell
Get-AzureRmApplicationGatewayBackendHealth -Name ApplicationGateway1 -ResourceGroupName Contoso
```

### <a name="view-back-end-health-through-azure-cli-20"></a><span data-ttu-id="b139e-128">透過 Azure CLI 2.0 檢視後端健康情況</span><span class="sxs-lookup"><span data-stu-id="b139e-128">View back-end health through Azure CLI 2.0</span></span>

```azurecli
az network application-gateway show-backend-health --resource-group AdatumAppGatewayRG --name AdatumAppGateway
```

### <a name="results"></a><span data-ttu-id="b139e-129">結果</span><span class="sxs-lookup"><span data-stu-id="b139e-129">Results</span></span>

<span data-ttu-id="b139e-130">下列程式碼片段的 hello 顯示 hello 回應的範例：</span><span class="sxs-lookup"><span data-stu-id="b139e-130">hello following snippet shows an example of hello response:</span></span>

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

## <span data-ttu-id="b139e-131"><a name="diagnostic-logging"></a>診斷記錄</span><span class="sxs-lookup"><span data-stu-id="b139e-131"><a name="diagnostic-logging"></a>Diagnostic logs</span></span>

<span data-ttu-id="b139e-132">您可以在 Azure toomanage 中使用不同類型的記錄檔和疑難排解應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="b139e-132">You can use different types of logs in Azure toomanage and troubleshoot application gateways.</span></span> <span data-ttu-id="b139e-133">您可以透過 hello 入口網站存取這些記錄檔部份。</span><span class="sxs-lookup"><span data-stu-id="b139e-133">You can access some of these logs through hello portal.</span></span> <span data-ttu-id="b139e-134">可以從 Azure Blob 儲存體擷取所有記錄，並且在不同的工具中進行檢視 (例如 [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md)、Excel、PowerBI)。</span><span class="sxs-lookup"><span data-stu-id="b139e-134">All logs can be extracted from Azure Blob storage and viewed in different tools, such as [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md), Excel, and Power BI.</span></span> <span data-ttu-id="b139e-135">您可以深入了解 hello 來自不同類型的記錄檔清單後面的 hello:</span><span class="sxs-lookup"><span data-stu-id="b139e-135">You can learn more about hello different types of logs from hello following list:</span></span>

* <span data-ttu-id="b139e-136">**活動記錄檔**： 您可以使用[Azure 活動記錄檔](../monitoring-and-diagnostics/insights-debugging-with-events.md)（以前稱為操作記錄檔和稽核記錄檔） tooview 所有作業都提交 tooyour Azure 訂用帳戶，以及它們的狀態。</span><span class="sxs-lookup"><span data-stu-id="b139e-136">**Activity log**: You can use [Azure activity logs](../monitoring-and-diagnostics/insights-debugging-with-events.md) (formerly known as operational logs and audit logs) tooview all operations that are submitted tooyour Azure subscription, and their status.</span></span> <span data-ttu-id="b139e-137">活動記錄檔項目會根據預設，收集和 hello Azure 入口網站中進行檢視。</span><span class="sxs-lookup"><span data-stu-id="b139e-137">Activity log entries are collected by default, and you can view them in hello Azure portal.</span></span>
* <span data-ttu-id="b139e-138">**存取記錄檔**： 您可以使用此記錄 tooview 應用程式閘道存取模式和分析的重要資訊，包括 hello 呼叫者的 IP、 要求的 URL、 回應延遲，傳回碼和位元組和縮小。每隔 300 秒會收集一次存取記錄。</span><span class="sxs-lookup"><span data-stu-id="b139e-138">**Access log**: You can use this log tooview Application Gateway access patterns and analyze important information, including hello caller's IP, requested URL, response latency, return code, and bytes in and out. An access log is collected every 300 seconds.</span></span> <span data-ttu-id="b139e-139">此記錄檔包含每個應用程式閘道執行個體的一筆記錄。</span><span class="sxs-lookup"><span data-stu-id="b139e-139">This log contains one record per instance of Application Gateway.</span></span> <span data-ttu-id="b139e-140">hello 應用程式閘道執行個體可以 hello instanceId 屬性的識別。</span><span class="sxs-lookup"><span data-stu-id="b139e-140">hello Application Gateway instance can be identified by hello instanceId property.</span></span>
* <span data-ttu-id="b139e-141">**效能記錄**： 您可以使用此應用程式閘道器執行個體的執行方式的記錄檔 tooview。</span><span class="sxs-lookup"><span data-stu-id="b139e-141">**Performance log**: You can use this log tooview how Application Gateway instances are performing.</span></span> <span data-ttu-id="b139e-142">此記錄會擷取每個執行個體的效能資訊，包括提供的要求總數、輸送量 (以位元組為單位)、提供的總要求數、失敗的要求計數、狀況良好和狀況不良的後端執行個體計數。</span><span class="sxs-lookup"><span data-stu-id="b139e-142">This log captures performance information for each instance, including total requests served, throughput in bytes, total requests served, failed request count, and healthy and unhealthy back-end instance count.</span></span> <span data-ttu-id="b139e-143">每隔 60 秒會收集一次效能記錄。</span><span class="sxs-lookup"><span data-stu-id="b139e-143">A performance log is collected every 60 seconds.</span></span>
* <span data-ttu-id="b139e-144">**防火牆記錄**： 您可以使用透過偵測或防止應用程式閘道以 hello web 應用程式的防火牆設定的模式會記錄這個記錄 tooview hello 的要求。</span><span class="sxs-lookup"><span data-stu-id="b139e-144">**Firewall log**: You can use this log tooview hello requests that are logged through either detection or prevention mode of an application gateway that is configured with hello web application firewall.</span></span>

> [!NOTE]
> <span data-ttu-id="b139e-145">記錄是僅供部署在 hello Azure Resource Manager 部署模型中的資源。</span><span class="sxs-lookup"><span data-stu-id="b139e-145">Logs are available only for resources deployed in hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="b139e-146">您無法使用記錄檔 hello 傳統部署模型中的資源。</span><span class="sxs-lookup"><span data-stu-id="b139e-146">You cannot use logs for resources in hello classic deployment model.</span></span> <span data-ttu-id="b139e-147">進一步了解 hello 兩個模型，請參閱 hello[了解資源管理員部署和傳統部署](../azure-resource-manager/resource-manager-deployment-model.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="b139e-147">For a better understanding of hello two models, see hello [Understanding Resource Manager deployment and classic deployment](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>

<span data-ttu-id="b139e-148">您有三個選項可用來排序您的記錄：</span><span class="sxs-lookup"><span data-stu-id="b139e-148">You have three options for storing your logs:</span></span>

* <span data-ttu-id="b139e-149">**儲存體帳戶**：如果記錄會儲存一段較長的持續期間，並在需要時加以檢閱，則最好針對記錄使用儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="b139e-149">**Storage account**: Storage accounts are best used for logs when logs are stored for a longer duration and reviewed when needed.</span></span>
* <span data-ttu-id="b139e-150">**事件中心**： 事件中心是絕佳的選項與其他安全性資訊整合與事件管理 (SEIM) 工具 tooget 警示，您的資源。</span><span class="sxs-lookup"><span data-stu-id="b139e-150">**Event hubs**: Event hubs are a great option for integrating with other security information and event management (SEIM) tools tooget alerts on your resources.</span></span>
* <span data-ttu-id="b139e-151">**Log Analytics**：Log Analytics 最適合用來進行應用程式的一般即時監視，或查看趨勢。</span><span class="sxs-lookup"><span data-stu-id="b139e-151">**Log Analytics**: Log Analytics is best used for general real-time monitoring of your application or looking at trends.</span></span>

### <a name="enable-logging-through-powershell"></a><span data-ttu-id="b139e-152">透過 PowerShell 啟用記錄功能</span><span class="sxs-lookup"><span data-stu-id="b139e-152">Enable logging through PowerShell</span></span>

<span data-ttu-id="b139e-153">每個 Resource Manager 資源都會自動啟用活動記錄功能。</span><span class="sxs-lookup"><span data-stu-id="b139e-153">Activity logging is automatically enabled for every Resource Manager resource.</span></span> <span data-ttu-id="b139e-154">您必須啟用存取和效能記錄 toostart 收集 hello 資料可透過這些記錄檔。</span><span class="sxs-lookup"><span data-stu-id="b139e-154">You must enable access and performance logging toostart collecting hello data available through those logs.</span></span> <span data-ttu-id="b139e-155">tooenable 記錄、 使用 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="b139e-155">tooenable logging, use hello following steps:</span></span>

1. <span data-ttu-id="b139e-156">請注意 hello 記錄資料的儲存位置的儲存體帳戶的資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="b139e-156">Note your storage account's resource ID, where hello log data is stored.</span></span> <span data-ttu-id="b139e-157">此值為 hello 格式： /subscriptions/\<subscriptionId\>/resourceGroups/\<資源群組名稱\>/providers/Microsoft.Storage/storageAccounts/\<的儲存體帳戶名稱\>.</span><span class="sxs-lookup"><span data-stu-id="b139e-157">This value is of hello form: /subscriptions/\<subscriptionId\>/resourceGroups/\<resource group name\>/providers/Microsoft.Storage/storageAccounts/\<storage account name\>.</span></span> <span data-ttu-id="b139e-158">您可以使用訂用帳戶中的所有儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="b139e-158">You can use any storage account in your subscription.</span></span> <span data-ttu-id="b139e-159">您可以使用 Azure 入口網站 toofind hello 這項資訊。</span><span class="sxs-lookup"><span data-stu-id="b139e-159">You can use hello Azure portal toofind this information.</span></span>

    ![入口網站：儲存體帳戶的資源識別碼](./media/application-gateway-diagnostics/diagnostics1.png)

2. <span data-ttu-id="b139e-161">請記下您的應用程式閘道的資源識別碼 (將為其啟用記錄功能)。</span><span class="sxs-lookup"><span data-stu-id="b139e-161">Note your application gateway's resource ID for which logging is enabled.</span></span> <span data-ttu-id="b139e-162">此值為 hello 格式： /subscriptions/\<subscriptionId\>/resourceGroups/\<資源群組名稱\>/providers/Microsoft.Network/applicationGateways/\<應用程式閘道名稱\>。</span><span class="sxs-lookup"><span data-stu-id="b139e-162">This value is of hello form: /subscriptions/\<subscriptionId\>/resourceGroups/\<resource group name\>/providers/Microsoft.Network/applicationGateways/\<application gateway name\>.</span></span> <span data-ttu-id="b139e-163">您可以使用 hello 入口 toofind 這項資訊。</span><span class="sxs-lookup"><span data-stu-id="b139e-163">You can use hello portal toofind this information.</span></span>

    ![入口網站：應用程式閘道的資源識別碼](./media/application-gateway-diagnostics/diagnostics2.png)

3. <span data-ttu-id="b139e-165">使用下列 PowerShell cmdlet 的 hello 啟用診斷記錄：</span><span class="sxs-lookup"><span data-stu-id="b139e-165">Enable diagnostic logging by using hello following PowerShell cmdlet:</span></span>

    ```powershell
    Set-AzureRmDiagnosticSetting  -ResourceId /subscriptions/<subscriptionId>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name> -StorageAccountId /subscriptions/<subscriptionId>/resourceGroups/<resource group name>/providers/Microsoft.Storage/storageAccounts/<storage account name> -Enabled $true     
    ```
    
> [!TIP] 
><span data-ttu-id="b139e-166">活動記錄檔不需要個別的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="b139e-166">Activity logs do not require a separate storage account.</span></span> <span data-ttu-id="b139e-167">hello 使用儲存體的存取和效能記錄不會產生服務費用。</span><span class="sxs-lookup"><span data-stu-id="b139e-167">hello use of storage for access and performance logging incurs service charges.</span></span>

### <a name="enable-logging-through-hello-azure-portal"></a><span data-ttu-id="b139e-168">啟用記錄 hello 透過 Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="b139e-168">Enable logging through hello Azure portal</span></span>

1. <span data-ttu-id="b139e-169">在 hello Azure 入口網站，尋找您的資源，然後按一下**診斷記錄**。</span><span class="sxs-lookup"><span data-stu-id="b139e-169">In hello Azure portal, find your resource and click **Diagnostic logs**.</span></span>

   <span data-ttu-id="b139e-170">應用程式閘道有三個記錄：</span><span class="sxs-lookup"><span data-stu-id="b139e-170">For Application Gateway, three logs are available:</span></span>

   * <span data-ttu-id="b139e-171">存取記錄檔</span><span class="sxs-lookup"><span data-stu-id="b139e-171">Access log</span></span>
   * <span data-ttu-id="b139e-172">效能記錄檔</span><span class="sxs-lookup"><span data-stu-id="b139e-172">Performance log</span></span>
   * <span data-ttu-id="b139e-173">防火牆記錄檔</span><span class="sxs-lookup"><span data-stu-id="b139e-173">Firewall log</span></span>

2. <span data-ttu-id="b139e-174">toostart 收集資料，按一下**開啟診斷**。</span><span class="sxs-lookup"><span data-stu-id="b139e-174">toostart collecting data, click **Turn on diagnostics**.</span></span>

   ![開啟診斷][1]

3. <span data-ttu-id="b139e-176">hello**診斷設定**刀鋒視窗中提供的 hello hello 設定診斷記錄檔。</span><span class="sxs-lookup"><span data-stu-id="b139e-176">hello **Diagnostics settings** blade provides hello settings for hello diagnostic logs.</span></span> <span data-ttu-id="b139e-177">在此範例中，記錄分析儲存 hello 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="b139e-177">In this example, Log Analytics stores hello logs.</span></span> <span data-ttu-id="b139e-178">按一下**設定**下**記錄分析**tooconfigure 您的工作區。</span><span class="sxs-lookup"><span data-stu-id="b139e-178">Click **Configure** under **Log Analytics** tooconfigure your workspace.</span></span> <span data-ttu-id="b139e-179">您也可以使用事件中樞與儲存體帳戶 toosave hello 診斷記錄。</span><span class="sxs-lookup"><span data-stu-id="b139e-179">You can also use event hubs and a storage account toosave hello diagnostic logs.</span></span>

   ![啟動 hello 組態程序][2]

4. <span data-ttu-id="b139e-181">選擇現有的 Operations Management Suite (OMS) 工作區或建立新的。</span><span class="sxs-lookup"><span data-stu-id="b139e-181">Choose an existing Operations Management Suite (OMS) workspace or create a new one.</span></span> <span data-ttu-id="b139e-182">這個範例使用現有工作區。</span><span class="sxs-lookup"><span data-stu-id="b139e-182">This example uses an existing one.</span></span>

   ![OMS 工作區的選項][3]

5. <span data-ttu-id="b139e-184">確認 hello 設定然後按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="b139e-184">Confirm hello settings and click **Save**.</span></span>

   ![診斷設定刀鋒視窗與選項][4]

### <a name="activity-log"></a><span data-ttu-id="b139e-186">活動記錄檔</span><span class="sxs-lookup"><span data-stu-id="b139e-186">Activity log</span></span>

<span data-ttu-id="b139e-187">根據預設，azure 會產生 hello 活動記錄檔。</span><span class="sxs-lookup"><span data-stu-id="b139e-187">Azure generates hello activity log by default.</span></span> <span data-ttu-id="b139e-188">hello 記錄檔會保留 90 天，hello Azure 事件記錄檔存放區中。</span><span class="sxs-lookup"><span data-stu-id="b139e-188">hello logs are preserved for 90 days in hello Azure event logs store.</span></span> <span data-ttu-id="b139e-189">深入了解這些記錄檔讀取 hello[檢視事件和活動記錄檔](../monitoring-and-diagnostics/insights-debugging-with-events.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="b139e-189">Learn more about these logs by reading hello [View events and activity log](../monitoring-and-diagnostics/insights-debugging-with-events.md) article.</span></span>

### <a name="access-log"></a><span data-ttu-id="b139e-190">存取記錄檔</span><span class="sxs-lookup"><span data-stu-id="b139e-190">Access log</span></span>

<span data-ttu-id="b139e-191">只有當您已將它啟用每個應用程式閘道執行個體上，hello 先前步驟中所述，會產生 hello 存取記錄。</span><span class="sxs-lookup"><span data-stu-id="b139e-191">hello access log is generated only if you've enabled it on each Application Gateway instance, as detailed in hello preceding steps.</span></span> <span data-ttu-id="b139e-192">hello 資料會儲存在您指定當您啟用 hello 記錄 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="b139e-192">hello data is stored in hello storage account that you specified when you enabled hello logging.</span></span> <span data-ttu-id="b139e-193">每次存取的應用程式閘道會記錄 JSON 格式 hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="b139e-193">Each access of Application Gateway is logged in JSON format, as shown in hello following example:</span></span>


|<span data-ttu-id="b139e-194">值</span><span class="sxs-lookup"><span data-stu-id="b139e-194">Value</span></span>  |<span data-ttu-id="b139e-195">說明</span><span class="sxs-lookup"><span data-stu-id="b139e-195">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="b139e-196">instanceId</span><span class="sxs-lookup"><span data-stu-id="b139e-196">instanceId</span></span>     | <span data-ttu-id="b139e-197">應用程式閘道執行個體提供的 hello 要求。</span><span class="sxs-lookup"><span data-stu-id="b139e-197">Application Gateway instance that served hello request.</span></span>        |
|<span data-ttu-id="b139e-198">clientIP</span><span class="sxs-lookup"><span data-stu-id="b139e-198">clientIP</span></span>     | <span data-ttu-id="b139e-199">Hello 要求的原始 IP。</span><span class="sxs-lookup"><span data-stu-id="b139e-199">Originating IP for hello request.</span></span>        |
|<span data-ttu-id="b139e-200">clientPort</span><span class="sxs-lookup"><span data-stu-id="b139e-200">clientPort</span></span>     | <span data-ttu-id="b139e-201">Hello 要求的原始連接埠。</span><span class="sxs-lookup"><span data-stu-id="b139e-201">Originating port for hello request.</span></span>       |
|<span data-ttu-id="b139e-202">httpMethod</span><span class="sxs-lookup"><span data-stu-id="b139e-202">httpMethod</span></span>     | <span data-ttu-id="b139e-203">Hello 要求所使用的 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="b139e-203">HTTP method used by hello request.</span></span>       |
|<span data-ttu-id="b139e-204">requestUri</span><span class="sxs-lookup"><span data-stu-id="b139e-204">requestUri</span></span>     | <span data-ttu-id="b139e-205">Hello 接收到要求的 URI。</span><span class="sxs-lookup"><span data-stu-id="b139e-205">URI of hello received request.</span></span>        |
|<span data-ttu-id="b139e-206">RequestQuery</span><span class="sxs-lookup"><span data-stu-id="b139e-206">RequestQuery</span></span>     | <span data-ttu-id="b139e-207">**伺服器路由**： 已傳送嗨要求的後端集區執行個體。</span><span class="sxs-lookup"><span data-stu-id="b139e-207">**Server-Routed**: Back-end pool instance that was sent hello request.</span></span> </br> <span data-ttu-id="b139e-208">**X AzureApplicationGateway-記錄識別碼**: hello 要求使用的相互關聯識別碼。</span><span class="sxs-lookup"><span data-stu-id="b139e-208">**X-AzureApplicationGateway-LOG-ID**: Correlation ID used for hello request.</span></span> <span data-ttu-id="b139e-209">它可以是使用的 tootroubleshoot hello 後端伺服器上的流量問題。</span><span class="sxs-lookup"><span data-stu-id="b139e-209">It can be used tootroubleshoot traffic issues on hello back-end servers.</span></span> </br><span data-ttu-id="b139e-210">**伺服器狀態**： 應用程式閘道收到 hello 後端的 HTTP 回應碼。</span><span class="sxs-lookup"><span data-stu-id="b139e-210">**SERVER-STATUS**: HTTP response code that Application Gateway received from hello back end.</span></span>       |
|<span data-ttu-id="b139e-211">UserAgent</span><span class="sxs-lookup"><span data-stu-id="b139e-211">UserAgent</span></span>     | <span data-ttu-id="b139e-212">Hello HTTP 要求標頭中的使用者代理程式。</span><span class="sxs-lookup"><span data-stu-id="b139e-212">User agent from hello HTTP request header.</span></span>        |
|<span data-ttu-id="b139e-213">httpStatus</span><span class="sxs-lookup"><span data-stu-id="b139e-213">httpStatus</span></span>     | <span data-ttu-id="b139e-214">從應用程式閘道 toohello 用戶端傳回 HTTP 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="b139e-214">HTTP status code returned toohello client from Application Gateway.</span></span>       |
|<span data-ttu-id="b139e-215">httpVersion</span><span class="sxs-lookup"><span data-stu-id="b139e-215">httpVersion</span></span>     | <span data-ttu-id="b139e-216">Hello 要求的 HTTP 版本。</span><span class="sxs-lookup"><span data-stu-id="b139e-216">HTTP version of hello request.</span></span>        |
|<span data-ttu-id="b139e-217">receivedBytes</span><span class="sxs-lookup"><span data-stu-id="b139e-217">receivedBytes</span></span>     | <span data-ttu-id="b139e-218">接收的封包大小，單位為位元組。</span><span class="sxs-lookup"><span data-stu-id="b139e-218">Size of packet received, in bytes.</span></span>        |
|<span data-ttu-id="b139e-219">sentBytes</span><span class="sxs-lookup"><span data-stu-id="b139e-219">sentBytes</span></span>| <span data-ttu-id="b139e-220">傳送的封包大小，單位為位元組。</span><span class="sxs-lookup"><span data-stu-id="b139e-220">Size of packet sent, in bytes.</span></span>|
|<span data-ttu-id="b139e-221">timeTaken</span><span class="sxs-lookup"><span data-stu-id="b139e-221">timeTaken</span></span>| <span data-ttu-id="b139e-222">處理要求 toobe 並傳送其回應 toobe 的時間 （以毫秒為單位） 的長度。</span><span class="sxs-lookup"><span data-stu-id="b139e-222">Length of time (in milliseconds) that it takes for a request toobe processed and its response toobe sent.</span></span> <span data-ttu-id="b139e-223">這被計算為從應用程式閘道當收到 hello 回應 hello 當傳送作業完成 HTTP 要求 toohello 時間第一個位元組的 hello 時間 hello 間隔。</span><span class="sxs-lookup"><span data-stu-id="b139e-223">This is calculated as hello interval from hello time when Application Gateway receives hello first byte of an HTTP request toohello time when hello response send operation finishes.</span></span> <span data-ttu-id="b139e-224">請務必通常 hello 花費的時間欄位的 toonote 包含 hello hello 要求和回應封包在出差 hello 網路上的時間。</span><span class="sxs-lookup"><span data-stu-id="b139e-224">It's important toonote that hello Time-Taken field usually includes hello time that hello request and response packets are traveling over hello network.</span></span> |
|<span data-ttu-id="b139e-225">sslEnabled</span><span class="sxs-lookup"><span data-stu-id="b139e-225">sslEnabled</span></span>| <span data-ttu-id="b139e-226">是否通訊 toohello 後端集區會使用 SSL。</span><span class="sxs-lookup"><span data-stu-id="b139e-226">Whether communication toohello back-end pools used SSL.</span></span> <span data-ttu-id="b139e-227">有效值為 on 和 off。</span><span class="sxs-lookup"><span data-stu-id="b139e-227">Valid values are on and off.</span></span>|
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

### <a name="performance-log"></a><span data-ttu-id="b139e-228">效能記錄檔</span><span class="sxs-lookup"><span data-stu-id="b139e-228">Performance log</span></span>

<span data-ttu-id="b139e-229">只有當 hello 先前步驟中有詳細說明每個應用程式閘道執行個體上啟用它，就會產生 hello 效能記錄。</span><span class="sxs-lookup"><span data-stu-id="b139e-229">hello performance log is generated only if you have enabled it on each Application Gateway instance, as detailed in hello preceding steps.</span></span> <span data-ttu-id="b139e-230">hello 資料會儲存在您指定當您啟用 hello 記錄 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="b139e-230">hello data is stored in hello storage account that you specified when you enabled hello logging.</span></span> <span data-ttu-id="b139e-231">hello 效能記錄資料會產生每隔 1 分鐘。</span><span class="sxs-lookup"><span data-stu-id="b139e-231">hello performance log data is generated in 1-minute intervals.</span></span> <span data-ttu-id="b139e-232">會記錄下列資料的 hello:</span><span class="sxs-lookup"><span data-stu-id="b139e-232">hello following data is logged:</span></span>


|<span data-ttu-id="b139e-233">值</span><span class="sxs-lookup"><span data-stu-id="b139e-233">Value</span></span>  |<span data-ttu-id="b139e-234">說明</span><span class="sxs-lookup"><span data-stu-id="b139e-234">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="b139e-235">instanceId</span><span class="sxs-lookup"><span data-stu-id="b139e-235">instanceId</span></span>     |  <span data-ttu-id="b139e-236">將產生此應用程式閘道執行個體的效能資料。</span><span class="sxs-lookup"><span data-stu-id="b139e-236">Application Gateway instance for which performance data is being generated.</span></span> <span data-ttu-id="b139e-237">應用程式閘道若有多個執行個體，則是一個執行個體一行資料。</span><span class="sxs-lookup"><span data-stu-id="b139e-237">For a multiple-instance application gateway, there is one row per instance.</span></span>        |
|<span data-ttu-id="b139e-238">healthyHostCount</span><span class="sxs-lookup"><span data-stu-id="b139e-238">healthyHostCount</span></span>     | <span data-ttu-id="b139e-239">狀況良好 hello 後端集區中的主機數目。</span><span class="sxs-lookup"><span data-stu-id="b139e-239">Number of healthy hosts in hello back-end pool.</span></span>        |
|<span data-ttu-id="b139e-240">unHealthyHostCount</span><span class="sxs-lookup"><span data-stu-id="b139e-240">unHealthyHostCount</span></span>     | <span data-ttu-id="b139e-241">狀況不良 hello 後端集區中的主機數目。</span><span class="sxs-lookup"><span data-stu-id="b139e-241">Number of unhealthy hosts in hello back-end pool.</span></span>        |
|<span data-ttu-id="b139e-242">requestCount</span><span class="sxs-lookup"><span data-stu-id="b139e-242">requestCount</span></span>     | <span data-ttu-id="b139e-243">處理的要求數目。</span><span class="sxs-lookup"><span data-stu-id="b139e-243">Number of requests served.</span></span>        |
|<span data-ttu-id="b139e-244">latency</span><span class="sxs-lookup"><span data-stu-id="b139e-244">latency</span></span> | <span data-ttu-id="b139e-245">Hello 執行個體 toohello 來自要求的延遲時間 （以毫秒為單位） 後端服務 hello 要求。</span><span class="sxs-lookup"><span data-stu-id="b139e-245">Latency (in milliseconds) of requests from hello instance toohello back end that serves hello requests.</span></span> |
|<span data-ttu-id="b139e-246">failedRequestCount</span><span class="sxs-lookup"><span data-stu-id="b139e-246">failedRequestCount</span></span>| <span data-ttu-id="b139e-247">失敗的要求數目。</span><span class="sxs-lookup"><span data-stu-id="b139e-247">Number of failed requests.</span></span>|
|<span data-ttu-id="b139e-248">throughput</span><span class="sxs-lookup"><span data-stu-id="b139e-248">throughput</span></span>| <span data-ttu-id="b139e-249">由於 hello 最後一個記錄，以每秒位元組為單位的平均輸送量。</span><span class="sxs-lookup"><span data-stu-id="b139e-249">Average throughput since hello last log, measured in bytes per second.</span></span>|

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
> <span data-ttu-id="b139e-250">延遲會計算從 hello hello hello HTTP 要求第一個位元組收到的 toohello 什麼時候是當傳送 hello 最後一個位元組的 hello HTTP 回應的時間。</span><span class="sxs-lookup"><span data-stu-id="b139e-250">Latency is calculated from hello time when hello first byte of hello HTTP request is received toohello time when hello last byte of hello HTTP response is sent.</span></span> <span data-ttu-id="b139e-251">它的 hello 總和 hello 應用程式閘道處理時間，加上 hello 回網路成本 toohello 結束，再加上 hello hello 後端採用 tooprocess hello 要求的時間。</span><span class="sxs-lookup"><span data-stu-id="b139e-251">It's hello sum of hello Application Gateway processing time plus hello network cost toohello back end, plus hello time that hello back end takes tooprocess hello request.</span></span>

### <a name="firewall-log"></a><span data-ttu-id="b139e-252">防火牆記錄檔</span><span class="sxs-lookup"><span data-stu-id="b139e-252">Firewall log</span></span>

<span data-ttu-id="b139e-253">只有當您已啟用每個應用程式閘道，hello 先前步驟中所述，會產生 hello 防火牆記錄。</span><span class="sxs-lookup"><span data-stu-id="b139e-253">hello firewall log is generated only if you have enabled it for each application gateway, as detailed in hello preceding steps.</span></span> <span data-ttu-id="b139e-254">此記錄檔也會需要 hello web 應用程式防火牆應用程式閘道上設定。</span><span class="sxs-lookup"><span data-stu-id="b139e-254">This log also requires that hello web application firewall is configured on an application gateway.</span></span> <span data-ttu-id="b139e-255">hello 資料會儲存在您指定當您啟用 hello 記錄 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="b139e-255">hello data is stored in hello storage account that you specified when you enabled hello logging.</span></span> <span data-ttu-id="b139e-256">會記錄下列資料的 hello:</span><span class="sxs-lookup"><span data-stu-id="b139e-256">hello following data is logged:</span></span>


|<span data-ttu-id="b139e-257">值</span><span class="sxs-lookup"><span data-stu-id="b139e-257">Value</span></span>  |<span data-ttu-id="b139e-258">說明</span><span class="sxs-lookup"><span data-stu-id="b139e-258">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="b139e-259">instanceId</span><span class="sxs-lookup"><span data-stu-id="b139e-259">instanceId</span></span>     | <span data-ttu-id="b139e-260">將產生此應用程式閘道執行個體的防火牆資料。</span><span class="sxs-lookup"><span data-stu-id="b139e-260">Application Gateway instance for which firewall data is being generated.</span></span> <span data-ttu-id="b139e-261">應用程式閘道若有多個執行個體，則是一個執行個體一行資料。</span><span class="sxs-lookup"><span data-stu-id="b139e-261">For a multiple-instance application gateway, there is one row per instance.</span></span>         |
|<span data-ttu-id="b139e-262">clientIp</span><span class="sxs-lookup"><span data-stu-id="b139e-262">clientIp</span></span>     |   <span data-ttu-id="b139e-263">Hello 要求的原始 IP。</span><span class="sxs-lookup"><span data-stu-id="b139e-263">Originating IP for hello request.</span></span>      |
|<span data-ttu-id="b139e-264">clientPort</span><span class="sxs-lookup"><span data-stu-id="b139e-264">clientPort</span></span>     |  <span data-ttu-id="b139e-265">Hello 要求的原始連接埠。</span><span class="sxs-lookup"><span data-stu-id="b139e-265">Originating port for hello request.</span></span>       |
|<span data-ttu-id="b139e-266">requestUri</span><span class="sxs-lookup"><span data-stu-id="b139e-266">requestUri</span></span>     | <span data-ttu-id="b139e-267">Hello 接收到要求的 URL。</span><span class="sxs-lookup"><span data-stu-id="b139e-267">URL of hello received request.</span></span>       |
|<span data-ttu-id="b139e-268">ruleSetType</span><span class="sxs-lookup"><span data-stu-id="b139e-268">ruleSetType</span></span>     | <span data-ttu-id="b139e-269">規則集類型。</span><span class="sxs-lookup"><span data-stu-id="b139e-269">Rule set type.</span></span> <span data-ttu-id="b139e-270">hello 可用的值是 OWASP。</span><span class="sxs-lookup"><span data-stu-id="b139e-270">hello available value is OWASP.</span></span>        |
|<span data-ttu-id="b139e-271">ruleSetVersion</span><span class="sxs-lookup"><span data-stu-id="b139e-271">ruleSetVersion</span></span>     | <span data-ttu-id="b139e-272">規則集版本。</span><span class="sxs-lookup"><span data-stu-id="b139e-272">Rule set version used.</span></span> <span data-ttu-id="b139e-273">可用值為 2.2.9 和 3.0。</span><span class="sxs-lookup"><span data-stu-id="b139e-273">Available values are 2.2.9 and 3.0.</span></span>     |
|<span data-ttu-id="b139e-274">ruleId</span><span class="sxs-lookup"><span data-stu-id="b139e-274">ruleId</span></span>     | <span data-ttu-id="b139e-275">規則識別碼 hello 觸發事件。</span><span class="sxs-lookup"><span data-stu-id="b139e-275">Rule ID of hello triggering event.</span></span>        |
|<span data-ttu-id="b139e-276">Message</span><span class="sxs-lookup"><span data-stu-id="b139e-276">message</span></span>     | <span data-ttu-id="b139e-277">使用者易記的 hello 觸發事件的詳細訊息。</span><span class="sxs-lookup"><span data-stu-id="b139e-277">User-friendly message for hello triggering event.</span></span> <span data-ttu-id="b139e-278">Hello 詳細資料 區段中提供更多詳細資料。</span><span class="sxs-lookup"><span data-stu-id="b139e-278">More details are provided in hello details section.</span></span>        |
|<span data-ttu-id="b139e-279">動作</span><span class="sxs-lookup"><span data-stu-id="b139e-279">action</span></span>     |  <span data-ttu-id="b139e-280">Hello 要求上採取的動作。</span><span class="sxs-lookup"><span data-stu-id="b139e-280">Action taken on hello request.</span></span> <span data-ttu-id="b139e-281">可用的值為 Blocked 和 Allowed。</span><span class="sxs-lookup"><span data-stu-id="b139e-281">Available values are Blocked and Allowed.</span></span>      |
|<span data-ttu-id="b139e-282">site</span><span class="sxs-lookup"><span data-stu-id="b139e-282">site</span></span>     | <span data-ttu-id="b139e-283">記錄檔產生哪些 hello 站台。</span><span class="sxs-lookup"><span data-stu-id="b139e-283">Site for which hello log was generated.</span></span> <span data-ttu-id="b139e-284">目前只列出 Global，因為規則為全域。</span><span class="sxs-lookup"><span data-stu-id="b139e-284">Currently, only Global is listed because rules are global.</span></span>|
|<span data-ttu-id="b139e-285">詳細資料</span><span class="sxs-lookup"><span data-stu-id="b139e-285">details</span></span>     | <span data-ttu-id="b139e-286">Hello 觸發事件的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="b139e-286">Details of hello triggering event.</span></span>        |
|<span data-ttu-id="b139e-287">details.message</span><span class="sxs-lookup"><span data-stu-id="b139e-287">details.message</span></span>     | <span data-ttu-id="b139e-288">Hello 規則的描述。</span><span class="sxs-lookup"><span data-stu-id="b139e-288">Description of hello rule.</span></span>        |
|<span data-ttu-id="b139e-289">details.data</span><span class="sxs-lookup"><span data-stu-id="b139e-289">details.data</span></span>     | <span data-ttu-id="b139e-290">在要求中發現的特定資料該相符的 hello 規則。</span><span class="sxs-lookup"><span data-stu-id="b139e-290">Specific data found in request that matched hello rule.</span></span>         |
|<span data-ttu-id="b139e-291">details.file</span><span class="sxs-lookup"><span data-stu-id="b139e-291">details.file</span></span>     | <span data-ttu-id="b139e-292">Hello 規則所包含的組態檔。</span><span class="sxs-lookup"><span data-stu-id="b139e-292">Configuration file that contained hello rule.</span></span>        |
|<span data-ttu-id="b139e-293">details.line</span><span class="sxs-lookup"><span data-stu-id="b139e-293">details.line</span></span>     | <span data-ttu-id="b139e-294">Hello 觸發 hello 事件的組態檔中的行號。</span><span class="sxs-lookup"><span data-stu-id="b139e-294">Line number in hello configuration file that triggered hello event.</span></span>       |

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

### <a name="view-and-analyze-hello-activity-log"></a><span data-ttu-id="b139e-295">檢視及分析 hello 活動記錄檔</span><span class="sxs-lookup"><span data-stu-id="b139e-295">View and analyze hello activity log</span></span>

<span data-ttu-id="b139e-296">您可以檢視並分析活動記錄資料使用任何 hello 下列方法：</span><span class="sxs-lookup"><span data-stu-id="b139e-296">You can view and analyze activity log data by using any of hello following methods:</span></span>

* <span data-ttu-id="b139e-297">**Azure tools**： 從 Azure PowerShell，hello Azure CLI，hello Azure REST API，透過 hello 活動記錄檔中擷取資訊或 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="b139e-297">**Azure tools**: Retrieve information from hello activity log through Azure PowerShell, hello Azure CLI, hello Azure REST API, or hello Azure portal.</span></span> <span data-ttu-id="b139e-298">每個方法的逐步指示的詳細 hello[活動作業與資源管理員](../azure-resource-manager/resource-group-audit.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="b139e-298">Step-by-step instructions for each method are detailed in hello [Activity operations with Resource Manager](../azure-resource-manager/resource-group-audit.md) article.</span></span>
* <span data-ttu-id="b139e-299">**Power BI**：如果還沒有 [Power BI](https://powerbi.microsoft.com/pricing) 帳戶，您可以免費試用。</span><span class="sxs-lookup"><span data-stu-id="b139e-299">**Power BI**: If you don't already have a [Power BI](https://powerbi.microsoft.com/pricing) account, you can try it for free.</span></span> <span data-ttu-id="b139e-300">使用 hello [Power BI 的 Azure 活動記錄內容套件](https://powerbi.microsoft.com/en-us/documentation/powerbi-content-pack-azure-audit-logs/)，您可以分析資料與預先設定，您可以使用，或自訂儀表板。</span><span class="sxs-lookup"><span data-stu-id="b139e-300">By using hello [Azure Activity Logs content pack for Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-content-pack-azure-audit-logs/), you can analyze your data with preconfigured dashboards that you can use as is or customize.</span></span>

### <a name="view-and-analyze-hello-access-performance-and-firewall-logs"></a><span data-ttu-id="b139e-301">檢視及分析 hello 存取、 效能及防火牆記錄檔</span><span class="sxs-lookup"><span data-stu-id="b139e-301">View and analyze hello access, performance, and firewall logs</span></span>

<span data-ttu-id="b139e-302">Azure[記錄分析](../log-analytics/log-analytics-azure-networking-analytics.md)可以從 Blob 儲存體帳戶收集 hello 計數器和事件記錄檔。</span><span class="sxs-lookup"><span data-stu-id="b139e-302">Azure [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md) can collect hello counter and event log files from your Blob storage account.</span></span> <span data-ttu-id="b139e-303">它包括視覺效果和強大的搜尋功能 tooanalyze 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="b139e-303">It includes visualizations and powerful search capabilities tooanalyze your logs.</span></span>

<span data-ttu-id="b139e-304">您也可以連接 tooyour 儲存體帳戶，並擷取 hello JSON 記錄項目，以存取和效能記錄檔。</span><span class="sxs-lookup"><span data-stu-id="b139e-304">You can also connect tooyour storage account and retrieve hello JSON log entries for access and performance logs.</span></span> <span data-ttu-id="b139e-305">下載 hello JSON 檔案之後，您可以將它們轉換 tooCSV，並在 Excel、 Power BI 中或任何其他資料視覺效果工具中檢視它們。</span><span class="sxs-lookup"><span data-stu-id="b139e-305">After you download hello JSON files, you can convert them tooCSV and view them in Excel, Power BI, or any other data-visualization tool.</span></span>

> [!TIP]
> <span data-ttu-id="b139e-306">如果您熟悉 Visual Studio 和變更值的常數和變數在 C# 中的基本概念，您可以使用 hello[記錄轉換器工具](https://github.com/Azure-Samples/networking-dotnet-log-converter)可從 GitHub 取得。</span><span class="sxs-lookup"><span data-stu-id="b139e-306">If you are familiar with Visual Studio and basic concepts of changing values for constants and variables in C#, you can use hello [log converter tools](https://github.com/Azure-Samples/networking-dotnet-log-converter) available from GitHub.</span></span>
> 
> 

## <a name="metrics"></a><span data-ttu-id="b139e-307">度量</span><span class="sxs-lookup"><span data-stu-id="b139e-307">Metrics</span></span>

<span data-ttu-id="b139e-308">度量是特定的 Azure 資源，您可以檢視效能計數器 hello 入口網站中的功能。</span><span class="sxs-lookup"><span data-stu-id="b139e-308">Metrics are a feature for certain Azure resources where you can view performance counters in hello portal.</span></span> <span data-ttu-id="b139e-309">目前應用程式閘道只有一個計量。</span><span class="sxs-lookup"><span data-stu-id="b139e-309">For Application Gateway, one metric is available now.</span></span> <span data-ttu-id="b139e-310">此度量是輸送量，以及您可以在 hello 入口網站中看到它。</span><span class="sxs-lookup"><span data-stu-id="b139e-310">This metric is throughput, and you can see it in hello portal.</span></span> <span data-ttu-id="b139e-311">瀏覽 tooan 應用程式閘道並按一下**度量**。</span><span class="sxs-lookup"><span data-stu-id="b139e-311">Browse tooan application gateway and click **Metrics**.</span></span> <span data-ttu-id="b139e-312">tooview hello 值選取輸送量 hello**可用的度量**> 一節。</span><span class="sxs-lookup"><span data-stu-id="b139e-312">tooview hello values, select throughput in hello **Available metrics** section.</span></span> <span data-ttu-id="b139e-313">在下列映像的 hello，您可以看到 hello 篩選器，您可以在不同的時間範圍內使用 toodisplay hello 資料範例。</span><span class="sxs-lookup"><span data-stu-id="b139e-313">In hello following image, you can see an example with hello filters that you can use toodisplay hello data in different time ranges.</span></span>

![計量與篩選器的檢視][5]

<span data-ttu-id="b139e-315">toosee 目前清單的度量資訊，請參閱[支援的 Azure 監視的度量](../monitoring-and-diagnostics/monitoring-supported-metrics.md)。</span><span class="sxs-lookup"><span data-stu-id="b139e-315">toosee a current list of metrics, see [Supported metrics with Azure Monitor](../monitoring-and-diagnostics/monitoring-supported-metrics.md).</span></span>

### <a name="alert-rules"></a><span data-ttu-id="b139e-316">警示規則</span><span class="sxs-lookup"><span data-stu-id="b139e-316">Alert rules</span></span>

<span data-ttu-id="b139e-317">您可以根據資源的計量來啟動警示規則。</span><span class="sxs-lookup"><span data-stu-id="b139e-317">You can start alert rules based on metrics for a resource.</span></span> <span data-ttu-id="b139e-318">例如，警示可以呼叫 webhook 或電子郵件系統管理員，如果 hello hello 應用程式閘道輸送量之上、 之下，或在臨界值是在指定期間內。</span><span class="sxs-lookup"><span data-stu-id="b139e-318">For example, an alert can call a webhook or email an administrator if hello throughput of hello application gateway is above, below, or at a threshold for a specified period.</span></span>

<span data-ttu-id="b139e-319">下列範例中的 hello 會引導您建立警示規則之後輸送量違反的臨界值所傳送的電子郵件 tooan 系統管理員：</span><span class="sxs-lookup"><span data-stu-id="b139e-319">hello following example walks you through creating an alert rule that sends an email tooan administrator after throughput breaches a threshold:</span></span>

1. <span data-ttu-id="b139e-320">按一下**新增度量的警示**tooopen hello**加入規則**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="b139e-320">Click **Add metric alert** tooopen hello **Add rule** blade.</span></span> <span data-ttu-id="b139e-321">您也可以連線到此刀鋒視窗中的 hello 度量 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="b139e-321">You can also reach this blade from hello metrics blade.</span></span>

   ![新增計量警示按鈕][6]

2. <span data-ttu-id="b139e-323">在 hello**加入規則**刀鋒視窗中，填寫 hello 名稱、 條件，並通知區段中，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="b139e-323">On hello **Add rule** blade, fill out hello name, condition, and notify sections, and click **OK**.</span></span>

   * <span data-ttu-id="b139e-324">在 hello**條件**選取器，選取其中一個 hello 四個值：**大於**，**大於或等於**，**小於**，或**小於或等於**。</span><span class="sxs-lookup"><span data-stu-id="b139e-324">In hello **Condition** selector, select one of hello four values: **Greater than**, **Greater than or equal**, **Less than**, or **Less than or equal to**.</span></span>

   * <span data-ttu-id="b139e-325">在 hello**期間**選取器選取的期間 5 分鐘 too6 小時。</span><span class="sxs-lookup"><span data-stu-id="b139e-325">In hello **Period** selector, select a period from 5 minutes too6 hours.</span></span>

   * <span data-ttu-id="b139e-326">如果您選取**電子郵件擁有者、 參與者與讀者**，hello 電子郵件可以有動態 hello 使用者擁有存取 toothat 資源為基礎。</span><span class="sxs-lookup"><span data-stu-id="b139e-326">If you select **Email owners, contributors, and readers**, hello email can be dynamic based on hello users who have access toothat resource.</span></span> <span data-ttu-id="b139e-327">否則，您可以提供以逗號分隔的使用者清單中 hello**其他的系統管理員 email(s)**方塊。</span><span class="sxs-lookup"><span data-stu-id="b139e-327">Otherwise, you can provide a comma-separated list of users in hello **Additional administrator email(s)** box.</span></span>

   ![新增規則刀鋒視窗][7]

<span data-ttu-id="b139e-329">如果達到 hello 閾值時，會在下列映像的 hello 類似 toohello 一封電子郵件送達：</span><span class="sxs-lookup"><span data-stu-id="b139e-329">If hello threshold is breached, an email that's similar toohello one in hello following image arrives:</span></span>

![違反臨界值的電子郵件][8]

<span data-ttu-id="b139e-331">建立計量警示之後，就會出現警示的清單，</span><span class="sxs-lookup"><span data-stu-id="b139e-331">A list of alerts appears after you create a metric alert.</span></span> <span data-ttu-id="b139e-332">它提供所有 hello 警示規則的概觀。</span><span class="sxs-lookup"><span data-stu-id="b139e-332">It provides an overview of all hello alert rules.</span></span>

![警示和規則的清單][9]

<span data-ttu-id="b139e-334">toolearn 進一步了解警示通知，請參閱[接收警示通知](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)。</span><span class="sxs-lookup"><span data-stu-id="b139e-334">toolearn more about alert notifications, see [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span>

<span data-ttu-id="b139e-335">toounderstand 進一步了解 webhook 及如何使用這些警示，請瀏覽[Azure 度量警示上設定的 webhook](../monitoring-and-diagnostics/insights-webhooks-alerts.md)。</span><span class="sxs-lookup"><span data-stu-id="b139e-335">toounderstand more about webhooks and how you can use them with alerts, visit [Configure a webhook on an Azure metric alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b139e-336">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b139e-336">Next steps</span></span>

* <span data-ttu-id="b139e-337">利用 [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md) 將計數器和事件記錄視覺化。</span><span class="sxs-lookup"><span data-stu-id="b139e-337">Visualize counter and event logs by using [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md).</span></span>
* <span data-ttu-id="b139e-338">[使用 Power BI 將您的 Azure 活動記錄視覺化](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx)部落格文章。</span><span class="sxs-lookup"><span data-stu-id="b139e-338">[Visualize your Azure activity log with Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) blog post.</span></span>
* <span data-ttu-id="b139e-339">[在 Power BI 和其他工具中檢視和分析 Azure 活動記錄](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/)部落格文章。</span><span class="sxs-lookup"><span data-stu-id="b139e-339">[View and analyze Azure activity logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) blog post.</span></span>

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
