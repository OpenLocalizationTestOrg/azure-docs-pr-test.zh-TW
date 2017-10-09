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
# <a name="heading"></a>在 Azure 上 SQL Server 中進行資料取樣
本文件示範 toosample 資料如何儲存在 Azure 上的 SQL Server 使用 SQL 或 hello Python 程式設計語言。 它也會示範如何 toomove 取樣資料到 Azure Machine Learning 儲存 tooa 檔案，將資料上傳，藉以 tooan 的 Azure blob，然後再讀取它到 Azure Machine Learning Studio。

hello Python 取樣會針對使用 hello [pyodbc](https://code.google.com/p/pyodbc/) ODBC 程式庫 tooconnect tooSQL 伺服器，Azure 並 hello[熊](http://pandas.pydata.org/)文件庫 toodo hello 取樣。

> [!NOTE]
> 本文件中的 hello 範例 SQL 程式碼會假設該資料是在 Azure 上的 SQL Server 中的 hello。 如果不存在，請參閱太[移動資料 tooSQL 伺服器在 Azure 上](machine-learning-data-science-move-sql-server-virtual-machine.md)主題的指示 toomove 您資料 tooSQL 在 Azure 上的伺服器。
> 
> 

hello 下列**功能表**連結 tootopics 描述如何從各種不同的儲存體環境 toosample 資料。 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

**為何要對您的資料進行取樣？**
如果您計劃 tooanalyze hello 資料集很大，它通常是個不錯的主意 toodown 範例 hello 資料 tooreduce 它 tooa 小型但具代表性且更容易管理的大小。 這有助於資料了解、探索和功能工程。 其角色在 hello[小組資料科學程序 (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/)是 tooenable 快速原型化的 hello 資料處理函式和機器學習模型。

此取樣工作是在 hello 步驟[小組資料科學程序 (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/)。

## <a name="SQL"></a>使用 SQL
本章節描述使用 SQL tooperform 簡單的隨機取樣針對 hello 資料 hello 資料庫中的數種方法。 請根據資料大小及其分佈來選擇方法。

hello 兩個項目下方會顯示如何在 SQL Server tooperform toouse newid hello 取樣。 hello 您選擇的方法取決於您想 hello 範例 toobe 隨機 （pk_id 下面的的 hello 範例程式碼會假設 toobe 自動產生的主索引鍵）。

1. 較不嚴格的隨機取樣
   
        select  * from <table_name> where <primary_key> in 
        (select top 10 percent <primary_key> from <table_name> order by newid())
2. 更隨機範例 
   
        SELECT * FROM <table_name>
        WHERE 0.1 >= CAST(CHECKSUM(NEWID(), <primary_key>) & 0x7fffffff AS float)/ CAST (0x7fffffff AS int)

Tablesample 可用來進行取樣及示範，如下所示。 這可能在合理的時間，如果您的資料大小很大 （假設不同頁面上的資料不會相互關聯） 和 hello 查詢 toocomplete 是更好的方法。

    SELECT *
    FROM <table_name> 
    TABLESAMPLE (10 PERCENT)

> [!NOTE]
> 您可以藉由將這個取樣的資料儲存於新的資料表中，從該資料中探索並產生功能
> 
> 

### <a name="sql-aml"></a>連接 tooAzure 機器學習服務
您可以直接使用 hello Azure Machine Learning 中的 hello 上面的範例查詢[匯入資料][ import-data]模組 toodown 範例 hello 資料上 hello 飛和帶入 Azure 機器學習實驗。 使用 hello 讀取器模組 tooread hello 取樣資料的螢幕擷取畫面所示：

![讀取器 SQL][1]

## <a name="python"></a>使用 hello Python 程式設計語言
本節示範如何使用 hello [pyodbc 文件庫](https://code.google.com/p/pyodbc/)tooestablish ODBC 連接以 Python tooa SQL server 資料庫。 如下所示為 hello 資料庫連接字串: （servername、 dbname、 username 與 password 以取代您的設定）：

    #Set up hello SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

hello[熊](http://pandas.pydata.org/)Python 中的程式庫提供一組豐富的資料結構和資料分析工具的 Python 程式設計的資料操作。 hello 的下列程式碼從 Azure SQL database 中的資料表將熊資料讀入 0.1 %hello 資料的範例：

    import pandas as pd

    # Query database and load hello returned results in pandas data frame
    data_frame = pd.read_sql('''select column1, cloumn2... from <table_name> tablesample (0.1 percent)''', conn)

您現在可以使用 hello 熊資料框架中的 hello 取樣資料。 

### <a name="python-aml"></a>連接 tooAzure 機器學習服務
您可以使用下列範例程式碼 toosave hello 下取樣資料 tooa 檔 hello，並將它上傳 tooan Azure blob。 hello hello blob 中可以直接讀取資料到 Azure 機器學習實驗中使用 hello[匯入資料][ import-data]模組。 hello 步驟如下所示： 

1. 寫入 hello 熊資料框架 tooa 本機檔案
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. 本機檔案 tooAzure blob 上傳
   
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
3. 從使用 Azure Machine Learning 的 Azure blob 讀取資料[匯入資料][ import-data]模組 hello 螢幕擷取以下所示：

![讀取器 Blob][2]

## <a name="hello-team-data-science-process-in-action-example"></a>在動作範例中的 hello 小組資料科學程序
Hello 小組資料科學程序的端對端逐步解說範例，使用公用的資料集，請參閱[小組的操作資料科學程序： 使用 SQL Sever](machine-learning-data-science-process-sql-walkthrough.md)。

[1]: ./media/machine-learning-data-science-sample-sql-server-virtual-machine/reader_database.png
[2]: ./media/machine-learning-data-science-sample-sql-server-virtual-machine/reader_blob.png

[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
