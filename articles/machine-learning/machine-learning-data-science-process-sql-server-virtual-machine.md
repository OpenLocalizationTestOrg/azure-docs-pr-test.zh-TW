---
title: "在 Azure 上瀏覽 SQL Server 虛擬機器中的資料 | Microsoft Docs"
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
ms.openlocfilehash: 16fabb29bdc8ec770efd843e18e9016e338a8f4e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <span data-ttu-id="ed356-103"><a name="heading"></a>在 Azure 上處理 SQL Server 虛擬機器中的資料</span><span class="sxs-lookup"><span data-stu-id="ed356-103"><a name="heading"></a>Process Data in SQL Server Virtual Machine on Azure</span></span>
<span data-ttu-id="ed356-104">本文件涵蓋如何探索資料及如何針對儲存於 Azure 上之 SQL Server VM 中的資料產生功能。</span><span class="sxs-lookup"><span data-stu-id="ed356-104">This document covers how to explore data and generate features for data stored in a SQL Server VM on Azure.</span></span> <span data-ttu-id="ed356-105">使用 SQL整理資料或使用 Python 這類程式設計語言，即可完成此動作。</span><span class="sxs-lookup"><span data-stu-id="ed356-105">This can be done by data wrangling using SQL or by using a programming language like Python.</span></span>

> [!NOTE]
> <span data-ttu-id="ed356-106">本文件中的 SQL 陳述式範例假設資料位於 SQL Server 中。</span><span class="sxs-lookup"><span data-stu-id="ed356-106">The sample SQL statements in this document assume that data is in SQL Server.</span></span> <span data-ttu-id="ed356-107">如果不是，請參閱雲端資料科學程序圖，以了解如何將資料移至 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="ed356-107">If it isn't, refer to the cloud data science process map to learn how to move your data to SQL Server.</span></span>
> 
> 

## <span data-ttu-id="ed356-108"><a name="SQL"></a>使用 SQL</span><span class="sxs-lookup"><span data-stu-id="ed356-108"><a name="SQL"></a>Using SQL</span></span>
<span data-ttu-id="ed356-109">我們將在本節中使用 SQL，來說明下列資料有爭議的工作：</span><span class="sxs-lookup"><span data-stu-id="ed356-109">We describe the following data wrangling tasks in this section using SQL:</span></span>

1. [<span data-ttu-id="ed356-110">資料探索</span><span class="sxs-lookup"><span data-stu-id="ed356-110">Data Exploration</span></span>](#sql-dataexploration)
2. [<span data-ttu-id="ed356-111">功能產生</span><span class="sxs-lookup"><span data-stu-id="ed356-111">Feature Generation</span></span>](#sql-featuregen)

### <span data-ttu-id="ed356-112"><a name="sql-dataexploration"></a>資料探索</span><span class="sxs-lookup"><span data-stu-id="ed356-112"><a name="sql-dataexploration"></a>Data Exploration</span></span>
<span data-ttu-id="ed356-113">以下是數個 SQL 指令碼範例，可用來探索儲存於 SQL Server 中的資料。</span><span class="sxs-lookup"><span data-stu-id="ed356-113">Here are a few sample SQL scripts that can be used to explore data stores in SQL Server.</span></span>

> [!NOTE]
> <span data-ttu-id="ed356-114">如需實用範例，您可以使用 [NYC 計程車資料集](http://www.andresmh.com/nyctaxitrips/)，並參考標題為[使用 IPython Notebook 和 SQL Server 來處理有爭議的 NYC 資料](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb)的 IPNB，以進行端對端逐步解說。</span><span class="sxs-lookup"><span data-stu-id="ed356-114">For a practical example, you can use the [NYC Taxi dataset](http://www.andresmh.com/nyctaxitrips/) and refer to the IPNB titled [NYC Data wrangling using IPython Notebook and SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) for an end-to-end walk-through.</span></span>
> 
> 

1. <span data-ttu-id="ed356-115">取得每天的觀察計數</span><span class="sxs-lookup"><span data-stu-id="ed356-115">Get the count of observations per day</span></span>
   
    `SELECT CONVERT(date, <date_columnname>) as date, count(*) as c from <tablename> group by CONVERT(date, <date_columnname>)` 
2. <span data-ttu-id="ed356-116">取得類別資料行中的層級</span><span class="sxs-lookup"><span data-stu-id="ed356-116">Get the levels in a categorical column</span></span>
   
    `select  distinct <column_name> from <databasename>`
3. <span data-ttu-id="ed356-117">取得兩個類別資料行組合中的層級數目</span><span class="sxs-lookup"><span data-stu-id="ed356-117">Get the number of levels in combination of two categorical columns</span></span> 
   
    `select <column_a>, <column_b>,count(*) from <tablename> group by <column_a>, <column_b>`
4. <span data-ttu-id="ed356-118">取得數值資料行的分佈</span><span class="sxs-lookup"><span data-stu-id="ed356-118">Get the distribution for numerical columns</span></span>
   
    `select <column_name>, count(*) from <tablename> group by <column_name>`

### <span data-ttu-id="ed356-119"><a name="sql-featuregen"></a>功能產生</span><span class="sxs-lookup"><span data-stu-id="ed356-119"><a name="sql-featuregen"></a>Feature Generation</span></span>
<span data-ttu-id="ed356-120">在本節中，我們將說明使用 SQL 產生功能的方式：</span><span class="sxs-lookup"><span data-stu-id="ed356-120">In this section, we describe ways of generating features using SQL:</span></span>  

1. [<span data-ttu-id="ed356-121">以計數為基礎的功能產生</span><span class="sxs-lookup"><span data-stu-id="ed356-121">Count based Feature Generation</span></span>](#sql-countfeature)
2. [<span data-ttu-id="ed356-122">分類收納功能產生</span><span class="sxs-lookup"><span data-stu-id="ed356-122">Binning Feature Generation</span></span>](#sql-binningfeature)
3. [<span data-ttu-id="ed356-123">從單一資料行衍生功能</span><span class="sxs-lookup"><span data-stu-id="ed356-123">Rolling out the features from a single column</span></span>](#sql-featurerollout)

> [!NOTE]
> <span data-ttu-id="ed356-124">一旦產生額外功能之後，就可以將它們當成資料行新增至現有的資料表，或是建立具有其他功能和主索引鍵的新資料表 (可與原始資料表聯結)。</span><span class="sxs-lookup"><span data-stu-id="ed356-124">Once you generate additional features, you can either add them as columns to the existing table or create a new table with the additional features and primary key, that can be joined with the original table.</span></span> 
> 
> 

### <span data-ttu-id="ed356-125"><a name="sql-countfeature"></a>以計數為基礎的功能產生</span><span class="sxs-lookup"><span data-stu-id="ed356-125"><a name="sql-countfeature"></a>Count based Feature Generation</span></span>
<span data-ttu-id="ed356-126">下列範例示範兩種產生計數功能的方法。</span><span class="sxs-lookup"><span data-stu-id="ed356-126">The following examples demonstrate two ways of generating count features.</span></span> <span data-ttu-id="ed356-127">第一種方法會使用條件式加總，而第二種方法會使用 'where' 子句。</span><span class="sxs-lookup"><span data-stu-id="ed356-127">The first method uses conditional sum and the second method uses the 'where' clause.</span></span> <span data-ttu-id="ed356-128">這些接著可與原始資料表聯結 (使用主索引鍵資料行)，以具備計數功能及原始資料。</span><span class="sxs-lookup"><span data-stu-id="ed356-128">These can then be joined with the original table (using primary key columns) to have count features alongside the original data.</span></span>

    select <column_name1>,<column_name2>,<column_name3>, COUNT(*) as Count_Features from <tablename> group by <column_name1>,<column_name2>,<column_name3> 

    select <column_name1>,<column_name2> , sum(1) as Count_Features from <tablename> 
    where <column_name3> = '<some_value>' group by <column_name1>,<column_name2> 

### <span data-ttu-id="ed356-129"><a name="sql-binningfeature"></a>分類收納功能產生</span><span class="sxs-lookup"><span data-stu-id="ed356-129"><a name="sql-binningfeature"></a>Binning Feature Generation</span></span>
<span data-ttu-id="ed356-130">下列範例將示範如何藉由分類收納 (使用五個分類收納組) 可改用來做為功能的數值資料行，來產生分類收納功能：</span><span class="sxs-lookup"><span data-stu-id="ed356-130">The following example shows how to generate binned features by binning (using five bins) a numerical column that can be used as a feature instead:</span></span>

    `SELECT <column_name>, NTILE(5) OVER (ORDER BY <column_name>) AS BinNumber from <tablename>`


### <span data-ttu-id="ed356-131"><a name="sql-featurerollout"></a>從單一資料行衍生功能</span><span class="sxs-lookup"><span data-stu-id="ed356-131"><a name="sql-featurerollout"></a>Rolling out the features from a single column</span></span>
<span data-ttu-id="ed356-132">本節示範如何在資料表中衍生單一資料行來產生額外功能。</span><span class="sxs-lookup"><span data-stu-id="ed356-132">In this section, we demonstrate how to roll out a single column in a table to generate additional features.</span></span> <span data-ttu-id="ed356-133">此範例假設您正嘗試從中產生功能的資料表中具有緯度或經度資料行。</span><span class="sxs-lookup"><span data-stu-id="ed356-133">The example assumes that there is a latitude or longitude column in the table from which you are trying to generate features.</span></span>

<span data-ttu-id="ed356-134">以下是有關經緯度位置資料的簡短入門指南 (源自 stackoverflow [如何測量經度和緯度的準確性？](http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude))。</span><span class="sxs-lookup"><span data-stu-id="ed356-134">Here is a brief primer on latitude/longitude location data (resourced from stackoverflow [How to measure the accuracy of latitude and longitude?](http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude)).</span></span> <span data-ttu-id="ed356-135">這有助於您在將功能化位置欄位之前先行了解：</span><span class="sxs-lookup"><span data-stu-id="ed356-135">This is useful to understand before featurizing the location field:</span></span>

* <span data-ttu-id="ed356-136">正負號告訴我們是否位於地球的北方或南方、東方或西方。</span><span class="sxs-lookup"><span data-stu-id="ed356-136">The sign tells us whether we are north or south, east or west on the globe.</span></span>
* <span data-ttu-id="ed356-137">非零的數百個位數告訴我們使用的是經度，而不是緯度！</span><span class="sxs-lookup"><span data-stu-id="ed356-137">A nonzero hundreds digit tells us that we're using longitude, not latitude!</span></span>
* <span data-ttu-id="ed356-138">數十個位數可提供大約 1,000 公里的位置。</span><span class="sxs-lookup"><span data-stu-id="ed356-138">The tens digit gives a position to about 1,000 kilometers.</span></span> <span data-ttu-id="ed356-139">它會為我們提供身處哪個大陸或海洋的實用資訊。</span><span class="sxs-lookup"><span data-stu-id="ed356-139">It gives us useful information about what continent or ocean we are on.</span></span>
* <span data-ttu-id="ed356-140">單位數 (一個十進位度數) 提供一個最多可達 111 公里 (60 海浬，大約 69 英哩) 的位置。</span><span class="sxs-lookup"><span data-stu-id="ed356-140">The units digit (one decimal degree) gives a position up to 111 kilometers (60 nautical miles, about 69 miles).</span></span> <span data-ttu-id="ed356-141">它會告知我們大致上位於哪一個大的州或國家/地區中。</span><span class="sxs-lookup"><span data-stu-id="ed356-141">It can tell us roughly what large state or country we are in.</span></span>
* <span data-ttu-id="ed356-142">第一個小數點最多可達 11.1 km：它能夠分辨某一個大型縣 (市) 的位置與鄰近的大型縣 (市)。</span><span class="sxs-lookup"><span data-stu-id="ed356-142">The first decimal place is worth up to 11.1 km: it can distinguish the position of one large city from a neighboring large city.</span></span>
* <span data-ttu-id="ed356-143">第二個小數位數最多可達 1.1 km：它可以將某一個村莊與下一個村莊分隔開來。</span><span class="sxs-lookup"><span data-stu-id="ed356-143">The second decimal place is worth up to 1.1 km: it can separate one village from the next.</span></span>
* <span data-ttu-id="ed356-144">第三個小數位數最多可達 110 m：它可以識別大型農場或學術機構校區。</span><span class="sxs-lookup"><span data-stu-id="ed356-144">The third decimal place is worth up to 110 m: it can identify a large agricultural field or institutional campus.</span></span>
* <span data-ttu-id="ed356-145">第四個小數位數最多可達 11 m：它可以識別某一塊土地。</span><span class="sxs-lookup"><span data-stu-id="ed356-145">The fourth decimal place is worth up to 11 m: it can identify a parcel of land.</span></span> <span data-ttu-id="ed356-146">它相當於未修正的 GPS 單位且無干擾的一般精確度。</span><span class="sxs-lookup"><span data-stu-id="ed356-146">It is comparable to the typical accuracy of an uncorrected GPS unit with no interference.</span></span>
* <span data-ttu-id="ed356-147">第五個小數位數最多可達 1.1 m：它會分辨彼此的樹狀結構。</span><span class="sxs-lookup"><span data-stu-id="ed356-147">The fifth decimal place is worth up to 1.1 m: it distinguishes trees from each other.</span></span> <span data-ttu-id="ed356-148">您只能使用微分校正來達到此層級利用商業 GPS 單位所達到的精確度。</span><span class="sxs-lookup"><span data-stu-id="ed356-148">Accuracy to this level with commercial GPS units can only be achieved with differential correction.</span></span>
* <span data-ttu-id="ed356-149">第六個小數位數最多可達 0.11 m：您可以使用此項目來詳細配置結構，其適用於設計環境和建置道路。</span><span class="sxs-lookup"><span data-stu-id="ed356-149">The sixth decimal place is worth up to 0.11 m: you can use this for laying out structures in detail, for designing landscapes, building roads.</span></span> <span data-ttu-id="ed356-150">比起足以追蹤冰河和河流的移動，這應該是更好的方式。</span><span class="sxs-lookup"><span data-stu-id="ed356-150">It should be more than good enough for tracking movements of glaciers and rivers.</span></span> <span data-ttu-id="ed356-151">您可以採用含有 GPS 的精心度量 (例如，微分校正的 GPS) 來達成此項目。</span><span class="sxs-lookup"><span data-stu-id="ed356-151">This can be achieved by taking painstaking measures with GPS, such as differentially corrected GPS.</span></span>

<span data-ttu-id="ed356-152">您可以使用下列方式來將位置資訊功能化，以分隔出區域、位置及縣 (市) 資訊。</span><span class="sxs-lookup"><span data-stu-id="ed356-152">The location information can be featurized as follows, separating out region, location, and city information.</span></span> <span data-ttu-id="ed356-153">請注意，您也可以呼叫 REST 端點，例如，可在 [依點尋找位置](https://msdn.microsoft.com/library/ff701710.aspx) 上取得的 Bing Maps API，以取得區域或地區資訊。</span><span class="sxs-lookup"><span data-stu-id="ed356-153">Note that you can also call a REST end point such as Bing Maps API available at [Find a Location by Point](https://msdn.microsoft.com/library/ff701710.aspx) to get the region/district information.</span></span>

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

<span data-ttu-id="ed356-154">這些以位置為基礎的功能可進一步用來產生其他計數功能，如先前所述。</span><span class="sxs-lookup"><span data-stu-id="ed356-154">These location-based features can be further used to generate additional count features as described earlier.</span></span> 

> [!TIP]
> <span data-ttu-id="ed356-155">您可以使用所選擇的語言，利用程式設計方式插入記錄。</span><span class="sxs-lookup"><span data-stu-id="ed356-155">You can programmatically insert the records using your language of choice.</span></span> <span data-ttu-id="ed356-156">您可能需要將資料插入區塊中，以改善寫入效率 ( [使用 Python 存取 SQLServer 的 HelloWorld 範例](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python))。</span><span class="sxs-lookup"><span data-stu-id="ed356-156">You may need to insert the data in chunks to improve write efficiency (for an example of how to do this using pyodbc, see [A HelloWorld sample to access SQLServer with python](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python)).</span></span> <span data-ttu-id="ed356-157">另一個替代方式是使用 [BCP 公用程式](https://msdn.microsoft.com/library/ms162802.aspx)在資料庫中插入資料</span><span class="sxs-lookup"><span data-stu-id="ed356-157">Another alternative is to insert data in the database using the [BCP utility](https://msdn.microsoft.com/library/ms162802.aspx).</span></span>
> 
> 

### <span data-ttu-id="ed356-158"><a name="sql-aml"></a>連接到 Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="ed356-158"><a name="sql-aml"></a>Connecting to Azure Machine Learning</span></span>
<span data-ttu-id="ed356-159">新產生的功能可當成資料行新增至現有資料表或儲存於新的資料表中，並與原始資料表加以聯結以進行機器學習服務。</span><span class="sxs-lookup"><span data-stu-id="ed356-159">The newly generated feature can be added as a column to an existing table or stored in a new table and joined with the original table for machine learning.</span></span> <span data-ttu-id="ed356-160">您可以使用 Azure Machine Learning 中的[匯入資料][import-data]模組來產生或存取特徵 (若已建立)，如下所示：</span><span class="sxs-lookup"><span data-stu-id="ed356-160">Features can be generated or accessed if already created, using the [Import Data][import-data] module in Azure Machine Learning as shown below:</span></span>

![azureml 讀取器][1] 

## <span data-ttu-id="ed356-162"><a name="python"></a>使用類似 Python 的程式設計語言</span><span class="sxs-lookup"><span data-stu-id="ed356-162"><a name="python"></a>Using a programming language like Python</span></span>
<span data-ttu-id="ed356-163">當資料位於 SQL Server 時，使用 Python 來瀏覽資料與產生特徵，類似於使用 Python 來處理 Azure Blob 中的資料，如[在資料科學環境中處理 Azure Blob 資料](machine-learning-data-science-process-data-blob.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="ed356-163">Using Python to explore data and generate features when the data is in SQL Server is similar to processing data in Azure blob using Python as documented in [Process Azure Blob data in your data science environment](machine-learning-data-science-process-data-blob.md).</span></span> <span data-ttu-id="ed356-164">資料必須從資料庫載入 Pandas 資料框架，然後就能進一步處理。</span><span class="sxs-lookup"><span data-stu-id="ed356-164">The data needs to be loaded from the database into a pandas data frame and then can be processed further.</span></span> <span data-ttu-id="ed356-165">我們將在本節中說明連接到資料庫以及將資料載入資料框架的程序。</span><span class="sxs-lookup"><span data-stu-id="ed356-165">We document the process of connecting to the database and loading the data into the data frame in this section.</span></span>

<span data-ttu-id="ed356-166">下列連接字串格式可用來使用 pyodbc (使用您的特定值來取代 servername、dbname、username 和 password)，從 Python 連接到 SQL Server 資料庫：</span><span class="sxs-lookup"><span data-stu-id="ed356-166">The following connection string format can be used to connect to a SQL Server database from Python using pyodbc (replace servername, dbname, username, and password with your specific values):</span></span>

    #Set up the SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

<span data-ttu-id="ed356-167">Python 中的 [Pandas 程式庫](http://pandas.pydata.org/) 提供一組豐富的資料結構和資料分析工具，可用來對 Python 程式設計進行資料操作。</span><span class="sxs-lookup"><span data-stu-id="ed356-167">The [Pandas library](http://pandas.pydata.org/) in Python provides a rich set of data structures and data analysis tools for data manipulation for Python programming.</span></span> <span data-ttu-id="ed356-168">下列程式碼會將從 SQL Server 資料庫傳回的結果讀取至 Pandas 資料框架：</span><span class="sxs-lookup"><span data-stu-id="ed356-168">The code below reads the results returned from a SQL Server database into a Pandas data frame:</span></span>

    # Query database and load the returned results in pandas data frame
    data_frame = pd.read_sql('''select <columnname1>, <cloumnname2>... from <tablename>''', conn)

<span data-ttu-id="ed356-169">現在您可以利用[在資料科學環境中處理 Azure Blob 資料](machine-learning-data-science-process-data-blob.md)一文中說明的方式來使用 Pandas 資料框架。</span><span class="sxs-lookup"><span data-stu-id="ed356-169">Now you can work with the Pandas data frame as covered in the article [Process Azure Blob data in your data science environment](machine-learning-data-science-process-data-blob.md).</span></span>

## <a name="azure-data-science-in-action-example"></a><span data-ttu-id="ed356-170">作用中的 Azure 資料科學範例</span><span class="sxs-lookup"><span data-stu-id="ed356-170">Azure Data Science in Action Example</span></span>
<span data-ttu-id="ed356-171">如需使用公用資料集之 Azure 資料科學程序的端對端逐步解說範例，請參閱 [作用中的 Azure 資料科學範例](machine-learning-data-science-process-sql-walkthrough.md)。</span><span class="sxs-lookup"><span data-stu-id="ed356-171">For an end-to-end walkthrough example of the Azure Data Science Process using a public dataset, see [Azure Data Science Process in Action](machine-learning-data-science-process-sql-walkthrough.md).</span></span>

[1]: ./media/machine-learning-data-science-process-sql-server-virtual-machine/reader_db_featurizedinput.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/

