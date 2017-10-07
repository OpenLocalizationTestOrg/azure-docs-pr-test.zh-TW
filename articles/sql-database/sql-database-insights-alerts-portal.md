---
title: "aaaUse SQL Database 的 Azure 入口網站 toocreate 警示 |Microsoft 文件"
description: "使用 hello Azure 入口網站 toocreate SQL Database 的警示，可以觸發通知或自動化您指定的 hello 條件符合時。"
author: aamalvea
manager: jhubbard
editor: 
services: sql-database
documentationcenter: 
ms.assetid: f7457655-ced6-4102-a9dd-7ddf2265c0e2
ms.service: sql-database
ms.custom: monitor and tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: aamalvea
ms.openlocfilehash: 4e494b130a26c4cdf42445cb49648fce9bf4d300
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-portal-toocreate-alerts-for-azure-sql-database-and-data-warehouse"></a>使用 Azure 入口網站 toocreate 警示的 Azure SQL Database 和資料倉儲

## <a name="overview"></a>概觀
本文章將示範如何使用 Azure SQL Database 和資料倉儲警示 tooset hello Azure 入口網站。 本文也提供設定警示期間的最佳做法。    

您可以收到以您 Azure 服務的監視計量或事件為基礎的警示。

* **度量值**-hello hello 值，指定的度量超出您在任一方向中指派的閾值時，警示觸發程序。 也就是說，它會觸發兩者當第一次符合 hello 條件，並且再之後時，條件不再達成。    
* **活動記錄檔事件** - 警示可觸發*每一個*事件，或是僅在發生特定事件數目時才觸發。

您可以設定警示 toodo hello，下列情況觸發：

* 傳送電子郵件通知 toohello 服務管理員和共同管理員
* 您指定的 tooadditional 電子郵件傳送電子郵件。
* 呼叫 webhook

您可以透過下列方式設定和取得有關警示規則的資訊

* [Azure 入口網站](../monitoring-and-diagnostics/insights-alerts-portal.md)
* [PowerShell](../monitoring-and-diagnostics/insights-alerts-powershell.md)
* [命令列介面 (CLI)](../monitoring-and-diagnostics/insights-alerts-command-line-interface.md)
* [Azure 監視器 REST API](https://msdn.microsoft.com/library/azure/dn931945.aspx)

## <a name="create-an-alert-rule-on-a-metric-with-hello-azure-portal"></a>建立警示規則上 hello Azure 入口網站的度量
1. 在 hello[入口網站](https://portal.azure.com/)，找出您感興趣監視 hello 資源並加以選取。
2. SQL DB 和彈性集區的此這個步驟與 SQL DW 不相同： 

   - **SQL 資料庫 （& s) 只彈性集區**： 選取**警示**或**警示規則**hello [監視] 區段底下。 hello 文字和圖示可能各不相同稍有不同的資源。  
   
     ![監視](../monitoring-and-diagnostics/media/insights-alerts-portal/AlertRulesButton.png)
  
   - **只有 SQL DW**： 選取**監視**下 hello 一般工作 > 一節。 按一下 hello **DWU 使用量**圖形。

     ![一般工作](../monitoring-and-diagnostics/media/insights-alerts-portal/AlertRulesButtonDW.png)

3. 選取 hello**新增警示**命令，並填寫 hello 欄位。
   
    ![新增警示](../monitoring-and-diagnostics/media/insights-alerts-portal/AddDBAlertPage.png)
4. 為您的警示規則命名 ([名稱])，選擇將會顯示在電子郵件通知中的 [描述]。
5. 選取 hello**度量**toomonitor，然後選擇 **條件**和**閾值**hello 公制值。 同時選擇 hello**期間**的 hello 度量的時間必須符合規則之前 hello 警示觸發程序。 例如，如果您使用 hello 期間 」 PT5M 」 警示會尋找 CPU 高於 80%，hello 警示時，觸發 hello CPU 已經一致上述 80 %5 分鐘。 一旦發生 hello 第一個觸發程序，一次觸發時 hello CPU 會保持低於 80 %5 分鐘。 hello CPU 度量，就會發生每隔 1 分鐘。   
6. 請檢查**電子郵件擁有者...**如果您想要以電子郵件傳送的系統管理員和共同管理員 toobe 當 hello 引發警示。
7. 如果您想要其他的電子郵件 tooreceive 通知時 hello 警示引發，增益 hello**其他的系統管理員 email(s)**欄位。 以分號分隔多個電子郵件 - *email@contoso.com;email2@contoso.com*
8. 將放在有效的 URI，在 hello **Webhook**欄位若要呼叫它時 hello 引發警示。
9. 選取**確定**時完成的 toocreate hello 警示。   

在幾分鐘的時間內 hello 警示為作用中，且觸發程序，如先前所述。

## <a name="managing-your-alerts"></a>管理警示
一旦建立警示，您可以選取警示，並且︰

* 檢視圖表顯示 hello 度量的閾值，從 hello 的 hello 實際值的前一天。
* 編輯或刪除警示。
* **停用**或**啟用**它，如果您想要 tootemporarily 停止或繼續接收該警示的通知。


## <a name="sql-database-alert-values"></a>SQL Database 警示值

| 資源類型 | 度量名稱 | 易記名稱 | 彙總類型 | 警示時間間隔下限|
| --- | --- | --- | --- | --- |
| SQL Database | cpu_percent | CPU 百分比 | 平均值 | 5 分鐘 |
| SQL Database | physical_data_read_percent | 資料 IO 百分比 | 平均值 | 5 分鐘 |
| SQL Database | log_write_percent | 記錄 IO 百分比 | 平均值 | 5 分鐘 |
| SQL Database | dtu_consumption_percent | DTU 百分比 | 平均值 | 5 分鐘 |
| SQL Database | 儲存體 | 資料庫大小總計 | 最大值 | 30 分鐘 |
| SQL Database | connection_successful | 成功的連線 | 總計 | 10 分鐘 |
| SQL Database | connection_failed | 失敗的連線 | 總計 | 10 分鐘 |
| SQL Database | blocked_by_firewall | 遭到防火牆封鎖 | 總計 | 10 分鐘 |
| SQL Database | 死結 | 死結 | 總計 | 10 分鐘 |
| SQL Database | storage_percent | 資料庫大小百分比 | 最大值 | 30 分鐘 |
| SQL Database | xtp_storage_percent | 記憶體中 OLTP 儲存體百分比 (預覽) | 平均值 | 5 分鐘 |
| SQL Database | workers_percent | 背景工作角色百分比 | 平均值 | 5 分鐘 |
| SQL Database | sessions_percent | 工作階段百分比 | 平均值 | 5 分鐘 |
| SQL Database | dtu_limit | DTU 限制 | 平均值 | 5 分鐘 |
| SQL Database | dtu_used | 已使用 DTU | 平均值 | 5 分鐘 |
||||||
| 彈性集區 | cpu_percent | CPU 百分比 | 平均值 | 10 分鐘 |
| 彈性集區 | physical_data_read_percent | 資料 IO 百分比 | 平均值 | 10 分鐘 |
| 彈性集區 | log_write_percent | 記錄 IO 百分比 | 平均值 | 10 分鐘 |
| 彈性集區 | dtu_consumption_percent | DTU 百分比 | 平均值 | 10 分鐘 |
| 彈性集區 | storage_percent | 儲存體百分比 | 平均值 | 10 分鐘 |
| 彈性集區 | workers_percent | 背景工作角色百分比 | 平均值 | 10 分鐘 |
| 彈性集區 | eDTU_limit | eDTU 限制 | 平均值 | 10 分鐘 |
| 彈性集區 | storage_limit | 儲存體限制 | 平均值 | 10 分鐘 |
| 彈性集區 | eDTU_used | 已使用 eDTU | 平均值 | 10 分鐘 |
| 彈性集區 | storage_used | 已使用儲存體 | 平均值 | 10 分鐘 |
||||||               
| SQL 資料倉儲 | cpu_percent | CPU 百分比 | 平均值 | 10 分鐘 |
| SQL 資料倉儲 | physical_data_read_percent | 資料 IO 百分比 | 平均值 | 10 分鐘 |
| SQL 資料倉儲 | 儲存體 | 資料庫大小總計 | 最大值 | 10 分鐘 |
| SQL 資料倉儲 | connection_successful | 成功的連線 | 總計 | 10 分鐘 |
| SQL 資料倉儲 | connection_failed | 失敗的連線 | 總計 | 10 分鐘 |
| SQL 資料倉儲 | blocked_by_firewall | 遭到防火牆封鎖 | 總計 | 10 分鐘 |
| SQL 資料倉儲 | service_level_objective | Hello 資料庫的服務等級目標 | 總計 | 10 分鐘 |
| SQL 資料倉儲 | dwu_limit | dwu 限制 | 最大值 | 10 分鐘 |
| SQL 資料倉儲 | dwu_consumption_percent | DWU 百分比 | 平均值 | 10 分鐘 |
| SQL 資料倉儲 | dwu_used | 已使用 DWU | 平均值 | 10 分鐘 |
||||||


## <a name="next-steps"></a>後續步驟
* [取得的 Azure 監視概觀](../monitoring-and-diagnostics/monitoring-overview.md)包括 hello 類型的資訊，您可以收集和監視。
* 深入了解 [在警示中設定 webhook](../monitoring-and-diagnostics/insights-webhooks-alerts.md)。
* 依照 [診斷記錄檔概觀](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) 中的做法，收集您服務中詳細的高頻率計量。
* 取得[概觀度量收集](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md)toomake 確定您的服務可用，並能繼續回應。
