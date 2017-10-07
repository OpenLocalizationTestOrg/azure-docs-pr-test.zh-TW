---
title: "SQL Server 使用 SQL 和 Python 中資料的 aaaCreate 功能 |Microsoft 文件"
description: "處理 SQL Azure 的資料"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: 
ms.assetid: bf1f4a6c-7711-4456-beb7-35fdccd46a44
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;fashah;garye
ms.openlocfilehash: 223352edb0377a159333e7528ad03c43902e6f45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-features-for-data-in-sql-server-using-sql-and-python"></a><span data-ttu-id="d90fa-103">使用 SQL 和 Python 對 SQL Server 中的資料建立功能</span><span class="sxs-lookup"><span data-stu-id="d90fa-103">Create features for data in SQL Server using SQL and Python</span></span>
<span data-ttu-id="d90fa-104">本文件示範 toogenerate 功能資料會儲存在 Azure 上的 SQL Server VM，協助演算法的學習更有效率的 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="d90fa-104">This document shows how toogenerate features for data stored in a SQL Server VM on Azure that help algorithms learn more efficiently from hello data.</span></span> <span data-ttu-id="d90fa-105">使用 SQL 或使用類似 Python 的程式設計語言都可以達到此目的，以下示範這兩者。</span><span class="sxs-lookup"><span data-stu-id="d90fa-105">This can be done by using SQL or by using a programming language like Python, both of which are demonstrated here.</span></span>

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

<span data-ttu-id="d90fa-106">這**功能表**連結 tootopics 描述 toocreate 各種環境中的資料的功能。</span><span class="sxs-lookup"><span data-stu-id="d90fa-106">This **menu** links tootopics that describe how toocreate features for data in various environments.</span></span> <span data-ttu-id="d90fa-107">這項工作是在 hello 步驟[小組資料科學程序 (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/)。</span><span class="sxs-lookup"><span data-stu-id="d90fa-107">This task is a step in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

> [!NOTE]
> <span data-ttu-id="d90fa-108">如需實用範例，請參閱 hello [NYC 計程車資料集](http://www.andresmh.com/nyctaxitrips/)和參考 toohello IPNB 標題為[NYC 資料 wrangling 使用 IPython 筆記型電腦和 SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb)的端對端逐步解說。</span><span class="sxs-lookup"><span data-stu-id="d90fa-108">For a practical example, you can consult hello [NYC Taxi dataset](http://www.andresmh.com/nyctaxitrips/) and refer toohello IPNB titled [NYC Data wrangling using IPython Notebook and SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) for an end-to-end walk-through.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="d90fa-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="d90fa-109">Prerequisites</span></span>
<span data-ttu-id="d90fa-110">本文假設您已經：</span><span class="sxs-lookup"><span data-stu-id="d90fa-110">This article assumes that you have:</span></span>

* <span data-ttu-id="d90fa-111">建立 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="d90fa-111">Created an Azure storage account.</span></span> <span data-ttu-id="d90fa-112">如需指示，請參閱[建立 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="d90fa-112">If you need instructions, see [Create an Azure Storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span></span>
* <span data-ttu-id="d90fa-113">將資料儲存在 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="d90fa-113">Stored your data in SQL Server.</span></span> <span data-ttu-id="d90fa-114">如果您沒有這樣做，請參閱[移動資料 tooan Azure SQL Database 的 Azure Machine Learning](machine-learning-data-science-move-sql-azure.md)如需如何 toomove hello 那里資料的指示。</span><span class="sxs-lookup"><span data-stu-id="d90fa-114">If you have not, see [Move data tooan Azure SQL Database for Azure Machine Learning](machine-learning-data-science-move-sql-azure.md) for instructions on how toomove hello data there.</span></span>

## <span data-ttu-id="d90fa-115"><a name="sql-featuregen"></a>使用 SQL 的功能產生</span><span class="sxs-lookup"><span data-stu-id="d90fa-115"><a name="sql-featuregen"></a>Feature Generation with SQL</span></span>
<span data-ttu-id="d90fa-116">在本節中，我們將說明使用 SQL 產生功能的方式：</span><span class="sxs-lookup"><span data-stu-id="d90fa-116">In this section, we describe ways of generating features using SQL:</span></span>  

1. [<span data-ttu-id="d90fa-117">以計數為基礎的功能產生</span><span class="sxs-lookup"><span data-stu-id="d90fa-117">Count based Feature Generation</span></span>](#sql-countfeature)
2. [<span data-ttu-id="d90fa-118">分類收納功能產生</span><span class="sxs-lookup"><span data-stu-id="d90fa-118">Binning Feature Generation</span></span>](#sql-binningfeature)
3. [<span data-ttu-id="d90fa-119">推出 hello 功能，從單一資料行</span><span class="sxs-lookup"><span data-stu-id="d90fa-119">Rolling out hello features from a single column</span></span>](#sql-featurerollout)

> [!NOTE]
> <span data-ttu-id="d90fa-120">一旦您產生額外的功能，您可以將它們加入為資料行 toohello 現有資料表或 hello 額外的功能與主索引鍵，可以與 hello 原始資料表聯結，建立新的資料表。</span><span class="sxs-lookup"><span data-stu-id="d90fa-120">Once you generate additional features, you can either add them as columns toohello existing table or create a new table with hello additional features and primary key, that can be joined with hello original table.</span></span>
> 
> 

### <span data-ttu-id="d90fa-121"><a name="sql-countfeature"></a>以計數為基礎的功能產生</span><span class="sxs-lookup"><span data-stu-id="d90fa-121"><a name="sql-countfeature"></a>Count based Feature Generation</span></span>
<span data-ttu-id="d90fa-122">本文件示範兩種產生計數功能的方法。</span><span class="sxs-lookup"><span data-stu-id="d90fa-122">This document demonstrates two ways of generating count features.</span></span> <span data-ttu-id="d90fa-123">hello 第一種方法會使用條件式 sum 和第二個方法會使用 hello hello 'where' 子句。</span><span class="sxs-lookup"><span data-stu-id="d90fa-123">hello first method uses conditional sum and hello second method uses hello 'where\` clause.</span></span> <span data-ttu-id="d90fa-124">這些屬性然後與 hello 原始資料表 （使用主索引鍵資料行） toohave 計數功能一起 hello 原始資料聯結。</span><span class="sxs-lookup"><span data-stu-id="d90fa-124">These can then be joined with hello original table (using primary key columns) toohave count features alongside hello original data.</span></span>

    select <column_name1>,<column_name2>,<column_name3>, COUNT(*) as Count_Features from <tablename> group by <column_name1>,<column_name2>,<column_name3>

    select <column_name1>,<column_name2> , sum(1) as Count_Features from <tablename>
    where <column_name3> = '<some_value>' group by <column_name1>,<column_name2>

### <span data-ttu-id="d90fa-125"><a name="sql-binningfeature"></a>分類收納功能產生</span><span class="sxs-lookup"><span data-stu-id="d90fa-125"><a name="sql-binningfeature"></a>Binning Feature Generation</span></span>
<span data-ttu-id="d90fa-126">hello 下列範例顯示如何 toogenerate 透過分類收納功能分組 （使用 5 個分類收納） 可用來當做一項功能改為數值資料行：</span><span class="sxs-lookup"><span data-stu-id="d90fa-126">hello following example shows how toogenerate binned features by binning (using 5 bins) a numerical column that can be used as a feature instead:</span></span>

    `SELECT <column_name>, NTILE(5) OVER (ORDER BY <column_name>) AS BinNumber from <tablename>`


### <span data-ttu-id="d90fa-127"><a name="sql-featurerollout"></a>推出 hello 功能，從單一資料行</span><span class="sxs-lookup"><span data-stu-id="d90fa-127"><a name="sql-featurerollout"></a>Rolling out hello features from a single column</span></span>
<span data-ttu-id="d90fa-128">在本節中，我們會示範如何 tooroll 外的單一資料行資料表 toogenerate 其他功能。</span><span class="sxs-lookup"><span data-stu-id="d90fa-128">In this section, we demonstrate how tooroll-out a single column in a table toogenerate additional features.</span></span> <span data-ttu-id="d90fa-129">hello 範例假設嘗試 toogenerate 功能 hello 資料表中有經度或緯度的資料行。</span><span class="sxs-lookup"><span data-stu-id="d90fa-129">hello example assumes that there is a latitude or longitude column in hello table from which you are trying toogenerate features.</span></span>

<span data-ttu-id="d90fa-130">以下是有關經緯度位置資料的簡短入門指南 (源自 stackoverflow `http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude`)。</span><span class="sxs-lookup"><span data-stu-id="d90fa-130">Here is a brief primer on latitude/longitude location data (resourced from stackoverflow `http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude`).</span></span> <span data-ttu-id="d90fa-131">這是很有用 toounderstand featurizing hello 位置欄位之前：</span><span class="sxs-lookup"><span data-stu-id="d90fa-131">This is useful toounderstand before featurizing hello location field:</span></span>

* <span data-ttu-id="d90fa-132">hello 登告訴我們我們是否北或南、 東或西 hello 地球上。</span><span class="sxs-lookup"><span data-stu-id="d90fa-132">hello sign tells us whether we are north or south, east or west on hello globe.</span></span>
* <span data-ttu-id="d90fa-133">非零的數百個位數告訴我們使用的是經度，而不是緯度！</span><span class="sxs-lookup"><span data-stu-id="d90fa-133">A nonzero hundreds digit tells us we're using longitude, not latitude!</span></span>
* <span data-ttu-id="d90fa-134">hello 數以萬計的數字提供位置 tooabout 1,000 公里為單位。</span><span class="sxs-lookup"><span data-stu-id="d90fa-134">hello tens digit gives a position tooabout 1,000 kilometers.</span></span> <span data-ttu-id="d90fa-135">它會為我們提供身處哪個大陸或海洋的實用資訊。</span><span class="sxs-lookup"><span data-stu-id="d90fa-135">It gives us useful information about what continent or ocean we are on.</span></span>
* <span data-ttu-id="d90fa-136">hello 單位數字 （一個十進位度） 提供 too111 公里 （60 海英哩，大約 69 英哩） 上的位置。</span><span class="sxs-lookup"><span data-stu-id="d90fa-136">hello units digit (one decimal degree) gives a position up too111 kilometers (60 nautical miles, about 69 miles).</span></span> <span data-ttu-id="d90fa-137">它會告知我們大致上位於哪一個大的州或國家/地區中。</span><span class="sxs-lookup"><span data-stu-id="d90fa-137">It can tell us roughly what large state or country we are in.</span></span>
* <span data-ttu-id="d90fa-138">第一個小數位數 hello 值得向上 too11.1 金鑰管理： 它可以區別 hello 的鄰近大型縣 （市） 從一個大城市的位置。</span><span class="sxs-lookup"><span data-stu-id="d90fa-138">hello first decimal place is worth up too11.1 km: it can distinguish hello position of one large city from a neighboring large city.</span></span>
* <span data-ttu-id="d90fa-139">第二個小數位數 hello 值得向上 too1.1 金鑰管理： 它可以分開一個 village hello 下一步。</span><span class="sxs-lookup"><span data-stu-id="d90fa-139">hello second decimal place is worth up too1.1 km: it can separate one village from hello next.</span></span>
* <span data-ttu-id="d90fa-140">第三個小數位數 hello 值得向上 too110 m： 大型農業欄位或機構校園，它能識別。</span><span class="sxs-lookup"><span data-stu-id="d90fa-140">hello third decimal place is worth up too110 m: it can identify a large agricultural field or institutional campus.</span></span>
* <span data-ttu-id="d90fa-141">第四個小數位數 hello 值得向上 too11 m： 它能識別的土地的資料。</span><span class="sxs-lookup"><span data-stu-id="d90fa-141">hello fourth decimal place is worth up too11 m: it can identify a parcel of land.</span></span> <span data-ttu-id="d90fa-142">它是可比較 toohello 未修正 GPS 單位沒有干擾的典型的精確度。</span><span class="sxs-lookup"><span data-stu-id="d90fa-142">It is comparable toohello typical accuracy of an uncorrected GPS unit with no interference.</span></span>
* <span data-ttu-id="d90fa-143">hello 第五個小數位數是值得向上 too1.1 m： 形式彼此區分樹狀結構。</span><span class="sxs-lookup"><span data-stu-id="d90fa-143">hello fifth decimal place is worth up too1.1 m: it distinguish trees from each other.</span></span> <span data-ttu-id="d90fa-144">精確度 toothis 層級與商業 GPS 裝置只完成差異更正。</span><span class="sxs-lookup"><span data-stu-id="d90fa-144">Accuracy toothis level with commercial GPS units can only be achieved with differential correction.</span></span>
* <span data-ttu-id="d90fa-145">第六個小數位數 hello 值得 too0.11 m： 您可以使用此配置結構的資料，來設計環境，建置道路組成。</span><span class="sxs-lookup"><span data-stu-id="d90fa-145">hello sixth decimal place is worth up too0.11 m: you can use this for laying out structures in detail, for designing landscapes, building roads.</span></span> <span data-ttu-id="d90fa-146">比起足以追蹤冰河和河流的移動，這應該是更好的方式。</span><span class="sxs-lookup"><span data-stu-id="d90fa-146">It should be more than good enough for tracking movements of glaciers and rivers.</span></span> <span data-ttu-id="d90fa-147">您可以採用含有 GPS 的精心度量 (例如，微分校正的 GPS) 來達成此項目。</span><span class="sxs-lookup"><span data-stu-id="d90fa-147">This can be achieved by taking painstaking measures with GPS, such as differentially corrected GPS.</span></span>

<span data-ttu-id="d90fa-148">hello 位置資訊可以可能特徵化，如下所示，分開地區、 位置和縣 （市） 資訊。</span><span class="sxs-lookup"><span data-stu-id="d90fa-148">hello location information can can be featurized as follows, separating out region, location and city information.</span></span> <span data-ttu-id="d90fa-149">請注意，一次也可以呼叫 REST 端點，例如 Bing Maps API 位於`https://msdn.microsoft.com/library/ff701710.aspx`tooget hello 地區/地區的資訊。</span><span class="sxs-lookup"><span data-stu-id="d90fa-149">Note that once can also call a REST end point such as Bing Maps API available at `https://msdn.microsoft.com/library/ff701710.aspx` tooget hello region/district information.</span></span>

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

<span data-ttu-id="d90fa-150">hello 上述位置根據的功能可以進一步使用 toogenerate 其他計數功能，如先前所述。</span><span class="sxs-lookup"><span data-stu-id="d90fa-150">hello above location based features can be further used toogenerate additional count features as described earlier.</span></span>

> [!TIP]
> <span data-ttu-id="d90fa-151">您可以透過程式設計方式插入 hello 記錄使用您所選擇的語言。</span><span class="sxs-lookup"><span data-stu-id="d90fa-151">You can programmatically insert hello records using your language of choice.</span></span> <span data-ttu-id="d90fa-152">您可能需要 tooinsert hello 資料區塊 （chunk） tooimprove 寫入效率[簽出的 hello 範例 toodo 此使用 pyodbc 此處](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python)。</span><span class="sxs-lookup"><span data-stu-id="d90fa-152">You may need tooinsert hello data in chunks tooimprove write efficiency [Check out hello example of how toodo this using pyodbc here](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python).</span></span>
> <span data-ttu-id="d90fa-153">另一個替代方式是在 hello 資料庫使用的 tooinsert 資料[BCP 公用程式](https://msdn.microsoft.com/library/ms162802.aspx)</span><span class="sxs-lookup"><span data-stu-id="d90fa-153">Another alternative is tooinsert data in hello database using [BCP utility](https://msdn.microsoft.com/library/ms162802.aspx)</span></span>
> 
> 

### <span data-ttu-id="d90fa-154"><a name="sql-aml"></a>連接 tooAzure 機器學習服務</span><span class="sxs-lookup"><span data-stu-id="d90fa-154"><a name="sql-aml"></a>Connecting tooAzure Machine Learning</span></span>
<span data-ttu-id="d90fa-155">新產生的 hello 功能可以當做 tooan 現有資料行的資料表加入或儲存在新的資料表，與機器學習的 hello 原始資料表聯結。</span><span class="sxs-lookup"><span data-stu-id="d90fa-155">hello newly generated feature can be added as a column tooan existing table or stored in a new table and joined with hello original table for machine learning.</span></span> <span data-ttu-id="d90fa-156">功能可以產生或存取已經建立時，使用 hello[匯入資料](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/)中如下所示，Azure ML 模組：</span><span class="sxs-lookup"><span data-stu-id="d90fa-156">Features can be generated or accessed if already created, using hello [Import Data](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) module in Azure ML as shown below:</span></span>

![azureml 讀取器](./media/machine-learning-data-science-process-sql-server-virtual-machine/reader_db_featurizedinput.png)

## <span data-ttu-id="d90fa-158"><a name="python"></a>使用類似 Python 的程式設計語言</span><span class="sxs-lookup"><span data-stu-id="d90fa-158"><a name="python"></a>Using a programming language like Python</span></span>
<span data-ttu-id="d90fa-159">Hello 資料是以 SQL Server 時，使用 Python toogenerate 功能類似 tooprocessing 資料位於使用 Python，如中所述的 Azure blob[您資料科學環境中的程序的 Azure Blob 資料](machine-learning-data-science-process-data-blob.md)。</span><span class="sxs-lookup"><span data-stu-id="d90fa-159">Using Python toogenerate features when hello data is in SQL Server is similar tooprocessing data in Azure blob using Python as documented in [Process Azure Blob data in you data science environment](machine-learning-data-science-process-data-blob.md).</span></span> <span data-ttu-id="d90fa-160">hello 資料需要 toobe hello 資料庫載入熊資料框架，然後可以進一步處理。</span><span class="sxs-lookup"><span data-stu-id="d90fa-160">hello data needs toobe loaded from hello database into a pandas data frame and then can be processed further.</span></span> <span data-ttu-id="d90fa-161">我們的文件 hello 連接 toohello 資料庫並將在本節中的 hello 資料框架 hello 資料載入程序。</span><span class="sxs-lookup"><span data-stu-id="d90fa-161">We document hello process of connecting toohello database and loading hello data into hello data frame in this section.</span></span>

<span data-ttu-id="d90fa-162">下列連接字串格式的 hello 可以是使用的 tooconnect tooa SQL Server 資料庫，來自 Python 使用 pyodbc （取代 servername、 dbname、 使用者名稱和密碼的特定值）：</span><span class="sxs-lookup"><span data-stu-id="d90fa-162">hello following connection string format can be used tooconnect tooa SQL Server database from Python using pyodbc (replace servername, dbname, username and password with your specific values):</span></span>

    #Set up hello SQL Azure connection
    import pyodbc
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

<span data-ttu-id="d90fa-163">hello[熊程式庫](http://pandas.pydata.org/)Python 中提供一組豐富的資料結構和資料分析工具的 Python 程式設計資料操作。</span><span class="sxs-lookup"><span data-stu-id="d90fa-163">hello [Pandas library](http://pandas.pydata.org/) in Python provides a rich set of data structures and data analysis tools for data manipulation for Python programming.</span></span> <span data-ttu-id="d90fa-164">下列程式碼 hello 讀取從 SQL Server 資料庫傳回至熊資料框架的 hello 結果：</span><span class="sxs-lookup"><span data-stu-id="d90fa-164">hello code below reads hello results returned from a SQL Server database into a Pandas data frame:</span></span>

    # Query database and load hello returned results in pandas data frame
    data_frame = pd.read_sql('''select <columnname1>, <cloumnname2>... from <tablename>''', conn)

<span data-ttu-id="d90fa-165">現在您可與 hello 熊資料框架中的主題涵蓋[建立功能的 Azure blob 儲存體資料使用貓熊](machine-learning-data-science-create-features-blob.md)。</span><span class="sxs-lookup"><span data-stu-id="d90fa-165">Now you can work with hello Pandas data frame as covered in topics [Create features for Azure blob storage data using Panda](machine-learning-data-science-create-features-blob.md).</span></span>

