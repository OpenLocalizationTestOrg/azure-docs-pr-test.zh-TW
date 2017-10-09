---
title: "aaaRestore Azure SQL database 中的多租用戶應用程式 |Microsoft 文件"
description: "了解如何 toorestore 單一租用戶 SQL 資料庫不小心刪除的資料之後"
keywords: SQL Database Azure
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: billgib;sstein
ms.openlocfilehash: 8507ecec2424c135f1859b88ebf2bb4e17538a58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="restore-a-wingtip-saas-tenants-sql-database"></a>還原 Wingtip SaaS 租用戶 SQL 資料庫

hello Wingtip SaaS 應用程式是使用每個租用戶的資料庫模型，其中每個租用戶都有各自的資料庫所建立。 其中一個 hello 這個模型的優點是它是簡單 toorestore 單一租用戶隔離，而不會影響其他租用戶中的資料。

在本教學課程中，您將了解兩個資料復原模式：

> [!div class="checklist"]

> * 將資料庫還原到平行資料庫 (並存)
> * 就地還原資料庫


|||
|:--|:--|
| **還原時間，租用戶 tooa 先前點到平行資料庫** | 檢閱、 稽核、 相容性 hello 租用戶可以使用此模式，等 hello 原始資料庫仍在線上且不變。 |
| **就地還原租用戶** | 此模式相當常用的 toorecover 租用戶 tooa 先前點在租用戶不小心刪除的資料之後的時間。 hello 原始資料庫是離線，以及取代 hello 還原的資料庫。 |
|||

toocomplete 完成本教學課程，請確定 hello 下列必要條件：

* hello Wingtip SaaS 應用程式部署。 toodeploy 在五分鐘內，請參閱[部署及瀏覽 hello Wingtip SaaS 應用程式](sql-database-saas-tutorial.md)
* 已安裝 Azure PowerShell。 如需詳細資料，請參閱[開始使用 Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)

## <a name="introduction-toohello-saas-tenant-restore-pattern"></a>簡介 toohello SaaS 租用戶還原模式

Hello 租用戶還原模式，有兩個簡單的模式還原個別租用戶的資料。 由於租用戶資料庫彼此互相隔離，因此還原一個租用戶並不會影響到任何其他租用戶的資料。

在 hello 第一個模式中，會將資料還原到新的資料庫。 hello 租用戶將會授與存取 toothis 資料庫連同其實際執行資料。 此模式可讓租用戶系統管理員 tooreview hello 還原資料，且有可能利用 tooselectively 覆寫目前的資料值。 它是最多 toohello SaaS 應用程式設計師 toodetermine 多麼複雜 hello 選項應該是資料復原。 只要正在 hello 的狀態，在特定時點的時間可以 tooreview 資料可能只需要在某些情況下。 如果 hello 資料庫使用[地理複寫](sql-database-geo-replication-overview.md)，我們建議您所需的 hello 資料複製到 hello 原始資料庫的 hello 還原複本。 如果您取代 hello 原始資料庫與 hello 還原資料庫時，您會需要 tooreconfigure，並重新同步處理地理複寫。

Hello 租用戶的實際執行資料庫還原在 hello 第二個模式中，假設該 hello 租用戶發生遺失或損毀的資料，tooa 先前時間點。 在 hello 還原中的位置模式中，hello 租用戶會離線短暫時還原並上線 hello 資料庫。 hello 原始資料庫已刪除，但仍可還原從如果您需要 toogo 後 tooan 更早的時間點。 此模式的一種變化無法重新命名 hello 資料庫，而不刪除，雖然重新命名的 hello 資料庫提供不了任何其他的優勢，根據資料安全性。

## <a name="get-hello-wingtip-application-scripts"></a>取得 hello Wingtip 應用程式指令碼

hello Wingtip SaaS 指令碼和應用程式的原始程式碼中可用 hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github 儲存機制。 [步驟 toodownload hello Wingtip SaaS 指令碼](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts)。

## <a name="simulate-a-tenant-accidentally-deleting-data"></a>模擬租用戶不小心刪除資料的情況

toodemonstrate 這些復原案例中，我們需要太*意外*刪除其中一個 hello 租用戶資料庫中的部分資料。 您可以刪除任何記錄，而參考完整性違規取得封鎖 hello 下一個步驟設定 hello 示範 toonot ！ 它也會加入您可以使用某些票證採購資料稍後 hello *Wingtip SaaS 分析教學課程*。

執行 hello 票證產生器的指令碼並建立其他資料。 刻意 hello 票證產生器不會購買的每個租用戶最後一個事件的票證。

1. 開啟...\\學習模組\\公用程式\\*示範 TicketGenerator.ps1*在 hello *PowerShell ISE*
1. 按**F5** toorun hello 指令碼和產生客戶和票證銷售資料。


### <a name="open-hello-events-app-tooreview-hello-current-events"></a>開啟 hello 事件應用程式 tooreview hello 目前事件

1. 開啟 hello*事件中樞*(http://events.wtp。&lt;使用者&gt;。 trafficmanager.net) 按一下**Contoso 搭配 Hall**:

   ![事件中樞](media/sql-database-saas-tutorial-restore-single-tenant/events-hub.png)

1. 捲動 hello 事件清單，並記下 hello 最後一個事件 hello 清單中：

   ![最後一個事件](media/sql-database-saas-tutorial-restore-single-tenant/last-event.png)


### <a name="run-hello-demo-scenario-tooaccidentally-delete-hello-last-event"></a>執行 hello 示範案例 tooaccidentally delete hello 最後一個事件

1. 開啟...\\學習模組\\業務續航力和災害復原\\RestoreTenant\\*示範 RestoreTenant.ps1*在 hello *PowerShell ISE*，並設定 hello 下列值：
   * **$DemoScenario** = **1**，太將**1** -刪除沒有任何票證銷售的事件。
1. 按**F5** toorun hello 指令碼，並刪除 hello 最後一個事件。 您應該會看到確認訊息類似 toohello 下列：

   ```Console
   Deleting unsold events from Contoso Concert Hall ...
   Deleted event 'Seriously Strauss' from Contoso Concert Hall venue.
   ```

1. hello Contoso 事件頁面隨即開啟。 向下捲動並確認 hello 事件就會消失。 如果 hello 事件仍在 hello 清單中，按一下 重新整理，並確認它消失。

   ![最後一個事件](media/sql-database-saas-tutorial-restore-single-tenant/last-event-deleted.png)


## <a name="restore-a-tenant-database-in-parallel-with-hello-production-database"></a>還原租用戶資料庫與 hello 生產資料庫並行

這個練習還原 hello Contoso 搭配 Hall database tooa 點之前已刪除 hello 事件的時間。 在 hello 先前步驟中刪除 hello 事件之後，您會想 toorecover，並查看 hello 刪除資料。 您不需要 toorestore 與 hello 刪除記錄，在生產資料庫，但您需要針對其他商業用途的 toorecover hello 舊資料庫 tooaccess hello 舊資料。

 hello*還原 TenantInParallel.ps1*指令碼會建立平行的租用戶資料庫，以及平行類別目錄項目這兩個名為*ContosoConcertHall\_舊*。 此復原模式最適用於從較不嚴重的資料遺失進行復原，或用於合規性和稽核復原案例。 它也是建議的方法，當您使用的 hello[地理複寫](sql-database-geo-replication-overview.md)。

1. 完整的 hello[模擬使用者不小心刪除資料](#simulate-a-tenant-accidentally-deleting-data)> 一節。
1. 開啟...\\學習模組\\業務續航力和災害復原\\RestoreTenant\\_示範 RestoreTenant.ps1_在 hello *PowerShell ISE*.
1. 設定**$DemoScenario** = **2**，設定得**2**太*還原租用戶，以平行方式*。
1. 按**F5** toorun hello 指令碼。

hello 指令碼還原 hello 租用戶資料庫 （tooa 平行資料庫） tooa 點刪除 hello 前一節中的 hello 事件之前的時間。 它會建立第二個資料庫，移除任何現有的目錄中繼資料存在於此資料庫，並將 hello 資料庫 toohello 目錄下 hello *ContosoConcertHall\_舊*項目。

hello 的示範指令碼會在您的瀏覽器中開啟 hello 事件頁面。 請注意，從 hello URL:```http://events.wtp.&lt;user&gt;.trafficmanager.net/contosoconcerthall_old```這會顯示 hello 還原資料庫中的資料其中*_old*加入 toohello 名稱。

已還原捲動 hello 事件列在 hello 瀏覽器 tooconfirm hello 刪除 hello 前一節中的事件。

請注意該公開 hello 還原租用戶，因為與它自己的事件的應用程式 toobrowse 票證的其他租用戶不太可能 toobe 會提供租用戶存取 toorestored 資料，但可做 tooeasily 說明 hello 還原模式的方式。

事實上，您可能只會依據一段定義的期間保留這個已還原的資料庫。 您可以刪除 hello 還原租用戶項目，當您已完成後，由呼叫 hello*移除 RestoredTenant.ps1*指令碼。

1. 設定**$DemoScenario**太**4** tooselect hello*還原移除租用戶*案例。
1. **使用** **F5** 來**執行**
1. hello *ContosoConcertHall\_舊*從 hello 類別目錄現在刪除項目。 請繼續並關閉您的瀏覽器中的此租用戶的 hello 事件頁面。


## <a name="restore-a-tenant-in-place-replacing-hello-existing-tenant-database"></a>還原租用戶的位置，以取代 hello 現有租用戶資料庫

這個練習還原 hello Contoso 搭配 Hall 租用戶 tooa 點之前已刪除 hello 事件的時間。 hello*還原 TenantInPlace*指令碼還原 hello 目前租用戶資料庫 tooa 新資料庫指向 tooa 前一個點的時間，並刪除 hello 原始資料庫。 從嚴重的資料損毀復原，因為可能會有重大資料遺失的 hello 租用戶會有 tooaccommodate，最適合這種模式的還原。

1. 在 PowerShell ISE 中開啟 **Demo-RestoreTenant.ps1** 檔案
1. 設定**$DemoScenario**太**5** tooselect hello*還原位置的案例中的租用戶*。
1. 使用 **F5** 來執行。

hello 指令碼會還原 hello 租用戶資料庫 tooa 點五分鐘的時間才能 hello 事件已刪除。 其做法是先採取 hello Contoso 搭配 Hall 離線因此沒有其他進一步的租用戶更新 toohello 資料。 然後，建立從 hello 還原點還原，名為平行資料庫時間戳記 tooensure hello 資料庫名稱未與 hello 現有租用戶資料庫名稱衝突。 接下來，hello 舊的租用戶資料庫被刪除，且 hello 還原的資料庫重新命名的 toohello 原始資料庫名稱。 最後，Contoso 搭配 Hall 資料庫處於線上 tooallow hello 應用程式存取 toohello 還原資料庫。

您已成功刪除 hello 事件之前的時間還原 hello database tooa 點。 hello 事件頁面隨即開啟，因此確認還原 hello 最後一個事件。


## <a name="next-steps"></a>後續步驟

在本教學課程中，您已了解如何：

> [!div class="checklist"]

> * 將資料庫還原到平行資料庫 (並存)
> * 就地還原資料庫

[管理租用戶資料庫結構描述](sql-database-saas-tutorial-schema-management.md)

## <a name="additional-resources"></a>其他資源

* 其他[hello Wingtip SaaS 應用程式為基礎的教學課程](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [使用 Azure SQL Database 的商務持續性概觀](sql-database-business-continuity.md)
* [了解 SQL Database 備份](sql-database-automated-backups.md)
