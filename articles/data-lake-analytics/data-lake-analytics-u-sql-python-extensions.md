---
title: "aaaExtend U-SQL 指令碼使用在 Azure Data Lake Analytics Python |Microsoft 文件"
description: "了解 toorun Python U-SQL 指令碼中的程式碼"
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
ms.openlocfilehash: f051f56f67522d4f2b8e6e54fd21a5c95ce3ba92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-get-started-with-extending-u-sql-with-python"></a><span data-ttu-id="8da6c-103">教學課程︰開始擴充 U-SQL 與 Python</span><span class="sxs-lookup"><span data-stu-id="8da6c-103">Tutorial: Get started with extending U-SQL with Python</span></span>

<span data-ttu-id="8da6c-104">U sql Python 延伸可讓開發人員 tooperform 大量平行執行 Python 程式碼。</span><span class="sxs-lookup"><span data-stu-id="8da6c-104">Python Extensions for U-SQL enable developers tooperform massively parallel execution of Python code.</span></span> <span data-ttu-id="8da6c-105">hello 下列範例將說明 hello 基本步驟：</span><span class="sxs-lookup"><span data-stu-id="8da6c-105">hello following example illustrates hello basic steps:</span></span>

* <span data-ttu-id="8da6c-106">使用 hello `REFERENCE ASSEMBLY` hello U-SQL 指令碼的陳述式 tooenable Python 擴充功能</span><span class="sxs-lookup"><span data-stu-id="8da6c-106">Use hello `REFERENCE ASSEMBLY` statement tooenable Python extensions for hello U-SQL Script</span></span>
* <span data-ttu-id="8da6c-107">使用 hello`REDUCE`作業 toopartition hello 輸入在索引鍵的資料</span><span class="sxs-lookup"><span data-stu-id="8da6c-107">Using hello `REDUCE` operation toopartition hello input data on a key</span></span>
* <span data-ttu-id="8da6c-108">hello U-SQL 的 Python 擴充功能包含內建減壓器 (`Extension.Python.Reducer`) 每個頂點指派 toohello 減壓器上執行的 Python 程式碼</span><span class="sxs-lookup"><span data-stu-id="8da6c-108">hello Python extensions for U-SQL include a built-in reducer (`Extension.Python.Reducer`) that runs Python code on each vertex assigned toohello reducer</span></span>
* <span data-ttu-id="8da6c-109">hello U-SQL 指令碼包含內嵌的 hello Python 程式碼具有函式，呼叫`usqlml_main`，接受熊做為輸入的資料框架，並傳回熊做為輸出資料框架。</span><span class="sxs-lookup"><span data-stu-id="8da6c-109">hello U-SQL script contains hello embedded Python code that has a function called `usqlml_main` that accepts a pandas DataFrame as input and returns a pandas DataFrame as output.</span></span>

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
        too"/tweetmentions.csv"
        USING Outputters.Csv();

## <a name="how-python-integrates-with-u-sql"></a><span data-ttu-id="8da6c-110">Python 如何與 U-SQL 整合</span><span class="sxs-lookup"><span data-stu-id="8da6c-110">How Python Integrates with U-SQL</span></span>

### <a name="datatypes"></a><span data-ttu-id="8da6c-111">資料類型</span><span class="sxs-lookup"><span data-stu-id="8da6c-111">Datatypes</span></span>

* <span data-ttu-id="8da6c-112">U-SQL 的字串和數值資料行在 Pandas 和 U-SQL 之間會如現狀轉換</span><span class="sxs-lookup"><span data-stu-id="8da6c-112">String and numeric columns from U-SQL are converted as-is between Pandas and U-SQL</span></span>
* <span data-ttu-id="8da6c-113">U SQL Null 會轉換從熊 tooand`NA`值</span><span class="sxs-lookup"><span data-stu-id="8da6c-113">U-SQL Nulls are converted tooand from Pandas `NA` values</span></span>

### <a name="schemas"></a><span data-ttu-id="8da6c-114">結構描述</span><span class="sxs-lookup"><span data-stu-id="8da6c-114">Schemas</span></span>

* <span data-ttu-id="8da6c-115">U-SQL 不支援 Pandas 的索引向量。</span><span class="sxs-lookup"><span data-stu-id="8da6c-115">Index vectors in Pandas are not supported in U-SQL.</span></span> <span data-ttu-id="8da6c-116">Hello Python 函式中的所有輸入的資料框架一定 64 位元數字的索引，從 0 到 hello 資料列數目減 1。</span><span class="sxs-lookup"><span data-stu-id="8da6c-116">All input data frames in hello Python function always have a 64-bit numerical index from 0 through hello number of rows minus 1.</span></span> 
* <span data-ttu-id="8da6c-117">U-SQL 資料集不能有重複的資料行名稱。</span><span class="sxs-lookup"><span data-stu-id="8da6c-117">U-SQL datasets cannot have duplicate column names</span></span>
* <span data-ttu-id="8da6c-118">U-SQL 資料集的資料行名稱不是字串。</span><span class="sxs-lookup"><span data-stu-id="8da6c-118">U-SQL datasets column names that are not strings.</span></span> 

### <a name="python-versions"></a><span data-ttu-id="8da6c-119">Python 版本</span><span class="sxs-lookup"><span data-stu-id="8da6c-119">Python Versions</span></span>
<span data-ttu-id="8da6c-120">僅支援 Python 3.5.1 (針對 Windows 編譯)。</span><span class="sxs-lookup"><span data-stu-id="8da6c-120">Only Python 3.5.1 (compiled for Windows) is supported.</span></span> 

### <a name="standard-python-modules"></a><span data-ttu-id="8da6c-121">標準 Python 模組</span><span class="sxs-lookup"><span data-stu-id="8da6c-121">Standard Python modules</span></span>
<span data-ttu-id="8da6c-122">包含的所有 hello 標準 Python 模組。</span><span class="sxs-lookup"><span data-stu-id="8da6c-122">All hello standard Python modules are included.</span></span>

### <a name="additional-python-modules"></a><span data-ttu-id="8da6c-123">其他 Python 模組</span><span class="sxs-lookup"><span data-stu-id="8da6c-123">Additional Python modules</span></span>
<span data-ttu-id="8da6c-124">除了 hello 標準的 Python 程式庫，幾個常用的 python 程式庫會包含：</span><span class="sxs-lookup"><span data-stu-id="8da6c-124">Besides hello standard Python libraries, several commonly used python libraries are included:</span></span>

    pandas
    numpy
    numexpr

### <a name="exception-messages"></a><span data-ttu-id="8da6c-125">例外狀況訊息</span><span class="sxs-lookup"><span data-stu-id="8da6c-125">Exception Messages</span></span>
<span data-ttu-id="8da6c-126">目前，Python 程式碼中的例外狀況是顯示為泛型頂點失敗。</span><span class="sxs-lookup"><span data-stu-id="8da6c-126">Currently, an exception in Python code shows up as generic vertex failure.</span></span> <span data-ttu-id="8da6c-127">在未來的 hello，hello U-SQL 作業錯誤訊息會顯示 hello Python 例外狀況訊息。</span><span class="sxs-lookup"><span data-stu-id="8da6c-127">In hello future, hello U-SQL Job error messages will display hello Python exception message.</span></span>

### <a name="input-and-output-size-limitations"></a><span data-ttu-id="8da6c-128">輸入和輸出的大小限制</span><span class="sxs-lookup"><span data-stu-id="8da6c-128">Input and Output size limitations</span></span>
<span data-ttu-id="8da6c-129">每個頂點都有指派 tooit 的記憶體數量有限。</span><span class="sxs-lookup"><span data-stu-id="8da6c-129">Every vertex has a limited amount of memory assigned tooit.</span></span> <span data-ttu-id="8da6c-130">目前，該限制為 6 GB 用於 AU。</span><span class="sxs-lookup"><span data-stu-id="8da6c-130">Currently, that limit is 6 GB for an AU.</span></span> <span data-ttu-id="8da6c-131">Hello 輸入和輸出資料框架必須存在於記憶體中 hello Python 程式碼，因為 hello hello 輸入和輸出的大小總計不能超過 6 GB。</span><span class="sxs-lookup"><span data-stu-id="8da6c-131">Because hello input and output DataFrames must exist in memory in hello Python code, hello total size for hello input and output cannot exceed 6 GB.</span></span>

## <a name="see-also"></a><span data-ttu-id="8da6c-132">另請參閱</span><span class="sxs-lookup"><span data-stu-id="8da6c-132">See also</span></span>
* [<span data-ttu-id="8da6c-133">Microsoft Azure Data Lake Analytics 概觀</span><span class="sxs-lookup"><span data-stu-id="8da6c-133">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="8da6c-134">使用 Data Lake Tools for Visual Studio 開發 U-SQL 指令碼</span><span class="sxs-lookup"><span data-stu-id="8da6c-134">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="8da6c-135">針對 Azure 資料湖分析工作使用 U-SQL 視窗函式</span><span class="sxs-lookup"><span data-stu-id="8da6c-135">Using U-SQL window functions for Azure Data Lake Analytics jobs</span></span>](data-lake-analytics-use-window-functions.md)

