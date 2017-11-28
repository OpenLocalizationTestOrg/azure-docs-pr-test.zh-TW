---
title: "aaaUse HDInsight 中的，以時間為基礎 Hadoop Oozie coordinator |Microsoft 文件"
description: "在 HDInsight 上使用以時間為基礎的 Hadoop Oozie 協調器：一項巨量資料服務。 深入了解如何 toodefine Oozie 工作流程和協調，並提交工作。"
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 00c3a395-d51a-44ff-af2d-1f116c4b1c83
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: aecbb5ee94a4234d1a7768bdb6de2a33508b1e4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-time-based-oozie-coordinator-with-hadoop-in-hdinsight-toodefine-workflows-and-coordinate-jobs"></a><span data-ttu-id="961d5-104">以時間為基礎的 Oozie 協調器使用 HDInsight toodefine 工作流程中的 Hadoop 和協調工作</span><span class="sxs-lookup"><span data-stu-id="961d5-104">Use time-based Oozie coordinator with Hadoop in HDInsight toodefine workflows and coordinate jobs</span></span>
<span data-ttu-id="961d5-105">在本文中，您將學習如何 toodefine 工作流程及協調員，和如何 tootrigger hello 協調器工作，根據時間。</span><span class="sxs-lookup"><span data-stu-id="961d5-105">In this article, you'll learn how toodefine workflows and coordinators, and how tootrigger hello coordinator jobs, based on time.</span></span> <span data-ttu-id="961d5-106">它是透過有幫助 toogo[與 HDInsight 的使用 Oozie] [ hdinsight-use-oozie]閱讀本文之前。</span><span class="sxs-lookup"><span data-stu-id="961d5-106">It is helpful toogo through [Use Oozie with HDInsight][hdinsight-use-oozie] before you read this article.</span></span> <span data-ttu-id="961d5-107">此外 tooOozie，您也可以排定工作，使用 Azure Data Factory。</span><span class="sxs-lookup"><span data-stu-id="961d5-107">In addition tooOozie, you can also schedule jobs using Azure Data Factory.</span></span> <span data-ttu-id="961d5-108">toolearn Azure Data Factory，請參閱[搭配使用 Pig 和 Hive 與 Data Factory](../data-factory/data-factory-data-transformation-activities.md)。</span><span class="sxs-lookup"><span data-stu-id="961d5-108">toolearn Azure Data Factory, see [Use Pig and Hive with Data Factory](../data-factory/data-factory-data-transformation-activities.md).</span></span>

> [!NOTE]
> <span data-ttu-id="961d5-109">本文章需有以 Windows 為基礎的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="961d5-109">This article requires a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="961d5-110">如需使用 Oozie，包括以時間為基礎的工作，在以 Linux 為基礎的叢集上，請參閱[Hadoop toodefine 與執行工作流程以 Linux 為基礎的 HDInsight 上使用 Oozie](hdinsight-use-oozie-linux-mac.md)</span><span class="sxs-lookup"><span data-stu-id="961d5-110">For information on using Oozie, including time-based jobs, on a Linux-based cluster, see [Use Oozie with Hadoop toodefine and run a workflow on Linux-based HDInsight](hdinsight-use-oozie-linux-mac.md)</span></span>

## <a name="what-is-oozie"></a><span data-ttu-id="961d5-111">什麼是 Oozie</span><span class="sxs-lookup"><span data-stu-id="961d5-111">What is Oozie</span></span>
<span data-ttu-id="961d5-112">Apache Oozie 是可管理 Hadoop 工作的工作流程/協調系統。</span><span class="sxs-lookup"><span data-stu-id="961d5-112">Apache Oozie is a workflow/coordination system that manages Hadoop jobs.</span></span> <span data-ttu-id="961d5-113">Hello Hadoop 堆疊，與整合，並支援 Apache MapReduce、 Apache Pig、 Apache Hive，和 Apache Sqoop Hadoop 工作。</span><span class="sxs-lookup"><span data-stu-id="961d5-113">It is integrated with hello Hadoop stack, and it supports Hadoop jobs for Apache MapReduce, Apache Pig, Apache Hive, and Apache Sqoop.</span></span> <span data-ttu-id="961d5-114">它也可以使用的 tooschedule 作業的特定 tooa 系統，例如 Java 程式或殼層指令碼。</span><span class="sxs-lookup"><span data-stu-id="961d5-114">It can also be used tooschedule jobs that are specific tooa system, such as Java programs or shell scripts.</span></span>

<span data-ttu-id="961d5-115">hello 下列影像顯示 hello 工作流程將實作：</span><span class="sxs-lookup"><span data-stu-id="961d5-115">hello following image shows hello workflow you will implement:</span></span>

![Workflow diagram][img-workflow-diagram]

<span data-ttu-id="961d5-117">hello 工作流程包含兩個動作：</span><span class="sxs-lookup"><span data-stu-id="961d5-117">hello workflow contains two actions:</span></span>

1. <span data-ttu-id="961d5-118">登錄區動作會執行下列 HiveQL 指令碼 toocount hello 每個記錄層級類型的發生 log4j 記錄檔中。</span><span class="sxs-lookup"><span data-stu-id="961d5-118">A Hive action runs a HiveQL script toocount hello occurrences of each log-level type in a log4j log file.</span></span> <span data-ttu-id="961d5-119">每個 log4j 記錄檔所組成，其中包含 [記錄層級] 欄位 tooshow hello 類型和 hello 嚴重性，例如欄位一行：</span><span class="sxs-lookup"><span data-stu-id="961d5-119">Each log4j log consists of a line of fields that contains a [LOG LEVEL] field tooshow hello type and hello severity, for example:</span></span>

        2012-02-03 18:35:34 SampleClass6 [INFO] everything normal for id 577725851
        2012-02-03 18:35:34 SampleClass4 [FATAL] system problem at id 1991281254
        2012-02-03 18:35:34 SampleClass3 [DEBUG] detail for id 1304807656
        ...

    <span data-ttu-id="961d5-120">hello Hive 指令碼輸出如下：</span><span class="sxs-lookup"><span data-stu-id="961d5-120">hello Hive script output is similar to:</span></span>

        [DEBUG] 434
        [ERROR] 3
        [FATAL] 1
        [INFO]  96
        [TRACE] 816
        [WARN]  4

    <span data-ttu-id="961d5-121">如需 Hive 的詳細資訊，請參閱[在 HDInsight 上使用 Hive][hdinsight-use-hive]。</span><span class="sxs-lookup"><span data-stu-id="961d5-121">For more information about Hive, see [Use Hive with HDInsight][hdinsight-use-hive].</span></span>
2. <span data-ttu-id="961d5-122">Sqoop 動作匯出 hello HiveQL 動作輸出 tooa 資料表在 Azure SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="961d5-122">A Sqoop action exports hello HiveQL action output tooa table in an Azure SQL database.</span></span> <span data-ttu-id="961d5-123">如需 Sqoop 的詳細資訊，請參閱[搭配 HDInsight 使用 Sqoop][hdinsight-use-sqoop]。</span><span class="sxs-lookup"><span data-stu-id="961d5-123">For more information about Sqoop, see [Use Sqoop with HDInsight][hdinsight-use-sqoop].</span></span>

> [!NOTE]
> <span data-ttu-id="961d5-124">HDInsight 叢集上支援 Oozie 版本，請參閱[HDInsight 所提供的 hello 叢集版本中最新消息？][hdinsight-versions].</span><span class="sxs-lookup"><span data-stu-id="961d5-124">For supported Oozie versions on HDInsight clusters, see [What's new in hello cluster versions provided by HDInsight?][hdinsight-versions].</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="961d5-125">必要條件</span><span class="sxs-lookup"><span data-stu-id="961d5-125">Prerequisites</span></span>
<span data-ttu-id="961d5-126">開始本教學課程之前，您必須擁有 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="961d5-126">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="961d5-127">**具有 Azure PowerShell 的工作站**。</span><span class="sxs-lookup"><span data-stu-id="961d5-127">**A workstation with Azure PowerShell**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="961d5-128">使用 Azure Service Manager 管理 HDInsight 資源的 Azure PowerShell 支援已**被取代**，將會在 2017 年 1 月 1 日前移除。</span><span class="sxs-lookup"><span data-stu-id="961d5-128">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and will be removed by January 1, 2017.</span></span> <span data-ttu-id="961d5-129">此文件使用 hello 新 HDInsight 的 cmdlet 可與 Azure 資源管理員中的步驟 hello。</span><span class="sxs-lookup"><span data-stu-id="961d5-129">hello steps in this document use hello new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="961d5-130">請依照中的 hello 步驟[安裝和設定 Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello 最新版的 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="961d5-130">Please follow hello steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="961d5-131">如果您有指令碼的需要 toobe 修改 toouse hello 新的 cmdlet 可與 Azure 資源管理員，請參閱[移轉 tooAzure 資源管理員為基礎的開發工具的 HDInsight 叢集](hdinsight-hadoop-development-using-azure-resource-manager.md)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="961d5-131">If you have scripts that need toobe modified toouse hello new cmdlets that work with Azure Resource Manager, see [Migrating tooAzure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

* <span data-ttu-id="961d5-132">**HDInsight 叢集**。</span><span class="sxs-lookup"><span data-stu-id="961d5-132">**An HDInsight cluster**.</span></span> <span data-ttu-id="961d5-133">如需關於建立 HDInsight 叢集的詳細資訊，請參閱[建立 HDInsight 叢集][hdinsight-provision]或[開始使用 HDInsight][hdinsight-get-started]。</span><span class="sxs-lookup"><span data-stu-id="961d5-133">For information about creating an HDInsight cluster, see [Create HDInsight clusters][hdinsight-provision], or [Get started with HDInsight][hdinsight-get-started].</span></span> <span data-ttu-id="961d5-134">您需要下列資料 toogo hello 教學課程的 hello:</span><span class="sxs-lookup"><span data-stu-id="961d5-134">You will need hello following data toogo through hello tutorial:</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="961d5-135">叢集屬性</span><span class="sxs-lookup"><span data-stu-id="961d5-135">Cluster property</span></span></th><th><span data-ttu-id="961d5-136">Windows PowerShell 變數名稱</span><span class="sxs-lookup"><span data-stu-id="961d5-136">Windows PowerShell variable name</span></span></th><th><span data-ttu-id="961d5-137">值</span><span class="sxs-lookup"><span data-stu-id="961d5-137">Value</span></span></th><th><span data-ttu-id="961d5-138">說明</span><span class="sxs-lookup"><span data-stu-id="961d5-138">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="961d5-139">HDInsight 叢集名稱</span><span class="sxs-lookup"><span data-stu-id="961d5-139">HDInsight cluster name</span></span></td><td><span data-ttu-id="961d5-140">$clusterName</span><span class="sxs-lookup"><span data-stu-id="961d5-140">$clusterName</span></span></td><td></td><td><span data-ttu-id="961d5-141">您會在其執行本教學課程中的 hello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="961d5-141">hello HDInsight cluster on which you will run this tutorial.</span></span></td></tr>
    <tr><td><span data-ttu-id="961d5-142">HDInsight 叢集使用者名稱</span><span class="sxs-lookup"><span data-stu-id="961d5-142">HDInsight cluster username</span></span></td><td><span data-ttu-id="961d5-143">$clusterUsername</span><span class="sxs-lookup"><span data-stu-id="961d5-143">$clusterUsername</span></span></td><td></td><td><span data-ttu-id="961d5-144">hello HDInsight 叢集使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="961d5-144">hello HDInsight cluster user name.</span></span> </td></tr>
    <tr><td><span data-ttu-id="961d5-145">HDInsight 叢集使用者的密碼</span><span class="sxs-lookup"><span data-stu-id="961d5-145">HDInsight cluster user password</span></span> </td><td><span data-ttu-id="961d5-146">$clusterPassword</span><span class="sxs-lookup"><span data-stu-id="961d5-146">$clusterPassword</span></span></td><td></td><td><span data-ttu-id="961d5-147">hello HDInsight 叢集的使用者密碼。</span><span class="sxs-lookup"><span data-stu-id="961d5-147">hello HDInsight cluster user password.</span></span></td></tr>
    <tr><td><span data-ttu-id="961d5-148">Azure 儲存體帳戶名稱</span><span class="sxs-lookup"><span data-stu-id="961d5-148">Azure storage account name</span></span></td><td><span data-ttu-id="961d5-149">$storageAccountName</span><span class="sxs-lookup"><span data-stu-id="961d5-149">$storageAccountName</span></span></td><td></td><td><span data-ttu-id="961d5-150">Azure 儲存體帳戶可用 toohello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="961d5-150">An Azure Storage account available toohello HDInsight cluster.</span></span> <span data-ttu-id="961d5-151">此教學課程中，使用 hello hello 叢集佈建程序期間所指定預設儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="961d5-151">For this tutorial, use hello default storage account that you specified during hello cluster provision process.</span></span></td></tr>
    <tr><td><span data-ttu-id="961d5-152">Azure Blob 容器名稱</span><span class="sxs-lookup"><span data-stu-id="961d5-152">Azure Blob container name</span></span></td><td><span data-ttu-id="961d5-153">$containerName</span><span class="sxs-lookup"><span data-stu-id="961d5-153">$containerName</span></span></td><td></td><td><span data-ttu-id="961d5-154">此範例中，使用適用於 hello 預設 HDInsight 叢集檔案系統的 hello Azure Blob 儲存體容器。</span><span class="sxs-lookup"><span data-stu-id="961d5-154">For this example, use hello Azure Blob storage container that is used for hello default HDInsight cluster file system.</span></span> <span data-ttu-id="961d5-155">根據預設，它有名稱為 hello HDInsight 叢集相同的 hello。</span><span class="sxs-lookup"><span data-stu-id="961d5-155">By default, it has hello same name as hello HDInsight cluster.</span></span></td></tr>
    </table><span data-ttu-id="961d5-156">
* **Azure SQL Database**。</span><span class="sxs-lookup"><span data-stu-id="961d5-156">
* **An Azure SQL database**.</span></span> <span data-ttu-id="961d5-157">您必須從您的工作站設定 hello SQL Database 伺服器 tooallow 存取的防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="961d5-157">You must configure a firewall rule for hello SQL Database server tooallow access from your workstation.</span></span> <span data-ttu-id="961d5-158">如需有關建立 Azure SQL database 和 hello 防火牆設定的指示，請參閱 [開始使用 Azure SQL database] [sql database-get-已啟動]。</span><span class="sxs-lookup"><span data-stu-id="961d5-158">For instructions about creating an Azure SQL database and configuring hello firewall, see [Get started using Azure SQL database][sqldatabase-get-started].</span></span> <span data-ttu-id="961d5-159">本文章提供 Windows PowerShell 指令碼來建立您需要在此教學課程的 hello Azure SQL 資料庫資料表。</span><span class="sxs-lookup"><span data-stu-id="961d5-159">This article provides a Windows PowerShell script for creating hello Azure SQL database table that you need for this tutorial.</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="961d5-160">SQL Database 屬性</span><span class="sxs-lookup"><span data-stu-id="961d5-160">SQL database property</span></span></th><th><span data-ttu-id="961d5-161">Windows PowerShell 變數名稱</span><span class="sxs-lookup"><span data-stu-id="961d5-161">Windows PowerShell variable name</span></span></th><th><span data-ttu-id="961d5-162">值</span><span class="sxs-lookup"><span data-stu-id="961d5-162">Value</span></span></th><th><span data-ttu-id="961d5-163">說明</span><span class="sxs-lookup"><span data-stu-id="961d5-163">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="961d5-164">SQL Database 伺服器名稱</span><span class="sxs-lookup"><span data-stu-id="961d5-164">SQL database server name</span></span></td><td><span data-ttu-id="961d5-165">$sqlDatabaseServer</span><span class="sxs-lookup"><span data-stu-id="961d5-165">$sqlDatabaseServer</span></span></td><td></td><td><span data-ttu-id="961d5-166">hello SQL 資料庫伺服器 toowhich Sqoop 會將資料匯出。</span><span class="sxs-lookup"><span data-stu-id="961d5-166">hello SQL database server toowhich Sqoop will export data.</span></span> </td></tr>
    <tr><td><span data-ttu-id="961d5-167">SQL Database 登入名稱</span><span class="sxs-lookup"><span data-stu-id="961d5-167">SQL database login name</span></span></td><td><span data-ttu-id="961d5-168">$sqlDatabaseLogin</span><span class="sxs-lookup"><span data-stu-id="961d5-168">$sqlDatabaseLogin</span></span></td><td></td><td><span data-ttu-id="961d5-169">SQL Database 登入名稱。</span><span class="sxs-lookup"><span data-stu-id="961d5-169">SQL Database login name.</span></span></td></tr>
    <tr><td><span data-ttu-id="961d5-170">SQL Database 登入密碼</span><span class="sxs-lookup"><span data-stu-id="961d5-170">SQL database login password</span></span></td><td><span data-ttu-id="961d5-171">$sqlDatabaseLoginPassword</span><span class="sxs-lookup"><span data-stu-id="961d5-171">$sqlDatabaseLoginPassword</span></span></td><td></td><td><span data-ttu-id="961d5-172">SQL Database 登入密碼。</span><span class="sxs-lookup"><span data-stu-id="961d5-172">SQL Database login password.</span></span></td></tr>
    <tr><td><span data-ttu-id="961d5-173">SQL Database 名稱</span><span class="sxs-lookup"><span data-stu-id="961d5-173">SQL database name</span></span></td><td><span data-ttu-id="961d5-174">$sqlDatabaseName</span><span class="sxs-lookup"><span data-stu-id="961d5-174">$sqlDatabaseName</span></span></td><td></td><td><span data-ttu-id="961d5-175">hello Azure SQL database toowhich Sqoop 會將資料匯出。</span><span class="sxs-lookup"><span data-stu-id="961d5-175">hello Azure SQL database toowhich Sqoop will export data.</span></span> </td></tr>
    </table>

  > [!NOTE]
  > <span data-ttu-id="961d5-176">根據預設，Azure SQL Database 接受來自 Azure 服務 (例如 Azure HDInsight) 的連線。</span><span class="sxs-lookup"><span data-stu-id="961d5-176">By default an Azure SQL database allows connections from Azure Services, such as Azure HDInsight.</span></span> <span data-ttu-id="961d5-177">如果防火牆已停用此設定，您必須從 hello Azure 入口網站來啟用它。</span><span class="sxs-lookup"><span data-stu-id="961d5-177">If this firewall setting is disabled, you must enable it from hello Azure Portal.</span></span> <span data-ttu-id="961d5-178">如需關於建立 SQL Database 和設定防火牆規則的指示，請參閱[建立和設定 SQL Database][sqldatabase-get-started]。</span><span class="sxs-lookup"><span data-stu-id="961d5-178">For instruction about creating a SQL Database and configuring firewall rules, see [Create and Configure SQL Database][sqldatabase-get-started].</span></span>

> [!NOTE]
> <span data-ttu-id="961d5-179">填入 hello hello 資料表中的值。</span><span class="sxs-lookup"><span data-stu-id="961d5-179">Fill-in hello values in hello tables.</span></span> <span data-ttu-id="961d5-180">這將有助於本教學課程的執行。</span><span class="sxs-lookup"><span data-stu-id="961d5-180">It will be helpful for going through this tutorial.</span></span>

## <a name="define-oozie-workflow-and-hello-related-hiveql-script"></a><span data-ttu-id="961d5-181">定義 Oozie 工作流程和 hello 相關的下列 HiveQL 指令碼</span><span class="sxs-lookup"><span data-stu-id="961d5-181">Define Oozie workflow and hello related HiveQL script</span></span>
<span data-ttu-id="961d5-182">Oozie 工作流程定義會以 hPDL 撰寫 (一種 XML 程序定義語言)。</span><span class="sxs-lookup"><span data-stu-id="961d5-182">Oozie workflows definitions are written in hPDL (an XML process definition language).</span></span> <span data-ttu-id="961d5-183">hello 預設工作流程檔案名稱是*workflow.xml*。</span><span class="sxs-lookup"><span data-stu-id="961d5-183">hello default workflow file name is *workflow.xml*.</span></span>  <span data-ttu-id="961d5-184">您將 hello 工作流程在本機儲存檔案，然後再部署它 toohello HDInsight 叢集稍後在本教學課程使用 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="961d5-184">You will save hello workflow file locally, and then deploy it toohello HDInsight cluster by using Azure PowerShell later in this tutorial.</span></span>

<span data-ttu-id="961d5-185">hello hello 工作流程中的登錄區動作呼叫下列 HiveQL 指令碼檔案。</span><span class="sxs-lookup"><span data-stu-id="961d5-185">hello Hive action in hello workflow calls a HiveQL script file.</span></span> <span data-ttu-id="961d5-186">此指令碼檔案包含三個 HiveQL 陳述式：</span><span class="sxs-lookup"><span data-stu-id="961d5-186">This script file contains three HiveQL statements:</span></span>

1. <span data-ttu-id="961d5-187">**DROP TABLE 陳述式 hello**刪除 hello log4j Hive 資料表，如果存在的話。</span><span class="sxs-lookup"><span data-stu-id="961d5-187">**hello DROP TABLE statement** deletes hello log4j Hive table if it exists.</span></span>
2. <span data-ttu-id="961d5-188">**hello CREATE TABLE 陳述式**建立 log4j Hive 外部資料表，指向 toohello hello log4j 記錄檔的位置。</span><span class="sxs-lookup"><span data-stu-id="961d5-188">**hello CREATE TABLE statement** creates a log4j Hive external table, which points toohello location of hello log4j log file;</span></span>
3. <span data-ttu-id="961d5-189">**hello hello log4j 記錄檔的位置**。</span><span class="sxs-lookup"><span data-stu-id="961d5-189">**hello location of hello log4j log file**.</span></span> <span data-ttu-id="961d5-190">hello 欄位分隔符號是"，"。</span><span class="sxs-lookup"><span data-stu-id="961d5-190">hello field delimiter is ",".</span></span> <span data-ttu-id="961d5-191">hello 預設列的分隔符號是"\n"。</span><span class="sxs-lookup"><span data-stu-id="961d5-191">hello default line delimiter is "\n".</span></span> <span data-ttu-id="961d5-192">Hive 外部資料表是要移除 hello 原始位置，從使用的 tooavoid hello 資料檔，萬一您想要讓 toorun hello Oozie 流程多次。</span><span class="sxs-lookup"><span data-stu-id="961d5-192">A Hive external table is used tooavoid hello data file being removed from hello original location, in case you want toorun hello Oozie workflow multiple times.</span></span>
4. <span data-ttu-id="961d5-193">**hello 插入覆寫陳述式**計算 hello 出現從每個記錄層級型別 hello log4j Hive 資料表，並將儲存 hello 輸出 tooan Azure Blob 儲存體位置。</span><span class="sxs-lookup"><span data-stu-id="961d5-193">**hello INSERT OVERWRITE statement** counts hello occurrences of each log-level type from hello log4j Hive table, and it saves hello output tooan Azure Blob storage location.</span></span>

> [!NOTE]
> <span data-ttu-id="961d5-194">Hive 路徑有已知問題。</span><span class="sxs-lookup"><span data-stu-id="961d5-194">There is a known Hive path issue.</span></span> <span data-ttu-id="961d5-195">此問題會在您提交 Oozie 工作時發生。</span><span class="sxs-lookup"><span data-stu-id="961d5-195">You will run into this problem when submitting an Oozie job.</span></span> <span data-ttu-id="961d5-196">hello 修正 hello 問題可以找到 hello TechNet Wiki 上的指示： [HDInsight Hive 錯誤： 無法 toorename][technetwiki-hive-error]。</span><span class="sxs-lookup"><span data-stu-id="961d5-196">hello instructions for fixing hello issue can be found on hello TechNet Wiki: [HDInsight Hive error: Unable toorename][technetwiki-hive-error].</span></span>

<span data-ttu-id="961d5-197">**toodefine hello 下列 HiveQL 指令碼檔案 toobe 呼叫 hello 工作流程**</span><span class="sxs-lookup"><span data-stu-id="961d5-197">**toodefine hello HiveQL script file toobe called by hello workflow**</span></span>

1. <span data-ttu-id="961d5-198">建立以下列的 hello 文字檔案內容：</span><span class="sxs-lookup"><span data-stu-id="961d5-198">Create a text file with hello following content:</span></span>

        DROP TABLE ${hiveTableName};
        CREATE EXTERNAL TABLE ${hiveTableName}(t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) ROW FORMAT DELIMITED FIELDS TERMINATED BY ' ' STORED AS TEXTFILE LOCATION '${hiveDataFolder}';
        INSERT OVERWRITE DIRECTORY '${hiveOutputFolder}' SELECT t4 AS sev, COUNT(*) AS cnt FROM ${hiveTableName} WHERE t4 LIKE '[%' GROUP BY t4;

    <span data-ttu-id="961d5-199">有三個 hello 指令碼中使用的變數：</span><span class="sxs-lookup"><span data-stu-id="961d5-199">There are three variables used in hello script:</span></span>

   * <span data-ttu-id="961d5-200">${hiveTableName}</span><span class="sxs-lookup"><span data-stu-id="961d5-200">${hiveTableName}</span></span>
   * <span data-ttu-id="961d5-201">${hiveDataFolder}</span><span class="sxs-lookup"><span data-stu-id="961d5-201">${hiveDataFolder}</span></span>
   * <span data-ttu-id="961d5-202">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="961d5-202">${hiveOutputFolder}</span></span>

     <span data-ttu-id="961d5-203">hello 工作流程定義檔 (在本教學課程 workflow.xml) 會在執行階段傳遞這些值 toothis 下列 HiveQL 指令碼。</span><span class="sxs-lookup"><span data-stu-id="961d5-203">hello workflow definition file (workflow.xml in this tutorial) will pass these values toothis HiveQL script at run time.</span></span>
2. <span data-ttu-id="961d5-204">將 hello 檔案儲存為**C:\Tutorials\UseOozie\useooziewf.hql**使用 ANSI (ASCII) 的編碼方式。</span><span class="sxs-lookup"><span data-stu-id="961d5-204">Save hello file as **C:\Tutorials\UseOozie\useooziewf.hql** by using ANSI (ASCII) encoding.</span></span> <span data-ttu-id="961d5-205">(如果您的文字編輯器沒有此選項，請使用「記事本」)。此指令碼檔案會在 hello 教學課程稍後部署的 toohello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="961d5-205">(Use Notepad if your text editor doesn't provide this option.) This script file will be deployed toohello HDInsight cluster later in hello tutorial.</span></span>

<span data-ttu-id="961d5-206">**toodefine 工作流程**</span><span class="sxs-lookup"><span data-stu-id="961d5-206">**toodefine a workflow**</span></span>

1. <span data-ttu-id="961d5-207">建立以下列的 hello 文字檔案內容：</span><span class="sxs-lookup"><span data-stu-id="961d5-207">Create a text file with hello following content:</span></span>

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
    ```

    <span data-ttu-id="961d5-208">有兩個 hello 工作流程中定義的動作。</span><span class="sxs-lookup"><span data-stu-id="961d5-208">There are two actions defined in hello workflow.</span></span> <span data-ttu-id="961d5-209">hello 開始 tooaction 是*RunHiveScript*。</span><span class="sxs-lookup"><span data-stu-id="961d5-209">hello start-tooaction is *RunHiveScript*.</span></span> <span data-ttu-id="961d5-210">如果 hello 動作執行*確定*，hello 下一個動作是*RunSqoopExport*。</span><span class="sxs-lookup"><span data-stu-id="961d5-210">If hello action runs *OK*, hello next action is *RunSqoopExport*.</span></span>

    <span data-ttu-id="961d5-211">hello RunHiveScript 有數個變數。</span><span class="sxs-lookup"><span data-stu-id="961d5-211">hello RunHiveScript has several variables.</span></span> <span data-ttu-id="961d5-212">當您使用 Azure PowerShell 提交從工作站 hello Oozie 作業時，您將會傳遞 hello 值。</span><span class="sxs-lookup"><span data-stu-id="961d5-212">You will pass hello values when you submit hello Oozie job from your workstation by using Azure PowerShell.</span></span>

    <span data-ttu-id="961d5-213">工作流程變數</span><span class="sxs-lookup"><span data-stu-id="961d5-213">Workflow variables</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="961d5-214">工作流程變數</span><span class="sxs-lookup"><span data-stu-id="961d5-214">Workflow variables</span></span></th><th><span data-ttu-id="961d5-215">說明</span><span class="sxs-lookup"><span data-stu-id="961d5-215">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="961d5-216">${jobTracker}</span><span class="sxs-lookup"><span data-stu-id="961d5-216">${jobTracker}</span></span></td><td><span data-ttu-id="961d5-217">指定 hello URL hello Hadoop 作業追蹤程式。</span><span class="sxs-lookup"><span data-stu-id="961d5-217">Specify hello URL of hello Hadoop job tracker.</span></span> <span data-ttu-id="961d5-218">請在 HDInsight 叢集 3.0 和 2.0 版上使用 <strong>jobtrackerhost:9010</strong>。</span><span class="sxs-lookup"><span data-stu-id="961d5-218">Use <strong>jobtrackerhost:9010</strong> on HDInsight cluster version 3.0 and 2.0.</span></span></td></tr>
    <tr><td><span data-ttu-id="961d5-219">${nameNode}</span><span class="sxs-lookup"><span data-stu-id="961d5-219">${nameNode}</span></span></td><td><span data-ttu-id="961d5-220">指定 hello Hadoop 名稱節點 hello URL。</span><span class="sxs-lookup"><span data-stu-id="961d5-220">Specify hello URL of hello Hadoop name node.</span></span> <span data-ttu-id="961d5-221">使用 hello 預設檔案系統 wasb: / / 位址，例如<i>wasb: / /&lt;containerName&gt;@&lt;storageAccountName&gt;。 account>.blob.core.windows.net</i>。</span><span class="sxs-lookup"><span data-stu-id="961d5-221">Use hello default file system wasb:// address, for example, <i>wasb://&lt;containerName&gt;@&lt;storageAccountName&gt;.blob.core.windows.net</i>.</span></span></td></tr>
    <tr><td><span data-ttu-id="961d5-222">${queueName}</span><span class="sxs-lookup"><span data-stu-id="961d5-222">${queueName}</span></span></td><td><span data-ttu-id="961d5-223">指定要送往 hello hello 工作的佇列名稱。</span><span class="sxs-lookup"><span data-stu-id="961d5-223">Specifies hello queue name that hello job will be submitted to.</span></span> <span data-ttu-id="961d5-224">使用<strong>預設值</strong>。</span><span class="sxs-lookup"><span data-stu-id="961d5-224">Use <strong>default</strong>.</span></span></td></tr>
    </table>

    <span data-ttu-id="961d5-225">Hive 動作變數</span><span class="sxs-lookup"><span data-stu-id="961d5-225">Hive action variables</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="961d5-226">Hive 動作變數</span><span class="sxs-lookup"><span data-stu-id="961d5-226">Hive action variable</span></span></th><th><span data-ttu-id="961d5-227">說明</span><span class="sxs-lookup"><span data-stu-id="961d5-227">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="961d5-228">${hiveDataFolder}</span><span class="sxs-lookup"><span data-stu-id="961d5-228">${hiveDataFolder}</span></span></td><td><span data-ttu-id="961d5-229">hello hello Hive Create Table 命令的來源目錄。</span><span class="sxs-lookup"><span data-stu-id="961d5-229">hello source directory for hello Hive Create Table command.</span></span></td></tr>
    <tr><td><span data-ttu-id="961d5-230">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="961d5-230">${hiveOutputFolder}</span></span></td><td><span data-ttu-id="961d5-231">hello hello 插入覆寫陳述式的輸出資料夾。</span><span class="sxs-lookup"><span data-stu-id="961d5-231">hello output folder for hello INSERT OVERWRITE statement.</span></span></td></tr>
    <tr><td><span data-ttu-id="961d5-232">${hiveTableName}</span><span class="sxs-lookup"><span data-stu-id="961d5-232">${hiveTableName}</span></span></td><td><span data-ttu-id="961d5-233">hello hello Hive 資料表參考 hello log4j 資料檔案的名稱。</span><span class="sxs-lookup"><span data-stu-id="961d5-233">hello name of hello Hive table that references hello log4j data files.</span></span></td></tr>
    </table>

    <span data-ttu-id="961d5-234">Sqoop 動作變數</span><span class="sxs-lookup"><span data-stu-id="961d5-234">Sqoop action variables</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="961d5-235">Sqoop 動作變數</span><span class="sxs-lookup"><span data-stu-id="961d5-235">Sqoop action variable</span></span></th><th><span data-ttu-id="961d5-236">說明</span><span class="sxs-lookup"><span data-stu-id="961d5-236">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="961d5-237">${sqlDatabaseConnectionString}</span><span class="sxs-lookup"><span data-stu-id="961d5-237">${sqlDatabaseConnectionString}</span></span></td><td><span data-ttu-id="961d5-238">SQL Database 連接字串。</span><span class="sxs-lookup"><span data-stu-id="961d5-238">SQL Database connection string.</span></span></td></tr>
    <tr><td><span data-ttu-id="961d5-239">${sqlDatabaseTableName}</span><span class="sxs-lookup"><span data-stu-id="961d5-239">${sqlDatabaseTableName}</span></span></td><td><span data-ttu-id="961d5-240">將匯出 hello Azure SQL 資料庫資料表 toowhere hello 資料。</span><span class="sxs-lookup"><span data-stu-id="961d5-240">hello Azure SQL database table toowhere hello data will be exported.</span></span></td></tr>
    <tr><td><span data-ttu-id="961d5-241">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="961d5-241">${hiveOutputFolder}</span></span></td><td><span data-ttu-id="961d5-242">hello hello hive 控制檔插入覆寫陳述式的輸出資料夾。</span><span class="sxs-lookup"><span data-stu-id="961d5-242">hello output folder for hello Hive INSERT OVERWRITE statement.</span></span> <span data-ttu-id="961d5-243">這是 hello hello Sqoop 匯出 (匯出 dir) 相同的資料夾。</span><span class="sxs-lookup"><span data-stu-id="961d5-243">This is hello same folder for hello Sqoop export (export-dir).</span></span></td></tr>
    </table>

    <span data-ttu-id="961d5-244">如需 Oozie 工作流程，並使用 hello 工作流程動作的詳細資訊，請參閱[Apache Oozie 4.0 版文件][ apache-oozie-400] （適用於 HDInsight 叢集版本 3.0） 或[Apache Oozie 3.3.2文件][ apache-oozie-332] （適用於 HDInsight 叢集版本 2.1）。</span><span class="sxs-lookup"><span data-stu-id="961d5-244">For more information about Oozie workflow and using hello workflow actions, see [Apache Oozie 4.0 documentation][apache-oozie-400] (for HDInsight cluster version 3.0) or [Apache Oozie 3.3.2 documentation][apache-oozie-332] (for HDInsight cluster version 2.1).</span></span>

1. <span data-ttu-id="961d5-245">將 hello 檔案儲存為**C:\Tutorials\UseOozie\workflow.xml**使用 ANSI (ASCII) 的編碼方式。</span><span class="sxs-lookup"><span data-stu-id="961d5-245">Save hello file as **C:\Tutorials\UseOozie\workflow.xml** by using ANSI (ASCII) encoding.</span></span> <span data-ttu-id="961d5-246">(如果您的文字編輯器沒有此選項，請使用「記事本」)。</span><span class="sxs-lookup"><span data-stu-id="961d5-246">(Use Notepad if your text editor doesn't provide this option.)</span></span>

<span data-ttu-id="961d5-247">**toodefine 協調器**</span><span class="sxs-lookup"><span data-stu-id="961d5-247">**toodefine coordinator**</span></span>

1. <span data-ttu-id="961d5-248">建立以下列的 hello 文字檔案內容：</span><span class="sxs-lookup"><span data-stu-id="961d5-248">Create a text file with hello following content:</span></span>

    ```xml
    <coordinator-app name="my_coord_app" frequency="${coordFrequency}" start="${coordStart}" end="${coordEnd}" timezone="${coordTimezone}" xmlns="uri:oozie:coordinator:0.4">
        <action>
            <workflow>
                <app-path>${wfPath}</app-path>
            </workflow>
        </action>
    </coordinator-app>
    ```

    <span data-ttu-id="961d5-249">有五個 hello 定義檔中所使用的變數：</span><span class="sxs-lookup"><span data-stu-id="961d5-249">There are five variables used in hello definition file:</span></span>

   | <span data-ttu-id="961d5-250">變數</span><span class="sxs-lookup"><span data-stu-id="961d5-250">Variable</span></span> | <span data-ttu-id="961d5-251">說明</span><span class="sxs-lookup"><span data-stu-id="961d5-251">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="961d5-252">${coordFrequency}</span><span class="sxs-lookup"><span data-stu-id="961d5-252">${coordFrequency}</span></span> |<span data-ttu-id="961d5-253">工作暫停時間。</span><span class="sxs-lookup"><span data-stu-id="961d5-253">Job pause time.</span></span> <span data-ttu-id="961d5-254">頻率一律以分鐘表示。</span><span class="sxs-lookup"><span data-stu-id="961d5-254">Frequency is always expressed in minutes.</span></span> |
   | <span data-ttu-id="961d5-255">${coordStart}</span><span class="sxs-lookup"><span data-stu-id="961d5-255">${coordStart}</span></span> |<span data-ttu-id="961d5-256">工作開始時間。</span><span class="sxs-lookup"><span data-stu-id="961d5-256">Job start time.</span></span> |
   | <span data-ttu-id="961d5-257">${coordEnd}</span><span class="sxs-lookup"><span data-stu-id="961d5-257">${coordEnd}</span></span> |<span data-ttu-id="961d5-258">工作結束時間。</span><span class="sxs-lookup"><span data-stu-id="961d5-258">Job end time.</span></span> |
   | <span data-ttu-id="961d5-259">${coordTimezone}</span><span class="sxs-lookup"><span data-stu-id="961d5-259">${coordTimezone}</span></span> |<span data-ttu-id="961d5-260">Oozie 在固定時區處理協調器工作，不受日光節約時間影響 (通常使用 UTC 表示)。</span><span class="sxs-lookup"><span data-stu-id="961d5-260">Oozie processes coordinator jobs in a fixed time zone with no daylight saving time (typically represented by using UTC).</span></span> <span data-ttu-id="961d5-261">這個時區稱為 hello"Oozie 處理 timezone。 」</span><span class="sxs-lookup"><span data-stu-id="961d5-261">This time zone is referred as hello "Oozie processing timezone."</span></span> |
   | <span data-ttu-id="961d5-262">${wfPath}</span><span class="sxs-lookup"><span data-stu-id="961d5-262">${wfPath}</span></span> |<span data-ttu-id="961d5-263">hello workflow.xml hello 路徑。</span><span class="sxs-lookup"><span data-stu-id="961d5-263">hello path for hello workflow.xml.</span></span>  <span data-ttu-id="961d5-264">如果 hello 工作流程檔案名稱不是 hello 預設檔名 (workflow.xml)，您必須指定它。</span><span class="sxs-lookup"><span data-stu-id="961d5-264">If hello workflow file name is not hello default file name (workflow.xml), you must specify it.</span></span> |
2. <span data-ttu-id="961d5-265">將 hello 檔案儲存為**C:\Tutorials\UseOozie\coordinator.xml**使用 hello ANSI (ASCII) 的編碼方式。</span><span class="sxs-lookup"><span data-stu-id="961d5-265">Save hello file as **C:\Tutorials\UseOozie\coordinator.xml** by using hello ANSI (ASCII) encoding.</span></span> <span data-ttu-id="961d5-266">(如果您的文字編輯器沒有此選項，請使用「記事本」)。</span><span class="sxs-lookup"><span data-stu-id="961d5-266">(Use Notepad if your text editor doesn't provide this option.)</span></span>

## <a name="deploy-hello-oozie-project-and-prepare-hello-tutorial"></a><span data-ttu-id="961d5-267">部署 hello Oozie 專案，並準備 hello 教學課程</span><span class="sxs-lookup"><span data-stu-id="961d5-267">Deploy hello Oozie project and prepare hello tutorial</span></span>
<span data-ttu-id="961d5-268">您將會執行 Azure PowerShell 指令碼 tooperform hello 下列：</span><span class="sxs-lookup"><span data-stu-id="961d5-268">You will run an Azure PowerShell script tooperform hello following:</span></span>

* <span data-ttu-id="961d5-269">複製 hello 下列 HiveQL 指令碼 (useoozie.hql) tooAzure Blob 儲存體，wasb:///tutorials/useoozie/useoozie.hql。</span><span class="sxs-lookup"><span data-stu-id="961d5-269">Copy hello HiveQL script (useoozie.hql) tooAzure Blob storage, wasb:///tutorials/useoozie/useoozie.hql.</span></span>
* <span data-ttu-id="961d5-270">將複製 workflow.xml toowasb:///tutorials/useoozie/workflow.xml。</span><span class="sxs-lookup"><span data-stu-id="961d5-270">Copy workflow.xml toowasb:///tutorials/useoozie/workflow.xml.</span></span>
* <span data-ttu-id="961d5-271">將複製 coordinator.xml toowasb:///tutorials/useoozie/coordinator.xml。</span><span class="sxs-lookup"><span data-stu-id="961d5-271">Copy coordinator.xml toowasb:///tutorials/useoozie/coordinator.xml.</span></span>
* <span data-ttu-id="961d5-272">複製 hello 資料檔 (/ example/data/sample.log) toowasb:///tutorials/useoozie/data/sample.log。</span><span class="sxs-lookup"><span data-stu-id="961d5-272">Copy hello data file (/example/data/sample.log) toowasb:///tutorials/useoozie/data/sample.log.</span></span>
* <span data-ttu-id="961d5-273">建立用於儲存 Sqoop 匯出資料的 Azure SQL Database 資料表。</span><span class="sxs-lookup"><span data-stu-id="961d5-273">Create an Azure SQL database table for storing Sqoop export data.</span></span> <span data-ttu-id="961d5-274">hello 資料表名稱是*log4jLogCount*。</span><span class="sxs-lookup"><span data-stu-id="961d5-274">hello table name is *log4jLogCount*.</span></span>

<span data-ttu-id="961d5-275">**了解 HDInsight 儲存體**</span><span class="sxs-lookup"><span data-stu-id="961d5-275">**Understand HDInsight storage**</span></span>

<span data-ttu-id="961d5-276">HDInsight 使用 Azure Blob 儲存體來儲存資料。</span><span class="sxs-lookup"><span data-stu-id="961d5-276">HDInsight uses Azure Blob storage for data storage.</span></span> <span data-ttu-id="961d5-277">wasb: / / 是 Microsoft 的 hello Hadoop 分散式檔案系統 (HDFS) Azure Blob 儲存體中的實作。</span><span class="sxs-lookup"><span data-stu-id="961d5-277">wasb:// is Microsoft's implementation of hello Hadoop distributed file system (HDFS) in Azure Blob storage.</span></span> <span data-ttu-id="961d5-278">如需詳細資訊，請參閱[搭配 HDInsight 使用 Azure Blob 儲存體][hdinsight-storage]。</span><span class="sxs-lookup"><span data-stu-id="961d5-278">For more information, see [Use Azure Blob storage with HDInsight][hdinsight-storage].</span></span>

<span data-ttu-id="961d5-279">當您佈建的 HDInsight 叢集時，Azure Blob 儲存體帳戶和特定的容器，從該帳戶指定為 hello 預設的檔案系統，例如 HDFS 中。</span><span class="sxs-lookup"><span data-stu-id="961d5-279">When you provision an HDInsight cluster, an Azure Blob storage account and a specific container from that account is designated as hello default file system, like in HDFS.</span></span> <span data-ttu-id="961d5-280">此外 toothis 儲存體帳戶，您可以加入額外的儲存體帳戶從 hello 相同 Azure 訂用帳戶或從不同的 Azure 訂閱 hello 佈建程序期間。</span><span class="sxs-lookup"><span data-stu-id="961d5-280">In addition toothis storage account, you can add additional storage accounts from hello same Azure subscription or from different Azure subscriptions during hello provisioning process.</span></span> <span data-ttu-id="961d5-281">如需關於新增其他儲存體帳戶的指示，請參閱[佈建 HDInsight 叢集][hdinsight-provision]。</span><span class="sxs-lookup"><span data-stu-id="961d5-281">For instructions about adding additional storage accounts, see [Provision HDInsight clusters][hdinsight-provision].</span></span> <span data-ttu-id="961d5-282">toosimplify hello Azure PowerShell 指令碼用在此教學課程中，所有的檔案儲存在 hello 預設檔案系統容器中的 hello 位於*/教學課程/useoozie*。</span><span class="sxs-lookup"><span data-stu-id="961d5-282">toosimplify hello Azure PowerShell script used in this tutorial, all of hello files are stored in hello default file system container located at */tutorials/useoozie*.</span></span> <span data-ttu-id="961d5-283">根據預設，此容器擁有的 hello 名稱做為 hello HDInsight 叢集名稱相同。</span><span class="sxs-lookup"><span data-stu-id="961d5-283">By default, this container has hello same name as hello HDInsight cluster name.</span></span>
<span data-ttu-id="961d5-284">hello 語法為：</span><span class="sxs-lookup"><span data-stu-id="961d5-284">hello syntax is:</span></span>

    wasb[s]://<ContainerName>@<StorageAccountName>.blob.core.windows.net/<path>/<filename>

> [!NOTE]
> <span data-ttu-id="961d5-285">只有 hello *wasb: / /*在 HDInsight 叢集版本 3.0 支援語法。</span><span class="sxs-lookup"><span data-stu-id="961d5-285">Only hello *wasb://* syntax is supported in HDInsight cluster version 3.0.</span></span> <span data-ttu-id="961d5-286">較舊的 hello *asv: / /*語法支援 HDInsight 2.1 和 1.6 的叢集，但它不支援 HDInsight 3.0 叢集。</span><span class="sxs-lookup"><span data-stu-id="961d5-286">hello older *asv://* syntax is supported in HDInsight 2.1 and 1.6 clusters, but it is not supported in HDInsight 3.0 clusters.</span></span>
>
> <span data-ttu-id="961d5-287">hello wasb: / / 是虛擬路徑。</span><span class="sxs-lookup"><span data-stu-id="961d5-287">hello wasb:// path is a virtual path.</span></span> <span data-ttu-id="961d5-288">如需詳細資訊，請參閱[搭配 HDInsight 使用 Azure Blob 儲存體][hdinsight-storage]。</span><span class="sxs-lookup"><span data-stu-id="961d5-288">For more information see [Use Azure Blob storage with HDInsight][hdinsight-storage].</span></span>

<span data-ttu-id="961d5-289">可以使用任何 hello 下列的 Uri （我使用 workflow.xml 做為範例），從 HDInsight 存取儲存在 hello 預設檔案系統容器中的檔案：</span><span class="sxs-lookup"><span data-stu-id="961d5-289">A file that is stored in hello default file system container can be accessed from HDInsight by using any of hello following URIs (I am using workflow.xml as an example):</span></span>

    wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie/workflow.xml
    wasb:///tutorials/useoozie/workflow.xml
    /tutorials/useoozie/workflow.xml

<span data-ttu-id="961d5-290">如果您想直接從 hello 儲存體帳戶的 tooaccess hello 檔案，hello hello 檔案的 blob 名稱是：</span><span class="sxs-lookup"><span data-stu-id="961d5-290">If you want tooaccess hello file directly from hello storage account, hello blob name for hello file is:</span></span>

    tutorials/useoozie/workflow.xml

<span data-ttu-id="961d5-291">**了解 Hive 內部和外部資料表**</span><span class="sxs-lookup"><span data-stu-id="961d5-291">**Understand Hive internal and external tables**</span></span>

<span data-ttu-id="961d5-292">有幾件事，您需要 tooknow Hive 內部和外部資料表的相關：</span><span class="sxs-lookup"><span data-stu-id="961d5-292">There are a few things you need tooknow about Hive internal and external tables:</span></span>

* <span data-ttu-id="961d5-293">hello CREATE TABLE 命令會建立內部資料表中，也稱為受管理的資料表。</span><span class="sxs-lookup"><span data-stu-id="961d5-293">hello CREATE TABLE command creates an internal table, also known as a managed table.</span></span> <span data-ttu-id="961d5-294">hello 資料檔必須位於 hello 預設容器。</span><span class="sxs-lookup"><span data-stu-id="961d5-294">hello data file must be located in hello default container.</span></span>
* <span data-ttu-id="961d5-295">hello CREATE TABLE 命令移動 hello 資料檔案toohello/hive/倉儲/<TableName> hello 預設容器中的資料夾。</span><span class="sxs-lookup"><span data-stu-id="961d5-295">hello CREATE TABLE command moves hello data file toohello /hive/warehouse/<TableName> folder in hello default container.</span></span>
* <span data-ttu-id="961d5-296">hello CREATE EXTERNAL TABLE 命令會建立外部資料表。</span><span class="sxs-lookup"><span data-stu-id="961d5-296">hello CREATE EXTERNAL TABLE command creates an external table.</span></span> <span data-ttu-id="961d5-297">hello 資料檔案可以位於外部 hello 預設容器。</span><span class="sxs-lookup"><span data-stu-id="961d5-297">hello data file can be located outside hello default container.</span></span>
* <span data-ttu-id="961d5-298">hello CREATE EXTERNAL TABLE 命令不會移動 hello 資料檔案。</span><span class="sxs-lookup"><span data-stu-id="961d5-298">hello CREATE EXTERNAL TABLE command does not move hello data file.</span></span>
* <span data-ttu-id="961d5-299">hello CREATE EXTERNAL TABLE 命令不允許 hello 位置子句中指定的 hello 資料夾下的任何子資料夾。</span><span class="sxs-lookup"><span data-stu-id="961d5-299">hello CREATE EXTERNAL TABLE command doesn't allow any subfolders under hello folder that is specified in hello LOCATION clause.</span></span> <span data-ttu-id="961d5-300">這是為什麼 hello 教學課程會建立一份 hello sample.log 檔案 hello 原因。</span><span class="sxs-lookup"><span data-stu-id="961d5-300">This is hello reason why hello tutorial makes a copy of hello sample.log file.</span></span>

<span data-ttu-id="961d5-301">如需詳細資訊，請參閱 [HDInsight：Hive 內部和外部資料表簡介][cindygross-hive-tables]。</span><span class="sxs-lookup"><span data-stu-id="961d5-301">For more information, see [HDInsight: Hive Internal and External Tables Intro][cindygross-hive-tables].</span></span>

<span data-ttu-id="961d5-302">**tooprepare hello 教學課程**</span><span class="sxs-lookup"><span data-stu-id="961d5-302">**tooprepare hello tutorial**</span></span>

1. <span data-ttu-id="961d5-303">開啟 hello Windows PowerShell ISE (在 hello Windows 8 開始 畫面中，輸入**PowerShell_ISE**，然後按一下 **Windows PowerShell ISE**。</span><span class="sxs-lookup"><span data-stu-id="961d5-303">Open hello Windows PowerShell ISE (in hello Windows 8 Start screen, type **PowerShell_ISE**, and then click **Windows PowerShell ISE**.</span></span> <span data-ttu-id="961d5-304">如需詳細資訊，請參閱[在 Windows 8 和 Windows 上啟動 Windows PowerShell][powershell-start])。</span><span class="sxs-lookup"><span data-stu-id="961d5-304">For more information, see [Start Windows PowerShell on Windows 8 and Windows][powershell-start]).</span></span>
2. <span data-ttu-id="961d5-305">在 hello 底部窗格中，執行下列命令 tooconnect tooyour Azure 訂用帳戶的 hello:</span><span class="sxs-lookup"><span data-stu-id="961d5-305">In hello bottom pane, run hello following command tooconnect tooyour Azure subscription:</span></span>

    ```powershell
    Add-AzureAccount
    ```

    <span data-ttu-id="961d5-306">您將會提示的 tooenter 您的 Azure 帳戶的認證。</span><span class="sxs-lookup"><span data-stu-id="961d5-306">You will be prompted tooenter your Azure account credentials.</span></span> <span data-ttu-id="961d5-307">此方法加入訂用帳戶連接的逾時和 12 小時之後，您就會再次具有 toorun hello cmdlet。</span><span class="sxs-lookup"><span data-stu-id="961d5-307">This method of adding a subscription connection times out, and after 12 hours, you will have toorun hello cmdlet again.</span></span>

   > [!NOTE]
   > <span data-ttu-id="961d5-308">如果您有多個 Azure 訂閱 hello 預設訂用帳戶不是您想要 toouse hello，請使用 hello <strong>Select-azuresubscription</strong> cmdlet tooselect 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="961d5-308">If you have multiple Azure subscriptions and hello default subscription is not hello one you want toouse, use hello <strong>Select-AzureSubscription</strong> cmdlet tooselect a subscription.</span></span>

3. <span data-ttu-id="961d5-309">複製 hello 到 hello 指令碼窗格中，下列指令碼，然後設定 hello 前六個變數：</span><span class="sxs-lookup"><span data-stu-id="961d5-309">Copy hello following script into hello script pane, and then set hello first six variables:</span></span>

    ```powershell
    # WASB variables
    $storageAccountName = "<StorageAccountName>"
    $containerName = "<BlobStorageContainerName>"

    # SQL database variables
    $sqlDatabaseServer = "<SQLDatabaseServerName>"
    $sqlDatabaseLogin = "<SQLDatabaseLoginName>"
    $sqlDatabaseLoginPassword = "SQLDatabaseLoginPassword>"
    $sqlDatabaseName = "<SQLDatabaseName>"
    $sqlDatabaseTableName = "log4jLogsCount"

    # Oozie files for hello tutorial
    $hiveQLScript = "C:\Tutorials\UseOozie\useooziewf.hql"
    $workflowDefinition = "C:\Tutorials\UseOozie\workflow.xml"
    $coordDefinition =  "C:\Tutorials\UseOozie\coordinator.xml"

    # WASB folder for storing hello Oozie tutorial files.
    $destFolder = "tutorials/useoozie"  # Do NOT use hello long path here
    ```

    <span data-ttu-id="961d5-310">如需 hello 變數的詳細描述，請參閱 hello[必要條件](#prerequisites)在本教學課程 > 一節。</span><span class="sxs-lookup"><span data-stu-id="961d5-310">For more descriptions of hello variables, see hello [Prerequisites](#prerequisites) section in this tutorial.</span></span>

4. <span data-ttu-id="961d5-311">附加 hello 遵循 toohello hello 指令碼窗格中的指令碼：</span><span class="sxs-lookup"><span data-stu-id="961d5-311">Append hello following toohello script in hello script pane:</span></span>

    ```powershell
    # Create a storage context object
    $storageaccountkey = get-azurestoragekey $storageAccountName | %{$_.Primary}
    $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageaccountkey

    function uploadOozieFiles()
    {
        Write-Host "Copy HiveQL script, workflow definition and coordinator definition ..." -ForegroundColor Green
        Set-AzureStorageBlobContent -File $hiveQLScript -Container $containerName -Blob "$destFolder/useooziewf.hql" -Context $destContext
        Set-AzureStorageBlobContent -File $workflowDefinition -Container $containerName -Blob "$destFolder/workflow.xml" -Context $destContext
        Set-AzureStorageBlobContent -File $coordDefinition -Container $containerName -Blob "$destFolder/coordinator.xml" -Context $destContext
    }

    function prepareHiveDataFile()
    {
        Write-Host "Make a copy of hello sample.log file ... " -ForegroundColor Green
        Start-CopyAzureStorageBlob -SrcContainer $containerName -SrcBlob "example/data/sample.log" -Context $destContext -DestContainer $containerName -destBlob "$destFolder/data/sample.log" -DestContext $destContext
    }

    function prepareSQLDatabase()
    {
        # SQL query string for creating log4jLogsCount table
        $cmdCreateLog4jCountTable = " CREATE TABLE [dbo].[$sqlDatabaseTableName](
                [Level] [nvarchar](10) NOT NULL,
                [Total] float,
            CONSTRAINT [PK_$sqlDatabaseTableName] PRIMARY KEY CLUSTERED
            (
            [Level] ASC
            )
            )"

        #Create hello log4jLogsCount table
        Write-Host "Create Log4jLogsCount table ..." -ForegroundColor Green
        $conn = New-Object System.Data.SqlClient.SqlConnection
        $conn.ConnectionString = "Data Source=$sqlDatabaseServer.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabaseLoginPassword;Encrypt=true;Trusted_Connection=false;"
        $conn.open()
        $cmd = New-Object System.Data.SqlClient.SqlCommand
        $cmd.connection = $conn
        $cmd.commandtext = $cmdCreateLog4jCountTable
        $cmd.executenonquery()

        $conn.close()
    }

    # upload workflow.xml, coordinator.xml, and ooziewf.hql
    uploadOozieFiles;

    # make a copy of example/data/sample.log tooexample/data/log4j/sample.log
    prepareHiveDataFile;

    # create log4jlogsCount table on SQL database
    prepareSQLDatabase;
    ```

5. <span data-ttu-id="961d5-312">按一下**執行指令碼**或按**F5** toorun hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="961d5-312">Click **Run Script** or press **F5** toorun hello script.</span></span> <span data-ttu-id="961d5-313">hello 輸出將會類似於：</span><span class="sxs-lookup"><span data-stu-id="961d5-313">hello output will be similar to:</span></span>

    ![Tutorial preparation output][img-preparation-output]

## <a name="run-hello-oozie-project"></a><span data-ttu-id="961d5-315">執行 hello Oozie 專案</span><span class="sxs-lookup"><span data-stu-id="961d5-315">Run hello Oozie project</span></span>
<span data-ttu-id="961d5-316">Azure PowerShell 目前並未提供任何用以定義 Oozie 工作的 Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="961d5-316">Azure PowerShell currently doesn't provide any cmdlets for defining Oozie jobs.</span></span> <span data-ttu-id="961d5-317">您可以使用 hello **Invoke-restmethod** cmdlet tooinvoke Oozie web 服務。</span><span class="sxs-lookup"><span data-stu-id="961d5-317">You can use hello **Invoke-RestMethod** cmdlet tooinvoke Oozie web services.</span></span> <span data-ttu-id="961d5-318">hello Oozie web 服務應用程式開發介面是 HTTP REST JSON API。</span><span class="sxs-lookup"><span data-stu-id="961d5-318">hello Oozie web services API is a HTTP REST JSON API.</span></span> <span data-ttu-id="961d5-319">如需 hello Oozie web 服務應用程式開發介面的詳細資訊，請參閱[Apache Oozie 4.0 版文件][ apache-oozie-400] （適用於 HDInsight 叢集版本 3.0） 或[Apache Oozie 3.3.2 文件] [ apache-oozie-332] （適用於 HDInsight 叢集版本 2.1）。</span><span class="sxs-lookup"><span data-stu-id="961d5-319">For more information about hello Oozie web services API, see [Apache Oozie 4.0 documentation][apache-oozie-400] (for HDInsight cluster version 3.0) or [Apache Oozie 3.3.2 documentation][apache-oozie-332] (for HDInsight cluster version 2.1).</span></span>

<span data-ttu-id="961d5-320">**toosubmit Oozie 工作**</span><span class="sxs-lookup"><span data-stu-id="961d5-320">**toosubmit an Oozie job**</span></span>

1. <span data-ttu-id="961d5-321">開啟 hello Windows PowerShell ISE (在 Windows 8 [開始] 畫面中，輸入**PowerShell_ISE**，然後按一下 **Windows PowerShell ISE**。</span><span class="sxs-lookup"><span data-stu-id="961d5-321">Open hello Windows PowerShell ISE (in Windows 8 Start screen, type **PowerShell_ISE**, and then click **Windows PowerShell ISE**.</span></span> <span data-ttu-id="961d5-322">如需詳細資訊，請參閱[在 Windows 8 和 Windows 上啟動 Windows PowerShell][powershell-start])。</span><span class="sxs-lookup"><span data-stu-id="961d5-322">For more information, see [Start Windows PowerShell on Windows 8 and Windows][powershell-start]).</span></span>
2. <span data-ttu-id="961d5-323">複製 hello 下列指令碼到 hello 指令碼窗格中，並設定然後 hello 先 14 個變數 (不過，請略過**$storageUri**)。</span><span class="sxs-lookup"><span data-stu-id="961d5-323">Copy hello following script into hello script pane, and then set hello first fourteen variables (however, skip **$storageUri**).</span></span>

    ```powershell
    #HDInsight cluster variables
    $clusterName = "<HDInsightClusterName>"
    $clusterUsername = "<HDInsightClusterUsername>"
    $clusterPassword = "<HDInsightClusterUserPassword>"

    #Azure Blob storage (WASB) variables
    $storageAccountName = "<StorageAccountName>"
    $storageContainerName = "<BlobContainerName>"
    $storageUri="wasb://$storageContainerName@$storageAccountName.blob.core.windows.net"

    #Azure SQL database variables
    $sqlDatabaseServer = "<SQLDatabaseServerName>"
    $sqlDatabaseLogin = "<SQLDatabaseLoginName>"
    $sqlDatabaseLoginPassword = "<SQLDatabaseloginPassword>"
    $sqlDatabaseName = "<SQLDatabaseName>"

    #Oozie WF/coordinator variables
    $coordStart = "2014-03-21T13:45Z"
    $coordEnd = "2014-03-21T13:45Z"
    $coordFrequency = "1440"    # in minutes, 24h x 60m = 1440m
    $coordTimezone = "UTC"    #UTC/GMT

    $oozieWFPath="$storageUri/tutorials/useoozie"  # hello default name is workflow.xml. And you don't need toospecify hello file name.
    $waitTimeBetweenOozieJobStatusCheck=10

    #Hive action variables
    $hiveScript = "$storageUri/tutorials/useoozie/useooziewf.hql"
    $hiveTableName = "log4jlogs"
    $hiveDataFolder = "$storageUri/tutorials/useoozie/data"
    $hiveOutputFolder = "$storageUri/tutorials/useoozie/output"

    #Sqoop action variables
    $sqlDatabaseConnectionString = "jdbc:sqlserver://$sqlDatabaseServer.database.windows.net;user=$sqlDatabaseLogin@$sqlDatabaseServer;password=$sqlDatabaseLoginPassword;database=$sqlDatabaseName"
    $sqlDatabaseTableName = "log4jLogsCount"

    $passwd = ConvertTo-SecureString $clusterPassword -AsPlainText -Force
    $creds = New-Object System.Management.Automation.PSCredential ($clusterUsername, $passwd)
    ```

    <span data-ttu-id="961d5-324">如需 hello 變數的詳細描述，請參閱 hello[必要條件](#prerequisites)在本教學課程 > 一節。</span><span class="sxs-lookup"><span data-stu-id="961d5-324">For more descriptions of hello variables, see hello [Prerequisites](#prerequisites) section in this tutorial.</span></span>

    <span data-ttu-id="961d5-325">$coordstart 和 $coordend 是 hello 工作流程開始和結束時間。</span><span class="sxs-lookup"><span data-stu-id="961d5-325">$coordstart and $coordend are hello workflow starting and ending time.</span></span> <span data-ttu-id="961d5-326">toofind hello UTC/GMT 時間，搜尋 bing.com 的 「 utc 時間 」。hello $coordFrequency 頻率為您想要讓 toorun hello 流程分鐘。</span><span class="sxs-lookup"><span data-stu-id="961d5-326">toofind out hello UTC/GMT time, search "utc time" on bing.com. hello $coordFrequency is how often in minutes you want toorun hello workflow.</span></span>
3. <span data-ttu-id="961d5-327">附加 hello 遵循 toohello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="961d5-327">Append hello following toohello script.</span></span> <span data-ttu-id="961d5-328">此組件定義 hello Oozie 裝載：</span><span class="sxs-lookup"><span data-stu-id="961d5-328">This part defines hello Oozie payload:</span></span>

    ```powershell
    #OoziePayload used for Oozie web service submission
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
            <name>oozie.coord.application.path</name>
            <value>$oozieWFPath</value>
        </property>

        <property>
            <name>wfPath</name>
            <value>$oozieWFPath</value>
        </property>

        <property>
            <name>coordStart</name>
            <value>$coordStart</value>
        </property>

        <property>
            <name>coordEnd</name>
            <value>$coordEnd</value>
        </property>

        <property>
            <name>coordFrequency</name>
            <value>$coordFrequency</value>
        </property>

        <property>
            <name>coordTimezone</name>
            <value>$coordTimezone</value>
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
            <value>admin</value>
        </property>

    </configuration>
    "@
    ```

   > [!NOTE]
   > <span data-ttu-id="961d5-329">hello 主要的差異比較 toohello 工作流程提交裝載檔案是 hello 變數**oozie.coord.application.path**。</span><span class="sxs-lookup"><span data-stu-id="961d5-329">hello major difference compared toohello workflow submission payload file is hello variable **oozie.coord.application.path**.</span></span> <span data-ttu-id="961d5-330">提交工作流程工作時，您必須改用 **oozie.wf.application.path** 。</span><span class="sxs-lookup"><span data-stu-id="961d5-330">When you submit a workflow job, you use **oozie.wf.application.path** instead.</span></span>

4. <span data-ttu-id="961d5-331">附加 hello 遵循 toohello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="961d5-331">Append hello following toohello script.</span></span> <span data-ttu-id="961d5-332">此組件會檢查 hello Oozie web 服務狀態：</span><span class="sxs-lookup"><span data-stu-id="961d5-332">This part checks hello Oozie web service status:</span></span>

    ```powershell
    function checkOozieServerStatus()
    {
        Write-Host "Checking Oozie server status..." -ForegroundColor Green
        $clusterUriStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/admin/status"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriStatus -Credential $creds -OutVariable $OozieServerStatus

        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $oozieServerSatus = $jsonResponse[0].("systemMode")
        Write-Host "Oozie server status is $oozieServerSatus..."

        if($oozieServerSatus -notmatch "NORMAL")
        {
            Write-Host "Oozie server status is $oozieServerSatus...cannot submit Oozie jobs. Check hello server status and re-run hello job."
            exit 1
        }
    }
    ```

5. <span data-ttu-id="961d5-333">附加 hello 遵循 toohello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="961d5-333">Append hello following toohello script.</span></span> <span data-ttu-id="961d5-334">這部分會建立 Oozie 工作：</span><span class="sxs-lookup"><span data-stu-id="961d5-334">This part creates an Oozie job:</span></span>

    ```powershell
    function createOozieJob()
    {
        # create Oozie job
        Write-Host "Sending hello following Payload toohello cluster:" -ForegroundColor Green
        Write-Host "`n--------`n$OoziePayload`n--------"
        $clusterUriCreateJob = "https://$clusterName.azurehdinsight.net:443/oozie/v2/jobs"
        $response = Invoke-RestMethod -Method Post -Uri $clusterUriCreateJob -Credential $creds -Body $OoziePayload -ContentType "application/xml" -OutVariable $OozieJobName -debug -Verbose

        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $oozieJobId = $jsonResponse[0].("id")
        Write-Host "Oozie job id is $oozieJobId..."

        return $oozieJobId
    }
    ```

   > [!NOTE]
   > <span data-ttu-id="961d5-335">當您提交的工作流程工作時，您必須在 hello 工作建立之後，進行另一個 web 服務呼叫 toostart hello 工作。</span><span class="sxs-lookup"><span data-stu-id="961d5-335">When you submit a workflow job, you must make another web service call toostart hello job after hello job is created.</span></span> <span data-ttu-id="961d5-336">在此情況下，依時間觸發 hello 協調器工作。</span><span class="sxs-lookup"><span data-stu-id="961d5-336">In this case, hello coordinator job is triggered by time.</span></span> <span data-ttu-id="961d5-337">hello 作業將自動啟動。</span><span class="sxs-lookup"><span data-stu-id="961d5-337">hello job will start automatically.</span></span>

6. <span data-ttu-id="961d5-338">附加 hello 遵循 toohello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="961d5-338">Append hello following toohello script.</span></span> <span data-ttu-id="961d5-339">此組件會檢查 hello Oozie 工作狀態：</span><span class="sxs-lookup"><span data-stu-id="961d5-339">This part checks hello Oozie job status:</span></span>

    ```powershell
    function checkOozieJobStatus($oozieJobId)
    {
        # get job status
        Write-Host "Sleeping for $waitTimeBetweenOozieJobStatusCheck seconds until hello job metadata is populated in hello Oozie metastore..." -ForegroundColor Green
        Start-Sleep -Seconds $waitTimeBetweenOozieJobStatusCheck

        Write-Host "Getting job status and waiting for hello job toocomplete..." -ForegroundColor Green
        $clusterUriGetJobStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/job/" + $oozieJobId + "?show=info"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriGetJobStatus -Credential $creds
        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $JobStatus = $jsonResponse[0].("status")

        while($JobStatus -notmatch "SUCCEEDED|KILLED")
        {
            Write-Host "$(Get-Date -format 'G'): $oozieJobId is in $JobStatus state...waiting $waitTimeBetweenOozieJobStatusCheck seconds for hello job toocomplete..."
            Start-Sleep -Seconds $waitTimeBetweenOozieJobStatusCheck
            $response = Invoke-RestMethod -Method Get -Uri $clusterUriGetJobStatus -Credential $creds
            $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
            $JobStatus = $jsonResponse[0].("status")
        }

        Write-Host "$(Get-Date -format 'G'): $oozieJobId is in $JobStatus state!"
        if($JobStatus -notmatch "SUCCEEDED")
        {
            Write-Host "Check logs at http://headnode0:9014/cluster for detais."
            exit -1
        }
    }
    ```

7. <span data-ttu-id="961d5-340">（選擇性）附加 hello 遵循 toohello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="961d5-340">(Optional) Append hello following toohello script.</span></span>

    ```powershell
    function listOozieJobs()
    {
        Write-Host "Listing Oozie jobs..." -ForegroundColor Green
        $clusterUriStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/jobs"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriStatus -Credential $creds

        write-host "Job ID                                   App Name        Status      Started                         Ended"
        write-host "----------------------------------------------------------------------------------------------------------------------------------"
        foreach($job in $response.workflows)
        {
            Write-Host $job.id "`t" $job.appName "`t" $job.status "`t" $job.startTime "`t" $job.endTime
        }
    }

    function ShowOozieJobLog($oozieJobId)
    {
        Write-Host "Showing Oozie job info..." -ForegroundColor Green
        $clusterUriStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/job/$oozieJobId" + "?show=log"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriStatus -Credential $creds
        write-host $response
    }

    function killOozieJob($oozieJobId)
    {
        Write-Host "Killing hello Oozie job $oozieJobId..." -ForegroundColor Green
        $clusterUriStartJob = "https://$clusterName.azurehdinsight.net:443/oozie/v2/job/" + $oozieJobId + "?action=kill" #Valid values for hello 'action' parameter are 'start', 'suspend', 'resume', 'kill', 'dryrun', 'rerun', and 'change'.
        $response = Invoke-RestMethod -Method Put -Uri $clusterUriStartJob -Credential $creds | Format-Table -HideTableHeaders -debug
    }
    ```

8. <span data-ttu-id="961d5-341">附加 hello 遵循 toohello 指令碼：</span><span class="sxs-lookup"><span data-stu-id="961d5-341">Append hello following toohello script:</span></span>

    ```powershell
    checkOozieServerStatus
    # listOozieJobs
    $oozieJobId = createOozieJob($oozieJobId)
    checkOozieJobStatus($oozieJobId)
    # ShowOozieJobLog($oozieJobId)
    # killOozieJob($oozieJobId)
    ```

    <span data-ttu-id="961d5-342">如果您想 toorun hello 其他函式，請移除 hello # 符號。</span><span class="sxs-lookup"><span data-stu-id="961d5-342">Remove hello # signs if you want toorun hello additional functions.</span></span>
9. <span data-ttu-id="961d5-343">如果您的 HDinsight 叢集是 2.1 版，請將 "https://$clusterName.azurehdinsight.net:443/oozie/v2/" 取代為 "https://$clusterName.azurehdinsight.net:443/oozie/v1/"。</span><span class="sxs-lookup"><span data-stu-id="961d5-343">If your HDinsight cluster is version 2.1, replace "https://$clusterName.azurehdinsight.net:443/oozie/v2/" with "https://$clusterName.azurehdinsight.net:443/oozie/v1/".</span></span> <span data-ttu-id="961d5-344">HDInsight 叢集版本 2.1 並不支援第 2 版的 hello web 服務。</span><span class="sxs-lookup"><span data-stu-id="961d5-344">HDInsight cluster version 2.1 does not supports version 2 of hello web services.</span></span>
10. <span data-ttu-id="961d5-345">按一下**執行指令碼**或按**F5** toorun hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="961d5-345">Click **Run Script** or press **F5** toorun hello script.</span></span> <span data-ttu-id="961d5-346">hello 輸出將會類似於：</span><span class="sxs-lookup"><span data-stu-id="961d5-346">hello output will be similar to:</span></span>

     ![Tutorial run workflow output][img-runworkflow-output]
11. <span data-ttu-id="961d5-348">連接 tooyour SQL Database toosee hello 匯出資料。</span><span class="sxs-lookup"><span data-stu-id="961d5-348">Connect tooyour SQL Database toosee hello exported data.</span></span>

<span data-ttu-id="961d5-349">**toocheck hello 作業錯誤記錄檔**</span><span class="sxs-lookup"><span data-stu-id="961d5-349">**toocheck hello job error log**</span></span>

<span data-ttu-id="961d5-350">tootroubleshoot 工作流程，hello Oozie 記錄檔可以在找到 C:\apps\dist\oozie-3.3.2.1.3.2.0-05\oozie-win-distro\logs\Oozie.log 從 hello 叢集前端節點。</span><span class="sxs-lookup"><span data-stu-id="961d5-350">tootroubleshoot a workflow, hello Oozie log file can be found at C:\apps\dist\oozie-3.3.2.1.3.2.0-05\oozie-win-distro\logs\Oozie.log from hello cluster headnode.</span></span> <span data-ttu-id="961d5-351">如需 RDP 資訊，請參閱[管理 HDInsight 叢集使用 hello Azure 入口網站][hdinsight-admin-portal]。</span><span class="sxs-lookup"><span data-stu-id="961d5-351">For information on RDP, see [Administering HDInsight clusters using hello Azure portal][hdinsight-admin-portal].</span></span>

<span data-ttu-id="961d5-352">**toorerun hello 教學課程**</span><span class="sxs-lookup"><span data-stu-id="961d5-352">**toorerun hello tutorial**</span></span>

<span data-ttu-id="961d5-353">toorerun hello 工作流程，您必須執行下列工作的 hello:</span><span class="sxs-lookup"><span data-stu-id="961d5-353">toorerun hello workflow, you must perform hello following tasks:</span></span>

* <span data-ttu-id="961d5-354">刪除 hello Hive 指令碼輸出檔。</span><span class="sxs-lookup"><span data-stu-id="961d5-354">Delete hello Hive script output file.</span></span>
* <span data-ttu-id="961d5-355">刪除 hello hello log4jLogsCount 資料表中的資料。</span><span class="sxs-lookup"><span data-stu-id="961d5-355">Delete hello data in hello log4jLogsCount table.</span></span>

<span data-ttu-id="961d5-356">以下是您可使用的範例 Windows PowerShell 指令碼：</span><span class="sxs-lookup"><span data-stu-id="961d5-356">Here is a sample Windows PowerShell script that you can use:</span></span>

```powershell
$storageAccountName = "<AzureStorageAccountName>"
$containerName = "<ContainerName>"

#SQL database variables
$sqlDatabaseServer = "<SQLDatabaseServerName>"
$sqlDatabaseLogin = "<SQLDatabaseLoginName>"
$sqlDatabaseLoginPassword = "<SQLDatabaseLoginPassword>"
$sqlDatabaseName = "<SQLDatabaseName>"
$sqlDatabaseTableName = "log4jLogsCount"

Write-host "Delete hello Hive script output file ..." -ForegroundColor Green
$storageaccountkey = get-azurestoragekey $storageAccountName | %{$_.Primary}
$destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageaccountkey
Remove-AzureStorageBlob -Context $destContext -Blob "tutorials/useoozie/output/000000_0" -Container $containerName

Write-host "Delete all hello records from hello log4jLogsCount table ..." -ForegroundColor Green
$conn = New-Object System.Data.SqlClient.SqlConnection
$conn.ConnectionString = "Data Source=$sqlDatabaseServer.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabaseLoginPassword;Encrypt=true;Trusted_Connection=false;"
$conn.open()
$cmd = New-Object System.Data.SqlClient.SqlCommand
$cmd.connection = $conn
$cmd.commandtext = "delete from $sqlDatabaseTableName"
$cmd.executenonquery()

$conn.close()
```

## <a name="next-steps"></a><span data-ttu-id="961d5-357">後續步驟</span><span class="sxs-lookup"><span data-stu-id="961d5-357">Next steps</span></span>
<span data-ttu-id="961d5-358">在本教學課程中，您學到如何 toodefine Oozie 工作流程和 Oozie 協調器，以及使用 Azure PowerShell toorun Oozie 協調者作業的方式。</span><span class="sxs-lookup"><span data-stu-id="961d5-358">In this tutorial, you learned how toodefine an Oozie workflow and an Oozie coordinator, and how toorun an Oozie coordinator job by using Azure PowerShell.</span></span> <span data-ttu-id="961d5-359">toolearn 詳細資訊，請參閱下列文章 hello:</span><span class="sxs-lookup"><span data-stu-id="961d5-359">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="961d5-360">[開始使用 HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="961d5-360">[Get started with HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="961d5-361">[搭配 HDInsight 使用 Azure Blob 儲存體][hdinsight-storage]</span><span class="sxs-lookup"><span data-stu-id="961d5-361">[Use Azure Blob storage with HDInsight][hdinsight-storage]</span></span>
* <span data-ttu-id="961d5-362">[使用 Azure PowerShell 管理 HDInsight][hdinsight-admin-powershell]</span><span class="sxs-lookup"><span data-stu-id="961d5-362">[Administer HDInsight by using Azure PowerShell][hdinsight-admin-powershell]</span></span>
* <span data-ttu-id="961d5-363">[上傳資料 tooHDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="961d5-363">[Upload data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="961d5-364">[搭配 HDInsight 使用 Sqoop][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="961d5-364">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="961d5-365">[搭配 HDInsight 使用 Hivet][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="961d5-365">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="961d5-366">[搭配 HDInsight 使用 Pig][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="961d5-366">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="961d5-367">[開發 HDInsight 的 Java MapReduce 程式][hdinsight-develop-java-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="961d5-367">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-java-mapreduce]</span></span>

[hdinsight-cmdlets-download]: http://go.microsoft.com/fwlink/?LinkID=325563

[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md

[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-develop-java-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-use-oozie]: hdinsight-use-oozie.md

[sqldatabase-get-started]: ../sql-database/sql-database-get-started.md

[azure-management-portal]: https://portal.azure.com/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md

[apache-hadoop]: http://hadoop.apache.org/
[apache-oozie-400]: http://oozie.apache.org/docs/4.0.0/
[apache-oozie-332]: http://oozie.apache.org/docs/3.3.2/

[powershell-download]: http://azure.microsoft.com/downloads/
[powershell-about-profiles]: http://go.microsoft.com/fwlink/?LinkID=113729
[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-script]: http://technet.microsoft.com/library/ee176949.aspx

[cindygross-hive-tables]: http://blogs.msdn.com/b/cindygross/archive/2013/02/06/hdinsight-hive-internal-and-external-tables-intro.aspx

[img-workflow-diagram]: ./media/hdinsight-use-oozie-coordinator-time/HDI.UseOozie.Workflow.Diagram.png
[img-preparation-output]: ./media/hdinsight-use-oozie-coordinator-time/HDI.UseOozie.Preparation.Output1.png
[img-runworkflow-output]: ./media/hdinsight-use-oozie-coordinator-time/HDI.UseOozie.RunCoord.Output.png

[technetwiki-hive-error]: http://social.technet.microsoft.com/wiki/contents/articles/23047.hdinsight-hive-error-unable-to-rename.aspx
