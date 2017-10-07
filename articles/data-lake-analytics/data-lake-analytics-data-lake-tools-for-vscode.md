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
# <a name="use-azure-data-lake-tools-for-visual-studio-code"></a>使用 Azure Data Lake Tools for Visual Studio Code

了解如何 toouse Azure 資料湖 Tools for Visual Studio 程式碼 (VS Code) toocreate 測試，以及執行 U-SQL 指令碼。 下列視訊 hello 也涵蓋 hello 資訊：

<a href="https://www.youtube.com/watch?v=J_gWuyFnaGA&feature=youtu.be"><img src="./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-video.png"></a>

## <a name="prerequisites"></a>必要條件

資料湖工具可以安裝支援的 VS Code hello 平台上。 hello 支援平台包括 Windows、 Linux 及 MacOS。 hello 不同平台具有下列必要條件 hello:

- Windows

    - [Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx)。
    - [Java SE Runtime Environment version 8 update 77 或更新版本](https://java.com/download/manual.jsp)。 新增 hello java.exe toohello 系統環境變數的路徑。 組態指示，請參閱[如何設定或變更 hello Path 系統變數？]( https://www.java.com/download/help/path.xml)。 hello 路徑是類似 tooC:\Program Files\Java\jdk1.8.0_77\jre\bin。
    - [.NET Core SDK 1.0.3 或 .NET Core 1.1 執行階段](https://www.microsoft.com/net/download)。
    
- Linux (我們建議使用 Ubuntu 14.04 LTS)

    - [Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx)。 tooinstall hello 程式碼中，輸入下列命令的 hello:

              sudo dpkg -i code_<version_number>_amd64.deb

    - [Mono 4.2.x](http://www.mono-project.com/docs/getting-started/install/linux/)。 

        - tooupdate hello deb 套件來源中，輸入下列命令的 hello:

                sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
                echo "deb http://download.mono-project.com/repo/debian wheezy/snapshots 4.2.4.4/main" | sudo tee /etc/apt/sources.list.d/mono-xamarin.list
                sudo apt-get update

        - tooinstall Mono，輸入下列命令的 hello:

                sudo apt-get install mono-complete

            > [!NOTE] 
            > 不支援 Mono 4.6。 在安裝 4.2.x 之前，請先徹底解除安裝 4.6 版。  

        - [Java SE Runtime Environment version 8 update 77 或更新版本](https://java.com/download/manual.jsp)。 如需安裝指示，請參閱 hello [for Java 的 Linux 64 位元安裝指示]( https://java.com/en/download/help/linux_x64_install.xml)頁面。
        - [.NET Core SDK 1.0.3 或 .NET Core 1.1 執行階段](https://www.microsoft.com/net/download)。
- MacOS

    - [Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx)。
    - [Mono 4.2.4](http://download.mono-project.com/archive/4.2.4/macos-10-x86/)。 
    - [Java SE Runtime Environment version 8 update 77 或更新版本](https://java.com/download/manual.jsp)。 如需安裝指示，請參閱 hello [for Java 的 Linux 64 位元安裝指示](https://java.com/en/download/help/mac_install.xml)頁面。
    - [.NET Core SDK 1.0.3 或 .NET Core 1.1 執行階段](https://www.microsoft.com/net/download)。

## <a name="install-data-lake-tools"></a>安裝 Data Lake Tools

安裝 hello 必要條件之後，您可以安裝 Data Lake Tools VS 程式碼。

**tooinstall 資料湖工具**

1. 開啟 Visual Studio Code。
2. 選擇 Ctrl + P，，然後輸入 hello 下列命令：
```
ext install usql-vscode-ext
```
您可以看到一份 Visual Studio 程式碼擴充功能清單。 其中一個是 **Azure Data Lake Tools**。

3. 選取**安裝**下一步太**Azure Data Lake Tools**。 幾秒之後，hello**安裝**太按鈕變更**重新載入**。
4. 選取**重新載入**tooactivate hello 延伸模組。
5. 選取**確定**tooconfirm。 您可以在 hello 看到 Azure Data Lake Tools**延伸**窗格。
    ![Data Lake Tools for Visual Studio Code 擴充功能窗格](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extensions.png)

## <a name="activate-azure-data-lake-tools"></a>啟動 Azure Data Lake Tools
建立新的.usql 檔案或開啟現有.usql tooactivate hello 的副檔名。 

## <a name="connect-tooazure"></a>連接 tooAzure

您可以編譯並執行 Data Lake Analytics U-SQL 指令碼之前，您必須連接 tooyour Azure 帳戶。

**tooconnect tooAzure**

1.  選擇 Ctrl + Shift + P tooopen hello 命令選擇區。 
2.  輸入 **ADL: Login**。 hello 登入資訊會出現在 hello**輸出**窗格。

    ![Data Lake Tools for Visual Studio Code 命令選擇區](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login.png)
    ![Data Lake Tools for Visual Studio Code 裝置登入資訊](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-login-info.png)
3. 選擇 Ctrl + 按一下 hello 登入 URL: https://aka.ms/devicelogin tooopen hello 登入網頁。 輸入 hello 代碼**G567LX42V**到 hello 文字，然後再選取**繼續**。

   ![Data Lake Tools for Visual Studio Code 登入貼上代碼](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login-paste-code.png )   
4.  請依照中的 hello 指示 toosign hello 網頁。 您連線，您的 Azure 帳戶名稱會出現在 hello 狀態列中的 hello hello 左下角**VS Code**視窗。 

    > [!NOTE] 
    > 如果您的帳戶已啟用雙因素驗證，建議您使用電話驗證而非使用 PIN 碼。

out，toosign 輸入 hello 命令**ADL： 登出**。

## <a name="list-your-data-lake-analytics-accounts"></a>列出 Data Lake Analytics 帳戶

tootest hello 連線，get Data Lake Analytics 帳戶的清單。

**您的 Azure 訂用帳戶底下 toolist hello Data Lake Analytics 帳戶**

1. 選擇 Ctrl + Shift + P tooopen hello 命令選擇區。
2. 輸入 **ADL: List Accounts**。 hello 帳戶會出現在 hello**輸出**窗格。

## <a name="open-hello-sample-script"></a>開啟 hello 範例指令碼
開啟 hello 命令選擇區 (Ctrl + Shift + P)，並輸入**ADL： 開啟範例指令碼**。 這會開啟此範例的另一個執行個體。 您也可以在此執行個體上編輯、設定及提交指令碼。

## <a name="work-with-u-sql"></a>使用 U-SQL

您需要使用 U-SQL 開啟 U-SQL 檔案或資料夾 toowork。

**tooopen U-SQL 專案的資料夾**

1. 從 Visual Studio 程式碼中，選取 [hello**檔案**] 功能表，然後選取**開啟資料夾**。
2. 指定資料夾，然後選取 [選取資料夾]。
3. 選取 hello**檔案** 功能表，然後選取**新增**。 未命名 1 檔案會加入 toohello 專案。
4. 輸入下列程式碼到 hello 未命名 1 檔案 hello:

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

    hello 指令碼會建立 departments.csv 檔案以包含在 hello /output 資料夾中特定資料。

5. 將 hello 檔案儲存為**myUSQL.usql** hello 中開啟資料夾。 Adltools_settings.json 組態檔也會加入 toohello 專案。
4. 開啟並設定 adltools_settings.json 以 hello 下列屬性：

    - 帳戶：在您的 Azure 訂用帳戶下的 Data Lake Analytics 帳戶。
    - 資料庫：您帳戶底下的資料庫。 hello 預設值是**主要**。
    - 結構描述：您資料庫底下的結構描述。 hello 預設值是**dbo**。
    - 選擇性設定︰
        - 優先順序： hello 優先順序範圍是從 1 too1000 1 為 hello 最高優先權。 hello 預設值是**1000年**。
        - 平行處理原則： hello 平行處理原則的範圍是從 1 too150。 hello 預設值為 hello Azure Data Lake Analytics 帳戶中允許的最大平行處理。 
        
        > [!NOTE] 
        > 如果 hello 設定無效，則會使用 hello 預設值。

    ![Data Lake Tools for Visual Studio Code 組態檔](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-configuration-file.png)

    Data Lake Analytics 帳戶是計算需要 toocompile，並執行 U-SQL 工作。 您可以編譯及執行 U SQL 作業之前，您必須設定 hello 電腦帳戶。
    
儲存 hello 組態之後，hello 帳戶、 資料庫和結構描述資訊出現在 hello 狀態列 hello 左下角的 hello 對應.usql 檔案。 
 
 
比較的 tooopening 檔案，當您開啟的資料夾，您可以：

- 使用程式碼後置檔案。 在 hello 單一檔案模式中，不支援程式碼後置。
- 使用組態檔。 當您開啟資料夾時，hello 工作資料夾中的 hello 指令碼會共用單一設定檔。


hello U-SQL 指令碼會編譯從遠端透過 hello 資料湖分析服務。 當您發出 hello**編譯**命令 hello U-SQL 指令碼會傳送 tooyour Data Lake Analytics 帳戶。 更新版本中，Visual Studio 程式碼會收到 hello 編譯結果。 由於 toohello 遠端編譯，Visual Studio 程式碼需要您列出 hello tooconnect tooyour hello 組態檔中的 Data Lake Analytics 帳戶的資訊。

**toocompile U-SQL 指令碼**

1. 選擇 Ctrl + Shift + P tooopen hello 命令選擇區。 
2. 輸入 **ADL: Compile Script**。 hello 編譯結果會出現在 hello**輸出**視窗。 您可以也在指令碼檔案，以滑鼠右鍵按一下，然後選取**ADL： 編譯指令碼**toocompile U SQL 作業。 hello 編譯結果會出現在 hello**輸出**窗格。
 

**toosubmit U-SQL 指令碼**

1. 選擇 Ctrl + Shift + P tooopen hello 命令選擇區。 
2. 輸入 **ADL: Submit Job**。  您也可以在指令碼檔案上按一下滑鼠右鍵，然後選取 [ADL: Submit Job]。 

Hello 送出記錄檔送出 U-SQL 工作後，會出現在 hello**輸出**VS 程式碼中的視窗。 如果 hello 提交成功，hello 工作 URL 也會出現。 您可以開啟 hello 工作 URL 中的 web 瀏覽器 tootrack hello 即時作業狀態。

設定 tooenable hello 輸出 hello 工作詳細資料， **jobInformationOutputPath**在 hello **vs 程式碼 hello u sql_settings.json**檔案。
 
## <a name="use-a-code-behind-file"></a>使用程式碼後置檔案

程式碼後置檔案是與單一 U-SQL 指令碼關聯的 C# 檔案。 您可以定義指令碼專用 tooUDO、 UDA、 UDT 和 UDF hello 程式碼後置檔案中。 hello UDO、 UDA、 UDT 和 UDF 可直接在 hello 指令碼而不先註冊 hello 組件。 hello 程式碼後置檔案放在 hello 相同為其對等互連的 U-SQL 指令碼檔案的資料夾。 如果 hello 指令碼為 xxx.usql，hello 程式碼後置會稱為 xxx.usql.cs。 如果您以手動方式刪除 hello 程式碼後置檔案，其相關聯的 U-SQL 指令碼的 hello 程式碼後置功能已停用。 如需撰寫 U-SQL 指令碼之客戶程式碼的詳細資訊，請參閱[在 U-SQL 中撰寫並使用自訂程式碼：使用者定義函式]( https://blogs.msdn.microsoft.com/visualstudio/2015/10/28/writing-and-using-custom-code-in-u-sql-user-defined-functions/) (英文)。

toosupport 程式碼後置，您必須開啟工作資料夾。 

**toogenerate 程式碼後置檔案**

1. 開啟來源檔案。 
2. 選擇 Ctrl + Shift + P tooopen hello 命令選擇區。
3. 輸入 **ADL: Generate Code Behind**。 程式碼後置檔案中建立 hello 相同資料夾。 

您也可以在指令碼檔案上按一下滑鼠右鍵，然後選取 [ADL: Generate Code Behind]。 

toocompile 並提交 U-SQL 指令碼的程式碼後置檔案是 hello 相同與 hello 獨立 U-SQL 指令碼檔案。

hello 下列兩個螢幕擷取畫面顯示程式碼後置檔案和其相關聯的 U-SQL 指令碼檔案：
 
![Data Lake Tools for Visual Studio Code 程式碼後置](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-code-behind.png)

![Data Lake Tools for Visual Studio Code 程式碼後置指令碼檔案](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-code-behind-call.png) 

## <a name="use-assemblies"></a>使用組件

如需有關開發組件的資訊，請參閱[針對 Azure Data Lake Analytics 作業開發 U-SQL 組件](data-lake-analytics-u-sql-develop-assemblies.md)。

您可以使用 Data Lake Tools tooregister 自訂程式碼組件 hello Data Lake Analytics 類別目錄中。

**tooregister 組件**

您可以註冊 hello 組件透過 hello **ADL： 註冊組件**或**ADL： 註冊組件，透過組態**命令。

**透過 hello ADL tooregister： 註冊組件命令**
1.  選擇 Ctrl + Shift + P tooopen hello 命令選擇區。
2.  輸入 **ADL: Register Assembly**。 
3.  指定 hello 本機組件路徑。 
4.  選取 Data Lake Analytics 帳戶。
5.  選取資料庫。

結果： hello 入口網站會在瀏覽器中開啟，並顯示 hello 組件註冊程序。  

另一個便利的方式 tootrigger hello **ADL： 註冊組件**命令是在檔案總管中的 tooright 按一下 hello.dll 檔案。 

**tooregister 雖然 hello ADL： 註冊組件，透過組態命令**
1.  選擇 Ctrl + Shift + P tooopen hello 命令選擇區。
2.  輸入 **ADL: Register Assembly through Configuration**。 
3.  指定 hello 本機組件路徑。 
4.  會顯示 hello JSON 檔案。 檢閱並視需要編輯 hello 組件相依性及資源參數。 指示會顯示在 hello**輸出**視窗。 tooproceed toohello 組件註冊，(Ctrl + S) hello JSON 檔案儲存。

![Data Lake Tools for Visual Studio Code 程式碼後置](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-register-assembly-advance.png)
>[!NOTE]
>- 組件相依性： Azure Data Lake Tools autodetects hello DLL 是否有任何相依性。 hello 相依性會顯示 hello JSON 檔案中之後就會偵測衝突。 
>- 資源： 您可以將上傳您 DLL 的資源 （例如.txt、.png 和.csv） hello 組件註冊的一部分。 

另一個方式 tootrigger hello **ADL： 註冊組件，透過組態**命令是在檔案總管中的 tooright 按一下 hello.dll 檔案。 

hello 遵循 U SQL 程式碼示範如何 toocall 組件。 在 hello 範例 hello 組件名稱是*測試*。

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


## <a name="access-hello-data-lake-analytics-catalog"></a>存取 hello Data Lake Analytics 類別目錄

連接 tooAzure 之後，您可以使用下列步驟 tooaccess hello U-SQL 目錄 hello。

**tooaccess hello Azure Data Lake Analytics 中繼資料**

1.  選取 Ctrl+Shift+P，然後輸入 **ADL: List Tables**。
2.  選取其中一個 hello Data Lake Analytics 帳戶。
3.  選取其中一個 hello 資料湖分析資料庫。
4.  選取其中一個 hello 結構描述。 您可以看到 hello 的資料表清單。

## <a name="view-data-lake-analytics-jobs"></a>檢視 Data Lake Analytics 作業

**tooview Data Lake Analytics 工作**
1.  開啟 hello 命令選擇區 (Ctrl + Shift + P)，然後選取**ADL： 顯示工作**。 
2.  選取 Data Lake Analytics 帳戶或本機帳戶。 
3.  等候 hello 帳戶 tooappear hello 工作清單。
4.  從工作清單中選取的作業，資料湖工具在 hello Azure 入口網站中開啟 hello 工作詳細資料，並顯示 VS 程式碼中的 hello JobInfo 檔案。

![Data Lake Tools for Visual Studio Code IntelliSense 物件類型](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-show-job.png)

## <a name="azure-data-lake-storage-integration"></a>Azure Data Lake Storage 整合

您可以使用 Azure Data Lake Storage 相關命令來進行下列作業：
 - 瀏覽 hello Azure 資料湖存放區資源。 
 - 預覽 hello Azure 資料湖存放區檔案。  
 - 上傳 hello 檔案與程式碼中直接 tooAzure 資料湖存放區。 

### <a name="list-hello-storage-path"></a>清單 hello 儲存體路徑 
您可以列出透過 hello 命令選擇區或以滑鼠右鍵按一下 hello 儲存路徑。

**透過 hello 命令選擇區 toolist hello 儲存路徑**

1.  開啟 hello 命令選擇區 (Ctrl + Shift + P)，並輸入**ADL： 清單存放路徑**。

    ![Data Lake Tools for Visual Studio Code 列出儲存體路徑](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-storage.png)

2.  選取您慣用的方法，以列出 hello 儲存路徑。 本段使用 [Enter a path] \(輸入路徑\) 作為範例。

    ![Visual Studio Code 其中一種方式 toolist hello 儲存路徑的資料湖工具](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account-selectoneway.png)

    > [!NOTE]
    >- VS Code 的每個 Data Lake Analytics 帳戶中保留 hello 上次造訪的路徑。 例如：/tt/ss。
    >- 瀏覽器從根路徑： hello 清單根路徑，從選取的資料湖分析帳戶或本機路徑。
    >- 輸入路徑：從所選 Data Lake Analytics 帳戶或本機路徑列出指定的路徑。
    
3. 選取從 hello 本機路徑或 Data Lake Analytics 帳戶的帳戶。

    ![Data Lake Tools for Visual Studio Code 選取更多](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

4. 選取**詳細**toolist 詳細資料湖分析帳戶，然後選取 Data Lake Analytics 帳戶。

    ![Data Lake Tools for Visual Studio Code 選取一個帳戶](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-select-adla-account.png)

5.  輸入 Azure 儲存體路徑。 例如，/output。

    ![Data Lake Tools for Visual Studio Code 輸入儲存體路徑](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-path.png)

6.  結果： hello 命令選擇區列出根據項目 hello 路徑資訊。

    ![Data Lake Tools for Visual Studio Code 列出儲存體路徑結果](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-path.png)

Toolist hello 相對路徑是透過 hello 較方便的方式上按一下滑鼠右鍵內容功能表。

**透過 toolist hello 儲存路徑上按一下滑鼠右鍵**

1.  以滑鼠右鍵按一下 hello 路徑字串 tooselect**清單存放路徑**。

       ![Data Lake Tools for Visual Studio Code 右鍵快顯功能表](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-right-click-path.png)

2. hello 選相對路徑會出現在 hello 命令選擇區。

   ![Data Lake Tools for Visual Studio Code 選取的相對路徑](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-relative-path.png)

3.  選取從 hello 本機路徑或 Data Lake Analytics 帳戶的帳戶。

       ![Data Lake Tools for Visual Studio Code 選取一個帳戶](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

4.  結果： hello 命令選擇區列出 hello 資料夾和檔案 hello 目前路徑。

       ![Visual Studio 程式碼清單 hello 目前路徑中的資料湖工具](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-current.png)

### <a name="preview-hello-storage-file"></a>預覽 hello 儲存體檔案
您可以預覽 hello 透過 hello 命令選擇區或以滑鼠右鍵按一下儲存體檔案。

**透過 hello 命令選擇區 toopreview hello 儲存體檔案**

1.  開啟 hello 命令選擇區 (Ctrl + Shift + P)，並輸入**ADL： 預覽儲存體檔案**。

       ![Data Lake Tools for Visual Studio Code 預覽儲存體檔案](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-preview.png)

2.  選取從 hello 本機路徑或 Data Lake Analytics 帳戶的帳戶。

       ![Data Lake Tools for Visual Studio Code 列出帳戶](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

3.  選取**詳細**toolist 詳細資料湖分析帳戶，然後選取 Data Lake Analytics 帳戶。

       ![Data Lake Tools for Visual Studio Code 選取一個帳戶](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-select-adla-account.png)

4.  輸入 Azure 儲存體路徑或檔案。 例如：/output/SearchLog.txt。

       ![Data Lake Tools for Visual Studio Code 輸入儲存體路徑和檔案](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-preview-file.png)

5.  結果： hello 命令選擇區列出根據項目 hello 路徑資訊。

       ![Data Lake Tools for Visual Studio Code 預覽檔案結果](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-preview-results.png)

**透過 toolist hello 儲存路徑上按一下滑鼠右鍵**

1.  toopreview 檔案，以滑鼠右鍵按一下 hello 檔案路徑。

   ![Data Lake Tools for Visual Studio Code 右鍵快顯功能表](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-right-click-preview.png) 

2.  選取從 hello 本機路徑或 Data Lake Analytics 帳戶的帳戶。

       ![Data Lake Tools for Visual Studio Code 選取一個帳戶](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

3.  結果： VS 程式碼會顯示 hello 檔案 hello 預覽結果。

       ![Data Lake Tools for Visual Studio Code 預覽檔案結果](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-preview-results.png)

### <a name="upload-a-file"></a>上傳檔案 

您可以將檔案上傳輸入 hello 命令**ADL： 上傳檔案**或**ADL： 上傳的檔案，透過組態**。

**tooupload 檔案雖然 hello ADL： 上傳檔案命令**
1. 選取 Ctrl + Shift + P tooopen hello 命令選擇區或 hello 指令碼編輯器 中，以滑鼠右鍵按一下，然後輸入**上傳檔案**。
2.  tooupload hello 檔案中，輸入本機路徑。

    ![Data Lake Tools for Visual Studio Code 輸入本機路徑](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-input-local-path.png)

3. 選取其中一種清單 hello 儲存路徑的 hello。 本段使用 [Enter a path] \(輸入路徑\) 作為範例。

    ![Data Lake Tools for Visual Studio Code 列出儲存體路徑](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account-selectoneway.png)
    >[!NOTE]
    >- VS Code 的每個 Data Lake Analytics 帳戶中保留 hello 上次造訪的路徑。 例如：/tt/ss。
    >- 瀏覽器從根路徑： hello 清單根路徑，從選取的資料湖分析帳戶或本機路徑。
    >- 輸入路徑：從所選 Data Lake Analytics 帳戶或本機路徑列出指定的路徑。

4. 選取從 hello 本機路徑或 Data Lake Analytics 帳戶的帳戶。

    ![Data Lake Tools for Visual Studio Code 在儲存體上按一下滑鼠右鍵](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

5. 輸入 Azure 儲存體路徑。 例如：/output。

       ![Data Lake Tools for Visual Studio Code enter storage path](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-preview-file.png)

6. 找出您的 Azure 儲存體路徑。 選取 [Choose current folder] \(選擇目前的資料夾\)。

    ![Data Lake Tools for Visual Studio Code 選取資料夾](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-choose-current-folder.png)

7.  結果： hello**輸出**視窗會顯示 hello 檔案上傳狀態。

       ![Data Lake Tools for Visual Studio Code 上傳狀態](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-status.png)    

**tooupload 檔案雖然 hello ADL： 上傳的檔案，透過組態命令**
1.  選取 Ctrl + Shift + P tooopen hello 命令選擇區或 hello 指令碼編輯器 中，以滑鼠右鍵按一下，然後輸入**上傳的檔案，透過組態**。
2.  VS Code 會顯示一個 JSON 檔案。 您可以輸入檔案路徑，然後在 hello 的多個檔案上傳相同的時間。 指示會顯示在 hello**輸出**視窗。 tooproceed tooupload hello 檔案、 儲存 (Ctrl + S) hello JSON 檔案。

       ![Data Lake Tools for Visual Studio Code 檔案路徑](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-file.png)

3.  結果： hello**輸出**視窗會顯示 hello 檔案上傳狀態。

       ![Data Lake Tools for Visual Studio Code 上傳狀態](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-status.png)     

另一個方式 tooupload 檔案 toostorage 是透過 hello 上按一下滑鼠右鍵功能表 hello 檔案的完整路徑或 hello 指令碼編輯器中的 hello 檔案的相對路徑。 輸入 hello 本機檔案路徑，然後再選取 hello 帳戶。 hello**輸出**視窗會顯示 hello 上傳狀態。 

### <a name="open-azure-storage-explorer"></a>開啟 Azure 儲存體總管
您可以開啟**Azure 儲存體總管**輸入 hello 命令**ADL： 開啟 Web Azure 儲存體總管**或從 hello 以滑鼠右鍵按一下內容功能表中選取它。

**tooopen Azure 儲存體總管**

1. 選擇 Ctrl + Shift + P tooopen hello 命令選擇區。
2. 輸入**開啟 Web Azure 儲存體總管**或相對路徑或 hello 在 hello 指令碼編輯器中，完整的路徑上按一下滑鼠右鍵，然後選取**開啟 Web Azure 儲存體總管**。
3. 選取 Data Lake Analytics 帳戶。

資料湖工具會在 hello Azure 入口網站中開啟 hello Azure 儲存體路徑。 您可以找到從 hello web hello 路徑和預覽 hello 檔案。

### <a name="local-run-and-local-debug-for-windows-users"></a>Windows 使用者的本機執行和本機偵錯
執行的 U-SQL 本機測試您的本機資料和已發行的 tooData 湖分析您的程式碼之前驗證指令碼在本機。 hello 本機偵錯功能可讓您 toocomplete hello 下列工作，您的程式碼之前提交 tooData 湖分析： 
- 偵錯您的 C# 程式碼後置。 
- 逐步執行 hello 程式碼。 
- 在本機驗證您的指令碼。

如需本機執行和本機偵錯的指示，請參閱[使用 Visual Studio Code 來進行 U-SQL 本機執行和本機偵錯](data-lake-tools-for-vscode-local-run-and-debug.md)。

## <a name="additional-features"></a>其他功能

VS Code 的資料湖工具支援下列功能的 hello:

-   IntelliSense 自動完成：關鍵字、方法和變數等項目周圍的快顯視窗會出現建議。 不同的圖示代表不同類型的 hello 物件：

    - Scala 資料類型
    - 複雜資料類型
    - 內建 UDT
    - .NET 集合和類別
    - C# 運算式
    - 內建 C# UDF、UDO 和 UDAAG 
    - U-SQL 函式
    - U-SQL 時間範圍函式
 
    ![Data Lake Tools for Visual Studio Code IntelliSense 物件類型](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-complete-objects.png)
 
-   IntelliSense 自動完成 Data Lake Analytics 中繼資料： 資料湖工具下載 hello Data Lake Analytics 中繼資料資訊在本機。 hello IntelliSense 功能會自動填入物件，包括 hello 資料庫、 結構描述、 資料表、 檢視、 資料表值函數、 程序和 C# 組件，從 hello Data Lake Analytics 中繼資料。
 
    ![Data Lake Tools for Visual Studio Code IntelliSense 中繼資料](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-complete-metastore.png)

-   IntelliSense 錯誤標記： Data Lake Tools 加上底線 hello 編輯 U SQL 和 C# 的錯誤。 
-   語法醒目提示： Data Lake Tools 會使用不同的色彩 toodifferentiate 項目，例如變數、 關鍵字、 資料類型和函數。 

    ![Data Lake Tools for Visual Studio Code 語法醒目顯示](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-syntax-highlights.png)

## <a name="next-steps"></a>後續步驟

- 如需了解如何使用 Visual Studio Code 來進行 U-SQL 本機執行和本機偵錯，請參閱[使用 Visual Studio Code 來進行 U-SQL 本機執行和本機偵錯](data-lake-tools-for-vscode-local-run-and-debug.md)。
- 如需 Data Lake Analytics 的入門資訊，請參閱[教學課程︰開始使用 Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md)。
- 如需 Data Lake Tools for Visual Studio 的相關資訊，請參閱[教學課程：使用 Data Lake Tools for Visual Studio 開發 U-SQL 指令碼](data-lake-analytics-data-lake-tools-get-started.md)。
- 如需有關開發組件的資訊，請參閱[針對 Azure Data Lake Analytics 作業開發 U-SQL 組件](data-lake-analytics-u-sql-develop-assemblies.md)。



