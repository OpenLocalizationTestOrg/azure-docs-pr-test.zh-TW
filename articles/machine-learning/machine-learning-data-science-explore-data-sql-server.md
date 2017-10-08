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
# <a name="explore-data-in-sql-server-virtual-machine-on-azure"></a>在 Azure 上瀏覽 SQL Server 虛擬機器中的資料
本文件涵蓋如何 tooexplore 資料儲存在 Azure 上的 SQL Server VM。 使用 SQL整理資料或使用 Python 這類程式設計語言，即可完成此動作。

hello 下列**功能表**連結 tootopics 描述 toouse 工具 tooexplore 資料，從不同的儲存體環境的方式。 這項工作是 hello Cortana 分析程序 (CAP) 的步驟。

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

> [!NOTE]
> 這份文件中的 hello 範例 SQL 陳述式會假設資料是在 SQL Server。 如果沒有，請參閱 toohello 雲端資料科學程序對應 toolearn 如何 toomove 您資料 tooSQL 伺服器。
> 
> 

## <a name="sql-dataexploration"></a>使用 SQL 指令碼瀏覽 SQL 資料
以下是一些範例 SQL 指令碼可能是 SQL Server 中的使用的 tooexplore 資料存放區。

1. 取得每日的觀察值的 hello 計數
   
    `SELECT CONVERT(date, <date_columnname>) as date, count(*) as c from <tablename> group by CONVERT(date, <date_columnname>)` 
2. 取得類別的資料行中的 hello 層級
   
    `select  distinct <column_name> from <databasename>`
3. 取得 hello 層級數目的兩個類別資料行組合中 
   
    `select <column_a>, <column_b>,count(*) from <tablename> group by <column_a>, <column_b>`
4. 取得數值資料行的 hello 發佈
   
    `select <column_name>, count(*) from <tablename> group by <column_name>`

> [!NOTE]
> 如需實用範例，您可以使用 hello [NYC 計程車資料集](http://www.andresmh.com/nyctaxitrips/)和參考 toohello IPNB 標題為[NYC 資料 wrangling 使用 IPython 筆記型電腦和 SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb)的端對端逐步解說。
> 
> 

## <a name="python"></a>使用 Python 瀏覽 SQL 資料
使用 Python tooexplore 資料，並產生功能，資料是 SQL Server 中的 hello 類似 tooprocessing 資料時使用 Python，Azure blob 中所述[資料科學環境中的程序的 Azure Blob 資料](machine-learning-data-science-process-data-blob.md)。 hello 資料需要 toobe hello 資料庫載入熊資料框架，然後可以進一步處理。 我們的文件連接 toohello 資料庫以及 hello 資料載入 hello 本節中的資料框架的 hello 程的序。

下列連接字串格式的 hello 可以是使用的 tooconnect tooa SQL Server 資料庫，來自 Python 使用 pyodbc （取代 servername、 dbname、 username 和 password 的特定值）：

    #Set up hello SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

hello[熊程式庫](http://pandas.pydata.org/)Python 中提供一組豐富的資料結構和資料分析工具的 Python 程式設計資料操作。 hello 下列程式碼會讀取從 SQL Server 資料庫傳回至熊資料框架的 hello 結果：

    # Query database and load hello returned results in pandas data frame
    data_frame = pd.read_sql('''select <columnname1>, <cloumnname2>... from <tablename>''', conn)

現在您可以在 hello 主題涵蓋與 hello 熊資料框架[資料科學環境中的程序的 Azure Blob 資料](machine-learning-data-science-process-data-blob.md)。

## <a name="cortana-analytics-process-in-action-example"></a>Cortana 分析程序實務範例
如需端對端逐步解說的範例 hello Cortana 分析程序，使用公用的資料集，請參閱[hello 動作中的資料科學的小組流程： 使用 SQL Server](machine-learning-data-science-process-sql-walkthrough.md)。

