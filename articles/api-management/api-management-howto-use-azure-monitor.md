---
title: "API 管理的 Azure 監視 aaaMonitor |Microsoft 文件"
description: "了解如何 toomonitor Azure API 管理服務使用 Azure 監視器。"
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 2fa193cd-ea71-4b33-a5ca-1f55e5351e23
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 5012d8ed57ea4f94ea6bc1b7c4e1102516ec4414
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-api-management-with-azure-monitor"></a><span data-ttu-id="68170-103">使用 Azure 監視器監視 API 管理</span><span class="sxs-lookup"><span data-stu-id="68170-103">Monitor API Management with Azure Monitor</span></span>
<span data-ttu-id="68170-104">Azure 監視器是一項 Azure 服務，可提供單一來源來讓您監視所有 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="68170-104">Azure Monitor is an Azure service that provides a single source for monitoring all your Azure resources.</span></span> <span data-ttu-id="68170-105">Azure 監視，您可以視覺化方式檢視、 查詢、 路由、 封存，並採取動作上 hello 衡量標準及來自 Azure API 管理等的資源記錄。</span><span class="sxs-lookup"><span data-stu-id="68170-105">With Azure Monitor, you can visualize, query, route, archive, and take actions on hello metrics and logs coming from Azure resources such as API Management.</span></span> 

<span data-ttu-id="68170-106">hello 下列影片示範如何使用 Azure 監視的應用程式開發介面管理 toomonitor。</span><span class="sxs-lookup"><span data-stu-id="68170-106">hello following video shows how toomonitor API Management using Azure Monitor.</span></span> <span data-ttu-id="68170-107">如需 Azure 監視器的詳細資訊，請參閱[開始使用 Azure 監視器]。</span><span class="sxs-lookup"><span data-stu-id="68170-107">For more information about Azure Monitor, see [Get Started with Azure Monitor].</span></span> 


> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Monitor-API-Management-with-Azure-Monitor/player]
>
>
 
## <a name="metrics"></a><span data-ttu-id="68170-108">度量</span><span class="sxs-lookup"><span data-stu-id="68170-108">Metrics</span></span>
<span data-ttu-id="68170-109">API 管理目前發出五個度量，我們計劃 tooadd hello 未來在多個。</span><span class="sxs-lookup"><span data-stu-id="68170-109">API Management currently emits five metrics and we plan tooadd more in hello future.</span></span> <span data-ttu-id="68170-110">這些度量會發出每隔一分鐘，讓您附近 hello 狀態和您的應用程式開發介面的健全狀況的即時可視性。</span><span class="sxs-lookup"><span data-stu-id="68170-110">These metrics are emitted every minute, giving you near real-time visibility into hello state and health of your APIs.</span></span> <span data-ttu-id="68170-111">以下是 hello 度量資訊的摘要：</span><span class="sxs-lookup"><span data-stu-id="68170-111">Following is a summary of hello metrics:</span></span>
* <span data-ttu-id="68170-112">閘道要求總數： hello 期間內要求的應用程式開發介面的 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="68170-112">Total Gateway Requests: hello number of API requests in hello period.</span></span> 
* <span data-ttu-id="68170-113">成功的閘道要求： hello API 的要求數目接收到成功的 HTTP 回應碼，包括 304、 307 和小於 301 (例如，200) 的任何項目。</span><span class="sxs-lookup"><span data-stu-id="68170-113">Successful Gateway Requests: hello number of API requests that received successful HTTP response codes including 304, 307 and anything smaller than 301 (for example, 200).</span></span> 
* <span data-ttu-id="68170-114">失敗的閘道要求： hello API 的要求數目收到錯誤的 HTTP 回應碼，包括 400 和 500 大於任何項目。</span><span class="sxs-lookup"><span data-stu-id="68170-114">Failed Gateway Requests: hello number of API requests that received erroneous HTTP response codes including 400 and anything larger than 500.</span></span>
* <span data-ttu-id="68170-115">未經授權的閘道要求： hello API 的要求數目收到包括 401、 403 和 429 HTTP 回應碼。</span><span class="sxs-lookup"><span data-stu-id="68170-115">Unauthorized Gateway Requests: hello number of API requests that received HTTP response codes including 401, 403, and 429.</span></span> 
* <span data-ttu-id="68170-116">其他閘道要求： hello API 的要求數目收到不屬於 tooany hello 前面類別 (例如，418) 的 HTTP 回應碼。</span><span class="sxs-lookup"><span data-stu-id="68170-116">Other Gateway Requests: hello number of API requests that received HTTP response codes that do not belong tooany of hello preceding categories (for example, 418).</span></span>

<span data-ttu-id="68170-117">您可以在 API 管理服務中存取計量，或在 Azure 監視器中存取所有 Azure 資源的計量。</span><span class="sxs-lookup"><span data-stu-id="68170-117">You can access metrics in your API Management service, or access metrics of all your Azure resources in Azure Monitor.</span></span> <span data-ttu-id="68170-118">在您的 API 管理服務 tooview 度量：</span><span class="sxs-lookup"><span data-stu-id="68170-118">tooview metrics in your API Management service:</span></span>
1. <span data-ttu-id="68170-119">開啟 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="68170-119">Open hello Azure portal.</span></span>
2. <span data-ttu-id="68170-120">移 tooyour API 管理服務。</span><span class="sxs-lookup"><span data-stu-id="68170-120">Go tooyour API Management service.</span></span>
3. <span data-ttu-id="68170-121">按一下 [計量]。</span><span class="sxs-lookup"><span data-stu-id="68170-121">Click **Metrics**.</span></span>

![[計量] 刀鋒視窗][metrics-blade]

<span data-ttu-id="68170-123">如需有關如何 toouse 度量資訊，請參閱[概觀的度量]。</span><span class="sxs-lookup"><span data-stu-id="68170-123">For more information about how toouse Metrics, see [Overview of Metrics].</span></span>

## <a name="activity-logs"></a><span data-ttu-id="68170-124">活動記錄檔</span><span class="sxs-lookup"><span data-stu-id="68170-124">Activity Logs</span></span>
<span data-ttu-id="68170-125">活動記錄檔提供深入了解 API 管理服務執行的 hello 操作。</span><span class="sxs-lookup"><span data-stu-id="68170-125">Activity logs provide insight into hello operations that were performed on your API Management services.</span></span> <span data-ttu-id="68170-126">此記錄以前稱為「稽核記錄」或「作業記錄」。</span><span class="sxs-lookup"><span data-stu-id="68170-126">It was previously known as "audit logs" or "operational logs".</span></span> <span data-ttu-id="68170-127">使用活動記錄檔，您可以決定 hello 」 功能，對象、 及何時"的任何寫入作業 (PUT、 POST、 DELETE) 的 API 管理服務。</span><span class="sxs-lookup"><span data-stu-id="68170-127">Using activity logs, you can determine hello "what, who, and when" for any write operations (PUT, POST, DELETE) taken on your API Management services.</span></span> 

> [!NOTE]
> <span data-ttu-id="68170-128">活動記錄檔不包括讀取 (GET) 作業或執行中作業 hello 傳統發行者入口網站，或使用 hello 原始的管理 Api。</span><span class="sxs-lookup"><span data-stu-id="68170-128">Activity logs do not include read (GET) operations or operations performed in hello classic Publisher Portal or using hello original Management APIs.</span></span>

<span data-ttu-id="68170-129">您可以在 API 管理服務中存取活動記錄，或在 Azure 監視器中存取所有 Azure 資源的記錄。</span><span class="sxs-lookup"><span data-stu-id="68170-129">You can access activity logs in your API Management service, or access logs of all your Azure resources in Azure Monitor.</span></span> <span data-ttu-id="68170-130">tooview 活動記錄在您的 API 管理服務：</span><span class="sxs-lookup"><span data-stu-id="68170-130">tooview activity logs in your API Management service:</span></span>
1. <span data-ttu-id="68170-131">開啟 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="68170-131">Open hello Azure portal.</span></span>
2. <span data-ttu-id="68170-132">移 tooyour API 管理服務。</span><span class="sxs-lookup"><span data-stu-id="68170-132">Go tooyour API Management service.</span></span>
3. <span data-ttu-id="68170-133">按一下 [活動記錄]。</span><span class="sxs-lookup"><span data-stu-id="68170-133">Click **Activity log**.</span></span>

![[活動記錄] 刀鋒視窗][activity-logs-blade]

<span data-ttu-id="68170-135">如需有關如何 toouse 度量資訊，請參閱[活動記錄概觀]。</span><span class="sxs-lookup"><span data-stu-id="68170-135">For more information about how toouse Metrics, see [Overview of Activity Logs].</span></span>

## <a name="alerts"></a><span data-ttu-id="68170-136">Alerts</span><span class="sxs-lookup"><span data-stu-id="68170-136">Alerts</span></span>
<span data-ttu-id="68170-137">您可以設定 tooreceive 根據度量和活動記錄檔的警示。</span><span class="sxs-lookup"><span data-stu-id="68170-137">You can configure tooreceive alerts based on metrics and activity logs.</span></span> <span data-ttu-id="68170-138">Azure 監視器可讓您 tooconfigure 警示 toodo hello，下列情況觸發：</span><span class="sxs-lookup"><span data-stu-id="68170-138">Azure Monitor allows you tooconfigure an alert toodo hello following when it triggers:</span></span>

* <span data-ttu-id="68170-139">傳送電子郵件通知</span><span class="sxs-lookup"><span data-stu-id="68170-139">Send an email notification</span></span>
* <span data-ttu-id="68170-140">呼叫 Webhook</span><span class="sxs-lookup"><span data-stu-id="68170-140">Call a webhook</span></span>
* <span data-ttu-id="68170-141">叫用 Azure 邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="68170-141">Invoke an Azure Logic App</span></span>

<span data-ttu-id="68170-142">您可以在 API 管理服務或 Azure 監視器中設定警示規則。</span><span class="sxs-lookup"><span data-stu-id="68170-142">You can configure alert rules in your API Management service, or in Azure Monitor.</span></span> <span data-ttu-id="68170-143">tooconfigure API 管理中：</span><span class="sxs-lookup"><span data-stu-id="68170-143">tooconfigure them in API Management:</span></span> 
1. <span data-ttu-id="68170-144">開啟 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="68170-144">Open hello Azure portal.</span></span>
2. <span data-ttu-id="68170-145">移 tooyour API 管理服務。</span><span class="sxs-lookup"><span data-stu-id="68170-145">Go tooyour API Management service.</span></span>
3. <span data-ttu-id="68170-146">按一下 [警示規則]。</span><span class="sxs-lookup"><span data-stu-id="68170-146">Click **Alert rules**.</span></span>

![警示規則刀鋒視窗][alert-rules-blade]

<span data-ttu-id="68170-148">如需有關使用警示的詳細資訊，請參閱[警示概觀]。</span><span class="sxs-lookup"><span data-stu-id="68170-148">For more information about using Alerts, see [Overview of Alerts].</span></span>

## <a name="diagnostic-logs"></a><span data-ttu-id="68170-149">診斷記錄檔</span><span class="sxs-lookup"><span data-stu-id="68170-149">Diagnostic Logs</span></span>
<span data-ttu-id="68170-150">診斷記錄可提供豐富的作業與錯誤資訊，這些資訊對於稽核和疑難排解用途來說很重要。</span><span class="sxs-lookup"><span data-stu-id="68170-150">Diagnostic logs provide rich information about operations and errors that are important for auditing as well as troubleshooting purposes.</span></span> <span data-ttu-id="68170-151">診斷記錄與活動記錄不同。</span><span class="sxs-lookup"><span data-stu-id="68170-151">Diagnostics logs differ from activity logs.</span></span> <span data-ttu-id="68170-152">活動記錄檔提供深入了解您的 Azure 資源執行的 hello 操作。</span><span class="sxs-lookup"><span data-stu-id="68170-152">Activity logs provide insights into hello operations that were performed on your Azure resources.</span></span> <span data-ttu-id="68170-153">診斷記錄能讓您了解資源自行執行的作業。</span><span class="sxs-lookup"><span data-stu-id="68170-153">Diagnostics logs provide insight into operations that your resource performed itself.</span></span>

<span data-ttu-id="68170-154">API 管理目前提供診斷與每個項目具有下列結構的 hello 要求個別應用程式開發介面的相關記錄 （每小時批次）：</span><span class="sxs-lookup"><span data-stu-id="68170-154">API Management currently provides diagnostics logs (batched hourly) about individual API request with each entry having hello following structure:</span></span>

```
{
    "Tenant": "",
      "DeploymentName": "",
      "time": "",
      "resourceId": "",
      "category": "GatewayLogs",
      "operationName": "Microsoft.ApiManagement/GatewayLogs",
      "durationMs": ,
      "Level": ,
      "properties": "{
          "ApiId": "",
          "OperationId": "",
          "ProductId": "",
          "SubscriptionId": "",
          "Method": "",
          "Url": "",
          "RequestSize": ,
          "ServiceTime": "",
          "BackendMethod": "",
          "BackendUrl": "",
          "BackendResponseCode": ,
          "ResponseCode": ,
          "ResponseSize": ,
          "Cache": "",
          "UserId"
      }"
 }
```

<span data-ttu-id="68170-155">您可以在 API 管理服務中存取診斷記錄，或在 Azure 監視器中存取所有 Azure 資源的記錄。</span><span class="sxs-lookup"><span data-stu-id="68170-155">You can access diagnostic logs in your API Management service, or access logs of all your Azure resources in Azure Monitor.</span></span> <span data-ttu-id="68170-156">tooview API 管理服務中的診斷記錄：</span><span class="sxs-lookup"><span data-stu-id="68170-156">tooview diagnostic logs in your API Management service:</span></span>
1. <span data-ttu-id="68170-157">開啟 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="68170-157">Open hello Azure portal.</span></span>
2. <span data-ttu-id="68170-158">移 tooyour API 管理服務。</span><span class="sxs-lookup"><span data-stu-id="68170-158">Go tooyour API Management service.</span></span>
3. <span data-ttu-id="68170-159">按一下 [診斷記錄]。</span><span class="sxs-lookup"><span data-stu-id="68170-159">Click **Diagnostic log**.</span></span>

![診斷記錄檔刀鋒視窗][diagnostic-logs-blade]

<span data-ttu-id="68170-161">如需有關如何 toouse 度量資訊，請參閱[診斷記錄概觀]。</span><span class="sxs-lookup"><span data-stu-id="68170-161">For more information about how toouse Metrics, see [Overview of Diagnostic Logs].</span></span>

## <a name="next-step"></a><span data-ttu-id="68170-162">後續步驟</span><span class="sxs-lookup"><span data-stu-id="68170-162">Next Step</span></span>

* <span data-ttu-id="68170-163">[開始使用 Azure 監視器]</span><span class="sxs-lookup"><span data-stu-id="68170-163">[Get Started with Azure Monitor]</span></span>
* <span data-ttu-id="68170-164">[概觀的度量]</span><span class="sxs-lookup"><span data-stu-id="68170-164">[Overview of Metrics]</span></span>
* <span data-ttu-id="68170-165">[活動記錄概觀]</span><span class="sxs-lookup"><span data-stu-id="68170-165">[Overview of Activity Logs]</span></span>
* <span data-ttu-id="68170-166">[診斷記錄概觀]</span><span class="sxs-lookup"><span data-stu-id="68170-166">[Overview of Diagnostic Logs]</span></span>
* <span data-ttu-id="68170-167">[警示概觀]</span><span class="sxs-lookup"><span data-stu-id="68170-167">[Overview of Alerts]</span></span>

[開始使用 Azure 監視器]: ../monitoring-and-diagnostics/monitoring-get-started.md
[概觀的度量]: ../monitoring-and-diagnostics/monitoring-overview-metrics.md
[活動記錄概觀]: ../monitoring-and-diagnostics/monitoring-overview-activity-logs.md
[診斷記錄概觀]: ../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md
[警示概觀]: ../monitoring-and-diagnostics/insights-alerts-portal.md



[metrics-blade]: ./media/api-management-azure-monitor/api-management-metrics-blade.png
[activity-logs-blade]: ./media/api-management-azure-monitor/api-management-activity-logs-blade.png
[alert-rules-blade]: ./media/api-management-azure-monitor/api-management-alert-rules-blade.png
[diagnostic-logs-blade]: ./media/api-management-azure-monitor/api-management-diagnostic-logs-blade.png
