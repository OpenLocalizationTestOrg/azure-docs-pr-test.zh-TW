---
title: "aaaMonitor 作業、 事件與負載平衡器的計數器 |Microsoft 文件"
description: "了解 tooenable 警示的事件，並探查 Azure 負載平衡器的健全狀況狀態記錄"
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
ms.openlocfilehash: ac53c2254e06cad780ad6144c5c30f0085d12576
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-for-azure-load-balancer"></a><span data-ttu-id="9059d-103">Azure 負載平衡器的記錄檔分析</span><span class="sxs-lookup"><span data-stu-id="9059d-103">Log analytics for Azure Load Balancer</span></span>

<span data-ttu-id="9059d-104">您可以在 Azure toomanage 中使用不同類型的記錄檔，並進行疑難排解的負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="9059d-104">You can use different types of logs in Azure toomanage and troubleshoot load balancers.</span></span> <span data-ttu-id="9059d-105">這些記錄檔的某些可以存取透過 hello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="9059d-105">Some of these logs can be accessed through hello portal.</span></span> <span data-ttu-id="9059d-106">從 Azure Blob 儲存體可以擷取所有記錄，並且在不同的工具中進行檢視 (例如 Excel 和 PowerBI)。</span><span class="sxs-lookup"><span data-stu-id="9059d-106">All logs can be extracted from Azure blob storage, and viewed in different tools, such as Excel and PowerBI.</span></span> <span data-ttu-id="9059d-107">您可以深入了解 hello 不同類型的記錄檔從 hello 下方的清單。</span><span class="sxs-lookup"><span data-stu-id="9059d-107">You can learn more about hello different types of logs from hello list below.</span></span>

* <span data-ttu-id="9059d-108">**稽核記錄檔：**您可以使用[Azure 稽核記錄檔](../monitoring-and-diagnostics/insights-debugging-with-events.md)（之前稱為操作記錄檔） tooview 要提交的 tooyour Azure 訂閱，且其狀態的所有作業。</span><span class="sxs-lookup"><span data-stu-id="9059d-108">**Audit logs:** You can use [Azure Audit Logs](../monitoring-and-diagnostics/insights-debugging-with-events.md) (formerly known as Operational Logs) tooview all operations being submitted tooyour Azure subscription(s), and their status.</span></span> <span data-ttu-id="9059d-109">依預設，會啟用稽核記錄檔，並可以在 hello Azure 入口網站中檢視。</span><span class="sxs-lookup"><span data-stu-id="9059d-109">Audit logs are enabled by default, and can be viewed in hello Azure portal.</span></span>
* <span data-ttu-id="9059d-110">**警示事件記錄檔：**您可以使用此記錄 tooview 警示 rasied hello 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="9059d-110">**Alert event logs:** You can use this log tooview alerts rasied by hello load balancer.</span></span> <span data-ttu-id="9059d-111">hello 狀態 hello 負載平衡器會收集每隔五分鐘。</span><span class="sxs-lookup"><span data-stu-id="9059d-111">hello status for hello load balancer is collected every five minutes.</span></span> <span data-ttu-id="9059d-112">只有在引發負載平衡器警示事件時，才會寫入此記錄檔。</span><span class="sxs-lookup"><span data-stu-id="9059d-112">This log is only written if a load balancer alert event is raised.</span></span>
* <span data-ttu-id="9059d-113">**健全狀況探查記錄檔：**您可以使用您的健全狀況探查，例如您的後端集區中沒有接收要求從 hello 負載平衡器健全狀況探查失敗的執行個體的 hello 數目所偵測到此記錄 tooview 問題。</span><span class="sxs-lookup"><span data-stu-id="9059d-113">**Health probe logs:** You can use this log tooview problems detected by your health probe, such as hello number of instances in your backend-pool that are not receiving requests from hello load balancer because of health probe failures.</span></span> <span data-ttu-id="9059d-114">此記錄檔會寫入 toowhen 沒有 hello 健全狀況探查狀態的變更。</span><span class="sxs-lookup"><span data-stu-id="9059d-114">This log is written toowhen there is a change in hello health probe status.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9059d-115">記錄檔分析目前僅適用於網際網路面向的負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="9059d-115">Log analytics currently works only for Internet facing load balancers.</span></span> <span data-ttu-id="9059d-116">記錄檔只可供部署在 hello Resource Manager 部署模型中的資源。</span><span class="sxs-lookup"><span data-stu-id="9059d-116">Logs are only available for resources deployed in hello Resource Manager deployment model.</span></span> <span data-ttu-id="9059d-117">您無法使用記錄檔 hello 傳統部署模型中的資源。</span><span class="sxs-lookup"><span data-stu-id="9059d-117">You cannot use logs for resources in hello classic deployment model.</span></span> <span data-ttu-id="9059d-118">如需 hello 部署模型的詳細資訊，請參閱[了解資源管理員部署和傳統部署](../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="9059d-118">For more information about hello deployment models, see [Understanding Resource Manager deployment and classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>

## <a name="enable-logging"></a><span data-ttu-id="9059d-119">啟用記錄</span><span class="sxs-lookup"><span data-stu-id="9059d-119">Enable logging</span></span>

<span data-ttu-id="9059d-120">每個 Resource Manager 資源都會自動啟用稽核記錄。</span><span class="sxs-lookup"><span data-stu-id="9059d-120">Audit logging is automatically enabled for every Resource Manager resource.</span></span> <span data-ttu-id="9059d-121">您需要 tooenable 事件和健全狀況探查記錄 toostart 收集 hello 資料可透過這些記錄檔。</span><span class="sxs-lookup"><span data-stu-id="9059d-121">You need tooenable event and health probe logging toostart collecting hello data available through those logs.</span></span> <span data-ttu-id="9059d-122">使用下列步驟 tooenable 記錄 hello。</span><span class="sxs-lookup"><span data-stu-id="9059d-122">Use hello following steps tooenable logging.</span></span>

<span data-ttu-id="9059d-123">登入 toohello [Azure 入口網站](http://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="9059d-123">Sign-in toohello [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="9059d-124">如果您還沒有負載平衡器，請先 [建立負載平衡器](load-balancer-get-started-internet-arm-ps.md) 再繼續。</span><span class="sxs-lookup"><span data-stu-id="9059d-124">If you don't already have a load balancer, [create a load balancer](load-balancer-get-started-internet-arm-ps.md) before you continue.</span></span>

1. <span data-ttu-id="9059d-125">在 hello 入口網站中，按一下 **瀏覽**。</span><span class="sxs-lookup"><span data-stu-id="9059d-125">In hello portal, click **Browse**.</span></span>
2. <span data-ttu-id="9059d-126">選取 [負載平衡器]。</span><span class="sxs-lookup"><span data-stu-id="9059d-126">Select **Load Balancers**.</span></span>

    ![入口網站 - 負載平衡器](./media/load-balancer-monitor-log/load-balancer-browse.png)

3. <span data-ttu-id="9059d-128">選取現有的負載平衡器 >> [所有設定]。</span><span class="sxs-lookup"><span data-stu-id="9059d-128">Select an existing load balancer >> **All Settings**.</span></span>
4. <span data-ttu-id="9059d-129">右側 hello hello 對話方塊 hello hello 負載平衡器名稱下，捲動太**監視**，按一下 **診斷**。</span><span class="sxs-lookup"><span data-stu-id="9059d-129">On hello right side of hello dialog under hello name of hello load balancer, scroll too**Monitoring**, click **Diagnostics**.</span></span>

    ![入口網站 - 負載平衡器 - 設定](./media/load-balancer-monitor-log/load-balancer-settings.png)

5. <span data-ttu-id="9059d-131">在 hello**診斷**窗格下**狀態**，選取**上**。</span><span class="sxs-lookup"><span data-stu-id="9059d-131">In hello **Diagnostics** pane, under **Status**, select **On**.</span></span>
6. <span data-ttu-id="9059d-132">按一下 [儲存體帳戶]。</span><span class="sxs-lookup"><span data-stu-id="9059d-132">Click **Storage Account**.</span></span>
7. <span data-ttu-id="9059d-133">在 [記錄] 下方，選取現有的儲存體帳戶或建立一個新的。</span><span class="sxs-lookup"><span data-stu-id="9059d-133">Under **LOGS**, select an existing storage account, or create a new one.</span></span> <span data-ttu-id="9059d-134">使用 hello 滑桿 toodetermine 過去事件資料會儲存在 hello 事件記錄檔的天數。</span><span class="sxs-lookup"><span data-stu-id="9059d-134">Use hello slider toodetermine how many days worth of event data will be stored in hello event logs.</span></span> 
8. <span data-ttu-id="9059d-135">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="9059d-135">Click **Save**.</span></span>

    ![入口網站 - 診斷記錄檔](./media/load-balancer-monitor-log/load-balancer-diagnostics.png)

> [!NOTE]
> <span data-ttu-id="9059d-137">稽核記錄檔不需要個別的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="9059d-137">Audit logs do not require a separate storage account.</span></span> <span data-ttu-id="9059d-138">hello 使用的儲存體事件和健全狀況探查記錄將會產生服務費用。</span><span class="sxs-lookup"><span data-stu-id="9059d-138">hello use of storage for event and health probe logging will incur service charges.</span></span>

## <a name="audit-log"></a><span data-ttu-id="9059d-139">稽核記錄檔</span><span class="sxs-lookup"><span data-stu-id="9059d-139">Audit log</span></span>

<span data-ttu-id="9059d-140">根據預設，會產生 hello 稽核記錄。</span><span class="sxs-lookup"><span data-stu-id="9059d-140">hello audit log is generated by default.</span></span> <span data-ttu-id="9059d-141">hello 記錄檔會保留 90 天，在 Azure 的事件記錄檔存放區中。</span><span class="sxs-lookup"><span data-stu-id="9059d-141">hello logs are preserved for 90 days in Azure's Event Logs store.</span></span> <span data-ttu-id="9059d-142">深入了解這些記錄檔讀取 hello[檢視的事件，並稽核記錄檔](../monitoring-and-diagnostics/insights-debugging-with-events.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="9059d-142">Learn more about these logs by reading hello [View events and audit logs](../monitoring-and-diagnostics/insights-debugging-with-events.md) article.</span></span>

## <a name="alert-event-log"></a><span data-ttu-id="9059d-143">警示事件記錄檔</span><span class="sxs-lookup"><span data-stu-id="9059d-143">Alert event log</span></span>

<span data-ttu-id="9059d-144">您必須對每一個負載平衡器進行啟用，才會產生此記錄檔。</span><span class="sxs-lookup"><span data-stu-id="9059d-144">This log is only generated if you've enabled it on a per load balancer basis.</span></span> <span data-ttu-id="9059d-145">hello 事件記錄以 JSON 格式，儲存在您指定當您啟用 hello 記錄的 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="9059d-145">hello events are logged in JSON format and stored in hello storage account you specified when you enabled hello logging.</span></span> <span data-ttu-id="9059d-146">hello 以下是事件的範例。</span><span class="sxs-lookup"><span data-stu-id="9059d-146">hello following is an example of an event.</span></span>

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

<span data-ttu-id="9059d-147">hello JSON 輸出會顯示 hello *eventname*屬性會描述 hello 負載平衡器的 hello 原因建立警示。</span><span class="sxs-lookup"><span data-stu-id="9059d-147">hello JSON output shows hello *eventname* property which will describe hello reason for hello load balancer created an alert.</span></span> <span data-ttu-id="9059d-148">在此情況下，產生的 hello 警示已到期 tooTCP 連接埠耗盡來源 IP NAT 限制所造成 (SNAT)。</span><span class="sxs-lookup"><span data-stu-id="9059d-148">In this case, hello alert generated was due tooTCP port exhaustion caused by source IP NAT limits (SNAT).</span></span>

## <a name="health-probe-log"></a><span data-ttu-id="9059d-149">健全狀況探查記錄檔</span><span class="sxs-lookup"><span data-stu-id="9059d-149">Health probe log</span></span>

<span data-ttu-id="9059d-150">如果您已如上所述對每一個負載平衡器進行啟用，才會產生此記錄檔。</span><span class="sxs-lookup"><span data-stu-id="9059d-150">This log is only generated if you've enabled it on a per load balancer basis as detailed above.</span></span> <span data-ttu-id="9059d-151">hello 資料會儲存在您指定當您啟用 hello 記錄的 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="9059d-151">hello data is stored in hello storage account you specified when you enabled hello logging.</span></span> <span data-ttu-id="9059d-152">會建立名為 ' insights-記錄檔-loadbalancerprobehealthstatus' 的容器，並會記錄下列資料的 hello:</span><span class="sxs-lookup"><span data-stu-id="9059d-152">A container named 'insights-logs-loadbalancerprobehealthstatus' is created and hello following data is logged:</span></span>

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

<span data-ttu-id="9059d-153">hello JSON 輸出會顯示以 hello 屬性欄位 hello 基本資訊 hello 探查健全狀態。</span><span class="sxs-lookup"><span data-stu-id="9059d-153">hello JSON output shows in hello properties field hello basic information for hello probe health status.</span></span> <span data-ttu-id="9059d-154">hello *dipDownCount*屬性會顯示 hello 後端不接收網路流量，因為 toofailed 探查回應其上的執行個體的 hello 總數。</span><span class="sxs-lookup"><span data-stu-id="9059d-154">hello *dipDownCount* property shows hello total number of instances on hello back-end which are not receiving network traffic due toofailed probe responses.</span></span>

## <a name="view-and-analyze-hello-audit-log"></a><span data-ttu-id="9059d-155">檢視及分析 hello 稽核記錄檔</span><span class="sxs-lookup"><span data-stu-id="9059d-155">View and analyze hello audit log</span></span>

<span data-ttu-id="9059d-156">您可以檢視及分析稽核記錄檔資料，使用任何 hello 下列方法：</span><span class="sxs-lookup"><span data-stu-id="9059d-156">You can view and analyze audit log data using any of hello following methods:</span></span>

* <span data-ttu-id="9059d-157">**Azure 工具：**從 Azure PowerShell，hello Azure 命令列介面 (CLI) (hello Azure REST API，透過 hello 稽核記錄檔中擷取資訊或 hello Azure preview 入口網站。</span><span class="sxs-lookup"><span data-stu-id="9059d-157">**Azure tools:** Retrieve information from hello audit logs through Azure PowerShell, hello Azure Command Line Interface (CLI), hello Azure REST API, or hello Azure preview portal.</span></span> <span data-ttu-id="9059d-158">每個方法的逐步指示的詳細 hello[稽核與資源管理員作業](../azure-resource-manager/resource-group-audit.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="9059d-158">Step-by-step instructions for each method are detailed in hello [Audit operations with Resource Manager](../azure-resource-manager/resource-group-audit.md) article.</span></span>
* <span data-ttu-id="9059d-159">**Power BI︰**如果您還沒有 [Power BI](https://powerbi.microsoft.com/pricing) 帳戶，您可以免費試用。</span><span class="sxs-lookup"><span data-stu-id="9059d-159">**Power BI:** If you do not already have a [Power BI](https://powerbi.microsoft.com/pricing) account, you can try it for free.</span></span> <span data-ttu-id="9059d-160">使用 hello [Power BI 的 Azure 稽核記錄內容套件](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs)、 您可以分析資料與預先設定的儀表板，或您可以自訂檢視 toosuit 您的需求。</span><span class="sxs-lookup"><span data-stu-id="9059d-160">Using hello [Azure Audit Logs content pack for Power BI](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs), you can analyze your data with pre-configured dashboards, or you can customize views toosuit your requirements.</span></span>

## <a name="view-and-analyze-hello-health-probe-and-event-log"></a><span data-ttu-id="9059d-161">檢視及分析 hello 健全狀況探查和事件記錄檔</span><span class="sxs-lookup"><span data-stu-id="9059d-161">View and analyze hello health probe and event log</span></span>

<span data-ttu-id="9059d-162">您需要 tooconnect tooyour 儲存體帳戶，並擷取事件和健全狀況探查記錄檔的 hello JSON 記錄項目。</span><span class="sxs-lookup"><span data-stu-id="9059d-162">You need tooconnect tooyour storage account and retrieve hello JSON log entries for event and health probe logs.</span></span> <span data-ttu-id="9059d-163">一旦您下載 hello JSON 檔案，您可以將它們轉換 tooCSV 和 Excel、 power Bi 或任何其他資料視覺效果工具中的檢視。</span><span class="sxs-lookup"><span data-stu-id="9059d-163">Once you download hello JSON files, you can convert them tooCSV and view in Excel, PowerBI, or any other data visualization tool.</span></span>

> [!TIP]
> <span data-ttu-id="9059d-164">如果您熟悉 Visual Studio 和變更值的常數和變數在 C# 中的基本概念，您可以使用 hello[記錄轉換器工具](https://github.com/Azure-Samples/networking-dotnet-log-converter)可從 GitHub 取得。</span><span class="sxs-lookup"><span data-stu-id="9059d-164">If you are familiar with Visual Studio and basic concepts of changing values for constants and variables in C#, you can use hello [log converter tools](https://github.com/Azure-Samples/networking-dotnet-log-converter) available from GitHub.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9059d-165">其他資源</span><span class="sxs-lookup"><span data-stu-id="9059d-165">Additional resources</span></span>

* <span data-ttu-id="9059d-166">[使用 Power BI 視覺化您的 Azure 稽核記錄檔](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) 部落格文章。</span><span class="sxs-lookup"><span data-stu-id="9059d-166">[Visualize your Azure Audit Logs with Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) blog post.</span></span>
* <span data-ttu-id="9059d-167">[在 Power BI 和其他工具中檢視和分析 Azure 稽核記錄](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) 部落格文章。</span><span class="sxs-lookup"><span data-stu-id="9059d-167">[View and analyze Azure Audit Logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) blog post.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9059d-168">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9059d-168">Next steps</span></span>

[<span data-ttu-id="9059d-169">了解負載平衡器偵查</span><span class="sxs-lookup"><span data-stu-id="9059d-169">Understand load balancer probes</span></span>](load-balancer-custom-probe-overview.md)
