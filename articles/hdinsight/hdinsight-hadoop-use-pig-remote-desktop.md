---
title: "aaaUse HDInsight 的 Azure 中的遠端桌面的 Hadoop Pig |Microsoft 文件"
description: "了解如何 toouse hello Pig 命令 toorun Pig 拉丁陳述式從 HDInsight 中的遠端桌面連線 tooa Windows 為基礎的 Hadoop 叢集。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: e034a286-de0f-465f-8bf1-3d085ca6abed
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/17/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 2a4565fa827cd45fdbe6194b0486df93a6561084
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="run-pig-jobs-from-a-remote-desktop-connection"></a>從遠端桌面連線執行 Pig 工作
[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

本文件提供逐步解說使用 hello Pig 命令 toorun Pig 拉丁陳述式從遠端桌面連線 tooa Windows 為基礎的 HDInsight 叢集。 Pig 拉丁可讓您透過描述資料轉換的 toocreate MapReduce 應用程式，而非對應並減少函式。

> [!IMPORTANT]
> 只有在使用 Windows 做為 hello 作業系統的 HDInsight 叢集上使用遠端桌面。 Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。 如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。
>
> HDInsight 3.4 或更高，請參閱[HDInsight 和 SSH 搭配使用 Pig](hdinsight-hadoop-use-pig-ssh.md)有關以互動方式執行 Pig 工作直接在 hello 叢集從命令列。

## <a id="prereq"></a>必要條件
toocomplete hello 本文中的步驟，您將需要下列 hello。

* Windows 型 HDInsight (HDInsight 上的 Hadoop) 叢集
* 執行 Windows 10、Windows 8 或 Windows 7 的用戶端電腦

## <a id="connect"></a>使用遠端桌面連線
Hello HDInsight 叢集，啟用遠端桌面，然後依照指示 hello 連接 tooit[連接使用 RDP tooHDInsight 叢集](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)。

## <a id="pig"></a>使用 hello Pig 命令
1. 您有遠端桌面連線之後，請啟動 hello **Hadoop 命令列**hello 桌面上使用 hello 圖示。
2. 使用下列 toostart hello Pig 命令 hello:

        %pig_home%\bin\pig

    您會看到 `grunt>` 提示字元。
3. 輸入下列陳述式的 hello:

        LOGS = LOAD 'wasb:///example/data/sample.log';

    此命令會載入 hello 記錄檔中的 hello hello sample.log 檔案內容。 您可以使用下列命令的 hello 檢視 hello hello 檔案內容：

        DUMP LOGS;
4. Hello 資料轉換從每一筆記錄套用的規則運算式 tooextract 只有 hello 記錄層級：

        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;

    您可以使用**傾印**tooview hello hello 轉換後的資料。 在此案例中為 `DUMP LEVELS;`。
5. 繼續使用下列陳述式的 hello 套用轉換。 使用`DUMP`tooview hello 結果的每個步驟之後的 hello 轉換。

    <table>
    <tr>
    <th>陳述式</th><th>作用</th>
    </tr>
    <tr>
    <td>FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;</td><td>移除包含 hello 記錄層級的 null 值的資料列，並將 hello 結果儲存到 FILTEREDLEVELS。</td>
    </tr>
    <tr>
    <td>GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;</td><td>群組 hello 的記錄層級的資料列，並將 hello 結果儲存到 GROUPEDLEVELS。</td>
    </tr>
    <tr>
    <td>FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;</td><td>建立一組新的資料，其中包含每個唯一記錄層級值和其發生次數。 這會儲存到 FREQUENCIES</td>
    </tr>
    <tr>
    <td>RESULT = order FREQUENCIES by COUNT desc;</td><td>訂單 hello 記錄層級計數 （遞減），並儲存成結果</td>
    </tr>
    </table>
6.您也可以儲存轉換的 hello 結果使用 hello`STORE`陳述式。 例如，下列命令的 hello 儲存 hello `RESULT` toohello **/example/data/pigout**目錄中為您的叢集 hello 預設儲存體容器：

        STORE RESULT into 'wasb:///example/data/pigout'

   > [!NOTE]
   > hello 資料會儲存在名為的檔案中的 hello 指定目錄**一部分 nnnnn**。 如果 hello 目錄已經存在，您會收到錯誤訊息。
   >
   >
7. tooexit hello 提示字元中，grunt 輸入 hello 陳述式之後。

        QUIT;

### <a name="pig-latin-batch-files"></a>Pig Latin 批次檔
您也可以使用 hello Pig 命令 toorun Pig 拉丁包含在檔案中。

1. 結束 hello grunt 提示字元後, 開啟**記事本**並建立新的檔案命名為**pigbatch.pig**在 hello **%pig_home%**目錄。
2. 型別或貼上 hello 下列各行至 hello **pigbatch.pig**檔案，並將其儲存：

        LOGS = LOAD 'wasb:///example/data/sample.log';
        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
        FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
        GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
        FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
        RESULT = order FREQUENCIES by COUNT desc;
        DUMP RESULT;
3. 使用 hello 遵循 toorun hello **pigbatch.pig**使用 hello pig 命令的檔案。

        pig %PIG_HOME%\pigbatch.pig

    Hello 批次工作完成時，您應該會看到下列輸出，應該是 hello 相同做為當您使用的 hello `DUMP RESULT;` hello 前述步驟中：

        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)

## <a id="summary"></a>摘要
如您所見，hello Pig 命令可讓您 toointeractively 執行 MapReduce 作業，或執行批次檔中儲存的 Pig 拉丁作業。

## <a id="nextsteps"></a>接續步驟
如需 HDInsight 中 Pig 的一般資訊：

* [搭配使用 Pig 與 HDInsight 上的 Hadoop](hdinsight-use-pig.md)

如需您可以在 HDInsight 上使用 Hadoop 之其他方式的詳細資訊：

* [搭配使用 Hive 與 HDInsight 上的 Hadoop](hdinsight-use-hive.md)
* [搭配使用 MapReduce 與 HDInsight 上的 Hadoop](hdinsight-use-mapreduce.md)
