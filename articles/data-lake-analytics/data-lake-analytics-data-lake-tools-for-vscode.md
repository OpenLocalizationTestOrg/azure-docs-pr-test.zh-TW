---
title: "Azure Data Lake Tools：使用 Azure Data Lake Tools for Visual Studio Code | Microsoft Docs"
description: "了解如何 toouse Azure 資料湖 Tools for Visual Studio Code toocreate 測試，以及執行 U-SQL 指令碼。 "
Keywords: "VScode，Azure 資料湖工具，本機執行，本機偵錯，本機偵錯預覽的儲存體檔案上, 傳 toostorage 路徑"
services: data-lake-analytics
documentationcenter: 
author: jejiang
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: dc9b21d8-c5f4-4f77-bcbc-eff458f48de2
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/14/2017
ms.author: jejiang
ms.openlocfilehash: 77771c5d5dae3bfce4ad2df240ea6c6ef848f288
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-data-lake-tools-for-visual-studio-code"></a><span data-ttu-id="19f54-104">使用 Azure Data Lake Tools for Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="19f54-104">Use Azure Data Lake Tools for Visual Studio Code</span></span>

<span data-ttu-id="19f54-105">了解如何 toouse Azure 資料湖 Tools for Visual Studio 程式碼 (VS Code) toocreate 測試，以及執行 U-SQL 指令碼。</span><span class="sxs-lookup"><span data-stu-id="19f54-105">Learn how toouse Azure Data Lake Tools for Visual Studio Code (VS Code) toocreate, test, and run U-SQL scripts.</span></span> <span data-ttu-id="19f54-106">下列視訊 hello 也涵蓋 hello 資訊：</span><span class="sxs-lookup"><span data-stu-id="19f54-106">hello information is also covered in hello following video:</span></span>

<a href="https://www.youtube.com/watch?v=J_gWuyFnaGA&feature=youtu.be"><img src="./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-video.png"></a>

## <a name="prerequisites"></a><span data-ttu-id="19f54-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="19f54-107">Prerequisites</span></span>

<span data-ttu-id="19f54-108">資料湖工具可以安裝支援的 VS Code hello 平台上。</span><span class="sxs-lookup"><span data-stu-id="19f54-108">Data Lake Tools can be installed on hello platforms supported by VS Code.</span></span> <span data-ttu-id="19f54-109">hello 支援平台包括 Windows、 Linux 及 MacOS。</span><span class="sxs-lookup"><span data-stu-id="19f54-109">hello supported platforms include Windows, Linux, and MacOS.</span></span> <span data-ttu-id="19f54-110">hello 不同平台具有下列必要條件 hello:</span><span class="sxs-lookup"><span data-stu-id="19f54-110">hello different platforms have hello following prerequisites:</span></span>

- <span data-ttu-id="19f54-111">Windows</span><span class="sxs-lookup"><span data-stu-id="19f54-111">Windows</span></span>

    - <span data-ttu-id="19f54-112">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx)。</span><span class="sxs-lookup"><span data-stu-id="19f54-112">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span></span>
    - <span data-ttu-id="19f54-113">[Java SE Runtime Environment version 8 update 77 或更新版本](https://java.com/download/manual.jsp)。</span><span class="sxs-lookup"><span data-stu-id="19f54-113">[Java SE Runtime Environment version 8 update 77 or later](https://java.com/download/manual.jsp).</span></span> <span data-ttu-id="19f54-114">新增 hello java.exe toohello 系統環境變數的路徑。</span><span class="sxs-lookup"><span data-stu-id="19f54-114">Add hello java.exe path toohello system environment variable path.</span></span> <span data-ttu-id="19f54-115">組態指示，請參閱[如何設定或變更 hello Path 系統變數？]( https://www.java.com/download/help/path.xml)。</span><span class="sxs-lookup"><span data-stu-id="19f54-115">For configuration instructions, see [How do I set or change hello Path system variable?]( https://www.java.com/download/help/path.xml).</span></span> <span data-ttu-id="19f54-116">hello 路徑是類似 tooC:\Program Files\Java\jdk1.8.0_77\jre\bin。</span><span class="sxs-lookup"><span data-stu-id="19f54-116">hello path is similar tooC:\Program Files\Java\jdk1.8.0_77\jre\bin.</span></span>
    - <span data-ttu-id="19f54-117">[.NET Core SDK 1.0.3 或 .NET Core 1.1 執行階段](https://www.microsoft.com/net/download)。</span><span class="sxs-lookup"><span data-stu-id="19f54-117">[.NET Core SDK 1.0.3 or .NET Core 1.1 runtime](https://www.microsoft.com/net/download).</span></span>
    
- <span data-ttu-id="19f54-118">Linux (我們建議使用 Ubuntu 14.04 LTS)</span><span class="sxs-lookup"><span data-stu-id="19f54-118">Linux (We recommend Ubuntu 14.04 LTS)</span></span>

    - <span data-ttu-id="19f54-119">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx)。</span><span class="sxs-lookup"><span data-stu-id="19f54-119">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span></span> <span data-ttu-id="19f54-120">tooinstall hello 程式碼中，輸入下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="19f54-120">tooinstall hello code, enter hello following command:</span></span>

              sudo dpkg -i code_<version_number>_amd64.deb

    - <span data-ttu-id="19f54-121">[Mono 4.2.x](http://www.mono-project.com/docs/getting-started/install/linux/)。</span><span class="sxs-lookup"><span data-stu-id="19f54-121">[Mono 4.2.x](http://www.mono-project.com/docs/getting-started/install/linux/).</span></span> 

        - <span data-ttu-id="19f54-122">tooupdate hello deb 套件來源中，輸入下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="19f54-122">tooupdate hello deb package source, enter hello following commands:</span></span>

                sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
                echo "deb http://download.mono-project.com/repo/debian wheezy/snapshots 4.2.4.4/main" | sudo tee /etc/apt/sources.list.d/mono-xamarin.list
                sudo apt-get update

        - <span data-ttu-id="19f54-123">tooinstall Mono，輸入下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="19f54-123">tooinstall Mono, enter hello following command:</span></span>

                sudo apt-get install mono-complete

            > [!NOTE] 
            > <span data-ttu-id="19f54-124">不支援 Mono 4.6。</span><span class="sxs-lookup"><span data-stu-id="19f54-124">Mono 4.6 is not supported.</span></span> <span data-ttu-id="19f54-125">在安裝 4.2.x 之前，請先徹底解除安裝 4.6 版。</span><span class="sxs-lookup"><span data-stu-id="19f54-125">Uninstall version 4.6 entirely before you install 4.2.x.</span></span>  

        - <span data-ttu-id="19f54-126">[Java SE Runtime Environment version 8 update 77 或更新版本](https://java.com/download/manual.jsp)。</span><span class="sxs-lookup"><span data-stu-id="19f54-126">[Java SE Runtime Environment version 8 update 77 or later](https://java.com/download/manual.jsp).</span></span> <span data-ttu-id="19f54-127">如需安裝指示，請參閱 hello [for Java 的 Linux 64 位元安裝指示]( https://java.com/en/download/help/linux_x64_install.xml)頁面。</span><span class="sxs-lookup"><span data-stu-id="19f54-127">For instructions on installation, see hello [Linux 64-bit installation instructions for Java]( https://java.com/en/download/help/linux_x64_install.xml) page.</span></span>
        - <span data-ttu-id="19f54-128">[.NET Core SDK 1.0.3 或 .NET Core 1.1 執行階段](https://www.microsoft.com/net/download)。</span><span class="sxs-lookup"><span data-stu-id="19f54-128">[.NET Core SDK 1.0.3 or .NET Core 1.1 runtime](https://www.microsoft.com/net/download).</span></span>
- <span data-ttu-id="19f54-129">MacOS</span><span class="sxs-lookup"><span data-stu-id="19f54-129">MacOS</span></span>

    - <span data-ttu-id="19f54-130">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx)。</span><span class="sxs-lookup"><span data-stu-id="19f54-130">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span></span>
    - <span data-ttu-id="19f54-131">[Mono 4.2.4](http://download.mono-project.com/archive/4.2.4/macos-10-x86/)。</span><span class="sxs-lookup"><span data-stu-id="19f54-131">[Mono 4.2.4](http://download.mono-project.com/archive/4.2.4/macos-10-x86/).</span></span> 
    - <span data-ttu-id="19f54-132">[Java SE Runtime Environment version 8 update 77 或更新版本](https://java.com/download/manual.jsp)。</span><span class="sxs-lookup"><span data-stu-id="19f54-132">[Java SE Runtime Environment version 8 update 77 or later](https://java.com/download/manual.jsp).</span></span> <span data-ttu-id="19f54-133">如需安裝指示，請參閱 hello [for Java 的 Linux 64 位元安裝指示](https://java.com/en/download/help/mac_install.xml)頁面。</span><span class="sxs-lookup"><span data-stu-id="19f54-133">For instructions on installation, see hello [Linux 64-bit installation instructions for Java](https://java.com/en/download/help/mac_install.xml) page.</span></span>
    - <span data-ttu-id="19f54-134">[.NET Core SDK 1.0.3 或 .NET Core 1.1 執行階段](https://www.microsoft.com/net/download)。</span><span class="sxs-lookup"><span data-stu-id="19f54-134">[.NET Core SDK 1.0.3 or .NET Core 1.1 runtime](https://www.microsoft.com/net/download).</span></span>

## <a name="install-data-lake-tools"></a><span data-ttu-id="19f54-135">安裝 Data Lake Tools</span><span class="sxs-lookup"><span data-stu-id="19f54-135">Install Data Lake Tools</span></span>

<span data-ttu-id="19f54-136">安裝 hello 必要條件之後，您可以安裝 Data Lake Tools VS 程式碼。</span><span class="sxs-lookup"><span data-stu-id="19f54-136">After you install hello prerequisites, you can install Data Lake Tools for VS Code.</span></span>

<span data-ttu-id="19f54-137">**tooinstall 資料湖工具**</span><span class="sxs-lookup"><span data-stu-id="19f54-137">**tooinstall Data Lake Tools**</span></span>

1. <span data-ttu-id="19f54-138">開啟 Visual Studio Code。</span><span class="sxs-lookup"><span data-stu-id="19f54-138">Open Visual Studio Code.</span></span>
2. <span data-ttu-id="19f54-139">選擇 Ctrl + P，，然後輸入 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="19f54-139">Select Ctrl+P, and then enter hello following command:</span></span>
```
ext install usql-vscode-ext
```
<span data-ttu-id="19f54-140">您可以看到一份 Visual Studio 程式碼擴充功能清單。</span><span class="sxs-lookup"><span data-stu-id="19f54-140">You can see a list of Visual Studio code extensions.</span></span> <span data-ttu-id="19f54-141">其中一個是 **Azure Data Lake Tools**。</span><span class="sxs-lookup"><span data-stu-id="19f54-141">One of them is **Azure Data Lake Tools**.</span></span>

3. <span data-ttu-id="19f54-142">選取**安裝**下一步太**Azure Data Lake Tools**。</span><span class="sxs-lookup"><span data-stu-id="19f54-142">Select **Install** next too**Azure Data Lake Tools**.</span></span> <span data-ttu-id="19f54-143">幾秒之後，hello**安裝**太按鈕變更**重新載入**。</span><span class="sxs-lookup"><span data-stu-id="19f54-143">After a few seconds, hello **Install** button changes too**Reload**.</span></span>
4. <span data-ttu-id="19f54-144">選取**重新載入**tooactivate hello 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="19f54-144">Select **Reload** tooactivate hello extension.</span></span>
5. <span data-ttu-id="19f54-145">選取**確定**tooconfirm。</span><span class="sxs-lookup"><span data-stu-id="19f54-145">Select **OK** tooconfirm.</span></span> <span data-ttu-id="19f54-146">您可以在 hello 看到 Azure Data Lake Tools**延伸**窗格。</span><span class="sxs-lookup"><span data-stu-id="19f54-146">You can see Azure Data Lake Tools in hello **Extensions** pane.</span></span>
    <span data-ttu-id="19f54-147">![Data Lake Tools for Visual Studio Code 擴充功能窗格](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extensions.png)</span><span class="sxs-lookup"><span data-stu-id="19f54-147">![Data Lake Tools for Visual Studio Code Extensions pane](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extensions.png)</span></span>

## <a name="activate-azure-data-lake-tools"></a><span data-ttu-id="19f54-148">啟動 Azure Data Lake Tools</span><span class="sxs-lookup"><span data-stu-id="19f54-148">Activate Azure Data Lake Tools</span></span>
<span data-ttu-id="19f54-149">建立新的.usql 檔案或開啟現有.usql tooactivate hello 的副檔名。</span><span class="sxs-lookup"><span data-stu-id="19f54-149">Create a new .usql file or open an existing .usql file tooactivate hello extension.</span></span> 

## <a name="connect-tooazure"></a><span data-ttu-id="19f54-150">連接 tooAzure</span><span class="sxs-lookup"><span data-stu-id="19f54-150">Connect tooAzure</span></span>

<span data-ttu-id="19f54-151">您可以編譯並執行 Data Lake Analytics U-SQL 指令碼之前，您必須連接 tooyour Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="19f54-151">Before you can compile and run U-SQL scripts in Data Lake Analytics, you must connect tooyour Azure account.</span></span>

<span data-ttu-id="19f54-152">**tooconnect tooAzure**</span><span class="sxs-lookup"><span data-stu-id="19f54-152">**tooconnect tooAzure**</span></span>

1.  <span data-ttu-id="19f54-153">選擇 Ctrl + Shift + P tooopen hello 命令選擇區。</span><span class="sxs-lookup"><span data-stu-id="19f54-153">Select Ctrl+Shift+P tooopen hello command palette.</span></span> 
2.  <span data-ttu-id="19f54-154">輸入 **ADL: Login**。</span><span class="sxs-lookup"><span data-stu-id="19f54-154">Enter **ADL: Login**.</span></span> <span data-ttu-id="19f54-155">hello 登入資訊會出現在 hello**輸出**窗格。</span><span class="sxs-lookup"><span data-stu-id="19f54-155">hello login information appears in hello **Output** pane.</span></span>

    <span data-ttu-id="19f54-156">![Data Lake Tools for Visual Studio Code 命令選擇區](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login.png)
    ![Data Lake Tools for Visual Studio Code 裝置登入資訊](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-login-info.png)</span><span class="sxs-lookup"><span data-stu-id="19f54-156">![Data Lake Tools for Visual Studio Code command palette](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login.png)
![Data Lake Tools for Visual Studio Code device login information](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-login-info.png)</span></span>
3. <span data-ttu-id="19f54-157">選擇 Ctrl + 按一下 hello 登入 URL: https://aka.ms/devicelogin tooopen hello 登入網頁。</span><span class="sxs-lookup"><span data-stu-id="19f54-157">Select Ctrl+click on hello login URL: https://aka.ms/devicelogin tooopen hello login webpage.</span></span> <span data-ttu-id="19f54-158">輸入 hello 代碼**G567LX42V**到 hello 文字，然後再選取**繼續**。</span><span class="sxs-lookup"><span data-stu-id="19f54-158">Enter hello code **G567LX42V** into hello text box, and then select **Continue**.</span></span>

   ![Data Lake Tools for Visual Studio Code 登入貼上代碼](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login-paste-code.png )   
4.  <span data-ttu-id="19f54-160">請依照中的 hello 指示 toosign hello 網頁。</span><span class="sxs-lookup"><span data-stu-id="19f54-160">Follow hello instructions toosign in from hello webpage.</span></span> <span data-ttu-id="19f54-161">您連線，您的 Azure 帳戶名稱會出現在 hello 狀態列中的 hello hello 左下角**VS Code**視窗。</span><span class="sxs-lookup"><span data-stu-id="19f54-161">When you're connected, your Azure account name appears on hello status bar in hello lower-left corner of hello **VS Code** window.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="19f54-162">如果您的帳戶已啟用雙因素驗證，建議您使用電話驗證而非使用 PIN 碼。</span><span class="sxs-lookup"><span data-stu-id="19f54-162">If your account has two factors enabled, we recommend that you use phone authentication rather than using a PIN.</span></span>

<span data-ttu-id="19f54-163">out，toosign 輸入 hello 命令**ADL： 登出**。</span><span class="sxs-lookup"><span data-stu-id="19f54-163">toosign out, enter hello command **ADL: Logout**.</span></span>

## <a name="list-your-data-lake-analytics-accounts"></a><span data-ttu-id="19f54-164">列出 Data Lake Analytics 帳戶</span><span class="sxs-lookup"><span data-stu-id="19f54-164">List your Data Lake Analytics accounts</span></span>

<span data-ttu-id="19f54-165">tootest hello 連線，get Data Lake Analytics 帳戶的清單。</span><span class="sxs-lookup"><span data-stu-id="19f54-165">tootest hello connection, get a list of your Data Lake Analytics accounts.</span></span>

<span data-ttu-id="19f54-166">**您的 Azure 訂用帳戶底下 toolist hello Data Lake Analytics 帳戶**</span><span class="sxs-lookup"><span data-stu-id="19f54-166">**toolist hello Data Lake Analytics accounts under your Azure subscription**</span></span>

1. <span data-ttu-id="19f54-167">選擇 Ctrl + Shift + P tooopen hello 命令選擇區。</span><span class="sxs-lookup"><span data-stu-id="19f54-167">Select Ctrl+Shift+P tooopen hello command palette.</span></span>
2. <span data-ttu-id="19f54-168">輸入 **ADL: List Accounts**。</span><span class="sxs-lookup"><span data-stu-id="19f54-168">Enter **ADL: List Accounts**.</span></span> <span data-ttu-id="19f54-169">hello 帳戶會出現在 hello**輸出**窗格。</span><span class="sxs-lookup"><span data-stu-id="19f54-169">hello accounts appear in hello **Output** pane.</span></span>

## <a name="open-hello-sample-script"></a><span data-ttu-id="19f54-170">開啟 hello 範例指令碼</span><span class="sxs-lookup"><span data-stu-id="19f54-170">Open hello sample script</span></span>
<span data-ttu-id="19f54-171">開啟 hello 命令選擇區 (Ctrl + Shift + P)，並輸入**ADL： 開啟範例指令碼**。</span><span class="sxs-lookup"><span data-stu-id="19f54-171">Open hello command palette (Ctrl+Shift+P) and enter **ADL: Open Sample Script**.</span></span> <span data-ttu-id="19f54-172">這會開啟此範例的另一個執行個體。</span><span class="sxs-lookup"><span data-stu-id="19f54-172">This opens another instance of this sample.</span></span> <span data-ttu-id="19f54-173">您也可以在此執行個體上編輯、設定及提交指令碼。</span><span class="sxs-lookup"><span data-stu-id="19f54-173">You can also edit, configure, and submit script on this instance.</span></span>

## <a name="work-with-u-sql"></a><span data-ttu-id="19f54-174">使用 U-SQL</span><span class="sxs-lookup"><span data-stu-id="19f54-174">Work with U-SQL</span></span>

<span data-ttu-id="19f54-175">您需要使用 U-SQL 開啟 U-SQL 檔案或資料夾 toowork。</span><span class="sxs-lookup"><span data-stu-id="19f54-175">You need open either a U-SQL file or a folder toowork with U-SQL.</span></span>

<span data-ttu-id="19f54-176">**tooopen U-SQL 專案的資料夾**</span><span class="sxs-lookup"><span data-stu-id="19f54-176">**tooopen a folder for your U-SQL project**</span></span>

1. <span data-ttu-id="19f54-177">從 Visual Studio 程式碼中，選取 [hello**檔案**] 功能表，然後選取**開啟資料夾**。</span><span class="sxs-lookup"><span data-stu-id="19f54-177">From Visual Studio Code, select hello **File** menu, and then select **Open Folder**.</span></span>
2. <span data-ttu-id="19f54-178">指定資料夾，然後選取 [選取資料夾]。</span><span class="sxs-lookup"><span data-stu-id="19f54-178">Specify a folder, and then select **Select Folder**.</span></span>
3. <span data-ttu-id="19f54-179">選取 hello**檔案** 功能表，然後選取**新增**。</span><span class="sxs-lookup"><span data-stu-id="19f54-179">Select hello **File** menu, and then select **New**.</span></span> <span data-ttu-id="19f54-180">未命名 1 檔案會加入 toohello 專案。</span><span class="sxs-lookup"><span data-stu-id="19f54-180">An Untitled-1 file is added toohello project.</span></span>
4. <span data-ttu-id="19f54-181">輸入下列程式碼到 hello 未命名 1 檔案 hello:</span><span class="sxs-lookup"><span data-stu-id="19f54-181">Enter hello following code into hello Untitled-1 file:</span></span>

        @departments  = 
            SELECT * FROM 
                (VALUES
                    (31,    "Sales"),
                    (33,    "Engineering"), 
                    (34,    "Clerical"),
                    (35,    "Marketing")
                ) AS 
                      D( DepID, DepName );
         
        OUTPUT @departments
            TO “/Output/departments.csv”

    <span data-ttu-id="19f54-182">hello 指令碼會建立 departments.csv 檔案以包含在 hello /output 資料夾中特定資料。</span><span class="sxs-lookup"><span data-stu-id="19f54-182">hello script creates a departments.csv file with some data included in hello /output folder.</span></span>

5. <span data-ttu-id="19f54-183">將 hello 檔案儲存為**myUSQL.usql** hello 中開啟資料夾。</span><span class="sxs-lookup"><span data-stu-id="19f54-183">Save hello file as **myUSQL.usql** in hello opened folder.</span></span> <span data-ttu-id="19f54-184">Adltools_settings.json 組態檔也會加入 toohello 專案。</span><span class="sxs-lookup"><span data-stu-id="19f54-184">A adltools_settings.json configuration file is also added toohello project.</span></span>
4. <span data-ttu-id="19f54-185">開啟並設定 adltools_settings.json 以 hello 下列屬性：</span><span class="sxs-lookup"><span data-stu-id="19f54-185">Open and configure adltools_settings.json with hello following properties:</span></span>

    - <span data-ttu-id="19f54-186">帳戶：在您的 Azure 訂用帳戶下的 Data Lake Analytics 帳戶。</span><span class="sxs-lookup"><span data-stu-id="19f54-186">Account:  A Data Lake Analytics account under your Azure subscription.</span></span>
    - <span data-ttu-id="19f54-187">資料庫：您帳戶底下的資料庫。</span><span class="sxs-lookup"><span data-stu-id="19f54-187">Database: A database under your account.</span></span> <span data-ttu-id="19f54-188">hello 預設值是**主要**。</span><span class="sxs-lookup"><span data-stu-id="19f54-188">hello default is **master**.</span></span>
    - <span data-ttu-id="19f54-189">結構描述：您資料庫底下的結構描述。</span><span class="sxs-lookup"><span data-stu-id="19f54-189">Schema: A schema under your database.</span></span> <span data-ttu-id="19f54-190">hello 預設值是**dbo**。</span><span class="sxs-lookup"><span data-stu-id="19f54-190">hello default is **dbo**.</span></span>
    - <span data-ttu-id="19f54-191">選擇性設定︰</span><span class="sxs-lookup"><span data-stu-id="19f54-191">Optional settings:</span></span>
        - <span data-ttu-id="19f54-192">優先順序： hello 優先順序範圍是從 1 too1000 1 為 hello 最高優先權。</span><span class="sxs-lookup"><span data-stu-id="19f54-192">Priority: hello priority range is from 1 too1000 with 1 as hello highest priority.</span></span> <span data-ttu-id="19f54-193">hello 預設值是**1000年**。</span><span class="sxs-lookup"><span data-stu-id="19f54-193">hello default value is **1000**.</span></span>
        - <span data-ttu-id="19f54-194">平行處理原則： hello 平行處理原則的範圍是從 1 too150。</span><span class="sxs-lookup"><span data-stu-id="19f54-194">Parallelism: hello parallelism range is from 1 too150.</span></span> <span data-ttu-id="19f54-195">hello 預設值為 hello Azure Data Lake Analytics 帳戶中允許的最大平行處理。</span><span class="sxs-lookup"><span data-stu-id="19f54-195">hello default value is hello maximum parallelism allowed in your Azure Data Lake Analytics account.</span></span> 
        
        > [!NOTE] 
        > <span data-ttu-id="19f54-196">如果 hello 設定無效，則會使用 hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="19f54-196">If hello settings are invalid, hello default values are used.</span></span>

    ![Data Lake Tools for Visual Studio Code 組態檔](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-configuration-file.png)

    <span data-ttu-id="19f54-198">Data Lake Analytics 帳戶是計算需要 toocompile，並執行 U-SQL 工作。</span><span class="sxs-lookup"><span data-stu-id="19f54-198">A compute Data Lake Analytics account is needed toocompile and run U-SQL jobs.</span></span> <span data-ttu-id="19f54-199">您可以編譯及執行 U SQL 作業之前，您必須設定 hello 電腦帳戶。</span><span class="sxs-lookup"><span data-stu-id="19f54-199">You must configure hello computer account before you can compile and run U-SQL jobs.</span></span>
    
<span data-ttu-id="19f54-200">儲存 hello 組態之後，hello 帳戶、 資料庫和結構描述資訊出現在 hello 狀態列 hello 左下角的 hello 對應.usql 檔案。</span><span class="sxs-lookup"><span data-stu-id="19f54-200">After hello configuration is saved, hello account, database, and schema information appears on hello status bar at hello bottom-left corner of hello corresponding .usql file.</span></span> 
 
 
<span data-ttu-id="19f54-201">比較的 tooopening 檔案，當您開啟的資料夾，您可以：</span><span class="sxs-lookup"><span data-stu-id="19f54-201">Compared tooopening a file, when you open a folder you can:</span></span>

- <span data-ttu-id="19f54-202">使用程式碼後置檔案。</span><span class="sxs-lookup"><span data-stu-id="19f54-202">Use a code-behind file.</span></span> <span data-ttu-id="19f54-203">在 hello 單一檔案模式中，不支援程式碼後置。</span><span class="sxs-lookup"><span data-stu-id="19f54-203">In hello single-file mode, code-behind is not supported.</span></span>
- <span data-ttu-id="19f54-204">使用組態檔。</span><span class="sxs-lookup"><span data-stu-id="19f54-204">Use a configuration file.</span></span> <span data-ttu-id="19f54-205">當您開啟資料夾時，hello 工作資料夾中的 hello 指令碼會共用單一設定檔。</span><span class="sxs-lookup"><span data-stu-id="19f54-205">When you open a folder, hello scripts in hello working folder share a single configuration file.</span></span>


<span data-ttu-id="19f54-206">hello U-SQL 指令碼會編譯從遠端透過 hello 資料湖分析服務。</span><span class="sxs-lookup"><span data-stu-id="19f54-206">hello U-SQL script compiles remotely through hello Data Lake Analytics service.</span></span> <span data-ttu-id="19f54-207">當您發出 hello**編譯**命令 hello U-SQL 指令碼會傳送 tooyour Data Lake Analytics 帳戶。</span><span class="sxs-lookup"><span data-stu-id="19f54-207">When you issue hello **compile** command, hello U-SQL script is sent tooyour Data Lake Analytics account.</span></span> <span data-ttu-id="19f54-208">更新版本中，Visual Studio 程式碼會收到 hello 編譯結果。</span><span class="sxs-lookup"><span data-stu-id="19f54-208">Later, Visual Studio Code receives hello compilation result.</span></span> <span data-ttu-id="19f54-209">由於 toohello 遠端編譯，Visual Studio 程式碼需要您列出 hello tooconnect tooyour hello 組態檔中的 Data Lake Analytics 帳戶的資訊。</span><span class="sxs-lookup"><span data-stu-id="19f54-209">Due toohello remote compilation, Visual Studio Code requires that you list hello information tooconnect tooyour Data Lake Analytics account in hello configuration file.</span></span>

<span data-ttu-id="19f54-210">**toocompile U-SQL 指令碼**</span><span class="sxs-lookup"><span data-stu-id="19f54-210">**toocompile a U-SQL script**</span></span>

1. <span data-ttu-id="19f54-211">選擇 Ctrl + Shift + P tooopen hello 命令選擇區。</span><span class="sxs-lookup"><span data-stu-id="19f54-211">Select Ctrl+Shift+P tooopen hello command palette.</span></span> 
2. <span data-ttu-id="19f54-212">輸入 **ADL: Compile Script**。</span><span class="sxs-lookup"><span data-stu-id="19f54-212">Enter **ADL: Compile Script**.</span></span> <span data-ttu-id="19f54-213">hello 編譯結果會出現在 hello**輸出**視窗。</span><span class="sxs-lookup"><span data-stu-id="19f54-213">hello compile results appear in hello **Output** window.</span></span> <span data-ttu-id="19f54-214">您可以也在指令碼檔案，以滑鼠右鍵按一下，然後選取**ADL： 編譯指令碼**toocompile U SQL 作業。</span><span class="sxs-lookup"><span data-stu-id="19f54-214">You can also right-click a script file, and then select **ADL: Compile Script** toocompile a U-SQL job.</span></span> <span data-ttu-id="19f54-215">hello 編譯結果會出現在 hello**輸出**窗格。</span><span class="sxs-lookup"><span data-stu-id="19f54-215">hello compilation result appears in hello **Output** pane.</span></span>
 

<span data-ttu-id="19f54-216">**toosubmit U-SQL 指令碼**</span><span class="sxs-lookup"><span data-stu-id="19f54-216">**toosubmit a U-SQL script**</span></span>

1. <span data-ttu-id="19f54-217">選擇 Ctrl + Shift + P tooopen hello 命令選擇區。</span><span class="sxs-lookup"><span data-stu-id="19f54-217">Select Ctrl+Shift+P tooopen hello command palette.</span></span> 
2. <span data-ttu-id="19f54-218">輸入 **ADL: Submit Job**。</span><span class="sxs-lookup"><span data-stu-id="19f54-218">Enter **ADL: Submit Job**.</span></span>  <span data-ttu-id="19f54-219">您也可以在指令碼檔案上按一下滑鼠右鍵，然後選取 [ADL: Submit Job]。</span><span class="sxs-lookup"><span data-stu-id="19f54-219">You can also right-click a script file, and then select **ADL: Submit Job**.</span></span> 

<span data-ttu-id="19f54-220">Hello 送出記錄檔送出 U-SQL 工作後，會出現在 hello**輸出**VS 程式碼中的視窗。</span><span class="sxs-lookup"><span data-stu-id="19f54-220">After you submit a U-SQL job, hello submission logs appear in hello **Output** window in VS Code.</span></span> <span data-ttu-id="19f54-221">如果 hello 提交成功，hello 工作 URL 也會出現。</span><span class="sxs-lookup"><span data-stu-id="19f54-221">If hello submission is successful, hello job URL appears as well.</span></span> <span data-ttu-id="19f54-222">您可以開啟 hello 工作 URL 中的 web 瀏覽器 tootrack hello 即時作業狀態。</span><span class="sxs-lookup"><span data-stu-id="19f54-222">You can open hello job URL in a web browser tootrack hello real-time job status.</span></span>

<span data-ttu-id="19f54-223">設定 tooenable hello 輸出 hello 工作詳細資料， **jobInformationOutputPath**在 hello **vs 程式碼 hello u sql_settings.json**檔案。</span><span class="sxs-lookup"><span data-stu-id="19f54-223">tooenable hello output of hello job details, set **jobInformationOutputPath** in hello **vs code for hello u-sql_settings.json** file.</span></span>
 
## <a name="use-a-code-behind-file"></a><span data-ttu-id="19f54-224">使用程式碼後置檔案</span><span class="sxs-lookup"><span data-stu-id="19f54-224">Use a code-behind file</span></span>

<span data-ttu-id="19f54-225">程式碼後置檔案是與單一 U-SQL 指令碼關聯的 C# 檔案。</span><span class="sxs-lookup"><span data-stu-id="19f54-225">A code-behind file is a C# file associated with a single U-SQL script.</span></span> <span data-ttu-id="19f54-226">您可以定義指令碼專用 tooUDO、 UDA、 UDT 和 UDF hello 程式碼後置檔案中。</span><span class="sxs-lookup"><span data-stu-id="19f54-226">You can define a script dedicated tooUDO, UDA, UDT, and UDF in hello code-behind file.</span></span> <span data-ttu-id="19f54-227">hello UDO、 UDA、 UDT 和 UDF 可直接在 hello 指令碼而不先註冊 hello 組件。</span><span class="sxs-lookup"><span data-stu-id="19f54-227">hello UDO, UDA, UDT, and UDF can be used directly in hello script without registering hello assembly first.</span></span> <span data-ttu-id="19f54-228">hello 程式碼後置檔案放在 hello 相同為其對等互連的 U-SQL 指令碼檔案的資料夾。</span><span class="sxs-lookup"><span data-stu-id="19f54-228">hello code-behind file is put in hello same folder as its peering U-SQL script file.</span></span> <span data-ttu-id="19f54-229">如果 hello 指令碼為 xxx.usql，hello 程式碼後置會稱為 xxx.usql.cs。</span><span class="sxs-lookup"><span data-stu-id="19f54-229">If hello script is named xxx.usql, hello code-behind is named as xxx.usql.cs.</span></span> <span data-ttu-id="19f54-230">如果您以手動方式刪除 hello 程式碼後置檔案，其相關聯的 U-SQL 指令碼的 hello 程式碼後置功能已停用。</span><span class="sxs-lookup"><span data-stu-id="19f54-230">If you manually delete hello code-behind file, hello code-behind feature is disabled for its associated U-SQL script.</span></span> <span data-ttu-id="19f54-231">如需撰寫 U-SQL 指令碼之客戶程式碼的詳細資訊，請參閱[在 U-SQL 中撰寫並使用自訂程式碼：使用者定義函式]( https://blogs.msdn.microsoft.com/visualstudio/2015/10/28/writing-and-using-custom-code-in-u-sql-user-defined-functions/) (英文)。</span><span class="sxs-lookup"><span data-stu-id="19f54-231">For more information about writing customer code for U-SQL script, see [Writing and Using Custom Code in U-SQL: User-Defined Functions]( https://blogs.msdn.microsoft.com/visualstudio/2015/10/28/writing-and-using-custom-code-in-u-sql-user-defined-functions/).</span></span>

<span data-ttu-id="19f54-232">toosupport 程式碼後置，您必須開啟工作資料夾。</span><span class="sxs-lookup"><span data-stu-id="19f54-232">toosupport code-behind, you must open a working folder.</span></span> 

<span data-ttu-id="19f54-233">**toogenerate 程式碼後置檔案**</span><span class="sxs-lookup"><span data-stu-id="19f54-233">**toogenerate a code-behind file**</span></span>

1. <span data-ttu-id="19f54-234">開啟來源檔案。</span><span class="sxs-lookup"><span data-stu-id="19f54-234">Open a source file.</span></span> 
2. <span data-ttu-id="19f54-235">選擇 Ctrl + Shift + P tooopen hello 命令選擇區。</span><span class="sxs-lookup"><span data-stu-id="19f54-235">Select Ctrl+Shift+P tooopen hello command palette.</span></span>
3. <span data-ttu-id="19f54-236">輸入 **ADL: Generate Code Behind**。</span><span class="sxs-lookup"><span data-stu-id="19f54-236">Enter **ADL: Generate Code Behind**.</span></span> <span data-ttu-id="19f54-237">程式碼後置檔案中建立 hello 相同資料夾。</span><span class="sxs-lookup"><span data-stu-id="19f54-237">A code-behind file is created in hello same folder.</span></span> 

<span data-ttu-id="19f54-238">您也可以在指令碼檔案上按一下滑鼠右鍵，然後選取 [ADL: Generate Code Behind]。</span><span class="sxs-lookup"><span data-stu-id="19f54-238">You can also right-click a script file, and then select **ADL: Generate Code Behind**.</span></span> 

<span data-ttu-id="19f54-239">toocompile 並提交 U-SQL 指令碼的程式碼後置檔案是 hello 相同與 hello 獨立 U-SQL 指令碼檔案。</span><span class="sxs-lookup"><span data-stu-id="19f54-239">toocompile and submit a U-SQL script with a code-behind file is hello same as with hello standalone U-SQL script file.</span></span>

<span data-ttu-id="19f54-240">hello 下列兩個螢幕擷取畫面顯示程式碼後置檔案和其相關聯的 U-SQL 指令碼檔案：</span><span class="sxs-lookup"><span data-stu-id="19f54-240">hello following two screenshots show a code-behind file and its associated U-SQL script file:</span></span>
 
![Data Lake Tools for Visual Studio Code 程式碼後置](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-code-behind.png)

![Data Lake Tools for Visual Studio Code 程式碼後置指令碼檔案](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-code-behind-call.png) 

## <a name="use-assemblies"></a><span data-ttu-id="19f54-243">使用組件</span><span class="sxs-lookup"><span data-stu-id="19f54-243">Use assemblies</span></span>

<span data-ttu-id="19f54-244">如需有關開發組件的資訊，請參閱[針對 Azure Data Lake Analytics 作業開發 U-SQL 組件](data-lake-analytics-u-sql-develop-assemblies.md)。</span><span class="sxs-lookup"><span data-stu-id="19f54-244">For information on developing assemblies, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md).</span></span>

<span data-ttu-id="19f54-245">您可以使用 Data Lake Tools tooregister 自訂程式碼組件 hello Data Lake Analytics 類別目錄中。</span><span class="sxs-lookup"><span data-stu-id="19f54-245">You can use Data Lake Tools tooregister custom code assemblies in hello Data Lake Analytics catalog.</span></span>

<span data-ttu-id="19f54-246">**tooregister 組件**</span><span class="sxs-lookup"><span data-stu-id="19f54-246">**tooregister an assembly**</span></span>

<span data-ttu-id="19f54-247">您可以註冊 hello 組件透過 hello **ADL： 註冊組件**或**ADL： 註冊組件，透過組態**命令。</span><span class="sxs-lookup"><span data-stu-id="19f54-247">You can register hello assembly through hello **ADL: Register Assembly** or **ADL: Register Assembly through Configuration** commands.</span></span>

<span data-ttu-id="19f54-248">**透過 hello ADL tooregister： 註冊組件命令**</span><span class="sxs-lookup"><span data-stu-id="19f54-248">**tooregister through hello ADL: Register Assembly command**</span></span>
1.  <span data-ttu-id="19f54-249">選擇 Ctrl + Shift + P tooopen hello 命令選擇區。</span><span class="sxs-lookup"><span data-stu-id="19f54-249">Select Ctrl+Shift+P tooopen hello command palette.</span></span>
2.  <span data-ttu-id="19f54-250">輸入 **ADL: Register Assembly**。</span><span class="sxs-lookup"><span data-stu-id="19f54-250">Enter **ADL: Register Assembly**.</span></span> 
3.  <span data-ttu-id="19f54-251">指定 hello 本機組件路徑。</span><span class="sxs-lookup"><span data-stu-id="19f54-251">Specify hello local assembly path.</span></span> 
4.  <span data-ttu-id="19f54-252">選取 Data Lake Analytics 帳戶。</span><span class="sxs-lookup"><span data-stu-id="19f54-252">Select a Data Lake Analytics account.</span></span>
5.  <span data-ttu-id="19f54-253">選取資料庫。</span><span class="sxs-lookup"><span data-stu-id="19f54-253">Select a database.</span></span>

<span data-ttu-id="19f54-254">結果： hello 入口網站會在瀏覽器中開啟，並顯示 hello 組件註冊程序。</span><span class="sxs-lookup"><span data-stu-id="19f54-254">Results: hello portal is opened in a browser and displays hello assembly registration process.</span></span>  

<span data-ttu-id="19f54-255">另一個便利的方式 tootrigger hello **ADL： 註冊組件**命令是在檔案總管中的 tooright 按一下 hello.dll 檔案。</span><span class="sxs-lookup"><span data-stu-id="19f54-255">Another convenient way tootrigger hello **ADL: Register Assembly** command is tooright-click hello .dll file in File Explorer.</span></span> 

<span data-ttu-id="19f54-256">**tooregister 雖然 hello ADL： 註冊組件，透過組態命令**</span><span class="sxs-lookup"><span data-stu-id="19f54-256">**tooregister though hello ADL: Register Assembly through Configuration command**</span></span>
1.  <span data-ttu-id="19f54-257">選擇 Ctrl + Shift + P tooopen hello 命令選擇區。</span><span class="sxs-lookup"><span data-stu-id="19f54-257">Select Ctrl+Shift+P tooopen hello command palette.</span></span>
2.  <span data-ttu-id="19f54-258">輸入 **ADL: Register Assembly through Configuration**。</span><span class="sxs-lookup"><span data-stu-id="19f54-258">Enter **ADL: Register Assembly through Configuration**.</span></span> 
3.  <span data-ttu-id="19f54-259">指定 hello 本機組件路徑。</span><span class="sxs-lookup"><span data-stu-id="19f54-259">Specify hello local assembly path.</span></span> 
4.  <span data-ttu-id="19f54-260">會顯示 hello JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="19f54-260">hello JSON file is displayed.</span></span> <span data-ttu-id="19f54-261">檢閱並視需要編輯 hello 組件相依性及資源參數。</span><span class="sxs-lookup"><span data-stu-id="19f54-261">Review and edit hello assembly dependencies and resource parameters, if needed.</span></span> <span data-ttu-id="19f54-262">指示會顯示在 hello**輸出**視窗。</span><span class="sxs-lookup"><span data-stu-id="19f54-262">Instructions are displayed in hello **Output** window.</span></span> <span data-ttu-id="19f54-263">tooproceed toohello 組件註冊，(Ctrl + S) hello JSON 檔案儲存。</span><span class="sxs-lookup"><span data-stu-id="19f54-263">tooproceed toohello assembly registration, save (Ctrl+S) hello JSON file.</span></span>

![Data Lake Tools for Visual Studio Code 程式碼後置](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-register-assembly-advance.png)
>[!NOTE]
>- <span data-ttu-id="19f54-265">組件相依性： Azure Data Lake Tools autodetects hello DLL 是否有任何相依性。</span><span class="sxs-lookup"><span data-stu-id="19f54-265">Assembly dependencies: Azure Data Lake Tools autodetects whether hello DLL has any dependencies.</span></span> <span data-ttu-id="19f54-266">hello 相依性會顯示 hello JSON 檔案中之後就會偵測衝突。</span><span class="sxs-lookup"><span data-stu-id="19f54-266">hello dependencies are displayed in hello JSON file after they are detected.</span></span> 
>- <span data-ttu-id="19f54-267">資源： 您可以將上傳您 DLL 的資源 （例如.txt、.png 和.csv） hello 組件註冊的一部分。</span><span class="sxs-lookup"><span data-stu-id="19f54-267">Resources: You can upload your DLL resources (for example, .txt, .png, and .csv) as part of hello assembly registration.</span></span> 

<span data-ttu-id="19f54-268">另一個方式 tootrigger hello **ADL： 註冊組件，透過組態**命令是在檔案總管中的 tooright 按一下 hello.dll 檔案。</span><span class="sxs-lookup"><span data-stu-id="19f54-268">Another way tootrigger hello **ADL: Register Assembly through Configuration** command is tooright-click hello .dll file in File Explorer.</span></span> 

<span data-ttu-id="19f54-269">hello 遵循 U SQL 程式碼示範如何 toocall 組件。</span><span class="sxs-lookup"><span data-stu-id="19f54-269">hello following U-SQL code demonstrates how toocall an assembly.</span></span> <span data-ttu-id="19f54-270">在 hello 範例 hello 組件名稱是*測試*。</span><span class="sxs-lookup"><span data-stu-id="19f54-270">In hello sample, hello assembly name is *test*.</span></span>

```
REFERENCE ASSEMBLY [test];

@a = 
    EXTRACT 
        Iid int,
    Starts DateTime,
    Region string,
    Query string,
    DwellTime int,
    Results string,
    ClickedUrls string 
    FROM @"Sample/SearchLog.txt" 
    USING Extractors.Tsv();

@d =
    SELECT DISTINCT Region 
    FROM @a;

@d1 = 
    PROCESS @d
    PRODUCE 
        Region string,
    Mkt string
    USING new USQLApplication_codebehind.MyProcessor();

OUTPUT @d1 
    too@"Sample/SearchLogtest.txt" 
    USING Outputters.Tsv();
```


## <a name="access-hello-data-lake-analytics-catalog"></a><span data-ttu-id="19f54-271">存取 hello Data Lake Analytics 類別目錄</span><span class="sxs-lookup"><span data-stu-id="19f54-271">Access hello Data Lake Analytics catalog</span></span>

<span data-ttu-id="19f54-272">連接 tooAzure 之後，您可以使用下列步驟 tooaccess hello U-SQL 目錄 hello。</span><span class="sxs-lookup"><span data-stu-id="19f54-272">After you have connected tooAzure, you can use hello following steps tooaccess hello U-SQL catalog.</span></span>

<span data-ttu-id="19f54-273">**tooaccess hello Azure Data Lake Analytics 中繼資料**</span><span class="sxs-lookup"><span data-stu-id="19f54-273">**tooaccess hello Azure Data Lake Analytics metadata**</span></span>

1.  <span data-ttu-id="19f54-274">選取 Ctrl+Shift+P，然後輸入 **ADL: List Tables**。</span><span class="sxs-lookup"><span data-stu-id="19f54-274">Select Ctrl+Shift+P, and then enter **ADL: List Tables**.</span></span>
2.  <span data-ttu-id="19f54-275">選取其中一個 hello Data Lake Analytics 帳戶。</span><span class="sxs-lookup"><span data-stu-id="19f54-275">Select one of hello Data Lake Analytics accounts.</span></span>
3.  <span data-ttu-id="19f54-276">選取其中一個 hello 資料湖分析資料庫。</span><span class="sxs-lookup"><span data-stu-id="19f54-276">Select one of hello Data Lake Analytics databases.</span></span>
4.  <span data-ttu-id="19f54-277">選取其中一個 hello 結構描述。</span><span class="sxs-lookup"><span data-stu-id="19f54-277">Select one of hello schemas.</span></span> <span data-ttu-id="19f54-278">您可以看到 hello 的資料表清單。</span><span class="sxs-lookup"><span data-stu-id="19f54-278">You can see hello list of tables.</span></span>

## <a name="view-data-lake-analytics-jobs"></a><span data-ttu-id="19f54-279">檢視 Data Lake Analytics 作業</span><span class="sxs-lookup"><span data-stu-id="19f54-279">View Data Lake Analytics jobs</span></span>

<span data-ttu-id="19f54-280">**tooview Data Lake Analytics 工作**</span><span class="sxs-lookup"><span data-stu-id="19f54-280">**tooview Data Lake Analytics jobs**</span></span>
1.  <span data-ttu-id="19f54-281">開啟 hello 命令選擇區 (Ctrl + Shift + P)，然後選取**ADL： 顯示工作**。</span><span class="sxs-lookup"><span data-stu-id="19f54-281">Open hello command palette (Ctrl+Shift+P) and select **ADL: Show Job**.</span></span> 
2.  <span data-ttu-id="19f54-282">選取 Data Lake Analytics 帳戶或本機帳戶。</span><span class="sxs-lookup"><span data-stu-id="19f54-282">Select a Data Lake Analytics or local account.</span></span> 
3.  <span data-ttu-id="19f54-283">等候 hello 帳戶 tooappear hello 工作清單。</span><span class="sxs-lookup"><span data-stu-id="19f54-283">Wait for hello jobs list for hello account tooappear.</span></span>
4.  <span data-ttu-id="19f54-284">從工作清單中選取的作業，資料湖工具在 hello Azure 入口網站中開啟 hello 工作詳細資料，並顯示 VS 程式碼中的 hello JobInfo 檔案。</span><span class="sxs-lookup"><span data-stu-id="19f54-284">Select a job from job list, Data Lake Tools opens hello job details in hello Azure portal and displays hello JobInfo file in VS Code.</span></span>

![Data Lake Tools for Visual Studio Code IntelliSense 物件類型](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-show-job.png)

## <a name="azure-data-lake-storage-integration"></a><span data-ttu-id="19f54-286">Azure Data Lake Storage 整合</span><span class="sxs-lookup"><span data-stu-id="19f54-286">Azure Data Lake Storage integration</span></span>

<span data-ttu-id="19f54-287">您可以使用 Azure Data Lake Storage 相關命令來進行下列作業：</span><span class="sxs-lookup"><span data-stu-id="19f54-287">You can use Azure Data Lake Storage-related commands to:</span></span>
 - <span data-ttu-id="19f54-288">瀏覽 hello Azure 資料湖存放區資源。</span><span class="sxs-lookup"><span data-stu-id="19f54-288">Browse through hello Azure Data Lake Storage resources.</span></span> 
 - <span data-ttu-id="19f54-289">預覽 hello Azure 資料湖存放區檔案。</span><span class="sxs-lookup"><span data-stu-id="19f54-289">Preview hello Azure Data Lake Storage file.</span></span>  
 - <span data-ttu-id="19f54-290">上傳 hello 檔案與程式碼中直接 tooAzure 資料湖存放區。</span><span class="sxs-lookup"><span data-stu-id="19f54-290">Upload hello file directly tooAzure Data Lake Storage in VS Code.</span></span> 

### <a name="list-hello-storage-path"></a><span data-ttu-id="19f54-291">清單 hello 儲存體路徑</span><span class="sxs-lookup"><span data-stu-id="19f54-291">List hello storage path</span></span> 
<span data-ttu-id="19f54-292">您可以列出透過 hello 命令選擇區或以滑鼠右鍵按一下 hello 儲存路徑。</span><span class="sxs-lookup"><span data-stu-id="19f54-292">You can list hello storage path through hello command palette or through right-click.</span></span>

<span data-ttu-id="19f54-293">**透過 hello 命令選擇區 toolist hello 儲存路徑**</span><span class="sxs-lookup"><span data-stu-id="19f54-293">**toolist hello storage path through hello command palette**</span></span>

1.  <span data-ttu-id="19f54-294">開啟 hello 命令選擇區 (Ctrl + Shift + P)，並輸入**ADL： 清單存放路徑**。</span><span class="sxs-lookup"><span data-stu-id="19f54-294">Open hello command palette (Ctrl+Shift+P) and enter **ADL: List Storage Path**.</span></span>

    ![Data Lake Tools for Visual Studio Code 列出儲存體路徑](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-storage.png)

2.  <span data-ttu-id="19f54-296">選取您慣用的方法，以列出 hello 儲存路徑。</span><span class="sxs-lookup"><span data-stu-id="19f54-296">Select your preferred way for listing hello storage path.</span></span> <span data-ttu-id="19f54-297">本段使用 [Enter a path] \(輸入路徑\) 作為範例。</span><span class="sxs-lookup"><span data-stu-id="19f54-297">This passage uses **Enter a path** as an example.</span></span>

    ![Visual Studio Code 其中一種方式 toolist hello 儲存路徑的資料湖工具](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account-selectoneway.png)

    > [!NOTE]
    >- <span data-ttu-id="19f54-299">VS Code 的每個 Data Lake Analytics 帳戶中保留 hello 上次造訪的路徑。</span><span class="sxs-lookup"><span data-stu-id="19f54-299">VS Code keeps hello last-visited path in every Data Lake Analytics account.</span></span> <span data-ttu-id="19f54-300">例如：/tt/ss。</span><span class="sxs-lookup"><span data-stu-id="19f54-300">For example: /tt/ss.</span></span>
    >- <span data-ttu-id="19f54-301">瀏覽器從根路徑： hello 清單根路徑，從選取的資料湖分析帳戶或本機路徑。</span><span class="sxs-lookup"><span data-stu-id="19f54-301">Browser from root path: hello list root path from your selected Data Lake Analytics account or a local path.</span></span>
    >- <span data-ttu-id="19f54-302">輸入路徑：從所選 Data Lake Analytics 帳戶或本機路徑列出指定的路徑。</span><span class="sxs-lookup"><span data-stu-id="19f54-302">Enter a path: List a specified path from your selected Data Lake Analytics account or a local path.</span></span>
    
3. <span data-ttu-id="19f54-303">選取從 hello 本機路徑或 Data Lake Analytics 帳戶的帳戶。</span><span class="sxs-lookup"><span data-stu-id="19f54-303">Select an account from hello local path or a Data Lake Analytics account.</span></span>

    ![Data Lake Tools for Visual Studio Code 選取更多](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

4. <span data-ttu-id="19f54-305">選取**詳細**toolist 詳細資料湖分析帳戶，然後選取 Data Lake Analytics 帳戶。</span><span class="sxs-lookup"><span data-stu-id="19f54-305">Select **more** toolist more Data Lake Analytics accounts, and then select a Data Lake Analytics account.</span></span>

    ![Data Lake Tools for Visual Studio Code 選取一個帳戶](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-select-adla-account.png)

5.  <span data-ttu-id="19f54-307">輸入 Azure 儲存體路徑。</span><span class="sxs-lookup"><span data-stu-id="19f54-307">Enter an Azure storage path.</span></span> <span data-ttu-id="19f54-308">例如，/output。</span><span class="sxs-lookup"><span data-stu-id="19f54-308">For example, /output.</span></span>

    ![Data Lake Tools for Visual Studio Code 輸入儲存體路徑](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-path.png)

6.  <span data-ttu-id="19f54-310">結果： hello 命令選擇區列出根據項目 hello 路徑資訊。</span><span class="sxs-lookup"><span data-stu-id="19f54-310">Results: hello command palette lists hello path information based on your entries.</span></span>

    ![Data Lake Tools for Visual Studio Code 列出儲存體路徑結果](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-path.png)

<span data-ttu-id="19f54-312">Toolist hello 相對路徑是透過 hello 較方便的方式上按一下滑鼠右鍵內容功能表。</span><span class="sxs-lookup"><span data-stu-id="19f54-312">A more convenient way toolist hello relative path is through hello right-click context menu.</span></span>

<span data-ttu-id="19f54-313">**透過 toolist hello 儲存路徑上按一下滑鼠右鍵**</span><span class="sxs-lookup"><span data-stu-id="19f54-313">**toolist hello storage path through right-click**</span></span>

1.  <span data-ttu-id="19f54-314">以滑鼠右鍵按一下 hello 路徑字串 tooselect**清單存放路徑**。</span><span class="sxs-lookup"><span data-stu-id="19f54-314">Right-click hello path string tooselect **List Storage Path**.</span></span>

       ![Data Lake Tools for Visual Studio Code 右鍵快顯功能表](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-right-click-path.png)

2. <span data-ttu-id="19f54-316">hello 選相對路徑會出現在 hello 命令選擇區。</span><span class="sxs-lookup"><span data-stu-id="19f54-316">hello selected relative path appears in hello command palette.</span></span>

   ![Data Lake Tools for Visual Studio Code 選取的相對路徑](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-relative-path.png)

3.  <span data-ttu-id="19f54-318">選取從 hello 本機路徑或 Data Lake Analytics 帳戶的帳戶。</span><span class="sxs-lookup"><span data-stu-id="19f54-318">Select an account from hello local path or a Data Lake Analytics account.</span></span>

       ![Data Lake Tools for Visual Studio Code 選取一個帳戶](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

4.  <span data-ttu-id="19f54-320">結果： hello 命令選擇區列出 hello 資料夾和檔案 hello 目前路徑。</span><span class="sxs-lookup"><span data-stu-id="19f54-320">Results: hello command palette lists hello folders and files for hello current path.</span></span>

       ![Visual Studio 程式碼清單 hello 目前路徑中的資料湖工具](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-current.png)

### <a name="preview-hello-storage-file"></a><span data-ttu-id="19f54-322">預覽 hello 儲存體檔案</span><span class="sxs-lookup"><span data-stu-id="19f54-322">Preview hello storage file</span></span>
<span data-ttu-id="19f54-323">您可以預覽 hello 透過 hello 命令選擇區或以滑鼠右鍵按一下儲存體檔案。</span><span class="sxs-lookup"><span data-stu-id="19f54-323">You can preview hello storage file through hello command palette or through right-click.</span></span>

<span data-ttu-id="19f54-324">**透過 hello 命令選擇區 toopreview hello 儲存體檔案**</span><span class="sxs-lookup"><span data-stu-id="19f54-324">**toopreview hello storage file through hello command palette**</span></span>

1.  <span data-ttu-id="19f54-325">開啟 hello 命令選擇區 (Ctrl + Shift + P)，並輸入**ADL： 預覽儲存體檔案**。</span><span class="sxs-lookup"><span data-stu-id="19f54-325">Open hello command palette (Ctrl+Shift+P) and enter **ADL: Preview Storage File**.</span></span>

       ![Data Lake Tools for Visual Studio Code 預覽儲存體檔案](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-preview.png)

2.  <span data-ttu-id="19f54-327">選取從 hello 本機路徑或 Data Lake Analytics 帳戶的帳戶。</span><span class="sxs-lookup"><span data-stu-id="19f54-327">Select an account from hello local path or a Data Lake Analytics account.</span></span>

       ![Data Lake Tools for Visual Studio Code 列出帳戶](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

3.  <span data-ttu-id="19f54-329">選取**詳細**toolist 詳細資料湖分析帳戶，然後選取 Data Lake Analytics 帳戶。</span><span class="sxs-lookup"><span data-stu-id="19f54-329">Select **more** toolist more Data Lake Analytics accounts, and then select a Data Lake Analytics account.</span></span>

       ![Data Lake Tools for Visual Studio Code 選取一個帳戶](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-select-adla-account.png)

4.  <span data-ttu-id="19f54-331">輸入 Azure 儲存體路徑或檔案。</span><span class="sxs-lookup"><span data-stu-id="19f54-331">Enter an Azure storage path or file.</span></span> <span data-ttu-id="19f54-332">例如：/output/SearchLog.txt。</span><span class="sxs-lookup"><span data-stu-id="19f54-332">For example, /output/SearchLog.txt.</span></span>

       ![Data Lake Tools for Visual Studio Code 輸入儲存體路徑和檔案](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-preview-file.png)

5.  <span data-ttu-id="19f54-334">結果： hello 命令選擇區列出根據項目 hello 路徑資訊。</span><span class="sxs-lookup"><span data-stu-id="19f54-334">Results: hello command palette lists hello path information based on your entries.</span></span>

       ![Data Lake Tools for Visual Studio Code 預覽檔案結果](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-preview-results.png)

<span data-ttu-id="19f54-336">**透過 toolist hello 儲存路徑上按一下滑鼠右鍵**</span><span class="sxs-lookup"><span data-stu-id="19f54-336">**toolist hello storage path through right-click**</span></span>

1.  <span data-ttu-id="19f54-337">toopreview 檔案，以滑鼠右鍵按一下 hello 檔案路徑。</span><span class="sxs-lookup"><span data-stu-id="19f54-337">toopreview a file, right-click hello file path.</span></span>

   ![Data Lake Tools for Visual Studio Code 右鍵快顯功能表](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-right-click-preview.png) 

2.  <span data-ttu-id="19f54-339">選取從 hello 本機路徑或 Data Lake Analytics 帳戶的帳戶。</span><span class="sxs-lookup"><span data-stu-id="19f54-339">Select an account from hello local path or a Data Lake Analytics account.</span></span>

       ![Data Lake Tools for Visual Studio Code 選取一個帳戶](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

3.  <span data-ttu-id="19f54-341">結果： VS 程式碼會顯示 hello 檔案 hello 預覽結果。</span><span class="sxs-lookup"><span data-stu-id="19f54-341">Results: VS Code displays hello preview results of hello file.</span></span>

       ![Data Lake Tools for Visual Studio Code 預覽檔案結果](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-preview-results.png)

### <a name="upload-a-file"></a><span data-ttu-id="19f54-343">上傳檔案</span><span class="sxs-lookup"><span data-stu-id="19f54-343">Upload a file</span></span> 

<span data-ttu-id="19f54-344">您可以將檔案上傳輸入 hello 命令**ADL： 上傳檔案**或**ADL： 上傳的檔案，透過組態**。</span><span class="sxs-lookup"><span data-stu-id="19f54-344">You can upload files by entering hello commands **ADL: Upload File** or **ADL: Upload File through Configuration**.</span></span>

<span data-ttu-id="19f54-345">**tooupload 檔案雖然 hello ADL： 上傳檔案命令**</span><span class="sxs-lookup"><span data-stu-id="19f54-345">**tooupload files though hello ADL: Upload File command**</span></span>
1. <span data-ttu-id="19f54-346">選取 Ctrl + Shift + P tooopen hello 命令選擇區或 hello 指令碼編輯器 中，以滑鼠右鍵按一下，然後輸入**上傳檔案**。</span><span class="sxs-lookup"><span data-stu-id="19f54-346">Select Ctrl+Shift+P tooopen hello command palette or right-click hello script editor, and then enter **Upload File**.</span></span>
2.  <span data-ttu-id="19f54-347">tooupload hello 檔案中，輸入本機路徑。</span><span class="sxs-lookup"><span data-stu-id="19f54-347">tooupload hello file, enter a local path.</span></span>

    ![Data Lake Tools for Visual Studio Code 輸入本機路徑](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-input-local-path.png)

3. <span data-ttu-id="19f54-349">選取其中一種清單 hello 儲存路徑的 hello。</span><span class="sxs-lookup"><span data-stu-id="19f54-349">Select one of hello ways of listing hello storage path.</span></span> <span data-ttu-id="19f54-350">本段使用 [Enter a path] \(輸入路徑\) 作為範例。</span><span class="sxs-lookup"><span data-stu-id="19f54-350">This passage uses **Enter a path** as an example.</span></span>

    ![Data Lake Tools for Visual Studio Code 列出儲存體路徑](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account-selectoneway.png)
    >[!NOTE]
    >- <span data-ttu-id="19f54-352">VS Code 的每個 Data Lake Analytics 帳戶中保留 hello 上次造訪的路徑。</span><span class="sxs-lookup"><span data-stu-id="19f54-352">VS Code keeps hello last-visited path in every Data Lake Analytics account.</span></span> <span data-ttu-id="19f54-353">例如：/tt/ss。</span><span class="sxs-lookup"><span data-stu-id="19f54-353">For example: /tt/ss.</span></span>
    >- <span data-ttu-id="19f54-354">瀏覽器從根路徑： hello 清單根路徑，從選取的資料湖分析帳戶或本機路徑。</span><span class="sxs-lookup"><span data-stu-id="19f54-354">Browser from root path: hello list root path from your selected Data Lake Analytics account or a local path.</span></span>
    >- <span data-ttu-id="19f54-355">輸入路徑：從所選 Data Lake Analytics 帳戶或本機路徑列出指定的路徑。</span><span class="sxs-lookup"><span data-stu-id="19f54-355">Enter a path: List a specified path from your selected Data Lake Analytics account or a local path.</span></span>

4. <span data-ttu-id="19f54-356">選取從 hello 本機路徑或 Data Lake Analytics 帳戶的帳戶。</span><span class="sxs-lookup"><span data-stu-id="19f54-356">Select an account from hello local path or a Data Lake Analytics account.</span></span>

    ![Data Lake Tools for Visual Studio Code 在儲存體上按一下滑鼠右鍵](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

5. <span data-ttu-id="19f54-358">輸入 Azure 儲存體路徑。</span><span class="sxs-lookup"><span data-stu-id="19f54-358">Enter an Azure storage path.</span></span> <span data-ttu-id="19f54-359">例如：/output。</span><span class="sxs-lookup"><span data-stu-id="19f54-359">For example: /output.</span></span>

       ![Data Lake Tools for Visual Studio Code enter storage path](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-preview-file.png)

6. <span data-ttu-id="19f54-360">找出您的 Azure 儲存體路徑。</span><span class="sxs-lookup"><span data-stu-id="19f54-360">Find your Azure storage path.</span></span> <span data-ttu-id="19f54-361">選取 [Choose current folder] \(選擇目前的資料夾\)。</span><span class="sxs-lookup"><span data-stu-id="19f54-361">Select **Choose current folder**.</span></span>

    ![Data Lake Tools for Visual Studio Code 選取資料夾](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-choose-current-folder.png)

7.  <span data-ttu-id="19f54-363">結果： hello**輸出**視窗會顯示 hello 檔案上傳狀態。</span><span class="sxs-lookup"><span data-stu-id="19f54-363">Results: hello **Output** window displays hello file upload status.</span></span>

       ![Data Lake Tools for Visual Studio Code 上傳狀態](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-status.png)    

<span data-ttu-id="19f54-365">**tooupload 檔案雖然 hello ADL： 上傳的檔案，透過組態命令**</span><span class="sxs-lookup"><span data-stu-id="19f54-365">**tooupload files though hello ADL: Upload File through Configuration command**</span></span>
1.  <span data-ttu-id="19f54-366">選取 Ctrl + Shift + P tooopen hello 命令選擇區或 hello 指令碼編輯器 中，以滑鼠右鍵按一下，然後輸入**上傳的檔案，透過組態**。</span><span class="sxs-lookup"><span data-stu-id="19f54-366">Select Ctrl+Shift+P tooopen hello command palette or right-click hello script editor, and then enter **Upload File through Configuration**.</span></span>
2.  <span data-ttu-id="19f54-367">VS Code 會顯示一個 JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="19f54-367">VS Code displays a JSON file.</span></span> <span data-ttu-id="19f54-368">您可以輸入檔案路徑，然後在 hello 的多個檔案上傳相同的時間。</span><span class="sxs-lookup"><span data-stu-id="19f54-368">You can enter file paths and upload multiple files at hello same time.</span></span> <span data-ttu-id="19f54-369">指示會顯示在 hello**輸出**視窗。</span><span class="sxs-lookup"><span data-stu-id="19f54-369">Instructions are displayed in hello **Output** window.</span></span> <span data-ttu-id="19f54-370">tooproceed tooupload hello 檔案、 儲存 (Ctrl + S) hello JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="19f54-370">tooproceed tooupload hello file, save (Ctrl+S) hello JSON file.</span></span>

       ![Data Lake Tools for Visual Studio Code 檔案路徑](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-file.png)

3.  <span data-ttu-id="19f54-372">結果： hello**輸出**視窗會顯示 hello 檔案上傳狀態。</span><span class="sxs-lookup"><span data-stu-id="19f54-372">Results: hello **Output** window displays hello file upload status.</span></span>

       ![Data Lake Tools for Visual Studio Code 上傳狀態](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-status.png)     

<span data-ttu-id="19f54-374">另一個方式 tooupload 檔案 toostorage 是透過 hello 上按一下滑鼠右鍵功能表 hello 檔案的完整路徑或 hello 指令碼編輯器中的 hello 檔案的相對路徑。</span><span class="sxs-lookup"><span data-stu-id="19f54-374">Another way tooupload a file toostorage is through hello right-click menu on hello file's full path or hello file's relative path in hello script editor.</span></span> <span data-ttu-id="19f54-375">輸入 hello 本機檔案路徑，然後再選取 hello 帳戶。</span><span class="sxs-lookup"><span data-stu-id="19f54-375">Enter hello local file path, and then select hello account.</span></span> <span data-ttu-id="19f54-376">hello**輸出**視窗會顯示 hello 上傳狀態。</span><span class="sxs-lookup"><span data-stu-id="19f54-376">hello **Output** window displays hello upload status.</span></span> 

### <a name="open-azure-storage-explorer"></a><span data-ttu-id="19f54-377">開啟 Azure 儲存體總管</span><span class="sxs-lookup"><span data-stu-id="19f54-377">Open Azure Storage Explorer</span></span>
<span data-ttu-id="19f54-378">您可以開啟**Azure 儲存體總管**輸入 hello 命令**ADL： 開啟 Web Azure 儲存體總管**或從 hello 以滑鼠右鍵按一下內容功能表中選取它。</span><span class="sxs-lookup"><span data-stu-id="19f54-378">You can open **Azure Storage Explorer** by entering hello command **ADL: Open Web Azure Storage Explorer** or by selecting it from hello right-click context menu.</span></span>

<span data-ttu-id="19f54-379">**tooopen Azure 儲存體總管**</span><span class="sxs-lookup"><span data-stu-id="19f54-379">**tooopen Azure Storage Explorer**</span></span>

1. <span data-ttu-id="19f54-380">選擇 Ctrl + Shift + P tooopen hello 命令選擇區。</span><span class="sxs-lookup"><span data-stu-id="19f54-380">Select Ctrl+Shift+P tooopen hello command palette.</span></span>
2. <span data-ttu-id="19f54-381">輸入**開啟 Web Azure 儲存體總管**或相對路徑或 hello 在 hello 指令碼編輯器中，完整的路徑上按一下滑鼠右鍵，然後選取**開啟 Web Azure 儲存體總管**。</span><span class="sxs-lookup"><span data-stu-id="19f54-381">Enter **Open Web Azure Storage Explorer** or right-click on a relative path or hello full path in hello script editor, and then select **Open Web Azure Storage Explorer**.</span></span>
3. <span data-ttu-id="19f54-382">選取 Data Lake Analytics 帳戶。</span><span class="sxs-lookup"><span data-stu-id="19f54-382">Select a Data Lake Analytics account.</span></span>

<span data-ttu-id="19f54-383">資料湖工具會在 hello Azure 入口網站中開啟 hello Azure 儲存體路徑。</span><span class="sxs-lookup"><span data-stu-id="19f54-383">Data Lake Tools opens hello Azure storage path in hello Azure portal.</span></span> <span data-ttu-id="19f54-384">您可以找到從 hello web hello 路徑和預覽 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="19f54-384">You can find hello path and preview hello file from hello web.</span></span>

### <a name="local-run-and-local-debug-for-windows-users"></a><span data-ttu-id="19f54-385">Windows 使用者的本機執行和本機偵錯</span><span class="sxs-lookup"><span data-stu-id="19f54-385">Local run and local debug for Windows users</span></span>
<span data-ttu-id="19f54-386">執行的 U-SQL 本機測試您的本機資料和已發行的 tooData 湖分析您的程式碼之前驗證指令碼在本機。</span><span class="sxs-lookup"><span data-stu-id="19f54-386">U-SQL local run tests your local data and validates your script locally, before your code is published tooData Lake Analytics.</span></span> <span data-ttu-id="19f54-387">hello 本機偵錯功能可讓您 toocomplete hello 下列工作，您的程式碼之前提交 tooData 湖分析：</span><span class="sxs-lookup"><span data-stu-id="19f54-387">hello local debug feature enables you toocomplete hello following tasks before your code is submitted tooData Lake Analytics:</span></span> 
- <span data-ttu-id="19f54-388">偵錯您的 C# 程式碼後置。</span><span class="sxs-lookup"><span data-stu-id="19f54-388">Debug your C# code-behind.</span></span> 
- <span data-ttu-id="19f54-389">逐步執行 hello 程式碼。</span><span class="sxs-lookup"><span data-stu-id="19f54-389">Step through hello code.</span></span> 
- <span data-ttu-id="19f54-390">在本機驗證您的指令碼。</span><span class="sxs-lookup"><span data-stu-id="19f54-390">Validate your script locally.</span></span>

<span data-ttu-id="19f54-391">如需本機執行和本機偵錯的指示，請參閱[使用 Visual Studio Code 來進行 U-SQL 本機執行和本機偵錯](data-lake-tools-for-vscode-local-run-and-debug.md)。</span><span class="sxs-lookup"><span data-stu-id="19f54-391">For instructions on local run and local debug, see [U-SQL local run and local debug with Visual Studio Code](data-lake-tools-for-vscode-local-run-and-debug.md).</span></span>

## <a name="additional-features"></a><span data-ttu-id="19f54-392">其他功能</span><span class="sxs-lookup"><span data-stu-id="19f54-392">Additional features</span></span>

<span data-ttu-id="19f54-393">VS Code 的資料湖工具支援下列功能的 hello:</span><span class="sxs-lookup"><span data-stu-id="19f54-393">Data Lake Tools for VS Code supports hello following features:</span></span>

-   <span data-ttu-id="19f54-394">IntelliSense 自動完成：關鍵字、方法和變數等項目周圍的快顯視窗會出現建議。</span><span class="sxs-lookup"><span data-stu-id="19f54-394">IntelliSense auto-complete: Suggestions appear in pop-up windows around items, such as keywords, methods, and variables.</span></span> <span data-ttu-id="19f54-395">不同的圖示代表不同類型的 hello 物件：</span><span class="sxs-lookup"><span data-stu-id="19f54-395">Different icons represent different types of hello objects:</span></span>

    - <span data-ttu-id="19f54-396">Scala 資料類型</span><span class="sxs-lookup"><span data-stu-id="19f54-396">Scala data type</span></span>
    - <span data-ttu-id="19f54-397">複雜資料類型</span><span class="sxs-lookup"><span data-stu-id="19f54-397">Complex data type</span></span>
    - <span data-ttu-id="19f54-398">內建 UDT</span><span class="sxs-lookup"><span data-stu-id="19f54-398">Built-in UDTs</span></span>
    - <span data-ttu-id="19f54-399">.NET 集合和類別</span><span class="sxs-lookup"><span data-stu-id="19f54-399">.NET collection and classes</span></span>
    - <span data-ttu-id="19f54-400">C# 運算式</span><span class="sxs-lookup"><span data-stu-id="19f54-400">C# expressions</span></span>
    - <span data-ttu-id="19f54-401">內建 C# UDF、UDO 和 UDAAG</span><span class="sxs-lookup"><span data-stu-id="19f54-401">Built-in C# UDFs, UDOs, and UDAAGs</span></span> 
    - <span data-ttu-id="19f54-402">U-SQL 函式</span><span class="sxs-lookup"><span data-stu-id="19f54-402">U-SQL functions</span></span>
    - <span data-ttu-id="19f54-403">U-SQL 時間範圍函式</span><span class="sxs-lookup"><span data-stu-id="19f54-403">U-SQL windowing function</span></span>
 
    ![Data Lake Tools for Visual Studio Code IntelliSense 物件類型](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-complete-objects.png)
 
-   <span data-ttu-id="19f54-405">IntelliSense 自動完成 Data Lake Analytics 中繼資料： 資料湖工具下載 hello Data Lake Analytics 中繼資料資訊在本機。</span><span class="sxs-lookup"><span data-stu-id="19f54-405">IntelliSense auto-complete on Data Lake Analytics metadata: Data Lake Tools downloads hello Data Lake Analytics metadata information locally.</span></span> <span data-ttu-id="19f54-406">hello IntelliSense 功能會自動填入物件，包括 hello 資料庫、 結構描述、 資料表、 檢視、 資料表值函數、 程序和 C# 組件，從 hello Data Lake Analytics 中繼資料。</span><span class="sxs-lookup"><span data-stu-id="19f54-406">hello IntelliSense feature automatically populates objects, including hello database, schema, table, view, table-valued function, procedures, and C# assemblies, from hello Data Lake Analytics metadata.</span></span>
 
    ![Data Lake Tools for Visual Studio Code IntelliSense 中繼資料](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-complete-metastore.png)

-   <span data-ttu-id="19f54-408">IntelliSense 錯誤標記： Data Lake Tools 加上底線 hello 編輯 U SQL 和 C# 的錯誤。</span><span class="sxs-lookup"><span data-stu-id="19f54-408">IntelliSense error marker: Data Lake Tools underlines hello editing errors for U-SQL and C#.</span></span> 
-   <span data-ttu-id="19f54-409">語法醒目提示： Data Lake Tools 會使用不同的色彩 toodifferentiate 項目，例如變數、 關鍵字、 資料類型和函數。</span><span class="sxs-lookup"><span data-stu-id="19f54-409">Syntax highlights: Data Lake Tools uses different colors toodifferentiate items, such as variables, keywords, data type, and functions.</span></span> 

    ![Data Lake Tools for Visual Studio Code 語法醒目顯示](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-syntax-highlights.png)

## <a name="next-steps"></a><span data-ttu-id="19f54-411">後續步驟</span><span class="sxs-lookup"><span data-stu-id="19f54-411">Next steps</span></span>

- <span data-ttu-id="19f54-412">如需了解如何使用 Visual Studio Code 來進行 U-SQL 本機執行和本機偵錯，請參閱[使用 Visual Studio Code 來進行 U-SQL 本機執行和本機偵錯](data-lake-tools-for-vscode-local-run-and-debug.md)。</span><span class="sxs-lookup"><span data-stu-id="19f54-412">For U-SQL local run and local debug with Visual Studio Code, see [U-SQL local run and local debug with Visual Studio Code](data-lake-tools-for-vscode-local-run-and-debug.md).</span></span>
- <span data-ttu-id="19f54-413">如需 Data Lake Analytics 的入門資訊，請參閱[教學課程︰開始使用 Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="19f54-413">For getting-started information on Data Lake Analytics, see [Tutorial: Get started with Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).</span></span>
- <span data-ttu-id="19f54-414">如需 Data Lake Tools for Visual Studio 的相關資訊，請參閱[教學課程：使用 Data Lake Tools for Visual Studio 開發 U-SQL 指令碼](data-lake-analytics-data-lake-tools-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="19f54-414">For information about Data Lake Tools for Visual Studio, see [Tutorial: Develop U-SQL scripts by using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
- <span data-ttu-id="19f54-415">如需有關開發組件的資訊，請參閱[針對 Azure Data Lake Analytics 作業開發 U-SQL 組件](data-lake-analytics-u-sql-develop-assemblies.md)。</span><span class="sxs-lookup"><span data-stu-id="19f54-415">For information on developing assemblies, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md).</span></span>



