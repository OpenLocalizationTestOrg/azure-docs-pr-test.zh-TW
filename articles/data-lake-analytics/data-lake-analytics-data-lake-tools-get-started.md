---
title: "aaaDevelop U-SQL 指令碼以使用 Data Lake Tools for Visual Studio |Microsoft 文件"
description: "了解如何 tooinstall Data Lake Tools for Visual Studio 中，以及如何 toodevelop 和測試 U-SQL 指令碼。"
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: jhubbard
editor: cgronlun
ms.assetid: ad8a6992-02c7-47d4-a108-62fc5a0777a3
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/28/2017
ms.author: saveenr, yanacai
ms.openlocfilehash: 7a0c02c275b8cefecbe784ba63969cbf24a150d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="develop-u-sql-scripts-by-using-data-lake-tools-for-visual-studio"></a>使用適用於 Visual Studio 的 Data Lake 工具來開發 U-SQL 指令碼
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]


深入了解如何 toouse Visual Studio toocreate Azure Data Lake Analytics 帳戶，會定義中的工作[U-SQL](data-lake-analytics-u-sql-get-started.md)，並提交作業 toohello 資料湖分析服務。 如需有關 Data Lake Analytics 的詳細資訊，請參閱 [Azure Data Lake Analytics 概觀](data-lake-analytics-overview.md)。


## <a name="prerequisites"></a>必要條件

* **Visual Studio**：支援 Express 以外的所有版本。
    * Visual Studio 2017
    * Visual Studio 2015
    * Visual Studio 2013
* **Microsoft Azure SDK for .NET** 2.7.1 版或更新版本。  安裝使用 hello [Web platform installer](http://www.microsoft.com/web/downloads/platform.aspx)。
* **Data Lake Analytics** 帳戶。 toocreate 的帳戶，請參閱[開始使用 Azure 入口網站的 Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md)。

## <a name="install-azure-data-lake-tools-for-visual-studio"></a>安裝 Azure Data Lake Tools for Visual Studio 

下載並安裝 Azure 資料湖 Tools for Visual Studio[從 hello 下載中心](http://aka.ms/adltoolsvs)。 安裝後，請注意：
* hello**伺服器總管** > **Azure**節點包含**Data Lake Analytics**節點。 
* hello**工具**功能表有**Data Lake**項目。

## <a name="connect-tooan-azure-data-lake-analytics-account"></a>Tooan Azure Data Lake Analytics 帳戶連線

1. 開啟 Visual Studio。
2. 選取 [檢視] > [伺服器總管] 可開啟伺服器總管。
3. 以滑鼠右鍵按一下 [Azure]。 然後選取**連接 tooMicrosoft Azure 訂用帳戶**並遵循 hello 指示。
4. 在 [伺服器總管] 中，選取 **Azure** > **Data Lake Analytics**。 您會看到 Data Lake Analytics 帳戶的清單。


## <a name="write-your-first-u-sql-script"></a>撰寫第一個 U-SQL 指令碼

下列文字的 hello 是簡單的 U-SQL 指令碼。 它會定義小型資料集和資料集 toohello 預設 Data Lake Store 檔案呼叫寫入`/data.csv`。

```
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    too"/data.csv"
    USING Outputters.Csv();
```

### <a name="submit-a-data-lake-analytics-job"></a>提交資料湖分析作業

1. 選取 [檔案] > [新增] > [專案]。

2. 選取 hello **U-SQL 專案**輸入，然後再按一下**確定**。 Visual Studio 會建立具有 **Script.usql** 檔案的解決方案。

3. Hello 先前的指令碼貼到 hello **Script.usql**視窗。

4. 在 [hello 左上角的 hello **Script.usql**視窗中，指定 hello Data Lake Analytics 帳戶。

    ![提交 U-SQL Visual Studio 專案](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-submit-job.png)

5. 在 [hello 左上角的 hello **Script.usql**視窗中，選取**送出**。
6. 確認 hello **Analytics 帳戶**，然後選取**送出**。 Hello 提交完成後使用 hello 資料湖 Tools for Visual Studio 結果中提交的結果。

    ![提交 U-SQL Visual Studio 專案](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-submit-job-advanced.png)
7. toosee hello 最新作業的狀態和重新整理 hello 畫面上，按一下 [**重新整理**。 Hello 作業成功時，它會顯示 hello**作業圖形**，**中繼資料作業**，**狀態記錄**，和**診斷**:

    ![U SQL Visual Studio Data Lake Analytics 工作效能圖表](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-performance-graph.png)

   * **工作摘要**顯示 hello hello 工作的摘要。   
   * **工作詳細資料**顯示 hello 工作，其中包括 hello 指令碼、 資源和頂點的其他特定資訊。
   * **作業圖形**視覺化 hello hello 作業進度。
   * **中繼資料作業**顯示 hello U-SQL 目錄上所執行的所有 hello 動作。
   * **資料**顯示所有 hello 輸入和輸出。
   * **診斷**會提供作業執行和效能最佳化的進階分析。

### <a name="toocheck-job-state"></a>toocheck 工作狀態

1. 在 [伺服器總管] 中，選取 **Azure** > **Data Lake Analytics**。 
2. 展開 hello Data Lake Analytics 帳戶名稱。
3. 按兩下 [作業]。
4. 選取您先前送出 hello 工作。

### <a name="toosee-hello-output-of-a-job"></a>工作的 toosee hello 輸出

1. 在 [伺服器總管瀏覽 toohello 您提交的工作。
2. 按一下 hello**資料**] 索引標籤。
3. 在 [hello**作業輸出**索引標籤，選取 hello`"/data.csv"`檔案。

## <a name="next-steps"></a>後續步驟

* [在您自己的工作站上執行 U-SQL 指令碼進行測試和偵錯](data-lake-analytics-data-lake-tools-local-run.md)
* [在 U-SQL 作業中進行 C# 程式碼偵錯](data-lake-analytics-debug-u-sql-jobs.md)
* [使用 hello Azure 資料湖 Tools for Visual Studio 程式碼](data-lake-analytics-data-lake-tools-for-vscode.md)
