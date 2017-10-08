---
title: "aaaUse hello 頂點資料湖 Tools for Visual Studio 中的執行檢視 |Microsoft 文件"
description: "了解如何 toouse hello 頂點執行檢視 tooexam Data Lake Analytics 工作。"
services: data-lake-analytics
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 5366d852-e7d6-44cf-a88c-e9f52f15f7df
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 10/13/2016
ms.author: jgao
ms.openlocfilehash: fb54d2af8a32aa27a54ff50a73c1b4903677a21e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-vertex-execution-view-in-data-lake-tools-for-visual-studio"></a>在資料湖 Tools for Visual Studio 使用 hello 頂點執行檢視
了解如何 toouse hello 頂點執行檢視 tooexam Data Lake Analytics 工作。

## <a name="prerequisites"></a>必要條件

您必須使用 Data Lake Tools for Visual Studio toodevelop U-SQL 指令碼的基本知識。  請參閱[教學課程：使用適用於 Visual Studio 的 Data Lake 工具開發 U-SQL 指令碼](data-lake-analytics-data-lake-tools-get-started.md)。

## <a name="open-hello-vertex-execution-view"></a>開啟 hello 頂點執行檢視
在 Data Lake Tools for Visual Studio 中開啟 U-SQL 作業。 按一下**頂點執行檢視**hello 左下角中。 您可能會先提示的 tooload 設定檔，它可能需要一些時間，視您的網路連線。

![Data Lake Analytics 工具頂點執行檢視](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-open-vertex-execution-view.png)

## <a name="understand-vertex-execution-view"></a>了解頂點執行檢視
hello 頂點執行檢視有三個部分：

![Data Lake Analytics 工具頂點執行檢視](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view.png)

hello**頂點選取器**在 hello 左可讓您可以選取頂點功能 （例如前 10 個資料讀取，或選擇由階段）。 其中一個 hello 最常用的篩選器為 toosee hello**關鍵路徑的頂點**。 hello**徑**hello U SQL 作業的頂點的最長的鏈結。 了解 hello 關鍵路徑可用於最佳化您的工作，藉由檢查哪些頂點採用 hello 最長時間。
  
![Data Lake Analytics 工具頂點執行檢視](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view-pane2.png)

hello 正上方窗格會顯示 hello**執行中 狀態的所有 hello 頂點**。
  
![Data Lake Analytics 工具頂點執行檢視](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view-pane3.png)

hello 底端中央窗格會顯示每個頂點的相關資訊：
* 處理序名稱： hello hello 頂點的執行個體名稱。 由 StageName|VertexName|VertexRunInstance 中的不同部分組成。 比方說，hello SV7_Split [62].v1 頂點代表 hello 第二個執行個體 （.v1，從 0 開始的索引） 的頂點數目 62 階段 SV7_Split 中。
* 總資料讀取/寫入： hello 資料為讀取/寫入此頂點。
* 狀態/結束： hello 最終狀態 hello 頂點結束時。
* Hello 頂點失敗時，結束碼/失敗類型： hello 時發生錯誤。
* 建立的原因： 為何 hello 頂點已建立。
* 資源延遲處理/延遲/PN 佇列延遲： hello 的時間 hello 頂點 toowait 資源、 tooprocess 資料和 toostay hello 佇列中。
* 處理序/建立者 GUID: Hello 的目前執行頂點或其建立者的 GUID。
* 版本： 執行頂點的 hello hello 第 N 個執行個體 （hello 系統可能會針對的排程頂點的新執行個體有許多原因，例如容錯移轉時，計算備援等。）
* 版本建立時間。
* 處理建立開始時間/處理序已排入佇列時間/處理序開始時間/處理序完成時間： hello 頂點處理序啟動建立; 時hello 頂點處理序啟動時執行 tooqueue;當 hello 特定頂點的程序會啟動。hello 特定頂點完成時。

## <a name="next-steps"></a>後續步驟
* toolog 診斷資訊，請參閱[存取 Azure 資料湖分析診斷記錄檔](data-lake-analytics-diagnostic-logs.md)
* toosee 更複雜的查詢，請參閱[使用 Azure Data Lake Analytics 分析網站記錄檔](data-lake-analytics-analyze-weblogs.md)。
* tooview 作業的詳細資訊，請參閱[使用作業瀏覽器和 Azure Data lake Analytics 工作的工作檢視](data-lake-analytics-data-lake-tools-view-jobs.md)
