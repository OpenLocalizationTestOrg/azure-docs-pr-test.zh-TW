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
# <a name="debug-user-defined-c-code-for-failed-u-sql-jobs"></a>對 U-SQL 失敗作業的使用者定義 C# 程式碼進行偵錯

U-SQL 提供使用 C# 中，所以您可以撰寫您的程式碼 tooadd 功能，例如自訂擷取程式 」 或減壓器的擴充性模型。 詳細資訊，請參閱 toolearn [U-SQL 程式設計指南](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-u-sql-programmability-guide#use-user-defined-functions-udf)。 在實務上，任何程式碼都可能需要偵錯，而且巨量資料系統可能僅提供有限的執行階段偵錯資訊，例如記錄檔。

Azure 資料湖 Tools for Visual Studio 提供的功能，稱為**無法偵錯頂點**，可讓您複製失敗的作業，從 偵錯的 hello 雲端 tooyour 本機電腦。 hello 本機複本擷取 hello 整個雲端環境，包括任何輸入的資料和使用者程式碼。

hello 下列影片示範失敗頂點偵錯在 Azure Data Lake Tools for Visual Studio。

> [!VIDEO https://e0d1.wpc.azureedge.net/80E0D1/OfficeMixProdMediaBlobStorage/asset-d3aeab42-6149-4ecc-b044-aa624901ab32/b0fc0373c8f94f1bb8cd39da1310adb8.mp4?sv=2012-02-12&sr=c&si=a91fad76-cfdd-4513-9668-483de39e739c&sig=K%2FR%2FdnIi9S6P%2FBlB3iLAEV5pYu6OJFBDlQy%2FQtZ7E7M%3D&se=2116-07-19T09:27:30Z&rscd=attachment%3B%20filename%3DDebugyourcustomcodeinUSQLADLA.mp4]
>

> [!NOTE]
> 如果尚未安裝，visual Studio 需要下列兩個更新，hello: [Microsoft Visual c + + 2015年可轉散發套件 Update 3](https://www.microsoft.com/en-us/download/details.aspx?id=53840)和[通用 C 執行階段的 Windows](https://www.microsoft.com/download/details.aspx?id=50410)。

## <a name="download-failed-vertex-toolocal-machine"></a>下載失敗頂點 toolocal 機器

當您開啟失敗的作業在 Azure Data Lake Tools for Visual Studio 時，您會看到一個警示的黃色列，hello 錯誤 索引標籤中的詳細的錯誤訊息。

1. 按一下**下載**toodownload 所有 hello 必要資源和輸入資料流。 如果 hello 下載未完成，請按一下**重試**。

2. 按一下**開啟**hello 下載完成 toogenerate 本機偵錯環境之後。 隨即會自動建立並開啟具有偵錯方案的新 Visual Studio 執行個體。

![Azure Data Lake Analytics U-SQL 偵錯 Visual Studio 下載 Vertex](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-download-vertex.png)

作業可能會包含程式碼後置原始程式檔或已註冊的組件，且這兩種類型有不同的偵錯案例。

- [偵錯程式碼後置失敗的作業](#debug-job-failed-with-code-behind)
- [偵錯組件失敗的作業](#debug-job-failed-with-assemblies)


## <a name="debug-job-failed-with-code-behind"></a>偵錯程式碼後置失敗的作業

如果 U SQL 作業失敗，而且 hello 作業會包括使用者程式碼 (通常會命名為`Script.usql.cs`U-SQL 專案中)，程式碼會匯入解決方案進行偵錯的 hello。  您可以從該處使用 hello Visual Studio 偵錯工具 （監看式、 變數等） tootroubleshoot hello 問題。

> [!NOTE]
> 偵錯之前，要確定 toocheck **Common Language Runtime 例外**hello 例外狀況設定視窗中 (**Ctrl + Alt + E**)。

![Azure Data Lake Analytics U-SQL 偵錯 Visual Studio 設定](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-clr-exception-setting.png)

1. 按**F5** toorun hello 程式碼後置程式碼。 它會一直執行到被例外狀況停止為止。

2. 開啟 hello`ADLTool_Codebehind.usql.cs`檔案，並設定中斷點，然後按下**F5** toodebug hello 程式碼逐步解說。

    ![Azure Data Lake Analytics U-SQL 偵錯例外狀況](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-debug-exception.png)

## <a name="debug-job-failed-with-assemblies"></a>偵錯組件失敗的作業

如果您使用已註冊組件 U-SQL 指令碼中，hello 系統無法自動取得 hello 原始程式碼。 在此情況下，手動新增 hello 組件的來源檔案 toohello 方案的 code。

### <a name="configure-hello-solution"></a>設定 hello 解決方案

1. 以滑鼠右鍵按一下**方案 'VertexDebug' > 新增 > 現有專案...** toofind hello 組件的原始程式碼，並加入 hello 專案 toohello 方案進行偵錯。

    ![Azure Data Lake Analytics U-SQL 偵錯新增專案](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-add-project-to-debug-solution.png)

2. 以滑鼠右鍵按一下**LocalVertexHost > 屬性**在 hello 方案，並複製 hello**工作目錄**路徑。

3. 以滑鼠右鍵按一下**組件原始程式碼專案 > 屬性**，選取 hello**建置**索引標籤上，在左邊，並貼上複製的 hello 路徑做為**輸出 > 輸出路徑**。

    ![Azure Data Lake Analytics U-SQL 偵錯設定 pdb 路徑](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-set-pdb-path.png)

4. 按 **Ctrl + Alt + E**，核取 [例外狀況設定] 視窗中的 [Common Language Runtime 例外狀況]。

### <a name="start-debug"></a>開始偵錯

1. 以滑鼠右鍵按一下**組件原始程式碼專案 > 重建**toooutput.pdb 檔案 toohello`LocalVertexHost`工作目錄。

2. 按**F5** hello 專案將會執行直到它已停止的例外狀況。 您可能會看到下列警告訊息，您可以放心忽略 hello。 它可能會佔用 tooa 分鐘 tooget toohello 偵錯螢幕。

    ![Azure Data Lake Analytics U-SQL 偵錯 Visual Studio 警告](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-visual-studio-u-sql-debug-warning.png)

3. 開啟您的原始程式碼，並設定中斷點，然後按下**F5** toodebug hello 程式碼逐步解說。

您也可以使用 hello Visual Studio 偵錯工具 （監看式、 變數等） tootroubleshoot hello 問題。

> [!NOTE]
> 每次修改 hello toogenerate 更新.pdb 檔案之後重建 hello 組件來源的程式碼專案。

偵錯之後，如果成功完成 hello 專案 hello [輸出] 視窗會顯示下列訊息的 hello:

```
hello Program 'LocalVertexHost.exe' has exited with code 0 (0x0).
```

![Azure Data Lake Analytics U-SQL 偵錯成功](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-debug-succeed.png)

## <a name="resubmit-hello-job"></a>再重新送出 hello 工作

當您完成偵錯時，再重新送出 hello 失敗的作業。

1. 工作與程式碼後置解決方案、 C# 程式碼複製到 hello 程式碼後置原始程式檔 (通常`Script.usql.cs`)。
2. 使用組件的工作、 註冊 ADLA 資料庫 hello 更新.dll 組件：
    1. 從伺服器總管或 Cloud Explorer 中，展開 hello **ADLA 帳戶 > 資料庫**節點。
    2. 以滑鼠右鍵按一下**組件**並註冊新的.dll 組件以 hello ADLA 資料庫： ![Azure 資料湖分析 U-SQL 偵錯註冊組件](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-register-assembly.png)
3. 重新提交您的作業。

## <a name="next-steps"></a>後續步驟

- [U-SQL 可程式性指南](data-lake-analytics-u-sql-programmability-guide.md)
- [針對 Azure Data Lake Analytics 作業開發 U-SQL 使用者定義運算子](data-lake-analytics-u-sql-develop-user-defined-operators.md)
- [教學課程：使用適用於 Visual Studio 的資料湖工具開發 U-SQL 指令碼](data-lake-analytics-data-lake-tools-get-started.md)
