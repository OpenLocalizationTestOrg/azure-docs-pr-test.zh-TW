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
# <a name="explore-data-in-hive-tables-with-hive-queries"></a><span data-ttu-id="8c431-103">使用 Hive 查詢來瀏覽 Hive 資料表的資料</span><span class="sxs-lookup"><span data-stu-id="8c431-103">Explore data in Hive tables with Hive queries</span></span>
<span data-ttu-id="8c431-104">本文件提供範例 Hive 指令碼會使用的 tooexplore HDInsight Hadoop 叢集中的 Hive 資料表中的資料。</span><span class="sxs-lookup"><span data-stu-id="8c431-104">This document provides sample Hive scripts that are used tooexplore data in Hive tables in an HDInsight Hadoop cluster.</span></span>

<span data-ttu-id="8c431-105">hello 下列**功能表**連結 tootopics 描述 toouse 工具 tooexplore 資料，從不同的儲存體環境的方式。</span><span class="sxs-lookup"><span data-stu-id="8c431-105">hello following **menu** links tootopics that describe how toouse tools tooexplore data from various storage environments.</span></span>

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

## <a name="prerequisites"></a><span data-ttu-id="8c431-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="8c431-106">Prerequisites</span></span>
<span data-ttu-id="8c431-107">本文假設您已經：</span><span class="sxs-lookup"><span data-stu-id="8c431-107">This article assumes that you have:</span></span>

* <span data-ttu-id="8c431-108">建立 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="8c431-108">Created an Azure storage account.</span></span> <span data-ttu-id="8c431-109">如需指示，請參閱[建立 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="8c431-109">If you need instructions, see [Create an Azure Storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span></span>
* <span data-ttu-id="8c431-110">自訂的 Hadoop 叢集以 hello HDInsight 服務使用者佈建。</span><span class="sxs-lookup"><span data-stu-id="8c431-110">Provisioned a customized Hadoop cluster with hello HDInsight service.</span></span> <span data-ttu-id="8c431-111">如需指示，請參閱 [自訂適用於進階分析的 Azure HDInsight Hadoop 叢集](machine-learning-data-science-customize-hadoop-cluster.md)。</span><span class="sxs-lookup"><span data-stu-id="8c431-111">If you need instructions, see [Customize Azure HDInsight Hadoop Clusters for Advanced Analytics](machine-learning-data-science-customize-hadoop-cluster.md).</span></span>
* <span data-ttu-id="8c431-112">hello 資料已上傳的 tooHive Azure HDInsight Hadoop 叢集中的資料表。</span><span class="sxs-lookup"><span data-stu-id="8c431-112">hello data has been uploaded tooHive tables in Azure HDInsight Hadoop clusters.</span></span> <span data-ttu-id="8c431-113">如果尚未存在，請依照下列中的 hello 指示[建立和載入資料 tooHive 資料表](machine-learning-data-science-move-hive-tables.md)tooupload 資料 tooHive 資料表第一次。</span><span class="sxs-lookup"><span data-stu-id="8c431-113">If it has not, follow hello instructions in [Create and load data tooHive tables](machine-learning-data-science-move-hive-tables.md) tooupload data tooHive tables first.</span></span>
* <span data-ttu-id="8c431-114">啟用遠端存取 toohello 叢集。</span><span class="sxs-lookup"><span data-stu-id="8c431-114">Enabled remote access toohello cluster.</span></span> <span data-ttu-id="8c431-115">如果您需要的指示，請參閱[存取 hello 的 Hadoop 叢集前端節點](machine-learning-data-science-customize-hadoop-cluster.md#headnode)。</span><span class="sxs-lookup"><span data-stu-id="8c431-115">If you need instructions, see [Access hello Head Node of Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span></span>
* <span data-ttu-id="8c431-116">如果您需要如何指示 toosubmit Hive 查詢，請參閱[如何 tooSubmit Hive 查詢](machine-learning-data-science-move-hive-tables.md#submit)</span><span class="sxs-lookup"><span data-stu-id="8c431-116">If you need instructions on how toosubmit Hive queries, see [How tooSubmit Hive Queries](machine-learning-data-science-move-hive-tables.md#submit)</span></span>

## <a name="example-hive-query-scripts-for-data-exploration"></a><span data-ttu-id="8c431-117">資料探索的 Hive 查詢指令碼範例</span><span class="sxs-lookup"><span data-stu-id="8c431-117">Example Hive query scripts for data exploration</span></span>
1. <span data-ttu-id="8c431-118">取得每個資料分割的觀察值的 hello 計數`SELECT <partitionfieldname>, count(*) from <databasename>.<tablename> group by <partitionfieldname>;`</span><span class="sxs-lookup"><span data-stu-id="8c431-118">Get hello count of observations per partition  `SELECT <partitionfieldname>, count(*) from <databasename>.<tablename> group by <partitionfieldname>;`</span></span>
2. <span data-ttu-id="8c431-119">取得每日的觀察值的 hello 計數`SELECT to_date(<date_columnname>), count(*) from <databasename>.<tablename> group by to_date(<date_columnname>);`</span><span class="sxs-lookup"><span data-stu-id="8c431-119">Get hello count of observations per day  `SELECT to_date(<date_columnname>), count(*) from <databasename>.<tablename> group by to_date(<date_columnname>);`</span></span>
3. <span data-ttu-id="8c431-120">取得類別的資料行中的 hello 層級</span><span class="sxs-lookup"><span data-stu-id="8c431-120">Get hello levels in a categorical column</span></span>  
    `SELECT  distinct <column_name> from <databasename>.<tablename>`
4. <span data-ttu-id="8c431-121">取得 hello 層級數目的兩個類別資料行組合中`SELECT <column_a>, <column_b>, count(*) from <databasename>.<tablename> group by <column_a>, <column_b>`</span><span class="sxs-lookup"><span data-stu-id="8c431-121">Get hello number of levels in combination of two categorical columns  `SELECT <column_a>, <column_b>, count(*) from <databasename>.<tablename> group by <column_a>, <column_b>`</span></span>
5. <span data-ttu-id="8c431-122">取得數值資料行的 hello 發佈</span><span class="sxs-lookup"><span data-stu-id="8c431-122">Get hello distribution for numerical columns</span></span>  
    `SELECT <column_name>, count(*) from <databasename>.<tablename> group by <column_name>`
6. <span data-ttu-id="8c431-123">聯結兩個資料表來擷取記錄</span><span class="sxs-lookup"><span data-stu-id="8c431-123">Extract records from joining two tables</span></span>
   
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

## <a name="additional-query-scripts-for-taxi-trip-data-scenarios"></a><span data-ttu-id="8c431-124">計程車路線資料案例的其他查詢指令碼</span><span class="sxs-lookup"><span data-stu-id="8c431-124">Additional query scripts for taxi trip data scenarios</span></span>
<span data-ttu-id="8c431-125">也都是特定的查詢的範例[NYC 計程車路線資料](http://chriswhong.com/open-data/foil_nyc_taxi/)案例也會提供在[GitHub 儲存機制](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts)。</span><span class="sxs-lookup"><span data-stu-id="8c431-125">Examples of queries that are specific too[NYC Taxi Trip Data](http://chriswhong.com/open-data/foil_nyc_taxi/) scenarios are also provided in [GitHub repository](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts).</span></span> <span data-ttu-id="8c431-126">這些查詢已經有指定的資料結構描述，而且準備好 toobe 提交 toorun。</span><span class="sxs-lookup"><span data-stu-id="8c431-126">These queries already have data schema specified and are ready toobe submitted toorun.</span></span>

