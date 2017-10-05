---
title: "在 HDInsight 上啟用 Hadoop 服務的堆積傾印 - Azure | Microsoft Docs"
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
ms.openlocfilehash: 59942e989d622c2486edf181d76e13344c71e6f9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="enable-heap-dumps-for-hadoop-services-on-linux-based-hdinsight"></a><span data-ttu-id="71782-103">在以 Linux 為基礎的 HDInsight 上啟用 Hadoop 服務的堆積傾印</span><span class="sxs-lookup"><span data-stu-id="71782-103">Enable heap dumps for Hadoop services on Linux-based HDInsight</span></span>

[!INCLUDE [heapdump-selector](../../includes/hdinsight-selector-heap-dump.md)]

<span data-ttu-id="71782-104">堆積傾印含有應用程式記憶體的快照，其中包括建立傾印時的變數值。</span><span class="sxs-lookup"><span data-stu-id="71782-104">Heap dumps contain a snapshot of the application's memory, including the values of variables at the time the dump was created.</span></span> <span data-ttu-id="71782-105">因此它們有助於為執行階段發生的問題進行診斷。</span><span class="sxs-lookup"><span data-stu-id="71782-105">So they are useful for diagnosing problems that occur at run-time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="71782-106">本文件中的步驟只適用於使用 Linux 的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="71782-106">The steps in this document only work with HDInsight clusters that use Linux.</span></span> <span data-ttu-id="71782-107">Linux 是唯一使用於 HDInsight 3.4 版或更新版本的作業系統。</span><span class="sxs-lookup"><span data-stu-id="71782-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="71782-108">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="71782-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="71782-109"><a name="whichServices"></a>服務</span><span class="sxs-lookup"><span data-stu-id="71782-109"><a name="whichServices"></a>Services</span></span>

<span data-ttu-id="71782-110">您可以啟用下列服務的堆積傾印：</span><span class="sxs-lookup"><span data-stu-id="71782-110">You can enable heap dumps for the following services:</span></span>

* <span data-ttu-id="71782-111">**hcatalog** - tempelton</span><span class="sxs-lookup"><span data-stu-id="71782-111">**hcatalog** - tempelton</span></span>
* <span data-ttu-id="71782-112">**hive** - hiveserver2、metastore、derbyserver</span><span class="sxs-lookup"><span data-stu-id="71782-112">**hive** - hiveserver2, metastore, derbyserver</span></span>
* <span data-ttu-id="71782-113">**mapreduce** - jobhistoryserver</span><span class="sxs-lookup"><span data-stu-id="71782-113">**mapreduce** - jobhistoryserver</span></span>
* <span data-ttu-id="71782-114">**yarn** - resourcemanager、nodemanager、timelineserver</span><span class="sxs-lookup"><span data-stu-id="71782-114">**yarn** - resourcemanager, nodemanager, timelineserver</span></span>
* <span data-ttu-id="71782-115">**hdfs** - datanode、secondarynamenode、namenode</span><span class="sxs-lookup"><span data-stu-id="71782-115">**hdfs** - datanode, secondarynamenode, namenode</span></span>

<span data-ttu-id="71782-116">您也可以針對 HDInsight 所執行的 map 和 reduce 處理序來啟用堆積傾印。</span><span class="sxs-lookup"><span data-stu-id="71782-116">You can also enable heap dumps for the map and reduce processes ran by HDInsight.</span></span>

## <span data-ttu-id="71782-117"><a name="configuration"></a>了解堆積傾印組態</span><span class="sxs-lookup"><span data-stu-id="71782-117"><a name="configuration"></a>Understanding heap dump configuration</span></span>

<span data-ttu-id="71782-118">堆積傾印的啟用方式，是在服務啟動時將選項 (有時稱為參數) 傳遞至 JVM。</span><span class="sxs-lookup"><span data-stu-id="71782-118">Heap dumps are enabled by passing options (sometimes known as opts, or parameters) to the JVM when a service is started.</span></span> <span data-ttu-id="71782-119">就大部分的 Hadoop 服務而言，您可以修改用於啟動服務的殼層指令碼以略過這些選項。</span><span class="sxs-lookup"><span data-stu-id="71782-119">For most Hadoop services, you can modify the shell script used to start the service to pass these options.</span></span>

<span data-ttu-id="71782-120">在每個指令碼中，有一項 **\*\_OPTS** 匯出，其中含有傳遞至 JVM 的選項。</span><span class="sxs-lookup"><span data-stu-id="71782-120">In each script, there is an export for **\*\_OPTS**, which contains the options passed to the JVM.</span></span> <span data-ttu-id="71782-121">例如，在 **hadoop-env.sh** 指令碼中，以 `export HADOOP_NAMENODE_OPTS=` 為開頭的那一行即含有 NameNode 服務的選項。</span><span class="sxs-lookup"><span data-stu-id="71782-121">For example, in the **hadoop-env.sh** script, the line that begins with `export HADOOP_NAMENODE_OPTS=` contains the options for the NameNode service.</span></span>

<span data-ttu-id="71782-122">map 和 reduce 處理序會稍有不同，因為這些作業是 MapReduce 服務的子處理序。</span><span class="sxs-lookup"><span data-stu-id="71782-122">Map and reduce processes are slightly different, as these operations are a child process of the MapReduce service.</span></span> <span data-ttu-id="71782-123">每個 map 或 reduce 處理序都會在一個子容器中執行，且有兩個含有 JVM 選項的項目。</span><span class="sxs-lookup"><span data-stu-id="71782-123">Each map or reduce process runs in a child container, and there are two entries that contain the JVM options.</span></span> <span data-ttu-id="71782-124">兩者均包含在 **mapred-site.xml** 中：</span><span class="sxs-lookup"><span data-stu-id="71782-124">Both contained in **mapred-site.xml**:</span></span>

* <span data-ttu-id="71782-125">**mapreduce.admin.map.child.java.opts**</span><span class="sxs-lookup"><span data-stu-id="71782-125">**mapreduce.admin.map.child.java.opts**</span></span>
* <span data-ttu-id="71782-126">**mapreduce.admin.reduce.child.java.opts**</span><span class="sxs-lookup"><span data-stu-id="71782-126">**mapreduce.admin.reduce.child.java.opts**</span></span>

> [!NOTE]
> <span data-ttu-id="71782-127">我們建議使用 Ambari 來修改指令碼和 mapred-site.xml 設定，因為 Ambari 會處理叢集中跨節點的複寫變更。</span><span class="sxs-lookup"><span data-stu-id="71782-127">We recommend using Ambari to modify both the scripts and mapred-site.xml settings, as Ambari handle replicating changes across nodes in the cluster.</span></span> <span data-ttu-id="71782-128">如需特定的步驟，請參閱 [使用 Ambari](#using-ambari) 一節。</span><span class="sxs-lookup"><span data-stu-id="71782-128">See the [Using Ambari](#using-ambari) section for specific steps.</span></span>

### <a name="enable-heap-dumps"></a><span data-ttu-id="71782-129">啟用堆積傾印</span><span class="sxs-lookup"><span data-stu-id="71782-129">Enable heap dumps</span></span>

<span data-ttu-id="71782-130">以下選項可在發生 OutOfMemoryError 時啟用堆積傾印：</span><span class="sxs-lookup"><span data-stu-id="71782-130">The following option enables heap dumps when an OutOfMemoryError occurs:</span></span>

    -XX:+HeapDumpOnOutOfMemoryError

<span data-ttu-id="71782-131">**+** 表示已啟用此選項。</span><span class="sxs-lookup"><span data-stu-id="71782-131">The **+** indicates that this option is enabled.</span></span> <span data-ttu-id="71782-132">預設值為停用。</span><span class="sxs-lookup"><span data-stu-id="71782-132">The default is disabled.</span></span>

> [!WARNING]
> <span data-ttu-id="71782-133">根據預設不會在 HDInsight 上啟用 Hadoop 服務的堆積傾印，因為傾印檔案可能會很龐大。</span><span class="sxs-lookup"><span data-stu-id="71782-133">Heap dumps are not enabled for Hadoop services on HDInsight by default, as the dump files can be large.</span></span> <span data-ttu-id="71782-134">如果您為了進行疑難排解而啟用它們，請記得在重現問題並收集傾印檔案之後將其停用。</span><span class="sxs-lookup"><span data-stu-id="71782-134">If you do enable them for troubleshooting, remember to disable them once you have reproduced the problem and gathered the dump files.</span></span>

### <a name="dump-location"></a><span data-ttu-id="71782-135">傾印位置</span><span class="sxs-lookup"><span data-stu-id="71782-135">Dump location</span></span>

<span data-ttu-id="71782-136">傾印檔案的預設位置是目前的工作目錄。</span><span class="sxs-lookup"><span data-stu-id="71782-136">The default location for the dump file is the current working directory.</span></span> <span data-ttu-id="71782-137">您可以使用以下選項，控制檔案的儲存位置：</span><span class="sxs-lookup"><span data-stu-id="71782-137">You can control where the file is stored using the following option:</span></span>

    -XX:HeapDumpPath=/path

<span data-ttu-id="71782-138">例如，使用 `-XX:HeapDumpPath=/tmp` 會使傾印儲存在 /tmp 目錄中。</span><span class="sxs-lookup"><span data-stu-id="71782-138">For example, using `-XX:HeapDumpPath=/tmp` causes the dumps to be stored in the /tmp directory.</span></span>

### <a name="scripts"></a><span data-ttu-id="71782-139">指令碼</span><span class="sxs-lookup"><span data-stu-id="71782-139">Scripts</span></span>

<span data-ttu-id="71782-140">您也可以在發生 **OutOfMemoryError** 時觸發指令碼。</span><span class="sxs-lookup"><span data-stu-id="71782-140">You can also trigger a script when an **OutOfMemoryError** occurs.</span></span> <span data-ttu-id="71782-141">例如觸發通知，讓您知道發生了錯誤。</span><span class="sxs-lookup"><span data-stu-id="71782-141">For example, triggering a notification so you know that the error has occurred.</span></span> <span data-ttu-id="71782-142">使用下列選項可在發生 __OutOfMemoryError__ 時觸發指令碼：</span><span class="sxs-lookup"><span data-stu-id="71782-142">Use the following option to trigger a script on an __OutOfMemoryError__:</span></span>

    -XX:OnOutOfMemoryError=/path/to/script

> [!NOTE]
> <span data-ttu-id="71782-143">由於 Hadoop 是分散式系統，因此所有使用的指令碼都必須放置在服務所在叢集中的所有節點上。</span><span class="sxs-lookup"><span data-stu-id="71782-143">Since Hadoop is a distributed system, any script used must be placed on all nodes in the cluster that the service runs on.</span></span>
> 
> <span data-ttu-id="71782-144">指令碼也必須位於服務所屬的帳戶可以存取的位置中，而且必須提供執行權限。</span><span class="sxs-lookup"><span data-stu-id="71782-144">The script must also be in a location that is accessible by the account the service runs as, and must provide execute permissions.</span></span> <span data-ttu-id="71782-145">例如，您可能想要在 `/usr/local/bin` 中存放指令碼，並用 `chmod go+rx /usr/local/bin/filename.sh` 授與讀取和執行權限。</span><span class="sxs-lookup"><span data-stu-id="71782-145">For example, you may wish to store scripts in `/usr/local/bin` and use `chmod go+rx /usr/local/bin/filename.sh` to grant read and execute permissions.</span></span>

## <a name="using-ambari"></a><span data-ttu-id="71782-146">使用 Ambari</span><span class="sxs-lookup"><span data-stu-id="71782-146">Using Ambari</span></span>

<span data-ttu-id="71782-147">若要修改服務的組態，請依照下列步驟進行：</span><span class="sxs-lookup"><span data-stu-id="71782-147">To modify the configuration for a service, use the following steps:</span></span>

1. <span data-ttu-id="71782-148">開啟叢集的 Ambari Web UI。</span><span class="sxs-lookup"><span data-stu-id="71782-148">Open the Ambari web UI for your cluster.</span></span> <span data-ttu-id="71782-149">URL 為 https://YOURCLUSTERNAME.azurehdinsight.net。</span><span class="sxs-lookup"><span data-stu-id="71782-149">The URL is https://YOURCLUSTERNAME.azurehdinsight.net.</span></span>

    <span data-ttu-id="71782-150">出現提示時，請使用您叢集的 HTTP 帳戶名稱 (預設值：admin) 和密碼來向網站驗證。</span><span class="sxs-lookup"><span data-stu-id="71782-150">When prompted, authenticate to the site using the HTTP account name (default: admin) and password for your cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="71782-151">Ambari 可能會再次提示您輸入使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="71782-151">You may be prompted a second time by Ambari for the user name and password.</span></span> <span data-ttu-id="71782-152">此時，請輸入同一組帳戶名稱和密碼</span><span class="sxs-lookup"><span data-stu-id="71782-152">If so, enter the same account name and password</span></span>

2. <span data-ttu-id="71782-153">使用左側的清單，選取您想要修改的服務區域。</span><span class="sxs-lookup"><span data-stu-id="71782-153">Using the list of on the left, select the service area you want to modify.</span></span> <span data-ttu-id="71782-154">例如 **HDFS**。</span><span class="sxs-lookup"><span data-stu-id="71782-154">For example, **HDFS**.</span></span> <span data-ttu-id="71782-155">在中間區域內，選取 [設定]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="71782-155">In the center area, select the **Configs** tab.</span></span>

    ![Ambari Web 圖片 (已選取 HDFS 設定索引標籤)](./media/hdinsight-hadoop-heap-dump-linux/serviceconfig.png)

3. <span data-ttu-id="71782-157">在 [篩選...] 項目中輸入 **opts**。</span><span class="sxs-lookup"><span data-stu-id="71782-157">Using the **Filter...** entry, enter **opts**.</span></span> <span data-ttu-id="71782-158">只會顯示包含此文字的項目。</span><span class="sxs-lookup"><span data-stu-id="71782-158">Only items containing this text are displayed.</span></span>

    ![篩選的清單](./media/hdinsight-hadoop-heap-dump-linux/filter.png)

4. <span data-ttu-id="71782-160">針對您想要啟用堆積傾印的服務尋找 **\*\_OPTS** 項目，並新增您想要啟用的選項。</span><span class="sxs-lookup"><span data-stu-id="71782-160">Find the **\*\_OPTS** entry for the service you want to enable heap dumps for, and add the options you wish to enable.</span></span> <span data-ttu-id="71782-161">在下圖中，我將 `-XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp/` 新增至 **HADOOP\_NAMENODE\_OPTS** 項目：</span><span class="sxs-lookup"><span data-stu-id="71782-161">In the following image, I've added `-XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp/` to the **HADOOP\_NAMENODE\_OPTS** entry:</span></span>

    ![含有 -XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp/ 的 HADOOP_NAMENODE_OPTS](./media/hdinsight-hadoop-heap-dump-linux/opts.png)

   > [!NOTE]
   > <span data-ttu-id="71782-163">啟用 map 或 reduce 子處理序的堆積傾印時，請尋找名為 **mapreduce.admin.map.child.java.opts** 和 **mapreduce.admin.reduce.child.java.opts** 的欄位。</span><span class="sxs-lookup"><span data-stu-id="71782-163">When enabling heap dumps for the map or reduce child process, look for the fields named **mapreduce.admin.map.child.java.opts** and **mapreduce.admin.reduce.child.java.opts**.</span></span>

    <span data-ttu-id="71782-164">使用 [儲存] 按鈕來儲存變更。</span><span class="sxs-lookup"><span data-stu-id="71782-164">Use the **Save** button to save the changes.</span></span> <span data-ttu-id="71782-165">您可以輸入簡短的附註來說明所做的變更。</span><span class="sxs-lookup"><span data-stu-id="71782-165">You can enter a short note describing the changes.</span></span>

5. <span data-ttu-id="71782-166">套用變更後，一或多個服務旁邊就會出現**必須重新啟動**圖示。</span><span class="sxs-lookup"><span data-stu-id="71782-166">Once the changes have been applied, the **Restart required** icon appears beside one or more services.</span></span>

    ![必須重新啟動圖示和重新啟動按鈕](./media/hdinsight-hadoop-heap-dump-linux/restartrequiredicon.png)

6. <span data-ttu-id="71782-168">選取每個需要重新啟動的服務，並使用 [服務動作] 按鈕**開啟維護模式**。</span><span class="sxs-lookup"><span data-stu-id="71782-168">Select each service that needs a restart, and use the **Service Actions** button to **Turn On Maintenance Mode**.</span></span> <span data-ttu-id="71782-169">維護模式可避免您在重新啟動服務產生警示。</span><span class="sxs-lookup"><span data-stu-id="71782-169">Maintenance mode prevents alerts from being generated from the service when you restart it.</span></span>

    ![開啟維護模式功能表](./media/hdinsight-hadoop-heap-dump-linux/maintenancemode.png)

7. <span data-ttu-id="71782-171">啟用維護模式後，請使用服務的 [重新啟動] 按鈕來**重新啟動所有受影響的項目**。</span><span class="sxs-lookup"><span data-stu-id="71782-171">Once you have enabled maintenance mode, use the **Restart** button for the service to **Restart All Effected**</span></span>

    ![重新啟動所有受影響的項目](./media/hdinsight-hadoop-heap-dump-linux/restartbutton.png)

   > [!NOTE]
   > <span data-ttu-id="71782-173">其他服務的 [重新啟動] 按鈕項目可能會有所不同。</span><span class="sxs-lookup"><span data-stu-id="71782-173">the entries for the **Restart** button may be different for other services.</span></span>

8. <span data-ttu-id="71782-174">重新啟動服務後，請使用 [服務動作] 按鈕**關閉維護模式**。</span><span class="sxs-lookup"><span data-stu-id="71782-174">Once the services have been restarted, use the **Service Actions** button to **Turn Off Maintenance Mode**.</span></span> <span data-ttu-id="71782-175">這麼做可讓 Ambari 繼續監視服務是否有警示。</span><span class="sxs-lookup"><span data-stu-id="71782-175">This Ambari to resume monitoring for alerts for the service.</span></span>

