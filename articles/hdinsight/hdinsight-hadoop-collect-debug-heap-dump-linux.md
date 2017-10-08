---
title: "HDInsight 的 Azure 上的 Hadoop 服務 aaaEnable 堆積傾印 |Microsoft 文件"
description: "在以 Linux 為基礎的 HDInsight 叢集上啟用 Hadoop 服務的堆積傾印，以進行偵錯和分析。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 8f151adb-f687-41e4-aca0-82b551953725
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 49e30f26e1a83f19e068e9da253b5548caec70d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-heap-dumps-for-hadoop-services-on-linux-based-hdinsight"></a>在以 Linux 為基礎的 HDInsight 上啟用 Hadoop 服務的堆積傾印

[!INCLUDE [heapdump-selector](../../includes/hdinsight-selector-heap-dump.md)]

堆積的傾印包含 hello 應用程式的記憶體，包括 hello 變數的值在建立 hello 傾印的 hello 階段的快照集。 因此它們有助於為執行階段發生的問題進行診斷。

> [!IMPORTANT]
> hello 本文件中的步驟只適用於使用 Linux 的 HDInsight 叢集。 Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。 如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。

## <a name="whichServices"></a>服務

您可以啟用下列服務的 hello 的堆積傾印：

* **hcatalog** - tempelton
* **hive** - hiveserver2、metastore、derbyserver
* **mapreduce** - jobhistoryserver
* **yarn** - resourcemanager、nodemanager、timelineserver
* **hdfs** - datanode、secondarynamenode、namenode

您也可以啟用 hello 對應的堆積傾印，並減少 HDInsight 所執行的處理程序。

## <a name="configuration"></a>了解堆積傾印組態

藉由傳遞選項會啟用堆積傾印 (有時稱為 opts，或參數) toohello JVM 時啟動服務。 對於大部分的 Hadoop 服務，您可以修改 hello 殼層使用指令碼 toostart hello 服務 toopass 這些選項。

在每個指令碼中，沒有匯出 **\* \_OPTS**，其中包含 hello 選項傳遞 toohello JVM。 例如，在 hello **hadoop env.sh**指令碼開頭的 hello 列`export HADOOP_NAMENODE_OPTS=`包含 hello NameNode 服務的 hello 選項。

對應並減少處理序都稍有不同，因為這些作業 hello MapReduce 服務的子處理序。 每個對應，或降低處理序會執行子容器，而且有兩個項目包含 hello JVM 選項。 兩者均包含在 **mapred-site.xml** 中：

* **mapreduce.admin.map.child.java.opts**
* **mapreduce.admin.reduce.child.java.opts**

> [!NOTE]
> 我們建議使用 Ambari toomodify 這兩個 hello 指令碼和 mapred-site.xml 設定為 Ambari 處理 hello 叢集節點之間複寫變更。 請參閱 hello[使用 Ambari](#using-ambari) > 一節，如需特定步驟。

### <a name="enable-heap-dumps"></a>啟用堆積傾印

hello 下列選項可讓堆積傾印 OutOfMemoryError 發生時：

    -XX:+HeapDumpOnOutOfMemoryError

hello  **+** 表示會啟用此選項。 hello 預設會停用。

> [!WARNING]
> 堆積會啟用傾印不 HDInsight Hadoop 服務根據預設，如 hello 傾印檔案可能很大。 如果您不要啟用以進行疑難排解，請記得 toodisable 它們一旦您重現 hello 問題和收集的 hello 傾印檔案。

### <a name="dump-location"></a>傾印位置

hello hello 傾印檔案的預設位置是 hello 目前工作目錄。 您可以控制在 hello 檔案會儲存使用 hello 下列選項：

    -XX:HeapDumpPath=/path

例如，使用`-XX:HeapDumpPath=/tmp`導致 hello 傾印 toobe 儲存在 hello tec_rule 位於 /tmp 目錄中。

### <a name="scripts"></a>指令碼

您也可以在發生 **OutOfMemoryError** 時觸發指令碼。 例如，觸發通知，因此您知道該 hello 錯誤發生。 使用 hello 下列選項 tootrigger 指令碼__OutOfMemoryError__:

    -XX:OnOutOfMemoryError=/path/to/script

> [!NOTE]
> 由於 Hadoop 分散式的系統，使用任何指令碼必須放置在 hello hello 服務執行所在叢集的所有節點上。
> 
> hello 指令碼也必須是可存取之 hello hello 服務執行的帳戶，且必須提供的位置中執行的權限。 例如，您可能希望 toostore 指令碼中的`/usr/local/bin`並用`chmod go+rx /usr/local/bin/filename.sh`toogrant 讀取和執行權限。

## <a name="using-ambari"></a>使用 Ambari

服務中，使用下列步驟的 hello toomodify hello 設定：

1. 開啟您的叢集，hello Ambari web UI。 https://YOURCLUSTERNAME.azurehdinsight.net hello URL。

    出現提示時，驗證 toohello 站台使用 hello HTTP 帳戶名稱 (預設： 系統管理員) 和密碼，供您的叢集。

   > [!NOTE]
   > 您可能會提示輸入第二次 Ambari hello 使用者名稱和密碼。 如果是的話，請輸入 hello 相同的帳戶名稱和密碼

2. 使用 hello 清單 hello 左側，選取您想 toomodify hello 服務區域。 例如 **HDFS**。 在 hello 中心區域中，選取 hello **Configs**  索引標籤。

    ![Ambari Web 圖片 (已選取 HDFS 設定索引標籤)](./media/hdinsight-hadoop-heap-dump-linux/serviceconfig.png)

3. 使用 hello**篩選...**項目，請輸入**opts**。 只會顯示包含此文字的項目。

    ![篩選的清單](./media/hdinsight-hadoop-heap-dump-linux/filter.png)

4. 尋找 hello  **\* \_OPTS** hello 服務 tooenable 堆積的傾印，並將 hello 選項項目想 tooenable。 在下列映像的 hello，我已將加入`-XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp/`toohello **HADOOP\_NAMENODE\_OPTS**項目：

    ![含有 -XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp/ 的 HADOOP_NAMENODE_OPTS](./media/hdinsight-hadoop-heap-dump-linux/opts.png)

   > [!NOTE]
   > 當啟用堆積傾印 hello 對應，或降低子處理序時，請尋找名為 hello 欄位**mapreduce.admin.map.child.java.opts**和**mapreduce.admin.reduce.child.java.opts**。

    使用 hello**儲存**按鈕 toosave hello 變更。 您可以輸入簡短描述 hello 變更的附註。

5. 套用 hello 變更之後, hello**需要重新啟動**一或多個服務旁邊的圖示會出現。

    ![必須重新啟動圖示和重新啟動按鈕](./media/hdinsight-hadoop-heap-dump-linux/restartrequiredicon.png)

6. 選取每個服務，需要重新啟動，並使用 hello**服務動作**太按鈕**上維護模式開啟**。 維護模式會防止 hello 服務在重新啟動時所產生警示。

    ![開啟維護模式功能表](./media/hdinsight-hadoop-heap-dump-linux/maintenancemode.png)

7. 一旦您已啟用維護模式，使用 hello**重新啟動**太按鈕 hello 服務**重新啟動所有受影響的**

    ![重新啟動所有受影響的項目](./media/hdinsight-hadoop-heap-dump-linux/restartbutton.png)

   > [!NOTE]
   > hello hello 的項目**重新啟動**可能不同的其他服務 按鈕。

8. 一旦 hello 服務重新啟動後，使用 hello**服務動作**太按鈕**啟動維護模式**。 此監視的警示 hello 服務的 Ambari tooresume。

