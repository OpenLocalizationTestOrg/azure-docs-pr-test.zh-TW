---
title: "Azure 服務-PowerShell aaaCreate 警示 |Microsoft 文件"
description: "符合您指定的 hello 條件時，觸發程序的電子郵件，通知，便會呼叫網站 Url (webhook) 或自動化。"
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d26ab15b-7b7e-42a9-81c8-3ce9ead5d252
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/20/2016
ms.author: robb
ms.openlocfilehash: 80d3a3f194fc6a5a09a81d04206ea7a1640bddb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---powershell"></a>在 Azure 監視器中為 Azure 服務建立計量警示 - PowerShell
> [!div class="op_single_selector"]
> * [入口網站](insights-alerts-portal.md)
> * [PowerShell](insights-alerts-powershell.md)
> * [CLI](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a>概觀
本文將說明如何註冊 Azure 度量 tooset 警示使用 PowerShell。  

您可以收到以您 Azure 服務的監視計量或事件為基礎的警示。

* **度量值**-hello hello 值，指定的度量超出您在任一方向中指派的閾值時，警示觸發程序。 也就是說，它會觸發兩者當第一次符合 hello 條件，並且再之後時，條件不再達成。    
* **活動記錄檔事件** - 警示可在*每一個*事件上觸發，或是僅在發生特定事件時才觸發。 深入了解活動記錄檔警示 toolearn[按一下這裡](monitoring-activity-log-alerts.md)

您可以設定警示的度量 toodo hello 時，下列觸發：

* 傳送電子郵件通知 toohello 服務管理員和共同管理員
* 您指定的 tooadditional 電子郵件傳送電子郵件。
* 呼叫 webhook
* 開始執行的 Azure runbook （只能從 hello Azure 入口網站)

您可以透過下列方式設定和取得有關警示規則的資訊

* [Azure 入口網站](insights-alerts-portal.md)
* [PowerShell](insights-alerts-powershell.md)
* [命令列介面 (CLI)](insights-alerts-command-line-interface.md)
* [Azure 監視器 REST API](https://msdn.microsoft.com/library/azure/dn931945.aspx)

如需詳細資訊，您可以一律輸入```Get-Help```，然後 hello 您想要說明的 PowerShell 命令。

## <a name="create-alert-rules-in-powershell"></a>在 PowerShell 中建立警示規則
1. 登入 tooAzure。   

    ```PowerShell
    Login-AzureRmAccount

    ```
2. 取得清單的 hello 訂閱您可以使用。 請確認您使用與 hello 右訂用帳戶。 如果沒有，請將它設定 toohello 右移一個使用 hello 輸出`Get-AzureRmSubscription`。

    ```PowerShell
    Get-AzureRmSubscription
    Get-AzureRmContext
    Set-AzureRmContext -SubscriptionId <subscriptionid>
    ```
3. 在資源群組中，下列命令使用 hello toolist 現有規則：

   ```PowerShell
   Get-AzureRmAlertRule -ResourceGroup <myresourcegroup> -DetailedOutput
   ```
4. toocreate 規則，您需要 toohave 數個重要的資訊片段第一次。

  * hello**資源識別碼**hello 資源要 tooset 的警示
  * hello**度量定義**可用於該項資源

     其中一種方式 tooget hello 資源識別碼為 toouse hello Azure 入口網站。 假設已經建立 hello 資源時，在 hello 入口網站中選取它。 然後在 [hello 下一步] 刀鋒視窗中，選取*屬性*下 hello*設定*> 一節。 **資源識別碼**是在 hello 下一步 刀鋒視窗中的欄位。 另一種方式為 toouse hello [Azure 資源總管](https://resources.azure.com/)。

     以下是 Web 應用程式的範例資源識別碼：

     ```
     /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename
     ```

     您可以使用`Get-AzureRmMetricDefinition`tooview hello 清單的特定資源的所有標準定義。

     ```PowerShell
     Get-AzureRmMetricDefinition -ResourceId <resource_id>
     ```

     hello 下列範例會產生包含 hello 度量名稱的資料表和 hello 單位，該度量。

     ```PowerShell
     Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit

     ```
     執行 Get-MetricDefinitions 可取得 Get-AzureRmMetricDefinition 的可用選項完整清單。
5. 下列範例設定警示的網站資源上的 hello。 hello 警示觸發程序每當它以一致的方式接收任何流量 5 分鐘，一次當它收到沒有流量 5 分鐘。

    ```PowerShell
    Add-AzureRmMetricAlertRule -Name myMetricRuleWithWebhookAndEmail -Location "East US" -ResourceGroup myresourcegroup -TargetResourceId /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename -MetricName "BytesReceived" -Operator GreaterThan -Threshold 2 -WindowSize 00:05:00 -TimeAggregationOperator Total -Description "alert on any website activity"

    ```
6. toocreate webhook 或傳送電子郵件時警示觸發時，會先建立 hello 電子郵件和/或 webhook。 立即建立 hello 規則之後 hello-動作標記和 hello 下列範例所示。 您無法透過 PowerShell 將 webhook 或電子郵件與已建立的規則建立關聯。

    ```PowerShell
    $actionEmail = New-AzureRmAlertRuleEmail -CustomEmail myname@company.com
    $actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri https://www.contoso.com?token=mytoken

    Add-AzureRmMetricAlertRule -Name myMetricRuleWithWebhookAndEmail -Location "East US" -ResourceGroup myresourcegroup -TargetResourceId /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename -MetricName "BytesReceived" -Operator GreaterThan -Threshold 2 -WindowSize 00:05:00 -TimeAggregationOperator Total -Actions $actionEmail, $actionWebhook -Description "alert on any website activity"
    ```

7. tooverify 警示有已正確建立藉由查看 hello 個別規則。

    ```PowerShell
    Get-AzureRmAlertRule -Name myMetricRuleWithWebhookAndEmail -ResourceGroup myresourcegroup -DetailedOutput

    Get-AzureRmAlertRule -Name myLogAlertRule -ResourceGroup myresourcegroup -DetailedOutput
    ```
8. 刪除您的警示。 這些命令會刪除先前建立本文章中的 hello 規則。

    ```PowerShell
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myrule
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myMetricRuleWithWebhookAndEmail
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myLogAlertRule
    ```

## <a name="next-steps"></a>後續步驟
* [取得的 Azure 監視概觀](monitoring-overview.md)包括 hello 類型的資訊，您可以收集和監視。
* 深入了解 [在警示中設定 webhook](insights-webhooks-alerts.md)。
* 深入了解[在活動記錄檔事件上設定警示](monitoring-activity-log-alerts.md)。
* 深入了解 [Azure 自動化 Runbook](../automation/automation-starting-a-runbook.md)。
* 取得[收集診斷記錄檔的概觀](monitoring-overview-of-diagnostic-logs.md)toocollect 詳細高頻率度量，您的服務。
* 取得[概觀度量收集](insights-how-to-customize-monitoring.md)toomake 確定您的服務可用，並能繼續回應。
