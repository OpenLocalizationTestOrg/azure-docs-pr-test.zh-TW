---
title: "開發程式碼的 Visual Studio 中的 Azure Data Lake Analytics U-SQL Python、 R、 和 C# |Microsoft 文件"
description: "了解如何使用 Python，R 和 C# 程式碼後置提交 Azure Data Lake 中的工作。"
services: data-lake-analytics
documentationcenter: 
author: jejiang
manager: 
editor: 
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 11/22/2017
ms.author: jejiang
ms.openlocfilehash: 8fd8decfde1220be6aaa099c3afb24e8c1eecce4
ms.sourcegitcommit: 4ac89872f4c86c612a71eb7ec30b755e7df89722
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/07/2017
---
# <a name="develop-u-sql-with-python-r-and-c-for-azure-data-lake-analytics-in-visual-studio-code"></a>開發使用 Python，R 和 C# 的 Visual Studio 程式碼中的 Azure Data Lake Analytics U-SQL
了解如何使用 Visual Studio 程式碼 (VSCode) 撰寫 Python，R 和 C# 程式碼後置以 U-SQL 和提交工作至 Azure 資料湖服務。 如需關於 Azure Data Lake Tools for VSCode 的詳細資訊，請參閱[使用 Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md)。

撰寫程式碼後置自訂程式碼之前，您需要在 VSCode 中開啟資料夾或工作區。


## <a name="prerequisites-for-python-and-r"></a>Python 和 R 的必要條件
為您的 ADL 帳戶註冊 Python 和 R 擴充功能組件。 
1. 在入口網站開啟您的帳戶。
   - 選取 [概觀]。 
   - 按一下 [範例指令碼]。
2. 按一下 [更多]。
3. 選取 [安裝 U-SQL 擴充功能]。 
4. 安裝 U-SQL 擴充功能之後，會顯示確認訊息。 

  ![設定 Python 與 R 的環境](./media/data-lake-analytics-data-lake-tools-for-vscode/setup-the-enrionment-for-python-and-r.png)

  > [!Note]
  > 為了在 Python 與 R 語言服務方面獲得最佳體驗，請安裝 VSCode Python 與 R 擴充功能。 

## <a name="develop-python-file"></a>開發 Python 檔案
1. 在您的工作區中按一下 [新增檔案]。
2. 在 U-SQL 中撰寫程式碼。 以下是程式碼範例。
    ```U-SQL
    REFERENCE ASSEMBLY [ExtPython];
    @t  = 
        SELECT * FROM 
        (VALUES
            ("D1","T1","A1","@foo Hello World @bar"),
            ("D2","T2","A2","@baz Hello World @beer")
        ) AS 
            D( date, time, author, tweet );

    @m  =
        REDUCE @t ON date
        PRODUCE date string, mentions string
        USING new Extension.Python.Reducer("pythonSample.usql.py", pyVersion : "3.5.1");

    OUTPUT @m
        TO "/tweetmentions.csv"
        USING Outputters.Csv();
    ```
    
3. 在指令檔上按一下滑鼠右鍵，然後選取 [ADL: Generate Python Code Behind File]。 
4. 工作資料夾中會隨即產生 **xxx.usql.py** 檔案。 在 Python 檔案中撰寫程式碼。 以下是程式碼範例。

    ```Python
    def get_mentions(tweet):
        return ';'.join( ( w[1:] for w in tweet.split() if w[0]=='@' ) )

    def usqlml_main(df):
        del df['time']
        del df['author']
        df['mentions'] = df.tweet.apply(get_mentions)
        del df['tweet']
        return df
    ```
5. 以滑鼠右鍵按一下 **USQL** 檔案，按一下 [編譯指令碼] 或 [提交作業] 即可執行作業。

## <a name="develop-r-file"></a>開發 R 檔案
1. 在您的工作區中按一下 [新增檔案]。
2. 在 U-SQL 檔案中撰寫程式碼。 以下是程式碼範例。
    ```U-SQL
    DEPLOY RESOURCE @"/usqlext/samples/R/my_model_LM_Iris.rda";
    DECLARE @IrisData string = @"/usqlext/samples/R/iris.csv";
    DECLARE @OutputFilePredictions string = @"/my/R/Output/LMPredictionsIris.txt";
    DECLARE @PartitionCount int = 10;

    @InputData =
        EXTRACT SepalLength double,
                SepalWidth double,
                PetalLength double,
                PetalWidth double,
                Species string
        FROM @IrisData
        USING Extractors.Csv();

    @ExtendedData =
        SELECT Extension.R.RandomNumberGenerator.GetRandomNumber(@PartitionCount) AS Par,
            SepalLength,
            SepalWidth,
            PetalLength,
            PetalWidth
        FROM @InputData;

    // Predict Species

    @RScriptOutput =
        REDUCE @ExtendedData
        ON Par
        PRODUCE Par,
                fit double,
                lwr double,
                upr double
        READONLY Par
        USING new Extension.R.Reducer(scriptFile : "RClusterRun.usql.R", rReturnType : "dataframe", stringsAsFactors : false);
    OUTPUT @RScriptOutput
    TO @OutputFilePredictions
    USING Outputters.Tsv();
    ```
3. 以滑鼠右鍵按一下 **USQL** 檔案，然後選取 [ADL: Generate R Code Behind File]。 
4. 工作資料夾中會隨即產生 **xxx.usql.y** 檔案。 在 R 檔案中撰寫程式碼。 以下是程式碼範例。

    ```R
    load("my_model_LM_Iris.rda")
    outputToUSQL=data.frame(predict(lm.fit, inputFromUSQL, interval="confidence"))
    ```
5. 以滑鼠右鍵按一下 **USQL** 檔案，按一下 [編譯指令碼] 或 [提交作業] 即可執行作業。

## <a name="develop-c-file"></a>開發 C# 檔案
程式碼後置檔案是與單一 U-SQL 指令碼關聯的 C# 檔案。 您可以在程式碼後置檔案中定義專用於 UDO、UDA、UDT 和 UDF 的指令碼。 UDO、UDA、UDT 和 UDF 可以直接在指令碼中使用，而不需要先註冊組件。 程式碼後置檔案會放在與其對等互連 U-SQL 指令碼檔案相同的資料夾中。 如果指令碼名稱為 xxx.usql，程式碼後置就會被命名為 xxx.usql.cs。 如果您手動刪除該程式碼後置檔案，系統就會停用其相關聯之 U-SQL 指令碼的程式碼後置功能。 如需撰寫 U-SQL 指令碼之客戶程式碼的詳細資訊，請參閱[在 U-SQL 中撰寫並使用自訂程式碼：使用者定義函式]( https://blogs.msdn.microsoft.com/visualstudio/2015/10/28/writing-and-using-custom-code-in-u-sql-user-defined-functions/) (英文)。

1. 在您的工作區中按一下 [新增檔案]。
2. 在 U-SQL 檔案中撰寫程式碼。 以下是程式碼範例。
    ```U-SQL
    @a = 
        EXTRACT 
            Iid int,
        Starts DateTime,
        Region string,
        Query string,
        DwellTime int,
        Results string,
        ClickedUrls string 
        FROM @"/Samples/Data/SearchLog.tsv" 
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
        TO @"/output/SearchLogtest.txt" 
        USING Outputters.Tsv();
    ```
3. 以滑鼠右鍵按一下 **USQL** 檔案，然後選取 [ADL: Generate CS Code Behind File]。 
4. 工作資料夾中會隨即產生 **xxx.usql.cs** 檔案。 在 CS 檔案中撰寫程式碼。 以下是程式碼範例。

    ```CS
    namespace USQLApplication_codebehind
    {
        [SqlUserDefinedProcessor]

        public class MyProcessor : IProcessor
        {
            public override IRow Process(IRow input, IUpdatableRow output)
            {
                output.Set(0, input.Get<string>(0));
                output.Set(1, input.Get<string>(0));
                return output.AsReadOnly();
            } 
        }
    }
    ```
5. 以滑鼠右鍵按一下 **USQL** 檔案，按一下 [編譯指令碼] 或 [提交作業] 即可執行作業。

## <a name="next-steps"></a>後續步驟
* [使用 Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md)
* [使用 Visual Studio Code 來進行 U-SQL 本機執行和本機偵錯](data-lake-tools-for-vscode-local-run-and-debug.md)
* [針對 Azure Data Lake Analytics 作業開發 U-SQL 組件](data-lake-analytics-u-sql-develop-assemblies.md)
* [使用 PowerShell 開始使用 Data Lake Analytics](data-lake-analytics-get-started-powershell.md)
* [使用 Azure 入口網站開始使用 Data Lake Analytics](data-lake-analytics-get-started-portal.md)
* [使用適用於 Visual Studio 的 Data Lake 工具來開發 U-SQL 應用程式](data-lake-analytics-data-lake-tools-get-started.md)
* [使用 Data Lake Analytics (U-SQL) 目錄](data-lake-analytics-use-u-sql-catalog.md)
