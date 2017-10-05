---
title: "使用 SQL 和 Python 對 SQL Server 中的資料建立功能 | Microsoft Docs"
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
ms.openlocfilehash: f0ac2799e2d8f18b2dd5b633555bfca08a44ba27
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="create-features-for-data-in-sql-server-using-sql-and-python"></a><span data-ttu-id="3b1e7-103">使用 SQL 和 Python 對 SQL Server 中的資料建立功能</span><span class="sxs-lookup"><span data-stu-id="3b1e7-103">Create features for data in SQL Server using SQL and Python</span></span>
<span data-ttu-id="3b1e7-104">本文件說明如何針對儲存在 Azure 上的 SQL Server VM 中資料產生特徵，以協助演算法更有效率地從資料學習。</span><span class="sxs-lookup"><span data-stu-id="3b1e7-104">This document shows how to generate features for data stored in a SQL Server VM on Azure that help algorithms learn more efficiently from the data.</span></span> <span data-ttu-id="3b1e7-105">使用 SQL 或使用類似 Python 的程式設計語言都可以達到此目的，以下示範這兩者。</span><span class="sxs-lookup"><span data-stu-id="3b1e7-105">This can be done by using SQL or by using a programming language like Python, both of which are demonstrated here.</span></span>

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

<span data-ttu-id="3b1e7-106">這個 **功能表** 所連結的主題會說明如何在各種環境中建立資料的特徵。</span><span class="sxs-lookup"><span data-stu-id="3b1e7-106">This **menu** links to topics that describe how to create features for data in various environments.</span></span> <span data-ttu-id="3b1e7-107">此工作是 [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/)中的一個步驟。</span><span class="sxs-lookup"><span data-stu-id="3b1e7-107">This task is a step in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

> [!NOTE]
> <span data-ttu-id="3b1e7-108">如需實用範例，您可以參考 [NYC 計程車資料集](http://www.andresmh.com/nyctaxitrips/)，並參考標題為[使用 IPython Notebook 和 SQL Server 來處理有爭議的 NYC 資料](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb)的 IPNB，以進行端對端逐步解說。</span><span class="sxs-lookup"><span data-stu-id="3b1e7-108">For a practical example, you can consult the [NYC Taxi dataset](http://www.andresmh.com/nyctaxitrips/) and refer to the IPNB titled [NYC Data wrangling using IPython Notebook and SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) for an end-to-end walk-through.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="3b1e7-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="3b1e7-109">Prerequisites</span></span>
<span data-ttu-id="3b1e7-110">本文假設您已經：</span><span class="sxs-lookup"><span data-stu-id="3b1e7-110">This article assumes that you have:</span></span>

* <span data-ttu-id="3b1e7-111">建立 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="3b1e7-111">Created an Azure storage account.</span></span> <span data-ttu-id="3b1e7-112">如需指示，請參閱[建立 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="3b1e7-112">If you need instructions, see [Create an Azure Storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span></span>
* <span data-ttu-id="3b1e7-113">將資料儲存在 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="3b1e7-113">Stored your data in SQL Server.</span></span> <span data-ttu-id="3b1e7-114">如果還沒這麼做，請參閱 [移動資料至 Azure 機器學習的 Azure SQL Database](machine-learning-data-science-move-sql-azure.md) ，以取得如何移動資料到該處的指示。</span><span class="sxs-lookup"><span data-stu-id="3b1e7-114">If you have not, see [Move data to an Azure SQL Database for Azure Machine Learning](machine-learning-data-science-move-sql-azure.md) for instructions on how to move the data there.</span></span>

## <span data-ttu-id="3b1e7-115"><a name="sql-featuregen"></a>使用 SQL 的功能產生</span><span class="sxs-lookup"><span data-stu-id="3b1e7-115"><a name="sql-featuregen"></a>Feature Generation with SQL</span></span>
<span data-ttu-id="3b1e7-116">在本節中，我們將說明使用 SQL 產生功能的方式：</span><span class="sxs-lookup"><span data-stu-id="3b1e7-116">In this section, we describe ways of generating features using SQL:</span></span>  

1. [<span data-ttu-id="3b1e7-117">以計數為基礎的功能產生</span><span class="sxs-lookup"><span data-stu-id="3b1e7-117">Count based Feature Generation</span></span>](#sql-countfeature)
2. [<span data-ttu-id="3b1e7-118">分類收納功能產生</span><span class="sxs-lookup"><span data-stu-id="3b1e7-118">Binning Feature Generation</span></span>](#sql-binningfeature)
3. [<span data-ttu-id="3b1e7-119">從單一資料行衍生功能</span><span class="sxs-lookup"><span data-stu-id="3b1e7-119">Rolling out the features from a single column</span></span>](#sql-featurerollout)

> [!NOTE]
> <span data-ttu-id="3b1e7-120">一旦產生額外功能之後，就可以將它們當成資料行新增至現有的資料表，或是建立具有其他功能和主索引鍵的新資料表 (可與原始資料表聯結)。</span><span class="sxs-lookup"><span data-stu-id="3b1e7-120">Once you generate additional features, you can either add them as columns to the existing table or create a new table with the additional features and primary key, that can be joined with the original table.</span></span>
> 
> 

### <span data-ttu-id="3b1e7-121"><a name="sql-countfeature"></a>以計數為基礎的功能產生</span><span class="sxs-lookup"><span data-stu-id="3b1e7-121"><a name="sql-countfeature"></a>Count based Feature Generation</span></span>
<span data-ttu-id="3b1e7-122">本文件示範兩種產生計數功能的方法。</span><span class="sxs-lookup"><span data-stu-id="3b1e7-122">This document demonstrates two ways of generating count features.</span></span> <span data-ttu-id="3b1e7-123">第一種方法會使用條件式加總，而第二種方法會使用 'where' 子句。</span><span class="sxs-lookup"><span data-stu-id="3b1e7-123">The first method uses conditional sum and the second method uses the 'where\` clause.</span></span> <span data-ttu-id="3b1e7-124">這些接著可與原始資料表聯結 (使用主索引鍵資料行)，以具備計數功能及原始資料。</span><span class="sxs-lookup"><span data-stu-id="3b1e7-124">These can then be joined with the original table (using primary key columns) to have count features alongside the original data.</span></span>

    select <column_name1>,<column_name2>,<column_name3>, COUNT(*) as Count_Features from <tablename> group by <column_name1>,<column_name2>,<column_name3>

    select <column_name1>,<column_name2> , sum(1) as Count_Features from <tablename>
    where <column_name3> = '<some_value>' group by <column_name1>,<column_name2>

### <span data-ttu-id="3b1e7-125"><a name="sql-binningfeature"></a>分類收納功能產生</span><span class="sxs-lookup"><span data-stu-id="3b1e7-125"><a name="sql-binningfeature"></a>Binning Feature Generation</span></span>
<span data-ttu-id="3b1e7-126">下列範例將示範如何藉由分類收納 (使用 5 個分類收納組) 可改用來做為功能的數值資料行，來產生分類收納功能：</span><span class="sxs-lookup"><span data-stu-id="3b1e7-126">The following example shows how to generate binned features by binning (using 5 bins) a numerical column that can be used as a feature instead:</span></span>

    `SELECT <column_name>, NTILE(5) OVER (ORDER BY <column_name>) AS BinNumber from <tablename>`


### <span data-ttu-id="3b1e7-127"><a name="sql-featurerollout"></a>從單一資料行衍生功能</span><span class="sxs-lookup"><span data-stu-id="3b1e7-127"><a name="sql-featurerollout"></a>Rolling out the features from a single column</span></span>
<span data-ttu-id="3b1e7-128">本節示範如何在資料表中衍生單一資料行來產生額外功能。</span><span class="sxs-lookup"><span data-stu-id="3b1e7-128">In this section, we demonstrate how to roll-out a single column in a table to generate additional features.</span></span> <span data-ttu-id="3b1e7-129">此範例假設您正嘗試從中產生功能的資料表中具有緯度或經度資料行。</span><span class="sxs-lookup"><span data-stu-id="3b1e7-129">The example assumes that there is a latitude or longitude column in the table from which you are trying to generate features.</span></span>

<span data-ttu-id="3b1e7-130">以下是有關經緯度位置資料的簡短入門指南 (源自 stackoverflow `http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude`)。</span><span class="sxs-lookup"><span data-stu-id="3b1e7-130">Here is a brief primer on latitude/longitude location data (resourced from stackoverflow `http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude`).</span></span> <span data-ttu-id="3b1e7-131">這有助於您在將功能化位置欄位之前先行了解：</span><span class="sxs-lookup"><span data-stu-id="3b1e7-131">This is useful to understand before featurizing the location field:</span></span>

* <span data-ttu-id="3b1e7-132">正負號告訴我們是否位於地球的北方或南方、東方或西方。</span><span class="sxs-lookup"><span data-stu-id="3b1e7-132">The sign tells us whether we are north or south, east or west on the globe.</span></span>
* <span data-ttu-id="3b1e7-133">非零的數百個位數告訴我們使用的是經度，而不是緯度！</span><span class="sxs-lookup"><span data-stu-id="3b1e7-133">A nonzero hundreds digit tells us we're using longitude, not latitude!</span></span>
* <span data-ttu-id="3b1e7-134">數十個位數可提供大約 1,000 公里的位置。</span><span class="sxs-lookup"><span data-stu-id="3b1e7-134">The tens digit gives a position to about 1,000 kilometers.</span></span> <span data-ttu-id="3b1e7-135">它會為我們提供身處哪個大陸或海洋的實用資訊。</span><span class="sxs-lookup"><span data-stu-id="3b1e7-135">It gives us useful information about what continent or ocean we are on.</span></span>
* <span data-ttu-id="3b1e7-136">單位數 (一個十進位度數) 提供一個最多可達 111 公里 (60 海浬，大約 69 英哩) 的位置。</span><span class="sxs-lookup"><span data-stu-id="3b1e7-136">The units digit (one decimal degree) gives a position up to 111 kilometers (60 nautical miles, about 69 miles).</span></span> <span data-ttu-id="3b1e7-137">它會告知我們大致上位於哪一個大的州或國家/地區中。</span><span class="sxs-lookup"><span data-stu-id="3b1e7-137">It can tell us roughly what large state or country we are in.</span></span>
* <span data-ttu-id="3b1e7-138">第一個小數點最多可達 11.1 km：它能夠分辨某一個大型縣 (市) 的位置與鄰近的大型縣 (市)。</span><span class="sxs-lookup"><span data-stu-id="3b1e7-138">The first decimal place is worth up to 11.1 km: it can distinguish the position of one large city from a neighboring large city.</span></span>
* <span data-ttu-id="3b1e7-139">第二個小數位數最多可達 1.1 km：它可以將某一個村莊與下一個村莊分隔開來。</span><span class="sxs-lookup"><span data-stu-id="3b1e7-139">The second decimal place is worth up to 1.1 km: it can separate one village from the next.</span></span>
* <span data-ttu-id="3b1e7-140">第三個小數位數最多可達 110 m：它可以識別大型農場或學術機構校區。</span><span class="sxs-lookup"><span data-stu-id="3b1e7-140">The third decimal place is worth up to 110 m: it can identify a large agricultural field or institutional campus.</span></span>
* <span data-ttu-id="3b1e7-141">第四個小數位數最多可達 11 m：它可以識別某一塊土地。</span><span class="sxs-lookup"><span data-stu-id="3b1e7-141">The fourth decimal place is worth up to 11 m: it can identify a parcel of land.</span></span> <span data-ttu-id="3b1e7-142">它相當於未修正的 GPS 單位且無干擾的一般精確度。</span><span class="sxs-lookup"><span data-stu-id="3b1e7-142">It is comparable to the typical accuracy of an uncorrected GPS unit with no interference.</span></span>
* <span data-ttu-id="3b1e7-143">第五個小數位數最多可達 1.1 m：它會分辨彼此的樹狀結構。</span><span class="sxs-lookup"><span data-stu-id="3b1e7-143">The fifth decimal place is worth up to 1.1 m: it distinguish trees from each other.</span></span> <span data-ttu-id="3b1e7-144">您只能使用微分校正來達到此層級利用商業 GPS 單位所達到的精確度。</span><span class="sxs-lookup"><span data-stu-id="3b1e7-144">Accuracy to this level with commercial GPS units can only be achieved with differential correction.</span></span>
* <span data-ttu-id="3b1e7-145">第六個小數位數最多可達 0.11 m：您可以使用此項目來詳細配置結構，其適用於設計環境和建置道路。</span><span class="sxs-lookup"><span data-stu-id="3b1e7-145">The sixth decimal place is worth up to 0.11 m: you can use this for laying out structures in detail, for designing landscapes, building roads.</span></span> <span data-ttu-id="3b1e7-146">比起足以追蹤冰河和河流的移動，這應該是更好的方式。</span><span class="sxs-lookup"><span data-stu-id="3b1e7-146">It should be more than good enough for tracking movements of glaciers and rivers.</span></span> <span data-ttu-id="3b1e7-147">您可以採用含有 GPS 的精心度量 (例如，微分校正的 GPS) 來達成此項目。</span><span class="sxs-lookup"><span data-stu-id="3b1e7-147">This can be achieved by taking painstaking measures with GPS, such as differentially corrected GPS.</span></span>

<span data-ttu-id="3b1e7-148">您可以使用下列方式來將位置資訊功能化，以分隔出區域、位置及縣 (市) 資訊。</span><span class="sxs-lookup"><span data-stu-id="3b1e7-148">The location information can can be featurized as follows, separating out region, location and city information.</span></span> <span data-ttu-id="3b1e7-149">請注意，一次也可以呼叫 REST 端點，例如，可在 `https://msdn.microsoft.com/library/ff701710.aspx` 上取得的 Bing Maps API，以取得區域或學區資訊。</span><span class="sxs-lookup"><span data-stu-id="3b1e7-149">Note that once can also call a REST end point such as Bing Maps API available at `https://msdn.microsoft.com/library/ff701710.aspx` to get the region/district information.</span></span>

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

<span data-ttu-id="3b1e7-150">上述以位置為基礎的功能可進一步用來產生其他計數功能，如先前所述。</span><span class="sxs-lookup"><span data-stu-id="3b1e7-150">The above location based features can be further used to generate additional count features as described earlier.</span></span>

> [!TIP]
> <span data-ttu-id="3b1e7-151">您可以使用所選擇的語言，利用程式設計方式插入記錄。</span><span class="sxs-lookup"><span data-stu-id="3b1e7-151">You can programmatically insert the records using your language of choice.</span></span> <span data-ttu-id="3b1e7-152">您可能需要插入區塊中的資料以改善寫入效率 [在此處看看如何使用 pyodbc 來執行此動作的範例](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python)。</span><span class="sxs-lookup"><span data-stu-id="3b1e7-152">You may need to insert the data in chunks to improve write efficiency [Check out the example of how to do this using pyodbc here](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python).</span></span>
> <span data-ttu-id="3b1e7-153">另一個替代方式是使用 [BCP 公用程式](https://msdn.microsoft.com/library/ms162802.aspx)</span><span class="sxs-lookup"><span data-stu-id="3b1e7-153">Another alternative is to insert data in the database using [BCP utility](https://msdn.microsoft.com/library/ms162802.aspx)</span></span>
> 
> 

### <span data-ttu-id="3b1e7-154"><a name="sql-aml"></a>連接到 Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="3b1e7-154"><a name="sql-aml"></a>Connecting to Azure Machine Learning</span></span>
<span data-ttu-id="3b1e7-155">新產生的功能可當成資料行新增至現有資料表或儲存於新的資料表中，並與原始資料表加以聯結以進行機器學習服務。</span><span class="sxs-lookup"><span data-stu-id="3b1e7-155">The newly generated feature can be added as a column to an existing table or stored in a new table and joined with the original table for machine learning.</span></span> <span data-ttu-id="3b1e7-156">如果已經建立功能，就可以使用 Azure ML 中的 [匯入資料](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) 模組來產生或存取功能，如以下所示：</span><span class="sxs-lookup"><span data-stu-id="3b1e7-156">Features can be generated or accessed if already created, using the [Import Data](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) module in Azure ML as shown below:</span></span>

![azureml 讀取器](./media/machine-learning-data-science-process-sql-server-virtual-machine/reader_db_featurizedinput.png)

## <span data-ttu-id="3b1e7-158"><a name="python"></a>使用類似 Python 的程式設計語言</span><span class="sxs-lookup"><span data-stu-id="3b1e7-158"><a name="python"></a>Using a programming language like Python</span></span>
<span data-ttu-id="3b1e7-159">當資料位於 SQL Server 時，使用 Python 來產生功能，類似於使用 Python 來處理 Azure blob 中的資料，如 [在資料科學環境中處理 Azure Blob 資料](machine-learning-data-science-process-data-blob.md)文件所述。</span><span class="sxs-lookup"><span data-stu-id="3b1e7-159">Using Python to generate features when the data is in SQL Server is similar to processing data in Azure blob using Python as documented in [Process Azure Blob data in you data science environment](machine-learning-data-science-process-data-blob.md).</span></span> <span data-ttu-id="3b1e7-160">資料必須從資料庫載入 Pandas 資料框架，然後就能進一步處理。</span><span class="sxs-lookup"><span data-stu-id="3b1e7-160">The data needs to be loaded from the database into a pandas data frame and then can be processed further.</span></span> <span data-ttu-id="3b1e7-161">我們將在本節中說明連接到資料庫以及將資料載入資料框架的程序。</span><span class="sxs-lookup"><span data-stu-id="3b1e7-161">We document the process of connecting to the database and loading the data into the data frame in this section.</span></span>

<span data-ttu-id="3b1e7-162">下列連接字串格式可用來使用 pyodbc (使用您的特定值來取代伺服器名稱、dbname、使用者名稱和密碼)，從 Python 連接到 SQL Server 資料庫：</span><span class="sxs-lookup"><span data-stu-id="3b1e7-162">The following connection string format can be used to connect to a SQL Server database from Python using pyodbc (replace servername, dbname, username and password with your specific values):</span></span>

    #Set up the SQL Azure connection
    import pyodbc
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

<span data-ttu-id="3b1e7-163">Python 中的 [Pandas 程式庫](http://pandas.pydata.org/) 提供一組豐富的資料結構和資料分析工具，可用來對 Python 程式設計進行資料操作。</span><span class="sxs-lookup"><span data-stu-id="3b1e7-163">The [Pandas library](http://pandas.pydata.org/) in Python provides a rich set of data structures and data analysis tools for data manipulation for Python programming.</span></span> <span data-ttu-id="3b1e7-164">下列程式碼會將從 SQL Server 資料庫傳回的結果讀取至 Pandas 資料框架：</span><span class="sxs-lookup"><span data-stu-id="3b1e7-164">The code below reads the results returned from a SQL Server database into a Pandas data frame:</span></span>

    # Query database and load the returned results in pandas data frame
    data_frame = pd.read_sql('''select <columnname1>, <cloumnname2>... from <tablename>''', conn)

<span data-ttu-id="3b1e7-165">現在您可以利用 [使用 Panda 建立 Azure blob 儲存體資料功能](machine-learning-data-science-create-features-blob.md)主題中說明的方式來使用 Pandas 資料框架。</span><span class="sxs-lookup"><span data-stu-id="3b1e7-165">Now you can work with the Pandas data frame as covered in topics [Create features for Azure blob storage data using Panda](machine-learning-data-science-create-features-blob.md).</span></span>

