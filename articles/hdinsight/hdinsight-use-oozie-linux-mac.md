---
title: "在 Linux 型 HDInsight 上使用 Hadoop Oozie 工作流程 | Microsoft Docs"
description: "在 Linux 型 HDInsight 上使用 Hadoop Oozie。 了解如何定義 Oozie 工作流程，以及提交 Oozie 工作。"
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
ms.openlocfilehash: e3206078e451aefe02689bfb61ce22a20dd0fa70
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="use-oozie-with-hadoop-to-define-and-run-a-workflow-on-linux-based-hdinsight"></a><span data-ttu-id="434e4-104">在 Linux 型 HDInsight 上搭配 Hadoop 使用 Oozie 來定義並執行工作流程</span><span class="sxs-lookup"><span data-stu-id="434e4-104">Use Oozie with Hadoop to define and run a workflow on Linux-based HDInsight</span></span>

[!INCLUDE [oozie-selector](../../includes/hdinsight-oozie-selector.md)]

<span data-ttu-id="434e4-105">了解如何在 HDInsight 上搭配 Hadoop 使用 Apache Oozie。</span><span class="sxs-lookup"><span data-stu-id="434e4-105">Learn how to use Apache Oozie with Hadoop on HDInsight.</span></span> <span data-ttu-id="434e4-106">Apache Oozie 是可管理 Hadoop 工作的工作流程/協調系統。</span><span class="sxs-lookup"><span data-stu-id="434e4-106">Apache Oozie is a workflow/coordination system that manages Hadoop jobs.</span></span> <span data-ttu-id="434e4-107">Oozie 已與 Hadoop 堆疊整合，並支援下列作業：</span><span class="sxs-lookup"><span data-stu-id="434e4-107">Oozie is integrated with the Hadoop stack, and it supports the following jobs:</span></span>

* <span data-ttu-id="434e4-108">Apache MapReduce</span><span class="sxs-lookup"><span data-stu-id="434e4-108">Apache MapReduce</span></span>
* <span data-ttu-id="434e4-109">Apache Pig</span><span class="sxs-lookup"><span data-stu-id="434e4-109">Apache Pig</span></span>
* <span data-ttu-id="434e4-110">Apache Hive</span><span class="sxs-lookup"><span data-stu-id="434e4-110">Apache Hive</span></span>
* <span data-ttu-id="434e4-111">Apache Sqoop</span><span class="sxs-lookup"><span data-stu-id="434e4-111">Apache Sqoop</span></span>

<span data-ttu-id="434e4-112">Oozie 也可用來排程系統的特定工作，例如 Java 程式或 Shell 指令碼</span><span class="sxs-lookup"><span data-stu-id="434e4-112">Oozie can also be used to schedule jobs that are specific to a system, like Java programs or shell scripts</span></span>

> [!NOTE]
> <span data-ttu-id="434e4-113">還有另一個選項可以定義與 HDInsight 搭配的工作流程，那就是 Azure Data Factory。</span><span class="sxs-lookup"><span data-stu-id="434e4-113">Another option for defining workflows with HDInsight is Azure Data Factory.</span></span> <span data-ttu-id="434e4-114">若要深入了解 Azure Data Factory，請參閱[搭配 Data Factory 使用 Pig 和 Hive][azure-data-factory-pig-hive]。</span><span class="sxs-lookup"><span data-stu-id="434e4-114">To learn more about Azure Data Factory, see [Use Pig and Hive with Data Factory][azure-data-factory-pig-hive].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="434e4-115">Oozie 未在已加入網域的 HDInsight 上啟用。</span><span class="sxs-lookup"><span data-stu-id="434e4-115">Oozie is not enabled on domain-joined HDInsight.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="434e4-116">必要條件</span><span class="sxs-lookup"><span data-stu-id="434e4-116">Prerequisites</span></span>

* <span data-ttu-id="434e4-117">**HDInsight 叢集**：請參閱 [開始使用 Linux 上的 HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="434e4-117">**An HDInsight cluster**: See [Get Started with HDInsight on Linux](hdinsight-hadoop-linux-tutorial-get-started.md)</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="434e4-118">此文件中的步驟需要使用 Linux 的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="434e4-118">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="434e4-119">Linux 是唯一使用於 HDInsight 3.4 版或更新版本的作業系統。</span><span class="sxs-lookup"><span data-stu-id="434e4-119">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="434e4-120">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="434e4-120">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="example-workflow"></a><span data-ttu-id="434e4-121">範例工作流程</span><span class="sxs-lookup"><span data-stu-id="434e4-121">Example workflow</span></span>

<span data-ttu-id="434e4-122">此文件中使用的工作流程包含兩個動作。</span><span class="sxs-lookup"><span data-stu-id="434e4-122">The workflow used in this document contains two actions.</span></span> <span data-ttu-id="434e4-123">動作就是工作的定義，例如執行 Hive、Sqoop、MapReduce 或其他處理序：</span><span class="sxs-lookup"><span data-stu-id="434e4-123">Actions are definitions for tasks, such as running Hive, Sqoop, MapReduce, or other process:</span></span>

![Workflow diagram][img-workflow-diagram]

1. <span data-ttu-id="434e4-125">Hive 動作會執行 HiveQL 指令碼，以從 HDInsight 隨附的 **hivesampletable** 擷取記錄。</span><span class="sxs-lookup"><span data-stu-id="434e4-125">A Hive action runs a HiveQL script to extract records from the **hivesampletable** included with HDInsight.</span></span> <span data-ttu-id="434e4-126">每個資料列均代表來自特定行動裝置的瀏覽。</span><span class="sxs-lookup"><span data-stu-id="434e4-126">Each row of data describes a visit from a specific mobile device.</span></span> <span data-ttu-id="434e4-127">顯示的記錄格式類似下列文字：</span><span class="sxs-lookup"><span data-stu-id="434e4-127">The record format appears similar to the following text:</span></span>

        8       18:54:20        en-US   Android Samsung SCH-i500        California     United States    13.9204007      0       0
        23      19:19:44        en-US   Android HTC     Incredible      Pennsylvania   United States    NULL    0       0
        23      19:19:46        en-US   Android HTC     Incredible      Pennsylvania   United States    1.4757422       0       1

    <span data-ttu-id="434e4-128">本文件中使用的 Hive 指令碼會計算每個平台 (例如 Android 或 iPhone) 的總瀏覽次數，並將計數儲存到新的 Hive 資料表。</span><span class="sxs-lookup"><span data-stu-id="434e4-128">The Hive script used in this document counts the total visits for each platform (such as Android or iPhone) and stores the counts to a new Hive table.</span></span>

    <span data-ttu-id="434e4-129">如需 Hive 的詳細資訊，請參閱[在 HDInsight 上使用 Hive][hdinsight-use-hive]。</span><span class="sxs-lookup"><span data-stu-id="434e4-129">For more information about Hive, see [Use Hive with HDInsight][hdinsight-use-hive].</span></span>

2. <span data-ttu-id="434e4-130">Sqoop 動作會將新的 Hive 資料表內容匯出至 Azure SQL Database 中的資料表。</span><span class="sxs-lookup"><span data-stu-id="434e4-130">A Sqoop action exports the contents of the new Hive table to a table in an Azure SQL database.</span></span> <span data-ttu-id="434e4-131">如需 Sqoop 的詳細資訊，請參閱[搭配 HDInsight 使用 Hadoop Sqoop][hdinsight-use-sqoop]。</span><span class="sxs-lookup"><span data-stu-id="434e4-131">For more information about Sqoop, see [Use Hadoop Sqoop with HDInsight][hdinsight-use-sqoop].</span></span>

> [!NOTE]
> <span data-ttu-id="434e4-132">如需 HDInsight 叢集支援的 Oozie 版本，請參閱 [HDInsight 提供之 Hadoop 叢集版本中的新增功能][hdinsight-versions]。</span><span class="sxs-lookup"><span data-stu-id="434e4-132">For supported Oozie versions on HDInsight clusters, see [What's new in the Hadoop cluster versions provided by HDInsight][hdinsight-versions].</span></span>

## <a name="create-the-working-directory"></a><span data-ttu-id="434e4-133">建立工作目錄</span><span class="sxs-lookup"><span data-stu-id="434e4-133">Create the working directory</span></span>

<span data-ttu-id="434e4-134">Oozie 的工作所需資源必須儲存在同一個目錄中。</span><span class="sxs-lookup"><span data-stu-id="434e4-134">Oozie expects resources required for a job to be stored in the same directory.</span></span> <span data-ttu-id="434e4-135">這個範例會使用 **wasb:///tutorials/useoozie**。</span><span class="sxs-lookup"><span data-stu-id="434e4-135">This example uses **wasb:///tutorials/useoozie**.</span></span> <span data-ttu-id="434e4-136">請使用以下命令建立此目錄，以及建立資料目錄，以保存此工作流程所建立的新 Hive 資料表：</span><span class="sxs-lookup"><span data-stu-id="434e4-136">Use the following command to create this directory, and the data directory that holds the new Hive table created by this workflow:</span></span>

```
hdfs dfs -mkdir -p /tutorials/useoozie/data
```

> [!NOTE]
> <span data-ttu-id="434e4-137">`-p` 參數會使系統建立路徑中的所有目錄。</span><span class="sxs-lookup"><span data-stu-id="434e4-137">The `-p` parameter causes all directories in the path to be created.</span></span> <span data-ttu-id="434e4-138">**data** 目錄是用來保存 **useooziewf.hql** 指令碼所使用的資料。</span><span class="sxs-lookup"><span data-stu-id="434e4-138">The **data** directory is used to hold data used by the **useooziewf.hql** script.</span></span>

<span data-ttu-id="434e4-139">此外，也請執行以下命令，確保 Oozie 在執行 Hive 和 Sqoop 工作時可以模擬您的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="434e4-139">Also run the following command, which ensures that Oozie can impersonate your user account when running Hive and Sqoop jobs.</span></span> <span data-ttu-id="434e4-140">將 **USERNAME** 取代為您的登入名稱：</span><span class="sxs-lookup"><span data-stu-id="434e4-140">Replace **USERNAME** with your login name:</span></span>

```
sudo adduser USERNAME users
```

> [!NOTE]
> <span data-ttu-id="434e4-141">您可以忽略使用者已是 `users` 群組之成員的錯誤。</span><span class="sxs-lookup"><span data-stu-id="434e4-141">You can ignore errors that the user is already a member of the `users` group.</span></span>

## <a name="add-a-database-driver"></a><span data-ttu-id="434e4-142">新增資料庫驅動程式</span><span class="sxs-lookup"><span data-stu-id="434e4-142">Add a database driver</span></span>

<span data-ttu-id="434e4-143">由於此工作流程會使用 Sqoop 將資料匯出至 SQL Database，因此您必須提供一份要用來與 SQL Database 溝通的 JDBC 驅動程式複本。</span><span class="sxs-lookup"><span data-stu-id="434e4-143">Since this workflow uses Sqoop to export data to SQL Database, you must provide a copy of the JDBC driver used to talk to SQL Database.</span></span> <span data-ttu-id="434e4-144">請使用以下命令將該複本複製到工作目錄：</span><span class="sxs-lookup"><span data-stu-id="434e4-144">Use the following command to copy it to the working directory:</span></span>

```
hdfs dfs -put /usr/share/java/sqljdbc_4.1/enu/sqljdbc*.jar /tutorials/useoozie/
```

<span data-ttu-id="434e4-145">如果工作流程使用了其他資源，例如含有 MapReduce 應用程式的 jar，則您也必須新增這些資源。</span><span class="sxs-lookup"><span data-stu-id="434e4-145">If your workflow used other resources, such as a jar containing a MapReduce application, you would need to add these resources as well.</span></span>

## <a name="define-the-hive-query"></a><span data-ttu-id="434e4-146">定義 Hive 查詢</span><span class="sxs-lookup"><span data-stu-id="434e4-146">Define the Hive query</span></span>

<span data-ttu-id="434e4-147">使用下列步驟建立 HiveQL 指令碼，以定義此文件之後的 Oozie 工作流程中要使用的查詢。</span><span class="sxs-lookup"><span data-stu-id="434e4-147">Use the following steps to create a HiveQL script that defines a query, which is used in an Oozie workflow later in this document.</span></span>

1. <span data-ttu-id="434e4-148">使用 SSH 連線到叢集。</span><span class="sxs-lookup"><span data-stu-id="434e4-148">Connect to the cluster using SSH.</span></span> <span data-ttu-id="434e4-149">下列命令是使用 `ssh` 命令的範例。</span><span class="sxs-lookup"><span data-stu-id="434e4-149">The following command is an example of using the `ssh` command.</span></span> <span data-ttu-id="434e4-150">將 __USERNAME__ 取代為叢集的 SSH 使用者。</span><span class="sxs-lookup"><span data-stu-id="434e4-150">Replace __USERNAME__ with the SSH user for the cluster.</span></span> <span data-ttu-id="434e4-151">將 __CLUSTERNAME__ 取代為 HDInsight 叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="434e4-151">Replace __CLUSTERNAME__ with the name of the HDInsight cluster.</span></span>

    ```
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="434e4-152">如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="434e4-152">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="434e4-153">從 SSH 連線，使用下列命令來建立檔案：</span><span class="sxs-lookup"><span data-stu-id="434e4-153">From the SSH connection, use the following command to create a file:</span></span>

    ```
    nano useooziewf.hql
    ```

3. <span data-ttu-id="434e4-154">開啟 nano 編輯器後，請使用下列查詢做為檔案的內容：</span><span class="sxs-lookup"><span data-stu-id="434e4-154">Once the nano editor opens, use the following query as the contents of the file:</span></span>

    ```hiveql
    DROP TABLE ${hiveTableName};
    CREATE EXTERNAL TABLE ${hiveTableName}(deviceplatform string, count string) ROW FORMAT DELIMITED
    FIELDS TERMINATED BY '\t' STORED AS TEXTFILE LOCATION '${hiveDataFolder}';
    INSERT OVERWRITE TABLE ${hiveTableName} SELECT deviceplatform, COUNT(*) as count FROM hivesampletable GROUP BY deviceplatform;
    ```

    <span data-ttu-id="434e4-155">指令碼中使用了兩個變數：</span><span class="sxs-lookup"><span data-stu-id="434e4-155">There are two variables used in the script:</span></span>

    * <span data-ttu-id="434e4-156">**${hiveTableName}**：包含要建立的資料表名稱</span><span class="sxs-lookup"><span data-stu-id="434e4-156">**${hiveTableName}**: contains the name of the table to be created</span></span>

    * <span data-ttu-id="434e4-157">**${hiveDataFolder}**：包含儲存資料表之資料檔案的位置</span><span class="sxs-lookup"><span data-stu-id="434e4-157">**${hiveDataFolder}**: contains the location to store the data files for the table</span></span>

    <span data-ttu-id="434e4-158">工作流程定義檔 (在此教學課程中為 workflow.xml) 會在執行階段將這些值傳遞至此 HiveQL 指令碼</span><span class="sxs-lookup"><span data-stu-id="434e4-158">The workflow definition file (workflow.xml in this tutorial) passes these values to this HiveQL script at run time</span></span>

4. <span data-ttu-id="434e4-159">若要結束編輯器，請按 Ctrl-X。</span><span class="sxs-lookup"><span data-stu-id="434e4-159">To exit the editor, press Ctrl-X.</span></span> <span data-ttu-id="434e4-160">出現提示時，請選取 **Y** 儲存檔案，然後按 **Enter** 鍵以使用 **useooziewf.hql** 檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="434e4-160">When prompted, select **Y** to save the file, then use **Enter** to use the **useooziewf.hql** file name.</span></span>

5. <span data-ttu-id="434e4-161">使用下列命令將 **useooziewf.hql** 複製到 **wasb:///tutorials/useoozie/useooziewf.hql**：</span><span class="sxs-lookup"><span data-stu-id="434e4-161">Use the following commands to copy **useooziewf.hql** to **wasb:///tutorials/useoozie/useooziewf.hql**:</span></span>

    ```
    hdfs dfs -put useooziewf.hql /tutorials/useoozie/useooziewf.hql
    ```

    <span data-ttu-id="434e4-162">這些命令會在叢集的 HDFS 相容儲存體上儲存 **useooziewf.hql** 檔案。</span><span class="sxs-lookup"><span data-stu-id="434e4-162">These commands store the **useooziewf.hql** file on the HDFS-compatible storage for the cluster.</span></span>

## <a name="define-the-workflow"></a><span data-ttu-id="434e4-163">定義工作流程</span><span class="sxs-lookup"><span data-stu-id="434e4-163">Define the workflow</span></span>

<span data-ttu-id="434e4-164">Oozie 工作流程定義是以 hPDL 撰寫 (一種 XML 程序定義語言)。</span><span class="sxs-lookup"><span data-stu-id="434e4-164">Oozie workflows definitions are written in hPDL (an XML Process Definition Language).</span></span> <span data-ttu-id="434e4-165">使用下列步驟定義工作流程：</span><span class="sxs-lookup"><span data-stu-id="434e4-165">Use the following steps to define the workflow:</span></span>

1. <span data-ttu-id="434e4-166">使用以下陳述式建立和編輯新的檔案：</span><span class="sxs-lookup"><span data-stu-id="434e4-166">Use the following statement to create and edit a new file:</span></span>

    ```
    nano workflow.xml
    ```

2. <span data-ttu-id="434e4-167">開啟 nano 編輯器後，請輸入下列 XML 做為檔案內容：</span><span class="sxs-lookup"><span data-stu-id="434e4-167">Once the nano editor opens, enter the following XML as the file contents:</span></span>

    ```xml
    <workflow-app name="useooziewf" xmlns="uri:oozie:workflow:0.2">
        <start to = "RunHiveScript"/>
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

    <span data-ttu-id="434e4-168">此工作流程中定義了兩個動作：</span><span class="sxs-lookup"><span data-stu-id="434e4-168">There are two actions defined in the workflow:</span></span>

   * <span data-ttu-id="434e4-169">**RunHiveScript**：這是起始動作，且會執行 **useooziewf.hql** Hive 指令碼</span><span class="sxs-lookup"><span data-stu-id="434e4-169">**RunHiveScript**: This action is the start action, and runs the **useooziewf.hql** Hive script</span></span>

   * <span data-ttu-id="434e4-170">**RunSqoopExport**：此動作會使用 Sqoop 將 Hive 指令碼建立的資料匯出到 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="434e4-170">**RunSqoopExport**: This action exports the data created from the Hive script to SQL Database using Sqoop.</span></span> <span data-ttu-id="434e4-171">只有 **RunHiveScript** 動作成功時才會執行此動作。</span><span class="sxs-lookup"><span data-stu-id="434e4-171">This action only runs if the **RunHiveScript** action is successful.</span></span>

     <span data-ttu-id="434e4-172">工作流程有數個項目，例如 `${jobTracker}`。</span><span class="sxs-lookup"><span data-stu-id="434e4-172">The workflow has several entries, such as `${jobTracker}`.</span></span> <span data-ttu-id="434e4-173">這些項目會取代為您在工作定義中使用的值。</span><span class="sxs-lookup"><span data-stu-id="434e4-173">These entries are replaced by values you use in the job definition.</span></span> <span data-ttu-id="434e4-174">本文件稍後將說明建立工作定義。</span><span class="sxs-lookup"><span data-stu-id="434e4-174">The job definition is created later in this document.</span></span>

     <span data-ttu-id="434e4-175">此外也請注意 Sqoop 區段中的 `<archive>sqljdbc4.jar</arcive>` 項目。</span><span class="sxs-lookup"><span data-stu-id="434e4-175">Also note the `<archive>sqljdbc4.jar</arcive>` entry in the Sqoop section.</span></span> <span data-ttu-id="434e4-176">此項目會指示 Oozie 在此動作執行時，讓 Sqoop 可取得此封存。</span><span class="sxs-lookup"><span data-stu-id="434e4-176">This entry instructs Oozie to make this archive available for Sqoop when this action runs.</span></span>

3. <span data-ttu-id="434e4-177">依序按 Ctrl-X、**Y** 和 **Enter** 鍵以儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="434e4-177">Use Ctrl-X, then **Y** and **Enter** to save the file.</span></span>

4. <span data-ttu-id="434e4-178">使用以下命令，將 **workflow.xml** 檔案複製到 **/tutorials/useoozie/workflow.xml**：</span><span class="sxs-lookup"><span data-stu-id="434e4-178">Use the following command to copy the **workflow.xml** file to **/tutorials/useoozie/workflow.xml**:</span></span>

    ```
    hdfs dfs -put workflow.xml /tutorials/useoozie/workflow.xml
    ```

## <a name="create-the-database"></a><span data-ttu-id="434e4-179">建立資料庫</span><span class="sxs-lookup"><span data-stu-id="434e4-179">Create the database</span></span>

<span data-ttu-id="434e4-180">若要建立 Azure SQL Database，請依照[建立 SQL Database](../sql-database/sql-database-get-started.md) 文件中的步驟執行。</span><span class="sxs-lookup"><span data-stu-id="434e4-180">To create an Azure SQL Database, follow the steps in the [Create a SQL Database](../sql-database/sql-database-get-started.md) document.</span></span> <span data-ttu-id="434e4-181">建立資料庫時，請使用 `oozietest` 做為資料庫名稱。</span><span class="sxs-lookup"><span data-stu-id="434e4-181">When creating the database, use `oozietest` as the database name.</span></span> <span data-ttu-id="434e4-182">也請記下資料庫伺服器的名稱。</span><span class="sxs-lookup"><span data-stu-id="434e4-182">Also make a note of the name of the database server.</span></span>

### <a name="create-the-table"></a><span data-ttu-id="434e4-183">建立資料表</span><span class="sxs-lookup"><span data-stu-id="434e4-183">Create the table</span></span>

> [!NOTE]
> <span data-ttu-id="434e4-184">連接至 SQL Database 建立資料表的方法有很多種。</span><span class="sxs-lookup"><span data-stu-id="434e4-184">There are many ways to connect to SQL Database to create a table.</span></span> <span data-ttu-id="434e4-185">下列步驟會從 HDInsight 叢集使用 [FreeTDS](http://www.freetds.org/) 。</span><span class="sxs-lookup"><span data-stu-id="434e4-185">The following steps use [FreeTDS](http://www.freetds.org/) from the HDInsight cluster.</span></span>


1. <span data-ttu-id="434e4-186">使用以下命令在 HDInsight 叢集上安裝 FreeTDS：</span><span class="sxs-lookup"><span data-stu-id="434e4-186">Use the following command to install FreeTDS on the HDInsight cluster:</span></span>

    ```
    sudo apt-get --assume-yes install freetds-dev freetds-bin
    ```

2. <span data-ttu-id="434e4-187">安裝 FreeTDS 後，請使用下列命令來連接至先前建立的 SQL Database 伺服器：</span><span class="sxs-lookup"><span data-stu-id="434e4-187">Once FreeTDS has been installed, use the following command to connect to the SQL Database server you created previously:</span></span>

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <sqlLogin> -P <sqlPassword> -p 1433 -D oozietest
    ```

    <span data-ttu-id="434e4-188">您會收到如以下文字的輸出：</span><span class="sxs-lookup"><span data-stu-id="434e4-188">You receive output similar to the following text:</span></span>

        locale is "en_US.UTF-8"
        locale charset is "UTF-8"
        using default charset "UTF-8"
        Default database being set to oozietest
        1>

3. <span data-ttu-id="434e4-189">在 `1>` 提示字元輸入下列幾行：</span><span class="sxs-lookup"><span data-stu-id="434e4-189">At the `1>` prompt, enter the following lines:</span></span>

    ```
    CREATE TABLE [dbo].[mobiledata](
    [deviceplatform] [nvarchar](50),
    [count] [bigint])
    GO
    CREATE CLUSTERED INDEX mobiledata_clustered_index on mobiledata(deviceplatform)
    GO
    ```

    <span data-ttu-id="434e4-190">輸入 `GO` 陳述式後，將評估先前的陳述式。</span><span class="sxs-lookup"><span data-stu-id="434e4-190">When the `GO` statement is entered, the previous statements are evaluated.</span></span> <span data-ttu-id="434e4-191">這些陳述式會建立工作流程所使用，名為 **mobiledata** 的資料表。</span><span class="sxs-lookup"><span data-stu-id="434e4-191">These statements create a table named **mobiledata** that is used by the workflow.</span></span>

    <span data-ttu-id="434e4-192">使用下列命令來確認已建立資料表：</span><span class="sxs-lookup"><span data-stu-id="434e4-192">Use the following to verify that the table has been created:</span></span>

    ```
    SELECT * FROM information_schema.tables
    GO
    ```

    <span data-ttu-id="434e4-193">您會看到類似以下的文字：</span><span class="sxs-lookup"><span data-stu-id="434e4-193">You see output similar to the following text:</span></span>

    ```
    TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
    oozietest       dbo     mobiledata      BASE TABLE
    ```

4. <span data-ttu-id="434e4-194">在 `exit` at the `1>` 以結束 tsql 公用程式。</span><span class="sxs-lookup"><span data-stu-id="434e4-194">Enter `exit` at the `1>` prompt to exit the tsql utility.</span></span>

## <a name="create-the-job-definition"></a><span data-ttu-id="434e4-195">建立工作定義</span><span class="sxs-lookup"><span data-stu-id="434e4-195">Create the job definition</span></span>

<span data-ttu-id="434e4-196">工作定義描述 workflow.xml 位於何處。</span><span class="sxs-lookup"><span data-stu-id="434e4-196">The job definition describes where to find the workflow.xml.</span></span> <span data-ttu-id="434e4-197">它也描述工作流程使用的其他檔案 (例如 useooziewf.hql) 位於何處。它也會定義工作流程中所使用的屬性值，以及相關聯的檔案。</span><span class="sxs-lookup"><span data-stu-id="434e4-197">It also describes where to find other files used by the workflow (such as useooziewf.hql.) It also defines the values for properties used within the workflow and associated files.</span></span>

1. <span data-ttu-id="434e4-198">使用以下命令取得預設儲存體的完整位址。</span><span class="sxs-lookup"><span data-stu-id="434e4-198">Use the following command to get the full address of the default storage.</span></span> <span data-ttu-id="434e4-199">稍後在組態檔中會用到此位址：</span><span class="sxs-lookup"><span data-stu-id="434e4-199">This address is used in the configuration file in a moment:</span></span>

    ```
    sed -n '/<name>fs.default/,/<\/value>/p' /etc/hadoop/conf/core-site.xml
    ```

    <span data-ttu-id="434e4-200">此命令會傳回類似以下 XML 的資訊：</span><span class="sxs-lookup"><span data-stu-id="434e4-200">This command returns information similar to the following XML:</span></span>

    ```xml
    <name>fs.defaultFS</name>
    <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net</value>
    ```

    > [!NOTE]
    > <span data-ttu-id="434e4-201">若 HDInsight 叢集使用 Azure 儲存體做為預設儲存體，`<value>` 元素內容的開頭將會是 `wasb://`。</span><span class="sxs-lookup"><span data-stu-id="434e4-201">If the HDInsight cluster uses Azure Storage as the default storage, the `<value>` element contents begin with `wasb://`.</span></span> <span data-ttu-id="434e4-202">若改為使用 Azure Data Lake Store，則其開頭將會是 `adl://`。</span><span class="sxs-lookup"><span data-stu-id="434e4-202">If Azure Data Lake Store is used instead, it begins with `adl://`.</span></span>

    <span data-ttu-id="434e4-203">儲存 `<value>` 元素的內容，因為在後續步驟將會用到它。</span><span class="sxs-lookup"><span data-stu-id="434e4-203">Save the contents of the `<value>` element, as it is used in the next steps.</span></span>

2. <span data-ttu-id="434e4-204">使用以下命令取得叢集前端節點的 FQDN。</span><span class="sxs-lookup"><span data-stu-id="434e4-204">Use the following command to get FQDN of the cluster headnode.</span></span> <span data-ttu-id="434e4-205">此資訊將用於叢集的 JobTracker 位址：</span><span class="sxs-lookup"><span data-stu-id="434e4-205">This information is used for the JobTracker address for the cluster:</span></span>

    ```
    hostname -f
    ```

    <span data-ttu-id="434e4-206">此命令會傳回類似以下文字的資訊：</span><span class="sxs-lookup"><span data-stu-id="434e4-206">This returns information similar to the following text:</span></span>

    ```hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net```

    <span data-ttu-id="434e4-207">用於 JobTracker 的連接埠是 8050，因此將用於 JobTracker 的完整位址是 `hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8050`。</span><span class="sxs-lookup"><span data-stu-id="434e4-207">The port used for the JobTracker is 8050, so the full address to use for the JobTracker is `hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8050`.</span></span>

3. <span data-ttu-id="434e4-208">使用以下命令建立 Oozie 工作定義組態：</span><span class="sxs-lookup"><span data-stu-id="434e4-208">Use the following to create the Oozie job definition configuration:</span></span>

    ```
    nano job.xml
    ```

4. <span data-ttu-id="434e4-209">開啟 nano 編輯器後，請使用下列 XML 做為檔案的內容：</span><span class="sxs-lookup"><span data-stu-id="434e4-209">Once the nano editor opens, use the following XML as the contents of the file:</span></span>

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

   * <span data-ttu-id="434e4-210">將 **wasb://mycontainer@mystorageaccount.blob.core.windows.net** 的所有執行個體取代為您之前收到的預設儲存體值。</span><span class="sxs-lookup"><span data-stu-id="434e4-210">Replace all instances of **wasb://mycontainer@mystorageaccount.blob.core.windows.net** with the value you received earlier for default storage.</span></span>

     > [!WARNING]
     > <span data-ttu-id="434e4-211">若該路徑是 `wasb` 路徑，您必須使用完整路徑。</span><span class="sxs-lookup"><span data-stu-id="434e4-211">If the path is a `wasb` path, you must use the full path.</span></span> <span data-ttu-id="434e4-212">不要將它縮短為 `wasb:///`。</span><span class="sxs-lookup"><span data-stu-id="434e4-212">Do not shorten it to just `wasb:///`.</span></span>

   * <span data-ttu-id="434e4-213">將 **JOBTRACKERADDRESS** 取代為您之前收到的 JobTracker/ResourceManager 位址。</span><span class="sxs-lookup"><span data-stu-id="434e4-213">Replace **JOBTRACKERADDRESS** with the JobTracker/ResourceManager address you received earlier.</span></span>
   * <span data-ttu-id="434e4-214">用您 HDInsight 叢集的登入名稱取代 **YourName** 。</span><span class="sxs-lookup"><span data-stu-id="434e4-214">Replace **YourName** with your login name for the HDInsight cluster.</span></span>
   * <span data-ttu-id="434e4-215">用您 Azure SQL Database 的資訊取代 **serverName**、**adminLogin** 和 **adminPassword**。</span><span class="sxs-lookup"><span data-stu-id="434e4-215">Replace **serverName**, **adminLogin**, and **adminPassword** with the information for your Azure SQL Database.</span></span>

     <span data-ttu-id="434e4-216">此檔案中大部分的資訊都會用來填入 workflow.xml 或 ooziewf.hql 檔案中所使用的值 (例如 ${nameNode})。</span><span class="sxs-lookup"><span data-stu-id="434e4-216">Most of the information in this file is used to populate the values used in the workflow.xml or ooziewf.hql files (such as ${nameNode}.)</span></span>

     > [!NOTE]
     > <span data-ttu-id="434e4-217">**oozie.wf.application.path** 項目會定義要在何處尋找 workflow.xml 檔案，該檔案包含此工作執行過的工作流程。</span><span class="sxs-lookup"><span data-stu-id="434e4-217">The **oozie.wf.application.path** entry defines where to find the workflow.xml file, which contains the workflow ran by this job.</span></span>

5. <span data-ttu-id="434e4-218">依序按 Ctrl-X、**Y** 和 **Enter** 鍵以儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="434e4-218">Use Ctrl-X, then **Y** and **Enter** to save the file.</span></span>

## <a name="submit-and-manage-the-job"></a><span data-ttu-id="434e4-219">提交和管理工作</span><span class="sxs-lookup"><span data-stu-id="434e4-219">Submit and manage the job</span></span>

<span data-ttu-id="434e4-220">下列步驟使用 Oozie 命令提交及管理叢集上的 Oozie 工作流程。</span><span class="sxs-lookup"><span data-stu-id="434e4-220">The following steps use the Oozie command to submit and manage Oozie workflows on the cluster.</span></span> <span data-ttu-id="434e4-221">Oozie 命令是 [Oozie REST API](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html)上的易記介面。</span><span class="sxs-lookup"><span data-stu-id="434e4-221">The Oozie command is a friendly interface over the [Oozie REST API](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="434e4-222">使用 Oozie 命令時，您必須使用 HDInsight 前端節點的 FQDN。</span><span class="sxs-lookup"><span data-stu-id="434e4-222">When using the Oozie command, you must use the FQDN for the HDInsight headnode.</span></span> <span data-ttu-id="434e4-223">只有從叢集才能存取此 FQDN，或者，如果叢集位於 Azure 虛擬網路，就必須從同一個網路中的其他電腦來存取。</span><span class="sxs-lookup"><span data-stu-id="434e4-223">This FQDN is only accessible from the cluster, or if the cluster is on an Azure Virtual Network, from other machines on the same network.</span></span>


1. <span data-ttu-id="434e4-224">使用以下命令取得 Oozie 服務的 URL：</span><span class="sxs-lookup"><span data-stu-id="434e4-224">Use the following to obtain the URL to the Oozie service:</span></span>

    ```
    sed -n '/<name>oozie.base.url/,/<\/value>/p' /etc/oozie/conf/oozie-site.xml
    ```

    <span data-ttu-id="434e4-225">此命令會傳回如以下 XML 的資訊：</span><span class="sxs-lookup"><span data-stu-id="434e4-225">This returns information similar to the following XML:</span></span>

    ```xml
    <name>oozie.base.url</name>
    <value>http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie</value>
    ```

    <span data-ttu-id="434e4-226">`http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie` 部分是要搭配 Oozie 命令使用的 URL。</span><span class="sxs-lookup"><span data-stu-id="434e4-226">The `http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie` portion is the URL to use with the Oozie command.</span></span>

2. <span data-ttu-id="434e4-227">使用以下命令建立 URL 的環境變數，讓您不必為每個命令輸入該 URL：</span><span class="sxs-lookup"><span data-stu-id="434e4-227">Use the following to create an environment variable for the URL, so you don't have to type it for every command:</span></span>

    ```
    export OOZIE_URL=http://HOSTNAMEt:11000/oozie
    ```

    <span data-ttu-id="434e4-228">將 URL 取代為您稍早收到的 URL。</span><span class="sxs-lookup"><span data-stu-id="434e4-228">Replace the URL with the one you received earlier.</span></span>
3. <span data-ttu-id="434e4-229">使用以下命令提交工作：</span><span class="sxs-lookup"><span data-stu-id="434e4-229">Use the following to submit the job:</span></span>

    ```
    oozie job -config job.xml -submit
    ```

    <span data-ttu-id="434e4-230">此命令會從 **job.xml** 載入工作資訊，並將工作資訊提交至 Oozie，但不會執行該工作。</span><span class="sxs-lookup"><span data-stu-id="434e4-230">This command loads the job information from **job.xml** and submits it to Oozie, but does not run it.</span></span>

    <span data-ttu-id="434e4-231">命令完成時，會傳回工作的 ID。</span><span class="sxs-lookup"><span data-stu-id="434e4-231">Once the command completes, it should return the ID of the job.</span></span> <span data-ttu-id="434e4-232">例如， `0000005-150622124850154-oozie-oozi-W`。</span><span class="sxs-lookup"><span data-stu-id="434e4-232">For example, `0000005-150622124850154-oozie-oozi-W`.</span></span> <span data-ttu-id="434e4-233">此 ID 將用來管理工作。</span><span class="sxs-lookup"><span data-stu-id="434e4-233">This ID is used to manage the job.</span></span>

4. <span data-ttu-id="434e4-234">使用以下命令檢視工作的狀態：</span><span class="sxs-lookup"><span data-stu-id="434e4-234">View the status of the job using the following command:</span></span>

    ```
    oozie job -info <JOBID>
    ```

    > [!NOTE]
    > <span data-ttu-id="434e4-235">將 `<JOBID>` 取代為上一個步驟中所傳回的 ID。</span><span class="sxs-lookup"><span data-stu-id="434e4-235">Replace `<JOBID>` with the ID returned in the previous step.</span></span>

    <span data-ttu-id="434e4-236">此命令會傳回類似以下文字的資訊：</span><span class="sxs-lookup"><span data-stu-id="434e4-236">This returns information similar to the following text:</span></span>

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

    <span data-ttu-id="434e4-237">這項工作的狀態為 `PREP`。</span><span class="sxs-lookup"><span data-stu-id="434e4-237">This job has a status of `PREP`.</span></span> <span data-ttu-id="434e4-238">這個狀態表示作業雖已建立但未啟動。</span><span class="sxs-lookup"><span data-stu-id="434e4-238">This status indicates that the job was created, but not started.</span></span>

5. <span data-ttu-id="434e4-239">使用下列命令可啟動工作：</span><span class="sxs-lookup"><span data-stu-id="434e4-239">Use the following command to start the job:</span></span>

    ```
    oozie job -start JOBID
    ```

    > [!NOTE]
    > <span data-ttu-id="434e4-240">使用先前傳回的 ID 取代 `<JOBID>`。</span><span class="sxs-lookup"><span data-stu-id="434e4-240">Replace `<JOBID>` with the ID returned previously.</span></span>

    <span data-ttu-id="434e4-241">如果您在使用此命令後檢查狀態，會發現作業為執行中狀態，並傳回作業內的動作資訊。</span><span class="sxs-lookup"><span data-stu-id="434e4-241">If you check the status after this command, it is in a running state, and information is returned for the actions within the job.</span></span>

6. <span data-ttu-id="434e4-242">工作順利完成後，您可以使用以下命令，確認是否已產生資料並匯出至 SQL Database 資料表：</span><span class="sxs-lookup"><span data-stu-id="434e4-242">Once the task completes successfully, you can verify that the data was generated and exported to the SQL Database table by using the following commands:</span></span>

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D oozietest
    ```

    <span data-ttu-id="434e4-243">在 `1>` 提示字元輸入下列查詢：</span><span class="sxs-lookup"><span data-stu-id="434e4-243">At the `1>` prompt, enter the following query:</span></span>

    ```
    SELECT * FROM mobiledata
    GO
    ```

    <span data-ttu-id="434e4-244">所傳回的資訊類似下列文字︰</span><span class="sxs-lookup"><span data-stu-id="434e4-244">The information returned is similar to the following text:</span></span>

        deviceplatform  count
        Android 31591
        iPhone OS       22731
        proprietary development 3
        RIM OS  3464
        Unknown 213
        Windows Phone   1791
        (6 rows affected)

<span data-ttu-id="434e4-245">如需 Oozie 命令的詳細資訊，請參閱 [Oozie 命令列工具](https://oozie.apache.org/docs/4.1.0/DG_CommandLineTool.html)。</span><span class="sxs-lookup"><span data-stu-id="434e4-245">For more information on the Oozie command, see [Oozie command-line tool](https://oozie.apache.org/docs/4.1.0/DG_CommandLineTool.html).</span></span>

## <a name="oozie-rest-api"></a><span data-ttu-id="434e4-246">Oozie REST API</span><span class="sxs-lookup"><span data-stu-id="434e4-246">Oozie REST API</span></span>

<span data-ttu-id="434e4-247">Oozie REST API 可讓您建置自己的工具來搭配 Oozie 使用。</span><span class="sxs-lookup"><span data-stu-id="434e4-247">The Oozie REST API allows you to build your own tools that work with Oozie.</span></span> <span data-ttu-id="434e4-248">以下為使用 Oozie REST API 時 HDInsight 的特定資訊：</span><span class="sxs-lookup"><span data-stu-id="434e4-248">The following are HDInsight specific information about using the Oozie REST API:</span></span>

* <span data-ttu-id="434e4-249">**URI**：可從叢集的外部 (位於 `https://CLUSTERNAME.azurehdinsight.net/oozie`) 存取 REST API</span><span class="sxs-lookup"><span data-stu-id="434e4-249">**URI**: The REST API can be accessed from outside the cluster at `https://CLUSTERNAME.azurehdinsight.net/oozie`</span></span>

* <span data-ttu-id="434e4-250">**驗證**：使用叢集的 HTTP 帳戶 (admin) 和密碼來驗證 API。</span><span class="sxs-lookup"><span data-stu-id="434e4-250">**Authentication**: Authenticate to the API using the cluster HTTP account (admin) and password.</span></span> <span data-ttu-id="434e4-251">例如：</span><span class="sxs-lookup"><span data-stu-id="434e4-251">For example:</span></span>

    ```
    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/oozie/versions
    ```

<span data-ttu-id="434e4-252">如需使用 Oozie REST API 的詳細資訊，請參閱 [Oozie Web 服務 API](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html)。</span><span class="sxs-lookup"><span data-stu-id="434e4-252">For more information on using the Oozie REST API, see [Oozie Web Services API](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).</span></span>

## <a name="oozie-web-ui"></a><span data-ttu-id="434e4-253">Oozie Web UI</span><span class="sxs-lookup"><span data-stu-id="434e4-253">Oozie Web UI</span></span>

<span data-ttu-id="434e4-254">Oozie Web UI 可讓您用網頁檢視叢集上 Oozie 工作的狀態。</span><span class="sxs-lookup"><span data-stu-id="434e4-254">The Oozie Web UI provides a web-based view into the status of Oozie jobs on the cluster.</span></span> <span data-ttu-id="434e4-255">Web UI 可讓您檢視下列資訊︰</span><span class="sxs-lookup"><span data-stu-id="434e4-255">The web UI allows you to view the following information:</span></span>

* <span data-ttu-id="434e4-256">工作狀態</span><span class="sxs-lookup"><span data-stu-id="434e4-256">Job status</span></span>
* <span data-ttu-id="434e4-257">工作定義</span><span class="sxs-lookup"><span data-stu-id="434e4-257">Job definition</span></span>
* <span data-ttu-id="434e4-258">組態</span><span class="sxs-lookup"><span data-stu-id="434e4-258">Configuration</span></span>
* <span data-ttu-id="434e4-259">工作中的動作圖表</span><span class="sxs-lookup"><span data-stu-id="434e4-259">A graph of the actions in the job</span></span>
* <span data-ttu-id="434e4-260">工作的記錄</span><span class="sxs-lookup"><span data-stu-id="434e4-260">Logs for the job</span></span>

<span data-ttu-id="434e4-261">您也可以檢視工作內的動作詳細資料。</span><span class="sxs-lookup"><span data-stu-id="434e4-261">You can also view details for actions within a job.</span></span>

<span data-ttu-id="434e4-262">若要存取 Oozie Web UI，請依照下列步驟進行：</span><span class="sxs-lookup"><span data-stu-id="434e4-262">To access the Oozie Web UI, use the following steps:</span></span>

1. <span data-ttu-id="434e4-263">建立 HDInsight 叢集的 SSH 通道。</span><span class="sxs-lookup"><span data-stu-id="434e4-263">Create an SSH tunnel to the HDInsight cluster.</span></span> <span data-ttu-id="434e4-264">如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH 通道](hdinsight-linux-ambari-ssh-tunnel.md)文件。</span><span class="sxs-lookup"><span data-stu-id="434e4-264">For information, see the [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

2. <span data-ttu-id="434e4-265">建立通道後，請在網頁瀏覽器中開啟 Ambari Web UI。</span><span class="sxs-lookup"><span data-stu-id="434e4-265">Once a tunnel has been created, open the Ambari web UI in your web browser.</span></span> <span data-ttu-id="434e4-266">Ambari 網站的 URI 是 **https://CLUSTERNAME.azurehdinsight.net**。</span><span class="sxs-lookup"><span data-stu-id="434e4-266">The URI for the Ambari site is **https://CLUSTERNAME.azurehdinsight.net**.</span></span> <span data-ttu-id="434e4-267">請將 **CLUSTERNAME** 取代為您的 Linux 型 HDInsight 叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="434e4-267">Replace **CLUSTERNAME** with the name of your Linux-based HDInsight cluster.</span></span>

3. <span data-ttu-id="434e4-268">在頁面左邊選取 [Oozie]，然後依序選取 [快速連結] 和 [Oozie Web UI]。</span><span class="sxs-lookup"><span data-stu-id="434e4-268">From the left side of the page, select **Oozie**, then **Quick Links**, and finally **Oozie Web UI**.</span></span>

    ![功能表的圖](./media/hdinsight-use-oozie-linux-mac/ooziewebuisteps.png)

4. <span data-ttu-id="434e4-270">Oozie Web UI 預設會顯示執行中的工作流程工作。</span><span class="sxs-lookup"><span data-stu-id="434e4-270">The Oozie Web UI defaults to displaying running Workflow Jobs.</span></span> <span data-ttu-id="434e4-271">若要查看所有的工作流程工作，請選取 [所有工作] 。</span><span class="sxs-lookup"><span data-stu-id="434e4-271">To see all workflow jobs, select **All Jobs**.</span></span>

    ![顯示的所有工作](./media/hdinsight-use-oozie-linux-mac/ooziejobs.png)

5. <span data-ttu-id="434e4-273">選取一項工作，以檢視該工作的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="434e4-273">Select a job to view more information about the job.</span></span>

    ![工作資訊](./media/hdinsight-use-oozie-linux-mac/jobinfo.png)

6. <span data-ttu-id="434e4-275">您可以在 [Job Info (工作資訊)] 索引標籤中看到基本的工作資訊，以及工作內的個別動作。</span><span class="sxs-lookup"><span data-stu-id="434e4-275">From the Job Info tab, you can see basic job information and the individual actions within the job.</span></span> <span data-ttu-id="434e4-276">使用上方的索引標籤，即可檢視 Job Definition (工作定義)、Job Configuration (工作組態)，以及存取 Job Log (工作記錄)，或檢視工作的定向非循環圖 (DAG)。</span><span class="sxs-lookup"><span data-stu-id="434e4-276">Using the tabs at the top you can view the Job Definition, Job Configuration, access the Job Log or view a Directed Acyclic Graph (DAG) of the job.</span></span>

   * <span data-ttu-id="434e4-277">**作業記錄**：選取 [取得記錄] 按鈕，以取得作業的所有記錄，或使用 [輸入搜尋篩選條件] 欄位來篩選記錄</span><span class="sxs-lookup"><span data-stu-id="434e4-277">**Job Log**: Select the **GetLogs** button to get all logs for the job, or use the **Enter Search Filter** field to filter logs</span></span>

       ![工作記錄](./media/hdinsight-use-oozie-linux-mac/joblog.png)

   * <span data-ttu-id="434e4-279">**JobDAG**：DAG 是將整個工作流程所採取的資料路徑予以圖形化的概觀</span><span class="sxs-lookup"><span data-stu-id="434e4-279">**JobDAG**: The DAG is a graphical overview of the data paths taken through the workflow</span></span>

       ![工作 DAG](./media/hdinsight-use-oozie-linux-mac/jobdag.png)

7. <span data-ttu-id="434e4-281">在 [作業資訊] 索引標籤中選取其中一個動作，以顯示該動作的資訊。</span><span class="sxs-lookup"><span data-stu-id="434e4-281">Selecting one of the actions from the **Job Info** tab brings up information for the action.</span></span> <span data-ttu-id="434e4-282">例如，選取 **RunHiveScript** 動作。</span><span class="sxs-lookup"><span data-stu-id="434e4-282">For example, select the **RunHiveScript** action.</span></span>

    ![動作資訊](./media/hdinsight-use-oozie-linux-mac/action.png)

8. <span data-ttu-id="434e4-284">您可以查看動作的詳細資料，例如 **Console URL** (主控台 URL) 的連結。</span><span class="sxs-lookup"><span data-stu-id="434e4-284">You can see details for the action, such as a link to the **Console URL**.</span></span> <span data-ttu-id="434e4-285">此連結可用來檢視工作的 JobTracker 資訊。</span><span class="sxs-lookup"><span data-stu-id="434e4-285">This link can be used to view JobTracker information for the job.</span></span>

## <a name="scheduling-jobs"></a><span data-ttu-id="434e4-286">排程工作</span><span class="sxs-lookup"><span data-stu-id="434e4-286">Scheduling jobs</span></span>

<span data-ttu-id="434e4-287">協調器可讓您指定工作的開始時間、結束時間和發生頻率。</span><span class="sxs-lookup"><span data-stu-id="434e4-287">The coordinator allows you to specify a start, end, and occurrence frequency for jobs.</span></span> <span data-ttu-id="434e4-288">若要定義工作流程的排程，請依照下列步驟進行：</span><span class="sxs-lookup"><span data-stu-id="434e4-288">To define a schedule for the workflow, use the following steps:</span></span>

1. <span data-ttu-id="434e4-289">使用以下命令建立名為 **coordinator.xml** 的檔案：</span><span class="sxs-lookup"><span data-stu-id="434e4-289">Use the following to create a file named **coordinator.xml**:</span></span>

    ```
    nano coordinator.xml
    ```

    <span data-ttu-id="434e4-290">使用下列 XML 做為檔案的內容：</span><span class="sxs-lookup"><span data-stu-id="434e4-290">Use the following XML as the contents of the file:</span></span>

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
    > <span data-ttu-id="434e4-291">`${...}` 變數在執行階段將被工作定義中的值取代。</span><span class="sxs-lookup"><span data-stu-id="434e4-291">The `${...}` variables are replaced by values in the job definition at run-time.</span></span> <span data-ttu-id="434e4-292">這些變數分為別：</span><span class="sxs-lookup"><span data-stu-id="434e4-292">The variables are:</span></span>
    >
    > * <span data-ttu-id="434e4-293">`${coordFrequency}`：執行工作執行個體的間隔時間。</span><span class="sxs-lookup"><span data-stu-id="434e4-293">`${coordFrequency}`: Time between running instances of the job.</span></span>
    > <span data-ttu-id="434e4-294">** `${coordStart}`：工作開始時間。</span><span class="sxs-lookup"><span data-stu-id="434e4-294">** `${coordStart}`: The job start time.</span></span>
    > * <span data-ttu-id="434e4-295">`${coordEnd}`：工作結束時間。</span><span class="sxs-lookup"><span data-stu-id="434e4-295">`${coordEnd}`: The job end time.</span></span>
    > * <span data-ttu-id="434e4-296">`${coordTimezone}`：協調器工作位在固定時區，不受日光節約時間影響 (通常使用 UTC 表示)。</span><span class="sxs-lookup"><span data-stu-id="434e4-296">`${coordTimezone}`: Coordinator jobs are in a fixed time zone with no daylight savings time (typically represented by using UTC).</span></span> <span data-ttu-id="434e4-297">此時區稱為「Oozie 處理時區」。</span><span class="sxs-lookup"><span data-stu-id="434e4-297">This time zone is referred as the "Oozie processing timezone."</span></span>
    > * <span data-ttu-id="434e4-298">`${wfPath}`：workflow.xml 的路徑。</span><span class="sxs-lookup"><span data-stu-id="434e4-298">`${wfPath}`: The path to the workflow.xml.</span></span>

2. <span data-ttu-id="434e4-299">若要儲存檔案，請使用 Ctrl-X、**Y** 和 **Enter** 鍵。</span><span class="sxs-lookup"><span data-stu-id="434e4-299">To save the file, use Ctrl-X, **Y**, and **Enter**.</span></span>

3. <span data-ttu-id="434e4-300">使用以下命令將該檔案複製到此作業的工作目錄：</span><span class="sxs-lookup"><span data-stu-id="434e4-300">Use the following command to copy the file to the working directory for this job:</span></span>

    ```
    hadoop fs -put coordinator.xml /tutorials/useoozie/coordinator.xml
    ```

4. <span data-ttu-id="434e4-301">使用以下命令修改 **job.xml** 檔案：</span><span class="sxs-lookup"><span data-stu-id="434e4-301">Use the following to modify the **job.xml** file:</span></span>

    ```
    nano job.xml
    ```

    <span data-ttu-id="434e4-302">進行下列變更：</span><span class="sxs-lookup"><span data-stu-id="434e4-302">Make the following changes:</span></span>

   * <span data-ttu-id="434e4-303">若要指示 Oozie 執行協調器檔案而非工作流程，請將 `<name>oozie.wf.application.path</name>` 變更為 `<name>oozie.coord.application.path</name>`。</span><span class="sxs-lookup"><span data-stu-id="434e4-303">To instruct oozie to run the coordinator file instead of the workflow, change `<name>oozie.wf.application.path</name>` to `<name>oozie.coord.application.path</name>`.</span></span>

   * <span data-ttu-id="434e4-304">若要設定協調器使用的 `workflowPath` 變數，請新增下列 XML：</span><span class="sxs-lookup"><span data-stu-id="434e4-304">To set the `workflowPath` variable used by the coordinator, add the following XML:</span></span>

        ```xml
        <property>
            <name>workflowPath</name>
            <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie</value>
        </property>
        ```

       <span data-ttu-id="434e4-305">將 `wasb://mycontainer@mystorageaccount.blob.core.windows` 文字取代為在 job.xml 檔案之其他項目中使用的值。</span><span class="sxs-lookup"><span data-stu-id="434e4-305">Replace the `wasb://mycontainer@mystorageaccount.blob.core.windows` text with the value used in other entries in the job.xml file.</span></span>

   * <span data-ttu-id="434e4-306">若要定義協調器的開始時間、結束時間和頻率，請新增下列 XML：</span><span class="sxs-lookup"><span data-stu-id="434e4-306">To define the start, end, and frequency for the coordinator, add the following XML:</span></span>

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

       <span data-ttu-id="434e4-307">這些值會將開始時間設為 2017 年 5 月 10 日下午 12:00，將結束時間設為 2017 年 5 月 12 日。</span><span class="sxs-lookup"><span data-stu-id="434e4-307">These values set the start time to 12:00PM on May 10, 2017, the end time to May 12, 2017.</span></span> <span data-ttu-id="434e4-308">執行此工作的間隔是每日。</span><span class="sxs-lookup"><span data-stu-id="434e4-308">The interval for running this job daily.</span></span> <span data-ttu-id="434e4-309">頻率的單位是分鐘，因此 24 小時 x 60 分鐘 = 1440 分鐘。</span><span class="sxs-lookup"><span data-stu-id="434e4-309">The frequency is in minutes, so 24 hours x 60 minutes = 1440 minutes.</span></span> <span data-ttu-id="434e4-310">最後，時區會設定為 UTC。</span><span class="sxs-lookup"><span data-stu-id="434e4-310">Finally, the timezone is set to UTC.</span></span>

5. <span data-ttu-id="434e4-311">依序按 Ctrl-X、**Y** 和 **Enter** 鍵以儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="434e4-311">Use Ctrl-X, then **Y** and **Enter** to save the file.</span></span>

6. <span data-ttu-id="434e4-312">若要執行工作，請使用以下命令：</span><span class="sxs-lookup"><span data-stu-id="434e4-312">To run the job, use the following command:</span></span>

    ```
    oozie job -config job.xml -run
    ```

    <span data-ttu-id="434e4-313">此命令會提交並啟動工作。</span><span class="sxs-lookup"><span data-stu-id="434e4-313">This command submits and starts the job.</span></span>

7. <span data-ttu-id="434e4-314">如果您瀏覽 Oozie Web UI，並選取 [Coordinator Jobs (協調器工作)] 索引標籤，您會看到如下圖的資訊：</span><span class="sxs-lookup"><span data-stu-id="434e4-314">If you visit the Oozie Web UI and select the **Coordinator Jobs** tab, you see information similar to the following image:</span></span>

    ![協調器工作索引標籤](./media/hdinsight-use-oozie-linux-mac/coordinatorjob.png)

    <span data-ttu-id="434e4-316">[Next Materialization (下次具體化)] 項目包含下次工作執行的時間。</span><span class="sxs-lookup"><span data-stu-id="434e4-316">The **Next Materialization** entry contains the next time that the job runs.</span></span>

8. <span data-ttu-id="434e4-317">與先前的工作流程作業類似，在 Web UI 中選取作業項目會顯示作業的資訊：</span><span class="sxs-lookup"><span data-stu-id="434e4-317">Similar to the earlier workflow job, selecting the job entry in the web UI displays information on the job:</span></span>

    ![協調器工作資訊](./media/hdinsight-use-oozie-linux-mac/coordinatorjobinfo.png)

    > [!NOTE]
    > <span data-ttu-id="434e4-319">此影像只會顯示工作的成功執行項目，而不是排程工作流程內的個別動作。</span><span class="sxs-lookup"><span data-stu-id="434e4-319">This image only shows successful runs of the job, not individual actions within the scheduled workflow.</span></span> <span data-ttu-id="434e4-320">若要查看這些動作，請選取其中一個 [動作]  項目。</span><span class="sxs-lookup"><span data-stu-id="434e4-320">To see that, select one of the **Action** entries.</span></span>

    ![動作資訊](./media/hdinsight-use-oozie-linux-mac/coordinatoractionjob.png)

## <a name="troubleshooting"></a><span data-ttu-id="434e4-322">疑難排解</span><span class="sxs-lookup"><span data-stu-id="434e4-322">Troubleshooting</span></span>

<span data-ttu-id="434e4-323">Oozie UI 可讓您檢視 Oozie 記錄。</span><span class="sxs-lookup"><span data-stu-id="434e4-323">The Oozie UI allows you to view Oozie logs.</span></span> <span data-ttu-id="434e4-324">它也包含工作流程啟動之 MapReduce 工作的 JobTracker 記錄連結。</span><span class="sxs-lookup"><span data-stu-id="434e4-324">It also contains links to JobTracker logs for MapReduce tasks started by the workflow.</span></span> <span data-ttu-id="434e4-325">疑難排解的模式應該是：</span><span class="sxs-lookup"><span data-stu-id="434e4-325">The pattern for troubleshooting should be:</span></span>

1. <span data-ttu-id="434e4-326">在 Oozie Web UI 中檢視工作。</span><span class="sxs-lookup"><span data-stu-id="434e4-326">View the job in Oozie Web UI.</span></span>

2. <span data-ttu-id="434e4-327">如果發生錯誤或特定動作失敗，請選取該動作，以查看 [Error Message] \(錯誤訊息)  欄位是否有提供失敗的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="434e4-327">If there is an error or failure for a specific action, select the action to see if the **Error Message** field provides more information on the failure.</span></span>

3. <span data-ttu-id="434e4-328">如果有提供，請使用動作的 URL 以檢視動作的更多詳細資料 (例如 JobTracker 記錄)。</span><span class="sxs-lookup"><span data-stu-id="434e4-328">If available, use the URL from the action to view more details (such as JobTracker logs) for the action.</span></span>

<span data-ttu-id="434e4-329">以下是您可能會遇到的特定錯誤，以及解決這些問題的方法。</span><span class="sxs-lookup"><span data-stu-id="434e4-329">The following are specific errors you may encounter, and how to resolve them.</span></span>

### <a name="ja009-cannot-initialize-cluster"></a><span data-ttu-id="434e4-330">JA009：無法初始化叢集</span><span class="sxs-lookup"><span data-stu-id="434e4-330">JA009: Cannot initialize cluster</span></span>

<span data-ttu-id="434e4-331">**徵兆**：作業狀態會變更為 **SUSPENDED**。</span><span class="sxs-lookup"><span data-stu-id="434e4-331">**Symptoms**: The job status changes to **SUSPENDED**.</span></span> <span data-ttu-id="434e4-332">工作的詳細資料會將 RunHiveScript 狀態顯示為 **START_MANUAL**。</span><span class="sxs-lookup"><span data-stu-id="434e4-332">Details for the job show the RunHiveScript status as **START_MANUAL**.</span></span> <span data-ttu-id="434e4-333">選取該動作會顯示下列錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="434e4-333">Selecting the action displays the following error message:</span></span>

    JA009: Cannot initialize Cluster. Please check your configuration for map

<span data-ttu-id="434e4-334">**原因**：**job.xml** 檔案中使用的 WASB 位址未包含儲存體容器或儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="434e4-334">**Cause**: The WASB addresses used in the **job.xml** file do not contain the storage container or storage account name.</span></span> <span data-ttu-id="434e4-335">WASB 位址格式必須是 `wasb://containername@storageaccountname.blob.core.windows.net`。</span><span class="sxs-lookup"><span data-stu-id="434e4-335">The WASB address format must be `wasb://containername@storageaccountname.blob.core.windows.net`.</span></span>

<span data-ttu-id="434e4-336">**解決方法**：變更工作所使用的 WASB 位址。</span><span class="sxs-lookup"><span data-stu-id="434e4-336">**Resolution**: Change the WASB addresses used by the job.</span></span>

### <a name="ja002-oozie-is-not-allowed-to-impersonate-ltuser"></a><span data-ttu-id="434e4-337">JA002：不允許 Oozie 模擬 &lt;USER></span><span class="sxs-lookup"><span data-stu-id="434e4-337">JA002: Oozie is not allowed to impersonate &lt;USER></span></span>

<span data-ttu-id="434e4-338">**徵兆**：作業狀態會變更為 **SUSPENDED**。</span><span class="sxs-lookup"><span data-stu-id="434e4-338">**Symptoms**: The job status changes to **SUSPENDED**.</span></span> <span data-ttu-id="434e4-339">工作的詳細資料會將 RunHiveScript 狀態顯示為 **START_MANUAL**。</span><span class="sxs-lookup"><span data-stu-id="434e4-339">Details for the job show the RunHiveScript status as **START_MANUAL**.</span></span> <span data-ttu-id="434e4-340">選取該動作會顯示下列錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="434e4-340">Selecting the action shows the following error message:</span></span>

    JA002: User: oozie is not allowed to impersonate <USER>

<span data-ttu-id="434e4-341">**原因**：目前的權限設定不允許 Oozie 模擬指定的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="434e4-341">**Cause**: Current permission settings do not allow Oozie to impersonate the specified user account.</span></span>

<span data-ttu-id="434e4-342">**解決方法**：Oozie 可以模擬 **users** 群組中的使用者。</span><span class="sxs-lookup"><span data-stu-id="434e4-342">**Resolution**: Oozie is allowed to impersonate users in the **users** group.</span></span> <span data-ttu-id="434e4-343">使用 `groups USERNAME` 查看使用者帳戶所屬的群組。</span><span class="sxs-lookup"><span data-stu-id="434e4-343">Use the `groups USERNAME` to see the groups that the user account is a member of.</span></span> <span data-ttu-id="434e4-344">如果使用者不是 **users** 群組的成員，請使用以下命令將使用者新增至群組：</span><span class="sxs-lookup"><span data-stu-id="434e4-344">If the user is not a member of the **users** group, use the following command to add the user to the group:</span></span>

    sudo adduser USERNAME users

> [!NOTE]
> <span data-ttu-id="434e4-345">這可能需要幾分鐘，HDInsight 才能辨識出使用者已新增至該群組。</span><span class="sxs-lookup"><span data-stu-id="434e4-345">It may take several minutes before HDInsight recognizes that the user has been added to the group.</span></span>

### <a name="launcher-error-sqoop"></a><span data-ttu-id="434e4-346">啟動器錯誤 (Sqoop)</span><span class="sxs-lookup"><span data-stu-id="434e4-346">Launcher ERROR (Sqoop)</span></span>

<span data-ttu-id="434e4-347">**徵兆**：作業狀態會變更為 **KILLED**。</span><span class="sxs-lookup"><span data-stu-id="434e4-347">**Symptoms**: The job status changes to **KILLED**.</span></span> <span data-ttu-id="434e4-348">工作的詳細資料會將 RunSqoopExport 狀態顯示為 **ERROR**。</span><span class="sxs-lookup"><span data-stu-id="434e4-348">Details for the job show the RunSqoopExport status as **ERROR**.</span></span> <span data-ttu-id="434e4-349">選取該動作會顯示下列錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="434e4-349">Selecting the action shows the following error message:</span></span>

    Launcher ERROR, reason: Main class [org.apache.oozie.action.hadoop.SqoopMain], exit code [1]

<span data-ttu-id="434e4-350">**原因**：Sqoop 無法載入存取資料庫時所需的資料庫驅動程式。</span><span class="sxs-lookup"><span data-stu-id="434e4-350">**Cause**: Sqoop is unable to load the database driver required to access the database.</span></span>

<span data-ttu-id="434e4-351">**解決方法**：從 Oozie 工作使用 Sqoop 時，必須將資料庫驅動程式與工作所使用的其他資源 (例如 workflow.xml) 包含在一起。</span><span class="sxs-lookup"><span data-stu-id="434e4-351">**Resolution**: When using Sqoop from an Oozie job, you must include the database driver with the other resources (such as the workflow.xml) used by the job.</span></span> <span data-ttu-id="434e4-352">您還必須從 workflow.xml 的 `<sqoop>...</sqoop>` 區段，參考含有資料庫驅動程式的封存。</span><span class="sxs-lookup"><span data-stu-id="434e4-352">Also Reference the archive containing the database driver from the `<sqoop>...</sqoop>` section of the workflow.xml.</span></span>

<span data-ttu-id="434e4-353">例如，您可以針對本文件中的工作使用下列步驟：</span><span class="sxs-lookup"><span data-stu-id="434e4-353">For example, for the job in this document, you would use the following steps:</span></span>

1. <span data-ttu-id="434e4-354">將 sqljdbc4.1.jar 檔複製到 /tutorials/useoozie 目錄：</span><span class="sxs-lookup"><span data-stu-id="434e4-354">Copy the sqljdbc4.1.jar file to the /tutorials/useoozie directory:</span></span>

    ```
    hdfs dfs -put /usr/share/java/sqljdbc_4.1/enu/sqljdbc41.jar /tutorials/useoozie/sqljdbc41.jar
    ```

2. <span data-ttu-id="434e4-355">修改 workflow.xml，在 `</sqoop>` 上方用新的一行加入下列 XML：</span><span class="sxs-lookup"><span data-stu-id="434e4-355">Modify the workflow.xml to add the following XML on a new line above `</sqoop>`:</span></span>

    ```xml
    <archive>sqljdbc41.jar</archive>
    ```

## <a name="next-steps"></a><span data-ttu-id="434e4-356">後續步驟</span><span class="sxs-lookup"><span data-stu-id="434e4-356">Next steps</span></span>

<span data-ttu-id="434e4-357">在本教學課程中，您已了解如何定義 Oozie 工作流程，以及如何執行 Oozie 工作。</span><span class="sxs-lookup"><span data-stu-id="434e4-357">In this tutorial, you learned how to define an Oozie workflow and how to run an Oozie job.</span></span> <span data-ttu-id="434e4-358">若要深入了解如何使用 HDInsight，請參閱下列文章：</span><span class="sxs-lookup"><span data-stu-id="434e4-358">To learn more about working with HDInsight, see the following articles:</span></span>

* <span data-ttu-id="434e4-359">[搭配 HDInsight 使用以時間為基礎的 Hadoop Oozie 協調器][hdinsight-oozie-coordinator-time]</span><span class="sxs-lookup"><span data-stu-id="434e4-359">[Use time-based Oozie Coordinator with HDInsight][hdinsight-oozie-coordinator-time]</span></span>
* <span data-ttu-id="434e4-360">[在 HDInsight 中上傳 Hadoop 作業的資料][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="434e4-360">[Upload data for Hadoop jobs in HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="434e4-361">[搭配使用 Sqoop 與 HDInsight 中的 Hadoop][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="434e4-361">[Use Sqoop with Hadoop in HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="434e4-362">[搭配使用 Hive 與 HDInsight 上的 Hadoop][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="434e4-362">[Use Hive with Hadoop on HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="434e4-363">[搭配使用 Pig 與 HDInsight 上的 Hadoop][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="434e4-363">[Use Pig with Hadoop on HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="434e4-364">[開發 HDInsight 的 Java MapReduce 程式][hdinsight-develop-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="434e4-364">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-mapreduce]</span></span>

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
