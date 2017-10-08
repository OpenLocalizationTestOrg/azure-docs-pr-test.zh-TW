---
title: "在 HDInsight Hadoop Oozie aaaUse |Microsoft 文件"
description: "在 HDInsight 上使用 Hadoop Oozie：一項巨量資料服務。 深入了解如何 toodefine Oozie 工作流程，並提交 Oozie 作業。"
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 870098f0-f416-4491-9719-78994bf4a369
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 12d0cf1a01838ab0f4e699c384ce2fb18f85cbad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-oozie-with-hadoop-toodefine-and-run-a-workflow-in-hdinsight"></a><span data-ttu-id="9e74c-104">使用 Hadoop toodefine Oozie 和 HDInsight 中執行的工作流程</span><span class="sxs-lookup"><span data-stu-id="9e74c-104">Use Oozie with Hadoop toodefine and run a workflow in HDInsight</span></span>
[!INCLUDE [oozie-selector](../../includes/hdinsight-oozie-selector.md)]

<span data-ttu-id="9e74c-105">了解 toouse Apache Oozie toodefine 工作流程和執行 hello HDInsight 上的工作流程。</span><span class="sxs-lookup"><span data-stu-id="9e74c-105">Learn how toouse Apache Oozie toodefine a workflow and run hello workflow on HDInsight.</span></span> <span data-ttu-id="9e74c-106">toolearn 有關 hello Oozie 協調器，請參閱[HDInsight 搭配使用以時間為基礎的 Hadoop Oozie 協調器][hdinsight-oozie-coordinator-time]。</span><span class="sxs-lookup"><span data-stu-id="9e74c-106">toolearn about hello Oozie coordinator, see [Use time-based Hadoop Oozie Coordinator with HDInsight][hdinsight-oozie-coordinator-time].</span></span> <span data-ttu-id="9e74c-107">toolearn Azure Data Factory，請參閱[搭配使用 Pig 和 Hive 與 Data Factory][azure-data-factory-pig-hive]。</span><span class="sxs-lookup"><span data-stu-id="9e74c-107">toolearn Azure Data Factory, see [Use Pig and Hive with Data Factory][azure-data-factory-pig-hive].</span></span>

<span data-ttu-id="9e74c-108">Apache Oozie 是可管理 Hadoop 工作的工作流程/協調系統。</span><span class="sxs-lookup"><span data-stu-id="9e74c-108">Apache Oozie is a workflow/coordination system that manages Hadoop jobs.</span></span> <span data-ttu-id="9e74c-109">Hello Hadoop 堆疊，與整合，並支援 Apache MapReduce、 Apache Pig、 Apache Hive，和 Apache Sqoop Hadoop 工作。</span><span class="sxs-lookup"><span data-stu-id="9e74c-109">It is integrated with hello Hadoop stack, and it supports Hadoop jobs for Apache MapReduce, Apache Pig, Apache Hive, and Apache Sqoop.</span></span> <span data-ttu-id="9e74c-110">它也可以使用的 tooschedule 作業的特定 tooa 系統，例如 Java 程式或殼層指令碼。</span><span class="sxs-lookup"><span data-stu-id="9e74c-110">It can also be used tooschedule jobs that are specific tooa system, like Java programs or shell scripts.</span></span>

<span data-ttu-id="9e74c-111">您遵循本教學課程中的 hello 指示實作 hello 工作流程包含兩個動作：</span><span class="sxs-lookup"><span data-stu-id="9e74c-111">hello workflow you implement by following hello instructions in this tutorial contains two actions:</span></span>

![Workflow diagram][img-workflow-diagram]

1. <span data-ttu-id="9e74c-113">登錄區動作會執行下列 HiveQL 指令碼 toocount hello 每個記錄層級類型的發生 log4j 檔案中。</span><span class="sxs-lookup"><span data-stu-id="9e74c-113">A Hive action runs a HiveQL script toocount hello occurrences of each log-level type in a log4j file.</span></span> <span data-ttu-id="9e74c-114">每個 log4j 檔案欄位的一行，其中包含顯示 hello 類型和 hello 嚴重性，例如 [記錄層級] 欄位所組成：</span><span class="sxs-lookup"><span data-stu-id="9e74c-114">Each log4j file consists of a line of fields that contains a [LOG LEVEL] field that shows hello type and hello severity, for example:</span></span>
   
        2012-02-03 18:35:34 SampleClass6 [INFO] everything normal for id 577725851
        2012-02-03 18:35:34 SampleClass4 [FATAL] system problem at id 1991281254
        2012-02-03 18:35:34 SampleClass3 [DEBUG] detail for id 1304807656
        ...
   
    <span data-ttu-id="9e74c-115">hello Hive 指令碼輸出如下：</span><span class="sxs-lookup"><span data-stu-id="9e74c-115">hello Hive script output is similar to:</span></span>
   
        [DEBUG] 434
        [ERROR] 3
        [FATAL] 1
        [INFO]  96
        [TRACE] 816
        [WARN]  4
   
    <span data-ttu-id="9e74c-116">如需 Hive 的詳細資訊，請參閱[在 HDInsight 上使用 Hive][hdinsight-use-hive]。</span><span class="sxs-lookup"><span data-stu-id="9e74c-116">For more information about Hive, see [Use Hive with HDInsight][hdinsight-use-hive].</span></span>
2. <span data-ttu-id="9e74c-117">Sqoop 動作匯出 Azure SQL database 中的 hello HiveQL 輸出 tooa 資料表。</span><span class="sxs-lookup"><span data-stu-id="9e74c-117">A Sqoop action exports hello HiveQL output tooa table in an Azure SQL database.</span></span> <span data-ttu-id="9e74c-118">如需 Sqoop 的詳細資訊，請參閱[搭配 HDInsight 使用 Hadoop Sqoop][hdinsight-use-sqoop]。</span><span class="sxs-lookup"><span data-stu-id="9e74c-118">For more information about Sqoop, see [Use Hadoop Sqoop with HDInsight][hdinsight-use-sqoop].</span></span>

> [!NOTE]
> <span data-ttu-id="9e74c-119">HDInsight 叢集上支援 Oozie 版本，請參閱[hello HDInsight 所提供的 Hadoop 叢集版本中最新消息？][hdinsight-versions].</span><span class="sxs-lookup"><span data-stu-id="9e74c-119">For supported Oozie versions on HDInsight clusters, see [What's new in hello Hadoop cluster versions provided by HDInsight?][hdinsight-versions].</span></span>
> 
> 

### <a name="prerequisites"></a><span data-ttu-id="9e74c-120">必要條件</span><span class="sxs-lookup"><span data-stu-id="9e74c-120">Prerequisites</span></span>
<span data-ttu-id="9e74c-121">開始本教學課程之前，您必須擁有 hello 下列項目：</span><span class="sxs-lookup"><span data-stu-id="9e74c-121">Before you begin this tutorial, you must have hello following item:</span></span>

* <span data-ttu-id="9e74c-122">**具有 Azure PowerShell 的工作站**。</span><span class="sxs-lookup"><span data-stu-id="9e74c-122">**A workstation with Azure PowerShell**.</span></span> 
  

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]
  

## <a name="define-oozie-workflow-and-hello-related-hiveql-script"></a><span data-ttu-id="9e74c-123">定義 Oozie 工作流程和 hello 相關的下列 HiveQL 指令碼</span><span class="sxs-lookup"><span data-stu-id="9e74c-123">Define Oozie workflow and hello related HiveQL script</span></span>
<span data-ttu-id="9e74c-124">Oozie 工作流程定義會以 hPDL 撰寫 (一種 XML 程序定義語言)。</span><span class="sxs-lookup"><span data-stu-id="9e74c-124">Oozie workflows definitions are written in hPDL (a XML Process Definition Language).</span></span> <span data-ttu-id="9e74c-125">hello 預設工作流程檔案名稱是*workflow.xml*。</span><span class="sxs-lookup"><span data-stu-id="9e74c-125">hello default workflow file name is *workflow.xml*.</span></span> <span data-ttu-id="9e74c-126">hello 以下是您在本教學課程中使用的 hello 工作流程檔案。</span><span class="sxs-lookup"><span data-stu-id="9e74c-126">hello following is hello workflow file you use in this tutorial.</span></span>

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
                <param>hiveOutputFolder=${hiveOutputFolder}</param>
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
            <arg>${hiveOutputFolder}</arg>
            <arg>-m</arg>
            <arg>1</arg>
            <arg>--input-fields-terminated-by</arg>
            <arg>"\001"</arg>
            </sqoop>
            <ok to="end"/>
            <error to="fail"/>
        </action>

        <kill name="fail">
            <message>Job failed, error message[${wf:errorMessage(wf:lastErrorNode())}] </message>
        </kill>

        <end name="end"/>
    </workflow-app>

<span data-ttu-id="9e74c-127">有兩個 hello 工作流程中定義的動作。</span><span class="sxs-lookup"><span data-stu-id="9e74c-127">There are two actions defined in hello workflow.</span></span> <span data-ttu-id="9e74c-128">hello 開始 tooaction 是*RunHiveScript*。</span><span class="sxs-lookup"><span data-stu-id="9e74c-128">hello start-tooaction is *RunHiveScript*.</span></span> <span data-ttu-id="9e74c-129">如果 hello 動作成功執行，hello 下一個動作是*RunSqoopExport*。</span><span class="sxs-lookup"><span data-stu-id="9e74c-129">If hello action runs successfully, hello next action is *RunSqoopExport*.</span></span>

<span data-ttu-id="9e74c-130">hello RunHiveScript 有數個變數。</span><span class="sxs-lookup"><span data-stu-id="9e74c-130">hello RunHiveScript has several variables.</span></span> <span data-ttu-id="9e74c-131">當您使用 Azure PowerShell 提交從工作站 hello Oozie 作業時，您可以傳遞 hello 值。</span><span class="sxs-lookup"><span data-stu-id="9e74c-131">You pass hello values when you submit hello Oozie job from your workstation by using Azure PowerShell.</span></span>

<table border = "1">
<tr><th><span data-ttu-id="9e74c-132">工作流程變數</span><span class="sxs-lookup"><span data-stu-id="9e74c-132">Workflow variables</span></span></th><th><span data-ttu-id="9e74c-133">說明</span><span class="sxs-lookup"><span data-stu-id="9e74c-133">Description</span></span></th></tr>
<tr><td><span data-ttu-id="9e74c-134">${jobTracker}</span><span class="sxs-lookup"><span data-stu-id="9e74c-134">${jobTracker}</span></span></td><td><span data-ttu-id="9e74c-135">指定 hello URL hello Hadoop 作業追蹤程式。</span><span class="sxs-lookup"><span data-stu-id="9e74c-135">Specifies hello URL of hello Hadoop job tracker.</span></span> <span data-ttu-id="9e74c-136">在 HDInsight 3.0 和 2.1 版中使用 <strong>jobtrackerhost:9010</strong>。</span><span class="sxs-lookup"><span data-stu-id="9e74c-136">Use <strong>jobtrackerhost:9010</strong> in HDInsight version 3.0 and 2.1.</span></span></td></tr>
<tr><td><span data-ttu-id="9e74c-137">${nameNode}</span><span class="sxs-lookup"><span data-stu-id="9e74c-137">${nameNode}</span></span></td><td><span data-ttu-id="9e74c-138">指定 hello Hadoop 名稱節點 hello URL。</span><span class="sxs-lookup"><span data-stu-id="9e74c-138">Specifies hello URL of hello Hadoop name node.</span></span> <span data-ttu-id="9e74c-139">例如，使用 hello 預設檔案系統位址， <i>wasb: / /&lt;containerName&gt;@&lt;storageAccountName&gt;。 account>.blob.core.windows.net</i>。</span><span class="sxs-lookup"><span data-stu-id="9e74c-139">Use hello default file system address, for example, <i>wasb://&lt;containerName&gt;@&lt;storageAccountName&gt;.blob.core.windows.net</i>.</span></span></td></tr>
<tr><td><span data-ttu-id="9e74c-140">${queueName}</span><span class="sxs-lookup"><span data-stu-id="9e74c-140">${queueName}</span></span></td><td><span data-ttu-id="9e74c-141">指定要送出 hello hello 工作的佇列名稱。</span><span class="sxs-lookup"><span data-stu-id="9e74c-141">Specifies hello queue name that hello job is submitted to.</span></span> <span data-ttu-id="9e74c-142">使用 hello<strong>預設</strong>。</span><span class="sxs-lookup"><span data-stu-id="9e74c-142">Use hello <strong>default</strong>.</span></span></td></tr>
</table>

<table border = "1">
<tr><th><span data-ttu-id="9e74c-143">Hive 動作變數</span><span class="sxs-lookup"><span data-stu-id="9e74c-143">Hive action variable</span></span></th><th><span data-ttu-id="9e74c-144">說明</span><span class="sxs-lookup"><span data-stu-id="9e74c-144">Description</span></span></th></tr>
<tr><td><span data-ttu-id="9e74c-145">${hiveDataFolder}</span><span class="sxs-lookup"><span data-stu-id="9e74c-145">${hiveDataFolder}</span></span></td><td><span data-ttu-id="9e74c-146">指定 hello Hive Create Table 命令的 hello 來源目錄。</span><span class="sxs-lookup"><span data-stu-id="9e74c-146">Specifies hello source directory for hello Hive Create Table command.</span></span></td></tr>
<tr><td><span data-ttu-id="9e74c-147">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="9e74c-147">${hiveOutputFolder}</span></span></td><td><span data-ttu-id="9e74c-148">指定 hello hello 插入覆寫陳述式的輸出資料夾。</span><span class="sxs-lookup"><span data-stu-id="9e74c-148">Specifies hello output folder for hello INSERT OVERWRITE statement.</span></span></td></tr>
<tr><td><span data-ttu-id="9e74c-149">${hiveTableName}</span><span class="sxs-lookup"><span data-stu-id="9e74c-149">${hiveTableName}</span></span></td><td><span data-ttu-id="9e74c-150">指定 hello hello Hive 資料表參考 hello log4j 資料檔案的名稱。</span><span class="sxs-lookup"><span data-stu-id="9e74c-150">Specifies hello name of hello Hive table that references hello log4j data files.</span></span></td></tr>
</table>

<table border = "1">
<tr><th><span data-ttu-id="9e74c-151">Sqoop 動作變數</span><span class="sxs-lookup"><span data-stu-id="9e74c-151">Sqoop action variable</span></span></th><th><span data-ttu-id="9e74c-152">說明</span><span class="sxs-lookup"><span data-stu-id="9e74c-152">Description</span></span></th></tr>
<tr><td><span data-ttu-id="9e74c-153">${sqlDatabaseConnectionString}</span><span class="sxs-lookup"><span data-stu-id="9e74c-153">${sqlDatabaseConnectionString}</span></span></td><td><span data-ttu-id="9e74c-154">指定 hello Azure SQL 資料庫連接字串。</span><span class="sxs-lookup"><span data-stu-id="9e74c-154">Specifies hello Azure SQL database connection string.</span></span></td></tr>
<tr><td><span data-ttu-id="9e74c-155">${sqlDatabaseTableName}</span><span class="sxs-lookup"><span data-stu-id="9e74c-155">${sqlDatabaseTableName}</span></span></td><td><span data-ttu-id="9e74c-156">指定 hello 資料匯出至其中的 hello Azure SQL 資料庫資料表。</span><span class="sxs-lookup"><span data-stu-id="9e74c-156">Specifies hello Azure SQL database table where hello data is exported to.</span></span></td></tr>
<tr><td><span data-ttu-id="9e74c-157">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="9e74c-157">${hiveOutputFolder}</span></span></td><td><span data-ttu-id="9e74c-158">指定 hello hello hive 控制檔插入覆寫陳述式的輸出資料夾。</span><span class="sxs-lookup"><span data-stu-id="9e74c-158">Specifies hello output folder for hello Hive INSERT OVERWRITE statement.</span></span> <span data-ttu-id="9e74c-159">這是 hello hello Sqoop 匯出 (匯出 dir) 相同的資料夾。</span><span class="sxs-lookup"><span data-stu-id="9e74c-159">This is hello same folder for hello Sqoop export (export-dir).</span></span></td></tr>
</table>

<span data-ttu-id="9e74c-160">如需關於 Oozie 工作流程和使用工作流程動作的詳細資訊，請參閱 [Apache Oozie 4.0 文件][apache-oozie-400] (適用於 HDInsight 3.0 版) 或 [Apache Oozie 3.3.2 文件][apache-oozie-332] (適用於 HDInsight 2.1 版)。</span><span class="sxs-lookup"><span data-stu-id="9e74c-160">For more information about Oozie workflow and using workflow actions, see [Apache Oozie 4.0 documentation][apache-oozie-400] (for HDInsight version 3.0) or [Apache Oozie 3.3.2 documentation][apache-oozie-332] (for HDInsight version 2.1).</span></span>

<span data-ttu-id="9e74c-161">hello hello 工作流程中的登錄區動作呼叫下列 HiveQL 指令碼檔案。</span><span class="sxs-lookup"><span data-stu-id="9e74c-161">hello Hive action in hello workflow calls a HiveQL script file.</span></span> <span data-ttu-id="9e74c-162">此指令碼檔案包含三個 HiveQL 陳述式：</span><span class="sxs-lookup"><span data-stu-id="9e74c-162">This script file contains three HiveQL statements:</span></span>

    DROP TABLE ${hiveTableName};
    CREATE EXTERNAL TABLE ${hiveTableName}(t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) ROW FORMAT DELIMITED FIELDS TERMINATED BY ' ' STORED AS TEXTFILE LOCATION '${hiveDataFolder}';
    INSERT OVERWRITE DIRECTORY '${hiveOutputFolder}' SELECT t4 AS sev, COUNT(*) AS cnt FROM ${hiveTableName} WHERE t4 LIKE '[%' GROUP BY t4;

1. <span data-ttu-id="9e74c-163">**DROP TABLE 陳述式 hello**刪除 hello log4j Hive 資料表，如果存在的話。</span><span class="sxs-lookup"><span data-stu-id="9e74c-163">**hello DROP TABLE statement** deletes hello log4j Hive table if it exists.</span></span>
2. <span data-ttu-id="9e74c-164">**hello CREATE TABLE 陳述式**建立 log4j Hive 外部資料表指向 toohello hello log4j 記錄檔的位置。</span><span class="sxs-lookup"><span data-stu-id="9e74c-164">**hello CREATE TABLE statement** creates a log4j Hive external table that points toohello location of hello log4j log file.</span></span> <span data-ttu-id="9e74c-165">hello 欄位分隔符號是"，"。</span><span class="sxs-lookup"><span data-stu-id="9e74c-165">hello field delimiter is ",".</span></span> <span data-ttu-id="9e74c-166">hello 預設列的分隔符號是"\n"。</span><span class="sxs-lookup"><span data-stu-id="9e74c-166">hello default line delimiter is "\n".</span></span> <span data-ttu-id="9e74c-167">Hive 外部資料表是使用的 tooavoid hello 資料檔案，而如果您想要讓 toorun hello Oozie 流程多次正在從 hello 原始位置中移除。</span><span class="sxs-lookup"><span data-stu-id="9e74c-167">A Hive external table is used tooavoid hello data file being removed from hello original location if you want toorun hello Oozie workflow multiple times.</span></span>
3. <span data-ttu-id="9e74c-168">**hello 插入覆寫陳述式**計算 hello 出現 hello log4j Hive 資料表，從每個記錄層級型別，並將 hello 輸出 tooa blob 儲存在 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="9e74c-168">**hello INSERT OVERWRITE statement** counts hello occurrences of each log-level type from hello log4j Hive table, and saves hello output tooa blob in Azure Storage.</span></span>

<span data-ttu-id="9e74c-169">有三個 hello 指令碼中使用的變數：</span><span class="sxs-lookup"><span data-stu-id="9e74c-169">There are three variables used in hello script:</span></span>

* <span data-ttu-id="9e74c-170">${hiveTableName}</span><span class="sxs-lookup"><span data-stu-id="9e74c-170">${hiveTableName}</span></span>
* <span data-ttu-id="9e74c-171">${hiveDataFolder}</span><span class="sxs-lookup"><span data-stu-id="9e74c-171">${hiveDataFolder}</span></span>
* <span data-ttu-id="9e74c-172">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="9e74c-172">${hiveOutputFolder}</span></span>

<span data-ttu-id="9e74c-173">hello 工作流程定義檔 (在本教學課程 workflow.xml) 會傳遞這些值 toothis 下列 HiveQL 指令碼在執行階段。</span><span class="sxs-lookup"><span data-stu-id="9e74c-173">hello workflow definition file (workflow.xml in this tutorial) passes these values toothis HiveQL script at run time.</span></span>

<span data-ttu-id="9e74c-174">Hello 工作流程檔案和 hello HiveQL 檔案會儲存在 blob 容器中。</span><span class="sxs-lookup"><span data-stu-id="9e74c-174">Both hello workflow file and hello HiveQL file are stored in a blob container.</span></span>  <span data-ttu-id="9e74c-175">hello 您稍後在本教學課程中使用的 PowerShell 指令碼將複製這兩個檔案 toohello 預設儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="9e74c-175">hello PowerShell script you use later in this tutorial copies both files toohello default Storage account.</span></span> 

## <a name="submit-oozie-jobs-using-powershell"></a><span data-ttu-id="9e74c-176">使用 PowerShell 提交 Oozie 工作</span><span class="sxs-lookup"><span data-stu-id="9e74c-176">Submit Oozie jobs using PowerShell</span></span>
<span data-ttu-id="9e74c-177">Azure PowerShell 目前並未提供任何用以定義 Oozie 工作的 Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="9e74c-177">Azure PowerShell currently doesn't provide any cmdlets for defining Oozie jobs.</span></span> <span data-ttu-id="9e74c-178">您可以使用 hello **Invoke-restmethod** cmdlet tooinvoke Oozie web 服務。</span><span class="sxs-lookup"><span data-stu-id="9e74c-178">You can use hello **Invoke-RestMethod** cmdlet tooinvoke Oozie web services.</span></span> <span data-ttu-id="9e74c-179">hello Oozie web 服務應用程式開發介面是 HTTP REST JSON API。</span><span class="sxs-lookup"><span data-stu-id="9e74c-179">hello Oozie web services API is a HTTP REST JSON API.</span></span> <span data-ttu-id="9e74c-180">如需 hello Oozie web 服務應用程式開發介面的詳細資訊，請參閱[Apache Oozie 4.0 版文件][ apache-oozie-400] （適用於 HDInsight 3.0 版) 或[Apache Oozie 3.3.2 文件][apache-oozie-332] （適用於 HDInsight 版本 2.1)。</span><span class="sxs-lookup"><span data-stu-id="9e74c-180">For more information about hello Oozie web services API, see [Apache Oozie 4.0 documentation][apache-oozie-400] (for HDInsight version 3.0) or [Apache Oozie 3.3.2 documentation][apache-oozie-332] (for HDInsight version 2.1).</span></span>

<span data-ttu-id="9e74c-181">hello 本節中的 PowerShell 指令碼會執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="9e74c-181">hello PowerShell script in this section performs hello following steps:</span></span>

1. <span data-ttu-id="9e74c-182">連接 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="9e74c-182">Connect tooAzure.</span></span>
2. <span data-ttu-id="9e74c-183">建立 Azure 資源群組。</span><span class="sxs-lookup"><span data-stu-id="9e74c-183">Create an Azure resource group.</span></span> <span data-ttu-id="9e74c-184">如需詳細資訊，請參閱 [將 Azure PowerShell 與 Azure 資源管理員搭配使用](../powershell-azure-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="9e74c-184">For more information, see [Use Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>
3. <span data-ttu-id="9e74c-185">建立 Azure SQL Database 伺服器、Azure SQL Database 和兩個資料表。</span><span class="sxs-lookup"><span data-stu-id="9e74c-185">Create an Azure SQL Database server, an Azure SQL database, and two tables.</span></span> <span data-ttu-id="9e74c-186">Hello Sqoop hello 工作流程中的動作會使用這些名稱。</span><span class="sxs-lookup"><span data-stu-id="9e74c-186">These are used by hello Sqoop action in hello workflow.</span></span>
   
    <span data-ttu-id="9e74c-187">hello 資料表名稱是*log4jLogCount*。</span><span class="sxs-lookup"><span data-stu-id="9e74c-187">hello table name is *log4jLogCount*.</span></span>
4. <span data-ttu-id="9e74c-188">建立 HDInsight 叢集使用 toorun Oozie 作業。</span><span class="sxs-lookup"><span data-stu-id="9e74c-188">Create an HDInsight cluster used toorun Oozie jobs.</span></span>
   
    <span data-ttu-id="9e74c-189">tooexamine hello 叢集中，您可以使用 hello Azure 入口網站或 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="9e74c-189">tooexamine hello cluster, you can use hello Azure portal or Azure PowerShell.</span></span>
5. <span data-ttu-id="9e74c-190">Hello oozie 工作流程檔案和 hello 下列 HiveQL 指令碼檔案 toohello 預設檔案系統複製。</span><span class="sxs-lookup"><span data-stu-id="9e74c-190">Copy hello oozie workflow file and hello HiveQL script file toohello default file system.</span></span>
   
    <span data-ttu-id="9e74c-191">這兩個檔案會儲存在公用 Blob 容器。</span><span class="sxs-lookup"><span data-stu-id="9e74c-191">Both files are stored in a public Blob container.</span></span>
   
   * <span data-ttu-id="9e74c-192">將複製 hello 下列 HiveQL 指令碼 (useoozie.hql) tooAzure 儲存體 (wasb:///tutorials/useoozie/useoozie.hql)。</span><span class="sxs-lookup"><span data-stu-id="9e74c-192">Copy hello HiveQL script (useoozie.hql) tooAzure Storage (wasb:///tutorials/useoozie/useoozie.hql).</span></span>
   * <span data-ttu-id="9e74c-193">將複製 workflow.xml toowasb:///tutorials/useoozie/workflow.xml。</span><span class="sxs-lookup"><span data-stu-id="9e74c-193">Copy workflow.xml toowasb:///tutorials/useoozie/workflow.xml.</span></span>
   * <span data-ttu-id="9e74c-194">複製 hello 資料檔 (/ example/data/sample.log) toowasb:///tutorials/useoozie/data/sample.log。</span><span class="sxs-lookup"><span data-stu-id="9e74c-194">Copy hello data file (/example/data/sample.log) toowasb:///tutorials/useoozie/data/sample.log.</span></span>
6. <span data-ttu-id="9e74c-195">提交 Oozie 工作。</span><span class="sxs-lookup"><span data-stu-id="9e74c-195">Submit an Oozie job.</span></span>
   
    <span data-ttu-id="9e74c-196">tooexamine hello OOzie 作業結果，請使用 Visual Studio 或其他工具 tooconnect toohello Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="9e74c-196">tooexamine hello OOzie job results, use Visual Studio or other tools tooconnect toohello Azure SQL Database.</span></span>

<span data-ttu-id="9e74c-197">以下是 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="9e74c-197">Here is hello script.</span></span>  <span data-ttu-id="9e74c-198">您可以從 Windows PowerShell ISE 中執行 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="9e74c-198">You can run hello script from Windows PowerShell ISE.</span></span> <span data-ttu-id="9e74c-199">您只需要 tooconfigure hello 前 7 的變數。</span><span class="sxs-lookup"><span data-stu-id="9e74c-199">You only need tooconfigure hello first 7 variables.</span></span>

    #region - provide hello following values

    $subscriptionID = "<Enter your Azure subscription ID>"

    # SQL Database server login credentials used for creating and connecting
    $sqlDatabaseLogin = "<Enter SQL Database Login Name>"
    $sqlDatabasePassword = "<Enter SQL Database Login Password>"

    # HDInsight cluster HTTP user credential used for creating and connectin
    $httpUserName = "admin"  # hello default name is "admin"
    $httpPassword = "<Enter HDInsight Cluster HTTP User Password>"

    # Used for creating Azure service names
    $nameToken = "<Enter an Alias>"
    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")
    #endregion

    #region - variables

    # Resource group variables
    $resourceGroupName = $namePrefix + "rg"
    $location = "East US 2" # used by all Azure services defined in this tutorial

    # SQL database varialbes
    $sqlDatabaseServerName = $namePrefix + "sqldbserver"
    $sqlDatabaseName = $namePrefix + "sqldb"
    $sqlDatabaseConnectionString = "Data Source=$sqlDatabaseServerName.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabasePassword;Encrypt=true;Trusted_Connection=false;"
    $sqlDatabaseMaxSizeGB = 10

    # Used for retrieving external IP address and creating firewall rules
    $ipAddressRestService = "http://bot.whatismyipaddress.com"
    $fireWallRuleName = "UseSqoop"

    # HDInsight variables
    $hdinsightClusterName = $namePrefix + "hdi"
    $defaultStorageAccountName = $namePrefix + "store"
    $defaultBlobContainerName = $hdinsightClusterName
    #endregion

    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    #region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{
        Login-AzureRmAccount
        Select-AzureRmSubscription -SubscriptionId $subscriptionID
    }
    #endregion

    #region - Create Azure resouce group
    Write-Host "`nCreating an Azure resource group ..." -ForegroundColor Green
    try{
        Get-AzureRmResourceGroup -Name $resourceGroupName
    }
    catch{
        New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
    }
    #endregion

    #region - Create Azure SQL database server
    Write-Host "`nCreating an Azure SQL Database server ..." -ForegroundColor Green
    try{
        Get-AzureRmSqlServer -ServerName $sqlDatabaseServerName -ResourceGroupName $resourceGroupName}
    catch{
        Write-Host "`nCreating SQL Database server ..."  -ForegroundColor Green

        $sqlDatabasePW = ConvertTo-SecureString -String $sqlDatabasePassword -AsPlainText -Force
        $sqlLoginCredentials = New-Object System.Management.Automation.PSCredential($sqlDatabaseLogin,$sqlDatabasePW)

        $sqlDatabaseServerName = (New-AzureRmSqlServer `
                                    -ResourceGroupName $resourceGroupName `
                                    -ServerName $sqlDatabaseServerName `
                                    -SqlAdministratorCredentials $sqlLoginCredentials `
                                    -Location $location).ServerName
        Write-Host "`tThe new SQL database server name is $sqlDatabaseServerName." -ForegroundColor Cyan

        Write-Host "`nCreating firewall rule, $fireWallRuleName ..." -ForegroundColor Green
        $workstationIPAddress = Invoke-RestMethod $ipAddressRestService
        New-AzureRmSqlServerFirewallRule `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -FirewallRuleName "$fireWallRuleName-workstation" `
            -StartIpAddress $workstationIPAddress `
            -EndIpAddress $workstationIPAddress

        #tooallow other Azure services tooaccess hello server add a firewall rule and set both hello StartIpAddress and EndIpAddress too0.0.0.0. 
        #Note that this allows Azure traffic from any Azure subscription tooaccess hello server.
        New-AzureRmSqlServerFirewallRule `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -FirewallRuleName "$fireWallRuleName-Azureservices" `
            -StartIpAddress "0.0.0.0" `
            -EndIpAddress "0.0.0.0"
    }
    #endregion

    #region - Create and validate Azure SQL database
    Write-Host "`nCreating SQL Database, $sqlDatabaseName ..."  -ForegroundColor Green

    try {
        Get-AzureRmSqlDatabase `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -DatabaseName $sqlDatabaseName
    }
    catch {
        New-AzureRMSqlDatabase `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -DatabaseName $sqlDatabaseName `
            -Edition "Standard" `
            -RequestedServiceObjectiveName "S1"
    }
    #endregion

    #region - Create SQL database tables
    Write-Host "Creating hello log4jlogs table  ..." -ForegroundColor Green

    $sqlDatabaseTableName = "log4jLogsCount"
    $cmdCreateLog4jCountTable = " CREATE TABLE [dbo].[$sqlDatabaseTableName](
            [Level] [nvarchar](10) NOT NULL,
            [Total] float,
        CONSTRAINT [PK_$sqlDatabaseTableName] PRIMARY KEY CLUSTERED
        (
        [Level] ASC
        )
        )"

    $conn = New-Object System.Data.SqlClient.SqlConnection
    $conn.ConnectionString = $sqlDatabaseConnectionString
    $conn.Open()

    # Create hello log4jlogs table and index
    $cmd = New-Object System.Data.SqlClient.SqlCommand
    $cmd.Connection = $conn
    $cmd.CommandText = $cmdCreateLog4jCountTable
    $cmd.ExecuteNonQuery()

    $conn.close()
    #endregion

    #region - Create HDInsight cluster

    Write-Host "Creating hello HDInsight cluster and hello dependent services ..." -ForegroundColor Green

    # Create hello default storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $defaultStorageAccountName `
        -Location $location `
        -Type Standard_LRS

    # Create hello default Blob container
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                    -ResourceGroupName $resourceGroupName `
                                    -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext `
                                        -StorageAccountName $defaultStorageAccountName `
                                        -StorageAccountKey $defaultStorageAccountKey 
    New-AzureStorageContainer `
        -Name $defaultBlobContainerName `
        -Context $defaultStorageAccountContext 

    # Create hello HDInsight cluster
    $pw = ConvertTo-SecureString -String $httpPassword -AsPlainText -Force
    $httpCredential = New-Object System.Management.Automation.PSCredential($httpUserName,$pw)

    New-AzureRmHDInsightCluster `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $HDInsightClusterName `
        -Location $location `
        -ClusterType Hadoop `
        -OSType Windows `
        -ClusterSizeInNodes 2 `
        -HttpCredential $httpCredential `
        -DefaultStorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultStorageContainer $defaultBlobContainerName 

    # Validate hello cluster
    Get-AzureRmHDInsightCluster -ClusterName $hdinsightClusterName
    #endregion

    #region - copy Oozie workflow and HiveQL files

    Write-Host "Copy workflow definition and HiveQL script file ..." -ForegroundColor Green

    # Both files are stored in a public Blob
    $publicBlobContext = New-AzureStorageContext -StorageAccountName "hditutorialdata" -Anonymous

    # WASB folder for storing hello Oozie tutorial files.
    $destFolder = "tutorials/useoozie"  # Do NOT use hello long path here

    Start-CopyAzureStorageBlob `
        -Context $publicBlobContext `
        -SrcContainer "useoozie" `
        -SrcBlob "useooziewf.hql"  `
        -DestContext $defaultStorageAccountContext `
        -DestContainer $defaultBlobContainerName `
        -DestBlob "$destFolder/useooziewf.hql" `
        -Force

    Start-CopyAzureStorageBlob `
        -Context $publicBlobContext `
        -SrcContainer "useoozie" `
        -SrcBlob "workflow.xml"  `
        -DestContext $defaultStorageAccountContext `
        -DestContainer $defaultBlobContainerName `
        -DestBlob "$destFolder/workflow.xml" `
        -Force

    #validate hello copy
    Get-AzureStorageBlob `
        -Context $defaultStorageAccountContext `
        -Container $defaultBlobContainerName `
        -Blob $destFolder/workflow.xml

    Get-AzureStorageBlob `
        -Context $defaultStorageAccountContext `
        -Container $defaultBlobContainerName `
        -Blob $destFolder/useooziewf.hql

    #endregion

    #region - copy hello sample.log file

    Write-Host "Make a copy of hello sample.log file ... " -ForegroundColor Green

    Start-CopyAzureStorageBlob `
        -Context $defaultStorageAccountContext `
        -SrcContainer $defaultBlobContainerName `
        -SrcBlob "example/data/sample.log"  `
        -DestContext $defaultStorageAccountContext `
        -DestContainer $defaultBlobContainerName `
        -destBlob "$destFolder/data/sample.log" 

    #validate hello copy
    Get-AzureStorageBlob `
        -Context $defaultStorageAccountContext `
        -Container $defaultBlobContainerName `
        -Blob $destFolder/data/sample.log

    #endregion

    #region - submit Oozie job

    $storageUri="wasb://$defaultBlobContainerName@$defaultStorageAccountName.blob.core.windows.net"

    $oozieJobName = $namePrefix + "OozieJob"

    #Oozie WF variables
    $oozieWFPath="$storageUri/tutorials/useoozie"  # hello default name is workflow.xml. And you don't need toospecify hello file name.
    $waitTimeBetweenOozieJobStatusCheck=10

    #Hive action variables
    $hiveScript = "$storageUri/tutorials/useoozie/useooziewf.hql"
    $hiveTableName = "log4jlogs"
    $hiveDataFolder = "$storageUri/tutorials/useoozie/data"
    $hiveOutputFolder = "$storageUri/tutorials/useoozie/output"

    #Sqoop action variables
    $sqlDatabaseConnectionString = "jdbc:sqlserver://$sqlDatabaseServerName.database.windows.net;user=$sqlDatabaseLogin@$sqlDatabaseServerName;password=$sqlDatabasePassword;database=$sqlDatabaseName"

    $OoziePayload =  @"
    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>

    <property>
        <name>nameNode</name>
        <value>$storageUrI</value>
    </property>

    <property>
        <name>jobTracker</name>
        <value>jobtrackerhost:9010</value>
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
        <value>$hiveScript</value>
    </property>

    <property>
        <name>hiveTableName</name>
        <value>$hiveTableName</value>
    </property>

    <property>
        <name>hiveDataFolder</name>
        <value>$hiveDataFolder</value>
    </property>

    <property>
        <name>hiveOutputFolder</name>
        <value>$hiveOutputFolder</value>
    </property>

    <property>
        <name>sqlDatabaseConnectionString</name>
        <value>&quot;$sqlDatabaseConnectionString&quot;</value>
    </property>

    <property>
        <name>sqlDatabaseTableName</name>
        <value>$SQLDatabaseTableName</value>
    </property>

    <property>
        <name>user.name</name>
        <value>$httpUserName</value>
    </property>

    <property>
        <name>oozie.wf.application.path</name>
        <value>$oozieWFPath</value>
    </property>

    </configuration>
    "@

    Write-Host "Checking Oozie server status..." -ForegroundColor Green
    $clusterUriStatus = "https://$hdinsightClusterName.azurehdinsight.net:443/oozie/v2/admin/status"
    $response = Invoke-RestMethod -Method Get -Uri $clusterUriStatus -Credential $httpCredential -OutVariable $OozieServerStatus

    $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
    $oozieServerSatus = $jsonResponse[0].("systemMode")
    Write-Host "Oozie server status is $oozieServerSatus."

    # create Oozie job
    Write-Host "Sending hello following Payload toohello cluster:" -ForegroundColor Green
    Write-Host "`n--------`n$OoziePayload`n--------"
    $clusterUriCreateJob = "https://$hdinsightClusterName.azurehdinsight.net:443/oozie/v2/jobs"
    $response = Invoke-RestMethod -Method Post -Uri $clusterUriCreateJob -Credential $httpCredential -Body $OoziePayload -ContentType "application/xml" -OutVariable $OozieJobName #-debug

    $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
    $oozieJobId = $jsonResponse[0].("id")
    Write-Host "Oozie job id is $oozieJobId..."

    # start Oozie job
    Write-Host "Starting hello Oozie job $oozieJobId..." -ForegroundColor Green
    $clusterUriStartJob = "https://$hdinsightClusterName.azurehdinsight.net:443/oozie/v2/job/" + $oozieJobId + "?action=start"
    $response = Invoke-RestMethod -Method Put -Uri $clusterUriStartJob -Credential $httpCredential | Format-Table -HideTableHeaders #-debug

    # get job status
    Write-Host "Sleeping for $waitTimeBetweenOozieJobStatusCheck seconds until hello job metadata is populated in hello Oozie metastore..." -ForegroundColor Green
    Start-Sleep -Seconds $waitTimeBetweenOozieJobStatusCheck

    Write-Host "Getting job status and waiting for hello job toocomplete..." -ForegroundColor Green
    $clusterUriGetJobStatus = "https://$hdinsightClusterName.azurehdinsight.net:443/oozie/v2/job/" + $oozieJobId + "?show=info"
    $response = Invoke-RestMethod -Method Get -Uri $clusterUriGetJobStatus -Credential $httpCredential
    $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
    $JobStatus = $jsonResponse[0].("status")

    while($JobStatus -notmatch "SUCCEEDED|KILLED")
    {
        Write-Host "$(Get-Date -format 'G'): $oozieJobId is in $JobStatus state...waiting $waitTimeBetweenOozieJobStatusCheck seconds for hello job toocomplete..."
        Start-Sleep -Seconds $waitTimeBetweenOozieJobStatusCheck
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriGetJobStatus -Credential $httpCredential
        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $JobStatus = $jsonResponse[0].("status")
        $jobStatus
    }

    Write-Host "$(Get-Date -format 'G'): $oozieJobId is in $JobStatus state!" -ForegroundColor Green

    #endregion


<span data-ttu-id="9e74c-200">**toore 執行 hello 教學課程**</span><span class="sxs-lookup"><span data-stu-id="9e74c-200">**toore-run hello tutorial**</span></span>

<span data-ttu-id="9e74c-201">hello toore 執行工作流程，您必須刪除下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="9e74c-201">toore-run hello workflow, you must delete hello following items:</span></span>

* <span data-ttu-id="9e74c-202">hello Hive 指令碼輸出檔</span><span class="sxs-lookup"><span data-stu-id="9e74c-202">hello Hive script output file</span></span>
* <span data-ttu-id="9e74c-203">hello log4jLogsCount 資料表中的 hello 資料</span><span class="sxs-lookup"><span data-stu-id="9e74c-203">hello data in hello log4jLogsCount table</span></span>

<span data-ttu-id="9e74c-204">以下提供可供使用的範例 PowerShell 指令碼：</span><span class="sxs-lookup"><span data-stu-id="9e74c-204">Here is a sample PowerShell script that you can use:</span></span>

    $resourceGroupName = "<AzureResourceGroupName>"

    $defaultStorageAccountName = "<AzureStorageAccountName>"
    $defaultBlobContainerName = "<ContainerName>"

    #SQL database variables
    $sqlDatabaseServerName = "<SQLDatabaseServerName>"
    $sqlDatabaseLogin = "<SQLDatabaseLoginName>"
    $sqlDatabasePassword = "<SQLDatabaseLoginPassword>"
    $sqlDatabaseName = "<SQLDatabaseName>"
    $sqlDatabaseTableName = "log4jLogsCount"

    Write-host "Delete hello Hive script output file ..." -ForegroundColor Green
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                -ResourceGroupName $resourceGroupName `
                                -Name $defaultStorageAccountName)[0].Value
    $destContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey
    Remove-AzureStorageBlob -Context $destContext -Blob "tutorials/useoozie/output/000000_0" -Container $defaultBlobContainerName

    Write-host "Delete all hello records from hello log4jLogsCount table ..." -ForegroundColor Green
    $conn = New-Object System.Data.SqlClient.SqlConnection
    $conn.ConnectionString = "Data Source=$sqlDatabaseServerName.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabasePassword;Encrypt=true;Trusted_Connection=false;"
    $conn.open()
    $cmd = New-Object System.Data.SqlClient.SqlCommand
    $cmd.connection = $conn
    $cmd.commandtext = "delete from $sqlDatabaseTableName"
    $cmd.executenonquery()

    $conn.close()

## <a name="next-steps"></a><span data-ttu-id="9e74c-205">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9e74c-205">Next steps</span></span>
<span data-ttu-id="9e74c-206">在本教學課程中，您學到如何 toodefine Oozie 工作流程和 toorun Oozie 使用 PowerShell 的工作。</span><span class="sxs-lookup"><span data-stu-id="9e74c-206">In this tutorial, you learned how toodefine an Oozie workflow and how toorun an Oozie job by using PowerShell.</span></span> <span data-ttu-id="9e74c-207">toolearn 詳細資訊，請參閱下列文章 hello:</span><span class="sxs-lookup"><span data-stu-id="9e74c-207">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="9e74c-208">[搭配 HDInsight 使用以時間為基礎的 Hadoop Oozie 協調器][hdinsight-oozie-coordinator-time]</span><span class="sxs-lookup"><span data-stu-id="9e74c-208">[Use time-based Oozie Coordinator with HDInsight][hdinsight-oozie-coordinator-time]</span></span>
* <span data-ttu-id="9e74c-209">[開始使用登錄區中的 Hadoop，HDInsight tooanalyze 行動話筒使用中][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="9e74c-209">[Get started using Hadoop with Hive in HDInsight tooanalyze mobile handset use][hdinsight-get-started]</span></span>
* <span data-ttu-id="9e74c-210">[搭配 HDInsight 使用 Azure Blob 儲存體][hdinsight-storage]</span><span class="sxs-lookup"><span data-stu-id="9e74c-210">[Use Azure Blob storage with HDInsight][hdinsight-storage]</span></span>
* <span data-ttu-id="9e74c-211">[使用 PowerShell 管理 HDInsight][hdinsight-admin-powershell]</span><span class="sxs-lookup"><span data-stu-id="9e74c-211">[Administer HDInsight using PowerShell][hdinsight-admin-powershell]</span></span>
* <span data-ttu-id="9e74c-212">[在 HDInsight 中上傳 Hadoop 作業的資料][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="9e74c-212">[Upload data for Hadoop jobs in HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="9e74c-213">[搭配使用 Sqoop 與 HDInsight 中的 Hadoop][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="9e74c-213">[Use Sqoop with Hadoop in HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="9e74c-214">[搭配使用 Hive 與 HDInsight 上的 Hadoop][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="9e74c-214">[Use Hive with Hadoop on HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="9e74c-215">[搭配使用 Pig 與 HDInsight 上的 Hadoop][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="9e74c-215">[Use Pig with Hadoop on HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="9e74c-216">[開發 HDInsight 的 Java MapReduce 程式][hdinsight-develop-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="9e74c-216">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-mapreduce]</span></span>

[hdinsight-cmdlets-download]: http://go.microsoft.com/fwlink/?LinkID=325563



[azure-data-factory-pig-hive]: ../data-factory/data-factory-data-transformation-activities.md
[hdinsight-oozie-coordinator-time]: hdinsight-use-oozie-coordinator-time.md
[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md


[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-develop-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md

[sqldatabase-create-configue]: ../sql-database-create-configure.md
[sqldatabase-get-started]: ../sql-database-get-started.md

[azure-management-portal]: https://portal.azure.com/
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
