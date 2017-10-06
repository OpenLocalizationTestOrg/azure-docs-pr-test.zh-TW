---
title: "使用 Azure 入口網站的 aaaTroubleshoot Azure Data Lake Analytics 作業 |Microsoft 文件"
description: "了解如何 toouse hello Azure 入口網站 tootroubleshoot Data Lake Analytics 工作。 "
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: b7066d81-3142-474f-8a34-32b0b39656dc
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: e810d56bab8f1a8254721ec9906bb6a4508dc22a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-data-lake-analytics-jobs-using-azure-portal"></a>使用 Azure 入口網站疑難排解 Azure 資料湖分析作業
了解如何 toouse hello Azure 入口網站 tootroubleshoot Data Lake Analytics 工作。

在本教學課程中，您會安裝遺失的來源檔案問題，並使用 hello Azure 入口網站 tootroubleshoot hello 問題。

## <a name="submit-a-data-lake-analytics-job"></a>提交資料湖分析作業

送出 hello 遵循 U-SQL 作業：

```
@searchlog =
   EXTRACT UserId          int,
           Start           DateTime,
           Region          string,
           Query           string,
           Duration        int?,
           Urls            string,
           ClickedUrls     string
   FROM "/Samples/Data/SearchLog.tsv1"
   USING Extractors.Tsv();

OUTPUT @searchlog   
   too"/output/SearchLog-from-adls.csv"
   USING Outputters.Csv();
```
    
hello hello 指令碼中定義的原始程式檔是**/Samples/Data/SearchLog.tsv1**，應該是**/Samples/Data/SearchLog.tsv**。


## <a name="troubleshoot-hello-job"></a>疑難排解 hello 作業

**toosee 所有 hello 工作**

1. 從 hello Azure 入口網站，按一下  **Microsoft Azure** hello 左上角。
2. 按一下 hello 磚使用 Data Lake Analytics 帳戶名稱。  hello 工作摘要會顯示在 hello**作業管理**磚。

    ![Azure 資料湖分析作業管理](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-job-management.png)

    hello 作業管理可讓您一目瞭然 hello 作業狀態。 請注意失敗的工作。
3. 按一下 hello**作業管理**磚 toosee hello 作業。 hello 作業分為**執行**，**排入佇列**，和**結束**。 您應該會看到您失敗的作業在 hello**結束**> 一節。 應該就能 hello 清單中的第一個。 當您有大量的工作時，您可以按一下**篩選**toohelp 您 toolocate 作業。

    ![Azure 資料湖分析篩選作業](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-filter-jobs.png)
4. 按一下 hello hello 清單 tooopen hello 工作詳細資料中的新刀鋒視窗從失敗的作業：

    ![Azure 資料湖分析失敗作業](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-failed-job.png)

    請注意 hello**重新提交** 按鈕。 修正 hello 問題之後，您可以重新提交 hello 作業。
5. 按一下反白顯示的部分從 hello 上一個螢幕擷取畫面 tooopen hello 錯誤詳細資料。  您會看到類似下面的畫面：

    ![Azure 資料湖分析失敗作業詳細資料](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-failed-job-details.png)

    它會告訴您找不到 hello 來源資料夾。
6. 按一下 [ **重複的指令碼**]。
7. 更新 hello **FROM**路徑 toohello 下列：

    "/Samples/Data/SearchLog.tsv"
8. 按一下 [ **提交作業**]。

## <a name="see-also"></a>另請參閱
* [Azure 資料湖分析概觀](data-lake-analytics-overview.md)
* [使用 Azure PowerShell 開始使用 Azure 資料湖分析](data-lake-analytics-get-started-powershell.md)
* [透過 Visual Studio 開始使用 Azure 資料湖分析與 U-SQL](data-lake-analytics-u-sql-get-started.md)
* [使用 Azure 入口網站管理 Azure Data Lake Analytics](data-lake-analytics-manage-use-portal.md)
