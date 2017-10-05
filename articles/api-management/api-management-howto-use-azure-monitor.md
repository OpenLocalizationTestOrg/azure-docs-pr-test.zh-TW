---
title: "使用 Azure 監視器來監視 API 管理 | Microsoft Docs"
description: "了解如何使用 Azure 監視器來監視 Azure API 管理服務。"
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
ms.openlocfilehash: 0f64947755c79739bb6f15325929bd074cfd7210
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-api-management-with-azure-monitor"></a><span data-ttu-id="b1adb-103">使用 Azure 監視器監視 API 管理</span><span class="sxs-lookup"><span data-stu-id="b1adb-103">Monitor API Management with Azure Monitor</span></span>
<span data-ttu-id="b1adb-104">Azure 監視器是一項 Azure 服務，可提供單一來源來讓您監視所有 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="b1adb-104">Azure Monitor is an Azure service that provides a single source for monitoring all your Azure resources.</span></span> <span data-ttu-id="b1adb-105">您可以使用 Azure 監視器來視覺化、查詢、路由、封存及針對來自 Azure 資源 (例如 API 管理) 的計量和記錄採取行動。</span><span class="sxs-lookup"><span data-stu-id="b1adb-105">With Azure Monitor, you can visualize, query, route, archive, and take actions on the metrics and logs coming from Azure resources such as API Management.</span></span> 

<span data-ttu-id="b1adb-106">下列影片示範如何使用 Azure 監視器來監視 API 管理。</span><span class="sxs-lookup"><span data-stu-id="b1adb-106">The following video shows how to monitor API Management using Azure Monitor.</span></span> <span data-ttu-id="b1adb-107">如需 Azure 監視器的詳細資訊，請參閱[開始使用 Azure 監視器]。</span><span class="sxs-lookup"><span data-stu-id="b1adb-107">For more information about Azure Monitor, see [Get Started with Azure Monitor].</span></span> 


> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Monitor-API-Management-with-Azure-Monitor/player]
>
>
 
## <a name="metrics"></a><span data-ttu-id="b1adb-108">度量</span><span class="sxs-lookup"><span data-stu-id="b1adb-108">Metrics</span></span>
<span data-ttu-id="b1adb-109">API 管理目前可發出五個計量，未來預計會新增更多計量。</span><span class="sxs-lookup"><span data-stu-id="b1adb-109">API Management currently emits five metrics and we plan to add more in the future.</span></span> <span data-ttu-id="b1adb-110">這些計量會每分鐘發出一次，讓您近乎即時地了解 API 的狀態和健全狀況。</span><span class="sxs-lookup"><span data-stu-id="b1adb-110">These metrics are emitted every minute, giving you near real-time visibility into the state and health of your APIs.</span></span> <span data-ttu-id="b1adb-111">以下是計量的摘要：</span><span class="sxs-lookup"><span data-stu-id="b1adb-111">Following is a summary of the metrics:</span></span>
* <span data-ttu-id="b1adb-112">閘道要求總數︰該期間內的 API 要求數目。</span><span class="sxs-lookup"><span data-stu-id="b1adb-112">Total Gateway Requests: the number of API requests in the period.</span></span> 
* <span data-ttu-id="b1adb-113">成功的閘道要求︰收到 HTTP 成功回應碼的 API 要求數目，這些回應碼包括 304、307 和任何小於 301 的代碼 (例如 200)。</span><span class="sxs-lookup"><span data-stu-id="b1adb-113">Successful Gateway Requests: the number of API requests that received successful HTTP response codes including 304, 307 and anything smaller than 301 (for example, 200).</span></span> 
* <span data-ttu-id="b1adb-114">失敗的閘道要求︰收到 HTTP 錯誤回應碼的 API 要求數目，這些回應碼包括 400 和任何大於 500 的代碼。</span><span class="sxs-lookup"><span data-stu-id="b1adb-114">Failed Gateway Requests: the number of API requests that received erroneous HTTP response codes including 400 and anything larger than 500.</span></span>
* <span data-ttu-id="b1adb-115">未經授權閘道器要求︰收到 401、403 和 429 HTTP 回應碼的 API 要求數目。</span><span class="sxs-lookup"><span data-stu-id="b1adb-115">Unauthorized Gateway Requests: the number of API requests that received HTTP response codes including 401, 403, and 429.</span></span> 
* <span data-ttu-id="b1adb-116">其他閘道要求︰所收到的 HTTP 回應碼不屬於上述任何類別 (例如 418) 的 API 要求數目。</span><span class="sxs-lookup"><span data-stu-id="b1adb-116">Other Gateway Requests: the number of API requests that received HTTP response codes that do not belong to any of the preceding categories (for example, 418).</span></span>

<span data-ttu-id="b1adb-117">您可以在 API 管理服務中存取計量，或在 Azure 監視器中存取所有 Azure 資源的計量。</span><span class="sxs-lookup"><span data-stu-id="b1adb-117">You can access metrics in your API Management service, or access metrics of all your Azure resources in Azure Monitor.</span></span> <span data-ttu-id="b1adb-118">若要在 API 管理服務中檢視計量︰</span><span class="sxs-lookup"><span data-stu-id="b1adb-118">To view metrics in your API Management service:</span></span>
1. <span data-ttu-id="b1adb-119">開啟 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="b1adb-119">Open the Azure portal.</span></span>
2. <span data-ttu-id="b1adb-120">移至 API 管理服務。</span><span class="sxs-lookup"><span data-stu-id="b1adb-120">Go to your API Management service.</span></span>
3. <span data-ttu-id="b1adb-121">按一下 [計量]。</span><span class="sxs-lookup"><span data-stu-id="b1adb-121">Click **Metrics**.</span></span>

![[計量] 刀鋒視窗][metrics-blade]

<span data-ttu-id="b1adb-123">如需如何使用計量的詳細資訊，請參閱[計量概觀]。</span><span class="sxs-lookup"><span data-stu-id="b1adb-123">For more information about how to use Metrics, see [Overview of Metrics].</span></span>

## <a name="activity-logs"></a><span data-ttu-id="b1adb-124">活動記錄檔</span><span class="sxs-lookup"><span data-stu-id="b1adb-124">Activity Logs</span></span>
<span data-ttu-id="b1adb-125">活動記錄可讓您深入了解 API 管理服務上所執行的作業。</span><span class="sxs-lookup"><span data-stu-id="b1adb-125">Activity logs provide insight into the operations that were performed on your API Management services.</span></span> <span data-ttu-id="b1adb-126">此記錄以前稱為「稽核記錄」或「作業記錄」。</span><span class="sxs-lookup"><span data-stu-id="b1adb-126">It was previously known as "audit logs" or "operational logs".</span></span> <span data-ttu-id="b1adb-127">您可以使用活動記錄來判斷 API 管理服務上所執行之任何寫入作業 (PUT、POST、DELETE) 的「內容、對象和時間」。</span><span class="sxs-lookup"><span data-stu-id="b1adb-127">Using activity logs, you can determine the "what, who, and when" for any write operations (PUT, POST, DELETE) taken on your API Management services.</span></span> 

> [!NOTE]
> <span data-ttu-id="b1adb-128">活動記錄不會納入讀取 (GET) 作業，也不會納入透過傳統發行者入口網站或原始管理 API 所執行的作業。</span><span class="sxs-lookup"><span data-stu-id="b1adb-128">Activity logs do not include read (GET) operations or operations performed in the classic Publisher Portal or using the original Management APIs.</span></span>

<span data-ttu-id="b1adb-129">您可以在 API 管理服務中存取活動記錄，或在 Azure 監視器中存取所有 Azure 資源的記錄。</span><span class="sxs-lookup"><span data-stu-id="b1adb-129">You can access activity logs in your API Management service, or access logs of all your Azure resources in Azure Monitor.</span></span> <span data-ttu-id="b1adb-130">若要在 API 管理服務中檢視活動記錄︰</span><span class="sxs-lookup"><span data-stu-id="b1adb-130">To view activity logs in your API Management service:</span></span>
1. <span data-ttu-id="b1adb-131">開啟 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="b1adb-131">Open the Azure portal.</span></span>
2. <span data-ttu-id="b1adb-132">移至 API 管理服務。</span><span class="sxs-lookup"><span data-stu-id="b1adb-132">Go to your API Management service.</span></span>
3. <span data-ttu-id="b1adb-133">按一下 [活動記錄]。</span><span class="sxs-lookup"><span data-stu-id="b1adb-133">Click **Activity log**.</span></span>

![[活動記錄] 刀鋒視窗][activity-logs-blade]

<span data-ttu-id="b1adb-135">如需如何使用計量的詳細資訊，請參閱[活動記錄概觀]。</span><span class="sxs-lookup"><span data-stu-id="b1adb-135">For more information about how to use Metrics, see [Overview of Activity Logs].</span></span>

## <a name="alerts"></a><span data-ttu-id="b1adb-136">Alerts</span><span class="sxs-lookup"><span data-stu-id="b1adb-136">Alerts</span></span>
<span data-ttu-id="b1adb-137">您可以進行設定來收到以計量和活動記錄為基礎的警示。</span><span class="sxs-lookup"><span data-stu-id="b1adb-137">You can configure to receive alerts based on metrics and activity logs.</span></span> <span data-ttu-id="b1adb-138">Azure 監視器可讓您將警示設定為在觸發時執行下列動作︰</span><span class="sxs-lookup"><span data-stu-id="b1adb-138">Azure Monitor allows you to configure an alert to do the following when it triggers:</span></span>

* <span data-ttu-id="b1adb-139">傳送電子郵件通知</span><span class="sxs-lookup"><span data-stu-id="b1adb-139">Send an email notification</span></span>
* <span data-ttu-id="b1adb-140">呼叫 Webhook</span><span class="sxs-lookup"><span data-stu-id="b1adb-140">Call a webhook</span></span>
* <span data-ttu-id="b1adb-141">叫用 Azure 邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="b1adb-141">Invoke an Azure Logic App</span></span>

<span data-ttu-id="b1adb-142">您可以在 API 管理服務或 Azure 監視器中設定警示規則。</span><span class="sxs-lookup"><span data-stu-id="b1adb-142">You can configure alert rules in your API Management service, or in Azure Monitor.</span></span> <span data-ttu-id="b1adb-143">若要在 API 管理中進行設定︰</span><span class="sxs-lookup"><span data-stu-id="b1adb-143">To configure them in API Management:</span></span> 
1. <span data-ttu-id="b1adb-144">開啟 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="b1adb-144">Open the Azure portal.</span></span>
2. <span data-ttu-id="b1adb-145">移至 API 管理服務。</span><span class="sxs-lookup"><span data-stu-id="b1adb-145">Go to your API Management service.</span></span>
3. <span data-ttu-id="b1adb-146">按一下 [警示規則]。</span><span class="sxs-lookup"><span data-stu-id="b1adb-146">Click **Alert rules**.</span></span>

![警示規則刀鋒視窗][alert-rules-blade]

<span data-ttu-id="b1adb-148">如需有關使用警示的詳細資訊，請參閱[警示概觀]。</span><span class="sxs-lookup"><span data-stu-id="b1adb-148">For more information about using Alerts, see [Overview of Alerts].</span></span>

## <a name="diagnostic-logs"></a><span data-ttu-id="b1adb-149">診斷記錄檔</span><span class="sxs-lookup"><span data-stu-id="b1adb-149">Diagnostic Logs</span></span>
<span data-ttu-id="b1adb-150">診斷記錄可提供豐富的作業與錯誤資訊，這些資訊對於稽核和疑難排解用途來說很重要。</span><span class="sxs-lookup"><span data-stu-id="b1adb-150">Diagnostic logs provide rich information about operations and errors that are important for auditing as well as troubleshooting purposes.</span></span> <span data-ttu-id="b1adb-151">診斷記錄與活動記錄不同。</span><span class="sxs-lookup"><span data-stu-id="b1adb-151">Diagnostics logs differ from activity logs.</span></span> <span data-ttu-id="b1adb-152">活動記錄可讓您深入了解 Azure 資源上所執行的作業。</span><span class="sxs-lookup"><span data-stu-id="b1adb-152">Activity logs provide insights into the operations that were performed on your Azure resources.</span></span> <span data-ttu-id="b1adb-153">診斷記錄能讓您了解資源自行執行的作業。</span><span class="sxs-lookup"><span data-stu-id="b1adb-153">Diagnostics logs provide insight into operations that your resource performed itself.</span></span>

<span data-ttu-id="b1adb-154">API 管理目前提供關於個別 API 要求的診斷記錄 (每小時提供一批)，且每個要求項目都有下列結構︰</span><span class="sxs-lookup"><span data-stu-id="b1adb-154">API Management currently provides diagnostics logs (batched hourly) about individual API request with each entry having the following structure:</span></span>

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

<span data-ttu-id="b1adb-155">您可以在 API 管理服務中存取診斷記錄，或在 Azure 監視器中存取所有 Azure 資源的記錄。</span><span class="sxs-lookup"><span data-stu-id="b1adb-155">You can access diagnostic logs in your API Management service, or access logs of all your Azure resources in Azure Monitor.</span></span> <span data-ttu-id="b1adb-156">若要在 API 管理服務中檢視診斷記錄︰</span><span class="sxs-lookup"><span data-stu-id="b1adb-156">To view diagnostic logs in your API Management service:</span></span>
1. <span data-ttu-id="b1adb-157">開啟 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="b1adb-157">Open the Azure portal.</span></span>
2. <span data-ttu-id="b1adb-158">移至 API 管理服務。</span><span class="sxs-lookup"><span data-stu-id="b1adb-158">Go to your API Management service.</span></span>
3. <span data-ttu-id="b1adb-159">按一下 [診斷記錄]。</span><span class="sxs-lookup"><span data-stu-id="b1adb-159">Click **Diagnostic log**.</span></span>

![診斷記錄檔刀鋒視窗][diagnostic-logs-blade]

<span data-ttu-id="b1adb-161">如需如何使用計量的詳細資訊，請參閱[診斷記錄概觀]。</span><span class="sxs-lookup"><span data-stu-id="b1adb-161">For more information about how to use Metrics, see [Overview of Diagnostic Logs].</span></span>

## <a name="next-step"></a><span data-ttu-id="b1adb-162">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b1adb-162">Next Step</span></span>

* <span data-ttu-id="b1adb-163">[開始使用 Azure 監視器]</span><span class="sxs-lookup"><span data-stu-id="b1adb-163">[Get Started with Azure Monitor]</span></span>
* <span data-ttu-id="b1adb-164">[計量概觀]</span><span class="sxs-lookup"><span data-stu-id="b1adb-164">[Overview of Metrics]</span></span>
* <span data-ttu-id="b1adb-165">[活動記錄概觀]</span><span class="sxs-lookup"><span data-stu-id="b1adb-165">[Overview of Activity Logs]</span></span>
* <span data-ttu-id="b1adb-166">[診斷記錄概觀]</span><span class="sxs-lookup"><span data-stu-id="b1adb-166">[Overview of Diagnostic Logs]</span></span>
* <span data-ttu-id="b1adb-167">[警示概觀]</span><span class="sxs-lookup"><span data-stu-id="b1adb-167">[Overview of Alerts]</span></span>

<span data-ttu-id="b1adb-168">[開始使用 Azure 監視器]: ../monitoring-and-diagnostics/monitoring-get-started.md</span><span class="sxs-lookup"><span data-stu-id="b1adb-168">[Get Started with Azure Monitor]: ../monitoring-and-diagnostics/monitoring-get-started.md</span></span>
<span data-ttu-id="b1adb-169">[計量概觀]: ../monitoring-and-diagnostics/monitoring-overview-metrics.md</span><span class="sxs-lookup"><span data-stu-id="b1adb-169">[Overview of Metrics]: ../monitoring-and-diagnostics/monitoring-overview-metrics.md</span></span>
<span data-ttu-id="b1adb-170">[活動記錄概觀]: ../monitoring-and-diagnostics/monitoring-overview-activity-logs.md</span><span class="sxs-lookup"><span data-stu-id="b1adb-170">[Overview of Activity Logs]: ../monitoring-and-diagnostics/monitoring-overview-activity-logs.md</span></span>
<span data-ttu-id="b1adb-171">[診斷記錄概觀]: ../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md</span><span class="sxs-lookup"><span data-stu-id="b1adb-171">[Overview of Diagnostic Logs]: ../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md</span></span>
<span data-ttu-id="b1adb-172">[警示概觀]: ../monitoring-and-diagnostics/insights-alerts-portal.md</span><span class="sxs-lookup"><span data-stu-id="b1adb-172">[Overview of Alerts]: ../monitoring-and-diagnostics/insights-alerts-portal.md</span></span>



[metrics-blade]: ./media/api-management-azure-monitor/api-management-metrics-blade.png
[activity-logs-blade]: ./media/api-management-azure-monitor/api-management-activity-logs-blade.png
[alert-rules-blade]: ./media/api-management-azure-monitor/api-management-alert-rules-blade.png
[diagnostic-logs-blade]: ./media/api-management-azure-monitor/api-management-diagnostic-logs-blade.png
