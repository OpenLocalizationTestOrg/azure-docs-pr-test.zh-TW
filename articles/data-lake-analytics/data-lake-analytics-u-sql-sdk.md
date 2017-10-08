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
# <a name="scale-u-sql-local-run-and-test-with-azure-data-lake-u-sql-sdk"></a>使用 Azure Data Lake U-SQL SDK 調整 U-SQL 本機執行和測試

在開發 U-SQL 指令碼時，是通用 toorun，並在本機測試 U-SQL 指令碼之前送出 toocloud。 Azure Data Lake 針對此案例提供稱為 Azure Data Lake U-SQL SDK 的 Nuget 套件，讓您可以輕鬆地調整 U-SQL 本機執行和測試。 它也是可能 toointegrate 此 U-SQL 測試 CI （連續整合） 系統 tooautomate hello 編譯和測試。

如果您在意如何 toomanually 本機執行和偵錯 U-SQL 指令碼的 GUI 工具，則您可以使用 Azure 資料湖 Tools for Visual Studio 的。 您可以在[這裡](data-lake-analytics-data-lake-tools-local-run.md)深入了解。

## <a name="install-azure-data-lake-u-sql-sdk"></a>安裝 Azure Data Lake U-SQL SDK

您可以取得 hello Azure 資料湖 U-SQL SDK[這裡](https://www.nuget.org/packages/Microsoft.Azure.DataLake.USQL.SDK/)Nuget.org 上。然後再將它，您需要 toomake 確定您有相依性，如下所示。

### <a name="dependencies"></a>相依項目

hello 資料湖 U-SQL SDK 需要下列相依性的 hello:

- [Microsoft .NET Framework 4.6 或更新版本](https://www.microsoft.com/download/details.aspx?id=17851)。
- Microsoft Visual C++ 14 和 Windows SDK 10.0.10240.0 或更新版本 (在本文中稱為 CppSDK)。 有兩種方式 tooget CppSDK:

    - 安裝 [Visual Studio Community 版本](https://developer.microsoft.com/downloads/vs-thankyou)。 您必須在 hello Program Files 資料夾，例如，C:\Program Files (x86) \Windows Kits\10\ \Windows Kits\10 資料夾。 您也可以找到下 \Windows Kits\10\Lib hello Windows 10 SDK 版本。 如果您沒有看到這些資料夾，請重新安裝 Visual Studio 並確定 tooselect hello Windows 10 SDK hello 安裝期間。 如果您有這與 Visual Studio 一起安裝，hello U-SQL 本機編譯器會自動找到它。

    ![Data Lake Tools for Visual Studio 本機執行的 Windows 10 SDK](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-windows-10-sdk.png)

    - 安裝 [Data Lake Tools for Visual Studio](http://aka.ms/adltoolsvs)。 您可以找到 hello 套裝位於 C:\Program Files (x86) \Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\ADL Tools\X.X.XXXX.X\CppSDK 的 Visual c + + 和 Windows SDK 檔案。 在此情況下，hello U-SQL 本機編譯器無法自動找到 hello 相依性。 您為它需要 toospecify hello CppSDK 路徑。 您可以複製 hello 檔案 tooanother 位置，或使用原狀。

## <a name="understand-basic-concepts"></a>了解基本概念

### <a name="data-root"></a>資料根

hello 資料根資料夾是 hello 本機計算帳戶 「 本機存放區 」。 它是 Data Lake Analytics 帳戶的對等 toohello Azure Data Lake Store 帳戶。 切換 tooa 不同的資料根資料夾，就如同切換 tooa 不同儲存體帳戶。 如果您想 tooaccess 共用資料使用不同的資料根資料夾，您必須在您的指令碼中使用絕對路徑。 或者，建立檔案系統中的符號連結 (比方說， **mklink**上 NTFS) 下 hello 資料根資料夾 toopoint toohello 共用資料。

hello 資料根資料夾用來：

- 儲存本機中繼資料，包括資料庫、資料表、資料表值函式 (TVF)，以及組件。
- 查閱 hello 輸入和輸出路徑定義為 U SQL 中的相對路徑。 使用相對路徑會更容易 toodeploy 您 U-SQL 專案 tooAzure。

### <a name="file-path-in-u-sql"></a>U-SQL 中的檔案路徑

您可以在 U-SQL 指令碼中使用相對路徑和本機絕對路徑。 hello 相對路徑是相對 toohello 指定的資料根資料夾路徑。 我們建議您使用"/"作為 hello 路徑分隔符號 toomake 相容 hello 伺服器端指令碼。 以下是一些相對路徑及其對等絕對路徑的範例。 在這些範例中，C:\LocalRunDataRoot 會為 hello 資料根資料夾。

|相對路徑|絕對路徑|
|-------------|-------------|
|/abc/def/input.csv |C:\LocalRunDataRoot\abc\def\input.csv|
|abc/def/input.csv  |C:\LocalRunDataRoot\abc\def\input.csv|
|D:/abc/def/input.csv |D:\abc\def\input.csv|

### <a name="working-directory"></a>工作目錄

當在本機執行 hello U-SQL 指令碼，在目前的執行目錄下的編譯期間建立的工作目錄。 此外會輸出 toohello 編譯，hello 所需的本機執行的執行階段檔案會陰影複製的 toothis 工作目錄。 工作目錄的根資料夾的 hello 稱為 「 ScopeWorkDir"和 hello 工作目錄下的 hello 檔案如下：

|目錄/檔案|目錄/檔案|目錄/檔案|定義|說明|
|--------------|--------------|--------------|----------|-----------|
|C6A101DDCB470506| | |執行階段版本的雜湊字串|陰影複製本機執行所需的執行階段檔案|
| |Script_66AE4909AA0ED06C| |指令碼名稱 + 指令碼路徑的雜湊字串|編譯輸出和執行步驟記錄|
| | |\_script\_.abr|編譯器輸出|代數檔案|
| | |\_ScopeCodeGen\_.*|編譯器輸出|產生的 Managed 程式碼|
| | |\_ScopeCodeGenEngine\_.*|編譯器輸出|產生的原生程式碼|
| | |參考的組件|組件參考|參考的組件檔案|
| | |deployed_resources|資源部署|資源部署檔案|
| | |xxxxxxxx.xxx[1..n]\_\*.*|執行記錄檔|執行步驟的記錄檔|


## <a name="use-hello-sdk-from-hello-command-line"></a>從 hello 命令列使用 hello SDK

### <a name="command-line-interface-of-hello-helper-application"></a>Hello 協助應用程式的命令列介面

SDK directory\build\runtime 下 LocalRunHelper.exe 是提供介面 toomost hello 常用的本機執行的函式的 hello 協助程式命令列應用程式。 請注意，兩者 hello 命令 hello 引數的參數會區分大小寫。 tooinvoke 它：

    LocalRunHelper.exe <command> <Required-Command-Arguments> [Optional-Command-Arguments]

不使用引數，或以 hello 執行 LocalRunHelper.exe**協助**切換 tooshow hello 說明資訊：

    > LocalRunHelper.exe help

        Command 'help' :  Show usage information
        Command 'compile' :  Compile hello script
        Required Arguments :
            -Script param
                    Script File Path
        Optional Arguments :
            -Shallow [default value 'False']
                    Shallow compile

Hello 說明中的資訊：

-  **命令**提供 hello 命令的名稱。  
-  **Required Argument** 列出必須提供的引數。  
-  **Optional Argument** 列出選擇性的引數，並具有預設值。  選擇性布林值的引數並不需要參數，而且其外觀表示負數 tootheir 預設值。

### <a name="return-value-and-logging"></a>傳回值和記錄

hello 協助應用程式會傳回**0**成功和**-1**失敗。 根據預設，hello helper 會傳送所有訊息 toohello 目前的主控台。 不過，大部分的 hello 命令支援 hello **-MessageOut path_to_log_file** hello 將重新導向的選擇性引數輸出 tooa 記錄檔。

### <a name="environment-variable-configuring"></a>環境變數設定

U-SQL 本機執行需要指定的資料根做為本機儲存體帳戶，以及針對相依性指定的 CppSDK 路徑。 您可以為它們的命令列或設定環境變數中的兩個組 hello 引數。

- 設定 hello **SCOPE_CPP_SDK**環境變數。

    如果您取得 Microsoft Visual c + + 和 hello Windows SDK 安裝 Data Lake Tools for Visual Studio，請確認您擁有 hello 下列資料夾：

        C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\Microsoft Azure Data Lake Tools for Visual Studio 2015\X.X.XXXX.X\CppSDK

    定義新的環境變數，呼叫**SCOPE_CPP_SDK** toopoint toothis 目錄。 或複製 hello 資料夾 toohello 其他位置，並指定**SCOPE_CPP_SDK**的。

    在加法 toosetting hello 環境變數中，您可以指定 hello **-CppSDK**當您使用 hello 命令列引數。 這個引數會覆寫預設的 CppSDK 環境變數。

- 設定 hello **LOCALRUN_DATAROOT**環境變數。

    定義新的環境變數，呼叫**LOCALRUN_DATAROOT** ，以指 toohello 資料根目錄。

    在加法 toosetting hello 環境變數中，您可以指定 hello **-DataRoot** hello 資料根路徑，當您使用命令列引數。 這個引數會覆寫預設的資料根環境變數。 您需要 tooadd 您正在執行，讓您可以覆寫 hello 預設資料根目錄的所有作業的環境變數的這個引數 tooevery 命令列。

### <a name="sdk-command-line-usage-samples"></a>SDK 命令列使用範例

#### <a name="compile-and-run"></a>編譯和執行

hello**執行**命令用來 toocompile hello 指令碼，然後執行 已編譯的結果。 其命令列引數結合 **compile** 和 **excute** 的引數。

    LocalRunHelper run -Script path_to_usql_script.usql [optional_arguments]

hello 以下是選擇性的引數**執行**:


|引數|預設值|說明|
|--------|-------------|-----------|
|-CodeBehind|False|hello 指令碼有.cs 程式碼後置|
|-CppSDK| |CppSDK 目錄|
|-DataRoot| DataRoot 環境變數|本機執行，DataRoot 太預設 'LOCALRUN_DATAROOT' 環境變數|
|-MessageOut| |傾印主控台 tooa 檔案上的訊息|
|-Parallel|1|執行 hello 計劃與 hello 指定平行處理原則|
|-References| |清單的路徑 tooextra 參考組件或資料檔案中的程式碼後置，以分隔 ';'|
|-UdoRedirect|False|產生 Udo 組件重新導向設定|
|-UseDatabase|master|程式碼後置暫存組件註冊資料庫 toouse|
|-Verbose|False|顯示詳細的執行階段輸出|
|-WorkDir|目前的目錄|編譯器使用方式和輸出的目錄|
|-RunScopeCEP|0|ScopeCEP 模式 toouse|
|-ScopeCEPTempPath|temp|暫存路徑 toouse 串流處理資料|
|-OptFlags| |最佳化工具旗標的逗號分隔清單|


以下是範例：

    LocalRunHelper run -Script d:\test\test1.usql -WorkDir d:\test\bin -CodeBehind -References "d:\asm\ref1.dll;d:\asm\ref2.dll" -UseDatabase testDB –Parallel 5 -Verbose

除了結合**編譯**和**執行**，您可以編譯並分開執行 hello 編譯可執行檔。

#### <a name="compile-a-u-sql-script"></a>編譯 U-SQL 指令碼

hello**編譯**命令是使用的 toocompile U-SQL 指令碼 tooexecutables。

    LocalRunHelper compile -Script path_to_usql_script.usql [optional_arguments]

hello 以下是選擇性的引數**編譯**:


|引數|說明|
|--------|-----------|
| -CodeBehind [預設值 'False']|hello 指令碼有.cs 程式碼後置|
| -CppSDK [預設值 '']|CppSDK 目錄|
| -DataRoot [預設值 'DataRoot environment variable']|本機執行，DataRoot 太預設 'LOCALRUN_DATAROOT' 環境變數|
| -MessageOut [預設值 '']|傾印主控台 tooa 檔案上的訊息|
| -References [預設值 '']|清單的路徑 tooextra 參考組件或資料檔案中的程式碼後置，以分隔 ';'|
| -Shallow [預設值 'False']|淺層編譯|
| -UdoRedirect [預設值 'False']|產生 Udo 組件重新導向設定|
| -UseDatabase [預設值 'master']|程式碼後置暫存組件註冊資料庫 toouse|
| -WorkDir [預設值 'Current Directory']|編譯器使用方式和輸出的目錄|
| -RunScopeCEP [預設值 '0']|ScopeCEP 模式 toouse|
| -ScopeCEPTempPath [預設值 'temp']|暫存路徑 toouse 串流處理資料|
| -OptFlags [預設值 '']|最佳化工具旗標的逗號分隔清單|


這裡有一些使用範例。

編譯 U-SQL 指令碼：

    LocalRunHelper compile -Script d:\test\test1.usql

編譯 U-SQL 指令碼，並設定 hello 資料根資料夾。 請注意這會覆寫 hello 設定環境變數。

    LocalRunHelper compile -Script d:\test\test1.usql –DataRoot c:\DataRoot

編譯 U-SQL 指令碼並設定工作目錄、參考組件和資料庫：

    LocalRunHelper compile -Script d:\test\test1.usql -WorkDir d:\test\bin -References "d:\asm\ref1.dll;d:\asm\ref2.dll" -UseDatabase testDB

#### <a name="execute-compiled-results"></a>執行編譯的結果

hello**執行**命令是使用的 tooexecute 編譯結果。   

    LocalRunHelper execute -Algebra path_to_compiled_algebra_file [optional_arguments]

hello 以下是選擇性的引數**執行**:

|引數|說明|
|--------|-----------|
|-DataRoot [預設值 '']|中繼資料執行的資料根。 它會預設 toohello **LOCALRUN_DATAROOT**環境變數。|
|-MessageOut [預設值 '']|傾印 hello 主控台 tooa 檔案上的訊息。|
|-Parallel [預設值 '1']|指標 toorun hello 產生以 hello 的本機執行步驟指定平行處理原則層級。|
|-Verbose [預設值 'False']|指標 tooshow 詳細的執行階段的輸出。|

以下是使用範例︰

    LocalRunHelper execute -Algebra d:\test\workdir\C6A101DDCB470506\Script_66AE4909AA0ED06C\__script__.abr –DataRoot c:\DataRoot –Parallel 5


## <a name="use-hello-sdk-with-programming-interfaces"></a>使用程式設計介面中的 hello SDK

hello 程式設計介面都位於 hello LocalRunHelper.exe。 您可以使用它們的 hello U-SQL SDK toointegrate hello 功能，且 hello C# 測試 framework tooscale U-SQL 指令碼的本機測試。 在本文中，我將會如何使用 hello 標準 C# 單元測試專案 tooshow toouse 這些介面 tootest U-SQL 指令碼。

### <a name="step-1-create-c-unit-test-project-and-configuration"></a>步驟 1︰建立 C# 單元測試專案和設定

- 透過 [檔案] > [新增] > [專案] > [Visual C#] > [測試] > [單元測試專案] 來建立 C# 單元測試專案。
- 新增 LocalRunHelper.exe hello 專案的參考。 hello LocalRunHelper.exe 位於 \build\runtime\LocalRunHelper.exe Nuget 封裝中。

    ![Azure Data Lake U-SQL SDK 加入參考](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-add-reference.png)

- U-SQL SDK**只**支援 x64 環境，請確定 tooset 組建平台目標為 x64。 您可以透過 [專案屬性] > [建置] > [平台目標] 來設定。

    ![Azure Data Lake U-SQL SDK 設定 x64 專案](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-configure-x64.png)

- 請確定 tooset 您的測試環境為 x64。 在 Visual Studio 中，您可以透過 [測試] > [測試設定] > [預設處理器架構] > [x64] 來設定。

    ![Azure Data Lake U-SQL SDK 設定 x64 測試環境](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-configure-test-x64.png)

- 請確定 toocopy 通常是在 ProjectFolder\bin\x64\Debug NugetPackage\build\runtime\ tooproject 工作目錄下的所有相依性檔案。

### <a name="step-2-create-u-sql-script-test-case"></a>步驟 2：建立 U-SQL 指令碼測試案例

以下是 hello U-SQL 指令碼測試的範例程式碼。 為了測試，您需要 tooprepare 指令碼中，輸入的檔和預期的輸出檔。

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


### <a name="programming-interfaces-in-localrunhelperexe"></a>LocalRunHelper.exe 中的程式設計介面

LocalRunHelper.exe 提供 hello 程式設計介面的 U-SQL 本機編譯、 執行、 列出等 hello 介面，如下所示。

**建構函式**

public LocalRunHelper([System.IO.TextWriter messageOutput = null])

|參數|類型|說明|
|---------|----|-----------|
|messageOutput|System.IO.TextWriter|對於輸出訊息，設定 toonull toouse 主控台|

**屬性**

|屬性|類型|說明|
|--------|----|-----------|
|AlgebraPath|字串|hello 路徑 tooalgebra 檔案 （代數檔案是其中一個 hello 編譯結果）|
|CodeBehindReferences|字串|如果 hello 指令碼額外的程式碼參考之後，請指定 hello 路徑，並以 ';'|
|CppSdkDir|字串|CppSDK 目錄|
|CurrentDir|字串|目前的目錄|
|DataRoot|string|資料根路徑|
|DebuggerMailPath|字串|hello 路徑 toodebugger 槽|
|GenerateUdoRedirect|布林|如果我們想要載入的 toogenerate 組件重新導向會覆寫設定|
|HasCodeBehind|布林|如果 hello 指令碼後置程式碼|
|InputDir|string|輸入資料的目錄|
|MessagePath|字串|訊息傾印檔案路徑|
|OutputDir|string|輸出資料的目錄|
|平行處理原則|int|平行處理原則 toorun hello 代數|
|ParentPid|int|哪些 hello 服務會監視 tooexit、 組 too0 或負 tooignore hello 父系的 PID|
|ResultPath|字串|結果傾印檔案路徑|
|RuntimeDir|字串|執行階段目錄|
|ScriptPath|字串|其中 toofind hello 指令碼|
|Shallow|布林|是否進行淺層編譯|
|TempDir|字串|Temp 目錄|
|UseDataBase|字串|指定程式碼後置暫存組件註冊時，根據預設，主要的 hello 資料庫 toouse|
|WorkDir|字串|慣用的工作目錄|


**方法**

|方法|說明|傳回|參數|
|------|-----------|------|---------|
|public bool DoCompile()|編譯 hello U-SQL 指令碼|成功時為 True| |
|public bool DoExec()|執行 hello 編譯結果|成功時為 True| |
|public bool DoRun()|執行 hello U-SQL 指令碼 （編譯 + 執行）|成功時為 True| |
|public bool IsValidRuntimeDir(string path)|檢查指定路徑的 hello 是否為有效的執行階段的路徑|有效則為 True|hello 目錄路徑的執行階段|


## <a name="faq-about-common-issue"></a>有關常見問題的常見問題集

### <a name="error-1"></a>錯誤 1：
E_CSC_SYSTEM_INTERNAL: 內部錯誤! 無法載入檔案或組件 'ScopeEngineManaged.dll' 或其相依性的其中之一。 找不到 hello 指定的模組。

請檢查下列 hello:

- 確定您使用 x64 環境。 hello 建置目標平台與 hello 測試環境應該是 x64，請參閱太**步驟 1： 建立 C# 單元測試專案和組態**上方。
- 請確定您已複製 NugetPackage\build\runtime\ tooproject 工作目錄下的所有相依性檔案。


## <a name="next-steps"></a>後續步驟

* toolearn U-SQL，請參閱[開始使用 Azure 資料湖分析 U-SQL 語言](data-lake-analytics-u-sql-get-started.md)。
* toolog 診斷資訊，請參閱[存取診斷記錄檔的 Azure Data Lake Analytics](data-lake-analytics-diagnostic-logs.md)。
* toosee 更複雜的查詢，請參閱[分析網站記錄檔，使用 Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md)。
* tooview 作業的詳細資訊，請參閱[使用作業瀏覽器和 Azure Data Lake Analytics 工作的工作檢視](data-lake-analytics-data-lake-tools-view-jobs.md)。
* toouse hello 頂點執行檢視，請參閱[使用 hello 頂點資料湖 Tools for Visual Studio 中的執行檢視](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md)。
