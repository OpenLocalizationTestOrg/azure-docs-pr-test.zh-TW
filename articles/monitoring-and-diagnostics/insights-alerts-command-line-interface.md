---
title: "Azure 服務的跨平台 CLI aaaCreate 警示 |Microsoft 文件"
description: "符合您指定的 hello 條件時，觸發程序的電子郵件，通知，便會呼叫網站 Url (webhook) 或自動化。"
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 5c6a2d27-7dcc-4f89-8752-9bb31b05ff35
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: robb
ms.openlocfilehash: e53701e5377a415038a69fbd32f1e5fc5fe99be9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---cross-platform-cli"></a>在 Azure 監視器中為 Azure 服務建立計量警示 - 跨平台 CLI
> [!div class="op_single_selector"]
> * [入口網站](insights-alerts-portal.md)
> * [PowerShell](insights-alerts-powershell.md)
> * [CLI](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a>概觀
本文章將示範如何使用 Azure 的度量警示 tooset hello 跨平台命令列介面 (CLI)。

> [!NOTE]
> Azure 的監視是 hello 所謂 「 Azure Insights"的新名稱，直到 2016 年 9 月 25 日。 不過，hello 命名空間，因此下列 hello 命令仍包含 hello"見解"。
>
>

您可以收到以您 Azure 服務的監視計量或事件為基礎的警示。

* **度量值**-hello hello 值，指定的度量超出您在任一方向中指派的閾值時，警示觸發程序。 也就是說，它會觸發兩者當第一次符合 hello 條件，並且再之後時，條件不再達成。    
* **活動記錄檔事件** - 警示可在*每一個*事件上觸發，或是僅在發生特定事件時才觸發。 深入了解活動記錄檔警示 toolearn[按一下這裡](monitoring-activity-log-alerts.md)

您可以設定警示的度量 toodo hello 時，下列觸發：

* 傳送電子郵件通知 toohello 服務管理員和共同管理員
* 您指定的 tooadditional 電子郵件傳送電子郵件。
* 呼叫 webhook
* 開始執行的 Azure runbook （只能從 hello Azure 入口網站在此階段)

您可以透過下列方式設定和取得有關計量警示規則的資訊

* [Azure 入口網站](insights-alerts-portal.md)
* [PowerShell](insights-alerts-powershell.md)
* [命令列介面 (CLI)](insights-alerts-command-line-interface.md)
* [Azure 監視器 REST API](https://msdn.microsoft.com/library/azure/dn931945.aspx)

您一律可以收到的命令說明輸入命令，並將-協助 hello 結尾。 例如：

    ```console
    azure insights alerts -help
    azure insights alerts actions email create -help
    ```

## <a name="create-alert-rules-using-hello-cli"></a>建立使用 hello CLI 的警示規則
1. 執行 hello 必要條件和登入 tooAzure。 請參閱 [Azure 監視器 CLI 範例](insights-cli-samples.md)。 簡單地說，安裝 hello CLI，並執行下列命令。 它們可以獲得您登入，顯示您正在使用，並讓您準備 toorun Azure 監視器命令什麼訂用帳戶。

    ```console
    azure login
    azure account show
    azure config mode arm

    ```

2. toolist 現有規則上的資源群組中，使用下列格式的 hello**警示規則清單的 azure insights** *[選項] &lt;resourceGroup&gt;*

   ```console
   azure insights alerts rule list myresourcegroupname

   ```
3. toocreate 規則，您需要 toohave 數個重要的資訊片段第一次。
  * hello**資源識別碼**hello 資源要 tooset 的警示
  * hello**度量定義**可用於該項資源

     其中一種方式 tooget hello 資源識別碼為 toouse hello Azure 入口網站。 假設已經建立 hello 資源時，在 hello 入口網站中選取它。 然後在 [hello 下一步] 刀鋒視窗中，選取*屬性*下 hello*設定*> 一節。 hello*資源識別碼*是在 hello 下一步 刀鋒視窗中的欄位。 另一種方式為 toouse hello [Azure 資源總管](https://resources.azure.com/)。

     以下是 Web 應用程式的範例資源識別碼：

     ```console
     /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename
     ```

     tooget hello 可用的度量和 hello 上述資源範例中，使用下列 CLI 命令的 hello 這些度量單位的清單：  

     ```console
     azure insights metrics list /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename PT1M
     ```

     *PT1M*是 hello 資料粒度的 hello 可用度量 （每隔 1 分鐘）。 使用不同的資料粒度可提供您不同的計量選項。
4. toocreate 標準為基礎的警示規則，使用下列形式的 hello 的命令：

    **azure insights alerts rule metric set** *[options] &lt;ruleName&gt; &lt;location&gt; &lt;resourceGroup&gt; &lt;windowSize&gt; &lt;operator&gt; &lt;threshold&gt; &lt;targetResourceId&gt; &lt;metricName&gt; &lt;timeAggregationOperator&gt;*

    下列範例設定警示的網站資源上的 hello。 hello 警示觸發程序每當它以一致的方式接收任何流量 5 分鐘，一次當它收到沒有流量 5 分鐘。

    ```console
    azure insights alerts rule metric set myrule eastus myreasourcegroup PT5M GreaterThan 2 /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename BytesReceived Total

    ```
5. toocreate webhook 或傳送電子郵件時度量的警示引發時，會先建立 hello 電子郵件和/或 webhook。 然後立即建立 hello 規則之後。 您無法將 webhook 或電子郵件與已建立使用 hello CLI 規則。

    ```console
    azure insights alerts actions email create --customEmails myemail@contoso.com

    azure insights alerts actions webhook create https://www.contoso.com

    azure insights alerts rule metric set myrulewithwebhookandemail eastus myreasourcegroup PT5M GreaterThan 2 /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename BytesReceived Total
    ```

6. 您可以藉由查看個別規則來確認您的警示已正確建立。

    ```console
    azure insights alerts rule list myresourcegroup --ruleName myrule
    ```
7. toodelete 規則使用 hello 格式的命令：

    **insights alerts rule delete** [options] &lt;resourceGroup&gt; &lt;ruleName&gt;

    這些命令會刪除先前建立的這篇文章中的 hello 規則。

    ```console
    azure insights alerts rule delete myresourcegroup myrule
    azure insights alerts rule delete myresourcegroup myrulewithwebhookandemail
    azure insights alerts rule delete myresourcegroup myActivityLogRule
    ```

## <a name="next-steps"></a>後續步驟
* [取得的 Azure 監視概觀](monitoring-overview.md)包括 hello 類型的資訊，您可以收集和監視。
* 深入了解 [在警示中設定 webhook](insights-webhooks-alerts.md)。
* 深入了解[在活動記錄檔事件上設定警示](monitoring-activity-log-alerts.md)。
* 深入了解 [Azure 自動化 Runbook](../automation/automation-starting-a-runbook.md)。
* 取得[收集診斷記錄檔的概觀](monitoring-overview-of-diagnostic-logs.md)toocollect 詳細高頻率度量，您的服務。
* 取得[概觀度量收集](insights-how-to-customize-monitoring.md)toomake 確定您的服務可用，並能繼續回應。
