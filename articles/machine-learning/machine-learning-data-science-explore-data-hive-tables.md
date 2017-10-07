---
title: "使用 Hive 查詢的 Hive 資料表中的 aaaExplore 資料 |Microsoft 文件"
description: "使用 Hive 查詢來瀏覽 Hive 資料表的資料。"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 0d46cea5-2b4c-4384-9bfa-fa20f6f75148
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 2ede3d41682aa08ced19284f7a83ec95e0c2a93a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="explore-data-in-hive-tables-with-hive-queries"></a>使用 Hive 查詢來瀏覽 Hive 資料表的資料
本文件提供範例 Hive 指令碼會使用的 tooexplore HDInsight Hadoop 叢集中的 Hive 資料表中的資料。

hello 下列**功能表**連結 tootopics 描述 toouse 工具 tooexplore 資料，從不同的儲存體環境的方式。

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

## <a name="prerequisites"></a>必要條件
本文假設您已經：

* 建立 Azure 儲存體帳戶。 如需指示，請參閱[建立 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)
* 自訂的 Hadoop 叢集以 hello HDInsight 服務使用者佈建。 如需指示，請參閱 [自訂適用於進階分析的 Azure HDInsight Hadoop 叢集](machine-learning-data-science-customize-hadoop-cluster.md)。
* hello 資料已上傳的 tooHive Azure HDInsight Hadoop 叢集中的資料表。 如果尚未存在，請依照下列中的 hello 指示[建立和載入資料 tooHive 資料表](machine-learning-data-science-move-hive-tables.md)tooupload 資料 tooHive 資料表第一次。
* 啟用遠端存取 toohello 叢集。 如果您需要的指示，請參閱[存取 hello 的 Hadoop 叢集前端節點](machine-learning-data-science-customize-hadoop-cluster.md#headnode)。
* 如果您需要如何指示 toosubmit Hive 查詢，請參閱[如何 tooSubmit Hive 查詢](machine-learning-data-science-move-hive-tables.md#submit)

## <a name="example-hive-query-scripts-for-data-exploration"></a>資料探索的 Hive 查詢指令碼範例
1. 取得每個資料分割的觀察值的 hello 計數`SELECT <partitionfieldname>, count(*) from <databasename>.<tablename> group by <partitionfieldname>;`
2. 取得每日的觀察值的 hello 計數`SELECT to_date(<date_columnname>), count(*) from <databasename>.<tablename> group by to_date(<date_columnname>);`
3. 取得類別的資料行中的 hello 層級  
    `SELECT  distinct <column_name> from <databasename>.<tablename>`
4. 取得 hello 層級數目的兩個類別資料行組合中`SELECT <column_a>, <column_b>, count(*) from <databasename>.<tablename> group by <column_a>, <column_b>`
5. 取得數值資料行的 hello 發佈  
    `SELECT <column_name>, count(*) from <databasename>.<tablename> group by <column_name>`
6. 聯結兩個資料表來擷取記錄
   
        SELECT
            a.<common_columnname1> as <new_name1>,
            a.<common_columnname2> as <new_name2>,
            a.<a_column_name1> as <new_name3>,
            a.<a_column_name2> as <new_name4>,
            b.<b_column_name1> as <new_name5>,
            b.<b_column_name2> as <new_name6>
        FROM
            (
            SELECT <common_columnname1>,
                <common_columnname2>,
                <a_column_name1>,
                <a_column_name2>,
            FROM <databasename>.<tablename1>
            ) a
            join
            (
            SELECT <common_columnname1>,
                <common_columnname2>,
                <b_column_name1>,
                <b_column_name2>,
            FROM <databasename>.<tablename2>
            ) b
            ON a.<common_columnname1>=b.<common_columnname1> and a.<common_columnname2>=b.<common_columnname2>

## <a name="additional-query-scripts-for-taxi-trip-data-scenarios"></a>計程車路線資料案例的其他查詢指令碼
也都是特定的查詢的範例[NYC 計程車路線資料](http://chriswhong.com/open-data/foil_nyc_taxi/)案例也會提供在[GitHub 儲存機制](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts)。 這些查詢已經有指定的資料結構描述，而且準備好 toobe 提交 toorun。

