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
# <a name="analyze-website-logs-using-azure-data-lake-analytics"></a><span data-ttu-id="30d35-103">使用 Azure Data Lake Analytics 來分析網站記錄</span><span class="sxs-lookup"><span data-stu-id="30d35-103">Analyze Website logs using Azure Data Lake Analytics</span></span>
<span data-ttu-id="30d35-104">了解如何使用 Data Lake Analytics，特別是在找出哪些推薦者 」 上 tooanalyze 網站記錄檔發生錯誤當他們嘗試 toovisit hello 網站。</span><span class="sxs-lookup"><span data-stu-id="30d35-104">Learn how tooanalyze website logs using Data Lake Analytics, especially on finding out which referrers ran into errors when they tried toovisit hello website.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="30d35-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="30d35-105">Prerequisites</span></span>
* <span data-ttu-id="30d35-106">**Visual Studio 2015 或 Visual Studio 2013**。</span><span class="sxs-lookup"><span data-stu-id="30d35-106">**Visual Studio 2015 or Visual Studio 2013**.</span></span>
* <span data-ttu-id="30d35-107">**[Visual Studio 適用的 Data Lake 工具](http://aka.ms/adltoolsvs)**。</span><span class="sxs-lookup"><span data-stu-id="30d35-107">**[Data Lake Tools for Visual Studio](http://aka.ms/adltoolsvs)**.</span></span>

    <span data-ttu-id="30d35-108">資料湖 Tools for Visual Studio 安裝之後，您會看到**Data Lake** hello 中的項目**工具**Visual Studio 中的功能表：</span><span class="sxs-lookup"><span data-stu-id="30d35-108">Once Data Lake Tools for Visual Studio is installed, you will see a **Data Lake** item in hello **Tools** menu in Visual Studio:</span></span>

    ![U-SQL Visual Studio 功能表](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-menu.png)
* <span data-ttu-id="30d35-110">**Data Lake Analytics 和 hello 資料湖 Tools for Visual Studio 的基本知識**。</span><span class="sxs-lookup"><span data-stu-id="30d35-110">**Basic knowledge of Data Lake Analytics and hello Data Lake Tools for Visual Studio**.</span></span> <span data-ttu-id="30d35-111">tooget 啟動，請參閱：</span><span class="sxs-lookup"><span data-stu-id="30d35-111">tooget started, see:</span></span>

  * <span data-ttu-id="30d35-112">[使用適用於 Visual Studio 的資料湖工具開發 U-SQL 指令碼](data-lake-analytics-data-lake-tools-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="30d35-112">[Develop U-SQL script using Data Lake tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
* <span data-ttu-id="30d35-113">**資料湖分析帳戶。**</span><span class="sxs-lookup"><span data-stu-id="30d35-113">**A Data Lake Analytics account.**</span></span>  <span data-ttu-id="30d35-114">請參閱[建立 Azure Data Lake Analytics 帳戶可節省時間](data-lake-analytics-get-started-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="30d35-114">See [Create an Azure Data Lake Analytics account](data-lake-analytics-get-started-portal.md).</span></span>
* <span data-ttu-id="30d35-115">**上傳 hello 範例資料 toohello Data Lake Analytics 帳戶。**</span><span class="sxs-lookup"><span data-stu-id="30d35-115">**Upload hello sample data toohello Data Lake Analytics account.**</span></span> <span data-ttu-id="30d35-116">請參閱[toocopy 範例資料檔](data-lake-analytics-get-started-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="30d35-116">See [toocopy sample data files](data-lake-analytics-get-started-portal.md).</span></span>

    <span data-ttu-id="30d35-117">toorun Data Lake Analytics 工作中，您將需要一些資料。</span><span class="sxs-lookup"><span data-stu-id="30d35-117">toorun a Data Lake Analytics job, you will need some data.</span></span> <span data-ttu-id="30d35-118">即使 hello Data Lake Tools 支援上傳的資料，您將在此教學課程更容易 toofollow 時使用 hello 入口 tooupload hello 範例資料 toomake。</span><span class="sxs-lookup"><span data-stu-id="30d35-118">Even though hello Data Lake Tools supports uploading data, you will use hello portal tooupload hello sample data toomake this tutorial easier toofollow.</span></span>

## <a name="connect-tooazure"></a><span data-ttu-id="30d35-119">連接 tooAzure</span><span class="sxs-lookup"><span data-stu-id="30d35-119">Connect tooAzure</span></span>
<span data-ttu-id="30d35-120">您可以建立和測試任何 U-SQL 指令碼之前，您必須先連接 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="30d35-120">Before you can build and test any U-SQL scripts, you must first connect tooAzure.</span></span>

<span data-ttu-id="30d35-121">**tooconnect tooData Lake Analytics**</span><span class="sxs-lookup"><span data-stu-id="30d35-121">**tooconnect tooData Lake Analytics**</span></span>

1. <span data-ttu-id="30d35-122">開啟 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="30d35-122">Open Visual Studio.</span></span>
2. <span data-ttu-id="30d35-123">按一下 [Data Lake] > [選項和設定]。</span><span class="sxs-lookup"><span data-stu-id="30d35-123">Click **Data Lake > Options and Settings**.</span></span>
3. <span data-ttu-id="30d35-124">按一下**登入**，或**變更使用者**如果有人已登入，並遵循 hello 指示。</span><span class="sxs-lookup"><span data-stu-id="30d35-124">Click **Sign In**, or **Change User** if someone has signed in, and follow hello instructions.</span></span>
4. <span data-ttu-id="30d35-125">按一下**確定**tooclose hello 選項和設定 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="30d35-125">Click **OK** tooclose hello Options and Settings dialog.</span></span>

<span data-ttu-id="30d35-126">**toobrowse Data Lake Analytics 帳戶**</span><span class="sxs-lookup"><span data-stu-id="30d35-126">**toobrowse your Data Lake Analytics accounts**</span></span>

1. <span data-ttu-id="30d35-127">從 Visual Studio 中，按 **CTRL+ALT+S**，開啟 [伺服器總管]。</span><span class="sxs-lookup"><span data-stu-id="30d35-127">From Visual Studio, open **Server Explorer** by press **CTRL+ALT+S**.</span></span>
2. <span data-ttu-id="30d35-128">在 [伺服器總管] 中展開 [Azure]，然後展開 [Data Lake Analytics]。</span><span class="sxs-lookup"><span data-stu-id="30d35-128">From **Server Explorer**, expand **Azure**, and then expand **Data Lake Analytics**.</span></span> <span data-ttu-id="30d35-129">如果有資料湖分析帳戶，您就會看到其清單。</span><span class="sxs-lookup"><span data-stu-id="30d35-129">You shall see a list of your Data Lake Analytics accounts if there are any.</span></span> <span data-ttu-id="30d35-130">您無法從 hello studio 建立 Data Lake Analytics 帳戶。</span><span class="sxs-lookup"><span data-stu-id="30d35-130">You cannot create Data Lake Analytics accounts from hello studio.</span></span> <span data-ttu-id="30d35-131">toocreate 的帳戶，請參閱[開始使用 Azure 入口網站的 Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md)或[開始使用 Azure PowerShell 的 Azure Data Lake Analytics](data-lake-analytics-get-started-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="30d35-131">toocreate an account, see [Get Started with Azure Data Lake Analytics using Azure Portal](data-lake-analytics-get-started-portal.md) or [Get Started with Azure Data Lake Analytics using Azure PowerShell](data-lake-analytics-get-started-powershell.md).</span></span>

## <a name="develop-u-sql-application"></a><span data-ttu-id="30d35-132">開發 U-SQL 應用程式</span><span class="sxs-lookup"><span data-stu-id="30d35-132">Develop U-SQL application</span></span>
<span data-ttu-id="30d35-133">U-SQL 應用程式基本上是 U-SQL 指令碼。</span><span class="sxs-lookup"><span data-stu-id="30d35-133">A U-SQL application is mostly a U-SQL script.</span></span> <span data-ttu-id="30d35-134">toolearn 進一步了解 U-SQL，請參閱[開始使用 U-SQL](data-lake-analytics-u-sql-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="30d35-134">toolearn more about U-SQL, see [Get started with U-SQL](data-lake-analytics-u-sql-get-started.md).</span></span>

<span data-ttu-id="30d35-135">您可以加入 新增使用者定義運算子 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="30d35-135">You can add addition user-defined operators toohello application.</span></span>  <span data-ttu-id="30d35-136">如需詳細資訊，請參閱 [針對資料湖分析工作開發 U-SQL 使用者定義運算子](data-lake-analytics-u-sql-develop-user-defined-operators.md)。</span><span class="sxs-lookup"><span data-stu-id="30d35-136">For more information, see [Develop U-SQL user defined operators for Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-user-defined-operators.md).</span></span>

<span data-ttu-id="30d35-137">**toocreate 和送出 Data Lake Analytics 工作**</span><span class="sxs-lookup"><span data-stu-id="30d35-137">**toocreate and submit a Data Lake Analytics job**</span></span>

1. <span data-ttu-id="30d35-138">按一下 hello**檔案 > 新增 > 專案**。</span><span class="sxs-lookup"><span data-stu-id="30d35-138">Click hello **File > New > Project**.</span></span>
2. <span data-ttu-id="30d35-139">選取 hello U-SQL 專案類型。</span><span class="sxs-lookup"><span data-stu-id="30d35-139">Select hello U-SQL Project type.</span></span>

    ![新的 U-SQL Visual Studio 專案](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-new-project.png)
3. <span data-ttu-id="30d35-141">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="30d35-141">Click **OK**.</span></span> <span data-ttu-id="30d35-142">Visual Studio 會建立具有 Script.usql 檔案的方案。</span><span class="sxs-lookup"><span data-stu-id="30d35-142">Visual studio creates a solution with a Script.usql file.</span></span>
4. <span data-ttu-id="30d35-143">輸入下列指令碼到 hello Script.usql 檔案 hello:</span><span class="sxs-lookup"><span data-stu-id="30d35-143">Enter hello following script into hello Script.usql file:</span></span>

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

    <span data-ttu-id="30d35-144">toounderstand hello U-SQL，請參閱[開始使用資料 Lake Analytics U-SQL 語言](data-lake-analytics-u-sql-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="30d35-144">toounderstand hello U-SQL, see [Get started with Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>    
5. <span data-ttu-id="30d35-145">加入新的 U-SQL 指令碼 tooyour 專案，然後輸入 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="30d35-145">Add a new U-SQL script tooyour project and enter hello following:</span></span>

        // Query hello referrers that ran into errors
        @content =
            SELECT *
            FROM SampleDBTutorials.dbo.ReferrersPerDay
            WHERE sc_status >=400 AND sc_status < 500;

        OUTPUT @content
        too@"/Samples/Outputs/UnsuccessfulResponses.log"
        USING Outputters.Tsv();
6. <span data-ttu-id="30d35-146">切換後 toohello 第一個 U-SQL 指令碼和 下一步 toohello**送出**按鈕，指定您 Analytics 帳戶。</span><span class="sxs-lookup"><span data-stu-id="30d35-146">Switch back toohello first U-SQL script and next toohello **Submit** button, specify your Analytics account.</span></span>
7. <span data-ttu-id="30d35-147">從 方案總管 中，在 Script.usql 上按一下滑鼠右鍵，然後按一下建置指令碼。</span><span class="sxs-lookup"><span data-stu-id="30d35-147">From **Solution Explorer**, right click **Script.usql**, and then click **Build Script**.</span></span> <span data-ttu-id="30d35-148">請確認 hello [輸出] 窗格中的 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="30d35-148">Verify hello results in hello Output pane.</span></span>
8. <span data-ttu-id="30d35-149">從 方案總管 中，在 Script.usql 上按一下滑鼠右鍵，然後按一下提交指令碼。</span><span class="sxs-lookup"><span data-stu-id="30d35-149">From **Solution Explorer**, right click **Script.usql**, and then click **Submit Script**.</span></span>
9. <span data-ttu-id="30d35-150">確認 hello **Analytics 帳戶**為您想 toorun hello 工作，然後再按一下其中一個 hello**送出**。</span><span class="sxs-lookup"><span data-stu-id="30d35-150">Verify hello **Analytics Account** is hello one where you want toorun hello job, and then click **Submit**.</span></span> <span data-ttu-id="30d35-151">Hello 提交完成時，都可使用 hello Data Lake Tools for Visual Studio 結果 視窗中送出結果和工作連結。</span><span class="sxs-lookup"><span data-stu-id="30d35-151">Submission results and job link are available in hello Data Lake Tools for Visual Studio Results window when hello submission is completed.</span></span>
10. <span data-ttu-id="30d35-152">請等到 hello 工作順利完成。</span><span class="sxs-lookup"><span data-stu-id="30d35-152">Wait until hello job is completed successfully.</span></span>  <span data-ttu-id="30d35-153">如果 hello 工作失敗，它很可能遺失 hello 原始程式檔。</span><span class="sxs-lookup"><span data-stu-id="30d35-153">If hello job failed, it is most likely missing hello source file.</span></span>  <span data-ttu-id="30d35-154">請參閱 hello 本教學課程的必要條件一節。</span><span class="sxs-lookup"><span data-stu-id="30d35-154">Please see hello Prerequisite section of this tutorial.</span></span> <span data-ttu-id="30d35-155">如需其他疑難排解資訊，請參閱 [監視和疑難排解 Azure 資料湖分析工作](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)。</span><span class="sxs-lookup"><span data-stu-id="30d35-155">For additional troubleshooting information, see [Monitor and troubleshoot Azure Data Lake Analytics jobs](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).</span></span>

    <span data-ttu-id="30d35-156">Hello 作業完成時，您應該會看到下列畫面 hello:</span><span class="sxs-lookup"><span data-stu-id="30d35-156">When hello job is completed, you shall see hello following screen:</span></span>

    ![資料湖分析分析 weblog 網站記錄](./media/data-lake-analytics-analyze-weblogs/data-lake-analytics-analyze-weblogs-job-completed.png)
11. <span data-ttu-id="30d35-158">現在針對 **Script1.usql**重複步驟 7 - 10。</span><span class="sxs-lookup"><span data-stu-id="30d35-158">Now repeat steps 7- 10 for **Script1.usql**.</span></span>

<span data-ttu-id="30d35-159">**toosee hello 作業輸出**</span><span class="sxs-lookup"><span data-stu-id="30d35-159">**toosee hello job output**</span></span>

1. <span data-ttu-id="30d35-160">從**伺服器總管**，依序展開**Azure**，依序展開**Data Lake Analytics**，依序展開您的資料湖分析帳戶**的儲存體帳戶**hello 預設資料湖存放區的帳戶，以滑鼠右鍵按一下，然後按**總管**。</span><span class="sxs-lookup"><span data-stu-id="30d35-160">From **Server Explorer**, expand **Azure**, expand **Data Lake Analytics**, expand your Data Lake Analytics account, expand **Storage Accounts**, right-click hello default Data Lake Storage account, and then click **Explorer**.</span></span>
2. <span data-ttu-id="30d35-161">按兩下**範例**tooopen hello 資料夾，然後按兩下 **輸出**。</span><span class="sxs-lookup"><span data-stu-id="30d35-161">Double-click **Samples** tooopen hello folder, and then double-click **Outputs**.</span></span>
3. <span data-ttu-id="30d35-162">按兩下 **UnsuccessfulResponsees.log**。</span><span class="sxs-lookup"><span data-stu-id="30d35-162">Double-click **UnsuccessfulResponsees.log**.</span></span>
4. <span data-ttu-id="30d35-163">直接 toohello 輸出，您也可以按兩下 hello hello 圖表檢視順序 toonavigate 中的 hello 作業內的輸出檔。</span><span class="sxs-lookup"><span data-stu-id="30d35-163">You can also double-click hello output file inside hello graph view of hello job in order toonavigate directly toohello output.</span></span>

## <a name="see-also"></a><span data-ttu-id="30d35-164">另請參閱</span><span class="sxs-lookup"><span data-stu-id="30d35-164">See also</span></span>
<span data-ttu-id="30d35-165">tooget 開始使用 Data Lake Analytics 使用不同的工具，請參閱：</span><span class="sxs-lookup"><span data-stu-id="30d35-165">tooget started with Data Lake Analytics using different tools, see:</span></span>

* [<span data-ttu-id="30d35-166">使用 Azure 入口網站開始使用 Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="30d35-166">Get started with Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="30d35-167">使用 Azure PowerShell 開始使用資料湖分析</span><span class="sxs-lookup"><span data-stu-id="30d35-167">Get started with Data Lake Analytics using Azure PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="30d35-168">使用 .NET SDK 開始使用資料湖分析</span><span class="sxs-lookup"><span data-stu-id="30d35-168">Get started with Data Lake Analytics using .NET SDK</span></span>](data-lake-analytics-get-started-net-sdk.md)
