---
title: "在 Azure 上瀏覽 SQL Server 虛擬機器中的資料 | Microsoft Docs"
description: "如何瀏覽儲存在 Azure 上 SQL Server VM 中的資料。"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: ccbb3085-af9e-4ec2-9df2-15dcab261d05
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: a2be21ef15b9209db1e97150e0297558fa69a7be
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="explore-data-in-sql-server-virtual-machine-on-azure"></a><span data-ttu-id="f4302-103">在 Azure 上瀏覽 SQL Server 虛擬機器中的資料</span><span class="sxs-lookup"><span data-stu-id="f4302-103">Explore data in SQL Server Virtual Machine on Azure</span></span>
<span data-ttu-id="f4302-104">本文件涵蓋如何瀏覽儲存在 Azure 上 SQL Server VM 中的資料。</span><span class="sxs-lookup"><span data-stu-id="f4302-104">This document covers how to explore data that is stored in a SQL Server VM on Azure.</span></span> <span data-ttu-id="f4302-105">使用 SQL整理資料或使用 Python 這類程式設計語言，即可完成此動作。</span><span class="sxs-lookup"><span data-stu-id="f4302-105">This can be done by data wrangling using SQL or by using a programming language like Python.</span></span>

<span data-ttu-id="f4302-106">下列 **功能表** 所連結的主題會說明如何從各種不同的儲存體環境使用工具來瀏覽資料。</span><span class="sxs-lookup"><span data-stu-id="f4302-106">The following **menu** links to topics that describe how to use tools to explore data from various storage environments.</span></span> <span data-ttu-id="f4302-107">此工作是 Cortana 分析程序 (CAP) 中的一個步驟。</span><span class="sxs-lookup"><span data-stu-id="f4302-107">This task is a step in the Cortana Analytics Process (CAP).</span></span>

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

> [!NOTE]
> <span data-ttu-id="f4302-108">本文件中的 SQL 陳述式範例假設資料位於 SQL Server 中。</span><span class="sxs-lookup"><span data-stu-id="f4302-108">The sample SQL statements in this document assume that data is in SQL Server.</span></span> <span data-ttu-id="f4302-109">如果不是，請參閱雲端資料科學程序圖，以了解如何將資料移至 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="f4302-109">If it isn't, refer to the cloud data science process map to learn how to move your data to SQL Server.</span></span>
> 
> 

## <span data-ttu-id="f4302-110"><a name="sql-dataexploration"></a>使用 SQL 指令碼瀏覽 SQL 資料</span><span class="sxs-lookup"><span data-stu-id="f4302-110"><a name="sql-dataexploration"></a>Explore SQL data with SQL scripts</span></span>
<span data-ttu-id="f4302-111">以下是數個 SQL 指令碼範例，可用來探索儲存於 SQL Server 中的資料。</span><span class="sxs-lookup"><span data-stu-id="f4302-111">Here are a few sample SQL scripts that can be used to explore data stores in SQL Server.</span></span>

1. <span data-ttu-id="f4302-112">取得每天的觀察計數</span><span class="sxs-lookup"><span data-stu-id="f4302-112">Get the count of observations per day</span></span>
   
    `SELECT CONVERT(date, <date_columnname>) as date, count(*) as c from <tablename> group by CONVERT(date, <date_columnname>)` 
2. <span data-ttu-id="f4302-113">取得類別資料行中的層級</span><span class="sxs-lookup"><span data-stu-id="f4302-113">Get the levels in a categorical column</span></span>
   
    `select  distinct <column_name> from <databasename>`
3. <span data-ttu-id="f4302-114">取得兩個類別資料行組合中的層級數目</span><span class="sxs-lookup"><span data-stu-id="f4302-114">Get the number of levels in combination of two categorical columns</span></span> 
   
    `select <column_a>, <column_b>,count(*) from <tablename> group by <column_a>, <column_b>`
4. <span data-ttu-id="f4302-115">取得數值資料行的分佈 </span><span class="sxs-lookup"><span data-stu-id="f4302-115">Get the distribution for numerical columns</span></span>
   
    `select <column_name>, count(*) from <tablename> group by <column_name>`

> [!NOTE]
> <span data-ttu-id="f4302-116">如需實用範例，您可以使用 [NYC 計程車資料集](http://www.andresmh.com/nyctaxitrips/)，並參考標題為[使用 IPython Notebook 和 SQL Server 來處理有爭議的 NYC 資料](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb)的 IPNB，以進行端對端逐步解說。</span><span class="sxs-lookup"><span data-stu-id="f4302-116">For a practical example, you can use the [NYC Taxi dataset](http://www.andresmh.com/nyctaxitrips/) and refer to the IPNB titled [NYC Data wrangling using IPython Notebook and SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) for an end-to-end walk-through.</span></span>
> 
> 

## <span data-ttu-id="f4302-117"><a name="python"></a>使用 Python 瀏覽 SQL 資料</span><span class="sxs-lookup"><span data-stu-id="f4302-117"><a name="python"></a>Explore SQL data with Python</span></span>
<span data-ttu-id="f4302-118">當資料位於 SQL Server 時，使用 Python 來瀏覽資料與產生特徵，類似於使用 Python 來處理 Azure Blob 中的資料，如 [在資料科學環境中處理 Azure Blob 資料](machine-learning-data-science-process-data-blob.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="f4302-118">Using Python to explore data and generate features when the data is in SQL Server is similar to processing data in Azure blob using Python, as documented in [Process Azure Blob data in your data science environment](machine-learning-data-science-process-data-blob.md).</span></span> <span data-ttu-id="f4302-119">資料必須從資料庫載入 Pandas 資料框架，然後就能進一步處理。</span><span class="sxs-lookup"><span data-stu-id="f4302-119">The data needs to be loaded from the database into a pandas DataFrame and then can be processed further.</span></span> <span data-ttu-id="f4302-120">我們將在本節中說明連接到資料庫以及將資料載入資料框架的程序。</span><span class="sxs-lookup"><span data-stu-id="f4302-120">We document the process of connecting to the database and loading the data into the DataFrame in this section.</span></span>

<span data-ttu-id="f4302-121">下列連接字串格式可用來使用 pyodbc (使用您的特定值來取代 servername、dbname、username 和 password)，從 Python 連接到 SQL Server 資料庫：</span><span class="sxs-lookup"><span data-stu-id="f4302-121">The following connection string format can be used to connect to a SQL Server database from Python using pyodbc (replace servername, dbname, username, and password with your specific values):</span></span>

    #Set up the SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

<span data-ttu-id="f4302-122">Python 中的 [Pandas 程式庫](http://pandas.pydata.org/) 提供一組豐富的資料結構和資料分析工具，可用來對 Python 程式設計進行資料操作。</span><span class="sxs-lookup"><span data-stu-id="f4302-122">The [Pandas library](http://pandas.pydata.org/) in Python provides a rich set of data structures and data analysis tools for data manipulation for Python programming.</span></span> <span data-ttu-id="f4302-123">下列程式碼會將從 SQL Server 資料庫傳回的結果讀取至 Pandas 資料框架：</span><span class="sxs-lookup"><span data-stu-id="f4302-123">The following code reads the results returned from a SQL Server database into a Pandas data frame:</span></span>

    # Query database and load the returned results in pandas data frame
    data_frame = pd.read_sql('''select <columnname1>, <cloumnname2>... from <tablename>''', conn)

<span data-ttu-id="f4302-124">現在您可以利用 [在資料科學環境中處理 Azure Blob 資料](machine-learning-data-science-process-data-blob.md)主題中說明的方式來使用 Pandas 資料框架。</span><span class="sxs-lookup"><span data-stu-id="f4302-124">Now you can work with the Pandas DataFrame as covered in the topic [Process Azure Blob data in your data science environment](machine-learning-data-science-process-data-blob.md).</span></span>

## <a name="cortana-analytics-process-in-action-example"></a><span data-ttu-id="f4302-125">Cortana 分析程序實務範例</span><span class="sxs-lookup"><span data-stu-id="f4302-125">Cortana Analytics Process in Action Example</span></span>
<span data-ttu-id="f4302-126">如需使用公用資料集進行 Cortana Analytics 程序的端對端逐步解說範例，請參閱 [Team Data Science Process 實務：使用 SQL Server](machine-learning-data-science-process-sql-walkthrough.md)。</span><span class="sxs-lookup"><span data-stu-id="f4302-126">For an end-to-end walkthrough example of the Cortana Analytics Process using a public dataset, see [The Team Data Science Process in action: using SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span></span>

