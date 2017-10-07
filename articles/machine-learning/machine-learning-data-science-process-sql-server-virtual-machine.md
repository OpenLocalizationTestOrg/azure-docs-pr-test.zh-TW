---
title: "在 Azure 上的 SQL Server 虛擬機器的 aaaExplore 資料 |Microsoft 文件"
description: "在 Azure 上的 SQL Server 虛擬機器中瀏覽資料和產生功能"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: 
ms.assetid: 3949fb2c-ffab-49fb-908d-27d5e42f743b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: fashah;garye;bradsev
ms.openlocfilehash: 67f4b058b0f6557ee15fd42795c918d68f1a9871
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="e770f-103"><a name="heading"></a>在 Azure 上處理 SQL Server 虛擬機器中的資料</span><span class="sxs-lookup"><span data-stu-id="e770f-103"><a name="heading"></a>Process Data in SQL Server Virtual Machine on Azure</span></span>
<span data-ttu-id="e770f-104">本文件涵蓋如何 tooexplore 資料並產生資料儲存在 Azure 上的 SQL Server VM 的功能。</span><span class="sxs-lookup"><span data-stu-id="e770f-104">This document covers how tooexplore data and generate features for data stored in a SQL Server VM on Azure.</span></span> <span data-ttu-id="e770f-105">使用 SQL整理資料或使用 Python 這類程式設計語言，即可完成此動作。</span><span class="sxs-lookup"><span data-stu-id="e770f-105">This can be done by data wrangling using SQL or by using a programming language like Python.</span></span>

> [!NOTE]
> <span data-ttu-id="e770f-106">這份文件中的 hello 範例 SQL 陳述式會假設資料是在 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="e770f-106">hello sample SQL statements in this document assume that data is in SQL Server.</span></span> <span data-ttu-id="e770f-107">如果沒有，請參閱 toohello 雲端資料科學程序對應 toolearn 如何 toomove 您資料 tooSQL 伺服器。</span><span class="sxs-lookup"><span data-stu-id="e770f-107">If it isn't, refer toohello cloud data science process map toolearn how toomove your data tooSQL Server.</span></span>
> 
> 

## <span data-ttu-id="e770f-108"><a name="SQL"></a>使用 SQL</span><span class="sxs-lookup"><span data-stu-id="e770f-108"><a name="SQL"></a>Using SQL</span></span>
<span data-ttu-id="e770f-109">我們會描述下列資料 wrangling 工作使用 SQL 本節中的 hello:</span><span class="sxs-lookup"><span data-stu-id="e770f-109">We describe hello following data wrangling tasks in this section using SQL:</span></span>

1. [<span data-ttu-id="e770f-110">資料探索</span><span class="sxs-lookup"><span data-stu-id="e770f-110">Data Exploration</span></span>](#sql-dataexploration)
2. [<span data-ttu-id="e770f-111">功能產生</span><span class="sxs-lookup"><span data-stu-id="e770f-111">Feature Generation</span></span>](#sql-featuregen)

### <span data-ttu-id="e770f-112"><a name="sql-dataexploration"></a>資料探索</span><span class="sxs-lookup"><span data-stu-id="e770f-112"><a name="sql-dataexploration"></a>Data Exploration</span></span>
<span data-ttu-id="e770f-113">以下是一些範例 SQL 指令碼可能是 SQL Server 中的使用的 tooexplore 資料存放區。</span><span class="sxs-lookup"><span data-stu-id="e770f-113">Here are a few sample SQL scripts that can be used tooexplore data stores in SQL Server.</span></span>

> [!NOTE]
> <span data-ttu-id="e770f-114">如需實用範例，您可以使用 hello [NYC 計程車資料集](http://www.andresmh.com/nyctaxitrips/)和參考 toohello IPNB 標題為[NYC 資料 wrangling 使用 IPython 筆記型電腦和 SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb)的端對端逐步解說。</span><span class="sxs-lookup"><span data-stu-id="e770f-114">For a practical example, you can use hello [NYC Taxi dataset](http://www.andresmh.com/nyctaxitrips/) and refer toohello IPNB titled [NYC Data wrangling using IPython Notebook and SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) for an end-to-end walk-through.</span></span>
> 
> 

1. <span data-ttu-id="e770f-115">取得每日的觀察值的 hello 計數</span><span class="sxs-lookup"><span data-stu-id="e770f-115">Get hello count of observations per day</span></span>
   
    `SELECT CONVERT(date, <date_columnname>) as date, count(*) as c from <tablename> group by CONVERT(date, <date_columnname>)` 
2. <span data-ttu-id="e770f-116">取得類別的資料行中的 hello 層級</span><span class="sxs-lookup"><span data-stu-id="e770f-116">Get hello levels in a categorical column</span></span>
   
    `select  distinct <column_name> from <databasename>`
3. <span data-ttu-id="e770f-117">取得 hello 層級數目的兩個類別資料行組合中</span><span class="sxs-lookup"><span data-stu-id="e770f-117">Get hello number of levels in combination of two categorical columns</span></span> 
   
    `select <column_a>, <column_b>,count(*) from <tablename> group by <column_a>, <column_b>`
4. <span data-ttu-id="e770f-118">取得數值資料行的 hello 發佈</span><span class="sxs-lookup"><span data-stu-id="e770f-118">Get hello distribution for numerical columns</span></span>
   
    `select <column_name>, count(*) from <tablename> group by <column_name>`

### <span data-ttu-id="e770f-119"><a name="sql-featuregen"></a>功能產生</span><span class="sxs-lookup"><span data-stu-id="e770f-119"><a name="sql-featuregen"></a>Feature Generation</span></span>
<span data-ttu-id="e770f-120">在本節中，我們將說明使用 SQL 產生功能的方式：</span><span class="sxs-lookup"><span data-stu-id="e770f-120">In this section, we describe ways of generating features using SQL:</span></span>  

1. [<span data-ttu-id="e770f-121">以計數為基礎的功能產生</span><span class="sxs-lookup"><span data-stu-id="e770f-121">Count based Feature Generation</span></span>](#sql-countfeature)
2. [<span data-ttu-id="e770f-122">分類收納功能產生</span><span class="sxs-lookup"><span data-stu-id="e770f-122">Binning Feature Generation</span></span>](#sql-binningfeature)
3. [<span data-ttu-id="e770f-123">推出 hello 功能，從單一資料行</span><span class="sxs-lookup"><span data-stu-id="e770f-123">Rolling out hello features from a single column</span></span>](#sql-featurerollout)

> [!NOTE]
> <span data-ttu-id="e770f-124">一旦您產生額外的功能，您可以將它們加入為資料行 toohello 現有資料表或 hello 額外的功能與主索引鍵，可以與 hello 原始資料表聯結，建立新的資料表。</span><span class="sxs-lookup"><span data-stu-id="e770f-124">Once you generate additional features, you can either add them as columns toohello existing table or create a new table with hello additional features and primary key, that can be joined with hello original table.</span></span> 
> 
> 

### <span data-ttu-id="e770f-125"><a name="sql-countfeature"></a>以計數為基礎的功能產生</span><span class="sxs-lookup"><span data-stu-id="e770f-125"><a name="sql-countfeature"></a>Count based Feature Generation</span></span>
<span data-ttu-id="e770f-126">hello 下列範例示範兩種產生計數功能。</span><span class="sxs-lookup"><span data-stu-id="e770f-126">hello following examples demonstrate two ways of generating count features.</span></span> <span data-ttu-id="e770f-127">hello 第一種方法會使用條件式 sum 和第二個方法會使用 hello hello 'where' 子句。</span><span class="sxs-lookup"><span data-stu-id="e770f-127">hello first method uses conditional sum and hello second method uses hello 'where' clause.</span></span> <span data-ttu-id="e770f-128">這些屬性然後與 hello 原始資料表 （使用主索引鍵資料行） toohave 計數功能一起 hello 原始資料聯結。</span><span class="sxs-lookup"><span data-stu-id="e770f-128">These can then be joined with hello original table (using primary key columns) toohave count features alongside hello original data.</span></span>

    select <column_name1>,<column_name2>,<column_name3>, COUNT(*) as Count_Features from <tablename> group by <column_name1>,<column_name2>,<column_name3> 

    select <column_name1>,<column_name2> , sum(1) as Count_Features from <tablename> 
    where <column_name3> = '<some_value>' group by <column_name1>,<column_name2> 

### <span data-ttu-id="e770f-129"><a name="sql-binningfeature"></a>分類收納功能產生</span><span class="sxs-lookup"><span data-stu-id="e770f-129"><a name="sql-binningfeature"></a>Binning Feature Generation</span></span>
<span data-ttu-id="e770f-130">hello 下列範例顯示如何 toogenerate 透過分類收納功能分組 （使用五個分類收納） 可用來當做一項功能改為數值資料行：</span><span class="sxs-lookup"><span data-stu-id="e770f-130">hello following example shows how toogenerate binned features by binning (using five bins) a numerical column that can be used as a feature instead:</span></span>

    `SELECT <column_name>, NTILE(5) OVER (ORDER BY <column_name>) AS BinNumber from <tablename>`


### <span data-ttu-id="e770f-131"><a name="sql-featurerollout"></a>推出 hello 功能，從單一資料行</span><span class="sxs-lookup"><span data-stu-id="e770f-131"><a name="sql-featurerollout"></a>Rolling out hello features from a single column</span></span>
<span data-ttu-id="e770f-132">在本節中，我們將示範如何 tooroll 出資料表 toogenerate 其他功能的單一資料行。</span><span class="sxs-lookup"><span data-stu-id="e770f-132">In this section, we demonstrate how tooroll out a single column in a table toogenerate additional features.</span></span> <span data-ttu-id="e770f-133">hello 範例假設嘗試 toogenerate 功能 hello 資料表中有經度或緯度的資料行。</span><span class="sxs-lookup"><span data-stu-id="e770f-133">hello example assumes that there is a latitude or longitude column in hello table from which you are trying toogenerate features.</span></span>

<span data-ttu-id="e770f-134">以下是簡短入門經緯度位置資料 (從 stackoverflow 資源[toomeasure hello 精確度的緯度與經度的方式？](http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude))。</span><span class="sxs-lookup"><span data-stu-id="e770f-134">Here is a brief primer on latitude/longitude location data (resourced from stackoverflow [How toomeasure hello accuracy of latitude and longitude?](http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude)).</span></span> <span data-ttu-id="e770f-135">這是很有用 toounderstand featurizing hello 位置欄位之前：</span><span class="sxs-lookup"><span data-stu-id="e770f-135">This is useful toounderstand before featurizing hello location field:</span></span>

* <span data-ttu-id="e770f-136">hello 登告訴我們我們是否北或南、 東或西 hello 地球上。</span><span class="sxs-lookup"><span data-stu-id="e770f-136">hello sign tells us whether we are north or south, east or west on hello globe.</span></span>
* <span data-ttu-id="e770f-137">非零的數百個位數告訴我們使用的是經度，而不是緯度！</span><span class="sxs-lookup"><span data-stu-id="e770f-137">A nonzero hundreds digit tells us that we're using longitude, not latitude!</span></span>
* <span data-ttu-id="e770f-138">hello 數以萬計的數字提供位置 tooabout 1,000 公里為單位。</span><span class="sxs-lookup"><span data-stu-id="e770f-138">hello tens digit gives a position tooabout 1,000 kilometers.</span></span> <span data-ttu-id="e770f-139">它會為我們提供身處哪個大陸或海洋的實用資訊。</span><span class="sxs-lookup"><span data-stu-id="e770f-139">It gives us useful information about what continent or ocean we are on.</span></span>
* <span data-ttu-id="e770f-140">hello 單位數字 （一個十進位度） 提供 too111 公里 （60 海英哩，大約 69 英哩） 上的位置。</span><span class="sxs-lookup"><span data-stu-id="e770f-140">hello units digit (one decimal degree) gives a position up too111 kilometers (60 nautical miles, about 69 miles).</span></span> <span data-ttu-id="e770f-141">它會告知我們大致上位於哪一個大的州或國家/地區中。</span><span class="sxs-lookup"><span data-stu-id="e770f-141">It can tell us roughly what large state or country we are in.</span></span>
* <span data-ttu-id="e770f-142">第一個小數位數 hello 值得向上 too11.1 金鑰管理： 它可以區別 hello 的鄰近大型縣 （市） 從一個大城市的位置。</span><span class="sxs-lookup"><span data-stu-id="e770f-142">hello first decimal place is worth up too11.1 km: it can distinguish hello position of one large city from a neighboring large city.</span></span>
* <span data-ttu-id="e770f-143">第二個小數位數 hello 值得向上 too1.1 金鑰管理： 它可以分開一個 village hello 下一步。</span><span class="sxs-lookup"><span data-stu-id="e770f-143">hello second decimal place is worth up too1.1 km: it can separate one village from hello next.</span></span>
* <span data-ttu-id="e770f-144">第三個小數位數 hello 值得向上 too110 m： 大型農業欄位或機構校園，它能識別。</span><span class="sxs-lookup"><span data-stu-id="e770f-144">hello third decimal place is worth up too110 m: it can identify a large agricultural field or institutional campus.</span></span>
* <span data-ttu-id="e770f-145">第四個小數位數 hello 值得向上 too11 m： 它能識別的土地的資料。</span><span class="sxs-lookup"><span data-stu-id="e770f-145">hello fourth decimal place is worth up too11 m: it can identify a parcel of land.</span></span> <span data-ttu-id="e770f-146">它是可比較 toohello 未修正 GPS 單位沒有干擾的典型的精確度。</span><span class="sxs-lookup"><span data-stu-id="e770f-146">It is comparable toohello typical accuracy of an uncorrected GPS unit with no interference.</span></span>
* <span data-ttu-id="e770f-147">第五個小數位數 hello 值得向上 too1.1 m： 它可以區別樹狀結構與彼此。</span><span class="sxs-lookup"><span data-stu-id="e770f-147">hello fifth decimal place is worth up too1.1 m: it distinguishes trees from each other.</span></span> <span data-ttu-id="e770f-148">精確度 toothis 層級與商業 GPS 裝置只完成差異更正。</span><span class="sxs-lookup"><span data-stu-id="e770f-148">Accuracy toothis level with commercial GPS units can only be achieved with differential correction.</span></span>
* <span data-ttu-id="e770f-149">第六個小數位數 hello 值得 too0.11 m： 您可以使用此配置結構的資料，來設計環境，建置道路組成。</span><span class="sxs-lookup"><span data-stu-id="e770f-149">hello sixth decimal place is worth up too0.11 m: you can use this for laying out structures in detail, for designing landscapes, building roads.</span></span> <span data-ttu-id="e770f-150">比起足以追蹤冰河和河流的移動，這應該是更好的方式。</span><span class="sxs-lookup"><span data-stu-id="e770f-150">It should be more than good enough for tracking movements of glaciers and rivers.</span></span> <span data-ttu-id="e770f-151">您可以採用含有 GPS 的精心度量 (例如，微分校正的 GPS) 來達成此項目。</span><span class="sxs-lookup"><span data-stu-id="e770f-151">This can be achieved by taking painstaking measures with GPS, such as differentially corrected GPS.</span></span>

<span data-ttu-id="e770f-152">hello 位置資訊可能特徵化，如下所示，分開地區、 位置和縣 （市） 資訊。</span><span class="sxs-lookup"><span data-stu-id="e770f-152">hello location information can be featurized as follows, separating out region, location, and city information.</span></span> <span data-ttu-id="e770f-153">請注意，您也可以呼叫 REST 端點，例如 Bing Maps API 位於[找出的位置點](https://msdn.microsoft.com/library/ff701710.aspx)tooget hello 地區/地區的資訊。</span><span class="sxs-lookup"><span data-stu-id="e770f-153">Note that you can also call a REST end point such as Bing Maps API available at [Find a Location by Point](https://msdn.microsoft.com/library/ff701710.aspx) tooget hello region/district information.</span></span>

    select 
        <location_columnname>
        ,round(<location_columnname>,0) as l1        
        ,l2=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 1 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),1,1) else '0' end     
        ,l3=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 2 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),2,1) else '0' end     
        ,l4=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 3 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),3,1) else '0' end     
        ,l5=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 4 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),4,1) else '0' end     
        ,l6=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 5 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),5,1) else '0' end     
        ,l7=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 6 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),6,1) else '0' end     
    from <tablename>

<span data-ttu-id="e770f-154">這些位置為基礎的功能可以進一步使用的 toogenerate 其他計數功能如先前所述。</span><span class="sxs-lookup"><span data-stu-id="e770f-154">These location-based features can be further used toogenerate additional count features as described earlier.</span></span> 

> [!TIP]
> <span data-ttu-id="e770f-155">您可以透過程式設計方式插入 hello 記錄使用您所選擇的語言。</span><span class="sxs-lookup"><span data-stu-id="e770f-155">You can programmatically insert hello records using your language of choice.</span></span> <span data-ttu-id="e770f-156">您可能需要在區塊 tooimprove 寫入效率 tooinsert hello 資料 (如需如何 toodo 此使用 pyodbc，請參閱[使用 python HelloWorld 範例 tooaccess SQLServer](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python))。</span><span class="sxs-lookup"><span data-stu-id="e770f-156">You may need tooinsert hello data in chunks tooimprove write efficiency (for an example of how toodo this using pyodbc, see [A HelloWorld sample tooaccess SQLServer with python](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python)).</span></span> <span data-ttu-id="e770f-157">另一個替代方式是使用 hello hello 資料庫中的 tooinsert 資料[BCP 公用程式](https://msdn.microsoft.com/library/ms162802.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e770f-157">Another alternative is tooinsert data in hello database using hello [BCP utility](https://msdn.microsoft.com/library/ms162802.aspx).</span></span>
> 
> 

### <span data-ttu-id="e770f-158"><a name="sql-aml"></a>連接 tooAzure 機器學習服務</span><span class="sxs-lookup"><span data-stu-id="e770f-158"><a name="sql-aml"></a>Connecting tooAzure Machine Learning</span></span>
<span data-ttu-id="e770f-159">新產生的 hello 功能可以當做 tooan 現有資料行的資料表加入或儲存在新的資料表，與機器學習的 hello 原始資料表聯結。</span><span class="sxs-lookup"><span data-stu-id="e770f-159">hello newly generated feature can be added as a column tooan existing table or stored in a new table and joined with hello original table for machine learning.</span></span> <span data-ttu-id="e770f-160">功能可以產生或存取已經建立時，使用 hello[匯入資料][ import-data]如下所示，Azure Machine Learning 中的模組：</span><span class="sxs-lookup"><span data-stu-id="e770f-160">Features can be generated or accessed if already created, using hello [Import Data][import-data] module in Azure Machine Learning as shown below:</span></span>

![azureml 讀取器][1] 

## <span data-ttu-id="e770f-162"><a name="python"></a>使用類似 Python 的程式設計語言</span><span class="sxs-lookup"><span data-stu-id="e770f-162"><a name="python"></a>Using a programming language like Python</span></span>
<span data-ttu-id="e770f-163">使用 Python tooexplore 資料以及資料是 SQL Server 中的 hello 類似 tooprocessing 資料使用 Python，如中所述的 Azure blob 中的時產生功能[資料科學環境中的程序的 Azure Blob 資料](machine-learning-data-science-process-data-blob.md)。</span><span class="sxs-lookup"><span data-stu-id="e770f-163">Using Python tooexplore data and generate features when hello data is in SQL Server is similar tooprocessing data in Azure blob using Python as documented in [Process Azure Blob data in your data science environment](machine-learning-data-science-process-data-blob.md).</span></span> <span data-ttu-id="e770f-164">hello 資料需要 toobe hello 資料庫載入熊資料框架，然後可以進一步處理。</span><span class="sxs-lookup"><span data-stu-id="e770f-164">hello data needs toobe loaded from hello database into a pandas data frame and then can be processed further.</span></span> <span data-ttu-id="e770f-165">我們的文件 hello 連接 toohello 資料庫並將在本節中的 hello 資料框架 hello 資料載入程序。</span><span class="sxs-lookup"><span data-stu-id="e770f-165">We document hello process of connecting toohello database and loading hello data into hello data frame in this section.</span></span>

<span data-ttu-id="e770f-166">下列連接字串格式的 hello 可以是使用的 tooconnect tooa SQL Server 資料庫，來自 Python 使用 pyodbc （取代 servername、 dbname、 username 和 password 的特定值）：</span><span class="sxs-lookup"><span data-stu-id="e770f-166">hello following connection string format can be used tooconnect tooa SQL Server database from Python using pyodbc (replace servername, dbname, username, and password with your specific values):</span></span>

    #Set up hello SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

<span data-ttu-id="e770f-167">hello[熊程式庫](http://pandas.pydata.org/)Python 中提供一組豐富的資料結構和資料分析工具的 Python 程式設計資料操作。</span><span class="sxs-lookup"><span data-stu-id="e770f-167">hello [Pandas library](http://pandas.pydata.org/) in Python provides a rich set of data structures and data analysis tools for data manipulation for Python programming.</span></span> <span data-ttu-id="e770f-168">下列程式碼 hello 讀取從 SQL Server 資料庫傳回至熊資料框架的 hello 結果：</span><span class="sxs-lookup"><span data-stu-id="e770f-168">hello code below reads hello results returned from a SQL Server database into a Pandas data frame:</span></span>

    # Query database and load hello returned results in pandas data frame
    data_frame = pd.read_sql('''select <columnname1>, <cloumnname2>... from <tablename>''', conn)

<span data-ttu-id="e770f-169">現在您可以在 hello 文件中涵蓋 hello 熊資料框架[資料科學環境中的程序的 Azure Blob 資料](machine-learning-data-science-process-data-blob.md)。</span><span class="sxs-lookup"><span data-stu-id="e770f-169">Now you can work with hello Pandas data frame as covered in hello article [Process Azure Blob data in your data science environment](machine-learning-data-science-process-data-blob.md).</span></span>

## <a name="azure-data-science-in-action-example"></a><span data-ttu-id="e770f-170">作用中的 Azure 資料科學範例</span><span class="sxs-lookup"><span data-stu-id="e770f-170">Azure Data Science in Action Example</span></span>
<span data-ttu-id="e770f-171">如需端對端逐步解說的範例 hello Azure 資料科學使用公用資料集的處理程序，請參閱[動作中的 Azure 資料科學程序](machine-learning-data-science-process-sql-walkthrough.md)。</span><span class="sxs-lookup"><span data-stu-id="e770f-171">For an end-to-end walkthrough example of hello Azure Data Science Process using a public dataset, see [Azure Data Science Process in Action](machine-learning-data-science-process-sql-walkthrough.md).</span></span>

[1]: ./media/machine-learning-data-science-process-sql-server-virtual-machine/reader_db_featurizedinput.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/

