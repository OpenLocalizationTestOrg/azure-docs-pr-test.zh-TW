---
title: "Azure Data Lake Tools：使用 Visual Studio Code 來進行 U-SQL 本機執行和本機偵錯 | Microsoft Docs"
description: "了解如何進行 toouse Azure 資料湖 Tools for Visual Studio Code toolocal 執行和本機偵錯。"
Keywords: "VScode，Azure 資料湖工具，本機執行，本機偵錯，本機偵錯預覽的儲存體檔案上, 傳 toostorage 路徑"
services: data-lake-analytics
documentationcenter: 
author: jejiang
manager: DJ
editor: jejiang
tags: azure-portal
ms.assetid: dc9b21d8-c5f4-4f77-bcbc-eff458f48de2
ms.service: data-lake-analytics
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: big-data
ms.date: 07/14/2017
ms.author: jejiang
ms.openlocfilehash: fb152f07fe8c4b03dde8fb8e62c7475eccda0578
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="u-sql-local-run-and-local-debug-with-visual-studio-code"></a><span data-ttu-id="7b152-104">使用 Visual Studio Code 來進行 U-SQL 本機執行和本機偵錯</span><span class="sxs-lookup"><span data-stu-id="7b152-104">U-SQL local run and local debug with Visual Studio Code</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7b152-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="7b152-105">Prerequisites</span></span>
<span data-ttu-id="7b152-106">請確定您有下列先決條件備妥，然後再開始這些程序的 hello:</span><span class="sxs-lookup"><span data-stu-id="7b152-106">Make sure you have hello following prerequisites in place before you start these procedures:</span></span>
- <span data-ttu-id="7b152-107">Azure Data Lake Tools for Visual Studio Code。</span><span class="sxs-lookup"><span data-stu-id="7b152-107">Azure Data Lake Tool for Visual Studio Code.</span></span> <span data-ttu-id="7b152-108">如需相關指示，請參閱[使用 Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md)。</span><span class="sxs-lookup"><span data-stu-id="7b152-108">For instructions, see [Use Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span></span>
- <span data-ttu-id="7b152-109">C# Visual Studio 程式碼 （如果您想 tooperform U-SQL 本機偵錯）。</span><span class="sxs-lookup"><span data-stu-id="7b152-109">C# for Visual Studio Code (if you want tooperform a U-SQL local debug).</span></span>

   ![安裝 Data Lake Tools for Visual Studio Code 中的 C#](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-install-ms-vscodecsharp.png)
   
   > [!NOTE]
   > <span data-ttu-id="7b152-111">hello U-SQL 本機執行和偵錯功能目前僅支援 Windows 使用者。</span><span class="sxs-lookup"><span data-stu-id="7b152-111">hello U-SQL local run and debug features currently only support Windows users.</span></span> 


## <a name="set-up-hello-u-sql-local-run-environment"></a><span data-ttu-id="7b152-112">設定 hello U-SQL 本機執行環境</span><span class="sxs-lookup"><span data-stu-id="7b152-112">Set up hello U-SQL local run environment</span></span>

1. <span data-ttu-id="7b152-113">選取 Ctrl + Shift + P tooopen hello 命令調色盤，然後輸入**ADL： 下載 LocalRun 相依性**toodownload hello 封裝。</span><span class="sxs-lookup"><span data-stu-id="7b152-113">Select Ctrl+Shift+P tooopen hello command palette, and then enter **ADL: Download LocalRun Dependency** toodownload hello packages.</span></span>  

   ![下載 hello ADL LocalRun 相依性套件](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/DownloadLocalRun.png)

2. <span data-ttu-id="7b152-115">找出 hello hello hello 所示的路徑中的相依性套件**輸出** 窗格中，然後安裝 BuildTools 及 Win10SDK 10240。</span><span class="sxs-lookup"><span data-stu-id="7b152-115">Locate hello dependency packages from hello path shown in hello **Output** pane, and then install BuildTools and Win10SDK 10240.</span></span> <span data-ttu-id="7b152-116">路徑範例如下：</span><span class="sxs-lookup"><span data-stu-id="7b152-116">Here is an example path:</span></span>  
`C:\Users\xxx\.vscode\extensions\usqlextpublisher.usql-vscode-ext-x.x.x\LocalRunDependency
`  
  <span data-ttu-id="7b152-117">![找出 hello 相依性套件](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/LocateDependencyPath.png)</span><span class="sxs-lookup"><span data-stu-id="7b152-117">![Locate hello dependency packages](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/LocateDependencyPath.png)</span></span>

   <span data-ttu-id="7b152-118">a.</span><span class="sxs-lookup"><span data-stu-id="7b152-118">a.</span></span> <span data-ttu-id="7b152-119">tooinstall BuildTools，依照 hello 精靈的指示。</span><span class="sxs-lookup"><span data-stu-id="7b152-119">tooinstall BuildTools, follow hello wizard instructions.</span></span>   

  ![安裝 BuildTools](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/InstallBuildTools.png)

   <span data-ttu-id="7b152-121">b.</span><span class="sxs-lookup"><span data-stu-id="7b152-121">b.</span></span> <span data-ttu-id="7b152-122">tooinstall Win10SDK 10240 依照 hello 精靈的指示。</span><span class="sxs-lookup"><span data-stu-id="7b152-122">tooinstall Win10SDK 10240, follow hello wizard instructions.</span></span>  

  ![安裝 Win10SDK 10240](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/InstallWin10SDK.png)

3. <span data-ttu-id="7b152-124">設定 hello 環境變數。</span><span class="sxs-lookup"><span data-stu-id="7b152-124">Set up hello environment variable.</span></span> <span data-ttu-id="7b152-125">設定 hello **SCOPE_CPP_SDK**環境變數：</span><span class="sxs-lookup"><span data-stu-id="7b152-125">Set hello **SCOPE_CPP_SDK** environment variable to:</span></span>  
`C:\Users\xxx\.vscode\extensions\usqlextpublisher.usql-vscode-ext-x.x.x\LocalRunDependency\CppSDK_3rdparty
`  
4. <span data-ttu-id="7b152-126">重新啟動 hello OS toomake 確定 hello 環境變數設定才會生效。</span><span class="sxs-lookup"><span data-stu-id="7b152-126">Restart hello OS toomake sure that hello environment variable settings take effect.</span></span>  

   ![請確定已安裝 hello SCOPE_CPP_SDK 環境變數](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/ConfigScopeCppSDk.png)

## <a name="start-hello-local-run-service-and-submit-hello-u-sql-job-tooa-local-account"></a><span data-ttu-id="7b152-128">啟動 hello 本機執行的服務，然後送出 hello U-SQL 作業 tooa 本機帳戶</span><span class="sxs-lookup"><span data-stu-id="7b152-128">Start hello local run service and submit hello U-SQL job tooa local account</span></span> 
<span data-ttu-id="7b152-129">Hello 第一次使用者，您會提示的 toodownload hello ADL： 如果尚未安裝的封裝下載 LocalRun 相依性。</span><span class="sxs-lookup"><span data-stu-id="7b152-129">For hello first-time user, you are prompted toodownload hello ADL: Download LocalRun Dependency packages if they are not already installed.</span></span>
1. <span data-ttu-id="7b152-130">選取 Ctrl + Shift + P tooopen hello 命令調色盤，然後輸入**ADL： 啟動本機執行服務**。</span><span class="sxs-lookup"><span data-stu-id="7b152-130">Select Ctrl+Shift+P tooopen hello command palette, and then enter **ADL: Start Local Run Service**.</span></span>
2. <span data-ttu-id="7b152-131">選取**接受**tooaccept hello hello 第一次的 Microsoft 軟體授權條款。</span><span class="sxs-lookup"><span data-stu-id="7b152-131">Select **Accept** tooaccept hello Microsoft Software License Terms for hello first time.</span></span> 

   ![接受 hello Microsoft 軟體授權條款](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/AcceptEULA.png)   
3. <span data-ttu-id="7b152-133">hello cmd 主控台隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="7b152-133">hello cmd console opens.</span></span> <span data-ttu-id="7b152-134">對於第一次的使用者，您需要 tooenter **3**，然後找出您的資料輸入和輸出的 hello 本機資料夾路徑。</span><span class="sxs-lookup"><span data-stu-id="7b152-134">For first-time users, you need tooenter **3**, and then locate hello local folder path for your data input and output.</span></span> <span data-ttu-id="7b152-135">如需其他選項，您可以使用 hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="7b152-135">For other options, you can use hello default values.</span></span> 

   ![Data Lake Tools for Visual Studio Code 本機執行 CMD](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-cmd.png)
4. <span data-ttu-id="7b152-137">選擇 Ctrl + Shift + P tooopen hello 命令選擇區中，輸入**ADL： 送出工作**，然後選取**本機**toosubmit hello 作業 tooyour 本機帳戶。</span><span class="sxs-lookup"><span data-stu-id="7b152-137">Select Ctrl+Shift+P tooopen hello command palette, enter **ADL: Submit Job**, and then select **Local** toosubmit hello job tooyour local account.</span></span>

   ![Data Lake Tools for Visual Studio Code 選取本機](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-select-local.png)
5. <span data-ttu-id="7b152-139">您送出 hello 作業之後，您可以檢視 hello 提交詳細資料。</span><span class="sxs-lookup"><span data-stu-id="7b152-139">After you submit hello job, you can view hello submission details.</span></span> <span data-ttu-id="7b152-140">tooview hello 提交詳細資料選取**jobUrl**在 hello**輸出**視窗。</span><span class="sxs-lookup"><span data-stu-id="7b152-140">tooview hello submission details select **jobUrl** in hello **Output** window.</span></span> <span data-ttu-id="7b152-141">您也可以檢視從 hello cmd 主控台 hello 作業提交狀態。</span><span class="sxs-lookup"><span data-stu-id="7b152-141">You can also view hello job submission status from hello cmd console.</span></span> <span data-ttu-id="7b152-142">輸入**7** hello cmd 主控台中如果您想 tooknow 更多的作業詳細資料。</span><span class="sxs-lookup"><span data-stu-id="7b152-142">Enter **7** in hello cmd console if you want tooknow more job details.</span></span>

   <span data-ttu-id="7b152-143">![Data Lake Tools for Visual Studio Code 本機執行輸出](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-result.png)
   ![Data Lake Tools for Visual Studio Code 本機執行 CMD 狀態](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-localrun-cmd-status.png)</span><span class="sxs-lookup"><span data-stu-id="7b152-143">![Data Lake Tools for Visual Studio Code local run output](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-result.png)
![Data Lake Tools for Visual Studio Code local run cmd status](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-localrun-cmd-status.png)</span></span> 


## <a name="start-a-local-debug-for-hello-u-sql-job"></a><span data-ttu-id="7b152-144">啟動本機偵錯 hello U-SQL 工作</span><span class="sxs-lookup"><span data-stu-id="7b152-144">Start a local debug for hello U-SQL job</span></span>  
<span data-ttu-id="7b152-145">Hello 第一次使用者，您會提示的 toodownload hello ADL： 如果尚未安裝的封裝下載 LocalRun 相依性。</span><span class="sxs-lookup"><span data-stu-id="7b152-145">For hello first-time user, you are prompted toodownload hello ADL: Download LocalRun Dependency packages if they are not already installed.</span></span>
  
1. <span data-ttu-id="7b152-146">選取 Ctrl + Shift + P tooopen hello 命令調色盤，然後輸入**ADL： 啟動本機執行服務**。</span><span class="sxs-lookup"><span data-stu-id="7b152-146">Select Ctrl+Shift+P tooopen hello command palette, and then enter **ADL: Start Local Run Service**.</span></span> <span data-ttu-id="7b152-147">hello cmd 主控台隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="7b152-147">hello cmd console opens.</span></span> <span data-ttu-id="7b152-148">請確定該 hello **DataRoot**設定。</span><span class="sxs-lookup"><span data-stu-id="7b152-148">Make sure that hello **DataRoot** is set.</span></span>
3. <span data-ttu-id="7b152-149">在您的 C# 程式碼後置中設定中斷點。</span><span class="sxs-lookup"><span data-stu-id="7b152-149">Set a breakpoint in your C# code-behind.</span></span>
4. <span data-ttu-id="7b152-150">在 [hello 指令碼編輯器] 中，選取 Ctrl + Shift + P tooopen hello 命令主控台，然後輸入**本機偵錯**toostart 本機偵錯服務。</span><span class="sxs-lookup"><span data-stu-id="7b152-150">Back in hello script editor, select Ctrl+Shift+P tooopen hello command console, and then enter **Local Debug** toostart your local debug service.</span></span>

![Data Lake Tools for Visual Studio Code 本機偵錯結果](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-debug-result.png)


## <a name="next-steps"></a><span data-ttu-id="7b152-152">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7b152-152">Next steps</span></span>
- <span data-ttu-id="7b152-153">若要了解如何使用 Azure Data Lake Tools for Visual Studio Code，請參閱[使用 Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md)。</span><span class="sxs-lookup"><span data-stu-id="7b152-153">For using Azure Data Lake Tools for Visual Studio Code, see [Use Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span></span>
- <span data-ttu-id="7b152-154">如需 Data Lake Analytics 的入門資訊，請參閱[教學課程︰開始使用 Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="7b152-154">For getting started information on Data Lake Analytics, see [Tutorial: Get started with Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).</span></span>
- <span data-ttu-id="7b152-155">如需 Data Lake Tools for Visual Studio 的相關資訊，請參閱[教學課程：使用 Data Lake Tools for Visual Studio 開發 U-SQL 指令碼](data-lake-analytics-data-lake-tools-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="7b152-155">For information about Data Lake Tools for Visual Studio, see [Tutorial: Develop U-SQL scripts by using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
- <span data-ttu-id="7b152-156">Hello 上開發的組件的資訊，請參閱[開發 U-SQL Azure Data Lake Analytics 工作的組件](data-lake-analytics-u-sql-develop-assemblies.md)。</span><span class="sxs-lookup"><span data-stu-id="7b152-156">For hello information on developing assemblies, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md).</span></span>
