---
title: "Azure Data Lake 的 U-SQL 可程式性指南 | Microsoft Docs"
description: "深入了解在 Azure Data Lake 可讓您建立雲端型巨量資料平台的服務集。"
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
ms.openlocfilehash: e4e298475d7be7d51c8bd55be498371ed6ce77a9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="u-sql-programmability-guide"></a><span data-ttu-id="fd31d-103">U-SQL 可程式性指南</span><span class="sxs-lookup"><span data-stu-id="fd31d-103">U-SQL programmability guide</span></span>

<span data-ttu-id="fd31d-104">U-SQL 是為巨量資料類型的工作負載所設計的查詢語言。</span><span class="sxs-lookup"><span data-stu-id="fd31d-104">U-SQL is a query language that's designed for big data-type of workloads.</span></span> <span data-ttu-id="fd31d-105">U-SQL 的其中一項獨特功能是，可將類 SQL 的宣告式語言與 C# 所提供的擴充性和可程式性結合在一起。</span><span class="sxs-lookup"><span data-stu-id="fd31d-105">One of the unique features of U-SQL is the combination of the SQL-like declarative language with the extensibility and programmability that's provided by C#.</span></span> <span data-ttu-id="fd31d-106">在本指南中，我們將著重於介紹由 C# 所實現的 U-SQL 語言之擴充性和可程式性。</span><span class="sxs-lookup"><span data-stu-id="fd31d-106">In this guide, we concentrate on the extensibility and programmability of the U-SQL language that's enabled by C#.</span></span>

## <a name="requirements"></a><span data-ttu-id="fd31d-107">需求</span><span class="sxs-lookup"><span data-stu-id="fd31d-107">Requirements</span></span>

<span data-ttu-id="fd31d-108">下載及安裝 [Azure Data Lake Tools for Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504)。</span><span class="sxs-lookup"><span data-stu-id="fd31d-108">Download and install [Azure Data Lake Tools for Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span></span>

## <a name="get-started-with-u-sql"></a><span data-ttu-id="fd31d-109">開始使用 U-SQL</span><span class="sxs-lookup"><span data-stu-id="fd31d-109">Get started with U-SQL</span></span>  

<span data-ttu-id="fd31d-110">我們來看看下面的 U-SQL 指令碼：</span><span class="sxs-lookup"><span data-stu-id="fd31d-110">Let’s look at the following U-SQL script:</span></span>

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

<span data-ttu-id="fd31d-111">它會定義名為 @a 的資料列集，並且從 @a 建立名為 @results 的資料列集。</span><span class="sxs-lookup"><span data-stu-id="fd31d-111">It defines a RowSet called @a and creates a RowSet called @results from @a.</span></span>

## <a name="c-types-and-expressions-in-u-sql-script"></a><span data-ttu-id="fd31d-112">U-SQL 指令碼中的 C# 類型和運算式</span><span class="sxs-lookup"><span data-stu-id="fd31d-112">C# types and expressions in U-SQL script</span></span>

<span data-ttu-id="fd31d-113">U-SQL 運算式是 C# 運算式，與例如 `AND`、`OR` 和 `NOT` 的 U-SQL 邏輯作業合併。</span><span class="sxs-lookup"><span data-stu-id="fd31d-113">A U-SQL Expression is a C# expression combined with U-SQL logical operations such `AND`, `OR`, and `NOT`.</span></span> <span data-ttu-id="fd31d-114">U-SQL 運算式可以與 SELECT、EXTRACT、WHERE、HAVING、GROUP BY 和 DECLARE 搭配使用。</span><span class="sxs-lookup"><span data-stu-id="fd31d-114">U-SQL Expressions can be used with SELECT, EXTRACT, WHERE, HAVING, GROUP BY and DECLARE.</span></span>

<span data-ttu-id="fd31d-115">例如，下列指令碼會剖析字串，該字串是 SELECT 子句中的 DateTime 值。</span><span class="sxs-lookup"><span data-stu-id="fd31d-115">For example, the following script parses a string a DateTime value in the SELECT clause.</span></span>

```
@results =
    SELECT
        customer,
    amount,
    DateTime.Parse(date) AS date
    FROM @a;    
```

<span data-ttu-id="fd31d-116">下列指令碼會剖析字串，該字串是 DECLARE 陳述式中的 DateTime 值。</span><span class="sxs-lookup"><span data-stu-id="fd31d-116">The following script parses a string a DateTime value in a DECLARE statement.</span></span>

```
DECLARE @d DateTime = ToDateTime.Date("2016/01/01");
```

### <a name="use-c-expressions-for-data-type-conversions"></a><span data-ttu-id="fd31d-117">使用 C# 運算式轉換資料類型</span><span class="sxs-lookup"><span data-stu-id="fd31d-117">Use C# expressions for data type conversions</span></span>
<span data-ttu-id="fd31d-118">下列範例示範如何使用 C# 運算式進行日期時間資料轉換。</span><span class="sxs-lookup"><span data-stu-id="fd31d-118">The following example demonstrates how you can do a datetime data conversion by using C# expressions.</span></span> <span data-ttu-id="fd31d-119">在這個特別案例中，字串日期時間資料會轉換成標準日期時間，也就是以午夜 00:00:00 為準的時間標記法。</span><span class="sxs-lookup"><span data-stu-id="fd31d-119">In this particular scenario, string datetime data is converted to standard datetime with midnight 00:00:00 time notation.</span></span>

```
DECLARE @dt String = "2016-07-06 10:23:15";

@rs1 =
    SELECT 
        Convert.ToDateTime(Convert.ToDateTime(@dt).ToString("yyyy-MM-dd")) AS dt,
        dt AS olddt
    FROM @rs0;
OUTPUT @rs1 TO @output_file USING Outputters.Text();
```

### <a name="use-c-expressions-for-todays-date"></a><span data-ttu-id="fd31d-120">使用 C# 運算式來表示今天的日期</span><span class="sxs-lookup"><span data-stu-id="fd31d-120">Use C# expressions for today’s date</span></span>
<span data-ttu-id="fd31d-121">若要提取今天的日期，我們可以將下列 C# 運算式：</span><span class="sxs-lookup"><span data-stu-id="fd31d-121">To pull today’s date, we can use the following C# expression:</span></span>

```
DateTime.Now.ToString("M/d/yyyy")
```

<span data-ttu-id="fd31d-122">如何在指令碼中使用此運算式的範例如下︰</span><span class="sxs-lookup"><span data-stu-id="fd31d-122">Here's an example of how to use this expression in a script:</span></span>

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



## <a name="using-net-assemblies"></a><span data-ttu-id="fd31d-123">使用 .NET 組件</span><span class="sxs-lookup"><span data-stu-id="fd31d-123">Using .NET assemblies</span></span>
<span data-ttu-id="fd31d-124">U-SQL 的擴充性模型極為依賴新增自訂程式碼的能力。</span><span class="sxs-lookup"><span data-stu-id="fd31d-124">U-SQL’s extensibility model relies heavily on the ability to add custom code.</span></span> <span data-ttu-id="fd31d-125">目前，U-SQL 會為您提供簡單的方法，以新增您自己的 Microsoft .NET 為基礎的程式碼 (尤其是 C#)。</span><span class="sxs-lookup"><span data-stu-id="fd31d-125">Currently, U-SQL provides you with easy ways to add your own Microsoft .NET-based code (in particular, C#).</span></span> <span data-ttu-id="fd31d-126">不過，您也可以新增以其他 .NET 語言 (例如 VB.NET 或 F#) 撰寫的自訂程式碼。</span><span class="sxs-lookup"><span data-stu-id="fd31d-126">However, you can also add custom code that's written in other .NET languages, such as VB.NET or F#.</span></span> 

### <a name="register-a-net-assembly"></a><span data-ttu-id="fd31d-127">註冊 .NET 組件</span><span class="sxs-lookup"><span data-stu-id="fd31d-127">Register a .NET assembly</span></span>

<span data-ttu-id="fd31d-128">使用 CREATE ASSEMBLY 陳述式將 .NET 組件放到 U-SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="fd31d-128">Use the CREATE ASSEMBLY statement to place a .NET assembly into a U-SQL Database.</span></span> <span data-ttu-id="fd31d-129">一旦組件放到資料庫，U-SQL 指令碼可以藉由使用 REFERENCE ASSEMBLY 陳述式來使用這些組件。</span><span class="sxs-lookup"><span data-stu-id="fd31d-129">Once an assembly is in a database, U-SQL scripts can use those assemblies by using the REFERENCE ASSEMBLY statement.</span></span> 

<span data-ttu-id="fd31d-130">下列程式碼將說明如何註冊組件：</span><span class="sxs-lookup"><span data-stu-id="fd31d-130">The following code shows how to register an assembly:</span></span>

```
CREATE ASSEMBLY MyDB.[MyAssembly]
    FROM "/myassembly.dll";
```

<span data-ttu-id="fd31d-131">下列程式碼將說明如何參考組件：</span><span class="sxs-lookup"><span data-stu-id="fd31d-131">The following code shows how to reference an assembly:</span></span>

```
REFERENCE ASSEMBLY MyDB.[MyAssembly];
```

<span data-ttu-id="fd31d-132">請參閱更詳細涵蓋此主題的[組件註冊指示](https://blogs.msdn.microsoft.com/azuredatalake/2016/08/26/how-to-register-u-sql-assemblies-in-your-u-sql-catalog/)。</span><span class="sxs-lookup"><span data-stu-id="fd31d-132">Consult the [assembly registration instructions](https://blogs.msdn.microsoft.com/azuredatalake/2016/08/26/how-to-register-u-sql-assemblies-in-your-u-sql-catalog/) that covers this topic in greater detail.</span></span>


### <a name="use-assembly-versioning"></a><span data-ttu-id="fd31d-133">使用組件版本控制</span><span class="sxs-lookup"><span data-stu-id="fd31d-133">Use assembly versioning</span></span>
<span data-ttu-id="fd31d-134">U-SQL 目前使用 .Net Framework 4.5 版。</span><span class="sxs-lookup"><span data-stu-id="fd31d-134">Currently, U-SQL uses the .NET Framework version 4.5.</span></span> <span data-ttu-id="fd31d-135">因此，請確定您自己的組件與該執行階段版本相容。</span><span class="sxs-lookup"><span data-stu-id="fd31d-135">So ensure that your own assemblies are compatible with that version of the runtime.</span></span>

<span data-ttu-id="fd31d-136">如前面所述，U-SQL 會執行 64 位元 (x64) 格式的程式碼。</span><span class="sxs-lookup"><span data-stu-id="fd31d-136">As mentioned earlier, U-SQL runs code in a 64-bit (x64) format.</span></span> <span data-ttu-id="fd31d-137">因此，請確定您的程式碼是編譯為可在 x64 上執行。</span><span class="sxs-lookup"><span data-stu-id="fd31d-137">So make sure that your code is compiled to run on x64.</span></span> <span data-ttu-id="fd31d-138">否則，您會得到如上所示的格式不正確錯誤。</span><span class="sxs-lookup"><span data-stu-id="fd31d-138">Otherwise you get the incorrect format error shown earlier.</span></span>

<span data-ttu-id="fd31d-139">每個上傳的組件 DLL 和資源檔，例如不同的執行階段、原生組件或組態檔中，最多可達 400 MB。</span><span class="sxs-lookup"><span data-stu-id="fd31d-139">Each uploaded assembly DLL and resource file, such as a different runtime, a native assembly, or a config file, can be at most 400 MB.</span></span> <span data-ttu-id="fd31d-140">已部署資源的大小總計 (透過 DEPLOY RESOURCE 或透過參考組件及其他檔案) 不能超過 3 GB。</span><span class="sxs-lookup"><span data-stu-id="fd31d-140">The total size of deployed resources, either via DEPLOY RESOURCE or via references to assemblies and their additional files, cannot exceed 3 GB.</span></span>

<span data-ttu-id="fd31d-141">最後請注意，每一個 U-SQL 資料庫所包含的任何指定組件只能有一個版本。</span><span class="sxs-lookup"><span data-stu-id="fd31d-141">Finally, note that each U-SQL database can only contain one version of any given assembly.</span></span> <span data-ttu-id="fd31d-142">例如，如果您同時需要第 7 版和第 8 版的 NewtonSoft Json.Net 程式庫，您需要將它們註冊到兩個不同的資料庫。</span><span class="sxs-lookup"><span data-stu-id="fd31d-142">For example, if you need both version 7 and version 8 of the NewtonSoft Json.Net library, you need to register them in two different databases.</span></span> <span data-ttu-id="fd31d-143">此外，每個指令碼所參考的指定組件 DLL 只能有一個版本。</span><span class="sxs-lookup"><span data-stu-id="fd31d-143">Furthermore, each script can only refer to one version of a given assembly DLL.</span></span> <span data-ttu-id="fd31d-144">在這方面，U-SQL 會遵循 C# 組件的管理和版本設定語意。</span><span class="sxs-lookup"><span data-stu-id="fd31d-144">In this respect, U-SQL follows the C# assembly management and versioning semantics.</span></span>


## <a name="use-user-defined-functions-udf"></a><span data-ttu-id="fd31d-145">使用使用者定義函式：UDF</span><span class="sxs-lookup"><span data-stu-id="fd31d-145">Use user-defined functions: UDF</span></span>
<span data-ttu-id="fd31d-146">U-SQL 使用者定義函數 (簡稱 UDF) 會編寫常式，以接受參數、執行動作 (例如複雜計算)，以及傳回該動作結果的值。</span><span class="sxs-lookup"><span data-stu-id="fd31d-146">U-SQL user-defined functions, or UDF, are programming routines that accept parameters, perform an action (such as a complex calculation), and return the result of that action as a value.</span></span> <span data-ttu-id="fd31d-147">UDF 的傳回值只能是單一純量。</span><span class="sxs-lookup"><span data-stu-id="fd31d-147">The return value of UDF can only be a single scalar.</span></span> <span data-ttu-id="fd31d-148">U-SQL UDF 可以和任何其他 C# 純量函式一樣，在 U-SQL 基底指令碼中進行呼叫。</span><span class="sxs-lookup"><span data-stu-id="fd31d-148">U-SQL UDF can be called in U-SQL base script like any other C# scalar function.</span></span>

<span data-ttu-id="fd31d-149">我們建議您將 U-SQL 使用者定義函式初始化為**公用**且**靜態**的函式。</span><span class="sxs-lookup"><span data-stu-id="fd31d-149">We recommend that you initialize U-SQL user-defined functions as **public** and **static**.</span></span>

```
public static string MyFunction(string param1)
{
    return "my result";
}
```

<span data-ttu-id="fd31d-150">我們先看看簡單的建立 UDF 範例。</span><span class="sxs-lookup"><span data-stu-id="fd31d-150">First let’s look at the simple example of creating a UDF.</span></span>

<span data-ttu-id="fd31d-151">在此使用案例中，我們必須決定特定使用者首次登入的會計週期 (包括會計季度和會計月份)。</span><span class="sxs-lookup"><span data-stu-id="fd31d-151">In this use-case scenario, we need to determine the fiscal period, including the fiscal quarter and fiscal month of the first sign-in for the specific user.</span></span> <span data-ttu-id="fd31d-152">在我們的案例中，一年的第一個會計月份為六月。</span><span class="sxs-lookup"><span data-stu-id="fd31d-152">The first fiscal month of the year in our scenario is June.</span></span>

<span data-ttu-id="fd31d-153">為了計算會計週期，我們引進了下列 C# 函式：</span><span class="sxs-lookup"><span data-stu-id="fd31d-153">To calculate fiscal period, we introduce the following C# function:</span></span>

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

<span data-ttu-id="fd31d-154">它只會計算會計月份和季度，並傳回字串值。</span><span class="sxs-lookup"><span data-stu-id="fd31d-154">It simply calculates fiscal month and quarter and returns a string value.</span></span> <span data-ttu-id="fd31d-155">六月 (第一個會計季度的第一個月份)，我們使用「Q1:P1」。</span><span class="sxs-lookup"><span data-stu-id="fd31d-155">For June, the first month of the first fiscal quarter, we use "Q1:P1".</span></span> <span data-ttu-id="fd31d-156">七月，我們使用「Q1:P2」，以此類推。</span><span class="sxs-lookup"><span data-stu-id="fd31d-156">For July, we use "Q1:P2", and so on.</span></span>

<span data-ttu-id="fd31d-157">這是一般 C# 函式，我們將使用我們的 U-SQL 專案。</span><span class="sxs-lookup"><span data-stu-id="fd31d-157">This is a regular C# function that we are going to use in our U-SQL project.</span></span>

<span data-ttu-id="fd31d-158">此案例中的程式碼後置區段外觀如下：</span><span class="sxs-lookup"><span data-stu-id="fd31d-158">Here is how the code-behind section looks in this scenario:</span></span>

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

<span data-ttu-id="fd31d-159">現在，我們要從基底 U-SQL 指令碼呼叫此函式。</span><span class="sxs-lookup"><span data-stu-id="fd31d-159">Now we are going to call this function from the base U-SQL script.</span></span> <span data-ttu-id="fd31d-160">若要這樣做，我們必須提供完整函式名稱，包括命名空間，在此案例中為 NameSpace.Class.Function(parameter)。</span><span class="sxs-lookup"><span data-stu-id="fd31d-160">To do this, we have to provide a fully qualified name for the function, including the namespace, which in this case is NameSpace.Class.Function(parameter).</span></span>

```
USQL_Programmability.CustomFunctions.GetFiscalPeriod(dt)
```

<span data-ttu-id="fd31d-161">以下是實際的 U-SQL 基底指令碼：</span><span class="sxs-lookup"><span data-stu-id="fd31d-161">Following is the actual U-SQL base script:</span></span>

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
    TO @output_file 
    USING Outputters.Text();
```

<span data-ttu-id="fd31d-162">以下是指令碼執行的輸出檔案：</span><span class="sxs-lookup"><span data-stu-id="fd31d-162">Following is the output file of the script execution:</span></span>

```
0d8b9630-d5ca-11e5-8329-251efa3a2941,2016-02-11T07:04:17.2630000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User1",""

20843640-d771-11e5-b87b-8b7265c75a44,2016-02-11T07:04:17.2630000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User2",""

301f23d2-d690-11e5-9a98-4b4f60a1836f,2016-02-11T09:01:33.9720000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User3",""
```

<span data-ttu-id="fd31d-163">這個範例示範 U-SQL 中內嵌 UDF 的簡易用法。</span><span class="sxs-lookup"><span data-stu-id="fd31d-163">This example demonstrates a simple usage of inline UDF in U-SQL.</span></span>

### <a name="keep-state-between-udf-invocations"></a><span data-ttu-id="fd31d-164">在 UDF 的引動過程之間保持狀態</span><span class="sxs-lookup"><span data-stu-id="fd31d-164">Keep state between UDF invocations</span></span>
<span data-ttu-id="fd31d-165">U-SQL C# 可程式性物件可以透過程式碼後置全域變數，更加複雜地利用互動性。</span><span class="sxs-lookup"><span data-stu-id="fd31d-165">U-SQL C# programmability objects can be more sophisticated, utilizing interactivity through the code-behind global variables.</span></span> <span data-ttu-id="fd31d-166">讓我們看看下列商務使用案例。</span><span class="sxs-lookup"><span data-stu-id="fd31d-166">Let’s look at the following business use-case scenario.</span></span>

<span data-ttu-id="fd31d-167">在大型組織中，使用者可以切換使用各種內部應用程式。</span><span class="sxs-lookup"><span data-stu-id="fd31d-167">In large organizations, users can switch between varieties of internal applications.</span></span> <span data-ttu-id="fd31d-168">這些可能包括 Microsoft Dynamics CRM、PowerBI 等等。</span><span class="sxs-lookup"><span data-stu-id="fd31d-168">These can include Microsoft Dynamics CRM, PowerBI, and so on.</span></span> <span data-ttu-id="fd31d-169">客戶可能想要以遙測資料分析使用者切換使用不同應用程式的方式、使用趨勢為何等等的資訊。</span><span class="sxs-lookup"><span data-stu-id="fd31d-169">Customers might want to apply a telemetry analysis of how users switch between different applications, what the usage trends are, and so on.</span></span> <span data-ttu-id="fd31d-170">企業的目的是獲得最佳的應用程式使用情況。</span><span class="sxs-lookup"><span data-stu-id="fd31d-170">The goal for the business is to optimize application usage.</span></span> <span data-ttu-id="fd31d-171">他們或許也想要會合併不同應用程式或特定登入常式。</span><span class="sxs-lookup"><span data-stu-id="fd31d-171">They also might want to combine different applications or specific sign-on routines.</span></span>

<span data-ttu-id="fd31d-172">為了達成此目標，我們必須確定工作階段識別碼，以及最後發生之工作階段間的延遲時間。</span><span class="sxs-lookup"><span data-stu-id="fd31d-172">To achieve this goal, we have to determine session IDs and lag time between the last session that occurred.</span></span>

<span data-ttu-id="fd31d-173">我們必須找到上一次登入，然後對所有將為相同應用程式產生的工作階段指派此登入。</span><span class="sxs-lookup"><span data-stu-id="fd31d-173">We need to find a previous sign-in and then assign this sign-in to all sessions that are being generated to the same application.</span></span> <span data-ttu-id="fd31d-174">第一項挑戰是 U-SQL 基底指令碼無法讓我們使用 LAG 函數，對所有已經過計算的資料行套用計算。</span><span class="sxs-lookup"><span data-stu-id="fd31d-174">The first challenge is that U-SQL base script doesn't allow us to apply calculations over already-calculated columns with LAG function.</span></span> <span data-ttu-id="fd31d-175">第二項挑戰在於，我們必須讓相同時間週期內的所有工作階段保持在特定工作階段。</span><span class="sxs-lookup"><span data-stu-id="fd31d-175">The second challenge is that we have to keep the specific session for all sessions within the same time period.</span></span>

<span data-ttu-id="fd31d-176">為了解決這個問題，我們將在程式碼後置區段內使用全域變數：`static public string globalSession;`。</span><span class="sxs-lookup"><span data-stu-id="fd31d-176">To solve this problem, we use a global variable inside a code-behind section: `static public string globalSession;`.</span></span>

<span data-ttu-id="fd31d-177">在我們執行指令碼期間，此全域變數會套用到整個資料列集。</span><span class="sxs-lookup"><span data-stu-id="fd31d-177">This global variable is applied to the entire rowset during our script execution.</span></span>

<span data-ttu-id="fd31d-178">以下是 U-SQL 程式的程式碼後置區段：</span><span class="sxs-lookup"><span data-stu-id="fd31d-178">Here is the code-behind section of our U-SQL program:</span></span>

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

<span data-ttu-id="fd31d-179">這個範例會示範全域變數 `static public string globalSession;` 用於 `getStampUserSession` 函式內，每次工作階段參數變更時都會重新初始化。</span><span class="sxs-lookup"><span data-stu-id="fd31d-179">This example shows the global variable `static public string globalSession;` used inside the `getStampUserSession` function and getting reinitialized each time the Session parameter is changed.</span></span>

<span data-ttu-id="fd31d-180">U-SQL 基礎指令碼如下所示︰</span><span class="sxs-lookup"><span data-stu-id="fd31d-180">The U-SQL base script is as follows:</span></span>

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
    TO @out2
    ORDER BY UserName, EventDateTime ASC
    USING Outputters.Csv();
```

<span data-ttu-id="fd31d-181">第二次計算記憶體資料列集期間會在此呼叫函式 `USQLApplication21.UserSession.getStampUserSession(UserSessionTimestamp)`。</span><span class="sxs-lookup"><span data-stu-id="fd31d-181">Function `USQLApplication21.UserSession.getStampUserSession(UserSessionTimestamp)` is called here during the second memory rowset calculation.</span></span> <span data-ttu-id="fd31d-182">它會傳遞 `UserSessionTimestamp` 資料行，並傳回值直到 `UserSessionTimestamp` 變更。</span><span class="sxs-lookup"><span data-stu-id="fd31d-182">It passes the `UserSessionTimestamp` column and returns the value until `UserSessionTimestamp` has changed.</span></span>

<span data-ttu-id="fd31d-183">輸出檔案如下所示：</span><span class="sxs-lookup"><span data-stu-id="fd31d-183">The output file is as follows:</span></span>

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

<span data-ttu-id="fd31d-184">此範例示範當我們在程式碼後置區段內使用套用至整個記憶體資料列集之全域變數時的更複雜使用案例。</span><span class="sxs-lookup"><span data-stu-id="fd31d-184">This example demonstrates a more complicated use-case scenario in which we use a global variable inside a code-behind section that's applied to the entire memory rowset.</span></span>

## <a name="use-user-defined-types-udt"></a><span data-ttu-id="fd31d-185">使用使用者定義的類型：UDT</span><span class="sxs-lookup"><span data-stu-id="fd31d-185">Use user-defined types: UDT</span></span>
<span data-ttu-id="fd31d-186">使用者定義類型 (UDT) 是 U-SQL 的另一個可程式性功能。</span><span class="sxs-lookup"><span data-stu-id="fd31d-186">User-defined types, or UDT, is another programmability feature of U-SQL.</span></span> <span data-ttu-id="fd31d-187">U-SQL UDT 的作用就像一般的 C# 使用者定義類型。</span><span class="sxs-lookup"><span data-stu-id="fd31d-187">U-SQL UDT acts like a regular C# user-defined type.</span></span> <span data-ttu-id="fd31d-188">C# 是強類型的語言，允許使用內建和自訂的使用者定義類型。</span><span class="sxs-lookup"><span data-stu-id="fd31d-188">C# is a strongly typed language that allows the use of built-in and custom user-defined types.</span></span>

<span data-ttu-id="fd31d-189">在資料列集的頂點之間傳遞 UDT 時，U-SQL 無法以隱含方式序列化或還原序列化任意 UDT。</span><span class="sxs-lookup"><span data-stu-id="fd31d-189">U-SQL cannot implicitly serialize or de-serialize arbitrary UDTs when the UDT is passed between vertices in rowsets.</span></span> <span data-ttu-id="fd31d-190">這表示使用者必須使用 IFormatter 介面提供明確的格式器。</span><span class="sxs-lookup"><span data-stu-id="fd31d-190">This means that the user has to provide an explicit formatter by using the IFormatter interface.</span></span> <span data-ttu-id="fd31d-191">這將提供 U-SQL 將 UDT 序列化和還原序列化的方法。</span><span class="sxs-lookup"><span data-stu-id="fd31d-191">This provides U-SQL with the serialize and de-serialize methods for the UDT.</span></span>

> [!NOTE]
> <span data-ttu-id="fd31d-192">U-SQL 的內建擷取器和 outputter 目前無法將 UDT 資料從檔案往返序列化或還原序列化，即使是已設定 IFormatter 亦然。</span><span class="sxs-lookup"><span data-stu-id="fd31d-192">U-SQL’s built-in extractors and outputters currently cannot serialize or de-serialize UDT data to or from files even with the IFormatter set.</span></span> <span data-ttu-id="fd31d-193">因此當您使用 OUTPUT 陳述式撰寫 UDT 資料至檔案，或是使用解壓縮讀取它時，您必須將它做為字串或位元組陣列傳遞。</span><span class="sxs-lookup"><span data-stu-id="fd31d-193">So when you're writing UDT data to a file with the OUTPUT statement, or reading it with an extractor, you have to pass it as a string or byte array.</span></span> <span data-ttu-id="fd31d-194">然後呼叫序列化，並明確地還原序列化程式碼 (也就是 UDT 的 ToString() 方法)。</span><span class="sxs-lookup"><span data-stu-id="fd31d-194">Then you call the serialization and deserialization code (that is, the UDT’s ToString() method) explicitly.</span></span> <span data-ttu-id="fd31d-195">另一方面，使用者定義的擷取器和 outputter 可以讀取並寫入 UDT。</span><span class="sxs-lookup"><span data-stu-id="fd31d-195">User-defined extractors and outputters, on the other hand, can read and write UDTs.</span></span>

<span data-ttu-id="fd31d-196">如果我們嘗試在 EXTRACTOR 或 OUTPUTTER 中使用 UDT (出自上一個 SELECT)，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="fd31d-196">If we try to use UDT in EXTRACTOR or OUTPUTTER (out of previous SELECT), as shown here:</span></span>

```
@rs1 =
    SELECT 
        MyNameSpace.Myfunction_Returning_UDT(filed1) AS myfield
    FROM @rs0;

OUTPUT @rs1 
    TO @output_file 
    USING Outputters.Text();
```

<span data-ttu-id="fd31d-197">我們會收到下列錯誤：</span><span class="sxs-lookup"><span data-stu-id="fd31d-197">We receive the following error:</span></span>

```
Error   1   E_CSC_USER_INVALIDTYPEINOUTPUTTER: Outputters.Text was used to output column myfield of type
MyNameSpace.Myfunction_Returning_UDT.

Description:

Outputters.Text only supports built-in types.

Resolution:

Implement a custom outputter that knows how to serialize this type, or call a serialization method on the type in
the preceding SELECT.   C:\Users\sergeypu\Documents\Visual Studio 2013\Projects\USQL-Programmability\
USQL-Programmability\Types.usql 52  1   USQL-Programmability
```

<span data-ttu-id="fd31d-198">若要在 Outptutter 中使用 UDT，我們必須使用 ToString() 方法將它序列化為字串，或建立自訂 Outputter。</span><span class="sxs-lookup"><span data-stu-id="fd31d-198">To work with UDT in outputter, we either have to serialize it to string with the ToString() method or create a custom outputter.</span></span>

<span data-ttu-id="fd31d-199">UDT 目前不能用於 GROUP BY。</span><span class="sxs-lookup"><span data-stu-id="fd31d-199">UDTs currently cannot be used in GROUP BY.</span></span> <span data-ttu-id="fd31d-200">如果將 UDT 用於 GROUP BY，系統會擲回下列錯誤︰</span><span class="sxs-lookup"><span data-stu-id="fd31d-200">If UDT is used in GROUP BY, the following error is thrown:</span></span>

```
Error   1   E_CSC_USER_INVALIDTYPEINCLAUSE: GROUP BY doesn't support type MyNameSpace.Myfunction_Returning_UDT
for column myfield

Description:

GROUP BY doesn't support UDT or Complex types.

Resolution:

Add a SELECT statement where you can project a scalar column that you want to use with GROUP BY.
C:\Users\sergeypu\Documents\Visual Studio 2013\Projects\USQL-Programmability\USQL-Programmability\Types.usql
62  5   USQL-Programmability
```

<span data-ttu-id="fd31d-201">若要定義 UDT，我們必須︰</span><span class="sxs-lookup"><span data-stu-id="fd31d-201">To define a UDT, we have to:</span></span>

* <span data-ttu-id="fd31d-202">新增下列命名空間：</span><span class="sxs-lookup"><span data-stu-id="fd31d-202">Add the following namespaces:</span></span>

```
using Microsoft.Analytics.Interfaces
using System.IO;
```

* <span data-ttu-id="fd31d-203">新增 `Microsoft.Analytics.Interfaces`，其為 UDT 介面所需。</span><span class="sxs-lookup"><span data-stu-id="fd31d-203">Add `Microsoft.Analytics.Interfaces`, which is required for the UDT interfaces.</span></span> <span data-ttu-id="fd31d-204">此外，`System.IO` 可能需要用來定義 IFormatter 介面。</span><span class="sxs-lookup"><span data-stu-id="fd31d-204">In addition, `System.IO` might be needed to define the IFormatter interface.</span></span>

* <span data-ttu-id="fd31d-205">使用 SqlUserDefinedType 屬性來定義使用者定義類型。</span><span class="sxs-lookup"><span data-stu-id="fd31d-205">Define a used-defined type with SqlUserDefinedType attribute.</span></span>

<span data-ttu-id="fd31d-206">**SqlUserDefinedType** 可用來將組件中的類型定義標示為 U-SQL 中的使用者定義類型 (UDT)。</span><span class="sxs-lookup"><span data-stu-id="fd31d-206">**SqlUserDefinedType** is used to mark a type definition in an assembly as a user-defined type (UDT) in U-SQL.</span></span> <span data-ttu-id="fd31d-207">屬性 (attribute) 上的屬性 (property) 會反映 UDT 的實際特性。</span><span class="sxs-lookup"><span data-stu-id="fd31d-207">The properties on the attribute reflect the physical characteristics of the UDT.</span></span> <span data-ttu-id="fd31d-208">這個類別無法繼承。</span><span class="sxs-lookup"><span data-stu-id="fd31d-208">This class cannot be inherited.</span></span>

<span data-ttu-id="fd31d-209">SqlUserDefinedType 是 UDT 定義的必要屬性 (attribute)。</span><span class="sxs-lookup"><span data-stu-id="fd31d-209">SqlUserDefinedType is a required attribute for UDT definition.</span></span>

<span data-ttu-id="fd31d-210">類別的建構函式：</span><span class="sxs-lookup"><span data-stu-id="fd31d-210">The constructor of the class:</span></span>  

* <span data-ttu-id="fd31d-211">SqlUserDefinedTypeAttribute (類型格式器)</span><span class="sxs-lookup"><span data-stu-id="fd31d-211">SqlUserDefinedTypeAttribute (type formatter)</span></span>

* <span data-ttu-id="fd31d-212">輸入格式器︰需要參數來定義 UDT 格式器--明確地說，必須在這裡傳遞 `IFormatter` 介面的類型。</span><span class="sxs-lookup"><span data-stu-id="fd31d-212">Type formatter: Required parameter to define an UDT formatter--specifically, the type of the `IFormatter` interface must be passed here.</span></span>

```
[SqlUserDefinedType(typeof(MyTypeFormatter))]
public class MyType
{ … }
```

* <span data-ttu-id="fd31d-213">典型的 UDT 也需要 IFormatter 介面定義，如下列範例所示︰</span><span class="sxs-lookup"><span data-stu-id="fd31d-213">Typical UDT also requires definition of the IFormatter interface, as shown in the following example:</span></span>

```
public class MyTypeFormatter : IFormatter<MyType>
{
    public void Serialize(MyType instance, IColumnWriter writer, ISerializationContext context)
    { … }

    public MyType Deserialize(IColumnReader reader, ISerializationContext context)
    { … }
}
```

<span data-ttu-id="fd31d-214">用來將根類型為 \<typeparamref name="T"> 之物件圖形序列化和還原序列化的 `IFormatter` 介面。</span><span class="sxs-lookup"><span data-stu-id="fd31d-214">The `IFormatter` interface serializes and de-serializes an object graph with the root type of \<typeparamref name="T">.</span></span>

<span data-ttu-id="fd31d-215">\<typeparam name="T"> 要序列化和還原序列化之物件圖形的根類型。</span><span class="sxs-lookup"><span data-stu-id="fd31d-215">\<typeparam name="T">The root type for the object graph to serialize and de-serialize.</span></span>

* <span data-ttu-id="fd31d-216">**還原序列化**：對所提供串流上的資料還原序列化，並重組物件的圖形。</span><span class="sxs-lookup"><span data-stu-id="fd31d-216">**Deserialize**: De-serializes the data on the provided stream and reconstitutes the graph of objects.</span></span>

* <span data-ttu-id="fd31d-217">**序列化**：使用指定根將物件或物件圖形序列化到所提供的串流。</span><span class="sxs-lookup"><span data-stu-id="fd31d-217">**Serialize**: Serializes an object, or graph of objects, with the given root to the provided stream.</span></span>

<span data-ttu-id="fd31d-218">`MyType` 執行個體：類型的執行個體。</span><span class="sxs-lookup"><span data-stu-id="fd31d-218">`MyType` instance: Instance of the type.</span></span>  
<span data-ttu-id="fd31d-219">`IColumnWriter` writer / `IColumnReader` 讀取器：基礎資料行串流。</span><span class="sxs-lookup"><span data-stu-id="fd31d-219">`IColumnWriter` writer / `IColumnReader` reader: The underlying column stream.</span></span>  
<span data-ttu-id="fd31d-220">`ISerializationContext` 內容：定義一組旗標的列舉，可在序列化期間指定串流的來源或目的地內容。</span><span class="sxs-lookup"><span data-stu-id="fd31d-220">`ISerializationContext` context: Enum that defines a set of flags that specifies the source or destination context for the stream during serialization.</span></span>

* <span data-ttu-id="fd31d-221">**中繼**：指定來源或目的地內容不是持續性存放區。</span><span class="sxs-lookup"><span data-stu-id="fd31d-221">**Intermediate**: Specifies that the source or destination context is not a persisted store.</span></span>

* <span data-ttu-id="fd31d-222">**持續性**：指定來源或目的地內容是持續性存放區。</span><span class="sxs-lookup"><span data-stu-id="fd31d-222">**Persistence**: Specifies that the source or destination context is a persisted store.</span></span>

<span data-ttu-id="fd31d-223">做為一般的 C# 類型，U-SQL UDT 定義可包括 +/==/!= 等運算子的覆寫。</span><span class="sxs-lookup"><span data-stu-id="fd31d-223">As a regular C# type, a U-SQL UDT definition can include overrides for operators such as +/==/!=.</span></span> <span data-ttu-id="fd31d-224">它也可以包含靜態方法。</span><span class="sxs-lookup"><span data-stu-id="fd31d-224">It can also include static methods.</span></span> <span data-ttu-id="fd31d-225">例如，如果我們要使用此 UDT 做為 U-SQL MIN 彙總函式的參數，我們必須定義 < 運算子覆寫。</span><span class="sxs-lookup"><span data-stu-id="fd31d-225">For example, if we are going to use this UDT as a parameter to a U-SQL MIN aggregate function, we have to define < operator override.</span></span>

<span data-ttu-id="fd31d-226">本指南稍早曾示範過從格式為 Qn:Pn (Q1:P10) 之特定日期識別會計週期的範例。</span><span class="sxs-lookup"><span data-stu-id="fd31d-226">Earlier in this guide, we demonstrated an example for fiscal period identification from the specific date in the format Qn:Pn (Q1:P10).</span></span> <span data-ttu-id="fd31d-227">下列範例將示範如何為會計週期值定義自訂類型。</span><span class="sxs-lookup"><span data-stu-id="fd31d-227">The following example shows how to define a custom type for fiscal period values.</span></span>

<span data-ttu-id="fd31d-228">以下是具有自訂 UDT 和 IFormatter 介面的程式碼後置區段範例︰</span><span class="sxs-lookup"><span data-stu-id="fd31d-228">Following is an example of a code-behind section with custom UDT and IFormatter interface:</span></span>

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

<span data-ttu-id="fd31d-229">已定義的類型包含兩個數字：季度和月份。</span><span class="sxs-lookup"><span data-stu-id="fd31d-229">The defined type includes two numbers: quarter and month.</span></span> <span data-ttu-id="fd31d-230">運算子 ==/!=/>/< 和靜態方法 ToString() 定義於此。</span><span class="sxs-lookup"><span data-stu-id="fd31d-230">Operators ==/!=/>/< and static method ToString() are defined here.</span></span>

<span data-ttu-id="fd31d-231">如先前所述，UDT 可用於 SELECT 運算式中，但不能用在沒有自訂序列化的 OUTPUTTER/EXTRACTOR。</span><span class="sxs-lookup"><span data-stu-id="fd31d-231">As mentioned earlier, UDT can be used in SELECT expressions, but cannot be used in OUTPUTTER/EXTRACTOR without custom serialization.</span></span> <span data-ttu-id="fd31d-232">它必須使用 ToString() 序列化為字串或與自訂 OUTPUTTER/EXTRACTOR 搭配使用。</span><span class="sxs-lookup"><span data-stu-id="fd31d-232">It either has to be serialized as a string with ToString() or used with a custom OUTPUTTER/EXTRACTOR.</span></span>

<span data-ttu-id="fd31d-233">現在我們來討論一下 UDT 的使用方式。</span><span class="sxs-lookup"><span data-stu-id="fd31d-233">Now let’s discuss usage of UDT.</span></span> <span data-ttu-id="fd31d-234">在程式碼後置區段中，我們已將 GetFiscalPeriod 函式變更為：</span><span class="sxs-lookup"><span data-stu-id="fd31d-234">In a code-behind section, we changed our GetFiscalPeriod function to the following:</span></span>

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

<span data-ttu-id="fd31d-235">如您所見，它會傳回 FiscalPeriod 類型的值。</span><span class="sxs-lookup"><span data-stu-id="fd31d-235">As you can see, it returns the value of our FiscalPeriod type.</span></span>

<span data-ttu-id="fd31d-236">這裡我們提供如何在 U-SQL 基底指令碼中進一步使用它的範例。</span><span class="sxs-lookup"><span data-stu-id="fd31d-236">Here we provide an example of how to use it further in U-SQL base script.</span></span> <span data-ttu-id="fd31d-237">這個範例會示範從 U-SQL 指令碼叫用 UDT 的不同方式。</span><span class="sxs-lookup"><span data-stu-id="fd31d-237">This example demonstrates different forms of UDT invocation from U-SQL script.</span></span>

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

       // This user-defined type was created in the prior SELECT.  Passing the UDT to this subsequent SELECT would have failed if the UDT was not annotated with an IFormatter.
           fiscalperiod_adjusted.ToString() AS fiscalperiod_adjusted,
           user,
           des
    FROM @rs1;

OUTPUT @rs2 
    TO @output_file 
    USING Outputters.Text();
```

<span data-ttu-id="fd31d-238">以下是完整程式碼後置區段的範例︰</span><span class="sxs-lookup"><span data-stu-id="fd31d-238">Here's an example of a full code-behind section:</span></span>

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

## <a name="use-user-defined-aggregates-udagg"></a><span data-ttu-id="fd31d-239">使用使用者定義彙總：UDAGG</span><span class="sxs-lookup"><span data-stu-id="fd31d-239">Use user-defined aggregates: UDAGG</span></span>
<span data-ttu-id="fd31d-240">使用者定義彙總是指並非 U-SQL 現成提供的彙總相關函式。</span><span class="sxs-lookup"><span data-stu-id="fd31d-240">User-defined aggregates are any aggregation-related functions that are not shipped out-of-the-box with U-SQL.</span></span> <span data-ttu-id="fd31d-241">其範例包括用來執行自訂數學計算、字串串連、使用字串之操作等彙總。</span><span class="sxs-lookup"><span data-stu-id="fd31d-241">The example can be an aggregate to perform custom math calculations, string concatenations, manipulations with strings, and so on.</span></span>

<span data-ttu-id="fd31d-242">使用者定義彙總的基底類別定義如下所示：</span><span class="sxs-lookup"><span data-stu-id="fd31d-242">The user-defined aggregate base class definition is as follows:</span></span>

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

<span data-ttu-id="fd31d-243">**SqlUserDefinedAggregate** 表示類型應該註冊為使用者定義彙總。</span><span class="sxs-lookup"><span data-stu-id="fd31d-243">**SqlUserDefinedAggregate** indicates that the type should be registered as a user-defined aggregate.</span></span> <span data-ttu-id="fd31d-244">這個類別無法繼承。</span><span class="sxs-lookup"><span data-stu-id="fd31d-244">This class cannot be inherited.</span></span>

<span data-ttu-id="fd31d-245">SqlUserDefinedType 是 UDAGG 定義的**選擇性**屬性。</span><span class="sxs-lookup"><span data-stu-id="fd31d-245">SqlUserDefinedType attribute is **optional** for UDAGG definition.</span></span>


<span data-ttu-id="fd31d-246">基底類別可讓您傳遞三個抽象參數：其中兩個做為輸入參數，一個做為結果參數。</span><span class="sxs-lookup"><span data-stu-id="fd31d-246">The base class allows you to pass three abstract parameters: two as input parameters and one as the result.</span></span> <span data-ttu-id="fd31d-247">資料類型會變動，但應該會在繼承類別時進行定義。</span><span class="sxs-lookup"><span data-stu-id="fd31d-247">The data types are variable and should be defined during class inheritance.</span></span>

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

* <span data-ttu-id="fd31d-248">**Init** 會在計算期間，為每個群組叫用一次。</span><span class="sxs-lookup"><span data-stu-id="fd31d-248">**Init** invokes once for each group during computation.</span></span> <span data-ttu-id="fd31d-249">Init 可為每個彙總群組提供初始化常式。</span><span class="sxs-lookup"><span data-stu-id="fd31d-249">It provides an initialization routine for each aggregation group.</span></span>  
* <span data-ttu-id="fd31d-250">**Accumulate** 會為每個值執行一次。</span><span class="sxs-lookup"><span data-stu-id="fd31d-250">**Accumulate** is executed once for each value.</span></span> <span data-ttu-id="fd31d-251">它提供彙總演算法的主要功能。</span><span class="sxs-lookup"><span data-stu-id="fd31d-251">It provides the main functionality for the aggregation algorithm.</span></span> <span data-ttu-id="fd31d-252">在繼承類別時，它可用來彙總各種資料類型的值。</span><span class="sxs-lookup"><span data-stu-id="fd31d-252">It can be used to aggregate values with various data types that are defined during class inheritance.</span></span> <span data-ttu-id="fd31d-253">它可接受兩個變數資料類型的參數。</span><span class="sxs-lookup"><span data-stu-id="fd31d-253">It can accept two parameters of variable data types.</span></span>
* <span data-ttu-id="fd31d-254">**Terminate** 在處理結束時對每個彙總群組執行一次，以輸出每個群組的結果。</span><span class="sxs-lookup"><span data-stu-id="fd31d-254">**Terminate** is executed once per aggregation group at the end of processing to output the result for each group.</span></span>

<span data-ttu-id="fd31d-255">若要宣告正確的輸入和輸出資料類型，使用類別定義如下所示︰</span><span class="sxs-lookup"><span data-stu-id="fd31d-255">To declare correct input and output data types, use the class definition as follows:</span></span>

```
public abstract class IAggregate<T1, T2, TResult> : IAggregate
```

* <span data-ttu-id="fd31d-256">T1：要累積的第一個參數</span><span class="sxs-lookup"><span data-stu-id="fd31d-256">T1: First parameter to accumulate</span></span>
* <span data-ttu-id="fd31d-257">T2：要累積的第二個參數</span><span class="sxs-lookup"><span data-stu-id="fd31d-257">T2: First parameter to accumulate</span></span>
* <span data-ttu-id="fd31d-258">TResult：傳回終止的類型</span><span class="sxs-lookup"><span data-stu-id="fd31d-258">TResult: Return type of terminate</span></span>

<span data-ttu-id="fd31d-259">例如：</span><span class="sxs-lookup"><span data-stu-id="fd31d-259">For example:</span></span>

```
public class GuidAggregate : IAggregate<string, int, int>
```

<span data-ttu-id="fd31d-260">或</span><span class="sxs-lookup"><span data-stu-id="fd31d-260">or</span></span>

```
public class GuidAggregate : IAggregate<string, string, string>
```

### <a name="use-udagg-in-u-sql"></a><span data-ttu-id="fd31d-261">在 U-SQL 中使用 UDAGG</span><span class="sxs-lookup"><span data-stu-id="fd31d-261">Use UDAGG in U-SQL</span></span>
<span data-ttu-id="fd31d-262">若要使用 UDAGG，請先在程式碼後置中加以定義，或如稍早所述從現存的可程式性 DLL 參考它。</span><span class="sxs-lookup"><span data-stu-id="fd31d-262">To use UDAGG, first define it in code-behind or reference it from the existent programmability DLL as discussed earlier.</span></span>

<span data-ttu-id="fd31d-263">然後使用下列語法：</span><span class="sxs-lookup"><span data-stu-id="fd31d-263">Then use the following syntax:</span></span>

```
AGG<UDAGG_functionname>(param1,param2)
```

<span data-ttu-id="fd31d-264">UDAGG 範例如下：</span><span class="sxs-lookup"><span data-stu-id="fd31d-264">Here is an example of UDAGG:</span></span>

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

<span data-ttu-id="fd31d-265">以及基底 U-SQL 指令碼：</span><span class="sxs-lookup"><span data-stu-id="fd31d-265">And base U-SQL script:</span></span>

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

OUTPUT @rs1 TO @output_file USING Outputters.Text();
```

<span data-ttu-id="fd31d-266">在此使用案例中，我們會串連特定使用者的類別 GUID。</span><span class="sxs-lookup"><span data-stu-id="fd31d-266">In this use-case scenario, we concatenate class GUIDs for the specific users.</span></span>

## <a name="use-user-defined-objects-udo"></a><span data-ttu-id="fd31d-267">使用使用者定義物件：UDO</span><span class="sxs-lookup"><span data-stu-id="fd31d-267">Use user-defined objects: UDO</span></span>
<span data-ttu-id="fd31d-268">U-SQL 可讓您定義自訂可程式性物件，我們將它稱為使用者定義物件，簡稱 UDO。</span><span class="sxs-lookup"><span data-stu-id="fd31d-268">U-SQL enables you to define custom programmability objects, which are called user-defined objects or UDO.</span></span>

<span data-ttu-id="fd31d-269">以下是 U-SQL 中的 UDO 清單：</span><span class="sxs-lookup"><span data-stu-id="fd31d-269">The following is a list of UDO in U-SQL:</span></span>

* <span data-ttu-id="fd31d-270">使用者定義擷取器</span><span class="sxs-lookup"><span data-stu-id="fd31d-270">User-defined extractors</span></span>
    * <span data-ttu-id="fd31d-271">逐列擷取</span><span class="sxs-lookup"><span data-stu-id="fd31d-271">Extract row by row</span></span>
    * <span data-ttu-id="fd31d-272">用來實作從自訂結構化檔案擷取資料的作業</span><span class="sxs-lookup"><span data-stu-id="fd31d-272">Used to implement data extraction from custom structured files</span></span>

* <span data-ttu-id="fd31d-273">使用者定義輸出器</span><span class="sxs-lookup"><span data-stu-id="fd31d-273">User-defined outputters</span></span>
    * <span data-ttu-id="fd31d-274">逐列輸出</span><span class="sxs-lookup"><span data-stu-id="fd31d-274">Output row by row</span></span>
    * <span data-ttu-id="fd31d-275">用來輸出自訂資料類型或用來自訂檔案格式</span><span class="sxs-lookup"><span data-stu-id="fd31d-275">Used to output custom data types or custom file formats</span></span>

* <span data-ttu-id="fd31d-276">使用者定義處理器</span><span class="sxs-lookup"><span data-stu-id="fd31d-276">User-defined processors</span></span>
    * <span data-ttu-id="fd31d-277">擷取一列並產生一列</span><span class="sxs-lookup"><span data-stu-id="fd31d-277">Take one row and produce one row</span></span>
    * <span data-ttu-id="fd31d-278">用來減少資料行數目，或以衍生自現存資料行集的值產生新的資料行</span><span class="sxs-lookup"><span data-stu-id="fd31d-278">Used to reduce the number of columns or produce new columns with values that are derived from an existing column set</span></span>

* <span data-ttu-id="fd31d-279">使用者定義套用器</span><span class="sxs-lookup"><span data-stu-id="fd31d-279">User-defined appliers</span></span>
    * <span data-ttu-id="fd31d-280">擷取一列並產生 0 到 n 列</span><span class="sxs-lookup"><span data-stu-id="fd31d-280">Take one row and produce 0 to n rows</span></span>
    * <span data-ttu-id="fd31d-281">與 OUTER/CROSS APPLY 搭配使用</span><span class="sxs-lookup"><span data-stu-id="fd31d-281">Used with OUTER/CROSS APPLY</span></span>

* <span data-ttu-id="fd31d-282">使用者定義結合器</span><span class="sxs-lookup"><span data-stu-id="fd31d-282">User-defined combiners</span></span>
    * <span data-ttu-id="fd31d-283">結合資料列集--使用者定義 JOIN</span><span class="sxs-lookup"><span data-stu-id="fd31d-283">Combines rowsets--user-defined JOINs</span></span>

* <span data-ttu-id="fd31d-284">使用者定義歸納器</span><span class="sxs-lookup"><span data-stu-id="fd31d-284">User-defined reducers</span></span>
    * <span data-ttu-id="fd31d-285">擷取 n 列並產生一列</span><span class="sxs-lookup"><span data-stu-id="fd31d-285">Take n rows and produce one row</span></span>
    * <span data-ttu-id="fd31d-286">用來減少資料列數目</span><span class="sxs-lookup"><span data-stu-id="fd31d-286">Used to reduce the number of rows</span></span>

<span data-ttu-id="fd31d-287">U-SQL 指令碼中通常會明確地呼叫 UDO 以做為下列 U-SQL 陳述式的一部分︰</span><span class="sxs-lookup"><span data-stu-id="fd31d-287">UDO is typically called explicitly in U-SQL script as part of the following U-SQL statements:</span></span>

* <span data-ttu-id="fd31d-288">EXTRACT</span><span class="sxs-lookup"><span data-stu-id="fd31d-288">EXTRACT</span></span>
* <span data-ttu-id="fd31d-289">OUTPUT</span><span class="sxs-lookup"><span data-stu-id="fd31d-289">OUTPUT</span></span>
* <span data-ttu-id="fd31d-290">PROCESS</span><span class="sxs-lookup"><span data-stu-id="fd31d-290">PROCESS</span></span>
* <span data-ttu-id="fd31d-291">COMBINE</span><span class="sxs-lookup"><span data-stu-id="fd31d-291">COMBINE</span></span>
* <span data-ttu-id="fd31d-292">REDUCE</span><span class="sxs-lookup"><span data-stu-id="fd31d-292">REDUCE</span></span>

> [!NOTE]  
> <span data-ttu-id="fd31d-293">UDO 限制為 0.5 Gb 記憶體。</span><span class="sxs-lookup"><span data-stu-id="fd31d-293">UDO’s are limited to consume 0.5Gb memory.</span></span>  <span data-ttu-id="fd31d-294">這個記憶體限制不適用於本機執行。</span><span class="sxs-lookup"><span data-stu-id="fd31d-294">This memory limitation does not apply to local executions.</span></span>

## <a name="use-user-defined-extractors"></a><span data-ttu-id="fd31d-295">使用使用者定義擷取器</span><span class="sxs-lookup"><span data-stu-id="fd31d-295">Use user-defined extractors</span></span>
<span data-ttu-id="fd31d-296">U-SQL 可讓您使用 EXTRACT 陳述式來匯入外部資料。</span><span class="sxs-lookup"><span data-stu-id="fd31d-296">U-SQL allows you to import external data by using an EXTRACT statement.</span></span> <span data-ttu-id="fd31d-297">EXTRACT 陳述式可以使用內建的 UDO 擷取器：</span><span class="sxs-lookup"><span data-stu-id="fd31d-297">An EXTRACT statement can use built-in UDO extractors:</span></span>  

* <span data-ttu-id="fd31d-298">Extractors.Text()︰可從不同編碼的分隔文字檔進行擷取。</span><span class="sxs-lookup"><span data-stu-id="fd31d-298">*Extractors.Text()*: Provides extraction from delimited text files of different encodings.</span></span>

* <span data-ttu-id="fd31d-299">Extractors.Csv()︰可從不同編碼的逗號分隔值 (CSV) 檔案進行擷取。</span><span class="sxs-lookup"><span data-stu-id="fd31d-299">*Extractors.Csv()*: Provides extraction from comma-separated value (CSV) files of different encodings.</span></span>

* <span data-ttu-id="fd31d-300">Extractors.Tsv()︰可從不同編碼的定位鍵分隔值 (TSV) 檔案進行擷取。</span><span class="sxs-lookup"><span data-stu-id="fd31d-300">*Extractors.Tsv()*: Provides extraction from tab-separated value (TSV) files of different encodings.</span></span>

<span data-ttu-id="fd31d-301">它很適合用來開發自訂擷取器。</span><span class="sxs-lookup"><span data-stu-id="fd31d-301">It can be useful to develop a custom extractor.</span></span> <span data-ttu-id="fd31d-302">在匯入資料期間，如果我們想要執行下列任何作業，這會很有幫助：</span><span class="sxs-lookup"><span data-stu-id="fd31d-302">This can be helpful during data import if we want to do any of the following tasks:</span></span>

* <span data-ttu-id="fd31d-303">分割資料行並修改個別值，以修改輸入資料。</span><span class="sxs-lookup"><span data-stu-id="fd31d-303">Modify input data by splitting columns and modifying individual values.</span></span> <span data-ttu-id="fd31d-304">PROCESSOR 功能更適合用來結合資料行。</span><span class="sxs-lookup"><span data-stu-id="fd31d-304">The PROCESSOR functionality is better for combining columns.</span></span>
* <span data-ttu-id="fd31d-305">剖析非結構化資料 (例如網頁/電子郵件) 或半非結構化資料 (例如 XML/JSON)。</span><span class="sxs-lookup"><span data-stu-id="fd31d-305">Parse unstructured data such as Web pages and emails, or semi-unstructured data such as XML/JSON.</span></span>
* <span data-ttu-id="fd31d-306">剖析編碼不受支援的資料。</span><span class="sxs-lookup"><span data-stu-id="fd31d-306">Parse data in unsupported encoding.</span></span>

<span data-ttu-id="fd31d-307">若要定義使用者定義擷取器 (UDE)，我們需要建立 `IExtractor` 介面。</span><span class="sxs-lookup"><span data-stu-id="fd31d-307">To define a user-defined extractor, or UDE, we need to create an `IExtractor` interface.</span></span> <span data-ttu-id="fd31d-308">擷取器的所有輸入參數 (例如資料行/資料列分隔符號和編碼等) 都必須在類別的建構函式中加以定義。</span><span class="sxs-lookup"><span data-stu-id="fd31d-308">All input parameters to the extractor, such as column/row delimiters, and encoding, need to be defined in the constructor of the class.</span></span> <span data-ttu-id="fd31d-309">`IExtractor` 介面也應包含 `IEnumerable<IRow>` 覆寫的定義，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="fd31d-309">The `IExtractor`  interface should also contain a definition for the `IEnumerable<IRow>` override as follows:</span></span>

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

<span data-ttu-id="fd31d-310">**SqlUserDefinedExtractor** 表示類型應該註冊為使用者定義擷取器。</span><span class="sxs-lookup"><span data-stu-id="fd31d-310">The **SqlUserDefinedExtractor** attribute indicates that the type should be registered as a user-defined extractor.</span></span> <span data-ttu-id="fd31d-311">這個類別無法繼承。</span><span class="sxs-lookup"><span data-stu-id="fd31d-311">This class cannot be inherited.</span></span>

<span data-ttu-id="fd31d-312">SqlUserDefinedExtractor 是 UDE 定義的選擇性屬性。</span><span class="sxs-lookup"><span data-stu-id="fd31d-312">SqlUserDefinedExtractor is an optional attribute for UDE definition.</span></span> <span data-ttu-id="fd31d-313">它可用來定義 UDE 物件的 AtomicFileProcessing 屬性。</span><span class="sxs-lookup"><span data-stu-id="fd31d-313">It used to define AtomicFileProcessing property for the UDE object.</span></span>

* <span data-ttu-id="fd31d-314">bool     AtomicFileProcessing</span><span class="sxs-lookup"><span data-stu-id="fd31d-314">bool     AtomicFileProcessing</span></span>   

* <span data-ttu-id="fd31d-315">**true** = 表示此擷取器需要不可部分完成的輸入檔 (JSON、XML ...)</span><span class="sxs-lookup"><span data-stu-id="fd31d-315">**true** = Indicates that this extractor requires atomic input files (JSON, XML, ...)</span></span>
* <span data-ttu-id="fd31d-316">**false** = 表示此擷取器可以處理分割/分散式檔案 (CSV、SEQ ...)</span><span class="sxs-lookup"><span data-stu-id="fd31d-316">**false** = Indicates that this extractor can deal with split / distributed files (CSV, SEQ, ...)</span></span>

<span data-ttu-id="fd31d-317">主要的 UDE 可程式性物件為「輸入」和「輸出」。</span><span class="sxs-lookup"><span data-stu-id="fd31d-317">The main UDE programmability objects are **input** and **output**.</span></span> <span data-ttu-id="fd31d-318">輸入物件用來列舉輸入資料做為 `IUnstructuredReader`。</span><span class="sxs-lookup"><span data-stu-id="fd31d-318">The input object is used to enumerate input data as `IUnstructuredReader`.</span></span> <span data-ttu-id="fd31d-319">輸入物件可用來將輸出資料設定為擷取器活動的結果。</span><span class="sxs-lookup"><span data-stu-id="fd31d-319">The output object is used to set output data as a result of the extractor activity.</span></span>

<span data-ttu-id="fd31d-320">輸入資料是透過 `System.IO.Stream` 和 `System.IO.StreamReader` 來存取。</span><span class="sxs-lookup"><span data-stu-id="fd31d-320">The input data is accessed through `System.IO.Stream` and `System.IO.StreamReader`.</span></span>

<span data-ttu-id="fd31d-321">若要列舉輸入資料行，我們必須先使用資料列分隔符號分割輸入串流。</span><span class="sxs-lookup"><span data-stu-id="fd31d-321">For input columns enumeration, we first split the input stream by using a row delimiter.</span></span>

```
foreach (Stream current in input.Split(my_row_delimiter))
{
…
}
```

<span data-ttu-id="fd31d-322">然後，將輸入資料列進一步分割為資料行組件。</span><span class="sxs-lookup"><span data-stu-id="fd31d-322">Then, further split input row into column parts.</span></span>

```
foreach (Stream current in input.Split(my_row_delimiter))
{
…
    string[] parts = line.Split(my_column_delimiter);
    foreach (string part in parts)
    { … }
}
```

<span data-ttu-id="fd31d-323">若要設定輸出資料，我們可以使用 `output.Set` 方法。</span><span class="sxs-lookup"><span data-stu-id="fd31d-323">To set output data, we use the `output.Set` method.</span></span>

<span data-ttu-id="fd31d-324">請務必了解，自訂擷取程式只會輸出資料行和使用輸出定義的值。</span><span class="sxs-lookup"><span data-stu-id="fd31d-324">It's important to understand that the custom extractor only outputs columns and values that are defined with the output.</span></span> <span data-ttu-id="fd31d-325">設定方法呼叫。</span><span class="sxs-lookup"><span data-stu-id="fd31d-325">Set method call.</span></span>

```
output.Set<string>(count, part);
```

<span data-ttu-id="fd31d-326">呼叫 `yield return output.AsReadOnly();` 就會觸發實際的擷取器輸出。</span><span class="sxs-lookup"><span data-stu-id="fd31d-326">The actual extractor output is triggered by calling `yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="fd31d-327">以下是擷取器範例：</span><span class="sxs-lookup"><span data-stu-id="fd31d-327">Following is the extractor example:</span></span>

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
         //Read the input line by line
         foreach (Stream current in input.Split(_encoding.GetBytes("\r\n")))
         {
        using (System.IO.StreamReader streamReader = new StreamReader(current, this._encoding))
         {
             line = streamReader.ReadToEnd().Trim();
             //Split the input by the column delimiter
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
                 // for column “user”, convert to UPPER case
                 output.Set<string>(count, part.ToUpper());

             }
             else
             {
                 // keep the rest of the columns as-is
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

<span data-ttu-id="fd31d-328">在此使用案例中，擷取器會為「guid」資料行重新產生 GUID，並將「使用者」資料行的值轉換為大寫。</span><span class="sxs-lookup"><span data-stu-id="fd31d-328">In this use-case scenario, the extractor regenerates the GUID for “guid” column and converts the values of “user” column to upper case.</span></span> <span data-ttu-id="fd31d-329">自訂擷取器可藉由剖析輸入資料並用它進行操作，來產生更複雜的結果。</span><span class="sxs-lookup"><span data-stu-id="fd31d-329">Custom extractors can produce more complicated results by parsing input data and manipulating it.</span></span>

<span data-ttu-id="fd31d-330">以下為使用自訂擷取器的基底 U-SQL 指令碼：</span><span class="sxs-lookup"><span data-stu-id="fd31d-330">Following is base U-SQL script that uses a custom extractor:</span></span>

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

OUTPUT @rs0 TO @output_file USING Outputters.Text();
```

## <a name="use-user-defined-outputters"></a><span data-ttu-id="fd31d-331">使用使用者定義輸出器</span><span class="sxs-lookup"><span data-stu-id="fd31d-331">Use user-defined outputters</span></span>
<span data-ttu-id="fd31d-332">使用者定義輸出器是另一個 U-SQL UDO，其可讓您擴充內建的 U-SQL 功能。</span><span class="sxs-lookup"><span data-stu-id="fd31d-332">User-defined outputter is another U-SQL UDO that allows you to extend built-in U-SQL functionality.</span></span> <span data-ttu-id="fd31d-333">和擷取器類似，系統也有數個內建輸出器。</span><span class="sxs-lookup"><span data-stu-id="fd31d-333">Similar to the extractor, there are several built-in outputters.</span></span>

* <span data-ttu-id="fd31d-334">Outputters.Text()︰將資料寫入不同編碼的分隔文字檔。</span><span class="sxs-lookup"><span data-stu-id="fd31d-334">*Outputters.Text()*: Writes data to delimited text files of different encodings.</span></span>
* <span data-ttu-id="fd31d-335">Outputters.Csv()︰將資料寫入不同編碼的逗號分隔值 (CSV) 檔案。</span><span class="sxs-lookup"><span data-stu-id="fd31d-335">*Outputters.Csv()*: Writes data to comma-separated value (CSV) files of different encodings.</span></span>
* <span data-ttu-id="fd31d-336">Outputters.Tsv()︰將資料寫入不同編碼的定位鍵分隔值 (TSV) 檔案。</span><span class="sxs-lookup"><span data-stu-id="fd31d-336">*Outputters.Tsv()*: Writes data to tab-separated value (TSV) files of different encodings.</span></span>

<span data-ttu-id="fd31d-337">自訂輸出器可讓您以自訂的定義格式寫入資料。</span><span class="sxs-lookup"><span data-stu-id="fd31d-337">Custom outputter allows you to write data in a custom defined format.</span></span> <span data-ttu-id="fd31d-338">這可適用於下列工作︰</span><span class="sxs-lookup"><span data-stu-id="fd31d-338">This can be useful for the following tasks:</span></span>

* <span data-ttu-id="fd31d-339">將資料寫入半結構化檔案或非結構化檔案。</span><span class="sxs-lookup"><span data-stu-id="fd31d-339">Writing data to semi-structured or unstructured files.</span></span>
* <span data-ttu-id="fd31d-340">寫入編碼不受支援的資料。</span><span class="sxs-lookup"><span data-stu-id="fd31d-340">Writing data not supported encodings.</span></span>
* <span data-ttu-id="fd31d-341">修改輸出資料或新增自訂屬性。</span><span class="sxs-lookup"><span data-stu-id="fd31d-341">Modifying output data or adding custom attributes.</span></span>

<span data-ttu-id="fd31d-342">若要定義使用者定義輸出器，我們需要建立 `IOutputter` 介面。</span><span class="sxs-lookup"><span data-stu-id="fd31d-342">To define user-defined outputter, we need to create the `IOutputter` interface.</span></span>

<span data-ttu-id="fd31d-343">以下是基底 `IOutputter` 類別實作︰</span><span class="sxs-lookup"><span data-stu-id="fd31d-343">Following is the base `IOutputter` class implementation:</span></span>

```
public abstract class IOutputter : IUserDefinedOperator
{
    protected IOutputter();

    public virtual void Close();
    public abstract void Output(IRow input, IUnstructuredWriter output);
}
```

<span data-ttu-id="fd31d-344">輸出器的所有輸入參數 (例如資料行/資料列分隔符號、編碼等) 都必須在類別的建構函式中加以定義。</span><span class="sxs-lookup"><span data-stu-id="fd31d-344">All input parameters to the outputter, such as column/row delimiters, encoding, and so on, need to be defined in the constructor of the class.</span></span> <span data-ttu-id="fd31d-345">`IOutputter` 介面也應包含 `void Output` 覆寫的定義。</span><span class="sxs-lookup"><span data-stu-id="fd31d-345">The `IOutputter` interface should also contain a definition for `void Output` override.</span></span> <span data-ttu-id="fd31d-346">可選擇性地將屬性 `[SqlUserDefinedOutputter(AtomicFileProcessing = true)` 設定為不可部分完成檔案處理。</span><span class="sxs-lookup"><span data-stu-id="fd31d-346">The attribute `[SqlUserDefinedOutputter(AtomicFileProcessing = true)` can optionally be set for atomic file processing.</span></span> <span data-ttu-id="fd31d-347">如需詳細資訊，請參閱下列詳細資料。</span><span class="sxs-lookup"><span data-stu-id="fd31d-347">For more information, see the following details.</span></span>

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

* <span data-ttu-id="fd31d-348">會針對每個輸入資料列呼叫 `Output`。</span><span class="sxs-lookup"><span data-stu-id="fd31d-348">`Output` is called for each input row.</span></span> <span data-ttu-id="fd31d-349">它會傳回 `IUnstructuredWriter output` 資料列集。</span><span class="sxs-lookup"><span data-stu-id="fd31d-349">It returns the `IUnstructuredWriter output` rowset.</span></span>
* <span data-ttu-id="fd31d-350">建構函式類別可用來將參數傳遞至使用者定義輸出器。</span><span class="sxs-lookup"><span data-stu-id="fd31d-350">The Constructor class is used to pass parameters to the user-defined outputter.</span></span>
* <span data-ttu-id="fd31d-351">`Close` 可選擇性地覆寫，以釋出耗費資源的狀態或判斷最後一個資料列的寫入時間。</span><span class="sxs-lookup"><span data-stu-id="fd31d-351">`Close` is used to optionally override to release expensive state or determine when the last row was written.</span></span>

<span data-ttu-id="fd31d-352">**SqlUserDefinedOutputter** 表示類型應該註冊為使用者定義輸出器。</span><span class="sxs-lookup"><span data-stu-id="fd31d-352">**SqlUserDefinedOutputter** attribute indicates that the type should be registered as a user-defined outputter.</span></span> <span data-ttu-id="fd31d-353">這個類別無法繼承。</span><span class="sxs-lookup"><span data-stu-id="fd31d-353">This class cannot be inherited.</span></span>

<span data-ttu-id="fd31d-354">SqlUserDefinedOutputter 是使用者定義輸出器之定義的選擇性屬性。</span><span class="sxs-lookup"><span data-stu-id="fd31d-354">SqlUserDefinedOutputter is an optional attribute for a user-defined outputter definition.</span></span> <span data-ttu-id="fd31d-355">它可用來定義 AtomicFileProcessing 屬性。</span><span class="sxs-lookup"><span data-stu-id="fd31d-355">It's used to define the AtomicFileProcessing property.</span></span>

* <span data-ttu-id="fd31d-356">bool     AtomicFileProcessing</span><span class="sxs-lookup"><span data-stu-id="fd31d-356">bool     AtomicFileProcessing</span></span>   

* <span data-ttu-id="fd31d-357">**true** = 表示此輸出器需要不可部分完成的輸出檔 (JSON、XML ...)</span><span class="sxs-lookup"><span data-stu-id="fd31d-357">**true** = Indicates that this outputter requires atomic output files (JSON, XML, ...)</span></span>
* <span data-ttu-id="fd31d-358">**false** = 表示此輸出器可以處理分割/分散式檔案 (CSV、SEQ ...)</span><span class="sxs-lookup"><span data-stu-id="fd31d-358">**false** = Indicates that this outputter can deal with split / distributed files (CSV, SEQ, ...)</span></span>

<span data-ttu-id="fd31d-359">主要的可程式性物件為「資料列」和「輸出」。</span><span class="sxs-lookup"><span data-stu-id="fd31d-359">The main programmability objects are **row** and **output**.</span></span> <span data-ttu-id="fd31d-360">**列**物件可用來列舉輸出資料做為 `IRow` 介面。</span><span class="sxs-lookup"><span data-stu-id="fd31d-360">The **row** object is used to enumerate output data as `IRow` interface.</span></span> <span data-ttu-id="fd31d-361">**輸出**用來設定輸出資料至目標檔案。</span><span class="sxs-lookup"><span data-stu-id="fd31d-361">**Output** is used to set output data to the target file.</span></span>

<span data-ttu-id="fd31d-362">輸出資料是透過 `IRow` 介面來存取。</span><span class="sxs-lookup"><span data-stu-id="fd31d-362">The output data is accessed through the `IRow` interface.</span></span> <span data-ttu-id="fd31d-363">一次會對輸出資料傳遞一個資料列。</span><span class="sxs-lookup"><span data-stu-id="fd31d-363">Output data is passed a row at a time.</span></span>

<span data-ttu-id="fd31d-364">藉由呼叫 IRow 介面的 Get 方法可列舉個別的值：</span><span class="sxs-lookup"><span data-stu-id="fd31d-364">The individual values are enumerated by calling the Get method of the IRow interface:</span></span>

```
row.Get<string>("column_name")
```

<span data-ttu-id="fd31d-365">呼叫 `row.Schema` 即可判斷個別資料行名稱：</span><span class="sxs-lookup"><span data-stu-id="fd31d-365">Individual column names can be determined by calling `row.Schema`:</span></span>

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

<span data-ttu-id="fd31d-366">這種方法可讓您為任何中繼資料結構描述建置彈性的輸出器。</span><span class="sxs-lookup"><span data-stu-id="fd31d-366">This approach enables you to build a flexible outputter for any metadata schema.</span></span>

<span data-ttu-id="fd31d-367">會使用 `System.IO.StreamWriter` 將輸出資料寫入檔案。</span><span class="sxs-lookup"><span data-stu-id="fd31d-367">The output data is written to file by using `System.IO.StreamWriter`.</span></span> <span data-ttu-id="fd31d-368">資料流參數會設為 `output.BaseStrea` 做為 `IUnstructuredWriter output` 的一部分。</span><span class="sxs-lookup"><span data-stu-id="fd31d-368">The stream parameter is set to `output.BaseStrea` as part of `IUnstructuredWriter output`.</span></span>

<span data-ttu-id="fd31d-369">請注意，必須在每個資料列反覆項目之後排清檔案的資料緩衝區。</span><span class="sxs-lookup"><span data-stu-id="fd31d-369">Note that it's important to flush the data buffer to the file after each row iteration.</span></span> <span data-ttu-id="fd31d-370">此外，`StreamWriter` 物件必須可用於啟用可處置的屬性 (預設值) 與**使用**關鍵字︰</span><span class="sxs-lookup"><span data-stu-id="fd31d-370">In addition, the `StreamWriter` object must be used with the Disposable attribute enabled (default) and with the **using** keyword:</span></span>

```
using (StreamWriter streamWriter = new StreamWriter(output.BaseStream, this._encoding))
{
…
}
```

<span data-ttu-id="fd31d-371">否則，在每個反覆項目之後明確地呼叫 Flush() 方法。</span><span class="sxs-lookup"><span data-stu-id="fd31d-371">Otherwise, call Flush() method explicitly after each iteration.</span></span> <span data-ttu-id="fd31d-372">我們將此顯示在下列範例中。</span><span class="sxs-lookup"><span data-stu-id="fd31d-372">We show this in the following example.</span></span>

### <a name="set-headers-and-footers-for-user-defined-outputter"></a><span data-ttu-id="fd31d-373">設定使用者定義輸出器的頁首和頁尾</span><span class="sxs-lookup"><span data-stu-id="fd31d-373">Set headers and footers for user-defined outputter</span></span>
<span data-ttu-id="fd31d-374">若要設定頁首，請使用單一的反覆運算執行流程。</span><span class="sxs-lookup"><span data-stu-id="fd31d-374">To set a header, use single iteration execution flow.</span></span>

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

<span data-ttu-id="fd31d-375">第一個 `if (isHeaderRow)` 區塊中的程式碼只會執行一次。</span><span class="sxs-lookup"><span data-stu-id="fd31d-375">The code in the first `if (isHeaderRow)` block is executed only once.</span></span>

<span data-ttu-id="fd31d-376">針對頁尾，使用參考 `System.IO.Stream` 物件的執行個體 (`output.BaseStream`)。</span><span class="sxs-lookup"><span data-stu-id="fd31d-376">For the footer, use the reference to the instance of `System.IO.Stream` object (`output.BaseStream`).</span></span> <span data-ttu-id="fd31d-377">在 `IOutputter` 介面的 Close() 方法中撰寫頁尾。</span><span class="sxs-lookup"><span data-stu-id="fd31d-377">Write the footer in the Close() method of the `IOutputter` interface.</span></span>  <span data-ttu-id="fd31d-378">(如需詳細資訊，請參閱下列範例。)</span><span class="sxs-lookup"><span data-stu-id="fd31d-378">(For more information, see the following example.)</span></span>

<span data-ttu-id="fd31d-379">以下是使用者定義 outputter 的範例︰</span><span class="sxs-lookup"><span data-stu-id="fd31d-379">Following is an example of a user-defined outputter:</span></span>

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

    // The Close method is used to write the footer to the file. It's executed only once, after all rows
    public override void Close().
    {
    //Reference to IO.Stream object - g_writer
    StreamWriter streamWriter = new StreamWriter(g_writer, this.encoding);
    streamWriter.Write("</table>");
    streamWriter.Flush();
    streamWriter.Close();
    }

    public override void Output(IRow row, IUnstructuredWriter output)
    {
    System.IO.StreamWriter streamWriter = new StreamWriter(output.BaseStream, this.encoding);

    // Metadata schema initialization to enumerate column names
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
        // Data type enumeration--required to match the distinct list of types from OUTPUT statement
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
    // Reference to the instance of the IO.Stream object for footer generation
    g_writer = output.BaseStream;
    streamWriter.Flush();
    }
}

// Define the factory classes
public static class Factory
{
    public static HTMLOutputter HTMLOutputter(bool isHeader = false, Encoding encoding = null)
    {
    return new HTMLOutputter(isHeader, encoding);
    }
}
```

<span data-ttu-id="fd31d-380">以及 U-SQL 基底指令碼：</span><span class="sxs-lookup"><span data-stu-id="fd31d-380">And U-SQL base script:</span></span>

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
    TO @output_file 
    USING new USQL_Programmability.HTMLOutputter(isHeader: true);
```

<span data-ttu-id="fd31d-381">這是 HTML 輸出器，會以資料表資料建立 HTML 檔案。</span><span class="sxs-lookup"><span data-stu-id="fd31d-381">This is an HTML outputter, which creates an HTML file with table data.</span></span>

### <a name="call-outputter-from-u-sql-base-script"></a><span data-ttu-id="fd31d-382">從 U-SQL 基底指令碼呼叫輸出器</span><span class="sxs-lookup"><span data-stu-id="fd31d-382">Call outputter from U-SQL base script</span></span>
<span data-ttu-id="fd31d-383">若要從基底 U-SQL 指令碼呼叫自訂輸出器，您必須為輸出器物件建立新的執行個體。</span><span class="sxs-lookup"><span data-stu-id="fd31d-383">To call a custom outputter from the base U-SQL script, the new instance of the outputter object has to be created.</span></span>

```sql
OUTPUT @rs0 TO @output_file USING new USQL_Programmability.HTMLOutputter(isHeader: true);
```

<span data-ttu-id="fd31d-384">若不要在基底指令碼中建立物件執行個體，我們可以建立函式的包裝函式，如先前的範例所示︰</span><span class="sxs-lookup"><span data-stu-id="fd31d-384">To avoid creating an instance of the object in base script, we can create a function wrapper, as shown in our earlier example:</span></span>

```c#
        // Define the factory classes
        public static class Factory
        {
            public static HTMLOutputter HTMLOutputter(bool isHeader = false, Encoding encoding = null)
            {
                return new HTMLOutputter(isHeader, encoding);
            }
        }
```

<span data-ttu-id="fd31d-385">在此案例中，原始呼叫看起來像：</span><span class="sxs-lookup"><span data-stu-id="fd31d-385">In this case, the original call looks like the following:</span></span>

```
OUTPUT @rs0 
TO @output_file 
USING USQL_Programmability.Factory.HTMLOutputter(isHeader: true);
```

## <a name="use-user-defined-processors"></a><span data-ttu-id="fd31d-386">使用使用者定義處理器</span><span class="sxs-lookup"><span data-stu-id="fd31d-386">Use user-defined processors</span></span>
<span data-ttu-id="fd31d-387">使用者定義處理器 (簡稱 UDP) 是一種 U-SQL UDO，可藉由套用可程式性功能處理傳入的資料列。</span><span class="sxs-lookup"><span data-stu-id="fd31d-387">User-defined processor, or UDP, is a type of U-SQL UDO that enables you to process the incoming rows by applying programmability features.</span></span> <span data-ttu-id="fd31d-388">UDP 可讓您視需要結合資料行、修改值，以及新增資料行。</span><span class="sxs-lookup"><span data-stu-id="fd31d-388">UDP enables you to combine columns, modify values, and add new columns if necessary.</span></span> <span data-ttu-id="fd31d-389">基本上，它能夠協助您處理資料列集，以產生所需的資料元素。</span><span class="sxs-lookup"><span data-stu-id="fd31d-389">Basically, it helps to process a rowset to produce required data elements.</span></span>

<span data-ttu-id="fd31d-390">若要定義 UDP，我們必須以 `SqlUserDefinedProcessor` 屬性 (這是 UDP 的選擇性屬性) 建立 `IProcessor`。</span><span class="sxs-lookup"><span data-stu-id="fd31d-390">To define a UDP, we need to create an `IProcessor` interface with the `SqlUserDefinedProcessor` attribute, which is optional for UDP.</span></span>

<span data-ttu-id="fd31d-391">此介面應該包含 `IRow` 介面資料列集覆寫的定義，如下列範例所示︰</span><span class="sxs-lookup"><span data-stu-id="fd31d-391">This interface should contain the definition for the `IRow` interface rowset override, as shown in the following example:</span></span>

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

<span data-ttu-id="fd31d-392">**SqlUserDefinedProcessor** 表示類型應該註冊為使用者定義處理器。</span><span class="sxs-lookup"><span data-stu-id="fd31d-392">**SqlUserDefinedProcessor** indicates that the type should be registered as a user-defined processor.</span></span> <span data-ttu-id="fd31d-393">這個類別無法繼承。</span><span class="sxs-lookup"><span data-stu-id="fd31d-393">This class cannot be inherited.</span></span>

<span data-ttu-id="fd31d-394">SqlUserDefinedProcessor 是 UDP 定義的**選擇性**屬性。</span><span class="sxs-lookup"><span data-stu-id="fd31d-394">The SqlUserDefinedProcessor attribute is **optional** for UDP definition.</span></span>

<span data-ttu-id="fd31d-395">主要的可程式性物件為「輸入」和「輸出」。</span><span class="sxs-lookup"><span data-stu-id="fd31d-395">The main programmability objects are **input** and **output**.</span></span> <span data-ttu-id="fd31d-396">輸入物件可用來列舉輸入資料欄和輸出，以將輸出資料設定為處理器活動的結果。</span><span class="sxs-lookup"><span data-stu-id="fd31d-396">The input object is used to enumerate input columns and output, and to set output data as a result of the processor activity.</span></span>

<span data-ttu-id="fd31d-397">若要列舉輸入資料行，我們可以使用 `input.Get` 方法。</span><span class="sxs-lookup"><span data-stu-id="fd31d-397">For input columns enumeration, we use the `input.Get` method.</span></span>

```
string column_name = input.Get<string>("column_name");
```

<span data-ttu-id="fd31d-398">`input.Get` 方法的參數是傳遞做為 U-SQL 基底指令碼之 `PROCESS` 陳述式內 `PRODUCE` 子句一部分的資料行。</span><span class="sxs-lookup"><span data-stu-id="fd31d-398">The parameter for `input.Get` method is a column that's passed as part of the `PRODUCE` clause of the `PROCESS` statement of the U-SQL base script.</span></span> <span data-ttu-id="fd31d-399">在此，我們必須使用正確的資料類型。</span><span class="sxs-lookup"><span data-stu-id="fd31d-399">We need to use the correct data type here.</span></span>

<span data-ttu-id="fd31d-400">針對輸出，使用 `output.Set` 方法。</span><span class="sxs-lookup"><span data-stu-id="fd31d-400">For output, use the `output.Set` method.</span></span>

<span data-ttu-id="fd31d-401">請務必注意，自訂產生程式只會輸出資料行和使用 `output.Set` 方法呼叫定義的值。</span><span class="sxs-lookup"><span data-stu-id="fd31d-401">It's important to note that custom producer only outputs columns and values that are defined with the `output.Set` method call.</span></span>

```
output.Set<string>("mycolumn", mycolumn);
```

<span data-ttu-id="fd31d-402">呼叫 `return output.AsReadOnly();` 就會觸發實際的處理器輸出。</span><span class="sxs-lookup"><span data-stu-id="fd31d-402">The actual processor output is triggered by calling `return output.AsReadOnly();`.</span></span>

<span data-ttu-id="fd31d-403">以下是處理器範例：</span><span class="sxs-lookup"><span data-stu-id="fd31d-403">Following is a processor example:</span></span>

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

<span data-ttu-id="fd31d-404">在此使用案例中，處理器會結合現存資料行 (在此使用案例中為大寫的「user」和「des」) 來產生稱為「full_description」的新資料行。</span><span class="sxs-lookup"><span data-stu-id="fd31d-404">In this use-case scenario, the processor is generating a new column called “full_description” by combining the existing columns--in this case, “user” in upper case, and “des”.</span></span> <span data-ttu-id="fd31d-405">它也會重新產生 GUID，並傳回原始及新的 GUID 值。</span><span class="sxs-lookup"><span data-stu-id="fd31d-405">It also regenerates a GUID and returns the original and new GUID values.</span></span>

<span data-ttu-id="fd31d-406">如您在上一個範例中所看到，您可以在 `output.Set` 方法呼叫期間呼叫 C# 方法。</span><span class="sxs-lookup"><span data-stu-id="fd31d-406">As you can see from the previous example, you can call C# methods during `output.Set` method call.</span></span>

<span data-ttu-id="fd31d-407">以下是使用自訂處理器的基底 U-SQL 指令碼範例：</span><span class="sxs-lookup"><span data-stu-id="fd31d-407">Following is an example of base U-SQL script that uses a custom processor:</span></span>

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

OUTPUT @rs1 TO @output_file USING Outputters.Text();
```

## <a name="use-user-defined-appliers"></a><span data-ttu-id="fd31d-408">使用使用者定義套用器</span><span class="sxs-lookup"><span data-stu-id="fd31d-408">Use user-defined appliers</span></span>
<span data-ttu-id="fd31d-409">U-SQL 使用者定義套用器可讓您針對查詢的外部資料表運算式所傳回的每個資料列，叫用自訂 C# 函式。</span><span class="sxs-lookup"><span data-stu-id="fd31d-409">A U-SQL user-defined applier enables you to invoke a custom C# function for each row that's returned by the outer table expression of a query.</span></span> <span data-ttu-id="fd31d-410">系統會針對左邊輸入中的每個資料列評估右邊輸入，然後結合所產生的資料列來產生最終輸出。</span><span class="sxs-lookup"><span data-stu-id="fd31d-410">The right input is evaluated for each row from the left input, and the rows that are produced are combined for the final output.</span></span> <span data-ttu-id="fd31d-411">APPLY 運算子所產生的資料行清單是左邊輸入和右邊輸入之資料行集的組合。</span><span class="sxs-lookup"><span data-stu-id="fd31d-411">The list of columns that are produced by the APPLY operator are the combination of the set of columns in the left and the right input.</span></span>

<span data-ttu-id="fd31d-412">U-SQL SELECT 運算式中會叫用使用者定義套用器。</span><span class="sxs-lookup"><span data-stu-id="fd31d-412">User-defined applier is being invoked as part of the USQL SELECT expression.</span></span>

<span data-ttu-id="fd31d-413">使用者定義套用器的典型呼叫看起來如下所示︰</span><span class="sxs-lookup"><span data-stu-id="fd31d-413">The typical call to the user-defined applier looks like the following:</span></span>

```
SELECT …
FROM …
CROSS APPLYis used to pass parameters
new MyScript.MyApplier(param1, param2) AS alias(output_param1 string, …);
```

<span data-ttu-id="fd31d-414">如需在 SELECT 運算式中使用套用器的詳細資訊，請參閱[從 CROSS APPLY 和 OUTER APPLY 選取的 U-SQL SELECT](https://msdn.microsoft.com/library/azure/mt621307.aspx)。</span><span class="sxs-lookup"><span data-stu-id="fd31d-414">For more information about using appliers in a SELECT expression, see [U-SQL SELECT Selecting from CROSS APPLY and OUTER APPLY](https://msdn.microsoft.com/library/azure/mt621307.aspx).</span></span>

<span data-ttu-id="fd31d-415">使用者定義套用器的基底類別定義如下所示：</span><span class="sxs-lookup"><span data-stu-id="fd31d-415">The user-defined applier base class definition is as follows:</span></span>

```
public abstract class IApplier : IUserDefinedOperator
{
protected IApplier();

public abstract IEnumerable<IRow> Apply(IRow input, IUpdatableRow output);
}
```

<span data-ttu-id="fd31d-416">若要定義使用者定義套用器，我們必須以 [`SqlUserDefinedApplier`] 屬性 (這是使用者定義套用器之定義的選擇性屬性) 建立 `IApplier` 介面。</span><span class="sxs-lookup"><span data-stu-id="fd31d-416">To define a user-defined applier, we need to create the `IApplier` interface with the [`SqlUserDefinedApplier`] attribute, which is optional for a user-defined applier definition.</span></span>

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

* <span data-ttu-id="fd31d-417">會針對外部資料表的每個資料列呼叫 Apply。</span><span class="sxs-lookup"><span data-stu-id="fd31d-417">Apply is called for each row of the outer table.</span></span> <span data-ttu-id="fd31d-418">它會傳回 `IUpdatableRow` 輸出資料列集。</span><span class="sxs-lookup"><span data-stu-id="fd31d-418">It returns the `IUpdatableRow` output rowset.</span></span>
* <span data-ttu-id="fd31d-419">建構函式類別可用來將參數傳遞至使用者定義套用器。</span><span class="sxs-lookup"><span data-stu-id="fd31d-419">The Constructor class is used to pass parameters to the user-defined applier.</span></span>

<span data-ttu-id="fd31d-420">**SqlUserDefinedApplier** 表示類型應該註冊為使用者定義套用器。</span><span class="sxs-lookup"><span data-stu-id="fd31d-420">**SqlUserDefinedApplier** indicates that the type should be registered as a user-defined applier.</span></span> <span data-ttu-id="fd31d-421">這個類別無法繼承。</span><span class="sxs-lookup"><span data-stu-id="fd31d-421">This class cannot be inherited.</span></span>

<span data-ttu-id="fd31d-422">**SqlUserDefinedApplier** 是使用者定義套用器定義的**選擇性**。</span><span class="sxs-lookup"><span data-stu-id="fd31d-422">**SqlUserDefinedApplier** is **optional** for a user-defined applier definition.</span></span>


<span data-ttu-id="fd31d-423">主要的可程式性物件如下所示︰</span><span class="sxs-lookup"><span data-stu-id="fd31d-423">The main programmability objects are as follows:</span></span>

```
public override IEnumerable<IRow> Apply(IRow input, IUpdatableRow output)
```

<span data-ttu-id="fd31d-424">輸入資料列集會傳遞做為 `IRow` 輸入。</span><span class="sxs-lookup"><span data-stu-id="fd31d-424">Input rowsets are passed as `IRow` input.</span></span> <span data-ttu-id="fd31d-425">輸出資料列會產生為 `IUpdatableRow` 輸出介面。</span><span class="sxs-lookup"><span data-stu-id="fd31d-425">The output rows are generated as `IUpdatableRow` output interface.</span></span>

<span data-ttu-id="fd31d-426">呼叫 `IRow` 結構描述方法即可判斷個別資料行名稱。</span><span class="sxs-lookup"><span data-stu-id="fd31d-426">Individual column names can be determined by calling the `IRow` Schema method.</span></span>

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

<span data-ttu-id="fd31d-427">若要從傳入的 `IRow` 取得實際資料值，我們可以使用 `IRow` 介面的 Get() 方法。</span><span class="sxs-lookup"><span data-stu-id="fd31d-427">To get the actual data values from the incoming `IRow`, we use the Get() method of `IRow` interface.</span></span>

```
mycolumn = row.Get<int>("mycolumn")
```

<span data-ttu-id="fd31d-428">或者，我們使用結構描述資料行名稱︰</span><span class="sxs-lookup"><span data-stu-id="fd31d-428">Or we use the schema column name:</span></span>

```
row.Get<int>(row.Schema[0].Name)
```

<span data-ttu-id="fd31d-429">輸出值必須使用 `IUpdatableRow` 輸出進行設定：</span><span class="sxs-lookup"><span data-stu-id="fd31d-429">The output values must be set with `IUpdatableRow` output:</span></span>

```
output.Set<int>("mycolumn", mycolumn)
```

<span data-ttu-id="fd31d-430">請務必了解，自訂套用器只會輸出以 `output.Set` 方法呼叫定義的資料行和值。</span><span class="sxs-lookup"><span data-stu-id="fd31d-430">It is important to understand that custom appliers only output columns and values that are defined with `output.Set` method call.</span></span>

<span data-ttu-id="fd31d-431">呼叫 `yield return output.AsReadOnly();` 就會觸發實際的輸出。</span><span class="sxs-lookup"><span data-stu-id="fd31d-431">The actual output is triggered by calling `yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="fd31d-432">使用者定義套用器參數可以傳遞給建構函式。</span><span class="sxs-lookup"><span data-stu-id="fd31d-432">The user-defined applier parameters can be passed to the constructor.</span></span> <span data-ttu-id="fd31d-433">在基底 U-SQL 指令碼的套用器呼叫期間，套用器可傳回數目不定且需要加以定義的資料行。</span><span class="sxs-lookup"><span data-stu-id="fd31d-433">Applier can return a variable number of columns that need to be defined during the applier call in base U-SQL Script.</span></span>

```
new USQL_Programmability.ParserApplier ("all") AS properties(make string, model string, year string, type string, millage int);
```

<span data-ttu-id="fd31d-434">以下是使用者定義套用器的範例︰</span><span class="sxs-lookup"><span data-stu-id="fd31d-434">Here is the user-defined applier example:</span></span>

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

<span data-ttu-id="fd31d-435">以下是此使用者定義套用器的基底 U-SQL 指令碼：</span><span class="sxs-lookup"><span data-stu-id="fd31d-435">Following is the base U-SQL script for this user-defined applier:</span></span>

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

OUTPUT @rs1 TO @output_file USING Outputters.Text();
```

<span data-ttu-id="fd31d-436">在此使用案例中，使用者定義套用器可做為車隊屬性的逗號分隔值剖析器。</span><span class="sxs-lookup"><span data-stu-id="fd31d-436">In this use case scenario, user-defined applier acts as a comma-delimited value parser for the car fleet properties.</span></span> <span data-ttu-id="fd31d-437">輸入檔資料列看起來如下所示︰</span><span class="sxs-lookup"><span data-stu-id="fd31d-437">The input file rows look like the following:</span></span>

```
103 Z1AB2CD123XY45889   Ford,Explorer,2005,SUV,152345
303 Y0AB2CD34XY458890   Shevrolet,Cruise,2010,4Dr,32455
210 X5AB2CD45XY458893   Nissan,Altima,2011,4Dr,74000
```

<span data-ttu-id="fd31d-438">這是典型的定位點分隔符號 TSV 檔案，其屬性資料行內含製造商、型號等汽車屬性。</span><span class="sxs-lookup"><span data-stu-id="fd31d-438">It is a typical tab-delimited TSV file with a properties column that contains car properties such as make and model.</span></span> <span data-ttu-id="fd31d-439">這些屬性必須剖析到資料表資料行。</span><span class="sxs-lookup"><span data-stu-id="fd31d-439">Those properties must be parsed to the table columns.</span></span> <span data-ttu-id="fd31d-440">所提供的套用者也可讓您根據傳遞的參數，在結果資料列集中產生屬性的動態數字。</span><span class="sxs-lookup"><span data-stu-id="fd31d-440">The applier that's provided also enables you to generate a dynamic number of properties in the result rowset, based on the parameter that's passed.</span></span> <span data-ttu-id="fd31d-441">您可以產生所有屬性或僅一組特定的內容。</span><span class="sxs-lookup"><span data-stu-id="fd31d-441">You can generate either all properties or a specific set of properties only.</span></span>

    …USQL_Programmability.ParserApplier ("all")
    …USQL_Programmability.ParserApplier ("make")
    …USQL_Programmability.ParserApplier ("make&model")

<span data-ttu-id="fd31d-442">使用者定義套用器可以呼叫做為套用器物件的新執行個體：</span><span class="sxs-lookup"><span data-stu-id="fd31d-442">The user-defined applier can be called as a new instance of applier object:</span></span>

```
CROSS APPLY new MyNameSpace.MyApplier (parameter: “value”) AS alias([columns types]…);
```

<span data-ttu-id="fd31d-443">或透過叫用包裝函式 Factory 方法來呼叫：</span><span class="sxs-lookup"><span data-stu-id="fd31d-443">Or with the invocation of a wrapper factory method:</span></span>

```c#
    CROSS APPLY MyNameSpace.MyApplier (parameter: “value”) AS alias([columns types]…);
```

## <a name="use-user-defined-combiners"></a><span data-ttu-id="fd31d-444">使用使用者定義結合器</span><span class="sxs-lookup"><span data-stu-id="fd31d-444">Use user-defined combiners</span></span>
<span data-ttu-id="fd31d-445">使用者定義結合器 (簡稱 UDC) 可讓您根據自訂邏輯結合左邊和右邊資料列集中的資料列。</span><span class="sxs-lookup"><span data-stu-id="fd31d-445">User-defined combiner, or UDC, enables you to combine rows from left and right rowsets, based on custom logic.</span></span> <span data-ttu-id="fd31d-446">使用者定義結合器會與 COMBINE 運算式搭配使用。</span><span class="sxs-lookup"><span data-stu-id="fd31d-446">User-defined combiner is used with COMBINE expression.</span></span>

<span data-ttu-id="fd31d-447">結合器會使用 COMBINE 運算式來叫用，以提供關於輸入資料列集、群組資料行、預期的結果結構描述和其他資訊的必要資訊。</span><span class="sxs-lookup"><span data-stu-id="fd31d-447">A combiner is being invoked with the COMBINE expression that provides the necessary information about both the input rowsets, the grouping columns, the expected result schema, and additional information.</span></span>

<span data-ttu-id="fd31d-448">若要在基底 U-SQL 指令碼中呼叫結合器，我們可以使用下列語法：</span><span class="sxs-lookup"><span data-stu-id="fd31d-448">To call a combiner in a base U-SQL script, we use the following syntax:</span></span>

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

<span data-ttu-id="fd31d-449">如需詳細資訊，請參閱 [COMBINE 運算式 (U-SQL)](https://msdn.microsoft.com/library/azure/mt621339.aspx)。</span><span class="sxs-lookup"><span data-stu-id="fd31d-449">For more information, see [COMBINE Expression (U-SQL)](https://msdn.microsoft.com/library/azure/mt621339.aspx).</span></span>

<span data-ttu-id="fd31d-450">若要定義使用者定義結合器，我們必須以 [`SqlUserDefinedCombiner`] 屬性 (這是使用者定義結合器之定義的選擇性屬性) 建立 `ICombiner` 介面。</span><span class="sxs-lookup"><span data-stu-id="fd31d-450">To define a user-defined combiner, we need to create the `ICombiner` interface with the [`SqlUserDefinedCombiner`] attribute, which is optional for a user-defined Combiner definition.</span></span>

<span data-ttu-id="fd31d-451">基底 `ICombiner` 類別定義：</span><span class="sxs-lookup"><span data-stu-id="fd31d-451">Base `ICombiner` class definition:</span></span>

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

<span data-ttu-id="fd31d-452">`ICombiner` 介面的自訂實作應該包含 `IEnumerable<IRow>` 結合覆寫的定義。</span><span class="sxs-lookup"><span data-stu-id="fd31d-452">The custom implementation of an `ICombiner` interface should contain the definition for an `IEnumerable<IRow>` Combine override.</span></span>

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

<span data-ttu-id="fd31d-453">**SqlUserDefinedCombiner** 表示類型應該註冊為使用者定義結合器。</span><span class="sxs-lookup"><span data-stu-id="fd31d-453">The **SqlUserDefinedCombiner** attribute indicates that the type should be registered as a user-defined combiner.</span></span> <span data-ttu-id="fd31d-454">這個類別無法繼承。</span><span class="sxs-lookup"><span data-stu-id="fd31d-454">This class cannot be inherited.</span></span>

<span data-ttu-id="fd31d-455">**SqlUserDefinedCombiner** 用來定義合併程式模式屬性。</span><span class="sxs-lookup"><span data-stu-id="fd31d-455">**SqlUserDefinedCombiner** is used to define the Combiner mode property.</span></span> <span data-ttu-id="fd31d-456">它是使用者定義結合器定義的選擇性屬性。</span><span class="sxs-lookup"><span data-stu-id="fd31d-456">It is an optional attribute for a user-defined combiner definition.</span></span>

<span data-ttu-id="fd31d-457">CombinerMode     Mode</span><span class="sxs-lookup"><span data-stu-id="fd31d-457">CombinerMode     Mode</span></span>

<span data-ttu-id="fd31d-458">CombinerMode 列舉可以採用下列值︰</span><span class="sxs-lookup"><span data-stu-id="fd31d-458">CombinerMode enum can take the following values:</span></span>

* <span data-ttu-id="fd31d-459">完整 (0) 每個輸出資料列可能相依於所有具有相同金鑰值的左邊和右邊輸入資料列。</span><span class="sxs-lookup"><span data-stu-id="fd31d-459">Full  (0) Every output row potentially depends on all the input rows from left and right       with the same key value.</span></span>

* <span data-ttu-id="fd31d-460">左邊 (1) 每個輸出資料列相依於左邊的單一輸入資料列 (並可能相依於所有具有相同金鑰值的右邊資料列)。</span><span class="sxs-lookup"><span data-stu-id="fd31d-460">Left  (1) Every output row depends on a single input row from the left (and potentially all rows       from the right with the same key value).</span></span>

* <span data-ttu-id="fd31d-461">右邊 (2) 每個輸出資料列相依於右邊的單一輸入資料列 (並可能相依於所有具有相同金鑰值的左邊資料列)。</span><span class="sxs-lookup"><span data-stu-id="fd31d-461">Right (2)     Every output row depends on a single input row from the right (and potentially all rows       from the left with the same key value).</span></span>

* <span data-ttu-id="fd31d-462">內部 (3) 每個輸出資料列相依於具有相同值的左邊和右邊單一輸入資料列。</span><span class="sxs-lookup"><span data-stu-id="fd31d-462">Inner (3) Every output row depends on a single input row from left and right with the same value.</span></span>

<span data-ttu-id="fd31d-463">範例：[`SqlUserDefinedCombiner(Mode=CombinerMode.Left)`]</span><span class="sxs-lookup"><span data-stu-id="fd31d-463">Example:    [`SqlUserDefinedCombiner(Mode=CombinerMode.Left)`]</span></span>


<span data-ttu-id="fd31d-464">主要的可程式性物件為：</span><span class="sxs-lookup"><span data-stu-id="fd31d-464">The main programmability objects are:</span></span>

```c#
    public override IEnumerable<IRow> Combine(IRowset left, IRowset right,
        IUpdatableRow output
```

<span data-ttu-id="fd31d-465">輸入資料列集會傳遞做為介面的「左邊」和「右邊」 `IRowset` 類型。</span><span class="sxs-lookup"><span data-stu-id="fd31d-465">Input rowsets are passed as **left** and **right** `IRowset` type of interface.</span></span> <span data-ttu-id="fd31d-466">這兩個資料列集必須列舉以進行處理。</span><span class="sxs-lookup"><span data-stu-id="fd31d-466">Both rowsets must be enumerated for processing.</span></span> <span data-ttu-id="fd31d-467">您僅可以允許每個介面列舉一次，因此我們必須在必要時加以列舉和快取。</span><span class="sxs-lookup"><span data-stu-id="fd31d-467">You can only enumerate each interface once, so we have to enumerate and cache it if necessary.</span></span>

<span data-ttu-id="fd31d-468">若要快取，我們可以透過執行 LINQ 查詢來建立記憶體結構的 List\<T\> 類型，特別是 List<`IRow`>。</span><span class="sxs-lookup"><span data-stu-id="fd31d-468">For caching purposes, we can create a List\<T\> type of memory structure as a result of a LINQ query execution, specifically List<`IRow`>.</span></span> <span data-ttu-id="fd31d-469">列舉期間也可以使用匿名資料類型。</span><span class="sxs-lookup"><span data-stu-id="fd31d-469">The anonymous data type can be used during enumeration as well.</span></span>

<span data-ttu-id="fd31d-470">如需 LINQ 查詢的詳細資訊，請參閱 [LINQ 查詢 (C#) 簡介](https://msdn.microsoft.com/library/bb397906.aspx)，如需 IEnumerable\<T\> 介面的詳細資訊，請參閱 [IEnumerable\<T\> 介面](https://msdn.microsoft.com/library/9eekhta0(v=vs.110).aspx)。</span><span class="sxs-lookup"><span data-stu-id="fd31d-470">See [Introduction to LINQ Queries (C#)](https://msdn.microsoft.com/library/bb397906.aspx) for more information about LINQ queries, and [IEnumerable\<T\> Interface](https://msdn.microsoft.com/library/9eekhta0(v=vs.110).aspx) for more information about IEnumerable\<T\> interface.</span></span>

<span data-ttu-id="fd31d-471">若要從傳入的 `IRowset` 取得實際資料值，我們可以使用 `IRow` 介面的 Get() 方法。</span><span class="sxs-lookup"><span data-stu-id="fd31d-471">To get the actual data values from the incoming `IRowset`, we use the Get() method of `IRow` interface.</span></span>

```
mycolumn = row.Get<int>("mycolumn")
```

<span data-ttu-id="fd31d-472">呼叫 `IRow` 結構描述方法即可判斷個別資料行名稱。</span><span class="sxs-lookup"><span data-stu-id="fd31d-472">Individual column names can be determined by calling the `IRow` Schema method.</span></span>

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

<span data-ttu-id="fd31d-473">或者，使用結構描述資料行名稱︰</span><span class="sxs-lookup"><span data-stu-id="fd31d-473">Or by using the schema column name:</span></span>

```
c# row.Get<int>(row.Schema[0].Name)
```

<span data-ttu-id="fd31d-474">LINQ 的一般列舉看起來如下所示︰</span><span class="sxs-lookup"><span data-stu-id="fd31d-474">The general enumeration with LINQ looks like the following:</span></span>

```
var myRowset =
            (from row in left.Rows
                          select new
                          {
                              Mycolumn = row.Get<int>("mycolumn"),
                          }).ToList();
```

<span data-ttu-id="fd31d-475">列舉這兩個資料列集之後，我們將所有資料列執行迴圈。</span><span class="sxs-lookup"><span data-stu-id="fd31d-475">After enumerating both rowsets, we are going to loop through all rows.</span></span> <span data-ttu-id="fd31d-476">針對資料列集左邊的每個資料列，我們要尋找符合我們合併程式條件的所有資料列。</span><span class="sxs-lookup"><span data-stu-id="fd31d-476">For each row in the left rowset, we are going to find all rows that satisfy the condition of our combiner.</span></span>

<span data-ttu-id="fd31d-477">輸出值必須使用 `IUpdatableRow` 輸出進行設定。</span><span class="sxs-lookup"><span data-stu-id="fd31d-477">The output values must be set with `IUpdatableRow` output.</span></span>

```
output.Set<int>("mycolumn", mycolumn)
```

<span data-ttu-id="fd31d-478">呼叫 `yield return output.AsReadOnly();` 就會觸發實際的輸出。</span><span class="sxs-lookup"><span data-stu-id="fd31d-478">The actual output is triggered by calling to `yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="fd31d-479">以下是結合器範例：</span><span class="sxs-lookup"><span data-stu-id="fd31d-479">Following is a combiner example:</span></span>

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

<span data-ttu-id="fd31d-480">在此使用案例中，我們會建置零售商的分析報告。</span><span class="sxs-lookup"><span data-stu-id="fd31d-480">In this use-case scenario, we are building an analytics report for the retailer.</span></span> <span data-ttu-id="fd31d-481">目標是要尋找成本超過 20,000 美元，且特定時間範圍內透過網站的銷售速度快過一般零售商的所有產品。</span><span class="sxs-lookup"><span data-stu-id="fd31d-481">The goal is to find all products that cost more than $20,000 and that sell through the website faster than through the regular retailer within a certain time frame.</span></span>

<span data-ttu-id="fd31d-482">以下是基底 U-SQL 指令碼。</span><span class="sxs-lookup"><span data-stu-id="fd31d-482">Here is the base U-SQL script.</span></span> <span data-ttu-id="fd31d-483">您可以比較一般 JOIN 與結合器之間的邏輯︰</span><span class="sxs-lookup"><span data-stu-id="fd31d-483">You can compare the logic between a regular JOIN and a combiner:</span></span>

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

OUTPUT @rs1 TO @output_file1 USING Outputters.Tsv();
OUTPUT @rs2 TO @output_file2 USING Outputters.Tsv();
```

<span data-ttu-id="fd31d-484">使用者定義結合器可以呼叫做為套用器物件的新執行個體︰</span><span class="sxs-lookup"><span data-stu-id="fd31d-484">A user-defined combiner can be called as a new instance of the applier object:</span></span>

```
USING new MyNameSpace.MyCombiner();
```


<span data-ttu-id="fd31d-485">或透過叫用包裝函式 Factory 方法來呼叫：</span><span class="sxs-lookup"><span data-stu-id="fd31d-485">Or with the invocation of a wrapper factory method:</span></span>

```
USING MyNameSpace.MyCombiner();
```

## <a name="use-user-defined-reducers"></a><span data-ttu-id="fd31d-486">使用使用者定義歸納器</span><span class="sxs-lookup"><span data-stu-id="fd31d-486">Use user-defined reducers</span></span>

<span data-ttu-id="fd31d-487">U-SQL 可讓您藉由實作 IReducer 介面，在 C# 中使用使用者定義運算子擴充性架構撰寫自訂的資料列集歸納器。</span><span class="sxs-lookup"><span data-stu-id="fd31d-487">U-SQL enables you to write custom rowset reducers in C# by using the user-defined operator extensibility framework and implementing an IReducer interface.</span></span>

<span data-ttu-id="fd31d-488">使用者定義歸納器 (簡稱 UDR) 可用來在資料擷取 (匯入) 期間消除不必要的資料列。</span><span class="sxs-lookup"><span data-stu-id="fd31d-488">User-defined reducer, or UDR, can be used to eliminate unnecessary rows during data extraction (import).</span></span> <span data-ttu-id="fd31d-489">也可以用來操作和評估資料列和資料行。</span><span class="sxs-lookup"><span data-stu-id="fd31d-489">It also can be used to manipulate and evaluate rows and columns.</span></span> <span data-ttu-id="fd31d-490">根據程式設計邏輯，它也可以定義需要擷取哪些資料列。</span><span class="sxs-lookup"><span data-stu-id="fd31d-490">Based on programmability logic, it can also define which rows need to be extracted.</span></span>

<span data-ttu-id="fd31d-491">若要定義 UDR 類別，我們需要使用選擇性的 `SqlUserDefinedReducer` 屬性建立 `IReducer` 介面。</span><span class="sxs-lookup"><span data-stu-id="fd31d-491">To define a UDR class, we need to create an `IReducer` interface with an optional `SqlUserDefinedReducer` attribute.</span></span>

<span data-ttu-id="fd31d-492">此類別介面應該包含 `IEnumerable` 介面資料列集覆寫的定義。</span><span class="sxs-lookup"><span data-stu-id="fd31d-492">This class interface should contain a definition for the `IEnumerable` interface rowset override.</span></span>

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

<span data-ttu-id="fd31d-493">**SqlUserDefinedReducer** 表示類型應該註冊為使用者定義歸納器。</span><span class="sxs-lookup"><span data-stu-id="fd31d-493">The **SqlUserDefinedReducer** attribute indicates that the type should be registered as a user-defined reducer.</span></span> <span data-ttu-id="fd31d-494">這個類別無法繼承。</span><span class="sxs-lookup"><span data-stu-id="fd31d-494">This class cannot be inherited.</span></span>
<span data-ttu-id="fd31d-495">**SqlUserDefinedReducer** 是使用者定義歸納器之定義的選擇性屬性。</span><span class="sxs-lookup"><span data-stu-id="fd31d-495">**SqlUserDefinedReducer** is an optional attribute for a user-defined reducer definition.</span></span> <span data-ttu-id="fd31d-496">它可用來定義 IsRecursive 屬性。</span><span class="sxs-lookup"><span data-stu-id="fd31d-496">It's used to define IsRecursive property.</span></span>

* <span data-ttu-id="fd31d-497">bool     IsRecursive</span><span class="sxs-lookup"><span data-stu-id="fd31d-497">bool     IsRecursive</span></span>    
* <span data-ttu-id="fd31d-498">**true** = 表示此歸納器是否等冪</span><span class="sxs-lookup"><span data-stu-id="fd31d-498">**true**  = Indicates whether this Reducer is idempotent</span></span>

<span data-ttu-id="fd31d-499">主要的可程式性物件為「輸入」和「輸出」。</span><span class="sxs-lookup"><span data-stu-id="fd31d-499">The main programmability objects are **input** and **output**.</span></span> <span data-ttu-id="fd31d-500">輸入物件用來列舉輸入資料列。</span><span class="sxs-lookup"><span data-stu-id="fd31d-500">The input object is used to enumerate input rows.</span></span> <span data-ttu-id="fd31d-501">輸出用來設定減少活動結果的輸出資料列。</span><span class="sxs-lookup"><span data-stu-id="fd31d-501">Output is used to set output rows as a result of reducing activity.</span></span>

<span data-ttu-id="fd31d-502">若要列舉輸入資料列，我們可以使用 `Row.Get` 方法。</span><span class="sxs-lookup"><span data-stu-id="fd31d-502">For input rows enumeration, we use the `Row.Get` method.</span></span>

```
foreach (IRow row in input.Rows)
{
    row.Get<string>("mycolumn");
}
```

<span data-ttu-id="fd31d-503">`Row.Get` 方法的參數是傳遞做為 U-SQL 基底指令碼之 `REDUCE` 陳述式內 `PRODUCE` 類別一部分的資料行。</span><span class="sxs-lookup"><span data-stu-id="fd31d-503">The parameter for the `Row.Get` method is a column that's passed as part of the `PRODUCE` class of the `REDUCE` statement of the U-SQL base script.</span></span> <span data-ttu-id="fd31d-504">在此，我們也必須使用正確的資料類型。</span><span class="sxs-lookup"><span data-stu-id="fd31d-504">We need to use the correct data type here as well.</span></span>

<span data-ttu-id="fd31d-505">針對輸出，使用 `output.Set` 方法。</span><span class="sxs-lookup"><span data-stu-id="fd31d-505">For output, use the `output.Set` method.</span></span>

<span data-ttu-id="fd31d-506">請務必了解，自訂歸納器只會輸出以 `output.Set` 方法呼叫定義的值。</span><span class="sxs-lookup"><span data-stu-id="fd31d-506">It is important to understand that custom reducer only outputs values that are defined with the `output.Set` method call.</span></span>

```
output.Set<string>("mycolumn", guid);
```

<span data-ttu-id="fd31d-507">呼叫 `yield return output.AsReadOnly();` 就會觸發實際的歸納器輸出。</span><span class="sxs-lookup"><span data-stu-id="fd31d-507">The actual reducer output is triggered by calling `yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="fd31d-508">以下是歸納器範例：</span><span class="sxs-lookup"><span data-stu-id="fd31d-508">Following is a reducer example:</span></span>

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

<span data-ttu-id="fd31d-509">在此使用案例中，歸納器會略過使用者名稱空白的資料列。</span><span class="sxs-lookup"><span data-stu-id="fd31d-509">In this use-case scenario, the reducer is skipping rows with an empty user name.</span></span> <span data-ttu-id="fd31d-510">針對資料列集中的每個資料列，它會讀取每個必要的資料行，然後評估使用者名稱的長度。</span><span class="sxs-lookup"><span data-stu-id="fd31d-510">For each row in rowset, it reads each required column, then evaluates the length of the user name.</span></span> <span data-ttu-id="fd31d-511">只有當使用者名稱值的長度大於 0 時，它才會輸出實際的資料列。</span><span class="sxs-lookup"><span data-stu-id="fd31d-511">It outputs the actual row only if user name value length is more than 0.</span></span>

<span data-ttu-id="fd31d-512">以下為使用自訂歸納器的基底 U-SQL 指令碼：</span><span class="sxs-lookup"><span data-stu-id="fd31d-512">Following is base U-SQL script that uses a custom reducer:</span></span>

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
    TO @output_file 
    USING Outputters.Text();
```
