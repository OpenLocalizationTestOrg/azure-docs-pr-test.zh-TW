---
title: "將 Azure 活動記錄檔串流至事件中樞 | Microsoft Docs"
description: "了解如何將 Azure 活動記錄檔串流至事件中樞。"
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: ec4c2d2c-8907-484f-a910-712403a06829
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 6/06/2017
ms.author: johnkem
ms.openlocfilehash: 88c5701279f370914fac68872d67b02a7571748a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="stream-the-azure-activity-log-to-event-hubs"></a><span data-ttu-id="bd9c1-103">將 Azure 活動記錄檔串流至事件中樞</span><span class="sxs-lookup"><span data-stu-id="bd9c1-103">Stream the Azure Activity Log to Event Hubs</span></span>
<span data-ttu-id="bd9c1-104">您可以使用入口網站中內建的「匯出」選項，或透過 Azure PowerShell Cmdlet 或 Azure CLI 來啟用記錄設定檔中服務匯流排規則識別碼的方式，迅速將 [**Azure 活動記錄檔**](monitoring-overview-activity-logs.md)串流至任何應用程式。</span><span class="sxs-lookup"><span data-stu-id="bd9c1-104">The [**Azure Activity Log**](monitoring-overview-activity-logs.md) can be streamed in near real time to any application using the built-in “Export” option in the portal, or by enabling the Service Bus Rule Id in a Log Profile via the Azure PowerShell Cmdlets or Azure CLI.</span></span>

## <a name="what-you-can-do-with-the-activity-log-and-event-hubs"></a><span data-ttu-id="bd9c1-105">您可以使用活動記錄檔與事件中樞執行的項目</span><span class="sxs-lookup"><span data-stu-id="bd9c1-105">What you can do with the Activity Log and Event Hubs</span></span>
<span data-ttu-id="bd9c1-106">此處提供一些您可以使用活動記錄檔串流功能的方法：</span><span class="sxs-lookup"><span data-stu-id="bd9c1-106">Here are just a few ways you might use the streaming capability for the Activity Log:</span></span>

* <span data-ttu-id="bd9c1-107">**串流至協力廠商記錄與遙測系統** – 經過一段時間，事件中樞串流會成為將活動記錄檔輸送到協力廠商的 SIEM 與記錄分析解決方案的機制。</span><span class="sxs-lookup"><span data-stu-id="bd9c1-107">**Stream to third-party logging and telemetry systems** – Over time, Event Hubs streaming will become the mechanism to pipe your Activity Log into third-party SIEMs and log analytics solutions.</span></span>
* <span data-ttu-id="bd9c1-108">**建置自訂遙測及記錄平台** – 如果您已有自建遙測平台或正在考慮建置一個，事件中樞所具備的高度可調整發佈訂閱特質可讓您靈活擷取活動記錄檔。</span><span class="sxs-lookup"><span data-stu-id="bd9c1-108">**Build a custom telemetry and logging platform** – If you already have a custom-built telemetry platform or are just thinking about building one, the highly scalable publish-subscribe nature of Event Hubs allows you to flexibly ingest the activity log.</span></span> [<span data-ttu-id="bd9c1-109">請參閱此處的 Dan Rosanova 指南，以在全球級別的遙測平台中使用事件中樞。</span><span class="sxs-lookup"><span data-stu-id="bd9c1-109">See Dan Rosanova’s guide to using Event Hubs in a global scale telemetry platform here.</span></span>](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/)

## <a name="enable-streaming-of-the-activity-log"></a><span data-ttu-id="bd9c1-110">啟用活動記錄檔的串流功能</span><span class="sxs-lookup"><span data-stu-id="bd9c1-110">Enable streaming of the Activity Log</span></span>
<span data-ttu-id="bd9c1-111">您可以以程式控制的方式，或透過入口網站來啟用活動記錄檔的串流功能。</span><span class="sxs-lookup"><span data-stu-id="bd9c1-111">You can enable streaming of the Activity Log either programmatically or via the portal.</span></span> <span data-ttu-id="bd9c1-112">無論您使用何種方式，您都會選擇服務匯流排命名空間及該命名空間的共用存取原則，而且在第一個新的活動記錄檔事件發生時，該命名空間中將會建立事件中樞。</span><span class="sxs-lookup"><span data-stu-id="bd9c1-112">Either way, you pick a Service Bus Namespace and a shared access policy for that namespace, and an Event Hub is created in that namespace when the first new Activity Log event occurs.</span></span> <span data-ttu-id="bd9c1-113">如果您沒有服務匯流排命名空間，您必須先建立一個。</span><span class="sxs-lookup"><span data-stu-id="bd9c1-113">If you do not have a Service Bus Namespace, you first need to create one.</span></span> <span data-ttu-id="bd9c1-114">如果您先前已將活動記錄檔事件串流處理到此服務匯流排命名空間，則會重複使用先前建立的事件中樞。</span><span class="sxs-lookup"><span data-stu-id="bd9c1-114">If you have previously streamed Activity Log events to this Service Bus Namespace, the Event Hub that was previously created will be reused.</span></span> <span data-ttu-id="bd9c1-115">共用存取原則會定義串流機制具有的權限。</span><span class="sxs-lookup"><span data-stu-id="bd9c1-115">The shared access policy defines the permissions that the streaming mechanism has.</span></span> <span data-ttu-id="bd9c1-116">目前，串流到事件中樞需要**管理**、**傳送**和**接聽**權限。</span><span class="sxs-lookup"><span data-stu-id="bd9c1-116">Today, streaming to an Event Hubs requires **Manage**, **Send**, and **Listen** permissions.</span></span> <span data-ttu-id="bd9c1-117">您可以在傳統入口網站 [設定] 索引標籤下，為您的服務匯流排命名空間建立或修改服務匯流排命名空間共用存取原則。</span><span class="sxs-lookup"><span data-stu-id="bd9c1-117">You can create or modify Service Bus Namespace shared access policies in the classic portal under the “Configure” tab for your Service Bus Namespace.</span></span> <span data-ttu-id="bd9c1-118">若要更新活動記錄檔設定檔以加入串流，進行變更的使用者必須擁有該服務匯流排授權規則的 ListKey 權限。</span><span class="sxs-lookup"><span data-stu-id="bd9c1-118">To update the Activity Log log profile to include streaming, the user making the change must have the ListKey permission on that Service Bus Authorization Rule.</span></span>

<span data-ttu-id="bd9c1-119">服務匯流排或事件中樞命名空間不一定要和訂用帳戶發出記錄檔屬於相同的訂用帳戶，只要使用者有適當的設定可 RBAC 存取這兩個訂用帳戶即可。</span><span class="sxs-lookup"><span data-stu-id="bd9c1-119">The service bus or event hub namespace does not have to be in the same subscription as the subscription emitting logs as long as the user who configures the setting has appropriate RBAC access to both subscriptions.</span></span>

### <a name="via-azure-portal"></a><span data-ttu-id="bd9c1-120">透過 Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="bd9c1-120">Via Azure portal</span></span>
1. <span data-ttu-id="bd9c1-121">使用入口網站左側的功能表，瀏覽至 [活動記錄檔]  刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="bd9c1-121">Navigate to the **Activity Log** blade using the menu on the left side of the portal.</span></span>
   
    ![在入口網站中瀏覽至活動記錄檔](./media/monitoring-overview-activity-logs/activity-logs-portal-navigate.png)
2. <span data-ttu-id="bd9c1-123">按一下刀鋒視窗頂端的 [匯出]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="bd9c1-123">Click the **Export** button at the top of the blade.</span></span>
   
    ![入口網站中的匯出按鈕](./media/monitoring-overview-activity-logs/activity-logs-portal-export.png)
3. <span data-ttu-id="bd9c1-125">在出現的刀鋒視窗中，您可以選取想要串流事件的區域，以及服務匯流排命名空間，以在其中建立事件中樞建立以對這些事件進行串流處理。</span><span class="sxs-lookup"><span data-stu-id="bd9c1-125">In the blade that appears, you can select the regions for which you would like to stream events and the Service Bus Namespace in which you would like an Event Hub to be created for streaming these events.</span></span>
   
    ![匯出活動記錄檔刀鋒視窗](./media/monitoring-overview-activity-logs/activity-logs-portal-export-blade.png)
4. <span data-ttu-id="bd9c1-127">按一下 [儲存]  來儲存這些設定。</span><span class="sxs-lookup"><span data-stu-id="bd9c1-127">Click **Save** to save these settings.</span></span> <span data-ttu-id="bd9c1-128">您的訂用帳戶時會立即套用設定。</span><span class="sxs-lookup"><span data-stu-id="bd9c1-128">The settings are immediately be applied to your subscription.</span></span>

### <a name="via-powershell-cmdlets"></a><span data-ttu-id="bd9c1-129">透過 PowerShell Cmdlet</span><span class="sxs-lookup"><span data-stu-id="bd9c1-129">Via PowerShell Cmdlets</span></span>
<span data-ttu-id="bd9c1-130">如果記錄檔設定檔已存在，您必須先移除該設定檔。</span><span class="sxs-lookup"><span data-stu-id="bd9c1-130">If a log profile already exists, you first need to remove that profile.</span></span>

1. <span data-ttu-id="bd9c1-131">使用 `Get-AzureRmLogProfile` 來識別記錄檔設定檔是否存在</span><span class="sxs-lookup"><span data-stu-id="bd9c1-131">Use `Get-AzureRmLogProfile` to identify if a log profile exists</span></span>
2. <span data-ttu-id="bd9c1-132">如果有，使用 `Remove-AzureRmLogProfile` 來進行移除。</span><span class="sxs-lookup"><span data-stu-id="bd9c1-132">If so, use `Remove-AzureRmLogProfile` to remove it.</span></span>
3. <span data-ttu-id="bd9c1-133">使用 `Set-AzureRmLogProfile` 來建立設定檔：</span><span class="sxs-lookup"><span data-stu-id="bd9c1-133">Use `Set-AzureRmLogProfile` to create a profile:</span></span>

```
Add-AzureRmLogProfile -Name my_log_profile -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Locations global,westus,eastus -RetentionInDays 90 -Categories Write,Delete,Action
```

<span data-ttu-id="bd9c1-134">舉例來說，服務匯流排規則識別碼一組字串，格式如下：{service bus resource ID}/authorizationrules/{key name}</span><span class="sxs-lookup"><span data-stu-id="bd9c1-134">The Service Bus Rule ID is a string with this format: {service bus resource ID}/authorizationrules/{key name}, for example</span></span> 

### <a name="via-azure-cli"></a><span data-ttu-id="bd9c1-135">透過 Azure CLI</span><span class="sxs-lookup"><span data-stu-id="bd9c1-135">Via Azure CLI</span></span>
<span data-ttu-id="bd9c1-136">如果記錄檔設定檔已存在，您必須先移除該設定檔。</span><span class="sxs-lookup"><span data-stu-id="bd9c1-136">If a log profile already exists, you first need to remove that profile.</span></span>

1. <span data-ttu-id="bd9c1-137">使用 `azure insights logprofile list` 來識別記錄檔設定檔是否存在</span><span class="sxs-lookup"><span data-stu-id="bd9c1-137">Use `azure insights logprofile list` to identify if a log profile exists</span></span>
2. <span data-ttu-id="bd9c1-138">如果有，使用 `azure insights logprofile delete` 來進行移除。</span><span class="sxs-lookup"><span data-stu-id="bd9c1-138">If so, use `azure insights logprofile delete` to remove it.</span></span>
3. <span data-ttu-id="bd9c1-139">使用 `azure insights logprofile add` 來建立設定檔：</span><span class="sxs-lookup"><span data-stu-id="bd9c1-139">Use `azure insights logprofile add` to create a profile:</span></span>

```
azure insights logprofile add --name my_log_profile --storageId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/my_storage --serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey --locations global,westus,eastus,northeurope --retentionInDays 90 –categories Write,Delete,Action
```

<span data-ttu-id="bd9c1-140">服務匯流排規則識別碼是此格式的字串︰ `{service bus resource ID}/authorizationrules/{key name}`。</span><span class="sxs-lookup"><span data-stu-id="bd9c1-140">The Service Bus Rule ID is a string with this format: `{service bus resource ID}/authorizationrules/{key name}`.</span></span>

## <a name="how-do-i-consume-the-log-data-from-event-hubs"></a><span data-ttu-id="bd9c1-141">我要如何透過事件中樞取用記錄檔資料？</span><span class="sxs-lookup"><span data-stu-id="bd9c1-141">How do I consume the log data from Event Hubs?</span></span>
<span data-ttu-id="bd9c1-142">[記錄檔的結構描述可在此取得](monitoring-overview-activity-logs.md)。</span><span class="sxs-lookup"><span data-stu-id="bd9c1-142">[The schema for the Activity Log is available here](monitoring-overview-activity-logs.md).</span></span> <span data-ttu-id="bd9c1-143">每個事件位於名為「記錄」的 JSON blob 陣列中。</span><span class="sxs-lookup"><span data-stu-id="bd9c1-143">Each event is in an array of JSON blobs called “records.”</span></span>

## <a name="next-steps"></a><span data-ttu-id="bd9c1-144">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bd9c1-144">Next Steps</span></span>
* [<span data-ttu-id="bd9c1-145">將活動記錄檔封存至儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="bd9c1-145">Archive the Activity Log to a storage account</span></span>](monitoring-archive-activity-log.md)
* [<span data-ttu-id="bd9c1-146">閱讀 Azure 活動記錄檔的概觀</span><span class="sxs-lookup"><span data-stu-id="bd9c1-146">Read the overview of the Azure Activity Log</span></span>](monitoring-overview-activity-logs.md)
* [<span data-ttu-id="bd9c1-147">根據活動記錄檔事件設定警示</span><span class="sxs-lookup"><span data-stu-id="bd9c1-147">Set up an alert based on an Activity Log event</span></span>](insights-auditlog-to-webhook-email.md)

