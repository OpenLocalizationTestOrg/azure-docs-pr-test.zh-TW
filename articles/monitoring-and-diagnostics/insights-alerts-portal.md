---
title: "Azure 服務-aaaCreate 警示 Azure 入口網站 |Microsoft 文件"
description: "符合您指定的 hello 條件時，觸發程序的電子郵件，通知，便會呼叫網站 Url (webhook) 或自動化。"
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: f7457655-ced6-4102-a9dd-7ddf2265c0e2
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/23/2016
ms.author: robb
ms.openlocfilehash: 78d862d25255cda9fdfe347329e908a471c39846
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---azure-portal"></a>在 Azure 監視器中為 Azure 服務建立計量警示 - Azure 入口網站
> [!div class="op_single_selector"]
> * [入口網站](insights-alerts-portal.md)
> * [PowerShell](insights-alerts-powershell.md)
> * [CLI](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a>概觀
本文章將示範如何使用 Azure 的度量警示 tooset hello Azure 入口網站。   

您可以收到以您 Azure 服務的監視計量或事件為基礎的警示。

* **度量值**-hello hello 值，指定的度量超出您在任一方向中指派的閾值時，警示觸發程序。 也就是說，它會觸發兩者當第一次符合 hello 條件，並且再之後時，條件不再達成。    
* **活動記錄檔事件** - 警示可在*每一個*事件上觸發，或是僅在發生特定事件時才觸發。 深入了解活動記錄檔警示 toolearn[按一下這裡](monitoring-activity-log-alerts.md)

您可以設定警示的度量 toodo hello 時，下列觸發：

* 傳送電子郵件通知 toohello 服務管理員和共同管理員
* 您指定的 tooadditional 電子郵件傳送電子郵件。
* 呼叫 webhook
* 開始執行的 Azure runbook （只能從 hello Azure 入口網站)

您可以透過下列方式設定和取得有關計量警示規則的資訊

* [Azure 入口網站](insights-alerts-portal.md)
* [PowerShell](insights-alerts-powershell.md)
* [命令列介面 (CLI)](insights-alerts-command-line-interface.md)
* [Azure 監視器 REST API](https://msdn.microsoft.com/library/azure/dn931945.aspx)

## <a name="create-an-alert-rule-on-a-metric-with-hello-azure-portal"></a>建立警示規則上 hello Azure 入口網站的度量
1. 在 hello[入口網站](https://portal.azure.com/)，找出您感興趣監視 hello 資源並加以選取。

2. 選取**警示**或**警示規則**hello [監視] 區段底下。 hello 文字和圖示可能各不相同稍有不同的資源。  

    ![監視](./media/insights-alerts-portal/AlertRulesButton.png)

3. 選取 hello**新增警示**命令，並填寫 hello 欄位。

    ![新增警示](./media/insights-alerts-portal/AddAlertOnlyParamsPage.png)

4. 為您的警示規則命名 ([名稱])，選擇將會顯示在電子郵件通知中的 [描述]。

5. 選取 hello**度量**toomonitor，然後選擇 **條件**和**閾值**hello 公制值。 同時選擇 hello**期間**的 hello 度量的時間必須符合規則之前 hello 警示觸發程序。 例如，如果您使用 hello 期間 」 PT5M 」 警示會尋找 CPU 高於 80%，hello 警示時，觸發 hello CPU 已經一致上述 80 %5 分鐘。 一旦發生 hello 第一個觸發程序，一次觸發時 hello CPU 會保持低於 80 %5 分鐘。 hello CPU 度量，就會發生每隔 1 分鐘。   

6. 請檢查**電子郵件擁有者...**如果您想要以電子郵件傳送的系統管理員和共同管理員 toobe 當 hello 引發警示。

7. 如果您想要其他的電子郵件 tooreceive 通知時 hello 警示引發，增益 hello**其他的系統管理員 email(s)**欄位。 以分號分隔多個電子郵件 - *email@contoso.com;email2@contoso.com*

8. 將放在有效的 URI，在 hello **Webhook**欄位若要呼叫它時 hello 引發警示。

9. 如果您使用 Azure 自動化，您可以選取 Runbook toobe hello 警示觸發時執行。

10. 選取**確定**時完成的 toocreate hello 警示。   

在幾分鐘的時間內 hello 警示為作用中，且觸發程序，如先前所述。

## <a name="managing-your-alerts"></a>管理警示
一旦建立警示，您可以選取警示，並且︰

* 檢視圖表顯示 hello 度量的閾值，從 hello 的 hello 實際值的前一天。
* 編輯或刪除警示。
* **停用**或**啟用**它，如果您想要 tootemporarily 停止或繼續接收該警示的通知。

## <a name="next-steps"></a>後續步驟
* [取得的 Azure 監視概觀](monitoring-overview.md)包括 hello 類型的資訊，您可以收集和監視。
* 深入了解 [在警示中設定 webhook](insights-webhooks-alerts.md)。
* 深入了解[在活動記錄檔事件上設定警示](monitoring-activity-log-alerts.md)。
* 深入了解 [Azure 自動化 Runbook](../automation/automation-starting-a-runbook.md)。
* 依照 [診斷記錄檔概觀](monitoring-overview-of-diagnostic-logs.md) 中的做法，收集您服務中詳細的高頻率計量。
* 取得[概觀度量收集](insights-how-to-customize-monitoring.md)toomake 確定您的服務可用，並能繼續回應。
