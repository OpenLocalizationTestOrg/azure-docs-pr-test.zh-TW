---
title: "使用 Azure Data Lake Analytics aaaAnalyze 網站記錄檔 |Microsoft 文件"
description: "了解 tooanalyze 網站記錄使用 Data Lake Analytics 的方式。 "
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 3a196735-d0d9-4deb-ba68-c4b3f3be8403
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: saveenr
ms.openlocfilehash: d27aaca95ed2b643cfed7a17b0066bf7fa4a1bf5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-website-logs-using-azure-data-lake-analytics"></a>使用 Azure Data Lake Analytics 來分析網站記錄
了解如何使用 Data Lake Analytics，特別是在找出哪些推薦者 」 上 tooanalyze 網站記錄檔發生錯誤當他們嘗試 toovisit hello 網站。

## <a name="prerequisites"></a>必要條件
* **Visual Studio 2015 或 Visual Studio 2013**。
* **[Visual Studio 適用的 Data Lake 工具](http://aka.ms/adltoolsvs)**。

    資料湖 Tools for Visual Studio 安裝之後，您會看到**Data Lake** hello 中的項目**工具**Visual Studio 中的功能表：

    ![U-SQL Visual Studio 功能表](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-menu.png)
* **Data Lake Analytics 和 hello 資料湖 Tools for Visual Studio 的基本知識**。 tooget 啟動，請參閱：

  * [使用適用於 Visual Studio 的資料湖工具開發 U-SQL 指令碼](data-lake-analytics-data-lake-tools-get-started.md)。
* **資料湖分析帳戶。**  請參閱[建立 Azure Data Lake Analytics 帳戶可節省時間](data-lake-analytics-get-started-portal.md)。
* **上傳 hello 範例資料 toohello Data Lake Analytics 帳戶。** 請參閱[toocopy 範例資料檔](data-lake-analytics-get-started-portal.md)。

    toorun Data Lake Analytics 工作中，您將需要一些資料。 即使 hello Data Lake Tools 支援上傳的資料，您將在此教學課程更容易 toofollow 時使用 hello 入口 tooupload hello 範例資料 toomake。

## <a name="connect-tooazure"></a>連接 tooAzure
您可以建立和測試任何 U-SQL 指令碼之前，您必須先連接 tooAzure。

**tooconnect tooData Lake Analytics**

1. 開啟 Visual Studio。
2. 按一下 [Data Lake] > [選項和設定]。
3. 按一下**登入**，或**變更使用者**如果有人已登入，並遵循 hello 指示。
4. 按一下**確定**tooclose hello 選項和設定 對話方塊。

**toobrowse Data Lake Analytics 帳戶**

1. 從 Visual Studio 中，按 **CTRL+ALT+S**，開啟 [伺服器總管]。
2. 在 [伺服器總管] 中展開 [Azure]，然後展開 [Data Lake Analytics]。 如果有資料湖分析帳戶，您就會看到其清單。 您無法從 hello studio 建立 Data Lake Analytics 帳戶。 toocreate 的帳戶，請參閱[開始使用 Azure 入口網站的 Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md)或[開始使用 Azure PowerShell 的 Azure Data Lake Analytics](data-lake-analytics-get-started-powershell.md)。

## <a name="develop-u-sql-application"></a>開發 U-SQL 應用程式
U-SQL 應用程式基本上是 U-SQL 指令碼。 toolearn 進一步了解 U-SQL，請參閱[開始使用 U-SQL](data-lake-analytics-u-sql-get-started.md)。

您可以加入 新增使用者定義運算子 toohello 應用程式。  如需詳細資訊，請參閱 [針對資料湖分析工作開發 U-SQL 使用者定義運算子](data-lake-analytics-u-sql-develop-user-defined-operators.md)。

**toocreate 和送出 Data Lake Analytics 工作**

1. 按一下 hello**檔案 > 新增 > 專案**。
2. 選取 hello U-SQL 專案類型。

    ![新的 U-SQL Visual Studio 專案](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-new-project.png)
3. 按一下 [確定] 。 Visual Studio 會建立具有 Script.usql 檔案的方案。
4. 輸入下列指令碼到 hello Script.usql 檔案 hello:

        // Create a database for easy reuse, so you don't need tooread from a file every time.
        CREATE DATABASE IF NOT EXISTS SampleDBTutorials;

        // Create a Table valued function. TVF ensures that your jobs fetch data from hello weblog file with hello correct schema.
        DROP FUNCTION IF EXISTS SampleDBTutorials.dbo.WeblogsView;
        CREATE FUNCTION SampleDBTutorials.dbo.WeblogsView()
        RETURNS @result TABLE
        (
            s_date DateTime,
            s_time string,
            s_sitename string,
            cs_method string,
            cs_uristem string,
            cs_uriquery string,
            s_port int,
            cs_username string,
            c_ip string,
            cs_useragent string,
            cs_cookie string,
            cs_referer string,
            cs_host string,
            sc_status int,
            sc_substatus int,
            sc_win32status int,
            sc_bytes int,
            cs_bytes int,
            s_timetaken int
        )
        AS
        BEGIN

            @result = EXTRACT
                s_date DateTime,
                s_time string,
                s_sitename string,
                cs_method string,
                cs_uristem string,
                cs_uriquery string,
                s_port int,
                cs_username string,
                c_ip string,
                cs_useragent string,
                cs_cookie string,
                cs_referer string,
                cs_host string,
                sc_status int,
                sc_substatus int,
                sc_win32status int,
                sc_bytes int,
                cs_bytes int,
                s_timetaken int
            FROM @"/Samples/Data/WebLog.log"
            USING Extractors.Text(delimiter:' ');
            RETURN;
        END;

        // Create a table for storing referrers and status
        DROP TABLE IF EXISTS SampleDBTutorials.dbo.ReferrersPerDay;
        @weblog = SampleDBTutorials.dbo.WeblogsView();
        CREATE TABLE SampleDBTutorials.dbo.ReferrersPerDay
        (
            INDEX idx1
            CLUSTERED(Year ASC)
            DISTRIBUTED BY HASH(Year)
        ) AS

        SELECT s_date.Year AS Year,
            s_date.Month AS Month,
            s_date.Day AS Day,
            cs_referer,
            sc_status,
            COUNT(DISTINCT c_ip) AS cnt
        FROM @weblog
        GROUP BY s_date,
                cs_referer,
                sc_status;

    toounderstand hello U-SQL，請參閱[開始使用資料 Lake Analytics U-SQL 語言](data-lake-analytics-u-sql-get-started.md)。    
5. 加入新的 U-SQL 指令碼 tooyour 專案，然後輸入 hello 下列：

        // Query hello referrers that ran into errors
        @content =
            SELECT *
            FROM SampleDBTutorials.dbo.ReferrersPerDay
            WHERE sc_status >=400 AND sc_status < 500;

        OUTPUT @content
        too@"/Samples/Outputs/UnsuccessfulResponses.log"
        USING Outputters.Tsv();
6. 切換後 toohello 第一個 U-SQL 指令碼和 下一步 toohello**送出**按鈕，指定您 Analytics 帳戶。
7. 從 方案總管 中，在 Script.usql 上按一下滑鼠右鍵，然後按一下建置指令碼。 請確認 hello [輸出] 窗格中的 hello 結果。
8. 從 方案總管 中，在 Script.usql 上按一下滑鼠右鍵，然後按一下提交指令碼。
9. 確認 hello **Analytics 帳戶**為您想 toorun hello 工作，然後再按一下其中一個 hello**送出**。 Hello 提交完成時，都可使用 hello Data Lake Tools for Visual Studio 結果 視窗中送出結果和工作連結。
10. 請等到 hello 工作順利完成。  如果 hello 工作失敗，它很可能遺失 hello 原始程式檔。  請參閱 hello 本教學課程的必要條件一節。 如需其他疑難排解資訊，請參閱 [監視和疑難排解 Azure 資料湖分析工作](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)。

    Hello 作業完成時，您應該會看到下列畫面 hello:

    ![資料湖分析分析 weblog 網站記錄](./media/data-lake-analytics-analyze-weblogs/data-lake-analytics-analyze-weblogs-job-completed.png)
11. 現在針對 **Script1.usql**重複步驟 7 - 10。

**toosee hello 作業輸出**

1. 從**伺服器總管**，依序展開**Azure**，依序展開**Data Lake Analytics**，依序展開您的資料湖分析帳戶**的儲存體帳戶**hello 預設資料湖存放區的帳戶，以滑鼠右鍵按一下，然後按**總管**。
2. 按兩下**範例**tooopen hello 資料夾，然後按兩下 **輸出**。
3. 按兩下 **UnsuccessfulResponsees.log**。
4. 直接 toohello 輸出，您也可以按兩下 hello hello 圖表檢視順序 toonavigate 中的 hello 作業內的輸出檔。

## <a name="see-also"></a>另請參閱
tooget 開始使用 Data Lake Analytics 使用不同的工具，請參閱：

* [使用 Azure 入口網站開始使用 Data Lake Analytics](data-lake-analytics-get-started-portal.md)
* [使用 Azure PowerShell 開始使用資料湖分析](data-lake-analytics-get-started-powershell.md)
* [使用 .NET SDK 開始使用資料湖分析](data-lake-analytics-get-started-net-sdk.md)
