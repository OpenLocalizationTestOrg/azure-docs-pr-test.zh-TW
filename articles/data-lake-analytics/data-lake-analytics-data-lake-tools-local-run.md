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
# <a name="test-and-debug-u-sql-jobs-by-using-local-run-and-hello-azure-data-lake-u-sql-sdk"></a>測試與偵錯使用本機執行和 hello Azure 資料湖 U-SQL SDK U SQL 作業

您可以使用 Azure 資料湖 Tools for Visual Studio 和 hello Azure 資料湖 U-SQL SDK toorun U SQL 作業在您的工作站一樣，您可以在 hello Azure 資料湖服務。 這兩個本機執行功能可節省您對 U-SQL 作業進行測試和偵錯的時間。

## <a name="understand-hello-data-root-folder-and-hello-file-path"></a>了解 hello 資料根資料夾和 hello 檔案路徑

本機執行和 hello U-SQL SDK 需要資料根資料夾。 hello 資料根資料夾是 hello 本機計算帳戶 「 本機存放區 」。 它是 Data Lake Analytics 帳戶的對等 toohello Azure Data Lake Store 帳戶。 切換 tooa 不同的資料根資料夾，就如同切換 tooa 不同儲存體帳戶。 如果您想 tooaccess 共用資料使用不同的資料根資料夾，您必須在您的指令碼中使用絕對路徑。 或者，建立檔案系統中的符號連結 (比方說， **mklink**上 NTFS) 下 hello 資料根資料夾 toopoint toohello 共用資料。

hello 資料根資料夾用來：

- 儲存中繼資料，包括資料庫、資料表，資料表值函式 (TVF)，以及組件。
- 查閱 hello 輸入和輸出路徑定義為 U SQL 中的相對路徑。 使用相對路徑會更容易 toodeploy 您 U-SQL 專案 tooAzure。

您可以在 U-SQL 指令碼中使用相對路徑和本機絕對路徑。 hello 相對路徑是相對 toohello 指定的資料根資料夾路徑。 我們建議您使用"/"作為 hello 路徑分隔符號 toomake 相容 hello 伺服器端指令碼。 以下是一些相對路徑及其對等絕對路徑的範例。 在這些範例中，C:\LocalRunDataRoot 會為 hello 資料根資料夾。

|相對路徑|絕對路徑|
|-------------|-------------|
|/abc/def/input.csv |C:\LocalRunDataRoot\abc\def\input.csv|
|abc/def/input.csv  |C:\LocalRunDataRoot\abc\def\input.csv|
|D:/abc/def/input.csv |D:\abc\def\input.csv|

## <a name="use-local-run-from-visual-studio"></a>從 Visual Studio 使用本機執行

Data Lake Tools for Visual Studio 提供 Visual Studio 中的 U-SQL 本機執行體驗。 透過使用這項功能，您可以︰

- 在本機執行 U-SQL 指令碼及 C# 組件。
- 在本機對 C# 組件進行偵錯。
- 從伺服器總管建立、檢視和刪除 U-SQL 目錄 (本機資料庫、組件、結構描述和資料表)。 您也可以從 [伺服器總管] 也尋找 hello 本機類別目錄。

    ![Data Lake Tools for Visual Studio 本機執行的本機目錄](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-local-catalog.png)

hello 資料湖工具安裝程式會建立做為 hello 預設資料根目錄資料夾 C:\LocalRunRoot 資料夾 toobe。 hello 預設本機執行平行處理原則是 1。

### <a name="tooconfigure-local-run-in-visual-studio"></a>tooconfigure 本機 Visual Studio 中執行

1. 開啟 Visual Studio。
2. 開啟 [伺服器總管]。
3. 展開 [Azure]  >  [Data Lake Analytics]。
4. 按一下 hello **Data Lake**功能表，然後再按一下**選項和設定**。
5. 在 hello 左邊樹狀目錄中，展開**Azure 資料湖**，然後展開**一般**。

    ![Data Lake Tools for Visual Studio 本機執行的組態設定](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-configure.png)

必須要有 Visual Studio U-SQL 專案才能執行本機執行。 這與從 Azure 執行 U-SQL 指令碼不同。

### <a name="toorun-a-u-sql-script-locally"></a>在本機 toorun U-SQL 指令碼
1. 從 Visual Studio 開啟您的 U-SQL 專案。   
2. 在 方案總管 中的 U-SQL 指令碼上按一下滑鼠右鍵，然後按一下提交指令碼。
3. 選取**（本機）**身分 hello Analytics 帳戶 toorun 指令碼在本機。
您也可以按一下 hello **（本機）** hello 指令碼視窗頂端的帳戶，然後按一下**送出**（或使用 hello Ctrl + F5 鍵盤快速鍵）。

    ![Data Lake Tools for Visual Studio 本機執行的提交作業](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-submit-job.png)

### <a name="debug-scripts-and-c-assemblies-locally"></a>在本機偵錯指令碼和 C# 組件

您可以偵錯 C# 組件，而送出，並註冊它 tooAzure 資料湖分析服務。 在這兩個的 hello 程式碼後置檔案中，以及參考的 C# 專案中，您可以設定中斷點。

#### <a name="toodebug-local-code-in-code-behind-file"></a>在程式碼後置檔案 toodebug 本機的程式碼

1. Hello 程式碼後置檔案中設定中斷點。
2. 按 F5 toodebug hello 指令碼在本機。

> [!NOTE]
   > 下列程序只適用於 Visual Studio 2015 中的 hello。 在舊版的 Visual Studio 中，您可能需要 toomanually 新增 hello pdb 檔案。  
   >
   >

#### <a name="toodebug-local-code-in-a-referenced-c-project"></a>toodebug 本機程式碼中參考的 C# 專案

1. 建立 C# 組件的專案，並建立該 toogenerate hello 輸出 dll 檔案。
2. 註冊 hello dll 使用 U SQL 陳述式：

        CREATE ASSEMBLY assemblyname FROM @"..\..\path\to\output\.dll";
        
3. Hello C# 程式碼中設定中斷點。
4. 按 F5 toodebug hello 指令碼以參考本機 hello C# dll。

## <a name="use-local-run-from-hello-data-lake-u-sql-sdk"></a>使用本機執行從 hello 資料湖 U-SQL SDK

此外 toorunning U-SQL 指令碼在本機上使用 Visual Studio，您可以使用命令列和程式設計介面，在本機使用 hello Azure 資料湖 U-SQL SDK toorun U-SQL 指令碼。 這能讓您調整 U-SQL 本機測試。

深入了解 [Azure Data Lake U-SQL SDK](data-lake-analytics-u-sql-sdk.md)。


## <a name="next-steps"></a>後續步驟

* toosee 更複雜的查詢，請參閱[分析網站記錄檔，使用 Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md)。
* tooview 作業的詳細資訊，請參閱[使用作業瀏覽器和 Azure Data Lake Analytics 工作的工作檢視](data-lake-analytics-data-lake-tools-view-jobs.md)。
* toouse hello 頂點執行檢視，請參閱[使用 hello 頂點資料湖 Tools for Visual Studio 中的執行檢視](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md)。
