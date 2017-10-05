---
title: "使用 Azure Data Lake Analytics 來分析網站記錄 | Microsoft Docs"
description: "了解如何使用資料湖分析來分析網站記錄。 "
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
ms.openlocfilehash: 25fbbe97d26491fc421f4821315761c18e523ec8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="analyze-website-logs-using-azure-data-lake-analytics"></a><span data-ttu-id="e0c79-103">使用 Azure Data Lake Analytics 來分析網站記錄</span><span class="sxs-lookup"><span data-stu-id="e0c79-103">Analyze Website logs using Azure Data Lake Analytics</span></span>
<span data-ttu-id="e0c79-104">了解如何使用資料湖分析來分析網站記錄，特別是找出哪些訪客來源在嘗試瀏覽網站時遇到錯誤。</span><span class="sxs-lookup"><span data-stu-id="e0c79-104">Learn how to analyze website logs using Data Lake Analytics, especially on finding out which referrers ran into errors when they tried to visit the website.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e0c79-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="e0c79-105">Prerequisites</span></span>
* <span data-ttu-id="e0c79-106">**Visual Studio 2015 或 Visual Studio 2013**。</span><span class="sxs-lookup"><span data-stu-id="e0c79-106">**Visual Studio 2015 or Visual Studio 2013**.</span></span>
* <span data-ttu-id="e0c79-107">**[Visual Studio 適用的 Data Lake 工具](http://aka.ms/adltoolsvs)**。</span><span class="sxs-lookup"><span data-stu-id="e0c79-107">**[Data Lake Tools for Visual Studio](http://aka.ms/adltoolsvs)**.</span></span>

    <span data-ttu-id="e0c79-108">安裝適用於 Visual Studio 的 Data Lake 工具之後，您會在 Visual Studio 的 [工具] 功能表中看到 [Datat Lake] 項目：</span><span class="sxs-lookup"><span data-stu-id="e0c79-108">Once Data Lake Tools for Visual Studio is installed, you will see a **Data Lake** item in the **Tools** menu in Visual Studio:</span></span>

    ![U-SQL Visual Studio 功能表](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-menu.png)
* <span data-ttu-id="e0c79-110">**對於資料湖分析和適用於 Visual Studio 的資料湖工具有基本的認識**。</span><span class="sxs-lookup"><span data-stu-id="e0c79-110">**Basic knowledge of Data Lake Analytics and the Data Lake Tools for Visual Studio**.</span></span> <span data-ttu-id="e0c79-111">若要開始使用，請參閱：</span><span class="sxs-lookup"><span data-stu-id="e0c79-111">To get started, see:</span></span>

  * <span data-ttu-id="e0c79-112">[使用適用於 Visual Studio 的資料湖工具開發 U-SQL 指令碼](data-lake-analytics-data-lake-tools-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="e0c79-112">[Develop U-SQL script using Data Lake tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
* <span data-ttu-id="e0c79-113">**資料湖分析帳戶。**</span><span class="sxs-lookup"><span data-stu-id="e0c79-113">**A Data Lake Analytics account.**</span></span>  <span data-ttu-id="e0c79-114">請參閱[建立 Azure Data Lake Analytics 帳戶可節省時間](data-lake-analytics-get-started-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="e0c79-114">See [Create an Azure Data Lake Analytics account](data-lake-analytics-get-started-portal.md).</span></span>
* <span data-ttu-id="e0c79-115">**將範例資料上傳到資料湖分析帳戶。**</span><span class="sxs-lookup"><span data-stu-id="e0c79-115">**Upload the sample data to the Data Lake Analytics account.**</span></span> <span data-ttu-id="e0c79-116">請參閱[複製範例資料檔案](data-lake-analytics-get-started-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="e0c79-116">See [To copy sample data files](data-lake-analytics-get-started-portal.md).</span></span>

    <span data-ttu-id="e0c79-117">若要執行資料湖分析工作，您需要一些資料。</span><span class="sxs-lookup"><span data-stu-id="e0c79-117">To run a Data Lake Analytics job, you will need some data.</span></span> <span data-ttu-id="e0c79-118">即使資料湖工具支援上傳資料，您將使用入口網站來上傳範例資料，以方便遵循本教學課程。</span><span class="sxs-lookup"><span data-stu-id="e0c79-118">Even though the Data Lake Tools supports uploading data, you will use the portal to upload the sample data to make this tutorial easier to follow.</span></span>

## <a name="connect-to-azure"></a><span data-ttu-id="e0c79-119">連接到 Azure</span><span class="sxs-lookup"><span data-stu-id="e0c79-119">Connect to Azure</span></span>
<span data-ttu-id="e0c79-120">您必須先連接至 Azure，然後才能建置及測試任何 U-SQL 指令碼。</span><span class="sxs-lookup"><span data-stu-id="e0c79-120">Before you can build and test any U-SQL scripts, you must first connect to Azure.</span></span>

<span data-ttu-id="e0c79-121">**連接到資料湖分析**</span><span class="sxs-lookup"><span data-stu-id="e0c79-121">**To connect to Data Lake Analytics**</span></span>

1. <span data-ttu-id="e0c79-122">開啟 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="e0c79-122">Open Visual Studio.</span></span>
2. <span data-ttu-id="e0c79-123">按一下 [Data Lake] > [選項和設定]。</span><span class="sxs-lookup"><span data-stu-id="e0c79-123">Click **Data Lake > Options and Settings**.</span></span>
3. <span data-ttu-id="e0c79-124">按一下 [登入]，或者如果已有其他人登入則按一下 [變更使用者]，並遵循指示。</span><span class="sxs-lookup"><span data-stu-id="e0c79-124">Click **Sign In**, or **Change User** if someone has signed in, and follow the instructions.</span></span>
4. <span data-ttu-id="e0c79-125">按一下 [確定]  關閉 [選項和設定] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="e0c79-125">Click **OK** to close the Options and Settings dialog.</span></span>

<span data-ttu-id="e0c79-126">**瀏覽您的資料湖分析帳戶**</span><span class="sxs-lookup"><span data-stu-id="e0c79-126">**To browse your Data Lake Analytics accounts**</span></span>

1. <span data-ttu-id="e0c79-127">從 Visual Studio 中，按 **CTRL+ALT+S**，開啟 [伺服器總管]。</span><span class="sxs-lookup"><span data-stu-id="e0c79-127">From Visual Studio, open **Server Explorer** by press **CTRL+ALT+S**.</span></span>
2. <span data-ttu-id="e0c79-128">在 [伺服器總管] 中展開 [Azure]，然後展開 [Data Lake Analytics]。</span><span class="sxs-lookup"><span data-stu-id="e0c79-128">From **Server Explorer**, expand **Azure**, and then expand **Data Lake Analytics**.</span></span> <span data-ttu-id="e0c79-129">如果有資料湖分析帳戶，您就會看到其清單。</span><span class="sxs-lookup"><span data-stu-id="e0c79-129">You shall see a list of your Data Lake Analytics accounts if there are any.</span></span> <span data-ttu-id="e0c79-130">您無法從 Visual Studio 建立資料湖分析帳戶。</span><span class="sxs-lookup"><span data-stu-id="e0c79-130">You cannot create Data Lake Analytics accounts from the studio.</span></span> <span data-ttu-id="e0c79-131">若要建立帳戶，請參閱[使用 Azure 入口網站開始使用 Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md) 或[使用 Azure PowerShell 開始使用 Azure Data Lake Analytics](data-lake-analytics-get-started-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="e0c79-131">To create an account, see [Get Started with Azure Data Lake Analytics using Azure Portal](data-lake-analytics-get-started-portal.md) or [Get Started with Azure Data Lake Analytics using Azure PowerShell](data-lake-analytics-get-started-powershell.md).</span></span>

## <a name="develop-u-sql-application"></a><span data-ttu-id="e0c79-132">開發 U-SQL 應用程式</span><span class="sxs-lookup"><span data-stu-id="e0c79-132">Develop U-SQL application</span></span>
<span data-ttu-id="e0c79-133">U-SQL 應用程式基本上是 U-SQL 指令碼。</span><span class="sxs-lookup"><span data-stu-id="e0c79-133">A U-SQL application is mostly a U-SQL script.</span></span> <span data-ttu-id="e0c79-134">若要深入了解 U-SQL，請參閱 [開始使用 U-SQL 語言](data-lake-analytics-u-sql-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="e0c79-134">To learn more about U-SQL, see [Get started with U-SQL](data-lake-analytics-u-sql-get-started.md).</span></span>

<span data-ttu-id="e0c79-135">您可以加入其他使用者定義的運算子至應用程式。</span><span class="sxs-lookup"><span data-stu-id="e0c79-135">You can add addition user-defined operators to the application.</span></span>  <span data-ttu-id="e0c79-136">如需詳細資訊，請參閱 [針對資料湖分析工作開發 U-SQL 使用者定義運算子](data-lake-analytics-u-sql-develop-user-defined-operators.md)。</span><span class="sxs-lookup"><span data-stu-id="e0c79-136">For more information, see [Develop U-SQL user defined operators for Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-user-defined-operators.md).</span></span>

<span data-ttu-id="e0c79-137">**建立並提交資料湖分析工作**</span><span class="sxs-lookup"><span data-stu-id="e0c79-137">**To create and submit a Data Lake Analytics job**</span></span>

1. <span data-ttu-id="e0c79-138">按一下 [檔案] > [新增] > [專案]。</span><span class="sxs-lookup"><span data-stu-id="e0c79-138">Click the **File > New > Project**.</span></span>
2. <span data-ttu-id="e0c79-139">選取 [U-SQL 專案] 類型。</span><span class="sxs-lookup"><span data-stu-id="e0c79-139">Select the U-SQL Project type.</span></span>

    ![新的 U-SQL Visual Studio 專案](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-new-project.png)
3. <span data-ttu-id="e0c79-141">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="e0c79-141">Click **OK**.</span></span> <span data-ttu-id="e0c79-142">Visual Studio 會建立具有 Script.usql 檔案的方案。</span><span class="sxs-lookup"><span data-stu-id="e0c79-142">Visual studio creates a solution with a Script.usql file.</span></span>
4. <span data-ttu-id="e0c79-143">在 Script.usql 檔案中輸入下列指令碼：</span><span class="sxs-lookup"><span data-stu-id="e0c79-143">Enter the following script into the Script.usql file:</span></span>

        // Create a database for easy reuse, so you don't need to read from a file every time.
        CREATE DATABASE IF NOT EXISTS SampleDBTutorials;

        // Create a Table valued function. TVF ensures that your jobs fetch data from the weblog file with the correct schema.
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

    <span data-ttu-id="e0c79-144">若要了解 U-SQL，請參閱 [開始使用資料湖分析 U-SQL 語言](data-lake-analytics-u-sql-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="e0c79-144">To understand the U-SQL, see [Get started with Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>    
5. <span data-ttu-id="e0c79-145">將新的 U-SQL 指令碼加入至專案並輸入下列資訊：</span><span class="sxs-lookup"><span data-stu-id="e0c79-145">Add a new U-SQL script to your project and enter the following:</span></span>

        // Query the referrers that ran into errors
        @content =
            SELECT *
            FROM SampleDBTutorials.dbo.ReferrersPerDay
            WHERE sc_status >=400 AND sc_status < 500;

        OUTPUT @content
        TO @"/Samples/Outputs/UnsuccessfulResponses.log"
        USING Outputters.Tsv();
6. <span data-ttu-id="e0c79-146">依序切換回至第一個 U-SQL 指令碼和 [提交]  按鈕，指定您的分析帳戶。</span><span class="sxs-lookup"><span data-stu-id="e0c79-146">Switch back to the first U-SQL script and next to the **Submit** button, specify your Analytics account.</span></span>
7. <span data-ttu-id="e0c79-147">從 [方案總管] 中，在 [Script.usql] 上按一下滑鼠右鍵，然後按一下 [建置指令碼]。</span><span class="sxs-lookup"><span data-stu-id="e0c79-147">From **Solution Explorer**, right click **Script.usql**, and then click **Build Script**.</span></span> <span data-ttu-id="e0c79-148">確認 [輸出] 窗格中的結果。</span><span class="sxs-lookup"><span data-stu-id="e0c79-148">Verify the results in the Output pane.</span></span>
8. <span data-ttu-id="e0c79-149">從 [方案總管] 中，在 [Script.usql] 上按一下滑鼠右鍵，然後按一下 [提交指令碼]。</span><span class="sxs-lookup"><span data-stu-id="e0c79-149">From **Solution Explorer**, right click **Script.usql**, and then click **Submit Script**.</span></span>
9. <span data-ttu-id="e0c79-150">確認 [分析帳戶] 是在您想要執行工作的帳戶，然後按一下 [提交]。</span><span class="sxs-lookup"><span data-stu-id="e0c79-150">Verify the **Analytics Account** is the one where you want to run the job, and then click **Submit**.</span></span> <span data-ttu-id="e0c79-151">提交作業完成時，[適用於 Visual Studio 的資料湖工具結果] 視窗中便會出現提交結果和工作連結。</span><span class="sxs-lookup"><span data-stu-id="e0c79-151">Submission results and job link are available in the Data Lake Tools for Visual Studio Results window when the submission is completed.</span></span>
10. <span data-ttu-id="e0c79-152">請等待工作成功完成。</span><span class="sxs-lookup"><span data-stu-id="e0c79-152">Wait until the job is completed successfully.</span></span>  <span data-ttu-id="e0c79-153">如果工作失敗，很可能是因為遺漏了原始檔。</span><span class="sxs-lookup"><span data-stu-id="e0c79-153">If the job failed, it is most likely missing the source file.</span></span>  <span data-ttu-id="e0c79-154">請參閱本教學課程的＜必要條件＞一節。</span><span class="sxs-lookup"><span data-stu-id="e0c79-154">Please see the Prerequisite section of this tutorial.</span></span> <span data-ttu-id="e0c79-155">如需其他疑難排解資訊，請參閱 [監視和疑難排解 Azure 資料湖分析工作](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)。</span><span class="sxs-lookup"><span data-stu-id="e0c79-155">For additional troubleshooting information, see [Monitor and troubleshoot Azure Data Lake Analytics jobs](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).</span></span>

    <span data-ttu-id="e0c79-156">工作完成之後，您會看到下列畫面：</span><span class="sxs-lookup"><span data-stu-id="e0c79-156">When the job is completed, you shall see the following screen:</span></span>

    ![資料湖分析分析 weblog 網站記錄](./media/data-lake-analytics-analyze-weblogs/data-lake-analytics-analyze-weblogs-job-completed.png)
11. <span data-ttu-id="e0c79-158">現在針對 **Script1.usql**重複步驟 7 - 10。</span><span class="sxs-lookup"><span data-stu-id="e0c79-158">Now repeat steps 7- 10 for **Script1.usql**.</span></span>

<span data-ttu-id="e0c79-159">**查看作業輸出**</span><span class="sxs-lookup"><span data-stu-id="e0c79-159">**To see the job output**</span></span>

1. <span data-ttu-id="e0c79-160">在 [伺服器總管] 中，依序展開 [Azure]、[Data Lake Analytics]、您的 Data Lake Analytics 帳戶，以及 [儲存體帳戶]，然後用滑鼠右鍵按一下預設的 Data Lake 儲存體帳戶，再按一下 [總管]。</span><span class="sxs-lookup"><span data-stu-id="e0c79-160">From **Server Explorer**, expand **Azure**, expand **Data Lake Analytics**, expand your Data Lake Analytics account, expand **Storage Accounts**, right-click the default Data Lake Storage account, and then click **Explorer**.</span></span>
2. <span data-ttu-id="e0c79-161">按兩下 [範例] 來開啟資料夾，然後再連按兩下 [輸出]。</span><span class="sxs-lookup"><span data-stu-id="e0c79-161">Double-click **Samples** to open the folder, and then double-click **Outputs**.</span></span>
3. <span data-ttu-id="e0c79-162">按兩下 **UnsuccessfulResponsees.log**。</span><span class="sxs-lookup"><span data-stu-id="e0c79-162">Double-click **UnsuccessfulResponsees.log**.</span></span>
4. <span data-ttu-id="e0c79-163">您也可以按兩下工作的圖形檢視內的輸出檔，直接瀏覽至輸出。</span><span class="sxs-lookup"><span data-stu-id="e0c79-163">You can also double-click the output file inside the graph view of the job in order to navigate directly to the output.</span></span>

## <a name="see-also"></a><span data-ttu-id="e0c79-164">另請參閱</span><span class="sxs-lookup"><span data-stu-id="e0c79-164">See also</span></span>
<span data-ttu-id="e0c79-165">若要使用不同的工具開始使用資料湖分析，請參閱：</span><span class="sxs-lookup"><span data-stu-id="e0c79-165">To get started with Data Lake Analytics using different tools, see:</span></span>

* [<span data-ttu-id="e0c79-166">使用 Azure 入口網站開始使用資料湖分析</span><span class="sxs-lookup"><span data-stu-id="e0c79-166">Get started with Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="e0c79-167">使用 Azure PowerShell 開始使用資料湖分析</span><span class="sxs-lookup"><span data-stu-id="e0c79-167">Get started with Data Lake Analytics using Azure PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="e0c79-168">使用 .NET SDK 開始使用資料湖分析</span><span class="sxs-lookup"><span data-stu-id="e0c79-168">Get started with Data Lake Analytics using .NET SDK</span></span>](data-lake-analytics-get-started-net-sdk.md)
