---
title: "aaaStream hello Azure 活動記錄檔 tooEvent 中心 |Microsoft 文件"
description: "了解如何 toostream hello Azure 活動記錄檔 tooEvent 集線器。"
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
ms.openlocfilehash: 336f92771b9d4379ad9dbcadc6997dfae7fae7bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="stream-hello-azure-activity-log-tooevent-hubs"></a><span data-ttu-id="da4c6-103">資料流 hello Azure 活動記錄檔 tooEvent 集線器</span><span class="sxs-lookup"><span data-stu-id="da4c6-103">Stream hello Azure Activity Log tooEvent Hubs</span></span>
<span data-ttu-id="da4c6-104">hello [ **Azure 活動記錄檔**](monitoring-overview-activity-logs.md)可以附近使用 hello 內建 「 匯出 」 選項在 hello 入口網站的即時 tooany 應用程式資料流中，或藉由啟用 hello hello 透過記錄檔中的服務匯流排規則識別碼Azure PowerShell Cmdlet 或 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="da4c6-104">hello [**Azure Activity Log**](monitoring-overview-activity-logs.md) can be streamed in near real time tooany application using hello built-in “Export” option in hello portal, or by enabling hello Service Bus Rule Id in a Log Profile via hello Azure PowerShell Cmdlets or Azure CLI.</span></span>

## <a name="what-you-can-do-with-hello-activity-log-and-event-hubs"></a><span data-ttu-id="da4c6-105">您可以使用 hello 活動記錄檔和事件中心執行</span><span class="sxs-lookup"><span data-stu-id="da4c6-105">What you can do with hello Activity Log and Event Hubs</span></span>
<span data-ttu-id="da4c6-106">以下是幾個方法，您可能會使用 hello 串流 hello 活動記錄檔的功能：</span><span class="sxs-lookup"><span data-stu-id="da4c6-106">Here are just a few ways you might use hello streaming capability for hello Activity Log:</span></span>

* <span data-ttu-id="da4c6-107">**資料流 toothird 合作對象記錄與遙測系統**– 一段時間，事件中心資料流將會變成 hello 機制 toopipe 活動記錄，到第三方 Siem 且記錄分析解決方案。</span><span class="sxs-lookup"><span data-stu-id="da4c6-107">**Stream toothird-party logging and telemetry systems** – Over time, Event Hubs streaming will become hello mechanism toopipe your Activity Log into third-party SIEMs and log analytics solutions.</span></span>
* <span data-ttu-id="da4c6-108">**建置自訂的遙測及記錄平台**– 如果您已自訂的遙測平台，或都只考慮的建立一個具有高擴充性 hello 發行-訂閱性質的事件中心可讓您 tooflexibly 內嵌 hello活動記錄檔。</span><span class="sxs-lookup"><span data-stu-id="da4c6-108">**Build a custom telemetry and logging platform** – If you already have a custom-built telemetry platform or are just thinking about building one, hello highly scalable publish-subscribe nature of Event Hubs allows you tooflexibly ingest hello activity log.</span></span> [<span data-ttu-id="da4c6-109">請參閱 Dan Rosanova 指南 toousing 事件中心的全球遙測平台。</span><span class="sxs-lookup"><span data-stu-id="da4c6-109">See Dan Rosanova’s guide toousing Event Hubs in a global scale telemetry platform here.</span></span>](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/)

## <a name="enable-streaming-of-hello-activity-log"></a><span data-ttu-id="da4c6-110">啟用資料流的 hello 活動記錄檔</span><span class="sxs-lookup"><span data-stu-id="da4c6-110">Enable streaming of hello Activity Log</span></span>
<span data-ttu-id="da4c6-111">您可以啟用以程式設計方式或透過 hello 入口網站的 hello 活動記錄檔資料流。</span><span class="sxs-lookup"><span data-stu-id="da4c6-111">You can enable streaming of hello Activity Log either programmatically or via hello portal.</span></span> <span data-ttu-id="da4c6-112">無論如何，您會選擇服務匯流排命名空間和共用的存取原則，該命名空間，且 hello 第一個新活動記錄檔事件發生時，將會建立該命名空間中的事件中心。</span><span class="sxs-lookup"><span data-stu-id="da4c6-112">Either way, you pick a Service Bus Namespace and a shared access policy for that namespace, and an Event Hub is created in that namespace when hello first new Activity Log event occurs.</span></span> <span data-ttu-id="da4c6-113">如果您沒有服務匯流排命名空間，您必須先 toocreate 其中一個。</span><span class="sxs-lookup"><span data-stu-id="da4c6-113">If you do not have a Service Bus Namespace, you first need toocreate one.</span></span> <span data-ttu-id="da4c6-114">如果您先前串流處理的資料活動記錄檔事件 toothis 服務匯流排命名空間，將會重複使用 hello 先前建立的事件中樞。</span><span class="sxs-lookup"><span data-stu-id="da4c6-114">If you have previously streamed Activity Log events toothis Service Bus Namespace, hello Event Hub that was previously created will be reused.</span></span> <span data-ttu-id="da4c6-115">hello 共用存取原則是定義 hello hello 串流處理機制具有的權限。</span><span class="sxs-lookup"><span data-stu-id="da4c6-115">hello shared access policy defines hello permissions that hello streaming mechanism has.</span></span> <span data-ttu-id="da4c6-116">現在，資料流 tooan 事件中心需要**管理**，**傳送**，和**接聽**權限。</span><span class="sxs-lookup"><span data-stu-id="da4c6-116">Today, streaming tooan Event Hubs requires **Manage**, **Send**, and **Listen** permissions.</span></span> <span data-ttu-id="da4c6-117">您可以建立或修改您的服務匯流排命名空間的 hello hello 「 設定 」 索引標籤底下的傳統入口網站中的服務匯流排命名空間共用存取原則。</span><span class="sxs-lookup"><span data-stu-id="da4c6-117">You can create or modify Service Bus Namespace shared access policies in hello classic portal under hello “Configure” tab for your Service Bus Namespace.</span></span> <span data-ttu-id="da4c6-118">tooupdate hello 活動記錄檔記錄的設定檔 tooinclude 串流、 變更 hello hello 使用者必須擁有該服務匯流排的授權規則 hello ListKey 權限。</span><span class="sxs-lookup"><span data-stu-id="da4c6-118">tooupdate hello Activity Log log profile tooinclude streaming, hello user making hello change must have hello ListKey permission on that Service Bus Authorization Rule.</span></span>

<span data-ttu-id="da4c6-119">hello 服務匯流排或事件中樞命名空間中並沒有 toobe hello 發出記錄檔，只要將設定 hello 設定 hello 使用者擁有適當的 RBAC 存取 tooboth 訂閱 hello 訂用帳戶相同訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="da4c6-119">hello service bus or event hub namespace does not have toobe in hello same subscription as hello subscription emitting logs as long as hello user who configures hello setting has appropriate RBAC access tooboth subscriptions.</span></span>

### <a name="via-azure-portal"></a><span data-ttu-id="da4c6-120">透過 Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="da4c6-120">Via Azure portal</span></span>
1. <span data-ttu-id="da4c6-121">瀏覽 toohello**活動記錄檔**刀鋒視窗上 hello hello 入口網站的左側使用 hello 功能表。</span><span class="sxs-lookup"><span data-stu-id="da4c6-121">Navigate toohello **Activity Log** blade using hello menu on hello left side of hello portal.</span></span>
   
    ![瀏覽 tooActivity 記錄在入口網站](./media/monitoring-overview-activity-logs/activity-logs-portal-navigate.png)
2. <span data-ttu-id="da4c6-123">按一下 hello**匯出**在 hello hello 刀鋒視窗頂端的按鈕。</span><span class="sxs-lookup"><span data-stu-id="da4c6-123">Click hello **Export** button at hello top of hello blade.</span></span>
   
    ![入口網站中的匯出按鈕](./media/monitoring-overview-activity-logs/activity-logs-portal-export.png)
3. <span data-ttu-id="da4c6-125">在 hello 刀鋒視窗中出現，您可以選取您想其 toostream 事件和 hello 服務匯流排命名空間中，您想要串流處理這些事件建立事件中樞 toobe hello 區域。</span><span class="sxs-lookup"><span data-stu-id="da4c6-125">In hello blade that appears, you can select hello regions for which you would like toostream events and hello Service Bus Namespace in which you would like an Event Hub toobe created for streaming these events.</span></span>
   
    ![匯出活動記錄檔刀鋒視窗](./media/monitoring-overview-activity-logs/activity-logs-portal-export-blade.png)
4. <span data-ttu-id="da4c6-127">按一下**儲存**toosave 這些設定。</span><span class="sxs-lookup"><span data-stu-id="da4c6-127">Click **Save** toosave these settings.</span></span> <span data-ttu-id="da4c6-128">hello 設定會立即會套用的 tooyour 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="da4c6-128">hello settings are immediately be applied tooyour subscription.</span></span>

### <a name="via-powershell-cmdlets"></a><span data-ttu-id="da4c6-129">透過 PowerShell Cmdlet</span><span class="sxs-lookup"><span data-stu-id="da4c6-129">Via PowerShell Cmdlets</span></span>
<span data-ttu-id="da4c6-130">如果記錄檔的設定檔已經存在，您必須先 tooremove 該設定檔。</span><span class="sxs-lookup"><span data-stu-id="da4c6-130">If a log profile already exists, you first need tooremove that profile.</span></span>

1. <span data-ttu-id="da4c6-131">使用`Get-AzureRmLogProfile`tooidentify 如果記錄檔的設定檔</span><span class="sxs-lookup"><span data-stu-id="da4c6-131">Use `Get-AzureRmLogProfile` tooidentify if a log profile exists</span></span>
2. <span data-ttu-id="da4c6-132">如果是，使用`Remove-AzureRmLogProfile`tooremove 它。</span><span class="sxs-lookup"><span data-stu-id="da4c6-132">If so, use `Remove-AzureRmLogProfile` tooremove it.</span></span>
3. <span data-ttu-id="da4c6-133">使用`Set-AzureRmLogProfile`toocreate 設定檔：</span><span class="sxs-lookup"><span data-stu-id="da4c6-133">Use `Set-AzureRmLogProfile` toocreate a profile:</span></span>

```
Add-AzureRmLogProfile -Name my_log_profile -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Locations global,westus,eastus -RetentionInDays 90 -Categories Write,Delete,Action
```

<span data-ttu-id="da4c6-134">服務匯流排規則識別碼 hello 是這種格式的字串: {服務匯流排資源識別碼} /authorizationrules/ {索引鍵名稱}，例如</span><span class="sxs-lookup"><span data-stu-id="da4c6-134">hello Service Bus Rule ID is a string with this format: {service bus resource ID}/authorizationrules/{key name}, for example</span></span> 

### <a name="via-azure-cli"></a><span data-ttu-id="da4c6-135">透過 Azure CLI</span><span class="sxs-lookup"><span data-stu-id="da4c6-135">Via Azure CLI</span></span>
<span data-ttu-id="da4c6-136">如果記錄檔的設定檔已經存在，您必須先 tooremove 該設定檔。</span><span class="sxs-lookup"><span data-stu-id="da4c6-136">If a log profile already exists, you first need tooremove that profile.</span></span>

1. <span data-ttu-id="da4c6-137">使用`azure insights logprofile list`tooidentify 如果記錄檔的設定檔</span><span class="sxs-lookup"><span data-stu-id="da4c6-137">Use `azure insights logprofile list` tooidentify if a log profile exists</span></span>
2. <span data-ttu-id="da4c6-138">如果是，使用`azure insights logprofile delete`tooremove 它。</span><span class="sxs-lookup"><span data-stu-id="da4c6-138">If so, use `azure insights logprofile delete` tooremove it.</span></span>
3. <span data-ttu-id="da4c6-139">使用`azure insights logprofile add`toocreate 設定檔：</span><span class="sxs-lookup"><span data-stu-id="da4c6-139">Use `azure insights logprofile add` toocreate a profile:</span></span>

```
azure insights logprofile add --name my_log_profile --storageId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/my_storage --serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey --locations global,westus,eastus,northeurope --retentionInDays 90 –categories Write,Delete,Action
```

<span data-ttu-id="da4c6-140">服務匯流排規則識別碼 hello 是這種格式的字串： `{service bus resource ID}/authorizationrules/{key name}`。</span><span class="sxs-lookup"><span data-stu-id="da4c6-140">hello Service Bus Rule ID is a string with this format: `{service bus resource ID}/authorizationrules/{key name}`.</span></span>

## <a name="how-do-i-consume-hello-log-data-from-event-hubs"></a><span data-ttu-id="da4c6-141">我要如何使用 hello 記錄資料，從事件中心？</span><span class="sxs-lookup"><span data-stu-id="da4c6-141">How do I consume hello log data from Event Hubs?</span></span>
<span data-ttu-id="da4c6-142">[這裡會提供 hello hello 活動記錄檔的結構描述](monitoring-overview-activity-logs.md)。</span><span class="sxs-lookup"><span data-stu-id="da4c6-142">[hello schema for hello Activity Log is available here](monitoring-overview-activity-logs.md).</span></span> <span data-ttu-id="da4c6-143">每個事件位於名為「記錄」的 JSON blob 陣列中。</span><span class="sxs-lookup"><span data-stu-id="da4c6-143">Each event is in an array of JSON blobs called “records.”</span></span>

## <a name="next-steps"></a><span data-ttu-id="da4c6-144">後續步驟</span><span class="sxs-lookup"><span data-stu-id="da4c6-144">Next Steps</span></span>
* [<span data-ttu-id="da4c6-145">封存 hello 活動記錄檔 tooa 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="da4c6-145">Archive hello Activity Log tooa storage account</span></span>](monitoring-archive-activity-log.md)
* [<span data-ttu-id="da4c6-146">讀取 hello hello Azure 活動記錄檔的概觀</span><span class="sxs-lookup"><span data-stu-id="da4c6-146">Read hello overview of hello Azure Activity Log</span></span>](monitoring-overview-activity-logs.md)
* [<span data-ttu-id="da4c6-147">根據活動記錄檔事件設定警示</span><span class="sxs-lookup"><span data-stu-id="da4c6-147">Set up an alert based on an Activity Log event</span></span>](insights-auditlog-to-webhook-email.md)

