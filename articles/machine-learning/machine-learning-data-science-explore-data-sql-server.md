---
title: "aaaExplore 資料在 SQL Server 虛擬機器在 Azure 上 |Microsoft 文件"
description: "如何儲存在 Azure 上的 SQL Server VM 的 tooexplore 資料。"
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
ms.openlocfilehash: fcc449fc0d0e49be9b673cfb2de347cf44804017
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="explore-data-in-sql-server-virtual-machine-on-azure"></a><span data-ttu-id="513c5-103">在 Azure 上瀏覽 SQL Server 虛擬機器中的資料</span><span class="sxs-lookup"><span data-stu-id="513c5-103">Explore data in SQL Server Virtual Machine on Azure</span></span>
<span data-ttu-id="513c5-104">本文件涵蓋如何 tooexplore 資料儲存在 Azure 上的 SQL Server VM。</span><span class="sxs-lookup"><span data-stu-id="513c5-104">This document covers how tooexplore data that is stored in a SQL Server VM on Azure.</span></span> <span data-ttu-id="513c5-105">使用 SQL整理資料或使用 Python 這類程式設計語言，即可完成此動作。</span><span class="sxs-lookup"><span data-stu-id="513c5-105">This can be done by data wrangling using SQL or by using a programming language like Python.</span></span>

<span data-ttu-id="513c5-106">hello 下列**功能表**連結 tootopics 描述 toouse 工具 tooexplore 資料，從不同的儲存體環境的方式。</span><span class="sxs-lookup"><span data-stu-id="513c5-106">hello following **menu** links tootopics that describe how toouse tools tooexplore data from various storage environments.</span></span> <span data-ttu-id="513c5-107">這項工作是 hello Cortana 分析程序 (CAP) 的步驟。</span><span class="sxs-lookup"><span data-stu-id="513c5-107">This task is a step in hello Cortana Analytics Process (CAP).</span></span>

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

> [!NOTE]
> <span data-ttu-id="513c5-108">這份文件中的 hello 範例 SQL 陳述式會假設資料是在 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="513c5-108">hello sample SQL statements in this document assume that data is in SQL Server.</span></span> <span data-ttu-id="513c5-109">如果沒有，請參閱 toohello 雲端資料科學程序對應 toolearn 如何 toomove 您資料 tooSQL 伺服器。</span><span class="sxs-lookup"><span data-stu-id="513c5-109">If it isn't, refer toohello cloud data science process map toolearn how toomove your data tooSQL Server.</span></span>
> 
> 

## <span data-ttu-id="513c5-110"><a name="sql-dataexploration"></a>使用 SQL 指令碼瀏覽 SQL 資料</span><span class="sxs-lookup"><span data-stu-id="513c5-110"><a name="sql-dataexploration"></a>Explore SQL data with SQL scripts</span></span>
<span data-ttu-id="513c5-111">以下是一些範例 SQL 指令碼可能是 SQL Server 中的使用的 tooexplore 資料存放區。</span><span class="sxs-lookup"><span data-stu-id="513c5-111">Here are a few sample SQL scripts that can be used tooexplore data stores in SQL Server.</span></span>

1. <span data-ttu-id="513c5-112">取得每日的觀察值的 hello 計數</span><span class="sxs-lookup"><span data-stu-id="513c5-112">Get hello count of observations per day</span></span>
   
    `SELECT CONVERT(date, <date_columnname>) as date, count(*) as c from <tablename> group by CONVERT(date, <date_columnname>)` 
2. <span data-ttu-id="513c5-113">取得類別的資料行中的 hello 層級</span><span class="sxs-lookup"><span data-stu-id="513c5-113">Get hello levels in a categorical column</span></span>
   
    `select  distinct <column_name> from <databasename>`
3. <span data-ttu-id="513c5-114">取得 hello 層級數目的兩個類別資料行組合中</span><span class="sxs-lookup"><span data-stu-id="513c5-114">Get hello number of levels in combination of two categorical columns</span></span> 
   
    `select <column_a>, <column_b>,count(*) from <tablename> group by <column_a>, <column_b>`
4. <span data-ttu-id="513c5-115">取得數值資料行的 hello 發佈</span><span class="sxs-lookup"><span data-stu-id="513c5-115">Get hello distribution for numerical columns</span></span>
   
    `select <column_name>, count(*) from <tablename> group by <column_name>`

> [!NOTE]
> <span data-ttu-id="513c5-116">如需實用範例，您可以使用 hello [NYC 計程車資料集](http://www.andresmh.com/nyctaxitrips/)和參考 toohello IPNB 標題為[NYC 資料 wrangling 使用 IPython 筆記型電腦和 SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb)的端對端逐步解說。</span><span class="sxs-lookup"><span data-stu-id="513c5-116">For a practical example, you can use hello [NYC Taxi dataset](http://www.andresmh.com/nyctaxitrips/) and refer toohello IPNB titled [NYC Data wrangling using IPython Notebook and SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) for an end-to-end walk-through.</span></span>
> 
> 

## <span data-ttu-id="513c5-117"><a name="python"></a>使用 Python 瀏覽 SQL 資料</span><span class="sxs-lookup"><span data-stu-id="513c5-117"><a name="python"></a>Explore SQL data with Python</span></span>
<span data-ttu-id="513c5-118">使用 Python tooexplore 資料，並產生功能，資料是 SQL Server 中的 hello 類似 tooprocessing 資料時使用 Python，Azure blob 中所述[資料科學環境中的程序的 Azure Blob 資料](machine-learning-data-science-process-data-blob.md)。</span><span class="sxs-lookup"><span data-stu-id="513c5-118">Using Python tooexplore data and generate features when hello data is in SQL Server is similar tooprocessing data in Azure blob using Python, as documented in [Process Azure Blob data in your data science environment](machine-learning-data-science-process-data-blob.md).</span></span> <span data-ttu-id="513c5-119">hello 資料需要 toobe hello 資料庫載入熊資料框架，然後可以進一步處理。</span><span class="sxs-lookup"><span data-stu-id="513c5-119">hello data needs toobe loaded from hello database into a pandas DataFrame and then can be processed further.</span></span> <span data-ttu-id="513c5-120">我們的文件連接 toohello 資料庫以及 hello 資料載入 hello 本節中的資料框架的 hello 程的序。</span><span class="sxs-lookup"><span data-stu-id="513c5-120">We document hello process of connecting toohello database and loading hello data into hello DataFrame in this section.</span></span>

<span data-ttu-id="513c5-121">下列連接字串格式的 hello 可以是使用的 tooconnect tooa SQL Server 資料庫，來自 Python 使用 pyodbc （取代 servername、 dbname、 username 和 password 的特定值）：</span><span class="sxs-lookup"><span data-stu-id="513c5-121">hello following connection string format can be used tooconnect tooa SQL Server database from Python using pyodbc (replace servername, dbname, username, and password with your specific values):</span></span>

    #Set up hello SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

<span data-ttu-id="513c5-122">hello[熊程式庫](http://pandas.pydata.org/)Python 中提供一組豐富的資料結構和資料分析工具的 Python 程式設計資料操作。</span><span class="sxs-lookup"><span data-stu-id="513c5-122">hello [Pandas library](http://pandas.pydata.org/) in Python provides a rich set of data structures and data analysis tools for data manipulation for Python programming.</span></span> <span data-ttu-id="513c5-123">hello 下列程式碼會讀取從 SQL Server 資料庫傳回至熊資料框架的 hello 結果：</span><span class="sxs-lookup"><span data-stu-id="513c5-123">hello following code reads hello results returned from a SQL Server database into a Pandas data frame:</span></span>

    # Query database and load hello returned results in pandas data frame
    data_frame = pd.read_sql('''select <columnname1>, <cloumnname2>... from <tablename>''', conn)

<span data-ttu-id="513c5-124">現在您可以在 hello 主題涵蓋與 hello 熊資料框架[資料科學環境中的程序的 Azure Blob 資料](machine-learning-data-science-process-data-blob.md)。</span><span class="sxs-lookup"><span data-stu-id="513c5-124">Now you can work with hello Pandas DataFrame as covered in hello topic [Process Azure Blob data in your data science environment](machine-learning-data-science-process-data-blob.md).</span></span>

## <a name="cortana-analytics-process-in-action-example"></a><span data-ttu-id="513c5-125">Cortana 分析程序實務範例</span><span class="sxs-lookup"><span data-stu-id="513c5-125">Cortana Analytics Process in Action Example</span></span>
<span data-ttu-id="513c5-126">如需端對端逐步解說的範例 hello Cortana 分析程序，使用公用的資料集，請參閱[hello 動作中的資料科學的小組流程： 使用 SQL Server](machine-learning-data-science-process-sql-walkthrough.md)。</span><span class="sxs-lookup"><span data-stu-id="513c5-126">For an end-to-end walkthrough example of hello Cortana Analytics Process using a public dataset, see [hello Team Data Science Process in action: using SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span></span>

