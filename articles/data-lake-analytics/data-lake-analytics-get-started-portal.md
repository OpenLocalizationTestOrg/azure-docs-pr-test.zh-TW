---
title: "開始使用 Azure 入口網站的 Azure Data Lake Analytics 使用 aaaGet |Microsoft 文件"
description: "了解如何 toouse hello Azure 入口網站 toocreate Data Lake Analytics 帳戶中建立使用 U SQL Data Lake Analytics 工作並送出 hello 作業。 "
services: data-lake-analytics
documentationcenter: 
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: b1584d16-e0d2-4019-ad1f-f04be8c5b430
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/21/2017
ms.author: edmaca
ms.openlocfilehash: 6bb54404fa42cfed25b18bc2bfb7c72e6c361149
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-portal"></a>使用 Azure 入口網站開始使用 Azure Data Lake Analytics
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

了解如何 toouse hello Azure 入口網站 toocreate Azure Data Lake Analytics 帳戶，定義中的工作[U-SQL](data-lake-analytics-u-sql-get-started.md)，並提交作業 toohello 資料湖分析服務。 如需有關 Data Lake Analytics 的詳細資訊，請參閱 [Azure Data Lake Analytics 概觀](data-lake-analytics-overview.md)。

## <a name="prerequisites"></a>必要條件

開始進行本教學課程之前，您必須擁有 **Azure 訂用帳戶**。 請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。

## <a name="create-a-data-lake-analytics-account"></a>建立 Data Lake Analytics 帳戶

現在，您會建立 Data Lake Analytics 並 Data Lake Store 帳戶 hello 在相同的時間。  這個步驟很簡單，而且只需要 60 秒 toofinish。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 按一下 [新增] >  [資料 + 分析] > [Data Lake Analytics]。
3. 選取下列項目 hello 的值：
   * **名稱**：替 Data Lake Analytics 帳戶命名 (只允許小寫字母和數字)。
   * **訂用帳戶**： 選擇 hello 用於 hello Analytics 帳戶的 Azure 訂用帳戶。
   * **資源群組**。 選取現有的 Azure 資源群組，或建立一個新的群組。
   * **位置**。 選取 Azure 資料中心 hello Data Lake Analytics 帳戶。
   * **Data Lake Store**： 遵循 hello 指令 toocreate 新的 Data Lake Store 帳戶，或選取現有的我的最愛。 
4. (選擇性) 選取 Data Lake Analytics 帳戶的定價層。
5. 按一下 [建立] 。 


## <a name="your-first-u-sql-script"></a>您的第一個 U-SQL 指令碼

下列文字的 hello 是非常簡單的 U-SQL 指令碼。 它會定義 hello 指令碼內的小型資料集，並接著寫為名的檔案中的 toohello 預設 Data Lake Store 出該資料集`/data.csv`。

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

## <a name="submit-a-u-sql-job"></a>提交 U-SQL 作業

1. 從 hello Data Lake Analytics 帳戶中，按一下 **新工作**。
2. 如上所示的 U-SQL 指令碼貼上 hello hello 文字中。 
3. 按一下 [ **提交作業**]。   
4. 等候直到在 hello 作業狀態變更太**Succeeded**。
5. 如果 hello 作業失敗，請參閱[監視和疑難排解資料湖分析作業](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)。
6. 按一下 hello**輸出**索引標籤，然後再按一下`data.csv`。 

## <a name="see-also"></a>另請參閱

* tooget 開始開發 U-SQL 應用程式，請參閱[使用 Data Lake Tools for Visual Studio 的開發 U-SQL 指令碼](data-lake-analytics-data-lake-tools-get-started.md)。
* toolearn U-SQL，請參閱[開始使用 Azure 資料湖分析 U-SQL 語言](data-lake-analytics-u-sql-get-started.md)。
* 針對管理工作，請參閱 [使用 Azure 入口網站管理 Azure Data Lake Analytics](data-lake-analytics-manage-use-portal.md)。
