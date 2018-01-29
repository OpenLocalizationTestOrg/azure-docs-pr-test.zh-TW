---
title: "在 HDInsight 中搭配使用 DataFu 與 Pig - Azure | Microsoft Docs"
description: "DataFu 是搭配 Hadoop 使用的程式庫集合。 了解如何在 HDInsight 叢集上搭配使用 DataFu 與 Pig。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 0016721a-82be-4773-88ad-91e6b2c21cbb
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/17/2018
ms.author: larryfr
ms.openlocfilehash: d9aaef778f08500f45b6d1260f2a5d301fabeba8
ms.sourcegitcommit: f1c1789f2f2502d683afaf5a2f46cc548c0dea50
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/18/2018
---
# <a name="use-datafu-with-pig-on-hdinsight"></a>在 HDInsight 上搭配使用 DataFu 與 Pig

了解如何搭配 HDInsight 使用 DataFu。 DataFu 是搭配 Hadoop 上的 Pig 使用的開放原始碼程式庫集合。

## <a name="prerequisites"></a>先決條件

* Azure 訂用帳戶。

* Azure HDInsight 叢集 (以 Linux 或 Windows 為基礎)

  > [!IMPORTANT]
  > Linux 是唯一使用於 HDInsight 3.4 版或更新版本的作業系統。 如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](../hdinsight-component-versioning.md#hdinsight-windows-retirement)。

* [在 HDInsight 使用 Pig](hdinsight-use-pig.md)

## <a name="install-datafu-on-linux-based-hdinsight"></a>在以 Linux 為基礎的 HDInsight 上安裝 DataFu

> [!IMPORTANT]
> DataFu 是安裝在 Linux 架構的叢集 3.3 版和更高版本上，以及在 Windows 架構的叢集上。 不會安裝在比 3.3 版更早的 Linux 架構叢集上。
>
> 如果您使用 Windows 架構的叢集或是高於 3.3 版的 Linux 架構叢集，請略過本節。

可以從 Maven 儲存機制下載並安裝 DataFu。 使用下列步驟將 DataFu 新增至您的 HDInsight 叢集：

1. 使用 SSH 連線至以 Linux 為基礎的 HDInsight 叢集： 如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](../hdinsight-hadoop-linux-use-ssh-unix.md)。

2. 使用下列命令以 wget 公用程式下載 DataFu jar 檔案，或複製連結並在瀏覽器中貼上來開始下載。

    ```
    wget http://central.maven.org/maven2/com/linkedin/datafu/datafu/1.2.0/datafu-1.2.0.jar
    ```

3. 接下來，將檔案上傳至 HDInsight 叢集的預設儲存體。 如果將檔案放在預設儲存體中，則叢集的所有節點都可使用此檔案。

    ```
    hdfs dfs -put datafu-1.2.0.jar /example/jars
    ```

    > [!NOTE]
    > 前一個命令會將 jar 儲存在 `/example/jars`，因為叢集儲存體上已經有此目錄。 您可以使用 HDInsight 叢集上任何想要的位置。

## <a name="use-datafu-with-pig"></a>搭配使用 DataFu 與 Pig

本節中的步驟假設您已熟悉如何在 HDInsight 上使用 Pig。 如需搭配使用 Pig 與 HDInsight 的詳細資訊，請參閱 [搭配使用 Pig 與 HDInsight](hdinsight-use-pig.md)。

> [!IMPORTANT]
> 如果您使用上一節的步驟手動安裝 DataFu，您必須先進行註冊才能使用。
>
> * 如果叢集使用 Azure 儲存體，請使用 `wasb://` 路徑。 例如： `register wasb:///example/jars/datafu-1.2.0.jar`。
>
> * 如果叢集使用 Azure Data Lake Store，請使用 `adl://` 路徑。 例如： `register adl://home/example/jars/datafu-1.2.0.jar`。

您通常會定義 DataFu 函式的別名。 下列範例會定義 `SHA` 的別名：

```piglatin
DEFINE SHA datafu.pig.hash.SHA();
```

您之後可以在 Pig Latin 指令碼中使用此別名來產生輸入資料的雜湊值。 例如，下列程式碼會使用雜湊值取代輸入資料中的位置：

```piglatin
raw = LOAD '/HdiSamples/HdiSamples/SensorSampleData/building/building.csv' USING
    org.apache.pig.piggybank.storage.CSVExcelStorage(',', 'NO_MULTILINE', 'UNIX', 'SKIP_INPUT_HEADER') AS
    (int1:int,
     id1:chararray,
     int2:int,
     id2:chararray,
     location:chararray);
mask = FOREACH raw GENERATE int1, id1, int2, id2, SHA(location);
DUMP mask;
```

它會產生下列輸出：

    (1,M1,25,AC1000,aa5ab35a9174c2062b7f7697b33fafe5ce404cf5fecf6bfbbf0dc96ba0d90046)
    (2,M2,27,FN39TG,7a1ca4ef7515f7276bae7230545829c27810c9d9e98ab2c06066bee6270d5153)
    (3,M3,28,JDNS77,07f62b021771d3cf67e2e1faf18769cc5e5c119ad7d4d1847a11e11d6d5a7ecb)
    (4,M4,17,GG1919,aed8f531aa7e785be255bc435e2582e74c58defedebcb629eeabf365b809bd6f)
    (5,M5,3,ACMAX22,1ed8c7e56c947bebc0cfcf88c4ea0f02c944568f71df893a99970e4f0c78cddc)
    (6,M6,9,AC1000,c96dd81db196cca5f57bd4270bbb9d9e9d1b242d67f9364005ee1dfdc2632523)
    (7,M7,13,FN39TG,3e049d78d958038ac6bd5dcf038075cc73362b4956aaf7308c3a69c8eca76297)
    (8,M8,25,JDNS77,c1ef40ce0484c698eb4bd27fe56c1e7b68d74f9780ed674210d0e5013dae45e9)
    (9,M9,11,GG1919,a7d355b26bda6bf1196ccffead0b2cf2b81f0a9de5b4876b44407f1dc07e51e6)
    (10,M10,23,ACMAX22,10436829032f361a3de50048de41755140e581467bc1895e6c1a17f423e42d10)
    (11,M11,14,AC1000,348841ef53dbd5a64008a86be432973db790774fb28b59b0d99702a3188b3705)
    (12,M12,26,FN39TG,aed8f531aa7e785be255bc435e2582e74c58defedebcb629eeabf365b809bd6f)
    (13,M13,25,JDNS77,ed9ad13611d7164839dd3feaf9a7f6a75a4138f389e0d45f8e07fa38da1116a2)
    (14,M14,17,GG1919,80db4ccdca106d37b920206331fcfe3e9e50a9e763d89b54ce3ad5ac8cf30f03)
    (15,M15,19,ACMAX22,3552ac0c032467fbf592cb4d10c5c9267800c01e343ad8ca557256d882ae9327)
    (16,M16,23,AC1000,07c67d76ef92ac9853588e098983fefba4ba5965f8fec95f42ab0d04c27865ba)
    (17,M17,11,FN39TG,557c1599d9a04895d3817d293e0806a4419a14de31958386182798d0d2ed3a56)
    (18,M18,25,JDNS77,dbc74a36d8e7439c45c64d856388506cc9b1218619cef979c3d605115a7a4546)
    (19,M19,14,GG1919,be55ef3f4c4e6c2d9c2afe2a33ac90ad0f50d4de7f9163999877e2a9ca5a54f8)
    (20,M20,19,ACMAX22,ea0b937ea317101ee2c26b03a4843a19ceced8a2b9673c3cf409a726ca2b0fd8)

## <a name="next-steps"></a>後續步驟

如需 DataFu 或 Pig 的詳細資訊，請參閱下列文件：

* [Apache DataFu Pig 指南](http://datafu.incubator.apache.org/docs/datafu/guide.html)(英文)。
* [搭配 HDInsight 使用 Pig](hdinsight-use-pig.md)
