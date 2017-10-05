---
title: "在 Azure Data Lake Analytics 中擴充 U-SQL 指令碼與 Python | Microsoft Docs"
description: "了解如何在 U-SQL 指令碼中執行 Python 程式碼"
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: jhubbard
editor: cgronlun
ms.assetid: c1c74e5e-3e4a-41ab-9e3f-e9085da1d315
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/20/2017
ms.author: saveenr
ms.openlocfilehash: d18ef1f747aee2fa01cef9891432d0461031ee4c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-get-started-with-extending-u-sql-with-python"></a><span data-ttu-id="5e250-103">教學課程︰開始擴充 U-SQL 與 Python</span><span class="sxs-lookup"><span data-stu-id="5e250-103">Tutorial: Get started with extending U-SQL with Python</span></span>

<span data-ttu-id="5e250-104">U-SQL 的 Python 擴充可讓開發人員進行大量的 Python 程式碼平行執行。</span><span class="sxs-lookup"><span data-stu-id="5e250-104">Python Extensions for U-SQL enable developers to perform massively parallel execution of Python code.</span></span> <span data-ttu-id="5e250-105">以下範例說明基本概念：</span><span class="sxs-lookup"><span data-stu-id="5e250-105">The following example illustrates the basic steps:</span></span>

* <span data-ttu-id="5e250-106">使用 `REFERENCE ASSEMBLY` 陳述式啟用 U-SQL 指令碼的 Python 延伸模組</span><span class="sxs-lookup"><span data-stu-id="5e250-106">Use the `REFERENCE ASSEMBLY` statement to enable Python extensions for the U-SQL Script</span></span>
* <span data-ttu-id="5e250-107">使用 `REDUCE` 作業分割索引鍵上的輸入資料</span><span class="sxs-lookup"><span data-stu-id="5e250-107">Using the `REDUCE` operation to partition the input data on a key</span></span>
* <span data-ttu-id="5e250-108">U-SQL 的 Python 延伸模組有內建的歸納器 (`Extension.Python.Reducer`)，可執行指派給歸納器之每一個頂點上的 Python 程式碼</span><span class="sxs-lookup"><span data-stu-id="5e250-108">The Python extensions for U-SQL include a built-in reducer (`Extension.Python.Reducer`) that runs Python code on each vertex assigned to the reducer</span></span>
* <span data-ttu-id="5e250-109">U-SQL 指令碼包含內嵌的 Python 程式碼，其中的 `usqlml_main` 函式會接受 pandas 資料框架作為輸入，並傳回 pandas 資料框架作為輸出。</span><span class="sxs-lookup"><span data-stu-id="5e250-109">The U-SQL script contains the embedded Python code that has a function called `usqlml_main` that accepts a pandas DataFrame as input and returns a pandas DataFrame as output.</span></span>

--

    REFERENCE ASSEMBLY [ExtPython];

    DECLARE @myScript = @"
    def get_mentions(tweet):
        return ';'.join( ( w[1:] for w in tweet.split() if w[0]=='@' ) )

    def usqlml_main(df):
        del df['time']
        del df['author']
        df['mentions'] = df.tweet.apply(get_mentions)
        del df['tweet']
        return df
    ";

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
        USING new Extension.Python.Reducer(pyScript:@myScript);

    OUTPUT @m
        TO "/tweetmentions.csv"
        USING Outputters.Csv();

## <a name="how-python-integrates-with-u-sql"></a><span data-ttu-id="5e250-110">Python 如何與 U-SQL 整合</span><span class="sxs-lookup"><span data-stu-id="5e250-110">How Python Integrates with U-SQL</span></span>

### <a name="datatypes"></a><span data-ttu-id="5e250-111">資料類型</span><span class="sxs-lookup"><span data-stu-id="5e250-111">Datatypes</span></span>

* <span data-ttu-id="5e250-112">U-SQL 的字串和數值資料行在 Pandas 和 U-SQL 之間會如現狀轉換</span><span class="sxs-lookup"><span data-stu-id="5e250-112">String and numeric columns from U-SQL are converted as-is between Pandas and U-SQL</span></span>
* <span data-ttu-id="5e250-113">U-SQL 的 Null 與 Pandas 的 `NA` 值會互相轉換</span><span class="sxs-lookup"><span data-stu-id="5e250-113">U-SQL Nulls are converted to and from Pandas `NA` values</span></span>

### <a name="schemas"></a><span data-ttu-id="5e250-114">結構描述</span><span class="sxs-lookup"><span data-stu-id="5e250-114">Schemas</span></span>

* <span data-ttu-id="5e250-115">U-SQL 不支援 Pandas 的索引向量。</span><span class="sxs-lookup"><span data-stu-id="5e250-115">Index vectors in Pandas are not supported in U-SQL.</span></span> <span data-ttu-id="5e250-116">Python 函式中所有的輸入資料框架一律具有 64 位元的數值索引，範圍從 0 到資料列數目減 1。</span><span class="sxs-lookup"><span data-stu-id="5e250-116">All input data frames in the Python function always have a 64-bit numerical index from 0 through the number of rows minus 1.</span></span> 
* <span data-ttu-id="5e250-117">U-SQL 資料集不能有重複的資料行名稱。</span><span class="sxs-lookup"><span data-stu-id="5e250-117">U-SQL datasets cannot have duplicate column names</span></span>
* <span data-ttu-id="5e250-118">U-SQL 資料集的資料行名稱不是字串。</span><span class="sxs-lookup"><span data-stu-id="5e250-118">U-SQL datasets column names that are not strings.</span></span> 

### <a name="python-versions"></a><span data-ttu-id="5e250-119">Python 版本</span><span class="sxs-lookup"><span data-stu-id="5e250-119">Python Versions</span></span>
<span data-ttu-id="5e250-120">僅支援 Python 3.5.1 (針對 Windows 編譯)。</span><span class="sxs-lookup"><span data-stu-id="5e250-120">Only Python 3.5.1 (compiled for Windows) is supported.</span></span> 

### <a name="standard-python-modules"></a><span data-ttu-id="5e250-121">標準 Python 模組</span><span class="sxs-lookup"><span data-stu-id="5e250-121">Standard Python modules</span></span>
<span data-ttu-id="5e250-122">包含所有的標準 Python 模組。</span><span class="sxs-lookup"><span data-stu-id="5e250-122">All the standard Python modules are included.</span></span>

### <a name="additional-python-modules"></a><span data-ttu-id="5e250-123">其他 Python 模組</span><span class="sxs-lookup"><span data-stu-id="5e250-123">Additional Python modules</span></span>
<span data-ttu-id="5e250-124">除了標準 Python 程式庫，還包含數個常用的 Python 程式庫︰</span><span class="sxs-lookup"><span data-stu-id="5e250-124">Besides the standard Python libraries, several commonly used python libraries are included:</span></span>

    pandas
    numpy
    numexpr

### <a name="exception-messages"></a><span data-ttu-id="5e250-125">例外狀況訊息</span><span class="sxs-lookup"><span data-stu-id="5e250-125">Exception Messages</span></span>
<span data-ttu-id="5e250-126">目前，Python 程式碼中的例外狀況是顯示為泛型頂點失敗。</span><span class="sxs-lookup"><span data-stu-id="5e250-126">Currently, an exception in Python code shows up as generic vertex failure.</span></span> <span data-ttu-id="5e250-127">在未來，U-SQL 作業的錯誤訊息將會顯示 Python 例外狀況訊息。</span><span class="sxs-lookup"><span data-stu-id="5e250-127">In the future, the U-SQL Job error messages will display the Python exception message.</span></span>

### <a name="input-and-output-size-limitations"></a><span data-ttu-id="5e250-128">輸入和輸出的大小限制</span><span class="sxs-lookup"><span data-stu-id="5e250-128">Input and Output size limitations</span></span>
<span data-ttu-id="5e250-129">指派給每個頂點的記憶體數量皆有上限。</span><span class="sxs-lookup"><span data-stu-id="5e250-129">Every vertex has a limited amount of memory assigned to it.</span></span> <span data-ttu-id="5e250-130">目前，該限制為 6 GB 用於 AU。</span><span class="sxs-lookup"><span data-stu-id="5e250-130">Currently, that limit is 6 GB for an AU.</span></span> <span data-ttu-id="5e250-131">因為輸入和輸出資料框架必須存在於Python 程式碼的記憶體中，輸入和輸出的大小總和不能超過 6 GB。</span><span class="sxs-lookup"><span data-stu-id="5e250-131">Because the input and output DataFrames must exist in memory in the Python code, the total size for the input and output cannot exceed 6 GB.</span></span>

## <a name="see-also"></a><span data-ttu-id="5e250-132">另請參閱</span><span class="sxs-lookup"><span data-stu-id="5e250-132">See also</span></span>
* [<span data-ttu-id="5e250-133">Microsoft Azure Data Lake Analytics 概觀</span><span class="sxs-lookup"><span data-stu-id="5e250-133">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="5e250-134">使用 Data Lake Tools for Visual Studio 開發 U-SQL 指令碼</span><span class="sxs-lookup"><span data-stu-id="5e250-134">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="5e250-135">針對 Azure 資料湖分析工作使用 U-SQL 視窗函式</span><span class="sxs-lookup"><span data-stu-id="5e250-135">Using U-SQL window functions for Azure Data Lake Analytics jobs</span></span>](data-lake-analytics-use-window-functions.md)

