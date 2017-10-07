---
title: "aaa\"Azure Analysis Services 的 Adventure Works 教學課程 |Microsoft 文件 」"
description: "Hello Adventure Works 教學課程介紹 Azure Analysis services"
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 06/01/2017
ms.author: owend
ms.openlocfilehash: 2df8b3ab4e8c4ffbe0086418d60fd2e2abd35e7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-analysis-services---adventure-works-tutorial"></a>Azure Analysis Services - Adventure Works 教學課程

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

本教學課程提供如何課程 toocreate 和部署的 hello 1400 相容性層級的表格式模型使用[SQL Server Data Tools (SSDT)](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)。  

如果您是新 tooAnalysis 服務和表格式模型，完成本教學課程會最快速方式 toolearn hello 是如何 toocreate 和部署的基本表格式模型。 一旦您擁有 hello 必要條件就地，所應使用兩個 toothree 小時 toocomplete 之間。  
  
## <a name="what-you-learn"></a>您學到什麼   
  
-   在 hello toocreate 新的表格式模型專案的方式**1400年相容性層級**在 SSDT 中。
  
-   如何從關聯式資料庫到表格式模型專案 tooimport 資料。  
  
-   如何 toocreate 和管理 hello 模型中的資料表之間的關聯性。  
  
-   如何 toocreate 導出資料行、 量值和關鍵效能指標，幫助使用者分析重要商務標準。  
  
-   如何 toocreate 和管理檢視方塊和階層，幫助使用者更輕鬆地瀏覽模型資料提供業務和應用程式特有視點。  
  
-   如何 toocreate 資料分割的資料表資料分成較小的邏輯部分可獨立於其他資料分割處理。  
  
-   如何 toosecure 藉由建立角色的使用者成員模型物件和資料。  
  
-   如何 toodeploy 表格式模型 tooan **Azure Analysis Services**伺服器或內部部署 SQL Server 2017 Analysis Services 伺服器。  
  
## <a name="prerequisites"></a>必要條件  
toocomplete 本教學課程中，您需要：  
  
-   Azure Analysis Services 或 SQL Server 2017 Analysis Services 執行個體 toodeploy 至模型。 註冊免費的 [Azure Analysis Services 試用版](https://azure.microsoft.com/services/analysis-services/)和[建立伺服器](../analysis-services-create-server.md)。 或者，註冊並下載 [SQL Server 2017 Community Technology Preview](https://www.microsoft.com/evalcenter/evaluate-sql-server-vnext-ctp)。 

-   SQL Server 資料倉儲或 Azure SQL 資料倉儲以 hello [AdventureWorksDW2014 範例資料庫](http://go.microsoft.com/fwlink/?LinkID=335807)。 這個範例資料庫包括 hello 資料所需 toocomplete 本教學課程。 下載 [SQL Server 免費版本](https://www.microsoft.com/sql-server/sql-server-downloads)。 或者，註冊免費的 [Azure SQL Database 試用版](https://azure.microsoft.com/services/sql-database/)。 

    **重要事項：**如果您在內部部署 SQL Server 上安裝 hello 範例資料庫，而且您部署模型 tooan Azure Analysis Services 伺服器時，[在內部部署資料閘道](../analysis-services-gateway.md)需要。

-   hello 最新版本的[SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx)。

-   hello 最新版本的[SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。    

-   用戶端應用程式，例如 [Power BI Desktop](https://powerbi.microsoft.com/desktop/) 或 Excel。 

## <a name="scenario"></a>案例  
本教學課程以虛構公司 Adventure Works Cycles 做為基礎。 Adventure Works 則是大型的跨國製造公司，製造及批發自行車、 組件] 和 [附屬應用程式 toocommercial 市場中北美、 歐洲和亞洲。 hello 公司雇用 500 位員工。 此外，Adventure Works 僱用數個區域銷售團隊，遍布其市場規模。 您的專案是 toocreate 表格式模型，讓銷售及行銷使用者 tooanalyze hello AdventureWorksDW 資料庫中的網際網路銷售資料。  
  
toocomplete hello 教學課程中，您必須完成各種課程。 每個課程有一些工作。 必須完成 hello 課程完成每項工作順序。 特定的課程中可能有幾項工作會達成類似的結果，但您完成每項工作的方式會稍有不同。 這個方法顯示，通常會有多個方法之一 toocomplete 工作和 toochallenge 您使用技術學中先前的課程和工作。  
  
hello hello 課程的目的是的 tooguide 您透過撰寫的基本表格式模型使用的許多 hello 功能包含在 SSDT 中。 因為每個課程根據 hello 上一課，您應該完成 hello 課程中的順序。
  
本教學課程不提供有關管理伺服器，以在 Azure 入口網站，管理伺服器或資料庫使用 SSMS，或使用用戶端應用程式 toobrowse 模型資料。 


## <a name="lessons"></a>課程  
這個教學課程包括下列課程中的 hello:  
  
|課程|預估的時間 toocomplete|  
|----------|------------------------------|  
|[1 - 建立新的表格式模型專案](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md)|10 分鐘|  
|[2 - 取得資料](../tutorials/aas-lesson-2-get-data.md)|10 分鐘|  
|[3 - 標記為日期資料表](../tutorials/aas-lesson-3-mark-as-date-table.md)|3 分鐘|  
|[4 - 建立關聯性](../tutorials/aas-lesson-4-create-relationships.md)|10 分鐘|  
|[5 - 建立計算結果欄](../tutorials/aas-lesson-5-create-calculated-columns.md)|15 Minuten|
|[6 - 建立量值](../tutorials/aas-lesson-6-create-measures.md)|30 分鐘|  
|[7 - 建立關鍵效能指標 (KPI)](../tutorials/aas-lesson-7-create-key-performance-indicators.md)|15 Minuten|  
|[8 - 建立檢視方塊](../tutorials/aas-lesson-8-create-perspectives.md)|5 分鐘|  
|[9 - 建立階層](../tutorials/aas-lesson-9-create-hierarchies.md)|20 分鐘|  
|[10 - 建立分割區](../tutorials/aas-lesson-10-create-partitions.md)|15 Minuten|  
|[11 - 建立角色](../tutorials/aas-lesson-11-create-roles.md)|15 Minuten|  
|[12 - 在 Excel 中分析](../tutorials/aas-lesson-12-analyze-in-excel.md)|5 分鐘| 
|[13 - 部署](../tutorials/aas-lesson-13-deploy.md)|5 分鐘|  
  
## <a name="supplemental-lessons"></a>補充課程  
這些課程不需要的 toocomplete hello 教學課程中，但可能有助於更佳了解進階表格式模型撰寫功能。  
  
|課程|預估的時間 toocomplete|  
|----------|------------------------------|  
|[詳細資料列](../tutorials/aas-supplemental-lesson-detail-rows.md)|10 分鐘|
|[動態安全性](../tutorials/aas-supplemental-lesson-dynamic-security.md)|30 分鐘|
|[不完全階層](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)|20 分鐘| 

  
## <a name="next-steps"></a>後續步驟  
tooget 啟動，請參閱[第 1 課： 建立新的表格式模型專案](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md)。  
  
  
  

