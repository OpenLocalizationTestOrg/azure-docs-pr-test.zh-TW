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
# <a name="u-sql-programmability-guide"></a><span data-ttu-id="06d06-103">U-SQL 可程式性指南</span><span class="sxs-lookup"><span data-stu-id="06d06-103">U-SQL programmability guide</span></span>

<span data-ttu-id="06d06-104">U-SQL 是為巨量資料類型的工作負載所設計的查詢語言。</span><span class="sxs-lookup"><span data-stu-id="06d06-104">U-SQL is a query language that's designed for big data-type of workloads.</span></span> <span data-ttu-id="06d06-105">Hello 組合 hello 類似 SQL 的宣告式語言 hello 擴充性和可程式性所提供的 C# 的其中一個 hello U-SQL 獨特功能。</span><span class="sxs-lookup"><span data-stu-id="06d06-105">One of hello unique features of U-SQL is hello combination of hello SQL-like declarative language with hello extensibility and programmability that's provided by C#.</span></span> <span data-ttu-id="06d06-106">本指南中，我們會專注於 hello 擴充性和可程式性的啟用 C# 的 hello U-SQL 語言。</span><span class="sxs-lookup"><span data-stu-id="06d06-106">In this guide, we concentrate on hello extensibility and programmability of hello U-SQL language that's enabled by C#.</span></span>

## <a name="requirements"></a><span data-ttu-id="06d06-107">需求</span><span class="sxs-lookup"><span data-stu-id="06d06-107">Requirements</span></span>

<span data-ttu-id="06d06-108">下載及安裝 [Azure Data Lake Tools for Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504)。</span><span class="sxs-lookup"><span data-stu-id="06d06-108">Download and install [Azure Data Lake Tools for Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span></span>

## <a name="get-started-with-u-sql"></a><span data-ttu-id="06d06-109">開始使用 U-SQL</span><span class="sxs-lookup"><span data-stu-id="06d06-109">Get started with U-SQL</span></span>  

<span data-ttu-id="06d06-110">讓我們看看下列 U-SQL 指令碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="06d06-110">Let’s look at hello following U-SQL script:</span></span>

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

<span data-ttu-id="06d06-111">它會定義名為 @a 的資料列集，並且從 @a 建立名為 @results 的資料列集。</span><span class="sxs-lookup"><span data-stu-id="06d06-111">It defines a RowSet called @a and creates a RowSet called @results from @a.</span></span>

## <a name="c-types-and-expressions-in-u-sql-script"></a><span data-ttu-id="06d06-112">U-SQL 指令碼中的 C# 類型和運算式</span><span class="sxs-lookup"><span data-stu-id="06d06-112">C# types and expressions in U-SQL script</span></span>

<span data-ttu-id="06d06-113">U-SQL 運算式是 C# 運算式，與例如 `AND`、`OR` 和 `NOT` 的 U-SQL 邏輯作業合併。</span><span class="sxs-lookup"><span data-stu-id="06d06-113">A U-SQL Expression is a C# expression combined with U-SQL logical operations such `AND`, `OR`, and `NOT`.</span></span> <span data-ttu-id="06d06-114">U-SQL 運算式可以與 SELECT、EXTRACT、WHERE、HAVING、GROUP BY 和 DECLARE 搭配使用。</span><span class="sxs-lookup"><span data-stu-id="06d06-114">U-SQL Expressions can be used with SELECT, EXTRACT, WHERE, HAVING, GROUP BY and DECLARE.</span></span>

<span data-ttu-id="06d06-115">例如，下列指令碼的 hello 剖析字串 hello SELECT 子句中的 DateTime 值。</span><span class="sxs-lookup"><span data-stu-id="06d06-115">For example, hello following script parses a string a DateTime value in hello SELECT clause.</span></span>

```
@results =
    SELECT
        customer,
    amount,
    DateTime.Parse(date) AS date
    FROM @a;    
```

<span data-ttu-id="06d06-116">hello 下列指令碼將字串剖析 DECLARE 陳述式中的 DateTime 值。</span><span class="sxs-lookup"><span data-stu-id="06d06-116">hello following script parses a string a DateTime value in a DECLARE statement.</span></span>

```
DECLARE @d DateTime = ToDateTime.Date("2016/01/01");
```

### <a name="use-c-expressions-for-data-type-conversions"></a><span data-ttu-id="06d06-117">使用 C# 運算式轉換資料類型</span><span class="sxs-lookup"><span data-stu-id="06d06-117">Use C# expressions for data type conversions</span></span>
<span data-ttu-id="06d06-118">hello 下列範例會示範如何日期時間資料轉換，以及在使用 C# 運算式。</span><span class="sxs-lookup"><span data-stu-id="06d06-118">hello following example demonstrates how you can do a datetime data conversion by using C# expressions.</span></span> <span data-ttu-id="06d06-119">在這個特定案例中，字串的日期時間資料會是轉換的 toostandard datetime 午夜 00:00:00 時間標記法。</span><span class="sxs-lookup"><span data-stu-id="06d06-119">In this particular scenario, string datetime data is converted toostandard datetime with midnight 00:00:00 time notation.</span></span>

```
DECLARE @dt String = "2016-07-06 10:23:15";

@rs1 =
    SELECT 
        Convert.ToDateTime(Convert.ToDateTime(@dt).ToString("yyyy-MM-dd")) AS dt,
        dt AS olddt
    FROM @rs0;
OUTPUT @rs1 too@output_file USING Outputters.Text();
```

### <a name="use-c-expressions-for-todays-date"></a><span data-ttu-id="06d06-120">使用 C# 運算式來表示今天的日期</span><span class="sxs-lookup"><span data-stu-id="06d06-120">Use C# expressions for today’s date</span></span>
<span data-ttu-id="06d06-121">toopull 今天的日期，我們可以使用下列 C# 運算式的 hello:</span><span class="sxs-lookup"><span data-stu-id="06d06-121">toopull today’s date, we can use hello following C# expression:</span></span>

```
DateTime.Now.ToString("M/d/yyyy")
```

<span data-ttu-id="06d06-122">以下是如何的範例 toouse 指令碼中的這個運算式：</span><span class="sxs-lookup"><span data-stu-id="06d06-122">Here's an example of how toouse this expression in a script:</span></span>

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



## <a name="using-net-assemblies"></a><span data-ttu-id="06d06-123">使用 .NET 組件</span><span class="sxs-lookup"><span data-stu-id="06d06-123">Using .NET assemblies</span></span>
<span data-ttu-id="06d06-124">U SQL 的擴充性模型非常依賴 hello 能力 tooadd 自訂程式碼。</span><span class="sxs-lookup"><span data-stu-id="06d06-124">U-SQL’s extensibility model relies heavily on hello ability tooadd custom code.</span></span> <span data-ttu-id="06d06-125">目前，U-SQL 提供簡單的方法 tooadd 您自己的 Microsoft。（尤其是，C#） 以網路為基礎的程式碼。</span><span class="sxs-lookup"><span data-stu-id="06d06-125">Currently, U-SQL provides you with easy ways tooadd your own Microsoft .NET-based code (in particular, C#).</span></span> <span data-ttu-id="06d06-126">不過，您也可以新增以其他 .NET 語言 (例如 VB.NET 或 F#) 撰寫的自訂程式碼。</span><span class="sxs-lookup"><span data-stu-id="06d06-126">However, you can also add custom code that's written in other .NET languages, such as VB.NET or F#.</span></span> 

### <a name="register-a-net-assembly"></a><span data-ttu-id="06d06-127">註冊 .NET 組件</span><span class="sxs-lookup"><span data-stu-id="06d06-127">Register a .NET assembly</span></span>

<span data-ttu-id="06d06-128">使用 hello CREATE ASSEMBLY 陳述式 tooplace U SQL 資料庫到.NET 組件。</span><span class="sxs-lookup"><span data-stu-id="06d06-128">Use hello CREATE ASSEMBLY statement tooplace a .NET assembly into a U-SQL Database.</span></span> <span data-ttu-id="06d06-129">一旦將組件中的資料庫，U-SQL 指令碼可以使用 hello 參考組件陳述式來使用這些組件。</span><span class="sxs-lookup"><span data-stu-id="06d06-129">Once an assembly is in a database, U-SQL scripts can use those assemblies by using hello REFERENCE ASSEMBLY statement.</span></span> 

<span data-ttu-id="06d06-130">hello 下列程式碼會示範如何 tooregister 組件：</span><span class="sxs-lookup"><span data-stu-id="06d06-130">hello following code shows how tooregister an assembly:</span></span>

```
CREATE ASSEMBLY MyDB.[MyAssembly]
    FROM "/myassembly.dll";
```

<span data-ttu-id="06d06-131">hello 下列程式碼會示範如何 tooreference 組件：</span><span class="sxs-lookup"><span data-stu-id="06d06-131">hello following code shows how tooreference an assembly:</span></span>

```
REFERENCE ASSEMBLY MyDB.[MyAssembly];
```

<span data-ttu-id="06d06-132">請參閱 hello[組件註冊指示](https://blogs.msdn.microsoft.com/azuredatalake/2016/08/26/how-to-register-u-sql-assemblies-in-your-u-sql-catalog/)涵蓋本主題會更詳細地。</span><span class="sxs-lookup"><span data-stu-id="06d06-132">Consult hello [assembly registration instructions](https://blogs.msdn.microsoft.com/azuredatalake/2016/08/26/how-to-register-u-sql-assemblies-in-your-u-sql-catalog/) that covers this topic in greater detail.</span></span>


### <a name="use-assembly-versioning"></a><span data-ttu-id="06d06-133">使用組件版本控制</span><span class="sxs-lookup"><span data-stu-id="06d06-133">Use assembly versioning</span></span>
<span data-ttu-id="06d06-134">目前，U-SQL 使用 hello.NET Framework 4.5 版。</span><span class="sxs-lookup"><span data-stu-id="06d06-134">Currently, U-SQL uses hello .NET Framework version 4.5.</span></span> <span data-ttu-id="06d06-135">因此請確定您自己的組件會與該新版 hello 執行階段相容。</span><span class="sxs-lookup"><span data-stu-id="06d06-135">So ensure that your own assemblies are compatible with that version of hello runtime.</span></span>

<span data-ttu-id="06d06-136">如前面所述，U-SQL 會執行 64 位元 (x64) 格式的程式碼。</span><span class="sxs-lookup"><span data-stu-id="06d06-136">As mentioned earlier, U-SQL runs code in a 64-bit (x64) format.</span></span> <span data-ttu-id="06d06-137">因此請確定您的程式碼編譯的 toorun x64 上。</span><span class="sxs-lookup"><span data-stu-id="06d06-137">So make sure that your code is compiled toorun on x64.</span></span> <span data-ttu-id="06d06-138">否則，您會收到 hello 不正確的格式錯誤稍早所示。</span><span class="sxs-lookup"><span data-stu-id="06d06-138">Otherwise you get hello incorrect format error shown earlier.</span></span>

<span data-ttu-id="06d06-139">每個上傳的組件 DLL 和資源檔，例如不同的執行階段、原生組件或組態檔中，最多可達 400 MB。</span><span class="sxs-lookup"><span data-stu-id="06d06-139">Each uploaded assembly DLL and resource file, such as a different runtime, a native assembly, or a config file, can be at most 400 MB.</span></span> <span data-ttu-id="06d06-140">hello 的已部署的資源，不論是透過部署資源，或是透過參考 tooassemblies 及其他檔案，大小總計不得超過 3 GB。</span><span class="sxs-lookup"><span data-stu-id="06d06-140">hello total size of deployed resources, either via DEPLOY RESOURCE or via references tooassemblies and their additional files, cannot exceed 3 GB.</span></span>

<span data-ttu-id="06d06-141">最後請注意，每一個 U-SQL 資料庫所包含的任何指定組件只能有一個版本。</span><span class="sxs-lookup"><span data-stu-id="06d06-141">Finally, note that each U-SQL database can only contain one version of any given assembly.</span></span> <span data-ttu-id="06d06-142">例如，如果您需要第 7 版和第 8 版的 hello NewtonSoft Json.Net 程式庫，您需要 tooregister 兩個不同資料庫中。</span><span class="sxs-lookup"><span data-stu-id="06d06-142">For example, if you need both version 7 and version 8 of hello NewtonSoft Json.Net library, you need tooregister them in two different databases.</span></span> <span data-ttu-id="06d06-143">此外，每個指令碼只能參考指定的組件 DLL tooone 版本。</span><span class="sxs-lookup"><span data-stu-id="06d06-143">Furthermore, each script can only refer tooone version of a given assembly DLL.</span></span> <span data-ttu-id="06d06-144">在這一方面，U-SQL 遵循 hello C# 組件管理和版本控制語意。</span><span class="sxs-lookup"><span data-stu-id="06d06-144">In this respect, U-SQL follows hello C# assembly management and versioning semantics.</span></span>


## <a name="use-user-defined-functions-udf"></a><span data-ttu-id="06d06-145">使用使用者定義函式：UDF</span><span class="sxs-lookup"><span data-stu-id="06d06-145">Use user-defined functions: UDF</span></span>
<span data-ttu-id="06d06-146">U SQL 使用者定義函數或 UDF，進行程式設計可接受參數、 執行動作 （如複雜計算），以及傳回該動作所得值的 hello 結果的常式。</span><span class="sxs-lookup"><span data-stu-id="06d06-146">U-SQL user-defined functions, or UDF, are programming routines that accept parameters, perform an action (such as a complex calculation), and return hello result of that action as a value.</span></span> <span data-ttu-id="06d06-147">hello 傳回 UDF 的值只能是單一純量。</span><span class="sxs-lookup"><span data-stu-id="06d06-147">hello return value of UDF can only be a single scalar.</span></span> <span data-ttu-id="06d06-148">U-SQL UDF 可以和任何其他 C# 純量函式一樣，在 U-SQL 基底指令碼中進行呼叫。</span><span class="sxs-lookup"><span data-stu-id="06d06-148">U-SQL UDF can be called in U-SQL base script like any other C# scalar function.</span></span>

<span data-ttu-id="06d06-149">我們建議您將 U-SQL 使用者定義函式初始化為**公用**且**靜態**的函式。</span><span class="sxs-lookup"><span data-stu-id="06d06-149">We recommend that you initialize U-SQL user-defined functions as **public** and **static**.</span></span>

```
public static string MyFunction(string param1)
{
    return "my result";
}
```

<span data-ttu-id="06d06-150">第一個讓我們看看 hello 建立 UDF 的簡單的範例。</span><span class="sxs-lookup"><span data-stu-id="06d06-150">First let’s look at hello simple example of creating a UDF.</span></span>

<span data-ttu-id="06d06-151">在此使用案例案例中，我們需要 toodetermine hello 會計週期，包括 hello 會計季度和會計月份的 hello 首次登入 hello 特定使用者。</span><span class="sxs-lookup"><span data-stu-id="06d06-151">In this use-case scenario, we need toodetermine hello fiscal period, including hello fiscal quarter and fiscal month of hello first sign-in for hello specific user.</span></span> <span data-ttu-id="06d06-152">hello 我們的案例中的 hello 年的第一個會計月份為六月。</span><span class="sxs-lookup"><span data-stu-id="06d06-152">hello first fiscal month of hello year in our scenario is June.</span></span>

<span data-ttu-id="06d06-153">toocalculate 會計週期，我們引進下列 C# 函式的 hello:</span><span class="sxs-lookup"><span data-stu-id="06d06-153">toocalculate fiscal period, we introduce hello following C# function:</span></span>

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

<span data-ttu-id="06d06-154">它只會計算會計月份和季度，並傳回字串值。</span><span class="sxs-lookup"><span data-stu-id="06d06-154">It simply calculates fiscal month and quarter and returns a string value.</span></span> <span data-ttu-id="06d06-155">年 6 月，hello 的第一個月 hello 第一個會計季度，我們使用 「 Q1:P1"。</span><span class="sxs-lookup"><span data-stu-id="06d06-155">For June, hello first month of hello first fiscal quarter, we use "Q1:P1".</span></span> <span data-ttu-id="06d06-156">七月，我們使用「Q1:P2」，以此類推。</span><span class="sxs-lookup"><span data-stu-id="06d06-156">For July, we use "Q1:P2", and so on.</span></span>

<span data-ttu-id="06d06-157">這是一般 C# 函式，我們處於持續 toouse 我們 U-SQL 專案。</span><span class="sxs-lookup"><span data-stu-id="06d06-157">This is a regular C# function that we are going toouse in our U-SQL project.</span></span>

<span data-ttu-id="06d06-158">在此案例中的 hello 程式碼後置區段外觀如下：</span><span class="sxs-lookup"><span data-stu-id="06d06-158">Here is how hello code-behind section looks in this scenario:</span></span>

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

<span data-ttu-id="06d06-159">現在我們 toocall 此函式從 hello 基底 U-SQL 指令碼。</span><span class="sxs-lookup"><span data-stu-id="06d06-159">Now we are going toocall this function from hello base U-SQL script.</span></span> <span data-ttu-id="06d06-160">toodo，我們有 tooprovide hello 函式，包括 hello 命名空間，在此案例中 NameSpace.Class.Function(parameter) 的完整的名稱。</span><span class="sxs-lookup"><span data-stu-id="06d06-160">toodo this, we have tooprovide a fully qualified name for hello function, including hello namespace, which in this case is NameSpace.Class.Function(parameter).</span></span>

```
USQL_Programmability.CustomFunctions.GetFiscalPeriod(dt)
```

<span data-ttu-id="06d06-161">以下是 hello 實際 U-SQL 基底的指令碼：</span><span class="sxs-lookup"><span data-stu-id="06d06-161">Following is hello actual U-SQL base script:</span></span>

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

<span data-ttu-id="06d06-162">以下是 hello hello 執行指令碼的輸出檔：</span><span class="sxs-lookup"><span data-stu-id="06d06-162">Following is hello output file of hello script execution:</span></span>

```
0d8b9630-d5ca-11e5-8329-251efa3a2941,2016-02-11T07:04:17.2630000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User1",""

20843640-d771-11e5-b87b-8b7265c75a44,2016-02-11T07:04:17.2630000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User2",""

301f23d2-d690-11e5-9a98-4b4f60a1836f,2016-02-11T09:01:33.9720000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User3",""
```

<span data-ttu-id="06d06-163">這個範例示範 U-SQL 中內嵌 UDF 的簡易用法。</span><span class="sxs-lookup"><span data-stu-id="06d06-163">This example demonstrates a simple usage of inline UDF in U-SQL.</span></span>

### <a name="keep-state-between-udf-invocations"></a><span data-ttu-id="06d06-164">在 UDF 的引動過程之間保持狀態</span><span class="sxs-lookup"><span data-stu-id="06d06-164">Keep state between UDF invocations</span></span>
<span data-ttu-id="06d06-165">U-SQL C# 程式設計物件可以是更複雜，利用透過 hello 程式碼後置全域變數的互動性。</span><span class="sxs-lookup"><span data-stu-id="06d06-165">U-SQL C# programmability objects can be more sophisticated, utilizing interactivity through hello code-behind global variables.</span></span> <span data-ttu-id="06d06-166">讓我們看看下列商務案例中使用案例的 hello。</span><span class="sxs-lookup"><span data-stu-id="06d06-166">Let’s look at hello following business use-case scenario.</span></span>

<span data-ttu-id="06d06-167">在大型組織中，使用者可以切換使用各種內部應用程式。</span><span class="sxs-lookup"><span data-stu-id="06d06-167">In large organizations, users can switch between varieties of internal applications.</span></span> <span data-ttu-id="06d06-168">這些可能包括 Microsoft Dynamics CRM、PowerBI 等等。</span><span class="sxs-lookup"><span data-stu-id="06d06-168">These can include Microsoft Dynamics CRM, PowerBI, and so on.</span></span> <span data-ttu-id="06d06-169">客戶可能會想 tooapply 使用者如何切換不同的應用程式，哪些 hello 使用量趨勢，以及等等的遙測分析。</span><span class="sxs-lookup"><span data-stu-id="06d06-169">Customers might want tooapply a telemetry analysis of how users switch between different applications, what hello usage trends are, and so on.</span></span> <span data-ttu-id="06d06-170">hello hello 的商務目標是 toooptimize 應用程式使用情形。</span><span class="sxs-lookup"><span data-stu-id="06d06-170">hello goal for hello business is toooptimize application usage.</span></span> <span data-ttu-id="06d06-171">他們也可能會想 toocombine 不同的應用程式或特定的登入常式。</span><span class="sxs-lookup"><span data-stu-id="06d06-171">They also might want toocombine different applications or specific sign-on routines.</span></span>

<span data-ttu-id="06d06-172">tooachieve 此目標中，我們有 toodetermine 工作階段識別碼和 hello 發生的最後一個工作階段之間的延遲時間。</span><span class="sxs-lookup"><span data-stu-id="06d06-172">tooachieve this goal, we have toodetermine session IDs and lag time between hello last session that occurred.</span></span>

<span data-ttu-id="06d06-173">我們需要 toofind 先前登入，然後將所產生的 toohello 此登入 tooall 工作階段指派相同的應用程式。</span><span class="sxs-lookup"><span data-stu-id="06d06-173">We need toofind a previous sign-in and then assign this sign-in tooall sessions that are being generated toohello same application.</span></span> <span data-ttu-id="06d06-174">hello 第一項挑戰是 U-SQL 基底的指令碼不允許我們 tooapply 計算透過 LAG 函式的已計算資料行。</span><span class="sxs-lookup"><span data-stu-id="06d06-174">hello first challenge is that U-SQL base script doesn't allow us tooapply calculations over already-calculated columns with LAG function.</span></span> <span data-ttu-id="06d06-175">hello 第二個挑戰是我們有 tookeep hello 特定的工作階段內 hello 的所有工作階段的時間週期相同。</span><span class="sxs-lookup"><span data-stu-id="06d06-175">hello second challenge is that we have tookeep hello specific session for all sessions within hello same time period.</span></span>

<span data-ttu-id="06d06-176">toosolve 這個問題，我們的程式碼後置區段內使用的全域變數： `static public string globalSession;`。</span><span class="sxs-lookup"><span data-stu-id="06d06-176">toosolve this problem, we use a global variable inside a code-behind section: `static public string globalSession;`.</span></span>

<span data-ttu-id="06d06-177">這個全域變數會是我們的指令碼執行期間套用的 toohello 整個資料列集。</span><span class="sxs-lookup"><span data-stu-id="06d06-177">This global variable is applied toohello entire rowset during our script execution.</span></span>

<span data-ttu-id="06d06-178">以下是我們 U-SQL 程式 hello 程式碼後置區段：</span><span class="sxs-lookup"><span data-stu-id="06d06-178">Here is hello code-behind section of our U-SQL program:</span></span>

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

<span data-ttu-id="06d06-179">此範例中會顯示 hello 全域變數`static public string globalSession;`hello 內使用`getStampUserSession`函式，並取得重新初始化每個時間 hello 參數變更的工作階段。</span><span class="sxs-lookup"><span data-stu-id="06d06-179">This example shows hello global variable `static public string globalSession;` used inside hello `getStampUserSession` function and getting reinitialized each time hello Session parameter is changed.</span></span>

<span data-ttu-id="06d06-180">hello U-SQL 基底的指令碼如下所示：</span><span class="sxs-lookup"><span data-stu-id="06d06-180">hello U-SQL base script is as follows:</span></span>

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

<span data-ttu-id="06d06-181">函式`USQLApplication21.UserSession.getStampUserSession(UserSessionTimestamp)`hello 第二個記憶體資料列集計算期間會呼叫這裡。</span><span class="sxs-lookup"><span data-stu-id="06d06-181">Function `USQLApplication21.UserSession.getStampUserSession(UserSessionTimestamp)` is called here during hello second memory rowset calculation.</span></span> <span data-ttu-id="06d06-182">它會傳遞 hello`UserSessionTimestamp`資料行，並傳回 hello 值直到`UserSessionTimestamp`已變更。</span><span class="sxs-lookup"><span data-stu-id="06d06-182">It passes hello `UserSessionTimestamp` column and returns hello value until `UserSessionTimestamp` has changed.</span></span>

<span data-ttu-id="06d06-183">hello 輸出檔如下所示：</span><span class="sxs-lookup"><span data-stu-id="06d06-183">hello output file is as follows:</span></span>

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

<span data-ttu-id="06d06-184">此範例示範更複雜的使用案例案例，我們使用全域變數套用的 toohello 整個記憶體的資料列集的程式碼後置區段內。</span><span class="sxs-lookup"><span data-stu-id="06d06-184">This example demonstrates a more complicated use-case scenario in which we use a global variable inside a code-behind section that's applied toohello entire memory rowset.</span></span>

## <a name="use-user-defined-types-udt"></a><span data-ttu-id="06d06-185">使用使用者定義的類型：UDT</span><span class="sxs-lookup"><span data-stu-id="06d06-185">Use user-defined types: UDT</span></span>
<span data-ttu-id="06d06-186">使用者定義類型 (UDT) 是 U-SQL 的另一個可程式性功能。</span><span class="sxs-lookup"><span data-stu-id="06d06-186">User-defined types, or UDT, is another programmability feature of U-SQL.</span></span> <span data-ttu-id="06d06-187">U-SQL UDT 的作用就像一般的 C# 使用者定義類型。</span><span class="sxs-lookup"><span data-stu-id="06d06-187">U-SQL UDT acts like a regular C# user-defined type.</span></span> <span data-ttu-id="06d06-188">C# 是強型別的語言，允許 hello 使用內建和自訂的使用者定義型別。</span><span class="sxs-lookup"><span data-stu-id="06d06-188">C# is a strongly typed language that allows hello use of built-in and custom user-defined types.</span></span>

<span data-ttu-id="06d06-189">U-SQL 隱含無法序列化或還原序列化任意 Udt 個資料列集中的頂點傳遞 hello UDT 時。</span><span class="sxs-lookup"><span data-stu-id="06d06-189">U-SQL cannot implicitly serialize or de-serialize arbitrary UDTs when hello UDT is passed between vertices in rowsets.</span></span> <span data-ttu-id="06d06-190">這表示該 hello 使用者 tooprovide 明確的格式器使用 hello IFormatter 介面。</span><span class="sxs-lookup"><span data-stu-id="06d06-190">This means that hello user has tooprovide an explicit formatter by using hello IFormatter interface.</span></span> <span data-ttu-id="06d06-191">如此可提供 hello U-SQL 序列化和還原序列化 hello UDT 的方法。</span><span class="sxs-lookup"><span data-stu-id="06d06-191">This provides U-SQL with hello serialize and de-serialize methods for hello UDT.</span></span>

> [!NOTE]
> <span data-ttu-id="06d06-192">U SQL 的內建擷取器和 outputters 目前無法序列化或還原序列化 UDT 資料 tooor 從甚至以 hello IFormatter 組的檔案。</span><span class="sxs-lookup"><span data-stu-id="06d06-192">U-SQL’s built-in extractors and outputters currently cannot serialize or de-serialize UDT data tooor from files even with hello IFormatter set.</span></span> <span data-ttu-id="06d06-193">因此，當您撰寫 UDT 資料 tooa 檔案以 hello 輸出陳述式，或讀取以擷取程式 」，您有 toopass 它做為字串或位元組陣列。</span><span class="sxs-lookup"><span data-stu-id="06d06-193">So when you're writing UDT data tooa file with hello OUTPUT statement, or reading it with an extractor, you have toopass it as a string or byte array.</span></span> <span data-ttu-id="06d06-194">然後呼叫 hello 序列化，並明確地還原序列化程式碼 （也就是 hello UDT 的 tostring （） 方法）。</span><span class="sxs-lookup"><span data-stu-id="06d06-194">Then you call hello serialization and deserialization code (that is, hello UDT’s ToString() method) explicitly.</span></span> <span data-ttu-id="06d06-195">使用者定義的擷取器和其他 hello 上的 outputters，另一方面，可以讀取和寫入 Udt。</span><span class="sxs-lookup"><span data-stu-id="06d06-195">User-defined extractors and outputters, on hello other hand, can read and write UDTs.</span></span>

<span data-ttu-id="06d06-196">如果我們嘗試 toouse UDT 中擷取程式 」 或 「 OUTPUTTER （從上一個選取），如下所示：</span><span class="sxs-lookup"><span data-stu-id="06d06-196">If we try toouse UDT in EXTRACTOR or OUTPUTTER (out of previous SELECT), as shown here:</span></span>

```
@rs1 =
    SELECT 
        MyNameSpace.Myfunction_Returning_UDT(filed1) AS myfield
    FROM @rs0;

OUTPUT @rs1 
    too@output_file 
    USING Outputters.Text();
```

<span data-ttu-id="06d06-197">我們收到 hello 下列錯誤：</span><span class="sxs-lookup"><span data-stu-id="06d06-197">We receive hello following error:</span></span>

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

<span data-ttu-id="06d06-198">toowork UDT outputter 中的，我們有 tooserialize 它與 toostring hello tostring （） 方法，或建立自訂 outputter。</span><span class="sxs-lookup"><span data-stu-id="06d06-198">toowork with UDT in outputter, we either have tooserialize it toostring with hello ToString() method or create a custom outputter.</span></span>

<span data-ttu-id="06d06-199">UDT 目前不能用於 GROUP BY。</span><span class="sxs-lookup"><span data-stu-id="06d06-199">UDTs currently cannot be used in GROUP BY.</span></span> <span data-ttu-id="06d06-200">如果 UDT 用於 GROUP BY，則會擲回下列錯誤 hello:</span><span class="sxs-lookup"><span data-stu-id="06d06-200">If UDT is used in GROUP BY, hello following error is thrown:</span></span>

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

<span data-ttu-id="06d06-201">我們必須 toodefine UDT:</span><span class="sxs-lookup"><span data-stu-id="06d06-201">toodefine a UDT, we have to:</span></span>

* <span data-ttu-id="06d06-202">加入下列命名空間的 hello:</span><span class="sxs-lookup"><span data-stu-id="06d06-202">Add hello following namespaces:</span></span>

```
using Microsoft.Analytics.Interfaces
using System.IO;
```

* <span data-ttu-id="06d06-203">新增`Microsoft.Analytics.Interfaces`，所需之 hello UDT 介面。</span><span class="sxs-lookup"><span data-stu-id="06d06-203">Add `Microsoft.Analytics.Interfaces`, which is required for hello UDT interfaces.</span></span> <span data-ttu-id="06d06-204">此外，`System.IO`可能需要的 toodefine hello IFormatter 介面。</span><span class="sxs-lookup"><span data-stu-id="06d06-204">In addition, `System.IO` might be needed toodefine hello IFormatter interface.</span></span>

* <span data-ttu-id="06d06-205">使用 SqlUserDefinedType 屬性來定義使用者定義類型。</span><span class="sxs-lookup"><span data-stu-id="06d06-205">Define a used-defined type with SqlUserDefinedType attribute.</span></span>

<span data-ttu-id="06d06-206">**SqlUserDefinedType** U-SQL 中是使用的 toomark 為使用者定義型別 (UDT) 的組件中的類型定義。</span><span class="sxs-lookup"><span data-stu-id="06d06-206">**SqlUserDefinedType** is used toomark a type definition in an assembly as a user-defined type (UDT) in U-SQL.</span></span> <span data-ttu-id="06d06-207">hello hello 屬性上的屬性會反映 hello UDT hello 實體特性。</span><span class="sxs-lookup"><span data-stu-id="06d06-207">hello properties on hello attribute reflect hello physical characteristics of hello UDT.</span></span> <span data-ttu-id="06d06-208">這個類別無法繼承。</span><span class="sxs-lookup"><span data-stu-id="06d06-208">This class cannot be inherited.</span></span>

<span data-ttu-id="06d06-209">SqlUserDefinedType 是 UDT 定義的必要屬性 (attribute)。</span><span class="sxs-lookup"><span data-stu-id="06d06-209">SqlUserDefinedType is a required attribute for UDT definition.</span></span>

<span data-ttu-id="06d06-210">hello 類別建構 hello 函式：</span><span class="sxs-lookup"><span data-stu-id="06d06-210">hello constructor of hello class:</span></span>  

* <span data-ttu-id="06d06-211">SqlUserDefinedTypeAttribute (類型格式器)</span><span class="sxs-lookup"><span data-stu-id="06d06-211">SqlUserDefinedTypeAttribute (type formatter)</span></span>

* <span data-ttu-id="06d06-212">型別格式器： 需要參數 toodefine UDT 格式器-具體來說，hello 類型 hello`IFormatter`介面必須這裡傳遞。</span><span class="sxs-lookup"><span data-stu-id="06d06-212">Type formatter: Required parameter toodefine an UDT formatter--specifically, hello type of hello `IFormatter` interface must be passed here.</span></span>

```
[SqlUserDefinedType(typeof(MyTypeFormatter))]
public class MyType
{ … }
```

* <span data-ttu-id="06d06-213">典型的 UDT 也需要 hello IFormatter 介面定義，hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="06d06-213">Typical UDT also requires definition of hello IFormatter interface, as shown in hello following example:</span></span>

```
public class MyTypeFormatter : IFormatter<MyType>
{
    public void Serialize(MyType instance, IColumnWriter writer, ISerializationContext context)
    { … }

    public MyType Deserialize(IColumnReader reader, ISerializationContext context)
    { … }
}
```

<span data-ttu-id="06d06-214">hello`IFormatter`介面序列化和還原序列化物件圖形與 hello 根型別\<typeparamref 名稱 ="T">。</span><span class="sxs-lookup"><span data-stu-id="06d06-214">hello `IFormatter` interface serializes and de-serializes an object graph with hello root type of \<typeparamref name="T">.</span></span>

<span data-ttu-id="06d06-215">\<typeparam 名稱 ="T"> hello hello 物件圖形 tooserialize 的根型別和還原序列化。</span><span class="sxs-lookup"><span data-stu-id="06d06-215">\<typeparam name="T">hello root type for hello object graph tooserialize and de-serialize.</span></span>

* <span data-ttu-id="06d06-216">**還原序列化**: hello hello 提供資料流上的資料會取消序列化和重新組成 hello 的物件圖形。</span><span class="sxs-lookup"><span data-stu-id="06d06-216">**Deserialize**: De-serializes hello data on hello provided stream and reconstitutes hello graph of objects.</span></span>

* <span data-ttu-id="06d06-217">**序列化**： 序列化物件或圖形的物件，以指定根 toohello 提供資料流的 hello。</span><span class="sxs-lookup"><span data-stu-id="06d06-217">**Serialize**: Serializes an object, or graph of objects, with hello given root toohello provided stream.</span></span>

<span data-ttu-id="06d06-218">`MyType`執行個體： hello 型別的執行個體。</span><span class="sxs-lookup"><span data-stu-id="06d06-218">`MyType` instance: Instance of hello type.</span></span>  
<span data-ttu-id="06d06-219">`IColumnWriter`寫入器 /`IColumnReader`讀取器： hello 基礎資料行的資料流。</span><span class="sxs-lookup"><span data-stu-id="06d06-219">`IColumnWriter` writer / `IColumnReader` reader: hello underlying column stream.</span></span>  
<span data-ttu-id="06d06-220">`ISerializationContext`內容： 定義一組旗標會指定序列化期間的 hello hello 資料流的來源或目的端內容的列舉。</span><span class="sxs-lookup"><span data-stu-id="06d06-220">`ISerializationContext` context: Enum that defines a set of flags that specifies hello source or destination context for hello stream during serialization.</span></span>

* <span data-ttu-id="06d06-221">**中繼**： 指定該 hello 來源或目的地的內容不是持續性存放區。</span><span class="sxs-lookup"><span data-stu-id="06d06-221">**Intermediate**: Specifies that hello source or destination context is not a persisted store.</span></span>

* <span data-ttu-id="06d06-222">**持續性**： 指定該 hello 來源或目的地的內容是持續性存放區。</span><span class="sxs-lookup"><span data-stu-id="06d06-222">**Persistence**: Specifies that hello source or destination context is a persisted store.</span></span>

<span data-ttu-id="06d06-223">做為一般的 C# 類型，U-SQL UDT 定義可包括 +/==/!= 等運算子的覆寫。</span><span class="sxs-lookup"><span data-stu-id="06d06-223">As a regular C# type, a U-SQL UDT definition can include overrides for operators such as +/==/!=.</span></span> <span data-ttu-id="06d06-224">它也可以包含靜態方法。</span><span class="sxs-lookup"><span data-stu-id="06d06-224">It can also include static methods.</span></span> <span data-ttu-id="06d06-225">例如，如果我們 toouse 此 UDT 當做參數 tooa U SQL MIN 彙總函式，我們有 toodefine < 運算子覆寫。</span><span class="sxs-lookup"><span data-stu-id="06d06-225">For example, if we are going toouse this UDT as a parameter tooa U-SQL MIN aggregate function, we have toodefine < operator override.</span></span>

<span data-ttu-id="06d06-226">稍早在本指南中，我們會示範會計週期的識別從 hello hello 格式 Qn:Pn (Q1:P10) 中的特定日期的範例。</span><span class="sxs-lookup"><span data-stu-id="06d06-226">Earlier in this guide, we demonstrated an example for fiscal period identification from hello specific date in hello format Qn:Pn (Q1:P10).</span></span> <span data-ttu-id="06d06-227">hello 下列範例顯示如何 toodefine 自訂型別會計週期的值。</span><span class="sxs-lookup"><span data-stu-id="06d06-227">hello following example shows how toodefine a custom type for fiscal period values.</span></span>

<span data-ttu-id="06d06-228">以下是具有自訂 UDT 和 IFormatter 介面的程式碼後置區段範例︰</span><span class="sxs-lookup"><span data-stu-id="06d06-228">Following is an example of a code-behind section with custom UDT and IFormatter interface:</span></span>

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

<span data-ttu-id="06d06-229">hello 定義的類型包含兩個數字： 季度和月份。</span><span class="sxs-lookup"><span data-stu-id="06d06-229">hello defined type includes two numbers: quarter and month.</span></span> <span data-ttu-id="06d06-230">運算子 ==/!=/>/< 和靜態方法 ToString() 定義於此。</span><span class="sxs-lookup"><span data-stu-id="06d06-230">Operators ==/!=/>/< and static method ToString() are defined here.</span></span>

<span data-ttu-id="06d06-231">如先前所述，UDT 可用於 SELECT 運算式中，但不能用在沒有自訂序列化的 OUTPUTTER/EXTRACTOR。</span><span class="sxs-lookup"><span data-stu-id="06d06-231">As mentioned earlier, UDT can be used in SELECT expressions, but cannot be used in OUTPUTTER/EXTRACTOR without custom serialization.</span></span> <span data-ttu-id="06d06-232">它擁有 toobe 序列化為具有 tostring （） 的字串，或與自訂 OUTPUTTER/抽選程式搭配使用。</span><span class="sxs-lookup"><span data-stu-id="06d06-232">It either has toobe serialized as a string with ToString() or used with a custom OUTPUTTER/EXTRACTOR.</span></span>

<span data-ttu-id="06d06-233">現在我們來討論一下 UDT 的使用方式。</span><span class="sxs-lookup"><span data-stu-id="06d06-233">Now let’s discuss usage of UDT.</span></span> <span data-ttu-id="06d06-234">在程式碼後置 區段中，我們可以變更我們 GetFiscalPeriod 函式 toohello 下列：</span><span class="sxs-lookup"><span data-stu-id="06d06-234">In a code-behind section, we changed our GetFiscalPeriod function toohello following:</span></span>

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

<span data-ttu-id="06d06-235">如您所見，它會傳回 hello 我們 FiscalPeriod 類型值。</span><span class="sxs-lookup"><span data-stu-id="06d06-235">As you can see, it returns hello value of our FiscalPeriod type.</span></span>

<span data-ttu-id="06d06-236">在這裡，我們會提供如何 toouse 它進一步 U-SQL 基底的指令碼中的範例。</span><span class="sxs-lookup"><span data-stu-id="06d06-236">Here we provide an example of how toouse it further in U-SQL base script.</span></span> <span data-ttu-id="06d06-237">這個範例會示範從 U-SQL 指令碼叫用 UDT 的不同方式。</span><span class="sxs-lookup"><span data-stu-id="06d06-237">This example demonstrates different forms of UDT invocation from U-SQL script.</span></span>

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

<span data-ttu-id="06d06-238">以下是完整程式碼後置區段的範例︰</span><span class="sxs-lookup"><span data-stu-id="06d06-238">Here's an example of a full code-behind section:</span></span>

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

## <a name="use-user-defined-aggregates-udagg"></a><span data-ttu-id="06d06-239">使用使用者定義彙總：UDAGG</span><span class="sxs-lookup"><span data-stu-id="06d06-239">Use user-defined aggregates: UDAGG</span></span>
<span data-ttu-id="06d06-240">使用者定義彙總是指並非 U-SQL 現成提供的彙總相關函式。</span><span class="sxs-lookup"><span data-stu-id="06d06-240">User-defined aggregates are any aggregation-related functions that are not shipped out-of-the-box with U-SQL.</span></span> <span data-ttu-id="06d06-241">hello 範例可以是彙總的 tooperform 自訂數學計算，字串串連字串的操作，並以此類推。</span><span class="sxs-lookup"><span data-stu-id="06d06-241">hello example can be an aggregate tooperform custom math calculations, string concatenations, manipulations with strings, and so on.</span></span>

<span data-ttu-id="06d06-242">hello 使用者定義彙總的基底類別定義如下所示：</span><span class="sxs-lookup"><span data-stu-id="06d06-242">hello user-defined aggregate base class definition is as follows:</span></span>

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

<span data-ttu-id="06d06-243">**SqlUserDefinedAggregate**表示 hello 類型應該註冊為使用者定義彙總。</span><span class="sxs-lookup"><span data-stu-id="06d06-243">**SqlUserDefinedAggregate** indicates that hello type should be registered as a user-defined aggregate.</span></span> <span data-ttu-id="06d06-244">這個類別無法繼承。</span><span class="sxs-lookup"><span data-stu-id="06d06-244">This class cannot be inherited.</span></span>

<span data-ttu-id="06d06-245">SqlUserDefinedType 是 UDAGG 定義的**選擇性**屬性。</span><span class="sxs-lookup"><span data-stu-id="06d06-245">SqlUserDefinedType attribute is **optional** for UDAGG definition.</span></span>


<span data-ttu-id="06d06-246">hello 基底類別可讓您 toopass 三個抽象參數： 兩個輸入的參數及另一個目錄當做 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="06d06-246">hello base class allows you toopass three abstract parameters: two as input parameters and one as hello result.</span></span> <span data-ttu-id="06d06-247">hello 資料型別變動而應定義類別繼承時。</span><span class="sxs-lookup"><span data-stu-id="06d06-247">hello data types are variable and should be defined during class inheritance.</span></span>

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

* <span data-ttu-id="06d06-248">**Init** 會在計算期間，為每個群組叫用一次。</span><span class="sxs-lookup"><span data-stu-id="06d06-248">**Init** invokes once for each group during computation.</span></span> <span data-ttu-id="06d06-249">Init 可為每個彙總群組提供初始化常式。</span><span class="sxs-lookup"><span data-stu-id="06d06-249">It provides an initialization routine for each aggregation group.</span></span>  
* <span data-ttu-id="06d06-250">**Accumulate** 會為每個值執行一次。</span><span class="sxs-lookup"><span data-stu-id="06d06-250">**Accumulate** is executed once for each value.</span></span> <span data-ttu-id="06d06-251">它提供 hello 彙總演算法 hello 主要功能。</span><span class="sxs-lookup"><span data-stu-id="06d06-251">It provides hello main functionality for hello aggregation algorithm.</span></span> <span data-ttu-id="06d06-252">它可以是使用的 tooaggregate 類別繼承期間定義的各種資料類型的值。</span><span class="sxs-lookup"><span data-stu-id="06d06-252">It can be used tooaggregate values with various data types that are defined during class inheritance.</span></span> <span data-ttu-id="06d06-253">它可接受兩個變數資料類型的參數。</span><span class="sxs-lookup"><span data-stu-id="06d06-253">It can accept two parameters of variable data types.</span></span>
* <span data-ttu-id="06d06-254">**終止**每個彙總群組結尾 hello 處理 toooutput hello 結果的每個群組執行一次。</span><span class="sxs-lookup"><span data-stu-id="06d06-254">**Terminate** is executed once per aggregation group at hello end of processing toooutput hello result for each group.</span></span>

<span data-ttu-id="06d06-255">toodeclare 正確的輸入和輸出資料類型，使用 hello 類別定義，如下所示：</span><span class="sxs-lookup"><span data-stu-id="06d06-255">toodeclare correct input and output data types, use hello class definition as follows:</span></span>

```
public abstract class IAggregate<T1, T2, TResult> : IAggregate
```

* <span data-ttu-id="06d06-256">第一個參數 tooaccumulate T1:</span><span class="sxs-lookup"><span data-stu-id="06d06-256">T1: First parameter tooaccumulate</span></span>
* <span data-ttu-id="06d06-257">第一個參數 tooaccumulate T2:</span><span class="sxs-lookup"><span data-stu-id="06d06-257">T2: First parameter tooaccumulate</span></span>
* <span data-ttu-id="06d06-258">TResult：傳回終止的類型</span><span class="sxs-lookup"><span data-stu-id="06d06-258">TResult: Return type of terminate</span></span>

<span data-ttu-id="06d06-259">例如：</span><span class="sxs-lookup"><span data-stu-id="06d06-259">For example:</span></span>

```
public class GuidAggregate : IAggregate<string, int, int>
```

<span data-ttu-id="06d06-260">或</span><span class="sxs-lookup"><span data-stu-id="06d06-260">or</span></span>

```
public class GuidAggregate : IAggregate<string, string, string>
```

### <a name="use-udagg-in-u-sql"></a><span data-ttu-id="06d06-261">在 U-SQL 中使用 UDAGG</span><span class="sxs-lookup"><span data-stu-id="06d06-261">Use UDAGG in U-SQL</span></span>
<span data-ttu-id="06d06-262">toouse UDAGG，先在程式碼後置中定義它，或從 hello 存在可程式性 DLL 參考先前所述。</span><span class="sxs-lookup"><span data-stu-id="06d06-262">toouse UDAGG, first define it in code-behind or reference it from hello existent programmability DLL as discussed earlier.</span></span>

<span data-ttu-id="06d06-263">接著，使用下列語法的 hello:</span><span class="sxs-lookup"><span data-stu-id="06d06-263">Then use hello following syntax:</span></span>

```
AGG<UDAGG_functionname>(param1,param2)
```

<span data-ttu-id="06d06-264">UDAGG 範例如下：</span><span class="sxs-lookup"><span data-stu-id="06d06-264">Here is an example of UDAGG:</span></span>

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

<span data-ttu-id="06d06-265">以及基底 U-SQL 指令碼：</span><span class="sxs-lookup"><span data-stu-id="06d06-265">And base U-SQL script:</span></span>

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

<span data-ttu-id="06d06-266">在此使用案例案例中，我們會串連 hello 特定使用者的類別 Guid。</span><span class="sxs-lookup"><span data-stu-id="06d06-266">In this use-case scenario, we concatenate class GUIDs for hello specific users.</span></span>

## <a name="use-user-defined-objects-udo"></a><span data-ttu-id="06d06-267">使用使用者定義物件：UDO</span><span class="sxs-lookup"><span data-stu-id="06d06-267">Use user-defined objects: UDO</span></span>
<span data-ttu-id="06d06-268">U SQL 可讓您會在呼叫使用者定義物件或 UDO toodefine 自訂的可程式性物件。</span><span class="sxs-lookup"><span data-stu-id="06d06-268">U-SQL enables you toodefine custom programmability objects, which are called user-defined objects or UDO.</span></span>

<span data-ttu-id="06d06-269">hello 以下是中 U-SQL UDO 的清單：</span><span class="sxs-lookup"><span data-stu-id="06d06-269">hello following is a list of UDO in U-SQL:</span></span>

* <span data-ttu-id="06d06-270">使用者定義擷取器</span><span class="sxs-lookup"><span data-stu-id="06d06-270">User-defined extractors</span></span>
    * <span data-ttu-id="06d06-271">逐列擷取</span><span class="sxs-lookup"><span data-stu-id="06d06-271">Extract row by row</span></span>
    * <span data-ttu-id="06d06-272">使用自訂的結構化檔案從 tooimplement 資料擷取</span><span class="sxs-lookup"><span data-stu-id="06d06-272">Used tooimplement data extraction from custom structured files</span></span>

* <span data-ttu-id="06d06-273">使用者定義輸出器</span><span class="sxs-lookup"><span data-stu-id="06d06-273">User-defined outputters</span></span>
    * <span data-ttu-id="06d06-274">逐列輸出</span><span class="sxs-lookup"><span data-stu-id="06d06-274">Output row by row</span></span>
    * <span data-ttu-id="06d06-275">使用 toooutput 自訂資料類型或自訂的檔案格式</span><span class="sxs-lookup"><span data-stu-id="06d06-275">Used toooutput custom data types or custom file formats</span></span>

* <span data-ttu-id="06d06-276">使用者定義處理器</span><span class="sxs-lookup"><span data-stu-id="06d06-276">User-defined processors</span></span>
    * <span data-ttu-id="06d06-277">擷取一列並產生一列</span><span class="sxs-lookup"><span data-stu-id="06d06-277">Take one row and produce one row</span></span>
    * <span data-ttu-id="06d06-278">使用的 tooreduce hello 的資料行數目，或產生新的資料行衍生自現有的資料行集的值</span><span class="sxs-lookup"><span data-stu-id="06d06-278">Used tooreduce hello number of columns or produce new columns with values that are derived from an existing column set</span></span>

* <span data-ttu-id="06d06-279">使用者定義套用器</span><span class="sxs-lookup"><span data-stu-id="06d06-279">User-defined appliers</span></span>
    * <span data-ttu-id="06d06-280">需要一個資料列，並產生 0 toon 個資料列</span><span class="sxs-lookup"><span data-stu-id="06d06-280">Take one row and produce 0 toon rows</span></span>
    * <span data-ttu-id="06d06-281">與 OUTER/CROSS APPLY 搭配使用</span><span class="sxs-lookup"><span data-stu-id="06d06-281">Used with OUTER/CROSS APPLY</span></span>

* <span data-ttu-id="06d06-282">使用者定義結合器</span><span class="sxs-lookup"><span data-stu-id="06d06-282">User-defined combiners</span></span>
    * <span data-ttu-id="06d06-283">結合資料列集--使用者定義 JOIN</span><span class="sxs-lookup"><span data-stu-id="06d06-283">Combines rowsets--user-defined JOINs</span></span>

* <span data-ttu-id="06d06-284">使用者定義歸納器</span><span class="sxs-lookup"><span data-stu-id="06d06-284">User-defined reducers</span></span>
    * <span data-ttu-id="06d06-285">擷取 n 列並產生一列</span><span class="sxs-lookup"><span data-stu-id="06d06-285">Take n rows and produce one row</span></span>
    * <span data-ttu-id="06d06-286">使用資料列的 tooreduce hello 數目</span><span class="sxs-lookup"><span data-stu-id="06d06-286">Used tooreduce hello number of rows</span></span>

<span data-ttu-id="06d06-287">UDO 通常會遵循 U SQL 陳述式的 hello 一部分 U-SQL 指令碼中明確呼叫：</span><span class="sxs-lookup"><span data-stu-id="06d06-287">UDO is typically called explicitly in U-SQL script as part of hello following U-SQL statements:</span></span>

* <span data-ttu-id="06d06-288">EXTRACT</span><span class="sxs-lookup"><span data-stu-id="06d06-288">EXTRACT</span></span>
* <span data-ttu-id="06d06-289">OUTPUT</span><span class="sxs-lookup"><span data-stu-id="06d06-289">OUTPUT</span></span>
* <span data-ttu-id="06d06-290">PROCESS</span><span class="sxs-lookup"><span data-stu-id="06d06-290">PROCESS</span></span>
* <span data-ttu-id="06d06-291">COMBINE</span><span class="sxs-lookup"><span data-stu-id="06d06-291">COMBINE</span></span>
* <span data-ttu-id="06d06-292">REDUCE</span><span class="sxs-lookup"><span data-stu-id="06d06-292">REDUCE</span></span>

> [!NOTE]  
> <span data-ttu-id="06d06-293">UDO 的是有限的 tooconsume 0.5 Gb 記憶體。</span><span class="sxs-lookup"><span data-stu-id="06d06-293">UDO’s are limited tooconsume 0.5Gb memory.</span></span>  <span data-ttu-id="06d06-294">此記憶體限制不適用 toolocal 執行。</span><span class="sxs-lookup"><span data-stu-id="06d06-294">This memory limitation does not apply toolocal executions.</span></span>

## <a name="use-user-defined-extractors"></a><span data-ttu-id="06d06-295">使用使用者定義擷取器</span><span class="sxs-lookup"><span data-stu-id="06d06-295">Use user-defined extractors</span></span>
<span data-ttu-id="06d06-296">U SQL 可讓您 tooimport 外部資料使用的擷取陳述式。</span><span class="sxs-lookup"><span data-stu-id="06d06-296">U-SQL allows you tooimport external data by using an EXTRACT statement.</span></span> <span data-ttu-id="06d06-297">EXTRACT 陳述式可以使用內建的 UDO 擷取器：</span><span class="sxs-lookup"><span data-stu-id="06d06-297">An EXTRACT statement can use built-in UDO extractors:</span></span>  

* <span data-ttu-id="06d06-298">Extractors.Text()︰可從不同編碼的分隔文字檔進行擷取。</span><span class="sxs-lookup"><span data-stu-id="06d06-298">*Extractors.Text()*: Provides extraction from delimited text files of different encodings.</span></span>

* <span data-ttu-id="06d06-299">Extractors.Csv()︰可從不同編碼的逗號分隔值 (CSV) 檔案進行擷取。</span><span class="sxs-lookup"><span data-stu-id="06d06-299">*Extractors.Csv()*: Provides extraction from comma-separated value (CSV) files of different encodings.</span></span>

* <span data-ttu-id="06d06-300">Extractors.Tsv()︰可從不同編碼的定位鍵分隔值 (TSV) 檔案進行擷取。</span><span class="sxs-lookup"><span data-stu-id="06d06-300">*Extractors.Tsv()*: Provides extraction from tab-separated value (TSV) files of different encodings.</span></span>

<span data-ttu-id="06d06-301">它可以是很有用 toodevelop 自訂擷取程式 」。</span><span class="sxs-lookup"><span data-stu-id="06d06-301">It can be useful toodevelop a custom extractor.</span></span> <span data-ttu-id="06d06-302">這可能是很有幫助資料匯入期間如果我們想要 toodo 任何 hello 下列工作：</span><span class="sxs-lookup"><span data-stu-id="06d06-302">This can be helpful during data import if we want toodo any of hello following tasks:</span></span>

* <span data-ttu-id="06d06-303">分割資料行並修改個別值，以修改輸入資料。</span><span class="sxs-lookup"><span data-stu-id="06d06-303">Modify input data by splitting columns and modifying individual values.</span></span> <span data-ttu-id="06d06-304">hello 處理器功能是為了合併資料行。</span><span class="sxs-lookup"><span data-stu-id="06d06-304">hello PROCESSOR functionality is better for combining columns.</span></span>
* <span data-ttu-id="06d06-305">剖析非結構化資料 (例如網頁/電子郵件) 或半非結構化資料 (例如 XML/JSON)。</span><span class="sxs-lookup"><span data-stu-id="06d06-305">Parse unstructured data such as Web pages and emails, or semi-unstructured data such as XML/JSON.</span></span>
* <span data-ttu-id="06d06-306">剖析編碼不受支援的資料。</span><span class="sxs-lookup"><span data-stu-id="06d06-306">Parse data in unsupported encoding.</span></span>

<span data-ttu-id="06d06-307">toodefine 使用者定義的擷取程式，或者 UDE，我們需要 toocreate`IExtractor`介面。</span><span class="sxs-lookup"><span data-stu-id="06d06-307">toodefine a user-defined extractor, or UDE, we need toocreate an `IExtractor` interface.</span></span> <span data-ttu-id="06d06-308">所有的輸入參數 toohello 抽選程式，例如資料行/資料列分隔符號和編碼，則需要 toobe hello 類別 hello 建構函式中定義。</span><span class="sxs-lookup"><span data-stu-id="06d06-308">All input parameters toohello extractor, such as column/row delimiters, and encoding, need toobe defined in hello constructor of hello class.</span></span> <span data-ttu-id="06d06-309">hello`IExtractor`介面也應包含 hello 的定義`IEnumerable<IRow>`覆寫，如下所示：</span><span class="sxs-lookup"><span data-stu-id="06d06-309">hello `IExtractor`  interface should also contain a definition for hello `IEnumerable<IRow>` override as follows:</span></span>

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

<span data-ttu-id="06d06-310">hello **SqlUserDefinedExtractor**屬性會指出 hello 類型應該要註冊為使用者定義的擷取程式。</span><span class="sxs-lookup"><span data-stu-id="06d06-310">hello **SqlUserDefinedExtractor** attribute indicates that hello type should be registered as a user-defined extractor.</span></span> <span data-ttu-id="06d06-311">這個類別無法繼承。</span><span class="sxs-lookup"><span data-stu-id="06d06-311">This class cannot be inherited.</span></span>

<span data-ttu-id="06d06-312">SqlUserDefinedExtractor 是 UDE 定義的選擇性屬性。</span><span class="sxs-lookup"><span data-stu-id="06d06-312">SqlUserDefinedExtractor is an optional attribute for UDE definition.</span></span> <span data-ttu-id="06d06-313">它會將 toodefine AtomicFileProcessing 屬性用於 hello UDE 物件。</span><span class="sxs-lookup"><span data-stu-id="06d06-313">It used toodefine AtomicFileProcessing property for hello UDE object.</span></span>

* <span data-ttu-id="06d06-314">bool     AtomicFileProcessing</span><span class="sxs-lookup"><span data-stu-id="06d06-314">bool     AtomicFileProcessing</span></span>   

* <span data-ttu-id="06d06-315">**true** = 表示此擷取器需要不可部分完成的輸入檔 (JSON、XML ...)</span><span class="sxs-lookup"><span data-stu-id="06d06-315">**true** = Indicates that this extractor requires atomic input files (JSON, XML, ...)</span></span>
* <span data-ttu-id="06d06-316">**false** = 表示此擷取器可以處理分割/分散式檔案 (CSV、SEQ ...)</span><span class="sxs-lookup"><span data-stu-id="06d06-316">**false** = Indicates that this extractor can deal with split / distributed files (CSV, SEQ, ...)</span></span>

<span data-ttu-id="06d06-317">hello 主要 UDE 可程式性物件**輸入**和**輸出**。</span><span class="sxs-lookup"><span data-stu-id="06d06-317">hello main UDE programmability objects are **input** and **output**.</span></span> <span data-ttu-id="06d06-318">hello 輸入的物件是使用的 tooenumerate 輸入的資料為`IUnstructuredReader`。</span><span class="sxs-lookup"><span data-stu-id="06d06-318">hello input object is used tooenumerate input data as `IUnstructuredReader`.</span></span> <span data-ttu-id="06d06-319">hello 輸出物件是使用的 tooset hello 擷取程式 」 活動的輸出資料。</span><span class="sxs-lookup"><span data-stu-id="06d06-319">hello output object is used tooset output data as a result of hello extractor activity.</span></span>

<span data-ttu-id="06d06-320">hello 輸入的資料透過存取`System.IO.Stream`和`System.IO.StreamReader`。</span><span class="sxs-lookup"><span data-stu-id="06d06-320">hello input data is accessed through `System.IO.Stream` and `System.IO.StreamReader`.</span></span>

<span data-ttu-id="06d06-321">針對輸入資料行列舉型別，我們先分割 hello 輸入資料流使用資料列分隔符號。</span><span class="sxs-lookup"><span data-stu-id="06d06-321">For input columns enumeration, we first split hello input stream by using a row delimiter.</span></span>

```
foreach (Stream current in input.Split(my_row_delimiter))
{
…
}
```

<span data-ttu-id="06d06-322">然後，將輸入資料列進一步分割為資料行組件。</span><span class="sxs-lookup"><span data-stu-id="06d06-322">Then, further split input row into column parts.</span></span>

```
foreach (Stream current in input.Split(my_row_delimiter))
{
…
    string[] parts = line.Split(my_column_delimiter);
    foreach (string part in parts)
    { … }
}
```

<span data-ttu-id="06d06-323">tooset 輸出的資料，我們使用 hello`output.Set`方法。</span><span class="sxs-lookup"><span data-stu-id="06d06-323">tooset output data, we use hello `output.Set` method.</span></span>

<span data-ttu-id="06d06-324">請務必 hello 自訂擷取程式 」 的 toounderstand 只輸出資料行和值定義與 hello 輸出。</span><span class="sxs-lookup"><span data-stu-id="06d06-324">It's important toounderstand that hello custom extractor only outputs columns and values that are defined with hello output.</span></span> <span data-ttu-id="06d06-325">設定方法呼叫。</span><span class="sxs-lookup"><span data-stu-id="06d06-325">Set method call.</span></span>

```
output.Set<string>(count, part);
```

<span data-ttu-id="06d06-326">hello 實際擷取程式 」 輸出由呼叫觸發`yield return output.AsReadOnly();`。</span><span class="sxs-lookup"><span data-stu-id="06d06-326">hello actual extractor output is triggered by calling `yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="06d06-327">以下是 hello 擷取程式 」 範例：</span><span class="sxs-lookup"><span data-stu-id="06d06-327">Following is hello extractor example:</span></span>

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

<span data-ttu-id="06d06-328">在此使用案例案例中，hello 抽選程式重新 hello GUID"guid"資料行，並將 「 使用者 」 資料行 tooupper 案例的 hello 值轉換。</span><span class="sxs-lookup"><span data-stu-id="06d06-328">In this use-case scenario, hello extractor regenerates hello GUID for “guid” column and converts hello values of “user” column tooupper case.</span></span> <span data-ttu-id="06d06-329">自訂擷取器可藉由剖析輸入資料並用它進行操作，來產生更複雜的結果。</span><span class="sxs-lookup"><span data-stu-id="06d06-329">Custom extractors can produce more complicated results by parsing input data and manipulating it.</span></span>

<span data-ttu-id="06d06-330">以下為使用自訂擷取器的基底 U-SQL 指令碼：</span><span class="sxs-lookup"><span data-stu-id="06d06-330">Following is base U-SQL script that uses a custom extractor:</span></span>

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

## <a name="use-user-defined-outputters"></a><span data-ttu-id="06d06-331">使用使用者定義輸出器</span><span class="sxs-lookup"><span data-stu-id="06d06-331">Use user-defined outputters</span></span>
<span data-ttu-id="06d06-332">使用者定義 outputter 是另一個 U-SQL UDO，可讓您 tooextend 內建 U-SQL 功能。</span><span class="sxs-lookup"><span data-stu-id="06d06-332">User-defined outputter is another U-SQL UDO that allows you tooextend built-in U-SQL functionality.</span></span> <span data-ttu-id="06d06-333">類似 toohello 抽選程式，有數個內建 outputters。</span><span class="sxs-lookup"><span data-stu-id="06d06-333">Similar toohello extractor, there are several built-in outputters.</span></span>

* <span data-ttu-id="06d06-334">*Outputters.Text()*： 寫入資料 toodelimited 不同編碼的文字檔案。</span><span class="sxs-lookup"><span data-stu-id="06d06-334">*Outputters.Text()*: Writes data toodelimited text files of different encodings.</span></span>
* <span data-ttu-id="06d06-335">*Outputters.Csv()*： 會寫入資料 toocomma 分隔值 (CSV) 檔案的不同的編碼方式。</span><span class="sxs-lookup"><span data-stu-id="06d06-335">*Outputters.Csv()*: Writes data toocomma-separated value (CSV) files of different encodings.</span></span>
* <span data-ttu-id="06d06-336">*Outputters.Tsv()*： 會寫入資料 tootab 分隔值 (TSV) 檔案的不同的編碼方式。</span><span class="sxs-lookup"><span data-stu-id="06d06-336">*Outputters.Tsv()*: Writes data tootab-separated value (TSV) files of different encodings.</span></span>

<span data-ttu-id="06d06-337">自訂 outputter 可讓您 toowrite 資料中定義的自訂格式。</span><span class="sxs-lookup"><span data-stu-id="06d06-337">Custom outputter allows you toowrite data in a custom defined format.</span></span> <span data-ttu-id="06d06-338">這可用於 hello 下列工作：</span><span class="sxs-lookup"><span data-stu-id="06d06-338">This can be useful for hello following tasks:</span></span>

* <span data-ttu-id="06d06-339">撰寫資料 toosemi 結構化或非結構化檔案。</span><span class="sxs-lookup"><span data-stu-id="06d06-339">Writing data toosemi-structured or unstructured files.</span></span>
* <span data-ttu-id="06d06-340">寫入編碼不受支援的資料。</span><span class="sxs-lookup"><span data-stu-id="06d06-340">Writing data not supported encodings.</span></span>
* <span data-ttu-id="06d06-341">修改輸出資料或新增自訂屬性。</span><span class="sxs-lookup"><span data-stu-id="06d06-341">Modifying output data or adding custom attributes.</span></span>

<span data-ttu-id="06d06-342">我們需要 toocreate hello toodefine 使用者定義 outputter`IOutputter`介面。</span><span class="sxs-lookup"><span data-stu-id="06d06-342">toodefine user-defined outputter, we need toocreate hello `IOutputter` interface.</span></span>

<span data-ttu-id="06d06-343">以下是基底 hello`IOutputter`類別實作：</span><span class="sxs-lookup"><span data-stu-id="06d06-343">Following is hello base `IOutputter` class implementation:</span></span>

```
public abstract class IOutputter : IUserDefinedOperator
{
    protected IOutputter();

    public virtual void Close();
    public abstract void Output(IRow input, IUnstructuredWriter output);
}
```

<span data-ttu-id="06d06-344">所有的輸入參數 toohello outputter，例如資料行/資料列分隔符號、 編碼和等等，需要 toobe hello 類別 hello 建構函式中定義。</span><span class="sxs-lookup"><span data-stu-id="06d06-344">All input parameters toohello outputter, such as column/row delimiters, encoding, and so on, need toobe defined in hello constructor of hello class.</span></span> <span data-ttu-id="06d06-345">hello`IOutputter`介面也應包含的定義`void Output`覆寫。</span><span class="sxs-lookup"><span data-stu-id="06d06-345">hello `IOutputter` interface should also contain a definition for `void Output` override.</span></span> <span data-ttu-id="06d06-346">hello 屬性`[SqlUserDefinedOutputter(AtomicFileProcessing = true)`可以選擇性地設定為不可部分完成檔案處理。</span><span class="sxs-lookup"><span data-stu-id="06d06-346">hello attribute `[SqlUserDefinedOutputter(AtomicFileProcessing = true)` can optionally be set for atomic file processing.</span></span> <span data-ttu-id="06d06-347">如需詳細資訊，請參閱 hello 下列詳細資料。</span><span class="sxs-lookup"><span data-stu-id="06d06-347">For more information, see hello following details.</span></span>

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

* <span data-ttu-id="06d06-348">會針對每個輸入資料列呼叫 `Output`。</span><span class="sxs-lookup"><span data-stu-id="06d06-348">`Output` is called for each input row.</span></span> <span data-ttu-id="06d06-349">它會傳回 hello`IUnstructuredWriter output`資料列集。</span><span class="sxs-lookup"><span data-stu-id="06d06-349">It returns hello `IUnstructuredWriter output` rowset.</span></span>
* <span data-ttu-id="06d06-350">hello 建構函式類別用 toopass 參數 toohello 使用者定義 outputter。</span><span class="sxs-lookup"><span data-stu-id="06d06-350">hello Constructor class is used toopass parameters toohello user-defined outputter.</span></span>
* <span data-ttu-id="06d06-351">`Close`使用 toooptionally 覆寫 toorelease 高度耗費資源的狀態，或判斷 hello 最後一個資料列寫入的時。</span><span class="sxs-lookup"><span data-stu-id="06d06-351">`Close` is used toooptionally override toorelease expensive state or determine when hello last row was written.</span></span>

<span data-ttu-id="06d06-352">**SqlUserDefinedOutputter**屬性會指出 hello 類型應該要註冊為使用者定義的 outputter。</span><span class="sxs-lookup"><span data-stu-id="06d06-352">**SqlUserDefinedOutputter** attribute indicates that hello type should be registered as a user-defined outputter.</span></span> <span data-ttu-id="06d06-353">這個類別無法繼承。</span><span class="sxs-lookup"><span data-stu-id="06d06-353">This class cannot be inherited.</span></span>

<span data-ttu-id="06d06-354">SqlUserDefinedOutputter 是使用者定義輸出器之定義的選擇性屬性。</span><span class="sxs-lookup"><span data-stu-id="06d06-354">SqlUserDefinedOutputter is an optional attribute for a user-defined outputter definition.</span></span> <span data-ttu-id="06d06-355">它已用 toodefine hello AtomicFileProcessing 屬性。</span><span class="sxs-lookup"><span data-stu-id="06d06-355">It's used toodefine hello AtomicFileProcessing property.</span></span>

* <span data-ttu-id="06d06-356">bool     AtomicFileProcessing</span><span class="sxs-lookup"><span data-stu-id="06d06-356">bool     AtomicFileProcessing</span></span>   

* <span data-ttu-id="06d06-357">**true** = 表示此輸出器需要不可部分完成的輸出檔 (JSON、XML ...)</span><span class="sxs-lookup"><span data-stu-id="06d06-357">**true** = Indicates that this outputter requires atomic output files (JSON, XML, ...)</span></span>
* <span data-ttu-id="06d06-358">**false** = 表示此輸出器可以處理分割/分散式檔案 (CSV、SEQ ...)</span><span class="sxs-lookup"><span data-stu-id="06d06-358">**false** = Indicates that this outputter can deal with split / distributed files (CSV, SEQ, ...)</span></span>

<span data-ttu-id="06d06-359">hello 主要的可程式性物件**列**和**輸出**。</span><span class="sxs-lookup"><span data-stu-id="06d06-359">hello main programmability objects are **row** and **output**.</span></span> <span data-ttu-id="06d06-360">hello**列**物件是使用的 tooenumerate 輸出資料做為`IRow`介面。</span><span class="sxs-lookup"><span data-stu-id="06d06-360">hello **row** object is used tooenumerate output data as `IRow` interface.</span></span> <span data-ttu-id="06d06-361">**輸出**使用的 tooset 輸出資料 toohello 目標檔案。</span><span class="sxs-lookup"><span data-stu-id="06d06-361">**Output** is used tooset output data toohello target file.</span></span>

<span data-ttu-id="06d06-362">hello 輸出資料透過存取 hello`IRow`介面。</span><span class="sxs-lookup"><span data-stu-id="06d06-362">hello output data is accessed through hello `IRow` interface.</span></span> <span data-ttu-id="06d06-363">一次會對輸出資料傳遞一個資料列。</span><span class="sxs-lookup"><span data-stu-id="06d06-363">Output data is passed a row at a time.</span></span>

<span data-ttu-id="06d06-364">藉由呼叫 hello IRow 介面 hello Get 方法列舉 hello 個別的值：</span><span class="sxs-lookup"><span data-stu-id="06d06-364">hello individual values are enumerated by calling hello Get method of hello IRow interface:</span></span>

```
row.Get<string>("column_name")
```

<span data-ttu-id="06d06-365">呼叫 `row.Schema` 即可判斷個別資料行名稱：</span><span class="sxs-lookup"><span data-stu-id="06d06-365">Individual column names can be determined by calling `row.Schema`:</span></span>

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

<span data-ttu-id="06d06-366">這種方法可讓您針對任何中繼資料結構描述的彈性 outputter toobuild。</span><span class="sxs-lookup"><span data-stu-id="06d06-366">This approach enables you toobuild a flexible outputter for any metadata schema.</span></span>

<span data-ttu-id="06d06-367">hello 輸出資料寫入 toofile 使用`System.IO.StreamWriter`。</span><span class="sxs-lookup"><span data-stu-id="06d06-367">hello output data is written toofile by using `System.IO.StreamWriter`.</span></span> <span data-ttu-id="06d06-368">hello 資料流參數設定得`output.BaseStrea`一部分`IUnstructuredWriter output`。</span><span class="sxs-lookup"><span data-stu-id="06d06-368">hello stream parameter is set too`output.BaseStrea` as part of `IUnstructuredWriter output`.</span></span>

<span data-ttu-id="06d06-369">請注意，它會是重要 tooflush hello 資料緩衝區 toohello 檔在每個資料列反覆項目。</span><span class="sxs-lookup"><span data-stu-id="06d06-369">Note that it's important tooflush hello data buffer toohello file after each row iteration.</span></span> <span data-ttu-id="06d06-370">此外，hello`StreamWriter`物件必須用在 hello 可處置的啟用屬性 （預設值） 與 hello**使用**關鍵字：</span><span class="sxs-lookup"><span data-stu-id="06d06-370">In addition, hello `StreamWriter` object must be used with hello Disposable attribute enabled (default) and with hello **using** keyword:</span></span>

```
using (StreamWriter streamWriter = new StreamWriter(output.BaseStream, this._encoding))
{
…
}
```

<span data-ttu-id="06d06-371">否則，在每個反覆項目之後明確地呼叫 Flush() 方法。</span><span class="sxs-lookup"><span data-stu-id="06d06-371">Otherwise, call Flush() method explicitly after each iteration.</span></span> <span data-ttu-id="06d06-372">我們會顯示這在下列範例中的 hello。</span><span class="sxs-lookup"><span data-stu-id="06d06-372">We show this in hello following example.</span></span>

### <a name="set-headers-and-footers-for-user-defined-outputter"></a><span data-ttu-id="06d06-373">設定使用者定義輸出器的頁首和頁尾</span><span class="sxs-lookup"><span data-stu-id="06d06-373">Set headers and footers for user-defined outputter</span></span>
<span data-ttu-id="06d06-374">tooset 標頭，使用單一的反覆項目執行流程。</span><span class="sxs-lookup"><span data-stu-id="06d06-374">tooset a header, use single iteration execution flow.</span></span>

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

<span data-ttu-id="06d06-375">第一次 hello hello 中的程式碼`if (isHeaderRow)`區塊執行一次。</span><span class="sxs-lookup"><span data-stu-id="06d06-375">hello code in hello first `if (isHeaderRow)` block is executed only once.</span></span>

<span data-ttu-id="06d06-376">Hello 頁尾使用 hello 參考 toohello 執行個體`System.IO.Stream`物件 (`output.BaseStream`)。</span><span class="sxs-lookup"><span data-stu-id="06d06-376">For hello footer, use hello reference toohello instance of `System.IO.Stream` object (`output.BaseStream`).</span></span> <span data-ttu-id="06d06-377">在 hello hello 的 close （） 方法中撰寫 hello 頁尾`IOutputter`介面。</span><span class="sxs-lookup"><span data-stu-id="06d06-377">Write hello footer in hello Close() method of hello `IOutputter` interface.</span></span>  <span data-ttu-id="06d06-378">（如需詳細資訊，請參閱下列範例中的 hello）。</span><span class="sxs-lookup"><span data-stu-id="06d06-378">(For more information, see hello following example.)</span></span>

<span data-ttu-id="06d06-379">以下是使用者定義 outputter 的範例︰</span><span class="sxs-lookup"><span data-stu-id="06d06-379">Following is an example of a user-defined outputter:</span></span>

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

<span data-ttu-id="06d06-380">以及 U-SQL 基底指令碼：</span><span class="sxs-lookup"><span data-stu-id="06d06-380">And U-SQL base script:</span></span>

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

<span data-ttu-id="06d06-381">這是 HTML 輸出器，會以資料表資料建立 HTML 檔案。</span><span class="sxs-lookup"><span data-stu-id="06d06-381">This is an HTML outputter, which creates an HTML file with table data.</span></span>

### <a name="call-outputter-from-u-sql-base-script"></a><span data-ttu-id="06d06-382">從 U-SQL 基底指令碼呼叫輸出器</span><span class="sxs-lookup"><span data-stu-id="06d06-382">Call outputter from U-SQL base script</span></span>
<span data-ttu-id="06d06-383">toocall 從 hello 基底 U-SQL 指令碼的自訂 outputter，hello hello outputter 物件的新執行個體具有建立 toobe。</span><span class="sxs-lookup"><span data-stu-id="06d06-383">toocall a custom outputter from hello base U-SQL script, hello new instance of hello outputter object has toobe created.</span></span>

```sql
OUTPUT @rs0 too@output_file USING new USQL_Programmability.HTMLOutputter(isHeader: true);
```

<span data-ttu-id="06d06-384">tooavoid 建立 hello 的執行個體物件存放至基底的指令碼，我們可以建立函式的包裝函式，在先前的範例所示：</span><span class="sxs-lookup"><span data-stu-id="06d06-384">tooavoid creating an instance of hello object in base script, we can create a function wrapper, as shown in our earlier example:</span></span>

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

<span data-ttu-id="06d06-385">在此情況下，hello 原始呼叫看起來像下列 hello:</span><span class="sxs-lookup"><span data-stu-id="06d06-385">In this case, hello original call looks like hello following:</span></span>

```
OUTPUT @rs0 
too@output_file 
USING USQL_Programmability.Factory.HTMLOutputter(isHeader: true);
```

## <a name="use-user-defined-processors"></a><span data-ttu-id="06d06-386">使用使用者定義處理器</span><span class="sxs-lookup"><span data-stu-id="06d06-386">Use user-defined processors</span></span>
<span data-ttu-id="06d06-387">使用者定義的處理器或 UDP 是一種可讓您藉由套用 可程式性功能的 tooprocess hello 內送資料列的 U-SQL UDO。</span><span class="sxs-lookup"><span data-stu-id="06d06-387">User-defined processor, or UDP, is a type of U-SQL UDO that enables you tooprocess hello incoming rows by applying programmability features.</span></span> <span data-ttu-id="06d06-388">UDP 可讓您 toocombine 資料行、 修改值，並視需要新增新的資料行。</span><span class="sxs-lookup"><span data-stu-id="06d06-388">UDP enables you toocombine columns, modify values, and add new columns if necessary.</span></span> <span data-ttu-id="06d06-389">基本上，它會協助 tooprocess 資料列集所需的 tooproduce 資料元素。</span><span class="sxs-lookup"><span data-stu-id="06d06-389">Basically, it helps tooprocess a rowset tooproduce required data elements.</span></span>

<span data-ttu-id="06d06-390">toodefine UDP，我們需要 toocreate`IProcessor`介面以 hello`SqlUserDefinedProcessor`屬性，這是選擇性的 UDP。</span><span class="sxs-lookup"><span data-stu-id="06d06-390">toodefine a UDP, we need toocreate an `IProcessor` interface with hello `SqlUserDefinedProcessor` attribute, which is optional for UDP.</span></span>

<span data-ttu-id="06d06-391">這個介面應該包含 hello hello 定義`IRow`介面資料列集覆寫，hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="06d06-391">This interface should contain hello definition for hello `IRow` interface rowset override, as shown in hello following example:</span></span>

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

<span data-ttu-id="06d06-392">**SqlUserDefinedProcessor**表示 hello 類型應該註冊為使用者定義的處理器。</span><span class="sxs-lookup"><span data-stu-id="06d06-392">**SqlUserDefinedProcessor** indicates that hello type should be registered as a user-defined processor.</span></span> <span data-ttu-id="06d06-393">這個類別無法繼承。</span><span class="sxs-lookup"><span data-stu-id="06d06-393">This class cannot be inherited.</span></span>

<span data-ttu-id="06d06-394">hello SqlUserDefinedProcessor 屬性是**選擇性**UDP 定義。</span><span class="sxs-lookup"><span data-stu-id="06d06-394">hello SqlUserDefinedProcessor attribute is **optional** for UDP definition.</span></span>

<span data-ttu-id="06d06-395">hello 主要的可程式性物件**輸入**和**輸出**。</span><span class="sxs-lookup"><span data-stu-id="06d06-395">hello main programmability objects are **input** and **output**.</span></span> <span data-ttu-id="06d06-396">hello 輸入的物件是使用的 tooenumerate 輸入資料行和輸出和 tooset hello 處理器活動的輸出資料。</span><span class="sxs-lookup"><span data-stu-id="06d06-396">hello input object is used tooenumerate input columns and output, and tooset output data as a result of hello processor activity.</span></span>

<span data-ttu-id="06d06-397">輸入資料行列舉型別，我們使用 hello`input.Get`方法。</span><span class="sxs-lookup"><span data-stu-id="06d06-397">For input columns enumeration, we use hello `input.Get` method.</span></span>

```
string column_name = input.Get<string>("column_name");
```

<span data-ttu-id="06d06-398">hello 參數`input.Get`方法是傳遞做為 hello 一部分的資料行`PRODUCE`子句 hello `PROCESS` hello U-SQL 基底的指令碼陳述式。</span><span class="sxs-lookup"><span data-stu-id="06d06-398">hello parameter for `input.Get` method is a column that's passed as part of hello `PRODUCE` clause of hello `PROCESS` statement of hello U-SQL base script.</span></span> <span data-ttu-id="06d06-399">我們需要 toouse hello 正確資料類型，這裡。</span><span class="sxs-lookup"><span data-stu-id="06d06-399">We need toouse hello correct data type here.</span></span>

<span data-ttu-id="06d06-400">輸出中，使用 hello`output.Set`方法。</span><span class="sxs-lookup"><span data-stu-id="06d06-400">For output, use hello `output.Set` method.</span></span>

<span data-ttu-id="06d06-401">請務必 toonote 該自訂生產者只會輸出資料行和值所定義的 hello`output.Set`方法呼叫。</span><span class="sxs-lookup"><span data-stu-id="06d06-401">It's important toonote that custom producer only outputs columns and values that are defined with hello `output.Set` method call.</span></span>

```
output.Set<string>("mycolumn", mycolumn);
```

<span data-ttu-id="06d06-402">藉由呼叫觸發 hello 實際處理器輸出`return output.AsReadOnly();`。</span><span class="sxs-lookup"><span data-stu-id="06d06-402">hello actual processor output is triggered by calling `return output.AsReadOnly();`.</span></span>

<span data-ttu-id="06d06-403">以下是處理器範例：</span><span class="sxs-lookup"><span data-stu-id="06d06-403">Following is a processor example:</span></span>

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

<span data-ttu-id="06d06-404">在此使用案例案例中，hello 處理器正在產生新的資料行稱為"full_description 」 結合 hello 現有資料行-在此情況下，「 使用者 」 中大寫，而"des"。</span><span class="sxs-lookup"><span data-stu-id="06d06-404">In this use-case scenario, hello processor is generating a new column called “full_description” by combining hello existing columns--in this case, “user” in upper case, and “des”.</span></span> <span data-ttu-id="06d06-405">它也會重新產生 GUID，並傳回 hello 原始值和新的 GUID 值。</span><span class="sxs-lookup"><span data-stu-id="06d06-405">It also regenerates a GUID and returns hello original and new GUID values.</span></span>

<span data-ttu-id="06d06-406">您可以看到 hello 前一個範例中，您可以呼叫 C# 方法期間`output.Set`方法呼叫。</span><span class="sxs-lookup"><span data-stu-id="06d06-406">As you can see from hello previous example, you can call C# methods during `output.Set` method call.</span></span>

<span data-ttu-id="06d06-407">以下是使用自訂處理器的基底 U-SQL 指令碼範例：</span><span class="sxs-lookup"><span data-stu-id="06d06-407">Following is an example of base U-SQL script that uses a custom processor:</span></span>

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

## <a name="use-user-defined-appliers"></a><span data-ttu-id="06d06-408">使用使用者定義套用器</span><span class="sxs-lookup"><span data-stu-id="06d06-408">Use user-defined appliers</span></span>
<span data-ttu-id="06d06-409">U SQL 使用者定義套用者可讓您查詢的 hello 外部資料表運算式所傳回的每個資料列的 tooinvoke 自訂 C# 函式。</span><span class="sxs-lookup"><span data-stu-id="06d06-409">A U-SQL user-defined applier enables you tooinvoke a custom C# function for each row that's returned by hello outer table expression of a query.</span></span> <span data-ttu-id="06d06-410">hello 右邊輸入會評估每個資料列從 hello 左邊的輸入，以及在 hello 最終輸出結合 hello 所產生的資料列。</span><span class="sxs-lookup"><span data-stu-id="06d06-410">hello right input is evaluated for each row from hello left input, and hello rows that are produced are combined for hello final output.</span></span> <span data-ttu-id="06d06-411">hello hello APPLY 運算子所產生的資料行清單是 hello hello left 和 hello 右輸入中的資料行集的 hello 組合。</span><span class="sxs-lookup"><span data-stu-id="06d06-411">hello list of columns that are produced by hello APPLY operator are hello combination of hello set of columns in hello left and hello right input.</span></span>

<span data-ttu-id="06d06-412">正在叫用使用者定義套用者 hello USQL 選取運算式的一部分。</span><span class="sxs-lookup"><span data-stu-id="06d06-412">User-defined applier is being invoked as part of hello USQL SELECT expression.</span></span>

<span data-ttu-id="06d06-413">典型的 hello 呼叫 toohello 使用者定義 applier 似乎 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="06d06-413">hello typical call toohello user-defined applier looks like hello following:</span></span>

```
SELECT …
FROM …
CROSS APPLYis used toopass parameters
new MyScript.MyApplier(param1, param2) AS alias(output_param1 string, …);
```

<span data-ttu-id="06d06-414">如需在 SELECT 運算式中使用套用器的詳細資訊，請參閱[從 CROSS APPLY 和 OUTER APPLY 選取的 U-SQL SELECT](https://msdn.microsoft.com/library/azure/mt621307.aspx)。</span><span class="sxs-lookup"><span data-stu-id="06d06-414">For more information about using appliers in a SELECT expression, see [U-SQL SELECT Selecting from CROSS APPLY and OUTER APPLY](https://msdn.microsoft.com/library/azure/mt621307.aspx).</span></span>

<span data-ttu-id="06d06-415">hello 使用者定義 applier 基底類別的定義如下所示：</span><span class="sxs-lookup"><span data-stu-id="06d06-415">hello user-defined applier base class definition is as follows:</span></span>

```
public abstract class IApplier : IUserDefinedOperator
{
protected IApplier();

public abstract IEnumerable<IRow> Apply(IRow input, IUpdatableRow output);
}
```

<span data-ttu-id="06d06-416">toodefine 使用者定義套用者，我們需要 toocreate hello`IApplier`介面以 hello [`SqlUserDefinedApplier`] 屬性，這是選擇性的使用者定義的 applier 定義。</span><span class="sxs-lookup"><span data-stu-id="06d06-416">toodefine a user-defined applier, we need toocreate hello `IApplier` interface with hello [`SqlUserDefinedApplier`] attribute, which is optional for a user-defined applier definition.</span></span>

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

* <span data-ttu-id="06d06-417">套用稱為 hello 外部資料表的每個資料列。</span><span class="sxs-lookup"><span data-stu-id="06d06-417">Apply is called for each row of hello outer table.</span></span> <span data-ttu-id="06d06-418">它會傳回 hello`IUpdatableRow`輸出資料列集。</span><span class="sxs-lookup"><span data-stu-id="06d06-418">It returns hello `IUpdatableRow` output rowset.</span></span>
* <span data-ttu-id="06d06-419">hello 建構函式類別是使用的 toopass 參數 toohello 使用者定義套用者。</span><span class="sxs-lookup"><span data-stu-id="06d06-419">hello Constructor class is used toopass parameters toohello user-defined applier.</span></span>

<span data-ttu-id="06d06-420">**SqlUserDefinedApplier**指出 hello 類型應該要註冊為使用者定義套用者。</span><span class="sxs-lookup"><span data-stu-id="06d06-420">**SqlUserDefinedApplier** indicates that hello type should be registered as a user-defined applier.</span></span> <span data-ttu-id="06d06-421">這個類別無法繼承。</span><span class="sxs-lookup"><span data-stu-id="06d06-421">This class cannot be inherited.</span></span>

<span data-ttu-id="06d06-422">**SqlUserDefinedApplier** 是使用者定義套用器定義的**選擇性**。</span><span class="sxs-lookup"><span data-stu-id="06d06-422">**SqlUserDefinedApplier** is **optional** for a user-defined applier definition.</span></span>


<span data-ttu-id="06d06-423">hello 主要的可程式性物件如下所示：</span><span class="sxs-lookup"><span data-stu-id="06d06-423">hello main programmability objects are as follows:</span></span>

```
public override IEnumerable<IRow> Apply(IRow input, IUpdatableRow output)
```

<span data-ttu-id="06d06-424">輸入資料列集會傳遞做為 `IRow` 輸入。</span><span class="sxs-lookup"><span data-stu-id="06d06-424">Input rowsets are passed as `IRow` input.</span></span> <span data-ttu-id="06d06-425">hello 輸出資料列會產生為`IUpdatableRow`輸出介面。</span><span class="sxs-lookup"><span data-stu-id="06d06-425">hello output rows are generated as `IUpdatableRow` output interface.</span></span>

<span data-ttu-id="06d06-426">個別資料行名稱由呼叫 hello`IRow`結構描述的方法。</span><span class="sxs-lookup"><span data-stu-id="06d06-426">Individual column names can be determined by calling hello `IRow` Schema method.</span></span>

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

<span data-ttu-id="06d06-427">tooget hello 實際資料值從傳入的 hello `IRow`，我們使用 get （） 方法 hello`IRow`介面。</span><span class="sxs-lookup"><span data-stu-id="06d06-427">tooget hello actual data values from hello incoming `IRow`, we use hello Get() method of `IRow` interface.</span></span>

```
mycolumn = row.Get<int>("mycolumn")
```

<span data-ttu-id="06d06-428">或者，我們使用 hello 結構描述資料行名稱：</span><span class="sxs-lookup"><span data-stu-id="06d06-428">Or we use hello schema column name:</span></span>

```
row.Get<int>(row.Schema[0].Name)
```

<span data-ttu-id="06d06-429">hello 輸出值必須設定`IUpdatableRow`輸出：</span><span class="sxs-lookup"><span data-stu-id="06d06-429">hello output values must be set with `IUpdatableRow` output:</span></span>

```
output.Set<int>("mycolumn", mycolumn)
```

<span data-ttu-id="06d06-430">它是自訂 appliers 只輸出資料行和值所定義的重要 toounderstand`output.Set`方法呼叫。</span><span class="sxs-lookup"><span data-stu-id="06d06-430">It is important toounderstand that custom appliers only output columns and values that are defined with `output.Set` method call.</span></span>

<span data-ttu-id="06d06-431">藉由呼叫觸發 hello 實際輸出`yield return output.AsReadOnly();`。</span><span class="sxs-lookup"><span data-stu-id="06d06-431">hello actual output is triggered by calling `yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="06d06-432">hello 使用者定義 applier 參數傳遞 toohello 建構函式。</span><span class="sxs-lookup"><span data-stu-id="06d06-432">hello user-defined applier parameters can be passed toohello constructor.</span></span> <span data-ttu-id="06d06-433">套用者可以傳回變動數目的需要 toobe 期間 hello applier 呼叫基底 U-SQL 指令碼中定義的資料行。</span><span class="sxs-lookup"><span data-stu-id="06d06-433">Applier can return a variable number of columns that need toobe defined during hello applier call in base U-SQL Script.</span></span>

```
new USQL_Programmability.ParserApplier ("all") AS properties(make string, model string, year string, type string, millage int);
```

<span data-ttu-id="06d06-434">以下是 hello 使用者定義 applier 範例：</span><span class="sxs-lookup"><span data-stu-id="06d06-434">Here is hello user-defined applier example:</span></span>

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

<span data-ttu-id="06d06-435">以下是 hello 基底 U-SQL 指令碼這個使用者定義套用者：</span><span class="sxs-lookup"><span data-stu-id="06d06-435">Following is hello base U-SQL script for this user-defined applier:</span></span>

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

<span data-ttu-id="06d06-436">在此使用的情況下，使用者定義 applier 作為 hello 汽車船隊屬性的逗號分隔值剖析器。</span><span class="sxs-lookup"><span data-stu-id="06d06-436">In this use case scenario, user-defined applier acts as a comma-delimited value parser for hello car fleet properties.</span></span> <span data-ttu-id="06d06-437">hello 輸入的檔資料列看起來像下列 hello:</span><span class="sxs-lookup"><span data-stu-id="06d06-437">hello input file rows look like hello following:</span></span>

```
103 Z1AB2CD123XY45889   Ford,Explorer,2005,SUV,152345
303 Y0AB2CD34XY458890   Shevrolet,Cruise,2010,4Dr,32455
210 X5AB2CD45XY458893   Nissan,Altima,2011,4Dr,74000
```

<span data-ttu-id="06d06-438">這是典型的定位點分隔符號 TSV 檔案，其屬性資料行內含製造商、型號等汽車屬性。</span><span class="sxs-lookup"><span data-stu-id="06d06-438">It is a typical tab-delimited TSV file with a properties column that contains car properties such as make and model.</span></span> <span data-ttu-id="06d06-439">這些屬性必須是剖析的 toohello 資料表資料行。</span><span class="sxs-lookup"><span data-stu-id="06d06-439">Those properties must be parsed toohello table columns.</span></span> <span data-ttu-id="06d06-440">hello 套用提供者也可讓您 toogenerate 動態許多屬性在 hello 產生資料列集，根據所傳入的 hello 參數。</span><span class="sxs-lookup"><span data-stu-id="06d06-440">hello applier that's provided also enables you toogenerate a dynamic number of properties in hello result rowset, based on hello parameter that's passed.</span></span> <span data-ttu-id="06d06-441">您可以產生所有屬性或僅一組特定的內容。</span><span class="sxs-lookup"><span data-stu-id="06d06-441">You can generate either all properties or a specific set of properties only.</span></span>

    …USQL_Programmability.ParserApplier ("all")
    …USQL_Programmability.ParserApplier ("make")
    …USQL_Programmability.ParserApplier ("make&model")

<span data-ttu-id="06d06-442">使用者定義套用者 hello 可稱作 applier 物件的新執行個體：</span><span class="sxs-lookup"><span data-stu-id="06d06-442">hello user-defined applier can be called as a new instance of applier object:</span></span>

```
CROSS APPLY new MyNameSpace.MyApplier (parameter: “value”) AS alias([columns types]…);
```

<span data-ttu-id="06d06-443">或使用的包裝函式的 factory 方法的引動過程 hello:</span><span class="sxs-lookup"><span data-stu-id="06d06-443">Or with hello invocation of a wrapper factory method:</span></span>

```c#
    CROSS APPLY MyNameSpace.MyApplier (parameter: “value”) AS alias([columns types]…);
```

## <a name="use-user-defined-combiners"></a><span data-ttu-id="06d06-444">使用使用者定義結合器</span><span class="sxs-lookup"><span data-stu-id="06d06-444">Use user-defined combiners</span></span>
<span data-ttu-id="06d06-445">使用者定義的結合子或 UDC，可讓您從左邊和右邊資料列集，根據自訂邏輯 toocombine 資料列。</span><span class="sxs-lookup"><span data-stu-id="06d06-445">User-defined combiner, or UDC, enables you toocombine rows from left and right rowsets, based on custom logic.</span></span> <span data-ttu-id="06d06-446">使用者定義結合器會與 COMBINE 運算式搭配使用。</span><span class="sxs-lookup"><span data-stu-id="06d06-446">User-defined combiner is used with COMBINE expression.</span></span>

<span data-ttu-id="06d06-447">正在叫用的結合子提供有關這兩個 hello 輸入資料列集的 hello 必要資訊的 hello 結合運算式、 群組資料行，hello hello 預期結果的結構描述，以及其他資訊。</span><span class="sxs-lookup"><span data-stu-id="06d06-447">A combiner is being invoked with hello COMBINE expression that provides hello necessary information about both hello input rowsets, hello grouping columns, hello expected result schema, and additional information.</span></span>

<span data-ttu-id="06d06-448">toocall 基底的 U-SQL 指令碼中的結合子，我們使用 hello，請使用下列語法：</span><span class="sxs-lookup"><span data-stu-id="06d06-448">toocall a combiner in a base U-SQL script, we use hello following syntax:</span></span>

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

<span data-ttu-id="06d06-449">如需詳細資訊，請參閱 [COMBINE 運算式 (U-SQL)](https://msdn.microsoft.com/library/azure/mt621339.aspx)。</span><span class="sxs-lookup"><span data-stu-id="06d06-449">For more information, see [COMBINE Expression (U-SQL)](https://msdn.microsoft.com/library/azure/mt621339.aspx).</span></span>

<span data-ttu-id="06d06-450">toodefine 使用者定義的結合子，我們需要 toocreate hello`ICombiner`介面以 hello [`SqlUserDefinedCombiner`] 屬性，這是選擇性的使用者定義的結合子定義。</span><span class="sxs-lookup"><span data-stu-id="06d06-450">toodefine a user-defined combiner, we need toocreate hello `ICombiner` interface with hello [`SqlUserDefinedCombiner`] attribute, which is optional for a user-defined Combiner definition.</span></span>

<span data-ttu-id="06d06-451">基底 `ICombiner` 類別定義：</span><span class="sxs-lookup"><span data-stu-id="06d06-451">Base `ICombiner` class definition:</span></span>

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

<span data-ttu-id="06d06-452">hello 的自訂實作`ICombiner`介面應該包含 hello 定義`IEnumerable<IRow>`結合覆寫。</span><span class="sxs-lookup"><span data-stu-id="06d06-452">hello custom implementation of an `ICombiner` interface should contain hello definition for an `IEnumerable<IRow>` Combine override.</span></span>

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

<span data-ttu-id="06d06-453">hello **SqlUserDefinedCombiner**屬性會指出 hello 類型應該要註冊為使用者定義的結合子。</span><span class="sxs-lookup"><span data-stu-id="06d06-453">hello **SqlUserDefinedCombiner** attribute indicates that hello type should be registered as a user-defined combiner.</span></span> <span data-ttu-id="06d06-454">這個類別無法繼承。</span><span class="sxs-lookup"><span data-stu-id="06d06-454">This class cannot be inherited.</span></span>

<span data-ttu-id="06d06-455">**SqlUserDefinedCombiner**是使用的 toodefine hello 的結合子模式屬性。</span><span class="sxs-lookup"><span data-stu-id="06d06-455">**SqlUserDefinedCombiner** is used toodefine hello Combiner mode property.</span></span> <span data-ttu-id="06d06-456">它是使用者定義結合器定義的選擇性屬性。</span><span class="sxs-lookup"><span data-stu-id="06d06-456">It is an optional attribute for a user-defined combiner definition.</span></span>

<span data-ttu-id="06d06-457">CombinerMode     Mode</span><span class="sxs-lookup"><span data-stu-id="06d06-457">CombinerMode     Mode</span></span>

<span data-ttu-id="06d06-458">CombinerMode 列舉可以採用下列值的 hello:</span><span class="sxs-lookup"><span data-stu-id="06d06-458">CombinerMode enum can take hello following values:</span></span>

* <span data-ttu-id="06d06-459">每個輸出資料列可能相依於 hello 輸入的所有資料列的全文 (0) 的左和右的 hello 相同機碼值。</span><span class="sxs-lookup"><span data-stu-id="06d06-459">Full  (0) Every output row potentially depends on all hello input rows from left and right       with hello same key value.</span></span>

* <span data-ttu-id="06d06-460">Left (1) 的單一輸入資料列從 hello 左取決於每個輸出資料列 (和所有可能列 hello hello 權限與從相同機碼值)。</span><span class="sxs-lookup"><span data-stu-id="06d06-460">Left  (1) Every output row depends on a single input row from hello left (and potentially all rows       from hello right with hello same key value).</span></span>

* <span data-ttu-id="06d06-461">每個輸出資料列而定右 hello 的單一輸入資料列的右邊 (2) (和所有可能列 hello 左 hello 與從相同機碼值)。</span><span class="sxs-lookup"><span data-stu-id="06d06-461">Right (2)     Every output row depends on a single input row from hello right (and potentially all rows       from hello left with hello same key value).</span></span>

* <span data-ttu-id="06d06-462">內部 (3) 的單一輸入取決於每個輸出資料列中的資料列左側和右側 hello 與相同值。</span><span class="sxs-lookup"><span data-stu-id="06d06-462">Inner (3) Every output row depends on a single input row from left and right with hello same value.</span></span>

<span data-ttu-id="06d06-463">範例：[`SqlUserDefinedCombiner(Mode=CombinerMode.Left)`]</span><span class="sxs-lookup"><span data-stu-id="06d06-463">Example:    [`SqlUserDefinedCombiner(Mode=CombinerMode.Left)`]</span></span>


<span data-ttu-id="06d06-464">hello 主要的可程式性物件如下：</span><span class="sxs-lookup"><span data-stu-id="06d06-464">hello main programmability objects are:</span></span>

```c#
    public override IEnumerable<IRow> Combine(IRowset left, IRowset right,
        IUpdatableRow output
```

<span data-ttu-id="06d06-465">輸入資料列集會傳遞做為介面的「左邊」和「右邊」 `IRowset` 類型。</span><span class="sxs-lookup"><span data-stu-id="06d06-465">Input rowsets are passed as **left** and **right** `IRowset` type of interface.</span></span> <span data-ttu-id="06d06-466">這兩個資料列集必須列舉以進行處理。</span><span class="sxs-lookup"><span data-stu-id="06d06-466">Both rowsets must be enumerated for processing.</span></span> <span data-ttu-id="06d06-467">您可以只列舉每個介面一次，因此我們有 tooenumerate，視快取。</span><span class="sxs-lookup"><span data-stu-id="06d06-467">You can only enumerate each interface once, so we have tooenumerate and cache it if necessary.</span></span>

<span data-ttu-id="06d06-468">若要快取，我們可以透過執行 LINQ 查詢來建立記憶體結構的 List\<T\> 類型，特別是 List<`IRow`>。</span><span class="sxs-lookup"><span data-stu-id="06d06-468">For caching purposes, we can create a List\<T\> type of memory structure as a result of a LINQ query execution, specifically List<`IRow`>.</span></span> <span data-ttu-id="06d06-469">hello 匿名資料型別可以用於期間以及列舉型別。</span><span class="sxs-lookup"><span data-stu-id="06d06-469">hello anonymous data type can be used during enumeration as well.</span></span>

<span data-ttu-id="06d06-470">請參閱[簡介 tooLINQ 查詢 (C#)](https://msdn.microsoft.com/library/bb397906.aspx)如需有關 LINQ 查詢和[IEnumerable\<T\>介面](https://msdn.microsoft.com/library/9eekhta0(v=vs.110).aspx)如需有關 IEnumerable\<T\>介面。</span><span class="sxs-lookup"><span data-stu-id="06d06-470">See [Introduction tooLINQ Queries (C#)](https://msdn.microsoft.com/library/bb397906.aspx) for more information about LINQ queries, and [IEnumerable\<T\> Interface](https://msdn.microsoft.com/library/9eekhta0(v=vs.110).aspx) for more information about IEnumerable\<T\> interface.</span></span>

<span data-ttu-id="06d06-471">tooget hello 實際資料值從傳入的 hello `IRowset`，我們使用 get （） 方法 hello`IRow`介面。</span><span class="sxs-lookup"><span data-stu-id="06d06-471">tooget hello actual data values from hello incoming `IRowset`, we use hello Get() method of `IRow` interface.</span></span>

```
mycolumn = row.Get<int>("mycolumn")
```

<span data-ttu-id="06d06-472">個別資料行名稱由呼叫 hello`IRow`結構描述的方法。</span><span class="sxs-lookup"><span data-stu-id="06d06-472">Individual column names can be determined by calling hello `IRow` Schema method.</span></span>

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

<span data-ttu-id="06d06-473">或使用 hello 結構描述資料行名稱：</span><span class="sxs-lookup"><span data-stu-id="06d06-473">Or by using hello schema column name:</span></span>

```
c# row.Get<int>(row.Schema[0].Name)
```

<span data-ttu-id="06d06-474">hello 使用 LINQ 的一般列舉型別看起來像下列 hello:</span><span class="sxs-lookup"><span data-stu-id="06d06-474">hello general enumeration with LINQ looks like hello following:</span></span>

```
var myRowset =
            (from row in left.Rows
                          select new
                          {
                              Mycolumn = row.Get<int>("mycolumn"),
                          }).ToList();
```

<span data-ttu-id="06d06-475">列舉兩個資料列集之後, 我們 tooloop 透過所有資料列。</span><span class="sxs-lookup"><span data-stu-id="06d06-475">After enumerating both rowsets, we are going tooloop through all rows.</span></span> <span data-ttu-id="06d06-476">每個資料列 hello 左資料列集，我們 toofind 符合我們的結合子 hello 條件的所有資料列。</span><span class="sxs-lookup"><span data-stu-id="06d06-476">For each row in hello left rowset, we are going toofind all rows that satisfy hello condition of our combiner.</span></span>

<span data-ttu-id="06d06-477">hello 輸出值必須設定`IUpdatableRow`輸出。</span><span class="sxs-lookup"><span data-stu-id="06d06-477">hello output values must be set with `IUpdatableRow` output.</span></span>

```
output.Set<int>("mycolumn", mycolumn)
```

<span data-ttu-id="06d06-478">藉由呼叫太觸發 hello 實際輸出`yield return output.AsReadOnly();`。</span><span class="sxs-lookup"><span data-stu-id="06d06-478">hello actual output is triggered by calling too`yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="06d06-479">以下是結合器範例：</span><span class="sxs-lookup"><span data-stu-id="06d06-479">Following is a combiner example:</span></span>

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

<span data-ttu-id="06d06-480">在此使用案例案例中，我們會建置 hello 零售商的分析報表。</span><span class="sxs-lookup"><span data-stu-id="06d06-480">In this use-case scenario, we are building an analytics report for hello retailer.</span></span> <span data-ttu-id="06d06-481">hello 目標是的 toofind 成本 $ 20,000 名以上而且的所有產品都銷售透過 hello 較快，透過特定時間範圍內的 hello 規則零售商的網站。</span><span class="sxs-lookup"><span data-stu-id="06d06-481">hello goal is toofind all products that cost more than $20,000 and that sell through hello website faster than through hello regular retailer within a certain time frame.</span></span>

<span data-ttu-id="06d06-482">以下是 hello 基底 U-SQL 指令碼。</span><span class="sxs-lookup"><span data-stu-id="06d06-482">Here is hello base U-SQL script.</span></span> <span data-ttu-id="06d06-483">您可以比較 hello 一般聯結和結合子之間的邏輯：</span><span class="sxs-lookup"><span data-stu-id="06d06-483">You can compare hello logic between a regular JOIN and a combiner:</span></span>

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

<span data-ttu-id="06d06-484">使用者定義的結合子可稱作 hello applier 物件的新執行個體：</span><span class="sxs-lookup"><span data-stu-id="06d06-484">A user-defined combiner can be called as a new instance of hello applier object:</span></span>

```
USING new MyNameSpace.MyCombiner();
```


<span data-ttu-id="06d06-485">或使用的包裝函式的 factory 方法的引動過程 hello:</span><span class="sxs-lookup"><span data-stu-id="06d06-485">Or with hello invocation of a wrapper factory method:</span></span>

```
USING MyNameSpace.MyCombiner();
```

## <a name="use-user-defined-reducers"></a><span data-ttu-id="06d06-486">使用使用者定義歸納器</span><span class="sxs-lookup"><span data-stu-id="06d06-486">Use user-defined reducers</span></span>

<span data-ttu-id="06d06-487">U-SQL 可讓您將自訂的資料列集 reducers toowrite C# 中使用 hello 使用者定義運算子的擴充性架構，並實作 IReducer 介面。</span><span class="sxs-lookup"><span data-stu-id="06d06-487">U-SQL enables you toowrite custom rowset reducers in C# by using hello user-defined operator extensibility framework and implementing an IReducer interface.</span></span>

<span data-ttu-id="06d06-488">使用者定義減壓器或 UDR，可以使用的 tooeliminate 不必要的資料列在資料擷取 （匯入）。</span><span class="sxs-lookup"><span data-stu-id="06d06-488">User-defined reducer, or UDR, can be used tooeliminate unnecessary rows during data extraction (import).</span></span> <span data-ttu-id="06d06-489">也可以使用的 toomanipulate 並評估資料列和資料行。</span><span class="sxs-lookup"><span data-stu-id="06d06-489">It also can be used toomanipulate and evaluate rows and columns.</span></span> <span data-ttu-id="06d06-490">可程式性邏輯為基礎，它也可以定義哪些資料列需要 toobe 擷取。</span><span class="sxs-lookup"><span data-stu-id="06d06-490">Based on programmability logic, it can also define which rows need toobe extracted.</span></span>

<span data-ttu-id="06d06-491">toodefine UDR 類別，我們需要 toocreate`IReducer`具有選擇性介面`SqlUserDefinedReducer`屬性。</span><span class="sxs-lookup"><span data-stu-id="06d06-491">toodefine a UDR class, we need toocreate an `IReducer` interface with an optional `SqlUserDefinedReducer` attribute.</span></span>

<span data-ttu-id="06d06-492">這個類別的介面應該包含 hello 的定義`IEnumerable`介面資料列集覆寫。</span><span class="sxs-lookup"><span data-stu-id="06d06-492">This class interface should contain a definition for hello `IEnumerable` interface rowset override.</span></span>

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

<span data-ttu-id="06d06-493">hello **SqlUserDefinedReducer**屬性會指出 hello 類型應該要註冊為使用者定義的減壓器。</span><span class="sxs-lookup"><span data-stu-id="06d06-493">hello **SqlUserDefinedReducer** attribute indicates that hello type should be registered as a user-defined reducer.</span></span> <span data-ttu-id="06d06-494">這個類別無法繼承。</span><span class="sxs-lookup"><span data-stu-id="06d06-494">This class cannot be inherited.</span></span>
<span data-ttu-id="06d06-495">**SqlUserDefinedReducer** 是使用者定義歸納器之定義的選擇性屬性。</span><span class="sxs-lookup"><span data-stu-id="06d06-495">**SqlUserDefinedReducer** is an optional attribute for a user-defined reducer definition.</span></span> <span data-ttu-id="06d06-496">它已用 toodefine IsRecursive 屬性。</span><span class="sxs-lookup"><span data-stu-id="06d06-496">It's used toodefine IsRecursive property.</span></span>

* <span data-ttu-id="06d06-497">bool     IsRecursive</span><span class="sxs-lookup"><span data-stu-id="06d06-497">bool     IsRecursive</span></span>    
* <span data-ttu-id="06d06-498">**true** = 表示此歸納器是否等冪</span><span class="sxs-lookup"><span data-stu-id="06d06-498">**true**  = Indicates whether this Reducer is idempotent</span></span>

<span data-ttu-id="06d06-499">hello 主要的可程式性物件**輸入**和**輸出**。</span><span class="sxs-lookup"><span data-stu-id="06d06-499">hello main programmability objects are **input** and **output**.</span></span> <span data-ttu-id="06d06-500">hello 輸入的物件是使用的 tooenumerate 輸入資料列。</span><span class="sxs-lookup"><span data-stu-id="06d06-500">hello input object is used tooenumerate input rows.</span></span> <span data-ttu-id="06d06-501">輸出是使用的 tooset 輸出資料列，減少活動的結果。</span><span class="sxs-lookup"><span data-stu-id="06d06-501">Output is used tooset output rows as a result of reducing activity.</span></span>

<span data-ttu-id="06d06-502">輸入資料列列舉型別，我們使用 hello`Row.Get`方法。</span><span class="sxs-lookup"><span data-stu-id="06d06-502">For input rows enumeration, we use hello `Row.Get` method.</span></span>

```
foreach (IRow row in input.Rows)
{
    row.Get<string>("mycolumn");
}
```

<span data-ttu-id="06d06-503">hello 參數 hello`Row.Get`方法是傳遞做為 hello 一部分的資料行`PRODUCE`的 hello 類別`REDUCE`hello U-SQL 基底的指令碼陳述式。</span><span class="sxs-lookup"><span data-stu-id="06d06-503">hello parameter for hello `Row.Get` method is a column that's passed as part of hello `PRODUCE` class of hello `REDUCE` statement of hello U-SQL base script.</span></span> <span data-ttu-id="06d06-504">我們需要 toouse hello 正確資料類型，這裡以及。</span><span class="sxs-lookup"><span data-stu-id="06d06-504">We need toouse hello correct data type here as well.</span></span>

<span data-ttu-id="06d06-505">輸出中，使用 hello`output.Set`方法。</span><span class="sxs-lookup"><span data-stu-id="06d06-505">For output, use hello `output.Set` method.</span></span>

<span data-ttu-id="06d06-506">它是自訂減壓器只有輸出的值所定義的 hello 的重要 toounderstand`output.Set`方法呼叫。</span><span class="sxs-lookup"><span data-stu-id="06d06-506">It is important toounderstand that custom reducer only outputs values that are defined with hello `output.Set` method call.</span></span>

```
output.Set<string>("mycolumn", guid);
```

<span data-ttu-id="06d06-507">hello 實際減壓器的輸出由呼叫觸發`yield return output.AsReadOnly();`。</span><span class="sxs-lookup"><span data-stu-id="06d06-507">hello actual reducer output is triggered by calling `yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="06d06-508">以下是歸納器範例：</span><span class="sxs-lookup"><span data-stu-id="06d06-508">Following is a reducer example:</span></span>

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

<span data-ttu-id="06d06-509">在此使用案例案例中，hello 減壓器即將略過具有空的使用者名稱的資料列。</span><span class="sxs-lookup"><span data-stu-id="06d06-509">In this use-case scenario, hello reducer is skipping rows with an empty user name.</span></span> <span data-ttu-id="06d06-510">每個資料列中資料列集，它會讀取每個必要的資料行，然後評估 hello hello 使用者名稱的長度。</span><span class="sxs-lookup"><span data-stu-id="06d06-510">For each row in rowset, it reads each required column, then evaluates hello length of hello user name.</span></span> <span data-ttu-id="06d06-511">只有當使用者名稱值的長度大於 0，它會輸出 hello 實際資料列。</span><span class="sxs-lookup"><span data-stu-id="06d06-511">It outputs hello actual row only if user name value length is more than 0.</span></span>

<span data-ttu-id="06d06-512">以下為使用自訂歸納器的基底 U-SQL 指令碼：</span><span class="sxs-lookup"><span data-stu-id="06d06-512">Following is base U-SQL script that uses a custom reducer:</span></span>

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
