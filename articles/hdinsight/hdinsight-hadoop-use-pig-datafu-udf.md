---
title: "與 HDInsight 的 Azure 上的 Pig DataFu aaaUse |Microsoft 文件"
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
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 357ad8f9694cc590115289877e752bdd242bdadc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-datafu-with-pig-on-hdinsight"></a><span data-ttu-id="4288b-104">在 HDInsight 上搭配使用 DataFu 與 Pig</span><span class="sxs-lookup"><span data-stu-id="4288b-104">Use DataFu with pig on HDInsight</span></span>

<span data-ttu-id="4288b-105">深入了解如何與 HDInsight DataFu toouse。</span><span class="sxs-lookup"><span data-stu-id="4288b-105">Learn how toouse DataFu with HDInsight.</span></span> <span data-ttu-id="4288b-106">DataFu 是搭配 Hadoop 上的 Pig 使用的開放原始碼程式庫集合。</span><span class="sxs-lookup"><span data-stu-id="4288b-106">DataFu is a collection of Open Source libraries for use with Pig on Hadoop.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4288b-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="4288b-107">Prerequisites</span></span>

* <span data-ttu-id="4288b-108">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="4288b-108">An Azure subscription.</span></span>

* <span data-ttu-id="4288b-109">Azure HDInsight 叢集 (以 Linux 或 Windows 為基礎)</span><span class="sxs-lookup"><span data-stu-id="4288b-109">An Azure HDInsight cluster (Linux or Windows based)</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="4288b-110">Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。</span><span class="sxs-lookup"><span data-stu-id="4288b-110">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="4288b-111">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="4288b-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="4288b-112">[在 HDInsight 使用 Pig](hdinsight-use-pig.md)</span><span class="sxs-lookup"><span data-stu-id="4288b-112">A basic familiarity with [using Pig on HDInsight](hdinsight-use-pig.md)</span></span>

## <a name="install-datafu-on-linux-based-hdinsight"></a><span data-ttu-id="4288b-113">在以 Linux 為基礎的 HDInsight 上安裝 DataFu</span><span class="sxs-lookup"><span data-stu-id="4288b-113">Install DataFu on Linux-based HDInsight</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4288b-114">DataFu 是安裝在 Linux 架構的叢集 3.3 版和更高版本上，以及在 Windows 架構的叢集上。</span><span class="sxs-lookup"><span data-stu-id="4288b-114">DataFu is installed on Linux-based clusters version 3.3 and higher, and on Windows-based clusters.</span></span> <span data-ttu-id="4288b-115">不會安裝在比 3.3 版更早的 Linux 架構叢集上。</span><span class="sxs-lookup"><span data-stu-id="4288b-115">It is not installed on Linux-based clusters earlier than 3.3.</span></span>
>
> <span data-ttu-id="4288b-116">如果您使用 Windows 架構的叢集或是高於 3.3 版的 Linux 架構叢集，請略過本節。</span><span class="sxs-lookup"><span data-stu-id="4288b-116">If you are using a Windows-based cluster, or a Linux-based cluster higher than version 3.3, skip this section.</span></span>

<span data-ttu-id="4288b-117">DataFu 可以下載並安裝從 hello Maven 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="4288b-117">DataFu can be downloaded and installed from hello Maven repository.</span></span> <span data-ttu-id="4288b-118">使用下列步驟 tooadd DataFu tooyour HDInsight 叢集的 hello:</span><span class="sxs-lookup"><span data-stu-id="4288b-118">Use hello following steps tooadd DataFu tooyour HDInsight cluster:</span></span>

1. <span data-ttu-id="4288b-119">Tooyour 以 Linux 為基礎的 HDInsight 叢集使用 SSH 連線。</span><span class="sxs-lookup"><span data-stu-id="4288b-119">Connect tooyour Linux-based HDInsight cluster using SSH.</span></span> <span data-ttu-id="4288b-120">如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="4288b-120">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="4288b-121">使用下列命令 toodownload hello DataFu jar 檔使用 hello wget 公用程式，hello 或複製並貼入 hello 連結您的瀏覽器 toobegin hello 下載。</span><span class="sxs-lookup"><span data-stu-id="4288b-121">Use hello following command toodownload hello DataFu jar file using hello wget utility, or copy and paste hello link into your browser toobegin hello download.</span></span>

    ```
    wget http://central.maven.org/maven2/com/linkedin/datafu/datafu/1.2.0/datafu-1.2.0.jar
    ```

3. <span data-ttu-id="4288b-122">接下來上, 傳您的 HDInsight 叢集的 hello 檔案 toodefault 存放裝置。</span><span class="sxs-lookup"><span data-stu-id="4288b-122">Next, upload hello file toodefault storage for your HDInsight cluster.</span></span> <span data-ttu-id="4288b-123">將 hello 檔案放在預設儲存體可讓可用 tooall 節點 hello 叢集中。</span><span class="sxs-lookup"><span data-stu-id="4288b-123">Placing hello file in default storage makes it available tooall nodes in hello cluster.</span></span>

    ```
    hdfs dfs -put datafu-1.2.0.jar /example/jars
    ```

    > [!NOTE]
    > <span data-ttu-id="4288b-124">hello 前一個命令會儲存在 hello jar`/example/jars`因為 hello 叢集存放裝置上的此目錄已經存在。</span><span class="sxs-lookup"><span data-stu-id="4288b-124">hello previous command stores hello jar in `/example/jars` since this directory already exists on hello cluster storage.</span></span> <span data-ttu-id="4288b-125">您可以使用 HDInsight 叢集上任何想要的位置。</span><span class="sxs-lookup"><span data-stu-id="4288b-125">You can use any location you wish on HDInsight cluster storage.</span></span>

## <a name="use-datafu-with-pig"></a><span data-ttu-id="4288b-126">搭配使用 DataFu 與 Pig</span><span class="sxs-lookup"><span data-stu-id="4288b-126">Use DataFu With Pig</span></span>

<span data-ttu-id="4288b-127">本節中的 hello 步驟假設您已熟悉使用 Pig HDInsight 上。</span><span class="sxs-lookup"><span data-stu-id="4288b-127">hello steps in this section assume that you are familiar with using Pig on HDInsight.</span></span> <span data-ttu-id="4288b-128">如需搭配使用 Pig 與 HDInsight 的詳細資訊，請參閱 [搭配使用 Pig 與 HDInsight](hdinsight-use-pig.md)。</span><span class="sxs-lookup"><span data-stu-id="4288b-128">For more information on using Pig with HDInsight, see [Use Pig with HDInsight](hdinsight-use-pig.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4288b-129">如果您手動安裝 DataFu hello 前一節中使用 hello 步驟，您必須再使用它來進行註冊。</span><span class="sxs-lookup"><span data-stu-id="4288b-129">If you manually installed DataFu using hello steps in hello previous section, you must register it before using it.</span></span>
>
> * <span data-ttu-id="4288b-130">如果叢集使用 Azure 儲存體，請使用 `wasb://` 路徑。</span><span class="sxs-lookup"><span data-stu-id="4288b-130">If your cluster uses Azure Storage, use a `wasb://` path.</span></span> <span data-ttu-id="4288b-131">例如， `register wasb:///example/jars/datafu-1.2.0.jar`。</span><span class="sxs-lookup"><span data-stu-id="4288b-131">For example, `register wasb:///example/jars/datafu-1.2.0.jar`.</span></span>
>
> * <span data-ttu-id="4288b-132">如果叢集使用 Azure Data Lake Store，請使用 `adl://` 路徑。</span><span class="sxs-lookup"><span data-stu-id="4288b-132">If your cluster uses Azure Data Lake Store, use an `adl://` path.</span></span> <span data-ttu-id="4288b-133">例如， `register adl://home/example/jars/datafu-1.2.0.jar`。</span><span class="sxs-lookup"><span data-stu-id="4288b-133">For example, `register adl://home/example/jars/datafu-1.2.0.jar`.</span></span>

<span data-ttu-id="4288b-134">您通常會定義 DataFu 函式的別名。</span><span class="sxs-lookup"><span data-stu-id="4288b-134">You often define an alias for DataFu functions.</span></span> <span data-ttu-id="4288b-135">hello 下列範例會定義的別名`SHA`:</span><span class="sxs-lookup"><span data-stu-id="4288b-135">hello following example defines an alias of `SHA`:</span></span>

```piglatin
DEFINE SHA datafu.pig.hash.SHA();
```

<span data-ttu-id="4288b-136">然後，您可以使用的拉丁 Pig 指令碼 toogenerate 雜湊中此別名 hello 輸入資料。</span><span class="sxs-lookup"><span data-stu-id="4288b-136">You can then use this alias in a Pig Latin script toogenerate a hash for hello input data.</span></span> <span data-ttu-id="4288b-137">例如，hello 下列程式碼取代 hello 輸入資料中的 hello 位置的雜湊值：</span><span class="sxs-lookup"><span data-stu-id="4288b-137">For example, hello following code replaces hello location in hello input data with a hash value:</span></span>

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

<span data-ttu-id="4288b-138">它會產生下列輸出的 hello:</span><span class="sxs-lookup"><span data-stu-id="4288b-138">It generates hello following output:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="4288b-139">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4288b-139">Next steps</span></span>

<span data-ttu-id="4288b-140">如需 DataFu 或 Pig 的詳細資訊，請參閱下列文件的 hello:</span><span class="sxs-lookup"><span data-stu-id="4288b-140">For more information on DataFu or Pig, see hello following documents:</span></span>

* <span data-ttu-id="4288b-141">[Apache DataFu Pig 指南](http://datafu.incubator.apache.org/docs/datafu/guide.html)(英文)。</span><span class="sxs-lookup"><span data-stu-id="4288b-141">[Apache DataFu Pig Guide](http://datafu.incubator.apache.org/docs/datafu/guide.html).</span></span>
* [<span data-ttu-id="4288b-142">搭配 HDInsight 使用 Pig</span><span class="sxs-lookup"><span data-stu-id="4288b-142">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
