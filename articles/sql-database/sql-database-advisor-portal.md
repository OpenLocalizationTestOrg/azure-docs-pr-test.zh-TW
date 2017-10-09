---
title: "aaaApply 效能建議 Azure SQL Database |Microsoft 文件"
description: "您可以使用 hello Azure 入口網站 toofind 效能建議可以將您的 Azure SQL Database 或 toocorrect 的效能最佳化，您的工作負載中所識別的一些問題。"
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: monicar
ms.assetid: cda8a646-0584-4368-b28a-85cdd9b54fcd
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/05/2017
ms.author: sstein
ms.openlocfilehash: 0b2234840fc3254d235db9e7d18f5bc912851c6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="find-and-apply-performance-recommendations"></a>尋找和套用效能建議

您可以使用 hello Azure 入口網站 toofind 效能建議可以將您的 Azure SQL Database 或 toocorrect 的效能最佳化，您的工作負載中所識別的一些問題。 **效能建議**Azure 入口網站中的頁面可讓您根據其潛在影響 toofind hello 熱門建議。 

## <a name="viewing-recommendations"></a>檢視建議

tooview 並套用效能的建議，您需要 hello 正確[角色型存取控制](../active-directory/role-based-access-control-what-is.md)在 Azure 中的權限。 **讀取器**， **SQL DB 參與者**權限是必要的 tooview 建議，和**擁有者**， **SQL DB 參與者**不需要權限tooexecute 任何動作;建立或卸除索引並取消索引建立。

使用 Azure 入口網站上遵循步驟 toofind 效能建議事項的 hello:

1. 登入 toohello [Azure 入口網站](https://portal.azure.com/)。
2. 跳過**更多服務** > **SQL 資料庫**，然後選取您的資料庫。
3. 瀏覽過**效能建議**tooview hello 選取的資料庫可用的建議。

效能建議為 shonw hello 資料表類似 toohello hello 遵循圖上顯示的其中一個：

![建議](./media/sql-database-advisor-portal/recommendations.png)

建議會依照其對成下列類別目錄的 hello 效能的潛在影響：

| 影響 | 說明 |
|:--- |:--- |
| 高 |具有強烈影響的建議應該提供 hello 最重要的效能影響。 |
| 中型 |中度影響建議會改善效能，但不顯著。 |
| 低 |低影響建議比沒有建議時提供更好的效能，但改善可能不顯著。 |


> [!NOTE]
> Azure SQL Database 需要 toomonitor 活動至少一天中順序 tooidentify 一些建議。 比隨機收訊活動暴增的 hello Azure SQL Database 可以更輕鬆地將最佳化的一致的查詢模式。 如果建議不使用 corrently，hello**效能建議**頁面會提供訊息說明原因。
> 

您也可以檢視 hello hello 歷史操作狀態。 選取建議或狀態 toosee 更多詳細資料。

以下是範例的 < Create index"hello Azure 入口網站中的建議動作。

![建立索引](./media/sql-database-advisor-portal/sql-database-performance-recommendation.png)

## <a name="applying-recommendations"></a>套用建議
Azure SQL Database 可讓您完整控制建議的方式啟用使用任何下列三個選項的 hello: 

* 一次套用一個個別的建議。
* 啟用 hello 自動微調 tooautomatically 套用建議。
* tooimplement 建議手動執行 hello 建議針對您的資料庫 T-SQL 指令碼。

選取任何建議 tooview 其詳細資料，然後按一下**檢視指令碼**tooreview hello 確切的 hello 建議的建立方式的詳細資料。

hello 資料庫仍在線上時套用 hello 建議-使用效能建議或自動調整永遠不會讓資料庫離線。

### <a name="apply-an-individual-recommendation"></a>套用個別的建議
您可以一次檢閱並接受一個建議。

1. 在 hello**建議**刀鋒視窗中，選取的建議。
2. 在 [hello**詳細資料**刀鋒視窗中按一下**套用**] 按鈕。
   
    ![套用建議](./media/sql-database-advisor-portal/apply.png)

Hello 資料庫上，將會套用選取的建議。

### <a name="removing-recommendations-from-hello-list"></a>移除 hello 清單中的建議
如果您的建議清單包含您想從 hello 清單 tooremove 項目，您可以捨棄 hello 建議：

1. Hello 清單中選取建議**建議**tooopen hello 詳細資料。
2. 按一下**捨棄**上 hello**詳細資料**刀鋒視窗。

如有需要，您可以將丟棄的項目加回 toohello**建議**清單：

1. 在 hello**建議**刀鋒視窗中按一下**捨棄檢視**。
2. 選取已捨棄的項目從 hello 清單 tooview 其詳細資料。
3. （選擇性） 按一下**復原捨棄**tooadd hello 索引上一頁 toohello 主要清單**建議**。


### <a name="enable-automatic-tuning"></a>啟用自動微調
您可以自動設定 hello Azure SQL Database tooimplement 建議。 當建議可供使用時將會自動套用。 為所有建議受 hello 與服務如果 hello 效能影響為負值 hello 建議將還原。

1. 在 hello**建議**刀鋒視窗中，按一下 **自動化**:
   
    ![建議程式設定](./media/sql-database-advisor-portal/settings.png)
2. 選取動作 tooautomate:
   
    ![建議的索引](./media/sql-database-advisor-portal/automation.png)

### <a name="manually-run-hello-recommended-t-sql-script"></a>手動執行 hello 建議 T-SQL 指令碼
選取任何建議，然後按一下檢視指令碼 。 針對資料庫執行這個指令碼 toomanually 套用 hello 建議。

*以手動方式執行的索引不受監視且 hello 服務的效能影響驗證*因此建議您在建立 tooverify 之後監視這些索引它們提供效能提升和調整或刪除它們，如果必要的。 如需有關建立索引的詳細資訊，請參閱 [CREATE INDEX (Transact-SQL)](https://msdn.microsoft.com/library/ms188783.aspx)。

### <a name="canceling-recommendations"></a>取消建議
可以取消處於**擱置中**、**確認中**或**成功**狀態的建議。 狀態為 **執行中** 的建議無法取消。

1. 在 hello 中選取建議**微調記錄**區域 tooopen hello**建議詳細資料**刀鋒視窗。
2. 按一下**取消**tooabort hello 套用 hello 建議的處理程序。

## <a name="monitoring-operations"></a>監視作業
套用建議時可能不會立即執行。 hello 入口網站提供建議的 hello 狀態相關的詳細資料。 hello 下面是可以是索引的可能狀態：

| 狀態 | 說明 |
|:--- |:--- |
| Pending |已收到套用建議命令，且已排程執行。 |
| 執行中 |正在套用 hello 建議。 |
| 驗證中 |已成功套用建議事項和 hello 服務要衡量 hello 優點。 |
| 成功 |已成功套用建議，並證實有益處。 |
| 錯誤 |將套用 hello 建議 hello 程序期間發生錯誤。 這可以是暫時性的問題，或可能是結構描述變更 toohello 資料表和 hello 指令碼已不再有效。 |
| 還原 |hello 建議已套用，但已視為非效能，並自動還原。 |
| 已還原 |hello 建議已還原。 |

按一下從 hello 清單 toosee 同處理序建議更多詳細資料：

![建議的索引](./media/sql-database-advisor-portal/operations.png)

### <a name="reverting-a-recommendation"></a>還原建議
如果您使用 hello 效能建議 tooapply hello 建議 （表示您沒有手動執行 hello T-SQL 指令碼） 它將會自動將它還原如果找到 hello 效能影響 toobe 負數。 如果您只想 toorevert 因故建議您可以 hello 下列：

1. 選取已成功套用建議事項中 hello**微調記錄**區域。
2. 按一下**Revert**上 hello**建議詳細資料**刀鋒視窗。

![建議的索引](./media/sql-database-advisor-portal/details.png)

## <a name="monitoring-performance-impact-of-index-recommendations"></a>監視索引建議的效能影響
已成功實作建議之後 （目前，索引作業和參數化查詢建議只） 您可以按一下**查詢 Insights** hello 建議詳細資料 刀鋒視窗 tooopen 上[查詢效能深入資訊](sql-database-query-performance.md)並查看您排名最前面查詢 hello 效能影響。

![監視效能影響](./media/sql-database-advisor-portal/query-insights.png)

## <a name="summary"></a>摘要
Azure SQL Database 會提供可改善 SQL Database 效能的建議。 藉由提供 T-SQL 指令碼，以及獨立且全自動的，您會獲得最佳化資料庫的實用協助，並最終改善查詢效能。

## <a name="next-steps"></a>後續步驟
監視您的建議，並繼續 tooapply 它們 toorefine 效能。 資料庫工作負載會動態地持續變更。 Azure SQL Database 會繼續 toomonitor，並提供可以改善您的資料庫效能的建議。 

* 請參閱[自動微調](sql-database-automatic-tuning.md)toolearn 深入了解 hello Azure SQL Database 中的自動調整。
* 如需 Azure SQL Database 效能建議的概觀，請參閱[效能建議](sql-database-advisor.md)。
* 請參閱[查詢效能深入資訊](sql-database-query-performance.md)toolearn 有關檢視 hello 您排名最前面的查詢效能影響。

## <a name="additional-resources"></a>其他資源
* [查詢存放區](https://msdn.microsoft.com/library/dn817826.aspx)
* [CREATE INDEX](https://msdn.microsoft.com/library/ms188783.aspx)
* [角色型存取控制](../active-directory/role-based-access-control-what-is.md)

