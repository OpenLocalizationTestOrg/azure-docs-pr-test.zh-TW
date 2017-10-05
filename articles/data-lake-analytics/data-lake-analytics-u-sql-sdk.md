---
title: "使用 Azure Data Lake U-SQL SDK 調整 U-SQL 本機執行和測試 | Microsoft Docs"
description: "了解如何使用 Azure Data Lake U-SQL SDK 在本機工作站上使用命令列及程式設計介面來調整 U-SQL 作業本機執行和測試。"
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
ms.openlocfilehash: 55242bcf644ca0e7f30cfe7eada2130451c36e64
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="scale-u-sql-local-run-and-test-with-azure-data-lake-u-sql-sdk"></a><span data-ttu-id="f1e53-103">使用 Azure Data Lake U-SQL SDK 調整 U-SQL 本機執行和測試</span><span class="sxs-lookup"><span data-stu-id="f1e53-103">Scale U-SQL local run and test with Azure Data Lake U-SQL SDK</span></span>

<span data-ttu-id="f1e53-104">在開發 U-SQL 指令碼時，通常會在本機執行並測試 U-SQL 指令碼，然後才送出至雲端。</span><span class="sxs-lookup"><span data-stu-id="f1e53-104">When developing U-SQL script, it is common to run and test U-SQL script locally before submit it to cloud.</span></span> <span data-ttu-id="f1e53-105">Azure Data Lake 針對此案例提供稱為 Azure Data Lake U-SQL SDK 的 Nuget 套件，讓您可以輕鬆地調整 U-SQL 本機執行和測試。</span><span class="sxs-lookup"><span data-stu-id="f1e53-105">Azure Data Lake provides a Nuget package called Azure Data Lake U-SQL SDK for this scenario, through which you can easily scale U-SQL local run and test.</span></span> <span data-ttu-id="f1e53-106">此外，也可以將此 U-SQL 測試與 CI (持續整合) 系統整合以自動化編譯和測試。</span><span class="sxs-lookup"><span data-stu-id="f1e53-106">It is also possible to integrate this U-SQL test with CI (Continuous Integration) system to automate the compile and test.</span></span>

<span data-ttu-id="f1e53-107">如果您在意要如何使用 GUI 工具來手動本機執行並針對 U-SQL 指令碼進行偵錯，您可以使用 Azure Data Lake Tools for Visual Studio 來執行。</span><span class="sxs-lookup"><span data-stu-id="f1e53-107">If you care about how to manually local run and debug U-SQL script with GUI tooling, then you can use Azure Data Lake Tools for Visual Studio for that.</span></span> <span data-ttu-id="f1e53-108">您可以在[這裡](data-lake-analytics-data-lake-tools-local-run.md)深入了解。</span><span class="sxs-lookup"><span data-stu-id="f1e53-108">You can learn more from [here](data-lake-analytics-data-lake-tools-local-run.md).</span></span>

## <a name="install-azure-data-lake-u-sql-sdk"></a><span data-ttu-id="f1e53-109">安裝 Azure Data Lake U-SQL SDK</span><span class="sxs-lookup"><span data-stu-id="f1e53-109">Install Azure Data Lake U-SQL SDK</span></span>

<span data-ttu-id="f1e53-110">您可以在 Nuget.org 上的[這裡](https://www.nuget.org/packages/Microsoft.Azure.DataLake.USQL.SDK/)取得 Azure Data Lake U-SQL SDK。</span><span class="sxs-lookup"><span data-stu-id="f1e53-110">You can get the Azure Data Lake U-SQL SDK [here](https://www.nuget.org/packages/Microsoft.Azure.DataLake.USQL.SDK/) on Nuget.org.</span></span> <span data-ttu-id="f1e53-111">在使用它之前，您必須確定您具有下列相依性。</span><span class="sxs-lookup"><span data-stu-id="f1e53-111">And before using it, you need to make sure you have dependencies as follows.</span></span>

### <a name="dependencies"></a><span data-ttu-id="f1e53-112">相依項目</span><span class="sxs-lookup"><span data-stu-id="f1e53-112">Dependencies</span></span>

<span data-ttu-id="f1e53-113">Data Lake U-SQL SDK 需要下列相依性︰</span><span class="sxs-lookup"><span data-stu-id="f1e53-113">The Data Lake U-SQL SDK requires the following dependencies:</span></span>

- <span data-ttu-id="f1e53-114">[Microsoft .NET Framework 4.6 或更新版本](https://www.microsoft.com/download/details.aspx?id=17851)。</span><span class="sxs-lookup"><span data-stu-id="f1e53-114">[Microsoft .NET Framework 4.6 or newer](https://www.microsoft.com/download/details.aspx?id=17851).</span></span>
- <span data-ttu-id="f1e53-115">Microsoft Visual C++ 14 和 Windows SDK 10.0.10240.0 或更新版本 (在本文中稱為 CppSDK)。</span><span class="sxs-lookup"><span data-stu-id="f1e53-115">Microsoft Visual C++ 14 and Windows SDK 10.0.10240.0 or newer (which is called CppSDK in this article).</span></span> <span data-ttu-id="f1e53-116">有兩種方式可取得 CppSDK：</span><span class="sxs-lookup"><span data-stu-id="f1e53-116">There are two ways to get CppSDK:</span></span>

    - <span data-ttu-id="f1e53-117">安裝 [Visual Studio Community 版本](https://developer.microsoft.com/downloads/vs-thankyou)。</span><span class="sxs-lookup"><span data-stu-id="f1e53-117">Install [Visual Studio Community Edition](https://developer.microsoft.com/downloads/vs-thankyou).</span></span> <span data-ttu-id="f1e53-118">在 Program Files 資料夾下應該會有 \Windows Kits\10 資料夾，例如 C:\Program Files (x86)\Windows Kits\10。</span><span class="sxs-lookup"><span data-stu-id="f1e53-118">You'll have a \Windows Kits\10 folder under the Program Files folder--for example, C:\Program Files (x86)\Windows Kits\10\.</span></span> <span data-ttu-id="f1e53-119">您也會在 \Windows Kits\10\Lib 下找到 Windows 10 SDK 版本。</span><span class="sxs-lookup"><span data-stu-id="f1e53-119">You'll also find the Windows 10 SDK version under \Windows Kits\10\Lib.</span></span> <span data-ttu-id="f1e53-120">如果您看不見這些資料夾，請重新安裝 Visual Studio，並務必在安裝期間選取 Windows 10 SDK。</span><span class="sxs-lookup"><span data-stu-id="f1e53-120">If you don’t see these folders, reinstall Visual Studio and be sure to select the Windows 10 SDK during the installation.</span></span> <span data-ttu-id="f1e53-121">如果您已經隨 Visual Studio 一起安裝此項目，U-SQL 本機編譯器會自動尋找它。</span><span class="sxs-lookup"><span data-stu-id="f1e53-121">If you have this installed with Visual Studio, the U-SQL local compiler will find it automatically.</span></span>

    ![Data Lake Tools for Visual Studio 本機執行的 Windows 10 SDK](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-windows-10-sdk.png)

    - <span data-ttu-id="f1e53-123">安裝 [Data Lake Tools for Visual Studio](http://aka.ms/adltoolsvs)。</span><span class="sxs-lookup"><span data-stu-id="f1e53-123">Install [Data Lake Tools for Visual Studio](http://aka.ms/adltoolsvs).</span></span> <span data-ttu-id="f1e53-124">您可以在 C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\ADL Tools\X.X.XXXX.X\CppSDK 找到預先封裝的 Visual C++ 和 Windows SDK 檔案。</span><span class="sxs-lookup"><span data-stu-id="f1e53-124">You can find the prepackaged Visual C++ and Windows SDK files at C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\ADL Tools\X.X.XXXX.X\CppSDK.</span></span> <span data-ttu-id="f1e53-125">在此情況下，U-SQL 本機編譯器就無法自動找到相依性。</span><span class="sxs-lookup"><span data-stu-id="f1e53-125">In this case, the U-SQL local compiler cannot find the dependencies automatically.</span></span> <span data-ttu-id="f1e53-126">您必須為它指定 CppSDK 路徑。</span><span class="sxs-lookup"><span data-stu-id="f1e53-126">You need to specify the CppSDK path for it.</span></span> <span data-ttu-id="f1e53-127">您可以將檔案複製到另一個位置，或直接使用它。</span><span class="sxs-lookup"><span data-stu-id="f1e53-127">You can either copy the files to another location or use it as is.</span></span>

## <a name="understand-basic-concepts"></a><span data-ttu-id="f1e53-128">了解基本概念</span><span class="sxs-lookup"><span data-stu-id="f1e53-128">Understand basic concepts</span></span>

### <a name="data-root"></a><span data-ttu-id="f1e53-129">資料根</span><span class="sxs-lookup"><span data-stu-id="f1e53-129">Data root</span></span>

<span data-ttu-id="f1e53-130">資料根資料夾是本機計算帳戶的「本機存放區」。</span><span class="sxs-lookup"><span data-stu-id="f1e53-130">The data-root folder is a "local store" for the local compute account.</span></span> <span data-ttu-id="f1e53-131">它就相當於 Data Lake Analytics 帳戶的 Azure Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="f1e53-131">It's equivalent to the Azure Data Lake Store account of a Data Lake Analytics account.</span></span> <span data-ttu-id="f1e53-132">切換到不同的資料根資料夾，就如同切換到不同的存放區帳戶。</span><span class="sxs-lookup"><span data-stu-id="f1e53-132">Switching to a different data-root folder is just like switching to a different store account.</span></span> <span data-ttu-id="f1e53-133">如果您想要存取具有不同資料根資料夾的常用共用資料，便必須在指令碼中使用絕對路徑。</span><span class="sxs-lookup"><span data-stu-id="f1e53-133">If you want to access commonly shared data with different data-root folders, you must use absolute paths in your scripts.</span></span> <span data-ttu-id="f1e53-134">或者，您可以在資料根資料夾下建立檔案系統符號連結 (例如 NTFS 上的 **mklink**)，來指向共用資料。</span><span class="sxs-lookup"><span data-stu-id="f1e53-134">Or, create file system symbolic links (for example, **mklink** on NTFS) under the data-root folder to point to the shared data.</span></span>

<span data-ttu-id="f1e53-135">資料根資料夾是用來︰</span><span class="sxs-lookup"><span data-stu-id="f1e53-135">The data-root folder is used to:</span></span>

- <span data-ttu-id="f1e53-136">儲存本機中繼資料，包括資料庫、資料表、資料表值函式 (TVF)，以及組件。</span><span class="sxs-lookup"><span data-stu-id="f1e53-136">Store local metadata, including databases, tables, table-valued functions (TVFs), and assemblies.</span></span>
- <span data-ttu-id="f1e53-137">查詢在 U-SQL 中定義為相對路徑的輸入和輸出路徑。</span><span class="sxs-lookup"><span data-stu-id="f1e53-137">Look up the input and output paths that are defined as relative paths in U-SQL.</span></span> <span data-ttu-id="f1e53-138">使用相對路徑能夠更容易將 U-SQL 專案部署至 Azure。</span><span class="sxs-lookup"><span data-stu-id="f1e53-138">Using relative paths makes it easier to deploy your U-SQL projects to Azure.</span></span>

### <a name="file-path-in-u-sql"></a><span data-ttu-id="f1e53-139">U-SQL 中的檔案路徑</span><span class="sxs-lookup"><span data-stu-id="f1e53-139">File path in U-SQL</span></span>

<span data-ttu-id="f1e53-140">您可以在 U-SQL 指令碼中使用相對路徑和本機絕對路徑。</span><span class="sxs-lookup"><span data-stu-id="f1e53-140">You can use both a relative path and a local absolute path in U-SQL scripts.</span></span> <span data-ttu-id="f1e53-141">相對路徑是相對於指定的資料根資料夾路徑。</span><span class="sxs-lookup"><span data-stu-id="f1e53-141">The relative path is relative to the specified data-root folder path.</span></span> <span data-ttu-id="f1e53-142">我們建議您使用 "/" 做為路徑分隔符號，讓您的指令碼與伺服器端相容。</span><span class="sxs-lookup"><span data-stu-id="f1e53-142">We recommend that you use "/" as the path separator to make your scripts compatible with the server side.</span></span> <span data-ttu-id="f1e53-143">以下是一些相對路徑及其對等絕對路徑的範例。</span><span class="sxs-lookup"><span data-stu-id="f1e53-143">Here are some examples of relative paths and their equivalent absolute paths.</span></span> <span data-ttu-id="f1e53-144">在這些範例中，C:\LocalRunDataRoot 是資料根資料夾。</span><span class="sxs-lookup"><span data-stu-id="f1e53-144">In these examples, C:\LocalRunDataRoot is the data-root folder.</span></span>

|<span data-ttu-id="f1e53-145">相對路徑</span><span class="sxs-lookup"><span data-stu-id="f1e53-145">Relative path</span></span>|<span data-ttu-id="f1e53-146">絕對路徑</span><span class="sxs-lookup"><span data-stu-id="f1e53-146">Absolute path</span></span>|
|-------------|-------------|
|<span data-ttu-id="f1e53-147">/abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="f1e53-147">/abc/def/input.csv</span></span> |<span data-ttu-id="f1e53-148">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="f1e53-148">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="f1e53-149">abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="f1e53-149">abc/def/input.csv</span></span>  |<span data-ttu-id="f1e53-150">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="f1e53-150">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="f1e53-151">D:/abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="f1e53-151">D:/abc/def/input.csv</span></span> |<span data-ttu-id="f1e53-152">D:\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="f1e53-152">D:\abc\def\input.csv</span></span>|

### <a name="working-directory"></a><span data-ttu-id="f1e53-153">工作目錄</span><span class="sxs-lookup"><span data-stu-id="f1e53-153">Working directory</span></span>

<span data-ttu-id="f1e53-154">當在本機執行 U-SQL 指令碼時，系統會在編譯期間於目前執行的目錄下建立一個工作目錄。</span><span class="sxs-lookup"><span data-stu-id="f1e53-154">When running the U-SQL script locally, a working directory is created during compilation under current running directory.</span></span> <span data-ttu-id="f1e53-155">除了編譯輸出，本機執行所需的執行階段檔案會陰影複製到這個工作目錄。</span><span class="sxs-lookup"><span data-stu-id="f1e53-155">In addition to the compilation outputs, the needed runtime files for local execution will be shadow copied to this working directory.</span></span> <span data-ttu-id="f1e53-156">工作目錄根資料夾稱為 "ScopeWorkDir"，而在工作目錄下的檔案如下：</span><span class="sxs-lookup"><span data-stu-id="f1e53-156">The working directory root folder is called "ScopeWorkDir" and the files under the working directory are as follows:</span></span>

|<span data-ttu-id="f1e53-157">目錄/檔案</span><span class="sxs-lookup"><span data-stu-id="f1e53-157">Directory/file</span></span>|<span data-ttu-id="f1e53-158">目錄/檔案</span><span class="sxs-lookup"><span data-stu-id="f1e53-158">Directory/file</span></span>|<span data-ttu-id="f1e53-159">目錄/檔案</span><span class="sxs-lookup"><span data-stu-id="f1e53-159">Directory/file</span></span>|<span data-ttu-id="f1e53-160">定義</span><span class="sxs-lookup"><span data-stu-id="f1e53-160">Definition</span></span>|<span data-ttu-id="f1e53-161">說明</span><span class="sxs-lookup"><span data-stu-id="f1e53-161">Description</span></span>|
|--------------|--------------|--------------|----------|-----------|
|<span data-ttu-id="f1e53-162">C6A101DDCB470506</span><span class="sxs-lookup"><span data-stu-id="f1e53-162">C6A101DDCB470506</span></span>| | |<span data-ttu-id="f1e53-163">執行階段版本的雜湊字串</span><span class="sxs-lookup"><span data-stu-id="f1e53-163">Hash string of runtime version</span></span>|<span data-ttu-id="f1e53-164">陰影複製本機執行所需的執行階段檔案</span><span class="sxs-lookup"><span data-stu-id="f1e53-164">Shadow copy of runtime files needed for local execution</span></span>|
| |<span data-ttu-id="f1e53-165">Script_66AE4909AA0ED06C</span><span class="sxs-lookup"><span data-stu-id="f1e53-165">Script_66AE4909AA0ED06C</span></span>| |<span data-ttu-id="f1e53-166">指令碼名稱 + 指令碼路徑的雜湊字串</span><span class="sxs-lookup"><span data-stu-id="f1e53-166">Script name + hash string of script path</span></span>|<span data-ttu-id="f1e53-167">編譯輸出和執行步驟記錄</span><span class="sxs-lookup"><span data-stu-id="f1e53-167">Compilation outputs and execution step logging</span></span>|
| | |<span data-ttu-id="f1e53-168">\_script\_.abr</span><span class="sxs-lookup"><span data-stu-id="f1e53-168">\_script\_.abr</span></span>|<span data-ttu-id="f1e53-169">編譯器輸出</span><span class="sxs-lookup"><span data-stu-id="f1e53-169">Compiler output</span></span>|<span data-ttu-id="f1e53-170">代數檔案</span><span class="sxs-lookup"><span data-stu-id="f1e53-170">Algebra file</span></span>|
| | |<span data-ttu-id="f1e53-171">\_ScopeCodeGen\_.*</span><span class="sxs-lookup"><span data-stu-id="f1e53-171">\_ScopeCodeGen\_.*</span></span>|<span data-ttu-id="f1e53-172">編譯器輸出</span><span class="sxs-lookup"><span data-stu-id="f1e53-172">Compiler output</span></span>|<span data-ttu-id="f1e53-173">產生的 Managed 程式碼</span><span class="sxs-lookup"><span data-stu-id="f1e53-173">Generated managed code</span></span>|
| | |<span data-ttu-id="f1e53-174">\_ScopeCodeGenEngine\_.*</span><span class="sxs-lookup"><span data-stu-id="f1e53-174">\_ScopeCodeGenEngine\_.*</span></span>|<span data-ttu-id="f1e53-175">編譯器輸出</span><span class="sxs-lookup"><span data-stu-id="f1e53-175">Compiler output</span></span>|<span data-ttu-id="f1e53-176">產生的原生程式碼</span><span class="sxs-lookup"><span data-stu-id="f1e53-176">Generated native code</span></span>|
| | |<span data-ttu-id="f1e53-177">參考的組件</span><span class="sxs-lookup"><span data-stu-id="f1e53-177">referenced assemblies</span></span>|<span data-ttu-id="f1e53-178">組件參考</span><span class="sxs-lookup"><span data-stu-id="f1e53-178">Assembly reference</span></span>|<span data-ttu-id="f1e53-179">參考的組件檔案</span><span class="sxs-lookup"><span data-stu-id="f1e53-179">Referenced assembly files</span></span>|
| | |<span data-ttu-id="f1e53-180">deployed_resources</span><span class="sxs-lookup"><span data-stu-id="f1e53-180">deployed_resources</span></span>|<span data-ttu-id="f1e53-181">資源部署</span><span class="sxs-lookup"><span data-stu-id="f1e53-181">Resource deployment</span></span>|<span data-ttu-id="f1e53-182">資源部署檔案</span><span class="sxs-lookup"><span data-stu-id="f1e53-182">Resource deployment files</span></span>|
| | |<span data-ttu-id="f1e53-183">xxxxxxxx.xxx[1..n]\_\*.*</span><span class="sxs-lookup"><span data-stu-id="f1e53-183">xxxxxxxx.xxx[1..n]\_\*.*</span></span>|<span data-ttu-id="f1e53-184">執行記錄檔</span><span class="sxs-lookup"><span data-stu-id="f1e53-184">Execution log</span></span>|<span data-ttu-id="f1e53-185">執行步驟的記錄檔</span><span class="sxs-lookup"><span data-stu-id="f1e53-185">Log of execution steps</span></span>|


## <a name="use-the-sdk-from-the-command-line"></a><span data-ttu-id="f1e53-186">從命令列使用 SDK</span><span class="sxs-lookup"><span data-stu-id="f1e53-186">Use the SDK from the command line</span></span>

### <a name="command-line-interface-of-the-helper-application"></a><span data-ttu-id="f1e53-187">輔助應用程式的命令列介面</span><span class="sxs-lookup"><span data-stu-id="f1e53-187">Command-line interface of the helper application</span></span>

<span data-ttu-id="f1e53-188">在 SDK directory\build\runtime 底下，LocalRunHelper.exe 是命令列輔助應用程式，能為大部分最常使用的本機執行函式提供介面。</span><span class="sxs-lookup"><span data-stu-id="f1e53-188">Under SDK directory\build\runtime, LocalRunHelper.exe is the command-line helper application that provides interfaces to most of the commonly used local-run functions.</span></span> <span data-ttu-id="f1e53-189">請注意，命令和引數參數都區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="f1e53-189">Note that both the command and the argument switches are case-sensitive.</span></span> <span data-ttu-id="f1e53-190">若要叫用此應用程式︰</span><span class="sxs-lookup"><span data-stu-id="f1e53-190">To invoke it:</span></span>

    LocalRunHelper.exe <command> <Required-Command-Arguments> [Optional-Command-Arguments]

<span data-ttu-id="f1e53-191">不使用引數執行 LocalRunHelper.exe，或使用 **help** 參數顯示說明資訊︰</span><span class="sxs-lookup"><span data-stu-id="f1e53-191">Run LocalRunHelper.exe without arguments or with the **help** switch to show the help information:</span></span>

    > LocalRunHelper.exe help

        Command 'help' :  Show usage information
        Command 'compile' :  Compile the script
        Required Arguments :
            -Script param
                    Script File Path
        Optional Arguments :
            -Shallow [default value 'False']
                    Shallow compile

<span data-ttu-id="f1e53-192">在說明資訊中︰</span><span class="sxs-lookup"><span data-stu-id="f1e53-192">In the help information:</span></span>

-  <span data-ttu-id="f1e53-193">**Command** 提供命令的名稱。</span><span class="sxs-lookup"><span data-stu-id="f1e53-193">**Command** gives the command’s name.</span></span>  
-  <span data-ttu-id="f1e53-194">**Required Argument** 列出必須提供的引數。</span><span class="sxs-lookup"><span data-stu-id="f1e53-194">**Required Argument** lists arguments that must be supplied.</span></span>  
-  <span data-ttu-id="f1e53-195">**Optional Argument** 列出選擇性的引數，並具有預設值。</span><span class="sxs-lookup"><span data-stu-id="f1e53-195">**Optional Argument** lists arguments that are optional, with default values.</span></span>  <span data-ttu-id="f1e53-196">選擇性的布林引數沒有參數，如果出現參數則表示其預設值的負值。</span><span class="sxs-lookup"><span data-stu-id="f1e53-196">Optional Boolean arguments don’t have parameters, and their appearances mean negative to their default value.</span></span>

### <a name="return-value-and-logging"></a><span data-ttu-id="f1e53-197">傳回值和記錄</span><span class="sxs-lookup"><span data-stu-id="f1e53-197">Return value and logging</span></span>

<span data-ttu-id="f1e53-198">如果成功，輔助應用程式會傳回 **0**；如果失敗，則會傳回 **-1**。</span><span class="sxs-lookup"><span data-stu-id="f1e53-198">The helper application returns **0** for success and **-1** for failure.</span></span> <span data-ttu-id="f1e53-199">根據預設，協助程式會將所有訊息傳送到目前的主控台。</span><span class="sxs-lookup"><span data-stu-id="f1e53-199">By default, the helper sends all messages to the current console.</span></span> <span data-ttu-id="f1e53-200">不過，大部分的命令都支援 **-MessageOut path_to_log_file** 選擇性引數，該引數會將輸出重新導向至記錄檔。</span><span class="sxs-lookup"><span data-stu-id="f1e53-200">However, most of the commands support the **-MessageOut path_to_log_file** optional argument that redirects the outputs to a log file.</span></span>

### <a name="environment-variable-configuring"></a><span data-ttu-id="f1e53-201">環境變數設定</span><span class="sxs-lookup"><span data-stu-id="f1e53-201">Environment variable configuring</span></span>

<span data-ttu-id="f1e53-202">U-SQL 本機執行需要指定的資料根做為本機儲存體帳戶，以及針對相依性指定的 CppSDK 路徑。</span><span class="sxs-lookup"><span data-stu-id="f1e53-202">U-SQL local run needs a specified data root as local storage account, as well as a specified CppSDK path for dependencies.</span></span> <span data-ttu-id="f1e53-203">您可以針對它們在命令列中設定引數，或是設定環境變數。</span><span class="sxs-lookup"><span data-stu-id="f1e53-203">You can both set the argument in command-line or set environment variable for them.</span></span>

- <span data-ttu-id="f1e53-204">設定 **SCOPE_CPP_SDK** 環境變數。</span><span class="sxs-lookup"><span data-stu-id="f1e53-204">Set the **SCOPE_CPP_SDK** environment variable.</span></span>

    <span data-ttu-id="f1e53-205">如果您是透過安裝 Data Lake Tools for Visual Studio 來取得 Microsoft Visual C++ 和 Windows SDK，請確認您有下列資料夾︰</span><span class="sxs-lookup"><span data-stu-id="f1e53-205">If you get Microsoft Visual C++ and the Windows SDK by installing Data Lake Tools for Visual Studio, verify that you have the following folder:</span></span>

        C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\Microsoft Azure Data Lake Tools for Visual Studio 2015\X.X.XXXX.X\CppSDK

    <span data-ttu-id="f1e53-206">定義一個名為 **SCOPE_CPP_SDK** 的新環境變數來指向此目錄。</span><span class="sxs-lookup"><span data-stu-id="f1e53-206">Define a new environment variable called **SCOPE_CPP_SDK** to point to this directory.</span></span> <span data-ttu-id="f1e53-207">或將資料夾複製到其他位置，並依同樣方式將 **SCOPE_CPP_SDK** 指定為該資料夾。</span><span class="sxs-lookup"><span data-stu-id="f1e53-207">Or copy the folder to the other location and specify **SCOPE_CPP_SDK** as that.</span></span>

    <span data-ttu-id="f1e53-208">除了設定環境變數，您可以在使用命令列時指定 **-CppSDK** 引數。</span><span class="sxs-lookup"><span data-stu-id="f1e53-208">In addition to setting the environment variable, you can specify the **-CppSDK** argument when you're using the command line.</span></span> <span data-ttu-id="f1e53-209">這個引數會覆寫預設的 CppSDK 環境變數。</span><span class="sxs-lookup"><span data-stu-id="f1e53-209">This argument overwrites your default CppSDK environment variable.</span></span>

- <span data-ttu-id="f1e53-210">設定 **LOCALRUN_DATAROOT** 環境變數。</span><span class="sxs-lookup"><span data-stu-id="f1e53-210">Set the **LOCALRUN_DATAROOT** environment variable.</span></span>

    <span data-ttu-id="f1e53-211">定義一個名為 **LOCALRUN_DATAROOT** 的新環境變數指向資料根目錄。</span><span class="sxs-lookup"><span data-stu-id="f1e53-211">Define a new environment variable called **LOCALRUN_DATAROOT** that points to the data root.</span></span>

    <span data-ttu-id="f1e53-212">除了設定環境變數，您可以在使用命令列時對資料根目錄路徑指定 **-DataRoot** 引數。</span><span class="sxs-lookup"><span data-stu-id="f1e53-212">In addition to setting the environment variable, you can specify the **-DataRoot** argument with the data-root path when you're using a command line.</span></span> <span data-ttu-id="f1e53-213">這個引數會覆寫預設的資料根環境變數。</span><span class="sxs-lookup"><span data-stu-id="f1e53-213">This argument overwrites your default data-root environment variable.</span></span> <span data-ttu-id="f1e53-214">您必須將這個引數加入您要執行的每個命令列，以覆寫所有作業的預設資料根環境變數。</span><span class="sxs-lookup"><span data-stu-id="f1e53-214">You need to add this argument to every command line you're running so that you can overwrite the default data-root environment variable for all operations.</span></span>

### <a name="sdk-command-line-usage-samples"></a><span data-ttu-id="f1e53-215">SDK 命令列使用範例</span><span class="sxs-lookup"><span data-stu-id="f1e53-215">SDK command line usage samples</span></span>

#### <a name="compile-and-run"></a><span data-ttu-id="f1e53-216">編譯和執行</span><span class="sxs-lookup"><span data-stu-id="f1e53-216">Compile and run</span></span>

<span data-ttu-id="f1e53-217">**run** 命令用來編譯指令碼，然後執行編譯的結果。</span><span class="sxs-lookup"><span data-stu-id="f1e53-217">The **run** command is used to compile the script and then execute compiled results.</span></span> <span data-ttu-id="f1e53-218">其命令列引數結合 **compile** 和 **excute** 的引數。</span><span class="sxs-lookup"><span data-stu-id="f1e53-218">Its command-line arguments are a combination of those from **compile** and **execute**.</span></span>

    LocalRunHelper run -Script path_to_usql_script.usql [optional_arguments]

<span data-ttu-id="f1e53-219">下列為 **run** 的選擇性引數：</span><span class="sxs-lookup"><span data-stu-id="f1e53-219">The following are optional arguments for **run**:</span></span>


|<span data-ttu-id="f1e53-220">引數</span><span class="sxs-lookup"><span data-stu-id="f1e53-220">Argument</span></span>|<span data-ttu-id="f1e53-221">預設值</span><span class="sxs-lookup"><span data-stu-id="f1e53-221">Default value</span></span>|<span data-ttu-id="f1e53-222">說明</span><span class="sxs-lookup"><span data-stu-id="f1e53-222">Description</span></span>|
|--------|-------------|-----------|
|<span data-ttu-id="f1e53-223">-CodeBehind</span><span class="sxs-lookup"><span data-stu-id="f1e53-223">-CodeBehind</span></span>|<span data-ttu-id="f1e53-224">False</span><span class="sxs-lookup"><span data-stu-id="f1e53-224">False</span></span>|<span data-ttu-id="f1e53-225">指令碼具有.cs 程式碼後置</span><span class="sxs-lookup"><span data-stu-id="f1e53-225">The script has .cs code behind</span></span>|
|<span data-ttu-id="f1e53-226">-CppSDK</span><span class="sxs-lookup"><span data-stu-id="f1e53-226">-CppSDK</span></span>| |<span data-ttu-id="f1e53-227">CppSDK 目錄</span><span class="sxs-lookup"><span data-stu-id="f1e53-227">CppSDK Directory</span></span>|
|<span data-ttu-id="f1e53-228">-DataRoot</span><span class="sxs-lookup"><span data-stu-id="f1e53-228">-DataRoot</span></span>| <span data-ttu-id="f1e53-229">DataRoot 環境變數</span><span class="sxs-lookup"><span data-stu-id="f1e53-229">DataRoot environment variable</span></span>|<span data-ttu-id="f1e53-230">本機執行的 DataRoot，預設為 'LOCALRUN_DATAROOT' 環境變數</span><span class="sxs-lookup"><span data-stu-id="f1e53-230">DataRoot for local run, default to 'LOCALRUN_DATAROOT' environment variable</span></span>|
|<span data-ttu-id="f1e53-231">-MessageOut</span><span class="sxs-lookup"><span data-stu-id="f1e53-231">-MessageOut</span></span>| |<span data-ttu-id="f1e53-232">將主控台上的訊息傾印成檔案</span><span class="sxs-lookup"><span data-stu-id="f1e53-232">Dump messages on console to a file</span></span>|
|<span data-ttu-id="f1e53-233">-Parallel</span><span class="sxs-lookup"><span data-stu-id="f1e53-233">-Parallel</span></span>|<span data-ttu-id="f1e53-234">1</span><span class="sxs-lookup"><span data-stu-id="f1e53-234">1</span></span>|<span data-ttu-id="f1e53-235">使用指定的平行處理原則執行計畫</span><span class="sxs-lookup"><span data-stu-id="f1e53-235">Run the plan with the specified parallelism</span></span>|
|<span data-ttu-id="f1e53-236">-References</span><span class="sxs-lookup"><span data-stu-id="f1e53-236">-References</span></span>| |<span data-ttu-id="f1e53-237">列出程式碼後置額外的參考組件或資料檔案的路徑，以 ';' 分隔</span><span class="sxs-lookup"><span data-stu-id="f1e53-237">List of paths to extra reference assemblies or data files of code behind, separated by ';'</span></span>|
|<span data-ttu-id="f1e53-238">-UdoRedirect</span><span class="sxs-lookup"><span data-stu-id="f1e53-238">-UdoRedirect</span></span>|<span data-ttu-id="f1e53-239">False</span><span class="sxs-lookup"><span data-stu-id="f1e53-239">False</span></span>|<span data-ttu-id="f1e53-240">產生 Udo 組件重新導向設定</span><span class="sxs-lookup"><span data-stu-id="f1e53-240">Generate Udo assembly redirect config</span></span>|
|<span data-ttu-id="f1e53-241">-UseDatabase</span><span class="sxs-lookup"><span data-stu-id="f1e53-241">-UseDatabase</span></span>|<span data-ttu-id="f1e53-242">master</span><span class="sxs-lookup"><span data-stu-id="f1e53-242">master</span></span>|<span data-ttu-id="f1e53-243">供程式碼後置暫時註冊組件使用的資料庫</span><span class="sxs-lookup"><span data-stu-id="f1e53-243">Database to use for code behind temporary assembly registration</span></span>|
|<span data-ttu-id="f1e53-244">-Verbose</span><span class="sxs-lookup"><span data-stu-id="f1e53-244">-Verbose</span></span>|<span data-ttu-id="f1e53-245">False</span><span class="sxs-lookup"><span data-stu-id="f1e53-245">False</span></span>|<span data-ttu-id="f1e53-246">顯示詳細的執行階段輸出</span><span class="sxs-lookup"><span data-stu-id="f1e53-246">Show detailed outputs from runtime</span></span>|
|<span data-ttu-id="f1e53-247">-WorkDir</span><span class="sxs-lookup"><span data-stu-id="f1e53-247">-WorkDir</span></span>|<span data-ttu-id="f1e53-248">目前的目錄</span><span class="sxs-lookup"><span data-stu-id="f1e53-248">Current Directory</span></span>|<span data-ttu-id="f1e53-249">編譯器使用方式和輸出的目錄</span><span class="sxs-lookup"><span data-stu-id="f1e53-249">Directory for compiler usage and outputs</span></span>|
|<span data-ttu-id="f1e53-250">-RunScopeCEP</span><span class="sxs-lookup"><span data-stu-id="f1e53-250">-RunScopeCEP</span></span>|<span data-ttu-id="f1e53-251">0</span><span class="sxs-lookup"><span data-stu-id="f1e53-251">0</span></span>|<span data-ttu-id="f1e53-252">要使用的 ScopeCEP 模式</span><span class="sxs-lookup"><span data-stu-id="f1e53-252">ScopeCEP mode to use</span></span>|
|<span data-ttu-id="f1e53-253">-ScopeCEPTempPath</span><span class="sxs-lookup"><span data-stu-id="f1e53-253">-ScopeCEPTempPath</span></span>|<span data-ttu-id="f1e53-254">temp</span><span class="sxs-lookup"><span data-stu-id="f1e53-254">temp</span></span>|<span data-ttu-id="f1e53-255">用於串流資料的暫存路徑</span><span class="sxs-lookup"><span data-stu-id="f1e53-255">Temp path to use for streaming data</span></span>|
|<span data-ttu-id="f1e53-256">-OptFlags</span><span class="sxs-lookup"><span data-stu-id="f1e53-256">-OptFlags</span></span>| |<span data-ttu-id="f1e53-257">最佳化工具旗標的逗號分隔清單</span><span class="sxs-lookup"><span data-stu-id="f1e53-257">Comma-separated list of optimizer flags</span></span>|


<span data-ttu-id="f1e53-258">以下是範例：</span><span class="sxs-lookup"><span data-stu-id="f1e53-258">Here's an example:</span></span>

    LocalRunHelper run -Script d:\test\test1.usql -WorkDir d:\test\bin -CodeBehind -References "d:\asm\ref1.dll;d:\asm\ref2.dll" -UseDatabase testDB –Parallel 5 -Verbose

<span data-ttu-id="f1e53-259">除了結合 **compile** 和 **excute**，您可以分別編譯和執行已編譯的可執行檔。</span><span class="sxs-lookup"><span data-stu-id="f1e53-259">Besides combining **compile** and **execute**, you can compile and execute the compiled executables separately.</span></span>

#### <a name="compile-a-u-sql-script"></a><span data-ttu-id="f1e53-260">編譯 U-SQL 指令碼</span><span class="sxs-lookup"><span data-stu-id="f1e53-260">Compile a U-SQL script</span></span>

<span data-ttu-id="f1e53-261">**compile** 命令用來將 U-SQL 指令碼編譯為可執行檔。</span><span class="sxs-lookup"><span data-stu-id="f1e53-261">The **compile** command is used to compile a U-SQL script to executables.</span></span>

    LocalRunHelper compile -Script path_to_usql_script.usql [optional_arguments]

<span data-ttu-id="f1e53-262">下列為 **compile** 的選擇性引數：</span><span class="sxs-lookup"><span data-stu-id="f1e53-262">The following are optional arguments for **compile**:</span></span>


|<span data-ttu-id="f1e53-263">引數</span><span class="sxs-lookup"><span data-stu-id="f1e53-263">Argument</span></span>|<span data-ttu-id="f1e53-264">說明</span><span class="sxs-lookup"><span data-stu-id="f1e53-264">Description</span></span>|
|--------|-----------|
| <span data-ttu-id="f1e53-265">-CodeBehind [預設值 'False']</span><span class="sxs-lookup"><span data-stu-id="f1e53-265">-CodeBehind [default value 'False']</span></span>|<span data-ttu-id="f1e53-266">指令碼具有.cs 程式碼後置</span><span class="sxs-lookup"><span data-stu-id="f1e53-266">The script has .cs code behind</span></span>|
| <span data-ttu-id="f1e53-267">-CppSDK [預設值 '']</span><span class="sxs-lookup"><span data-stu-id="f1e53-267">-CppSDK [default value '']</span></span>|<span data-ttu-id="f1e53-268">CppSDK 目錄</span><span class="sxs-lookup"><span data-stu-id="f1e53-268">CppSDK Directory</span></span>|
| <span data-ttu-id="f1e53-269">-DataRoot [預設值 'DataRoot environment variable']</span><span class="sxs-lookup"><span data-stu-id="f1e53-269">-DataRoot [default value 'DataRoot environment variable']</span></span>|<span data-ttu-id="f1e53-270">本機執行的 DataRoot，預設為 'LOCALRUN_DATAROOT' 環境變數</span><span class="sxs-lookup"><span data-stu-id="f1e53-270">DataRoot for local run, default to 'LOCALRUN_DATAROOT' environment variable</span></span>|
| <span data-ttu-id="f1e53-271">-MessageOut [預設值 '']</span><span class="sxs-lookup"><span data-stu-id="f1e53-271">-MessageOut [default value '']</span></span>|<span data-ttu-id="f1e53-272">將主控台上的訊息傾印成檔案</span><span class="sxs-lookup"><span data-stu-id="f1e53-272">Dump messages on console to a file</span></span>|
| <span data-ttu-id="f1e53-273">-References [預設值 '']</span><span class="sxs-lookup"><span data-stu-id="f1e53-273">-References [default value '']</span></span>|<span data-ttu-id="f1e53-274">列出程式碼後置額外的參考組件或資料檔案的路徑，以 ';' 分隔</span><span class="sxs-lookup"><span data-stu-id="f1e53-274">List of paths to extra reference assemblies or data files of code behind, separated by ';'</span></span>|
| <span data-ttu-id="f1e53-275">-Shallow [預設值 'False']</span><span class="sxs-lookup"><span data-stu-id="f1e53-275">-Shallow [default value 'False']</span></span>|<span data-ttu-id="f1e53-276">淺層編譯</span><span class="sxs-lookup"><span data-stu-id="f1e53-276">Shallow compile</span></span>|
| <span data-ttu-id="f1e53-277">-UdoRedirect [預設值 'False']</span><span class="sxs-lookup"><span data-stu-id="f1e53-277">-UdoRedirect [default value 'False']</span></span>|<span data-ttu-id="f1e53-278">產生 Udo 組件重新導向設定</span><span class="sxs-lookup"><span data-stu-id="f1e53-278">Generate Udo assembly redirect config</span></span>|
| <span data-ttu-id="f1e53-279">-UseDatabase [預設值 'master']</span><span class="sxs-lookup"><span data-stu-id="f1e53-279">-UseDatabase [default value 'master']</span></span>|<span data-ttu-id="f1e53-280">供程式碼後置暫時註冊組件使用的資料庫</span><span class="sxs-lookup"><span data-stu-id="f1e53-280">Database to use for code behind temporary assembly registration</span></span>|
| <span data-ttu-id="f1e53-281">-WorkDir [預設值 'Current Directory']</span><span class="sxs-lookup"><span data-stu-id="f1e53-281">-WorkDir [default value 'Current Directory']</span></span>|<span data-ttu-id="f1e53-282">編譯器使用方式和輸出的目錄</span><span class="sxs-lookup"><span data-stu-id="f1e53-282">Directory for compiler usage and outputs</span></span>|
| <span data-ttu-id="f1e53-283">-RunScopeCEP [預設值 '0']</span><span class="sxs-lookup"><span data-stu-id="f1e53-283">-RunScopeCEP [default value '0']</span></span>|<span data-ttu-id="f1e53-284">要使用的 ScopeCEP 模式</span><span class="sxs-lookup"><span data-stu-id="f1e53-284">ScopeCEP mode to use</span></span>|
| <span data-ttu-id="f1e53-285">-ScopeCEPTempPath [預設值 'temp']</span><span class="sxs-lookup"><span data-stu-id="f1e53-285">-ScopeCEPTempPath [default value 'temp']</span></span>|<span data-ttu-id="f1e53-286">用於串流資料的暫存路徑</span><span class="sxs-lookup"><span data-stu-id="f1e53-286">Temp path to use for streaming data</span></span>|
| <span data-ttu-id="f1e53-287">-OptFlags [預設值 '']</span><span class="sxs-lookup"><span data-stu-id="f1e53-287">-OptFlags [default value '']</span></span>|<span data-ttu-id="f1e53-288">最佳化工具旗標的逗號分隔清單</span><span class="sxs-lookup"><span data-stu-id="f1e53-288">Comma-separated list of optimizer flags</span></span>|


<span data-ttu-id="f1e53-289">這裡有一些使用範例。</span><span class="sxs-lookup"><span data-stu-id="f1e53-289">Here are some usage examples.</span></span>

<span data-ttu-id="f1e53-290">編譯 U-SQL 指令碼：</span><span class="sxs-lookup"><span data-stu-id="f1e53-290">Compile a U-SQL script:</span></span>

    LocalRunHelper compile -Script d:\test\test1.usql

<span data-ttu-id="f1e53-291">編譯 U-SQL 指令碼並設定資料根資料夾。</span><span class="sxs-lookup"><span data-stu-id="f1e53-291">Compile a U-SQL script and set the data-root folder.</span></span> <span data-ttu-id="f1e53-292">請注意，這將會覆寫設定環境變數。</span><span class="sxs-lookup"><span data-stu-id="f1e53-292">Note that this will overwrite the set environment variable.</span></span>

    LocalRunHelper compile -Script d:\test\test1.usql –DataRoot c:\DataRoot

<span data-ttu-id="f1e53-293">編譯 U-SQL 指令碼並設定工作目錄、參考組件和資料庫：</span><span class="sxs-lookup"><span data-stu-id="f1e53-293">Compile a U-SQL script and set a working directory, reference assembly, and database:</span></span>

    LocalRunHelper compile -Script d:\test\test1.usql -WorkDir d:\test\bin -References "d:\asm\ref1.dll;d:\asm\ref2.dll" -UseDatabase testDB

#### <a name="execute-compiled-results"></a><span data-ttu-id="f1e53-294">執行編譯的結果</span><span class="sxs-lookup"><span data-stu-id="f1e53-294">Execute compiled results</span></span>

<span data-ttu-id="f1e53-295">**execute** 命令用來執行編譯的結果。</span><span class="sxs-lookup"><span data-stu-id="f1e53-295">The **execute** command is used to execute compiled results.</span></span>   

    LocalRunHelper execute -Algebra path_to_compiled_algebra_file [optional_arguments]

<span data-ttu-id="f1e53-296">下列為 **execute** 的選擇性引數：</span><span class="sxs-lookup"><span data-stu-id="f1e53-296">The following are optional arguments for **execute**:</span></span>

|<span data-ttu-id="f1e53-297">引數</span><span class="sxs-lookup"><span data-stu-id="f1e53-297">Argument</span></span>|<span data-ttu-id="f1e53-298">說明</span><span class="sxs-lookup"><span data-stu-id="f1e53-298">Description</span></span>|
|--------|-----------|
|<span data-ttu-id="f1e53-299">-DataRoot [預設值 '']</span><span class="sxs-lookup"><span data-stu-id="f1e53-299">-DataRoot [default value '']</span></span>|<span data-ttu-id="f1e53-300">中繼資料執行的資料根。</span><span class="sxs-lookup"><span data-stu-id="f1e53-300">Data root for metadata execution.</span></span> <span data-ttu-id="f1e53-301">它預設為 **LOCALRUN_DATAROOT** 環境變數。</span><span class="sxs-lookup"><span data-stu-id="f1e53-301">It defaults to the **LOCALRUN_DATAROOT** environment variable.</span></span>|
|<span data-ttu-id="f1e53-302">-MessageOut [預設值 '']</span><span class="sxs-lookup"><span data-stu-id="f1e53-302">-MessageOut [default value '']</span></span>|<span data-ttu-id="f1e53-303">將主控台上的訊息傾印成檔案。</span><span class="sxs-lookup"><span data-stu-id="f1e53-303">Dump messages on the console to a file.</span></span>|
|<span data-ttu-id="f1e53-304">-Parallel [預設值 '1']</span><span class="sxs-lookup"><span data-stu-id="f1e53-304">-Parallel [default value '1']</span></span>|<span data-ttu-id="f1e53-305">使用指定的平行處理原則層級執行產生本機執行步驟的指示器。</span><span class="sxs-lookup"><span data-stu-id="f1e53-305">Indicator to run the generated local-run steps with the specified parallelism level.</span></span>|
|<span data-ttu-id="f1e53-306">-Verbose [預設值 'False']</span><span class="sxs-lookup"><span data-stu-id="f1e53-306">-Verbose [default value 'False']</span></span>|<span data-ttu-id="f1e53-307">顯示詳細執行階段輸出的指示器。</span><span class="sxs-lookup"><span data-stu-id="f1e53-307">Indicator to show detailed outputs from runtime.</span></span>|

<span data-ttu-id="f1e53-308">以下是使用範例︰</span><span class="sxs-lookup"><span data-stu-id="f1e53-308">Here's a usage example:</span></span>

    LocalRunHelper execute -Algebra d:\test\workdir\C6A101DDCB470506\Script_66AE4909AA0ED06C\__script__.abr –DataRoot c:\DataRoot –Parallel 5


## <a name="use-the-sdk-with-programming-interfaces"></a><span data-ttu-id="f1e53-309">透過程式設計介面使用 SDK</span><span class="sxs-lookup"><span data-stu-id="f1e53-309">Use the SDK with programming interfaces</span></span>

<span data-ttu-id="f1e53-310">程式設計介面都位於 LocalRunHelper.exe 中。</span><span class="sxs-lookup"><span data-stu-id="f1e53-310">The programming interfaces are all located in the LocalRunHelper.exe.</span></span> <span data-ttu-id="f1e53-311">您可以使用它們來整合 U-SQL SDK 的功能性及 C# 測試架構，以調整您的 U-SQL 指令碼本機測試。</span><span class="sxs-lookup"><span data-stu-id="f1e53-311">You can use them to integrate the functionality of the U-SQL SDK and the C# test framework to scale your U-SQL script local test.</span></span> <span data-ttu-id="f1e53-312">在此文章中，我將會使用標準 C# 單元測試專案來示範如何使用這些介面來測試您的 U-SQL 指令碼。</span><span class="sxs-lookup"><span data-stu-id="f1e53-312">In this article, I will use the standard C# unit test project to show how to use these interfaces to test your U-SQL script.</span></span>

### <a name="step-1-create-c-unit-test-project-and-configuration"></a><span data-ttu-id="f1e53-313">步驟 1︰建立 C# 單元測試專案和設定</span><span class="sxs-lookup"><span data-stu-id="f1e53-313">Step 1: Create C# unit test project and configuration</span></span>

- <span data-ttu-id="f1e53-314">透過 [檔案] > [新增] > [專案] > [Visual C#] > [測試] > [單元測試專案] 來建立 C# 單元測試專案。</span><span class="sxs-lookup"><span data-stu-id="f1e53-314">Create a C# unit test project through File > New > Project > Visual C# > Test > Unit Test Project.</span></span>
- <span data-ttu-id="f1e53-315">加入 LocalRunHelper.exe 做為專案的參考。</span><span class="sxs-lookup"><span data-stu-id="f1e53-315">Add LocalRunHelper.exe as a reference for the project.</span></span> <span data-ttu-id="f1e53-316">LocalRunHelper.exe 位於 Nuget 套件中的 \build\runtime\LocalRunHelper.exe。</span><span class="sxs-lookup"><span data-stu-id="f1e53-316">The LocalRunHelper.exe is located at \build\runtime\LocalRunHelper.exe in Nuget package.</span></span>

    ![Azure Data Lake U-SQL SDK 加入參考](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-add-reference.png)

- <span data-ttu-id="f1e53-318">U-SQL SDK「僅」支援 x64 環境，請務必將建置平台目標設定為 [x64]。</span><span class="sxs-lookup"><span data-stu-id="f1e53-318">U-SQL SDK **only** support x64 environment, make sure to set build platform target as x64.</span></span> <span data-ttu-id="f1e53-319">您可以透過 [專案屬性] > [建置] > [平台目標] 來設定。</span><span class="sxs-lookup"><span data-stu-id="f1e53-319">You can set that through Project Property > Build > Platform target.</span></span>

    ![Azure Data Lake U-SQL SDK 設定 x64 專案](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-configure-x64.png)

- <span data-ttu-id="f1e53-321">請務必將測試環境設定為 [x64]。</span><span class="sxs-lookup"><span data-stu-id="f1e53-321">Make sure to set your test environment as x64.</span></span> <span data-ttu-id="f1e53-322">在 Visual Studio 中，您可以透過 [測試] > [測試設定] > [預設處理器架構] > [x64] 來設定。</span><span class="sxs-lookup"><span data-stu-id="f1e53-322">In Visual Studio, you can set it through Test > Test Settings > Default Processor Architecture > x64.</span></span>

    ![Azure Data Lake U-SQL SDK 設定 x64 測試環境](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-configure-test-x64.png)

- <span data-ttu-id="f1e53-324">請務必將 NugetPackage\build\runtime\ 下的所有相依性檔案複製到專案工作目錄 (通常位於 ProjectFolder\bin\x64\Debug 之下)。</span><span class="sxs-lookup"><span data-stu-id="f1e53-324">Make sure to copy all dependency files under NugetPackage\build\runtime\ to project working directory which is usually under ProjectFolder\bin\x64\Debug.</span></span>

### <a name="step-2-create-u-sql-script-test-case"></a><span data-ttu-id="f1e53-325">步驟 2：建立 U-SQL 指令碼測試案例</span><span class="sxs-lookup"><span data-stu-id="f1e53-325">Step 2: Create U-SQL script test case</span></span>

<span data-ttu-id="f1e53-326">以下是 U-SQL 指令碼測試的範例程式碼。</span><span class="sxs-lookup"><span data-stu-id="f1e53-326">Below is the sample code for U-SQL script test.</span></span> <span data-ttu-id="f1e53-327">若要進行測試，您需要準備指令碼、輸入檔和預期的輸出檔。</span><span class="sxs-lookup"><span data-stu-id="f1e53-327">For testing, you need to prepare scripts, input files and expected output files.</span></span>

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
                //Specify the local run message output path
                StreamWriter MessageOutput = new StreamWriter("../../../log.txt");

                LocalRunHelper localrun = new LocalRunHelper(MessageOutput);

                //Configure the DateRoot path, Script Path and CPPSDK path
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

                //Don't forget to close MessageOutput to get logs into file
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


### <a name="programming-interfaces-in-localrunhelperexe"></a><span data-ttu-id="f1e53-328">LocalRunHelper.exe 中的程式設計介面</span><span class="sxs-lookup"><span data-stu-id="f1e53-328">Programming interfaces in LocalRunHelper.exe</span></span>

<span data-ttu-id="f1e53-329">LocalRunHelper.exe 提供 U-SQL 本機編譯、執行等等的程式設計介面。介面如下所列。</span><span class="sxs-lookup"><span data-stu-id="f1e53-329">LocalRunHelper.exe provides the programming interfaces for U-SQL local compile, run, etc. The interfaces are listed as follows.</span></span>

<span data-ttu-id="f1e53-330">**建構函式**</span><span class="sxs-lookup"><span data-stu-id="f1e53-330">**Constructor**</span></span>

<span data-ttu-id="f1e53-331">public LocalRunHelper([System.IO.TextWriter messageOutput = null])</span><span class="sxs-lookup"><span data-stu-id="f1e53-331">public LocalRunHelper([System.IO.TextWriter messageOutput = null])</span></span>

|<span data-ttu-id="f1e53-332">參數</span><span class="sxs-lookup"><span data-stu-id="f1e53-332">Parameter</span></span>|<span data-ttu-id="f1e53-333">類型</span><span class="sxs-lookup"><span data-stu-id="f1e53-333">Type</span></span>|<span data-ttu-id="f1e53-334">說明</span><span class="sxs-lookup"><span data-stu-id="f1e53-334">Description</span></span>|
|---------|----|-----------|
|<span data-ttu-id="f1e53-335">messageOutput</span><span class="sxs-lookup"><span data-stu-id="f1e53-335">messageOutput</span></span>|<span data-ttu-id="f1e53-336">System.IO.TextWriter</span><span class="sxs-lookup"><span data-stu-id="f1e53-336">System.IO.TextWriter</span></span>|<span data-ttu-id="f1e53-337">針對輸出訊息，請設為 null 以使用主控台</span><span class="sxs-lookup"><span data-stu-id="f1e53-337">for output messages, set to null to use Console</span></span>|

<span data-ttu-id="f1e53-338">**屬性**</span><span class="sxs-lookup"><span data-stu-id="f1e53-338">**Properties**</span></span>

|<span data-ttu-id="f1e53-339">屬性</span><span class="sxs-lookup"><span data-stu-id="f1e53-339">Property</span></span>|<span data-ttu-id="f1e53-340">類型</span><span class="sxs-lookup"><span data-stu-id="f1e53-340">Type</span></span>|<span data-ttu-id="f1e53-341">說明</span><span class="sxs-lookup"><span data-stu-id="f1e53-341">Description</span></span>|
|--------|----|-----------|
|<span data-ttu-id="f1e53-342">AlgebraPath</span><span class="sxs-lookup"><span data-stu-id="f1e53-342">AlgebraPath</span></span>|<span data-ttu-id="f1e53-343">字串</span><span class="sxs-lookup"><span data-stu-id="f1e53-343">string</span></span>|<span data-ttu-id="f1e53-344">代數檔案的路徑 (代數檔案是其中一個編譯結果)</span><span class="sxs-lookup"><span data-stu-id="f1e53-344">The path to algebra file (algebra file is one of the compilation results)</span></span>|
|<span data-ttu-id="f1e53-345">CodeBehindReferences</span><span class="sxs-lookup"><span data-stu-id="f1e53-345">CodeBehindReferences</span></span>|<span data-ttu-id="f1e53-346">string</span><span class="sxs-lookup"><span data-stu-id="f1e53-346">string</span></span>|<span data-ttu-id="f1e53-347">如果指令碼具有其他程式碼後置參考，請指定路徑並以 ';' 分隔</span><span class="sxs-lookup"><span data-stu-id="f1e53-347">If the script has additional code behind references, specify the paths separated with ';'</span></span>|
|<span data-ttu-id="f1e53-348">CppSdkDir</span><span class="sxs-lookup"><span data-stu-id="f1e53-348">CppSdkDir</span></span>|<span data-ttu-id="f1e53-349">字串</span><span class="sxs-lookup"><span data-stu-id="f1e53-349">string</span></span>|<span data-ttu-id="f1e53-350">CppSDK 目錄</span><span class="sxs-lookup"><span data-stu-id="f1e53-350">CppSDK directory</span></span>|
|<span data-ttu-id="f1e53-351">CurrentDir</span><span class="sxs-lookup"><span data-stu-id="f1e53-351">CurrentDir</span></span>|<span data-ttu-id="f1e53-352">字串</span><span class="sxs-lookup"><span data-stu-id="f1e53-352">string</span></span>|<span data-ttu-id="f1e53-353">目前的目錄</span><span class="sxs-lookup"><span data-stu-id="f1e53-353">Current directory</span></span>|
|<span data-ttu-id="f1e53-354">DataRoot</span><span class="sxs-lookup"><span data-stu-id="f1e53-354">DataRoot</span></span>|<span data-ttu-id="f1e53-355">string</span><span class="sxs-lookup"><span data-stu-id="f1e53-355">string</span></span>|<span data-ttu-id="f1e53-356">資料根路徑</span><span class="sxs-lookup"><span data-stu-id="f1e53-356">Data root path</span></span>|
|<span data-ttu-id="f1e53-357">DebuggerMailPath</span><span class="sxs-lookup"><span data-stu-id="f1e53-357">DebuggerMailPath</span></span>|<span data-ttu-id="f1e53-358">字串</span><span class="sxs-lookup"><span data-stu-id="f1e53-358">string</span></span>|<span data-ttu-id="f1e53-359">偵錯工具郵件槽的路徑</span><span class="sxs-lookup"><span data-stu-id="f1e53-359">The path to debugger mailslot</span></span>|
|<span data-ttu-id="f1e53-360">GenerateUdoRedirect</span><span class="sxs-lookup"><span data-stu-id="f1e53-360">GenerateUdoRedirect</span></span>|<span data-ttu-id="f1e53-361">布林</span><span class="sxs-lookup"><span data-stu-id="f1e53-361">bool</span></span>|<span data-ttu-id="f1e53-362">是否要產生載入重新導向覆寫設定的組件</span><span class="sxs-lookup"><span data-stu-id="f1e53-362">If we want to generate assembly loading redirection override config</span></span>|
|<span data-ttu-id="f1e53-363">HasCodeBehind</span><span class="sxs-lookup"><span data-stu-id="f1e53-363">HasCodeBehind</span></span>|<span data-ttu-id="f1e53-364">布林</span><span class="sxs-lookup"><span data-stu-id="f1e53-364">bool</span></span>|<span data-ttu-id="f1e53-365">指令碼是否具有程式碼後置</span><span class="sxs-lookup"><span data-stu-id="f1e53-365">If the script has code behind</span></span>|
|<span data-ttu-id="f1e53-366">InputDir</span><span class="sxs-lookup"><span data-stu-id="f1e53-366">InputDir</span></span>|<span data-ttu-id="f1e53-367">string</span><span class="sxs-lookup"><span data-stu-id="f1e53-367">string</span></span>|<span data-ttu-id="f1e53-368">輸入資料的目錄</span><span class="sxs-lookup"><span data-stu-id="f1e53-368">Directory for input data</span></span>|
|<span data-ttu-id="f1e53-369">MessagePath</span><span class="sxs-lookup"><span data-stu-id="f1e53-369">MessagePath</span></span>|<span data-ttu-id="f1e53-370">字串</span><span class="sxs-lookup"><span data-stu-id="f1e53-370">string</span></span>|<span data-ttu-id="f1e53-371">訊息傾印檔案路徑</span><span class="sxs-lookup"><span data-stu-id="f1e53-371">Message dump file path</span></span>|
|<span data-ttu-id="f1e53-372">OutputDir</span><span class="sxs-lookup"><span data-stu-id="f1e53-372">OutputDir</span></span>|<span data-ttu-id="f1e53-373">string</span><span class="sxs-lookup"><span data-stu-id="f1e53-373">string</span></span>|<span data-ttu-id="f1e53-374">輸出資料的目錄</span><span class="sxs-lookup"><span data-stu-id="f1e53-374">Directory for output data</span></span>|
|<span data-ttu-id="f1e53-375">平行處理原則</span><span class="sxs-lookup"><span data-stu-id="f1e53-375">Parallelism</span></span>|<span data-ttu-id="f1e53-376">int</span><span class="sxs-lookup"><span data-stu-id="f1e53-376">int</span></span>|<span data-ttu-id="f1e53-377">執行代數的平行處理原則</span><span class="sxs-lookup"><span data-stu-id="f1e53-377">Parallelism to run the algebra</span></span>|
|<span data-ttu-id="f1e53-378">ParentPid</span><span class="sxs-lookup"><span data-stu-id="f1e53-378">ParentPid</span></span>|<span data-ttu-id="f1e53-379">int</span><span class="sxs-lookup"><span data-stu-id="f1e53-379">int</span></span>|<span data-ttu-id="f1e53-380">服務監視器結束的父項 PID，設定為 0 或負數以略過</span><span class="sxs-lookup"><span data-stu-id="f1e53-380">PID of the parent on which the service monitors to exit, set to 0 or negative to ignore</span></span>|
|<span data-ttu-id="f1e53-381">ResultPath</span><span class="sxs-lookup"><span data-stu-id="f1e53-381">ResultPath</span></span>|<span data-ttu-id="f1e53-382">字串</span><span class="sxs-lookup"><span data-stu-id="f1e53-382">string</span></span>|<span data-ttu-id="f1e53-383">結果傾印檔案路徑</span><span class="sxs-lookup"><span data-stu-id="f1e53-383">Result dump file path</span></span>|
|<span data-ttu-id="f1e53-384">RuntimeDir</span><span class="sxs-lookup"><span data-stu-id="f1e53-384">RuntimeDir</span></span>|<span data-ttu-id="f1e53-385">字串</span><span class="sxs-lookup"><span data-stu-id="f1e53-385">string</span></span>|<span data-ttu-id="f1e53-386">執行階段目錄</span><span class="sxs-lookup"><span data-stu-id="f1e53-386">Runtime directory</span></span>|
|<span data-ttu-id="f1e53-387">ScriptPath</span><span class="sxs-lookup"><span data-stu-id="f1e53-387">ScriptPath</span></span>|<span data-ttu-id="f1e53-388">string</span><span class="sxs-lookup"><span data-stu-id="f1e53-388">string</span></span>|<span data-ttu-id="f1e53-389">尋找指令碼的位置</span><span class="sxs-lookup"><span data-stu-id="f1e53-389">Where to find the script</span></span>|
|<span data-ttu-id="f1e53-390">Shallow</span><span class="sxs-lookup"><span data-stu-id="f1e53-390">Shallow</span></span>|<span data-ttu-id="f1e53-391">布林</span><span class="sxs-lookup"><span data-stu-id="f1e53-391">bool</span></span>|<span data-ttu-id="f1e53-392">是否進行淺層編譯</span><span class="sxs-lookup"><span data-stu-id="f1e53-392">Shallow compile or not</span></span>|
|<span data-ttu-id="f1e53-393">TempDir</span><span class="sxs-lookup"><span data-stu-id="f1e53-393">TempDir</span></span>|<span data-ttu-id="f1e53-394">字串</span><span class="sxs-lookup"><span data-stu-id="f1e53-394">string</span></span>|<span data-ttu-id="f1e53-395">Temp 目錄</span><span class="sxs-lookup"><span data-stu-id="f1e53-395">Temp directory</span></span>|
|<span data-ttu-id="f1e53-396">UseDataBase</span><span class="sxs-lookup"><span data-stu-id="f1e53-396">UseDataBase</span></span>|<span data-ttu-id="f1e53-397">字串</span><span class="sxs-lookup"><span data-stu-id="f1e53-397">string</span></span>|<span data-ttu-id="f1e53-398">指定程式碼後置暫存組件註冊要使用的資料庫，預設為 master</span><span class="sxs-lookup"><span data-stu-id="f1e53-398">Specify the database to use for code behind temporary assembly registration, master by default</span></span>|
|<span data-ttu-id="f1e53-399">WorkDir</span><span class="sxs-lookup"><span data-stu-id="f1e53-399">WorkDir</span></span>|<span data-ttu-id="f1e53-400">字串</span><span class="sxs-lookup"><span data-stu-id="f1e53-400">string</span></span>|<span data-ttu-id="f1e53-401">慣用的工作目錄</span><span class="sxs-lookup"><span data-stu-id="f1e53-401">Preferred working directory</span></span>|


<span data-ttu-id="f1e53-402">**方法**</span><span class="sxs-lookup"><span data-stu-id="f1e53-402">**Method**</span></span>

|<span data-ttu-id="f1e53-403">方法</span><span class="sxs-lookup"><span data-stu-id="f1e53-403">Method</span></span>|<span data-ttu-id="f1e53-404">說明</span><span class="sxs-lookup"><span data-stu-id="f1e53-404">Description</span></span>|<span data-ttu-id="f1e53-405">傳回</span><span class="sxs-lookup"><span data-stu-id="f1e53-405">Return</span></span>|<span data-ttu-id="f1e53-406">參數</span><span class="sxs-lookup"><span data-stu-id="f1e53-406">Parameter</span></span>|
|------|-----------|------|---------|
|<span data-ttu-id="f1e53-407">public bool DoCompile()</span><span class="sxs-lookup"><span data-stu-id="f1e53-407">public bool DoCompile()</span></span>|<span data-ttu-id="f1e53-408">編譯 U-SQL 指令碼</span><span class="sxs-lookup"><span data-stu-id="f1e53-408">Compile the U-SQL script</span></span>|<span data-ttu-id="f1e53-409">成功時為 True</span><span class="sxs-lookup"><span data-stu-id="f1e53-409">True on success</span></span>| |
|<span data-ttu-id="f1e53-410">public bool DoExec()</span><span class="sxs-lookup"><span data-stu-id="f1e53-410">public bool DoExec()</span></span>|<span data-ttu-id="f1e53-411">執行編譯的結果</span><span class="sxs-lookup"><span data-stu-id="f1e53-411">Execute the compiled result</span></span>|<span data-ttu-id="f1e53-412">成功時為 True</span><span class="sxs-lookup"><span data-stu-id="f1e53-412">True on success</span></span>| |
|<span data-ttu-id="f1e53-413">public bool DoRun()</span><span class="sxs-lookup"><span data-stu-id="f1e53-413">public bool DoRun()</span></span>|<span data-ttu-id="f1e53-414">執行 U-SQL 指令碼 (編譯 + 執行)</span><span class="sxs-lookup"><span data-stu-id="f1e53-414">Run the U-SQL script (Compile + Execute)</span></span>|<span data-ttu-id="f1e53-415">成功時為 True</span><span class="sxs-lookup"><span data-stu-id="f1e53-415">True on success</span></span>| |
|<span data-ttu-id="f1e53-416">public bool IsValidRuntimeDir(string path)</span><span class="sxs-lookup"><span data-stu-id="f1e53-416">public bool IsValidRuntimeDir(string path)</span></span>|<span data-ttu-id="f1e53-417">檢查指定的路徑是否為有效的執行階段路徑</span><span class="sxs-lookup"><span data-stu-id="f1e53-417">Check if the given path is valid runtime path</span></span>|<span data-ttu-id="f1e53-418">有效則為 True</span><span class="sxs-lookup"><span data-stu-id="f1e53-418">True for valid</span></span>|<span data-ttu-id="f1e53-419">執行階段目錄的路徑</span><span class="sxs-lookup"><span data-stu-id="f1e53-419">The path of runtime directory</span></span>|


## <a name="faq-about-common-issue"></a><span data-ttu-id="f1e53-420">有關常見問題的常見問題集</span><span class="sxs-lookup"><span data-stu-id="f1e53-420">FAQ about common issue</span></span>

### <a name="error-1"></a><span data-ttu-id="f1e53-421">錯誤 1：</span><span class="sxs-lookup"><span data-stu-id="f1e53-421">Error 1:</span></span>
<span data-ttu-id="f1e53-422">E_CSC_SYSTEM_INTERNAL: 內部錯誤!</span><span class="sxs-lookup"><span data-stu-id="f1e53-422">E_CSC_SYSTEM_INTERNAL: Internal error!</span></span> <span data-ttu-id="f1e53-423">無法載入檔案或組件 'ScopeEngineManaged.dll' 或其相依性的其中之一。</span><span class="sxs-lookup"><span data-stu-id="f1e53-423">Could not load file or assembly 'ScopeEngineManaged.dll' or one of its dependencies.</span></span> <span data-ttu-id="f1e53-424">找不到指定的模組。</span><span class="sxs-lookup"><span data-stu-id="f1e53-424">The specified module could not be found.</span></span>

<span data-ttu-id="f1e53-425">請檢查下列項目：</span><span class="sxs-lookup"><span data-stu-id="f1e53-425">Please check the following:</span></span>

- <span data-ttu-id="f1e53-426">確定您使用 x64 環境。</span><span class="sxs-lookup"><span data-stu-id="f1e53-426">Make sure you have x64 environment.</span></span> <span data-ttu-id="f1e53-427">建置目標平台和測試環境應該要是 x64，請參閱上方的＜步驟 1︰建立 C# 單元測試專案和設定＞。</span><span class="sxs-lookup"><span data-stu-id="f1e53-427">The build target platform and the test environment should be x64, refer to **Step 1: Create C# unit test project and configuration** above.</span></span>
- <span data-ttu-id="f1e53-428">確定您已經將 NugetPackage\build\runtime\ 下的所有相依性檔案複製到專案工作目錄。</span><span class="sxs-lookup"><span data-stu-id="f1e53-428">Make sure you have copied all dependency files under NugetPackage\build\runtime\ to project working directory.</span></span>


## <a name="next-steps"></a><span data-ttu-id="f1e53-429">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f1e53-429">Next steps</span></span>

* <span data-ttu-id="f1e53-430">若要了解 U-SQL，請參閱 [開始使用 Azure Data Lake Analytics U-SQL 語言](data-lake-analytics-u-sql-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="f1e53-430">To learn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="f1e53-431">若要記錄診斷資訊，請參閱 [為 Azure Data Lake Analytics 存取診斷記錄檔](data-lake-analytics-diagnostic-logs.md)。</span><span class="sxs-lookup"><span data-stu-id="f1e53-431">To log diagnostics information, see [Accessing diagnostics logs for Azure Data Lake Analytics](data-lake-analytics-diagnostic-logs.md).</span></span>
* <span data-ttu-id="f1e53-432">若要了解更複雜的查詢，請參閱 [使用 Azure Data Lake Analytics 來分析網站記錄檔](data-lake-analytics-analyze-weblogs.md)。</span><span class="sxs-lookup"><span data-stu-id="f1e53-432">To see a more complex query, see [Analyze website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="f1e53-433">若要檢視作業詳細資料，請參閱[針對 Azure Data Lake Analytics 作業使用作業瀏覽器和作業檢視](data-lake-analytics-data-lake-tools-view-jobs.md)。</span><span class="sxs-lookup"><span data-stu-id="f1e53-433">To view job details, see [Use Job Browser and Job View for Azure Data Lake Analytics jobs](data-lake-analytics-data-lake-tools-view-jobs.md).</span></span>
* <span data-ttu-id="f1e53-434">若要使用頂點執行檢視，請參閱[在 Data Lake Tools for Visual Studio 中使用頂點執行檢視](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md)。</span><span class="sxs-lookup"><span data-stu-id="f1e53-434">To use the vertex execution view, see [Use the Vertex Execution View in Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).</span></span>
