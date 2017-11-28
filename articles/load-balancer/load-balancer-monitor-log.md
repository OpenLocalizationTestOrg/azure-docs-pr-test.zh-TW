---
title: "監視負載平衡器的作業、事件和計數器 | Microsoft Docs"
description: "了解如何啟用 Azure 負載平衡器的警示事件和探查健全狀況狀態記錄"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: 56656d74-0241-4096-88c8-aa88515d676d
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 638ecd5e02889bd8cb6e7429dfcec335feaac4a3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="log-analytics-for-azure-load-balancer"></a><span data-ttu-id="a68d3-103">Azure 負載平衡器的記錄檔分析</span><span class="sxs-lookup"><span data-stu-id="a68d3-103">Log analytics for Azure Load Balancer</span></span>

<span data-ttu-id="a68d3-104">您可以在 Azure 中使用不同類型的記錄檔來管理和疑難排解負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="a68d3-104">You can use different types of logs in Azure to manage and troubleshoot load balancers.</span></span> <span data-ttu-id="a68d3-105">透過入口網站可以存取其中一些記錄檔。</span><span class="sxs-lookup"><span data-stu-id="a68d3-105">Some of these logs can be accessed through the portal.</span></span> <span data-ttu-id="a68d3-106">從 Azure Blob 儲存體可以擷取所有記錄，並且在不同的工具中進行檢視 (例如 Excel 和 PowerBI)。</span><span class="sxs-lookup"><span data-stu-id="a68d3-106">All logs can be extracted from Azure blob storage, and viewed in different tools, such as Excel and PowerBI.</span></span> <span data-ttu-id="a68d3-107">您可以從下列清單進一步了解不同類型的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="a68d3-107">You can learn more about the different types of logs from the list below.</span></span>

* <span data-ttu-id="a68d3-108">**稽核記錄檔︰**您可以使用 [Azure 稽核記錄檔](../monitoring-and-diagnostics/insights-debugging-with-events.md) (之前稱為「作業記錄檔」) 來檢視提交至您 Azure 訂用帳戶的所有作業及其狀態。</span><span class="sxs-lookup"><span data-stu-id="a68d3-108">**Audit logs:** You can use [Azure Audit Logs](../monitoring-and-diagnostics/insights-debugging-with-events.md) (formerly known as Operational Logs) to view all operations being submitted to your Azure subscription(s), and their status.</span></span> <span data-ttu-id="a68d3-109">預設會啟用稽核記錄檔，並可在 Azure 入口網站中進行檢視。</span><span class="sxs-lookup"><span data-stu-id="a68d3-109">Audit logs are enabled by default, and can be viewed in the Azure portal.</span></span>
* <span data-ttu-id="a68d3-110">**警示事件記錄：**您可以使用此記錄來檢視負載平衡器所引發的警示。</span><span class="sxs-lookup"><span data-stu-id="a68d3-110">**Alert event logs:** You can use this log to view alerts rasied by the load balancer.</span></span> <span data-ttu-id="a68d3-111">系統每五分鐘會收集一次負載平衡器的狀態。</span><span class="sxs-lookup"><span data-stu-id="a68d3-111">The status for the load balancer is collected every five minutes.</span></span> <span data-ttu-id="a68d3-112">只有在引發負載平衡器警示事件時，才會寫入此記錄檔。</span><span class="sxs-lookup"><span data-stu-id="a68d3-112">This log is only written if a load balancer alert event is raised.</span></span>
* <span data-ttu-id="a68d3-113">**健康狀態探查記錄︰**您可以使用此記錄來檢視健康狀態探查所偵測到的問題，例如後端集區中因為健康狀態探查失敗而未從負載平衡器接收要求的執行個體數目。</span><span class="sxs-lookup"><span data-stu-id="a68d3-113">**Health probe logs:** You can use this log to view problems detected by your health probe, such as the number of instances in your backend-pool that are not receiving requests from the load balancer because of health probe failures.</span></span> <span data-ttu-id="a68d3-114">健康狀態探查狀態發生變更時會寫入此記錄。</span><span class="sxs-lookup"><span data-stu-id="a68d3-114">This log is written to when there is a change in the health probe status.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a68d3-115">記錄檔分析目前僅適用於網際網路面向的負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="a68d3-115">Log analytics currently works only for Internet facing load balancers.</span></span> <span data-ttu-id="a68d3-116">記錄檔僅適用於在資源管理員部署模型中部署的資源。</span><span class="sxs-lookup"><span data-stu-id="a68d3-116">Logs are only available for resources deployed in the Resource Manager deployment model.</span></span> <span data-ttu-id="a68d3-117">您無法將記錄檔使用於傳統部署模型中的資源。</span><span class="sxs-lookup"><span data-stu-id="a68d3-117">You cannot use logs for resources in the classic deployment model.</span></span> <span data-ttu-id="a68d3-118">如需這些部署模型的詳細資訊，請參閱[了解 Resource Manager 部署和傳統部署](../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="a68d3-118">For more information about the deployment models, see [Understanding Resource Manager deployment and classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>

## <a name="enable-logging"></a><span data-ttu-id="a68d3-119">啟用記錄</span><span class="sxs-lookup"><span data-stu-id="a68d3-119">Enable logging</span></span>

<span data-ttu-id="a68d3-120">每個 Resource Manager 資源都會自動啟用稽核記錄。</span><span class="sxs-lookup"><span data-stu-id="a68d3-120">Audit logging is automatically enabled for every Resource Manager resource.</span></span> <span data-ttu-id="a68d3-121">您需要啟用事件和健全狀況探查記錄，才能開始收集可透過這些記錄檔取得的資料。</span><span class="sxs-lookup"><span data-stu-id="a68d3-121">You need to enable event and health probe logging to start collecting the data available through those logs.</span></span> <span data-ttu-id="a68d3-122">使用下列步驟以啟用記錄功能。</span><span class="sxs-lookup"><span data-stu-id="a68d3-122">Use the following steps to enable logging.</span></span>

<span data-ttu-id="a68d3-123">登入 [Azure 入口網站](http://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="a68d3-123">Sign-in to the [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="a68d3-124">如果您還沒有負載平衡器，請先 [建立負載平衡器](load-balancer-get-started-internet-arm-ps.md) 再繼續。</span><span class="sxs-lookup"><span data-stu-id="a68d3-124">If you don't already have a load balancer, [create a load balancer](load-balancer-get-started-internet-arm-ps.md) before you continue.</span></span>

1. <span data-ttu-id="a68d3-125">在入口網站中，按一下 [瀏覽]。</span><span class="sxs-lookup"><span data-stu-id="a68d3-125">In the portal, click **Browse**.</span></span>
2. <span data-ttu-id="a68d3-126">選取 [負載平衡器]。</span><span class="sxs-lookup"><span data-stu-id="a68d3-126">Select **Load Balancers**.</span></span>

    ![入口網站 - 負載平衡器](./media/load-balancer-monitor-log/load-balancer-browse.png)

3. <span data-ttu-id="a68d3-128">選取現有的負載平衡器 >> [所有設定]。</span><span class="sxs-lookup"><span data-stu-id="a68d3-128">Select an existing load balancer >> **All Settings**.</span></span>
4. <span data-ttu-id="a68d3-129">在對話方塊的右側，於負載平衡器的名稱下方，捲動至 [監視]，按一下 [診斷]。</span><span class="sxs-lookup"><span data-stu-id="a68d3-129">On the right side of the dialog under the name of the load balancer, scroll to **Monitoring**, click **Diagnostics**.</span></span>

    ![入口網站 - 負載平衡器 - 設定](./media/load-balancer-monitor-log/load-balancer-settings.png)

5. <span data-ttu-id="a68d3-131">在 [診斷] 窗格中，在 [狀態] 下方，選取 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="a68d3-131">In the **Diagnostics** pane, under **Status**, select **On**.</span></span>
6. <span data-ttu-id="a68d3-132">按一下 [儲存體帳戶]。</span><span class="sxs-lookup"><span data-stu-id="a68d3-132">Click **Storage Account**.</span></span>
7. <span data-ttu-id="a68d3-133">在 [記錄] 下方，選取現有的儲存體帳戶或建立一個新的。</span><span class="sxs-lookup"><span data-stu-id="a68d3-133">Under **LOGS**, select an existing storage account, or create a new one.</span></span> <span data-ttu-id="a68d3-134">使用滑桿來決定值得在事件記錄中儲存多少天的事件資料。</span><span class="sxs-lookup"><span data-stu-id="a68d3-134">Use the slider to determine how many days worth of event data will be stored in the event logs.</span></span> 
8. <span data-ttu-id="a68d3-135">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="a68d3-135">Click **Save**.</span></span>

    ![入口網站 - 診斷記錄檔](./media/load-balancer-monitor-log/load-balancer-diagnostics.png)

> [!NOTE]
> <span data-ttu-id="a68d3-137">稽核記錄檔不需要個別的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="a68d3-137">Audit logs do not require a separate storage account.</span></span> <span data-ttu-id="a68d3-138">將儲存體用於事件和健全狀況探查記錄將會產生服務費用。</span><span class="sxs-lookup"><span data-stu-id="a68d3-138">The use of storage for event and health probe logging will incur service charges.</span></span>

## <a name="audit-log"></a><span data-ttu-id="a68d3-139">稽核記錄檔</span><span class="sxs-lookup"><span data-stu-id="a68d3-139">Audit log</span></span>

<span data-ttu-id="a68d3-140">預設會產生稽核記錄檔。</span><span class="sxs-lookup"><span data-stu-id="a68d3-140">The audit log is generated by default.</span></span> <span data-ttu-id="a68d3-141">記錄檔會在 Azure 的 [事件記錄檔] 存放區中保留 90 天。</span><span class="sxs-lookup"><span data-stu-id="a68d3-141">The logs are preserved for 90 days in Azure's Event Logs store.</span></span> <span data-ttu-id="a68d3-142">閱讀 [檢視事件和稽核記錄檔](../monitoring-and-diagnostics/insights-debugging-with-events.md) 一文，進一步了解這些記錄檔。</span><span class="sxs-lookup"><span data-stu-id="a68d3-142">Learn more about these logs by reading the [View events and audit logs](../monitoring-and-diagnostics/insights-debugging-with-events.md) article.</span></span>

## <a name="alert-event-log"></a><span data-ttu-id="a68d3-143">警示事件記錄檔</span><span class="sxs-lookup"><span data-stu-id="a68d3-143">Alert event log</span></span>

<span data-ttu-id="a68d3-144">您必須對每一個負載平衡器進行啟用，才會產生此記錄檔。</span><span class="sxs-lookup"><span data-stu-id="a68d3-144">This log is only generated if you've enabled it on a per load balancer basis.</span></span> <span data-ttu-id="a68d3-145">事件會以 JSON 格式記錄，並儲存在您啟用記錄時所指定的儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="a68d3-145">The events are logged in JSON format and stored in the storage account you specified when you enabled the logging.</span></span> <span data-ttu-id="a68d3-146">以下是事件的範例。</span><span class="sxs-lookup"><span data-stu-id="a68d3-146">The following is an example of an event.</span></span>

```json
{
    "time": "2016-01-26T10:37:46.6024215Z",
    "systemId": "32077926-b9c4-42fb-94c1-762e528b5b27",
    "category": "LoadBalancerAlertEvent",
    "resourceId": "/SUBSCRIPTIONS/XXXXXXXXXXXXXXXXX-XXXX-XXXX-XXXXXXXXX/RESOURCEGROUPS/RG7/PROVIDERS/MICROSOFT.NETWORK/LOADBALANCERS/WWEBLB",
    "operationName": "LoadBalancerProbeHealthStatus",
    "properties": {
        "eventName": "Resource Limits Hit",
        "eventDescription": "Ports exhausted",
        "eventProperties": {
            "public ip address": "40.117.227.32"
        }
    }
}
```

<span data-ttu-id="a68d3-147">JSON 輸出中會顯示 *eventname* 屬性，此屬性會描述負載平衡器建立警示的原因。</span><span class="sxs-lookup"><span data-stu-id="a68d3-147">The JSON output shows the *eventname* property which will describe the reason for the load balancer created an alert.</span></span> <span data-ttu-id="a68d3-148">在此案例中，來源 IP NAT (SNAT) 限制導致了 TCP 連接埠耗盡，因此產生此警示。</span><span class="sxs-lookup"><span data-stu-id="a68d3-148">In this case, the alert generated was due to TCP port exhaustion caused by source IP NAT limits (SNAT).</span></span>

## <a name="health-probe-log"></a><span data-ttu-id="a68d3-149">健全狀況探查記錄檔</span><span class="sxs-lookup"><span data-stu-id="a68d3-149">Health probe log</span></span>

<span data-ttu-id="a68d3-150">如果您已如上所述對每一個負載平衡器進行啟用，才會產生此記錄檔。</span><span class="sxs-lookup"><span data-stu-id="a68d3-150">This log is only generated if you've enabled it on a per load balancer basis as detailed above.</span></span> <span data-ttu-id="a68d3-151">資料會儲存在您啟用記錄時所指定的儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="a68d3-151">The data is stored in the storage account you specified when you enabled the logging.</span></span> <span data-ttu-id="a68d3-152">系統會建立名為 'insights-logs-loadbalancerprobehealthstatus' 的容器，並記錄下列資料：</span><span class="sxs-lookup"><span data-stu-id="a68d3-152">A container named 'insights-logs-loadbalancerprobehealthstatus' is created and the following data is logged:</span></span>

```json
{
    "records":[
    {
        "time": "2016-01-26T10:37:46.6024215Z",
        "systemId": "32077926-b9c4-42fb-94c1-762e528b5b27",
        "category": "LoadBalancerProbeHealthStatus",
        "resourceId": "/SUBSCRIPTIONS/XXXXXXXXXXXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXX/RESOURCEGROUPS/RG7/PROVIDERS/MICROSOFT.NETWORK/LOADBALANCERS/WWEBLB",
        "operationName": "LoadBalancerProbeHealthStatus",
        "properties": {
            "publicIpAddress": "40.83.190.158",
            "port": "81",
            "totalDipCount": 2,
            "dipDownCount": 1,
            "healthPercentage": 50.000000
        }
    },
    {
        "time": "2016-01-26T10:37:46.6024215Z",
        "systemId": "32077926-b9c4-42fb-94c1-762e528b5b27",
        "category": "LoadBalancerProbeHealthStatus",
        "resourceId": "/SUBSCRIPTIONS/XXXXXXXXXXXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXX/RESOURCEGROUPS/RG7/PROVIDERS/MICROSOFT.NETWORK/LOADBALANCERS/WWEBLB",
        "operationName": "LoadBalancerProbeHealthStatus",
        "properties": {
            "publicIpAddress": "40.83.190.158",
            "port": "81",
            "totalDipCount": 2,
            "dipDownCount": 0,
            "healthPercentage": 100.000000
        }
    }]
}
```

<span data-ttu-id="a68d3-153">JSON 輸出在屬性欄位中顯示了探查健全狀況狀態的基本資訊。</span><span class="sxs-lookup"><span data-stu-id="a68d3-153">The JSON output shows in the properties field the basic information for the probe health status.</span></span> <span data-ttu-id="a68d3-154">*dipDownCount* 屬性會顯示後端上因為探查回應失敗而不會接收網路流量的執行個體總數。</span><span class="sxs-lookup"><span data-stu-id="a68d3-154">The *dipDownCount* property shows the total number of instances on the back-end which are not receiving network traffic due to failed probe responses.</span></span>

## <a name="view-and-analyze-the-audit-log"></a><span data-ttu-id="a68d3-155">檢視和分析稽核記錄檔</span><span class="sxs-lookup"><span data-stu-id="a68d3-155">View and analyze the audit log</span></span>

<span data-ttu-id="a68d3-156">您可以使用下列任何方法，檢視和分析稽核記錄檔資料：</span><span class="sxs-lookup"><span data-stu-id="a68d3-156">You can view and analyze audit log data using any of the following methods:</span></span>

* <span data-ttu-id="a68d3-157">**Azure 工具︰** 透過 Azure PowerShell、Azure 命令列介面 (CLI)、Azure REST API 或 Azure Preview 入口網站，從稽核記錄擷取資訊。</span><span class="sxs-lookup"><span data-stu-id="a68d3-157">**Azure tools:** Retrieve information from the audit logs through Azure PowerShell, the Azure Command Line Interface (CLI), the Azure REST API, or the Azure preview portal.</span></span> <span data-ttu-id="a68d3-158">[稽核作業與資源管理員](../azure-resource-manager/resource-group-audit.md) 一文會詳述每個方法的逐步指示。</span><span class="sxs-lookup"><span data-stu-id="a68d3-158">Step-by-step instructions for each method are detailed in the [Audit operations with Resource Manager](../azure-resource-manager/resource-group-audit.md) article.</span></span>
* <span data-ttu-id="a68d3-159">**Power BI︰**如果您還沒有 [Power BI](https://powerbi.microsoft.com/pricing) 帳戶，您可以免費試用。</span><span class="sxs-lookup"><span data-stu-id="a68d3-159">**Power BI:** If you do not already have a [Power BI](https://powerbi.microsoft.com/pricing) account, you can try it for free.</span></span> <span data-ttu-id="a68d3-160">使用 [Power BI 的 Azure 稽核記錄檔內容套件](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs)，您可以使用預先設定的儀表板來分析資料，或根據您的需求自訂檢視。</span><span class="sxs-lookup"><span data-stu-id="a68d3-160">Using the [Azure Audit Logs content pack for Power BI](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs), you can analyze your data with pre-configured dashboards, or you can customize views to suit your requirements.</span></span>

## <a name="view-and-analyze-the-health-probe-and-event-log"></a><span data-ttu-id="a68d3-161">檢視和分析健全狀況探查與事件記錄檔</span><span class="sxs-lookup"><span data-stu-id="a68d3-161">View and analyze the health probe and event log</span></span>

<span data-ttu-id="a68d3-162">您需要連接到儲存體帳戶並擷取事件和健全狀況探查記錄檔的 JSON 記錄項目。</span><span class="sxs-lookup"><span data-stu-id="a68d3-162">You need to connect to your storage account and retrieve the JSON log entries for event and health probe logs.</span></span> <span data-ttu-id="a68d3-163">下載 JSON 檔案後，您可以將它們轉換成 CSV 並在 Excel、PowerBI 或任何其他資料視覺化工具中檢視。</span><span class="sxs-lookup"><span data-stu-id="a68d3-163">Once you download the JSON files, you can convert them to CSV and view in Excel, PowerBI, or any other data visualization tool.</span></span>

> [!TIP]
> <span data-ttu-id="a68d3-164">如果您熟悉 Visual Studio 以及在 C# 中變更常數和變數值的基本概念，您可以使用 GitHub 所提供的[記錄檔轉換器工具 (英文)](https://github.com/Azure-Samples/networking-dotnet-log-converter)。</span><span class="sxs-lookup"><span data-stu-id="a68d3-164">If you are familiar with Visual Studio and basic concepts of changing values for constants and variables in C#, you can use the [log converter tools](https://github.com/Azure-Samples/networking-dotnet-log-converter) available from GitHub.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a68d3-165">其他資源</span><span class="sxs-lookup"><span data-stu-id="a68d3-165">Additional resources</span></span>

* <span data-ttu-id="a68d3-166">[使用 Power BI 視覺化您的 Azure 稽核記錄檔](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) 部落格文章。</span><span class="sxs-lookup"><span data-stu-id="a68d3-166">[Visualize your Azure Audit Logs with Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) blog post.</span></span>
* <span data-ttu-id="a68d3-167">[在 Power BI 和其他工具中檢視和分析 Azure 稽核記錄](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) 部落格文章。</span><span class="sxs-lookup"><span data-stu-id="a68d3-167">[View and analyze Azure Audit Logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) blog post.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a68d3-168">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a68d3-168">Next steps</span></span>

[<span data-ttu-id="a68d3-169">了解負載平衡器偵查</span><span class="sxs-lookup"><span data-stu-id="a68d3-169">Understand load balancer probes</span></span>](load-balancer-custom-probe-overview.md)
