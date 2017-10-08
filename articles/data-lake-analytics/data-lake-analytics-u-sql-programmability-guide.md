---
title: "Azure 資料湖 aaaU SQL 可程式性指南 |Microsoft 文件"
description: "了解 hello 組服務，在 Azure 資料湖 toocreate 可讓您的雲端巨量資料平台。"
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
ms.assetid: 63be271e-7c44-4d19-9897-c2913ee9599d
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/30/2017
ms.author: saveenr
ms.openlocfilehash: cc8f126234c6106a0dc633ce85a1d9ab1e634e30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="u-sql-programmability-guide"></a>U-SQL 可程式性指南

U-SQL 是為巨量資料類型的工作負載所設計的查詢語言。 Hello 組合 hello 類似 SQL 的宣告式語言 hello 擴充性和可程式性所提供的 C# 的其中一個 hello U-SQL 獨特功能。 本指南中，我們會專注於 hello 擴充性和可程式性的啟用 C# 的 hello U-SQL 語言。

## <a name="requirements"></a>需求

下載及安裝 [Azure Data Lake Tools for Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504)。

## <a name="get-started-with-u-sql"></a>開始使用 U-SQL  

讓我們看看下列 U-SQL 指令碼的 hello:

```
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso",   1500.0, "2017-03-39"),
            ("Woodgrove", 2700.0, "2017-04-10")
        ) AS 
              D( customer, amount );
@results =
    SELECT
        customer,
    amount,
    date
    FROM @a;    
```

它會定義名為 @a 的資料列集，並且從 @a 建立名為 @results 的資料列集。

## <a name="c-types-and-expressions-in-u-sql-script"></a>U-SQL 指令碼中的 C# 類型和運算式

U-SQL 運算式是 C# 運算式，與例如 `AND`、`OR` 和 `NOT` 的 U-SQL 邏輯作業合併。 U-SQL 運算式可以與 SELECT、EXTRACT、WHERE、HAVING、GROUP BY 和 DECLARE 搭配使用。

例如，下列指令碼的 hello 剖析字串 hello SELECT 子句中的 DateTime 值。

```
@results =
    SELECT
        customer,
    amount,
    DateTime.Parse(date) AS date
    FROM @a;    
```

hello 下列指令碼將字串剖析 DECLARE 陳述式中的 DateTime 值。

```
DECLARE @d DateTime = ToDateTime.Date("2016/01/01");
```

### <a name="use-c-expressions-for-data-type-conversions"></a>使用 C# 運算式轉換資料類型
hello 下列範例會示範如何日期時間資料轉換，以及在使用 C# 運算式。 在這個特定案例中，字串的日期時間資料會是轉換的 toostandard datetime 午夜 00:00:00 時間標記法。

```
DECLARE @dt String = "2016-07-06 10:23:15";

@rs1 =
    SELECT 
        Convert.ToDateTime(Convert.ToDateTime(@dt).ToString("yyyy-MM-dd")) AS dt,
        dt AS olddt
    FROM @rs0;
OUTPUT @rs1 too@output_file USING Outputters.Text();
```

### <a name="use-c-expressions-for-todays-date"></a>使用 C# 運算式來表示今天的日期
toopull 今天的日期，我們可以使用下列 C# 運算式的 hello:

```
DateTime.Now.ToString("M/d/yyyy")
```

以下是如何的範例 toouse 指令碼中的這個運算式：

```
@rs1 =
    SELECT
        MAX(guid) AS start_id,
        MIN(dt) AS start_time,
        MIN(Convert.ToDateTime(Convert.ToDateTime(dt<@default_dt?@default_dt:dt).ToString("yyyy-MM-dd"))) AS start_zero_time,
        MIN(USQL_Programmability.CustomFunctions.GetFiscalPeriod(dt)) AS start_fiscalperiod,
        DateTime.Now.ToString("M/d/yyyy") AS Nowdate,
        user,
        des
    FROM @rs0
    GROUP BY user, des;
```



## <a name="using-net-assemblies"></a>使用 .NET 組件
U SQL 的擴充性模型非常依賴 hello 能力 tooadd 自訂程式碼。 目前，U-SQL 提供簡單的方法 tooadd 您自己的 Microsoft。（尤其是，C#） 以網路為基礎的程式碼。 不過，您也可以新增以其他 .NET 語言 (例如 VB.NET 或 F#) 撰寫的自訂程式碼。 

### <a name="register-a-net-assembly"></a>註冊 .NET 組件

使用 hello CREATE ASSEMBLY 陳述式 tooplace U SQL 資料庫到.NET 組件。 一旦將組件中的資料庫，U-SQL 指令碼可以使用 hello 參考組件陳述式來使用這些組件。 

hello 下列程式碼會示範如何 tooregister 組件：

```
CREATE ASSEMBLY MyDB.[MyAssembly]
    FROM "/myassembly.dll";
```

hello 下列程式碼會示範如何 tooreference 組件：

```
REFERENCE ASSEMBLY MyDB.[MyAssembly];
```

請參閱 hello[組件註冊指示](https://blogs.msdn.microsoft.com/azuredatalake/2016/08/26/how-to-register-u-sql-assemblies-in-your-u-sql-catalog/)涵蓋本主題會更詳細地。


### <a name="use-assembly-versioning"></a>使用組件版本控制
目前，U-SQL 使用 hello.NET Framework 4.5 版。 因此請確定您自己的組件會與該新版 hello 執行階段相容。

如前面所述，U-SQL 會執行 64 位元 (x64) 格式的程式碼。 因此請確定您的程式碼編譯的 toorun x64 上。 否則，您會收到 hello 不正確的格式錯誤稍早所示。

每個上傳的組件 DLL 和資源檔，例如不同的執行階段、原生組件或組態檔中，最多可達 400 MB。 hello 的已部署的資源，不論是透過部署資源，或是透過參考 tooassemblies 及其他檔案，大小總計不得超過 3 GB。

最後請注意，每一個 U-SQL 資料庫所包含的任何指定組件只能有一個版本。 例如，如果您需要第 7 版和第 8 版的 hello NewtonSoft Json.Net 程式庫，您需要 tooregister 兩個不同資料庫中。 此外，每個指令碼只能參考指定的組件 DLL tooone 版本。 在這一方面，U-SQL 遵循 hello C# 組件管理和版本控制語意。


## <a name="use-user-defined-functions-udf"></a>使用使用者定義函式：UDF
U SQL 使用者定義函數或 UDF，進行程式設計可接受參數、 執行動作 （如複雜計算），以及傳回該動作所得值的 hello 結果的常式。 hello 傳回 UDF 的值只能是單一純量。 U-SQL UDF 可以和任何其他 C# 純量函式一樣，在 U-SQL 基底指令碼中進行呼叫。

我們建議您將 U-SQL 使用者定義函式初始化為**公用**且**靜態**的函式。

```
public static string MyFunction(string param1)
{
    return "my result";
}
```

第一個讓我們看看 hello 建立 UDF 的簡單的範例。

在此使用案例案例中，我們需要 toodetermine hello 會計週期，包括 hello 會計季度和會計月份的 hello 首次登入 hello 特定使用者。 hello 我們的案例中的 hello 年的第一個會計月份為六月。

toocalculate 會計週期，我們引進下列 C# 函式的 hello:

```
public static string GetFiscalPeriod(DateTime dt)
{
    int FiscalMonth=0;
    if (dt.Month < 7)
    {
    FiscalMonth = dt.Month + 6;
    }
    else
    {
    FiscalMonth = dt.Month - 6;
    }

    int FiscalQuarter=0;
    if (FiscalMonth >=1 && FiscalMonth<=3)
    {
    FiscalQuarter = 1;
    }
    if (FiscalMonth >= 4 && FiscalMonth <= 6)
    {
    FiscalQuarter = 2;
    }
    if (FiscalMonth >= 7 && FiscalMonth <= 9)
    {
    FiscalQuarter = 3;
    }
    if (FiscalMonth >= 10 && FiscalMonth <= 12)
    {
    FiscalQuarter = 4;
    }

    return "Q" + FiscalQuarter.ToString() + ":P" + FiscalMonth.ToString();
}
```

它只會計算會計月份和季度，並傳回字串值。 年 6 月，hello 的第一個月 hello 第一個會計季度，我們使用 「 Q1:P1"。 七月，我們使用「Q1:P2」，以此類推。

這是一般 C# 函式，我們處於持續 toouse 我們 U-SQL 專案。

在此案例中的 hello 程式碼後置區段外觀如下：

```
using Microsoft.Analytics.Interfaces;
using Microsoft.Analytics.Types.Sql;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace USQL_Programmability
{
    public class CustomFunctions
    {
        public static string GetFiscalPeriod(DateTime dt)
        {
            int FiscalMonth=0;
            if (dt.Month < 7)
            {
                FiscalMonth = dt.Month + 6;
            }
            else
            {
                FiscalMonth = dt.Month - 6;
            }

            int FiscalQuarter=0;
            if (FiscalMonth >=1 && FiscalMonth<=3)
            {
                FiscalQuarter = 1;
            }
            if (FiscalMonth >= 4 && FiscalMonth <= 6)
            {
                FiscalQuarter = 2;
            }
            if (FiscalMonth >= 7 && FiscalMonth <= 9)
            {
                FiscalQuarter = 3;
            }
            if (FiscalMonth >= 10 && FiscalMonth <= 12)
            {
                FiscalQuarter = 4;
            }

            return "Q" + FiscalQuarter.ToString() + ":" + FiscalMonth.ToString();
        }

    }

}
```

現在我們 toocall 此函式從 hello 基底 U-SQL 指令碼。 toodo，我們有 tooprovide hello 函式，包括 hello 命名空間，在此案例中 NameSpace.Class.Function(parameter) 的完整的名稱。

```
USQL_Programmability.CustomFunctions.GetFiscalPeriod(dt)
```

以下是 hello 實際 U-SQL 基底的指令碼：

```
DECLARE @input_file string = @"\usql-programmability\input_file.tsv";
DECLARE @output_file string = @"\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
            guid Guid,
        dt DateTime,
            user String,
            des String
    FROM @input_file USING Extractors.Tsv();

DECLARE @default_dt DateTime = Convert.ToDateTime("06/01/2016");

@rs1 =
    SELECT
        MAX(guid) AS start_id,
    MIN(dt) AS start_time,
        MIN(Convert.ToDateTime(Convert.ToDateTime(dt<@default_dt?@default_dt:dt).ToString("yyyy-MM-dd"))) AS start_zero_time,
        MIN(USQL_Programmability.CustomFunctions.GetFiscalPeriod(dt)) AS start_fiscalperiod,
        user,
        des
    FROM @rs0
    GROUP BY user, des;

OUTPUT @rs1 
    too@output_file 
    USING Outputters.Text();
```

以下是 hello hello 執行指令碼的輸出檔：

```
0d8b9630-d5ca-11e5-8329-251efa3a2941,2016-02-11T07:04:17.2630000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User1",""

20843640-d771-11e5-b87b-8b7265c75a44,2016-02-11T07:04:17.2630000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User2",""

301f23d2-d690-11e5-9a98-4b4f60a1836f,2016-02-11T09:01:33.9720000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User3",""
```

這個範例示範 U-SQL 中內嵌 UDF 的簡易用法。

### <a name="keep-state-between-udf-invocations"></a>在 UDF 的引動過程之間保持狀態
U-SQL C# 程式設計物件可以是更複雜，利用透過 hello 程式碼後置全域變數的互動性。 讓我們看看下列商務案例中使用案例的 hello。

在大型組織中，使用者可以切換使用各種內部應用程式。 這些可能包括 Microsoft Dynamics CRM、PowerBI 等等。 客戶可能會想 tooapply 使用者如何切換不同的應用程式，哪些 hello 使用量趨勢，以及等等的遙測分析。 hello hello 的商務目標是 toooptimize 應用程式使用情形。 他們也可能會想 toocombine 不同的應用程式或特定的登入常式。

tooachieve 此目標中，我們有 toodetermine 工作階段識別碼和 hello 發生的最後一個工作階段之間的延遲時間。

我們需要 toofind 先前登入，然後將所產生的 toohello 此登入 tooall 工作階段指派相同的應用程式。 hello 第一項挑戰是 U-SQL 基底的指令碼不允許我們 tooapply 計算透過 LAG 函式的已計算資料行。 hello 第二個挑戰是我們有 tookeep hello 特定的工作階段內 hello 的所有工作階段的時間週期相同。

toosolve 這個問題，我們的程式碼後置區段內使用的全域變數： `static public string globalSession;`。

這個全域變數會是我們的指令碼執行期間套用的 toohello 整個資料列集。

以下是我們 U-SQL 程式 hello 程式碼後置區段：

```
using Microsoft.Analytics.Interfaces;
using Microsoft.Analytics.Types.Sql;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace USQLApplication21
{
    public class UserSession
    {
        static public string globalSession;
        static public string StampUserSession(string eventTime, string PreviousRow, string Session)
        {

            if (!string.IsNullOrEmpty(PreviousRow))
            {
                double timeGap = Convert.ToDateTime(eventTime).Subtract(Convert.ToDateTime(PreviousRow)).TotalMinutes;
                if (timeGap <= 60) {return Session;}
                else {return Guid.NewGuid().ToString();}
            }
            else {return Guid.NewGuid().ToString();}

        }

        static public string getStampUserSession(string Session)
        {
            if (Session != globalSession && !string.IsNullOrEmpty(Session)) { globalSession = Session; }
            return globalSession;
        }

    }
}
```

此範例中會顯示 hello 全域變數`static public string globalSession;`hello 內使用`getStampUserSession`函式，並取得重新初始化每個時間 hello 參數變更的工作階段。

hello U-SQL 基底的指令碼如下所示：

```
DECLARE @in string = @"\UserSession\test1.tsv";
DECLARE @out1 string = @"\UserSession\Out1.csv";
DECLARE @out2 string = @"\UserSession\Out2.csv";
DECLARE @out3 string = @"\UserSession\Out3.csv";

@records =
    EXTRACT DataId string,
            EventDateTime string,           
            UserName string,
            UserSessionTimestamp string

    FROM @in
    USING Extractors.Tsv();

@rs1 =
    SELECT 
        EventDateTime,
        UserName,
    LAG(EventDateTime, 1) 
        OVER(PARTITION BY UserName ORDER BY EventDateTime ASC) AS prevDateTime,          
        string.IsNullOrEmpty(LAG(EventDateTime, 1) 
        OVER(PARTITION BY UserName ORDER BY EventDateTime ASC)) AS Flag,           
        USQLApplication21.UserSession.StampUserSession
           (
            EventDateTime,
            LAG(EventDateTime, 1) OVER(PARTITION BY UserName ORDER BY EventDateTime ASC),
            LAG(UserSessionTimestamp, 1) OVER(PARTITION BY UserName ORDER BY EventDateTime ASC)
           ) AS UserSessionTimestamp
    FROM @records;

@rs2 =
    SELECT 
        EventDateTime,
        UserName,
        LAG(EventDateTime, 1) 
        OVER(PARTITION BY UserName ORDER BY EventDateTime ASC) AS prevDateTime,
        string.IsNullOrEmpty( LAG(EventDateTime, 1) OVER(PARTITION BY UserName ORDER BY EventDateTime ASC)) AS Flag,
        USQLApplication21.UserSession.getStampUserSession(UserSessionTimestamp) AS UserSessionTimestamp
    FROM @rs1
    WHERE UserName != "UserName";

OUTPUT @rs2
    too@out2
    ORDER BY UserName, EventDateTime ASC
    USING Outputters.Csv();
```

函式`USQLApplication21.UserSession.getStampUserSession(UserSessionTimestamp)`hello 第二個記憶體資料列集計算期間會呼叫這裡。 它會傳遞 hello`UserSessionTimestamp`資料行，並傳回 hello 值直到`UserSessionTimestamp`已變更。

hello 輸出檔如下所示：

```
"2016-02-19T07:32:36.8420000-08:00","User1",,True,"72a0660e-22df-428e-b672-e0977007177f"
"2016-02-17T11:52:43.6350000-08:00","User2",,True,"4a0cd19a-6e67-4d95-a119-4eda590226ba"
"2016-02-17T11:59:08.8320000-08:00","User2","2016-02-17T11:52:43.6350000-08:00",False,"4a0cd19a-6e67-4d95-a119-4eda590226ba"
"2016-02-11T07:04:17.2630000-08:00","User3",,True,"51860a7a-1610-4f74-a9ea-69d5eef7cd9c"
"2016-02-11T07:10:33.9720000-08:00","User3","2016-02-11T07:04:17.2630000-08:00",False,"51860a7a-1610-4f74-a9ea-69d5eef7cd9c"
"2016-02-15T21:27:41.8210000-08:00","User3","2016-02-11T07:10:33.9720000-08:00",False,"4d2bc48d-bdf3-4591-a9c1-7b15ceb8e074"
"2016-02-16T05:48:49.6360000-08:00","User3","2016-02-15T21:27:41.8210000-08:00",False,"dd3006d0-2dcd-42d0-b3a2-bc03dd77c8b9"
"2016-02-16T06:22:43.6390000-08:00","User3","2016-02-16T05:48:49.6360000-08:00",False,"dd3006d0-2dcd-42d0-b3a2-bc03dd77c8b9"
"2016-02-17T16:29:53.2280000-08:00","User3","2016-02-16T06:22:43.6390000-08:00",False,"2fa899c7-eecf-4b1b-a8cd-30c5357b4f3a"
"2016-02-17T16:39:07.2430000-08:00","User3","2016-02-17T16:29:53.2280000-08:00",False,"2fa899c7-eecf-4b1b-a8cd-30c5357b4f3a"
"2016-02-17T17:20:39.3220000-08:00","User3","2016-02-17T16:39:07.2430000-08:00",False,"2fa899c7-eecf-4b1b-a8cd-30c5357b4f3a"
"2016-02-19T05:23:54.5710000-08:00","User3","2016-02-17T17:20:39.3220000-08:00",False,"6ca7ed80-c149-4c22-b24b-94ff5b0d824d"
"2016-02-19T05:48:37.7510000-08:00","User3","2016-02-19T05:23:54.5710000-08:00",False,"6ca7ed80-c149-4c22-b24b-94ff5b0d824d"
"2016-02-19T06:40:27.4830000-08:00","User3","2016-02-19T05:48:37.7510000-08:00",False,"6ca7ed80-c149-4c22-b24b-94ff5b0d824d"
"2016-02-19T07:27:37.7550000-08:00","User3","2016-02-19T06:40:27.4830000-08:00",False,"6ca7ed80-c149-4c22-b24b-94ff5b0d824d"
"2016-02-19T19:35:40.9450000-08:00","User3","2016-02-19T07:27:37.7550000-08:00",False,"3f385f0b-3e68-4456-ac74-ff6cef093674"
"2016-02-20T00:07:37.8250000-08:00","User3","2016-02-19T19:35:40.9450000-08:00",False,"685f76d5-ca48-4c58-b77d-bd3a9ddb33da"
"2016-02-11T09:01:33.9720000-08:00","User4",,True,"9f0cf696-c8ba-449a-8d5f-1ca6ed8f2ee8"
"2016-02-17T06:30:38.6210000-08:00","User4","2016-02-11T09:01:33.9720000-08:00",False,"8b11fd2a-01bf-4a5e-a9af-3c92c4e4382a"
"2016-02-17T22:15:26.4020000-08:00","User4","2016-02-17T06:30:38.6210000-08:00",False,"4e1cb707-3b5f-49c1-90c7-9b33b86ca1f4"
"2016-02-18T14:37:27.6560000-08:00","User4","2016-02-17T22:15:26.4020000-08:00",False,"f4e44400-e837-40ed-8dfd-2ea264d4e338"
"2016-02-19T01:20:31.4800000-08:00","User4","2016-02-18T14:37:27.6560000-08:00",False,"2136f4cf-7c7d-43c1-8ae2-08f4ad6a6e08"
```

此範例示範更複雜的使用案例案例，我們使用全域變數套用的 toohello 整個記憶體的資料列集的程式碼後置區段內。

## <a name="use-user-defined-types-udt"></a>使用使用者定義的類型：UDT
使用者定義類型 (UDT) 是 U-SQL 的另一個可程式性功能。 U-SQL UDT 的作用就像一般的 C# 使用者定義類型。 C# 是強型別的語言，允許 hello 使用內建和自訂的使用者定義型別。

U-SQL 隱含無法序列化或還原序列化任意 Udt 個資料列集中的頂點傳遞 hello UDT 時。 這表示該 hello 使用者 tooprovide 明確的格式器使用 hello IFormatter 介面。 如此可提供 hello U-SQL 序列化和還原序列化 hello UDT 的方法。

> [!NOTE]
> U SQL 的內建擷取器和 outputters 目前無法序列化或還原序列化 UDT 資料 tooor 從甚至以 hello IFormatter 組的檔案。 因此，當您撰寫 UDT 資料 tooa 檔案以 hello 輸出陳述式，或讀取以擷取程式 」，您有 toopass 它做為字串或位元組陣列。 然後呼叫 hello 序列化，並明確地還原序列化程式碼 （也就是 hello UDT 的 tostring （） 方法）。 使用者定義的擷取器和其他 hello 上的 outputters，另一方面，可以讀取和寫入 Udt。

如果我們嘗試 toouse UDT 中擷取程式 」 或 「 OUTPUTTER （從上一個選取），如下所示：

```
@rs1 =
    SELECT 
        MyNameSpace.Myfunction_Returning_UDT(filed1) AS myfield
    FROM @rs0;

OUTPUT @rs1 
    too@output_file 
    USING Outputters.Text();
```

我們收到 hello 下列錯誤：

```
Error   1   E_CSC_USER_INVALIDTYPEINOUTPUTTER: Outputters.Text was used toooutput column myfield of type
MyNameSpace.Myfunction_Returning_UDT.

Description:

Outputters.Text only supports built-in types.

Resolution:

Implement a custom outputter that knows how tooserialize this type, or call a serialization method on hello type in
hello preceding SELECT. C:\Users\sergeypu\Documents\Visual Studio 2013\Projects\USQL-Programmability\
USQL-Programmability\Types.usql 52  1   USQL-Programmability
```

toowork UDT outputter 中的，我們有 tooserialize 它與 toostring hello tostring （） 方法，或建立自訂 outputter。

UDT 目前不能用於 GROUP BY。 如果 UDT 用於 GROUP BY，則會擲回下列錯誤 hello:

```
Error   1   E_CSC_USER_INVALIDTYPEINCLAUSE: GROUP BY doesn't support type MyNameSpace.Myfunction_Returning_UDT
for column myfield

Description:

GROUP BY doesn't support UDT or Complex types.

Resolution:

Add a SELECT statement where you can project a scalar column that you want toouse with GROUP BY.
C:\Users\sergeypu\Documents\Visual Studio 2013\Projects\USQL-Programmability\USQL-Programmability\Types.usql
62  5   USQL-Programmability
```

我們必須 toodefine UDT:

* 加入下列命名空間的 hello:

```
using Microsoft.Analytics.Interfaces
using System.IO;
```

* 新增`Microsoft.Analytics.Interfaces`，所需之 hello UDT 介面。 此外，`System.IO`可能需要的 toodefine hello IFormatter 介面。

* 使用 SqlUserDefinedType 屬性來定義使用者定義類型。

**SqlUserDefinedType** U-SQL 中是使用的 toomark 為使用者定義型別 (UDT) 的組件中的類型定義。 hello hello 屬性上的屬性會反映 hello UDT hello 實體特性。 這個類別無法繼承。

SqlUserDefinedType 是 UDT 定義的必要屬性 (attribute)。

hello 類別建構 hello 函式：  

* SqlUserDefinedTypeAttribute (類型格式器)

* 型別格式器： 需要參數 toodefine UDT 格式器-具體來說，hello 類型 hello`IFormatter`介面必須這裡傳遞。

```
[SqlUserDefinedType(typeof(MyTypeFormatter))]
public class MyType
{ … }
```

* 典型的 UDT 也需要 hello IFormatter 介面定義，hello 下列範例所示：

```
public class MyTypeFormatter : IFormatter<MyType>
{
    public void Serialize(MyType instance, IColumnWriter writer, ISerializationContext context)
    { … }

    public MyType Deserialize(IColumnReader reader, ISerializationContext context)
    { … }
}
```

hello`IFormatter`介面序列化和還原序列化物件圖形與 hello 根型別\<typeparamref 名稱 ="T">。

\<typeparam 名稱 ="T"> hello hello 物件圖形 tooserialize 的根型別和還原序列化。

* **還原序列化**: hello hello 提供資料流上的資料會取消序列化和重新組成 hello 的物件圖形。

* **序列化**： 序列化物件或圖形的物件，以指定根 toohello 提供資料流的 hello。

`MyType`執行個體： hello 型別的執行個體。  
`IColumnWriter`寫入器 /`IColumnReader`讀取器： hello 基礎資料行的資料流。  
`ISerializationContext`內容： 定義一組旗標會指定序列化期間的 hello hello 資料流的來源或目的端內容的列舉。

* **中繼**： 指定該 hello 來源或目的地的內容不是持續性存放區。

* **持續性**： 指定該 hello 來源或目的地的內容是持續性存放區。

做為一般的 C# 類型，U-SQL UDT 定義可包括 +/==/!= 等運算子的覆寫。 它也可以包含靜態方法。 例如，如果我們 toouse 此 UDT 當做參數 tooa U SQL MIN 彙總函式，我們有 toodefine < 運算子覆寫。

稍早在本指南中，我們會示範會計週期的識別從 hello hello 格式 Qn:Pn (Q1:P10) 中的特定日期的範例。 hello 下列範例顯示如何 toodefine 自訂型別會計週期的值。

以下是具有自訂 UDT 和 IFormatter 介面的程式碼後置區段範例︰

```
[SqlUserDefinedType(typeof(FiscalPeriodFormatter))]
public struct FiscalPeriod
{
    public int Quarter { get; private set; }

    public int Month { get; private set; }

    public FiscalPeriod(int quarter, int month):this()
    {
    this.Quarter = quarter;
    this.Month = month;
    }

    public override bool Equals(object obj)
    {
    if (ReferenceEquals(null, obj))
    {
        return false;
    }

    return obj is FiscalPeriod && Equals((FiscalPeriod)obj);
    }

    public bool Equals(FiscalPeriod other)
    {
return this.Quarter.Equals(other.Quarter) && this.Month.Equals(other.Month);
    }

    public bool GreaterThan(FiscalPeriod other)
    {
return this.Quarter.CompareTo(other.Quarter) > 0 || this.Month.CompareTo(other.Month) > 0;
    }

    public bool LessThan(FiscalPeriod other)
    {
return this.Quarter.CompareTo(other.Quarter) < 0 || this.Month.CompareTo(other.Month) < 0;
    }

    public override int GetHashCode()
    {
    unchecked
    {
        return (this.Quarter.GetHashCode() * 397) ^ this.Month.GetHashCode();
    }
    }

    public static FiscalPeriod operator +(FiscalPeriod c1, FiscalPeriod c2)
    {
return new FiscalPeriod((c1.Quarter + c2.Quarter) > 4 ? (c1.Quarter + c2.Quarter)-4 : (c1.Quarter + c2.Quarter), (c1.Month + c2.Month) > 12 ? (c1.Month + c2.Month) - 12 : (c1.Month + c2.Month));
    }

    public static bool operator ==(FiscalPeriod c1, FiscalPeriod c2)
    {
    return c1.Equals(c2);
    }

    public static bool operator !=(FiscalPeriod c1, FiscalPeriod c2)
    {
    return !c1.Equals(c2);
    }
    public static bool operator >(FiscalPeriod c1, FiscalPeriod c2)
    {
    return c1.GreaterThan(c2);
    }
    public static bool operator <(FiscalPeriod c1, FiscalPeriod c2)
    {
    return c1.LessThan(c2);
    }
    public override string ToString()
    {
    return (String.Format("Q{0}:P{1}", this.Quarter, this.Month));
    }

}

public class FiscalPeriodFormatter : IFormatter<FiscalPeriod>
{
    public void Serialize(FiscalPeriod instance, IColumnWriter writer, ISerializationContext context)
    {
    using (var binaryWriter = new BinaryWriter(writer.BaseStream))
    {
        binaryWriter.Write(instance.Quarter);
        binaryWriter.Write(instance.Month);
        binaryWriter.Flush();
    }
    }

    public FiscalPeriod Deserialize(IColumnReader reader, ISerializationContext context)
    {
    using (var binaryReader = new BinaryReader(reader.BaseStream))
    {
var result = new FiscalPeriod(binaryReader.ReadInt16(), binaryReader.ReadInt16());
        return result;
    }
    }
}
```

hello 定義的類型包含兩個數字： 季度和月份。 運算子 ==/!=/>/< 和靜態方法 ToString() 定義於此。

如先前所述，UDT 可用於 SELECT 運算式中，但不能用在沒有自訂序列化的 OUTPUTTER/EXTRACTOR。 它擁有 toobe 序列化為具有 tostring （） 的字串，或與自訂 OUTPUTTER/抽選程式搭配使用。

現在我們來討論一下 UDT 的使用方式。 在程式碼後置 區段中，我們可以變更我們 GetFiscalPeriod 函式 toohello 下列：

```
public static FiscalPeriod GetFiscalPeriodWithCustomType(DateTime dt)
{
    int FiscalMonth = 0;
    if (dt.Month < 7)
    {
    FiscalMonth = dt.Month + 6;
    }
    else
    {
    FiscalMonth = dt.Month - 6;
    }

    int FiscalQuarter = 0;
    if (FiscalMonth >= 1 && FiscalMonth <= 3)
    {
    FiscalQuarter = 1;
    }
    if (FiscalMonth >= 4 && FiscalMonth <= 6)
    {
    FiscalQuarter = 2;
    }
    if (FiscalMonth >= 7 && FiscalMonth <= 9)
    {
    FiscalQuarter = 3;
    }
    if (FiscalMonth >= 10 && FiscalMonth <= 12)
    {
    FiscalQuarter = 4;
    }

    return new FiscalPeriod(FiscalQuarter, FiscalMonth);
}
```

如您所見，它會傳回 hello 我們 FiscalPeriod 類型值。

在這裡，我們會提供如何 toouse 它進一步 U-SQL 基底的指令碼中的範例。 這個範例會示範從 U-SQL 指令碼叫用 UDT 的不同方式。

```
DECLARE @input_file string = @"c:\work\cosmos\usql-programmability\input_file.tsv";
DECLARE @output_file string = @"c:\work\cosmos\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
        guid string,
        dt DateTime,
        user String,
        des String
    FROM @input_file USING Extractors.Tsv();

@rs1 =
    SELECT 
        guid AS start_id,
        dt,
        DateTime.Now.ToString("M/d/yyyy") AS Nowdate,
        USQL_Programmability.CustomFunctions.GetFiscalPeriodWithCustomType(dt).Quarter AS fiscalquarter,
        USQL_Programmability.CustomFunctions.GetFiscalPeriodWithCustomType(dt).Month AS fiscalmonth,
        USQL_Programmability.CustomFunctions.GetFiscalPeriodWithCustomType(dt) + new USQL_Programmability.CustomFunctions.FiscalPeriod(1,7) AS fiscalperiod_adjusted,
        user,
        des
    FROM @rs0;

@rs2 =
    SELECT 
           start_id,
           dt,
           DateTime.Now.ToString("M/d/yyyy") AS Nowdate,
           fiscalquarter,
           fiscalmonth,
           USQL_Programmability.CustomFunctions.GetFiscalPeriodWithCustomType(dt).ToString() AS fiscalperiod,

       // This user-defined type was created in hello prior SELECT.  Passing hello UDT toothis subsequent SELECT would have failed if hello UDT was not annotated with an IFormatter.
           fiscalperiod_adjusted.ToString() AS fiscalperiod_adjusted,
           user,
           des
    FROM @rs1;

OUTPUT @rs2 
    too@output_file 
    USING Outputters.Text();
```

以下是完整程式碼後置區段的範例︰

```
using Microsoft.Analytics.Interfaces;
using Microsoft.Analytics.Types.Sql;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.IO;

namespace USQL_Programmability
{
    public class CustomFunctions
    {
        static public DateTime? ToDateTime(string dt)
        {
            DateTime dtValue;

            if (!DateTime.TryParse(dt, out dtValue))
                return Convert.ToDateTime(dt);
            else
                return null;
        }

        public static FiscalPeriod GetFiscalPeriodWithCustomType(DateTime dt)
        {
            int FiscalMonth = 0;
            if (dt.Month < 7)
            {
                FiscalMonth = dt.Month + 6;
            }
            else
            {
                FiscalMonth = dt.Month - 6;
            }

            int FiscalQuarter = 0;
            if (FiscalMonth >= 1 && FiscalMonth <= 3)
            {
                FiscalQuarter = 1;
            }
            if (FiscalMonth >= 4 && FiscalMonth <= 6)
            {
                FiscalQuarter = 2;
            }
            if (FiscalMonth >= 7 && FiscalMonth <= 9)
            {
                FiscalQuarter = 3;
            }
            if (FiscalMonth >= 10 && FiscalMonth <= 12)
            {
                FiscalQuarter = 4;
            }

            return new FiscalPeriod(FiscalQuarter, FiscalMonth);
        }



        [SqlUserDefinedType(typeof(FiscalPeriodFormatter))]
        public struct FiscalPeriod
        {
            public int Quarter { get; private set; }

            public int Month { get; private set; }

            public FiscalPeriod(int quarter, int month):this()
            {
                this.Quarter = quarter;
                this.Month = month;
            }

            public override bool Equals(object obj)
            {
                if (ReferenceEquals(null, obj))
                {
                    return false;
                }

                return obj is FiscalPeriod && Equals((FiscalPeriod)obj);
            }

            public bool Equals(FiscalPeriod other)
            {
return this.Quarter.Equals(other.Quarter) &&    this.Month.Equals(other.Month);
            }

            public bool GreaterThan(FiscalPeriod other)
            {
return this.Quarter.CompareTo(other.Quarter) > 0 || this.Month.CompareTo(other.Month) > 0;
            }

            public bool LessThan(FiscalPeriod other)
            {
return this.Quarter.CompareTo(other.Quarter) < 0 || this.Month.CompareTo(other.Month) < 0;
            }

            public override int GetHashCode()
            {
                unchecked
                {
                    return (this.Quarter.GetHashCode() * 397) ^ this.Month.GetHashCode();
                }
            }

            public static FiscalPeriod operator +(FiscalPeriod c1, FiscalPeriod c2)
            {
return new FiscalPeriod((c1.Quarter + c2.Quarter) > 4 ? (c1.Quarter + c2.Quarter)-4 : (c1.Quarter + c2.Quarter), (c1.Month + c2.Month) > 12 ? (c1.Month + c2.Month) - 12 : (c1.Month + c2.Month));
            }

            public static bool operator ==(FiscalPeriod c1, FiscalPeriod c2)
            {
                return c1.Equals(c2);
            }

            public static bool operator !=(FiscalPeriod c1, FiscalPeriod c2)
            {
                return !c1.Equals(c2);
            }
            public static bool operator >(FiscalPeriod c1, FiscalPeriod c2)
            {
                return c1.GreaterThan(c2);
            }
            public static bool operator <(FiscalPeriod c1, FiscalPeriod c2)
            {
                return c1.LessThan(c2);
            }
            public override string ToString()
            {
                return (String.Format("Q{0}:P{1}", this.Quarter, this.Month));
            }

        }

        public class FiscalPeriodFormatter : IFormatter<FiscalPeriod>
        {
public void Serialize(FiscalPeriod instance, IColumnWriter writer, ISerializationContext context)
            {
                using (var binaryWriter = new BinaryWriter(writer.BaseStream))
                {
                    binaryWriter.Write(instance.Quarter);
                    binaryWriter.Write(instance.Month);
                    binaryWriter.Flush();
                }
            }

public FiscalPeriod Deserialize(IColumnReader reader, ISerializationContext context)
            {
                using (var binaryReader = new BinaryReader(reader.BaseStream))
                {
var result = new FiscalPeriod(binaryReader.ReadInt16(), binaryReader.ReadInt16());
                    return result;
                }
            }
        }
    }
}
```

## <a name="use-user-defined-aggregates-udagg"></a>使用使用者定義彙總：UDAGG
使用者定義彙總是指並非 U-SQL 現成提供的彙總相關函式。 hello 範例可以是彙總的 tooperform 自訂數學計算，字串串連字串的操作，並以此類推。

hello 使用者定義彙總的基底類別定義如下所示：

```c#
    [SqlUserDefinedAggregate]
    public abstract class IAggregate<T1, T2, TResult> : IAggregate
    {
        protected IAggregate();

        public abstract void Accumulate(T1 t1, T2 t2);
        public abstract void Init();
        public abstract TResult Terminate();
    }
```

**SqlUserDefinedAggregate**表示 hello 類型應該註冊為使用者定義彙總。 這個類別無法繼承。

SqlUserDefinedType 是 UDAGG 定義的**選擇性**屬性。


hello 基底類別可讓您 toopass 三個抽象參數： 兩個輸入的參數及另一個目錄當做 hello 結果。 hello 資料型別變動而應定義類別繼承時。

```
public class GuidAggregate : IAggregate<string, string, string>
{
    string guid_agg;

    public override void Init()
    { … }

    public override void Accumulate(string guid, string user)
    { … }

    public override string Terminate()
    { … }
}
```

* **Init** 會在計算期間，為每個群組叫用一次。 Init 可為每個彙總群組提供初始化常式。  
* **Accumulate** 會為每個值執行一次。 它提供 hello 彙總演算法 hello 主要功能。 它可以是使用的 tooaggregate 類別繼承期間定義的各種資料類型的值。 它可接受兩個變數資料類型的參數。
* **終止**每個彙總群組結尾 hello 處理 toooutput hello 結果的每個群組執行一次。

toodeclare 正確的輸入和輸出資料類型，使用 hello 類別定義，如下所示：

```
public abstract class IAggregate<T1, T2, TResult> : IAggregate
```

* 第一個參數 tooaccumulate T1:
* 第一個參數 tooaccumulate T2:
* TResult：傳回終止的類型

例如：

```
public class GuidAggregate : IAggregate<string, int, int>
```

或

```
public class GuidAggregate : IAggregate<string, string, string>
```

### <a name="use-udagg-in-u-sql"></a>在 U-SQL 中使用 UDAGG
toouse UDAGG，先在程式碼後置中定義它，或從 hello 存在可程式性 DLL 參考先前所述。

接著，使用下列語法的 hello:

```
AGG<UDAGG_functionname>(param1,param2)
```

UDAGG 範例如下：

```
public class GuidAggregate : IAggregate<string, string, string>
{
    string guid_agg;

    public override void Init()
    {
        guid_agg = "";
    }

    public override void Accumulate(string guid, string user)
    {
        if (user.ToUpper()== "USER1")
        {
        guid_agg += "{" + guid + "}";
        }
    }

    public override string Terminate()
    {
        return guid_agg;
    }

}
```

以及基底 U-SQL 指令碼：

```
DECLARE @input_file string = @"\usql-programmability\input_file.tsv";
DECLARE @output_file string = @" \usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
            guid string,
        dt DateTime,
            user String,
            des String
    FROM @input_file 
    USING Extractors.Tsv();

@rs1 =
    SELECT
        user,
        AGG<USQL_Programmability.GuidAggregate>(guid,user) AS guid_list
    FROM @rs0
    GROUP BY user;

OUTPUT @rs1 too@output_file USING Outputters.Text();
```

在此使用案例案例中，我們會串連 hello 特定使用者的類別 Guid。

## <a name="use-user-defined-objects-udo"></a>使用使用者定義物件：UDO
U SQL 可讓您會在呼叫使用者定義物件或 UDO toodefine 自訂的可程式性物件。

hello 以下是中 U-SQL UDO 的清單：

* 使用者定義擷取器
    * 逐列擷取
    * 使用自訂的結構化檔案從 tooimplement 資料擷取

* 使用者定義輸出器
    * 逐列輸出
    * 使用 toooutput 自訂資料類型或自訂的檔案格式

* 使用者定義處理器
    * 擷取一列並產生一列
    * 使用的 tooreduce hello 的資料行數目，或產生新的資料行衍生自現有的資料行集的值

* 使用者定義套用器
    * 需要一個資料列，並產生 0 toon 個資料列
    * 與 OUTER/CROSS APPLY 搭配使用

* 使用者定義結合器
    * 結合資料列集--使用者定義 JOIN

* 使用者定義歸納器
    * 擷取 n 列並產生一列
    * 使用資料列的 tooreduce hello 數目

UDO 通常會遵循 U SQL 陳述式的 hello 一部分 U-SQL 指令碼中明確呼叫：

* EXTRACT
* OUTPUT
* PROCESS
* COMBINE
* REDUCE

> [!NOTE]  
> UDO 的是有限的 tooconsume 0.5 Gb 記憶體。  此記憶體限制不適用 toolocal 執行。

## <a name="use-user-defined-extractors"></a>使用使用者定義擷取器
U SQL 可讓您 tooimport 外部資料使用的擷取陳述式。 EXTRACT 陳述式可以使用內建的 UDO 擷取器：  

* Extractors.Text()︰可從不同編碼的分隔文字檔進行擷取。

* Extractors.Csv()︰可從不同編碼的逗號分隔值 (CSV) 檔案進行擷取。

* Extractors.Tsv()︰可從不同編碼的定位鍵分隔值 (TSV) 檔案進行擷取。

它可以是很有用 toodevelop 自訂擷取程式 」。 這可能是很有幫助資料匯入期間如果我們想要 toodo 任何 hello 下列工作：

* 分割資料行並修改個別值，以修改輸入資料。 hello 處理器功能是為了合併資料行。
* 剖析非結構化資料 (例如網頁/電子郵件) 或半非結構化資料 (例如 XML/JSON)。
* 剖析編碼不受支援的資料。

toodefine 使用者定義的擷取程式，或者 UDE，我們需要 toocreate`IExtractor`介面。 所有的輸入參數 toohello 抽選程式，例如資料行/資料列分隔符號和編碼，則需要 toobe hello 類別 hello 建構函式中定義。 hello`IExtractor`介面也應包含 hello 的定義`IEnumerable<IRow>`覆寫，如下所示：

```
[SqlUserDefinedExtractor]
public class SampleExtractor : IExtractor
{
     public SampleExtractor(string row_delimiter, char col_delimiter)
     { … }

     public override IEnumerable<IRow> Extract(IUnstructuredReader input, IUpdatableRow output)
     { … }
}
```

hello **SqlUserDefinedExtractor**屬性會指出 hello 類型應該要註冊為使用者定義的擷取程式。 這個類別無法繼承。

SqlUserDefinedExtractor 是 UDE 定義的選擇性屬性。 它會將 toodefine AtomicFileProcessing 屬性用於 hello UDE 物件。

* bool     AtomicFileProcessing   

* **true** = 表示此擷取器需要不可部分完成的輸入檔 (JSON、XML ...)
* **false** = 表示此擷取器可以處理分割/分散式檔案 (CSV、SEQ ...)

hello 主要 UDE 可程式性物件**輸入**和**輸出**。 hello 輸入的物件是使用的 tooenumerate 輸入的資料為`IUnstructuredReader`。 hello 輸出物件是使用的 tooset hello 擷取程式 」 活動的輸出資料。

hello 輸入的資料透過存取`System.IO.Stream`和`System.IO.StreamReader`。

針對輸入資料行列舉型別，我們先分割 hello 輸入資料流使用資料列分隔符號。

```
foreach (Stream current in input.Split(my_row_delimiter))
{
…
}
```

然後，將輸入資料列進一步分割為資料行組件。

```
foreach (Stream current in input.Split(my_row_delimiter))
{
…
    string[] parts = line.Split(my_column_delimiter);
    foreach (string part in parts)
    { … }
}
```

tooset 輸出的資料，我們使用 hello`output.Set`方法。

請務必 hello 自訂擷取程式 」 的 toounderstand 只輸出資料行和值定義與 hello 輸出。 設定方法呼叫。

```
output.Set<string>(count, part);
```

hello 實際擷取程式 」 輸出由呼叫觸發`yield return output.AsReadOnly();`。

以下是 hello 擷取程式 」 範例：

```
[SqlUserDefinedExtractor(AtomicFileProcessing = true)]
public class FullDescriptionExtractor : IExtractor
{
     private Encoding _encoding;
     private byte[] _row_delim;
     private char _col_delim;

    public FullDescriptionExtractor(Encoding encoding, string row_delim = "\r\n", char col_delim = '\t')
    {
         this._encoding = ((encoding == null) ? Encoding.UTF8 : encoding);
         this._row_delim = this._encoding.GetBytes(row_delim);
         this._col_delim = col_delim;

    }

    public override IEnumerable<IRow> Extract(IUnstructuredReader input, IUpdatableRow output)
    {
         string line;
         //Read hello input line by line
         foreach (Stream current in input.Split(_encoding.GetBytes("\r\n")))
         {
        using (System.IO.StreamReader streamReader = new StreamReader(current, this._encoding))
         {
             line = streamReader.ReadToEnd().Trim();
             //Split hello input by hello column delimiter
             string[] parts = line.Split(this._col_delim);
             int count = 0; // start with first column
             foreach (string part in parts)
             {
    if (count == 0)
             {  // for column “guid”, re-generated guid
                 Guid new_guid = Guid.NewGuid();
                 output.Set<Guid>(count, new_guid);
             }
             else if (count == 2)
             {
                 // for column “user”, convert tooUPPER case
                 output.Set<string>(count, part.ToUpper());

             }
             else
             {
                 // keep hello rest of hello columns as-is
                 output.Set<string>(count, part);
             }
             count += 1;
             }

         }
         yield return output.AsReadOnly();
         }
         yield break;
     }
}
```

在此使用案例案例中，hello 抽選程式重新 hello GUID"guid"資料行，並將 「 使用者 」 資料行 tooupper 案例的 hello 值轉換。 自訂擷取器可藉由剖析輸入資料並用它進行操作，來產生更複雜的結果。

以下為使用自訂擷取器的基底 U-SQL 指令碼：

```
DECLARE @input_file string = @"\usql-programmability\input_file.tsv";
DECLARE @output_file string = @"\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
            guid Guid,
        dt String,
            user String,
            des String
    FROM @input_file
        USING new USQL_Programmability.FullDescriptionExtractor(Encoding.UTF8);

OUTPUT @rs0 too@output_file USING Outputters.Text();
```

## <a name="use-user-defined-outputters"></a>使用使用者定義輸出器
使用者定義 outputter 是另一個 U-SQL UDO，可讓您 tooextend 內建 U-SQL 功能。 類似 toohello 抽選程式，有數個內建 outputters。

* *Outputters.Text()*： 寫入資料 toodelimited 不同編碼的文字檔案。
* *Outputters.Csv()*： 會寫入資料 toocomma 分隔值 (CSV) 檔案的不同的編碼方式。
* *Outputters.Tsv()*： 會寫入資料 tootab 分隔值 (TSV) 檔案的不同的編碼方式。

自訂 outputter 可讓您 toowrite 資料中定義的自訂格式。 這可用於 hello 下列工作：

* 撰寫資料 toosemi 結構化或非結構化檔案。
* 寫入編碼不受支援的資料。
* 修改輸出資料或新增自訂屬性。

我們需要 toocreate hello toodefine 使用者定義 outputter`IOutputter`介面。

以下是基底 hello`IOutputter`類別實作：

```
public abstract class IOutputter : IUserDefinedOperator
{
    protected IOutputter();

    public virtual void Close();
    public abstract void Output(IRow input, IUnstructuredWriter output);
}
```

所有的輸入參數 toohello outputter，例如資料行/資料列分隔符號、 編碼和等等，需要 toobe hello 類別 hello 建構函式中定義。 hello`IOutputter`介面也應包含的定義`void Output`覆寫。 hello 屬性`[SqlUserDefinedOutputter(AtomicFileProcessing = true)`可以選擇性地設定為不可部分完成檔案處理。 如需詳細資訊，請參閱 hello 下列詳細資料。

```
[SqlUserDefinedOutputter(AtomicFileProcessing = true)]
public class MyOutputter : IOutputter
{

    public MyOutputter(myparam1, myparam2)
    {
      …
    }

    public override void Close()
    {
      …
    }

    public override void Output(IRow row, IUnstructuredWriter output)
    {
      …
    }
}
```

* 會針對每個輸入資料列呼叫 `Output`。 它會傳回 hello`IUnstructuredWriter output`資料列集。
* hello 建構函式類別用 toopass 參數 toohello 使用者定義 outputter。
* `Close`使用 toooptionally 覆寫 toorelease 高度耗費資源的狀態，或判斷 hello 最後一個資料列寫入的時。

**SqlUserDefinedOutputter**屬性會指出 hello 類型應該要註冊為使用者定義的 outputter。 這個類別無法繼承。

SqlUserDefinedOutputter 是使用者定義輸出器之定義的選擇性屬性。 它已用 toodefine hello AtomicFileProcessing 屬性。

* bool     AtomicFileProcessing   

* **true** = 表示此輸出器需要不可部分完成的輸出檔 (JSON、XML ...)
* **false** = 表示此輸出器可以處理分割/分散式檔案 (CSV、SEQ ...)

hello 主要的可程式性物件**列**和**輸出**。 hello**列**物件是使用的 tooenumerate 輸出資料做為`IRow`介面。 **輸出**使用的 tooset 輸出資料 toohello 目標檔案。

hello 輸出資料透過存取 hello`IRow`介面。 一次會對輸出資料傳遞一個資料列。

藉由呼叫 hello IRow 介面 hello Get 方法列舉 hello 個別的值：

```
row.Get<string>("column_name")
```

呼叫 `row.Schema` 即可判斷個別資料行名稱：

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

這種方法可讓您針對任何中繼資料結構描述的彈性 outputter toobuild。

hello 輸出資料寫入 toofile 使用`System.IO.StreamWriter`。 hello 資料流參數設定得`output.BaseStrea`一部分`IUnstructuredWriter output`。

請注意，它會是重要 tooflush hello 資料緩衝區 toohello 檔在每個資料列反覆項目。 此外，hello`StreamWriter`物件必須用在 hello 可處置的啟用屬性 （預設值） 與 hello**使用**關鍵字：

```
using (StreamWriter streamWriter = new StreamWriter(output.BaseStream, this._encoding))
{
…
}
```

否則，在每個反覆項目之後明確地呼叫 Flush() 方法。 我們會顯示這在下列範例中的 hello。

### <a name="set-headers-and-footers-for-user-defined-outputter"></a>設定使用者定義輸出器的頁首和頁尾
tooset 標頭，使用單一的反覆項目執行流程。

```
public override void Output(IRow row, IUnstructuredWriter output)
{
 …
if (isHeaderRow)
{
    …                
}

 …
if (isHeaderRow)
{
    isHeaderRow = false;
}
 …
}
}
```

第一次 hello hello 中的程式碼`if (isHeaderRow)`區塊執行一次。

Hello 頁尾使用 hello 參考 toohello 執行個體`System.IO.Stream`物件 (`output.BaseStream`)。 在 hello hello 的 close （） 方法中撰寫 hello 頁尾`IOutputter`介面。  （如需詳細資訊，請參閱下列範例中的 hello）。

以下是使用者定義 outputter 的範例︰

```
[SqlUserDefinedOutputter(AtomicFileProcessing = true)]
public class HTMLOutputter : IOutputter
{
    // Local variables initialization
    private string row_delimiter;
    private char col_delimiter;
    private bool isHeaderRow;
    private Encoding encoding;
    private bool IsTableHeader = true;
    private Stream g_writer;

    // Parameters definition            
    public HTMLOutputter(bool isHeader = false, Encoding encoding = null)
    {
    this.isHeaderRow = isHeader;
    this.encoding = ((encoding == null) ? Encoding.UTF8 : encoding);
    }

    // hello Close method is used toowrite hello footer toohello file. It's executed only once, after all rows
    public override void Close().
    {
    //Reference tooIO.Stream object - g_writer
    StreamWriter streamWriter = new StreamWriter(g_writer, this.encoding);
    streamWriter.Write("</table>");
    streamWriter.Flush();
    streamWriter.Close();
    }

    public override void Output(IRow row, IUnstructuredWriter output)
    {
    System.IO.StreamWriter streamWriter = new StreamWriter(output.BaseStream, this.encoding);

    // Metadata schema initialization tooenumerate column names
    ISchema schema = row.Schema;

    // This is a data-independent header--HTML table definition
    if (IsTableHeader)
    {
        streamWriter.Write("<table border=1>");
        IsTableHeader = false;
    }

    // HTML table attributes
    string header_wrapper_on = "<th>";
    string header_wrapper_off = "</th>";
    string data_wrapper_on = "<td>";
    string data_wrapper_off = "</td>";

    // Header row output--runs only once
    if (isHeaderRow)
    {
        streamWriter.Write("<tr>");
        for (int i = 0; i < schema.Count(); i++)
        {
        var col = schema[i];
        streamWriter.Write(header_wrapper_on + col.Name + header_wrapper_off);
        }
        streamWriter.Write("</tr>");
    }

    // Data row output
    streamWriter.Write("<tr>");                
    for (int i = 0; i < schema.Count(); i++)
    {
        var col = schema[i];
        string val = "";
        try
        {
        // Data type enumeration--required toomatch hello distinct list of types from OUTPUT statement
        switch (col.Type.Name.ToString().ToLower())
        {
            case "string": val = row.Get<string>(col.Name).ToString(); break;
            case "guid": val = row.Get<Guid>(col.Name).ToString(); break;
            default: break;
        }
        }
        // Handling NULL values--keeping them empty
        catch (System.NullReferenceException)
        {
        }
        streamWriter.Write(data_wrapper_on + val + data_wrapper_off);
    }
    streamWriter.Write("</tr>");

    if (isHeaderRow)
    {
        isHeaderRow = false;
    }
    // Reference toohello instance of hello IO.Stream object for footer generation
    g_writer = output.BaseStream;
    streamWriter.Flush();
    }
}

// Define hello factory classes
public static class Factory
{
    public static HTMLOutputter HTMLOutputter(bool isHeader = false, Encoding encoding = null)
    {
    return new HTMLOutputter(isHeader, encoding);
    }
}
```

以及 U-SQL 基底指令碼：

```
DECLARE @input_file string = @"\usql-programmability\input_file.tsv";
DECLARE @output_file string = @"\usql-programmability\output_file.html";

@rs0 =
    EXTRACT
            guid Guid,
        dt String,
            user String,
            des String
         FROM @input_file
         USING new USQL_Programmability.FullDescriptionExtractor(Encoding.UTF8);

OUTPUT @rs0 
    too@output_file 
    USING new USQL_Programmability.HTMLOutputter(isHeader: true);
```

這是 HTML 輸出器，會以資料表資料建立 HTML 檔案。

### <a name="call-outputter-from-u-sql-base-script"></a>從 U-SQL 基底指令碼呼叫輸出器
toocall 從 hello 基底 U-SQL 指令碼的自訂 outputter，hello hello outputter 物件的新執行個體具有建立 toobe。

```sql
OUTPUT @rs0 too@output_file USING new USQL_Programmability.HTMLOutputter(isHeader: true);
```

tooavoid 建立 hello 的執行個體物件存放至基底的指令碼，我們可以建立函式的包裝函式，在先前的範例所示：

```c#
        // Define hello factory classes
        public static class Factory
        {
            public static HTMLOutputter HTMLOutputter(bool isHeader = false, Encoding encoding = null)
            {
                return new HTMLOutputter(isHeader, encoding);
            }
        }
```

在此情況下，hello 原始呼叫看起來像下列 hello:

```
OUTPUT @rs0 
too@output_file 
USING USQL_Programmability.Factory.HTMLOutputter(isHeader: true);
```

## <a name="use-user-defined-processors"></a>使用使用者定義處理器
使用者定義的處理器或 UDP 是一種可讓您藉由套用 可程式性功能的 tooprocess hello 內送資料列的 U-SQL UDO。 UDP 可讓您 toocombine 資料行、 修改值，並視需要新增新的資料行。 基本上，它會協助 tooprocess 資料列集所需的 tooproduce 資料元素。

toodefine UDP，我們需要 toocreate`IProcessor`介面以 hello`SqlUserDefinedProcessor`屬性，這是選擇性的 UDP。

這個介面應該包含 hello hello 定義`IRow`介面資料列集覆寫，hello 下列範例所示：

```
[SqlUserDefinedProcessor]
public class MyProcessor: IProcessor
{
public override IRow Process(IRow input, IUpdatableRow output)
 {
        …
 }
}
```

**SqlUserDefinedProcessor**表示 hello 類型應該註冊為使用者定義的處理器。 這個類別無法繼承。

hello SqlUserDefinedProcessor 屬性是**選擇性**UDP 定義。

hello 主要的可程式性物件**輸入**和**輸出**。 hello 輸入的物件是使用的 tooenumerate 輸入資料行和輸出和 tooset hello 處理器活動的輸出資料。

輸入資料行列舉型別，我們使用 hello`input.Get`方法。

```
string column_name = input.Get<string>("column_name");
```

hello 參數`input.Get`方法是傳遞做為 hello 一部分的資料行`PRODUCE`子句 hello `PROCESS` hello U-SQL 基底的指令碼陳述式。 我們需要 toouse hello 正確資料類型，這裡。

輸出中，使用 hello`output.Set`方法。

請務必 toonote 該自訂生產者只會輸出資料行和值所定義的 hello`output.Set`方法呼叫。

```
output.Set<string>("mycolumn", mycolumn);
```

藉由呼叫觸發 hello 實際處理器輸出`return output.AsReadOnly();`。

以下是處理器範例：

```
[SqlUserDefinedProcessor]
public class FullDescriptionProcessor : IProcessor
{
public override IRow Process(IRow input, IUpdatableRow output)
 {
     string user = input.Get<string>("user");
     string des = input.Get<string>("des");
     string full_description = user.ToUpper() + "=>" + des;
     output.Set<string>("dt", input.Get<string>("dt"));
     output.Set<string>("full_description", full_description);
     output.Set<Guid>("new_guid", Guid.NewGuid());
     output.Set<Guid>("guid", input.Get<Guid>("guid"));
     return output.AsReadOnly();
 }
}
```

在此使用案例案例中，hello 處理器正在產生新的資料行稱為"full_description 」 結合 hello 現有資料行-在此情況下，「 使用者 」 中大寫，而"des"。 它也會重新產生 GUID，並傳回 hello 原始值和新的 GUID 值。

您可以看到 hello 前一個範例中，您可以呼叫 C# 方法期間`output.Set`方法呼叫。

以下是使用自訂處理器的基底 U-SQL 指令碼範例：

```
DECLARE @input_file string = @"\usql-programmability\input_file.tsv";
DECLARE @output_file string = @"\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
            guid Guid,
        dt String,
            user String,
            des String
    FROM @input_file USING Extractors.Tsv();

@rs1 =
     PROCESS @rs0
     PRODUCE dt String,
             full_description String,
             guid Guid,
             new_guid Guid
     USING new USQL_Programmability.FullDescriptionProcessor();

OUTPUT @rs1 too@output_file USING Outputters.Text();
```

## <a name="use-user-defined-appliers"></a>使用使用者定義套用器
U SQL 使用者定義套用者可讓您查詢的 hello 外部資料表運算式所傳回的每個資料列的 tooinvoke 自訂 C# 函式。 hello 右邊輸入會評估每個資料列從 hello 左邊的輸入，以及在 hello 最終輸出結合 hello 所產生的資料列。 hello hello APPLY 運算子所產生的資料行清單是 hello hello left 和 hello 右輸入中的資料行集的 hello 組合。

正在叫用使用者定義套用者 hello USQL 選取運算式的一部分。

典型的 hello 呼叫 toohello 使用者定義 applier 似乎 hello 下列：

```
SELECT …
FROM …
CROSS APPLYis used toopass parameters
new MyScript.MyApplier(param1, param2) AS alias(output_param1 string, …);
```

如需在 SELECT 運算式中使用套用器的詳細資訊，請參閱[從 CROSS APPLY 和 OUTER APPLY 選取的 U-SQL SELECT](https://msdn.microsoft.com/library/azure/mt621307.aspx)。

hello 使用者定義 applier 基底類別的定義如下所示：

```
public abstract class IApplier : IUserDefinedOperator
{
protected IApplier();

public abstract IEnumerable<IRow> Apply(IRow input, IUpdatableRow output);
}
```

toodefine 使用者定義套用者，我們需要 toocreate hello`IApplier`介面以 hello [`SqlUserDefinedApplier`] 屬性，這是選擇性的使用者定義的 applier 定義。

```
[SqlUserDefinedApplier]
public class ParserApplier : IApplier
{
    public ParserApplier()
    {
        …
    }

    public override IEnumerable<IRow> Apply(IRow input, IUpdatableRow output)
    {
        …
    }
}
```

* 套用稱為 hello 外部資料表的每個資料列。 它會傳回 hello`IUpdatableRow`輸出資料列集。
* hello 建構函式類別是使用的 toopass 參數 toohello 使用者定義套用者。

**SqlUserDefinedApplier**指出 hello 類型應該要註冊為使用者定義套用者。 這個類別無法繼承。

**SqlUserDefinedApplier** 是使用者定義套用器定義的**選擇性**。


hello 主要的可程式性物件如下所示：

```
public override IEnumerable<IRow> Apply(IRow input, IUpdatableRow output)
```

輸入資料列集會傳遞做為 `IRow` 輸入。 hello 輸出資料列會產生為`IUpdatableRow`輸出介面。

個別資料行名稱由呼叫 hello`IRow`結構描述的方法。

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

tooget hello 實際資料值從傳入的 hello `IRow`，我們使用 get （） 方法 hello`IRow`介面。

```
mycolumn = row.Get<int>("mycolumn")
```

或者，我們使用 hello 結構描述資料行名稱：

```
row.Get<int>(row.Schema[0].Name)
```

hello 輸出值必須設定`IUpdatableRow`輸出：

```
output.Set<int>("mycolumn", mycolumn)
```

它是自訂 appliers 只輸出資料行和值所定義的重要 toounderstand`output.Set`方法呼叫。

藉由呼叫觸發 hello 實際輸出`yield return output.AsReadOnly();`。

hello 使用者定義 applier 參數傳遞 toohello 建構函式。 套用者可以傳回變動數目的需要 toobe 期間 hello applier 呼叫基底 U-SQL 指令碼中定義的資料行。

```
new USQL_Programmability.ParserApplier ("all") AS properties(make string, model string, year string, type string, millage int);
```

以下是 hello 使用者定義 applier 範例：

```
[SqlUserDefinedApplier]
public class ParserApplier : IApplier
{
private string parsingPart;

public ParserApplier(string parsingPart)
{
    if (parsingPart.ToUpper().Contains("ALL")
    || parsingPart.ToUpper().Contains("MAKE")
    || parsingPart.ToUpper().Contains("MODEL")
    || parsingPart.ToUpper().Contains("YEAR")
    || parsingPart.ToUpper().Contains("TYPE")
    || parsingPart.ToUpper().Contains("MILLAGE")
    )
    {
    this.parsingPart = parsingPart;
    }
    else
    {
    throw new ArgumentException("Incorrect parameter. Please use: 'ALL[MAKE|MODEL|TYPE|MILLAGE]'");
    }
}

public override IEnumerable<IRow> Apply(IRow input, IUpdatableRow output)
{

    string[] properties = input.Get<string>("properties").Split(',');

    //  only process with correct number of properties
    if (properties.Count() == 5)
    {

    string make = properties[0];
    string model = properties[1];
    string year = properties[2];
    string type = properties[3];
    int millage = -1;

    // Only return millage if it is number, otherwise, -1
    if (!int.TryParse(properties[4], out millage))
    {
        millage = -1;
    }

    if (parsingPart.ToUpper().Contains("MAKE") || parsingPart.ToUpper().Contains("ALL")) output.Set<string>("make", make);
    if (parsingPart.ToUpper().Contains("MODEL") || parsingPart.ToUpper().Contains("ALL")) output.Set<string>("model", model);
    if (parsingPart.ToUpper().Contains("YEAR") || parsingPart.ToUpper().Contains("ALL")) output.Set<string>("year", year);
    if (parsingPart.ToUpper().Contains("TYPE") || parsingPart.ToUpper().Contains("ALL")) output.Set<string>("type", type);
    if (parsingPart.ToUpper().Contains("MILLAGE") || parsingPart.ToUpper().Contains("ALL")) output.Set<int>("millage", millage);
    }
    yield return output.AsReadOnly();            
}
}
```

以下是 hello 基底 U-SQL 指令碼這個使用者定義套用者：

```
DECLARE @input_file string = @"c:\usql-programmability\car_fleet.tsv";
DECLARE @output_file string = @"c:\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
        stocknumber int,
        vin String,
        properties String
    FROM @input_file USING Extractors.Tsv();

@rs1 =
    SELECT
        r.stocknumber,
        r.vin,
        properties.make,
        properties.model,
        properties.year,
        properties.type,
        properties.millage
    FROM @rs0 AS r
    CROSS APPLY
    new USQL_Programmability.ParserApplier ("all") AS properties(make string, model string, year string, type string, millage int);

OUTPUT @rs1 too@output_file USING Outputters.Text();
```

在此使用的情況下，使用者定義 applier 作為 hello 汽車船隊屬性的逗號分隔值剖析器。 hello 輸入的檔資料列看起來像下列 hello:

```
103 Z1AB2CD123XY45889   Ford,Explorer,2005,SUV,152345
303 Y0AB2CD34XY458890   Shevrolet,Cruise,2010,4Dr,32455
210 X5AB2CD45XY458893   Nissan,Altima,2011,4Dr,74000
```

這是典型的定位點分隔符號 TSV 檔案，其屬性資料行內含製造商、型號等汽車屬性。 這些屬性必須是剖析的 toohello 資料表資料行。 hello 套用提供者也可讓您 toogenerate 動態許多屬性在 hello 產生資料列集，根據所傳入的 hello 參數。 您可以產生所有屬性或僅一組特定的內容。

    …USQL_Programmability.ParserApplier ("all")
    …USQL_Programmability.ParserApplier ("make")
    …USQL_Programmability.ParserApplier ("make&model")

使用者定義套用者 hello 可稱作 applier 物件的新執行個體：

```
CROSS APPLY new MyNameSpace.MyApplier (parameter: “value”) AS alias([columns types]…);
```

或使用的包裝函式的 factory 方法的引動過程 hello:

```c#
    CROSS APPLY MyNameSpace.MyApplier (parameter: “value”) AS alias([columns types]…);
```

## <a name="use-user-defined-combiners"></a>使用使用者定義結合器
使用者定義的結合子或 UDC，可讓您從左邊和右邊資料列集，根據自訂邏輯 toocombine 資料列。 使用者定義結合器會與 COMBINE 運算式搭配使用。

正在叫用的結合子提供有關這兩個 hello 輸入資料列集的 hello 必要資訊的 hello 結合運算式、 群組資料行，hello hello 預期結果的結構描述，以及其他資訊。

toocall 基底的 U-SQL 指令碼中的結合子，我們使用 hello，請使用下列語法：

```
Combine_Expression :=
    'COMBINE' Combine_Input
    'WITH' Combine_Input
    Join_On_Clause
    Produce_Clause
    [Readonly_Clause]
    [Required_Clause]
    USING_Clause.
```

如需詳細資訊，請參閱 [COMBINE 運算式 (U-SQL)](https://msdn.microsoft.com/library/azure/mt621339.aspx)。

toodefine 使用者定義的結合子，我們需要 toocreate hello`ICombiner`介面以 hello [`SqlUserDefinedCombiner`] 屬性，這是選擇性的使用者定義的結合子定義。

基底 `ICombiner` 類別定義：

```
public abstract class ICombiner : IUserDefinedOperator
{
protected ICombiner();
public virtual IEnumerable<IRow> Combine(List<IRowset> inputs,
       IUpdatableRow output);
public abstract IEnumerable<IRow> Combine(IRowset left, IRowset right,
       IUpdatableRow output);
}
```

hello 的自訂實作`ICombiner`介面應該包含 hello 定義`IEnumerable<IRow>`結合覆寫。

```
[SqlUserDefinedCombiner]
public class MyCombiner : ICombiner
{

public override IEnumerable<IRow> Combine(IRowset left, IRowset right,
    IUpdatableRow output)
{
    …
}
}
```

hello **SqlUserDefinedCombiner**屬性會指出 hello 類型應該要註冊為使用者定義的結合子。 這個類別無法繼承。

**SqlUserDefinedCombiner**是使用的 toodefine hello 的結合子模式屬性。 它是使用者定義結合器定義的選擇性屬性。

CombinerMode     Mode

CombinerMode 列舉可以採用下列值的 hello:

* 每個輸出資料列可能相依於 hello 輸入的所有資料列的全文 (0) 的左和右的 hello 相同機碼值。

* Left (1) 的單一輸入資料列從 hello 左取決於每個輸出資料列 (和所有可能列 hello hello 權限與從相同機碼值)。

* 每個輸出資料列而定右 hello 的單一輸入資料列的右邊 (2) (和所有可能列 hello 左 hello 與從相同機碼值)。

* 內部 (3) 的單一輸入取決於每個輸出資料列中的資料列左側和右側 hello 與相同值。

範例：[`SqlUserDefinedCombiner(Mode=CombinerMode.Left)`]


hello 主要的可程式性物件如下：

```c#
    public override IEnumerable<IRow> Combine(IRowset left, IRowset right,
        IUpdatableRow output
```

輸入資料列集會傳遞做為介面的「左邊」和「右邊」 `IRowset` 類型。 這兩個資料列集必須列舉以進行處理。 您可以只列舉每個介面一次，因此我們有 tooenumerate，視快取。

若要快取，我們可以透過執行 LINQ 查詢來建立記憶體結構的 List\<T\> 類型，特別是 List<`IRow`>。 hello 匿名資料型別可以用於期間以及列舉型別。

請參閱[簡介 tooLINQ 查詢 (C#)](https://msdn.microsoft.com/library/bb397906.aspx)如需有關 LINQ 查詢和[IEnumerable\<T\>介面](https://msdn.microsoft.com/library/9eekhta0(v=vs.110).aspx)如需有關 IEnumerable\<T\>介面。

tooget hello 實際資料值從傳入的 hello `IRowset`，我們使用 get （） 方法 hello`IRow`介面。

```
mycolumn = row.Get<int>("mycolumn")
```

個別資料行名稱由呼叫 hello`IRow`結構描述的方法。

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

或使用 hello 結構描述資料行名稱：

```
c# row.Get<int>(row.Schema[0].Name)
```

hello 使用 LINQ 的一般列舉型別看起來像下列 hello:

```
var myRowset =
            (from row in left.Rows
                          select new
                          {
                              Mycolumn = row.Get<int>("mycolumn"),
                          }).ToList();
```

列舉兩個資料列集之後, 我們 tooloop 透過所有資料列。 每個資料列 hello 左資料列集，我們 toofind 符合我們的結合子 hello 條件的所有資料列。

hello 輸出值必須設定`IUpdatableRow`輸出。

```
output.Set<int>("mycolumn", mycolumn)
```

藉由呼叫太觸發 hello 實際輸出`yield return output.AsReadOnly();`。

以下是結合器範例：

```
[SqlUserDefinedCombiner]
public class CombineSales : ICombiner
{

public override IEnumerable<IRow> Combine(IRowset left, IRowset right,
    IUpdatableRow output)
{
    var internetSales =
    (from row in left.Rows
          select new
          {
              ProductKey = row.Get<int>("ProductKey"),
              OrderDateKey = row.Get<int>("OrderDateKey"),
              SalesAmount = row.Get<decimal>("SalesAmount"),
              TaxAmt = row.Get<decimal>("TaxAmt")
          }).ToList();

    var resellerSales =
    (from row in right.Rows
     select new
     {
     ProductKey = row.Get<int>("ProductKey"),
     OrderDateKey = row.Get<int>("OrderDateKey"),
     SalesAmount = row.Get<decimal>("SalesAmount"),
     TaxAmt = row.Get<decimal>("TaxAmt")
     }).ToList();

    foreach (var row_i in internetSales)
    {
    foreach (var row_r in resellerSales)
    {

        if (
        row_i.OrderDateKey > 0
        && row_i.OrderDateKey < row_r.OrderDateKey
        && row_i.OrderDateKey == 20010701
        && (row_r.SalesAmount + row_r.TaxAmt) > 20000)
        {
        output.Set<int>("OrderDateKey", row_i.OrderDateKey);
        output.Set<int>("ProductKey", row_i.ProductKey);
        output.Set<decimal>("Internet_Sales_Amount", row_i.SalesAmount + row_i.TaxAmt);
        output.Set<decimal>("Reseller_Sales_Amount", row_r.SalesAmount + row_r.TaxAmt);
        }

    }
    }
    yield return output.AsReadOnly();
}
}
```

在此使用案例案例中，我們會建置 hello 零售商的分析報表。 hello 目標是的 toofind 成本 $ 20,000 名以上而且的所有產品都銷售透過 hello 較快，透過特定時間範圍內的 hello 規則零售商的網站。

以下是 hello 基底 U-SQL 指令碼。 您可以比較 hello 一般聯結和結合子之間的邏輯：

```sql
DECLARE @LocalURI string = @"\usql-programmability\";

DECLARE @input_file_internet_sales string = @LocalURI+"FactInternetSales.txt";
DECLARE @input_file_reseller_sales string = @LocalURI+"FactResellerSales.txt";
DECLARE @output_file1 string = @LocalURI+"output_file1.tsv";
DECLARE @output_file2 string = @LocalURI+"output_file2.tsv";

@fact_internet_sales =
EXTRACT
    ProductKey int ,
    OrderDateKey int ,
    DueDateKey int ,
    ShipDateKey int ,
    CustomerKey int ,
    PromotionKey int ,
    CurrencyKey int ,
    SalesTerritoryKey int ,
    SalesOrderNumber String ,
    SalesOrderLineNumber  int ,
    RevisionNumber int ,
    OrderQuantity int ,
    UnitPrice decimal ,
    ExtendedAmount decimal,
    UnitPriceDiscountPct float ,
    DiscountAmount float ,
    ProductStandardCost decimal ,
    TotalProductCost decimal ,
    SalesAmount decimal ,
    TaxAmt decimal ,
    Freight decimal ,
    CarrierTrackingNumber String,
    CustomerPONumber String
FROM @input_file_internet_sales
USING Extractors.Text(delimiter:'|', encoding: Encoding.Unicode);

@fact_reseller_sales =
EXTRACT
    ProductKey int ,
    OrderDateKey int ,
    DueDateKey int ,
    ShipDateKey int ,
    ResellerKey int ,
    EmployeeKey int ,
    PromotionKey int ,
    CurrencyKey int ,
    SalesTerritoryKey int ,
    SalesOrderNumber String ,
    SalesOrderLineNumber  int ,
    RevisionNumber int ,
    OrderQuantity int ,
    UnitPrice decimal ,
    ExtendedAmount decimal,
    UnitPriceDiscountPct float ,
    DiscountAmount float ,
    ProductStandardCost decimal ,
    TotalProductCost decimal ,
    SalesAmount decimal ,
    TaxAmt decimal ,
    Freight decimal ,
    CarrierTrackingNumber String,
    CustomerPONumber String
FROM @input_file_reseller_sales
USING Extractors.Text(delimiter:'|', encoding: Encoding.Unicode);

@rs1 =
SELECT
    fis.OrderDateKey,
    fis.ProductKey,
    fis.SalesAmount+fis.TaxAmt AS Internet_Sales_Amount,
    frs.SalesAmount+frs.TaxAmt AS Reseller_Sales_Amount
FROM @fact_internet_sales AS fis
     INNER JOIN @fact_reseller_sales AS frs
     ON fis.ProductKey == frs.ProductKey
WHERE
    fis.OrderDateKey < frs.OrderDateKey
    AND fis.OrderDateKey == 20010701
    AND frs.SalesAmount+frs.TaxAmt > 20000;

@rs2 =
COMBINE @fact_internet_sales AS fis
WITH @fact_reseller_sales AS frs
ON fis.ProductKey == frs.ProductKey
PRODUCE OrderDateKey int,
        ProductKey int,
        Internet_Sales_Amount decimal,
        Reseller_Sales_Amount decimal
USING new USQL_Programmability.CombineSales();

OUTPUT @rs1 too@output_file1 USING Outputters.Tsv();
OUTPUT @rs2 too@output_file2 USING Outputters.Tsv();
```

使用者定義的結合子可稱作 hello applier 物件的新執行個體：

```
USING new MyNameSpace.MyCombiner();
```


或使用的包裝函式的 factory 方法的引動過程 hello:

```
USING MyNameSpace.MyCombiner();
```

## <a name="use-user-defined-reducers"></a>使用使用者定義歸納器

U-SQL 可讓您將自訂的資料列集 reducers toowrite C# 中使用 hello 使用者定義運算子的擴充性架構，並實作 IReducer 介面。

使用者定義減壓器或 UDR，可以使用的 tooeliminate 不必要的資料列在資料擷取 （匯入）。 也可以使用的 toomanipulate 並評估資料列和資料行。 可程式性邏輯為基礎，它也可以定義哪些資料列需要 toobe 擷取。

toodefine UDR 類別，我們需要 toocreate`IReducer`具有選擇性介面`SqlUserDefinedReducer`屬性。

這個類別的介面應該包含 hello 的定義`IEnumerable`介面資料列集覆寫。

```
[SqlUserDefinedReducer]
public class EmptyUserReducer : IReducer
{

    public override IEnumerable<IRow> Reduce(IRowset input, IUpdatableRow output)
    {
        …
    }

}
```

hello **SqlUserDefinedReducer**屬性會指出 hello 類型應該要註冊為使用者定義的減壓器。 這個類別無法繼承。
**SqlUserDefinedReducer** 是使用者定義歸納器之定義的選擇性屬性。 它已用 toodefine IsRecursive 屬性。

* bool     IsRecursive    
* **true** = 表示此歸納器是否等冪

hello 主要的可程式性物件**輸入**和**輸出**。 hello 輸入的物件是使用的 tooenumerate 輸入資料列。 輸出是使用的 tooset 輸出資料列，減少活動的結果。

輸入資料列列舉型別，我們使用 hello`Row.Get`方法。

```
foreach (IRow row in input.Rows)
{
    row.Get<string>("mycolumn");
}
```

hello 參數 hello`Row.Get`方法是傳遞做為 hello 一部分的資料行`PRODUCE`的 hello 類別`REDUCE`hello U-SQL 基底的指令碼陳述式。 我們需要 toouse hello 正確資料類型，這裡以及。

輸出中，使用 hello`output.Set`方法。

它是自訂減壓器只有輸出的值所定義的 hello 的重要 toounderstand`output.Set`方法呼叫。

```
output.Set<string>("mycolumn", guid);
```

hello 實際減壓器的輸出由呼叫觸發`yield return output.AsReadOnly();`。

以下是歸納器範例：

```
[SqlUserDefinedReducer]
public class EmptyUserReducer : IReducer
{

    public override IEnumerable<IRow> Reduce(IRowset input, IUpdatableRow output)
    {
    string guid;
    DateTime dt;
    string user;
    string des;

    foreach (IRow row in input.Rows)
    {
        guid = row.Get<string>("guid");
        dt = row.Get<DateTime>("dt");
        user = row.Get<string>("user");
        des = row.Get<string>("des");

        if (user.Length > 0)
        {
        output.Set<string>("guid", guid);
        output.Set<DateTime>("dt", dt);
        output.Set<string>("user", user);
        output.Set<string>("des", des);

        yield return output.AsReadOnly();
        }
    }
    }

}
```

在此使用案例案例中，hello 減壓器即將略過具有空的使用者名稱的資料列。 每個資料列中資料列集，它會讀取每個必要的資料行，然後評估 hello hello 使用者名稱的長度。 只有當使用者名稱值的長度大於 0，它會輸出 hello 實際資料列。

以下為使用自訂歸納器的基底 U-SQL 指令碼：

```
DECLARE @input_file string = @"\usql-programmability\input_file_reducer.tsv";
DECLARE @output_file string = @"\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
            guid string,
        dt DateTime,
            user String,
            des String
    FROM @input_file 
    USING Extractors.Tsv();

@rs1 =
    REDUCE @rs0 PRESORT guid
    ON guid  
    PRODUCE guid string, dt DateTime, user String, des String
    USING new USQL_Programmability.EmptyUserReducer();

@rs2 =
    SELECT guid AS start_id,
           dt AS start_time,
           DateTime.Now.ToString("M/d/yyyy") AS Nowdate,
           USQL_Programmability.CustomFunctions.GetFiscalPeriodWithCustomType(dt).ToString() AS start_fiscalperiod,
           user,
           des
    FROM @rs1;

OUTPUT @rs2 
    too@output_file 
    USING Outputters.Text();
```
