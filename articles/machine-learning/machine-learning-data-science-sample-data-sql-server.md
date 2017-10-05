---
title: "Azure 上的 SQL Server 取樣資料 | Microsoft Docs"
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
ms.openlocfilehash: 1bdcc7175dac325de1144d805e977264524b3fbc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <span data-ttu-id="1affb-103"><a name="heading"></a>在 Azure 上 SQL Server 中進行資料取樣</span><span class="sxs-lookup"><span data-stu-id="1affb-103"><a name="heading"></a>Sample data in SQL Server on Azure</span></span>
<span data-ttu-id="1affb-104">本文件顯示如何使用 SQL 或 Python 程式設計語言，對儲存在 Azure 上之 SQL Server 中的資料進行取樣。</span><span class="sxs-lookup"><span data-stu-id="1affb-104">This document shows how to sample data stored in SQL Server on Azure using either SQL or the Python programming language.</span></span> <span data-ttu-id="1affb-105">也示範如何透過將取樣的資料儲存到檔案，讓取樣資料移動到 Azure Machine Learning、將取樣的資料上傳至 Azure blob，然後將其讀入 Azure Machine Learning Studio。</span><span class="sxs-lookup"><span data-stu-id="1affb-105">It also shows how to move sampled data into Azure Machine Learning by saving it to a file, uploading it to an Azure blob, and then reading it into Azure Machine Learning Studio.</span></span>

<span data-ttu-id="1affb-106">Python 取樣使用 [pyodbc](https://code.google.com/p/pyodbc/) ODBC 程式庫來連接到 Azure 上的 SQL Server 以及 [Pandas](http://pandas.pydata.org/) 程式庫來進行取樣。</span><span class="sxs-lookup"><span data-stu-id="1affb-106">The Python sampling uses the [pyodbc](https://code.google.com/p/pyodbc/) ODBC library to connect to SQL Server on Azure and the [Pandas](http://pandas.pydata.org/) library to do the sampling.</span></span>

> [!NOTE]
> <span data-ttu-id="1affb-107">本文件中的 SQL 程式碼範例假設資料位於 Azure 上的 SQL Server 中。</span><span class="sxs-lookup"><span data-stu-id="1affb-107">The sample SQL code in this document assumes that the data is in a SQL Server on Azure.</span></span> <span data-ttu-id="1affb-108">如果資料不在其中，請參閱 [移動資料至 Azure 虛擬機器上的 SQL Server](machine-learning-data-science-move-sql-server-virtual-machine.md) 主題，以取得如何將資料移至 Azure 上 SQL Server 的指示。</span><span class="sxs-lookup"><span data-stu-id="1affb-108">If it is not, please refer to [Move data to SQL Server on Azure](machine-learning-data-science-move-sql-server-virtual-machine.md) topic for instructions on how to move your data to SQL Server on Azure.</span></span>
> 
> 

<span data-ttu-id="1affb-109">以下**功能表**所連結的主題會說明如何從各種不同儲存體環境進行資料取樣。</span><span class="sxs-lookup"><span data-stu-id="1affb-109">The following **menu** links to topics that describe how to sample data from various storage environments.</span></span> 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

<span data-ttu-id="1affb-110">**為何要對您的資料進行取樣？**</span><span class="sxs-lookup"><span data-stu-id="1affb-110">**Why sample your data?**</span></span>
<span data-ttu-id="1affb-111">如果您規劃分析的資料集很龐大，通常最好是對資料進行向下取樣，將資料縮減為更小但具代表性且更容易管理的大小。</span><span class="sxs-lookup"><span data-stu-id="1affb-111">If the dataset you plan to analyze is large, it's usually a good idea to down-sample the data to reduce it to a smaller but representative and more manageable size.</span></span> <span data-ttu-id="1affb-112">這有助於資料了解、探索和功能工程。</span><span class="sxs-lookup"><span data-stu-id="1affb-112">This facilitates data understanding, exploration, and feature engineering.</span></span> <span data-ttu-id="1affb-113">它在 [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) 中扮演的角色是，能夠快速建立資料處理函式與機器學習服務模型的原型。</span><span class="sxs-lookup"><span data-stu-id="1affb-113">Its role in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) is to enable fast prototyping of the data processing functions and machine learning models.</span></span>

<span data-ttu-id="1affb-114">這個取樣工作是 [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/)中的一個步驟。</span><span class="sxs-lookup"><span data-stu-id="1affb-114">This sampling task is a step in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <span data-ttu-id="1affb-115"><a name="SQL"></a>使用 SQL</span><span class="sxs-lookup"><span data-stu-id="1affb-115"><a name="SQL"></a>Using SQL</span></span>
<span data-ttu-id="1affb-116">本節將說明使用 SQL，對資料庫中的資料執行簡單隨機取樣的數個方法。</span><span class="sxs-lookup"><span data-stu-id="1affb-116">This section describes several methods using SQL to perform simple random sampling against the data in the database.</span></span> <span data-ttu-id="1affb-117">請根據資料大小及其分佈來選擇方法。</span><span class="sxs-lookup"><span data-stu-id="1affb-117">Please choose a method based on your data size and its distribution.</span></span>

<span data-ttu-id="1affb-118">以下兩個項目示範如何在 SQL Server 中使用 newid 進行取樣。</span><span class="sxs-lookup"><span data-stu-id="1affb-118">The two items below show how to use newid in SQL Server to perform the sampling.</span></span> <span data-ttu-id="1affb-119">您選擇的方法取決於想要的隨機取樣程度 (程式碼範例底下的 pk_id 已假設為自動產生的主索引鍵)。</span><span class="sxs-lookup"><span data-stu-id="1affb-119">The method you choose depends on how random you want the sample to be (pk_id in the sample code below is assumed to be an auto-generated primary key).</span></span>

1. <span data-ttu-id="1affb-120">較不嚴格的隨機取樣</span><span class="sxs-lookup"><span data-stu-id="1affb-120">Less strict random sample</span></span>
   
        select  * from <table_name> where <primary_key> in 
        (select top 10 percent <primary_key> from <table_name> order by newid())
2. <span data-ttu-id="1affb-121">更隨機範例</span><span class="sxs-lookup"><span data-stu-id="1affb-121">More random sample</span></span> 
   
        SELECT * FROM <table_name>
        WHERE 0.1 >= CAST(CHECKSUM(NEWID(), <primary_key>) & 0x7fffffff AS float)/ CAST (0x7fffffff AS int)

<span data-ttu-id="1affb-122">Tablesample 可用來進行取樣及示範，如下所示。</span><span class="sxs-lookup"><span data-stu-id="1affb-122">Tablesample can be used for sampling as well as demonstrated below.</span></span> <span data-ttu-id="1affb-123">如果資料大小很大 (假設不同頁面上的資料不會相互關聯)，而且要讓查詢在合理時間內完成，這可能是較好的方法。</span><span class="sxs-lookup"><span data-stu-id="1affb-123">This may be a better approach if your data size is large (assuming that data on different pages is not correlated) and for the query to complete in a reasonable time.</span></span>

    SELECT *
    FROM <table_name> 
    TABLESAMPLE (10 PERCENT)

> [!NOTE]
> <span data-ttu-id="1affb-124">您可以藉由將這個取樣的資料儲存於新的資料表中，從該資料中探索並產生功能</span><span class="sxs-lookup"><span data-stu-id="1affb-124">You can explore and generate features from this sampled data by storing it in a new table</span></span>
> 
> 

### <span data-ttu-id="1affb-125"><a name="sql-aml"></a>連接到 Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="1affb-125"><a name="sql-aml"></a>Connecting to Azure Machine Learning</span></span>
<span data-ttu-id="1affb-126">您可以在 Azure Machine Learning [匯入資料][import-data]模組中直接使用上述取樣查詢，來進行即時資料縮小取樣，然後帶入 Azure Machine Learning 實驗中。</span><span class="sxs-lookup"><span data-stu-id="1affb-126">You can directly  use the sample queries above in the Azure Machine Learning [Import Data][import-data] module to down-sample the data on the fly and bring it into an Azure Machine Learning experiment.</span></span> <span data-ttu-id="1affb-127">使用讀取程式模組讀取取樣資料的螢幕擷取畫面如下所示：</span><span class="sxs-lookup"><span data-stu-id="1affb-127">A screen shot of using the reader module to read the sampled data is shown below:</span></span>

![讀取器 SQL][1]

## <span data-ttu-id="1affb-129"><a name="python"></a>使用 Python 程式設計語言</span><span class="sxs-lookup"><span data-stu-id="1affb-129"><a name="python"></a>Using the Python programming language</span></span>
<span data-ttu-id="1affb-130">本節示範如何使用 [pyodbc 程式庫](https://code.google.com/p/pyodbc/) 來建立連線至 Python 中 SQL Server 資料庫的 ODBC。</span><span class="sxs-lookup"><span data-stu-id="1affb-130">This section demonstrates using the [pyodbc library](https://code.google.com/p/pyodbc/) to establish an ODBC connect to a SQL server database in Python.</span></span> <span data-ttu-id="1affb-131">資料庫連接字串如下：(使用您的設定來取代伺服器名稱、資料庫名稱、使用者名稱和密碼)：</span><span class="sxs-lookup"><span data-stu-id="1affb-131">The database connection string is as follows: (replace servername, dbname, username and password with your configuration):</span></span>

    #Set up the SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

<span data-ttu-id="1affb-132">Python 中的 [Pandas](http://pandas.pydata.org/) 程式庫提供一組豐富的資料結構和資料分析工具，可用來對 Python 程式設計進行資料操作。</span><span class="sxs-lookup"><span data-stu-id="1affb-132">The [Pandas](http://pandas.pydata.org/) library in Python provides a rich set of data structures and data analysis tools for data manipulation for Python programming.</span></span> <span data-ttu-id="1affb-133">下列程式碼會從 Azure SQL 資料庫中的資料表，將 0.1% 的資料樣本讀取至 Pandas 資料中：</span><span class="sxs-lookup"><span data-stu-id="1affb-133">The code below reads a 0.1% sample of the data from a table in Azure SQL database into a Pandas data :</span></span>

    import pandas as pd

    # Query database and load the returned results in pandas data frame
    data_frame = pd.read_sql('''select column1, cloumn2... from <table_name> tablesample (0.1 percent)''', conn)

<span data-ttu-id="1affb-134">您現在可以在 Pandas 資料框架中使用取樣資料。</span><span class="sxs-lookup"><span data-stu-id="1affb-134">You can now work with the sampled data in the Pandas data frame.</span></span> 

### <span data-ttu-id="1affb-135"><a name="python-aml"></a>連接到 Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="1affb-135"><a name="python-aml"></a>Connecting to Azure Machine Learning</span></span>
<span data-ttu-id="1affb-136">您可以使用下列程式碼範例，將向下取樣的資料儲存至檔案，並將它上傳至 Azure Blob。</span><span class="sxs-lookup"><span data-stu-id="1affb-136">You can use the following sample code to save the down-sampled data to a file and upload it to an Azure blob.</span></span> <span data-ttu-id="1affb-137">使用[匯入資料][import-data]模組即可將 Blob 中的資料直接讀取到「Azure Machine Learning 實驗」中。</span><span class="sxs-lookup"><span data-stu-id="1affb-137">The data in the blob can be directly read into an Azure Machine Learning Experiment using the [Import Data][import-data] module.</span></span> <span data-ttu-id="1affb-138">步驟如下：</span><span class="sxs-lookup"><span data-stu-id="1affb-138">The steps are as follows:</span></span> 

1. <span data-ttu-id="1affb-139">將 Pandas 資料框架寫入本機檔案</span><span class="sxs-lookup"><span data-stu-id="1affb-139">Write the pandas data frame to a local file</span></span>
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. <span data-ttu-id="1affb-140">將本機檔案上傳至 Azure Blob</span><span class="sxs-lookup"><span data-stu-id="1affb-140">Upload local file to Azure blob</span></span>
   
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
3. <span data-ttu-id="1affb-141">使用 Azure Machine Learning [匯入資料][import-data]模組從 Azure Blob 讀取資料，如以下螢幕擷取畫面所示：</span><span class="sxs-lookup"><span data-stu-id="1affb-141">Read data from Azure blob using Azure Machine Learning [Import Data][import-data] module as shown in the screen grab below:</span></span>

![讀取器 Blob][2]

## <a name="the-team-data-science-process-in-action-example"></a><span data-ttu-id="1affb-143">Team Data Science Process 實務範例</span><span class="sxs-lookup"><span data-stu-id="1affb-143">The Team Data Science Process in Action example</span></span>
<span data-ttu-id="1affb-144">如需使用公用資料集進行 Team Data Science Process 的端對端逐步解說範例，請參閱 [Team Data Science Process 實務：使用 SQL Server](machine-learning-data-science-process-sql-walkthrough.md)。</span><span class="sxs-lookup"><span data-stu-id="1affb-144">For an end-to-end walkthrough example of the Team Data Science Process a using a public dataset, see [Team Data Science Process in Action: using SQL Sever](machine-learning-data-science-process-sql-walkthrough.md).</span></span>

[1]: ./media/machine-learning-data-science-sample-sql-server-virtual-machine/reader_database.png
[2]: ./media/machine-learning-data-science-sample-sql-server-virtual-machine/reader_blob.png

[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
