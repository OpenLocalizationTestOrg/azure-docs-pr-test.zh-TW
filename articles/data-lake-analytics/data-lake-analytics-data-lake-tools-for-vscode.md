---
title: "Azure Data Lake Tools：使用 Azure Data Lake Tools for Visual Studio Code | Microsoft Docs"
description: "了解如何使用 Azure Data Lake Tools for Visual Studio Code 來建立、測試和執行 U-SQL 指令碼。 "
Keywords: "VScode,Azure Data Lake Tools,本機執行,本機偵錯,預覽儲存體檔案,上傳至儲存體路徑"
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
ms.openlocfilehash: 833d14af47454a01fa3c97ffa854d688dd35871f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-data-lake-tools-for-visual-studio-code"></a><span data-ttu-id="ee2c9-104">使用 Azure Data Lake Tools for Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="ee2c9-104">Use Azure Data Lake Tools for Visual Studio Code</span></span>

<span data-ttu-id="ee2c9-105">了解如何使用 Azure Data Lake Tools for Visual Studio Code (VS Code) 來建立、測試和執行 U-SQL 指令碼。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-105">Learn how to use Azure Data Lake Tools for Visual Studio Code (VS Code) to create, test, and run U-SQL scripts.</span></span> <span data-ttu-id="ee2c9-106">下列影片中也涵蓋此資訊︰</span><span class="sxs-lookup"><span data-stu-id="ee2c9-106">The information is also covered in the following video:</span></span>

<a href="https://www.youtube.com/watch?v=J_gWuyFnaGA&feature=youtu.be"><img src="./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-video.png"></a>

## <a name="prerequisites"></a><span data-ttu-id="ee2c9-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="ee2c9-107">Prerequisites</span></span>

<span data-ttu-id="ee2c9-108">Data Lake Tools 可以安裝在受 VS Code 支援的平台上。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-108">Data Lake Tools can be installed on the platforms supported by VS Code.</span></span> <span data-ttu-id="ee2c9-109">所支援的平台包括 Windows、Linux 及 MacOS。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-109">The supported platforms include Windows, Linux, and MacOS.</span></span> <span data-ttu-id="ee2c9-110">不同的平台各自具有下列必要條件：</span><span class="sxs-lookup"><span data-stu-id="ee2c9-110">The different platforms have the following prerequisites:</span></span>

- <span data-ttu-id="ee2c9-111">Windows</span><span class="sxs-lookup"><span data-stu-id="ee2c9-111">Windows</span></span>

    - <span data-ttu-id="ee2c9-112">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-112">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span></span>
    - <span data-ttu-id="ee2c9-113">[Java SE Runtime Environment version 8 update 77 或更新版本](https://java.com/download/manual.jsp)。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-113">[Java SE Runtime Environment version 8 update 77 or later](https://java.com/download/manual.jsp).</span></span> <span data-ttu-id="ee2c9-114">請將 java.exe 路徑新增至系統環境變數路徑中。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-114">Add the java.exe path to the system environment variable path.</span></span> <span data-ttu-id="ee2c9-115">如需設定方面的指示，請參閱[我要如何設定或變更 Path 系統變數？]( https://www.java.com/download/help/path.xml)。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-115">For configuration instructions, see [How do I set or change the Path system variable?]( https://www.java.com/download/help/path.xml).</span></span> <span data-ttu-id="ee2c9-116">路徑類似於 C:\Program Files\Java\jdk1.8.0_77\jre\bin。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-116">The path is similar to C:\Program Files\Java\jdk1.8.0_77\jre\bin.</span></span>
    - <span data-ttu-id="ee2c9-117">[.NET Core SDK 1.0.3 或 .NET Core 1.1 執行階段](https://www.microsoft.com/net/download)。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-117">[.NET Core SDK 1.0.3 or .NET Core 1.1 runtime](https://www.microsoft.com/net/download).</span></span>
    
- <span data-ttu-id="ee2c9-118">Linux (我們建議使用 Ubuntu 14.04 LTS)</span><span class="sxs-lookup"><span data-stu-id="ee2c9-118">Linux (We recommend Ubuntu 14.04 LTS)</span></span>

    - <span data-ttu-id="ee2c9-119">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-119">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span></span> <span data-ttu-id="ee2c9-120">若要安裝程式碼，請輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="ee2c9-120">To install the code, enter the following command:</span></span>

              sudo dpkg -i code_<version_number>_amd64.deb

    - <span data-ttu-id="ee2c9-121">[Mono 4.2.x](http://www.mono-project.com/docs/getting-started/install/linux/)。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-121">[Mono 4.2.x](http://www.mono-project.com/docs/getting-started/install/linux/).</span></span> 

        - <span data-ttu-id="ee2c9-122">若要更新 deb 套件來源，請輸入下列命令︰</span><span class="sxs-lookup"><span data-stu-id="ee2c9-122">To update the deb package source, enter the following commands:</span></span>

                sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
                echo "deb http://download.mono-project.com/repo/debian wheezy/snapshots 4.2.4.4/main" | sudo tee /etc/apt/sources.list.d/mono-xamarin.list
                sudo apt-get update

        - <span data-ttu-id="ee2c9-123">若要安裝 Mono，請輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="ee2c9-123">To install Mono, enter the following command:</span></span>

                sudo apt-get install mono-complete

            > [!NOTE] 
            > <span data-ttu-id="ee2c9-124">不支援 Mono 4.6。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-124">Mono 4.6 is not supported.</span></span> <span data-ttu-id="ee2c9-125">在安裝 4.2.x 之前，請先徹底解除安裝 4.6 版。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-125">Uninstall version 4.6 entirely before you install 4.2.x.</span></span>  

        - <span data-ttu-id="ee2c9-126">[Java SE Runtime Environment version 8 update 77 或更新版本](https://java.com/download/manual.jsp)。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-126">[Java SE Runtime Environment version 8 update 77 or later](https://java.com/download/manual.jsp).</span></span> <span data-ttu-id="ee2c9-127">如需安裝方面的指示，請參閱[適用於 Java 的 Linux 64 位元安裝指示]( https://java.com/en/download/help/linux_x64_install.xml)頁面。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-127">For instructions on installation, see the [Linux 64-bit installation instructions for Java]( https://java.com/en/download/help/linux_x64_install.xml) page.</span></span>
        - <span data-ttu-id="ee2c9-128">[.NET Core SDK 1.0.3 或 .NET Core 1.1 執行階段](https://www.microsoft.com/net/download)。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-128">[.NET Core SDK 1.0.3 or .NET Core 1.1 runtime](https://www.microsoft.com/net/download).</span></span>
- <span data-ttu-id="ee2c9-129">MacOS</span><span class="sxs-lookup"><span data-stu-id="ee2c9-129">MacOS</span></span>

    - <span data-ttu-id="ee2c9-130">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-130">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span></span>
    - <span data-ttu-id="ee2c9-131">[Mono 4.2.4](http://download.mono-project.com/archive/4.2.4/macos-10-x86/)。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-131">[Mono 4.2.4](http://download.mono-project.com/archive/4.2.4/macos-10-x86/).</span></span> 
    - <span data-ttu-id="ee2c9-132">[Java SE Runtime Environment version 8 update 77 或更新版本](https://java.com/download/manual.jsp)。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-132">[Java SE Runtime Environment version 8 update 77 or later](https://java.com/download/manual.jsp).</span></span> <span data-ttu-id="ee2c9-133">如需安裝方面的指示，請參閱[適用於 Java 的 Linux 64 位元安裝指示](https://java.com/en/download/help/mac_install.xml)頁面。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-133">For instructions on installation, see the [Linux 64-bit installation instructions for Java](https://java.com/en/download/help/mac_install.xml) page.</span></span>
    - <span data-ttu-id="ee2c9-134">[.NET Core SDK 1.0.3 或 .NET Core 1.1 執行階段](https://www.microsoft.com/net/download)。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-134">[.NET Core SDK 1.0.3 or .NET Core 1.1 runtime](https://www.microsoft.com/net/download).</span></span>

## <a name="install-data-lake-tools"></a><span data-ttu-id="ee2c9-135">安裝 Data Lake Tools</span><span class="sxs-lookup"><span data-stu-id="ee2c9-135">Install Data Lake Tools</span></span>

<span data-ttu-id="ee2c9-136">安裝完必要條件之後，您就可以安裝 Data Lake Tools for VS Code。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-136">After you install the prerequisites, you can install Data Lake Tools for VS Code.</span></span>

<span data-ttu-id="ee2c9-137">**安裝 Data Lake Tools**</span><span class="sxs-lookup"><span data-stu-id="ee2c9-137">**To install Data Lake Tools**</span></span>

1. <span data-ttu-id="ee2c9-138">開啟 Visual Studio Code。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-138">Open Visual Studio Code.</span></span>
2. <span data-ttu-id="ee2c9-139">選取 Ctrl+P，然後輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="ee2c9-139">Select Ctrl+P, and then enter the following command:</span></span>
```
ext install usql-vscode-ext
```
<span data-ttu-id="ee2c9-140">您可以看到一份 Visual Studio 程式碼擴充功能清單。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-140">You can see a list of Visual Studio code extensions.</span></span> <span data-ttu-id="ee2c9-141">其中一個是 **Azure Data Lake Tools**。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-141">One of them is **Azure Data Lake Tools**.</span></span>

3. <span data-ttu-id="ee2c9-142">選取 [Azure Data Lake Tools] 旁邊的 [安裝]。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-142">Select **Install** next to **Azure Data Lake Tools**.</span></span> <span data-ttu-id="ee2c9-143">幾秒鐘後，[安裝] 按鈕會變為 [重新載入]。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-143">After a few seconds, the **Install** button changes to **Reload**.</span></span>
4. <span data-ttu-id="ee2c9-144">選取 [重新載入] 以啟動擴充功能。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-144">Select **Reload** to activate the extension.</span></span>
5. <span data-ttu-id="ee2c9-145">選取 [確定] 來進行確認。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-145">Select **OK** to confirm.</span></span> <span data-ttu-id="ee2c9-146">您會在 [擴充功能] 窗格中看到 Azure Data Lake Tools。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-146">You can see Azure Data Lake Tools in the **Extensions** pane.</span></span>
    <span data-ttu-id="ee2c9-147">![Data Lake Tools for Visual Studio Code 擴充功能窗格](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extensions.png)</span><span class="sxs-lookup"><span data-stu-id="ee2c9-147">![Data Lake Tools for Visual Studio Code Extensions pane](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extensions.png)</span></span>

## <a name="activate-azure-data-lake-tools"></a><span data-ttu-id="ee2c9-148">啟動 Azure Data Lake Tools</span><span class="sxs-lookup"><span data-stu-id="ee2c9-148">Activate Azure Data Lake Tools</span></span>
<span data-ttu-id="ee2c9-149">建立一個新的 .usql 檔案或開啟現有的 .usql 檔案，以啟動擴充功能。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-149">Create a new .usql file or open an existing .usql file to activate the extension.</span></span> 

## <a name="connect-to-azure"></a><span data-ttu-id="ee2c9-150">連接到 Azure</span><span class="sxs-lookup"><span data-stu-id="ee2c9-150">Connect to Azure</span></span>

<span data-ttu-id="ee2c9-151">您必須先連線到 Azure 帳戶，才能在 Data Lake Analytics 中編譯和執行 U-SQL 指令碼。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-151">Before you can compile and run U-SQL scripts in Data Lake Analytics, you must connect to your Azure account.</span></span>

<span data-ttu-id="ee2c9-152">**連接到 Azure**</span><span class="sxs-lookup"><span data-stu-id="ee2c9-152">**To connect to Azure**</span></span>

1.  <span data-ttu-id="ee2c9-153">選取 Ctrl+Shift+P 以開啟命令選擇區。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-153">Select Ctrl+Shift+P to open the command palette.</span></span> 
2.  <span data-ttu-id="ee2c9-154">輸入 **ADL: Login**。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-154">Enter **ADL: Login**.</span></span> <span data-ttu-id="ee2c9-155">登入資訊便會出現在 [輸出] 窗格。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-155">The login information appears in the **Output** pane.</span></span>

    <span data-ttu-id="ee2c9-156">![Data Lake Tools for Visual Studio Code 命令選擇區](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login.png)
    ![Data Lake Tools for Visual Studio Code 裝置登入資訊](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-login-info.png)</span><span class="sxs-lookup"><span data-stu-id="ee2c9-156">![Data Lake Tools for Visual Studio Code command palette](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login.png)
![Data Lake Tools for Visual Studio Code device login information](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-login-info.png)</span></span>
3. <span data-ttu-id="ee2c9-157">在登入 URL (https://aka.ms/devicelogin) 上選取 Ctrl 鍵再按一下滑鼠左鍵，以開啟登入網頁。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-157">Select Ctrl+click on the login URL: https://aka.ms/devicelogin to open the login webpage.</span></span> <span data-ttu-id="ee2c9-158">在文字方塊中輸入代碼 **G567LX42V**，然後選取 [繼續]。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-158">Enter the code **G567LX42V** into the text box, and then select **Continue**.</span></span>

   ![Data Lake Tools for Visual Studio Code 登入貼上代碼](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login-paste-code.png )   
4.  <span data-ttu-id="ee2c9-160">依照網頁上的指示登入。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-160">Follow the instructions to sign in from the webpage.</span></span> <span data-ttu-id="ee2c9-161">當您連線時，您的 Azure 帳戶名稱會出現在 [VS Code] 視窗左下角的狀態列中。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-161">When you're connected, your Azure account name appears on the status bar in the lower-left corner of the **VS Code** window.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="ee2c9-162">如果您的帳戶已啟用雙因素驗證，建議您使用電話驗證而非使用 PIN 碼。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-162">If your account has two factors enabled, we recommend that you use phone authentication rather than using a PIN.</span></span>

<span data-ttu-id="ee2c9-163">若要登出，請輸入命令 **ADL: Logout**。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-163">To sign out, enter the command **ADL: Logout**.</span></span>

## <a name="list-your-data-lake-analytics-accounts"></a><span data-ttu-id="ee2c9-164">列出 Data Lake Analytics 帳戶</span><span class="sxs-lookup"><span data-stu-id="ee2c9-164">List your Data Lake Analytics accounts</span></span>

<span data-ttu-id="ee2c9-165">若要測試連線，請取得 Data Lake Analytics 帳戶的清單。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-165">To test the connection, get a list of your Data Lake Analytics accounts.</span></span>

<span data-ttu-id="ee2c9-166">**列出您的 Azure 訂用帳戶下的 Data Lake Analytics 帳戶**</span><span class="sxs-lookup"><span data-stu-id="ee2c9-166">**To list the Data Lake Analytics accounts under your Azure subscription**</span></span>

1. <span data-ttu-id="ee2c9-167">選取 Ctrl+Shift+P 以開啟命令選擇區。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-167">Select Ctrl+Shift+P to open the command palette.</span></span>
2. <span data-ttu-id="ee2c9-168">輸入 **ADL: List Accounts**。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-168">Enter **ADL: List Accounts**.</span></span> <span data-ttu-id="ee2c9-169">帳戶會出現在 [輸出] 窗格中。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-169">The accounts appear in the **Output** pane.</span></span>

## <a name="open-the-sample-script"></a><span data-ttu-id="ee2c9-170">開啟範例指令碼</span><span class="sxs-lookup"><span data-stu-id="ee2c9-170">Open the sample script</span></span>
<span data-ttu-id="ee2c9-171">開啟命令選擇區 (Ctrl+Shift+P)，然後輸入 **ADL: Open Sample Script**。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-171">Open the command palette (Ctrl+Shift+P) and enter **ADL: Open Sample Script**.</span></span> <span data-ttu-id="ee2c9-172">這會開啟此範例的另一個執行個體。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-172">This opens another instance of this sample.</span></span> <span data-ttu-id="ee2c9-173">您也可以在此執行個體上編輯、設定及提交指令碼。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-173">You can also edit, configure, and submit script on this instance.</span></span>

## <a name="work-with-u-sql"></a><span data-ttu-id="ee2c9-174">使用 U-SQL</span><span class="sxs-lookup"><span data-stu-id="ee2c9-174">Work with U-SQL</span></span>

<span data-ttu-id="ee2c9-175">您需要開啟 U-SQL 檔案或資料夾以使用 U-SQL。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-175">You need open either a U-SQL file or a folder to work with U-SQL.</span></span>

<span data-ttu-id="ee2c9-176">**開啟 U-SQL 專案的資料夾**</span><span class="sxs-lookup"><span data-stu-id="ee2c9-176">**To open a folder for your U-SQL project**</span></span>

1. <span data-ttu-id="ee2c9-177">從 Visual Studio Code 選取 [檔案] 功能表，然後選取 [開啟資料夾]。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-177">From Visual Studio Code, select the **File** menu, and then select **Open Folder**.</span></span>
2. <span data-ttu-id="ee2c9-178">指定資料夾，然後選取 [選取資料夾]。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-178">Specify a folder, and then select **Select Folder**.</span></span>
3. <span data-ttu-id="ee2c9-179">選取 [檔案] 功能表，然後選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-179">Select the **File** menu, and then select **New**.</span></span> <span data-ttu-id="ee2c9-180">專案中就會加入一個 Untitled-1 檔案。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-180">An Untitled-1 file is added to the project.</span></span>
4. <span data-ttu-id="ee2c9-181">在 Untitled-1 檔案中輸入以下程式碼：</span><span class="sxs-lookup"><span data-stu-id="ee2c9-181">Enter the following code into the Untitled-1 file:</span></span>

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

    <span data-ttu-id="ee2c9-182">這個指令碼會在 /output 資料夾中建立 departments.csv 檔案並納入一些資料。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-182">The script creates a departments.csv file with some data included in the /output folder.</span></span>

5. <span data-ttu-id="ee2c9-183">在開啟的資料夾中，將檔案儲存為 **myUSQL.usql**。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-183">Save the file as **myUSQL.usql** in the opened folder.</span></span> <span data-ttu-id="ee2c9-184">專案中也會加入 adltools_settings.json 組態檔。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-184">A adltools_settings.json configuration file is also added to the project.</span></span>
4. <span data-ttu-id="ee2c9-185">開啟 adltools_settings.json，並使用下列屬性設定︰</span><span class="sxs-lookup"><span data-stu-id="ee2c9-185">Open and configure adltools_settings.json with the following properties:</span></span>

    - <span data-ttu-id="ee2c9-186">帳戶：在您的 Azure 訂用帳戶下的 Data Lake Analytics 帳戶。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-186">Account:  A Data Lake Analytics account under your Azure subscription.</span></span>
    - <span data-ttu-id="ee2c9-187">資料庫：您帳戶底下的資料庫。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-187">Database: A database under your account.</span></span> <span data-ttu-id="ee2c9-188">預設值為 **master**。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-188">The default is **master**.</span></span>
    - <span data-ttu-id="ee2c9-189">結構描述：您資料庫底下的結構描述。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-189">Schema: A schema under your database.</span></span> <span data-ttu-id="ee2c9-190">預設值為 **dbo**。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-190">The default is **dbo**.</span></span>
    - <span data-ttu-id="ee2c9-191">選擇性設定︰</span><span class="sxs-lookup"><span data-stu-id="ee2c9-191">Optional settings:</span></span>
        - <span data-ttu-id="ee2c9-192">優先順序︰優先順序範圍是從 1 到 1000，1 是最高的優先順序。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-192">Priority: The priority range is from 1 to 1000 with 1 as the highest priority.</span></span> <span data-ttu-id="ee2c9-193">預設值為 **1000**。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-193">The default value is **1000**.</span></span>
        - <span data-ttu-id="ee2c9-194">平行處理原則︰平行處理原則的範圍是從 1 到 150。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-194">Parallelism: The parallelism range is from 1 to 150.</span></span> <span data-ttu-id="ee2c9-195">預設值為您 Azure Data Lake Analytics 帳戶中允許的平行處理原則上限。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-195">The default value is the maximum parallelism allowed in your Azure Data Lake Analytics account.</span></span> 
        
        > [!NOTE] 
        > <span data-ttu-id="ee2c9-196">如果設定無效，則會使用預設值。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-196">If the settings are invalid, the default values are used.</span></span>

    ![Data Lake Tools for Visual Studio Code 組態檔](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-configuration-file.png)

    <span data-ttu-id="ee2c9-198">編譯和執行 U-SQL 作業需要計算 Data Lake Analytics 帳戶。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-198">A compute Data Lake Analytics account is needed to compile and run U-SQL jobs.</span></span> <span data-ttu-id="ee2c9-199">編譯和執行 U-SQL 作業之前，您必須先設定電腦帳戶。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-199">You must configure the computer account before you can compile and run U-SQL jobs.</span></span>
    
<span data-ttu-id="ee2c9-200">在儲存組態後，帳戶、資料庫和結構描述資訊就會出現在對應之 .usql 檔案左下角的狀態列上。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-200">After the configuration is saved, the account, database, and schema information appears on the status bar at the bottom-left corner of the corresponding .usql file.</span></span> 
 
 
<span data-ttu-id="ee2c9-201">相較於開啟檔案，當您開啟資料夾時，您可以：</span><span class="sxs-lookup"><span data-stu-id="ee2c9-201">Compared to opening a file, when you open a folder you can:</span></span>

- <span data-ttu-id="ee2c9-202">使用程式碼後置檔案。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-202">Use a code-behind file.</span></span> <span data-ttu-id="ee2c9-203">在單一檔案模式中，不支援程式碼後置。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-203">In the single-file mode, code-behind is not supported.</span></span>
- <span data-ttu-id="ee2c9-204">使用組態檔。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-204">Use a configuration file.</span></span> <span data-ttu-id="ee2c9-205">當您開啟資料夾時，工作資料夾中的指令碼會共用一個組態檔。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-205">When you open a folder, the scripts in the working folder share a single configuration file.</span></span>


<span data-ttu-id="ee2c9-206">U-SQL 指令碼會透過 Data Lake Analytics 服務在遠端進行編譯。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-206">The U-SQL script compiles remotely through the Data Lake Analytics service.</span></span> <span data-ttu-id="ee2c9-207">當您發出**編譯**命令時，U-SQL 指令碼會傳送至 Data Lake Analytics 帳戶。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-207">When you issue the **compile** command, the U-SQL script is sent to your Data Lake Analytics account.</span></span> <span data-ttu-id="ee2c9-208">之後，Visual Studio Code 會收到編譯結果。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-208">Later, Visual Studio Code receives the compilation result.</span></span> <span data-ttu-id="ee2c9-209">因為是遠端編譯，所以 Visual Studio Code 會需要您列出資訊才能連線到您在組態檔中的 Data Lake Analytics 帳戶。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-209">Due to the remote compilation, Visual Studio Code requires that you list the information to connect to your Data Lake Analytics account in the configuration file.</span></span>

<span data-ttu-id="ee2c9-210">**編譯 U-SQL 指令碼**</span><span class="sxs-lookup"><span data-stu-id="ee2c9-210">**To compile a U-SQL script**</span></span>

1. <span data-ttu-id="ee2c9-211">選取 Ctrl+Shift+P 以開啟命令選擇區。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-211">Select Ctrl+Shift+P to open the command palette.</span></span> 
2. <span data-ttu-id="ee2c9-212">輸入 **ADL: Compile Script**。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-212">Enter **ADL: Compile Script**.</span></span> <span data-ttu-id="ee2c9-213">編譯結果會出現在 [輸出] 視窗中。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-213">The compile results appear in the **Output** window.</span></span> <span data-ttu-id="ee2c9-214">您可以也在指令碼檔案上按一下滑鼠右鍵，然後選取 [ADL: Compile Script] 來編譯 U-SQL 作業。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-214">You can also right-click a script file, and then select **ADL: Compile Script** to compile a U-SQL job.</span></span> <span data-ttu-id="ee2c9-215">編譯結果會出現在 [輸出] 窗格中。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-215">The compilation result appears in the **Output** pane.</span></span>
 

<span data-ttu-id="ee2c9-216">**提交 U-SQL 指令碼**</span><span class="sxs-lookup"><span data-stu-id="ee2c9-216">**To submit a U-SQL script**</span></span>

1. <span data-ttu-id="ee2c9-217">選取 Ctrl+Shift+P 以開啟命令選擇區。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-217">Select Ctrl+Shift+P to open the command palette.</span></span> 
2. <span data-ttu-id="ee2c9-218">輸入 **ADL: Submit Job**。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-218">Enter **ADL: Submit Job**.</span></span>  <span data-ttu-id="ee2c9-219">您也可以在指令碼檔案上按一下滑鼠右鍵，然後選取 [ADL: Submit Job]。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-219">You can also right-click a script file, and then select **ADL: Submit Job**.</span></span> 

<span data-ttu-id="ee2c9-220">在提交 U-SQL 作業後，提交記錄會出現在 VS Code 的 [輸出] 視窗中。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-220">After you submit a U-SQL job, the submission logs appear in the **Output** window in VS Code.</span></span> <span data-ttu-id="ee2c9-221">如果提交成功，則作業 URL 也會出現。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-221">If the submission is successful, the job URL appears as well.</span></span> <span data-ttu-id="ee2c9-222">您可以在網頁瀏覽器中開啟作業 URL 來追蹤即時的作業狀態。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-222">You can open the job URL in a web browser to track the real-time job status.</span></span>

<span data-ttu-id="ee2c9-223">若要能夠輸出作業詳細資料，請在 **vs code for the u-sql_settings.json** 檔案中設定 **jobInformationOutputPath**。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-223">To enable the output of the job details, set **jobInformationOutputPath** in the **vs code for the u-sql_settings.json** file.</span></span>
 
## <a name="use-a-code-behind-file"></a><span data-ttu-id="ee2c9-224">使用程式碼後置檔案</span><span class="sxs-lookup"><span data-stu-id="ee2c9-224">Use a code-behind file</span></span>

<span data-ttu-id="ee2c9-225">程式碼後置檔案是與單一 U-SQL 指令碼關聯的 C# 檔案。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-225">A code-behind file is a C# file associated with a single U-SQL script.</span></span> <span data-ttu-id="ee2c9-226">您可以在程式碼後置檔案中定義專用於 UDO、UDA、UDT 和 UDF 的指令碼。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-226">You can define a script dedicated to UDO, UDA, UDT, and UDF in the code-behind file.</span></span> <span data-ttu-id="ee2c9-227">UDO、UDA、UDT 和 UDF 可以直接在指令碼中使用，而不需要先註冊組件。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-227">The UDO, UDA, UDT, and UDF can be used directly in the script without registering the assembly first.</span></span> <span data-ttu-id="ee2c9-228">程式碼後置檔案會放在與其對等互連 U-SQL 指令碼檔案相同的資料夾中。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-228">The code-behind file is put in the same folder as its peering U-SQL script file.</span></span> <span data-ttu-id="ee2c9-229">如果指令碼名稱為 xxx.usql，程式碼後置就會被命名為 xxx.usql.cs。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-229">If the script is named xxx.usql, the code-behind is named as xxx.usql.cs.</span></span> <span data-ttu-id="ee2c9-230">如果您手動刪除該程式碼後置檔案，系統就會停用其相關聯之 U-SQL 指令碼的程式碼後置功能。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-230">If you manually delete the code-behind file, the code-behind feature is disabled for its associated U-SQL script.</span></span> <span data-ttu-id="ee2c9-231">如需撰寫 U-SQL 指令碼之客戶程式碼的詳細資訊，請參閱[在 U-SQL 中撰寫並使用自訂程式碼：使用者定義函式]( https://blogs.msdn.microsoft.com/visualstudio/2015/10/28/writing-and-using-custom-code-in-u-sql-user-defined-functions/) (英文)。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-231">For more information about writing customer code for U-SQL script, see [Writing and Using Custom Code in U-SQL: User-Defined Functions]( https://blogs.msdn.microsoft.com/visualstudio/2015/10/28/writing-and-using-custom-code-in-u-sql-user-defined-functions/).</span></span>

<span data-ttu-id="ee2c9-232">若要支援程式碼後置，您必須開啟工作資料夾。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-232">To support code-behind, you must open a working folder.</span></span> 

<span data-ttu-id="ee2c9-233">**產生程式碼後置檔案**</span><span class="sxs-lookup"><span data-stu-id="ee2c9-233">**To generate a code-behind file**</span></span>

1. <span data-ttu-id="ee2c9-234">開啟來源檔案。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-234">Open a source file.</span></span> 
2. <span data-ttu-id="ee2c9-235">選取 Ctrl+Shift+P 以開啟命令選擇區。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-235">Select Ctrl+Shift+P to open the command palette.</span></span>
3. <span data-ttu-id="ee2c9-236">輸入 **ADL: Generate Code Behind**。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-236">Enter **ADL: Generate Code Behind**.</span></span> <span data-ttu-id="ee2c9-237">程式碼後置檔案會建立在相同的資料夾中。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-237">A code-behind file is created in the same folder.</span></span> 

<span data-ttu-id="ee2c9-238">您也可以在指令碼檔案上按一下滑鼠右鍵，然後選取 [ADL: Generate Code Behind]。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-238">You can also right-click a script file, and then select **ADL: Generate Code Behind**.</span></span> 

<span data-ttu-id="ee2c9-239">若要使用程式碼後置檔案來編譯並提交 U-SQL 指令碼，其方式與獨立的 U-SQL 指令碼檔案相同。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-239">To compile and submit a U-SQL script with a code-behind file is the same as with the standalone U-SQL script file.</span></span>

<span data-ttu-id="ee2c9-240">下列兩個螢幕擷取畫面顯示程式碼後置檔案及其相關聯的 U-SQL 指令碼檔案︰</span><span class="sxs-lookup"><span data-stu-id="ee2c9-240">The following two screenshots show a code-behind file and its associated U-SQL script file:</span></span>
 
![Data Lake Tools for Visual Studio Code 程式碼後置](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-code-behind.png)

![Data Lake Tools for Visual Studio Code 程式碼後置指令碼檔案](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-code-behind-call.png) 

## <a name="use-assemblies"></a><span data-ttu-id="ee2c9-243">使用組件</span><span class="sxs-lookup"><span data-stu-id="ee2c9-243">Use assemblies</span></span>

<span data-ttu-id="ee2c9-244">如需有關開發組件的資訊，請參閱[針對 Azure Data Lake Analytics 作業開發 U-SQL 組件](data-lake-analytics-u-sql-develop-assemblies.md)。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-244">For information on developing assemblies, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md).</span></span>

<span data-ttu-id="ee2c9-245">您可以使用 Data Lake Tools 在 Data Lake Analytics 目錄中註冊自訂程式碼組件。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-245">You can use Data Lake Tools to register custom code assemblies in the Data Lake Analytics catalog.</span></span>

<span data-ttu-id="ee2c9-246">**註冊組件**</span><span class="sxs-lookup"><span data-stu-id="ee2c9-246">**To register an assembly**</span></span>

<span data-ttu-id="ee2c9-247">您可以透過 **ADL: Register Assembly** 或 **ADL: Register Assembly through Configuration** 命令來註冊組件。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-247">You can register the assembly through the **ADL: Register Assembly** or **ADL: Register Assembly through Configuration** commands.</span></span>

<span data-ttu-id="ee2c9-248">**透過 ADL: Register Assembly 命令來進行註冊**</span><span class="sxs-lookup"><span data-stu-id="ee2c9-248">**To register through the ADL: Register Assembly command**</span></span>
1.  <span data-ttu-id="ee2c9-249">選取 Ctrl+Shift+P 以開啟命令選擇區。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-249">Select Ctrl+Shift+P to open the command palette.</span></span>
2.  <span data-ttu-id="ee2c9-250">輸入 **ADL: Register Assembly**。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-250">Enter **ADL: Register Assembly**.</span></span> 
3.  <span data-ttu-id="ee2c9-251">指定本機組件路徑。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-251">Specify the local assembly path.</span></span> 
4.  <span data-ttu-id="ee2c9-252">選取 Data Lake Analytics 帳戶。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-252">Select a Data Lake Analytics account.</span></span>
5.  <span data-ttu-id="ee2c9-253">選取資料庫。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-253">Select a database.</span></span>

<span data-ttu-id="ee2c9-254">結果：入口網站會在瀏覽器中開啟，並顯示組件註冊程序。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-254">Results: The portal is opened in a browser and displays the assembly registration process.</span></span>  

<span data-ttu-id="ee2c9-255">另一個可供觸發 **ADL: Register Assembly** 命令的便利方式，是對檔案總管中的 .dll 檔案按一下滑鼠右鍵。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-255">Another convenient way to trigger the **ADL: Register Assembly** command is to right-click the .dll file in File Explorer.</span></span> 

<span data-ttu-id="ee2c9-256">**透過 ADL: Register Assembly through Configuration 命令來進行註冊**</span><span class="sxs-lookup"><span data-stu-id="ee2c9-256">**To register though the ADL: Register Assembly through Configuration command**</span></span>
1.  <span data-ttu-id="ee2c9-257">選取 Ctrl+Shift+P 以開啟命令選擇區。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-257">Select Ctrl+Shift+P to open the command palette.</span></span>
2.  <span data-ttu-id="ee2c9-258">輸入 **ADL: Register Assembly through Configuration**。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-258">Enter **ADL: Register Assembly through Configuration**.</span></span> 
3.  <span data-ttu-id="ee2c9-259">指定本機組件路徑。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-259">Specify the local assembly path.</span></span> 
4.  <span data-ttu-id="ee2c9-260">隨即會顯示 JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-260">The JSON file is displayed.</span></span> <span data-ttu-id="ee2c9-261">請視需要檢閱並編輯組件相依性及資源參數。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-261">Review and edit the assembly dependencies and resource parameters, if needed.</span></span> <span data-ttu-id="ee2c9-262">指示會顯示在 [輸出] 視窗中。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-262">Instructions are displayed in the **Output** window.</span></span> <span data-ttu-id="ee2c9-263">若要繼續進行組件註冊，請儲存 (Ctrl + S) JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-263">To proceed to the assembly registration, save (Ctrl+S) the JSON file.</span></span>

![Data Lake Tools for Visual Studio Code 程式碼後置](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-register-assembly-advance.png)
>[!NOTE]
>- <span data-ttu-id="ee2c9-265">組件相依性：Azure Data Lake Tools 會自動偵測 DLL 是否有任何相依項目。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-265">Assembly dependencies: Azure Data Lake Tools autodetects whether the DLL has any dependencies.</span></span> <span data-ttu-id="ee2c9-266">系統偵測到相依項目後，就會將其顯示在 JSON 檔案中。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-266">The dependencies are displayed in the JSON file after they are detected.</span></span> 
>- <span data-ttu-id="ee2c9-267">資源：您可以在註冊組件時上傳 DLL 資源 (例如 .txt、.png 和 .csv)。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-267">Resources: You can upload your DLL resources (for example, .txt, .png, and .csv) as part of the assembly registration.</span></span> 

<span data-ttu-id="ee2c9-268">另一個可供觸發 **ADL: Register Assembly through Configuration** 命令的方式，是對檔案總管中的 .dll 檔案按一下滑鼠右鍵。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-268">Another way to trigger the **ADL: Register Assembly through Configuration** command is to right-click the .dll file in File Explorer.</span></span> 

<span data-ttu-id="ee2c9-269">下列 U-SQL 程式碼示範如何呼叫組件。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-269">The following U-SQL code demonstrates how to call an assembly.</span></span> <span data-ttu-id="ee2c9-270">在此範例中，組件名稱是 *test*。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-270">In the sample, the assembly name is *test*.</span></span>

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
    TO @"Sample/SearchLogtest.txt" 
    USING Outputters.Tsv();
```


## <a name="access-the-data-lake-analytics-catalog"></a><span data-ttu-id="ee2c9-271">存取 Data Lake Analytics 目錄</span><span class="sxs-lookup"><span data-stu-id="ee2c9-271">Access the Data Lake Analytics catalog</span></span>

<span data-ttu-id="ee2c9-272">連線至 Azure 之後，您可以使用下列步驟來存取 U-SQL 目錄。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-272">After you have connected to Azure, you can use the following steps to access the U-SQL catalog.</span></span>

<span data-ttu-id="ee2c9-273">**存取 Azure Data Lake Analytics 中繼資料**</span><span class="sxs-lookup"><span data-stu-id="ee2c9-273">**To access the Azure Data Lake Analytics metadata**</span></span>

1.  <span data-ttu-id="ee2c9-274">選取 Ctrl+Shift+P，然後輸入 **ADL: List Tables**。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-274">Select Ctrl+Shift+P, and then enter **ADL: List Tables**.</span></span>
2.  <span data-ttu-id="ee2c9-275">選取其中一個 Data Lake Analytics 帳戶。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-275">Select one of the Data Lake Analytics accounts.</span></span>
3.  <span data-ttu-id="ee2c9-276">選取其中一個 Data Lake Analytics 資料庫。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-276">Select one of the Data Lake Analytics databases.</span></span>
4.  <span data-ttu-id="ee2c9-277">選取其中一個結構描述。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-277">Select one of the schemas.</span></span> <span data-ttu-id="ee2c9-278">您就會看到資料表清單。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-278">You can see the list of tables.</span></span>

## <a name="view-data-lake-analytics-jobs"></a><span data-ttu-id="ee2c9-279">檢視 Data Lake Analytics 作業</span><span class="sxs-lookup"><span data-stu-id="ee2c9-279">View Data Lake Analytics jobs</span></span>

<span data-ttu-id="ee2c9-280">**檢視 Data Lake Analytics 作業**</span><span class="sxs-lookup"><span data-stu-id="ee2c9-280">**To view Data Lake Analytics jobs**</span></span>
1.  <span data-ttu-id="ee2c9-281">開啟命令選擇區 (Ctrl+Shift+P)，然後選取 [ADL: Show Job]。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-281">Open the command palette (Ctrl+Shift+P) and select **ADL: Show Job**.</span></span> 
2.  <span data-ttu-id="ee2c9-282">選取 Data Lake Analytics 帳戶或本機帳戶。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-282">Select a Data Lake Analytics or local account.</span></span> 
3.  <span data-ttu-id="ee2c9-283">等候帳戶的作業清單出現。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-283">Wait for the jobs list for the account to appear.</span></span>
4.  <span data-ttu-id="ee2c9-284">從作業清單中選取一個作業，Data Lake Tools 就會在 Azure 入口網站中開啟作業的詳細資料，並在 VS Code 中顯示 JobInfo 檔案。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-284">Select a job from job list, Data Lake Tools opens the job details in the Azure portal and displays the JobInfo file in VS Code.</span></span>

![Data Lake Tools for Visual Studio Code IntelliSense 物件類型](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-show-job.png)

## <a name="azure-data-lake-storage-integration"></a><span data-ttu-id="ee2c9-286">Azure Data Lake Storage 整合</span><span class="sxs-lookup"><span data-stu-id="ee2c9-286">Azure Data Lake Storage integration</span></span>

<span data-ttu-id="ee2c9-287">您可以使用 Azure Data Lake Storage 相關命令來進行下列作業：</span><span class="sxs-lookup"><span data-stu-id="ee2c9-287">You can use Azure Data Lake Storage-related commands to:</span></span>
 - <span data-ttu-id="ee2c9-288">瀏覽 Azure Data Lake Storage 資源。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-288">Browse through the Azure Data Lake Storage resources.</span></span> 
 - <span data-ttu-id="ee2c9-289">預覽 Azure Data Lake Storage 檔案。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-289">Preview the Azure Data Lake Storage file.</span></span>  
 - <span data-ttu-id="ee2c9-290">在 VS Code 中直接將檔案上傳至 Azure Data Lake Storage。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-290">Upload the file directly to Azure Data Lake Storage in VS Code.</span></span> 

### <a name="list-the-storage-path"></a><span data-ttu-id="ee2c9-291">列出儲存體路徑</span><span class="sxs-lookup"><span data-stu-id="ee2c9-291">List the storage path</span></span> 
<span data-ttu-id="ee2c9-292">您可以透過命令選擇區或透過按一下滑鼠右鍵來列出儲存體路徑。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-292">You can list the storage path through the command palette or through right-click.</span></span>

<span data-ttu-id="ee2c9-293">**透過命令選擇區來列出儲存體路徑**</span><span class="sxs-lookup"><span data-stu-id="ee2c9-293">**To list the storage path through the command palette**</span></span>

1.  <span data-ttu-id="ee2c9-294">開啟命令選擇區 (Ctrl+Shift+P)，然後輸入 [ADL: List Storage Path]。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-294">Open the command palette (Ctrl+Shift+P) and enter **ADL: List Storage Path**.</span></span>

    ![Data Lake Tools for Visual Studio Code 列出儲存體路徑](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-storage.png)

2.  <span data-ttu-id="ee2c9-296">選取您慣用的列出儲存體路徑方式。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-296">Select your preferred way for listing the storage path.</span></span> <span data-ttu-id="ee2c9-297">本段使用 [Enter a path] \(輸入路徑\) 作為範例。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-297">This passage uses **Enter a path** as an example.</span></span>

    ![Data Lake Tools for Visual Studio Code 是其中一種用來列出儲存體路徑的方法](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account-selectoneway.png)

    > [!NOTE]
    >- <span data-ttu-id="ee2c9-299">VS Code 會在每個 Data Lake Analytics 帳戶中保留最後一次瀏覽路徑。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-299">VS Code keeps the last-visited path in every Data Lake Analytics account.</span></span> <span data-ttu-id="ee2c9-300">例如：/tt/ss。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-300">For example: /tt/ss.</span></span>
    >- <span data-ttu-id="ee2c9-301">來自根路徑的瀏覽器：來自所選 Data Lake Analytics 帳戶或本機路徑的清單根路徑。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-301">Browser from root path: The list root path from your selected Data Lake Analytics account or a local path.</span></span>
    >- <span data-ttu-id="ee2c9-302">輸入路徑：從所選 Data Lake Analytics 帳戶或本機路徑列出指定的路徑。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-302">Enter a path: List a specified path from your selected Data Lake Analytics account or a local path.</span></span>
    
3. <span data-ttu-id="ee2c9-303">選取本機路徑中的帳戶或 Data Lake Analytics 帳戶。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-303">Select an account from the local path or a Data Lake Analytics account.</span></span>

    ![Data Lake Tools for Visual Studio Code 選取更多](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

4. <span data-ttu-id="ee2c9-305">選取 [更多] 以列出更多個 Data Lake Analytics 帳戶，然後選取某個 Data Lake Analytics 帳戶。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-305">Select **more** to list more Data Lake Analytics accounts, and then select a Data Lake Analytics account.</span></span>

    ![Data Lake Tools for Visual Studio Code 選取一個帳戶](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-select-adla-account.png)

5.  <span data-ttu-id="ee2c9-307">輸入 Azure 儲存體路徑。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-307">Enter an Azure storage path.</span></span> <span data-ttu-id="ee2c9-308">例如，/output。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-308">For example, /output.</span></span>

    ![Data Lake Tools for Visual Studio Code 輸入儲存體路徑](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-path.png)

6.  <span data-ttu-id="ee2c9-310">結果：命令選擇區會根據您的輸入列出路徑資訊。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-310">Results: The command palette lists the path information based on your entries.</span></span>

    ![Data Lake Tools for Visual Studio Code 列出儲存體路徑結果](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-path.png)

<span data-ttu-id="ee2c9-312">可供列出相對路徑的更便利方式為透過右鍵快顯功能表。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-312">A more convenient way to list the relative path is through the right-click context menu.</span></span>

<span data-ttu-id="ee2c9-313">**透過按一下滑鼠右鍵來列出儲存體路徑**</span><span class="sxs-lookup"><span data-stu-id="ee2c9-313">**To list the storage path through right-click**</span></span>

1.  <span data-ttu-id="ee2c9-314">在路徑字串上按一下滑鼠右鍵以選取 [List Storage Path]。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-314">Right-click the path string to select **List Storage Path**.</span></span>

       ![Data Lake Tools for Visual Studio Code 右鍵快顯功能表](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-right-click-path.png)

2. <span data-ttu-id="ee2c9-316">所選取的相對路徑會出現在命令選擇區中。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-316">The selected relative path appears in the command palette.</span></span>

   ![Data Lake Tools for Visual Studio Code 選取的相對路徑](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-relative-path.png)

3.  <span data-ttu-id="ee2c9-318">選取本機路徑中的帳戶或 Data Lake Analytics 帳戶。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-318">Select an account from the local path or a Data Lake Analytics account.</span></span>

       ![Data Lake Tools for Visual Studio Code 選取一個帳戶](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

4.  <span data-ttu-id="ee2c9-320">結果：命令選擇區會列出目前路徑的資料夾和檔案。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-320">Results: The command palette lists the folders and files for the current path.</span></span>

       ![目前路徑中的 Data Lake Tools for Visual Studio Code 清單](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-current.png)

### <a name="preview-the-storage-file"></a><span data-ttu-id="ee2c9-322">預覽儲存體檔案</span><span class="sxs-lookup"><span data-stu-id="ee2c9-322">Preview the storage file</span></span>
<span data-ttu-id="ee2c9-323">您可以透過命令選擇區或透過按一下滑鼠右鍵來預覽儲存體檔案。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-323">You can preview the storage file through the command palette or through right-click.</span></span>

<span data-ttu-id="ee2c9-324">**透過命令選擇區來預覽儲存體檔案**</span><span class="sxs-lookup"><span data-stu-id="ee2c9-324">**To preview the storage file through the command palette**</span></span>

1.  <span data-ttu-id="ee2c9-325">開啟命令選擇區 (Ctrl+Shift+P)，然後輸入 [ADL: Preview Storage File]。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-325">Open the command palette (Ctrl+Shift+P) and enter **ADL: Preview Storage File**.</span></span>

       ![Data Lake Tools for Visual Studio Code 預覽儲存體檔案](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-preview.png)

2.  <span data-ttu-id="ee2c9-327">選取本機路徑中的帳戶或 Data Lake Analytics 帳戶。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-327">Select an account from the local path or a Data Lake Analytics account.</span></span>

       ![Data Lake Tools for Visual Studio Code 列出帳戶](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

3.  <span data-ttu-id="ee2c9-329">選取 [更多] 以列出更多個 Data Lake Analytics 帳戶，然後選取某個 Data Lake Analytics 帳戶。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-329">Select **more** to list more Data Lake Analytics accounts, and then select a Data Lake Analytics account.</span></span>

       ![Data Lake Tools for Visual Studio Code 選取一個帳戶](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-select-adla-account.png)

4.  <span data-ttu-id="ee2c9-331">輸入 Azure 儲存體路徑或檔案。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-331">Enter an Azure storage path or file.</span></span> <span data-ttu-id="ee2c9-332">例如：/output/SearchLog.txt。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-332">For example, /output/SearchLog.txt.</span></span>

       ![Data Lake Tools for Visual Studio Code 輸入儲存體路徑和檔案](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-preview-file.png)

5.  <span data-ttu-id="ee2c9-334">結果：命令選擇區會根據您的輸入列出路徑資訊。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-334">Results: The command palette lists the path information based on your entries.</span></span>

       ![Data Lake Tools for Visual Studio Code 預覽檔案結果](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-preview-results.png)

<span data-ttu-id="ee2c9-336">**透過按一下滑鼠右鍵來列出儲存體路徑**</span><span class="sxs-lookup"><span data-stu-id="ee2c9-336">**To list the storage path through right-click**</span></span>

1.  <span data-ttu-id="ee2c9-337">若要預覽檔案，請在檔案路徑上按一下滑鼠右鍵。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-337">To preview a file, right-click the file path.</span></span>

   ![Data Lake Tools for Visual Studio Code 右鍵快顯功能表](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-right-click-preview.png) 

2.  <span data-ttu-id="ee2c9-339">選取本機路徑中的帳戶或 Data Lake Analytics 帳戶。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-339">Select an account from the local path or a Data Lake Analytics account.</span></span>

       ![Data Lake Tools for Visual Studio Code 選取一個帳戶](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

3.  <span data-ttu-id="ee2c9-341">結果：VS Code 會顯示檔案的預覽結果。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-341">Results: VS Code displays the preview results of the file.</span></span>

       ![Data Lake Tools for Visual Studio Code 預覽檔案結果](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-preview-results.png)

### <a name="upload-a-file"></a><span data-ttu-id="ee2c9-343">上傳檔案</span><span class="sxs-lookup"><span data-stu-id="ee2c9-343">Upload a file</span></span> 

<span data-ttu-id="ee2c9-344">您可以透過輸入 **ADL: Upload File** 或 **ADL: Upload File through Configuration** 命令來上傳檔案。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-344">You can upload files by entering the commands **ADL: Upload File** or **ADL: Upload File through Configuration**.</span></span>

<span data-ttu-id="ee2c9-345">**透過 ADL: Upload File 命令來上傳檔案**</span><span class="sxs-lookup"><span data-stu-id="ee2c9-345">**To upload files though the ADL: Upload File command**</span></span>
1. <span data-ttu-id="ee2c9-346">選取 Ctrl+Shift+P 以開啟命令選擇區或在指令碼編輯器上按一下滑鼠右鍵，然後輸入 **Upload File**。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-346">Select Ctrl+Shift+P to open the command palette or right-click the script editor, and then enter **Upload File**.</span></span>
2.  <span data-ttu-id="ee2c9-347">若要上傳檔案，請輸入本機路徑。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-347">To upload the file, enter a local path.</span></span>

    ![Data Lake Tools for Visual Studio Code 輸入本機路徑](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-input-local-path.png)

3. <span data-ttu-id="ee2c9-349">選取其中一個用來列出儲存體路徑的方式。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-349">Select one of the ways of listing the storage path.</span></span> <span data-ttu-id="ee2c9-350">本段使用 [Enter a path] \(輸入路徑\) 作為範例。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-350">This passage uses **Enter a path** as an example.</span></span>

    ![Data Lake Tools for Visual Studio Code 列出儲存體路徑](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account-selectoneway.png)
    >[!NOTE]
    >- <span data-ttu-id="ee2c9-352">VS Code 會在每個 Data Lake Analytics 帳戶中保留最後一次瀏覽路徑。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-352">VS Code keeps the last-visited path in every Data Lake Analytics account.</span></span> <span data-ttu-id="ee2c9-353">例如：/tt/ss。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-353">For example: /tt/ss.</span></span>
    >- <span data-ttu-id="ee2c9-354">來自根路徑的瀏覽器：來自所選 Data Lake Analytics 帳戶或本機路徑的清單根路徑。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-354">Browser from root path: The list root path from your selected Data Lake Analytics account or a local path.</span></span>
    >- <span data-ttu-id="ee2c9-355">輸入路徑：從所選 Data Lake Analytics 帳戶或本機路徑列出指定的路徑。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-355">Enter a path: List a specified path from your selected Data Lake Analytics account or a local path.</span></span>

4. <span data-ttu-id="ee2c9-356">選取本機路徑中的帳戶或 Data Lake Analytics 帳戶。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-356">Select an account from the local path or a Data Lake Analytics account.</span></span>

    ![Data Lake Tools for Visual Studio Code 在儲存體上按一下滑鼠右鍵](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

5. <span data-ttu-id="ee2c9-358">輸入 Azure 儲存體路徑。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-358">Enter an Azure storage path.</span></span> <span data-ttu-id="ee2c9-359">例如：/output。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-359">For example: /output.</span></span>

       ![Data Lake Tools for Visual Studio Code enter storage path](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-preview-file.png)

6. <span data-ttu-id="ee2c9-360">找出您的 Azure 儲存體路徑。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-360">Find your Azure storage path.</span></span> <span data-ttu-id="ee2c9-361">選取 [Choose current folder] \(選擇目前的資料夾\)。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-361">Select **Choose current folder**.</span></span>

    ![Data Lake Tools for Visual Studio Code 選取資料夾](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-choose-current-folder.png)

7.  <span data-ttu-id="ee2c9-363">結果：[輸出] 視窗會顯示檔案上傳狀態。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-363">Results: The **Output** window displays the file upload status.</span></span>

       ![Data Lake Tools for Visual Studio Code 上傳狀態](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-status.png)    

<span data-ttu-id="ee2c9-365">**透過 ADL: Upload File through Configuration 命令來上傳檔案**</span><span class="sxs-lookup"><span data-stu-id="ee2c9-365">**To upload files though the ADL: Upload File through Configuration command**</span></span>
1.  <span data-ttu-id="ee2c9-366">選取 Ctrl+Shift+P 以開啟命令選擇區或在指令碼編輯器上按一下滑鼠右鍵，然後輸入 **Upload File through Configuration**。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-366">Select Ctrl+Shift+P to open the command palette or right-click the script editor, and then enter **Upload File through Configuration**.</span></span>
2.  <span data-ttu-id="ee2c9-367">VS Code 會顯示一個 JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-367">VS Code displays a JSON file.</span></span> <span data-ttu-id="ee2c9-368">您可以輸入檔案路徑，然後同時上傳多個檔案。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-368">You can enter file paths and upload multiple files at the same time.</span></span> <span data-ttu-id="ee2c9-369">指示會顯示在 [輸出] 視窗中。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-369">Instructions are displayed in the **Output** window.</span></span> <span data-ttu-id="ee2c9-370">若要繼續上傳檔案，請儲存 (Ctrl+S) JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-370">To proceed to upload the file, save (Ctrl+S) the JSON file.</span></span>

       ![Data Lake Tools for Visual Studio Code 檔案路徑](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-file.png)

3.  <span data-ttu-id="ee2c9-372">結果：[輸出] 視窗會顯示檔案上傳狀態。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-372">Results: The **Output** window displays the file upload status.</span></span>

       ![Data Lake Tools for Visual Studio Code 上傳狀態](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-status.png)     

<span data-ttu-id="ee2c9-374">還有另一個將檔案上傳到儲存體的方式，就是在指令碼編輯器中的檔案完整路徑或檔案相對路徑上，透過右鍵操作功能表來上傳。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-374">Another way to upload a file to storage is through the right-click menu on the file's full path or the file's relative path in the script editor.</span></span> <span data-ttu-id="ee2c9-375">輸入本機檔案路徑，然後選取帳戶。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-375">Enter the local file path, and then select the account.</span></span> <span data-ttu-id="ee2c9-376">[輸出] 視窗會顯示上傳狀態。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-376">The **Output** window displays the upload status.</span></span> 

### <a name="open-azure-storage-explorer"></a><span data-ttu-id="ee2c9-377">開啟 Azure 儲存體總管</span><span class="sxs-lookup"><span data-stu-id="ee2c9-377">Open Azure Storage Explorer</span></span>
<span data-ttu-id="ee2c9-378">您可以透過輸入 **ADL: Open Web Azure Storage Explorer** 命令來開啟 **Azure 儲存體總管**，或透過從右鍵快顯功能表選取 Azure 儲存體總管來加以開啟。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-378">You can open **Azure Storage Explorer** by entering the command **ADL: Open Web Azure Storage Explorer** or by selecting it from the right-click context menu.</span></span>

<span data-ttu-id="ee2c9-379">**開啟 Azure 儲存體總管**</span><span class="sxs-lookup"><span data-stu-id="ee2c9-379">**To open Azure Storage Explorer**</span></span>

1. <span data-ttu-id="ee2c9-380">選取 Ctrl+Shift+P 以開啟命令選擇區。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-380">Select Ctrl+Shift+P to open the command palette.</span></span>
2. <span data-ttu-id="ee2c9-381">輸入 **Open Web Azure Storage Explorer**，或在指令碼編輯器中的相對路徑或完整路徑上按一下滑鼠右鍵，然後選取 **Open Web Azure Storage Explorer**。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-381">Enter **Open Web Azure Storage Explorer** or right-click on a relative path or the full path in the script editor, and then select **Open Web Azure Storage Explorer**.</span></span>
3. <span data-ttu-id="ee2c9-382">選取 Data Lake Analytics 帳戶。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-382">Select a Data Lake Analytics account.</span></span>

<span data-ttu-id="ee2c9-383">Data Lake Tools 會在 Azure 入口網站中開啟 Azure 儲存體路徑。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-383">Data Lake Tools opens the Azure storage path in the Azure portal.</span></span> <span data-ttu-id="ee2c9-384">您可以找到該路徑，並從網路預覽檔案。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-384">You can find the path and preview the file from the web.</span></span>

### <a name="local-run-and-local-debug-for-windows-users"></a><span data-ttu-id="ee2c9-385">Windows 使用者的本機執行和本機偵錯</span><span class="sxs-lookup"><span data-stu-id="ee2c9-385">Local run and local debug for Windows users</span></span>
<span data-ttu-id="ee2c9-386">U-SQL 本機執行會先測試您的本機資料並在本機驗證您的指令碼，然後才將您的程式碼發行至 Data Lake Analytics。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-386">U-SQL local run tests your local data and validates your script locally, before your code is published to Data Lake Analytics.</span></span> <span data-ttu-id="ee2c9-387">本機偵錯功能可讓您先完成下列工作，再將您的程式碼提交給 Data Lake Analytics：</span><span class="sxs-lookup"><span data-stu-id="ee2c9-387">The local debug feature enables you to complete the following tasks before your code is submitted to Data Lake Analytics:</span></span> 
- <span data-ttu-id="ee2c9-388">偵錯您的 C# 程式碼後置。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-388">Debug your C# code-behind.</span></span> 
- <span data-ttu-id="ee2c9-389">逐步執行程式碼。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-389">Step through the code.</span></span> 
- <span data-ttu-id="ee2c9-390">在本機驗證您的指令碼。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-390">Validate your script locally.</span></span>

<span data-ttu-id="ee2c9-391">如需本機執行和本機偵錯的指示，請參閱[使用 Visual Studio Code 來進行 U-SQL 本機執行和本機偵錯](data-lake-tools-for-vscode-local-run-and-debug.md)。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-391">For instructions on local run and local debug, see [U-SQL local run and local debug with Visual Studio Code](data-lake-tools-for-vscode-local-run-and-debug.md).</span></span>

## <a name="additional-features"></a><span data-ttu-id="ee2c9-392">其他功能</span><span class="sxs-lookup"><span data-stu-id="ee2c9-392">Additional features</span></span>

<span data-ttu-id="ee2c9-393">Data Lake Tools for VSCode 支援下列功能︰</span><span class="sxs-lookup"><span data-stu-id="ee2c9-393">Data Lake Tools for VS Code supports the following features:</span></span>

-   <span data-ttu-id="ee2c9-394">IntelliSense 自動完成：關鍵字、方法和變數等項目周圍的快顯視窗會出現建議。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-394">IntelliSense auto-complete: Suggestions appear in pop-up windows around items, such as keywords, methods, and variables.</span></span> <span data-ttu-id="ee2c9-395">不同圖示代表不同類型的物件︰</span><span class="sxs-lookup"><span data-stu-id="ee2c9-395">Different icons represent different types of the objects:</span></span>

    - <span data-ttu-id="ee2c9-396">Scala 資料類型</span><span class="sxs-lookup"><span data-stu-id="ee2c9-396">Scala data type</span></span>
    - <span data-ttu-id="ee2c9-397">複雜資料類型</span><span class="sxs-lookup"><span data-stu-id="ee2c9-397">Complex data type</span></span>
    - <span data-ttu-id="ee2c9-398">內建 UDT</span><span class="sxs-lookup"><span data-stu-id="ee2c9-398">Built-in UDTs</span></span>
    - <span data-ttu-id="ee2c9-399">.NET 集合和類別</span><span class="sxs-lookup"><span data-stu-id="ee2c9-399">.NET collection and classes</span></span>
    - <span data-ttu-id="ee2c9-400">C# 運算式</span><span class="sxs-lookup"><span data-stu-id="ee2c9-400">C# expressions</span></span>
    - <span data-ttu-id="ee2c9-401">內建 C# UDF、UDO 和 UDAAG</span><span class="sxs-lookup"><span data-stu-id="ee2c9-401">Built-in C# UDFs, UDOs, and UDAAGs</span></span> 
    - <span data-ttu-id="ee2c9-402">U-SQL 函式</span><span class="sxs-lookup"><span data-stu-id="ee2c9-402">U-SQL functions</span></span>
    - <span data-ttu-id="ee2c9-403">U-SQL 時間範圍函式</span><span class="sxs-lookup"><span data-stu-id="ee2c9-403">U-SQL windowing function</span></span>
 
    ![Data Lake Tools for Visual Studio Code IntelliSense 物件類型](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-complete-objects.png)
 
-   <span data-ttu-id="ee2c9-405">Data Lake Analytics 中繼資料的 IntelliSense 自動完成：Data Lake Tools 會將 Data Lake Analytics 中繼資料資訊下載到本機。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-405">IntelliSense auto-complete on Data Lake Analytics metadata: Data Lake Tools downloads the Data Lake Analytics metadata information locally.</span></span> <span data-ttu-id="ee2c9-406">IntelliSense 功能會從 Data Lake Analytics 中繼資料自動填入物件，包括資料庫、結構描述、資料表、檢視、資料表值函式、程序和 C# 組件。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-406">The IntelliSense feature automatically populates objects, including the database, schema, table, view, table-valued function, procedures, and C# assemblies, from the Data Lake Analytics metadata.</span></span>
 
    ![Data Lake Tools for Visual Studio Code IntelliSense 中繼資料](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-complete-metastore.png)

-   <span data-ttu-id="ee2c9-408">IntelliSense 錯誤標記：Data Lake Tools 會為 U-SQL 和 C# 的編輯錯誤加上底線。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-408">IntelliSense error marker: Data Lake Tools underlines the editing errors for U-SQL and C#.</span></span> 
-   <span data-ttu-id="ee2c9-409">語法醒目提示：Data Lake Tools 會使用不同顏色來區分項目，例如變數、關鍵字、資料類型和函式。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-409">Syntax highlights: Data Lake Tools uses different colors to differentiate items, such as variables, keywords, data type, and functions.</span></span> 

    ![Data Lake Tools for Visual Studio Code 語法醒目顯示](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-syntax-highlights.png)

## <a name="next-steps"></a><span data-ttu-id="ee2c9-411">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ee2c9-411">Next steps</span></span>

- <span data-ttu-id="ee2c9-412">如需了解如何使用 Visual Studio Code 來進行 U-SQL 本機執行和本機偵錯，請參閱[使用 Visual Studio Code 來進行 U-SQL 本機執行和本機偵錯](data-lake-tools-for-vscode-local-run-and-debug.md)。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-412">For U-SQL local run and local debug with Visual Studio Code, see [U-SQL local run and local debug with Visual Studio Code](data-lake-tools-for-vscode-local-run-and-debug.md).</span></span>
- <span data-ttu-id="ee2c9-413">如需 Data Lake Analytics 的入門資訊，請參閱[教學課程︰開始使用 Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-413">For getting-started information on Data Lake Analytics, see [Tutorial: Get started with Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).</span></span>
- <span data-ttu-id="ee2c9-414">如需 Data Lake Tools for Visual Studio 的相關資訊，請參閱[教學課程：使用 Data Lake Tools for Visual Studio 開發 U-SQL 指令碼](data-lake-analytics-data-lake-tools-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-414">For information about Data Lake Tools for Visual Studio, see [Tutorial: Develop U-SQL scripts by using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
- <span data-ttu-id="ee2c9-415">如需有關開發組件的資訊，請參閱[針對 Azure Data Lake Analytics 作業開發 U-SQL 組件](data-lake-analytics-u-sql-develop-assemblies.md)。</span><span class="sxs-lookup"><span data-stu-id="ee2c9-415">For information on developing assemblies, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md).</span></span>



