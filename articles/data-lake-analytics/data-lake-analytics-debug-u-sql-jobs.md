---
title: "aaaDebug U-SQL 作業 |Microsoft 文件"
description: "了解如何 toodebug U-SQL 無法使用 Visual Studio 的頂點。"
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
ms.openlocfilehash: 092bffa1a59ed91c5837402d0276447480b923fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="debug-user-defined-c-code-for-failed-u-sql-jobs"></a><span data-ttu-id="6f0f3-103">對 U-SQL 失敗作業的使用者定義 C# 程式碼進行偵錯</span><span class="sxs-lookup"><span data-stu-id="6f0f3-103">Debug user-defined C# code for failed U-SQL jobs</span></span>

<span data-ttu-id="6f0f3-104">U-SQL 提供使用 C# 中，所以您可以撰寫您的程式碼 tooadd 功能，例如自訂擷取程式 」 或減壓器的擴充性模型。</span><span class="sxs-lookup"><span data-stu-id="6f0f3-104">U-SQL provides an extensibility model using C#, so you can write your code tooadd functionality such as a custom extractor or reducer.</span></span> <span data-ttu-id="6f0f3-105">詳細資訊，請參閱 toolearn [U-SQL 程式設計指南](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-u-sql-programmability-guide#use-user-defined-functions-udf)。</span><span class="sxs-lookup"><span data-stu-id="6f0f3-105">toolearn more, see [U-SQL programmability guide](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-u-sql-programmability-guide#use-user-defined-functions-udf).</span></span> <span data-ttu-id="6f0f3-106">在實務上，任何程式碼都可能需要偵錯，而且巨量資料系統可能僅提供有限的執行階段偵錯資訊，例如記錄檔。</span><span class="sxs-lookup"><span data-stu-id="6f0f3-106">In practice any code may need debugging, and big data systems may only provide limited runtime debugging information such as log files.</span></span>

<span data-ttu-id="6f0f3-107">Azure 資料湖 Tools for Visual Studio 提供的功能，稱為**無法偵錯頂點**，可讓您複製失敗的作業，從 偵錯的 hello 雲端 tooyour 本機電腦。</span><span class="sxs-lookup"><span data-stu-id="6f0f3-107">Azure Data Lake Tools for Visual Studio provides a feature called **Failed Vertex Debug**, which lets you clone a failed job from hello cloud tooyour local machine for debugging.</span></span> <span data-ttu-id="6f0f3-108">hello 本機複本擷取 hello 整個雲端環境，包括任何輸入的資料和使用者程式碼。</span><span class="sxs-lookup"><span data-stu-id="6f0f3-108">hello local clone captures hello entire cloud environment, including any input data and user code.</span></span>

<span data-ttu-id="6f0f3-109">hello 下列影片示範失敗頂點偵錯在 Azure Data Lake Tools for Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="6f0f3-109">hello following video demonstrates Failed Vertex Debug in Azure Data Lake Tools for Visual Studio.</span></span>

> [!VIDEO https://e0d1.wpc.azureedge.net/80E0D1/OfficeMixProdMediaBlobStorage/asset-d3aeab42-6149-4ecc-b044-aa624901ab32/b0fc0373c8f94f1bb8cd39da1310adb8.mp4?sv=2012-02-12&sr=c&si=a91fad76-cfdd-4513-9668-483de39e739c&sig=K%2FR%2FdnIi9S6P%2FBlB3iLAEV5pYu6OJFBDlQy%2FQtZ7E7M%3D&se=2116-07-19T09:27:30Z&rscd=attachment%3B%20filename%3DDebugyourcustomcodeinUSQLADLA.mp4]
>

> [!NOTE]
> <span data-ttu-id="6f0f3-110">如果尚未安裝，visual Studio 需要下列兩個更新，hello: [Microsoft Visual c + + 2015年可轉散發套件 Update 3](https://www.microsoft.com/en-us/download/details.aspx?id=53840)和[通用 C 執行階段的 Windows](https://www.microsoft.com/download/details.aspx?id=50410)。</span><span class="sxs-lookup"><span data-stu-id="6f0f3-110">Visual Studio requires hello following two updates, if they are not already installed: [Microsoft Visual C++ 2015 Redistributable Update 3](https://www.microsoft.com/en-us/download/details.aspx?id=53840) and the [Universal C Runtime for Windows](https://www.microsoft.com/download/details.aspx?id=50410).</span></span>

## <a name="download-failed-vertex-toolocal-machine"></a><span data-ttu-id="6f0f3-111">下載失敗頂點 toolocal 機器</span><span class="sxs-lookup"><span data-stu-id="6f0f3-111">Download failed vertex toolocal machine</span></span>

<span data-ttu-id="6f0f3-112">當您開啟失敗的作業在 Azure Data Lake Tools for Visual Studio 時，您會看到一個警示的黃色列，hello 錯誤 索引標籤中的詳細的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="6f0f3-112">When you open a failed job in Azure Data Lake Tools for Visual Studio, you see a yellow alert bar with detailed error messages in hello error tab.</span></span>

1. <span data-ttu-id="6f0f3-113">按一下**下載**toodownload 所有 hello 必要資源和輸入資料流。</span><span class="sxs-lookup"><span data-stu-id="6f0f3-113">Click **Download** toodownload all hello required resources and input streams.</span></span> <span data-ttu-id="6f0f3-114">如果 hello 下載未完成，請按一下**重試**。</span><span class="sxs-lookup"><span data-stu-id="6f0f3-114">If hello download doesn't complete, click **Retry**.</span></span>

2. <span data-ttu-id="6f0f3-115">按一下**開啟**hello 下載完成 toogenerate 本機偵錯環境之後。</span><span class="sxs-lookup"><span data-stu-id="6f0f3-115">Click **Open** after hello download completes toogenerate a local debugging environment.</span></span> <span data-ttu-id="6f0f3-116">隨即會自動建立並開啟具有偵錯方案的新 Visual Studio 執行個體。</span><span class="sxs-lookup"><span data-stu-id="6f0f3-116">A new Visual Studio instance with a debugging solution is automatically created and opened.</span></span>

![Azure Data Lake Analytics U-SQL 偵錯 Visual Studio 下載 Vertex](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-download-vertex.png)

<span data-ttu-id="6f0f3-118">作業可能會包含程式碼後置原始程式檔或已註冊的組件，且這兩種類型有不同的偵錯案例。</span><span class="sxs-lookup"><span data-stu-id="6f0f3-118">Jobs may include code-behind source files or registered assemblies, and these two types have different debugging scenarios.</span></span>

- [<span data-ttu-id="6f0f3-119">偵錯程式碼後置失敗的作業</span><span class="sxs-lookup"><span data-stu-id="6f0f3-119">Debug a failed job with code-behind</span></span>](#debug-job-failed-with-code-behind)
- [<span data-ttu-id="6f0f3-120">偵錯組件失敗的作業</span><span class="sxs-lookup"><span data-stu-id="6f0f3-120">Debug a failed job with assemblies</span></span>](#debug-job-failed-with-assemblies)


## <a name="debug-job-failed-with-code-behind"></a><span data-ttu-id="6f0f3-121">偵錯程式碼後置失敗的作業</span><span class="sxs-lookup"><span data-stu-id="6f0f3-121">Debug job failed with code-behind</span></span>

<span data-ttu-id="6f0f3-122">如果 U SQL 作業失敗，而且 hello 作業會包括使用者程式碼 (通常會命名為`Script.usql.cs`U-SQL 專案中)，程式碼會匯入解決方案進行偵錯的 hello。</span><span class="sxs-lookup"><span data-stu-id="6f0f3-122">If a U-SQL job fails, and hello job includes user code (typically named `Script.usql.cs` in a U-SQL project), that source code is imported into hello debugging solution.</span></span>  <span data-ttu-id="6f0f3-123">您可以從該處使用 hello Visual Studio 偵錯工具 （監看式、 變數等） tootroubleshoot hello 問題。</span><span class="sxs-lookup"><span data-stu-id="6f0f3-123">From there you can use hello Visual Studio debugging tools (watch, variables, etc.) tootroubleshoot hello problem.</span></span>

> [!NOTE]
> <span data-ttu-id="6f0f3-124">偵錯之前，要確定 toocheck **Common Language Runtime 例外**hello 例外狀況設定視窗中 (**Ctrl + Alt + E**)。</span><span class="sxs-lookup"><span data-stu-id="6f0f3-124">Before debugging, be sure toocheck **Common Language Runtime Exceptions** in hello Exception Settings window (**Ctrl + Alt + E**).</span></span>

![Azure Data Lake Analytics U-SQL 偵錯 Visual Studio 設定](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-clr-exception-setting.png)

1. <span data-ttu-id="6f0f3-126">按**F5** toorun hello 程式碼後置程式碼。</span><span class="sxs-lookup"><span data-stu-id="6f0f3-126">Press **F5** toorun hello code-behind code.</span></span> <span data-ttu-id="6f0f3-127">它會一直執行到被例外狀況停止為止。</span><span class="sxs-lookup"><span data-stu-id="6f0f3-127">It will run until it is stopped by an exception.</span></span>

2. <span data-ttu-id="6f0f3-128">開啟 hello`ADLTool_Codebehind.usql.cs`檔案，並設定中斷點，然後按下**F5** toodebug hello 程式碼逐步解說。</span><span class="sxs-lookup"><span data-stu-id="6f0f3-128">Open hello `ADLTool_Codebehind.usql.cs` file and set breakpoints, then press **F5** toodebug hello code step by step.</span></span>

    ![Azure Data Lake Analytics U-SQL 偵錯例外狀況](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-debug-exception.png)

## <a name="debug-job-failed-with-assemblies"></a><span data-ttu-id="6f0f3-130">偵錯組件失敗的作業</span><span class="sxs-lookup"><span data-stu-id="6f0f3-130">Debug job failed with assemblies</span></span>

<span data-ttu-id="6f0f3-131">如果您使用已註冊組件 U-SQL 指令碼中，hello 系統無法自動取得 hello 原始程式碼。</span><span class="sxs-lookup"><span data-stu-id="6f0f3-131">If you use registered assemblies in your U-SQL script, hello system can't get hello source code automatically.</span></span> <span data-ttu-id="6f0f3-132">在此情況下，手動新增 hello 組件的來源檔案 toohello 方案的 code。</span><span class="sxs-lookup"><span data-stu-id="6f0f3-132">In this case, manually add hello assemblies' source code files toohello solution.</span></span>

### <a name="configure-hello-solution"></a><span data-ttu-id="6f0f3-133">設定 hello 解決方案</span><span class="sxs-lookup"><span data-stu-id="6f0f3-133">Configure hello solution</span></span>

1. <span data-ttu-id="6f0f3-134">以滑鼠右鍵按一下**方案 'VertexDebug' > 新增 > 現有專案...** toofind hello 組件的原始程式碼，並加入 hello 專案 toohello 方案進行偵錯。</span><span class="sxs-lookup"><span data-stu-id="6f0f3-134">Right-click **Solution 'VertexDebug' > Add > Existing Project...** toofind hello assemblies' source code and add hello project toohello debugging solution.</span></span>

    ![Azure Data Lake Analytics U-SQL 偵錯新增專案](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-add-project-to-debug-solution.png)

2. <span data-ttu-id="6f0f3-136">以滑鼠右鍵按一下**LocalVertexHost > 屬性**在 hello 方案，並複製 hello**工作目錄**路徑。</span><span class="sxs-lookup"><span data-stu-id="6f0f3-136">Right-click **LocalVertexHost > Properties** in hello solution and copy hello **Working Directory** path.</span></span>

3. <span data-ttu-id="6f0f3-137">以滑鼠右鍵按一下**組件原始程式碼專案 > 屬性**，選取 hello**建置**索引標籤上，在左邊，並貼上複製的 hello 路徑做為**輸出 > 輸出路徑**。</span><span class="sxs-lookup"><span data-stu-id="6f0f3-137">Right-Click **assembly source code project > Properties**, select hello **Build** tab at left, and paste hello copied path as **Output > Output path**.</span></span>

    ![Azure Data Lake Analytics U-SQL 偵錯設定 pdb 路徑](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-set-pdb-path.png)

4. <span data-ttu-id="6f0f3-139">按 **Ctrl + Alt + E**，核取 [例外狀況設定] 視窗中的 [Common Language Runtime 例外狀況]。</span><span class="sxs-lookup"><span data-stu-id="6f0f3-139">Press **Ctrl + Alt + E**, check **Common Language Runtime Exceptions** in Exception Settings window.</span></span>

### <a name="start-debug"></a><span data-ttu-id="6f0f3-140">開始偵錯</span><span class="sxs-lookup"><span data-stu-id="6f0f3-140">Start debug</span></span>

1. <span data-ttu-id="6f0f3-141">以滑鼠右鍵按一下**組件原始程式碼專案 > 重建**toooutput.pdb 檔案 toohello`LocalVertexHost`工作目錄。</span><span class="sxs-lookup"><span data-stu-id="6f0f3-141">Right-click **assembly source code project > Rebuild** toooutput .pdb files toohello `LocalVertexHost` working directory.</span></span>

2. <span data-ttu-id="6f0f3-142">按**F5** hello 專案將會執行直到它已停止的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="6f0f3-142">Press **F5** and hello project will run until it is stopped by an exception.</span></span> <span data-ttu-id="6f0f3-143">您可能會看到下列警告訊息，您可以放心忽略 hello。</span><span class="sxs-lookup"><span data-stu-id="6f0f3-143">You may see hello following warning message, which you can safely ignore.</span></span> <span data-ttu-id="6f0f3-144">它可能會佔用 tooa 分鐘 tooget toohello 偵錯螢幕。</span><span class="sxs-lookup"><span data-stu-id="6f0f3-144">It can take up tooa minute tooget toohello debug screen.</span></span>

    ![Azure Data Lake Analytics U-SQL 偵錯 Visual Studio 警告](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-visual-studio-u-sql-debug-warning.png)

3. <span data-ttu-id="6f0f3-146">開啟您的原始程式碼，並設定中斷點，然後按下**F5** toodebug hello 程式碼逐步解說。</span><span class="sxs-lookup"><span data-stu-id="6f0f3-146">Open your source code and set breakpoints, then press **F5** toodebug hello code step by step.</span></span>

<span data-ttu-id="6f0f3-147">您也可以使用 hello Visual Studio 偵錯工具 （監看式、 變數等） tootroubleshoot hello 問題。</span><span class="sxs-lookup"><span data-stu-id="6f0f3-147">You can also use hello Visual Studio debugging tools (watch, variables, etc.) tootroubleshoot hello problem.</span></span>

> [!NOTE]
> <span data-ttu-id="6f0f3-148">每次修改 hello toogenerate 更新.pdb 檔案之後重建 hello 組件來源的程式碼專案。</span><span class="sxs-lookup"><span data-stu-id="6f0f3-148">Rebuild hello assembly source code project each time after you modify hello code toogenerate updated .pdb files.</span></span>

<span data-ttu-id="6f0f3-149">偵錯之後，如果成功完成 hello 專案 hello [輸出] 視窗會顯示下列訊息的 hello:</span><span class="sxs-lookup"><span data-stu-id="6f0f3-149">After debugging, if hello project completes successfully hello output window shows hello following message:</span></span>

```
hello Program 'LocalVertexHost.exe' has exited with code 0 (0x0).
```

![Azure Data Lake Analytics U-SQL 偵錯成功](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-debug-succeed.png)

## <a name="resubmit-hello-job"></a><span data-ttu-id="6f0f3-151">再重新送出 hello 工作</span><span class="sxs-lookup"><span data-stu-id="6f0f3-151">Resubmit hello job</span></span>

<span data-ttu-id="6f0f3-152">當您完成偵錯時，再重新送出 hello 失敗的作業。</span><span class="sxs-lookup"><span data-stu-id="6f0f3-152">Once you have completed debugging, resubmit hello failed job.</span></span>

1. <span data-ttu-id="6f0f3-153">工作與程式碼後置解決方案、 C# 程式碼複製到 hello 程式碼後置原始程式檔 (通常`Script.usql.cs`)。</span><span class="sxs-lookup"><span data-stu-id="6f0f3-153">For jobs with code-behind solutions, copy your C# code into hello code-behind source file (typically `Script.usql.cs`).</span></span>
2. <span data-ttu-id="6f0f3-154">使用組件的工作、 註冊 ADLA 資料庫 hello 更新.dll 組件：</span><span class="sxs-lookup"><span data-stu-id="6f0f3-154">For jobs with assemblies, register hello updated .dll assemblies into your ADLA database:</span></span>
    1. <span data-ttu-id="6f0f3-155">從伺服器總管或 Cloud Explorer 中，展開 hello **ADLA 帳戶 > 資料庫**節點。</span><span class="sxs-lookup"><span data-stu-id="6f0f3-155">From Server Explorer or Cloud Explorer, expand hello **ADLA account > Databases** node.</span></span>
    2. <span data-ttu-id="6f0f3-156">以滑鼠右鍵按一下**組件**並註冊新的.dll 組件以 hello ADLA 資料庫： ![Azure 資料湖分析 U-SQL 偵錯註冊組件](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-register-assembly.png)</span><span class="sxs-lookup"><span data-stu-id="6f0f3-156">Right-click **Assemblies** and register your new .dll assemblies with hello ADLA database: ![Azure Data Lake Analytics U-SQL debug register assembly](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-register-assembly.png)</span></span>
3. <span data-ttu-id="6f0f3-157">重新提交您的作業。</span><span class="sxs-lookup"><span data-stu-id="6f0f3-157">Resubmit your job.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6f0f3-158">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6f0f3-158">Next steps</span></span>

- [<span data-ttu-id="6f0f3-159">U-SQL 可程式性指南</span><span class="sxs-lookup"><span data-stu-id="6f0f3-159">U-SQL programmability guide</span></span>](data-lake-analytics-u-sql-programmability-guide.md)
- [<span data-ttu-id="6f0f3-160">針對 Azure Data Lake Analytics 作業開發 U-SQL 使用者定義運算子</span><span class="sxs-lookup"><span data-stu-id="6f0f3-160">Develop U-SQL User-defined operators for Azure Data Lake Analytics jobs</span></span>](data-lake-analytics-u-sql-develop-user-defined-operators.md)
- [<span data-ttu-id="6f0f3-161">教學課程：使用適用於 Visual Studio 的資料湖工具開發 U-SQL 指令碼</span><span class="sxs-lookup"><span data-stu-id="6f0f3-161">Tutorial: develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
