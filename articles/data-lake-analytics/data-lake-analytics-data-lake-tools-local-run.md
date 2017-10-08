---
title: "aaaTest 和偵錯 U-SQL 作業使用本機執行和 hello Azure 資料湖 U-SQL SDK |Microsoft 文件"
description: "了解 toouse Azure 資料湖 Tools for Visual Studio 和 hello Azure 資料湖 U-SQL SDK tootest 和 U SQL 偵錯您的本機工作站上的工作。"
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
ms.openlocfilehash: be04558a504acf6a088e207608ee2d4a011d3ffc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="test-and-debug-u-sql-jobs-by-using-local-run-and-hello-azure-data-lake-u-sql-sdk"></a><span data-ttu-id="55f58-103">測試與偵錯使用本機執行和 hello Azure 資料湖 U-SQL SDK U SQL 作業</span><span class="sxs-lookup"><span data-stu-id="55f58-103">Test and debug U-SQL jobs by using local run and hello Azure Data Lake U-SQL SDK</span></span>

<span data-ttu-id="55f58-104">您可以使用 Azure 資料湖 Tools for Visual Studio 和 hello Azure 資料湖 U-SQL SDK toorun U SQL 作業在您的工作站一樣，您可以在 hello Azure 資料湖服務。</span><span class="sxs-lookup"><span data-stu-id="55f58-104">You can use Azure Data Lake Tools for Visual Studio and hello Azure Data Lake U-SQL SDK toorun U-SQL jobs on your workstation, just as you can in hello Azure Data Lake service.</span></span> <span data-ttu-id="55f58-105">這兩個本機執行功能可節省您對 U-SQL 作業進行測試和偵錯的時間。</span><span class="sxs-lookup"><span data-stu-id="55f58-105">These two local-run features save you time in testing and debugging your U-SQL jobs.</span></span>

## <a name="understand-hello-data-root-folder-and-hello-file-path"></a><span data-ttu-id="55f58-106">了解 hello 資料根資料夾和 hello 檔案路徑</span><span class="sxs-lookup"><span data-stu-id="55f58-106">Understand hello data-root folder and hello file path</span></span>

<span data-ttu-id="55f58-107">本機執行和 hello U-SQL SDK 需要資料根資料夾。</span><span class="sxs-lookup"><span data-stu-id="55f58-107">Both local run and hello U-SQL SDK require a data-root folder.</span></span> <span data-ttu-id="55f58-108">hello 資料根資料夾是 hello 本機計算帳戶 「 本機存放區 」。</span><span class="sxs-lookup"><span data-stu-id="55f58-108">hello data-root folder is a "local store" for hello local compute account.</span></span> <span data-ttu-id="55f58-109">它是 Data Lake Analytics 帳戶的對等 toohello Azure Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="55f58-109">It's equivalent toohello Azure Data Lake Store account of a Data Lake Analytics account.</span></span> <span data-ttu-id="55f58-110">切換 tooa 不同的資料根資料夾，就如同切換 tooa 不同儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="55f58-110">Switching tooa different data-root folder is just like switching tooa different store account.</span></span> <span data-ttu-id="55f58-111">如果您想 tooaccess 共用資料使用不同的資料根資料夾，您必須在您的指令碼中使用絕對路徑。</span><span class="sxs-lookup"><span data-stu-id="55f58-111">If you want tooaccess commonly shared data with different data-root folders, you must use absolute paths in your scripts.</span></span> <span data-ttu-id="55f58-112">或者，建立檔案系統中的符號連結 (比方說， **mklink**上 NTFS) 下 hello 資料根資料夾 toopoint toohello 共用資料。</span><span class="sxs-lookup"><span data-stu-id="55f58-112">Or, create file system symbolic links (for example, **mklink** on NTFS) under hello data-root folder toopoint toohello shared data.</span></span>

<span data-ttu-id="55f58-113">hello 資料根資料夾用來：</span><span class="sxs-lookup"><span data-stu-id="55f58-113">hello data-root folder is used to:</span></span>

- <span data-ttu-id="55f58-114">儲存中繼資料，包括資料庫、資料表，資料表值函式 (TVF)，以及組件。</span><span class="sxs-lookup"><span data-stu-id="55f58-114">Store metadata, including databases, tables, table-valued functions (TVFs), and assemblies.</span></span>
- <span data-ttu-id="55f58-115">查閱 hello 輸入和輸出路徑定義為 U SQL 中的相對路徑。</span><span class="sxs-lookup"><span data-stu-id="55f58-115">Look up hello input and output paths that are defined as relative paths in U-SQL.</span></span> <span data-ttu-id="55f58-116">使用相對路徑會更容易 toodeploy 您 U-SQL 專案 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="55f58-116">Using relative paths makes it easier toodeploy your U-SQL projects tooAzure.</span></span>

<span data-ttu-id="55f58-117">您可以在 U-SQL 指令碼中使用相對路徑和本機絕對路徑。</span><span class="sxs-lookup"><span data-stu-id="55f58-117">You can use both a relative path and a local absolute path in U-SQL scripts.</span></span> <span data-ttu-id="55f58-118">hello 相對路徑是相對 toohello 指定的資料根資料夾路徑。</span><span class="sxs-lookup"><span data-stu-id="55f58-118">hello relative path is relative toohello specified data-root folder path.</span></span> <span data-ttu-id="55f58-119">我們建議您使用"/"作為 hello 路徑分隔符號 toomake 相容 hello 伺服器端指令碼。</span><span class="sxs-lookup"><span data-stu-id="55f58-119">We recommend that you use "/" as hello path separator toomake your scripts compatible with hello server side.</span></span> <span data-ttu-id="55f58-120">以下是一些相對路徑及其對等絕對路徑的範例。</span><span class="sxs-lookup"><span data-stu-id="55f58-120">Here are some examples of relative paths and their equivalent absolute paths.</span></span> <span data-ttu-id="55f58-121">在這些範例中，C:\LocalRunDataRoot 會為 hello 資料根資料夾。</span><span class="sxs-lookup"><span data-stu-id="55f58-121">In these examples, C:\LocalRunDataRoot is hello data-root folder.</span></span>

|<span data-ttu-id="55f58-122">相對路徑</span><span class="sxs-lookup"><span data-stu-id="55f58-122">Relative path</span></span>|<span data-ttu-id="55f58-123">絕對路徑</span><span class="sxs-lookup"><span data-stu-id="55f58-123">Absolute path</span></span>|
|-------------|-------------|
|<span data-ttu-id="55f58-124">/abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="55f58-124">/abc/def/input.csv</span></span> |<span data-ttu-id="55f58-125">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="55f58-125">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="55f58-126">abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="55f58-126">abc/def/input.csv</span></span>  |<span data-ttu-id="55f58-127">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="55f58-127">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="55f58-128">D:/abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="55f58-128">D:/abc/def/input.csv</span></span> |<span data-ttu-id="55f58-129">D:\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="55f58-129">D:\abc\def\input.csv</span></span>|

## <a name="use-local-run-from-visual-studio"></a><span data-ttu-id="55f58-130">從 Visual Studio 使用本機執行</span><span class="sxs-lookup"><span data-stu-id="55f58-130">Use local run from Visual Studio</span></span>

<span data-ttu-id="55f58-131">Data Lake Tools for Visual Studio 提供 Visual Studio 中的 U-SQL 本機執行體驗。</span><span class="sxs-lookup"><span data-stu-id="55f58-131">Data Lake Tools for Visual Studio provides a U-SQL local-run experience in Visual Studio.</span></span> <span data-ttu-id="55f58-132">透過使用這項功能，您可以︰</span><span class="sxs-lookup"><span data-stu-id="55f58-132">By using this feature, you can:</span></span>

- <span data-ttu-id="55f58-133">在本機執行 U-SQL 指令碼及 C# 組件。</span><span class="sxs-lookup"><span data-stu-id="55f58-133">Run a U-SQL script locally, along with C# assemblies.</span></span>
- <span data-ttu-id="55f58-134">在本機對 C# 組件進行偵錯。</span><span class="sxs-lookup"><span data-stu-id="55f58-134">Debug a C# assembly locally.</span></span>
- <span data-ttu-id="55f58-135">從伺服器總管建立、檢視和刪除 U-SQL 目錄 (本機資料庫、組件、結構描述和資料表)。</span><span class="sxs-lookup"><span data-stu-id="55f58-135">Create, view, and delete U-SQL catalogs (local databases, assemblies, schemas, and tables) from Server Explorer.</span></span> <span data-ttu-id="55f58-136">您也可以從 [伺服器總管] 也尋找 hello 本機類別目錄。</span><span class="sxs-lookup"><span data-stu-id="55f58-136">You can also find hello local catalog also from Server Explorer.</span></span>

    ![Data Lake Tools for Visual Studio 本機執行的本機目錄](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-local-catalog.png)

<span data-ttu-id="55f58-138">hello 資料湖工具安裝程式會建立做為 hello 預設資料根目錄資料夾 C:\LocalRunRoot 資料夾 toobe。</span><span class="sxs-lookup"><span data-stu-id="55f58-138">hello Data Lake Tools installer creates a C:\LocalRunRoot folder toobe used as hello default data-root folder.</span></span> <span data-ttu-id="55f58-139">hello 預設本機執行平行處理原則是 1。</span><span class="sxs-lookup"><span data-stu-id="55f58-139">hello default local-run parallelism is 1.</span></span>

### <a name="tooconfigure-local-run-in-visual-studio"></a><span data-ttu-id="55f58-140">tooconfigure 本機 Visual Studio 中執行</span><span class="sxs-lookup"><span data-stu-id="55f58-140">tooconfigure local run in Visual Studio</span></span>

1. <span data-ttu-id="55f58-141">開啟 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="55f58-141">Open Visual Studio.</span></span>
2. <span data-ttu-id="55f58-142">開啟 [伺服器總管]。</span><span class="sxs-lookup"><span data-stu-id="55f58-142">Open **Server Explorer**.</span></span>
3. <span data-ttu-id="55f58-143">展開 [Azure]  >  [Data Lake Analytics]。</span><span class="sxs-lookup"><span data-stu-id="55f58-143">Expand **Azure** > **Data Lake Analytics**.</span></span>
4. <span data-ttu-id="55f58-144">按一下 hello **Data Lake**功能表，然後再按一下**選項和設定**。</span><span class="sxs-lookup"><span data-stu-id="55f58-144">Click hello **Data Lake** menu, and then click **Options and Settings**.</span></span>
5. <span data-ttu-id="55f58-145">在 hello 左邊樹狀目錄中，展開**Azure 資料湖**，然後展開**一般**。</span><span class="sxs-lookup"><span data-stu-id="55f58-145">In hello left tree, expand **Azure Data Lake**, and then expand **General**.</span></span>

    ![Data Lake Tools for Visual Studio 本機執行的組態設定](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-configure.png)

<span data-ttu-id="55f58-147">必須要有 Visual Studio U-SQL 專案才能執行本機執行。</span><span class="sxs-lookup"><span data-stu-id="55f58-147">A Visual Studio U-SQL project is required for performing local run.</span></span> <span data-ttu-id="55f58-148">這與從 Azure 執行 U-SQL 指令碼不同。</span><span class="sxs-lookup"><span data-stu-id="55f58-148">This part is different from running U-SQL scripts from Azure.</span></span>

### <a name="toorun-a-u-sql-script-locally"></a><span data-ttu-id="55f58-149">在本機 toorun U-SQL 指令碼</span><span class="sxs-lookup"><span data-stu-id="55f58-149">toorun a U-SQL script locally</span></span>
1. <span data-ttu-id="55f58-150">從 Visual Studio 開啟您的 U-SQL 專案。</span><span class="sxs-lookup"><span data-stu-id="55f58-150">From Visual Studio, open your U-SQL project.</span></span>   
2. <span data-ttu-id="55f58-151">在 方案總管 中的 U-SQL 指令碼上按一下滑鼠右鍵，然後按一下提交指令碼。</span><span class="sxs-lookup"><span data-stu-id="55f58-151">Right-click a U-SQL script in Solution Explorer, and then click **Submit Script**.</span></span>
3. <span data-ttu-id="55f58-152">選取**（本機）**身分 hello Analytics 帳戶 toorun 指令碼在本機。</span><span class="sxs-lookup"><span data-stu-id="55f58-152">Select **(Local)** as hello Analytics account toorun your script locally.</span></span>
<span data-ttu-id="55f58-153">您也可以按一下 hello **（本機）** hello 指令碼視窗頂端的帳戶，然後按一下**送出**（或使用 hello Ctrl + F5 鍵盤快速鍵）。</span><span class="sxs-lookup"><span data-stu-id="55f58-153">You can also click hello **(Local)** account on hello top of script window, and then click **Submit** (or use hello Ctrl + F5 keyboard shortcut).</span></span>

    ![Data Lake Tools for Visual Studio 本機執行的提交作業](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-submit-job.png)

### <a name="debug-scripts-and-c-assemblies-locally"></a><span data-ttu-id="55f58-155">在本機偵錯指令碼和 C# 組件</span><span class="sxs-lookup"><span data-stu-id="55f58-155">Debug scripts and C# assemblies locally</span></span>

<span data-ttu-id="55f58-156">您可以偵錯 C# 組件，而送出，並註冊它 tooAzure 資料湖分析服務。</span><span class="sxs-lookup"><span data-stu-id="55f58-156">You can debug C# assemblies without submitting and registering it tooAzure Data Lake Analytics Service.</span></span> <span data-ttu-id="55f58-157">在這兩個的 hello 程式碼後置檔案中，以及參考的 C# 專案中，您可以設定中斷點。</span><span class="sxs-lookup"><span data-stu-id="55f58-157">You can set breakpoints in both hello code behind file and in a referenced C# project.</span></span>

#### <a name="toodebug-local-code-in-code-behind-file"></a><span data-ttu-id="55f58-158">在程式碼後置檔案 toodebug 本機的程式碼</span><span class="sxs-lookup"><span data-stu-id="55f58-158">toodebug local code in code behind file</span></span>

1. <span data-ttu-id="55f58-159">Hello 程式碼後置檔案中設定中斷點。</span><span class="sxs-lookup"><span data-stu-id="55f58-159">Set breakpoints in hello code behind file.</span></span>
2. <span data-ttu-id="55f58-160">按 F5 toodebug hello 指令碼在本機。</span><span class="sxs-lookup"><span data-stu-id="55f58-160">Press F5 toodebug hello script locally.</span></span>

> [!NOTE]
   > <span data-ttu-id="55f58-161">下列程序只適用於 Visual Studio 2015 中的 hello。</span><span class="sxs-lookup"><span data-stu-id="55f58-161">hello following procedure only works in Visual Studio 2015.</span></span> <span data-ttu-id="55f58-162">在舊版的 Visual Studio 中，您可能需要 toomanually 新增 hello pdb 檔案。</span><span class="sxs-lookup"><span data-stu-id="55f58-162">In older Visual Studio you may need toomanually add hello pdb files.</span></span>  
   >
   >

#### <a name="toodebug-local-code-in-a-referenced-c-project"></a><span data-ttu-id="55f58-163">toodebug 本機程式碼中參考的 C# 專案</span><span class="sxs-lookup"><span data-stu-id="55f58-163">toodebug local code in a referenced C# project</span></span>

1. <span data-ttu-id="55f58-164">建立 C# 組件的專案，並建立該 toogenerate hello 輸出 dll 檔案。</span><span class="sxs-lookup"><span data-stu-id="55f58-164">Create a C# Assembly project, and build it toogenerate hello output dll.</span></span>
2. <span data-ttu-id="55f58-165">註冊 hello dll 使用 U SQL 陳述式：</span><span class="sxs-lookup"><span data-stu-id="55f58-165">Register hello dll using a U-SQL statement:</span></span>

        CREATE ASSEMBLY assemblyname FROM @"..\..\path\to\output\.dll";
        
3. <span data-ttu-id="55f58-166">Hello C# 程式碼中設定中斷點。</span><span class="sxs-lookup"><span data-stu-id="55f58-166">Set breakpoints in hello C# code.</span></span>
4. <span data-ttu-id="55f58-167">按 F5 toodebug hello 指令碼以參考本機 hello C# dll。</span><span class="sxs-lookup"><span data-stu-id="55f58-167">Press F5 toodebug hello script with referencing hello C# dll locally.</span></span>

## <a name="use-local-run-from-hello-data-lake-u-sql-sdk"></a><span data-ttu-id="55f58-168">使用本機執行從 hello 資料湖 U-SQL SDK</span><span class="sxs-lookup"><span data-stu-id="55f58-168">Use local run from hello Data Lake U-SQL SDK</span></span>

<span data-ttu-id="55f58-169">此外 toorunning U-SQL 指令碼在本機上使用 Visual Studio，您可以使用命令列和程式設計介面，在本機使用 hello Azure 資料湖 U-SQL SDK toorun U-SQL 指令碼。</span><span class="sxs-lookup"><span data-stu-id="55f58-169">In addition toorunning U-SQL scripts locally by using Visual Studio, you can use hello Azure Data Lake U-SQL SDK toorun U-SQL scripts locally with command-line and programming interfaces.</span></span> <span data-ttu-id="55f58-170">這能讓您調整 U-SQL 本機測試。</span><span class="sxs-lookup"><span data-stu-id="55f58-170">Through these, you can scale your U-SQL local test.</span></span>

<span data-ttu-id="55f58-171">深入了解 [Azure Data Lake U-SQL SDK](data-lake-analytics-u-sql-sdk.md)。</span><span class="sxs-lookup"><span data-stu-id="55f58-171">Learn more about [Azure Data Lake U-SQL SDK](data-lake-analytics-u-sql-sdk.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="55f58-172">後續步驟</span><span class="sxs-lookup"><span data-stu-id="55f58-172">Next steps</span></span>

* <span data-ttu-id="55f58-173">toosee 更複雜的查詢，請參閱[分析網站記錄檔，使用 Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md)。</span><span class="sxs-lookup"><span data-stu-id="55f58-173">toosee a more complex query, see [Analyze website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="55f58-174">tooview 作業的詳細資訊，請參閱[使用作業瀏覽器和 Azure Data Lake Analytics 工作的工作檢視](data-lake-analytics-data-lake-tools-view-jobs.md)。</span><span class="sxs-lookup"><span data-stu-id="55f58-174">tooview job details, see [Use Job Browser and Job View for Azure Data Lake Analytics jobs](data-lake-analytics-data-lake-tools-view-jobs.md).</span></span>
* <span data-ttu-id="55f58-175">toouse hello 頂點執行檢視，請參閱[使用 hello 頂點資料湖 Tools for Visual Studio 中的執行檢視](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md)。</span><span class="sxs-lookup"><span data-stu-id="55f58-175">toouse hello vertex execution view, see [Use hello Vertex Execution View in Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).</span></span>
