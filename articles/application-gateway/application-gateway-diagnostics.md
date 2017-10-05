---
title: "監視應用程式閘道的存取記錄、效能記錄、後端健康情況及計量 | Microsoft Docs"
description: "了解如何啟用和管理應用程式閘道的存取記錄和效能記錄"
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
ms.openlocfilehash: 12c252340b82aba5ee69b12db83353750782e7c5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="back-end-health-diagnostic-logs-and-metrics-for-application-gateway"></a><span data-ttu-id="60821-103">應用程式閘道的後端健康情況、診斷記錄和計量</span><span class="sxs-lookup"><span data-stu-id="60821-103">Back-end health, diagnostic logs, and metrics for Application Gateway</span></span>

<span data-ttu-id="60821-104">使用 Azure 應用程式閘道，您可以下列方式監視資源：</span><span class="sxs-lookup"><span data-stu-id="60821-104">By using Azure Application Gateway, you can monitor resources in the following ways:</span></span>

* <span data-ttu-id="60821-105">[後端健康情況](#back-end-health)：應用程式閘道提供透過 Azure 入口網站和 PowerShell 監視後端集區中伺服器健康情況的功能。</span><span class="sxs-lookup"><span data-stu-id="60821-105">[Back-end health](#back-end-health): Application Gateway provides the capability to monitor the health of the servers in the back-end pools through the Azure portal and through PowerShell.</span></span> <span data-ttu-id="60821-106">您也可以透過效能診斷記錄找到後端集區的健康情況。</span><span class="sxs-lookup"><span data-stu-id="60821-106">You can also find the health of the back-end pools through the performance diagnostic logs.</span></span>

* <span data-ttu-id="60821-107">[記錄](#diagnostic-logs)：記錄能夠儲存效能、存取和其他資料，或從資源取用記錄以便進行監視。</span><span class="sxs-lookup"><span data-stu-id="60821-107">[Logs](#diagnostic-logs): Logs allow for performance, access, and other data to be saved or consumed from a resource for monitoring purposes.</span></span>

* <span data-ttu-id="60821-108">[計量](#metrics)：應用程式閘道目前有一個計量。</span><span class="sxs-lookup"><span data-stu-id="60821-108">[Metrics](#metrics): Application Gateway currently has one metric.</span></span> <span data-ttu-id="60821-109">此計量會測量應用程式閘道的輸送量，以每秒的位元組數為單位。</span><span class="sxs-lookup"><span data-stu-id="60821-109">This metric measures the throughput of the application gateway in bytes per second.</span></span>

## <a name="back-end-health"></a><span data-ttu-id="60821-110">後端健康情況</span><span class="sxs-lookup"><span data-stu-id="60821-110">Back-end health</span></span>

<span data-ttu-id="60821-111">應用程式閘道提供透過入口網站、PowerShell 及命令列界面 (CLI) 監視後端集區中個別成員健康情況的功能。</span><span class="sxs-lookup"><span data-stu-id="60821-111">Application Gateway provides the capability to monitor the health of individual members of the back-end pools through the portal, PowerShell, and the command-line interface (CLI).</span></span> <span data-ttu-id="60821-112">您也可以透過效能診斷記錄找到彙總的後端集區健康情況摘要。</span><span class="sxs-lookup"><span data-stu-id="60821-112">You can also find an aggregated health summary of back-end pools through the performance diagnostic logs.</span></span> 

<span data-ttu-id="60821-113">後端健康情況報表會將應用程式閘道健康情況探查的輸出反映到後端執行個體。</span><span class="sxs-lookup"><span data-stu-id="60821-113">The back-end health report reflects the output of the Application Gateway health probe to the back-end instances.</span></span> <span data-ttu-id="60821-114">當探查成功且後端可以接收流量，則視為狀況良好。</span><span class="sxs-lookup"><span data-stu-id="60821-114">When probing is successful and the back end can receive traffic, it's considered healthy.</span></span> <span data-ttu-id="60821-115">否則，視為狀況不良。</span><span class="sxs-lookup"><span data-stu-id="60821-115">Otherwise, it's considered unhealthy.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="60821-116">如果應用程式閘道子網路上有網路安全性群組 (NSG)，請在應用程式閘道子網路上開啟連接埠範圍 65503-65534，供輸入流量使用。</span><span class="sxs-lookup"><span data-stu-id="60821-116">If there is a network security group (NSG) on an Application Gateway subnet, open port ranges 65503-65534 on the Application Gateway subnet for inbound traffic.</span></span> <span data-ttu-id="60821-117">需要這些連接埠，後端健康情況 API 才能運作。</span><span class="sxs-lookup"><span data-stu-id="60821-117">These ports are required for the back-end health API to work.</span></span>


### <a name="view-back-end-health-through-the-portal"></a><span data-ttu-id="60821-118">透過入口網站檢視後端健康情況</span><span class="sxs-lookup"><span data-stu-id="60821-118">View back-end health through the portal</span></span>

<span data-ttu-id="60821-119">入口網站中會自動提供後端的健康情況。</span><span class="sxs-lookup"><span data-stu-id="60821-119">In the portal, back-end health is provided automatically.</span></span> <span data-ttu-id="60821-120">在現有的應用程式閘道中，選取 [監視]  >  [後端健康情況]。</span><span class="sxs-lookup"><span data-stu-id="60821-120">In an existing application gateway, select **Monitoring** > **Backend health**.</span></span> 

<span data-ttu-id="60821-121">後端集區中的每個成員均會列於此頁面中 (無論是 NIC、IP 或 FQDN)。</span><span class="sxs-lookup"><span data-stu-id="60821-121">Each member in the back-end pool is listed on this page (whether it's a NIC, IP, or FQDN).</span></span> <span data-ttu-id="60821-122">後端集區名稱、連接埠、後端 HTTP 設定名稱和健康情況均會顯示。</span><span class="sxs-lookup"><span data-stu-id="60821-122">Back-end pool name, port, back-end HTTP settings name, and health status are shown.</span></span> <span data-ttu-id="60821-123">健康情況的有效值為「狀況良好」、「狀況不良」和「未知」。</span><span class="sxs-lookup"><span data-stu-id="60821-123">Valid values for health status are **Healthy**, **Unhealthy**, and **Unknown**.</span></span>

> [!NOTE]
> <span data-ttu-id="60821-124">如果您看到後端健康情況為 [未知]，請確定 NSG 規則、使用者定義的路由 (UDR) 或虛擬網路中的自訂 DNS 並未封鎖對後端的存取。</span><span class="sxs-lookup"><span data-stu-id="60821-124">If you see a back-end health status of **Unknown**, ensure that access to the back end is not blocked by an NSG rule, a user-defined route (UDR), or a custom DNS in the virtual network.</span></span>

![後端健康情況][10]

### <a name="view-back-end-health-through-powershell"></a><span data-ttu-id="60821-126">透過 PowerShell 檢視後端健康情況</span><span class="sxs-lookup"><span data-stu-id="60821-126">View back-end health through PowerShell</span></span>

<span data-ttu-id="60821-127">下列 PowerShell 程式碼示範如何使用 `Get-AzureRmApplicationGatewayBackendHealth` Cmdlet 檢視後端健康情況：</span><span class="sxs-lookup"><span data-stu-id="60821-127">The following PowerShell code shows how to view back-end health by using the `Get-AzureRmApplicationGatewayBackendHealth` cmdlet:</span></span>

```powershell
Get-AzureRmApplicationGatewayBackendHealth -Name ApplicationGateway1 -ResourceGroupName Contoso
```

### <a name="view-back-end-health-through-azure-cli-20"></a><span data-ttu-id="60821-128">透過 Azure CLI 2.0 檢視後端健康情況</span><span class="sxs-lookup"><span data-stu-id="60821-128">View back-end health through Azure CLI 2.0</span></span>

```azurecli
az network application-gateway show-backend-health --resource-group AdatumAppGatewayRG --name AdatumAppGateway
```

### <a name="results"></a><span data-ttu-id="60821-129">結果</span><span class="sxs-lookup"><span data-stu-id="60821-129">Results</span></span>

<span data-ttu-id="60821-130">以下是回應範例：</span><span class="sxs-lookup"><span data-stu-id="60821-130">The following snippet shows an example of the response:</span></span>

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

## <span data-ttu-id="60821-131"><a name="diagnostic-logging"></a>診斷記錄</span><span class="sxs-lookup"><span data-stu-id="60821-131"><a name="diagnostic-logging"></a>Diagnostic logs</span></span>

<span data-ttu-id="60821-132">您可以在 Azure 中使用不同類型的記錄檔來管理和針對應用程式閘道進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="60821-132">You can use different types of logs in Azure to manage and troubleshoot application gateways.</span></span> <span data-ttu-id="60821-133">您可以透過入口網站存取其中一些記錄。</span><span class="sxs-lookup"><span data-stu-id="60821-133">You can access some of these logs through the portal.</span></span> <span data-ttu-id="60821-134">可以從 Azure Blob 儲存體擷取所有記錄，並且在不同的工具中進行檢視 (例如 [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md)、Excel、PowerBI)。</span><span class="sxs-lookup"><span data-stu-id="60821-134">All logs can be extracted from Azure Blob storage and viewed in different tools, such as [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md), Excel, and Power BI.</span></span> <span data-ttu-id="60821-135">您可以從下列清單進一步了解不同類型的記錄檔：</span><span class="sxs-lookup"><span data-stu-id="60821-135">You can learn more about the different types of logs from the following list:</span></span>

* <span data-ttu-id="60821-136">**活動記錄**：您可以使用 [Azure 活動記錄](../monitoring-and-diagnostics/insights-debugging-with-events.md) (之前稱為「作業記錄和稽核記錄」) 來檢視提交至您的 Azure 訂用帳戶的所有作業及其狀態。</span><span class="sxs-lookup"><span data-stu-id="60821-136">**Activity log**: You can use [Azure activity logs](../monitoring-and-diagnostics/insights-debugging-with-events.md) (formerly known as operational logs and audit logs) to view all operations that are submitted to your Azure subscription, and their status.</span></span> <span data-ttu-id="60821-137">預設會收集活動記錄，您可在 Azure 入口網站中檢視它們。</span><span class="sxs-lookup"><span data-stu-id="60821-137">Activity log entries are collected by default, and you can view them in the Azure portal.</span></span>
* <span data-ttu-id="60821-138">**存取記錄**：您可以使用此記錄來檢視應用程式閘道存取模式及分析重要資訊，包括呼叫端的 IP、要求的 URL、回應延遲、傳回碼、輸入和輸出位元組。每隔 300 秒會收集一次存取記錄。</span><span class="sxs-lookup"><span data-stu-id="60821-138">**Access log**: You can use this log to view Application Gateway access patterns and analyze important information, including the caller's IP, requested URL, response latency, return code, and bytes in and out. An access log is collected every 300 seconds.</span></span> <span data-ttu-id="60821-139">此記錄檔包含每個應用程式閘道執行個體的一筆記錄。</span><span class="sxs-lookup"><span data-stu-id="60821-139">This log contains one record per instance of Application Gateway.</span></span> <span data-ttu-id="60821-140">應用程式閘道執行個體可以由 instanceId 屬性識別。</span><span class="sxs-lookup"><span data-stu-id="60821-140">The Application Gateway instance can be identified by the instanceId property.</span></span>
* <span data-ttu-id="60821-141">**效能記錄**：您可以使用此記錄來檢視應用程式閘道執行個體的執行情況。</span><span class="sxs-lookup"><span data-stu-id="60821-141">**Performance log**: You can use this log to view how Application Gateway instances are performing.</span></span> <span data-ttu-id="60821-142">此記錄會擷取每個執行個體的效能資訊，包括提供的要求總數、輸送量 (以位元組為單位)、提供的總要求數、失敗的要求計數、狀況良好和狀況不良的後端執行個體計數。</span><span class="sxs-lookup"><span data-stu-id="60821-142">This log captures performance information for each instance, including total requests served, throughput in bytes, total requests served, failed request count, and healthy and unhealthy back-end instance count.</span></span> <span data-ttu-id="60821-143">每隔 60 秒會收集一次效能記錄。</span><span class="sxs-lookup"><span data-stu-id="60821-143">A performance log is collected every 60 seconds.</span></span>
* <span data-ttu-id="60821-144">**防火牆記錄**：您可以使用此記錄，檢視透過應用程式閘道的偵測或防止模式 (依 Web 應用程式防火牆的設定) 所記錄的要求。</span><span class="sxs-lookup"><span data-stu-id="60821-144">**Firewall log**: You can use this log to view the requests that are logged through either detection or prevention mode of an application gateway that is configured with the web application firewall.</span></span>

> [!NOTE]
> <span data-ttu-id="60821-145">記錄僅適用於在 Azure Resource Manager 部署模型中部署的資源。</span><span class="sxs-lookup"><span data-stu-id="60821-145">Logs are available only for resources deployed in the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="60821-146">您無法將記錄檔使用於傳統部署模型中的資源。</span><span class="sxs-lookup"><span data-stu-id="60821-146">You cannot use logs for resources in the classic deployment model.</span></span> <span data-ttu-id="60821-147">若要深入了解這兩個模型，請參閱[了解 Resource Manager 部署和傳統部署](../azure-resource-manager/resource-manager-deployment-model.md)一文。</span><span class="sxs-lookup"><span data-stu-id="60821-147">For a better understanding of the two models, see the [Understanding Resource Manager deployment and classic deployment](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>

<span data-ttu-id="60821-148">您有三個選項可用來排序您的記錄：</span><span class="sxs-lookup"><span data-stu-id="60821-148">You have three options for storing your logs:</span></span>

* <span data-ttu-id="60821-149">**儲存體帳戶**：如果記錄會儲存一段較長的持續期間，並在需要時加以檢閱，則最好針對記錄使用儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="60821-149">**Storage account**: Storage accounts are best used for logs when logs are stored for a longer duration and reviewed when needed.</span></span>
* <span data-ttu-id="60821-150">**事件中樞**：如果要整合其他安全性資訊和事件管理 (SEIM) 工具以便在資源上取得警示，則事件中樞是絕佳的選項。</span><span class="sxs-lookup"><span data-stu-id="60821-150">**Event hubs**: Event hubs are a great option for integrating with other security information and event management (SEIM) tools to get alerts on your resources.</span></span>
* <span data-ttu-id="60821-151">**Log Analytics**：Log Analytics 最適合用來進行應用程式的一般即時監視，或查看趨勢。</span><span class="sxs-lookup"><span data-stu-id="60821-151">**Log Analytics**: Log Analytics is best used for general real-time monitoring of your application or looking at trends.</span></span>

### <a name="enable-logging-through-powershell"></a><span data-ttu-id="60821-152">透過 PowerShell 啟用記錄功能</span><span class="sxs-lookup"><span data-stu-id="60821-152">Enable logging through PowerShell</span></span>

<span data-ttu-id="60821-153">每個 Resource Manager 資源都會自動啟用活動記錄功能。</span><span class="sxs-lookup"><span data-stu-id="60821-153">Activity logging is automatically enabled for every Resource Manager resource.</span></span> <span data-ttu-id="60821-154">您必須啟用存取和效能記錄功能，才能開始收集可透過這些記錄檔取得的資料。</span><span class="sxs-lookup"><span data-stu-id="60821-154">You must enable access and performance logging to start collecting the data available through those logs.</span></span> <span data-ttu-id="60821-155">使用下列步驟啟用記錄：</span><span class="sxs-lookup"><span data-stu-id="60821-155">To enable logging, use the following steps:</span></span>

1. <span data-ttu-id="60821-156">請記下您的儲存體帳戶的資源識別碼 (記錄資料的儲存之處)。</span><span class="sxs-lookup"><span data-stu-id="60821-156">Note your storage account's resource ID, where the log data is stored.</span></span> <span data-ttu-id="60821-157">此值的形式為：/subscriptions/\<subscriptionId\>/resourceGroups/\<資源群組名稱\>/providers/Microsoft.Storage/storageAccounts/\<儲存體帳戶名稱\>。</span><span class="sxs-lookup"><span data-stu-id="60821-157">This value is of the form: /subscriptions/\<subscriptionId\>/resourceGroups/\<resource group name\>/providers/Microsoft.Storage/storageAccounts/\<storage account name\>.</span></span> <span data-ttu-id="60821-158">您可以使用訂用帳戶中的所有儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="60821-158">You can use any storage account in your subscription.</span></span> <span data-ttu-id="60821-159">您可以使用 Azure 入口網站來尋找此資訊。</span><span class="sxs-lookup"><span data-stu-id="60821-159">You can use the Azure portal to find this information.</span></span>

    ![入口網站：儲存體帳戶的資源識別碼](./media/application-gateway-diagnostics/diagnostics1.png)

2. <span data-ttu-id="60821-161">請記下您的應用程式閘道的資源識別碼 (將為其啟用記錄功能)。</span><span class="sxs-lookup"><span data-stu-id="60821-161">Note your application gateway's resource ID for which logging is enabled.</span></span> <span data-ttu-id="60821-162">此值的形式為：/subscriptions/\<subscriptionId\>/resourceGroups/\<資源群組名稱\>/providers/Microsoft.Network/applicationGateways/\<應用程式閘道名稱\>。</span><span class="sxs-lookup"><span data-stu-id="60821-162">This value is of the form: /subscriptions/\<subscriptionId\>/resourceGroups/\<resource group name\>/providers/Microsoft.Network/applicationGateways/\<application gateway name\>.</span></span> <span data-ttu-id="60821-163">您可以使用入口網站來尋找此資訊。</span><span class="sxs-lookup"><span data-stu-id="60821-163">You can use the portal to find this information.</span></span>

    ![入口網站：應用程式閘道的資源識別碼](./media/application-gateway-diagnostics/diagnostics2.png)

3. <span data-ttu-id="60821-165">使用下列 Powershell Cmdlet 啟用診斷記錄功能：</span><span class="sxs-lookup"><span data-stu-id="60821-165">Enable diagnostic logging by using the following PowerShell cmdlet:</span></span>

    ```powershell
    Set-AzureRmDiagnosticSetting  -ResourceId /subscriptions/<subscriptionId>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name> -StorageAccountId /subscriptions/<subscriptionId>/resourceGroups/<resource group name>/providers/Microsoft.Storage/storageAccounts/<storage account name> -Enabled $true     
    ```
    
> [!TIP] 
><span data-ttu-id="60821-166">活動記錄檔不需要個別的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="60821-166">Activity logs do not require a separate storage account.</span></span> <span data-ttu-id="60821-167">將儲存體用於記錄存取和效能會產生服務費用。</span><span class="sxs-lookup"><span data-stu-id="60821-167">The use of storage for access and performance logging incurs service charges.</span></span>

### <a name="enable-logging-through-the-azure-portal"></a><span data-ttu-id="60821-168">透過 Azure 入口網站啟用記錄功能</span><span class="sxs-lookup"><span data-stu-id="60821-168">Enable logging through the Azure portal</span></span>

1. <span data-ttu-id="60821-169">在 Azure 入口網站中，找到您的資源並按一下 [診斷記錄]。</span><span class="sxs-lookup"><span data-stu-id="60821-169">In the Azure portal, find your resource and click **Diagnostic logs**.</span></span>

   <span data-ttu-id="60821-170">應用程式閘道有三個記錄：</span><span class="sxs-lookup"><span data-stu-id="60821-170">For Application Gateway, three logs are available:</span></span>

   * <span data-ttu-id="60821-171">存取記錄檔</span><span class="sxs-lookup"><span data-stu-id="60821-171">Access log</span></span>
   * <span data-ttu-id="60821-172">效能記錄檔</span><span class="sxs-lookup"><span data-stu-id="60821-172">Performance log</span></span>
   * <span data-ttu-id="60821-173">防火牆記錄檔</span><span class="sxs-lookup"><span data-stu-id="60821-173">Firewall log</span></span>

2. <span data-ttu-id="60821-174">若要開始收集資料，請按一下 [開啟診斷]。</span><span class="sxs-lookup"><span data-stu-id="60821-174">To start collecting data, click **Turn on diagnostics**.</span></span>

   ![開啟診斷][1]

3. <span data-ttu-id="60821-176">[診斷設定] 刀鋒視窗中提供診斷記錄的設定。</span><span class="sxs-lookup"><span data-stu-id="60821-176">The **Diagnostics settings** blade provides the settings for the diagnostic logs.</span></span> <span data-ttu-id="60821-177">在此範例中，Log Analytics 會儲存記錄。</span><span class="sxs-lookup"><span data-stu-id="60821-177">In this example, Log Analytics stores the logs.</span></span> <span data-ttu-id="60821-178">按一下 [Log Analytics] 底下的 [設定] 來設定您的工作區。</span><span class="sxs-lookup"><span data-stu-id="60821-178">Click **Configure** under **Log Analytics** to configure your workspace.</span></span> <span data-ttu-id="60821-179">您也可以使用事件中樞和儲存體帳戶來儲存診斷記錄。</span><span class="sxs-lookup"><span data-stu-id="60821-179">You can also use event hubs and a storage account to save the diagnostic logs.</span></span>

   ![啟動設定程序][2]

4. <span data-ttu-id="60821-181">選擇現有的 Operations Management Suite (OMS) 工作區或建立新的。</span><span class="sxs-lookup"><span data-stu-id="60821-181">Choose an existing Operations Management Suite (OMS) workspace or create a new one.</span></span> <span data-ttu-id="60821-182">這個範例使用現有工作區。</span><span class="sxs-lookup"><span data-stu-id="60821-182">This example uses an existing one.</span></span>

   ![OMS 工作區的選項][3]

5. <span data-ttu-id="60821-184">確認設定並按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="60821-184">Confirm the settings and click **Save**.</span></span>

   ![診斷設定刀鋒視窗與選項][4]

### <a name="activity-log"></a><span data-ttu-id="60821-186">活動記錄檔</span><span class="sxs-lookup"><span data-stu-id="60821-186">Activity log</span></span>

<span data-ttu-id="60821-187">根據預設，Azure 會產生活動記錄。</span><span class="sxs-lookup"><span data-stu-id="60821-187">Azure generates the activity log by default.</span></span> <span data-ttu-id="60821-188">記錄會在 Azure 的事件記錄存放區中保留 90 天。</span><span class="sxs-lookup"><span data-stu-id="60821-188">The logs are preserved for 90 days in the Azure event logs store.</span></span> <span data-ttu-id="60821-189">閱讀[檢視事件和活動記錄](../monitoring-and-diagnostics/insights-debugging-with-events.md)一文，深入了解這些記錄。</span><span class="sxs-lookup"><span data-stu-id="60821-189">Learn more about these logs by reading the [View events and activity log](../monitoring-and-diagnostics/insights-debugging-with-events.md) article.</span></span>

### <a name="access-log"></a><span data-ttu-id="60821-190">存取記錄檔</span><span class="sxs-lookup"><span data-stu-id="60821-190">Access log</span></span>

<span data-ttu-id="60821-191">只有當您如上述步驟所述，在每個應用程式閘道上啟用存取記錄，才會產生存取記錄。</span><span class="sxs-lookup"><span data-stu-id="60821-191">The access log is generated only if you've enabled it on each Application Gateway instance, as detailed in the preceding steps.</span></span> <span data-ttu-id="60821-192">資料會儲存在您啟用記錄功能時指定的儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="60821-192">The data is stored in the storage account that you specified when you enabled the logging.</span></span> <span data-ttu-id="60821-193">應用程式閘道的每次存取會以 JSON 格式記錄下來，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="60821-193">Each access of Application Gateway is logged in JSON format, as shown in the following example:</span></span>


|<span data-ttu-id="60821-194">值</span><span class="sxs-lookup"><span data-stu-id="60821-194">Value</span></span>  |<span data-ttu-id="60821-195">說明</span><span class="sxs-lookup"><span data-stu-id="60821-195">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="60821-196">instanceId</span><span class="sxs-lookup"><span data-stu-id="60821-196">instanceId</span></span>     | <span data-ttu-id="60821-197">處理要求的應用程式閘道執行個體。</span><span class="sxs-lookup"><span data-stu-id="60821-197">Application Gateway instance that served the request.</span></span>        |
|<span data-ttu-id="60821-198">clientIP</span><span class="sxs-lookup"><span data-stu-id="60821-198">clientIP</span></span>     | <span data-ttu-id="60821-199">要求的原始 IP。</span><span class="sxs-lookup"><span data-stu-id="60821-199">Originating IP for the request.</span></span>        |
|<span data-ttu-id="60821-200">clientPort</span><span class="sxs-lookup"><span data-stu-id="60821-200">clientPort</span></span>     | <span data-ttu-id="60821-201">要求的原始連接埠。</span><span class="sxs-lookup"><span data-stu-id="60821-201">Originating port for the request.</span></span>       |
|<span data-ttu-id="60821-202">httpMethod</span><span class="sxs-lookup"><span data-stu-id="60821-202">httpMethod</span></span>     | <span data-ttu-id="60821-203">要求使用的 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="60821-203">HTTP method used by the request.</span></span>       |
|<span data-ttu-id="60821-204">requestUri</span><span class="sxs-lookup"><span data-stu-id="60821-204">requestUri</span></span>     | <span data-ttu-id="60821-205">接收之要求的 URI。</span><span class="sxs-lookup"><span data-stu-id="60821-205">URI of the received request.</span></span>        |
|<span data-ttu-id="60821-206">RequestQuery</span><span class="sxs-lookup"><span data-stu-id="60821-206">RequestQuery</span></span>     | <span data-ttu-id="60821-207">**Server-Routed**：傳送要求的後端集區執行個體。</span><span class="sxs-lookup"><span data-stu-id="60821-207">**Server-Routed**: Back-end pool instance that was sent the request.</span></span> </br> <span data-ttu-id="60821-208">**X-AzureApplicationGateway-LOG-ID**：要求所使用的相互關聯識別碼。</span><span class="sxs-lookup"><span data-stu-id="60821-208">**X-AzureApplicationGateway-LOG-ID**: Correlation ID used for the request.</span></span> <span data-ttu-id="60821-209">它可以用來針對後端伺服器上的流量問題進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="60821-209">It can be used to troubleshoot traffic issues on the back-end servers.</span></span> </br><span data-ttu-id="60821-210">**SERVER-STATUS**：應用程式閘道從後端收到的 HTTP 回應碼。</span><span class="sxs-lookup"><span data-stu-id="60821-210">**SERVER-STATUS**: HTTP response code that Application Gateway received from the back end.</span></span>       |
|<span data-ttu-id="60821-211">UserAgent</span><span class="sxs-lookup"><span data-stu-id="60821-211">UserAgent</span></span>     | <span data-ttu-id="60821-212">HTTP 要求標頭中的使用者代理程式。</span><span class="sxs-lookup"><span data-stu-id="60821-212">User agent from the HTTP request header.</span></span>        |
|<span data-ttu-id="60821-213">httpStatus</span><span class="sxs-lookup"><span data-stu-id="60821-213">httpStatus</span></span>     | <span data-ttu-id="60821-214">應用程式閘道傳回用戶端的 HTTP 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="60821-214">HTTP status code returned to the client from Application Gateway.</span></span>       |
|<span data-ttu-id="60821-215">httpVersion</span><span class="sxs-lookup"><span data-stu-id="60821-215">httpVersion</span></span>     | <span data-ttu-id="60821-216">要求的 HTTP 版本。</span><span class="sxs-lookup"><span data-stu-id="60821-216">HTTP version of the request.</span></span>        |
|<span data-ttu-id="60821-217">receivedBytes</span><span class="sxs-lookup"><span data-stu-id="60821-217">receivedBytes</span></span>     | <span data-ttu-id="60821-218">接收的封包大小，單位為位元組。</span><span class="sxs-lookup"><span data-stu-id="60821-218">Size of packet received, in bytes.</span></span>        |
|<span data-ttu-id="60821-219">sentBytes</span><span class="sxs-lookup"><span data-stu-id="60821-219">sentBytes</span></span>| <span data-ttu-id="60821-220">傳送的封包大小，單位為位元組。</span><span class="sxs-lookup"><span data-stu-id="60821-220">Size of packet sent, in bytes.</span></span>|
|<span data-ttu-id="60821-221">timeTaken</span><span class="sxs-lookup"><span data-stu-id="60821-221">timeTaken</span></span>| <span data-ttu-id="60821-222">處理要求並傳送其回應所花費的時間長度，單位為毫秒。</span><span class="sxs-lookup"><span data-stu-id="60821-222">Length of time (in milliseconds) that it takes for a request to be processed and its response to be sent.</span></span> <span data-ttu-id="60821-223">算法是從應用程式閘道收到 HTTP 要求的回應第一個位元組的時間，到回應傳送作業完成時的時間間隔。</span><span class="sxs-lookup"><span data-stu-id="60821-223">This is calculated as the interval from the time when Application Gateway receives the first byte of an HTTP request to the time when the response send operation finishes.</span></span> <span data-ttu-id="60821-224">請務必注意，timeTaken 欄位通常包含要求和回應封包在網路上傳輸的時間。</span><span class="sxs-lookup"><span data-stu-id="60821-224">It's important to note that the Time-Taken field usually includes the time that the request and response packets are traveling over the network.</span></span> |
|<span data-ttu-id="60821-225">sslEnabled</span><span class="sxs-lookup"><span data-stu-id="60821-225">sslEnabled</span></span>| <span data-ttu-id="60821-226">與後端集區的通訊是否使用 SSL。</span><span class="sxs-lookup"><span data-stu-id="60821-226">Whether communication to the back-end pools used SSL.</span></span> <span data-ttu-id="60821-227">有效值為 on 和 off。</span><span class="sxs-lookup"><span data-stu-id="60821-227">Valid values are on and off.</span></span>|
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

### <a name="performance-log"></a><span data-ttu-id="60821-228">效能記錄檔</span><span class="sxs-lookup"><span data-stu-id="60821-228">Performance log</span></span>

<span data-ttu-id="60821-229">只有當您如上述步驟所述，在每個應用程式閘道上啟用效能記錄，才會產生效能記錄。</span><span class="sxs-lookup"><span data-stu-id="60821-229">The performance log is generated only if you have enabled it on each Application Gateway instance, as detailed in the preceding steps.</span></span> <span data-ttu-id="60821-230">資料會儲存在您啟用記錄功能時指定的儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="60821-230">The data is stored in the storage account that you specified when you enabled the logging.</span></span> <span data-ttu-id="60821-231">產生效能記錄資料的時間間隔為 1 分鐘。</span><span class="sxs-lookup"><span data-stu-id="60821-231">The performance log data is generated in 1-minute intervals.</span></span> <span data-ttu-id="60821-232">會記錄下列資料：</span><span class="sxs-lookup"><span data-stu-id="60821-232">The following data is logged:</span></span>


|<span data-ttu-id="60821-233">值</span><span class="sxs-lookup"><span data-stu-id="60821-233">Value</span></span>  |<span data-ttu-id="60821-234">說明</span><span class="sxs-lookup"><span data-stu-id="60821-234">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="60821-235">instanceId</span><span class="sxs-lookup"><span data-stu-id="60821-235">instanceId</span></span>     |  <span data-ttu-id="60821-236">將產生此應用程式閘道執行個體的效能資料。</span><span class="sxs-lookup"><span data-stu-id="60821-236">Application Gateway instance for which performance data is being generated.</span></span> <span data-ttu-id="60821-237">應用程式閘道若有多個執行個體，則是一個執行個體一行資料。</span><span class="sxs-lookup"><span data-stu-id="60821-237">For a multiple-instance application gateway, there is one row per instance.</span></span>        |
|<span data-ttu-id="60821-238">healthyHostCount</span><span class="sxs-lookup"><span data-stu-id="60821-238">healthyHostCount</span></span>     | <span data-ttu-id="60821-239">後端集區中狀況良好主機的數目。</span><span class="sxs-lookup"><span data-stu-id="60821-239">Number of healthy hosts in the back-end pool.</span></span>        |
|<span data-ttu-id="60821-240">unHealthyHostCount</span><span class="sxs-lookup"><span data-stu-id="60821-240">unHealthyHostCount</span></span>     | <span data-ttu-id="60821-241">後端集區中狀況不良主機的數目。</span><span class="sxs-lookup"><span data-stu-id="60821-241">Number of unhealthy hosts in the back-end pool.</span></span>        |
|<span data-ttu-id="60821-242">requestCount</span><span class="sxs-lookup"><span data-stu-id="60821-242">requestCount</span></span>     | <span data-ttu-id="60821-243">處理的要求數目。</span><span class="sxs-lookup"><span data-stu-id="60821-243">Number of requests served.</span></span>        |
|<span data-ttu-id="60821-244">latency</span><span class="sxs-lookup"><span data-stu-id="60821-244">latency</span></span> | <span data-ttu-id="60821-245">從執行個體到處理要求的後端之間的要求延遲，單位為毫秒。</span><span class="sxs-lookup"><span data-stu-id="60821-245">Latency (in milliseconds) of requests from the instance to the back end that serves the requests.</span></span> |
|<span data-ttu-id="60821-246">failedRequestCount</span><span class="sxs-lookup"><span data-stu-id="60821-246">failedRequestCount</span></span>| <span data-ttu-id="60821-247">失敗的要求數目。</span><span class="sxs-lookup"><span data-stu-id="60821-247">Number of failed requests.</span></span>|
|<span data-ttu-id="60821-248">throughput</span><span class="sxs-lookup"><span data-stu-id="60821-248">throughput</span></span>| <span data-ttu-id="60821-249">自最後一個記錄以來的平均輸送量，測量單位為每秒位元組。</span><span class="sxs-lookup"><span data-stu-id="60821-249">Average throughput since the last log, measured in bytes per second.</span></span>|

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
> <span data-ttu-id="60821-250">延遲的計算是從收到 HTTP 要求的第一個位元組時算起，到送出 HTTP 回應的最後一個位元組時結束。</span><span class="sxs-lookup"><span data-stu-id="60821-250">Latency is calculated from the time when the first byte of the HTTP request is received to the time when the last byte of the HTTP response is sent.</span></span> <span data-ttu-id="60821-251">是應用程式閘道處理時間，加上網路傳送到後端的時間，再加上後端處理要求所花時間的總和。</span><span class="sxs-lookup"><span data-stu-id="60821-251">It's the sum of the Application Gateway processing time plus the network cost to the back end, plus the time that the back end takes to process the request.</span></span>

### <a name="firewall-log"></a><span data-ttu-id="60821-252">防火牆記錄檔</span><span class="sxs-lookup"><span data-stu-id="60821-252">Firewall log</span></span>

<span data-ttu-id="60821-253">只有當您如上述步驟所述，在每個應用程式閘道上啟用防火牆記錄，才會產生防火牆記錄。</span><span class="sxs-lookup"><span data-stu-id="60821-253">The firewall log is generated only if you have enabled it for each application gateway, as detailed in the preceding steps.</span></span> <span data-ttu-id="60821-254">此記錄也需要在應用程式閘道上設定該 Web 應用程式防火牆。</span><span class="sxs-lookup"><span data-stu-id="60821-254">This log also requires that the web application firewall is configured on an application gateway.</span></span> <span data-ttu-id="60821-255">資料會儲存在您啟用記錄功能時指定的儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="60821-255">The data is stored in the storage account that you specified when you enabled the logging.</span></span> <span data-ttu-id="60821-256">會記錄下列資料：</span><span class="sxs-lookup"><span data-stu-id="60821-256">The following data is logged:</span></span>


|<span data-ttu-id="60821-257">值</span><span class="sxs-lookup"><span data-stu-id="60821-257">Value</span></span>  |<span data-ttu-id="60821-258">說明</span><span class="sxs-lookup"><span data-stu-id="60821-258">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="60821-259">instanceId</span><span class="sxs-lookup"><span data-stu-id="60821-259">instanceId</span></span>     | <span data-ttu-id="60821-260">將產生此應用程式閘道執行個體的防火牆資料。</span><span class="sxs-lookup"><span data-stu-id="60821-260">Application Gateway instance for which firewall data is being generated.</span></span> <span data-ttu-id="60821-261">應用程式閘道若有多個執行個體，則是一個執行個體一行資料。</span><span class="sxs-lookup"><span data-stu-id="60821-261">For a multiple-instance application gateway, there is one row per instance.</span></span>         |
|<span data-ttu-id="60821-262">clientIp</span><span class="sxs-lookup"><span data-stu-id="60821-262">clientIp</span></span>     |   <span data-ttu-id="60821-263">要求的原始 IP。</span><span class="sxs-lookup"><span data-stu-id="60821-263">Originating IP for the request.</span></span>      |
|<span data-ttu-id="60821-264">clientPort</span><span class="sxs-lookup"><span data-stu-id="60821-264">clientPort</span></span>     |  <span data-ttu-id="60821-265">要求的原始連接埠。</span><span class="sxs-lookup"><span data-stu-id="60821-265">Originating port for the request.</span></span>       |
|<span data-ttu-id="60821-266">requestUri</span><span class="sxs-lookup"><span data-stu-id="60821-266">requestUri</span></span>     | <span data-ttu-id="60821-267">接收之要求的 URL。</span><span class="sxs-lookup"><span data-stu-id="60821-267">URL of the received request.</span></span>       |
|<span data-ttu-id="60821-268">ruleSetType</span><span class="sxs-lookup"><span data-stu-id="60821-268">ruleSetType</span></span>     | <span data-ttu-id="60821-269">規則集類型。</span><span class="sxs-lookup"><span data-stu-id="60821-269">Rule set type.</span></span> <span data-ttu-id="60821-270">可用的值是 OWASP。</span><span class="sxs-lookup"><span data-stu-id="60821-270">The available value is OWASP.</span></span>        |
|<span data-ttu-id="60821-271">ruleSetVersion</span><span class="sxs-lookup"><span data-stu-id="60821-271">ruleSetVersion</span></span>     | <span data-ttu-id="60821-272">規則集版本。</span><span class="sxs-lookup"><span data-stu-id="60821-272">Rule set version used.</span></span> <span data-ttu-id="60821-273">可用值為 2.2.9 和 3.0。</span><span class="sxs-lookup"><span data-stu-id="60821-273">Available values are 2.2.9 and 3.0.</span></span>     |
|<span data-ttu-id="60821-274">ruleId</span><span class="sxs-lookup"><span data-stu-id="60821-274">ruleId</span></span>     | <span data-ttu-id="60821-275">觸發事件的規則識別碼。</span><span class="sxs-lookup"><span data-stu-id="60821-275">Rule ID of the triggering event.</span></span>        |
|<span data-ttu-id="60821-276">Message</span><span class="sxs-lookup"><span data-stu-id="60821-276">message</span></span>     | <span data-ttu-id="60821-277">方便使用的觸發事件訊息。</span><span class="sxs-lookup"><span data-stu-id="60821-277">User-friendly message for the triggering event.</span></span> <span data-ttu-id="60821-278">詳細資料區段中會提供詳細資料。</span><span class="sxs-lookup"><span data-stu-id="60821-278">More details are provided in the details section.</span></span>        |
|<span data-ttu-id="60821-279">動作</span><span class="sxs-lookup"><span data-stu-id="60821-279">action</span></span>     |  <span data-ttu-id="60821-280">對要求採取的動作。</span><span class="sxs-lookup"><span data-stu-id="60821-280">Action taken on the request.</span></span> <span data-ttu-id="60821-281">可用的值為 Blocked 和 Allowed。</span><span class="sxs-lookup"><span data-stu-id="60821-281">Available values are Blocked and Allowed.</span></span>      |
|<span data-ttu-id="60821-282">site</span><span class="sxs-lookup"><span data-stu-id="60821-282">site</span></span>     | <span data-ttu-id="60821-283">將產生此網站的記錄。</span><span class="sxs-lookup"><span data-stu-id="60821-283">Site for which the log was generated.</span></span> <span data-ttu-id="60821-284">目前只列出 Global，因為規則為全域。</span><span class="sxs-lookup"><span data-stu-id="60821-284">Currently, only Global is listed because rules are global.</span></span>|
|<span data-ttu-id="60821-285">詳細資料</span><span class="sxs-lookup"><span data-stu-id="60821-285">details</span></span>     | <span data-ttu-id="60821-286">觸發事件的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="60821-286">Details of the triggering event.</span></span>        |
|<span data-ttu-id="60821-287">details.message</span><span class="sxs-lookup"><span data-stu-id="60821-287">details.message</span></span>     | <span data-ttu-id="60821-288">規則的描述。</span><span class="sxs-lookup"><span data-stu-id="60821-288">Description of the rule.</span></span>        |
|<span data-ttu-id="60821-289">details.data</span><span class="sxs-lookup"><span data-stu-id="60821-289">details.data</span></span>     | <span data-ttu-id="60821-290">在符合規則之要求中找到的特定資料。</span><span class="sxs-lookup"><span data-stu-id="60821-290">Specific data found in request that matched the rule.</span></span>         |
|<span data-ttu-id="60821-291">details.file</span><span class="sxs-lookup"><span data-stu-id="60821-291">details.file</span></span>     | <span data-ttu-id="60821-292">包含規則的組態檔。</span><span class="sxs-lookup"><span data-stu-id="60821-292">Configuration file that contained the rule.</span></span>        |
|<span data-ttu-id="60821-293">details.line</span><span class="sxs-lookup"><span data-stu-id="60821-293">details.line</span></span>     | <span data-ttu-id="60821-294">觸發事件的組態檔中的行號。</span><span class="sxs-lookup"><span data-stu-id="60821-294">Line number in the configuration file that triggered the event.</span></span>       |

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

### <a name="view-and-analyze-the-activity-log"></a><span data-ttu-id="60821-295">檢視和分析活動記錄檔</span><span class="sxs-lookup"><span data-stu-id="60821-295">View and analyze the activity log</span></span>

<span data-ttu-id="60821-296">您可以使用下列任何方法，檢視和分析活動記錄資料：</span><span class="sxs-lookup"><span data-stu-id="60821-296">You can view and analyze activity log data by using any of the following methods:</span></span>

* <span data-ttu-id="60821-297">**Azure 工具**：透過 Azure PowerShell、Azure CLI、Azure REST API 或 Azure 入口網站，從活動記錄擷取資訊。</span><span class="sxs-lookup"><span data-stu-id="60821-297">**Azure tools**: Retrieve information from the activity log through Azure PowerShell, the Azure CLI, the Azure REST API, or the Azure portal.</span></span> <span data-ttu-id="60821-298">[活動作業與 Resource Manager](../azure-resource-manager/resource-group-audit.md) 一文會詳述每個方法的逐步指示。</span><span class="sxs-lookup"><span data-stu-id="60821-298">Step-by-step instructions for each method are detailed in the [Activity operations with Resource Manager](../azure-resource-manager/resource-group-audit.md) article.</span></span>
* <span data-ttu-id="60821-299">**Power BI**：如果還沒有 [Power BI](https://powerbi.microsoft.com/pricing) 帳戶，您可以免費試用。</span><span class="sxs-lookup"><span data-stu-id="60821-299">**Power BI**: If you don't already have a [Power BI](https://powerbi.microsoft.com/pricing) account, you can try it for free.</span></span> <span data-ttu-id="60821-300">使用 [Power BI 的 Azure 活動記錄內容套件](https://powerbi.microsoft.com/en-us/documentation/powerbi-content-pack-azure-audit-logs/)，您可以使用預先設定的儀表板 (可按原樣使用或加以自訂) 來分析資料。</span><span class="sxs-lookup"><span data-stu-id="60821-300">By using the [Azure Activity Logs content pack for Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-content-pack-azure-audit-logs/), you can analyze your data with preconfigured dashboards that you can use as is or customize.</span></span>

### <a name="view-and-analyze-the-access-performance-and-firewall-logs"></a><span data-ttu-id="60821-301">檢視及分析存取、效能和防火牆記錄</span><span class="sxs-lookup"><span data-stu-id="60821-301">View and analyze the access, performance, and firewall logs</span></span>

<span data-ttu-id="60821-302">Azure [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md) 可以從您的 Blob 儲存體帳戶收集計數器和事件記錄檔。</span><span class="sxs-lookup"><span data-stu-id="60821-302">Azure [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md) can collect the counter and event log files from your Blob storage account.</span></span> <span data-ttu-id="60821-303">它也納入了視覺效果和強大的搜尋功能來分析您的記錄。</span><span class="sxs-lookup"><span data-stu-id="60821-303">It includes visualizations and powerful search capabilities to analyze your logs.</span></span>

<span data-ttu-id="60821-304">您也可以連接到儲存體帳戶並擷取存取和效能記錄檔的 JSON 記錄檔項目。</span><span class="sxs-lookup"><span data-stu-id="60821-304">You can also connect to your storage account and retrieve the JSON log entries for access and performance logs.</span></span> <span data-ttu-id="60821-305">下載 JSON 檔案後，可以將它們轉換成 CSV，並在 Excel、PowerBI 或任何其他資料視覺化工具中檢視它們。</span><span class="sxs-lookup"><span data-stu-id="60821-305">After you download the JSON files, you can convert them to CSV and view them in Excel, Power BI, or any other data-visualization tool.</span></span>

> [!TIP]
> <span data-ttu-id="60821-306">如果您熟悉 Visual Studio 以及在 C# 中變更常數和變數值的基本概念，您可以使用 GitHub 所提供的[記錄檔轉換器工具 (英文)](https://github.com/Azure-Samples/networking-dotnet-log-converter)。</span><span class="sxs-lookup"><span data-stu-id="60821-306">If you are familiar with Visual Studio and basic concepts of changing values for constants and variables in C#, you can use the [log converter tools](https://github.com/Azure-Samples/networking-dotnet-log-converter) available from GitHub.</span></span>
> 
> 

## <a name="metrics"></a><span data-ttu-id="60821-307">度量</span><span class="sxs-lookup"><span data-stu-id="60821-307">Metrics</span></span>

<span data-ttu-id="60821-308">計量是某些 Azure 資源的功能，可供您在入口網站中檢視效能計數器。</span><span class="sxs-lookup"><span data-stu-id="60821-308">Metrics are a feature for certain Azure resources where you can view performance counters in the portal.</span></span> <span data-ttu-id="60821-309">目前應用程式閘道只有一個計量。</span><span class="sxs-lookup"><span data-stu-id="60821-309">For Application Gateway, one metric is available now.</span></span> <span data-ttu-id="60821-310">此計量是輸送量，可在入口網站中看到它。</span><span class="sxs-lookup"><span data-stu-id="60821-310">This metric is throughput, and you can see it in the portal.</span></span> <span data-ttu-id="60821-311">瀏覽至應用程式閘道，然後按一下 [計量]。</span><span class="sxs-lookup"><span data-stu-id="60821-311">Browse to an application gateway and click **Metrics**.</span></span> <span data-ttu-id="60821-312">若要檢視這些值，請在 [可用的計量] 區段中選取輸送量。</span><span class="sxs-lookup"><span data-stu-id="60821-312">To view the values, select throughput in the **Available metrics** section.</span></span> <span data-ttu-id="60821-313">您可以在下圖中看到一個範例，內有篩選器可用來顯示不同時間範圍的資料。</span><span class="sxs-lookup"><span data-stu-id="60821-313">In the following image, you can see an example with the filters that you can use to display the data in different time ranges.</span></span>

![計量與篩選器的檢視][5]

<span data-ttu-id="60821-315">若要查看最新的度量清單，請參閱[支援 Azure Monitor 的計量](../monitoring-and-diagnostics/monitoring-supported-metrics.md)。</span><span class="sxs-lookup"><span data-stu-id="60821-315">To see a current list of metrics, see [Supported metrics with Azure Monitor](../monitoring-and-diagnostics/monitoring-supported-metrics.md).</span></span>

### <a name="alert-rules"></a><span data-ttu-id="60821-316">警示規則</span><span class="sxs-lookup"><span data-stu-id="60821-316">Alert rules</span></span>

<span data-ttu-id="60821-317">您可以根據資源的計量來啟動警示規則。</span><span class="sxs-lookup"><span data-stu-id="60821-317">You can start alert rules based on metrics for a resource.</span></span> <span data-ttu-id="60821-318">例如，如果應用程式閘道的輸送量高於、低於或等於臨界值達到一段指定時間，警示便可以呼叫 Webhook 或寄送電子郵件給系統管理員。</span><span class="sxs-lookup"><span data-stu-id="60821-318">For example, an alert can call a webhook or email an administrator if the throughput of the application gateway is above, below, or at a threshold for a specified period.</span></span>

<span data-ttu-id="60821-319">下列範例會逐步引導您建立警示規則，以在輸送量達到臨界值之後傳送電子郵件給系統管理員：</span><span class="sxs-lookup"><span data-stu-id="60821-319">The following example walks you through creating an alert rule that sends an email to an administrator after throughput breaches a threshold:</span></span>

1. <span data-ttu-id="60821-320">按一下 [新增計量警示] 以開啟 [新增規則] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="60821-320">Click **Add metric alert** to open the **Add rule** blade.</span></span> <span data-ttu-id="60821-321">您也可以透過計量刀鋒視窗來到達此刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="60821-321">You can also reach this blade from the metrics blade.</span></span>

   ![新增計量警示按鈕][6]

2. <span data-ttu-id="60821-323">在 [新增規則] 刀鋒視窗中，填入名稱、條件、通知等區段，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="60821-323">On the **Add rule** blade, fill out the name, condition, and notify sections, and click **OK**.</span></span>

   * <span data-ttu-id="60821-324">在 [條件] 選取器中，選取這 4 個值之一：[大於]、[大於或等於]、[小於] 或 [小於或等於]。</span><span class="sxs-lookup"><span data-stu-id="60821-324">In the **Condition** selector, select one of the four values: **Greater than**, **Greater than or equal**, **Less than**, or **Less than or equal to**.</span></span>

   * <span data-ttu-id="60821-325">在 [期間]  選取器可中，選取 5 分鐘到 6 小時的期間。</span><span class="sxs-lookup"><span data-stu-id="60821-325">In the **Period** selector, select a period from 5 minutes to 6 hours.</span></span>

   * <span data-ttu-id="60821-326">如果選取 [傳送電子郵件給擁有者、參與者和讀者]，便可根據可存取該資源的使用者動態傳送電子郵件。</span><span class="sxs-lookup"><span data-stu-id="60821-326">If you select **Email owners, contributors, and readers**, the email can be dynamic based on the users who have access to that resource.</span></span> <span data-ttu-id="60821-327">否則，您可以在 [其他系統管理員電子郵件] 方塊中提供以逗號分隔的使用者清單。</span><span class="sxs-lookup"><span data-stu-id="60821-327">Otherwise, you can provide a comma-separated list of users in the **Additional administrator email(s)** box.</span></span>

   ![新增規則刀鋒視窗][7]

<span data-ttu-id="60821-329">如果達到臨界值，送達的電子郵件會類似下圖︰</span><span class="sxs-lookup"><span data-stu-id="60821-329">If the threshold is breached, an email that's similar to the one in the following image arrives:</span></span>

![違反臨界值的電子郵件][8]

<span data-ttu-id="60821-331">建立計量警示之後，就會出現警示的清單，</span><span class="sxs-lookup"><span data-stu-id="60821-331">A list of alerts appears after you create a metric alert.</span></span> <span data-ttu-id="60821-332">其中提供所有警示規則的概觀。</span><span class="sxs-lookup"><span data-stu-id="60821-332">It provides an overview of all the alert rules.</span></span>

![警示和規則的清單][9]

<span data-ttu-id="60821-334">若要深入了解警示通知，請參閱[接收警示通知](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)。</span><span class="sxs-lookup"><span data-stu-id="60821-334">To learn more about alert notifications, see [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span>

<span data-ttu-id="60821-335">若要深入了解 Webhook 以及其如何與警示搭配使用，請造訪[針對 Azure 計量警示設定 Webhook](../monitoring-and-diagnostics/insights-webhooks-alerts.md)。</span><span class="sxs-lookup"><span data-stu-id="60821-335">To understand more about webhooks and how you can use them with alerts, visit [Configure a webhook on an Azure metric alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="60821-336">後續步驟</span><span class="sxs-lookup"><span data-stu-id="60821-336">Next steps</span></span>

* <span data-ttu-id="60821-337">利用 [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md) 將計數器和事件記錄視覺化。</span><span class="sxs-lookup"><span data-stu-id="60821-337">Visualize counter and event logs by using [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md).</span></span>
* <span data-ttu-id="60821-338">[使用 Power BI 將您的 Azure 活動記錄視覺化](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx)部落格文章。</span><span class="sxs-lookup"><span data-stu-id="60821-338">[Visualize your Azure activity log with Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) blog post.</span></span>
* <span data-ttu-id="60821-339">[在 Power BI 和其他工具中檢視和分析 Azure 活動記錄](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/)部落格文章。</span><span class="sxs-lookup"><span data-stu-id="60821-339">[View and analyze Azure activity logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) blog post.</span></span>

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
