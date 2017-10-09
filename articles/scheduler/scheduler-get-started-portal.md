---
title: "aaaGet Azure 入口網站中開始使用 Azure 排程器 |Microsoft 文件"
description: "開始在 Azure 入口網站中使用 Azure 排程器"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: e69542ec-d10f-4f17-9b7a-2ee441ee7d68
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/10/2016
ms.author: deli
ms.openlocfilehash: 58255c0ad19da65932f8b1d36cb8fef1ff6e651b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-scheduler-in-azure-portal"></a>開始在 Azure 入口網站中使用 Azure 排程器
它是 Azure 排程器中的簡單 toocreate 排程工作。 在此教學課程中，您將學習如何 toocreate 作業。 您也將學習排程器的監視和管理功能。

## <a name="create-a-job"></a>建立工作
1. 登入太[Azure 入口網站](https://portal.azure.com/)。  
2. 按一下**+ 新增**> 類型*排程器*hello [搜尋] 方塊中 > 選取**排程器**結果中 > 按一下**建立**。
   
    ![][marketplace-create]
3. 讓我們使用 GET 要求建立只要點擊 http://www.microsoft.com/ 的工作。 在 hello**排程器工作**畫面上，輸入下列資訊的 hello:
   
   1. **名稱：** `getmicrosoft`  
   2. **訂用帳戶：** 您的 Azure 訂用帳戶   
   3. **作業集合：**選取現有的作業集合，或按一下 [建立新項目] > 輸入名稱。
4. 接下來，在**動作設定**，定義 hello 下列值：
   
   1. **動作類型：** ` HTTP`  
   2. **方法：** `GET`  
   3. **URL：** ` http://www.microsoft.com`  
      
      ![][action-settings]
5. 最後，讓我們定義排程。 hello 作業可定義為一次性工作，但我們挑選週期性排程：
   
   1. **週期**：`Recurring`
   2. **開始**：今天的日期
   3. **重複頻率**：`12 Hours`
   4. **結束於**：今天日期的前兩天  
      
      ![][recurrence-schedule]
6. 按一下 [建立] 

## <a name="manage-and-monitor-jobs"></a>管理和監視作業
一旦建立工作時，它會出現在 hello 主要的 Azure 儀表板。 按一下 hello 工作及新視窗隨即開啟並 hello 下列索引標籤：

1. 屬性  
2. 動作設定  
3. 排程  
4. 歷程記錄
5. 使用者
   
   ![][job-overview]

### <a name="properties"></a>屬性
唯讀屬性說明 hello 排程器工作的 hello 管理中繼資料。

   ![][job-properties]

### <a name="action-settings"></a>動作設定
按一下 上一 hello 的工作**作業**螢幕可讓您工作的 tooconfigure。 這可讓您設定進階的設定，如果您沒有 hello 中進行設定快速建立精靈。

對於所有的動作類型，您可以變更 hello 重試原則和 hello 錯誤動作。

對於 HTTP 和 HTTPS 工作動作類型，您可以變更 hello 方法 tooany 允許 HTTP 指令動詞。 您也可以新增、 刪除或變更 hello 標頭和基本驗證資訊。

對於儲存體佇列動作類型，您可以變更 hello 儲存體帳戶、 佇列名稱、 SAS 權杖和主體。

服務匯流排動作類型，您可以變更 hello 命名空間、 主題/佇列路徑、 驗證設定、 傳輸類型、 訊息屬性和訊息內文。

   ![][job-action-settings]

### <a name="schedule"></a>排程
這可讓您重新設定 hello 排程，如果您想要建立 hello toochange hello 排程快速建立精靈。

這是有機會 toobuild[複雜的排程與您的工作中的進階循環](scheduler-advanced-complexity.md)

您可以變更 hello 開始日期和時間、 週期性排程和 hello 結束日期和時間 （如果 hello 週期性工作。）

   ![][job-schedule]

### <a name="history"></a>歷程記錄
hello**記錄**索引標籤會顯示 hello 選取作業的 hello 系統中的選定的度量的每項工作執行。 這些度量會提供有關您的排程器 hello 健全狀況的即時值：

1. 狀態  
2. 詳細資料  
3. 重試次數
4. 發生次數：第 1 次、第 2 次、第 3 次等。
5. 執行開始時間  
6. 執行結束時間
   
   ![][job-history]

您可以按一下執行 tooview 其**詳細歷程記錄**，包括 hello 每個執行完整的回應。 此對話方塊也可讓您 toocopy hello 回應 toohello 剪貼簿。

   ![][job-history-details]

### <a name="users"></a>使用者
Azure 角色型存取控制 (RBAC) 可以對 Azure 排程器進行更細緻的存取權管理。 如何 toouse hello 使用者 索引標籤，請參閱太 toolearn[所有存取控制](../active-directory/role-based-access-control-configure.md)

## <a name="see-also"></a>另請參閱
 [排程器是什麼？](scheduler-intro.md)

 [排程器概念、術語及實體階層](scheduler-concepts-terms.md)

 [Azure 排程器的計劃和計費](scheduler-plans-billing.md)

 [排程 toobuild 複雜的方式與進階循環使用 Azure 排程器](scheduler-advanced-complexity.md)

 [排程器 REST API 參考](https://msdn.microsoft.com/library/mt629143)

 [排程器 PowerShell Cmdlet 參考](scheduler-powershell-reference.md)

 [排程器高可用性和可靠性](scheduler-high-availability-reliability.md)

 [排程器限制、預設值和錯誤碼](scheduler-limits-defaults-errors.md)

 [排程器輸出驗證](scheduler-outbound-authentication.md)

[marketplace-create]: ./media/scheduler-get-started-portal/scheduler-v2-portal-marketplace-create.png
[action-settings]: ./media/scheduler-get-started-portal/scheduler-v2-portal-action-settings.png
[recurrence-schedule]: ./media/scheduler-get-started-portal/scheduler-v2-portal-recurrence-schedule.png
[job-properties]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-properties.png
[job-overview]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-overview-1.png
[job-action-settings]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-action-settings.png
[job-schedule]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-schedule.png
[job-history]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-history.png
[job-history-details]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-history-details.png


[1]: ./media/scheduler-get-started-portal/scheduler-get-started-portal001.png
[2]: ./media/scheduler-get-started-portal/scheduler-get-started-portal002.png
[3]: ./media/scheduler-get-started-portal/scheduler-get-started-portal003.png
[4]: ./media/scheduler-get-started-portal/scheduler-get-started-portal004.png
[5]: ./media/scheduler-get-started-portal/scheduler-get-started-portal005.png
[6]: ./media/scheduler-get-started-portal/scheduler-get-started-portal006.png
[7]: ./media/scheduler-get-started-portal/scheduler-get-started-portal007.png
[8]: ./media/scheduler-get-started-portal/scheduler-get-started-portal008.png
[9]: ./media/scheduler-get-started-portal/scheduler-get-started-portal009.png
[10]: ./media/scheduler-get-started-portal/scheduler-get-started-portal010.png
[11]: ./media/scheduler-get-started-portal/scheduler-get-started-portal011.png
[12]: ./media/scheduler-get-started-portal/scheduler-get-started-portal012.png
[13]: ./media/scheduler-get-started-portal/scheduler-get-started-portal013.png
[14]: ./media/scheduler-get-started-portal/scheduler-get-started-portal014.png
[15]: ./media/scheduler-get-started-portal/scheduler-get-started-portal015.png
