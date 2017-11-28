---
title: "對 U-SQL 作業進行偵錯 | Microsoft Docs"
description: "了解如何使用 Visual Studio 對失敗的 U-SQL Vertex 進行偵錯。"
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: jhubbard
editor: cgronlun
ms.assetid: bcd0b01e-1755-4112-8e8a-a5cabdca4df2
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 09/02/2016
ms.author: saveenr
ms.openlocfilehash: 2a77c72d3062272305208934d6406d040266c753
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="debug-user-defined-c-code-for-failed-u-sql-jobs"></a><span data-ttu-id="04b2c-103">對 U-SQL 失敗作業的使用者定義 C# 程式碼進行偵錯</span><span class="sxs-lookup"><span data-stu-id="04b2c-103">Debug user-defined C# code for failed U-SQL jobs</span></span>

<span data-ttu-id="04b2c-104">U-SQL 提供使用 C# 的擴充性模型，所以您可以撰寫程式碼以新增功能，例如自訂擷取程式或減壓器。</span><span class="sxs-lookup"><span data-stu-id="04b2c-104">U-SQL provides an extensibility model using C#, so you can write your code to add functionality such as a custom extractor or reducer.</span></span> <span data-ttu-id="04b2c-105">若要深入了解，請參閱 [U-SQL 程式設計指南](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-u-sql-programmability-guide#use-user-defined-functions-udf)。</span><span class="sxs-lookup"><span data-stu-id="04b2c-105">To learn more, see [U-SQL programmability guide](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-u-sql-programmability-guide#use-user-defined-functions-udf).</span></span> <span data-ttu-id="04b2c-106">在實務上，任何程式碼都可能需要偵錯，而且巨量資料系統可能僅提供有限的執行階段偵錯資訊，例如記錄檔。</span><span class="sxs-lookup"><span data-stu-id="04b2c-106">In practice any code may need debugging, and big data systems may only provide limited runtime debugging information such as log files.</span></span>

<span data-ttu-id="04b2c-107">Azure Data Lake Tools for Visual Studio 提供稱為**頂點失敗偵錯**的功能，可讓您將失敗的作業從雲端複製到本機電腦進行偵錯。</span><span class="sxs-lookup"><span data-stu-id="04b2c-107">Azure Data Lake Tools for Visual Studio provides a feature called **Failed Vertex Debug**, which lets you clone a failed job from the cloud to your local machine for debugging.</span></span> <span data-ttu-id="04b2c-108">本機複本會擷取整個雲端環境，包括任何輸入資料和使用者程式碼。</span><span class="sxs-lookup"><span data-stu-id="04b2c-108">The local clone captures the entire cloud environment, including any input data and user code.</span></span>

<span data-ttu-id="04b2c-109">下列影片示範 Azure Data Lake Tools for Visual Studio 中的頂點失敗偵錯。</span><span class="sxs-lookup"><span data-stu-id="04b2c-109">The following video demonstrates Failed Vertex Debug in Azure Data Lake Tools for Visual Studio.</span></span>

> [!VIDEO https://e0d1.wpc.azureedge.net/80E0D1/OfficeMixProdMediaBlobStorage/asset-d3aeab42-6149-4ecc-b044-aa624901ab32/b0fc0373c8f94f1bb8cd39da1310adb8.mp4?sv=2012-02-12&sr=c&si=a91fad76-cfdd-4513-9668-483de39e739c&sig=K%2FR%2FdnIi9S6P%2FBlB3iLAEV5pYu6OJFBDlQy%2FQtZ7E7M%3D&se=2116-07-19T09:27:30Z&rscd=attachment%3B%20filename%3DDebugyourcustomcodeinUSQLADLA.mp4]
>

> [!NOTE]
> <span data-ttu-id="04b2c-110">如果尚未安裝，Visual Studio 需要下列兩項更新：[Microsoft Visual C++ 2015 可轉散發套件 Update 3](https://www.microsoft.com/en-us/download/details.aspx?id=53840) 和 [Windows 通用 C 執行階段](https://www.microsoft.com/download/details.aspx?id=50410)。</span><span class="sxs-lookup"><span data-stu-id="04b2c-110">Visual Studio requires the following two updates, if they are not already installed: [Microsoft Visual C++ 2015 Redistributable Update 3](https://www.microsoft.com/en-us/download/details.aspx?id=53840) and the [Universal C Runtime for Windows](https://www.microsoft.com/download/details.aspx?id=50410).</span></span>

## <a name="download-failed-vertex-to-local-machine"></a><span data-ttu-id="04b2c-111">將失敗的頂點下載至本機電腦</span><span class="sxs-lookup"><span data-stu-id="04b2c-111">Download failed vertex to local machine</span></span>

<span data-ttu-id="04b2c-112">當您在 Azure Data Lake Tools for Visual Studio 中開啟失敗的作業時，您會看到一個黃色的警示列，[錯誤] 索引標籤中有詳細的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="04b2c-112">When you open a failed job in Azure Data Lake Tools for Visual Studio, you see a yellow alert bar with detailed error messages in the error tab.</span></span>

1. <span data-ttu-id="04b2c-113">按一下 [下載]  以下載所有必要的資源和輸入資料流。</span><span class="sxs-lookup"><span data-stu-id="04b2c-113">Click **Download** to download all the required resources and input streams.</span></span> <span data-ttu-id="04b2c-114">如果下載未完成，請按一下 [重試]。</span><span class="sxs-lookup"><span data-stu-id="04b2c-114">If the download doesn't complete, click **Retry**.</span></span>

2. <span data-ttu-id="04b2c-115">在下載完成後按一下 [開啟]，以產生本機的偵錯環境。</span><span class="sxs-lookup"><span data-stu-id="04b2c-115">Click **Open** after the download completes to generate a local debugging environment.</span></span> <span data-ttu-id="04b2c-116">隨即會自動建立並開啟具有偵錯方案的新 Visual Studio 執行個體。</span><span class="sxs-lookup"><span data-stu-id="04b2c-116">A new Visual Studio instance with a debugging solution is automatically created and opened.</span></span>

![Azure Data Lake Analytics U-SQL 偵錯 Visual Studio 下載 Vertex](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-download-vertex.png)

<span data-ttu-id="04b2c-118">作業可能會包含程式碼後置原始程式檔或已註冊的組件，且這兩種類型有不同的偵錯案例。</span><span class="sxs-lookup"><span data-stu-id="04b2c-118">Jobs may include code-behind source files or registered assemblies, and these two types have different debugging scenarios.</span></span>

- [<span data-ttu-id="04b2c-119">偵錯程式碼後置失敗的作業</span><span class="sxs-lookup"><span data-stu-id="04b2c-119">Debug a failed job with code-behind</span></span>](#debug-job-failed-with-code-behind)
- [<span data-ttu-id="04b2c-120">偵錯組件失敗的作業</span><span class="sxs-lookup"><span data-stu-id="04b2c-120">Debug a failed job with assemblies</span></span>](#debug-job-failed-with-assemblies)


## <a name="debug-job-failed-with-code-behind"></a><span data-ttu-id="04b2c-121">偵錯程式碼後置失敗的作業</span><span class="sxs-lookup"><span data-stu-id="04b2c-121">Debug job failed with code-behind</span></span>

<span data-ttu-id="04b2c-122">如果 U-SQL 作業失敗，而且作業包含使用者程式碼 (U-SQL 專案中通常命名為 `Script.usql.cs`)，原始程式碼會匯入偵錯方案。</span><span class="sxs-lookup"><span data-stu-id="04b2c-122">If a U-SQL job fails, and the job includes user code (typically named `Script.usql.cs` in a U-SQL project), that source code is imported into the debugging solution.</span></span>  <span data-ttu-id="04b2c-123">您可從這裡使用 Visual Studio 偵錯工具 (監看式、變數等等) 對問題進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="04b2c-123">From there you can use the Visual Studio debugging tools (watch, variables, etc.) to troubleshoot the problem.</span></span>

> [!NOTE]
> <span data-ttu-id="04b2c-124">在進行偵錯之前，請確定核取 [例外狀況設定] 視窗中的 [Common Language Runtime 例外狀況] (**Ctrl + Alt + E**)。</span><span class="sxs-lookup"><span data-stu-id="04b2c-124">Before debugging, be sure to check **Common Language Runtime Exceptions** in the Exception Settings window (**Ctrl + Alt + E**).</span></span>

![Azure Data Lake Analytics U-SQL 偵錯 Visual Studio 設定](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-clr-exception-setting.png)

1. <span data-ttu-id="04b2c-126">按 **F5** 執行程式碼後置程式碼。</span><span class="sxs-lookup"><span data-stu-id="04b2c-126">Press **F5** to run the code-behind code.</span></span> <span data-ttu-id="04b2c-127">它會一直執行到被例外狀況停止為止。</span><span class="sxs-lookup"><span data-stu-id="04b2c-127">It will run until it is stopped by an exception.</span></span>

2. <span data-ttu-id="04b2c-128">開啟 `ADLTool_Codebehind.usql.cs` 檔案並設定中斷點，然後按 **F5** 逐步偵錯程式碼。</span><span class="sxs-lookup"><span data-stu-id="04b2c-128">Open the `ADLTool_Codebehind.usql.cs` file and set breakpoints, then press **F5** to debug the code step by step.</span></span>

    ![Azure Data Lake Analytics U-SQL 偵錯例外狀況](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-debug-exception.png)

## <a name="debug-job-failed-with-assemblies"></a><span data-ttu-id="04b2c-130">偵錯組件失敗的作業</span><span class="sxs-lookup"><span data-stu-id="04b2c-130">Debug job failed with assemblies</span></span>

<span data-ttu-id="04b2c-131">如果在 U-SQL 指令碼中使用已註冊的組件，系統就無法自動取得原始程式碼。</span><span class="sxs-lookup"><span data-stu-id="04b2c-131">If you use registered assemblies in your U-SQL script, the system can't get the source code automatically.</span></span> <span data-ttu-id="04b2c-132">在此情況下，請手動將組件的原始程式碼檔案新增至方案。</span><span class="sxs-lookup"><span data-stu-id="04b2c-132">In this case, manually add the assemblies' source code files to the solution.</span></span>

### <a name="configure-the-solution"></a><span data-ttu-id="04b2c-133">設定方案</span><span class="sxs-lookup"><span data-stu-id="04b2c-133">Configure the solution</span></span>

1. <span data-ttu-id="04b2c-134">以滑鼠右鍵按一下 [方案 'VertexDebug'] > [新增] > [現有專案...]，以尋找組件的原始程式碼，並將專案新增至偵錯方案。</span><span class="sxs-lookup"><span data-stu-id="04b2c-134">Right-click **Solution 'VertexDebug' > Add > Existing Project...** to find the assemblies' source code and add the project to the debugging solution.</span></span>

    ![Azure Data Lake Analytics U-SQL 偵錯新增專案](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-add-project-to-debug-solution.png)

2. <span data-ttu-id="04b2c-136">在方案中，以滑鼠右鍵按一下 [LocalVertexHost] > [屬性]，並複製**工作目錄**路徑。</span><span class="sxs-lookup"><span data-stu-id="04b2c-136">Right-click **LocalVertexHost > Properties** in the solution and copy the **Working Directory** path.</span></span>

3. <span data-ttu-id="04b2c-137">以滑鼠右鍵按一下 [組件原始程式碼專案] > [屬性]，選取位於左側的 [建置] 索引標籤，將複製的路徑貼到 [輸出] > [輸出路徑]。</span><span class="sxs-lookup"><span data-stu-id="04b2c-137">Right-Click **assembly source code project > Properties**, select the **Build** tab at left, and paste the copied path as **Output > Output path**.</span></span>

    ![Azure Data Lake Analytics U-SQL 偵錯設定 pdb 路徑](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-set-pdb-path.png)

4. <span data-ttu-id="04b2c-139">按 **Ctrl + Alt + E**，核取 [例外狀況設定] 視窗中的 [Common Language Runtime 例外狀況]。</span><span class="sxs-lookup"><span data-stu-id="04b2c-139">Press **Ctrl + Alt + E**, check **Common Language Runtime Exceptions** in Exception Settings window.</span></span>

### <a name="start-debug"></a><span data-ttu-id="04b2c-140">開始偵錯</span><span class="sxs-lookup"><span data-stu-id="04b2c-140">Start debug</span></span>

1. <span data-ttu-id="04b2c-141">以滑鼠右鍵按一下 [組件原始程式碼專案] > [重建]，將 .pdb 檔案輸出至 `LocalVertexHost` 工作目錄。</span><span class="sxs-lookup"><span data-stu-id="04b2c-141">Right-click **assembly source code project > Rebuild** to output .pdb files to the `LocalVertexHost` working directory.</span></span>

2. <span data-ttu-id="04b2c-142">按 **F5**，專案就會一直執行到被例外狀況停止為止。</span><span class="sxs-lookup"><span data-stu-id="04b2c-142">Press **F5** and the project will run until it is stopped by an exception.</span></span> <span data-ttu-id="04b2c-143">您會看到下列警告訊息，可以放心忽略。</span><span class="sxs-lookup"><span data-stu-id="04b2c-143">You may see the following warning message, which you can safely ignore.</span></span> <span data-ttu-id="04b2c-144">可能需要一分鐘左右才會移至 [偵錯] 畫面。</span><span class="sxs-lookup"><span data-stu-id="04b2c-144">It can take up to a minute to get to the debug screen.</span></span>

    ![Azure Data Lake Analytics U-SQL 偵錯 Visual Studio 警告](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-visual-studio-u-sql-debug-warning.png)

3. <span data-ttu-id="04b2c-146">開啟您的原始程式碼並設定中斷點，然後按 **F5** 逐步偵錯程式碼。</span><span class="sxs-lookup"><span data-stu-id="04b2c-146">Open your source code and set breakpoints, then press **F5** to debug the code step by step.</span></span>

<span data-ttu-id="04b2c-147">您也可以使用 Visual Studio 偵錯工具 (監看式、變數等等) 對問題進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="04b2c-147">You can also use the Visual Studio debugging tools (watch, variables, etc.) to troubleshoot the problem.</span></span>

> [!NOTE]
> <span data-ttu-id="04b2c-148">每次修改程式碼以產生更新的 .pdb 檔案之後，都會重建組件原始程式碼專案。</span><span class="sxs-lookup"><span data-stu-id="04b2c-148">Rebuild the assembly source code project each time after you modify the code to generate updated .pdb files.</span></span>

<span data-ttu-id="04b2c-149">偵錯之後，如果專案成功完成，[輸出] 視窗就會顯示下列訊息：</span><span class="sxs-lookup"><span data-stu-id="04b2c-149">After debugging, if the project completes successfully the output window shows the following message:</span></span>

```
The Program 'LocalVertexHost.exe' has exited with code 0 (0x0).
```

![Azure Data Lake Analytics U-SQL 偵錯成功](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-debug-succeed.png)

## <a name="resubmit-the-job"></a><span data-ttu-id="04b2c-151">重新提交作業</span><span class="sxs-lookup"><span data-stu-id="04b2c-151">Resubmit the job</span></span>

<span data-ttu-id="04b2c-152">完成偵錯之後，請重新提交失敗的作業。</span><span class="sxs-lookup"><span data-stu-id="04b2c-152">Once you have completed debugging, resubmit the failed job.</span></span>

1. <span data-ttu-id="04b2c-153">對於有程式碼後置解決方案的作業，請將 C# 程式碼複製到程式碼後置來源檔 (通常是 `Script.usql.cs`)。</span><span class="sxs-lookup"><span data-stu-id="04b2c-153">For jobs with code-behind solutions, copy your C# code into the code-behind source file (typically `Script.usql.cs`).</span></span>
2. <span data-ttu-id="04b2c-154">對於有組件的作業，請將更新的 .dll 組件登入到 ADLA 資料庫：</span><span class="sxs-lookup"><span data-stu-id="04b2c-154">For jobs with assemblies, register the updated .dll assemblies into your ADLA database:</span></span>
    1. <span data-ttu-id="04b2c-155">從伺服器總管或 Cloud Explorer 展開 [ADLA 帳戶] > [資料庫] 節點。</span><span class="sxs-lookup"><span data-stu-id="04b2c-155">From Server Explorer or Cloud Explorer, expand the **ADLA account > Databases** node.</span></span>
    2. <span data-ttu-id="04b2c-156">以滑鼠右鍵按一下 [組件] 並向 ADLA 資料庫註冊新的 .dll 組件：![Azure Data Lake Analytics U-SQL 偵錯註冊組件](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-register-assembly.png)。</span><span class="sxs-lookup"><span data-stu-id="04b2c-156">Right-click **Assemblies** and register your new .dll assemblies with the ADLA database: ![Azure Data Lake Analytics U-SQL debug register assembly](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-register-assembly.png)</span></span>
3. <span data-ttu-id="04b2c-157">重新提交您的作業。</span><span class="sxs-lookup"><span data-stu-id="04b2c-157">Resubmit your job.</span></span>

## <a name="next-steps"></a><span data-ttu-id="04b2c-158">後續步驟</span><span class="sxs-lookup"><span data-stu-id="04b2c-158">Next steps</span></span>

- [<span data-ttu-id="04b2c-159">U-SQL 可程式性指南</span><span class="sxs-lookup"><span data-stu-id="04b2c-159">U-SQL programmability guide</span></span>](data-lake-analytics-u-sql-programmability-guide.md)
- [<span data-ttu-id="04b2c-160">針對 Azure Data Lake Analytics 作業開發 U-SQL 使用者定義運算子</span><span class="sxs-lookup"><span data-stu-id="04b2c-160">Develop U-SQL User-defined operators for Azure Data Lake Analytics jobs</span></span>](data-lake-analytics-u-sql-develop-user-defined-operators.md)
- [<span data-ttu-id="04b2c-161">教學課程：使用適用於 Visual Studio 的資料湖工具開發 U-SQL 指令碼</span><span class="sxs-lookup"><span data-stu-id="04b2c-161">Tutorial: develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
