---
title: "使用適用於 Visual Studio 的 Data Lake 工具開發 U-SQL 指令碼 | Microsoft Docs"
description: "了解如何安裝適用於 Visual Studio 的 Data Lake 工具，如何開發和測試 U-SQL 指令碼。"
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
ms.openlocfilehash: 7bbbb08ff635477a88403a3ae6bd3486d31838ef
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="develop-u-sql-scripts-by-using-data-lake-tools-for-visual-studio"></a><span data-ttu-id="21fab-103">使用適用於 Visual Studio 的 Data Lake 工具來開發 U-SQL 指令碼</span><span class="sxs-lookup"><span data-stu-id="21fab-103">Develop U-SQL scripts by using Data Lake Tools for Visual Studio</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]


<span data-ttu-id="21fab-104">了解如何使用 Visual Studio 建立 Azure Data Lake Analytics 帳戶、在 [U-SQL](data-lake-analytics-u-sql-get-started.md) 中定義作業，以及將作業提交至 Data Lake Analytics 服務。</span><span class="sxs-lookup"><span data-stu-id="21fab-104">Learn how to use Visual Studio to create Azure Data Lake Analytics accounts, define jobs in [U-SQL](data-lake-analytics-u-sql-get-started.md), and submit jobs to the Data Lake Analytics service.</span></span> <span data-ttu-id="21fab-105">如需有關 Data Lake Analytics 的詳細資訊，請參閱 [Azure Data Lake Analytics 概觀](data-lake-analytics-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="21fab-105">For more information about Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="21fab-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="21fab-106">Prerequisites</span></span>

* <span data-ttu-id="21fab-107">**Visual Studio**：支援 Express 以外的所有版本。</span><span class="sxs-lookup"><span data-stu-id="21fab-107">**Visual Studio**: All editions except Express are supported.</span></span>
    * <span data-ttu-id="21fab-108">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="21fab-108">Visual Studio 2017</span></span>
    * <span data-ttu-id="21fab-109">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="21fab-109">Visual Studio 2015</span></span>
    * <span data-ttu-id="21fab-110">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="21fab-110">Visual Studio 2013</span></span>
* <span data-ttu-id="21fab-111">**Microsoft Azure SDK for .NET** 2.7.1 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="21fab-111">**Microsoft Azure SDK for .NET** version 2.7.1 or later.</span></span>  <span data-ttu-id="21fab-112">使用 [Web Platform Installer](http://www.microsoft.com/web/downloads/platform.aspx) 來進行安裝。</span><span class="sxs-lookup"><span data-stu-id="21fab-112">Install it by using the [Web platform installer](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
* <span data-ttu-id="21fab-113">**Data Lake Analytics** 帳戶。</span><span class="sxs-lookup"><span data-stu-id="21fab-113">A **Data Lake Analytics** account.</span></span> <span data-ttu-id="21fab-114">如需建立帳戶，請參閱[使用 Azure 入口網站開始使用 Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="21fab-114">To create an account, see [Get Started with Azure Data Lake Analytics using Azure portal](data-lake-analytics-get-started-portal.md).</span></span>

## <a name="install-azure-data-lake-tools-for-visual-studio"></a><span data-ttu-id="21fab-115">安裝 Azure Data Lake Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="21fab-115">Install Azure Data Lake Tools for Visual Studio</span></span> 

<span data-ttu-id="21fab-116">[從下載中心](http://aka.ms/adltoolsvs)下載並安裝 Azure Data Lake Tools for Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="21fab-116">Download and install Azure Data Lake Tools for Visual Studio [from the Download Center](http://aka.ms/adltoolsvs).</span></span> <span data-ttu-id="21fab-117">安裝後，請注意：</span><span class="sxs-lookup"><span data-stu-id="21fab-117">After installation, note that:</span></span>
* <span data-ttu-id="21fab-118">**伺服器總管** > **Azure** 節點包含 **Data Lake Analytics** 節點。</span><span class="sxs-lookup"><span data-stu-id="21fab-118">The **Server Explorer** > **Azure** node contains a **Data Lake Analytics** node.</span></span> 
* <span data-ttu-id="21fab-119">[工具] 功能表包含 [Data Lake] 項目。</span><span class="sxs-lookup"><span data-stu-id="21fab-119">The **Tools** menu has a **Data Lake** item.</span></span>

## <a name="connect-to-an-azure-data-lake-analytics-account"></a><span data-ttu-id="21fab-120">連線至 Azure Data Lake Analytics 帳戶</span><span class="sxs-lookup"><span data-stu-id="21fab-120">Connect to an Azure Data Lake Analytics account</span></span>

1. <span data-ttu-id="21fab-121">開啟 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="21fab-121">Open Visual Studio.</span></span>
2. <span data-ttu-id="21fab-122">選取 [檢視] > [伺服器總管] 可開啟伺服器總管。</span><span class="sxs-lookup"><span data-stu-id="21fab-122">Open Server Explorer by selecting **View** > **Server Explorer**.</span></span>
3. <span data-ttu-id="21fab-123">以滑鼠右鍵按一下 [Azure]。</span><span class="sxs-lookup"><span data-stu-id="21fab-123">Right-click **Azure**.</span></span> <span data-ttu-id="21fab-124">然後選取 [連線到 Microsoft Azure 訂用帳戶]並遵循指示進行。</span><span class="sxs-lookup"><span data-stu-id="21fab-124">Then select **Connect to Microsoft Azure Subscription** and follow the instructions.</span></span>
4. <span data-ttu-id="21fab-125">在 [伺服器總管] 中，選取 **Azure** > **Data Lake Analytics**。</span><span class="sxs-lookup"><span data-stu-id="21fab-125">In Server Explorer, select **Azure** > **Data Lake Analytics**.</span></span> <span data-ttu-id="21fab-126">您會看到 Data Lake Analytics 帳戶的清單。</span><span class="sxs-lookup"><span data-stu-id="21fab-126">You see a list of your Data Lake Analytics accounts.</span></span>


## <a name="write-your-first-u-sql-script"></a><span data-ttu-id="21fab-127">撰寫第一個 U-SQL 指令碼</span><span class="sxs-lookup"><span data-stu-id="21fab-127">Write your first U-SQL script</span></span>

<span data-ttu-id="21fab-128">下列文字是簡單的 U-SQL 指令碼。</span><span class="sxs-lookup"><span data-stu-id="21fab-128">The following text is a simple U-SQL script.</span></span> <span data-ttu-id="21fab-129">它會定義小型資料集，並將該資料集寫入預設 Data Lake Store 中，作為名為 `/data.csv` 的檔案。</span><span class="sxs-lookup"><span data-stu-id="21fab-129">It defines a small dataset and writes that dataset to the default Data Lake Store as a file called `/data.csv`.</span></span>

```
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    TO "/data.csv"
    USING Outputters.Csv();
```

### <a name="submit-a-data-lake-analytics-job"></a><span data-ttu-id="21fab-130">提交 Data Lake Analytics 作業</span><span class="sxs-lookup"><span data-stu-id="21fab-130">Submit a Data Lake Analytics job</span></span>

1. <span data-ttu-id="21fab-131">選取 [檔案] > [新增] > [專案]。</span><span class="sxs-lookup"><span data-stu-id="21fab-131">Select **File** > **New** > **Project**.</span></span>

2. <span data-ttu-id="21fab-132">選取 [U-SQL 專案] 類型，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="21fab-132">Select the **U-SQL Project** type, and then click **OK**.</span></span> <span data-ttu-id="21fab-133">Visual Studio 會建立具有 **Script.usql** 檔案的解決方案。</span><span class="sxs-lookup"><span data-stu-id="21fab-133">Visual Studio creates a solution with a **Script.usql** file.</span></span>

3. <span data-ttu-id="21fab-134">將先前的指令碼貼上 **Script.usql** 視窗。</span><span class="sxs-lookup"><span data-stu-id="21fab-134">Paste the previous script into the **Script.usql** window.</span></span>

4. <span data-ttu-id="21fab-135">在 **Script.usql** 視窗的左上角中，指定 Data Lake Analytics 帳戶。</span><span class="sxs-lookup"><span data-stu-id="21fab-135">In the upper-left corner of the **Script.usql** window, specify the Data Lake Analytics account.</span></span>

    ![提交 U-SQL Visual Studio 專案](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-submit-job.png)

5. <span data-ttu-id="21fab-137">在 **Script.usql** 視窗的左上角中，選取 [提交]。</span><span class="sxs-lookup"><span data-stu-id="21fab-137">In the upper-left corner of the **Script.usql** window, select **Submit**.</span></span>
6. <span data-ttu-id="21fab-138">確認 **Analytics 帳戶**，然後選取 [提交]。</span><span class="sxs-lookup"><span data-stu-id="21fab-138">Verify the **Analytics Account**, and then select **Submit**.</span></span> <span data-ttu-id="21fab-139">提交作業完成時，適用於 Visual Studio 結果的 Data Lake 工具中便會出現提交結果。</span><span class="sxs-lookup"><span data-stu-id="21fab-139">Submission results are available in the Data Lake Tools for Visual Studio Results after the submission is complete.</span></span>

    ![提交 U-SQL Visual Studio 專案](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-submit-job-advanced.png)
7. <span data-ttu-id="21fab-141">按一下 [重新整理]，可查看最新的作業狀態並重新整理畫面。</span><span class="sxs-lookup"><span data-stu-id="21fab-141">To see the latest job status and refresh the screen, click **Refresh**.</span></span> <span data-ttu-id="21fab-142">當作業成功時，它會顯示**作業圖形**、**中繼資料作業**、**狀態記錄**和**診斷**：</span><span class="sxs-lookup"><span data-stu-id="21fab-142">When the job succeeds, it shows the **Job Graph**, **MetaData Operations**, **State History**, and **Diagnostics**:</span></span>

    ![U SQL Visual Studio Data Lake Analytics 工作效能圖表](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-performance-graph.png)

   * <span data-ttu-id="21fab-144">**作業摘要**會顯示作業的摘要。</span><span class="sxs-lookup"><span data-stu-id="21fab-144">**Job Summary** shows the summary of the job.</span></span>   
   * <span data-ttu-id="21fab-145">**作業詳細資料**會顯示更多作業的相關資訊，包括指令碼、資源和頂點。</span><span class="sxs-lookup"><span data-stu-id="21fab-145">**Job Details** shows more specific information about the job, including the script, resources, and vertices.</span></span>
   * <span data-ttu-id="21fab-146">**作業圖形**會以視覺化方式檢視作業的進度。</span><span class="sxs-lookup"><span data-stu-id="21fab-146">**Job Graph** visualizes the progress of the job.</span></span>
   * <span data-ttu-id="21fab-147">**中繼資料作業**會顯示 U-SQL 目錄上所執行的所有動作。</span><span class="sxs-lookup"><span data-stu-id="21fab-147">**MetaData Operations** shows all the actions that were taken on the U-SQL catalog.</span></span>
   * <span data-ttu-id="21fab-148">**資料**會顯示所有的輸入和輸出。</span><span class="sxs-lookup"><span data-stu-id="21fab-148">**Data** shows all the inputs and outputs.</span></span>
   * <span data-ttu-id="21fab-149">**診斷**會提供作業執行和效能最佳化的進階分析。</span><span class="sxs-lookup"><span data-stu-id="21fab-149">**Diagnostics** provides an advanced analysis for job execution and performance optimization.</span></span>

### <a name="to-check-job-state"></a><span data-ttu-id="21fab-150">檢查作業狀態</span><span class="sxs-lookup"><span data-stu-id="21fab-150">To check job state</span></span>

1. <span data-ttu-id="21fab-151">在 [伺服器總管] 中，選取 **Azure** > **Data Lake Analytics**。</span><span class="sxs-lookup"><span data-stu-id="21fab-151">In Server Explorer, select **Azure** > **Data Lake Analytics**.</span></span> 
2. <span data-ttu-id="21fab-152">展開 Data Lake Analytics 帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="21fab-152">Expand the Data Lake Analytics account name.</span></span>
3. <span data-ttu-id="21fab-153">按兩下 [作業]。</span><span class="sxs-lookup"><span data-stu-id="21fab-153">Double-click **Jobs**.</span></span>
4. <span data-ttu-id="21fab-154">選取您先前提交的作業。</span><span class="sxs-lookup"><span data-stu-id="21fab-154">Select the job that you previously submitted.</span></span>

### <a name="to-see-the-output-of-a-job"></a><span data-ttu-id="21fab-155">若要查看作業的輸出</span><span class="sxs-lookup"><span data-stu-id="21fab-155">To see the output of a job</span></span>

1. <span data-ttu-id="21fab-156">在伺服器總管中，瀏覽至您所提交的作業。</span><span class="sxs-lookup"><span data-stu-id="21fab-156">In Server Explorer, browse to the job you submitted.</span></span>
2. <span data-ttu-id="21fab-157">按一下 [資料]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="21fab-157">Click the **Data** tab.</span></span>
3. <span data-ttu-id="21fab-158">在 [作業輸出] 索引標籤中，選取 `"/data.csv"` 檔案。</span><span class="sxs-lookup"><span data-stu-id="21fab-158">In the **Job Outputs** tab, select the `"/data.csv"` file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="21fab-159">後續步驟</span><span class="sxs-lookup"><span data-stu-id="21fab-159">Next steps</span></span>

* [<span data-ttu-id="21fab-160">在您自己的工作站上執行 U-SQL 指令碼進行測試和偵錯</span><span class="sxs-lookup"><span data-stu-id="21fab-160">Run U-SQL scripts on your own workstation for testing and debugging</span></span>](data-lake-analytics-data-lake-tools-local-run.md)
* [<span data-ttu-id="21fab-161">在 U-SQL 作業中進行 C# 程式碼偵錯</span><span class="sxs-lookup"><span data-stu-id="21fab-161">Debug C# code in U-SQL jobs</span></span>](data-lake-analytics-debug-u-sql-jobs.md)
* [<span data-ttu-id="21fab-162">使用 Azure Data Lake Tools for Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="21fab-162">Use the Azure Data Lake Tools for Visual Studio Code</span></span>](data-lake-analytics-data-lake-tools-for-vscode.md)
