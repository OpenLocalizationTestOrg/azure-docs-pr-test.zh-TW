---
title: "使用 Azure 虛擬機器的自動調整規模 aaaAdvanced |Microsoft 文件"
description: "使用 Resource Manager 和 VM 擴展集，搭配多個規則與設定檔，以傳送電子郵件並使用調整動作來呼叫 Webhook URL。"
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 7e3576e2-4a2b-4736-b5ae-98c4689cdd2b
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2016
ms.author: ancav
ms.openlocfilehash: ecb01e3094f715837b75ef07a7dbecdf0f2e78f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-autoscale-configuration-using-resource-manager-templates-for-vm-scale-sets"></a><span data-ttu-id="3bff3-103">針對 VM 擴展集使用 Resource Manager 範本的進階自動調整設定</span><span class="sxs-lookup"><span data-stu-id="3bff3-103">Advanced autoscale configuration using Resource Manager templates for VM Scale Sets</span></span>
<span data-ttu-id="3bff3-104">您可以根據效能標準臨界值、循環排程或特定日期，針對虛擬機器擴展集進行相應縮小和放大。</span><span class="sxs-lookup"><span data-stu-id="3bff3-104">You can scale-in and scale-out in Virtual Machine Scale Sets based on performance metric thresholds, by a recurring schedule, or by a particular date.</span></span> <span data-ttu-id="3bff3-105">您也可以針對調整動作設定電子郵件和 webhook 通知。</span><span class="sxs-lookup"><span data-stu-id="3bff3-105">You can also configure email and webhook notifications for scale actions.</span></span> <span data-ttu-id="3bff3-106">本逐步解說會示範在 VM 擴展集上使用 Resource Manager 範本設定所有這些物件。</span><span class="sxs-lookup"><span data-stu-id="3bff3-106">This walkthrough shows an example of configuring all these objects using a Resource Manager template on a VM Scale Set.</span></span>

> [!NOTE]
> <span data-ttu-id="3bff3-107">雖然這個逐步解說將說明 VM 規模集的 hello 步驟，hello 相同的資訊適用於 tooautoscaling[雲端服務](https://azure.microsoft.com/services/cloud-services/)，和[應用程式服務-Web 應用程式](https://azure.microsoft.com/services/app-service/web/)。</span><span class="sxs-lookup"><span data-stu-id="3bff3-107">While this walkthrough explains hello steps for VM Scale Sets, hello same information applies tooautoscaling [Cloud Services](https://azure.microsoft.com/services/cloud-services/), and [App Service - Web Apps](https://azure.microsoft.com/services/app-service/web/).</span></span>
> <span data-ttu-id="3bff3-108">簡單標尺 in/out 上虛擬機器擴展集設定為基礎的簡單的效能度量，如 CPU，參閱 toohello [Linux](../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md)和[Windows](../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md)文件</span><span class="sxs-lookup"><span data-stu-id="3bff3-108">For a simple scale in/out setting on a VM Scale Set based on a simple performance metric such as CPU, refer toohello [Linux](../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md) and [Windows](../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md) documents</span></span>
>
>

## <a name="walkthrough"></a><span data-ttu-id="3bff3-109">逐步介紹</span><span class="sxs-lookup"><span data-stu-id="3bff3-109">Walkthrough</span></span>
<span data-ttu-id="3bff3-110">在此逐步解說中，我們使用[Azure 資源總管](https://resources.azure.com/)擴展集 tooconfigure 和 update hello 自動調整規模設定。</span><span class="sxs-lookup"><span data-stu-id="3bff3-110">In this walkthrough, we use [Azure Resource Explorer](https://resources.azure.com/) tooconfigure and update hello autoscale setting for a scale set.</span></span> <span data-ttu-id="3bff3-111">Azure 資源總管是簡單的方式 toomanage 資源管理員範本透過 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="3bff3-111">Azure Resource Explorer is an easy way toomanage Azure resources via Resource Manager templates.</span></span> <span data-ttu-id="3bff3-112">如果您是新 tooAzure 資源總管工具，請參閱[本簡介](https://azure.microsoft.com/blog/azure-resource-explorer-a-new-tool-to-discover-the-azure-api/)。</span><span class="sxs-lookup"><span data-stu-id="3bff3-112">If you are new tooAzure Resource Explorer tool, read [this introduction](https://azure.microsoft.com/blog/azure-resource-explorer-a-new-tool-to-discover-the-azure-api/).</span></span>

1. <span data-ttu-id="3bff3-113">使用基本自動調整設定部署新的擴展集。</span><span class="sxs-lookup"><span data-stu-id="3bff3-113">Deploy a new scale set with a basic autoscale setting.</span></span> <span data-ttu-id="3bff3-114">本文使用從 hello Azure 快速入門圖庫具有 Windows hello 其中一個基本的自動調整規模範本與設定小數位數。</span><span class="sxs-lookup"><span data-stu-id="3bff3-114">This article uses hello one from hello Azure QuickStart Gallery, which has a Windows scale set with a basic autoscale template.</span></span> <span data-ttu-id="3bff3-115">Linux 小數位數設定工作 hello 相同的方式。</span><span class="sxs-lookup"><span data-stu-id="3bff3-115">Linux scale sets work hello same way.</span></span>
2. <span data-ttu-id="3bff3-116">建立 hello 規模集之後，瀏覽 toohello 小數位數組資源從 Azure 資源總管。</span><span class="sxs-lookup"><span data-stu-id="3bff3-116">After hello scale set is created, navigate toohello scale set resource from Azure Resource Explorer.</span></span> <span data-ttu-id="3bff3-117">您會看到 hello 下列 Microsoft.Insights 節點下。</span><span class="sxs-lookup"><span data-stu-id="3bff3-117">You see hello following under Microsoft.Insights node.</span></span>

    ![Azure Explorer](./media/insights-advanced-autoscale-vmss/azure_explorer_navigate.png)

    <span data-ttu-id="3bff3-119">hello 範本執行已建立預設的自動調整規模設定具有 hello 名稱**'autoscalewad'**。</span><span class="sxs-lookup"><span data-stu-id="3bff3-119">hello template execution has created a default autoscale setting with hello name **'autoscalewad'**.</span></span> <span data-ttu-id="3bff3-120">在 hello 右側，您可以檢視 hello 完整定義，此自動調整規模設定。</span><span class="sxs-lookup"><span data-stu-id="3bff3-120">On hello right-hand side, you can view hello full definition of this autoscale setting.</span></span> <span data-ttu-id="3bff3-121">在此情況下，CPU %基礎向外延展和向中規則內建 hello 預設自動調整規模設定。</span><span class="sxs-lookup"><span data-stu-id="3bff3-121">In this case, hello default autoscale setting comes with a CPU% based scale-out and scale-in rule.</span></span>  

3. <span data-ttu-id="3bff3-122">您現在可以新增多個設定檔和 hello 排程或特定的需求為基礎的規則。</span><span class="sxs-lookup"><span data-stu-id="3bff3-122">You can now add more profiles and rules based on hello schedule or specific requirements.</span></span> <span data-ttu-id="3bff3-123">我們會建立具有三個設定檔的自動調整設定。</span><span class="sxs-lookup"><span data-stu-id="3bff3-123">We create an autoscale setting with three profiles.</span></span> <span data-ttu-id="3bff3-124">toounderstand 設定檔及規則中自動調整規模，請先檢閱[自動調整規模的最佳作法](insights-autoscale-best-practices.md)。</span><span class="sxs-lookup"><span data-stu-id="3bff3-124">toounderstand profiles and rules in autoscale, review [Autoscale Best Practices](insights-autoscale-best-practices.md).</span></span>  

    | <span data-ttu-id="3bff3-125">設定檔與規則</span><span class="sxs-lookup"><span data-stu-id="3bff3-125">Profiles & Rules</span></span> | <span data-ttu-id="3bff3-126">說明</span><span class="sxs-lookup"><span data-stu-id="3bff3-126">Description</span></span> |
    |--- | --- |
    | <span data-ttu-id="3bff3-127">**設定檔**</span><span class="sxs-lookup"><span data-stu-id="3bff3-127">**Profile**</span></span> |<span data-ttu-id="3bff3-128">**以效能/計量為基礎**</span><span class="sxs-lookup"><span data-stu-id="3bff3-128">**Performance/metric based**</span></span> |
    | <span data-ttu-id="3bff3-129">規則</span><span class="sxs-lookup"><span data-stu-id="3bff3-129">Rule</span></span> |<span data-ttu-id="3bff3-130">服務匯流排佇列訊息計數 > x</span><span class="sxs-lookup"><span data-stu-id="3bff3-130">Service Bus Queue Message Count > x</span></span> |
    | <span data-ttu-id="3bff3-131">規則</span><span class="sxs-lookup"><span data-stu-id="3bff3-131">Rule</span></span> |<span data-ttu-id="3bff3-132">服務匯流排佇列訊息計數 < y</span><span class="sxs-lookup"><span data-stu-id="3bff3-132">Service Bus Queue Message Count < y</span></span> |
    | <span data-ttu-id="3bff3-133">規則</span><span class="sxs-lookup"><span data-stu-id="3bff3-133">Rule</span></span> |<span data-ttu-id="3bff3-134">CPU% > n</span><span class="sxs-lookup"><span data-stu-id="3bff3-134">CPU% > n</span></span> |
    | <span data-ttu-id="3bff3-135">規則</span><span class="sxs-lookup"><span data-stu-id="3bff3-135">Rule</span></span> |<span data-ttu-id="3bff3-136">CPU% < p</span><span class="sxs-lookup"><span data-stu-id="3bff3-136">CPU% < p</span></span> |
    | <span data-ttu-id="3bff3-137">**設定檔**</span><span class="sxs-lookup"><span data-stu-id="3bff3-137">**Profile**</span></span> |<span data-ttu-id="3bff3-138">**工作日早上時間 (無規則)**</span><span class="sxs-lookup"><span data-stu-id="3bff3-138">**Weekday morning hours (no rules)**</span></span> |
    | <span data-ttu-id="3bff3-139">**設定檔**</span><span class="sxs-lookup"><span data-stu-id="3bff3-139">**Profile**</span></span> |<span data-ttu-id="3bff3-140">**產品發行日 (無規則)**</span><span class="sxs-lookup"><span data-stu-id="3bff3-140">**Product Launch day (no rules)**</span></span> |

4. <span data-ttu-id="3bff3-141">以下是我們用於此逐步解說的虛構調整案例。</span><span class="sxs-lookup"><span data-stu-id="3bff3-141">Here is a hypothetical scaling scenario that we use for this walk-through.</span></span>

    * <span data-ttu-id="3bff3-142">**負載平衡**-我想 tooscale 出或根據應用程式裝載於我的小數位數 set.* hello 負載</span><span class="sxs-lookup"><span data-stu-id="3bff3-142">**Load based** - I'd like tooscale out or in based on hello load on my application hosted on my scale set.*</span></span>
    * <span data-ttu-id="3bff3-143">**訊息佇列大小**-hello 內送訊息 toomy 應用程式使用服務匯流排佇列。</span><span class="sxs-lookup"><span data-stu-id="3bff3-143">**Message Queue size** - I use a Service Bus Queue for hello incoming messages toomy application.</span></span> <span data-ttu-id="3bff3-144">我使用 hello 佇列的訊息計數和 CPU %，而且如果叫用訊息計數或 CPU hello threshold.* 設定預設設定檔 tootrigger 調整規模動作</span><span class="sxs-lookup"><span data-stu-id="3bff3-144">I use hello queue's message count and CPU% and configure a default profile tootrigger a scale action if either of message count or CPU hits hello threshold.*</span></span>
    * <span data-ttu-id="3bff3-145">**時間的週次和日子**-我想要每週重複執行 '的時間 hello' 基礎稱為的設定檔 ' 工作日上午 Hours'。</span><span class="sxs-lookup"><span data-stu-id="3bff3-145">**Time of week and day** - I want a weekly recurring 'time of hello day' based profile called 'Weekday Morning Hours'.</span></span> <span data-ttu-id="3bff3-146">我知道這是較佳 toohave 特定的 VM 執行個體數目 toohandle 我的應用程式負載期間這個 time.* 根據歷程記錄資料，</span><span class="sxs-lookup"><span data-stu-id="3bff3-146">Based on historical data, I know it is better toohave certain number of VM instances toohandle my application's load during this time.*</span></span>
    * <span data-ttu-id="3bff3-147">**特殊日期** - 我已新增「產品發行日」設定檔。</span><span class="sxs-lookup"><span data-stu-id="3bff3-147">**Special Dates** - I added a 'Product Launch Day' profile.</span></span> <span data-ttu-id="3bff3-148">我計劃繼續的特定日期因此我的應用程式準備好 toohandle hello 負載行銷公告到期和當我們將新的產品放在 hello application.*</span><span class="sxs-lookup"><span data-stu-id="3bff3-148">I plan ahead for specific dates so my application is ready toohandle hello load due marketing announcements and when we put a new product in hello application.*</span></span>
    * <span data-ttu-id="3bff3-149">*hello 最後兩個設定檔也可以有其他效能度量根據的規則中。在此情況下，我決定不一的 toohave 和 hello 預設效能度量上的 toorely 改為基礎的規則。規則是選擇性的 hello 週期性和日期為基礎的設定檔。*</span><span class="sxs-lookup"><span data-stu-id="3bff3-149">*hello last two profiles can also have other performance metric based rules within them. In this case, I decided not toohave one and instead toorely on hello default performance metric based rules. Rules are optional for hello recurring and date-based profiles.*</span></span>

    <span data-ttu-id="3bff3-150">自動調整引擎 hello 設定檔和規則的優先順序也會擷取在 hello[自動調整的最佳作法](insights-autoscale-best-practices.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="3bff3-150">Autoscale engine's prioritization of hello profiles and rules is also captured in hello [autoscaling best practices](insights-autoscale-best-practices.md) article.</span></span>
    <span data-ttu-id="3bff3-151">如需自動調整的常見計量清單，請參閱[自動調整的常用計量](insights-autoscale-common-metrics.md)</span><span class="sxs-lookup"><span data-stu-id="3bff3-151">For a list of common metrics for autoscale, refer [Common metrics for Autoscale](insights-autoscale-common-metrics.md)</span></span>

5. <span data-ttu-id="3bff3-152">請確定您是在 hello**讀/寫**資源總管 中的模式</span><span class="sxs-lookup"><span data-stu-id="3bff3-152">Make sure you are on hello **Read/Write** mode in Resource Explorer</span></span>

    ![Autoscalewad, default autoscale setting, 自動調整, 預設自動調整設定](./media/insights-advanced-autoscale-vmss/autoscalewad.png)

6. <span data-ttu-id="3bff3-154">按一下 [編輯]。</span><span class="sxs-lookup"><span data-stu-id="3bff3-154">Click Edit.</span></span> <span data-ttu-id="3bff3-155">**取代**以 hello 下列組態的自動調整規模設定中的 hello '的設定檔 」 項目：</span><span class="sxs-lookup"><span data-stu-id="3bff3-155">**Replace** hello 'profiles' element in autoscale setting with hello following configuration:</span></span>

    ![設定檔](./media/insights-advanced-autoscale-vmss/profiles.png)

    ```
    {
            "name": "Perf_Based_Scale",
            "capacity": {
              "minimum": "2",
              "maximum": "12",
              "default": "2"
            },
            "rules": [
              {
                "metricTrigger": {
                  "metricName": "MessageCount",
                  "metricNamespace": "",
                  "metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ServiceBus/namespaces/mySB/queues/myqueue",
                  "timeGrain": "PT5M",
                  "statistic": "Average",
                  "timeWindow": "PT5M",
                  "timeAggregation": "Average",
                  "operator": "GreaterThan",
                  "threshold": 10
                },
                "scaleAction": {
                  "direction": "Increase",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              },
              {
                "metricTrigger": {
                  "metricName": "MessageCount",
                  "metricNamespace": "",
                  "metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ServiceBus/namespaces/mySB/queues/myqueue",
                  "timeGrain": "PT5M",
                  "statistic": "Average",
                  "timeWindow": "PT5M",
                  "timeAggregation": "Average",
                  "operator": "LessThan",
                  "threshold": 3
                },
                "scaleAction": {
                  "direction": "Decrease",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              },
              {
                "metricTrigger": {
                  "metricName": "Percentage CPU",
                  "metricNamespace": "",
                  "metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.Compute/virtualMachineScaleSets/<this_vmss_name>",
                  "timeGrain": "PT5M",
                  "statistic": "Average",
                  "timeWindow": "PT30M",
                  "timeAggregation": "Average",
                  "operator": "GreaterThan",
                  "threshold": 85
                },
                "scaleAction": {
                  "direction": "Increase",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              },
              {
                "metricTrigger": {
                  "metricName": "Percentage CPU",
                  "metricNamespace": "",
                  "metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.Compute/virtualMachineScaleSets/<this_vmss_name>",
                  "timeGrain": "PT5M",
                  "statistic": "Average",
                  "timeWindow": "PT30M",
                  "timeAggregation": "Average",
                  "operator": "LessThan",
                  "threshold": 60
                },
                "scaleAction": {
                  "direction": "Decrease",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              }
            ]
          },
          {
            "name": "Weekday_Morning_Hours_Scale",
            "capacity": {
              "minimum": "4",
              "maximum": "12",
              "default": "4"
            },
            "rules": [],
            "recurrence": {
              "frequency": "Week",
              "schedule": {
                "timeZone": "Pacific Standard Time",
                "days": [
                  "Monday",
                  "Tuesday",
                  "Wednesday",
                  "Thursday",
                  "Friday"
                ],
                "hours": [
                  6
                ],
                "minutes": [
                  0
                ]
              }
            }
          },
          {
            "name": "Product_Launch_Day",
            "capacity": {
              "minimum": "6",
              "maximum": "20",
              "default": "6"
            },
            "rules": [],
            "fixedDate": {
              "timeZone": "Pacific Standard Time",
              "start": "2016-06-20T00:06:00Z",
              "end": "2016-06-21T23:59:00Z"
            }
          }
    ```
    <span data-ttu-id="3bff3-157">如需支援的欄位和其值，請參閱[自動調整 REST API 文件](https://msdn.microsoft.com/en-us/library/azure/dn931928.aspx)。</span><span class="sxs-lookup"><span data-stu-id="3bff3-157">For supported fields and their values, see [Autoscale REST API documentation](https://msdn.microsoft.com/en-us/library/azure/dn931928.aspx).</span></span> <span data-ttu-id="3bff3-158">現在您的自動調整規模設定包含先前所述的 hello 三個設定檔。</span><span class="sxs-lookup"><span data-stu-id="3bff3-158">Now your autoscale setting contains hello three profiles explained previously.</span></span>

7. <span data-ttu-id="3bff3-159">最後，看看 hello 自動調整規模**通知**> 一節。</span><span class="sxs-lookup"><span data-stu-id="3bff3-159">Finally, look at hello Autoscale **notification** section.</span></span> <span data-ttu-id="3bff3-160">自動調整規模通知讓您 toodo 三件事，向外延展時，或在動作已成功地在觸發。</span><span class="sxs-lookup"><span data-stu-id="3bff3-160">Autoscale notifications allow you toodo three things when a scale-out or in action is successfully triggered.</span></span>
   - <span data-ttu-id="3bff3-161">通知 hello 系統管理員和共同管理員的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="3bff3-161">Notify hello admin and co-admins of your subscription</span></span>
   - <span data-ttu-id="3bff3-162">傳送電子郵件給一組使用者</span><span class="sxs-lookup"><span data-stu-id="3bff3-162">Email a set of users</span></span>
   - <span data-ttu-id="3bff3-163">觸發 webhook 呼叫。</span><span class="sxs-lookup"><span data-stu-id="3bff3-163">Trigger a webhook call.</span></span> <span data-ttu-id="3bff3-164">當引發，此 webhook 傳送嗨自動調整條件的相關中繼資料和 hello 規模調整集合資源。</span><span class="sxs-lookup"><span data-stu-id="3bff3-164">When fired, this webhook sends metadata about hello autoscaling condition and hello scale set resource.</span></span> <span data-ttu-id="3bff3-165">請參閱詳細資料的自動調整規模 webhook hello 裝載 toolearn[設定 Webhook 和自動調整規模的電子郵件通知](insights-autoscale-to-webhook-email.md)。</span><span class="sxs-lookup"><span data-stu-id="3bff3-165">toolearn more about hello payload of autoscale webhook, see [Configure Webhook & Email Notifications for Autoscale](insights-autoscale-to-webhook-email.md).</span></span>

   <span data-ttu-id="3bff3-166">新增下列 toohello 自動調整規模設定取代 hello 您**通知**其值為 null 的項目</span><span class="sxs-lookup"><span data-stu-id="3bff3-166">Add hello following toohello Autoscale setting replacing your **notification** element whose value is null</span></span>

   ```
   "notifications": [
      {
        "operation": "Scale",
        "email": {
          "sendToSubscriptionAdministrator": true,
          "sendToSubscriptionCoAdministrators": false,
          "customEmails": [
              "user1@mycompany.com",
              "user2@mycompany.com"
              ]
        },
        "webhooks": [
          {
            "serviceUri": "https://foo.webhook.example.com?token=abcd1234",
            "properties": {
              "optional_key1": "optional_value1",
              "optional_key2": "optional_value2"
            }
          }
        ]
      }
    ]

   ```

   <span data-ttu-id="3bff3-167">叫用**放**資源總管 tooupdate hello 自動調整規模設定中的按鈕。</span><span class="sxs-lookup"><span data-stu-id="3bff3-167">Hit **Put** button in Resource Explorer tooupdate hello autoscale setting.</span></span>

<span data-ttu-id="3bff3-168">您已更新的自動調整規模設定 VM 規模調整集合 tooinclude 上的多個小數位數設定檔，並調整通知。</span><span class="sxs-lookup"><span data-stu-id="3bff3-168">You have updated an autoscale setting on a VM Scale set tooinclude multiple scale profiles and scale notifications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3bff3-169">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3bff3-169">Next Steps</span></span>
<span data-ttu-id="3bff3-170">使用這些連結 toolearn 深入了解自動調整。</span><span class="sxs-lookup"><span data-stu-id="3bff3-170">Use these links toolearn more about autoscaling.</span></span>

[<span data-ttu-id="3bff3-171">針對使用虛擬機器擴展集的自動調整進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="3bff3-171">TroubleShoot Autoscale with Virtual Machine Scale Sets</span></span>](../virtual-machine-scale-sets/virtual-machine-scale-sets-troubleshoot.md)

[<span data-ttu-id="3bff3-172">自動調整的常用計量</span><span class="sxs-lookup"><span data-stu-id="3bff3-172">Common Metrics for Autoscale</span></span>](insights-autoscale-common-metrics.md)

[<span data-ttu-id="3bff3-173">Azure 自動調整的最佳作法</span><span class="sxs-lookup"><span data-stu-id="3bff3-173">Best Practices for Azure Autoscale</span></span>](insights-autoscale-best-practices.md)

[<span data-ttu-id="3bff3-174">使用 PowerShell 管理自動調整</span><span class="sxs-lookup"><span data-stu-id="3bff3-174">Manage Autoscale using PowerShell</span></span>](insights-powershell-samples.md#create-and-manage-autoscale-settings)

[<span data-ttu-id="3bff3-175">使用 CLI 管理自動調整</span><span class="sxs-lookup"><span data-stu-id="3bff3-175">Manage Autoscale using CLI</span></span>](insights-cli-samples.md#autoscale)

[<span data-ttu-id="3bff3-176">針對自動調整設定 Webhook 與電子郵件通知</span><span class="sxs-lookup"><span data-stu-id="3bff3-176">Configure Webhook & Email Notifications for Autoscale</span></span>](insights-autoscale-to-webhook-email.md)
