---
title: "aaaScale U-SQL 本機執行和測試 Azure 資料湖 U-SQL sdk |Microsoft 文件"
description: "了解如何 toouse 本機的 Azure 資料湖 U-SQL SDK tooscale U-SQL 作業執行及測試命令列與您的本機工作站上的程式設計介面。"
services: data-lake-analytics
documentationcenter: 
author: 
manager: 
editor: 
ms.assetid: 
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/01/2017
ms.author: yanacai
ms.openlocfilehash: 2b0a16229789268e333f723ff6fc2c3efdc29905
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="scale-u-sql-local-run-and-test-with-azure-data-lake-u-sql-sdk"></a><span data-ttu-id="99598-103">使用 Azure Data Lake U-SQL SDK 調整 U-SQL 本機執行和測試</span><span class="sxs-lookup"><span data-stu-id="99598-103">Scale U-SQL local run and test with Azure Data Lake U-SQL SDK</span></span>

<span data-ttu-id="99598-104">在開發 U-SQL 指令碼時，是通用 toorun，並在本機測試 U-SQL 指令碼之前送出 toocloud。</span><span class="sxs-lookup"><span data-stu-id="99598-104">When developing U-SQL script, it is common toorun and test U-SQL script locally before submit it toocloud.</span></span> <span data-ttu-id="99598-105">Azure Data Lake 針對此案例提供稱為 Azure Data Lake U-SQL SDK 的 Nuget 套件，讓您可以輕鬆地調整 U-SQL 本機執行和測試。</span><span class="sxs-lookup"><span data-stu-id="99598-105">Azure Data Lake provides a Nuget package called Azure Data Lake U-SQL SDK for this scenario, through which you can easily scale U-SQL local run and test.</span></span> <span data-ttu-id="99598-106">它也是可能 toointegrate 此 U-SQL 測試 CI （連續整合） 系統 tooautomate hello 編譯和測試。</span><span class="sxs-lookup"><span data-stu-id="99598-106">It is also possible toointegrate this U-SQL test with CI (Continuous Integration) system tooautomate hello compile and test.</span></span>

<span data-ttu-id="99598-107">如果您在意如何 toomanually 本機執行和偵錯 U-SQL 指令碼的 GUI 工具，則您可以使用 Azure 資料湖 Tools for Visual Studio 的。</span><span class="sxs-lookup"><span data-stu-id="99598-107">If you care about how toomanually local run and debug U-SQL script with GUI tooling, then you can use Azure Data Lake Tools for Visual Studio for that.</span></span> <span data-ttu-id="99598-108">您可以在[這裡](data-lake-analytics-data-lake-tools-local-run.md)深入了解。</span><span class="sxs-lookup"><span data-stu-id="99598-108">You can learn more from [here](data-lake-analytics-data-lake-tools-local-run.md).</span></span>

## <a name="install-azure-data-lake-u-sql-sdk"></a><span data-ttu-id="99598-109">安裝 Azure Data Lake U-SQL SDK</span><span class="sxs-lookup"><span data-stu-id="99598-109">Install Azure Data Lake U-SQL SDK</span></span>

<span data-ttu-id="99598-110">您可以取得 hello Azure 資料湖 U-SQL SDK[這裡](https://www.nuget.org/packages/Microsoft.Azure.DataLake.USQL.SDK/)Nuget.org 上。然後再將它，您需要 toomake 確定您有相依性，如下所示。</span><span class="sxs-lookup"><span data-stu-id="99598-110">You can get hello Azure Data Lake U-SQL SDK [here](https://www.nuget.org/packages/Microsoft.Azure.DataLake.USQL.SDK/) on Nuget.org. And before using it, you need toomake sure you have dependencies as follows.</span></span>

### <a name="dependencies"></a><span data-ttu-id="99598-111">相依項目</span><span class="sxs-lookup"><span data-stu-id="99598-111">Dependencies</span></span>

<span data-ttu-id="99598-112">hello 資料湖 U-SQL SDK 需要下列相依性的 hello:</span><span class="sxs-lookup"><span data-stu-id="99598-112">hello Data Lake U-SQL SDK requires hello following dependencies:</span></span>

- <span data-ttu-id="99598-113">[Microsoft .NET Framework 4.6 或更新版本](https://www.microsoft.com/download/details.aspx?id=17851)。</span><span class="sxs-lookup"><span data-stu-id="99598-113">[Microsoft .NET Framework 4.6 or newer](https://www.microsoft.com/download/details.aspx?id=17851).</span></span>
- <span data-ttu-id="99598-114">Microsoft Visual C++ 14 和 Windows SDK 10.0.10240.0 或更新版本 (在本文中稱為 CppSDK)。</span><span class="sxs-lookup"><span data-stu-id="99598-114">Microsoft Visual C++ 14 and Windows SDK 10.0.10240.0 or newer (which is called CppSDK in this article).</span></span> <span data-ttu-id="99598-115">有兩種方式 tooget CppSDK:</span><span class="sxs-lookup"><span data-stu-id="99598-115">There are two ways tooget CppSDK:</span></span>

    - <span data-ttu-id="99598-116">安裝 [Visual Studio Community 版本](https://developer.microsoft.com/downloads/vs-thankyou)。</span><span class="sxs-lookup"><span data-stu-id="99598-116">Install [Visual Studio Community Edition](https://developer.microsoft.com/downloads/vs-thankyou).</span></span> <span data-ttu-id="99598-117">您必須在 hello Program Files 資料夾，例如，C:\Program Files (x86) \Windows Kits\10\ \Windows Kits\10 資料夾。</span><span class="sxs-lookup"><span data-stu-id="99598-117">You'll have a \Windows Kits\10 folder under hello Program Files folder--for example, C:\Program Files (x86)\Windows Kits\10\.</span></span> <span data-ttu-id="99598-118">您也可以找到下 \Windows Kits\10\Lib hello Windows 10 SDK 版本。</span><span class="sxs-lookup"><span data-stu-id="99598-118">You'll also find hello Windows 10 SDK version under \Windows Kits\10\Lib.</span></span> <span data-ttu-id="99598-119">如果您沒有看到這些資料夾，請重新安裝 Visual Studio 並確定 tooselect hello Windows 10 SDK hello 安裝期間。</span><span class="sxs-lookup"><span data-stu-id="99598-119">If you don’t see these folders, reinstall Visual Studio and be sure tooselect hello Windows 10 SDK during hello installation.</span></span> <span data-ttu-id="99598-120">如果您有這與 Visual Studio 一起安裝，hello U-SQL 本機編譯器會自動找到它。</span><span class="sxs-lookup"><span data-stu-id="99598-120">If you have this installed with Visual Studio, hello U-SQL local compiler will find it automatically.</span></span>

    ![Data Lake Tools for Visual Studio 本機執行的 Windows 10 SDK](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-windows-10-sdk.png)

    - <span data-ttu-id="99598-122">安裝 [Data Lake Tools for Visual Studio](http://aka.ms/adltoolsvs)。</span><span class="sxs-lookup"><span data-stu-id="99598-122">Install [Data Lake Tools for Visual Studio](http://aka.ms/adltoolsvs).</span></span> <span data-ttu-id="99598-123">您可以找到 hello 套裝位於 C:\Program Files (x86) \Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\ADL Tools\X.X.XXXX.X\CppSDK 的 Visual c + + 和 Windows SDK 檔案。</span><span class="sxs-lookup"><span data-stu-id="99598-123">You can find hello prepackaged Visual C++ and Windows SDK files at C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\ADL Tools\X.X.XXXX.X\CppSDK.</span></span> <span data-ttu-id="99598-124">在此情況下，hello U-SQL 本機編譯器無法自動找到 hello 相依性。</span><span class="sxs-lookup"><span data-stu-id="99598-124">In this case, hello U-SQL local compiler cannot find hello dependencies automatically.</span></span> <span data-ttu-id="99598-125">您為它需要 toospecify hello CppSDK 路徑。</span><span class="sxs-lookup"><span data-stu-id="99598-125">You need toospecify hello CppSDK path for it.</span></span> <span data-ttu-id="99598-126">您可以複製 hello 檔案 tooanother 位置，或使用原狀。</span><span class="sxs-lookup"><span data-stu-id="99598-126">You can either copy hello files tooanother location or use it as is.</span></span>

## <a name="understand-basic-concepts"></a><span data-ttu-id="99598-127">了解基本概念</span><span class="sxs-lookup"><span data-stu-id="99598-127">Understand basic concepts</span></span>

### <a name="data-root"></a><span data-ttu-id="99598-128">資料根</span><span class="sxs-lookup"><span data-stu-id="99598-128">Data root</span></span>

<span data-ttu-id="99598-129">hello 資料根資料夾是 hello 本機計算帳戶 「 本機存放區 」。</span><span class="sxs-lookup"><span data-stu-id="99598-129">hello data-root folder is a "local store" for hello local compute account.</span></span> <span data-ttu-id="99598-130">它是 Data Lake Analytics 帳戶的對等 toohello Azure Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="99598-130">It's equivalent toohello Azure Data Lake Store account of a Data Lake Analytics account.</span></span> <span data-ttu-id="99598-131">切換 tooa 不同的資料根資料夾，就如同切換 tooa 不同儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="99598-131">Switching tooa different data-root folder is just like switching tooa different store account.</span></span> <span data-ttu-id="99598-132">如果您想 tooaccess 共用資料使用不同的資料根資料夾，您必須在您的指令碼中使用絕對路徑。</span><span class="sxs-lookup"><span data-stu-id="99598-132">If you want tooaccess commonly shared data with different data-root folders, you must use absolute paths in your scripts.</span></span> <span data-ttu-id="99598-133">或者，建立檔案系統中的符號連結 (比方說， **mklink**上 NTFS) 下 hello 資料根資料夾 toopoint toohello 共用資料。</span><span class="sxs-lookup"><span data-stu-id="99598-133">Or, create file system symbolic links (for example, **mklink** on NTFS) under hello data-root folder toopoint toohello shared data.</span></span>

<span data-ttu-id="99598-134">hello 資料根資料夾用來：</span><span class="sxs-lookup"><span data-stu-id="99598-134">hello data-root folder is used to:</span></span>

- <span data-ttu-id="99598-135">儲存本機中繼資料，包括資料庫、資料表、資料表值函式 (TVF)，以及組件。</span><span class="sxs-lookup"><span data-stu-id="99598-135">Store local metadata, including databases, tables, table-valued functions (TVFs), and assemblies.</span></span>
- <span data-ttu-id="99598-136">查閱 hello 輸入和輸出路徑定義為 U SQL 中的相對路徑。</span><span class="sxs-lookup"><span data-stu-id="99598-136">Look up hello input and output paths that are defined as relative paths in U-SQL.</span></span> <span data-ttu-id="99598-137">使用相對路徑會更容易 toodeploy 您 U-SQL 專案 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="99598-137">Using relative paths makes it easier toodeploy your U-SQL projects tooAzure.</span></span>

### <a name="file-path-in-u-sql"></a><span data-ttu-id="99598-138">U-SQL 中的檔案路徑</span><span class="sxs-lookup"><span data-stu-id="99598-138">File path in U-SQL</span></span>

<span data-ttu-id="99598-139">您可以在 U-SQL 指令碼中使用相對路徑和本機絕對路徑。</span><span class="sxs-lookup"><span data-stu-id="99598-139">You can use both a relative path and a local absolute path in U-SQL scripts.</span></span> <span data-ttu-id="99598-140">hello 相對路徑是相對 toohello 指定的資料根資料夾路徑。</span><span class="sxs-lookup"><span data-stu-id="99598-140">hello relative path is relative toohello specified data-root folder path.</span></span> <span data-ttu-id="99598-141">我們建議您使用"/"作為 hello 路徑分隔符號 toomake 相容 hello 伺服器端指令碼。</span><span class="sxs-lookup"><span data-stu-id="99598-141">We recommend that you use "/" as hello path separator toomake your scripts compatible with hello server side.</span></span> <span data-ttu-id="99598-142">以下是一些相對路徑及其對等絕對路徑的範例。</span><span class="sxs-lookup"><span data-stu-id="99598-142">Here are some examples of relative paths and their equivalent absolute paths.</span></span> <span data-ttu-id="99598-143">在這些範例中，C:\LocalRunDataRoot 會為 hello 資料根資料夾。</span><span class="sxs-lookup"><span data-stu-id="99598-143">In these examples, C:\LocalRunDataRoot is hello data-root folder.</span></span>

|<span data-ttu-id="99598-144">相對路徑</span><span class="sxs-lookup"><span data-stu-id="99598-144">Relative path</span></span>|<span data-ttu-id="99598-145">絕對路徑</span><span class="sxs-lookup"><span data-stu-id="99598-145">Absolute path</span></span>|
|-------------|-------------|
|<span data-ttu-id="99598-146">/abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="99598-146">/abc/def/input.csv</span></span> |<span data-ttu-id="99598-147">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="99598-147">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="99598-148">abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="99598-148">abc/def/input.csv</span></span>  |<span data-ttu-id="99598-149">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="99598-149">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="99598-150">D:/abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="99598-150">D:/abc/def/input.csv</span></span> |<span data-ttu-id="99598-151">D:\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="99598-151">D:\abc\def\input.csv</span></span>|

### <a name="working-directory"></a><span data-ttu-id="99598-152">工作目錄</span><span class="sxs-lookup"><span data-stu-id="99598-152">Working directory</span></span>

<span data-ttu-id="99598-153">當在本機執行 hello U-SQL 指令碼，在目前的執行目錄下的編譯期間建立的工作目錄。</span><span class="sxs-lookup"><span data-stu-id="99598-153">When running hello U-SQL script locally, a working directory is created during compilation under current running directory.</span></span> <span data-ttu-id="99598-154">此外會輸出 toohello 編譯，hello 所需的本機執行的執行階段檔案會陰影複製的 toothis 工作目錄。</span><span class="sxs-lookup"><span data-stu-id="99598-154">In addition toohello compilation outputs, hello needed runtime files for local execution will be shadow copied toothis working directory.</span></span> <span data-ttu-id="99598-155">工作目錄的根資料夾的 hello 稱為 「 ScopeWorkDir"和 hello 工作目錄下的 hello 檔案如下：</span><span class="sxs-lookup"><span data-stu-id="99598-155">hello working directory root folder is called "ScopeWorkDir" and hello files under hello working directory are as follows:</span></span>

|<span data-ttu-id="99598-156">目錄/檔案</span><span class="sxs-lookup"><span data-stu-id="99598-156">Directory/file</span></span>|<span data-ttu-id="99598-157">目錄/檔案</span><span class="sxs-lookup"><span data-stu-id="99598-157">Directory/file</span></span>|<span data-ttu-id="99598-158">目錄/檔案</span><span class="sxs-lookup"><span data-stu-id="99598-158">Directory/file</span></span>|<span data-ttu-id="99598-159">定義</span><span class="sxs-lookup"><span data-stu-id="99598-159">Definition</span></span>|<span data-ttu-id="99598-160">說明</span><span class="sxs-lookup"><span data-stu-id="99598-160">Description</span></span>|
|--------------|--------------|--------------|----------|-----------|
|<span data-ttu-id="99598-161">C6A101DDCB470506</span><span class="sxs-lookup"><span data-stu-id="99598-161">C6A101DDCB470506</span></span>| | |<span data-ttu-id="99598-162">執行階段版本的雜湊字串</span><span class="sxs-lookup"><span data-stu-id="99598-162">Hash string of runtime version</span></span>|<span data-ttu-id="99598-163">陰影複製本機執行所需的執行階段檔案</span><span class="sxs-lookup"><span data-stu-id="99598-163">Shadow copy of runtime files needed for local execution</span></span>|
| |<span data-ttu-id="99598-164">Script_66AE4909AA0ED06C</span><span class="sxs-lookup"><span data-stu-id="99598-164">Script_66AE4909AA0ED06C</span></span>| |<span data-ttu-id="99598-165">指令碼名稱 + 指令碼路徑的雜湊字串</span><span class="sxs-lookup"><span data-stu-id="99598-165">Script name + hash string of script path</span></span>|<span data-ttu-id="99598-166">編譯輸出和執行步驟記錄</span><span class="sxs-lookup"><span data-stu-id="99598-166">Compilation outputs and execution step logging</span></span>|
| | |<span data-ttu-id="99598-167">\_script\_.abr</span><span class="sxs-lookup"><span data-stu-id="99598-167">\_script\_.abr</span></span>|<span data-ttu-id="99598-168">編譯器輸出</span><span class="sxs-lookup"><span data-stu-id="99598-168">Compiler output</span></span>|<span data-ttu-id="99598-169">代數檔案</span><span class="sxs-lookup"><span data-stu-id="99598-169">Algebra file</span></span>|
| | |<span data-ttu-id="99598-170">\_ScopeCodeGen\_.*</span><span class="sxs-lookup"><span data-stu-id="99598-170">\_ScopeCodeGen\_.*</span></span>|<span data-ttu-id="99598-171">編譯器輸出</span><span class="sxs-lookup"><span data-stu-id="99598-171">Compiler output</span></span>|<span data-ttu-id="99598-172">產生的 Managed 程式碼</span><span class="sxs-lookup"><span data-stu-id="99598-172">Generated managed code</span></span>|
| | |<span data-ttu-id="99598-173">\_ScopeCodeGenEngine\_.*</span><span class="sxs-lookup"><span data-stu-id="99598-173">\_ScopeCodeGenEngine\_.*</span></span>|<span data-ttu-id="99598-174">編譯器輸出</span><span class="sxs-lookup"><span data-stu-id="99598-174">Compiler output</span></span>|<span data-ttu-id="99598-175">產生的原生程式碼</span><span class="sxs-lookup"><span data-stu-id="99598-175">Generated native code</span></span>|
| | |<span data-ttu-id="99598-176">參考的組件</span><span class="sxs-lookup"><span data-stu-id="99598-176">referenced assemblies</span></span>|<span data-ttu-id="99598-177">組件參考</span><span class="sxs-lookup"><span data-stu-id="99598-177">Assembly reference</span></span>|<span data-ttu-id="99598-178">參考的組件檔案</span><span class="sxs-lookup"><span data-stu-id="99598-178">Referenced assembly files</span></span>|
| | |<span data-ttu-id="99598-179">deployed_resources</span><span class="sxs-lookup"><span data-stu-id="99598-179">deployed_resources</span></span>|<span data-ttu-id="99598-180">資源部署</span><span class="sxs-lookup"><span data-stu-id="99598-180">Resource deployment</span></span>|<span data-ttu-id="99598-181">資源部署檔案</span><span class="sxs-lookup"><span data-stu-id="99598-181">Resource deployment files</span></span>|
| | |<span data-ttu-id="99598-182">xxxxxxxx.xxx[1..n]\_\*.*</span><span class="sxs-lookup"><span data-stu-id="99598-182">xxxxxxxx.xxx[1..n]\_\*.*</span></span>|<span data-ttu-id="99598-183">執行記錄檔</span><span class="sxs-lookup"><span data-stu-id="99598-183">Execution log</span></span>|<span data-ttu-id="99598-184">執行步驟的記錄檔</span><span class="sxs-lookup"><span data-stu-id="99598-184">Log of execution steps</span></span>|


## <a name="use-hello-sdk-from-hello-command-line"></a><span data-ttu-id="99598-185">從 hello 命令列使用 hello SDK</span><span class="sxs-lookup"><span data-stu-id="99598-185">Use hello SDK from hello command line</span></span>

### <a name="command-line-interface-of-hello-helper-application"></a><span data-ttu-id="99598-186">Hello 協助應用程式的命令列介面</span><span class="sxs-lookup"><span data-stu-id="99598-186">Command-line interface of hello helper application</span></span>

<span data-ttu-id="99598-187">SDK directory\build\runtime 下 LocalRunHelper.exe 是提供介面 toomost hello 常用的本機執行的函式的 hello 協助程式命令列應用程式。</span><span class="sxs-lookup"><span data-stu-id="99598-187">Under SDK directory\build\runtime, LocalRunHelper.exe is hello command-line helper application that provides interfaces toomost of hello commonly used local-run functions.</span></span> <span data-ttu-id="99598-188">請注意，兩者 hello 命令 hello 引數的參數會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="99598-188">Note that both hello command and hello argument switches are case-sensitive.</span></span> <span data-ttu-id="99598-189">tooinvoke 它：</span><span class="sxs-lookup"><span data-stu-id="99598-189">tooinvoke it:</span></span>

    LocalRunHelper.exe <command> <Required-Command-Arguments> [Optional-Command-Arguments]

<span data-ttu-id="99598-190">不使用引數，或以 hello 執行 LocalRunHelper.exe**協助**切換 tooshow hello 說明資訊：</span><span class="sxs-lookup"><span data-stu-id="99598-190">Run LocalRunHelper.exe without arguments or with hello **help** switch tooshow hello help information:</span></span>

    > LocalRunHelper.exe help

        Command 'help' :  Show usage information
        Command 'compile' :  Compile hello script
        Required Arguments :
            -Script param
                    Script File Path
        Optional Arguments :
            -Shallow [default value 'False']
                    Shallow compile

<span data-ttu-id="99598-191">Hello 說明中的資訊：</span><span class="sxs-lookup"><span data-stu-id="99598-191">In hello help information:</span></span>

-  <span data-ttu-id="99598-192">**命令**提供 hello 命令的名稱。</span><span class="sxs-lookup"><span data-stu-id="99598-192">**Command** gives hello command’s name.</span></span>  
-  <span data-ttu-id="99598-193">**Required Argument** 列出必須提供的引數。</span><span class="sxs-lookup"><span data-stu-id="99598-193">**Required Argument** lists arguments that must be supplied.</span></span>  
-  <span data-ttu-id="99598-194">**Optional Argument** 列出選擇性的引數，並具有預設值。</span><span class="sxs-lookup"><span data-stu-id="99598-194">**Optional Argument** lists arguments that are optional, with default values.</span></span>  <span data-ttu-id="99598-195">選擇性布林值的引數並不需要參數，而且其外觀表示負數 tootheir 預設值。</span><span class="sxs-lookup"><span data-stu-id="99598-195">Optional Boolean arguments don’t have parameters, and their appearances mean negative tootheir default value.</span></span>

### <a name="return-value-and-logging"></a><span data-ttu-id="99598-196">傳回值和記錄</span><span class="sxs-lookup"><span data-stu-id="99598-196">Return value and logging</span></span>

<span data-ttu-id="99598-197">hello 協助應用程式會傳回**0**成功和**-1**失敗。</span><span class="sxs-lookup"><span data-stu-id="99598-197">hello helper application returns **0** for success and **-1** for failure.</span></span> <span data-ttu-id="99598-198">根據預設，hello helper 會傳送所有訊息 toohello 目前的主控台。</span><span class="sxs-lookup"><span data-stu-id="99598-198">By default, hello helper sends all messages toohello current console.</span></span> <span data-ttu-id="99598-199">不過，大部分的 hello 命令支援 hello **-MessageOut path_to_log_file** hello 將重新導向的選擇性引數輸出 tooa 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="99598-199">However, most of hello commands support hello **-MessageOut path_to_log_file** optional argument that redirects hello outputs tooa log file.</span></span>

### <a name="environment-variable-configuring"></a><span data-ttu-id="99598-200">環境變數設定</span><span class="sxs-lookup"><span data-stu-id="99598-200">Environment variable configuring</span></span>

<span data-ttu-id="99598-201">U-SQL 本機執行需要指定的資料根做為本機儲存體帳戶，以及針對相依性指定的 CppSDK 路徑。</span><span class="sxs-lookup"><span data-stu-id="99598-201">U-SQL local run needs a specified data root as local storage account, as well as a specified CppSDK path for dependencies.</span></span> <span data-ttu-id="99598-202">您可以為它們的命令列或設定環境變數中的兩個組 hello 引數。</span><span class="sxs-lookup"><span data-stu-id="99598-202">You can both set hello argument in command-line or set environment variable for them.</span></span>

- <span data-ttu-id="99598-203">設定 hello **SCOPE_CPP_SDK**環境變數。</span><span class="sxs-lookup"><span data-stu-id="99598-203">Set hello **SCOPE_CPP_SDK** environment variable.</span></span>

    <span data-ttu-id="99598-204">如果您取得 Microsoft Visual c + + 和 hello Windows SDK 安裝 Data Lake Tools for Visual Studio，請確認您擁有 hello 下列資料夾：</span><span class="sxs-lookup"><span data-stu-id="99598-204">If you get Microsoft Visual C++ and hello Windows SDK by installing Data Lake Tools for Visual Studio, verify that you have hello following folder:</span></span>

        C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\Microsoft Azure Data Lake Tools for Visual Studio 2015\X.X.XXXX.X\CppSDK

    <span data-ttu-id="99598-205">定義新的環境變數，呼叫**SCOPE_CPP_SDK** toopoint toothis 目錄。</span><span class="sxs-lookup"><span data-stu-id="99598-205">Define a new environment variable called **SCOPE_CPP_SDK** toopoint toothis directory.</span></span> <span data-ttu-id="99598-206">或複製 hello 資料夾 toohello 其他位置，並指定**SCOPE_CPP_SDK**的。</span><span class="sxs-lookup"><span data-stu-id="99598-206">Or copy hello folder toohello other location and specify **SCOPE_CPP_SDK** as that.</span></span>

    <span data-ttu-id="99598-207">在加法 toosetting hello 環境變數中，您可以指定 hello **-CppSDK**當您使用 hello 命令列引數。</span><span class="sxs-lookup"><span data-stu-id="99598-207">In addition toosetting hello environment variable, you can specify hello **-CppSDK** argument when you're using hello command line.</span></span> <span data-ttu-id="99598-208">這個引數會覆寫預設的 CppSDK 環境變數。</span><span class="sxs-lookup"><span data-stu-id="99598-208">This argument overwrites your default CppSDK environment variable.</span></span>

- <span data-ttu-id="99598-209">設定 hello **LOCALRUN_DATAROOT**環境變數。</span><span class="sxs-lookup"><span data-stu-id="99598-209">Set hello **LOCALRUN_DATAROOT** environment variable.</span></span>

    <span data-ttu-id="99598-210">定義新的環境變數，呼叫**LOCALRUN_DATAROOT** ，以指 toohello 資料根目錄。</span><span class="sxs-lookup"><span data-stu-id="99598-210">Define a new environment variable called **LOCALRUN_DATAROOT** that points toohello data root.</span></span>

    <span data-ttu-id="99598-211">在加法 toosetting hello 環境變數中，您可以指定 hello **-DataRoot** hello 資料根路徑，當您使用命令列引數。</span><span class="sxs-lookup"><span data-stu-id="99598-211">In addition toosetting hello environment variable, you can specify hello **-DataRoot** argument with hello data-root path when you're using a command line.</span></span> <span data-ttu-id="99598-212">這個引數會覆寫預設的資料根環境變數。</span><span class="sxs-lookup"><span data-stu-id="99598-212">This argument overwrites your default data-root environment variable.</span></span> <span data-ttu-id="99598-213">您需要 tooadd 您正在執行，讓您可以覆寫 hello 預設資料根目錄的所有作業的環境變數的這個引數 tooevery 命令列。</span><span class="sxs-lookup"><span data-stu-id="99598-213">You need tooadd this argument tooevery command line you're running so that you can overwrite hello default data-root environment variable for all operations.</span></span>

### <a name="sdk-command-line-usage-samples"></a><span data-ttu-id="99598-214">SDK 命令列使用範例</span><span class="sxs-lookup"><span data-stu-id="99598-214">SDK command line usage samples</span></span>

#### <a name="compile-and-run"></a><span data-ttu-id="99598-215">編譯和執行</span><span class="sxs-lookup"><span data-stu-id="99598-215">Compile and run</span></span>

<span data-ttu-id="99598-216">hello**執行**命令用來 toocompile hello 指令碼，然後執行 已編譯的結果。</span><span class="sxs-lookup"><span data-stu-id="99598-216">hello **run** command is used toocompile hello script and then execute compiled results.</span></span> <span data-ttu-id="99598-217">其命令列引數結合 **compile** 和 **excute** 的引數。</span><span class="sxs-lookup"><span data-stu-id="99598-217">Its command-line arguments are a combination of those from **compile** and **execute**.</span></span>

    LocalRunHelper run -Script path_to_usql_script.usql [optional_arguments]

<span data-ttu-id="99598-218">hello 以下是選擇性的引數**執行**:</span><span class="sxs-lookup"><span data-stu-id="99598-218">hello following are optional arguments for **run**:</span></span>


|<span data-ttu-id="99598-219">引數</span><span class="sxs-lookup"><span data-stu-id="99598-219">Argument</span></span>|<span data-ttu-id="99598-220">預設值</span><span class="sxs-lookup"><span data-stu-id="99598-220">Default value</span></span>|<span data-ttu-id="99598-221">說明</span><span class="sxs-lookup"><span data-stu-id="99598-221">Description</span></span>|
|--------|-------------|-----------|
|<span data-ttu-id="99598-222">-CodeBehind</span><span class="sxs-lookup"><span data-stu-id="99598-222">-CodeBehind</span></span>|<span data-ttu-id="99598-223">False</span><span class="sxs-lookup"><span data-stu-id="99598-223">False</span></span>|<span data-ttu-id="99598-224">hello 指令碼有.cs 程式碼後置</span><span class="sxs-lookup"><span data-stu-id="99598-224">hello script has .cs code behind</span></span>|
|<span data-ttu-id="99598-225">-CppSDK</span><span class="sxs-lookup"><span data-stu-id="99598-225">-CppSDK</span></span>| |<span data-ttu-id="99598-226">CppSDK 目錄</span><span class="sxs-lookup"><span data-stu-id="99598-226">CppSDK Directory</span></span>|
|<span data-ttu-id="99598-227">-DataRoot</span><span class="sxs-lookup"><span data-stu-id="99598-227">-DataRoot</span></span>| <span data-ttu-id="99598-228">DataRoot 環境變數</span><span class="sxs-lookup"><span data-stu-id="99598-228">DataRoot environment variable</span></span>|<span data-ttu-id="99598-229">本機執行，DataRoot 太預設 'LOCALRUN_DATAROOT' 環境變數</span><span class="sxs-lookup"><span data-stu-id="99598-229">DataRoot for local run, default too'LOCALRUN_DATAROOT' environment variable</span></span>|
|<span data-ttu-id="99598-230">-MessageOut</span><span class="sxs-lookup"><span data-stu-id="99598-230">-MessageOut</span></span>| |<span data-ttu-id="99598-231">傾印主控台 tooa 檔案上的訊息</span><span class="sxs-lookup"><span data-stu-id="99598-231">Dump messages on console tooa file</span></span>|
|<span data-ttu-id="99598-232">-Parallel</span><span class="sxs-lookup"><span data-stu-id="99598-232">-Parallel</span></span>|<span data-ttu-id="99598-233">1</span><span class="sxs-lookup"><span data-stu-id="99598-233">1</span></span>|<span data-ttu-id="99598-234">執行 hello 計劃與 hello 指定平行處理原則</span><span class="sxs-lookup"><span data-stu-id="99598-234">Run hello plan with hello specified parallelism</span></span>|
|<span data-ttu-id="99598-235">-References</span><span class="sxs-lookup"><span data-stu-id="99598-235">-References</span></span>| |<span data-ttu-id="99598-236">清單的路徑 tooextra 參考組件或資料檔案中的程式碼後置，以分隔 ';'</span><span class="sxs-lookup"><span data-stu-id="99598-236">List of paths tooextra reference assemblies or data files of code behind, separated by ';'</span></span>|
|<span data-ttu-id="99598-237">-UdoRedirect</span><span class="sxs-lookup"><span data-stu-id="99598-237">-UdoRedirect</span></span>|<span data-ttu-id="99598-238">False</span><span class="sxs-lookup"><span data-stu-id="99598-238">False</span></span>|<span data-ttu-id="99598-239">產生 Udo 組件重新導向設定</span><span class="sxs-lookup"><span data-stu-id="99598-239">Generate Udo assembly redirect config</span></span>|
|<span data-ttu-id="99598-240">-UseDatabase</span><span class="sxs-lookup"><span data-stu-id="99598-240">-UseDatabase</span></span>|<span data-ttu-id="99598-241">master</span><span class="sxs-lookup"><span data-stu-id="99598-241">master</span></span>|<span data-ttu-id="99598-242">程式碼後置暫存組件註冊資料庫 toouse</span><span class="sxs-lookup"><span data-stu-id="99598-242">Database toouse for code behind temporary assembly registration</span></span>|
|<span data-ttu-id="99598-243">-Verbose</span><span class="sxs-lookup"><span data-stu-id="99598-243">-Verbose</span></span>|<span data-ttu-id="99598-244">False</span><span class="sxs-lookup"><span data-stu-id="99598-244">False</span></span>|<span data-ttu-id="99598-245">顯示詳細的執行階段輸出</span><span class="sxs-lookup"><span data-stu-id="99598-245">Show detailed outputs from runtime</span></span>|
|<span data-ttu-id="99598-246">-WorkDir</span><span class="sxs-lookup"><span data-stu-id="99598-246">-WorkDir</span></span>|<span data-ttu-id="99598-247">目前的目錄</span><span class="sxs-lookup"><span data-stu-id="99598-247">Current Directory</span></span>|<span data-ttu-id="99598-248">編譯器使用方式和輸出的目錄</span><span class="sxs-lookup"><span data-stu-id="99598-248">Directory for compiler usage and outputs</span></span>|
|<span data-ttu-id="99598-249">-RunScopeCEP</span><span class="sxs-lookup"><span data-stu-id="99598-249">-RunScopeCEP</span></span>|<span data-ttu-id="99598-250">0</span><span class="sxs-lookup"><span data-stu-id="99598-250">0</span></span>|<span data-ttu-id="99598-251">ScopeCEP 模式 toouse</span><span class="sxs-lookup"><span data-stu-id="99598-251">ScopeCEP mode toouse</span></span>|
|<span data-ttu-id="99598-252">-ScopeCEPTempPath</span><span class="sxs-lookup"><span data-stu-id="99598-252">-ScopeCEPTempPath</span></span>|<span data-ttu-id="99598-253">temp</span><span class="sxs-lookup"><span data-stu-id="99598-253">temp</span></span>|<span data-ttu-id="99598-254">暫存路徑 toouse 串流處理資料</span><span class="sxs-lookup"><span data-stu-id="99598-254">Temp path toouse for streaming data</span></span>|
|<span data-ttu-id="99598-255">-OptFlags</span><span class="sxs-lookup"><span data-stu-id="99598-255">-OptFlags</span></span>| |<span data-ttu-id="99598-256">最佳化工具旗標的逗號分隔清單</span><span class="sxs-lookup"><span data-stu-id="99598-256">Comma-separated list of optimizer flags</span></span>|


<span data-ttu-id="99598-257">以下是範例：</span><span class="sxs-lookup"><span data-stu-id="99598-257">Here's an example:</span></span>

    LocalRunHelper run -Script d:\test\test1.usql -WorkDir d:\test\bin -CodeBehind -References "d:\asm\ref1.dll;d:\asm\ref2.dll" -UseDatabase testDB –Parallel 5 -Verbose

<span data-ttu-id="99598-258">除了結合**編譯**和**執行**，您可以編譯並分開執行 hello 編譯可執行檔。</span><span class="sxs-lookup"><span data-stu-id="99598-258">Besides combining **compile** and **execute**, you can compile and execute hello compiled executables separately.</span></span>

#### <a name="compile-a-u-sql-script"></a><span data-ttu-id="99598-259">編譯 U-SQL 指令碼</span><span class="sxs-lookup"><span data-stu-id="99598-259">Compile a U-SQL script</span></span>

<span data-ttu-id="99598-260">hello**編譯**命令是使用的 toocompile U-SQL 指令碼 tooexecutables。</span><span class="sxs-lookup"><span data-stu-id="99598-260">hello **compile** command is used toocompile a U-SQL script tooexecutables.</span></span>

    LocalRunHelper compile -Script path_to_usql_script.usql [optional_arguments]

<span data-ttu-id="99598-261">hello 以下是選擇性的引數**編譯**:</span><span class="sxs-lookup"><span data-stu-id="99598-261">hello following are optional arguments for **compile**:</span></span>


|<span data-ttu-id="99598-262">引數</span><span class="sxs-lookup"><span data-stu-id="99598-262">Argument</span></span>|<span data-ttu-id="99598-263">說明</span><span class="sxs-lookup"><span data-stu-id="99598-263">Description</span></span>|
|--------|-----------|
| <span data-ttu-id="99598-264">-CodeBehind [預設值 'False']</span><span class="sxs-lookup"><span data-stu-id="99598-264">-CodeBehind [default value 'False']</span></span>|<span data-ttu-id="99598-265">hello 指令碼有.cs 程式碼後置</span><span class="sxs-lookup"><span data-stu-id="99598-265">hello script has .cs code behind</span></span>|
| <span data-ttu-id="99598-266">-CppSDK [預設值 '']</span><span class="sxs-lookup"><span data-stu-id="99598-266">-CppSDK [default value '']</span></span>|<span data-ttu-id="99598-267">CppSDK 目錄</span><span class="sxs-lookup"><span data-stu-id="99598-267">CppSDK Directory</span></span>|
| <span data-ttu-id="99598-268">-DataRoot [預設值 'DataRoot environment variable']</span><span class="sxs-lookup"><span data-stu-id="99598-268">-DataRoot [default value 'DataRoot environment variable']</span></span>|<span data-ttu-id="99598-269">本機執行，DataRoot 太預設 'LOCALRUN_DATAROOT' 環境變數</span><span class="sxs-lookup"><span data-stu-id="99598-269">DataRoot for local run, default too'LOCALRUN_DATAROOT' environment variable</span></span>|
| <span data-ttu-id="99598-270">-MessageOut [預設值 '']</span><span class="sxs-lookup"><span data-stu-id="99598-270">-MessageOut [default value '']</span></span>|<span data-ttu-id="99598-271">傾印主控台 tooa 檔案上的訊息</span><span class="sxs-lookup"><span data-stu-id="99598-271">Dump messages on console tooa file</span></span>|
| <span data-ttu-id="99598-272">-References [預設值 '']</span><span class="sxs-lookup"><span data-stu-id="99598-272">-References [default value '']</span></span>|<span data-ttu-id="99598-273">清單的路徑 tooextra 參考組件或資料檔案中的程式碼後置，以分隔 ';'</span><span class="sxs-lookup"><span data-stu-id="99598-273">List of paths tooextra reference assemblies or data files of code behind, separated by ';'</span></span>|
| <span data-ttu-id="99598-274">-Shallow [預設值 'False']</span><span class="sxs-lookup"><span data-stu-id="99598-274">-Shallow [default value 'False']</span></span>|<span data-ttu-id="99598-275">淺層編譯</span><span class="sxs-lookup"><span data-stu-id="99598-275">Shallow compile</span></span>|
| <span data-ttu-id="99598-276">-UdoRedirect [預設值 'False']</span><span class="sxs-lookup"><span data-stu-id="99598-276">-UdoRedirect [default value 'False']</span></span>|<span data-ttu-id="99598-277">產生 Udo 組件重新導向設定</span><span class="sxs-lookup"><span data-stu-id="99598-277">Generate Udo assembly redirect config</span></span>|
| <span data-ttu-id="99598-278">-UseDatabase [預設值 'master']</span><span class="sxs-lookup"><span data-stu-id="99598-278">-UseDatabase [default value 'master']</span></span>|<span data-ttu-id="99598-279">程式碼後置暫存組件註冊資料庫 toouse</span><span class="sxs-lookup"><span data-stu-id="99598-279">Database toouse for code behind temporary assembly registration</span></span>|
| <span data-ttu-id="99598-280">-WorkDir [預設值 'Current Directory']</span><span class="sxs-lookup"><span data-stu-id="99598-280">-WorkDir [default value 'Current Directory']</span></span>|<span data-ttu-id="99598-281">編譯器使用方式和輸出的目錄</span><span class="sxs-lookup"><span data-stu-id="99598-281">Directory for compiler usage and outputs</span></span>|
| <span data-ttu-id="99598-282">-RunScopeCEP [預設值 '0']</span><span class="sxs-lookup"><span data-stu-id="99598-282">-RunScopeCEP [default value '0']</span></span>|<span data-ttu-id="99598-283">ScopeCEP 模式 toouse</span><span class="sxs-lookup"><span data-stu-id="99598-283">ScopeCEP mode toouse</span></span>|
| <span data-ttu-id="99598-284">-ScopeCEPTempPath [預設值 'temp']</span><span class="sxs-lookup"><span data-stu-id="99598-284">-ScopeCEPTempPath [default value 'temp']</span></span>|<span data-ttu-id="99598-285">暫存路徑 toouse 串流處理資料</span><span class="sxs-lookup"><span data-stu-id="99598-285">Temp path toouse for streaming data</span></span>|
| <span data-ttu-id="99598-286">-OptFlags [預設值 '']</span><span class="sxs-lookup"><span data-stu-id="99598-286">-OptFlags [default value '']</span></span>|<span data-ttu-id="99598-287">最佳化工具旗標的逗號分隔清單</span><span class="sxs-lookup"><span data-stu-id="99598-287">Comma-separated list of optimizer flags</span></span>|


<span data-ttu-id="99598-288">這裡有一些使用範例。</span><span class="sxs-lookup"><span data-stu-id="99598-288">Here are some usage examples.</span></span>

<span data-ttu-id="99598-289">編譯 U-SQL 指令碼：</span><span class="sxs-lookup"><span data-stu-id="99598-289">Compile a U-SQL script:</span></span>

    LocalRunHelper compile -Script d:\test\test1.usql

<span data-ttu-id="99598-290">編譯 U-SQL 指令碼，並設定 hello 資料根資料夾。</span><span class="sxs-lookup"><span data-stu-id="99598-290">Compile a U-SQL script and set hello data-root folder.</span></span> <span data-ttu-id="99598-291">請注意這會覆寫 hello 設定環境變數。</span><span class="sxs-lookup"><span data-stu-id="99598-291">Note that this will overwrite hello set environment variable.</span></span>

    LocalRunHelper compile -Script d:\test\test1.usql –DataRoot c:\DataRoot

<span data-ttu-id="99598-292">編譯 U-SQL 指令碼並設定工作目錄、參考組件和資料庫：</span><span class="sxs-lookup"><span data-stu-id="99598-292">Compile a U-SQL script and set a working directory, reference assembly, and database:</span></span>

    LocalRunHelper compile -Script d:\test\test1.usql -WorkDir d:\test\bin -References "d:\asm\ref1.dll;d:\asm\ref2.dll" -UseDatabase testDB

#### <a name="execute-compiled-results"></a><span data-ttu-id="99598-293">執行編譯的結果</span><span class="sxs-lookup"><span data-stu-id="99598-293">Execute compiled results</span></span>

<span data-ttu-id="99598-294">hello**執行**命令是使用的 tooexecute 編譯結果。</span><span class="sxs-lookup"><span data-stu-id="99598-294">hello **execute** command is used tooexecute compiled results.</span></span>   

    LocalRunHelper execute -Algebra path_to_compiled_algebra_file [optional_arguments]

<span data-ttu-id="99598-295">hello 以下是選擇性的引數**執行**:</span><span class="sxs-lookup"><span data-stu-id="99598-295">hello following are optional arguments for **execute**:</span></span>

|<span data-ttu-id="99598-296">引數</span><span class="sxs-lookup"><span data-stu-id="99598-296">Argument</span></span>|<span data-ttu-id="99598-297">說明</span><span class="sxs-lookup"><span data-stu-id="99598-297">Description</span></span>|
|--------|-----------|
|<span data-ttu-id="99598-298">-DataRoot [預設值 '']</span><span class="sxs-lookup"><span data-stu-id="99598-298">-DataRoot [default value '']</span></span>|<span data-ttu-id="99598-299">中繼資料執行的資料根。</span><span class="sxs-lookup"><span data-stu-id="99598-299">Data root for metadata execution.</span></span> <span data-ttu-id="99598-300">它會預設 toohello **LOCALRUN_DATAROOT**環境變數。</span><span class="sxs-lookup"><span data-stu-id="99598-300">It defaults toohello **LOCALRUN_DATAROOT** environment variable.</span></span>|
|<span data-ttu-id="99598-301">-MessageOut [預設值 '']</span><span class="sxs-lookup"><span data-stu-id="99598-301">-MessageOut [default value '']</span></span>|<span data-ttu-id="99598-302">傾印 hello 主控台 tooa 檔案上的訊息。</span><span class="sxs-lookup"><span data-stu-id="99598-302">Dump messages on hello console tooa file.</span></span>|
|<span data-ttu-id="99598-303">-Parallel [預設值 '1']</span><span class="sxs-lookup"><span data-stu-id="99598-303">-Parallel [default value '1']</span></span>|<span data-ttu-id="99598-304">指標 toorun hello 產生以 hello 的本機執行步驟指定平行處理原則層級。</span><span class="sxs-lookup"><span data-stu-id="99598-304">Indicator toorun hello generated local-run steps with hello specified parallelism level.</span></span>|
|<span data-ttu-id="99598-305">-Verbose [預設值 'False']</span><span class="sxs-lookup"><span data-stu-id="99598-305">-Verbose [default value 'False']</span></span>|<span data-ttu-id="99598-306">指標 tooshow 詳細的執行階段的輸出。</span><span class="sxs-lookup"><span data-stu-id="99598-306">Indicator tooshow detailed outputs from runtime.</span></span>|

<span data-ttu-id="99598-307">以下是使用範例︰</span><span class="sxs-lookup"><span data-stu-id="99598-307">Here's a usage example:</span></span>

    LocalRunHelper execute -Algebra d:\test\workdir\C6A101DDCB470506\Script_66AE4909AA0ED06C\__script__.abr –DataRoot c:\DataRoot –Parallel 5


## <a name="use-hello-sdk-with-programming-interfaces"></a><span data-ttu-id="99598-308">使用程式設計介面中的 hello SDK</span><span class="sxs-lookup"><span data-stu-id="99598-308">Use hello SDK with programming interfaces</span></span>

<span data-ttu-id="99598-309">hello 程式設計介面都位於 hello LocalRunHelper.exe。</span><span class="sxs-lookup"><span data-stu-id="99598-309">hello programming interfaces are all located in hello LocalRunHelper.exe.</span></span> <span data-ttu-id="99598-310">您可以使用它們的 hello U-SQL SDK toointegrate hello 功能，且 hello C# 測試 framework tooscale U-SQL 指令碼的本機測試。</span><span class="sxs-lookup"><span data-stu-id="99598-310">You can use them toointegrate hello functionality of hello U-SQL SDK and hello C# test framework tooscale your U-SQL script local test.</span></span> <span data-ttu-id="99598-311">在本文中，我將會如何使用 hello 標準 C# 單元測試專案 tooshow toouse 這些介面 tootest U-SQL 指令碼。</span><span class="sxs-lookup"><span data-stu-id="99598-311">In this article, I will use hello standard C# unit test project tooshow how toouse these interfaces tootest your U-SQL script.</span></span>

### <a name="step-1-create-c-unit-test-project-and-configuration"></a><span data-ttu-id="99598-312">步驟 1︰建立 C# 單元測試專案和設定</span><span class="sxs-lookup"><span data-stu-id="99598-312">Step 1: Create C# unit test project and configuration</span></span>

- <span data-ttu-id="99598-313">透過 [檔案] > [新增] > [專案] > [Visual C#] > [測試] > [單元測試專案] 來建立 C# 單元測試專案。</span><span class="sxs-lookup"><span data-stu-id="99598-313">Create a C# unit test project through File > New > Project > Visual C# > Test > Unit Test Project.</span></span>
- <span data-ttu-id="99598-314">新增 LocalRunHelper.exe hello 專案的參考。</span><span class="sxs-lookup"><span data-stu-id="99598-314">Add LocalRunHelper.exe as a reference for hello project.</span></span> <span data-ttu-id="99598-315">hello LocalRunHelper.exe 位於 \build\runtime\LocalRunHelper.exe Nuget 封裝中。</span><span class="sxs-lookup"><span data-stu-id="99598-315">hello LocalRunHelper.exe is located at \build\runtime\LocalRunHelper.exe in Nuget package.</span></span>

    ![Azure Data Lake U-SQL SDK 加入參考](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-add-reference.png)

- <span data-ttu-id="99598-317">U-SQL SDK**只**支援 x64 環境，請確定 tooset 組建平台目標為 x64。</span><span class="sxs-lookup"><span data-stu-id="99598-317">U-SQL SDK **only** support x64 environment, make sure tooset build platform target as x64.</span></span> <span data-ttu-id="99598-318">您可以透過 [專案屬性] > [建置] > [平台目標] 來設定。</span><span class="sxs-lookup"><span data-stu-id="99598-318">You can set that through Project Property > Build > Platform target.</span></span>

    ![Azure Data Lake U-SQL SDK 設定 x64 專案](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-configure-x64.png)

- <span data-ttu-id="99598-320">請確定 tooset 您的測試環境為 x64。</span><span class="sxs-lookup"><span data-stu-id="99598-320">Make sure tooset your test environment as x64.</span></span> <span data-ttu-id="99598-321">在 Visual Studio 中，您可以透過 [測試] > [測試設定] > [預設處理器架構] > [x64] 來設定。</span><span class="sxs-lookup"><span data-stu-id="99598-321">In Visual Studio, you can set it through Test > Test Settings > Default Processor Architecture > x64.</span></span>

    ![Azure Data Lake U-SQL SDK 設定 x64 測試環境](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-configure-test-x64.png)

- <span data-ttu-id="99598-323">請確定 toocopy 通常是在 ProjectFolder\bin\x64\Debug NugetPackage\build\runtime\ tooproject 工作目錄下的所有相依性檔案。</span><span class="sxs-lookup"><span data-stu-id="99598-323">Make sure toocopy all dependency files under NugetPackage\build\runtime\ tooproject working directory which is usually under ProjectFolder\bin\x64\Debug.</span></span>

### <a name="step-2-create-u-sql-script-test-case"></a><span data-ttu-id="99598-324">步驟 2：建立 U-SQL 指令碼測試案例</span><span class="sxs-lookup"><span data-stu-id="99598-324">Step 2: Create U-SQL script test case</span></span>

<span data-ttu-id="99598-325">以下是 hello U-SQL 指令碼測試的範例程式碼。</span><span class="sxs-lookup"><span data-stu-id="99598-325">Below is hello sample code for U-SQL script test.</span></span> <span data-ttu-id="99598-326">為了測試，您需要 tooprepare 指令碼中，輸入的檔和預期的輸出檔。</span><span class="sxs-lookup"><span data-stu-id="99598-326">For testing, you need tooprepare scripts, input files and expected output files.</span></span>

    using System;
    using Microsoft.VisualStudio.TestTools.UnitTesting;
    using System.IO;
    using System.Text;
    using System.Security.Cryptography;
    using Microsoft.Analytics.LocalRun;

    namespace UnitTestProject1
    {
        [TestClass]
        public class USQLUnitTest
        {
            [TestMethod]
            public void TestUSQLScript()
            {
                //Specify hello local run message output path
                StreamWriter MessageOutput = new StreamWriter("../../../log.txt");

                LocalRunHelper localrun = new LocalRunHelper(MessageOutput);

                //Configure hello DateRoot path, Script Path and CPPSDK path
                localrun.DataRoot = "../../../";
                localrun.ScriptPath = "../../../Script/Script.usql";
                localrun.CppSdkDir = "../../../CppSDK";

                //Run U-SQL script
                localrun.DoRun();

                //Script output 
                string Result = Path.Combine(localrun.DataRoot, "Output/result.csv");

                //Expected script output
                string ExpectedResult = "../../../ExpectedOutput/result.csv";

                Test.Helpers.FileAssert.AreEqual(Result, ExpectedResult);

                //Don't forget tooclose MessageOutput tooget logs into file
                MessageOutput.Close();
            }
        }
    }

    namespace Test.Helpers
    {
        public static class FileAssert
        {
            static string GetFileHash(string filename)
            {
                Assert.IsTrue(File.Exists(filename));

                using (var hash = new SHA1Managed())
                {
                    var clearBytes = File.ReadAllBytes(filename);
                    var hashedBytes = hash.ComputeHash(clearBytes);
                    return ConvertBytesToHex(hashedBytes);
                }
            }

            static string ConvertBytesToHex(byte[] bytes)
            {
                var sb = new StringBuilder();

                for (var i = 0; i < bytes.Length; i++)
                {
                    sb.Append(bytes[i].ToString("x"));
                }
                return sb.ToString();
            }

            public static void AreEqual(string filename1, string filename2)
            {
                string hash1 = GetFileHash(filename1);
                string hash2 = GetFileHash(filename2);

                Assert.AreEqual(hash1, hash2);
            }
        }
    }


### <a name="programming-interfaces-in-localrunhelperexe"></a><span data-ttu-id="99598-327">LocalRunHelper.exe 中的程式設計介面</span><span class="sxs-lookup"><span data-stu-id="99598-327">Programming interfaces in LocalRunHelper.exe</span></span>

<span data-ttu-id="99598-328">LocalRunHelper.exe 提供 hello 程式設計介面的 U-SQL 本機編譯、 執行、 列出等 hello 介面，如下所示。</span><span class="sxs-lookup"><span data-stu-id="99598-328">LocalRunHelper.exe provides hello programming interfaces for U-SQL local compile, run, etc. hello interfaces are listed as follows.</span></span>

<span data-ttu-id="99598-329">**建構函式**</span><span class="sxs-lookup"><span data-stu-id="99598-329">**Constructor**</span></span>

<span data-ttu-id="99598-330">public LocalRunHelper([System.IO.TextWriter messageOutput = null])</span><span class="sxs-lookup"><span data-stu-id="99598-330">public LocalRunHelper([System.IO.TextWriter messageOutput = null])</span></span>

|<span data-ttu-id="99598-331">參數</span><span class="sxs-lookup"><span data-stu-id="99598-331">Parameter</span></span>|<span data-ttu-id="99598-332">類型</span><span class="sxs-lookup"><span data-stu-id="99598-332">Type</span></span>|<span data-ttu-id="99598-333">說明</span><span class="sxs-lookup"><span data-stu-id="99598-333">Description</span></span>|
|---------|----|-----------|
|<span data-ttu-id="99598-334">messageOutput</span><span class="sxs-lookup"><span data-stu-id="99598-334">messageOutput</span></span>|<span data-ttu-id="99598-335">System.IO.TextWriter</span><span class="sxs-lookup"><span data-stu-id="99598-335">System.IO.TextWriter</span></span>|<span data-ttu-id="99598-336">對於輸出訊息，設定 toonull toouse 主控台</span><span class="sxs-lookup"><span data-stu-id="99598-336">for output messages, set toonull toouse Console</span></span>|

<span data-ttu-id="99598-337">**屬性**</span><span class="sxs-lookup"><span data-stu-id="99598-337">**Properties**</span></span>

|<span data-ttu-id="99598-338">屬性</span><span class="sxs-lookup"><span data-stu-id="99598-338">Property</span></span>|<span data-ttu-id="99598-339">類型</span><span class="sxs-lookup"><span data-stu-id="99598-339">Type</span></span>|<span data-ttu-id="99598-340">說明</span><span class="sxs-lookup"><span data-stu-id="99598-340">Description</span></span>|
|--------|----|-----------|
|<span data-ttu-id="99598-341">AlgebraPath</span><span class="sxs-lookup"><span data-stu-id="99598-341">AlgebraPath</span></span>|<span data-ttu-id="99598-342">字串</span><span class="sxs-lookup"><span data-stu-id="99598-342">string</span></span>|<span data-ttu-id="99598-343">hello 路徑 tooalgebra 檔案 （代數檔案是其中一個 hello 編譯結果）</span><span class="sxs-lookup"><span data-stu-id="99598-343">hello path tooalgebra file (algebra file is one of hello compilation results)</span></span>|
|<span data-ttu-id="99598-344">CodeBehindReferences</span><span class="sxs-lookup"><span data-stu-id="99598-344">CodeBehindReferences</span></span>|<span data-ttu-id="99598-345">字串</span><span class="sxs-lookup"><span data-stu-id="99598-345">string</span></span>|<span data-ttu-id="99598-346">如果 hello 指令碼額外的程式碼參考之後，請指定 hello 路徑，並以 ';'</span><span class="sxs-lookup"><span data-stu-id="99598-346">If hello script has additional code behind references, specify hello paths separated with ';'</span></span>|
|<span data-ttu-id="99598-347">CppSdkDir</span><span class="sxs-lookup"><span data-stu-id="99598-347">CppSdkDir</span></span>|<span data-ttu-id="99598-348">字串</span><span class="sxs-lookup"><span data-stu-id="99598-348">string</span></span>|<span data-ttu-id="99598-349">CppSDK 目錄</span><span class="sxs-lookup"><span data-stu-id="99598-349">CppSDK directory</span></span>|
|<span data-ttu-id="99598-350">CurrentDir</span><span class="sxs-lookup"><span data-stu-id="99598-350">CurrentDir</span></span>|<span data-ttu-id="99598-351">字串</span><span class="sxs-lookup"><span data-stu-id="99598-351">string</span></span>|<span data-ttu-id="99598-352">目前的目錄</span><span class="sxs-lookup"><span data-stu-id="99598-352">Current directory</span></span>|
|<span data-ttu-id="99598-353">DataRoot</span><span class="sxs-lookup"><span data-stu-id="99598-353">DataRoot</span></span>|<span data-ttu-id="99598-354">string</span><span class="sxs-lookup"><span data-stu-id="99598-354">string</span></span>|<span data-ttu-id="99598-355">資料根路徑</span><span class="sxs-lookup"><span data-stu-id="99598-355">Data root path</span></span>|
|<span data-ttu-id="99598-356">DebuggerMailPath</span><span class="sxs-lookup"><span data-stu-id="99598-356">DebuggerMailPath</span></span>|<span data-ttu-id="99598-357">字串</span><span class="sxs-lookup"><span data-stu-id="99598-357">string</span></span>|<span data-ttu-id="99598-358">hello 路徑 toodebugger 槽</span><span class="sxs-lookup"><span data-stu-id="99598-358">hello path toodebugger mailslot</span></span>|
|<span data-ttu-id="99598-359">GenerateUdoRedirect</span><span class="sxs-lookup"><span data-stu-id="99598-359">GenerateUdoRedirect</span></span>|<span data-ttu-id="99598-360">布林</span><span class="sxs-lookup"><span data-stu-id="99598-360">bool</span></span>|<span data-ttu-id="99598-361">如果我們想要載入的 toogenerate 組件重新導向會覆寫設定</span><span class="sxs-lookup"><span data-stu-id="99598-361">If we want toogenerate assembly loading redirection override config</span></span>|
|<span data-ttu-id="99598-362">HasCodeBehind</span><span class="sxs-lookup"><span data-stu-id="99598-362">HasCodeBehind</span></span>|<span data-ttu-id="99598-363">布林</span><span class="sxs-lookup"><span data-stu-id="99598-363">bool</span></span>|<span data-ttu-id="99598-364">如果 hello 指令碼後置程式碼</span><span class="sxs-lookup"><span data-stu-id="99598-364">If hello script has code behind</span></span>|
|<span data-ttu-id="99598-365">InputDir</span><span class="sxs-lookup"><span data-stu-id="99598-365">InputDir</span></span>|<span data-ttu-id="99598-366">string</span><span class="sxs-lookup"><span data-stu-id="99598-366">string</span></span>|<span data-ttu-id="99598-367">輸入資料的目錄</span><span class="sxs-lookup"><span data-stu-id="99598-367">Directory for input data</span></span>|
|<span data-ttu-id="99598-368">MessagePath</span><span class="sxs-lookup"><span data-stu-id="99598-368">MessagePath</span></span>|<span data-ttu-id="99598-369">字串</span><span class="sxs-lookup"><span data-stu-id="99598-369">string</span></span>|<span data-ttu-id="99598-370">訊息傾印檔案路徑</span><span class="sxs-lookup"><span data-stu-id="99598-370">Message dump file path</span></span>|
|<span data-ttu-id="99598-371">OutputDir</span><span class="sxs-lookup"><span data-stu-id="99598-371">OutputDir</span></span>|<span data-ttu-id="99598-372">string</span><span class="sxs-lookup"><span data-stu-id="99598-372">string</span></span>|<span data-ttu-id="99598-373">輸出資料的目錄</span><span class="sxs-lookup"><span data-stu-id="99598-373">Directory for output data</span></span>|
|<span data-ttu-id="99598-374">平行處理原則</span><span class="sxs-lookup"><span data-stu-id="99598-374">Parallelism</span></span>|<span data-ttu-id="99598-375">int</span><span class="sxs-lookup"><span data-stu-id="99598-375">int</span></span>|<span data-ttu-id="99598-376">平行處理原則 toorun hello 代數</span><span class="sxs-lookup"><span data-stu-id="99598-376">Parallelism toorun hello algebra</span></span>|
|<span data-ttu-id="99598-377">ParentPid</span><span class="sxs-lookup"><span data-stu-id="99598-377">ParentPid</span></span>|<span data-ttu-id="99598-378">int</span><span class="sxs-lookup"><span data-stu-id="99598-378">int</span></span>|<span data-ttu-id="99598-379">哪些 hello 服務會監視 tooexit、 組 too0 或負 tooignore hello 父系的 PID</span><span class="sxs-lookup"><span data-stu-id="99598-379">PID of hello parent on which hello service monitors tooexit, set too0 or negative tooignore</span></span>|
|<span data-ttu-id="99598-380">ResultPath</span><span class="sxs-lookup"><span data-stu-id="99598-380">ResultPath</span></span>|<span data-ttu-id="99598-381">字串</span><span class="sxs-lookup"><span data-stu-id="99598-381">string</span></span>|<span data-ttu-id="99598-382">結果傾印檔案路徑</span><span class="sxs-lookup"><span data-stu-id="99598-382">Result dump file path</span></span>|
|<span data-ttu-id="99598-383">RuntimeDir</span><span class="sxs-lookup"><span data-stu-id="99598-383">RuntimeDir</span></span>|<span data-ttu-id="99598-384">字串</span><span class="sxs-lookup"><span data-stu-id="99598-384">string</span></span>|<span data-ttu-id="99598-385">執行階段目錄</span><span class="sxs-lookup"><span data-stu-id="99598-385">Runtime directory</span></span>|
|<span data-ttu-id="99598-386">ScriptPath</span><span class="sxs-lookup"><span data-stu-id="99598-386">ScriptPath</span></span>|<span data-ttu-id="99598-387">字串</span><span class="sxs-lookup"><span data-stu-id="99598-387">string</span></span>|<span data-ttu-id="99598-388">其中 toofind hello 指令碼</span><span class="sxs-lookup"><span data-stu-id="99598-388">Where toofind hello script</span></span>|
|<span data-ttu-id="99598-389">Shallow</span><span class="sxs-lookup"><span data-stu-id="99598-389">Shallow</span></span>|<span data-ttu-id="99598-390">布林</span><span class="sxs-lookup"><span data-stu-id="99598-390">bool</span></span>|<span data-ttu-id="99598-391">是否進行淺層編譯</span><span class="sxs-lookup"><span data-stu-id="99598-391">Shallow compile or not</span></span>|
|<span data-ttu-id="99598-392">TempDir</span><span class="sxs-lookup"><span data-stu-id="99598-392">TempDir</span></span>|<span data-ttu-id="99598-393">字串</span><span class="sxs-lookup"><span data-stu-id="99598-393">string</span></span>|<span data-ttu-id="99598-394">Temp 目錄</span><span class="sxs-lookup"><span data-stu-id="99598-394">Temp directory</span></span>|
|<span data-ttu-id="99598-395">UseDataBase</span><span class="sxs-lookup"><span data-stu-id="99598-395">UseDataBase</span></span>|<span data-ttu-id="99598-396">字串</span><span class="sxs-lookup"><span data-stu-id="99598-396">string</span></span>|<span data-ttu-id="99598-397">指定程式碼後置暫存組件註冊時，根據預設，主要的 hello 資料庫 toouse</span><span class="sxs-lookup"><span data-stu-id="99598-397">Specify hello database toouse for code behind temporary assembly registration, master by default</span></span>|
|<span data-ttu-id="99598-398">WorkDir</span><span class="sxs-lookup"><span data-stu-id="99598-398">WorkDir</span></span>|<span data-ttu-id="99598-399">字串</span><span class="sxs-lookup"><span data-stu-id="99598-399">string</span></span>|<span data-ttu-id="99598-400">慣用的工作目錄</span><span class="sxs-lookup"><span data-stu-id="99598-400">Preferred working directory</span></span>|


<span data-ttu-id="99598-401">**方法**</span><span class="sxs-lookup"><span data-stu-id="99598-401">**Method**</span></span>

|<span data-ttu-id="99598-402">方法</span><span class="sxs-lookup"><span data-stu-id="99598-402">Method</span></span>|<span data-ttu-id="99598-403">說明</span><span class="sxs-lookup"><span data-stu-id="99598-403">Description</span></span>|<span data-ttu-id="99598-404">傳回</span><span class="sxs-lookup"><span data-stu-id="99598-404">Return</span></span>|<span data-ttu-id="99598-405">參數</span><span class="sxs-lookup"><span data-stu-id="99598-405">Parameter</span></span>|
|------|-----------|------|---------|
|<span data-ttu-id="99598-406">public bool DoCompile()</span><span class="sxs-lookup"><span data-stu-id="99598-406">public bool DoCompile()</span></span>|<span data-ttu-id="99598-407">編譯 hello U-SQL 指令碼</span><span class="sxs-lookup"><span data-stu-id="99598-407">Compile hello U-SQL script</span></span>|<span data-ttu-id="99598-408">成功時為 True</span><span class="sxs-lookup"><span data-stu-id="99598-408">True on success</span></span>| |
|<span data-ttu-id="99598-409">public bool DoExec()</span><span class="sxs-lookup"><span data-stu-id="99598-409">public bool DoExec()</span></span>|<span data-ttu-id="99598-410">執行 hello 編譯結果</span><span class="sxs-lookup"><span data-stu-id="99598-410">Execute hello compiled result</span></span>|<span data-ttu-id="99598-411">成功時為 True</span><span class="sxs-lookup"><span data-stu-id="99598-411">True on success</span></span>| |
|<span data-ttu-id="99598-412">public bool DoRun()</span><span class="sxs-lookup"><span data-stu-id="99598-412">public bool DoRun()</span></span>|<span data-ttu-id="99598-413">執行 hello U-SQL 指令碼 （編譯 + 執行）</span><span class="sxs-lookup"><span data-stu-id="99598-413">Run hello U-SQL script (Compile + Execute)</span></span>|<span data-ttu-id="99598-414">成功時為 True</span><span class="sxs-lookup"><span data-stu-id="99598-414">True on success</span></span>| |
|<span data-ttu-id="99598-415">public bool IsValidRuntimeDir(string path)</span><span class="sxs-lookup"><span data-stu-id="99598-415">public bool IsValidRuntimeDir(string path)</span></span>|<span data-ttu-id="99598-416">檢查指定路徑的 hello 是否為有效的執行階段的路徑</span><span class="sxs-lookup"><span data-stu-id="99598-416">Check if hello given path is valid runtime path</span></span>|<span data-ttu-id="99598-417">有效則為 True</span><span class="sxs-lookup"><span data-stu-id="99598-417">True for valid</span></span>|<span data-ttu-id="99598-418">hello 目錄路徑的執行階段</span><span class="sxs-lookup"><span data-stu-id="99598-418">hello path of runtime directory</span></span>|


## <a name="faq-about-common-issue"></a><span data-ttu-id="99598-419">有關常見問題的常見問題集</span><span class="sxs-lookup"><span data-stu-id="99598-419">FAQ about common issue</span></span>

### <a name="error-1"></a><span data-ttu-id="99598-420">錯誤 1：</span><span class="sxs-lookup"><span data-stu-id="99598-420">Error 1:</span></span>
<span data-ttu-id="99598-421">E_CSC_SYSTEM_INTERNAL: 內部錯誤!</span><span class="sxs-lookup"><span data-stu-id="99598-421">E_CSC_SYSTEM_INTERNAL: Internal error!</span></span> <span data-ttu-id="99598-422">無法載入檔案或組件 'ScopeEngineManaged.dll' 或其相依性的其中之一。</span><span class="sxs-lookup"><span data-stu-id="99598-422">Could not load file or assembly 'ScopeEngineManaged.dll' or one of its dependencies.</span></span> <span data-ttu-id="99598-423">找不到 hello 指定的模組。</span><span class="sxs-lookup"><span data-stu-id="99598-423">hello specified module could not be found.</span></span>

<span data-ttu-id="99598-424">請檢查下列 hello:</span><span class="sxs-lookup"><span data-stu-id="99598-424">Please check hello following:</span></span>

- <span data-ttu-id="99598-425">確定您使用 x64 環境。</span><span class="sxs-lookup"><span data-stu-id="99598-425">Make sure you have x64 environment.</span></span> <span data-ttu-id="99598-426">hello 建置目標平台與 hello 測試環境應該是 x64，請參閱太**步驟 1： 建立 C# 單元測試專案和組態**上方。</span><span class="sxs-lookup"><span data-stu-id="99598-426">hello build target platform and hello test environment should be x64, refer too**Step 1: Create C# unit test project and configuration** above.</span></span>
- <span data-ttu-id="99598-427">請確定您已複製 NugetPackage\build\runtime\ tooproject 工作目錄下的所有相依性檔案。</span><span class="sxs-lookup"><span data-stu-id="99598-427">Make sure you have copied all dependency files under NugetPackage\build\runtime\ tooproject working directory.</span></span>


## <a name="next-steps"></a><span data-ttu-id="99598-428">後續步驟</span><span class="sxs-lookup"><span data-stu-id="99598-428">Next steps</span></span>

* <span data-ttu-id="99598-429">toolearn U-SQL，請參閱[開始使用 Azure 資料湖分析 U-SQL 語言](data-lake-analytics-u-sql-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="99598-429">toolearn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="99598-430">toolog 診斷資訊，請參閱[存取診斷記錄檔的 Azure Data Lake Analytics](data-lake-analytics-diagnostic-logs.md)。</span><span class="sxs-lookup"><span data-stu-id="99598-430">toolog diagnostics information, see [Accessing diagnostics logs for Azure Data Lake Analytics](data-lake-analytics-diagnostic-logs.md).</span></span>
* <span data-ttu-id="99598-431">toosee 更複雜的查詢，請參閱[分析網站記錄檔，使用 Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md)。</span><span class="sxs-lookup"><span data-stu-id="99598-431">toosee a more complex query, see [Analyze website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="99598-432">tooview 作業的詳細資訊，請參閱[使用作業瀏覽器和 Azure Data Lake Analytics 工作的工作檢視](data-lake-analytics-data-lake-tools-view-jobs.md)。</span><span class="sxs-lookup"><span data-stu-id="99598-432">tooview job details, see [Use Job Browser and Job View for Azure Data Lake Analytics jobs](data-lake-analytics-data-lake-tools-view-jobs.md).</span></span>
* <span data-ttu-id="99598-433">toouse hello 頂點執行檢視，請參閱[使用 hello 頂點資料湖 Tools for Visual Studio 中的執行檢視](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md)。</span><span class="sxs-lookup"><span data-stu-id="99598-433">toouse hello vertex execution view, see [Use hello Vertex Execution View in Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).</span></span>
