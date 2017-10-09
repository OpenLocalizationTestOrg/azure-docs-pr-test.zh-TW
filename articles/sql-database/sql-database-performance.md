---
title: "aaaMonitor 並改善效能-Azure SQL Database |Microsoft 文件"
description: "hello Azure SQL Database 提供效能工具 toohelp 識別可改善目前的查詢效能的區域。"
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: monicar
ms.assetid: a60b75ac-cf27-4d73-8322-ee4d4c448aa2
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/19/2016
ms.author: sstein
ms.openlocfilehash: 84b8a1bc62698a29deb49e765f208bd7e14d0870
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-improve-performance"></a>監視並改善效能
Azure SQL Database 可找出資料庫中的潛在問題，並透過提供智慧型微調動作和建議來建議可以改善工作負載效能的動作。

tooreview 您的資料庫效能、 使用 hello**效能**hello 概觀 頁面上的磚或向下巡覽太"支援 + 疑難排解 」 一節：

   ![檢視效能](./media/sql-database-performance/entries.png)

在 hello"支援 + 疑難排解"區段中，您可以使用 hello 下列頁面：


1. [效能概觀](#performance-overview)toomonitor 對資料庫效能。 
2. [效能建議](#performance-recommendations)toofind 效能的建議可改善您的工作負載的效能。
3. [查詢效能深入解析](#query-performance-insight)toofind 熱門資源取用查詢。
4. [自動調整](#automatic-tuning)toolet Azure SQL Database 會自動最佳化您的資料庫。

## <a name="performance-overview"></a>效能概觀
此檢視會提供您的資料庫效能的摘要，並可協助您進行效能調整和疑難排解。 

![效能](./media/sql-database-performance/performance.png)

* hello**建議**磚提供的微調建議，以您的資料庫分析 （前三個建議會顯示是否有更多）。 按一下此磚會帶您太**[效能建議](#performance-recommendations)**。 
* hello**微調活動**磚提供 hello 持續和已完成微調您資料庫的動作，讓您快速檢視的微調活動 hello 歷程記錄的摘要。 按一下此磚會帶您 toohello 完整微調您資料庫的歷程記錄檢視。
* hello**自動調整**磚會顯示 hello[自動調整設定](sql-database-automatic-tuning-enable.md)資料庫 （微調選項會自動套用的 tooyour 資料庫）。 按一下此磚會開啟 hello 自動化組態對話方塊。
* hello**資料庫查詢**磚會顯示 hello hello 查詢效能，為您的資料庫 （整體 DTU 使用量和 top 的資源取用查詢） 的摘要。 按一下此磚會帶您太**[查詢效能深入解析](#query-performance-insight)**。

## <a name="performance-recommendations"></a>效能建議
此頁面提供可改善資料庫效能的智慧型[微調建議](sql-database-advisor.md)。 hello 下列類型的建議會顯示此頁面上：

* 建議的索引 toocreate 或卸除。
* 當 hello 資料庫中所識別的結構描述問題的建議。
* 當查詢可以受益於參數化查詢時的建議。

![效能](./media/sql-database-performance/recommendations.png)

您也可以找到完整的歷程記錄的微調 hello 過去在已套用的動作。

深入了解如何 toofind apply 效能建議[尋找並套用效能建議](sql-database-advisor-portal.md)發行項。

## <a name="automatic-tuning"></a>自動微調
Azure SQL Databases 能透過套用[效能建議](sql-database-advisor.md)來自動微調資料庫效能。 詳細資訊，讀取 toolearn[自動調整的發行項](sql-database-automatic-tuning.md)。 讀取 tooenable[如何 tooenable 自動微調](sql-database-automatic-tuning-enable.md)。

## <a name="query-performance-insight"></a>查詢效能深入解析
[查詢效能深入解析](sql-database-query-performance.md)可讓您 toospend 疑難排解資料庫效能所提供的時間：

* 更深入的資料庫資源 (DTU) 取用分析。 
* hello cpu 使用量最大可能會改善效能進行微調的查詢。 
* 向下的能力 toodrill hello 到 hello 詳細資料的查詢中。 

  ![效能儀表板](./media/sql-database-query-performance/performance.png)

Hello 文件中找到此頁面的詳細資訊**[如何 toouse 查詢效能深入解析](sql-database-query-performance.md)**。

## <a name="additional-resources"></a>其他資源
* [單一資料庫的 Azure SQL Database 效能指引](sql-database-performance-guidance.md)
* [何時使用彈性集區？](sql-database-elastic-pool-guidance.md)

