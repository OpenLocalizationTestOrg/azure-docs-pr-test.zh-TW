---
title: "aaaTroubleshoot 效能問題，並最佳化您的資料庫 |Microsoft 文件"
description: "適用於效能建議 tooyour SQL 資料庫，以及上清除 toogain 深入了解如何 hello hello 查詢您的資料庫上執行的效能。"
metakeywords: azure sql database performance monitoring recommendation
services: sql-database
documentationcenter: 
manager: jhubbard
author: jan-eng
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,monitor & tune
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: janeng
ms.openlocfilehash: e948d30ac74eecf45420d5d77ef55e3c0b6f3f47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-performance-issues-and-optimize-your-database"></a>針對效能問題進行疑難排解並將資料庫最佳化

遺漏索引與查詢最佳化不足是資料庫效能不佳的常見原因。 您會在本教學課程中學到：
> [!div class="checklist"]
> * 檢閱、套用和還原效能改進建議
> * 尋找具有高資源使用率的查詢
> * 尋找長時間執行的查詢

> 您需要連續的工作負載效能問題 – 遺漏索引，例如 tooreceive 建議使用的資料庫上。
>

## <a name="log-in-toohello-azure-portal"></a>登入 toohello Azure 入口網站

登入 toohello [Azure 入口網站](https://portal.azure.com/)。

## <a name="review-and-apply-a-recommendation"></a>檢閱並套用建議

從 hello 系統為您的資料庫，請遵循這些步驟 tooapply 建議：

1. 按一下 hello**效能建議**hello 資料庫刀鋒視窗中的功能表。

    ![效能建議](./media/sql-database-performance-tutorial/perf_recommendations.png)

2. 從 hello 的建議清單，選取 使用中的建議。 在此範例中是「建立索引」。

    ![選取建議](./media/sql-database-performance-tutorial/create_index.png)

3. 按一下 hello 套用 hello 建議**套用** 按鈕。 （選擇性） 檢閱 hello 建議詳細資料，並查看 hello T-SQL 指令碼太執行上的 [**檢視指令碼**] 按鈕。

    ![套用建議](./media/sql-database-performance-tutorial/apply.png)

4. [選用]啟用自動微調建議 toobe 自動套用。

    ![自動調整](./media/sql-database-performance-tutorial/auto_tuning.png)

## <a name="revert-a-recommendation"></a>還原建議

hello Database Advisor 監視實作的每個建議。 如果建議未能改善 hello 工作負載將會自動還原。 您可以手動還原建議，但大部分情況下並不需要這麼做。 toorevert 建議：

1. 移 toohello 效能建議功能表，然後選取其中一個 hello 套用建議事項。

    ![選取建議](./media/sql-database-performance-tutorial/select.png)

2. 在 hello 詳細資料檢視中，按一下  **Revert**。

    ![還原建議](./media/sql-database-performance-tutorial/revert.png)

## <a name="find-hello-query-that-consumes-hello-most-resources"></a>尋找取用 hello hello 查詢最多資源

請依照下列耗用 hello 這些步驟 toofind hello 查詢最多資源：

1. 按一下 hello**查詢效能深入解析**hello 資料庫刀鋒視窗中的功能表。

    ![查詢深入解析](./media/sql-database-performance-tutorial/query_perf_insights.png)

2. 選取資源類型。

    ![查詢深入解析](./media/sql-database-performance-tutorial/select_resource_type.png)

3. 選取 hello hello 資料表中的第一個查詢。

    ![查詢深入解析](./media/sql-database-performance-tutorial/select_query.png)

4. 檢閱 hello 查詢詳細資料。

    ![查詢深入解析](./media/sql-database-performance-tutorial/query_details.png)

## <a name="find-hello-longest-running-query"></a>尋找 hello 最長執行的查詢

1. 移 tooQuery 效能深入解析，然後選取 hello**長時間執行的查詢** 索引標籤。

    ![查詢深入解析](./media/sql-database-performance-tutorial/long_running.png)

3. 選取 hello hello 資料表中的第一個查詢。

    ![查詢深入解析](./media/sql-database-performance-tutorial/select_first_query.png)

4. 檢閱 hello 查詢詳細資料。

    ![查詢深入解析](./media/sql-database-performance-tutorial/review_query_details.png)



## <a name="next-steps"></a>後續步驟 
遺漏索引與查詢最佳化不足是資料庫效能不佳的常見原因。 在本教學課程中，您已了解：
> [!div class="checklist"]
> * 檢閱、套用和還原效能改進建議
> * 尋找具有高資源使用率的查詢
> * 尋找長時間執行的查詢

[SQL Database 效能調整秘訣](https://docs.microsoft.com/azure/sql-database/sql-database-troubleshoot-performance)
