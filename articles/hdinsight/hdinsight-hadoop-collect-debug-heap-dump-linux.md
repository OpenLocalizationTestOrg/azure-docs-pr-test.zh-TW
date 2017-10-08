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
# <a name="enable-heap-dumps-for-hadoop-services-on-linux-based-hdinsight"></a><span data-ttu-id="13b82-103">在以 Linux 為基礎的 HDInsight 上啟用 Hadoop 服務的堆積傾印</span><span class="sxs-lookup"><span data-stu-id="13b82-103">Enable heap dumps for Hadoop services on Linux-based HDInsight</span></span>

[!INCLUDE [heapdump-selector](../../includes/hdinsight-selector-heap-dump.md)]

<span data-ttu-id="13b82-104">堆積的傾印包含 hello 應用程式的記憶體，包括 hello 變數的值在建立 hello 傾印的 hello 階段的快照集。</span><span class="sxs-lookup"><span data-stu-id="13b82-104">Heap dumps contain a snapshot of hello application's memory, including hello values of variables at hello time hello dump was created.</span></span> <span data-ttu-id="13b82-105">因此它們有助於為執行階段發生的問題進行診斷。</span><span class="sxs-lookup"><span data-stu-id="13b82-105">So they are useful for diagnosing problems that occur at run-time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="13b82-106">hello 本文件中的步驟只適用於使用 Linux 的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="13b82-106">hello steps in this document only work with HDInsight clusters that use Linux.</span></span> <span data-ttu-id="13b82-107">Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。</span><span class="sxs-lookup"><span data-stu-id="13b82-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="13b82-108">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="13b82-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="13b82-109"><a name="whichServices"></a>服務</span><span class="sxs-lookup"><span data-stu-id="13b82-109"><a name="whichServices"></a>Services</span></span>

<span data-ttu-id="13b82-110">您可以啟用下列服務的 hello 的堆積傾印：</span><span class="sxs-lookup"><span data-stu-id="13b82-110">You can enable heap dumps for hello following services:</span></span>

* <span data-ttu-id="13b82-111">**hcatalog** - tempelton</span><span class="sxs-lookup"><span data-stu-id="13b82-111">**hcatalog** - tempelton</span></span>
* <span data-ttu-id="13b82-112">**hive** - hiveserver2、metastore、derbyserver</span><span class="sxs-lookup"><span data-stu-id="13b82-112">**hive** - hiveserver2, metastore, derbyserver</span></span>
* <span data-ttu-id="13b82-113">**mapreduce** - jobhistoryserver</span><span class="sxs-lookup"><span data-stu-id="13b82-113">**mapreduce** - jobhistoryserver</span></span>
* <span data-ttu-id="13b82-114">**yarn** - resourcemanager、nodemanager、timelineserver</span><span class="sxs-lookup"><span data-stu-id="13b82-114">**yarn** - resourcemanager, nodemanager, timelineserver</span></span>
* <span data-ttu-id="13b82-115">**hdfs** - datanode、secondarynamenode、namenode</span><span class="sxs-lookup"><span data-stu-id="13b82-115">**hdfs** - datanode, secondarynamenode, namenode</span></span>

<span data-ttu-id="13b82-116">您也可以啟用 hello 對應的堆積傾印，並減少 HDInsight 所執行的處理程序。</span><span class="sxs-lookup"><span data-stu-id="13b82-116">You can also enable heap dumps for hello map and reduce processes ran by HDInsight.</span></span>

## <span data-ttu-id="13b82-117"><a name="configuration"></a>了解堆積傾印組態</span><span class="sxs-lookup"><span data-stu-id="13b82-117"><a name="configuration"></a>Understanding heap dump configuration</span></span>

<span data-ttu-id="13b82-118">藉由傳遞選項會啟用堆積傾印 (有時稱為 opts，或參數) toohello JVM 時啟動服務。</span><span class="sxs-lookup"><span data-stu-id="13b82-118">Heap dumps are enabled by passing options (sometimes known as opts, or parameters) toohello JVM when a service is started.</span></span> <span data-ttu-id="13b82-119">對於大部分的 Hadoop 服務，您可以修改 hello 殼層使用指令碼 toostart hello 服務 toopass 這些選項。</span><span class="sxs-lookup"><span data-stu-id="13b82-119">For most Hadoop services, you can modify hello shell script used toostart hello service toopass these options.</span></span>

<span data-ttu-id="13b82-120">在每個指令碼中，沒有匯出 **\* \_OPTS**，其中包含 hello 選項傳遞 toohello JVM。</span><span class="sxs-lookup"><span data-stu-id="13b82-120">In each script, there is an export for **\*\_OPTS**, which contains hello options passed toohello JVM.</span></span> <span data-ttu-id="13b82-121">例如，在 hello **hadoop env.sh**指令碼開頭的 hello 列`export HADOOP_NAMENODE_OPTS=`包含 hello NameNode 服務的 hello 選項。</span><span class="sxs-lookup"><span data-stu-id="13b82-121">For example, in hello **hadoop-env.sh** script, hello line that begins with `export HADOOP_NAMENODE_OPTS=` contains hello options for hello NameNode service.</span></span>

<span data-ttu-id="13b82-122">對應並減少處理序都稍有不同，因為這些作業 hello MapReduce 服務的子處理序。</span><span class="sxs-lookup"><span data-stu-id="13b82-122">Map and reduce processes are slightly different, as these operations are a child process of hello MapReduce service.</span></span> <span data-ttu-id="13b82-123">每個對應，或降低處理序會執行子容器，而且有兩個項目包含 hello JVM 選項。</span><span class="sxs-lookup"><span data-stu-id="13b82-123">Each map or reduce process runs in a child container, and there are two entries that contain hello JVM options.</span></span> <span data-ttu-id="13b82-124">兩者均包含在 **mapred-site.xml** 中：</span><span class="sxs-lookup"><span data-stu-id="13b82-124">Both contained in **mapred-site.xml**:</span></span>

* <span data-ttu-id="13b82-125">**mapreduce.admin.map.child.java.opts**</span><span class="sxs-lookup"><span data-stu-id="13b82-125">**mapreduce.admin.map.child.java.opts**</span></span>
* <span data-ttu-id="13b82-126">**mapreduce.admin.reduce.child.java.opts**</span><span class="sxs-lookup"><span data-stu-id="13b82-126">**mapreduce.admin.reduce.child.java.opts**</span></span>

> [!NOTE]
> <span data-ttu-id="13b82-127">我們建議使用 Ambari toomodify 這兩個 hello 指令碼和 mapred-site.xml 設定為 Ambari 處理 hello 叢集節點之間複寫變更。</span><span class="sxs-lookup"><span data-stu-id="13b82-127">We recommend using Ambari toomodify both hello scripts and mapred-site.xml settings, as Ambari handle replicating changes across nodes in hello cluster.</span></span> <span data-ttu-id="13b82-128">請參閱 hello[使用 Ambari](#using-ambari) > 一節，如需特定步驟。</span><span class="sxs-lookup"><span data-stu-id="13b82-128">See hello [Using Ambari](#using-ambari) section for specific steps.</span></span>

### <a name="enable-heap-dumps"></a><span data-ttu-id="13b82-129">啟用堆積傾印</span><span class="sxs-lookup"><span data-stu-id="13b82-129">Enable heap dumps</span></span>

<span data-ttu-id="13b82-130">hello 下列選項可讓堆積傾印 OutOfMemoryError 發生時：</span><span class="sxs-lookup"><span data-stu-id="13b82-130">hello following option enables heap dumps when an OutOfMemoryError occurs:</span></span>

    -XX:+HeapDumpOnOutOfMemoryError

<span data-ttu-id="13b82-131">hello  **+** 表示會啟用此選項。</span><span class="sxs-lookup"><span data-stu-id="13b82-131">hello **+** indicates that this option is enabled.</span></span> <span data-ttu-id="13b82-132">hello 預設會停用。</span><span class="sxs-lookup"><span data-stu-id="13b82-132">hello default is disabled.</span></span>

> [!WARNING]
> <span data-ttu-id="13b82-133">堆積會啟用傾印不 HDInsight Hadoop 服務根據預設，如 hello 傾印檔案可能很大。</span><span class="sxs-lookup"><span data-stu-id="13b82-133">Heap dumps are not enabled for Hadoop services on HDInsight by default, as hello dump files can be large.</span></span> <span data-ttu-id="13b82-134">如果您不要啟用以進行疑難排解，請記得 toodisable 它們一旦您重現 hello 問題和收集的 hello 傾印檔案。</span><span class="sxs-lookup"><span data-stu-id="13b82-134">If you do enable them for troubleshooting, remember toodisable them once you have reproduced hello problem and gathered hello dump files.</span></span>

### <a name="dump-location"></a><span data-ttu-id="13b82-135">傾印位置</span><span class="sxs-lookup"><span data-stu-id="13b82-135">Dump location</span></span>

<span data-ttu-id="13b82-136">hello hello 傾印檔案的預設位置是 hello 目前工作目錄。</span><span class="sxs-lookup"><span data-stu-id="13b82-136">hello default location for hello dump file is hello current working directory.</span></span> <span data-ttu-id="13b82-137">您可以控制在 hello 檔案會儲存使用 hello 下列選項：</span><span class="sxs-lookup"><span data-stu-id="13b82-137">You can control where hello file is stored using hello following option:</span></span>

    -XX:HeapDumpPath=/path

<span data-ttu-id="13b82-138">例如，使用`-XX:HeapDumpPath=/tmp`導致 hello 傾印 toobe 儲存在 hello tec_rule 位於 /tmp 目錄中。</span><span class="sxs-lookup"><span data-stu-id="13b82-138">For example, using `-XX:HeapDumpPath=/tmp` causes hello dumps toobe stored in hello /tmp directory.</span></span>

### <a name="scripts"></a><span data-ttu-id="13b82-139">指令碼</span><span class="sxs-lookup"><span data-stu-id="13b82-139">Scripts</span></span>

<span data-ttu-id="13b82-140">您也可以在發生 **OutOfMemoryError** 時觸發指令碼。</span><span class="sxs-lookup"><span data-stu-id="13b82-140">You can also trigger a script when an **OutOfMemoryError** occurs.</span></span> <span data-ttu-id="13b82-141">例如，觸發通知，因此您知道該 hello 錯誤發生。</span><span class="sxs-lookup"><span data-stu-id="13b82-141">For example, triggering a notification so you know that hello error has occurred.</span></span> <span data-ttu-id="13b82-142">使用 hello 下列選項 tootrigger 指令碼__OutOfMemoryError__:</span><span class="sxs-lookup"><span data-stu-id="13b82-142">Use hello following option tootrigger a script on an __OutOfMemoryError__:</span></span>

    -XX:OnOutOfMemoryError=/path/to/script

> [!NOTE]
> <span data-ttu-id="13b82-143">由於 Hadoop 分散式的系統，使用任何指令碼必須放置在 hello hello 服務執行所在叢集的所有節點上。</span><span class="sxs-lookup"><span data-stu-id="13b82-143">Since Hadoop is a distributed system, any script used must be placed on all nodes in hello cluster that hello service runs on.</span></span>
> 
> <span data-ttu-id="13b82-144">hello 指令碼也必須是可存取之 hello hello 服務執行的帳戶，且必須提供的位置中執行的權限。</span><span class="sxs-lookup"><span data-stu-id="13b82-144">hello script must also be in a location that is accessible by hello account hello service runs as, and must provide execute permissions.</span></span> <span data-ttu-id="13b82-145">例如，您可能希望 toostore 指令碼中的`/usr/local/bin`並用`chmod go+rx /usr/local/bin/filename.sh`toogrant 讀取和執行權限。</span><span class="sxs-lookup"><span data-stu-id="13b82-145">For example, you may wish toostore scripts in `/usr/local/bin` and use `chmod go+rx /usr/local/bin/filename.sh` toogrant read and execute permissions.</span></span>

## <a name="using-ambari"></a><span data-ttu-id="13b82-146">使用 Ambari</span><span class="sxs-lookup"><span data-stu-id="13b82-146">Using Ambari</span></span>

<span data-ttu-id="13b82-147">服務中，使用下列步驟的 hello toomodify hello 設定：</span><span class="sxs-lookup"><span data-stu-id="13b82-147">toomodify hello configuration for a service, use hello following steps:</span></span>

1. <span data-ttu-id="13b82-148">開啟您的叢集，hello Ambari web UI。</span><span class="sxs-lookup"><span data-stu-id="13b82-148">Open hello Ambari web UI for your cluster.</span></span> <span data-ttu-id="13b82-149">https://YOURCLUSTERNAME.azurehdinsight.net hello URL。</span><span class="sxs-lookup"><span data-stu-id="13b82-149">hello URL is https://YOURCLUSTERNAME.azurehdinsight.net.</span></span>

    <span data-ttu-id="13b82-150">出現提示時，驗證 toohello 站台使用 hello HTTP 帳戶名稱 (預設： 系統管理員) 和密碼，供您的叢集。</span><span class="sxs-lookup"><span data-stu-id="13b82-150">When prompted, authenticate toohello site using hello HTTP account name (default: admin) and password for your cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="13b82-151">您可能會提示輸入第二次 Ambari hello 使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="13b82-151">You may be prompted a second time by Ambari for hello user name and password.</span></span> <span data-ttu-id="13b82-152">如果是的話，請輸入 hello 相同的帳戶名稱和密碼</span><span class="sxs-lookup"><span data-stu-id="13b82-152">If so, enter hello same account name and password</span></span>

2. <span data-ttu-id="13b82-153">使用 hello 清單 hello 左側，選取您想 toomodify hello 服務區域。</span><span class="sxs-lookup"><span data-stu-id="13b82-153">Using hello list of on hello left, select hello service area you want toomodify.</span></span> <span data-ttu-id="13b82-154">例如 **HDFS**。</span><span class="sxs-lookup"><span data-stu-id="13b82-154">For example, **HDFS**.</span></span> <span data-ttu-id="13b82-155">在 hello 中心區域中，選取 hello **Configs**  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="13b82-155">In hello center area, select hello **Configs** tab.</span></span>

    ![Ambari Web 圖片 (已選取 HDFS 設定索引標籤)](./media/hdinsight-hadoop-heap-dump-linux/serviceconfig.png)

3. <span data-ttu-id="13b82-157">使用 hello**篩選...**項目，請輸入**opts**。</span><span class="sxs-lookup"><span data-stu-id="13b82-157">Using hello **Filter...** entry, enter **opts**.</span></span> <span data-ttu-id="13b82-158">只會顯示包含此文字的項目。</span><span class="sxs-lookup"><span data-stu-id="13b82-158">Only items containing this text are displayed.</span></span>

    ![篩選的清單](./media/hdinsight-hadoop-heap-dump-linux/filter.png)

4. <span data-ttu-id="13b82-160">尋找 hello  **\* \_OPTS** hello 服務 tooenable 堆積的傾印，並將 hello 選項項目想 tooenable。</span><span class="sxs-lookup"><span data-stu-id="13b82-160">Find hello **\*\_OPTS** entry for hello service you want tooenable heap dumps for, and add hello options you wish tooenable.</span></span> <span data-ttu-id="13b82-161">在下列映像的 hello，我已將加入`-XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp/`toohello **HADOOP\_NAMENODE\_OPTS**項目：</span><span class="sxs-lookup"><span data-stu-id="13b82-161">In hello following image, I've added `-XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp/` toohello **HADOOP\_NAMENODE\_OPTS** entry:</span></span>

    ![含有 -XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp/ 的 HADOOP_NAMENODE_OPTS](./media/hdinsight-hadoop-heap-dump-linux/opts.png)

   > [!NOTE]
   > <span data-ttu-id="13b82-163">當啟用堆積傾印 hello 對應，或降低子處理序時，請尋找名為 hello 欄位**mapreduce.admin.map.child.java.opts**和**mapreduce.admin.reduce.child.java.opts**。</span><span class="sxs-lookup"><span data-stu-id="13b82-163">When enabling heap dumps for hello map or reduce child process, look for hello fields named **mapreduce.admin.map.child.java.opts** and **mapreduce.admin.reduce.child.java.opts**.</span></span>

    <span data-ttu-id="13b82-164">使用 hello**儲存**按鈕 toosave hello 變更。</span><span class="sxs-lookup"><span data-stu-id="13b82-164">Use hello **Save** button toosave hello changes.</span></span> <span data-ttu-id="13b82-165">您可以輸入簡短描述 hello 變更的附註。</span><span class="sxs-lookup"><span data-stu-id="13b82-165">You can enter a short note describing hello changes.</span></span>

5. <span data-ttu-id="13b82-166">套用 hello 變更之後, hello**需要重新啟動**一或多個服務旁邊的圖示會出現。</span><span class="sxs-lookup"><span data-stu-id="13b82-166">Once hello changes have been applied, hello **Restart required** icon appears beside one or more services.</span></span>

    ![必須重新啟動圖示和重新啟動按鈕](./media/hdinsight-hadoop-heap-dump-linux/restartrequiredicon.png)

6. <span data-ttu-id="13b82-168">選取每個服務，需要重新啟動，並使用 hello**服務動作**太按鈕**上維護模式開啟**。</span><span class="sxs-lookup"><span data-stu-id="13b82-168">Select each service that needs a restart, and use hello **Service Actions** button too**Turn On Maintenance Mode**.</span></span> <span data-ttu-id="13b82-169">維護模式會防止 hello 服務在重新啟動時所產生警示。</span><span class="sxs-lookup"><span data-stu-id="13b82-169">Maintenance mode prevents alerts from being generated from hello service when you restart it.</span></span>

    ![開啟維護模式功能表](./media/hdinsight-hadoop-heap-dump-linux/maintenancemode.png)

7. <span data-ttu-id="13b82-171">一旦您已啟用維護模式，使用 hello**重新啟動**太按鈕 hello 服務**重新啟動所有受影響的**</span><span class="sxs-lookup"><span data-stu-id="13b82-171">Once you have enabled maintenance mode, use hello **Restart** button for hello service too**Restart All Effected**</span></span>

    ![重新啟動所有受影響的項目](./media/hdinsight-hadoop-heap-dump-linux/restartbutton.png)

   > [!NOTE]
   > <span data-ttu-id="13b82-173">hello hello 的項目**重新啟動**可能不同的其他服務 按鈕。</span><span class="sxs-lookup"><span data-stu-id="13b82-173">hello entries for hello **Restart** button may be different for other services.</span></span>

8. <span data-ttu-id="13b82-174">一旦 hello 服務重新啟動後，使用 hello**服務動作**太按鈕**啟動維護模式**。</span><span class="sxs-lookup"><span data-stu-id="13b82-174">Once hello services have been restarted, use hello **Service Actions** button too**Turn Off Maintenance Mode**.</span></span> <span data-ttu-id="13b82-175">此監視的警示 hello 服務的 Ambari tooresume。</span><span class="sxs-lookup"><span data-stu-id="13b82-175">This Ambari tooresume monitoring for alerts for hello service.</span></span>

