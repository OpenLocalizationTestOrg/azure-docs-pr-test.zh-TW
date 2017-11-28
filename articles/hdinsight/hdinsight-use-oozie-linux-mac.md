---
title: "aaaUse Hadoop Oozie 工作流程中以 Linux 為基礎的 HDInsight |Microsoft 文件"
description: "在 Linux 型 HDInsight 上使用 Hadoop Oozie。 深入了解如何 toodefine Oozie 工作流程，並提交 Oozie 作業。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: d7603471-5076-43d1-8b9a-dbc4e366ce5d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: larryfr
ms.openlocfilehash: cb5682837543312621e3424b7a9341b5d2a00bf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-oozie-with-hadoop-toodefine-and-run-a-workflow-on-linux-based-hdinsight"></a><span data-ttu-id="1c7eb-104">使用 Hadoop toodefine Oozie 和 Linux 為基礎的 HDInsight 上執行的工作流程</span><span class="sxs-lookup"><span data-stu-id="1c7eb-104">Use Oozie with Hadoop toodefine and run a workflow on Linux-based HDInsight</span></span>

[!INCLUDE [oozie-selector](../../includes/hdinsight-oozie-selector.md)]

<span data-ttu-id="1c7eb-105">深入了解如何 toouse Apache Oozie Hadoop HDInsight 上使用。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-105">Learn how toouse Apache Oozie with Hadoop on HDInsight.</span></span> <span data-ttu-id="1c7eb-106">Apache Oozie 是可管理 Hadoop 工作的工作流程/協調系統。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-106">Apache Oozie is a workflow/coordination system that manages Hadoop jobs.</span></span> <span data-ttu-id="1c7eb-107">Oozie hello Hadoop 堆疊，與整合並支援下列作業的 hello:</span><span class="sxs-lookup"><span data-stu-id="1c7eb-107">Oozie is integrated with hello Hadoop stack, and it supports hello following jobs:</span></span>

* <span data-ttu-id="1c7eb-108">Apache MapReduce</span><span class="sxs-lookup"><span data-stu-id="1c7eb-108">Apache MapReduce</span></span>
* <span data-ttu-id="1c7eb-109">Apache Pig</span><span class="sxs-lookup"><span data-stu-id="1c7eb-109">Apache Pig</span></span>
* <span data-ttu-id="1c7eb-110">Apache Hive</span><span class="sxs-lookup"><span data-stu-id="1c7eb-110">Apache Hive</span></span>
* <span data-ttu-id="1c7eb-111">Apache Sqoop</span><span class="sxs-lookup"><span data-stu-id="1c7eb-111">Apache Sqoop</span></span>

<span data-ttu-id="1c7eb-112">Oozie 也可以使用的 tooschedule 作業的特定 tooa 系統，例如 Java 程式或殼層指令碼</span><span class="sxs-lookup"><span data-stu-id="1c7eb-112">Oozie can also be used tooschedule jobs that are specific tooa system, like Java programs or shell scripts</span></span>

> [!NOTE]
> <span data-ttu-id="1c7eb-113">還有另一個選項可以定義與 HDInsight 搭配的工作流程，那就是 Azure Data Factory。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-113">Another option for defining workflows with HDInsight is Azure Data Factory.</span></span> <span data-ttu-id="1c7eb-114">toolearn 深入了解 Azure Data Factory，請參閱[搭配使用 Pig 和 Hive 與 Data Factory][azure-data-factory-pig-hive]。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-114">toolearn more about Azure Data Factory, see [Use Pig and Hive with Data Factory][azure-data-factory-pig-hive].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1c7eb-115">Oozie 未在已加入網域的 HDInsight 上啟用。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-115">Oozie is not enabled on domain-joined HDInsight.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1c7eb-116">必要條件</span><span class="sxs-lookup"><span data-stu-id="1c7eb-116">Prerequisites</span></span>

* <span data-ttu-id="1c7eb-117">**HDInsight 叢集**：請參閱 [開始使用 Linux 上的 HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="1c7eb-117">**An HDInsight cluster**: See [Get Started with HDInsight on Linux](hdinsight-hadoop-linux-tutorial-get-started.md)</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="1c7eb-118">本文件中的 hello 步驟需要使用 Linux 的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-118">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="1c7eb-119">Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-119">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="1c7eb-120">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-120">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="example-workflow"></a><span data-ttu-id="1c7eb-121">範例工作流程</span><span class="sxs-lookup"><span data-stu-id="1c7eb-121">Example workflow</span></span>

<span data-ttu-id="1c7eb-122">使用這份文件中的 hello 工作流程包含兩個動作。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-122">hello workflow used in this document contains two actions.</span></span> <span data-ttu-id="1c7eb-123">動作就是工作的定義，例如執行 Hive、Sqoop、MapReduce 或其他處理序：</span><span class="sxs-lookup"><span data-stu-id="1c7eb-123">Actions are definitions for tasks, such as running Hive, Sqoop, MapReduce, or other process:</span></span>

![Workflow diagram][img-workflow-diagram]

1. <span data-ttu-id="1c7eb-125">登錄區動作會在執行下列 HiveQL 指令碼 tooextract 記錄從 hello **hivesampletable**隨附 HDInsight。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-125">A Hive action runs a HiveQL script tooextract records from hello **hivesampletable** included with HDInsight.</span></span> <span data-ttu-id="1c7eb-126">每個資料列均代表來自特定行動裝置的瀏覽。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-126">Each row of data describes a visit from a specific mobile device.</span></span> <span data-ttu-id="1c7eb-127">hello 記錄格式會顯示下列文字類似 toohello:</span><span class="sxs-lookup"><span data-stu-id="1c7eb-127">hello record format appears similar toohello following text:</span></span>

        8       18:54:20        en-US   Android Samsung SCH-i500        California     United States    13.9204007      0       0
        23      19:19:44        en-US   Android HTC     Incredible      Pennsylvania   United States    NULL    0       0
        23      19:19:46        en-US   Android HTC     Incredible      Pennsylvania   United States    1.4757422       0       1

    <span data-ttu-id="1c7eb-128">hello 本文件中使用的 Hive 指令碼計算 hello 總造訪每個平台 （例如 Android 或 iPhone），並會儲存 hello 計數 tooa 新 Hive 資料表。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-128">hello Hive script used in this document counts hello total visits for each platform (such as Android or iPhone) and stores hello counts tooa new Hive table.</span></span>

    <span data-ttu-id="1c7eb-129">如需 Hive 的詳細資訊，請參閱[在 HDInsight 上使用 Hive][hdinsight-use-hive]。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-129">For more information about Hive, see [Use Hive with HDInsight][hdinsight-use-hive].</span></span>

2. <span data-ttu-id="1c7eb-130">Sqoop 動作會將匯出 hello 新 Hive 資料表 tooa 資料表中 Azure SQL database 的 hello 的內容。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-130">A Sqoop action exports hello contents of hello new Hive table tooa table in an Azure SQL database.</span></span> <span data-ttu-id="1c7eb-131">如需 Sqoop 的詳細資訊，請參閱[搭配 HDInsight 使用 Hadoop Sqoop][hdinsight-use-sqoop]。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-131">For more information about Sqoop, see [Use Hadoop Sqoop with HDInsight][hdinsight-use-sqoop].</span></span>

> [!NOTE]
> <span data-ttu-id="1c7eb-132">HDInsight 叢集上支援 Oozie 版本，請參閱[hello HDInsight 所提供的 Hadoop 叢集版本的新][hdinsight-versions]。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-132">For supported Oozie versions on HDInsight clusters, see [What's new in hello Hadoop cluster versions provided by HDInsight][hdinsight-versions].</span></span>

## <a name="create-hello-working-directory"></a><span data-ttu-id="1c7eb-133">建立 hello 工作目錄</span><span class="sxs-lookup"><span data-stu-id="1c7eb-133">Create hello working directory</span></span>

<span data-ttu-id="1c7eb-134">Oozie 必須要有資源所需作業 toobe 儲存在 hello 相同目錄。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-134">Oozie expects resources required for a job toobe stored in hello same directory.</span></span> <span data-ttu-id="1c7eb-135">這個範例會使用 **wasb:///tutorials/useoozie**。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-135">This example uses **wasb:///tutorials/useoozie**.</span></span> <span data-ttu-id="1c7eb-136">此目錄和 hello 保存 hello 由此工作流程建立新 Hive 資料表的資料目錄，請使用下列命令 toocreate hello:</span><span class="sxs-lookup"><span data-stu-id="1c7eb-136">Use hello following command toocreate this directory, and hello data directory that holds hello new Hive table created by this workflow:</span></span>

```
hdfs dfs -mkdir -p /tutorials/useoozie/data
```

> [!NOTE]
> <span data-ttu-id="1c7eb-137">hello`-p`參數會導致 hello 路徑 toobe 建立所有目錄。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-137">hello `-p` parameter causes all directories in hello path toobe created.</span></span> <span data-ttu-id="1c7eb-138">hello**資料**目錄是使用的 toohold 資料供 hello **useooziewf.hql**指令碼。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-138">hello **data** directory is used toohold data used by hello **useooziewf.hql** script.</span></span>

<span data-ttu-id="1c7eb-139">也請執行下列命令，可確保 Oozie 可以模擬使用者帳戶時執行的 Hive 和 Sqoop 工作 hello。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-139">Also run hello following command, which ensures that Oozie can impersonate your user account when running Hive and Sqoop jobs.</span></span> <span data-ttu-id="1c7eb-140">將 **USERNAME** 取代為您的登入名稱：</span><span class="sxs-lookup"><span data-stu-id="1c7eb-140">Replace **USERNAME** with your login name:</span></span>

```
sudo adduser USERNAME users
```

> [!NOTE]
> <span data-ttu-id="1c7eb-141">您可以忽略錯誤 hello 使用者已屬於 hello`users`群組。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-141">You can ignore errors that hello user is already a member of hello `users` group.</span></span>

## <a name="add-a-database-driver"></a><span data-ttu-id="1c7eb-142">新增資料庫驅動程式</span><span class="sxs-lookup"><span data-stu-id="1c7eb-142">Add a database driver</span></span>

<span data-ttu-id="1c7eb-143">由於此工作流程使用 Sqoop tooexport 資料 tooSQL 資料庫，您必須提供一份 hello JDBC 驅動程式使用 tootalk tooSQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-143">Since this workflow uses Sqoop tooexport data tooSQL Database, you must provide a copy of hello JDBC driver used tootalk tooSQL Database.</span></span> <span data-ttu-id="1c7eb-144">使用 hello 下列命令 toocopy 它 toohello 工作目錄：</span><span class="sxs-lookup"><span data-stu-id="1c7eb-144">Use hello following command toocopy it toohello working directory:</span></span>

```
hdfs dfs -put /usr/share/java/sqljdbc_4.1/enu/sqljdbc*.jar /tutorials/useoozie/
```

<span data-ttu-id="1c7eb-145">如果您的工作流程會使用其他資源，例如 jar，包含 MapReduce 應用程式，您需要 tooadd 以及這些資源。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-145">If your workflow used other resources, such as a jar containing a MapReduce application, you would need tooadd these resources as well.</span></span>

## <a name="define-hello-hive-query"></a><span data-ttu-id="1c7eb-146">定義 hello Hive 查詢</span><span class="sxs-lookup"><span data-stu-id="1c7eb-146">Define hello Hive query</span></span>

<span data-ttu-id="1c7eb-147">使用下列步驟 toocreate 下列 HiveQL 指令碼會定義的查詢，在本文件稍後的 Oozie 工作流程中使用的 hello。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-147">Use hello following steps toocreate a HiveQL script that defines a query, which is used in an Oozie workflow later in this document.</span></span>

1. <span data-ttu-id="1c7eb-148">Toohello 叢集使用 SSH 連線。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-148">Connect toohello cluster using SSH.</span></span> <span data-ttu-id="1c7eb-149">hello 下列命令會示範如何使用 hello`ssh`命令。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-149">hello following command is an example of using hello `ssh` command.</span></span> <span data-ttu-id="1c7eb-150">取代__USERNAME__與 hello SSH 使用者 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-150">Replace __USERNAME__ with hello SSH user for hello cluster.</span></span> <span data-ttu-id="1c7eb-151">取代__CLUSTERNAME__ hello hello HDInsight 叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-151">Replace __CLUSTERNAME__ with hello name of hello HDInsight cluster.</span></span>

    ```
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="1c7eb-152">如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-152">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="1c7eb-153">從 hello SSH 連線，使用下列命令 toocreate 檔案 hello:</span><span class="sxs-lookup"><span data-stu-id="1c7eb-153">From hello SSH connection, use hello following command toocreate a file:</span></span>

    ```
    nano useooziewf.hql
    ```

3. <span data-ttu-id="1c7eb-154">一旦 hello nano 編輯器隨即開啟，請使用 hello hello hello 檔案內容為下列查詢：</span><span class="sxs-lookup"><span data-stu-id="1c7eb-154">Once hello nano editor opens, use hello following query as hello contents of hello file:</span></span>

    ```hiveql
    DROP TABLE ${hiveTableName};
    CREATE EXTERNAL TABLE ${hiveTableName}(deviceplatform string, count string) ROW FORMAT DELIMITED
    FIELDS TERMINATED BY '\t' STORED AS TEXTFILE LOCATION '${hiveDataFolder}';
    INSERT OVERWRITE TABLE ${hiveTableName} SELECT deviceplatform, COUNT(*) as count FROM hivesampletable GROUP BY deviceplatform;
    ```

    <span data-ttu-id="1c7eb-155">有兩個 hello 指令碼中使用的變數：</span><span class="sxs-lookup"><span data-stu-id="1c7eb-155">There are two variables used in hello script:</span></span>

    * <span data-ttu-id="1c7eb-156">**${hiveTableName}**： 包含建立 hello 資料表 toobe hello 名稱</span><span class="sxs-lookup"><span data-stu-id="1c7eb-156">**${hiveTableName}**: contains hello name of hello table toobe created</span></span>

    * <span data-ttu-id="1c7eb-157">**${hiveDataFolder}**： 包含 hello toostore hello 資料檔案位置 hello 資料表</span><span class="sxs-lookup"><span data-stu-id="1c7eb-157">**${hiveDataFolder}**: contains hello location toostore hello data files for hello table</span></span>

    <span data-ttu-id="1c7eb-158">hello 工作流程定義檔 (在本教學課程 workflow.xml) 傳遞這些值 toothis 下列 HiveQL 指令碼在執行階段</span><span class="sxs-lookup"><span data-stu-id="1c7eb-158">hello workflow definition file (workflow.xml in this tutorial) passes these values toothis HiveQL script at run time</span></span>

4. <span data-ttu-id="1c7eb-159">tooexit hello 編輯器 中，按下 Ctrl X。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-159">tooexit hello editor, press Ctrl-X.</span></span> <span data-ttu-id="1c7eb-160">出現提示時，選取**Y** toosave hello 檔案，然後使用**Enter** toouse hello **useooziewf.hql**檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-160">When prompted, select **Y** toosave hello file, then use **Enter** toouse hello **useooziewf.hql** file name.</span></span>

5. <span data-ttu-id="1c7eb-161">使用 hello 下列命令 toocopy **useooziewf.hql**太**wasb:///tutorials/useoozie/useooziewf.hql**:</span><span class="sxs-lookup"><span data-stu-id="1c7eb-161">Use hello following commands toocopy **useooziewf.hql** too**wasb:///tutorials/useoozie/useooziewf.hql**:</span></span>

    ```
    hdfs dfs -put useooziewf.hql /tutorials/useoozie/useooziewf.hql
    ```

    <span data-ttu-id="1c7eb-162">這些命令儲存 hello **useooziewf.hql** hello 叢集 hello HDFS 相容存放裝置上的檔案。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-162">These commands store hello **useooziewf.hql** file on hello HDFS-compatible storage for hello cluster.</span></span>

## <a name="define-hello-workflow"></a><span data-ttu-id="1c7eb-163">定義 hello 工作流程</span><span class="sxs-lookup"><span data-stu-id="1c7eb-163">Define hello workflow</span></span>

<span data-ttu-id="1c7eb-164">Oozie 工作流程定義是以 hPDL 撰寫 (一種 XML 程序定義語言)。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-164">Oozie workflows definitions are written in hPDL (an XML Process Definition Language).</span></span> <span data-ttu-id="1c7eb-165">使用下列步驟 toodefine hello 工作流程的 hello:</span><span class="sxs-lookup"><span data-stu-id="1c7eb-165">Use hello following steps toodefine hello workflow:</span></span>

1. <span data-ttu-id="1c7eb-166">使用下列陳述式 toocreate hello 和編輯新檔案：</span><span class="sxs-lookup"><span data-stu-id="1c7eb-166">Use hello following statement toocreate and edit a new file:</span></span>

    ```
    nano workflow.xml
    ```

2. <span data-ttu-id="1c7eb-167">一旦 hello nano 編輯器隨即開啟，請輸入 hello hello 檔案內容為下列 XML:</span><span class="sxs-lookup"><span data-stu-id="1c7eb-167">Once hello nano editor opens, enter hello following XML as hello file contents:</span></span>

    ```xml
    <workflow-app name="useooziewf" xmlns="uri:oozie:workflow:0.2">
        <start too= "RunHiveScript"/>
        <action name="RunHiveScript">
        <hive xmlns="uri:oozie:hive-action:0.2">
            <job-tracker>${jobTracker}</job-tracker>
            <name-node>${nameNode}</name-node>
            <configuration>
            <property>
                <name>mapred.job.queue.name</name>
                <value>${queueName}</value>
            </property>
            </configuration>
            <script>${hiveScript}</script>
            <param>hiveTableName=${hiveTableName}</param>
            <param>hiveDataFolder=${hiveDataFolder}</param>
        </hive>
        <ok to="RunSqoopExport"/>
        <error to="fail"/>
        </action>
        <action name="RunSqoopExport">
        <sqoop xmlns="uri:oozie:sqoop-action:0.2">
            <job-tracker>${jobTracker}</job-tracker>
            <name-node>${nameNode}</name-node>
            <configuration>
            <property>
                <name>mapred.compress.map.output</name>
                <value>true</value>
            </property>
            </configuration>
            <arg>export</arg>
            <arg>--connect</arg>
            <arg>${sqlDatabaseConnectionString}</arg>
            <arg>--table</arg>
            <arg>${sqlDatabaseTableName}</arg>
            <arg>--export-dir</arg>
            <arg>${hiveDataFolder}</arg>
            <arg>-m</arg>
            <arg>1</arg>
            <arg>--input-fields-terminated-by</arg>
            <arg>"\t"</arg>
            <archive>sqljdbc41.jar</archive>
            </sqoop>
        <ok to="end"/>
        <error to="fail"/>
        </action>
        <kill name="fail">
        <message>Job failed, error message[${wf:errorMessage(wf:lastErrorNode())}] </message>
        </kill>
        <end name="end"/>
    </workflow-app>
    ```

    <span data-ttu-id="1c7eb-168">有兩個 hello 工作流程中定義的動作：</span><span class="sxs-lookup"><span data-stu-id="1c7eb-168">There are two actions defined in hello workflow:</span></span>

   * <span data-ttu-id="1c7eb-169">**RunHiveScript**: hello 開始的動作，此動作，並執行 hello **useooziewf.hql** Hive 指令碼</span><span class="sxs-lookup"><span data-stu-id="1c7eb-169">**RunHiveScript**: This action is hello start action, and runs hello **useooziewf.hql** Hive script</span></span>

   * <span data-ttu-id="1c7eb-170">**RunSqoopExport**： 這個動作將匯出的 hello 資料所建立的 hello Hive 指令碼 tooSQL Sqoop 資料庫。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-170">**RunSqoopExport**: This action exports hello data created from hello Hive script tooSQL Database using Sqoop.</span></span> <span data-ttu-id="1c7eb-171">這個動作才會執行 hello **RunHiveScript**動作是否成功。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-171">This action only runs if hello **RunHiveScript** action is successful.</span></span>

     <span data-ttu-id="1c7eb-172">hello 工作流程中有數個項目，例如`${jobTracker}`。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-172">hello workflow has several entries, such as `${jobTracker}`.</span></span> <span data-ttu-id="1c7eb-173">這些項目會以您在 hello 工作定義中使用的值取代。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-173">These entries are replaced by values you use in hello job definition.</span></span> <span data-ttu-id="1c7eb-174">在本文件稍後建立 hello 工作定義。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-174">hello job definition is created later in this document.</span></span>

     <span data-ttu-id="1c7eb-175">也請注意 hello `<archive>sqljdbc4.jar</arcive>` hello Sqoop > 一節中的項目。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-175">Also note hello `<archive>sqljdbc4.jar</arcive>` entry in hello Sqoop section.</span></span> <span data-ttu-id="1c7eb-176">此項目執行此動作時，指示 Oozie toomake Sqoop 可用在此封存。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-176">This entry instructs Oozie toomake this archive available for Sqoop when this action runs.</span></span>

3. <span data-ttu-id="1c7eb-177">然後使用 Ctrl-X **Y**和**Enter** toosave hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-177">Use Ctrl-X, then **Y** and **Enter** toosave hello file.</span></span>

4. <span data-ttu-id="1c7eb-178">使用 hello 下列命令 toocopy hello **workflow.xml**檔案太**/tutorials/useoozie/workflow.xml**:</span><span class="sxs-lookup"><span data-stu-id="1c7eb-178">Use hello following command toocopy hello **workflow.xml** file too**/tutorials/useoozie/workflow.xml**:</span></span>

    ```
    hdfs dfs -put workflow.xml /tutorials/useoozie/workflow.xml
    ```

## <a name="create-hello-database"></a><span data-ttu-id="1c7eb-179">建立 hello 資料庫</span><span class="sxs-lookup"><span data-stu-id="1c7eb-179">Create hello database</span></span>

<span data-ttu-id="1c7eb-180">Azure SQL Database，toocreate hello 中步驟 hello[建立 SQL Database](../sql-database/sql-database-get-started.md)文件。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-180">toocreate an Azure SQL Database, follow hello steps in hello [Create a SQL Database](../sql-database/sql-database-get-started.md) document.</span></span> <span data-ttu-id="1c7eb-181">建立 hello 資料庫時，使用`oozietest`與 hello 資料庫名稱。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-181">When creating hello database, use `oozietest` as hello database name.</span></span> <span data-ttu-id="1c7eb-182">也請記下 hello hello 資料庫伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-182">Also make a note of hello name of hello database server.</span></span>

### <a name="create-hello-table"></a><span data-ttu-id="1c7eb-183">建立 hello 資料表</span><span class="sxs-lookup"><span data-stu-id="1c7eb-183">Create hello table</span></span>

> [!NOTE]
> <span data-ttu-id="1c7eb-184">有許多方式 tooconnect tooSQL 資料庫 toocreate 資料表。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-184">There are many ways tooconnect tooSQL Database toocreate a table.</span></span> <span data-ttu-id="1c7eb-185">hello 下列步驟使用[freetds 才能使用](http://www.freetds.org/)從 hello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-185">hello following steps use [FreeTDS](http://www.freetds.org/) from hello HDInsight cluster.</span></span>


1. <span data-ttu-id="1c7eb-186">使用下列命令 tooinstall freetds 才能使用 hello HDInsight 叢集上的 hello:</span><span class="sxs-lookup"><span data-stu-id="1c7eb-186">Use hello following command tooinstall FreeTDS on hello HDInsight cluster:</span></span>

    ```
    sudo apt-get --assume-yes install freetds-dev freetds-bin
    ```

2. <span data-ttu-id="1c7eb-187">一旦安裝 freetds 才能使用之後，使用下列命令 tooconnect toohello SQL Database 伺服器您先前建立的 hello:</span><span class="sxs-lookup"><span data-stu-id="1c7eb-187">Once FreeTDS has been installed, use hello following command tooconnect toohello SQL Database server you created previously:</span></span>

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <sqlLogin> -P <sqlPassword> -p 1433 -D oozietest
    ```

    <span data-ttu-id="1c7eb-188">您收到的輸出類似 toohello 下列文字：</span><span class="sxs-lookup"><span data-stu-id="1c7eb-188">You receive output similar toohello following text:</span></span>

        locale is "en_US.UTF-8"
        locale charset is "UTF-8"
        using default charset "UTF-8"
        Default database being set toooozietest
        1>

3. <span data-ttu-id="1c7eb-189">在 hello`1>`提示字元中，輸入下列行 hello:</span><span class="sxs-lookup"><span data-stu-id="1c7eb-189">At hello `1>` prompt, enter hello following lines:</span></span>

    ```
    CREATE TABLE [dbo].[mobiledata](
    [deviceplatform] [nvarchar](50),
    [count] [bigint])
    GO
    CREATE CLUSTERED INDEX mobiledata_clustered_index on mobiledata(deviceplatform)
    GO
    ```

    <span data-ttu-id="1c7eb-190">當 hello`GO`輸入陳述式、 評估 hello 前一個陳述式。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-190">When hello `GO` statement is entered, hello previous statements are evaluated.</span></span> <span data-ttu-id="1c7eb-191">這些陳述式建立了名為**mobiledata** ，會由 hello 工作流程。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-191">These statements create a table named **mobiledata** that is used by hello workflow.</span></span>

    <span data-ttu-id="1c7eb-192">已建立下列 hello 資料表的 tooverify 使用 hello:</span><span class="sxs-lookup"><span data-stu-id="1c7eb-192">Use hello following tooverify that hello table has been created:</span></span>

    ```
    SELECT * FROM information_schema.tables
    GO
    ```

    <span data-ttu-id="1c7eb-193">您會看到下列文字的輸出類似 toohello:</span><span class="sxs-lookup"><span data-stu-id="1c7eb-193">You see output similar toohello following text:</span></span>

    ```
    TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
    oozietest       dbo     mobiledata      BASE TABLE
    ```

4. <span data-ttu-id="1c7eb-194">輸入`exit`在 hello`1>`提示 tooexit hello tsql 公用程式。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-194">Enter `exit` at hello `1>` prompt tooexit hello tsql utility.</span></span>

## <a name="create-hello-job-definition"></a><span data-ttu-id="1c7eb-195">建立 hello 工作定義</span><span class="sxs-lookup"><span data-stu-id="1c7eb-195">Create hello job definition</span></span>

<span data-ttu-id="1c7eb-196">hello 工作定義描述 toofind hello workflow.xml 的位置。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-196">hello job definition describes where toofind hello workflow.xml.</span></span> <span data-ttu-id="1c7eb-197">它也會描述 where toofind hello 工作流程 （例如 useooziewf.hql。) 所使用的其他檔案它也會定義 hello 值的屬性 hello 工作流程中使用，而且相關聯的檔案。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-197">It also describes where toofind other files used by hello workflow (such as useooziewf.hql.) It also defines hello values for properties used within hello workflow and associated files.</span></span>

1. <span data-ttu-id="1c7eb-198">使用下列命令 tooget hello 完整位址 hello 預設儲存體的 hello。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-198">Use hello following command tooget hello full address of hello default storage.</span></span> <span data-ttu-id="1c7eb-199">Hello 設定檔中會使用此位址，在不久後：</span><span class="sxs-lookup"><span data-stu-id="1c7eb-199">This address is used in hello configuration file in a moment:</span></span>

    ```
    sed -n '/<name>fs.default/,/<\/value>/p' /etc/hadoop/conf/core-site.xml
    ```

    <span data-ttu-id="1c7eb-200">此命令會傳回下列 XML 的資訊類似 toohello:</span><span class="sxs-lookup"><span data-stu-id="1c7eb-200">This command returns information similar toohello following XML:</span></span>

    ```xml
    <name>fs.defaultFS</name>
    <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net</value>
    ```

    > [!NOTE]
    > <span data-ttu-id="1c7eb-201">如果 hello HDInsight 叢集會使用 Azure 儲存體為 hello 預設儲存體，hello`<value>`項目內容的開頭`wasb://`。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-201">If hello HDInsight cluster uses Azure Storage as hello default storage, hello `<value>` element contents begin with `wasb://`.</span></span> <span data-ttu-id="1c7eb-202">若改為使用 Azure Data Lake Store，則其開頭將會是 `adl://`。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-202">If Azure Data Lake Store is used instead, it begins with `adl://`.</span></span>

    <span data-ttu-id="1c7eb-203">儲存 hello hello 內容`<value>`元素，因為它用於 hello 接下來的步驟。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-203">Save hello contents of hello `<value>` element, as it is used in hello next steps.</span></span>

2. <span data-ttu-id="1c7eb-204">使用下列命令 tooget hello 叢集前端節點的 FQDN 的 hello。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-204">Use hello following command tooget FQDN of hello cluster headnode.</span></span> <span data-ttu-id="1c7eb-205">這項資訊可用於 hello JobTracker hello 叢集位址：</span><span class="sxs-lookup"><span data-stu-id="1c7eb-205">This information is used for hello JobTracker address for hello cluster:</span></span>

    ```
    hostname -f
    ```

    <span data-ttu-id="1c7eb-206">這會傳回資訊的類似 toohello 下列文字：</span><span class="sxs-lookup"><span data-stu-id="1c7eb-206">This returns information similar toohello following text:</span></span>

    ```hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net```

    <span data-ttu-id="1c7eb-207">hello 使用連接埠 hello JobTracker 是 8050，因此 hello 完整位址 toouse hello JobTracker `hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8050`。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-207">hello port used for hello JobTracker is 8050, so hello full address toouse for hello JobTracker is `hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8050`.</span></span>

3. <span data-ttu-id="1c7eb-208">使用下列 toocreate hello Oozie 工作定義組態 hello:</span><span class="sxs-lookup"><span data-stu-id="1c7eb-208">Use hello following toocreate hello Oozie job definition configuration:</span></span>

    ```
    nano job.xml
    ```

4. <span data-ttu-id="1c7eb-209">一旦 hello nano 編輯器隨即開啟，請使用 hello hello hello 檔案內容為下列 XML:</span><span class="sxs-lookup"><span data-stu-id="1c7eb-209">Once hello nano editor opens, use hello following XML as hello contents of hello file:</span></span>

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>

        <property>
        <name>nameNode</name>
        <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net</value>
        </property>

        <property>
        <name>jobTracker</name>
        <value>JOBTRACKERADDRESS</value>
        </property>

        <property>
        <name>queueName</name>
        <value>default</value>
        </property>

        <property>
        <name>oozie.use.system.libpath</name>
        <value>true</value>
        </property>

        <property>
        <name>hiveScript</name>
        <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie/useooziewf.hql</value>
        </property>

        <property>
        <name>hiveTableName</name>
        <value>mobilecount</value>
        </property>

        <property>
        <name>hiveDataFolder</name>
        <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie/data</value>
        </property>

        <property>
        <name>sqlDatabaseConnectionString</name>
        <value>"jdbc:sqlserver://serverName.database.windows.net;user=adminLogin;password=adminPassword;database=oozietest"</value>
        </property>

        <property>
        <name>sqlDatabaseTableName</name>
        <value>mobiledata</value>
        </property>

        <property>
        <name>user.name</name>
        <value>YourName</value>
        </property>

        <property>
        <name>oozie.wf.application.path</name>
        <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie</value>
        </property>
    </configuration>
    ```

   * <span data-ttu-id="1c7eb-210">所有執行個體 **wasb://mycontainer@mystorageaccount.blob.core.windows.net** 預設儲存體之前收到 hello 值。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-210">Replace all instances of **wasb://mycontainer@mystorageaccount.blob.core.windows.net** with hello value you received earlier for default storage.</span></span>

     > [!WARNING]
     > <span data-ttu-id="1c7eb-211">如果 hello 路徑`wasb`路徑，您必須使用 hello 完整路徑。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-211">If hello path is a `wasb` path, you must use hello full path.</span></span> <span data-ttu-id="1c7eb-212">請勿它縮短 toojust `wasb:///`。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-212">Do not shorten it toojust `wasb:///`.</span></span>

   * <span data-ttu-id="1c7eb-213">取代**JOBTRACKERADDRESS**以 hello 您稍早收到 JobTracker/ResourceManager 位址。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-213">Replace **JOBTRACKERADDRESS** with hello JobTracker/ResourceManager address you received earlier.</span></span>
   * <span data-ttu-id="1c7eb-214">取代**YourName**與 hello HDInsight 叢集的登入名稱。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-214">Replace **YourName** with your login name for hello HDInsight cluster.</span></span>
   * <span data-ttu-id="1c7eb-215">取代**serverName**， **adminLogin**，和**adminPassword** hello Azure SQL database 的資訊。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-215">Replace **serverName**, **adminLogin**, and **adminPassword** with hello information for your Azure SQL Database.</span></span>

     <span data-ttu-id="1c7eb-216">大部分的此檔案中的 hello 資訊是使用的 toopopulate hello 值用於 hello workflow.xml 或 ooziewf.hql 檔 （例如 ${nameNode}。）</span><span class="sxs-lookup"><span data-stu-id="1c7eb-216">Most of hello information in this file is used toopopulate hello values used in hello workflow.xml or ooziewf.hql files (such as ${nameNode}.)</span></span>

     > [!NOTE]
     > <span data-ttu-id="1c7eb-217">hello **oozie.wf.application.path**項目會定義 where toofind hello workflow.xml 檔案，其中包含 hello 工作流程執行此作業。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-217">hello **oozie.wf.application.path** entry defines where toofind hello workflow.xml file, which contains hello workflow ran by this job.</span></span>

5. <span data-ttu-id="1c7eb-218">然後使用 Ctrl-X **Y**和**Enter** toosave hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-218">Use Ctrl-X, then **Y** and **Enter** toosave hello file.</span></span>

## <a name="submit-and-manage-hello-job"></a><span data-ttu-id="1c7eb-219">送出並管理 hello 工作</span><span class="sxs-lookup"><span data-stu-id="1c7eb-219">Submit and manage hello job</span></span>

<span data-ttu-id="1c7eb-220">hello 下列步驟使用 hello Oozie 命令 toosubmit 和管理 Oozie hello 叢集上的工作流程。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-220">hello following steps use hello Oozie command toosubmit and manage Oozie workflows on hello cluster.</span></span> <span data-ttu-id="1c7eb-221">hello Oozie 命令是容易使用的介面，透過 hello [Oozie REST API](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html)。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-221">hello Oozie command is a friendly interface over hello [Oozie REST API](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1c7eb-222">當使用 hello Oozie 命令時，您必須使用 hello FQDN 的 hello HDInsight 叢集前端節點。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-222">When using hello Oozie command, you must use hello FQDN for hello HDInsight headnode.</span></span> <span data-ttu-id="1c7eb-223">這個 FQDN 只能存取從 hello 叢集或 hello 叢集是否在 Azure 虛擬網路上，從 hello 上的其他機器相同網路。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-223">This FQDN is only accessible from hello cluster, or if hello cluster is on an Azure Virtual Network, from other machines on hello same network.</span></span>


1. <span data-ttu-id="1c7eb-224">使用下列 tooobtain hello URL toohello Oozie service hello:</span><span class="sxs-lookup"><span data-stu-id="1c7eb-224">Use hello following tooobtain hello URL toohello Oozie service:</span></span>

    ```
    sed -n '/<name>oozie.base.url/,/<\/value>/p' /etc/oozie/conf/oozie-site.xml
    ```

    <span data-ttu-id="1c7eb-225">這會傳回下列 XML 的資訊類似 toohello:</span><span class="sxs-lookup"><span data-stu-id="1c7eb-225">This returns information similar toohello following XML:</span></span>

    ```xml
    <name>oozie.base.url</name>
    <value>http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie</value>
    ```

    <span data-ttu-id="1c7eb-226">hello`http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie`部分是 hello URL toouse 以 hello Oozie 命令。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-226">hello `http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie` portion is hello URL toouse with hello Oozie command.</span></span>

2. <span data-ttu-id="1c7eb-227">使用 hello hello url 遵循 toocreate 環境變數，所以您不需 tootype 會針對每個命令：</span><span class="sxs-lookup"><span data-stu-id="1c7eb-227">Use hello following toocreate an environment variable for hello URL, so you don't have tootype it for every command:</span></span>

    ```
    export OOZIE_URL=http://HOSTNAMEt:11000/oozie
    ```

    <span data-ttu-id="1c7eb-228">取代為您稍早收到 hello hello URL。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-228">Replace hello URL with hello one you received earlier.</span></span>
3. <span data-ttu-id="1c7eb-229">使用下列 toosubmit hello 作業 hello:</span><span class="sxs-lookup"><span data-stu-id="1c7eb-229">Use hello following toosubmit hello job:</span></span>

    ```
    oozie job -config job.xml -submit
    ```

    <span data-ttu-id="1c7eb-230">這個命令載入 hello 作業資訊從**job.xml**並將它提交 tooOozie，但無法執行它。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-230">This command loads hello job information from **job.xml** and submits it tooOozie, but does not run it.</span></span>

    <span data-ttu-id="1c7eb-231">Hello 命令完成之後，它應該傳回 hello hello 作業識別碼。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-231">Once hello command completes, it should return hello ID of hello job.</span></span> <span data-ttu-id="1c7eb-232">例如： `0000005-150622124850154-oozie-oozi-W`。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-232">For example, `0000005-150622124850154-oozie-oozi-W`.</span></span> <span data-ttu-id="1c7eb-233">這個識別碼是使用的 toomanage hello 作業。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-233">This ID is used toomanage hello job.</span></span>

4. <span data-ttu-id="1c7eb-234">使用下列命令的 hello hello 工作檢視 hello 狀態：</span><span class="sxs-lookup"><span data-stu-id="1c7eb-234">View hello status of hello job using hello following command:</span></span>

    ```
    oozie job -info <JOBID>
    ```

    > [!NOTE]
    > <span data-ttu-id="1c7eb-235">取代`<JOBID>`hello 上一個步驟中傳回以 hello 識別碼。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-235">Replace `<JOBID>` with hello ID returned in hello previous step.</span></span>

    <span data-ttu-id="1c7eb-236">這會傳回資訊的類似 toohello 下列文字：</span><span class="sxs-lookup"><span data-stu-id="1c7eb-236">This returns information similar toohello following text:</span></span>

    ```
    Job ID : 0000005-150622124850154-oozie-oozi-W
    ------------------------------------------------------------------------------------------------------------------------------------
    Workflow Name : useooziewf
    App Path      : wasb:///tutorials/useoozie
    Status        : PREP
    Run           : 0
    User          : USERNAME
    Group         : -
    Created       : 2015-06-22 15:06 GMT
    Started       : -
    Last Modified : 2015-06-22 15:06 GMT
    Ended         : -
    CoordAction ID: -
    ------------------------------------------------------------------------------------------------------------------------------------
    ```

    <span data-ttu-id="1c7eb-237">這項工作的狀態為 `PREP`。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-237">This job has a status of `PREP`.</span></span> <span data-ttu-id="1c7eb-238">這個狀態表示該 hello 作業所建立，但不是會啟動。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-238">This status indicates that hello job was created, but not started.</span></span>

5. <span data-ttu-id="1c7eb-239">使用下列命令 toostart hello 作業 hello:</span><span class="sxs-lookup"><span data-stu-id="1c7eb-239">Use hello following command toostart hello job:</span></span>

    ```
    oozie job -start JOBID
    ```

    > [!NOTE]
    > <span data-ttu-id="1c7eb-240">取代`<JOBID>`以 hello 識別碼傳回前面。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-240">Replace `<JOBID>` with hello ID returned previously.</span></span>

    <span data-ttu-id="1c7eb-241">如果您檢查 hello 狀態這個命令之後，它處於執行狀態，並傳回 hello 作業中的 hello 動作的資訊。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-241">If you check hello status after this command, it is in a running state, and information is returned for hello actions within hello job.</span></span>

6. <span data-ttu-id="1c7eb-242">一旦 hello 工作順利完成，您可以確認 hello 資料產生 toohello SQL 資料庫資料表使用匯出的 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="1c7eb-242">Once hello task completes successfully, you can verify that hello data was generated and exported toohello SQL Database table by using hello following commands:</span></span>

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D oozietest
    ```

    <span data-ttu-id="1c7eb-243">在 hello`1>`提示字元中，輸入下列查詢的 hello:</span><span class="sxs-lookup"><span data-stu-id="1c7eb-243">At hello `1>` prompt, enter hello following query:</span></span>

    ```
    SELECT * FROM mobiledata
    GO
    ```

    <span data-ttu-id="1c7eb-244">傳回的 hello 資訊是類似 toohello 下列文字：</span><span class="sxs-lookup"><span data-stu-id="1c7eb-244">hello information returned is similar toohello following text:</span></span>

        deviceplatform  count
        Android 31591
        iPhone OS       22731
        proprietary development 3
        RIM OS  3464
        Unknown 213
        Windows Phone   1791
        (6 rows affected)

<span data-ttu-id="1c7eb-245">如需有關 hello Oozie 命令的詳細資訊，請參閱[Oozie 命令列工具](https://oozie.apache.org/docs/4.1.0/DG_CommandLineTool.html)。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-245">For more information on hello Oozie command, see [Oozie command-line tool](https://oozie.apache.org/docs/4.1.0/DG_CommandLineTool.html).</span></span>

## <a name="oozie-rest-api"></a><span data-ttu-id="1c7eb-246">Oozie REST API</span><span class="sxs-lookup"><span data-stu-id="1c7eb-246">Oozie REST API</span></span>

<span data-ttu-id="1c7eb-247">hello Oozie REST API 可讓您 toobuild 自己 Oozie 所使用的工具。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-247">hello Oozie REST API allows you toobuild your own tools that work with Oozie.</span></span> <span data-ttu-id="1c7eb-248">hello 下面是有關使用 hello Oozie REST API 的 HDInsight 特定資訊：</span><span class="sxs-lookup"><span data-stu-id="1c7eb-248">hello following are HDInsight specific information about using hello Oozie REST API:</span></span>

* <span data-ttu-id="1c7eb-249">**URI**: hello 可從外部 hello 叢集存取 REST API`https://CLUSTERNAME.azurehdinsight.net/oozie`</span><span class="sxs-lookup"><span data-stu-id="1c7eb-249">**URI**: hello REST API can be accessed from outside hello cluster at `https://CLUSTERNAME.azurehdinsight.net/oozie`</span></span>

* <span data-ttu-id="1c7eb-250">**驗證**: toohello API 使用 hello 叢集 HTTP 帳戶 （管理員） 和密碼進行驗證。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-250">**Authentication**: Authenticate toohello API using hello cluster HTTP account (admin) and password.</span></span> <span data-ttu-id="1c7eb-251">例如：</span><span class="sxs-lookup"><span data-stu-id="1c7eb-251">For example:</span></span>

    ```
    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/oozie/versions
    ```

<span data-ttu-id="1c7eb-252">如需有關使用 hello Oozie REST API 的詳細資訊，請參閱[Oozie Web 服務 API](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html)。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-252">For more information on using hello Oozie REST API, see [Oozie Web Services API](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).</span></span>

## <a name="oozie-web-ui"></a><span data-ttu-id="1c7eb-253">Oozie Web UI</span><span class="sxs-lookup"><span data-stu-id="1c7eb-253">Oozie Web UI</span></span>

<span data-ttu-id="1c7eb-254">hello Oozie Web UI hello 叢集上提供網頁 hello Oozie 工作狀態檢視。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-254">hello Oozie Web UI provides a web-based view into hello status of Oozie jobs on hello cluster.</span></span> <span data-ttu-id="1c7eb-255">hello web UI 可讓您 tooview hello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="1c7eb-255">hello web UI allows you tooview hello following information:</span></span>

* <span data-ttu-id="1c7eb-256">工作狀態</span><span class="sxs-lookup"><span data-stu-id="1c7eb-256">Job status</span></span>
* <span data-ttu-id="1c7eb-257">工作定義</span><span class="sxs-lookup"><span data-stu-id="1c7eb-257">Job definition</span></span>
* <span data-ttu-id="1c7eb-258">組態</span><span class="sxs-lookup"><span data-stu-id="1c7eb-258">Configuration</span></span>
* <span data-ttu-id="1c7eb-259">Hello 作業中的 hello 動作的圖形</span><span class="sxs-lookup"><span data-stu-id="1c7eb-259">A graph of hello actions in hello job</span></span>
* <span data-ttu-id="1c7eb-260">記錄檔中的 hello 工作</span><span class="sxs-lookup"><span data-stu-id="1c7eb-260">Logs for hello job</span></span>

<span data-ttu-id="1c7eb-261">您也可以檢視工作內的動作詳細資料。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-261">You can also view details for actions within a job.</span></span>

<span data-ttu-id="1c7eb-262">tooaccess hello Oozie Web UI，請使用下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="1c7eb-262">tooaccess hello Oozie Web UI, use hello following steps:</span></span>

1. <span data-ttu-id="1c7eb-263">建立 SSH 通道 toohello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-263">Create an SSH tunnel toohello HDInsight cluster.</span></span> <span data-ttu-id="1c7eb-264">如需資訊，請參閱 hello[使用 SSH 通道，與 HDInsight](hdinsight-linux-ambari-ssh-tunnel.md)文件。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-264">For information, see hello [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

2. <span data-ttu-id="1c7eb-265">一旦建立通道之後，請 web 瀏覽器中開啟 hello Ambari web UI。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-265">Once a tunnel has been created, open hello Ambari web UI in your web browser.</span></span> <span data-ttu-id="1c7eb-266">hello URI hello Ambari 站台是**https://CLUSTERNAME.azurehdinsight.net**。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-266">hello URI for hello Ambari site is **https://CLUSTERNAME.azurehdinsight.net**.</span></span> <span data-ttu-id="1c7eb-267">取代**CLUSTERNAME** hello 以 Linux 為基礎的 HDInsight 叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-267">Replace **CLUSTERNAME** with hello name of your Linux-based HDInsight cluster.</span></span>

3. <span data-ttu-id="1c7eb-268">從 hello hello 頁面的左側，選取**Oozie**，然後**快速連結**，最後再**Oozie Web UI**。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-268">From hello left side of hello page, select **Oozie**, then **Quick Links**, and finally **Oozie Web UI**.</span></span>

    ![hello 功能表的影像](./media/hdinsight-use-oozie-linux-mac/ooziewebuisteps.png)

4. <span data-ttu-id="1c7eb-270">hello Oozie Web UI 的預設值 toodisplaying 執行工作流程工作。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-270">hello Oozie Web UI defaults toodisplaying running Workflow Jobs.</span></span> <span data-ttu-id="1c7eb-271">所有的工作流程工作，選取 toosee**所有工作**。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-271">toosee all workflow jobs, select **All Jobs**.</span></span>

    ![顯示的所有工作](./media/hdinsight-use-oozie-linux-mac/ooziejobs.png)

5. <span data-ttu-id="1c7eb-273">選取作業 tooview hello 工作的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-273">Select a job tooview more information about hello job.</span></span>

    ![工作資訊](./media/hdinsight-use-oozie-linux-mac/jobinfo.png)

6. <span data-ttu-id="1c7eb-275">從 hello 工作資訊 索引標籤，您可以查看基本作業資訊和 hello hello 作業內的個別動作。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-275">From hello Job Info tab, you can see basic job information and hello individual actions within hello job.</span></span> <span data-ttu-id="1c7eb-276">使用 hello 索引標籤頂端 hello 您可以檢視 hello 工作定義，作業設定存取 hello 作業記錄，或檢視導向非循環圖 (DAG) 的 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-276">Using hello tabs at hello top you can view hello Job Definition, Job Configuration, access hello Job Log or view a Directed Acyclic Graph (DAG) of hello job.</span></span>

   * <span data-ttu-id="1c7eb-277">**作業記錄**： 選取 hello **GetLogs**按鈕 tooget hello 作業的所有記錄檔，或使用 hello**輸入的搜尋篩選器**欄位 toofilter 記錄檔</span><span class="sxs-lookup"><span data-stu-id="1c7eb-277">**Job Log**: Select hello **GetLogs** button tooget all logs for hello job, or use hello **Enter Search Filter** field toofilter logs</span></span>

       ![工作記錄](./media/hdinsight-use-oozie-linux-mac/joblog.png)

   * <span data-ttu-id="1c7eb-279">**JobDAG**: hello DAG 是 hello 資料路徑，引導他們完成 hello 工作流程的圖形化概觀</span><span class="sxs-lookup"><span data-stu-id="1c7eb-279">**JobDAG**: hello DAG is a graphical overview of hello data paths taken through hello workflow</span></span>

       ![工作 DAG](./media/hdinsight-use-oozie-linux-mac/jobdag.png)

7. <span data-ttu-id="1c7eb-281">選取其中一個 hello 動作從 hello**作業資訊** 索引標籤會顯示 hello 動作的資訊。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-281">Selecting one of hello actions from hello **Job Info** tab brings up information for hello action.</span></span> <span data-ttu-id="1c7eb-282">例如，選取 hello **RunHiveScript**動作。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-282">For example, select hello **RunHiveScript** action.</span></span>

    ![動作資訊](./media/hdinsight-use-oozie-linux-mac/action.png)

8. <span data-ttu-id="1c7eb-284">您可以看到 hello 動作，例如連結 toohello 詳細資料**主控台 URL**。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-284">You can see details for hello action, such as a link toohello **Console URL**.</span></span> <span data-ttu-id="1c7eb-285">這個連結可以在使用的 tooview JobTracker hello 工作資訊。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-285">This link can be used tooview JobTracker information for hello job.</span></span>

## <a name="scheduling-jobs"></a><span data-ttu-id="1c7eb-286">排程工作</span><span class="sxs-lookup"><span data-stu-id="1c7eb-286">Scheduling jobs</span></span>

<span data-ttu-id="1c7eb-287">hello 協調器可讓您 toospecify 工作的開始、 結束和出現頻率。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-287">hello coordinator allows you toospecify a start, end, and occurrence frequency for jobs.</span></span> <span data-ttu-id="1c7eb-288">toodefine hello 工作流程中，使用下列步驟的 hello 的排程：</span><span class="sxs-lookup"><span data-stu-id="1c7eb-288">toodefine a schedule for hello workflow, use hello following steps:</span></span>

1. <span data-ttu-id="1c7eb-289">遵循 toocreate 名為的檔案使用 hello **coordinator.xml**:</span><span class="sxs-lookup"><span data-stu-id="1c7eb-289">Use hello following toocreate a file named **coordinator.xml**:</span></span>

    ```
    nano coordinator.xml
    ```

    <span data-ttu-id="1c7eb-290">使用下列 XML 當做 hello hello 檔案內容的 hello:</span><span class="sxs-lookup"><span data-stu-id="1c7eb-290">Use hello following XML as hello contents of hello file:</span></span>

    ```xml
    <coordinator-app name="my_coord_app" frequency="${coordFrequency}" start="${coordStart}" end="${coordEnd}" timezone="${coordTimezone}" xmlns="uri:oozie:coordinator:0.4">
        <action>
        <workflow>
            <app-path>${workflowPath}</app-path>
        </workflow>
        </action>
    </coordinator-app>
    ```

    > [!NOTE]
    > <span data-ttu-id="1c7eb-291">hello`${...}`以 hello 工作定義，在執行階段中的值取代變數。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-291">hello `${...}` variables are replaced by values in hello job definition at run-time.</span></span> <span data-ttu-id="1c7eb-292">hello 變數包括：</span><span class="sxs-lookup"><span data-stu-id="1c7eb-292">hello variables are:</span></span>
    >
    > * <span data-ttu-id="1c7eb-293">`${coordFrequency}`： 執行 hello 工作的執行個體之間的時間。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-293">`${coordFrequency}`: Time between running instances of hello job.</span></span>
    > <span data-ttu-id="1c7eb-294">** `${coordStart}`: hello 工作開始時間。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-294">** `${coordStart}`: hello job start time.</span></span>
    > * <span data-ttu-id="1c7eb-295">`${coordEnd}`: hello 工作結束時間。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-295">`${coordEnd}`: hello job end time.</span></span>
    > * <span data-ttu-id="1c7eb-296">`${coordTimezone}`：協調器工作位在固定時區，不受日光節約時間影響 (通常使用 UTC 表示)。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-296">`${coordTimezone}`: Coordinator jobs are in a fixed time zone with no daylight savings time (typically represented by using UTC).</span></span> <span data-ttu-id="1c7eb-297">這個時區稱為 hello"Oozie 處理 timezone。 」</span><span class="sxs-lookup"><span data-stu-id="1c7eb-297">This time zone is referred as hello "Oozie processing timezone."</span></span>
    > * <span data-ttu-id="1c7eb-298">`${wfPath}`: hello 路徑 toohello workflow.xml。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-298">`${wfPath}`: hello path toohello workflow.xml.</span></span>

2. <span data-ttu-id="1c7eb-299">toosave hello 檔案，請使用 Ctrl-X **Y**，和**Enter**。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-299">toosave hello file, use Ctrl-X, **Y**, and **Enter**.</span></span>

3. <span data-ttu-id="1c7eb-300">使用下列命令 toocopy hello 檔案 toohello 工作目錄為此工作的 hello:</span><span class="sxs-lookup"><span data-stu-id="1c7eb-300">Use hello following command toocopy hello file toohello working directory for this job:</span></span>

    ```
    hadoop fs -put coordinator.xml /tutorials/useoozie/coordinator.xml
    ```

4. <span data-ttu-id="1c7eb-301">使用 hello 遵循 toomodify hello **job.xml**檔案：</span><span class="sxs-lookup"><span data-stu-id="1c7eb-301">Use hello following toomodify hello **job.xml** file:</span></span>

    ```
    nano job.xml
    ```

    <span data-ttu-id="1c7eb-302">進行下列變更 hello:</span><span class="sxs-lookup"><span data-stu-id="1c7eb-302">Make hello following changes:</span></span>

   * <span data-ttu-id="1c7eb-303">tooinstruct oozie toorun hello 協調器檔案而不是 hello 工作流程中，變更`<name>oozie.wf.application.path</name>`太`<name>oozie.coord.application.path</name>`。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-303">tooinstruct oozie toorun hello coordinator file instead of hello workflow, change `<name>oozie.wf.application.path</name>` too`<name>oozie.coord.application.path</name>`.</span></span>

   * <span data-ttu-id="1c7eb-304">tooset hello `workflowPath` hello 協調器 中，所使用的變數加入下列 XML 的 hello:</span><span class="sxs-lookup"><span data-stu-id="1c7eb-304">tooset hello `workflowPath` variable used by hello coordinator, add hello following XML:</span></span>

        ```xml
        <property>
            <name>workflowPath</name>
            <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie</value>
        </property>
        ```

       <span data-ttu-id="1c7eb-305">取代 hello `wasb://mycontainer@mystorageaccount.blob.core.windows` hello job.xml 檔案中的其他項目中所使用的 hello 值的文字。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-305">Replace hello `wasb://mycontainer@mystorageaccount.blob.core.windows` text with hello value used in other entries in hello job.xml file.</span></span>

   * <span data-ttu-id="1c7eb-306">toodefine hello 開始、 結束和頻率 hello 協調器 中，加入下列 XML 的 hello:</span><span class="sxs-lookup"><span data-stu-id="1c7eb-306">toodefine hello start, end, and frequency for hello coordinator, add hello following XML:</span></span>

        ```xml
        <property>
            <name>coordStart</name>
            <value>2017-05-10T12:00Z</value>
        </property>

        <property>
            <name>coordEnd</name>
            <value>2017-05-12T12:00Z</value>
        </property>

        <property>
            <name>coordFrequency</name>
            <value>1440</value>
        </property>

        <property>
            <name>coordTimezone</name>
            <value>UTC</value>
        </property>
        ```

       <span data-ttu-id="1c7eb-307">這些值來設定 hello 開始時間 too12: 00 PM 2017 年 10 hello 的結束時間 tooMay 12，2017年。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-307">These values set hello start time too12:00PM on May 10, 2017, hello end time tooMay 12, 2017.</span></span> <span data-ttu-id="1c7eb-308">hello 間隔為每日執行此作業。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-308">hello interval for running this job daily.</span></span> <span data-ttu-id="1c7eb-309">hello 頻率是以分鐘為單位，因此 24 小時 x 60 分鐘 = 1440年分鐘。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-309">hello frequency is in minutes, so 24 hours x 60 minutes = 1440 minutes.</span></span> <span data-ttu-id="1c7eb-310">最後，hello 時區會設定 tooUTC。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-310">Finally, hello timezone is set tooUTC.</span></span>

5. <span data-ttu-id="1c7eb-311">然後使用 Ctrl-X **Y**和**Enter** toosave hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-311">Use Ctrl-X, then **Y** and **Enter** toosave hello file.</span></span>

6. <span data-ttu-id="1c7eb-312">下列命令使用 hello toorun hello 工作：</span><span class="sxs-lookup"><span data-stu-id="1c7eb-312">toorun hello job, use hello following command:</span></span>

    ```
    oozie job -config job.xml -run
    ```

    <span data-ttu-id="1c7eb-313">此命令送出，並開始 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-313">This command submits and starts hello job.</span></span>

7. <span data-ttu-id="1c7eb-314">如果您瀏覽 hello Oozie Web UI，並選取 hello**協調者作業**索引標籤上，您會看到下列映像的資訊類似 toohello:</span><span class="sxs-lookup"><span data-stu-id="1c7eb-314">If you visit hello Oozie Web UI and select hello **Coordinator Jobs** tab, you see information similar toohello following image:</span></span>

    ![協調器工作索引標籤](./media/hdinsight-use-oozie-linux-mac/coordinatorjob.png)

    <span data-ttu-id="1c7eb-316">hello**下一步具體化**項目包含 hello hello 工作執行的下一次。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-316">hello **Next Materialization** entry contains hello next time that hello job runs.</span></span>

8. <span data-ttu-id="1c7eb-317">類似 toohello 舊版工作流程工作，在 hello web UI 中選取 hello 工作項目會顯示 hello 作業有關的資訊：</span><span class="sxs-lookup"><span data-stu-id="1c7eb-317">Similar toohello earlier workflow job, selecting hello job entry in hello web UI displays information on hello job:</span></span>

    ![協調器工作資訊](./media/hdinsight-use-oozie-linux-mac/coordinatorjobinfo.png)

    > [!NOTE]
    > <span data-ttu-id="1c7eb-319">此映像只會顯示成功執行 hello 作業不是個別 hello 排定的工作流程內的動作。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-319">This image only shows successful runs of hello job, not individual actions within hello scheduled workflow.</span></span> <span data-ttu-id="1c7eb-320">選取其中一個 hello toosee**動作**項目。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-320">toosee that, select one of hello **Action** entries.</span></span>

    ![動作資訊](./media/hdinsight-use-oozie-linux-mac/coordinatoractionjob.png)

## <a name="troubleshooting"></a><span data-ttu-id="1c7eb-322">疑難排解</span><span class="sxs-lookup"><span data-stu-id="1c7eb-322">Troubleshooting</span></span>

<span data-ttu-id="1c7eb-323">hello Oozie UI 可讓您 tooview Oozie 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-323">hello Oozie UI allows you tooview Oozie logs.</span></span> <span data-ttu-id="1c7eb-324">它也包含連結 tooJobTracker 記錄檔中的 hello 工作流程啟動 MapReduce 工作。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-324">It also contains links tooJobTracker logs for MapReduce tasks started by hello workflow.</span></span> <span data-ttu-id="1c7eb-325">如需疑難排解的 hello 模式應該是：</span><span class="sxs-lookup"><span data-stu-id="1c7eb-325">hello pattern for troubleshooting should be:</span></span>

1. <span data-ttu-id="1c7eb-326">檢視 hello Oozie Web UI 中的工作。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-326">View hello job in Oozie Web UI.</span></span>

2. <span data-ttu-id="1c7eb-327">如果沒有錯誤或特定的動作失敗，選取如果 hello hello 動作 toosee**錯誤訊息**欄位提供有關 hello 失敗的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-327">If there is an error or failure for a specific action, select hello action toosee if hello **Error Message** field provides more information on hello failure.</span></span>

3. <span data-ttu-id="1c7eb-328">如果有的話，使用 hello URL hello 動作 tooview 從更多詳細資料 （例如 JobTracker 記錄） hello 動作。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-328">If available, use hello URL from hello action tooview more details (such as JobTracker logs) for hello action.</span></span>

<span data-ttu-id="1c7eb-329">hello 以下是您可能會遇到的特定錯誤及如何 tooresolve 它們。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-329">hello following are specific errors you may encounter, and how tooresolve them.</span></span>

### <a name="ja009-cannot-initialize-cluster"></a><span data-ttu-id="1c7eb-330">JA009：無法初始化叢集</span><span class="sxs-lookup"><span data-stu-id="1c7eb-330">JA009: Cannot initialize cluster</span></span>

<span data-ttu-id="1c7eb-331">**徵兆**: hello 作業狀態變更太**SUSPENDED**。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-331">**Symptoms**: hello job status changes too**SUSPENDED**.</span></span> <span data-ttu-id="1c7eb-332">Hello 工作的詳細資料顯示 hello RunHiveScript 狀態為**START_MANUAL**。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-332">Details for hello job show hello RunHiveScript status as **START_MANUAL**.</span></span> <span data-ttu-id="1c7eb-333">選取 hello 動作會顯示下列錯誤訊息的 hello:</span><span class="sxs-lookup"><span data-stu-id="1c7eb-333">Selecting hello action displays hello following error message:</span></span>

    JA009: Cannot initialize Cluster. Please check your configuration for map

<span data-ttu-id="1c7eb-334">**可能的原因**: hello WASB 位址用於 hello **job.xml**檔案不包含 hello 儲存體容器或儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-334">**Cause**: hello WASB addresses used in hello **job.xml** file do not contain hello storage container or storage account name.</span></span> <span data-ttu-id="1c7eb-335">hello WASB 位址格式必須為`wasb://containername@storageaccountname.blob.core.windows.net`。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-335">hello WASB address format must be `wasb://containername@storageaccountname.blob.core.windows.net`.</span></span>

<span data-ttu-id="1c7eb-336">**解析**： 變更 hello 作業所使用的 hello WASB 位址。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-336">**Resolution**: Change hello WASB addresses used by hello job.</span></span>

### <a name="ja002-oozie-is-not-allowed-tooimpersonate-ltuser"></a><span data-ttu-id="1c7eb-337">JA002: Oozie 不允許 tooimpersonate&lt;使用者 ></span><span class="sxs-lookup"><span data-stu-id="1c7eb-337">JA002: Oozie is not allowed tooimpersonate &lt;USER></span></span>

<span data-ttu-id="1c7eb-338">**徵兆**: hello 作業狀態變更太**SUSPENDED**。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-338">**Symptoms**: hello job status changes too**SUSPENDED**.</span></span> <span data-ttu-id="1c7eb-339">Hello 工作的詳細資料顯示 hello RunHiveScript 狀態為**START_MANUAL**。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-339">Details for hello job show hello RunHiveScript status as **START_MANUAL**.</span></span> <span data-ttu-id="1c7eb-340">選取 hello 動作會顯示下列錯誤訊息的 hello:</span><span class="sxs-lookup"><span data-stu-id="1c7eb-340">Selecting hello action shows hello following error message:</span></span>

    JA002: User: oozie is not allowed tooimpersonate <USER>

<span data-ttu-id="1c7eb-341">**可能的原因**： 目前的權限設定不允許 Oozie tooimpersonate hello 指定使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-341">**Cause**: Current permission settings do not allow Oozie tooimpersonate hello specified user account.</span></span>

<span data-ttu-id="1c7eb-342">**解析**: Oozie hello 中允許 tooimpersonate 使用者**使用者**群組。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-342">**Resolution**: Oozie is allowed tooimpersonate users in hello **users** group.</span></span> <span data-ttu-id="1c7eb-343">使用 hello `groups USERNAME` hello 使用者帳戶的 toosee hello 群組是的成員。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-343">Use hello `groups USERNAME` toosee hello groups that hello user account is a member of.</span></span> <span data-ttu-id="1c7eb-344">如果 hello 使用者不屬於 hello**使用者**群組中，使用下列命令 tooadd hello 使用者 toohello 群組 hello:</span><span class="sxs-lookup"><span data-stu-id="1c7eb-344">If hello user is not a member of hello **users** group, use hello following command tooadd hello user toohello group:</span></span>

    sudo adduser USERNAME users

> [!NOTE]
> <span data-ttu-id="1c7eb-345">可能需要幾分鐘的時間才能 HDInsight 辨識該 hello 使用者已新增 toohello 群組。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-345">It may take several minutes before HDInsight recognizes that hello user has been added toohello group.</span></span>

### <a name="launcher-error-sqoop"></a><span data-ttu-id="1c7eb-346">啟動器錯誤 (Sqoop)</span><span class="sxs-lookup"><span data-stu-id="1c7eb-346">Launcher ERROR (Sqoop)</span></span>

<span data-ttu-id="1c7eb-347">**徵兆**: hello 作業狀態變更太**KILLED**。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-347">**Symptoms**: hello job status changes too**KILLED**.</span></span> <span data-ttu-id="1c7eb-348">Hello 工作的詳細資料顯示 hello RunSqoopExport 狀態為**錯誤**。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-348">Details for hello job show hello RunSqoopExport status as **ERROR**.</span></span> <span data-ttu-id="1c7eb-349">選取 hello 動作會顯示下列錯誤訊息的 hello:</span><span class="sxs-lookup"><span data-stu-id="1c7eb-349">Selecting hello action shows hello following error message:</span></span>

    Launcher ERROR, reason: Main class [org.apache.oozie.action.hadoop.SqoopMain], exit code [1]

<span data-ttu-id="1c7eb-350">**可能的原因**: Sqoop 是無法 tooload hello 資料庫驅動程式需要的 tooaccess hello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-350">**Cause**: Sqoop is unable tooload hello database driver required tooaccess hello database.</span></span>

<span data-ttu-id="1c7eb-351">**解析**： 當使用 Sqoop 從 Oozie 作業，您必須包含以 hello hello 資料庫驅動程式 hello 作業所使用其他資源 （例如 hello workflow.xml)。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-351">**Resolution**: When using Sqoop from an Oozie job, you must include hello database driver with hello other resources (such as hello workflow.xml) used by hello job.</span></span> <span data-ttu-id="1c7eb-352">也會參考包含 hello 資料庫驅動程式從 hello hello 封存`<sqoop>...</sqoop>`hello workflow.xml 一節。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-352">Also Reference hello archive containing hello database driver from hello `<sqoop>...</sqoop>` section of hello workflow.xml.</span></span>

<span data-ttu-id="1c7eb-353">比方說，這份文件中的 hello 作業，您會使用 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="1c7eb-353">For example, for hello job in this document, you would use hello following steps:</span></span>

1. <span data-ttu-id="1c7eb-354">複製 hello sqljdbc4.1.jar 檔案 toohello /tutorials/useoozie 目錄：</span><span class="sxs-lookup"><span data-stu-id="1c7eb-354">Copy hello sqljdbc4.1.jar file toohello /tutorials/useoozie directory:</span></span>

    ```
    hdfs dfs -put /usr/share/java/sqljdbc_4.1/enu/sqljdbc41.jar /tutorials/useoozie/sqljdbc41.jar
    ```

2. <span data-ttu-id="1c7eb-355">修改下列新的一行上述 XML hello workflow.xml tooadd hello `</sqoop>`:</span><span class="sxs-lookup"><span data-stu-id="1c7eb-355">Modify hello workflow.xml tooadd hello following XML on a new line above `</sqoop>`:</span></span>

    ```xml
    <archive>sqljdbc41.jar</archive>
    ```

## <a name="next-steps"></a><span data-ttu-id="1c7eb-356">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1c7eb-356">Next steps</span></span>

<span data-ttu-id="1c7eb-357">在本教學課程中，您學到如何 toodefine Oozie 工作流程以及 toorun Oozie 作業。</span><span class="sxs-lookup"><span data-stu-id="1c7eb-357">In this tutorial, you learned how toodefine an Oozie workflow and how toorun an Oozie job.</span></span> <span data-ttu-id="1c7eb-358">toolearn 進一步了解使用 HDInsight，請參閱下列文章的 hello:</span><span class="sxs-lookup"><span data-stu-id="1c7eb-358">toolearn more about working with HDInsight, see hello following articles:</span></span>

* <span data-ttu-id="1c7eb-359">[搭配 HDInsight 使用以時間為基礎的 Hadoop Oozie 協調器][hdinsight-oozie-coordinator-time]</span><span class="sxs-lookup"><span data-stu-id="1c7eb-359">[Use time-based Oozie Coordinator with HDInsight][hdinsight-oozie-coordinator-time]</span></span>
* <span data-ttu-id="1c7eb-360">[在 HDInsight 中上傳 Hadoop 作業的資料][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="1c7eb-360">[Upload data for Hadoop jobs in HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="1c7eb-361">[搭配使用 Sqoop 與 HDInsight 中的 Hadoop][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="1c7eb-361">[Use Sqoop with Hadoop in HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="1c7eb-362">[搭配使用 Hive 與 HDInsight 上的 Hadoop][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="1c7eb-362">[Use Hive with Hadoop on HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="1c7eb-363">[搭配使用 Pig 與 HDInsight 上的 Hadoop][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="1c7eb-363">[Use Pig with Hadoop on HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="1c7eb-364">[開發 HDInsight 的 Java MapReduce 程式][hdinsight-develop-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="1c7eb-364">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-mapreduce]</span></span>

[hdinsight-cmdlets-download]: http://go.microsoft.com/fwlink/?LinkID=325563
[azure-data-factory-pig-hive]: ../data-factory/data-factory-data-transformation-activities.md
[hdinsight-oozie-coordinator-time]: hdinsight-use-oozie-coordinator-time.md
[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-storage]: hdinsight-use-blob-storage.md
[hdinsight-get-started]: hdinsight-get-started.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop-mac-linux.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-storage]: hdinsight-use-blob-storage.md
[hdinsight-get-started-emulator]: hdinsight-get-started-emulator.md
[hdinsight-develop-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md

[sqldatabase-create-configue]: sql-database-create-configure.md
[sqldatabase-get-started]: sql-database-get-started.md

[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md

[apache-hadoop]: http://hadoop.apache.org/
[apache-oozie-400]: http://oozie.apache.org/docs/4.0.0/
[apache-oozie-332]: http://oozie.apache.org/docs/3.3.2/

[powershell-download]: http://azure.microsoft.com/downloads/
[powershell-about-profiles]: http://go.microsoft.com/fwlink/?LinkID=113729
[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-script]: https://technet.microsoft.com/en-us/library/ee176961.aspx

[cindygross-hive-tables]: http://blogs.msdn.com/b/cindygross/archive/2013/02/06/hdinsight-hive-internal-and-external-tables-intro.aspx

[img-workflow-diagram]: ./media/hdinsight-use-oozie/HDI.UseOozie.Workflow.Diagram.png
[img-preparation-output]: ./media/hdinsight-use-oozie/HDI.UseOozie.Preparation.Output1.png
[img-runworkflow-output]: ./media/hdinsight-use-oozie/HDI.UseOozie.RunWF.Output.png

[technetwiki-hive-error]: http://social.technet.microsoft.com/wiki/contents/articles/23047.hdinsight-hive-error-unable-to-rename.aspx
