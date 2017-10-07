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
# <a name="develop-u-sql-scripts-by-using-data-lake-tools-for-visual-studio"></a><span data-ttu-id="4b94c-103">使用適用於 Visual Studio 的 Data Lake 工具來開發 U-SQL 指令碼</span><span class="sxs-lookup"><span data-stu-id="4b94c-103">Develop U-SQL scripts by using Data Lake Tools for Visual Studio</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]


<span data-ttu-id="4b94c-104">深入了解如何 toouse Visual Studio toocreate Azure Data Lake Analytics 帳戶，會定義中的工作[U-SQL](data-lake-analytics-u-sql-get-started.md)，並提交作業 toohello 資料湖分析服務。</span><span class="sxs-lookup"><span data-stu-id="4b94c-104">Learn how toouse Visual Studio toocreate Azure Data Lake Analytics accounts, define jobs in [U-SQL](data-lake-analytics-u-sql-get-started.md), and submit jobs toohello Data Lake Analytics service.</span></span> <span data-ttu-id="4b94c-105">如需有關 Data Lake Analytics 的詳細資訊，請參閱 [Azure Data Lake Analytics 概觀](data-lake-analytics-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="4b94c-105">For more information about Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="4b94c-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="4b94c-106">Prerequisites</span></span>

* <span data-ttu-id="4b94c-107">**Visual Studio**：支援 Express 以外的所有版本。</span><span class="sxs-lookup"><span data-stu-id="4b94c-107">**Visual Studio**: All editions except Express are supported.</span></span>
    * <span data-ttu-id="4b94c-108">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="4b94c-108">Visual Studio 2017</span></span>
    * <span data-ttu-id="4b94c-109">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="4b94c-109">Visual Studio 2015</span></span>
    * <span data-ttu-id="4b94c-110">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="4b94c-110">Visual Studio 2013</span></span>
* <span data-ttu-id="4b94c-111">**Microsoft Azure SDK for .NET** 2.7.1 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="4b94c-111">**Microsoft Azure SDK for .NET** version 2.7.1 or later.</span></span>  <span data-ttu-id="4b94c-112">安裝使用 hello [Web platform installer](http://www.microsoft.com/web/downloads/platform.aspx)。</span><span class="sxs-lookup"><span data-stu-id="4b94c-112">Install it by using hello [Web platform installer](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
* <span data-ttu-id="4b94c-113">**Data Lake Analytics** 帳戶。</span><span class="sxs-lookup"><span data-stu-id="4b94c-113">A **Data Lake Analytics** account.</span></span> <span data-ttu-id="4b94c-114">toocreate 的帳戶，請參閱[開始使用 Azure 入口網站的 Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="4b94c-114">toocreate an account, see [Get Started with Azure Data Lake Analytics using Azure portal](data-lake-analytics-get-started-portal.md).</span></span>

## <a name="install-azure-data-lake-tools-for-visual-studio"></a><span data-ttu-id="4b94c-115">安裝 Azure Data Lake Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4b94c-115">Install Azure Data Lake Tools for Visual Studio</span></span> 

<span data-ttu-id="4b94c-116">下載並安裝 Azure 資料湖 Tools for Visual Studio[從 hello 下載中心](http://aka.ms/adltoolsvs)。</span><span class="sxs-lookup"><span data-stu-id="4b94c-116">Download and install Azure Data Lake Tools for Visual Studio [from hello Download Center](http://aka.ms/adltoolsvs).</span></span> <span data-ttu-id="4b94c-117">安裝後，請注意：</span><span class="sxs-lookup"><span data-stu-id="4b94c-117">After installation, note that:</span></span>
* <span data-ttu-id="4b94c-118">hello**伺服器總管** > **Azure**節點包含**Data Lake Analytics**節點。</span><span class="sxs-lookup"><span data-stu-id="4b94c-118">hello **Server Explorer** > **Azure** node contains a **Data Lake Analytics** node.</span></span> 
* <span data-ttu-id="4b94c-119">hello**工具**功能表有**Data Lake**項目。</span><span class="sxs-lookup"><span data-stu-id="4b94c-119">hello **Tools** menu has a **Data Lake** item.</span></span>

## <a name="connect-tooan-azure-data-lake-analytics-account"></a><span data-ttu-id="4b94c-120">Tooan Azure Data Lake Analytics 帳戶連線</span><span class="sxs-lookup"><span data-stu-id="4b94c-120">Connect tooan Azure Data Lake Analytics account</span></span>

1. <span data-ttu-id="4b94c-121">開啟 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="4b94c-121">Open Visual Studio.</span></span>
2. <span data-ttu-id="4b94c-122">選取 [檢視] > [伺服器總管] 可開啟伺服器總管。</span><span class="sxs-lookup"><span data-stu-id="4b94c-122">Open Server Explorer by selecting **View** > **Server Explorer**.</span></span>
3. <span data-ttu-id="4b94c-123">以滑鼠右鍵按一下 [Azure]。</span><span class="sxs-lookup"><span data-stu-id="4b94c-123">Right-click **Azure**.</span></span> <span data-ttu-id="4b94c-124">然後選取**連接 tooMicrosoft Azure 訂用帳戶**並遵循 hello 指示。</span><span class="sxs-lookup"><span data-stu-id="4b94c-124">Then select **Connect tooMicrosoft Azure Subscription** and follow hello instructions.</span></span>
4. <span data-ttu-id="4b94c-125">在 [伺服器總管] 中，選取 **Azure** > **Data Lake Analytics**。</span><span class="sxs-lookup"><span data-stu-id="4b94c-125">In Server Explorer, select **Azure** > **Data Lake Analytics**.</span></span> <span data-ttu-id="4b94c-126">您會看到 Data Lake Analytics 帳戶的清單。</span><span class="sxs-lookup"><span data-stu-id="4b94c-126">You see a list of your Data Lake Analytics accounts.</span></span>


## <a name="write-your-first-u-sql-script"></a><span data-ttu-id="4b94c-127">撰寫第一個 U-SQL 指令碼</span><span class="sxs-lookup"><span data-stu-id="4b94c-127">Write your first U-SQL script</span></span>

<span data-ttu-id="4b94c-128">下列文字的 hello 是簡單的 U-SQL 指令碼。</span><span class="sxs-lookup"><span data-stu-id="4b94c-128">hello following text is a simple U-SQL script.</span></span> <span data-ttu-id="4b94c-129">它會定義小型資料集和資料集 toohello 預設 Data Lake Store 檔案呼叫寫入`/data.csv`。</span><span class="sxs-lookup"><span data-stu-id="4b94c-129">It defines a small dataset and writes that dataset toohello default Data Lake Store as a file called `/data.csv`.</span></span>

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

### <a name="submit-a-data-lake-analytics-job"></a><span data-ttu-id="4b94c-130">提交資料湖分析作業</span><span class="sxs-lookup"><span data-stu-id="4b94c-130">Submit a Data Lake Analytics job</span></span>

1. <span data-ttu-id="4b94c-131">選取 [檔案] > [新增] > [專案]。</span><span class="sxs-lookup"><span data-stu-id="4b94c-131">Select **File** > **New** > **Project**.</span></span>

2. <span data-ttu-id="4b94c-132">選取 hello **U-SQL 專案**輸入，然後再按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="4b94c-132">Select hello **U-SQL Project** type, and then click **OK**.</span></span> <span data-ttu-id="4b94c-133">Visual Studio 會建立具有 **Script.usql** 檔案的解決方案。</span><span class="sxs-lookup"><span data-stu-id="4b94c-133">Visual Studio creates a solution with a **Script.usql** file.</span></span>

3. <span data-ttu-id="4b94c-134">Hello 先前的指令碼貼到 hello **Script.usql**視窗。</span><span class="sxs-lookup"><span data-stu-id="4b94c-134">Paste hello previous script into hello **Script.usql** window.</span></span>

4. <span data-ttu-id="4b94c-135">在 [hello 左上角的 hello **Script.usql**視窗中，指定 hello Data Lake Analytics 帳戶。</span><span class="sxs-lookup"><span data-stu-id="4b94c-135">In hello upper-left corner of hello **Script.usql** window, specify hello Data Lake Analytics account.</span></span>

    ![提交 U-SQL Visual Studio 專案](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-submit-job.png)

5. <span data-ttu-id="4b94c-137">在 [hello 左上角的 hello **Script.usql**視窗中，選取**送出**。</span><span class="sxs-lookup"><span data-stu-id="4b94c-137">In hello upper-left corner of hello **Script.usql** window, select **Submit**.</span></span>
6. <span data-ttu-id="4b94c-138">確認 hello **Analytics 帳戶**，然後選取**送出**。</span><span class="sxs-lookup"><span data-stu-id="4b94c-138">Verify hello **Analytics Account**, and then select **Submit**.</span></span> <span data-ttu-id="4b94c-139">Hello 提交完成後使用 hello 資料湖 Tools for Visual Studio 結果中提交的結果。</span><span class="sxs-lookup"><span data-stu-id="4b94c-139">Submission results are available in hello Data Lake Tools for Visual Studio Results after hello submission is complete.</span></span>

    ![提交 U-SQL Visual Studio 專案](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-submit-job-advanced.png)
7. <span data-ttu-id="4b94c-141">toosee hello 最新作業的狀態和重新整理 hello 畫面上，按一下 [**重新整理**。</span><span class="sxs-lookup"><span data-stu-id="4b94c-141">toosee hello latest job status and refresh hello screen, click **Refresh**.</span></span> <span data-ttu-id="4b94c-142">Hello 作業成功時，它會顯示 hello**作業圖形**，**中繼資料作業**，**狀態記錄**，和**診斷**:</span><span class="sxs-lookup"><span data-stu-id="4b94c-142">When hello job succeeds, it shows hello **Job Graph**, **MetaData Operations**, **State History**, and **Diagnostics**:</span></span>

    ![U SQL Visual Studio Data Lake Analytics 工作效能圖表](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-performance-graph.png)

   * <span data-ttu-id="4b94c-144">**工作摘要**顯示 hello hello 工作的摘要。</span><span class="sxs-lookup"><span data-stu-id="4b94c-144">**Job Summary** shows hello summary of hello job.</span></span>   
   * <span data-ttu-id="4b94c-145">**工作詳細資料**顯示 hello 工作，其中包括 hello 指令碼、 資源和頂點的其他特定資訊。</span><span class="sxs-lookup"><span data-stu-id="4b94c-145">**Job Details** shows more specific information about hello job, including hello script, resources, and vertices.</span></span>
   * <span data-ttu-id="4b94c-146">**作業圖形**視覺化 hello hello 作業進度。</span><span class="sxs-lookup"><span data-stu-id="4b94c-146">**Job Graph** visualizes hello progress of hello job.</span></span>
   * <span data-ttu-id="4b94c-147">**中繼資料作業**顯示 hello U-SQL 目錄上所執行的所有 hello 動作。</span><span class="sxs-lookup"><span data-stu-id="4b94c-147">**MetaData Operations** shows all hello actions that were taken on hello U-SQL catalog.</span></span>
   * <span data-ttu-id="4b94c-148">**資料**顯示所有 hello 輸入和輸出。</span><span class="sxs-lookup"><span data-stu-id="4b94c-148">**Data** shows all hello inputs and outputs.</span></span>
   * <span data-ttu-id="4b94c-149">**診斷**會提供作業執行和效能最佳化的進階分析。</span><span class="sxs-lookup"><span data-stu-id="4b94c-149">**Diagnostics** provides an advanced analysis for job execution and performance optimization.</span></span>

### <a name="toocheck-job-state"></a><span data-ttu-id="4b94c-150">toocheck 工作狀態</span><span class="sxs-lookup"><span data-stu-id="4b94c-150">toocheck job state</span></span>

1. <span data-ttu-id="4b94c-151">在 [伺服器總管] 中，選取 **Azure** > **Data Lake Analytics**。</span><span class="sxs-lookup"><span data-stu-id="4b94c-151">In Server Explorer, select **Azure** > **Data Lake Analytics**.</span></span> 
2. <span data-ttu-id="4b94c-152">展開 hello Data Lake Analytics 帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="4b94c-152">Expand hello Data Lake Analytics account name.</span></span>
3. <span data-ttu-id="4b94c-153">按兩下 [作業]。</span><span class="sxs-lookup"><span data-stu-id="4b94c-153">Double-click **Jobs**.</span></span>
4. <span data-ttu-id="4b94c-154">選取您先前送出 hello 工作。</span><span class="sxs-lookup"><span data-stu-id="4b94c-154">Select hello job that you previously submitted.</span></span>

### <a name="toosee-hello-output-of-a-job"></a><span data-ttu-id="4b94c-155">工作的 toosee hello 輸出</span><span class="sxs-lookup"><span data-stu-id="4b94c-155">toosee hello output of a job</span></span>

1. <span data-ttu-id="4b94c-156">在 [伺服器總管瀏覽 toohello 您提交的工作。</span><span class="sxs-lookup"><span data-stu-id="4b94c-156">In Server Explorer, browse toohello job you submitted.</span></span>
2. <span data-ttu-id="4b94c-157">按一下 hello**資料**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="4b94c-157">Click hello **Data** tab.</span></span>
3. <span data-ttu-id="4b94c-158">在 [hello**作業輸出**索引標籤，選取 hello`"/data.csv"`檔案。</span><span class="sxs-lookup"><span data-stu-id="4b94c-158">In hello **Job Outputs** tab, select hello `"/data.csv"` file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4b94c-159">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4b94c-159">Next steps</span></span>

* [<span data-ttu-id="4b94c-160">在您自己的工作站上執行 U-SQL 指令碼進行測試和偵錯</span><span class="sxs-lookup"><span data-stu-id="4b94c-160">Run U-SQL scripts on your own workstation for testing and debugging</span></span>](data-lake-analytics-data-lake-tools-local-run.md)
* [<span data-ttu-id="4b94c-161">在 U-SQL 作業中進行 C# 程式碼偵錯</span><span class="sxs-lookup"><span data-stu-id="4b94c-161">Debug C# code in U-SQL jobs</span></span>](data-lake-analytics-debug-u-sql-jobs.md)
* [<span data-ttu-id="4b94c-162">使用 hello Azure 資料湖 Tools for Visual Studio 程式碼</span><span class="sxs-lookup"><span data-stu-id="4b94c-162">Use hello Azure Data Lake Tools for Visual Studio Code</span></span>](data-lake-analytics-data-lake-tools-for-vscode.md)
