---
title: "在 Azure 上的 SQL Server 中的資料 aaaSample |Microsoft 文件"
description: "Azure 上的 SQL Server 取樣資料"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 33c030d4-5cca-4cc9-99d7-2bd13a3926af
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: fashah;garye;bradsev
ms.openlocfilehash: dc7f9529c771f6deb633775557e64a04b774f5b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="3f7d4-103"><a name="heading"></a>在 Azure 上 SQL Server 中進行資料取樣</span><span class="sxs-lookup"><span data-stu-id="3f7d4-103"><a name="heading"></a>Sample data in SQL Server on Azure</span></span>
<span data-ttu-id="3f7d4-104">本文件示範 toosample 資料如何儲存在 Azure 上的 SQL Server 使用 SQL 或 hello Python 程式設計語言。</span><span class="sxs-lookup"><span data-stu-id="3f7d4-104">This document shows how toosample data stored in SQL Server on Azure using either SQL or hello Python programming language.</span></span> <span data-ttu-id="3f7d4-105">它也會示範如何 toomove 取樣資料到 Azure Machine Learning 儲存 tooa 檔案，將資料上傳，藉以 tooan 的 Azure blob，然後再讀取它到 Azure Machine Learning Studio。</span><span class="sxs-lookup"><span data-stu-id="3f7d4-105">It also shows how toomove sampled data into Azure Machine Learning by saving it tooa file, uploading it tooan Azure blob, and then reading it into Azure Machine Learning Studio.</span></span>

<span data-ttu-id="3f7d4-106">hello Python 取樣會針對使用 hello [pyodbc](https://code.google.com/p/pyodbc/) ODBC 程式庫 tooconnect tooSQL 伺服器，Azure 並 hello[熊](http://pandas.pydata.org/)文件庫 toodo hello 取樣。</span><span class="sxs-lookup"><span data-stu-id="3f7d4-106">hello Python sampling uses hello [pyodbc](https://code.google.com/p/pyodbc/) ODBC library tooconnect tooSQL Server on Azure and hello [Pandas](http://pandas.pydata.org/) library toodo hello sampling.</span></span>

> [!NOTE]
> <span data-ttu-id="3f7d4-107">本文件中的 hello 範例 SQL 程式碼會假設該資料是在 Azure 上的 SQL Server 中的 hello。</span><span class="sxs-lookup"><span data-stu-id="3f7d4-107">hello sample SQL code in this document assumes that hello data is in a SQL Server on Azure.</span></span> <span data-ttu-id="3f7d4-108">如果不存在，請參閱太[移動資料 tooSQL 伺服器在 Azure 上](machine-learning-data-science-move-sql-server-virtual-machine.md)主題的指示 toomove 您資料 tooSQL 在 Azure 上的伺服器。</span><span class="sxs-lookup"><span data-stu-id="3f7d4-108">If it is not, please refer too[Move data tooSQL Server on Azure](machine-learning-data-science-move-sql-server-virtual-machine.md) topic for instructions on how toomove your data tooSQL Server on Azure.</span></span>
> 
> 

<span data-ttu-id="3f7d4-109">hello 下列**功能表**連結 tootopics 描述如何從各種不同的儲存體環境 toosample 資料。</span><span class="sxs-lookup"><span data-stu-id="3f7d4-109">hello following **menu** links tootopics that describe how toosample data from various storage environments.</span></span> 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

<span data-ttu-id="3f7d4-110">**為何要對您的資料進行取樣？**</span><span class="sxs-lookup"><span data-stu-id="3f7d4-110">**Why sample your data?**</span></span>
<span data-ttu-id="3f7d4-111">如果您計劃 tooanalyze hello 資料集很大，它通常是個不錯的主意 toodown 範例 hello 資料 tooreduce 它 tooa 小型但具代表性且更容易管理的大小。</span><span class="sxs-lookup"><span data-stu-id="3f7d4-111">If hello dataset you plan tooanalyze is large, it's usually a good idea toodown-sample hello data tooreduce it tooa smaller but representative and more manageable size.</span></span> <span data-ttu-id="3f7d4-112">這有助於資料了解、探索和功能工程。</span><span class="sxs-lookup"><span data-stu-id="3f7d4-112">This facilitates data understanding, exploration, and feature engineering.</span></span> <span data-ttu-id="3f7d4-113">其角色在 hello[小組資料科學程序 (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/)是 tooenable 快速原型化的 hello 資料處理函式和機器學習模型。</span><span class="sxs-lookup"><span data-stu-id="3f7d4-113">Its role in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) is tooenable fast prototyping of hello data processing functions and machine learning models.</span></span>

<span data-ttu-id="3f7d4-114">此取樣工作是在 hello 步驟[小組資料科學程序 (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/)。</span><span class="sxs-lookup"><span data-stu-id="3f7d4-114">This sampling task is a step in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <span data-ttu-id="3f7d4-115"><a name="SQL"></a>使用 SQL</span><span class="sxs-lookup"><span data-stu-id="3f7d4-115"><a name="SQL"></a>Using SQL</span></span>
<span data-ttu-id="3f7d4-116">本章節描述使用 SQL tooperform 簡單的隨機取樣針對 hello 資料 hello 資料庫中的數種方法。</span><span class="sxs-lookup"><span data-stu-id="3f7d4-116">This section describes several methods using SQL tooperform simple random sampling against hello data in hello database.</span></span> <span data-ttu-id="3f7d4-117">請根據資料大小及其分佈來選擇方法。</span><span class="sxs-lookup"><span data-stu-id="3f7d4-117">Please choose a method based on your data size and its distribution.</span></span>

<span data-ttu-id="3f7d4-118">hello 兩個項目下方會顯示如何在 SQL Server tooperform toouse newid hello 取樣。</span><span class="sxs-lookup"><span data-stu-id="3f7d4-118">hello two items below show how toouse newid in SQL Server tooperform hello sampling.</span></span> <span data-ttu-id="3f7d4-119">hello 您選擇的方法取決於您想 hello 範例 toobe 隨機 （pk_id 下面的的 hello 範例程式碼會假設 toobe 自動產生的主索引鍵）。</span><span class="sxs-lookup"><span data-stu-id="3f7d4-119">hello method you choose depends on how random you want hello sample toobe (pk_id in hello sample code below is assumed toobe an auto-generated primary key).</span></span>

1. <span data-ttu-id="3f7d4-120">較不嚴格的隨機取樣</span><span class="sxs-lookup"><span data-stu-id="3f7d4-120">Less strict random sample</span></span>
   
        select  * from <table_name> where <primary_key> in 
        (select top 10 percent <primary_key> from <table_name> order by newid())
2. <span data-ttu-id="3f7d4-121">更隨機範例</span><span class="sxs-lookup"><span data-stu-id="3f7d4-121">More random sample</span></span> 
   
        SELECT * FROM <table_name>
        WHERE 0.1 >= CAST(CHECKSUM(NEWID(), <primary_key>) & 0x7fffffff AS float)/ CAST (0x7fffffff AS int)

<span data-ttu-id="3f7d4-122">Tablesample 可用來進行取樣及示範，如下所示。</span><span class="sxs-lookup"><span data-stu-id="3f7d4-122">Tablesample can be used for sampling as well as demonstrated below.</span></span> <span data-ttu-id="3f7d4-123">這可能在合理的時間，如果您的資料大小很大 （假設不同頁面上的資料不會相互關聯） 和 hello 查詢 toocomplete 是更好的方法。</span><span class="sxs-lookup"><span data-stu-id="3f7d4-123">This may be a better approach if your data size is large (assuming that data on different pages is not correlated) and for hello query toocomplete in a reasonable time.</span></span>

    SELECT *
    FROM <table_name> 
    TABLESAMPLE (10 PERCENT)

> [!NOTE]
> <span data-ttu-id="3f7d4-124">您可以藉由將這個取樣的資料儲存於新的資料表中，從該資料中探索並產生功能</span><span class="sxs-lookup"><span data-stu-id="3f7d4-124">You can explore and generate features from this sampled data by storing it in a new table</span></span>
> 
> 

### <span data-ttu-id="3f7d4-125"><a name="sql-aml"></a>連接 tooAzure 機器學習服務</span><span class="sxs-lookup"><span data-stu-id="3f7d4-125"><a name="sql-aml"></a>Connecting tooAzure Machine Learning</span></span>
<span data-ttu-id="3f7d4-126">您可以直接使用 hello Azure Machine Learning 中的 hello 上面的範例查詢[匯入資料][ import-data]模組 toodown 範例 hello 資料上 hello 飛和帶入 Azure 機器學習實驗。</span><span class="sxs-lookup"><span data-stu-id="3f7d4-126">You can directly  use hello sample queries above in hello Azure Machine Learning [Import Data][import-data] module toodown-sample hello data on hello fly and bring it into an Azure Machine Learning experiment.</span></span> <span data-ttu-id="3f7d4-127">使用 hello 讀取器模組 tooread hello 取樣資料的螢幕擷取畫面所示：</span><span class="sxs-lookup"><span data-stu-id="3f7d4-127">A screen shot of using hello reader module tooread hello sampled data is shown below:</span></span>

![讀取器 SQL][1]

## <span data-ttu-id="3f7d4-129"><a name="python"></a>使用 hello Python 程式設計語言</span><span class="sxs-lookup"><span data-stu-id="3f7d4-129"><a name="python"></a>Using hello Python programming language</span></span>
<span data-ttu-id="3f7d4-130">本節示範如何使用 hello [pyodbc 文件庫](https://code.google.com/p/pyodbc/)tooestablish ODBC 連接以 Python tooa SQL server 資料庫。</span><span class="sxs-lookup"><span data-stu-id="3f7d4-130">This section demonstrates using hello [pyodbc library](https://code.google.com/p/pyodbc/) tooestablish an ODBC connect tooa SQL server database in Python.</span></span> <span data-ttu-id="3f7d4-131">如下所示為 hello 資料庫連接字串: （servername、 dbname、 username 與 password 以取代您的設定）：</span><span class="sxs-lookup"><span data-stu-id="3f7d4-131">hello database connection string is as follows: (replace servername, dbname, username and password with your configuration):</span></span>

    #Set up hello SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

<span data-ttu-id="3f7d4-132">hello[熊](http://pandas.pydata.org/)Python 中的程式庫提供一組豐富的資料結構和資料分析工具的 Python 程式設計的資料操作。</span><span class="sxs-lookup"><span data-stu-id="3f7d4-132">hello [Pandas](http://pandas.pydata.org/) library in Python provides a rich set of data structures and data analysis tools for data manipulation for Python programming.</span></span> <span data-ttu-id="3f7d4-133">hello 的下列程式碼從 Azure SQL database 中的資料表將熊資料讀入 0.1 %hello 資料的範例：</span><span class="sxs-lookup"><span data-stu-id="3f7d4-133">hello code below reads a 0.1% sample of hello data from a table in Azure SQL database into a Pandas data :</span></span>

    import pandas as pd

    # Query database and load hello returned results in pandas data frame
    data_frame = pd.read_sql('''select column1, cloumn2... from <table_name> tablesample (0.1 percent)''', conn)

<span data-ttu-id="3f7d4-134">您現在可以使用 hello 熊資料框架中的 hello 取樣資料。</span><span class="sxs-lookup"><span data-stu-id="3f7d4-134">You can now work with hello sampled data in hello Pandas data frame.</span></span> 

### <span data-ttu-id="3f7d4-135"><a name="python-aml"></a>連接 tooAzure 機器學習服務</span><span class="sxs-lookup"><span data-stu-id="3f7d4-135"><a name="python-aml"></a>Connecting tooAzure Machine Learning</span></span>
<span data-ttu-id="3f7d4-136">您可以使用下列範例程式碼 toosave hello 下取樣資料 tooa 檔 hello，並將它上傳 tooan Azure blob。</span><span class="sxs-lookup"><span data-stu-id="3f7d4-136">You can use hello following sample code toosave hello down-sampled data tooa file and upload it tooan Azure blob.</span></span> <span data-ttu-id="3f7d4-137">hello hello blob 中可以直接讀取資料到 Azure 機器學習實驗中使用 hello[匯入資料][ import-data]模組。</span><span class="sxs-lookup"><span data-stu-id="3f7d4-137">hello data in hello blob can be directly read into an Azure Machine Learning Experiment using hello [Import Data][import-data] module.</span></span> <span data-ttu-id="3f7d4-138">hello 步驟如下所示：</span><span class="sxs-lookup"><span data-stu-id="3f7d4-138">hello steps are as follows:</span></span> 

1. <span data-ttu-id="3f7d4-139">寫入 hello 熊資料框架 tooa 本機檔案</span><span class="sxs-lookup"><span data-stu-id="3f7d4-139">Write hello pandas data frame tooa local file</span></span>
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. <span data-ttu-id="3f7d4-140">本機檔案 tooAzure blob 上傳</span><span class="sxs-lookup"><span data-stu-id="3f7d4-140">Upload local file tooAzure blob</span></span>
   
        from azure.storage import BlobService
        import tables
   
        STORAGEACCOUNTNAME= <storage_account_name>
        LOCALFILENAME= <local_file_name>
        STORAGEACCOUNTKEY= <storage_account_key>
        CONTAINERNAME= <container_name>
        BLOBNAME= <blob_name>
   
        output_blob_service=BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)    
        localfileprocessed = os.path.join(os.getcwd(),LOCALFILENAME) #assuming file is in current working directory
   
        try:
   
        #perform upload
        output_blob_service.put_block_blob_from_path(CONTAINERNAME,BLOBNAME,localfileprocessed)
   
        except:            
            print ("Something went wrong with uploading blob:"+BLOBNAME)
3. <span data-ttu-id="3f7d4-141">從使用 Azure Machine Learning 的 Azure blob 讀取資料[匯入資料][ import-data]模組 hello 螢幕擷取以下所示：</span><span class="sxs-lookup"><span data-stu-id="3f7d4-141">Read data from Azure blob using Azure Machine Learning [Import Data][import-data] module as shown in hello screen grab below:</span></span>

![讀取器 Blob][2]

## <a name="hello-team-data-science-process-in-action-example"></a><span data-ttu-id="3f7d4-143">在動作範例中的 hello 小組資料科學程序</span><span class="sxs-lookup"><span data-stu-id="3f7d4-143">hello Team Data Science Process in Action example</span></span>
<span data-ttu-id="3f7d4-144">Hello 小組資料科學程序的端對端逐步解說範例，使用公用的資料集，請參閱[小組的操作資料科學程序： 使用 SQL Sever](machine-learning-data-science-process-sql-walkthrough.md)。</span><span class="sxs-lookup"><span data-stu-id="3f7d4-144">For an end-to-end walkthrough example of hello Team Data Science Process a using a public dataset, see [Team Data Science Process in Action: using SQL Sever](machine-learning-data-science-process-sql-walkthrough.md).</span></span>

[1]: ./media/machine-learning-data-science-sample-sql-server-virtual-machine/reader_database.png
[2]: ./media/machine-learning-data-science-sample-sql-server-virtual-machine/reader_blob.png

[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
