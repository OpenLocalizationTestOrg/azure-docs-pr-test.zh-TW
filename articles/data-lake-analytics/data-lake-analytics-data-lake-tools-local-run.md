---
title: "使用本機執行和 Azure Data Lake U-SQL SDK 對 U-SQL 作業進行測試和偵錯 | Microsoft Docs"
description: "了解如何使用 Azure Data Lake Tools for Visual Studio 和 Azure Data Lake U-SQL SDK 在本機工作站上對 U-SQL 作業進行測試和偵錯。"
services: data-lake-analytics
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 66dd58b1-0b28-46d1-aaae-43ee2739ae0a
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 11/15/2016
ms.author: yanacai
ms.openlocfilehash: 771a96df5cc66bac46e7144785be8cc072b57b31
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="test-and-debug-u-sql-jobs-by-using-local-run-and-the-azure-data-lake-u-sql-sdk"></a><span data-ttu-id="4f99f-103">使用本機執行和 Azure Data Lake U-SQL SDK 對 U-SQL 作業進行測試和偵錯</span><span class="sxs-lookup"><span data-stu-id="4f99f-103">Test and debug U-SQL jobs by using local run and the Azure Data Lake U-SQL SDK</span></span>

<span data-ttu-id="4f99f-104">您可以使用 Azure Data Lake Tools for Visual Studio 和 Azure Data Lake U-SQL SDK，和在 Azure Data Lake 服務中一樣地在工作站上執行 U-SQL 作業。</span><span class="sxs-lookup"><span data-stu-id="4f99f-104">You can use Azure Data Lake Tools for Visual Studio and the Azure Data Lake U-SQL SDK to run U-SQL jobs on your workstation, just as you can in the Azure Data Lake service.</span></span> <span data-ttu-id="4f99f-105">這兩個本機執行功能可節省您對 U-SQL 作業進行測試和偵錯的時間。</span><span class="sxs-lookup"><span data-stu-id="4f99f-105">These two local-run features save you time in testing and debugging your U-SQL jobs.</span></span>

## <a name="understand-the-data-root-folder-and-the-file-path"></a><span data-ttu-id="4f99f-106">了解資料根資料夾和檔案路徑</span><span class="sxs-lookup"><span data-stu-id="4f99f-106">Understand the data-root folder and the file path</span></span>

<span data-ttu-id="4f99f-107">本機執行和 U-SQL SDK 兩者都需要資料根資料夾。</span><span class="sxs-lookup"><span data-stu-id="4f99f-107">Both local run and the U-SQL SDK require a data-root folder.</span></span> <span data-ttu-id="4f99f-108">資料根資料夾是本機計算帳戶的「本機存放區」。</span><span class="sxs-lookup"><span data-stu-id="4f99f-108">The data-root folder is a "local store" for the local compute account.</span></span> <span data-ttu-id="4f99f-109">它就相當於 Data Lake Analytics 帳戶的 Azure Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="4f99f-109">It's equivalent to the Azure Data Lake Store account of a Data Lake Analytics account.</span></span> <span data-ttu-id="4f99f-110">切換到不同的資料根資料夾，就如同切換到不同的存放區帳戶。</span><span class="sxs-lookup"><span data-stu-id="4f99f-110">Switching to a different data-root folder is just like switching to a different store account.</span></span> <span data-ttu-id="4f99f-111">如果您想要存取具有不同資料根資料夾的常用共用資料，便必須在指令碼中使用絕對路徑。</span><span class="sxs-lookup"><span data-stu-id="4f99f-111">If you want to access commonly shared data with different data-root folders, you must use absolute paths in your scripts.</span></span> <span data-ttu-id="4f99f-112">或者，您可以在資料根資料夾下建立檔案系統符號連結 (例如 NTFS 上的 **mklink**)，來指向共用資料。</span><span class="sxs-lookup"><span data-stu-id="4f99f-112">Or, create file system symbolic links (for example, **mklink** on NTFS) under the data-root folder to point to the shared data.</span></span>

<span data-ttu-id="4f99f-113">資料根資料夾是用來︰</span><span class="sxs-lookup"><span data-stu-id="4f99f-113">The data-root folder is used to:</span></span>

- <span data-ttu-id="4f99f-114">儲存中繼資料，包括資料庫、資料表，資料表值函式 (TVF)，以及組件。</span><span class="sxs-lookup"><span data-stu-id="4f99f-114">Store metadata, including databases, tables, table-valued functions (TVFs), and assemblies.</span></span>
- <span data-ttu-id="4f99f-115">查詢在 U-SQL 中定義為相對路徑的輸入和輸出路徑。</span><span class="sxs-lookup"><span data-stu-id="4f99f-115">Look up the input and output paths that are defined as relative paths in U-SQL.</span></span> <span data-ttu-id="4f99f-116">使用相對路徑能夠更容易將 U-SQL 專案部署至 Azure。</span><span class="sxs-lookup"><span data-stu-id="4f99f-116">Using relative paths makes it easier to deploy your U-SQL projects to Azure.</span></span>

<span data-ttu-id="4f99f-117">您可以在 U-SQL 指令碼中使用相對路徑和本機絕對路徑。</span><span class="sxs-lookup"><span data-stu-id="4f99f-117">You can use both a relative path and a local absolute path in U-SQL scripts.</span></span> <span data-ttu-id="4f99f-118">相對路徑是相對於指定的資料根資料夾路徑。</span><span class="sxs-lookup"><span data-stu-id="4f99f-118">The relative path is relative to the specified data-root folder path.</span></span> <span data-ttu-id="4f99f-119">我們建議您使用 "/" 做為路徑分隔符號，讓您的指令碼與伺服器端相容。</span><span class="sxs-lookup"><span data-stu-id="4f99f-119">We recommend that you use "/" as the path separator to make your scripts compatible with the server side.</span></span> <span data-ttu-id="4f99f-120">以下是一些相對路徑及其對等絕對路徑的範例。</span><span class="sxs-lookup"><span data-stu-id="4f99f-120">Here are some examples of relative paths and their equivalent absolute paths.</span></span> <span data-ttu-id="4f99f-121">在這些範例中，C:\LocalRunDataRoot 是資料根資料夾。</span><span class="sxs-lookup"><span data-stu-id="4f99f-121">In these examples, C:\LocalRunDataRoot is the data-root folder.</span></span>

|<span data-ttu-id="4f99f-122">相對路徑</span><span class="sxs-lookup"><span data-stu-id="4f99f-122">Relative path</span></span>|<span data-ttu-id="4f99f-123">絕對路徑</span><span class="sxs-lookup"><span data-stu-id="4f99f-123">Absolute path</span></span>|
|-------------|-------------|
|<span data-ttu-id="4f99f-124">/abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="4f99f-124">/abc/def/input.csv</span></span> |<span data-ttu-id="4f99f-125">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="4f99f-125">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="4f99f-126">abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="4f99f-126">abc/def/input.csv</span></span>  |<span data-ttu-id="4f99f-127">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="4f99f-127">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="4f99f-128">D:/abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="4f99f-128">D:/abc/def/input.csv</span></span> |<span data-ttu-id="4f99f-129">D:\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="4f99f-129">D:\abc\def\input.csv</span></span>|

## <a name="use-local-run-from-visual-studio"></a><span data-ttu-id="4f99f-130">從 Visual Studio 使用本機執行</span><span class="sxs-lookup"><span data-stu-id="4f99f-130">Use local run from Visual Studio</span></span>

<span data-ttu-id="4f99f-131">Data Lake Tools for Visual Studio 提供 Visual Studio 中的 U-SQL 本機執行體驗。</span><span class="sxs-lookup"><span data-stu-id="4f99f-131">Data Lake Tools for Visual Studio provides a U-SQL local-run experience in Visual Studio.</span></span> <span data-ttu-id="4f99f-132">透過使用這項功能，您可以︰</span><span class="sxs-lookup"><span data-stu-id="4f99f-132">By using this feature, you can:</span></span>

- <span data-ttu-id="4f99f-133">在本機執行 U-SQL 指令碼及 C# 組件。</span><span class="sxs-lookup"><span data-stu-id="4f99f-133">Run a U-SQL script locally, along with C# assemblies.</span></span>
- <span data-ttu-id="4f99f-134">在本機對 C# 組件進行偵錯。</span><span class="sxs-lookup"><span data-stu-id="4f99f-134">Debug a C# assembly locally.</span></span>
- <span data-ttu-id="4f99f-135">從伺服器總管建立、檢視和刪除 U-SQL 目錄 (本機資料庫、組件、結構描述和資料表)。</span><span class="sxs-lookup"><span data-stu-id="4f99f-135">Create, view, and delete U-SQL catalogs (local databases, assemblies, schemas, and tables) from Server Explorer.</span></span> <span data-ttu-id="4f99f-136">您也可以從伺服器總管中找到本機目錄。</span><span class="sxs-lookup"><span data-stu-id="4f99f-136">You can also find the local catalog also from Server Explorer.</span></span>

    ![Data Lake Tools for Visual Studio 本機執行的本機目錄](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-local-catalog.png)

<span data-ttu-id="4f99f-138">Data Lake Tools 安裝程式會建立 C:\LocalRunRoot 資料夾，做為預設的資料根資料夾。</span><span class="sxs-lookup"><span data-stu-id="4f99f-138">The Data Lake Tools installer creates a C:\LocalRunRoot folder to be used as the default data-root folder.</span></span> <span data-ttu-id="4f99f-139">預設的本機執行平行處理原則是 1。</span><span class="sxs-lookup"><span data-stu-id="4f99f-139">The default local-run parallelism is 1.</span></span>

### <a name="to-configure-local-run-in-visual-studio"></a><span data-ttu-id="4f99f-140">在 Visual Studio 中設定本機執行</span><span class="sxs-lookup"><span data-stu-id="4f99f-140">To configure local run in Visual Studio</span></span>

1. <span data-ttu-id="4f99f-141">開啟 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="4f99f-141">Open Visual Studio.</span></span>
2. <span data-ttu-id="4f99f-142">開啟 [伺服器總管]。</span><span class="sxs-lookup"><span data-stu-id="4f99f-142">Open **Server Explorer**.</span></span>
3. <span data-ttu-id="4f99f-143">展開 [Azure]  >  [Data Lake Analytics]。</span><span class="sxs-lookup"><span data-stu-id="4f99f-143">Expand **Azure** > **Data Lake Analytics**.</span></span>
4. <span data-ttu-id="4f99f-144">按一下 [Data Lake] 功能表，然後按一下 [選項和設定]。</span><span class="sxs-lookup"><span data-stu-id="4f99f-144">Click the **Data Lake** menu, and then click **Options and Settings**.</span></span>
5. <span data-ttu-id="4f99f-145">在左邊的樹狀目錄中，展開 [Azure Data Lake]，然後展開 [一般]。</span><span class="sxs-lookup"><span data-stu-id="4f99f-145">In the left tree, expand **Azure Data Lake**, and then expand **General**.</span></span>

    ![Data Lake Tools for Visual Studio 本機執行的組態設定](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-configure.png)

<span data-ttu-id="4f99f-147">必須要有 Visual Studio U-SQL 專案才能執行本機執行。</span><span class="sxs-lookup"><span data-stu-id="4f99f-147">A Visual Studio U-SQL project is required for performing local run.</span></span> <span data-ttu-id="4f99f-148">這與從 Azure 執行 U-SQL 指令碼不同。</span><span class="sxs-lookup"><span data-stu-id="4f99f-148">This part is different from running U-SQL scripts from Azure.</span></span>

### <a name="to-run-a-u-sql-script-locally"></a><span data-ttu-id="4f99f-149">在本機執行 U-SQL 指令碼</span><span class="sxs-lookup"><span data-stu-id="4f99f-149">To run a U-SQL script locally</span></span>
1. <span data-ttu-id="4f99f-150">從 Visual Studio 開啟您的 U-SQL 專案。</span><span class="sxs-lookup"><span data-stu-id="4f99f-150">From Visual Studio, open your U-SQL project.</span></span>   
2. <span data-ttu-id="4f99f-151">在 [方案總管] 中的 U-SQL 指令碼上按一下滑鼠右鍵，然後按一下 [提交指令碼]。</span><span class="sxs-lookup"><span data-stu-id="4f99f-151">Right-click a U-SQL script in Solution Explorer, and then click **Submit Script**.</span></span>
3. <span data-ttu-id="4f99f-152">選取 [(本機)] 做為要在本機執行指令碼的 Analytics 帳戶。</span><span class="sxs-lookup"><span data-stu-id="4f99f-152">Select **(Local)** as the Analytics account to run your script locally.</span></span>
<span data-ttu-id="4f99f-153">您也可以按一下指令碼視窗頂端的 [(本機)] 帳戶，然後按一下 [提交] \(或使用 Ctrl + F5 鍵盤快速鍵)。</span><span class="sxs-lookup"><span data-stu-id="4f99f-153">You can also click the **(Local)** account on the top of script window, and then click **Submit** (or use the Ctrl + F5 keyboard shortcut).</span></span>

    ![Data Lake Tools for Visual Studio 本機執行的提交作業](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-submit-job.png)

### <a name="debug-scripts-and-c-assemblies-locally"></a><span data-ttu-id="4f99f-155">在本機偵錯指令碼和 C# 組件</span><span class="sxs-lookup"><span data-stu-id="4f99f-155">Debug scripts and C# assemblies locally</span></span>

<span data-ttu-id="4f99f-156">您可以在無需將 C# 組件提交並註冊至 Azure Data Lake Analytics 服務的情況下，對它進行偵錯。</span><span class="sxs-lookup"><span data-stu-id="4f99f-156">You can debug C# assemblies without submitting and registering it to Azure Data Lake Analytics Service.</span></span> <span data-ttu-id="4f99f-157">您可以在這兩個程式碼後置檔案和參考的 C# 專案中設定中斷點。</span><span class="sxs-lookup"><span data-stu-id="4f99f-157">You can set breakpoints in both the code behind file and in a referenced C# project.</span></span>

#### <a name="to-debug-local-code-in-code-behind-file"></a><span data-ttu-id="4f99f-158">如何為程式碼後置檔案中的本機程式碼偵錯</span><span class="sxs-lookup"><span data-stu-id="4f99f-158">To debug local code in code behind file</span></span>

1. <span data-ttu-id="4f99f-159">在程式碼後置檔案中設定中斷點。</span><span class="sxs-lookup"><span data-stu-id="4f99f-159">Set breakpoints in the code behind file.</span></span>
2. <span data-ttu-id="4f99f-160">按下 F5 以便在本機為指令碼偵錯。</span><span class="sxs-lookup"><span data-stu-id="4f99f-160">Press F5 to debug the script locally.</span></span>

> [!NOTE]
   > <span data-ttu-id="4f99f-161">下列程序僅適用於 Visual Studio 2015。</span><span class="sxs-lookup"><span data-stu-id="4f99f-161">The following procedure only works in Visual Studio 2015.</span></span> <span data-ttu-id="4f99f-162">在舊版 Visual Studio 中，您可能需要手動加入 pdb 檔案。</span><span class="sxs-lookup"><span data-stu-id="4f99f-162">In older Visual Studio you may need to manually add the pdb files.</span></span>  
   >
   >

#### <a name="to-debug-local-code-in-a-referenced-c-project"></a><span data-ttu-id="4f99f-163">如何為參考的 C# 專案中的本機程式碼偵錯</span><span class="sxs-lookup"><span data-stu-id="4f99f-163">To debug local code in a referenced C# project</span></span>

1. <span data-ttu-id="4f99f-164">建立 C# 組件專案，並建置它來產生輸出 dll。</span><span class="sxs-lookup"><span data-stu-id="4f99f-164">Create a C# Assembly project, and build it to generate the output dll.</span></span>
2. <span data-ttu-id="4f99f-165">使用 U-SQL 陳述式來註冊 dll：</span><span class="sxs-lookup"><span data-stu-id="4f99f-165">Register the dll using a U-SQL statement:</span></span>

        CREATE ASSEMBLY assemblyname FROM @"..\..\path\to\output\.dll";
        
3. <span data-ttu-id="4f99f-166">在 C# 程式碼中設定中斷點。</span><span class="sxs-lookup"><span data-stu-id="4f99f-166">Set breakpoints in the C# code.</span></span>
4. <span data-ttu-id="4f99f-167">按下 F5 以便在本機為參考 C# dll 的指令碼偵錯。</span><span class="sxs-lookup"><span data-stu-id="4f99f-167">Press F5 to debug the script with referencing the C# dll locally.</span></span>

## <a name="use-local-run-from-the-data-lake-u-sql-sdk"></a><span data-ttu-id="4f99f-168">從 Data Lake U-SQL SDK 使用本機執行</span><span class="sxs-lookup"><span data-stu-id="4f99f-168">Use local run from the Data Lake U-SQL SDK</span></span>

<span data-ttu-id="4f99f-169">除了使用 Visual Studio 在本機執行 U-SQL 指令碼之外，您可以利用 Azure Data Lake U-SQL SDK，使用命令列和程式設計介面在本機執行 U-SQL 指令碼。</span><span class="sxs-lookup"><span data-stu-id="4f99f-169">In addition to running U-SQL scripts locally by using Visual Studio, you can use the Azure Data Lake U-SQL SDK to run U-SQL scripts locally with command-line and programming interfaces.</span></span> <span data-ttu-id="4f99f-170">這能讓您調整 U-SQL 本機測試。</span><span class="sxs-lookup"><span data-stu-id="4f99f-170">Through these, you can scale your U-SQL local test.</span></span>

<span data-ttu-id="4f99f-171">深入了解 [Azure Data Lake U-SQL SDK](data-lake-analytics-u-sql-sdk.md)。</span><span class="sxs-lookup"><span data-stu-id="4f99f-171">Learn more about [Azure Data Lake U-SQL SDK](data-lake-analytics-u-sql-sdk.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="4f99f-172">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4f99f-172">Next steps</span></span>

* <span data-ttu-id="4f99f-173">若要了解更複雜的查詢，請參閱 [使用 Azure Data Lake Analytics 來分析網站記錄檔](data-lake-analytics-analyze-weblogs.md)。</span><span class="sxs-lookup"><span data-stu-id="4f99f-173">To see a more complex query, see [Analyze website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="4f99f-174">若要檢視作業詳細資料，請參閱[針對 Azure Data Lake Analytics 作業使用作業瀏覽器和作業檢視](data-lake-analytics-data-lake-tools-view-jobs.md)。</span><span class="sxs-lookup"><span data-stu-id="4f99f-174">To view job details, see [Use Job Browser and Job View for Azure Data Lake Analytics jobs](data-lake-analytics-data-lake-tools-view-jobs.md).</span></span>
* <span data-ttu-id="4f99f-175">若要使用頂點執行檢視，請參閱[在 Data Lake Tools for Visual Studio 中使用頂點執行檢視](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md)。</span><span class="sxs-lookup"><span data-stu-id="4f99f-175">To use the vertex execution view, see [Use the Vertex Execution View in Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).</span></span>
