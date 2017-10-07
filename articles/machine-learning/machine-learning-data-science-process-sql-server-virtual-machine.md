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
# <a name="heading"></a>在 Azure 上處理 SQL Server 虛擬機器中的資料
本文件涵蓋如何 tooexplore 資料並產生資料儲存在 Azure 上的 SQL Server VM 的功能。 使用 SQL整理資料或使用 Python 這類程式設計語言，即可完成此動作。

> [!NOTE]
> 這份文件中的 hello 範例 SQL 陳述式會假設資料是在 SQL Server。 如果沒有，請參閱 toohello 雲端資料科學程序對應 toolearn 如何 toomove 您資料 tooSQL 伺服器。
> 
> 

## <a name="SQL"></a>使用 SQL
我們會描述下列資料 wrangling 工作使用 SQL 本節中的 hello:

1. [資料探索](#sql-dataexploration)
2. [功能產生](#sql-featuregen)

### <a name="sql-dataexploration"></a>資料探索
以下是一些範例 SQL 指令碼可能是 SQL Server 中的使用的 tooexplore 資料存放區。

> [!NOTE]
> 如需實用範例，您可以使用 hello [NYC 計程車資料集](http://www.andresmh.com/nyctaxitrips/)和參考 toohello IPNB 標題為[NYC 資料 wrangling 使用 IPython 筆記型電腦和 SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb)的端對端逐步解說。
> 
> 

1. 取得每日的觀察值的 hello 計數
   
    `SELECT CONVERT(date, <date_columnname>) as date, count(*) as c from <tablename> group by CONVERT(date, <date_columnname>)` 
2. 取得類別的資料行中的 hello 層級
   
    `select  distinct <column_name> from <databasename>`
3. 取得 hello 層級數目的兩個類別資料行組合中 
   
    `select <column_a>, <column_b>,count(*) from <tablename> group by <column_a>, <column_b>`
4. 取得數值資料行的 hello 發佈
   
    `select <column_name>, count(*) from <tablename> group by <column_name>`

### <a name="sql-featuregen"></a>功能產生
在本節中，我們將說明使用 SQL 產生功能的方式：  

1. [以計數為基礎的功能產生](#sql-countfeature)
2. [分類收納功能產生](#sql-binningfeature)
3. [推出 hello 功能，從單一資料行](#sql-featurerollout)

> [!NOTE]
> 一旦您產生額外的功能，您可以將它們加入為資料行 toohello 現有資料表或 hello 額外的功能與主索引鍵，可以與 hello 原始資料表聯結，建立新的資料表。 
> 
> 

### <a name="sql-countfeature"></a>以計數為基礎的功能產生
hello 下列範例示範兩種產生計數功能。 hello 第一種方法會使用條件式 sum 和第二個方法會使用 hello hello 'where' 子句。 這些屬性然後與 hello 原始資料表 （使用主索引鍵資料行） toohave 計數功能一起 hello 原始資料聯結。

    select <column_name1>,<column_name2>,<column_name3>, COUNT(*) as Count_Features from <tablename> group by <column_name1>,<column_name2>,<column_name3> 

    select <column_name1>,<column_name2> , sum(1) as Count_Features from <tablename> 
    where <column_name3> = '<some_value>' group by <column_name1>,<column_name2> 

### <a name="sql-binningfeature"></a>分類收納功能產生
hello 下列範例顯示如何 toogenerate 透過分類收納功能分組 （使用五個分類收納） 可用來當做一項功能改為數值資料行：

    `SELECT <column_name>, NTILE(5) OVER (ORDER BY <column_name>) AS BinNumber from <tablename>`


### <a name="sql-featurerollout"></a>推出 hello 功能，從單一資料行
在本節中，我們將示範如何 tooroll 出資料表 toogenerate 其他功能的單一資料行。 hello 範例假設嘗試 toogenerate 功能 hello 資料表中有經度或緯度的資料行。

以下是簡短入門經緯度位置資料 (從 stackoverflow 資源[toomeasure hello 精確度的緯度與經度的方式？](http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude))。 這是很有用 toounderstand featurizing hello 位置欄位之前：

* hello 登告訴我們我們是否北或南、 東或西 hello 地球上。
* 非零的數百個位數告訴我們使用的是經度，而不是緯度！
* hello 數以萬計的數字提供位置 tooabout 1,000 公里為單位。 它會為我們提供身處哪個大陸或海洋的實用資訊。
* hello 單位數字 （一個十進位度） 提供 too111 公里 （60 海英哩，大約 69 英哩） 上的位置。 它會告知我們大致上位於哪一個大的州或國家/地區中。
* 第一個小數位數 hello 值得向上 too11.1 金鑰管理： 它可以區別 hello 的鄰近大型縣 （市） 從一個大城市的位置。
* 第二個小數位數 hello 值得向上 too1.1 金鑰管理： 它可以分開一個 village hello 下一步。
* 第三個小數位數 hello 值得向上 too110 m： 大型農業欄位或機構校園，它能識別。
* 第四個小數位數 hello 值得向上 too11 m： 它能識別的土地的資料。 它是可比較 toohello 未修正 GPS 單位沒有干擾的典型的精確度。
* 第五個小數位數 hello 值得向上 too1.1 m： 它可以區別樹狀結構與彼此。 精確度 toothis 層級與商業 GPS 裝置只完成差異更正。
* 第六個小數位數 hello 值得 too0.11 m： 您可以使用此配置結構的資料，來設計環境，建置道路組成。 比起足以追蹤冰河和河流的移動，這應該是更好的方式。 您可以採用含有 GPS 的精心度量 (例如，微分校正的 GPS) 來達成此項目。

hello 位置資訊可能特徵化，如下所示，分開地區、 位置和縣 （市） 資訊。 請注意，您也可以呼叫 REST 端點，例如 Bing Maps API 位於[找出的位置點](https://msdn.microsoft.com/library/ff701710.aspx)tooget hello 地區/地區的資訊。

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

這些位置為基礎的功能可以進一步使用的 toogenerate 其他計數功能如先前所述。 

> [!TIP]
> 您可以透過程式設計方式插入 hello 記錄使用您所選擇的語言。 您可能需要在區塊 tooimprove 寫入效率 tooinsert hello 資料 (如需如何 toodo 此使用 pyodbc，請參閱[使用 python HelloWorld 範例 tooaccess SQLServer](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python))。 另一個替代方式是使用 hello hello 資料庫中的 tooinsert 資料[BCP 公用程式](https://msdn.microsoft.com/library/ms162802.aspx)。
> 
> 

### <a name="sql-aml"></a>連接 tooAzure 機器學習服務
新產生的 hello 功能可以當做 tooan 現有資料行的資料表加入或儲存在新的資料表，與機器學習的 hello 原始資料表聯結。 功能可以產生或存取已經建立時，使用 hello[匯入資料][ import-data]如下所示，Azure Machine Learning 中的模組：

![azureml 讀取器][1] 

## <a name="python"></a>使用類似 Python 的程式設計語言
使用 Python tooexplore 資料以及資料是 SQL Server 中的 hello 類似 tooprocessing 資料使用 Python，如中所述的 Azure blob 中的時產生功能[資料科學環境中的程序的 Azure Blob 資料](machine-learning-data-science-process-data-blob.md)。 hello 資料需要 toobe hello 資料庫載入熊資料框架，然後可以進一步處理。 我們的文件 hello 連接 toohello 資料庫並將在本節中的 hello 資料框架 hello 資料載入程序。

下列連接字串格式的 hello 可以是使用的 tooconnect tooa SQL Server 資料庫，來自 Python 使用 pyodbc （取代 servername、 dbname、 username 和 password 的特定值）：

    #Set up hello SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

hello[熊程式庫](http://pandas.pydata.org/)Python 中提供一組豐富的資料結構和資料分析工具的 Python 程式設計資料操作。 下列程式碼 hello 讀取從 SQL Server 資料庫傳回至熊資料框架的 hello 結果：

    # Query database and load hello returned results in pandas data frame
    data_frame = pd.read_sql('''select <columnname1>, <cloumnname2>... from <tablename>''', conn)

現在您可以在 hello 文件中涵蓋 hello 熊資料框架[資料科學環境中的程序的 Azure Blob 資料](machine-learning-data-science-process-data-blob.md)。

## <a name="azure-data-science-in-action-example"></a>作用中的 Azure 資料科學範例
如需端對端逐步解說的範例 hello Azure 資料科學使用公用資料集的處理程序，請參閱[動作中的 Azure 資料科學程序](machine-learning-data-science-process-sql-walkthrough.md)。

[1]: ./media/machine-learning-data-science-process-sql-server-virtual-machine/reader_db_featurizedinput.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/

